---
title: "aaaAssess las aplicaciones de Service Fabric con análisis de registros de Azure mediante PowerShell | Documentos de Microsoft"
description: "Puede usar soluciones de Service Fabric hello en análisis de registros con el riesgo de hello tooassess de PowerShell y el estado de las aplicaciones de Service Fabric, micro-services, nodos y clústeres."
services: log-analytics
documentationcenter: 
author: niniikhena
manager: jochan
editor: 
ms.assetid: 2047b3fa-96b1-4230-af5d-a4c331d973ce
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2017
ms.author: nini
ms.openlocfilehash: 3f6d6c0df02d6d453b77e50b75b64bf7eb73bbbf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="assess-azure-service-fabric-applications-and-micro-services-with-powershell"></a><span data-ttu-id="b66ec-103">Evaluación de aplicaciones y microservicios de Azure Service Fabric con PowerShell</span><span class="sxs-lookup"><span data-stu-id="b66ec-103">Assess Azure Service Fabric applications and micro-services with PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b66ec-104">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b66ec-104">Resource Manager</span></span>](log-analytics-service-fabric-azure-resource-manager.md)
> * [<span data-ttu-id="b66ec-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b66ec-105">PowerShell</span></span>](log-analytics-service-fabric.md)
>
>


![Símbolo de Service Fabric](./media/log-analytics-service-fabric/service-fabric-assessment-symbol.png)

<span data-ttu-id="b66ec-107">Este artículo describe cómo toouse Hola solución de Service Fabric en análisis de registros toohelp identificar y solucionar problemas en el clúster de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="b66ec-107">This article describes how toouse hello Service Fabric solution in Log Analytics toohelp identify and troubleshoot issues across your Service Fabric cluster.</span></span> <span data-ttu-id="b66ec-108">Le ayuda a ver cómo funcionan los nodos de Service Fabric y cómo se ejecutan sus aplicaciones y microservicios.</span><span class="sxs-lookup"><span data-stu-id="b66ec-108">It helps you see how your Service Fabric nodes are performing and how your applications and micro-services are running.</span></span>

<span data-ttu-id="b66ec-109">Hola soluciones de Service Fabric utiliza datos de diagnósticos de Azure de las máquinas virtuales tejido de servicio, mediante la recopilación de estos datos de las tablas de WAD de Azure.</span><span class="sxs-lookup"><span data-stu-id="b66ec-109">hello Service Fabric solution uses Azure Diagnostics data from your Service Fabric VMs, by collecting this data from your Azure WAD tables.</span></span> <span data-ttu-id="b66ec-110">Análisis de registros, a continuación, leen Hola después de eventos de Service Fabric framework:</span><span class="sxs-lookup"><span data-stu-id="b66ec-110">Log Analytics then reads hello following Service Fabric framework events:</span></span>

- <span data-ttu-id="b66ec-111">**Eventos de Reliable Services**</span><span class="sxs-lookup"><span data-stu-id="b66ec-111">**Reliable Service Events**</span></span>
- <span data-ttu-id="b66ec-112">**Eventos de actor**</span><span class="sxs-lookup"><span data-stu-id="b66ec-112">**Actor Events**</span></span>
- <span data-ttu-id="b66ec-113">**Eventos operativos**</span><span class="sxs-lookup"><span data-stu-id="b66ec-113">**Operational Events**</span></span>
- <span data-ttu-id="b66ec-114">**Eventos de ETW personalizados**</span><span class="sxs-lookup"><span data-stu-id="b66ec-114">**Custom ETW events**</span></span>

<span data-ttu-id="b66ec-115">panel de soluciones de tejido de servicio de Hello muestra problemas importantes y los eventos relevantes en su entorno de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="b66ec-115">hello Service Fabric solution dashboard shows you notable issues and relevant events in your Service Fabric environment.</span></span>

## <a name="installing-and-configuring-hello-solution"></a><span data-ttu-id="b66ec-116">Instalar y configurar soluciones de Hola</span><span class="sxs-lookup"><span data-stu-id="b66ec-116">Installing and configuring hello solution</span></span>
<span data-ttu-id="b66ec-117">Siga estos tres pasos sencillos tooinstall y configurar soluciones de hello:</span><span class="sxs-lookup"><span data-stu-id="b66ec-117">Follow these three easy steps tooinstall and configure hello solution:</span></span>

1. <span data-ttu-id="b66ec-118">Asociar Hola suscripción de Azure usada toocreate todos los recursos de clúster, incluidas las cuentas de almacenamiento, con el área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="b66ec-118">Associate hello Azure subscription that you used toocreate all cluster resources, including storage accounts, with your workspace.</span></span> <span data-ttu-id="b66ec-119">Consulte [Introducción a Log Analytics](log-analytics-get-started.md) para obtener información sobre cómo crear un área de trabajo de Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="b66ec-119">See [Get started with Log Analytics](log-analytics-get-started.md) for information about creating a Log Analytics workspace.</span></span>
2. <span data-ttu-id="b66ec-120">Configurar análisis de registros toocollect y ver los registros de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="b66ec-120">Configure Log Analytics toocollect and view Service Fabric logs.</span></span>
3. <span data-ttu-id="b66ec-121">Habilitar la solución de Service Fabric de hello en el área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="b66ec-121">Enable hello Service Fabric solution in your workspace.</span></span>

## <a name="configure-log-analytics-toocollect-and-view-service-fabric-logs"></a><span data-ttu-id="b66ec-122">Configurar análisis de registros toocollect y ver los registros de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="b66ec-122">Configure Log Analytics toocollect and view Service Fabric logs</span></span>
<span data-ttu-id="b66ec-123">En esta sección, aprenderá cómo registra tooretrieve de análisis de registros de tooconfigure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="b66ec-123">In this section, you learn how tooconfigure Log Analytics tooretrieve Service Fabric logs.</span></span> <span data-ttu-id="b66ec-124">Hola registros permiten tooview, analizar y solución problemas en el clúster o en aplicaciones de Hola y servicios que se ejecutan en dicho clúster, mediante el portal de OMS Hola.</span><span class="sxs-lookup"><span data-stu-id="b66ec-124">hello logs allow you tooview, analyze, and troubleshoot issues in your cluster or in hello applications and services running in that cluster, using hello OMS portal.</span></span>

> [!NOTE]
> <span data-ttu-id="b66ec-125">Configurar registros hello tooupload de extensión de diagnósticos de Azure de Hola para las tablas de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="b66ec-125">Configure hello Azure Diagnostics extension tooupload hello logs for storage tables.</span></span> <span data-ttu-id="b66ec-126">tablas de Hello deben coincidir con lo que busca análisis de registros.</span><span class="sxs-lookup"><span data-stu-id="b66ec-126">hello tables must match what Log Analytics looks for.</span></span> <span data-ttu-id="b66ec-127">Para obtener más información, consulte [modo toocollect registra con diagnósticos de Azure](../service-fabric/service-fabric-diagnostics-how-to-setup-wad.md).</span><span class="sxs-lookup"><span data-stu-id="b66ec-127">For more information, see [How toocollect logs with Azure Diagnostics](../service-fabric/service-fabric-diagnostics-how-to-setup-wad.md).</span></span> <span data-ttu-id="b66ec-128">ejemplos de valores de configuración de Hello en este artículo muestran qué nombres Hola de almacenamiento de hello tablas deberían ser.</span><span class="sxs-lookup"><span data-stu-id="b66ec-128">hello configuration settings examples in this article show you what hello names of hello storage tables should be.</span></span> <span data-ttu-id="b66ec-129">Una vez que se ha configurado en el clúster de Hola y está cargando cuenta de almacenamiento de registros tooa diagnóstico, Hola siguiente paso es toocollect de análisis de registros tooconfigure estos registros.</span><span class="sxs-lookup"><span data-stu-id="b66ec-129">Once Diagnostics is set up on hello cluster and is uploading logs tooa storage account, hello next step is tooconfigure Log Analytics toocollect these logs.</span></span>
>
>

<span data-ttu-id="b66ec-130">Asegúrese de que se actualice hello **EtwEventSourceProviderConfiguration** sección Hola **template.json** archivo tooadd entradas para hello actualizar EventSources nueva antes de aplicar la configuración de Hola ejecuta **deploy.ps1**.</span><span class="sxs-lookup"><span data-stu-id="b66ec-130">Ensure that you update hello **EtwEventSourceProviderConfiguration** section in hello **template.json** file tooadd entries for hello new EventSources before you apply hello configuration update by running **deploy.ps1**.</span></span> <span data-ttu-id="b66ec-131">tabla de Hello para la carga es Hola igual como (ETWEventTable).</span><span class="sxs-lookup"><span data-stu-id="b66ec-131">hello table for upload is hello same as (ETWEventTable).</span></span> <span data-ttu-id="b66ec-132">En el momento de hello, análisis de registros solo puede leer los eventos ETW de aplicación de hello *WADETWEventTable* tabla.</span><span class="sxs-lookup"><span data-stu-id="b66ec-132">At hello moment, Log Analytics can only read application ETW events from hello *WADETWEventTable* table.</span></span>

<span data-ttu-id="b66ec-133">Hello siguientes herramientas están tooperform usado alguna de las operaciones de hello en esta sección:</span><span class="sxs-lookup"><span data-stu-id="b66ec-133">hello following tools are used tooperform some of hello operations in this section:</span></span>

* <span data-ttu-id="b66ec-134">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="b66ec-134">Azure PowerShell</span></span>
* [<span data-ttu-id="b66ec-135">Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="b66ec-135">Operations Management Suite</span></span>](http://www.microsoft.com/oms)

### <a name="configure-a-log-analytics-workspace-tooshow-hello-cluster-logs"></a><span data-ttu-id="b66ec-136">Configurar un análisis de registros área de trabajo tooshow Hola clúster inicia una sesión</span><span class="sxs-lookup"><span data-stu-id="b66ec-136">Configure a Log Analytics workspace tooshow hello cluster logs</span></span>

<span data-ttu-id="b66ec-137">Después de crear un área de trabajo de análisis de registros, configurar registros de toopull de área de trabajo de Hola de tablas de almacenamiento de Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="b66ec-137">After you create a Log Analytics workspace, configure hello workspace toopull logs from hello Azure storage tables.</span></span> <span data-ttu-id="b66ec-138">A continuación, ejecute el siguiente script de PowerShell de hello:</span><span class="sxs-lookup"><span data-stu-id="b66ec-138">Then, run hello following PowerShell script:</span></span>

```
<#
    This script will configure an Operations Management Suite workspace (previously called an Operational Insights workspace) tooread Diagnostics from an Azure Storage account.
    It will enable all supported data types (currently Service Fabric Events, ETW Events and IIS Logs).
    It supports Resource Manager storage accounts.
    If you have more than one Azure Subscription, you will be prompted for hello subscription tooconfigure.
    If you have more than one Log Analytics workspace you will be prompted for hello workspace tooconfigure.
    It will then look through your Service Fabric clusters, and configure your Log Analytics workspace tooread Diagnostics from storage accounts that are connected toothat cluster and have diagnostics enabled.
#>

try
{
    Get-AzureRMContext
}
catch [System.Management.Automation.PSInvalidOperationException]
{
    Add-AzureRmAccount
}

$validTables = "WADServiceFabric*EventTable", "WADETWEventTable"
function Select-Subscription {
      $subscription = ""
      $allSubscriptions = Get-AzureRmSubscription
      switch ($allSubscriptions.Count) {
             0 {Write-Error "No Operations Management Suite workspaces found"}
             1 {return $allSubscriptions}
        default {
            $uiPrompt = "Enter hello number corresponding toohello Azure subscription you would like toowork with.`n"

            $count = 1
            foreach ($subscription in $allSubscriptions) {
                $uiPrompt += "$count. " + $subscription.Name + " (" + $subscription.Id + ")`n"
                $count++
            }
            $answer = (Read-Host -Prompt $uiPrompt) - 1
            $subscription = $allSubscriptions[$answer]
             Write-Host $subscription.Id
        }  
    }
    return $subscription
}

function Select-Workspace {
    $workspace = ""
    $allWorkspaces = Get-AzureRmOperationalInsightsWorkspace  

    switch ($allWorkspaces.Count) {
        0 {Write-Error "No Operations Management Suite workspaces found. `n"}
        1 {return $allWorkspaces}
        default {
            $uiPrompt = "Enter hello number corresponding toohello workspace you want tooconfigure.`n"
            $count = 1
            foreach ($workspace in $allWorkspaces) {
                $uiPrompt += "$count. " + $workspace.Name + " (" + $workspace.CustomerId + ")`n"
                $count++
            }
            $answer = (Read-Host -Prompt $uiPrompt) - 1
            $workspace = $allWorkspaces[$answer]
             Write-Host $workspace.WorkspaceName
        }  
    }
    return $workspace
}

function Check-ETWProviderLogging {
     param(
     [string]$id,
     [string]$provider,
     [string]$expectedTable,
     [string]$table
    )       
         Write-Debug ("ID: $id Provider: $provider ExpectedTable $expectedTable ActualTable $table")
         if ( ($table -eq $null) -or ($table -eq ""))  
         {
             Write-Warning ("$id No configuration found for $provider. Configure Azure diagnostics toowrite too$expectedTable.")
         }  
         elseif ( $table -ne $expectedTable )
         {
             Write-Warning ("$id $provider events are being written too$table instead of WAD$expectedTable. Events will not be collected by Log Analytics")
         }  
         else
         {
             Write-Verbose "$id $provider events are being written tooWAD$expectedTable (Correct configuration.)"
         }
 }

function Check-ServiceFabricScaleSetDiagnostics {
     param(
          [psobject]$scaleSetDiagnostics
   )
     $storageAccountsFound = @()
     Write-Verbose ("Checking " + $scaleSetDiagnostics)
     $sfReliableActorTable = $null
     $sfReliableServiceTable = $null
     $sfOperationalTable = $null

     Write-Debug $scaleSetDiagnostics
     $serviceFabricProviderList = ""
     $etwManifestProviderList = ""

     if ( $scaleSetDiagnostics.xmlCfg )  
      {
             Write-Debug ("Found XMLcfg")
             $xmlCfg = [System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($scaleSetDiagnostics.xmlCfg))
             Write-Debug $xmlCfg
             $etwProviders = Select-Xml -Content $xmlCfg -XPath "//EtwProviders"                 
             $serviceFabricProviderList = $etwProviders.Node.EtwEventSourceProviderConfiguration
             $etwManifestProviderList = $etwProviders.Node.EtwManifestProviderConfiguration
      } elseif ($scaleSetDiagnostics.WadCfg )  
     {
         Write-Debug ("Found WADcfg")
         Write-Debug $scaleSetDiagnostics.WadCfg
         $serviceFabricProviderList = $scaleSetDiagnostics.WadCfg.DiagnosticMonitorConfiguration.EtwProviders.EtwEventSourceProviderConfiguration
         $etwManifestProviderList = $scaleSetDiagnostics.WadCfg.DiagnosticMonitorConfiguration.EtwProviders.EtwManifestProviderConfiguration
     } else
     {
         Write-Error "Unable tooparse Azure Diagnostics setting for $id"
             Write-Warning ("$id does not have diagnostics enabled")
     }
     foreach ($provider in $serviceFabricProviderList)  
     {
         Write-Debug ("Event Source Provider: " + $provider.Provider + " Destination: " + $provider.DefaultEvents.eventDestination)
         if ($provider.Provider -eq "Microsoft-ServiceFabric-Actors")
         {
             $sfReliableActorTable = $provider.DefaultEvents.eventDestination  
         } elseif ($provider.Provider -eq "Microsoft-ServiceFabric-Services")  
         {  
             $sfReliableServiceTable = $provider.DefaultEvents.eventDestination  
         } else  
         {
             Check-ETWProviderLogging $id $provider.Provider "ETWEventTable" $provider.DefaultEvents.eventDestination
         }
     }
     foreach ($provider in $etwManifestProviderList)
     {
         Write-Debug ("Manifest Provider: " + $provider.Provider + " Destination: " + $provider.DefaultEvents.eventDestination)
         if ($provider.Provider -eq "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8")
         {
             $sfOperationalTable = $provider.DefaultEvents.eventDestination  
         } else  
         {
             Check-ETWProviderLogging $id $provider.Provider "ETWEventTable" $provider.DefaultEvents.eventDestination
         }
     }

     Check-ETWProviderLogging $id "Microsoft-ServiceFabric-Actors" "ServiceFabricReliableActorEventTable" $sfReliableActorTable
     Check-ETWProviderLogging $id "Microsoft-ServiceFabric-Services" "ServiceFabricReliableServiceEventTable" $sfReliableServiceTable
     Check-ETWProviderLogging $id "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8 (System events)" "ServiceFabricSystemEventTable" $sfOperationalTable

     Write-Verbose ("StorageAccount: " + $scaleSetDiagnostics.StorageAccount)
     $storageAccountsFound += ($scaleSetDiagnostics.StorageAccount)
     return ($storageAccountsFound)
 }

function Select-StorageAccount {
    $allResources = Get-AzureRmResource #pulls in all resources
    $serviceFabricClusters = $allResources.Where({$_.ResourceType -eq "Microsoft.ServiceFabric/clusters"}) #pulls in all service fabric clusters in hello resource
    $storageAccountList = @()
    foreach($cluster in $serviceFabricClusters) {
        Write-Host("Checking cluster: " + $cluster.Name)
         $scaleSet = $allResources.Where({($_.ResourceType -eq "Microsoft.Compute/virtualMachineScaleSets") -and ($_.ResourceGroupName -eq $cluster.ResourceGroupName)})

         foreach($set in $scaleSet) {
             $resource = Get-AzureRmResource -ResourceId $set.ResourceId
             $extensions = $resource.Properties.VirtualMachineProfile.ExtensionProfile.Extensions

             foreach($ext in $extensions) {
                 if ($ext.Properties.Publisher -eq "Microsoft.Azure.Diagnostics" -and $ext.Properties.Type -eq "IaaSDiagnostics") {
                     $storageAccountList += (Check-ServiceFabricScaleSetDiagnostics $ext.Properties.Settings)
                 }
             }
          }

         $storageAccountsToCheck = $allResources.Where({($_.ResourceType -eq "Microsoft.Storage/storageAccounts") -and ($_.ResourceName -in $storageAccountList)})

         if ($storageAccountsToCheck.Count -eq "0") {
                Write-Error "No storage accounts found"
           }
           else {
                    foreach ($storageAccount in $storageAccountsToCheck) {
                        Write-Host("Checking Storage Account: " + $storageAccount.Name)
                        $insightsName = $storageAccount.Name + $workspace.Name
                        $existingConfig = ""
                        try
                            {
                                $existingConfig = Get-AzureRmOperationalInsightsStorageInsight -Workspace $workspace -Name $insightsName -ErrorAction Stop
                            }
                        catch
                            {
                                # HTTP Not Found is returned if hello storage insight doesn't exist
                            }
                        if ($existingConfig) {                         
                                  [array]$Tables = $existingConfig.Tables
                                   foreach($table in $validTables) {
                                         if($Tables -notcontains $table) {
                                               $Tables += $table
                                               $dirty = $true;
                                               Write-Host "Adding Table: $table";
                                         }
                                         else {
                                               Write-Host "$table is already configured.`n";
                                             }
                                      }
                                      # If any of hello tables from hello table list are not already monitored, then we add them
                                   if($dirty -eq $true) {
                                           Set-AzureRmOperationalInsightsStorageInsight -Workspace $workspace -Name $insightsName -Tables $Tables
                                           Write-Host "Updating Storage Insight. `n"
                                    }
                                    else {
                                           Write-Host "Storage Insight already updated."
                                  }
                          }
                     else {
                            $key = (Get-AzureRmStorageAccountKey -ResourceGroupName $storageAccount.ResourceGroupName -Name $storageAccount.Name)[0].Value
                           New-AzureRmOperationalInsightsStorageInsight -Workspace $workspace -Name $insightsName -StorageAccountResourceId $storageAccount.ResourceId -StorageAccountKey $key -Tables $validTables
                            Write-Host "New Azure Storage Insight Configured. `n"
                           }
                    }
             }
      }
      return
     }

$subscription = Select-Subscription
$subscriptionId = $subscription.SubscriptionId
$subscription = Select-AzureRmSubscription -SubscriptionId $subscriptionId
$workspace = Select-Workspace
$storageAccount = Select-StorageAccount
```

<span data-ttu-id="b66ec-139">Después de haber configurado hello tooread de área de trabajo de análisis de registros de hello Azure tablas en la cuenta de almacenamiento, inicie sesión en toohello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="b66ec-139">After you've configured hello Log Analytics workspace tooread from hello Azure tables in your storage account, log in toohello Azure portal.</span></span> <span data-ttu-id="b66ec-140">Seleccione el área de trabajo de análisis de registros de Hola desde **todos los recursos**.</span><span class="sxs-lookup"><span data-stu-id="b66ec-140">Select hello Log Analytics workspace from **All Resources**.</span></span> <span data-ttu-id="b66ec-141">se muestra el número de Hola de área de trabajo toohello conectados los registros de cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="b66ec-141">hello number of storage account logs connected toohello workspace is displayed.</span></span> <span data-ttu-id="b66ec-142">Seleccione hello **registros de la cuenta de almacenamiento** icono.</span><span class="sxs-lookup"><span data-stu-id="b66ec-142">Select hello **Storage account logs** tile.</span></span> <span data-ttu-id="b66ec-143">Revisar la lista de Hola de cuenta de almacenamiento registra tooverify que la cuenta de almacenamiento está conectado toohello área de trabajo correcta.</span><span class="sxs-lookup"><span data-stu-id="b66ec-143">Review hello list of storage account logs tooverify that your storage account is connected toohello correct workspace.</span></span>

![Registros de la cuenta de almacenamiento](./media/log-analytics-service-fabric/sf1.png)

## <a name="enable-hello-service-fabric-solution"></a><span data-ttu-id="b66ec-145">Habilitar la solución de Service Fabric Hola</span><span class="sxs-lookup"><span data-stu-id="b66ec-145">Enable hello Service Fabric solution</span></span>
<span data-ttu-id="b66ec-146">Usar hello siguiendo el área de trabajo de script tooadd Hola solución tooyour análisis de registros.</span><span class="sxs-lookup"><span data-stu-id="b66ec-146">Use hello following script tooadd hello solution tooyour Log Analytics workspace.</span></span> <span data-ttu-id="b66ec-147">Ejecutar script de Hola en PowerShell, mediante Hola suscripción de Azure que está asociado con el área de trabajo de análisis de registros de Hola que quiera soluciones de Service Fabric hello tooenable.</span><span class="sxs-lookup"><span data-stu-id="b66ec-147">Run hello script in PowerShell, using hello Azure subscription that is associated with hello Log Analytics workspace that you want tooenable hello Service Fabric solution in.</span></span>

```
function Select-Subscription {
      $subscription = ""
      $allSubscriptions = Get-AzureRmSubscription
      switch ($allSubscriptions.Count) {
             0 {Write-Error "No Operations Management Suite workspaces found"}
             1 {return $allSubscriptions}
        default {
            $uiPrompt = "Enter hello number corresponding toohello Azure subscription you would like toowork with.`n"
            $count = 1
            foreach ($subscription in $allSubscriptions) {
                $uiPrompt += "$count. " + $subscription.SubscriptionName + " (" + $subscription.SubscriptionId + ")`n"
                $count++
            }
            $answer = (Read-Host -Prompt $uiPrompt) - 1
            $subscription = $allSubscriptions[$answer]
             Write-Host $subscription.SubscriptionId
        }  
    }
    return $subscription
}

function Select-Workspace {
    $workspace = ""
    $allWorkspaces = Get-AzureRmOperationalInsightsWorkspace  
    switch ($allWorkspaces.Count) {
        0 {Write-Error "No Operations Management Suite workspaces found"}
        1 {return $allWorkspaces}
        default {
            $uiPrompt = "Enter hello number corresponding toohello workspace you want tooconfigure.`n"
            $count = 1
            foreach ($workspace in $allWorkspaces) {
                $uiPrompt += "$count. " + $workspace.Name + " (" + $workspace.CustomerId + ")`n"
                $count++
            }
            $answer = (Read-Host -Prompt $uiPrompt) - 1
            $workspace = $allWorkspaces[$answer]
                           Write-Host $workspace.WorkspaceName
        }  
    }
    return $workspace
}
$subscription = Select-Subscription
$subscriptionId = $subscription.Id
$subscription = Select-AzureRmSubscription -SubscriptionId $subscriptionId
$workspace = Select-Workspace
Set-AzureRmOperationalInsightsIntelligencePack -ResourceGroupName $workspace.ResourceGroupName -WorkspaceName $workspace.Name -IntelligencePackName "ServiceFabric" -Enabled $true
```

<span data-ttu-id="b66ec-148">Después de habilitar la solución de hello, es agregar el icono de Service Fabric de hello tooyour análisis de registros *Introducción* página.</span><span class="sxs-lookup"><span data-stu-id="b66ec-148">After you enable hello solution, hello Service Fabric tile is added tooyour Log Analytics *Overview* page.</span></span> <span data-ttu-id="b66ec-149">página de Hello muestra una vista de problemas importantes, como errores de Coredispatcher y cancelaciones ocurridos en hello últimas 24 horas.</span><span class="sxs-lookup"><span data-stu-id="b66ec-149">hello page shows a view of notable issues such as runAsync failures and cancellations that occurred in hello last 24 hours.</span></span>

![Icono de Service Fabric](./media/log-analytics-service-fabric/sf2.png)

### <a name="view-service-fabric-events"></a><span data-ttu-id="b66ec-151">Visualización de eventos de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="b66ec-151">View Service Fabric events</span></span>
<span data-ttu-id="b66ec-152">Haga clic en hello **Service Fabric** icono tooopen Hola o panel de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="b66ec-152">Click hello **Service Fabric** tile tooopen hello Service Fabric dashboard.</span></span> <span data-ttu-id="b66ec-153">panel de Hello incluye columnas de hello en tabla Hola siguiente.</span><span class="sxs-lookup"><span data-stu-id="b66ec-153">hello dashboard includes hello columns in hello table that follows.</span></span> <span data-ttu-id="b66ec-154">Cada columna muestra top 10 eventos de hello mediante la correspondencia de recuento que han especificado criterios de la columna para hello intervalo de tiempo.</span><span class="sxs-lookup"><span data-stu-id="b66ec-154">Each column lists hello top 10 events by count matching that column's criteria for hello specified time range.</span></span> <span data-ttu-id="b66ec-155">Puede ejecutar una búsqueda de registros que proporciona la lista completa de hello haciendo clic en **ver todas** en hello derecha, abajo de cada columna, o haciendo clic en el encabezado de columna de Hola.</span><span class="sxs-lookup"><span data-stu-id="b66ec-155">You can run a log search that provides hello entire list by clicking **See all** at hello right bottom of each column, or by clicking hello column header.</span></span>

| <span data-ttu-id="b66ec-156">**Evento de Service Fabric**</span><span class="sxs-lookup"><span data-stu-id="b66ec-156">**Service Fabric event**</span></span> | <span data-ttu-id="b66ec-157">**descripción**</span><span class="sxs-lookup"><span data-stu-id="b66ec-157">**description**</span></span> |
| --- | --- |
| <span data-ttu-id="b66ec-158">Problemas importantes</span><span class="sxs-lookup"><span data-stu-id="b66ec-158">Notable Issues</span></span> | <span data-ttu-id="b66ec-159">Se muestran problemas, como RunAsyncFailures, RunAsynCancellations y nodos inactivos.</span><span class="sxs-lookup"><span data-stu-id="b66ec-159">Displays issues including RunAsyncFailures, RunAsynCancellations, and Node Downs.</span></span> |
| <span data-ttu-id="b66ec-160">Eventos operativos</span><span class="sxs-lookup"><span data-stu-id="b66ec-160">Operational Events</span></span> | <span data-ttu-id="b66ec-161">Se muestran eventos operativos destacados, como implementaciones y actualizaciones de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="b66ec-161">Displays notable operational events including application upgrade and deployments.</span></span> |
| <span data-ttu-id="b66ec-162">Eventos de servicios de confianza</span><span class="sxs-lookup"><span data-stu-id="b66ec-162">Reliable Service Events</span></span> | <span data-ttu-id="b66ec-163">Se muestran eventos destacados de Reliable Services, como Runasyncinvocations.</span><span class="sxs-lookup"><span data-stu-id="b66ec-163">Displays notable reliable service events including  Runasyncinvocations.</span></span> |
| <span data-ttu-id="b66ec-164">Eventos de actor</span><span class="sxs-lookup"><span data-stu-id="b66ec-164">Actor Events</span></span> | <span data-ttu-id="b66ec-165">Se muestran eventos destacados de actor generados por los microservicios.</span><span class="sxs-lookup"><span data-stu-id="b66ec-165">Displays notable actor events generated by your micro-services.</span></span> <span data-ttu-id="b66ec-166">Los eventos incluyen las excepciones producidas por un método de actor, las activaciones y desactivaciones de actor, etc.</span><span class="sxs-lookup"><span data-stu-id="b66ec-166">Events include exceptions thrown by an actor method, actor activations and deactivations, and so on.</span></span> |
| <span data-ttu-id="b66ec-167">Eventos de aplicación</span><span class="sxs-lookup"><span data-stu-id="b66ec-167">Application Events</span></span> | <span data-ttu-id="b66ec-168">Todos los eventos ETW personalizados generados por las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="b66ec-168">Displays all custom ETW events generated by your applications.</span></span> |

![Panel de Service Fabric](./media/log-analytics-service-fabric/sf3.png)

![Panel de Service Fabric](./media/log-analytics-service-fabric/sf4.png)

<span data-ttu-id="b66ec-171">Hello tabla siguiente muestran los métodos de recopilación de datos y otros detalles acerca de cómo se recopilan los datos de Service Fabric:</span><span class="sxs-lookup"><span data-stu-id="b66ec-171">hello following table shows data collection methods and other details about how data is collected for Service Fabric:</span></span>

| <span data-ttu-id="b66ec-172">plataforma</span><span class="sxs-lookup"><span data-stu-id="b66ec-172">platform</span></span> | <span data-ttu-id="b66ec-173">Agente directo</span><span class="sxs-lookup"><span data-stu-id="b66ec-173">Direct Agent</span></span> | <span data-ttu-id="b66ec-174">Agente de Operations Manager</span><span class="sxs-lookup"><span data-stu-id="b66ec-174">Operations Manager agent</span></span> | <span data-ttu-id="b66ec-175">Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="b66ec-175">Azure Storage</span></span> | <span data-ttu-id="b66ec-176">¿Se requiere Operations Manager?</span><span class="sxs-lookup"><span data-stu-id="b66ec-176">Operations Manager required?</span></span> | <span data-ttu-id="b66ec-177">Se envían los datos del agente de Operations Manager a través del grupo de administración</span><span class="sxs-lookup"><span data-stu-id="b66ec-177">Operations Manager agent data sent via management group</span></span> | <span data-ttu-id="b66ec-178">Frecuencia de recopilación</span><span class="sxs-lookup"><span data-stu-id="b66ec-178">collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="b66ec-179">Windows</span><span class="sxs-lookup"><span data-stu-id="b66ec-179">Windows</span></span> |  |  | <span data-ttu-id="b66ec-180">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b66ec-180">&#8226;</span></span> |  |  |<span data-ttu-id="b66ec-181">10 minutos</span><span class="sxs-lookup"><span data-stu-id="b66ec-181">10 minutes</span></span> |

> [!NOTE]
> <span data-ttu-id="b66ec-182">Cambiar el ámbito de Hola de eventos con **datos basándose en los últimos siete días** en parte superior de hello del panel de Hola.</span><span class="sxs-lookup"><span data-stu-id="b66ec-182">Change hello scope of events with **Data based on last seven days** at hello top of hello dashboard.</span></span> <span data-ttu-id="b66ec-183">También puede mostrar los eventos generados en hello últimos siete días, un día o seis horas.</span><span class="sxs-lookup"><span data-stu-id="b66ec-183">You can also show events generated within hello last seven days, one day, or six hours.</span></span> <span data-ttu-id="b66ec-184">O bien, puede seleccionar **personalizado** toospecify un intervalo de fechas personalizado.</span><span class="sxs-lookup"><span data-stu-id="b66ec-184">Or, you can select **Custom** toospecify a custom date range.</span></span>
>
>

## <a name="troubleshoot-your-service-fabric-and-log-analytics-configuration"></a><span data-ttu-id="b66ec-185">Solución de problemas de Service Fabric y configuración de Log Analytics</span><span class="sxs-lookup"><span data-stu-id="b66ec-185">Troubleshoot your Service Fabric and Log Analytics configuration</span></span>
<span data-ttu-id="b66ec-186">Si necesita tooverify la configuración de análisis de registros porque son datos de análisis de registros de eventos de tooview no se puede, utilice Hola siguiente secuencia de comandos.</span><span class="sxs-lookup"><span data-stu-id="b66ec-186">If you need tooverify your Log Analytics configuration because you are unable tooview event data in Log Analytics, use hello following script.</span></span> <span data-ttu-id="b66ec-187">Esta herramienta realiza Hola siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="b66ec-187">It performs hello following actions:</span></span>

1. <span data-ttu-id="b66ec-188">Lee la configuración de diagnóstico de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="b66ec-188">Reads your Service Fabric diagnostics configuration</span></span>
2. <span data-ttu-id="b66ec-189">Comprueba si los datos escritos en tablas de Hola</span><span class="sxs-lookup"><span data-stu-id="b66ec-189">Checks for data written into hello tables</span></span>
3. <span data-ttu-id="b66ec-190">Comprueba que el análisis de registros es tooread configurado de tablas de Hola</span><span class="sxs-lookup"><span data-stu-id="b66ec-190">Verifies that Log Analytics is configured tooread from hello tables</span></span>

```
<#
    Verify Service Fabric and Log Analytics configuration
    1. Read Service Fabric diagnostics configuration
    2. Check for data being written into hello tables
    3. Verify Log Analytics is configured tooread from hello tables

    Supported tables:
    WADServiceFabricReliableActorEventTable
    WADServiceFabricReliableServiceEventTable
    WADServiceFabricSystemEventTable
    WADETWEventTable

    Script will write a warning for every misconfiguration detected
    toosee items that are correctly configured set $VerbosePreference="Continue"
#>
Param
(
    [Parameter(Mandatory=$true,
    ValueFromPipeline=$true,
    Position=1)]
    [string]$workspaceName
)

$WADtables = @("WADServiceFabricReliableActorEventTable",
               "WADServiceFabricReliableServiceEventTable",
               "WADServiceFabricSystemEventTable",
               "WADETWEventTable"
               )

<#
    Check if OMS Log Analytics is configured tooindex service fabric events from hello specified table
#>

function Check-OMSLogAnalyticsConfiguration {
    param(
    [psobject]$workspace,
    [psobject]$storageAccount,
    [string]$id
    )

    $existingInsights = Get-AzureRmOperationalInsightsStorageInsight -ResourceGroupName $workspace.ResourceGroupName -WorkspaceName $workspace.Name

    if ($existingInsights)
    {
        $currentStorageAccountInsight = $existingInsights.Where({$_.StorageAccountResourceId -eq $storageAccount.ResourceId})

        if ("WADServiceFabric*EventTable" -in $currentStorageAccountInsight.Tables)
        {
            Write-Verbose ("OMS Log Analytics workspace " + $workspace.Name + " is configured tooindex service fabric actor, service and operational events from " + $storageAccount.Name)
        } else
        {
            Write-Warning ("OMS Log Analytics workspace " + $workspace.Name + " is not configured tooindex service fabric actor, service and operational events from " + $storageAccount.Name)
        }
        if ("WADETWEventTable" -in $currentStorageAccountInsight.Tables)
        {
            Write-Verbose ("OMS Log Analytics workspace " + $workspace.Name + " is configured tooindex service fabric application events from " + $storageAccount.Name)
        } else
        {
            Write-Warning ("OMS Log Analytics workspace " + $workspace.Name + " is not configured tooindex service fabric application events from " + $storageAccount.Name)
        }
    } else
    {
        Write-Warning ("OMS Log Analytics workspace " + $workspace.Name + "is not configured tooread service fabric events from " + $storageAccount.Name)
    }    
}

<#
    Check Azure table storage tooconfirm there is recent data written by Service Fabric
#>

function Check-TablesForData {
    param(
    [psobject]$storageAccount
    )

    $ctx = (Get-AzureRmStorageAccount -ResourceGroupName $storageAccount.ResourceGroupName -Name $storageAccount.ResourceName).Context

    $createdTables = Get-AzureStorageTable -Context $ctx

    $recently = Get-Date -Format s ((Get-Date).AddMinutes(-20).ToUniversalTime())
    $recently = $recently + "Z"

    foreach ($table in $WADtables)
    {
        if ($table -in $createdTables.Name)
        {
            $tbl = Get-AzureStorageTable -Name $table -Context $ctx
            $query = New-Object Microsoft.WindowsAzure.Storage.Table.TableQuery
            $list = New-Object System.Collections.Generic.List[string]
            $list.Add("RowKey")
            $list.Add("ProviderName")
            $list.Add("Timestamp")
            $query.FilterString = "Timestamp gt datetime'$recently'"
            $query.SelectColumns = $list
            $query.TakeCount = 20
            $entities = $tbl.CloudTable.ExecuteQuery($query)
            Write-Debug $entities
            if ($entities.Count -gt 0)
            {
                Write-Verbose ("Data was written too$table in " + $storageAccount.ResourceName + "after $recently")
            } else
            {
                Write-Warning ("No data after $recently is in  $table in " + $storageAccount.ResourceName)
            }
        } else
        {
            Write-Warning ("$table does not exist in storage account " + $storageAccount.ResourceName)
        }
    }
}

<#
    Check if ETW provider is configured toolog events toohello expected table storage
#>
function Check-ETWProviderLogging {
    param(
    [string]$id,
    [string]$provider,
    [string]$expectedTable,
    [string]$table
    )      
        Write-Debug ("ID: $id Provider: $provider ExpectedTable $expectedTable ActualTable $table")
        if ( ($table -eq $null) -or ($table -eq ""))
        {
            Write-Warning ("$id No configuration found for $provider. Configure Azure diagnostics toowrite too$expectedTable.")
        }
        elseif ( $table -ne $expectedTable )
        {
            Write-Warning ("$id $provider events are being written too$table instead of WAD$expectedTable. Events will not be collected by Log Analytics")
        }
        else
        {
            Write-Verbose "$id $provider events are being written tooWAD$expectedTable (Correct configuration.)"
        }
}

<#
    Check Azure Diagnostics Configuration for a Service Fabric cluster
#>
function Check-ServiceFabricScaleSetDiagnostics {
    param(
    [psobject]$scaleSetDiagnostics
    )

    $storageAccountsFound = @()
    Write-Verbose ("Checking " + $scaleSetDiagnostics)
    $sfReliableActorTable = $null
    $sfReliableServiceTable = $null
    $sfOperationalTable = $null
    Write-Debug $scaleSetDiagnostics
    $serviceFabricProviderList = ""
    $etwManifestProviderList = ""

    if ( $scaleSetDiagnostics.xmlCfg )
    {
        Write-Debug ("Found XMLcfg")
        $xmlCfg = [System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($scaleSetDiagnostics.xmlCfg))
        Write-Debug $xmlCfg
        $etwProviders = Select-Xml -Content $xmlCfg -XPath "//EtwProviders"                
        $serviceFabricProviderList = $etwProviders.Node.EtwEventSourceProviderConfiguration
        $etwManifestProviderList = $etwProviders.Node.EtwManifestProviderConfiguration
    } elseif ($scaleSetDiagnostics.WadCfg )
    {
        Write-Debug ("Found WADcfg")
        Write-Debug $scaleSetDiagnostics.WadCfg
        $serviceFabricProviderList = $scaleSetDiagnostics.WadCfg.DiagnosticMonitorConfiguration.EtwProviders.EtwEventSourceProviderConfiguration
        $etwManifestProviderList = $scaleSetDiagnostics.WadCfg.DiagnosticMonitorConfiguration.EtwProviders.EtwManifestProviderConfiguration
    } else
    {
        Write-Error "Unable tooparse Azure Diagnostics setting for $id"
        Write-Warning ("$id does not have diagnostics enabled")
    }

    foreach ($provider in $serviceFabricProviderList)
    {
        Write-Debug ("Event Source Provider: " + $provider.Provider + " Destination: " + $provider.DefaultEvents.eventDestination)
        if ($provider.Provider -eq "Microsoft-ServiceFabric-Actors")
        {
            $sfReliableActorTable = $provider.DefaultEvents.eventDestination
        } elseif ($provider.Provider -eq "Microsoft-ServiceFabric-Services")
        {
            $sfReliableServiceTable = $provider.DefaultEvents.eventDestination
        } else
        {
            Check-ETWProviderLogging $id $provider.Provider "ETWEventTable" $provider.DefaultEvents.eventDestination
        }
    }
    foreach ($provider in $etwManifestProviderList)
    {
        Write-Debug ("Manifest Provider: " + $provider.Provider + " Destination: " + $provider.DefaultEvents.eventDestination)
        if ($provider.Provider -eq "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8")
        {
            $sfOperationalTable = $provider.DefaultEvents.eventDestination
        } else
        {
            Check-ETWProviderLogging $id $provider.Provider "ETWEventTable" $provider.DefaultEvents.eventDestination
        }
    }

    Check-ETWProviderLogging $id "Microsoft-ServiceFabric-Actors" "ServiceFabricReliableActorEventTable" $sfReliableActorTable
    Check-ETWProviderLogging $id "Microsoft-ServiceFabric-Services" "ServiceFabricReliableServiceEventTable" $sfReliableServiceTable
    Check-ETWProviderLogging $id "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8 (System events)" "ServiceFabricSystemEventTable" $sfOperationalTable

    Write-Verbose ("StorageAccount: " + $scaleSetDiagnostics.StorageAccount)

    $storageAccountsFound += ($scaleSetDiagnostics.StorageAccount)
    return ($storageAccountsFound)
}

# This script uses Get-AzureRmVMDiagnosticsExtension and needs a version where -Name is not a required parameter
Import-Module AzureRM.Compute -MinimumVersion 1.2.2

try
{
    Get-AzureRmContext
}
catch [System.Management.Automation.PSInvalidOperationException]
{
    Login-AzureRmAccount
}

$allResources = Get-AzureRmResource

$OMSworkspace = $allResources.Where({($_.ResourceType -eq "Microsoft.OperationalInsights/workspaces") -and ($_.ResourceName -eq $workspaceName)})

if ($OMSworkspace.Name -ne $workspaceName)
{
    Write-Error ("Unable toofind Log Analytics Workspace " + $workspaceName)
}

$serviceFabricClusters = $allResources.Where({$_.ResourceType -eq "Microsoft.ServiceFabric/clusters"})
$storageAccountList = @()
foreach($cluster in $serviceFabricClusters) {
    Write-Verbose ("Checking cluster: " + $cluster.Name)
    $scaleSet = ($allResources.Where({($_.ResourceType -eq "Microsoft.Compute/virtualMachineScaleSets") -and ($_.ResourceGroupName -eq $cluster.ResourceGroupName)}))

    foreach($set in $scaleSet) {
        $resource = Get-AzureRmResource -ResourceId $set.ResourceId
        $extensions = $resource.Properties.VirtualMachineProfile.ExtensionProfile.Extensions
        foreach($ext in $extensions) {
            if ($ext.Properties.Publisher -eq "Microsoft.Azure.Diagnostics" -and $ext.Properties.Type -eq "IaaSDiagnostics") {
                $storageAccountList += (Check-ServiceFabricScaleSetDiagnostics $ext.Properties.Settings)
            }
        }
    }
}

$storageAccountList = $storageAccountList | Sort-Object | Get-Unique
$storageAccountsToCheck = ($allResources.Where({($_.ResourceType -eq "Microsoft.Storage/storageAccounts") -and ($_.ResourceName -in $storageAccountList)}))

foreach($storageAccount in $storageAccountsToCheck)
{
    Check-TablesForData $storageAccount
    Check-OMSLogAnalyticsConfiguration $OMSworkspace $storageAccount
}
 ```


## <a name="next-steps"></a><span data-ttu-id="b66ec-191">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b66ec-191">Next steps</span></span>
* <span data-ttu-id="b66ec-192">Use [búsquedas de registros de análisis de registros](log-analytics-log-searches.md) tooview obtener datos de eventos de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="b66ec-192">Use [Log Searches in Log Analytics](log-analytics-log-searches.md) tooview detailed Service Fabric event data.</span></span>
