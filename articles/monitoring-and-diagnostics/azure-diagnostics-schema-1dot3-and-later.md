---
title: "Esquema de configuración de la versión 1.3 y posterior de la extensión Azure Diagnostics | Microsoft Docs"
description: "La versión 1.3 y posterior del esquema de Azure Diagnostics se incluye como parte de Microsoft Azure SDK 2.4 y posterior."
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
ms.openlocfilehash: 0d814825fb08452238a254ccd30bde230380c74c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="azure-diagnostics-13-and-later-configuration-schema"></a><span data-ttu-id="7b511-103">Esquema de configuración de Azure Diagnostics 1.3 y posterior</span><span class="sxs-lookup"><span data-stu-id="7b511-103">Azure Diagnostics 1.3 and later configuration schema</span></span>
> [!NOTE]
> <span data-ttu-id="7b511-104">La extensión Azure Diagnostics es el componente que se usa para recopilar los contadores de rendimiento y otras estadísticas de los siguientes recursos:</span><span class="sxs-lookup"><span data-stu-id="7b511-104">The Azure Diagnostics extension is the component used to collect performance counters and other statistics from:</span></span>
> - <span data-ttu-id="7b511-105">Máquinas virtuales de Azure</span><span class="sxs-lookup"><span data-stu-id="7b511-105">Azure Virtual Machines</span></span> 
> - <span data-ttu-id="7b511-106">Conjuntos de escalado de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="7b511-106">Virtual Machine Scale Sets</span></span>
> - <span data-ttu-id="7b511-107">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="7b511-107">Service Fabric</span></span> 
> - <span data-ttu-id="7b511-108">Cloud Services</span><span class="sxs-lookup"><span data-stu-id="7b511-108">Cloud Services</span></span> 
> - <span data-ttu-id="7b511-109">Grupos de seguridad de red</span><span class="sxs-lookup"><span data-stu-id="7b511-109">Network Security Groups</span></span>
> 
> <span data-ttu-id="7b511-110">Esta página solo es pertinente si está usando uno de estos servicios.</span><span class="sxs-lookup"><span data-stu-id="7b511-110">This page is only relevant if you are using one of these services.</span></span>

<span data-ttu-id="7b511-111">Esta página es válida para las versiones 1.3 y posterior (Azure SDK 2.4 y posterior).</span><span class="sxs-lookup"><span data-stu-id="7b511-111">This page is valid for versions 1.3 and newer (Azure SDK 2.4 and newer).</span></span> <span data-ttu-id="7b511-112">Las secciones de configuración más recientes incluyen comentarios para mostrar en qué versión se agregaron.</span><span class="sxs-lookup"><span data-stu-id="7b511-112">Newer configuration sections are commented to show in what version they were added.</span></span>  

<span data-ttu-id="7b511-113">El archivo de configuración descrito en este artículo se usa para establecer la configuración de diagnóstico al iniciar el monitor de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="7b511-113">The configuration file described here is used to set diagnostic configuration settings when the diagnostics monitor starts.</span></span>  

<span data-ttu-id="7b511-114">La extensión se usa junto con otros productos de diagnósticos de Microsoft, como Azure Monitor, Application Insights y Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="7b511-114">The extension is used in conjunction with other Microsoft diagnostics products like Azure Monitor, Application Insights, and Log Analytics.</span></span>



<span data-ttu-id="7b511-115">Descargue la definición del esquema del archivo de configuración público ejecutando el comando de PowerShell siguiente:</span><span class="sxs-lookup"><span data-stu-id="7b511-115">Download the public configuration file schema definition by executing the following PowerShell command:</span></span>  

```powershell  
(Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File –Encoding utf8 -FilePath 'C:\temp\WadConfig.xsd'  
```  

<span data-ttu-id="7b511-116">Para obtener información sobre Azure Diagnostics, consulte [este artículo sobre dicha extensión](azure-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="7b511-116">For more information about using Azure Diagnostics, see [Azure Diagnostics Extension](azure-diagnostics.md).</span></span>  

## <a name="example-of-the-diagnostics-configuration-file"></a><span data-ttu-id="7b511-117">Ejemplo del archivo de configuración de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="7b511-117">Example of the diagnostics configuration file</span></span>  
 <span data-ttu-id="7b511-118">En el ejemplo siguiente se muestra un archivo de configuración de diagnóstico típico:</span><span class="sxs-lookup"><span data-stu-id="7b511-118">The following example shows a typical diagnostics configuration file:</span></span>  

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

<span data-ttu-id="7b511-119">Este es el equivalente JSON del archivo de configuración XML anterior.</span><span class="sxs-lookup"><span data-stu-id="7b511-119">JSON equivalent of the previous XML configuration file.</span></span> 

<span data-ttu-id="7b511-120">PublicConfig y PrivateConfig están separados porque en la mayoría de los casos de uso de JSON se pasan como variables distintas.</span><span class="sxs-lookup"><span data-stu-id="7b511-120">The PublicConfig and PrivateConfig are separated because in most json usage cases, they are passed as different variables.</span></span> <span data-ttu-id="7b511-121">En estos casos se incluyen plantillas de Resource Manager, conjuntos de escalado de máquinas virtuales, PowerShell y Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7b511-121">These cases include Resource Manager templates, Virtual Machine Scale set PowerShell, and Visual Studio.</span></span> 

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

## <a name="reading-this-page"></a><span data-ttu-id="7b511-122">Lectura de esta página</span><span class="sxs-lookup"><span data-stu-id="7b511-122">Reading this page</span></span>  
 <span data-ttu-id="7b511-123">Las etiquetas siguientes se encuentran aproximadamente en el orden mostrado en el ejemplo anterior.</span><span class="sxs-lookup"><span data-stu-id="7b511-123">The tags following are roughly in order shown in the preceding example.</span></span>  <span data-ttu-id="7b511-124">Si no ve una descripción completa donde la espera, busque en la página el elemento o atributo.</span><span class="sxs-lookup"><span data-stu-id="7b511-124">If you don't see a full description where you expect it, search the page for the element or attribute.</span></span>  

## <a name="common-attribute-types"></a><span data-ttu-id="7b511-125">Tipos de atributos comunes</span><span class="sxs-lookup"><span data-stu-id="7b511-125">Common Attribute Types</span></span>  
 <span data-ttu-id="7b511-126">El atributo **scheduledTransferPeriod** aparece en varios elementos.</span><span class="sxs-lookup"><span data-stu-id="7b511-126">**scheduledTransferPeriod** attribute appears in several elements.</span></span> <span data-ttu-id="7b511-127">Es el intervalo entre las transferencias programadas en el almacenamiento, redondeado al minuto más cercano.</span><span class="sxs-lookup"><span data-stu-id="7b511-127">It is the interval between scheduled transfers to storage rounded up to the nearest minute.</span></span> <span data-ttu-id="7b511-128">El valor es un [“tipo de datos de duración” XML](http://www.w3schools.com/schema/schema_dtypes_date.asp).</span><span class="sxs-lookup"><span data-stu-id="7b511-128">The value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span></span>


## <a name="diagnosticsconfiguration-element"></a><span data-ttu-id="7b511-129">Elemento DiagnosticsConfiguration</span><span class="sxs-lookup"><span data-stu-id="7b511-129">DiagnosticsConfiguration Element</span></span>  
 <span data-ttu-id="7b511-130">*Árbol: Raíz - DiagnosticsConfiguration*</span><span class="sxs-lookup"><span data-stu-id="7b511-130">*Tree: Root - DiagnosticsConfiguration*</span></span>

<span data-ttu-id="7b511-131">Agregado en la versión 1.3.</span><span class="sxs-lookup"><span data-stu-id="7b511-131">Added in version 1.3.</span></span>  

<span data-ttu-id="7b511-132">Elemento de nivel superior del archivo de configuración de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="7b511-132">The top-level element of the diagnostics configuration file.</span></span>  

<span data-ttu-id="7b511-133">**Atributo**: xmlns - El espacio de nombres XML del archivo de configuración de diagnóstico es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="7b511-133">**Attribute**  xmlns - The XML namespace for the diagnostics configuration file is:</span></span>  
<span data-ttu-id="7b511-134">http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration</span><span class="sxs-lookup"><span data-stu-id="7b511-134">http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration</span></span>  


|<span data-ttu-id="7b511-135">Elementos secundarios</span><span class="sxs-lookup"><span data-stu-id="7b511-135">Child Elements</span></span>|<span data-ttu-id="7b511-136">Descripción</span><span class="sxs-lookup"><span data-stu-id="7b511-136">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="7b511-137">**PublicConfig**</span><span class="sxs-lookup"><span data-stu-id="7b511-137">**PublicConfig**</span></span>|<span data-ttu-id="7b511-138">Obligatorio.</span><span class="sxs-lookup"><span data-stu-id="7b511-138">Required.</span></span> <span data-ttu-id="7b511-139">Consulte la descripción en cualquier parte de esta página.</span><span class="sxs-lookup"><span data-stu-id="7b511-139">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="7b511-140">**PrivateConfig**</span><span class="sxs-lookup"><span data-stu-id="7b511-140">**PrivateConfig**</span></span>|<span data-ttu-id="7b511-141">Opcional.</span><span class="sxs-lookup"><span data-stu-id="7b511-141">Optional.</span></span> <span data-ttu-id="7b511-142">Consulte la descripción en cualquier parte de esta página.</span><span class="sxs-lookup"><span data-stu-id="7b511-142">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="7b511-143">**IsEnabled**</span><span class="sxs-lookup"><span data-stu-id="7b511-143">**IsEnabled**</span></span>|<span data-ttu-id="7b511-144">Booleano.</span><span class="sxs-lookup"><span data-stu-id="7b511-144">Boolean.</span></span> <span data-ttu-id="7b511-145">Consulte la descripción en cualquier parte de esta página.</span><span class="sxs-lookup"><span data-stu-id="7b511-145">See description elsewhere on this page.</span></span>|  

## <a name="publicconfig-element"></a><span data-ttu-id="7b511-146">Elemento PublicConfig</span><span class="sxs-lookup"><span data-stu-id="7b511-146">PublicConfig Element</span></span>  
 <span data-ttu-id="7b511-147">*Árbol: Raíz - DiagnosticsConfiguration - PublicConfig*</span><span class="sxs-lookup"><span data-stu-id="7b511-147">*Tree: Root - DiagnosticsConfiguration - PublicConfig*</span></span>

 <span data-ttu-id="7b511-148">Describe la configuración de diagnóstico pública.</span><span class="sxs-lookup"><span data-stu-id="7b511-148">Describes the public diagnostics configuration.</span></span>  

|<span data-ttu-id="7b511-149">Elementos secundarios</span><span class="sxs-lookup"><span data-stu-id="7b511-149">Child Elements</span></span>|<span data-ttu-id="7b511-150">Descripción</span><span class="sxs-lookup"><span data-stu-id="7b511-150">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="7b511-151">**WadCfg**</span><span class="sxs-lookup"><span data-stu-id="7b511-151">**WadCfg**</span></span>|<span data-ttu-id="7b511-152">Obligatorio.</span><span class="sxs-lookup"><span data-stu-id="7b511-152">Required.</span></span> <span data-ttu-id="7b511-153">Consulte la descripción en cualquier parte de esta página.</span><span class="sxs-lookup"><span data-stu-id="7b511-153">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="7b511-154">**StorageAccount**</span><span class="sxs-lookup"><span data-stu-id="7b511-154">**StorageAccount**</span></span>|<span data-ttu-id="7b511-155">El nombre de la cuenta de Azure Storage en la que se van a almacenar los datos.</span><span class="sxs-lookup"><span data-stu-id="7b511-155">The name of the Azure Storage account to store the data in.</span></span> <span data-ttu-id="7b511-156">También se puede especificar como un parámetro al ejecutar el cmdlet Set-AzureServiceDiagnosticsExtension.</span><span class="sxs-lookup"><span data-stu-id="7b511-156">May also be specified as a parameter when executing the Set-AzureServiceDiagnosticsExtension cmdlet.</span></span>|  
|<span data-ttu-id="7b511-157">**StorageType**</span><span class="sxs-lookup"><span data-stu-id="7b511-157">**StorageType**</span></span>|<span data-ttu-id="7b511-158">Puede ser *Table*, *Blob* o *TableAndBlob*.</span><span class="sxs-lookup"><span data-stu-id="7b511-158">Can be *Table*, *Blob*, or *TableAndBlob*.</span></span> <span data-ttu-id="7b511-159">Table es el valor predeterminado.</span><span class="sxs-lookup"><span data-stu-id="7b511-159">Table is default.</span></span> <span data-ttu-id="7b511-160">Cuando se elige TableAndBlob, los datos de diagnóstico se escriben dos veces: una vez en cada tipo.</span><span class="sxs-lookup"><span data-stu-id="7b511-160">When TableAndBlob is chosen, diagnostic data is written twice -- once to each type.</span></span>|  
|<span data-ttu-id="7b511-161">**LocalResourceDirectory**</span><span class="sxs-lookup"><span data-stu-id="7b511-161">**LocalResourceDirectory**</span></span>|<span data-ttu-id="7b511-162">El directorio en la máquina virtual donde Monitoring Agent almacena los datos del evento.</span><span class="sxs-lookup"><span data-stu-id="7b511-162">The directory on the virtual machine where the Monitoring Agent stores event data.</span></span> <span data-ttu-id="7b511-163">Si no se establece, se usa el directorio predeterminado:</span><span class="sxs-lookup"><span data-stu-id="7b511-163">If not, set, the default directory is used:</span></span><br /><br /> <span data-ttu-id="7b511-164">Para un rol de trabajo o web: `C:\Resources\<guid>\directory\<guid>.<RoleName.DiagnosticStore\`</span><span class="sxs-lookup"><span data-stu-id="7b511-164">For a Worker/web role: `C:\Resources\<guid>\directory\<guid>.<RoleName.DiagnosticStore\`</span></span><br /><br /> <span data-ttu-id="7b511-165">Para una máquina virtual: `C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<WADVersion>\WAD<WADVersion>`</span><span class="sxs-lookup"><span data-stu-id="7b511-165">For a Virtual Machine: `C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<WADVersion>\WAD<WADVersion>`</span></span><br /><br /> <span data-ttu-id="7b511-166">Los atributos necesarios son:</span><span class="sxs-lookup"><span data-stu-id="7b511-166">Required attributes are:</span></span><br /><br /> <span data-ttu-id="7b511-167">- **path**: el directorio del sistema que va a usar Diagnósticos de Azure.</span><span class="sxs-lookup"><span data-stu-id="7b511-167">- **path** - The directory on the system to be used by Azure Diagnostics.</span></span><br /><br /> <span data-ttu-id="7b511-168">- **expandEnvironment**: controla si se expanden las variables de entorno en el nombre de ruta de acceso.</span><span class="sxs-lookup"><span data-stu-id="7b511-168">- **expandEnvironment** - Controls whether environment variables are expanded in the path name.</span></span>|  

## <a name="wadcfg-element"></a><span data-ttu-id="7b511-169">Elemento WadCFG</span><span class="sxs-lookup"><span data-stu-id="7b511-169">WadCFG Element</span></span>  
 <span data-ttu-id="7b511-170">*Árbol: Raíz - DiagnosticsConfiguration - PublicConfig - WadCFG*</span><span class="sxs-lookup"><span data-stu-id="7b511-170">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG*</span></span>
 
 <span data-ttu-id="7b511-171">Identifica y configura los datos de telemetría que se van a recopilar.</span><span class="sxs-lookup"><span data-stu-id="7b511-171">Identifies and configures the telemetry data to be collected.</span></span>  


## <a name="diagnosticmonitorconfiguration-element"></a><span data-ttu-id="7b511-172">Elemento DiagnosticMonitorConfiguration</span><span class="sxs-lookup"><span data-stu-id="7b511-172">DiagnosticMonitorConfiguration Element</span></span> 
 <span data-ttu-id="7b511-173">*Árbol: Raíz - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration*</span><span class="sxs-lookup"><span data-stu-id="7b511-173">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration*</span></span>

 <span data-ttu-id="7b511-174">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="7b511-174">Required</span></span> 

|<span data-ttu-id="7b511-175">Attributes</span><span class="sxs-lookup"><span data-stu-id="7b511-175">Attributes</span></span>|<span data-ttu-id="7b511-176">Descripción</span><span class="sxs-lookup"><span data-stu-id="7b511-176">Description</span></span>|  
|----------------|-----------------|  
| <span data-ttu-id="7b511-177">**overallQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="7b511-177">**overallQuotaInMB**</span></span> | <span data-ttu-id="7b511-178">La cantidad máxima de espacio en disco local que se puede utilizar en los distintos tipos de datos de diagnóstico que recopila Azure Diagnostics.</span><span class="sxs-lookup"><span data-stu-id="7b511-178">The maximum amount of local disk space that may be consumed by the various types of diagnostic data collected by Azure Diagnostics.</span></span> <span data-ttu-id="7b511-179">La configuración predeterminada es 5120 MB.</span><span class="sxs-lookup"><span data-stu-id="7b511-179">The default setting is 5120 MB.</span></span><br />
|<span data-ttu-id="7b511-180">**useProxyServer**</span><span class="sxs-lookup"><span data-stu-id="7b511-180">**useProxyServer**</span></span> | <span data-ttu-id="7b511-181">Configure Azure Diagnostics para utilizar la configuración del servidor proxy tal como se estableció en la configuración de Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="7b511-181">Configure Azure Diagnostics to use the proxy server settings as set in IE settings.</span></span>|  

<br /> <br />

|<span data-ttu-id="7b511-182">Elementos secundarios</span><span class="sxs-lookup"><span data-stu-id="7b511-182">Child Elements</span></span>|<span data-ttu-id="7b511-183">Descripción</span><span class="sxs-lookup"><span data-stu-id="7b511-183">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="7b511-184">**CrashDumps**</span><span class="sxs-lookup"><span data-stu-id="7b511-184">**CrashDumps**</span></span>|<span data-ttu-id="7b511-185">Consulte la descripción en cualquier parte de esta página.</span><span class="sxs-lookup"><span data-stu-id="7b511-185">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="7b511-186">**DiagnosticInfrastructureLogs**</span><span class="sxs-lookup"><span data-stu-id="7b511-186">**DiagnosticInfrastructureLogs**</span></span>|<span data-ttu-id="7b511-187">Habilite la recopilación de registros generados por Diagnósticos de Azure.</span><span class="sxs-lookup"><span data-stu-id="7b511-187">Enable collection of logs generated by Azure Diagnostics.</span></span> <span data-ttu-id="7b511-188">Los registros de infraestructura de diagnóstico son útiles para solucionar problemas del mismo sistema de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="7b511-188">The diagnostic infrastructure logs are useful for troubleshooting the diagnostics system itself.</span></span> <span data-ttu-id="7b511-189">Los atributos opcionales son:</span><span class="sxs-lookup"><span data-stu-id="7b511-189">Optional attributes are:</span></span><br /><br /> <span data-ttu-id="7b511-190">- **scheduledTransferLogLevelFilter**: configura el nivel de gravedad mínimo de los registros recopilados.</span><span class="sxs-lookup"><span data-stu-id="7b511-190">- **scheduledTransferLogLevelFilter** - Configures the minimum severity level of the logs collected.</span></span><br /><br /> <span data-ttu-id="7b511-191">- **scheduledTransferPeriod**: el intervalo existente entre las transferencias programadas en el almacenamiento, redondeado al minuto más cercano.</span><span class="sxs-lookup"><span data-stu-id="7b511-191">- **scheduledTransferPeriod** - The interval between scheduled transfers to storage rounded up to the nearest minute.</span></span> <span data-ttu-id="7b511-192">El valor es un [“tipo de datos de duración” XML](http://www.w3schools.com/schema/schema_dtypes_date.asp).</span><span class="sxs-lookup"><span data-stu-id="7b511-192">The value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span></span> |  
|<span data-ttu-id="7b511-193">**Directorios**</span><span class="sxs-lookup"><span data-stu-id="7b511-193">**Directories**</span></span>|<span data-ttu-id="7b511-194">Consulte la descripción en cualquier parte de esta página.</span><span class="sxs-lookup"><span data-stu-id="7b511-194">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="7b511-195">**EtwProviders**</span><span class="sxs-lookup"><span data-stu-id="7b511-195">**EtwProviders**</span></span>|<span data-ttu-id="7b511-196">Consulte la descripción en cualquier parte de esta página.</span><span class="sxs-lookup"><span data-stu-id="7b511-196">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="7b511-197">**Métricas**</span><span class="sxs-lookup"><span data-stu-id="7b511-197">**Metrics**</span></span>|<span data-ttu-id="7b511-198">Consulte la descripción en cualquier parte de esta página.</span><span class="sxs-lookup"><span data-stu-id="7b511-198">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="7b511-199">**PerformanceCounters**</span><span class="sxs-lookup"><span data-stu-id="7b511-199">**PerformanceCounters**</span></span>|<span data-ttu-id="7b511-200">Consulte la descripción en cualquier parte de esta página.</span><span class="sxs-lookup"><span data-stu-id="7b511-200">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="7b511-201">**WindowsEventLog**</span><span class="sxs-lookup"><span data-stu-id="7b511-201">**WindowsEventLog**</span></span>|<span data-ttu-id="7b511-202">Consulte la descripción en cualquier parte de esta página.</span><span class="sxs-lookup"><span data-stu-id="7b511-202">See description elsewhere on this page.</span></span>| 
|<span data-ttu-id="7b511-203">**DockerSources**</span><span class="sxs-lookup"><span data-stu-id="7b511-203">**DockerSources**</span></span>|<span data-ttu-id="7b511-204">Consulte la descripción en cualquier parte de esta página.</span><span class="sxs-lookup"><span data-stu-id="7b511-204">See description elsewhere on this page.</span></span> | 



## <a name="crashdumps-element"></a><span data-ttu-id="7b511-205">Elemento CrashDumps</span><span class="sxs-lookup"><span data-stu-id="7b511-205">CrashDumps Element</span></span>  
 <span data-ttu-id="7b511-206">*Árbol: Raíz - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - CrashDumps*</span><span class="sxs-lookup"><span data-stu-id="7b511-206">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - CrashDumps*</span></span>
 
 <span data-ttu-id="7b511-207">Habilita la recopilación de volcados de memoria.</span><span class="sxs-lookup"><span data-stu-id="7b511-207">Enable the collection of crash dumps.</span></span>  

|<span data-ttu-id="7b511-208">Atributos</span><span class="sxs-lookup"><span data-stu-id="7b511-208">Attributes</span></span>|<span data-ttu-id="7b511-209">Descripción</span><span class="sxs-lookup"><span data-stu-id="7b511-209">Description</span></span>|  
|----------------|-----------------|  
|<span data-ttu-id="7b511-210">**containerName**</span><span class="sxs-lookup"><span data-stu-id="7b511-210">**containerName**</span></span>|<span data-ttu-id="7b511-211">Opcional.</span><span class="sxs-lookup"><span data-stu-id="7b511-211">Optional.</span></span> <span data-ttu-id="7b511-212">El nombre del contenedor de blobs en la cuenta de Azure Storage que se usará para almacenar los volcados de memoria.</span><span class="sxs-lookup"><span data-stu-id="7b511-212">The name of the blob container in your Azure Storage account to be used to store crash dumps.</span></span>|  
|<span data-ttu-id="7b511-213">**crashDumpType**</span><span class="sxs-lookup"><span data-stu-id="7b511-213">**crashDumpType**</span></span>|<span data-ttu-id="7b511-214">Opcional.</span><span class="sxs-lookup"><span data-stu-id="7b511-214">Optional.</span></span>  <span data-ttu-id="7b511-215">Configura Diagnósticos de Azure para recopilar volcados de memoria parciales o completos.</span><span class="sxs-lookup"><span data-stu-id="7b511-215">Configures Azure Diagnostics to collect mini or full crash dumps.</span></span>|  
|<span data-ttu-id="7b511-216">**directoryQuotaPercentage**</span><span class="sxs-lookup"><span data-stu-id="7b511-216">**directoryQuotaPercentage**</span></span>|<span data-ttu-id="7b511-217">Opcional.</span><span class="sxs-lookup"><span data-stu-id="7b511-217">Optional.</span></span>  <span data-ttu-id="7b511-218">Configura el porcentaje de **overallQuotaInMB** que se va a reservar para los volcados de memoria en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="7b511-218">Configures the percentage of **overallQuotaInMB** to be reserved for crash dumps on the VM.</span></span>|  

|<span data-ttu-id="7b511-219">Elementos secundarios</span><span class="sxs-lookup"><span data-stu-id="7b511-219">Child Elements</span></span>|<span data-ttu-id="7b511-220">Descripción</span><span class="sxs-lookup"><span data-stu-id="7b511-220">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="7b511-221">**CrashDumpConfiguration**</span><span class="sxs-lookup"><span data-stu-id="7b511-221">**CrashDumpConfiguration**</span></span>|<span data-ttu-id="7b511-222">Obligatorio.</span><span class="sxs-lookup"><span data-stu-id="7b511-222">Required.</span></span> <span data-ttu-id="7b511-223">Define los valores de configuración para cada proceso.</span><span class="sxs-lookup"><span data-stu-id="7b511-223">Defines configuration values for each process.</span></span><br /><br /> <span data-ttu-id="7b511-224">También se necesita el atributo siguiente:</span><span class="sxs-lookup"><span data-stu-id="7b511-224">The following attribute is also required:</span></span><br /><br /> <span data-ttu-id="7b511-225">**processName**: el nombre del proceso para el que desea que Diagnósticos de Azure recopile un volcado de memoria.</span><span class="sxs-lookup"><span data-stu-id="7b511-225">**processName** - The name of the process you want Azure Diagnostics to collect a crash dump for.</span></span>|  

## <a name="directories-element"></a><span data-ttu-id="7b511-226">Elemento Directories</span><span class="sxs-lookup"><span data-stu-id="7b511-226">Directories Element</span></span> 
 <span data-ttu-id="7b511-227">*Árbol: Raíz - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration -  Directories*</span><span class="sxs-lookup"><span data-stu-id="7b511-227">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration -  Directories*</span></span>

 <span data-ttu-id="7b511-228">Habilita la recopilación del contenido de un directorio, los registros de solicitud de acceso de error de IIS o los registros de IIS.</span><span class="sxs-lookup"><span data-stu-id="7b511-228">Enables the collection of the contents of a directory, IIS failed access request logs and/or IIS logs.</span></span>  

 <span data-ttu-id="7b511-229">Atributo **scheduledTransferPeriod** opcional.</span><span class="sxs-lookup"><span data-stu-id="7b511-229">Optional **scheduledTransferPeriod** attribute.</span></span> <span data-ttu-id="7b511-230">Consulte la explicación anterior.</span><span class="sxs-lookup"><span data-stu-id="7b511-230">See explanation earlier.</span></span>  

|<span data-ttu-id="7b511-231">Elementos secundarios</span><span class="sxs-lookup"><span data-stu-id="7b511-231">Child Elements</span></span>|<span data-ttu-id="7b511-232">Descripción</span><span class="sxs-lookup"><span data-stu-id="7b511-232">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="7b511-233">**IISLogs**</span><span class="sxs-lookup"><span data-stu-id="7b511-233">**IISLogs**</span></span>|<span data-ttu-id="7b511-234">La inclusión de este elemento en la configuración habilita la recopilación de registros de IIS:</span><span class="sxs-lookup"><span data-stu-id="7b511-234">Including this element in the configuration enables the collection of IIS logs:</span></span><br /><br /> <span data-ttu-id="7b511-235">**containerName**: el nombre del contenedor de blobs en la cuenta de Azure Storage que se usará para almacenar los registros de IIS.</span><span class="sxs-lookup"><span data-stu-id="7b511-235">**containerName** - The name of the blob container in your Azure Storage account to be used to store the IIS logs.</span></span>|   
|<span data-ttu-id="7b511-236">**FailedRequestLogs**</span><span class="sxs-lookup"><span data-stu-id="7b511-236">**FailedRequestLogs**</span></span>|<span data-ttu-id="7b511-237">La inclusión de este elemento en la configuración habilita la recopilación de registros sobre las solicitudes erróneas en un sitio o aplicación de IIS.</span><span class="sxs-lookup"><span data-stu-id="7b511-237">Including this element in the configuration enables collection of logs about failed requests to an IIS site or application.</span></span> <span data-ttu-id="7b511-238">También debe habilitar las opciones de seguimiento en **system.WebServer** de **Web.config**.</span><span class="sxs-lookup"><span data-stu-id="7b511-238">You must also enable tracing options under **system.WebServer** in **Web.config**.</span></span>|  
|<span data-ttu-id="7b511-239">**DataSources**</span><span class="sxs-lookup"><span data-stu-id="7b511-239">**DataSources**</span></span>|<span data-ttu-id="7b511-240">Una lista de directorios que se van a supervisar.</span><span class="sxs-lookup"><span data-stu-id="7b511-240">A list of directories to monitor.</span></span>| 




## <a name="datasources-element"></a><span data-ttu-id="7b511-241">Elemento DataSources</span><span class="sxs-lookup"><span data-stu-id="7b511-241">DataSources Element</span></span>  
 <span data-ttu-id="7b511-242">*Árbol: Raíz - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Directories - DataSources*</span><span class="sxs-lookup"><span data-stu-id="7b511-242">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Directories - DataSources*</span></span>

 <span data-ttu-id="7b511-243">Una lista de directorios que se van a supervisar.</span><span class="sxs-lookup"><span data-stu-id="7b511-243">A list of directories to monitor.</span></span>  

|<span data-ttu-id="7b511-244">Elementos secundarios</span><span class="sxs-lookup"><span data-stu-id="7b511-244">Child Elements</span></span>|<span data-ttu-id="7b511-245">Descripción</span><span class="sxs-lookup"><span data-stu-id="7b511-245">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="7b511-246">**DirectoryConfiguration**</span><span class="sxs-lookup"><span data-stu-id="7b511-246">**DirectoryConfiguration**</span></span>|<span data-ttu-id="7b511-247">Obligatorio.</span><span class="sxs-lookup"><span data-stu-id="7b511-247">Required.</span></span> <span data-ttu-id="7b511-248">Atributo necesario:</span><span class="sxs-lookup"><span data-stu-id="7b511-248">Required attribute:</span></span><br /><br /> <span data-ttu-id="7b511-249">**containerName**: el nombre del contenedor de blobs en la cuenta de Azure Storage que se usará para almacenar los archivos de registro.</span><span class="sxs-lookup"><span data-stu-id="7b511-249">**containerName** - The name of the blob container in your Azure Storage account that to be used to store the log files.</span></span>|  





## <a name="directoryconfiguration-element"></a><span data-ttu-id="7b511-250">Elemento DirectoryConfiguration</span><span class="sxs-lookup"><span data-stu-id="7b511-250">DirectoryConfiguration Element</span></span>  
 <span data-ttu-id="7b511-251">*Árbol: Raíz - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Directories - DataSources - DirectoryConfiguration*</span><span class="sxs-lookup"><span data-stu-id="7b511-251">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Directories - DataSources - DirectoryConfiguration*</span></span>

 <span data-ttu-id="7b511-252">Puede incluir el elemento **Absolute** o el elemento **LocalResource**, pero no ambos.</span><span class="sxs-lookup"><span data-stu-id="7b511-252">May include either the **Absolute** or **LocalResource** element but not both.</span></span>  

|<span data-ttu-id="7b511-253">Elementos secundarios</span><span class="sxs-lookup"><span data-stu-id="7b511-253">Child Elements</span></span>|<span data-ttu-id="7b511-254">Descripción</span><span class="sxs-lookup"><span data-stu-id="7b511-254">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="7b511-255">**Absolute**</span><span class="sxs-lookup"><span data-stu-id="7b511-255">**Absolute**</span></span>|<span data-ttu-id="7b511-256">La ruta de acceso absoluta al directorio que se va a supervisar.</span><span class="sxs-lookup"><span data-stu-id="7b511-256">The absolute path to the directory to monitor.</span></span> <span data-ttu-id="7b511-257">Los atributos siguientes son necesarios:</span><span class="sxs-lookup"><span data-stu-id="7b511-257">The following attributes are required:</span></span><br /><br /> <span data-ttu-id="7b511-258">- **Path**: la ruta de acceso absoluta al directorio que se va a supervisar.</span><span class="sxs-lookup"><span data-stu-id="7b511-258">- **Path** - The absolute path to the directory to monitor.</span></span><br /><br /> <span data-ttu-id="7b511-259">- **expandEnvironment**: configura si se expanden las variables de entorno en Path.</span><span class="sxs-lookup"><span data-stu-id="7b511-259">- **expandEnvironment** - Configures whether environment variables in Path are expanded.</span></span>|  
|<span data-ttu-id="7b511-260">**LocalResource**</span><span class="sxs-lookup"><span data-stu-id="7b511-260">**LocalResource**</span></span>|<span data-ttu-id="7b511-261">La ruta de acceso relativa a un recurso local que se va a supervisar.</span><span class="sxs-lookup"><span data-stu-id="7b511-261">The path relative to a local resource to monitor.</span></span> <span data-ttu-id="7b511-262">Los atributos necesarios son:</span><span class="sxs-lookup"><span data-stu-id="7b511-262">Required attributes are:</span></span><br /><br /> <span data-ttu-id="7b511-263">- **Name**: el recurso local que contiene el directorio que se va a supervisar</span><span class="sxs-lookup"><span data-stu-id="7b511-263">- **Name** - The local resource that contains the directory to monitor</span></span><br /><br /> <span data-ttu-id="7b511-264">- **relativePath**: la ruta de acceso relativa al nombre que contiene el directorio que se va a supervisar</span><span class="sxs-lookup"><span data-stu-id="7b511-264">- **relativePath** - The path relative to Name that contains the directory to monitor</span></span>|  



## <a name="etwproviders-element"></a><span data-ttu-id="7b511-265">Elemento EtwProviders</span><span class="sxs-lookup"><span data-stu-id="7b511-265">EtwProviders Element</span></span>  
 <span data-ttu-id="7b511-266">*Árbol: Raíz - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders*</span><span class="sxs-lookup"><span data-stu-id="7b511-266">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders*</span></span>

 <span data-ttu-id="7b511-267">Configura la recopilación de eventos ETW en EventSource o el manifiesto de ETW en función de los proveedores.</span><span class="sxs-lookup"><span data-stu-id="7b511-267">Configures collection of ETW events from EventSource and/or ETW Manifest based providers.</span></span>  

|<span data-ttu-id="7b511-268">Elementos secundarios</span><span class="sxs-lookup"><span data-stu-id="7b511-268">Child Elements</span></span>|<span data-ttu-id="7b511-269">Descripción</span><span class="sxs-lookup"><span data-stu-id="7b511-269">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="7b511-270">**EtwEventSourceProviderConfiguration**</span><span class="sxs-lookup"><span data-stu-id="7b511-270">**EtwEventSourceProviderConfiguration**</span></span>|<span data-ttu-id="7b511-271">Configura la recopilación de eventos generados a partir de la [clase EventSource](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx).</span><span class="sxs-lookup"><span data-stu-id="7b511-271">Configures collection of events generated from [EventSource Class](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx).</span></span> <span data-ttu-id="7b511-272">Atributo necesario:</span><span class="sxs-lookup"><span data-stu-id="7b511-272">Required attribute:</span></span><br /><br /> <span data-ttu-id="7b511-273">**provider**: el nombre de clase del evento EventSource.</span><span class="sxs-lookup"><span data-stu-id="7b511-273">**provider** - The class name of the EventSource event.</span></span><br /><br /> <span data-ttu-id="7b511-274">Los atributos opcionales son:</span><span class="sxs-lookup"><span data-stu-id="7b511-274">Optional attributes are:</span></span><br /><br /> <span data-ttu-id="7b511-275">- **scheduledTransferLogLevelFilter**: el nivel de gravedad mínimo para transferir a la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="7b511-275">- **scheduledTransferLogLevelFilter** - The minimum severity level to transfer to your storage account.</span></span><br /><br /> <span data-ttu-id="7b511-276">- **scheduledTransferPeriod**: el intervalo existente entre las transferencias programadas en el almacenamiento, redondeado al minuto más cercano.</span><span class="sxs-lookup"><span data-stu-id="7b511-276">- **scheduledTransferPeriod** - The interval between scheduled transfers to storage rounded up to the nearest minute.</span></span> <span data-ttu-id="7b511-277">El valor es un [“tipo de datos de duración” XML](http://www.w3schools.com/schema/schema_dtypes_date.asp).</span><span class="sxs-lookup"><span data-stu-id="7b511-277">The value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span></span> |  
|<span data-ttu-id="7b511-278">**EtwManifestProviderConfiguration**</span><span class="sxs-lookup"><span data-stu-id="7b511-278">**EtwManifestProviderConfiguration**</span></span>|<span data-ttu-id="7b511-279">Atributo necesario:</span><span class="sxs-lookup"><span data-stu-id="7b511-279">Required attribute:</span></span><br /><br /> <span data-ttu-id="7b511-280">**provider**: el GUID del proveedor de eventos</span><span class="sxs-lookup"><span data-stu-id="7b511-280">**provider** - The GUID of the event provider</span></span><br /><br /> <span data-ttu-id="7b511-281">Los atributos opcionales son:</span><span class="sxs-lookup"><span data-stu-id="7b511-281">Optional attributes are:</span></span><br /><br /> <span data-ttu-id="7b511-282">- **scheduledTransferLogLevelFilter**: el nivel de gravedad mínimo para transferir a la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="7b511-282">- **scheduledTransferLogLevelFilter** - The minimum severity level to transfer to your storage account.</span></span><br /><br /> <span data-ttu-id="7b511-283">- **scheduledTransferPeriod**: el intervalo existente entre las transferencias programadas en el almacenamiento, redondeado al minuto más cercano.</span><span class="sxs-lookup"><span data-stu-id="7b511-283">- **scheduledTransferPeriod** - The interval between scheduled transfers to storage rounded up to the nearest minute.</span></span> <span data-ttu-id="7b511-284">El valor es un [“tipo de datos de duración” XML](http://www.w3schools.com/schema/schema_dtypes_date.asp).</span><span class="sxs-lookup"><span data-stu-id="7b511-284">The value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span></span> |  



## <a name="etweventsourceproviderconfiguration-element"></a><span data-ttu-id="7b511-285">Elemento EtwEventSourceProviderConfiguration</span><span class="sxs-lookup"><span data-stu-id="7b511-285">EtwEventSourceProviderConfiguration Element</span></span>  
 <span data-ttu-id="7b511-286">*Árbol: Raíz - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders- EtwEventSourceProviderConfiguration*</span><span class="sxs-lookup"><span data-stu-id="7b511-286">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders- EtwEventSourceProviderConfiguration*</span></span>

 <span data-ttu-id="7b511-287">Configura la recopilación de eventos generados a partir de la [clase EventSource](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx).</span><span class="sxs-lookup"><span data-stu-id="7b511-287">Configures collection of events generated from [EventSource Class](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx).</span></span>  

|<span data-ttu-id="7b511-288">Elementos secundarios</span><span class="sxs-lookup"><span data-stu-id="7b511-288">Child Elements</span></span>|<span data-ttu-id="7b511-289">Descripción</span><span class="sxs-lookup"><span data-stu-id="7b511-289">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="7b511-290">**DefaultEvents**</span><span class="sxs-lookup"><span data-stu-id="7b511-290">**DefaultEvents**</span></span>|<span data-ttu-id="7b511-291">Atributo opcional:</span><span class="sxs-lookup"><span data-stu-id="7b511-291">Optional attribute:</span></span><br/><br/> <span data-ttu-id="7b511-292">**eventDestination**: el nombre de la tabla en la que se van a almacenar los eventos</span><span class="sxs-lookup"><span data-stu-id="7b511-292">**eventDestination** - The name of the table to store the events in</span></span>|  
|<span data-ttu-id="7b511-293">**Evento**</span><span class="sxs-lookup"><span data-stu-id="7b511-293">**Event**</span></span>|<span data-ttu-id="7b511-294">Atributo necesario:</span><span class="sxs-lookup"><span data-stu-id="7b511-294">Required attribute:</span></span><br /><br /> <span data-ttu-id="7b511-295">**id**: el identificador del evento.</span><span class="sxs-lookup"><span data-stu-id="7b511-295">**id** - The id of the event.</span></span><br /><br /> <span data-ttu-id="7b511-296">Atributo opcional:</span><span class="sxs-lookup"><span data-stu-id="7b511-296">Optional attribute:</span></span><br /><br /> <span data-ttu-id="7b511-297">**eventDestination**: el nombre de la tabla en la que se van a almacenar los eventos</span><span class="sxs-lookup"><span data-stu-id="7b511-297">**eventDestination** - The name of the table to store the events in</span></span>|  



## <a name="etwmanifestproviderconfiguration-element"></a><span data-ttu-id="7b511-298">Elemento EtwManifestProviderConfiguration</span><span class="sxs-lookup"><span data-stu-id="7b511-298">EtwManifestProviderConfiguration Element</span></span>  
 <span data-ttu-id="7b511-299">*Árbol: Raíz - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders - EtwManifestProviderConfiguration*</span><span class="sxs-lookup"><span data-stu-id="7b511-299">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders - EtwManifestProviderConfiguration*</span></span>

|<span data-ttu-id="7b511-300">Elementos secundarios</span><span class="sxs-lookup"><span data-stu-id="7b511-300">Child Elements</span></span>|<span data-ttu-id="7b511-301">Descripción</span><span class="sxs-lookup"><span data-stu-id="7b511-301">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="7b511-302">**DefaultEvents**</span><span class="sxs-lookup"><span data-stu-id="7b511-302">**DefaultEvents**</span></span>|<span data-ttu-id="7b511-303">Atributo opcional:</span><span class="sxs-lookup"><span data-stu-id="7b511-303">Optional attribute:</span></span><br /><br /> <span data-ttu-id="7b511-304">**eventDestination**: el nombre de la tabla en la que se van a almacenar los eventos</span><span class="sxs-lookup"><span data-stu-id="7b511-304">**eventDestination** - The name of the table to store the events in</span></span>|  
|<span data-ttu-id="7b511-305">**Evento**</span><span class="sxs-lookup"><span data-stu-id="7b511-305">**Event**</span></span>|<span data-ttu-id="7b511-306">Atributo necesario:</span><span class="sxs-lookup"><span data-stu-id="7b511-306">Required attribute:</span></span><br /><br /> <span data-ttu-id="7b511-307">**id**: el identificador del evento.</span><span class="sxs-lookup"><span data-stu-id="7b511-307">**id** - The id of the event.</span></span><br /><br /> <span data-ttu-id="7b511-308">Atributo opcional:</span><span class="sxs-lookup"><span data-stu-id="7b511-308">Optional attribute:</span></span><br /><br /> <span data-ttu-id="7b511-309">**eventDestination**: el nombre de la tabla en la que se van a almacenar los eventos</span><span class="sxs-lookup"><span data-stu-id="7b511-309">**eventDestination** - The name of the table to store the events in</span></span>|  



## <a name="metrics-element"></a><span data-ttu-id="7b511-310">Elemento Metrics</span><span class="sxs-lookup"><span data-stu-id="7b511-310">Metrics Element</span></span>  
 <span data-ttu-id="7b511-311">*Árbol: Raíz - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Metrics*</span><span class="sxs-lookup"><span data-stu-id="7b511-311">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Metrics*</span></span>

 <span data-ttu-id="7b511-312">Le permite generar una tabla de contadores de rendimiento optimizada para las consultas rápidas.</span><span class="sxs-lookup"><span data-stu-id="7b511-312">Enables you to generate a performance counter table that is optimized for fast queries.</span></span> <span data-ttu-id="7b511-313">Cada contador de rendimiento que se define en el elemento **PerformanceCounters** se almacena en la tabla de métricas además de la tabla de contadores de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="7b511-313">Each performance counter that is defined in the **PerformanceCounters** element is stored in the Metrics table in addition to the Performance Counter table.</span></span>  

 <span data-ttu-id="7b511-314">El atributo **resourceId** es necesario.</span><span class="sxs-lookup"><span data-stu-id="7b511-314">The **resourceId** attribute is required.</span></span>  <span data-ttu-id="7b511-315">Se trata del identificador de recurso de la máquina virtual en donde se va a implementar Azure Diagnostics.</span><span class="sxs-lookup"><span data-stu-id="7b511-315">The resource ID of the Virtual Machine you are deploying Azure Diagnostics to.</span></span> <span data-ttu-id="7b511-316">Obtenga el valor de **resourceID** en [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7b511-316">Get the **resourceID** from the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="7b511-317">Seleccione **Examinar** -> **Grupos de recursos** -> **<Nombre\>**.</span><span class="sxs-lookup"><span data-stu-id="7b511-317">Select **Browse** -> **Resource Groups** -> **<Name\>**.</span></span> <span data-ttu-id="7b511-318">Haga clic en el icono **Propiedades** y copie el valor del campo **ID**.</span><span class="sxs-lookup"><span data-stu-id="7b511-318">Click the **Properties** tile and copy the value from the **ID** field.</span></span>  

|<span data-ttu-id="7b511-319">Elementos secundarios</span><span class="sxs-lookup"><span data-stu-id="7b511-319">Child Elements</span></span>|<span data-ttu-id="7b511-320">Descripción</span><span class="sxs-lookup"><span data-stu-id="7b511-320">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="7b511-321">**MetricAggregation**</span><span class="sxs-lookup"><span data-stu-id="7b511-321">**MetricAggregation**</span></span>|<span data-ttu-id="7b511-322">Atributo necesario:</span><span class="sxs-lookup"><span data-stu-id="7b511-322">Required attribute:</span></span><br /><br /> <span data-ttu-id="7b511-323">**scheduledTransferPeriod**: el intervalo existente entre las transferencias programadas en el almacenamiento, redondeado al minuto más cercano.</span><span class="sxs-lookup"><span data-stu-id="7b511-323">**scheduledTransferPeriod** - The interval between scheduled transfers to storage rounded up to the nearest minute.</span></span> <span data-ttu-id="7b511-324">El valor es un [“tipo de datos de duración” XML](http://www.w3schools.com/schema/schema_dtypes_date.asp).</span><span class="sxs-lookup"><span data-stu-id="7b511-324">The value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span></span> |  



## <a name="performancecounters-element"></a><span data-ttu-id="7b511-325">Elemento PerformanceCounters</span><span class="sxs-lookup"><span data-stu-id="7b511-325">PerformanceCounters Element</span></span>  
 <span data-ttu-id="7b511-326">*Árbol: Raíz - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - PerformanceCounters*</span><span class="sxs-lookup"><span data-stu-id="7b511-326">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - PerformanceCounters*</span></span>

 <span data-ttu-id="7b511-327">Habilita la recopilación de contadores de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="7b511-327">Enables the collection of performance counters.</span></span>  

 <span data-ttu-id="7b511-328">Atributo opcional:</span><span class="sxs-lookup"><span data-stu-id="7b511-328">Optional attribute:</span></span>  

 <span data-ttu-id="7b511-329">Atributo **scheduledTransferPeriod** opcional.</span><span class="sxs-lookup"><span data-stu-id="7b511-329">Optional **scheduledTransferPeriod** attribute.</span></span> <span data-ttu-id="7b511-330">Consulte la explicación anterior.</span><span class="sxs-lookup"><span data-stu-id="7b511-330">See explanation earlier.</span></span>

|<span data-ttu-id="7b511-331">Elemento secundario</span><span class="sxs-lookup"><span data-stu-id="7b511-331">Child Element</span></span>|<span data-ttu-id="7b511-332">Descripción</span><span class="sxs-lookup"><span data-stu-id="7b511-332">Description</span></span>|  
|-------------------|-----------------|  
|<span data-ttu-id="7b511-333">**PerformanceCounterConfiguration**</span><span class="sxs-lookup"><span data-stu-id="7b511-333">**PerformanceCounterConfiguration**</span></span>|<span data-ttu-id="7b511-334">Los atributos siguientes son necesarios:</span><span class="sxs-lookup"><span data-stu-id="7b511-334">The following attributes are required:</span></span><br /><br /> <span data-ttu-id="7b511-335">- **counterSpecifier**: el nombre del contador de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="7b511-335">- **counterSpecifier** - The name of the performance counter.</span></span> <span data-ttu-id="7b511-336">Por ejemplo: `\Processor(_Total)\% Processor Time`.</span><span class="sxs-lookup"><span data-stu-id="7b511-336">For example, `\Processor(_Total)\% Processor Time`.</span></span> <span data-ttu-id="7b511-337">Para obtener una lista de contadores de rendimiento en el host, ejecute el comando `typeperf`.</span><span class="sxs-lookup"><span data-stu-id="7b511-337">To get a list of performance counters on your host, run the command `typeperf`.</span></span><br /><br /> <span data-ttu-id="7b511-338">- **sampleRate**: la frecuencia de muestreo del contador.</span><span class="sxs-lookup"><span data-stu-id="7b511-338">- **sampleRate** - How often the counter should be sampled.</span></span><br /><br /> <span data-ttu-id="7b511-339">Atributo opcional:</span><span class="sxs-lookup"><span data-stu-id="7b511-339">Optional attribute:</span></span><br /><br /> <span data-ttu-id="7b511-340">**unit**: la unidad de medida del contador.</span><span class="sxs-lookup"><span data-stu-id="7b511-340">**unit** - The unit of measure of the counter.</span></span>|  




## <a name="windowseventlog-element"></a><span data-ttu-id="7b511-341">Elemento WindowsEventLog</span><span class="sxs-lookup"><span data-stu-id="7b511-341">WindowsEventLog Element</span></span>
 <span data-ttu-id="7b511-342">*Árbol: Raíz - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - WindowsEventLog*</span><span class="sxs-lookup"><span data-stu-id="7b511-342">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - WindowsEventLog*</span></span>
 
 <span data-ttu-id="7b511-343">Habilita la recopilación de registros de eventos de Windows.</span><span class="sxs-lookup"><span data-stu-id="7b511-343">Enables the collection of Windows Event Logs.</span></span>  

 <span data-ttu-id="7b511-344">Atributo **scheduledTransferPeriod** opcional.</span><span class="sxs-lookup"><span data-stu-id="7b511-344">Optional **scheduledTransferPeriod** attribute.</span></span> <span data-ttu-id="7b511-345">Consulte la explicación anterior.</span><span class="sxs-lookup"><span data-stu-id="7b511-345">See explanation  earlier.</span></span>  

|<span data-ttu-id="7b511-346">Elemento secundario</span><span class="sxs-lookup"><span data-stu-id="7b511-346">Child Element</span></span>|<span data-ttu-id="7b511-347">Descripción</span><span class="sxs-lookup"><span data-stu-id="7b511-347">Description</span></span>|  
|-------------------|-----------------|  
|<span data-ttu-id="7b511-348">**DataSource**</span><span class="sxs-lookup"><span data-stu-id="7b511-348">**DataSource**</span></span>|<span data-ttu-id="7b511-349">Los registros de eventos de Windows que se van a recopilar.</span><span class="sxs-lookup"><span data-stu-id="7b511-349">The Windows Event logs to collect.</span></span> <span data-ttu-id="7b511-350">Atributo necesario:</span><span class="sxs-lookup"><span data-stu-id="7b511-350">Required attribute:</span></span><br /><br /> <span data-ttu-id="7b511-351">**name**: la consulta de XPath que describe los eventos de Windows que se van a recopilar.</span><span class="sxs-lookup"><span data-stu-id="7b511-351">**name** - The XPath query describing the windows events to be collected.</span></span> <span data-ttu-id="7b511-352">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="7b511-352">For example:</span></span><br /><br /> `Application!*[System[(Level <=3)]], System!*[System[(Level <=3)]], System!*[System[Provider[@Name='Microsoft Antimalware']]], Security!*[System[(Level <= 3)]`<br /><br /> <span data-ttu-id="7b511-353">Para recopilar todos los eventos, especifique "*".</span><span class="sxs-lookup"><span data-stu-id="7b511-353">To collect all events, specify "*"</span></span>|  




## <a name="logs-element"></a><span data-ttu-id="7b511-354">Elemento Logs</span><span class="sxs-lookup"><span data-stu-id="7b511-354">Logs Element</span></span>  
 <span data-ttu-id="7b511-355">*Árbol: Raíz - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Logs*</span><span class="sxs-lookup"><span data-stu-id="7b511-355">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Logs*</span></span>

 <span data-ttu-id="7b511-356">Se presenta en la versión 1.0 y 1.1.</span><span class="sxs-lookup"><span data-stu-id="7b511-356">Present in version 1.0 and 1.1.</span></span> <span data-ttu-id="7b511-357">Falta en 1.2.</span><span class="sxs-lookup"><span data-stu-id="7b511-357">Missing in 1.2.</span></span> <span data-ttu-id="7b511-358">Se ha agregado en 1.3.</span><span class="sxs-lookup"><span data-stu-id="7b511-358">Added back in 1.3.</span></span>  

 <span data-ttu-id="7b511-359">Define la configuración del búfer para los registros básicos de Azure.</span><span class="sxs-lookup"><span data-stu-id="7b511-359">Defines the buffer configuration for basic Azure logs.</span></span>  

|<span data-ttu-id="7b511-360">Atributo</span><span class="sxs-lookup"><span data-stu-id="7b511-360">Attribute</span></span>|<span data-ttu-id="7b511-361">Tipo</span><span class="sxs-lookup"><span data-stu-id="7b511-361">Type</span></span>|<span data-ttu-id="7b511-362">Descripción</span><span class="sxs-lookup"><span data-stu-id="7b511-362">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="7b511-363">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="7b511-363">**bufferQuotaInMB**</span></span>|<span data-ttu-id="7b511-364">**unsignedInt**</span><span class="sxs-lookup"><span data-stu-id="7b511-364">**unsignedInt**</span></span>|<span data-ttu-id="7b511-365">Opcional.</span><span class="sxs-lookup"><span data-stu-id="7b511-365">Optional.</span></span> <span data-ttu-id="7b511-366">Especifica la cantidad máxima de almacenamiento del sistema de archivos que está disponible para los datos especificados.</span><span class="sxs-lookup"><span data-stu-id="7b511-366">Specifies the maximum amount of file system storage that is available for the specified data.</span></span><br /><br /> <span data-ttu-id="7b511-367">El valor predeterminado es 0.</span><span class="sxs-lookup"><span data-stu-id="7b511-367">The default is 0.</span></span>|  
|<span data-ttu-id="7b511-368">**scheduledTransferLogLevelFilterr**</span><span class="sxs-lookup"><span data-stu-id="7b511-368">**scheduledTransferLogLevelFilterr**</span></span>|<span data-ttu-id="7b511-369">**cadena**</span><span class="sxs-lookup"><span data-stu-id="7b511-369">**string**</span></span>|<span data-ttu-id="7b511-370">Opcional.</span><span class="sxs-lookup"><span data-stu-id="7b511-370">Optional.</span></span> <span data-ttu-id="7b511-371">Especifica el nivel de gravedad mínimo para las entradas de registro que se van a transferir.</span><span class="sxs-lookup"><span data-stu-id="7b511-371">Specifies the minimum severity level for log entries that are transferred.</span></span> <span data-ttu-id="7b511-372">El valor predeterminado es **Undefined**, que transfiere todos los registros.</span><span class="sxs-lookup"><span data-stu-id="7b511-372">The default value is **Undefined**, which transfers all logs.</span></span> <span data-ttu-id="7b511-373">Otros valores posibles (en orden de mayor a menor información) son **Verbose**, **Information**, **Warning**, **Error** y **Critical**.</span><span class="sxs-lookup"><span data-stu-id="7b511-373">Other possible values (in order of most to least information) are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span></span>|  
|<span data-ttu-id="7b511-374">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="7b511-374">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="7b511-375">**duration**</span><span class="sxs-lookup"><span data-stu-id="7b511-375">**duration**</span></span>|<span data-ttu-id="7b511-376">Opcional.</span><span class="sxs-lookup"><span data-stu-id="7b511-376">Optional.</span></span> <span data-ttu-id="7b511-377">Especifica el intervalo existente entre las transferencias programadas de datos, redondeado al minuto más cercano.</span><span class="sxs-lookup"><span data-stu-id="7b511-377">Specifies the interval between scheduled transfers of data, rounded up to the nearest minute.</span></span><br /><br /> <span data-ttu-id="7b511-378">El valor predeterminado es PT0S.</span><span class="sxs-lookup"><span data-stu-id="7b511-378">The default is PT0S.</span></span>|  
|<span data-ttu-id="7b511-379">**sinks**: agregado en 1.5</span><span class="sxs-lookup"><span data-stu-id="7b511-379">**sinks** Added in 1.5</span></span>|<span data-ttu-id="7b511-380">**cadena**</span><span class="sxs-lookup"><span data-stu-id="7b511-380">**string**</span></span>|<span data-ttu-id="7b511-381">Opcional.</span><span class="sxs-lookup"><span data-stu-id="7b511-381">Optional.</span></span> <span data-ttu-id="7b511-382">Apunta a una ubicación de receptor para enviar datos de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="7b511-382">Points to a sink location to also send diagnostic data.</span></span> <span data-ttu-id="7b511-383">Por ejemplo, Application Insights.</span><span class="sxs-lookup"><span data-stu-id="7b511-383">For example, Application Insights.</span></span>|  

## <a name="dockersources"></a><span data-ttu-id="7b511-384">DockerSources</span><span class="sxs-lookup"><span data-stu-id="7b511-384">DockerSources</span></span>
 <span data-ttu-id="7b511-385">*Árbol: Raíz - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - DockerSources*</span><span class="sxs-lookup"><span data-stu-id="7b511-385">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - DockerSources*</span></span>

 <span data-ttu-id="7b511-386">Se agregó en la versión 1.9.</span><span class="sxs-lookup"><span data-stu-id="7b511-386">Added in 1.9.</span></span>

|<span data-ttu-id="7b511-387">Nombre del elemento</span><span class="sxs-lookup"><span data-stu-id="7b511-387">Element Name</span></span>|<span data-ttu-id="7b511-388">Descripción</span><span class="sxs-lookup"><span data-stu-id="7b511-388">Description</span></span>|  
|------------------|-----------------|  
|<span data-ttu-id="7b511-389">**Stats**</span><span class="sxs-lookup"><span data-stu-id="7b511-389">**Stats**</span></span>|<span data-ttu-id="7b511-390">Indica al sistema para recopilar estadísticas de los contenedores de Docker.</span><span class="sxs-lookup"><span data-stu-id="7b511-390">Tells the system to collect stats for Docker containers</span></span>|  

## <a name="sinksconfig-element"></a><span data-ttu-id="7b511-391">Elemento SinksConfig</span><span class="sxs-lookup"><span data-stu-id="7b511-391">SinksConfig Element</span></span>  
 <span data-ttu-id="7b511-392">*Árbol: Raíz - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig*</span><span class="sxs-lookup"><span data-stu-id="7b511-392">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig*</span></span>

 <span data-ttu-id="7b511-393">Una lista de ubicaciones donde enviar datos de diagnóstico y la configuración asociada a estas ubicaciones.</span><span class="sxs-lookup"><span data-stu-id="7b511-393">A list of locations to send diagnostics data to and the configuration associated with those locations.</span></span>  

|<span data-ttu-id="7b511-394">Nombre del elemento</span><span class="sxs-lookup"><span data-stu-id="7b511-394">Element Name</span></span>|<span data-ttu-id="7b511-395">Descripción</span><span class="sxs-lookup"><span data-stu-id="7b511-395">Description</span></span>|  
|------------------|-----------------|  
|<span data-ttu-id="7b511-396">**Sink**</span><span class="sxs-lookup"><span data-stu-id="7b511-396">**Sink**</span></span>|<span data-ttu-id="7b511-397">Consulte la descripción en cualquier parte de esta página.</span><span class="sxs-lookup"><span data-stu-id="7b511-397">See description elsewhere on this page.</span></span>|  

## <a name="sink-element"></a><span data-ttu-id="7b511-398">Elemento Sink</span><span class="sxs-lookup"><span data-stu-id="7b511-398">Sink Element</span></span>
 <span data-ttu-id="7b511-399">*Árbol: Raíz - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink*</span><span class="sxs-lookup"><span data-stu-id="7b511-399">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink*</span></span>

 <span data-ttu-id="7b511-400">Agregado en la versión 1.5.</span><span class="sxs-lookup"><span data-stu-id="7b511-400">Added in version 1.5.</span></span>  

 <span data-ttu-id="7b511-401">Define las ubicaciones donde se van a enviar datos de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="7b511-401">Defines locations to send diagnostic data to.</span></span> <span data-ttu-id="7b511-402">Por ejemplo, el servicio Application Insights.</span><span class="sxs-lookup"><span data-stu-id="7b511-402">For example, the Application Insights service.</span></span>  

|<span data-ttu-id="7b511-403">Atributo</span><span class="sxs-lookup"><span data-stu-id="7b511-403">Attribute</span></span>|<span data-ttu-id="7b511-404">Tipo</span><span class="sxs-lookup"><span data-stu-id="7b511-404">Type</span></span>|<span data-ttu-id="7b511-405">Descripción</span><span class="sxs-lookup"><span data-stu-id="7b511-405">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="7b511-406">**name**</span><span class="sxs-lookup"><span data-stu-id="7b511-406">**name**</span></span>|<span data-ttu-id="7b511-407">string</span><span class="sxs-lookup"><span data-stu-id="7b511-407">string</span></span>|<span data-ttu-id="7b511-408">Cadena que identifica el nombre de receptor.</span><span class="sxs-lookup"><span data-stu-id="7b511-408">A string identifying the sinkname.</span></span>|  

|<span data-ttu-id="7b511-409">Elemento</span><span class="sxs-lookup"><span data-stu-id="7b511-409">Element</span></span>|<span data-ttu-id="7b511-410">Escriba</span><span class="sxs-lookup"><span data-stu-id="7b511-410">Type</span></span>|<span data-ttu-id="7b511-411">Descripción</span><span class="sxs-lookup"><span data-stu-id="7b511-411">Description</span></span>|  
|-------------|----------|-----------------|  
|<span data-ttu-id="7b511-412">**Application Insights**</span><span class="sxs-lookup"><span data-stu-id="7b511-412">**Application Insights**</span></span>|<span data-ttu-id="7b511-413">cadena</span><span class="sxs-lookup"><span data-stu-id="7b511-413">string</span></span>|<span data-ttu-id="7b511-414">Se usa solo al enviar datos a Application Insights.</span><span class="sxs-lookup"><span data-stu-id="7b511-414">Used only when sending data to Application Insights.</span></span> <span data-ttu-id="7b511-415">Contiene la clave de instrumentación para una cuenta activa de Application Insights a la que tiene acceso.</span><span class="sxs-lookup"><span data-stu-id="7b511-415">Contain the Instrumentation Key for an active Application Insights account that you have access to.</span></span>|  
|<span data-ttu-id="7b511-416">**Channels**</span><span class="sxs-lookup"><span data-stu-id="7b511-416">**Channels**</span></span>|<span data-ttu-id="7b511-417">cadena</span><span class="sxs-lookup"><span data-stu-id="7b511-417">string</span></span>|<span data-ttu-id="7b511-418">Uno para cada filtrado adicional transmitido</span><span class="sxs-lookup"><span data-stu-id="7b511-418">One for each additional filtering that stream that you</span></span>|  

## <a name="channels-element"></a><span data-ttu-id="7b511-419">Elemento Channels</span><span class="sxs-lookup"><span data-stu-id="7b511-419">Channels Element</span></span>  
 <span data-ttu-id="7b511-420">*Árbol: Raíz - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink - Channels*</span><span class="sxs-lookup"><span data-stu-id="7b511-420">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink - Channels*</span></span>

 <span data-ttu-id="7b511-421">Agregado en la versión 1.5.</span><span class="sxs-lookup"><span data-stu-id="7b511-421">Added in version 1.5.</span></span>  

 <span data-ttu-id="7b511-422">Define los filtros para los flujos de datos de registro que se pasan a través de un receptor.</span><span class="sxs-lookup"><span data-stu-id="7b511-422">Defines filters for streams of log data passing through a sink.</span></span>  

|<span data-ttu-id="7b511-423">Elemento</span><span class="sxs-lookup"><span data-stu-id="7b511-423">Element</span></span>|<span data-ttu-id="7b511-424">Escriba</span><span class="sxs-lookup"><span data-stu-id="7b511-424">Type</span></span>|<span data-ttu-id="7b511-425">Descripción</span><span class="sxs-lookup"><span data-stu-id="7b511-425">Description</span></span>|  
|-------------|----------|-----------------|  
|<span data-ttu-id="7b511-426">**Channel**</span><span class="sxs-lookup"><span data-stu-id="7b511-426">**Channel**</span></span>|<span data-ttu-id="7b511-427">string</span><span class="sxs-lookup"><span data-stu-id="7b511-427">string</span></span>|<span data-ttu-id="7b511-428">Consulte la descripción en cualquier parte de esta página.</span><span class="sxs-lookup"><span data-stu-id="7b511-428">See description elsewhere on this page.</span></span>|  

## <a name="channel-element"></a><span data-ttu-id="7b511-429">Elemento Channel</span><span class="sxs-lookup"><span data-stu-id="7b511-429">Channel Element</span></span>
 <span data-ttu-id="7b511-430">*Árbol: Raíz - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink - Channels - Channel*</span><span class="sxs-lookup"><span data-stu-id="7b511-430">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink - Channels - Channel*</span></span>

 <span data-ttu-id="7b511-431">Agregado en la versión 1.5.</span><span class="sxs-lookup"><span data-stu-id="7b511-431">Added in version 1.5.</span></span>  

 <span data-ttu-id="7b511-432">Define las ubicaciones donde se van a enviar datos de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="7b511-432">Defines locations to send diagnostic data to.</span></span> <span data-ttu-id="7b511-433">Por ejemplo, el servicio Application Insights.</span><span class="sxs-lookup"><span data-stu-id="7b511-433">For example, the Application Insights service.</span></span>  

|<span data-ttu-id="7b511-434">Atributos</span><span class="sxs-lookup"><span data-stu-id="7b511-434">Attributes</span></span>|<span data-ttu-id="7b511-435">Escriba</span><span class="sxs-lookup"><span data-stu-id="7b511-435">Type</span></span>|<span data-ttu-id="7b511-436">Descripción</span><span class="sxs-lookup"><span data-stu-id="7b511-436">Description</span></span>|  
|----------------|----------|-----------------|  
|<span data-ttu-id="7b511-437">**logLevel**</span><span class="sxs-lookup"><span data-stu-id="7b511-437">**logLevel**</span></span>|<span data-ttu-id="7b511-438">**cadena**</span><span class="sxs-lookup"><span data-stu-id="7b511-438">**string**</span></span>|<span data-ttu-id="7b511-439">Especifica el nivel de gravedad mínimo para las entradas de registro que se van a transferir.</span><span class="sxs-lookup"><span data-stu-id="7b511-439">Specifies the minimum severity level for log entries that are transferred.</span></span> <span data-ttu-id="7b511-440">El valor predeterminado es **Undefined**, que transfiere todos los registros.</span><span class="sxs-lookup"><span data-stu-id="7b511-440">The default value is **Undefined**, which transfers all logs.</span></span> <span data-ttu-id="7b511-441">Otros valores posibles (en orden de mayor a menor información) son **Verbose**, **Information**, **Warning**, **Error** y **Critical**.</span><span class="sxs-lookup"><span data-stu-id="7b511-441">Other possible values (in order of most to least information) are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span></span>|  
|<span data-ttu-id="7b511-442">**name**</span><span class="sxs-lookup"><span data-stu-id="7b511-442">**name**</span></span>|<span data-ttu-id="7b511-443">**cadena**</span><span class="sxs-lookup"><span data-stu-id="7b511-443">**string**</span></span>|<span data-ttu-id="7b511-444">Un nombre único del canal al que se hace referencia</span><span class="sxs-lookup"><span data-stu-id="7b511-444">A unique name of the channel to refer to</span></span>|  


## <a name="privateconfig-element"></a><span data-ttu-id="7b511-445">Elemento PrivateConfig</span><span class="sxs-lookup"><span data-stu-id="7b511-445">PrivateConfig Element</span></span> 
 <span data-ttu-id="7b511-446">*Árbol: Raíz - DiagnosticsConfiguration - PrivateConfig*</span><span class="sxs-lookup"><span data-stu-id="7b511-446">*Tree: Root - DiagnosticsConfiguration - PrivateConfig*</span></span>

 <span data-ttu-id="7b511-447">Agregado en la versión 1.3.</span><span class="sxs-lookup"><span data-stu-id="7b511-447">Added in version 1.3.</span></span>  

 <span data-ttu-id="7b511-448">Opcional</span><span class="sxs-lookup"><span data-stu-id="7b511-448">Optional</span></span>  

 <span data-ttu-id="7b511-449">Almacena los detalles privados de la cuenta de almacenamiento (nombre, clave y punto de conexión).</span><span class="sxs-lookup"><span data-stu-id="7b511-449">Stores the private details of the storage account (name, key, and endpoint).</span></span> <span data-ttu-id="7b511-450">Esta información se envía a la máquina virtual, pero no se puede recuperar de ella.</span><span class="sxs-lookup"><span data-stu-id="7b511-450">This information is sent to the virtual machine, but cannot be retrieved from it.</span></span>  

|<span data-ttu-id="7b511-451">Elementos secundarios</span><span class="sxs-lookup"><span data-stu-id="7b511-451">Child Elements</span></span>|<span data-ttu-id="7b511-452">Descripción</span><span class="sxs-lookup"><span data-stu-id="7b511-452">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="7b511-453">**StorageAccount**</span><span class="sxs-lookup"><span data-stu-id="7b511-453">**StorageAccount**</span></span>|<span data-ttu-id="7b511-454">La cuenta de almacenamiento que se va a usar.</span><span class="sxs-lookup"><span data-stu-id="7b511-454">The storage account to use.</span></span> <span data-ttu-id="7b511-455">Los atributos siguientes son necesarios</span><span class="sxs-lookup"><span data-stu-id="7b511-455">The following attributes are required</span></span><br /><br /> <span data-ttu-id="7b511-456">- **name**: el nombre de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="7b511-456">- **name** - The name of the storage account.</span></span><br /><br /> <span data-ttu-id="7b511-457">- **key**: la clave de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="7b511-457">- **key** - The key to the storage account.</span></span><br /><br /> <span data-ttu-id="7b511-458">- **endpoint**: el punto de conexión para acceder a la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="7b511-458">- **endpoint** - The endpoint to access the storage account.</span></span> <br /><br /> <span data-ttu-id="7b511-459">-**sasToken** (se agregó en la versión 1.8.1): puede especificar un token de SAS en lugar de una clave de cuenta de almacenamiento en la configuración privada.</span><span class="sxs-lookup"><span data-stu-id="7b511-459">-**sasToken** (added 1.8.1)- You can specify an SAS token instead of a storage account key in the private config.</span></span> <span data-ttu-id="7b511-460">Si se proporciona, se omite la clave de cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="7b511-460">If provided, the storage account key is ignored.</span></span> <br /><span data-ttu-id="7b511-461">Requisitos del token de SAS:</span><span class="sxs-lookup"><span data-stu-id="7b511-461">Requirements for the SAS Token:</span></span> <br /><span data-ttu-id="7b511-462">- Solo admite el token de SAS de la cuenta.</span><span class="sxs-lookup"><span data-stu-id="7b511-462">- Supports account SAS token only</span></span> <br /><span data-ttu-id="7b511-463">Se requieren los tipos de servicio - *b* y *t*.</span><span class="sxs-lookup"><span data-stu-id="7b511-463">- *b*, *t* service types are required.</span></span> <br /> <span data-ttu-id="7b511-464">Se requieren los permisos - *a*, *c*, *u* y *w*.</span><span class="sxs-lookup"><span data-stu-id="7b511-464">- *a*, *c*, *u*, *w* permissions are required.</span></span> <br /> <span data-ttu-id="7b511-465">Se requieren los tipos de recursos - *c* y *o*.</span><span class="sxs-lookup"><span data-stu-id="7b511-465">- *c*, *o* resource types are required.</span></span> <br /> <span data-ttu-id="7b511-466">- Solo admite únicamente el protocolo HTTPS.</span><span class="sxs-lookup"><span data-stu-id="7b511-466">- Supports the HTTPS protocol only</span></span> <br /> <span data-ttu-id="7b511-467">- La hora de inicio y de expiración debe ser válida.</span><span class="sxs-lookup"><span data-stu-id="7b511-467">- Start and expiry time must be valid.</span></span>|  


## <a name="isenabled-element"></a><span data-ttu-id="7b511-468">Elemento IsEnabled</span><span class="sxs-lookup"><span data-stu-id="7b511-468">IsEnabled Element</span></span>  
 <span data-ttu-id="7b511-469">*Árbol: Raíz - DiagnosticsConfiguration - IsEnabled*</span><span class="sxs-lookup"><span data-stu-id="7b511-469">*Tree: Root - DiagnosticsConfiguration - IsEnabled*</span></span>

 <span data-ttu-id="7b511-470">Booleano.</span><span class="sxs-lookup"><span data-stu-id="7b511-470">Boolean.</span></span> <span data-ttu-id="7b511-471">Use `true` para habilitar los diagnósticos o `false` para deshabilitarlos.</span><span class="sxs-lookup"><span data-stu-id="7b511-471">Use `true` to enable the diagnostics or `false` to disable the diagnostics.</span></span>
