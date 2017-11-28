---
title: "aaaAdd o quitar nodos tooa independiente clúster de Service Fabric | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooadd o quitar nodos tooan Azure Service Fabric clúster en una máquina física o virtual ejecuta Windows Server, que puede ser local o en cualquier nube."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: bc6b8fc0-d2af-42f8-a164-58538be38d02
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 2/02/2017
ms.author: dekapur
ms.openlocfilehash: 1da908ad9840faa052e0b4021bc2d4ce732b02bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-or-remove-nodes-tooa-standalone-service-fabric-cluster-running-on-windows-server"></a><span data-ttu-id="b0a9c-103">Agregar o quitar el clúster de Service Fabric como nodos tooa independiente que se ejecuta en Windows Server</span><span class="sxs-lookup"><span data-stu-id="b0a9c-103">Add or remove nodes tooa standalone Service Fabric cluster running on Windows Server</span></span>
<span data-ttu-id="b0a9c-104">Una vez haya [creó el clúster de Service Fabric independientes en equipos con Windows Server](service-fabric-cluster-creation-for-windows-server.md), pueden cambiar sus necesidades empresariales y tal vez necesite tooadd o quitar nodos tooyour clúster.</span><span class="sxs-lookup"><span data-stu-id="b0a9c-104">After you have [created your standalone Service Fabric cluster on Windows Server machines](service-fabric-cluster-creation-for-windows-server.md), your business needs may change and you might need tooadd or remove nodes tooyour cluster.</span></span> <span data-ttu-id="b0a9c-105">Este artículo proporciona los pasos detallados tooachieve esto.</span><span class="sxs-lookup"><span data-stu-id="b0a9c-105">This article provides detailed steps tooachieve this.</span></span> <span data-ttu-id="b0a9c-106">Tenga en cuenta que no se permite agregar o eliminar nodos en los clústeres de desarrollo local.</span><span class="sxs-lookup"><span data-stu-id="b0a9c-106">Please note that add/remove node functionality is not supported in local development clusters.</span></span>

## <a name="add-nodes-tooyour-cluster"></a><span data-ttu-id="b0a9c-107">Agregar nodos tooyour clúster</span><span class="sxs-lookup"><span data-stu-id="b0a9c-107">Add nodes tooyour cluster</span></span>
1. <span data-ttu-id="b0a9c-108">Hola preparar la máquina virtual u otro equipo que desee tooadd tooyour clúster siguiendo los pasos de hello mencionados en hello [Hola de preparar máquinas toomeet requisitos previos de hello para la implementación de clúster](service-fabric-cluster-creation-for-windows-server.md) sección</span><span class="sxs-lookup"><span data-stu-id="b0a9c-108">Prepare hello VM/machine you want tooadd tooyour cluster by following hello steps mentioned in hello [Prepare hello machines toomeet hello prerequisites for cluster deployment](service-fabric-cluster-creation-for-windows-server.md) section</span></span>
2. <span data-ttu-id="b0a9c-109">Identificar qué dominio de error y el dominio de actualización son tooadd continuo que esta máquina virtual/máquina</span><span class="sxs-lookup"><span data-stu-id="b0a9c-109">Identify which fault domain and upgrade domain you are going tooadd this VM/machine to</span></span>
3. <span data-ttu-id="b0a9c-110">Escritorio remoto (RDP) en hello VM u otro equipo que desea que el clúster de toohello tooadd</span><span class="sxs-lookup"><span data-stu-id="b0a9c-110">Remote desktop (RDP) into hello VM/machine that you want tooadd toohello cluster</span></span>
4. <span data-ttu-id="b0a9c-111">Copia o [Descargar paquete de independiente de Hola para Service Fabric para Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690) toohello VM/máquina y descomprima el paquete de Hola</span><span class="sxs-lookup"><span data-stu-id="b0a9c-111">Copy or [download hello standalone package for Service Fabric for Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690) toohello VM/machine and unzip hello package</span></span>
5. <span data-ttu-id="b0a9c-112">Ejecutar Powershell con privilegios elevados y vaya toohello ubicación del paquete descomprimida Hola</span><span class="sxs-lookup"><span data-stu-id="b0a9c-112">Run Powershell with elevated privileges, and navigate toohello location of hello unzipped package</span></span>
6. <span data-ttu-id="b0a9c-113">Ejecute hello *AddNode.ps1* secuencia de comandos con parámetros de Hola que describen Hola nuevo nodo tooadd.</span><span class="sxs-lookup"><span data-stu-id="b0a9c-113">Run hello *AddNode.ps1* script with hello parameters describing hello new node tooadd.</span></span> <span data-ttu-id="b0a9c-114">ejemplo de Hola siguiente agrega un nuevo nodo denominado VM5, con el tipo NodeType0 y una dirección IP 182.17.34.52, en UD1 y fd: / dc1/r0.</span><span class="sxs-lookup"><span data-stu-id="b0a9c-114">hello example below adds a new node called VM5, with type NodeType0 and IP address 182.17.34.52, into UD1 and fd:/dc1/r0.</span></span> <span data-ttu-id="b0a9c-115">Hola *ExistingClusterConnectionEndPoint* ya está un extremo de conexión para un nodo de clúster existente de hello, que puede ser la dirección IP de Hola de *cualquier* nodo de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="b0a9c-115">hello *ExistingClusterConnectionEndPoint* is a connection endpoint for a node already in hello existing cluster, which can be hello IP address of *any* node in hello cluster.</span></span>

    ```
    .\AddNode.ps1 -NodeName VM5 -NodeType NodeType0 -NodeIPAddressorFQDN 182.17.34.52 -ExistingClientConnectionEndpoint 182.17.34.50:19000 -UpgradeDomain UD1 -FaultDomain fd:/dc1/r0 -AcceptEULA
    ```
    <span data-ttu-id="b0a9c-116">Una vez que el script de Hola finaliza su ejecución, puede comprobar si se ha agregado el nuevo nodo de hello ejecutando hello [ServiceFabricNode Get](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b0a9c-116">Once hello script finishes running, you can check if hello new node has been added by running hello [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) cmdlet.</span></span>

7. <span data-ttu-id="b0a9c-117">tooensure coherencia a través de varios nodos en clúster de hello, debe iniciar una actualización de la configuración.</span><span class="sxs-lookup"><span data-stu-id="b0a9c-117">tooensure consistency across different nodes in hello cluster, you must initiate a configuration upgrade.</span></span> <span data-ttu-id="b0a9c-118">Ejecutar [ServiceFabricClusterConfiguration Get](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) tooget Hola archivo de configuración más reciente y agregar Hola recién agregado nodo demasiado sección "Nodos".</span><span class="sxs-lookup"><span data-stu-id="b0a9c-118">Run [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) tooget hello latest configuration file and add hello newly added node too"Nodes" section.</span></span> <span data-ttu-id="b0a9c-119">También se recomienda tooalways tiene la configuración de clúster más reciente de hello disponible en caso de Hola que necesita un clúster con hello tooredploy misma configuración.</span><span class="sxs-lookup"><span data-stu-id="b0a9c-119">It is also recommended tooalways have hello latest cluster configuration available in hello case that you need tooredploy a cluster with hello same configuration.</span></span>

    ```
        {
            "nodeName": "vm5",
            "iPAddress": "182.17.34.52",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc1/r0",
            "upgradeDomain": "UD1"
        }
    ```
8. <span data-ttu-id="b0a9c-120">Ejecutar [ServiceFabricClusterConfigurationUpgrade inicio](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) actualización de hello toobegin.</span><span class="sxs-lookup"><span data-stu-id="b0a9c-120">Run [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) toobegin hello upgrade.</span></span>

    ```
    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>

    ```
    <span data-ttu-id="b0a9c-121">Puede supervisar el progreso de Hola de actualización de hello en el Explorador de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="b0a9c-121">You can monitor hello progress of hello upgrade on Service Fabric Explorer.</span></span> <span data-ttu-id="b0a9c-122">Como alternativa, puede ejecutar [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)</span><span class="sxs-lookup"><span data-stu-id="b0a9c-122">Alternatively, you can run [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)</span></span>

### <a name="add-nodes-tooclusters-configured-with-windows-security-using-gmsa"></a><span data-ttu-id="b0a9c-123">Agregar nodos tooclusters configurado con seguridad de Windows que usan gMSA.</span><span class="sxs-lookup"><span data-stu-id="b0a9c-123">Add nodes tooclusters configured with Windows Security using gMSA</span></span>
<span data-ttu-id="b0a9c-124">En clústeres configurados con cuentas de servicio administradas de grupo (gMSA)(https://technet.microsoft.com/library/hh831782.aspx), se puede agregar un nuevo nodo mediante una actualización de configuración:</span><span class="sxs-lookup"><span data-stu-id="b0a9c-124">For clusters configured with Group Managed Service Account(gMSA)(https://technet.microsoft.com/library/hh831782.aspx), a new node can be added using a configuration upgrade:</span></span>
1. <span data-ttu-id="b0a9c-125">Ejecutar [ServiceFabricClusterConfiguration Get](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) en cualquiera de los nodos existentes de hello tooget Hola archivo de configuración más reciente y agregar los detalles acerca del nuevo nodo de hello desea tooadd en sección Hola "nodos".</span><span class="sxs-lookup"><span data-stu-id="b0a9c-125">Run [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) on any of hello existing nodes tooget hello latest configuration file and add details about hello new node you want tooadd in hello "Nodes" section.</span></span> <span data-ttu-id="b0a9c-126">Asegúrese de que el nuevo nodo de hello forma parte del programa Hola misma cuenta administrada de grupo.</span><span class="sxs-lookup"><span data-stu-id="b0a9c-126">Make sure hello new node is part of hello same group managed account.</span></span> <span data-ttu-id="b0a9c-127">Esta cuenta debe ser un administrador en todos los equipos.</span><span class="sxs-lookup"><span data-stu-id="b0a9c-127">This account should be an Administrator on all machines.</span></span>

    ```
        {
            "nodeName": "vm5",
            "iPAddress": "182.17.34.52",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc1/r0",
            "upgradeDomain": "UD1"
        }
    ```
2. <span data-ttu-id="b0a9c-128">Ejecutar [ServiceFabricClusterConfigurationUpgrade inicio](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) actualización de hello toobegin.</span><span class="sxs-lookup"><span data-stu-id="b0a9c-128">Run [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) toobegin hello upgrade.</span></span>

    ```
    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>
    ```
    <span data-ttu-id="b0a9c-129">Puede supervisar el progreso de Hola de actualización de hello en el Explorador de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="b0a9c-129">You can monitor hello progress of hello upgrade on Service Fabric Explorer.</span></span> <span data-ttu-id="b0a9c-130">Como alternativa, puede ejecutar [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)</span><span class="sxs-lookup"><span data-stu-id="b0a9c-130">Alternatively, you can run [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)</span></span>

### <a name="add-node-types-tooyour-cluster"></a><span data-ttu-id="b0a9c-131">Agregar clúster de tooyour de tipos de nodo</span><span class="sxs-lookup"><span data-stu-id="b0a9c-131">Add node types tooyour cluster</span></span>
<span data-ttu-id="b0a9c-132">En Ordenar tooadd un nuevo tipo de nodo, modifique su configuración tooinclude Hola nuevo tipo de nodo en la sección "NodeTypes" en "Propiedades" y empezar a una configuración de actualización mediante [ServiceFabricClusterConfigurationUpgrade de inicio](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="b0a9c-132">In order tooadd a new node type, modify your configuration tooinclude hello new node type in "NodeTypes" section under "Properties" and begin a configuration upgrade using [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps).</span></span> <span data-ttu-id="b0a9c-133">Una vez completada la actualización de hello, puede agregar el nuevo clúster de nodos tooyour con este tipo de nodo.</span><span class="sxs-lookup"><span data-stu-id="b0a9c-133">Once hello upgrade completes, you can add new nodes tooyour cluster with this node type.</span></span>

## <a name="remove-nodes-from-your-cluster"></a><span data-ttu-id="b0a9c-134">Eliminación de nodos del clúster</span><span class="sxs-lookup"><span data-stu-id="b0a9c-134">Remove nodes from your cluster</span></span>
<span data-ttu-id="b0a9c-135">Puede quitarse un nodo de un clúster con una actualización de la configuración, en hello siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="b0a9c-135">A node can be removed from a cluster using a configuration upgrade, in hello following manner:</span></span>

1. <span data-ttu-id="b0a9c-136">Ejecutar [Get ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) archivo de configuración más reciente de tooget hello y *quitar* nodo Hola desde la sección "Nodos".</span><span class="sxs-lookup"><span data-stu-id="b0a9c-136">Run [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) tooget hello latest configuration file and *remove* hello node from "Nodes" section.</span></span>
<span data-ttu-id="b0a9c-137">Agregar Hola "NodesToBeRemoved" parámetro demasiado "el programa de instalación" sección dentro de la sección "FabricSettings".</span><span class="sxs-lookup"><span data-stu-id="b0a9c-137">Add hello "NodesToBeRemoved" parameter too"Setup" section inside "FabricSettings" section.</span></span> <span data-ttu-id="b0a9c-138">Hola "valor" debe ser una lista separada por comas de nombres de nodo de los nodos que necesitan toobe quitar.</span><span class="sxs-lookup"><span data-stu-id="b0a9c-138">hello "value" should be a comma separated list of node names of nodes that need toobe removed.</span></span>

    ```
         "fabricSettings": [
            {
            "name": "Setup",
            "parameters": [
                {
                "name": "FabricDataRoot",
                "value": "C:\\ProgramData\\SF"
                },
                {
                "name": "FabricLogRoot",
                "value": "C:\\ProgramData\\SF\\Log"
                },
                {
                "name": "NodesToBeRemoved",
                "value": "vm0, vm1"
                }
            ]
            }
        ]
    ```
2. <span data-ttu-id="b0a9c-139">Ejecutar [ServiceFabricClusterConfigurationUpgrade inicio](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) actualización de hello toobegin.</span><span class="sxs-lookup"><span data-stu-id="b0a9c-139">Run [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) toobegin hello upgrade.</span></span>

    ```
    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>

    ```
    <span data-ttu-id="b0a9c-140">Puede supervisar el progreso de Hola de actualización de hello en el Explorador de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="b0a9c-140">You can monitor hello progress of hello upgrade on Service Fabric Explorer.</span></span> <span data-ttu-id="b0a9c-141">Como alternativa, puede ejecutar [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)</span><span class="sxs-lookup"><span data-stu-id="b0a9c-141">Alternatively, you can run [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)</span></span>

> [!NOTE]
> <span data-ttu-id="b0a9c-142">La eliminación de nodos puede iniciar varias actualizaciones.</span><span class="sxs-lookup"><span data-stu-id="b0a9c-142">Removal of nodes may initiate multiple upgrades.</span></span> <span data-ttu-id="b0a9c-143">Algunos nodos se marcan con `IsSeedNode=”true”` etiqueta y se pueden identificar consultando clúster Hola manifiesto mediante `Get-ServiceFabricClusterManifest`.</span><span class="sxs-lookup"><span data-stu-id="b0a9c-143">Some nodes are marked with `IsSeedNode=”true”` tag and can be identified by querying hello cluster manifest using `Get-ServiceFabricClusterManifest`.</span></span> <span data-ttu-id="b0a9c-144">Eliminación de estos nodos puede tardar más que otros debido a que los nodos de valor de inicialización de hello tendrán toobe mueven en tales escenarios.</span><span class="sxs-lookup"><span data-stu-id="b0a9c-144">Removal of such nodes may take longer than others since hello seed nodes will have toobe moved around in such scenarios.</span></span> <span data-ttu-id="b0a9c-145">clúster de Hello debe mantener un mínimo de 3 nodos de tipo de nodo principal.</span><span class="sxs-lookup"><span data-stu-id="b0a9c-145">hello cluster must maintain a minimum of 3 primary node type nodes.</span></span>
> 
> 

### <a name="remove-node-types-from-your-cluster"></a><span data-ttu-id="b0a9c-146">Eliminación de tipos de nodo del clúster</span><span class="sxs-lookup"><span data-stu-id="b0a9c-146">Remove node types from your cluster</span></span>
<span data-ttu-id="b0a9c-147">Antes de quitar un tipo de nodo, compruebe de nuevo si hay nodos que hacen referencia a tipo de nodo de Hola.</span><span class="sxs-lookup"><span data-stu-id="b0a9c-147">Before removing a node type, please double check if there are any nodes referencing hello node type.</span></span> <span data-ttu-id="b0a9c-148">Quite estos nodos antes de quitar el tipo de nodo correspondiente Hola.</span><span class="sxs-lookup"><span data-stu-id="b0a9c-148">Remove these nodes before removing hello corresponding node type.</span></span> <span data-ttu-id="b0a9c-149">Una vez que se quitan todos los nodos correspondientes, puede quitar Hola NodeType de configuración de clúster de Hola y empezar a una configuración de actualización mediante [ServiceFabricClusterConfigurationUpgrade inicio](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="b0a9c-149">Once all corresponding nodes are removed, you can remove hello NodeType from hello cluster configuration and begin a configuration upgrade using [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps).</span></span>


### <a name="replace-primary-nodes-of-your-cluster"></a><span data-ttu-id="b0a9c-150">Sustitución de los nodos principales del clúster</span><span class="sxs-lookup"><span data-stu-id="b0a9c-150">Replace primary nodes of your cluster</span></span>
<span data-ttu-id="b0a9c-151">reemplazo de Hola de nodos principales debe ser realizada un nodo tras otra, en lugar de quitar y, a continuación, agregarlos en lotes.</span><span class="sxs-lookup"><span data-stu-id="b0a9c-151">hello replacement of primary nodes should be performed one node after another, instead of removing and then adding in batches.</span></span>


## <a name="next-steps"></a><span data-ttu-id="b0a9c-152">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b0a9c-152">Next steps</span></span>
* [<span data-ttu-id="b0a9c-153">Opciones de configuración de clústeres de Windows independientes</span><span class="sxs-lookup"><span data-stu-id="b0a9c-153">Configuration settings for standalone Windows cluster</span></span>](service-fabric-cluster-manifest.md)
* [<span data-ttu-id="b0a9c-154">Protección de un clúster de Windows independiente mediante certificados</span><span class="sxs-lookup"><span data-stu-id="b0a9c-154">Secure a standalone cluster on Windows using X509 certificates</span></span>](service-fabric-windows-cluster-x509-security.md)
* [<span data-ttu-id="b0a9c-155">Creación de un clúster de Service Fabric independiente con VM de Azure con Windows</span><span class="sxs-lookup"><span data-stu-id="b0a9c-155">Create a standalone Service Fabric cluster with Azure VMs running Windows</span></span>](service-fabric-cluster-creation-with-windows-azure-vms.md)

