---
title: "una aplicación de Azure Service Fabric aaaPackage | Documentos de Microsoft"
description: "¿Cómo toopackage una aplicación de Service Fabric antes de implementar el clúster de tooa."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: mani-ramaswamy
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: ryanwi
ms.openlocfilehash: b3918e1e25e532acdc9440855213e1fa364ea000
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="package-an-application"></a>Empaquetar una aplicación
Este artículo se describe cómo toopackage una aplicación de Service Fabric y prepararlo para la implementación.

## <a name="package-layout"></a>Diseño del paquete
manifiesto de aplicación Hola, uno o varios de los manifiestos de servicio y otro paquete necesario de archivos deben estar organizados en un diseño específico para la implementación en un clúster de Service Fabric. manifiestos de ejemplo de Hola en este artículo necesitaría toobe organizado en hello siguiendo la estructura de directorios:

```
PS D:\temp> tree /f .\MyApplicationType

D:\TEMP\MYAPPLICATIONTYPE
│   ApplicationManifest.xml
│
└───MyServiceManifest
    │   ServiceManifest.xml
    │
    ├───MyCode
    │       MyServiceHost.exe
    │
    ├───MyConfig
    │       Settings.xml
    │
    └───MyData
            init.dat
```

carpetas de Hola se llaman hello toomatch **nombre** atributos de cada elemento correspondiente. Por ejemplo, si hello manifiesto del servicio contiene dos paquetes de código con nombres de hello **MyCodeA** y **MyCodeB**, a continuación, dos carpetas con hello suele contener los mismos nombres Hola archivos binarios necesarios para cada código paquete.

## <a name="use-setupentrypoint"></a>Usar SetupEntrypoint
Escenarios típicos de uso **SetupEntryPoint** se da cuando necesita toorun un ejecutable antes de iniciar servicio de Hola o necesita tooperform una operación con privilegios elevados. Por ejemplo:

* Configurar e inicializar variables de entorno que Hola necesidades ejecutable del servicio. No es ejecutables tooonly limitado escritos a través de los modelos de programación de Service Fabric Hola. Por ejemplo, npm.exe necesita algunas variables de entorno configuradas para implementar una aplicación node.js.
* Configuración del control de acceso mediante la instalación de certificados de seguridad.

Para obtener más información acerca de cómo hello tooconfigure **SetupEntryPoint**, consulte [configurar Directiva de Hola para un punto de entrada del programa de instalación de servicio](service-fabric-application-runas-security.md)

<a id="Package-App"></a>
## <a name="configure"></a>Configuración
### <a name="build-a-package-by-using-visual-studio"></a>Crear un paquete mediante Visual Studio
Si usa Visual Studio 2015 toocreate su aplicación, puede usar Hola paquete comando tooautomatically crear un paquete que coincida con el diseño de Hola se ha descrito anteriormente.

toocreate un paquete, haga clic en proyecto de aplicación de hello en el Explorador de soluciones y elija el comando de paquete de hello, tal y como se muestra a continuación:

![Empaquetado de una aplicación con Visual Studio][vs-package-command]

Una vez completado empaquetado, puede encontrar Hola ubicación del paquete de Hola Hola **salida** ventana. paso de empaquetado de Hola se produce automáticamente al implementar o depurar la aplicación en Visual Studio.

### <a name="build-a-package-by-command-line"></a>Creación de un paquete mediante la línea de comandos
También es posible tooprogrammatically paquete una aplicación mediante `msbuild.exe`. Bajo el paraguas de hello, Visual Studio se está ejecutando, por lo que la salida de hello es la misma.

```shell
D:\Temp> msbuild HelloWorld.sfproj /t:Package
```

## <a name="test-hello-package"></a>Paquete de Hola de prueba
Puede comprobar la estructura del paquete Hola localmente a través de PowerShell mediante el uso de hello [ServiceFabricApplicationPackage prueba](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) comando.
Este comando comprueba si existen problemas de análisis de manifiestos y verifica todas las referencias. Este comando sólo comprueba la corrección estructural de Hola de hello directorios y archivos de paquete de Hola.
Información no comprueba cualquier elemento de contenido de los paquetes de código o datos de hello más allá de la comprobación de que todos los archivos necesarios están presentes.

```
PS D:\temp> Test-ServiceFabricApplicationPackage .\MyApplicationType
False
Test-ServiceFabricApplicationPackage : hello EntryPoint MySetup.bat is not found.
FileName: C:\Users\servicefabric\AppData\Local\Temp\TestApplicationPackage_7195781181\nrri205a.e2h\MyApplicationType\MyServiceManifest\ServiceManifest.xml
```

Este error muestra ese hello *MySetup.bat* archivo hace referencia en el manifiesto del servicio de hello **SetupEntryPoint** no está en el paquete de código de hello. Después de agrega el archivo que falta hello, pasa la comprobación de aplicación Hola:

```
PS D:\temp> tree /f .\MyApplicationType

D:\TEMP\MYAPPLICATIONTYPE
│   ApplicationManifest.xml
│
└───MyServiceManifest
    │   ServiceManifest.xml
    │
    ├───MyCode
    │       MyServiceHost.exe
    │       MySetup.bat
    │
    ├───MyConfig
    │       Settings.xml
    │
    └───MyData
            init.dat

PS D:\temp> Test-ServiceFabricApplicationPackage .\MyApplicationType
True
PS D:\temp>
```

Si la aplicación tiene [parámetros de aplicación](service-fabric-manage-multiple-environment-app-configuration.md) definidos, puede pasarlos en [Test-ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) para realizar una validación adecuada.

Si conoce el clúster de Hola donde se implementará la aplicación hello, se recomienda pasar en hello `ImageStoreConnectionString` parámetro. En este caso, también se valida el paquete de hello con versiones anteriores de la aplicación hello que se están ejecutando en el clúster de Hola. Por ejemplo, validación de hello puede detectar si un paquete con hello misma versión, pero distinto contenido ya se había implementado.  

Una vez que la aplicación hello se empaqueta correctamente y pasa la validación, evaluar basándose en tamaño de Hola y número de Hola de archivos si es necesaria la compresión.

## <a name="compress-a-package"></a>Compresión de un paquete
Cuando un paquete es grande o tiene muchos archivos, puede comprimirlo para acelerar la implementación. La compresión reduce el número de Hola de archivos y el tamaño de paquete de Hola.
Para un paquete de aplicación comprimidos, [paquete de aplicación de carga hello](service-fabric-deploy-remove-applications.md#upload-the-application-package) puede tardar ya comparados toouploading Hola paquete sin comprimir (especialmente si el tiempo de compresión se tienen en cuenta), pero [registrar](service-fabric-deploy-remove-applications.md#register-the-application-package) y [tipo anulación del registro de la aplicación hello](service-fabric-deploy-remove-applications.md#unregister-an-application-type) son más rápidos para un paquete de aplicación comprimido.

mecanismo de implementación de Hello es el mismo para los paquetes comprimidos y sin comprimir. Si el paquete de saludo se comprime, se almacena como tal en el almacén de imágenes de clúster de Hola y está comprimida en el nodo de hello antes de ejecuta la aplicación hello.
compresión de Hello reemplaza paquete de Service Fabric válido Hola con la versión comprimida de Hola. carpeta de Hello debe permitir los permisos de escritura. La ejecución de la compresión en un paquete ya comprimido no produce ningún cambio.

Puede comprimir un paquete mediante la ejecución de comandos de Powershell de hello [copia ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) con `CompressPackage` cambiar. Puede descomprimir Hola empaquetar con hello mismo comando, mediante `UncompressPackage` cambiar.

Hello siguiente comando comprime paquete Hola sin copiar toohello almacén de imágenes. Puede copiar un paquete comprimido tooone o más clústeres de Service Fabric, según sea necesario, con [copia ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) sin hello `SkipCopy` marca.
paquete de Hello ahora incluye archivos comprimidos para hello `code`, `config`, y `data` paquetes. manifiesto de aplicación de Hola y Hola manifiestos de servicio no se comprimen, porque son necesarios para muchas operaciones internas (por ejemplo, uso compartido, extracción de nombre y la versión del tipo de aplicación para determinadas validaciones de paquete).
Manifiestos de hello en zip haría que estas operaciones ineficaces.

```
PS D:\temp> tree /f .\MyApplicationType

D:\TEMP\MYAPPLICATIONTYPE
│   ApplicationManifest.xml
│
└───MyServiceManifest
    │   ServiceManifest.xml
    │
    ├───MyCode
    │       MyServiceHost.exe
    │       MySetup.bat
    │
    ├───MyConfig
    │       Settings.xml
    │
    └───MyData
            init.dat
PS D:\temp> Copy-ServiceFabricApplicationPackage -ApplicationPackagePath .\MyApplicationType -CompressPackage -SkipCopy

PS D:\temp> tree /f .\MyApplicationType

D:\TEMP\MYAPPLICATIONTYPE
│   ApplicationManifest.xml
│
└───MyServiceManifest
       ServiceManifest.xml
       MyCode.zip
       MyConfig.zip
       MyData.zip

```

Como alternativa, puede comprimir y copiar el paquete Hola con [ServiceFabricApplicationPackage copia](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) en un solo paso.
Si el paquete de hello es grande, proporcione una hora de tooallow tiempo de espera lo suficientemente alto como para la compresión del paquete hello y clúster de hello carga toohello.
```
PS D:\temp> Copy-ServiceFabricApplicationPackage -ApplicationPackagePath .\MyApplicationType -ApplicationPackagePathInImageStore MyApplicationType -ImageStoreConnectionString fabric:ImageStore -CompressPackage -TimeoutSec 5400
```

Internamente, Service Fabric calcula las sumas de comprobación para los paquetes de aplicación hello para la validación. Cuando utilice la compresión, se calculan las sumas de comprobación de hello en hello las versiones comprimida de cada paquete.
Si ha copiado una versión sin comprimir el paquete de aplicación, y desea compresión toouse para hello mismo paquete, debe cambiar las versiones de Hola de hello `code`, `config`, y `data` incoherencia de suma de comprobación de paquetes tooavoid. Si los paquetes de saludo se modifican, en lugar de cambiar la versión de hello, puede usar [diferencias aprovisionamiento](service-fabric-application-upgrade-advanced.md). Con esta opción, no incluyen paquetes de saludo sin cambios en su lugar la referencia de manifiesto del servicio Hola.

De forma similar, si carga una versión comprimida del paquete de Hola y desea toouse un paquete sin comprimir, debe actualizar incoherencia de suma de comprobación de hello versiones tooavoid Hola.

Hello paquete es ahora empaqueta correctamente, validar y comprimido (si es necesario), por lo que está listo para [implementación](service-fabric-deploy-remove-applications.md) tooone o del tejido de servicio más clústeres.

### <a name="compress-packages-when-deploying-using-visual-studio"></a>Compresión de paquetes al implementar con Visual Studio
Puede indicar a paquetes de Visual Studio toocompress sobre la implementación, mediante la adición de hello `CopyPackageParameters` tooyour elemento perfil de publicación y establezca hello `CompressPackage` atributo demasiado`true`.

``` xml
    <PublishProfile xmlns="http://schemas.microsoft.com/2015/05/fabrictools">
        <ClusterConnectionParameters ConnectionEndpoint="mycluster.westus.cloudapp.azure.com" />
        <ApplicationParameterFile Path="..\ApplicationParameters\Cloud.xml" />
        <CopyPackageParameters CompressPackage="true"/>
    </PublishProfile>
```

## <a name="next-steps"></a>Pasos siguientes
[Implementar y quitar aplicaciones] [ 10] describe cómo toouse instancias de la aplicación de toomanage de PowerShell

[Administrar parámetros de la aplicación para varios entornos] [ 11] describe cómo tooconfigure parámetros y variables de entorno para las instancias de aplicación diferente.

[Configurar directivas de seguridad para la aplicación] [ 12] describe cómo toorun servicios con acceso de toorestrict de directivas de seguridad.

<!--Image references-->
[vs-package-command]: ./media/service-fabric-package-apps/vs-package-command.png

<!--Link references--In actual articles, you only need a single period before hello slash-->
[10]: service-fabric-deploy-remove-applications.md
[11]: service-fabric-manage-multiple-environment-app-configuration.md
[12]: service-fabric-application-runas-security.md
