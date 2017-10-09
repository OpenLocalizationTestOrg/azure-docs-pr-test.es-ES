---
title: aaaMonitor operaciones, eventos y contadores de equilibrador de carga | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooenable eventos de alerta y sondeo de registro de estado de mantenimiento para el equilibrador de carga de Azure"
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
ms.openlocfilehash: ac53c2254e06cad780ad6144c5c30f0085d12576
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-for-azure-load-balancer"></a><span data-ttu-id="ad441-103">Análisis del registros para el Equilibrador de carga de Azure</span><span class="sxs-lookup"><span data-stu-id="ad441-103">Log analytics for Azure Load Balancer</span></span>

<span data-ttu-id="ad441-104">Puede usar diferentes tipos de registros en Azure toomanage y solucionar problemas de equilibradores de carga.</span><span class="sxs-lookup"><span data-stu-id="ad441-104">You can use different types of logs in Azure toomanage and troubleshoot load balancers.</span></span> <span data-ttu-id="ad441-105">Algunos de estos registros pueden tener acceso a través del portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="ad441-105">Some of these logs can be accessed through hello portal.</span></span> <span data-ttu-id="ad441-106">Se pueden extraer todos los registros desde Azure Blob Storage y visualizarse en distintas herramientas, como Excel y PowerBI.</span><span class="sxs-lookup"><span data-stu-id="ad441-106">All logs can be extracted from Azure blob storage, and viewed in different tools, such as Excel and PowerBI.</span></span> <span data-ttu-id="ad441-107">Se puede obtener más información sobre Hola diferentes tipos de registros de lista de hello siguiente.</span><span class="sxs-lookup"><span data-stu-id="ad441-107">You can learn more about hello different types of logs from hello list below.</span></span>

* <span data-ttu-id="ad441-108">**Registros de auditoría:** puede usar [los registros de auditoría de Azure](../monitoring-and-diagnostics/insights-debugging-with-events.md) (anteriormente conocido como registros operativos) tooview todas las operaciones que se va a tooyour enviado suscripciones de Azure y su estado.</span><span class="sxs-lookup"><span data-stu-id="ad441-108">**Audit logs:** You can use [Azure Audit Logs](../monitoring-and-diagnostics/insights-debugging-with-events.md) (formerly known as Operational Logs) tooview all operations being submitted tooyour Azure subscription(s), and their status.</span></span> <span data-ttu-id="ad441-109">Los registros de auditoría están habilitados de forma predeterminada y pueden verse en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="ad441-109">Audit logs are enabled by default, and can be viewed in hello Azure portal.</span></span>
* <span data-ttu-id="ad441-110">**Registros de eventos de alertas:** puede utilizar esta rasied de alertas de registro tooview equilibrador de carga de Hola.</span><span class="sxs-lookup"><span data-stu-id="ad441-110">**Alert event logs:** You can use this log tooview alerts rasied by hello load balancer.</span></span> <span data-ttu-id="ad441-111">estado de Hola Hola equilibrador de carga se recopila cada cinco minutos.</span><span class="sxs-lookup"><span data-stu-id="ad441-111">hello status for hello load balancer is collected every five minutes.</span></span> <span data-ttu-id="ad441-112">Este registro se escribe solo si se produce un evento de alerta del equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="ad441-112">This log is only written if a load balancer alert event is raised.</span></span>
* <span data-ttu-id="ad441-113">**Registros de sondeo de estado:** puede utilizar esta tooview los registros de problemas detectados por el sondeo de estado, como el número de Hola de instancias en el grupo back-end que no reciben las solicitudes del equilibrador de carga de hello debido a errores de sondeo de estado.</span><span class="sxs-lookup"><span data-stu-id="ad441-113">**Health probe logs:** You can use this log tooview problems detected by your health probe, such as hello number of instances in your backend-pool that are not receiving requests from hello load balancer because of health probe failures.</span></span> <span data-ttu-id="ad441-114">Este registro se escribe toowhen hay un cambio en el estado de sondeo de estado de Hola.</span><span class="sxs-lookup"><span data-stu-id="ad441-114">This log is written toowhen there is a change in hello health probe status.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ad441-115">El análisis de registros actualmente solo funciona para los equilibradores de carga orientados hacia Internet.</span><span class="sxs-lookup"><span data-stu-id="ad441-115">Log analytics currently works only for Internet facing load balancers.</span></span> <span data-ttu-id="ad441-116">Registros solo están disponibles para los recursos implementados en el modelo de implementación del Administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="ad441-116">Logs are only available for resources deployed in hello Resource Manager deployment model.</span></span> <span data-ttu-id="ad441-117">No puede usar registros de recursos en el modelo de implementación clásica de Hola.</span><span class="sxs-lookup"><span data-stu-id="ad441-117">You cannot use logs for resources in hello classic deployment model.</span></span> <span data-ttu-id="ad441-118">Para obtener más información acerca de los modelos de implementación de hello, consulte [Administrador de recursos de la descripción y la implementación clásica](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="ad441-118">For more information about hello deployment models, see [Understanding Resource Manager deployment and classic deployment](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>

## <a name="enable-logging"></a><span data-ttu-id="ad441-119">Habilitación del registro</span><span class="sxs-lookup"><span data-stu-id="ad441-119">Enable logging</span></span>

<span data-ttu-id="ad441-120">El registro de auditoría se habilita automáticamente para todos los recursos de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ad441-120">Audit logging is automatically enabled for every Resource Manager resource.</span></span> <span data-ttu-id="ad441-121">Necesita eventos tooenable y toostart de registro de mantenimiento sondeo recopilar datos de hello disponibles a través de esos registros.</span><span class="sxs-lookup"><span data-stu-id="ad441-121">You need tooenable event and health probe logging toostart collecting hello data available through those logs.</span></span> <span data-ttu-id="ad441-122">Usar hello siguiendo el registro de pasos tooenable.</span><span class="sxs-lookup"><span data-stu-id="ad441-122">Use hello following steps tooenable logging.</span></span>

<span data-ttu-id="ad441-123">Inicio de sesión toohello [portal de Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ad441-123">Sign-in toohello [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="ad441-124">Si aún no tiene un equilibrador de carga, [cree uno](load-balancer-get-started-internet-arm-ps.md) antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="ad441-124">If you don't already have a load balancer, [create a load balancer](load-balancer-get-started-internet-arm-ps.md) before you continue.</span></span>

1. <span data-ttu-id="ad441-125">En el portal de hello, haga clic en **examinar**.</span><span class="sxs-lookup"><span data-stu-id="ad441-125">In hello portal, click **Browse**.</span></span>
2. <span data-ttu-id="ad441-126">Seleccione **Equilibradores de carga**.</span><span class="sxs-lookup"><span data-stu-id="ad441-126">Select **Load Balancers**.</span></span>

    ![portal - load-balancer](./media/load-balancer-monitor-log/load-balancer-browse.png)

3. <span data-ttu-id="ad441-128">Seleccione un equilibrador de carga existente >> **Toda la configuración**.</span><span class="sxs-lookup"><span data-stu-id="ad441-128">Select an existing load balancer >> **All Settings**.</span></span>
4. <span data-ttu-id="ad441-129">En hello derecha del cuadro de diálogo Hola nombre Hola Hola de equilibrador de carga, desplácese demasiado**supervisión**, haga clic en **diagnósticos**.</span><span class="sxs-lookup"><span data-stu-id="ad441-129">On hello right side of hello dialog under hello name of hello load balancer, scroll too**Monitoring**, click **Diagnostics**.</span></span>

    ![portal - load-balancer-settings](./media/load-balancer-monitor-log/load-balancer-settings.png)

5. <span data-ttu-id="ad441-131">Hola **diagnósticos** panel, en **estado**, seleccione **en**.</span><span class="sxs-lookup"><span data-stu-id="ad441-131">In hello **Diagnostics** pane, under **Status**, select **On**.</span></span>
6. <span data-ttu-id="ad441-132">Haga clic en **Cuenta de almacenamiento**.</span><span class="sxs-lookup"><span data-stu-id="ad441-132">Click **Storage Account**.</span></span>
7. <span data-ttu-id="ad441-133">En **Registros**, seleccione una cuenta de almacenamiento existente o cree una nueva.</span><span class="sxs-lookup"><span data-stu-id="ad441-133">Under **LOGS**, select an existing storage account, or create a new one.</span></span> <span data-ttu-id="ad441-134">Utilice toodetermine de control deslizante de Hola durante cuántos días correspondientes a los datos de eventos se almacenarán en los registros de eventos de Hola.</span><span class="sxs-lookup"><span data-stu-id="ad441-134">Use hello slider toodetermine how many days worth of event data will be stored in hello event logs.</span></span> 
8. <span data-ttu-id="ad441-135">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="ad441-135">Click **Save**.</span></span>

    ![Portal - Registros de diagnósticos](./media/load-balancer-monitor-log/load-balancer-diagnostics.png)

> [!NOTE]
> <span data-ttu-id="ad441-137">Los registros de auditoría no requieren una cuenta de almacenamiento separada.</span><span class="sxs-lookup"><span data-stu-id="ad441-137">Audit logs do not require a separate storage account.</span></span> <span data-ttu-id="ad441-138">Hola uso de almacenamiento para el evento y el estado de registro de sondeo supondrán un coste adicional de servicio.</span><span class="sxs-lookup"><span data-stu-id="ad441-138">hello use of storage for event and health probe logging will incur service charges.</span></span>

## <a name="audit-log"></a><span data-ttu-id="ad441-139">Registro de auditoría</span><span class="sxs-lookup"><span data-stu-id="ad441-139">Audit log</span></span>

<span data-ttu-id="ad441-140">registro de auditoría de Hola se genera de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="ad441-140">hello audit log is generated by default.</span></span> <span data-ttu-id="ad441-141">Hola registros se conservan durante 90 días en el almacén de registros de eventos de Azure.</span><span class="sxs-lookup"><span data-stu-id="ad441-141">hello logs are preserved for 90 days in Azure's Event Logs store.</span></span> <span data-ttu-id="ad441-142">Obtener más información sobre estos registros leyendo hello [ver eventos y registros de auditoría](../monitoring-and-diagnostics/insights-debugging-with-events.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="ad441-142">Learn more about these logs by reading hello [View events and audit logs](../monitoring-and-diagnostics/insights-debugging-with-events.md) article.</span></span>

## <a name="alert-event-log"></a><span data-ttu-id="ad441-143">Registro de eventos de alerta</span><span class="sxs-lookup"><span data-stu-id="ad441-143">Alert event log</span></span>

<span data-ttu-id="ad441-144">Este registro solo se genera si lo habilitó para cada uno de los equilibradores de carga.</span><span class="sxs-lookup"><span data-stu-id="ad441-144">This log is only generated if you've enabled it on a per load balancer basis.</span></span> <span data-ttu-id="ad441-145">eventos de Hola se registran en formato JSON y se almacena en la cuenta de almacenamiento de hello especificada cuando se habilitó el registro de hello.</span><span class="sxs-lookup"><span data-stu-id="ad441-145">hello events are logged in JSON format and stored in hello storage account you specified when you enabled hello logging.</span></span> <span data-ttu-id="ad441-146">Hola aquí te mostramos un ejemplo de un evento.</span><span class="sxs-lookup"><span data-stu-id="ad441-146">hello following is an example of an event.</span></span>

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

<span data-ttu-id="ad441-147">Hola JSON de salida muestra hello *eventname* propiedad que se describirá el motivo de Hola Hola equilibrador de carga crea una alerta.</span><span class="sxs-lookup"><span data-stu-id="ad441-147">hello JSON output shows hello *eventname* property which will describe hello reason for hello load balancer created an alert.</span></span> <span data-ttu-id="ad441-148">En este caso, alerta de hello generada venció el agotamiento de puertos de tooTCP causado por origen que IP NAT limita (SNAT).</span><span class="sxs-lookup"><span data-stu-id="ad441-148">In this case, hello alert generated was due tooTCP port exhaustion caused by source IP NAT limits (SNAT).</span></span>

## <a name="health-probe-log"></a><span data-ttu-id="ad441-149">Registro de sondeo de estado</span><span class="sxs-lookup"><span data-stu-id="ad441-149">Health probe log</span></span>

<span data-ttu-id="ad441-150">Este registro solo se genera si lo habilitó para cada uno de los equilibradores de carga, tal como se indicó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="ad441-150">This log is only generated if you've enabled it on a per load balancer basis as detailed above.</span></span> <span data-ttu-id="ad441-151">Hola datos se almacenan en la cuenta de almacenamiento de hello especificada cuando se habilitó el registro de hello.</span><span class="sxs-lookup"><span data-stu-id="ad441-151">hello data is stored in hello storage account you specified when you enabled hello logging.</span></span> <span data-ttu-id="ad441-152">Se crea un contenedor denominado 'loadbalancerprobehealthstatus de registros de visión' y se registra Hola datos siguientes:</span><span class="sxs-lookup"><span data-stu-id="ad441-152">A container named 'insights-logs-loadbalancerprobehealthstatus' is created and hello following data is logged:</span></span>

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

<span data-ttu-id="ad441-153">salida JSON de Hello muestra de Hola propiedades campo Hola información básica de estado de mantenimiento de sondeo de Hola.</span><span class="sxs-lookup"><span data-stu-id="ad441-153">hello JSON output shows in hello properties field hello basic information for hello probe health status.</span></span> <span data-ttu-id="ad441-154">Hola *dipDownCount* propiedad muestra el número total de Hola de instancias en hello back-end, que no están recibiendo tráfico de red debido a las respuestas del sondeo de toofailed.</span><span class="sxs-lookup"><span data-stu-id="ad441-154">hello *dipDownCount* property shows hello total number of instances on hello back-end which are not receiving network traffic due toofailed probe responses.</span></span>

## <a name="view-and-analyze-hello-audit-log"></a><span data-ttu-id="ad441-155">Ver y analizar el registro de auditoría de Hola</span><span class="sxs-lookup"><span data-stu-id="ad441-155">View and analyze hello audit log</span></span>

<span data-ttu-id="ad441-156">Puede ver y analizar datos de registro de auditoría mediante cualquiera de los siguientes métodos de hello:</span><span class="sxs-lookup"><span data-stu-id="ad441-156">You can view and analyze audit log data using any of hello following methods:</span></span>

* <span data-ttu-id="ad441-157">**Herramientas de Azure:** recuperar información de los registros de auditoría de Hola a través de PowerShell de Azure, hello Azure interfaz de línea de comandos (CLI), Hola API de REST de Azure, u Hola portal de vista previa.</span><span class="sxs-lookup"><span data-stu-id="ad441-157">**Azure tools:** Retrieve information from hello audit logs through Azure PowerShell, hello Azure Command Line Interface (CLI), hello Azure REST API, or hello Azure preview portal.</span></span> <span data-ttu-id="ad441-158">Instrucciones paso a paso para cada método se detallan en hello [auditoría de las operaciones con el Administrador de recursos](../azure-resource-manager/resource-group-audit.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="ad441-158">Step-by-step instructions for each method are detailed in hello [Audit operations with Resource Manager](../azure-resource-manager/resource-group-audit.md) article.</span></span>
* <span data-ttu-id="ad441-159">**Power BI:** si todavía no tiene una cuenta de [Power BI](https://powerbi.microsoft.com/pricing), puede probarlo gratis.</span><span class="sxs-lookup"><span data-stu-id="ad441-159">**Power BI:** If you do not already have a [Power BI](https://powerbi.microsoft.com/pricing) account, you can try it for free.</span></span> <span data-ttu-id="ad441-160">Con hello [contenido de los registros de auditoría de Azure para Power BI](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-audit-logs), puede analizar los datos con paneles configurados previamente o puede personalizar vistas toosuit sus requisitos.</span><span class="sxs-lookup"><span data-stu-id="ad441-160">Using hello [Azure Audit Logs content pack for Power BI](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-audit-logs), you can analyze your data with pre-configured dashboards, or you can customize views toosuit your requirements.</span></span>

## <a name="view-and-analyze-hello-health-probe-and-event-log"></a><span data-ttu-id="ad441-161">Ver y analizar el sondeo de estado de Hola y de registro de eventos</span><span class="sxs-lookup"><span data-stu-id="ad441-161">View and analyze hello health probe and event log</span></span>

<span data-ttu-id="ad441-162">Necesita tooconnect tooyour almacenamiento de la cuenta y recuperar entradas de registro de hello JSON para registros de sondeo de estado y eventos.</span><span class="sxs-lookup"><span data-stu-id="ad441-162">You need tooconnect tooyour storage account and retrieve hello JSON log entries for event and health probe logs.</span></span> <span data-ttu-id="ad441-163">Una vez descargados los archivos de hello JSON, puede convertir tooCSV y view en Excel, Power BI o cualquier otra herramienta de visualización de datos.</span><span class="sxs-lookup"><span data-stu-id="ad441-163">Once you download hello JSON files, you can convert them tooCSV and view in Excel, PowerBI, or any other data visualization tool.</span></span>

> [!TIP]
> <span data-ttu-id="ad441-164">Si está familiarizado con los conceptos básicos del cambio de valores de constantes y variables de C# y Visual Studio, puede usar hello [iniciar herramientas de convertidor](https://github.com/Azure-Samples/networking-dotnet-log-converter) disponible en GitHub.</span><span class="sxs-lookup"><span data-stu-id="ad441-164">If you are familiar with Visual Studio and basic concepts of changing values for constants and variables in C#, you can use hello [log converter tools](https://github.com/Azure-Samples/networking-dotnet-log-converter) available from GitHub.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ad441-165">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="ad441-165">Additional resources</span></span>

* <span data-ttu-id="ad441-166">[Visualize your Azure Audit Logs with Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx) (Visualizar los registros de auditoría de Azure con Power BI).</span><span class="sxs-lookup"><span data-stu-id="ad441-166">[Visualize your Azure Audit Logs with Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx) blog post.</span></span>
* <span data-ttu-id="ad441-167">[View and analyze Azure Audit Logs in Power BI and more](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) (Visualizar los registros de auditoría de Azure con Power BI).</span><span class="sxs-lookup"><span data-stu-id="ad441-167">[View and analyze Azure Audit Logs in Power BI and more](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) blog post.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ad441-168">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ad441-168">Next steps</span></span>

[<span data-ttu-id="ad441-169">Descripción de los sondeos del equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="ad441-169">Understand load balancer probes</span></span>](load-balancer-custom-probe-overview.md)
