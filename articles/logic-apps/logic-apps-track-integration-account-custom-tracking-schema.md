---
title: "Esquemas de seguimiento personalizados para la supervisión de B2B - Azure Logic Apps | Microsoft Docs"
description: "Cree esquemas de seguimiento personalizados para supervisar mensajes B2B de transacciones en la cuenta de la integración de Azure."
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
ms.openlocfilehash: b71a4938dde2a71f1ce29403af7aa9101358d64c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="enable-tracking-to-monitor-your-complete-workflow-end-to-end"></a><span data-ttu-id="9abca-103">Habilitación del seguimiento para supervisar el flujo de trabajo completo de manera integral</span><span class="sxs-lookup"><span data-stu-id="9abca-103">Enable tracking to monitor your complete workflow, end-to-end</span></span>
<span data-ttu-id="9abca-104">Hay disponible una característica de seguimiento integrada que puede habilitar para las distintas partes de su flujo de trabajo de negocio a negocio, por ejemplo, para realizar un seguimiento de mensajes AS2 o X12.</span><span class="sxs-lookup"><span data-stu-id="9abca-104">There is built-in tracking that you can enable for different parts of your business-to-business workflow, such as tracking AS2 or X12 messages.</span></span> <span data-ttu-id="9abca-105">Cuando cree flujos de trabajo que incluyan una lógica de aplicación, BizTalk Server, SQL Server o cualquier otra capa, podrá habilitar el seguimiento personalizado que registre los eventos desde el principio hasta el final del flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="9abca-105">When you create workflows that includes a logic app, BizTalk Server, SQL Server, or any other layer, then you can enable custom tracking that logs events from the beginning to the end of your workflow.</span></span> 

<span data-ttu-id="9abca-106">En este tema se proporciona un código personalizado que puede usar en las capas externas de la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="9abca-106">This topic provides custom code that you can use in the layers outside of your logic app.</span></span> 

## <a name="custom-tracking-schema"></a><span data-ttu-id="9abca-107">Esquema de seguimiento personalizado</span><span class="sxs-lookup"><span data-stu-id="9abca-107">Custom tracking schema</span></span>
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

| <span data-ttu-id="9abca-108">Propiedad</span><span class="sxs-lookup"><span data-stu-id="9abca-108">Property</span></span> | <span data-ttu-id="9abca-109">Escriba</span><span class="sxs-lookup"><span data-stu-id="9abca-109">Type</span></span> | <span data-ttu-id="9abca-110">Descripción</span><span class="sxs-lookup"><span data-stu-id="9abca-110">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9abca-111">sourceType</span><span class="sxs-lookup"><span data-stu-id="9abca-111">sourceType</span></span> |   | <span data-ttu-id="9abca-112">Tipo del origen de ejecución.</span><span class="sxs-lookup"><span data-stu-id="9abca-112">Type of the run source.</span></span> <span data-ttu-id="9abca-113">Los valores permitidos son **Microsoft.Logic/workflows** y **custom**.</span><span class="sxs-lookup"><span data-stu-id="9abca-113">Allowed values are **Microsoft.Logic/workflows** and **custom**.</span></span> <span data-ttu-id="9abca-114">(Obligatorio).</span><span class="sxs-lookup"><span data-stu-id="9abca-114">(Mandatory)</span></span> |
| <span data-ttu-id="9abca-115">Origen</span><span class="sxs-lookup"><span data-stu-id="9abca-115">Source</span></span> |   | <span data-ttu-id="9abca-116">Si el tipo de origen es **Microsoft.Logic/workflows**, la información de origen tiene que ir detrás de este esquema.</span><span class="sxs-lookup"><span data-stu-id="9abca-116">If the source type is **Microsoft.Logic/workflows**, the source information needs to follow this schema.</span></span> <span data-ttu-id="9abca-117">Si el tipo de origen es **custom**, el esquema es un JToken</span><span class="sxs-lookup"><span data-stu-id="9abca-117">If the source type is **custom**, the schema is a JToken.</span></span> <span data-ttu-id="9abca-118">(Obligatorio).</span><span class="sxs-lookup"><span data-stu-id="9abca-118">(Mandatory)</span></span> |
| <span data-ttu-id="9abca-119">systemId</span><span class="sxs-lookup"><span data-stu-id="9abca-119">systemId</span></span> | <span data-ttu-id="9abca-120">String</span><span class="sxs-lookup"><span data-stu-id="9abca-120">String</span></span> | <span data-ttu-id="9abca-121">Id. de sistema de aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="9abca-121">Logic app system ID.</span></span> <span data-ttu-id="9abca-122">(Obligatorio).</span><span class="sxs-lookup"><span data-stu-id="9abca-122">(Mandatory)</span></span> |
| <span data-ttu-id="9abca-123">runId</span><span class="sxs-lookup"><span data-stu-id="9abca-123">runId</span></span> | <span data-ttu-id="9abca-124">string</span><span class="sxs-lookup"><span data-stu-id="9abca-124">String</span></span> | <span data-ttu-id="9abca-125">Id. de ejecución de aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="9abca-125">Logic app run ID.</span></span> <span data-ttu-id="9abca-126">(Obligatorio).</span><span class="sxs-lookup"><span data-stu-id="9abca-126">(Mandatory)</span></span> |
| <span data-ttu-id="9abca-127">operationName</span><span class="sxs-lookup"><span data-stu-id="9abca-127">operationName</span></span> | <span data-ttu-id="9abca-128">string</span><span class="sxs-lookup"><span data-stu-id="9abca-128">String</span></span> | <span data-ttu-id="9abca-129">Nombre de la operación (por ejemplo, acción o desencadenador).</span><span class="sxs-lookup"><span data-stu-id="9abca-129">Name of the operation (for example, action or trigger).</span></span> <span data-ttu-id="9abca-130">(Obligatorio).</span><span class="sxs-lookup"><span data-stu-id="9abca-130">(Mandatory)</span></span> |
| <span data-ttu-id="9abca-131">repeatItemScopeName</span><span class="sxs-lookup"><span data-stu-id="9abca-131">repeatItemScopeName</span></span> | <span data-ttu-id="9abca-132">String</span><span class="sxs-lookup"><span data-stu-id="9abca-132">String</span></span> | <span data-ttu-id="9abca-133">Repita el nombre del elemento si la acción se encuentra dentro de un bucle `foreach`/`until`.</span><span class="sxs-lookup"><span data-stu-id="9abca-133">Repeat item name if the action is inside a `foreach`/`until` loop.</span></span> <span data-ttu-id="9abca-134">(Obligatorio).</span><span class="sxs-lookup"><span data-stu-id="9abca-134">(Mandatory)</span></span> |
| <span data-ttu-id="9abca-135">repeatItemIndex</span><span class="sxs-lookup"><span data-stu-id="9abca-135">repeatItemIndex</span></span> | <span data-ttu-id="9abca-136">Entero </span><span class="sxs-lookup"><span data-stu-id="9abca-136">Integer</span></span> | <span data-ttu-id="9abca-137">Si la acción se encuentra dentro de un bucle `foreach`/`until`.</span><span class="sxs-lookup"><span data-stu-id="9abca-137">Whether the action is inside a `foreach`/`until` loop.</span></span> <span data-ttu-id="9abca-138">Indica el índice del elemento repetido.</span><span class="sxs-lookup"><span data-stu-id="9abca-138">Indicates the repeated item index.</span></span> <span data-ttu-id="9abca-139">(Obligatorio).</span><span class="sxs-lookup"><span data-stu-id="9abca-139">(Mandatory)</span></span> |
| <span data-ttu-id="9abca-140">trackingId</span><span class="sxs-lookup"><span data-stu-id="9abca-140">trackingId</span></span> | <span data-ttu-id="9abca-141">String</span><span class="sxs-lookup"><span data-stu-id="9abca-141">String</span></span> | <span data-ttu-id="9abca-142">Id. de seguimiento para correlacionar los mensajes.</span><span class="sxs-lookup"><span data-stu-id="9abca-142">Tracking ID, to correlate the messages.</span></span> <span data-ttu-id="9abca-143">(Opcional).</span><span class="sxs-lookup"><span data-stu-id="9abca-143">(Optional)</span></span> |
| <span data-ttu-id="9abca-144">correlationId</span><span class="sxs-lookup"><span data-stu-id="9abca-144">correlationId</span></span> | <span data-ttu-id="9abca-145">String</span><span class="sxs-lookup"><span data-stu-id="9abca-145">String</span></span> | <span data-ttu-id="9abca-146">Id. de correlación para correlacionar los mensajes.</span><span class="sxs-lookup"><span data-stu-id="9abca-146">Correlation ID, to correlate the messages.</span></span> <span data-ttu-id="9abca-147">(Opcional).</span><span class="sxs-lookup"><span data-stu-id="9abca-147">(Optional)</span></span> |
| <span data-ttu-id="9abca-148">clientRequestId</span><span class="sxs-lookup"><span data-stu-id="9abca-148">clientRequestId</span></span> | <span data-ttu-id="9abca-149">String</span><span class="sxs-lookup"><span data-stu-id="9abca-149">String</span></span> | <span data-ttu-id="9abca-150">El cliente puede rellenarlo para correlacionar mensajes.</span><span class="sxs-lookup"><span data-stu-id="9abca-150">Client can populate it to correlate messages.</span></span> <span data-ttu-id="9abca-151">(Opcional).</span><span class="sxs-lookup"><span data-stu-id="9abca-151">(Optional)</span></span> |
| <span data-ttu-id="9abca-152">eventLevel</span><span class="sxs-lookup"><span data-stu-id="9abca-152">eventLevel</span></span> |   | <span data-ttu-id="9abca-153">Nivel del evento.</span><span class="sxs-lookup"><span data-stu-id="9abca-153">Level of the event.</span></span> <span data-ttu-id="9abca-154">(Obligatorio).</span><span class="sxs-lookup"><span data-stu-id="9abca-154">(Mandatory)</span></span> |
| <span data-ttu-id="9abca-155">eventTime</span><span class="sxs-lookup"><span data-stu-id="9abca-155">eventTime</span></span> |   | <span data-ttu-id="9abca-156">Hora del evento, en formato UTC: AAAA-MM-DDTHH:MM:SS.00000Z.</span><span class="sxs-lookup"><span data-stu-id="9abca-156">Time of the event, in UTC format YYYY-MM-DDTHH:MM:SS.00000Z.</span></span> <span data-ttu-id="9abca-157">(Obligatorio).</span><span class="sxs-lookup"><span data-stu-id="9abca-157">(Mandatory)</span></span> |
| <span data-ttu-id="9abca-158">recordType</span><span class="sxs-lookup"><span data-stu-id="9abca-158">recordType</span></span> |   | <span data-ttu-id="9abca-159">Tipo del registro.</span><span class="sxs-lookup"><span data-stu-id="9abca-159">Type of the track record.</span></span> <span data-ttu-id="9abca-160">El valor permitido es **custom**.</span><span class="sxs-lookup"><span data-stu-id="9abca-160">Allowed value is **custom**.</span></span> <span data-ttu-id="9abca-161">(Obligatorio).</span><span class="sxs-lookup"><span data-stu-id="9abca-161">(Mandatory)</span></span> |
| <span data-ttu-id="9abca-162">record</span><span class="sxs-lookup"><span data-stu-id="9abca-162">record</span></span> |   | <span data-ttu-id="9abca-163">Tipo de registro personalizado.</span><span class="sxs-lookup"><span data-stu-id="9abca-163">Custom record type.</span></span> <span data-ttu-id="9abca-164">El formato permitido es JToken.</span><span class="sxs-lookup"><span data-stu-id="9abca-164">Allowed format is JToken.</span></span> <span data-ttu-id="9abca-165">(Obligatorio).</span><span class="sxs-lookup"><span data-stu-id="9abca-165">(Mandatory)</span></span> |

## <a name="b2b-protocol-tracking-schemas"></a><span data-ttu-id="9abca-166">Esquemas de seguimiento de protocolos B2B</span><span class="sxs-lookup"><span data-stu-id="9abca-166">B2B protocol tracking schemas</span></span>
<span data-ttu-id="9abca-167">Para obtener información sobre los esquemas de seguimiento de protocolos B2B, consulte:</span><span class="sxs-lookup"><span data-stu-id="9abca-167">For information about B2B protocol tracking schemas, see:</span></span>
* [<span data-ttu-id="9abca-168">Esquemas de seguimiento de AS2</span><span class="sxs-lookup"><span data-stu-id="9abca-168">AS2 tracking schemas</span></span>](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md)   
* [<span data-ttu-id="9abca-169">Esquemas de seguimiento de X12</span><span class="sxs-lookup"><span data-stu-id="9abca-169">X12 tracking schemas</span></span>](logic-apps-track-integration-account-x12-tracking-schema.md)

## <a name="next-steps"></a><span data-ttu-id="9abca-170">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9abca-170">Next steps</span></span>
* <span data-ttu-id="9abca-171">Más información sobre la [supervisión de mensajes B2B](logic-apps-monitor-b2b-message.md)</span><span class="sxs-lookup"><span data-stu-id="9abca-171">Learn more about [monitoring B2B messages](logic-apps-monitor-b2b-message.md).</span></span>   
* <span data-ttu-id="9abca-172">Más información sobre el [seguimiento de mensajes B2B en el portal de Operations Management Suite](../logic-apps/logic-apps-track-b2b-messages-omsportal.md)</span><span class="sxs-lookup"><span data-stu-id="9abca-172">Learn about [tracking B2B messages in the Operations Management Suite portal](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span></span>
* <span data-ttu-id="9abca-173">Más información sobre el [Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md)</span><span class="sxs-lookup"><span data-stu-id="9abca-173">Learn more about the [Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md).</span></span>
