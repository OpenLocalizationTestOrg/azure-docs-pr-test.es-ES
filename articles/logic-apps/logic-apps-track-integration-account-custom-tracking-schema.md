---
title: "aaaCustom seguimiento esquemas para B2B supervisión: las aplicaciones lógicas de Azure | Documentos de Microsoft"
description: "Crear esquemas de seguimiento personalizado toomonitor B2B mensajes de las transacciones en la cuenta de la integración de Azure."
author: padmavc
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 433ae852-a833-44d3-a3c3-14cca33403a2
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8cf26a43d89f0414a2a8c5ef59d804235afeb5d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="enable-tracking-toomonitor-your-complete-workflow-end-to-end"></a>Habilitar el seguimiento toomonitor el flujo de trabajo completo,-to-end
Hay disponible una característica de seguimiento integrada que puede habilitar para las distintas partes de su flujo de trabajo de negocio a negocio, por ejemplo, para realizar un seguimiento de mensajes AS2 o X12. Al crear flujos de trabajo que incluye una lógica de aplicación, BizTalk Server, SQL Server o cualquier otra capa, a continuación, puede habilitar el seguimiento personalizado que registra los eventos de fin de toohello de Hola a partir del flujo de trabajo. 

En este tema se proporciona código personalizado que puede usar en las capas de hello fuera de la aplicación lógica. 

## <a name="custom-tracking-schema"></a>Esquema de seguimiento personalizado
````java

        {
            "sourceType": "",
            "source": {

            "workflow": {
                "systemId": ""
            },
            "runInstance": {
                "runId": ""
            },
            "operation": {
                "operationName": "",
                "repeatItemScopeName": "",
                "repeatItemIndex": "",
                "trackingId": "",
                "correlationId": "",
                "clientRequestId": ""
                }
            },
            "events": [
            {
                "eventLevel": "",
                "eventTime": "",
                "recordType": "",
                "record": {                
                }
            }
         ]
      }

````

| Propiedad | Escriba | Descripción |
| --- | --- | --- |
| sourceType |   | Tipo de origen de hello ejecutar. Los valores permitidos son **Microsoft.Logic/workflows** y **custom**. (Obligatorio). |
| Origen |   | Si es de tipo de origen de hello **Microsoft.Logic/workflows**, información de origen de hello necesita toofollow este esquema. Si es de tipo de origen de hello **personalizado**, esquema de hello es un JToken. (Obligatorio) |
| systemId | String | Id. de sistema de aplicación lógica. (Obligatorio). |
| runId | string | Id. de ejecución de aplicación lógica. (Obligatorio). |
| operationName | String | Nombre de operación de hello (por ejemplo, la acción o el desencadenador). (Obligatorio) |
| repeatItemScopeName | String | Repita el nombre del elemento si acción de hello está dentro de un `foreach` / `until` bucle. (Obligatorio) |
| repeatItemIndex | Entero | Si acción de hello está dentro de un `foreach` / `until` bucle. Indica el índice del elemento repetido de Hola. (Obligatorio) |
| trackingId | String | Id. de seguimiento, mensajes de saludo de toocorrelate. (Opcional) |
| correlationId | String | Id. de correlación, mensajes de saludo de toocorrelate. (Opcional) |
| clientRequestId | String | Cliente puede rellenar toocorrelate mensajes. (Opcional) |
| eventLevel |   | Nivel de evento de Hola. (Obligatorio) |
| eventTime |   | Hora del evento de hello, en formato aaaa-MM-DDTHH:MM:SS.00000Z de UTC. (Obligatorio) |
| recordType |   | Tipo de registro de seguimiento de Hola. El valor permitido es **custom**. (Obligatorio). |
| record |   | Tipo de registro personalizado. El formato permitido es JToken. (Obligatorio). |

## <a name="b2b-protocol-tracking-schemas"></a>Esquemas de seguimiento de protocolos B2B
Para obtener información sobre los esquemas de seguimiento de protocolos B2B, consulte:
* [Esquemas de seguimiento de AS2](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md)   
* [Esquemas de seguimiento de X12](logic-apps-track-integration-account-x12-tracking-schema.md)

## <a name="next-steps"></a>Pasos siguientes
* Más información sobre la [supervisión de mensajes B2B](logic-apps-monitor-b2b-message.md).   
* Obtenga información acerca de [seguimiento de mensajes B2B en el portal de Operations Management Suite hello](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).
* Obtener más información sobre hello [paquete de integración empresarial](../logic-apps/logic-apps-enterprise-integration-overview.md).
