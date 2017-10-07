---
title: "administración de aplicaciones de Azure Service Fabric aaaAutomate | Documentos de Microsoft"
description: "Implementación, actualización, prueba y eliminación de aplicaciones de Service Fabric con PowerShell."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: f03f4294-571d-4262-8a77-cc8b481b959d
ms.service: service-fabric
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/16/2017
ms.author: ryanwi
redirect_url: /azure/service-fabric/service-fabric-deploy-remove-applications
ms.openlocfilehash: a64a39dbee26be8ac15fee767a90fd06bfe4b896
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="automate-hello-application-lifecycle-using-powershell"></a>Automatizar Hola de ciclo de vida de aplicación mediante PowerShell
Muchos aspectos de hello [ciclo de vida de aplicación de Service Fabric](service-fabric-application-lifecycle.md) puede automatizarse.  Este artículo muestra cómo las tareas de toouse PowerShell tooautomate común de implementar, actualizar, quitar y probar aplicaciones de Azure Service Fabric.  También cuenta con API HTTP y administradas para la administración de aplicaciones. Consulte el [ciclo de vida de las aplicaciones](service-fabric-application-lifecycle.md) para más información.  

## <a name="prerequisites"></a>Requisitos previos
Antes de pasar toohello tareas en el artículo hello, no olvide:

* Familiarizarse con los conceptos de Service Fabric Hola se describe en [descripción general técnica de Service Fabric](service-fabric-technical-overview.md).
* [Instalar en tiempo de ejecución de hello, SDK y herramientas](service-fabric-get-started.md), que también instala hello **ServiceFabric** módulo de PowerShell.
* [Habilite la ejecución del script de PowerShell](service-fabric-get-started.md#enable-powershell-script-execution).
* Inicie un clúster local.  Inicie una nueva ventana de PowerShell como administrador y, a continuación, ejecute el script de instalación de clúster de Hola desde la carpeta del SDK de hello:`& "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\ClusterSetup\DevClusterSetup.ps1"`
* Antes de ejecutar los comandos de PowerShell en este artículo, primero conecte toohello clúster de Service Fabric local mediante el uso de [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps):`Connect-ServiceFabricCluster localhost:19000`
* Hola siguiente las tareas requiere una toodeploy de paquete de aplicación v1 y un paquete de aplicación v2 para la actualización. Descargar hello [ **WordCount** aplicación de ejemplo](http://aka.ms/servicefabricsamples) (que se encuentra en los ejemplos de introducción de hello). Compilar y empaquetar la aplicación hello en Visual Studio (haga doble clic en **WordCount** en el Explorador de soluciones y seleccione **paquete**). Copia el paquete de v1 de hello en `C:\ServiceFabricSamples\Services\WordCount\WordCount\pkg\Debug` demasiado`C:\Temp\WordCount`. Copia `C:\Temp\WordCount` demasiado`C:\Temp\WordCountV2`, crear paquete de la aplicación hello v2 para la actualización. Abra `C:\Temp\WordCountV2\ApplicationManifest.xml` en un editor de texto. Hola **ApplicationManifest** elemento, cambio hello **ApplicationTypeVersion** de atributo de "1.0.0" demasiado "2.0.0" número de versión de aplicación de tooupdate Hola. Guarde el archivo de ApplicationManifest.xml de hello cambiado.

## <a name="task-deploy-a-service-fabric-application"></a>Tarea: Implementar una aplicación de Service Fabric
Después de haber creado y empaqueta la aplicación hello (o descargar el paquete de aplicación Hola), puede implementar la aplicación hello en un clúster de Service Fabric local. Implementación implica cargar paquete de aplicación Hola, registrar el tipo de aplicación hello y crear la instancia de la aplicación hello. Siga las instrucciones de hello en este toodeploy sección un nuevo clúster tooa de aplicación.

### <a name="step-1-upload-hello-application-package"></a>Paso 1: Cargar el paquete de aplicación Hola
Cargando toohello de paquete de aplicación Hola almacén de imágenes lo coloca en un componente de ubicación accesible toointernal Service Fabric.  paquete de aplicación Hola contiene la configuración necesaria de manifiesto de aplicación, los manifiestos de servicio y código de hello y aplicación de hello de toocreate de paquetes de datos e instancias de servicio. Si desea tooverify Hola paquete de la aplicación localmente, utilice hello [ServiceFabricApplicationPackage prueba](/powershell/servicefabric/vlatest/test-servicefabricapplicationpackage) cmdlet.  Hola [ServiceFabricApplicationPackage copia](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) comando cargas Hola paquete. Por ejemplo:

```powershell
Copy-ServiceFabricApplicationPackage C:\Temp\WordCount\ -ImageStoreConnectionString file:C:\SfDevCluster\Data\ImageStoreShare -ApplicationPackagePathInImageStore WordCount
```

### <a name="step-2-register-hello-application-type"></a>Paso 2: Registrar el tipo de aplicación Hola
Paquete de aplicación del registro de hello hace tipo de aplicación hello y la versión que se declara en el manifiesto de aplicación de hello disponible para su uso. sistema Hola lee paquete Hola cargado en el paso 1 de hello, comprobar el paquete de hello (equivalente toorunning [ServiceFabricApplicationPackage prueba](/powershell/servicefabric/vlatest/test-servicefabricapplicationpackage) localmente), procesar el contenido del paquete hello y copie Hola procesa paquete tooan ubicación del sistema interno.  Ejecute hello [ServiceFabricApplicationType Register](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) cmdlet:

```powershell
Register-ServiceFabricApplicationType WordCount
```
toosee todos los tipos de aplicación Hola registrados en clúster de hello, ejecute hello [ServiceFabricApplicationType Get](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) cmdlet:

```powershell
Get-ServiceFabricApplicationType
```

### <a name="step-3-create-hello-application-instance"></a>Paso 3: Crear instancia de la aplicación hello
Se puede crear instancias de una aplicación mediante el uso de cualquier versión del tipo de aplicación que se ha registrado correctamente mediante el uso de hello [ServiceFabricApplication New](/powershell/module/servicefabric/new-servicefabricapplication?view=azureservicefabricps) comando. nombre de Hola de cada aplicación se declara en el tiempo de implementación y debe comenzar con hello **fabric:** esquema y ser únicos para cada instancia de la aplicación. Hello nombre de tipo de aplicación y la versión del tipo de aplicación se declaran en hello **ApplicationManifest.xml** archivo hello del paquete de aplicación. Si los servicios predeterminados se definieron en el manifiesto de aplicación Hola del tipo de aplicación de destino de hello, las que se crean en este momento.

```powershell
New-ServiceFabricApplication fabric:/WordCount WordCount 1.0.0
```

Hola [Get ServiceFabricApplication](/powershell/servicefabric/vlatest/get-servicefabricapplication) comando enumera todas las instancias de aplicación que se crearon correctamente, junto con su estado general. Hola [Get ServiceFabricService](/powershell/module/servicefabric/get-servicefabricservice?view=azureservicefabricps) comando enumera todas las instancias de servicio de Hola que se crearon correctamente dentro de una instancia de aplicación determinada. Se enumeran los servicios predeterminados (en caso de haberlos).

```powershell
Get-ServiceFabricApplication

Get-ServiceFabricApplication | Get-ServiceFabricService
```

## <a name="task-upgrade-a-service-fabric-application"></a>Tarea: Actualizar una aplicación de Service Fabric
Puede actualizar una aplicación de Service Fabric ya implementada con un paquete de aplicación actualizado. Esta tarea actualiza la aplicación WordCount hello que se implementó en "tarea: implementar una aplicación de Service Fabric." Lea el [Tutorial de actualización de aplicación de Service Fabric](service-fabric-application-upgrade.md) para obtener más información.

se actualizó tookeep cosas simple para este ejemplo, el número de versión de aplicación a solo Hola Hola WordCountV2 paquete de aplicación creado en los requisitos previos de Hola. Un escenario más realista implicaría actualizar los archivos de código, la configuración o datos de servicio y, a continuación, volver a generar y empaquetar la aplicación hello con números de versión actualizada.  

### <a name="step-1-upload-hello-updated-application-package"></a>Paso 1: Cargar el paquete de aplicación actualizada Hola
Hola WordCount v1 aplicación es listo toobe actualizado. Si abre una ventana de PowerShell como administrador y escriba [ **Get ServiceFabricApplication**](/powershell/module/servicefabric/get-servicefabricapplication?view=azureservicefabricps), verá que se implementa esa versión 1.0.0 de hello tipo de aplicación WordCount.  

Hola copia había actualizado almacén de la imagen de Service Fabric de aplicación paquetes toohello (donde se almacenan los paquetes de aplicación Hola por Service Fabric). Hola parámetro **ApplicationPackagePathInImageStore** informa a Service Fabric dónde puede encontrar paquete de aplicación Hola. Hola el siguiente comando copia Hola paquete de aplicación demasiado**WordCountV2** en almacén de imágenes de hello:  

```powershell
Copy-ServiceFabricApplicationPackage C:\Temp\WordCountV2\ -ImageStoreConnectionString file:C:\SfDevCluster\Data\ImageStoreShare -ApplicationPackagePathInImageStore WordCountV2

```
### <a name="step-2-register-hello-updated-application-type"></a>Paso 2: Registrar Hola actualiza el tipo de aplicación
paso siguiente Hello es tooregister Hola nueva versión de aplicación Hola con Service Fabric, lo que puede realizarse mediante hello [ServiceFabricApplicationType Register](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) cmdlet:

```powershell
Register-ServiceFabricApplicationType WordCountV2
```

### <a name="step-3-start-hello-upgrade"></a>Paso 3: Iniciar la actualización de Hola
Varios parámetros de actualización, los tiempos de espera y criterios de estado pueden ser tooapplication aplicado actualizaciones. Lea hello [parámetros de actualización de la aplicación](service-fabric-application-upgrade-parameters.md) y [proceso de actualización](service-fabric-application-upgrade.md) documentos toolearn más. Todos los servicios y las instancias deben ser *correcto* después de la actualización de Hola.  Conjunto hello **HealthCheckStableDuration** too60 segundos (de modo que los servicios de hello están en buenas condiciones de al menos 20 segundos antes de que realiza la actualización de hello toohello siguiente dominio de actualización).  También conjunto hello **UpgradeDomainTimeout** too1200 segundos y Hola **UpgradeTimeout** too3000 segundos. Por último, establezca hello **UpgradeFailureAction** demasiado**reversión**, que las solicitudes que Service Fabric revierte Hola versión anterior de la aplicación toohello si se producen errores durante la actualización.

Ahora puede iniciar actualización de la aplicación hello mediante hello [ServiceFabricApplicationUpgrade inicio](/powershell/module/servicefabric/start-servicefabricapplicationupgrade?view=azureservicefabricps) cmdlet:

```powershell
Start-ServiceFabricApplicationUpgrade -ApplicationName fabric:/WordCount -ApplicationTypeVersion 2.0.0 -HealthCheckStableDurationSec 60 -UpgradeDomainTimeoutSec 1200 -UpgradeTimeout 3000  -FailureAction Rollback -Monitored
```

Tenga en cuenta ese nombre de la aplicación hello es Hola igual como Hola implementado previamente el nombre de la aplicación v1.0.0 (fabric: / WordCount). Service Fabric usa este tooidentify nombre obtener se actualiza la aplicación. Si establece hello toobe de los tiempos de espera demasiado corto, podría encontrar un mensaje de error de tiempo de espera que los Estados Hola problema. Consulte demasiado[solucionar problemas de actualizaciones de la aplicación](service-fabric-application-upgrade-troubleshooting.md), o aumentar los tiempos de espera de Hola.

### <a name="step-4-check-upgrade-progress"></a>Paso 4: Comprobación del progreso de la actualización
Puede supervisar el progreso de actualización de la aplicación mediante [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md), o mediante el uso de hello [ServiceFabricApplicationUpgrade Get](/powershell/module/servicefabric/get-servicefabricapplicationupgrade?view=azureservicefabricps) cmdlet:

```powershell
Get-ServiceFabricApplicationUpgrade fabric:/WordCount
```

En unos minutos, Hola [ServiceFabricApplicationUpgrade Get](/powershell/module/servicefabric/get-servicefabricapplicationupgrade?view=azureservicefabricps) muestra que se actualizaron todos los dominios de actualización (completado).

## <a name="task-test-a-service-fabric-application"></a>Tarea: Probar una aplicación de Service Fabric
Servicios de alta calidad toowrite, los desarrolladores necesitan toobe tooinduce capaz de infraestructura no confiable errores tootest Hola estabilidad de sus servicios. Service Fabric proporciona a los programadores de acciones de error de hello capacidad tooinduce y probar servicios en presencia de Hola de errores mediante el uso de Hola escenarios de prueba de conmutación por error y caos.  Lea [Introducción toohello servicio de análisis de errores](service-fabric-testability-overview.md) para obtener información adicional.

### <a name="step-1-run-hello-chaos-test-scenario"></a>Paso 1: Ejecutar el escenario de prueba de caos Hola
escenario de prueba de Hello chaos genera errores en el clúster de Service Fabric todo Hola. escenario de Hello comprime errores generalmente vistos durante meses o años tooa pocas horas. combinación de Hola de errores intercalados con una tasa alta de error busca casos más complejos que en caso contrario, se perderán. Hello en el ejemplo siguiente se ejecuta el escenario de prueba de hello chaos durante 60 minutos.

```powershell
$timeToRun = 60
$maxStabilizationTimeSecs = 180
$concurrentFaults = 3
$waitTimeBetweenIterationsSec = 60

Invoke-ServiceFabricChaosTestScenario -TimeToRunMinute $timeToRun -MaxClusterStabilizationTimeoutSec $maxStabilizationTimeSecs -MaxConcurrentFaults $concurrentFaults -EnableMoveReplicaFaults -WaitTimeBetweenIterationsSec $waitTimeBetweenIterationsSec
```

### <a name="step-2-run-hello-failover-test-scenario"></a>Paso 2: Ejecutar el escenario de prueba de conmutación por error de Hola
Hola conmutación por error de prueba de destinos de escenario una partición de servicio específico en lugar de clúster completo de Hola y deja otros servicios afectadas. escenario de Hello procesa una iteración a través de una secuencia de simulada errores de validación del servicio mientras se ejecuta la lógica de negocios. Un error en la validación de servicio indica un problema que necesita más investigación. prueba de conmutación por error de Hello induce a solo error en un momento, según el escenario de prueba de caos toohello opuestos, que puede inducir a errores varios. Hello en el ejemplo siguiente se ejecuta pruebas de conmutación por error de Hola durante 60 minutos en el tejido de hello: / WordCount/servicio WordCountService.

```powershell
$timeToRun = 60
$maxStabilizationTimeSecs = 180
$waitTimeBetweenFaultsSec = 10
$serviceName = "fabric:/WordCount/WordCountService"

Invoke-ServiceFabricFailoverTestScenario -TimeToRunMinute $timeToRun -MaxServiceStabilizationTimeoutSec $maxStabilizationTimeSecs -WaitTimeBetweenFaultsSec $waitTimeBetweenFaultsSec -ServiceName $serviceName -PartitionKindUniformInt64 -PartitionKey 1
```

## <a name="task-remove-a-service-fabric-application"></a>Tarea: Quitar una aplicación de Service Fabric
Puede eliminar una instancia de una aplicación implementada, quitar el tipo de aplicación Hola aprovisionado de clúster de Hola y quitar el paquete de aplicación Hola de hello ImageStore.

### <a name="step-1-remove-an-application-instance"></a>Paso 1: quite una instancia de aplicación
Cuando ya no se necesita una instancia de la aplicación, permanentemente puede quitar mediante hello [Remove-ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) cmdlet. Esto quita automáticamente todos los servicios pertenecientes toohello aplicación, eliminar permanentemente todos los Estados de servicio. No se puede deshacer esta operación y no se puede recuperar el estado de la aplicación.

```powershell
Remove-ServiceFabricApplication fabric:/WordCount
```

### <a name="step-2-unregister-hello-application-type"></a>Paso 2: Anular el registro del tipo de aplicación Hola
Cuando ya no necesita una versión concreta de un tipo de aplicación, anule el registro mediante el uso de hello [Unregister-ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) cmdlet. Al anular el registro tipos sin usar versiones espacio de almacenamiento utilizado por el paquete de aplicación hello en el almacén de imágenes de Hola. No se puede anular el registro de un tipo de aplicación ya que no hay ninguna aplicación con instancias con él o hay actualizaciones de aplicaciones pendientes que hacen referencia a él.

```powershell
Unregister-ServiceFabricApplicationType WordCount 1.0.0
```

### <a name="step-3-remove-hello-application-package"></a>Paso 3: Quitar el paquete de aplicación Hola
Después de que no está registrado el tipo de aplicación Hola, se puede quitar paquete de aplicación Hola Hola almacén de imágenes mediante hello [Remove-ServiceFabricApplicationPackage](/powershell/module/servicefabric/remove-servicefabricapplicationpackage?view=azureservicefabricps) cmdlet.

```powershell
Remove-ServiceFabricApplicationPackage -ImageStoreConnectionString file:C:\SfDevCluster\Data\ImageStoreShare -ApplicationPackagePathInImageStore WordCount
```

## <a name="next-steps"></a>Pasos siguientes
[Ciclo de vida de la aplicación de Service Fabric](service-fabric-application-lifecycle.md)

[Implementar una aplicación](service-fabric-deploy-remove-applications.md)

[Actualización de aplicaciones](service-fabric-application-upgrade.md)

[Cmdlets de Azure Service Fabric](/powershell/azure/overview?view=azureservicefabricps)

