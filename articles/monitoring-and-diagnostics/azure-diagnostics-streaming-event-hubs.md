---
title: "datos de diagnóstico de Azure en hello ruta de acceso activa con los concentradores de eventos aaaStreaming | Documentos de Microsoft"
description: "Configuración de diagnóstico de Azure con los concentradores de eventos finalizar tooend, incluidos detalles de los escenarios comunes."
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
ms.openlocfilehash: a2528ddd0688d1c23a8631e769ca016dd79e4159
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="streaming-azure-diagnostics-data-in-hello-hot-path-by-using-event-hubs"></a><span data-ttu-id="ca05e-103">Transmisión de datos de diagnóstico de Azure en la ruta de acceso activa hello mediante el uso de los centros de eventos</span><span class="sxs-lookup"><span data-stu-id="ca05e-103">Streaming Azure Diagnostics data in hello hot path by using Event Hubs</span></span>
<span data-ttu-id="ca05e-104">Diagnósticos de Azure proporciona maneras flexibles toocollect métricas y los registros de servicios las máquinas virtuales (VM) en la nube y transferir tooAzure almacenamiento de resultados.</span><span class="sxs-lookup"><span data-stu-id="ca05e-104">Azure Diagnostics provides flexible ways toocollect metrics and logs from cloud services virtual machines (VMs) and transfer results tooAzure Storage.</span></span> <span data-ttu-id="ca05e-105">A partir de período de tiempo de hello (SDK 2.9) de marzo de 2016, puede enviar diagnósticos toocustom orígenes de datos y transferir datos de ruta de acceso activa en segundos mediante [centros de eventos de Azure](https://azure.microsoft.com/services/event-hubs/).</span><span class="sxs-lookup"><span data-stu-id="ca05e-105">Starting in hello March 2016 (SDK 2.9) time frame, you can send Diagnostics toocustom data sources and transfer hot path data in seconds by using [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/).</span></span>

<span data-ttu-id="ca05e-106">Entre los tipos de datos admitidos se incluyen:</span><span class="sxs-lookup"><span data-stu-id="ca05e-106">Supported data types include:</span></span>

* <span data-ttu-id="ca05e-107">Eventos de Seguimiento de eventos para Windows (ETW)</span><span class="sxs-lookup"><span data-stu-id="ca05e-107">Event Tracing for Windows (ETW) events</span></span>
* <span data-ttu-id="ca05e-108">Contadores de rendimiento</span><span class="sxs-lookup"><span data-stu-id="ca05e-108">Performance counters</span></span>
* <span data-ttu-id="ca05e-109">Registros de eventos de Windows</span><span class="sxs-lookup"><span data-stu-id="ca05e-109">Windows event logs</span></span>
* <span data-ttu-id="ca05e-110">Registros de aplicación</span><span class="sxs-lookup"><span data-stu-id="ca05e-110">Application logs</span></span>
* <span data-ttu-id="ca05e-111">Registros de infraestructura de diagnóstico de Azure</span><span class="sxs-lookup"><span data-stu-id="ca05e-111">Azure Diagnostics infrastructure logs</span></span>

<span data-ttu-id="ca05e-112">Este artículo muestra cómo tooconfigure diagnósticos de Azure con los concentradores de eventos de finalización tooend.</span><span class="sxs-lookup"><span data-stu-id="ca05e-112">This article shows you how tooconfigure Azure Diagnostics with Event Hubs from end tooend.</span></span> <span data-ttu-id="ca05e-113">También se proporciona orientación para hello escenarios comunes siguientes:</span><span class="sxs-lookup"><span data-stu-id="ca05e-113">Guidance is also provided for hello following common scenarios:</span></span>

* <span data-ttu-id="ca05e-114">Funcionamiento de los registros toocustomize hello y métricas que se envíen los centros de tooEvent</span><span class="sxs-lookup"><span data-stu-id="ca05e-114">How toocustomize hello logs and metrics that get sent tooEvent Hubs</span></span>
* <span data-ttu-id="ca05e-115">¿Cómo toochange configuraciones en cada entorno</span><span class="sxs-lookup"><span data-stu-id="ca05e-115">How toochange configurations in each environment</span></span>
* <span data-ttu-id="ca05e-116">Los concentradores de eventos de tooview cómo los datos de secuencia</span><span class="sxs-lookup"><span data-stu-id="ca05e-116">How tooview Event Hubs stream data</span></span>
* <span data-ttu-id="ca05e-117">¿Cómo tootroubleshoot Hola conexión</span><span class="sxs-lookup"><span data-stu-id="ca05e-117">How tootroubleshoot hello connection</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="ca05e-118">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="ca05e-118">Prerequisites</span></span>
<span data-ttu-id="ca05e-119">Datos de receieving de concentradores de eventos de diagnósticos de Azure se admiten en los servicios en la nube, máquinas virtuales, conjuntos de escalas de máquina Virtual y Service Fabric a partir de Azure SDK 2.9 de Hola y Hola correspondiente Azure Tools para Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ca05e-119">Event Hubs receieving data from Azure Diagnostics is supported in Cloud Services, VMs, Virtual Machine Scale Sets, and Service Fabric starting in hello Azure SDK 2.9 and hello corresponding Azure Tools for Visual Studio.</span></span>

* <span data-ttu-id="ca05e-120">La extensión de Diagnósticos de Azure 1.6 ([Azure SDK para .NET 2.9 o posterior](https://azure.microsoft.com/downloads/) sirve a este fin de forma predeterminada).</span><span class="sxs-lookup"><span data-stu-id="ca05e-120">Azure Diagnostics extension 1.6 ([Azure SDK for .NET 2.9 or later](https://azure.microsoft.com/downloads/) targets this by default)</span></span>
* [<span data-ttu-id="ca05e-121">Visual Studio 2013 o posterior.</span><span class="sxs-lookup"><span data-stu-id="ca05e-121">Visual Studio 2013 or later</span></span>](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)
* <span data-ttu-id="ca05e-122">Las configuraciones existentes de diagnósticos de Azure en una aplicación mediante el uso de un *wadcfgx* uno de los siguientes métodos de Hola y de archivo:</span><span class="sxs-lookup"><span data-stu-id="ca05e-122">Existing configurations of Azure Diagnostics in an application by using a *.wadcfgx* file and one of hello following methods:</span></span>
  * <span data-ttu-id="ca05e-123">Visual Studio: [Configuración de Diagnósticos en Servicios en la nube y Máquinas virtuales de Azure](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md)</span><span class="sxs-lookup"><span data-stu-id="ca05e-123">Visual Studio: [Configuring Diagnostics for Azure Cloud Services and Virtual Machines](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md)</span></span>
  * <span data-ttu-id="ca05e-124">Windows PowerShell: [Habilitar el diagnóstico en Servicios en la nube de Azure mediante PowerShell](../cloud-services/cloud-services-diagnostics-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="ca05e-124">Windows PowerShell: [Enable diagnostics in Azure Cloud Services using PowerShell](../cloud-services/cloud-services-diagnostics-powershell.md)</span></span>
* <span data-ttu-id="ca05e-125">Espacio de nombres de los centros de eventos aprovisionado por artículo hello, [empezar a trabajar con concentradores de eventos](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)</span><span class="sxs-lookup"><span data-stu-id="ca05e-125">Event Hubs namespace provisioned per hello article, [Get started with Event Hubs](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)</span></span>

## <a name="connect-azure-diagnostics-tooevent-hubs-sink"></a><span data-ttu-id="ca05e-126">Conectar el receptor de los centros de tooEvent de diagnósticos de Azure</span><span class="sxs-lookup"><span data-stu-id="ca05e-126">Connect Azure Diagnostics tooEvent Hubs sink</span></span>
<span data-ttu-id="ca05e-127">De forma predeterminada, diagnósticos de Azure siempre envía los registros y las métricas tooan cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="ca05e-127">By default, Azure Diagnostics always sends logs and metrics tooan Azure Storage account.</span></span> <span data-ttu-id="ca05e-128">Una aplicación también puede enviar tooEvent centros de datos agregando un nuevo **receptores** sección hello **PublicConfig** / **WadCfg** elemento de hello *wadcfgx* archivo.</span><span class="sxs-lookup"><span data-stu-id="ca05e-128">An application may also send data tooEvent Hubs by adding a new **Sinks** section under hello **PublicConfig** / **WadCfg** element of hello *.wadcfgx* file.</span></span> <span data-ttu-id="ca05e-129">En Visual Studio, Hola *wadcfgx* archivo se almacena en hello siguiendo la ruta de acceso: **proyecto de servicio de nube** > **Roles** > **() RoleName)** > **diagnostics.wadcfgx** archivo.</span><span class="sxs-lookup"><span data-stu-id="ca05e-129">In Visual Studio, hello *.wadcfgx* file is stored in hello following path: **Cloud Service Project** > **Roles** > **(RoleName)** > **diagnostics.wadcfgx** file.</span></span>

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

<span data-ttu-id="ca05e-130">En este ejemplo, centro de eventos de Hola se establece URL toohello totalmente calificado de espacio de nombres del centro de eventos de hello: espacio de nombres de los centros de eventos + "/" + nombre de concentrador de eventos.</span><span class="sxs-lookup"><span data-stu-id="ca05e-130">In this example, hello event hub URL is set toohello fully qualified namespace of hello event hub: Event Hubs namespace  + "/" + event hub name.</span></span>  

<span data-ttu-id="ca05e-131">Centro de eventos de Hello URL se visualiza en hello [portal de Azure](http://go.microsoft.com/fwlink/?LinkID=213885) en panel de hello centros de eventos.</span><span class="sxs-lookup"><span data-stu-id="ca05e-131">hello event hub URL is displayed in hello [Azure portal](http://go.microsoft.com/fwlink/?LinkID=213885) on hello Event Hubs dashboard.</span></span>  

<span data-ttu-id="ca05e-132">Hola **receptor** puede establecer nombre de cadena válida de tooany como hello mismo valor se usa siempre en el archivo de configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="ca05e-132">hello **Sink** name can be set tooany valid string as long as hello same value is used consistently throughout hello config file.</span></span>

> [!NOTE]
> <span data-ttu-id="ca05e-133">Puede que haya más receptores configurados en esta sección, como *applicationInsights* .</span><span class="sxs-lookup"><span data-stu-id="ca05e-133">There may be additional sinks, such as *applicationInsights* configured in this section.</span></span> <span data-ttu-id="ca05e-134">Diagnósticos de Azure permite uno o varios receptores toobe definida si cada receptor también se declara en hello **PrivateConfig** sección.</span><span class="sxs-lookup"><span data-stu-id="ca05e-134">Azure Diagnostics allows one or more sinks toobe defined if each sink is also declared in hello **PrivateConfig** section.</span></span>  
>
>

<span data-ttu-id="ca05e-135">Hello receptores de los centros de eventos deben también se declaran y se definen en hello **PrivateConfig** sección de hello *wadcfgx* el archivo de configuración.</span><span class="sxs-lookup"><span data-stu-id="ca05e-135">hello Event Hubs sink must also be declared and defined in hello **PrivateConfig** section of hello *.wadcfgx* config file.</span></span>

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

<span data-ttu-id="ca05e-136">Hola `SharedAccessKeyName` valor debe coincidir con una clave de firma de acceso compartido (SAS) y la directiva que se ha definido en hello **centros de eventos** espacio de nombres.</span><span class="sxs-lookup"><span data-stu-id="ca05e-136">hello `SharedAccessKeyName` value must match a Shared Access Signature (SAS) key and policy that has been defined in hello **Event Hubs** namespace.</span></span> <span data-ttu-id="ca05e-137">Examinar el panel de centros de eventos de toohello en hello [portal de Azure](https://manage.windowsazure.com), haga clic en hello **configurar** y a configurar una directiva con nombre (por ejemplo, "SendRule") que tiene *enviar* permisos.</span><span class="sxs-lookup"><span data-stu-id="ca05e-137">Browse toohello Event Hubs dashboard in hello [Azure portal](https://manage.windowsazure.com), click hello **Configure** tab, and set up a named policy (for example, "SendRule") that has *Send* permissions.</span></span> <span data-ttu-id="ca05e-138">Hola **StorageAccount** también se declara en **PrivateConfig**.</span><span class="sxs-lookup"><span data-stu-id="ca05e-138">hello **StorageAccount** is also declared in **PrivateConfig**.</span></span> <span data-ttu-id="ca05e-139">No hay valores toochange aquí si están funcionando.</span><span class="sxs-lookup"><span data-stu-id="ca05e-139">There is no need toochange values here if they are working.</span></span> <span data-ttu-id="ca05e-140">En este ejemplo, se deje Hola valores vacíos, que es un inicio de sesión que un recurso de nivel inferior establecerá los valores de hello.</span><span class="sxs-lookup"><span data-stu-id="ca05e-140">In this example, we leave hello values empty, which is a sign that a downstream asset will set hello values.</span></span> <span data-ttu-id="ca05e-141">Por ejemplo, hello *ServiceConfiguration.Cloud.cscfg* archivo de configuración de entorno establece los nombres de entorno que le corresponda hello y las claves.</span><span class="sxs-lookup"><span data-stu-id="ca05e-141">For example, hello *ServiceConfiguration.Cloud.cscfg* environment configuration file sets hello environment-appropriate names and keys.</span></span>  

> [!WARNING]
> <span data-ttu-id="ca05e-142">clave de SAS de concentradores de eventos de Hola se almacena en texto sin formato en hello *wadcfgx* archivo.</span><span class="sxs-lookup"><span data-stu-id="ca05e-142">hello Event Hubs SAS key is stored in plain text in hello *.wadcfgx* file.</span></span> <span data-ttu-id="ca05e-143">A menudo, esta clave se comprueba en el control de código de toosource o está disponible como un recurso en el servidor de compilación, por lo que debería proteger según corresponda.</span><span class="sxs-lookup"><span data-stu-id="ca05e-143">Often, this key is checked in toosource code control or is available as an asset in your build server, so you should protect it as appropriate.</span></span> <span data-ttu-id="ca05e-144">Se recomienda usar una clave de SAS con *solo enviar* permisos para que un usuario malintencionado puede escribir toohello concentrador de eventos, pero no escuchar tooit o administrarlo.</span><span class="sxs-lookup"><span data-stu-id="ca05e-144">We recommend that you use a SAS key here with *Send only* permissions so that a malicious user can write toohello event hub, but not listen tooit or manage it.</span></span>
>
>

## <a name="configure-azure-diagnostics-toosend-logs-and-metrics-tooevent-hubs"></a><span data-ttu-id="ca05e-145">Configurar diagnósticos de Azure toosend registros y métricas tooEvent centros</span><span class="sxs-lookup"><span data-stu-id="ca05e-145">Configure Azure Diagnostics toosend logs and metrics tooEvent Hubs</span></span>
<span data-ttu-id="ca05e-146">Según lo descrito anteriormente, todos los datos de diagnóstico personalizado y predeterminado, es decir, las métricas y los registros, se envía automáticamente tooAzure almacenamiento en intervalos de hello configurado.</span><span class="sxs-lookup"><span data-stu-id="ca05e-146">As discussed previously, all default and custom diagnostics data, that is, metrics and logs, is automatically sent tooAzure Storage in hello configured intervals.</span></span> <span data-ttu-id="ca05e-147">Con los concentradores de eventos y cualquier receptor adicional, puede especificar cualquier nodo raíz u hoja en hello jerarquía toobe enviado toohello concentrador de eventos.</span><span class="sxs-lookup"><span data-stu-id="ca05e-147">With Event Hubs and any additional sink, you can specify any root or leaf node in hello hierarchy toobe sent toohello event hub.</span></span> <span data-ttu-id="ca05e-148">Esto incluye eventos ETW, contadores de rendimiento, registros de eventos de Windows y registros de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="ca05e-148">This includes ETW events, performance counters, Windows event logs, and application logs.</span></span>   

<span data-ttu-id="ca05e-149">Es importante tooconsider cuántos puntos de datos se deben transferir tooEvent concentradores.</span><span class="sxs-lookup"><span data-stu-id="ca05e-149">It is important tooconsider how many data points should actually be transferred tooEvent Hubs.</span></span> <span data-ttu-id="ca05e-150">Normalmente, los desarrolladores transfieren datos de ruta de acceso activa y de baja latencia que deben consumirse e interpretarse rápidamente.</span><span class="sxs-lookup"><span data-stu-id="ca05e-150">Typically, developers transfer low-latency hot-path data that must be consumed and interpreted quickly.</span></span> <span data-ttu-id="ca05e-151">Los sistemas que supervisan las alertas o las reglas de escalado automático son algunos ejemplos.</span><span class="sxs-lookup"><span data-stu-id="ca05e-151">Systems that monitor alerts or autoscale rules are examples.</span></span> <span data-ttu-id="ca05e-152">Un desarrollador también puede configurar un almacén de búsqueda o un almacén de análisis alternativo (por ejemplo, Análisis de transmisiones de Azure, Elasticsearch, un sistema de supervisión personalizado o un sistema de supervisión favorito de terceros).</span><span class="sxs-lookup"><span data-stu-id="ca05e-152">A developer might also configure an alternate analysis store or search store -- for example, Azure Stream Analytics, Elasticsearch, a custom monitoring system, or a favorite monitoring system from others.</span></span>

<span data-ttu-id="ca05e-153">los siguientes Hola son algunas configuraciones de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="ca05e-153">hello following are some example configurations.</span></span>

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

<span data-ttu-id="ca05e-154">Hola ejemplo anterior, receptor de hello es toohello aplicado primario **PerformanceCounters** nodo en la jerarquía de hello, lo que significa que todos los secundarios **PerformanceCounters** enviará tooEvent concentradores.</span><span class="sxs-lookup"><span data-stu-id="ca05e-154">In hello above example, hello sink is applied toohello parent **PerformanceCounters** node in hello hierarchy, which means all child **PerformanceCounters** will be sent tooEvent Hubs.</span></span>  

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

<span data-ttu-id="ca05e-155">En el ejemplo anterior de hello, el receptor de hello es tooonly aplicado tres contadores: **solicitudes en cola**, **rechazar las solicitudes de**, y **% de tiempo de procesador**.</span><span class="sxs-lookup"><span data-stu-id="ca05e-155">In hello previous example, hello sink is applied tooonly three counters: **Requests Queued**, **Requests Rejected**, and **% Processor time**.</span></span>  

<span data-ttu-id="ca05e-156">Hello en el ejemplo siguiente se muestra cómo un programador puede limitar la cantidad de Hola de datos enviados toobe Hola métricas críticas que se usan para el estado de este servicio.</span><span class="sxs-lookup"><span data-stu-id="ca05e-156">hello following example shows how a developer can limit hello amount of sent data toobe hello critical metrics that are used for this service’s health.</span></span>  

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

<span data-ttu-id="ca05e-157">En este ejemplo, receptores de hello es toologs aplicados y es filtrado seguimiento de nivel de tooerror solo.</span><span class="sxs-lookup"><span data-stu-id="ca05e-157">In this example, hello sink is applied toologs and is filtered only tooerror level trace.</span></span>

## <a name="deploy-and-update-a-cloud-services-application-and-diagnostics-config"></a><span data-ttu-id="ca05e-158">Implementación y actualización de una aplicación de servicios en la nube y configuración de diagnósticos</span><span class="sxs-lookup"><span data-stu-id="ca05e-158">Deploy and update a Cloud Services application and diagnostics config</span></span>
<span data-ttu-id="ca05e-159">Visual Studio proporciona la aplicación de Hola de ruta de acceso más fácil de hello toodeploy y configuración del receptor de los centros de eventos.</span><span class="sxs-lookup"><span data-stu-id="ca05e-159">Visual Studio provides hello easiest path toodeploy hello application and Event Hubs sink configuration.</span></span> <span data-ttu-id="ca05e-160">tooview y editar archivo hello, abra hello *wadcfgx* un archivo en Visual Studio, editarlo y guardarlo.</span><span class="sxs-lookup"><span data-stu-id="ca05e-160">tooview and edit hello file, open hello *.wadcfgx* file in Visual Studio, edit it, and save it.</span></span> <span data-ttu-id="ca05e-161">ruta de acceso de Hello es **proyecto de servicio de nube** > **Roles** > **(RoleName)** > **diagnostics.wadcfgx**.</span><span class="sxs-lookup"><span data-stu-id="ca05e-161">hello path is **Cloud Service Project** > **Roles** > **(RoleName)** > **diagnostics.wadcfgx**.</span></span>  

<span data-ttu-id="ca05e-162">En este momento, todos los e implementación actualizan acciones en Visual Studio, Visual Studio Team System y todos los comandos o scripts que se basan en MSBuild y usar hello **/t: publicar** destino incluyen hello *wadcfgx*  en proceso de empaquetado de Hola.</span><span class="sxs-lookup"><span data-stu-id="ca05e-162">At this point, all deployment and deployment update actions in Visual Studio, Visual Studio Team System, and all commands or scripts that are based on MSBuild and use hello **/t:publish** target include hello *.wadcfgx* in hello packaging process.</span></span> <span data-ttu-id="ca05e-163">Además, implementaciones y actualizaciones implementación hello tooAzure de archivo con extensión del agente de diagnósticos de Azure adecuada de hello en las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="ca05e-163">In addition, deployments and updates deploy hello file tooAzure by using hello appropriate Azure Diagnostics agent extension on your VMs.</span></span>

<span data-ttu-id="ca05e-164">Después de implementar la aplicación hello y la configuración de diagnósticos de Azure, verá inmediatamente actividad en el panel de Hola de concentrador de eventos de Hola.</span><span class="sxs-lookup"><span data-stu-id="ca05e-164">After you deploy hello application and Azure Diagnostics configuration, you will immediately see activity in hello dashboard of hello event hub.</span></span> <span data-ttu-id="ca05e-165">Esto indica que está listo toomove en los datos de ruta de acceso activa tooviewing hello en herramienta de cliente o los análisis de agente de escucha de Hola de su elección.</span><span class="sxs-lookup"><span data-stu-id="ca05e-165">This indicates that you're ready toomove on tooviewing hello hot-path data in hello listener client or analysis tool of your choice.</span></span>  

<span data-ttu-id="ca05e-166">Hola figura siguiente, panel de centros de eventos de hello muestra envío correcto de inicio de diagnóstico datos toohello evento concentrador algún tiempo después de 23: 00.</span><span class="sxs-lookup"><span data-stu-id="ca05e-166">In hello following figure, hello Event Hubs dashboard shows healthy sending of diagnostics data toohello event hub starting sometime after 11 PM.</span></span> <span data-ttu-id="ca05e-167">Es decir, cuando se implementó la aplicación hello con un controlador actualizado, *wadcfgx* de archivos y Hola receptor se configuró correctamente.</span><span class="sxs-lookup"><span data-stu-id="ca05e-167">That's when hello application was deployed with an updated *.wadcfgx* file, and hello sink was configured properly.</span></span>

![][0]  

> [!NOTE]
> <span data-ttu-id="ca05e-168">Al realizar el archivo de configuración de diagnósticos de Azure actualizaciones toohello (.wadcfgx), se recomienda que realice una inserción Hola actualizaciones toohello toda aplicación, así como la configuración de hello mediante la publicación de Visual Studio o un script de Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ca05e-168">When you make updates toohello Azure Diagnostics config file (.wadcfgx), it's recommended that you push hello updates toohello entire application as well as hello configuration by using either Visual Studio publishing, or a Windows PowerShell script.</span></span>  
>
>

## <a name="view-hot-path-data"></a><span data-ttu-id="ca05e-169">Ver los datos de la ruta de acceso activa</span><span class="sxs-lookup"><span data-stu-id="ca05e-169">View hot-path data</span></span>
<span data-ttu-id="ca05e-170">Según lo descrito anteriormente, hay muchos casos de uso de escucha tooand procesamiento de datos de los centros de eventos.</span><span class="sxs-lookup"><span data-stu-id="ca05e-170">As discussed previously, there are many use cases for listening tooand processing Event Hubs data.</span></span>

<span data-ttu-id="ca05e-171">Una estrategia sencilla consiste toocreate un concentrador de eventos de prueba pequeñas consola aplicación toolisten toohello y flujo de salida de impresión Hola.</span><span class="sxs-lookup"><span data-stu-id="ca05e-171">One simple approach is toocreate a small test console application toolisten toohello event hub and print hello output stream.</span></span> <span data-ttu-id="ca05e-172">Puede colocar Hola siguiente código, que se explica con más detalle en [empezar a trabajar con concentradores de eventos](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)), en una aplicación de consola.</span><span class="sxs-lookup"><span data-stu-id="ca05e-172">You can place hello following code, which is explained in more detail in [Get started with Event Hubs](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)), in a console application.</span></span>  

<span data-ttu-id="ca05e-173">Tenga en cuenta que la aplicación de consola de hello debe incluir hello [paquete NuGet de Host de procesador de eventos](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/).</span><span class="sxs-lookup"><span data-stu-id="ca05e-173">Note that hello console application must include hello [Event Processor Host NuGet package](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/).</span></span>  

<span data-ttu-id="ca05e-174">Recuerde que los valores de hello tooreplace corchetes angulares en hello **Main** función con valores de los recursos.</span><span class="sxs-lookup"><span data-stu-id="ca05e-174">Remember tooreplace hello values in angle brackets in hello **Main** function with values for your resources.</span></span>   

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

            Console.WriteLine("Receiving. Press enter key toostop worker.");
            Console.ReadLine();
            eventProcessorHost.UnregisterEventProcessorAsync().Wait();
        }
    }
}
```

## <a name="troubleshoot-event-hubs-sinks"></a><span data-ttu-id="ca05e-175">Solución de problemas con los receptores de Event Hubs</span><span class="sxs-lookup"><span data-stu-id="ca05e-175">Troubleshoot Event Hubs sinks</span></span>
* <span data-ttu-id="ca05e-176">Centro de eventos de Hello no muestra la actividad de evento entrante o saliente según lo previsto.</span><span class="sxs-lookup"><span data-stu-id="ca05e-176">hello event hub does not show incoming or outgoing event activity as expected.</span></span>

    <span data-ttu-id="ca05e-177">Compruebe que el centro de eventos esté correctamente aprovisionado.</span><span class="sxs-lookup"><span data-stu-id="ca05e-177">Check that your event hub is successfully provisioned.</span></span> <span data-ttu-id="ca05e-178">Toda la información de conexión en hello **PrivateConfig** sección de *wadcfgx* deben coincidir con los valores de hello de su recurso tal como se muestra en el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="ca05e-178">All connection info in hello **PrivateConfig** section of *.wadcfgx* must match hello values of your resource as seen in hello portal.</span></span> <span data-ttu-id="ca05e-179">Asegúrese de que tiene una directiva SAS definida ("SendRule" en el ejemplo de Hola) en el portal de Hola y que *enviar* se concede el permiso.</span><span class="sxs-lookup"><span data-stu-id="ca05e-179">Make sure that you have a SAS policy defined ("SendRule" in hello example) in hello portal and that *Send* permission is granted.</span></span>  
* <span data-ttu-id="ca05e-180">Después de una actualización, centro de eventos de hello ya no muestra la actividad de evento entrante o saliente.</span><span class="sxs-lookup"><span data-stu-id="ca05e-180">After an update, hello event hub no longer shows incoming or outgoing event activity.</span></span>

    <span data-ttu-id="ca05e-181">En primer lugar, asegúrese de que ese concentrador de eventos de Hola y obtener información de configuración es correcta como se explicó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="ca05e-181">First, make sure that hello event hub and configuration info is correct as explained previously.</span></span> <span data-ttu-id="ca05e-182">A veces Hola **PrivateConfig** se restablece en una actualización de la implementación.</span><span class="sxs-lookup"><span data-stu-id="ca05e-182">Sometimes hello **PrivateConfig** is reset in a deployment update.</span></span> <span data-ttu-id="ca05e-183">Hola recomendado corrección es toomake cambios demasiado*wadcfgx* en Hola proyecto y, a continuación, insertar una actualización de la aplicación completa.</span><span class="sxs-lookup"><span data-stu-id="ca05e-183">hello recommended fix is toomake all changes too*.wadcfgx* in hello project and then push a complete application update.</span></span> <span data-ttu-id="ca05e-184">Si esto no es posible, asegúrese de que esa actualización de diagnósticos de hello inserta una completa **PrivateConfig** que incluye la clave SAS Hola.</span><span class="sxs-lookup"><span data-stu-id="ca05e-184">If this is not possible, make sure that hello diagnostics update pushes a complete **PrivateConfig** that includes hello SAS key.</span></span>  
* <span data-ttu-id="ca05e-185">Se ha intentado sugerencias de Hola y centro de eventos de hello sigue sin funcionar.</span><span class="sxs-lookup"><span data-stu-id="ca05e-185">I tried hello suggestions, and hello event hub is still not working.</span></span>

    <span data-ttu-id="ca05e-186">Pruebe a buscar en tabla de almacenamiento de Azure de Hola que contiene errores y los registros de diagnósticos de Azure propia: **WADDiagnosticInfrastructureLogsTable**.</span><span class="sxs-lookup"><span data-stu-id="ca05e-186">Try looking in hello Azure Storage table that contains logs and errors for Azure Diagnostics itself: **WADDiagnosticInfrastructureLogsTable**.</span></span> <span data-ttu-id="ca05e-187">Una opción es toouse una herramienta como [Azure Storage Explorer](http://www.storageexplorer.com) cuenta de almacenamiento de tooconnect toothis, ver esta tabla y agregar una consulta de marca de tiempo en hello las últimas 24 horas.</span><span class="sxs-lookup"><span data-stu-id="ca05e-187">One option is toouse a tool such as [Azure Storage Explorer](http://www.storageexplorer.com) tooconnect toothis storage account, view this table, and add a query for TimeStamp in hello last 24 hours.</span></span> <span data-ttu-id="ca05e-188">Puede usar la herramienta de hello tooexport un archivo .csv y ábralo en una aplicación como Microsoft Excel.</span><span class="sxs-lookup"><span data-stu-id="ca05e-188">You can use hello tool tooexport a .csv file and open it in an application such as Microsoft Excel.</span></span> <span data-ttu-id="ca05e-189">Excel resulta fácil toosearch para las cadenas de tarjeta de llamada, como **EventHubs**, toosee se notifica el error.</span><span class="sxs-lookup"><span data-stu-id="ca05e-189">Excel makes it easy toosearch for calling-card strings, such as **EventHubs**, toosee what error is reported.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="ca05e-190">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ca05e-190">Next steps</span></span>
<span data-ttu-id="ca05e-191">•    [Más información sobre Event Hubs](https://azure.microsoft.com/services/event-hubs/)</span><span class="sxs-lookup"><span data-stu-id="ca05e-191">•    [Learn more about Event Hubs](https://azure.microsoft.com/services/event-hubs/)</span></span>

## <a name="appendix-complete-azure-diagnostics-configuration-file-wadcfgx-example"></a><span data-ttu-id="ca05e-192">Apéndice: Archivo de configuración completo de Diagnósticos de Azure (.wadcfgx): ejemplo</span><span class="sxs-lookup"><span data-stu-id="ca05e-192">Appendix: Complete Azure Diagnostics configuration file (.wadcfgx) example</span></span>
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

<span data-ttu-id="ca05e-193">Hola complementario *ServiceConfiguration.Cloud.cscfg* para este ejemplo es similar a Hola siguiente.</span><span class="sxs-lookup"><span data-stu-id="ca05e-193">hello complementary *ServiceConfiguration.Cloud.cscfg* for this example looks like hello following.</span></span>

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

<span data-ttu-id="ca05e-194">La configuración JSON equivalente para máquinas virtuales es la siguiente:</span><span class="sxs-lookup"><span data-stu-id="ca05e-194">Equivalent Json based settings for virtual machines is as follows:</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="ca05e-195">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ca05e-195">Next steps</span></span>
<span data-ttu-id="ca05e-196">Para obtener más información acerca de los centros de eventos información visitando Hola siguientes vínculos:</span><span class="sxs-lookup"><span data-stu-id="ca05e-196">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="ca05e-197">Información general de Event Hubs</span><span class="sxs-lookup"><span data-stu-id="ca05e-197">Event Hubs overview</span></span>](../event-hubs/event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="ca05e-198">Creación de un centro de eventos</span><span class="sxs-lookup"><span data-stu-id="ca05e-198">Create an event hub</span></span>](../event-hubs/event-hubs-create.md)
* [<span data-ttu-id="ca05e-199">Preguntas más frecuentes sobre Event Hubs</span><span class="sxs-lookup"><span data-stu-id="ca05e-199">Event Hubs FAQ</span></span>](../event-hubs/event-hubs-faq.md)

<!-- Images. -->
[0]: ../event-hubs/media/event-hubs-streaming-azure-diags-data/dashboard.png
