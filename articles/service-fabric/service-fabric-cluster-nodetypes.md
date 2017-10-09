---
title: aaaService tejido tipos de nodos y conjuntos de escalas de VM | Documentos de Microsoft
description: "Describe cómo los tipos de nodos de Service Fabric se relacionan con los conjuntos de escalas de tooVM y cómo se conectan tooremote tooa instancia de conjunto de escalado de VM o un nodo de clúster."
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
ms.openlocfilehash: 830ea2816f5864de146a77483c85de26f91c2425
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="hello-relationship-between-service-fabric-node-types-and-virtual-machine-scale-sets"></a><span data-ttu-id="b2956-103">relación de Hello entre tipos de nodos de Service Fabric y conjuntos de escalas de máquina Virtual</span><span class="sxs-lookup"><span data-stu-id="b2956-103">hello relationship between Service Fabric node types and Virtual Machine Scale Sets</span></span>
<span data-ttu-id="b2956-104">Conjuntos de escalas de máquina virtual son un recurso de proceso de Azure puede usar toodeploy y administrar una colección de máquinas virtuales como un conjunto.</span><span class="sxs-lookup"><span data-stu-id="b2956-104">Virtual Machine Scale Sets are an Azure Compute resource you can use toodeploy and manage a collection of virtual machines as a set.</span></span> <span data-ttu-id="b2956-105">Cada tipo de nodo que se define en un clúster de Service Fabric está configurado como un conjunto de escalado de VM independiente.</span><span class="sxs-lookup"><span data-stu-id="b2956-105">Every node type that is defined in a Service Fabric cluster is set up as a separate VM Scale Set.</span></span> <span data-ttu-id="b2956-106">Cada tipo de nodo se puede escalar o reducir verticalmente de forma independiente. Cada uno tiene diferentes conjuntos de puertos abiertos y puede tener distintas métricas de capacidad.</span><span class="sxs-lookup"><span data-stu-id="b2956-106">Each node type can then be scaled up or down independently, have different sets of ports open, and can have different capacity metrics.</span></span>

<span data-ttu-id="b2956-107">Hola siguiente captura de pantalla muestra un clúster que tiene dos tipos de nodo: front-end y back-end.</span><span class="sxs-lookup"><span data-stu-id="b2956-107">hello following screen shot shows a cluster that has two node types: FrontEnd and BackEnd.</span></span>  <span data-ttu-id="b2956-108">A su vez, cada tipo de nodo tiene cinco nodos.</span><span class="sxs-lookup"><span data-stu-id="b2956-108">Each node type has five nodes each.</span></span>

![Captura de pantalla de un clúster que tiene dos tipos de nodos][NodeTypes]

## <a name="mapping-vm-scale-set-instances-toonodes"></a><span data-ttu-id="b2956-110">Asignación toonodes de instancias de conjunto de escala de VM.</span><span class="sxs-lookup"><span data-stu-id="b2956-110">Mapping VM Scale Set instances toonodes</span></span>
<span data-ttu-id="b2956-111">Como puede ver anteriormente, Hola conjunto de escalado de máquinas virtuales se inician las instancias de la instancia 0 y, a continuación, aumenta.</span><span class="sxs-lookup"><span data-stu-id="b2956-111">As you can see above, hello VM Scale Set instances start from instance 0 and then goes up.</span></span> <span data-ttu-id="b2956-112">Hola numeración se refleja en los nombres de Hola.</span><span class="sxs-lookup"><span data-stu-id="b2956-112">hello numbering is reflected in hello names.</span></span> <span data-ttu-id="b2956-113">Por ejemplo, BackEnd_0 es instancia 0 de hello conjunto de escalado de la máquina virtual de back-end.</span><span class="sxs-lookup"><span data-stu-id="b2956-113">For example, BackEnd_0 is instance 0 of hello BackEnd VM Scale Set.</span></span> <span data-ttu-id="b2956-114">En concreto, este conjunto de escalado de máquinas virtuales tiene cinco instancias, denominadas BackEnd_0, BackEnd_1, BackEnd_2, BackEnd_3 y BackEnd_4.</span><span class="sxs-lookup"><span data-stu-id="b2956-114">This particular VM Scale Set has five instances, named BackEnd_0, BackEnd_1, BackEnd_2, BackEnd_3 and BackEnd_4.</span></span>

<span data-ttu-id="b2956-115">Al escalar verticalmente un conjunto de escalado de máquinas virtuales, se crea una nueva instancia.</span><span class="sxs-lookup"><span data-stu-id="b2956-115">When you scale up a VM Scale Set a new instance is created.</span></span> <span data-ttu-id="b2956-116">Hola nuevo conjunto de escalado de VM nombre de instancia normalmente será el nombre de conjunto de escalado de VM de hello + número de instancia siguiente de Hola.</span><span class="sxs-lookup"><span data-stu-id="b2956-116">hello new VM Scale Set instance name will typically be hello VM Scale Set name + hello next instance number.</span></span> <span data-ttu-id="b2956-117">En nuestro ejemplo, es BackEnd_5.</span><span class="sxs-lookup"><span data-stu-id="b2956-117">In our example, it is BackEnd_5.</span></span>

## <a name="mapping-vm-scale-set-load-balancers-tooeach-node-typevm-scale-set"></a><span data-ttu-id="b2956-118">Asignación de máquina virtual conjunto de escalas de carga equilibradores tooeach nodo tipo/VM conjunto de escala</span><span class="sxs-lookup"><span data-stu-id="b2956-118">Mapping VM scale set load balancers tooeach node type/VM Scale Set</span></span>
<span data-ttu-id="b2956-119">Si ha implementado el clúster desde el portal de Hola o ha usado la plantilla de administrador de recursos de ejemplo de Hola que se proporciona, a continuación, cuando se obtiene una lista de todos los recursos en un grupo de recursos verá equilibradores de carga de Hola para cada tipo de nodo o conjunto de escalado de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="b2956-119">If you have deployed your cluster from hello portal or have used hello sample Resource Manager template that we provided, then when you get a list of all resources under a Resource Group then you will see hello load balancers for each VM Scale Set or node type.</span></span>

<span data-ttu-id="b2956-120">Hello nombre sería algo parecido a: **LB -&lt;NodeType nombre&gt;**.</span><span class="sxs-lookup"><span data-stu-id="b2956-120">hello name would something like: **LB-&lt;NodeType name&gt;**.</span></span> <span data-ttu-id="b2956-121">Por ejemplo, LB-sfcluster4doc-0, como se muestra en esta captura de pantalla:</span><span class="sxs-lookup"><span data-stu-id="b2956-121">For example, LB-sfcluster4doc-0, as shown in this screenshot:</span></span>

![Recursos][Resources]

## <a name="remote-connect-tooa-vm-scale-set-instance-or-a-cluster-node"></a><span data-ttu-id="b2956-123">Instancia de conjunto de escalado de VM de tooa o un nodo de clúster de conexión remota</span><span class="sxs-lookup"><span data-stu-id="b2956-123">Remote connect tooa VM Scale Set instance or a cluster node</span></span>
<span data-ttu-id="b2956-124">Cada tipo de nodo que se define en un clúster está configurado como un conjunto de escalado de VM independiente.</span><span class="sxs-lookup"><span data-stu-id="b2956-124">Every Node type that is defined in a cluster is set up as a separate VM Scale Set.</span></span>  <span data-ttu-id="b2956-125">Que significa Hola tipos de nodo se puede escalar una copia de seguridad o el detalle de forma independiente y se pueden realizar de diferentes SKU de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="b2956-125">That means hello node types can be scaled up or down independently and can be made of different VM SKUs.</span></span> <span data-ttu-id="b2956-126">A diferencia de las máquinas virtuales de instancia única, instancias de conjunto de escalado de VM de hello no obtiene una dirección IP virtual por sí mismos.</span><span class="sxs-lookup"><span data-stu-id="b2956-126">Unlike single instance VMs, hello VM Scale Set instances do not get a virtual IP address of their own.</span></span> <span data-ttu-id="b2956-127">Por lo que puede ser un poco complicado cuando se desea obtener una dirección IP dirección y el puerto que se puede usar tooremote conectan instancia específica de tooa.</span><span class="sxs-lookup"><span data-stu-id="b2956-127">So it can be a bit challenging when you are looking for an IP address and port that you can use tooremote connect tooa specific instance.</span></span>

<span data-ttu-id="b2956-128">Estos son los pasos de hello puede seguir toodiscover ellos.</span><span class="sxs-lookup"><span data-stu-id="b2956-128">Here are hello steps you can follow toodiscover them.</span></span>

### <a name="step-1-find-out-hello-virtual-ip-address-for-hello-node-type-and-then-inbound-nat-rules-for-rdp"></a><span data-ttu-id="b2956-129">Paso 1: Obtener dirección IP virtual de hello para el tipo de nodo de hello y, a continuación, las reglas de NAT de entrada para RDP</span><span class="sxs-lookup"><span data-stu-id="b2956-129">Step 1: Find out hello virtual IP address for hello node type and then Inbound NAT rules for RDP</span></span>
<span data-ttu-id="b2956-130">En tooget orden esto, necesita tooget Hola NAT de entrada de reglas de valores que se definieron como parte de la definición de recursos de Hola para **Microsoft.Network/loadBalancers**.</span><span class="sxs-lookup"><span data-stu-id="b2956-130">In order tooget that, you need tooget hello inbound NAT rules values that were defined as a part of hello resource definition for **Microsoft.Network/loadBalancers**.</span></span>

<span data-ttu-id="b2956-131">En el portal de hello, navegar por hoja de equilibrador de carga de toohello y, a continuación, **configuración**.</span><span class="sxs-lookup"><span data-stu-id="b2956-131">In hello portal, navigate toohello Load balancer blade and then **Settings**.</span></span>

![LBBlade][LBBlade]

<span data-ttu-id="b2956-133">En **Configuración**, haga clic en **Reglas NAT de entrada**.</span><span class="sxs-lookup"><span data-stu-id="b2956-133">In **Settings**, click on **Inbound NAT rules**.</span></span> <span data-ttu-id="b2956-134">Ahora Esto proporciona Hola dirección IP y puerto que se puede usar tooremote conectar toohello primera instancia del conjunto de escalado de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="b2956-134">This now gives you hello IP address and port that you can use tooremote connect toohello first VM Scale Set instance.</span></span> <span data-ttu-id="b2956-135">En la siguiente captura de pantalla de hello, es **104.42.106.156** y **3389**</span><span class="sxs-lookup"><span data-stu-id="b2956-135">In hello screenshot below, it is **104.42.106.156** and **3389**</span></span>

![NATRules][NATRules]

### <a name="step-2-find-out-hello-port-that-you-can-use-tooremote-connect-toohello-specific-vm-scale-set-instancenode"></a><span data-ttu-id="b2956-137">Paso 2: Obtenga más información sobre el puerto de Hola que puede usar tooremote conexión toohello conjunto de escalado de VM instancia/nodo específico</span><span class="sxs-lookup"><span data-stu-id="b2956-137">Step 2: Find out hello port that you can use tooremote connect toohello specific VM Scale Set instance/node</span></span>
<span data-ttu-id="b2956-138">Anteriormente en este documento, describe cómo asignan los nodos toohello en instancias de conjunto de escalado de VM de Hola.</span><span class="sxs-lookup"><span data-stu-id="b2956-138">Earlier in this document, I talked about how hello VM Scale Set instances map toohello nodes.</span></span> <span data-ttu-id="b2956-139">Se usará ese toofigure puerto exacto de Hola de salida.</span><span class="sxs-lookup"><span data-stu-id="b2956-139">We will use that toofigure out hello exact port.</span></span>

<span data-ttu-id="b2956-140">puertos de Hola se asignan en orden ascendente de instancia de conjunto de escalado de VM de Hola.</span><span class="sxs-lookup"><span data-stu-id="b2956-140">hello ports are allocated in ascending order of hello VM Scale Set instance.</span></span> <span data-ttu-id="b2956-141">por lo que en el ejemplo de Hola tipo de nodo de front-end, puertos de Hola para cada una de las cinco instancias de hello son siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="b2956-141">so in my example for hello FrontEnd node type, hello ports for each of hello five instances are hello following.</span></span> <span data-ttu-id="b2956-142">Ahora necesita toodo Hola misma asignación para la instancia del conjunto de escalado de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="b2956-142">you now need toodo hello same mapping for your VM Scale Set instance.</span></span>

| <span data-ttu-id="b2956-143">**Instancia de conjunto de escalado de VM**</span><span class="sxs-lookup"><span data-stu-id="b2956-143">**VM Scale Set Instance**</span></span> | <span data-ttu-id="b2956-144">**Puerto**</span><span class="sxs-lookup"><span data-stu-id="b2956-144">**Port**</span></span> |
| --- | --- |
| <span data-ttu-id="b2956-145">FrontEnd_0</span><span class="sxs-lookup"><span data-stu-id="b2956-145">FrontEnd_0</span></span> |<span data-ttu-id="b2956-146">3389</span><span class="sxs-lookup"><span data-stu-id="b2956-146">3389</span></span> |
| <span data-ttu-id="b2956-147">FrontEnd_1</span><span class="sxs-lookup"><span data-stu-id="b2956-147">FrontEnd_1</span></span> |<span data-ttu-id="b2956-148">3390</span><span class="sxs-lookup"><span data-stu-id="b2956-148">3390</span></span> |
| <span data-ttu-id="b2956-149">FrontEnd_2</span><span class="sxs-lookup"><span data-stu-id="b2956-149">FrontEnd_2</span></span> |<span data-ttu-id="b2956-150">3391</span><span class="sxs-lookup"><span data-stu-id="b2956-150">3391</span></span> |
| <span data-ttu-id="b2956-151">FrontEnd_3</span><span class="sxs-lookup"><span data-stu-id="b2956-151">FrontEnd_3</span></span> |<span data-ttu-id="b2956-152">3392</span><span class="sxs-lookup"><span data-stu-id="b2956-152">3392</span></span> |
| <span data-ttu-id="b2956-153">FrontEnd_4</span><span class="sxs-lookup"><span data-stu-id="b2956-153">FrontEnd_4</span></span> |<span data-ttu-id="b2956-154">3393</span><span class="sxs-lookup"><span data-stu-id="b2956-154">3393</span></span> |
| <span data-ttu-id="b2956-155">FrontEnd_5</span><span class="sxs-lookup"><span data-stu-id="b2956-155">FrontEnd_5</span></span> |<span data-ttu-id="b2956-156">3394</span><span class="sxs-lookup"><span data-stu-id="b2956-156">3394</span></span> |

### <a name="step-3-remote-connect-toohello-specific-vm-scale-set-instance"></a><span data-ttu-id="b2956-157">Paso 3: Instancia de conjunto de escalado de VM de toohello específica de conexión remota</span><span class="sxs-lookup"><span data-stu-id="b2956-157">Step 3: Remote connect toohello specific VM Scale Set instance</span></span>
<span data-ttu-id="b2956-158">En la siguiente captura de pantalla de hello Usar conexión a Escritorio remoto tooconnect toohello FrontEnd_1:</span><span class="sxs-lookup"><span data-stu-id="b2956-158">In hello screenshot below I use Remote Desktop Connection tooconnect toohello FrontEnd_1:</span></span>

![RDP][RDP]

## <a name="how-toochange-hello-rdp-port-range-values"></a><span data-ttu-id="b2956-160">Hola toochange puerto RDP cómo los valores de intervalo</span><span class="sxs-lookup"><span data-stu-id="b2956-160">How toochange hello RDP port range values</span></span>
### <a name="before-cluster-deployment"></a><span data-ttu-id="b2956-161">Antes de la implementación del clúster</span><span class="sxs-lookup"><span data-stu-id="b2956-161">Before cluster deployment</span></span>
<span data-ttu-id="b2956-162">Cuando se configura usando una plantilla de administrador de recursos de clúster de hello, puede especificar el intervalo de Hola Hola **inboundNatPools**.</span><span class="sxs-lookup"><span data-stu-id="b2956-162">When you are setting up hello cluster using an Resource Manager template, you can specify hello range in hello **inboundNatPools**.</span></span>

<span data-ttu-id="b2956-163">Ir a definición de recursos de toohello para **Microsoft.Network/loadBalancers**.</span><span class="sxs-lookup"><span data-stu-id="b2956-163">Go toohello resource definition for **Microsoft.Network/loadBalancers**.</span></span> <span data-ttu-id="b2956-164">En la que buscar descripción Hola para **inboundNatPools**.</span><span class="sxs-lookup"><span data-stu-id="b2956-164">Under that you find hello description for **inboundNatPools**.</span></span>  <span data-ttu-id="b2956-165">Reemplace hello *frontendPortRangeStart* y *frontendPortRangeEnd* valores.</span><span class="sxs-lookup"><span data-stu-id="b2956-165">Replace hello *frontendPortRangeStart* and *frontendPortRangeEnd* values.</span></span>

![inboundNatPools][InboundNatPools]

### <a name="after-cluster-deployment"></a><span data-ttu-id="b2956-167">Después de la implementación del clúster</span><span class="sxs-lookup"><span data-stu-id="b2956-167">After cluster deployment</span></span>
<span data-ttu-id="b2956-168">Esto es un poco más complicada y podría resultar en máquinas virtuales de Hola que se reciclen.</span><span class="sxs-lookup"><span data-stu-id="b2956-168">This is a bit more involved and may result in hello VMs getting recycled.</span></span> <span data-ttu-id="b2956-169">Ahora tienes tooset nuevos valores mediante Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b2956-169">You will now have tooset new values using Azure PowerShell.</span></span> <span data-ttu-id="b2956-170">Asegúrese de que Azure PowerShell 1.0 esté instalado en su equipo (o una versión posterior).</span><span class="sxs-lookup"><span data-stu-id="b2956-170">Make sure that Azure PowerShell 1.0 or later is installed on your machine.</span></span> <span data-ttu-id="b2956-171">Si no ha hecho esto antes, es recomendable que siga los pasos de Hola que se describen en [cómo tooinstall y configurar Azure PowerShell.](/powershell/azure/overview)</span><span class="sxs-lookup"><span data-stu-id="b2956-171">If you have not done this before, I strongly suggest that you follow hello steps outlined in [How tooinstall and configure Azure PowerShell.](/powershell/azure/overview)</span></span>

<span data-ttu-id="b2956-172">Inicie sesión en tooyour cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="b2956-172">Sign in tooyour Azure account.</span></span> <span data-ttu-id="b2956-173">Si este comando de PowerShell da error por algún motivo, debe comprobar si tiene instalado correctamente Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b2956-173">If this PowerShell command fails for some reason, you should check whether you have Azure PowerShell installed correctly.</span></span>

```
Login-AzureRmAccount
```

<span data-ttu-id="b2956-174">Ejecute hello tooget detalla en el equilibrador de carga y ver valores de hello para la descripción de Hola para **inboundNatPools**:</span><span class="sxs-lookup"><span data-stu-id="b2956-174">Run hello following tooget details on your load balancer and you see hello values for hello description for **inboundNatPools**:</span></span>

```
Get-AzureRmResource -ResourceGroupName <RGname> -ResourceType Microsoft.Network/loadBalancers -ResourceName <load balancer name>
```

<span data-ttu-id="b2956-175">Establecer ahora *frontendPortRangeEnd* y *frontendPortRangeStart* toohello los valores que desee.</span><span class="sxs-lookup"><span data-stu-id="b2956-175">Now set *frontendPortRangeEnd* and *frontendPortRangeStart* toohello values you want.</span></span>

```
$PropertiesObject = @{
    #Property = value;
}
Set-AzureRmResource -PropertyObject $PropertiesObject -ResourceGroupName <RG name> -ResourceType Microsoft.Network/loadBalancers -ResourceName <load Balancer name> -ApiVersion <use hello API version that get returned> -Force
```


## <a name="next-steps"></a><span data-ttu-id="b2956-176">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b2956-176">Next steps</span></span>
* [<span data-ttu-id="b2956-177">Información general sobre la característica de "En cualquier lugar para implementar" hello y hacer una comparación con clústeres administrado de Azure</span><span class="sxs-lookup"><span data-stu-id="b2956-177">Overview of hello "Deploy anywhere" feature and a comparison with Azure-managed clusters</span></span>](service-fabric-deploy-anywhere.md)
* [<span data-ttu-id="b2956-178">Seguridad de clúster</span><span class="sxs-lookup"><span data-stu-id="b2956-178">Cluster security</span></span>](service-fabric-cluster-security.md)
* [<span data-ttu-id="b2956-179"> SDK de Service Fabric e introducción</span><span class="sxs-lookup"><span data-stu-id="b2956-179"> Service Fabric SDK and getting started</span></span>](service-fabric-get-started.md)

<!--Image references-->
[NodeTypes]: ./media/service-fabric-cluster-nodetypes/NodeTypes.png
[Resources]: ./media/service-fabric-cluster-nodetypes/Resources.png
[InboundNatPools]: ./media/service-fabric-cluster-nodetypes/InboundNatPools.png
[LBBlade]: ./media/service-fabric-cluster-nodetypes/LBBlade.png
[NATRules]: ./media/service-fabric-cluster-nodetypes/NATRules.png
[RDP]: ./media/service-fabric-cluster-nodetypes/RDP.png
