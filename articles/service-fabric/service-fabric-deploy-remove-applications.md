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
# <a name="deploy-and-remove-applications-using-powershell"></a><span data-ttu-id="e49f7-103">Implementación y eliminación de aplicaciones con PowerShell</span><span class="sxs-lookup"><span data-stu-id="e49f7-103">Deploy and remove applications using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e49f7-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e49f7-104">PowerShell</span></span>](service-fabric-deploy-remove-applications.md)
> * [<span data-ttu-id="e49f7-105">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e49f7-105">Visual Studio</span></span>](service-fabric-publish-app-remote-cluster.md)
> * [<span data-ttu-id="e49f7-106">API de FabricClient</span><span class="sxs-lookup"><span data-stu-id="e49f7-106">FabricClient APIs</span></span>](service-fabric-deploy-remove-applications-fabricclient.md)
> 
> 

<br/>

<span data-ttu-id="e49f7-107">Una vez que un [tipo de aplicación se ha empaquetado][10], está listo para la implementación en un clúster de Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="e49f7-107">Once an [application type has been packaged][10], it's ready for deployment into an Azure Service Fabric cluster.</span></span> <span data-ttu-id="e49f7-108">Implementación implica Hola siga tres pasos:</span><span class="sxs-lookup"><span data-stu-id="e49f7-108">Deployment involves hello following three steps:</span></span>

1. <span data-ttu-id="e49f7-109">Cargar el almacén de imágenes de toohello de paquete de aplicación de Hola</span><span class="sxs-lookup"><span data-stu-id="e49f7-109">Upload hello application package toohello image store</span></span>
2. <span data-ttu-id="e49f7-110">Registrar el tipo de aplicación Hola</span><span class="sxs-lookup"><span data-stu-id="e49f7-110">Register hello application type</span></span>
3. <span data-ttu-id="e49f7-111">Crear instancia de la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="e49f7-111">Create hello application instance</span></span>

<span data-ttu-id="e49f7-112">Después de implementa una aplicación y se ejecuta una instancia en clúster de hello, puede eliminar la instancia de la aplicación hello y su tipo de aplicación.</span><span class="sxs-lookup"><span data-stu-id="e49f7-112">After an application is deployed and an instance is running in hello cluster, you can delete hello application instance and its application type.</span></span> <span data-ttu-id="e49f7-113">toocompletely quitar una aplicación de clúster de hello implica Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="e49f7-113">toocompletely remove an application from hello cluster involves hello following steps:</span></span>

1. <span data-ttu-id="e49f7-114">Quitar (o eliminar) Hola ejecutando la instancia de la aplicación</span><span class="sxs-lookup"><span data-stu-id="e49f7-114">Remove (or delete) hello running application instance</span></span>
2. <span data-ttu-id="e49f7-115">Anular el registro del tipo de aplicación Hola si ya no lo necesite</span><span class="sxs-lookup"><span data-stu-id="e49f7-115">Unregister hello application type if you no longer need it</span></span>
3. <span data-ttu-id="e49f7-116">Quitar el paquete de aplicación Hola Hola almacén de imágenes</span><span class="sxs-lookup"><span data-stu-id="e49f7-116">Remove hello application package from hello image store</span></span>

<span data-ttu-id="e49f7-117">Si usa [Visual Studio para implementar y depurar aplicaciones](service-fabric-publish-app-remote-cluster.md) en el clúster de desarrollo local, todo Hola pasos anteriores se administran automáticamente a través de un script de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e49f7-117">If you use [Visual Studio for deploying and debugging applications](service-fabric-publish-app-remote-cluster.md) on your local development cluster, all hello preceding steps are handled automatically through a PowerShell script.</span></span>  <span data-ttu-id="e49f7-118">Este script se encuentra en hello *Scripts* carpeta de proyecto de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="e49f7-118">This script is found in hello *Scripts* folder of hello application project.</span></span> <span data-ttu-id="e49f7-119">Este artículo proporciona información general acerca de lo que está haciendo esa secuencia de comandos para que pueda realizar Hola mismas operaciones fuera de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e49f7-119">This article provides background on what that script is doing so that you can perform hello same operations outside of Visual Studio.</span></span> 
 
## <a name="connect-toohello-cluster"></a><span data-ttu-id="e49f7-120">Conectar el clúster toohello</span><span class="sxs-lookup"><span data-stu-id="e49f7-120">Connect toohello cluster</span></span>
<span data-ttu-id="e49f7-121">Antes de ejecutar los comandos de PowerShell en este artículo, siempre se inicie mediante [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) clúster de Service Fabric toohello tooconnect.</span><span class="sxs-lookup"><span data-stu-id="e49f7-121">Before you run any PowerShell commands in this article, always start by using [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) tooconnect toohello Service Fabric cluster.</span></span> <span data-ttu-id="e49f7-122">clúster de desarrollo local en toohello tooconnect, ejecute hello siguiente:</span><span class="sxs-lookup"><span data-stu-id="e49f7-122">tooconnect toohello local development cluster, run hello following:</span></span>

```powershell
PS C:\>Connect-ServiceFabricCluster
```

<span data-ttu-id="e49f7-123">Para obtener ejemplos de conexión clúster remoto tooa o protegidos con Azure Active Directory, X509 certificados o Active Directory de Windows consulte [clúster segura de conectar tooa](service-fabric-connect-to-secure-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="e49f7-123">For examples of connecting tooa remote cluster or cluster secured using Azure Active Directory, X509 certificates, or Windows Active Directory see [Connect tooa secure cluster](service-fabric-connect-to-secure-cluster.md).</span></span>

## <a name="upload-hello-application-package"></a><span data-ttu-id="e49f7-124">Cargar el paquete de aplicación Hola</span><span class="sxs-lookup"><span data-stu-id="e49f7-124">Upload hello application package</span></span>
<span data-ttu-id="e49f7-125">Paquete de aplicación Hola cargando lo coloca en una ubicación que sea accesible para los componentes internos de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="e49f7-125">Uploading hello application package puts it in a location that's accessible by internal Service Fabric components.</span></span>
<span data-ttu-id="e49f7-126">Si desea que el paquete de aplicación de Hola de tooverify localmente, use hello [ServiceFabricApplicationPackage prueba](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e49f7-126">If you want tooverify hello application package locally, use hello [Test-ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="e49f7-127">Hola [ServiceFabricApplicationPackage copia](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) comando cargas Hola almacén de imágenes de clúster de toohello de paquete de aplicación.</span><span class="sxs-lookup"><span data-stu-id="e49f7-127">hello [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) command uploads hello application package toohello cluster image store.</span></span>
<span data-ttu-id="e49f7-128">Hola **ImageStoreConnectionStringFromClusterManifest Get** cmdlet, que forma parte del módulo de PowerShell de SDK de tejido de servicio de hello, es la imagen de Hola de tooget usado almacenar la cadena de conexión.</span><span class="sxs-lookup"><span data-stu-id="e49f7-128">hello **Get-ImageStoreConnectionStringFromClusterManifest** cmdlet, which is part of hello Service Fabric SDK PowerShell module, is used tooget hello image store connection string.</span></span>  <span data-ttu-id="e49f7-129">módulo tooimport Hola SDK, ejecute:</span><span class="sxs-lookup"><span data-stu-id="e49f7-129">tooimport hello SDK module, run:</span></span>

```powershell
Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
```

<span data-ttu-id="e49f7-130">Imagine que compila y empaqueta una aplicación denominada *MyApplication* en Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="e49f7-130">Suppose you build and package an application named *MyApplication* in Visual Studio 2015.</span></span> <span data-ttu-id="e49f7-131">De forma predeterminada, el nombre de tipo de aplicación de hello enumerado en hello ApplicationManifest.xml es "MyApplicationType".</span><span class="sxs-lookup"><span data-stu-id="e49f7-131">By default, hello application type name listed in hello ApplicationManifest.xml is "MyApplicationType".</span></span>  <span data-ttu-id="e49f7-132">paquete de aplicación, que contiene el manifiesto de aplicación necesarios de hello, manifiestos de servicio y los paquetes de datos/config/código, Hello se encuentra una en *C:\Users\<nombre de usuario\>\Documents\Visual Studio 2015\Projects\ MyApplication\MyApplication\pkg\Debug*.</span><span class="sxs-lookup"><span data-stu-id="e49f7-132">hello application package, which contains hello necessary application manifest, service manifests, and code/config/data packages, is located in *C:\Users\<username\>\Documents\Visual Studio 2015\Projects\MyApplication\MyApplication\pkg\Debug*.</span></span> 

<span data-ttu-id="e49f7-133">Hello comando siguiente muestra contenido Hola Hola del paquete de aplicación:</span><span class="sxs-lookup"><span data-stu-id="e49f7-133">hello following command lists hello contents of hello application package:</span></span>

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

<span data-ttu-id="e49f7-134">Si el paquete de aplicación hello es grande y tiene muchos archivos, puede [comprimirlo](service-fabric-package-apps.md#compress-a-package).</span><span class="sxs-lookup"><span data-stu-id="e49f7-134">If hello application package is large and/or has many files, you can [compress it](service-fabric-package-apps.md#compress-a-package).</span></span> <span data-ttu-id="e49f7-135">compresión de Hola reduce el tamaño de Hola y el número de Hola de archivos.</span><span class="sxs-lookup"><span data-stu-id="e49f7-135">hello compression reduces hello size and hello number of files.</span></span>
<span data-ttu-id="e49f7-136">Hello inconveniente es que hello registro y anulación del registro tipo de aplicación son más rápidos.</span><span class="sxs-lookup"><span data-stu-id="e49f7-136">hello side effect is that registering and un-registering hello application type are faster.</span></span> <span data-ttu-id="e49f7-137">Tiempo de carga puede ser más lento en la actualidad, sobre todo si incluyen paquetes de saludo tiempo toocompress Hola.</span><span class="sxs-lookup"><span data-stu-id="e49f7-137">Upload time may be slower currently, especially if you include hello time toocompress hello package.</span></span> 

<span data-ttu-id="e49f7-138">toocompress un paquete, utilice Hola mismo [ServiceFabricApplicationPackage copia](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) comando.</span><span class="sxs-lookup"><span data-stu-id="e49f7-138">toocompress a package, use hello same [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) command.</span></span> <span data-ttu-id="e49f7-139">La compresión puede hacerse independiente de carga, mediante el uso de hello `SkipCopy` marcar o junto con hello la operación de carga.</span><span class="sxs-lookup"><span data-stu-id="e49f7-139">Compression can be done separate from upload, by using hello `SkipCopy` flag, or together with hello upload operation.</span></span> <span data-ttu-id="e49f7-140">Comprimir un paquete comprimido es una operación inútil.</span><span class="sxs-lookup"><span data-stu-id="e49f7-140">Applying compression on a compressed package is no-op.</span></span>
<span data-ttu-id="e49f7-141">toouncompress un paquete comprimido, utilice Hola mismo [copia ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) comando con hello `UncompressPackage` cambiar.</span><span class="sxs-lookup"><span data-stu-id="e49f7-141">toouncompress a compressed package, use hello same [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) command with hello `UncompressPackage` switch.</span></span>

<span data-ttu-id="e49f7-142">Hello siguiente cmdlet comprime paquete Hola sin copiar toohello almacén de imágenes.</span><span class="sxs-lookup"><span data-stu-id="e49f7-142">hello following cmdlet compresses hello package without copying it toohello image store.</span></span> <span data-ttu-id="e49f7-143">paquete de Hello ahora incluye archivos comprimidos para hello `Code` y `Config` paquetes.</span><span class="sxs-lookup"><span data-stu-id="e49f7-143">hello package now includes zipped files for hello `Code` and `Config` packages.</span></span> <span data-ttu-id="e49f7-144">no se comprimen aplicación Hello y manifiestos de servicio de hello, porque son necesarios para muchas operaciones internas (por ejemplo, uso compartido, extracción de nombre y la versión del tipo de aplicación para determinadas validaciones de paquete).</span><span class="sxs-lookup"><span data-stu-id="e49f7-144">hello application and hello service manifests are not zipped, because they are needed for many internal operations (like package sharing, application type name and version extraction for certain validations).</span></span> <span data-ttu-id="e49f7-145">Manifiestos de hello en zip haría que estas operaciones ineficaces.</span><span class="sxs-lookup"><span data-stu-id="e49f7-145">Zipping hello manifests would make these operations inefficient.</span></span>

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

<span data-ttu-id="e49f7-146">Para los paquetes de aplicación de gran tamaño, la compresión de hello lleva tiempo.</span><span class="sxs-lookup"><span data-stu-id="e49f7-146">For large application packages, hello compression takes time.</span></span> <span data-ttu-id="e49f7-147">Para obtener mejores resultados, use una unidad SSD rápida.</span><span class="sxs-lookup"><span data-stu-id="e49f7-147">For best results, use a fast SSD drive.</span></span> <span data-ttu-id="e49f7-148">tiempos de compresión de Hola y el tamaño de hello del paquete comprimido de hello también varían en función de contenido del paquete de saludo.</span><span class="sxs-lookup"><span data-stu-id="e49f7-148">hello compression times and hello size of hello compressed package also differ based on hello package content.</span></span>
<span data-ttu-id="e49f7-149">Por ejemplo, aquí son las estadísticas de compresión de algunos paquetes, que muestran inicial Hola y Hola a tamaño del paquete comprimido, con tiempo de compresión de Hola.</span><span class="sxs-lookup"><span data-stu-id="e49f7-149">For example, here is compression statistics for some packages, which show hello initial and hello compressed package size, with hello compression time.</span></span>

|<span data-ttu-id="e49f7-150">Tamaño inicial (MB)</span><span class="sxs-lookup"><span data-stu-id="e49f7-150">Initial size (MB)</span></span>|<span data-ttu-id="e49f7-151">Número de archivos</span><span class="sxs-lookup"><span data-stu-id="e49f7-151">File count</span></span>|<span data-ttu-id="e49f7-152">Tipos de compresión</span><span class="sxs-lookup"><span data-stu-id="e49f7-152">Compression Time</span></span>|<span data-ttu-id="e49f7-153">Tamaño de paquete comprimido (MB)</span><span class="sxs-lookup"><span data-stu-id="e49f7-153">Compressed package size (MB)</span></span>|
|----------------:|---------:|---------------:|---------------------------:|
|<span data-ttu-id="e49f7-154">100</span><span class="sxs-lookup"><span data-stu-id="e49f7-154">100</span></span>|<span data-ttu-id="e49f7-155">100</span><span class="sxs-lookup"><span data-stu-id="e49f7-155">100</span></span>|<span data-ttu-id="e49f7-156">00:00:03.3547592</span><span class="sxs-lookup"><span data-stu-id="e49f7-156">00:00:03.3547592</span></span>|<span data-ttu-id="e49f7-157">60</span><span class="sxs-lookup"><span data-stu-id="e49f7-157">60</span></span>|
|<span data-ttu-id="e49f7-158">512</span><span class="sxs-lookup"><span data-stu-id="e49f7-158">512</span></span>|<span data-ttu-id="e49f7-159">100</span><span class="sxs-lookup"><span data-stu-id="e49f7-159">100</span></span>|<span data-ttu-id="e49f7-160">00:00:16.3850303</span><span class="sxs-lookup"><span data-stu-id="e49f7-160">00:00:16.3850303</span></span>|<span data-ttu-id="e49f7-161">307</span><span class="sxs-lookup"><span data-stu-id="e49f7-161">307</span></span>|
|<span data-ttu-id="e49f7-162">1024</span><span class="sxs-lookup"><span data-stu-id="e49f7-162">1024</span></span>|<span data-ttu-id="e49f7-163">500</span><span class="sxs-lookup"><span data-stu-id="e49f7-163">500</span></span>|<span data-ttu-id="e49f7-164">00:00:32.5907950</span><span class="sxs-lookup"><span data-stu-id="e49f7-164">00:00:32.5907950</span></span>|<span data-ttu-id="e49f7-165">615</span><span class="sxs-lookup"><span data-stu-id="e49f7-165">615</span></span>|
|<span data-ttu-id="e49f7-166">2048</span><span class="sxs-lookup"><span data-stu-id="e49f7-166">2048</span></span>|<span data-ttu-id="e49f7-167">1000</span><span class="sxs-lookup"><span data-stu-id="e49f7-167">1000</span></span>|<span data-ttu-id="e49f7-168">00:01:04.3775554</span><span class="sxs-lookup"><span data-stu-id="e49f7-168">00:01:04.3775554</span></span>|<span data-ttu-id="e49f7-169">1231</span><span class="sxs-lookup"><span data-stu-id="e49f7-169">1231</span></span>|
|<span data-ttu-id="e49f7-170">5012</span><span class="sxs-lookup"><span data-stu-id="e49f7-170">5012</span></span>|<span data-ttu-id="e49f7-171">100</span><span class="sxs-lookup"><span data-stu-id="e49f7-171">100</span></span>|<span data-ttu-id="e49f7-172">00:02:45.2951288</span><span class="sxs-lookup"><span data-stu-id="e49f7-172">00:02:45.2951288</span></span>|<span data-ttu-id="e49f7-173">3074</span><span class="sxs-lookup"><span data-stu-id="e49f7-173">3074</span></span>|

<span data-ttu-id="e49f7-174">Una vez que un paquete está comprimido, puede ser tooone cargado o clústeres de varios Service Fabric según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="e49f7-174">Once a package is compressed, it can be uploaded tooone or multiple Service Fabric clusters as needed.</span></span> <span data-ttu-id="e49f7-175">mecanismo de implementación de Hello es el mismo para los paquetes comprimidos y sin comprimir.</span><span class="sxs-lookup"><span data-stu-id="e49f7-175">hello deployment mechanism is same for compressed and uncompressed packages.</span></span> <span data-ttu-id="e49f7-176">Si el paquete de saludo se comprime, se almacena como tal en el almacén de imágenes de clúster de Hola y está comprimida en el nodo de hello antes de ejecuta la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="e49f7-176">If hello package is compressed, it is stored as such in hello cluster image store and it's uncompressed on hello node before hello application is run.</span></span>


<span data-ttu-id="e49f7-177">Hello en el ejemplo siguiente se carga el almacén de imágenes de toohello de paquete de hello en una carpeta denominada "MyApplicationV1":</span><span class="sxs-lookup"><span data-stu-id="e49f7-177">hello following example uploads hello package toohello image store, into a folder named "MyApplicationV1":</span></span>

```powershell
PS C:\> Copy-ServiceFabricApplicationPackage -ApplicationPackagePath $path -ApplicationPackagePathInImageStore MyApplicationV1 -ImageStoreConnectionString (Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest)) -TimeoutSec 1800
```

<span data-ttu-id="e49f7-178">Hola **ImageStoreConnectionStringFromClusterManifest Get** cmdlet, que forma parte del módulo de PowerShell de SDK de tejido de servicio de hello, es la imagen de Hola de tooget usado almacenar la cadena de conexión.</span><span class="sxs-lookup"><span data-stu-id="e49f7-178">hello **Get-ImageStoreConnectionStringFromClusterManifest** cmdlet, which is part of hello Service Fabric SDK PowerShell module, is used tooget hello image store connection string.</span></span>  <span data-ttu-id="e49f7-179">módulo tooimport Hola SDK, ejecute:</span><span class="sxs-lookup"><span data-stu-id="e49f7-179">tooimport hello SDK module, run:</span></span>

```powershell
Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
```

<span data-ttu-id="e49f7-180">Si no se especifica hello *ApplicationPackagePathInImageStore -* parámetro, el paquete de aplicación Hola se copia en la carpeta de "Debug" hello en el almacén de imágenes de Hola.</span><span class="sxs-lookup"><span data-stu-id="e49f7-180">If you do not specify hello *-ApplicationPackagePathInImageStore* parameter, hello application package is copied into hello "Debug" folder in hello image store.</span></span>

<span data-ttu-id="e49f7-181">Hola tarda tooupload un paquete depende de varios factores.</span><span class="sxs-lookup"><span data-stu-id="e49f7-181">hello time it takes tooupload a package differs depending on multiple factors.</span></span> <span data-ttu-id="e49f7-182">Algunos de estos factores son el número de Hola de archivos de paquete de hello, tamaño de paquete de Hola y tamaños de archivo Hola.</span><span class="sxs-lookup"><span data-stu-id="e49f7-182">Some of these factors are hello number of files in hello package, hello package size, and hello file sizes.</span></span> <span data-ttu-id="e49f7-183">velocidad de la red entre la máquina de origen de Hola y clúster de Service Fabric Hola Hola también afecta al tiempo de carga de Hola.</span><span class="sxs-lookup"><span data-stu-id="e49f7-183">hello network speed between hello source machine and hello Service Fabric cluster also impacts hello upload time.</span></span> <span data-ttu-id="e49f7-184">Hola tiempo de espera predeterminado para [ServiceFabricApplicationPackage copia](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) es de 30 minutos.</span><span class="sxs-lookup"><span data-stu-id="e49f7-184">hello default timeout for [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) is 30 minutes.</span></span>
<span data-ttu-id="e49f7-185">Dependiendo de Hola factores descritos, es posible que tenga tiempo de espera de tooincrease Hola.</span><span class="sxs-lookup"><span data-stu-id="e49f7-185">Depending on hello described factors, you may have tooincrease hello timeout.</span></span> <span data-ttu-id="e49f7-186">Si va a comprimir paquete hello en llamada de copia de hello, necesita tooalso considere la posibilidad de tiempo de compresión de Hola.</span><span class="sxs-lookup"><span data-stu-id="e49f7-186">If you are compressing hello package in hello copy call, you need tooalso consider hello compression time.</span></span>

<span data-ttu-id="e49f7-187">Vea [comprender la cadena de conexión de almacén de imágenes de hello](service-fabric-image-store-connection-string.md) para obtener información adicional sobre Hola image store e imagen almacenan la cadena de conexión.</span><span class="sxs-lookup"><span data-stu-id="e49f7-187">See [Understand hello image store connection string](service-fabric-image-store-connection-string.md) for supplementary information about hello image store and image store connection string.</span></span>

## <a name="register-hello-application-package"></a><span data-ttu-id="e49f7-188">Registrar el paquete de aplicación Hola</span><span class="sxs-lookup"><span data-stu-id="e49f7-188">Register hello application package</span></span>
<span data-ttu-id="e49f7-189">tipo de aplicación de Hola y la versión declarada en el manifiesto de aplicación Hola estén disponible para su uso cuando se registra el paquete de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="e49f7-189">hello application type and version declared in hello application manifest become available for use when hello application package is registered.</span></span> <span data-ttu-id="e49f7-190">sistema Hola lee el paquete de hello cargado en el paso anterior de hello, comprueba el paquete de hello, procesa el contenido del paquete hello y copia la ubicación de hello procesa paquete tooan interno del sistema.</span><span class="sxs-lookup"><span data-stu-id="e49f7-190">hello system reads hello package uploaded in hello previous step, verifies hello package, processes hello package contents, and copies hello processed package tooan internal system location.</span></span>  

<span data-ttu-id="e49f7-191">Ejecute hello [ServiceFabricApplicationType Register](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) cmdlet tooregister Hola tipo de aplicación en clúster de Hola y ponerla a disposición de implementación:</span><span class="sxs-lookup"><span data-stu-id="e49f7-191">Run hello [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) cmdlet tooregister hello application type in hello cluster and make it available for deployment:</span></span>

```powershell
PS C:\> Register-ServiceFabricApplicationType MyApplicationV1
Register application type succeeded
```

<span data-ttu-id="e49f7-192">"MyApplicationV1" es la carpeta de hello en almacén de imágenes de Hola donde se encuentra el paquete de aplicación de Hola.</span><span class="sxs-lookup"><span data-stu-id="e49f7-192">"MyApplicationV1" is hello folder in hello image store where hello application package is located.</span></span> <span data-ttu-id="e49f7-193">tipo de aplicación Hola con nombre "MyApplicationType" y la versión "1.0.0" (ambos se encuentran en el manifiesto de aplicación Hola) ya está registrado en clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="e49f7-193">hello application type with name "MyApplicationType" and version "1.0.0" (both are found in hello application manifest) is now registered in hello cluster.</span></span>

<span data-ttu-id="e49f7-194">Hola [ServiceFabricApplicationType Register](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) comando devuelve solo después de sistema de hello tiene el paquete de aplicación Hola se registró correctamente.</span><span class="sxs-lookup"><span data-stu-id="e49f7-194">hello [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) command returns only after hello system has successfully registered hello application package.</span></span> <span data-ttu-id="e49f7-195">Cuánto tiempo toma del registro depende de tamaño de Hola y el contenido del paquete de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="e49f7-195">How long registration takes depends on hello size and contents of hello application package.</span></span> <span data-ttu-id="e49f7-196">Si es necesario, Hola **- TimeoutSec** parámetro puede ser usado toosupply un tiempo de espera (tiempo de espera de hello predeterminado es 60 segundos).</span><span class="sxs-lookup"><span data-stu-id="e49f7-196">If needed, hello **-TimeoutSec** parameter can be used toosupply a longer timeout (hello default timeout is 60 seconds).</span></span>

<span data-ttu-id="e49f7-197">Si tiene una aplicación grande del paquete o si se producen tiempos de espera, utilice hello **- Async** parámetro.</span><span class="sxs-lookup"><span data-stu-id="e49f7-197">If you have a large application package or if you are experiencing timeouts, use hello **-Async** parameter.</span></span> <span data-ttu-id="e49f7-198">comando de Hello devuelve al clúster de hello acepta comandos de registro de hello, y el procesamiento de hello continúa según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="e49f7-198">hello command returns when hello cluster accepts hello register command, and hello processing continues as needed.</span></span>
<span data-ttu-id="e49f7-199">Hola [Get ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) comando enumera todas las versiones de tipo de aplicación se registró correctamente y su estado de registro.</span><span class="sxs-lookup"><span data-stu-id="e49f7-199">hello [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) command lists all successfully registered application type versions and their registration status.</span></span> <span data-ttu-id="e49f7-200">Puede usar este comando toodetermine cuando se realizó el registro de hello.</span><span class="sxs-lookup"><span data-stu-id="e49f7-200">You can use this command toodetermine when hello registration is done.</span></span>

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

## <a name="create-hello-application"></a><span data-ttu-id="e49f7-201">Crear aplicación hello</span><span class="sxs-lookup"><span data-stu-id="e49f7-201">Create hello application</span></span>
<span data-ttu-id="e49f7-202">Puede crear una instancia de una aplicación desde cualquier versión de tipo de aplicación que se ha registrado correctamente mediante el uso de hello [ServiceFabricApplication New](/powershell/module/servicefabric/new-servicefabricapplication?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e49f7-202">You can instantiate an application from any application type version that has been registered successfully by using hello [New-ServiceFabricApplication](/powershell/module/servicefabric/new-servicefabricapplication?view=azureservicefabricps) cmdlet.</span></span> <span data-ttu-id="e49f7-203">Hola de cada aplicación debe empezar con hello *"fabric:"* esquema y debe ser único para cada instancia de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e49f7-203">hello name of each application must start with hello *"fabric:"* scheme and must be unique for each application instance.</span></span> <span data-ttu-id="e49f7-204">También se crean los servicios de valor predeterminado definidos en el manifiesto de aplicación Hola del tipo de aplicación de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="e49f7-204">Any default services defined in hello application manifest of hello target application type are also created.</span></span>

```powershell
PS C:\> New-ServiceFabricApplication fabric:/MyApp MyApplicationType 1.0.0

ApplicationName        : fabric:/MyApp
ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
ApplicationParameters  : {}
```
<span data-ttu-id="e49f7-205">Pueden crearse varias instancias de aplicación para cualquier versión concreta de un tipo de aplicación registrado.</span><span class="sxs-lookup"><span data-stu-id="e49f7-205">Multiple application instances can be created for any given version of a registered application type.</span></span> <span data-ttu-id="e49f7-206">Cada instancia de la aplicación se ejecuta de forma aislada, con su propio proceso y directorio de trabajo.</span><span class="sxs-lookup"><span data-stu-id="e49f7-206">Each application instance runs in isolation, with its own work directory and process.</span></span>

<span data-ttu-id="e49f7-207">toosee que el nombre de aplicaciones y servicios se ejecutan en el clúster hello, ejecute hello [Get ServiceFabricApplication](/powershell/servicefabric/vlatest/get-servicefabricapplication) y [ServiceFabricService Get](/powershell/module/servicefabric/get-servicefabricservice?view=azureservicefabricps) cmdlets:</span><span class="sxs-lookup"><span data-stu-id="e49f7-207">toosee which named apps and services are running in hello cluster, run hello [Get-ServiceFabricApplication](/powershell/servicefabric/vlatest/get-servicefabricapplication) and [Get-ServiceFabricService](/powershell/module/servicefabric/get-servicefabricservice?view=azureservicefabricps) cmdlets:</span></span>

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

## <a name="remove-an-application"></a><span data-ttu-id="e49f7-208">Eliminación de una aplicación</span><span class="sxs-lookup"><span data-stu-id="e49f7-208">Remove an application</span></span>
<span data-ttu-id="e49f7-209">Cuando ya no se necesita una instancia de la aplicación, permanentemente puede quitar por nombre usando hello [Remove-ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e49f7-209">When an application instance is no longer needed, you can permanently remove it by name using hello [Remove-ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) cmdlet.</span></span> <span data-ttu-id="e49f7-210">[Remove-ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) quita automáticamente todos los servicios que pertenecen, así, permanentemente quitar todo el estado de servicio de aplicación de toohello.</span><span class="sxs-lookup"><span data-stu-id="e49f7-210">[Remove-ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) automatically removes all services that belong toohello application as well, permanently removing all service state.</span></span> 

> [!WARNING]
> <span data-ttu-id="e49f7-211">No se puede deshacer esta operación y no se puede recuperar el estado de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e49f7-211">This operation cannot be reversed, and application state cannot be recovered.</span></span>

```powershell
PS C:\> Remove-ServiceFabricApplication fabric:/MyApp

Confirm
Continue with this operation?
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"):
Remove application instance succeeded

PS C:\> Get-ServiceFabricApplication
```

## <a name="unregister-an-application-type"></a><span data-ttu-id="e49f7-212">Anulación de un registro del tipo de aplicación</span><span class="sxs-lookup"><span data-stu-id="e49f7-212">Unregister an application type</span></span>
<span data-ttu-id="e49f7-213">Cuando ya no se necesita una versión concreta de un tipo de aplicación, debe anular el registro del tipo de aplicación Hola con hello [Unregister-ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e49f7-213">When a particular version of an application type is no longer needed, you should unregister hello application type using hello [Unregister-ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) cmdlet.</span></span> <span data-ttu-id="e49f7-214">Al anular el registro aplicación sin usar tipos versiones espacio de almacenamiento utilizado por el almacén de imágenes de Hola.</span><span class="sxs-lookup"><span data-stu-id="e49f7-214">Unregistering unused application types releases storage space used by hello image store.</span></span> <span data-ttu-id="e49f7-215">No se puede anular el registro de un tipo de aplicación mientras no haya ninguna aplicación con instancias con él o no haya actualizaciones de aplicaciones pendientes que hagan referencia a él.</span><span class="sxs-lookup"><span data-stu-id="e49f7-215">An application type can be unregistered as long as no applications are instantiated against it and no pending application upgrades are referencing it.</span></span>

<span data-ttu-id="e49f7-216">Ejecutar [ServiceFabricApplicationType Get](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) toosee los tipos de aplicación Hola registran actualmente en el clúster de hello:</span><span class="sxs-lookup"><span data-stu-id="e49f7-216">Run [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) toosee hello application types currently registered in hello cluster:</span></span>

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

<span data-ttu-id="e49f7-217">Ejecutar [Unregister-ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) toounregister un tipo concreto de aplicación:</span><span class="sxs-lookup"><span data-stu-id="e49f7-217">Run [Unregister-ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) toounregister a specific application type:</span></span>

```powershell
PS C:\> Unregister-ServiceFabricApplicationType MyApplicationType 1.0.0
```

## <a name="remove-an-application-package-from-hello-image-store"></a><span data-ttu-id="e49f7-218">Quitar un paquete de aplicación Hola almacén de imágenes</span><span class="sxs-lookup"><span data-stu-id="e49f7-218">Remove an application package from hello image store</span></span>
<span data-ttu-id="e49f7-219">Cuando ya no se necesita un paquete de aplicación, puede eliminarla del Hola imagen almacén toofree los recursos del sistema.</span><span class="sxs-lookup"><span data-stu-id="e49f7-219">When an application package is no longer needed, you can delete it from hello image store toofree up system resources.</span></span>

```powershell
PS C:\>Remove-ServiceFabricApplicationPackage -ApplicationPackagePathInImageStore MyApplicationV1 -ImageStoreConnectionString (Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest))
```

## <a name="troubleshooting"></a><span data-ttu-id="e49f7-220">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="e49f7-220">Troubleshooting</span></span>
### <a name="copy-servicefabricapplicationpackage-asks-for-an-imagestoreconnectionstring"></a><span data-ttu-id="e49f7-221">Copy-ServiceFabricApplicationPackage pide una ImageStoreConnectionString</span><span class="sxs-lookup"><span data-stu-id="e49f7-221">Copy-ServiceFabricApplicationPackage asks for an ImageStoreConnectionString</span></span>
<span data-ttu-id="e49f7-222">entorno de SDK del servicio Fabric Hola ya debe tener Hola correcto de configurar los valores predeterminados.</span><span class="sxs-lookup"><span data-stu-id="e49f7-222">hello Service Fabric SDK environment should already have hello correct defaults set up.</span></span> <span data-ttu-id="e49f7-223">Pero si es necesario, debe coincidir con el valor de Hola Hola ImageStoreConnectionString para todos los comandos que Hola tejido de servicio de clúster.</span><span class="sxs-lookup"><span data-stu-id="e49f7-223">But if needed, hello ImageStoreConnectionString for all commands should match hello value that hello Service Fabric cluster is using.</span></span> <span data-ttu-id="e49f7-224">Puede encontrar Hola ImageStoreConnectionString en el manifiesto de clúster de hello, recuperar con hello [Get-ServiceFabricClusterManifest](/powershell/module/servicefabric/get-servicefabricclustermanifest?view=azureservicefabricps) y comandos de Get-ImageStoreConnectionStringFromClusterManifest:</span><span class="sxs-lookup"><span data-stu-id="e49f7-224">You can find hello ImageStoreConnectionString in hello cluster manifest, retrieved using hello [Get-ServiceFabricClusterManifest](/powershell/module/servicefabric/get-servicefabricclustermanifest?view=azureservicefabricps) and Get-ImageStoreConnectionStringFromClusterManifest commands:</span></span>

```powershell
PS C:\> Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest)
```

<span data-ttu-id="e49f7-225">Hola **ImageStoreConnectionStringFromClusterManifest Get** cmdlet, que forma parte del módulo de PowerShell de SDK de tejido de servicio de hello, es la imagen de Hola de tooget usado almacenar la cadena de conexión.</span><span class="sxs-lookup"><span data-stu-id="e49f7-225">hello **Get-ImageStoreConnectionStringFromClusterManifest** cmdlet, which is part of hello Service Fabric SDK PowerShell module, is used tooget hello image store connection string.</span></span>  <span data-ttu-id="e49f7-226">módulo tooimport Hola SDK, ejecute:</span><span class="sxs-lookup"><span data-stu-id="e49f7-226">tooimport hello SDK module, run:</span></span>

```powershell
Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
```

<span data-ttu-id="e49f7-227">Hola ImageStoreConnectionString se encuentra en el manifiesto de clúster de hello:</span><span class="sxs-lookup"><span data-stu-id="e49f7-227">hello ImageStoreConnectionString is found in hello cluster manifest:</span></span>

```xml
<ClusterManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Name="Server-Default-SingleNode" Version="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">

    [...]

    <Section Name="Management">
      <Parameter Name="ImageStoreConnectionString" Value="file:D:\ServiceFabric\Data\ImageStore" />
    </Section>

    [...]
```

<span data-ttu-id="e49f7-228">Vea [comprender la cadena de conexión de almacén de imágenes de hello](service-fabric-image-store-connection-string.md) para obtener información adicional sobre Hola image store e imagen almacenan la cadena de conexión.</span><span class="sxs-lookup"><span data-stu-id="e49f7-228">See [Understand hello image store connection string](service-fabric-image-store-connection-string.md) for supplementary information about hello image store and image store connection string.</span></span>

### <a name="deploy-large-application-package"></a><span data-ttu-id="e49f7-229">Implementación de un paquete de aplicación grande</span><span class="sxs-lookup"><span data-stu-id="e49f7-229">Deploy large application package</span></span>
<span data-ttu-id="e49f7-230">Problema: [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) agota el tiempo de espera para un paquete de aplicación grande (del orden de GB).</span><span class="sxs-lookup"><span data-stu-id="e49f7-230">Issue: [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) times out for a large application package (order of GB).</span></span>
<span data-ttu-id="e49f7-231">Pruebe lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="e49f7-231">Try:</span></span>
- <span data-ttu-id="e49f7-232">Especifique un tiempo de espera mayor para el comando [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) con el parámetro `TimeoutSec`.</span><span class="sxs-lookup"><span data-stu-id="e49f7-232">Specify a larger timeout for [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) command, with `TimeoutSec` parameter.</span></span> <span data-ttu-id="e49f7-233">De forma predeterminada, el tiempo de espera de hello es de 30 minutos.</span><span class="sxs-lookup"><span data-stu-id="e49f7-233">By default, hello timeout is 30 minutes.</span></span>
- <span data-ttu-id="e49f7-234">Compruebe la conexión de red de hello entre la máquina de origen y el clúster.</span><span class="sxs-lookup"><span data-stu-id="e49f7-234">Check hello network connection between your source machine and cluster.</span></span> <span data-ttu-id="e49f7-235">Si Hola conexión es lenta, considere la posibilidad de usar una máquina con una conexión de red mejor.</span><span class="sxs-lookup"><span data-stu-id="e49f7-235">If hello connection is slow, consider using a machine with a better network connection.</span></span>
<span data-ttu-id="e49f7-236">Si es equipo del cliente de hello en otra región de clúster de hello, considere la posibilidad de mediante un equipo cliente en una región más cerca o mismo como clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="e49f7-236">If hello client machine is in another region than hello cluster, consider using a client machine in a closer or same region as hello cluster.</span></span>
- <span data-ttu-id="e49f7-237">Compruebe si está alcanzando la limitación externa.</span><span class="sxs-lookup"><span data-stu-id="e49f7-237">Check if you are hitting external throttling.</span></span> <span data-ttu-id="e49f7-238">Por ejemplo, al almacén de imágenes de hello es almacenamiento configurado toouse de azure, se puede limitar carga.</span><span class="sxs-lookup"><span data-stu-id="e49f7-238">For example, when hello image store is configured toouse azure storage, upload may be throttled.</span></span>

<span data-ttu-id="e49f7-239">Problema: La carga del paquete se completó correctamente, pero [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) agota el tiempo de espera. Pruebe lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="e49f7-239">Issue: Upload package completed successfully, but [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) times out. Try:</span></span>
- <span data-ttu-id="e49f7-240">[Comprimir el paquete de hello](service-fabric-package-apps.md#compress-a-package) antes de copiar el almacén de imágenes de toohello.</span><span class="sxs-lookup"><span data-stu-id="e49f7-240">[Compress hello package](service-fabric-package-apps.md#compress-a-package) before copying toohello image store.</span></span>
<span data-ttu-id="e49f7-241">compresión Hola reduce el tamaño de Hola y número de Hola de archivos, que a su vez, reduce la cantidad de Hola de tráfico y funcionar a ese Service Fabric debe realizar.</span><span class="sxs-lookup"><span data-stu-id="e49f7-241">hello compression reduces hello size and hello number of files, which in turn reduces hello amount of traffic and work that Service Fabric must perform.</span></span> <span data-ttu-id="e49f7-242">operación de carga de Hello puede ser más lento (sobre todo si se incluye el tiempo de compresión de hello), pero el tipo de aplicación Hola registrar y anular el registro son más rápidos.</span><span class="sxs-lookup"><span data-stu-id="e49f7-242">hello upload operation may be slower (especially if you include hello compression time), but register and un-register hello application type are faster.</span></span>
- <span data-ttu-id="e49f7-243">Especifique un tiempo de espera mayor para [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) con el parámetro `TimeoutSec`.</span><span class="sxs-lookup"><span data-stu-id="e49f7-243">Specify a larger timeout for [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) with `TimeoutSec` parameter.</span></span>
- <span data-ttu-id="e49f7-244">Especifique el modificador `Async` para [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="e49f7-244">Specify `Async` switch for [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps).</span></span> <span data-ttu-id="e49f7-245">comando de Hello devuelve al clúster Hola acepta comandos de Hola y registro de hello del tipo de aplicación Hola continúa de forma asincrónica.</span><span class="sxs-lookup"><span data-stu-id="e49f7-245">hello command returns when hello cluster accepts hello command and hello registration of hello application type continues asynchronously.</span></span> <span data-ttu-id="e49f7-246">Por este motivo, no hay ninguna necesidad de toospecify un mayor tiempo de espera en este caso.</span><span class="sxs-lookup"><span data-stu-id="e49f7-246">For this reason, there is no need toospecify a higher timeout in this case.</span></span> <span data-ttu-id="e49f7-247">Hola [Get ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) comando enumera todas las versiones de tipo de aplicación se registró correctamente y su estado de registro.</span><span class="sxs-lookup"><span data-stu-id="e49f7-247">hello [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) command lists all successfully registered application type versions and their registration status.</span></span> <span data-ttu-id="e49f7-248">Puede usar este comando toodetermine cuando se realizó el registro de hello.</span><span class="sxs-lookup"><span data-stu-id="e49f7-248">You can use this command toodetermine when hello registration is done.</span></span>

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

### <a name="deploy-application-package-with-many-files"></a><span data-ttu-id="e49f7-249">Implementación del paquete de aplicación con muchos archivos</span><span class="sxs-lookup"><span data-stu-id="e49f7-249">Deploy application package with many files</span></span>
<span data-ttu-id="e49f7-250">Problema: [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) agota el tiempo de espera para un paquete de aplicación con muchos archivos (del orden de miles).</span><span class="sxs-lookup"><span data-stu-id="e49f7-250">Issue: [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) times out for an application package with many files (order of thousands).</span></span>
<span data-ttu-id="e49f7-251">Pruebe lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="e49f7-251">Try:</span></span>
- <span data-ttu-id="e49f7-252">[Comprimir el paquete de hello](service-fabric-package-apps.md#compress-a-package) antes de copiar el almacén de imágenes de toohello.</span><span class="sxs-lookup"><span data-stu-id="e49f7-252">[Compress hello package](service-fabric-package-apps.md#compress-a-package) before copying toohello image store.</span></span> <span data-ttu-id="e49f7-253">compresión de Hello reduce el número Hola de archivos.</span><span class="sxs-lookup"><span data-stu-id="e49f7-253">hello compression reduces hello number of files.</span></span>
- <span data-ttu-id="e49f7-254">Especifique un tiempo de espera mayor para [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) con el parámetro `TimeoutSec`.</span><span class="sxs-lookup"><span data-stu-id="e49f7-254">Specify a larger timeout for [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) with `TimeoutSec` parameter.</span></span>
- <span data-ttu-id="e49f7-255">Especifique el modificador `Async` para [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="e49f7-255">Specify `Async` switch for [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps).</span></span> <span data-ttu-id="e49f7-256">comando de Hello devuelve al clúster Hola acepta comandos de Hola y registro de hello del tipo de aplicación Hola continúa de forma asincrónica.</span><span class="sxs-lookup"><span data-stu-id="e49f7-256">hello command returns when hello cluster accepts hello command and hello registration of hello application type continues asynchronously.</span></span>
<span data-ttu-id="e49f7-257">Por este motivo, no hay ninguna necesidad de toospecify un mayor tiempo de espera en este caso.</span><span class="sxs-lookup"><span data-stu-id="e49f7-257">For this reason, there is no need toospecify a higher timeout in this case.</span></span> <span data-ttu-id="e49f7-258">Hola [Get ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) comando enumera todas las versiones de tipo de aplicación se registró correctamente y su estado de registro.</span><span class="sxs-lookup"><span data-stu-id="e49f7-258">hello [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) command lists all successfully registered application type versions and their registration status.</span></span> <span data-ttu-id="e49f7-259">Puede usar este comando toodetermine cuando se realizó el registro de hello.</span><span class="sxs-lookup"><span data-stu-id="e49f7-259">You can use this command toodetermine when hello registration is done.</span></span>

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

## <a name="next-steps"></a><span data-ttu-id="e49f7-260">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e49f7-260">Next steps</span></span>
[<span data-ttu-id="e49f7-261">Actualización de la aplicación de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="e49f7-261">Service Fabric application upgrade</span></span>](service-fabric-application-upgrade.md)

[<span data-ttu-id="e49f7-262">Introducción al estado de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="e49f7-262">Service Fabric health introduction</span></span>](service-fabric-health-introduction.md)

[<span data-ttu-id="e49f7-263">Diagnosticar y solucionar problemas de un servicio de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="e49f7-263">Diagnose and troubleshoot a Service Fabric service</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[<span data-ttu-id="e49f7-264">Modelar una aplicación en Service Fabric</span><span class="sxs-lookup"><span data-stu-id="e49f7-264">Model an application in Service Fabric</span></span>](service-fabric-application-model.md)

<!--Link references--In actual articles, you only need a single period before hello slash-->
[10]: service-fabric-application-model.md
[11]: service-fabric-application-upgrade.md
