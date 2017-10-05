---
title: "Implementación de la aplicación de Azure Service Fabric | Microsoft Docs"
description: Use las API de FabricClient para implementar y quitar aplicaciones de Service Fabric.
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
ms.openlocfilehash: 2e4ca1069b4e8e473b26b790e81770b41e25ff50
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-and-remove-applications-using-fabricclient"></a><span data-ttu-id="8720e-103">Implementación y eliminación de aplicaciones mediante FabricClient</span><span class="sxs-lookup"><span data-stu-id="8720e-103">Deploy and remove applications using FabricClient</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8720e-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8720e-104">PowerShell</span></span>](service-fabric-deploy-remove-applications.md)
> * [<span data-ttu-id="8720e-105">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="8720e-105">Visual Studio</span></span>](service-fabric-publish-app-remote-cluster.md)
> * [<span data-ttu-id="8720e-106">API de FabricClient</span><span class="sxs-lookup"><span data-stu-id="8720e-106">FabricClient APIs</span></span>](service-fabric-deploy-remove-applications-fabricclient.md)
> 
> 

<br/>

<span data-ttu-id="8720e-107">Una vez que un [tipo de aplicación se ha empaquetado][10], está listo para la implementación en un clúster de Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="8720e-107">Once an [application type has been packaged][10], it's ready for deployment into an Azure Service Fabric cluster.</span></span> <span data-ttu-id="8720e-108">La implementación implica los tres pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="8720e-108">Deployment involves the following three steps:</span></span>

1. <span data-ttu-id="8720e-109">Carga del paquete de aplicación en el almacén de imágenes</span><span class="sxs-lookup"><span data-stu-id="8720e-109">Upload the application package to the image store</span></span>
2. <span data-ttu-id="8720e-110">Cargar el tipo de aplicación</span><span class="sxs-lookup"><span data-stu-id="8720e-110">Register the application type</span></span>
3. <span data-ttu-id="8720e-111">Crear la instancia de aplicación</span><span class="sxs-lookup"><span data-stu-id="8720e-111">Create the application instance</span></span>

<span data-ttu-id="8720e-112">Después de que se ha implementado una aplicación y una instancia está en funcionamiento en el clúster, puede eliminar la instancia de aplicación y su tipo de aplicación.</span><span class="sxs-lookup"><span data-stu-id="8720e-112">After an application is deployed and an instance is running in the cluster, you can delete the application instance and its application type.</span></span> <span data-ttu-id="8720e-113">Para quitar completamente una aplicación del clúster, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="8720e-113">To completely remove an application from the cluster involves the following steps:</span></span>

1. <span data-ttu-id="8720e-114">Quitar (o eliminar) la instancia de la aplicación en ejecución</span><span class="sxs-lookup"><span data-stu-id="8720e-114">Remove (or delete) the running application instance</span></span>
2. <span data-ttu-id="8720e-115">Anular el registro del tipo de aplicación si ya no lo necesita</span><span class="sxs-lookup"><span data-stu-id="8720e-115">Unregister the application type if you no longer need it</span></span>
3. <span data-ttu-id="8720e-116">Quitar el paquete de aplicación del almacén de imágenes</span><span class="sxs-lookup"><span data-stu-id="8720e-116">Remove the application package from the image store</span></span>

<span data-ttu-id="8720e-117">Si usa [Visual Studio para implementar y depurar aplicaciones](service-fabric-publish-app-remote-cluster.md) en el clúster de desarrollo local, todos los pasos anteriores se controlan automáticamente mediante un script de PowerShell,</span><span class="sxs-lookup"><span data-stu-id="8720e-117">If you use [Visual Studio for deploying and debugging applications](service-fabric-publish-app-remote-cluster.md) on your local development cluster, all the preceding steps are handled automatically through a PowerShell script.</span></span>  <span data-ttu-id="8720e-118">que se encuentra en la carpeta *Scripts* del proyecto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="8720e-118">This script is found in the *Scripts* folder of the application project.</span></span> <span data-ttu-id="8720e-119">En este artículo se ofrece información sobre lo que hace ese script para que pueda realizar las mismas operaciones fuera de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8720e-119">This article provides background on what that script is doing so that you can perform the same operations outside of Visual Studio.</span></span> 
 
## <a name="connect-to-the-cluster"></a><span data-ttu-id="8720e-120">Conexión al clúster</span><span class="sxs-lookup"><span data-stu-id="8720e-120">Connect to the cluster</span></span>
<span data-ttu-id="8720e-121">Para conectarse al clúster, cree una instancia de [FabricClient](/dotnet/api/system.fabric.fabricclient) antes de ejecutar cualquiera de los ejemplos de código de este artículo.</span><span class="sxs-lookup"><span data-stu-id="8720e-121">Connect to the cluster by creating a [FabricClient](/dotnet/api/system.fabric.fabricclient) instance before you run any of the code examples in this article.</span></span> <span data-ttu-id="8720e-122">Para obtener ejemplos de conexión a un clúster de desarrollo local, a un clúster remoto o a un cluster protegido con Azure Active Directory, certificados X509 o Windows Active Directory, consulte [Conexión a un clúster seguro](service-fabric-connect-to-secure-cluster.md#connect-to-a-cluster-using-the-fabricclient-apis).</span><span class="sxs-lookup"><span data-stu-id="8720e-122">For examples of connecting to a local development cluster or a remote cluster or cluster secured using Azure Active Directory, X509 certificates, or Windows Active Directory see [Connect to a secure cluster](service-fabric-connect-to-secure-cluster.md#connect-to-a-cluster-using-the-fabricclient-apis).</span></span> <span data-ttu-id="8720e-123">Para conectarse al clúster de desarrollo local, ejecute lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="8720e-123">To connect to the local development cluster, run the following:</span></span>

```csharp
// Connect to the local cluster.
FabricClient fabricClient = new FabricClient();
```

## <a name="upload-the-application-package"></a><span data-ttu-id="8720e-124">Cargar el paquete de la aplicación</span><span class="sxs-lookup"><span data-stu-id="8720e-124">Upload the application package</span></span>
<span data-ttu-id="8720e-125">Imagine que compila y empaqueta una aplicación denominada *MyApplication* en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8720e-125">Suppose you build and package an application named *MyApplication* in Visual Studio.</span></span> <span data-ttu-id="8720e-126">De forma predeterminada, el nombre del tipo de aplicación que aparece en ApplicationManifest.xml es "MyApplicationType".</span><span class="sxs-lookup"><span data-stu-id="8720e-126">By default, the application type name listed in the ApplicationManifest.xml is "MyApplicationType".</span></span>  <span data-ttu-id="8720e-127">El paquete de aplicación, que contiene el manifiesto de aplicación necesario, así como los manifiestos de servicio y los paquetes code/config/data, se encuentra en *C:\Users\&username&gt;\Documents\Visual Studio 2017\Projects\MyApplication\MyApplication\pkg\Debug*.</span><span class="sxs-lookup"><span data-stu-id="8720e-127">The application package, which contains the necessary application manifest, service manifests, and code/config/data packages, is located in *C:\Users\&lt;username&gt;\Documents\Visual Studio 2017\Projects\MyApplication\MyApplication\pkg\Debug*.</span></span>

<span data-ttu-id="8720e-128">Cargar el paquete de aplicación lo pone en una ubicación a la que pueden tener acceso los componentes internos de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="8720e-128">Uploading the application package puts it in a location that's accessible by the internal Service Fabric components.</span></span> <span data-ttu-id="8720e-129">Service Fabric comprueba el paquete de aplicación durante su registro.</span><span class="sxs-lookup"><span data-stu-id="8720e-129">Service Fabric verifies the application package during the registration of the application package.</span></span> <span data-ttu-id="8720e-130">Sin embargo, si quiere comprobar el paquete de aplicación de forma local (es decir, antes de cargarlo), use el cmdlet [Test-ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="8720e-130">However, if you want to verify the application package locally (i.e., before uploading), use the [Test-ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="8720e-131">La API [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) carga el paquete de aplicación en el almacén de imágenes del clúster.</span><span class="sxs-lookup"><span data-stu-id="8720e-131">The [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) API uploads the application package to the cluster image store.</span></span> 

<span data-ttu-id="8720e-132">Si el paquete de aplicación es grande o tiene muchos archivos, puede [comprimirlo](service-fabric-package-apps.md#compress-a-package) y copiarlo en el almacén de imágenes mediante PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8720e-132">If the application package is large and/or has many files, you can [compress it](service-fabric-package-apps.md#compress-a-package) and copy it to the image store using PowerShell.</span></span> <span data-ttu-id="8720e-133">La compresión reduce el tamaño y el número de archivos.</span><span class="sxs-lookup"><span data-stu-id="8720e-133">The compression reduces the size and the number of files.</span></span>

<span data-ttu-id="8720e-134">Consulte [Descripción del valor ImageStoreConnectionString](service-fabric-image-store-connection-string.md) para más información sobre el almacén de imágenes y su cadena de conexión.</span><span class="sxs-lookup"><span data-stu-id="8720e-134">See [Understand the image store connection string](service-fabric-image-store-connection-string.md) for supplementary information about the image store and image store connection string.</span></span>

## <a name="register-the-application-package"></a><span data-ttu-id="8720e-135">Registrar el paquete de la aplicación</span><span class="sxs-lookup"><span data-stu-id="8720e-135">Register the application package</span></span>
<span data-ttu-id="8720e-136">El tipo y la versión de la aplicación declarados en el manifiesto de aplicación estarán disponibles para usarse cuando se registre el paquete de aplicación.</span><span class="sxs-lookup"><span data-stu-id="8720e-136">The application type and version declared in the application manifest become available for use when the application package is registered.</span></span> <span data-ttu-id="8720e-137">El sistema leerá el paquete cargado en el paso anterior, comprobará dicho paquete, procesará su contenido y copiará el paquete procesado en una ubicación del sistema interno.</span><span class="sxs-lookup"><span data-stu-id="8720e-137">The system reads the package uploaded in the previous step, verifies the package, processes the package contents, and copies the processed package to an internal system location.</span></span>  

<span data-ttu-id="8720e-138">La API [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) registra el tipo de aplicación en el clúster y hace que esté disponible para su implementación.</span><span class="sxs-lookup"><span data-stu-id="8720e-138">The [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) API registers the application type in the cluster and make it available for deployment.</span></span>

<span data-ttu-id="8720e-139">La API [GetApplicationTypeListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationtypelistasync) proporciona información acerca de todos los tipos de aplicaciones registradas correctamente.</span><span class="sxs-lookup"><span data-stu-id="8720e-139">The [GetApplicationTypeListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationtypelistasync) API provides information about all successfully registered application types.</span></span> <span data-ttu-id="8720e-140">Puede usar esta API para determinar cuándo se realiza el registro.</span><span class="sxs-lookup"><span data-stu-id="8720e-140">You can use this API to determine when the registration is done.</span></span>

## <a name="create-an-application-instance"></a><span data-ttu-id="8720e-141">Creación de una instancia de aplicación</span><span class="sxs-lookup"><span data-stu-id="8720e-141">Create an application instance</span></span>
<span data-ttu-id="8720e-142">Se pueden crear instancias de una aplicación a partir de cualquier tipo de aplicación que se haya registrado correctamente mediante la API [CreateApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.createapplicationasync).</span><span class="sxs-lookup"><span data-stu-id="8720e-142">You can instantiate an application from any application type that has been registered successfully by using the [CreateApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.createapplicationasync) API.</span></span> <span data-ttu-id="8720e-143">El nombre de cada aplicación debe empezar con el esquema *"fabric:"* y ser único para cada instancia de la aplicación (dentro de un clúster).</span><span class="sxs-lookup"><span data-stu-id="8720e-143">The name of each application must start with the *"fabric:"* scheme and must be unique for each application instance (within a cluster).</span></span> <span data-ttu-id="8720e-144">También se crean los servicios predeterminados que se hayan definido en el manifiesto de aplicación del tipo de aplicación de destino.</span><span class="sxs-lookup"><span data-stu-id="8720e-144">Any default services defined in the application manifest of the target application type are also created.</span></span>

<span data-ttu-id="8720e-145">Pueden crearse varias instancias de aplicación para cualquier versión concreta de un tipo de aplicación registrado.</span><span class="sxs-lookup"><span data-stu-id="8720e-145">Multiple application instances can be created for any given version of a registered application type.</span></span> <span data-ttu-id="8720e-146">Cada instancia de la aplicación se ejecuta de forma aislada, con su propio directorio de trabajo y conjunto de procesos.</span><span class="sxs-lookup"><span data-stu-id="8720e-146">Each application instance runs in isolation, with its own working directory and set of processes.</span></span>

<span data-ttu-id="8720e-147">Para ver qué aplicaciones y servicios con nombre se ejecutan en el clúster, ejecute las API [GetApplicationListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationlistasync) y [GetServiceListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getservicelistasync).</span><span class="sxs-lookup"><span data-stu-id="8720e-147">To see which named applications and services are running in the cluster, run the [GetApplicationListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationlistasync) and [GetServiceListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getservicelistasync) APIs.</span></span>

## <a name="create-a-service-instance"></a><span data-ttu-id="8720e-148">Creación de una instancia de servicio</span><span class="sxs-lookup"><span data-stu-id="8720e-148">Create a service instance</span></span>
<span data-ttu-id="8720e-149">Puede crear una instancia de un servicio a partir de un tipo de servicio mediante la API [CreateServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync).</span><span class="sxs-lookup"><span data-stu-id="8720e-149">You can instantiate a service from a service type using the [CreateServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) API.</span></span>  <span data-ttu-id="8720e-150">Si el servicio se declara como servicio predeterminado en el manifiesto de aplicación, se crea una instancia de este con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="8720e-150">If the service is declared as a default service in the application manifest, the service is instantiated when the application is instantiated.</span></span>  <span data-ttu-id="8720e-151">Al llamar a la API [CreateServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) en un servicio para el que ya se ha creado una instancia se devuelve una excepción de tipo FabricException que contiene un código de error con un valor de FabricErrorCode.ServiceAlreadyExists.</span><span class="sxs-lookup"><span data-stu-id="8720e-151">Calling the [CreateServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) API for a service that is already instantiated will return an exception of type FabricException containing an error code with a value of FabricErrorCode.ServiceAlreadyExists.</span></span>

## <a name="remove-a-service-instance"></a><span data-ttu-id="8720e-152">Eliminación de una instancia de servicio</span><span class="sxs-lookup"><span data-stu-id="8720e-152">Remove a service instance</span></span>
<span data-ttu-id="8720e-153">Cuando una instancia de servicio deja de ser necesaria, para quitarla de la instancia de aplicación en funcionamiento, hay que llamar a la API [DeleteServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.deleteserviceasync).</span><span class="sxs-lookup"><span data-stu-id="8720e-153">When a service instance is no longer needed, you can remove it from the running application instance by calling the [DeleteServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.deleteserviceasync) API.</span></span>  

> [!WARNING]
> <span data-ttu-id="8720e-154">Esta operación no se puede revertir y el estado del servicio no se puede recuperar.</span><span class="sxs-lookup"><span data-stu-id="8720e-154">This operation cannot be reversed, and service state cannot be recovered.</span></span>

## <a name="remove-an-application-instance"></a><span data-ttu-id="8720e-155">Eliminación de una instancia de aplicación</span><span class="sxs-lookup"><span data-stu-id="8720e-155">Remove an application instance</span></span>
<span data-ttu-id="8720e-156">Cuando una instancia de aplicación deja de ser necesaria, puede quitarla de manera permanente por el nombre mediante la API [DeleteApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.deleteapplicationasync).</span><span class="sxs-lookup"><span data-stu-id="8720e-156">When an application instance is no longer needed, you can permanently remove it by name using the [DeleteApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.deleteapplicationasync) API.</span></span> <span data-ttu-id="8720e-157">[DeleteApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.deleteapplicationasync) quita automáticamente todos los servicios que pertenecen a la aplicación, con lo que se eliminan de forma permanente todos los estados de servicio.</span><span class="sxs-lookup"><span data-stu-id="8720e-157">[DeleteApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.deleteapplicationasync) automatically removes all services that belong to the application as well, permanently removing all service state.</span></span>

> [!WARNING]
> <span data-ttu-id="8720e-158">No se puede deshacer esta operación y no se puede recuperar el estado de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="8720e-158">This operation cannot be reversed, and application state cannot be recovered.</span></span>

## <a name="unregister-an-application-type"></a><span data-ttu-id="8720e-159">Anulación de un registro del tipo de aplicación</span><span class="sxs-lookup"><span data-stu-id="8720e-159">Unregister an application type</span></span>
<span data-ttu-id="8720e-160">Cuando ya no se necesita una versión concreta de un tipo de aplicación, debe anularse el registro de esa versión en particular del tipo de aplicación mediante la API [Unregister-ServiceFabricApplicationType](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.unprovisionapplicationasync).</span><span class="sxs-lookup"><span data-stu-id="8720e-160">When a particular version of an application type is no longer needed, you should unregister that particular version of the application type using the [Unregister-ServiceFabricApplicationType](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.unprovisionapplicationasync) API.</span></span> <span data-ttu-id="8720e-161">La anulación del registro de versiones no usadas de tipos de aplicación permite liberar espacio de almacenamiento usado en el almacén de imágenes.</span><span class="sxs-lookup"><span data-stu-id="8720e-161">Unregistering unused versions of application types releases storage space used by the image store.</span></span> <span data-ttu-id="8720e-162">Se puede anular el registro de un tipo de aplicación siempre y cuando no se haya creado ninguna instancia de la aplicación con esa versión del tipo de aplicación y ninguna actualización pendiente de la aplicación haga referencia a esa versión del tipo de aplicación.</span><span class="sxs-lookup"><span data-stu-id="8720e-162">A version of an application type can be unregistered as long as no applications are instantiated against that version of the application type and no pending application upgrades are referencing that version of the application type.</span></span>

## <a name="remove-an-application-package-from-the-image-store"></a><span data-ttu-id="8720e-163">Eliminación de un paquete de aplicación del almacén de imágenes</span><span class="sxs-lookup"><span data-stu-id="8720e-163">Remove an application package from the image store</span></span>
<span data-ttu-id="8720e-164">Cuando un paquete de aplicación deje de necesitarse, puede eliminarlo del almacén de imágenes para liberar recursos del sistema mediante la API [RemoveApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.removeapplicationpackage).</span><span class="sxs-lookup"><span data-stu-id="8720e-164">When an application package is no longer needed, you can delete it from the image store to free up system resources using the [RemoveApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.removeapplicationpackage) API.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="8720e-165">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="8720e-165">Troubleshooting</span></span>
### <a name="copy-servicefabricapplicationpackage-asks-for-an-imagestoreconnectionstring"></a><span data-ttu-id="8720e-166">Copy-ServiceFabricApplicationPackage pide una ImageStoreConnectionString</span><span class="sxs-lookup"><span data-stu-id="8720e-166">Copy-ServiceFabricApplicationPackage asks for an ImageStoreConnectionString</span></span>
<span data-ttu-id="8720e-167">El entorno del SDK de Service Fabric ya debe tener configurados los valores predeterminados correctos.</span><span class="sxs-lookup"><span data-stu-id="8720e-167">The Service Fabric SDK environment should already have the correct defaults set up.</span></span> <span data-ttu-id="8720e-168">Pero si es necesario, ImageStoreConnectionString para todos los comandos debe coincidir con el valor que usa el clúster de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="8720e-168">But if needed, the ImageStoreConnectionString for all commands should match the value that the Service Fabric cluster is using.</span></span> <span data-ttu-id="8720e-169">Puede encontrar ImageStoreConnectionString en el manifiesto del clúster, recuperado mediante los comandos [Get-ServiceFabricClusterManifest](/powershell/module/servicefabric/get-servicefabricclustermanifest?view=azureservicefabricps) y Get-ImageStoreConnectionStringFromClusterManifest:</span><span class="sxs-lookup"><span data-stu-id="8720e-169">You can find the ImageStoreConnectionString in the cluster manifest, retrieved using the [Get-ServiceFabricClusterManifest](/powershell/module/servicefabric/get-servicefabricclustermanifest?view=azureservicefabricps) and Get-ImageStoreConnectionStringFromClusterManifest commands:</span></span>

```powershell
PS C:\> Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest)
```

<span data-ttu-id="8720e-170">El cmdlet **Get-ImageStoreConnectionStringFromClusterManifest** , que forma parte del módulo de PowerShell correspondiente al SDK de Service Fabric, se utiliza para obtener la cadena de conexión del almacén de imágenes.</span><span class="sxs-lookup"><span data-stu-id="8720e-170">The **Get-ImageStoreConnectionStringFromClusterManifest** cmdlet, which is part of the Service Fabric SDK PowerShell module, is used to get the image store connection string.</span></span>  <span data-ttu-id="8720e-171">Para importar el módulo de SDK, ejecute el siguiente código:</span><span class="sxs-lookup"><span data-stu-id="8720e-171">To import the SDK module, run:</span></span>

```powershell
Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
```


<span data-ttu-id="8720e-172">ImageStoreConnectionString se encuentra en el manifiesto de clúster:</span><span class="sxs-lookup"><span data-stu-id="8720e-172">The ImageStoreConnectionString is found in the cluster manifest:</span></span>

```xml
<ClusterManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Name="Server-Default-SingleNode" Version="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">

    [...]

    <Section Name="Management">
      <Parameter Name="ImageStoreConnectionString" Value="file:D:\ServiceFabric\Data\ImageStore" />
    </Section>

    [...]
```

<span data-ttu-id="8720e-173">Consulte [Descripción del valor ImageStoreConnectionString](service-fabric-image-store-connection-string.md) para más información sobre el almacén de imágenes y su cadena de conexión.</span><span class="sxs-lookup"><span data-stu-id="8720e-173">See [Understand the image store connection string](service-fabric-image-store-connection-string.md) for supplementary information about the image store and image store connection string.</span></span>

### <a name="deploy-large-application-package"></a><span data-ttu-id="8720e-174">Implementación de un paquete de aplicación grande</span><span class="sxs-lookup"><span data-stu-id="8720e-174">Deploy large application package</span></span>
<span data-ttu-id="8720e-175">Problema: la API [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) agota el tiempo de espera para un paquete de aplicación grande (del orden de GB).</span><span class="sxs-lookup"><span data-stu-id="8720e-175">Issue: [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) API times out for a large application package (order of GB).</span></span>
<span data-ttu-id="8720e-176">Pruebe lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="8720e-176">Try:</span></span>
- <span data-ttu-id="8720e-177">Especifique un tiempo de espera mayor para el método [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) con el parámetro `timeout`.</span><span class="sxs-lookup"><span data-stu-id="8720e-177">Specify a larger timeout for [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) method, with `timeout` parameter.</span></span> <span data-ttu-id="8720e-178">De forma predeterminada, el tiempo de espera es de 30 minutos.</span><span class="sxs-lookup"><span data-stu-id="8720e-178">By default, the timeout is 30 minutes.</span></span>
- <span data-ttu-id="8720e-179">Compruebe la conexión de red entre la máquina de origen y el clúster.</span><span class="sxs-lookup"><span data-stu-id="8720e-179">Check the network connection between your source machine and cluster.</span></span> <span data-ttu-id="8720e-180">Si la conexión es lenta, considere la posibilidad de usar una máquina con una conexión de red mejor.</span><span class="sxs-lookup"><span data-stu-id="8720e-180">If the connection is slow, consider using a machine with a better network connection.</span></span>
<span data-ttu-id="8720e-181">Si la máquina cliente se encuentra en otra región diferente al clúster, considere el uso de una máquina cliente que se encuentre en una región más cercana o en la misma región que el clúster.</span><span class="sxs-lookup"><span data-stu-id="8720e-181">If the client machine is in another region than the cluster, consider using a client machine in a closer or same region as the cluster.</span></span>
- <span data-ttu-id="8720e-182">Compruebe si está alcanzando la limitación externa.</span><span class="sxs-lookup"><span data-stu-id="8720e-182">Check if you are hitting external throttling.</span></span> <span data-ttu-id="8720e-183">Por ejemplo, cuando el almacén de imágenes está configurado para usar Azure Storage, se puede limitar carga.</span><span class="sxs-lookup"><span data-stu-id="8720e-183">For example, when the image store is configured to use azure storage, upload may be throttled.</span></span>

<span data-ttu-id="8720e-184">Problema: la carga del paquete se completó correctamente, pero la API [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) agota el tiempo de espera.</span><span class="sxs-lookup"><span data-stu-id="8720e-184">Issue: Upload package completed successfully, but [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) API times out.</span></span>
<span data-ttu-id="8720e-185">Pruebe lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="8720e-185">Try:</span></span>
- <span data-ttu-id="8720e-186">[Comprima el paquete](service-fabric-package-apps.md#compress-a-package) antes de realizar la copia en el almacén de imágenes.</span><span class="sxs-lookup"><span data-stu-id="8720e-186">[Compress the package](service-fabric-package-apps.md#compress-a-package) before copying to the image store.</span></span>
<span data-ttu-id="8720e-187">La compresión reduce el tamaño y el número de archivos lo que, a su vez, reduce la cantidad de tráfico y trabajo que Service Fabric debe realizar.</span><span class="sxs-lookup"><span data-stu-id="8720e-187">The compression reduces the size and the number of files, which in turn reduces the amount of traffic and work that Service Fabric must perform.</span></span> <span data-ttu-id="8720e-188">La operación de carga puede ser más lenta (especialmente si incluyen el tiempo de compresión), pero el registro y la anulación del registro del tipo de aplicación son más rápidos.</span><span class="sxs-lookup"><span data-stu-id="8720e-188">The upload operation may be slower (especially if you include the compression time), but register and un-register the application type are faster.</span></span>
- <span data-ttu-id="8720e-189">Especifique un tiempo de espera mayor para la API [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) con el parámetro `timeout`.</span><span class="sxs-lookup"><span data-stu-id="8720e-189">Specify a larger timeout for [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) API with `timeout` parameter.</span></span>

### <a name="deploy-application-package-with-many-files"></a><span data-ttu-id="8720e-190">Implementación del paquete de aplicación con muchos archivos</span><span class="sxs-lookup"><span data-stu-id="8720e-190">Deploy application package with many files</span></span>
<span data-ttu-id="8720e-191">Problema: [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) agota el tiempo de espera para un paquete de aplicación con muchos archivos (del orden de miles).</span><span class="sxs-lookup"><span data-stu-id="8720e-191">Issue: [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) times out for an application package with many files (order of thousands).</span></span>
<span data-ttu-id="8720e-192">Pruebe lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="8720e-192">Try:</span></span>
- <span data-ttu-id="8720e-193">[Comprima el paquete](service-fabric-package-apps.md#compress-a-package) antes de realizar la copia en el almacén de imágenes.</span><span class="sxs-lookup"><span data-stu-id="8720e-193">[Compress the package](service-fabric-package-apps.md#compress-a-package) before copying to the image store.</span></span> <span data-ttu-id="8720e-194">La compresión reduce el número de archivos.</span><span class="sxs-lookup"><span data-stu-id="8720e-194">The compression reduces the number of files.</span></span>
- <span data-ttu-id="8720e-195">Especifique un tiempo de espera mayor para [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) con el parámetro `timeout`.</span><span class="sxs-lookup"><span data-stu-id="8720e-195">Specify a larger timeout for [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) with `timeout` parameter.</span></span>

## <a name="code-example"></a><span data-ttu-id="8720e-196">Ejemplo de código</span><span class="sxs-lookup"><span data-stu-id="8720e-196">Code example</span></span>
<span data-ttu-id="8720e-197">En el ejemplo siguiente se copia un paquete de aplicación en el almacén de imágenes, se aprovisiona el tipo de aplicación, se crea una instancia de la aplicación, crea una instancia de servicio, se quita la instancia de la aplicación, se desaprovisiona el tipo de aplicación y se elimina el paquete de aplicación del almacén de imágenes.</span><span class="sxs-lookup"><span data-stu-id="8720e-197">The following example copies an application package to the image store, provisions the application type, creates an application instance, creates a service instance, removes the application instance, un-provisions the application type, and deletes the application package from the image store.</span></span>

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

    // Connect to the cluster.
    FabricClient fabricClient = new FabricClient(clusterConnection);

    // Copy the application package to a location in the image store
    try
    {
        fabricClient.ApplicationManager.CopyApplicationPackage(imageStoreConnectionString, packagePath, packagePathInImageStore);
        Console.WriteLine("Application package copied to {0}", packagePathInImageStore);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("Application package copy to Image Store failed: ");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Provision the application.  "MyApplicationV1" is the folder in the image store where the application package is located. 
    // The application type with name "MyApplicationType" and version "1.0.0" (both are found in the application manifest) 
    // is now registered in the cluster.            
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

    //  Create the application instance.
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

    // Create the stateless service description.  For stateful services, use a StatefulServiceDescription object.
    StatelessServiceDescription serviceDescription = new StatelessServiceDescription();
    serviceDescription.ApplicationName = new Uri(appName);
    serviceDescription.InstanceCount = 1;
    serviceDescription.PartitionSchemeDescription = new SingletonPartitionSchemeDescription();
    serviceDescription.ServiceName = new Uri(serviceName);
    serviceDescription.ServiceTypeName = serviceType;

    // Create the service instance.  If the service is declared as a default service in the ApplicationManifest.xml,
    // the service instance is already running and this call will fail.
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

    // Delete an application instance from the application type.
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

    // Un-provision the application type.
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

    // Delete the application package from a location in the image store.
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

## <a name="next-steps"></a><span data-ttu-id="8720e-198">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8720e-198">Next steps</span></span>
[<span data-ttu-id="8720e-199">Actualización de la aplicación de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="8720e-199">Service Fabric application upgrade</span></span>](service-fabric-application-upgrade.md)

[<span data-ttu-id="8720e-200">Introducción al estado de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="8720e-200">Service Fabric health introduction</span></span>](service-fabric-health-introduction.md)

[<span data-ttu-id="8720e-201">Diagnosticar y solucionar problemas de un servicio de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="8720e-201">Diagnose and troubleshoot a Service Fabric service</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[<span data-ttu-id="8720e-202">Modelar una aplicación en Service Fabric</span><span class="sxs-lookup"><span data-stu-id="8720e-202">Model an application in Service Fabric</span></span>](service-fabric-application-model.md)

<!--Link references--In actual articles, you only need a single period before the slash-->
[10]: service-fabric-application-model.md
[11]: service-fabric-application-upgrade.md
