---
title: "Transmisión de datos de Diagnósticos de Azure en la ruta de acceso activa mediante Centros de eventos | Microsoft Docs"
description: "Configuración de Diagnósticos de Azure con Event Hubs de un extremo a otro, con instrucciones para escenarios comunes"
services: event-hubs
documentationcenter: na
author: rboucher
manager: carmonm
editor: 
ms.assetid: edeebaac-1c47-4b43-9687-f28e7e1e446a
ms.service: monitoring-and-diagnostics
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/13/2017
ms.author: robb
ms.openlocfilehash: 1c05bd6dc4c4d394aa043b9995de9c184e4f14c6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="streaming-azure-diagnostics-data-in-the-hot-path-by-using-event-hubs"></a><span data-ttu-id="c5d21-103">Transmisión de datos de Diagnósticos de Azure en la ruta de acceso activa mediante Centros de eventos</span><span class="sxs-lookup"><span data-stu-id="c5d21-103">Streaming Azure Diagnostics data in the hot path by using Event Hubs</span></span>
<span data-ttu-id="c5d21-104">Diagnósticos de Azure proporciona maneras flexibles de recopilar métricas y registros de máquinas virtuales de servicios en la nube (VM) y transferir los resultados a Almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="c5d21-104">Azure Diagnostics provides flexible ways to collect metrics and logs from cloud services virtual machines (VMs) and transfer results to Azure Storage.</span></span> <span data-ttu-id="c5d21-105">A partir de marzo de 2016 (SDK 2.9), puede enviar diagnósticos a orígenes de datos personalizados y transferir datos de rutas de acceso activas en cuestión de segundos mediante [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/).</span><span class="sxs-lookup"><span data-stu-id="c5d21-105">Starting in the March 2016 (SDK 2.9) time frame, you can send Diagnostics to custom data sources and transfer hot path data in seconds by using [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/).</span></span>

<span data-ttu-id="c5d21-106">Entre los tipos de datos admitidos se incluyen:</span><span class="sxs-lookup"><span data-stu-id="c5d21-106">Supported data types include:</span></span>

* <span data-ttu-id="c5d21-107">Eventos de Seguimiento de eventos para Windows (ETW)</span><span class="sxs-lookup"><span data-stu-id="c5d21-107">Event Tracing for Windows (ETW) events</span></span>
* <span data-ttu-id="c5d21-108">Contadores de rendimiento</span><span class="sxs-lookup"><span data-stu-id="c5d21-108">Performance counters</span></span>
* <span data-ttu-id="c5d21-109">Registros de eventos de Windows</span><span class="sxs-lookup"><span data-stu-id="c5d21-109">Windows event logs</span></span>
* <span data-ttu-id="c5d21-110">Registros de aplicación</span><span class="sxs-lookup"><span data-stu-id="c5d21-110">Application logs</span></span>
* <span data-ttu-id="c5d21-111">Registros de infraestructura de diagnóstico de Azure</span><span class="sxs-lookup"><span data-stu-id="c5d21-111">Azure Diagnostics infrastructure logs</span></span>

<span data-ttu-id="c5d21-112">En este artículo se muestra cómo configurar Diagnósticos de Azure con Centros de eventos de manera integral.</span><span class="sxs-lookup"><span data-stu-id="c5d21-112">This article shows you how to configure Azure Diagnostics with Event Hubs from end to end.</span></span> <span data-ttu-id="c5d21-113">También se proporcionan instrucciones para los siguientes escenarios comunes:</span><span class="sxs-lookup"><span data-stu-id="c5d21-113">Guidance is also provided for the following common scenarios:</span></span>

* <span data-ttu-id="c5d21-114">Cómo personalizar los registros y las métricas enviadas a Event Hubs</span><span class="sxs-lookup"><span data-stu-id="c5d21-114">How to customize the logs and metrics that get sent to Event Hubs</span></span>
* <span data-ttu-id="c5d21-115">Cómo cambiar la configuración de cada entorno</span><span class="sxs-lookup"><span data-stu-id="c5d21-115">How to change configurations in each environment</span></span>
* <span data-ttu-id="c5d21-116">Cómo ver los datos de secuencia de los Centros de eventos</span><span class="sxs-lookup"><span data-stu-id="c5d21-116">How to view Event Hubs stream data</span></span>
* <span data-ttu-id="c5d21-117">Cómo solucionar los problemas de conexión</span><span class="sxs-lookup"><span data-stu-id="c5d21-117">How to troubleshoot the connection</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="c5d21-118">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="c5d21-118">Prerequisites</span></span>
<span data-ttu-id="c5d21-119">La recepción de Diagnósticos de Azure en Event Hubs se admite en Cloud Services, Virtual Machines, Conjuntos de escalado de máquinas virtuales y Service Fabric a partir de Azure SDK 2.9 y las correspondientes herramientas de Azure Tools para Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c5d21-119">Event Hubs receieving data from Azure Diagnostics is supported in Cloud Services, VMs, Virtual Machine Scale Sets, and Service Fabric starting in the Azure SDK 2.9 and the corresponding Azure Tools for Visual Studio.</span></span>

* <span data-ttu-id="c5d21-120">La extensión de Diagnósticos de Azure 1.6 ([Azure SDK para .NET 2.9 o posterior](https://azure.microsoft.com/downloads/) sirve a este fin de forma predeterminada).</span><span class="sxs-lookup"><span data-stu-id="c5d21-120">Azure Diagnostics extension 1.6 ([Azure SDK for .NET 2.9 or later](https://azure.microsoft.com/downloads/) targets this by default)</span></span>
* [<span data-ttu-id="c5d21-121">Visual Studio 2013 o posterior.</span><span class="sxs-lookup"><span data-stu-id="c5d21-121">Visual Studio 2013 or later</span></span>](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)
* <span data-ttu-id="c5d21-122">Configuraciones existentes de Diagnósticos de Azure en una aplicación mediante un archivo *.wadcfgx* y uno de los siguientes métodos:</span><span class="sxs-lookup"><span data-stu-id="c5d21-122">Existing configurations of Azure Diagnostics in an application by using a *.wadcfgx* file and one of the following methods:</span></span>
  * <span data-ttu-id="c5d21-123">Visual Studio: [Configuración de Diagnósticos en Servicios en la nube y Máquinas virtuales de Azure](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md)</span><span class="sxs-lookup"><span data-stu-id="c5d21-123">Visual Studio: [Configuring Diagnostics for Azure Cloud Services and Virtual Machines](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md)</span></span>
  * <span data-ttu-id="c5d21-124">Windows PowerShell: [Habilitar el diagnóstico en Servicios en la nube de Azure mediante PowerShell](../cloud-services/cloud-services-diagnostics-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="c5d21-124">Windows PowerShell: [Enable diagnostics in Azure Cloud Services using PowerShell](../cloud-services/cloud-services-diagnostics-powershell.md)</span></span>
* <span data-ttu-id="c5d21-125">Espacio de nombres de Event Hubs aprovisionado según el artículo [Introducción a los Event Hubs](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)</span><span class="sxs-lookup"><span data-stu-id="c5d21-125">Event Hubs namespace provisioned per the article, [Get started with Event Hubs](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)</span></span>

## <a name="connect-azure-diagnostics-to-event-hubs-sink"></a><span data-ttu-id="c5d21-126">Conectar Diagnósticos de Azure al receptor de Centros de eventos</span><span class="sxs-lookup"><span data-stu-id="c5d21-126">Connect Azure Diagnostics to Event Hubs sink</span></span>
<span data-ttu-id="c5d21-127">De forma predeterminada, Diagnósticos de Azure siempre envía registros y métricas a una cuenta de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="c5d21-127">By default, Azure Diagnostics always sends logs and metrics to an Azure Storage account.</span></span> <span data-ttu-id="c5d21-128">Una aplicación también puede enviar datos a Event Hubs con la incorporación de una nueva sección **Sinks** al elemento **PublicConfig** / **WadCfg** del archivo *.wadcfgx*.</span><span class="sxs-lookup"><span data-stu-id="c5d21-128">An application may also send data to Event Hubs by adding a new **Sinks** section under the **PublicConfig** / **WadCfg** element of the *.wadcfgx* file.</span></span> <span data-ttu-id="c5d21-129">En Visual Studio, el archivo *.wadcfgx* está almacenado en la siguiente ruta de acceso: **Proyecto de servicio en la nube** > **Roles** > **(nombreDelRol)** > archivo **diagnostics.wadcfgx**.</span><span class="sxs-lookup"><span data-stu-id="c5d21-129">In Visual Studio, the *.wadcfgx* file is stored in the following path: **Cloud Service Project** > **Roles** > **(RoleName)** > **diagnostics.wadcfgx** file.</span></span>

```xml
<SinksConfig>
  <Sink name="HotPath">
    <EventHub Url="https://diags-mycompany-ns.servicebus.windows.net/diageventhub" SharedAccessKeyName="SendRule" />
  </Sink>
</SinksConfig>
```
```JSON
"SinksConfig": {
    "Sink": [
        {
            "name": "HotPath",
            "EventHub": {
                "Url": "https://diags-mycompany-ns.servicebus.windows.net/diageventhub",
                "SharedAccessKeyName": "SendRule"
            }
        }
    ]
}
```

<span data-ttu-id="c5d21-130">En este ejemplo, la dirección URL del centro de eventos se establece en el espacio de nombres completo del centro de eventos: espacio de nombres del centro de eventos + "/" + nombre del centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="c5d21-130">In this example, the event hub URL is set to the fully qualified namespace of the event hub: Event Hubs namespace  + "/" + event hub name.</span></span>  

<span data-ttu-id="c5d21-131">La dirección URL del centro de eventos se muestra en el [Azure portal](http://go.microsoft.com/fwlink/?LinkID=213885) del panel de Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="c5d21-131">The event hub URL is displayed in the [Azure portal](http://go.microsoft.com/fwlink/?LinkID=213885) on the Event Hubs dashboard.</span></span>  

<span data-ttu-id="c5d21-132">El nombre **Sink** se puede establecer en cualquier cadena válida siempre y cuando se use el mismo valor sistemáticamente en el archivo de configuración.</span><span class="sxs-lookup"><span data-stu-id="c5d21-132">The **Sink** name can be set to any valid string as long as the same value is used consistently throughout the config file.</span></span>

> [!NOTE]
> <span data-ttu-id="c5d21-133">Puede que haya más receptores configurados en esta sección, como *applicationInsights* .</span><span class="sxs-lookup"><span data-stu-id="c5d21-133">There may be additional sinks, such as *applicationInsights* configured in this section.</span></span> <span data-ttu-id="c5d21-134">Diagnósticos de Azure permite definir uno o varios receptores, si cada uno de ellos también se declara en la sección **PrivateConfig** .</span><span class="sxs-lookup"><span data-stu-id="c5d21-134">Azure Diagnostics allows one or more sinks to be defined if each sink is also declared in the **PrivateConfig** section.</span></span>  
>
>

<span data-ttu-id="c5d21-135">El receptor de Centros de eventos también se debe declarar y definir en la sección **PrivateConfig** del archivo de configuración *.wadcfgx* .</span><span class="sxs-lookup"><span data-stu-id="c5d21-135">The Event Hubs sink must also be declared and defined in the **PrivateConfig** section of the *.wadcfgx* config file.</span></span>

```XML
<PrivateConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
  <StorageAccount name="{account name}" key="{account key}" endpoint="{optional storage endpoint}" />
  <EventHub Url="https://diags-mycompany-ns.servicebus.windows.net/diageventhub" SharedAccessKeyName="SendRule" SharedAccessKey="{base64 encoded key}" />
</PrivateConfig>
```
```JSON
{
    "storageAccountName": "{account name}",
    "storageAccountKey": "{account key}",
    "storageAccountEndPoint": "{optional storage endpoint}",
    "EventHub": {
        "Url": "https://diags-mycompany-ns.servicebus.windows.net/diageventhub",
        "SharedAccessKeyName": "SendRule",
        "SharedAccessKey": "{base64 encoded key}"
    }
}
```

<span data-ttu-id="c5d21-136">El valor de `SharedAccessKeyName` debe coincidir con una directiva y una clave de firma de acceso compartido (SAS) que se hayan definido en el espacio de nombres de **Centros de eventos** .</span><span class="sxs-lookup"><span data-stu-id="c5d21-136">The `SharedAccessKeyName` value must match a Shared Access Signature (SAS) key and policy that has been defined in the **Event Hubs** namespace.</span></span> <span data-ttu-id="c5d21-137">Vaya al panel de Centros de eventos en el [Portal de Azure](https://manage.windowsazure.com), seleccione la pestaña **Configurar** y configure una directiva con nombre (por ejemplo, SendRule) que tenga permisos de *envío* .</span><span class="sxs-lookup"><span data-stu-id="c5d21-137">Browse to the Event Hubs dashboard in the [Azure portal](https://manage.windowsazure.com), click the **Configure** tab, and set up a named policy (for example, "SendRule") that has *Send* permissions.</span></span> <span data-ttu-id="c5d21-138">El elemento **StorageAccount** también se declara en **PrivateConfig**.</span><span class="sxs-lookup"><span data-stu-id="c5d21-138">The **StorageAccount** is also declared in **PrivateConfig**.</span></span> <span data-ttu-id="c5d21-139">No hace falta cambiar estos valores si funcionan.</span><span class="sxs-lookup"><span data-stu-id="c5d21-139">There is no need to change values here if they are working.</span></span> <span data-ttu-id="c5d21-140">En este ejemplo, dejamos los valores vacíos, que indica que un activo de bajada establecerá los valores.</span><span class="sxs-lookup"><span data-stu-id="c5d21-140">In this example, we leave the values empty, which is a sign that a downstream asset will set the values.</span></span> <span data-ttu-id="c5d21-141">Por ejemplo, el archivo de configuración del entorno *ServiceConfiguration.Cloud.cscfg* establecerá las claves y los nombres apropiados.</span><span class="sxs-lookup"><span data-stu-id="c5d21-141">For example, the *ServiceConfiguration.Cloud.cscfg* environment configuration file sets the environment-appropriate names and keys.</span></span>  

> [!WARNING]
> <span data-ttu-id="c5d21-142">Tenga en cuenta que la clave SAS de Centros de eventos se almacena en texto sin formato en el archivo *wadcfgx* .</span><span class="sxs-lookup"><span data-stu-id="c5d21-142">The Event Hubs SAS key is stored in plain text in the *.wadcfgx* file.</span></span> <span data-ttu-id="c5d21-143">A menudo, esta clave se registra en el control de código fuente o está disponible como un recurso en el servidor de compilación, por lo que debe protegerla de la manera adecuada.</span><span class="sxs-lookup"><span data-stu-id="c5d21-143">Often, this key is checked in to source code control or is available as an asset in your build server, so you should protect it as appropriate.</span></span> <span data-ttu-id="c5d21-144">Se recomienda usar aquí una clave SAS con permisos de *solo envío* para que los usuarios malintencionados puedan escribir en el Centro de eventos, pero nunca realizar operaciones de administración ni de escucha.</span><span class="sxs-lookup"><span data-stu-id="c5d21-144">We recommend that you use a SAS key here with *Send only* permissions so that a malicious user can write to the event hub, but not listen to it or manage it.</span></span>
>
>

## <a name="configure-azure-diagnostics-to-send-logs-and-metrics-to-event-hubs"></a><span data-ttu-id="c5d21-145">Configuración de Diagnósticos de Azure para enviar registros y métricas a Event Hubs</span><span class="sxs-lookup"><span data-stu-id="c5d21-145">Configure Azure Diagnostics to send logs and metrics to Event Hubs</span></span>
<span data-ttu-id="c5d21-146">Como se ha indicado anteriormente, todos los datos de diagnóstico predeterminados y personalizados (es decir, métricas y registros) se envían automáticamente a Azure Storage en los intervalos configurados.</span><span class="sxs-lookup"><span data-stu-id="c5d21-146">As discussed previously, all default and custom diagnostics data, that is, metrics and logs, is automatically sent to Azure Storage in the configured intervals.</span></span> <span data-ttu-id="c5d21-147">Con Event Hubs y cualquier receptor adicional, puede especificar que cualquier nodo raíz u hoja de la jerarquía se envíe al centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="c5d21-147">With Event Hubs and any additional sink, you can specify any root or leaf node in the hierarchy to be sent to the event hub.</span></span> <span data-ttu-id="c5d21-148">Esto incluye eventos ETW, contadores de rendimiento, registros de eventos de Windows y registros de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="c5d21-148">This includes ETW events, performance counters, Windows event logs, and application logs.</span></span>   

<span data-ttu-id="c5d21-149">Es importante tener en cuenta cuántos puntos de datos se deben transferir realmente a Centros de eventos.</span><span class="sxs-lookup"><span data-stu-id="c5d21-149">It is important to consider how many data points should actually be transferred to Event Hubs.</span></span> <span data-ttu-id="c5d21-150">Normalmente, los desarrolladores transfieren datos de ruta de acceso activa y de baja latencia que deben consumirse e interpretarse rápidamente.</span><span class="sxs-lookup"><span data-stu-id="c5d21-150">Typically, developers transfer low-latency hot-path data that must be consumed and interpreted quickly.</span></span> <span data-ttu-id="c5d21-151">Los sistemas que supervisan las alertas o las reglas de escalado automático son algunos ejemplos.</span><span class="sxs-lookup"><span data-stu-id="c5d21-151">Systems that monitor alerts or autoscale rules are examples.</span></span> <span data-ttu-id="c5d21-152">Un desarrollador también puede configurar un almacén de búsqueda o un almacén de análisis alternativo (por ejemplo, Análisis de transmisiones de Azure, Elasticsearch, un sistema de supervisión personalizado o un sistema de supervisión favorito de terceros).</span><span class="sxs-lookup"><span data-stu-id="c5d21-152">A developer might also configure an alternate analysis store or search store -- for example, Azure Stream Analytics, Elasticsearch, a custom monitoring system, or a favorite monitoring system from others.</span></span>

<span data-ttu-id="c5d21-153">Las siguientes son algunas configuraciones de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="c5d21-153">The following are some example configurations.</span></span>

```xml
<PerformanceCounters scheduledTransferPeriod="PT1M" sinks="HotPath">
  <PerformanceCounterConfiguration counterSpecifier="\Memory\Available MBytes" sampleRate="PT3M" />
  <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\ISAPI Extension Requests/sec" sampleRate="PT3M" />
  <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\Bytes Total/Sec" sampleRate="PT3M" />
</PerformanceCounters>
```
```JSON
"PerformanceCounters": {
    "scheduledTransferPeriod": "PT1M",
    "sinks": "HotPath",
    "PerformanceCounterConfiguration": [
        {
            "counterSpecifier": "\\Processor(_Total)\\% Processor Time",
            "sampleRate": "PT3M"
        },
        {
            "counterSpecifier": "\\Memory\\Available MBytes",
            "sampleRate": "PT3M"
        },
        {
            "counterSpecifier": "\\Web Service(_Total)\\ISAPI Extension Requests/sec",
            "sampleRate": "PT3M"
        }
    ]
}
```

<span data-ttu-id="c5d21-154">En el ejemplo anterior, el receptor se aplica al nodo principal **PerformanceCounters** de la jerarquía, lo que significa que todos los nodos secundarios **PerformanceCounters** se enviarán a Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="c5d21-154">In the above example, the sink is applied to the parent **PerformanceCounters** node in the hierarchy, which means all child **PerformanceCounters** will be sent to Event Hubs.</span></span>  

```xml
<PerformanceCounters scheduledTransferPeriod="PT1M">
  <PerformanceCounterConfiguration counterSpecifier="\Memory\Available MBytes" sampleRate="PT3M" />
  <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\ISAPI Extension Requests/sec" sampleRate="PT3M" />
  <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Queued" sampleRate="PT3M" sinks="HotPath" />
  <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Rejected" sampleRate="PT3M" sinks="HotPath"/>
  <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT3M" sinks="HotPath"/>
</PerformanceCounters>
```
```JSON
"PerformanceCounters": {
    "scheduledTransferPeriod": "PT1M",
    "PerformanceCounterConfiguration": [
        {
            "counterSpecifier": "\\Processor(_Total)\\% Processor Time",
            "sampleRate": "PT3M",
            "sinks": "HotPath"
        },
        {
            "counterSpecifier": "\\Memory\\Available MBytes",
            "sampleRate": "PT3M"
        },
        {
            "counterSpecifier": "\\Web Service(_Total)\\ISAPI Extension Requests/sec",
            "sampleRate": "PT3M"
        },
        {
            "counterSpecifier": "\\ASP.NET\\Requests Rejected",
            "sampleRate": "PT3M",
            "sinks": "HotPath"
        },
        {
            "counterSpecifier": "\\ASP.NET\\Requests Queued",
            "sampleRate": "PT3M",
            "sinks": "HotPath"
        }
    ]
}
```

<span data-ttu-id="c5d21-155">En el ejemplo anterior, el receptor se aplica solo a tres contadores: **Solicitudes en cola**, **Solicitudes rechazadas** y **% de tiempo de procesador**.</span><span class="sxs-lookup"><span data-stu-id="c5d21-155">In the previous example, the sink is applied to only three counters: **Requests Queued**, **Requests Rejected**, and **% Processor time**.</span></span>  

<span data-ttu-id="c5d21-156">En el ejemplo siguiente se muestra cómo un desarrollador puede limitar la cantidad de datos que se envían como métricas críticas usadas para el estado del servicio.</span><span class="sxs-lookup"><span data-stu-id="c5d21-156">The following example shows how a developer can limit the amount of sent data to be the critical metrics that are used for this service’s health.</span></span>  

```XML
<Logs scheduledTransferPeriod="PT1M" sinks="HotPath" scheduledTransferLogLevelFilter="Error" />
```
```JSON
"Logs": {
    "scheduledTransferPeriod": "PT1M",
    "scheduledTransferLogLevelFilter": "Error",
    "sinks": "HotPath"
}
```

<span data-ttu-id="c5d21-157">En este ejemplo, el receptor se aplica a los registros y se filtra solo para el seguimiento de nivel Error.</span><span class="sxs-lookup"><span data-stu-id="c5d21-157">In this example, the sink is applied to logs and is filtered only to error level trace.</span></span>

## <a name="deploy-and-update-a-cloud-services-application-and-diagnostics-config"></a><span data-ttu-id="c5d21-158">Implementación y actualización de una aplicación de servicios en la nube y configuración de diagnósticos</span><span class="sxs-lookup"><span data-stu-id="c5d21-158">Deploy and update a Cloud Services application and diagnostics config</span></span>
<span data-ttu-id="c5d21-159">Visual Studio proporciona la manera más sencilla de implementar la aplicación y la configuración del receptor de Centros de eventos.</span><span class="sxs-lookup"><span data-stu-id="c5d21-159">Visual Studio provides the easiest path to deploy the application and Event Hubs sink configuration.</span></span> <span data-ttu-id="c5d21-160">Para ver y editar el archivo, abra el archivo *.wadcfgx* en Visual Studio, edítelo y guárdelo.</span><span class="sxs-lookup"><span data-stu-id="c5d21-160">To view and edit the file, open the *.wadcfgx* file in Visual Studio, edit it, and save it.</span></span> <span data-ttu-id="c5d21-161">La ruta de acceso es **Proyecto de servicio en la nube** > **Roles** > **(nombreDelRol)** > **diagnostics.wadcfgx**.</span><span class="sxs-lookup"><span data-stu-id="c5d21-161">The path is **Cloud Service Project** > **Roles** > **(RoleName)** > **diagnostics.wadcfgx**.</span></span>  

<span data-ttu-id="c5d21-162">En este punto, toda la implementación y las acciones de actualización de la implementación en Visual Studio, Visual Studio Team System, además de todos los comandos o scripts que se basan en MSBuild y usan el destino **/t:publish** incluirán el archivo *.wadcfgx* en el proceso de empaquetado.</span><span class="sxs-lookup"><span data-stu-id="c5d21-162">At this point, all deployment and deployment update actions in Visual Studio, Visual Studio Team System, and all commands or scripts that are based on MSBuild and use the **/t:publish** target include the *.wadcfgx* in the packaging process.</span></span> <span data-ttu-id="c5d21-163">Además, las implementaciones y actualizaciones implementan el archivo en Azure mediante la extensión del agente de Diagnósticos de Azure en las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="c5d21-163">In addition, deployments and updates deploy the file to Azure by using the appropriate Azure Diagnostics agent extension on your VMs.</span></span>

<span data-ttu-id="c5d21-164">Después de implementar la aplicación y la configuración de Diagnósticos de Azure, verá inmediatamente la actividad en el panel del centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="c5d21-164">After you deploy the application and Azure Diagnostics configuration, you will immediately see activity in the dashboard of the event hub.</span></span> <span data-ttu-id="c5d21-165">Esto indica que está listo para continuar y ver los datos de la ruta de acceso activa en el cliente de escucha o la herramienta de análisis que prefiera.</span><span class="sxs-lookup"><span data-stu-id="c5d21-165">This indicates that you're ready to move on to viewing the hot-path data in the listener client or analysis tool of your choice.</span></span>  

<span data-ttu-id="c5d21-166">En la siguiente figura, el panel de Event Hubs muestra el envío correcto de los datos de diagnóstico al centro de eventos a partir de las 23:00.</span><span class="sxs-lookup"><span data-stu-id="c5d21-166">In the following figure, the Event Hubs dashboard shows healthy sending of diagnostics data to the event hub starting sometime after 11 PM.</span></span> <span data-ttu-id="c5d21-167">Ese es el momento en que la aplicación se ha implementado con un archivo *.wadcfgx* actualizado y el receptor se ha configurado correctamente.</span><span class="sxs-lookup"><span data-stu-id="c5d21-167">That's when the application was deployed with an updated *.wadcfgx* file, and the sink was configured properly.</span></span>

![][0]  

> [!NOTE]
> <span data-ttu-id="c5d21-168">Al realizar actualizaciones en el archivo de configuración de Diagnósticos de Azure (.wadcfgx), se recomienda insertar las actualizaciones en toda la aplicación, además de la configuración, mediante el script de publicación de Visual Studio o el de Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c5d21-168">When you make updates to the Azure Diagnostics config file (.wadcfgx), it's recommended that you push the updates to the entire application as well as the configuration by using either Visual Studio publishing, or a Windows PowerShell script.</span></span>  
>
>

## <a name="view-hot-path-data"></a><span data-ttu-id="c5d21-169">Ver los datos de la ruta de acceso activa</span><span class="sxs-lookup"><span data-stu-id="c5d21-169">View hot-path data</span></span>
<span data-ttu-id="c5d21-170">Como se explicó anteriormente, la escucha y el procesamiento de datos de Centros de eventos tienen varias finalidades.</span><span class="sxs-lookup"><span data-stu-id="c5d21-170">As discussed previously, there are many use cases for listening to and processing Event Hubs data.</span></span>

<span data-ttu-id="c5d21-171">Un enfoque sencillo es crear una pequeña aplicación de consola de prueba para escuchar el centro de eventos e imprimir el flujo de salida.</span><span class="sxs-lookup"><span data-stu-id="c5d21-171">One simple approach is to create a small test console application to listen to the event hub and print the output stream.</span></span> <span data-ttu-id="c5d21-172">Puede colocar el código siguiente (que se explica con más detalle en [Introducción a Event Hubs](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)) en una aplicación de consola.</span><span class="sxs-lookup"><span data-stu-id="c5d21-172">You can place the following code, which is explained in more detail in [Get started with Event Hubs](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)), in a console application.</span></span>  

<span data-ttu-id="c5d21-173">Tenga en cuenta que la aplicación de consola debe incluir el [paquete NuGet del host del procesador de eventos](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/).</span><span class="sxs-lookup"><span data-stu-id="c5d21-173">Note that the console application must include the [Event Processor Host NuGet package](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/).</span></span>  

<span data-ttu-id="c5d21-174">No olvide sustituir los valores que aparecen entre corchetes angulares en la función **Main** por los valores de sus recursos.</span><span class="sxs-lookup"><span data-stu-id="c5d21-174">Remember to replace the values in angle brackets in the **Main** function with values for your resources.</span></span>   

```csharp
//Console application code for EventHub test client
using System;
using System.Collections.Generic;
using System.Diagnostics;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using Microsoft.ServiceBus.Messaging;

namespace EventHubListener
{
    class SimpleEventProcessor : IEventProcessor
    {
        Stopwatch checkpointStopWatch;

        async Task IEventProcessor.CloseAsync(PartitionContext context, CloseReason reason)
        {
            Console.WriteLine("Processor Shutting Down. Partition '{0}', Reason: '{1}'.", context.Lease.PartitionId, reason);
            if (reason == CloseReason.Shutdown)
            {
                await context.CheckpointAsync();
            }
        }

        Task IEventProcessor.OpenAsync(PartitionContext context)
        {
            Console.WriteLine("SimpleEventProcessor initialized.  Partition: '{0}', Offset: '{1}'", context.Lease.PartitionId, context.Lease.Offset);
            this.checkpointStopWatch = new Stopwatch();
            this.checkpointStopWatch.Start();
            return Task.FromResult<object>(null);
        }

        async Task IEventProcessor.ProcessEventsAsync(PartitionContext context, IEnumerable<EventData> messages)
        {
            foreach (EventData eventData in messages)
            {
                string data = Encoding.UTF8.GetString(eventData.GetBytes());
                    Console.WriteLine(string.Format("Message received.  Partition: '{0}', Data: '{1}'",
                        context.Lease.PartitionId, data));

                foreach (var x in eventData.Properties)
                {
                    Console.WriteLine(string.Format("    {0} = {1}", x.Key, x.Value));
                }
            }

            //Call checkpoint every 5 minutes, so that worker can resume processing from 5 minutes back if it restarts.
            if (this.checkpointStopWatch.Elapsed > TimeSpan.FromMinutes(5))
            {
                await context.CheckpointAsync();
                this.checkpointStopWatch.Restart();
            }
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            string eventHubConnectionString = "Endpoint= <your connection string>”
            string eventHubName = "<Event hub name>";
            string storageAccountName = "<Storage account name>";
            string storageAccountKey = "<Storage account key>”;
            string storageConnectionString = string.Format("DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}", storageAccountName, storageAccountKey);

            string eventProcessorHostName = Guid.NewGuid().ToString();
            EventProcessorHost eventProcessorHost = new EventProcessorHost(eventProcessorHostName, eventHubName, EventHubConsumerGroup.DefaultGroupName, eventHubConnectionString, storageConnectionString);
            Console.WriteLine("Registering EventProcessor...");
            var options = new EventProcessorOptions();
            options.ExceptionReceived += (sender, e) => { Console.WriteLine(e.Exception); };
            eventProcessorHost.RegisterEventProcessorAsync<SimpleEventProcessor>(options).Wait();

            Console.WriteLine("Receiving. Press enter key to stop worker.");
            Console.ReadLine();
            eventProcessorHost.UnregisterEventProcessorAsync().Wait();
        }
    }
}
```

## <a name="troubleshoot-event-hubs-sinks"></a><span data-ttu-id="c5d21-175">Solución de problemas con los receptores de Event Hubs</span><span class="sxs-lookup"><span data-stu-id="c5d21-175">Troubleshoot Event Hubs sinks</span></span>
* <span data-ttu-id="c5d21-176">El centro de eventos no muestra la actividad de eventos entrante o saliente esperada.</span><span class="sxs-lookup"><span data-stu-id="c5d21-176">The event hub does not show incoming or outgoing event activity as expected.</span></span>

    <span data-ttu-id="c5d21-177">Compruebe que el centro de eventos esté correctamente aprovisionado.</span><span class="sxs-lookup"><span data-stu-id="c5d21-177">Check that your event hub is successfully provisioned.</span></span> <span data-ttu-id="c5d21-178">Toda la información de conexión de la sección **PrivateConfig** de *wadcfgx* debe coincidir con los valores de su recurso, tal y como se muestra en el portal.</span><span class="sxs-lookup"><span data-stu-id="c5d21-178">All connection info in the **PrivateConfig** section of *.wadcfgx* must match the values of your resource as seen in the portal.</span></span> <span data-ttu-id="c5d21-179">Asegúrese de tener una directiva SAS definida (SendRule en el ejemplo) en el portal y que se haya concedido el permiso de *envío* .</span><span class="sxs-lookup"><span data-stu-id="c5d21-179">Make sure that you have a SAS policy defined ("SendRule" in the example) in the portal and that *Send* permission is granted.</span></span>  
* <span data-ttu-id="c5d21-180">Después de una actualización, el centro de eventos ya no muestra actividad de eventos entrante o saliente.</span><span class="sxs-lookup"><span data-stu-id="c5d21-180">After an update, the event hub no longer shows incoming or outgoing event activity.</span></span>

    <span data-ttu-id="c5d21-181">Primero, asegúrese de que la información del centro de eventos y de la configuración es correcta tal y como se ha explicado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="c5d21-181">First, make sure that the event hub and configuration info is correct as explained previously.</span></span> <span data-ttu-id="c5d21-182">A veces, **PrivateConfig** se restablece en una actualización de implementación.</span><span class="sxs-lookup"><span data-stu-id="c5d21-182">Sometimes the **PrivateConfig** is reset in a deployment update.</span></span> <span data-ttu-id="c5d21-183">La solución recomendada consiste en realizar todos los cambios en *.wadcfgx* en el proyecto y, luego, insertar una actualización completa de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c5d21-183">The recommended fix is to make all changes to *.wadcfgx* in the project and then push a complete application update.</span></span> <span data-ttu-id="c5d21-184">Si no es posible, asegúrese de que la actualización de diagnósticos inserta completamente **PrivateConfig** , lo que incluye la clave SAS.</span><span class="sxs-lookup"><span data-stu-id="c5d21-184">If this is not possible, make sure that the diagnostics update pushes a complete **PrivateConfig** that includes the SAS key.</span></span>  
* <span data-ttu-id="c5d21-185">He probado las sugerencias y el centro de eventos sigue sin funcionar.</span><span class="sxs-lookup"><span data-stu-id="c5d21-185">I tried the suggestions, and the event hub is still not working.</span></span>

    <span data-ttu-id="c5d21-186">Pruebe a mirar en la tabla de Almacenamiento de Azure que contiene registros y errores del servicio Diagnósticos de Azure: **WADDiagnosticInfrastructureLogsTable**.</span><span class="sxs-lookup"><span data-stu-id="c5d21-186">Try looking in the Azure Storage table that contains logs and errors for Azure Diagnostics itself: **WADDiagnosticInfrastructureLogsTable**.</span></span> <span data-ttu-id="c5d21-187">Una opción es usar una herramienta como el [Explorador de almacenamiento de Azure](http://www.storageexplorer.com) para conectarse a esta cuenta de almacenamiento, ver esta tabla y agregar una consulta para TimeStamp en las últimas 24 horas.</span><span class="sxs-lookup"><span data-stu-id="c5d21-187">One option is to use a tool such as [Azure Storage Explorer](http://www.storageexplorer.com) to connect to this storage account, view this table, and add a query for TimeStamp in the last 24 hours.</span></span> <span data-ttu-id="c5d21-188">Puede usar la herramienta para exportar un archivo .csv y abrirlo en una aplicación como Microsoft Excel.</span><span class="sxs-lookup"><span data-stu-id="c5d21-188">You can use the tool to export a .csv file and open it in an application such as Microsoft Excel.</span></span> <span data-ttu-id="c5d21-189">Excel facilita la búsqueda de cadenas de tarjeta de llamadas, como **EventHubs**, para ver qué error se notifica.</span><span class="sxs-lookup"><span data-stu-id="c5d21-189">Excel makes it easy to search for calling-card strings, such as **EventHubs**, to see what error is reported.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="c5d21-190">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c5d21-190">Next steps</span></span>
<span data-ttu-id="c5d21-191">•    [Más información sobre Event Hubs](https://azure.microsoft.com/services/event-hubs/)</span><span class="sxs-lookup"><span data-stu-id="c5d21-191">•    [Learn more about Event Hubs](https://azure.microsoft.com/services/event-hubs/)</span></span>

## <a name="appendix-complete-azure-diagnostics-configuration-file-wadcfgx-example"></a><span data-ttu-id="c5d21-192">Apéndice: Archivo de configuración completo de Diagnósticos de Azure (.wadcfgx): ejemplo</span><span class="sxs-lookup"><span data-stu-id="c5d21-192">Appendix: Complete Azure Diagnostics configuration file (.wadcfgx) example</span></span>
```xml
<?xml version="1.0" encoding="utf-8"?>
<DiagnosticsConfiguration xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
  <PublicConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
    <WadCfg>
      <DiagnosticMonitorConfiguration overallQuotaInMB="4096" sinks="applicationInsights.errors">
        <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter="Error" />
        <Directories scheduledTransferPeriod="PT1M">
          <IISLogs containerName="wad-iis-logfiles" />
          <FailedRequestLogs containerName="wad-failedrequestlogs" />
        </Directories>
        <PerformanceCounters scheduledTransferPeriod="PT1M" sinks="HotPath">
          <PerformanceCounterConfiguration counterSpecifier="\Memory\Available MBytes" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\ISAPI Extension Requests/sec" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\Bytes Total/Sec" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\ASP.NET Applications(__Total__)\Requests/Sec" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\ASP.NET Applications(__Total__)\Errors Total/Sec" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Queued" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Rejected" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT3M" />
        </PerformanceCounters>
        <WindowsEventLog scheduledTransferPeriod="PT1M">
          <DataSource name="Application!*" />
        </WindowsEventLog>
        <CrashDumps>
          <CrashDumpConfiguration processName="WaIISHost.exe" />
          <CrashDumpConfiguration processName="WaWorkerHost.exe" />
          <CrashDumpConfiguration processName="w3wp.exe" />
        </CrashDumps>
        <Logs scheduledTransferPeriod="PT1M" sinks="HotPath" scheduledTransferLogLevelFilter="Error" />
      </DiagnosticMonitorConfiguration>
      <SinksConfig>
        <Sink name="HotPath">
          <EventHub Url="https://diageventhub-py-ns.servicebus.windows.net/diageventhub-py" SharedAccessKeyName="SendRule" />
        </Sink>
        <Sink name="applicationInsights">
          <ApplicationInsights />
          <Channels>
            <Channel logLevel="Error" name="errors" />
          </Channels>
        </Sink>
      </SinksConfig>
    </WadCfg>
    <StorageAccount>ACCOUNT_NAME</StorageAccount>
  </PublicConfig>
  <PrivateConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
    <StorageAccount name="{account name}" key="{account key}" endpoint="{storage endpoint}" />
    <EventHub Url="https://diageventhub-py-ns.servicebus.windows.net/diageventhub-py" SharedAccessKeyName="SendRule" SharedAccessKey="YOUR_KEY_HERE" />
  </PrivateConfig>
  <IsEnabled>true</IsEnabled>
</DiagnosticsConfiguration>
```

<span data-ttu-id="c5d21-193">El archivo *ServiceConfiguration.Cloud.cscfg* complementario para este ejemplo se parece al siguiente.</span><span class="sxs-lookup"><span data-stu-id="c5d21-193">The complementary *ServiceConfiguration.Cloud.cscfg* for this example looks like the following.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceConfiguration serviceName="MyFixItCloudService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration" osFamily="3" osVersion="*" schemaVersion="2015-04.2.6">
  <Role name="MyFixIt.WorkerRole">
    <Instances count="1" />
    <ConfigurationSettings>
      <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="YOUR_CONNECTION_STRING" />
    </ConfigurationSettings>
  </Role>
</ServiceConfiguration>
```

<span data-ttu-id="c5d21-194">La configuración JSON equivalente para máquinas virtuales es la siguiente:</span><span class="sxs-lookup"><span data-stu-id="c5d21-194">Equivalent Json based settings for virtual machines is as follows:</span></span>
```JSON
"settings": {
    "WadCfg": {
        "DiagnosticMonitorConfiguration": {
            "overallQuotaInMB": 4096,
            "sinks": "applicationInsights.errors",
            "DiagnosticInfrastructureLogs": {
                "scheduledTransferLogLevelFilter": "Error"
            },
            "Directories": {
                "scheduledTransferPeriod": "PT1M",
                "IISLogs": {
                    "containerName": "wad-iis-logfiles"
                },
                "FailedRequestLogs": {
                    "containerName": "wad-failedrequestlogs"
                }
            },
            "PerformanceCounters": {
                "scheduledTransferPeriod": "PT1M",
                "sinks": "HotPath",
                "PerformanceCounterConfiguration": [
                    {
                        "counterSpecifier": "\\Memory\\Available MBytes",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\Web Service(_Total)\\ISAPI Extension Requests/sec",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\Web Service(_Total)\\Bytes Total/Sec",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\ASP.NET Applications(__Total__)\\Requests/Sec",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\ASP.NET Applications(__Total__)\\Errors Total/Sec",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\ASP.NET\\Requests Queued",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\ASP.NET\\Requests Rejected",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\Processor(_Total)\\% Processor Time",
                        "sampleRate": "PT3M"
                    }
                ]
            },
            "WindowsEventLog": {
                "scheduledTransferPeriod": "PT1M",
                "DataSource": [
                    {
                        "name": "Application!*"
                    }
                ]
            },
            "Logs": {
                "scheduledTransferPeriod": "PT1M",
                "scheduledTransferLogLevelFilter": "Error",
                "sinks": "HotPath"
            }
        },
        "SinksConfig": {
            "Sink": [
                {
                    "name": "HotPath",
                    "EventHub": {
                        "Url": "https://diageventhub-py-ns.servicebus.windows.net/diageventhub-py",
                        "SharedAccessKeyName": "SendRule"
                    }
                },
                {
                    "name": "applicationInsights",
                    "ApplicationInsights": "",
                    "Channels": {
                        "Channel": [
                            {
                                "logLevel": "Error",
                                "name": "errors"
                            }
                        ]
                    }
                }
            ]
        }
    },
    "StorageAccount": "{account name}"
}


"protectedSettings": {
    "storageAccountName": "{account name}",
    "storageAccountKey": "{account key}",
    "storageAccountEndPoint": "{storage endpoint}",
    "EventHub": {
        "Url": "https://diageventhub-py-ns.servicebus.windows.net/diageventhub-py",
        "SharedAccessKeyName": "SendRule",
        "SharedAccessKey": "YOUR_KEY_HERE"
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="c5d21-195">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c5d21-195">Next steps</span></span>
<span data-ttu-id="c5d21-196">Para más información acerca de Event Hubs, visite los vínculos siguientes:</span><span class="sxs-lookup"><span data-stu-id="c5d21-196">You can learn more about Event Hubs by visiting the following links:</span></span>

* [<span data-ttu-id="c5d21-197">Información general de Event Hubs</span><span class="sxs-lookup"><span data-stu-id="c5d21-197">Event Hubs overview</span></span>](../event-hubs/event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="c5d21-198">Creación de un centro de eventos</span><span class="sxs-lookup"><span data-stu-id="c5d21-198">Create an event hub</span></span>](../event-hubs/event-hubs-create.md)
* [<span data-ttu-id="c5d21-199">Preguntas más frecuentes sobre Event Hubs</span><span class="sxs-lookup"><span data-stu-id="c5d21-199">Event Hubs FAQ</span></span>](../event-hubs/event-hubs-faq.md)

<!-- Images. -->
[0]: ../event-hubs/media/event-hubs-streaming-azure-diags-data/dashboard.png
