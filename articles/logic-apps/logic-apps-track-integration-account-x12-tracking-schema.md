---
title: "aaaX12 esquemas de seguimiento para la supervisión de B2B - Azure Logic Apps | Documentos de Microsoft"
description: "Utilice X12 seguimiento de mensajes de toomonitor B2B de esquemas de las transacciones en la cuenta de la integración de Azure."
author: padmavc
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: a5413f80-eaad-4bcf-b371-2ad0ef629c3d
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ed1b338730214dcae12c367ebff025d7122328fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="start-or-enable-tracking-of-x12-messages-toomonitor-success-errors-and-message-properties"></a>Los mensajes de inicio o habilitar el seguimiento de X12 toomonitor correcto, los errores y las propiedades de mensaje
Puede usar estos X12 esquemas de seguimiento en su toohelp de cuenta de la integración de Azure supervisar las transacciones de negocio a negocio (B2B):

* Esquema de seguimiento de conjuntos de transacciones de X12
* Esquema de seguimiento de confirmación de conjuntos de transacciones de X12
* Esquema de seguimiento de intercambio de X12
* Esquema de seguimiento de confirmación de intercambio de X12
* Esquema de seguimiento de grupos funcionales de X12
* Esquema de seguimiento de confirmación de grupos funcionales de X12

## <a name="x12-transaction-set-tracking-schema"></a>Esquema de seguimiento de conjuntos de transacciones de X12
````java

    {
            "agreementProperties": {
                "senderPartnerName": "",
                "receiverPartnerName": "",
                "senderQualifier": "",
                "senderIdentifier": "",
                "receiverQualifier": "",
                "receiverIdentifier": "",
                "agreementName": ""
            },
            "messageProperties": {
                "direction": "",
                "interchangeControlNumber": "",
                "functionalGroupControlNumber": "",
                "transactionSetControlNumber": "",
                "CorrelationMessageId": "",
                "messageType": "",
                "isMessageFailed": "",
                "isTechnicalAcknowledgmentExpected": "",
                "isFunctionalAcknowledgmentExpected": "",
                "needAk2LoopForValidMessages":  "",
                "segmentsCount": ""
            }
    }
````

| Propiedad | Escriba | Descripción |
| --- | --- | --- |
| senderPartnerName | string | Nombre de asociado del remitente del mensaje X12. (Opcional) |
| receiverPartnerName | String | Nombre de asociado del destinatario del mensaje X12. (Opcional) |
| senderQualifier | string | Calificador del asociado remitente. (Obligatorio) |
| senderIdentifier | string | Identificador del asociado remitente. (Obligatorio) |
| receiverQualifier | String | Calificador del asociado destinatario. (Obligatorio) |
| receiverIdentifier | String | Identificador del asociado destinatario. (Obligatorio) |
| agreementName | String | Nombre de mensajes de saludo de hello X12 acuerdo toowhich se resuelve. (Opcional) |
| dirección | Enum | Dirección de flujo de mensajes de Hola, recepción o envío. (Obligatorio) |
| interchangeControlNumber | String | Número de control de intercambio. (Opcional) |
| functionalGroupControlNumber | String | Número de control funcional. (Opcional) |
| transactionSetControlNumber | string | Número de control de conjuntos de transacciones. (Opcional) |
| CorrelationMessageId | String | Identificador del mensaje de correlación. Una combinación de {AgreementName}{*GroupControlNumber*}{TransactionSetControlNumber}. (Opcional) |
| messageType | String | Conjunto de transacciones o tipo de documento. (Opcional) |
| isMessageFailed | Booleano | Si no se pudo mensaje hello X12. (Obligatorio) |
| isTechnicalAcknowledgmentExpected | Booleano | ¿Confirmación técnica Hola está configurada en el acuerdo de hello X12. (Obligatorio) |
| isFunctionalAcknowledgmentExpected | Booleano | ¿Confirmación funcional Hola está configurada en el acuerdo de hello X12. (Obligatorio) |
| needAk2LoopForValidMessages | Booleano | Si el bucle de hello AK2 es necesario para un mensaje válido. (Obligatorio) |
| segmentsCount | Entero | Número de segmentos de conjunto de transacciones de hello X12. (Opcional) |

## <a name="x12-transaction-set-acknowledgement-tracking-schema"></a>Esquema de seguimiento de confirmación de conjuntos de transacciones de X12
````java

    {
            "agreementProperties": {
                "senderPartnerName": "",
                "receiverPartnerName": "",
                "senderQualifier": "",
                "senderIdentifier": "",
                "receiverQualifier": "",
                "receiverIdentifier": "",
                "agreementName": ""
            },
            "messageProperties": {
                "direction": "",
                "interchangeControlNumber": "",
                "functionalGroupControlNumber": "",
                "isaSegment": "",
                "gsSegment": "",
                "respondingfunctionalGroupControlNumber": "",
                "respondingFunctionalGroupId": "",
                "respondingtransactionSetControlNumber": "",
                "respondingTransactionSetId": "",
                "statusCode": "",
                "processingStatus": "",
                "CorrelationMessageId": ""
                "isMessageFailed": "",
                "ak2Segment": "",
                "ak3Segment": "",
                "ak5Segment": ""
            }
    }
````

| Propiedad | Escriba | Descripción |
| --- | --- | --- |
| senderPartnerName | string | Nombre de asociado del remitente del mensaje X12. (Opcional) |
| receiverPartnerName | String | Nombre de asociado del destinatario del mensaje X12. (Opcional) |
| senderQualifier | string | Calificador del asociado remitente. (Obligatorio) |
| senderIdentifier | string | Identificador del asociado remitente. (Obligatorio) |
| receiverQualifier | String | Calificador del asociado destinatario. (Obligatorio) |
| receiverIdentifier | String | Identificador del asociado destinatario. (Obligatorio) |
| agreementName | String | Nombre de mensajes de saludo de hello X12 acuerdo toowhich se resuelve. (Opcional) |
| dirección | Enum | Dirección de flujo de mensajes de Hola, recepción o envío. (Obligatorio) |
| interchangeControlNumber | String | Número de control de confirmación funcional Hola de intercambio. Valor rellena solo para el lado de envío de Hola donde se recibe la confirmación funcional para hello toopartner de mensajes enviados. (Opcional) |
| functionalGroupControlNumber | String | Número de control de grupo funcional de confirmación funcional Hola. Valor rellena solo para el lado de envío de Hola donde se recibe la confirmación funcional para hello toopartner de mensajes enviados. (Opcional) |
| isaSegment | String | Segmento ISA del mensaje de bienvenida. Valor rellena solo para el lado de envío de Hola donde se recibe la confirmación funcional para hello toopartner de mensajes enviados. (Opcional) |
| gsSegment | String | Segmento GS de mensaje de bienvenida. Valor rellena solo para el lado de envío de Hola donde se recibe la confirmación funcional para hello toopartner de mensajes enviados. (Opcional) |
| respondingfunctionalGroupControlNumber | string | Número de control de intercambio de respuesta. (Opcional) |
| respondingFunctionalGroupId | String | Id. de grupo funcional de responder, que asigna tooAK101 en la confirmación de Hola. (Opcional) |
| respondingtransactionSetControlNumber | string | Número de control del conjunto de transacciones de respuesta. (Opcional) |
| respondingTransactionSetId | String | Id., que se asigna tooAK201 en la confirmación de hello del conjunto de transacciones responde. (Opcional) |
| statusCode | Booleano | Código de estado de la confirmación del conjunto de transacciones. (Obligatorio) |
| segmentsCount | Enum | Código de estado de la confirmación. Los valores permitidos son **Accepted**, **Rejected**, y **AcceptedWithErrors**. (Obligatorio) |
| processingStatus | Enum | Estado de procesamiento de confirmación de Hola. Los valores permitidos son **Received**, **Generated** y **Sent**. (Obligatorio) |
| CorrelationMessageId | String | Identificador del mensaje de correlación. Una combinación de {AgreementName}{*GroupControlNumber*}{TransactionSetControlNumber}. (Opcional) |
| isMessageFailed | Booleano | Si no se pudo mensaje hello X12. (Obligatorio) |
| ak2Segment | String | La confirmación de un conjunto de transacciones dentro de hello recibió grupo funcional. (Opcional) |
| ak3Segment | String | Indica que hay errores en un segmento de datos. (Opcional) |
| ak5Segment | String | Indica si se acepta o se rechaza Hola conjunto de transacciones identificado en el segmento de hello AK2 y el motivo. (Opcional) |

## <a name="x12-interchange-tracking-schema"></a>Esquema de seguimiento de intercambio de X12
````java

    {
            "agreementProperties": {
                "senderPartnerName": "",
                "receiverPartnerName": "",
                "senderQualifier": "",
                "senderIdentifier": "",
                "receiverQualifier": "",
                "receiverIdentifier": "",
                "agreementName": ""
            },
            "messageProperties": {
                "direction": "",
                "interchangeControlNumber": "",
                "isaSegment": "",
                "isTechnicalAcknowledgmentExpected": "",
                "isMessageFailed": "",
                "isa09": "",
                "isa10": "",
                "isa11": "",
                "isa12": "",
                "isa14": "",
                "isa15": "",
                "isa16": ""
            }
    }
````

| Propiedad | Escriba | Descripción |
| --- | --- | --- |
| senderPartnerName | string | Nombre de asociado del remitente del mensaje X12. (Opcional) |
| receiverPartnerName | String | Nombre de asociado del destinatario del mensaje X12. (Opcional) |
| senderQualifier | string | Calificador del asociado remitente. (Obligatorio) |
| senderIdentifier | string | Identificador del asociado remitente. (Obligatorio) |
| receiverQualifier | String | Calificador del asociado destinatario. (Obligatorio) |
| receiverIdentifier | String | Identificador del asociado destinatario. (Obligatorio) |
| agreementName | String | Nombre de mensajes de saludo de hello X12 acuerdo toowhich se resuelve. (Opcional) |
| dirección | Enum | Dirección de flujo de mensajes de Hola, recepción o envío. (Obligatorio) |
| interchangeControlNumber | String | Número de control de intercambio. (Opcional) |
| isaSegment | string | Segmento ISA del mensaje. (Opcional) |
| isTechnicalAcknowledgmentExpected | Booleano | ¿Confirmación técnica Hola está configurada en el acuerdo de hello X12. (Obligatorio) |
| isMessageFailed | Booleano | Si no se pudo mensaje hello X12. (Obligatorio) |
| isa09 | string | Fecha de intercambio del documento X12. (Opcional) |
| isa10 | string | Hora de intercambio del documento X12. (Opcional) |
| isa11 | string | Identificador de los estándares de control del intercambio de X12. (Opcional) |
| isa12 | String | Número de versión de control del intercambio de X12. (Opcional) |
| isa14 | string | Se solicita la confirmación de X12. (Opcional) |
| isa15 | String | Indicador de prueba o de producción. (Opcional) |
| isa16 | String | Separador de elementos. (Opcional) |

## <a name="x12-interchange-acknowledgement-tracking-schema"></a>Esquema de seguimiento de confirmación de intercambio de X12
````java
    {
            "agreementProperties": {
                "senderPartnerName": "",
                "receiverPartnerName": "",
                "senderQualifier": "",
                "senderIdentifier": "",
                "receiverQualifier": "",
                "receiverIdentifier": "",
                "agreementName": ""
            },
            "messageProperties": {
                "direction": "",
                "interchangeControlNumber": "",
                "isaSegment": "",
                "respondingInterchangeControlNumber": "",
                "isMessageFailed": "",
                "statusCode": "",
                "processingStatus": "",
                "ta102": "",
                "ta103": "",
                "ta105": ""
            }
    }
````

| Propiedad | Escriba | Descripción |
| --- | --- | --- |
| senderPartnerName | string | Nombre de asociado del remitente del mensaje X12. (Opcional) |
| receiverPartnerName | String | Nombre de asociado del destinatario del mensaje X12. (Opcional) |
| senderQualifier | string | Calificador del asociado remitente. (Obligatorio) |
| senderIdentifier | string | Identificador del asociado remitente. (Obligatorio) |
| receiverQualifier | String | Calificador del asociado destinatario. (Obligatorio) |
| receiverIdentifier | String | Identificador del asociado destinatario. (Obligatorio) |
| agreementName | String | Nombre de mensajes de saludo de hello X12 acuerdo toowhich se resuelve. (Opcional) |
| dirección | Enum | Dirección de flujo de mensajes de Hola, recepción o envío. (Obligatorio) |
| interchangeControlNumber | String | Número de control de confirmación técnica Hola que se recibe de los socios de intercambio. (Opcional) |
| isaSegment | String | Segmento ISA para la confirmación técnica Hola que se recibe de los socios. (Opcional) |
| respondingInterchangeControlNumber |String | Número de control de confirmación técnica Hola que se recibe de los socios de intercambio. (Opcional) |
| isMessageFailed | Booleano | Si no se pudo mensaje hello X12. (Obligatorio) |
| statusCode | Enum | Código de estado de la confirmación del intercambio. Los valores permitidos son **Accepted**, **Rejected**, y **AcceptedWithErrors**. (Obligatorio) |
| processingStatus | Enum | Estado de la confirmación. Los valores permitidos son **Received**, **Generated** y **Sent**. (Obligatorio) |
| ta102 | String | Fecha de intercambio. (Opcional) |
| ta103 | String | Hora de intercambio. (Opcional) |
| ta105 | String | Código de nota de intercambio. (Opcional) |

## <a name="x12-functional-group-tracking-schema"></a>Esquema de seguimiento de grupos funcionales de X12
````java

    {
            "agreementProperties": {
                "senderPartnerName": "",
                "receiverPartnerName": "",
                "senderQualifier": "",
                "senderIdentifier": "",
                "receiverQualifier": "",
                "receiverIdentifier": "",
                "agreementName": ""
            },
            "messageProperties": {
                "direction": "",
                "interchangeControlNumber": "",
                "functionalGroupControlNumber": "",
                "gsSegment": "",
                "isTechnicalAcknowledgmentExpected": "",
                "isFunctionalAcknowledgmentExpected": "",
                "isMessageFailed": "",
                "gs01": "",
                "gs02": "",
                "gs03": "",
                "gs04": "",
                "gs05": "",
                "gs07": "",
                "gs08": ""
            }
    }
````

| Propiedad | Escriba | Descripción |
| --- | --- | --- |
| senderPartnerName | string | Nombre de asociado del remitente del mensaje X12. (Opcional) |
| receiverPartnerName | String | Nombre de asociado del destinatario del mensaje X12. (Opcional) |
| senderQualifier | string | Calificador del asociado remitente. (Obligatorio) |
| senderIdentifier | string | Identificador del asociado remitente. (Obligatorio) |
| receiverQualifier | String | Calificador del asociado destinatario. (Obligatorio) |
| receiverIdentifier | String | Identificador del asociado destinatario. (Obligatorio) |
| agreementName | String | Nombre de mensajes de saludo de hello X12 acuerdo toowhich se resuelve. (Opcional) |
| dirección | Enum | Dirección de flujo de mensajes de Hola, recepción o envío. (Obligatorio) |
| interchangeControlNumber | String | Número de control de intercambio. (Opcional) |
| functionalGroupControlNumber | String | Número de control funcional. (Opcional) |
| gsSegment | string | Segmento GS del mensaje. (Opcional) |
| isTechnicalAcknowledgmentExpected | Booleano | ¿Confirmación técnica Hola está configurada en el acuerdo de hello X12. (Obligatorio) |
| isFunctionalAcknowledgmentExpected | Booleano | ¿Confirmación funcional Hola está configurada en el acuerdo de hello X12. (Obligatorio) |
| isMessageFailed | Booleano | Si no se pudo mensaje hello X12. (Obligatorio)|
| gs01 | String | Código del identificador funcional. (Opcional) |
| gs02 | string | Código del remitente de la aplicación. (Opcional) |
| gs03 | String | Código del destinatario de la aplicación. (Opcional) |
| gs04 | String | Fecha del grupo funcional. (Opcional) |
| gs05 | string | Hora del grupo funcional. (Opcional) |
| gs07 | string | Código de agencia responsable. (Opcional) |
| gs08 | string | Código de identificador de versión/lanzamiento/industria. (Opcional) |

## <a name="x12-functional-group-acknowledgement-tracking-schema"></a>Esquema de seguimiento de confirmación de grupos funcionales de X12
````java
    {
            "agreementProperties": {
                "senderPartnerName": "",
                "receiverPartnerName": "",
                "senderQualifier": "",
                "senderIdentifier": "",
                "receiverQualifier": "",
                "receiverIdentifier": "",
                "agreementName": ""
            },
            "messageProperties": {
                "direction": "",
                "interchangeControlNumber": "",
                "functionalGroupControlNumber": "",
                "isaSegment": "",
                "gsSegment": "",
                "respondingfunctionalGroupControlNumber": "",
                "respondingFunctionalGroupId": "",
                "isMessageFailed": "",
                "statusCode": "",
                "processingStatus": "",
                "ak903": "",
                "ak904": "",
                "ak9Segment": ""
            }
    }
````

| Propiedad | Escriba | Descripción |
| --- | --- | --- |
| senderPartnerName | string | Nombre de asociado del remitente del mensaje X12. (Opcional) |
| receiverPartnerName | String | Nombre de asociado del destinatario del mensaje X12. (Opcional) |
| senderQualifier | string | Calificador del asociado remitente. (Obligatorio) |
| senderIdentifier | string | Identificador del asociado remitente. (Obligatorio) |
| receiverQualifier | String | Calificador del asociado destinatario. (Obligatorio) |
| receiverIdentifier | String | Identificador del asociado destinatario. (Obligatorio) |
| agreementName | String | Nombre de mensajes de saludo de hello X12 acuerdo toowhich se resuelve. (Opcional) |
| dirección | Enum | Dirección de flujo de mensajes de Hola, recepción o envío. (Obligatorio) |
| interchangeControlNumber | String | Número de control de intercambio, que se rellena para hello el lado del envío cuando se recibe una confirmación técnica de socios comerciales. (Opcional) |
| functionalGroupControlNumber | String | Número de control de grupo funcional de confirmación técnica hello, que se rellena para hello el lado del envío cuando se recibe una confirmación técnica de socios comerciales. (Opcional) |
| isaSegment | string | Igual que el número de control de intercambio, pero se rellena solo en casos específicos. (Opcional) |
| gsSegment | string | Igual que el número de control de grupo funcional, pero se rellena solo en casos específicos. (Opcional) |
| respondingfunctionalGroupControlNumber | String | Número de control de grupo funcional original de Hola. (Opcional) |
| respondingFunctionalGroupId | String | Asigna tooAK101 en Id. de grupo funcional de confirmación de Hola. (Opcional) |
| isMessageFailed | Booleano | Si no se pudo mensaje hello X12. (Obligatorio) |
| statusCode | Enum | Código de estado de la confirmación. Los valores permitidos son **Accepted**, **Rejected**, y **AcceptedWithErrors**. (Obligatorio) |
| processingStatus | Enum | Estado de procesamiento de confirmación de Hola. Los valores permitidos son **Received**, **Generated** y **Sent**. (Obligatorio) |
| ak903 | String | Número de conjuntos de transacciones recibidos. (Opcional) |
| ak904 | String | Número de conjuntos de transacciones aceptados en el grupo funcional de hello identificado. (Opcional) |
| ak9Segment | String | Si el grupo funcional de hello identificado en el segmento de hello AK1 es aceptado o rechazado y el motivo. (Opcional) |

## <a name="next-steps"></a>Pasos siguientes
* Más información sobre la [supervisión de mensajes B2B](logic-apps-monitor-b2b-message.md).
* Más información sobre los [esquemas de seguimiento de AS2](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md).
* Más información sobre los [esquemas de seguimiento personalizado de B2B](../logic-apps/logic-apps-track-integration-account-custom-tracking-schema.md).
* Obtenga información acerca de [seguimiento de mensajes B2B en el portal de Operations Management Suite hello](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).
* Obtener más información sobre hello [paquete de integración empresarial](../logic-apps/logic-apps-enterprise-integration-overview.md).  
