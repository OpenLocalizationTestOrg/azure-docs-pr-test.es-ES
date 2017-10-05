---
title: "Implementación de la aplicación de Azure Service Fabric | Microsoft Docs"
description: "Cómo implementar y quitar aplicaciones de Service Fabric con PowerShell."
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
ms.openlocfilehash: edef23a8cdab7fd0bef54456f0caabb9db273bf9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-and-remove-applications-using-powershell"></a><span data-ttu-id="cda19-103">Implementación y eliminación de aplicaciones con PowerShell</span><span class="sxs-lookup"><span data-stu-id="cda19-103">Deploy and remove applications using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="cda19-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="cda19-104">PowerShell</span></span>](service-fabric-deploy-remove-applications.md)
> * [<span data-ttu-id="cda19-105">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="cda19-105">Visual Studio</span></span>](service-fabric-publish-app-remote-cluster.md)
> * [<span data-ttu-id="cda19-106">API de FabricClient</span><span class="sxs-lookup"><span data-stu-id="cda19-106">FabricClient APIs</span></span>](service-fabric-deploy-remove-applications-fabricclient.md)
> 
> 

<br/>

<span data-ttu-id="cda19-107">Una vez que un [tipo de aplicación se ha empaquetado][10], está listo para la implementación en un clúster de Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="cda19-107">Once an [application type has been packaged][10], it's ready for deployment into an Azure Service Fabric cluster.</span></span> <span data-ttu-id="cda19-108">La implementación implica los tres pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="cda19-108">Deployment involves the following three steps:</span></span>

1. <span data-ttu-id="cda19-109">Carga del paquete de aplicación en el almacén de imágenes</span><span class="sxs-lookup"><span data-stu-id="cda19-109">Upload the application package to the image store</span></span>
2. <span data-ttu-id="cda19-110">Cargar el tipo de aplicación</span><span class="sxs-lookup"><span data-stu-id="cda19-110">Register the application type</span></span>
3. <span data-ttu-id="cda19-111">Crear la instancia de aplicación</span><span class="sxs-lookup"><span data-stu-id="cda19-111">Create the application instance</span></span>

<span data-ttu-id="cda19-112">Después de que se ha implementado una aplicación y una instancia está en funcionamiento en el clúster, puede eliminar la instancia de aplicación y su tipo de aplicación.</span><span class="sxs-lookup"><span data-stu-id="cda19-112">After an application is deployed and an instance is running in the cluster, you can delete the application instance and its application type.</span></span> <span data-ttu-id="cda19-113">Para quitar completamente una aplicación del clúster, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="cda19-113">To completely remove an application from the cluster involves the following steps:</span></span>

1. <span data-ttu-id="cda19-114">Quitar (o eliminar) la instancia de la aplicación en ejecución</span><span class="sxs-lookup"><span data-stu-id="cda19-114">Remove (or delete) the running application instance</span></span>
2. <span data-ttu-id="cda19-115">Anular el registro del tipo de aplicación si ya no lo necesita</span><span class="sxs-lookup"><span data-stu-id="cda19-115">Unregister the application type if you no longer need it</span></span>
3. <span data-ttu-id="cda19-116">Quitar el paquete de aplicación del almacén de imágenes</span><span class="sxs-lookup"><span data-stu-id="cda19-116">Remove the application package from the image store</span></span>

<span data-ttu-id="cda19-117">Si usa [Visual Studio para implementar y depurar aplicaciones](service-fabric-publish-app-remote-cluster.md) en el clúster de desarrollo local, todos los pasos anteriores se controlan automáticamente mediante un script de PowerShell,</span><span class="sxs-lookup"><span data-stu-id="cda19-117">If you use [Visual Studio for deploying and debugging applications](service-fabric-publish-app-remote-cluster.md) on your local development cluster, all the preceding steps are handled automatically through a PowerShell script.</span></span>  <span data-ttu-id="cda19-118">que se encuentra en la carpeta *Scripts* del proyecto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="cda19-118">This script is found in the *Scripts* folder of the application project.</span></span> <span data-ttu-id="cda19-119">En este artículo se ofrece información sobre lo que hace ese script para que pueda realizar las mismas operaciones fuera de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="cda19-119">This article provides background on what that script is doing so that you can perform the same operations outside of Visual Studio.</span></span> 
 
## <a name="connect-to-the-cluster"></a><span data-ttu-id="cda19-120">Conexión al clúster</span><span class="sxs-lookup"><span data-stu-id="cda19-120">Connect to the cluster</span></span>
<span data-ttu-id="cda19-121">Antes de ejecutar los comandos de PowerShell en este artículo, empiece siempre usando [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) para conectarse al clúster de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="cda19-121">Before you run any PowerShell commands in this article, always start by using [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) to connect to the Service Fabric cluster.</span></span> <span data-ttu-id="cda19-122">Para conectarse al clúster de desarrollo local, ejecute lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="cda19-122">To connect to the local development cluster, run the following:</span></span>

```powershell
PS C:\>Connect-ServiceFabricCluster
```

<span data-ttu-id="cda19-123">Para obtener ejemplos de conexión a un clúster remoto o protegido con Azure Active Directory, certificados X509 o Windows Active Directory, consulte [Conexión a un clúster seguro](service-fabric-connect-to-secure-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="cda19-123">For examples of connecting to a remote cluster or cluster secured using Azure Active Directory, X509 certificates, or Windows Active Directory see [Connect to a secure cluster](service-fabric-connect-to-secure-cluster.md).</span></span>

## <a name="upload-the-application-package"></a><span data-ttu-id="cda19-124">Cargar el paquete de la aplicación</span><span class="sxs-lookup"><span data-stu-id="cda19-124">Upload the application package</span></span>
<span data-ttu-id="cda19-125">Cargar el paquete de aplicación lo pone en una ubicación a la que pueden tener acceso los componentes internos de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="cda19-125">Uploading the application package puts it in a location that's accessible by internal Service Fabric components.</span></span>
<span data-ttu-id="cda19-126">Si quiere comprobar el paquete de la aplicación de forma local, use el cmdlet [Test-ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="cda19-126">If you want to verify the application package locally, use the [Test-ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="cda19-127">El comando [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) cargará el paquete de aplicación en el almacén de imágenes del clúster.</span><span class="sxs-lookup"><span data-stu-id="cda19-127">The [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) command uploads the application package to the cluster image store.</span></span>
<span data-ttu-id="cda19-128">El cmdlet **Get-ImageStoreConnectionStringFromClusterManifest** , que forma parte del módulo de PowerShell correspondiente al SDK de Service Fabric, se utiliza para obtener la cadena de conexión del almacén de imágenes.</span><span class="sxs-lookup"><span data-stu-id="cda19-128">The **Get-ImageStoreConnectionStringFromClusterManifest** cmdlet, which is part of the Service Fabric SDK PowerShell module, is used to get the image store connection string.</span></span>  <span data-ttu-id="cda19-129">Para importar el módulo de SDK, ejecute el siguiente código:</span><span class="sxs-lookup"><span data-stu-id="cda19-129">To import the SDK module, run:</span></span>

```powershell
Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
```

<span data-ttu-id="cda19-130">Imagine que compila y empaqueta una aplicación denominada *MyApplication* en Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="cda19-130">Suppose you build and package an application named *MyApplication* in Visual Studio 2015.</span></span> <span data-ttu-id="cda19-131">De forma predeterminada, el nombre del tipo de aplicación que aparece en ApplicationManifest.xml es "MyApplicationType".</span><span class="sxs-lookup"><span data-stu-id="cda19-131">By default, the application type name listed in the ApplicationManifest.xml is "MyApplicationType".</span></span>  <span data-ttu-id="cda19-132">El paquete de aplicación, que contiene el manifiesto de aplicación necesario, así como los manifiestos de servicio y los paquetes code/config/data, se encuentra en *C:\Users\<username\>\Documents\Visual Studio 2015\Projects\MyApplication\MyApplication\pkg\Debug*.</span><span class="sxs-lookup"><span data-stu-id="cda19-132">The application package, which contains the necessary application manifest, service manifests, and code/config/data packages, is located in *C:\Users\<username\>\Documents\Visual Studio 2015\Projects\MyApplication\MyApplication\pkg\Debug*.</span></span> 

<span data-ttu-id="cda19-133">En el siguiente comando se muestra el contenido del paquete de aplicación:</span><span class="sxs-lookup"><span data-stu-id="cda19-133">The following command lists the contents of the application package:</span></span>

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

<span data-ttu-id="cda19-134">Si el paquete de aplicación es grande y/o tiene muchos archivos, puede [comprimirlo](service-fabric-package-apps.md#compress-a-package).</span><span class="sxs-lookup"><span data-stu-id="cda19-134">If the application package is large and/or has many files, you can [compress it](service-fabric-package-apps.md#compress-a-package).</span></span> <span data-ttu-id="cda19-135">La compresión reduce el tamaño y el número de archivos.</span><span class="sxs-lookup"><span data-stu-id="cda19-135">The compression reduces the size and the number of files.</span></span>
<span data-ttu-id="cda19-136">El inconveniente es que el registro y la anulación del registro del tipo de aplicación son más rápidos.</span><span class="sxs-lookup"><span data-stu-id="cda19-136">The side effect is that registering and un-registering the application type are faster.</span></span> <span data-ttu-id="cda19-137">El tiempo de carga puede ser más lento en la actualidad, especialmente si incluye el tiempo para comprimir el paquete.</span><span class="sxs-lookup"><span data-stu-id="cda19-137">Upload time may be slower currently, especially if you include the time to compress the package.</span></span> 

<span data-ttu-id="cda19-138">Para comprimir un paquete, use el mismo comando [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="cda19-138">To compress a package, use the same [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) command.</span></span> <span data-ttu-id="cda19-139">La compresión puede realizarse independiente de la carga, utilizando la marca `SkipCopy`, o junto con la operación de carga.</span><span class="sxs-lookup"><span data-stu-id="cda19-139">Compression can be done separate from upload, by using the `SkipCopy` flag, or together with the upload operation.</span></span> <span data-ttu-id="cda19-140">Comprimir un paquete comprimido es una operación inútil.</span><span class="sxs-lookup"><span data-stu-id="cda19-140">Applying compression on a compressed package is no-op.</span></span>
<span data-ttu-id="cda19-141">Para descomprimir un paquete comprimido, use el mismo comando [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) con el modificador `UncompressPackage`.</span><span class="sxs-lookup"><span data-stu-id="cda19-141">To uncompress a compressed package, use the same [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) command with the `UncompressPackage` switch.</span></span>

<span data-ttu-id="cda19-142">El siguiente cmdlet comprime el paquete sin copiarlo en el almacén de imágenes.</span><span class="sxs-lookup"><span data-stu-id="cda19-142">The following cmdlet compresses the package without copying it to the image store.</span></span> <span data-ttu-id="cda19-143">El paquete ahora incluye los archivos comprimidos para los paquetes `Code` y `Config`.</span><span class="sxs-lookup"><span data-stu-id="cda19-143">The package now includes zipped files for the `Code` and `Config` packages.</span></span> <span data-ttu-id="cda19-144">La aplicación y los manifiestos de servicio no se comprimen porque son necesarios para muchas operaciones internas (por ejemplo, uso compartido de paquetes, nombre de tipo de aplicación y extracción de versiones para ciertas validaciones).</span><span class="sxs-lookup"><span data-stu-id="cda19-144">The application and the service manifests are not zipped, because they are needed for many internal operations (like package sharing, application type name and version extraction for certain validations).</span></span> <span data-ttu-id="cda19-145">La compresión de los manifiestos haría que estas operaciones resultaran ineficaces.</span><span class="sxs-lookup"><span data-stu-id="cda19-145">Zipping the manifests would make these operations inefficient.</span></span>

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

<span data-ttu-id="cda19-146">Para paquetes de aplicación de gran tamaño, la compresión lleva tiempo.</span><span class="sxs-lookup"><span data-stu-id="cda19-146">For large application packages, the compression takes time.</span></span> <span data-ttu-id="cda19-147">Para obtener mejores resultados, use una unidad SSD rápida.</span><span class="sxs-lookup"><span data-stu-id="cda19-147">For best results, use a fast SSD drive.</span></span> <span data-ttu-id="cda19-148">Los tiempos de compresión y el tamaño del paquete comprimido también varían en función del contenido del paquete.</span><span class="sxs-lookup"><span data-stu-id="cda19-148">The compression times and the size of the compressed package also differ based on the package content.</span></span>
<span data-ttu-id="cda19-149">Por ejemplo, a continuación figuran estadísticas de compresión para algunos paquetes, que muestran el tamaño de paquete inicial y comprimido, con el tiempo de compresión.</span><span class="sxs-lookup"><span data-stu-id="cda19-149">For example, here is compression statistics for some packages, which show the initial and the compressed package size, with the compression time.</span></span>

|<span data-ttu-id="cda19-150">Tamaño inicial (MB)</span><span class="sxs-lookup"><span data-stu-id="cda19-150">Initial size (MB)</span></span>|<span data-ttu-id="cda19-151">Número de archivos</span><span class="sxs-lookup"><span data-stu-id="cda19-151">File count</span></span>|<span data-ttu-id="cda19-152">Tipos de compresión</span><span class="sxs-lookup"><span data-stu-id="cda19-152">Compression Time</span></span>|<span data-ttu-id="cda19-153">Tamaño de paquete comprimido (MB)</span><span class="sxs-lookup"><span data-stu-id="cda19-153">Compressed package size (MB)</span></span>|
|----------------:|---------:|---------------:|---------------------------:|
|<span data-ttu-id="cda19-154">100</span><span class="sxs-lookup"><span data-stu-id="cda19-154">100</span></span>|<span data-ttu-id="cda19-155">100</span><span class="sxs-lookup"><span data-stu-id="cda19-155">100</span></span>|<span data-ttu-id="cda19-156">00:00:03.3547592</span><span class="sxs-lookup"><span data-stu-id="cda19-156">00:00:03.3547592</span></span>|<span data-ttu-id="cda19-157">60</span><span class="sxs-lookup"><span data-stu-id="cda19-157">60</span></span>|
|<span data-ttu-id="cda19-158">512</span><span class="sxs-lookup"><span data-stu-id="cda19-158">512</span></span>|<span data-ttu-id="cda19-159">100</span><span class="sxs-lookup"><span data-stu-id="cda19-159">100</span></span>|<span data-ttu-id="cda19-160">00:00:16.3850303</span><span class="sxs-lookup"><span data-stu-id="cda19-160">00:00:16.3850303</span></span>|<span data-ttu-id="cda19-161">307</span><span class="sxs-lookup"><span data-stu-id="cda19-161">307</span></span>|
|<span data-ttu-id="cda19-162">1024</span><span class="sxs-lookup"><span data-stu-id="cda19-162">1024</span></span>|<span data-ttu-id="cda19-163">500</span><span class="sxs-lookup"><span data-stu-id="cda19-163">500</span></span>|<span data-ttu-id="cda19-164">00:00:32.5907950</span><span class="sxs-lookup"><span data-stu-id="cda19-164">00:00:32.5907950</span></span>|<span data-ttu-id="cda19-165">615</span><span class="sxs-lookup"><span data-stu-id="cda19-165">615</span></span>|
|<span data-ttu-id="cda19-166">2048</span><span class="sxs-lookup"><span data-stu-id="cda19-166">2048</span></span>|<span data-ttu-id="cda19-167">1000</span><span class="sxs-lookup"><span data-stu-id="cda19-167">1000</span></span>|<span data-ttu-id="cda19-168">00:01:04.3775554</span><span class="sxs-lookup"><span data-stu-id="cda19-168">00:01:04.3775554</span></span>|<span data-ttu-id="cda19-169">1231</span><span class="sxs-lookup"><span data-stu-id="cda19-169">1231</span></span>|
|<span data-ttu-id="cda19-170">5012</span><span class="sxs-lookup"><span data-stu-id="cda19-170">5012</span></span>|<span data-ttu-id="cda19-171">100</span><span class="sxs-lookup"><span data-stu-id="cda19-171">100</span></span>|<span data-ttu-id="cda19-172">00:02:45.2951288</span><span class="sxs-lookup"><span data-stu-id="cda19-172">00:02:45.2951288</span></span>|<span data-ttu-id="cda19-173">3074</span><span class="sxs-lookup"><span data-stu-id="cda19-173">3074</span></span>|

<span data-ttu-id="cda19-174">Una vez que un paquete está comprimido, se puede cargar en uno o varios clústeres de Service Fabric según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="cda19-174">Once a package is compressed, it can be uploaded to one or multiple Service Fabric clusters as needed.</span></span> <span data-ttu-id="cda19-175">El mecanismo de implementación es el mismo para los paquetes comprimidos y sin comprimir.</span><span class="sxs-lookup"><span data-stu-id="cda19-175">The deployment mechanism is same for compressed and uncompressed packages.</span></span> <span data-ttu-id="cda19-176">Si el paquete se comprime, se almacena como tal en el almacén de imágenes de clúster y se descomprime en el nodo antes de ejecutar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="cda19-176">If the package is compressed, it is stored as such in the cluster image store and it's uncompressed on the node before the application is run.</span></span>


<span data-ttu-id="cda19-177">En el ejemplo siguiente se carga el paquete en el almacén de imágenes en una carpeta denominada "MyApplicationV1":</span><span class="sxs-lookup"><span data-stu-id="cda19-177">The following example uploads the package to the image store, into a folder named "MyApplicationV1":</span></span>

```powershell
PS C:\> Copy-ServiceFabricApplicationPackage -ApplicationPackagePath $path -ApplicationPackagePathInImageStore MyApplicationV1 -ImageStoreConnectionString (Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest)) -TimeoutSec 1800
```

<span data-ttu-id="cda19-178">El cmdlet **Get-ImageStoreConnectionStringFromClusterManifest** , que forma parte del módulo de PowerShell correspondiente al SDK de Service Fabric, se utiliza para obtener la cadena de conexión del almacén de imágenes.</span><span class="sxs-lookup"><span data-stu-id="cda19-178">The **Get-ImageStoreConnectionStringFromClusterManifest** cmdlet, which is part of the Service Fabric SDK PowerShell module, is used to get the image store connection string.</span></span>  <span data-ttu-id="cda19-179">Para importar el módulo de SDK, ejecute el siguiente código:</span><span class="sxs-lookup"><span data-stu-id="cda19-179">To import the SDK module, run:</span></span>

```powershell
Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
```

<span data-ttu-id="cda19-180">Si no se especifica el parámetro *-ApplicationPackagePathInImageStore*, el paquete de aplicación se copia en la carpeta "Debug" del almacén de imágenes.</span><span class="sxs-lookup"><span data-stu-id="cda19-180">If you do not specify the *-ApplicationPackagePathInImageStore* parameter, the application package is copied into the "Debug" folder in the image store.</span></span>

<span data-ttu-id="cda19-181">El tiempo necesario para cargar un paquete depende de varios factores.</span><span class="sxs-lookup"><span data-stu-id="cda19-181">The time it takes to upload a package differs depending on multiple factors.</span></span> <span data-ttu-id="cda19-182">Algunos de estos factores son el número de archivos del paquete, el tamaño del paquete y los tamaños de archivo.</span><span class="sxs-lookup"><span data-stu-id="cda19-182">Some of these factors are the number of files in the package, the package size, and the file sizes.</span></span> <span data-ttu-id="cda19-183">La velocidad de la red entre la máquina de origen y el clúster de Service Fabric también afecta al tiempo de carga.</span><span class="sxs-lookup"><span data-stu-id="cda19-183">The network speed between the source machine and the Service Fabric cluster also impacts the upload time.</span></span> <span data-ttu-id="cda19-184">El tiempo de espera predeterminado para [ServiceFabricApplicationPackage copia](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) es de 30 minutos.</span><span class="sxs-lookup"><span data-stu-id="cda19-184">The default timeout for [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) is 30 minutes.</span></span>
<span data-ttu-id="cda19-185">Dependiendo de los factores descritos, puede que tenga que aumentar el tiempo de espera.</span><span class="sxs-lookup"><span data-stu-id="cda19-185">Depending on the described factors, you may have to increase the timeout.</span></span> <span data-ttu-id="cda19-186">Si va a comprimir el paquete en la llamada de copia, también debe tener en cuenta el tiempo de compresión.</span><span class="sxs-lookup"><span data-stu-id="cda19-186">If you are compressing the package in the copy call, you need to also consider the compression time.</span></span>

<span data-ttu-id="cda19-187">Consulte [Descripción del valor ImageStoreConnectionString](service-fabric-image-store-connection-string.md) para más información sobre el almacén de imágenes y su cadena de conexión.</span><span class="sxs-lookup"><span data-stu-id="cda19-187">See [Understand the image store connection string](service-fabric-image-store-connection-string.md) for supplementary information about the image store and image store connection string.</span></span>

## <a name="register-the-application-package"></a><span data-ttu-id="cda19-188">Registrar el paquete de la aplicación</span><span class="sxs-lookup"><span data-stu-id="cda19-188">Register the application package</span></span>
<span data-ttu-id="cda19-189">El tipo y la versión de la aplicación declarados en el manifiesto de aplicación estarán disponibles para usarse cuando se registre el paquete de aplicación.</span><span class="sxs-lookup"><span data-stu-id="cda19-189">The application type and version declared in the application manifest become available for use when the application package is registered.</span></span> <span data-ttu-id="cda19-190">El sistema leerá el paquete cargado en el paso anterior, comprobará dicho paquete, procesará su contenido y copiará el paquete procesado en una ubicación del sistema interno.</span><span class="sxs-lookup"><span data-stu-id="cda19-190">The system reads the package uploaded in the previous step, verifies the package, processes the package contents, and copies the processed package to an internal system location.</span></span>  

<span data-ttu-id="cda19-191">Ejecute el cmdlet [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) para registrar el tipo de aplicación en el clúster y ponerlo a disposición para la implementación:</span><span class="sxs-lookup"><span data-stu-id="cda19-191">Run the [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) cmdlet to register the application type in the cluster and make it available for deployment:</span></span>

```powershell
PS C:\> Register-ServiceFabricApplicationType MyApplicationV1
Register application type succeeded
```

<span data-ttu-id="cda19-192">"MyApplicationV1" es la carpeta del almacén de imágenes donde se encuentra el paquete de aplicación.</span><span class="sxs-lookup"><span data-stu-id="cda19-192">"MyApplicationV1" is the folder in the image store where the application package is located.</span></span> <span data-ttu-id="cda19-193">El tipo de aplicación con el nombre "MyApplicationType" y la versión "1.0.0" (ambos se encuentran en el manifiesto de aplicación) ya estará registrado en el clúster.</span><span class="sxs-lookup"><span data-stu-id="cda19-193">The application type with name "MyApplicationType" and version "1.0.0" (both are found in the application manifest) is now registered in the cluster.</span></span>

<span data-ttu-id="cda19-194">El comando [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) devuelve solo después de que el sistema haya registrado correctamente el paquete de aplicación.</span><span class="sxs-lookup"><span data-stu-id="cda19-194">The [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) command returns only after the system has successfully registered the application package.</span></span> <span data-ttu-id="cda19-195">El tiempo que tarde en registrarse dependerá del contenido del paquete de aplicación.</span><span class="sxs-lookup"><span data-stu-id="cda19-195">How long registration takes depends on the size and contents of the application package.</span></span> <span data-ttu-id="cda19-196">El parámetro **- TimeoutSec** se puede usar para proporcionar un tiempo de espera más largo (el tiempo de espera predeterminado es de 60 segundos).</span><span class="sxs-lookup"><span data-stu-id="cda19-196">If needed, the **-TimeoutSec** parameter can be used to supply a longer timeout (the default timeout is 60 seconds).</span></span>

<span data-ttu-id="cda19-197">Si tiene un paquete de aplicación grande o está experimentando tiempos de espera, use el parámetro **-Async**.</span><span class="sxs-lookup"><span data-stu-id="cda19-197">If you have a large application package or if you are experiencing timeouts, use the **-Async** parameter.</span></span> <span data-ttu-id="cda19-198">El comando se devuelve cuando el clúster acepta el comando de registro, y el procesamiento continúa según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="cda19-198">The command returns when the cluster accepts the register command, and the processing continues as needed.</span></span>
<span data-ttu-id="cda19-199">El comando [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) enumera todas las versiones del tipo de aplicación registradas correctamente, así como el estado de registro.</span><span class="sxs-lookup"><span data-stu-id="cda19-199">The [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) command lists all successfully registered application type versions and their registration status.</span></span> <span data-ttu-id="cda19-200">Puede utilizar este comando para determinar cuándo se realiza el registro.</span><span class="sxs-lookup"><span data-stu-id="cda19-200">You can use this command to determine when the registration is done.</span></span>

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

## <a name="create-the-application"></a><span data-ttu-id="cda19-201">Creación de la aplicación</span><span class="sxs-lookup"><span data-stu-id="cda19-201">Create the application</span></span>
<span data-ttu-id="cda19-202">Se pueden crear instancias de una aplicación a partir de cualquier versión del tipo de aplicación que se haya registrado correctamente mediante el cmdlet [New-ServiceFabricApplication](/powershell/module/servicefabric/new-servicefabricapplication?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="cda19-202">You can instantiate an application from any application type version that has been registered successfully by using the [New-ServiceFabricApplication](/powershell/module/servicefabric/new-servicefabricapplication?view=azureservicefabricps) cmdlet.</span></span> <span data-ttu-id="cda19-203">El nombre de cada aplicación debe empezar con el esquema *"fabric:"* y ser único para cada instancia de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="cda19-203">The name of each application must start with the *"fabric:"* scheme and must be unique for each application instance.</span></span> <span data-ttu-id="cda19-204">También se crean los servicios predeterminados que se hayan definido en el manifiesto de aplicación del tipo de aplicación de destino.</span><span class="sxs-lookup"><span data-stu-id="cda19-204">Any default services defined in the application manifest of the target application type are also created.</span></span>

```powershell
PS C:\> New-ServiceFabricApplication fabric:/MyApp MyApplicationType 1.0.0

ApplicationName        : fabric:/MyApp
ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
ApplicationParameters  : {}
```
<span data-ttu-id="cda19-205">Pueden crearse varias instancias de aplicación para cualquier versión concreta de un tipo de aplicación registrado.</span><span class="sxs-lookup"><span data-stu-id="cda19-205">Multiple application instances can be created for any given version of a registered application type.</span></span> <span data-ttu-id="cda19-206">Cada instancia de la aplicación se ejecuta de forma aislada, con su propio proceso y directorio de trabajo.</span><span class="sxs-lookup"><span data-stu-id="cda19-206">Each application instance runs in isolation, with its own work directory and process.</span></span>

<span data-ttu-id="cda19-207">Para ver el nombre de las aplicaciones y los servicios en ejecución en el clúster, ejecute los cmdlets [Get-ServiceFabricApplication](/powershell/servicefabric/vlatest/get-servicefabricapplication) y [Get-ServiceFabricService](/powershell/module/servicefabric/get-servicefabricservice?view=azureservicefabricps):</span><span class="sxs-lookup"><span data-stu-id="cda19-207">To see which named apps and services are running in the cluster, run the [Get-ServiceFabricApplication](/powershell/servicefabric/vlatest/get-servicefabricapplication) and [Get-ServiceFabricService](/powershell/module/servicefabric/get-servicefabricservice?view=azureservicefabricps) cmdlets:</span></span>

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

## <a name="remove-an-application"></a><span data-ttu-id="cda19-208">Eliminación de una aplicación</span><span class="sxs-lookup"><span data-stu-id="cda19-208">Remove an application</span></span>
<span data-ttu-id="cda19-209">Cuando ya no se necesite una instancia de aplicación, use el cmdlet [Remove-ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) para quitarla por nombre de manera permanente.</span><span class="sxs-lookup"><span data-stu-id="cda19-209">When an application instance is no longer needed, you can permanently remove it by name using the [Remove-ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) cmdlet.</span></span> <span data-ttu-id="cda19-210">[Remove-ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) también quita automáticamente todos los servicios que pertenezcan a la aplicación, con lo que se eliminan de forma permanente todos los estados del servicio.</span><span class="sxs-lookup"><span data-stu-id="cda19-210">[Remove-ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) automatically removes all services that belong to the application as well, permanently removing all service state.</span></span> 

> [!WARNING]
> <span data-ttu-id="cda19-211">No se puede deshacer esta operación y no se puede recuperar el estado de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="cda19-211">This operation cannot be reversed, and application state cannot be recovered.</span></span>

```powershell
PS C:\> Remove-ServiceFabricApplication fabric:/MyApp

Confirm
Continue with this operation?
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"):
Remove application instance succeeded

PS C:\> Get-ServiceFabricApplication
```

## <a name="unregister-an-application-type"></a><span data-ttu-id="cda19-212">Anulación de un registro del tipo de aplicación</span><span class="sxs-lookup"><span data-stu-id="cda19-212">Unregister an application type</span></span>
<span data-ttu-id="cda19-213">Cuando ya no se necesita una versión concreta de un tipo de aplicación, debe anularse el registro del tipo de aplicación mediante el cmdlet [Unregister-ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="cda19-213">When a particular version of an application type is no longer needed, you should unregister the application type using the [Unregister-ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) cmdlet.</span></span> <span data-ttu-id="cda19-214">Anular el registro de tipos de aplicación que no se usan libera espacio de almacenamiento del almacén de imágenes.</span><span class="sxs-lookup"><span data-stu-id="cda19-214">Unregistering unused application types releases storage space used by the image store.</span></span> <span data-ttu-id="cda19-215">No se puede anular el registro de un tipo de aplicación mientras no haya ninguna aplicación con instancias con él o no haya actualizaciones de aplicaciones pendientes que hagan referencia a él.</span><span class="sxs-lookup"><span data-stu-id="cda19-215">An application type can be unregistered as long as no applications are instantiated against it and no pending application upgrades are referencing it.</span></span>

<span data-ttu-id="cda19-216">Ejecute el cmdlet [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) para ver los tipos de aplicación registrados actualmente en el clúster:</span><span class="sxs-lookup"><span data-stu-id="cda19-216">Run [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) to see the application types currently registered in the cluster:</span></span>

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

<span data-ttu-id="cda19-217">Ejecute [Unregister-ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) para anular el registro de un tipo concreto de aplicación:</span><span class="sxs-lookup"><span data-stu-id="cda19-217">Run [Unregister-ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) to unregister a specific application type:</span></span>

```powershell
PS C:\> Unregister-ServiceFabricApplicationType MyApplicationType 1.0.0
```

## <a name="remove-an-application-package-from-the-image-store"></a><span data-ttu-id="cda19-218">Eliminación de un paquete de aplicación del almacén de imágenes</span><span class="sxs-lookup"><span data-stu-id="cda19-218">Remove an application package from the image store</span></span>
<span data-ttu-id="cda19-219">Cuando ya no se necesita un paquete de aplicación, puede eliminarlo del almacén de imágenes para liberar recursos del sistema.</span><span class="sxs-lookup"><span data-stu-id="cda19-219">When an application package is no longer needed, you can delete it from the image store to free up system resources.</span></span>

```powershell
PS C:\>Remove-ServiceFabricApplicationPackage -ApplicationPackagePathInImageStore MyApplicationV1 -ImageStoreConnectionString (Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest))
```

## <a name="troubleshooting"></a><span data-ttu-id="cda19-220">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="cda19-220">Troubleshooting</span></span>
### <a name="copy-servicefabricapplicationpackage-asks-for-an-imagestoreconnectionstring"></a><span data-ttu-id="cda19-221">Copy-ServiceFabricApplicationPackage pide una ImageStoreConnectionString</span><span class="sxs-lookup"><span data-stu-id="cda19-221">Copy-ServiceFabricApplicationPackage asks for an ImageStoreConnectionString</span></span>
<span data-ttu-id="cda19-222">El entorno del SDK de Service Fabric ya debe tener configurados los valores predeterminados correctos.</span><span class="sxs-lookup"><span data-stu-id="cda19-222">The Service Fabric SDK environment should already have the correct defaults set up.</span></span> <span data-ttu-id="cda19-223">Pero si es necesario, ImageStoreConnectionString para todos los comandos debe coincidir con el valor que usa el clúster de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="cda19-223">But if needed, the ImageStoreConnectionString for all commands should match the value that the Service Fabric cluster is using.</span></span> <span data-ttu-id="cda19-224">Puede encontrar ImageStoreConnectionString en el manifiesto del clúster, recuperado mediante los comandos [Get-ServiceFabricClusterManifest](/powershell/module/servicefabric/get-servicefabricclustermanifest?view=azureservicefabricps) y Get-ImageStoreConnectionStringFromClusterManifest:</span><span class="sxs-lookup"><span data-stu-id="cda19-224">You can find the ImageStoreConnectionString in the cluster manifest, retrieved using the [Get-ServiceFabricClusterManifest](/powershell/module/servicefabric/get-servicefabricclustermanifest?view=azureservicefabricps) and Get-ImageStoreConnectionStringFromClusterManifest commands:</span></span>

```powershell
PS C:\> Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest)
```

<span data-ttu-id="cda19-225">El cmdlet **Get-ImageStoreConnectionStringFromClusterManifest** , que forma parte del módulo de PowerShell correspondiente al SDK de Service Fabric, se utiliza para obtener la cadena de conexión del almacén de imágenes.</span><span class="sxs-lookup"><span data-stu-id="cda19-225">The **Get-ImageStoreConnectionStringFromClusterManifest** cmdlet, which is part of the Service Fabric SDK PowerShell module, is used to get the image store connection string.</span></span>  <span data-ttu-id="cda19-226">Para importar el módulo de SDK, ejecute el siguiente código:</span><span class="sxs-lookup"><span data-stu-id="cda19-226">To import the SDK module, run:</span></span>

```powershell
Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
```

<span data-ttu-id="cda19-227">ImageStoreConnectionString se encuentra en el manifiesto de clúster:</span><span class="sxs-lookup"><span data-stu-id="cda19-227">The ImageStoreConnectionString is found in the cluster manifest:</span></span>

```xml
<ClusterManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Name="Server-Default-SingleNode" Version="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">

    [...]

    <Section Name="Management">
      <Parameter Name="ImageStoreConnectionString" Value="file:D:\ServiceFabric\Data\ImageStore" />
    </Section>

    [...]
```

<span data-ttu-id="cda19-228">Consulte [Descripción del valor ImageStoreConnectionString](service-fabric-image-store-connection-string.md) para más información sobre el almacén de imágenes y su cadena de conexión.</span><span class="sxs-lookup"><span data-stu-id="cda19-228">See [Understand the image store connection string](service-fabric-image-store-connection-string.md) for supplementary information about the image store and image store connection string.</span></span>

### <a name="deploy-large-application-package"></a><span data-ttu-id="cda19-229">Implementación de un paquete de aplicación grande</span><span class="sxs-lookup"><span data-stu-id="cda19-229">Deploy large application package</span></span>
<span data-ttu-id="cda19-230">Problema: [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) agota el tiempo de espera para un paquete de aplicación grande (del orden de GB).</span><span class="sxs-lookup"><span data-stu-id="cda19-230">Issue: [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) times out for a large application package (order of GB).</span></span>
<span data-ttu-id="cda19-231">Pruebe lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="cda19-231">Try:</span></span>
- <span data-ttu-id="cda19-232">Especifique un tiempo de espera mayor para el comando [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) con el parámetro `TimeoutSec`.</span><span class="sxs-lookup"><span data-stu-id="cda19-232">Specify a larger timeout for [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) command, with `TimeoutSec` parameter.</span></span> <span data-ttu-id="cda19-233">De forma predeterminada, el tiempo de espera es de 30 minutos.</span><span class="sxs-lookup"><span data-stu-id="cda19-233">By default, the timeout is 30 minutes.</span></span>
- <span data-ttu-id="cda19-234">Compruebe la conexión de red entre la máquina de origen y el clúster.</span><span class="sxs-lookup"><span data-stu-id="cda19-234">Check the network connection between your source machine and cluster.</span></span> <span data-ttu-id="cda19-235">Si la conexión es lenta, considere la posibilidad de usar una máquina con una conexión de red mejor.</span><span class="sxs-lookup"><span data-stu-id="cda19-235">If the connection is slow, consider using a machine with a better network connection.</span></span>
<span data-ttu-id="cda19-236">Si la máquina cliente se encuentra en otra región diferente al clúster, considere el uso de una máquina cliente que se encuentre en una región más cercana o en la misma región que el clúster.</span><span class="sxs-lookup"><span data-stu-id="cda19-236">If the client machine is in another region than the cluster, consider using a client machine in a closer or same region as the cluster.</span></span>
- <span data-ttu-id="cda19-237">Compruebe si está alcanzando la limitación externa.</span><span class="sxs-lookup"><span data-stu-id="cda19-237">Check if you are hitting external throttling.</span></span> <span data-ttu-id="cda19-238">Por ejemplo, cuando el almacén de imágenes está configurado para usar Azure Storage, se puede limitar carga.</span><span class="sxs-lookup"><span data-stu-id="cda19-238">For example, when the image store is configured to use azure storage, upload may be throttled.</span></span>

<span data-ttu-id="cda19-239">Problema: La carga del paquete se completó correctamente, pero [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) agota el tiempo de espera.</span><span class="sxs-lookup"><span data-stu-id="cda19-239">Issue: Upload package completed successfully, but [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) times out.</span></span>
<span data-ttu-id="cda19-240">Pruebe lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="cda19-240">Try:</span></span>
- <span data-ttu-id="cda19-241">[Comprima el paquete](service-fabric-package-apps.md#compress-a-package) antes de realizar la copia en el almacén de imágenes.</span><span class="sxs-lookup"><span data-stu-id="cda19-241">[Compress the package](service-fabric-package-apps.md#compress-a-package) before copying to the image store.</span></span>
<span data-ttu-id="cda19-242">La compresión reduce el tamaño y el número de archivos lo que, a su vez, reduce la cantidad de tráfico y trabajo que Service Fabric debe realizar.</span><span class="sxs-lookup"><span data-stu-id="cda19-242">The compression reduces the size and the number of files, which in turn reduces the amount of traffic and work that Service Fabric must perform.</span></span> <span data-ttu-id="cda19-243">La operación de carga puede ser más lenta (especialmente si incluyen el tiempo de compresión), pero el registro y la anulación del registro del tipo de aplicación son más rápidos.</span><span class="sxs-lookup"><span data-stu-id="cda19-243">The upload operation may be slower (especially if you include the compression time), but register and un-register the application type are faster.</span></span>
- <span data-ttu-id="cda19-244">Especifique un tiempo de espera mayor para [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) con el parámetro `TimeoutSec`.</span><span class="sxs-lookup"><span data-stu-id="cda19-244">Specify a larger timeout for [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) with `TimeoutSec` parameter.</span></span>
- <span data-ttu-id="cda19-245">Especifique el modificador `Async` para [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="cda19-245">Specify `Async` switch for [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps).</span></span> <span data-ttu-id="cda19-246">El comando devuelve resultados cuando el clúster acepta dicho comando y el registro del tipo de aplicación continúa de manera asincrónica.</span><span class="sxs-lookup"><span data-stu-id="cda19-246">The command returns when the cluster accepts the command and the registration of the application type continues asynchronously.</span></span> <span data-ttu-id="cda19-247">Por esta razón, no hay ninguna necesidad de especificar un tiempo de espera mayor en este caso.</span><span class="sxs-lookup"><span data-stu-id="cda19-247">For this reason, there is no need to specify a higher timeout in this case.</span></span> <span data-ttu-id="cda19-248">El comando [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) enumera todas las versiones del tipo de aplicación registradas correctamente, así como el estado de registro.</span><span class="sxs-lookup"><span data-stu-id="cda19-248">The [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) command lists all successfully registered application type versions and their registration status.</span></span> <span data-ttu-id="cda19-249">Puede utilizar este comando para determinar cuándo se realiza el registro.</span><span class="sxs-lookup"><span data-stu-id="cda19-249">You can use this command to determine when the registration is done.</span></span>

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

### <a name="deploy-application-package-with-many-files"></a><span data-ttu-id="cda19-250">Implementación del paquete de aplicación con muchos archivos</span><span class="sxs-lookup"><span data-stu-id="cda19-250">Deploy application package with many files</span></span>
<span data-ttu-id="cda19-251">Problema: [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) agota el tiempo de espera para un paquete de aplicación con muchos archivos (del orden de miles).</span><span class="sxs-lookup"><span data-stu-id="cda19-251">Issue: [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) times out for an application package with many files (order of thousands).</span></span>
<span data-ttu-id="cda19-252">Pruebe lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="cda19-252">Try:</span></span>
- <span data-ttu-id="cda19-253">[Comprima el paquete](service-fabric-package-apps.md#compress-a-package) antes de realizar la copia en el almacén de imágenes.</span><span class="sxs-lookup"><span data-stu-id="cda19-253">[Compress the package](service-fabric-package-apps.md#compress-a-package) before copying to the image store.</span></span> <span data-ttu-id="cda19-254">La compresión reduce el número de archivos.</span><span class="sxs-lookup"><span data-stu-id="cda19-254">The compression reduces the number of files.</span></span>
- <span data-ttu-id="cda19-255">Especifique un tiempo de espera mayor para [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) con el parámetro `TimeoutSec`.</span><span class="sxs-lookup"><span data-stu-id="cda19-255">Specify a larger timeout for [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) with `TimeoutSec` parameter.</span></span>
- <span data-ttu-id="cda19-256">Especifique el modificador `Async` para [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="cda19-256">Specify `Async` switch for [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps).</span></span> <span data-ttu-id="cda19-257">El comando devuelve resultados cuando el clúster acepta dicho comando y el registro del tipo de aplicación continúa de manera asincrónica.</span><span class="sxs-lookup"><span data-stu-id="cda19-257">The command returns when the cluster accepts the command and the registration of the application type continues asynchronously.</span></span>
<span data-ttu-id="cda19-258">Por esta razón, no hay ninguna necesidad de especificar un tiempo de espera mayor en este caso.</span><span class="sxs-lookup"><span data-stu-id="cda19-258">For this reason, there is no need to specify a higher timeout in this case.</span></span> <span data-ttu-id="cda19-259">El comando [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) enumera todas las versiones del tipo de aplicación registradas correctamente, así como el estado de registro.</span><span class="sxs-lookup"><span data-stu-id="cda19-259">The [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) command lists all successfully registered application type versions and their registration status.</span></span> <span data-ttu-id="cda19-260">Puede utilizar este comando para determinar cuándo se realiza el registro.</span><span class="sxs-lookup"><span data-stu-id="cda19-260">You can use this command to determine when the registration is done.</span></span>

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

## <a name="next-steps"></a><span data-ttu-id="cda19-261">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="cda19-261">Next steps</span></span>
[<span data-ttu-id="cda19-262">Actualización de la aplicación de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="cda19-262">Service Fabric application upgrade</span></span>](service-fabric-application-upgrade.md)

[<span data-ttu-id="cda19-263">Introducción al estado de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="cda19-263">Service Fabric health introduction</span></span>](service-fabric-health-introduction.md)

[<span data-ttu-id="cda19-264">Diagnosticar y solucionar problemas de un servicio de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="cda19-264">Diagnose and troubleshoot a Service Fabric service</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[<span data-ttu-id="cda19-265">Modelar una aplicación en Service Fabric</span><span class="sxs-lookup"><span data-stu-id="cda19-265">Model an application in Service Fabric</span></span>](service-fabric-application-model.md)

<!--Link references--In actual articles, you only need a single period before the slash-->
[10]: service-fabric-application-model.md
[11]: service-fabric-application-upgrade.md
