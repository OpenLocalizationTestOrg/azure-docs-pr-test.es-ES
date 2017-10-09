---
title: "esquema de configuración 1.3 y versiones posteriores de extensión de diagnósticos de aaaAzure | Documentos de Microsoft"
description: "Esquema versión 1.3 y posteriores diagnósticos de Azure se incluyen como parte del programa Hola a Microsoft Azure SDK 2.4 y versiones posterior."
services: monitoring-and-diagnostics
documentationcenter: .net
author: rboucher
manager: carmonm
editor: 
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/15/2017
ms.author: robb
ms.openlocfilehash: bd15d3a79ea818fcb3235854717e58d5da36518e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-diagnostics-13-and-later-configuration-schema"></a>Esquema de configuración de Azure Diagnostics 1.3 y posterior
> [!NOTE]
> Hola extensión de diagnósticos de Azure es el componente de hello usa toocollect los contadores de rendimiento y otras estadísticas de:
> - Máquinas virtuales de Azure 
> - Conjuntos de escalado de máquina virtual
> - Service Fabric 
> - Cloud Services 
> - Grupos de seguridad de red
> 
> Esta página solo es pertinente si está usando uno de estos servicios.

Esta página es válida para las versiones 1.3 y posterior (Azure SDK 2.4 y posterior). Las secciones de configuración más recientes son tooshow comentado en qué versión se han agregado.  

archivo de configuración de Hello descrito aquí es configuración de diagnóstico de tooset usado cuando inicia de monitor de diagnóstico de Hola.  

extensión de Hola se utiliza junto con otros productos de diagnósticos de Microsoft como Monitor de Azure, Application Insights y análisis de registros.



Descargar definición de esquema de archivo de configuración pública de hello ejecutando el siguiente comando de PowerShell de hello:  

```powershell  
(Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File –Encoding utf8 -FilePath 'C:\temp\WadConfig.xsd'  
```  

Para obtener información sobre Azure Diagnostics, consulte [este artículo sobre dicha extensión](azure-diagnostics.md).  

## <a name="example-of-hello-diagnostics-configuration-file"></a>Ejemplo de archivo de configuración de diagnósticos de Hola  
 Hola de ejemplo siguiente muestra un archivo de configuración de diagnóstico típico:  

```xml  
<?xml version="1.0" encoding="utf-8"?>  
<DiagnosticsConfiguration  xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">   
  <PublicConfig>  
    <WadCfg>  
      <DiagnosticMonitorConfiguration overallQuotaInMB="10000">  

        <PerformanceCounters scheduledTransferPeriod="PT1M">  
          <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT1M" unit="percent" />  
        </PerformanceCounters>  

        <Directories scheduledTransferPeriod="PT5M">  
          <IISLogs containerName="iislogs" />  
          <FailedRequestLogs containerName="iisfailed" />  

          <DataSources>  
            <DirectoryConfiguration containerName="mynewprocess">  
              <Absolute path="C:\MyNewProcess" expandEnvironment="false" />  
            </DirectoryConfiguration>  
            <DirectoryConfiguration containerName="badapp">  
              <Absolute path="%SYSTEMDRIVE%\BadApp" expandEnvironment="true" />  
            </DirectoryConfiguration>  
            <DirectoryConfiguration containerName="goodapp">  
              <LocalResource name="Skippy" relativePath="..\PeanutButter"/>  
            </DirectoryConfiguration>  
          </DataSources>  

        </Directories>  

        <EtwProviders>  
          <EtwEventSourceProviderConfiguration   
                       provider="MyProviderClass"   
                       scheduledTransferPeriod="PT5M">  
            <Event id="0"/>  
            <Event id="1" eventDestination="errorTable"/>  
            <DefaultEvents />  
          </EtwEventSourceProviderConfiguration>  
          <EtwManifestProviderConfiguration provider="5974b00b-84c2-44bc-9e58-3a2451b4e3ad" scheduledTransferLogLevelFilter="Information" scheduledTransferPeriod="PT2M">  
            <Event id="0"/>  
            <DefaultEvents eventDestination="defaultTable"/>  
          </EtwManifestProviderConfiguration>  
        </EtwProviders>  

        <WindowsEventLog scheduledTransferPeriod="PT5M">  
          <DataSource name="System!*[System[Provider[@Name='Microsoft Antimalware']]]"/>  
          <DataSource name="System!*[System[Provider[@Name='NTFS'] and (EventID=55)]]" />  
          <DataSource name="System!*[System[Provider[@Name='disk'] and (EventID=7 or EventID=52 or EventID=55)]]" />  
        </WindowsEventLog>  

        <Logs  bufferQuotaInMB="1024"   
             scheduledTransferPeriod="PT1M"   
             scheduledTransferLogLevelFilter="Verbose"   
             sinks="ApplicationInsights.AppLogs"/>  <!-- sinks attribute added in 1.5 -->  

        <CrashDumps containerName="wad-crashdumps" directoryQuotaPercentage="30" dumpType="Mini">  
          <CrashDumpConfiguration processName="mynewprocess.exe" />  
          <CrashDumpConfiguration processName="badapp.exe"/>  
        </CrashDumps>  

        <DockerSources> <!-- Added in 1.9 --> 
          <Stats enabled="true" sampleRate="PT1M" scheduledTransferPeriod="PT1M" />
        </DockerSources>

      </DiagnosticMonitorConfiguration>  

      <SinksConfig>   <!-- Added in 1.5 -->  
        <Sink name="ApplicationInsights">   
          <ApplicationInsights>{Insert InstrumentationKey}</ApplicationInsights>   
          <Channels>   
            <Channel logLevel="Error" name="Errors"  />   
            <Channel logLevel="Verbose" name="AppLogs"  />   
          </Channels>   
        </Sink>   
        <Sink name="EventHub"> <!-- Added in 1.7 -->
          <EventHub Url="https://myeventhub-ns.servicebus.windows.net/diageventhub" SharedAccessKeyName="SendRule" usePublisherId="false" />
        </Sink>
        <Sink name="secondaryEventHub"> <!-- Added in 1.7 -->
          <EventHub Url="https://myeventhub-ns.servicebus.windows.net/secondarydiageventhub" SharedAccessKeyName="SendRule" usePublisherId="false" />
        </Sink>
        <Sink name="secondaryStorageAccount"> <!-- Added in 1.7 -->
          <StorageAccount name="secondarydiagstorageaccount" endpoint="https://core.windows.net" />
        </Sink>
   </SinksConfig>

  </WadCfg>  

  <StorageAccount>diagstorageaccount</StorageAccount>
  <StorageType>TableAndBlob</StorageType> <!-- Added in 1.8 -->  
  </PublicConfig>  

  <PrivateConfig>  <!-- Added in 1.3 -->  
    <StorageAccount name="" key="" endpoint="" sasToken="{sas token}"  />  <!-- sasToken in Private config added in 1.8.1 -->  
    <EventHub Url="https://myeventhub-ns.servicebus.windows.net/diageventhub" SharedAccessKeyName="SendRule" SharedAccessKey="{base64 encoded key}" />
   
    <SecondaryStorageAccounts>
       <StorageAccount name="secondarydiagstorageaccount" key="{base64 encoded key}" endpoint="https://core.windows.net" sasToken="{sas token}" />
    </SecondaryStorageAccounts>
   
    <SecondaryEventHubs>
       <EventHub Url="https://myeventhub-ns.servicebus.windows.net/secondarydiageventhub" SharedAccessKeyName="SendRule" SharedAccessKey="{base64 encoded key}" />
    </SecondaryEventHubs>

  </PrivateConfig>  
  <IsEnabled>true</IsEnabled>  
</DiagnosticsConfiguration>  

```  

Equivalente JSON de archivo de configuración XML anterior Hola. 

Hola PublicConfig y PrivateConfig se separan porque en la mayoría de los casos de uso de json, se pasan como variables distintas. En estos casos se incluyen plantillas de Resource Manager, conjuntos de escalado de máquinas virtuales, PowerShell y Visual Studio. 

```json
"PublicConfig" {
    "WadCfg": {
        "DiagnosticMonitorConfiguration": {
            "overallQuotaInMB": 10000,
            "DiagnosticInfrastructureLogs": {
                "scheduledTransferLogLevelFilter": "Error"
            },
            "PerformanceCounters": {
                "scheduledTransferPeriod": "PT1M",
                "PerformanceCounterConfiguration": [
                    {
                        "counterSpecifier": "\\Processor(_Total)\\% Processor Time",
                        "sampleRate": "PT1M",
                        "unit": "percent"
                    }
                ]
            },
            "Directories": {
                "scheduledTransferPeriod": "PT5M",
                "IISLogs": {
                    "containerName": "iislogs"
                },
                "FailedRequestLogs": {
                    "containerName": "iisfailed"
                },
                "DataSources": [
                    {
                        "containerName": "mynewprocess",
                        "Absolute": {
                            "path": "C:\\MyNewProcess",
                            "expandEnvironment": false
                        }
                    },
                    {
                        "containerName": "badapp",
                        "Absolute": {
                            "path": "%SYSTEMDRIVE%\\BadApp",
                            "expandEnvironment": true
                        }
                    },
                    {
                        "containerName": "goodapp",
                        "LocalResource": {
                            "relativePath": "..\\PeanutButter",
                            "name": "Skippy"
                        }
                    }
                ]
            },
            "EtwProviders": {
                "sinks": "",
                "EtwEventSourceProviderConfiguration": [
                    {
                        "scheduledTransferPeriod": "PT5M",
                        "provider": "MyProviderClass",
                        "Event": [
                            {
                                "id": 0
                            },
                            {
                                "id": 1,
                                "eventDestination": "errorTable"
                            }
                        ],
                        "DefaultEvents": {
                        }
                    }
                ],
                "EtwManifestProviderConfiguration": [
                    {
                        "scheduledTransferPeriod": "PT2M",
                        "scheduledTransferLogLevelFilter": "Information",
                        "provider": "5974b00b-84c2-44bc-9e58-3a2451b4e3ad",
                        "Event": [
                            {
                                "id": 0
                            }
                        ],
                        "DefaultEvents": {
                        }
                    }
                ]
            },
            "WindowsEventLog": {
                "scheduledTransferPeriod": "PT5M",
                "DataSource": [
                    {
                        "name": "System!*[System[Provider[@Name='Microsoft Antimalware']]]"
                    },
                    {
                        "name": "System!*[System[Provider[@Name='NTFS'] and (EventID=55)]]"
                    },
                    {
                        "name": "System!*[System[Provider[@Name='disk'] and (EventID=7 or EventID=52 or EventID=55)]]"
                    }
                ]
            },
            "Logs": {
                "scheduledTransferPeriod": "PT1M",
                "scheduledTransferLogLevelFilter": "Verbose",
                "sinks": "ApplicationInsights.AppLogs"
            },
            "CrashDumps": {
                "directoryQuotaPercentage": 30,
                "dumpType": "Mini",
                "containerName": "wad-crashdumps",
                "CrashDumpConfiguration": [
                    {
                        "processName": "mynewprocess.exe"
                    },
                    {
                        "processName": "badapp.exe"
                    }
                ]
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
                                "name": "Errors"
                            },
                            {
                                "logLevel": "Verbose",
                                "name": "AppLogs"
                            }
                        ]
                    }
                },
                {
                    "name": "EventHub",
                    "EventHub": {
                        "Url": "https://myeventhub-ns.servicebus.windows.net/diageventhub",
                        "SharedAccessKeyName": "SendRule",
                        "usePublisherId": false
                    }
                },
                {
                    "name": "secondaryEventHub",
                    "EventHub": {
                        "Url": "https://myeventhub-ns.servicebus.windows.net/secondarydiageventhub",
                        "SharedAccessKeyName": "SendRule",
                        "usePublisherId": false
                    }
                },
                {
                    "name": "secondaryStorageAccount",
                    "StorageAccount": {
                        "name": "secondarydiagstorageaccount",
                        "endpoint": "https://core.windows.net"
                    }
                }
            ]
        }
    },
    "StorageAccount": "diagstorageaccount",
    "StorageType": "TableAndBlob"
}
```

```json
"PrivateConfig" {
    "storageAccountName": "diagstorageaccount",
    "storageAccountKey": "{base64 encoded key}",
    "storageAccountEndPoint": "https://core.windows.net",
    "storageAccountSasToken": "{sas token}",
    "EventHub": {
        "Url": "https://myeventhub-ns.servicebus.windows.net/diageventhub",
        "SharedAccessKeyName": "SendRule",
        "SharedAccessKey": "{base64 encoded key}"
    },
    "SecondaryStorageAccounts": {
        "StorageAccount": [
            {
                "name": "secondarydiagstorageaccount",
                "key": "{base64 encoded key}",
                "endpoint": "https://core.windows.net",
                "sasToken": "{sas token}"
            }
        ]
    },
    "SecondaryEventHubs": {
        "EventHub": [
            {
                "Url": "https://myeventhub-ns.servicebus.windows.net/secondarydiageventhub",
                "SharedAccessKeyName": "SendRule",
                "SharedAccessKey": "{base64 encoded key}"
            }
        ]
    }
}

```

## <a name="reading-this-page"></a>Lectura de esta página  
 Hello las etiquetas siguientes son aproximadamente en el orden mostrado en el anterior ejemplo de Hola.  Si no ve una descripción completa donde se espera, la página de Hola de hello elemento o atributo de búsqueda.  

## <a name="common-attribute-types"></a>Tipos de atributos comunes  
 El atributo **scheduledTransferPeriod** aparece en varios elementos. Es intervalo de saludo entre toostorage transferencias programadas redondeado toohello más cercano de minuto. valor de Hello es un [XML "Tipo de datos de duración".](http://www.w3schools.com/schema/schema_dtypes_date.asp)


## <a name="diagnosticsconfiguration-element"></a>Elemento DiagnosticsConfiguration  
 *Árbol: Raíz - DiagnosticsConfiguration*

Agregado en la versión 1.3.  

elemento de nivel superior de Hola Hola diagnósticos del archivo de configuración.  

**Atributo** xmlns: Hola espacio de nombres XML para el archivo de configuración de diagnósticos de hello es:  
http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration  


|Elementos secundarios|Descripción|  
|--------------------|-----------------|  
|**PublicConfig**|Obligatorio. Consulte la descripción en cualquier parte de esta página.|  
|**PrivateConfig**|Opcional. Consulte la descripción en cualquier parte de esta página.|  
|**IsEnabled**|Booleano. Consulte la descripción en cualquier parte de esta página.|  

## <a name="publicconfig-element"></a>Elemento PublicConfig  
 *Árbol: Raíz - DiagnosticsConfiguration - PublicConfig*

 Describe la configuración de diagnóstico pública Hola.  

|Elementos secundarios|Descripción|  
|--------------------|-----------------|  
|**WadCfg**|Obligatorio. Consulte la descripción en cualquier parte de esta página.|  
|**StorageAccount**|nombre de Hola Hola almacenamiento de Azure toostore Hola los datos de cuenta en. También se puede especificar como parámetro al ejecutar el cmdlet de hello AzureServiceDiagnosticsExtension del conjunto.|  
|**StorageType**|Puede ser *Table*, *Blob* o *TableAndBlob*. Table es el valor predeterminado. Cuando se elige TableAndBlob, datos de diagnóstico se escriben dos veces: una vez tooeach tipo.|  
|**LocalResourceDirectory**|directorio de Hello en la máquina virtual de Hola donde hello Monitoring Agent almacena los datos del evento. Si no es así, se establece, se utiliza directorio predeterminado de hello:<br /><br /> Para un rol de trabajo o web: `C:\Resources\<guid>\directory\<guid>.<RoleName.DiagnosticStore\`<br /><br /> Para una máquina virtual: `C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<WADVersion>\WAD<WADVersion>`<br /><br /> Los atributos necesarios son:<br /><br /> - **ruta de acceso** : hello directorio Hola sistema toobe utilizado por diagnósticos de Azure.<br /><br /> - **expandEnvironment** -controla si las variables de entorno se expanden en nombre de ruta de acceso de Hola.|  

## <a name="wadcfg-element"></a>Elemento WadCFG  
 *Árbol: Raíz - DiagnosticsConfiguration - PublicConfig - WadCFG*
 
 Identifica y configura toobe de datos de telemetría de hello recopilado.  


## <a name="diagnosticmonitorconfiguration-element"></a>Elemento DiagnosticMonitorConfiguration 
 *Árbol: Raíz - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration*

 Obligatorio 

|Attributes|Descripción|  
|----------------|-----------------|  
| **overallQuotaInMB** | cantidad máxima de Hola de espacio en disco local que se puede utilizar en hello diversos tipos de datos de diagnóstico recopilan por diagnósticos de Azure. saludo predeterminado es 5.120 MB.<br />
|**useProxyServer** | Configurar el proxy de servidor de diagnósticos de Azure toouse hello como conjunto de configuración de Internet Explorer.|  

<br /> <br />

|Elementos secundarios|Descripción|  
|--------------------|-----------------|  
|**CrashDumps**|Consulte la descripción en cualquier parte de esta página.|  
|**DiagnosticInfrastructureLogs**|Habilite la recopilación de registros generados por Diagnósticos de Azure. registros de infraestructura de diagnóstico de Hello son útiles para solucionar Hola del sistema de diagnóstico. Los atributos opcionales son:<br /><br /> - **scheduledTransferLogLevelFilter** -configura el nivel de gravedad mínimo de Hola de registros de Hola se recopilan.<br /><br /> - **scheduledTransferPeriod** -intervalo de saludo entre las transferencias programadas toostorage redondea toohello más cercano de minuto. valor de Hello es un [XML "Tipo de datos de duración".](http://www.w3schools.com/schema/schema_dtypes_date.asp) |  
|**Directorios**|Consulte la descripción en cualquier parte de esta página.|  
|**EtwProviders**|Consulte la descripción en cualquier parte de esta página.|  
|**Métricas**|Consulte la descripción en cualquier parte de esta página.|  
|**PerformanceCounters**|Consulte la descripción en cualquier parte de esta página.|  
|**WindowsEventLog**|Consulte la descripción en cualquier parte de esta página.| 
|**DockerSources**|Consulte la descripción en cualquier parte de esta página. | 



## <a name="crashdumps-element"></a>Elemento CrashDumps  
 *Árbol: Raíz - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - CrashDumps*
 
 Habilite la recopilación de Hola de volcados de memoria.  

|Attributes|Descripción|  
|----------------|-----------------|  
|**containerName**|Opcional. nombre de Hola Hola del contenedor de blobs en su toobe de cuenta de almacenamiento de Azure usa toostore volcados de memoria.|  
|**crashDumpType**|Opcional.  Configura los diagnósticos de Azure toocollect parcial o completo volcados de memoria.|  
|**directoryQuotaPercentage**|Opcional.  Configura el porcentaje de Hola de **overallQuotaInMB** toobe reservado para volcados en hello máquina virtual.|  

|Elementos secundarios|Descripción|  
|--------------------|-----------------|  
|**CrashDumpConfiguration**|Obligatorio. Define los valores de configuración para cada proceso.<br /><br /> Hola siguiente atributo también se necesita:<br /><br /> **processName** : hello nombre del proceso de hello desea toocollect de diagnósticos de Azure un volcado de memoria de.|  

## <a name="directories-element"></a>Elemento Directories 
 *Árbol: Raíz - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration -  Directories*

 Habilita Hola Hola el contenido de un directorio de colección, error de IIS, los registros de solicitud de acceso y registros de IIS.  

 Atributo **scheduledTransferPeriod** opcional. Consulte la explicación anterior.  

|Elementos secundarios|Descripción|  
|--------------------|-----------------|  
|**IISLogs**|Incluir este elemento en configuración de hello habilita la recopilación de Hola de registros de IIS:<br /><br /> **containerName** -nombre de Hola Hola del contenedor de blobs en su toobe de cuenta de almacenamiento de Azure usa toostore Hola los registros de IIS.|   
|**FailedRequestLogs**|Incluir este elemento en configuración de hello habilita la recopilación de registros sobre las solicitudes con error tooan IIS sitio o aplicación. También debe habilitar las opciones de seguimiento en **system.WebServer** de **Web.config**.|  
|**DataSources**|Una lista de directorios toomonitor.| 




## <a name="datasources-element"></a>Elemento DataSources  
 *Árbol: Raíz - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Directories - DataSources*

 Una lista de directorios toomonitor.  

|Elementos secundarios|Descripción|  
|--------------------|-----------------|  
|**DirectoryConfiguration**|Obligatorio. Atributo necesario:<br /><br /> **containerName** : hello nombre de contenedor de blobs de hello en la cuenta de almacenamiento de Azure que toobe utiliza archivos de registro de hello toostore.|  





## <a name="directoryconfiguration-element"></a>Elemento DirectoryConfiguration  
 *Árbol: Raíz - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Directories - DataSources - DirectoryConfiguration*

 Puede incluir cualquier hello **absoluta** o **LocalResource** elemento pero no ambos.  

|Elementos secundarios|Descripción|  
|--------------------|-----------------|  
|**Absolute**|Hola toomonitor de directorio toohello de ruta de acceso absoluta. Hola siguientes atributos es necesario:<br /><br /> - **Ruta de acceso** -Hola toomonitor de directorio toohello de ruta de acceso absoluta.<br /><br /> - **expandEnvironment**: configura si se expanden las variables de entorno en Path.|  
|**LocalResource**|Hola toomonitor de ruta de acceso relativa tooa recurso local. Los atributos necesarios son:<br /><br /> - **Nombre de** -Hola recurso local que contiene Hola directory toomonitor<br /><br /> - **relativePath** -Hola tooName relativa de ruta de acceso que contiene Hola directory toomonitor|  



## <a name="etwproviders-element"></a>Elemento EtwProviders  
 *Árbol: Raíz - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders*

 Configura la recopilación de eventos ETW en EventSource o el manifiesto de ETW en función de los proveedores.  

|Elementos secundarios|Descripción|  
|--------------------|-----------------|  
|**EtwEventSourceProviderConfiguration**|Configura la recopilación de eventos generados a partir de la [clase EventSource](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx). Atributo necesario:<br /><br /> **proveedor de** -nombre de la clase hello de evento de EventSource Hola.<br /><br /> Los atributos opcionales son:<br /><br /> - **scheduledTransferLogLevelFilter** -Hola cuenta de almacenamiento de tooyour tootransfer de nivel de gravedad mínimo.<br /><br /> - **scheduledTransferPeriod** -intervalo de saludo entre las transferencias programadas toostorage redondea toohello más cercano de minuto. valor de Hello es un [XML "Tipo de datos de duración".](http://www.w3schools.com/schema/schema_dtypes_date.asp) |  
|**EtwManifestProviderConfiguration**|Atributo necesario:<br /><br /> **proveedor** -Hola GUID del proveedor de eventos de Hola<br /><br /> Los atributos opcionales son:<br /><br /> - **scheduledTransferLogLevelFilter** -Hola cuenta de almacenamiento de tooyour tootransfer de nivel de gravedad mínimo.<br /><br /> - **scheduledTransferPeriod** -intervalo de saludo entre las transferencias programadas toostorage redondea toohello más cercano de minuto. valor de Hello es un [XML "Tipo de datos de duración".](http://www.w3schools.com/schema/schema_dtypes_date.asp) |  



## <a name="etweventsourceproviderconfiguration-element"></a>Elemento EtwEventSourceProviderConfiguration  
 *Árbol: Raíz - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders- EtwEventSourceProviderConfiguration*

 Configura la recopilación de eventos generados a partir de la [clase EventSource](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx).  

|Elementos secundarios|Descripción|  
|--------------------|-----------------|  
|**DefaultEvents**|Atributo opcional:<br/><br/> **eventDestination** : hello nombre hello toostore Hola eventos de tabla en|  
|**Evento**|Atributo necesario:<br /><br /> **Id. de** -Id. de Hola de evento Hola.<br /><br /> Atributo opcional:<br /><br /> **eventDestination** : hello nombre hello toostore Hola eventos de tabla en|  



## <a name="etwmanifestproviderconfiguration-element"></a>Elemento EtwManifestProviderConfiguration  
 *Árbol: Raíz - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders - EtwManifestProviderConfiguration*

|Elementos secundarios|Descripción|  
|--------------------|-----------------|  
|**DefaultEvents**|Atributo opcional:<br /><br /> **eventDestination** : hello nombre hello toostore Hola eventos de tabla en|  
|**Evento**|Atributo necesario:<br /><br /> **Id. de** -Id. de Hola de evento Hola.<br /><br /> Atributo opcional:<br /><br /> **eventDestination** : hello nombre hello toostore Hola eventos de tabla en|  



## <a name="metrics-element"></a>Elemento Metrics  
 *Árbol: Raíz - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Metrics*

 Le permite toogenerate una tabla de contador de rendimiento que se optimiza para las consultas rápidas. Cada contador de rendimiento que se define en hello **PerformanceCounters** elemento se almacena en la tabla de métricas de hello en la tabla de contador de rendimiento de toohello de adición.  

 Hola **resourceId** atributo es necesario.  Hola Id. de recurso de máquina Virtual que va a implementar diagnósticos de Azure para hello. Obtener hello **resourceID** de hello [portal de Azure](https://portal.azure.com). Seleccione **Examinar** -> **Grupos de recursos** -> **<Nombre\>**. Haga clic en hello **propiedades** icono y copie el valor de Hola de hello **identificador** campo.  

|Elementos secundarios|Descripción|  
|--------------------|-----------------|  
|**MetricAggregation**|Atributo necesario:<br /><br /> **scheduledTransferPeriod** -intervalo de saludo entre las transferencias programadas toostorage redondea toohello más cercano de minuto. valor de Hello es un [XML "Tipo de datos de duración".](http://www.w3schools.com/schema/schema_dtypes_date.asp) |  



## <a name="performancecounters-element"></a>Elemento PerformanceCounters  
 *Árbol: Raíz - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - PerformanceCounters*

 Habilita la recopilación de Hola de contadores de rendimiento.  

 Atributo opcional:  

 Atributo **scheduledTransferPeriod** opcional. Consulte la explicación anterior.

|Elemento secundario|Descripción|  
|-------------------|-----------------|  
|**PerformanceCounterConfiguration**|Hola siguientes atributos es necesario:<br /><br /> - **counterSpecifier** : hello nombre de contador de rendimiento de Hola. Por ejemplo: `\Processor(_Total)\% Processor Time`. tooget una lista de rendimiento de los contadores en el host, ejecute el comando de hello `typeperf`.<br /><br /> - **sampleRate** -¿con qué frecuencia hello contador debe realizarse el muestreo.<br /><br /> Atributo opcional:<br /><br /> **unidad** -Hola unidad de medida de contador de Hola.|  




## <a name="windowseventlog-element"></a>Elemento WindowsEventLog
 *Árbol: Raíz - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - WindowsEventLog*
 
 Habilita la recopilación de Hola de registros de eventos de Windows.  

 Atributo **scheduledTransferPeriod** opcional. Consulte la explicación anterior.  

|Elemento secundario|Descripción|  
|-------------------|-----------------|  
|**DataSource**|Hola toocollect de registros de eventos de Windows. Atributo necesario:<br /><br /> **nombre de** -recopilados de consulta de XPath de Hola que describe toobe de eventos de windows hello. Por ejemplo:<br /><br /> `Application!*[System[(Level <=3)]], System!*[System[(Level <=3)]], System!*[System[Provider[@Name='Microsoft Antimalware']]], Security!*[System[(Level <= 3)]`<br /><br /> toocollect todos los eventos, especifique "*"|  




## <a name="logs-element"></a>Elemento Logs  
 *Árbol: Raíz - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Logs*

 Se presenta en la versión 1.0 y 1.1. Falta en 1.2. Se ha agregado en 1.3.  

 Define la configuración de búfer de Hola para los registros básicos de Azure.  

|Atributo|Tipo|Descripción|  
|---------------|----------|-----------------|  
|**bufferQuotaInMB**|**unsignedInt**|Opcional. Especifica Hola cantidad máxima de almacenamiento del sistema de archivos que está disponible para hello especificado datos.<br /><br /> Hola predeterminado es 0.|  
|**scheduledTransferLogLevelFilterr**|**cadena**|Opcional. Especifica el nivel de gravedad mínimo de Hola para las entradas de registro que se transfieren. es el valor predeterminado de Hello **Undefined**, que transfiere todos los registros. Otros valores posibles (en orden de la mayoría de la información tooleast) son **detallado**, **información**, **advertencia**, **Error**y **Crítica**.|  
|**scheduledTransferPeriod**|**duration**|Opcional. Especifica el intervalo de hello entre las transferencias programadas de datos, redondeado hasta toohello más cercano de minuto.<br /><br /> valor predeterminado de Hello es PT0S.|  
|**sinks**: agregado en 1.5|**cadena**|Opcional. Puntos tooa receptor ubicación tooalso enviar datos de diagnóstico. Por ejemplo, Application Insights.|  

## <a name="dockersources"></a>DockerSources
 *Árbol: Raíz - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - DockerSources*

 Se agregó en la versión 1.9.

|Nombre del elemento|Descripción|  
|------------------|-----------------|  
|**Stats**|Indica el sistema de hello toocollect estadísticas para los contenedores de Docker|  

## <a name="sinksconfig-element"></a>Elemento SinksConfig  
 *Árbol: Raíz - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig*

 Una lista de ubicaciones toosend datos tooand Hola configuración de diagnóstico asociado con esas ubicaciones.  

|Nombre del elemento|Descripción|  
|------------------|-----------------|  
|**Sink**|Consulte la descripción en cualquier parte de esta página.|  

## <a name="sink-element"></a>Elemento Sink
 *Árbol: Raíz - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink*

 Agregado en la versión 1.5.  

 Define ubicaciones toosend datos de diagnóstico. Por ejemplo, hello servicio Application Insights.  

|Atributo|Tipo|Descripción|  
|---------------|----------|-----------------|  
|**name**|cadena|Sinkname de hello identificación de cadena.|  

|Elemento|Escriba|Descripción|  
|-------------|----------|-----------------|  
|**Application Insights**|cadena|Usar solo al enviar datos tooApplication visión. Contener Hola clave de instrumentación para una cuenta activa de Application Insights que tienen acceso a.|  
|**Channels**|cadena|Uno para cada filtrado adicional transmitido|  

## <a name="channels-element"></a>Elemento Channels  
 *Árbol: Raíz - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink - Channels*

 Agregado en la versión 1.5.  

 Define los filtros para los flujos de datos de registro que se pasan a través de un receptor.  

|Elemento|Escriba|Descripción|  
|-------------|----------|-----------------|  
|**Channel**|string|Consulte la descripción en cualquier parte de esta página.|  

## <a name="channel-element"></a>Elemento Channel
 *Árbol: Raíz - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink - Channels - Channel*

 Agregado en la versión 1.5.  

 Define ubicaciones toosend datos de diagnóstico. Por ejemplo, hello servicio Application Insights.  

|Attributes|Escriba|Descripción|  
|----------------|----------|-----------------|  
|**logLevel**|**cadena**|Especifica el nivel de gravedad mínimo de Hola para las entradas de registro que se transfieren. es el valor predeterminado de Hello **Undefined**, que transfiere todos los registros. Otros valores posibles (en orden de la mayoría de la información tooleast) son **detallado**, **información**, **advertencia**, **Error**y **Crítica**.|  
|**name**|**cadena**|Un nombre único de hello canal toorefer a|  


## <a name="privateconfig-element"></a>Elemento PrivateConfig 
 *Árbol: Raíz - DiagnosticsConfiguration - PrivateConfig*

 Agregado en la versión 1.3.  

 Opcional  

 Almacena información privada de hello de la cuenta de almacenamiento de hello (nombre, clave y el extremo). Esta información se envía la máquina virtual de toohello, pero no se puede recuperar del mismo.  

|Elementos secundarios|Descripción|  
|--------------------|-----------------|  
|**StorageAccount**|Hola toouse de cuenta de almacenamiento. Hola siguientes atributos es necesario<br /><br /> - **nombre** : hello nombre de la cuenta de almacenamiento de Hola.<br /><br /> - **clave** : hello clave toohello cuenta de almacenamiento.<br /><br /> - **punto de conexión** -tooaccess de punto de conexión de Hola Hola cuenta de almacenamiento. <br /><br /> -**sasToken** (agregado 1.8.1)-puede especificar un token SAS en lugar de una clave de cuenta de almacenamiento en la configuración privada de Hola. Si se proporciona, se omite la clave de cuenta de almacenamiento de Hola. <br />Requisitos para saludo del Token de SAS: <br />- Solo admite el token de SAS de la cuenta. <br />Se requieren los tipos de servicio - *b* y *t*. <br /> Se requieren los permisos - *a*, *c*, *u* y *w*. <br /> Se requieren los tipos de recursos - *c* y *o*. <br /> -Admite sólo protocolo de hello HTTPS <br /> - La hora de inicio y de expiración debe ser válida.|  


## <a name="isenabled-element"></a>Elemento IsEnabled  
 *Árbol: Raíz - DiagnosticsConfiguration - IsEnabled*

 Booleano. Use `true` tooenable diagnósticos de Hola o `false` diagnóstico de hello toodisable.
