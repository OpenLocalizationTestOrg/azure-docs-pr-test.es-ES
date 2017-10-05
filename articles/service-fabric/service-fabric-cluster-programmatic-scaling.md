---
title: "Escalado mediante programación de Azure Service Fabric | Microsoft Docs"
description: "Escalar o reducir horizontalmente mediante programación un clúster de Azure Service Fabric, de acuerdo a desencadenadores personalizados"
services: service-fabric
documentationcenter: .net
author: mjrousos
manager: jonjung
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: mikerou
ms.openlocfilehash: 46b0b62f92abbac57bc27bbcdd5821eafedf5519
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="scale-a-service-fabric-cluster-programmatically"></a><span data-ttu-id="57b5d-103">Escalado mediante programación de un clúster de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="57b5d-103">Scale a Service Fabric cluster programmatically</span></span> 

<span data-ttu-id="57b5d-104">Los aspectos básicos del escalado de un clúster de Service Fabric en Azure se tratan en la documentación sobre [escalado de clústeres](./service-fabric-cluster-scale-up-down.md).</span><span class="sxs-lookup"><span data-stu-id="57b5d-104">Fundamentals of scaling a Service Fabric cluster in Azure are covered in documentation on [cluster scaling](./service-fabric-cluster-scale-up-down.md).</span></span> <span data-ttu-id="57b5d-105">Ese artículo trata sobre como los clústeres de Service Fabric se basan en conjuntos de escalado de máquinas virtuales y se pueden escalar de forma manual o mediante reglas de escalado automático.</span><span class="sxs-lookup"><span data-stu-id="57b5d-105">That article covers how Service Fabric clusters are built on top of virtual machine scale sets and can be scaled either manually or with auto-scale rules.</span></span> <span data-ttu-id="57b5d-106">En este documento se examinan los métodos programáticos de coordinación de operaciones de escalado de Azure para escenarios más avanzados.</span><span class="sxs-lookup"><span data-stu-id="57b5d-106">This document looks at programmatic methods of coordinating Azure scaling operations for more advanced scenarios.</span></span> 

## <a name="reasons-for-programmatic-scaling"></a><span data-ttu-id="57b5d-107">Motivos para el escalado mediante programación</span><span class="sxs-lookup"><span data-stu-id="57b5d-107">Reasons for programmatic scaling</span></span>
<span data-ttu-id="57b5d-108">En muchos escenarios, el escalado de forma manual o mediante reglas de escalado automático son buenas soluciones.</span><span class="sxs-lookup"><span data-stu-id="57b5d-108">In many scenarios, scaling manually or via auto-scale rules are good solutions.</span></span> <span data-ttu-id="57b5d-109">Sin embargo, en otros escenarios, pueden no ser la mejor opción.</span><span class="sxs-lookup"><span data-stu-id="57b5d-109">In other scenarios, though, they may not be the right fit.</span></span> <span data-ttu-id="57b5d-110">Entre las desventajas potenciales de estos métodos se incluyen:</span><span class="sxs-lookup"><span data-stu-id="57b5d-110">Potential drawbacks to these approaches include:</span></span>

- <span data-ttu-id="57b5d-111">El escalado manual requiere que inicie sesión y solicite de forma explícita las operaciones de escalado.</span><span class="sxs-lookup"><span data-stu-id="57b5d-111">Manually scaling requires you to log in and explicitly request scaling operations.</span></span> <span data-ttu-id="57b5d-112">Si las operaciones de escalado se requieren con frecuencia o en momentos imprevisibles, este enfoque puede no ser una buena solución.</span><span class="sxs-lookup"><span data-stu-id="57b5d-112">If scaling operations are required frequently or at unpredictable times, this approach may not be a good solution.</span></span>
- <span data-ttu-id="57b5d-113">Cuando las reglas de escalado automático quitan una instancia de un conjunto de escalado de máquinas virtuales, no quitan automáticamente el conocimiento de ese nodo desde el clúster de Service Fabric asociado, a menos que el tipo de nodo tenga un nivel de durabilidad Silver o Gold.</span><span class="sxs-lookup"><span data-stu-id="57b5d-113">When auto-scale rules remove an instance from a virtual machine scale set, they do not automatically remove knowledge of that node from the associated Service Fabric cluster unless the node type has a durability level of Silver or Gold.</span></span> <span data-ttu-id="57b5d-114">Dado que las reglas de escalado automático funcionan a nivel de conjunto de escalado (en lugar de al nivel de Service Fabric), las reglas de escalado automático pueden quitar nodos de Service Fabric sin cerrarlos correctamente.</span><span class="sxs-lookup"><span data-stu-id="57b5d-114">Because auto-scale rules work at the scale set level (rather than at the Service Fabric level), auto-scale rules can remove Service Fabric nodes without shutting them down gracefully.</span></span> <span data-ttu-id="57b5d-115">Esta eliminación forzada de un nodo dejará un estado de nodo de Service Fabric "fantasma" después de operaciones de escalado.</span><span class="sxs-lookup"><span data-stu-id="57b5d-115">This rude node removal will leave 'ghost' Service Fabric node state behind after scale-in operations.</span></span> <span data-ttu-id="57b5d-116">Es necesario que una persona (o un servicio) limpie periódicamente el estado de los nodos eliminados en el clúster de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="57b5d-116">An individual (or a service) would need to periodically clean up removed node state in the Service Fabric cluster.</span></span>
  - <span data-ttu-id="57b5d-117">Tenga en cuenta que un tipo de nodo con un nivel de durabilidad Gold o Silver limpiará automáticamente los nodos eliminados.</span><span class="sxs-lookup"><span data-stu-id="57b5d-117">Note that a node type with a durability level of Gold or Silver will automatically clean up removed nodes.</span></span>  
- <span data-ttu-id="57b5d-118">Aunque hay [muchas métricas](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md) compatibles con las reglas de escalado automático, se trata aún de un conjunto limitado.</span><span class="sxs-lookup"><span data-stu-id="57b5d-118">Although there are [many metrics](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md) supported by auto-scale rules, it is still a limited set.</span></span> <span data-ttu-id="57b5d-119">Si su escenario requiere un escalado automático basado en alguna métrica que no se trata en ese conjunto, es posible que las reglas de escalado automático no sean una buena opción.</span><span class="sxs-lookup"><span data-stu-id="57b5d-119">If your scenario calls for scaling based on some metric not covered in that set, then auto-scale rules may not be a good option.</span></span>

<span data-ttu-id="57b5d-120">En función de estas limitaciones, puede que desee implementar más modelos de escalado automático personalizados.</span><span class="sxs-lookup"><span data-stu-id="57b5d-120">Based on these limitations, you may wish to implement more customized automatic scaling models.</span></span> 

## <a name="scaling-apis"></a><span data-ttu-id="57b5d-121">API de escalado</span><span class="sxs-lookup"><span data-stu-id="57b5d-121">Scaling APIs</span></span>
<span data-ttu-id="57b5d-122">Hay algunas API de Azure que permiten que las aplicaciones trabajen de forma programática con conjuntos de escalado de máquinas virtuales y clústeres de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="57b5d-122">Azure APIs exist which allow applications to programmatically work with virtual machine scale sets and Service Fabric clusters.</span></span> <span data-ttu-id="57b5d-123">Si las opciones existentes de escalado automático no funcionan para su escenario, estas API permiten implementar una lógica de escalado personalizada.</span><span class="sxs-lookup"><span data-stu-id="57b5d-123">If existing auto-scale options don't work for your scenario, these APIs make it possible to implement custom scaling logic.</span></span> 

<span data-ttu-id="57b5d-124">Un enfoque para implementar esta funcionalidad de escalado automático "casero" consiste en agregar un nuevo servicio sin estado a la aplicación de Service Fabric para administrar las operaciones de escalado.</span><span class="sxs-lookup"><span data-stu-id="57b5d-124">One approach to implementing this 'home-made' auto-scaling functionality is to add a new stateless service to the Service Fabric application to manage scaling operations.</span></span> <span data-ttu-id="57b5d-125">Dentro del método `RunAsync` del servicio, un conjunto de desencadenadores puede determinar si es necesario el escalado (incluyendo la comprobación de parámetros como el tamaño máximo del clúster y las recuperaciones de escalado).</span><span class="sxs-lookup"><span data-stu-id="57b5d-125">Within the service's `RunAsync` method, a set of triggers can determine if scaling is required (including checking parameters such as maximum cluster size and scaling cooldowns).</span></span>   

<span data-ttu-id="57b5d-126">La API que se utiliza para las interacciones de conjunto de escalado de máquinas virtuales (tanto para comprobar el número actual de instancias de máquina virtual como para modificarlo) es la fluida [Azure Compute Management Library](https://www.nuget.org/packages/Microsoft.Azure.Management.Compute.Fluent/).</span><span class="sxs-lookup"><span data-stu-id="57b5d-126">The API used for virtual machine scale set interactions (both to check the current number of virtual machine instances and to modify it) is the [fluent Azure Management Compute library](https://www.nuget.org/packages/Microsoft.Azure.Management.Compute.Fluent/).</span></span> <span data-ttu-id="57b5d-127">Esta biblioteca de proceso fluida proporciona una API fácil de usar para interactuar con los conjuntos de escalado de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="57b5d-127">The fluent compute library provides an easy-to-use API for interacting with virtual machine scale sets.</span></span>

<span data-ttu-id="57b5d-128">Para interactuar con el clúster de Service Fabric propiamente dicho, utilice [System.Fabric.FabricClient](/dotnet/api/system.fabric.fabricclient).</span><span class="sxs-lookup"><span data-stu-id="57b5d-128">To interact with the Service Fabric cluster itself, use [System.Fabric.FabricClient](/dotnet/api/system.fabric.fabricclient).</span></span>

<span data-ttu-id="57b5d-129">Por supuesto, el código de escalado no tiene que ejecutarse como un servicio en el clúster que se va a escalar.</span><span class="sxs-lookup"><span data-stu-id="57b5d-129">Of course, the scaling code doesn't need to run as a service in the cluster to be scaled.</span></span> <span data-ttu-id="57b5d-130">Ambos `IAzure` y `FabricClient` pueden conectarse a sus recursos asociados de Azure de forma remota, por lo que el servicio de escalado podría ser fácilmente una aplicación de consola o el servicio de Windows que se ejecuta desde fuera de la aplicación de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="57b5d-130">Both `IAzure` and `FabricClient` can connect to their associated Azure resources remotely, so the scaling service could easily be a console application or Windows service running from outside the Service Fabric application.</span></span> 

## <a name="credential-management"></a><span data-ttu-id="57b5d-131">Administración de credenciales</span><span class="sxs-lookup"><span data-stu-id="57b5d-131">Credential management</span></span>
<span data-ttu-id="57b5d-132">Una dificultad que se presenta al escribir un servicio para controlar el escalado es que el servicio tiene que tener acceso a recursos de conjunto de escalado de máquinas virtuales sin un inicio de sesión interactivo.</span><span class="sxs-lookup"><span data-stu-id="57b5d-132">One challenge of writing a service to handle scaling is that the service must be able to access virtual machine scale set resources without an interactive login.</span></span> <span data-ttu-id="57b5d-133">El acceso al clúster de Service Fabric es fácil si el servicio de escalado está modificando su propia aplicación de Service Fabric, pero se requieren credenciales para tener acceso al conjunto de escalado.</span><span class="sxs-lookup"><span data-stu-id="57b5d-133">Accessing the Service Fabric cluster is easy if the scaling service is modifying its own Service Fabric application, but credentials are needed to access the scale set.</span></span> <span data-ttu-id="57b5d-134">Para iniciar sesión, puede usar un [entidad de servicio](https://github.com/Azure/azure-sdk-for-net/blob/Fluent/AUTH.md#creating-a-service-principal-in-azure) creada con la [CLI de Azure 2.0](https://github.com/azure/azure-cli).</span><span class="sxs-lookup"><span data-stu-id="57b5d-134">To log in, you can use a [service principal](https://github.com/Azure/azure-sdk-for-net/blob/Fluent/AUTH.md#creating-a-service-principal-in-azure) created with the [Azure CLI 2.0](https://github.com/azure/azure-cli).</span></span>

<span data-ttu-id="57b5d-135">Una entidad de servicio se puede crear con los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="57b5d-135">A service principal can be created with the following steps:</span></span>

1. <span data-ttu-id="57b5d-136">Inicie sesión en la CLI de Azure (`az login`) como un usuario con acceso al conjunto de escalado de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="57b5d-136">Log in to the Azure CLI (`az login`) as a user with access to the virtual machine scale set</span></span>
2. <span data-ttu-id="57b5d-137">Cree la entidad de servicio con `az ad sp create-for-rbac`</span><span class="sxs-lookup"><span data-stu-id="57b5d-137">Create the service principal with `az ad sp create-for-rbac`</span></span>
    1. <span data-ttu-id="57b5d-138">Anote el appId (denominado "ID de cliente" en otros lugares), el nombre, la contraseña y el inquilino para su uso posterior.</span><span class="sxs-lookup"><span data-stu-id="57b5d-138">Make note of the appId (called 'client ID' elsewhere), name, password, and tenant for later use.</span></span>
    2. <span data-ttu-id="57b5d-139">También necesitará el identificador de suscripción, que se puede ver con `az account list`</span><span class="sxs-lookup"><span data-stu-id="57b5d-139">You will also need your subscription ID, which can be viewed with `az account list`</span></span>

<span data-ttu-id="57b5d-140">Se puede iniciar sesión en la biblioteca de proceso fluida puede con estas credenciales de la siguiente forma (tenga en cuenta que los tipos de Azure fluidos principales como `IAzure` se encuentran en el paquete [Microsoft.Azure.Management.Fluent](https://www.nuget.org/packages/Microsoft.Azure.Management.Fluent/)):</span><span class="sxs-lookup"><span data-stu-id="57b5d-140">The fluent compute library can log in using these credentials as follows (note that core fluent Azure types like `IAzure` are in the [Microsoft.Azure.Management.Fluent](https://www.nuget.org/packages/Microsoft.Azure.Management.Fluent/) package):</span></span>

```C#
var credentials = new AzureCredentials(new ServicePrincipalLoginInformation {
                ClientId = AzureClientId,
                ClientSecret = 
                AzureClientKey }, AzureTenantId, AzureEnvironment.AzureGlobalCloud);
IAzure AzureClient = Azure.Authenticate(credentials).WithSubscription(AzureSubscriptionId);

if (AzureClient?.SubscriptionId == AzureSubscriptionId)
{
    ServiceEventSource.Current.ServiceMessage(Context, "Successfully logged into Azure");
}
else
{
    ServiceEventSource.Current.ServiceMessage(Context, "ERROR: Failed to login to Azure");
}
```

<span data-ttu-id="57b5d-141">Una vez iniciada la sesión, el recuento de instancias de conjunto de escalado se puede consultar a través de `AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId).Capacity`.</span><span class="sxs-lookup"><span data-stu-id="57b5d-141">Once logged in, scale set instance count can be queried via `AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId).Capacity`.</span></span>

## <a name="scaling-out"></a><span data-ttu-id="57b5d-142">Escalado horizontal</span><span class="sxs-lookup"><span data-stu-id="57b5d-142">Scaling out</span></span>
<span data-ttu-id="57b5d-143">Con SDK de proceso fluido de Azure, se pueden agregar instancias al conjunto de escalado de máquinas virtuales con unas pocas llamadas.</span><span class="sxs-lookup"><span data-stu-id="57b5d-143">Using the fluent Azure compute SDK, instances can be added to the virtual machine scale set with just a few calls -</span></span>

```C#
var scaleSet = AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId);
var newCapacity = (int)Math.Min(MaximumNodeCount, scaleSet.Capacity + 1);
scaleSet.Update().WithCapacity(newCapacity).Apply(); 
``` 

<span data-ttu-id="57b5d-144">Como alternativa, el tamaño del conjunto de escalado de máquinas virtuales también puede administrarse con cmdlets de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="57b5d-144">Alternatively, virtual machine scale set size can also be managed with PowerShell cmdlets.</span></span> <span data-ttu-id="57b5d-145">[`Get-AzureRmVmss`](https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/get-azurermvmss) puede recuperar el objeto del conjunto de escalado de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="57b5d-145">[`Get-AzureRmVmss`](https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/get-azurermvmss) can retrieve the virtual machine scale set object.</span></span> <span data-ttu-id="57b5d-146">La capacidad actual se almacenará en la propiedad `.sku.capacity`.</span><span class="sxs-lookup"><span data-stu-id="57b5d-146">The current capacity will be stored in the `.sku.capacity` property.</span></span> <span data-ttu-id="57b5d-147">Después de cambiarla capacidad al valor deseado, el conjunto de escalado de máquinas virtuales en Azure puede actualizarse con el comando [`Update-AzureRmVmss`](https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/update-azurermvmss).</span><span class="sxs-lookup"><span data-stu-id="57b5d-147">After changing the capacity to the desired value, the virtual machine scale set in Azure can be updated with the [`Update-AzureRmVmss`](https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/update-azurermvmss) command.</span></span>

<span data-ttu-id="57b5d-148">Tal y como cuando se agrega manualmente un nodo, agregar una instancia de conjunto de escalado debe ser todo lo que se necesita para iniciar un nuevo nodo de Service Fabric, ya que la plantilla de conjunto de escalado incluye extensiones para unir automáticamente nuevas instancias al clúster de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="57b5d-148">As when adding a node manually, adding a scale set instance should be all that's needed to start a new Service Fabric node since the scale set template includes extensions to automatically join new instances to the Service Fabric cluster.</span></span> 

## <a name="scaling-in"></a><span data-ttu-id="57b5d-149">Reducir horizontalmente</span><span class="sxs-lookup"><span data-stu-id="57b5d-149">Scaling in</span></span>

<span data-ttu-id="57b5d-150">Reducir horizontalmente es similar a escalar horizontalmente.</span><span class="sxs-lookup"><span data-stu-id="57b5d-150">Scaling in is similar to scaling out.</span></span> <span data-ttu-id="57b5d-151">Los cambios reales del conjunto de escalado de máquinas virtuales son prácticamente los mismos.</span><span class="sxs-lookup"><span data-stu-id="57b5d-151">The actual virtual machine scale set changes are practically the same.</span></span> <span data-ttu-id="57b5d-152">Pero, tal y como se ha descrito anteriormente, Service Fabric solo limpia automáticamente los nodos eliminados con una durabilidad Gold o Silver.</span><span class="sxs-lookup"><span data-stu-id="57b5d-152">But, as was discussed previously, Service Fabric only automatically cleans up removed nodes with a durability of Gold or Silver.</span></span> <span data-ttu-id="57b5d-153">Por lo tanto, en el caso de reducción horizontal de durabilidad Bronze, es necesario interactuar con el clúster de Service Fabric para apagar el nodo que desea eliminar y a continuación eliminar su estado.</span><span class="sxs-lookup"><span data-stu-id="57b5d-153">So, in the Bronze-durability scale-in case, it's necessary to interact with the Service Fabric cluster to shut down the node to be removed and then to remove its state.</span></span>

<span data-ttu-id="57b5d-154">Preparar el nodo para el apagado implica buscar el nodo que se va a eliminar (el nodo agregado más recientemente) y desactivarlo.</span><span class="sxs-lookup"><span data-stu-id="57b5d-154">Preparing the node for shutdown involves finding the node to be removed (the most recently added node) and deactivating it.</span></span> <span data-ttu-id="57b5d-155">Para nodos que no sean de raíz, se pueden encontrar nodos más recientes mediante la comparación de `NodeInstanceId`.</span><span class="sxs-lookup"><span data-stu-id="57b5d-155">For non-seed nodes, newer nodes can be found by comparing `NodeInstanceId`.</span></span> 

```C#
using (var client = new FabricClient())
{
    var mostRecentLiveNode = (await client.QueryManager.GetNodeListAsync())
        .Where(n => n.NodeType.Equals(NodeTypeToScale, StringComparison.OrdinalIgnoreCase))
        .Where(n => n.NodeStatus == System.Fabric.Query.NodeStatus.Up)
        .OrderByDescending(n => n.NodeInstanceId)
        .FirstOrDefault();
```

<span data-ttu-id="57b5d-156">Tenga en cuenta que lo nodos *raíz* no parece que sigan siempre la convención de que se quiten primero los identificadores de instancia mayores.</span><span class="sxs-lookup"><span data-stu-id="57b5d-156">Be aware that *seed* nodes don't seem to always follow the convention that greater instance IDs are removed first.</span></span>

<span data-ttu-id="57b5d-157">Cuando se encuentre el nodo que se va a quitar, puede desactivarse y eliminarse utilizando la misma instancia `FabricClient` y la `IAzure` que se usó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="57b5d-157">Once the node to be removed is found, it can be deactivated and removed using the same `FabricClient` instance and the `IAzure` instance from earlier.</span></span>

```C#
var scaleSet = AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId);

// Remove the node from the Service Fabric cluster
ServiceEventSource.Current.ServiceMessage(Context, $"Disabling node {mostRecentLiveNode.NodeName}");
await client.ClusterManager.DeactivateNodeAsync(mostRecentLiveNode.NodeName, NodeDeactivationIntent.RemoveNode);

// Wait (up to a timeout) for the node to gracefully shutdown
var timeout = TimeSpan.FromMinutes(5);
var waitStart = DateTime.Now;
while ((mostRecentLiveNode.NodeStatus == System.Fabric.Query.NodeStatus.Up || mostRecentLiveNode.NodeStatus == System.Fabric.Query.NodeStatus.Disabling) &&
        DateTime.Now - waitStart < timeout)
{
    mostRecentLiveNode = (await client.QueryManager.GetNodeListAsync()).FirstOrDefault(n => n.NodeName == mostRecentLiveNode.NodeName);
    await Task.Delay(10 * 1000);
}

// Decrement VMSS capacity
var newCapacity = (int)Math.Max(MinimumNodeCount, scaleSet.Capacity - 1); // Check min count 

scaleSet.Update().WithCapacity(newCapacity).Apply(); 
```

<span data-ttu-id="57b5d-158">Como con el escalado, los cmdlets de PowerShell para la capacidad de modificación del conjunto de escalado de máquinas virtuales pueden usarse aquí si es preferible un enfoque de scripting.</span><span class="sxs-lookup"><span data-stu-id="57b5d-158">As with scaling out, PowerShell cmdlets for modifying virtual machine scale set capacity can also be used here if a scripting approach is preferable.</span></span> <span data-ttu-id="57b5d-159">Una vez que se ha eliminado la instancia de máquina virtual, se puede quitar el estado del nodo de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="57b5d-159">Once the virtual machine instance is removed, Service Fabric node state can be removed.</span></span>

```C#
await client.ClusterManager.RemoveNodeStateAsync(mostRecentLiveNode.NodeName);
```

## <a name="potential-drawbacks"></a><span data-ttu-id="57b5d-160">Desventajas potenciales</span><span class="sxs-lookup"><span data-stu-id="57b5d-160">Potential drawbacks</span></span>

<span data-ttu-id="57b5d-161">Como se muestra en los fragmentos de código anterior, crear su propio servicio de escalado proporciona el mayor grado de control y personalización sobre el comportamiento de escalado de su aplicación.</span><span class="sxs-lookup"><span data-stu-id="57b5d-161">As demonstrated in the preceding code snippets, creating your own scaling service provides the highest degree of control and customizability over your application's scaling behavior.</span></span> <span data-ttu-id="57b5d-162">Esto puede ser útil para escenarios que requieren un control preciso sobre cuándo y cómo una aplicación se escala o reduce horizontalmente.</span><span class="sxs-lookup"><span data-stu-id="57b5d-162">This can be useful for scenarios requiring precise control over when or how an application scales in or out.</span></span> <span data-ttu-id="57b5d-163">Sin embargo, este control acarrea el inconveniente de la complejidad del código.</span><span class="sxs-lookup"><span data-stu-id="57b5d-163">However, this control comes with a tradeoff of code complexity.</span></span> <span data-ttu-id="57b5d-164">Para usar este enfoque tiene que tener en propiedad código de escalado, lo que no es fácil.</span><span class="sxs-lookup"><span data-stu-id="57b5d-164">Using this approach means that you need to own scaling code, which is non-trivial.</span></span>

<span data-ttu-id="57b5d-165">La forma en la que debe enfocar el escalado de Service Fabric depende de su escenario.</span><span class="sxs-lookup"><span data-stu-id="57b5d-165">How you should approach Service Fabric scaling depends on your scenario.</span></span> <span data-ttu-id="57b5d-166">Si el escalado no es común, la capacidad de agregar o quitar nodos de forma manual es probablemente suficiente.</span><span class="sxs-lookup"><span data-stu-id="57b5d-166">If scaling is uncommon, the ability to add or remove nodes manually is probably sufficient.</span></span> <span data-ttu-id="57b5d-167">Para escenarios más complejos, las reglas de escalado automático y los SDK con la capacidad de escalar mediante programación ofrecen unas eficaces alternativas.</span><span class="sxs-lookup"><span data-stu-id="57b5d-167">For more complex scenarios, auto-scale rules and SDKs exposing the ability to scale programmatically offer powerful alternatives.</span></span>

## <a name="next-steps"></a><span data-ttu-id="57b5d-168">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="57b5d-168">Next steps</span></span>

<span data-ttu-id="57b5d-169">Para empezar a implementar su propia lógica de escalado automático, familiarícese con los siguientes conceptos y API útiles:</span><span class="sxs-lookup"><span data-stu-id="57b5d-169">To get started implementing your own auto-scaling logic, familiarize yourself with the following concepts and useful APIs:</span></span>

- [<span data-ttu-id="57b5d-170">Escalado manual o con reglas de escalado automático</span><span class="sxs-lookup"><span data-stu-id="57b5d-170">Scaling manually or with auto-scale rules</span></span>](./service-fabric-cluster-scale-up-down.md)
- <span data-ttu-id="57b5d-171">[Bibliotecas fluidas de administración de Azure para .NET](https://github.com/Azure/azure-sdk-for-net/tree/Fluent) (resulta útil para interactuar con los conjuntos de escalado de máquinas virtuales subyacentes de un clúster de Service Fabric)</span><span class="sxs-lookup"><span data-stu-id="57b5d-171">[Fluent Azure Management Libraries for .NET](https://github.com/Azure/azure-sdk-for-net/tree/Fluent) (useful for interacting with a Service Fabric cluster's underlying virtual machine scale sets)</span></span>
- <span data-ttu-id="57b5d-172">[System.Fabric.FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) (resulta útil para interactuar con un clúster de Service Fabric y sus nodos)</span><span class="sxs-lookup"><span data-stu-id="57b5d-172">[System.Fabric.FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) (useful for interacting with a Service Fabric cluster and its nodes)</span></span>
