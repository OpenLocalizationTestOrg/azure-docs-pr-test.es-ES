---
title: "Tipos de nodos de Service Fabric y conjuntos de escalado de máquinas virtuales | Microsoft Docs"
description: "Describe cómo se relacionan los tipos de nodos de Service Fabric con los conjuntos de escalado de máquinas virtuales y cómo conectarse de forma remota a una instancia de conjunto de escalado de máquinas virtuales o un nodo de clúster."
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: 5441e7e0-d842-4398-b060-8c9d34b07c48
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/05/2017
ms.author: chackdan
ms.openlocfilehash: 3b1a22bb3653abb68fc73645ad2cb623fabc7736
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="the-relationship-between-service-fabric-node-types-and-virtual-machine-scale-sets"></a><span data-ttu-id="ff9dd-103">Relación entre los tipos de nodos de Service Fabric y los conjuntos de escalado de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="ff9dd-103">The relationship between Service Fabric node types and Virtual Machine Scale Sets</span></span>
<span data-ttu-id="ff9dd-104">Los conjuntos de escalado de máquinas virtuales son un recurso de proceso de Azure que se puede usar para implementar y administrar una colección de máquinas virtuales de forma conjunta.</span><span class="sxs-lookup"><span data-stu-id="ff9dd-104">Virtual Machine Scale Sets are an Azure Compute resource you can use to deploy and manage a collection of virtual machines as a set.</span></span> <span data-ttu-id="ff9dd-105">Cada tipo de nodo que se define en un clúster de Service Fabric está configurado como un conjunto de escalado de VM independiente.</span><span class="sxs-lookup"><span data-stu-id="ff9dd-105">Every node type that is defined in a Service Fabric cluster is set up as a separate VM Scale Set.</span></span> <span data-ttu-id="ff9dd-106">Cada tipo de nodo se puede escalar o reducir verticalmente de forma independiente. Cada uno tiene diferentes conjuntos de puertos abiertos y puede tener distintas métricas de capacidad.</span><span class="sxs-lookup"><span data-stu-id="ff9dd-106">Each node type can then be scaled up or down independently, have different sets of ports open, and can have different capacity metrics.</span></span>

<span data-ttu-id="ff9dd-107">En la siguiente captura de pantalla, se muestra un clúster que tiene dos tipos de nodos: front-end y back-end.</span><span class="sxs-lookup"><span data-stu-id="ff9dd-107">The following screen shot shows a cluster that has two node types: FrontEnd and BackEnd.</span></span>  <span data-ttu-id="ff9dd-108">A su vez, cada tipo de nodo tiene cinco nodos.</span><span class="sxs-lookup"><span data-stu-id="ff9dd-108">Each node type has five nodes each.</span></span>

![Captura de pantalla de un clúster que tiene dos tipos de nodos][NodeTypes]

## <a name="mapping-vm-scale-set-instances-to-nodes"></a><span data-ttu-id="ff9dd-110">Asignación de instancias de conjuntos de escalado de máquinas virtuales a los nodos</span><span class="sxs-lookup"><span data-stu-id="ff9dd-110">Mapping VM Scale Set instances to nodes</span></span>
<span data-ttu-id="ff9dd-111">Como se ha indicado anteriormente, las instancias de conjuntos de escalado de máquinas virtuales comienzan por la instancia 0 y van aumentando.</span><span class="sxs-lookup"><span data-stu-id="ff9dd-111">As you can see above, the VM Scale Set instances start from instance 0 and then goes up.</span></span> <span data-ttu-id="ff9dd-112">La numeración se refleja en los nombres.</span><span class="sxs-lookup"><span data-stu-id="ff9dd-112">The numbering is reflected in the names.</span></span> <span data-ttu-id="ff9dd-113">Por ejemplo, BackEnd_0 es la instancia 0 del conjunto de escalado de máquinas virtuales de back-end.</span><span class="sxs-lookup"><span data-stu-id="ff9dd-113">For example, BackEnd_0 is instance 0 of the BackEnd VM Scale Set.</span></span> <span data-ttu-id="ff9dd-114">En concreto, este conjunto de escalado de máquinas virtuales tiene cinco instancias, denominadas BackEnd_0, BackEnd_1, BackEnd_2, BackEnd_3 y BackEnd_4.</span><span class="sxs-lookup"><span data-stu-id="ff9dd-114">This particular VM Scale Set has five instances, named BackEnd_0, BackEnd_1, BackEnd_2, BackEnd_3 and BackEnd_4.</span></span>

<span data-ttu-id="ff9dd-115">Al escalar verticalmente un conjunto de escalado de máquinas virtuales, se crea una nueva instancia.</span><span class="sxs-lookup"><span data-stu-id="ff9dd-115">When you scale up a VM Scale Set a new instance is created.</span></span> <span data-ttu-id="ff9dd-116">El nuevo nombre de instancia de conjunto de escalado de máquinas virtuales será normalmente el nombre del conjunto de escalado de máquinas virtuales seguido del número de instancia.</span><span class="sxs-lookup"><span data-stu-id="ff9dd-116">The new VM Scale Set instance name will typically be the VM Scale Set name + the next instance number.</span></span> <span data-ttu-id="ff9dd-117">En nuestro ejemplo, es BackEnd_5.</span><span class="sxs-lookup"><span data-stu-id="ff9dd-117">In our example, it is BackEnd_5.</span></span>

## <a name="mapping-vm-scale-set-load-balancers-to-each-node-typevm-scale-set"></a><span data-ttu-id="ff9dd-118">Asignación de equilibradores de carga de conjunto de escalado de máquinas virtuales a cada tipo de nodo o conjunto de escalado de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="ff9dd-118">Mapping VM scale set load balancers to each node type/VM Scale Set</span></span>
<span data-ttu-id="ff9dd-119">Si ha implementado el clúster desde el portal o ha usado la plantilla de Azure Resource Manager que le hemos proporcionado, al mostrar una lista de todos los recursos incluidos en un grupo de recursos, verá los equilibradores de carga para cada conjunto de escalado de VM o tipo de nodo.</span><span class="sxs-lookup"><span data-stu-id="ff9dd-119">If you have deployed your cluster from the portal or have used the sample Resource Manager template that we provided, then when you get a list of all resources under a Resource Group then you will see the load balancers for each VM Scale Set or node type.</span></span>

<span data-ttu-id="ff9dd-120">El nombre sería algo parecido a: **LB-&lt;Nombre del tipo de nodo&gt;**.</span><span class="sxs-lookup"><span data-stu-id="ff9dd-120">The name would something like: **LB-&lt;NodeType name&gt;**.</span></span> <span data-ttu-id="ff9dd-121">Por ejemplo, LB-sfcluster4doc-0, como se muestra en esta captura de pantalla:</span><span class="sxs-lookup"><span data-stu-id="ff9dd-121">For example, LB-sfcluster4doc-0, as shown in this screenshot:</span></span>

![Recursos][Resources]

## <a name="remote-connect-to-a-vm-scale-set-instance-or-a-cluster-node"></a><span data-ttu-id="ff9dd-123">Conexión remota a una instancia de conjunto de escalado de máquinas virtuales o un nodo de clúster</span><span class="sxs-lookup"><span data-stu-id="ff9dd-123">Remote connect to a VM Scale Set instance or a cluster node</span></span>
<span data-ttu-id="ff9dd-124">Cada tipo de nodo que se define en un clúster está configurado como un conjunto de escalado de VM independiente.</span><span class="sxs-lookup"><span data-stu-id="ff9dd-124">Every Node type that is defined in a cluster is set up as a separate VM Scale Set.</span></span>  <span data-ttu-id="ff9dd-125">Esto significa que los tipos de nodos se pueden escalar o reducir verticalmente de forma independiente y que pueden estar formados por diferentes SKU de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="ff9dd-125">That means the node types can be scaled up or down independently and can be made of different VM SKUs.</span></span> <span data-ttu-id="ff9dd-126">A diferencia de las máquinas virtuales de instancia única, las instancias de conjunto de escalado de máquinas virtuales no obtienen una dirección IP virtual por sí mismas.</span><span class="sxs-lookup"><span data-stu-id="ff9dd-126">Unlike single instance VMs, the VM Scale Set instances do not get a virtual IP address of their own.</span></span> <span data-ttu-id="ff9dd-127">Por lo que puede ser un poco complicado si desea obtener una dirección IP y un puerto que pueda usar para conectarse de manera remota a una instancia específica.</span><span class="sxs-lookup"><span data-stu-id="ff9dd-127">So it can be a bit challenging when you are looking for an IP address and port that you can use to remote connect to a specific instance.</span></span>

<span data-ttu-id="ff9dd-128">Estos son los pasos que puede seguir para detectarlos.</span><span class="sxs-lookup"><span data-stu-id="ff9dd-128">Here are the steps you can follow to discover them.</span></span>

### <a name="step-1-find-out-the-virtual-ip-address-for-the-node-type-and-then-inbound-nat-rules-for-rdp"></a><span data-ttu-id="ff9dd-129">Paso 1: Averiguar la dirección IP virtual para el tipo de nodo y, a continuación, las reglas NAT de entrada para RDP</span><span class="sxs-lookup"><span data-stu-id="ff9dd-129">Step 1: Find out the virtual IP address for the node type and then Inbound NAT rules for RDP</span></span>
<span data-ttu-id="ff9dd-130">Para conseguirlo, debe obtener los valores de las reglas NAT de entrada que se especificaron como parte de la definición de recursos para **Microsoft.Network/loadBalancers**.</span><span class="sxs-lookup"><span data-stu-id="ff9dd-130">In order to get that, you need to get the inbound NAT rules values that were defined as a part of the resource definition for **Microsoft.Network/loadBalancers**.</span></span>

<span data-ttu-id="ff9dd-131">En el portal, vaya a la hoja del equilibrador de carga y, a continuación, acceda a **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="ff9dd-131">In the portal, navigate to the Load balancer blade and then **Settings**.</span></span>

![LBBlade][LBBlade]

<span data-ttu-id="ff9dd-133">En **Configuración**, haga clic en **Reglas NAT de entrada**.</span><span class="sxs-lookup"><span data-stu-id="ff9dd-133">In **Settings**, click on **Inbound NAT rules**.</span></span> <span data-ttu-id="ff9dd-134">Aquí verá la dirección IP y el puerto que puede usar para conectarse de forma remota a la primera instancia de conjunto de escalado de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="ff9dd-134">This now gives you the IP address and port that you can use to remote connect to the first VM Scale Set instance.</span></span> <span data-ttu-id="ff9dd-135">En la captura de pantalla siguiente, los valores son **104.42.106.156** y **3389**.</span><span class="sxs-lookup"><span data-stu-id="ff9dd-135">In the screenshot below, it is **104.42.106.156** and **3389**</span></span>

![NATRules][NATRules]

### <a name="step-2-find-out-the-port-that-you-can-use-to-remote-connect-to-the-specific-vm-scale-set-instancenode"></a><span data-ttu-id="ff9dd-137">Paso 2: Buscar el puerto que puede usar para conectarse de forma remota al nodo o a la instancia específica del conjunto de escalado de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="ff9dd-137">Step 2: Find out the port that you can use to remote connect to the specific VM Scale Set instance/node</span></span>
<span data-ttu-id="ff9dd-138">Anteriormente en este documento, se describió la forma de asignar instancias de conjunto de escalado de máquinas virtuales a los nodos.</span><span class="sxs-lookup"><span data-stu-id="ff9dd-138">Earlier in this document, I talked about how the VM Scale Set instances map to the nodes.</span></span> <span data-ttu-id="ff9dd-139">Usaremos ese procedimiento para averiguar el puerto exacto.</span><span class="sxs-lookup"><span data-stu-id="ff9dd-139">We will use that to figure out the exact port.</span></span>

<span data-ttu-id="ff9dd-140">Los puertos se asignan en orden ascendente de la instancia del conjunto de escalado de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="ff9dd-140">The ports are allocated in ascending order of the VM Scale Set instance.</span></span> <span data-ttu-id="ff9dd-141">Así que en mi ejemplo del tipo de nodo de front-end, los puertos de cada una de las cinco instancias son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="ff9dd-141">so in my example for the FrontEnd node type, the ports for each of the five instances are the following.</span></span> <span data-ttu-id="ff9dd-142">Ahora debe realizar la misma asignación para la instancia del conjunto de escalado de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="ff9dd-142">you now need to do the same mapping for your VM Scale Set instance.</span></span>

| <span data-ttu-id="ff9dd-143">**Instancia de conjunto de escalado de VM**</span><span class="sxs-lookup"><span data-stu-id="ff9dd-143">**VM Scale Set Instance**</span></span> | <span data-ttu-id="ff9dd-144">**Puerto**</span><span class="sxs-lookup"><span data-stu-id="ff9dd-144">**Port**</span></span> |
| --- | --- |
| <span data-ttu-id="ff9dd-145">FrontEnd_0</span><span class="sxs-lookup"><span data-stu-id="ff9dd-145">FrontEnd_0</span></span> |<span data-ttu-id="ff9dd-146">3389</span><span class="sxs-lookup"><span data-stu-id="ff9dd-146">3389</span></span> |
| <span data-ttu-id="ff9dd-147">FrontEnd_1</span><span class="sxs-lookup"><span data-stu-id="ff9dd-147">FrontEnd_1</span></span> |<span data-ttu-id="ff9dd-148">3390</span><span class="sxs-lookup"><span data-stu-id="ff9dd-148">3390</span></span> |
| <span data-ttu-id="ff9dd-149">FrontEnd_2</span><span class="sxs-lookup"><span data-stu-id="ff9dd-149">FrontEnd_2</span></span> |<span data-ttu-id="ff9dd-150">3391</span><span class="sxs-lookup"><span data-stu-id="ff9dd-150">3391</span></span> |
| <span data-ttu-id="ff9dd-151">FrontEnd_3</span><span class="sxs-lookup"><span data-stu-id="ff9dd-151">FrontEnd_3</span></span> |<span data-ttu-id="ff9dd-152">3392</span><span class="sxs-lookup"><span data-stu-id="ff9dd-152">3392</span></span> |
| <span data-ttu-id="ff9dd-153">FrontEnd_4</span><span class="sxs-lookup"><span data-stu-id="ff9dd-153">FrontEnd_4</span></span> |<span data-ttu-id="ff9dd-154">3393</span><span class="sxs-lookup"><span data-stu-id="ff9dd-154">3393</span></span> |
| <span data-ttu-id="ff9dd-155">FrontEnd_5</span><span class="sxs-lookup"><span data-stu-id="ff9dd-155">FrontEnd_5</span></span> |<span data-ttu-id="ff9dd-156">3394</span><span class="sxs-lookup"><span data-stu-id="ff9dd-156">3394</span></span> |

### <a name="step-3-remote-connect-to-the-specific-vm-scale-set-instance"></a><span data-ttu-id="ff9dd-157">Paso 3: Conectarse remotamente a la instancia específica del conjunto de escalado de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="ff9dd-157">Step 3: Remote connect to the specific VM Scale Set instance</span></span>
<span data-ttu-id="ff9dd-158">En la siguiente captura de pantalla, se usa la conexión a escritorio remoto para conectarse a FrontEnd_1:</span><span class="sxs-lookup"><span data-stu-id="ff9dd-158">In the screenshot below I use Remote Desktop Connection to connect to the FrontEnd_1:</span></span>

![RDP][RDP]

## <a name="how-to-change-the-rdp-port-range-values"></a><span data-ttu-id="ff9dd-160">Cómo cambiar los valores del intervalo de puertos RDP</span><span class="sxs-lookup"><span data-stu-id="ff9dd-160">How to change the RDP port range values</span></span>
### <a name="before-cluster-deployment"></a><span data-ttu-id="ff9dd-161">Antes de la implementación del clúster</span><span class="sxs-lookup"><span data-stu-id="ff9dd-161">Before cluster deployment</span></span>
<span data-ttu-id="ff9dd-162">Cuando se configura el clúster mediante una plantilla de Azure Resource Manager, se puede especificar el intervalo en **inboundNatPools**.</span><span class="sxs-lookup"><span data-stu-id="ff9dd-162">When you are setting up the cluster using an Resource Manager template, you can specify the range in the **inboundNatPools**.</span></span>

<span data-ttu-id="ff9dd-163">Acceda a la definición de recursos para **Microsoft.Network/loadBalancers**.</span><span class="sxs-lookup"><span data-stu-id="ff9dd-163">Go to the resource definition for **Microsoft.Network/loadBalancers**.</span></span> <span data-ttu-id="ff9dd-164">Ahí encontrará la descripción de **inboundNatPools**.</span><span class="sxs-lookup"><span data-stu-id="ff9dd-164">Under that you find the description for **inboundNatPools**.</span></span>  <span data-ttu-id="ff9dd-165">Reemplace los valores de *frontendPortRangeStart* y *frontendPortRangeEnd*.</span><span class="sxs-lookup"><span data-stu-id="ff9dd-165">Replace the *frontendPortRangeStart* and *frontendPortRangeEnd* values.</span></span>

![inboundNatPools][InboundNatPools]

### <a name="after-cluster-deployment"></a><span data-ttu-id="ff9dd-167">Después de la implementación del clúster</span><span class="sxs-lookup"><span data-stu-id="ff9dd-167">After cluster deployment</span></span>
<span data-ttu-id="ff9dd-168">Esto es un poco más complicado y puede provocar que las máquinas virtuales se reciclen.</span><span class="sxs-lookup"><span data-stu-id="ff9dd-168">This is a bit more involved and may result in the VMs getting recycled.</span></span> <span data-ttu-id="ff9dd-169">Ahora tendrá que establecer nuevos valores usando Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ff9dd-169">You will now have to set new values using Azure PowerShell.</span></span> <span data-ttu-id="ff9dd-170">Asegúrese de que Azure PowerShell 1.0 esté instalado en su equipo (o una versión posterior).</span><span class="sxs-lookup"><span data-stu-id="ff9dd-170">Make sure that Azure PowerShell 1.0 or later is installed on your machine.</span></span> <span data-ttu-id="ff9dd-171">Si no lo ha hecho antes, se aconseja encarecidamente que siga los pasos descritos en [Cómo instalar y configurar Azure PowerShell](/powershell/azure/overview)</span><span class="sxs-lookup"><span data-stu-id="ff9dd-171">If you have not done this before, I strongly suggest that you follow the steps outlined in [How to install and configure Azure PowerShell.](/powershell/azure/overview)</span></span>

<span data-ttu-id="ff9dd-172">Inicie sesión en la cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="ff9dd-172">Sign in to your Azure account.</span></span> <span data-ttu-id="ff9dd-173">Si este comando de PowerShell da error por algún motivo, debe comprobar si tiene instalado correctamente Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ff9dd-173">If this PowerShell command fails for some reason, you should check whether you have Azure PowerShell installed correctly.</span></span>

```
Login-AzureRmAccount
```

<span data-ttu-id="ff9dd-174">Ejecute lo siguiente para obtener detalles sobre el equilibrador de carga y verá los valores para la descripción de **inboundNatPools**:</span><span class="sxs-lookup"><span data-stu-id="ff9dd-174">Run the following to get details on your load balancer and you see the values for the description for **inboundNatPools**:</span></span>

```
Get-AzureRmResource -ResourceGroupName <RGname> -ResourceType Microsoft.Network/loadBalancers -ResourceName <load balancer name>
```

<span data-ttu-id="ff9dd-175">Ahora configure *frontendPortRangeEnd* y *frontendPortRangeStart* con los valores que desee.</span><span class="sxs-lookup"><span data-stu-id="ff9dd-175">Now set *frontendPortRangeEnd* and *frontendPortRangeStart* to the values you want.</span></span>

```
$PropertiesObject = @{
    #Property = value;
}
Set-AzureRmResource -PropertyObject $PropertiesObject -ResourceGroupName <RG name> -ResourceType Microsoft.Network/loadBalancers -ResourceName <load Balancer name> -ApiVersion <use the API version that get returned> -Force
```


## <a name="next-steps"></a><span data-ttu-id="ff9dd-176">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ff9dd-176">Next steps</span></span>
* [<span data-ttu-id="ff9dd-177">Descripción general de la característica "Deploy anywhere" y comparación con los clústeres administrados de Azure</span><span class="sxs-lookup"><span data-stu-id="ff9dd-177">Overview of the "Deploy anywhere" feature and a comparison with Azure-managed clusters</span></span>](service-fabric-deploy-anywhere.md)
* [<span data-ttu-id="ff9dd-178">Seguridad de clúster</span><span class="sxs-lookup"><span data-stu-id="ff9dd-178">Cluster security</span></span>](service-fabric-cluster-security.md)
* [<span data-ttu-id="ff9dd-179"> SDK de Service Fabric e introducción</span><span class="sxs-lookup"><span data-stu-id="ff9dd-179"> Service Fabric SDK and getting started</span></span>](service-fabric-get-started.md)

<!--Image references-->
[NodeTypes]: ./media/service-fabric-cluster-nodetypes/NodeTypes.png
[Resources]: ./media/service-fabric-cluster-nodetypes/Resources.png
[InboundNatPools]: ./media/service-fabric-cluster-nodetypes/InboundNatPools.png
[LBBlade]: ./media/service-fabric-cluster-nodetypes/LBBlade.png
[NATRules]: ./media/service-fabric-cluster-nodetypes/NATRules.png
[RDP]: ./media/service-fabric-cluster-nodetypes/RDP.png
