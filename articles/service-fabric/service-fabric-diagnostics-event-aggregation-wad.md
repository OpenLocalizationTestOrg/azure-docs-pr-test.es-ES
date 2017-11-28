---
title: "Agregación de eventos de servicio de Fabric con diagnósticos de Windows Azure aaaAzure | Documentos de Microsoft"
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
ms.openlocfilehash: 4827ce66620e61c5b4a8682db55952333113188a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="event-aggregation-and-collection-using-windows-azure-diagnostics"></a><span data-ttu-id="b410d-103">Recopilación y agregación de eventos con Azure Diagnostics de Windows</span><span class="sxs-lookup"><span data-stu-id="b410d-103">Event aggregation and collection using Windows Azure Diagnostics</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b410d-104">Windows</span><span class="sxs-lookup"><span data-stu-id="b410d-104">Windows</span></span>](service-fabric-diagnostics-event-aggregation-wad.md)
> * [<span data-ttu-id="b410d-105">Linux</span><span class="sxs-lookup"><span data-stu-id="b410d-105">Linux</span></span>](service-fabric-diagnostics-event-aggregation-lad.md)
>
>

<span data-ttu-id="b410d-106">Cuando se ejecuta un clúster de Azure Service Fabric, es un buena idea toocollect Hola inicia una sesión de todos los nodos de hello en una ubicación central.</span><span class="sxs-lookup"><span data-stu-id="b410d-106">When you're running an Azure Service Fabric cluster, it's a good idea toocollect hello logs from all hello nodes in a central location.</span></span> <span data-ttu-id="b410d-107">Tener registros de hello en una ubicación central le ayuda a analizar y solucionar problemas en el clúster o problemas en aplicaciones de Hola y servicios que se ejecutan en ese clúster.</span><span class="sxs-lookup"><span data-stu-id="b410d-107">Having hello logs in a central location helps you analyze and troubleshoot issues in your cluster, or issues in hello applications and services running in that cluster.</span></span>

<span data-ttu-id="b410d-108">Tooupload de una forma y recopilar registros es la extensión de diagnósticos de Windows Azure (WAD) de hello toouse, que carga tooAzure almacenamiento de registros pero también tiene Hola opción toosend registros tooAzure Application Insights o concentradores de eventos.</span><span class="sxs-lookup"><span data-stu-id="b410d-108">One way tooupload and collect logs is toouse hello Windows Azure Diagnostics (WAD) extension, which uploads logs tooAzure Storage, and also has hello option toosend logs tooAzure Application Insights or Event Hubs.</span></span> <span data-ttu-id="b410d-109">También puede usar un proceso externo tooread Hola de eventos de almacenamiento y colocarlos en un producto de plataforma de análisis, como [OMS Log Analytics](../log-analytics/log-analytics-service-fabric.md) u otra solución de análisis de registro.</span><span class="sxs-lookup"><span data-stu-id="b410d-109">You can also use an external process tooread hello events from storage and place them in an analysis platform product, such as [OMS Log Analytics](../log-analytics/log-analytics-service-fabric.md) or another log-parsing solution.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b410d-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="b410d-110">Prerequisites</span></span>
<span data-ttu-id="b410d-111">Estas herramientas están tooperform usado alguna de las operaciones de hello en este documento:</span><span class="sxs-lookup"><span data-stu-id="b410d-111">These tools are used tooperform some of hello operations in this document:</span></span>

* <span data-ttu-id="b410d-112">[Diagnósticos de Azure](../cloud-services/cloud-services-dotnet-diagnostics.md) (relacionadas con la tooAzure servicios en la nube, pero tiene buena información y ejemplos)</span><span class="sxs-lookup"><span data-stu-id="b410d-112">[Azure Diagnostics](../cloud-services/cloud-services-dotnet-diagnostics.md) (related tooAzure Cloud Services but has good information and examples)</span></span>
* [<span data-ttu-id="b410d-113">Administrador de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="b410d-113">Azure Resource Manager</span></span>](../azure-resource-manager/resource-group-overview.md)
* [<span data-ttu-id="b410d-114">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="b410d-114">Azure PowerShell</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="b410d-115">Cliente de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b410d-115">Azure Resource Manager client</span></span>](https://github.com/projectkudu/ARMClient)
* [<span data-ttu-id="b410d-116">Plantilla de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b410d-116">Azure Resource Manager template</span></span>](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="log-and-event-sources"></a><span data-ttu-id="b410d-117">Orígenes de eventos y registros</span><span class="sxs-lookup"><span data-stu-id="b410d-117">Log and event sources</span></span>

### <a name="service-fabric-platform-events"></a><span data-ttu-id="b410d-118">Eventos de plataforma de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="b410d-118">Service Fabric platform events</span></span>
<span data-ttu-id="b410d-119">Como se describe en [este artículo](service-fabric-diagnostics-event-generation-infra.md), Service Fabric se configura la con algunos canales de registro remoto, del que Hola siguientes canales fácilmente se configuran con WAD toosend supervisión y diagnóstico tooa almacenamiento tabla de datos o en otros lugares:</span><span class="sxs-lookup"><span data-stu-id="b410d-119">As discussed in [this article](service-fabric-diagnostics-event-generation-infra.md), Service Fabric sets you up with a few out-of-the-box logging channels, of which hello following channels are easily configured with WAD toosend monitoring and diagnostics data tooa storage table or elsewhere:</span></span>
  * <span data-ttu-id="b410d-120">Los eventos operativos: operaciones de nivel superior que Hola Service Fabric realiza la plataforma.</span><span class="sxs-lookup"><span data-stu-id="b410d-120">Operational events: higher-level operations that hello Service Fabric platform performs.</span></span> <span data-ttu-id="b410d-121">Algunos ejemplos son la creación de aplicaciones y servicios, los cambios de estado de nodo y la información sobre la actualización.</span><span class="sxs-lookup"><span data-stu-id="b410d-121">Examples include creation of applications and services, node state changes, and upgrade information.</span></span> <span data-ttu-id="b410d-122">Se emiten como registros de Seguimiento de eventos para Windows (ETW).</span><span class="sxs-lookup"><span data-stu-id="b410d-122">These are emitted as Event Tracing for Windows (ETW) logs</span></span>
  * [<span data-ttu-id="b410d-123">Eventos del modelo de programación de Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="b410d-123">Reliable Actors programming model events</span></span>](service-fabric-reliable-actors-diagnostics.md)
  * [<span data-ttu-id="b410d-124">Eventos del modelo de programación de Reliable Services</span><span class="sxs-lookup"><span data-stu-id="b410d-124">Reliable Services programming model events</span></span>](service-fabric-reliable-services-diagnostics.md)

### <a name="application-events"></a><span data-ttu-id="b410d-125">Eventos de aplicación</span><span class="sxs-lookup"><span data-stu-id="b410d-125">Application events</span></span>
 <span data-ttu-id="b410d-126">Eventos emitidos desde las aplicaciones y servicios de código y que se escribe mediante el uso de la clase de aplicación auxiliar de hello EventSource en hello proporcionan plantillas de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b410d-126">Events emitted from your applications' and services' code and written out by using hello EventSource helper class provided in hello Visual Studio templates.</span></span> <span data-ttu-id="b410d-127">Para obtener más información sobre cómo se registra toowrite EventSource desde su aplicación, consulte [Monitor y diagnosticar los servicios en una configuración de desarrollo de equipo local](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span><span class="sxs-lookup"><span data-stu-id="b410d-127">For more information on how toowrite EventSource logs from your application, see [Monitor and diagnose services in a local machine development setup](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span></span>

## <a name="deploy-hello-diagnostics-extension"></a><span data-ttu-id="b410d-128">Implementar la extensión de diagnósticos de Hola</span><span class="sxs-lookup"><span data-stu-id="b410d-128">Deploy hello Diagnostics extension</span></span>
<span data-ttu-id="b410d-129">Hola primer paso en la recopilación de registros es toodeploy extensión de diagnósticos de hello en cada una de las máquinas virtuales de hello en clúster de Service Fabric Hola.</span><span class="sxs-lookup"><span data-stu-id="b410d-129">hello first step in collecting logs is toodeploy hello Diagnostics extension on each of hello VMs in hello Service Fabric cluster.</span></span> <span data-ttu-id="b410d-130">extensión de diagnósticos de Hello recopila registros en cada máquina virtual y los carga toohello cuenta de almacenamiento que especifique.</span><span class="sxs-lookup"><span data-stu-id="b410d-130">hello Diagnostics extension collects logs on each VM and uploads them toohello storage account that you specify.</span></span> <span data-ttu-id="b410d-131">pasos de Hello varían ligeramente en función de si utiliza Hola portal de Azure o Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b410d-131">hello steps vary a little based on whether you use hello Azure portal or Azure Resource Manager.</span></span> <span data-ttu-id="b410d-132">pasos de Hello también varían en función de si implementación hello es parte de la creación de clúster o de un clúster que ya existe.</span><span class="sxs-lookup"><span data-stu-id="b410d-132">hello steps also vary based on whether hello deployment is part of cluster creation or is for a cluster that already exists.</span></span> <span data-ttu-id="b410d-133">Echemos un vistazo a los pasos de Hola para cada escenario.</span><span class="sxs-lookup"><span data-stu-id="b410d-133">Let's look at hello steps for each scenario.</span></span>

### <a name="deploy-hello-diagnostics-extension-as-part-of-cluster-creation-through-azure-portal"></a><span data-ttu-id="b410d-134">Implementar la extensión de diagnósticos de hello como parte de la creación del clúster a través del portal de Azure</span><span class="sxs-lookup"><span data-stu-id="b410d-134">Deploy hello Diagnostics extension as part of cluster creation through Azure portal</span></span>
<span data-ttu-id="b410d-135">toodeploy Hola diagnósticos extensión toohello máquinas virtuales en clúster de hello como parte de la creación del clúster, usa panel de configuración de diagnósticos de Hola se muestra en el siguiente de saludo de la imagen: asegúrese de que los diagnósticos está establecido demasiado**en** (Hola la configuración predeterminada) .</span><span class="sxs-lookup"><span data-stu-id="b410d-135">toodeploy hello Diagnostics extension toohello VMs in hello cluster as part of cluster creation, you use hello Diagnostics settings panel shown in hello following image - ensure that Diagnostics is set too**On** (hello default setting).</span></span> <span data-ttu-id="b410d-136">Después de crear el clúster de hello, no se puede cambiar esta configuración mediante el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="b410d-136">After you create hello cluster, you can't change these settings by using hello portal.</span></span>

![Configuración de diagnóstico de Azure en el portal de hello para la creación de clúster](media/service-fabric-diagnostics-event-aggregation-wad/azure-enable-diagnostics.png)

<span data-ttu-id="b410d-138">Al crear un clúster mediante el portal de hello, recomendamos encarecidamente que descargue la plantilla de hello **antes de hacer clic en Aceptar** clúster de hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="b410d-138">When you're creating a cluster by using hello portal, we highly recommend that you download hello template **before you click OK** toocreate hello cluster.</span></span> <span data-ttu-id="b410d-139">Para obtener más información, consulte demasiado[configurar un clúster de Service Fabric mediante una plantilla de Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).</span><span class="sxs-lookup"><span data-stu-id="b410d-139">For details, refer too[Set up a Service Fabric cluster by using an Azure Resource Manager template](service-fabric-cluster-creation-via-arm.md).</span></span> <span data-ttu-id="b410d-140">Necesitará toomake cambios de la plantilla de hello más tarde, debido a que no puede realizar algunos cambios mediante el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="b410d-140">You'll need hello template toomake changes later, because you can't make some changes by using hello portal.</span></span>

### <a name="deploy-hello-diagnostics-extension-as-part-of-cluster-creation-by-using-azure-resource-manager"></a><span data-ttu-id="b410d-141">Implementar la extensión de diagnósticos de hello como parte de la creación del clúster mediante el Administrador de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="b410d-141">Deploy hello Diagnostics extension as part of cluster creation by using Azure Resource Manager</span></span>
<span data-ttu-id="b410d-142">toocreate un clúster mediante el Administrador de recursos, necesita hello tooadd diagnósticos JSON configuración toohello el Administrador de recursos completo del clúster plantilla antes de crear el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="b410d-142">toocreate a cluster by using Resource Manager, you need tooadd hello Diagnostics configuration JSON toohello full cluster Resource Manager template before you create hello cluster.</span></span> <span data-ttu-id="b410d-143">Proporcionamos una plantilla de administrador de recursos de clúster de cinco VM de ejemplo con la configuración de diagnóstico agrega tooit como parte de nuestros ejemplos de la plantilla de administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="b410d-143">We provide a sample five-VM cluster Resource Manager template with Diagnostics configuration added tooit as part of our Resource Manager template samples.</span></span> <span data-ttu-id="b410d-144">Puede ver en esta ubicación en la Galería de ejemplos de Azure hello: [clúster de cinco nodos con el ejemplo de la plantilla de administrador de recursos de diagnóstico](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype-wad).</span><span class="sxs-lookup"><span data-stu-id="b410d-144">You can see it at this location in hello Azure Samples gallery: [Five-node cluster with Diagnostics Resource Manager template sample](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype-wad).</span></span>

<span data-ttu-id="b410d-145">configuración de diagnósticos de hello toosee en plantilla de administrador de recursos de hello, archivo de azuredeploy.json de hello abierto y busque **IaaSDiagnostics**.</span><span class="sxs-lookup"><span data-stu-id="b410d-145">toosee hello Diagnostics setting in hello Resource Manager template, open hello azuredeploy.json file and search for **IaaSDiagnostics**.</span></span> <span data-ttu-id="b410d-146">un clúster con esta plantilla, seleccione hello toocreate **implementar tooAzure** botón está disponible en el vínculo anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="b410d-146">toocreate a cluster by using this template, select hello **Deploy tooAzure** button available at hello previous link.</span></span>

<span data-ttu-id="b410d-147">Como alternativa, puede descargar el ejemplo de Hola a Administrador de recursos, realizar cambios tooit y crear un clúster con la plantilla modificada hello mediante Hola `New-AzureRmResourceGroupDeployment` comando en una ventana de PowerShell de Azure.</span><span class="sxs-lookup"><span data-stu-id="b410d-147">Alternatively, you can download hello Resource Manager sample, make changes tooit, and create a cluster with hello modified template by using hello `New-AzureRmResourceGroupDeployment` command in an Azure PowerShell window.</span></span> <span data-ttu-id="b410d-148">Vea Hola siguiente código para los parámetros de Hola que se pasan en el comando toohello.</span><span class="sxs-lookup"><span data-stu-id="b410d-148">See hello following code for hello parameters that you pass in toohello command.</span></span> <span data-ttu-id="b410d-149">Para obtener información detallada sobre cómo toodeploy un recurso de grupo mediante el uso de PowerShell, vea el artículo de hello [implementar un grupo de recursos con la plantilla de Azure Resource Manager hello](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="b410d-149">For detailed information on how toodeploy a resource group by using PowerShell, see hello article [Deploy a resource group with hello Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md).</span></span>

### <a name="deploy-hello-diagnostics-extension-tooan-existing-cluster"></a><span data-ttu-id="b410d-150">Implementar el clúster existente de hello diagnósticos extensión tooan</span><span class="sxs-lookup"><span data-stu-id="b410d-150">Deploy hello Diagnostics extension tooan existing cluster</span></span>
<span data-ttu-id="b410d-151">Si tiene un clúster existente que no tiene implementado de diagnóstico, o si desea toomodify una configuración existente, puede agregar o actualizar.</span><span class="sxs-lookup"><span data-stu-id="b410d-151">If you have an existing cluster that doesn't have Diagnostics deployed, or if you want toomodify an existing configuration, you can add or update it.</span></span> <span data-ttu-id="b410d-152">Modificar plantilla de administrador de recursos de Hola que es usado toocreate Hola existente clúster o descargar plantilla de Hola desde el portal de hello, tal como se describió anteriormente.</span><span class="sxs-lookup"><span data-stu-id="b410d-152">Modify hello Resource Manager template that's used toocreate hello existing cluster or download hello template from hello portal as described earlier.</span></span> <span data-ttu-id="b410d-153">Modificar el archivo de template.json de hello realizando Hola siguiente las tareas.</span><span class="sxs-lookup"><span data-stu-id="b410d-153">Modify hello template.json file by performing hello following tasks.</span></span>

<span data-ttu-id="b410d-154">Agregar una nueva plantilla de toohello de recursos de almacenamiento mediante la adición de la sección de recursos toohello.</span><span class="sxs-lookup"><span data-stu-id="b410d-154">Add a new storage resource toohello template by adding toohello resources section.</span></span>

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

 <span data-ttu-id="b410d-155">A continuación, agregue parámetros toohello sección justo después de las definiciones de la cuenta de almacenamiento de hello, entre `supportLogStorageAccountName` y `vmNodeType0Name`.</span><span class="sxs-lookup"><span data-stu-id="b410d-155">Next, add toohello parameters section just after hello storage account definitions, between `supportLogStorageAccountName` and `vmNodeType0Name`.</span></span> <span data-ttu-id="b410d-156">Reemplace el texto de marcador de posición de hello *aquí el nombre de cuenta de almacenamiento* con el nombre de Hola de cuenta de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="b410d-156">Replace hello placeholder text *storage account name goes here* with hello name of hello storage account.</span></span>

```json
    "applicationDiagnosticsStorageAccountType": {
      "type": "string",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS"
      ],
      "defaultValue": "Standard_LRS",
      "metadata": {
        "description": "Replication option for hello application diagnostics storage account"
      }
    },
    "applicationDiagnosticsStorageAccountName": {
      "type": "string",
      "defaultValue": "storage account name goes here",
      "metadata": {
        "description": "Name for hello storage account that contains application diagnostics data from hello cluster"
      }
    },
```
<span data-ttu-id="b410d-157">A continuación, actualice hello `VirtualMachineProfile` sección del archivo de template.json Hola agregando Hola siguiente código dentro de la matriz de extensiones de Hola.</span><span class="sxs-lookup"><span data-stu-id="b410d-157">Then, update hello `VirtualMachineProfile` section of hello template.json file by adding hello following code within hello extensions array.</span></span> <span data-ttu-id="b410d-158">Ser seguro tooadd una coma al principio de Hola o al final de hello, según donde se inserta.</span><span class="sxs-lookup"><span data-stu-id="b410d-158">Be sure tooadd a comma at hello beginning or hello end, depending on where it's inserted.</span></span>

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

<span data-ttu-id="b410d-159">Después de modificar el archivo de hello template.json tal como se describe, volver a publicar la plantilla de administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="b410d-159">After you modify hello template.json file as described, republish hello Resource Manager template.</span></span> <span data-ttu-id="b410d-160">Si se ha exportado la plantilla de hello, archivo de ejecución hello deploy.ps1 vuelve a publicar plantilla Hola.</span><span class="sxs-lookup"><span data-stu-id="b410d-160">If hello template was exported, running hello deploy.ps1 file republishes hello template.</span></span> <span data-ttu-id="b410d-161">Después de realizar la implementación, asegúrese de que el estado **ProvisioningState** sea **Correcto**.</span><span class="sxs-lookup"><span data-stu-id="b410d-161">After you deploy, ensure that **ProvisioningState** is **Succeeded**.</span></span>

## <a name="collect-health-and-load-events"></a><span data-ttu-id="b410d-162">Recopilar eventos de mantenimiento y carga</span><span class="sxs-lookup"><span data-stu-id="b410d-162">Collect health and load events</span></span>

<span data-ttu-id="b410d-163">A partir de hello 5.4 versión de Service Fabric, eventos de métrica de mantenimiento y carga están disponibles para la colección.</span><span class="sxs-lookup"><span data-stu-id="b410d-163">Starting with hello 5.4 release of Service Fabric, health and load metric events are available for collection.</span></span> <span data-ttu-id="b410d-164">Estos eventos reflejan los eventos generados por el sistema de hello o tu código mediante el uso de mantenimiento de Hola o cargue las API de generación de informes como [ReportPartitionHealth](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportpartitionhealth.aspx) o [ReportLoad](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportload.aspx).</span><span class="sxs-lookup"><span data-stu-id="b410d-164">These events reflect events generated by hello system or your code by using hello health or load reporting APIs such as [ReportPartitionHealth](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportpartitionhealth.aspx) or [ReportLoad](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportload.aspx).</span></span> <span data-ttu-id="b410d-165">Esto permite agregar y ver el estado de mantenimiento del sistema en el tiempo, y generar alertas basadas en eventos de estado de mantenimiento o carga.</span><span class="sxs-lookup"><span data-stu-id="b410d-165">This allows for aggregating and viewing system health over time and for alerting based on health or load events.</span></span> <span data-ttu-id="b410d-166">tooview agregan estos eventos en el Visor de eventos de diagnóstico de Visual Studio "Microsoft-ServiceFabric:4:0x4000000000000008" toohello lista de proveedores de ETW.</span><span class="sxs-lookup"><span data-stu-id="b410d-166">tooview these events in Visual Studio's Diagnostic Event Viewer add "Microsoft-ServiceFabric:4:0x4000000000000008" toohello list of ETW providers.</span></span>

<span data-ttu-id="b410d-167">eventos de hello toocollect, modificar tooinclude de plantilla del Administrador de recursos de Hola</span><span class="sxs-lookup"><span data-stu-id="b410d-167">toocollect hello events, modify hello Resource Manager template tooinclude</span></span>

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

## <a name="collect-reverse-proxy-events"></a><span data-ttu-id="b410d-168">Recopilación de eventos de proxy inverso</span><span class="sxs-lookup"><span data-stu-id="b410d-168">Collect reverse proxy events</span></span>

<span data-ttu-id="b410d-169">A partir de hello 5.7 versión de Service Fabric, [proxy inverso](service-fabric-reverseproxy.md) eventos están disponibles para la colección.</span><span class="sxs-lookup"><span data-stu-id="b410d-169">Starting with hello 5.7 release of Service Fabric, [reverse proxy](service-fabric-reverseproxy.md) events are available for collection.</span></span>
<span data-ttu-id="b410d-170">Proxy inverso emite eventos en dos canales, un error que contiene eventos reflejar errores de procesamiento de solicitud y otros uno que contiene eventos detallados de todas las solicitudes de hello procesadas en el proxy inverso Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="b410d-170">Reverse proxy emits events into two channels, one containing error events reflecting request processing failures and hello other one containing verbose events about all hello requests processed at hello reverse proxy.</span></span> 

1. <span data-ttu-id="b410d-171">Recopilar eventos de error: tooview agregan estos eventos en el Visor de eventos de diagnóstico de Visual Studio "Microsoft-ServiceFabric:4:0x4000000000000010" toohello lista de proveedores de ETW.</span><span class="sxs-lookup"><span data-stu-id="b410d-171">Collect error events: tooview these events in Visual Studio's Diagnostic Event Viewer add "Microsoft-ServiceFabric:4:0x4000000000000010" toohello list of ETW providers.</span></span>
<span data-ttu-id="b410d-172">eventos de hello toocollect de clústeres de Azure, modifique tooinclude de plantilla del Administrador de recursos de Hola</span><span class="sxs-lookup"><span data-stu-id="b410d-172">toocollect hello events from Azure clusters, modify hello Resource Manager template tooinclude</span></span>

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

2. <span data-ttu-id="b410d-173">Recopilar todos los eventos de procesamiento de solicitud: Visor de eventos de diagnóstico de en Visual Studio, en la entrada de hello Microsoft ServiceFabric actualización Hola lista de proveedores ETW demasiado "Microsoft-ServiceFabric:4:0x4000000000000020".</span><span class="sxs-lookup"><span data-stu-id="b410d-173">Collect all request processing events: In Visual Studio's Diagnostic Event Viewer, update hello Microsoft-ServiceFabric entry in hello ETW provider list too"Microsoft-ServiceFabric:4:0x4000000000000020".</span></span>
<span data-ttu-id="b410d-174">Para los clústeres de Azure Service Fabric, modificar tooinclude de plantilla de administrador de recursos de Hola</span><span class="sxs-lookup"><span data-stu-id="b410d-174">For Azure Service Fabric clusters, modify hello resource manager template tooinclude</span></span>

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
> <span data-ttu-id="b410d-175">Se recomienda toojudiciously habilitar recopilación de eventos de este canal ya que recopila todo el tráfico a través de proxy inverso de Hola y puede consumir rápidamente la capacidad de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="b410d-175">It is recommended toojudiciously enable collecting events from this channel as this collects all traffic through hello reverse proxy and can quickly consume storage capacity.</span></span>

<span data-ttu-id="b410d-176">Para los clústeres de Azure Service Fabric, eventos de Hola desde todos los nodos de Hola se recopilan y agregan en hello SystemEventTable.</span><span class="sxs-lookup"><span data-stu-id="b410d-176">For Azure Service Fabric clusters, hello events from all hello nodes are collected and aggregated in hello SystemEventTable.</span></span>
<span data-ttu-id="b410d-177">Para obtener la solución de problemas de eventos de proxy inverso de hello, consulte hello [Guía de diagnóstico de proxy inverso](service-fabric-reverse-proxy-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="b410d-177">For detailed troubleshooting of hello reverse proxy events, refer hello [reverse proxy diagnostics guide](service-fabric-reverse-proxy-diagnostics.md).</span></span>

## <a name="collect-from-new-eventsource-channels"></a><span data-ttu-id="b410d-178">Recopilar desde canales EventSource nuevos</span><span class="sxs-lookup"><span data-stu-id="b410d-178">Collect from new EventSource channels</span></span>

<span data-ttu-id="b410d-179">registros de toocollect tooupdate diagnósticos de nuevos canales EventSource que representan una nueva aplicación que le sobre toodeploy, realizar Hola mismos pasos descritos anteriormente para la instalación de Hola de diagnósticos para un clúster existente.</span><span class="sxs-lookup"><span data-stu-id="b410d-179">tooupdate Diagnostics toocollect logs from new EventSource channels that represent a new application that you're about toodeploy, perform hello same steps as previously described for hello setup of Diagnostics for an existing cluster.</span></span>

<span data-ttu-id="b410d-180">Actualizar hello `EtwEventSourceProviderConfiguration` sección entradas del archivo de hello template.json tooadd para actualización con Hola Hola EventSource canales nuevos antes de aplicar la configuración de hello `New-AzureRmResourceGroupDeployment` comando de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b410d-180">Update hello `EtwEventSourceProviderConfiguration` section in hello template.json file tooadd entries for hello new EventSource channels before you apply hello configuration update by using hello `New-AzureRmResourceGroupDeployment` PowerShell command.</span></span> <span data-ttu-id="b410d-181">nombre de Hola Hola del origen de evento se define como parte de su código en un archivo generado por Visual Studio ServiceEventSource.cs Hola.</span><span class="sxs-lookup"><span data-stu-id="b410d-181">hello name of hello event source is defined as part of your code in hello Visual Studio-generated ServiceEventSource.cs file.</span></span>

<span data-ttu-id="b410d-182">Por ejemplo, si el origen de eventos se denomina Mis Eventsource, agregar Hola siguientes eventos de código tooplace Hola de mi Eventsource en una tabla denominada MyDestinationTableName.</span><span class="sxs-lookup"><span data-stu-id="b410d-182">For example, if your event source is named My-Eventsource, add hello following code tooplace hello events from My-Eventsource into a table named MyDestinationTableName.</span></span>

```json
        {
            "provider": "My-Eventsource",
            "scheduledTransferPeriod": "PT5M",
            "DefaultEvents": {
            "eventDestination": "MyDestinationTableName"
            }
        }
```

<span data-ttu-id="b410d-183">contadores de rendimiento de toocollect o registros de eventos, modificar plantilla de administrador de recursos de hello mediante ejemplos de hello en [crear una máquina virtual de Windows con la supervisión y el diagnóstico mediante una plantilla de Azure Resource Manager](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b410d-183">toocollect performance counters or event logs, modify hello Resource Manager template by using hello examples provided in [Create a Windows virtual machine with monitoring and diagnostics by using an Azure Resource Manager template](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="b410d-184">A continuación, volver a publicar plantilla del Administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="b410d-184">Then, republish hello Resource Manager template.</span></span>

## <a name="collect-performance-counters"></a><span data-ttu-id="b410d-185">Recopilar contadores de rendimiento</span><span class="sxs-lookup"><span data-stu-id="b410d-185">Collect Performance Counters</span></span>

<span data-ttu-id="b410d-186">las métricas de rendimiento de toocollect desde el clúster, agregue tooyour de contadores de rendimiento de Hola "WadCfg > DiagnosticMonitorConfiguration" en la plantilla de administrador de recursos de hello para el clúster.</span><span class="sxs-lookup"><span data-stu-id="b410d-186">toocollect performance metrics from your cluster, add hello performance counters tooyour "WadCfg > DiagnosticMonitorConfiguration" in hello Resource Manager template for your cluster.</span></span> <span data-ttu-id="b410d-187">Vea en [Service Fabric Performance Counters](service-fabric-diagnostics-event-generation-perf.md) (Contadores de rendimiento de Service Fabric) los contadores de rendimiento que se recomienda recopilar.</span><span class="sxs-lookup"><span data-stu-id="b410d-187">See [Service Fabric Performance Counters](service-fabric-diagnostics-event-generation-perf.md) for performance counters that we recommend collecting.</span></span>

<span data-ttu-id="b410d-188">Por ejemplo, aquí se establezca un contador de rendimiento, muestreado cada 15 segundos (Esto se puede cambiar y se indica a continuación Hola formato de "PT\<tiempo >\<unidad >", por ejemplo, PT3M se muestra en intervalos de tres minutos) y transfieren toohello tabla de almacenamiento adecuado cada minuto.</span><span class="sxs-lookup"><span data-stu-id="b410d-188">For example, here we set one performance counter, sampled every 15 seconds (this can be changed and follows hello format of "PT\<time>\<unit>", for example, PT3M would sample at three minute intervals), and transferred toohello appropriate storage table every one minute.</span></span>

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
  
<span data-ttu-id="b410d-189">Si si está usando un receptor de Application Insights, tal y como se describe en la siguiente sección de Hola y desea que estas métricas tooshow seguridad en Application Insights, asegúrese de nombre de receptor de hello tooadd seguro en hello "receptores" sección como se indicó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="b410d-189">If you are using an Application Insights sink, as described in hello section below, and want these metrics tooshow up in Application Insights, then make sure tooadd hello sink name in hello "sinks" section as shown above.</span></span> <span data-ttu-id="b410d-190">Además, considere la posibilidad de crear una tabla independiente toosend los contadores de rendimiento, por lo que no sobrecargue out Hola Hola de datos procedentes de otros canales de registro que se ha habilitado.</span><span class="sxs-lookup"><span data-stu-id="b410d-190">Additionally, consider creating a separate table toosend your Performance Counters to, so they don't crowd out hello data coming from hello other logging channels you have enabled.</span></span>


## <a name="send-logs-tooapplication-insights"></a><span data-ttu-id="b410d-191">Enviar registros de visión tooApplication</span><span class="sxs-lookup"><span data-stu-id="b410d-191">Send logs tooApplication Insights</span></span>

<span data-ttu-id="b410d-192">Enviar tooApplication de datos de supervisión y diagnóstico de visión (AI) puede realizarse como parte de la configuración de WAD Hola.</span><span class="sxs-lookup"><span data-stu-id="b410d-192">Sending monitoring and diagnostics data tooApplication Insights (AI) can be done as part of hello WAD configuration.</span></span> <span data-ttu-id="b410d-193">Si decide toouse AI para visualización y análisis de eventos, leer [análisis de eventos y la visualización con Application Insights](service-fabric-diagnostics-event-analysis-appinsights.md) tooset seguridad un receptor de AI como parte de la "WadCfg".</span><span class="sxs-lookup"><span data-stu-id="b410d-193">If you decide toouse AI for event analysis and visualization, read [Event Analysis and Visualization with Application Insights](service-fabric-diagnostics-event-analysis-appinsights.md) tooset up an AI Sink as part of your "WadCfg".</span></span>

## <a name="next-steps"></a><span data-ttu-id="b410d-194">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b410d-194">Next steps</span></span>

<span data-ttu-id="b410d-195">Una vez que ha configurado correctamente los diagnósticos de Azure, verá los datos de las tablas de almacenamiento de registros de EventSource y Hola ETW.</span><span class="sxs-lookup"><span data-stu-id="b410d-195">Once you have correctly configured Azure diagnostics, you will see data in your Storage tables from hello ETW and EventSource logs.</span></span> <span data-ttu-id="b410d-196">Si elige toouse OMS, Kibana o cualquier otro análisis y visualización de plataforma de datos que no esté configurado directamente en la plantilla de administrador de recursos de hello, asegúrese de tooset seguro de la plataforma de Hola de su elección tooread en los datos de Hola de estas tablas de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="b410d-196">If you choose toouse OMS, Kibana, or any other data analytics and visualization platform that is not directly configured in hello Resource Manager template, make sure tooset up hello platform of your choice tooread in hello data from these storage tables.</span></span> <span data-ttu-id="b410d-197">Es relativamente fácil hacerlo para OMS, como se explica en [Event and log analysis through OMS](service-fabric-diagnostics-event-analysis-oms.md) (Análisis de eventos y registro mediante OMS).</span><span class="sxs-lookup"><span data-stu-id="b410d-197">Doing this for OMS is relatively trivial, and is explained in [Event and log analysis through OMS](service-fabric-diagnostics-event-analysis-oms.md).</span></span> <span data-ttu-id="b410d-198">Application Insights es un poco de un caso especial en este sentido, ya que puede configurarse como parte de la configuración de extensión de diagnósticos de hello, así que haga referencia toohello [artículo apropiado](service-fabric-diagnostics-event-analysis-appinsights.md) si elige toouse AI.</span><span class="sxs-lookup"><span data-stu-id="b410d-198">Application Insights is a bit of a special case in this sense, since it can be configured as part of hello Diagnostics extension configuration, so refer toohello [appropriate article](service-fabric-diagnostics-event-analysis-appinsights.md) if you choose toouse AI.</span></span>

>[!NOTE]
><span data-ttu-id="b410d-199">Actualmente no hay ningún evento de Hola de toofilter o limpiar de forma que se envía toohello tabla.</span><span class="sxs-lookup"><span data-stu-id="b410d-199">There is currently no way toofilter or groom hello events that are sent toohello table.</span></span> <span data-ttu-id="b410d-200">Si no implementan un tooremove procesar los eventos de tabla de hello, tabla de hello seguirá toogrow.</span><span class="sxs-lookup"><span data-stu-id="b410d-200">If you don't implement a process tooremove events from hello table, hello table will continue toogrow.</span></span> <span data-ttu-id="b410d-201">Actualmente, hay un ejemplo de un servicio de limpieza de datos ejecuta en hello [ejemplo guardián](https://github.com/Azure-Samples/service-fabric-watchdog-service), y se recomienda escribir uno para sí mismo, a menos que haya una buena razón para que los registros de toostore más allá de un plazo de 30 o 90 días.</span><span class="sxs-lookup"><span data-stu-id="b410d-201">Currently, there is an example of a data grooming service running in hello [Watchdog sample](https://github.com/Azure-Samples/service-fabric-watchdog-service), and it is recommended that you write one for yourself as well, unless there is a good reason for you toostore logs beyond a 30 or 90 day timeframe.</span></span>

* [<span data-ttu-id="b410d-202">Obtenga información acerca de cómo toocollect los contadores de rendimiento o de registros mediante el uso de Hola extensión de diagnósticos</span><span class="sxs-lookup"><span data-stu-id="b410d-202">Learn how toocollect performance counters or logs by using hello Diagnostics extension</span></span>](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="b410d-203">Análisis y visualización de eventos con Application Insights</span><span class="sxs-lookup"><span data-stu-id="b410d-203">Event Analysis and Visualization with Application Insights</span></span>](service-fabric-diagnostics-event-analysis-appinsights.md)
* [<span data-ttu-id="b410d-204">Análisis y visualización de eventos con OMS</span><span class="sxs-lookup"><span data-stu-id="b410d-204">Event Analysis and Visualization with OMS</span></span>](service-fabric-diagnostics-event-analysis-oms.md)