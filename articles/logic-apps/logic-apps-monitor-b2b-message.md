---
title: "las transacciones de aaaMonitor B2B y configurar el registro: las aplicaciones lógicas de Azure | Documentos de Microsoft"
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
ms.openlocfilehash: a6745ebf41aab331020bfec072f5806711d125bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-set-up-diagnostics-logging-for-b2b-communication-in-integration-accounts"></a><span data-ttu-id="56546-103">Supervisión y configuración del registro de diagnóstico para la comunicación B2B en cuentas de integración</span><span class="sxs-lookup"><span data-stu-id="56546-103">Monitor and set up diagnostics logging for B2B communication in integration accounts</span></span>

<span data-ttu-id="56546-104">Después de configurar la comunicación B2B entre dos procesos o aplicaciones empresariales mediante la cuenta de integración, esas entidades pueden intercambiar mensajes entre sí.</span><span class="sxs-lookup"><span data-stu-id="56546-104">After you set up B2B communication between two running business processes or applications through your integration account, those entities can exchange messages with each other.</span></span> <span data-ttu-id="56546-105">tooconfirm esta comunicación funciona según lo previsto, puede configurar la supervisión de AS2, X12, y mensajes EDIFACT, junto con el registro de diagnósticos para su cuenta de integración a través de hello [Azure Log Analytics](../log-analytics/log-analytics-overview.md) servicio.</span><span class="sxs-lookup"><span data-stu-id="56546-105">tooconfirm this communication works as expected, you can set up monitoring for AS2, X12, and EDIFACT messages, along with diagnostics logging for your integration account through hello [Azure Log Analytics](../log-analytics/log-analytics-overview.md) service.</span></span> <span data-ttu-id="56546-106">Este servicio en [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md) supervisa los entornos locales y en la nube, lo que le permiten conservar la disponibilidad y el rendimiento, y también recopila detalles de entorno de tiempo de ejecución y eventos para lograr una depuración más completa.</span><span class="sxs-lookup"><span data-stu-id="56546-106">This service in [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md) monitors your cloud and on-premises environments, helping you maintain their availability and performance, and also collects runtime details and events for richer debugging.</span></span> <span data-ttu-id="56546-107">También puede [usar los datos de diagnóstico con otros servicios](#extend-diagnostic-data), como Azure Storage y Azure Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="56546-107">You can also [use your diagnostic data with other services](#extend-diagnostic-data), like Azure Storage and Azure Event Hubs.</span></span>

## <a name="requirements"></a><span data-ttu-id="56546-108">Requisitos</span><span class="sxs-lookup"><span data-stu-id="56546-108">Requirements</span></span>

* <span data-ttu-id="56546-109">Una aplicación lógica configurada con registro de diagnósticos.</span><span class="sxs-lookup"><span data-stu-id="56546-109">A logic app that's set up with diagnostics logging.</span></span> <span data-ttu-id="56546-110">Obtenga información acerca de [cómo tooset el registro para esa aplicación lógica](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).</span><span class="sxs-lookup"><span data-stu-id="56546-110">Learn [how tooset up logging for that logic app](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).</span></span>

  > [!NOTE]
  > <span data-ttu-id="56546-111">Después de que se ha cumplido este requisito, debe tener un área de trabajo en hello [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md).</span><span class="sxs-lookup"><span data-stu-id="56546-111">After you've met this requirement, you should have a workspace in hello [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md).</span></span> <span data-ttu-id="56546-112">Debe usar Hola la misma área de trabajo OMS al configurar el registro para la cuenta de integración.</span><span class="sxs-lookup"><span data-stu-id="56546-112">You should use hello same OMS workspace when you set up logging for your integration account.</span></span> <span data-ttu-id="56546-113">Si no tiene un área de trabajo OMS, descubra [cómo toocreate un área de trabajo OMS](../log-analytics/log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="56546-113">If you don't have an OMS workspace, learn [how toocreate an OMS workspace](../log-analytics/log-analytics-get-started.md).</span></span>

* <span data-ttu-id="56546-114">Una cuenta de integración que se ha vinculado la aplicación lógica de tooyour.</span><span class="sxs-lookup"><span data-stu-id="56546-114">An integration account that's linked tooyour logic app.</span></span> <span data-ttu-id="56546-115">Obtenga información acerca de [cómo toocreate la integración de una cuenta con una aplicación de lógica de vínculo tooyour](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md).</span><span class="sxs-lookup"><span data-stu-id="56546-115">Learn [how toocreate an integration account with a link tooyour logic app](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md).</span></span>

## <a name="turn-on-diagnostics-logging-for-your-integration-account"></a><span data-ttu-id="56546-116">Activación del registro de diagnóstico para la cuenta de integración</span><span class="sxs-lookup"><span data-stu-id="56546-116">Turn on diagnostics logging for your integration account</span></span>

<span data-ttu-id="56546-117">Puede activar el registro directamente desde su cuenta de integración o [a través de hello Azure supervisar servicio](#azure-monitor-service).</span><span class="sxs-lookup"><span data-stu-id="56546-117">You can turn on logging either directly from your integration account or [through hello Azure Monitor service](#azure-monitor-service).</span></span> <span data-ttu-id="56546-118">Azure Monitor ofrece supervisión básica con datos de nivel de infraestructura.</span><span class="sxs-lookup"><span data-stu-id="56546-118">Azure Monitor provides basic monitoring with infrastructure-level data.</span></span> <span data-ttu-id="56546-119">Más información sobre [Azure Monitor](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md).</span><span class="sxs-lookup"><span data-stu-id="56546-119">Learn more about [Azure Monitor](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md).</span></span>

### <a name="turn-on-diagnostics-logging-directly-from-your-integration-account"></a><span data-ttu-id="56546-120">Activación del registro de diagnóstico directamente desde la cuenta de integración</span><span class="sxs-lookup"><span data-stu-id="56546-120">Turn on diagnostics logging directly from your integration account</span></span>

1. <span data-ttu-id="56546-121">Hola [portal de Azure](https://portal.azure.com), busque y seleccione su cuenta de integración.</span><span class="sxs-lookup"><span data-stu-id="56546-121">In hello [Azure portal](https://portal.azure.com), find and select your integration account.</span></span> <span data-ttu-id="56546-122">En **Supervisión**, elija **Registros de diagnóstico** como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="56546-122">Under **Monitoring**, choose **Diagnostics logs** as shown here:</span></span>

   ![Buscar y seleccionar la cuenta de integración, elegir "Registros de diagnóstico"](media/logic-apps-monitor-b2b-message/integration-account-diagnostics.png)

2. <span data-ttu-id="56546-124">Después de seleccionar su cuenta de integración, Hola después de los valores se selecciona automáticamente.</span><span class="sxs-lookup"><span data-stu-id="56546-124">After you select your integration account, hello following values are automatically selected.</span></span> <span data-ttu-id="56546-125">Si los valores son correctos, elija **Activar diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="56546-125">If these values are correct, choose **Turn on diagnostics**.</span></span> <span data-ttu-id="56546-126">También puede seleccionar valores de hello que desee:</span><span class="sxs-lookup"><span data-stu-id="56546-126">Otherwise, select hello values that you want:</span></span>

   1. <span data-ttu-id="56546-127">En **suscripción**, seleccione Hola suscripción de Azure que se utiliza con su cuenta de integración.</span><span class="sxs-lookup"><span data-stu-id="56546-127">Under **Subscription**, select hello Azure subscription that you use with your integration account.</span></span>
   2. <span data-ttu-id="56546-128">En **grupo de recursos**, seleccione grupo de recursos de Hola que se utiliza con su cuenta de integración.</span><span class="sxs-lookup"><span data-stu-id="56546-128">Under **Resource group**, select hello resource group that you use with your integration account.</span></span>
   3. <span data-ttu-id="56546-129">En **Tipo de recurso**, seleccione **Cuentas de integración**.</span><span class="sxs-lookup"><span data-stu-id="56546-129">Under **Resource type**, select **Integration accounts**.</span></span> 
   4. <span data-ttu-id="56546-130">En **Resource**, seleccione la cuenta de integración.</span><span class="sxs-lookup"><span data-stu-id="56546-130">Under **Resource**, select your integration account.</span></span> 
   5. <span data-ttu-id="56546-131">Elija **Activar diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="56546-131">Choose **Turn on diagnostics**.</span></span>

   ![Configuración de diagnósticos para la cuenta de integración](media/logic-apps-monitor-b2b-message/turn-on-diagnostics-integration-account.png)

3. <span data-ttu-id="56546-133">En **Configuración de diagnóstico**, **Estado**, elija **Activado**.</span><span class="sxs-lookup"><span data-stu-id="56546-133">Under **Diagnostics settings**, and then **Status**, choose **On**.</span></span>

   ![Activación de Diagnósticos de Azure](media/logic-apps-monitor-b2b-message/turn-on-diagnostics-integration-account-2.png)

4. <span data-ttu-id="56546-135">Ahora seleccione toouse de área de trabajo y los datos OMS de hello para el registro como se muestra:</span><span class="sxs-lookup"><span data-stu-id="56546-135">Now select hello OMS workspace and data toouse for logging as shown:</span></span>

   1. <span data-ttu-id="56546-136">Seleccione **enviar tooLog análisis**.</span><span class="sxs-lookup"><span data-stu-id="56546-136">Select **Send tooLog Analytics**.</span></span> 
   2. <span data-ttu-id="56546-137">En **Log Analytics**, elija **Configurar**.</span><span class="sxs-lookup"><span data-stu-id="56546-137">Under **Log Analytics**, choose **Configure**.</span></span> 
   3. <span data-ttu-id="56546-138">En **áreas de trabajo de OMS**, seleccione toouse de área de trabajo OMS de hello para el registro.</span><span class="sxs-lookup"><span data-stu-id="56546-138">Under **OMS Workspaces**, select hello OMS workspace toouse for logging.</span></span>
   4. <span data-ttu-id="56546-139">En **registro**, seleccione hello **IntegrationAccountTrackingEvents** categoría.</span><span class="sxs-lookup"><span data-stu-id="56546-139">Under **Log**, select hello **IntegrationAccountTrackingEvents** category.</span></span>
   5. <span data-ttu-id="56546-140">Elija **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="56546-140">Choose **Save**.</span></span>

   ![Configurar el análisis de registros para poder enviar registros de tooa de datos de diagnóstico](media/logic-apps-monitor-b2b-message/send-diagnostics-data-log-analytics-workspace.png)

5. <span data-ttu-id="56546-142">Ahora [configure el seguimiento de los mensajes B2B en OMS](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span><span class="sxs-lookup"><span data-stu-id="56546-142">Now [set up tracking for your B2B messages in OMS](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span></span>

<a name="azure-monitor-service"></a>

### <a name="turn-on-diagnostics-logging-through-azure-monitor"></a><span data-ttu-id="56546-143">Activación del registro de diagnóstico mediante Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="56546-143">Turn on diagnostics logging through Azure Monitor</span></span>

1. <span data-ttu-id="56546-144">Hola [portal de Azure](https://portal.azure.com), en Hola menú principal de Azure, elija **Monitor**, **registros de diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="56546-144">In hello [Azure portal](https://portal.azure.com), on hello main Azure menu, choose **Monitor**, **Diagnostics logs**.</span></span> <span data-ttu-id="56546-145">Luego, seleccione la cuenta de integración como se muestra aquí:</span><span class="sxs-lookup"><span data-stu-id="56546-145">Then select your integration account as shown here:</span></span>

   ![Elija "Supervisar", "Registros de diagnóstico", seleccione la cuenta de integración.](media/logic-apps-monitor-b2b-message/monitor-service-diagnostics-logs.png)

2. <span data-ttu-id="56546-147">Después de seleccionar su cuenta de integración, Hola después de los valores se selecciona automáticamente.</span><span class="sxs-lookup"><span data-stu-id="56546-147">After you select your integration account, hello following values are automatically selected.</span></span> <span data-ttu-id="56546-148">Si los valores son correctos, elija **Activar diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="56546-148">If these values are correct, choose **Turn on diagnostics**.</span></span> <span data-ttu-id="56546-149">También puede seleccionar valores de hello que desee:</span><span class="sxs-lookup"><span data-stu-id="56546-149">Otherwise, select hello values that you want:</span></span>

   1. <span data-ttu-id="56546-150">En **suscripción**, seleccione Hola suscripción de Azure que se utiliza con su cuenta de integración.</span><span class="sxs-lookup"><span data-stu-id="56546-150">Under **Subscription**, select hello Azure subscription that you use with your integration account.</span></span>
   2. <span data-ttu-id="56546-151">En **grupo de recursos**, seleccione grupo de recursos de Hola que se utiliza con su cuenta de integración.</span><span class="sxs-lookup"><span data-stu-id="56546-151">Under **Resource group**, select hello resource group that you use with your integration account.</span></span>
   3. <span data-ttu-id="56546-152">En **Tipo de recurso**, seleccione **Cuentas de integración**.</span><span class="sxs-lookup"><span data-stu-id="56546-152">Under **Resource type**, select **Integration accounts**.</span></span>
   4. <span data-ttu-id="56546-153">En **Resource**, seleccione la cuenta de integración.</span><span class="sxs-lookup"><span data-stu-id="56546-153">Under **Resource**, select your integration account.</span></span>
   5. <span data-ttu-id="56546-154">Elija **Activar diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="56546-154">Choose **Turn on diagnostics**.</span></span>

   ![Configuración de diagnósticos para la cuenta de integración](media/logic-apps-monitor-b2b-message/turn-on-diagnostics-integration-account.png)

3. <span data-ttu-id="56546-156">En **Configuración de diagnóstico**, elija **Activado**.</span><span class="sxs-lookup"><span data-stu-id="56546-156">Under **Diagnostics settings**, choose **On**.</span></span>

   ![Activación de Diagnósticos de Azure](media/logic-apps-monitor-b2b-message/turn-on-diagnostics-integration-account-2.png)

4. <span data-ttu-id="56546-158">Ahora seleccione categoría de evento y el área de trabajo OMS de hello para el registro como se muestra:</span><span class="sxs-lookup"><span data-stu-id="56546-158">Now select hello OMS workspace and event category for logging as shown:</span></span>

   1. <span data-ttu-id="56546-159">Seleccione **enviar tooLog análisis**.</span><span class="sxs-lookup"><span data-stu-id="56546-159">Select **Send tooLog Analytics**.</span></span> 
   2. <span data-ttu-id="56546-160">En **Log Analytics**, elija **Configurar**.</span><span class="sxs-lookup"><span data-stu-id="56546-160">Under **Log Analytics**, choose **Configure**.</span></span> 
   3. <span data-ttu-id="56546-161">En **áreas de trabajo de OMS**, seleccione toouse de área de trabajo OMS de hello para el registro.</span><span class="sxs-lookup"><span data-stu-id="56546-161">Under **OMS Workspaces**, select hello OMS workspace toouse for logging.</span></span>
   4. <span data-ttu-id="56546-162">En **registro**, seleccione hello **IntegrationAccountTrackingEvents** categoría.</span><span class="sxs-lookup"><span data-stu-id="56546-162">Under **Log**, select hello **IntegrationAccountTrackingEvents** category.</span></span>
   5. <span data-ttu-id="56546-163">Cuando termine, seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="56546-163">When you're done, choose **Save**.</span></span>

   ![Configurar el análisis de registros para poder enviar registros de tooa de datos de diagnóstico](media/logic-apps-monitor-b2b-message/send-diagnostics-data-log-analytics-workspace.png)

5. <span data-ttu-id="56546-165">Ahora [configure el seguimiento de los mensajes B2B en OMS](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span><span class="sxs-lookup"><span data-stu-id="56546-165">Now [set up tracking for your B2B messages in OMS](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span></span>

## <a name="extend-how-and-where-you-use-diagnostic-data-with-other-services"></a><span data-ttu-id="56546-166">Extensión de cómo y dónde usa los datos de diagnóstico con otros servicios</span><span class="sxs-lookup"><span data-stu-id="56546-166">Extend how and where you use diagnostic data with other services</span></span>

<span data-ttu-id="56546-167">Además de con Azure Log Analytics, puede usar los datos de diagnóstico de la aplicación lógica con otros servicios de Azure, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="56546-167">Along with Azure Log Analytics, you can extend how you use your logic app's diagnostic data with other Azure services, for example:</span></span> 

* [<span data-ttu-id="56546-168">Archivar registros de Diagnósticos de Azure en Azure Storage</span><span class="sxs-lookup"><span data-stu-id="56546-168">Archive Azure Diagnostics Logs in Azure Storage</span></span>](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md)
* [<span data-ttu-id="56546-169">Transmitir tooAzure centros de eventos de los registros de diagnóstico de Azure</span><span class="sxs-lookup"><span data-stu-id="56546-169">Stream Azure Diagnostics Logs tooAzure Event Hubs</span></span>](../monitoring-and-diagnostics/monitoring-stream-diagnostic-logs-to-event-hubs.md) 

<span data-ttu-id="56546-170">Luego puede obtener supervisión en tiempo real mediante la telemetría y los análisis de otros servicios, como [Azure Stream Analytics](../stream-analytics/stream-analytics-introduction.md) y [Power BI](../log-analytics/log-analytics-powerbi.md).</span><span class="sxs-lookup"><span data-stu-id="56546-170">You can then get real-time monitoring by using telemetry and analytics from other services, like [Azure Stream Analytics](../stream-analytics/stream-analytics-introduction.md) and [Power BI](../log-analytics/log-analytics-powerbi.md).</span></span> <span data-ttu-id="56546-171">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="56546-171">For example:</span></span>

* [<span data-ttu-id="56546-172">Datos de la secuencia de los centros de eventos tooStream análisis</span><span class="sxs-lookup"><span data-stu-id="56546-172">Stream data from Event Hubs tooStream Analytics</span></span>](../stream-analytics/stream-analytics-define-inputs.md)
* [<span data-ttu-id="56546-173">Analizar datos que se están transmitiendo con Stream Analytics y crear un panel de análisis en tiempo real en Power BI</span><span class="sxs-lookup"><span data-stu-id="56546-173">Analyze streaming data with Stream Analytics and create a real-time analytics dashboard in Power BI</span></span>](../stream-analytics/stream-analytics-power-bi-dashboard.md)

<span data-ttu-id="56546-174">En función de las opciones de Hola que desee configurar, asegúrese de que se primera [crear una cuenta de almacenamiento de Azure](../storage/common/storage-create-storage-account.md) o [crear un concentrador de eventos Azure](../event-hubs/event-hubs-create.md).</span><span class="sxs-lookup"><span data-stu-id="56546-174">Based on hello options that you want set up, make sure that you first [create an Azure storage account](../storage/common/storage-create-storage-account.md) or [create an Azure event hub](../event-hubs/event-hubs-create.md).</span></span> <span data-ttu-id="56546-175">A continuación, seleccione opciones de Hola para donde desea que los datos de diagnóstico de toosend:</span><span class="sxs-lookup"><span data-stu-id="56546-175">Then select hello options for where you want toosend diagnostic data:</span></span>

![Enviar datos tooAzure almacenamiento cuenta o evento de un centro](./media/logic-apps-monitor-b2b-message/storage-account-event-hubs.png)

> [!NOTE]
> <span data-ttu-id="56546-177">Períodos de retención se aplican únicamente cuando elija toouse una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="56546-177">Retention periods apply only when you choose toouse a storage account.</span></span>

## <a name="supported-tracking-schemas"></a><span data-ttu-id="56546-178">Esquemas de seguimiento compatibles</span><span class="sxs-lookup"><span data-stu-id="56546-178">Supported tracking schemas</span></span>

<span data-ttu-id="56546-179">Azure admite estos tipos de esquema, que se corrigieron esquemas excepto Hola tipo personalizado de seguimiento.</span><span class="sxs-lookup"><span data-stu-id="56546-179">Azure supports these tracking schema types, which all have fixed schemas except hello Custom type.</span></span>

* [<span data-ttu-id="56546-180">Esquema de seguimiento de AS2</span><span class="sxs-lookup"><span data-stu-id="56546-180">AS2 tracking schema</span></span>](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md)
* [<span data-ttu-id="56546-181">Esquemas de seguimiento de X12</span><span class="sxs-lookup"><span data-stu-id="56546-181">X12 tracking schema</span></span>](../logic-apps/logic-apps-track-integration-account-x12-tracking-schema.md)
* [<span data-ttu-id="56546-182">Esquema de seguimiento personalizado</span><span class="sxs-lookup"><span data-stu-id="56546-182">Custom tracking schema</span></span>](../logic-apps/logic-apps-track-integration-account-custom-tracking-schema.md)

## <a name="next-steps"></a><span data-ttu-id="56546-183">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="56546-183">Next steps</span></span>

* [<span data-ttu-id="56546-184">Seguimiento de mensajes B2B en OMS</span><span class="sxs-lookup"><span data-stu-id="56546-184">Track B2B messages in OMS</span></span>](../logic-apps/logic-apps-track-b2b-messages-omsportal.md "Seguimiento de mensajes B2B en OMS")
* [<span data-ttu-id="56546-185">Obtener más información sobre Hola paquete de integración empresarial</span><span class="sxs-lookup"><span data-stu-id="56546-185">Learn more about hello Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md "Obtenga más información sobre el paquete de integración empresarial")

