---
title: "actualización de App Fabric aaaService mediante PowerShell | Documentos de Microsoft"
description: "Este artículo le guía a través de la experiencia de Hola de implementar una aplicación de Service Fabric, cambiar el código de hello y efectuando una actualización mediante PowerShell."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: 9bc75748-96b0-49ca-8d8a-41fe08398f25
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: f31212264de45c3b257a0efafb75c10c279b989f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-application-upgrade-using-powershell"></a>Actualización de aplicaciones de Service Fabric con PowerShell
> [!div class="op_single_selector"]
> * [PowerShell](service-fabric-application-upgrade-tutorial-powershell.md)
> * [Visual Studio](service-fabric-application-upgrade-tutorial.md)
> 
> 

<br/>

Hola se usa con más frecuencia y enfoque de actualización recomendado es actualización gradual de hello supervisado.  Azure Service Fabric supervisa el estado de la Hola de aplicación Hola se actualiza por la que se basándose en un conjunto de directivas de mantenimiento. Una vez que se actualiza un dominio de actualización (UD), Service Fabric evalúa el estado de la aplicación hello y continúa toohello siguiente dominio de actualización o se produce un error de actualización de hello según las directivas de mantenimiento de Hola.

Se puede realizar una actualización de las aplicaciones supervisadas con Hola administrados o las API nativas, PowerShell o REST. Para obtener instrucciones sobre cómo realizar una actualización con Visual Studio, consulte [Actualización de la aplicación con Visual Studio](service-fabric-application-upgrade-tutorial.md).

Con actualizaciones graduales de Service Fabric supervisados, Administrador de la aplicación hello puede configurar la directiva de evaluación de mantenimiento de Hola que Service Fabric utiliza toodetermine si la aplicación hello es correcto. Además, Administrador de hello puede configurar hello toobe de acción realizada cuando se produce un error en la evaluación de mantenimiento de hello (por ejemplo, realizando una reversión automática). Esta sección le guía a través de una actualización para uno de los ejemplos de SDK de Hola que usa PowerShell supervisada. Hello siguiente vídeo de Microsoft Virtual Academy también le guía a través de una actualización de la aplicación:<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=OrHJH66yC_6406218965">
<img src="./media/service-fabric-application-upgrade-tutorial-powershell/AppLifecycleVid.png" WIDTH="360" HEIGHT="244">
</a></center>

## <a name="step-1-build-and-deploy-hello-visual-objects-sample"></a>Paso 1: Compilar e implementar el ejemplo de Hola a objetos visuales
Compilar y publicar la aplicación hello con el botón secundario en el proyecto de aplicación de hello, **VisualObjectsApplication,** y seleccionando hello **publicar** comando.  Para más información, consulte el [tutorial sobre la actualización de aplicaciones de Service Fabric](service-fabric-application-upgrade-tutorial.md).  Como alternativa, puede usar PowerShell toodeploy la aplicación.

> [!NOTE]
> Antes de cualquiera de los comandos de Service Fabric Hola puede usarse en PowerShell, primero debe tooconnect toohello clúster mediante el uso de hello `Connect-ServiceFabricCluster` cmdlet. De igual forma, se supone que Hola que clúster ya se ha configurado en el equipo local. Consulte el artículo de hello en [configuración del entorno de desarrollo de Service Fabric](service-fabric-get-started.md).
> 
> 

Después de compilar el proyecto de hello en Visual Studio, puede usar comandos de PowerShell de hello [ServiceFabricApplicationPackage copia](/powershell/servicefabric/vlatest/copy-servicefabricapplicationpackage) toocopy Hola aplicación paquete toohello ImageStore. Si desea tooverify Hola paquete de la aplicación localmente, utilice hello [ServiceFabricApplicationPackage prueba](/powershell/servicefabric/vlatest/test-servicefabricapplicationpackage) cmdlet. Hola siguiente paso es tooregister Hola aplicación toohello Service Fabric en tiempo de ejecución mediante hello [ServiceFabricApplicationPackage Register](/powershell/servicefabric/vlatest/register-servicefabricapplicationtype) cmdlet. Hello paso final es una instancia de la aplicación hello toostart mediante hello [ServiceFabricApplication New](/powershell/module/servicefabric/new-servicefabricapplication?view=azureservicefabricps) cmdlet.  Estos tres pasos son análogos toousing hello **implementar** elemento de menú en Visual Studio.

Ahora, puede usar [Service Fabric Explorer tooview Hola clúster y Hola una aplicación](service-fabric-visualizing-your-cluster.md). aplicación Hello tiene un servicio web que se puede navegar un tooin Internet Explorer escribiendo [http://localhost: 8081/visualobjects](http://localhost:8081/visualobjects) en la barra de direcciones de Hola.  Debería ver algunos objetos visuales flotantes desplazarse por la pantalla de bienvenida.  Además, puede usar [Get ServiceFabricApplication](/powershell/module/servicefabric/get-servicefabricapplication?view=azureservicefabricps) estado de la aplicación hello toocheck.

## <a name="step-2-update-hello-visual-objects-sample"></a>Paso 2: Actualizar la muestra de Hola a objetos visuales
Observará que con la versión de Hola que se implementó en el paso 1, los objetos visuales de hello no giran. Vamos a actualizar esta tooone de aplicación donde los objetos visuales de hello girar.

Seleccione proyecto de VisualObjects.ActorService Hola dentro de hello VisualObjects solución y abrir el archivo de hello StatefulVisualObjectActor.cs. Dentro de ese archivo, vaya toohello método `MoveObject`, comente `this.State.Move()`y quitar el comentario `this.State.Move(true)`. Este cambio gira objetos Hola después de la actualización de servicio de Hola.

También es necesario hello tooupdate *ServiceManifest.xml* archivo (bajo PackageRoot) del proyecto de hello **VisualObjects.ActorService**. Hola de actualización *CodePackage* Hola too2.0 de versión de servicio y Hola líneas correspondientes en hello *ServiceManifest.xml* archivo.
Puede usar Visual Studio hello *editar archivos de manifiesto* opción una vez que haga doble clic en cambios de archivo de manifiesto de hello solución toomake Hola.

Después de realizar cambios de hello, manifiesto Hola debería ser similar siguiente de hello (las partes resaltadas Mostrar cambios de hello):

```xml
<ServiceManifestName="VisualObjects.ActorService" Version="2.0" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">

<CodePackageName="Code" Version="2.0">
```

Hola ahora *ApplicationManifest.xml* archivo (se encuentra en hello **VisualObjects** proyecto bajo hello **VisualObjects** solución) está actualizada tooversion 2.0 de hello  **VisualObjects.ActorService** proyecto. Además, la versión de la aplicación hello es too2.0.0.0 actualizada de 1.0.0.0. Hola *ApplicationManifest.xml* debe Hola tenga el aspecto siguiente fragmento de código:

```xml
<ApplicationManifestxmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="VisualObjects" ApplicationTypeVersion="2.0.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">

 <ServiceManifestRefServiceManifestName="VisualObjects.ActorService" ServiceManifestVersion="2.0" />
```


Ahora, compile el proyecto de hello seleccionando Hola simplemente **ActorService** proyecto y, a continuación, con el botón secundario y seleccionando hello **generar** opción en Visual Studio. Si selecciona **volver a generar todo**, debe actualizar versiones de Hola para todos los proyectos, ya que el código de hello hubiera cambiado. A continuación, vamos a Hola paquete actualiza la aplicación con el botón secundario en ***VisualObjectsApplication***, seleccionar Hola menú de tejido de servicio y luego **paquete**. Esta acción crea un paquete de aplicación que se puede implementar.  La aplicación actualizada está listo toobe implementado.

## <a name="step-3--decide-on-health-policies-and-upgrade-parameters"></a>Paso 3: Decidir sobre las directivas de mantenimiento y los parámetros de actualización
Familiarícese con hello [parámetros de actualización de la aplicación](service-fabric-application-upgrade-parameters.md) hello y [proceso de actualización](service-fabric-application-upgrade.md) tooget un buen conocimiento de saludo diversos actualizan parámetros, los tiempos de espera y aplicar el criterio de mantenimiento . En este tutorial, criterio de evaluación de mantenimiento de servicio de Hola se establezca el valor predeterminado de toohello (y recomendado) valores, lo que significa que todos los servicios y las instancias deben ser *correcto* después de la actualización de Hola.  

Sin embargo, vamos a aumentar hello *HealthCheckStableDuration* too60 segundos (de modo que los servicios de hello están en buenas condiciones para al menos 20 segundos antes de que realiza la actualización de hello toohello siguiente dominio de actualización).  Configuremos también hello *UpgradeDomainTimeout* toobe hello y 1.200 segundos *UpgradeTimeout* toobe 3.000 segundos.

Por último, también Configuremos hello *UpgradeFailureAction* toorollback. Esta opción requiere la versión anterior de Service Fabric tooroll Hola atrás aplicación toohello si encuentra algún problema durante la actualización de Hola. Por lo tanto, al iniciar la actualización de hello (en el paso 4), hello son especificar los parámetros siguientes:

FailureAction = Rollback

HealthCheckStableDurationSec = 60

UpgradeDomainTimeoutSec = 1200

UpgradeTimeout = 3000

## <a name="step-4-prepare-application-for-upgrade"></a>Paso 4: Preparar la aplicación para la actualización
Ahora se compila la aplicación hello y actualiza toobe listo. Si abre una ventana de PowerShell como administrador y escribe [Get-ServiceFabricApplication](/powershell/module/servicefabric/get-servicefabricapplication?view=azureservicefabricps), debe indicarle que la aplicación que se ha implementado es el tipo de aplicación 1.0.0.0 de **VisualObjects**.  

paquete de aplicación Hello está almacenada una bajo siguiente de hello ruta de acceso relativa donde descomprimido Hola SDK del servicio de Fabric - *Samples\Services\Stateful\VisualObjects\VisualObjects\obj\x64\Debug*. Debería encontrar una carpeta de "Paquete" en ese directorio, donde se almacena el paquete de aplicación Hola. Compruebe hello tooensure de marcas de tiempo que se trata de compilación más reciente de hello (puede que tenga toomodify hello las rutas de acceso correctamente también).

Ahora vamos a Hola copia actualiza toohello de paquete de aplicación ImageStore de tejido de servicio (donde se almacenan los paquetes de aplicación Hola por Service Fabric). Hola parámetro *ApplicationPackagePathInImageStore* informa a Service Fabric dónde puede encontrar paquete de aplicación Hola. Hemos reunido aplicación hello actualizado "VisualObjects\_V2" con hello siguiente comando (que tenga las rutas de acceso de toomodify nuevo correctamente).

```powershell
Copy-ServiceFabricApplicationPackage  -ApplicationPackagePath .\Samples\Services\Stateful\VisualObjects\VisualObjects\obj\x64\Debug\Package
-ImageStoreConnectionString fabric:ImageStore   -ApplicationPackagePathInImageStore "VisualObjects\_V2"
```

paso siguiente Hello es tooregister esta aplicación con el tejido de servicio, que pueden realizarse usando hello [ServiceFabricApplicationType Register](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) comando:

```powershell
Register-ServiceFabricApplicationType -ApplicationPathInImageStore "VisualObjects\_V2"
```

Si el hello comando anterior no funciona, es probable que necesite una recompilación de todos los servicios. Como se mencionó en el paso 2, puede que tenga tooupdate la versión del servicio Web.

## <a name="step-5-start-hello-application-upgrade"></a>Paso 5: Iniciar la actualización de la aplicación hello
Ahora, estamos todas las aplicaciones de hello toostart de conjunto de actualización mediante el uso de hello [ServiceFabricApplicationUpgrade inicio](/powershell/module/servicefabric/start-servicefabricapplicationupgrade?view=azureservicefabricps) comando:

```powershell
Start-ServiceFabricApplicationUpgrade -ApplicationName fabric:/VisualObjects -ApplicationTypeVersion 2.0.0.0 -HealthCheckStableDurationSec 60 -UpgradeDomainTimeoutSec 1200 -UpgradeTimeout 3000   -FailureAction Rollback -Monitored
```


Hello nombre de la aplicación es Hola mismo tal y como se describió en hello *ApplicationManifest.xml* archivo. Service Fabric usa este tooidentify nombre obtener se actualiza la aplicación. Si establece hello toobe de los tiempos de espera demasiado corto, puede encontrar un mensaje de error que Estados Hola problema. Consulte la sección Solución de problemas de toohello o aumentar los tiempos de espera de Hola.

Ahora, como hello continúa de actualización de aplicación, puede supervisar mediante el Explorador de Service Fabric, o mediante el uso de hello [Get ServiceFabricApplicationUpgrade](/powershell/module/servicefabric/get-servicefabricapplicationupgrade?view=azureservicefabricps) comando de PowerShell: 

```powershell
Get-ServiceFabricApplicationUpgrade fabric:/VisualObjects
```

En unos minutos, estado de Hola que obtuvo mediante el uso de hello anterior comando de PowerShell, debe indicar que todos los dominios de actualización se han actualizado (completado). Y debería comprobar que se han iniciado de rotación de objetos visuales de hello en la ventana del explorador.

Puede intentar actualizar desde versión 2 tooversion 3, o desde la versión 2 tooversion 1 como un ejercicio. Mover desde la versión 2 tooversion 1 también se considera una actualización. Practicar con los tiempos de espera y toomake de directivas de mantenimiento usted mismo familiarizados con ellos. Cuando se implementan tooan clúster de Azure, Hola parámetros necesidad toobe establecidos correctamente. Es tiempos de espera de hello tooset buena manera conservadora.

## <a name="next-steps"></a>Pasos siguientes
[Actualización de la aplicación con Visual Studio](service-fabric-application-upgrade-tutorial.md) ofrece información para actualizar una aplicación mediante Visual Studio.

Puede controlar cómo se actualiza una aplicación usando [parámetros de actualización](service-fabric-application-upgrade-parameters.md).

Hacer que las actualizaciones de la aplicación sea compatible por el aprendizaje cómo toouse [serialización de datos](service-fabric-application-upgrade-data-serialization.md).

Obtenga información acerca de cómo toouse funcionalidad avanzada al actualizar la aplicación, se hace referencia demasiado[temas avanzados](service-fabric-application-upgrade-advanced.md).

Solucione problemas habituales en las actualizaciones de aplicaciones, se hace referencia a pasos toohello en [solución de problemas de las actualizaciones de aplicaciones](service-fabric-application-upgrade-troubleshooting.md).

