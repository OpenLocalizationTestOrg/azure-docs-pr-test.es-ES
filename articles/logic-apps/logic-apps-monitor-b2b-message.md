---
title: "Supervisión de transacciones B2B y configuración de los registros: Azure Logic Apps | Microsoft Docs"
description: "Supervisión de mensajes AS2, X12 y EDIFACT, inicio del registro de diagnóstico para la cuenta de integración"
author: padmavc
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: bb7d9432-b697-44db-aa88-bd16ddfad23f
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 07/21/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: f717dae9a70a96944b623f22b90cf8c5a943f382
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="monitor-and-set-up-diagnostics-logging-for-b2b-communication-in-integration-accounts"></a><span data-ttu-id="0599a-103">Supervisión y configuración del registro de diagnóstico para la comunicación B2B en cuentas de integración</span><span class="sxs-lookup"><span data-stu-id="0599a-103">Monitor and set up diagnostics logging for B2B communication in integration accounts</span></span>

<span data-ttu-id="0599a-104">Después de configurar la comunicación B2B entre dos procesos o aplicaciones empresariales mediante la cuenta de integración, esas entidades pueden intercambiar mensajes entre sí.</span><span class="sxs-lookup"><span data-stu-id="0599a-104">After you set up B2B communication between two running business processes or applications through your integration account, those entities can exchange messages with each other.</span></span> <span data-ttu-id="0599a-105">Para confirmar que esta comunicación funciona según lo esperado, puede configurar la supervisión de los mensajes AS2, X12 y EDIFACT, junto con el registro de diagnóstico de la cuenta de integración mediante el servicio [Azure Log Analytics](../log-analytics/log-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0599a-105">To confirm this communication works as expected, you can set up monitoring for AS2, X12, and EDIFACT messages, along with diagnostics logging for your integration account through the [Azure Log Analytics](../log-analytics/log-analytics-overview.md) service.</span></span> <span data-ttu-id="0599a-106">Este servicio en [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md) supervisa los entornos locales y en la nube, lo que le permiten conservar la disponibilidad y el rendimiento, y también recopila detalles de entorno de tiempo de ejecución y eventos para lograr una depuración más completa.</span><span class="sxs-lookup"><span data-stu-id="0599a-106">This service in [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md) monitors your cloud and on-premises environments, helping you maintain their availability and performance, and also collects runtime details and events for richer debugging.</span></span> <span data-ttu-id="0599a-107">También puede [usar los datos de diagnóstico con otros servicios](#extend-diagnostic-data), como Azure Storage y Azure Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="0599a-107">You can also [use your diagnostic data with other services](#extend-diagnostic-data), like Azure Storage and Azure Event Hubs.</span></span>

## <a name="requirements"></a><span data-ttu-id="0599a-108">Requisitos</span><span class="sxs-lookup"><span data-stu-id="0599a-108">Requirements</span></span>

* <span data-ttu-id="0599a-109">Una aplicación lógica configurada con registro de diagnósticos.</span><span class="sxs-lookup"><span data-stu-id="0599a-109">A logic app that's set up with diagnostics logging.</span></span> <span data-ttu-id="0599a-110">Obtenga información sobre [cómo configurar el registro para esa aplicación lógica](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).</span><span class="sxs-lookup"><span data-stu-id="0599a-110">Learn [how to set up logging for that logic app](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).</span></span>

  > [!NOTE]
  > <span data-ttu-id="0599a-111">Una vez satisfecho este requisito, debería tener un área de trabajo en [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0599a-111">After you've met this requirement, you should have a workspace in the [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md).</span></span> <span data-ttu-id="0599a-112">Debe usar la misma área de trabajo de OMS cuando configure el registro para la cuenta de integración.</span><span class="sxs-lookup"><span data-stu-id="0599a-112">You should use the same OMS workspace when you set up logging for your integration account.</span></span> <span data-ttu-id="0599a-113">Si no tiene un área de trabajo de OMS, aprenda a [crear un área de trabajo de OMS](../log-analytics/log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="0599a-113">If you don't have an OMS workspace, learn [how to create an OMS workspace](../log-analytics/log-analytics-get-started.md).</span></span>

* <span data-ttu-id="0599a-114">Una cuenta de integración vinculada a la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="0599a-114">An integration account that's linked to your logic app.</span></span> <span data-ttu-id="0599a-115">Aprenda a [crear una cuenta de integración con un vínculo a la aplicación lógica](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md).</span><span class="sxs-lookup"><span data-stu-id="0599a-115">Learn [how to create an integration account with a link to your logic app](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md).</span></span>

## <a name="turn-on-diagnostics-logging-for-your-integration-account"></a><span data-ttu-id="0599a-116">Activación del registro de diagnóstico para la cuenta de integración</span><span class="sxs-lookup"><span data-stu-id="0599a-116">Turn on diagnostics logging for your integration account</span></span>

<span data-ttu-id="0599a-117">Puede activar el registro directamente desde la cuenta de integración o [mediante el servicio de Azure Monitor](#azure-monitor-service).</span><span class="sxs-lookup"><span data-stu-id="0599a-117">You can turn on logging either directly from your integration account or [through the Azure Monitor service](#azure-monitor-service).</span></span> <span data-ttu-id="0599a-118">Azure Monitor ofrece supervisión básica con datos de nivel de infraestructura.</span><span class="sxs-lookup"><span data-stu-id="0599a-118">Azure Monitor provides basic monitoring with infrastructure-level data.</span></span> <span data-ttu-id="0599a-119">Más información sobre [Azure Monitor](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md).</span><span class="sxs-lookup"><span data-stu-id="0599a-119">Learn more about [Azure Monitor](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md).</span></span>

### <a name="turn-on-diagnostics-logging-directly-from-your-integration-account"></a><span data-ttu-id="0599a-120">Activación del registro de diagnóstico directamente desde la cuenta de integración</span><span class="sxs-lookup"><span data-stu-id="0599a-120">Turn on diagnostics logging directly from your integration account</span></span>

1. <span data-ttu-id="0599a-121">En [Azure Portal](https://portal.azure.com), busque y seleccione la cuenta de integración.</span><span class="sxs-lookup"><span data-stu-id="0599a-121">In the [Azure portal](https://portal.azure.com), find and select your integration account.</span></span> <span data-ttu-id="0599a-122">En **Supervisión**, elija **Registros de diagnóstico** como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="0599a-122">Under **Monitoring**, choose **Diagnostics logs** as shown here:</span></span>

   ![Buscar y seleccionar la cuenta de integración, elegir "Registros de diagnóstico"](media/logic-apps-monitor-b2b-message/integration-account-diagnostics.png)

2. <span data-ttu-id="0599a-124">Cuando selecciona la cuenta de integración, los valores siguientes se seleccionan de forma automática.</span><span class="sxs-lookup"><span data-stu-id="0599a-124">After you select your integration account, the following values are automatically selected.</span></span> <span data-ttu-id="0599a-125">Si los valores son correctos, elija **Activar diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="0599a-125">If these values are correct, choose **Turn on diagnostics**.</span></span> <span data-ttu-id="0599a-126">De lo contrario, seleccione los valores que desea:</span><span class="sxs-lookup"><span data-stu-id="0599a-126">Otherwise, select the values that you want:</span></span>

   1. <span data-ttu-id="0599a-127">En **Suscripción**, seleccione la suscripción de Azure que usa con la cuenta de integración.</span><span class="sxs-lookup"><span data-stu-id="0599a-127">Under **Subscription**, select the Azure subscription that you use with your integration account.</span></span>
   2. <span data-ttu-id="0599a-128">En **Grupo de recursos**, seleccione el grupo de recursos que usa con la cuenta de integración.</span><span class="sxs-lookup"><span data-stu-id="0599a-128">Under **Resource group**, select the resource group that you use with your integration account.</span></span>
   3. <span data-ttu-id="0599a-129">En **Tipo de recurso**, seleccione **Cuentas de integración**.</span><span class="sxs-lookup"><span data-stu-id="0599a-129">Under **Resource type**, select **Integration accounts**.</span></span> 
   4. <span data-ttu-id="0599a-130">En **Resource**, seleccione la cuenta de integración.</span><span class="sxs-lookup"><span data-stu-id="0599a-130">Under **Resource**, select your integration account.</span></span> 
   5. <span data-ttu-id="0599a-131">Elija **Activar diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="0599a-131">Choose **Turn on diagnostics**.</span></span>

   ![Configuración de diagnósticos para la cuenta de integración](media/logic-apps-monitor-b2b-message/turn-on-diagnostics-integration-account.png)

3. <span data-ttu-id="0599a-133">En **Configuración de diagnóstico**, **Estado**, elija **Activado**.</span><span class="sxs-lookup"><span data-stu-id="0599a-133">Under **Diagnostics settings**, and then **Status**, choose **On**.</span></span>

   ![Activación de Diagnósticos de Azure](media/logic-apps-monitor-b2b-message/turn-on-diagnostics-integration-account-2.png)

4. <span data-ttu-id="0599a-135">Ahora seleccione el área de trabajo de OMS y los datos para usar en el registro de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="0599a-135">Now select the OMS workspace and data to use for logging as shown:</span></span>

   1. <span data-ttu-id="0599a-136">Seleccione **Enviar a Log Analytics**.</span><span class="sxs-lookup"><span data-stu-id="0599a-136">Select **Send to Log Analytics**.</span></span> 
   2. <span data-ttu-id="0599a-137">En **Log Analytics**, elija **Configurar**.</span><span class="sxs-lookup"><span data-stu-id="0599a-137">Under **Log Analytics**, choose **Configure**.</span></span> 
   3. <span data-ttu-id="0599a-138">En **Áreas de trabajo de OMS**, seleccione el área de trabajo de OMS que va a usar para el registro.</span><span class="sxs-lookup"><span data-stu-id="0599a-138">Under **OMS Workspaces**, select the OMS workspace to use for logging.</span></span>
   4. <span data-ttu-id="0599a-139">En **Registro**, seleccione la categoría **IntegrationAccountTrackingEvents**.</span><span class="sxs-lookup"><span data-stu-id="0599a-139">Under **Log**, select the **IntegrationAccountTrackingEvents** category.</span></span>
   5. <span data-ttu-id="0599a-140">Elija **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="0599a-140">Choose **Save**.</span></span>

   ![Configuración de Log Analytics para que pueda enviar datos de diagnóstico a un registro](media/logic-apps-monitor-b2b-message/send-diagnostics-data-log-analytics-workspace.png)

5. <span data-ttu-id="0599a-142">Ahora [configure el seguimiento de los mensajes B2B en OMS](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span><span class="sxs-lookup"><span data-stu-id="0599a-142">Now [set up tracking for your B2B messages in OMS](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span></span>

<a name="azure-monitor-service"></a>

### <a name="turn-on-diagnostics-logging-through-azure-monitor"></a><span data-ttu-id="0599a-143">Activación del registro de diagnóstico mediante Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="0599a-143">Turn on diagnostics logging through Azure Monitor</span></span>

1. <span data-ttu-id="0599a-144">En [Azure Portal](https://portal.azure.com), en el menú principal de Azure, elija **Supervisar**, **Registro de diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="0599a-144">In the [Azure portal](https://portal.azure.com), on the main Azure menu, choose **Monitor**, **Diagnostics logs**.</span></span> <span data-ttu-id="0599a-145">Luego, seleccione la cuenta de integración como se muestra aquí:</span><span class="sxs-lookup"><span data-stu-id="0599a-145">Then select your integration account as shown here:</span></span>

   ![Elija "Supervisar", "Registros de diagnóstico", seleccione la cuenta de integración.](media/logic-apps-monitor-b2b-message/monitor-service-diagnostics-logs.png)

2. <span data-ttu-id="0599a-147">Cuando selecciona la cuenta de integración, los valores siguientes se seleccionan de forma automática.</span><span class="sxs-lookup"><span data-stu-id="0599a-147">After you select your integration account, the following values are automatically selected.</span></span> <span data-ttu-id="0599a-148">Si los valores son correctos, elija **Activar diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="0599a-148">If these values are correct, choose **Turn on diagnostics**.</span></span> <span data-ttu-id="0599a-149">De lo contrario, seleccione los valores que desea:</span><span class="sxs-lookup"><span data-stu-id="0599a-149">Otherwise, select the values that you want:</span></span>

   1. <span data-ttu-id="0599a-150">En **Suscripción**, seleccione la suscripción de Azure que usa con la cuenta de integración.</span><span class="sxs-lookup"><span data-stu-id="0599a-150">Under **Subscription**, select the Azure subscription that you use with your integration account.</span></span>
   2. <span data-ttu-id="0599a-151">En **Grupo de recursos**, seleccione el grupo de recursos que usa con la cuenta de integración.</span><span class="sxs-lookup"><span data-stu-id="0599a-151">Under **Resource group**, select the resource group that you use with your integration account.</span></span>
   3. <span data-ttu-id="0599a-152">En **Tipo de recurso**, seleccione **Cuentas de integración**.</span><span class="sxs-lookup"><span data-stu-id="0599a-152">Under **Resource type**, select **Integration accounts**.</span></span>
   4. <span data-ttu-id="0599a-153">En **Resource**, seleccione la cuenta de integración.</span><span class="sxs-lookup"><span data-stu-id="0599a-153">Under **Resource**, select your integration account.</span></span>
   5. <span data-ttu-id="0599a-154">Elija **Activar diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="0599a-154">Choose **Turn on diagnostics**.</span></span>

   ![Configuración de diagnósticos para la cuenta de integración](media/logic-apps-monitor-b2b-message/turn-on-diagnostics-integration-account.png)

3. <span data-ttu-id="0599a-156">En **Configuración de diagnóstico**, elija **Activado**.</span><span class="sxs-lookup"><span data-stu-id="0599a-156">Under **Diagnostics settings**, choose **On**.</span></span>

   ![Activación de Diagnósticos de Azure](media/logic-apps-monitor-b2b-message/turn-on-diagnostics-integration-account-2.png)

4. <span data-ttu-id="0599a-158">Ahora seleccione el área de trabajo de OMS y la categoría de evento para el registro como se muestra:</span><span class="sxs-lookup"><span data-stu-id="0599a-158">Now select the OMS workspace and event category for logging as shown:</span></span>

   1. <span data-ttu-id="0599a-159">Seleccione **Enviar a Log Analytics**.</span><span class="sxs-lookup"><span data-stu-id="0599a-159">Select **Send to Log Analytics**.</span></span> 
   2. <span data-ttu-id="0599a-160">En **Log Analytics**, elija **Configurar**.</span><span class="sxs-lookup"><span data-stu-id="0599a-160">Under **Log Analytics**, choose **Configure**.</span></span> 
   3. <span data-ttu-id="0599a-161">En **Áreas de trabajo de OMS**, seleccione el área de trabajo de OMS que va a usar para el registro.</span><span class="sxs-lookup"><span data-stu-id="0599a-161">Under **OMS Workspaces**, select the OMS workspace to use for logging.</span></span>
   4. <span data-ttu-id="0599a-162">En **Registro**, seleccione la categoría **IntegrationAccountTrackingEvents**.</span><span class="sxs-lookup"><span data-stu-id="0599a-162">Under **Log**, select the **IntegrationAccountTrackingEvents** category.</span></span>
   5. <span data-ttu-id="0599a-163">Cuando termine, seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="0599a-163">When you're done, choose **Save**.</span></span>

   ![Configuración de Log Analytics para que pueda enviar datos de diagnóstico a un registro](media/logic-apps-monitor-b2b-message/send-diagnostics-data-log-analytics-workspace.png)

5. <span data-ttu-id="0599a-165">Ahora [configure el seguimiento de los mensajes B2B en OMS](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span><span class="sxs-lookup"><span data-stu-id="0599a-165">Now [set up tracking for your B2B messages in OMS](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span></span>

## <a name="extend-how-and-where-you-use-diagnostic-data-with-other-services"></a><span data-ttu-id="0599a-166">Extensión de cómo y dónde usa los datos de diagnóstico con otros servicios</span><span class="sxs-lookup"><span data-stu-id="0599a-166">Extend how and where you use diagnostic data with other services</span></span>

<span data-ttu-id="0599a-167">Además de con Azure Log Analytics, puede usar los datos de diagnóstico de la aplicación lógica con otros servicios de Azure, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="0599a-167">Along with Azure Log Analytics, you can extend how you use your logic app's diagnostic data with other Azure services, for example:</span></span> 

* [<span data-ttu-id="0599a-168">Archivar registros de Diagnósticos de Azure en Azure Storage</span><span class="sxs-lookup"><span data-stu-id="0599a-168">Archive Azure Diagnostics Logs in Azure Storage</span></span>](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md)
* [<span data-ttu-id="0599a-169">Transmitir registros de Diagnósticos de Azure a Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="0599a-169">Stream Azure Diagnostics Logs to Azure Event Hubs</span></span>](../monitoring-and-diagnostics/monitoring-stream-diagnostic-logs-to-event-hubs.md) 

<span data-ttu-id="0599a-170">Luego puede obtener supervisión en tiempo real mediante la telemetría y los análisis de otros servicios, como [Azure Stream Analytics](../stream-analytics/stream-analytics-introduction.md) y [Power BI](../log-analytics/log-analytics-powerbi.md).</span><span class="sxs-lookup"><span data-stu-id="0599a-170">You can then get real-time monitoring by using telemetry and analytics from other services, like [Azure Stream Analytics](../stream-analytics/stream-analytics-introduction.md) and [Power BI](../log-analytics/log-analytics-powerbi.md).</span></span> <span data-ttu-id="0599a-171">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="0599a-171">For example:</span></span>

* [<span data-ttu-id="0599a-172">Transmitir datos de Event Hubs a Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="0599a-172">Stream data from Event Hubs to Stream Analytics</span></span>](../stream-analytics/stream-analytics-define-inputs.md)
* [<span data-ttu-id="0599a-173">Analizar datos que se están transmitiendo con Stream Analytics y crear un panel de análisis en tiempo real en Power BI</span><span class="sxs-lookup"><span data-stu-id="0599a-173">Analyze streaming data with Stream Analytics and create a real-time analytics dashboard in Power BI</span></span>](../stream-analytics/stream-analytics-power-bi-dashboard.md)

<span data-ttu-id="0599a-174">Según las opciones que quiera configurar, primero asegúrese de [crear una cuenta de Azure Storage](../storage/common/storage-create-storage-account.md) o [crear un centro de eventos de Azure](../event-hubs/event-hubs-create.md).</span><span class="sxs-lookup"><span data-stu-id="0599a-174">Based on the options that you want set up, make sure that you first [create an Azure storage account](../storage/common/storage-create-storage-account.md) or [create an Azure event hub](../event-hubs/event-hubs-create.md).</span></span> <span data-ttu-id="0599a-175">Luego seleccione las opciones para el envío de los datos de diagnóstico:</span><span class="sxs-lookup"><span data-stu-id="0599a-175">Then select the options for where you want to send diagnostic data:</span></span>

![Envío de los datos a una cuenta de Azure Storage o a un centro de eventos](./media/logic-apps-monitor-b2b-message/storage-account-event-hubs.png)

> [!NOTE]
> <span data-ttu-id="0599a-177">Los períodos de retención solo se aplican cuando se usa una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="0599a-177">Retention periods apply only when you choose to use a storage account.</span></span>

## <a name="supported-tracking-schemas"></a><span data-ttu-id="0599a-178">Esquemas de seguimiento compatibles</span><span class="sxs-lookup"><span data-stu-id="0599a-178">Supported tracking schemas</span></span>

<span data-ttu-id="0599a-179">Azure admite los siguientes tipos de esquema de seguimiento, de los que todos, salvo el tipo personalizado, tienen esquemas fijos.</span><span class="sxs-lookup"><span data-stu-id="0599a-179">Azure supports these tracking schema types, which all have fixed schemas except the Custom type.</span></span>

* [<span data-ttu-id="0599a-180">Esquema de seguimiento de AS2</span><span class="sxs-lookup"><span data-stu-id="0599a-180">AS2 tracking schema</span></span>](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md)
* [<span data-ttu-id="0599a-181">Esquemas de seguimiento de X12</span><span class="sxs-lookup"><span data-stu-id="0599a-181">X12 tracking schema</span></span>](../logic-apps/logic-apps-track-integration-account-x12-tracking-schema.md)
* [<span data-ttu-id="0599a-182">Esquema de seguimiento personalizado</span><span class="sxs-lookup"><span data-stu-id="0599a-182">Custom tracking schema</span></span>](../logic-apps/logic-apps-track-integration-account-custom-tracking-schema.md)

## <a name="next-steps"></a><span data-ttu-id="0599a-183">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0599a-183">Next steps</span></span>

* [<span data-ttu-id="0599a-184">Seguimiento de mensajes B2B en OMS</span><span class="sxs-lookup"><span data-stu-id="0599a-184">Track B2B messages in OMS</span></span>](../logic-apps/logic-apps-track-b2b-messages-omsportal.md "Seguimiento de mensajes B2B en OMS")
* [<span data-ttu-id="0599a-185">Más información sobre Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="0599a-185">Learn more about the Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md "Información sobre Enterprise Integration Pack")

