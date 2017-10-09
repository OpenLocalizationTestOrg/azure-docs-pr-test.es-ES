---
title: aaaLogic B2B aplicaciones descodificar edifact resolver UNH2.5 - Azure Logic Apps | Documentos de Microsoft
description: "Resolución de descodificación de edifact de Azure Logic Apps B2B UNH2.5"
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
ms.date: 04/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 6d85242d0f828fa52cdc9689938f3ba1e51b1183
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toohandle-edifact-documents-having-unh25-segment"></a>¿Cómo documenta tener UNH2.5 toohandle EDIFACT segmento
Si UNH2.5 está presente en el documento EDIFACT de hello, que se sirve para búsqueda de esquemas. 

Ejemplo: Hola UNH campo es **EAN008** en el mensaje de saludo EDIFACT  
UNH+SSDD1+ORDERS:D:03B:UN:**EAN008**'  

Mensaje de bienvenida de pasos toofollow toohandle 
1. Actualizar el esquema de Hola
2. Compruebe la configuración de acuerdo de Hola  

## <a name="update-hello-schema"></a>Actualizar el esquema de Hola
mensaje de saludo tooprocess, deberá toodeploy un esquema con el nombre de nodo raíz de hello UNH2.5.  Determinados un ejemplo, el nombre de raíz del esquema de hello sería **EFACT_D03B_ORDERS_EAN008**  

Para cada D03B_ORDERS con un segmento UNH2.5 diferente, deberá toodeploy un esquema en particular.  

## <a name="add-schema-toohello-edifact-agreement"></a>Agregar el acuerdo de EDIFACT toohello de esquema
### <a name="edifact-decode"></a>Descodificación EDIFACT
tooDecode Hola mensaje entrante, configure el esquema de Hola Hola EDIFACT configuración de recepción de acuerdo
1. Agregar cuenta de integración de hello esquema toohello    
2. Configurar el esquema de Hola Hola EDIFACT configuración de recepción de acuerdo. 
3. Seleccione el acuerdo EDIFACT y haga clic en **Editar como JSON**.  Agregue el valor UNH2.5 en hello acuerdo de recepción **schemaReferences**
![](./media/logic-apps-enterprise-integration-edifact_inputfile_unh2.5/image1.png)

### <a name="edifact-encode"></a>Codificación EDIFACT
tooEncode Hola mensaje entrante, configure el esquema de hello en la configuración de envío de acuerdo de EDIFACT de Hola
1. Agregar cuenta de integración de hello esquema toohello    
2. Configurar el esquema de hello en la configuración de envío de acuerdo de EDIFACT de Hola. 
3. Seleccione el acuerdo EDIFACT y haga clic en **Editar como JSON**.  Agregue el valor UNH2.5 en hello Enviar acuerdo **schemaReferences**
![](./media/logic-apps-enterprise-integration-edifact_inputfile_unh2.5/image2.png)

## <a name="next-steps"></a>Pasos siguientes
* [Más información sobre los acuerdos de cuentas de integración](../logic-apps/logic-apps-enterprise-integration-agreements.md "Más información sobre los acuerdos de cuentas de integración")  