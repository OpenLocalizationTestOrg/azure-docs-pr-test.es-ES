---
title: "Incorporación o eliminación de un clúster de Service Fabric independiente | Microsoft Docs"
description: "Obtenga información sobre cómo agregar o quitar nodos en un clúster de Azure Service Fabric en una máquina virtual o física con Windows Server, la que podría estar en el entorno local o en alguna nube."
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
ms.openlocfilehash: 9c6035e97de38ff63ef074109afd9f3c7484f828
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="add-or-remove-nodes-to-a-standalone-service-fabric-cluster-running-on-windows-server"></a><span data-ttu-id="2d490-103">Incorporación o eliminación de nodos de un clúster de Service Fabric independiente con Windows Server</span><span class="sxs-lookup"><span data-stu-id="2d490-103">Add or remove nodes to a standalone Service Fabric cluster running on Windows Server</span></span>
<span data-ttu-id="2d490-104">Una vez que [cree su clúster de Service Fabric independiente en máquinas de Windows Server](service-fabric-cluster-creation-for-windows-server.md), puede que las necesidades empresariales cambien y que deba agregar o eliminar nodos del clúster.</span><span class="sxs-lookup"><span data-stu-id="2d490-104">After you have [created your standalone Service Fabric cluster on Windows Server machines](service-fabric-cluster-creation-for-windows-server.md), your business needs may change and you might need to add or remove nodes to your cluster.</span></span> <span data-ttu-id="2d490-105">En este artículo, se muestran los pasos detallados para llevarlo a cabo.</span><span class="sxs-lookup"><span data-stu-id="2d490-105">This article provides detailed steps to achieve this.</span></span> <span data-ttu-id="2d490-106">Tenga en cuenta que no se permite agregar o eliminar nodos en los clústeres de desarrollo local.</span><span class="sxs-lookup"><span data-stu-id="2d490-106">Please note that add/remove node functionality is not supported in local development clusters.</span></span>

## <a name="add-nodes-to-your-cluster"></a><span data-ttu-id="2d490-107">Incorporación de nodos al clúster</span><span class="sxs-lookup"><span data-stu-id="2d490-107">Add nodes to your cluster</span></span>
1. <span data-ttu-id="2d490-108">Prepare la máquina virtual o la máquina que desea agregar al clúster con los pasos que se indican en la sección [Preparación de las máquinas para cumplir los requisitos previos de la implementación del clúster](service-fabric-cluster-creation-for-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="2d490-108">Prepare the VM/machine you want to add to your cluster by following the steps mentioned in the [Prepare the machines to meet the prerequisites for cluster deployment](service-fabric-cluster-creation-for-windows-server.md) section</span></span>
2. <span data-ttu-id="2d490-109">Identifique a qué dominio de error y de actualización va a agregar esta máquina o VM.</span><span class="sxs-lookup"><span data-stu-id="2d490-109">Identify which fault domain and upgrade domain you are going to add this VM/machine to</span></span>
3. <span data-ttu-id="2d490-110">Abra una conexión de Escritorio remoto (RDP) en la máquina o VM que desea agregar al clúster.</span><span class="sxs-lookup"><span data-stu-id="2d490-110">Remote desktop (RDP) into the VM/machine that you want to add to the cluster</span></span>
4. <span data-ttu-id="2d490-111">Copie o [descargue el paquete independiente de Service Fabric para Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690) en esta máquina o VM y descomprímalo.</span><span class="sxs-lookup"><span data-stu-id="2d490-111">Copy or [download the standalone package for Service Fabric for Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690) to the VM/machine and unzip the package</span></span>
5. <span data-ttu-id="2d490-112">Ejecute PowerShell con privilegios elevados y vaya a la ubicación del paquete descomprimido.</span><span class="sxs-lookup"><span data-stu-id="2d490-112">Run Powershell with elevated privileges, and navigate to the location of the unzipped package</span></span>
6. <span data-ttu-id="2d490-113">Ejecute el script *AddNode.ps1* con los parámetros que describen el nuevo nodo que se va a agregar.</span><span class="sxs-lookup"><span data-stu-id="2d490-113">Run the *AddNode.ps1* script with the parameters describing the new node to add.</span></span> <span data-ttu-id="2d490-114">En el ejemplo siguiente se agrega un nuevo nodo denominado VM5, con el tipo NodeType0 y la dirección IP 182.17.34.52, en UD1 y fd:/dc1/r0.</span><span class="sxs-lookup"><span data-stu-id="2d490-114">The example below adds a new node called VM5, with type NodeType0 and IP address 182.17.34.52, into UD1 and fd:/dc1/r0.</span></span> <span data-ttu-id="2d490-115">*ExistingClusterConnectionEndPoint* es un punto de conexión para un nodo que ya está presente en el clúster existente, puede ser la dirección IP de *cualquier* nodo del clúster.</span><span class="sxs-lookup"><span data-stu-id="2d490-115">The *ExistingClusterConnectionEndPoint* is a connection endpoint for a node already in the existing cluster, which can be the IP address of *any* node in the cluster.</span></span>

    ```
    .\AddNode.ps1 -NodeName VM5 -NodeType NodeType0 -NodeIPAddressorFQDN 182.17.34.52 -ExistingClientConnectionEndpoint 182.17.34.50:19000 -UpgradeDomain UD1 -FaultDomain fd:/dc1/r0 -AcceptEULA
    ```
    <span data-ttu-id="2d490-116">Una vez que finalice el script, puede comprobar si se ha agregado el nuevo nodo mediante la ejecución del cmdlet [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="2d490-116">Once the script finishes running, you can check if the new node has been added by running the [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) cmdlet.</span></span>

7. <span data-ttu-id="2d490-117">Para garantizar la coherencia entre los distintos nodos del clúster, debe iniciar una actualización de la configuración.</span><span class="sxs-lookup"><span data-stu-id="2d490-117">To ensure consistency across different nodes in the cluster, you must initiate a configuration upgrade.</span></span> <span data-ttu-id="2d490-118">Ejecute [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) para obtener el archivo de configuración más reciente y agregar el nodo recién agregado a la sección "Nodes".</span><span class="sxs-lookup"><span data-stu-id="2d490-118">Run [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) to get the latest configuration file and add the newly added node to "Nodes" section.</span></span> <span data-ttu-id="2d490-119">También se recomienda tener siempre la configuración del clúster más reciente disponible en el caso de que deba volver a implementar un clúster con la misma configuración.</span><span class="sxs-lookup"><span data-stu-id="2d490-119">It is also recommended to always have the latest cluster configuration available in the case that you need to redploy a cluster with the same configuration.</span></span>

    ```
        {
            "nodeName": "vm5",
            "iPAddress": "182.17.34.52",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc1/r0",
            "upgradeDomain": "UD1"
        }
    ```
8. <span data-ttu-id="2d490-120">Ejecute [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) para comenzar la actualización.</span><span class="sxs-lookup"><span data-stu-id="2d490-120">Run [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) to begin the upgrade.</span></span>

    ```
    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path to Configuration File>

    ```
    <span data-ttu-id="2d490-121">Puede supervisar el progreso de la actualización en Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="2d490-121">You can monitor the progress of the upgrade on Service Fabric Explorer.</span></span> <span data-ttu-id="2d490-122">Como alternativa, puede ejecutar [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)</span><span class="sxs-lookup"><span data-stu-id="2d490-122">Alternatively, you can run [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)</span></span>

### <a name="add-nodes-to-clusters-configured-with-windows-security-using-gmsa"></a><span data-ttu-id="2d490-123">Agregar nodos a clústeres configurados con seguridad de Windows mediante gMSA</span><span class="sxs-lookup"><span data-stu-id="2d490-123">Add nodes to clusters configured with Windows Security using gMSA</span></span>
<span data-ttu-id="2d490-124">En clústeres configurados con cuentas de servicio administradas de grupo (gMSA)(https://technet.microsoft.com/library/hh831782.aspx), se puede agregar un nuevo nodo mediante una actualización de configuración:</span><span class="sxs-lookup"><span data-stu-id="2d490-124">For clusters configured with Group Managed Service Account(gMSA)(https://technet.microsoft.com/library/hh831782.aspx), a new node can be added using a configuration upgrade:</span></span>
1. <span data-ttu-id="2d490-125">Ejecute [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) en cualquiera de los nodos existentes para obtener el archivo de configuración más reciente y agregue los detalles del nodo que desea agregar en la sección "Nodes".</span><span class="sxs-lookup"><span data-stu-id="2d490-125">Run [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) on any of the existing nodes to get the latest configuration file and add details about the new node you want to add in the "Nodes" section.</span></span> <span data-ttu-id="2d490-126">Asegúrese de que el nuevo nodo forma parte de la misma cuenta administrada de grupo.</span><span class="sxs-lookup"><span data-stu-id="2d490-126">Make sure the new node is part of the same group managed account.</span></span> <span data-ttu-id="2d490-127">Esta cuenta debe ser un administrador en todos los equipos.</span><span class="sxs-lookup"><span data-stu-id="2d490-127">This account should be an Administrator on all machines.</span></span>

    ```
        {
            "nodeName": "vm5",
            "iPAddress": "182.17.34.52",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc1/r0",
            "upgradeDomain": "UD1"
        }
    ```
2. <span data-ttu-id="2d490-128">Ejecute [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) para comenzar la actualización.</span><span class="sxs-lookup"><span data-stu-id="2d490-128">Run [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) to begin the upgrade.</span></span>

    ```
    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path to Configuration File>
    ```
    <span data-ttu-id="2d490-129">Puede supervisar el progreso de la actualización en Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="2d490-129">You can monitor the progress of the upgrade on Service Fabric Explorer.</span></span> <span data-ttu-id="2d490-130">Como alternativa, puede ejecutar [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)</span><span class="sxs-lookup"><span data-stu-id="2d490-130">Alternatively, you can run [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)</span></span>

### <a name="add-node-types-to-your-cluster"></a><span data-ttu-id="2d490-131">Agregar tipos de nodo al clúster</span><span class="sxs-lookup"><span data-stu-id="2d490-131">Add node types to your cluster</span></span>
<span data-ttu-id="2d490-132">Para agregar un nuevo tipo de nodo, modifique la configuración para incluir el nuevo tipo de nodo en la sección "NodeTypes" en "Properties" e inicie una actualización de configuración con [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="2d490-132">In order to add a new node type, modify your configuration to include the new node type in "NodeTypes" section under "Properties" and begin a configuration upgrade using [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps).</span></span> <span data-ttu-id="2d490-133">Una vez completada la actualización, puede agregar nuevos nodos al clúster con este tipo de nodo.</span><span class="sxs-lookup"><span data-stu-id="2d490-133">Once the upgrade completes, you can add new nodes to your cluster with this node type.</span></span>

## <a name="remove-nodes-from-your-cluster"></a><span data-ttu-id="2d490-134">Eliminación de nodos del clúster</span><span class="sxs-lookup"><span data-stu-id="2d490-134">Remove nodes from your cluster</span></span>
<span data-ttu-id="2d490-135">Es posible eliminar un nodo de un clúster con una actualización de la configuración de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="2d490-135">A node can be removed from a cluster using a configuration upgrade, in the following manner:</span></span>

1. <span data-ttu-id="2d490-136">Ejecute [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) para obtener el archivo de configuración más reciente y *elimine* el nodo de la sección "Nodes".</span><span class="sxs-lookup"><span data-stu-id="2d490-136">Run [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) to get the latest configuration file and *remove* the node from "Nodes" section.</span></span>
<span data-ttu-id="2d490-137">Agregue el parámetro "NodesToBeRemoved" a la sección "Setup" dentro de la sección "FabricSettings".</span><span class="sxs-lookup"><span data-stu-id="2d490-137">Add the "NodesToBeRemoved" parameter to "Setup" section inside "FabricSettings" section.</span></span> <span data-ttu-id="2d490-138">El "valor" debe ser una lista separada por comas de nombres de nodo de los nodos que deben eliminarse.</span><span class="sxs-lookup"><span data-stu-id="2d490-138">The "value" should be a comma separated list of node names of nodes that need to be removed.</span></span>

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
2. <span data-ttu-id="2d490-139">Ejecute [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) para comenzar la actualización.</span><span class="sxs-lookup"><span data-stu-id="2d490-139">Run [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) to begin the upgrade.</span></span>

    ```
    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path to Configuration File>

    ```
    <span data-ttu-id="2d490-140">Puede supervisar el progreso de la actualización en Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="2d490-140">You can monitor the progress of the upgrade on Service Fabric Explorer.</span></span> <span data-ttu-id="2d490-141">Como alternativa, puede ejecutar [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)</span><span class="sxs-lookup"><span data-stu-id="2d490-141">Alternatively, you can run [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)</span></span>

> [!NOTE]
> <span data-ttu-id="2d490-142">La eliminación de nodos puede iniciar varias actualizaciones.</span><span class="sxs-lookup"><span data-stu-id="2d490-142">Removal of nodes may initiate multiple upgrades.</span></span> <span data-ttu-id="2d490-143">Algunos nodos están marcados con la etiqueta `IsSeedNode=”true”` y se pueden identificar consultando el manifiesto del clúster mediante `Get-ServiceFabricClusterManifest`.</span><span class="sxs-lookup"><span data-stu-id="2d490-143">Some nodes are marked with `IsSeedNode=”true”` tag and can be identified by querying the cluster manifest using `Get-ServiceFabricClusterManifest`.</span></span> <span data-ttu-id="2d490-144">La eliminación de estos nodos puede tardar más que la de otros, ya que se tendrán que mover los nodos de inicialización en estos escenarios.</span><span class="sxs-lookup"><span data-stu-id="2d490-144">Removal of such nodes may take longer than others since the seed nodes will have to be moved around in such scenarios.</span></span> <span data-ttu-id="2d490-145">El clúster debe tener un mínimo de 3 nodos de tipo nodo primario.</span><span class="sxs-lookup"><span data-stu-id="2d490-145">The cluster must maintain a minimum of 3 primary node type nodes.</span></span>
> 
> 

### <a name="remove-node-types-from-your-cluster"></a><span data-ttu-id="2d490-146">Eliminación de tipos de nodo del clúster</span><span class="sxs-lookup"><span data-stu-id="2d490-146">Remove node types from your cluster</span></span>
<span data-ttu-id="2d490-147">Antes de eliminar un tipo de nodo, compruebe de nuevo si no hay algún nodo que haga referencia a dicho tipo.</span><span class="sxs-lookup"><span data-stu-id="2d490-147">Before removing a node type, please double check if there are any nodes referencing the node type.</span></span> <span data-ttu-id="2d490-148">Elimine estos nodos antes de quitar el tipo de nodo correspondiente.</span><span class="sxs-lookup"><span data-stu-id="2d490-148">Remove these nodes before removing the corresponding node type.</span></span> <span data-ttu-id="2d490-149">Una vez se han eliminado todos los nodos correspondientes, puede eliminar el valor de NodeType de la configuración del clúster y comenzar una actualización de la configuración mediante [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="2d490-149">Once all corresponding nodes are removed, you can remove the NodeType from the cluster configuration and begin a configuration upgrade using [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps).</span></span>


### <a name="replace-primary-nodes-of-your-cluster"></a><span data-ttu-id="2d490-150">Sustitución de los nodos principales del clúster</span><span class="sxs-lookup"><span data-stu-id="2d490-150">Replace primary nodes of your cluster</span></span>
<span data-ttu-id="2d490-151">Los nodos principales se deben sustituir uno por uno, en lugar de quitarlos y agregarlos de forma masiva.</span><span class="sxs-lookup"><span data-stu-id="2d490-151">The replacement of primary nodes should be performed one node after another, instead of removing and then adding in batches.</span></span>


## <a name="next-steps"></a><span data-ttu-id="2d490-152">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2d490-152">Next steps</span></span>
* [<span data-ttu-id="2d490-153">Opciones de configuración de clústeres de Windows independientes</span><span class="sxs-lookup"><span data-stu-id="2d490-153">Configuration settings for standalone Windows cluster</span></span>](service-fabric-cluster-manifest.md)
* [<span data-ttu-id="2d490-154">Protección de un clúster de Windows independiente mediante certificados</span><span class="sxs-lookup"><span data-stu-id="2d490-154">Secure a standalone cluster on Windows using X509 certificates</span></span>](service-fabric-windows-cluster-x509-security.md)
* [<span data-ttu-id="2d490-155">Creación de un clúster de Service Fabric independiente con VM de Azure con Windows</span><span class="sxs-lookup"><span data-stu-id="2d490-155">Create a standalone Service Fabric cluster with Azure VMs running Windows</span></span>](service-fabric-cluster-creation-with-windows-azure-vms.md)

