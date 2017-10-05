---
title: "Solución de problemas de las actualizaciones de aplicaciones | Microsoft Docs"
description: "En este artículo se tratan algunos de los problemas comunes de actualización de una aplicación de Service Fabric y cómo resolverlos."
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
ms.openlocfilehash: f7f6bc0c29e2b43fbc8e451c5a4a50110b78349e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="troubleshoot-application-upgrades"></a><span data-ttu-id="3847a-103">Solucionar problemas de actualizaciones de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="3847a-103">Troubleshoot application upgrades</span></span>
<span data-ttu-id="3847a-104">En este artículo se tratan algunos de los problemas comunes de actualización de una aplicación de Azure Service Fabric y cómo resolverlos.</span><span class="sxs-lookup"><span data-stu-id="3847a-104">This article covers some of the common issues around upgrading an Azure Service Fabric application and how to resolve them.</span></span>

## <a name="troubleshoot-a-failed-application-upgrade"></a><span data-ttu-id="3847a-105">Solucionar problemas de una actualización de aplicación con error</span><span class="sxs-lookup"><span data-stu-id="3847a-105">Troubleshoot a failed application upgrade</span></span>
<span data-ttu-id="3847a-106">Cuando se produce un error en una actualización, la salida del comando **Get-ServiceFabricApplicationUpgrade** contiene información adicional para depurar el error.</span><span class="sxs-lookup"><span data-stu-id="3847a-106">When an upgrade fails, the output of the **Get-ServiceFabricApplicationUpgrade** command contains additional information for debugging the failure.</span></span>  <span data-ttu-id="3847a-107">En la lista siguiente se especifica cómo se puede usar esa información adicional:</span><span class="sxs-lookup"><span data-stu-id="3847a-107">The following list specifies how the additional information can be used:</span></span>

1. <span data-ttu-id="3847a-108">Identificar el tipo de error.</span><span class="sxs-lookup"><span data-stu-id="3847a-108">Identify the failure type.</span></span>
2. <span data-ttu-id="3847a-109">Identificar el motivo del error.</span><span class="sxs-lookup"><span data-stu-id="3847a-109">Identify the failure reason.</span></span>
3. <span data-ttu-id="3847a-110">Aísle uno o más componentes de error para investigarlos en profundidad.</span><span class="sxs-lookup"><span data-stu-id="3847a-110">Isolate one or more failing components for further investigation.</span></span>

<span data-ttu-id="3847a-111">Esta información está disponible tan pronto como Service Fabric detecta el error, con independencia de si el valor de **FailureAction** es revertir o suspender la actualización.</span><span class="sxs-lookup"><span data-stu-id="3847a-111">This information is available when Service Fabric detects the failure regardless of whether the **FailureAction** is to roll back or suspend the upgrade.</span></span>

### <a name="identify-the-failure-type"></a><span data-ttu-id="3847a-112">Identificar el tipo de error</span><span class="sxs-lookup"><span data-stu-id="3847a-112">Identify the failure type</span></span>
<span data-ttu-id="3847a-113">En la salida de **Get-ServiceFabricApplicationUpgrade**, **FailureTimestampUtc** identifica la marca de tiempo (en UTC) en la que Service Fabric encontró un error de actualización y se desencadenó **FailureAction**.</span><span class="sxs-lookup"><span data-stu-id="3847a-113">In the output of **Get-ServiceFabricApplicationUpgrade**, **FailureTimestampUtc** identifies the timestamp (in UTC) at which an upgrade failure was detected by Service Fabric and **FailureAction** was triggered.</span></span> <span data-ttu-id="3847a-114">**FailureReason** identifica una de las tres posibles causas de alto nivel del error:</span><span class="sxs-lookup"><span data-stu-id="3847a-114">**FailureReason** identifies one of three potential high-level causes of the failure:</span></span>

1. <span data-ttu-id="3847a-115">UpgradeDomainTimeout: indica que un determinado dominio de actualización tardó demasiado tiempo en completarse y **UpgradeDomainTimeout** expiró.</span><span class="sxs-lookup"><span data-stu-id="3847a-115">UpgradeDomainTimeout - Indicates that a particular upgrade domain took too long to complete and **UpgradeDomainTimeout** expired.</span></span>
2. <span data-ttu-id="3847a-116">OverallUpgradeTimeout: indica que la actualización general tardó demasiado tiempo en completarse y **UpgradeTimeout** expiró.</span><span class="sxs-lookup"><span data-stu-id="3847a-116">OverallUpgradeTimeout - Indicates that the overall upgrade took too long to complete and **UpgradeTimeout** expired.</span></span>
3. <span data-ttu-id="3847a-117">HealthCheck: indica que, tras la actualización de un dominio de actualización, la aplicación permaneció en estado incorrecto según las directivas de mantenimiento especificadas y **HealthCheckRetryTimeout** expiró.</span><span class="sxs-lookup"><span data-stu-id="3847a-117">HealthCheck - Indicates that after upgrading an update domain, the application remained unhealthy according to the specified health policies and **HealthCheckRetryTimeout** expired.</span></span>

<span data-ttu-id="3847a-118">Estas entradas solo aparecen en la salida cuando se produce un error en la actualización y empieza la reversión.</span><span class="sxs-lookup"><span data-stu-id="3847a-118">These entries only show up in the output when the upgrade fails and starts rolling back.</span></span> <span data-ttu-id="3847a-119">Según el tipo de error, se muestra información adicional.</span><span class="sxs-lookup"><span data-stu-id="3847a-119">Further information is displayed depending on the type of the failure.</span></span>

### <a name="investigate-upgrade-timeouts"></a><span data-ttu-id="3847a-120">Investigar los tiempos de espera de actualización</span><span class="sxs-lookup"><span data-stu-id="3847a-120">Investigate upgrade timeouts</span></span>
<span data-ttu-id="3847a-121">Los errores de tiempo de espera de actualización se producen habitualmente por problemas de disponibilidad del servicio.</span><span class="sxs-lookup"><span data-stu-id="3847a-121">Upgrade timeout failures are most commonly caused by service availability issues.</span></span> <span data-ttu-id="3847a-122">La salida que sigue a este párrafo es habitual de las actualizaciones donde réplicas o instancias de servicio no se pueden iniciar en la nueva versión del código.</span><span class="sxs-lookup"><span data-stu-id="3847a-122">The output following this paragraph is typical of upgrades where service replicas or instances fail to start in the new code version.</span></span> <span data-ttu-id="3847a-123">El campo **UpgradeDomainProgressAtFailure** captura una instantánea de cualquier trabajo de actualización pendiente en el momento del error.</span><span class="sxs-lookup"><span data-stu-id="3847a-123">The **UpgradeDomainProgressAtFailure** field captures a snapshot of any pending upgrade work at the time of failure.</span></span>

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

<span data-ttu-id="3847a-124">En este ejemplo, la actualización produjo error en el dominio de actualización *MYUD1* y dos particiones, (*744c8d9f-1d26-417e-a60e-cd48f5c098f0* y *4b43f4d8-b26b-424e-9307-7a7a62e79750*), se bloquearon.</span><span class="sxs-lookup"><span data-stu-id="3847a-124">In this example, the upgrade failed at upgrade domain *MYUD1* and two partitions (*744c8d9f-1d26-417e-a60e-cd48f5c098f0* and *4b43f4d8-b26b-424e-9307-7a7a62e79750*) were stuck.</span></span> <span data-ttu-id="3847a-125">Esto fue debido a que el entorno de tiempo de ejecución no pudo colocar las réplicas principales (*WaitForPrimaryPlacement*) en los nodos de destino *Node1* y *Node4*.</span><span class="sxs-lookup"><span data-stu-id="3847a-125">The partitions were stuck because the runtime was unable to place primary replicas (*WaitForPrimaryPlacement*) on target nodes *Node1* and *Node4*.</span></span>

<span data-ttu-id="3847a-126">El comando **Get-ServiceFabricNode** se puede usar para comprobar que estos dos nodos están en el dominio de actualización *MYUD1*.</span><span class="sxs-lookup"><span data-stu-id="3847a-126">The **Get-ServiceFabricNode** command can be used to verify that these two nodes are in upgrade domain *MYUD1*.</span></span> <span data-ttu-id="3847a-127">La fase *UpgradePhase* indica *PostUpgradeSafetyCheck*, lo que significa que estas comprobaciones de seguridad se producen después de que todos los nodos del dominio de actualización hayan finalizado la actualización.</span><span class="sxs-lookup"><span data-stu-id="3847a-127">The *UpgradePhase* says *PostUpgradeSafetyCheck*, which means that these safety checks are occurring after all nodes in the upgrade domain have finished upgrading.</span></span> <span data-ttu-id="3847a-128">Toda esta información señala a un posible error con la nueva versión del código de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3847a-128">All this information points to a potential issue with the new version of the application code.</span></span> <span data-ttu-id="3847a-129">Los problemas más habituales son errores de servicio en la apertura o promoción a rutas de acceso de código principal.</span><span class="sxs-lookup"><span data-stu-id="3847a-129">The most common issues are service errors in the open or promotion to primary code paths.</span></span>

<span data-ttu-id="3847a-130">Una fase *UpgradePhase* de *PreUpgradeSafetyCheck* indica que se produjeron errores al preparar el dominio de actualización antes de realizar la actualización.</span><span class="sxs-lookup"><span data-stu-id="3847a-130">An *UpgradePhase* of *PreUpgradeSafetyCheck* means there were issues preparing the upgrade domain before it was performed.</span></span> <span data-ttu-id="3847a-131">Los problemas más habituales en este caso son errores de servicio en el cierre o disminución de nivel de las rutas de acceso de código principales.</span><span class="sxs-lookup"><span data-stu-id="3847a-131">The most common issues in this case are service errors in the close or demotion from primary code paths.</span></span>

<span data-ttu-id="3847a-132">El objeto **UpgradeState** actual es *RollingBackCompleted*, de modo que la actualización original debe haberse realizado con un objeto **FailureAction** de reversión, que revierte automáticamente la actualización tras el error.</span><span class="sxs-lookup"><span data-stu-id="3847a-132">The current **UpgradeState** is *RollingBackCompleted*, so the original upgrade must have been performed with a rollback **FailureAction**, which automatically rolled back the upgrade upon failure.</span></span> <span data-ttu-id="3847a-133">Si la actualización original se había realizado con un valor de **FailureAction**manual, la actualización estaría entonces en un estado suspendido para permitir una depuración en directo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3847a-133">If the original upgrade was performed with a manual **FailureAction**, then the upgrade would instead be in a suspended state to allow live debugging of the application.</span></span>

### <a name="investigate-health-check-failures"></a><span data-ttu-id="3847a-134">Investigar errores de comprobación de estado</span><span class="sxs-lookup"><span data-stu-id="3847a-134">Investigate health check failures</span></span>
<span data-ttu-id="3847a-135">Los errores de comprobación de estado pueden desencadenarse debido a varios problemas que se pueden producir después de que todos los nodos de un dominio de actualización terminen de actualizarse y pasen todas las comprobaciones de seguridad.</span><span class="sxs-lookup"><span data-stu-id="3847a-135">Health check failures can be triggered by various issues that can happen after all nodes in an upgrade domain finish upgrading and passing all safety checks.</span></span> <span data-ttu-id="3847a-136">La salida que sigue a este párrafo es habitual de un error de actualización debido a errores en las comprobaciones de estado.</span><span class="sxs-lookup"><span data-stu-id="3847a-136">The output following this paragraph is typical of an upgrade failure due to failed health checks.</span></span> <span data-ttu-id="3847a-137">El campo **UnhealthyEvaluations** captura una instantánea de todas las comprobaciones de estado con error en el momento de la actualización según la [directiva de mantenimiento](service-fabric-health-introduction.md)especificada.</span><span class="sxs-lookup"><span data-stu-id="3847a-137">The **UnhealthyEvaluations** field captures a snapshot of health checks that failed at the time of the upgrade according to the specified [health policy](service-fabric-health-introduction.md).</span></span>

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

<span data-ttu-id="3847a-138">Para investigar errores de comprobación de estado, es necesario conocer el modelo de mantenimiento de Service Fabric,</span><span class="sxs-lookup"><span data-stu-id="3847a-138">Investigating health check failures first requires an understanding of the Service Fabric health model.</span></span> <span data-ttu-id="3847a-139">pero incluso sin una comprensión profunda, podemos ver que los dos servicios son incorrectos: *fabric:/DemoApp/Svc3* y *fabric:/DemoApp/Svc2*, junto con los informes de mantenimiento de error ("InjectedFault" en este caso).</span><span class="sxs-lookup"><span data-stu-id="3847a-139">But even without such an in-depth understanding, we can see that two services are unhealthy: *fabric:/DemoApp/Svc3* and *fabric:/DemoApp/Svc2*, along with the error health reports ("InjectedFault" in this case).</span></span> <span data-ttu-id="3847a-140">En este ejemplo, dos de cada cuatro servicios son incorrectos, una relación que están por debajo del objetivo predeterminado de 0 % incorrecto (*MaxPercentUnhealthyServices*).</span><span class="sxs-lookup"><span data-stu-id="3847a-140">In this example, two out of four services are unhealthy, which is below the default target of 0% unhealthy (*MaxPercentUnhealthyServices*).</span></span>

<span data-ttu-id="3847a-141">La actualización se suspendió tras el error al especificar un valor de **FailureAction** manual cuando se inicia la actualización.</span><span class="sxs-lookup"><span data-stu-id="3847a-141">The upgrade was suspended upon failing by specifying a **FailureAction** of manual when starting the upgrade.</span></span> <span data-ttu-id="3847a-142">Este modo nos permite investigar el sistema activo en el estado de error antes de realizar ninguna acción.</span><span class="sxs-lookup"><span data-stu-id="3847a-142">This mode allows us to investigate the live system in the failed state before taking any further action.</span></span>

### <a name="recover-from-a-suspended-upgrade"></a><span data-ttu-id="3847a-143">Recuperarse de una actualización suspendida</span><span class="sxs-lookup"><span data-stu-id="3847a-143">Recover from a suspended upgrade</span></span>
<span data-ttu-id="3847a-144">Con un valor de **FailureAction**de reversión, no hace falta ninguna recuperación puesto que la actualización se revierte automáticamente tras el error.</span><span class="sxs-lookup"><span data-stu-id="3847a-144">With a rollback **FailureAction**, there is no recovery needed since the upgrade automatically rolls back upon failing.</span></span> <span data-ttu-id="3847a-145">Con una **FailureAction**manual, hay varias opciones de recuperación:</span><span class="sxs-lookup"><span data-stu-id="3847a-145">With a manual **FailureAction**, there are several recovery options:</span></span>

1.  <span data-ttu-id="3847a-146">Desencadenar una reversión</span><span class="sxs-lookup"><span data-stu-id="3847a-146">trigger a rollback</span></span>
2. <span data-ttu-id="3847a-147">Completar por el resto de la actualización manualmente</span><span class="sxs-lookup"><span data-stu-id="3847a-147">Proceed through the remainder of the upgrade manually</span></span>
3. <span data-ttu-id="3847a-148">Reanudar la actualización supervisada</span><span class="sxs-lookup"><span data-stu-id="3847a-148">Resume the monitored upgrade</span></span>

<span data-ttu-id="3847a-149">El comando **Start-ServiceFabricApplicationRollback** puede usarse en cualquier momento para empezar a revertir la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3847a-149">The **Start-ServiceFabricApplicationRollback** command can be used at any time to start rolling back the application.</span></span> <span data-ttu-id="3847a-150">Cuando el comando se devuelve correctamente, la solicitud de reversión se ha registrado en el sistema y comienza en breve.</span><span class="sxs-lookup"><span data-stu-id="3847a-150">Once the command returns successfully, the rollback request has been registered in the system and starts shortly thereafter.</span></span>

<span data-ttu-id="3847a-151">El comando **Resume-ServiceFabricApplicationUpgrade** se puede usar para continuar con el resto de la actualización manualmente, un dominio de actualización cada vez.</span><span class="sxs-lookup"><span data-stu-id="3847a-151">The **Resume-ServiceFabricApplicationUpgrade** command can be used to proceed through the remainder of the upgrade manually, one upgrade domain at a time.</span></span> <span data-ttu-id="3847a-152">En este modo, el sistema solo realiza comprobaciones de seguridad.</span><span class="sxs-lookup"><span data-stu-id="3847a-152">In this mode, only safety checks are performed by the system.</span></span> <span data-ttu-id="3847a-153">No se realizan más comprobaciones de estado.</span><span class="sxs-lookup"><span data-stu-id="3847a-153">No more health checks are performed.</span></span> <span data-ttu-id="3847a-154">Este comando solo se puede usar cuando *UpgradeState* muestra *RollingForwardPending*, lo que significa que el dominio de actualización actual ha terminado de actualizarse pero que el siguiente no se ha iniciado (está pendiente).</span><span class="sxs-lookup"><span data-stu-id="3847a-154">This command can only be used when the *UpgradeState* shows *RollingForwardPending*, which means that the current upgrade domain has finished upgrading but the next one has not started (pending).</span></span>

<span data-ttu-id="3847a-155">El comando **Update-ServiceFabricApplicationUpgrade** se puede usar para reanudar la actualización supervisada mientras se llevan a cabo las comprobaciones tanto de seguridad como de estado.</span><span class="sxs-lookup"><span data-stu-id="3847a-155">The **Update-ServiceFabricApplicationUpgrade** command can be used to resume the monitored upgrade with both safety and health checks being performed.</span></span>

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

<span data-ttu-id="3847a-156">La actualización continúa desde el dominio de actualización donde se suspendió la última vez y usa los mismos parámetros de actualización y las mismas directivas de mantenimiento que antes.</span><span class="sxs-lookup"><span data-stu-id="3847a-156">The upgrade continues from the upgrade domain where it was last suspended and use the same upgrade parameters and health policies as before.</span></span> <span data-ttu-id="3847a-157">En caso necesario, cualquiera de los parámetros de actualización y directivas de mantenimiento que se muestran en la salida anterior puede cambiarse en el mismo comando cuando la actualización se reanuda.</span><span class="sxs-lookup"><span data-stu-id="3847a-157">If needed, any of the upgrade parameters and health policies shown in the preceding output can be changed in the same command when the upgrade resumes.</span></span> <span data-ttu-id="3847a-158">En este ejemplo, la actualización se reanudó en modo supervisado, con los parámetros y las directivas de mantenimiento sin cambios.</span><span class="sxs-lookup"><span data-stu-id="3847a-158">In this example, the upgrade was resumed in Monitored mode, with the parameters and the health policies unchanged.</span></span>

## <a name="further-troubleshooting"></a><span data-ttu-id="3847a-159">Más información de solución de problemas</span><span class="sxs-lookup"><span data-stu-id="3847a-159">Further troubleshooting</span></span>
### <a name="service-fabric-is-not-following-the-specified-health-policies"></a><span data-ttu-id="3847a-160">Service Fabric no sigue las directivas de mantenimiento especificadas</span><span class="sxs-lookup"><span data-stu-id="3847a-160">Service Fabric is not following the specified health policies</span></span>
<span data-ttu-id="3847a-161">Causa posible 1:</span><span class="sxs-lookup"><span data-stu-id="3847a-161">Possible Cause 1:</span></span>

<span data-ttu-id="3847a-162">Service Fabric convierte todos los porcentajes en números reales de entidades (por ejemplo, réplicas, particiones y servicios) para la evaluación de estado y siempre se redondea a las entidades completas.</span><span class="sxs-lookup"><span data-stu-id="3847a-162">Service Fabric translates all percentages into actual numbers of entities (for example, replicas, partitions, and services) for health evaluation and always rounds up to whole entities.</span></span> <span data-ttu-id="3847a-163">Por ejemplo, si el valor máximo de *MaxPercentUnhealthyReplicasPerPartition* es 21 % y hay cinco réplicas, Service Fabric permite hasta dos réplicas con estado incorrecto (es decir, `Math.Ceiling (5*0.21)`).</span><span class="sxs-lookup"><span data-stu-id="3847a-163">For example, if the maximum *MaxPercentUnhealthyReplicasPerPartition* is 21% and there are five replicas, then Service Fabric allows up to two unhealthy replicas (that is,`Math.Ceiling (5*0.21)`).</span></span> <span data-ttu-id="3847a-164">Por lo tanto, las directivas de mantenimiento deben establecerse como corresponda.</span><span class="sxs-lookup"><span data-stu-id="3847a-164">Thus, health policies should be set accordingly.</span></span>

<span data-ttu-id="3847a-165">Causa posible 2:</span><span class="sxs-lookup"><span data-stu-id="3847a-165">Possible Cause 2:</span></span>

<span data-ttu-id="3847a-166">Las directivas de mantenimiento se especifican en términos de porcentajes de servicios totales e instancias de servicio no específicas.</span><span class="sxs-lookup"><span data-stu-id="3847a-166">Health policies are specified in terms of percentages of total services and not specific service instances.</span></span> <span data-ttu-id="3847a-167">Por ejemplo, antes de una actualización, supongamos que una aplicación tiene cuatro instancias de servicio A, B, C y D, donde el servicio D tiene un estado incorrecto, pero sin ningún impacto importante en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3847a-167">For example, before an upgrade, if an application has four service instances A, B, C, and D, where service D is unhealthy but with little impact to the application.</span></span> <span data-ttu-id="3847a-168">Queremos omitir el servicio D con estado incorrecto conocido durante la actualización y establecer el parámetro *MaxPercentUnhealthyServices* para que sea el 25 % suponiendo que solo A, B y C deban tener un estado correcto.</span><span class="sxs-lookup"><span data-stu-id="3847a-168">We want to ignore the known unhealthy service D during upgrade and set the parameter *MaxPercentUnhealthyServices* to be 25%, assuming only A, B, and C need to be healthy.</span></span>

<span data-ttu-id="3847a-169">Sin embargo, durante la actualización, D puede convertirse en correcto mientras C pasa a ser incorrecto.</span><span class="sxs-lookup"><span data-stu-id="3847a-169">However, during the upgrade, D may become healthy while C becomes unhealthy.</span></span> <span data-ttu-id="3847a-170">Aun así, la actualización se realizaría correctamente porque solo el 25 % de los servicios es incorrecto.</span><span class="sxs-lookup"><span data-stu-id="3847a-170">The upgrade would still succeed because only 25% of the services are unhealthy.</span></span> <span data-ttu-id="3847a-171">Sin embargo, como es C quién es incorrecto inesperadamente, en lugar de D, pueden producirse errores no anticipados. En esta situación, D se debe modelar como un tipo de servicio diferente de A, B y C. Como las directivas de mantenimiento se especifican por tipo de servicio, se pueden aplicar diferentes umbrales de porcentajes incorrectos a diferentes servicios.</span><span class="sxs-lookup"><span data-stu-id="3847a-171">However, it might result in unanticipated errors due to C being unexpectedly unhealthy instead of D. In this situation, D should be modeled as a different service type from A, B, and C. Since health policies are specified per service type, different unhealthy percentage thresholds can be applied to different services.</span></span> 

### <a name="i-did-not-specify-a-health-policy-for-application-upgrade-but-the-upgrade-still-fails-for-some-time-outs-that-i-never-specified"></a><span data-ttu-id="3847a-172">No he especificado una directiva de mantenimiento para la actualización de la aplicación, pero la actualización continúa generando errores para algunos tiempos de expiración que nunca he especificado</span><span class="sxs-lookup"><span data-stu-id="3847a-172">I did not specify a health policy for application upgrade, but the upgrade still fails for some time-outs that I never specified</span></span>
<span data-ttu-id="3847a-173">Si no se proporcionan directivas de mantenimiento para la solicitud de actualización, se obtienen del archivo *ApplicationManifest.xml* de la versión actual de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3847a-173">When health policies aren't provided to the upgrade request, they are taken from the *ApplicationManifest.xml* of the current application version.</span></span> <span data-ttu-id="3847a-174">Por ejemplo, si va a actualizar la aplicación x de la versión 1.0 a la versión 2.0, se usan las directivas de mantenimiento especificadas para la versión 1.0.</span><span class="sxs-lookup"><span data-stu-id="3847a-174">For example, if you're upgrading Application X from version 1.0 to version 2.0, application health policies specified for in version 1.0 are used.</span></span> <span data-ttu-id="3847a-175">Si se debe usar una directiva de mantenimiento diferente para la actualización, la directiva necesita especificarse como parte de la llamada API de actualización de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3847a-175">If a different health policy should be used for the upgrade, then the policy needs to be specified as part of the application upgrade API call.</span></span> <span data-ttu-id="3847a-176">Las directivas especificadas como parte de la llamada API solo se aplican durante la actualización.</span><span class="sxs-lookup"><span data-stu-id="3847a-176">The policies specified as part of the API call only apply during the upgrade.</span></span> <span data-ttu-id="3847a-177">Cuando se completa la actualización, se usan las directivas especificadas en el archivo *ApplicationManifest.xml* .</span><span class="sxs-lookup"><span data-stu-id="3847a-177">Once the upgrade is complete, the policies specified in the *ApplicationManifest.xml* are used.</span></span>

### <a name="incorrect-time-outs-are-specified"></a><span data-ttu-id="3847a-178">Se especifican los tiempos de expiración incorrectos</span><span class="sxs-lookup"><span data-stu-id="3847a-178">Incorrect time-outs are specified</span></span>
<span data-ttu-id="3847a-179">Es posible que se pregunte por lo que sucede cuando los tiempos de espera se establecen de forma incoherente.</span><span class="sxs-lookup"><span data-stu-id="3847a-179">You may have wondered about what happens when time-outs are set inconsistently.</span></span> <span data-ttu-id="3847a-180">Por ejemplo, si *UpgradeTimeout* es inferior a *UpgradeDomainTimeout*.</span><span class="sxs-lookup"><span data-stu-id="3847a-180">For example, you may have an *UpgradeTimeout* that's less than the *UpgradeDomainTimeout*.</span></span> <span data-ttu-id="3847a-181">La respuesta es que se devuelve un error.</span><span class="sxs-lookup"><span data-stu-id="3847a-181">The answer is that an error is returned.</span></span> <span data-ttu-id="3847a-182">Se devuelven errores si *UpgradeDomainTimeout* es inferior a la suma de *HealthCheckWaitDuration* y *HealthCheckRetryTimeout*, o si *UpgradeDomainTimeout* es inferior a la suma de *HealthCheckWaitDuration* y *HealthCheckStableDuration*.</span><span class="sxs-lookup"><span data-stu-id="3847a-182">Errors are returned if the *UpgradeDomainTimeout* is less than the sum of *HealthCheckWaitDuration* and *HealthCheckRetryTimeout*, or if *UpgradeDomainTimeout* is less than the sum of *HealthCheckWaitDuration* and *HealthCheckStableDuration*.</span></span>

### <a name="my-upgrades-are-taking-too-long"></a><span data-ttu-id="3847a-183">Mis actualizaciones están tardando mucho tiempo</span><span class="sxs-lookup"><span data-stu-id="3847a-183">My upgrades are taking too long</span></span>
<span data-ttu-id="3847a-184">El tiempo que tarde una actualización dependerá de las comprobaciones de estado y de los tiempos de espera especificados.</span><span class="sxs-lookup"><span data-stu-id="3847a-184">The time for an upgrade to complete depends on the health checks and time-outs specified.</span></span> <span data-ttu-id="3847a-185">Las comprobaciones de estado y los tiempos de espera dependen de lo que se tarde en copiar, implementar y estabilizar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3847a-185">Health checks and time-outs depend on how long it takes to copy, deploy, and stabilize the application.</span></span> <span data-ttu-id="3847a-186">Ser demasiado agresivo con los tiempos de expiración puede dar lugar a que se realicen más actualizaciones con errores; por ello, recomendamos empezar de manera conservadora con tiempos de expiración más prolongados.</span><span class="sxs-lookup"><span data-stu-id="3847a-186">Being too aggressive with time-outs might mean more failed upgrades, so we recommend starting conservatively with longer time-outs.</span></span>

<span data-ttu-id="3847a-187">A continuación ofrecemos un repaso rápido sobre la interacción de los tiempos de expiración con los tiempos de actualización:</span><span class="sxs-lookup"><span data-stu-id="3847a-187">Here's a quick refresher on how the time-outs interact with the upgrade times:</span></span>

<span data-ttu-id="3847a-188">Las actualizaciones de un dominio de actualización no se pueden completar con mayor rapidez que *HealthCheckWaitDuration* + *HealthCheckStableDuration*.</span><span class="sxs-lookup"><span data-stu-id="3847a-188">Upgrades for an upgrade domain cannot complete faster than *HealthCheckWaitDuration* + *HealthCheckStableDuration*.</span></span>

<span data-ttu-id="3847a-189">No se puede producir un error de actualización con mayor rapidez que *HealthCheckWaitDuration* + *HealthCheckRetryTimeout*.</span><span class="sxs-lookup"><span data-stu-id="3847a-189">Upgrade failure cannot occur faster than *HealthCheckWaitDuration* + *HealthCheckRetryTimeout*.</span></span>

<span data-ttu-id="3847a-190">El tiempo de actualización de un dominio de actualización está limitado por *UpgradeDomainTimeout*.</span><span class="sxs-lookup"><span data-stu-id="3847a-190">The upgrade time for an upgrade domain is limited by *UpgradeDomainTimeout*.</span></span>  <span data-ttu-id="3847a-191">Si *HealthCheckRetryTimeout* y *HealthCheckStableDuration* son distintos de cero y el estado de la aplicación continúa pasando de atrás para adelante, la actualización agotará el tiempo de espera en *UpgradeDomainTimeout*.</span><span class="sxs-lookup"><span data-stu-id="3847a-191">If *HealthCheckRetryTimeout* and *HealthCheckStableDuration* are both non-zero and the health of the application keeps switching back and forth, then the upgrade eventually times out on *UpgradeDomainTimeout*.</span></span> <span data-ttu-id="3847a-192">*UpgradeDomainTimeout* comienza la cuenta atrás cuando comienza la actualización para el dominio de actualización actual.</span><span class="sxs-lookup"><span data-stu-id="3847a-192">*UpgradeDomainTimeout* starts counting down once the upgrade for the current upgrade domain begins.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3847a-193">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3847a-193">Next steps</span></span>
<span data-ttu-id="3847a-194">[actualización de aplicaciones usando Visual Studio](service-fabric-application-upgrade-tutorial.md) ofrece información para actualizar una aplicación mediante Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3847a-194">[Upgrading your Application Using Visual Studio](service-fabric-application-upgrade-tutorial.md) walks you through an application upgrade using Visual Studio.</span></span>

<span data-ttu-id="3847a-195">[actualización de aplicaciones mediante PowerShell](service-fabric-application-upgrade-tutorial-powershell.md) se explica en detalle lo que tiene que hacer para actualizar una aplicación mediante PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3847a-195">[Upgrading your Application Using Powershell](service-fabric-application-upgrade-tutorial-powershell.md) walks you through an application upgrade using PowerShell.</span></span>

<span data-ttu-id="3847a-196">Puede controlar cómo se actualiza una aplicación usando [parámetros de actualización](service-fabric-application-upgrade-parameters.md).</span><span class="sxs-lookup"><span data-stu-id="3847a-196">Control how your application upgrades by using [Upgrade Parameters](service-fabric-application-upgrade-parameters.md).</span></span>

<span data-ttu-id="3847a-197">Consiga que sus actualizaciones de aplicaciones sean compatibles aprendiendo a usar la [serialización de datos](service-fabric-application-upgrade-data-serialization.md).</span><span class="sxs-lookup"><span data-stu-id="3847a-197">Make your application upgrades compatible by learning how to use [Data Serialization](service-fabric-application-upgrade-data-serialization.md).</span></span>

<span data-ttu-id="3847a-198">Aprenda a usar funcionalidades avanzadas para actualizar una aplicación. Para ello, consulte los [temas avanzados](service-fabric-application-upgrade-advanced.md).</span><span class="sxs-lookup"><span data-stu-id="3847a-198">Learn how to use advanced functionality while upgrading your application by referring to [Advanced Topics](service-fabric-application-upgrade-advanced.md).</span></span>
