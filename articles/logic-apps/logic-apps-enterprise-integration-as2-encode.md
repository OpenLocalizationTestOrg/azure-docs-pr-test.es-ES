---
title: mensajes de AS2 aaaEncode - Azure Logic Apps | Documentos de Microsoft
description: "¿Cómo toouse Hola codificador AS2 de hello paquete de integración empresarial para las aplicaciones lógicas de Azure"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: 332fb9e3-576c-4683-bd10-d177a0ebe9a3
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 2b372c416512ffa9ea5dc50ce0f767bfd8aefbc4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="encode-as2-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a>Codificar los mensajes de AS2 para las aplicaciones lógicas de Azure con hello paquete de integración empresarial

tooestablish seguridad y confiabilidad al transmitir los mensajes, utilice conector de mensaje de Hola codificar AS2. Este conector proporciona firma digital, cifrado y confirmaciones a través de notificaciones de disposición de mensaje (MDN), lo que conduce también toosupport para sin repudio.

## <a name="before-you-start"></a>Antes de comenzar

Aquí es elementos de Hola que necesita:

* Una cuenta de Azure; puede crear una [gratuita](https://azure.microsoft.com/free)
* Una [cuenta de integración](logic-apps-enterprise-integration-create-integration-account.md) que ya esté definida y asociada a su suscripción de Azure. Debe tener un conector integración cuenta toouse Hola AS2 codificar los mensajes.
* Al menos dos [asociados](logic-apps-enterprise-integration-partners.md) que ya estén definidos en su cuenta de integración.
* Un [contrato AS2](logic-apps-enterprise-integration-as2.md) ya definido en la cuenta de integración.

## <a name="encode-as2-messages"></a>Codificación de mensajes AS2

1. [Creación de una aplicación lógica](logic-apps-create-a-logic-app.md).

2. Conector de mensaje de Hola codificar AS2 no tiene desencadenadores, por lo que debe agregar un desencadenador para iniciar la aplicación lógica, como un desencadenador de la solicitud. Hola diseñador la lógica de aplicación, agregar un desencadenador y, a continuación, agregar una aplicación de lógica de tooyour de acción.

3.  En el cuadro de búsqueda de hello, escriba "AS2" para el filtro. Seleccione **AS2 – Encode AS2 Message** (AS2: codificación de mensajes AS2).
   
    ![Búsqueda de "AS2"](./media/logic-apps-enterprise-integration-as2-encode/as2decodeimage1.png)

4. Si previamente no creó ninguna conexión de cuenta de integración de tooyour, se te pedirá toocreate ahora esa conexión. Nombre de la conexión y seleccione cuenta de integración de Hola que desea tooconnect. 
   
    ![Crear cuenta de conexión de toointegration](./media/logic-apps-enterprise-integration-as2-encode/as2encodeimage1.png)  

    Aquellas propiedades con un asterisco son obligatorias.

    | Propiedad | Detalles |
    | --- | --- |
    | Nombre de la conexión * |Escriba cualquier nombre para la conexión. |
    | Cuenta de integración* |Escriba un nombre para la cuenta de integración. Asegúrese de que la aplicación de cuenta y la lógica de integración están en hello misma ubicación de Azure. |

5.  Cuando haya terminado, los detalles de la conexión deben tener un aspecto similar ejemplo toothis. toofinish crear la conexión, elija **crear**.
   
    ![detalles de la conexión de integración](./media/logic-apps-enterprise-integration-as2-encode/as2encodeimage2.png)

6. Una vez creada la conexión, como se muestra en este ejemplo, proporcione los detalles de **AS2-de**, **AS2 tooidentifiers** como está configurado en el acuerdo, y **cuerpo**, que es carga del mensaje Hola.
   
    ![especificar los campos obligatorios](./media/logic-apps-enterprise-integration-as2-encode/as2encodeimage3.png)

## <a name="as2-encoder-details"></a>Detalles de codificador de AS2

Hola codificar AS2 conector lleva a cabo estas tareas: 

* Aplica los encabezados AS2/HTTP.
* Firma los mensajes salientes (en caso de haberse configurado).
* Cifra los mensajes salientes (en caso de haberse configurado).
* Comprime el mensaje de bienvenida (si está configurado)

## <a name="try-this-sample"></a>Ejemplo para probar

tootry implementar un escenario de AS2 lógica totalmente operativo ejemplo y la aplicación, vea hello [AS2 plantilla de aplicación lógica y escenario](https://azure.microsoft.com/documentation/templates/201-logic-app-as2-send-receive/).

## <a name="view-hello-swagger"></a>Swagger de hello de vista
Vea hello [swagger detalles](/connectors/as2/). 

## <a name="next-steps"></a>Pasos siguientes
[Obtener más información sobre Hola paquete de integración empresarial](logic-apps-enterprise-integration-overview.md "Obtenga más información sobre el paquete de integración empresarial") 

