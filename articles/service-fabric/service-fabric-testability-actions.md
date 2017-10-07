---
title: errores de aaaSimulate en Azure microservicios | Documentos de Microsoft
description: "En este artículo se habla sobre acciones de capacidad de prueba de Hola que se encuentran en Microsoft Azure Service Fabric."
services: service-fabric
documentationcenter: .net
author: motanv
manager: timlt
editor: toddabel
ms.assetid: ed53ca5c-4d5e-4b48-93c9-e386f32d8b7a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/07/2017
ms.author: motanv;heeldin
ms.openlocfilehash: 5bdda1c0c5a40b243ab956c4791afd52e11c4089
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="testability-actions"></a>Acciones de Testability
En orden toosimulate una infraestructura confiable, Azure Service Fabric usted como desarrollador de hello, con formas toosimulate proporciona varios errores reales y las transiciones de estado. Dichas formas se exponen como acciones de Testability. acciones de Hola se Hola API de bajo nivel que provocan una inyección de código de error concreto, la transición de estado o la validación. Mediante la combinación de estas acciones, puede escribir escenarios de prueba completos para los servicios.

Service Fabric proporciona varios escenarios de prueba comunes que constan de estas acciones. Se recomienda encarecidamente que use estos escenarios integrados, que se eligen cuidadosamente las transiciones de estado comunes tootest y casos de error. Sin embargo, las acciones pueden ser toocreate usado escenarios de prueba personalizada si desea tooadd cobertura para escenarios que no están cubiertas por escenarios integrados Hola aún o que son personalizadas adaptadas a su aplicación.

Las implementaciones de C# de acciones de Hola se encuentran en hello System.Fabric.dll ensamblado. se encuentra el módulo de PowerShell de tejido de sistema de Hola Hola Microsoft.ServiceFabric.Powershell.dll ensamblado. Como parte de la instalación de en tiempo de ejecución, Hola módulo ServiceFabric PowerShell está instalado tooallow para facilitar su uso.

## <a name="graceful-vs-ungraceful-fault-actions"></a>Acciones de errores estables frente a inestables
Las acciones de Testability se clasifican en dos cubos principales:

* Errores inestables: simulan errores como reinicios de equipos y bloqueos de procesos. En tales casos de errores, contexto de ejecución de hello del proceso se detiene repentinamente. Esto significa que no puede ejecutar ninguna limpieza del estado de hello antes de aplicación hello vuelve a empezar.
* Errores estables: simulan acciones estables como movimientos y eliminaciones de réplicas desencadenados por el equilibrio de carga. En tales casos, el servicio de hello recibe una notificación de hello cerrar y puede limpiar el estado de hello antes de salir.

En la validación de mejor calidad, ejecute el servicio de Hola y carga de trabajo de negocios durante la inducción de diversos errores estable e incorrectas. Errores incorrectas actúan sobre escenarios donde el proceso del servicio de hello cierra abruptamente en medio de Hola de algunos flujos de trabajo. Esto permite probar la ruta de recuperación de hello una vez restaurado réplicas del servicio Hola por Service Fabric. Esto le ayudará a probar la coherencia de los datos y si se mantiene el estado de servicio de hello correctamente después de los errores. Hello otro conjunto de errores (Hola estable de errores) de prueba que el servicio de hello reacciona correctamente tooreplicas que se mueven por Service Fabric. Esto permite probar tratamiento de cancelación en el método de hello Coredispatcher. servicio de Hello necesita toocheck para hello cancelación símbolo (token) que se va a establecer, guardar correctamente su estado y salir del método de hello Coredispatcher.

## <a name="testability-actions-list"></a>Lista de acciones de Testability
| Acción | Descripción | API administrada | Cmdlet de PowerShell | Errores estables o no estables |
| --- | --- | --- | --- | --- |
| CleanTestState |Quita todos los Estados de prueba de Hola de clúster de hello en el caso de un cierre incorrecto del controlador de pruebas de Hola. |CleanTestStateAsync |Remove-ServiceFabricTestState |No aplicable |
| InvokeDataLoss |Provoca la pérdida de datos en una partición del servicio. |InvokeDataLossAsync |Invoke-ServiceFabricPartitionDataLoss |Estable |
| InvokeQuorumLoss |Coloca una partición determinada del servicio con estado en pérdida de quórum. |InvokeQuorumLossAsync |Invoke-ServiceFabricQuorumLoss |Estable |
| Move Primary |Se desplaza Hola había especificado réplica principal de un nodo de clúster especificado de servicio con estado toohello. |MovePrimaryAsync |Move-ServiceFabricPrimaryReplica |Estable |
| Move Secondary |Mueve la réplica secundaria actual de Hola de servicio con estado tooa otro nodo de clúster. |MoveSecondaryAsync |Move-ServiceFabricSecondaryReplica |Estable |
| RemoveReplica |Simula un error de réplica mediante la eliminación de una réplica de un clúster. Esto cerrará la réplica de Hola y realizará la transición se toorole 'None', quitar todo su estado de clúster de Hola. |RemoveReplicaAsync |Remove-ServiceFabricReplica |Estable |
| RestartDeployedCodePackage |Simula un error de proceso del paquete de código mediante el reinicio de un paquete de código implementado en un nodo de un clúster. Esto anula el proceso de paquete de código de hello, que se reiniciará todas las réplicas de servicio de usuario de hello hospedadas en ese proceso. |RestartDeployedCodePackageAsync |Restart-ServiceFabricDeployedCodePackage |Inestable |
| RestartNode |Simula un error de nodo de clúster de Service Fabric mediante el reinicio de un nodo. |RestartNodeAsync |Restart-ServiceFabricNode |Inestable |
| RestartPartition |Simula un escenario de falta de disponibilidad del centro de datos o una falta de disponibilidad del clúster mediante el reinicio de algunas o todas las réplicas de una partición. |RestartPartitionAsync |Restart-ServiceFabricPartition |Estable |
| RestartReplica |Simula un error de réplica al reiniciar una réplica almacenada en un clúster, cerrar réplica hello y, a continuación, volver a abrirlo. |RestartReplicaAsync |Restart-ServiceFabricReplica |Estable |
| StartNode |Inicia un nodo en un clúster que se ha detenido. |StartNodeAsync |Start-ServiceFabricNode |No aplicable |
| StopNode |Simula un error de nodo mediante la detención de un nodo en un clúster. nodo de Hello permanecerá hacia abajo hasta que se llama StartNode. |StopNodeAsync |Stop-ServiceFabricNode |Inestable |
| ValidateApplication |Valida la disponibilidad de Hola y el estado de todos los servicios de Service Fabric dentro de una aplicación, normalmente después de inducción de algunos errores en el sistema de Hola. |ValidateApplicationAsync |Test-ServiceFabricApplication |No aplicable |
| ValidateService |Valida la disponibilidad de Hola y el estado de un servicio de Service Fabric, normalmente después de inducción de algunos errores en el sistema de Hola. |ValidateServiceAsync |Test-ServiceFabricService |No aplicable |

## <a name="running-a-testability-action-using-powershell"></a>Ejecución de una acción de Testability con PowerShell
Este tutorial muestra cómo toorun una acción de la capacidad de prueba mediante el uso de PowerShell. Obtendrá información sobre cómo toorun una acción de la capacidad de prueba en un clúster (cuadro de uno) local o en un clúster de Azure. Microsoft.Fabric.Powershell.dll--hello módulo de PowerShell de tejido de servicio--se instala automáticamente al instalar Hola MSI de tejido de servicio de Microsoft. módulo de Hola se carga automáticamente cuando se abre un símbolo del sistema de PowerShell.

Secciones del tutorial:

* [Ejecución de una acción en un clúster one-box](#run-an-action-against-a-one-box-cluster)
* [Ejecución de una acción en un clúster de Azure](#run-an-action-against-an-azure-cluster)

### <a name="run-an-action-against-a-one-box-cluster"></a>Ejecución de una acción en un clúster one-box
toorun una acción de la capacidad de prueba en un clúster local, primero conecte toohello clúster y símbolo del sistema de PowerShell de hello abierto en modo de administrador. Echemos un vistazo en hello **ServiceFabricNode reinicio** acción.

```powershell
Restart-ServiceFabricNode -NodeName Node1 -CompletionMode DoNotVerify
```

Hola aquí acción **ServiceFabricNode reinicio** se está ejecutando en un nodo denominado "Nodo1". modo de finalización de Hello especifica que no debe comprobar si acción de reinicio del nodo de Hola se ha realizado correctamente. Especificar el modo de finalización hello como "Verificar" hará que se tooverify si realmente se realizó correctamente la acción de reinicio de Hola. En lugar de especificar directamente el nodo de Hola por su nombre, puede especificar esta a través de un tipo de partición de hello y clave de réplica, como se indica a continuación:

```powershell
Restart-ServiceFabricNode -ReplicaKindPrimary  -PartitionKindNamed -PartitionKey Partition3 -CompletionMode Verify
```


```powershell
$connection = "localhost:19000"
$nodeName = "Node1"

Connect-ServiceFabricCluster $connection
Restart-ServiceFabricNode -NodeName $nodeName -CompletionMode DoNotVerify
```

**Reinicio ServiceFabricNode** debe ser un nodo de Service Fabric en un clúster de toorestart usado. Este comando detiene el proceso Fabric.exe de hello, que se reiniciará todos Hola sistema servicio y usuario servicio réplicas hospedadas en ese nodo. Mediante este tootest API su servicio ayuda a detectar los errores a lo largo de las rutas de recuperación de conmutación por error de Hola. Ayuda a simular errores en los nodos de clúster de Hola.

Hello captura de pantalla siguiente muestra hello **ServiceFabricNode reinicio** comando de capacidad de prueba de acción.

![](media/service-fabric-testability-actions/Restart-ServiceFabricNode.png)

Hola de salida de hello primero **ServiceFabricNode Get** (un cmdlet del módulo de PowerShell de tejido de servicio de hello) muestra ese clúster local hello tiene cinco nodos: Node.1 tooNode.5. Después de la acción de capacidad de prueba de hello (cmdlet) **ServiceFabricNode reinicio** se ejecuta en el nodo de hello, denominado Node.4, vemos se ha restablecido el tiempo de actividad de ese nodo Hola.

### <a name="run-an-action-against-an-azure-cluster"></a>Ejecución de una acción en un clúster de Azure
Ejecutar una acción de la capacidad de prueba (mediante el uso de PowerShell) en un clúster de Azure es la acción de hello toorunning similar en un clúster local. Hello solo diferencia es que para poder ejecutar la acción de hello, en lugar de conexión toohello clúster local, deberá tooconnect toohello Azure primero del clúster.

## <a name="running-a-testability-action-using-c35"></a>Ejecución de una acción de Testability con C&#35;
toorun una acción de la capacidad de prueba mediante el uso de C#, primero debe tooconnect toohello clúster mediante el uso de FabricClient. A continuación, obtener Hola parámetros necesarios toorun Hola acción. Parámetros diferentes que pueden utilizarse toorun Hola misma acción.
Examinando hello RestartServiceFabricNode acción, una manera de toorun es mediante el uso de información del nodo hello (nombre de nodo e Id. de instancia de nodo) en clúster de Hola.

```csharp
RestartNodeAsync(nodeName, nodeInstanceId, completeMode, operationTimeout, CancellationToken.None)
```

Explicación de parámetros:

* **CompleteMode** especifica que el modo de hello no debe comprobar si acción de reinicio de Hola se ha realizado correctamente. Especificar el modo de finalización hello como "Verificar" hará que se tooverify si realmente se realizó correctamente la acción de reinicio de Hola.  
* **OperationTimeout** conjuntos Hola cantidad de tiempo para hello operación toofinish antes de que se produce una excepción TimeoutException.
* **CancellationToken** permite un toobe pendiente llamada cancelada.

En lugar de especificar directamente el nodo de Hola por su nombre, puede especificar esta a través de un tipo de hello y clave de partición de réplica.

Para obtener más información, consulte [PartitionSelector y ReplicaSelector](#partition_replica_selector).

```csharp
// Add a reference tooSystem.Fabric.Testability.dll and System.Fabric.dll
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Fabric.Testability;
using System.Fabric;
using System.Threading;
using System.Numerics;

class Test
{
    public static int Main(string[] args)
    {
        string clusterConnection = "localhost:19000";
        Uri serviceName = new Uri("fabric:/samples/PersistentToDoListApp/PersistentToDoListService");
        string nodeName = "N0040";
        BigInteger nodeInstanceId = 130743013389060139;

        Console.WriteLine("Starting RestartNode test");
        try
        {
            //Restart hello node by using ReplicaSelector
            RestartNodeAsync(clusterConnection, serviceName).Wait();

            //Another way toorestart node is by using nodeName and nodeInstanceId
            RestartNodeAsync(clusterConnection, nodeName, nodeInstanceId).Wait();
        }
        catch (AggregateException exAgg)
        {
            Console.WriteLine("RestartNode did not complete: ");
            foreach (Exception ex in exAgg.InnerExceptions)
            {
                if (ex is FabricException)
                {
                    Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
                }
            }
            return -1;
        }

        Console.WriteLine("RestartNode completed.");
        return 0;
    }

    static async Task RestartNodeAsync(string clusterConnection, Uri serviceName)
    {
        PartitionSelector randomPartitionSelector = PartitionSelector.RandomOf(serviceName);
        ReplicaSelector primaryofReplicaSelector = ReplicaSelector.PrimaryOf(randomPartitionSelector);

        // Create FabricClient with connection and security information here
        FabricClient fabricclient = new FabricClient(clusterConnection);
        await fabricclient.FaultManager.RestartNodeAsync(primaryofReplicaSelector, CompletionMode.Verify);
    }

    static async Task RestartNodeAsync(string clusterConnection, string nodeName, BigInteger nodeInstanceId)
    {
        // Create FabricClient with connection and security information here
        FabricClient fabricclient = new FabricClient(clusterConnection);
        await fabricclient.FaultManager.RestartNodeAsync(nodeName, nodeInstanceId, CompletionMode.Verify);
    }
}
```

## <a name="partitionselector-and-replicaselector"></a>PartitionSelector y ReplicaSelector
### <a name="partitionselector"></a>PartitionSelector
PartitionSelector es una aplicación auxiliar que se exponen en la capacidad de prueba y se tooselect usado un determinado crear particiones en qué tooperform cualquiera de las acciones de capacidad de prueba de Hola. Puede ser usado tooselect una partición específica si Hola Id. de partición se conoce de antemano. O bien, puede proporcionar la clave de partición de Hola y operación Hola resolverá el Id. de partición de hello internamente. También tiene Hola opción de seleccionar una partición aleatoria.

toouse esta función auxiliar, crear hello PartitionSelector objeto y seleccione partición hello mediante uno de los métodos de hello Select *. A continuación, pasar en hello PartitionSelector objeto toohello API que lo requiera. Si no se selecciona ninguna opción, el valor predeterminado es tooa aleatorio partición.

```csharp
Uri serviceName = new Uri("fabric:/samples/InMemoryToDoListApp/InMemoryToDoListService");
Guid partitionIdGuid = new Guid("8fb7ebcc-56ee-4862-9cc0-7c6421e68829");
string partitionName = "Partition1";
Int64 partitionKeyUniformInt64 = 1;

// Select a random partition
PartitionSelector randomPartitionSelector = PartitionSelector.RandomOf(serviceName);

// Select a partition based on ID
PartitionSelector partitionSelectorById = PartitionSelector.PartitionIdOf(serviceName, partitionIdGuid);

// Select a partition based on name
PartitionSelector namedPartitionSelector = PartitionSelector.PartitionKeyOf(serviceName, partitionName);

// Select a partition based on partition key
PartitionSelector uniformIntPartitionSelector = PartitionSelector.PartitionKeyOf(serviceName, partitionKeyUniformInt64);
```

### <a name="replicaselector"></a>ReplicaSelector
ReplicaSelector es una aplicación auxiliar que se exponen en la capacidad de prueba y se usa toohelp seleccione una réplica en qué tooperform cualquiera de las acciones de capacidad de prueba de Hola. Puede ser tooselect usa una réplica específica si Hola Id. de réplica se conoce de antemano. Además, tiene Hola opción de seleccionar una réplica principal o secundaria aleatoria. ReplicaSelector se deriva de los PartitionSelector, por lo que necesita tooselect ambos Hola hello y réplica de partición en la que desea operación de capacidad de prueba de tooperform Hola.

toouse esta función auxiliar, cree un objeto de ReplicaSelector y establezca Hola que quieras particiones de réplica y Hola Hola tooselect. A continuación, puede pasar en hello API que lo requiera. Si no se selecciona ninguna opción, el valor predeterminado es tooa aleatorio réplica y partición aleatoria.

```csharp
Guid partitionIdGuid = new Guid("8fb7ebcc-56ee-4862-9cc0-7c6421e68829");
PartitionSelector partitionSelector = PartitionSelector.PartitionIdOf(serviceName, partitionIdGuid);
long replicaId = 130559876481875498;

// Select a random replica
ReplicaSelector randomReplicaSelector = ReplicaSelector.RandomOf(partitionSelector);

// Select hello primary replica
ReplicaSelector primaryReplicaSelector = ReplicaSelector.PrimaryOf(partitionSelector);

// Select hello replica by ID
ReplicaSelector replicaByIdSelector = ReplicaSelector.ReplicaIdOf(partitionSelector, replicaId);

// Select a random secondary replica
ReplicaSelector secondaryReplicaSelector = ReplicaSelector.RandomSecondaryOf(partitionSelector);
```

## <a name="next-steps"></a>Pasos siguientes
* [Escenarios de Testability](service-fabric-testability-scenarios.md)
* Cómo tootest su servicio
  * [Simulación de errores durante las cargas de trabajo del servicio](service-fabric-testability-workload-tests.md)
  * [Errores de comunicación entre servicios](service-fabric-testability-scenarios-service-communication.md)

