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
# <a name="deploy-and-remove-applications-using-fabricclient"></a><span data-ttu-id="e0633-103">Implementación y eliminación de aplicaciones mediante FabricClient</span><span class="sxs-lookup"><span data-stu-id="e0633-103">Deploy and remove applications using FabricClient</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e0633-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e0633-104">PowerShell</span></span>](service-fabric-deploy-remove-applications.md)
> * [<span data-ttu-id="e0633-105">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e0633-105">Visual Studio</span></span>](service-fabric-publish-app-remote-cluster.md)
> * [<span data-ttu-id="e0633-106">API de FabricClient</span><span class="sxs-lookup"><span data-stu-id="e0633-106">FabricClient APIs</span></span>](service-fabric-deploy-remove-applications-fabricclient.md)
> 
> 

<br/>

<span data-ttu-id="e0633-107">Una vez que un [tipo de aplicación se ha empaquetado][10], está listo para la implementación en un clúster de Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="e0633-107">Once an [application type has been packaged][10], it's ready for deployment into an Azure Service Fabric cluster.</span></span> <span data-ttu-id="e0633-108">Implementación implica Hola siga tres pasos:</span><span class="sxs-lookup"><span data-stu-id="e0633-108">Deployment involves hello following three steps:</span></span>

1. <span data-ttu-id="e0633-109">Cargar el almacén de imágenes de toohello de paquete de aplicación de Hola</span><span class="sxs-lookup"><span data-stu-id="e0633-109">Upload hello application package toohello image store</span></span>
2. <span data-ttu-id="e0633-110">Registrar el tipo de aplicación Hola</span><span class="sxs-lookup"><span data-stu-id="e0633-110">Register hello application type</span></span>
3. <span data-ttu-id="e0633-111">Crear instancia de la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="e0633-111">Create hello application instance</span></span>

<span data-ttu-id="e0633-112">Después de implementa una aplicación y se ejecuta una instancia en clúster de hello, puede eliminar la instancia de la aplicación hello y su tipo de aplicación.</span><span class="sxs-lookup"><span data-stu-id="e0633-112">After an application is deployed and an instance is running in hello cluster, you can delete hello application instance and its application type.</span></span> <span data-ttu-id="e0633-113">toocompletely quitar una aplicación de clúster de hello implica Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="e0633-113">toocompletely remove an application from hello cluster involves hello following steps:</span></span>

1. <span data-ttu-id="e0633-114">Quitar (o eliminar) Hola ejecutando la instancia de la aplicación</span><span class="sxs-lookup"><span data-stu-id="e0633-114">Remove (or delete) hello running application instance</span></span>
2. <span data-ttu-id="e0633-115">Anular el registro del tipo de aplicación Hola si ya no lo necesite</span><span class="sxs-lookup"><span data-stu-id="e0633-115">Unregister hello application type if you no longer need it</span></span>
3. <span data-ttu-id="e0633-116">Quitar el paquete de aplicación Hola Hola almacén de imágenes</span><span class="sxs-lookup"><span data-stu-id="e0633-116">Remove hello application package from hello image store</span></span>

<span data-ttu-id="e0633-117">Si usa [Visual Studio para implementar y depurar aplicaciones](service-fabric-publish-app-remote-cluster.md) en el clúster de desarrollo local, todo Hola pasos anteriores se administran automáticamente a través de un script de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e0633-117">If you use [Visual Studio for deploying and debugging applications](service-fabric-publish-app-remote-cluster.md) on your local development cluster, all hello preceding steps are handled automatically through a PowerShell script.</span></span>  <span data-ttu-id="e0633-118">Este script se encuentra en hello *Scripts* carpeta de proyecto de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="e0633-118">This script is found in hello *Scripts* folder of hello application project.</span></span> <span data-ttu-id="e0633-119">Este artículo proporciona información general acerca de lo que está haciendo esa secuencia de comandos para que pueda realizar Hola mismas operaciones fuera de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e0633-119">This article provides background on what that script is doing so that you can perform hello same operations outside of Visual Studio.</span></span> 
 
## <a name="connect-toohello-cluster"></a><span data-ttu-id="e0633-120">Conectar el clúster toohello</span><span class="sxs-lookup"><span data-stu-id="e0633-120">Connect toohello cluster</span></span>
<span data-ttu-id="e0633-121">Conecta el clúster de toohello mediante la creación de un [FabricClient](/dotnet/api/system.fabric.fabricclient) instancia antes de ejecutar cualquiera de hello ejemplos de código de este artículo.</span><span class="sxs-lookup"><span data-stu-id="e0633-121">Connect toohello cluster by creating a [FabricClient](/dotnet/api/system.fabric.fabricclient) instance before you run any of hello code examples in this article.</span></span> <span data-ttu-id="e0633-122">Para obtener ejemplos de clúster de desarrollo local tooa conexión o un clúster remoto o un clúster protegido con Azure Active Directory, X509 certificados o Active Directory de Windows consulte [clúster segura de conectar tooa](service-fabric-connect-to-secure-cluster.md#connect-to-a-cluster-using-the-fabricclient-apis).</span><span class="sxs-lookup"><span data-stu-id="e0633-122">For examples of connecting tooa local development cluster or a remote cluster or cluster secured using Azure Active Directory, X509 certificates, or Windows Active Directory see [Connect tooa secure cluster](service-fabric-connect-to-secure-cluster.md#connect-to-a-cluster-using-the-fabricclient-apis).</span></span> <span data-ttu-id="e0633-123">clúster de desarrollo local en toohello tooconnect, ejecute hello siguiente:</span><span class="sxs-lookup"><span data-stu-id="e0633-123">tooconnect toohello local development cluster, run hello following:</span></span>

```csharp
// Connect toohello local cluster.
FabricClient fabricClient = new FabricClient();
```

## <a name="upload-hello-application-package"></a><span data-ttu-id="e0633-124">Cargar el paquete de aplicación Hola</span><span class="sxs-lookup"><span data-stu-id="e0633-124">Upload hello application package</span></span>
<span data-ttu-id="e0633-125">Imagine que compila y empaqueta una aplicación denominada *MyApplication* en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e0633-125">Suppose you build and package an application named *MyApplication* in Visual Studio.</span></span> <span data-ttu-id="e0633-126">De forma predeterminada, el nombre de tipo de aplicación de hello enumerado en hello ApplicationManifest.xml es "MyApplicationType".</span><span class="sxs-lookup"><span data-stu-id="e0633-126">By default, hello application type name listed in hello ApplicationManifest.xml is "MyApplicationType".</span></span>  <span data-ttu-id="e0633-127">paquete de aplicación, que contiene el manifiesto de aplicación necesarios de hello, manifiestos de servicio y los paquetes de datos/config/código, Hello se encuentra una en *C:\Users\&lt; nombre de usuario&gt;\Documents\Visual Studio 2017\Projects\ MyApplication\MyApplication\pkg\Debug*.</span><span class="sxs-lookup"><span data-stu-id="e0633-127">hello application package, which contains hello necessary application manifest, service manifests, and code/config/data packages, is located in *C:\Users\&lt;username&gt;\Documents\Visual Studio 2017\Projects\MyApplication\MyApplication\pkg\Debug*.</span></span>

<span data-ttu-id="e0633-128">Paquete de aplicación Hola cargando lo coloca en una ubicación que sea accesible para los componentes internos de Service Fabric Hola.</span><span class="sxs-lookup"><span data-stu-id="e0633-128">Uploading hello application package puts it in a location that's accessible by hello internal Service Fabric components.</span></span> <span data-ttu-id="e0633-129">Service Fabric comprueba el paquete de aplicación Hola durante el registro de Hola Hola del paquete de aplicación.</span><span class="sxs-lookup"><span data-stu-id="e0633-129">Service Fabric verifies hello application package during hello registration of hello application package.</span></span> <span data-ttu-id="e0633-130">Sin embargo, si desea tooverify Hola paquete de la aplicación localmente (es decir, antes de cargar), use hello [ServiceFabricApplicationPackage prueba](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e0633-130">However, if you want tooverify hello application package locally (i.e., before uploading), use hello [Test-ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="e0633-131">Hola [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) API carga el almacén de imágenes de clúster de toohello paquete de aplicación de Hola.</span><span class="sxs-lookup"><span data-stu-id="e0633-131">hello [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) API uploads hello application package toohello cluster image store.</span></span> 

<span data-ttu-id="e0633-132">Si el paquete de aplicación hello es grande y tiene muchos archivos, puede [comprimirlo](service-fabric-package-apps.md#compress-a-package) y cópielo toohello almacén de imágenes mediante PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e0633-132">If hello application package is large and/or has many files, you can [compress it](service-fabric-package-apps.md#compress-a-package) and copy it toohello image store using PowerShell.</span></span> <span data-ttu-id="e0633-133">compresión de Hola reduce el tamaño de Hola y el número de Hola de archivos.</span><span class="sxs-lookup"><span data-stu-id="e0633-133">hello compression reduces hello size and hello number of files.</span></span>

<span data-ttu-id="e0633-134">Vea [comprender la cadena de conexión de almacén de imágenes de hello](service-fabric-image-store-connection-string.md) para obtener información adicional sobre Hola image store e imagen almacenan la cadena de conexión.</span><span class="sxs-lookup"><span data-stu-id="e0633-134">See [Understand hello image store connection string](service-fabric-image-store-connection-string.md) for supplementary information about hello image store and image store connection string.</span></span>

## <a name="register-hello-application-package"></a><span data-ttu-id="e0633-135">Registrar el paquete de aplicación Hola</span><span class="sxs-lookup"><span data-stu-id="e0633-135">Register hello application package</span></span>
<span data-ttu-id="e0633-136">tipo de aplicación de Hola y la versión declarada en el manifiesto de aplicación Hola estén disponible para su uso cuando se registra el paquete de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="e0633-136">hello application type and version declared in hello application manifest become available for use when hello application package is registered.</span></span> <span data-ttu-id="e0633-137">sistema Hola lee el paquete de hello cargado en el paso anterior de hello, comprueba el paquete de hello, procesa el contenido del paquete hello y copia la ubicación de hello procesa paquete tooan interno del sistema.</span><span class="sxs-lookup"><span data-stu-id="e0633-137">hello system reads hello package uploaded in hello previous step, verifies hello package, processes hello package contents, and copies hello processed package tooan internal system location.</span></span>  

<span data-ttu-id="e0633-138">Hola [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) API registros Hola tipo de aplicación en clúster de Hola y hacer que esté disponible para la implementación.</span><span class="sxs-lookup"><span data-stu-id="e0633-138">hello [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) API registers hello application type in hello cluster and make it available for deployment.</span></span>

<span data-ttu-id="e0633-139">Hola [GetApplicationTypeListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationtypelistasync) API proporciona información acerca de todos los tipos de aplicación se registró correctamente.</span><span class="sxs-lookup"><span data-stu-id="e0633-139">hello [GetApplicationTypeListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationtypelistasync) API provides information about all successfully registered application types.</span></span> <span data-ttu-id="e0633-140">Puede utilizar esta API toodetermine cuando se realizó el registro de hello.</span><span class="sxs-lookup"><span data-stu-id="e0633-140">You can use this API toodetermine when hello registration is done.</span></span>

## <a name="create-an-application-instance"></a><span data-ttu-id="e0633-141">Creación de una instancia de aplicación</span><span class="sxs-lookup"><span data-stu-id="e0633-141">Create an application instance</span></span>
<span data-ttu-id="e0633-142">Puede crear una instancia de una aplicación de cualquier tipo de aplicación que se ha registrado correctamente mediante el uso de hello [CreateApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.createapplicationasync) API.</span><span class="sxs-lookup"><span data-stu-id="e0633-142">You can instantiate an application from any application type that has been registered successfully by using hello [CreateApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.createapplicationasync) API.</span></span> <span data-ttu-id="e0633-143">Hola de cada aplicación debe empezar con hello *"fabric:"* esquema y debe ser único para cada instancia de la aplicación (dentro de un clúster).</span><span class="sxs-lookup"><span data-stu-id="e0633-143">hello name of each application must start with hello *"fabric:"* scheme and must be unique for each application instance (within a cluster).</span></span> <span data-ttu-id="e0633-144">También se crean los servicios de valor predeterminado definidos en el manifiesto de aplicación Hola del tipo de aplicación de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="e0633-144">Any default services defined in hello application manifest of hello target application type are also created.</span></span>

<span data-ttu-id="e0633-145">Pueden crearse varias instancias de aplicación para cualquier versión concreta de un tipo de aplicación registrado.</span><span class="sxs-lookup"><span data-stu-id="e0633-145">Multiple application instances can be created for any given version of a registered application type.</span></span> <span data-ttu-id="e0633-146">Cada instancia de la aplicación se ejecuta de forma aislada, con su propio directorio de trabajo y conjunto de procesos.</span><span class="sxs-lookup"><span data-stu-id="e0633-146">Each application instance runs in isolation, with its own working directory and set of processes.</span></span>

<span data-ttu-id="e0633-147">toosee que el nombre de las aplicaciones y servicios se ejecutan en el clúster de hello, ejecute hello [GetApplicationListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationlistasync) y [GetServiceListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getservicelistasync) API.</span><span class="sxs-lookup"><span data-stu-id="e0633-147">toosee which named applications and services are running in hello cluster, run hello [GetApplicationListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationlistasync) and [GetServiceListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getservicelistasync) APIs.</span></span>

## <a name="create-a-service-instance"></a><span data-ttu-id="e0633-148">Creación de una instancia de servicio</span><span class="sxs-lookup"><span data-stu-id="e0633-148">Create a service instance</span></span>
<span data-ttu-id="e0633-149">Puede crear una instancia de un servicio de un tipo de servicio con hello [CreateServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) API.</span><span class="sxs-lookup"><span data-stu-id="e0633-149">You can instantiate a service from a service type using hello [CreateServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) API.</span></span>  <span data-ttu-id="e0633-150">Si el servicio de Hola se declara como un servicio de forma predeterminada en el manifiesto de aplicación Hola, servicio de Hola se crea una instancia cuando se crea una instancia de aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="e0633-150">If hello service is declared as a default service in hello application manifest, hello service is instantiated when hello application is instantiated.</span></span>  <span data-ttu-id="e0633-151">Llamar a hello [CreateServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) API para un servicio que ya se ha creado una instancia devolverá una excepción de tipo FabricException que contiene un código de error con un valor de FabricErrorCode.ServiceAlreadyExists.</span><span class="sxs-lookup"><span data-stu-id="e0633-151">Calling hello [CreateServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) API for a service that is already instantiated will return an exception of type FabricException containing an error code with a value of FabricErrorCode.ServiceAlreadyExists.</span></span>

## <a name="remove-a-service-instance"></a><span data-ttu-id="e0633-152">Eliminación de una instancia de servicio</span><span class="sxs-lookup"><span data-stu-id="e0633-152">Remove a service instance</span></span>
<span data-ttu-id="e0633-153">Cuando ya no se necesita una instancia de servicio, puede quitarlo de hello ejecuta instancia de la aplicación que realiza la llamada hello [DeleteServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.deleteserviceasync) API.</span><span class="sxs-lookup"><span data-stu-id="e0633-153">When a service instance is no longer needed, you can remove it from hello running application instance by calling hello [DeleteServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.deleteserviceasync) API.</span></span>  

> [!WARNING]
> <span data-ttu-id="e0633-154">Esta operación no se puede revertir y el estado del servicio no se puede recuperar.</span><span class="sxs-lookup"><span data-stu-id="e0633-154">This operation cannot be reversed, and service state cannot be recovered.</span></span>

## <a name="remove-an-application-instance"></a><span data-ttu-id="e0633-155">Eliminación de una instancia de aplicación</span><span class="sxs-lookup"><span data-stu-id="e0633-155">Remove an application instance</span></span>
<span data-ttu-id="e0633-156">Cuando ya no se necesita una instancia de la aplicación, permanentemente puede quitar por nombre usando hello [DeleteApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.deleteapplicationasync) API.</span><span class="sxs-lookup"><span data-stu-id="e0633-156">When an application instance is no longer needed, you can permanently remove it by name using hello [DeleteApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.deleteapplicationasync) API.</span></span> <span data-ttu-id="e0633-157">[DeleteApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.deleteapplicationasync) quita automáticamente todos los servicios que pertenecen, así, permanentemente quitar todo el estado de servicio de aplicación de toohello.</span><span class="sxs-lookup"><span data-stu-id="e0633-157">[DeleteApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.deleteapplicationasync) automatically removes all services that belong toohello application as well, permanently removing all service state.</span></span>

> [!WARNING]
> <span data-ttu-id="e0633-158">No se puede deshacer esta operación y no se puede recuperar el estado de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e0633-158">This operation cannot be reversed, and application state cannot be recovered.</span></span>

## <a name="unregister-an-application-type"></a><span data-ttu-id="e0633-159">Anulación de un registro del tipo de aplicación</span><span class="sxs-lookup"><span data-stu-id="e0633-159">Unregister an application type</span></span>
<span data-ttu-id="e0633-160">Cuando ya no se necesita una versión concreta de un tipo de aplicación, debe anular el registro de una versión concreta del tipo de aplicación Hola con hello [Unregister-ServiceFabricApplicationType](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.unprovisionapplicationasync) API.</span><span class="sxs-lookup"><span data-stu-id="e0633-160">When a particular version of an application type is no longer needed, you should unregister that particular version of hello application type using hello [Unregister-ServiceFabricApplicationType](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.unprovisionapplicationasync) API.</span></span> <span data-ttu-id="e0633-161">Versiones sin usar al anular el registro aplicación tipos versiones de espacio de almacenamiento utilizado por el almacén de imágenes de Hola.</span><span class="sxs-lookup"><span data-stu-id="e0633-161">Unregistering unused versions of application types releases storage space used by hello image store.</span></span> <span data-ttu-id="e0633-162">Se puede anular una versión de un tipo de aplicación siempre y cuando ninguna de las aplicaciones se crean instancias en esa versión del tipo de aplicación hello y ninguna actualización pendiente aplicación hacen referencia a esa versión del tipo de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="e0633-162">A version of an application type can be unregistered as long as no applications are instantiated against that version of hello application type and no pending application upgrades are referencing that version of hello application type.</span></span>

## <a name="remove-an-application-package-from-hello-image-store"></a><span data-ttu-id="e0633-163">Quitar un paquete de aplicación Hola almacén de imágenes</span><span class="sxs-lookup"><span data-stu-id="e0633-163">Remove an application package from hello image store</span></span>
<span data-ttu-id="e0633-164">Cuando ya no se necesita un paquete de aplicación, puede eliminarla del Hola imagen almacén toofree los recursos del sistema mediante hello [RemoveApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.removeapplicationpackage) API.</span><span class="sxs-lookup"><span data-stu-id="e0633-164">When an application package is no longer needed, you can delete it from hello image store toofree up system resources using hello [RemoveApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.removeapplicationpackage) API.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="e0633-165">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="e0633-165">Troubleshooting</span></span>
### <a name="copy-servicefabricapplicationpackage-asks-for-an-imagestoreconnectionstring"></a><span data-ttu-id="e0633-166">Copy-ServiceFabricApplicationPackage pide una ImageStoreConnectionString</span><span class="sxs-lookup"><span data-stu-id="e0633-166">Copy-ServiceFabricApplicationPackage asks for an ImageStoreConnectionString</span></span>
<span data-ttu-id="e0633-167">entorno de SDK del servicio Fabric Hola ya debe tener Hola correcto de configurar los valores predeterminados.</span><span class="sxs-lookup"><span data-stu-id="e0633-167">hello Service Fabric SDK environment should already have hello correct defaults set up.</span></span> <span data-ttu-id="e0633-168">Pero si es necesario, debe coincidir con el valor de Hola Hola ImageStoreConnectionString para todos los comandos que Hola tejido de servicio de clúster.</span><span class="sxs-lookup"><span data-stu-id="e0633-168">But if needed, hello ImageStoreConnectionString for all commands should match hello value that hello Service Fabric cluster is using.</span></span> <span data-ttu-id="e0633-169">Puede encontrar Hola ImageStoreConnectionString en el manifiesto de clúster de hello, recuperar con hello [Get-ServiceFabricClusterManifest](/powershell/module/servicefabric/get-servicefabricclustermanifest?view=azureservicefabricps) y comandos de Get-ImageStoreConnectionStringFromClusterManifest:</span><span class="sxs-lookup"><span data-stu-id="e0633-169">You can find hello ImageStoreConnectionString in hello cluster manifest, retrieved using hello [Get-ServiceFabricClusterManifest](/powershell/module/servicefabric/get-servicefabricclustermanifest?view=azureservicefabricps) and Get-ImageStoreConnectionStringFromClusterManifest commands:</span></span>

```powershell
PS C:\> Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest)
```

<span data-ttu-id="e0633-170">Hola **ImageStoreConnectionStringFromClusterManifest Get** cmdlet, que forma parte del módulo de PowerShell de SDK de tejido de servicio de hello, es la imagen de Hola de tooget usado almacenar la cadena de conexión.</span><span class="sxs-lookup"><span data-stu-id="e0633-170">hello **Get-ImageStoreConnectionStringFromClusterManifest** cmdlet, which is part of hello Service Fabric SDK PowerShell module, is used tooget hello image store connection string.</span></span>  <span data-ttu-id="e0633-171">módulo tooimport Hola SDK, ejecute:</span><span class="sxs-lookup"><span data-stu-id="e0633-171">tooimport hello SDK module, run:</span></span>

```powershell
Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
```


<span data-ttu-id="e0633-172">Hola ImageStoreConnectionString se encuentra en el manifiesto de clúster de hello:</span><span class="sxs-lookup"><span data-stu-id="e0633-172">hello ImageStoreConnectionString is found in hello cluster manifest:</span></span>

```xml
<ClusterManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Name="Server-Default-SingleNode" Version="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">

    [...]

    <Section Name="Management">
      <Parameter Name="ImageStoreConnectionString" Value="file:D:\ServiceFabric\Data\ImageStore" />
    </Section>

    [...]
```

<span data-ttu-id="e0633-173">Vea [comprender la cadena de conexión de almacén de imágenes de hello](service-fabric-image-store-connection-string.md) para obtener información adicional sobre Hola image store e imagen almacenan la cadena de conexión.</span><span class="sxs-lookup"><span data-stu-id="e0633-173">See [Understand hello image store connection string](service-fabric-image-store-connection-string.md) for supplementary information about hello image store and image store connection string.</span></span>

### <a name="deploy-large-application-package"></a><span data-ttu-id="e0633-174">Implementación de un paquete de aplicación grande</span><span class="sxs-lookup"><span data-stu-id="e0633-174">Deploy large application package</span></span>
<span data-ttu-id="e0633-175">Problema: la API [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) agota el tiempo de espera para un paquete de aplicación grande (del orden de GB).</span><span class="sxs-lookup"><span data-stu-id="e0633-175">Issue: [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) API times out for a large application package (order of GB).</span></span>
<span data-ttu-id="e0633-176">Pruebe lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="e0633-176">Try:</span></span>
- <span data-ttu-id="e0633-177">Especifique un tiempo de espera mayor para el método [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) con el parámetro `timeout`.</span><span class="sxs-lookup"><span data-stu-id="e0633-177">Specify a larger timeout for [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) method, with `timeout` parameter.</span></span> <span data-ttu-id="e0633-178">De forma predeterminada, el tiempo de espera de hello es de 30 minutos.</span><span class="sxs-lookup"><span data-stu-id="e0633-178">By default, hello timeout is 30 minutes.</span></span>
- <span data-ttu-id="e0633-179">Compruebe la conexión de red de hello entre la máquina de origen y el clúster.</span><span class="sxs-lookup"><span data-stu-id="e0633-179">Check hello network connection between your source machine and cluster.</span></span> <span data-ttu-id="e0633-180">Si Hola conexión es lenta, considere la posibilidad de usar una máquina con una conexión de red mejor.</span><span class="sxs-lookup"><span data-stu-id="e0633-180">If hello connection is slow, consider using a machine with a better network connection.</span></span>
<span data-ttu-id="e0633-181">Si es equipo del cliente de hello en otra región de clúster de hello, considere la posibilidad de mediante un equipo cliente en una región más cerca o mismo como clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="e0633-181">If hello client machine is in another region than hello cluster, consider using a client machine in a closer or same region as hello cluster.</span></span>
- <span data-ttu-id="e0633-182">Compruebe si está alcanzando la limitación externa.</span><span class="sxs-lookup"><span data-stu-id="e0633-182">Check if you are hitting external throttling.</span></span> <span data-ttu-id="e0633-183">Por ejemplo, al almacén de imágenes de hello es almacenamiento configurado toouse de azure, se puede limitar carga.</span><span class="sxs-lookup"><span data-stu-id="e0633-183">For example, when hello image store is configured toouse azure storage, upload may be throttled.</span></span>

<span data-ttu-id="e0633-184">Problema: la carga del paquete se completó correctamente, pero la API [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) agota el tiempo de espera. Pruebe lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="e0633-184">Issue: Upload package completed successfully, but [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) API times out. Try:</span></span>
- <span data-ttu-id="e0633-185">[Comprimir el paquete de hello](service-fabric-package-apps.md#compress-a-package) antes de copiar el almacén de imágenes de toohello.</span><span class="sxs-lookup"><span data-stu-id="e0633-185">[Compress hello package](service-fabric-package-apps.md#compress-a-package) before copying toohello image store.</span></span>
<span data-ttu-id="e0633-186">compresión Hola reduce el tamaño de Hola y número de Hola de archivos, que a su vez, reduce la cantidad de Hola de tráfico y funcionar a ese Service Fabric debe realizar.</span><span class="sxs-lookup"><span data-stu-id="e0633-186">hello compression reduces hello size and hello number of files, which in turn reduces hello amount of traffic and work that Service Fabric must perform.</span></span> <span data-ttu-id="e0633-187">operación de carga de Hello puede ser más lento (sobre todo si se incluye el tiempo de compresión de hello), pero el tipo de aplicación Hola registrar y anular el registro son más rápidos.</span><span class="sxs-lookup"><span data-stu-id="e0633-187">hello upload operation may be slower (especially if you include hello compression time), but register and un-register hello application type are faster.</span></span>
- <span data-ttu-id="e0633-188">Especifique un tiempo de espera mayor para la API [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) con el parámetro `timeout`.</span><span class="sxs-lookup"><span data-stu-id="e0633-188">Specify a larger timeout for [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) API with `timeout` parameter.</span></span>

### <a name="deploy-application-package-with-many-files"></a><span data-ttu-id="e0633-189">Implementación del paquete de aplicación con muchos archivos</span><span class="sxs-lookup"><span data-stu-id="e0633-189">Deploy application package with many files</span></span>
<span data-ttu-id="e0633-190">Problema: [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) agota el tiempo de espera para un paquete de aplicación con muchos archivos (del orden de miles).</span><span class="sxs-lookup"><span data-stu-id="e0633-190">Issue: [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) times out for an application package with many files (order of thousands).</span></span>
<span data-ttu-id="e0633-191">Pruebe lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="e0633-191">Try:</span></span>
- <span data-ttu-id="e0633-192">[Comprimir el paquete de hello](service-fabric-package-apps.md#compress-a-package) antes de copiar el almacén de imágenes de toohello.</span><span class="sxs-lookup"><span data-stu-id="e0633-192">[Compress hello package](service-fabric-package-apps.md#compress-a-package) before copying toohello image store.</span></span> <span data-ttu-id="e0633-193">compresión de Hello reduce el número Hola de archivos.</span><span class="sxs-lookup"><span data-stu-id="e0633-193">hello compression reduces hello number of files.</span></span>
- <span data-ttu-id="e0633-194">Especifique un tiempo de espera mayor para [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) con el parámetro `timeout`.</span><span class="sxs-lookup"><span data-stu-id="e0633-194">Specify a larger timeout for [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) with `timeout` parameter.</span></span>

## <a name="code-example"></a><span data-ttu-id="e0633-195">Ejemplo de código</span><span class="sxs-lookup"><span data-stu-id="e0633-195">Code example</span></span>
<span data-ttu-id="e0633-196">Hello en el ejemplo siguiente se copia un almacén de imágenes de toohello de paquete de aplicación, aprovisiona el tipo de aplicación Hola, crea una instancia de la aplicación, crea una instancia de servicio, instancia de la aplicación hello quita, aprovisiona un tipo de aplicación Hola, y Elimina el paquete de aplicación Hola Hola almacén de imágenes.</span><span class="sxs-lookup"><span data-stu-id="e0633-196">hello following example copies an application package toohello image store, provisions hello application type, creates an application instance, creates a service instance, removes hello application instance, un-provisions hello application type, and deletes hello application package from hello image store.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="e0633-197">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e0633-197">Next steps</span></span>
[<span data-ttu-id="e0633-198">Actualización de la aplicación de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="e0633-198">Service Fabric application upgrade</span></span>](service-fabric-application-upgrade.md)

[<span data-ttu-id="e0633-199">Introducción al estado de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="e0633-199">Service Fabric health introduction</span></span>](service-fabric-health-introduction.md)

[<span data-ttu-id="e0633-200">Diagnosticar y solucionar problemas de un servicio de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="e0633-200">Diagnose and troubleshoot a Service Fabric service</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[<span data-ttu-id="e0633-201">Modelar una aplicación en Service Fabric</span><span class="sxs-lookup"><span data-stu-id="e0633-201">Model an application in Service Fabric</span></span>](service-fabric-application-model.md)

<!--Link references--In actual articles, you only need a single period before hello slash-->
[10]: service-fabric-application-model.md
[11]: service-fabric-application-upgrade.md
