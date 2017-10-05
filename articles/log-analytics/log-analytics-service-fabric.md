---
title: "Evaluación de aplicaciones de Service Fabric con Azure Log Analytics mediante PowerShell | Microsoft Docs"
description: "Puede usar la solución de Service Fabric con Log Analytics mediante PowerShell para evaluar el riesgo y el estado de las aplicaciones, los microservicios, los nodos y los clústeres de Service Fabric."
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
ms.openlocfilehash: ca86787e344aa5e9e68934dee6e9e83aeb4cc340
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="assess-azure-service-fabric-applications-and-micro-services-with-powershell"></a><span data-ttu-id="abfb5-103">Evaluación de aplicaciones y microservicios de Azure Service Fabric con PowerShell</span><span class="sxs-lookup"><span data-stu-id="abfb5-103">Assess Azure Service Fabric applications and micro-services with PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="abfb5-104">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="abfb5-104">Resource Manager</span></span>](log-analytics-service-fabric-azure-resource-manager.md)
> * [<span data-ttu-id="abfb5-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="abfb5-105">PowerShell</span></span>](log-analytics-service-fabric.md)
>
>


![Símbolo de Service Fabric](./media/log-analytics-service-fabric/service-fabric-assessment-symbol.png)

<span data-ttu-id="abfb5-107">En este artículo se describe cómo utilizar la solución de Service Fabric en Log Analytics para ayudar a identificar y solucionar problemas en su clúster de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="abfb5-107">This article describes how to use the Service Fabric solution in Log Analytics to help identify and troubleshoot issues across your Service Fabric cluster.</span></span> <span data-ttu-id="abfb5-108">Le ayuda a ver cómo funcionan los nodos de Service Fabric y cómo se ejecutan sus aplicaciones y microservicios.</span><span class="sxs-lookup"><span data-stu-id="abfb5-108">It helps you see how your Service Fabric nodes are performing and how your applications and micro-services are running.</span></span>

<span data-ttu-id="abfb5-109">La solución de Service Fabric utiliza datos de Diagnósticos de Azure de las máquinas virtuales de Service Fabric recopilando estos datos de las tablas WAD de Azure.</span><span class="sxs-lookup"><span data-stu-id="abfb5-109">The Service Fabric solution uses Azure Diagnostics data from your Service Fabric VMs, by collecting this data from your Azure WAD tables.</span></span> <span data-ttu-id="abfb5-110">Log Analytics lee a continuación los siguientes eventos del marco de Service Fabric:</span><span class="sxs-lookup"><span data-stu-id="abfb5-110">Log Analytics then reads the following Service Fabric framework events:</span></span>

- <span data-ttu-id="abfb5-111">**Eventos de Reliable Services**</span><span class="sxs-lookup"><span data-stu-id="abfb5-111">**Reliable Service Events**</span></span>
- <span data-ttu-id="abfb5-112">**Eventos de actor**</span><span class="sxs-lookup"><span data-stu-id="abfb5-112">**Actor Events**</span></span>
- <span data-ttu-id="abfb5-113">**Eventos operativos**</span><span class="sxs-lookup"><span data-stu-id="abfb5-113">**Operational Events**</span></span>
- <span data-ttu-id="abfb5-114">**Eventos de ETW personalizados**</span><span class="sxs-lookup"><span data-stu-id="abfb5-114">**Custom ETW events**</span></span>

<span data-ttu-id="abfb5-115">Con el panel de la solución de Service Fabric, se pueden ver los eventos pertinentes y problemas importantes de su entorno de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="abfb5-115">The Service Fabric solution dashboard shows you notable issues and relevant events in your Service Fabric environment.</span></span>

## <a name="installing-and-configuring-the-solution"></a><span data-ttu-id="abfb5-116">Instalación y configuración de la solución</span><span class="sxs-lookup"><span data-stu-id="abfb5-116">Installing and configuring the solution</span></span>
<span data-ttu-id="abfb5-117">Siga estos tres sencillos pasos para instalar y configurar la solución:</span><span class="sxs-lookup"><span data-stu-id="abfb5-117">Follow these three easy steps to install and configure the solution:</span></span>

1. <span data-ttu-id="abfb5-118">Asocie la suscripción de Azure que usó para crear todos los recursos del clúster, incluidas las cuentas de almacenamiento, a su área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="abfb5-118">Associate the Azure subscription that you used to create all cluster resources, including storage accounts, with your workspace.</span></span> <span data-ttu-id="abfb5-119">Consulte [Introducción a Log Analytics](log-analytics-get-started.md) para obtener información sobre cómo crear un área de trabajo de Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="abfb5-119">See [Get started with Log Analytics](log-analytics-get-started.md) for information about creating a Log Analytics workspace.</span></span>
2. <span data-ttu-id="abfb5-120">Configure Log Analytics para recopilar y ver los registros de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="abfb5-120">Configure Log Analytics to collect and view Service Fabric logs.</span></span>
3. <span data-ttu-id="abfb5-121">Habilite la solución de Service Fabric en el área de trabajo de Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="abfb5-121">Enable the Service Fabric solution in your workspace.</span></span>

## <a name="configure-log-analytics-to-collect-and-view-service-fabric-logs"></a><span data-ttu-id="abfb5-122">Configuración de Log Analytics para recopilar y ver los registros de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="abfb5-122">Configure Log Analytics to collect and view Service Fabric logs</span></span>
<span data-ttu-id="abfb5-123">En esta sección, aprenderá a configurar Log Analytics para recuperar registros de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="abfb5-123">In this section, you learn how to configure Log Analytics to retrieve Service Fabric logs.</span></span> <span data-ttu-id="abfb5-124">Los registros permiten ver, analizar y solucionar problemas del clúster o de las aplicaciones y los servicios que se ejecutan en ese clúster mediante el portal de OMS.</span><span class="sxs-lookup"><span data-stu-id="abfb5-124">The logs allow you to view, analyze, and troubleshoot issues in your cluster or in the applications and services running in that cluster, using the OMS portal.</span></span>

> [!NOTE]
> <span data-ttu-id="abfb5-125">Configure la extensión Azure Diagnostics para cargar los registros de las tablas de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="abfb5-125">Configure the Azure Diagnostics extension to upload the logs for storage tables.</span></span> <span data-ttu-id="abfb5-126">Las tablas deben coincidir con lo que busca Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="abfb5-126">The tables must match what Log Analytics looks for.</span></span> <span data-ttu-id="abfb5-127">Para más información, vea [Recopilación de registros con Diagnósticos de Azure](../service-fabric/service-fabric-diagnostics-how-to-setup-wad.md).</span><span class="sxs-lookup"><span data-stu-id="abfb5-127">For more information, see [How to collect logs with Azure Diagnostics](../service-fabric/service-fabric-diagnostics-how-to-setup-wad.md).</span></span> <span data-ttu-id="abfb5-128">Los ejemplos de valores de configuración en este artículo muestran los nombres que deben tener las tablas de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="abfb5-128">The configuration settings examples in this article show you what the names of the storage tables should be.</span></span> <span data-ttu-id="abfb5-129">Cuando se haya configurado Diagnósticos en el clúster y se carguen los registros en una cuenta de almacenamiento, el siguiente paso consiste en configurar Log Analytics para recopilar estos registros.</span><span class="sxs-lookup"><span data-stu-id="abfb5-129">Once Diagnostics is set up on the cluster and is uploading logs to a storage account, the next step is to configure Log Analytics to collect these logs.</span></span>
>
>

<span data-ttu-id="abfb5-130">Tendrá que actualizar la sección **EtwEventSourceProviderConfiguration** en el archivo **template.json** para agregar entradas para el nuevo EventSources antes de aplicar la actualización de la configuración mediante el comando **deploy.ps1**.</span><span class="sxs-lookup"><span data-stu-id="abfb5-130">Ensure that you update the **EtwEventSourceProviderConfiguration** section in the **template.json** file to add entries for the new EventSources before you apply the configuration update by running **deploy.ps1**.</span></span> <span data-ttu-id="abfb5-131">La tabla para la carga es la misma que (ETWEventTable).</span><span class="sxs-lookup"><span data-stu-id="abfb5-131">The table for upload is the same as (ETWEventTable).</span></span> <span data-ttu-id="abfb5-132">En este momento, Log Analytics solo puede leer los eventos ETW de aplicación desde la tabla *WADETWEventTable*.</span><span class="sxs-lookup"><span data-stu-id="abfb5-132">At the moment, Log Analytics can only read application ETW events from the *WADETWEventTable* table.</span></span>

<span data-ttu-id="abfb5-133">Las siguientes herramientas se usarán para realizar algunas de las operaciones que se describen en esta sección:</span><span class="sxs-lookup"><span data-stu-id="abfb5-133">The following tools are used to perform some of the operations in this section:</span></span>

* <span data-ttu-id="abfb5-134">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="abfb5-134">Azure PowerShell</span></span>
* [<span data-ttu-id="abfb5-135">Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="abfb5-135">Operations Management Suite</span></span>](http://www.microsoft.com/oms)

### <a name="configure-a-log-analytics-workspace-to-show-the-cluster-logs"></a><span data-ttu-id="abfb5-136">Configuración de un área de trabajo de Log Analytics para mostrar los registros del clúster</span><span class="sxs-lookup"><span data-stu-id="abfb5-136">Configure a Log Analytics workspace to show the cluster logs</span></span>

<span data-ttu-id="abfb5-137">Después de crear un área de trabajo de Log Analytics, configúrela para extraer registros de las tablas de almacenamiento Azure.</span><span class="sxs-lookup"><span data-stu-id="abfb5-137">After you create a Log Analytics workspace, configure the workspace to pull logs from the Azure storage tables.</span></span> <span data-ttu-id="abfb5-138">A continuación, ejecute el siguiente script de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="abfb5-138">Then, run the following PowerShell script:</span></span>

```
<#
    This script will configure an Operations Management Suite workspace (previously called an Operational Insights workspace) to read Diagnostics from an Azure Storage account.
    It will enable all supported data types (currently Service Fabric Events, ETW Events and IIS Logs).
    It supports Resource Manager storage accounts.
    If you have more than one Azure Subscription, you will be prompted for the subscription to configure.
    If you have more than one Log Analytics workspace you will be prompted for the workspace to configure.
    It will then look through your Service Fabric clusters, and configure your Log Analytics workspace to read Diagnostics from storage accounts that are connected to that cluster and have diagnostics enabled.
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
            $uiPrompt = "Enter the number corresponding to the Azure subscription you would like to work with.`n"

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
            $uiPrompt = "Enter the number corresponding to the workspace you want to configure.`n"
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
             Write-Warning ("$id No configuration found for $provider. Configure Azure diagnostics to write to $expectedTable.")
         }  
         elseif ( $table -ne $expectedTable )
         {
             Write-Warning ("$id $provider events are being written to $table instead of WAD$expectedTable. Events will not be collected by Log Analytics")
         }  
         else
         {
             Write-Verbose "$id $provider events are being written to WAD$expectedTable (Correct configuration.)"
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
         Write-Error "Unable to parse Azure Diagnostics setting for $id"
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
    $serviceFabricClusters = $allResources.Where({$_.ResourceType -eq "Microsoft.ServiceFabric/clusters"}) #pulls in all service fabric clusters in the resource
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
                                # HTTP Not Found is returned if the storage insight doesn't exist
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
                                      # If any of the tables from the table list are not already monitored, then we add them
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

<span data-ttu-id="abfb5-139">Después de configurar el área de trabajo de Log Analytics para leer las tablas de Azure de su cuenta de almacenamiento, inicie sesión en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="abfb5-139">After you've configured the Log Analytics workspace to read from the Azure tables in your storage account, log in to the Azure portal.</span></span> <span data-ttu-id="abfb5-140">En **Todos los recursos**, seleccione el área de trabajo de Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="abfb5-140">Select the Log Analytics workspace from **All Resources**.</span></span> <span data-ttu-id="abfb5-141">Se muestra el número de registros de la cuenta de almacenamiento conectados al área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="abfb5-141">The number of storage account logs connected to the workspace is displayed.</span></span> <span data-ttu-id="abfb5-142">Seleccione el icono **Registros de la cuenta de almacenamiento**.</span><span class="sxs-lookup"><span data-stu-id="abfb5-142">Select the **Storage account logs** tile.</span></span> <span data-ttu-id="abfb5-143">Revise la lista de registros de la cuenta de almacenamiento para comprobar que la cuenta de almacenamiento está conectada al área de trabajo correcta.</span><span class="sxs-lookup"><span data-stu-id="abfb5-143">Review the list of storage account logs to verify that your storage account is connected to the correct workspace.</span></span>

![Registros de la cuenta de almacenamiento](./media/log-analytics-service-fabric/sf1.png)

## <a name="enable-the-service-fabric-solution"></a><span data-ttu-id="abfb5-145">Habilitación de la solución de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="abfb5-145">Enable the Service Fabric solution</span></span>
<span data-ttu-id="abfb5-146">Use el siguiente script para agregar la solución a su área de trabajo de Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="abfb5-146">Use the following script to add the solution to your Log Analytics workspace.</span></span> <span data-ttu-id="abfb5-147">Ejecute el script de PowerShell usando la suscripción de Azure asociada al área de trabajo de Log Analytics en la que desea habilitar la solución de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="abfb5-147">Run the script in PowerShell, using the Azure subscription that is associated with the Log Analytics workspace that you want to enable the Service Fabric solution in.</span></span>

```
function Select-Subscription {
      $subscription = ""
      $allSubscriptions = Get-AzureRmSubscription
      switch ($allSubscriptions.Count) {
             0 {Write-Error "No Operations Management Suite workspaces found"}
             1 {return $allSubscriptions}
        default {
            $uiPrompt = "Enter the number corresponding to the Azure subscription you would like to work with.`n"
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
            $uiPrompt = "Enter the number corresponding to the workspace you want to configure.`n"
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

<span data-ttu-id="abfb5-148">Después de habilitar la solución, se agrega el icono de Service Fabric a la página *Información general* de Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="abfb5-148">After you enable the solution, the Service Fabric tile is added to your Log Analytics *Overview* page.</span></span> <span data-ttu-id="abfb5-149">La página muestra una vista de problemas importantes, como errores de runAsync y cancelaciones producidos en las últimas 24 horas.</span><span class="sxs-lookup"><span data-stu-id="abfb5-149">The page shows a view of notable issues such as runAsync failures and cancellations that occurred in the last 24 hours.</span></span>

![Icono de Service Fabric](./media/log-analytics-service-fabric/sf2.png)

### <a name="view-service-fabric-events"></a><span data-ttu-id="abfb5-151">Visualización de eventos de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="abfb5-151">View Service Fabric events</span></span>
<span data-ttu-id="abfb5-152">Haga clic en el icono de **Service Fabric** icono para abrir el panel de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="abfb5-152">Click the **Service Fabric** tile to open the Service Fabric dashboard.</span></span> <span data-ttu-id="abfb5-153">El panel incluye las columnas de la tabla siguiente.</span><span class="sxs-lookup"><span data-stu-id="abfb5-153">The dashboard includes the columns in the table that follows.</span></span> <span data-ttu-id="abfb5-154">Cada columna muestra los 10 principales eventos por recuento que coinciden con los criterios de esa columna para el intervalo de tiempo especificados.</span><span class="sxs-lookup"><span data-stu-id="abfb5-154">Each column lists the top 10 events by count matching that column's criteria for the specified time range.</span></span> <span data-ttu-id="abfb5-155">Puede ejecutar una búsqueda de registros que proporcione toda la lista haciendo clic en **Ver todo** en la parte inferior derecha de la columna o haciendo clic en el encabezado de columna.</span><span class="sxs-lookup"><span data-stu-id="abfb5-155">You can run a log search that provides the entire list by clicking **See all** at the right bottom of each column, or by clicking the column header.</span></span>

| <span data-ttu-id="abfb5-156">**Evento de Service Fabric**</span><span class="sxs-lookup"><span data-stu-id="abfb5-156">**Service Fabric event**</span></span> | <span data-ttu-id="abfb5-157">**descripción**</span><span class="sxs-lookup"><span data-stu-id="abfb5-157">**description**</span></span> |
| --- | --- |
| <span data-ttu-id="abfb5-158">Problemas importantes</span><span class="sxs-lookup"><span data-stu-id="abfb5-158">Notable Issues</span></span> | <span data-ttu-id="abfb5-159">Se muestran problemas, como RunAsyncFailures, RunAsynCancellations y nodos inactivos.</span><span class="sxs-lookup"><span data-stu-id="abfb5-159">Displays issues including RunAsyncFailures, RunAsynCancellations, and Node Downs.</span></span> |
| <span data-ttu-id="abfb5-160">Eventos operativos</span><span class="sxs-lookup"><span data-stu-id="abfb5-160">Operational Events</span></span> | <span data-ttu-id="abfb5-161">Se muestran eventos operativos destacados, como implementaciones y actualizaciones de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="abfb5-161">Displays notable operational events including application upgrade and deployments.</span></span> |
| <span data-ttu-id="abfb5-162">Eventos de servicios de confianza</span><span class="sxs-lookup"><span data-stu-id="abfb5-162">Reliable Service Events</span></span> | <span data-ttu-id="abfb5-163">Se muestran eventos destacados de Reliable Services, como Runasyncinvocations.</span><span class="sxs-lookup"><span data-stu-id="abfb5-163">Displays notable reliable service events including  Runasyncinvocations.</span></span> |
| <span data-ttu-id="abfb5-164">Eventos de actor</span><span class="sxs-lookup"><span data-stu-id="abfb5-164">Actor Events</span></span> | <span data-ttu-id="abfb5-165">Se muestran eventos destacados de actor generados por los microservicios.</span><span class="sxs-lookup"><span data-stu-id="abfb5-165">Displays notable actor events generated by your micro-services.</span></span> <span data-ttu-id="abfb5-166">Los eventos incluyen las excepciones producidas por un método de actor, las activaciones y desactivaciones de actor, etc.</span><span class="sxs-lookup"><span data-stu-id="abfb5-166">Events include exceptions thrown by an actor method, actor activations and deactivations, and so on.</span></span> |
| <span data-ttu-id="abfb5-167">Eventos de aplicación</span><span class="sxs-lookup"><span data-stu-id="abfb5-167">Application Events</span></span> | <span data-ttu-id="abfb5-168">Todos los eventos ETW personalizados generados por las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="abfb5-168">Displays all custom ETW events generated by your applications.</span></span> |

![Panel de Service Fabric](./media/log-analytics-service-fabric/sf3.png)

![Panel de Service Fabric](./media/log-analytics-service-fabric/sf4.png)

<span data-ttu-id="abfb5-171">En la siguiente tabla se muestran los métodos de recolección de datos y otros detalles sobre cómo se recopilan los datos para Service Fabric:</span><span class="sxs-lookup"><span data-stu-id="abfb5-171">The following table shows data collection methods and other details about how data is collected for Service Fabric:</span></span>

| <span data-ttu-id="abfb5-172">plataforma</span><span class="sxs-lookup"><span data-stu-id="abfb5-172">platform</span></span> | <span data-ttu-id="abfb5-173">Agente directo</span><span class="sxs-lookup"><span data-stu-id="abfb5-173">Direct Agent</span></span> | <span data-ttu-id="abfb5-174">Agente de Operations Manager</span><span class="sxs-lookup"><span data-stu-id="abfb5-174">Operations Manager agent</span></span> | <span data-ttu-id="abfb5-175">Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="abfb5-175">Azure Storage</span></span> | <span data-ttu-id="abfb5-176">¿Se requiere Operations Manager?</span><span class="sxs-lookup"><span data-stu-id="abfb5-176">Operations Manager required?</span></span> | <span data-ttu-id="abfb5-177">Se envían los datos del agente de Operations Manager a través del grupo de administración</span><span class="sxs-lookup"><span data-stu-id="abfb5-177">Operations Manager agent data sent via management group</span></span> | <span data-ttu-id="abfb5-178">Frecuencia de recopilación</span><span class="sxs-lookup"><span data-stu-id="abfb5-178">collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="abfb5-179">Windows</span><span class="sxs-lookup"><span data-stu-id="abfb5-179">Windows</span></span> |  |  | <span data-ttu-id="abfb5-180">&#8226;</span><span class="sxs-lookup"><span data-stu-id="abfb5-180">&#8226;</span></span> |  |  |<span data-ttu-id="abfb5-181">10 minutos</span><span class="sxs-lookup"><span data-stu-id="abfb5-181">10 minutes</span></span> |

> [!NOTE]
> <span data-ttu-id="abfb5-182">Cambie el ámbito de los eventos con **Data based on last seven days** (Datos basados en los últimos siete días) en la parte superior del panel.</span><span class="sxs-lookup"><span data-stu-id="abfb5-182">Change the scope of events with **Data based on last seven days** at the top of the dashboard.</span></span> <span data-ttu-id="abfb5-183">También puede mostrar los eventos generados en los últimos 7 días, 1 día o 6 horas,</span><span class="sxs-lookup"><span data-stu-id="abfb5-183">You can also show events generated within the last seven days, one day, or six hours.</span></span> <span data-ttu-id="abfb5-184">o bien seleccionar **Personalizado** y especificar un intervalo de fechas personalizado.</span><span class="sxs-lookup"><span data-stu-id="abfb5-184">Or, you can select **Custom** to specify a custom date range.</span></span>
>
>

## <a name="troubleshoot-your-service-fabric-and-log-analytics-configuration"></a><span data-ttu-id="abfb5-185">Solución de problemas de Service Fabric y configuración de Log Analytics</span><span class="sxs-lookup"><span data-stu-id="abfb5-185">Troubleshoot your Service Fabric and Log Analytics configuration</span></span>
<span data-ttu-id="abfb5-186">Si necesita comprobar la configuración de Log Analytics porque no puede ver datos de eventos en Log Analytics, use el siguiente script.</span><span class="sxs-lookup"><span data-stu-id="abfb5-186">If you need to verify your Log Analytics configuration because you are unable to view event data in Log Analytics, use the following script.</span></span> <span data-ttu-id="abfb5-187">Las acciones que realiza son las siguientes:</span><span class="sxs-lookup"><span data-stu-id="abfb5-187">It performs the following actions:</span></span>

1. <span data-ttu-id="abfb5-188">Lee la configuración de diagnóstico de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="abfb5-188">Reads your Service Fabric diagnostics configuration</span></span>
2. <span data-ttu-id="abfb5-189">Comprueba los datos escritos en las tablas</span><span class="sxs-lookup"><span data-stu-id="abfb5-189">Checks for data written into the tables</span></span>
3. <span data-ttu-id="abfb5-190">Comprueba que Log Analytics está configurado para leer las tablas</span><span class="sxs-lookup"><span data-stu-id="abfb5-190">Verifies that Log Analytics is configured to read from the tables</span></span>

```
<#
    Verify Service Fabric and Log Analytics configuration
    1. Read Service Fabric diagnostics configuration
    2. Check for data being written into the tables
    3. Verify Log Analytics is configured to read from the tables

    Supported tables:
    WADServiceFabricReliableActorEventTable
    WADServiceFabricReliableServiceEventTable
    WADServiceFabricSystemEventTable
    WADETWEventTable

    Script will write a warning for every misconfiguration detected
    To see items that are correctly configured set $VerbosePreference="Continue"
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
    Check if OMS Log Analytics is configured to index service fabric events from the specified table
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
            Write-Verbose ("OMS Log Analytics workspace " + $workspace.Name + " is configured to index service fabric actor, service and operational events from " + $storageAccount.Name)
        } else
        {
            Write-Warning ("OMS Log Analytics workspace " + $workspace.Name + " is not configured to index service fabric actor, service and operational events from " + $storageAccount.Name)
        }
        if ("WADETWEventTable" -in $currentStorageAccountInsight.Tables)
        {
            Write-Verbose ("OMS Log Analytics workspace " + $workspace.Name + " is configured to index service fabric application events from " + $storageAccount.Name)
        } else
        {
            Write-Warning ("OMS Log Analytics workspace " + $workspace.Name + " is not configured to index service fabric application events from " + $storageAccount.Name)
        }
    } else
    {
        Write-Warning ("OMS Log Analytics workspace " + $workspace.Name + "is not configured to read service fabric events from " + $storageAccount.Name)
    }    
}

<#
    Check Azure table storage to confirm there is recent data written by Service Fabric
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
                Write-Verbose ("Data was written to $table in " + $storageAccount.ResourceName + "after $recently")
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
    Check if ETW provider is configured to log events to the expected table storage
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
            Write-Warning ("$id No configuration found for $provider. Configure Azure diagnostics to write to $expectedTable.")
        }
        elseif ( $table -ne $expectedTable )
        {
            Write-Warning ("$id $provider events are being written to $table instead of WAD$expectedTable. Events will not be collected by Log Analytics")
        }
        else
        {
            Write-Verbose "$id $provider events are being written to WAD$expectedTable (Correct configuration.)"
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
        Write-Error "Unable to parse Azure Diagnostics setting for $id"
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
    Write-Error ("Unable to find Log Analytics Workspace " + $workspaceName)
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


## <a name="next-steps"></a><span data-ttu-id="abfb5-191">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="abfb5-191">Next steps</span></span>
* <span data-ttu-id="abfb5-192">Use [Búsquedas de registros en Log Analytics](log-analytics-log-searches.md) para ver datos detallados sobre los datos de eventos de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="abfb5-192">Use [Log Searches in Log Analytics](log-analytics-log-searches.md) to view detailed Service Fabric event data.</span></span>
