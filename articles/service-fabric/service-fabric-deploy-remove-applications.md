---
title: "implementación de aplicaciones de Service Fabric aaaAzure | Documentos de Microsoft"
description: "¿Cómo toodeploy y quitar aplicaciones de Service Fabric mediante PowerShell."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: b120ffbf-f1e3-4b26-a492-347c29f8f66b
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/01/2017
ms.author: ryanwi
ms.openlocfilehash: 3de9c6a937ee7b29bf9ec86d6e9e631487797507
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-remove-applications-using-powershell"></a>Implementación y eliminación de aplicaciones con PowerShell
> [!div class="op_single_selector"]
> * [PowerShell](service-fabric-deploy-remove-applications.md)
> * [Visual Studio](service-fabric-publish-app-remote-cluster.md)
> * [API de FabricClient](service-fabric-deploy-remove-applications-fabricclient.md)
> 
> 

<br/>

Una vez que un [tipo de aplicación se ha empaquetado][10], está listo para la implementación en un clúster de Azure Service Fabric. Implementación implica Hola siga tres pasos:

1. Cargar el almacén de imágenes de toohello de paquete de aplicación de Hola
2. Registrar el tipo de aplicación Hola
3. Crear instancia de la aplicación hello

Después de implementa una aplicación y se ejecuta una instancia en clúster de hello, puede eliminar la instancia de la aplicación hello y su tipo de aplicación. toocompletely quitar una aplicación de clúster de hello implica Hola pasos:

1. Quitar (o eliminar) Hola ejecutando la instancia de la aplicación
2. Anular el registro del tipo de aplicación Hola si ya no lo necesite
3. Quitar el paquete de aplicación Hola Hola almacén de imágenes

Si usa [Visual Studio para implementar y depurar aplicaciones](service-fabric-publish-app-remote-cluster.md) en el clúster de desarrollo local, todo Hola pasos anteriores se administran automáticamente a través de un script de PowerShell.  Este script se encuentra en hello *Scripts* carpeta de proyecto de aplicación Hola. Este artículo proporciona información general acerca de lo que está haciendo esa secuencia de comandos para que pueda realizar Hola mismas operaciones fuera de Visual Studio. 
 
## <a name="connect-toohello-cluster"></a>Conectar el clúster toohello
Antes de ejecutar los comandos de PowerShell en este artículo, siempre se inicie mediante [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) clúster de Service Fabric toohello tooconnect. clúster de desarrollo local en toohello tooconnect, ejecute hello siguiente:

```powershell
PS C:\>Connect-ServiceFabricCluster
```

Para obtener ejemplos de conexión clúster remoto tooa o protegidos con Azure Active Directory, X509 certificados o Active Directory de Windows consulte [clúster segura de conectar tooa](service-fabric-connect-to-secure-cluster.md).

## <a name="upload-hello-application-package"></a>Cargar el paquete de aplicación Hola
Paquete de aplicación Hola cargando lo coloca en una ubicación que sea accesible para los componentes internos de Service Fabric.
Si desea que el paquete de aplicación de Hola de tooverify localmente, use hello [ServiceFabricApplicationPackage prueba](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) cmdlet.

Hola [ServiceFabricApplicationPackage copia](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) comando cargas Hola almacén de imágenes de clúster de toohello de paquete de aplicación.
Hola **ImageStoreConnectionStringFromClusterManifest Get** cmdlet, que forma parte del módulo de PowerShell de SDK de tejido de servicio de hello, es la imagen de Hola de tooget usado almacenar la cadena de conexión.  módulo tooimport Hola SDK, ejecute:

```powershell
Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
```

Imagine que compila y empaqueta una aplicación denominada *MyApplication* en Visual Studio 2015. De forma predeterminada, el nombre de tipo de aplicación de hello enumerado en hello ApplicationManifest.xml es "MyApplicationType".  paquete de aplicación, que contiene el manifiesto de aplicación necesarios de hello, manifiestos de servicio y los paquetes de datos/config/código, Hello se encuentra una en *C:\Users\<nombre de usuario\>\Documents\Visual Studio 2015\Projects\ MyApplication\MyApplication\pkg\Debug*. 

Hello comando siguiente muestra contenido Hola Hola del paquete de aplicación:

```powershell
PS C:\> $path = 'C:\Users\<user\>\Documents\Visual Studio 2015\Projects\MyApplication\MyApplication\pkg\Debug'
PS C:\> tree /f $path
Folder PATH listing for volume OSDisk
Volume serial number is 0459-2393
C:\USERS\USER\DOCUMENTS\VISUAL STUDIO 2015\PROJECTS\MYAPPLICATION\MYAPPLICATION\PKG\DEBUG
│   ApplicationManifest.xml
│
└───Stateless1Pkg
    │   ServiceManifest.xml
    │
    ├───Code
    │       Microsoft.ServiceFabric.Data.dll
    │       Microsoft.ServiceFabric.Data.Interfaces.dll
    │       Microsoft.ServiceFabric.Internal.dll
    │       Microsoft.ServiceFabric.Internal.Strings.dll
    │       Microsoft.ServiceFabric.Services.dll
    │       ServiceFabricServiceModel.dll
    │       Stateless1.exe
    │       Stateless1.exe.config
    │       Stateless1.pdb
    │       System.Fabric.dll
    │       System.Fabric.Strings.dll
    │
    └───Config
            Settings.xml
```

Si el paquete de aplicación hello es grande y tiene muchos archivos, puede [comprimirlo](service-fabric-package-apps.md#compress-a-package). compresión de Hola reduce el tamaño de Hola y el número de Hola de archivos.
Hello inconveniente es que hello registro y anulación del registro tipo de aplicación son más rápidos. Tiempo de carga puede ser más lento en la actualidad, sobre todo si incluyen paquetes de saludo tiempo toocompress Hola. 

toocompress un paquete, utilice Hola mismo [ServiceFabricApplicationPackage copia](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) comando. La compresión puede hacerse independiente de carga, mediante el uso de hello `SkipCopy` marcar o junto con hello la operación de carga. Comprimir un paquete comprimido es una operación inútil.
toouncompress un paquete comprimido, utilice Hola mismo [copia ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) comando con hello `UncompressPackage` cambiar.

Hello siguiente cmdlet comprime paquete Hola sin copiar toohello almacén de imágenes. paquete de Hello ahora incluye archivos comprimidos para hello `Code` y `Config` paquetes. no se comprimen aplicación Hello y manifiestos de servicio de hello, porque son necesarios para muchas operaciones internas (por ejemplo, uso compartido, extracción de nombre y la versión del tipo de aplicación para determinadas validaciones de paquete). Manifiestos de hello en zip haría que estas operaciones ineficaces.

```
PS C:\> Copy-ServiceFabricApplicationPackage -ApplicationPackagePath $path -CompressPackage -SkipCopy
PS C:\> tree /f $path
Folder PATH listing for volume OSDisk
Volume serial number is 0459-2393
C:\USERS\USER\DOCUMENTS\VISUAL STUDIO 2015\PROJECTS\MYAPPLICATION\MYAPPLICATION\PKG\DEBUG
|   ApplicationManifest.xml
|
└───Stateless1Pkg
       Code.zip
       Config.zip
       ServiceManifest.xml
```

Para los paquetes de aplicación de gran tamaño, la compresión de hello lleva tiempo. Para obtener mejores resultados, use una unidad SSD rápida. tiempos de compresión de Hola y el tamaño de hello del paquete comprimido de hello también varían en función de contenido del paquete de saludo.
Por ejemplo, aquí son las estadísticas de compresión de algunos paquetes, que muestran inicial Hola y Hola a tamaño del paquete comprimido, con tiempo de compresión de Hola.

|Tamaño inicial (MB)|Número de archivos|Tipos de compresión|Tamaño de paquete comprimido (MB)|
|----------------:|---------:|---------------:|---------------------------:|
|100|100|00:00:03.3547592|60|
|512|100|00:00:16.3850303|307|
|1024|500|00:00:32.5907950|615|
|2048|1000|00:01:04.3775554|1231|
|5012|100|00:02:45.2951288|3074|

Una vez que un paquete está comprimido, puede ser tooone cargado o clústeres de varios Service Fabric según sea necesario. mecanismo de implementación de Hello es el mismo para los paquetes comprimidos y sin comprimir. Si el paquete de saludo se comprime, se almacena como tal en el almacén de imágenes de clúster de Hola y está comprimida en el nodo de hello antes de ejecuta la aplicación hello.


Hello en el ejemplo siguiente se carga el almacén de imágenes de toohello de paquete de hello en una carpeta denominada "MyApplicationV1":

```powershell
PS C:\> Copy-ServiceFabricApplicationPackage -ApplicationPackagePath $path -ApplicationPackagePathInImageStore MyApplicationV1 -ImageStoreConnectionString (Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest)) -TimeoutSec 1800
```

Hola **ImageStoreConnectionStringFromClusterManifest Get** cmdlet, que forma parte del módulo de PowerShell de SDK de tejido de servicio de hello, es la imagen de Hola de tooget usado almacenar la cadena de conexión.  módulo tooimport Hola SDK, ejecute:

```powershell
Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
```

Si no se especifica hello *ApplicationPackagePathInImageStore -* parámetro, el paquete de aplicación Hola se copia en la carpeta de "Debug" hello en el almacén de imágenes de Hola.

Hola tarda tooupload un paquete depende de varios factores. Algunos de estos factores son el número de Hola de archivos de paquete de hello, tamaño de paquete de Hola y tamaños de archivo Hola. velocidad de la red entre la máquina de origen de Hola y clúster de Service Fabric Hola Hola también afecta al tiempo de carga de Hola. Hola tiempo de espera predeterminado para [ServiceFabricApplicationPackage copia](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) es de 30 minutos.
Dependiendo de Hola factores descritos, es posible que tenga tiempo de espera de tooincrease Hola. Si va a comprimir paquete hello en llamada de copia de hello, necesita tooalso considere la posibilidad de tiempo de compresión de Hola.

Vea [comprender la cadena de conexión de almacén de imágenes de hello](service-fabric-image-store-connection-string.md) para obtener información adicional sobre Hola image store e imagen almacenan la cadena de conexión.

## <a name="register-hello-application-package"></a>Registrar el paquete de aplicación Hola
tipo de aplicación de Hola y la versión declarada en el manifiesto de aplicación Hola estén disponible para su uso cuando se registra el paquete de aplicación Hola. sistema Hola lee el paquete de hello cargado en el paso anterior de hello, comprueba el paquete de hello, procesa el contenido del paquete hello y copia la ubicación de hello procesa paquete tooan interno del sistema.  

Ejecute hello [ServiceFabricApplicationType Register](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) cmdlet tooregister Hola tipo de aplicación en clúster de Hola y ponerla a disposición de implementación:

```powershell
PS C:\> Register-ServiceFabricApplicationType MyApplicationV1
Register application type succeeded
```

"MyApplicationV1" es la carpeta de hello en almacén de imágenes de Hola donde se encuentra el paquete de aplicación de Hola. tipo de aplicación Hola con nombre "MyApplicationType" y la versión "1.0.0" (ambos se encuentran en el manifiesto de aplicación Hola) ya está registrado en clúster de Hola.

Hola [ServiceFabricApplicationType Register](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) comando devuelve solo después de sistema de hello tiene el paquete de aplicación Hola se registró correctamente. Cuánto tiempo toma del registro depende de tamaño de Hola y el contenido del paquete de aplicación Hola. Si es necesario, Hola **- TimeoutSec** parámetro puede ser usado toosupply un tiempo de espera (tiempo de espera de hello predeterminado es 60 segundos).

Si tiene una aplicación grande del paquete o si se producen tiempos de espera, utilice hello **- Async** parámetro. comando de Hello devuelve al clúster de hello acepta comandos de registro de hello, y el procesamiento de hello continúa según sea necesario.
Hola [Get ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) comando enumera todas las versiones de tipo de aplicación se registró correctamente y su estado de registro. Puede usar este comando toodetermine cuando se realizó el registro de hello.

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

## <a name="create-hello-application"></a>Crear aplicación hello
Puede crear una instancia de una aplicación desde cualquier versión de tipo de aplicación que se ha registrado correctamente mediante el uso de hello [ServiceFabricApplication New](/powershell/module/servicefabric/new-servicefabricapplication?view=azureservicefabricps) cmdlet. Hola de cada aplicación debe empezar con hello *"fabric:"* esquema y debe ser único para cada instancia de la aplicación. También se crean los servicios de valor predeterminado definidos en el manifiesto de aplicación Hola del tipo de aplicación de destino de Hola.

```powershell
PS C:\> New-ServiceFabricApplication fabric:/MyApp MyApplicationType 1.0.0

ApplicationName        : fabric:/MyApp
ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
ApplicationParameters  : {}
```
Pueden crearse varias instancias de aplicación para cualquier versión concreta de un tipo de aplicación registrado. Cada instancia de la aplicación se ejecuta de forma aislada, con su propio proceso y directorio de trabajo.

toosee que el nombre de aplicaciones y servicios se ejecutan en el clúster hello, ejecute hello [Get ServiceFabricApplication](/powershell/servicefabric/vlatest/get-servicefabricapplication) y [ServiceFabricService Get](/powershell/module/servicefabric/get-servicefabricservice?view=azureservicefabricps) cmdlets:

```powershell
PS C:\> Get-ServiceFabricApplication  

ApplicationName        : fabric:/MyApp
ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
ApplicationStatus      : Ready
HealthState            : Ok
ApplicationParameters  : {}

PS C:\> Get-ServiceFabricApplication | Get-ServiceFabricService

ServiceName            : fabric:/MyApp/Stateless1
ServiceKind            : Stateless
ServiceTypeName        : Stateless1Type
IsServiceGroup         : False
ServiceManifestVersion : 1.0.0
ServiceStatus          : Active
HealthState            : Ok
```

## <a name="remove-an-application"></a>Eliminación de una aplicación
Cuando ya no se necesita una instancia de la aplicación, permanentemente puede quitar por nombre usando hello [Remove-ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) cmdlet. [Remove-ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) quita automáticamente todos los servicios que pertenecen, así, permanentemente quitar todo el estado de servicio de aplicación de toohello. 

> [!WARNING]
> No se puede deshacer esta operación y no se puede recuperar el estado de la aplicación.

```powershell
PS C:\> Remove-ServiceFabricApplication fabric:/MyApp

Confirm
Continue with this operation?
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"):
Remove application instance succeeded

PS C:\> Get-ServiceFabricApplication
```

## <a name="unregister-an-application-type"></a>Anulación de un registro del tipo de aplicación
Cuando ya no se necesita una versión concreta de un tipo de aplicación, debe anular el registro del tipo de aplicación Hola con hello [Unregister-ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) cmdlet. Al anular el registro aplicación sin usar tipos versiones espacio de almacenamiento utilizado por el almacén de imágenes de Hola. No se puede anular el registro de un tipo de aplicación mientras no haya ninguna aplicación con instancias con él o no haya actualizaciones de aplicaciones pendientes que hagan referencia a él.

Ejecutar [ServiceFabricApplicationType Get](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) toosee los tipos de aplicación Hola registran actualmente en el clúster de hello:

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

Ejecutar [Unregister-ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) toounregister un tipo concreto de aplicación:

```powershell
PS C:\> Unregister-ServiceFabricApplicationType MyApplicationType 1.0.0
```

## <a name="remove-an-application-package-from-hello-image-store"></a>Quitar un paquete de aplicación Hola almacén de imágenes
Cuando ya no se necesita un paquete de aplicación, puede eliminarla del Hola imagen almacén toofree los recursos del sistema.

```powershell
PS C:\>Remove-ServiceFabricApplicationPackage -ApplicationPackagePathInImageStore MyApplicationV1 -ImageStoreConnectionString (Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest))
```

## <a name="troubleshooting"></a>Solución de problemas
### <a name="copy-servicefabricapplicationpackage-asks-for-an-imagestoreconnectionstring"></a>Copy-ServiceFabricApplicationPackage pide una ImageStoreConnectionString
entorno de SDK del servicio Fabric Hola ya debe tener Hola correcto de configurar los valores predeterminados. Pero si es necesario, debe coincidir con el valor de Hola Hola ImageStoreConnectionString para todos los comandos que Hola tejido de servicio de clúster. Puede encontrar Hola ImageStoreConnectionString en el manifiesto de clúster de hello, recuperar con hello [Get-ServiceFabricClusterManifest](/powershell/module/servicefabric/get-servicefabricclustermanifest?view=azureservicefabricps) y comandos de Get-ImageStoreConnectionStringFromClusterManifest:

```powershell
PS C:\> Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest)
```

Hola **ImageStoreConnectionStringFromClusterManifest Get** cmdlet, que forma parte del módulo de PowerShell de SDK de tejido de servicio de hello, es la imagen de Hola de tooget usado almacenar la cadena de conexión.  módulo tooimport Hola SDK, ejecute:

```powershell
Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
```

Hola ImageStoreConnectionString se encuentra en el manifiesto de clúster de hello:

```xml
<ClusterManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Name="Server-Default-SingleNode" Version="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">

    [...]

    <Section Name="Management">
      <Parameter Name="ImageStoreConnectionString" Value="file:D:\ServiceFabric\Data\ImageStore" />
    </Section>

    [...]
```

Vea [comprender la cadena de conexión de almacén de imágenes de hello](service-fabric-image-store-connection-string.md) para obtener información adicional sobre Hola image store e imagen almacenan la cadena de conexión.

### <a name="deploy-large-application-package"></a>Implementación de un paquete de aplicación grande
Problema: [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) agota el tiempo de espera para un paquete de aplicación grande (del orden de GB).
Pruebe lo siguiente:
- Especifique un tiempo de espera mayor para el comando [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) con el parámetro `TimeoutSec`. De forma predeterminada, el tiempo de espera de hello es de 30 minutos.
- Compruebe la conexión de red de hello entre la máquina de origen y el clúster. Si Hola conexión es lenta, considere la posibilidad de usar una máquina con una conexión de red mejor.
Si es equipo del cliente de hello en otra región de clúster de hello, considere la posibilidad de mediante un equipo cliente en una región más cerca o mismo como clúster de Hola.
- Compruebe si está alcanzando la limitación externa. Por ejemplo, al almacén de imágenes de hello es almacenamiento configurado toouse de azure, se puede limitar carga.

Problema: La carga del paquete se completó correctamente, pero [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) agota el tiempo de espera. Pruebe lo siguiente:
- [Comprimir el paquete de hello](service-fabric-package-apps.md#compress-a-package) antes de copiar el almacén de imágenes de toohello.
compresión Hola reduce el tamaño de Hola y número de Hola de archivos, que a su vez, reduce la cantidad de Hola de tráfico y funcionar a ese Service Fabric debe realizar. operación de carga de Hello puede ser más lento (sobre todo si se incluye el tiempo de compresión de hello), pero el tipo de aplicación Hola registrar y anular el registro son más rápidos.
- Especifique un tiempo de espera mayor para [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) con el parámetro `TimeoutSec`.
- Especifique el modificador `Async` para [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps). comando de Hello devuelve al clúster Hola acepta comandos de Hola y registro de hello del tipo de aplicación Hola continúa de forma asincrónica. Por este motivo, no hay ninguna necesidad de toospecify un mayor tiempo de espera en este caso. Hola [Get ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) comando enumera todas las versiones de tipo de aplicación se registró correctamente y su estado de registro. Puede usar este comando toodetermine cuando se realizó el registro de hello.

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

### <a name="deploy-application-package-with-many-files"></a>Implementación del paquete de aplicación con muchos archivos
Problema: [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) agota el tiempo de espera para un paquete de aplicación con muchos archivos (del orden de miles).
Pruebe lo siguiente:
- [Comprimir el paquete de hello](service-fabric-package-apps.md#compress-a-package) antes de copiar el almacén de imágenes de toohello. compresión de Hello reduce el número Hola de archivos.
- Especifique un tiempo de espera mayor para [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) con el parámetro `TimeoutSec`.
- Especifique el modificador `Async` para [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps). comando de Hello devuelve al clúster Hola acepta comandos de Hola y registro de hello del tipo de aplicación Hola continúa de forma asincrónica.
Por este motivo, no hay ninguna necesidad de toospecify un mayor tiempo de espera en este caso. Hola [Get ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) comando enumera todas las versiones de tipo de aplicación se registró correctamente y su estado de registro. Puede usar este comando toodetermine cuando se realizó el registro de hello.

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

## <a name="next-steps"></a>Pasos siguientes
[Actualización de la aplicación de Service Fabric](service-fabric-application-upgrade.md)

[Introducción al estado de Service Fabric](service-fabric-health-introduction.md)

[Diagnosticar y solucionar problemas de un servicio de Service Fabric](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[Modelar una aplicación en Service Fabric](service-fabric-application-model.md)

<!--Link references--In actual articles, you only need a single period before hello slash-->
[10]: service-fabric-application-model.md
[11]: service-fabric-application-upgrade.md
