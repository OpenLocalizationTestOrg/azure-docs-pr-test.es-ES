---
title: "Agregación de eventos de Azure Service Fabric con Azure Diagnostics de Windows | Microsoft Docs"
description: "Obtenga información sobre la agregación y la recopilación de eventos con WAD para la supervisión y el diagnóstico de clústeres de Azure Service Fabric."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/17/2017
ms.author: dekapur
ms.openlocfilehash: 5773361fdec4cb8ee54fa2856f6aa969d5dac4e9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="event-aggregation-and-collection-using-windows-azure-diagnostics"></a><span data-ttu-id="b8906-103">Recopilación y agregación de eventos con Azure Diagnostics de Windows</span><span class="sxs-lookup"><span data-stu-id="b8906-103">Event aggregation and collection using Windows Azure Diagnostics</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b8906-104">Windows</span><span class="sxs-lookup"><span data-stu-id="b8906-104">Windows</span></span>](service-fabric-diagnostics-event-aggregation-wad.md)
> * [<span data-ttu-id="b8906-105">Linux</span><span class="sxs-lookup"><span data-stu-id="b8906-105">Linux</span></span>](service-fabric-diagnostics-event-aggregation-lad.md)
>
>

<span data-ttu-id="b8906-106">Cuando se ejecuta un clúster de Azure Service Fabric, es conveniente recopilar los registros de todos los nodos en una ubicación central.</span><span class="sxs-lookup"><span data-stu-id="b8906-106">When you're running an Azure Service Fabric cluster, it's a good idea to collect the logs from all the nodes in a central location.</span></span> <span data-ttu-id="b8906-107">La presencia de los registros en una ubicación central facilita el análisis y la solución de los problemas del clúster o de las aplicaciones y los servicios que se ejecutan en ese clúster.</span><span class="sxs-lookup"><span data-stu-id="b8906-107">Having the logs in a central location helps you analyze and troubleshoot issues in your cluster, or issues in the applications and services running in that cluster.</span></span>

<span data-ttu-id="b8906-108">Uno de los métodos para cargar y recopilar registros es usar la extensión Azure Diagnostics de Windows (WAD), que carga registros en Azure Storage, y también tiene la opción de enviar registros a Azure Application Insights o Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="b8906-108">One way to upload and collect logs is to use the Windows Azure Diagnostics (WAD) extension, which uploads logs to Azure Storage, and also has the option to send logs to Azure Application Insights or Event Hubs.</span></span> <span data-ttu-id="b8906-109">También puede usar un proceso externo para leer los eventos desde el almacenamiento y colocarlos en un producto de plataforma de análisis, como [Log Analytics de OMS](../log-analytics/log-analytics-service-fabric.md) u otra solución de análisis de registros.</span><span class="sxs-lookup"><span data-stu-id="b8906-109">You can also use an external process to read the events from storage and place them in an analysis platform product, such as [OMS Log Analytics](../log-analytics/log-analytics-service-fabric.md) or another log-parsing solution.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b8906-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="b8906-110">Prerequisites</span></span>
<span data-ttu-id="b8906-111">Estas herramientas se usan para realizar algunas de las operaciones que se describen en este documento:</span><span class="sxs-lookup"><span data-stu-id="b8906-111">These tools are used to perform some of the operations in this document:</span></span>

* <span data-ttu-id="b8906-112">[Diagnósticos de Azure](../cloud-services/cloud-services-dotnet-diagnostics.md) (relacionado con Azure Cloud Services, aunque con información y ejemplos adecuados)</span><span class="sxs-lookup"><span data-stu-id="b8906-112">[Azure Diagnostics](../cloud-services/cloud-services-dotnet-diagnostics.md) (related to Azure Cloud Services but has good information and examples)</span></span>
* [<span data-ttu-id="b8906-113">Administrador de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="b8906-113">Azure Resource Manager</span></span>](../azure-resource-manager/resource-group-overview.md)
* [<span data-ttu-id="b8906-114">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="b8906-114">Azure PowerShell</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="b8906-115">Cliente de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b8906-115">Azure Resource Manager client</span></span>](https://github.com/projectkudu/ARMClient)
* [<span data-ttu-id="b8906-116">Plantilla de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b8906-116">Azure Resource Manager template</span></span>](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="log-and-event-sources"></a><span data-ttu-id="b8906-117">Orígenes de eventos y registros</span><span class="sxs-lookup"><span data-stu-id="b8906-117">Log and event sources</span></span>

### <a name="service-fabric-platform-events"></a><span data-ttu-id="b8906-118">Eventos de plataforma de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="b8906-118">Service Fabric platform events</span></span>
<span data-ttu-id="b8906-119">Como se describe en [este artículo](service-fabric-diagnostics-event-generation-infra.md), Service Fabric configura algunos canales de registro predefinidos. Los que se indican a continuación se configuran fácilmente con WAD para que envíen datos de supervisión y diagnóstico a una tabla de almacenamiento u otro lugar:</span><span class="sxs-lookup"><span data-stu-id="b8906-119">As discussed in [this article](service-fabric-diagnostics-event-generation-infra.md), Service Fabric sets you up with a few out-of-the-box logging channels, of which the following channels are easily configured with WAD to send monitoring and diagnostics data to a storage table or elsewhere:</span></span>
  * <span data-ttu-id="b8906-120">Eventos operativos: operaciones de nivel superior realizadas por la plataforma Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="b8906-120">Operational events: higher-level operations that the Service Fabric platform performs.</span></span> <span data-ttu-id="b8906-121">Algunos ejemplos son la creación de aplicaciones y servicios, los cambios de estado de nodo y la información sobre la actualización.</span><span class="sxs-lookup"><span data-stu-id="b8906-121">Examples include creation of applications and services, node state changes, and upgrade information.</span></span> <span data-ttu-id="b8906-122">Se emiten como registros de Seguimiento de eventos para Windows (ETW).</span><span class="sxs-lookup"><span data-stu-id="b8906-122">These are emitted as Event Tracing for Windows (ETW) logs</span></span>
  * [<span data-ttu-id="b8906-123">Eventos del modelo de programación de Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="b8906-123">Reliable Actors programming model events</span></span>](service-fabric-reliable-actors-diagnostics.md)
  * [<span data-ttu-id="b8906-124">Eventos del modelo de programación de Reliable Services</span><span class="sxs-lookup"><span data-stu-id="b8906-124">Reliable Services programming model events</span></span>](service-fabric-reliable-services-diagnostics.md)

### <a name="application-events"></a><span data-ttu-id="b8906-125">Eventos de aplicación</span><span class="sxs-lookup"><span data-stu-id="b8906-125">Application events</span></span>
 <span data-ttu-id="b8906-126">Son los eventos que se emiten desde el código de las aplicaciones y los servicios y que se escriben mediante la clase auxiliar EventSource proporcionada en las plantillas de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b8906-126">Events emitted from your applications' and services' code and written out by using the EventSource helper class provided in the Visual Studio templates.</span></span> <span data-ttu-id="b8906-127">Para obtener más información sobre cómo escribir registros EventSource de la aplicación, vea [Supervisión y diagnóstico de servicios en una configuración de desarrollo de máquina local](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span><span class="sxs-lookup"><span data-stu-id="b8906-127">For more information on how to write EventSource logs from your application, see [Monitor and diagnose services in a local machine development setup](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span></span>

## <a name="deploy-the-diagnostics-extension"></a><span data-ttu-id="b8906-128">Implementación de la extensión de Diagnósticos</span><span class="sxs-lookup"><span data-stu-id="b8906-128">Deploy the Diagnostics extension</span></span>
<span data-ttu-id="b8906-129">El primer paso para recopilar registros será implementar la extensión WAD en cada una de las máquinas virtuales del clúster de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="b8906-129">The first step in collecting logs is to deploy the Diagnostics extension on each of the VMs in the Service Fabric cluster.</span></span> <span data-ttu-id="b8906-130">La extensión de Diagnósticos recopila registros en cada máquina virtual y los carga a la cuenta de almacenamiento que especifique.</span><span class="sxs-lookup"><span data-stu-id="b8906-130">The Diagnostics extension collects logs on each VM and uploads them to the storage account that you specify.</span></span> <span data-ttu-id="b8906-131">Los pasos varían ligeramente en función de si se utiliza Azure Portal o Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b8906-131">The steps vary a little based on whether you use the Azure portal or Azure Resource Manager.</span></span> <span data-ttu-id="b8906-132">Los pasos varían también en función de si la implementación forma parte de la creación del clúster o si es para un clúster que ya existe.</span><span class="sxs-lookup"><span data-stu-id="b8906-132">The steps also vary based on whether the deployment is part of cluster creation or is for a cluster that already exists.</span></span> <span data-ttu-id="b8906-133">Echemos un vistazo a los pasos para cada escenario.</span><span class="sxs-lookup"><span data-stu-id="b8906-133">Let's look at the steps for each scenario.</span></span>

### <a name="deploy-the-diagnostics-extension-as-part-of-cluster-creation-through-azure-portal"></a><span data-ttu-id="b8906-134">Implementación de la extensión Diagnostics como parte de la creación del clúster a través de Azure Portal</span><span class="sxs-lookup"><span data-stu-id="b8906-134">Deploy the Diagnostics extension as part of cluster creation through Azure portal</span></span>
<span data-ttu-id="b8906-135">Para implementar la extensión Diagnostics en las máquinas virtuales del clúster como parte de la creación de dicho clúster, se usa el panel Configuración de diagnóstico que se muestra en la imagen siguiente. Asegúrese de que Diagnostics esté establecido en **Activado** (valor predeterminado).</span><span class="sxs-lookup"><span data-stu-id="b8906-135">To deploy the Diagnostics extension to the VMs in the cluster as part of cluster creation, you use the Diagnostics settings panel shown in the following image - ensure that Diagnostics is set to **On** (the default setting).</span></span> <span data-ttu-id="b8906-136">Después de crear el clúster, no puede cambiar esta configuración mediante el portal.</span><span class="sxs-lookup"><span data-stu-id="b8906-136">After you create the cluster, you can't change these settings by using the portal.</span></span>

![Configuración de Diagnósticos de Azure en el portal para crear un clúster](media/service-fabric-diagnostics-event-aggregation-wad/azure-enable-diagnostics.png)

<span data-ttu-id="b8906-138">Al crear un clúster mediante el portal, es muy recomendable descargar la plantilla **antes de hacer clic en Aceptar** para crear el clúster.</span><span class="sxs-lookup"><span data-stu-id="b8906-138">When you're creating a cluster by using the portal, we highly recommend that you download the template **before you click OK** to create the cluster.</span></span> <span data-ttu-id="b8906-139">Para más información, vea [Configuración de un clúster de Service Fabric con una plantilla de Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).</span><span class="sxs-lookup"><span data-stu-id="b8906-139">For details, refer to [Set up a Service Fabric cluster by using an Azure Resource Manager template](service-fabric-cluster-creation-via-arm.md).</span></span> <span data-ttu-id="b8906-140">Necesitará la plantilla para realizar cambios más adelante, porque no se pueden realizar algunos cambios a través del portal.</span><span class="sxs-lookup"><span data-stu-id="b8906-140">You'll need the template to make changes later, because you can't make some changes by using the portal.</span></span>

### <a name="deploy-the-diagnostics-extension-as-part-of-cluster-creation-by-using-azure-resource-manager"></a><span data-ttu-id="b8906-141">Implementación de la extensión de Diagnósticos como parte de la creación del clúster a través del Administrador de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="b8906-141">Deploy the Diagnostics extension as part of cluster creation by using Azure Resource Manager</span></span>
<span data-ttu-id="b8906-142">Para crear un clúster mediante el Resource Manager, tiene que agregar el JSON de la configuración de Diagnósticos a la plantilla de Resource Manager del clúster completo antes de crear el clúster.</span><span class="sxs-lookup"><span data-stu-id="b8906-142">To create a cluster by using Resource Manager, you need to add the Diagnostics configuration JSON to the full cluster Resource Manager template before you create the cluster.</span></span> <span data-ttu-id="b8906-143">Dentro de los ejemplos de plantillas del Administrador de recursos, proporcionamos una plantilla de ejemplo del Administrador de recursos de clúster de cinco máquinas virtuales con la configuración de Diagnósticos añadida.</span><span class="sxs-lookup"><span data-stu-id="b8906-143">We provide a sample five-VM cluster Resource Manager template with Diagnostics configuration added to it as part of our Resource Manager template samples.</span></span> <span data-ttu-id="b8906-144">Puede verlo en: [Ejemplo de plantilla de clúster de cinco nodos con el Administrador de recursos de Diagnósticos](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype-wad)en la galería de ejemplos de Azure.</span><span class="sxs-lookup"><span data-stu-id="b8906-144">You can see it at this location in the Azure Samples gallery: [Five-node cluster with Diagnostics Resource Manager template sample](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype-wad).</span></span>

<span data-ttu-id="b8906-145">Para ver la configuración de Diagnósticos en la plantilla de Resource Manager, abra el archivo azuredeploy.json y busque **IaaSDiagnostics**.</span><span class="sxs-lookup"><span data-stu-id="b8906-145">To see the Diagnostics setting in the Resource Manager template, open the azuredeploy.json file and search for **IaaSDiagnostics**.</span></span> <span data-ttu-id="b8906-146">Para crear un clúster con esta plantilla, presione el botón **Deploy to Azure** (Implementar en Azure) disponible en el vínculo anterior.</span><span class="sxs-lookup"><span data-stu-id="b8906-146">To create a cluster by using this template, select the **Deploy to Azure** button available at the previous link.</span></span>

<span data-ttu-id="b8906-147">También puede descargar el ejemplo de Resource Manager, modificarlo y crear un clúster con la plantilla modificada mediante el comando `New-AzureRmResourceGroupDeployment` en una ventana de Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b8906-147">Alternatively, you can download the Resource Manager sample, make changes to it, and create a cluster with the modified template by using the `New-AzureRmResourceGroupDeployment` command in an Azure PowerShell window.</span></span> <span data-ttu-id="b8906-148">Vea el código siguiente para los parámetros que se pasan al comando.</span><span class="sxs-lookup"><span data-stu-id="b8906-148">See the following code for the parameters that you pass in to the command.</span></span> <span data-ttu-id="b8906-149">Para más información sobre cómo implementar un grupo de recursos con PowerShell, vea el artículo sobre la [implementación de un grupo de recursos con la plantilla de Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="b8906-149">For detailed information on how to deploy a resource group by using PowerShell, see the article [Deploy a resource group with the Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md).</span></span>

### <a name="deploy-the-diagnostics-extension-to-an-existing-cluster"></a><span data-ttu-id="b8906-150">Implementación de la extensión de Diagnósticos en un clúster existente</span><span class="sxs-lookup"><span data-stu-id="b8906-150">Deploy the Diagnostics extension to an existing cluster</span></span>
<span data-ttu-id="b8906-151">Si tiene un clúster existente que no tiene implementada la extensión Diagnósticos, o bien quiere modificar una configuración existente, puede agregarla o actualizarla.</span><span class="sxs-lookup"><span data-stu-id="b8906-151">If you have an existing cluster that doesn't have Diagnostics deployed, or if you want to modify an existing configuration, you can add or update it.</span></span> <span data-ttu-id="b8906-152">Modifique la plantilla de Resource Manager usada para crear el clúster existente o descargue la plantilla desde el portal, tal como se describió anteriormente.</span><span class="sxs-lookup"><span data-stu-id="b8906-152">Modify the Resource Manager template that's used to create the existing cluster or download the template from the portal as described earlier.</span></span> <span data-ttu-id="b8906-153">Modifique el archivo template.json mediante la realización de las siguientes tareas.</span><span class="sxs-lookup"><span data-stu-id="b8906-153">Modify the template.json file by performing the following tasks.</span></span>

<span data-ttu-id="b8906-154">Agregue un nuevo recurso de almacenamiento a la plantilla mediante una adición en la sección de recursos.</span><span class="sxs-lookup"><span data-stu-id="b8906-154">Add a new storage resource to the template by adding to the resources section.</span></span>

```json
{
  "apiVersion": "2015-05-01-preview",
  "type": "Microsoft.Storage/storageAccounts",
  "name": "[parameters('applicationDiagnosticsStorageAccountName')]",
  "location": "[parameters('computeLocation')]",
  "properties": {
    "accountType": "[parameters('applicationDiagnosticsStorageAccountType')]"
  },
  "tags": {
    "resourceType": "Service Fabric",
    "clusterName": "[parameters('clusterName')]"
  }
},
```

 <span data-ttu-id="b8906-155">A continuación, realice la adición en la sección de parámetros justo después de las definiciones de la cuenta de almacenamiento, entre `supportLogStorageAccountName` y `vmNodeType0Name`.</span><span class="sxs-lookup"><span data-stu-id="b8906-155">Next, add to the parameters section just after the storage account definitions, between `supportLogStorageAccountName` and `vmNodeType0Name`.</span></span> <span data-ttu-id="b8906-156">Reemplace el texto de marcador de posición *aquí va el nombre de la cuenta de almacenamiento* por el nombre de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="b8906-156">Replace the placeholder text *storage account name goes here* with the name of the storage account.</span></span>

```json
    "applicationDiagnosticsStorageAccountType": {
      "type": "string",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS"
      ],
      "defaultValue": "Standard_LRS",
      "metadata": {
        "description": "Replication option for the application diagnostics storage account"
      }
    },
    "applicationDiagnosticsStorageAccountName": {
      "type": "string",
      "defaultValue": "storage account name goes here",
      "metadata": {
        "description": "Name for the storage account that contains application diagnostics data from the cluster"
      }
    },
```
<span data-ttu-id="b8906-157">Luego, actualice la sección `VirtualMachineProfile` del archivo template.json. Para ello, agregue el siguiente código dentro de la matriz de extensiones.</span><span class="sxs-lookup"><span data-stu-id="b8906-157">Then, update the `VirtualMachineProfile` section of the template.json file by adding the following code within the extensions array.</span></span> <span data-ttu-id="b8906-158">Asegúrese de agregar una coma al principio o al final, según donde se inserte.</span><span class="sxs-lookup"><span data-stu-id="b8906-158">Be sure to add a comma at the beginning or the end, depending on where it's inserted.</span></span>

```json
{
    "name": "[concat(parameters('vmNodeType0Name'),'_Microsoft.Insights.VMDiagnosticsSettings')]",
    "properties": {
        "type": "IaaSDiagnostics",
        "autoUpgradeMinorVersion": true,
        "protectedSettings": {
        "storageAccountName": "[parameters('applicationDiagnosticsStorageAccountName')]",
        "storageAccountKey": "[listKeys(resourceId('Microsoft.Storage/storageAccounts', parameters('applicationDiagnosticsStorageAccountName')),'2015-05-01-preview').key1]",
        "storageAccountEndPoint": "https://core.windows.net/"
        },
        "publisher": "Microsoft.Azure.Diagnostics",
        "settings": {
        "WadCfg": {
            "DiagnosticMonitorConfiguration": {
            "overallQuotaInMB": "50000",
            "EtwProviders": {
                "EtwEventSourceProviderConfiguration": [
                {
                    "provider": "Microsoft-ServiceFabric-Actors",
                    "scheduledTransferKeywordFilter": "1",
                    "scheduledTransferPeriod": "PT5M",
                    "DefaultEvents": {
                    "eventDestination": "ServiceFabricReliableActorEventTable"
                    }
                },
                {
                    "provider": "Microsoft-ServiceFabric-Services",
                    "scheduledTransferPeriod": "PT5M",
                    "DefaultEvents": {
                    "eventDestination": "ServiceFabricReliableServiceEventTable"
                    }
                }
                ],
                "EtwManifestProviderConfiguration": [
                {
                    "provider": "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8",
                    "scheduledTransferLogLevelFilter": "Information",
                    "scheduledTransferKeywordFilter": "4611686018427387904",
                    "scheduledTransferPeriod": "PT5M",
                    "DefaultEvents": {
                    "eventDestination": "ServiceFabricSystemEventTable"
                    }
                }
                ]
            }
            }
        },
        "StorageAccount": "[parameters('applicationDiagnosticsStorageAccountName')]"
        },
        "typeHandlerVersion": "1.5"
    }
}
```

<span data-ttu-id="b8906-159">Después de modificar el archivo template.json tal como se indicó, vuelva a publicar la plantilla de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b8906-159">After you modify the template.json file as described, republish the Resource Manager template.</span></span> <span data-ttu-id="b8906-160">En caso de que la plantilla se haya exportado, si ejecuta el archivo deploy.ps1 , se vuelve a publicar dicha plantilla.</span><span class="sxs-lookup"><span data-stu-id="b8906-160">If the template was exported, running the deploy.ps1 file republishes the template.</span></span> <span data-ttu-id="b8906-161">Después de realizar la implementación, asegúrese de que el estado **ProvisioningState** sea **Correcto**.</span><span class="sxs-lookup"><span data-stu-id="b8906-161">After you deploy, ensure that **ProvisioningState** is **Succeeded**.</span></span>

## <a name="collect-health-and-load-events"></a><span data-ttu-id="b8906-162">Recopilar eventos de mantenimiento y carga</span><span class="sxs-lookup"><span data-stu-id="b8906-162">Collect health and load events</span></span>

<span data-ttu-id="b8906-163">A partir de la versión 5.4 de Service Fabric, los eventos de métricas de carga y estado de mantenimiento están disponibles para su recopilación.</span><span class="sxs-lookup"><span data-stu-id="b8906-163">Starting with the 5.4 release of Service Fabric, health and load metric events are available for collection.</span></span> <span data-ttu-id="b8906-164">Estos eventos reflejan los eventos generados por el sistema o por el código mediante las API de generación de informes de estado de mantenimiento o carga como [ReportPartitionHealth](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportpartitionhealth.aspx) o [ReportLoad](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportload.aspx).</span><span class="sxs-lookup"><span data-stu-id="b8906-164">These events reflect events generated by the system or your code by using the health or load reporting APIs such as [ReportPartitionHealth](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportpartitionhealth.aspx) or [ReportLoad](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportload.aspx).</span></span> <span data-ttu-id="b8906-165">Esto permite agregar y ver el estado de mantenimiento del sistema en el tiempo, y generar alertas basadas en eventos de estado de mantenimiento o carga.</span><span class="sxs-lookup"><span data-stu-id="b8906-165">This allows for aggregating and viewing system health over time and for alerting based on health or load events.</span></span> <span data-ttu-id="b8906-166">Para ver estos eventos en el Visor de eventos de diagnóstico de Visual Studio, agregue "Microsoft-ServiceFabric:4:0x4000000000000008" a la lista de proveedores de ETW.</span><span class="sxs-lookup"><span data-stu-id="b8906-166">To view these events in Visual Studio's Diagnostic Event Viewer add "Microsoft-ServiceFabric:4:0x4000000000000008" to the list of ETW providers.</span></span>

<span data-ttu-id="b8906-167">Para recopilar los eventos, modifique la plantilla de Resource Manager para incluir lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="b8906-167">To collect the events, modify the Resource Manager template to include</span></span>

```json
  "EtwManifestProviderConfiguration": [
    {
      "provider": "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8",
      "scheduledTransferLogLevelFilter": "Information",
      "scheduledTransferKeywordFilter": "4611686018427387912",
      "scheduledTransferPeriod": "PT5M",
      "DefaultEvents": {
        "eventDestination": "ServiceFabricSystemEventTable"
      }
    }
```

## <a name="collect-reverse-proxy-events"></a><span data-ttu-id="b8906-168">Recopilación de eventos de proxy inverso</span><span class="sxs-lookup"><span data-stu-id="b8906-168">Collect reverse proxy events</span></span>

<span data-ttu-id="b8906-169">A partir de la versión 5.7 de Service Fabric, los eventos de [proy inverso](service-fabric-reverseproxy.md) están disponibles para la recopilación.</span><span class="sxs-lookup"><span data-stu-id="b8906-169">Starting with the 5.7 release of Service Fabric, [reverse proxy](service-fabric-reverseproxy.md) events are available for collection.</span></span>
<span data-ttu-id="b8906-170">El proxy inverso emite eventos en dos canales, uno que contiene los eventos de error que reflejan los errores de procesamiento de solicitudes y el otro que contiene los eventos detallados de todas las solicitudes procesadas en el proxy inverso.</span><span class="sxs-lookup"><span data-stu-id="b8906-170">Reverse proxy emits events into two channels, one containing error events reflecting request processing failures and the other one containing verbose events about all the requests processed at the reverse proxy.</span></span> 

1. <span data-ttu-id="b8906-171">Recopilación de eventos de error: para ver estos eventos en el Visor de eventos de diagnóstico de Visual Studio, agregue "Microsoft-ServiceFabric:4:0x4000000000000010" a la lista de proveedores de ETW.</span><span class="sxs-lookup"><span data-stu-id="b8906-171">Collect error events: To view these events in Visual Studio's Diagnostic Event Viewer add "Microsoft-ServiceFabric:4:0x4000000000000010" to the list of ETW providers.</span></span>
<span data-ttu-id="b8906-172">Para recopilar los eventos de los clústeres de Azure, modifique la plantilla de Resource Manager para incluir lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="b8906-172">To collect the events from Azure clusters, modify the Resource Manager template to include</span></span>

```json
  "EtwManifestProviderConfiguration": [
    {
      "provider": "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8",
      "scheduledTransferLogLevelFilter": "Information",
      "scheduledTransferKeywordFilter": "4611686018427387920",
      "scheduledTransferPeriod": "PT5M",
      "DefaultEvents": {
        "eventDestination": "ServiceFabricSystemEventTable"
      }
    }
```

2. <span data-ttu-id="b8906-173">Recopilación de todos los eventos de procesamiento de solicitud: en el Visor de eventos de diagnóstico de Visual Studio, actualice la entrada Microsoft-ServiceFabric en la lista de proveedores de ETW a "Microsoft-ServiceFabric:4:0x4000000000000020".</span><span class="sxs-lookup"><span data-stu-id="b8906-173">Collect all request processing events: In Visual Studio's Diagnostic Event Viewer, update the Microsoft-ServiceFabric entry in the ETW provider list to "Microsoft-ServiceFabric:4:0x4000000000000020".</span></span>
<span data-ttu-id="b8906-174">En los clústeres de Azure Service Fabric, modifique la plantilla de Resource Manager para incluir lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="b8906-174">For Azure Service Fabric clusters, modify the resource manager template to include</span></span>

```json
  "EtwManifestProviderConfiguration": [
    {
      "provider": "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8",
      "scheduledTransferLogLevelFilter": "Information",
      "scheduledTransferKeywordFilter": "4611686018427387936",
      "scheduledTransferPeriod": "PT5M",
      "DefaultEvents": {
        "eventDestination": "ServiceFabricSystemEventTable"
      }
    }
```
> <span data-ttu-id="b8906-175">Se recomienda habilitar con prudencia la recopilación de eventos de este canal ya que se recopila todo el tráfico a través del proxy inverso y puede consumir rápidamente la capacidad de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="b8906-175">It is recommended to judiciously enable collecting events from this channel as this collects all traffic through the reverse proxy and can quickly consume storage capacity.</span></span>

<span data-ttu-id="b8906-176">Para los clústeres de Azure Service Fabric, los eventos de todos los nodos se recopilan y se agregan en SystemEventTable.</span><span class="sxs-lookup"><span data-stu-id="b8906-176">For Azure Service Fabric clusters, the events from all the nodes are collected and aggregated in the SystemEventTable.</span></span>
<span data-ttu-id="b8906-177">Para obtener información sobre solución de problemas de los eventos de proxy inverso, consulte la [Guía de diagnóstico de proxy inverso](service-fabric-reverse-proxy-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="b8906-177">For detailed troubleshooting of the reverse proxy events, refer the [reverse proxy diagnostics guide](service-fabric-reverse-proxy-diagnostics.md).</span></span>

## <a name="collect-from-new-eventsource-channels"></a><span data-ttu-id="b8906-178">Recopilar desde canales EventSource nuevos</span><span class="sxs-lookup"><span data-stu-id="b8906-178">Collect from new EventSource channels</span></span>

<span data-ttu-id="b8906-179">Para actualizar Diagnostics de forma que recopile registros de canales EventSource nuevos que representan una nueva aplicación que vaya a implementar, siga los mismos pasos que se han descrito anteriormente para configurar Diagnostics para un clúster existente.</span><span class="sxs-lookup"><span data-stu-id="b8906-179">To update Diagnostics to collect logs from new EventSource channels that represent a new application that you're about to deploy, perform the same steps as previously described for the setup of Diagnostics for an existing cluster.</span></span>

<span data-ttu-id="b8906-180">Actualice la sección `EtwEventSourceProviderConfiguration` del archivo template.json para agregar entradas para los canales EventSource nuevos antes de aplicar la actualización de la configuración mediante el comando `New-AzureRmResourceGroupDeployment` de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b8906-180">Update the `EtwEventSourceProviderConfiguration` section in the template.json file to add entries for the new EventSource channels before you apply the configuration update by using the `New-AzureRmResourceGroupDeployment` PowerShell command.</span></span> <span data-ttu-id="b8906-181">El nombre del origen del evento se define como parte del código en el archivo generado en Visual Studio ServiceEventSource.cs.</span><span class="sxs-lookup"><span data-stu-id="b8906-181">The name of the event source is defined as part of your code in the Visual Studio-generated ServiceEventSource.cs file.</span></span>

<span data-ttu-id="b8906-182">Por ejemplo, si el origen del evento se denomina My-Eventsource, agregue el código siguiente para colocar los eventos de My-Eventsource en una tabla denominada MyDestinationTableName.</span><span class="sxs-lookup"><span data-stu-id="b8906-182">For example, if your event source is named My-Eventsource, add the following code to place the events from My-Eventsource into a table named MyDestinationTableName.</span></span>

```json
        {
            "provider": "My-Eventsource",
            "scheduledTransferPeriod": "PT5M",
            "DefaultEvents": {
            "eventDestination": "MyDestinationTableName"
            }
        }
```

<span data-ttu-id="b8906-183">Para recopilar registros de eventos o contadores de rendimiento, modifique la plantilla de Resource Manager con los ejemplos proporcionados en [Creación de una máquina virtual de Windows con supervisión y diagnóstico mediante una plantilla de Azure Resource Manager](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b8906-183">To collect performance counters or event logs, modify the Resource Manager template by using the examples provided in [Create a Windows virtual machine with monitoring and diagnostics by using an Azure Resource Manager template](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="b8906-184">Luego, vuelva a publicar la plantilla de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b8906-184">Then, republish the Resource Manager template.</span></span>

## <a name="collect-performance-counters"></a><span data-ttu-id="b8906-185">Recopilar contadores de rendimiento</span><span class="sxs-lookup"><span data-stu-id="b8906-185">Collect Performance Counters</span></span>

<span data-ttu-id="b8906-186">Para recopilar métricas de rendimiento del clúster, agregue los contadores de rendimiento a "WadCfg > DiagnosticMonitorConfiguration" en la plantilla de Resource Manager para el clúster.</span><span class="sxs-lookup"><span data-stu-id="b8906-186">To collect performance metrics from your cluster, add the performance counters to your "WadCfg > DiagnosticMonitorConfiguration" in the Resource Manager template for your cluster.</span></span> <span data-ttu-id="b8906-187">Vea en [Service Fabric Performance Counters](service-fabric-diagnostics-event-generation-perf.md) (Contadores de rendimiento de Service Fabric) los contadores de rendimiento que se recomienda recopilar.</span><span class="sxs-lookup"><span data-stu-id="b8906-187">See [Service Fabric Performance Counters](service-fabric-diagnostics-event-generation-perf.md) for performance counters that we recommend collecting.</span></span>

<span data-ttu-id="b8906-188">Por ejemplo, aquí hemos establecido un contador de rendimiento que se muestrea cada 15 segundos (esto se puede cambiar y sigue el formato "PT\<tiempo>\<unidad>", por ejemplo, PT3M muestrea cada tres minutos) y se transfiere a la tabla de almacenamiento adecuada cada minuto.</span><span class="sxs-lookup"><span data-stu-id="b8906-188">For example, here we set one performance counter, sampled every 15 seconds (this can be changed and follows the format of "PT\<time>\<unit>", for example, PT3M would sample at three minute intervals), and transferred to the appropriate storage table every one minute.</span></span>

  ```json
  "PerformanceCounters": {
      "scheduledTransferPeriod": "PT1M",
      "PerformanceCounterConfiguration": [
          {
              "counterSpecifier": "\\Processor(_Total)\\% Processor Time",
              "sampleRate": "PT15S",
              "unit": "Percent",
              "annotation": [
              ],
              "sinks": ""
          }
      ]
  }
  ```
  
<span data-ttu-id="b8906-189">Si usa un receptor de Application Insights, como se describe en la siguiente sección, y quiere que estas métricas aparezcan en Application Insights, asegúrese de agregar el nombre del receptor en la sección "receptores", como se indicó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="b8906-189">If you are using an Application Insights sink, as described in the section below, and want these metrics to show up in Application Insights, then make sure to add the sink name in the "sinks" section as shown above.</span></span> <span data-ttu-id="b8906-190">Además, considere la posibilidad de crear una tabla independiente a la que enviar sus contadores de rendimiento, para que no sobrecarguen los datos procedentes de los demás canales de registro que ha habilitado.</span><span class="sxs-lookup"><span data-stu-id="b8906-190">Additionally, consider creating a separate table to send your Performance Counters to, so they don't crowd out the data coming from the other logging channels you have enabled.</span></span>


## <a name="send-logs-to-application-insights"></a><span data-ttu-id="b8906-191">Enviar registros a Application Insights</span><span class="sxs-lookup"><span data-stu-id="b8906-191">Send logs to Application Insights</span></span>

<span data-ttu-id="b8906-192">Como parte de la configuración de WAD, puede enviar datos de supervisión y diagnóstico a Application Insights (AI).</span><span class="sxs-lookup"><span data-stu-id="b8906-192">Sending monitoring and diagnostics data to Application Insights (AI) can be done as part of the WAD configuration.</span></span> <span data-ttu-id="b8906-193">Si decide usar AI para el análisis y la visualización de eventos, lea [Event Analysis and Visualization with Application Insights](service-fabric-diagnostics-event-analysis-appinsights.md) (Análisis y visualización de eventos con Application Insights) para configurar un receptor de AI como parte de "WadCfg".</span><span class="sxs-lookup"><span data-stu-id="b8906-193">If you decide to use AI for event analysis and visualization, read [Event Analysis and Visualization with Application Insights](service-fabric-diagnostics-event-analysis-appinsights.md) to set up an AI Sink as part of your "WadCfg".</span></span>

## <a name="next-steps"></a><span data-ttu-id="b8906-194">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b8906-194">Next steps</span></span>

<span data-ttu-id="b8906-195">Una vez que haya configurado correctamente los diagnósticos de Azure, verá los datos en las tablas de almacenamiento de los registros de ETW y EventSource.</span><span class="sxs-lookup"><span data-stu-id="b8906-195">Once you have correctly configured Azure diagnostics, you will see data in your Storage tables from the ETW and EventSource logs.</span></span> <span data-ttu-id="b8906-196">Si decide usar OMS, Kibana u otra plataforma de análisis y visualización de datos que no se configura directamente en la plantilla de Resource Manager, asegúrese de configurar la plataforma de su elección para leer los datos de estas tablas de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="b8906-196">If you choose to use OMS, Kibana, or any other data analytics and visualization platform that is not directly configured in the Resource Manager template, make sure to set up the platform of your choice to read in the data from these storage tables.</span></span> <span data-ttu-id="b8906-197">Es relativamente fácil hacerlo para OMS, como se explica en [Event and log analysis through OMS](service-fabric-diagnostics-event-analysis-oms.md) (Análisis de eventos y registro mediante OMS).</span><span class="sxs-lookup"><span data-stu-id="b8906-197">Doing this for OMS is relatively trivial, and is explained in [Event and log analysis through OMS](service-fabric-diagnostics-event-analysis-oms.md).</span></span> <span data-ttu-id="b8906-198">Application Insights es un caso especial en este sentido, ya que puede configurarse como parte de la configuración de la extensión de Diagnostics, por lo que debe leer el [artículo correspondiente](service-fabric-diagnostics-event-analysis-appinsights.md) si opta por usar AI.</span><span class="sxs-lookup"><span data-stu-id="b8906-198">Application Insights is a bit of a special case in this sense, since it can be configured as part of the Diagnostics extension configuration, so refer to the [appropriate article](service-fabric-diagnostics-event-analysis-appinsights.md) if you choose to use AI.</span></span>

>[!NOTE]
><span data-ttu-id="b8906-199">Actualmente no existe ninguna manera de filtrar o limpiar los eventos que se envían a la tabla.</span><span class="sxs-lookup"><span data-stu-id="b8906-199">There is currently no way to filter or groom the events that are sent to the table.</span></span> <span data-ttu-id="b8906-200">Si no se implementa un proceso para quitar eventos de la tabla, la tabla seguirá aumentando.</span><span class="sxs-lookup"><span data-stu-id="b8906-200">If you don't implement a process to remove events from the table, the table will continue to grow.</span></span> <span data-ttu-id="b8906-201">Actualmente, hay un ejemplo de un servicio de limpieza de datos en ejecución en el [ejemplo de guardián](https://github.com/Azure-Samples/service-fabric-watchdog-service). Se recomienda que escriba uno para sí mismo, a menos que tenga una buena razón para almacenar los registros durante más de 30 o 90 días.</span><span class="sxs-lookup"><span data-stu-id="b8906-201">Currently, there is an example of a data grooming service running in the [Watchdog sample](https://github.com/Azure-Samples/service-fabric-watchdog-service), and it is recommended that you write one for yourself as well, unless there is a good reason for you to store logs beyond a 30 or 90 day timeframe.</span></span>

* [<span data-ttu-id="b8906-202">Información sobre cómo recopilar registros o contadores de rendimiento mediante la extensión de Diagnósticos</span><span class="sxs-lookup"><span data-stu-id="b8906-202">Learn how to collect performance counters or logs by using the Diagnostics extension</span></span>](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="b8906-203">Análisis y visualización de eventos con Application Insights</span><span class="sxs-lookup"><span data-stu-id="b8906-203">Event Analysis and Visualization with Application Insights</span></span>](service-fabric-diagnostics-event-analysis-appinsights.md)
* [<span data-ttu-id="b8906-204">Análisis y visualización de eventos con OMS</span><span class="sxs-lookup"><span data-stu-id="b8906-204">Event Analysis and Visualization with OMS</span></span>](service-fabric-diagnostics-event-analysis-oms.md)