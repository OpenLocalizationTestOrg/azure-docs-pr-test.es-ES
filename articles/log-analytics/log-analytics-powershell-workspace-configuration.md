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
# <a name="manage-log-analytics-using-powershell"></a>Administración de Log Analytics mediante PowerShell
Puede usar hello [cmdlets de PowerShell de análisis de registro](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) tooperform varias funciones de análisis de registros desde una línea de comandos o como parte de una secuencia de comandos.  Ejemplos de tareas de Hola que puede realizar con PowerShell:

* Crear un área de trabajo
* Agregar o quitar una solución
* Importar y exportar búsquedas guardadas
* Crear un grupo de equipos
* Habilitar la recopilación de registros de IIS desde equipos que tengan instalado el agente de Windows hello
* Recopilar contadores de rendimiento en equipos Linux y Windows
* Recopilar eventos de Syslog en equipos Linux 
* Recopilar eventos de registros de eventos de Windows
* Recopilar registros de eventos personalizados
* Agregar tooan de agente de análisis de registro de hello máquina virtual de Azure
* Configurar datos de tooindex de análisis de registro recopilados con diagnósticos de Azure

Este artículo proporciona dos ejemplos de código que muestran algunas de las funciones de Hola que puede realizar desde PowerShell.  Puede hacer referencia a toohello [referencia de cmdlets de PowerShell de análisis de registro](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) para otras funciones.

> [!NOTE]
> Análisis de registros se llamaba anteriormente visión operativa, motivo por el cual es nombre de hello usado en los cmdlets de Hola.
> 
> 

## <a name="prerequisites"></a>Requisitos previos
Estos ejemplos de trabajo con la versión 2.3.0 o posterior del módulo de AzureRm.OperationalInsights Hola.


## <a name="create-and-configure-a-log-analytics-workspace"></a>Creación y configuración de un área de trabajo de Log Analytics
Hello ejemplo de secuencia de comandos siguiente se muestra cómo:

1. Crear un área de trabajo
2. Soluciones de lista Hola disponibles
3. Agregar área de trabajo de soluciones toohello
4. Importar búsquedas guardadas
5. Exportar búsquedas guardadas
6. Crear un grupo de equipos
7. Habilitar la recopilación de registros de IIS desde equipos que tengan instalado el agente de Windows hello
8. Recopilar contadores de rendimiento de discos lógicos de equipos Linux (% de inodos usados; megabytes libres; % de espacio usado; transferencias de disco/seg.; lecturas de disco/seg.; escrituras de disco/seg.)
9. Recopilar eventos de Syslog de equipos Linux
10. Recopilar eventos de Error y advertencia de hello registro de eventos de aplicación de los equipos de Windows
11. Recopilar contadores de rendimiento de MB disponibles de equipos Windows
12. Recopilar registros personalizados 

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

## <a name="configuring-log-analytics-tooindex-azure-diagnostics"></a>Configuración de análisis de registros tooindex diagnósticos de Azure
Para la supervisión de recursos de Azure, recursos de hello deben toohave área de trabajo de diagnóstico de Azure habilitado y configurado toowrite tooa análisis de registros. Este método envía datos directamente tooLog análisis y no requiere toobe de datos escrito tooa cuenta de almacenamiento. Los recursos admitidos son los siguientes:

| Tipo de recurso | Registros | Métricas |
| --- | --- | --- |
| Puertas de enlace de aplicaciones    | Sí | Sí |
| Cuentas de automatización     | Sí | |
| Cuentas de Batch          | Sí | Sí |
| Data Lake Analytics     | yes | | 
| Data Lake Store         | Sí | |
| Elastic SQL Pool        |     | Sí |
| Espacio de nombres del Centro de eventos     |     | Sí |
| IoT Hubs                |     | Sí |
| Key Vault               | Sí | |
| Equilibradores de carga          | Sí | |
| Logic Apps              | yes | Sí |
| Grupos de seguridad de red | Sí | |
| Caché en Redis             |     | yes |
| Servicios de búsqueda         | Sí | Sí |
| Espacio de nombres de Bus de servicio   |     | Sí |
| SQL (v12)               |     | Sí |
| Sitios web               |     | yes |
| Granjas de servidores web        |     | Sí |

Para obtener detalles de Hola de métricas disponibles hello, consulte demasiado[métricas con el Monitor de Azure admitidas](../monitoring-and-diagnostics/monitoring-supported-metrics.md).

Para obtener detalles de Hola de registros disponibles de hello, consulte demasiado[admite servicios y el esquema para los registros de diagnóstico](../monitoring-and-diagnostics/monitoring-diagnostic-logs-schema.md).

```
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$resourceId = "/SUBSCRIPTIONS/ec11ca60-1234-491e-5678-0ea07feae25c/RESOURCEGROUPS/DEMO/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/DEMO" 

Set-AzureRmDiagnosticSetting -ResourceId $resourceId -WorkspaceId $workspaceId -Enabled $true
```

También puede utilizar Hola anterior cmdlet toocollect registros de recursos que se encuentran en distintas suscripciones. cmdlet de Hello es toowork capaz de a través de suscripciones desde que se envían los registros de Hola de área de trabajo de Hola y va a proporcionar el Id. de Hola de ambos recursos Hola crear registros.


## <a name="configuring-log-analytics-tooindex-azure-diagnostics-from-storage"></a>Configuración de diagnósticos de Azure desde el almacenamiento del análisis de registros tooindex
datos del registro toocollect desde dentro de una instancia en ejecución de un servicio de nube clásico o un clúster de service fabric, necesita almacenamiento de tooAzure de toofirst escritura Hola datos. Análisis de registros es, a continuación, configurar registros de hello toocollect de cuenta de almacenamiento de Hola. Los recursos admitidos son los siguientes:

* Servicios en la nube clásicos (roles web y de trabajo)
* Clústeres de Service Fabric

Hola siguiente ejemplo se muestra cómo para:

1. Lista de cuentas de almacenamiento existentes de Hola y ubicaciones de análisis de registros se indizarán los datos de
2. Crear un tooread de configuración de una cuenta de almacenamiento
3. Hola actualización que acaba de crear datos de configuración tooindex desde ubicaciones adicionales
4. Eliminar la configuración de hello recién creado

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

También puede utilizar Hola anterior registros toocollect de secuencia de comandos de las cuentas de almacenamiento en distintas suscripciones. script de Hola es capaz de toowork en suscripciones puesto que va a proporcionar el identificador de recurso de cuenta de almacenamiento de Hola y su correspondiente clave de acceso. Cuando se cambia la clave de acceso de hello, debe tooupdate Hola almacenamiento insight toohave Hola nueva clave.


## <a name="next-steps"></a>Pasos siguientes
* [Revise los cmdlets de PowerShell de Log Analytics](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) para obtener información adicional sobre cómo usar PowerShell para la configuración de Log Analytics.

