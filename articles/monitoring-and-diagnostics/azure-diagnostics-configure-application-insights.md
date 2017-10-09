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
# <a name="send-cloud-service-virtual-machine-or-service-fabric-diagnostic-data-tooapplication-insights"></a>Enviar datos de diagnóstico del servicio en la nube, Máquina Virtual o Service Fabric tooApplication visión
Servicios en la nube, máquinas virtuales, los conjuntos de escalas de máquina Virtual y los Service Fabric usan datos de toocollect de extensión de diagnósticos de Azure de saludo.  Diagnósticos de Azure envía datos tooAzure tablas de almacenamiento.  Sin embargo, también puede canalización todos o un subconjunto de hello datos tooother ubicaciones mediante la extensión de diagnósticos de Azure 1.5 o posterior.

Este artículo describe cómo toosend datos de Hola tooApplication de extensión de diagnósticos de Azure Insights.

## <a name="diagnostics-configuration-explained"></a>Explicación de la configuración de Diagnostics
Hola receptores de extensión 1.5 introducida los diagnósticos de Azure, que son más ubicaciones donde puede enviar datos de diagnóstico.

Ejemplo de configuración de un receptor para Application Insights:

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
- Hola **receptor** *nombre* atributo es un valor de cadena que identifica de forma única el receptor de Hola.

- Hola **ApplicationInsights** elemento especifica la clave de instrumentación de recursos de información de aplicación dónde se envía los datos de diagnóstico de Azure de Hola Hola.
    - Si no tiene un recurso de Application Insights existente, consulte [crear un nuevo recurso de Application Insights](../application-insights/app-insights-create-new-resource.md) para obtener más información sobre cómo crear un recurso y cómo obtener clave de instrumentación de Hola.
    - Si está desarrollando un servicio en la nube con Azure SDK 2.8 y versiones posteriores, se rellena automáticamente esta clave de instrumentación. valor de Hola se basa en hello **APPINSIGHTS_INSTRUMENTATIONKEY** de configuración de servicio al empaquetar el proyecto de servicio de nube de Hola. Vea [problemas de servicio en la nube Use Application Insights con diagnósticos de Azure tootroubleshoot](../cloud-services/cloud-services-dotnet-diagnostics-applicationinsights.md).

- Hola **canales** elemento contiene uno o varios **canal** elementos.
    - Hola *nombre* atributo inequívocamente hace referencia toothat canal.
    - Hola *loglevel* permite especificar el nivel de registro de hello que Hola canal permite el atributo. Hola niveles de registro disponibles en orden de mayor cantidad de información de tooleast son:
        - Detallado
        - Información
        - Warning (Advertencia)
        - Error
        - Crítico

Un canal actúa como un filtro y permite tooselect registro específico niveles toosend toohello destino receptor. Por ejemplo, puede recopilar registros detallados y enviarlos toostorage, pero solo receptor toohello de errores de envío.

Hello gráfico siguiente muestra esta relación.

![Configuración pública de diagnósticos](./media/azure-diagnostics-configure-applicationinsights/AzDiag_Channels_App_Insights.png)

Hola siguiente gráfico resume los valores de configuración de Hola y cómo funcionan. Puede incluir varios receptores en la configuración de hello en distintos niveles de jerarquía de Hola. receptor de Hello en el nivel superior de hello actúa como una configuración global y hello especifica uno en hello individual elemento actúa como una configuración global de toothat de invalidación.

![Receptores de diagnósticos: configuración con Application Insights](./media/azure-diagnostics-configure-applicationinsights/Azure_Diagnostics_Sinks.png)

## <a name="complete-sink-configuration-example"></a>Ejemplo completo de configuración de receptor
Este es un ejemplo completo de la configuración pública de Hola de archivos que
1. envía todos los errores tooApplication visión (especificado en hello **DiagnosticMonitorConfiguration** nodo)
2. Además, envía los registros de nivel detallados para registros de la aplicación hello (especificado en hello **registros** nodo).

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
En la configuración anterior de hello, Hola después líneas tiene Hola siguientes significados:

### <a name="send-all-hello-data-that-is-being-collected-by-azure-diagnostics"></a>Enviar todos los datos de hello recopilados por diagnósticos de Azure

```XML
<DiagnosticMonitorConfiguration overallQuotaInMB="4096" sinks="ApplicationInsights">
```
```JSON
"DiagnosticMonitorConfiguration": {
    "overallQuotaInMB": 4096,
    "sinks": "ApplicationInsights",
}
```

### <a name="send-only-error-logs-toohello-application-insights-sink"></a>Enviar solo registros toohello Application Insights el receptor de errores

```XML
<DiagnosticMonitorConfiguration overallQuotaInMB="4096" sinks="ApplicationInsights.MyTopDiagdata">
```
```JSON
"DiagnosticMonitorConfiguration": {
    "overallQuotaInMB": 4096,
    "sinks": "ApplicationInsights.MyTopDiagData",
}
```

### <a name="send-verbose-application-logs-tooapplication-insights"></a>Enviar tooApplication visión de registros de aplicación detallado

```XML
<Logs scheduledTransferPeriod="PT1M" scheduledTransferLogLevelFilter="Verbose" sinks="ApplicationInsights.MyLogData"/>
```
```JSON
"DiagnosticMonitorConfiguration": {
    "overallQuotaInMB": 4096,
    "sinks": "ApplicationInsights.MyLogData",
}
```

## <a name="limitations"></a>Limitaciones

- **Channels solo registra el tipo de registro y no los contadores de rendimiento.** Si especifica un canal con un elemento de contador de rendimiento, se pasará por alto.
- **nivel de registro de Hello para un canal no puede superar el nivel de registro de hello para lo que se está recopilando por diagnósticos de Azure.** Por ejemplo, no se puede recopilar los errores de registro de aplicación en el elemento de registros de Hola e intente toosend registros detallados toohello Application Insight receptor. Hola *scheduledTransferLogLevelFilter* atributo siempre debe recopilar igual o más registros de Hola la sesión están tratando de toosend tooa receptor.
- **No se puede enviar datos de blob recopilados por diagnósticos de Azure extensión tooApplication visión.** Por ejemplo, especificar nada en hello *directorios* nodo. Para volcados Hola real volcado de memoria se envía tooblob almacenamiento y se genera solo una notificación que Hola volcado de memoria se envían información tooApplication.

## <a name="next-steps"></a>Pasos siguientes
* Obtenga información acerca de cómo demasiado[ver la información de diagnóstico de Azure](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-cloudservices#view-azure-diagnostic-events) en Application Insights.
* Use [PowerShell](../cloud-services/cloud-services-diagnostics-powershell.md) tooenable Hola extensión de diagnósticos de Azure para su aplicación.
* Use [Visual Studio](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md) tooenable Hola extensión de diagnósticos de Azure para la aplicación
