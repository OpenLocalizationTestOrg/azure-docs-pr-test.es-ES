---
title: "Resolución de descodificación de edifact de Logic Apps B2B UNH2.5 - Azure Logic Apps | Microsoft Docs"
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
ms.openlocfilehash: 62ad8183cc6e9f56255b2729a04ee7710d00a21a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-handle-edifact-documents-having-unh25-segment"></a><span data-ttu-id="d5260-103">Administración de documentos EDIFACT que tienen segmentos UNH2.5</span><span class="sxs-lookup"><span data-stu-id="d5260-103">How to handle EDIFACT documents having UNH2.5 segment</span></span>
<span data-ttu-id="d5260-104">Si UNH2.5 está presente en el documento EDIFACT, se va a usar para la búsqueda de esquema.</span><span class="sxs-lookup"><span data-stu-id="d5260-104">When UNH2.5 is present in the EDIFACT document, it is being used for schema lookup.</span></span> 

<span data-ttu-id="d5260-105">Ejemplo: El campo UNH es **EAN008** en el mensaje EDIFACT</span><span class="sxs-lookup"><span data-stu-id="d5260-105">Example: The UNH field is **EAN008** in the EDIFACT message</span></span>  
<span data-ttu-id="d5260-106">UNH+SSDD1+ORDERS:D:03B:UN:**EAN008**'</span><span class="sxs-lookup"><span data-stu-id="d5260-106">UNH+SSDD1+ORDERS:D:03B:UN:**EAN008**'</span></span>  

<span data-ttu-id="d5260-107">Pasos que deben seguirse para controlar el mensaje:</span><span class="sxs-lookup"><span data-stu-id="d5260-107">Steps to follow to handle the message</span></span> 
1. <span data-ttu-id="d5260-108">Revisión del esquema</span><span class="sxs-lookup"><span data-stu-id="d5260-108">Update the schema</span></span>
2. <span data-ttu-id="d5260-109">Comprobación de la configuración del acuerdo</span><span class="sxs-lookup"><span data-stu-id="d5260-109">Check the agreement settings</span></span>  

## <a name="update-the-schema"></a><span data-ttu-id="d5260-110">Revisión del esquema</span><span class="sxs-lookup"><span data-stu-id="d5260-110">Update the schema</span></span>
<span data-ttu-id="d5260-111">Para procesar el mensaje, debe implementar un esquema con el nombre del nodo raíz UNH2.5.</span><span class="sxs-lookup"><span data-stu-id="d5260-111">To process the message, you need to deploy a schema with the UNH2.5 root node name.</span></span>  <span data-ttu-id="d5260-112">Para un ejemplo dado, el nombre de raíz de esquema sería **EFACT_D03B_ORDERS_EAN008**.</span><span class="sxs-lookup"><span data-stu-id="d5260-112">For given an example, the schema root name would be **EFACT_D03B_ORDERS_EAN008**</span></span>  

<span data-ttu-id="d5260-113">Para cada D03B_ORDERS con un segmento UNH2.5 diferente, tendría que implementar un esquema individual.</span><span class="sxs-lookup"><span data-stu-id="d5260-113">For each D03B_ORDERS with a different UNH2.5 segment, you would have to deploy an individual schema.</span></span>  

## <a name="add-schema-to-the-edifact-agreement"></a><span data-ttu-id="d5260-114">Incorporación de un esquema al acuerdo de EDIFACT</span><span class="sxs-lookup"><span data-stu-id="d5260-114">Add schema to the EDIFACT agreement</span></span>
### <a name="edifact-decode"></a><span data-ttu-id="d5260-115">Descodificación EDIFACT</span><span class="sxs-lookup"><span data-stu-id="d5260-115">EDIFACT Decode</span></span>
<span data-ttu-id="d5260-116">Para descodificar el mensaje entrante, configure el esquema en la configuración de recepción del acuerdo EDIFACT:</span><span class="sxs-lookup"><span data-stu-id="d5260-116">To Decode the incoming message, configure the schema in the EDIFACT agreement receive settings</span></span>
1. <span data-ttu-id="d5260-117">Agregue el esquema a la cuenta de integración.</span><span class="sxs-lookup"><span data-stu-id="d5260-117">Add the schema to the integration account</span></span>    
2. <span data-ttu-id="d5260-118">Configure el esquema en la configuración de recepción del acuerdo EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="d5260-118">Configure the schema in the EDIFACT agreement receive settings.</span></span> 
3. <span data-ttu-id="d5260-119">Seleccione el acuerdo EDIFACT y haga clic en **Editar como JSON**.</span><span class="sxs-lookup"><span data-stu-id="d5260-119">Select EDIFACT agreement and click **Edit as JSON**.</span></span>  <span data-ttu-id="d5260-120">Agregue un valor UNH2.5 en el acuerdo de recepción **schemaReferences**
![](./media/logic-apps-enterprise-integration-edifact_inputfile_unh2.5/image1.png).</span><span class="sxs-lookup"><span data-stu-id="d5260-120">Add UNH2.5 value in the Receive Agreement **schemaReferences**
![](./media/logic-apps-enterprise-integration-edifact_inputfile_unh2.5/image1.png)</span></span>

### <a name="edifact-encode"></a><span data-ttu-id="d5260-121">Codificación EDIFACT</span><span class="sxs-lookup"><span data-stu-id="d5260-121">EDIFACT Encode</span></span>
<span data-ttu-id="d5260-122">Para codificar el mensaje entrante, configure el esquema en la configuración de envío del acuerdo EDIFACT:</span><span class="sxs-lookup"><span data-stu-id="d5260-122">To Encode the incoming message, configure the schema in the EDIFACT agreement send settings</span></span>
1. <span data-ttu-id="d5260-123">Agregue el esquema a la cuenta de integración.</span><span class="sxs-lookup"><span data-stu-id="d5260-123">Add the schema to the integration account</span></span>    
2. <span data-ttu-id="d5260-124">Configure el esquema en la configuración de envío del acuerdo EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="d5260-124">Configure the schema in the EDIFACT agreement send settings.</span></span> 
3. <span data-ttu-id="d5260-125">Seleccione el acuerdo EDIFACT y haga clic en **Editar como JSON**.</span><span class="sxs-lookup"><span data-stu-id="d5260-125">Select EDIFACT agreement and click **Edit as JSON**.</span></span>  <span data-ttu-id="d5260-126">Agregue un valor UNH2.5 en el acuerdo de envío **schemaReferences**
![](./media/logic-apps-enterprise-integration-edifact_inputfile_unh2.5/image2.png).</span><span class="sxs-lookup"><span data-stu-id="d5260-126">Add UNH2.5 value in the Send Agreement **schemaReferences**
![](./media/logic-apps-enterprise-integration-edifact_inputfile_unh2.5/image2.png)</span></span>

## <a name="next-steps"></a><span data-ttu-id="d5260-127">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d5260-127">Next Steps</span></span>
* [<span data-ttu-id="d5260-128">Más información sobre los acuerdos de cuentas de integración</span><span class="sxs-lookup"><span data-stu-id="d5260-128">Learn more about integration account agreements</span></span>](../logic-apps/logic-apps-enterprise-integration-agreements.md "Más información sobre los acuerdos de cuentas de integración")  