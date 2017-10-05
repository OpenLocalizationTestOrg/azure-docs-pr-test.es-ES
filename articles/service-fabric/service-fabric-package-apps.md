---
title: "Empaquetado de una aplicación de Azure Service Fabric | Microsoft Docs"
description: "Empaquetado de una aplicación de Service Fabric antes de implementarla en un clúster."
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
ms.openlocfilehash: 486a27d7ca576c8fe1552c02eb24ece6b8bb2ba8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="package-an-application"></a><span data-ttu-id="42607-103">Empaquetar una aplicación</span><span class="sxs-lookup"><span data-stu-id="42607-103">Package an application</span></span>
<span data-ttu-id="42607-104">En este artículo se describe cómo empaquetar una aplicación de Service Fabric y prepararla para su implementación.</span><span class="sxs-lookup"><span data-stu-id="42607-104">This article describes how to package a Service Fabric application and make it ready for deployment.</span></span>

## <a name="package-layout"></a><span data-ttu-id="42607-105">Diseño del paquete</span><span class="sxs-lookup"><span data-stu-id="42607-105">Package layout</span></span>
<span data-ttu-id="42607-106">El manifiesto de aplicación, uno o varios manifiestos de servicio y otros archivos de paquete necesarios deben organizarse en un diseño específico para la implementación en un clúster de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="42607-106">The application manifest, one or more service manifests, and other necessary package files must be organized in a specific layout for deployment into a Service Fabric cluster.</span></span> <span data-ttu-id="42607-107">Los manifiestos de ejemplo en este artículo deberían organizarse con la siguiente estructura de directorios:</span><span class="sxs-lookup"><span data-stu-id="42607-107">The example manifests in this article would need to be organized in the following directory structure:</span></span>

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

<span data-ttu-id="42607-108">Las carpetas reciben un nombre para coincidir con los atributos **Nombre** de cada elemento correspondiente.</span><span class="sxs-lookup"><span data-stu-id="42607-108">The folders are named to match the **Name** attributes of each corresponding element.</span></span> <span data-ttu-id="42607-109">Por ejemplo, si el manifiesto de servicio contenía dos paquetes de código con los nombres **MiCódigoA** y **MiCódigoB**, dos carpetas con los mismos nombres incluirán los archivos binarios necesarios para cada paquete de código.</span><span class="sxs-lookup"><span data-stu-id="42607-109">For example, if the service manifest contained two code packages with the names **MyCodeA** and **MyCodeB**, then two folders with the same names would contain the necessary binaries for each code package.</span></span>

## <a name="use-setupentrypoint"></a><span data-ttu-id="42607-110">Usar SetupEntrypoint</span><span class="sxs-lookup"><span data-stu-id="42607-110">Use SetupEntryPoint</span></span>
<span data-ttu-id="42607-111">Los escenarios de uso de **SetupEntryPoint** habituales corresponden a cuando se necesita ejecutar un archivo ejecutable antes de iniciar el servicio o cuando necesita realizar una operación con privilegios elevados.</span><span class="sxs-lookup"><span data-stu-id="42607-111">Typical scenarios for using **SetupEntryPoint** are when you need to run an executable before the service starts or you need to perform an operation with elevated privileges.</span></span> <span data-ttu-id="42607-112">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="42607-112">For example:</span></span>

* <span data-ttu-id="42607-113">configuración e inicialización de las variables de entorno que el ejecutable del servicio necesita.</span><span class="sxs-lookup"><span data-stu-id="42607-113">Setting up and initializing environment variables that the service executable needs.</span></span> <span data-ttu-id="42607-114">No se limita tan solo a los archivos ejecutables escritos a través de los modelos de programación de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="42607-114">It is not limited to only executables written via the Service Fabric programming models.</span></span> <span data-ttu-id="42607-115">Por ejemplo, npm.exe necesita algunas variables de entorno configuradas para implementar una aplicación node.js.</span><span class="sxs-lookup"><span data-stu-id="42607-115">For example, npm.exe needs some environment variables configured for deploying a node.js application.</span></span>
* <span data-ttu-id="42607-116">Configuración del control de acceso mediante la instalación de certificados de seguridad.</span><span class="sxs-lookup"><span data-stu-id="42607-116">Setting up access control by installing security certificates.</span></span>

<span data-ttu-id="42607-117">Para obtener más información sobre cómo configurar **SetupEntryPoint**, vea [Configuración de la directiva para un punto de entrada del programa de instalación del servicio](service-fabric-application-runas-security.md).</span><span class="sxs-lookup"><span data-stu-id="42607-117">For more information on how to configure the **SetupEntryPoint**, see [Configure the policy for a service setup entry point](service-fabric-application-runas-security.md)</span></span>

<a id="Package-App"></a>
## <a name="configure"></a><span data-ttu-id="42607-118">Configuración</span><span class="sxs-lookup"><span data-stu-id="42607-118">Configure</span></span>
### <a name="build-a-package-by-using-visual-studio"></a><span data-ttu-id="42607-119">Crear un paquete mediante Visual Studio</span><span class="sxs-lookup"><span data-stu-id="42607-119">Build a package by using Visual Studio</span></span>
<span data-ttu-id="42607-120">Si usa Visual Studio 2015 para crear su aplicación, puede utilizar el comando Package para crear automáticamente un paquete que coincida con el diseño descrito anteriormente.</span><span class="sxs-lookup"><span data-stu-id="42607-120">If you use Visual Studio 2015 to create your application, you can use the Package command to automatically create a package that matches the layout described above.</span></span>

<span data-ttu-id="42607-121">Para crear un paquete, haga clic con el botón derecho en el proyecto de aplicación del Explorador de soluciones y elegir el comando Package, como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="42607-121">To create a package, right-click the application project in Solution Explorer and choose the Package command, as shown below:</span></span>

![Empaquetado de una aplicación con Visual Studio][vs-package-command]

<span data-ttu-id="42607-123">Una vez completado el empaquetado, busque la ubicación del paquete en la ventana **Salida**.</span><span class="sxs-lookup"><span data-stu-id="42607-123">When packaging is complete, you can find the location of the package in the **Output** window.</span></span> <span data-ttu-id="42607-124">El paso de empaquetado se produce automáticamente al implementar o depurar la aplicación en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="42607-124">The packaging step occurs automatically when you deploy or debug your application in Visual Studio.</span></span>

### <a name="build-a-package-by-command-line"></a><span data-ttu-id="42607-125">Creación de un paquete mediante la línea de comandos</span><span class="sxs-lookup"><span data-stu-id="42607-125">Build a package by command line</span></span>
<span data-ttu-id="42607-126">También es posible empaquetar la aplicación mediante programación usando `msbuild.exe`.</span><span class="sxs-lookup"><span data-stu-id="42607-126">It is also possible to programmatically package up your application using `msbuild.exe`.</span></span> <span data-ttu-id="42607-127">En el fondo esto es lo que ejecuta Visual Studio, por lo que la salida es la misma.</span><span class="sxs-lookup"><span data-stu-id="42607-127">Under the hood, Visual Studio is running it so the output is same.</span></span>

```shell
D:\Temp> msbuild HelloWorld.sfproj /t:Package
```

## <a name="test-the-package"></a><span data-ttu-id="42607-128">Probar el paquete</span><span class="sxs-lookup"><span data-stu-id="42607-128">Test the package</span></span>
<span data-ttu-id="42607-129">Puede comprobar la estructura del paquete localmente a través de PowerShell mediante el comando [Test-ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) .</span><span class="sxs-lookup"><span data-stu-id="42607-129">You can verify the package structure locally through PowerShell by using the [Test-ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) command.</span></span>
<span data-ttu-id="42607-130">Este comando comprueba si existen problemas de análisis de manifiestos y verifica todas las referencias.</span><span class="sxs-lookup"><span data-stu-id="42607-130">This command checks for manifest parsing issues and verify all references.</span></span> <span data-ttu-id="42607-131">Este comando solo comprueba la corrección estructural de los directorios y archivos del paquete.</span><span class="sxs-lookup"><span data-stu-id="42607-131">This command only verifies the structural correctness of the directories and files in the package.</span></span>
<span data-ttu-id="42607-132">No comprobará ningún contenido de código o de paquete de datos y se limitará a comprobar que todos los archivos necesarios están presentes.</span><span class="sxs-lookup"><span data-stu-id="42607-132">It doesn't verify any of the code or data package contents beyond checking that all necessary files are present.</span></span>

```
PS D:\temp> Test-ServiceFabricApplicationPackage .\MyApplicationType
False
Test-ServiceFabricApplicationPackage : The EntryPoint MySetup.bat is not found.
FileName: C:\Users\servicefabric\AppData\Local\Temp\TestApplicationPackage_7195781181\nrri205a.e2h\MyApplicationType\MyServiceManifest\ServiceManifest.xml
```

<span data-ttu-id="42607-133">Este error muestra que el archivo *MySetup.bat* al que se hace referencia en el manifiesto de servicio **SetupEntryPoint** no está en el paquete de código.</span><span class="sxs-lookup"><span data-stu-id="42607-133">This error shows that the *MySetup.bat* file referenced in the service manifest **SetupEntryPoint** is missing from the code package.</span></span> <span data-ttu-id="42607-134">Después de agregar el archivo que falta, se comprueba la aplicación:</span><span class="sxs-lookup"><span data-stu-id="42607-134">After the missing file is added, the application verification passes:</span></span>

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

<span data-ttu-id="42607-135">Si la aplicación tiene [parámetros de aplicación](service-fabric-manage-multiple-environment-app-configuration.md) definidos, puede pasarlos en [Test-ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) para realizar una validación adecuada.</span><span class="sxs-lookup"><span data-stu-id="42607-135">If your application has [application parameters](service-fabric-manage-multiple-environment-app-configuration.md) defined, you can pass them in [Test-ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) for proper validation.</span></span>

<span data-ttu-id="42607-136">Si conoce el clúster donde se implementará la aplicación, se recomienda pasar el parámetro `ImageStoreConnectionString`.</span><span class="sxs-lookup"><span data-stu-id="42607-136">If you know the cluster where the application will be deployed, it is recommended you pass in the `ImageStoreConnectionString` parameter.</span></span> <span data-ttu-id="42607-137">En este caso, el paquete también se valida con las versiones anteriores de la aplicación que ya se está ejecutando en el clúster.</span><span class="sxs-lookup"><span data-stu-id="42607-137">In this case, the package is also validated against previous versions of the application that are already running in the cluster.</span></span> <span data-ttu-id="42607-138">Por ejemplo, la validación puede detectar si ya se implementó un paquete con la misma versión pero distinto contenido.</span><span class="sxs-lookup"><span data-stu-id="42607-138">For example, the validation can detect whether a package with the same version but different content was already deployed.</span></span>  

<span data-ttu-id="42607-139">Una vez que la aplicación se empaqueta correctamente y supera la validación, haga una evaluación según el tamaño y el número de archivos si es necesario comprimir.</span><span class="sxs-lookup"><span data-stu-id="42607-139">Once the application is packaged correctly and passes validation, evaluate based on the size and the number of files if compression is needed.</span></span>

## <a name="compress-a-package"></a><span data-ttu-id="42607-140">Compresión de un paquete</span><span class="sxs-lookup"><span data-stu-id="42607-140">Compress a package</span></span>
<span data-ttu-id="42607-141">Cuando un paquete es grande o tiene muchos archivos, puede comprimirlo para acelerar la implementación.</span><span class="sxs-lookup"><span data-stu-id="42607-141">When a package is large or has many files, you can compress it for faster deployment.</span></span> <span data-ttu-id="42607-142">La compresión reduce el número de archivos y el tamaño del paquete.</span><span class="sxs-lookup"><span data-stu-id="42607-142">Compression reduces the number of files and the package size.</span></span>
<span data-ttu-id="42607-143">Si se trata de un paquete de aplicación comprimido, la [carga del paquete de aplicación](service-fabric-deploy-remove-applications.md#upload-the-application-package) puede tardar más en comparación con un paquete sin comprimir, sobre todo, si se tiene en cuenta el tiempo de compresión; sin embargo, el [registro](service-fabric-deploy-remove-applications.md#register-the-application-package) y la [anulación del registro del tipo de aplicación](service-fabric-deploy-remove-applications.md#unregister-an-application-type) se realizan más rápido si el paquete está comprimido.</span><span class="sxs-lookup"><span data-stu-id="42607-143">For a compressed application package, [Uploading the application package](service-fabric-deploy-remove-applications.md#upload-the-application-package) may take longer compared to uploading the uncompressed package (specially if compression time is factored in), but [registering](service-fabric-deploy-remove-applications.md#register-the-application-package) and [un-registering the application type](service-fabric-deploy-remove-applications.md#unregister-an-application-type) are faster for a compressed application package.</span></span>

<span data-ttu-id="42607-144">El mecanismo de implementación es el mismo para los paquetes comprimidos y sin comprimir.</span><span class="sxs-lookup"><span data-stu-id="42607-144">The deployment mechanism is same for compressed and uncompressed packages.</span></span> <span data-ttu-id="42607-145">Si el paquete se comprime, se almacena como tal en el almacén de imágenes de clúster y se descomprime en el nodo antes de ejecutar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="42607-145">If the package is compressed, it is stored as such in the cluster image store and it's uncompressed on the node before the application is run.</span></span>
<span data-ttu-id="42607-146">La compresión reemplaza el paquete de Service Fabric válido por la versión comprimida.</span><span class="sxs-lookup"><span data-stu-id="42607-146">The compression replaces the valid Service Fabric package with the compressed version.</span></span> <span data-ttu-id="42607-147">La carpeta debe permitir permisos de escritura.</span><span class="sxs-lookup"><span data-stu-id="42607-147">The folder must allow write permissions.</span></span> <span data-ttu-id="42607-148">La ejecución de la compresión en un paquete ya comprimido no produce ningún cambio.</span><span class="sxs-lookup"><span data-stu-id="42607-148">Running compression on an already compressed package yields no changes.</span></span>

<span data-ttu-id="42607-149">Puede comprimir un paquete ejecutando el comando de Powershell [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) con el modificador `CompressPackage`.</span><span class="sxs-lookup"><span data-stu-id="42607-149">You can compress a package by running the Powershell command [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) with `CompressPackage` switch.</span></span> <span data-ttu-id="42607-150">Puede descomprimir el paquete con el mismo comando, mediante el modificador `UncompressPackage`.</span><span class="sxs-lookup"><span data-stu-id="42607-150">You can uncompress the package with the same command, using `UncompressPackage` switch.</span></span>

<span data-ttu-id="42607-151">El siguiente comando comprime el paquete sin copiarlo en el almacén de imágenes.</span><span class="sxs-lookup"><span data-stu-id="42607-151">The following command compresses the package without copying it to the image store.</span></span> <span data-ttu-id="42607-152">Puede copiar un paquete comprimido en uno o varios clústeres de Service Fabric, según sea necesario, con [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) sin la marca `SkipCopy`.</span><span class="sxs-lookup"><span data-stu-id="42607-152">You can copy a compressed package to one or more Service Fabric clusters, as needed, using [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) without the `SkipCopy` flag.</span></span>
<span data-ttu-id="42607-153">El paquete ahora incluye los archivos comprimidos para los paquetes `code`, `config` y `data`.</span><span class="sxs-lookup"><span data-stu-id="42607-153">The package now includes zipped files for the `code`, `config`, and `data` packages.</span></span> <span data-ttu-id="42607-154">Los manifiestos de aplicación y de servicio no se comprimen porque son necesarios para muchas operaciones internas (por ejemplo, uso compartido de paquetes, nombre de tipo de aplicación y extracción de versiones para ciertas validaciones).</span><span class="sxs-lookup"><span data-stu-id="42607-154">The application manifest and the service manifests are not zipped, because they are needed for many internal operations (like package sharing, application type name and version extraction for certain validations).</span></span>
<span data-ttu-id="42607-155">La compresión de los manifiestos haría que estas operaciones resultaran ineficaces.</span><span class="sxs-lookup"><span data-stu-id="42607-155">Zipping the manifests would make these operations inefficient.</span></span>

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

<span data-ttu-id="42607-156">Como alternativa, puede comprimir y copiar el paquete con [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) en un solo paso.</span><span class="sxs-lookup"><span data-stu-id="42607-156">Alternatively, you can compress and copy the package with [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) in one step.</span></span>
<span data-ttu-id="42607-157">Si el paquete es grande, proporcione un tiempo de espera lo suficientemente alto como para dar tiempo tanto para la compresión del paquete como para la carga en el clúster.</span><span class="sxs-lookup"><span data-stu-id="42607-157">If the package is large, provide a high enough timeout to allow time for both the package compression and the upload to the cluster.</span></span>
```
PS D:\temp> Copy-ServiceFabricApplicationPackage -ApplicationPackagePath .\MyApplicationType -ApplicationPackagePathInImageStore MyApplicationType -ImageStoreConnectionString fabric:ImageStore -CompressPackage -TimeoutSec 5400
```

<span data-ttu-id="42607-158">Internamente, Service Fabric calcula las sumas de comprobación para los paquetes de aplicación para la validación.</span><span class="sxs-lookup"><span data-stu-id="42607-158">Internally, Service Fabric computes checksums for the application packages for validation.</span></span> <span data-ttu-id="42607-159">Cuando se utilice la compresión, las sumas de comprobación se calculan en las versiones comprimidas de cada paquete.</span><span class="sxs-lookup"><span data-stu-id="42607-159">When using compression, the checksums are computed on the zipped versions of each package.</span></span>
<span data-ttu-id="42607-160">Si ha copiado una versión sin comprimir del paquete de aplicación y desea utilizar la compresión para el mismo paquete, debe cambiar la versión de los paquetes `code`, `config` y `data` para evitar la falta de coincidencia en la suma de comprobación.</span><span class="sxs-lookup"><span data-stu-id="42607-160">If you copied an uncompressed version of your application package, and you want to use compression for the same package, you must change the versions of the `code`, `config`, and `data` packages to avoid checksum mismatch.</span></span> <span data-ttu-id="42607-161">Si los paquetes no han cambiado, en lugar de modificar la versión, puede usar el [aprovisionamiento de diferencias](service-fabric-application-upgrade-advanced.md).</span><span class="sxs-lookup"><span data-stu-id="42607-161">If the packages are unchanged, instead of changing the version, you can use [diff provisioning](service-fabric-application-upgrade-advanced.md).</span></span> <span data-ttu-id="42607-162">Con esta opción, no incluya el paquete sin cambios; en su lugar, haga referencia a él desde el manifiesto de servicio.</span><span class="sxs-lookup"><span data-stu-id="42607-162">With this option, do not include the unchanged package instead reference it from the service manifest.</span></span>

<span data-ttu-id="42607-163">De forma similar, si ha cargado una versión comprimida del paquete y desea usar un paquete sin comprimir, debe actualizar las versiones para evitar la falta de coincidencia en la suma de comprobación.</span><span class="sxs-lookup"><span data-stu-id="42607-163">Similarly, if you uploaded a compressed version of the package and you want to use an uncompressed package, you must update the versions to avoid the checksum mismatch.</span></span>

<span data-ttu-id="42607-164">El paquete se empaqueta correctamente, validado y comprimido (si es necesario), por lo que está listo para la [implementación](service-fabric-deploy-remove-applications.md) en uno o varios clústeres de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="42607-164">The package is now packaged correctly, validated, and compressed (if needed), so it is ready for [deployment](service-fabric-deploy-remove-applications.md) to one or more Service Fabric clusters.</span></span>

### <a name="compress-packages-when-deploying-using-visual-studio"></a><span data-ttu-id="42607-165">Compresión de paquetes al implementar con Visual Studio</span><span class="sxs-lookup"><span data-stu-id="42607-165">Compress packages when deploying using Visual Studio</span></span>
<span data-ttu-id="42607-166">Puede indicar a Visual Studio que comprima paquetes en la implementación, agregando el elemento `CopyPackageParameters` al perfil de publicación, y establezca el atributo `CompressPackage` en `true`.</span><span class="sxs-lookup"><span data-stu-id="42607-166">You can instruct Visual Studio to compress packages on deployment, by adding the `CopyPackageParameters` element to your publish profile, and set the `CompressPackage` attribute to `true`.</span></span>

``` xml
    <PublishProfile xmlns="http://schemas.microsoft.com/2015/05/fabrictools">
        <ClusterConnectionParameters ConnectionEndpoint="mycluster.westus.cloudapp.azure.com" />
        <ApplicationParameterFile Path="..\ApplicationParameters\Cloud.xml" />
        <CopyPackageParameters CompressPackage="true"/>
    </PublishProfile>
```

## <a name="next-steps"></a><span data-ttu-id="42607-167">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="42607-167">Next steps</span></span>
<span data-ttu-id="42607-168">[Implementación y eliminación de aplicaciones][10] describe cómo usar PowerShell para administrar las instancias de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="42607-168">[Deploy and remove applications][10] describes how to use PowerShell to manage application instances</span></span>

<span data-ttu-id="42607-169">[Administración de los parámetros de la aplicación en varios entornos][11] describe cómo configurar parámetros y variables de entorno para diferentes instancias de aplicación.</span><span class="sxs-lookup"><span data-stu-id="42607-169">[Managing application parameters for multiple environments][11] describes how to configure parameters and environment variables for different application instances.</span></span>

<span data-ttu-id="42607-170">[Configuración de directivas de seguridad para la aplicación][12] describe cómo ejecutar los servicios a través de directivas de seguridad para restringir el acceso.</span><span class="sxs-lookup"><span data-stu-id="42607-170">[Configure security policies for your application][12] describes how to run services under security policies to restrict access.</span></span>

<!--Image references-->
[vs-package-command]: ./media/service-fabric-package-apps/vs-package-command.png

<!--Link references--In actual articles, you only need a single period before the slash-->
[10]: service-fabric-deploy-remove-applications.md
[11]: service-fabric-manage-multiple-environment-app-configuration.md
[12]: service-fabric-application-runas-security.md
