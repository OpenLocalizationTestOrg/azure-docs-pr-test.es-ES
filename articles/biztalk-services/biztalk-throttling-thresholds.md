---
title: "aaaLearn sobre limitación en servicios de BizTalk | Documentos de Microsoft"
description: "Obtenga información acerca de los umbrales de limitación y comportamientos en tiempo de ejecución resultantes para los Servicios de BizTalk. La limitación se basa en el uso de la memoria y el número de mensajes. MABS, WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: f6663cf2-cda4-4bac-855e-27d2ad5c4fa4
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: 46c8806c3a1f4eeb793f721f849771e0ec155197
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="biztalk-services-throttling"></a>Servicios de BizTalk: limitaciones

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

Servicios de BizTalk de Azure implementa el servicio limitación basada en dos condiciones: número de hello y uso de memoria de mensajes simultáneos que se procesan. Este tema enumeran Hola umbrales de limitación y describe el comportamiento de hello en tiempo de ejecución cuando se produce una condición de limitación.

## <a name="throttling-thresholds"></a>Umbrales de limitación
Hola tabla siguiente se muestran Hola origen limitación y los umbrales:

|  | Descripción | Umbral bajo | Umbral alto |
| --- | --- | --- | --- |
| Memoria |% de memoria total del sistema disponible/PageFileBytes. <p><p>Total PageFileBytes disponible es aproximadamente 2 veces Hola RAM del sistema de Hola. |60% |70% |
| Procesamiento de mensajes |Número de mensajes que se procesan simultáneamente |40 * número de núcleos |100 * número de núcleos |

Cuando se alcanza un umbral alta, servicios de BizTalk de Azure inicia toothrottle. La limitación se detiene cuando se alcanza el umbral inferior Hola. Por ejemplo, el servicio está utilizando un 65 % de la memoria del sistema. En esta situación, no limitar el servicio de Hola. El servicio empieza a usar un 70 % de la memoria del sistema. En esta situación, el servicio de hello limita y continúa toothrottle hasta que el servicio de hello utiliza memoria del sistema de 60% (umbral inferior).

Servicios de BizTalk de Azure realiza un seguimiento de hello duración de limitación y Hola limitación estado (estado normal frente a estado limitada).

## <a name="runtime-behavior"></a>Comportamiento del tiempo de ejecución
Cuando los servicios de BizTalk de Azure entra en un estado de limitación, se produce el siguiente hello:

* La limitación es por instancia de rol. Por ejemplo:<br/>
  RoleInstanceA se está limitando. RoleInstanceB no se está limitando. En esta situación, los mensajes en RoleInstanceB se procesan según lo esperado. Mensajes de RoleInstanceA se descartan y se producirá un error con hello siguiente error:<br/><br/>
  **El servidor está ocupado. Vuelva a intentarlo.**<br/><br/>
* Ningún origen de extracción sondea ni descarga un mensaje. Por ejemplo,<br/>
  una canalización extrae los mensajes desde un origen FTP externo. instancia de rol de Hello realizar la extracción de hello pone en un estado de limitación. En esta situación, detiene el Hola canalización descargar mensajes adicionales hasta que finaliza la instancia de rol de hello limitación.
* Se envía una respuesta toohello cliente para que cliente hello puede volver a enviar los mensajes de bienvenida.
* Debe esperar hasta que se resuelva la limitación de Hola. En concreto, debe esperar hasta que se alcanza el umbral inferior Hola.

## <a name="important-notes"></a>Notas importantes
* La limitación no se puede deshabilitar.
* Los umbrales de limitación no se pueden modificar.
* La limitación está implementada en todo el sistema.
* Hola servidor de base de datos de SQL Azure también tiene la limitación integrados.

## <a name="additional-azure-biztalk-services-topics"></a>Otros temas acerca de los servicios de BizTalk de Azure
* [Hola instalar SDK de servicios de BizTalk de Azure](http://go.microsoft.com/fwlink/p/?LinkID=241589)<br/>
* [Tutoriales: Azure BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=236944)<br/>
* [¿Cómo puedo comenzar a utilizar Hola SDK de servicios de BizTalk de Azure](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>
* [Servicios de BizTalk de Azure](http://go.microsoft.com/fwlink/p/?LinkID=303664)<br/>

## <a name="see-also"></a>Otras referencias
* [Servicios de BizTalk: gráfico de las ediciones Developer, Basic, Standard y Premium](http://go.microsoft.com/fwlink/p/?LinkID=302279)<br/>
* [Servicios de BizTalk: aprovisionamiento con el Portal de Azure clásico](http://go.microsoft.com/fwlink/p/?LinkID=302280)<br/>
* [Servicios de BizTalk: gráfico del estado de aprovisionamiento](http://go.microsoft.com/fwlink/p/?LinkID=329870)<br/>
* [Servicios de BizTalk: pestañas Panel, Monitor y Escala](http://go.microsoft.com/fwlink/p/?LinkID=302281)<br/>
* [Servicios de BizTalk: copias de seguridad y restauración](http://go.microsoft.com/fwlink/p/?LinkID=329873)<br/>
* [Servicios de BizTalk: nombre del emisor y clave del emisor](http://go.microsoft.com/fwlink/p/?LinkID=303941)<br/>

