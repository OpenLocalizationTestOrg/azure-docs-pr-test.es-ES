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
# <a name="troubleshoot-application-upgrades"></a><span data-ttu-id="964ee-103">Solucionar problemas de actualizaciones de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="964ee-103">Troubleshoot application upgrades</span></span>
<span data-ttu-id="964ee-104">Este artículo tratan algunos problemas comunes de hello alrededor de actualizar una aplicación de Azure Service Fabric y cómo tooresolve ellos.</span><span class="sxs-lookup"><span data-stu-id="964ee-104">This article covers some of hello common issues around upgrading an Azure Service Fabric application and how tooresolve them.</span></span>

## <a name="troubleshoot-a-failed-application-upgrade"></a><span data-ttu-id="964ee-105">Solucionar problemas de una actualización de aplicación con error</span><span class="sxs-lookup"><span data-stu-id="964ee-105">Troubleshoot a failed application upgrade</span></span>
<span data-ttu-id="964ee-106">Cuando falla una actualización, la salida de hello de hello **Get ServiceFabricApplicationUpgrade** comando contiene información adicional para la depuración de errores de Hola.</span><span class="sxs-lookup"><span data-stu-id="964ee-106">When an upgrade fails, hello output of hello **Get-ServiceFabricApplicationUpgrade** command contains additional information for debugging hello failure.</span></span>  <span data-ttu-id="964ee-107">Hello lista siguiente especifica cómo se puede utilizar la información adicional de hello:</span><span class="sxs-lookup"><span data-stu-id="964ee-107">hello following list specifies how hello additional information can be used:</span></span>

1. <span data-ttu-id="964ee-108">Identificar el tipo de error de Hola.</span><span class="sxs-lookup"><span data-stu-id="964ee-108">Identify hello failure type.</span></span>
2. <span data-ttu-id="964ee-109">Identificar el motivo del error de Hola.</span><span class="sxs-lookup"><span data-stu-id="964ee-109">Identify hello failure reason.</span></span>
3. <span data-ttu-id="964ee-110">Aísle uno o más componentes de error para investigarlos en profundidad.</span><span class="sxs-lookup"><span data-stu-id="964ee-110">Isolate one or more failing components for further investigation.</span></span>

<span data-ttu-id="964ee-111">Esta información está disponible cuando el tejido de servicio detecta el error de hello independientemente de si hello **FailureAction** tooroll vuelve o suspender actualización Hola.</span><span class="sxs-lookup"><span data-stu-id="964ee-111">This information is available when Service Fabric detects hello failure regardless of whether hello **FailureAction** is tooroll back or suspend hello upgrade.</span></span>

### <a name="identify-hello-failure-type"></a><span data-ttu-id="964ee-112">Identificar el tipo de error de Hola</span><span class="sxs-lookup"><span data-stu-id="964ee-112">Identify hello failure type</span></span>
<span data-ttu-id="964ee-113">En la salida de hello de **Get ServiceFabricApplicationUpgrade**, **FailureTimestampUtc** identifica Hola marca de tiempo (en UTC) a la que se detectó un error de actualización por Service Fabric y  **FailureAction** se activó.</span><span class="sxs-lookup"><span data-stu-id="964ee-113">In hello output of **Get-ServiceFabricApplicationUpgrade**, **FailureTimestampUtc** identifies hello timestamp (in UTC) at which an upgrade failure was detected by Service Fabric and **FailureAction** was triggered.</span></span> <span data-ttu-id="964ee-114">**FailureReason** identifica a uno de tres posibles causas del error de Hola de alto nivel:</span><span class="sxs-lookup"><span data-stu-id="964ee-114">**FailureReason** identifies one of three potential high-level causes of hello failure:</span></span>

1. <span data-ttu-id="964ee-115">UpgradeDomainTimeout - indica que un dominio de actualización concreto tardó demasiado toocomplete y **UpgradeDomainTimeout** expirado.</span><span class="sxs-lookup"><span data-stu-id="964ee-115">UpgradeDomainTimeout - Indicates that a particular upgrade domain took too long toocomplete and **UpgradeDomainTimeout** expired.</span></span>
2. <span data-ttu-id="964ee-116">OverallUpgradeTimeout - indica que Hola global de actualización tardó demasiado toocomplete y **UpgradeTimeout** expirado.</span><span class="sxs-lookup"><span data-stu-id="964ee-116">OverallUpgradeTimeout - Indicates that hello overall upgrade took too long toocomplete and **UpgradeTimeout** expired.</span></span>
3. <span data-ttu-id="964ee-117">La comprobación de estado - indica que, después de actualizar un dominio de actualización, aplicación hello permanecido incorrecto según toohello especifica las directivas de mantenimiento y **HealthCheckRetryTimeout** expirado.</span><span class="sxs-lookup"><span data-stu-id="964ee-117">HealthCheck - Indicates that after upgrading an update domain, hello application remained unhealthy according toohello specified health policies and **HealthCheckRetryTimeout** expired.</span></span>

<span data-ttu-id="964ee-118">Estas entradas sólo se muestran en la salida de hello al actualización Hola se produce un error e inicia la reversión.</span><span class="sxs-lookup"><span data-stu-id="964ee-118">These entries only show up in hello output when hello upgrade fails and starts rolling back.</span></span> <span data-ttu-id="964ee-119">Según el tipo de saludo de error de Hola se muestra información adicional.</span><span class="sxs-lookup"><span data-stu-id="964ee-119">Further information is displayed depending on hello type of hello failure.</span></span>

### <a name="investigate-upgrade-timeouts"></a><span data-ttu-id="964ee-120">Investigar los tiempos de espera de actualización</span><span class="sxs-lookup"><span data-stu-id="964ee-120">Investigate upgrade timeouts</span></span>
<span data-ttu-id="964ee-121">Los errores de tiempo de espera de actualización se producen habitualmente por problemas de disponibilidad del servicio.</span><span class="sxs-lookup"><span data-stu-id="964ee-121">Upgrade timeout failures are most commonly caused by service availability issues.</span></span> <span data-ttu-id="964ee-122">salida de Hello siguiendo este párrafo es típico de las actualizaciones en los que las réplicas de servicio o instancias no toostart en la nueva versión de código de hello.</span><span class="sxs-lookup"><span data-stu-id="964ee-122">hello output following this paragraph is typical of upgrades where service replicas or instances fail toostart in hello new code version.</span></span> <span data-ttu-id="964ee-123">Hola **UpgradeDomainProgressAtFailure** campo captura una instantánea de cualquier trabajo de actualización pendiente en tiempo de Hola de error.</span><span class="sxs-lookup"><span data-stu-id="964ee-123">hello **UpgradeDomainProgressAtFailure** field captures a snapshot of any pending upgrade work at hello time of failure.</span></span>

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

<span data-ttu-id="964ee-124">En este ejemplo, no se pudo actualizar hello en el dominio de actualización *MYUD1* y dos particiones (*744c8d9f-1d26-417e-a60e-cd48f5c098f0* y *4b43f4d8-b26b-424e-9307-7a7a62e79750*) se bloquea.</span><span class="sxs-lookup"><span data-stu-id="964ee-124">In this example, hello upgrade failed at upgrade domain *MYUD1* and two partitions (*744c8d9f-1d26-417e-a60e-cd48f5c098f0* and *4b43f4d8-b26b-424e-9307-7a7a62e79750*) were stuck.</span></span> <span data-ttu-id="964ee-125">particiones Hola se queda bloqueadas porque en tiempo de ejecución de hello era réplicas principales no se puede tooplace (*WaitForPrimaryPlacement*) en nodos de destino *Nodo1* y *Nodo4*.</span><span class="sxs-lookup"><span data-stu-id="964ee-125">hello partitions were stuck because hello runtime was unable tooplace primary replicas (*WaitForPrimaryPlacement*) on target nodes *Node1* and *Node4*.</span></span>

<span data-ttu-id="964ee-126">Hola **Get ServiceFabricNode** comando puede ser usado tooverify que estos dos nodos están en el dominio de actualización *MYUD1*.</span><span class="sxs-lookup"><span data-stu-id="964ee-126">hello **Get-ServiceFabricNode** command can be used tooverify that these two nodes are in upgrade domain *MYUD1*.</span></span> <span data-ttu-id="964ee-127">Hola *UpgradePhase* dice *PostUpgradeSafetyCheck*, lo que significa que estas comprobaciones de seguridad se producen después de que todos los nodos de dominio de actualización de hello han finalizado la actualización.</span><span class="sxs-lookup"><span data-stu-id="964ee-127">hello *UpgradePhase* says *PostUpgradeSafetyCheck*, which means that these safety checks are occurring after all nodes in hello upgrade domain have finished upgrading.</span></span> <span data-ttu-id="964ee-128">Toda esta información apunta tooa posible problema con la nueva versión de Hola Hola del código de aplicación.</span><span class="sxs-lookup"><span data-stu-id="964ee-128">All this information points tooa potential issue with hello new version of hello application code.</span></span> <span data-ttu-id="964ee-129">los problemas más comunes de Hello son errores del servicio en Hola abierto o las rutas de código de promoción tooprimary.</span><span class="sxs-lookup"><span data-stu-id="964ee-129">hello most common issues are service errors in hello open or promotion tooprimary code paths.</span></span>

<span data-ttu-id="964ee-130">Un *UpgradePhase* de *PreUpgradeSafetyCheck* significa hubo problemas de preparación de dominio de actualización de hello antes de que se haya ejecutado.</span><span class="sxs-lookup"><span data-stu-id="964ee-130">An *UpgradePhase* of *PreUpgradeSafetyCheck* means there were issues preparing hello upgrade domain before it was performed.</span></span> <span data-ttu-id="964ee-131">en este caso, los problemas más comunes de Hello son errores del servicio de cierre Hola o degradación de las rutas de código principal.</span><span class="sxs-lookup"><span data-stu-id="964ee-131">hello most common issues in this case are service errors in hello close or demotion from primary code paths.</span></span>

<span data-ttu-id="964ee-132">Hola actual **UpgradeState** es *RollingBackCompleted*, por lo que la actualización original Hola debe haberse realizada con una reversión **FailureAction**, que automáticamente revierte la actualización de hello en caso de error.</span><span class="sxs-lookup"><span data-stu-id="964ee-132">hello current **UpgradeState** is *RollingBackCompleted*, so hello original upgrade must have been performed with a rollback **FailureAction**, which automatically rolled back hello upgrade upon failure.</span></span> <span data-ttu-id="964ee-133">Si se realizó la actualización original Hola con un manual **FailureAction**, entonces en su lugar se actualización hello en un activo de depuración de la aplicación hello tooallow de estado suspendido.</span><span class="sxs-lookup"><span data-stu-id="964ee-133">If hello original upgrade was performed with a manual **FailureAction**, then hello upgrade would instead be in a suspended state tooallow live debugging of hello application.</span></span>

### <a name="investigate-health-check-failures"></a><span data-ttu-id="964ee-134">Investigar errores de comprobación de estado</span><span class="sxs-lookup"><span data-stu-id="964ee-134">Investigate health check failures</span></span>
<span data-ttu-id="964ee-135">Los errores de comprobación de estado pueden desencadenarse debido a varios problemas que se pueden producir después de que todos los nodos de un dominio de actualización terminen de actualizarse y pasen todas las comprobaciones de seguridad.</span><span class="sxs-lookup"><span data-stu-id="964ee-135">Health check failures can be triggered by various issues that can happen after all nodes in an upgrade domain finish upgrading and passing all safety checks.</span></span> <span data-ttu-id="964ee-136">salida de Hello siguiendo este párrafo es típico de un error de actualización debido a comprobaciones de mantenimiento de toofailed.</span><span class="sxs-lookup"><span data-stu-id="964ee-136">hello output following this paragraph is typical of an upgrade failure due toofailed health checks.</span></span> <span data-ttu-id="964ee-137">Hola **UnhealthyEvaluations** campo captura una instantánea de comprobaciones de estado que no se pudo en tiempo de Hola de actualización de hello según toohello especificado [directiva de mantenimiento](service-fabric-health-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="964ee-137">hello **UnhealthyEvaluations** field captures a snapshot of health checks that failed at hello time of hello upgrade according toohello specified [health policy](service-fabric-health-introduction.md).</span></span>

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

<span data-ttu-id="964ee-138">Investigar errores de comprobación de mantenimiento, en primer lugar requiere una descripción del modelo de estado de Service Fabric Hola.</span><span class="sxs-lookup"><span data-stu-id="964ee-138">Investigating health check failures first requires an understanding of hello Service Fabric health model.</span></span> <span data-ttu-id="964ee-139">Pero incluso sin una comprensión detallada, podemos ver que los dos servicios tienen un estado incorrecto: *fabric: / DemoApp/Svc3* y *fabric: / DemoApp/Svc2*, junto con los informes de estado de error de hello ("InjectedFault "en este caso).</span><span class="sxs-lookup"><span data-stu-id="964ee-139">But even without such an in-depth understanding, we can see that two services are unhealthy: *fabric:/DemoApp/Svc3* and *fabric:/DemoApp/Svc2*, along with hello error health reports ("InjectedFault" in this case).</span></span> <span data-ttu-id="964ee-140">En este ejemplo, dos de los cuatro servicios tienen un estado incorrecto, que está por debajo del umbral de hello predeterminado del 0% incorrecto (*MaxPercentUnhealthyServices*).</span><span class="sxs-lookup"><span data-stu-id="964ee-140">In this example, two out of four services are unhealthy, which is below hello default target of 0% unhealthy (*MaxPercentUnhealthyServices*).</span></span>

<span data-ttu-id="964ee-141">Hello actualización suspendió tras error especificando un **FailureAction** de cuando manual a partir de Hola actualización.</span><span class="sxs-lookup"><span data-stu-id="964ee-141">hello upgrade was suspended upon failing by specifying a **FailureAction** of manual when starting hello upgrade.</span></span> <span data-ttu-id="964ee-142">Este modo nos permite sistemas en vivo de hello tooinvestigate en estado de error de hello antes de realizar ninguna acción adicional.</span><span class="sxs-lookup"><span data-stu-id="964ee-142">This mode allows us tooinvestigate hello live system in hello failed state before taking any further action.</span></span>

### <a name="recover-from-a-suspended-upgrade"></a><span data-ttu-id="964ee-143">Recuperarse de una actualización suspendida</span><span class="sxs-lookup"><span data-stu-id="964ee-143">Recover from a suspended upgrade</span></span>
<span data-ttu-id="964ee-144">Con una reversión **FailureAction**, no hay ninguna recuperación es necesario ya que la actualización de Hola se revierte automáticamente al error.</span><span class="sxs-lookup"><span data-stu-id="964ee-144">With a rollback **FailureAction**, there is no recovery needed since hello upgrade automatically rolls back upon failing.</span></span> <span data-ttu-id="964ee-145">Con una **FailureAction**manual, hay varias opciones de recuperación:</span><span class="sxs-lookup"><span data-stu-id="964ee-145">With a manual **FailureAction**, there are several recovery options:</span></span>

1.  <span data-ttu-id="964ee-146">Desencadenar una reversión</span><span class="sxs-lookup"><span data-stu-id="964ee-146">trigger a rollback</span></span>
2. <span data-ttu-id="964ee-147">Continuar a través del resto de Hola de actualización de hello manualmente</span><span class="sxs-lookup"><span data-stu-id="964ee-147">Proceed through hello remainder of hello upgrade manually</span></span>
3. <span data-ttu-id="964ee-148">Hola reanudar supervisa la actualización</span><span class="sxs-lookup"><span data-stu-id="964ee-148">Resume hello monitored upgrade</span></span>

<span data-ttu-id="964ee-149">Hola **ServiceFabricApplicationRollback inicio** comando se puede usar en cualquier toostart tiempo Revertir aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="964ee-149">hello **Start-ServiceFabricApplicationRollback** command can be used at any time toostart rolling back hello application.</span></span> <span data-ttu-id="964ee-150">Una vez que se devuelve correctamente el comando hello, una solicitud rollback Hola se ha registrado en el sistema de hello e inicia poco después.</span><span class="sxs-lookup"><span data-stu-id="964ee-150">Once hello command returns successfully, hello rollback request has been registered in hello system and starts shortly thereafter.</span></span>

<span data-ttu-id="964ee-151">Hola **ServiceFabricApplicationUpgrade reanudar** comando se puede usar tooproceed a través del resto de Hola de hello manualmente, actualizar un dominio de actualización a la vez.</span><span class="sxs-lookup"><span data-stu-id="964ee-151">hello **Resume-ServiceFabricApplicationUpgrade** command can be used tooproceed through hello remainder of hello upgrade manually, one upgrade domain at a time.</span></span> <span data-ttu-id="964ee-152">En este modo, se realizan comprobaciones de seguridad solo sistema Hola.</span><span class="sxs-lookup"><span data-stu-id="964ee-152">In this mode, only safety checks are performed by hello system.</span></span> <span data-ttu-id="964ee-153">No se realizan más comprobaciones de estado.</span><span class="sxs-lookup"><span data-stu-id="964ee-153">No more health checks are performed.</span></span> <span data-ttu-id="964ee-154">Este comando solo puede usarse cuando hello *UpgradeState* muestra *RollingForwardPending*, lo que significa que ese dominio de actualización actual de hello ha finalizado la actualización pero hello junto uno no ha comenzado (pendiente).</span><span class="sxs-lookup"><span data-stu-id="964ee-154">This command can only be used when hello *UpgradeState* shows *RollingForwardPending*, which means that hello current upgrade domain has finished upgrading but hello next one has not started (pending).</span></span>

<span data-ttu-id="964ee-155">Hola **ServiceFabricApplicationUpgrade actualización** comando se puede tooresume usado Hola supervisado actualización con las comprobaciones de seguridad y mantenimiento que se va a realizar.</span><span class="sxs-lookup"><span data-stu-id="964ee-155">hello **Update-ServiceFabricApplicationUpgrade** command can be used tooresume hello monitored upgrade with both safety and health checks being performed.</span></span>

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

<span data-ttu-id="964ee-156">actualización de Hello continúa a partir de hello de uso mismo actualizar parámetros y las directivas de mantenimiento como antes y de dominio de actualización de Hola donde se suspendió la última.</span><span class="sxs-lookup"><span data-stu-id="964ee-156">hello upgrade continues from hello upgrade domain where it was last suspended and use hello same upgrade parameters and health policies as before.</span></span> <span data-ttu-id="964ee-157">Si es necesario, cualquiera de los parámetros de actualización de Hola y las directivas de mantenimiento que se muestra en hello anterior salida puede cambiarse en hello mismo comando cuando se reanuda la actualización de Hola.</span><span class="sxs-lookup"><span data-stu-id="964ee-157">If needed, any of hello upgrade parameters and health policies shown in hello preceding output can be changed in hello same command when hello upgrade resumes.</span></span> <span data-ttu-id="964ee-158">En este ejemplo, se reanudó actualización hello en modo supervisado, con parámetros de Hola y las directivas de mantenimiento de hello sin cambios.</span><span class="sxs-lookup"><span data-stu-id="964ee-158">In this example, hello upgrade was resumed in Monitored mode, with hello parameters and hello health policies unchanged.</span></span>

## <a name="further-troubleshooting"></a><span data-ttu-id="964ee-159">Más información de solución de problemas</span><span class="sxs-lookup"><span data-stu-id="964ee-159">Further troubleshooting</span></span>
### <a name="service-fabric-is-not-following-hello-specified-health-policies"></a><span data-ttu-id="964ee-160">Service Fabric no es posterior a Hola especificada las directivas de mantenimiento</span><span class="sxs-lookup"><span data-stu-id="964ee-160">Service Fabric is not following hello specified health policies</span></span>
<span data-ttu-id="964ee-161">Causa posible 1:</span><span class="sxs-lookup"><span data-stu-id="964ee-161">Possible Cause 1:</span></span>

<span data-ttu-id="964ee-162">Service Fabric convierte todos los porcentajes en números reales de entidades (por ejemplo, las réplicas, particiones y servicios) para la evaluación de mantenimiento y siempre se redondea hacia arriba toowhole entidades.</span><span class="sxs-lookup"><span data-stu-id="964ee-162">Service Fabric translates all percentages into actual numbers of entities (for example, replicas, partitions, and services) for health evaluation and always rounds up toowhole entities.</span></span> <span data-ttu-id="964ee-163">Por ejemplo, si hello máximo *MaxPercentUnhealthyReplicasPerPartition* es % 21 y hay cinco réplicas, Service Fabric permite que un tootwo réplicas en mal estado (es decir,`Math.Ceiling (5*0.21)`).</span><span class="sxs-lookup"><span data-stu-id="964ee-163">For example, if hello maximum *MaxPercentUnhealthyReplicasPerPartition* is 21% and there are five replicas, then Service Fabric allows up tootwo unhealthy replicas (that is,`Math.Ceiling (5*0.21)`).</span></span> <span data-ttu-id="964ee-164">Por lo tanto, las directivas de mantenimiento deben establecerse como corresponda.</span><span class="sxs-lookup"><span data-stu-id="964ee-164">Thus, health policies should be set accordingly.</span></span>

<span data-ttu-id="964ee-165">Causa posible 2:</span><span class="sxs-lookup"><span data-stu-id="964ee-165">Possible Cause 2:</span></span>

<span data-ttu-id="964ee-166">Las directivas de mantenimiento se especifican en términos de porcentajes de servicios totales e instancias de servicio no específicas.</span><span class="sxs-lookup"><span data-stu-id="964ee-166">Health policies are specified in terms of percentages of total services and not specific service instances.</span></span> <span data-ttu-id="964ee-167">Por ejemplo, antes de una actualización, si una aplicación tiene al menos cuatro instancias A, B, C y D, de servicio donde servicio D es incorrecto, pero con aplicaciones de toohello de poco impacto.</span><span class="sxs-lookup"><span data-stu-id="964ee-167">For example, before an upgrade, if an application has four service instances A, B, C, and D, where service D is unhealthy but with little impact toohello application.</span></span> <span data-ttu-id="964ee-168">Queremos hello tooignore conoce servicio D en mal estado durante el parámetro hello de actualización y defina *MaxPercentUnhealthyServices* toobe 25%, suponiendo que sólo A, B y C necesita toobe correcto.</span><span class="sxs-lookup"><span data-stu-id="964ee-168">We want tooignore hello known unhealthy service D during upgrade and set hello parameter *MaxPercentUnhealthyServices* toobe 25%, assuming only A, B, and C need toobe healthy.</span></span>

<span data-ttu-id="964ee-169">Sin embargo, durante la actualización de hello, d. quede correcto mientras C pasa a ser incorrecto.</span><span class="sxs-lookup"><span data-stu-id="964ee-169">However, during hello upgrade, D may become healthy while C becomes unhealthy.</span></span> <span data-ttu-id="964ee-170">actualización de Hello seguirían ejecutando correctamente porque solo el 25% de los servicios de hello tienen un estado incorrecto.</span><span class="sxs-lookup"><span data-stu-id="964ee-170">hello upgrade would still succeed because only 25% of hello services are unhealthy.</span></span> <span data-ttu-id="964ee-171">Sin embargo, podría dar como resultado errores no anticipados debido a que se va a tooC incorrecto inesperadamente en lugar de D. En esta situación, se debe modelar d. como un tipo de servicio diferente de A, B y C. Puesto que las directivas de mantenimiento se especifican por tipo de servicio, umbrales de otro porcentaje incorrecto pueden ser servicios toodifferent aplicada.</span><span class="sxs-lookup"><span data-stu-id="964ee-171">However, it might result in unanticipated errors due tooC being unexpectedly unhealthy instead of D. In this situation, D should be modeled as a different service type from A, B, and C. Since health policies are specified per service type, different unhealthy percentage thresholds can be applied toodifferent services.</span></span> 

### <a name="i-did-not-specify-a-health-policy-for-application-upgrade-but-hello-upgrade-still-fails-for-some-time-outs-that-i-never-specified"></a><span data-ttu-id="964ee-172">No especificó una directiva de mantenimiento para la actualización de la aplicación, pero sigue sin funcionar actualización Hola para algunos tiempos de espera que no se especificó nunca</span><span class="sxs-lookup"><span data-stu-id="964ee-172">I did not specify a health policy for application upgrade, but hello upgrade still fails for some time-outs that I never specified</span></span>
<span data-ttu-id="964ee-173">Cuando las directivas de mantenimiento no se proporciona la solicitud de actualización de toohello, se toman del hello *ApplicationManifest.xml* de la versión actual de la aplicación de Hola.</span><span class="sxs-lookup"><span data-stu-id="964ee-173">When health policies aren't provided toohello upgrade request, they are taken from hello *ApplicationManifest.xml* of hello current application version.</span></span> <span data-ttu-id="964ee-174">Por ejemplo, si está actualizando X de la aplicación desde la versión 1.0 tooversion 2.0, se usan las directivas de mantenimiento de aplicación especificadas para en la versión 1.0.</span><span class="sxs-lookup"><span data-stu-id="964ee-174">For example, if you're upgrading Application X from version 1.0 tooversion 2.0, application health policies specified for in version 1.0 are used.</span></span> <span data-ttu-id="964ee-175">Si se debe utilizar una directiva de mantenimiento diferente para la actualización de hello, directiva de hello debe toobe especificado como parte de la llamada de API de actualización de hello aplicación.</span><span class="sxs-lookup"><span data-stu-id="964ee-175">If a different health policy should be used for hello upgrade, then hello policy needs toobe specified as part of hello application upgrade API call.</span></span> <span data-ttu-id="964ee-176">Hello directivas especificadas como parte de la llamada de hello API solo se aplican durante la actualización de Hola.</span><span class="sxs-lookup"><span data-stu-id="964ee-176">hello policies specified as part of hello API call only apply during hello upgrade.</span></span> <span data-ttu-id="964ee-177">Una vez completada la actualización de hello, directivas de hello especificaron en hello *ApplicationManifest.xml* se usan.</span><span class="sxs-lookup"><span data-stu-id="964ee-177">Once hello upgrade is complete, hello policies specified in hello *ApplicationManifest.xml* are used.</span></span>

### <a name="incorrect-time-outs-are-specified"></a><span data-ttu-id="964ee-178">Se especifican los tiempos de expiración incorrectos</span><span class="sxs-lookup"><span data-stu-id="964ee-178">Incorrect time-outs are specified</span></span>
<span data-ttu-id="964ee-179">Es posible que se pregunte por lo que sucede cuando los tiempos de espera se establecen de forma incoherente.</span><span class="sxs-lookup"><span data-stu-id="964ee-179">You may have wondered about what happens when time-outs are set inconsistently.</span></span> <span data-ttu-id="964ee-180">Por ejemplo, puede tener un *UpgradeTimeout* que es menor que hello *UpgradeDomainTimeout*.</span><span class="sxs-lookup"><span data-stu-id="964ee-180">For example, you may have an *UpgradeTimeout* that's less than hello *UpgradeDomainTimeout*.</span></span> <span data-ttu-id="964ee-181">respuesta de Hello es que se devuelva un error.</span><span class="sxs-lookup"><span data-stu-id="964ee-181">hello answer is that an error is returned.</span></span> <span data-ttu-id="964ee-182">Los errores se devuelven si hello *UpgradeDomainTimeout* es menor que la suma de Hola de *HealthCheckWaitDuration* y *HealthCheckRetryTimeout*, o si  *UpgradeDomainTimeout* es menor que la suma de Hola de *HealthCheckWaitDuration* y *HealthCheckStableDuration*.</span><span class="sxs-lookup"><span data-stu-id="964ee-182">Errors are returned if hello *UpgradeDomainTimeout* is less than hello sum of *HealthCheckWaitDuration* and *HealthCheckRetryTimeout*, or if *UpgradeDomainTimeout* is less than hello sum of *HealthCheckWaitDuration* and *HealthCheckStableDuration*.</span></span>

### <a name="my-upgrades-are-taking-too-long"></a><span data-ttu-id="964ee-183">Mis actualizaciones están tardando mucho tiempo</span><span class="sxs-lookup"><span data-stu-id="964ee-183">My upgrades are taking too long</span></span>
<span data-ttu-id="964ee-184">tiempo de Hola para una actualización toocomplete depende de las comprobaciones de mantenimiento de Hola y los tiempos de espera especificados.</span><span class="sxs-lookup"><span data-stu-id="964ee-184">hello time for an upgrade toocomplete depends on hello health checks and time-outs specified.</span></span> <span data-ttu-id="964ee-185">Comprobaciones de estado y los tiempos de espera dependen sobre cuánto tiempo tarda toocopy, implementación y estabilizan la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="964ee-185">Health checks and time-outs depend on how long it takes toocopy, deploy, and stabilize hello application.</span></span> <span data-ttu-id="964ee-186">Ser demasiado agresivo con los tiempos de expiración puede dar lugar a que se realicen más actualizaciones con errores; por ello, recomendamos empezar de manera conservadora con tiempos de expiración más prolongados.</span><span class="sxs-lookup"><span data-stu-id="964ee-186">Being too aggressive with time-outs might mean more failed upgrades, so we recommend starting conservatively with longer time-outs.</span></span>

<span data-ttu-id="964ee-187">Este es un rápido repaso sobre cómo interactúan los tiempos de espera de hello con tiempos de actualización de hello:</span><span class="sxs-lookup"><span data-stu-id="964ee-187">Here's a quick refresher on how hello time-outs interact with hello upgrade times:</span></span>

<span data-ttu-id="964ee-188">Las actualizaciones de un dominio de actualización no se pueden completar con mayor rapidez que *HealthCheckWaitDuration* + *HealthCheckStableDuration*.</span><span class="sxs-lookup"><span data-stu-id="964ee-188">Upgrades for an upgrade domain cannot complete faster than *HealthCheckWaitDuration* + *HealthCheckStableDuration*.</span></span>

<span data-ttu-id="964ee-189">No se puede producir un error de actualización con mayor rapidez que *HealthCheckWaitDuration* + *HealthCheckRetryTimeout*.</span><span class="sxs-lookup"><span data-stu-id="964ee-189">Upgrade failure cannot occur faster than *HealthCheckWaitDuration* + *HealthCheckRetryTimeout*.</span></span>

<span data-ttu-id="964ee-190">Hello tiempo de actualización de un dominio de actualización limita *UpgradeDomainTimeout*.</span><span class="sxs-lookup"><span data-stu-id="964ee-190">hello upgrade time for an upgrade domain is limited by *UpgradeDomainTimeout*.</span></span>  <span data-ttu-id="964ee-191">Si *HealthCheckRetryTimeout* y *HealthCheckStableDuration* son distintos de cero y el estado de saludo de la aplicación hello mantiene cambio y hacia atrás, a continuación, la actualización de hello agota el tiempo de en  *UpgradeDomainTimeout*.</span><span class="sxs-lookup"><span data-stu-id="964ee-191">If *HealthCheckRetryTimeout* and *HealthCheckStableDuration* are both non-zero and hello health of hello application keeps switching back and forth, then hello upgrade eventually times out on *UpgradeDomainTimeout*.</span></span> <span data-ttu-id="964ee-192">*UpgradeDomainTimeout* empieza a contar hacia abajo una vez Hola actualización de dominio de actualización actual Hola comienza.</span><span class="sxs-lookup"><span data-stu-id="964ee-192">*UpgradeDomainTimeout* starts counting down once hello upgrade for hello current upgrade domain begins.</span></span>

## <a name="next-steps"></a><span data-ttu-id="964ee-193">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="964ee-193">Next steps</span></span>
<span data-ttu-id="964ee-194">[actualización de aplicaciones usando Visual Studio](service-fabric-application-upgrade-tutorial.md) ofrece información para actualizar una aplicación mediante Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="964ee-194">[Upgrading your Application Using Visual Studio](service-fabric-application-upgrade-tutorial.md) walks you through an application upgrade using Visual Studio.</span></span>

<span data-ttu-id="964ee-195">[actualización de aplicaciones mediante PowerShell](service-fabric-application-upgrade-tutorial-powershell.md) se explica en detalle lo que tiene que hacer para actualizar una aplicación mediante PowerShell.</span><span class="sxs-lookup"><span data-stu-id="964ee-195">[Upgrading your Application Using Powershell](service-fabric-application-upgrade-tutorial-powershell.md) walks you through an application upgrade using PowerShell.</span></span>

<span data-ttu-id="964ee-196">Puede controlar cómo se actualiza una aplicación usando [parámetros de actualización](service-fabric-application-upgrade-parameters.md).</span><span class="sxs-lookup"><span data-stu-id="964ee-196">Control how your application upgrades by using [Upgrade Parameters](service-fabric-application-upgrade-parameters.md).</span></span>

<span data-ttu-id="964ee-197">Hacer que las actualizaciones de la aplicación sea compatible por el aprendizaje cómo toouse [serialización de datos](service-fabric-application-upgrade-data-serialization.md).</span><span class="sxs-lookup"><span data-stu-id="964ee-197">Make your application upgrades compatible by learning how toouse [Data Serialization](service-fabric-application-upgrade-data-serialization.md).</span></span>

<span data-ttu-id="964ee-198">Obtenga información acerca de cómo toouse funcionalidad avanzada al actualizar la aplicación, se hace referencia demasiado[temas avanzados](service-fabric-application-upgrade-advanced.md).</span><span class="sxs-lookup"><span data-stu-id="964ee-198">Learn how toouse advanced functionality while upgrading your application by referring too[Advanced Topics](service-fabric-application-upgrade-advanced.md).</span></span>
