---
title: "una aplicación de Node.js que usa MongoDB aaaDeploy | Documentos de Microsoft"
description: "Tutorial sobre cómo toopackage varios clúster invitado ejecutables toodeploy tooan Azure Service Fabric"
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: b76bb756-c1ba-49f9-9666-e9807cf8f92f
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/02/2017
ms.author: msfussell;mikhegn
ms.openlocfilehash: 2775080f0d9d42d6ba15cca911e23067106be26d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-multiple-guest-executables"></a><span data-ttu-id="cb54b-103">Implementación de varios ejecutables invitados</span><span class="sxs-lookup"><span data-stu-id="cb54b-103">Deploy multiple guest executables</span></span>
<span data-ttu-id="cb54b-104">Este artículo se muestra cómo toopackage e implementar varios invitado ejecutables tooAzure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="cb54b-104">This article shows how toopackage and deploy multiple guest executables tooAzure Service Fabric.</span></span> <span data-ttu-id="cb54b-105">Para compilar e implementar un único paquete de Service Fabric leen cómo demasiado[implementar un tejido de invitado ejecutable tooService](service-fabric-deploy-existing-app.md).</span><span class="sxs-lookup"><span data-stu-id="cb54b-105">For building and deploying a single Service Fabric package read how too[deploy a guest executable tooService Fabric](service-fabric-deploy-existing-app.md).</span></span>

<span data-ttu-id="cb54b-106">Aunque este tutorial muestra cómo toodeploy una aplicación con un front-end Node.js que usa MongoDB como almacén de datos de hello, puede aplicar aplicación tooany de hello pasos que tiene dependencias en otra aplicación.</span><span class="sxs-lookup"><span data-stu-id="cb54b-106">While this walkthrough shows how toodeploy an application with a Node.js front end that uses MongoDB as hello data store, you can apply hello steps tooany application that has dependencies on another application.</span></span>   

<span data-ttu-id="cb54b-107">Puede usar el paquete de aplicación de Hola de tooproduce de Visual Studio que contiene varios archivos ejecutables de invitado.</span><span class="sxs-lookup"><span data-stu-id="cb54b-107">You can use Visual Studio tooproduce hello application package that contains multiple guest executables.</span></span> <span data-ttu-id="cb54b-108">Vea [toopackage en Visual Studio una aplicación existente](service-fabric-deploy-existing-app.md).</span><span class="sxs-lookup"><span data-stu-id="cb54b-108">See [Using Visual Studio toopackage an existing application](service-fabric-deploy-existing-app.md).</span></span> <span data-ttu-id="cb54b-109">Después de haber agregado el primer ejecutable de invitado hello, haga clic en proyecto de aplicación de Hola y Hola seleccione **Agregar -> servicio de Fabric de servicio nueva** tooadd Hola segunda invitado proyecto ejecutable toohello solución.</span><span class="sxs-lookup"><span data-stu-id="cb54b-109">After you have added hello first guest executable, right click on hello application project and select hello **Add->New Service Fabric service** tooadd hello second guest executable project toohello solution.</span></span> <span data-ttu-id="cb54b-110">Nota: Si elige toolink origen de Hola Hola proyecto de Visual Studio, compilar la solución de Visual Studio de hello, asegurará de que el paquete de aplicación es una toodate con cambios en el origen de Hola.</span><span class="sxs-lookup"><span data-stu-id="cb54b-110">Note: If you choose toolink hello source in hello Visual Studio project, building hello Visual Studio solution, will make sure that your application package is up toodate with changes in hello source.</span></span> 

## <a name="samples"></a><span data-ttu-id="cb54b-111">Muestras</span><span class="sxs-lookup"><span data-stu-id="cb54b-111">Samples</span></span>
* [<span data-ttu-id="cb54b-112">Ejemplo para empaquetar e implementar un archivo ejecutable invitado</span><span class="sxs-lookup"><span data-stu-id="cb54b-112">Sample for packaging and deploying a guest executable</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [<span data-ttu-id="cb54b-113">Ejemplo de dos archivos ejecutables (C# y nodejs) de invitado comunicarse a través del servicio de nomenclatura de hello con REST</span><span class="sxs-lookup"><span data-stu-id="cb54b-113">Sample of two guest executables (C# and nodejs) communicating via hello Naming service using REST</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-containers)

## <a name="manually-package-hello-multiple-guest-executable-application"></a><span data-ttu-id="cb54b-114">Manualmente el paquete Hola varias aplicaciones ejecutables de invitado</span><span class="sxs-lookup"><span data-stu-id="cb54b-114">Manually package hello multiple guest executable application</span></span>
<span data-ttu-id="cb54b-115">O bien puede empaquetar manualmente invitado Hola ejecutable.</span><span class="sxs-lookup"><span data-stu-id="cb54b-115">Alternatively you can manually package hello guest executable.</span></span> <span data-ttu-id="cb54b-116">Para hacer el empaquetado manual de hello, este artículo usa la herramienta de empaquetado de Service Fabric hello, que está disponible en [http://aka.ms/servicefabricpacktool](http://aka.ms/servicefabricpacktool).</span><span class="sxs-lookup"><span data-stu-id="cb54b-116">For hello manual packaging, this article uses hello Service Fabric packaging tool, which is available at [http://aka.ms/servicefabricpacktool](http://aka.ms/servicefabricpacktool).</span></span>

### <a name="packaging-hello-nodejs-application"></a><span data-ttu-id="cb54b-117">Hola de empaquetado aplicación Node.js</span><span class="sxs-lookup"><span data-stu-id="cb54b-117">Packaging hello Node.js application</span></span>
<span data-ttu-id="cb54b-118">En este artículo se da por supuesto que no está instalado Node.js en nodos de hello en clúster de Service Fabric Hola.</span><span class="sxs-lookup"><span data-stu-id="cb54b-118">This article assumes that Node.js is not installed on hello nodes in hello Service Fabric cluster.</span></span> <span data-ttu-id="cb54b-119">En consecuencia, es necesario tooadd Node.exe el directorio de raíz de toohello de la aplicación de nodo antes de empaquetar.</span><span class="sxs-lookup"><span data-stu-id="cb54b-119">As a consequence, you need tooadd Node.exe toohello root directory of your node application before packaging.</span></span> <span data-ttu-id="cb54b-120">estructura de directorios de Hola de aplicación de Node.js de hello (mediante el marco de trabajo de web Express y motor de plantillas Jade) debería ser similar toohello uno a continuación:</span><span class="sxs-lookup"><span data-stu-id="cb54b-120">hello directory structure of hello Node.js application (using Express web framework and Jade template engine) should look similar toohello one below:</span></span>

```
|-- NodeApplication
    |-- bin
        |-- www
    |-- node_modules
        |-- .bin
        |-- express
        |-- jade
        |-- etc.
    |-- public
        |-- images
        |-- etc.
    |-- routes
        |-- index.js
        |-- users.js
    |-- views
        |-- index.jade
        |-- etc.
    |-- app.js
    |-- package.json
    |-- node.exe
```

<span data-ttu-id="cb54b-121">El siguiente paso, creará un paquete de aplicación para hello aplicación Node.js.</span><span class="sxs-lookup"><span data-stu-id="cb54b-121">As a next step, you create an application package for hello Node.js application.</span></span> <span data-ttu-id="cb54b-122">código de Hello siguiente crea un paquete de aplicación de Service Fabric que contiene la aplicación de Node.js Hola.</span><span class="sxs-lookup"><span data-stu-id="cb54b-122">hello code below creates a Service Fabric application package that contains hello Node.js application.</span></span>

```
.\ServiceFabricAppPackageUtil.exe /source:'[yourdirectory]\MyNodeApplication' /target:'[yourtargetdirectory] /appname:NodeService /exe:'node.exe' /ma:'bin/www' /AppType:NodeAppType
```

<span data-ttu-id="cb54b-123">A continuación se muestra una descripción de los parámetros de Hola que se utilizan:</span><span class="sxs-lookup"><span data-stu-id="cb54b-123">Below is a description of hello parameters that are being used:</span></span>

* <span data-ttu-id="cb54b-124">**/ source** puntos toohello directorio de aplicación Hola que debe empaquetarse.</span><span class="sxs-lookup"><span data-stu-id="cb54b-124">**/source** points toohello directory of hello application that should be packaged.</span></span>
* <span data-ttu-id="cb54b-125">**/ target** define directorio hello en qué Hola se debe crear el paquete.</span><span class="sxs-lookup"><span data-stu-id="cb54b-125">**/target** defines hello directory in which hello package should be created.</span></span> <span data-ttu-id="cb54b-126">Este directorio tiene toobe diferente hello directorio de origen.</span><span class="sxs-lookup"><span data-stu-id="cb54b-126">This directory has toobe different from hello source directory.</span></span>
* <span data-ttu-id="cb54b-127">**/ appname** define el nombre de la aplicación hello de aplicación existente de Hola.</span><span class="sxs-lookup"><span data-stu-id="cb54b-127">**/appname** defines hello application name of hello existing application.</span></span> <span data-ttu-id="cb54b-128">Es importante toounderstand que esto traduce toohello nombre del servicio en el manifiesto de hello y no toohello nombre de aplicación de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="cb54b-128">It's important toounderstand that this translates toohello service name in hello manifest, and not toohello Service Fabric application name.</span></span>
* <span data-ttu-id="cb54b-129">**/exe** define Hola ejecutable que Service Fabric es ya debería estar toolaunch, en este caso `node.exe`.</span><span class="sxs-lookup"><span data-stu-id="cb54b-129">**/exe** defines hello executable that Service Fabric is supposed toolaunch, in this case `node.exe`.</span></span>
* <span data-ttu-id="cb54b-130">**/maen** define el argumento de Hola que está siendo usado toolaunch Hola ejecutable.</span><span class="sxs-lookup"><span data-stu-id="cb54b-130">**/ma** defines hello argument that is being used toolaunch hello executable.</span></span> <span data-ttu-id="cb54b-131">A medida que no está instalado Node.js, Service Fabric debe servidor web de toolaunch hello Node.js ejecutando `node.exe bin/www`.</span><span class="sxs-lookup"><span data-stu-id="cb54b-131">As Node.js is not installed, Service Fabric needs toolaunch hello Node.js web server by executing `node.exe bin/www`.</span></span>  <span data-ttu-id="cb54b-132">`/ma:'bin/www'`indica a toouse de herramienta de empaquetado de hello `bin/ma` como argumento de Hola para node.exe.</span><span class="sxs-lookup"><span data-stu-id="cb54b-132">`/ma:'bin/www'` tells hello packaging tool toouse `bin/ma` as hello argument for node.exe.</span></span>
* <span data-ttu-id="cb54b-133">**/ AppType** define el nombre del tipo de aplicación de hello Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="cb54b-133">**/AppType** defines hello Service Fabric application type name.</span></span>

<span data-ttu-id="cb54b-134">Si examina el directorio toohello que especificó en el parámetro de hello/Target, puede ver que esa herramienta Hola ha creado un paquete de Service Fabric totalmente operativo tal y como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="cb54b-134">If you browse toohello directory that was specified in hello /target parameter, you can see that hello tool has created a fully functioning Service Fabric package as shown below:</span></span>

```
|--[yourtargetdirectory]
    |-- NodeApplication
        |-- C
              |-- bin
              |-- data
              |-- node_modules
              |-- public
              |-- routes
              |-- views
              |-- app.js
              |-- package.json
              |-- node.exe
        |-- config
              |--Settings.xml
        |-- ServiceManifest.xml
    |-- ApplicationManifest.xml
```
<span data-ttu-id="cb54b-135">Hola ServiceManifest.xml generado tiene ahora una sección que describe cómo debería iniciarse servidor web de Node.js de hello, como se muestra en el siguiente fragmento de código de hello:</span><span class="sxs-lookup"><span data-stu-id="cb54b-135">hello generated ServiceManifest.xml now has a section that describes how hello Node.js web server should be launched, as shown in hello code snippet below:</span></span>

```xml
<CodePackage Name="C" Version="1.0">
    <EntryPoint>
        <ExeHost>
            <Program>node.exe</Program>
            <Arguments>'bin/www'</Arguments>
            <WorkingFolder>CodePackage</WorkingFolder>
        </ExeHost>
    </EntryPoint>
</CodePackage>
```
<span data-ttu-id="cb54b-136">En este ejemplo, servidor web de Node.js de hello escucha a tooport 3000, por lo que necesita información de extremo de hello tooupdate en archivo de hello ServiceManifest.xml tal y como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="cb54b-136">In this sample, hello Node.js web server listens tooport 3000, so you need tooupdate hello endpoint information in hello ServiceManifest.xml file as shown below.</span></span>   

```xml
<Resources>
      <Endpoints>
         <Endpoint Name="NodeServiceEndpoint" Protocol="http" Port="3000" Type="Input" />
      </Endpoints>
</Resources>
```
### <a name="packaging-hello-mongodb-application"></a><span data-ttu-id="cb54b-137">Hola empaquetar aplicación de MongoDB</span><span class="sxs-lookup"><span data-stu-id="cb54b-137">Packaging hello MongoDB application</span></span>
<span data-ttu-id="cb54b-138">Ahora que ha empaquetado aplicación Node.js de hello, puede seguir adelante y MongoDB del paquete.</span><span class="sxs-lookup"><span data-stu-id="cb54b-138">Now that you have packaged hello Node.js application, you can go ahead and package MongoDB.</span></span> <span data-ttu-id="cb54b-139">Como se mencionó antes, pasos de Hola que atraviesan ahora no son tooNode.js específico y MongoDB.</span><span class="sxs-lookup"><span data-stu-id="cb54b-139">As mentioned before, hello steps that you go through now are not specific tooNode.js and MongoDB.</span></span> <span data-ttu-id="cb54b-140">De hecho, se aplican a las aplicaciones de tooall que pretenden toobe empaquetada como una aplicación de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="cb54b-140">In fact, they apply tooall applications that are meant toobe packaged together as one Service Fabric application.</span></span>  

<span data-ttu-id="cb54b-141">toopackage MongoDB, desea toomake seguro que empaquetar Mongod.exe y Mongo.exe.</span><span class="sxs-lookup"><span data-stu-id="cb54b-141">toopackage MongoDB, you want toomake sure you package Mongod.exe and Mongo.exe.</span></span> <span data-ttu-id="cb54b-142">Ambos archivos binarios se encuentran en hello `bin` directorio de su directorio de instalación de MongoDB.</span><span class="sxs-lookup"><span data-stu-id="cb54b-142">Both binaries are located in hello `bin` directory of your MongoDB installation directory.</span></span> <span data-ttu-id="cb54b-143">estructura de directorios de Hello tiene un aspecto similar toohello uno a continuación.</span><span class="sxs-lookup"><span data-stu-id="cb54b-143">hello directory structure looks similar toohello one below.</span></span>

```
|-- MongoDB
    |-- bin
        |-- mongod.exe
        |-- mongo.exe
        |-- anybinary.exe
```
<span data-ttu-id="cb54b-144">Service Fabric necesita toostart MongoDB con un toohello similar de comando uno siguiente, por lo que necesita toouse hello `/ma` parámetro al empaquetar MongoDB.</span><span class="sxs-lookup"><span data-stu-id="cb54b-144">Service Fabric needs toostart MongoDB with a command similar toohello one below, so you need toouse hello `/ma` parameter when packaging MongoDB.</span></span>

```
mongod.exe --dbpath [path toodata]
```
> [!NOTE]
> <span data-ttu-id="cb54b-145">no se va a conservar datos Hello en caso de hello de un error de nodo si coloca el directorio de datos de MongoDB hello en el directorio local de hello del nodo de Hola.</span><span class="sxs-lookup"><span data-stu-id="cb54b-145">hello data is not being preserved in hello case of a node failure if you put hello MongoDB data directory on hello local directory of hello node.</span></span> <span data-ttu-id="cb54b-146">Debe usar almacenamiento duradero o implementar una réplica de MongoDB establecer orden tooprevent pérdida de datos.</span><span class="sxs-lookup"><span data-stu-id="cb54b-146">You should either use durable storage or implement a MongoDB replica set in order tooprevent data loss.</span></span>  
>
>

<span data-ttu-id="cb54b-147">En el shell de comandos de PowerShell o hello, ejecutamos la herramienta de empaquetado de hello con hello parámetros siguientes:</span><span class="sxs-lookup"><span data-stu-id="cb54b-147">In PowerShell or hello command shell, we run hello packaging tool with hello following parameters:</span></span>

```
.\ServiceFabricAppPackageUtil.exe /source: [yourdirectory]\MongoDB' /target:'[yourtargetdirectory]' /appname:MongoDB /exe:'bin\mongod.exe' /ma:'--dbpath [path toodata]' /AppType:NodeAppType
```

<span data-ttu-id="cb54b-148">Orden tooadd MongoDB tooyour Service Fabric paquete de aplicación, deberá toomake seguro ese parámetro / Target Hola señala toohello mismo directorio que ya contiene el manifiesto de aplicación Hola junto con la aplicación de hello Node.js.</span><span class="sxs-lookup"><span data-stu-id="cb54b-148">In order tooadd MongoDB tooyour Service Fabric application package, you need toomake sure that hello /target parameter points toohello same directory that already contains hello application manifest along with hello Node.js application.</span></span> <span data-ttu-id="cb54b-149">También necesita toomake seguro de que está usando Hola ApplicationType homónimas.</span><span class="sxs-lookup"><span data-stu-id="cb54b-149">You also need toomake sure that you are using hello same ApplicationType name.</span></span>

<span data-ttu-id="cb54b-150">Vamos a examinar el directorio toohello y examine qué herramienta Hola creada.</span><span class="sxs-lookup"><span data-stu-id="cb54b-150">Let's browse toohello directory and examine what hello tool has created.</span></span>

```
|--[yourtargetdirectory]
    |-- MyNodeApplication
    |-- MongoDB
        |-- C
            |--bin
                |-- mongod.exe
                |-- mongo.exe
                |-- etc.
        |-- config
            |--Settings.xml
        |-- ServiceManifest.xml
    |-- ApplicationManifest.xml
```
<span data-ttu-id="cb54b-151">Como puede ver, herramienta de hello agrega un nuevo directorio de toohello de carpeta, MongoDB, que contiene los archivos binarios de hello MongoDB.</span><span class="sxs-lookup"><span data-stu-id="cb54b-151">As you can see, hello tool added a new folder, MongoDB, toohello directory that contains hello MongoDB binaries.</span></span> <span data-ttu-id="cb54b-152">Si abre hello `ApplicationManifest.xml` archivo, puede ver ese paquete Hola ahora contiene aplicación Node.js de hello y MongoDB.</span><span class="sxs-lookup"><span data-stu-id="cb54b-152">If you open hello `ApplicationManifest.xml` file, you can see that hello package now contains both hello Node.js application and MongoDB.</span></span> <span data-ttu-id="cb54b-153">siguiente de código de Hello muestra el contenido del manifiesto de aplicación Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="cb54b-153">hello code below shows hello content of hello application manifest.</span></span>

```xml
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="MyNodeApp" ApplicationTypeVersion="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="MongoDB" ServiceManifestVersion="1.0" />
   </ServiceManifestImport>
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="NodeService" ServiceManifestVersion="1.0" />
   </ServiceManifestImport>
   <DefaultServices>
      <Service Name="MongoDBService">
         <StatelessService ServiceTypeName="MongoDB">
            <SingletonPartition />
         </StatelessService>
      </Service>
      <Service Name="NodeServiceService">
         <StatelessService ServiceTypeName="NodeService">
            <SingletonPartition />
         </StatelessService>
      </Service>
   </DefaultServices>
</ApplicationManifest>  
```

### <a name="publishing-hello-application"></a><span data-ttu-id="cb54b-154">Publicar aplicación de hello</span><span class="sxs-lookup"><span data-stu-id="cb54b-154">Publishing hello application</span></span>
<span data-ttu-id="cb54b-155">Hola último paso es clúster de Service Fabric local de toopublish Hola aplicación toohello mediante scripts de PowerShell de Hola a continuación:</span><span class="sxs-lookup"><span data-stu-id="cb54b-155">hello last step is toopublish hello application toohello local Service Fabric cluster by using hello PowerShell scripts below:</span></span>

```
Connect-ServiceFabricCluster localhost:19000

Write-Host 'Copying application package...'
Copy-ServiceFabricApplicationPackage -ApplicationPackagePath '[yourtargetdirectory]' -ImageStoreConnectionString 'file:C:\SfDevCluster\Data\ImageStoreShare' -ApplicationPackagePathInImageStore 'NodeAppType'

Write-Host 'Registering application type...'
Register-ServiceFabricApplicationType -ApplicationPathInImageStore 'NodeAppType'

New-ServiceFabricApplication -ApplicationName 'fabric:/NodeApp' -ApplicationTypeName 'NodeAppType' -ApplicationTypeVersion 1.0  
```

<span data-ttu-id="cb54b-156">Una vez aplicación hello clúster local toohello se publicó correctamente, puede tener acceso a aplicación Node.js de hello en el puerto de Hola que se ha introducido en el manifiesto del servicio Hola de aplicación de Node.js hello, por ejemplo http://localhost:3000.</span><span class="sxs-lookup"><span data-stu-id="cb54b-156">Once hello application is successfully published toohello local cluster, you can access hello Node.js application on hello port that we have entered in hello service manifest of hello Node.js application--for example http://localhost:3000.</span></span>

<span data-ttu-id="cb54b-157">En este tutorial, ha visto cómo tooeasily paquete dos aplicaciones existentes como una aplicación de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="cb54b-157">In this tutorial, you have seen how tooeasily package two existing applications as one Service Fabric application.</span></span> <span data-ttu-id="cb54b-158">También ha aprendido cómo toodeploy se tooService tejido para que TI puedan beneficiarse de algunas de hello características de Service Fabric, como la integración de sistema de estado y disponibilidad alta.</span><span class="sxs-lookup"><span data-stu-id="cb54b-158">You have also learned how toodeploy it tooService Fabric so that it can benefit from some of hello Service Fabric features, such as high availability and health system integration.</span></span>


## <a name="adding-more-guest-executables-tooan-existing-application-using-yeoman-on-linux"></a><span data-ttu-id="cb54b-159">Agregar más invitado ejecutables tooan aplicación existente mediante Yeoman en Linux</span><span class="sxs-lookup"><span data-stu-id="cb54b-159">Adding more guest executables tooan existing application using Yeoman on Linux</span></span>

<span data-ttu-id="cb54b-160">tooadd otra aplicación de tooan de servicio ya creado mediante `yo`, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="cb54b-160">tooadd another service tooan application already created using `yo`, perform hello following steps:</span></span> 
1. <span data-ttu-id="cb54b-161">Cambiar toohello raíz del directorio de aplicación existente de Hola.</span><span class="sxs-lookup"><span data-stu-id="cb54b-161">Change directory toohello root of hello existing application.</span></span>  <span data-ttu-id="cb54b-162">Por ejemplo, `cd ~/YeomanSamples/MyApplication`si `MyApplication` es aplicación Hola creado por Yeoman.</span><span class="sxs-lookup"><span data-stu-id="cb54b-162">For example, `cd ~/YeomanSamples/MyApplication`, if `MyApplication` is hello application created by Yeoman.</span></span>
2. <span data-ttu-id="cb54b-163">Ejecute `yo azuresfguest:AddService` y proporcionar detalles necesarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="cb54b-163">Run `yo azuresfguest:AddService` and provide hello necessary details.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cb54b-164">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="cb54b-164">Next steps</span></span>
* <span data-ttu-id="cb54b-165">Obtener información acerca de la implementación de contenedores con [información general de Service Fabric y contenedores](service-fabric-containers-overview.md)</span><span class="sxs-lookup"><span data-stu-id="cb54b-165">Learn about deploying containers with [Service Fabric and containers overview](service-fabric-containers-overview.md)</span></span>
* [<span data-ttu-id="cb54b-166">Ejemplo para empaquetar e implementar un archivo ejecutable invitado</span><span class="sxs-lookup"><span data-stu-id="cb54b-166">Sample for packaging and deploying a guest executable</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [<span data-ttu-id="cb54b-167">Ejemplo de dos archivos ejecutables (C# y nodejs) de invitado comunicarse a través del servicio de nomenclatura de hello con REST</span><span class="sxs-lookup"><span data-stu-id="cb54b-167">Sample of two guest executables (C# and nodejs) communicating via hello Naming service using REST</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-containers)
