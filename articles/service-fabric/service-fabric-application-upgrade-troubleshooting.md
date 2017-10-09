---
title: las actualizaciones de aplicaciones aaaTroubleshooting | Documentos de Microsoft
description: "En este artículo se trata algunos problemas comunes alrededor de actualizar una aplicación de Service Fabric y cómo tooresolve ellos."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: 19ad152e-ec50-4327-9f19-065c875c003c
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 0f56fa61db9b4e32824623f162dc1bfe7fda0f49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-application-upgrades"></a>Solucionar problemas de actualizaciones de aplicaciones
Este artículo tratan algunos problemas comunes de hello alrededor de actualizar una aplicación de Azure Service Fabric y cómo tooresolve ellos.

## <a name="troubleshoot-a-failed-application-upgrade"></a>Solucionar problemas de una actualización de aplicación con error
Cuando falla una actualización, la salida de hello de hello **Get ServiceFabricApplicationUpgrade** comando contiene información adicional para la depuración de errores de Hola.  Hello lista siguiente especifica cómo se puede utilizar la información adicional de hello:

1. Identificar el tipo de error de Hola.
2. Identificar el motivo del error de Hola.
3. Aísle uno o más componentes de error para investigarlos en profundidad.

Esta información está disponible cuando el tejido de servicio detecta el error de hello independientemente de si hello **FailureAction** tooroll vuelve o suspender actualización Hola.

### <a name="identify-hello-failure-type"></a>Identificar el tipo de error de Hola
En la salida de hello de **Get ServiceFabricApplicationUpgrade**, **FailureTimestampUtc** identifica Hola marca de tiempo (en UTC) a la que se detectó un error de actualización por Service Fabric y  **FailureAction** se activó. **FailureReason** identifica a uno de tres posibles causas del error de Hola de alto nivel:

1. UpgradeDomainTimeout - indica que un dominio de actualización concreto tardó demasiado toocomplete y **UpgradeDomainTimeout** expirado.
2. OverallUpgradeTimeout - indica que Hola global de actualización tardó demasiado toocomplete y **UpgradeTimeout** expirado.
3. La comprobación de estado - indica que, después de actualizar un dominio de actualización, aplicación hello permanecido incorrecto según toohello especifica las directivas de mantenimiento y **HealthCheckRetryTimeout** expirado.

Estas entradas sólo se muestran en la salida de hello al actualización Hola se produce un error e inicia la reversión. Según el tipo de saludo de error de Hola se muestra información adicional.

### <a name="investigate-upgrade-timeouts"></a>Investigar los tiempos de espera de actualización
Los errores de tiempo de espera de actualización se producen habitualmente por problemas de disponibilidad del servicio. salida de Hello siguiendo este párrafo es típico de las actualizaciones en los que las réplicas de servicio o instancias no toostart en la nueva versión de código de hello. Hola **UpgradeDomainProgressAtFailure** campo captura una instantánea de cualquier trabajo de actualización pendiente en tiempo de Hola de error.

```
PS D:\temp> Get-ServiceFabricApplicationUpgrade fabric:/DemoApp

ApplicationName                : fabric:/DemoApp
ApplicationTypeName            : DemoAppType
TargetApplicationTypeVersion   : v2
ApplicationParameters          : {}
StartTimestampUtc              : 4/14/2015 9:26:38 PM
FailureTimestampUtc            : 4/14/2015 9:27:05 PM
FailureReason                  : UpgradeDomainTimeout
UpgradeDomainProgressAtFailure : MYUD1

                                 NodeName            : Node4
                                 UpgradePhase        : PostUpgradeSafetyCheck
                                 PendingSafetyChecks :
                                     WaitForPrimaryPlacement - PartitionId: 744c8d9f-1d26-417e-a60e-cd48f5c098f0

                                 NodeName            : Node1
                                 UpgradePhase        : PostUpgradeSafetyCheck
                                 PendingSafetyChecks :
                                     WaitForPrimaryPlacement - PartitionId: 4b43f4d8-b26b-424e-9307-7a7a62e79750
UpgradeState                   : RollingBackCompleted
UpgradeDuration                : 00:00:46
CurrentUpgradeDomainDuration   : 00:00:00
NextUpgradeDomain              :
UpgradeDomainsStatus           : { "MYUD1" = "Completed";
                                 "MYUD2" = "Completed";
                                 "MYUD3" = "Completed" }
UpgradeKind                    : Rolling
RollingUpgradeMode             : UnmonitoredAuto
ForceRestart                   : False
UpgradeReplicaSetCheckTimeout  : 00:00:00
```

En este ejemplo, no se pudo actualizar hello en el dominio de actualización *MYUD1* y dos particiones (*744c8d9f-1d26-417e-a60e-cd48f5c098f0* y *4b43f4d8-b26b-424e-9307-7a7a62e79750*) se bloquea. particiones Hola se queda bloqueadas porque en tiempo de ejecución de hello era réplicas principales no se puede tooplace (*WaitForPrimaryPlacement*) en nodos de destino *Nodo1* y *Nodo4*.

Hola **Get ServiceFabricNode** comando puede ser usado tooverify que estos dos nodos están en el dominio de actualización *MYUD1*. Hola *UpgradePhase* dice *PostUpgradeSafetyCheck*, lo que significa que estas comprobaciones de seguridad se producen después de que todos los nodos de dominio de actualización de hello han finalizado la actualización. Toda esta información apunta tooa posible problema con la nueva versión de Hola Hola del código de aplicación. los problemas más comunes de Hello son errores del servicio en Hola abierto o las rutas de código de promoción tooprimary.

Un *UpgradePhase* de *PreUpgradeSafetyCheck* significa hubo problemas de preparación de dominio de actualización de hello antes de que se haya ejecutado. en este caso, los problemas más comunes de Hello son errores del servicio de cierre Hola o degradación de las rutas de código principal.

Hola actual **UpgradeState** es *RollingBackCompleted*, por lo que la actualización original Hola debe haberse realizada con una reversión **FailureAction**, que automáticamente revierte la actualización de hello en caso de error. Si se realizó la actualización original Hola con un manual **FailureAction**, entonces en su lugar se actualización hello en un activo de depuración de la aplicación hello tooallow de estado suspendido.

### <a name="investigate-health-check-failures"></a>Investigar errores de comprobación de estado
Los errores de comprobación de estado pueden desencadenarse debido a varios problemas que se pueden producir después de que todos los nodos de un dominio de actualización terminen de actualizarse y pasen todas las comprobaciones de seguridad. salida de Hello siguiendo este párrafo es típico de un error de actualización debido a comprobaciones de mantenimiento de toofailed. Hola **UnhealthyEvaluations** campo captura una instantánea de comprobaciones de estado que no se pudo en tiempo de Hola de actualización de hello según toohello especificado [directiva de mantenimiento](service-fabric-health-introduction.md).

```
PS D:\temp> Get-ServiceFabricApplicationUpgrade fabric:/DemoApp

ApplicationName                         : fabric:/DemoApp
ApplicationTypeName                     : DemoAppType
TargetApplicationTypeVersion            : v4
ApplicationParameters                   : {}
StartTimestampUtc                       : 4/24/2015 2:42:31 AM
UpgradeState                            : RollingForwardPending
UpgradeDuration                         : 00:00:27
CurrentUpgradeDomainDuration            : 00:00:27
NextUpgradeDomain                       : MYUD2
UpgradeDomainsStatus                    : { "MYUD1" = "Completed";
                                          "MYUD2" = "Pending";
                                          "MYUD3" = "Pending" }
UnhealthyEvaluations                    :
                                          Unhealthy services: 50% (2/4), ServiceType='PersistedServiceType', MaxPercentUnhealthyServices=0%.

                                          Unhealthy service: ServiceName='fabric:/DemoApp/Svc3', AggregatedHealthState='Error'.

                                              Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.

                                              Unhealthy partition: PartitionId='3a9911f6-a2e5-452d-89a8-09271e7e49a8', AggregatedHealthState='Error'.

                                                  Error event: SourceId='Replica', Property='InjectedFault'.

                                          Unhealthy service: ServiceName='fabric:/DemoApp/Svc2', AggregatedHealthState='Error'.

                                              Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.

                                              Unhealthy partition: PartitionId='744c8d9f-1d26-417e-a60e-cd48f5c098f0', AggregatedHealthState='Error'.

                                                  Error event: SourceId='Replica', Property='InjectedFault'.

UpgradeKind                             : Rolling
RollingUpgradeMode                      : Monitored
FailureAction                           : Manual
ForceRestart                            : False
UpgradeReplicaSetCheckTimeout           : 49710.06:28:15
HealthCheckWaitDuration                 : 00:00:00
HealthCheckStableDuration               : 00:00:10
HealthCheckRetryTimeout                 : 00:00:10
UpgradeDomainTimeout                    : 10675199.02:48:05.4775807
UpgradeTimeout                          : 10675199.02:48:05.4775807
ConsiderWarningAsError                  :
MaxPercentUnhealthyPartitionsPerService :
MaxPercentUnhealthyReplicasPerPartition :
MaxPercentUnhealthyServices             :
MaxPercentUnhealthyDeployedApplications :
ServiceTypeHealthPolicyMap              :
```

Investigar errores de comprobación de mantenimiento, en primer lugar requiere una descripción del modelo de estado de Service Fabric Hola. Pero incluso sin una comprensión detallada, podemos ver que los dos servicios tienen un estado incorrecto: *fabric: / DemoApp/Svc3* y *fabric: / DemoApp/Svc2*, junto con los informes de estado de error de hello ("InjectedFault "en este caso). En este ejemplo, dos de los cuatro servicios tienen un estado incorrecto, que está por debajo del umbral de hello predeterminado del 0% incorrecto (*MaxPercentUnhealthyServices*).

Hello actualización suspendió tras error especificando un **FailureAction** de cuando manual a partir de Hola actualización. Este modo nos permite sistemas en vivo de hello tooinvestigate en estado de error de hello antes de realizar ninguna acción adicional.

### <a name="recover-from-a-suspended-upgrade"></a>Recuperarse de una actualización suspendida
Con una reversión **FailureAction**, no hay ninguna recuperación es necesario ya que la actualización de Hola se revierte automáticamente al error. Con una **FailureAction**manual, hay varias opciones de recuperación:

1.  Desencadenar una reversión
2. Continuar a través del resto de Hola de actualización de hello manualmente
3. Hola reanudar supervisa la actualización

Hola **ServiceFabricApplicationRollback inicio** comando se puede usar en cualquier toostart tiempo Revertir aplicación hello. Una vez que se devuelve correctamente el comando hello, una solicitud rollback Hola se ha registrado en el sistema de hello e inicia poco después.

Hola **ServiceFabricApplicationUpgrade reanudar** comando se puede usar tooproceed a través del resto de Hola de hello manualmente, actualizar un dominio de actualización a la vez. En este modo, se realizan comprobaciones de seguridad solo sistema Hola. No se realizan más comprobaciones de estado. Este comando solo puede usarse cuando hello *UpgradeState* muestra *RollingForwardPending*, lo que significa que ese dominio de actualización actual de hello ha finalizado la actualización pero hello junto uno no ha comenzado (pendiente).

Hola **ServiceFabricApplicationUpgrade actualización** comando se puede tooresume usado Hola supervisado actualización con las comprobaciones de seguridad y mantenimiento que se va a realizar.

```
PS D:\temp> Update-ServiceFabricApplicationUpgrade fabric:/DemoApp -UpgradeMode Monitored

UpgradeMode                             : Monitored
ForceRestart                            :
UpgradeReplicaSetCheckTimeout           :
FailureAction                           :
HealthCheckWaitDuration                 :
HealthCheckStableDuration               :
HealthCheckRetryTimeout                 :
UpgradeTimeout                          :
UpgradeDomainTimeout                    :
ConsiderWarningAsError                  :
MaxPercentUnhealthyPartitionsPerService :
MaxPercentUnhealthyReplicasPerPartition :
MaxPercentUnhealthyServices             :
MaxPercentUnhealthyDeployedApplications :
ServiceTypeHealthPolicyMap              :

PS D:\temp>
```

actualización de Hello continúa a partir de hello de uso mismo actualizar parámetros y las directivas de mantenimiento como antes y de dominio de actualización de Hola donde se suspendió la última. Si es necesario, cualquiera de los parámetros de actualización de Hola y las directivas de mantenimiento que se muestra en hello anterior salida puede cambiarse en hello mismo comando cuando se reanuda la actualización de Hola. En este ejemplo, se reanudó actualización hello en modo supervisado, con parámetros de Hola y las directivas de mantenimiento de hello sin cambios.

## <a name="further-troubleshooting"></a>Más información de solución de problemas
### <a name="service-fabric-is-not-following-hello-specified-health-policies"></a>Service Fabric no es posterior a Hola especificada las directivas de mantenimiento
Causa posible 1:

Service Fabric convierte todos los porcentajes en números reales de entidades (por ejemplo, las réplicas, particiones y servicios) para la evaluación de mantenimiento y siempre se redondea hacia arriba toowhole entidades. Por ejemplo, si hello máximo *MaxPercentUnhealthyReplicasPerPartition* es % 21 y hay cinco réplicas, Service Fabric permite que un tootwo réplicas en mal estado (es decir,`Math.Ceiling (5*0.21)`). Por lo tanto, las directivas de mantenimiento deben establecerse como corresponda.

Causa posible 2:

Las directivas de mantenimiento se especifican en términos de porcentajes de servicios totales e instancias de servicio no específicas. Por ejemplo, antes de una actualización, si una aplicación tiene al menos cuatro instancias A, B, C y D, de servicio donde servicio D es incorrecto, pero con aplicaciones de toohello de poco impacto. Queremos hello tooignore conoce servicio D en mal estado durante el parámetro hello de actualización y defina *MaxPercentUnhealthyServices* toobe 25%, suponiendo que sólo A, B y C necesita toobe correcto.

Sin embargo, durante la actualización de hello, d. quede correcto mientras C pasa a ser incorrecto. actualización de Hello seguirían ejecutando correctamente porque solo el 25% de los servicios de hello tienen un estado incorrecto. Sin embargo, podría dar como resultado errores no anticipados debido a que se va a tooC incorrecto inesperadamente en lugar de D. En esta situación, se debe modelar d. como un tipo de servicio diferente de A, B y C. Puesto que las directivas de mantenimiento se especifican por tipo de servicio, umbrales de otro porcentaje incorrecto pueden ser servicios toodifferent aplicada. 

### <a name="i-did-not-specify-a-health-policy-for-application-upgrade-but-hello-upgrade-still-fails-for-some-time-outs-that-i-never-specified"></a>No especificó una directiva de mantenimiento para la actualización de la aplicación, pero sigue sin funcionar actualización Hola para algunos tiempos de espera que no se especificó nunca
Cuando las directivas de mantenimiento no se proporciona la solicitud de actualización de toohello, se toman del hello *ApplicationManifest.xml* de la versión actual de la aplicación de Hola. Por ejemplo, si está actualizando X de la aplicación desde la versión 1.0 tooversion 2.0, se usan las directivas de mantenimiento de aplicación especificadas para en la versión 1.0. Si se debe utilizar una directiva de mantenimiento diferente para la actualización de hello, directiva de hello debe toobe especificado como parte de la llamada de API de actualización de hello aplicación. Hello directivas especificadas como parte de la llamada de hello API solo se aplican durante la actualización de Hola. Una vez completada la actualización de hello, directivas de hello especificaron en hello *ApplicationManifest.xml* se usan.

### <a name="incorrect-time-outs-are-specified"></a>Se especifican los tiempos de expiración incorrectos
Es posible que se pregunte por lo que sucede cuando los tiempos de espera se establecen de forma incoherente. Por ejemplo, puede tener un *UpgradeTimeout* que es menor que hello *UpgradeDomainTimeout*. respuesta de Hello es que se devuelva un error. Los errores se devuelven si hello *UpgradeDomainTimeout* es menor que la suma de Hola de *HealthCheckWaitDuration* y *HealthCheckRetryTimeout*, o si  *UpgradeDomainTimeout* es menor que la suma de Hola de *HealthCheckWaitDuration* y *HealthCheckStableDuration*.

### <a name="my-upgrades-are-taking-too-long"></a>Mis actualizaciones están tardando mucho tiempo
tiempo de Hola para una actualización toocomplete depende de las comprobaciones de mantenimiento de Hola y los tiempos de espera especificados. Comprobaciones de estado y los tiempos de espera dependen sobre cuánto tiempo tarda toocopy, implementación y estabilizan la aplicación hello. Ser demasiado agresivo con los tiempos de expiración puede dar lugar a que se realicen más actualizaciones con errores; por ello, recomendamos empezar de manera conservadora con tiempos de expiración más prolongados.

Este es un rápido repaso sobre cómo interactúan los tiempos de espera de hello con tiempos de actualización de hello:

Las actualizaciones de un dominio de actualización no se pueden completar con mayor rapidez que *HealthCheckWaitDuration* + *HealthCheckStableDuration*.

No se puede producir un error de actualización con mayor rapidez que *HealthCheckWaitDuration* + *HealthCheckRetryTimeout*.

Hello tiempo de actualización de un dominio de actualización limita *UpgradeDomainTimeout*.  Si *HealthCheckRetryTimeout* y *HealthCheckStableDuration* son distintos de cero y el estado de saludo de la aplicación hello mantiene cambio y hacia atrás, a continuación, la actualización de hello agota el tiempo de en  *UpgradeDomainTimeout*. *UpgradeDomainTimeout* empieza a contar hacia abajo una vez Hola actualización de dominio de actualización actual Hola comienza.

## <a name="next-steps"></a>Pasos siguientes
[actualización de aplicaciones usando Visual Studio](service-fabric-application-upgrade-tutorial.md) ofrece información para actualizar una aplicación mediante Visual Studio.

[actualización de aplicaciones mediante PowerShell](service-fabric-application-upgrade-tutorial-powershell.md) se explica en detalle lo que tiene que hacer para actualizar una aplicación mediante PowerShell.

Puede controlar cómo se actualiza una aplicación usando [parámetros de actualización](service-fabric-application-upgrade-parameters.md).

Hacer que las actualizaciones de la aplicación sea compatible por el aprendizaje cómo toouse [serialización de datos](service-fabric-application-upgrade-data-serialization.md).

Obtenga información acerca de cómo toouse funcionalidad avanzada al actualizar la aplicación, se hace referencia demasiado[temas avanzados](service-fabric-application-upgrade-advanced.md).
