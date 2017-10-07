---
title: mensajes de AS2 aaaDecode - Azure Logic Apps | Documentos de Microsoft
description: "¿Cómo toouse Hola descodificador AS2 en hello paquete de integración empresarial para las aplicaciones lógicas de Azure"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: cf44af18-1fe5-41d5-9e06-cc57a968207c
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 2406e5ec68e0906700fad97d60cb83ef0d106cd6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="decode-as2-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a>Descodificar mensajes AS2 para las aplicaciones lógicas de Azure con hello paquete de integración empresarial 

tooestablish seguridad y confiabilidad al transmitir los mensajes, utilice el conector de mensaje de AS2 descodificar de Hola. Este conector proporciona firma digital, descifrado y confirmaciones a través de las notificaciones de disposición de mensajes (MDN).

## <a name="before-you-start"></a>Antes de comenzar

Aquí es elementos de Hola que necesita:

* Una cuenta de Azure; puede crear una [gratuita](https://azure.microsoft.com/free)
* Una [cuenta de integración](logic-apps-enterprise-integration-create-integration-account.md) que ya esté definida y asociada a su suscripción de Azure. Debe tener un conector de mensaje integración cuenta toouse Hola descodificar AS2.
* Al menos dos [asociados](logic-apps-enterprise-integration-partners.md) que ya estén definidos en su cuenta de integración.
* Un [contrato AS2](logic-apps-enterprise-integration-as2.md) ya definido en la cuenta de integración.

## <a name="decode-as2-messages"></a>Descodificación de mensajes AS2

1. [Creación de una aplicación lógica](../logic-apps/logic-apps-create-a-logic-app.md).

2. Conector de mensaje de Hola AS2 descodificar no tiene desencadenadores, por lo que debe agregar un desencadenador para iniciar la aplicación lógica, como un desencadenador de la solicitud. Hola diseñador la lógica de aplicación, agregar un desencadenador y, a continuación, agregar una aplicación de lógica de tooyour de acción.

3.  En el cuadro de búsqueda de hello, escriba "AS2" para el filtro. Seleccione **AS2 – Decode AS2 Message** (AS2: descodificación de mensajes AS2).
   
    ![Búsqueda de "AS2"](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage1.png)

4. Si previamente no creó ninguna conexión de cuenta de integración de tooyour, se te pedirá toocreate ahora esa conexión. Nombre de la conexión y seleccione cuenta de integración de Hola que desea tooconnect.
   
    ![Crear conexión de integración](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage2.png)

    Aquellas propiedades con un asterisco son obligatorias.

    | Propiedad | Detalles |
    | --- | --- |
    | Nombre de la conexión * |Escriba cualquier nombre para la conexión. |
    | Cuenta de integración* |Escriba un nombre para la cuenta de integración. Asegúrese de que la aplicación de cuenta y la lógica de integración están en hello misma ubicación de Azure. |

5.  Cuando haya terminado, los detalles de la conexión deben tener un aspecto similar ejemplo toothis. toofinish crear la conexión, elija **crear**.

    ![detalles de la conexión de integración](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage3.png)

6. Una vez creada la conexión, como se muestra en este ejemplo, seleccione **cuerpo** y **encabezados** de hello solicitar salidas.
   
    ![conexión de integración creada](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage4.png) 

    Por ejemplo:

    ![Seleccione el cuerpo y los encabezados de las salidas de la solicitud](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage5.png) 

## <a name="as2-decoder-details"></a>Detalles de descodificador de AS2

Hola descodificar AS2 conector lleva a cabo estas tareas: 

* Procesa encabezados AS2/HTTP.
* Comprueba la firma de hello (si está configurado)
* Descifra los mensajes de saludo (si está configurado)
* Descomprime el mensaje de bienvenida (si está configurado)
* Reconcilia un MDN recibido con el mensaje de salida original Hola
* Actualiza y correlaciona registros en la base de datos de hello sin repudio
* Escribe registros para los informes de estado de AS2.
* contenido de carga de salida de Hello está codificados con base64
* Determina si es necesario, un MDN y si Hola MDN debe ser sincrónica o asincrónicas basados en configuración de acuerdo AS2
* Genera un MDN sincrónico o asincrónico (en función de las configuraciones del acuerdo).
* Establece propiedades y los tokens de correlación de hello en hello MDN

## <a name="try-this-sample"></a>Ejemplo para probar

tootry implementar un escenario de AS2 lógica totalmente operativo ejemplo y la aplicación, vea hello [AS2 plantilla de aplicación lógica y escenario](https://azure.microsoft.com/documentation/templates/201-logic-app-as2-send-receive/).

## <a name="view-hello-swagger"></a>Swagger de hello de vista
Vea hello [swagger detalles](/connectors/as2/). 

## <a name="next-steps"></a>Pasos siguientes
[Obtener más información sobre Hola paquete de integración empresarial](logic-apps-enterprise-integration-overview.md) 

