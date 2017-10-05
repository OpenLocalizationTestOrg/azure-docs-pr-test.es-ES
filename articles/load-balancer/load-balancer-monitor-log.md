---
title: "Supervisión de operaciones, eventos y contadores de Load Balancer | Microsoft Docs"
description: Aprenda a habilitar eventos de alerta y el registro del estado de mantenimiento del sondeo para el Equilibrador de carga de Azure
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: 56656d74-0241-4096-88c8-aa88515d676d
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: 638ecd5e02889bd8cb6e7429dfcec335feaac4a3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="log-analytics-for-azure-load-balancer"></a><span data-ttu-id="37c7b-103">Análisis del registros para el Equilibrador de carga de Azure</span><span class="sxs-lookup"><span data-stu-id="37c7b-103">Log analytics for Azure Load Balancer</span></span>

<span data-ttu-id="37c7b-104">Puede usar diferentes tipos de registros en Azure para administrar y solucionar problemas de equilibradores de carga.</span><span class="sxs-lookup"><span data-stu-id="37c7b-104">You can use different types of logs in Azure to manage and troubleshoot load balancers.</span></span> <span data-ttu-id="37c7b-105">Se puede acceder a algunos de estos registros a través del portal.</span><span class="sxs-lookup"><span data-stu-id="37c7b-105">Some of these logs can be accessed through the portal.</span></span> <span data-ttu-id="37c7b-106">Se pueden extraer todos los registros desde Azure Blob Storage y visualizarse en distintas herramientas, como Excel y PowerBI.</span><span class="sxs-lookup"><span data-stu-id="37c7b-106">All logs can be extracted from Azure blob storage, and viewed in different tools, such as Excel and PowerBI.</span></span> <span data-ttu-id="37c7b-107">Puede obtener más información acerca de los diferentes tipos de registros en la lista siguiente.</span><span class="sxs-lookup"><span data-stu-id="37c7b-107">You can learn more about the different types of logs from the list below.</span></span>

* <span data-ttu-id="37c7b-108">**Registros de auditoría:** puede usar los [registros de auditoría de Azure](../monitoring-and-diagnostics/insights-debugging-with-events.md) (anteriormente conocido como registros operativos) para ver todas las operaciones enviadas a sus suscripciones de Azure, así como su estado.</span><span class="sxs-lookup"><span data-stu-id="37c7b-108">**Audit logs:** You can use [Azure Audit Logs](../monitoring-and-diagnostics/insights-debugging-with-events.md) (formerly known as Operational Logs) to view all operations being submitted to your Azure subscription(s), and their status.</span></span> <span data-ttu-id="37c7b-109">Los registros de auditoría están habilitados de forma predeterminada y se pueden ver en el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="37c7b-109">Audit logs are enabled by default, and can be viewed in the Azure portal.</span></span>
* <span data-ttu-id="37c7b-110">**Registros de eventos de alerta:** puede utilizar este registro para las alertas generadas por el equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="37c7b-110">**Alert event logs:** You can use this log to view alerts rasied by the load balancer.</span></span> <span data-ttu-id="37c7b-111">El estado del equilibrador de carga se recopila cada cinco minutos.</span><span class="sxs-lookup"><span data-stu-id="37c7b-111">The status for the load balancer is collected every five minutes.</span></span> <span data-ttu-id="37c7b-112">Este registro se escribe solo si se produce un evento de alerta del equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="37c7b-112">This log is only written if a load balancer alert event is raised.</span></span>
* <span data-ttu-id="37c7b-113">**Registros de sondeo de estado:** puede utilizar este registro para ver los problemas detectados por el sondeo de estado, como el número de instancias en el grupo back-end que no reciben las solicitudes del equilibrador de carga debido a errores de sondeo de estado.</span><span class="sxs-lookup"><span data-stu-id="37c7b-113">**Health probe logs:** You can use this log to view problems detected by your health probe, such as the number of instances in your backend-pool that are not receiving requests from the load balancer because of health probe failures.</span></span> <span data-ttu-id="37c7b-114">Este registro se escribe cuando se produce un cambio en el estatus del sondeo de estado.</span><span class="sxs-lookup"><span data-stu-id="37c7b-114">This log is written to when there is a change in the health probe status.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="37c7b-115">El análisis de registros actualmente solo funciona para los equilibradores de carga orientados hacia Internet.</span><span class="sxs-lookup"><span data-stu-id="37c7b-115">Log analytics currently works only for Internet facing load balancers.</span></span> <span data-ttu-id="37c7b-116">Los registros solo están disponibles para los recursos implementados en el modelo de implementación del Administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="37c7b-116">Logs are only available for resources deployed in the Resource Manager deployment model.</span></span> <span data-ttu-id="37c7b-117">No puede usar los registros de recursos del modelo de implementación clásica.</span><span class="sxs-lookup"><span data-stu-id="37c7b-117">You cannot use logs for resources in the classic deployment model.</span></span> <span data-ttu-id="37c7b-118">Para más información sobre estos modelos de implementación, consulte [Understanding Resource Manager deployment and classic deployment](../azure-resource-manager/resource-manager-deployment-model.md) (Descripción de la implementación de Resource Manager y la implementación clásica).</span><span class="sxs-lookup"><span data-stu-id="37c7b-118">For more information about the deployment models, see [Understanding Resource Manager deployment and classic deployment](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>

## <a name="enable-logging"></a><span data-ttu-id="37c7b-119">Habilitación del registro</span><span class="sxs-lookup"><span data-stu-id="37c7b-119">Enable logging</span></span>

<span data-ttu-id="37c7b-120">El registro de auditoría se habilita automáticamente para todos los recursos de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="37c7b-120">Audit logging is automatically enabled for every Resource Manager resource.</span></span> <span data-ttu-id="37c7b-121">Debe habilitar el registro de eventos y de sondeos de estado para iniciar la recopilación de los datos disponibles a través de esos registros.</span><span class="sxs-lookup"><span data-stu-id="37c7b-121">You need to enable event and health probe logging to start collecting the data available through those logs.</span></span> <span data-ttu-id="37c7b-122">Para habilitar el registro, realice los siguientes pasos.</span><span class="sxs-lookup"><span data-stu-id="37c7b-122">Use the following steps to enable logging.</span></span>

<span data-ttu-id="37c7b-123">Inicie sesión en el [Portal de Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="37c7b-123">Sign-in to the [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="37c7b-124">Si aún no tiene un equilibrador de carga, [cree uno](load-balancer-get-started-internet-arm-ps.md) antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="37c7b-124">If you don't already have a load balancer, [create a load balancer](load-balancer-get-started-internet-arm-ps.md) before you continue.</span></span>

1. <span data-ttu-id="37c7b-125">En el portal, haga clic en **Examinar**.</span><span class="sxs-lookup"><span data-stu-id="37c7b-125">In the portal, click **Browse**.</span></span>
2. <span data-ttu-id="37c7b-126">Seleccione **Equilibradores de carga**.</span><span class="sxs-lookup"><span data-stu-id="37c7b-126">Select **Load Balancers**.</span></span>

    ![portal - load-balancer](./media/load-balancer-monitor-log/load-balancer-browse.png)

3. <span data-ttu-id="37c7b-128">Seleccione un equilibrador de carga existente >> **Toda la configuración**.</span><span class="sxs-lookup"><span data-stu-id="37c7b-128">Select an existing load balancer >> **All Settings**.</span></span>
4. <span data-ttu-id="37c7b-129">En el lado derecho del cuadro de diálogo, bajo el nombre del equilibrador de carga, desplácese a **Supervisión** y haga clic en **Diagnósticos**.</span><span class="sxs-lookup"><span data-stu-id="37c7b-129">On the right side of the dialog under the name of the load balancer, scroll to **Monitoring**, click **Diagnostics**.</span></span>

    ![portal - load-balancer-settings](./media/load-balancer-monitor-log/load-balancer-settings.png)

5. <span data-ttu-id="37c7b-131">En el panel **Diagnósticos**, debajo de **Estado**, seleccione **Activar**.</span><span class="sxs-lookup"><span data-stu-id="37c7b-131">In the **Diagnostics** pane, under **Status**, select **On**.</span></span>
6. <span data-ttu-id="37c7b-132">Haga clic en **Cuenta de almacenamiento**.</span><span class="sxs-lookup"><span data-stu-id="37c7b-132">Click **Storage Account**.</span></span>
7. <span data-ttu-id="37c7b-133">En **Registros**, seleccione una cuenta de almacenamiento existente o cree una nueva.</span><span class="sxs-lookup"><span data-stu-id="37c7b-133">Under **LOGS**, select an existing storage account, or create a new one.</span></span> <span data-ttu-id="37c7b-134">Utilice el control deslizante para determinar cuántos días de datos de eventos se almacenarán en los registros de eventos.</span><span class="sxs-lookup"><span data-stu-id="37c7b-134">Use the slider to determine how many days worth of event data will be stored in the event logs.</span></span> 
8. <span data-ttu-id="37c7b-135">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="37c7b-135">Click **Save**.</span></span>

    ![Portal - Registros de diagnósticos](./media/load-balancer-monitor-log/load-balancer-diagnostics.png)

> [!NOTE]
> <span data-ttu-id="37c7b-137">Los registros de auditoría no requieren una cuenta de almacenamiento separada.</span><span class="sxs-lookup"><span data-stu-id="37c7b-137">Audit logs do not require a separate storage account.</span></span> <span data-ttu-id="37c7b-138">El uso del almacenamiento para el registro de eventos y de sondeo de estado supondrán un costo adicional de servicio.</span><span class="sxs-lookup"><span data-stu-id="37c7b-138">The use of storage for event and health probe logging will incur service charges.</span></span>

## <a name="audit-log"></a><span data-ttu-id="37c7b-139">Registro de auditoría</span><span class="sxs-lookup"><span data-stu-id="37c7b-139">Audit log</span></span>

<span data-ttu-id="37c7b-140">El registro de auditoría se genera de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="37c7b-140">The audit log is generated by default.</span></span> <span data-ttu-id="37c7b-141">Los registros se conservan durante 90 días en el almacén de registros de eventos de Azure.</span><span class="sxs-lookup"><span data-stu-id="37c7b-141">The logs are preserved for 90 days in Azure's Event Logs store.</span></span> <span data-ttu-id="37c7b-142">Para obtener más información sobre estos registros, consulte el artículo [Visualización de eventos y registros de auditoría](../monitoring-and-diagnostics/insights-debugging-with-events.md) .</span><span class="sxs-lookup"><span data-stu-id="37c7b-142">Learn more about these logs by reading the [View events and audit logs](../monitoring-and-diagnostics/insights-debugging-with-events.md) article.</span></span>

## <a name="alert-event-log"></a><span data-ttu-id="37c7b-143">Registro de eventos de alerta</span><span class="sxs-lookup"><span data-stu-id="37c7b-143">Alert event log</span></span>

<span data-ttu-id="37c7b-144">Este registro solo se genera si lo habilitó para cada uno de los equilibradores de carga.</span><span class="sxs-lookup"><span data-stu-id="37c7b-144">This log is only generated if you've enabled it on a per load balancer basis.</span></span> <span data-ttu-id="37c7b-145">Los eventos se registran en formato JSON y se almacenan en la cuenta de almacenamiento que especificó cuando habilitó el registro.</span><span class="sxs-lookup"><span data-stu-id="37c7b-145">The events are logged in JSON format and stored in the storage account you specified when you enabled the logging.</span></span> <span data-ttu-id="37c7b-146">A continuación, se muestra un ejemplo de un evento.</span><span class="sxs-lookup"><span data-stu-id="37c7b-146">The following is an example of an event.</span></span>

```json
{
    "time": "2016-01-26T10:37:46.6024215Z",
    "systemId": "32077926-b9c4-42fb-94c1-762e528b5b27",
    "category": "LoadBalancerAlertEvent",
    "resourceId": "/SUBSCRIPTIONS/XXXXXXXXXXXXXXXXX-XXXX-XXXX-XXXXXXXXX/RESOURCEGROUPS/RG7/PROVIDERS/MICROSOFT.NETWORK/LOADBALANCERS/WWEBLB",
    "operationName": "LoadBalancerProbeHealthStatus",
    "properties": {
        "eventName": "Resource Limits Hit",
        "eventDescription": "Ports exhausted",
        "eventProperties": {
            "public ip address": "40.117.227.32"
        }
    }
}
```

<span data-ttu-id="37c7b-147">El resultado de JSON muestra la propiedad *eventname* que describirá el motivo de creación de una alerta por parte del equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="37c7b-147">The JSON output shows the *eventname* property which will describe the reason for the load balancer created an alert.</span></span> <span data-ttu-id="37c7b-148">En este caso, la alerta generada se debió al agotamiento de puertos TCP causado por los límites de IP NAT de origen (SNAT).</span><span class="sxs-lookup"><span data-stu-id="37c7b-148">In this case, the alert generated was due to TCP port exhaustion caused by source IP NAT limits (SNAT).</span></span>

## <a name="health-probe-log"></a><span data-ttu-id="37c7b-149">Registro de sondeo de estado</span><span class="sxs-lookup"><span data-stu-id="37c7b-149">Health probe log</span></span>

<span data-ttu-id="37c7b-150">Este registro solo se genera si lo habilitó para cada uno de los equilibradores de carga, tal como se indicó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="37c7b-150">This log is only generated if you've enabled it on a per load balancer basis as detailed above.</span></span> <span data-ttu-id="37c7b-151">Los datos se almacenan en la cuenta de almacenamiento que especificó cuando habilitó el registro.</span><span class="sxs-lookup"><span data-stu-id="37c7b-151">The data is stored in the storage account you specified when you enabled the logging.</span></span> <span data-ttu-id="37c7b-152">Se crea un contenedor denominado "insights-logs-loadbalancerprobehealthstatus" y se registran los datos siguientes:</span><span class="sxs-lookup"><span data-stu-id="37c7b-152">A container named 'insights-logs-loadbalancerprobehealthstatus' is created and the following data is logged:</span></span>

```json
{
    "records":[
    {
        "time": "2016-01-26T10:37:46.6024215Z",
        "systemId": "32077926-b9c4-42fb-94c1-762e528b5b27",
        "category": "LoadBalancerProbeHealthStatus",
        "resourceId": "/SUBSCRIPTIONS/XXXXXXXXXXXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXX/RESOURCEGROUPS/RG7/PROVIDERS/MICROSOFT.NETWORK/LOADBALANCERS/WWEBLB",
        "operationName": "LoadBalancerProbeHealthStatus",
        "properties": {
            "publicIpAddress": "40.83.190.158",
            "port": "81",
            "totalDipCount": 2,
            "dipDownCount": 1,
            "healthPercentage": 50.000000
        }
    },
    {
        "time": "2016-01-26T10:37:46.6024215Z",
        "systemId": "32077926-b9c4-42fb-94c1-762e528b5b27",
        "category": "LoadBalancerProbeHealthStatus",
        "resourceId": "/SUBSCRIPTIONS/XXXXXXXXXXXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXX/RESOURCEGROUPS/RG7/PROVIDERS/MICROSOFT.NETWORK/LOADBALANCERS/WWEBLB",
        "operationName": "LoadBalancerProbeHealthStatus",
        "properties": {
            "publicIpAddress": "40.83.190.158",
            "port": "81",
            "totalDipCount": 2,
            "dipDownCount": 0,
            "healthPercentage": 100.000000
        }
    }]
}
```

<span data-ttu-id="37c7b-153">El resultado JSON muestra en el campo de propiedades la información básica del estado de mantenimiento del sondeo.</span><span class="sxs-lookup"><span data-stu-id="37c7b-153">The JSON output shows in the properties field the basic information for the probe health status.</span></span> <span data-ttu-id="37c7b-154">La propiedad *dipDownCount* muestra el número total de instancias en el back-end que no están recibiendo tráfico de red debido a las respuestas de sondeo con error.</span><span class="sxs-lookup"><span data-stu-id="37c7b-154">The *dipDownCount* property shows the total number of instances on the back-end which are not receiving network traffic due to failed probe responses.</span></span>

## <a name="view-and-analyze-the-audit-log"></a><span data-ttu-id="37c7b-155">Visualización y análisis del registro de auditoría</span><span class="sxs-lookup"><span data-stu-id="37c7b-155">View and analyze the audit log</span></span>

<span data-ttu-id="37c7b-156">Puede ver y analizar los datos del registro de auditoría mediante el uso de cualquiera de los métodos siguientes:</span><span class="sxs-lookup"><span data-stu-id="37c7b-156">You can view and analyze audit log data using any of the following methods:</span></span>

* <span data-ttu-id="37c7b-157">**Herramientas de Azure:** puede recuperar información de los registros de auditoría a través de Azure PowerShell, de la interfaz de la línea de comandos (CLI) de Azure, la API de REST de Azure o el Portal de vista previa de Azure.</span><span class="sxs-lookup"><span data-stu-id="37c7b-157">**Azure tools:** Retrieve information from the audit logs through Azure PowerShell, the Azure Command Line Interface (CLI), the Azure REST API, or the Azure preview portal.</span></span> <span data-ttu-id="37c7b-158">En el artículo [Operaciones de auditoría con el Administrador de recursos](../azure-resource-manager/resource-group-audit.md) se detallan instrucciones paso a paso de cada método.</span><span class="sxs-lookup"><span data-stu-id="37c7b-158">Step-by-step instructions for each method are detailed in the [Audit operations with Resource Manager](../azure-resource-manager/resource-group-audit.md) article.</span></span>
* <span data-ttu-id="37c7b-159">**Power BI:** si todavía no tiene una cuenta de [Power BI](https://powerbi.microsoft.com/pricing), puede probarlo gratis.</span><span class="sxs-lookup"><span data-stu-id="37c7b-159">**Power BI:** If you do not already have a [Power BI](https://powerbi.microsoft.com/pricing) account, you can try it for free.</span></span> <span data-ttu-id="37c7b-160">Con el [paquete de contenido de los registros de auditoría de Azure para Power BI](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-audit-logs) puede analizar los datos con los paneles preconfigurados o puede personalizar las vistas para que se adapten a sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="37c7b-160">Using the [Azure Audit Logs content pack for Power BI](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-audit-logs), you can analyze your data with pre-configured dashboards, or you can customize views to suit your requirements.</span></span>

## <a name="view-and-analyze-the-health-probe-and-event-log"></a><span data-ttu-id="37c7b-161">Visualización y análisis del registro de eventos y de sondeos de estado</span><span class="sxs-lookup"><span data-stu-id="37c7b-161">View and analyze the health probe and event log</span></span>

<span data-ttu-id="37c7b-162">Debe conectarse a la cuenta de almacenamiento y recuperar las entradas del registro de JSON para los registros de eventos y de sondeos de estado.</span><span class="sxs-lookup"><span data-stu-id="37c7b-162">You need to connect to your storage account and retrieve the JSON log entries for event and health probe logs.</span></span> <span data-ttu-id="37c7b-163">Cuando descargue los archivos JSON, se pueden convertir a CSV y consultarlos en Excel, PowerBI o cualquier otra herramienta de visualización de datos.</span><span class="sxs-lookup"><span data-stu-id="37c7b-163">Once you download the JSON files, you can convert them to CSV and view in Excel, PowerBI, or any other data visualization tool.</span></span>

> [!TIP]
> <span data-ttu-id="37c7b-164">Si está familiarizado con Visual Studio y con los conceptos básicos de cambio de los valores de constantes y variables de C#, puede usar las [herramientas convertidoras de registros](https://github.com/Azure-Samples/networking-dotnet-log-converter) que encontrará en GitHub.</span><span class="sxs-lookup"><span data-stu-id="37c7b-164">If you are familiar with Visual Studio and basic concepts of changing values for constants and variables in C#, you can use the [log converter tools](https://github.com/Azure-Samples/networking-dotnet-log-converter) available from GitHub.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="37c7b-165">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="37c7b-165">Additional resources</span></span>

* <span data-ttu-id="37c7b-166">[Visualize your Azure Audit Logs with Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx) (Visualizar los registros de auditoría de Azure con Power BI).</span><span class="sxs-lookup"><span data-stu-id="37c7b-166">[Visualize your Azure Audit Logs with Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx) blog post.</span></span>
* <span data-ttu-id="37c7b-167">[View and analyze Azure Audit Logs in Power BI and more](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) (Visualizar los registros de auditoría de Azure con Power BI).</span><span class="sxs-lookup"><span data-stu-id="37c7b-167">[View and analyze Azure Audit Logs in Power BI and more](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) blog post.</span></span>

## <a name="next-steps"></a><span data-ttu-id="37c7b-168">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="37c7b-168">Next steps</span></span>

[<span data-ttu-id="37c7b-169">Descripción de los sondeos del equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="37c7b-169">Understand load balancer probes</span></span>](load-balancer-custom-probe-overview.md)
