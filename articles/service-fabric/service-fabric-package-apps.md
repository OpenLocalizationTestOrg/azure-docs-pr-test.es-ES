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
# <a name="package-an-application"></a><span data-ttu-id="bc09d-103">Empaquetar una aplicación</span><span class="sxs-lookup"><span data-stu-id="bc09d-103">Package an application</span></span>
<span data-ttu-id="bc09d-104">Este artículo se describe cómo toopackage una aplicación de Service Fabric y prepararlo para la implementación.</span><span class="sxs-lookup"><span data-stu-id="bc09d-104">This article describes how toopackage a Service Fabric application and make it ready for deployment.</span></span>

## <a name="package-layout"></a><span data-ttu-id="bc09d-105">Diseño del paquete</span><span class="sxs-lookup"><span data-stu-id="bc09d-105">Package layout</span></span>
<span data-ttu-id="bc09d-106">manifiesto de aplicación Hola, uno o varios de los manifiestos de servicio y otro paquete necesario de archivos deben estar organizados en un diseño específico para la implementación en un clúster de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="bc09d-106">hello application manifest, one or more service manifests, and other necessary package files must be organized in a specific layout for deployment into a Service Fabric cluster.</span></span> <span data-ttu-id="bc09d-107">manifiestos de ejemplo de Hola en este artículo necesitaría toobe organizado en hello siguiendo la estructura de directorios:</span><span class="sxs-lookup"><span data-stu-id="bc09d-107">hello example manifests in this article would need toobe organized in hello following directory structure:</span></span>

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

<span data-ttu-id="bc09d-108">carpetas de Hola se llaman hello toomatch **nombre** atributos de cada elemento correspondiente.</span><span class="sxs-lookup"><span data-stu-id="bc09d-108">hello folders are named toomatch hello **Name** attributes of each corresponding element.</span></span> <span data-ttu-id="bc09d-109">Por ejemplo, si hello manifiesto del servicio contiene dos paquetes de código con nombres de hello **MyCodeA** y **MyCodeB**, a continuación, dos carpetas con hello suele contener los mismos nombres Hola archivos binarios necesarios para cada código paquete.</span><span class="sxs-lookup"><span data-stu-id="bc09d-109">For example, if hello service manifest contained two code packages with hello names **MyCodeA** and **MyCodeB**, then two folders with hello same names would contain hello necessary binaries for each code package.</span></span>

## <a name="use-setupentrypoint"></a><span data-ttu-id="bc09d-110">Usar SetupEntrypoint</span><span class="sxs-lookup"><span data-stu-id="bc09d-110">Use SetupEntryPoint</span></span>
<span data-ttu-id="bc09d-111">Escenarios típicos de uso **SetupEntryPoint** se da cuando necesita toorun un ejecutable antes de iniciar servicio de Hola o necesita tooperform una operación con privilegios elevados.</span><span class="sxs-lookup"><span data-stu-id="bc09d-111">Typical scenarios for using **SetupEntryPoint** are when you need toorun an executable before hello service starts or you need tooperform an operation with elevated privileges.</span></span> <span data-ttu-id="bc09d-112">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="bc09d-112">For example:</span></span>

* <span data-ttu-id="bc09d-113">Configurar e inicializar variables de entorno que Hola necesidades ejecutable del servicio.</span><span class="sxs-lookup"><span data-stu-id="bc09d-113">Setting up and initializing environment variables that hello service executable needs.</span></span> <span data-ttu-id="bc09d-114">No es ejecutables tooonly limitado escritos a través de los modelos de programación de Service Fabric Hola.</span><span class="sxs-lookup"><span data-stu-id="bc09d-114">It is not limited tooonly executables written via hello Service Fabric programming models.</span></span> <span data-ttu-id="bc09d-115">Por ejemplo, npm.exe necesita algunas variables de entorno configuradas para implementar una aplicación node.js.</span><span class="sxs-lookup"><span data-stu-id="bc09d-115">For example, npm.exe needs some environment variables configured for deploying a node.js application.</span></span>
* <span data-ttu-id="bc09d-116">Configuración del control de acceso mediante la instalación de certificados de seguridad.</span><span class="sxs-lookup"><span data-stu-id="bc09d-116">Setting up access control by installing security certificates.</span></span>

<span data-ttu-id="bc09d-117">Para obtener más información acerca de cómo hello tooconfigure **SetupEntryPoint**, consulte [configurar Directiva de Hola para un punto de entrada del programa de instalación de servicio](service-fabric-application-runas-security.md)</span><span class="sxs-lookup"><span data-stu-id="bc09d-117">For more information on how tooconfigure hello **SetupEntryPoint**, see [Configure hello policy for a service setup entry point](service-fabric-application-runas-security.md)</span></span>

<a id="Package-App"></a>
## <a name="configure"></a><span data-ttu-id="bc09d-118">Configuración</span><span class="sxs-lookup"><span data-stu-id="bc09d-118">Configure</span></span>
### <a name="build-a-package-by-using-visual-studio"></a><span data-ttu-id="bc09d-119">Crear un paquete mediante Visual Studio</span><span class="sxs-lookup"><span data-stu-id="bc09d-119">Build a package by using Visual Studio</span></span>
<span data-ttu-id="bc09d-120">Si usa Visual Studio 2015 toocreate su aplicación, puede usar Hola paquete comando tooautomatically crear un paquete que coincida con el diseño de Hola se ha descrito anteriormente.</span><span class="sxs-lookup"><span data-stu-id="bc09d-120">If you use Visual Studio 2015 toocreate your application, you can use hello Package command tooautomatically create a package that matches hello layout described above.</span></span>

<span data-ttu-id="bc09d-121">toocreate un paquete, haga clic en proyecto de aplicación de hello en el Explorador de soluciones y elija el comando de paquete de hello, tal y como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="bc09d-121">toocreate a package, right-click hello application project in Solution Explorer and choose hello Package command, as shown below:</span></span>

![Empaquetado de una aplicación con Visual Studio][vs-package-command]

<span data-ttu-id="bc09d-123">Una vez completado empaquetado, puede encontrar Hola ubicación del paquete de Hola Hola **salida** ventana.</span><span class="sxs-lookup"><span data-stu-id="bc09d-123">When packaging is complete, you can find hello location of hello package in hello **Output** window.</span></span> <span data-ttu-id="bc09d-124">paso de empaquetado de Hola se produce automáticamente al implementar o depurar la aplicación en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bc09d-124">hello packaging step occurs automatically when you deploy or debug your application in Visual Studio.</span></span>

### <a name="build-a-package-by-command-line"></a><span data-ttu-id="bc09d-125">Creación de un paquete mediante la línea de comandos</span><span class="sxs-lookup"><span data-stu-id="bc09d-125">Build a package by command line</span></span>
<span data-ttu-id="bc09d-126">También es posible tooprogrammatically paquete una aplicación mediante `msbuild.exe`.</span><span class="sxs-lookup"><span data-stu-id="bc09d-126">It is also possible tooprogrammatically package up your application using `msbuild.exe`.</span></span> <span data-ttu-id="bc09d-127">Bajo el paraguas de hello, Visual Studio se está ejecutando, por lo que la salida de hello es la misma.</span><span class="sxs-lookup"><span data-stu-id="bc09d-127">Under hello hood, Visual Studio is running it so hello output is same.</span></span>

```shell
D:\Temp> msbuild HelloWorld.sfproj /t:Package
```

## <a name="test-hello-package"></a><span data-ttu-id="bc09d-128">Paquete de Hola de prueba</span><span class="sxs-lookup"><span data-stu-id="bc09d-128">Test hello package</span></span>
<span data-ttu-id="bc09d-129">Puede comprobar la estructura del paquete Hola localmente a través de PowerShell mediante el uso de hello [ServiceFabricApplicationPackage prueba](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) comando.</span><span class="sxs-lookup"><span data-stu-id="bc09d-129">You can verify hello package structure locally through PowerShell by using hello [Test-ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) command.</span></span>
<span data-ttu-id="bc09d-130">Este comando comprueba si existen problemas de análisis de manifiestos y verifica todas las referencias.</span><span class="sxs-lookup"><span data-stu-id="bc09d-130">This command checks for manifest parsing issues and verify all references.</span></span> <span data-ttu-id="bc09d-131">Este comando sólo comprueba la corrección estructural de Hola de hello directorios y archivos de paquete de Hola.</span><span class="sxs-lookup"><span data-stu-id="bc09d-131">This command only verifies hello structural correctness of hello directories and files in hello package.</span></span>
<span data-ttu-id="bc09d-132">Información no comprueba cualquier elemento de contenido de los paquetes de código o datos de hello más allá de la comprobación de que todos los archivos necesarios están presentes.</span><span class="sxs-lookup"><span data-stu-id="bc09d-132">It doesn't verify any of hello code or data package contents beyond checking that all necessary files are present.</span></span>

```
PS D:\temp> Test-ServiceFabricApplicationPackage .\MyApplicationType
False
Test-ServiceFabricApplicationPackage : hello EntryPoint MySetup.bat is not found.
FileName: C:\Users\servicefabric\AppData\Local\Temp\TestApplicationPackage_7195781181\nrri205a.e2h\MyApplicationType\MyServiceManifest\ServiceManifest.xml
```

<span data-ttu-id="bc09d-133">Este error muestra ese hello *MySetup.bat* archivo hace referencia en el manifiesto del servicio de hello **SetupEntryPoint** no está en el paquete de código de hello.</span><span class="sxs-lookup"><span data-stu-id="bc09d-133">This error shows that hello *MySetup.bat* file referenced in hello service manifest **SetupEntryPoint** is missing from hello code package.</span></span> <span data-ttu-id="bc09d-134">Después de agrega el archivo que falta hello, pasa la comprobación de aplicación Hola:</span><span class="sxs-lookup"><span data-stu-id="bc09d-134">After hello missing file is added, hello application verification passes:</span></span>

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

<span data-ttu-id="bc09d-135">Si la aplicación tiene [parámetros de aplicación](service-fabric-manage-multiple-environment-app-configuration.md) definidos, puede pasarlos en [Test-ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) para realizar una validación adecuada.</span><span class="sxs-lookup"><span data-stu-id="bc09d-135">If your application has [application parameters](service-fabric-manage-multiple-environment-app-configuration.md) defined, you can pass them in [Test-ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) for proper validation.</span></span>

<span data-ttu-id="bc09d-136">Si conoce el clúster de Hola donde se implementará la aplicación hello, se recomienda pasar en hello `ImageStoreConnectionString` parámetro.</span><span class="sxs-lookup"><span data-stu-id="bc09d-136">If you know hello cluster where hello application will be deployed, it is recommended you pass in hello `ImageStoreConnectionString` parameter.</span></span> <span data-ttu-id="bc09d-137">En este caso, también se valida el paquete de hello con versiones anteriores de la aplicación hello que se están ejecutando en el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="bc09d-137">In this case, hello package is also validated against previous versions of hello application that are already running in hello cluster.</span></span> <span data-ttu-id="bc09d-138">Por ejemplo, validación de hello puede detectar si un paquete con hello misma versión, pero distinto contenido ya se había implementado.</span><span class="sxs-lookup"><span data-stu-id="bc09d-138">For example, hello validation can detect whether a package with hello same version but different content was already deployed.</span></span>  

<span data-ttu-id="bc09d-139">Una vez que la aplicación hello se empaqueta correctamente y pasa la validación, evaluar basándose en tamaño de Hola y número de Hola de archivos si es necesaria la compresión.</span><span class="sxs-lookup"><span data-stu-id="bc09d-139">Once hello application is packaged correctly and passes validation, evaluate based on hello size and hello number of files if compression is needed.</span></span>

## <a name="compress-a-package"></a><span data-ttu-id="bc09d-140">Compresión de un paquete</span><span class="sxs-lookup"><span data-stu-id="bc09d-140">Compress a package</span></span>
<span data-ttu-id="bc09d-141">Cuando un paquete es grande o tiene muchos archivos, puede comprimirlo para acelerar la implementación.</span><span class="sxs-lookup"><span data-stu-id="bc09d-141">When a package is large or has many files, you can compress it for faster deployment.</span></span> <span data-ttu-id="bc09d-142">La compresión reduce el número de Hola de archivos y el tamaño de paquete de Hola.</span><span class="sxs-lookup"><span data-stu-id="bc09d-142">Compression reduces hello number of files and hello package size.</span></span>
<span data-ttu-id="bc09d-143">Para un paquete de aplicación comprimidos, [paquete de aplicación de carga hello](service-fabric-deploy-remove-applications.md#upload-the-application-package) puede tardar ya comparados toouploading Hola paquete sin comprimir (especialmente si el tiempo de compresión se tienen en cuenta), pero [registrar](service-fabric-deploy-remove-applications.md#register-the-application-package) y [tipo anulación del registro de la aplicación hello](service-fabric-deploy-remove-applications.md#unregister-an-application-type) son más rápidos para un paquete de aplicación comprimido.</span><span class="sxs-lookup"><span data-stu-id="bc09d-143">For a compressed application package, [Uploading hello application package](service-fabric-deploy-remove-applications.md#upload-the-application-package) may take longer compared toouploading hello uncompressed package (specially if compression time is factored in), but [registering](service-fabric-deploy-remove-applications.md#register-the-application-package) and [un-registering hello application type](service-fabric-deploy-remove-applications.md#unregister-an-application-type) are faster for a compressed application package.</span></span>

<span data-ttu-id="bc09d-144">mecanismo de implementación de Hello es el mismo para los paquetes comprimidos y sin comprimir.</span><span class="sxs-lookup"><span data-stu-id="bc09d-144">hello deployment mechanism is same for compressed and uncompressed packages.</span></span> <span data-ttu-id="bc09d-145">Si el paquete de saludo se comprime, se almacena como tal en el almacén de imágenes de clúster de Hola y está comprimida en el nodo de hello antes de ejecuta la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="bc09d-145">If hello package is compressed, it is stored as such in hello cluster image store and it's uncompressed on hello node before hello application is run.</span></span>
<span data-ttu-id="bc09d-146">compresión de Hello reemplaza paquete de Service Fabric válido Hola con la versión comprimida de Hola.</span><span class="sxs-lookup"><span data-stu-id="bc09d-146">hello compression replaces hello valid Service Fabric package with hello compressed version.</span></span> <span data-ttu-id="bc09d-147">carpeta de Hello debe permitir los permisos de escritura.</span><span class="sxs-lookup"><span data-stu-id="bc09d-147">hello folder must allow write permissions.</span></span> <span data-ttu-id="bc09d-148">La ejecución de la compresión en un paquete ya comprimido no produce ningún cambio.</span><span class="sxs-lookup"><span data-stu-id="bc09d-148">Running compression on an already compressed package yields no changes.</span></span>

<span data-ttu-id="bc09d-149">Puede comprimir un paquete mediante la ejecución de comandos de Powershell de hello [copia ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) con `CompressPackage` cambiar.</span><span class="sxs-lookup"><span data-stu-id="bc09d-149">You can compress a package by running hello Powershell command [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) with `CompressPackage` switch.</span></span> <span data-ttu-id="bc09d-150">Puede descomprimir Hola empaquetar con hello mismo comando, mediante `UncompressPackage` cambiar.</span><span class="sxs-lookup"><span data-stu-id="bc09d-150">You can uncompress hello package with hello same command, using `UncompressPackage` switch.</span></span>

<span data-ttu-id="bc09d-151">Hello siguiente comando comprime paquete Hola sin copiar toohello almacén de imágenes.</span><span class="sxs-lookup"><span data-stu-id="bc09d-151">hello following command compresses hello package without copying it toohello image store.</span></span> <span data-ttu-id="bc09d-152">Puede copiar un paquete comprimido tooone o más clústeres de Service Fabric, según sea necesario, con [copia ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) sin hello `SkipCopy` marca.</span><span class="sxs-lookup"><span data-stu-id="bc09d-152">You can copy a compressed package tooone or more Service Fabric clusters, as needed, using [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) without hello `SkipCopy` flag.</span></span>
<span data-ttu-id="bc09d-153">paquete de Hello ahora incluye archivos comprimidos para hello `code`, `config`, y `data` paquetes.</span><span class="sxs-lookup"><span data-stu-id="bc09d-153">hello package now includes zipped files for hello `code`, `config`, and `data` packages.</span></span> <span data-ttu-id="bc09d-154">manifiesto de aplicación de Hola y Hola manifiestos de servicio no se comprimen, porque son necesarios para muchas operaciones internas (por ejemplo, uso compartido, extracción de nombre y la versión del tipo de aplicación para determinadas validaciones de paquete).</span><span class="sxs-lookup"><span data-stu-id="bc09d-154">hello application manifest and hello service manifests are not zipped, because they are needed for many internal operations (like package sharing, application type name and version extraction for certain validations).</span></span>
<span data-ttu-id="bc09d-155">Manifiestos de hello en zip haría que estas operaciones ineficaces.</span><span class="sxs-lookup"><span data-stu-id="bc09d-155">Zipping hello manifests would make these operations inefficient.</span></span>

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

<span data-ttu-id="bc09d-156">Como alternativa, puede comprimir y copiar el paquete Hola con [ServiceFabricApplicationPackage copia](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) en un solo paso.</span><span class="sxs-lookup"><span data-stu-id="bc09d-156">Alternatively, you can compress and copy hello package with [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) in one step.</span></span>
<span data-ttu-id="bc09d-157">Si el paquete de hello es grande, proporcione una hora de tooallow tiempo de espera lo suficientemente alto como para la compresión del paquete hello y clúster de hello carga toohello.</span><span class="sxs-lookup"><span data-stu-id="bc09d-157">If hello package is large, provide a high enough timeout tooallow time for both hello package compression and hello upload toohello cluster.</span></span>
```
PS D:\temp> Copy-ServiceFabricApplicationPackage -ApplicationPackagePath .\MyApplicationType -ApplicationPackagePathInImageStore MyApplicationType -ImageStoreConnectionString fabric:ImageStore -CompressPackage -TimeoutSec 5400
```

<span data-ttu-id="bc09d-158">Internamente, Service Fabric calcula las sumas de comprobación para los paquetes de aplicación hello para la validación.</span><span class="sxs-lookup"><span data-stu-id="bc09d-158">Internally, Service Fabric computes checksums for hello application packages for validation.</span></span> <span data-ttu-id="bc09d-159">Cuando utilice la compresión, se calculan las sumas de comprobación de hello en hello las versiones comprimida de cada paquete.</span><span class="sxs-lookup"><span data-stu-id="bc09d-159">When using compression, hello checksums are computed on hello zipped versions of each package.</span></span>
<span data-ttu-id="bc09d-160">Si ha copiado una versión sin comprimir el paquete de aplicación, y desea compresión toouse para hello mismo paquete, debe cambiar las versiones de Hola de hello `code`, `config`, y `data` incoherencia de suma de comprobación de paquetes tooavoid.</span><span class="sxs-lookup"><span data-stu-id="bc09d-160">If you copied an uncompressed version of your application package, and you want toouse compression for hello same package, you must change hello versions of hello `code`, `config`, and `data` packages tooavoid checksum mismatch.</span></span> <span data-ttu-id="bc09d-161">Si los paquetes de saludo se modifican, en lugar de cambiar la versión de hello, puede usar [diferencias aprovisionamiento](service-fabric-application-upgrade-advanced.md).</span><span class="sxs-lookup"><span data-stu-id="bc09d-161">If hello packages are unchanged, instead of changing hello version, you can use [diff provisioning](service-fabric-application-upgrade-advanced.md).</span></span> <span data-ttu-id="bc09d-162">Con esta opción, no incluyen paquetes de saludo sin cambios en su lugar la referencia de manifiesto del servicio Hola.</span><span class="sxs-lookup"><span data-stu-id="bc09d-162">With this option, do not include hello unchanged package instead reference it from hello service manifest.</span></span>

<span data-ttu-id="bc09d-163">De forma similar, si carga una versión comprimida del paquete de Hola y desea toouse un paquete sin comprimir, debe actualizar incoherencia de suma de comprobación de hello versiones tooavoid Hola.</span><span class="sxs-lookup"><span data-stu-id="bc09d-163">Similarly, if you uploaded a compressed version of hello package and you want toouse an uncompressed package, you must update hello versions tooavoid hello checksum mismatch.</span></span>

<span data-ttu-id="bc09d-164">Hello paquete es ahora empaqueta correctamente, validar y comprimido (si es necesario), por lo que está listo para [implementación](service-fabric-deploy-remove-applications.md) tooone o del tejido de servicio más clústeres.</span><span class="sxs-lookup"><span data-stu-id="bc09d-164">hello package is now packaged correctly, validated, and compressed (if needed), so it is ready for [deployment](service-fabric-deploy-remove-applications.md) tooone or more Service Fabric clusters.</span></span>

### <a name="compress-packages-when-deploying-using-visual-studio"></a><span data-ttu-id="bc09d-165">Compresión de paquetes al implementar con Visual Studio</span><span class="sxs-lookup"><span data-stu-id="bc09d-165">Compress packages when deploying using Visual Studio</span></span>
<span data-ttu-id="bc09d-166">Puede indicar a paquetes de Visual Studio toocompress sobre la implementación, mediante la adición de hello `CopyPackageParameters` tooyour elemento perfil de publicación y establezca hello `CompressPackage` atributo demasiado`true`.</span><span class="sxs-lookup"><span data-stu-id="bc09d-166">You can instruct Visual Studio toocompress packages on deployment, by adding hello `CopyPackageParameters` element tooyour publish profile, and set hello `CompressPackage` attribute too`true`.</span></span>

``` xml
    <PublishProfile xmlns="http://schemas.microsoft.com/2015/05/fabrictools">
        <ClusterConnectionParameters ConnectionEndpoint="mycluster.westus.cloudapp.azure.com" />
        <ApplicationParameterFile Path="..\ApplicationParameters\Cloud.xml" />
        <CopyPackageParameters CompressPackage="true"/>
    </PublishProfile>
```

## <a name="next-steps"></a><span data-ttu-id="bc09d-167">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="bc09d-167">Next steps</span></span>
<span data-ttu-id="bc09d-168">[Implementar y quitar aplicaciones] [ 10] describe cómo toouse instancias de la aplicación de toomanage de PowerShell</span><span class="sxs-lookup"><span data-stu-id="bc09d-168">[Deploy and remove applications][10] describes how toouse PowerShell toomanage application instances</span></span>

<span data-ttu-id="bc09d-169">[Administrar parámetros de la aplicación para varios entornos] [ 11] describe cómo tooconfigure parámetros y variables de entorno para las instancias de aplicación diferente.</span><span class="sxs-lookup"><span data-stu-id="bc09d-169">[Managing application parameters for multiple environments][11] describes how tooconfigure parameters and environment variables for different application instances.</span></span>

<span data-ttu-id="bc09d-170">[Configurar directivas de seguridad para la aplicación] [ 12] describe cómo toorun servicios con acceso de toorestrict de directivas de seguridad.</span><span class="sxs-lookup"><span data-stu-id="bc09d-170">[Configure security policies for your application][12] describes how toorun services under security policies toorestrict access.</span></span>

<!--Image references-->
[vs-package-command]: ./media/service-fabric-package-apps/vs-package-command.png

<!--Link references--In actual articles, you only need a single period before hello slash-->
[10]: service-fabric-deploy-remove-applications.md
[11]: service-fabric-manage-multiple-environment-app-configuration.md
[12]: service-fabric-application-runas-security.md
