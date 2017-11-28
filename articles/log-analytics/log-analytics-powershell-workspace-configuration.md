---
title: "Uso de PowerShell para crear y configurar un área de trabajo de Log Analytics | Microsoft Docs"
description: "Log Analytics usa datos de los servidores de la infraestructura local o de nube. Puede recopilar datos de equipo del almacenamiento de Azure cuando son generados por Diagnósticos de Azure."
services: log-analytics
documentationcenter: 
author: richrundmsft
manager: jochan
editor: 
ms.assetid: 3b9b7ade-3374-4596-afb1-51b695f481c2
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: powershell
ms.topic: article
ms.date: 11/21/2016
ms.author: richrund
ms.openlocfilehash: 6807ab67e3593da82c147669b29bfdae3b6c967c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="manage-log-analytics-using-powershell"></a><span data-ttu-id="30ec7-104">Administración de Log Analytics mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="30ec7-104">Manage Log Analytics using PowerShell</span></span>
<span data-ttu-id="30ec7-105">Puede usar los [cmdlets de PowerShell de Log Analytics](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) para realizar una serie de funciones en Log Analytics desde una línea de comandos o como parte de un script.</span><span class="sxs-lookup"><span data-stu-id="30ec7-105">You can use the [Log Analytics PowerShell cmdlets](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) to perform various functions in Log Analytics from a command line or as part of a script.</span></span>  <span data-ttu-id="30ec7-106">A continuación se indican algunos ejemplos de las tareas que puede realizar con PowerShell:</span><span class="sxs-lookup"><span data-stu-id="30ec7-106">Examples of the tasks you can perform with PowerShell include:</span></span>

* <span data-ttu-id="30ec7-107">Crear un área de trabajo</span><span class="sxs-lookup"><span data-stu-id="30ec7-107">Create a workspace</span></span>
* <span data-ttu-id="30ec7-108">Agregar o quitar una solución</span><span class="sxs-lookup"><span data-stu-id="30ec7-108">Add or remove a solution</span></span>
* <span data-ttu-id="30ec7-109">Importar y exportar búsquedas guardadas</span><span class="sxs-lookup"><span data-stu-id="30ec7-109">Import and export saved searches</span></span>
* <span data-ttu-id="30ec7-110">Crear un grupo de equipos</span><span class="sxs-lookup"><span data-stu-id="30ec7-110">Create a computer group</span></span>
* <span data-ttu-id="30ec7-111">Habilitar la recopilación de registros de IIS en equipos con el agente de Windows instalado</span><span class="sxs-lookup"><span data-stu-id="30ec7-111">Enable collection of IIS logs from computers with the Windows agent installed</span></span>
* <span data-ttu-id="30ec7-112">Recopilar contadores de rendimiento en equipos Linux y Windows</span><span class="sxs-lookup"><span data-stu-id="30ec7-112">Collect performance counters from Linux and Windows computers</span></span>
* <span data-ttu-id="30ec7-113">Recopilar eventos de Syslog en equipos Linux</span><span class="sxs-lookup"><span data-stu-id="30ec7-113">Collect events from syslog on Linux computers</span></span> 
* <span data-ttu-id="30ec7-114">Recopilar eventos de registros de eventos de Windows</span><span class="sxs-lookup"><span data-stu-id="30ec7-114">Collect events from Windows event logs</span></span>
* <span data-ttu-id="30ec7-115">Recopilar registros de eventos personalizados</span><span class="sxs-lookup"><span data-stu-id="30ec7-115">Collect custom event logs</span></span>
* <span data-ttu-id="30ec7-116">Agregar al agente de Log Analytics a una máquina virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="30ec7-116">Add the log analytics agent to an Azure virtual machine</span></span>
* <span data-ttu-id="30ec7-117">Configurar Log Analytics para indizar los datos recopilados mediante Diagnósticos de Azure</span><span class="sxs-lookup"><span data-stu-id="30ec7-117">Configure log analytics to index data collected using Azure diagnostics</span></span>

<span data-ttu-id="30ec7-118">Este artículo proporciona dos ejemplos de código que muestran algunas de las funciones que puede realizar desde PowerShell.</span><span class="sxs-lookup"><span data-stu-id="30ec7-118">This article provides two code samples that illustrate some of the functions that you can perform from PowerShell.</span></span>  <span data-ttu-id="30ec7-119">Puede consultar la [referencia de cmdlets de PowerShell de Log Analytics](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) para otras funciones.</span><span class="sxs-lookup"><span data-stu-id="30ec7-119">You can refer to the [Log Analytics PowerShell cmdlet reference](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) for other functions.</span></span>

> [!NOTE]
> <span data-ttu-id="30ec7-120">Log Analytics se llamaba anteriormente Operational Insights, razón por la cual se utiliza este nombre en los cmdlets.</span><span class="sxs-lookup"><span data-stu-id="30ec7-120">Log Analytics was previously called Operational Insights, which is why it is the name used in the cmdlets.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="30ec7-121">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="30ec7-121">Prerequisites</span></span>
<span data-ttu-id="30ec7-122">Estos ejemplos funcionan con la versión 2.3.0 o posteriores del módulo AzureRm.OperationalInsights.</span><span class="sxs-lookup"><span data-stu-id="30ec7-122">These examples work with version 2.3.0 or later of the AzureRm.OperationalInsights module.</span></span>


## <a name="create-and-configure-a-log-analytics-workspace"></a><span data-ttu-id="30ec7-123">Creación y configuración de un área de trabajo de Log Analytics</span><span class="sxs-lookup"><span data-stu-id="30ec7-123">Create and configure a Log Analytics Workspace</span></span>
<span data-ttu-id="30ec7-124">El siguiente ejemplo de script muestra cómo:</span><span class="sxs-lookup"><span data-stu-id="30ec7-124">The following script sample illustrates how to:</span></span>

1. <span data-ttu-id="30ec7-125">Crear un área de trabajo</span><span class="sxs-lookup"><span data-stu-id="30ec7-125">Create a workspace</span></span>
2. <span data-ttu-id="30ec7-126">Enumerar las soluciones disponibles</span><span class="sxs-lookup"><span data-stu-id="30ec7-126">List the available solutions</span></span>
3. <span data-ttu-id="30ec7-127">Agregar soluciones al área de trabajo</span><span class="sxs-lookup"><span data-stu-id="30ec7-127">Add solutions to the workspace</span></span>
4. <span data-ttu-id="30ec7-128">Importar búsquedas guardadas</span><span class="sxs-lookup"><span data-stu-id="30ec7-128">Import saved searches</span></span>
5. <span data-ttu-id="30ec7-129">Exportar búsquedas guardadas</span><span class="sxs-lookup"><span data-stu-id="30ec7-129">Export saved searches</span></span>
6. <span data-ttu-id="30ec7-130">Crear un grupo de equipos</span><span class="sxs-lookup"><span data-stu-id="30ec7-130">Create a computer group</span></span>
7. <span data-ttu-id="30ec7-131">Habilitar la recopilación de registros de IIS en equipos con el agente de Windows instalado</span><span class="sxs-lookup"><span data-stu-id="30ec7-131">Enable collection of IIS logs from computers with the Windows agent installed</span></span>
8. <span data-ttu-id="30ec7-132">Recopilar contadores de rendimiento de discos lógicos de equipos Linux (% de inodos usados; megabytes libres; % de espacio usado; transferencias de disco/seg.; lecturas de disco/seg.; escrituras de disco/seg.)</span><span class="sxs-lookup"><span data-stu-id="30ec7-132">Collect Logical Disk perf counters from Linux computers (% Used Inodes; Free Megabytes; % Used Space; Disk Transfers/sec; Disk Reads/sec; Disk Writes/sec)</span></span>
9. <span data-ttu-id="30ec7-133">Recopilar eventos de Syslog de equipos Linux</span><span class="sxs-lookup"><span data-stu-id="30ec7-133">Collect syslog events from Linux computers</span></span>
10. <span data-ttu-id="30ec7-134">Recopilar eventos de error y advertencia del registro de eventos de aplicación de los equipos de Windows</span><span class="sxs-lookup"><span data-stu-id="30ec7-134">Collect Error and Warning events from the Application Event Log from Windows computers</span></span>
11. <span data-ttu-id="30ec7-135">Recopilar contadores de rendimiento de MB disponibles de equipos Windows</span><span class="sxs-lookup"><span data-stu-id="30ec7-135">Collect Memory Available Mbytes performance counter from Windows computers</span></span>
12. <span data-ttu-id="30ec7-136">Recopilar registros personalizados</span><span class="sxs-lookup"><span data-stu-id="30ec7-136">Collect a custom log</span></span> 

```

$ResourceGroup = "oms-example"
$WorkspaceName = "log-analytics-" + (Get-Random -Maximum 99999) # workspace names need to be unique - Get-Random helps with this for the example code
$Location = "westeurope"

# List of solutions to enable
$Solutions = "Security", "Updates", "SQLAssessment"

# Saved Searches to import
$ExportedSearches = @"
[
    {
        "Category":  "My Saved Searches",
        "DisplayName":  "WAD Events (All)",
        "Query":  "Type=Event SourceSystem:AzureStorage ",
        "Version":  1
    },
    {        
        "Category":  "My Saved Searches",
        "DisplayName":  "Current Disk Queue Length",
        "Query":  "Type=Perf ObjectName=LogicalDisk InstanceName=\"C:\" CounterName=\"Current Disk Queue Length\"",
        "Version":  1
    }
]
"@ | ConvertFrom-Json

# Custom Log to collect
$CustomLog = @"
{
    "customLogName": "sampleCustomLog1", 
    "description": "Example custom log datasource", 
    "inputs": [
        { 
            "location": { 
            "fileSystemLocations": { 
                "windowsFileTypeLogPaths": [ "e:\\iis5\\*.log" ], 
                "linuxFileTypeLogPaths": [ "/var/logs" ] 
                } 
            }, 
        "recordDelimiter": { 
            "regexDelimiter": { 
                "pattern": "\\n", 
                "matchIndex": 0, 
                "matchIndexSpecified": true, 
                "numberedGroup": null 
                } 
            } 
        }
    ], 
    "extractions": [
        { 
            "extractionName": "TimeGenerated", 
            "extractionType": "DateTime", 
            "extractionProperties": { 
                "dateTimeExtraction": { 
                    "regex": null, 
                    "joinStringRegex": null 
                    } 
                } 
            }
        ] 
    }
"@

# Create the resource group if needed
try {
    Get-AzureRmResourceGroup -Name $ResourceGroup -ErrorAction Stop
} catch {
    New-AzureRmResourceGroup -Name $ResourceGroup -Location $Location
}

# Create the workspace
New-AzureRmOperationalInsightsWorkspace -Location $Location -Name $WorkspaceName -Sku Standard -ResourceGroupName $ResourceGroup

# List all solutions and their installation status
Get-AzureRmOperationalInsightsIntelligencePacks -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName

# Add solutions
foreach ($solution in $Solutions) {
    Set-AzureRmOperationalInsightsIntelligencePack -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName -IntelligencePackName $solution -Enabled $true
}

#List enabled solutions
(Get-AzureRmOperationalInsightsIntelligencePacks -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName).Where({($_.enabled -eq $true)})

# Import Saved Searches
foreach ($search in $ExportedSearches) {
    $id = $search.Category + "|" + $search.DisplayName
    New-AzureRmOperationalInsightsSavedSearch -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName -SavedSearchId $id -DisplayName $search.DisplayName -Category $search.Category -Query $search.Query -Version $search.Version
}

# Export Saved Searches
(Get-AzureRmOperationalInsightsSavedSearch -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName).Value.Properties | ConvertTo-Json 

# Create Computer Group based on a query
New-AzureRmOperationalInsightsComputerGroup -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName -SavedSearchId "My Web Servers" -DisplayName "Web Servers" -Category "My Saved Searches" -Query "Computer=""web*"" | distinct Computer" -Version 1

# Create a computer group based on names (up to 5000)
$computerGroup = """servername1.contoso.com"",""servername2.contoso.com"",""servername3.contoso.com"",""servername4.contoso.com"""
New-AzureRmOperationalInsightsComputerGroup -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName -SavedSearchId "My Named Servers" -DisplayName "Named Servers" -Category "My Saved Searches" -Query $computerGroup -Version 1

# Enable IIS Log Collection using agent
Enable-AzureRmOperationalInsightsIISLogCollection -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName

# Linux Perf
New-AzureRmOperationalInsightsLinuxPerformanceObjectDataSource -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName -ObjectName "Logical Disk" -InstanceName "*"  -CounterNames @("% Used Inodes", "Free Megabytes", "% Used Space", "Disk Transfers/sec", "Disk Reads/sec", "Disk Reads/sec", "Disk Writes/sec") -IntervalSeconds 20  -Name "Example Linux Disk Performance Counters"
Enable-AzureRmOperationalInsightsLinuxCustomLogCollection -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName

# Linux Syslog
New-AzureRmOperationalInsightsLinuxSyslogDataSource -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName -Facility "kern" -CollectEmergency -CollectAlert -CollectCritical -CollectError -CollectWarning -Name "Example kernal syslog collection"
Enable-AzureRmOperationalInsightsLinuxSyslogCollection -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName

# Windows Event
New-AzureRmOperationalInsightsWindowsEventDataSource -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName -EventLogName "Application" -CollectErrors -CollectWarnings -Name "Example Application Event Log"

# Windows Perf
New-AzureRmOperationalInsightsWindowsPerformanceCounterDataSource -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName -ObjectName "Memory" -InstanceName "*" -CounterName "Available MBytes" -IntervalSeconds 20 -Name "Example Windows Performance Counter"

# Custom Logs
New-AzureRmOperationalInsightsCustomLogDataSource -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName -CustomLogRawJson "$CustomLog" -Name "Example Custom Log Collection"

```

## <a name="configuring-log-analytics-to-index-azure-diagnostics"></a><span data-ttu-id="30ec7-137">Configuración de Log Analytics para indizar Diagnósticos de Azure</span><span class="sxs-lookup"><span data-stu-id="30ec7-137">Configuring Log Analytics to index Azure diagnostics</span></span>
<span data-ttu-id="30ec7-138">Para la supervisión de recursos de Azure sin agente, los recursos necesitan tener Diagnósticos de Azure habilitado y configurado para escribir en un área de trabajo de Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="30ec7-138">For agentless monitoring of Azure resources, the resources need to have Azure diagnostics enabled and configured to write to a Log Analytics workspace.</span></span> <span data-ttu-id="30ec7-139">Este método envía los datos directamente a Log Analytics y no requiere que los datos se escriban en una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="30ec7-139">This approach sends data directly to Log Analytics and does not require data to be written to a storage account.</span></span> <span data-ttu-id="30ec7-140">Los recursos admitidos son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="30ec7-140">Supported resources include:</span></span>

| <span data-ttu-id="30ec7-141">Tipo de recurso</span><span class="sxs-lookup"><span data-stu-id="30ec7-141">Resource Type</span></span> | <span data-ttu-id="30ec7-142">Registros</span><span class="sxs-lookup"><span data-stu-id="30ec7-142">Logs</span></span> | <span data-ttu-id="30ec7-143">Métricas</span><span class="sxs-lookup"><span data-stu-id="30ec7-143">Metrics</span></span> |
| --- | --- | --- |
| <span data-ttu-id="30ec7-144">Puertas de enlace de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="30ec7-144">Application Gateways</span></span>    | <span data-ttu-id="30ec7-145">Sí</span><span class="sxs-lookup"><span data-stu-id="30ec7-145">Yes</span></span> | <span data-ttu-id="30ec7-146">Sí</span><span class="sxs-lookup"><span data-stu-id="30ec7-146">Yes</span></span> |
| <span data-ttu-id="30ec7-147">Cuentas de automatización</span><span class="sxs-lookup"><span data-stu-id="30ec7-147">Automation accounts</span></span>     | <span data-ttu-id="30ec7-148">Sí</span><span class="sxs-lookup"><span data-stu-id="30ec7-148">Yes</span></span> | |
| <span data-ttu-id="30ec7-149">Cuentas de Batch</span><span class="sxs-lookup"><span data-stu-id="30ec7-149">Batch accounts</span></span>          | <span data-ttu-id="30ec7-150">Sí</span><span class="sxs-lookup"><span data-stu-id="30ec7-150">Yes</span></span> | <span data-ttu-id="30ec7-151">Sí</span><span class="sxs-lookup"><span data-stu-id="30ec7-151">Yes</span></span> |
| <span data-ttu-id="30ec7-152">Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="30ec7-152">Data Lake analytics</span></span>     | <span data-ttu-id="30ec7-153">yes</span><span class="sxs-lookup"><span data-stu-id="30ec7-153">Yes</span></span> | | 
| <span data-ttu-id="30ec7-154">Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="30ec7-154">Data Lake store</span></span>         | <span data-ttu-id="30ec7-155">Sí</span><span class="sxs-lookup"><span data-stu-id="30ec7-155">Yes</span></span> | |
| <span data-ttu-id="30ec7-156">Elastic SQL Pool</span><span class="sxs-lookup"><span data-stu-id="30ec7-156">Elastic SQL Pool</span></span>        |     | <span data-ttu-id="30ec7-157">Sí</span><span class="sxs-lookup"><span data-stu-id="30ec7-157">Yes</span></span> |
| <span data-ttu-id="30ec7-158">Espacio de nombres del Centro de eventos</span><span class="sxs-lookup"><span data-stu-id="30ec7-158">Event Hub namespace</span></span>     |     | <span data-ttu-id="30ec7-159">Sí</span><span class="sxs-lookup"><span data-stu-id="30ec7-159">Yes</span></span> |
| <span data-ttu-id="30ec7-160">IoT Hubs</span><span class="sxs-lookup"><span data-stu-id="30ec7-160">IoT Hubs</span></span>                |     | <span data-ttu-id="30ec7-161">Sí</span><span class="sxs-lookup"><span data-stu-id="30ec7-161">Yes</span></span> |
| <span data-ttu-id="30ec7-162">Key Vault</span><span class="sxs-lookup"><span data-stu-id="30ec7-162">Key Vault</span></span>               | <span data-ttu-id="30ec7-163">Sí</span><span class="sxs-lookup"><span data-stu-id="30ec7-163">Yes</span></span> | |
| <span data-ttu-id="30ec7-164">Equilibradores de carga</span><span class="sxs-lookup"><span data-stu-id="30ec7-164">Load Balancers</span></span>          | <span data-ttu-id="30ec7-165">Sí</span><span class="sxs-lookup"><span data-stu-id="30ec7-165">Yes</span></span> | |
| <span data-ttu-id="30ec7-166">Logic Apps</span><span class="sxs-lookup"><span data-stu-id="30ec7-166">Logic Apps</span></span>              | <span data-ttu-id="30ec7-167">yes</span><span class="sxs-lookup"><span data-stu-id="30ec7-167">Yes</span></span> | <span data-ttu-id="30ec7-168">Sí</span><span class="sxs-lookup"><span data-stu-id="30ec7-168">Yes</span></span> |
| <span data-ttu-id="30ec7-169">Grupos de seguridad de red</span><span class="sxs-lookup"><span data-stu-id="30ec7-169">Network Security Groups</span></span> | <span data-ttu-id="30ec7-170">Sí</span><span class="sxs-lookup"><span data-stu-id="30ec7-170">Yes</span></span> | |
| <span data-ttu-id="30ec7-171">Caché en Redis</span><span class="sxs-lookup"><span data-stu-id="30ec7-171">Redis Cache</span></span>             |     | <span data-ttu-id="30ec7-172">yes</span><span class="sxs-lookup"><span data-stu-id="30ec7-172">Yes</span></span> |
| <span data-ttu-id="30ec7-173">Servicios de búsqueda</span><span class="sxs-lookup"><span data-stu-id="30ec7-173">Search services</span></span>         | <span data-ttu-id="30ec7-174">Sí</span><span class="sxs-lookup"><span data-stu-id="30ec7-174">Yes</span></span> | <span data-ttu-id="30ec7-175">Sí</span><span class="sxs-lookup"><span data-stu-id="30ec7-175">Yes</span></span> |
| <span data-ttu-id="30ec7-176">Espacio de nombres de Bus de servicio</span><span class="sxs-lookup"><span data-stu-id="30ec7-176">Service Bus namespace</span></span>   |     | <span data-ttu-id="30ec7-177">Sí</span><span class="sxs-lookup"><span data-stu-id="30ec7-177">Yes</span></span> |
| <span data-ttu-id="30ec7-178">SQL (v12)</span><span class="sxs-lookup"><span data-stu-id="30ec7-178">SQL (v12)</span></span>               |     | <span data-ttu-id="30ec7-179">Sí</span><span class="sxs-lookup"><span data-stu-id="30ec7-179">Yes</span></span> |
| <span data-ttu-id="30ec7-180">Sitios web</span><span class="sxs-lookup"><span data-stu-id="30ec7-180">Web Sites</span></span>               |     | <span data-ttu-id="30ec7-181">yes</span><span class="sxs-lookup"><span data-stu-id="30ec7-181">Yes</span></span> |
| <span data-ttu-id="30ec7-182">Granjas de servidores web</span><span class="sxs-lookup"><span data-stu-id="30ec7-182">Web Server farms</span></span>        |     | <span data-ttu-id="30ec7-183">yes</span><span class="sxs-lookup"><span data-stu-id="30ec7-183">Yes</span></span> |

<span data-ttu-id="30ec7-184">Para obtener información detallada sobre las métricas disponibles, consulte las [métricas admitidas con Azure Monitor](../monitoring-and-diagnostics/monitoring-supported-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="30ec7-184">For the details of the available metrics, refer to [supported metrics with Azure Monitor](../monitoring-and-diagnostics/monitoring-supported-metrics.md).</span></span>

<span data-ttu-id="30ec7-185">Para obtener información detallada sobre los registros disponibles, consulte los [servicios admitidos y el esquema de los registros de diagnóstico](../monitoring-and-diagnostics/monitoring-diagnostic-logs-schema.md).</span><span class="sxs-lookup"><span data-stu-id="30ec7-185">For the details of the available logs, refer to [supported services and schema for diagnostic logs](../monitoring-and-diagnostics/monitoring-diagnostic-logs-schema.md).</span></span>

```
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$resourceId = "/SUBSCRIPTIONS/ec11ca60-1234-491e-5678-0ea07feae25c/RESOURCEGROUPS/DEMO/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/DEMO" 

Set-AzureRmDiagnosticSetting -ResourceId $resourceId -WorkspaceId $workspaceId -Enabled $true
```

<span data-ttu-id="30ec7-186">También puede usar el cmdlet anterior para recopilar registros de recursos que se encuentran en distintas suscripciones.</span><span class="sxs-lookup"><span data-stu-id="30ec7-186">You can also use the preceding cmdlet to collect logs from resources that are in different subscriptions.</span></span> <span data-ttu-id="30ec7-187">El cmdlet funciona en suscripciones distintas porque se proporciona tanto el identificador del recurso que crea los registros y como el del área de trabajo al que se envían los registros.</span><span class="sxs-lookup"><span data-stu-id="30ec7-187">The cmdlet is able to work across subscriptions since you are providing the id of both the resource creating logs and the workspace the logs are sent to.</span></span>


## <a name="configuring-log-analytics-to-index-azure-diagnostics-from-storage"></a><span data-ttu-id="30ec7-188">Configuración de Log Analytics para indizar diagnósticos de Azure desde el almacenamiento</span><span class="sxs-lookup"><span data-stu-id="30ec7-188">Configuring Log Analytics to index Azure diagnostics from storage</span></span>
<span data-ttu-id="30ec7-189">Para recopilar datos de registro desde una instancia en ejecución de un servicio en la nube clásico o un clúster de Service Fabric, tiene que escribir primero los datos en Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="30ec7-189">To collect log data from within a running instance of a classic cloud service or a service fabric cluster, you need to first write the data to Azure storage.</span></span> <span data-ttu-id="30ec7-190">Después, Log Analytics se puede configurar para recopilar los registros de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="30ec7-190">Log Analytics is then configured to collect the logs from the storage account.</span></span> <span data-ttu-id="30ec7-191">Los recursos admitidos son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="30ec7-191">Supported resources include:</span></span>

* <span data-ttu-id="30ec7-192">Servicios en la nube clásicos (roles web y de trabajo)</span><span class="sxs-lookup"><span data-stu-id="30ec7-192">Classic cloud services (web and worker roles)</span></span>
* <span data-ttu-id="30ec7-193">Clústeres de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="30ec7-193">Service fabric clusters</span></span>

<span data-ttu-id="30ec7-194">El ejemplo siguiente muestra cómo:</span><span class="sxs-lookup"><span data-stu-id="30ec7-194">The following example shows how to:</span></span>

1. <span data-ttu-id="30ec7-195">Enumerar las cuentas de almacenamiento existentes y las ubicaciones desde las que Log Analytics indizará datos</span><span class="sxs-lookup"><span data-stu-id="30ec7-195">List the existing storage accounts and locations that Log Analytics will index data from</span></span>
2. <span data-ttu-id="30ec7-196">Crear una configuración para leer desde una cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="30ec7-196">Create a configuration to read from a storage account</span></span>
3. <span data-ttu-id="30ec7-197">Actualizar la configuración recién creada para indizar datos desde ubicaciones adicionales</span><span class="sxs-lookup"><span data-stu-id="30ec7-197">Update the newly created configuration to index data from additional locations</span></span>
4. <span data-ttu-id="30ec7-198">Eliminar la configuración recién creada</span><span class="sxs-lookup"><span data-stu-id="30ec7-198">Delete the newly created configuration</span></span>

```
# validTables = "WADWindowsEventLogsTable", "LinuxsyslogVer2v0", "WADServiceFabric*EventTable", "WADETWEventTable" 
$workspace = (Get-AzureRmOperationalInsightsWorkspace).Where({$_.Name -eq "your workspace name"})

# Update these two lines with the storage account resource ID and the storage account key for the storage account you want to Log Analytics to  
$storageId = "/subscriptions/ec11ca60-1234-491e-5678-0ea07feae25c/resourceGroups/demo/providers/Microsoft.Storage/storageAccounts/wadv2storage"
$key = "abcd=="

# List existing insights
Get-AzureRmOperationalInsightsStorageInsight -ResourceGroupName $workspace.ResourceGroupName -WorkspaceName $workspace.Name

# Create a new insight
New-AzureRmOperationalInsightsStorageInsight -ResourceGroupName $workspace.ResourceGroupName -WorkspaceName $workspace.Name -Name "newinsight" -StorageAccountResourceId $storageId -StorageAccountKey $key -Tables @("WADWindowsEventLogsTable") -Containers @("wad-iis-logfiles")

# Update existing insight
Set-AzureRmOperationalInsightsStorageInsight -ResourceGroupName $workspace.ResourceGroupName -WorkspaceName $workspace.Name -Name "newinsight" -Tables @("WADWindowsEventLogsTable", "WADETWEventTable") -Containers @("wad-iis-logfiles")

# Remove the insight
Remove-AzureRmOperationalInsightsStorageInsight -ResourceGroupName $workspace.ResourceGroupName -WorkspaceName $workspace.Name -Name "newinsight" 

```

<span data-ttu-id="30ec7-199">También puede usar el script anterior para recopilar registros de cuentas de almacenamiento que se encuentran en distintas suscripciones.</span><span class="sxs-lookup"><span data-stu-id="30ec7-199">You can also use the preceding script to collect logs from storage accounts in different subscriptions.</span></span> <span data-ttu-id="30ec7-200">El script funciona en suscripciones distintas porque se proporciona tanto el identificador del recurso de cuenta de almacenamiento como la clave de acceso correspondiente.</span><span class="sxs-lookup"><span data-stu-id="30ec7-200">The script is able to work across subscriptions since you are providing the storage account resource id and a corresponding access key.</span></span> <span data-ttu-id="30ec7-201">Cuando se cambia la clave de acceso, hay que actualizar los datos del almacenamiento para que tenga la nueva clave.</span><span class="sxs-lookup"><span data-stu-id="30ec7-201">When you change the access key, you need to update the storage insight to have the new key.</span></span>


## <a name="next-steps"></a><span data-ttu-id="30ec7-202">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="30ec7-202">Next steps</span></span>
* <span data-ttu-id="30ec7-203">[Revise los cmdlets de PowerShell de Log Analytics](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) para obtener información adicional sobre cómo usar PowerShell para la configuración de Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="30ec7-203">[Review Log Analytics PowerShell cmdlets](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) for additional information on using PowerShell for configuration of Log Analytics.</span></span>

