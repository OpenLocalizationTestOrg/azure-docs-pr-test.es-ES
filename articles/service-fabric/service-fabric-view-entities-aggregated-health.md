---
title: aaaHow tooview Azure Service Fabric entidades agregan mantenimiento | Documentos de Microsoft
description: "Describe cómo ver tooquery y evaluar el estado de las entidades de Azure Service Fabric agregados, a través de consultas de estado y consultas generales."
services: service-fabric
documentationcenter: .net
author: oanapl
manager: timlt
editor: 
ms.assetid: fa34c52d-3a74-4b90-b045-ad67afa43fe5
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2017
ms.author: oanapl
ms.openlocfilehash: add810551cac26d2b4ff81b57d94ddd780c2cc2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="view-service-fabric-health-reports"></a>Vista de los informes de estado de Service Fabric
Azure Service Fabric presenta un [modelo de mantenimiento](service-fabric-health-introduction.md) con entidades de estado en las que componentes y guardianes del sistema pueden notificar las condiciones locales que están supervisando. Hola [almacén de estado](service-fabric-health-introduction.md#health-store) agrega todos los toodetermine de datos de estado si las entidades están en buen estadas.

clúster de Hola se rellena automáticamente con los informes de estado enviados por componentes del sistema Hola. Más información, lea [tootroubleshoot de informes de mantenimiento del sistema de uso](service-fabric-understand-and-troubleshoot-with-system-health-reports.md).

Service Fabric proporciona varias maneras tooget Hola agregado mantenimiento de entidades de hello:

* [Explorador de Service Fabric](service-fabric-visualizing-your-cluster.md) y otras herramientas de visualización
* Consultas de mantenimiento (a través de PowerShell, API o REST)
* General, las consultas que devuelven una lista de entidades que tienen el estado como una de las propiedades de hello (a través de PowerShell, API o REST)

toodemonstrate estas opciones, vamos a usar un clúster local con cinco nodos y hello [fabric: / aplicación WordCount](http://aka.ms/servicefabric-wordcountapp). Hola **fabric: / WordCount** aplicación contiene dos servicios de manera predeterminada, un servicio con estado de tipo `WordCountServiceType`y un servicio sin estado de tipo `WordCountWebServiceType`. He cambiado hello `ApplicationManifest.xml` toorequire siete réplicas de destino para el servicio con estado hello y una partición. Porque hay solo cinco nodos en clúster de hello, componentes del sistema Hola notificar una advertencia en la partición de servicio de hello porque es inferior al recuento de destino de Hola.

```xml
<Service Name="WordCountService">
<<<<<<< HEAD
    <StatefulService ServiceTypeName="WordCountServiceType" TargetReplicaSetSize="7" MinReplicaSetSize="3">
      <UniformInt64Partition PartitionCount="1" LowKey="1" HighKey="26" />
    </StatefulService>
=======
  <StatefulService ServiceTypeName="WordCountServiceType" TargetReplicaSetSize="7" MinReplicaSetSize="2">
    <UniformInt64Partition PartitionCount="[WordCountService_PartitionCount]" LowKey="1" HighKey="26" />
  </StatefulService>
>>>>>>> 5e84dbdd8e45a5d6b36f435a550b7433b873bf11
</Service>
```

## <a name="health-in-service-fabric-explorer"></a>Mantenimiento del Explorador de Service Fabric
Explorador de Service Fabric proporciona una vista visual de clúster de Hola. En la imagen de hello siguiente, puede ver que:

* Hola aplicación **fabric: / WordCount** está en rojo (en error) porque tiene un evento de error notificado por **MyWatchdog** para la propiedad de hello **disponibilidad**.
* Uno de sus servicios, **fabric:/WordCount/WordCountService** está en amarillo (en advertencia). Hola servicio está configurado con siete réplicas y clúster de hello tiene cinco nodos, por lo que no se puede colocar dos repicas. Aunque no se muestra aquí, la partición de servicio de hello es amarilla debido a un informe del sistema de `System.FM` que indique que `Partition is below target replica or instance count`. desencadenadores de partición amarillo Hola Hola servicio amarillo.
* clúster de Hello es rojo debido a la aplicación hello rojo.

evaluación de Hello usa las directivas predeterminadas de manifiesto de clúster de Hola y el manifiesto de aplicación. Son directivas estrictas y no toleran ningún error.

Vista de clúster de hello con Service Fabric Explorer:

![Vista de clúster de hello con Service Fabric Explorer.][1]

[1]: ./media/service-fabric-view-entities-aggregated-health/servicefabric-explorer-cluster-health.png


> [!NOTE]
> Obtenga más información sobre el [Explorador de Service Fabric](service-fabric-visualizing-your-cluster.md).
>
>

## <a name="health-queries"></a>Consultas de mantenimiento
Service Fabric expone consultas de estado para cada uno de hello admitida [tipos de entidad](service-fabric-health-introduction.md#health-entities-and-hierarchy). Son accesibles a través de API, utilizando los métodos en hello [FabricClient.HealthManager](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthmanager?view=azure-dotnet), cmdlets de PowerShell y REST. Estas consultas devuelven información de estado acerca de la entidad de hello: Hola agrega el estado, los eventos de estado de entidad, Estados de mantenimiento de elemento secundario (si procede), evaluaciones en mal estado (cuando la entidad de hello no es correcto) y las estadísticas de estado de los elementos secundarios (cuando aplicable).

> [!NOTE]
> Una entidad de estado se devuelve cuando se completa en el almacén de estado de Hola. entidad de Hello debe estar activo (no eliminado) y tiene un informe de sistema. Sus entidades primario en la cadena de jerarquía de hello también deben tener informes del sistema. Si no se cumple alguna de estas condiciones, mantenimiento de hello las consultas devuelven un [FabricException](https://docs.microsoft.com/dotnet/api/system.fabric.fabricexception) con [FabricErrorCode](https://docs.microsoft.com/dotnet/api/system.fabric.fabricerrorcode) `FabricHealthEntityNotFound` que muestra por qué no se devuelve la entidad de Hola.
>
>

consultas de estado de Hello deben pasar el identificador de entidad de hello, que depende del tipo de entidad de Hola. las consultas de Hello aceptan parámetros de la directiva de mantenimiento opcional. Si no se especifica ninguna directiva de mantenimiento, Hola [las directivas de mantenimiento](service-fabric-health-introduction.md#health-policies) del manifiesto de clúster o una aplicación Hola se usan para la evaluación. Si Hola manifiestos no contienen una definición de las directivas de mantenimiento, directivas de mantenimiento de hello predeterminadas se usan para la evaluación. las directivas de mantenimiento de Hello predeterminado no tolerar los errores. las consultas de Hello también aceptan filtros para devolver solo los elementos secundarios parciales o eventos--hello las que respetan Hola filtros especificados. Otro filtro permite excluir las estadísticas de los elementos secundarios de Hola.

> [!NOTE]
> se aplican los filtros de salida de Hello en servidor hello, por lo que se reduce el tamaño de respuesta del mensaje de Hola. Se recomienda que utilice los filtros de salida de hello toolimit Hola datos devuelven, en lugar de aplican filtros en el lado del cliente de Hola.
>
>

Contiene el mantenimiento de la entidad:

* Hola estado agregado de entidad de Hola. Calculado por el almacén de estado de hello basándose en los informes de estado de entidad, Estados de mantenimiento de elemento secundario (si procede) y las directivas de mantenimiento. Lea más sobre la [evaluación del mantenimiento de entidades](service-fabric-health-introduction.md#health-evaluation).  
* Hola eventos de estado de una entidad de Hola.
* colección de Hola de Estados de mantenimiento de todos los elementos secundarios para las entidades de Hola que pueden tener elementos secundarios. Estados de mantenimiento de Hello contienen los identificadores de entidad y Hola estado agregado. tooget estado para un elemento secundario, llamar a estado de consulta de hello para el tipo de entidad de secundarios de Hola y pase identificador secundario de Hola.
* evaluaciones en mal estado Hello toohello de ese punto de informes que desencadenan estado de Hola de entidad de hello, si Hola entidad no es correcto. las evaluaciones de Hello son recursivos, que contiene evaluaciones del mantenimiento de los elementos secundarios Hola que desencadenó el estado de mantenimiento actual. Por ejemplo, un guardián notificó un error en una réplica. estado de la aplicación Hello muestra una evaluación incorrecto debido tooan servicio incorrecto; servicio de Hello está en mal estado vencimiento partición tooa error; partición de Hello está en mal estado vencimiento réplica tooa error; réplica de Hello está en mal estado debido a informes de estado de error de guardián toohello.
* estadísticas de estado de Hola para todos los tipos de elementos secundarios de entidades de Hola que tienen elementos secundarios. Por ejemplo, el estado del clúster muestra el número total de Hola de aplicaciones, servicios, particiones, las réplicas e implementa entidades de clúster de Hola. Estado del servicio muestra el número total de Hola de particiones y réplicas en hello servicio especificado.

## <a name="get-cluster-health"></a>Obtención del mantenimiento de clúster
Devuelve Hola mantenimiento de entidad de clúster de Hola y contiene los Estados de mantenimiento de Hola de aplicaciones y nodos (elementos secundarios del clúster de hello). Entrada:

* Directiva de mantenimiento de clúster [opcional] Hola utiliza nodos de hello tooevaluate y eventos de clúster de Hola.
* Asignación de directiva de mantenimiento de aplicación Hola [opcional], con las directivas de mantenimiento de hello usa directivas de manifiesto de aplicación de Hola de toooverride.
* [Opcional] Filtros de eventos, nodos y aplicaciones que especifican las entradas que son de interés y se deben devolver en el resultado de hello (por ejemplo, únicamente, los errores o las advertencias y errores). Todos los eventos, nodos y aplicaciones son mantenimiento de entidad agregado hello tooevaluate usado, independientemente del filtro de Hola.
* [Opcional] Filtrar las estadísticas de estado de tooexclude.
* [Opcional] Filtrar tooinclude fabric: / Hola de las estadísticas de estado del sistema en las estadísticas de estado. Solo se aplica cuando no se excluyen las estadísticas de estado de Hola. De forma predeterminada, las estadísticas de estado de Hola incluyen solo las estadísticas de las aplicaciones de usuario y aplicación del sistema no Hola.

### <a name="api"></a>API
tooget estado del clúster, cree una `FabricClient` llamada hello y [GetClusterHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getclusterhealthasync) método en su **HealthManager**.

Hello llamada siguiente obtiene el estado del clúster hello:

```csharp
ClusterHealth clusterHealth = await fabricClient.HealthManager.GetClusterHealthAsync();
```

Hola código siguiente obtiene el estado del clúster hello mediante una directiva de mantenimiento de clúster personalizado y filtra los nodos y aplicaciones. Especifica que las estadísticas de estado de hello incluyen tejido hello: / estadísticas del sistema. Crea [ClusterHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.clusterhealthquerydescription), que contiene información de entrada de Hola.

```csharp
var policy = new ClusterHealthPolicy()
{
    MaxPercentUnhealthyNodes = 20
};
var nodesFilter = new NodeHealthStatesFilter()
{
    HealthStateFilterValue = HealthStateFilter.Error | HealthStateFilter.Warning
};
var applicationsFilter = new ApplicationHealthStatesFilter()
{
    HealthStateFilterValue = HealthStateFilter.Error
};
var healthStatisticsFilter = new ClusterHealthStatisticsFilter()
{
    ExcludeHealthStatistics = false,
    IncludeSystemApplicationHealthStatistics = true
};
var queryDescription = new ClusterHealthQueryDescription()
{
    HealthPolicy = policy,
    ApplicationsFilter = applicationsFilter,
    NodesFilter = nodesFilter,
    HealthStatisticsFilter = healthStatisticsFilter
};

ClusterHealth clusterHealth = await fabricClient.HealthManager.GetClusterHealthAsync(queryDescription);
```

### <a name="powershell"></a>PowerShell
es el estado de clúster de Hola Hola cmdlet tooget [ServiceFabricClusterHealth Get](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterhealth). En primer lugar, conectar toohello clúster mediante el uso de hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.

Hola estado del clúster de hello es cinco nodos, la aplicación de sistema de Hola y fabric: / WordCount configurado como se describe.

Hola siguiendo el cmdlet Obtiene el estado del clúster mediante el uso de directivas de mantenimiento de forma predeterminada. Hello estado agregado una advertencia, ya que Hola fabric: / aplicación WordCount produce una advertencia. Tenga en cuenta cómo evaluaciones en mal estado Hola proporcionan detalles de las condiciones de Hola que desencadenó Hola agregado mantenimiento.

```xml
PS D:\ServiceFabric> Get-ServiceFabricClusterHealth


AggregatedHealthState   : Warning
UnhealthyEvaluations    : 
                          Unhealthy applications: 100% (1/1), MaxPercentUnhealthyApplications=0%.
                          
                          Unhealthy application: ApplicationName='fabric:/WordCount', AggregatedHealthState='Warning'.
                          
                            Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                          
                            Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Warning'.
                          
                                Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                          
                                Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Warning'.
                          
                                    Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                          
                          
NodeHealthStates        : 
                          NodeName              : _Node_4
                          AggregatedHealthState : Ok
                          
                          NodeName              : _Node_3
                          AggregatedHealthState : Ok
                          
                          NodeName              : _Node_2
                          AggregatedHealthState : Ok
                          
                          NodeName              : _Node_1
                          AggregatedHealthState : Ok
                          
                          NodeName              : _Node_0
                          AggregatedHealthState : Ok
                          
ApplicationHealthStates : 
                          ApplicationName       : fabric:/System
                          AggregatedHealthState : Ok
                          
                          ApplicationName       : fabric:/WordCount
                          AggregatedHealthState : Warning
                          
HealthEvents            : None
HealthStatistics        : 
                          Node                  : 5 Ok, 0 Warning, 0 Error
                          Replica               : 6 Ok, 0 Warning, 0 Error
                          Partition             : 1 Ok, 1 Warning, 0 Error
                          Service               : 1 Ok, 1 Warning, 0 Error
                          DeployedServicePackage : 6 Ok, 0 Warning, 0 Error
                          DeployedApplication   : 5 Ok, 0 Warning, 0 Error
                          Application           : 0 Ok, 1 Warning, 0 Error
```

Hello siguiente cmdlet de PowerShell obtiene Hola mantenimiento de clúster de hello mediante una directiva de aplicación personalizada. Filtra los resultados tooget sólo las aplicaciones y los nodos de error o advertencia. Como resultado, no se devuelve ningún nodo, ya que todos son correctos. Hola solo fabric: / aplicación WordCount respeta el filtro de aplicaciones de Hola. Directiva personalizada de hello especifica tooconsider advertencias como errores de tejido de hello: / aplicación WordCount, aplicación hello se evalúa como erróneo y, por lo que es clúster Hola.

```powershell
PS D:\ServiceFabric> $appHealthPolicy = New-Object -TypeName System.Fabric.Health.ApplicationHealthPolicy
$appHealthPolicy.ConsiderWarningAsError = $true
$appHealthPolicyMap = New-Object -TypeName System.Fabric.Health.ApplicationHealthPolicyMap
$appUri1 = New-Object -TypeName System.Uri -ArgumentList "fabric:/WordCount"
$appHealthPolicyMap.Add($appUri1, $appHealthPolicy)
Get-ServiceFabricClusterHealth -ApplicationHealthPolicyMap $appHealthPolicyMap -ApplicationsFilter "Warning,Error" -NodesFilter "Warning,Error" -ExcludeHealthStatistics


AggregatedHealthState   : Error
UnhealthyEvaluations    : 
                          Unhealthy applications: 100% (1/1), MaxPercentUnhealthyApplications=0%.
                          
                          Unhealthy application: ApplicationName='fabric:/WordCount', AggregatedHealthState='Error'.
                          
                            Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                          
                            Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Error'.
                          
                                Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                          
                                Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Error'.
                          
                                    Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=true.
                          
                          
NodeHealthStates        : None
ApplicationHealthStates : 
                          ApplicationName       : fabric:/WordCount
                          AggregatedHealthState : Error
                          
HealthEvents            : None
```

### <a name="rest"></a>REST
Puede obtener el estado del clúster con un [solicitud GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster) o un [solicitud POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster-by-using-a-health-policy) que incluye las directivas de mantenimiento que se describe en el cuerpo de Hola.

## <a name="get-node-health"></a>Obtención del mantenimiento de nodo
Devuelve Hola estado de una entidad del nodo y contiene eventos de estado de hello notificados en el nodo de Hola. Entrada:

* Nombre de nodo de hello [obligatorio] que identifica el nodo de Hola.
* Configuración de directiva de mantenimiento de clúster de hello [opcional] usa tooevaluate mantenimiento.
* [Opcional] Filtros para los eventos que especifican las entradas que son de interés y se deben devolver en el resultado de hello (por ejemplo, únicamente, los errores o las advertencias y errores). Todos los eventos son mantenimiento de entidad agregado hello tooevaluate usado, independientemente del filtro de Hola.

### <a name="api"></a>API
estado de nodo de tooget a través de hello API, cree un `FabricClient` llamada hello y [GetNodeHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getnodehealthasync) método en su HealthManager.

Hello código siguiente obtiene mantenimiento de nodo de hello para el nombre del nodo especificado de hello:

```csharp
NodeHealth nodeHealth = await fabricClient.HealthManager.GetNodeHealthAsync(nodeName);
```

Hello código siguiente obtiene el estado del nodo de Hola para hello especificado nombre de nodo y pasa en el filtro de eventos y una directiva personalizada a través de [NodeHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.nodehealthquerydescription):

```csharp
var queryDescription = new NodeHealthQueryDescription(nodeName)
{
    HealthPolicy = new ClusterHealthPolicy() {  ConsiderWarningAsError = true },
    EventsFilter = new HealthEventsFilter() { HealthStateFilterValue = HealthStateFilter.Warning },
};

NodeHealth nodeHealth = await fabricClient.HealthManager.GetNodeHealthAsync(queryDescription);
```

### <a name="powershell"></a>PowerShell
el estado del nodo Hola cmdlet tooget hello es [ServiceFabricNodeHealth Get](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricnodehealth). En primer lugar, conectar toohello clúster mediante el uso de hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.
Hola siguiente cmdlet Obtiene el mantenimiento de nodo de hello mediante el uso de directivas de mantenimiento de manera predeterminada:

```powershell
PS D:\ServiceFabric> Get-ServiceFabricNodeHealth _Node_1


NodeName              : _Node_1
AggregatedHealthState : Ok
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 3
                        SentAt                : 7/13/2017 4:39:23 PM
                        ReceivedAt            : 7/13/2017 4:40:47 PM
                        TTL                   : Infinite
                        Description           : Fabric node is up.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 4:40:47 PM, LastWarning = 1/1/0001 12:00:00 AM
```

Hello siguiente cmdlet obtiene Hola mantenimiento de todos los nodos de clúster de hello:

```powershell
PS D:\ServiceFabric> Get-ServiceFabricNode | Get-ServiceFabricNodeHealth | select NodeName, AggregatedHealthState | ft -AutoSize

NodeName AggregatedHealthState
-------- ---------------------
_Node_4                     Ok
_Node_3                     Ok
_Node_2                     Ok
_Node_1                     Ok
_Node_0                     Ok
```

### <a name="rest"></a>REST
Puede obtener el estado de nodo con un [solicitud GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-node) o un [solicitud POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-node-by-using-a-health-policy) que incluye las directivas de mantenimiento que se describe en el cuerpo de Hola.

## <a name="get-application-health"></a>Obtención del mantenimiento de la aplicación
Devuelve el estado de saludo de una entidad de la aplicación. Contiene los Estados de mantenimiento de Hola de aplicación hello implementado y elementos secundarios de servicio. Entrada:

* Hola [obligatorio] nombre de la aplicación (URI) que identifica la aplicación hello.
* Directiva de mantenimiento de aplicación Hola [opcional] usa directivas de manifiesto de aplicación de Hola de toooverride.
* [Opcional] Filtros de eventos, servicios y aplicaciones implementadas que especifican las entradas que son de interés y se deben devolver en el resultado de hello (por ejemplo, únicamente, los errores o las advertencias y errores). Todos los eventos, servicios y aplicaciones implementadas son mantenimiento de entidad agregado hello tooevaluate usado, independientemente del filtro de Hola.
* [Opcional] Filtrar las estadísticas de estado de hello tooexclude. Si no se especifica, las estadísticas de estado de hello incluyen Aceptar hello, de advertencia y de recuento de errores para todos los elementos secundarios de la aplicación: servicios, particiones, las réplicas, las aplicaciones implementadas y paquetes de servicio implementados.

### <a name="api"></a>API
estado de la aplicación de tooget, crear un `FabricClient` llamada hello y [GetApplicationHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getapplicationhealthasync) método en su HealthManager.

Hello código siguiente obtiene el estado de aplicaciones de hello para el nombre de aplicación especificado hello (URI):

```csharp
ApplicationHealth applicationHealth = await fabricClient.HealthManager.GetApplicationHealthAsync(applicationName);
```

Hello código siguiente obtiene el estado de aplicaciones de hello para el nombre de aplicación especificado hello (URI), con los filtros y las directivas personalizadas especifican a través de [ApplicationHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.applicationhealthquerydescription).

```csharp
HealthStateFilter warningAndErrors = HealthStateFilter.Error | HealthStateFilter.Warning;
var serviceTypePolicy = new ServiceTypeHealthPolicy()
{
    MaxPercentUnhealthyPartitionsPerService = 0,
    MaxPercentUnhealthyReplicasPerPartition = 5,
    MaxPercentUnhealthyServices = 0,
};
var policy = new ApplicationHealthPolicy()
{
    ConsiderWarningAsError = false,
    DefaultServiceTypeHealthPolicy = serviceTypePolicy,
    MaxPercentUnhealthyDeployedApplications = 0,
};

var queryDescription = new ApplicationHealthQueryDescription(applicationName)
{
    HealthPolicy = policy,
    EventsFilter = new HealthEventsFilter() { HealthStateFilterValue = warningAndErrors },
    ServicesFilter = new ServiceHealthStatesFilter() { HealthStateFilterValue = warningAndErrors },
    DeployedApplicationsFilter = new DeployedApplicationHealthStatesFilter() { HealthStateFilterValue = warningAndErrors },
};

ApplicationHealth applicationHealth = await fabricClient.HealthManager.GetApplicationHealthAsync(queryDescription);
```

### <a name="powershell"></a>PowerShell
es el estado de aplicaciones de Hola Hola cmdlet tooget [ServiceFabricApplicationHealth Get](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps). En primer lugar, conectar toohello clúster mediante el uso de hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.

Hello siguiente cmdlet devuelve mantenimiento Hola de hello **fabric: / WordCount** aplicación:

```powershell
PS D:\ServiceFabric> Get-ServiceFabricApplicationHealth fabric:/WordCount


ApplicationName                 : fabric:/WordCount
AggregatedHealthState           : Warning
UnhealthyEvaluations            : 
                                  Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                                  
                                  Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Warning'.
                                  
                                    Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                                  
                                    Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Warning'.
                                  
                                        Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                                  
ServiceHealthStates             : 
                                  ServiceName           : fabric:/WordCount/WordCountWebService
                                  AggregatedHealthState : Ok
                                  
                                  ServiceName           : fabric:/WordCount/WordCountService
                                  AggregatedHealthState : Warning
                                  
DeployedApplicationHealthStates : 
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_4
                                  AggregatedHealthState : Ok
                                  
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_3
                                  AggregatedHealthState : Ok
                                  
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_0
                                  AggregatedHealthState : Ok
                                  
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_2
                                  AggregatedHealthState : Ok
                                  
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_1
                                  AggregatedHealthState : Ok
                                  
HealthEvents                    : 
                                  SourceId              : System.CM
                                  Property              : State
                                  HealthState           : Ok
                                  SequenceNumber        : 282
                                  SentAt                : 7/13/2017 5:57:05 PM
                                  ReceivedAt            : 7/13/2017 5:57:05 PM
                                  TTL                   : Infinite
                                  Description           : Application has been created.
                                  RemoveWhenExpired     : False
                                  IsExpired             : False
                                  Transitions           : Error->Ok = 7/13/2017 5:57:05 PM, LastWarning = 1/1/0001 12:00:00 AM
                                  
HealthStatistics                : 
                                  Replica               : 6 Ok, 0 Warning, 0 Error
                                  Partition             : 1 Ok, 1 Warning, 0 Error
                                  Service               : 1 Ok, 1 Warning, 0 Error
                                  DeployedServicePackage : 6 Ok, 0 Warning, 0 Error
                                  DeployedApplication   : 5 Ok, 0 Warning, 0 Error
```

Hola siguiendo los pasos de cmdlet de PowerShell de directivas personalizadas. También filtra los elementos secundarios y los eventos.

```powershell
PS D:\ServiceFabric> Get-ServiceFabricApplicationHealth -ApplicationName fabric:/WordCount -ConsiderWarningAsError $true -ServicesFilter Error -EventsFilter Error -DeployedApplicationsFilter Error -ExcludeHealthStatistics


ApplicationName                 : fabric:/WordCount
AggregatedHealthState           : Error
UnhealthyEvaluations            : 
                                  Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                                  
                                  Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Error'.
                                  
                                    Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                                  
                                    Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Error'.
                                  
                                        Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=true.
                                  
ServiceHealthStates             : 
                                  ServiceName           : fabric:/WordCount/WordCountService
                                  AggregatedHealthState : Error
                                  
DeployedApplicationHealthStates : None
HealthEvents                    : None
```

### <a name="rest"></a>REST
Puede obtener el estado de aplicación con un [solicitud GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-an-application) o un [solicitud POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-an-application-by-using-an-application-health-policy) que incluye las directivas de mantenimiento que se describe en el cuerpo de Hola.

## <a name="get-service-health"></a>Obtención del mantenimiento del servicio
Devuelve el estado de saludo de una entidad de servicio. Contiene los Estados de mantenimiento de partición Hola. Entrada:

* Hola [obligatorio] nombre del servicio (URI) que identifica el servicio de Hola.
* Directiva de mantenimiento de aplicación Hola [opcional] usa la directiva del manifiesto de aplicación toooverride Hola.
* [Opcional] Filtros de eventos y las particiones que especifican las entradas que son de interés y se deben devolver en el resultado de hello (por ejemplo, únicamente, los errores o las advertencias y errores). Todos los eventos y las particiones son mantenimiento de entidad agregado hello tooevaluate usado, independientemente del filtro de Hola.
* [Opcional] Filtrar las estadísticas de estado de tooexclude. Si no se especifica, Hola Hola de mostrar las estadísticas de estado correcto, advertencia y error de recuento de todas las particiones y réplicas de servicio de Hola.

### <a name="api"></a>API
estado del servicio tooget a través de hello API, cree un `FabricClient` llamada hello y [GetServiceHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getservicehealthasync) método en su HealthManager.

Hello en el ejemplo siguiente se obtiene Hola mantenimiento de un servicio con el nombre de servicio especificado (URI):

```charp
ServiceHealth serviceHealth = await fabricClient.HealthManager.GetServiceHealthAsync(serviceName);
```

Hello código siguiente obtiene Hola estado del servicio para el nombre de servicio especificado de hello (URI), especificar filtros y una directiva personalizada a través de [ServiceHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.servicehealthquerydescription):

```csharp
var queryDescription = new ServiceHealthQueryDescription(serviceName)
{
    EventsFilter = new HealthEventsFilter() { HealthStateFilterValue = HealthStateFilter.All },
    PartitionsFilter = new PartitionHealthStatesFilter() { HealthStateFilterValue = HealthStateFilter.Error },
};

ServiceHealth serviceHealth = await fabricClient.HealthManager.GetServiceHealthAsync(queryDescription);
```

### <a name="powershell"></a>PowerShell
es el estado del servicio de Hello cmdlet tooget hello [ServiceFabricServiceHealth Get](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricservicehealth). En primer lugar, conectar toohello clúster mediante el uso de hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.

Hola siguiendo el cmdlet Obtiene el estado del servicio de hello mediante el uso de directivas de mantenimiento de manera predeterminada:

```powershell
PS D:\ServiceFabric> Get-ServiceFabricServiceHealth -ServiceName fabric:/WordCount/WordCountService


ServiceName           : fabric:/WordCount/WordCountService
AggregatedHealthState : Warning
UnhealthyEvaluations  : 
                        Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                        
                        Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Warning'.
                        
                            Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                        
PartitionHealthStates : 
                        PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
                        AggregatedHealthState : Warning
                        
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 15
                        SentAt                : 7/13/2017 5:57:05 PM
                        ReceivedAt            : 7/13/2017 5:57:18 PM
                        TTL                   : Infinite
                        Description           : Service has been created.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
                        
HealthStatistics      : 
                        Replica               : 5 Ok, 0 Warning, 0 Error
                        Partition             : 0 Ok, 1 Warning, 0 Error
```

### <a name="rest"></a>REST
Puede obtener el estado del servicio con un [solicitud GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service) o un [solicitud POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-by-using-a-health-policy) que incluye las directivas de mantenimiento que se describe en el cuerpo de Hola.

## <a name="get-partition-health"></a>Obtención del mantenimiento de partición
Devuelve el estado de saludo de una entidad de la partición. Contiene los Estados de mantenimiento de réplica de Hola. Entrada:

* Partición de hello [obligatorio] identificador (GUID) que identifica la partición de Hola.
* Directiva de mantenimiento de aplicación Hola [opcional] usa la directiva del manifiesto de aplicación toooverride Hola.
* [Opcional] Filtros de eventos y las réplicas que especifican las entradas que son de interés y se deben devolver en el resultado de hello (por ejemplo, únicamente, los errores o las advertencias y errores). Todos los eventos y réplicas son mantenimiento de entidad agregado hello tooevaluate usado, independientemente del filtro de Hola.
* [Opcional] Filtrar las estadísticas de estado de tooexclude. Si no se especifica, muestran las estadísticas de estado de hello cuántas réplicas están en Aceptar, advertencia y error de Estados.

### <a name="api"></a>API
estado de la partición de tooget a través de hello API, cree un `FabricClient` llamada hello y [GetPartitionHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getpartitionhealthasync) método en su HealthManager. crear parámetros opcionales toospecify [PartitionHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.partitionhealthquerydescription).

```csharp
PartitionHealth partitionHealth = await fabricClient.HealthManager.GetPartitionHealthAsync(partitionId);
```

### <a name="powershell"></a>PowerShell
Mantenimiento de partición de Hello cmdlet tooget hello es [ServiceFabricPartitionHealth Get](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricpartitionhealth). En primer lugar, conectar toohello clúster mediante el uso de hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.

Hello siguiente obtiene mantenimiento Hola para todas las particiones de hello **fabric: / WordCount/WordCountService** servicio y filtra los Estados de mantenimiento de réplica:

```powershell
PS D:\ServiceFabric> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | Get-ServiceFabricPartitionHealth -ReplicasFilter None

PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
AggregatedHealthState : Warning
UnhealthyEvaluations  : 
                        Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                        
ReplicaHealthStates   : None
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Warning
                        SequenceNumber        : 72
                        SentAt                : 7/13/2017 5:57:29 PM
                        ReceivedAt            : 7/13/2017 5:57:48 PM
                        TTL                   : Infinite
                        Description           : Partition is below target replica or instance count.
                        fabric:/WordCount/WordCountService 7 2 af2e3e44-a8f8-45ac-9f31-4093eb897600
                          N/P RD _Node_2 Up 131444422260002646
                          N/S RD _Node_4 Up 131444422293113678
                          N/S RD _Node_3 Up 131444422293113679
                          N/S RD _Node_1 Up 131444422293118720
                          N/S RD _Node_0 Up 131444422293118721
                          (Showing 5 out of 5 replicas. Total available replicas: 5.)
                        
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Ok->Warning = 7/13/2017 5:57:48 PM, LastError = 1/1/0001 12:00:00 AM
                        
                        SourceId              : System.PLB
                        Property              : ServiceReplicaUnplacedHealth_Secondary_af2e3e44-a8f8-45ac-9f31-4093eb897600
                        HealthState           : Warning
                        SequenceNumber        : 131444445174851664
                        SentAt                : 7/13/2017 6:35:17 PM
                        ReceivedAt            : 7/13/2017 6:35:18 PM
                        TTL                   : 00:01:05
                        Description           : hello Load Balancer was unable toofind a placement for one or more of hello Service's Replicas:
                        Secondary replica could not be placed due toohello following constraints and properties:  
                        TargetReplicaSetSize: 7
                        Placement Constraint: N/A
                        Parent Service: N/A
                        
                        Constraint Elimination Sequence:
                        Existing Secondary Replicas eliminated 4 possible node(s) for placement -- 1/5 node(s) remain.
                        Existing Primary Replica eliminated 1 possible node(s) for placement -- 0/5 node(s) remain.
                        
                        Nodes Eliminated By Constraints:
                        
                        Existing Secondary Replicas -- Nodes with Partition's Existing Secondary Replicas/Instances:
                        --
                        FaultDomain:fd:/4 NodeName:_Node_4 NodeType:NodeType4 UpgradeDomain:4 UpgradeDomain: ud:/4 Deactivation Intent/Status: None/None
                        FaultDomain:fd:/3 NodeName:_Node_3 NodeType:NodeType3 UpgradeDomain:3 UpgradeDomain: ud:/3 Deactivation Intent/Status: None/None
                        FaultDomain:fd:/1 NodeName:_Node_1 NodeType:NodeType1 UpgradeDomain:1 UpgradeDomain: ud:/1 Deactivation Intent/Status: None/None
                        FaultDomain:fd:/0 NodeName:_Node_0 NodeType:NodeType0 UpgradeDomain:0 UpgradeDomain: ud:/0 Deactivation Intent/Status: None/None
                        
                        Existing Primary Replica -- Nodes with Partition's Existing Primary Replica or Secondary Replicas:
                        --
                        FaultDomain:fd:/2 NodeName:_Node_2 NodeType:NodeType2 UpgradeDomain:2 UpgradeDomain: ud:/2 Deactivation Intent/Status: None/None
                        
                        
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : Error->Warning = 7/13/2017 5:57:48 PM, LastOk = 1/1/0001 12:00:00 AM
                        
HealthStatistics      : 
                        Replica               : 5 Ok, 0 Warning, 0 Error
```

### <a name="rest"></a>REST
Puede obtener el estado de la partición con un [solicitud GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-partition) o un [solicitud POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-partition-by-using-a-health-policy) que incluye las directivas de mantenimiento que se describe en el cuerpo de Hola.

## <a name="get-replica-health"></a>Obtención del mantenimiento de réplica
Devuelve el estado de saludo de una réplica de servicio con estado o una instancia de servicio sin estado. Entrada:

* [Obligatorio] Hola identificador (GUID) y la réplica Id. de partición que identifica la réplica de Hola.
* Parámetros de la directiva de mantenimiento de hello [opcional] aplicación utilizan directivas de manifiesto de aplicación de Hola de toooverride.
* [Opcional] Filtros para los eventos que especifican las entradas que son de interés y se deben devolver en el resultado de hello (por ejemplo, únicamente, los errores o las advertencias y errores). Todos los eventos son mantenimiento de entidad agregado hello tooevaluate usado, independientemente del filtro de Hola.

### <a name="api"></a>API
Mantenimiento de réplica de hello tooget a través de hello API, cree un `FabricClient` llamada hello y [GetReplicaHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getreplicahealthasync) método en su HealthManager. parámetros avanzados, uso de toospecify [ReplicaHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.replicahealthquerydescription).

```csharp
ReplicaHealth replicaHealth = await fabricClient.HealthManager.GetReplicaHealthAsync(partitionId, replicaId);
```

### <a name="powershell"></a>PowerShell
el estado de réplica de Hola Hola cmdlet tooget es [ServiceFabricReplicaHealth Get](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricreplicahealth). En primer lugar, conectar toohello clúster mediante el uso de hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.

Hello siguiente cmdlet obtiene Hola mantenimiento de réplica principal de Hola para todas las particiones del servicio de hello:

```powershell
PS D:\ServiceFabric> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | Get-ServiceFabricReplica | where {$_.ReplicaRole -eq "Primary"} | Get-ServiceFabricReplicaHealth


PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
ReplicaId             : 131444422260002646
AggregatedHealthState : Ok
HealthEvents          : 
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 131444422263668344
                        SentAt                : 7/13/2017 5:57:06 PM
                        ReceivedAt            : 7/13/2017 5:57:18 PM
                        TTL                   : Infinite
                        Description           : Replica has been created._Node_2
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="rest"></a>REST
Puede obtener el estado de réplica con un [solicitud GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-replica) o un [solicitud POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-replica-by-using-a-health-policy) que incluye las directivas de mantenimiento que se describe en el cuerpo de Hola.

## <a name="get-deployed-application-health"></a>Obtención del mantenimiento de la aplicación implementada
Devuelve el estado de saludo de una aplicación implementada en una entidad del nodo. Contiene Estados de mantenimiento de paquete de servicio de hello implementado. Entrada:

* Nombre de la aplicación hello [obligatorio] (URI) y el nombre de nodo (cadena) que identifican Hola implementan la aplicación.
* Directiva de mantenimiento de aplicación Hola [opcional] usa directivas de manifiesto de aplicación de Hola de toooverride.
* [Opcional] Filtros de eventos y paquetes de servicio implementado que especifican las entradas que son de interés y se deben devolver en el resultado de hello (por ejemplo, únicamente, los errores o las advertencias y errores). Todos los eventos y paquetes de servicio implementados son mantenimiento de entidad agregado hello tooevaluate usado, independientemente del filtro de Hola.
* [Opcional] Filtrar las estadísticas de estado de tooexclude. Si no se especifica, las estadísticas de estado de hello mostrarán número de Hola de paquetes de servicio implementados en los Estados de mantenimiento de Aceptar, advertencia y error.

### <a name="api"></a>API
estado de hello tooget de una aplicación implementada en un nodo a través de hello API, cree un `FabricClient` llamada hello y [GetDeployedApplicationHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getdeployedapplicationhealthasync) método en su HealthManager. toospecify parámetros opcionales, use [DeployedApplicationHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.deployedapplicationhealthquerydescription).

```csharp
DeployedApplicationHealth health = await fabricClient.HealthManager.GetDeployedApplicationHealthAsync(
    new DeployedApplicationHealthQueryDescription(applicationName, nodeName));
```

### <a name="powershell"></a>PowerShell
Hola estado de la aplicación de cmdlet tooget Hola implementado es [ServiceFabricDeployedApplicationHealth Get](/powershell/module/servicefabric/get-servicefabricdeployedapplicationhealth?view=azureservicefabricps). En primer lugar, conectar toohello clúster mediante el uso de hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet. toofind out donde se implementa una aplicación, ejecutar [ServiceFabricApplicationHealth Get](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps) y vistazo Hola implementa elementos secundarios de la aplicación.

Hello siguiente obtiene mantenimiento Hola de hello **fabric: / WordCount** aplicación implementada en **_Node_2**.

```powershell
PS D:\ServiceFabric> Get-ServiceFabricDeployedApplicationHealth -ApplicationName fabric:/WordCount -NodeName _Node_0


ApplicationName                    : fabric:/WordCount
NodeName                           : _Node_0
AggregatedHealthState              : Ok
DeployedServicePackageHealthStates : 
                                     ServiceManifestName   : WordCountServicePkg
                                     ServicePackageActivationId : 
                                     NodeName              : _Node_0
                                     AggregatedHealthState : Ok
                                     
                                     ServiceManifestName   : WordCountWebServicePkg
                                     ServicePackageActivationId : 
                                     NodeName              : _Node_0
                                     AggregatedHealthState : Ok
                                     
HealthEvents                       : 
                                     SourceId              : System.Hosting
                                     Property              : Activation
                                     HealthState           : Ok
                                     SequenceNumber        : 131444422261848308
                                     SentAt                : 7/13/2017 5:57:06 PM
                                     ReceivedAt            : 7/13/2017 5:57:17 PM
                                     TTL                   : Infinite
                                     Description           : hello application was activated successfully.
                                     RemoveWhenExpired     : False
                                     IsExpired             : False
                                     Transitions           : Error->Ok = 7/13/2017 5:57:17 PM, LastWarning = 1/1/0001 12:00:00 AM
                                     
HealthStatistics                   : 
                                     DeployedServicePackage : 2 Ok, 0 Warning, 0 Error
```

### <a name="rest"></a>REST
Puede obtener el estado de la aplicación implementada con un [solicitud GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-deployed-application) o un [solicitud POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-deployed-application-by-using-a-health-policy) que incluye las directivas de mantenimiento que se describe en el cuerpo de Hola.

## <a name="get-deployed-service-package-health"></a>Obtención del mantenimiento del paquete de servicio implementado
Devuelve Hola estado de una entidad de paquete de servicio implementado. Entrada:

* Nombre de la aplicación hello [obligatorio] (URI), nombre de nodo (cadena) y el nombre de manifiesto de servicio (cadena) que identifican Hola implementan el paquete de servicio.
* Directiva de mantenimiento de aplicación Hola [opcional] usa la directiva del manifiesto de aplicación toooverride Hola.
* [Opcional] Filtros para los eventos que especifican las entradas que son de interés y se deben devolver en el resultado de hello (por ejemplo, únicamente, los errores o las advertencias y errores). Todos los eventos son mantenimiento de entidad agregado hello tooevaluate usado, independientemente del filtro de Hola.

### <a name="api"></a>API
estado de hello tooget de un paquete de servicio implementado a través de hello API, cree un `FabricClient` llamada hello y [GetDeployedServicePackageHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getdeployedservicepackagehealthasync) método en su HealthManager. toospecify parámetros opcionales, use [DeployedServicePackageHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.deployedservicepackagehealthquerydescription).

```csharp
DeployedServicePackageHealth health = await fabricClient.HealthManager.GetDeployedServicePackageHealthAsync(
    new DeployedServicePackageHealthQueryDescription(applicationName, nodeName, serviceManifestName));
```

### <a name="powershell"></a>PowerShell
Hola mantenimiento del paquete de servicio de cmdlet tooget Hola implementado es [ServiceFabricDeployedServicePackageHealth Get](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricdeployedservicepackagehealth). En primer lugar, conectar toohello clúster mediante el uso de hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet. toosee donde se implementa una aplicación, ejecutar [ServiceFabricApplicationHealth Get](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps) y ver las aplicaciones de hello implementado. toosee que los paquetes de servicio están en una aplicación, busque en hello implementa elementos secundarios de paquete de servicio en hello [ServiceFabricDeployedApplicationHealth Get](/powershell/module/servicefabric/get-servicefabricdeployedapplicationhealth?view=azureservicefabricps) salida.

Hello siguiente obtiene mantenimiento Hola de hello **WordCountServicePkg** paquete del servicio de hello **fabric: / WordCount** aplicación implementada en **_Node_2**. entidad de Hello tiene **System.Hosting** informes para una activación correcta del paquete de servicio y punto de entrada y el registro de tipo de servicio correcta.

```powershell
PS D:\ServiceFabric> Get-ServiceFabricDeployedApplication -ApplicationName fabric:/WordCount -NodeName _Node_2 | Get-ServiceFabricDeployedServicePackageHealth -ServiceManifestName WordCountServicePkg


ApplicationName            : fabric:/WordCount
ServiceManifestName        : WordCountServicePkg
ServicePackageActivationId : 
NodeName                   : _Node_2
AggregatedHealthState      : Ok
HealthEvents               : 
                             SourceId              : System.Hosting
                             Property              : Activation
                             HealthState           : Ok
                             SequenceNumber        : 131444422267693359
                             SentAt                : 7/13/2017 5:57:06 PM
                             ReceivedAt            : 7/13/2017 5:57:18 PM
                             TTL                   : Infinite
                             Description           : hello ServicePackage was activated successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
                             
                             SourceId              : System.Hosting
                             Property              : CodePackageActivation:Code:EntryPoint
                             HealthState           : Ok
                             SequenceNumber        : 131444422267903345
                             SentAt                : 7/13/2017 5:57:06 PM
                             ReceivedAt            : 7/13/2017 5:57:18 PM
                             TTL                   : Infinite
                             Description           : hello CodePackage was activated successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
                             
                             SourceId              : System.Hosting
                             Property              : ServiceTypeRegistration:WordCountServiceType
                             HealthState           : Ok
                             SequenceNumber        : 131444422272458374
                             SentAt                : 7/13/2017 5:57:07 PM
                             ReceivedAt            : 7/13/2017 5:57:18 PM
                             TTL                   : Infinite
                             Description           : hello ServiceType was registered successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="rest"></a>REST
Puede obtener el estado del paquete de servicio implementado con un [solicitud GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-package) o un [solicitud POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-package-by-using-a-health-policy) que incluye las directivas de mantenimiento que se describe en el cuerpo de Hola.

## <a name="health-chunk-queries"></a>Consultas de fragmentos de mantenimiento
las consultas de fragmento de mantenimiento de Hello pueden devolver a elementos secundarios de clúster de varios niveles (recursivamente), por los filtros de entrada. Admite filtros avanzados que permiten una gran flexibilidad al elegir elementos secundarios de hello toobe devuelto. los filtros de Hello pueden especificar a elementos secundarios por identificador único de Hola o por otros identificadores de grupo o Estados de mantenimiento. De forma predeterminada, ningún elemento secundario se incluyen, como comandos de toohealth lugar que siempre incluyen a elementos secundarios de primer nivel.

Hola [consultas de estado](service-fabric-view-entities-aggregated-health.md#health-queries) devueltos elementos secundarios de primer nivel sólo de hello especificado entidad por filtros necesarios. Hola tooget los elementos secundarios de elementos secundarios de hello, debe llamar a las API de estado adicional para cada entidad de interés. De forma similar, mantenimiento de hello tooget de entidades específicas, debe llamar a mantenimiento de una API para cada entidad deseada. Hello fragmento consulta filtrado avanzado permite toorequest varios elementos de interés en una sola consulta, lo que minimiza el tamaño del mensaje de Hola y número de Hola de mensajes.

valor de Hola de consulta de fragmento de hello es que puede obtener el estado más entidades de clúster (potencialmente todas las entidades de clúster a partir de raíz necesario) en una llamada. Puede expresar consultas de mantenimiento complejas, por ejemplo:

* Devolver solo las aplicaciones con error y, para esas aplicaciones, incluir todos los servicios con advertencias o errores. Para los servicios devueltos, incluir todas las particiones.
* Devolver solo el estado de Hola de cuatro aplicaciones, especificado por sus nombres.
* Devolver solo Hola estado de las aplicaciones de un tipo de aplicación que desee.
* Devolver todas las entidades implementadas en un nodo. Devuelve todas las aplicaciones, todas las aplicaciones implementadas en el nodo especificado hello y todos los paquetes de servicio de hello implementado en ese nodo.
* Devolver todas las réplicas con error. Devuelve todas las aplicaciones, los servicios, las particiones y solo las réplicas con error.
* Devolver todas las aplicaciones. Para un servicio especificado, incluir todas las particiones.

Actualmente, la consulta de fragmento de mantenimiento de Hola se expone solo para la entidad de clúster de Hola. Devuelve un fragmento de estado del clúster, que contiene:

* estado de mantenimiento de clúster agregado Hola.
* lista de fragmento del estado de mantenimiento Hola de nodos que respeta los filtros de entrada.
* lista de fragmento del estado de mantenimiento Hola de aplicaciones que respetan los filtros de entrada. Cada fragmento de estado de mantenimiento de aplicación contiene una lista de fragmentos con todos los servicios que respetan los filtros de entrada y una lista de fragmentos con todas las aplicaciones implementadas que respeta los filtros de Hola. Igual para los elementos secundarios de hello de servicios y las aplicaciones implementadas. De esta manera, todas las entidades de clúster de hello pueden devolverse potencialmente si solicita de forma jerárquica.

### <a name="cluster-health-chunk-query"></a>Consulta de fragmentos de mantenimiento del clúster
Devuelve Hola mantenimiento de entidad de clúster de Hola y contiene fragmentos de estado de mantenimiento jerárquica Hola de los elementos secundarios necesarios. Entrada:

* Directiva de mantenimiento de clúster [opcional] Hola utiliza nodos de hello tooevaluate y eventos de clúster de Hola.
* Asignación de directiva de mantenimiento de aplicación Hola [opcional], con las directivas de mantenimiento de hello usa directivas de manifiesto de aplicación de Hola de toooverride.
* [Opcional] Filtros para los nodos y las aplicaciones que especifican las entradas que son de interés y se deben devolver en el resultado de hello. Hola filtros son tooan específico/grupo de entidad de entidades o entidades tooall aplicables en ese nivel. lista de Hola de filtros puede contener un filtro general o filtros para entidades de toofine detalle específico de identificadores devueltos por la consulta de Hola. Si está vacío, no se devuelven los elementos secundarios de Hola de forma predeterminada.
  Obtenga más información sobre filtros de hello en [NodeHealthStateFilter](https://docs.microsoft.com/dotnet/api/system.fabric.health.nodehealthstatefilter) y [ApplicationHealthStateFilter](https://docs.microsoft.com/dotnet/api/system.fabric.health.applicationhealthstatefilter). recursivamente de Hello aplicación filtros puede especificar filtros avanzados para los elementos secundarios.

resultado del fragmento de Hello incluye a los elementos secundarios de hello respetan los filtros de Hola.

Actualmente, consulta de fragmento de hello no devolver evaluaciones en mal estado o los eventos de la entidad. Esa información adicional se puede obtener mediante la consulta del estado de clúster existente de Hola.

### <a name="api"></a>API
estado del clúster tooget los fragmentos, cree un `FabricClient` llamada hello y [GetClusterHealthChunkAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getclusterhealthchunkasync) método en su **HealthManager**. Se puede pasar en [ClusterHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.clusterhealthchunkquerydescription) las directivas de mantenimiento de toodescribe y filtros avanzados.

Hello código siguiente obtiene fragmentos de mantenimiento de clúster con filtros avanzados.

```csharp
var queryDescription = new ClusterHealthChunkQueryDescription();
queryDescription.ApplicationFilters.Add(new ApplicationHealthStateFilter()
    {
        // Return applications only if they are in error
        HealthStateFilter = HealthStateFilter.Error
    });

// Return all replicas
var wordCountServiceReplicaFilter = new ReplicaHealthStateFilter()
    {
        HealthStateFilter = HealthStateFilter.All
    };

// Return all replicas and all partitions
var wordCountServicePartitionFilter = new PartitionHealthStateFilter()
    {
        HealthStateFilter = HealthStateFilter.All
    };
wordCountServicePartitionFilter.ReplicaFilters.Add(wordCountServiceReplicaFilter);

// For specific service, return all partitions and all replicas
var wordCountServiceFilter = new ServiceHealthStateFilter()
{
    ServiceNameFilter = new Uri("fabric:/WordCount/WordCountService"),
};
wordCountServiceFilter.PartitionFilters.Add(wordCountServicePartitionFilter);

// Application filter: for specific application, return no services except hello ones of interest
var wordCountApplicationFilter = new ApplicationHealthStateFilter()
    {
        // Always return fabric:/WordCount application
        ApplicationNameFilter = new Uri("fabric:/WordCount"),
    };
wordCountApplicationFilter.ServiceFilters.Add(wordCountServiceFilter);

queryDescription.ApplicationFilters.Add(wordCountApplicationFilter);

var result = await fabricClient.HealthManager.GetClusterHealthChunkAsync(queryDescription);
```

### <a name="powershell"></a>PowerShell
es el estado de clúster de Hola Hola cmdlet tooget [ServiceFabricClusterChunkHealth Get](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterhealthchunk). En primer lugar, conectar toohello clúster mediante el uso de hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.

Hello código siguiente obtiene nodos solo si están en Error excepto para un nodo específico, que siempre se debe devolver.

```xml
PS D:\ServiceFabric> $errorFilter = [System.Fabric.Health.HealthStateFilter]::Error;
$allFilter = [System.Fabric.Health.HealthStateFilter]::All;

$nodeFilter1 = New-Object System.Fabric.Health.NodeHealthStateFilter -Property @{HealthStateFilter=$errorFilter}
$nodeFilter2 = New-Object System.Fabric.Health.NodeHealthStateFilter -Property @{NodeNameFilter="_Node_1";HealthStateFilter=$allFilter}
# Create node filter list that will be passed in hello cmdlet
$nodeFilters = New-Object System.Collections.Generic.List[System.Fabric.Health.NodeHealthStateFilter]
$nodeFilters.Add($nodeFilter1)
$nodeFilters.Add($nodeFilter2)

Get-ServiceFabricClusterHealthChunk -NodeFilters $nodeFilters


HealthState                  : Warning
NodeHealthStateChunks        : 
                               TotalCount            : 1
                               
                               NodeName              : _Node_1
                               HealthState           : Ok
                               
ApplicationHealthStateChunks : None
```

Hola siguiendo el cmdlet obtiene fragmentos de clúster con los filtros de aplicación.

```xml
PS D:\ServiceFabric> $errorFilter = [System.Fabric.Health.HealthStateFilter]::Error;
$allFilter = [System.Fabric.Health.HealthStateFilter]::All;

# All replicas
$replicaFilter = New-Object System.Fabric.Health.ReplicaHealthStateFilter -Property @{HealthStateFilter=$allFilter}

# All partitions
$partitionFilter = New-Object System.Fabric.Health.PartitionHealthStateFilter -Property @{HealthStateFilter=$allFilter}
$partitionFilter.ReplicaFilters.Add($replicaFilter)

# For WordCountService, return all partitions and all replicas
$svcFilter1 = New-Object System.Fabric.Health.ServiceHealthStateFilter -Property @{ServiceNameFilter="fabric:/WordCount/WordCountService"}
$svcFilter1.PartitionFilters.Add($partitionFilter)

$svcFilter2 = New-Object System.Fabric.Health.ServiceHealthStateFilter -Property @{HealthStateFilter=$errorFilter}

$appFilter = New-Object System.Fabric.Health.ApplicationHealthStateFilter -Property @{ApplicationNameFilter="fabric:/WordCount"}
$appFilter.ServiceFilters.Add($svcFilter1)
$appFilter.ServiceFilters.Add($svcFilter2)

$appFilters = New-Object System.Collections.Generic.List[System.Fabric.Health.ApplicationHealthStateFilter]
$appFilters.Add($appFilter)

Get-ServiceFabricClusterHealthChunk -ApplicationFilters $appFilters


HealthState                  : Error
NodeHealthStateChunks        : None
ApplicationHealthStateChunks : 
                               TotalCount            : 1
                               
                               ApplicationName       : fabric:/WordCount
                               ApplicationTypeName   : WordCount
                               HealthState           : Error
                               ServiceHealthStateChunks : 
                                TotalCount            : 1
                               
                                ServiceName           : fabric:/WordCount/WordCountService
                                HealthState           : Error
                                PartitionHealthStateChunks : 
                                    TotalCount            : 1
                               
                                    PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
                                    HealthState           : Error
                                    ReplicaHealthStateChunks : 
                                        TotalCount            : 5
                               
                                        ReplicaOrInstanceId   : 131444422293118720
                                        HealthState           : Ok
                               
                                        ReplicaOrInstanceId   : 131444422293118721
                                        HealthState           : Ok
                               
                                        ReplicaOrInstanceId   : 131444422293113678
                                        HealthState           : Ok
                               
                                        ReplicaOrInstanceId   : 131444422293113679
                                        HealthState           : Ok
                               
                                        ReplicaOrInstanceId   : 131444422260002646
                                        HealthState           : Error
```

Hello siguiente cmdlet devuelve implementadas todas las entidades en un nodo.

```xml
PS D:\ServiceFabric> $errorFilter = [System.Fabric.Health.HealthStateFilter]::Error;
$allFilter = [System.Fabric.Health.HealthStateFilter]::All;

$dspFilter = New-Object System.Fabric.Health.DeployedServicePackageHealthStateFilter -Property @{HealthStateFilter=$allFilter}
$daFilter =  New-Object System.Fabric.Health.DeployedApplicationHealthStateFilter -Property @{HealthStateFilter=$allFilter;NodeNameFilter="_Node_2"}
$daFilter.DeployedServicePackageFilters.Add($dspFilter)

$appFilter = New-Object System.Fabric.Health.ApplicationHealthStateFilter -Property @{HealthStateFilter=$allFilter}
$appFilter.DeployedApplicationFilters.Add($daFilter)

$appFilters = New-Object System.Collections.Generic.List[System.Fabric.Health.ApplicationHealthStateFilter]
$appFilters.Add($appFilter)
Get-ServiceFabricClusterHealthChunk -ApplicationFilters $appFilters


HealthState                  : Error
NodeHealthStateChunks        : None
ApplicationHealthStateChunks : 
                               TotalCount            : 2
                               
                               ApplicationName       : fabric:/System
                               HealthState           : Ok
                               DeployedApplicationHealthStateChunks : 
                                TotalCount            : 1
                               
                                NodeName              : _Node_2
                                HealthState           : Ok
                                DeployedServicePackageHealthStateChunks :
                                    TotalCount            : 1
                               
                                    ServiceManifestName   : FAS
                                    ServicePackageActivationId : 
                                    HealthState           : Ok
                               
                               
                               
                               ApplicationName       : fabric:/WordCount
                               ApplicationTypeName   : WordCount
                               HealthState           : Error
                               DeployedApplicationHealthStateChunks : 
                                TotalCount            : 1
                               
                                NodeName              : _Node_2
                                HealthState           : Ok
                                DeployedServicePackageHealthStateChunks :
                                    TotalCount            : 1
                               
                                    ServiceManifestName   : WordCountServicePkg
                                    ServicePackageActivationId : 
                                    HealthState           : Ok
```

### <a name="rest"></a>REST
Puede obtener el fragmento de estado del clúster con un [solicitud GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster-using-health-chunks) o un [solicitud POST](https://docs.microsoft.com/rest/api/servicefabric/health-of-cluster) que incluye las directivas de mantenimiento y los filtros avanzados se describe en el cuerpo de Hola.

## <a name="general-queries"></a>Consultas generales
Las consultas generales devuelven una lista de entidades de Service Fabric de un tipo especificado. Estas propiedades se exponen a través de la API de hello (mediante los métodos de hello en **FabricClient.QueryManager**), cmdlets de PowerShell y REST. Estas consultas agregan subconsultas de varios componentes. Uno de ellos es hello [almacén de estado](service-fabric-health-introduction.md#health-store), que rellena Hola agrega el estado de mantenimiento para cada resultado de la consulta.  

> [!NOTE]
> Consultas generales devuelven Hola agregado el estado de entidad de hello y no contienen datos de estado enriquecido. Si una entidad no es correcto, puede seguir con estado consultas tooget toda su información de estado, incluidos los eventos y Estados de mantenimiento de secundarios, evaluaciones en mal estado.
>
>

Si las consultas generales devuelven un estado desconocido para una entidad, es posible que ese almacén de estado de hello no tiene datos completos sobre la entidad de Hola. También es posible que un almacén de estado de subconsulta toohello no era correcta (por ejemplo, se produjo un error de comunicación o se limitó el almacén de estado de hello). Realizar un seguimiento con una consulta de estado de entidad de Hola. Si la subconsulta Hola detectó errores transitorios, como problemas de red, es posible que pueda realizar esta consulta de seguimiento. Pueden también proporcionan más detalles de hello health store sobre por qué no se expone la entidad de Hola.

Hola las consultas que contienen **HealthState** para las entidades son:

* Lista de nodos: devuelve nodos de la lista de hello en clúster hello (paginado).
  * API: [FabricClient.QueryClient.GetNodeListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getnodelistasync)
  * PowerShell: Get-ServiceFabricNode.
* Lista de aplicaciones: devuelve una lista de aplicaciones en clúster de hello (paginado) Hola.
  * API: [FabricClient.QueryClient.GetApplicationListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationlistasync)
  * PowerShell: Get-ServiceFabricApplication.
* Lista de servicios: devuelve la lista de hello de servicios en una aplicación (paginado).
  * API: [FabricClient.QueryClient.GetServiceListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getservicelistasync)
  * PowerShell: Get-ServiceFabricService.
* Lista de particiones: devuelve la lista de Hola de particiones en un servicio (paginado).
  * API: [FabricClient.QueryClient.GetPartitionListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getpartitionlistasync)
  * PowerShell: Get-ServiceFabricPartition.
* La lista de réplicas: devuelve la lista de Hola de réplicas de una partición (paginado).
  * API: [FabricClient.QueryClient.GetReplicaListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getreplicalistasync)
  * PowerShell: Get-ServiceFabricReplica.
* Implementa la lista de aplicaciones: devuelve una lista de las aplicaciones implementadas en un nodo Hola.
  * API: [FabricClient.QueryClient.GetDeployedApplicationListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getdeployedapplicationlistasync)
  * PowerShell: Get-ServiceFabricDeployedApplication.
* Implementa lista de paquetes de servicio: devuelve una lista de paquetes de servicio en una aplicación implementada Hola.
  * API: [FabricClient.QueryClient.GetDeployedServicePackageListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getdeployedservicepackagelistasync)
  * PowerShell: Get-ServiceFabricDeployedApplication.

> [!NOTE]
> Algunas de las consultas de hello devuelven resultados paginados. Hello devuelto de estas consultas es una lista que se deriva de [PagedList<T>](https://docs.microsoft.com/dotnet/api/system.fabric.query.pagedlist-1). Si los resultados de hello no ajustan a un mensaje, se devuelve solo una página y un ContinuationToken que realiza un seguimiento de dónde ha detenido la enumeración. Continuar toocall Hola igual de consulta y pase un token de continuación de Hola de hello anterior tooget siguientes resultados de la consulta.
>
>

### <a name="examples"></a>Ejemplos
Hello código siguiente obtiene aplicaciones en mal estado hello en clúster de hello:

```csharp
var applications = fabricClient.QueryManager.GetApplicationListAsync().Result.Where(
  app => app.HealthState == HealthState.Error);
```

Hello siguiente cmdlet obtiene los detalles de la aplicación hello para el tejido de hello: / aplicación WordCount. Observe que el estado de mantenimiento está en advertencia.

```powershell
PS C:\> Get-ServiceFabricApplication -ApplicationName fabric:/WordCount

ApplicationName        : fabric:/WordCount
ApplicationTypeName    : WordCount
ApplicationTypeVersion : 1.0.0
ApplicationStatus      : Ready
HealthState            : Warning
ApplicationParameters  : { "WordCountWebService_InstanceCount" = "1";
                         "_WFDebugParams_" = "[{"ServiceManifestName":"WordCountWebServicePkg","CodePackageName":"Code","EntryPointType":"Main","Debug
                         ExePath":"C:\\Program Files (x86)\\Microsoft Visual Studio
                         14.0\\Common7\\Packages\\Debugger\\VsDebugLaunchNotify.exe","DebugArguments":" {74f7e5d5-71a9-47e2-a8cd-1878ec4734f1} -p
                         [ProcessId] -tid [ThreadId]","EnvironmentBlock":"_NO_DEBUG_HEAP=1\u0000"},{"ServiceManifestName":"WordCountServicePkg","CodeP
                         ackageName":"Code","EntryPointType":"Main","DebugExePath":"C:\\Program Files (x86)\\Microsoft Visual Studio
                         14.0\\Common7\\Packages\\Debugger\\VsDebugLaunchNotify.exe","DebugArguments":" {2ab462e6-e0d1-4fda-a844-972f561fe751} -p
                         [ProcessId] -tid [ThreadId]","EnvironmentBlock":"_NO_DEBUG_HEAP=1\u0000"}]" }
```

Hello siguiente cmdlet obtiene servicios Hola con un estado de error:

```powershell
PS D:\ServiceFabric> Get-ServiceFabricApplication | Get-ServiceFabricService | where {$_.HealthState -eq "Error"}


ServiceName            : fabric:/WordCount/WordCountService
ServiceKind            : Stateful
ServiceTypeName        : WordCountServiceType
IsServiceGroup         : False
ServiceManifestVersion : 1.0.0
HasPersistedState      : True
ServiceStatus          : Active
HealthState            : Error
```

## <a name="cluster-and-application-upgrades"></a>Actualización de clústeres y aplicaciones
Durante una actualización supervisada de clúster de Hola y de aplicación, Service Fabric comprueba tooensure de mantenimiento que todo es correcto. Si una entidad está en mal estada según se ha evaluado mediante el uso de las directivas de mantenimiento configurada, actualización Hola aplica siguiente acción de directivas específicas de la actualización toodetermine Hola. actualización de Hello puede ser tooallow en pausa interacción del usuario (por ejemplo, corregir las condiciones de error o cambiar las directivas) o lo puede revierten automáticamente toohello de versión anterior válida.

Durante una *clúster* actualización, puede obtener estado de actualización de clúster de Hola. estado de actualización de Hello incluye evaluaciones en mal estado, qué toowhat punto está en mal estado en el clúster de Hola. Si se revierte la actualización Hola debido a problemas de toohealth, estado de actualización de hello recuerda a motivos de mal estado último Hola. Esta información puede ayudar a los administradores a investigar qué salió mal después de la actualización de hello revertido o detenido.

De forma similar, durante un *aplicación* actualización, las evaluaciones en mal estado se encuentran en estado de actualización de aplicación Hola.

Hello siguiente muestra estado de actualización de aplicación Hola de un tejido modificado: / aplicación WordCount. Un guardián ha informado de un error en una de sus réplicas. actualización de Hello es gradual porque no se respeten la hello las comprobaciones de mantenimiento.

```powershell
PS C:\> Get-ServiceFabricApplicationUpgrade fabric:/WordCount

ApplicationName               : fabric:/WordCount
ApplicationTypeName           : WordCount
TargetApplicationTypeVersion  : 1.0.0.0
ApplicationParameters         : {}
StartTimestampUtc             : 4/21/2017 5:23:26 PM
FailureTimestampUtc           : 4/21/2017 5:23:37 PM
FailureReason                 : HealthCheck
UpgradeState                  : RollingBackInProgress
UpgradeDuration               : 00:00:23
CurrentUpgradeDomainDuration  : 00:00:00
CurrentUpgradeDomainProgress  : UD1

                                NodeName            : _Node_1
                                UpgradePhase        : Upgrading

                                NodeName            : _Node_2
                                UpgradePhase        : Upgrading

                                NodeName            : _Node_3
                                UpgradePhase        : PreUpgradeSafetyCheck
                                PendingSafetyChecks :
                                EnsurePartitionQuorum - PartitionId: 30db5be6-4e20-4698-8185-4bd7ca744020
NextUpgradeDomain             : UD2
UpgradeDomainsStatus          : { "UD1" = "Completed";
                                "UD2" = "Pending";
                                "UD3" = "Pending";
                                "UD4" = "Pending" }
UnhealthyEvaluations          :
                                Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.

                                  Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Error'.

                                      Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.

                                      Unhealthy partition: PartitionId='a1f83a35-d6bf-4d39-b90d-28d15f39599b', AggregatedHealthState='Error'.

                                          Unhealthy replicas: 20% (1/5), MaxPercentUnhealthyReplicasPerPartition=0%.

                                          Unhealthy replica: PartitionId='a1f83a35-d6bf-4d39-b90d-28d15f39599b',
                                  ReplicaOrInstanceId='131031502346844058', AggregatedHealthState='Error'.

                                              Error event: SourceId='DiskWatcher', Property='Disk'.

UpgradeKind                   : Rolling
RollingUpgradeMode            : UnmonitoredAuto
ForceRestart                  : False
UpgradeReplicaSetCheckTimeout : 00:15:00
```

Obtener más información acerca de hello [actualización de la aplicación de Service Fabric](service-fabric-application-upgrade.md).

## <a name="use-health-evaluations-tootroubleshoot"></a>Usar tootroubleshoot de evaluaciones de estado
Siempre que haya un problema con el clúster de Hola o una aplicación, mire toopinpoint de mantenimiento de clúster o una aplicación Hola cuál es el problema. evaluaciones en mal estado Hola proporcionan detalles sobre qué Hola desencadenadas mal estado actual. Si necesita, puede profundizar en mal estado secundario entidades tooidentify Hola causa.

Por ejemplo, considere una aplicación con un estado incorrecto porque hay un informe de errores en una de sus réplicas. Hello siguiente cmdlet de Powershell muestra evaluaciones en mal estado hello:

```powershell
PS D:\ServiceFabric> Get-ServiceFabricApplicationHealth fabric:/WordCount -EventsFilter None -ServicesFilter None -DeployedApplicationsFilter None -ExcludeHealthStatistics


ApplicationName                 : fabric:/WordCount
AggregatedHealthState           : Error
UnhealthyEvaluations            : 
                                  Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                                  
                                  Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Error'.
                                  
                                    Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                                  
                                    Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Error'.
                                  
                                        Unhealthy replicas: 20% (1/5), MaxPercentUnhealthyReplicasPerPartition=0%.
                                  
                                        Unhealthy replica: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', ReplicaOrInstanceId='131444422260002646', AggregatedHealthState='Error'.
                                  
                                            Error event: SourceId='MyWatchdog', Property='Memory'.
                                  
ServiceHealthStates             : None
DeployedApplicationHealthStates : None
HealthEvents                    : None
```

Puede mirar Hola réplica tooget obtener más información:

```powershell
PS D:\ServiceFabric> Get-ServiceFabricReplicaHealth -ReplicaOrInstanceId 131444422260002646 -PartitionId af2e3e44-a8f8-45ac-9f31-4093eb897600


PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
ReplicaId             : 131444422260002646
AggregatedHealthState : Error
UnhealthyEvaluations  : 
                        Error event: SourceId='MyWatchdog', Property='Memory'.
                        
HealthEvents          : 
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 131444422263668344
                        SentAt                : 7/13/2017 5:57:06 PM
                        ReceivedAt            : 7/13/2017 5:57:18 PM
                        TTL                   : Infinite
                        Description           : Replica has been created._Node_2
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
                        
                        SourceId              : MyWatchdog
                        Property              : Memory
                        HealthState           : Error
                        SequenceNumber        : 131444451657749403
                        SentAt                : 7/13/2017 6:46:05 PM
                        ReceivedAt            : 7/13/2017 6:46:05 PM
                        TTL                   : Infinite
                        Description           : 
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Warning->Error = 7/13/2017 6:46:05 PM, LastOk = 1/1/0001 12:00:00 AM
```

> [!NOTE]
> Hello evaluaciones en mal estado Mostrar hello primer motivo Hola entidad es evalúa toocurrent estado de mantenimiento. Puede haber varios otros eventos que desencadenan este estado, pero no se reflejan en las evaluaciones de Hola. tooget obtener más información, explorar en profundidad en hello mantenimiento entidades toofigure todos los informes de hello incorrecto en clúster de Hola.
>
>

## <a name="next-steps"></a>Pasos siguientes
[Usar tootroubleshoot de informes de estado de sistema](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)

[Incorporación de informes de mantenimiento de Service Fabric personalizados](service-fabric-report-health.md)

[¿Cómo tooreport y comprobación de estado de servicio](service-fabric-diagnostics-how-to-report-and-check-service-health.md)

[Supervisión y diagnóstico de los servicios localmente](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[Actualización de la aplicación de Service Fabric](service-fabric-application-upgrade.md)
