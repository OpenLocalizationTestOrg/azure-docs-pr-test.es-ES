---
title: mensajes de aaaEncode X12 - Azure Logic Apps | Documentos de Microsoft
description: "Validar EDI y convertir la codificación XML mensajes con X12 mensaje codificador Hola paquete de integración empresarial para las aplicaciones lógicas de Azure"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: a01e9ca9-816b-479e-ab11-4a984f10f62d
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 785dbd2c7c82463154732921e07e3586d2307840
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="encode-x12-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a>Codificar X12 mensajes para las aplicaciones lógicas de Azure con hello paquete de integración empresarial

Con el conector de mensaje de Hola Encode X12, puede validar EDI y propiedades específicas del partner, convertir los mensajes codificados en XML en conjuntos de transacciones EDI en el intercambio de Hola y solicitar una confirmación técnica, la confirmación funcional o ambos.
toouse este conector, debe agregar Hola conector tooan existente desencadenador en la aplicación lógica.

## <a name="before-you-start"></a>Antes de comenzar

Aquí es elementos de Hola que necesita:

* Una cuenta de Azure; puede crear una [gratuita](https://azure.microsoft.com/free)
* Una [cuenta de integración](logic-apps-enterprise-integration-create-integration-account.md) que ya esté definida y asociada a su suscripción de Azure. Debe tener un conector integración cuenta toouse Hola Encode X12 mensaje.
* Al menos dos [asociados](logic-apps-enterprise-integration-partners.md) que ya estén definidos en su cuenta de integración.
* Un [contrato X12](logic-apps-enterprise-integration-x12.md) ya definido en su cuenta de integración

## <a name="encode-x12-messages"></a>Codificación de mensajes X12

1. [Creación de una aplicación lógica](logic-apps-create-a-logic-app.md).

2. Conector de mensaje de Hola Encode X12 no tiene desencadenadores, por lo que debe agregar un desencadenador para iniciar la aplicación lógica, como un desencadenador de la solicitud. Hola diseñador la lógica de aplicación, agregar un desencadenador y, a continuación, agregar una aplicación de lógica de tooyour de acción.

3.  En el cuadro de búsqueda de hello, escriba "x12" para el filtro. Seleccione **X12-codificar los mensajes tooX12 por el nombre del contrato** o **X12-codificar tooX12 mensaje identidades**.
   
    ![Búsqueda de "x12"](./media/logic-apps-enterprise-integration-x12-encode/x12decodeimage1.png) 

3. Si previamente no creó ninguna conexión de cuenta de integración de tooyour, se te pedirá toocreate ahora esa conexión. Nombre de la conexión y seleccione cuenta de integración de Hola que desea tooconnect. 
   
    ![conexión de la cuenta de integración](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage1.png)

    Aquellas propiedades con un asterisco son obligatorias.

    | Propiedad | Detalles |
    | --- | --- |
    | Nombre de la conexión * |Escriba cualquier nombre para la conexión. |
    | Cuenta de integración* |Escriba un nombre para la cuenta de integración. Asegúrese de que la aplicación de cuenta y la lógica de integración están en hello misma ubicación de Azure. |

5.  Cuando haya terminado, los detalles de la conexión deben tener un aspecto similar ejemplo toothis. toofinish crear la conexión, elija **crear**.

    ![creación de la conexión de la cuenta de integración](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage2.png)

    La conexión se ha creado.

    ![detalles de conexión de la cuenta de integración](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage3.png) 

#### <a name="encode-x12-messages-by-agreement-name"></a>Encode X12 Message por nombre de acuerdo

Si ha elegido tooencode X12 mensajes por nombre de contrato, abra hello **nombre de X12 acuerdo** lista, escriba o seleccione el X12 existente acuerdo. Escriba tooencode de mensaje de Hola XML.

![Escriba X12 tooencode de mensajes XML y el nombre de contrato](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage4.png)

#### <a name="encode-x12-messages-by-identities"></a>Encode X12 Message por identidades

Si elige tooencode X12 mensajes para las identidades, escriba el identificador del remitente de hello, calificador de remitente, identificador de receptor y calificador de receptor como está configurado en su X12 acuerdo. Seleccione tooencode de mensaje de Hola XML.
   
![Proporcione las identidades de remitente y receptor, seleccione tooencode de mensaje XML](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage5.png) 

## <a name="x12-encode-details"></a>Detalles de la codificación de X12

Hola X12 Encode conector lleva a cabo estas tareas:

* Resolución del acuerdo haciendo coincidir las propiedades de contexto de remitente y receptor.
* Serializa el intercambio EDI de hello, convertir los mensajes codificados en XML en conjuntos de transacciones EDI en el intercambio de Hola.
* Aplica segmentos de encabezado y finalizador del conjunto de transacciones.
* Genera un número de control de intercambio, un número de control de grupo y un número de control del conjunto de transacciones para cada intercambio de salida.
* Reemplaza los separadores en datos de carga de Hola
* Valida propiedades EDI y específicas del asociado.
  * Validación de esquema de los elementos de datos de conjuntos de transacciones de hello en mensajes de bienvenida del esquema
  * Validación de EDI realizada en los elementos de datos del conjunto de transacciones.
  * Validación extendida realizada en los elementos de datos del conjunto de transacciones.
* Solicita una confirmación técnica o funcional (si esta opción está configurada).
  * Se genera una confirmación técnica como resultado de la validación del encabezado. Hola confirmación técnica informa Hola del estado de procesamiento de Hola de un encabezado de intercambio y finalizador mediante el receptor de direcciones de Hola
  * Se genera una confirmación funcional como resultado de la validación del cuerpo. confirmación funcional Hello notifica cada error al procesar Hola recibió el documento

## <a name="view-hello-swagger"></a>Swagger de hello de vista
Vea hello [swagger detalles](/connectors/x12/). 

## <a name="next-steps"></a>Pasos siguientes
[Obtener más información sobre Hola paquete de integración empresarial](logic-apps-enterprise-integration-overview.md "Obtenga más información sobre el paquete de integración empresarial") 

