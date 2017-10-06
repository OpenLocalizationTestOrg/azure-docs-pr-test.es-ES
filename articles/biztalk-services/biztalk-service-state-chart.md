---
title: aaaTasks permitido en diferentes Estados o Estados en servicios de BizTalk | Documentos de Microsoft
description: "Hola acciones/operaciones permitidas en un estado MABS diferente: detener, iniciar, reiniciar, suspender, reanudar, eliminar, escalar, actualizar configuración y copia de seguridad"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: aea738f3-ec76-4099-a41b-e17fea9e252f
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/08/2016
ms.author: mandia
ms.openlocfilehash: 643307ba6fa9b05c82b867912feab249c42b65dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="what-you-can-and-cant-do-using-hello-biztalk-service-state"></a>¿Qué puede y no se puede hacer con hello estado BizTalk Service

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

Según el estado actual de Hola de hello servicio de BizTalk, existen operaciones que puede o no se puede realizar en hello servicio de BizTalk.

Por ejemplo, aprovisiona un nuevo servicio de BizTalk en hello portal de Azure clásico. Cuando se complete correctamente, Hola servicio de BizTalk está en `active` estado. En estado activo de hello, puede detener, suspender y eliminar el servicio de BizTalk de Hola. Si se detiene el servicio de BizTalk de hello y se produce un error de detención, después, Hola servicio de BizTalk continuará tooa `StopFailed` estado. Hola `StopFailed` estado, puede reiniciar el servicio de BizTalk Hola. Si trata de una operación que no está permitida, como la reanudación, se produce Hola siguiente error:

`Operation not allowed`

## <a name="view-hello-possible-states"></a>Hola posibles estados de vista

las tablas siguientes de Hola la lista de operaciones de Hola o las acciones que pueden realizarse una vez Hola BizTalk Service en un estado específico. Un ✔ significa que se permite la operación de hello mientras está en ese estado. Una entrada en blanco significa que no se puede realizar la operación de hello mientras está en ese estado.

| Estado de servicio | Iniciar | Detención | Reinicio | Suspensión | Reanudación | Eliminar | Escala | Actualizar <br/> Configuración | Copia de seguridad |
| --- | --- | --- | --- | --- | --- | --- |--- | --- | --- |
| Active |  | ✔ | ✔ | ✔ |  | ✔ |✔ |✔ |✔ |
| Disabled |  |  |  |  |  | ✔ | |  |  | 
| Suspended |  |  |  |  | ✔ | ✔ | |  | ✔ |
| Stopped | ✔ |  | ✔ |  |  | ✔ | |  | ✔ |
| Service Update Failed |  |  |  |  |  | ✔ | |  |  | 
| DisableFailed |  |  |  |  |  | ✔ | |  |  | 
| EnableFailed |  |  |  |  |  | ✔ | |  |  | 
| StartFailed <br/> StopFailed <br/> RestartFailed | ✔ | ✔ | ✔ |  |  | ✔ | | ✔ | |
| SuspendedFailed <br/> ResumeFailed|  |  |  | ✔ | ✔ | ✔ | |  |  | 
| CreatedFailed <br/> RestoreFailed |  |  |  |  |  | ✔ | |  |  | 
| ConfigUpdateFailed  |  |  | ✔ |  |  | ✔ | |✔ | |
| ScaleFailed |  |  |  |  |  | ✔ |✔ | |  |  | 



## <a name="see-also"></a>Otras referencias
* [Crear un BizTalk Service mediante Hola portal de Azure clásico](http://go.microsoft.com/fwlink/p/?LinkID=302280)<br/>
* [¿Qué puede hacer en pestañas del panel, monitor y escala de hello en servicios de BizTalk](http://go.microsoft.com/fwlink/p/?LinkID=302281)<br/>
* [Lo que se obtiene con las ediciones Developer, Basic, Standard y Premium hello en servicios de BizTalk](http://go.microsoft.com/fwlink/p/?LinkID=302279)<br/>
* [¿Cómo tooback una copia de seguridad y restaurar un BizTalk Service](http://go.microsoft.com/fwlink/p/?LinkID=329873)<br/>
* [BizTalk Services: limitaciones](http://go.microsoft.com/fwlink/p/?LinkID=302282)<br/>
* [Recuperar Hola Bus de servicio y Control de acceso emisor y el nombre de valores clave del emisor para su BizTalk Service](http://go.microsoft.com/fwlink/p/?LinkID=303941)<br/>
* [¿Cómo puedo comenzar a utilizar Hola SDK de servicios de BizTalk de Azure](http://go.microsoft.com/fwlink/p/?LinkID=302335)

