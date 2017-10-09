---
title: "aaaUse PowerShell tooCreate y configurar un área de trabajo de análisis de registro | Documentos de Microsoft"
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
ms.openlocfilehash: a6d66194204cc58de6aafb687a19fe9611e0c58e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-log-analytics-using-powershell"></a><span data-ttu-id="b8d98-104">Administración de Log Analytics mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="b8d98-104">Manage Log Analytics using PowerShell</span></span>
<span data-ttu-id="b8d98-105">Puede usar hello [cmdlets de PowerShell de análisis de registro](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) tooperform varias funciones de análisis de registros desde una línea de comandos o como parte de una secuencia de comandos.</span><span class="sxs-lookup"><span data-stu-id="b8d98-105">You can use hello [Log Analytics PowerShell cmdlets](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) tooperform various functions in Log Analytics from a command line or as part of a script.</span></span>  <span data-ttu-id="b8d98-106">Ejemplos de tareas de Hola que puede realizar con PowerShell:</span><span class="sxs-lookup"><span data-stu-id="b8d98-106">Examples of hello tasks you can perform with PowerShell include:</span></span>

* <span data-ttu-id="b8d98-107">Crear un área de trabajo</span><span class="sxs-lookup"><span data-stu-id="b8d98-107">Create a workspace</span></span>
* <span data-ttu-id="b8d98-108">Agregar o quitar una solución</span><span class="sxs-lookup"><span data-stu-id="b8d98-108">Add or remove a solution</span></span>
* <span data-ttu-id="b8d98-109">Importar y exportar búsquedas guardadas</span><span class="sxs-lookup"><span data-stu-id="b8d98-109">Import and export saved searches</span></span>
* <span data-ttu-id="b8d98-110">Crear un grupo de equipos</span><span class="sxs-lookup"><span data-stu-id="b8d98-110">Create a computer group</span></span>
* <span data-ttu-id="b8d98-111">Habilitar la recopilación de registros de IIS desde equipos que tengan instalado el agente de Windows hello</span><span class="sxs-lookup"><span data-stu-id="b8d98-111">Enable collection of IIS logs from computers with hello Windows agent installed</span></span>
* <span data-ttu-id="b8d98-112">Recopilar contadores de rendimiento en equipos Linux y Windows</span><span class="sxs-lookup"><span data-stu-id="b8d98-112">Collect performance counters from Linux and Windows computers</span></span>
* <span data-ttu-id="b8d98-113">Recopilar eventos de Syslog en equipos Linux</span><span class="sxs-lookup"><span data-stu-id="b8d98-113">Collect events from syslog on Linux computers</span></span> 
* <span data-ttu-id="b8d98-114">Recopilar eventos de registros de eventos de Windows</span><span class="sxs-lookup"><span data-stu-id="b8d98-114">Collect events from Windows event logs</span></span>
* <span data-ttu-id="b8d98-115">Recopilar registros de eventos personalizados</span><span class="sxs-lookup"><span data-stu-id="b8d98-115">Collect custom event logs</span></span>
* <span data-ttu-id="b8d98-116">Agregar tooan de agente de análisis de registro de hello máquina virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="b8d98-116">Add hello log analytics agent tooan Azure virtual machine</span></span>
* <span data-ttu-id="b8d98-117">Configurar datos de tooindex de análisis de registro recopilados con diagnósticos de Azure</span><span class="sxs-lookup"><span data-stu-id="b8d98-117">Configure log analytics tooindex data collected using Azure diagnostics</span></span>

<span data-ttu-id="b8d98-118">Este artículo proporciona dos ejemplos de código que muestran algunas de las funciones de Hola que puede realizar desde PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b8d98-118">This article provides two code samples that illustrate some of hello functions that you can perform from PowerShell.</span></span>  <span data-ttu-id="b8d98-119">Puede hacer referencia a toohello [referencia de cmdlets de PowerShell de análisis de registro](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) para otras funciones.</span><span class="sxs-lookup"><span data-stu-id="b8d98-119">You can refer toohello [Log Analytics PowerShell cmdlet reference](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) for other functions.</span></span>

> [!NOTE]
> <span data-ttu-id="b8d98-120">Análisis de registros se llamaba anteriormente visión operativa, motivo por el cual es nombre de hello usado en los cmdlets de Hola.</span><span class="sxs-lookup"><span data-stu-id="b8d98-120">Log Analytics was previously called Operational Insights, which is why it is hello name used in hello cmdlets.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="b8d98-121">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="b8d98-121">Prerequisites</span></span>
<span data-ttu-id="b8d98-122">Estos ejemplos de trabajo con la versión 2.3.0 o posterior del módulo de AzureRm.OperationalInsights Hola.</span><span class="sxs-lookup"><span data-stu-id="b8d98-122">These examples work with version 2.3.0 or later of hello AzureRm.OperationalInsights module.</span></span>


## <a name="create-and-configure-a-log-analytics-workspace"></a><span data-ttu-id="b8d98-123">Creación y configuración de un área de trabajo de Log Analytics</span><span class="sxs-lookup"><span data-stu-id="b8d98-123">Create and configure a Log Analytics Workspace</span></span>
<span data-ttu-id="b8d98-124">Hello ejemplo de secuencia de comandos siguiente se muestra cómo:</span><span class="sxs-lookup"><span data-stu-id="b8d98-124">hello following script sample illustrates how to:</span></span>

1. <span data-ttu-id="b8d98-125">Crear un área de trabajo</span><span class="sxs-lookup"><span data-stu-id="b8d98-125">Create a workspace</span></span>
2. <span data-ttu-id="b8d98-126">Soluciones de lista Hola disponibles</span><span class="sxs-lookup"><span data-stu-id="b8d98-126">List hello available solutions</span></span>
3. <span data-ttu-id="b8d98-127">Agregar área de trabajo de soluciones toohello</span><span class="sxs-lookup"><span data-stu-id="b8d98-127">Add solutions toohello workspace</span></span>
4. <span data-ttu-id="b8d98-128">Importar búsquedas guardadas</span><span class="sxs-lookup"><span data-stu-id="b8d98-128">Import saved searches</span></span>
5. <span data-ttu-id="b8d98-129">Exportar búsquedas guardadas</span><span class="sxs-lookup"><span data-stu-id="b8d98-129">Export saved searches</span></span>
6. <span data-ttu-id="b8d98-130">Crear un grupo de equipos</span><span class="sxs-lookup"><span data-stu-id="b8d98-130">Create a computer group</span></span>
7. <span data-ttu-id="b8d98-131">Habilitar la recopilación de registros de IIS desde equipos que tengan instalado el agente de Windows hello</span><span class="sxs-lookup"><span data-stu-id="b8d98-131">Enable collection of IIS logs from computers with hello Windows agent installed</span></span>
8. <span data-ttu-id="b8d98-132">Recopilar contadores de rendimiento de discos lógicos de equipos Linux (% de inodos usados; megabytes libres; % de espacio usado; transferencias de disco/seg.; lecturas de disco/seg.; escrituras de disco/seg.)</span><span class="sxs-lookup"><span data-stu-id="b8d98-132">Collect Logical Disk perf counters from Linux computers (% Used Inodes; Free Megabytes; % Used Space; Disk Transfers/sec; Disk Reads/sec; Disk Writes/sec)</span></span>
9. <span data-ttu-id="b8d98-133">Recopilar eventos de Syslog de equipos Linux</span><span class="sxs-lookup"><span data-stu-id="b8d98-133">Collect syslog events from Linux computers</span></span>
10. <span data-ttu-id="b8d98-134">Recopilar eventos de Error y advertencia de hello registro de eventos de aplicación de los equipos de Windows</span><span class="sxs-lookup"><span data-stu-id="b8d98-134">Collect Error and Warning events from hello Application Event Log from Windows computers</span></span>
11. <span data-ttu-id="b8d98-135">Recopilar contadores de rendimiento de MB disponibles de equipos Windows</span><span class="sxs-lookup"><span data-stu-id="b8d98-135">Collect Memory Available Mbytes performance counter from Windows computers</span></span>
12. <span data-ttu-id="b8d98-136">Recopilar registros personalizados</span><span class="sxs-lookup"><span data-stu-id="b8d98-136">Collect a custom log</span></span> 

```

$ResourceGroup = "oms-example"
$WorkspaceName = "log-analytics-" + (Get-Random -Maximum 99999) # workspace names need toobe unique - Get-Random helps with this for hello example code
$Location = "westeurope"

# List of solutions tooenable
$Solutions = "Security", "Updates", "SQLAssessment"

# Saved Searches tooimport
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

# Custom Log toocollect
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

# Create hello resource group if needed
try {
    Get-AzureRmResourceGroup -Name $ResourceGroup -ErrorAction Stop
} catch {
    New-AzureRmResourceGroup -Name $ResourceGroup -Location $Location
}

# Create hello workspace
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

# Create a computer group based on names (up too5000)
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

## <a name="configuring-log-analytics-tooindex-azure-diagnostics"></a><span data-ttu-id="b8d98-137">Configuración de análisis de registros tooindex diagnósticos de Azure</span><span class="sxs-lookup"><span data-stu-id="b8d98-137">Configuring Log Analytics tooindex Azure diagnostics</span></span>
<span data-ttu-id="b8d98-138">Para la supervisión de recursos de Azure, recursos de hello deben toohave área de trabajo de diagnóstico de Azure habilitado y configurado toowrite tooa análisis de registros.</span><span class="sxs-lookup"><span data-stu-id="b8d98-138">For agentless monitoring of Azure resources, hello resources need toohave Azure diagnostics enabled and configured toowrite tooa Log Analytics workspace.</span></span> <span data-ttu-id="b8d98-139">Este método envía datos directamente tooLog análisis y no requiere toobe de datos escrito tooa cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="b8d98-139">This approach sends data directly tooLog Analytics and does not require data toobe written tooa storage account.</span></span> <span data-ttu-id="b8d98-140">Los recursos admitidos son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="b8d98-140">Supported resources include:</span></span>

| <span data-ttu-id="b8d98-141">Tipo de recurso</span><span class="sxs-lookup"><span data-stu-id="b8d98-141">Resource Type</span></span> | <span data-ttu-id="b8d98-142">Registros</span><span class="sxs-lookup"><span data-stu-id="b8d98-142">Logs</span></span> | <span data-ttu-id="b8d98-143">Métricas</span><span class="sxs-lookup"><span data-stu-id="b8d98-143">Metrics</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b8d98-144">Puertas de enlace de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="b8d98-144">Application Gateways</span></span>    | <span data-ttu-id="b8d98-145">Sí</span><span class="sxs-lookup"><span data-stu-id="b8d98-145">Yes</span></span> | <span data-ttu-id="b8d98-146">Sí</span><span class="sxs-lookup"><span data-stu-id="b8d98-146">Yes</span></span> |
| <span data-ttu-id="b8d98-147">Cuentas de automatización</span><span class="sxs-lookup"><span data-stu-id="b8d98-147">Automation accounts</span></span>     | <span data-ttu-id="b8d98-148">Sí</span><span class="sxs-lookup"><span data-stu-id="b8d98-148">Yes</span></span> | |
| <span data-ttu-id="b8d98-149">Cuentas de Batch</span><span class="sxs-lookup"><span data-stu-id="b8d98-149">Batch accounts</span></span>          | <span data-ttu-id="b8d98-150">Sí</span><span class="sxs-lookup"><span data-stu-id="b8d98-150">Yes</span></span> | <span data-ttu-id="b8d98-151">Sí</span><span class="sxs-lookup"><span data-stu-id="b8d98-151">Yes</span></span> |
| <span data-ttu-id="b8d98-152">Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="b8d98-152">Data Lake analytics</span></span>     | <span data-ttu-id="b8d98-153">yes</span><span class="sxs-lookup"><span data-stu-id="b8d98-153">Yes</span></span> | | 
| <span data-ttu-id="b8d98-154">Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="b8d98-154">Data Lake store</span></span>         | <span data-ttu-id="b8d98-155">Sí</span><span class="sxs-lookup"><span data-stu-id="b8d98-155">Yes</span></span> | |
| <span data-ttu-id="b8d98-156">Elastic SQL Pool</span><span class="sxs-lookup"><span data-stu-id="b8d98-156">Elastic SQL Pool</span></span>        |     | <span data-ttu-id="b8d98-157">Sí</span><span class="sxs-lookup"><span data-stu-id="b8d98-157">Yes</span></span> |
| <span data-ttu-id="b8d98-158">Espacio de nombres del Centro de eventos</span><span class="sxs-lookup"><span data-stu-id="b8d98-158">Event Hub namespace</span></span>     |     | <span data-ttu-id="b8d98-159">Sí</span><span class="sxs-lookup"><span data-stu-id="b8d98-159">Yes</span></span> |
| <span data-ttu-id="b8d98-160">IoT Hubs</span><span class="sxs-lookup"><span data-stu-id="b8d98-160">IoT Hubs</span></span>                |     | <span data-ttu-id="b8d98-161">Sí</span><span class="sxs-lookup"><span data-stu-id="b8d98-161">Yes</span></span> |
| <span data-ttu-id="b8d98-162">Key Vault</span><span class="sxs-lookup"><span data-stu-id="b8d98-162">Key Vault</span></span>               | <span data-ttu-id="b8d98-163">Sí</span><span class="sxs-lookup"><span data-stu-id="b8d98-163">Yes</span></span> | |
| <span data-ttu-id="b8d98-164">Equilibradores de carga</span><span class="sxs-lookup"><span data-stu-id="b8d98-164">Load Balancers</span></span>          | <span data-ttu-id="b8d98-165">Sí</span><span class="sxs-lookup"><span data-stu-id="b8d98-165">Yes</span></span> | |
| <span data-ttu-id="b8d98-166">Logic Apps</span><span class="sxs-lookup"><span data-stu-id="b8d98-166">Logic Apps</span></span>              | <span data-ttu-id="b8d98-167">yes</span><span class="sxs-lookup"><span data-stu-id="b8d98-167">Yes</span></span> | <span data-ttu-id="b8d98-168">Sí</span><span class="sxs-lookup"><span data-stu-id="b8d98-168">Yes</span></span> |
| <span data-ttu-id="b8d98-169">Grupos de seguridad de red</span><span class="sxs-lookup"><span data-stu-id="b8d98-169">Network Security Groups</span></span> | <span data-ttu-id="b8d98-170">Sí</span><span class="sxs-lookup"><span data-stu-id="b8d98-170">Yes</span></span> | |
| <span data-ttu-id="b8d98-171">Caché en Redis</span><span class="sxs-lookup"><span data-stu-id="b8d98-171">Redis Cache</span></span>             |     | <span data-ttu-id="b8d98-172">yes</span><span class="sxs-lookup"><span data-stu-id="b8d98-172">Yes</span></span> |
| <span data-ttu-id="b8d98-173">Servicios de búsqueda</span><span class="sxs-lookup"><span data-stu-id="b8d98-173">Search services</span></span>         | <span data-ttu-id="b8d98-174">Sí</span><span class="sxs-lookup"><span data-stu-id="b8d98-174">Yes</span></span> | <span data-ttu-id="b8d98-175">Sí</span><span class="sxs-lookup"><span data-stu-id="b8d98-175">Yes</span></span> |
| <span data-ttu-id="b8d98-176">Espacio de nombres de Bus de servicio</span><span class="sxs-lookup"><span data-stu-id="b8d98-176">Service Bus namespace</span></span>   |     | <span data-ttu-id="b8d98-177">Sí</span><span class="sxs-lookup"><span data-stu-id="b8d98-177">Yes</span></span> |
| <span data-ttu-id="b8d98-178">SQL (v12)</span><span class="sxs-lookup"><span data-stu-id="b8d98-178">SQL (v12)</span></span>               |     | <span data-ttu-id="b8d98-179">Sí</span><span class="sxs-lookup"><span data-stu-id="b8d98-179">Yes</span></span> |
| <span data-ttu-id="b8d98-180">Sitios web</span><span class="sxs-lookup"><span data-stu-id="b8d98-180">Web Sites</span></span>               |     | <span data-ttu-id="b8d98-181">yes</span><span class="sxs-lookup"><span data-stu-id="b8d98-181">Yes</span></span> |
| <span data-ttu-id="b8d98-182">Granjas de servidores web</span><span class="sxs-lookup"><span data-stu-id="b8d98-182">Web Server farms</span></span>        |     | <span data-ttu-id="b8d98-183">Sí</span><span class="sxs-lookup"><span data-stu-id="b8d98-183">Yes</span></span> |

<span data-ttu-id="b8d98-184">Para obtener detalles de Hola de métricas disponibles hello, consulte demasiado[métricas con el Monitor de Azure admitidas](../monitoring-and-diagnostics/monitoring-supported-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="b8d98-184">For hello details of hello available metrics, refer too[supported metrics with Azure Monitor](../monitoring-and-diagnostics/monitoring-supported-metrics.md).</span></span>

<span data-ttu-id="b8d98-185">Para obtener detalles de Hola de registros disponibles de hello, consulte demasiado[admite servicios y el esquema para los registros de diagnóstico](../monitoring-and-diagnostics/monitoring-diagnostic-logs-schema.md).</span><span class="sxs-lookup"><span data-stu-id="b8d98-185">For hello details of hello available logs, refer too[supported services and schema for diagnostic logs](../monitoring-and-diagnostics/monitoring-diagnostic-logs-schema.md).</span></span>

```
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$resourceId = "/SUBSCRIPTIONS/ec11ca60-1234-491e-5678-0ea07feae25c/RESOURCEGROUPS/DEMO/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/DEMO" 

Set-AzureRmDiagnosticSetting -ResourceId $resourceId -WorkspaceId $workspaceId -Enabled $true
```

<span data-ttu-id="b8d98-186">También puede utilizar Hola anterior cmdlet toocollect registros de recursos que se encuentran en distintas suscripciones.</span><span class="sxs-lookup"><span data-stu-id="b8d98-186">You can also use hello preceding cmdlet toocollect logs from resources that are in different subscriptions.</span></span> <span data-ttu-id="b8d98-187">cmdlet de Hello es toowork capaz de a través de suscripciones desde que se envían los registros de Hola de área de trabajo de Hola y va a proporcionar el Id. de Hola de ambos recursos Hola crear registros.</span><span class="sxs-lookup"><span data-stu-id="b8d98-187">hello cmdlet is able toowork across subscriptions since you are providing hello id of both hello resource creating logs and hello workspace hello logs are sent to.</span></span>


## <a name="configuring-log-analytics-tooindex-azure-diagnostics-from-storage"></a><span data-ttu-id="b8d98-188">Configuración de diagnósticos de Azure desde el almacenamiento del análisis de registros tooindex</span><span class="sxs-lookup"><span data-stu-id="b8d98-188">Configuring Log Analytics tooindex Azure diagnostics from storage</span></span>
<span data-ttu-id="b8d98-189">datos del registro toocollect desde dentro de una instancia en ejecución de un servicio de nube clásico o un clúster de service fabric, necesita almacenamiento de tooAzure de toofirst escritura Hola datos.</span><span class="sxs-lookup"><span data-stu-id="b8d98-189">toocollect log data from within a running instance of a classic cloud service or a service fabric cluster, you need toofirst write hello data tooAzure storage.</span></span> <span data-ttu-id="b8d98-190">Análisis de registros es, a continuación, configurar registros de hello toocollect de cuenta de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="b8d98-190">Log Analytics is then configured toocollect hello logs from hello storage account.</span></span> <span data-ttu-id="b8d98-191">Los recursos admitidos son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="b8d98-191">Supported resources include:</span></span>

* <span data-ttu-id="b8d98-192">Servicios en la nube clásicos (roles web y de trabajo)</span><span class="sxs-lookup"><span data-stu-id="b8d98-192">Classic cloud services (web and worker roles)</span></span>
* <span data-ttu-id="b8d98-193">Clústeres de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="b8d98-193">Service fabric clusters</span></span>

<span data-ttu-id="b8d98-194">Hola siguiente ejemplo se muestra cómo para:</span><span class="sxs-lookup"><span data-stu-id="b8d98-194">hello following example shows how to:</span></span>

1. <span data-ttu-id="b8d98-195">Lista de cuentas de almacenamiento existentes de Hola y ubicaciones de análisis de registros se indizarán los datos de</span><span class="sxs-lookup"><span data-stu-id="b8d98-195">List hello existing storage accounts and locations that Log Analytics will index data from</span></span>
2. <span data-ttu-id="b8d98-196">Crear un tooread de configuración de una cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="b8d98-196">Create a configuration tooread from a storage account</span></span>
3. <span data-ttu-id="b8d98-197">Hola actualización que acaba de crear datos de configuración tooindex desde ubicaciones adicionales</span><span class="sxs-lookup"><span data-stu-id="b8d98-197">Update hello newly created configuration tooindex data from additional locations</span></span>
4. <span data-ttu-id="b8d98-198">Eliminar la configuración de hello recién creado</span><span class="sxs-lookup"><span data-stu-id="b8d98-198">Delete hello newly created configuration</span></span>

```
# validTables = "WADWindowsEventLogsTable", "LinuxsyslogVer2v0", "WADServiceFabric*EventTable", "WADETWEventTable" 
$workspace = (Get-AzureRmOperationalInsightsWorkspace).Where({$_.Name -eq "your workspace name"})

# Update these two lines with hello storage account resource ID and hello storage account key for hello storage account you want tooLog Analytics too 
$storageId = "/subscriptions/ec11ca60-1234-491e-5678-0ea07feae25c/resourceGroups/demo/providers/Microsoft.Storage/storageAccounts/wadv2storage"
$key = "abcd=="

# List existing insights
Get-AzureRmOperationalInsightsStorageInsight -ResourceGroupName $workspace.ResourceGroupName -WorkspaceName $workspace.Name

# Create a new insight
New-AzureRmOperationalInsightsStorageInsight -ResourceGroupName $workspace.ResourceGroupName -WorkspaceName $workspace.Name -Name "newinsight" -StorageAccountResourceId $storageId -StorageAccountKey $key -Tables @("WADWindowsEventLogsTable") -Containers @("wad-iis-logfiles")

# Update existing insight
Set-AzureRmOperationalInsightsStorageInsight -ResourceGroupName $workspace.ResourceGroupName -WorkspaceName $workspace.Name -Name "newinsight" -Tables @("WADWindowsEventLogsTable", "WADETWEventTable") -Containers @("wad-iis-logfiles")

# Remove hello insight
Remove-AzureRmOperationalInsightsStorageInsight -ResourceGroupName $workspace.ResourceGroupName -WorkspaceName $workspace.Name -Name "newinsight" 

```

<span data-ttu-id="b8d98-199">También puede utilizar Hola anterior registros toocollect de secuencia de comandos de las cuentas de almacenamiento en distintas suscripciones.</span><span class="sxs-lookup"><span data-stu-id="b8d98-199">You can also use hello preceding script toocollect logs from storage accounts in different subscriptions.</span></span> <span data-ttu-id="b8d98-200">script de Hola es capaz de toowork en suscripciones puesto que va a proporcionar el identificador de recurso de cuenta de almacenamiento de Hola y su correspondiente clave de acceso.</span><span class="sxs-lookup"><span data-stu-id="b8d98-200">hello script is able toowork across subscriptions since you are providing hello storage account resource id and a corresponding access key.</span></span> <span data-ttu-id="b8d98-201">Cuando se cambia la clave de acceso de hello, debe tooupdate Hola almacenamiento insight toohave Hola nueva clave.</span><span class="sxs-lookup"><span data-stu-id="b8d98-201">When you change hello access key, you need tooupdate hello storage insight toohave hello new key.</span></span>


## <a name="next-steps"></a><span data-ttu-id="b8d98-202">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b8d98-202">Next steps</span></span>
* <span data-ttu-id="b8d98-203">[Revise los cmdlets de PowerShell de Log Analytics](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) para obtener información adicional sobre cómo usar PowerShell para la configuración de Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="b8d98-203">[Review Log Analytics PowerShell cmdlets](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) for additional information on using PowerShell for configuration of Log Analytics.</span></span>

