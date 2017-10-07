---
title: "aplicación de orquestación de revisión de Service Fabric aaaAzure | Documentos de Microsoft"
description: "Aplicación tooautomate de funcionamiento de la aplicación de revisiones de sistema en un clúster de Service Fabric."
services: service-fabric
documentationcenter: .net
author: novino
manager: timlt
editor: 
ms.assetid: de7dacf5-4038-434a-a265-5d0de80a9b1d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 5/9/2017
ms.author: nachandr
ms.openlocfilehash: fbb89aa2ea418181ee908a01850178c113c462fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="patch-hello-windows-operating-system-in-your-service-fabric-cluster"></a><span data-ttu-id="6e20d-103">Hola revisión sistema operativo Windows en el clúster de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="6e20d-103">Patch hello Windows operating system in your Service Fabric cluster</span></span>

<span data-ttu-id="6e20d-104">aplicación de orquestación de revisión de Hello es una aplicación de Azure Service Fabric que automatiza la aplicación de revisiones en un clúster de Service Fabric en Azure sin tiempo de inactividad de sistema de operativo.</span><span class="sxs-lookup"><span data-stu-id="6e20d-104">hello patch orchestration application is an Azure Service Fabric application that automates operating system patching on a Service Fabric cluster on Azure without downtime.</span></span>

<span data-ttu-id="6e20d-105">aplicación de orquestación de revisión de Hello proporciona siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="6e20d-105">hello patch orchestration app provides hello following:</span></span>

- <span data-ttu-id="6e20d-106">**Instalación automática de actualizaciones de sistema operativo**.</span><span class="sxs-lookup"><span data-stu-id="6e20d-106">**Automatic operating system update installation**.</span></span> <span data-ttu-id="6e20d-107">Las actualizaciones de sistema operativo se descargan e instalan automáticamente.</span><span class="sxs-lookup"><span data-stu-id="6e20d-107">Operating system updates are automatically downloaded and installed.</span></span> <span data-ttu-id="6e20d-108">Los nodos de clúster se reinician según sea necesario sin tiempo de inactividad del clúster.</span><span class="sxs-lookup"><span data-stu-id="6e20d-108">Cluster nodes are rebooted as needed without cluster downtime.</span></span>

- <span data-ttu-id="6e20d-109">**Integración de la aplicación de revisiones y el estado del clúster**.</span><span class="sxs-lookup"><span data-stu-id="6e20d-109">**Cluster-aware patching and health integration**.</span></span> <span data-ttu-id="6e20d-110">Al aplicar las actualizaciones, aplicación de orquestación de revisión de hello supervisa el estado de Hola Hola de nodos de clúster.</span><span class="sxs-lookup"><span data-stu-id="6e20d-110">While applying updates, hello patch orchestration app monitors hello health of hello cluster nodes.</span></span> <span data-ttu-id="6e20d-111">Los nodos de clúster se actualizan de uno en uno o por dominio de actualización.</span><span class="sxs-lookup"><span data-stu-id="6e20d-111">Cluster nodes are upgraded one node at a time or one upgrade domain at a time.</span></span> <span data-ttu-id="6e20d-112">Si estado Hola de clúster de hello deja de funcionar debido proceso de revisión de toohello, aplicación de revisiones es detenido tooprevent agravar el problema de Hola.</span><span class="sxs-lookup"><span data-stu-id="6e20d-112">If hello health of hello cluster goes down due toohello patching process, patching is stopped tooprevent aggravating hello problem.</span></span>

## <a name="internal-details-of-hello-app"></a><span data-ttu-id="6e20d-113">Detalles internos de la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="6e20d-113">Internal details of hello app</span></span>

<span data-ttu-id="6e20d-114">aplicación de orquestación de revisión de Hello se compone de hello siguientes subcomponentes:</span><span class="sxs-lookup"><span data-stu-id="6e20d-114">hello patch orchestration app is composed of hello following subcomponents:</span></span>

- <span data-ttu-id="6e20d-115">**Coordinator Service**: este servicio con estado es responsable de:</span><span class="sxs-lookup"><span data-stu-id="6e20d-115">**Coordinator Service**: This stateful service is responsible for:</span></span>
    - <span data-ttu-id="6e20d-116">Coordinar el trabajo de actualización de Windows de hello en clúster completo Hola.</span><span class="sxs-lookup"><span data-stu-id="6e20d-116">Coordinating hello Windows Update job on hello entire cluster.</span></span>
    - <span data-ttu-id="6e20d-117">Almacenando el resultado de hello operaciones completadas que Windows Update.</span><span class="sxs-lookup"><span data-stu-id="6e20d-117">Storing hello result of completed Windows Update operations.</span></span>
- <span data-ttu-id="6e20d-118">**Node Agent Service**: es un servicio sin estado que se ejecuta en todos los nodos del clúster de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="6e20d-118">**Node Agent Service**: This stateless service runs on all Service Fabric cluster nodes.</span></span> <span data-ttu-id="6e20d-119">servicio de Hello es responsable de:</span><span class="sxs-lookup"><span data-stu-id="6e20d-119">hello service is responsible for:</span></span>
    - <span data-ttu-id="6e20d-120">Arranque Hola servicio NT de agente de nodo.</span><span class="sxs-lookup"><span data-stu-id="6e20d-120">Bootstrapping hello Node Agent NTService.</span></span>
    - <span data-ttu-id="6e20d-121">Hola servicio NT de agente de nodo de supervisión.</span><span class="sxs-lookup"><span data-stu-id="6e20d-121">Monitoring hello Node Agent NTService.</span></span>
- <span data-ttu-id="6e20d-122">**Node Agent NTService**: este servicio de Windows NT se ejecuta con privilegios elevados (SYSTEM).</span><span class="sxs-lookup"><span data-stu-id="6e20d-122">**Node Agent NTService**: This Windows NT service runs at a higher-level privilege (SYSTEM).</span></span> <span data-ttu-id="6e20d-123">En cambio, Hola nodo servicio de agente y Hola servicio Coordinador de ejecutan en un privilegio de nivel inferior (servicio de red).</span><span class="sxs-lookup"><span data-stu-id="6e20d-123">In contrast, hello Node Agent Service and hello Coordinator Service run at a lower-level privilege (NETWORK SERVICE).</span></span> <span data-ttu-id="6e20d-124">servicio de Hello es responsable de realizar Hola después de trabajos de Windows Update en todos los nodos de clúster de hello:</span><span class="sxs-lookup"><span data-stu-id="6e20d-124">hello service is responsible for performing hello following Windows Update jobs on all hello cluster nodes:</span></span>
    - <span data-ttu-id="6e20d-125">Deshabilitar las actualizaciones automáticas de Windows en el nodo de Hola.</span><span class="sxs-lookup"><span data-stu-id="6e20d-125">Disabling automatic Windows Update on hello node.</span></span>
    - <span data-ttu-id="6e20d-126">Descarga e instalación de Windows Update según usuario Hola de toohello directiva ha proporcionado.</span><span class="sxs-lookup"><span data-stu-id="6e20d-126">Downloading and installing Windows Update according toohello policy hello user has provided.</span></span>
    - <span data-ttu-id="6e20d-127">Reiniciar post de máquina de hello instalación de Windows Update.</span><span class="sxs-lookup"><span data-stu-id="6e20d-127">Restarting hello machine post Windows Update installation.</span></span>
    - <span data-ttu-id="6e20d-128">Cargar resultados de Hola de toohello de las actualizaciones de Windows servicio de coordinador.</span><span class="sxs-lookup"><span data-stu-id="6e20d-128">Uploading hello results of Windows updates toohello Coordinator Service.</span></span>
    - <span data-ttu-id="6e20d-129">Realizar un informe de estado en caso de error en la operación después de agotar todos los reintentos.</span><span class="sxs-lookup"><span data-stu-id="6e20d-129">Reporting health reports in case an operation has failed after exhausting all retries.</span></span>

> [!NOTE]
> <span data-ttu-id="6e20d-130">Hola revisión orquestación aplicación usa Hola Service Fabric reparar toodisable de servicio de sistema de administrador o permitir que el nodo de Hola y realiza comprobaciones de estado.</span><span class="sxs-lookup"><span data-stu-id="6e20d-130">hello patch orchestration app uses hello Service Fabric repair manager system service toodisable or enable hello node and perform health checks.</span></span> <span data-ttu-id="6e20d-131">tarea de reparación de Hello creada por Hola revisión orquestación aplicación pistas Hola progreso de la actualización de Windows para cada nodo.</span><span class="sxs-lookup"><span data-stu-id="6e20d-131">hello repair task created by hello patch orchestration app tracks hello Windows Update progress for each node.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6e20d-132">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="6e20d-132">Prerequisites</span></span>

### <a name="minimum-supported-service-fabric-runtime-version"></a><span data-ttu-id="6e20d-133">Versión mínima admitida del runtime de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="6e20d-133">Minimum supported Service Fabric runtime version</span></span>

#### <a name="azure-clusters"></a><span data-ttu-id="6e20d-134">Clústeres de Azure</span><span class="sxs-lookup"><span data-stu-id="6e20d-134">Azure clusters</span></span>
<span data-ttu-id="6e20d-135">se debe ejecutar la aplicación de orquestación de revisión de Hello en Azure clústeres que tienen v5.5 de versión de Service Fabric en tiempo de ejecución o una versión posterior.</span><span class="sxs-lookup"><span data-stu-id="6e20d-135">hello patch orchestration app must be run on Azure clusters that have Service Fabric runtime version v5.5 or later.</span></span>

#### <a name="standalone-on-premises-clusters"></a><span data-ttu-id="6e20d-136">Clústeres locales independientes</span><span class="sxs-lookup"><span data-stu-id="6e20d-136">Standalone on-premises Clusters</span></span>
<span data-ttu-id="6e20d-137">se debe ejecutar la aplicación de orquestación de revisión de Hello en clústeres independientes que tengan v5.6 de versión de Service Fabric en tiempo de ejecución o una versión posterior.</span><span class="sxs-lookup"><span data-stu-id="6e20d-137">hello patch orchestration app must be run on Standalone clusters that have Service Fabric runtime version v5.6 or later.</span></span>

### <a name="enable-hello-repair-manager-service-if-its-not-running-already"></a><span data-ttu-id="6e20d-138">Habilitar el servicio de administrador de reparación de hello (si ya no se está ejecutando)</span><span class="sxs-lookup"><span data-stu-id="6e20d-138">Enable hello repair manager service (if it's not running already)</span></span>

<span data-ttu-id="6e20d-139">aplicación de orquestación de revisión de Hello requiere Hola reparación manager system service toobe habilitado en el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="6e20d-139">hello patch orchestration app requires hello repair manager system service toobe enabled on hello cluster.</span></span>

#### <a name="azure-clusters"></a><span data-ttu-id="6e20d-140">Clústeres de Azure</span><span class="sxs-lookup"><span data-stu-id="6e20d-140">Azure clusters</span></span>

<span data-ttu-id="6e20d-141">Clústeres de Azure en el nivel de durabilidad plata Hola tienen Hola reparar servicio manager habilitada de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="6e20d-141">Azure clusters in hello silver durability tier have hello repair manager service enabled by default.</span></span> <span data-ttu-id="6e20d-142">Clústeres de Azure en el nivel de durabilidad gold Hola que no tenga o servicio de administrador de reparación de hello habilitado, dependiendo de cuándo se crearon esos clústeres.</span><span class="sxs-lookup"><span data-stu-id="6e20d-142">Azure clusters in hello gold durability tier might or might not have hello repair manager service enabled, depending on when those clusters were created.</span></span> <span data-ttu-id="6e20d-143">Clústeres de Azure en el nivel de durabilidad bronce hello, de forma predeterminada, no es necesario Hola reparar habilitado el servicio de administrador.</span><span class="sxs-lookup"><span data-stu-id="6e20d-143">Azure clusters in hello bronze durability tier, by default, do not have hello repair manager service enabled.</span></span> <span data-ttu-id="6e20d-144">Si ya está habilitado el servicio de hello, puede ver que se ejecuta en la sección de servicios de sistema de Hola Hola Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="6e20d-144">If hello service is already enabled, you can see it running in hello system services section in hello Service Fabric Explorer.</span></span>

##### <a name="azure-portal"></a><span data-ttu-id="6e20d-145">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="6e20d-145">Azure portal</span></span>
<span data-ttu-id="6e20d-146">Puede habilitar el Administrador de reparación de portal de Azure en tiempo de Hola de configuración de clúster.</span><span class="sxs-lookup"><span data-stu-id="6e20d-146">You can enable repair manager from Azure portal at hello time of setting up of cluster.</span></span> <span data-ttu-id="6e20d-147">Seleccione `Include Repair Manager` opción `Add on features` en tiempo de Hola de configuración del clúster.</span><span class="sxs-lookup"><span data-stu-id="6e20d-147">Select `Include Repair Manager` option under `Add on features` at hello time of Cluster configuration.</span></span>
<span data-ttu-id="6e20d-148">![Imagen de la habilitación del administrador de reparaciones de Azure Portal](media/service-fabric-patch-orchestration-application/EnableRepairManager.png)</span><span class="sxs-lookup"><span data-stu-id="6e20d-148">![Image of Enabling Repair Manager from Azure portal](media/service-fabric-patch-orchestration-application/EnableRepairManager.png)</span></span>

##### <a name="azure-resource-manager-template"></a><span data-ttu-id="6e20d-149">Plantilla del Administrador de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="6e20d-149">Azure Resource Manager template</span></span>
<span data-ttu-id="6e20d-150">O bien puede usar hello [plantilla de Azure Resource Manager](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm) tooenable servicio de administrador de reparación de hello en clústeres de Service Fabric existentes y nuevos.</span><span class="sxs-lookup"><span data-stu-id="6e20d-150">Alternatively you can use hello [Azure Resource Manager template](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm) tooenable hello repair manager service on new and existing Service Fabric clusters.</span></span> <span data-ttu-id="6e20d-151">Obtener plantilla hello para el clúster de Hola que desea toodeploy.</span><span class="sxs-lookup"><span data-stu-id="6e20d-151">Get hello template for hello cluster that you want toodeploy.</span></span> <span data-ttu-id="6e20d-152">Puede usar plantillas de ejemplo de Hola o crear una plantilla personalizada que el Administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="6e20d-152">You can either use hello sample templates or create a custom Resource Manager template.</span></span> 

<span data-ttu-id="6e20d-153">tooenable Hola reparación manager service mediante [plantilla de Azure Resource Manager](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm):</span><span class="sxs-lookup"><span data-stu-id="6e20d-153">tooenable hello repair manager service using [Azure Resource Manager template](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm):</span></span>

1. <span data-ttu-id="6e20d-154">En primer lugar, compruebe que hello `apiversion` se establece demasiado`2017-07-01-preview` para hello `Microsoft.ServiceFabric/clusters` recursos, como se muestra en el siguiente fragmento de código de hello.</span><span class="sxs-lookup"><span data-stu-id="6e20d-154">First check that hello `apiversion` is set too`2017-07-01-preview` for hello `Microsoft.ServiceFabric/clusters` resource, as shown in hello following snippet.</span></span> <span data-ttu-id="6e20d-155">Si es diferente, deberá hello tooupdate `apiVersion` toohello valor `2017-07-01-preview`:</span><span class="sxs-lookup"><span data-stu-id="6e20d-155">If it is different, then you need tooupdate hello `apiVersion` toohello value `2017-07-01-preview`:</span></span>

    ```json
    {
        "apiVersion": "2017-07-01-preview",
        "type": "Microsoft.ServiceFabric/clusters",
        "name": "[parameters('clusterName')]",
        "location": "[parameters('clusterLocation')]",
        ...
    }
    ```

2. <span data-ttu-id="6e20d-156">Ahora habilitar el servicio de administrador de reparación de hello agregando Hola siguientes `addonFeatures` sección tras hello `fabricSettings` sección:</span><span class="sxs-lookup"><span data-stu-id="6e20d-156">Now enable hello repair manager service by adding hello following `addonFeatures` section after hello `fabricSettings` section:</span></span>

    ```json
    "fabricSettings": [
        ...      
        ],
        "addonFeatures": [
            "RepairManager"
        ],
    ```

3. <span data-ttu-id="6e20d-157">Después de haber actualizado la plantilla de clúster con estos cambios, aplicarlos y permitir que actualización de Hola a finalizar.</span><span class="sxs-lookup"><span data-stu-id="6e20d-157">After you have updated your cluster template with these changes, apply them and let hello upgrade finish.</span></span> <span data-ttu-id="6e20d-158">Ahora puede ver ejecutan en el clúster de servicio del sistema de administrador de reparación Hola.</span><span class="sxs-lookup"><span data-stu-id="6e20d-158">You can now see hello repair manager system service running in your cluster.</span></span> <span data-ttu-id="6e20d-159">Se denomina `fabric:/System/RepairManagerService` en la sección de servicios de sistema de Hola Hola Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="6e20d-159">It is called `fabric:/System/RepairManagerService` in hello system services section in hello Service Fabric Explorer.</span></span> 

### <a name="standalone-on-premises-clusters"></a><span data-ttu-id="6e20d-160">Clústeres locales independientes</span><span class="sxs-lookup"><span data-stu-id="6e20d-160">Standalone on-premises clusters</span></span>

<span data-ttu-id="6e20d-161">Puede usar hello [valores de configuración de clúster de Windows independiente](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest) tooenable servicio de administrador de reparación de hello en clúster de Service Fabric nueva y existente.</span><span class="sxs-lookup"><span data-stu-id="6e20d-161">You can use hello [Configuration settings for standalone Windows cluster](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest) tooenable hello repair manager service on new and existing Service Fabric cluster.</span></span>

<span data-ttu-id="6e20d-162">servicio de administrador de reparación de Hola tooenable:</span><span class="sxs-lookup"><span data-stu-id="6e20d-162">tooenable hello repair manager service:</span></span>

1. <span data-ttu-id="6e20d-163">En primer lugar, compruebe que hello `apiversion` en [las configuraciones de clúster General](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest#general-cluster-configurations) se establece demasiado`04-2017` o superior:</span><span class="sxs-lookup"><span data-stu-id="6e20d-163">First check that hello `apiversion` in [General cluster configurations](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest#general-cluster-configurations) is set too`04-2017` or higher:</span></span>

    ```json
    {
        "name": "SampleCluster",
        "clusterConfigurationVersion": "1.0.0",
        "apiVersion": "04-2017",
        ...
    }
    ```

2. <span data-ttu-id="6e20d-164">Ahora habilitar el servicio de administrador de reparación agregando Hola siguientes `addonFeaturres` sección tras hello `fabricSettings` sección tal y como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="6e20d-164">Now enable repair manager service by adding hello following `addonFeaturres` section after hello `fabricSettings` section as shown below:</span></span>

    ```json
    "fabricSettings": [
        ...      
        ],
        "addonFeatures": [
            "RepairManager"
        ],
    ```

3. <span data-ttu-id="6e20d-165">Actualizar el manifiesto de clúster con estos cambios, usar manifiesto de clúster de hello actualiza [crear un nuevo clúster](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-for-windows-server) o [configuración de clúster de actualización hello](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-upgrade-windows-server#Upgrade-the-cluster-configuration).</span><span class="sxs-lookup"><span data-stu-id="6e20d-165">Update your cluster manifest with these changes, using hello updated cluster manifest [create a new cluster](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-for-windows-server) or [upgrade hello cluster configuration](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-upgrade-windows-server#Upgrade-the-cluster-configuration).</span></span> <span data-ttu-id="6e20d-166">Una vez Hola clúster se ejecuta con el manifiesto de clúster actualizados, ahora puede ver ejecutan en el clúster, que se denomina de servicio del sistema de administrador de reparación hello `fabric:/System/RepairManagerService`, en la sección en el Explorador de Service Fabric hello de servicios del sistema.</span><span class="sxs-lookup"><span data-stu-id="6e20d-166">Once hello cluster is running with updated cluster manifest, you can now see hello repair manager system service running in your cluster, which is called `fabric:/System/RepairManagerService`, under system services section in hello Service Fabric explorer.</span></span>

### <a name="disable-automatic-windows-update-on-all-nodes"></a><span data-ttu-id="6e20d-167">Deshabilitar las actualizaciones automáticas de Windows en todos los nodos</span><span class="sxs-lookup"><span data-stu-id="6e20d-167">Disable automatic Windows Update on all nodes</span></span>

<span data-ttu-id="6e20d-168">Actualizaciones automáticas de Windows podrían provocar la pérdida tooavailability porque varios nodos de clúster pueden reiniciar más Hola mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="6e20d-168">Automatic Windows updates might lead tooavailability loss because multiple cluster nodes can restart at hello same time.</span></span> <span data-ttu-id="6e20d-169">aplicación de orquestación de revisión de Hello, de forma predeterminada, los intentos toodisable Hola actualizaciones automáticas de Windows en cada nodo del clúster.</span><span class="sxs-lookup"><span data-stu-id="6e20d-169">hello patch orchestration app, by default, tries toodisable hello automatic Windows Update on each cluster node.</span></span> <span data-ttu-id="6e20d-170">Sin embargo, si administra la configuración de Hola por un administrador o la directiva de grupo, se recomienda Hola configuración directiva demasiado "notificar antes de descargar" explícitamente de Windows Update.</span><span class="sxs-lookup"><span data-stu-id="6e20d-170">However, if hello settings are managed by an administrator or group policy, we recommend setting hello Windows Update policy too“Notify before Download” explicitly.</span></span>

### <a name="optional-enable-azure-diagnostics"></a><span data-ttu-id="6e20d-171">Opcional: habilitar Azure Diagnostics</span><span class="sxs-lookup"><span data-stu-id="6e20d-171">Optional: Enable Azure Diagnostics</span></span>

<span data-ttu-id="6e20d-172">Los clústeres que ejecutan la versión `5.6.220.9494`, y versiones posteriores, del entorno en tiempo de ejecución de Service Fabric, recopilan registros de aplicación de orquestación de revisiones como parte de los registros de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="6e20d-172">Clusters running Service Fabric runtime version `5.6.220.9494` and above collect patch orchestration app logs as part of Service Fabric logs.</span></span>
<span data-ttu-id="6e20d-173">Puede omitir este paso si el clúster se ejecuta en la versión `5.6.220.9494`, y versiones posteriores, del entorno en tiempo de ejecución de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="6e20d-173">You can skip this step if your cluster is running on Service Fabric runtime version `5.6.220.9494` and above.</span></span>

<span data-ttu-id="6e20d-174">Para los clústeres que ejecutan la versión de Service Fabric en tiempo de ejecución menor que `5.6.220.9494`, registros de aplicación de orquestación de revisión de hello se recopilan localmente en cada uno de los nodos del clúster Hola.</span><span class="sxs-lookup"><span data-stu-id="6e20d-174">For clusters running Service Fabric runtime version less than `5.6.220.9494`, logs for hello patch orchestration app are collected locally on each of hello cluster nodes.</span></span>
<span data-ttu-id="6e20d-175">Se recomienda que configure los registros de diagnósticos de Azure tooupload desde ubicación central de todos los nodos tooa.</span><span class="sxs-lookup"><span data-stu-id="6e20d-175">We recommend that you configure Azure Diagnostics tooupload logs from all nodes tooa central location.</span></span>

<span data-ttu-id="6e20d-176">Para más información sobre Azure Diagnostics, vea [Recopilar de registros con Azure Diagnostics](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-how-to-setup-wad).</span><span class="sxs-lookup"><span data-stu-id="6e20d-176">For information on enabling Azure Diagnostics, see [Collect logs by using Azure Diagnostics](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-how-to-setup-wad).</span></span>

<span data-ttu-id="6e20d-177">Registros de aplicación de orquestación de revisión de hello se generan en hello después proveedor fijo identificadores:</span><span class="sxs-lookup"><span data-stu-id="6e20d-177">Logs for hello patch orchestration app are generated on hello following fixed provider IDs:</span></span>

- <span data-ttu-id="6e20d-178">e39b723c-590c-4090-abb0-11e3e6616346</span><span class="sxs-lookup"><span data-stu-id="6e20d-178">e39b723c-590c-4090-abb0-11e3e6616346</span></span>
- <span data-ttu-id="6e20d-179">fc0028ff-bfdc-499f-80dc-ed922c52c5e9</span><span class="sxs-lookup"><span data-stu-id="6e20d-179">fc0028ff-bfdc-499f-80dc-ed922c52c5e9</span></span>
- <span data-ttu-id="6e20d-180">24afa313-0d3b-4c7c-b485-1047fd964b60</span><span class="sxs-lookup"><span data-stu-id="6e20d-180">24afa313-0d3b-4c7c-b485-1047fd964b60</span></span>
- <span data-ttu-id="6e20d-181">05dc046c-60e9-4ef7-965e-91660adffa68</span><span class="sxs-lookup"><span data-stu-id="6e20d-181">05dc046c-60e9-4ef7-965e-91660adffa68</span></span>

<span data-ttu-id="6e20d-182">En el Administrador de recursos plantilla goto `EtwEventSourceProviderConfiguration` sección en `WadCfg` y agregue Hola siguientes entradas:</span><span class="sxs-lookup"><span data-stu-id="6e20d-182">In Resource Manager template goto `EtwEventSourceProviderConfiguration` section under `WadCfg` and add hello following entries:</span></span>

```json
  {
    "provider": "e39b723c-590c-4090-abb0-11e3e6616346",
    "scheduledTransferPeriod": "PT5M",
    "DefaultEvents": {
      "eventDestination": "PatchOrchestrationApplicationTable"
    }
  },
  {
    "provider": "fc0028ff-bfdc-499f-80dc-ed922c52c5e9",
    "scheduledTransferPeriod": "PT5M",
    "DefaultEvents": {
    "eventDestination": " PatchOrchestrationApplicationTable"
    }
  },
  {
    "provider": "24afa313-0d3b-4c7c-b485-1047fd964b60",
    "scheduledTransferPeriod": "PT5M",
    "DefaultEvents": {
    "eventDestination": " PatchOrchestrationApplicationTable"
    }
  },
  {
    "provider": "05dc046c-60e9-4ef7-965e-91660adffa68",
    "scheduledTransferPeriod": "PT5M",
    "DefaultEvents": {
    "eventDestination": " PatchOrchestrationApplicationTable"
    }
  }
```

> [!NOTE]
> <span data-ttu-id="6e20d-183">Si el clúster de Service Fabric tiene varios tipos de nodo, se debe agregar la sección anterior de Hola para Hola todos los `WadCfg` secciones.</span><span class="sxs-lookup"><span data-stu-id="6e20d-183">If your Service Fabric cluster has multiple node types, then hello previous section must be added for all hello `WadCfg` sections.</span></span>

## <a name="download-hello-app-package"></a><span data-ttu-id="6e20d-184">Descargar paquete de la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="6e20d-184">Download hello app package</span></span>

<span data-ttu-id="6e20d-185">Descargar la aplicación hello de hello [vínculo de descarga](https://go.microsoft.com/fwlink/P/?linkid=849590).</span><span class="sxs-lookup"><span data-stu-id="6e20d-185">Download hello application from hello [download link](https://go.microsoft.com/fwlink/P/?linkid=849590).</span></span>

## <a name="configure-hello-app"></a><span data-ttu-id="6e20d-186">Configurar la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="6e20d-186">Configure hello app</span></span>

<span data-ttu-id="6e20d-187">Hola comportamiento de aplicación de orquestación de revisión de hello puede ser toomeet configurado sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="6e20d-187">hello behavior of hello patch orchestration app can be configured toomeet your needs.</span></span> <span data-ttu-id="6e20d-188">Invalidar los valores predeterminados de Hola pasando en el parámetro de la aplicación hello durante la creación de la aplicación o actualización.</span><span class="sxs-lookup"><span data-stu-id="6e20d-188">Override hello default values by passing in hello application parameter during application creation or update.</span></span> <span data-ttu-id="6e20d-189">Se pueden proporcionar parámetros de la aplicación mediante la especificación de `ApplicationParameter` toohello `Start-ServiceFabricApplicationUpgrade` o `New-ServiceFabricApplication` cmdlets.</span><span class="sxs-lookup"><span data-stu-id="6e20d-189">Application parameters can be provided by specifying `ApplicationParameter` toohello `Start-ServiceFabricApplicationUpgrade` or `New-ServiceFabricApplication` cmdlets.</span></span>

|<span data-ttu-id="6e20d-190">**Parámetro**</span><span class="sxs-lookup"><span data-stu-id="6e20d-190">**Parameter**</span></span>        |<span data-ttu-id="6e20d-191">**Tipo**</span><span class="sxs-lookup"><span data-stu-id="6e20d-191">**Type**</span></span>                          | <span data-ttu-id="6e20d-192">**Detalles**</span><span class="sxs-lookup"><span data-stu-id="6e20d-192">**Details**</span></span>|
|:-|-|-|
|<span data-ttu-id="6e20d-193">MaxResultsToCache</span><span class="sxs-lookup"><span data-stu-id="6e20d-193">MaxResultsToCache</span></span>    |<span data-ttu-id="6e20d-194">long</span><span class="sxs-lookup"><span data-stu-id="6e20d-194">Long</span></span>                              | <span data-ttu-id="6e20d-195">Número máximo de resultados de Windows Update que deben almacenarse en caché.</span><span class="sxs-lookup"><span data-stu-id="6e20d-195">Maximum number of Windows Update results, which should be cached.</span></span> <br><span data-ttu-id="6e20d-196">El valor predeterminado es 3000 suponiendo que:</span><span class="sxs-lookup"><span data-stu-id="6e20d-196">Default value is 3000 assuming the:</span></span> <br> <span data-ttu-id="6e20d-197">- El número de nodos es 20.</span><span class="sxs-lookup"><span data-stu-id="6e20d-197">- Number of nodes is 20.</span></span> <br> <span data-ttu-id="6e20d-198">- El número de actualizaciones en un nodo al mes es cinco.</span><span class="sxs-lookup"><span data-stu-id="6e20d-198">- Number of updates happening on a node per month is five.</span></span> <br> <span data-ttu-id="6e20d-199">- El número de resultados por cada operación es 10.</span><span class="sxs-lookup"><span data-stu-id="6e20d-199">- Number of results per operation can be 10.</span></span> <br> <span data-ttu-id="6e20d-200">-Deben almacenarse resultados de hello últimos tres meses.</span><span class="sxs-lookup"><span data-stu-id="6e20d-200">- Results for hello past three months should be stored.</span></span> |
|<span data-ttu-id="6e20d-201">TaskApprovalPolicy</span><span class="sxs-lookup"><span data-stu-id="6e20d-201">TaskApprovalPolicy</span></span>   |<span data-ttu-id="6e20d-202">Enum</span><span class="sxs-lookup"><span data-stu-id="6e20d-202">Enum</span></span> <br> <span data-ttu-id="6e20d-203">{ NodeWise, UpgradeDomainWise }</span><span class="sxs-lookup"><span data-stu-id="6e20d-203">{ NodeWise, UpgradeDomainWise }</span></span>                          |<span data-ttu-id="6e20d-204">TaskApprovalPolicy indica la directiva de hello toobe utilizada por actualizaciones de Windows hello servicio Coordinador tooinstall de nodos de clúster de Service Fabric Hola.</span><span class="sxs-lookup"><span data-stu-id="6e20d-204">TaskApprovalPolicy indicates hello policy that is toobe used by hello Coordinator Service tooinstall Windows updates across hello Service Fabric cluster nodes.</span></span><br>                         <span data-ttu-id="6e20d-205">Los valores permitidos son:</span><span class="sxs-lookup"><span data-stu-id="6e20d-205">Allowed values are:</span></span> <br>                                                           <span data-ttu-id="6e20d-206"><b>NodeWise</b>.</span><span class="sxs-lookup"><span data-stu-id="6e20d-206"><b>NodeWise</b>.</span></span> <span data-ttu-id="6e20d-207">Windows Update se instala en un nodo cada vez.</span><span class="sxs-lookup"><span data-stu-id="6e20d-207">Windows Update is installed one node at a time.</span></span> <br>                                                           <span data-ttu-id="6e20d-208"><b>UpgradeDomainWise</b>.</span><span class="sxs-lookup"><span data-stu-id="6e20d-208"><b>UpgradeDomainWise</b>.</span></span> <span data-ttu-id="6e20d-209">Windows Update se instala en un dominio de actualización cada vez.</span><span class="sxs-lookup"><span data-stu-id="6e20d-209">Windows Update is installed one upgrade domain at a time.</span></span> <span data-ttu-id="6e20d-210">(En hello máximo, todos los nodos de Hola que pertenece el dominio de actualización tooan pueden ir de Windows Update).</span><span class="sxs-lookup"><span data-stu-id="6e20d-210">(At hello maximum, all hello nodes belonging tooan upgrade domain can go for Windows Update.)</span></span>
|<span data-ttu-id="6e20d-211">LogsDiskQuotaInMB</span><span class="sxs-lookup"><span data-stu-id="6e20d-211">LogsDiskQuotaInMB</span></span>   |<span data-ttu-id="6e20d-212">long</span><span class="sxs-lookup"><span data-stu-id="6e20d-212">Long</span></span>  <br> <span data-ttu-id="6e20d-213">(Valor predeterminado: 1024)</span><span class="sxs-lookup"><span data-stu-id="6e20d-213">(Default: 1024)</span></span>               |<span data-ttu-id="6e20d-214">Tamaño máximo de los registros de la aplicación de orquestación de revisiones en MB que se pueden almacenar de forma persistente y local en un nodo.</span><span class="sxs-lookup"><span data-stu-id="6e20d-214">Maximum size of patch orchestration app logs in MB, which can be persisted locally on nodes.</span></span>
| <span data-ttu-id="6e20d-215">WUQuery</span><span class="sxs-lookup"><span data-stu-id="6e20d-215">WUQuery</span></span>               | <span data-ttu-id="6e20d-216">cadena</span><span class="sxs-lookup"><span data-stu-id="6e20d-216">string</span></span><br><span data-ttu-id="6e20d-217">(Valor predeterminado: "IsInstalled=0")</span><span class="sxs-lookup"><span data-stu-id="6e20d-217">(Default: "IsInstalled=0")</span></span>                | <span data-ttu-id="6e20d-218">Consultar tooget actualizaciones de Windows.</span><span class="sxs-lookup"><span data-stu-id="6e20d-218">Query tooget Windows updates.</span></span> <span data-ttu-id="6e20d-219">Para más información, vea [WuQuery](https://msdn.microsoft.com/library/windows/desktop/aa386526(v=vs.85).aspx).</span><span class="sxs-lookup"><span data-stu-id="6e20d-219">For more information, see [WuQuery.](https://msdn.microsoft.com/library/windows/desktop/aa386526(v=vs.85).aspx)</span></span>
| <span data-ttu-id="6e20d-220">InstallWindowsOSOnlyUpdates</span><span class="sxs-lookup"><span data-stu-id="6e20d-220">InstallWindowsOSOnlyUpdates</span></span> | <span data-ttu-id="6e20d-221">Booleano</span><span class="sxs-lookup"><span data-stu-id="6e20d-221">Bool</span></span> <br> <span data-ttu-id="6e20d-222">(Valor predeterminado: True)</span><span class="sxs-lookup"><span data-stu-id="6e20d-222">(default: True)</span></span>                 | <span data-ttu-id="6e20d-223">Esta marca permite operativo toobe de las actualizaciones del sistema instalado Windows.</span><span class="sxs-lookup"><span data-stu-id="6e20d-223">This flag allows Windows operating system updates toobe installed.</span></span>            |
| <span data-ttu-id="6e20d-224">WUOperationTimeOutInMinutes</span><span class="sxs-lookup"><span data-stu-id="6e20d-224">WUOperationTimeOutInMinutes</span></span> | <span data-ttu-id="6e20d-225">int</span><span class="sxs-lookup"><span data-stu-id="6e20d-225">Int</span></span> <br><span data-ttu-id="6e20d-226">(Valor predeterminado: 90)</span><span class="sxs-lookup"><span data-stu-id="6e20d-226">(Default: 90)</span></span>                   | <span data-ttu-id="6e20d-227">Especifica el tiempo de espera de Hola para cualquier operación de actualización de Windows (búsqueda o descargar o instalar).</span><span class="sxs-lookup"><span data-stu-id="6e20d-227">Specifies hello timeout for any Windows Update operation (search or download or install).</span></span> <span data-ttu-id="6e20d-228">Si no se realiza una operación Hola dentro de Hola tiempo de espera especificado, se anula.</span><span class="sxs-lookup"><span data-stu-id="6e20d-228">If hello operation is not completed within hello specified timeout, it is aborted.</span></span>       |
| <span data-ttu-id="6e20d-229">WURescheduleCount</span><span class="sxs-lookup"><span data-stu-id="6e20d-229">WURescheduleCount</span></span>     | <span data-ttu-id="6e20d-230">int</span><span class="sxs-lookup"><span data-stu-id="6e20d-230">Int</span></span> <br> <span data-ttu-id="6e20d-231">(Valor predeterminado: 5)</span><span class="sxs-lookup"><span data-stu-id="6e20d-231">(Default: 5)</span></span>                  | <span data-ttu-id="6e20d-232">número máximo de Hola de veces servicio Hola reprograma Hola Windows update en caso de error de una operación de forma persistente.</span><span class="sxs-lookup"><span data-stu-id="6e20d-232">hello maximum number of times hello service reschedules hello Windows update in case an operation fails persistently.</span></span>          |
| <span data-ttu-id="6e20d-233">WURescheduleTimeInMinutes</span><span class="sxs-lookup"><span data-stu-id="6e20d-233">WURescheduleTimeInMinutes</span></span> | <span data-ttu-id="6e20d-234">int</span><span class="sxs-lookup"><span data-stu-id="6e20d-234">Int</span></span> <br><span data-ttu-id="6e20d-235">(Valor predeterminado: 30)</span><span class="sxs-lookup"><span data-stu-id="6e20d-235">(Default: 30)</span></span> | <span data-ttu-id="6e20d-236">intervalo de saludo en qué Hola servicio reprograma la actualización de Windows hello en caso de error persiste.</span><span class="sxs-lookup"><span data-stu-id="6e20d-236">hello interval at which hello service reschedules hello Windows update in case failure persists.</span></span> |
| <span data-ttu-id="6e20d-237">WUFrequency</span><span class="sxs-lookup"><span data-stu-id="6e20d-237">WUFrequency</span></span>           | <span data-ttu-id="6e20d-238">Cadena separada por comas (Valor predeterminado: "Weekly, Wednesday, 7:00:00")</span><span class="sxs-lookup"><span data-stu-id="6e20d-238">Comma-separated string (Default: "Weekly, Wednesday, 7:00:00")</span></span>     | <span data-ttu-id="6e20d-239">frecuencia de Hello para la instalación de Windows Update.</span><span class="sxs-lookup"><span data-stu-id="6e20d-239">hello frequency for installing Windows Update.</span></span> <span data-ttu-id="6e20d-240">Hola formato y los posibles valores son:</span><span class="sxs-lookup"><span data-stu-id="6e20d-240">hello format and possible values are:</span></span> <br><span data-ttu-id="6e20d-241">-   Monthly, DD,HH:MM:SS, por ejemplo, Monthly, 5,12:22:32.</span><span class="sxs-lookup"><span data-stu-id="6e20d-241">-   Monthly, DD,HH:MM:SS, for example, Monthly, 5,12:22:32.</span></span> <br> <span data-ttu-id="6e20d-242">- Weekly, DÍA,HH:MM:SS, por ejemplo, Weekly, Martes, 12:22:32.</span><span class="sxs-lookup"><span data-stu-id="6e20d-242">-   Weekly, DAY,HH:MM:SS, for example, Weekly, Tuesday, 12:22:32.</span></span>  <br> <span data-ttu-id="6e20d-243">-   Daily, HH:MM:SS, por ejemplo, Daily, 12:22:32.</span><span class="sxs-lookup"><span data-stu-id="6e20d-243">-   Daily, HH:MM:SS, for example, Daily, 12:22:32.</span></span>  <br> <span data-ttu-id="6e20d-244">-  None indica que no debe realizarse Windows Update.</span><span class="sxs-lookup"><span data-stu-id="6e20d-244">-  None indicates that Windows Update shouldn't be done.</span></span>  <br><br> <span data-ttu-id="6e20d-245">Tenga en cuenta que todos los tiempos de hello en UTC.</span><span class="sxs-lookup"><span data-stu-id="6e20d-245">Note that all hello times are in UTC.</span></span>|
| <span data-ttu-id="6e20d-246">AcceptWindowsUpdateEula</span><span class="sxs-lookup"><span data-stu-id="6e20d-246">AcceptWindowsUpdateEula</span></span> | <span data-ttu-id="6e20d-247">Booleano</span><span class="sxs-lookup"><span data-stu-id="6e20d-247">Bool</span></span> <br><span data-ttu-id="6e20d-248">(Valor predeterminado: true)</span><span class="sxs-lookup"><span data-stu-id="6e20d-248">(Default: true)</span></span> | <span data-ttu-id="6e20d-249">Al establecer esta marca, aplicación hello acepta Hola acuerdo de licencia de por el usuario final para Windows Update en nombre del propietario de la máquina de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="6e20d-249">By setting this flag, hello application accepts hello End-User License Agreement for Windows Update on behalf of hello owner of hello machine.</span></span>              |

> [!TIP]
> <span data-ttu-id="6e20d-250">Si desea que Windows Update toohappen inmediatamente, establezca `WUFrequency` toohello relativa momento de la implementación de aplicación.</span><span class="sxs-lookup"><span data-stu-id="6e20d-250">If you want Windows Update toohappen immediately, set `WUFrequency` relative toohello application deployment time.</span></span> <span data-ttu-id="6e20d-251">Por ejemplo, suponga que tiene una aplicación hello prueba de nodo de cinco clústeres y el plan toodeploy a aproximadamente 5:00 P.M. hora UTC.</span><span class="sxs-lookup"><span data-stu-id="6e20d-251">For example, suppose that you have a five-node test cluster and plan toodeploy hello app at around 5:00 PM UTC.</span></span> <span data-ttu-id="6e20d-252">Si asume que la implementación o actualización de la aplicación hello toma 30 minutos en Hola Hola máximo, establezca WUFrequency como "Todos los días, 17:30:00".</span><span class="sxs-lookup"><span data-stu-id="6e20d-252">If you assume that hello application upgrade or deployment takes 30 minutes at hello maximum, set hello WUFrequency as "Daily, 17:30:00."</span></span>

## <a name="deploy-hello-app"></a><span data-ttu-id="6e20d-253">Implementar la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="6e20d-253">Deploy hello app</span></span>

1. <span data-ttu-id="6e20d-254">Finalizar todos los clústeres de hello tooprepare de hello pasos previos necesarios.</span><span class="sxs-lookup"><span data-stu-id="6e20d-254">Finish all hello prerequisite steps tooprepare hello cluster.</span></span>
2. <span data-ttu-id="6e20d-255">Implementar la aplicación de orquestación de revisión de hello como cualquier otra aplicación de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="6e20d-255">Deploy hello patch orchestration app like any other Service Fabric app.</span></span> <span data-ttu-id="6e20d-256">Puede implementar la aplicación hello mediante PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6e20d-256">You can deploy hello app by using PowerShell.</span></span> <span data-ttu-id="6e20d-257">Siga los pasos de hello en [implementar y quitar aplicaciones con PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications).</span><span class="sxs-lookup"><span data-stu-id="6e20d-257">Follow hello steps in [Deploy and remove applications using PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications).</span></span>
3. <span data-ttu-id="6e20d-258">aplicación de Hola de tooconfigure en tiempo de Hola de implementación, pase hello `ApplicationParamater` toohello `New-ServiceFabricApplication` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="6e20d-258">tooconfigure hello application at hello time of deployment, pass hello `ApplicationParamater` toohello `New-ServiceFabricApplication` cmdlet.</span></span> <span data-ttu-id="6e20d-259">Para su comodidad, hemos proporcionado Hola script Deploy.ps1 junto con la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="6e20d-259">For your convenience, we’ve provided hello script Deploy.ps1 along with hello application.</span></span> <span data-ttu-id="6e20d-260">script de Hola toouse:</span><span class="sxs-lookup"><span data-stu-id="6e20d-260">toouse hello script:</span></span>

    - <span data-ttu-id="6e20d-261">Conectar el clúster de Service Fabric tooa mediante `Connect-ServiceFabricCluster`.</span><span class="sxs-lookup"><span data-stu-id="6e20d-261">Connect tooa Service Fabric cluster by using `Connect-ServiceFabricCluster`.</span></span>
    - <span data-ttu-id="6e20d-262">Ejecutar script de PowerShell de hello Deploy.ps1 con hello adecuado `ApplicationParameter` valor.</span><span class="sxs-lookup"><span data-stu-id="6e20d-262">Execute hello PowerShell script Deploy.ps1 with hello appropriate `ApplicationParameter` value.</span></span>

> [!NOTE]
> <span data-ttu-id="6e20d-263">Tenga en hello script de Hola y de carpeta de la aplicación hello PatchOrchestrationApplication mismo directorio.</span><span class="sxs-lookup"><span data-stu-id="6e20d-263">Keep hello script and hello application folder PatchOrchestrationApplication in hello same directory.</span></span>

## <a name="upgrade-hello-app"></a><span data-ttu-id="6e20d-264">Actualizar la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="6e20d-264">Upgrade hello app</span></span>

<span data-ttu-id="6e20d-265">tooupgrade una aplicación existente de orquestación de revisión con PowerShell, siga los pasos de hello en [actualización de la aplicación de Service Fabric mediante PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-application-upgrade-tutorial-powershell).</span><span class="sxs-lookup"><span data-stu-id="6e20d-265">tooupgrade an existing patch orchestration app by using PowerShell, follow hello steps in [Service Fabric application upgrade using PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-application-upgrade-tutorial-powershell).</span></span>

## <a name="remove-hello-app"></a><span data-ttu-id="6e20d-266">Quitar aplicación hello</span><span class="sxs-lookup"><span data-stu-id="6e20d-266">Remove hello app</span></span>

<span data-ttu-id="6e20d-267">aplicación de hello tooremove, siga los pasos de hello en [implementar y quitar aplicaciones con PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications).</span><span class="sxs-lookup"><span data-stu-id="6e20d-267">tooremove hello application, follow hello steps in [Deploy and remove applications using PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications).</span></span>

<span data-ttu-id="6e20d-268">Para su comodidad, hemos proporcionado Hola script Undeploy.ps1 junto con la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="6e20d-268">For your convenience, we've provided hello script Undeploy.ps1 along with hello application.</span></span> <span data-ttu-id="6e20d-269">script de Hola toouse:</span><span class="sxs-lookup"><span data-stu-id="6e20d-269">toouse hello script:</span></span>

  - <span data-ttu-id="6e20d-270">Conectar el clúster de Service Fabric tooa mediante ```Connect-ServiceFabricCluster```.</span><span class="sxs-lookup"><span data-stu-id="6e20d-270">Connect tooa Service Fabric cluster by using ```Connect-ServiceFabricCluster```.</span></span>

  - <span data-ttu-id="6e20d-271">Ejecutar script de PowerShell de hello Undeploy.ps1.</span><span class="sxs-lookup"><span data-stu-id="6e20d-271">Execute hello PowerShell script Undeploy.ps1.</span></span>

> [!NOTE]
> <span data-ttu-id="6e20d-272">Tenga en hello script de Hola y de carpeta de la aplicación hello PatchOrchestrationApplication mismo directorio.</span><span class="sxs-lookup"><span data-stu-id="6e20d-272">Keep hello script and hello application folder PatchOrchestrationApplication in hello same directory.</span></span>

## <a name="view-hello-windows-update-results"></a><span data-ttu-id="6e20d-273">Ver los resultados de actualización de Windows hello</span><span class="sxs-lookup"><span data-stu-id="6e20d-273">View hello Windows Update results</span></span>

<span data-ttu-id="6e20d-274">aplicación de orquestación de revisión de Hello expone el usuario toohello resultados históricos de las API de REST toodisplay Hola.</span><span class="sxs-lookup"><span data-stu-id="6e20d-274">hello patch orchestration app exposes REST APIs toodisplay hello historical results toohello user.</span></span> <span data-ttu-id="6e20d-275">Un ejemplo de Hola resultado JSON:</span><span class="sxs-lookup"><span data-stu-id="6e20d-275">An example of hello result JSON:</span></span>
```json
[
  {
    "NodeName": "_stg1vm_1",
    "WindowsUpdateOperationResults": [
      {
        "OperationResult": 0,
        "NodeName": "_stg1vm_1",
        "OperationTime": "2017-05-21T11:46:52.1953713Z",
        "UpdateDetails": [
          {
            "UpdateId": "7392acaf-6a85-427c-8a8d-058c25beb0d6",
            "Title": "Cumulative Security Update for Internet Explorer 11 for Windows Server 2012 R2 (KB3185319)",
            "Description": "A security issue has been identified in a Microsoft software product that could affect your system. You can help protect your system by installing this update from Microsoft. For a complete listing of hello issues that are included in this update, see hello associated Microsoft Knowledge Base article. After you install this update, you may have toorestart your system.",
            "ResultCode": 0
          }
        ],
        "OperationType": 1,
        "WindowsUpdateQuery": "IsInstalled=0",
        "WindowsUpdateFrequency": "Daily,10:00:00",
        "RebootRequired": false
      }
    ]
  },
  ...
]
```
<span data-ttu-id="6e20d-276">Si no hay ninguna actualización está programada todavía, el resultado de hello JSON está vacío.</span><span class="sxs-lookup"><span data-stu-id="6e20d-276">If no update is scheduled yet, hello result JSON is empty.</span></span>

<span data-ttu-id="6e20d-277">Inicie sesión en el clúster de toohello tooquery Windows Update resultados.</span><span class="sxs-lookup"><span data-stu-id="6e20d-277">Log in toohello cluster tooquery Windows Update results.</span></span> <span data-ttu-id="6e20d-278">A continuación, averiguar la dirección de la réplica de hello para el elemento primario de Hola de hello servicio Coordinador de y alcanza Hola URL desde el Explorador de hello: http://&lt;IP de réplica&gt;:&lt;ApplicationPort&gt;/PatchOrchestrationApplication/v1 / GetWindowsUpdateResults.</span><span class="sxs-lookup"><span data-stu-id="6e20d-278">Then find out hello replica address for hello primary of hello Coordinator Service, and hit hello URL from hello browser: http://&lt;REPLICA-IP&gt;:&lt;ApplicationPort&gt;/PatchOrchestrationApplication/v1/GetWindowsUpdateResults.</span></span>

<span data-ttu-id="6e20d-279">extremo REST de Hello para el servicio Coordinador de hello tiene un puerto dinámico.</span><span class="sxs-lookup"><span data-stu-id="6e20d-279">hello REST endpoint for hello Coordinator Service has a dynamic port.</span></span> <span data-ttu-id="6e20d-280">toocheck Hola URL exacta, consulte toohello Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="6e20d-280">toocheck hello exact URL, refer toohello Service Fabric Explorer.</span></span> <span data-ttu-id="6e20d-281">Por ejemplo, están disponibles en los resultados de hello `http://10.0.0.7:20000/PatchOrchestrationApplication/v1/GetWindowsUpdateResults`.</span><span class="sxs-lookup"><span data-stu-id="6e20d-281">For example, hello results are available at `http://10.0.0.7:20000/PatchOrchestrationApplication/v1/GetWindowsUpdateResults`.</span></span>

![Imagen de punto de conexión REST](media/service-fabric-patch-orchestration-application/Rest_Endpoint.png)


<span data-ttu-id="6e20d-283">Si está habilitado el proxy inverso de hello en clúster de hello, puede tener acceso URL Hola desde fuera de clúster de hello así.</span><span class="sxs-lookup"><span data-stu-id="6e20d-283">If hello reverse proxy is enabled on hello cluster, you can access hello URL from outside of hello cluster as well.</span></span>
<span data-ttu-id="6e20d-284">Hola de punto de conexión que necesita toobe aciertos es http://&lt;SERVERURL&gt;:&lt;REVERSEPROXYPORT&gt;/PatchOrchestrationApplication/CoordinatorService/v1/GetWindowsUpdateResults.</span><span class="sxs-lookup"><span data-stu-id="6e20d-284">hello endpoint that needs toobe hit is http://&lt;SERVERURL&gt;:&lt;REVERSEPROXYPORT&gt;/PatchOrchestrationApplication/CoordinatorService/v1/GetWindowsUpdateResults.</span></span>

<span data-ttu-id="6e20d-285">proxy inverso de hello tooenable en clúster de hello, siga los pasos de hello en [proxy en Azure Service Fabric inverso](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy).</span><span class="sxs-lookup"><span data-stu-id="6e20d-285">tooenable hello reverse proxy on hello cluster, follow hello steps in [Reverse proxy in Azure Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy).</span></span> 

> 
> [!WARNING]
> <span data-ttu-id="6e20d-286">Después de configura el proxy inverso de hello, todos los servicios en clúster de hello micro que exponen un extremo HTTP son direccionables desde fuera de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="6e20d-286">After hello reverse proxy is configured, all micro services in hello cluster that expose an HTTP endpoint are addressable from outside hello cluster.</span></span>

## <a name="diagnosticshealth-events"></a><span data-ttu-id="6e20d-287">Eventos de diagnóstico y mantenimiento</span><span class="sxs-lookup"><span data-stu-id="6e20d-287">Diagnostics/health events</span></span>

### <a name="collect-patch-orchestration-app-logs"></a><span data-ttu-id="6e20d-288">Recopilar los registros de la aplicación de orquestación de revisiones</span><span class="sxs-lookup"><span data-stu-id="6e20d-288">Collect patch orchestration app logs</span></span>

<span data-ttu-id="6e20d-289">Los registros de aplicación de orquestación de revisiones se recopilan como parte de los registros de Service Fabric en la versión del runtime `5.6.220.9494` y versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="6e20d-289">Patch orchestration app logs are collected as part of Service Fabric logs from runtime version `5.6.220.9494` and above.</span></span>
<span data-ttu-id="6e20d-290">Para los clústeres que ejecutan la versión en tiempo de ejecución de Service Fabric inferior a `5.6.220.9494`, se pueden recopilar registros mediante uno de los siguientes métodos de Hola.</span><span class="sxs-lookup"><span data-stu-id="6e20d-290">For clusters running Service Fabric runtime version less than `5.6.220.9494`, logs can be collected by using one of hello following methods.</span></span>

#### <a name="locally-on-each-node"></a><span data-ttu-id="6e20d-291">Localmente en cada nodo</span><span class="sxs-lookup"><span data-stu-id="6e20d-291">Locally on each node</span></span>

<span data-ttu-id="6e20d-292">Los registros se recopilan localmente en cada nodo de clúster de Service Fabric si la versión del entorno en tiempo de ejecución de Service Fabric es inferior a la `5.6.220.9494`.</span><span class="sxs-lookup"><span data-stu-id="6e20d-292">Logs are collected locally on each Service Fabric cluster node if Service Fabric runtime version is less than `5.6.220.9494`.</span></span> <span data-ttu-id="6e20d-293">Hola Hola registros de ubicación tooaccess es \[Service Fabric\_instalación\_unidad\]:\\PatchOrchestrationApplication\\registros.</span><span class="sxs-lookup"><span data-stu-id="6e20d-293">hello location tooaccess hello logs is \[Service Fabric\_Installation\_Drive\]:\\PatchOrchestrationApplication\\logs.</span></span>

<span data-ttu-id="6e20d-294">Por ejemplo, si Service Fabric se instala en la unidad D, ruta de acceso de hello es D:\\PatchOrchestrationApplication\\registros.</span><span class="sxs-lookup"><span data-stu-id="6e20d-294">For example, if Service Fabric is installed on drive D, hello path is D:\\PatchOrchestrationApplication\\logs.</span></span>

#### <a name="central-location"></a><span data-ttu-id="6e20d-295">Ubicación central</span><span class="sxs-lookup"><span data-stu-id="6e20d-295">Central location</span></span>

<span data-ttu-id="6e20d-296">Si diagnósticos de Azure está configurado como parte de los pasos de requisitos previos, registros de aplicación de orquestación de revisión de hello están disponibles en el almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="6e20d-296">If Azure Diagnostics is configured as part of prerequisite steps, logs for hello patch orchestration app are available in Azure Storage.</span></span>

### <a name="health-reports"></a><span data-ttu-id="6e20d-297">Informes de mantenimiento</span><span class="sxs-lookup"><span data-stu-id="6e20d-297">Health reports</span></span>

<span data-ttu-id="6e20d-298">aplicación de orquestación de revisión de Hello también publica los informes de mantenimiento contra Hola servicio Coordinador u Hola nodo servicio de agente en hello casos siguientes:</span><span class="sxs-lookup"><span data-stu-id="6e20d-298">hello patch orchestration app also publishes health reports against hello Coordinator Service or hello Node Agent Service in hello following cases:</span></span>

#### <a name="a-windows-update-operation-failed"></a><span data-ttu-id="6e20d-299">Error en la operación de Windows Update</span><span class="sxs-lookup"><span data-stu-id="6e20d-299">A Windows Update operation failed</span></span>

<span data-ttu-id="6e20d-300">Si se produce un error en una operación de actualización de Windows en un nodo, se genera un informe de mantenimiento contra Hola nodo servicio de agente.</span><span class="sxs-lookup"><span data-stu-id="6e20d-300">If a Windows Update operation fails on a node, a health report is generated against hello Node Agent Service.</span></span> <span data-ttu-id="6e20d-301">Detalles de informe de mantenimiento de hello contienen nombre de nodo problemático Hola.</span><span class="sxs-lookup"><span data-stu-id="6e20d-301">Details of hello health report contain hello problematic node name.</span></span>

<span data-ttu-id="6e20d-302">Después de aplicar revisiones se completó correctamente en el nodo problemático hello, informe de Hola se borra automáticamente.</span><span class="sxs-lookup"><span data-stu-id="6e20d-302">After patching is successfully completed on hello problematic node, hello report is automatically cleared.</span></span>

#### <a name="hello-node-agent-ntservice-is-down"></a><span data-ttu-id="6e20d-303">Hola servicio NT de agente de nodo está inactivo</span><span class="sxs-lookup"><span data-stu-id="6e20d-303">hello Node Agent NTService is down</span></span>

<span data-ttu-id="6e20d-304">Si Hola servicio NT de agente de nodo está inactivo en un nodo, se genera un informe de mantenimiento de nivel de advertencia contra Hola nodo servicio de agente.</span><span class="sxs-lookup"><span data-stu-id="6e20d-304">If hello Node Agent NTService is down on a node, a warning-level health report is generated against hello Node Agent Service.</span></span>

#### <a name="hello-repair-manager-service-is-not-enabled"></a><span data-ttu-id="6e20d-305">servicio de administrador de reparación de Hello no está habilitado</span><span class="sxs-lookup"><span data-stu-id="6e20d-305">hello repair manager service is not enabled</span></span>

<span data-ttu-id="6e20d-306">Si no se encuentra el servicio de administrador de reparación de hello en clúster de hello, se genera un informe de mantenimiento de nivel de advertencia para hello servicio Coordinador.</span><span class="sxs-lookup"><span data-stu-id="6e20d-306">If hello repair manager service is not found on hello cluster, a warning-level health report is generated for hello Coordinator Service.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="6e20d-307">Preguntas más frecuentes</span><span class="sxs-lookup"><span data-stu-id="6e20d-307">Frequently asked questions</span></span>

<span data-ttu-id="6e20d-308">P:</span><span class="sxs-lookup"><span data-stu-id="6e20d-308">Q.</span></span> <span data-ttu-id="6e20d-309">**¿Por qué veo mi clúster en un estado de error cuando se ejecuta la aplicación de orquestación de hello revisión?**</span><span class="sxs-lookup"><span data-stu-id="6e20d-309">**Why do I see my cluster in an error state when hello patch orchestration app is running?**</span></span>

<span data-ttu-id="6e20d-310">A.</span><span class="sxs-lookup"><span data-stu-id="6e20d-310">A.</span></span> <span data-ttu-id="6e20d-311">Durante el proceso de instalación de hello, aplicación de orquestación de revisión de hello deshabilita o reinicia nodos, lo que pueden producir temporalmente en estado de Hola de clúster de hello bajan.</span><span class="sxs-lookup"><span data-stu-id="6e20d-311">During hello installation process, hello patch orchestration app disables or restarts nodes, which can temporarily result in hello health of hello cluster going down.</span></span>

<span data-ttu-id="6e20d-312">Se basa en la directiva de hello para la aplicación hello, ya sea un nodo puede bajar durante una operación de aplicación de revisiones *o* todo un dominio de actualización puede desplazarse hacia abajo al mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="6e20d-312">Based on hello policy for hello application, either one node can go down during a patching operation *or* an entire upgrade domain can go down simultaneously.</span></span>

<span data-ttu-id="6e20d-313">Extremo de Hola de hello instalación de Windows Update, Hola nodos se vuelve a habilitar después del reinicio.</span><span class="sxs-lookup"><span data-stu-id="6e20d-313">By hello end of hello Windows Update installation, hello nodes are reenabled post restart.</span></span>

<span data-ttu-id="6e20d-314">En el siguiente ejemplo de Hola, clúster de hello produjo un estado de error de tooan temporalmente porque estaban apagados de dos nodos y Hola MaxPercentageUnhealthNodes directiva se ha infringido.</span><span class="sxs-lookup"><span data-stu-id="6e20d-314">In hello following example, hello cluster went tooan error state temporarily because two nodes were down and hello MaxPercentageUnhealthNodes policy was violated.</span></span> <span data-ttu-id="6e20d-315">error de Hello es temporal hasta que Hola aplicar revisiones operación está en curso.</span><span class="sxs-lookup"><span data-stu-id="6e20d-315">hello error is temporary until hello patching operation is ongoing.</span></span>

![Imagen de clúster en mal estado](media/service-fabric-patch-orchestration-application/MaxPercentage_causing_unhealthy_cluster.png)

<span data-ttu-id="6e20d-317">Si persiste el problema de hello, consulte la sección de solución de problemas de toohello.</span><span class="sxs-lookup"><span data-stu-id="6e20d-317">If hello issue persists, refer toohello Troubleshooting section.</span></span>

<span data-ttu-id="6e20d-318">P:</span><span class="sxs-lookup"><span data-stu-id="6e20d-318">Q.</span></span> <span data-ttu-id="6e20d-319">**La aplicación de orquestación de revisiones está en estado de advertencia**</span><span class="sxs-lookup"><span data-stu-id="6e20d-319">**Patch orchestration app is in warning state**</span></span>

<span data-ttu-id="6e20d-320">A.</span><span class="sxs-lookup"><span data-stu-id="6e20d-320">A.</span></span> <span data-ttu-id="6e20d-321">Compruebe toosee si un informe de estado registrado con la aplicación hello es la causa de Hola.</span><span class="sxs-lookup"><span data-stu-id="6e20d-321">Check toosee if a health report posted against hello application is hello root cause.</span></span> <span data-ttu-id="6e20d-322">Por lo general, la advertencia de hello contiene detalles del problema de Hola.</span><span class="sxs-lookup"><span data-stu-id="6e20d-322">Usually, hello warning contains details of hello problem.</span></span> <span data-ttu-id="6e20d-323">Si el problema de hello es transitorio, aplicación hello es esperado tooauto-recuperación de este estado.</span><span class="sxs-lookup"><span data-stu-id="6e20d-323">If hello issue is transient, hello application is expected tooauto-recover from this state.</span></span>

<span data-ttu-id="6e20d-324">P:</span><span class="sxs-lookup"><span data-stu-id="6e20d-324">Q.</span></span> <span data-ttu-id="6e20d-325">**¿Qué puedo hacer si el clúster está en mal estado y se necesita una actualización de sistema operativo urgentes toodo?**</span><span class="sxs-lookup"><span data-stu-id="6e20d-325">**What can I do if my cluster is unhealthy and I need toodo an urgent operating system update?**</span></span>

<span data-ttu-id="6e20d-326">A.</span><span class="sxs-lookup"><span data-stu-id="6e20d-326">A.</span></span> <span data-ttu-id="6e20d-327">aplicación de orquestación de revisión de Hello no instalar actualizaciones al clúster de hello está en mal estado.</span><span class="sxs-lookup"><span data-stu-id="6e20d-327">hello patch orchestration app does not install updates while hello cluster is unhealthy.</span></span> <span data-ttu-id="6e20d-328">Intente toobring el clúster tooa estado correcto toounblock Hola revisión orquestación aplicación flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="6e20d-328">Try toobring your cluster tooa healthy state toounblock hello patch orchestration app workflow.</span></span>

<span data-ttu-id="6e20d-329">P:</span><span class="sxs-lookup"><span data-stu-id="6e20d-329">Q.</span></span> <span data-ttu-id="6e20d-330">**¿Por qué aplicar revisiones a través de clústeres tardan tanto tiempo toorun?**</span><span class="sxs-lookup"><span data-stu-id="6e20d-330">**Why does patching across clusters take so long toorun?**</span></span>

<span data-ttu-id="6e20d-331">A.</span><span class="sxs-lookup"><span data-stu-id="6e20d-331">A.</span></span> <span data-ttu-id="6e20d-332">tiempo de Hello sea necesario mediante la aplicación de orquestación de revisión de hello depende principalmente de hello siguientes factores:</span><span class="sxs-lookup"><span data-stu-id="6e20d-332">hello time needed by hello patch orchestration app is mostly dependent on hello following factors:</span></span>

- <span data-ttu-id="6e20d-333">Directiva de Hola de hello servicio del coordinador.</span><span class="sxs-lookup"><span data-stu-id="6e20d-333">hello policy of hello Coordinator Service.</span></span> 
  - <span data-ttu-id="6e20d-334">Hola directiva predeterminada, `NodeWise`, da como resultado un solo nodo de aplicación de revisiones a la vez.</span><span class="sxs-lookup"><span data-stu-id="6e20d-334">hello default policy, `NodeWise`, results in patching only one node at a time.</span></span> <span data-ttu-id="6e20d-335">Especialmente en el caso de hello de clústeres más grandes, se recomienda que realice hello `UpgradeDomainWise` directiva tooachieve más rápido aplicar revisiones a través de clústeres.</span><span class="sxs-lookup"><span data-stu-id="6e20d-335">Especially in hello case of bigger clusters, we recommend that you use hello `UpgradeDomainWise` policy tooachieve faster patching across clusters.</span></span>
- <span data-ttu-id="6e20d-336">número de Hola de actualizaciones disponibles para su descarga e instalación.</span><span class="sxs-lookup"><span data-stu-id="6e20d-336">hello number of updates available for download and installation.</span></span> 
- <span data-ttu-id="6e20d-337">Hola toodownload tiempo promedio necesario e instale una actualización, lo que no debe tener más de un par de horas.</span><span class="sxs-lookup"><span data-stu-id="6e20d-337">hello average time needed toodownload and install an update, which should not exceed a couple of hours.</span></span>
- <span data-ttu-id="6e20d-338">Hola rendimiento de hello VM y ancho de banda de red.</span><span class="sxs-lookup"><span data-stu-id="6e20d-338">hello performance of hello VM and network bandwidth.</span></span>

<span data-ttu-id="6e20d-339">P:</span><span class="sxs-lookup"><span data-stu-id="6e20d-339">Q.</span></span> <span data-ttu-id="6e20d-340">**¿Por qué veo algunas actualizaciones en los resultados de Windows Update obtenidos a través de la api de REST, pero no se admite con hello historial de Windows Update en el equipo?**</span><span class="sxs-lookup"><span data-stu-id="6e20d-340">**Why do I see some updates in Windows Update results obtained via REST api's, but not under hello Windows Update history on machine?**</span></span>

<span data-ttu-id="6e20d-341">A.</span><span class="sxs-lookup"><span data-stu-id="6e20d-341">A.</span></span> <span data-ttu-id="6e20d-342">Algunas actualizaciones de producto necesitan toobe comprueba en su historial de actualización/revisión respectivos.</span><span class="sxs-lookup"><span data-stu-id="6e20d-342">Some product updates need toobe checked in their respective update/patch history.</span></span> <span data-ttu-id="6e20d-343">Por ejemplo: Las actualizaciones de Windows Defender no se muestran en el historial de Windows Update en Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="6e20d-343">Eg: Windows Defender updates do not show up in Windows Update history on Windows Server 2016.</span></span>

## <a name="disclaimers"></a><span data-ttu-id="6e20d-344">Declinación de responsabilidades</span><span class="sxs-lookup"><span data-stu-id="6e20d-344">Disclaimers</span></span>

- <span data-ttu-id="6e20d-345">aplicación de orquestación de revisión de Hello acepta Hola acuerdo de licencia de por el usuario final de Windows Update en nombre de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="6e20d-345">hello patch orchestration app accepts hello End-User License Agreement of Windows Update on behalf of hello user.</span></span> <span data-ttu-id="6e20d-346">Si lo desea, configuración de hello puede desactivarse en la configuración de Hola de aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="6e20d-346">Optionally, hello setting can be turned off in hello configuration of hello application.</span></span>

- <span data-ttu-id="6e20d-347">aplicación de orquestación de revisión de Hello recopila telemetría tootrack uso y el rendimiento.</span><span class="sxs-lookup"><span data-stu-id="6e20d-347">hello patch orchestration app collects telemetry tootrack usage and performance.</span></span> <span data-ttu-id="6e20d-348">telemetría de la aplicación Hello sigue configuración Hola de configuración de telemetría de hello Service Fabric en tiempo de ejecución (que está activada de forma predeterminada).</span><span class="sxs-lookup"><span data-stu-id="6e20d-348">hello application’s telemetry follows hello setting of hello Service Fabric runtime’s telemetry setting (which is on by default).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="6e20d-349">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="6e20d-349">Troubleshooting</span></span>

### <a name="a-node-is-not-coming-back-tooup-state"></a><span data-ttu-id="6e20d-350">Un nodo no es ir los tooup estado</span><span class="sxs-lookup"><span data-stu-id="6e20d-350">A node is not coming back tooup state</span></span>

<span data-ttu-id="6e20d-351">**nodo de Hello podría bloquearse en un estado deshabilitado porque**:</span><span class="sxs-lookup"><span data-stu-id="6e20d-351">**hello node might be stuck in a disabling state because**:</span></span>

<span data-ttu-id="6e20d-352">Hay una comprobación de seguridad pendiente.</span><span class="sxs-lookup"><span data-stu-id="6e20d-352">A safety check is pending.</span></span> <span data-ttu-id="6e20d-353">tooremedy esta situación, asegúrese de que hay suficientes nodos están disponibles en un estado correcto.</span><span class="sxs-lookup"><span data-stu-id="6e20d-353">tooremedy this situation, ensure that enough nodes are available in a healthy state.</span></span>

<span data-ttu-id="6e20d-354">**nodo de Hello podría bloquearse en un estado deshabilitado porque**:</span><span class="sxs-lookup"><span data-stu-id="6e20d-354">**hello node might be stuck in a disabled state because**:</span></span>

- <span data-ttu-id="6e20d-355">nodo de Hola se ha deshabilitado manualmente.</span><span class="sxs-lookup"><span data-stu-id="6e20d-355">hello node was disabled manually.</span></span>
- <span data-ttu-id="6e20d-356">nodo de Hola se deshabilitó debido tooan trabajo de infraestructura de Azure en curso.</span><span class="sxs-lookup"><span data-stu-id="6e20d-356">hello node was disabled due tooan ongoing Azure infrastructure job.</span></span>
- <span data-ttu-id="6e20d-357">nodo de Hello deshabilitó temporalmente por nodo de hello de la orquestación aplicación Hola revisión toopatch.</span><span class="sxs-lookup"><span data-stu-id="6e20d-357">hello node was disabled temporarily by hello patch orchestration app toopatch hello node.</span></span>

<span data-ttu-id="6e20d-358">**Hello nodo podría bloquearse en un estado inactivo porque**:</span><span class="sxs-lookup"><span data-stu-id="6e20d-358">**hello node might be stuck in a down state because**:</span></span>

- <span data-ttu-id="6e20d-359">nodo de Hola se puso en un estado inactivo manualmente.</span><span class="sxs-lookup"><span data-stu-id="6e20d-359">hello node was put in a down state manually.</span></span>
- <span data-ttu-id="6e20d-360">nodo de saludo se está llevando a cabo un reinicio (que podría ser desencadenado por la aplicación de orquestación de revisión de hello).</span><span class="sxs-lookup"><span data-stu-id="6e20d-360">hello node is undergoing a restart (which might be triggered by hello patch orchestration app).</span></span>
- <span data-ttu-id="6e20d-361">nodo de Hello está inactivo debido tooa defectuoso VM o equipo o red problemas de conectividad.</span><span class="sxs-lookup"><span data-stu-id="6e20d-361">hello node is down due tooa faulty VM or machine or network connectivity issues.</span></span>

### <a name="updates-were-skipped-on-some-nodes"></a><span data-ttu-id="6e20d-362">Las actualizaciones se omitieron en algunos nodos</span><span class="sxs-lookup"><span data-stu-id="6e20d-362">Updates were skipped on some nodes</span></span>

<span data-ttu-id="6e20d-363">aplicación de orquestación de revisión de Hello intenta tooinstall una actualización correspondiente toohello reprogramación directiva de Windows.</span><span class="sxs-lookup"><span data-stu-id="6e20d-363">hello patch orchestration app tries tooinstall a Windows update according toohello rescheduling policy.</span></span> <span data-ttu-id="6e20d-364">servicio de Hello trata de nodo de hello toorecover y omitir la directiva de aplicación de hello actualización correspondiente toohello.</span><span class="sxs-lookup"><span data-stu-id="6e20d-364">hello service tries toorecover hello node and skip hello update according toohello application policy.</span></span>

<span data-ttu-id="6e20d-365">En tal caso, se genera un informe de estado de nivel de advertencia contra Hola nodo servicio de agente.</span><span class="sxs-lookup"><span data-stu-id="6e20d-365">In such a case, a warning-level health report is generated against hello Node Agent Service.</span></span> <span data-ttu-id="6e20d-366">resultado de Hello de Windows Update también contiene hello es posible que el error de Hola.</span><span class="sxs-lookup"><span data-stu-id="6e20d-366">hello result for Windows Update also contains hello possible reason for hello failure.</span></span>

### <a name="hello-health-of-hello-cluster-goes-tooerror-while-hello-update-installs"></a><span data-ttu-id="6e20d-367">estado de Hola de clúster de Hola va tooerror mientras instala la actualización de Hola</span><span class="sxs-lookup"><span data-stu-id="6e20d-367">hello health of hello cluster goes tooerror while hello update installs</span></span>

<span data-ttu-id="6e20d-368">Una actualización de Windows defectuosa puede acabar con estado de Hola de una aplicación o un clúster en un nodo concreto o un dominio de actualización.</span><span class="sxs-lookup"><span data-stu-id="6e20d-368">A faulty Windows update can bring down hello health of an application or cluster on a particular node or upgrade domain.</span></span> <span data-ttu-id="6e20d-369">aplicación de orquestación de revisión de Hello interrumpe las operaciones posteriores de Windows Update hasta que el clúster Hola nuevo es correcto.</span><span class="sxs-lookup"><span data-stu-id="6e20d-369">hello patch orchestration app discontinues any subsequent Windows Update operation until hello cluster is healthy again.</span></span>

<span data-ttu-id="6e20d-370">Un administrador debe intervenir y determinar por qué aplicación hello o clúster pasara a ser incorrecto debido a tooWindows Update.</span><span class="sxs-lookup"><span data-stu-id="6e20d-370">An administrator must intervene and determine why hello application or cluster became unhealthy due tooWindows Update.</span></span>

## <a name="release-notes-"></a><span data-ttu-id="6e20d-371">Notas de la versión:</span><span class="sxs-lookup"><span data-stu-id="6e20d-371">Release Notes :</span></span>

### <a name="version-110"></a><span data-ttu-id="6e20d-372">Versión 1.1.0</span><span class="sxs-lookup"><span data-stu-id="6e20d-372">Version 1.1.0</span></span>
- <span data-ttu-id="6e20d-373">Versión pública</span><span class="sxs-lookup"><span data-stu-id="6e20d-373">Public release</span></span>

### <a name="version-111"></a><span data-ttu-id="6e20d-374">Versión 1.1.1</span><span class="sxs-lookup"><span data-stu-id="6e20d-374">Version 1.1.1</span></span>
- <span data-ttu-id="6e20d-375">Se ha corregido un error en SetupEntryPoint de NodeAgentService que impedía la instalación de NodeAgentNTService.</span><span class="sxs-lookup"><span data-stu-id="6e20d-375">Fixed a bug in SetupEntryPoint of NodeAgentService that prevented installation of NodeAgentNTService.</span></span>

### <a name="version-120-latest"></a><span data-ttu-id="6e20d-376">Versión 1.2.0 (más reciente)</span><span class="sxs-lookup"><span data-stu-id="6e20d-376">Version 1.2.0 (Latest)</span></span>

- <span data-ttu-id="6e20d-377">Correcciones de errores en el flujo de trabajo de reinicio del sistema.</span><span class="sxs-lookup"><span data-stu-id="6e20d-377">Bug fixes around system restart workflow.</span></span>
- <span data-ttu-id="6e20d-378">Corrección de errores en la creación de las tareas de RM pendientes toowhich comprobación de mantenimiento durante la preparación de las tareas de reparación no estaba sucediendo según lo previsto.</span><span class="sxs-lookup"><span data-stu-id="6e20d-378">Bug fix in creation of RM tasks due toowhich health check during preparing repair tasks wasn't happening as expected.</span></span>
- <span data-ttu-id="6e20d-379">Modo de inicio de hello modificada para servicio de windows POANodeSvc automática toodelayed-automáticamente.</span><span class="sxs-lookup"><span data-stu-id="6e20d-379">Changed hello startup mode for windows service POANodeSvc from auto toodelayed-auto.</span></span>
