---
title: aaaTroubleshoot con informes de mantenimiento del sistema | Documentos de Microsoft
description: "Describe los informes de mantenimiento de hello enviados por los componentes del tejido de servicio de Azure y su uso de clúster para solucionar problemas o problemas de la aplicación."
services: service-fabric
documentationcenter: .net
author: oanapl
manager: timlt
editor: 
ms.assetid: 52574ea7-eb37-47e0-a20a-101539177625
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2017
ms.author: oanapl
ms.openlocfilehash: c77a6cdd0440ce5d354cd8760f40151f674a3529
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-system-health-reports-tootroubleshoot"></a>Usar tootroubleshoot de informes de estado de sistema
Azure Service Fabric componentes informe fuera del cuadro de hello en todas las entidades de clúster de Hola. Hola [almacén de estado](service-fabric-health-introduction.md#health-store) crea y elimina las entidades basándose en los informes del sistema Hola. También las organiza en una jerarquía que captura las interacciones de la entidad.

> [!NOTE]
> más información, lea los conceptos relacionados con el estado de toounderstand, [modelo de estado de Service Fabric](service-fabric-health-introduction.md).
> 
> 

Los informes de mantenimiento del sistema proporcionan visibilidad en el clúster y funcionalidad de la aplicación, así como indican problemas a través del mantenimiento. Para aplicaciones y servicios, informes de mantenimiento del sistema comprueban que las entidades se implementan y se comportan correctamente desde la perspectiva de Service Fabric Hola. informes de Hello no proporcionan ninguna supervisión de estado de lógica de negocios de Hola de servicio de Hola o detección de procesos bloqueados. Servicios de usuario pueden enriquecer datos de estado de hello con lógica de tootheir específico de información.

> [!NOTE]
> Solo están visibles los informes de mantenimiento de watchdogs *después* componentes del sistema Hola crean una entidad. Cuando se elimina una entidad, almacén de estado de hello elimina automáticamente todos los informes de estado asociados a él. Hello mismo puede decirse cuando se crea una nueva instancia de entidad de hello (por ejemplo, se crea una nueva instancia de réplica de servicio persistente con estado). Todos los informes asociados a la instancia anterior de Hola se elimina y se limpian del almacén de Hola.
> 
> 

informes de componentes de sistema Hello se identifican una origen de hello, que empieza por hello "**System.**" . Watchdogs no puede usar Hola igual de prefijo para sus orígenes, tal y como se rechazan los informes con parámetros no válidos.
Echemos un vistazo a algún sistema notifica toounderstand lo que les activa y cómo toocorrect Hola posibles problemas que representan.

> [!NOTE]
> Service Fabric continúa tooadd informes en las condiciones de interés que mejoran la visibilidad de lo que ocurre en el clúster Hola y de aplicación. También se pueden mejorar los informes existentes con más detalles toohelp solucionar problema Hola con mayor rapidez.
> 
> 

## <a name="cluster-system-health-reports"></a>Informes de mantenimiento del sistema de clúster
entidad de mantenimiento del clúster de Hola se crea automáticamente en el almacén de estado de Hola. Si todo funciona correctamente, no tiene un informe del sistema.

### <a name="neighborhood-loss"></a>Pérdida de entorno
**System.Federation** notifica un error cuando detecta una pérdida de entorno. informe de Hello procede de los nodos individuales e Id. de nodo de Hola se incluye en el nombre de la propiedad de Hola. Si se pierde un entorno en anillo de Service Fabric todo hello, normalmente pueden esperar dos eventos (ambos lados del informe de brechas de hello). Si se pierden más entornos, se producen más eventos.

informe de Hello especifica el tiempo de espera de hello concesión global como hora de hello toolive. informe de Hola se vuelve a enviar cada media de duración TTL de Hola para como condición de hello permanece activa. evento de Hola se quita automáticamente cuando esta expire. Quitar al comportamiento expirada garantiza que el informe de Hola se limpia del almacén de estado de hello correctamente, incluso si Hola informes nodo está inactivo.

* **SourceId**: System.Federation
* **Propiedad**: comienza por **Neighborhood** e incluye información sobre el nodo.
* **Pasos siguientes**: investigar por qué entorno Hola se pierde (por ejemplo, verificación Hola comunicación entre nodos del clúster).

## <a name="node-system-health-reports"></a>Informes de mantenimiento del sistema de nodos
**System.FM**, que representa el servicio de administrador de conmutación por error de hello, es la autoridad de Hola que administra información acerca de los nodos de clúster. Todos los nodos deben tener un informe de System.FM que muestre el estado. entidades de nodo de Hola se quitan cuando se quita el estado del nodo hello (vea [RemoveNodeStateAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.clustermanagementclient.removenodestateasync)).

### <a name="node-updown"></a>Nodo activo o inactivo
System.FM notifica como Aceptar cuando une a nodo Hola anillo hello (está en funcionamiento). Notifica un error al nodo de hello sale anillo hello (no funciona, ya sea para actualizar o simplemente porque se produjo un error). jerarquía de estado de Hello generado con el almacén de estado de hello realiza una acción sobre entidades implementadas en correlación con los informes del nodo System.FM. Considera que el nodo de Hola de un elemento primario virtual de todas las entidades implementadas. entidades de Hello implementado en ese nodo se exponen a través de las consultas si el nodo de Hola se notifica como seguridad por System.FM, con hello misma instancia como instancia de hello asociada con entidades de Hola. Cuando System.FM notifica ese nodo Hola está inactivo o reiniciado (una nueva instancia), almacén de estado de Hola se limpia automáticamente los entidades de hello implementado que pueden existir sólo en hello hacia abajo del nodo o en la instancia anterior de hello del nodo de Hola.

* **SourceId**: System.FM
* **Property**: State
* **Pasos siguientes**: si el nodo de hello está inactivo para realizar una actualización, debería vuelven a estar en una vez que se ha actualizado. En este caso, el estado de mantenimiento de hello debería pasar tooOK atrás. Si el nodo de hello no vuelven a estar o se produce un error, problema de hello necesita más investigación.

Hello en el ejemplo siguiente se muestra eventos de hello System.FM con un estado de mantenimiento de Aceptar de nodo:

```powershell
PS C:\> Get-ServiceFabricNodeHealth  _Node_0

NodeName              : _Node_0
AggregatedHealthState : Ok
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 8
                        SentAt                : 7/14/2017 4:54:51 PM
                        ReceivedAt            : 7/14/2017 4:55:14 PM
                        TTL                   : Infinite
                        Description           : Fabric node is up.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
```


### <a name="certificate-expiration"></a>Caducidad del certificado
**System.FabricNode** emite una advertencia cuando los certificados usados por nodo de hello son van a caducar. Hay tres certificados por nodo: **Certificate_cluster**, **Certificate_server** y **Certificate_default_client**. Una vez expiración Hola al menos dos semanas, estado de mantenimiento de informes de hello es correcto. Una vez expiración Hola menos de dos semanas, el tipo de informe de hello es una advertencia. TTL de estos eventos es infinito, y se quitan cuando sale de un nodo de clúster de Hola.

* **SourceId**: System.FabricNode
* **Propiedad**: comienza con **certificado** y contiene más información sobre el tipo de certificado de Hola
* **Pasos siguientes**: actualizar certificados de hello si fueran van a caducar.

### <a name="load-capacity-violation"></a>Infracción de la capacidad de carga
Hola equilibrador de carga de tejido de servicio emite una advertencia cuando detecta una infracción de la capacidad de nodo.

* **SourceId**: System.PLB
* **Property**: comienza por **Capacity**.
* **Pasos siguientes**: comprobación proporciona métricas y la vista capacidad actual de hello en el nodo de Hola.

## <a name="application-system-health-reports"></a>Informes de mantenimiento del sistema de la aplicación
**System.CM**, que representa el servicio de administrador de clústeres de hello, es la autoridad de Hola que administra información acerca de una aplicación.

### <a name="state"></a>Estado
System.CM notifica como correcto cuando la aplicación hello se ha creado o actualizado. Informa al almacén de estado de hello cuando se ha eliminado la aplicación hello, por lo que se puede quitar del almacén.

* **SourceId**: System.CM
* **Property**: State
* **Pasos siguientes**: si se ha creado o actualizado aplicación hello, debe incluir el informe de mantenimiento del Administrador de clústeres de Hola. En caso contrario, compruebe el estado de Hola de aplicación hello mediante la emisión de una consulta (por ejemplo, Hola cmdlet de PowerShell **ServiceFabricApplication de Get - ApplicationName *applicationName***).

Hello en el ejemplo siguiente se muestra el evento de estado de hello en hello **fabric: / WordCount** aplicación:

```powershell
PS C:\> Get-ServiceFabricApplicationHealth fabric:/WordCount -ServicesFilter None -DeployedApplicationsFilter None -ExcludeHealthStatistics

ApplicationName                 : fabric:/WordCount
AggregatedHealthState           : Ok
ServiceHealthStates             : None
DeployedApplicationHealthStates : None
HealthEvents                    : 
                                  SourceId              : System.CM
                                  Property              : State
                                  HealthState           : Ok
                                  SequenceNumber        : 282
                                  SentAt                : 7/13/2017 5:57:05 PM
                                  ReceivedAt            : 7/14/2017 4:55:10 PM
                                  TTL                   : Infinite
                                  Description           : Application has been created.
                                  RemoveWhenExpired     : False
                                  IsExpired             : False
                                  Transitions           : Error->Ok = 7/13/2017 5:57:05 PM, LastWarning = 1/1/0001 12:00:00 AM
```

## <a name="service-system-health-reports"></a>Informes de mantenimiento del sistema de servicio
**System.FM**, que representa el servicio de administrador de conmutación por error de hello, es la autoridad de Hola que administra información acerca de los servicios.

### <a name="state"></a>Estado
System.FM notifica como correcta cuando se ha creado el servicio de Hola. Elimina la entidad de Hola de almacén de estado de hello, en cuando se ha eliminado el servicio de Hola.

* **SourceId**: System.FM
* **Property**: State

Hello en el ejemplo siguiente se muestra eventos de estado de hello en el servicio de hello **fabric: / WordCount/WordCountWebService**:

```powershell
PS C:\> Get-ServiceFabricServiceHealth fabric:/WordCount/WordCountWebService -ExcludeHealthStatistics


ServiceName           : fabric:/WordCount/WordCountWebService
AggregatedHealthState : Ok
PartitionHealthStates : 
                        PartitionId           : 8bbcd03a-3a53-47ec-a5f1-9b77f73c53b2
                        AggregatedHealthState : Ok
                        
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 14
                        SentAt                : 7/13/2017 5:57:05 PM
                        ReceivedAt            : 7/14/2017 4:55:10 PM
                        TTL                   : Infinite
                        Description           : Service has been created.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="service-correlation-error"></a>Error de correlación de servicio
**System.PLB** notifica un error cuando detecta que la actualización de un toobe servicio correlacionado con otro servicio crea una cadena de afinidad. informe de Hola se borra cuando se produce una actualización correcta.

* **SourceId**: System.PLB
* **Propiedad**: ServiceDescription
* **Pasos siguientes**: Hola de verificación correlacionado descripciones de servicio.

## <a name="partition-system-health-reports"></a>Informes de mantenimiento del sistema de partición
**System.FM**, que representa el servicio de administrador de conmutación por error de hello, es la autoridad de Hola que administra información acerca de las particiones de servicio.

### <a name="state"></a>Estado
System.FM notifica como correcto cuando partición Hola se ha creado y está en buen estado. Elimina la entidad de Hola de almacén de estado de hello, en cuando se elimina la partición de Hola.

Si la partición de hello es inferior al recuento de réplica mínimo hello, notifica un error. Si la partición hello no es inferior al recuento de réplica mínimo hello, pero es inferior al recuento de réplica de destino de hello, emite una advertencia. Si la partición de hello está en pérdida de quórum, System.FM notifica un error.

Otros eventos importantes incluyen una advertencia cuando una reconfiguración Hola tarda más de lo esperado y cuando la compilación de hello tarda más tiempo del esperado. tiempos de Hello esperado para la compilación de Hola y volver a configurar son configurables basándose en los escenarios de servicio. Por ejemplo, si un servicio tiene un terabyte del estado, como la base de datos de SQL, compilación Hola tarda más de un servicio con una pequeña cantidad de estado.

* **SourceId**: System.FM
* **Property**: State
* **Pasos siguientes**: si el estado de mantenimiento de hello no es correcto, es posible que algunas réplicas no han sido creado, abierto o promocionada tooprimary o base de datos secundaria correctamente. En muchos casos, causa de hello es un error de servicio en hello abierta o la implementación de cambio de rol.

Hola de ejemplo siguiente muestra una partición correcto:

```powershell
PS C:\> Get-ServiceFabricPartition fabric:/WordCount/WordCountWebService | Get-ServiceFabricPartitionHealth -ExcludeHealthStatistics -ReplicasFilter None

PartitionId           : 8bbcd03a-3a53-47ec-a5f1-9b77f73c53b2
AggregatedHealthState : Ok
ReplicaHealthStates   : None
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 70
                        SentAt                : 7/13/2017 5:57:05 PM
                        ReceivedAt            : 7/14/2017 4:55:10 PM
                        TTL                   : Infinite
                        Description           : Partition is healthy.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
```

Hello en el ejemplo siguiente se muestra el estado de saludo de una partición que sea inferior al recuento de la réplica de destino. Hola siguiente paso es descripción de la partición hello tooget, que muestra cómo se configura: **MinReplicaSetSize** es tres y **TargetReplicaSetSize** es siete. A continuación, obtener el número de Hola de nodos de clúster hello: cinco. En este caso, por lo que dos réplicas no se puede colocar como número de destino de Hola de réplicas es mayor que el número de Hola de nodos disponibles.

```powershell
PS C:\> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | Get-ServiceFabricPartitionHealth -ReplicasFilter None -ExcludeHealthStatistics


PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
AggregatedHealthState : Warning
UnhealthyEvaluations  : 
                        Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                        
ReplicaHealthStates   : None
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Warning
                        SequenceNumber        : 123
                        SentAt                : 7/14/2017 4:55:39 PM
                        ReceivedAt            : 7/14/2017 4:55:44 PM
                        TTL                   : Infinite
                        Description           : Partition is below target replica or instance count.
                        fabric:/WordCount/WordCountService 7 2 af2e3e44-a8f8-45ac-9f31-4093eb897600
                          N/S RD _Node_2 Up 131444422260002646
                          N/S RD _Node_4 Up 131444422293113678
                          N/S RD _Node_3 Up 131444422293113679
                          N/S RD _Node_1 Up 131444422293118720
                          N/P RD _Node_0 Up 131444422293118721
                          (Showing 5 out of 5 replicas. Total available replicas: 5.)
                        
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Warning = 7/14/2017 4:55:44 PM, LastOk = 1/1/0001 12:00:00 AM
                        
                        SourceId              : System.PLB
                        Property              : ServiceReplicaUnplacedHealth_Secondary_af2e3e44-a8f8-45ac-9f31-4093eb897600
                        HealthState           : Warning
                        SequenceNumber        : 131445250939703027
                        SentAt                : 7/14/2017 4:58:13 PM
                        ReceivedAt            : 7/14/2017 4:58:14 PM
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
                        FaultDomain:fd:/2 NodeName:_Node_2 NodeType:NodeType2 UpgradeDomain:2 UpgradeDomain: ud:/2 Deactivation Intent/Status: None/None
                        FaultDomain:fd:/1 NodeName:_Node_1 NodeType:NodeType1 UpgradeDomain:1 UpgradeDomain: ud:/1 Deactivation Intent/Status: None/None
                        
                        Existing Primary Replica -- Nodes with Partition's Existing Primary Replica or Secondary Replicas:
                        --
                        FaultDomain:fd:/0 NodeName:_Node_0 NodeType:NodeType0 UpgradeDomain:0 UpgradeDomain: ud:/0 Deactivation Intent/Status: None/None
                        
                        
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : Error->Warning = 7/14/2017 4:56:14 PM, LastOk = 1/1/0001 12:00:00 AM

PS C:\> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | select MinReplicaSetSize,TargetReplicaSetSize

MinReplicaSetSize TargetReplicaSetSize
----------------- --------------------
                2                    7                        

PS C:\> @(Get-ServiceFabricNode).Count
5
```

### <a name="replica-constraint-violation"></a>Infracción de restricción de réplica
**System.PLB** notifica una advertencia si detecta una infracción de restricción de réplica y no se pueden colocar todas las réplicas de la partición. Detalles del informe Hola muestran qué restricciones y propiedades de evitar que la ubicación de réplica de Hola.

* **SourceId**: System.PLB
* **Property**: comienza por **ReplicaConstraintViolation**.

## <a name="replica-system-health-reports"></a>Informes de mantenimiento del sistema de replica
**System.RA**, que representa el componente del agente de reconfiguración de hello, es la autoridad de hello para el estado de réplica de Hola.

### <a name="state"></a>Estado
**System.RA** notifica Aceptar si se ha creado la réplica de Hola.

* **SourceId**: System.RA
* **Property**: State

Hola de ejemplo siguiente muestra una réplica correcto:

```powershell
PS C:\> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | Get-ServiceFabricReplica | where {$_.ReplicaRole -eq "Primary"} | Get-ServiceFabricReplicaHealth

PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
ReplicaId             : 131444422293118721
AggregatedHealthState : Ok
HealthEvents          : 
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 131445248920273536
                        SentAt                : 7/14/2017 4:54:52 PM
                        ReceivedAt            : 7/14/2017 4:55:13 PM
                        TTL                   : Infinite
                        Description           : Replica has been created._Node_0
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/14/2017 4:55:13 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="replica-open-status"></a>Estado de apertura de réplica
Descripción de Hola de este informe de estado contiene la hora de inicio de hello (hora Universal) cuando se ha invocado Hola API llamada.

**System.RA** emite una advertencia si réplica Hola abierto tarda más de período de hello configurado (valor predeterminado: 30 minutos). Si Hola API afecta la disponibilidad de servicio, informe de Hola se emite mucho más rápido (un intervalo configurable, su valor predeterminado es 30 segundos). tiempo de Hello medido incluye tiempo Hola de Replicador de hello abierto y el servicio de hello abierto. Hola propiedad cambios tooOK si abre Hola completa.

* **SourceId**: System.RA
* **Property**: **ReplicaOpenStatus**
* **Pasos siguientes**: si el estado de mantenimiento de hello no es correcto, investigue por qué réplica Hola abierto tarda más de lo esperado.

### <a name="slow-service-api-call"></a>Llamada a la API de servicio lenta
**System.RAP** y **System.Replicator** notificar una advertencia si un código de servicio de llamada toohello usuario tarda más tiempo de hello configurado. Advertencia de Hola se borra cuando se complete la llamada de Hola.

* **SourceId**: System.RAP o System.Replicator
* **Propiedad**: nombre Hola de hello lenta API. Descripción de Hello proporciona más detalles sobre Hola Hola de tiempo API ha estado pendiente.
* **Pasos siguientes**: investigar por qué llamada Hola tarda más tiempo del esperado.

Hola de ejemplo siguiente muestra una partición de pérdida de quórum y Hola investigación pasos realiza toofigure el motivo. Una de las réplicas de hello tiene un estado de advertencia, por lo que obtiene su estado. Muestra que la operación de servicio de hello tarda más tiempo del esperado, un evento notificado por System.RAP. Una vez recibida esta información, Hola siguiente paso es toolook en el código del servicio de Hola e investigar no existe. En este caso, Hola **Coredispatcher** implementación de servicio con estado Hola produce una excepción no controlada. réplicas de Hola se reciclaje, por lo que quizás no pueda ver cualquier réplica en estado de advertencia de Hola. Puede vuelva a intentar obtener estado de mantenimiento de Hola y buscar las diferencias de hello Id. de réplica. En algunos casos, los reintentos de hello pueden proporcionar pistas.

```powershell
PS C:\> Get-ServiceFabricPartition fabric:/HelloWorldStatefulApplication/HelloWorldStateful | Get-ServiceFabricPartitionHealth -ExcludeHealthStatistics

PartitionId           : 72a0fb3e-53ec-44f2-9983-2f272aca3e38
AggregatedHealthState : Error
UnhealthyEvaluations  :
                        Error event: SourceId='System.FM', Property='State'.

ReplicaHealthStates   :
                        ReplicaId             : 130743748372546446
                        AggregatedHealthState : Ok

                        ReplicaId             : 130743746168084332
                        AggregatedHealthState : Ok

                        ReplicaId             : 130743746195428808
                        AggregatedHealthState : Warning

                        ReplicaId             : 130743746195428807
                        AggregatedHealthState : Ok

HealthEvents          :
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Error
                        SequenceNumber        : 182
                        SentAt                : 4/24/2015 7:00:17 PM
                        ReceivedAt            : 4/24/2015 7:00:31 PM
                        TTL                   : Infinite
                        Description           : Partition is in quorum loss.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Warning->Error = 4/24/2015 6:51:31 PM

PS C:\> Get-ServiceFabricPartition fabric:/HelloWorldStatefulApplication/HelloWorldStateful

PartitionId            : 72a0fb3e-53ec-44f2-9983-2f272aca3e38
PartitionKind          : Int64Range
PartitionLowKey        : -9223372036854775808
PartitionHighKey       : 9223372036854775807
PartitionStatus        : InQuorumLoss
LastQuorumLossDuration : 00:00:13
MinReplicaSetSize      : 3
TargetReplicaSetSize   : 3
HealthState            : Error
DataLossNumber         : 130743746152927699
ConfigurationNumber    : 227633266688

PS C:\> Get-ServiceFabricReplica 72a0fb3e-53ec-44f2-9983-2f272aca3e38 130743746195428808

ReplicaId           : 130743746195428808
ReplicaAddress      : PartitionId: 72a0fb3e-53ec-44f2-9983-2f272aca3e38, ReplicaId: 130743746195428808
ReplicaRole         : Primary
NodeName            : Node.3
ReplicaStatus       : Ready
LastInBuildDuration : 00:00:01
HealthState         : Warning

PS C:\> Get-ServiceFabricReplicaHealth 72a0fb3e-53ec-44f2-9983-2f272aca3e38 130743746195428808

PartitionId           : 72a0fb3e-53ec-44f2-9983-2f272aca3e38
ReplicaId             : 130743746195428808
AggregatedHealthState : Warning
UnhealthyEvaluations  :
                        Unhealthy event: SourceId='System.RAP', Property='ServiceOpenOperationDuration', HealthState='Warning', ConsiderWarningAsError=false.

HealthEvents          :
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 130743756170185892
                        SentAt                : 4/24/2015 7:00:17 PM
                        ReceivedAt            : 4/24/2015 7:00:33 PM
                        TTL                   : Infinite
                        Description           : Replica has been created.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : ->Ok = 4/24/2015 7:00:33 PM

                        SourceId              : System.RAP
                        Property              : ServiceOpenOperationDuration
                        HealthState           : Warning
                        SequenceNumber        : 130743756399407044
                        SentAt                : 4/24/2015 7:00:39 PM
                        ReceivedAt            : 4/24/2015 7:00:59 PM
                        TTL                   : Infinite
                        Description           : Start Time (UTC): 2015-04-24 19:00:17.019
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : ->Warning = 4/24/2015 7:00:59 PM
```

Cuando se inicia la aplicación defectuoso hello en el depurador de hello, ventanas de eventos de diagnóstico de hello muestran excepción Hola de Coredispatcher:

![Eventos de diagnóstico de Visual Studio 2015: Error de RunAsync en fabric:/HelloWorldStatefulApplication.][1]

Eventos de diagnóstico de Visual Studio 2015: Error de RunAsync en **fabric:/HelloWorldStatefulApplication**.

[1]: ./media/service-fabric-understand-and-troubleshoot-with-system-health-reports/servicefabric-health-vs-runasync-exception.png


### <a name="replication-queue-full"></a>Cola de replicación completa
**System.Replicator** emite una advertencia cuando la cola de replicación de hello está llena. En hello principal, cola de replicación normalmente llenarse porque una o varias réplicas secundarias son operaciones de tooacknowledge lenta. En hello secundaria, esto suele ocurrir cuando el servicio de hello tooapply lenta Hola operaciones. Advertencia de Hola se borra cuando Hola cola ya no está llena.

* **SourceId**: System.Replicator
* **Propiedad**: **PrimaryReplicationQueueStatus** o **SecondaryReplicationQueueStatus**, según el rol de réplica Hola

### <a name="slow-naming-operations"></a>Operaciones de nomenclatura lentas
**System.NamingService** informa del estado en su réplica principal cuando una operación de nomenclatura tarda más de lo aceptable. [CreateServiceAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) o [DeleteServiceAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.deleteserviceasync) son ejemplos de operaciones de nomenclatura. En FabricClient pueden encontrarse más métodos, como en [métodos de administración de servicios](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient) o [métodos de administración de propiedades](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.propertymanagementclient).

> [!NOTE]
> Hola Naming service resuelve ubicación tooa nombres del servicio de clúster de Hola y permite propiedades y los nombres de servicio de toomanage de los usuarios. Se trata de un servicio guardado con particiones de Service Fabric. Una de las particiones de hello representa Hola Authority Owner, que contiene metadatos sobre todos los servicios y nombres de Service Fabric. nombres de Service Fabric Hola son particiones de toodifferent asignadas, denominadas particiones Name Owner, por lo que el servicio de hello es extensible. Obtenga más información sobre el [servicio de nomenclatura](service-fabric-architecture.md).
> 
> 

Cuando una operación de escribir el nombre tiene más de lo esperado, operación Hola se marca con un informe de advertencia en hello *réplica principal de hello denominación de partición de servicio, que sirve de operación de hello*. Si finaliza correctamente la operación de hello, hello advertencia está desactivada. Si la operación de hello completa con un error, informe de mantenimiento de Hola incluye detalles sobre el error de Hola.

* **SourceId**: System.NamingService
* **Propiedad**: comienza con prefijo **Duration_** e identifica el funcionamiento lento de Hola y el nombre de Service Fabric hello en qué Hola se aplica la operación. Por ejemplo, si crear servicio en el tejido de nombre: / MyApp/MyService tarda demasiado, propiedad de hello es Duration_AOCreateService.fabric:/MyApp/MyService. Rol de toohello AO puntos del programa Hola a escribir el nombre de partición para este nombre y la operación.
* **Pasos siguientes**: ¿por qué se produce un error en la operación de nomenclatura de Hola de comprobación. Cada operación puede tener diferentes causas. Por ejemplo, eliminar servicio puede haberse atascado en un nodo porque el host de la aplicación hello sigue fallando en un nodo debido a errores de usuario de tooa en el código de servicio de Hola.

Hola de ejemplo siguiente muestra una operación de servicio de creación. operación de Hello ha tardado más tiempo más tiempo en ejecutarse Hola configurado. AO reintenta y envía tooNO de trabajo. NINGUNA operación de la última Hola completada con tiempo de espera. En este caso, hello misma réplica es el principal de hello AO y ningún rol.

```powershell
PartitionId           : 00000000-0000-0000-0000-000000001000
ReplicaId             : 131064359253133577
AggregatedHealthState : Warning
UnhealthyEvaluations  :
                        Unhealthy event: SourceId='System.NamingService', Property='Duration_AOCreateService.fabric:/MyApp/MyService', HealthState='Warning', ConsiderWarningAsError=false.

HealthEvents          :
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 131064359308715535
                        SentAt                : 4/29/2016 8:38:50 PM
                        ReceivedAt            : 4/29/2016 8:39:08 PM
                        TTL                   : Infinite
                        Description           : Replica has been created.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 4/29/2016 8:39:08 PM, LastWarning = 1/1/0001 12:00:00 AM

                        SourceId              : System.NamingService
                        Property              : Duration_AOCreateService.fabric:/MyApp/MyService
                        HealthState           : Warning
                        SequenceNumber        : 131064359526778775
                        SentAt                : 4/29/2016 8:39:12 PM
                        ReceivedAt            : 4/29/2016 8:39:38 PM
                        TTL                   : 00:05:00
                        Description           : hello AOCreateService started at 2016-04-29 20:39:08.677 is taking longer than 30.000.
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : Error->Warning = 4/29/2016 8:39:38 PM, LastOk = 1/1/0001 12:00:00 AM

                        SourceId              : System.NamingService
                        Property              : Duration_NOCreateService.fabric:/MyApp/MyService
                        HealthState           : Warning
                        SequenceNumber        : 131064360657607311
                        SentAt                : 4/29/2016 8:41:05 PM
                        ReceivedAt            : 4/29/2016 8:41:08 PM
                        TTL                   : 00:00:15
                        Description           : hello NOCreateService started at 2016-04-29 20:39:08.689 completed with FABRIC_E_TIMEOUT in more than 30.000.
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : Error->Warning = 4/29/2016 8:39:38 PM, LastOk = 1/1/0001 12:00:00 AM
```

## <a name="deployedapplication-system-health-reports"></a>Informes de mantenimiento del sistema DeployedApplication
**System.Hosting** es autoridad hello en entidades implementadas.

### <a name="activation"></a>Activación
System.Hosting notifica como correcta cuando una aplicación se ha activado correctamente en el nodo de Hola. De lo contrario, notifica un error.

* **SourceId**: System.Hosting
* **Propiedad**: activación, incluida la versión de lanzamiento de Hola
* **Pasos siguientes**: si la aplicación hello está en mal estado, investigue el motivo del error de activación de Hola.

Hello en el ejemplo siguiente se muestra una activación correcta:

```powershell
PS C:\> Get-ServiceFabricDeployedApplicationHealth -NodeName _Node_1 -ApplicationName fabric:/WordCount -ExcludeHealthStatistics

ApplicationName                    : fabric:/WordCount
NodeName                           : _Node_1
AggregatedHealthState              : Ok
DeployedServicePackageHealthStates : 
                                     ServiceManifestName   : WordCountServicePkg
                                     ServicePackageActivationId : 
                                     NodeName              : _Node_1
                                     AggregatedHealthState : Ok
                                     
HealthEvents                       : 
                                     SourceId              : System.Hosting
                                     Property              : Activation
                                     HealthState           : Ok
                                     SequenceNumber        : 131445249083836329
                                     SentAt                : 7/14/2017 4:55:08 PM
                                     ReceivedAt            : 7/14/2017 4:55:14 PM
                                     TTL                   : Infinite
                                     Description           : hello application was activated successfully.
                                     RemoveWhenExpired     : False
                                     IsExpired             : False
                                     Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="download"></a>Descargar
**System.Hosting** notifica un error si se produce un error en la descarga del paquete de aplicación Hola.

* **SourceId**: System.Hosting
* **Property**: **Download:*RolloutVersion***
* **Pasos siguientes**: investigar el motivo del error de descarga de hello en el nodo de Hola.

## <a name="deployedservicepackage-system-health-reports"></a>Informes de mantenimiento del sistema DeployedServicePackage
**System.Hosting** es autoridad hello en entidades implementadas.

### <a name="service-package-activation"></a>Activación de paquete de servicio
System.Hosting notifica como Aceptar si la activación del paquete de servicio de hello en el nodo de hello es correcta. De lo contrario, notifica un error.

* **SourceId**: System.Hosting
* **Property**: Activation.
* **Pasos siguientes**: investigar el motivo del error de activación de Hola.

### <a name="code-package-activation"></a>Activación del paquete de código
**System.Hosting** notifica como Aceptar para cada paquete de código si la activación de hello es correcta. Si se produce un error en activación de hello, emite una advertencia conforme a la configuración. Si **CodePackage** se produce un error tooactivate o se cierra con un error mayor Hola configurado **CodePackageHealthErrorThreshold**, hospedaje notifica un error. Si hay varios paquetes de código en un paquete de servicios, se genera un informe de activación para cada uno.

* **SourceId**: System.Hosting
* **Propiedad**: prefijo de hello usa **CodePackageActivation** y contiene el nombre de Hola de paquete de código de hello y punto de entrada de hello como  **CodePackageActivation:* CodePackageName*:*SetupEntryPoint/EntryPoint*** (por ejemplo, **CodePackageActivation:Code:SetupEntryPoint**)

### <a name="service-type-registration"></a>Registro del tipo de servicio
**System.Hosting** notifica como correcto si el tipo de servicio de Hola se ha registrado correctamente. Notifica un error si no se realizó el registro de hello en el tiempo (según la configuración utilizando **ServiceTypeRegistrationTimeout**). Si se cierra en tiempo de ejecución de hello, tipo de servicio de Hola se anula el registro del nodo de Hola y hospedaje emite una advertencia.

* **SourceId**: System.Hosting
* **Propiedad**: prefijo de hello usa **ServiceTypeRegistration** y contiene el nombre de tipo de servicio de hello (por ejemplo, **ServiceTypeRegistration:FileStoreServiceType**)

Hola de ejemplo siguiente muestra un paquete de servicio implementado correcto:

```powershell
PS C:\> Get-ServiceFabricDeployedServicePackageHealth -NodeName _Node_1 -ApplicationName fabric:/WordCount -ServiceManifestName WordCountServicePkg


ApplicationName            : fabric:/WordCount
ServiceManifestName        : WordCountServicePkg
ServicePackageActivationId : 
NodeName                   : _Node_1
AggregatedHealthState      : Ok
HealthEvents               : 
                             SourceId              : System.Hosting
                             Property              : Activation
                             HealthState           : Ok
                             SequenceNumber        : 131445249084026346
                             SentAt                : 7/14/2017 4:55:08 PM
                             ReceivedAt            : 7/14/2017 4:55:14 PM
                             TTL                   : Infinite
                             Description           : hello ServicePackage was activated successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
                             
                             SourceId              : System.Hosting
                             Property              : CodePackageActivation:Code:EntryPoint
                             HealthState           : Ok
                             SequenceNumber        : 131445249084306362
                             SentAt                : 7/14/2017 4:55:08 PM
                             ReceivedAt            : 7/14/2017 4:55:14 PM
                             TTL                   : Infinite
                             Description           : hello CodePackage was activated successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
                             
                             SourceId              : System.Hosting
                             Property              : ServiceTypeRegistration:WordCountServiceType
                             HealthState           : Ok
                             SequenceNumber        : 131445249088096842
                             SentAt                : 7/14/2017 4:55:08 PM
                             ReceivedAt            : 7/14/2017 4:55:14 PM
                             TTL                   : Infinite
                             Description           : hello ServiceType was registered successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="download"></a>Descargar
**System.Hosting** notifica un error si se produce un error en la descarga del paquete del servicio Hola.

* **SourceId**: System.Hosting
* **Property**: **Download:*RolloutVersion***
* **Pasos siguientes**: investigar el motivo del error de descarga de hello en el nodo de Hola.

### <a name="upgrade-validation"></a>Validación de actualización
**System.Hosting** notifica un error si se produce un error de validación durante la actualización de Hola o si hello actualización produce un error en el nodo de Hola.

* **SourceId**: System.Hosting
* **Propiedad**: prefijo de hello usa **FabricUpgradeValidation** y contiene la versión de actualización de Hola
* **Descripción**: puntos de error de toohello

## <a name="next-steps"></a>Pasos siguientes
[Vista de los informes de estado de Service Fabric](service-fabric-view-entities-aggregated-health.md)

[¿Cómo tooreport y comprobación de estado de servicio](service-fabric-diagnostics-how-to-report-and-check-service-health.md)

[Supervisión y diagnóstico de los servicios localmente](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[Actualización de la aplicación de Service Fabric](service-fabric-application-upgrade.md)

