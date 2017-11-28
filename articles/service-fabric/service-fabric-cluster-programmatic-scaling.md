---
title: "aaaAzure escalar mediante programación de Service Fabric | Documentos de Microsoft"
description: "Escalar un cluster Azure Service Fabric o alejar mediante programación, según toocustom desencadenadores"
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
ms.openlocfilehash: a0c6499b1a143a173006248cf8a15380632637e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="scale-a-service-fabric-cluster-programmatically"></a><span data-ttu-id="b8555-103">Escalado mediante programación de un clúster de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="b8555-103">Scale a Service Fabric cluster programmatically</span></span> 

<span data-ttu-id="b8555-104">Los aspectos básicos del escalado de un clúster de Service Fabric en Azure se tratan en la documentación sobre [escalado de clústeres](./service-fabric-cluster-scale-up-down.md).</span><span class="sxs-lookup"><span data-stu-id="b8555-104">Fundamentals of scaling a Service Fabric cluster in Azure are covered in documentation on [cluster scaling](./service-fabric-cluster-scale-up-down.md).</span></span> <span data-ttu-id="b8555-105">Ese artículo trata sobre como los clústeres de Service Fabric se basan en conjuntos de escalado de máquinas virtuales y se pueden escalar de forma manual o mediante reglas de escalado automático.</span><span class="sxs-lookup"><span data-stu-id="b8555-105">That article covers how Service Fabric clusters are built on top of virtual machine scale sets and can be scaled either manually or with auto-scale rules.</span></span> <span data-ttu-id="b8555-106">En este documento se examinan los métodos programáticos de coordinación de operaciones de escalado de Azure para escenarios más avanzados.</span><span class="sxs-lookup"><span data-stu-id="b8555-106">This document looks at programmatic methods of coordinating Azure scaling operations for more advanced scenarios.</span></span> 

## <a name="reasons-for-programmatic-scaling"></a><span data-ttu-id="b8555-107">Motivos para el escalado mediante programación</span><span class="sxs-lookup"><span data-stu-id="b8555-107">Reasons for programmatic scaling</span></span>
<span data-ttu-id="b8555-108">En muchos escenarios, el escalado de forma manual o mediante reglas de escalado automático son buenas soluciones.</span><span class="sxs-lookup"><span data-stu-id="b8555-108">In many scenarios, scaling manually or via auto-scale rules are good solutions.</span></span> <span data-ttu-id="b8555-109">Sin embargo, en otros escenarios, no pueden ser Hola ajustarse a la derecha.</span><span class="sxs-lookup"><span data-stu-id="b8555-109">In other scenarios, though, they may not be hello right fit.</span></span> <span data-ttu-id="b8555-110">Entre los posibles inconvenientes toothese enfoques se incluyen:</span><span class="sxs-lookup"><span data-stu-id="b8555-110">Potential drawbacks toothese approaches include:</span></span>

- <span data-ttu-id="b8555-111">Escala manual requiere toolog en y ajuste de escala en las operaciones de solicitud de forma explícita.</span><span class="sxs-lookup"><span data-stu-id="b8555-111">Manually scaling requires you toolog in and explicitly request scaling operations.</span></span> <span data-ttu-id="b8555-112">Si las operaciones de escalado se requieren con frecuencia o en momentos imprevisibles, este enfoque puede no ser una buena solución.</span><span class="sxs-lookup"><span data-stu-id="b8555-112">If scaling operations are required frequently or at unpredictable times, this approach may not be a good solution.</span></span>
- <span data-ttu-id="b8555-113">Cuando las reglas de escalado automático quitan una instancia de un conjunto de escalas de máquina virtual, quita automáticamente conocimientos de ese nodo de clúster de Service Fabric Hola asociado a menos que el tipo de nodo de hello tiene un nivel de durabilidad de plata y oro.</span><span class="sxs-lookup"><span data-stu-id="b8555-113">When auto-scale rules remove an instance from a virtual machine scale set, they do not automatically remove knowledge of that node from hello associated Service Fabric cluster unless hello node type has a durability level of Silver or Gold.</span></span> <span data-ttu-id="b8555-114">Dado que las reglas de escalado automático funcionan a establecer el nivel de escala de hello (en lugar de en el nivel de Service Fabric hello), reglas de escalado automático pueden quitar nodos de Service Fabric sin ellos cerrarse correctamente.</span><span class="sxs-lookup"><span data-stu-id="b8555-114">Because auto-scale rules work at hello scale set level (rather than at hello Service Fabric level), auto-scale rules can remove Service Fabric nodes without shutting them down gracefully.</span></span> <span data-ttu-id="b8555-115">Esta eliminación forzada de un nodo dejará un estado de nodo de Service Fabric "fantasma" después de operaciones de escalado.</span><span class="sxs-lookup"><span data-stu-id="b8555-115">This rude node removal will leave 'ghost' Service Fabric node state behind after scale-in operations.</span></span> <span data-ttu-id="b8555-116">Una persona (o un servicio) necesitaría tooperiodically limpiar el estado de los nodos quitados en clúster de Service Fabric Hola.</span><span class="sxs-lookup"><span data-stu-id="b8555-116">An individual (or a service) would need tooperiodically clean up removed node state in hello Service Fabric cluster.</span></span>
  - <span data-ttu-id="b8555-117">Tenga en cuenta que un tipo de nodo con un nivel de durabilidad Gold o Silver limpiará automáticamente los nodos eliminados.</span><span class="sxs-lookup"><span data-stu-id="b8555-117">Note that a node type with a durability level of Gold or Silver will automatically clean up removed nodes.</span></span>  
- <span data-ttu-id="b8555-118">Aunque hay [muchas métricas](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md) compatibles con las reglas de escalado automático, se trata aún de un conjunto limitado.</span><span class="sxs-lookup"><span data-stu-id="b8555-118">Although there are [many metrics](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md) supported by auto-scale rules, it is still a limited set.</span></span> <span data-ttu-id="b8555-119">Si su escenario requiere un escalado automático basado en alguna métrica que no se trata en ese conjunto, es posible que las reglas de escalado automático no sean una buena opción.</span><span class="sxs-lookup"><span data-stu-id="b8555-119">If your scenario calls for scaling based on some metric not covered in that set, then auto-scale rules may not be a good option.</span></span>

<span data-ttu-id="b8555-120">En función de estas limitaciones, es recomendable tooimplement más automática escala modelos personalizados.</span><span class="sxs-lookup"><span data-stu-id="b8555-120">Based on these limitations, you may wish tooimplement more customized automatic scaling models.</span></span> 

## <a name="scaling-apis"></a><span data-ttu-id="b8555-121">API de escalado</span><span class="sxs-lookup"><span data-stu-id="b8555-121">Scaling APIs</span></span>
<span data-ttu-id="b8555-122">Las API de Azure existen que permiten que el trabajo de tooprogrammatically de aplicaciones con conjuntos de escalas de máquina virtual y clústeres de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="b8555-122">Azure APIs exist which allow applications tooprogrammatically work with virtual machine scale sets and Service Fabric clusters.</span></span> <span data-ttu-id="b8555-123">Si las opciones existentes de escala automática no funcionan para su escenario, estas API puede hacerla lógica de ajuste de escala personalizada tooimplement posibles.</span><span class="sxs-lookup"><span data-stu-id="b8555-123">If existing auto-scale options don't work for your scenario, these APIs make it possible tooimplement custom scaling logic.</span></span> 

<span data-ttu-id="b8555-124">Tooimplementing un enfoque esto 'principal-realizados' escalado automático funcionalidad es tooadd un nuevo toomanage de la aplicación de Service Fabric de toohello servicio sin estado operaciones de ajuste de escala.</span><span class="sxs-lookup"><span data-stu-id="b8555-124">One approach tooimplementing this 'home-made' auto-scaling functionality is tooadd a new stateless service toohello Service Fabric application toomanage scaling operations.</span></span> <span data-ttu-id="b8555-125">Dentro del servicio de hello `RunAsync` método, un conjunto de desencadenadores puede determinar si el ajuste de escala es necesaria (incluida la comprobación de parámetros como el tamaño máximo del clúster y ajuste de escala en cooldowns).</span><span class="sxs-lookup"><span data-stu-id="b8555-125">Within hello service's `RunAsync` method, a set of triggers can determine if scaling is required (including checking parameters such as maximum cluster size and scaling cooldowns).</span></span>   

<span data-ttu-id="b8555-126">Hola API que se utiliza para las interacciones de conjunto de escala de máquina virtual (ambos toocheck Hola actual en número de instancias de máquina virtual y toomodify lo) es hello [biblioteca fluida de procesos de administración de Azure](https://www.nuget.org/packages/Microsoft.Azure.Management.Compute.Fluent/).</span><span class="sxs-lookup"><span data-stu-id="b8555-126">hello API used for virtual machine scale set interactions (both toocheck hello current number of virtual machine instances and toomodify it) is hello [fluent Azure Management Compute library](https://www.nuget.org/packages/Microsoft.Azure.Management.Compute.Fluent/).</span></span> <span data-ttu-id="b8555-127">biblioteca de cálculo fluida de Hello proporciona una API de fácil de usar para interactuar con los conjuntos de escalas de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="b8555-127">hello fluent compute library provides an easy-to-use API for interacting with virtual machine scale sets.</span></span>

<span data-ttu-id="b8555-128">usar toointeract con clúster de Service Fabric hello, [System.Fabric.FabricClient](/dotnet/api/system.fabric.fabricclient).</span><span class="sxs-lookup"><span data-stu-id="b8555-128">toointeract with hello Service Fabric cluster itself, use [System.Fabric.FabricClient](/dotnet/api/system.fabric.fabricclient).</span></span>

<span data-ttu-id="b8555-129">Por supuesto, no es necesario Hola escalar código toorun como un servicio en hello clúster toobe escalada.</span><span class="sxs-lookup"><span data-stu-id="b8555-129">Of course, hello scaling code doesn't need toorun as a service in hello cluster toobe scaled.</span></span> <span data-ttu-id="b8555-130">Ambos `IAzure` y `FabricClient` puede conectarse a tootheir asociado Azure recursos de forma remota, por lo Hola escalar servicio puede ser fácilmente una aplicación de consola o ejecutando desde la aplicación de Service Fabric de hello fuera de servicio de Windows.</span><span class="sxs-lookup"><span data-stu-id="b8555-130">Both `IAzure` and `FabricClient` can connect tootheir associated Azure resources remotely, so hello scaling service could easily be a console application or Windows service running from outside hello Service Fabric application.</span></span> 

## <a name="credential-management"></a><span data-ttu-id="b8555-131">Administración de credenciales</span><span class="sxs-lookup"><span data-stu-id="b8555-131">Credential management</span></span>
<span data-ttu-id="b8555-132">Presenta la dificultad de la escritura de una escala de toohandle de servicio es que el servicio de hello debe ser recursos de conjunto de escala de tooaccess capaz de máquina virtual sin un inicio de sesión interactivo.</span><span class="sxs-lookup"><span data-stu-id="b8555-132">One challenge of writing a service toohandle scaling is that hello service must be able tooaccess virtual machine scale set resources without an interactive login.</span></span> <span data-ttu-id="b8555-133">Acceso a Hola Service Fabric clúster es fácil si Hola escalar servicio modificando su propia aplicación de Service Fabric, pero las credenciales son necesarias tooaccess Hola conjunto de escala.</span><span class="sxs-lookup"><span data-stu-id="b8555-133">Accessing hello Service Fabric cluster is easy if hello scaling service is modifying its own Service Fabric application, but credentials are needed tooaccess hello scale set.</span></span> <span data-ttu-id="b8555-134">toolog en, puede usar un [entidad de servicio](https://github.com/Azure/azure-sdk-for-net/blob/Fluent/AUTH.md#creating-a-service-principal-in-azure) creado con hello [CLI de Azure 2.0](https://github.com/azure/azure-cli).</span><span class="sxs-lookup"><span data-stu-id="b8555-134">toolog in, you can use a [service principal](https://github.com/Azure/azure-sdk-for-net/blob/Fluent/AUTH.md#creating-a-service-principal-in-azure) created with hello [Azure CLI 2.0](https://github.com/azure/azure-cli).</span></span>

<span data-ttu-id="b8555-135">Una entidad de servicio puede crearse con hello pasos:</span><span class="sxs-lookup"><span data-stu-id="b8555-135">A service principal can be created with hello following steps:</span></span>

1. <span data-ttu-id="b8555-136">Inicie sesión en toohello CLI de Azure (`az login`) como un usuario con escala de máquinas virtuales de acceso toohello conjunto</span><span class="sxs-lookup"><span data-stu-id="b8555-136">Log in toohello Azure CLI (`az login`) as a user with access toohello virtual machine scale set</span></span>
2. <span data-ttu-id="b8555-137">Crear servicio Hola principal con`az ad sp create-for-rbac`</span><span class="sxs-lookup"><span data-stu-id="b8555-137">Create hello service principal with `az ad sp create-for-rbac`</span></span>
    1. <span data-ttu-id="b8555-138">Tome nota del appId hello (denominada 'ID de cliente' en otro lugar), nombre, contraseña e inquilino para su uso posterior.</span><span class="sxs-lookup"><span data-stu-id="b8555-138">Make note of hello appId (called 'client ID' elsewhere), name, password, and tenant for later use.</span></span>
    2. <span data-ttu-id="b8555-139">También necesitará el identificador de suscripción, que se puede ver con `az account list`</span><span class="sxs-lookup"><span data-stu-id="b8555-139">You will also need your subscription ID, which can be viewed with `az account list`</span></span>

<span data-ttu-id="b8555-140">biblioteca de cálculo fluida Hello puede iniciar una sesión con estas credenciales como se indica a continuación (tenga en cuenta que como tipos básicos de Azure fluida `IAzure` en hello [Microsoft.Azure.Management.Fluent](https://www.nuget.org/packages/Microsoft.Azure.Management.Fluent/) paquete):</span><span class="sxs-lookup"><span data-stu-id="b8555-140">hello fluent compute library can log in using these credentials as follows (note that core fluent Azure types like `IAzure` are in hello [Microsoft.Azure.Management.Fluent](https://www.nuget.org/packages/Microsoft.Azure.Management.Fluent/) package):</span></span>

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
    ServiceEventSource.Current.ServiceMessage(Context, "ERROR: Failed toologin tooAzure");
}
```

<span data-ttu-id="b8555-141">Una vez iniciada la sesión, el recuento de instancias de conjunto de escalado se puede consultar a través de `AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId).Capacity`.</span><span class="sxs-lookup"><span data-stu-id="b8555-141">Once logged in, scale set instance count can be queried via `AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId).Capacity`.</span></span>

## <a name="scaling-out"></a><span data-ttu-id="b8555-142">Escalado horizontal</span><span class="sxs-lookup"><span data-stu-id="b8555-142">Scaling out</span></span>
<span data-ttu-id="b8555-143">Mediante Hola fluida cálculo de Azure SDK, se pueden agregar instancias de escalas de máquina virtual de toohello establecer con unos pocos llamadas-</span><span class="sxs-lookup"><span data-stu-id="b8555-143">Using hello fluent Azure compute SDK, instances can be added toohello virtual machine scale set with just a few calls -</span></span>

```C#
var scaleSet = AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId);
var newCapacity = (int)Math.Min(MaximumNodeCount, scaleSet.Capacity + 1);
scaleSet.Update().WithCapacity(newCapacity).Apply(); 
``` 

<span data-ttu-id="b8555-144">Como alternativa, el tamaño del conjunto de escalado de máquinas virtuales también puede administrarse con cmdlets de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b8555-144">Alternatively, virtual machine scale set size can also be managed with PowerShell cmdlets.</span></span> <span data-ttu-id="b8555-145">[`Get-AzureRmVmss`](https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/get-azurermvmss)puede recuperar el objeto de conjunto de escala de hello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="b8555-145">[`Get-AzureRmVmss`](https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/get-azurermvmss) can retrieve hello virtual machine scale set object.</span></span> <span data-ttu-id="b8555-146">capacidad actual de Hola se almacenarán en hello `.sku.capacity` propiedad.</span><span class="sxs-lookup"><span data-stu-id="b8555-146">hello current capacity will be stored in hello `.sku.capacity` property.</span></span> <span data-ttu-id="b8555-147">Una vez hello toohello de capacidad de cambiar el valor deseado, escalas de máquina virtual de hello establecido en Azure pueden actualizarse con hello [ `Update-AzureRmVmss` ](https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/update-azurermvmss) comando.</span><span class="sxs-lookup"><span data-stu-id="b8555-147">After changing hello capacity toohello desired value, hello virtual machine scale set in Azure can be updated with hello [`Update-AzureRmVmss`](https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/update-azurermvmss) command.</span></span>

<span data-ttu-id="b8555-148">Como al agregar manualmente un nodo, agregar una escala establezca instancia debe estar todos los toostart necesario que incluye un nuevo nodo de Service Fabric ya que la plantilla de conjunto de escalado de Hola extensiones tooautomatically conectar el nuevo clúster de Service Fabric de toohello de instancias.</span><span class="sxs-lookup"><span data-stu-id="b8555-148">As when adding a node manually, adding a scale set instance should be all that's needed toostart a new Service Fabric node since hello scale set template includes extensions tooautomatically join new instances toohello Service Fabric cluster.</span></span> 

## <a name="scaling-in"></a><span data-ttu-id="b8555-149">Reducir horizontalmente</span><span class="sxs-lookup"><span data-stu-id="b8555-149">Scaling in</span></span>

<span data-ttu-id="b8555-150">Ajuste de escala en es similar tooscaling out. conjunto de escalas de máquina virtual real Hola cambios son prácticamente Hola igual.</span><span class="sxs-lookup"><span data-stu-id="b8555-150">Scaling in is similar tooscaling out. hello actual virtual machine scale set changes are practically hello same.</span></span> <span data-ttu-id="b8555-151">Pero, tal y como se ha descrito anteriormente, Service Fabric solo limpia automáticamente los nodos eliminados con una durabilidad Gold o Silver.</span><span class="sxs-lookup"><span data-stu-id="b8555-151">But, as was discussed previously, Service Fabric only automatically cleans up removed nodes with a durability of Gold or Silver.</span></span> <span data-ttu-id="b8555-152">Por lo tanto, en caso de escala Hola bronce durabilidad, es necesario toointeract con hello Service Fabric clúster tooshut hacia abajo Hola nodo toobe quitar y, a continuación, tooremove su estado.</span><span class="sxs-lookup"><span data-stu-id="b8555-152">So, in hello Bronze-durability scale-in case, it's necessary toointeract with hello Service Fabric cluster tooshut down hello node toobe removed and then tooremove its state.</span></span>

<span data-ttu-id="b8555-153">Preparando nodo de Hola para cierre implica buscar Hola nodo toobe quitó (nodo agregado más recientemente de hello) y desactivarla.</span><span class="sxs-lookup"><span data-stu-id="b8555-153">Preparing hello node for shutdown involves finding hello node toobe removed (hello most recently added node) and deactivating it.</span></span> <span data-ttu-id="b8555-154">Para nodos que no sean de raíz, se pueden encontrar nodos más recientes mediante la comparación de `NodeInstanceId`.</span><span class="sxs-lookup"><span data-stu-id="b8555-154">For non-seed nodes, newer nodes can be found by comparing `NodeInstanceId`.</span></span> 

```C#
using (var client = new FabricClient())
{
    var mostRecentLiveNode = (await client.QueryManager.GetNodeListAsync())
        .Where(n => n.NodeType.Equals(NodeTypeToScale, StringComparison.OrdinalIgnoreCase))
        .Where(n => n.NodeStatus == System.Fabric.Query.NodeStatus.Up)
        .OrderByDescending(n => n.NodeInstanceId)
        .FirstOrDefault();
```

<span data-ttu-id="b8555-155">Tenga en cuenta que *inicialización* nodos no parezcan tooalways siga la convención de Hola que primero se quitan los identificadores de instancia mayores.</span><span class="sxs-lookup"><span data-stu-id="b8555-155">Be aware that *seed* nodes don't seem tooalways follow hello convention that greater instance IDs are removed first.</span></span>

<span data-ttu-id="b8555-156">Una vez que se encuentra hello toobe de nodo quitado, se puede desactivar y quiten con Hola mismo `FabricClient` hello e instancia `IAzure` instancia a partir de versiones anteriores.</span><span class="sxs-lookup"><span data-stu-id="b8555-156">Once hello node toobe removed is found, it can be deactivated and removed using hello same `FabricClient` instance and hello `IAzure` instance from earlier.</span></span>

```C#
var scaleSet = AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId);

// Remove hello node from hello Service Fabric cluster
ServiceEventSource.Current.ServiceMessage(Context, $"Disabling node {mostRecentLiveNode.NodeName}");
await client.ClusterManager.DeactivateNodeAsync(mostRecentLiveNode.NodeName, NodeDeactivationIntent.RemoveNode);

// Wait (up tooa timeout) for hello node toogracefully shutdown
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

<span data-ttu-id="b8555-157">Como con el escalado, los cmdlets de PowerShell para la capacidad de modificación del conjunto de escalado de máquinas virtuales pueden usarse aquí si es preferible un enfoque de scripting.</span><span class="sxs-lookup"><span data-stu-id="b8555-157">As with scaling out, PowerShell cmdlets for modifying virtual machine scale set capacity can also be used here if a scripting approach is preferable.</span></span> <span data-ttu-id="b8555-158">Una vez que se quita la instancia de la máquina virtual de hello, se puede quitar el estado del nodo de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="b8555-158">Once hello virtual machine instance is removed, Service Fabric node state can be removed.</span></span>

```C#
await client.ClusterManager.RemoveNodeStateAsync(mostRecentLiveNode.NodeName);
```

## <a name="potential-drawbacks"></a><span data-ttu-id="b8555-159">Desventajas potenciales</span><span class="sxs-lookup"><span data-stu-id="b8555-159">Potential drawbacks</span></span>

<span data-ttu-id="b8555-160">Como se muestra en hello anterior fragmentos de código, crear su propio servicio de escalado proporciona comportamientos de escalado de hello mayor grado de control y personalización a través de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b8555-160">As demonstrated in hello preceding code snippets, creating your own scaling service provides hello highest degree of control and customizability over your application's scaling behavior.</span></span> <span data-ttu-id="b8555-161">Esto puede ser útil para escenarios que requieren un control preciso sobre cuándo y cómo una aplicación se escala o reduce horizontalmente. Sin embargo, este control acarrea el inconveniente de la complejidad del código.</span><span class="sxs-lookup"><span data-stu-id="b8555-161">This can be useful for scenarios requiring precise control over when or how an application scales in or out. However, this control comes with a tradeoff of code complexity.</span></span> <span data-ttu-id="b8555-162">Con este enfoque significa que necesita tooown ajuste de escala en código, lo que no es trivial.</span><span class="sxs-lookup"><span data-stu-id="b8555-162">Using this approach means that you need tooown scaling code, which is non-trivial.</span></span>

<span data-ttu-id="b8555-163">La forma en la que debe enfocar el escalado de Service Fabric depende de su escenario.</span><span class="sxs-lookup"><span data-stu-id="b8555-163">How you should approach Service Fabric scaling depends on your scenario.</span></span> <span data-ttu-id="b8555-164">Si el ajuste de escala es raro, Hola capacidad tooadd o quitar nodos manualmente es probablemente suficiente.</span><span class="sxs-lookup"><span data-stu-id="b8555-164">If scaling is uncommon, hello ability tooadd or remove nodes manually is probably sufficient.</span></span> <span data-ttu-id="b8555-165">Para escenarios más complejos, reglas de escalado automático y SDK exponer mediante programación Hola capacidad tooscale ofrece unas eficaces alternativas.</span><span class="sxs-lookup"><span data-stu-id="b8555-165">For more complex scenarios, auto-scale rules and SDKs exposing hello ability tooscale programmatically offer powerful alternatives.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b8555-166">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b8555-166">Next steps</span></span>

<span data-ttu-id="b8555-167">tooget comenzaron a implementar su propia lógica de escalado automático, familiarícese con hello siguientes conceptos y API útiles:</span><span class="sxs-lookup"><span data-stu-id="b8555-167">tooget started implementing your own auto-scaling logic, familiarize yourself with hello following concepts and useful APIs:</span></span>

- [<span data-ttu-id="b8555-168">Escalado manual o con reglas de escalado automático</span><span class="sxs-lookup"><span data-stu-id="b8555-168">Scaling manually or with auto-scale rules</span></span>](./service-fabric-cluster-scale-up-down.md)
- <span data-ttu-id="b8555-169">[Bibliotecas fluidas de administración de Azure para .NET](https://github.com/Azure/azure-sdk-for-net/tree/Fluent) (resulta útil para interactuar con los conjuntos de escalado de máquinas virtuales subyacentes de un clúster de Service Fabric)</span><span class="sxs-lookup"><span data-stu-id="b8555-169">[Fluent Azure Management Libraries for .NET](https://github.com/Azure/azure-sdk-for-net/tree/Fluent) (useful for interacting with a Service Fabric cluster's underlying virtual machine scale sets)</span></span>
- <span data-ttu-id="b8555-170">[System.Fabric.FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) (resulta útil para interactuar con un clúster de Service Fabric y sus nodos)</span><span class="sxs-lookup"><span data-stu-id="b8555-170">[System.Fabric.FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) (useful for interacting with a Service Fabric cluster and its nodes)</span></span>
