---
title: "aaaAS2 esquemas de seguimiento para la supervisión de B2B - Azure Logic Apps | Documentos de Microsoft"
description: "Usar AS2 seguimiento de mensajes de toomonitor B2B de esquemas de las transacciones en la cuenta de la integración de Azure."
author: padmavc
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: f169c411-1bd7-4554-80c1-84351247bf94
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: fe3c5845e2e80160d6857d8c308d836e88af7331
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="start-or-enable-tracking-of-as2-messages-and-mdns-toomonitor-success-errors-and-message-properties"></a>Iniciar o activar el seguimiento de mensajes AS2 y MDN toomonitor correcto, errores y propiedades de mensaje
Puede utilizar estos esquemas de seguimiento de AS2 en su toohelp de cuenta de la integración de Azure supervisar las transacciones de negocio a negocio (B2B):

* Esquema de seguimiento de mensaje AS2
* Esquema de seguimiento de MDN AS2

## <a name="as2-message-tracking-schema"></a>Esquema de seguimiento de mensaje AS2
````java

    {
       "agreementProperties": {  
            "senderPartnerName": "",  
            "receiverPartnerName": "",  
            "as2To": "",  
            "as2From": "",  
            "agreementName": ""  
        },  
        "messageProperties": {
            "direction": "",
            "messageId": "",
            "dispositionType": "",
            "fileName": "",
            "isMessageFailed": "",
            "isMessageSigned": "",
            "isMessageEncrypted": "",
            "isMessageCompressed": "",
            "correlationMessageId": "",
            "incomingHeaders": {
            },
            "outgoingHeaders": {
            },
        "isNrrEnabled": "",
        "isMdnExpected": "",
        "mdnType": ""
        }
    }
````

| Propiedad | Escriba | Descripción |
| --- | --- | --- |
| senderPartnerName | string | Nombre de asociado del remitente del mensaje AS2. (Opcional) |
| receiverPartnerName | String | Nombre de asociado del destinatario del mensaje AS2. (Opcional) |
| as2To | String | Nombre del receptor del mensaje de AS2, de encabezados de saludo del mensaje de Hola AS2. (Obligatorio) |
| as2From | String | Nombre del remitente del mensaje de AS2, de encabezados de saludo del mensaje de Hola AS2. (Obligatorio) |
| agreementName | String | Nombre AS2 acuerdo toowhich Hola de mensajes de saludo se resuelven. (Opcional) |
| dirección | String | Dirección de flujo de mensajes de Hola, recepción o envío. (Obligatorio) |
| messageId | String | Id. de mensaje de AS2, de encabezados de saludo del mensaje de Hola AS2 (opcional) |
| dispositionType |string | Valor del tipo de disposición de notificación de disposición del mensaje (MDN). (Opcional) |
| fileName | String | Nombre de archivo de encabezado Hola de mensaje de saludo AS2. (Opcional) |
| isMessageFailed |Booleano | Si no se pudo mensaje de bienvenida de AS2. (Obligatorio) |
| isMessageSigned | Booleano | Si se firmó el mensaje de bienvenida AS2. (Obligatorio) |
| isMessageEncrypted | Booleano | Si se cifró el mensaje de bienvenida AS2. (Obligatorio) |
| isMessageCompressed |Booleano | Si se comprimió mensaje Hola AS2. (Obligatorio) |
| correlationMessageId | String | Identificador del mensaje AS2, toocorrelate mensajes con MDN. (Opcional) |
| incomingHeaders |Diccionario de JToken | Detalles del encabezado del mensaje AS2 entrante. (Opcional) |
| outgoingHeaders |Diccionario de JToken | Detalles del encabezado del mensaje AS2 saliente. (Opcional) |
| isNrrEnabled | Booleano | Usar valor predeterminado si no se conoce el valor de Hola. (Obligatorio) |
| isMdnExpected | Booleano | Usar valor predeterminado si no se conoce el valor de Hola. (Obligatorio) |
| mdnType | Enum | Los valores permitidos son **NotConfigured**, **Sync** y **Async**. (Obligatorio) |

## <a name="as2-mdn-tracking-schema"></a>Esquema de seguimiento de MDN AS2
````java

    {
        "agreementProperties": {
                "senderPartnerName": "",
                "receiverPartnerName": "",
                "as2To": "",
                "as2From": "",
                "agreementName": "g"
            },
            "messageProperties": {
                "direction": "",
                "messageId": "",
                "originalMessageId": "",
                "dispositionType": "",
                "isMessageFailed": "",
                "isMessageSigned": "",
                "isNrrEnabled": "",
                "statusCode": "",
                "micVerificationStatus": "",
                "correlationMessageId": "",
                "incomingHeaders": {
                },
                "outgoingHeaders": {
                }
            }
    }
````

| Propiedad | Escriba | Descripción |
| --- | --- | --- |
| senderPartnerName | string | Nombre de asociado del remitente del mensaje AS2. (Opcional) |
| receiverPartnerName | String | Nombre de asociado del destinatario del mensaje AS2. (Opcional) |
| as2To | String | Nombre del socio que recibe el mensaje de bienvenida AS2. (Obligatorio) |
| as2From | String | Nombre de socio comercial que envía el mensaje de bienvenida AS2. (Obligatorio) |
| agreementName | String | Nombre AS2 acuerdo toowhich Hola de mensajes de saludo se resuelven. (Opcional) |
| dirección |String | Dirección de flujo de mensajes de Hola, recepción o envío. (Obligatorio) |
| messageId | string | Identificador del mensaje AS2. (Opcional) |
| originalMessageId |string | Identificador del mensaje original AS2. (Opcional) |
| dispositionType | string | Valor de tipo de disposición de MDN. (Opcional) |
| isMessageFailed |Booleano | Si no se pudo mensaje de bienvenida de AS2. (Obligatorio) |
| isMessageSigned |Booleano | Si se firmó el mensaje de bienvenida AS2. (Obligatorio) |
| isNrrEnabled | Booleano | Usar valor predeterminado si no se conoce el valor de Hola. (Obligatorio) |
| statusCode | Enum | Los valores permitidos son **Accepted**, **Rejected**, y **AcceptedWithErrors**. (Obligatorio) |
| micVerificationStatus | Enum | Los valores permitidos son **NotApplicable**, **Succeeded** y **Failed**. (Obligatorio) |
| correlationMessageId | string | Id. de correlación. Id. de mensajes de Hola original (Hola identificador del mensaje de Hola para el que está configurando MDN). (Opcional) |
| incomingHeaders | Diccionario de JToken | Indica los detalles del encabezado del mensaje entrante. (Opcional) |
| outgoingHeaders |Diccionario de JToken | Indica los detalles del encabezado del mensaje saliente. (Opcional) |

## <a name="next-steps"></a>Pasos siguientes
* Obtener más información sobre hello [paquete de integración empresarial](../logic-apps/logic-apps-enterprise-integration-overview.md).    
* Más información sobre la [supervisión de mensajes B2B](logic-apps-monitor-b2b-message.md).   
* Más información sobre los [esquemas de seguimiento personalizado de B2B](logic-apps-track-integration-account-custom-tracking-schema.md).   
* Más información sobre los [esquemas de seguimiento de X12](logic-apps-track-integration-account-x12-tracking-schema.md).   
* Obtenga información acerca de [seguimiento de mensajes B2B en el portal de Operations Management Suite hello](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).
