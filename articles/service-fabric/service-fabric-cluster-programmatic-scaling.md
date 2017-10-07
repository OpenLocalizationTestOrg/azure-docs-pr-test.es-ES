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
# <a name="scale-a-service-fabric-cluster-programmatically"></a>Escalado mediante programación de un clúster de Service Fabric 

Los aspectos básicos del escalado de un clúster de Service Fabric en Azure se tratan en la documentación sobre [escalado de clústeres](./service-fabric-cluster-scale-up-down.md). Ese artículo trata sobre como los clústeres de Service Fabric se basan en conjuntos de escalado de máquinas virtuales y se pueden escalar de forma manual o mediante reglas de escalado automático. En este documento se examinan los métodos programáticos de coordinación de operaciones de escalado de Azure para escenarios más avanzados. 

## <a name="reasons-for-programmatic-scaling"></a>Motivos para el escalado mediante programación
En muchos escenarios, el escalado de forma manual o mediante reglas de escalado automático son buenas soluciones. Sin embargo, en otros escenarios, no pueden ser Hola ajustarse a la derecha. Entre los posibles inconvenientes toothese enfoques se incluyen:

- Escala manual requiere toolog en y ajuste de escala en las operaciones de solicitud de forma explícita. Si las operaciones de escalado se requieren con frecuencia o en momentos imprevisibles, este enfoque puede no ser una buena solución.
- Cuando las reglas de escalado automático quitan una instancia de un conjunto de escalas de máquina virtual, quita automáticamente conocimientos de ese nodo de clúster de Service Fabric Hola asociado a menos que el tipo de nodo de hello tiene un nivel de durabilidad de plata y oro. Dado que las reglas de escalado automático funcionan a establecer el nivel de escala de hello (en lugar de en el nivel de Service Fabric hello), reglas de escalado automático pueden quitar nodos de Service Fabric sin ellos cerrarse correctamente. Esta eliminación forzada de un nodo dejará un estado de nodo de Service Fabric "fantasma" después de operaciones de escalado. Una persona (o un servicio) necesitaría tooperiodically limpiar el estado de los nodos quitados en clúster de Service Fabric Hola.
  - Tenga en cuenta que un tipo de nodo con un nivel de durabilidad Gold o Silver limpiará automáticamente los nodos eliminados.  
- Aunque hay [muchas métricas](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md) compatibles con las reglas de escalado automático, se trata aún de un conjunto limitado. Si su escenario requiere un escalado automático basado en alguna métrica que no se trata en ese conjunto, es posible que las reglas de escalado automático no sean una buena opción.

En función de estas limitaciones, es recomendable tooimplement más automática escala modelos personalizados. 

## <a name="scaling-apis"></a>API de escalado
Las API de Azure existen que permiten que el trabajo de tooprogrammatically de aplicaciones con conjuntos de escalas de máquina virtual y clústeres de Service Fabric. Si las opciones existentes de escala automática no funcionan para su escenario, estas API puede hacerla lógica de ajuste de escala personalizada tooimplement posibles. 

Tooimplementing un enfoque esto 'principal-realizados' escalado automático funcionalidad es tooadd un nuevo toomanage de la aplicación de Service Fabric de toohello servicio sin estado operaciones de ajuste de escala. Dentro del servicio de hello `RunAsync` método, un conjunto de desencadenadores puede determinar si el ajuste de escala es necesaria (incluida la comprobación de parámetros como el tamaño máximo del clúster y ajuste de escala en cooldowns).   

Hola API que se utiliza para las interacciones de conjunto de escala de máquina virtual (ambos toocheck Hola actual en número de instancias de máquina virtual y toomodify lo) es hello [biblioteca fluida de procesos de administración de Azure](https://www.nuget.org/packages/Microsoft.Azure.Management.Compute.Fluent/). biblioteca de cálculo fluida de Hello proporciona una API de fácil de usar para interactuar con los conjuntos de escalas de máquina virtual.

usar toointeract con clúster de Service Fabric hello, [System.Fabric.FabricClient](/dotnet/api/system.fabric.fabricclient).

Por supuesto, no es necesario Hola escalar código toorun como un servicio en hello clúster toobe escalada. Ambos `IAzure` y `FabricClient` puede conectarse a tootheir asociado Azure recursos de forma remota, por lo Hola escalar servicio puede ser fácilmente una aplicación de consola o ejecutando desde la aplicación de Service Fabric de hello fuera de servicio de Windows. 

## <a name="credential-management"></a>Administración de credenciales
Presenta la dificultad de la escritura de una escala de toohandle de servicio es que el servicio de hello debe ser recursos de conjunto de escala de tooaccess capaz de máquina virtual sin un inicio de sesión interactivo. Acceso a Hola Service Fabric clúster es fácil si Hola escalar servicio modificando su propia aplicación de Service Fabric, pero las credenciales son necesarias tooaccess Hola conjunto de escala. toolog en, puede usar un [entidad de servicio](https://github.com/Azure/azure-sdk-for-net/blob/Fluent/AUTH.md#creating-a-service-principal-in-azure) creado con hello [CLI de Azure 2.0](https://github.com/azure/azure-cli).

Una entidad de servicio puede crearse con hello pasos:

1. Inicie sesión en toohello CLI de Azure (`az login`) como un usuario con escala de máquinas virtuales de acceso toohello conjunto
2. Crear servicio Hola principal con`az ad sp create-for-rbac`
    1. Tome nota del appId hello (denominada 'ID de cliente' en otro lugar), nombre, contraseña e inquilino para su uso posterior.
    2. También necesitará el identificador de suscripción, que se puede ver con `az account list`

biblioteca de cálculo fluida Hello puede iniciar una sesión con estas credenciales como se indica a continuación (tenga en cuenta que como tipos básicos de Azure fluida `IAzure` en hello [Microsoft.Azure.Management.Fluent](https://www.nuget.org/packages/Microsoft.Azure.Management.Fluent/) paquete):

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

Una vez iniciada la sesión, el recuento de instancias de conjunto de escalado se puede consultar a través de `AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId).Capacity`.

## <a name="scaling-out"></a>Escalado horizontal
Mediante Hola fluida cálculo de Azure SDK, se pueden agregar instancias de escalas de máquina virtual de toohello establecer con unos pocos llamadas-

```C#
var scaleSet = AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId);
var newCapacity = (int)Math.Min(MaximumNodeCount, scaleSet.Capacity + 1);
scaleSet.Update().WithCapacity(newCapacity).Apply(); 
``` 

Como alternativa, el tamaño del conjunto de escalado de máquinas virtuales también puede administrarse con cmdlets de PowerShell. [`Get-AzureRmVmss`](https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/get-azurermvmss)puede recuperar el objeto de conjunto de escala de hello máquina virtual. capacidad actual de Hola se almacenarán en hello `.sku.capacity` propiedad. Una vez hello toohello de capacidad de cambiar el valor deseado, escalas de máquina virtual de hello establecido en Azure pueden actualizarse con hello [ `Update-AzureRmVmss` ](https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/update-azurermvmss) comando.

Como al agregar manualmente un nodo, agregar una escala establezca instancia debe estar todos los toostart necesario que incluye un nuevo nodo de Service Fabric ya que la plantilla de conjunto de escalado de Hola extensiones tooautomatically conectar el nuevo clúster de Service Fabric de toohello de instancias. 

## <a name="scaling-in"></a>Reducir horizontalmente

Ajuste de escala en es similar tooscaling out. conjunto de escalas de máquina virtual real Hola cambios son prácticamente Hola igual. Pero, tal y como se ha descrito anteriormente, Service Fabric solo limpia automáticamente los nodos eliminados con una durabilidad Gold o Silver. Por lo tanto, en caso de escala Hola bronce durabilidad, es necesario toointeract con hello Service Fabric clúster tooshut hacia abajo Hola nodo toobe quitar y, a continuación, tooremove su estado.

Preparando nodo de Hola para cierre implica buscar Hola nodo toobe quitó (nodo agregado más recientemente de hello) y desactivarla. Para nodos que no sean de raíz, se pueden encontrar nodos más recientes mediante la comparación de `NodeInstanceId`. 

```C#
using (var client = new FabricClient())
{
    var mostRecentLiveNode = (await client.QueryManager.GetNodeListAsync())
        .Where(n => n.NodeType.Equals(NodeTypeToScale, StringComparison.OrdinalIgnoreCase))
        .Where(n => n.NodeStatus == System.Fabric.Query.NodeStatus.Up)
        .OrderByDescending(n => n.NodeInstanceId)
        .FirstOrDefault();
```

Tenga en cuenta que *inicialización* nodos no parezcan tooalways siga la convención de Hola que primero se quitan los identificadores de instancia mayores.

Una vez que se encuentra hello toobe de nodo quitado, se puede desactivar y quiten con Hola mismo `FabricClient` hello e instancia `IAzure` instancia a partir de versiones anteriores.

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

Como con el escalado, los cmdlets de PowerShell para la capacidad de modificación del conjunto de escalado de máquinas virtuales pueden usarse aquí si es preferible un enfoque de scripting. Una vez que se quita la instancia de la máquina virtual de hello, se puede quitar el estado del nodo de Service Fabric.

```C#
await client.ClusterManager.RemoveNodeStateAsync(mostRecentLiveNode.NodeName);
```

## <a name="potential-drawbacks"></a>Desventajas potenciales

Como se muestra en hello anterior fragmentos de código, crear su propio servicio de escalado proporciona comportamientos de escalado de hello mayor grado de control y personalización a través de la aplicación. Esto puede ser útil para escenarios que requieren un control preciso sobre cuándo y cómo una aplicación se escala o reduce horizontalmente. Sin embargo, este control acarrea el inconveniente de la complejidad del código. Con este enfoque significa que necesita tooown ajuste de escala en código, lo que no es trivial.

La forma en la que debe enfocar el escalado de Service Fabric depende de su escenario. Si el ajuste de escala es raro, Hola capacidad tooadd o quitar nodos manualmente es probablemente suficiente. Para escenarios más complejos, reglas de escalado automático y SDK exponer mediante programación Hola capacidad tooscale ofrece unas eficaces alternativas.

## <a name="next-steps"></a>Pasos siguientes

tooget comenzaron a implementar su propia lógica de escalado automático, familiarícese con hello siguientes conceptos y API útiles:

- [Escalado manual o con reglas de escalado automático](./service-fabric-cluster-scale-up-down.md)
- [Bibliotecas fluidas de administración de Azure para .NET](https://github.com/Azure/azure-sdk-for-net/tree/Fluent) (resulta útil para interactuar con los conjuntos de escalado de máquinas virtuales subyacentes de un clúster de Service Fabric)
- [System.Fabric.FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) (resulta útil para interactuar con un clúster de Service Fabric y sus nodos)
