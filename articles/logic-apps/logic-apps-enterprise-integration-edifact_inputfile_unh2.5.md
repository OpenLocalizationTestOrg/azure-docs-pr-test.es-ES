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
# <a name="how-toohandle-edifact-documents-having-unh25-segment"></a><span data-ttu-id="3bd9f-103">¿Cómo documenta tener UNH2.5 toohandle EDIFACT segmento</span><span class="sxs-lookup"><span data-stu-id="3bd9f-103">How toohandle EDIFACT documents having UNH2.5 segment</span></span>
<span data-ttu-id="3bd9f-104">Si UNH2.5 está presente en el documento EDIFACT de hello, que se sirve para búsqueda de esquemas.</span><span class="sxs-lookup"><span data-stu-id="3bd9f-104">When UNH2.5 is present in hello EDIFACT document, it is being used for schema lookup.</span></span> 

<span data-ttu-id="3bd9f-105">Ejemplo: Hola UNH campo es **EAN008** en el mensaje de saludo EDIFACT</span><span class="sxs-lookup"><span data-stu-id="3bd9f-105">Example: hello UNH field is **EAN008** in hello EDIFACT message</span></span>  
<span data-ttu-id="3bd9f-106">UNH+SSDD1+ORDERS:D:03B:UN:**EAN008**'</span><span class="sxs-lookup"><span data-stu-id="3bd9f-106">UNH+SSDD1+ORDERS:D:03B:UN:**EAN008**'</span></span>  

<span data-ttu-id="3bd9f-107">Mensaje de bienvenida de pasos toofollow toohandle</span><span class="sxs-lookup"><span data-stu-id="3bd9f-107">Steps toofollow toohandle hello message</span></span> 
1. <span data-ttu-id="3bd9f-108">Actualizar el esquema de Hola</span><span class="sxs-lookup"><span data-stu-id="3bd9f-108">Update hello schema</span></span>
2. <span data-ttu-id="3bd9f-109">Compruebe la configuración de acuerdo de Hola</span><span class="sxs-lookup"><span data-stu-id="3bd9f-109">Check hello agreement settings</span></span>  

## <a name="update-hello-schema"></a><span data-ttu-id="3bd9f-110">Actualizar el esquema de Hola</span><span class="sxs-lookup"><span data-stu-id="3bd9f-110">Update hello schema</span></span>
<span data-ttu-id="3bd9f-111">mensaje de saludo tooprocess, deberá toodeploy un esquema con el nombre de nodo raíz de hello UNH2.5.</span><span class="sxs-lookup"><span data-stu-id="3bd9f-111">tooprocess hello message, you need toodeploy a schema with hello UNH2.5 root node name.</span></span>  <span data-ttu-id="3bd9f-112">Determinados un ejemplo, el nombre de raíz del esquema de hello sería **EFACT_D03B_ORDERS_EAN008**</span><span class="sxs-lookup"><span data-stu-id="3bd9f-112">For given an example, hello schema root name would be **EFACT_D03B_ORDERS_EAN008**</span></span>  

<span data-ttu-id="3bd9f-113">Para cada D03B_ORDERS con un segmento UNH2.5 diferente, deberá toodeploy un esquema en particular.</span><span class="sxs-lookup"><span data-stu-id="3bd9f-113">For each D03B_ORDERS with a different UNH2.5 segment, you would have toodeploy an individual schema.</span></span>  

## <a name="add-schema-toohello-edifact-agreement"></a><span data-ttu-id="3bd9f-114">Agregar el acuerdo de EDIFACT toohello de esquema</span><span class="sxs-lookup"><span data-stu-id="3bd9f-114">Add schema toohello EDIFACT agreement</span></span>
### <a name="edifact-decode"></a><span data-ttu-id="3bd9f-115">Descodificación EDIFACT</span><span class="sxs-lookup"><span data-stu-id="3bd9f-115">EDIFACT Decode</span></span>
<span data-ttu-id="3bd9f-116">tooDecode Hola mensaje entrante, configure el esquema de Hola Hola EDIFACT configuración de recepción de acuerdo</span><span class="sxs-lookup"><span data-stu-id="3bd9f-116">tooDecode hello incoming message, configure hello schema in hello EDIFACT agreement receive settings</span></span>
1. <span data-ttu-id="3bd9f-117">Agregar cuenta de integración de hello esquema toohello</span><span class="sxs-lookup"><span data-stu-id="3bd9f-117">Add hello schema toohello integration account</span></span>    
2. <span data-ttu-id="3bd9f-118">Configurar el esquema de Hola Hola EDIFACT configuración de recepción de acuerdo.</span><span class="sxs-lookup"><span data-stu-id="3bd9f-118">Configure hello schema in hello EDIFACT agreement receive settings.</span></span> 
3. <span data-ttu-id="3bd9f-119">Seleccione el acuerdo EDIFACT y haga clic en **Editar como JSON**.</span><span class="sxs-lookup"><span data-stu-id="3bd9f-119">Select EDIFACT agreement and click **Edit as JSON**.</span></span>  <span data-ttu-id="3bd9f-120">Agregue el valor UNH2.5 en hello acuerdo de recepción **schemaReferences**
![](./media/logic-apps-enterprise-integration-edifact_inputfile_unh2.5/image1.png)</span><span class="sxs-lookup"><span data-stu-id="3bd9f-120">Add UNH2.5 value in hello Receive Agreement **schemaReferences**
![](./media/logic-apps-enterprise-integration-edifact_inputfile_unh2.5/image1.png)</span></span>

### <a name="edifact-encode"></a><span data-ttu-id="3bd9f-121">Codificación EDIFACT</span><span class="sxs-lookup"><span data-stu-id="3bd9f-121">EDIFACT Encode</span></span>
<span data-ttu-id="3bd9f-122">tooEncode Hola mensaje entrante, configure el esquema de hello en la configuración de envío de acuerdo de EDIFACT de Hola</span><span class="sxs-lookup"><span data-stu-id="3bd9f-122">tooEncode hello incoming message, configure hello schema in hello EDIFACT agreement send settings</span></span>
1. <span data-ttu-id="3bd9f-123">Agregar cuenta de integración de hello esquema toohello</span><span class="sxs-lookup"><span data-stu-id="3bd9f-123">Add hello schema toohello integration account</span></span>    
2. <span data-ttu-id="3bd9f-124">Configurar el esquema de hello en la configuración de envío de acuerdo de EDIFACT de Hola.</span><span class="sxs-lookup"><span data-stu-id="3bd9f-124">Configure hello schema in hello EDIFACT agreement send settings.</span></span> 
3. <span data-ttu-id="3bd9f-125">Seleccione el acuerdo EDIFACT y haga clic en **Editar como JSON**.</span><span class="sxs-lookup"><span data-stu-id="3bd9f-125">Select EDIFACT agreement and click **Edit as JSON**.</span></span>  <span data-ttu-id="3bd9f-126">Agregue el valor UNH2.5 en hello Enviar acuerdo **schemaReferences**
![](./media/logic-apps-enterprise-integration-edifact_inputfile_unh2.5/image2.png)</span><span class="sxs-lookup"><span data-stu-id="3bd9f-126">Add UNH2.5 value in hello Send Agreement **schemaReferences**
![](./media/logic-apps-enterprise-integration-edifact_inputfile_unh2.5/image2.png)</span></span>

## <a name="next-steps"></a><span data-ttu-id="3bd9f-127">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3bd9f-127">Next Steps</span></span>
* [<span data-ttu-id="3bd9f-128">Más información sobre los acuerdos de cuentas de integración</span><span class="sxs-lookup"><span data-stu-id="3bd9f-128">Learn more about integration account agreements</span></span>](../logic-apps/logic-apps-enterprise-integration-agreements.md "Más información sobre los acuerdos de cuentas de integración")  