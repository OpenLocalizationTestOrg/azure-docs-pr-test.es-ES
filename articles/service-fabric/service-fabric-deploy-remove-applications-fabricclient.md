---
title: "implementación de aplicaciones de Service Fabric aaaAzure | Documentos de Microsoft"
description: Usar hello FabricClient APIs toodeploy y quite las aplicaciones de Service Fabric.
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
ms.date: 07/07/2017
ms.author: ryanwi
ms.openlocfilehash: b2986b71c461f3e785ba16ec1b827fe47ad852fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-remove-applications-using-fabricclient"></a>Implementación y eliminación de aplicaciones mediante FabricClient
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
Conecta el clúster de toohello mediante la creación de un [FabricClient](/dotnet/api/system.fabric.fabricclient) instancia antes de ejecutar cualquiera de hello ejemplos de código de este artículo. Para obtener ejemplos de clúster de desarrollo local tooa conexión o un clúster remoto o un clúster protegido con Azure Active Directory, X509 certificados o Active Directory de Windows consulte [clúster segura de conectar tooa](service-fabric-connect-to-secure-cluster.md#connect-to-a-cluster-using-the-fabricclient-apis). clúster de desarrollo local en toohello tooconnect, ejecute hello siguiente:

```csharp
// Connect toohello local cluster.
FabricClient fabricClient = new FabricClient();
```

## <a name="upload-hello-application-package"></a>Cargar el paquete de aplicación Hola
Imagine que compila y empaqueta una aplicación denominada *MyApplication* en Visual Studio. De forma predeterminada, el nombre de tipo de aplicación de hello enumerado en hello ApplicationManifest.xml es "MyApplicationType".  paquete de aplicación, que contiene el manifiesto de aplicación necesarios de hello, manifiestos de servicio y los paquetes de datos/config/código, Hello se encuentra una en *C:\Users\&lt; nombre de usuario&gt;\Documents\Visual Studio 2017\Projects\ MyApplication\MyApplication\pkg\Debug*.

Paquete de aplicación Hola cargando lo coloca en una ubicación que sea accesible para los componentes internos de Service Fabric Hola. Service Fabric comprueba el paquete de aplicación Hola durante el registro de Hola Hola del paquete de aplicación. Sin embargo, si desea tooverify Hola paquete de la aplicación localmente (es decir, antes de cargar), use hello [ServiceFabricApplicationPackage prueba](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) cmdlet.

Hola [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) API carga el almacén de imágenes de clúster de toohello paquete de aplicación de Hola. 

Si el paquete de aplicación hello es grande y tiene muchos archivos, puede [comprimirlo](service-fabric-package-apps.md#compress-a-package) y cópielo toohello almacén de imágenes mediante PowerShell. compresión de Hola reduce el tamaño de Hola y el número de Hola de archivos.

Vea [comprender la cadena de conexión de almacén de imágenes de hello](service-fabric-image-store-connection-string.md) para obtener información adicional sobre Hola image store e imagen almacenan la cadena de conexión.

## <a name="register-hello-application-package"></a>Registrar el paquete de aplicación Hola
tipo de aplicación de Hola y la versión declarada en el manifiesto de aplicación Hola estén disponible para su uso cuando se registra el paquete de aplicación Hola. sistema Hola lee el paquete de hello cargado en el paso anterior de hello, comprueba el paquete de hello, procesa el contenido del paquete hello y copia la ubicación de hello procesa paquete tooan interno del sistema.  

Hola [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) API registros Hola tipo de aplicación en clúster de Hola y hacer que esté disponible para la implementación.

Hola [GetApplicationTypeListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationtypelistasync) API proporciona información acerca de todos los tipos de aplicación se registró correctamente. Puede utilizar esta API toodetermine cuando se realizó el registro de hello.

## <a name="create-an-application-instance"></a>Creación de una instancia de aplicación
Puede crear una instancia de una aplicación de cualquier tipo de aplicación que se ha registrado correctamente mediante el uso de hello [CreateApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.createapplicationasync) API. Hola de cada aplicación debe empezar con hello *"fabric:"* esquema y debe ser único para cada instancia de la aplicación (dentro de un clúster). También se crean los servicios de valor predeterminado definidos en el manifiesto de aplicación Hola del tipo de aplicación de destino de Hola.

Pueden crearse varias instancias de aplicación para cualquier versión concreta de un tipo de aplicación registrado. Cada instancia de la aplicación se ejecuta de forma aislada, con su propio directorio de trabajo y conjunto de procesos.

toosee que el nombre de las aplicaciones y servicios se ejecutan en el clúster de hello, ejecute hello [GetApplicationListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationlistasync) y [GetServiceListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getservicelistasync) API.

## <a name="create-a-service-instance"></a>Creación de una instancia de servicio
Puede crear una instancia de un servicio de un tipo de servicio con hello [CreateServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) API.  Si el servicio de Hola se declara como un servicio de forma predeterminada en el manifiesto de aplicación Hola, servicio de Hola se crea una instancia cuando se crea una instancia de aplicación hello.  Llamar a hello [CreateServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) API para un servicio que ya se ha creado una instancia devolverá una excepción de tipo FabricException que contiene un código de error con un valor de FabricErrorCode.ServiceAlreadyExists.

## <a name="remove-a-service-instance"></a>Eliminación de una instancia de servicio
Cuando ya no se necesita una instancia de servicio, puede quitarlo de hello ejecuta instancia de la aplicación que realiza la llamada hello [DeleteServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.deleteserviceasync) API.  

> [!WARNING]
> Esta operación no se puede revertir y el estado del servicio no se puede recuperar.

## <a name="remove-an-application-instance"></a>Eliminación de una instancia de aplicación
Cuando ya no se necesita una instancia de la aplicación, permanentemente puede quitar por nombre usando hello [DeleteApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.deleteapplicationasync) API. [DeleteApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.deleteapplicationasync) quita automáticamente todos los servicios que pertenecen, así, permanentemente quitar todo el estado de servicio de aplicación de toohello.

> [!WARNING]
> No se puede deshacer esta operación y no se puede recuperar el estado de la aplicación.

## <a name="unregister-an-application-type"></a>Anulación de un registro del tipo de aplicación
Cuando ya no se necesita una versión concreta de un tipo de aplicación, debe anular el registro de una versión concreta del tipo de aplicación Hola con hello [Unregister-ServiceFabricApplicationType](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.unprovisionapplicationasync) API. Versiones sin usar al anular el registro aplicación tipos versiones de espacio de almacenamiento utilizado por el almacén de imágenes de Hola. Se puede anular una versión de un tipo de aplicación siempre y cuando ninguna de las aplicaciones se crean instancias en esa versión del tipo de aplicación hello y ninguna actualización pendiente aplicación hacen referencia a esa versión del tipo de aplicación Hola.

## <a name="remove-an-application-package-from-hello-image-store"></a>Quitar un paquete de aplicación Hola almacén de imágenes
Cuando ya no se necesita un paquete de aplicación, puede eliminarla del Hola imagen almacén toofree los recursos del sistema mediante hello [RemoveApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.removeapplicationpackage) API.

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
Problema: la API [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) agota el tiempo de espera para un paquete de aplicación grande (del orden de GB).
Pruebe lo siguiente:
- Especifique un tiempo de espera mayor para el método [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) con el parámetro `timeout`. De forma predeterminada, el tiempo de espera de hello es de 30 minutos.
- Compruebe la conexión de red de hello entre la máquina de origen y el clúster. Si Hola conexión es lenta, considere la posibilidad de usar una máquina con una conexión de red mejor.
Si es equipo del cliente de hello en otra región de clúster de hello, considere la posibilidad de mediante un equipo cliente en una región más cerca o mismo como clúster de Hola.
- Compruebe si está alcanzando la limitación externa. Por ejemplo, al almacén de imágenes de hello es almacenamiento configurado toouse de azure, se puede limitar carga.

Problema: la carga del paquete se completó correctamente, pero la API [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) agota el tiempo de espera. Pruebe lo siguiente:
- [Comprimir el paquete de hello](service-fabric-package-apps.md#compress-a-package) antes de copiar el almacén de imágenes de toohello.
compresión Hola reduce el tamaño de Hola y número de Hola de archivos, que a su vez, reduce la cantidad de Hola de tráfico y funcionar a ese Service Fabric debe realizar. operación de carga de Hello puede ser más lento (sobre todo si se incluye el tiempo de compresión de hello), pero el tipo de aplicación Hola registrar y anular el registro son más rápidos.
- Especifique un tiempo de espera mayor para la API [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) con el parámetro `timeout`.

### <a name="deploy-application-package-with-many-files"></a>Implementación del paquete de aplicación con muchos archivos
Problema: [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) agota el tiempo de espera para un paquete de aplicación con muchos archivos (del orden de miles).
Pruebe lo siguiente:
- [Comprimir el paquete de hello](service-fabric-package-apps.md#compress-a-package) antes de copiar el almacén de imágenes de toohello. compresión de Hello reduce el número Hola de archivos.
- Especifique un tiempo de espera mayor para [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) con el parámetro `timeout`.

## <a name="code-example"></a>Ejemplo de código
Hello en el ejemplo siguiente se copia un almacén de imágenes de toohello de paquete de aplicación, aprovisiona el tipo de aplicación Hola, crea una instancia de la aplicación, crea una instancia de servicio, instancia de la aplicación hello quita, aprovisiona un tipo de aplicación Hola, y Elimina el paquete de aplicación Hola Hola almacén de imágenes.

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Reflection;
using System.Threading.Tasks;

using System.Fabric;
using System.Fabric.Description;
using System.Threading;

namespace ServiceFabricAppLifecycle
{
class Program
{
static void Main(string[] args)
{

    string clusterConnection = "localhost:19000";
    string appName = "fabric:/MyApplication";
    string appType = "MyApplicationType";
    string appVersion = "1.0.0";
    string serviceName = "fabric:/MyApplication/Stateless1";
    string imageStoreConnectionString = "file:C:\\SfDevCluster\\Data\\ImageStoreShare";
    string packagePathInImageStore = "MyApplication";
    string packagePath = "C:\\Users\\username\\Documents\\Visual Studio 2017\\Projects\\MyApplication\\MyApplication\\pkg\\Debug";
    string serviceType = "Stateless1Type";

    // Connect toohello cluster.
    FabricClient fabricClient = new FabricClient(clusterConnection);

    // Copy hello application package tooa location in hello image store
    try
    {
        fabricClient.ApplicationManager.CopyApplicationPackage(imageStoreConnectionString, packagePath, packagePathInImageStore);
        Console.WriteLine("Application package copied too{0}", packagePathInImageStore);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("Application package copy tooImage Store failed: ");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Provision hello application.  "MyApplicationV1" is hello folder in hello image store where hello application package is located. 
    // hello application type with name "MyApplicationType" and version "1.0.0" (both are found in hello application manifest) 
    // is now registered in hello cluster.            
    try
    {
        fabricClient.ApplicationManager.ProvisionApplicationAsync(packagePathInImageStore).Wait();

        Console.WriteLine("Provisioned application type {0}", packagePathInImageStore);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("Provision Application Type failed:");

        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    //  Create hello application instance.
    try
    {
        ApplicationDescription appDesc = new ApplicationDescription(new Uri(appName), appType, appVersion);
        fabricClient.ApplicationManager.CreateApplicationAsync(appDesc).Wait();
        Console.WriteLine("Created application instance of type {0}, version {1}", appType, appVersion);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("CreateApplication failed.");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Create hello stateless service description.  For stateful services, use a StatefulServiceDescription object.
    StatelessServiceDescription serviceDescription = new StatelessServiceDescription();
    serviceDescription.ApplicationName = new Uri(appName);
    serviceDescription.InstanceCount = 1;
    serviceDescription.PartitionSchemeDescription = new SingletonPartitionSchemeDescription();
    serviceDescription.ServiceName = new Uri(serviceName);
    serviceDescription.ServiceTypeName = serviceType;

    // Create hello service instance.  If hello service is declared as a default service in hello ApplicationManifest.xml,
    // hello service instance is already running and this call will fail.
    try
    {
        fabricClient.ServiceManager.CreateServiceAsync(serviceDescription).Wait();
        Console.WriteLine("Created service instance {0}", serviceName);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("CreateService failed.");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Delete a service instance.
    try
    {
        DeleteServiceDescription deleteServiceDescription = new DeleteServiceDescription(new Uri(serviceName));

        fabricClient.ServiceManager.DeleteServiceAsync(deleteServiceDescription);
        Console.WriteLine("Deleted service instance {0}", serviceName);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("DeleteService failed.");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Delete an application instance from hello application type.
    try
    {
        DeleteApplicationDescription deleteApplicationDescription = new DeleteApplicationDescription(new Uri(appName));

        fabricClient.ApplicationManager.DeleteApplicationAsync(deleteApplicationDescription).Wait();
        Console.WriteLine("Deleted application instance {0}", appName);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("DeleteApplication failed.");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Un-provision hello application type.
    try
    {
        fabricClient.ApplicationManager.UnprovisionApplicationAsync(appType, appVersion).Wait();
        Console.WriteLine("Un-provisioned application type {0}, version {1}", appType, appVersion);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("Un-provision application type failed: ");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Delete hello application package from a location in hello image store.
    try
    {
        fabricClient.ApplicationManager.RemoveApplicationPackage(imageStoreConnectionString, packagePathInImageStore);
        Console.WriteLine("Application package removed from {0}", packagePathInImageStore);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("Application package removal from Image Store failed: ");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    Console.WriteLine("Hit enter...");
    Console.Read();
}        
}
}

```

## <a name="next-steps"></a>Pasos siguientes
[Actualización de la aplicación de Service Fabric](service-fabric-application-upgrade.md)

[Introducción al estado de Service Fabric](service-fabric-health-introduction.md)

[Diagnosticar y solucionar problemas de un servicio de Service Fabric](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[Modelar una aplicación en Service Fabric](service-fabric-application-model.md)

<!--Link references--In actual articles, you only need a single period before hello slash-->
[10]: service-fabric-application-model.md
[11]: service-fabric-application-upgrade.md
