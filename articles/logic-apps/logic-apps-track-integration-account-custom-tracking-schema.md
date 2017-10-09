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
# <a name="enable-tracking-toomonitor-your-complete-workflow-end-to-end"></a><span data-ttu-id="eef0b-103">Habilitar el seguimiento toomonitor el flujo de trabajo completo,-to-end</span><span class="sxs-lookup"><span data-stu-id="eef0b-103">Enable tracking toomonitor your complete workflow, end-to-end</span></span>
<span data-ttu-id="eef0b-104">Hay disponible una característica de seguimiento integrada que puede habilitar para las distintas partes de su flujo de trabajo de negocio a negocio, por ejemplo, para realizar un seguimiento de mensajes AS2 o X12.</span><span class="sxs-lookup"><span data-stu-id="eef0b-104">There is built-in tracking that you can enable for different parts of your business-to-business workflow, such as tracking AS2 or X12 messages.</span></span> <span data-ttu-id="eef0b-105">Al crear flujos de trabajo que incluye una lógica de aplicación, BizTalk Server, SQL Server o cualquier otra capa, a continuación, puede habilitar el seguimiento personalizado que registra los eventos de fin de toohello de Hola a partir del flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="eef0b-105">When you create workflows that includes a logic app, BizTalk Server, SQL Server, or any other layer, then you can enable custom tracking that logs events from hello beginning toohello end of your workflow.</span></span> 

<span data-ttu-id="eef0b-106">En este tema se proporciona código personalizado que puede usar en las capas de hello fuera de la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="eef0b-106">This topic provides custom code that you can use in hello layers outside of your logic app.</span></span> 

## <a name="custom-tracking-schema"></a><span data-ttu-id="eef0b-107">Esquema de seguimiento personalizado</span><span class="sxs-lookup"><span data-stu-id="eef0b-107">Custom tracking schema</span></span>
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

| <span data-ttu-id="eef0b-108">Propiedad</span><span class="sxs-lookup"><span data-stu-id="eef0b-108">Property</span></span> | <span data-ttu-id="eef0b-109">Escriba</span><span class="sxs-lookup"><span data-stu-id="eef0b-109">Type</span></span> | <span data-ttu-id="eef0b-110">Descripción</span><span class="sxs-lookup"><span data-stu-id="eef0b-110">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="eef0b-111">sourceType</span><span class="sxs-lookup"><span data-stu-id="eef0b-111">sourceType</span></span> |   | <span data-ttu-id="eef0b-112">Tipo de origen de hello ejecutar.</span><span class="sxs-lookup"><span data-stu-id="eef0b-112">Type of hello run source.</span></span> <span data-ttu-id="eef0b-113">Los valores permitidos son **Microsoft.Logic/workflows** y **custom**.</span><span class="sxs-lookup"><span data-stu-id="eef0b-113">Allowed values are **Microsoft.Logic/workflows** and **custom**.</span></span> <span data-ttu-id="eef0b-114">(Obligatorio).</span><span class="sxs-lookup"><span data-stu-id="eef0b-114">(Mandatory)</span></span> |
| <span data-ttu-id="eef0b-115">Origen</span><span class="sxs-lookup"><span data-stu-id="eef0b-115">Source</span></span> |   | <span data-ttu-id="eef0b-116">Si es de tipo de origen de hello **Microsoft.Logic/workflows**, información de origen de hello necesita toofollow este esquema.</span><span class="sxs-lookup"><span data-stu-id="eef0b-116">If hello source type is **Microsoft.Logic/workflows**, hello source information needs toofollow this schema.</span></span> <span data-ttu-id="eef0b-117">Si es de tipo de origen de hello **personalizado**, esquema de hello es un JToken.</span><span class="sxs-lookup"><span data-stu-id="eef0b-117">If hello source type is **custom**, hello schema is a JToken.</span></span> <span data-ttu-id="eef0b-118">(Obligatorio)</span><span class="sxs-lookup"><span data-stu-id="eef0b-118">(Mandatory)</span></span> |
| <span data-ttu-id="eef0b-119">systemId</span><span class="sxs-lookup"><span data-stu-id="eef0b-119">systemId</span></span> | <span data-ttu-id="eef0b-120">String</span><span class="sxs-lookup"><span data-stu-id="eef0b-120">String</span></span> | <span data-ttu-id="eef0b-121">Id. de sistema de aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="eef0b-121">Logic app system ID.</span></span> <span data-ttu-id="eef0b-122">(Obligatorio).</span><span class="sxs-lookup"><span data-stu-id="eef0b-122">(Mandatory)</span></span> |
| <span data-ttu-id="eef0b-123">runId</span><span class="sxs-lookup"><span data-stu-id="eef0b-123">runId</span></span> | <span data-ttu-id="eef0b-124">string</span><span class="sxs-lookup"><span data-stu-id="eef0b-124">String</span></span> | <span data-ttu-id="eef0b-125">Id. de ejecución de aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="eef0b-125">Logic app run ID.</span></span> <span data-ttu-id="eef0b-126">(Obligatorio).</span><span class="sxs-lookup"><span data-stu-id="eef0b-126">(Mandatory)</span></span> |
| <span data-ttu-id="eef0b-127">operationName</span><span class="sxs-lookup"><span data-stu-id="eef0b-127">operationName</span></span> | <span data-ttu-id="eef0b-128">String</span><span class="sxs-lookup"><span data-stu-id="eef0b-128">String</span></span> | <span data-ttu-id="eef0b-129">Nombre de operación de hello (por ejemplo, la acción o el desencadenador).</span><span class="sxs-lookup"><span data-stu-id="eef0b-129">Name of hello operation (for example, action or trigger).</span></span> <span data-ttu-id="eef0b-130">(Obligatorio)</span><span class="sxs-lookup"><span data-stu-id="eef0b-130">(Mandatory)</span></span> |
| <span data-ttu-id="eef0b-131">repeatItemScopeName</span><span class="sxs-lookup"><span data-stu-id="eef0b-131">repeatItemScopeName</span></span> | <span data-ttu-id="eef0b-132">String</span><span class="sxs-lookup"><span data-stu-id="eef0b-132">String</span></span> | <span data-ttu-id="eef0b-133">Repita el nombre del elemento si acción de hello está dentro de un `foreach` / `until` bucle.</span><span class="sxs-lookup"><span data-stu-id="eef0b-133">Repeat item name if hello action is inside a `foreach`/`until` loop.</span></span> <span data-ttu-id="eef0b-134">(Obligatorio)</span><span class="sxs-lookup"><span data-stu-id="eef0b-134">(Mandatory)</span></span> |
| <span data-ttu-id="eef0b-135">repeatItemIndex</span><span class="sxs-lookup"><span data-stu-id="eef0b-135">repeatItemIndex</span></span> | <span data-ttu-id="eef0b-136">Entero</span><span class="sxs-lookup"><span data-stu-id="eef0b-136">Integer</span></span> | <span data-ttu-id="eef0b-137">Si acción de hello está dentro de un `foreach` / `until` bucle.</span><span class="sxs-lookup"><span data-stu-id="eef0b-137">Whether hello action is inside a `foreach`/`until` loop.</span></span> <span data-ttu-id="eef0b-138">Indica el índice del elemento repetido de Hola.</span><span class="sxs-lookup"><span data-stu-id="eef0b-138">Indicates hello repeated item index.</span></span> <span data-ttu-id="eef0b-139">(Obligatorio)</span><span class="sxs-lookup"><span data-stu-id="eef0b-139">(Mandatory)</span></span> |
| <span data-ttu-id="eef0b-140">trackingId</span><span class="sxs-lookup"><span data-stu-id="eef0b-140">trackingId</span></span> | <span data-ttu-id="eef0b-141">String</span><span class="sxs-lookup"><span data-stu-id="eef0b-141">String</span></span> | <span data-ttu-id="eef0b-142">Id. de seguimiento, mensajes de saludo de toocorrelate.</span><span class="sxs-lookup"><span data-stu-id="eef0b-142">Tracking ID, toocorrelate hello messages.</span></span> <span data-ttu-id="eef0b-143">(Opcional)</span><span class="sxs-lookup"><span data-stu-id="eef0b-143">(Optional)</span></span> |
| <span data-ttu-id="eef0b-144">correlationId</span><span class="sxs-lookup"><span data-stu-id="eef0b-144">correlationId</span></span> | <span data-ttu-id="eef0b-145">String</span><span class="sxs-lookup"><span data-stu-id="eef0b-145">String</span></span> | <span data-ttu-id="eef0b-146">Id. de correlación, mensajes de saludo de toocorrelate.</span><span class="sxs-lookup"><span data-stu-id="eef0b-146">Correlation ID, toocorrelate hello messages.</span></span> <span data-ttu-id="eef0b-147">(Opcional)</span><span class="sxs-lookup"><span data-stu-id="eef0b-147">(Optional)</span></span> |
| <span data-ttu-id="eef0b-148">clientRequestId</span><span class="sxs-lookup"><span data-stu-id="eef0b-148">clientRequestId</span></span> | <span data-ttu-id="eef0b-149">String</span><span class="sxs-lookup"><span data-stu-id="eef0b-149">String</span></span> | <span data-ttu-id="eef0b-150">Cliente puede rellenar toocorrelate mensajes.</span><span class="sxs-lookup"><span data-stu-id="eef0b-150">Client can populate it toocorrelate messages.</span></span> <span data-ttu-id="eef0b-151">(Opcional)</span><span class="sxs-lookup"><span data-stu-id="eef0b-151">(Optional)</span></span> |
| <span data-ttu-id="eef0b-152">eventLevel</span><span class="sxs-lookup"><span data-stu-id="eef0b-152">eventLevel</span></span> |   | <span data-ttu-id="eef0b-153">Nivel de evento de Hola.</span><span class="sxs-lookup"><span data-stu-id="eef0b-153">Level of hello event.</span></span> <span data-ttu-id="eef0b-154">(Obligatorio)</span><span class="sxs-lookup"><span data-stu-id="eef0b-154">(Mandatory)</span></span> |
| <span data-ttu-id="eef0b-155">eventTime</span><span class="sxs-lookup"><span data-stu-id="eef0b-155">eventTime</span></span> |   | <span data-ttu-id="eef0b-156">Hora del evento de hello, en formato aaaa-MM-DDTHH:MM:SS.00000Z de UTC.</span><span class="sxs-lookup"><span data-stu-id="eef0b-156">Time of hello event, in UTC format YYYY-MM-DDTHH:MM:SS.00000Z.</span></span> <span data-ttu-id="eef0b-157">(Obligatorio)</span><span class="sxs-lookup"><span data-stu-id="eef0b-157">(Mandatory)</span></span> |
| <span data-ttu-id="eef0b-158">recordType</span><span class="sxs-lookup"><span data-stu-id="eef0b-158">recordType</span></span> |   | <span data-ttu-id="eef0b-159">Tipo de registro de seguimiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="eef0b-159">Type of hello track record.</span></span> <span data-ttu-id="eef0b-160">El valor permitido es **custom**.</span><span class="sxs-lookup"><span data-stu-id="eef0b-160">Allowed value is **custom**.</span></span> <span data-ttu-id="eef0b-161">(Obligatorio).</span><span class="sxs-lookup"><span data-stu-id="eef0b-161">(Mandatory)</span></span> |
| <span data-ttu-id="eef0b-162">record</span><span class="sxs-lookup"><span data-stu-id="eef0b-162">record</span></span> |   | <span data-ttu-id="eef0b-163">Tipo de registro personalizado.</span><span class="sxs-lookup"><span data-stu-id="eef0b-163">Custom record type.</span></span> <span data-ttu-id="eef0b-164">El formato permitido es JToken.</span><span class="sxs-lookup"><span data-stu-id="eef0b-164">Allowed format is JToken.</span></span> <span data-ttu-id="eef0b-165">(Obligatorio).</span><span class="sxs-lookup"><span data-stu-id="eef0b-165">(Mandatory)</span></span> |

## <a name="b2b-protocol-tracking-schemas"></a><span data-ttu-id="eef0b-166">Esquemas de seguimiento de protocolos B2B</span><span class="sxs-lookup"><span data-stu-id="eef0b-166">B2B protocol tracking schemas</span></span>
<span data-ttu-id="eef0b-167">Para obtener información sobre los esquemas de seguimiento de protocolos B2B, consulte:</span><span class="sxs-lookup"><span data-stu-id="eef0b-167">For information about B2B protocol tracking schemas, see:</span></span>
* [<span data-ttu-id="eef0b-168">Esquemas de seguimiento de AS2</span><span class="sxs-lookup"><span data-stu-id="eef0b-168">AS2 tracking schemas</span></span>](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md)   
* [<span data-ttu-id="eef0b-169">Esquemas de seguimiento de X12</span><span class="sxs-lookup"><span data-stu-id="eef0b-169">X12 tracking schemas</span></span>](logic-apps-track-integration-account-x12-tracking-schema.md)

## <a name="next-steps"></a><span data-ttu-id="eef0b-170">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="eef0b-170">Next steps</span></span>
* <span data-ttu-id="eef0b-171">Más información sobre la [supervisión de mensajes B2B](logic-apps-monitor-b2b-message.md).</span><span class="sxs-lookup"><span data-stu-id="eef0b-171">Learn more about [monitoring B2B messages](logic-apps-monitor-b2b-message.md).</span></span>   
* <span data-ttu-id="eef0b-172">Obtenga información acerca de [seguimiento de mensajes B2B en el portal de Operations Management Suite hello](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span><span class="sxs-lookup"><span data-stu-id="eef0b-172">Learn about [tracking B2B messages in hello Operations Management Suite portal](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span></span>
* <span data-ttu-id="eef0b-173">Obtener más información sobre hello [paquete de integración empresarial](../logic-apps/logic-apps-enterprise-integration-overview.md).</span><span class="sxs-lookup"><span data-stu-id="eef0b-173">Learn more about hello [Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md).</span></span>
