---
title: mensajes EDIFACT aaaEncode - Azure Logic Apps | Documentos de Microsoft
description: "Validar EDI y generar XML con el codificador de mensajes EDIFACT en hello paquete de integración empresarial para las aplicaciones lógicas de Azure"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: 974ac339-d97a-4715-bc92-62d02281e900
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: b3799dbd2492adef597022d017cf28f5ceb1085c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="encode-edifact-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a>Codificar los mensajes EDIFACT para las aplicaciones lógicas de Azure con hello paquete de integración empresarial

Con el conector de mensaje de Hola codificar EDIFACT, puede validar EDI y propiedades específicas del partner, generar un documento XML para cada conjunto de transacciones y solicitar una confirmación técnica, la confirmación funcional o ambos.
toouse este conector, debe agregar Hola conector tooan existente desencadenador en la aplicación lógica.

## <a name="before-you-start"></a>Antes de comenzar

Aquí es elementos de Hola que necesita:

* Una cuenta de Azure; puede crear una [gratuita](https://azure.microsoft.com/free)
* Una [cuenta de integración](logic-apps-enterprise-integration-create-integration-account.md) que ya esté definida y asociada a su suscripción de Azure. Debe tener un conector de mensaje integración cuenta toouse Hola codificar EDIFACT. 
* Al menos dos [asociados](logic-apps-enterprise-integration-partners.md) que ya estén definidos en su cuenta de integración.
* Un [contrato EDIFACT](logic-apps-enterprise-integration-edifact.md) ya definido en la cuenta de integración.

## <a name="encode-edifact-messages"></a>Codificación de mensajes EDIFACT

1. [Creación de una aplicación lógica](logic-apps-create-a-logic-app.md).

2. Conector de mensaje de Hola codificar EDIFACT no tiene desencadenadores, por lo que debe agregar un desencadenador para iniciar la aplicación lógica, como un desencadenador de la solicitud. Hola diseñador la lógica de aplicación, agregar un desencadenador y, a continuación, agregar una aplicación de lógica de tooyour de acción.

3.  En el cuadro de búsqueda de hello, escriba "EDIFACT" como filtro. Seleccione **codificar mensaje EDIFACT por el nombre del contrato** o **Encode tooEDIFACT mensaje identidades**.
   
    ![buscar EDIFACT](media/logic-apps-enterprise-integration-edifact-encode/edifactdecodeimage1.png)  

3. Si previamente no creó ninguna conexión de cuenta de integración de tooyour, se te pedirá toocreate ahora esa conexión. Nombre de la conexión y seleccione cuenta de integración de Hola que desea tooconnect.

    ![crear la conexión de la cuenta de integración](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage1.png)  

    Aquellas propiedades con un asterisco son obligatorias.

    | Propiedad | Detalles |
    | --- | --- |
    | Nombre de la conexión * |Escriba cualquier nombre para la conexión. |
    | Cuenta de integración* |Escriba un nombre para la cuenta de integración. Asegúrese de que la aplicación de cuenta y la lógica de integración están en hello misma ubicación de Azure. |

5.  Cuando haya terminado, los detalles de la conexión deben tener un aspecto similar ejemplo toothis. toofinish crear la conexión, elija **crear**.

    ![detalles de conexión de la cuenta de integración](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage2.png)

    La conexión se ha creado.

    ![creación de la conexión de la cuenta de integración](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage4.png)

#### <a name="encode-edifact-message-by-agreement-name"></a>Encode EDIFACT Message por nombre del acuerdo

Si ha elegido tooencode mensajes EDIFACT por nombre de contrato, abra hello **acuerdo nombre de EDIFACT** lista, escriba o seleccione el nombre del acuerdo de EDIFACT. Escriba tooencode de mensaje de Hola XML.

![Escriba el nombre del acuerdo de EDIFACT y tooencode de mensaje XML](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage6.png)

#### <a name="encode-edifact-message-by-identities"></a>Encode EDIFACT Message por identidades

Si elige tooencode mensajes EDIFACT para las identidades, escriba el identificador de remitente de hello, calificador de remitente, identificador de receptor y el calificador de receptor como está configurado en el acuerdo de EDIFACT. Seleccione tooencode de mensaje de Hola XML.

![Proporcione las identidades de remitente y receptor, seleccione tooencode de mensaje XML](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage7.png)

## <a name="edifact-encode-details"></a>Detalles de la codificación de EDIFACT

Hola codificar EDIFACT conector lleva a cabo estas tareas: 

* Resolver el acuerdo de hello haciendo coincidir el calificador de remitente de hello & identificador y calificador e identificador
* Serializa el intercambio EDI de hello, convertir los mensajes codificados en XML en conjuntos de transacciones EDI en el intercambio de Hola.
* Aplica segmentos de encabezado y finalizador del conjunto de transacciones.
* Genera un número de control de intercambio, un número de control de grupo y un número de control del conjunto de transacciones para cada intercambio de salida.
* Reemplaza los separadores en datos de carga de Hola
* Valida propiedades EDI y específicas del asociado.
  * Validación de esquema de los elementos de datos de conjuntos de transacciones de hello en el esquema de mensaje de Hola.
  * Validación de EDI realizada en los elementos de datos del conjunto de transacciones.
  * Validación extendida realizada en los elementos de datos del conjunto de transacciones.
* Genera un documento XML para cada conjunto de transacciones.
* Solicita una confirmación técnica o funcional (si esta opción está configurada).
  * Como confirmación técnica, mensaje de bienvenida de CONTRL indica la recepción de un intercambio.
  * Como una confirmación funcional, mensaje de bienvenida de CONTRL indica la aceptación o rechazo del intercambio de hello recibido, grupo o los mensajes, con una lista de errores o funcionalidad no admitida

## <a name="view-swagger-file"></a>Ver el archivo de Swagger
detalles de Swagger de tooview hello para el conector de saludo EDIFACT, vea [EDIFACT](/connectors/edifact/).

## <a name="next-steps"></a>Pasos siguientes
[Obtener más información sobre Hola paquete de integración empresarial](logic-apps-enterprise-integration-overview.md "Obtenga más información sobre el paquete de integración empresarial") 

