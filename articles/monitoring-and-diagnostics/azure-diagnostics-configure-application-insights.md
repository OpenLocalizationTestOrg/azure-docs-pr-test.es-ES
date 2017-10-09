---
title: "aaaConfigure diagnósticos de Azure toosend datos tooApplication visión | Documentos de Microsoft"
description: "Actualizar Hola diagnósticos de Azure configuración pública toosend datos tooApplication visión."
services: monitoring-and-diagnostics
documentationcenter: .net
author: rboucher
manager: carmonm
editor: 
ms.assetid: f9e12c3e-c307-435e-a149-ef0fef20513a
ms.service: monitoring-and-diagnostics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/19/2016
ms.author: robb
ms.openlocfilehash: 7c36f29da8fdc12fa58c17458348a311b900b0f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="send-cloud-service-virtual-machine-or-service-fabric-diagnostic-data-tooapplication-insights"></a><span data-ttu-id="ea626-103">Enviar datos de diagnóstico del servicio en la nube, Máquina Virtual o Service Fabric tooApplication visión</span><span class="sxs-lookup"><span data-stu-id="ea626-103">Send Cloud Service, Virtual Machine, or Service Fabric diagnostic data tooApplication Insights</span></span>
<span data-ttu-id="ea626-104">Servicios en la nube, máquinas virtuales, los conjuntos de escalas de máquina Virtual y los Service Fabric usan datos de toocollect de extensión de diagnósticos de Azure de saludo.</span><span class="sxs-lookup"><span data-stu-id="ea626-104">Cloud services, Virtual Machines, Virtual Machine Scale Sets and Service Fabric all use hello Azure Diagnostics extension toocollect data.</span></span>  <span data-ttu-id="ea626-105">Diagnósticos de Azure envía datos tooAzure tablas de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="ea626-105">Azure diagnostics sends data tooAzure Storage tables.</span></span>  <span data-ttu-id="ea626-106">Sin embargo, también puede canalización todos o un subconjunto de hello datos tooother ubicaciones mediante la extensión de diagnósticos de Azure 1.5 o posterior.</span><span class="sxs-lookup"><span data-stu-id="ea626-106">However, you can also pipe all or a subset of hello data tooother locations using Azure Diagnostics extension 1.5 or later.</span></span>

<span data-ttu-id="ea626-107">Este artículo describe cómo toosend datos de Hola tooApplication de extensión de diagnósticos de Azure Insights.</span><span class="sxs-lookup"><span data-stu-id="ea626-107">This article describes how toosend data from hello Azure Diagnostics extension tooApplication Insights.</span></span>

## <a name="diagnostics-configuration-explained"></a><span data-ttu-id="ea626-108">Explicación de la configuración de Diagnostics</span><span class="sxs-lookup"><span data-stu-id="ea626-108">Diagnostics configuration explained</span></span>
<span data-ttu-id="ea626-109">Hola receptores de extensión 1.5 introducida los diagnósticos de Azure, que son más ubicaciones donde puede enviar datos de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="ea626-109">hello Azure diagnostics extension 1.5 introduced sinks, which are additional locations where you can send diagnostic data.</span></span>

<span data-ttu-id="ea626-110">Ejemplo de configuración de un receptor para Application Insights:</span><span class="sxs-lookup"><span data-stu-id="ea626-110">Example configuration of a sink for Application Insights:</span></span>

```XML
<SinksConfig>
    <Sink name="ApplicationInsights">
      <ApplicationInsights>{Insert InstrumentationKey}</ApplicationInsights>
      <Channels>
        <Channel logLevel="Error" name="MyTopDiagData"  />
        <Channel logLevel="Verbose" name="MyLogData"  />
      </Channels>
    </Sink>
</SinksConfig>
```
```JSON
"SinksConfig": {
    "Sink": [
        {
            "name": "ApplicationInsights",
            "ApplicationInsights": "{Insert InstrumentationKey}",
            "Channels": {
                "Channel": [
                    {
                        "logLevel": "Error",
                        "name": "MyTopDiagData"
                    },
                    {
                        "logLevel": "Error",
                        "name": "MyLogData"
                    }
                ]
            }
        }
    ]
}
```
- <span data-ttu-id="ea626-111">Hola **receptor** *nombre* atributo es un valor de cadena que identifica de forma única el receptor de Hola.</span><span class="sxs-lookup"><span data-stu-id="ea626-111">hello **Sink** *name* attribute is a string value that uniquely identifies hello sink.</span></span>

- <span data-ttu-id="ea626-112">Hola **ApplicationInsights** elemento especifica la clave de instrumentación de recursos de información de aplicación dónde se envía los datos de diagnóstico de Azure de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="ea626-112">hello **ApplicationInsights** element specifies instrumentation key of hello Application insights resource where hello Azure diagnostics data is sent.</span></span>
    - <span data-ttu-id="ea626-113">Si no tiene un recurso de Application Insights existente, consulte [crear un nuevo recurso de Application Insights](../application-insights/app-insights-create-new-resource.md) para obtener más información sobre cómo crear un recurso y cómo obtener clave de instrumentación de Hola.</span><span class="sxs-lookup"><span data-stu-id="ea626-113">If you don't have an existing Application Insights resource, see [Create a new Application Insights resource](../application-insights/app-insights-create-new-resource.md) for more information on creating a resource and getting hello instrumentation key.</span></span>
    - <span data-ttu-id="ea626-114">Si está desarrollando un servicio en la nube con Azure SDK 2.8 y versiones posteriores, se rellena automáticamente esta clave de instrumentación.</span><span class="sxs-lookup"><span data-stu-id="ea626-114">If you are developing a Cloud Service with Azure SDK 2.8 and later, this instrumentation key is automatically populated.</span></span> <span data-ttu-id="ea626-115">valor de Hola se basa en hello **APPINSIGHTS_INSTRUMENTATIONKEY** de configuración de servicio al empaquetar el proyecto de servicio de nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="ea626-115">hello value is based on hello **APPINSIGHTS_INSTRUMENTATIONKEY** service configuration setting when packaging hello Cloud Service project.</span></span> <span data-ttu-id="ea626-116">Vea [problemas de servicio en la nube Use Application Insights con diagnósticos de Azure tootroubleshoot](../cloud-services/cloud-services-dotnet-diagnostics-applicationinsights.md).</span><span class="sxs-lookup"><span data-stu-id="ea626-116">See [Use Application Insights with Azure Diagnostics tootroubleshoot Cloud Service issues](../cloud-services/cloud-services-dotnet-diagnostics-applicationinsights.md).</span></span>

- <span data-ttu-id="ea626-117">Hola **canales** elemento contiene uno o varios **canal** elementos.</span><span class="sxs-lookup"><span data-stu-id="ea626-117">hello **Channels** element contains one or more **Channel** elements.</span></span>
    - <span data-ttu-id="ea626-118">Hola *nombre* atributo inequívocamente hace referencia toothat canal.</span><span class="sxs-lookup"><span data-stu-id="ea626-118">hello *name* attribute uniquely refers toothat channel.</span></span>
    - <span data-ttu-id="ea626-119">Hola *loglevel* permite especificar el nivel de registro de hello que Hola canal permite el atributo.</span><span class="sxs-lookup"><span data-stu-id="ea626-119">hello *loglevel* attribute lets you specify hello log level that hello channel allows.</span></span> <span data-ttu-id="ea626-120">Hola niveles de registro disponibles en orden de mayor cantidad de información de tooleast son:</span><span class="sxs-lookup"><span data-stu-id="ea626-120">hello available log levels in order of most tooleast information are:</span></span>
        - <span data-ttu-id="ea626-121">Detallado</span><span class="sxs-lookup"><span data-stu-id="ea626-121">Verbose</span></span>
        - <span data-ttu-id="ea626-122">Información</span><span class="sxs-lookup"><span data-stu-id="ea626-122">Information</span></span>
        - <span data-ttu-id="ea626-123">Warning (Advertencia)</span><span class="sxs-lookup"><span data-stu-id="ea626-123">Warning</span></span>
        - <span data-ttu-id="ea626-124">Error</span><span class="sxs-lookup"><span data-stu-id="ea626-124">Error</span></span>
        - <span data-ttu-id="ea626-125">Crítico</span><span class="sxs-lookup"><span data-stu-id="ea626-125">Critical</span></span>

<span data-ttu-id="ea626-126">Un canal actúa como un filtro y permite tooselect registro específico niveles toosend toohello destino receptor.</span><span class="sxs-lookup"><span data-stu-id="ea626-126">A channel acts like a filter and allows you tooselect specific log levels toosend toohello target sink.</span></span> <span data-ttu-id="ea626-127">Por ejemplo, puede recopilar registros detallados y enviarlos toostorage, pero solo receptor toohello de errores de envío.</span><span class="sxs-lookup"><span data-stu-id="ea626-127">For example, you could collect verbose logs and send them toostorage, but send only Errors toohello sink.</span></span>

<span data-ttu-id="ea626-128">Hello gráfico siguiente muestra esta relación.</span><span class="sxs-lookup"><span data-stu-id="ea626-128">hello following graphic shows this relationship.</span></span>

![Configuración pública de diagnósticos](./media/azure-diagnostics-configure-applicationinsights/AzDiag_Channels_App_Insights.png)

<span data-ttu-id="ea626-130">Hola siguiente gráfico resume los valores de configuración de Hola y cómo funcionan.</span><span class="sxs-lookup"><span data-stu-id="ea626-130">hello following graphic summarizes hello configuration values and how they work.</span></span> <span data-ttu-id="ea626-131">Puede incluir varios receptores en la configuración de hello en distintos niveles de jerarquía de Hola.</span><span class="sxs-lookup"><span data-stu-id="ea626-131">You can include multiple sinks in hello configuration at different levels in hello hierarchy.</span></span> <span data-ttu-id="ea626-132">receptor de Hello en el nivel superior de hello actúa como una configuración global y hello especifica uno en hello individual elemento actúa como una configuración global de toothat de invalidación.</span><span class="sxs-lookup"><span data-stu-id="ea626-132">hello sink at hello top level acts as a global setting and hello one specified at hello individual element acts like an override toothat global setting.</span></span>

![Receptores de diagnósticos: configuración con Application Insights](./media/azure-diagnostics-configure-applicationinsights/Azure_Diagnostics_Sinks.png)

## <a name="complete-sink-configuration-example"></a><span data-ttu-id="ea626-134">Ejemplo completo de configuración de receptor</span><span class="sxs-lookup"><span data-stu-id="ea626-134">Complete sink configuration example</span></span>
<span data-ttu-id="ea626-135">Este es un ejemplo completo de la configuración pública de Hola de archivos que</span><span class="sxs-lookup"><span data-stu-id="ea626-135">Here is a complete example of hello public configuration file that</span></span>
1. <span data-ttu-id="ea626-136">envía todos los errores tooApplication visión (especificado en hello **DiagnosticMonitorConfiguration** nodo)</span><span class="sxs-lookup"><span data-stu-id="ea626-136">sends all errors tooApplication Insights (specified at hello **DiagnosticMonitorConfiguration** node)</span></span>
2. <span data-ttu-id="ea626-137">Además, envía los registros de nivel detallados para registros de la aplicación hello (especificado en hello **registros** nodo).</span><span class="sxs-lookup"><span data-stu-id="ea626-137">also sends Verbose level logs for hello Application Logs (specified at hello **Logs** node).</span></span>

```XML
<WadCfg>
  <DiagnosticMonitorConfiguration overallQuotaInMB="4096"
       sinks="ApplicationInsights.MyTopDiagData"> <!-- All info below sent toothis channel -->
    <DiagnosticInfrastructureLogs />
    <PerformanceCounters>
      <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT3M" />
      <PerformanceCounterConfiguration counterSpecifier="\Memory\Available MBytes" sampleRate="PT3M" />
    </PerformanceCounters>
    <WindowsEventLog scheduledTransferPeriod="PT1M">
      <DataSource name="Application!*" />
    </WindowsEventLog>
    <Logs scheduledTransferPeriod="PT1M" scheduledTransferLogLevelFilter="Verbose"
            sinks="ApplicationInsights.MyLogData"/> <!-- This specific info sent toothis channel -->
  </DiagnosticMonitorConfiguration>

<SinksConfig>
    <Sink name="ApplicationInsights">
      <ApplicationInsights>{Insert InstrumentationKey}</ApplicationInsights>
      <Channels>
        <Channel logLevel="Error" name="MyTopDiagData"  />
        <Channel logLevel="Verbose" name="MyLogData"  />
      </Channels>
    </Sink>
  </SinksConfig>
</WadCfg>
```
```JSON
"WadCfg": {
    "DiagnosticMonitorConfiguration": {
        "overallQuotaInMB": 4096,
        "sinks": "ApplicationInsights.MyTopDiagData", "_comment": "All info below sent toothis channel",
        "DiagnosticInfrastructureLogs": {
        },
        "PerformanceCounters": {
            "PerformanceCounterConfiguration": [
                {
                    "counterSpecifier": "\\Processor(_Total)\\% Processor Time",
                    "sampleRate": "PT3M"
                },
                {
                    "counterSpecifier": "\\Memory\\Available MBytes",
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
            "scheduledTransferLogLevelFilter": "Verbose",
            "sinks": "ApplicationInsights.MyLogData", "_comment": "This specific info sent toothis channel"
        }
    },
    "SinksConfig": {
        "Sink": [
            {
                "name": "ApplicationInsights",
                "ApplicationInsights": "{Insert InstrumentationKey}",
                "Channels": {
                    "Channel": [
                        {
                            "logLevel": "Error",
                            "name": "MyTopDiagData"
                        },
                        {
                            "logLevel": "Verbose",
                            "name": "MyLogData"
                        }
                    ]
                }
            }
        ]
    }
}
```
<span data-ttu-id="ea626-138">En la configuración anterior de hello, Hola después líneas tiene Hola siguientes significados:</span><span class="sxs-lookup"><span data-stu-id="ea626-138">In hello previous configuration, hello following lines have hello following meanings:</span></span>

### <a name="send-all-hello-data-that-is-being-collected-by-azure-diagnostics"></a><span data-ttu-id="ea626-139">Enviar todos los datos de hello recopilados por diagnósticos de Azure</span><span class="sxs-lookup"><span data-stu-id="ea626-139">Send all hello data that is being collected by Azure diagnostics</span></span>

```XML
<DiagnosticMonitorConfiguration overallQuotaInMB="4096" sinks="ApplicationInsights">
```
```JSON
"DiagnosticMonitorConfiguration": {
    "overallQuotaInMB": 4096,
    "sinks": "ApplicationInsights",
}
```

### <a name="send-only-error-logs-toohello-application-insights-sink"></a><span data-ttu-id="ea626-140">Enviar solo registros toohello Application Insights el receptor de errores</span><span class="sxs-lookup"><span data-stu-id="ea626-140">Send only error logs toohello Application Insights sink</span></span>

```XML
<DiagnosticMonitorConfiguration overallQuotaInMB="4096" sinks="ApplicationInsights.MyTopDiagdata">
```
```JSON
"DiagnosticMonitorConfiguration": {
    "overallQuotaInMB": 4096,
    "sinks": "ApplicationInsights.MyTopDiagData",
}
```

### <a name="send-verbose-application-logs-tooapplication-insights"></a><span data-ttu-id="ea626-141">Enviar tooApplication visión de registros de aplicación detallado</span><span class="sxs-lookup"><span data-stu-id="ea626-141">Send Verbose application logs tooApplication Insights</span></span>

```XML
<Logs scheduledTransferPeriod="PT1M" scheduledTransferLogLevelFilter="Verbose" sinks="ApplicationInsights.MyLogData"/>
```
```JSON
"DiagnosticMonitorConfiguration": {
    "overallQuotaInMB": 4096,
    "sinks": "ApplicationInsights.MyLogData",
}
```

## <a name="limitations"></a><span data-ttu-id="ea626-142">Limitaciones</span><span class="sxs-lookup"><span data-stu-id="ea626-142">Limitations</span></span>

- <span data-ttu-id="ea626-143">**Channels solo registra el tipo de registro y no los contadores de rendimiento.**</span><span class="sxs-lookup"><span data-stu-id="ea626-143">**Channels only log type and not performance counters.**</span></span> <span data-ttu-id="ea626-144">Si especifica un canal con un elemento de contador de rendimiento, se pasará por alto.</span><span class="sxs-lookup"><span data-stu-id="ea626-144">If you specify a channel with a performance counter element, it is ignored.</span></span>
- <span data-ttu-id="ea626-145">**nivel de registro de Hello para un canal no puede superar el nivel de registro de hello para lo que se está recopilando por diagnósticos de Azure.**</span><span class="sxs-lookup"><span data-stu-id="ea626-145">**hello log level for a channel cannot exceed hello log level for what is being collected by Azure diagnostics.**</span></span> <span data-ttu-id="ea626-146">Por ejemplo, no se puede recopilar los errores de registro de aplicación en el elemento de registros de Hola e intente toosend registros detallados toohello Application Insight receptor.</span><span class="sxs-lookup"><span data-stu-id="ea626-146">For example, you cannot collect Application Log errors in hello Logs element and try toosend Verbose logs toohello Application Insight sink.</span></span> <span data-ttu-id="ea626-147">Hola *scheduledTransferLogLevelFilter* atributo siempre debe recopilar igual o más registros de Hola la sesión están tratando de toosend tooa receptor.</span><span class="sxs-lookup"><span data-stu-id="ea626-147">hello *scheduledTransferLogLevelFilter* attribute must always collect equal or more logs than hello logs you are trying toosend tooa sink.</span></span>
- <span data-ttu-id="ea626-148">**No se puede enviar datos de blob recopilados por diagnósticos de Azure extensión tooApplication visión.**</span><span class="sxs-lookup"><span data-stu-id="ea626-148">**You cannot send blob data collected by Azure diagnostics extension tooApplication Insights.**</span></span> <span data-ttu-id="ea626-149">Por ejemplo, especificar nada en hello *directorios* nodo.</span><span class="sxs-lookup"><span data-stu-id="ea626-149">For example, anything specified under hello *Directories* node.</span></span> <span data-ttu-id="ea626-150">Para volcados Hola real volcado de memoria se envía tooblob almacenamiento y se genera solo una notificación que Hola volcado de memoria se envían información tooApplication.</span><span class="sxs-lookup"><span data-stu-id="ea626-150">For Crash Dumps hello actual crash dump is sent tooblob storage and only a notification that hello crash dump was generated is sent tooApplication Insights.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ea626-151">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ea626-151">Next Steps</span></span>
* <span data-ttu-id="ea626-152">Obtenga información acerca de cómo demasiado[ver la información de diagnóstico de Azure](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-cloudservices#view-azure-diagnostic-events) en Application Insights.</span><span class="sxs-lookup"><span data-stu-id="ea626-152">Learn how too[view your Azure diagnostics information](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-cloudservices#view-azure-diagnostic-events) in Application Insights.</span></span>
* <span data-ttu-id="ea626-153">Use [PowerShell](../cloud-services/cloud-services-diagnostics-powershell.md) tooenable Hola extensión de diagnósticos de Azure para su aplicación.</span><span class="sxs-lookup"><span data-stu-id="ea626-153">Use [PowerShell](../cloud-services/cloud-services-diagnostics-powershell.md) tooenable hello Azure diagnostics extension for your application.</span></span>
* <span data-ttu-id="ea626-154">Use [Visual Studio](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md) tooenable Hola extensión de diagnósticos de Azure para la aplicación</span><span class="sxs-lookup"><span data-stu-id="ea626-154">Use [Visual Studio](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md) tooenable hello Azure diagnostics extension for your application</span></span>
