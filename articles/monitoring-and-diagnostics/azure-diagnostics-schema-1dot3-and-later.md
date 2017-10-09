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
# <a name="azure-diagnostics-13-and-later-configuration-schema"></a><span data-ttu-id="2a2e2-103">Esquema de configuración de Azure Diagnostics 1.3 y posterior</span><span class="sxs-lookup"><span data-stu-id="2a2e2-103">Azure Diagnostics 1.3 and later configuration schema</span></span>
> [!NOTE]
> <span data-ttu-id="2a2e2-104">Hola extensión de diagnósticos de Azure es el componente de hello usa toocollect los contadores de rendimiento y otras estadísticas de:</span><span class="sxs-lookup"><span data-stu-id="2a2e2-104">hello Azure Diagnostics extension is hello component used toocollect performance counters and other statistics from:</span></span>
> - <span data-ttu-id="2a2e2-105">Máquinas virtuales de Azure</span><span class="sxs-lookup"><span data-stu-id="2a2e2-105">Azure Virtual Machines</span></span> 
> - <span data-ttu-id="2a2e2-106">Conjuntos de escalado de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="2a2e2-106">Virtual Machine Scale Sets</span></span>
> - <span data-ttu-id="2a2e2-107">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="2a2e2-107">Service Fabric</span></span> 
> - <span data-ttu-id="2a2e2-108">Cloud Services</span><span class="sxs-lookup"><span data-stu-id="2a2e2-108">Cloud Services</span></span> 
> - <span data-ttu-id="2a2e2-109">Grupos de seguridad de red</span><span class="sxs-lookup"><span data-stu-id="2a2e2-109">Network Security Groups</span></span>
> 
> <span data-ttu-id="2a2e2-110">Esta página solo es pertinente si está usando uno de estos servicios.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-110">This page is only relevant if you are using one of these services.</span></span>

<span data-ttu-id="2a2e2-111">Esta página es válida para las versiones 1.3 y posterior (Azure SDK 2.4 y posterior).</span><span class="sxs-lookup"><span data-stu-id="2a2e2-111">This page is valid for versions 1.3 and newer (Azure SDK 2.4 and newer).</span></span> <span data-ttu-id="2a2e2-112">Las secciones de configuración más recientes son tooshow comentado en qué versión se han agregado.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-112">Newer configuration sections are commented tooshow in what version they were added.</span></span>  

<span data-ttu-id="2a2e2-113">archivo de configuración de Hello descrito aquí es configuración de diagnóstico de tooset usado cuando inicia de monitor de diagnóstico de Hola.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-113">hello configuration file described here is used tooset diagnostic configuration settings when hello diagnostics monitor starts.</span></span>  

<span data-ttu-id="2a2e2-114">extensión de Hola se utiliza junto con otros productos de diagnósticos de Microsoft como Monitor de Azure, Application Insights y análisis de registros.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-114">hello extension is used in conjunction with other Microsoft diagnostics products like Azure Monitor, Application Insights, and Log Analytics.</span></span>



<span data-ttu-id="2a2e2-115">Descargar definición de esquema de archivo de configuración pública de hello ejecutando el siguiente comando de PowerShell de hello:</span><span class="sxs-lookup"><span data-stu-id="2a2e2-115">Download hello public configuration file schema definition by executing hello following PowerShell command:</span></span>  

```powershell  
(Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File –Encoding utf8 -FilePath 'C:\temp\WadConfig.xsd'  
```  

<span data-ttu-id="2a2e2-116">Para obtener información sobre Azure Diagnostics, consulte [este artículo sobre dicha extensión](azure-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="2a2e2-116">For more information about using Azure Diagnostics, see [Azure Diagnostics Extension](azure-diagnostics.md).</span></span>  

## <a name="example-of-hello-diagnostics-configuration-file"></a><span data-ttu-id="2a2e2-117">Ejemplo de archivo de configuración de diagnósticos de Hola</span><span class="sxs-lookup"><span data-stu-id="2a2e2-117">Example of hello diagnostics configuration file</span></span>  
 <span data-ttu-id="2a2e2-118">Hola de ejemplo siguiente muestra un archivo de configuración de diagnóstico típico:</span><span class="sxs-lookup"><span data-stu-id="2a2e2-118">hello following example shows a typical diagnostics configuration file:</span></span>  

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

<span data-ttu-id="2a2e2-119">Equivalente JSON de archivo de configuración XML anterior Hola.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-119">JSON equivalent of hello previous XML configuration file.</span></span> 

<span data-ttu-id="2a2e2-120">Hola PublicConfig y PrivateConfig se separan porque en la mayoría de los casos de uso de json, se pasan como variables distintas.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-120">hello PublicConfig and PrivateConfig are separated because in most json usage cases, they are passed as different variables.</span></span> <span data-ttu-id="2a2e2-121">En estos casos se incluyen plantillas de Resource Manager, conjuntos de escalado de máquinas virtuales, PowerShell y Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-121">These cases include Resource Manager templates, Virtual Machine Scale set PowerShell, and Visual Studio.</span></span> 

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

## <a name="reading-this-page"></a><span data-ttu-id="2a2e2-122">Lectura de esta página</span><span class="sxs-lookup"><span data-stu-id="2a2e2-122">Reading this page</span></span>  
 <span data-ttu-id="2a2e2-123">Hello las etiquetas siguientes son aproximadamente en el orden mostrado en el anterior ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-123">hello tags following are roughly in order shown in hello preceding example.</span></span>  <span data-ttu-id="2a2e2-124">Si no ve una descripción completa donde se espera, la página de Hola de hello elemento o atributo de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-124">If you don't see a full description where you expect it, search hello page for hello element or attribute.</span></span>  

## <a name="common-attribute-types"></a><span data-ttu-id="2a2e2-125">Tipos de atributos comunes</span><span class="sxs-lookup"><span data-stu-id="2a2e2-125">Common Attribute Types</span></span>  
 <span data-ttu-id="2a2e2-126">El atributo **scheduledTransferPeriod** aparece en varios elementos.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-126">**scheduledTransferPeriod** attribute appears in several elements.</span></span> <span data-ttu-id="2a2e2-127">Es intervalo de saludo entre toostorage transferencias programadas redondeado toohello más cercano de minuto.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-127">It is hello interval between scheduled transfers toostorage rounded up toohello nearest minute.</span></span> <span data-ttu-id="2a2e2-128">valor de Hello es un [XML "Tipo de datos de duración".](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span><span class="sxs-lookup"><span data-stu-id="2a2e2-128">hello value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span></span>


## <a name="diagnosticsconfiguration-element"></a><span data-ttu-id="2a2e2-129">Elemento DiagnosticsConfiguration</span><span class="sxs-lookup"><span data-stu-id="2a2e2-129">DiagnosticsConfiguration Element</span></span>  
 <span data-ttu-id="2a2e2-130">*Árbol: Raíz - DiagnosticsConfiguration*</span><span class="sxs-lookup"><span data-stu-id="2a2e2-130">*Tree: Root - DiagnosticsConfiguration*</span></span>

<span data-ttu-id="2a2e2-131">Agregado en la versión 1.3.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-131">Added in version 1.3.</span></span>  

<span data-ttu-id="2a2e2-132">elemento de nivel superior de Hola Hola diagnósticos del archivo de configuración.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-132">hello top-level element of hello diagnostics configuration file.</span></span>  

<span data-ttu-id="2a2e2-133">**Atributo** xmlns: Hola espacio de nombres XML para el archivo de configuración de diagnósticos de hello es:</span><span class="sxs-lookup"><span data-stu-id="2a2e2-133">**Attribute**  xmlns - hello XML namespace for hello diagnostics configuration file is:</span></span>  
<span data-ttu-id="2a2e2-134">http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration</span><span class="sxs-lookup"><span data-stu-id="2a2e2-134">http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration</span></span>  


|<span data-ttu-id="2a2e2-135">Elementos secundarios</span><span class="sxs-lookup"><span data-stu-id="2a2e2-135">Child Elements</span></span>|<span data-ttu-id="2a2e2-136">Descripción</span><span class="sxs-lookup"><span data-stu-id="2a2e2-136">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="2a2e2-137">**PublicConfig**</span><span class="sxs-lookup"><span data-stu-id="2a2e2-137">**PublicConfig**</span></span>|<span data-ttu-id="2a2e2-138">Obligatorio.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-138">Required.</span></span> <span data-ttu-id="2a2e2-139">Consulte la descripción en cualquier parte de esta página.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-139">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="2a2e2-140">**PrivateConfig**</span><span class="sxs-lookup"><span data-stu-id="2a2e2-140">**PrivateConfig**</span></span>|<span data-ttu-id="2a2e2-141">Opcional.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-141">Optional.</span></span> <span data-ttu-id="2a2e2-142">Consulte la descripción en cualquier parte de esta página.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-142">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="2a2e2-143">**IsEnabled**</span><span class="sxs-lookup"><span data-stu-id="2a2e2-143">**IsEnabled**</span></span>|<span data-ttu-id="2a2e2-144">Booleano.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-144">Boolean.</span></span> <span data-ttu-id="2a2e2-145">Consulte la descripción en cualquier parte de esta página.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-145">See description elsewhere on this page.</span></span>|  

## <a name="publicconfig-element"></a><span data-ttu-id="2a2e2-146">Elemento PublicConfig</span><span class="sxs-lookup"><span data-stu-id="2a2e2-146">PublicConfig Element</span></span>  
 <span data-ttu-id="2a2e2-147">*Árbol: Raíz - DiagnosticsConfiguration - PublicConfig*</span><span class="sxs-lookup"><span data-stu-id="2a2e2-147">*Tree: Root - DiagnosticsConfiguration - PublicConfig*</span></span>

 <span data-ttu-id="2a2e2-148">Describe la configuración de diagnóstico pública Hola.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-148">Describes hello public diagnostics configuration.</span></span>  

|<span data-ttu-id="2a2e2-149">Elementos secundarios</span><span class="sxs-lookup"><span data-stu-id="2a2e2-149">Child Elements</span></span>|<span data-ttu-id="2a2e2-150">Descripción</span><span class="sxs-lookup"><span data-stu-id="2a2e2-150">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="2a2e2-151">**WadCfg**</span><span class="sxs-lookup"><span data-stu-id="2a2e2-151">**WadCfg**</span></span>|<span data-ttu-id="2a2e2-152">Obligatorio.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-152">Required.</span></span> <span data-ttu-id="2a2e2-153">Consulte la descripción en cualquier parte de esta página.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-153">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="2a2e2-154">**StorageAccount**</span><span class="sxs-lookup"><span data-stu-id="2a2e2-154">**StorageAccount**</span></span>|<span data-ttu-id="2a2e2-155">nombre de Hola Hola almacenamiento de Azure toostore Hola los datos de cuenta en.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-155">hello name of hello Azure Storage account toostore hello data in.</span></span> <span data-ttu-id="2a2e2-156">También se puede especificar como parámetro al ejecutar el cmdlet de hello AzureServiceDiagnosticsExtension del conjunto.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-156">May also be specified as a parameter when executing hello Set-AzureServiceDiagnosticsExtension cmdlet.</span></span>|  
|<span data-ttu-id="2a2e2-157">**StorageType**</span><span class="sxs-lookup"><span data-stu-id="2a2e2-157">**StorageType**</span></span>|<span data-ttu-id="2a2e2-158">Puede ser *Table*, *Blob* o *TableAndBlob*.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-158">Can be *Table*, *Blob*, or *TableAndBlob*.</span></span> <span data-ttu-id="2a2e2-159">Table es el valor predeterminado.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-159">Table is default.</span></span> <span data-ttu-id="2a2e2-160">Cuando se elige TableAndBlob, datos de diagnóstico se escriben dos veces: una vez tooeach tipo.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-160">When TableAndBlob is chosen, diagnostic data is written twice -- once tooeach type.</span></span>|  
|<span data-ttu-id="2a2e2-161">**LocalResourceDirectory**</span><span class="sxs-lookup"><span data-stu-id="2a2e2-161">**LocalResourceDirectory**</span></span>|<span data-ttu-id="2a2e2-162">directorio de Hello en la máquina virtual de Hola donde hello Monitoring Agent almacena los datos del evento.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-162">hello directory on hello virtual machine where hello Monitoring Agent stores event data.</span></span> <span data-ttu-id="2a2e2-163">Si no es así, se establece, se utiliza directorio predeterminado de hello:</span><span class="sxs-lookup"><span data-stu-id="2a2e2-163">If not, set, hello default directory is used:</span></span><br /><br /> <span data-ttu-id="2a2e2-164">Para un rol de trabajo o web: `C:\Resources\<guid>\directory\<guid>.<RoleName.DiagnosticStore\`</span><span class="sxs-lookup"><span data-stu-id="2a2e2-164">For a Worker/web role: `C:\Resources\<guid>\directory\<guid>.<RoleName.DiagnosticStore\`</span></span><br /><br /> <span data-ttu-id="2a2e2-165">Para una máquina virtual: `C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<WADVersion>\WAD<WADVersion>`</span><span class="sxs-lookup"><span data-stu-id="2a2e2-165">For a Virtual Machine: `C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<WADVersion>\WAD<WADVersion>`</span></span><br /><br /> <span data-ttu-id="2a2e2-166">Los atributos necesarios son:</span><span class="sxs-lookup"><span data-stu-id="2a2e2-166">Required attributes are:</span></span><br /><br /> <span data-ttu-id="2a2e2-167">- **ruta de acceso** : hello directorio Hola sistema toobe utilizado por diagnósticos de Azure.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-167">- **path** - hello directory on hello system toobe used by Azure Diagnostics.</span></span><br /><br /> <span data-ttu-id="2a2e2-168">- **expandEnvironment** -controla si las variables de entorno se expanden en nombre de ruta de acceso de Hola.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-168">- **expandEnvironment** - Controls whether environment variables are expanded in hello path name.</span></span>|  

## <a name="wadcfg-element"></a><span data-ttu-id="2a2e2-169">Elemento WadCFG</span><span class="sxs-lookup"><span data-stu-id="2a2e2-169">WadCFG Element</span></span>  
 <span data-ttu-id="2a2e2-170">*Árbol: Raíz - DiagnosticsConfiguration - PublicConfig - WadCFG*</span><span class="sxs-lookup"><span data-stu-id="2a2e2-170">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG*</span></span>
 
 <span data-ttu-id="2a2e2-171">Identifica y configura toobe de datos de telemetría de hello recopilado.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-171">Identifies and configures hello telemetry data toobe collected.</span></span>  


## <a name="diagnosticmonitorconfiguration-element"></a><span data-ttu-id="2a2e2-172">Elemento DiagnosticMonitorConfiguration</span><span class="sxs-lookup"><span data-stu-id="2a2e2-172">DiagnosticMonitorConfiguration Element</span></span> 
 <span data-ttu-id="2a2e2-173">*Árbol: Raíz - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration*</span><span class="sxs-lookup"><span data-stu-id="2a2e2-173">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration*</span></span>

 <span data-ttu-id="2a2e2-174">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="2a2e2-174">Required</span></span> 

|<span data-ttu-id="2a2e2-175">Attributes</span><span class="sxs-lookup"><span data-stu-id="2a2e2-175">Attributes</span></span>|<span data-ttu-id="2a2e2-176">Descripción</span><span class="sxs-lookup"><span data-stu-id="2a2e2-176">Description</span></span>|  
|----------------|-----------------|  
| <span data-ttu-id="2a2e2-177">**overallQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="2a2e2-177">**overallQuotaInMB**</span></span> | <span data-ttu-id="2a2e2-178">cantidad máxima de Hola de espacio en disco local que se puede utilizar en hello diversos tipos de datos de diagnóstico recopilan por diagnósticos de Azure.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-178">hello maximum amount of local disk space that may be consumed by hello various types of diagnostic data collected by Azure Diagnostics.</span></span> <span data-ttu-id="2a2e2-179">saludo predeterminado es 5.120 MB.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-179">hello default setting is 5120 MB.</span></span><br />
|<span data-ttu-id="2a2e2-180">**useProxyServer**</span><span class="sxs-lookup"><span data-stu-id="2a2e2-180">**useProxyServer**</span></span> | <span data-ttu-id="2a2e2-181">Configurar el proxy de servidor de diagnósticos de Azure toouse hello como conjunto de configuración de Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-181">Configure Azure Diagnostics toouse hello proxy server settings as set in IE settings.</span></span>|  

<br /> <br />

|<span data-ttu-id="2a2e2-182">Elementos secundarios</span><span class="sxs-lookup"><span data-stu-id="2a2e2-182">Child Elements</span></span>|<span data-ttu-id="2a2e2-183">Descripción</span><span class="sxs-lookup"><span data-stu-id="2a2e2-183">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="2a2e2-184">**CrashDumps**</span><span class="sxs-lookup"><span data-stu-id="2a2e2-184">**CrashDumps**</span></span>|<span data-ttu-id="2a2e2-185">Consulte la descripción en cualquier parte de esta página.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-185">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="2a2e2-186">**DiagnosticInfrastructureLogs**</span><span class="sxs-lookup"><span data-stu-id="2a2e2-186">**DiagnosticInfrastructureLogs**</span></span>|<span data-ttu-id="2a2e2-187">Habilite la recopilación de registros generados por Diagnósticos de Azure.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-187">Enable collection of logs generated by Azure Diagnostics.</span></span> <span data-ttu-id="2a2e2-188">registros de infraestructura de diagnóstico de Hello son útiles para solucionar Hola del sistema de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-188">hello diagnostic infrastructure logs are useful for troubleshooting hello diagnostics system itself.</span></span> <span data-ttu-id="2a2e2-189">Los atributos opcionales son:</span><span class="sxs-lookup"><span data-stu-id="2a2e2-189">Optional attributes are:</span></span><br /><br /> <span data-ttu-id="2a2e2-190">- **scheduledTransferLogLevelFilter** -configura el nivel de gravedad mínimo de Hola de registros de Hola se recopilan.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-190">- **scheduledTransferLogLevelFilter** - Configures hello minimum severity level of hello logs collected.</span></span><br /><br /> <span data-ttu-id="2a2e2-191">- **scheduledTransferPeriod** -intervalo de saludo entre las transferencias programadas toostorage redondea toohello más cercano de minuto.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-191">- **scheduledTransferPeriod** - hello interval between scheduled transfers toostorage rounded up toohello nearest minute.</span></span> <span data-ttu-id="2a2e2-192">valor de Hello es un [XML "Tipo de datos de duración".](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span><span class="sxs-lookup"><span data-stu-id="2a2e2-192">hello value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span></span> |  
|<span data-ttu-id="2a2e2-193">**Directorios**</span><span class="sxs-lookup"><span data-stu-id="2a2e2-193">**Directories**</span></span>|<span data-ttu-id="2a2e2-194">Consulte la descripción en cualquier parte de esta página.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-194">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="2a2e2-195">**EtwProviders**</span><span class="sxs-lookup"><span data-stu-id="2a2e2-195">**EtwProviders**</span></span>|<span data-ttu-id="2a2e2-196">Consulte la descripción en cualquier parte de esta página.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-196">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="2a2e2-197">**Métricas**</span><span class="sxs-lookup"><span data-stu-id="2a2e2-197">**Metrics**</span></span>|<span data-ttu-id="2a2e2-198">Consulte la descripción en cualquier parte de esta página.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-198">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="2a2e2-199">**PerformanceCounters**</span><span class="sxs-lookup"><span data-stu-id="2a2e2-199">**PerformanceCounters**</span></span>|<span data-ttu-id="2a2e2-200">Consulte la descripción en cualquier parte de esta página.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-200">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="2a2e2-201">**WindowsEventLog**</span><span class="sxs-lookup"><span data-stu-id="2a2e2-201">**WindowsEventLog**</span></span>|<span data-ttu-id="2a2e2-202">Consulte la descripción en cualquier parte de esta página.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-202">See description elsewhere on this page.</span></span>| 
|<span data-ttu-id="2a2e2-203">**DockerSources**</span><span class="sxs-lookup"><span data-stu-id="2a2e2-203">**DockerSources**</span></span>|<span data-ttu-id="2a2e2-204">Consulte la descripción en cualquier parte de esta página.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-204">See description elsewhere on this page.</span></span> | 



## <a name="crashdumps-element"></a><span data-ttu-id="2a2e2-205">Elemento CrashDumps</span><span class="sxs-lookup"><span data-stu-id="2a2e2-205">CrashDumps Element</span></span>  
 <span data-ttu-id="2a2e2-206">*Árbol: Raíz - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - CrashDumps*</span><span class="sxs-lookup"><span data-stu-id="2a2e2-206">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - CrashDumps*</span></span>
 
 <span data-ttu-id="2a2e2-207">Habilite la recopilación de Hola de volcados de memoria.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-207">Enable hello collection of crash dumps.</span></span>  

|<span data-ttu-id="2a2e2-208">Attributes</span><span class="sxs-lookup"><span data-stu-id="2a2e2-208">Attributes</span></span>|<span data-ttu-id="2a2e2-209">Descripción</span><span class="sxs-lookup"><span data-stu-id="2a2e2-209">Description</span></span>|  
|----------------|-----------------|  
|<span data-ttu-id="2a2e2-210">**containerName**</span><span class="sxs-lookup"><span data-stu-id="2a2e2-210">**containerName**</span></span>|<span data-ttu-id="2a2e2-211">Opcional.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-211">Optional.</span></span> <span data-ttu-id="2a2e2-212">nombre de Hola Hola del contenedor de blobs en su toobe de cuenta de almacenamiento de Azure usa toostore volcados de memoria.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-212">hello name of hello blob container in your Azure Storage account toobe used toostore crash dumps.</span></span>|  
|<span data-ttu-id="2a2e2-213">**crashDumpType**</span><span class="sxs-lookup"><span data-stu-id="2a2e2-213">**crashDumpType**</span></span>|<span data-ttu-id="2a2e2-214">Opcional.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-214">Optional.</span></span>  <span data-ttu-id="2a2e2-215">Configura los diagnósticos de Azure toocollect parcial o completo volcados de memoria.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-215">Configures Azure Diagnostics toocollect mini or full crash dumps.</span></span>|  
|<span data-ttu-id="2a2e2-216">**directoryQuotaPercentage**</span><span class="sxs-lookup"><span data-stu-id="2a2e2-216">**directoryQuotaPercentage**</span></span>|<span data-ttu-id="2a2e2-217">Opcional.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-217">Optional.</span></span>  <span data-ttu-id="2a2e2-218">Configura el porcentaje de Hola de **overallQuotaInMB** toobe reservado para volcados en hello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-218">Configures hello percentage of **overallQuotaInMB** toobe reserved for crash dumps on hello VM.</span></span>|  

|<span data-ttu-id="2a2e2-219">Elementos secundarios</span><span class="sxs-lookup"><span data-stu-id="2a2e2-219">Child Elements</span></span>|<span data-ttu-id="2a2e2-220">Descripción</span><span class="sxs-lookup"><span data-stu-id="2a2e2-220">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="2a2e2-221">**CrashDumpConfiguration**</span><span class="sxs-lookup"><span data-stu-id="2a2e2-221">**CrashDumpConfiguration**</span></span>|<span data-ttu-id="2a2e2-222">Obligatorio.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-222">Required.</span></span> <span data-ttu-id="2a2e2-223">Define los valores de configuración para cada proceso.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-223">Defines configuration values for each process.</span></span><br /><br /> <span data-ttu-id="2a2e2-224">Hola siguiente atributo también se necesita:</span><span class="sxs-lookup"><span data-stu-id="2a2e2-224">hello following attribute is also required:</span></span><br /><br /> <span data-ttu-id="2a2e2-225">**processName** : hello nombre del proceso de hello desea toocollect de diagnósticos de Azure un volcado de memoria de.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-225">**processName** - hello name of hello process you want Azure Diagnostics toocollect a crash dump for.</span></span>|  

## <a name="directories-element"></a><span data-ttu-id="2a2e2-226">Elemento Directories</span><span class="sxs-lookup"><span data-stu-id="2a2e2-226">Directories Element</span></span> 
 <span data-ttu-id="2a2e2-227">*Árbol: Raíz - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration -  Directories*</span><span class="sxs-lookup"><span data-stu-id="2a2e2-227">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration -  Directories*</span></span>

 <span data-ttu-id="2a2e2-228">Habilita Hola Hola el contenido de un directorio de colección, error de IIS, los registros de solicitud de acceso y registros de IIS.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-228">Enables hello collection of hello contents of a directory, IIS failed access request logs and/or IIS logs.</span></span>  

 <span data-ttu-id="2a2e2-229">Atributo **scheduledTransferPeriod** opcional.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-229">Optional **scheduledTransferPeriod** attribute.</span></span> <span data-ttu-id="2a2e2-230">Consulte la explicación anterior.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-230">See explanation earlier.</span></span>  

|<span data-ttu-id="2a2e2-231">Elementos secundarios</span><span class="sxs-lookup"><span data-stu-id="2a2e2-231">Child Elements</span></span>|<span data-ttu-id="2a2e2-232">Descripción</span><span class="sxs-lookup"><span data-stu-id="2a2e2-232">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="2a2e2-233">**IISLogs**</span><span class="sxs-lookup"><span data-stu-id="2a2e2-233">**IISLogs**</span></span>|<span data-ttu-id="2a2e2-234">Incluir este elemento en configuración de hello habilita la recopilación de Hola de registros de IIS:</span><span class="sxs-lookup"><span data-stu-id="2a2e2-234">Including this element in hello configuration enables hello collection of IIS logs:</span></span><br /><br /> <span data-ttu-id="2a2e2-235">**containerName** -nombre de Hola Hola del contenedor de blobs en su toobe de cuenta de almacenamiento de Azure usa toostore Hola los registros de IIS.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-235">**containerName** - hello name of hello blob container in your Azure Storage account toobe used toostore hello IIS logs.</span></span>|   
|<span data-ttu-id="2a2e2-236">**FailedRequestLogs**</span><span class="sxs-lookup"><span data-stu-id="2a2e2-236">**FailedRequestLogs**</span></span>|<span data-ttu-id="2a2e2-237">Incluir este elemento en configuración de hello habilita la recopilación de registros sobre las solicitudes con error tooan IIS sitio o aplicación.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-237">Including this element in hello configuration enables collection of logs about failed requests tooan IIS site or application.</span></span> <span data-ttu-id="2a2e2-238">También debe habilitar las opciones de seguimiento en **system.WebServer** de **Web.config**.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-238">You must also enable tracing options under **system.WebServer** in **Web.config**.</span></span>|  
|<span data-ttu-id="2a2e2-239">**DataSources**</span><span class="sxs-lookup"><span data-stu-id="2a2e2-239">**DataSources**</span></span>|<span data-ttu-id="2a2e2-240">Una lista de directorios toomonitor.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-240">A list of directories toomonitor.</span></span>| 




## <a name="datasources-element"></a><span data-ttu-id="2a2e2-241">Elemento DataSources</span><span class="sxs-lookup"><span data-stu-id="2a2e2-241">DataSources Element</span></span>  
 <span data-ttu-id="2a2e2-242">*Árbol: Raíz - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Directories - DataSources*</span><span class="sxs-lookup"><span data-stu-id="2a2e2-242">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Directories - DataSources*</span></span>

 <span data-ttu-id="2a2e2-243">Una lista de directorios toomonitor.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-243">A list of directories toomonitor.</span></span>  

|<span data-ttu-id="2a2e2-244">Elementos secundarios</span><span class="sxs-lookup"><span data-stu-id="2a2e2-244">Child Elements</span></span>|<span data-ttu-id="2a2e2-245">Descripción</span><span class="sxs-lookup"><span data-stu-id="2a2e2-245">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="2a2e2-246">**DirectoryConfiguration**</span><span class="sxs-lookup"><span data-stu-id="2a2e2-246">**DirectoryConfiguration**</span></span>|<span data-ttu-id="2a2e2-247">Obligatorio.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-247">Required.</span></span> <span data-ttu-id="2a2e2-248">Atributo necesario:</span><span class="sxs-lookup"><span data-stu-id="2a2e2-248">Required attribute:</span></span><br /><br /> <span data-ttu-id="2a2e2-249">**containerName** : hello nombre de contenedor de blobs de hello en la cuenta de almacenamiento de Azure que toobe utiliza archivos de registro de hello toostore.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-249">**containerName** - hello name of hello blob container in your Azure Storage account that toobe used toostore hello log files.</span></span>|  





## <a name="directoryconfiguration-element"></a><span data-ttu-id="2a2e2-250">Elemento DirectoryConfiguration</span><span class="sxs-lookup"><span data-stu-id="2a2e2-250">DirectoryConfiguration Element</span></span>  
 <span data-ttu-id="2a2e2-251">*Árbol: Raíz - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Directories - DataSources - DirectoryConfiguration*</span><span class="sxs-lookup"><span data-stu-id="2a2e2-251">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Directories - DataSources - DirectoryConfiguration*</span></span>

 <span data-ttu-id="2a2e2-252">Puede incluir cualquier hello **absoluta** o **LocalResource** elemento pero no ambos.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-252">May include either hello **Absolute** or **LocalResource** element but not both.</span></span>  

|<span data-ttu-id="2a2e2-253">Elementos secundarios</span><span class="sxs-lookup"><span data-stu-id="2a2e2-253">Child Elements</span></span>|<span data-ttu-id="2a2e2-254">Descripción</span><span class="sxs-lookup"><span data-stu-id="2a2e2-254">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="2a2e2-255">**Absolute**</span><span class="sxs-lookup"><span data-stu-id="2a2e2-255">**Absolute**</span></span>|<span data-ttu-id="2a2e2-256">Hola toomonitor de directorio toohello de ruta de acceso absoluta.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-256">hello absolute path toohello directory toomonitor.</span></span> <span data-ttu-id="2a2e2-257">Hola siguientes atributos es necesario:</span><span class="sxs-lookup"><span data-stu-id="2a2e2-257">hello following attributes are required:</span></span><br /><br /> <span data-ttu-id="2a2e2-258">- **Ruta de acceso** -Hola toomonitor de directorio toohello de ruta de acceso absoluta.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-258">- **Path** - hello absolute path toohello directory toomonitor.</span></span><br /><br /> <span data-ttu-id="2a2e2-259">- **expandEnvironment**: configura si se expanden las variables de entorno en Path.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-259">- **expandEnvironment** - Configures whether environment variables in Path are expanded.</span></span>|  
|<span data-ttu-id="2a2e2-260">**LocalResource**</span><span class="sxs-lookup"><span data-stu-id="2a2e2-260">**LocalResource**</span></span>|<span data-ttu-id="2a2e2-261">Hola toomonitor de ruta de acceso relativa tooa recurso local.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-261">hello path relative tooa local resource toomonitor.</span></span> <span data-ttu-id="2a2e2-262">Los atributos necesarios son:</span><span class="sxs-lookup"><span data-stu-id="2a2e2-262">Required attributes are:</span></span><br /><br /> <span data-ttu-id="2a2e2-263">- **Nombre de** -Hola recurso local que contiene Hola directory toomonitor</span><span class="sxs-lookup"><span data-stu-id="2a2e2-263">- **Name** - hello local resource that contains hello directory toomonitor</span></span><br /><br /> <span data-ttu-id="2a2e2-264">- **relativePath** -Hola tooName relativa de ruta de acceso que contiene Hola directory toomonitor</span><span class="sxs-lookup"><span data-stu-id="2a2e2-264">- **relativePath** - hello path relative tooName that contains hello directory toomonitor</span></span>|  



## <a name="etwproviders-element"></a><span data-ttu-id="2a2e2-265">Elemento EtwProviders</span><span class="sxs-lookup"><span data-stu-id="2a2e2-265">EtwProviders Element</span></span>  
 <span data-ttu-id="2a2e2-266">*Árbol: Raíz - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders*</span><span class="sxs-lookup"><span data-stu-id="2a2e2-266">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders*</span></span>

 <span data-ttu-id="2a2e2-267">Configura la recopilación de eventos ETW en EventSource o el manifiesto de ETW en función de los proveedores.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-267">Configures collection of ETW events from EventSource and/or ETW Manifest based providers.</span></span>  

|<span data-ttu-id="2a2e2-268">Elementos secundarios</span><span class="sxs-lookup"><span data-stu-id="2a2e2-268">Child Elements</span></span>|<span data-ttu-id="2a2e2-269">Descripción</span><span class="sxs-lookup"><span data-stu-id="2a2e2-269">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="2a2e2-270">**EtwEventSourceProviderConfiguration**</span><span class="sxs-lookup"><span data-stu-id="2a2e2-270">**EtwEventSourceProviderConfiguration**</span></span>|<span data-ttu-id="2a2e2-271">Configura la recopilación de eventos generados a partir de la [clase EventSource](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx).</span><span class="sxs-lookup"><span data-stu-id="2a2e2-271">Configures collection of events generated from [EventSource Class](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx).</span></span> <span data-ttu-id="2a2e2-272">Atributo necesario:</span><span class="sxs-lookup"><span data-stu-id="2a2e2-272">Required attribute:</span></span><br /><br /> <span data-ttu-id="2a2e2-273">**proveedor de** -nombre de la clase hello de evento de EventSource Hola.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-273">**provider** - hello class name of hello EventSource event.</span></span><br /><br /> <span data-ttu-id="2a2e2-274">Los atributos opcionales son:</span><span class="sxs-lookup"><span data-stu-id="2a2e2-274">Optional attributes are:</span></span><br /><br /> <span data-ttu-id="2a2e2-275">- **scheduledTransferLogLevelFilter** -Hola cuenta de almacenamiento de tooyour tootransfer de nivel de gravedad mínimo.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-275">- **scheduledTransferLogLevelFilter** - hello minimum severity level tootransfer tooyour storage account.</span></span><br /><br /> <span data-ttu-id="2a2e2-276">- **scheduledTransferPeriod** -intervalo de saludo entre las transferencias programadas toostorage redondea toohello más cercano de minuto.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-276">- **scheduledTransferPeriod** - hello interval between scheduled transfers toostorage rounded up toohello nearest minute.</span></span> <span data-ttu-id="2a2e2-277">valor de Hello es un [XML "Tipo de datos de duración".](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span><span class="sxs-lookup"><span data-stu-id="2a2e2-277">hello value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span></span> |  
|<span data-ttu-id="2a2e2-278">**EtwManifestProviderConfiguration**</span><span class="sxs-lookup"><span data-stu-id="2a2e2-278">**EtwManifestProviderConfiguration**</span></span>|<span data-ttu-id="2a2e2-279">Atributo necesario:</span><span class="sxs-lookup"><span data-stu-id="2a2e2-279">Required attribute:</span></span><br /><br /> <span data-ttu-id="2a2e2-280">**proveedor** -Hola GUID del proveedor de eventos de Hola</span><span class="sxs-lookup"><span data-stu-id="2a2e2-280">**provider** - hello GUID of hello event provider</span></span><br /><br /> <span data-ttu-id="2a2e2-281">Los atributos opcionales son:</span><span class="sxs-lookup"><span data-stu-id="2a2e2-281">Optional attributes are:</span></span><br /><br /> <span data-ttu-id="2a2e2-282">- **scheduledTransferLogLevelFilter** -Hola cuenta de almacenamiento de tooyour tootransfer de nivel de gravedad mínimo.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-282">- **scheduledTransferLogLevelFilter** - hello minimum severity level tootransfer tooyour storage account.</span></span><br /><br /> <span data-ttu-id="2a2e2-283">- **scheduledTransferPeriod** -intervalo de saludo entre las transferencias programadas toostorage redondea toohello más cercano de minuto.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-283">- **scheduledTransferPeriod** - hello interval between scheduled transfers toostorage rounded up toohello nearest minute.</span></span> <span data-ttu-id="2a2e2-284">valor de Hello es un [XML "Tipo de datos de duración".](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span><span class="sxs-lookup"><span data-stu-id="2a2e2-284">hello value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span></span> |  



## <a name="etweventsourceproviderconfiguration-element"></a><span data-ttu-id="2a2e2-285">Elemento EtwEventSourceProviderConfiguration</span><span class="sxs-lookup"><span data-stu-id="2a2e2-285">EtwEventSourceProviderConfiguration Element</span></span>  
 <span data-ttu-id="2a2e2-286">*Árbol: Raíz - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders- EtwEventSourceProviderConfiguration*</span><span class="sxs-lookup"><span data-stu-id="2a2e2-286">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders- EtwEventSourceProviderConfiguration*</span></span>

 <span data-ttu-id="2a2e2-287">Configura la recopilación de eventos generados a partir de la [clase EventSource](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx).</span><span class="sxs-lookup"><span data-stu-id="2a2e2-287">Configures collection of events generated from [EventSource Class](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx).</span></span>  

|<span data-ttu-id="2a2e2-288">Elementos secundarios</span><span class="sxs-lookup"><span data-stu-id="2a2e2-288">Child Elements</span></span>|<span data-ttu-id="2a2e2-289">Descripción</span><span class="sxs-lookup"><span data-stu-id="2a2e2-289">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="2a2e2-290">**DefaultEvents**</span><span class="sxs-lookup"><span data-stu-id="2a2e2-290">**DefaultEvents**</span></span>|<span data-ttu-id="2a2e2-291">Atributo opcional:</span><span class="sxs-lookup"><span data-stu-id="2a2e2-291">Optional attribute:</span></span><br/><br/> <span data-ttu-id="2a2e2-292">**eventDestination** : hello nombre hello toostore Hola eventos de tabla en</span><span class="sxs-lookup"><span data-stu-id="2a2e2-292">**eventDestination** - hello name of hello table toostore hello events in</span></span>|  
|<span data-ttu-id="2a2e2-293">**Evento**</span><span class="sxs-lookup"><span data-stu-id="2a2e2-293">**Event**</span></span>|<span data-ttu-id="2a2e2-294">Atributo necesario:</span><span class="sxs-lookup"><span data-stu-id="2a2e2-294">Required attribute:</span></span><br /><br /> <span data-ttu-id="2a2e2-295">**Id. de** -Id. de Hola de evento Hola.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-295">**id** - hello id of hello event.</span></span><br /><br /> <span data-ttu-id="2a2e2-296">Atributo opcional:</span><span class="sxs-lookup"><span data-stu-id="2a2e2-296">Optional attribute:</span></span><br /><br /> <span data-ttu-id="2a2e2-297">**eventDestination** : hello nombre hello toostore Hola eventos de tabla en</span><span class="sxs-lookup"><span data-stu-id="2a2e2-297">**eventDestination** - hello name of hello table toostore hello events in</span></span>|  



## <a name="etwmanifestproviderconfiguration-element"></a><span data-ttu-id="2a2e2-298">Elemento EtwManifestProviderConfiguration</span><span class="sxs-lookup"><span data-stu-id="2a2e2-298">EtwManifestProviderConfiguration Element</span></span>  
 <span data-ttu-id="2a2e2-299">*Árbol: Raíz - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders - EtwManifestProviderConfiguration*</span><span class="sxs-lookup"><span data-stu-id="2a2e2-299">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders - EtwManifestProviderConfiguration*</span></span>

|<span data-ttu-id="2a2e2-300">Elementos secundarios</span><span class="sxs-lookup"><span data-stu-id="2a2e2-300">Child Elements</span></span>|<span data-ttu-id="2a2e2-301">Descripción</span><span class="sxs-lookup"><span data-stu-id="2a2e2-301">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="2a2e2-302">**DefaultEvents**</span><span class="sxs-lookup"><span data-stu-id="2a2e2-302">**DefaultEvents**</span></span>|<span data-ttu-id="2a2e2-303">Atributo opcional:</span><span class="sxs-lookup"><span data-stu-id="2a2e2-303">Optional attribute:</span></span><br /><br /> <span data-ttu-id="2a2e2-304">**eventDestination** : hello nombre hello toostore Hola eventos de tabla en</span><span class="sxs-lookup"><span data-stu-id="2a2e2-304">**eventDestination** - hello name of hello table toostore hello events in</span></span>|  
|<span data-ttu-id="2a2e2-305">**Evento**</span><span class="sxs-lookup"><span data-stu-id="2a2e2-305">**Event**</span></span>|<span data-ttu-id="2a2e2-306">Atributo necesario:</span><span class="sxs-lookup"><span data-stu-id="2a2e2-306">Required attribute:</span></span><br /><br /> <span data-ttu-id="2a2e2-307">**Id. de** -Id. de Hola de evento Hola.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-307">**id** - hello id of hello event.</span></span><br /><br /> <span data-ttu-id="2a2e2-308">Atributo opcional:</span><span class="sxs-lookup"><span data-stu-id="2a2e2-308">Optional attribute:</span></span><br /><br /> <span data-ttu-id="2a2e2-309">**eventDestination** : hello nombre hello toostore Hola eventos de tabla en</span><span class="sxs-lookup"><span data-stu-id="2a2e2-309">**eventDestination** - hello name of hello table toostore hello events in</span></span>|  



## <a name="metrics-element"></a><span data-ttu-id="2a2e2-310">Elemento Metrics</span><span class="sxs-lookup"><span data-stu-id="2a2e2-310">Metrics Element</span></span>  
 <span data-ttu-id="2a2e2-311">*Árbol: Raíz - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Metrics*</span><span class="sxs-lookup"><span data-stu-id="2a2e2-311">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Metrics*</span></span>

 <span data-ttu-id="2a2e2-312">Le permite toogenerate una tabla de contador de rendimiento que se optimiza para las consultas rápidas.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-312">Enables you toogenerate a performance counter table that is optimized for fast queries.</span></span> <span data-ttu-id="2a2e2-313">Cada contador de rendimiento que se define en hello **PerformanceCounters** elemento se almacena en la tabla de métricas de hello en la tabla de contador de rendimiento de toohello de adición.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-313">Each performance counter that is defined in hello **PerformanceCounters** element is stored in hello Metrics table in addition toohello Performance Counter table.</span></span>  

 <span data-ttu-id="2a2e2-314">Hola **resourceId** atributo es necesario.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-314">hello **resourceId** attribute is required.</span></span>  <span data-ttu-id="2a2e2-315">Hola Id. de recurso de máquina Virtual que va a implementar diagnósticos de Azure para hello.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-315">hello resource ID of hello Virtual Machine you are deploying Azure Diagnostics to.</span></span> <span data-ttu-id="2a2e2-316">Obtener hello **resourceID** de hello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2a2e2-316">Get hello **resourceID** from hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="2a2e2-317">Seleccione **Examinar** -> **Grupos de recursos** -> **<Nombre\>**.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-317">Select **Browse** -> **Resource Groups** -> **<Name\>**.</span></span> <span data-ttu-id="2a2e2-318">Haga clic en hello **propiedades** icono y copie el valor de Hola de hello **identificador** campo.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-318">Click hello **Properties** tile and copy hello value from hello **ID** field.</span></span>  

|<span data-ttu-id="2a2e2-319">Elementos secundarios</span><span class="sxs-lookup"><span data-stu-id="2a2e2-319">Child Elements</span></span>|<span data-ttu-id="2a2e2-320">Descripción</span><span class="sxs-lookup"><span data-stu-id="2a2e2-320">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="2a2e2-321">**MetricAggregation**</span><span class="sxs-lookup"><span data-stu-id="2a2e2-321">**MetricAggregation**</span></span>|<span data-ttu-id="2a2e2-322">Atributo necesario:</span><span class="sxs-lookup"><span data-stu-id="2a2e2-322">Required attribute:</span></span><br /><br /> <span data-ttu-id="2a2e2-323">**scheduledTransferPeriod** -intervalo de saludo entre las transferencias programadas toostorage redondea toohello más cercano de minuto.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-323">**scheduledTransferPeriod** - hello interval between scheduled transfers toostorage rounded up toohello nearest minute.</span></span> <span data-ttu-id="2a2e2-324">valor de Hello es un [XML "Tipo de datos de duración".](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span><span class="sxs-lookup"><span data-stu-id="2a2e2-324">hello value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span></span> |  



## <a name="performancecounters-element"></a><span data-ttu-id="2a2e2-325">Elemento PerformanceCounters</span><span class="sxs-lookup"><span data-stu-id="2a2e2-325">PerformanceCounters Element</span></span>  
 <span data-ttu-id="2a2e2-326">*Árbol: Raíz - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - PerformanceCounters*</span><span class="sxs-lookup"><span data-stu-id="2a2e2-326">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - PerformanceCounters*</span></span>

 <span data-ttu-id="2a2e2-327">Habilita la recopilación de Hola de contadores de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-327">Enables hello collection of performance counters.</span></span>  

 <span data-ttu-id="2a2e2-328">Atributo opcional:</span><span class="sxs-lookup"><span data-stu-id="2a2e2-328">Optional attribute:</span></span>  

 <span data-ttu-id="2a2e2-329">Atributo **scheduledTransferPeriod** opcional.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-329">Optional **scheduledTransferPeriod** attribute.</span></span> <span data-ttu-id="2a2e2-330">Consulte la explicación anterior.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-330">See explanation earlier.</span></span>

|<span data-ttu-id="2a2e2-331">Elemento secundario</span><span class="sxs-lookup"><span data-stu-id="2a2e2-331">Child Element</span></span>|<span data-ttu-id="2a2e2-332">Descripción</span><span class="sxs-lookup"><span data-stu-id="2a2e2-332">Description</span></span>|  
|-------------------|-----------------|  
|<span data-ttu-id="2a2e2-333">**PerformanceCounterConfiguration**</span><span class="sxs-lookup"><span data-stu-id="2a2e2-333">**PerformanceCounterConfiguration**</span></span>|<span data-ttu-id="2a2e2-334">Hola siguientes atributos es necesario:</span><span class="sxs-lookup"><span data-stu-id="2a2e2-334">hello following attributes are required:</span></span><br /><br /> <span data-ttu-id="2a2e2-335">- **counterSpecifier** : hello nombre de contador de rendimiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-335">- **counterSpecifier** - hello name of hello performance counter.</span></span> <span data-ttu-id="2a2e2-336">Por ejemplo: `\Processor(_Total)\% Processor Time`.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-336">For example, `\Processor(_Total)\% Processor Time`.</span></span> <span data-ttu-id="2a2e2-337">tooget una lista de rendimiento de los contadores en el host, ejecute el comando de hello `typeperf`.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-337">tooget a list of performance counters on your host, run hello command `typeperf`.</span></span><br /><br /> <span data-ttu-id="2a2e2-338">- **sampleRate** -¿con qué frecuencia hello contador debe realizarse el muestreo.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-338">- **sampleRate** - How often hello counter should be sampled.</span></span><br /><br /> <span data-ttu-id="2a2e2-339">Atributo opcional:</span><span class="sxs-lookup"><span data-stu-id="2a2e2-339">Optional attribute:</span></span><br /><br /> <span data-ttu-id="2a2e2-340">**unidad** -Hola unidad de medida de contador de Hola.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-340">**unit** - hello unit of measure of hello counter.</span></span>|  




## <a name="windowseventlog-element"></a><span data-ttu-id="2a2e2-341">Elemento WindowsEventLog</span><span class="sxs-lookup"><span data-stu-id="2a2e2-341">WindowsEventLog Element</span></span>
 <span data-ttu-id="2a2e2-342">*Árbol: Raíz - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - WindowsEventLog*</span><span class="sxs-lookup"><span data-stu-id="2a2e2-342">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - WindowsEventLog*</span></span>
 
 <span data-ttu-id="2a2e2-343">Habilita la recopilación de Hola de registros de eventos de Windows.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-343">Enables hello collection of Windows Event Logs.</span></span>  

 <span data-ttu-id="2a2e2-344">Atributo **scheduledTransferPeriod** opcional.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-344">Optional **scheduledTransferPeriod** attribute.</span></span> <span data-ttu-id="2a2e2-345">Consulte la explicación anterior.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-345">See explanation  earlier.</span></span>  

|<span data-ttu-id="2a2e2-346">Elemento secundario</span><span class="sxs-lookup"><span data-stu-id="2a2e2-346">Child Element</span></span>|<span data-ttu-id="2a2e2-347">Descripción</span><span class="sxs-lookup"><span data-stu-id="2a2e2-347">Description</span></span>|  
|-------------------|-----------------|  
|<span data-ttu-id="2a2e2-348">**DataSource**</span><span class="sxs-lookup"><span data-stu-id="2a2e2-348">**DataSource**</span></span>|<span data-ttu-id="2a2e2-349">Hola toocollect de registros de eventos de Windows.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-349">hello Windows Event logs toocollect.</span></span> <span data-ttu-id="2a2e2-350">Atributo necesario:</span><span class="sxs-lookup"><span data-stu-id="2a2e2-350">Required attribute:</span></span><br /><br /> <span data-ttu-id="2a2e2-351">**nombre de** -recopilados de consulta de XPath de Hola que describe toobe de eventos de windows hello.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-351">**name** - hello XPath query describing hello windows events toobe collected.</span></span> <span data-ttu-id="2a2e2-352">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="2a2e2-352">For example:</span></span><br /><br /> `Application!*[System[(Level <=3)]], System!*[System[(Level <=3)]], System!*[System[Provider[@Name='Microsoft Antimalware']]], Security!*[System[(Level <= 3)]`<br /><br /> <span data-ttu-id="2a2e2-353">toocollect todos los eventos, especifique "*"</span><span class="sxs-lookup"><span data-stu-id="2a2e2-353">toocollect all events, specify "*"</span></span>|  




## <a name="logs-element"></a><span data-ttu-id="2a2e2-354">Elemento Logs</span><span class="sxs-lookup"><span data-stu-id="2a2e2-354">Logs Element</span></span>  
 <span data-ttu-id="2a2e2-355">*Árbol: Raíz - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Logs*</span><span class="sxs-lookup"><span data-stu-id="2a2e2-355">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Logs*</span></span>

 <span data-ttu-id="2a2e2-356">Se presenta en la versión 1.0 y 1.1.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-356">Present in version 1.0 and 1.1.</span></span> <span data-ttu-id="2a2e2-357">Falta en 1.2.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-357">Missing in 1.2.</span></span> <span data-ttu-id="2a2e2-358">Se ha agregado en 1.3.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-358">Added back in 1.3.</span></span>  

 <span data-ttu-id="2a2e2-359">Define la configuración de búfer de Hola para los registros básicos de Azure.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-359">Defines hello buffer configuration for basic Azure logs.</span></span>  

|<span data-ttu-id="2a2e2-360">Atributo</span><span class="sxs-lookup"><span data-stu-id="2a2e2-360">Attribute</span></span>|<span data-ttu-id="2a2e2-361">Tipo</span><span class="sxs-lookup"><span data-stu-id="2a2e2-361">Type</span></span>|<span data-ttu-id="2a2e2-362">Descripción</span><span class="sxs-lookup"><span data-stu-id="2a2e2-362">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="2a2e2-363">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="2a2e2-363">**bufferQuotaInMB**</span></span>|<span data-ttu-id="2a2e2-364">**unsignedInt**</span><span class="sxs-lookup"><span data-stu-id="2a2e2-364">**unsignedInt**</span></span>|<span data-ttu-id="2a2e2-365">Opcional.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-365">Optional.</span></span> <span data-ttu-id="2a2e2-366">Especifica Hola cantidad máxima de almacenamiento del sistema de archivos que está disponible para hello especificado datos.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-366">Specifies hello maximum amount of file system storage that is available for hello specified data.</span></span><br /><br /> <span data-ttu-id="2a2e2-367">Hola predeterminado es 0.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-367">hello default is 0.</span></span>|  
|<span data-ttu-id="2a2e2-368">**scheduledTransferLogLevelFilterr**</span><span class="sxs-lookup"><span data-stu-id="2a2e2-368">**scheduledTransferLogLevelFilterr**</span></span>|<span data-ttu-id="2a2e2-369">**cadena**</span><span class="sxs-lookup"><span data-stu-id="2a2e2-369">**string**</span></span>|<span data-ttu-id="2a2e2-370">Opcional.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-370">Optional.</span></span> <span data-ttu-id="2a2e2-371">Especifica el nivel de gravedad mínimo de Hola para las entradas de registro que se transfieren.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-371">Specifies hello minimum severity level for log entries that are transferred.</span></span> <span data-ttu-id="2a2e2-372">es el valor predeterminado de Hello **Undefined**, que transfiere todos los registros.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-372">hello default value is **Undefined**, which transfers all logs.</span></span> <span data-ttu-id="2a2e2-373">Otros valores posibles (en orden de la mayoría de la información tooleast) son **detallado**, **información**, **advertencia**, **Error**y **Crítica**.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-373">Other possible values (in order of most tooleast information) are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span></span>|  
|<span data-ttu-id="2a2e2-374">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="2a2e2-374">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="2a2e2-375">**duration**</span><span class="sxs-lookup"><span data-stu-id="2a2e2-375">**duration**</span></span>|<span data-ttu-id="2a2e2-376">Opcional.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-376">Optional.</span></span> <span data-ttu-id="2a2e2-377">Especifica el intervalo de hello entre las transferencias programadas de datos, redondeado hasta toohello más cercano de minuto.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-377">Specifies hello interval between scheduled transfers of data, rounded up toohello nearest minute.</span></span><br /><br /> <span data-ttu-id="2a2e2-378">valor predeterminado de Hello es PT0S.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-378">hello default is PT0S.</span></span>|  
|<span data-ttu-id="2a2e2-379">**sinks**: agregado en 1.5</span><span class="sxs-lookup"><span data-stu-id="2a2e2-379">**sinks** Added in 1.5</span></span>|<span data-ttu-id="2a2e2-380">**cadena**</span><span class="sxs-lookup"><span data-stu-id="2a2e2-380">**string**</span></span>|<span data-ttu-id="2a2e2-381">Opcional.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-381">Optional.</span></span> <span data-ttu-id="2a2e2-382">Puntos tooa receptor ubicación tooalso enviar datos de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-382">Points tooa sink location tooalso send diagnostic data.</span></span> <span data-ttu-id="2a2e2-383">Por ejemplo, Application Insights.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-383">For example, Application Insights.</span></span>|  

## <a name="dockersources"></a><span data-ttu-id="2a2e2-384">DockerSources</span><span class="sxs-lookup"><span data-stu-id="2a2e2-384">DockerSources</span></span>
 <span data-ttu-id="2a2e2-385">*Árbol: Raíz - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - DockerSources*</span><span class="sxs-lookup"><span data-stu-id="2a2e2-385">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - DockerSources*</span></span>

 <span data-ttu-id="2a2e2-386">Se agregó en la versión 1.9.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-386">Added in 1.9.</span></span>

|<span data-ttu-id="2a2e2-387">Nombre del elemento</span><span class="sxs-lookup"><span data-stu-id="2a2e2-387">Element Name</span></span>|<span data-ttu-id="2a2e2-388">Descripción</span><span class="sxs-lookup"><span data-stu-id="2a2e2-388">Description</span></span>|  
|------------------|-----------------|  
|<span data-ttu-id="2a2e2-389">**Stats**</span><span class="sxs-lookup"><span data-stu-id="2a2e2-389">**Stats**</span></span>|<span data-ttu-id="2a2e2-390">Indica el sistema de hello toocollect estadísticas para los contenedores de Docker</span><span class="sxs-lookup"><span data-stu-id="2a2e2-390">Tells hello system toocollect stats for Docker containers</span></span>|  

## <a name="sinksconfig-element"></a><span data-ttu-id="2a2e2-391">Elemento SinksConfig</span><span class="sxs-lookup"><span data-stu-id="2a2e2-391">SinksConfig Element</span></span>  
 <span data-ttu-id="2a2e2-392">*Árbol: Raíz - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig*</span><span class="sxs-lookup"><span data-stu-id="2a2e2-392">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig*</span></span>

 <span data-ttu-id="2a2e2-393">Una lista de ubicaciones toosend datos tooand Hola configuración de diagnóstico asociado con esas ubicaciones.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-393">A list of locations toosend diagnostics data tooand hello configuration associated with those locations.</span></span>  

|<span data-ttu-id="2a2e2-394">Nombre del elemento</span><span class="sxs-lookup"><span data-stu-id="2a2e2-394">Element Name</span></span>|<span data-ttu-id="2a2e2-395">Descripción</span><span class="sxs-lookup"><span data-stu-id="2a2e2-395">Description</span></span>|  
|------------------|-----------------|  
|<span data-ttu-id="2a2e2-396">**Sink**</span><span class="sxs-lookup"><span data-stu-id="2a2e2-396">**Sink**</span></span>|<span data-ttu-id="2a2e2-397">Consulte la descripción en cualquier parte de esta página.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-397">See description elsewhere on this page.</span></span>|  

## <a name="sink-element"></a><span data-ttu-id="2a2e2-398">Elemento Sink</span><span class="sxs-lookup"><span data-stu-id="2a2e2-398">Sink Element</span></span>
 <span data-ttu-id="2a2e2-399">*Árbol: Raíz - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink*</span><span class="sxs-lookup"><span data-stu-id="2a2e2-399">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink*</span></span>

 <span data-ttu-id="2a2e2-400">Agregado en la versión 1.5.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-400">Added in version 1.5.</span></span>  

 <span data-ttu-id="2a2e2-401">Define ubicaciones toosend datos de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-401">Defines locations toosend diagnostic data to.</span></span> <span data-ttu-id="2a2e2-402">Por ejemplo, hello servicio Application Insights.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-402">For example, hello Application Insights service.</span></span>  

|<span data-ttu-id="2a2e2-403">Atributo</span><span class="sxs-lookup"><span data-stu-id="2a2e2-403">Attribute</span></span>|<span data-ttu-id="2a2e2-404">Tipo</span><span class="sxs-lookup"><span data-stu-id="2a2e2-404">Type</span></span>|<span data-ttu-id="2a2e2-405">Descripción</span><span class="sxs-lookup"><span data-stu-id="2a2e2-405">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="2a2e2-406">**name**</span><span class="sxs-lookup"><span data-stu-id="2a2e2-406">**name**</span></span>|<span data-ttu-id="2a2e2-407">cadena</span><span class="sxs-lookup"><span data-stu-id="2a2e2-407">string</span></span>|<span data-ttu-id="2a2e2-408">Sinkname de hello identificación de cadena.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-408">A string identifying hello sinkname.</span></span>|  

|<span data-ttu-id="2a2e2-409">Elemento</span><span class="sxs-lookup"><span data-stu-id="2a2e2-409">Element</span></span>|<span data-ttu-id="2a2e2-410">Escriba</span><span class="sxs-lookup"><span data-stu-id="2a2e2-410">Type</span></span>|<span data-ttu-id="2a2e2-411">Descripción</span><span class="sxs-lookup"><span data-stu-id="2a2e2-411">Description</span></span>|  
|-------------|----------|-----------------|  
|<span data-ttu-id="2a2e2-412">**Application Insights**</span><span class="sxs-lookup"><span data-stu-id="2a2e2-412">**Application Insights**</span></span>|<span data-ttu-id="2a2e2-413">cadena</span><span class="sxs-lookup"><span data-stu-id="2a2e2-413">string</span></span>|<span data-ttu-id="2a2e2-414">Usar solo al enviar datos tooApplication visión.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-414">Used only when sending data tooApplication Insights.</span></span> <span data-ttu-id="2a2e2-415">Contener Hola clave de instrumentación para una cuenta activa de Application Insights que tienen acceso a.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-415">Contain hello Instrumentation Key for an active Application Insights account that you have access to.</span></span>|  
|<span data-ttu-id="2a2e2-416">**Channels**</span><span class="sxs-lookup"><span data-stu-id="2a2e2-416">**Channels**</span></span>|<span data-ttu-id="2a2e2-417">cadena</span><span class="sxs-lookup"><span data-stu-id="2a2e2-417">string</span></span>|<span data-ttu-id="2a2e2-418">Uno para cada filtrado adicional transmitido</span><span class="sxs-lookup"><span data-stu-id="2a2e2-418">One for each additional filtering that stream that you</span></span>|  

## <a name="channels-element"></a><span data-ttu-id="2a2e2-419">Elemento Channels</span><span class="sxs-lookup"><span data-stu-id="2a2e2-419">Channels Element</span></span>  
 <span data-ttu-id="2a2e2-420">*Árbol: Raíz - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink - Channels*</span><span class="sxs-lookup"><span data-stu-id="2a2e2-420">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink - Channels*</span></span>

 <span data-ttu-id="2a2e2-421">Agregado en la versión 1.5.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-421">Added in version 1.5.</span></span>  

 <span data-ttu-id="2a2e2-422">Define los filtros para los flujos de datos de registro que se pasan a través de un receptor.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-422">Defines filters for streams of log data passing through a sink.</span></span>  

|<span data-ttu-id="2a2e2-423">Elemento</span><span class="sxs-lookup"><span data-stu-id="2a2e2-423">Element</span></span>|<span data-ttu-id="2a2e2-424">Escriba</span><span class="sxs-lookup"><span data-stu-id="2a2e2-424">Type</span></span>|<span data-ttu-id="2a2e2-425">Descripción</span><span class="sxs-lookup"><span data-stu-id="2a2e2-425">Description</span></span>|  
|-------------|----------|-----------------|  
|<span data-ttu-id="2a2e2-426">**Channel**</span><span class="sxs-lookup"><span data-stu-id="2a2e2-426">**Channel**</span></span>|<span data-ttu-id="2a2e2-427">string</span><span class="sxs-lookup"><span data-stu-id="2a2e2-427">string</span></span>|<span data-ttu-id="2a2e2-428">Consulte la descripción en cualquier parte de esta página.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-428">See description elsewhere on this page.</span></span>|  

## <a name="channel-element"></a><span data-ttu-id="2a2e2-429">Elemento Channel</span><span class="sxs-lookup"><span data-stu-id="2a2e2-429">Channel Element</span></span>
 <span data-ttu-id="2a2e2-430">*Árbol: Raíz - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink - Channels - Channel*</span><span class="sxs-lookup"><span data-stu-id="2a2e2-430">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink - Channels - Channel*</span></span>

 <span data-ttu-id="2a2e2-431">Agregado en la versión 1.5.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-431">Added in version 1.5.</span></span>  

 <span data-ttu-id="2a2e2-432">Define ubicaciones toosend datos de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-432">Defines locations toosend diagnostic data to.</span></span> <span data-ttu-id="2a2e2-433">Por ejemplo, hello servicio Application Insights.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-433">For example, hello Application Insights service.</span></span>  

|<span data-ttu-id="2a2e2-434">Attributes</span><span class="sxs-lookup"><span data-stu-id="2a2e2-434">Attributes</span></span>|<span data-ttu-id="2a2e2-435">Escriba</span><span class="sxs-lookup"><span data-stu-id="2a2e2-435">Type</span></span>|<span data-ttu-id="2a2e2-436">Descripción</span><span class="sxs-lookup"><span data-stu-id="2a2e2-436">Description</span></span>|  
|----------------|----------|-----------------|  
|<span data-ttu-id="2a2e2-437">**logLevel**</span><span class="sxs-lookup"><span data-stu-id="2a2e2-437">**logLevel**</span></span>|<span data-ttu-id="2a2e2-438">**cadena**</span><span class="sxs-lookup"><span data-stu-id="2a2e2-438">**string**</span></span>|<span data-ttu-id="2a2e2-439">Especifica el nivel de gravedad mínimo de Hola para las entradas de registro que se transfieren.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-439">Specifies hello minimum severity level for log entries that are transferred.</span></span> <span data-ttu-id="2a2e2-440">es el valor predeterminado de Hello **Undefined**, que transfiere todos los registros.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-440">hello default value is **Undefined**, which transfers all logs.</span></span> <span data-ttu-id="2a2e2-441">Otros valores posibles (en orden de la mayoría de la información tooleast) son **detallado**, **información**, **advertencia**, **Error**y **Crítica**.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-441">Other possible values (in order of most tooleast information) are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span></span>|  
|<span data-ttu-id="2a2e2-442">**name**</span><span class="sxs-lookup"><span data-stu-id="2a2e2-442">**name**</span></span>|<span data-ttu-id="2a2e2-443">**cadena**</span><span class="sxs-lookup"><span data-stu-id="2a2e2-443">**string**</span></span>|<span data-ttu-id="2a2e2-444">Un nombre único de hello canal toorefer a</span><span class="sxs-lookup"><span data-stu-id="2a2e2-444">A unique name of hello channel toorefer to</span></span>|  


## <a name="privateconfig-element"></a><span data-ttu-id="2a2e2-445">Elemento PrivateConfig</span><span class="sxs-lookup"><span data-stu-id="2a2e2-445">PrivateConfig Element</span></span> 
 <span data-ttu-id="2a2e2-446">*Árbol: Raíz - DiagnosticsConfiguration - PrivateConfig*</span><span class="sxs-lookup"><span data-stu-id="2a2e2-446">*Tree: Root - DiagnosticsConfiguration - PrivateConfig*</span></span>

 <span data-ttu-id="2a2e2-447">Agregado en la versión 1.3.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-447">Added in version 1.3.</span></span>  

 <span data-ttu-id="2a2e2-448">Opcional</span><span class="sxs-lookup"><span data-stu-id="2a2e2-448">Optional</span></span>  

 <span data-ttu-id="2a2e2-449">Almacena información privada de hello de la cuenta de almacenamiento de hello (nombre, clave y el extremo).</span><span class="sxs-lookup"><span data-stu-id="2a2e2-449">Stores hello private details of hello storage account (name, key, and endpoint).</span></span> <span data-ttu-id="2a2e2-450">Esta información se envía la máquina virtual de toohello, pero no se puede recuperar del mismo.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-450">This information is sent toohello virtual machine, but cannot be retrieved from it.</span></span>  

|<span data-ttu-id="2a2e2-451">Elementos secundarios</span><span class="sxs-lookup"><span data-stu-id="2a2e2-451">Child Elements</span></span>|<span data-ttu-id="2a2e2-452">Descripción</span><span class="sxs-lookup"><span data-stu-id="2a2e2-452">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="2a2e2-453">**StorageAccount**</span><span class="sxs-lookup"><span data-stu-id="2a2e2-453">**StorageAccount**</span></span>|<span data-ttu-id="2a2e2-454">Hola toouse de cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-454">hello storage account toouse.</span></span> <span data-ttu-id="2a2e2-455">Hola siguientes atributos es necesario</span><span class="sxs-lookup"><span data-stu-id="2a2e2-455">hello following attributes are required</span></span><br /><br /> <span data-ttu-id="2a2e2-456">- **nombre** : hello nombre de la cuenta de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-456">- **name** - hello name of hello storage account.</span></span><br /><br /> <span data-ttu-id="2a2e2-457">- **clave** : hello clave toohello cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-457">- **key** - hello key toohello storage account.</span></span><br /><br /> <span data-ttu-id="2a2e2-458">- **punto de conexión** -tooaccess de punto de conexión de Hola Hola cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-458">- **endpoint** - hello endpoint tooaccess hello storage account.</span></span> <br /><br /> <span data-ttu-id="2a2e2-459">-**sasToken** (agregado 1.8.1)-puede especificar un token SAS en lugar de una clave de cuenta de almacenamiento en la configuración privada de Hola. Si se proporciona, se omite la clave de cuenta de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-459">-**sasToken** (added 1.8.1)- You can specify an SAS token instead of a storage account key in hello private config. If provided, hello storage account key is ignored.</span></span> <br /><span data-ttu-id="2a2e2-460">Requisitos para saludo del Token de SAS:</span><span class="sxs-lookup"><span data-stu-id="2a2e2-460">Requirements for hello SAS Token:</span></span> <br /><span data-ttu-id="2a2e2-461">- Solo admite el token de SAS de la cuenta.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-461">- Supports account SAS token only</span></span> <br /><span data-ttu-id="2a2e2-462">Se requieren los tipos de servicio - *b* y *t*.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-462">- *b*, *t* service types are required.</span></span> <br /> <span data-ttu-id="2a2e2-463">Se requieren los permisos - *a*, *c*, *u* y *w*.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-463">- *a*, *c*, *u*, *w* permissions are required.</span></span> <br /> <span data-ttu-id="2a2e2-464">Se requieren los tipos de recursos - *c* y *o*.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-464">- *c*, *o* resource types are required.</span></span> <br /> <span data-ttu-id="2a2e2-465">-Admite sólo protocolo de hello HTTPS</span><span class="sxs-lookup"><span data-stu-id="2a2e2-465">- Supports hello HTTPS protocol only</span></span> <br /> <span data-ttu-id="2a2e2-466">- La hora de inicio y de expiración debe ser válida.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-466">- Start and expiry time must be valid.</span></span>|  


## <a name="isenabled-element"></a><span data-ttu-id="2a2e2-467">Elemento IsEnabled</span><span class="sxs-lookup"><span data-stu-id="2a2e2-467">IsEnabled Element</span></span>  
 <span data-ttu-id="2a2e2-468">*Árbol: Raíz - DiagnosticsConfiguration - IsEnabled*</span><span class="sxs-lookup"><span data-stu-id="2a2e2-468">*Tree: Root - DiagnosticsConfiguration - IsEnabled*</span></span>

 <span data-ttu-id="2a2e2-469">Booleano.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-469">Boolean.</span></span> <span data-ttu-id="2a2e2-470">Use `true` tooenable diagnósticos de Hola o `false` diagnóstico de hello toodisable.</span><span class="sxs-lookup"><span data-stu-id="2a2e2-470">Use `true` tooenable hello diagnostics or `false` toodisable hello diagnostics.</span></span>
