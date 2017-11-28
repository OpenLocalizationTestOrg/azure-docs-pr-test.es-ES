---
title: aaaService tejido e implementar contenedores | Documentos de Microsoft
description: "Hello y Service Fabric el uso de aplicaciones de microservicio toodeploy de contenedores. Este artículo describen las capacidades de hello Service Fabric proporciona contenedores y cómo toodeploy imagen de un contenedor de Windows en un clúster."
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: 799cc9ad-32fd-486e-a6b6-efff6b13622d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 5/16/2017
ms.author: msfussell
ms.openlocfilehash: 8b6540579641474f21b8712b56049c7d177bec26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-windows-container-tooservice-fabric"></a><span data-ttu-id="b468d-104">Implementar un tooService de contenedor de Windows Fabric</span><span class="sxs-lookup"><span data-stu-id="b468d-104">Deploy a Windows container tooService Fabric</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b468d-105">Implementación de un contenedor de Windows</span><span class="sxs-lookup"><span data-stu-id="b468d-105">Deploy Windows Container</span></span>](service-fabric-deploy-container.md)
> * [<span data-ttu-id="b468d-106">Implementación de un contenedor de Docker</span><span class="sxs-lookup"><span data-stu-id="b468d-106">Deploy Docker Container</span></span>](service-fabric-deploy-container-linux.md)
> 
> 

<span data-ttu-id="b468d-107">Este artículo le guiará por el proceso de hello de la creación de servicios en contenedores en contenedores de Windows.</span><span class="sxs-lookup"><span data-stu-id="b468d-107">This article walks you through hello process of building containerized services in Windows containers.</span></span>

<span data-ttu-id="b468d-108">Service Fabric tiene varias funcionalidades que le ayudarán a crear aplicaciones compuestas de microservicios que se ejecutan en contenedores.</span><span class="sxs-lookup"><span data-stu-id="b468d-108">Service Fabric has several capabilities that help you with building applications that are composed of microservices running inside containers.</span></span> 

<span data-ttu-id="b468d-109">Hola capacidades incluyen:</span><span class="sxs-lookup"><span data-stu-id="b468d-109">hello capabilities include:</span></span>

* <span data-ttu-id="b468d-110">Activación e implementación de la imagen de contenedor</span><span class="sxs-lookup"><span data-stu-id="b468d-110">Container image deployment and activation</span></span>
* <span data-ttu-id="b468d-111">Regulador de recursos</span><span class="sxs-lookup"><span data-stu-id="b468d-111">Resource governance</span></span>
* <span data-ttu-id="b468d-112">Autenticación de repositorio</span><span class="sxs-lookup"><span data-stu-id="b468d-112">Repository authentication</span></span>
* <span data-ttu-id="b468d-113">Asignación de puerto a host de contenedor</span><span class="sxs-lookup"><span data-stu-id="b468d-113">Container port-to-host port mapping</span></span>
* <span data-ttu-id="b468d-114">Detección y comunicación entre contenedores</span><span class="sxs-lookup"><span data-stu-id="b468d-114">Container-to-container discovery and communication</span></span>
* <span data-ttu-id="b468d-115">Capacidad tooconfigure y establecer variables de entorno</span><span class="sxs-lookup"><span data-stu-id="b468d-115">Ability tooconfigure and set environment variables</span></span>

<span data-ttu-id="b468d-116">Echemos un vistazo a cómo las capacidades funciona cuando se está empaquetando una toobe de servicio en contenedores incluido en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b468d-116">Let's look at how each of capabilities works when you're packaging a containerized service toobe included in your application.</span></span>

## <a name="package-a-windows-container"></a><span data-ttu-id="b468d-117">Empaquetado de un contenedor de Windows</span><span class="sxs-lookup"><span data-stu-id="b468d-117">Package a Windows container</span></span>
<span data-ttu-id="b468d-118">Si empaqueta un contenedor, puede elegir toouse una plantilla de proyecto de Visual Studio o [crear paquete de aplicación Hola manualmente](#manually).</span><span class="sxs-lookup"><span data-stu-id="b468d-118">When you package a container, you can choose toouse either a Visual Studio project template or [create hello application package manually](#manually).</span></span>  <span data-ttu-id="b468d-119">Si utiliza Visual Studio, la estructura del paquete de aplicación hello y archivos de manifiesto se crean mediante la plantilla de proyecto nuevo de Hola.</span><span class="sxs-lookup"><span data-stu-id="b468d-119">When you use Visual Studio, hello application package structure and manifest files are created by hello New Project template for you.</span></span>

> [!TIP]
> <span data-ttu-id="b468d-120">toopackage de manera más fácil de Hello una imagen de contenedor existente en un servicio es toouse Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b468d-120">hello easiest way toopackage an existing container image into a service is toouse Visual Studio.</span></span>

## <a name="use-visual-studio-toopackage-an-existing-container-image"></a><span data-ttu-id="b468d-121">Usar Visual Studio toopackage una imagen de contenedor existente</span><span class="sxs-lookup"><span data-stu-id="b468d-121">Use Visual Studio toopackage an existing container image</span></span>
<span data-ttu-id="b468d-122">Visual Studio proporciona a un tejido de servicio toohelp de plantilla de servicio implementa un clúster de Service Fabric tooa de contenedor.</span><span class="sxs-lookup"><span data-stu-id="b468d-122">Visual Studio provides a Service Fabric service template toohelp you deploy a container tooa Service Fabric cluster.</span></span>

1. <span data-ttu-id="b468d-123">Seleccione **Archivo** > **Nuevo proyecto** y cree una aplicación de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="b468d-123">Choose **File** > **New Project**, and create a Service Fabric application.</span></span>
2. <span data-ttu-id="b468d-124">Elija **invitado contenedor** como plantilla de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="b468d-124">Choose **Guest Container** as hello service template.</span></span>
3. <span data-ttu-id="b468d-125">Elija **nombre de la imagen** y proporcionar la imagen de toohello de ruta de acceso de hello en el repositorio de contenedor.</span><span class="sxs-lookup"><span data-stu-id="b468d-125">Choose **Image Name** and provide hello path toohello image in your container repository.</span></span> <span data-ttu-id="b468d-126">Por ejemplo, `myrepo/myimage:v1` en https://hub.docker.com</span><span class="sxs-lookup"><span data-stu-id="b468d-126">For example, `myrepo/myimage:v1` in https://hub.docker.com</span></span>
4. <span data-ttu-id="b468d-127">Asigne un nombre a su servicio y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="b468d-127">Give your service a name, and click **OK**.</span></span>
5. <span data-ttu-id="b468d-128">Si el servicio en contenedores, necesita un punto de conexión para la comunicación, ahora puede agregar Hola protocolo, puerto y archivo de tipo toohello ServiceManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="b468d-128">If your containerized service needs an endpoint for communication, you can now add hello protocol, port, and type toohello ServiceManifest.xml file.</span></span> <span data-ttu-id="b468d-129">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="b468d-129">For example:</span></span> 
     
    `<Endpoint Name="MyContainerServiceEndpoint" Protocol="http" Port="80" UriScheme="http" PathSuffix="myapp/" Type="Input" />`
    
    <span data-ttu-id="b468d-130">Proporcionando hello `UriScheme`, Service Fabric registra automáticamente el punto de conexión de hello contenedor con servicio de nomenclatura para detectabilidad hello.</span><span class="sxs-lookup"><span data-stu-id="b468d-130">By providing hello `UriScheme`, Service Fabric automatically registers hello container endpoint with hello Naming service for discoverability.</span></span> <span data-ttu-id="b468d-131">puerto de Hello puede fijo (como se muestra en el anterior ejemplo de Hola) o se asigna de forma dinámica.</span><span class="sxs-lookup"><span data-stu-id="b468d-131">hello port can either be fixed (as shown in hello preceding example) or dynamically allocated.</span></span> <span data-ttu-id="b468d-132">Si no se especifica un puerto, se asigna dinámicamente de intervalo de puertos de aplicación Hola (tal y como sucedería con cualquier servicio).</span><span class="sxs-lookup"><span data-stu-id="b468d-132">If you don't specify a port, it is dynamically allocated from hello application port range (as would happen with any service).</span></span>
    <span data-ttu-id="b468d-133">También necesita asignación de puertos de tooconfigure Hola contenedor toohost especificando un `PortBinding` directiva en el manifiesto de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="b468d-133">You also need tooconfigure hello container toohost port mapping by specifying a `PortBinding` policy in hello application manifest.</span></span> <span data-ttu-id="b468d-134">Para obtener más información, consulte [configurar la asignación de puerto de contenedor toohost](#Portsection).</span><span class="sxs-lookup"><span data-stu-id="b468d-134">For more information, see [Configure container toohost port mapping](#Portsection).</span></span>
6. <span data-ttu-id="b468d-135">Si el contenedor necesita la regulación de los recursos, agregue una directiva `ResourceGovernancePolicy`.</span><span class="sxs-lookup"><span data-stu-id="b468d-135">If your container needs resource governance then add a `ResourceGovernancePolicy`.</span></span>
8. <span data-ttu-id="b468d-136">Si el contenedor necesita tooauthenticate con un repositorio privado, a continuación, agregue `RepositoryCredentials`.</span><span class="sxs-lookup"><span data-stu-id="b468d-136">If your container needs tooauthenticate with a private repository, then add `RepositoryCredentials`.</span></span>
7. <span data-ttu-id="b468d-137">Si está ejecutando en un equipo Windows Server 2016 con compatibilidad con el contenedor habilitado, puede usar el paquete de Hola y publicar el servicio de clúster local de acción toodeploy tooyour.</span><span class="sxs-lookup"><span data-stu-id="b468d-137">If you are running on a Windows Server 2016 machine with container support enabled, you can use hello package and publish action toodeploy tooyour local cluster.</span></span> 
8. <span data-ttu-id="b468d-138">Cuando esté listo, puede publicar clúster remoto de hello aplicación tooa o comprobar en el control de la solución toosource Hola.</span><span class="sxs-lookup"><span data-stu-id="b468d-138">When ready, you can publish hello application tooa remote cluster or check in hello solution toosource control.</span></span> 

<span data-ttu-id="b468d-139">Para obtener un ejemplo, Hola de desprotección [ejemplos de código de contenedor de Service Fabric en GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)</span><span class="sxs-lookup"><span data-stu-id="b468d-139">For an example, checkout hello [Service Fabric container code samples on GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)</span></span>

## <a name="creating-a-windows-server-2016-cluster"></a><span data-ttu-id="b468d-140">Creación de un clúster de Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="b468d-140">Creating a Windows Server 2016 cluster</span></span>
<span data-ttu-id="b468d-141">toodeploy la aplicación en contenedores, necesita toocreate habilitado de un clúster que ejecuta Windows Server 2016 con compatibilidad con el contenedor.</span><span class="sxs-lookup"><span data-stu-id="b468d-141">toodeploy your containerized application, you need toocreate a cluster running Windows Server 2016 with container support enabled.</span></span> <span data-ttu-id="b468d-142">El clúster puede ejecutarse localmente o implementarse en Azure mediante Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b468d-142">Your cluster may be running locally, or deployed via Azure Resource Manager in Azure.</span></span> 

<span data-ttu-id="b468d-143">toodeploy un clúster mediante el Administrador de recursos de Azure, elija hello **Windows Server 2016 con contenedores** opción en Azure de la imagen.</span><span class="sxs-lookup"><span data-stu-id="b468d-143">toodeploy a cluster using Azure Resource Manager, choose hello **Windows Server 2016 with Containers** image option in Azure.</span></span> <span data-ttu-id="b468d-144">Vea el artículo de hello [crear un clúster de Service Fabric mediante Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).</span><span class="sxs-lookup"><span data-stu-id="b468d-144">See hello article [Create a Service Fabric cluster by using Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).</span></span> <span data-ttu-id="b468d-145">Asegúrese de que usa Hola después de la configuración del Administrador de recursos de Azure:</span><span class="sxs-lookup"><span data-stu-id="b468d-145">Ensure that you use hello following Azure Resource Manager settings:</span></span>

```xml
"vmImageOffer": { "type": "string","defaultValue": "WindowsServer"     },
"vmImageSku": { "defaultValue": "2016-Datacenter-with-Containers","type": "string"     },
"vmImageVersion": { "defaultValue": "latest","type": "string"     },  
```
<span data-ttu-id="b468d-146">También puede usar hello [plantilla de cinco nodos Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype) toocreate un clúster.</span><span class="sxs-lookup"><span data-stu-id="b468d-146">You can also use hello [Five Node Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype) toocreate a cluster.</span></span> <span data-ttu-id="b468d-147">Como alternativa, lea una [entrada de blog](https://loekd.blogspot.com/2017/01/running-windows-containers-on-azure.html) de la comunidad sobre el uso de Service Fabric y los contenedores de Windows.</span><span class="sxs-lookup"><span data-stu-id="b468d-147">Alternatively read a community [blog post](https://loekd.blogspot.com/2017/01/running-windows-containers-on-azure.html) on using Service Fabric and Windows containers.</span></span>

<a id="manually"></a>

## <a name="manually-package-and-deploy-a-container-image"></a><span data-ttu-id="b468d-148">Empaquetado e implementación manual de una imagen de contenedor</span><span class="sxs-lookup"><span data-stu-id="b468d-148">Manually package and deploy a container image</span></span>
<span data-ttu-id="b468d-149">proceso de Hola de empaquetar manualmente un servicio en contenedores se basa en hello pasos:</span><span class="sxs-lookup"><span data-stu-id="b468d-149">hello process of manually packaging a containerized service is based on hello following steps:</span></span>

1. <span data-ttu-id="b468d-150">Publicar el repositorio de tooyour de contenedores de Hola.</span><span class="sxs-lookup"><span data-stu-id="b468d-150">Publish hello containers tooyour repository.</span></span>
2. <span data-ttu-id="b468d-151">Crear estructura de directorios de paquetes de saludo.</span><span class="sxs-lookup"><span data-stu-id="b468d-151">Create hello package directory structure.</span></span>
3. <span data-ttu-id="b468d-152">Edite el archivo de manifiesto de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="b468d-152">Edit hello service manifest file.</span></span>
4. <span data-ttu-id="b468d-153">Edite el archivo de manifiesto de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="b468d-153">Edit hello application manifest file.</span></span>

## <a name="deploy-and-activate-a-container-image"></a><span data-ttu-id="b468d-154">Implementación y activación de una imagen de contenedor</span><span class="sxs-lookup"><span data-stu-id="b468d-154">Deploy and activate a container image</span></span>
<span data-ttu-id="b468d-155">Hola Service Fabric [modelo de aplicación](service-fabric-application-model.md), un contenedor representa un host de aplicación en la que varios servicios se colocan las réplicas.</span><span class="sxs-lookup"><span data-stu-id="b468d-155">In hello Service Fabric [application model](service-fabric-application-model.md), a container represents an application host in which multiple service replicas are placed.</span></span> <span data-ttu-id="b468d-156">toodeploy y activar un contenedor, el nombre de hello put de imagen del contenedor hello en un `ContainerHost` elemento en el manifiesto del servicio Hola.</span><span class="sxs-lookup"><span data-stu-id="b468d-156">toodeploy and activate a container, put hello name of hello container image into a `ContainerHost` element in hello service manifest.</span></span>

<span data-ttu-id="b468d-157">En el manifiesto del servicio hello, agregue un `ContainerHost` Hola punto de entrada.</span><span class="sxs-lookup"><span data-stu-id="b468d-157">In hello service manifest, add a `ContainerHost` for hello entry point.</span></span> <span data-ttu-id="b468d-158">A continuación, el conjunto de hello `ImageName` toobe nombre de Hola de repositorio de contenedor de Hola y de imagen.</span><span class="sxs-lookup"><span data-stu-id="b468d-158">Then set hello `ImageName` toobe hello name of hello container repository and image.</span></span> <span data-ttu-id="b468d-159">Hello manifiesto parcial siguiente muestra un ejemplo de cómo se denomina contenedor de hello toodeploy `myimage:v1` desde un repositorio, denominado `myrepo`:</span><span class="sxs-lookup"><span data-stu-id="b468d-159">hello following partial manifest shows an example of how toodeploy hello container called `myimage:v1` from a repository called `myrepo`:</span></span>

```xml
    <CodePackage Name="Code" Version="1.0">
        <EntryPoint>
          <ContainerHost>
            <ImageName>myrepo/myimage:v1</ImageName>
            <Commands></Commands>
          </ContainerHost>
        </EntryPoint>
    </CodePackage>
```

<span data-ttu-id="b468d-160">Puede especificar toorun de comandos opcionales al iniciar el contenedor de hello en hello `Commands` elemento.</span><span class="sxs-lookup"><span data-stu-id="b468d-160">You can specify optional commands toorun upon starting hello container under hello `Commands` element.</span></span> <span data-ttu-id="b468d-161">Separe los distintos comandos con comas.</span><span class="sxs-lookup"><span data-stu-id="b468d-161">For multiple commands, comma-delimit them.</span></span> 

## <a name="understand-resource-governance"></a><span data-ttu-id="b468d-162">Descripción de la regulación de recursos</span><span class="sxs-lookup"><span data-stu-id="b468d-162">Understand resource governance</span></span>
<span data-ttu-id="b468d-163">La regulación de recursos es una funcionalidad de contenedor de Hola que limita los recursos de Hola que Hola contenedor puede utilizar en el host de Hola.</span><span class="sxs-lookup"><span data-stu-id="b468d-163">Resource governance is a capability of hello container that restricts hello resources that hello container can use on hello host.</span></span> <span data-ttu-id="b468d-164">Hola `ResourceGovernancePolicy`, que se especifica en el manifiesto de aplicación Hola es los límites de recursos de toodeclare usado para un paquete de código de servicio.</span><span class="sxs-lookup"><span data-stu-id="b468d-164">hello `ResourceGovernancePolicy`, which is specified in hello application manifest is used toodeclare resource limits for a service code package.</span></span> <span data-ttu-id="b468d-165">Se pueden establecer límites de recursos para hello recursos siguientes:</span><span class="sxs-lookup"><span data-stu-id="b468d-165">Resource limits can be set for hello following resources:</span></span>

* <span data-ttu-id="b468d-166">Memoria</span><span class="sxs-lookup"><span data-stu-id="b468d-166">Memory</span></span>
* <span data-ttu-id="b468d-167">MemorySwap</span><span class="sxs-lookup"><span data-stu-id="b468d-167">MemorySwap</span></span>
* <span data-ttu-id="b468d-168">CpuShares (peso relativo de CPU)</span><span class="sxs-lookup"><span data-stu-id="b468d-168">CpuShares (CPU relative weight)</span></span>
* <span data-ttu-id="b468d-169">MemoryReservationInMB</span><span class="sxs-lookup"><span data-stu-id="b468d-169">MemoryReservationInMB</span></span>  
* <span data-ttu-id="b468d-170">BlkioWeight (peso relativo de BlockIO).</span><span class="sxs-lookup"><span data-stu-id="b468d-170">BlkioWeight (BlockIO relative weight).</span></span>

> [!NOTE]
> <span data-ttu-id="b468d-171">Para una versión futura se ha planeado la compatibilidad para especificar límites de E/S de bloques como IOP, BPS de lectura/escritura y mucho más.</span><span class="sxs-lookup"><span data-stu-id="b468d-171">Support for specifying specific block IO limits such as IOPs, read/write BPS, and others are planned for a future release.</span></span>
> 
> 

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <Policies>
            <ResourceGovernancePolicy CodePackageRef="FrontendService.Code" CpuShares="500"
            MemoryInMB="1024" MemorySwapInMB="4084" MemoryReservationInMB="1024" />
        </Policies>
    </ServiceManifestImport>
```

## <a name="authenticate-a-repository"></a><span data-ttu-id="b468d-172">Autenticación de un repositorio</span><span class="sxs-lookup"><span data-stu-id="b468d-172">Authenticate a repository</span></span>
<span data-ttu-id="b468d-173">toodownload un contenedor, es posible que tenga repositorio de contenedor de toohello tooprovide las credenciales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="b468d-173">toodownload a container, you might have tooprovide sign-in credentials toohello container repository.</span></span> <span data-ttu-id="b468d-174">Hola inicio de sesión credenciales, especificadas en el manifiesto de aplicación Hola, son utilizados toospecify Hola inicio de sesión en la información o clave SSH, para descargar la imagen de contenedor de Hola Hola repositorio de imágenes.</span><span class="sxs-lookup"><span data-stu-id="b468d-174">hello sign-in credentials, specified in hello application manifest, are used toospecify hello sign-in information, or SSH key, for downloading hello container image from hello image repository.</span></span> <span data-ttu-id="b468d-175">Hello en el ejemplo siguiente se muestra una cuenta llamada *Usuarioprueba* junto con la contraseña de hello en texto no cifrado (*no* recomendado):</span><span class="sxs-lookup"><span data-stu-id="b468d-175">hello following example shows an account called *TestUser* along with hello password in clear text (*not* recommended):</span></span>

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <Policies>
            <ContainerHostPolicies CodePackageRef="FrontendService.Code">
                <RepositoryCredentials AccountName="TestUser" Password="12345" PasswordEncrypted="false"/>
            </ContainerHostPolicies>
        </Policies>
    </ServiceManifestImport>
```

<span data-ttu-id="b468d-176">Se recomienda que cifre la contraseña hello mediante un certificado que ha implementado la máquina toohello.</span><span class="sxs-lookup"><span data-stu-id="b468d-176">We recommend that you encrypt hello password by using a certificate that's deployed toohello machine.</span></span>

<span data-ttu-id="b468d-177">Hello en el ejemplo siguiente se muestra una cuenta llamada *Usuarioprueba*, donde contraseña hello se cifró mediante el uso de un certificado denominado *MyCert*.</span><span class="sxs-lookup"><span data-stu-id="b468d-177">hello following example shows an account called *TestUser*, where hello password was encrypted by using a certificate called *MyCert*.</span></span> <span data-ttu-id="b468d-178">Puede usar hello `Invoke-ServiceFabricEncryptText` texto PowerShell comando toocreate hello secreto cifrado de contraseña de Hola.</span><span class="sxs-lookup"><span data-stu-id="b468d-178">You can use hello `Invoke-ServiceFabricEncryptText` PowerShell command toocreate hello secret cipher text for hello password.</span></span> <span data-ttu-id="b468d-179">Para obtener más información, vea el artículo de hello [administrar secretos en aplicaciones de Service Fabric](service-fabric-application-secret-management.md).</span><span class="sxs-lookup"><span data-stu-id="b468d-179">For more information, see hello article [Managing secrets in Service Fabric applications](service-fabric-application-secret-management.md).</span></span>

<span data-ttu-id="b468d-180">clave privada de Hello del certificado de Hola que ha utilizado la contraseña de hello toodecrypt debe ser implementado toohello equipo local en un método fuera de banda.</span><span class="sxs-lookup"><span data-stu-id="b468d-180">hello private key of hello certificate that's used toodecrypt hello password must be deployed toohello local machine in an out-of-band method.</span></span> <span data-ttu-id="b468d-181">(en Azure esto se logra mediante Azure Resource Manager). A continuación, cuando Service Fabric implementa la máquina de toohello de paquete de servicio de hello, puede descifrar el secreto de Hola.</span><span class="sxs-lookup"><span data-stu-id="b468d-181">(In Azure, this method is Azure Resource Manager.) Then, when Service Fabric deploys hello service package toohello machine, it can decrypt hello secret.</span></span> <span data-ttu-id="b468d-182">Mediante el secreto de hello junto con el nombre de la cuenta de hello, a continuación, se pueda autenticar con el repositorio de contenedor de Hola.</span><span class="sxs-lookup"><span data-stu-id="b468d-182">By using hello secret along with hello account name, it can then authenticate with hello container repository.</span></span>

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <Policies>
            <ContainerHostPolicies CodePackageRef="FrontendService.Code">
                <RepositoryCredentials AccountName="TestUser" Password="[Put encrypted password here using MyCert certificate ]" PasswordEncrypted="true"/>
            </ContainerHostPolicies>
        </Policies>
    </ServiceManifestImport>
```

## <span data-ttu-id="b468d-183"><a name ="Portsection"></a>Configurar la asignación de puerto de contenedor toohost</span><span class="sxs-lookup"><span data-stu-id="b468d-183"><a name ="Portsection"></a> Configure container toohost port mapping</span></span>
<span data-ttu-id="b468d-184">Puede configurar una toocommunicate de puerto que se utiliza de host con el contenedor de hello especificando un `PortBinding` en el manifiesto de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="b468d-184">You can configure a host port used toocommunicate with hello container by specifying a `PortBinding` in hello application manifest.</span></span> <span data-ttu-id="b468d-185">Hola puerto enlace mapas Hola puerto toowhich Hola servicio está escuchando en hello contenedor tooa puerto en el host de Hola.</span><span class="sxs-lookup"><span data-stu-id="b468d-185">hello port binding maps hello port toowhich hello service is listening inside hello container tooa port on hello host.</span></span>

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <Policies>
            <ContainerHostPolicies CodePackageRef="FrontendService.Code">
                <PortBinding ContainerPort="8905"/>
            </ContainerHostPolicies>
        </Policies>
    </ServiceManifestImport>
```

## <a name="configure-container-to-container-discovery-and-communication"></a><span data-ttu-id="b468d-186">Configuración de detección y comunicación entre contenedores</span><span class="sxs-lookup"><span data-stu-id="b468d-186">Configure container-to-container discovery and communication</span></span>
<span data-ttu-id="b468d-187">Puede usar hello `PortBinding` elemento toomap un punto de conexión de tooan de puerto del contenedor en el manifiesto del servicio Hola.</span><span class="sxs-lookup"><span data-stu-id="b468d-187">You can use hello `PortBinding` element toomap a container port tooan endpoint in hello service manifest.</span></span> <span data-ttu-id="b468d-188">En el siguiente ejemplo de Hola Hola extremo `Endpoint1` especifica un puerto fijo, 8905.</span><span class="sxs-lookup"><span data-stu-id="b468d-188">In hello following example, hello endpoint `Endpoint1` specifies a fixed port, 8905.</span></span> <span data-ttu-id="b468d-189">También no puede especificar ningún puerto en absoluto, en cuyo caso se elige un puerto aleatorio del intervalo de puertos de aplicaciones del clúster de Hola para usted.</span><span class="sxs-lookup"><span data-stu-id="b468d-189">It can also specify no port at all, in which case a random port from hello cluster's application port range is chosen for you.</span></span>


```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <Policies>
            <ContainerHostPolicies CodePackageRef="FrontendService.Code">
                <PortBinding ContainerPort="8905" EndpointRef="Endpoint1"/>
            </ContainerHostPolicies>
        </Policies>
    </ServiceManifestImport>
```
<span data-ttu-id="b468d-190">Si especifica un punto de conexión, utilizando hello `Endpoint` etiqueta en el manifiesto del servicio Hola de un contenedor de invitado, Service Fabric automáticamente puede publicar este servicio de nombres de punto de conexión toohello.</span><span class="sxs-lookup"><span data-stu-id="b468d-190">If you specify an endpoint, using hello `Endpoint` tag in hello service manifest of a guest container, Service Fabric can automatically publish this endpoint toohello Naming service.</span></span> <span data-ttu-id="b468d-191">Otros servicios que se ejecutan en el clúster de hello, por tanto, pueden detectar este contenedor mediante consultas REST de hello en resolver.</span><span class="sxs-lookup"><span data-stu-id="b468d-191">Other services that are running in hello cluster can thus discover this container using hello REST queries for resolving.</span></span>

<span data-ttu-id="b468d-192">Registrando con servicio de nomenclatura de hello, puede realizar el contenedor a la comunicación dentro de su contenedor mediante hello [proxy inverso](service-fabric-reverseproxy.md).</span><span class="sxs-lookup"><span data-stu-id="b468d-192">By registering with hello Naming service, you can perform container-to-container communication within your container by using hello [reverse proxy](service-fabric-reverseproxy.md).</span></span> <span data-ttu-id="b468d-193">La comunicación se realiza proporcionando el puerto de escucha de http de proxy inverso de Hola y el nombre de hello de servicios de Hola que desee toocommunicate con como variables de entorno.</span><span class="sxs-lookup"><span data-stu-id="b468d-193">Communication is performed by providing hello reverse proxy http listening port and hello name of hello services that you want toocommunicate with as environment variables.</span></span> <span data-ttu-id="b468d-194">Para obtener más información, vea la sección siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="b468d-194">For more information, see hello next section.</span></span> 

## <a name="configure-and-set-environment-variables"></a><span data-ttu-id="b468d-195">Configuración y establecimiento de variables de entorno</span><span class="sxs-lookup"><span data-stu-id="b468d-195">Configure and set environment variables</span></span>
<span data-ttu-id="b468d-196">Las variables de entorno se pueden especificar para cada paquete de código en el manifiesto del servicio Hola.</span><span class="sxs-lookup"><span data-stu-id="b468d-196">Environment variables can be specified for each code package in hello service manifest.</span></span> <span data-ttu-id="b468d-197">Esta característica está disponible para todos los servicios, con independencia de si se implementan como contenedores, procesos o archivos ejecutables de invitado.</span><span class="sxs-lookup"><span data-stu-id="b468d-197">This feature is available for all services irrespective of whether they are deployed as containers or processes or guest executables.</span></span> <span data-ttu-id="b468d-198">Puede invalidar la variable de entorno valores de la aplicación hello manifiesto o especifican durante la implementación como parámetros de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b468d-198">You can override environment variable values in hello application manifest or specify them during deployment as application parameters.</span></span>

<span data-ttu-id="b468d-199">Hello fragmento XML de manifiesto de servicio siguiente muestra un ejemplo de cómo toospecify las variables de entorno para un paquete de código:</span><span class="sxs-lookup"><span data-stu-id="b468d-199">hello following service manifest XML snippet shows an example of how toospecify environment variables for a code package:</span></span>

```xml
    <ServiceManifest Name="FrontendServicePackage" Version="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <Description>a guest executable service in a container</Description>
        <ServiceTypes>
            <StatelessServiceType ServiceTypeName="StatelessFrontendService"  UseImplicitHost="true"/>
        </ServiceTypes>
        <CodePackage Name="FrontendService.Code" Version="1.0">
            <EntryPoint>
            <ContainerHost>
                <ImageName>myrepo/myimage:v1</ImageName>
                <Commands></Commands>
            </ContainerHost>
            </EntryPoint>
            <EnvironmentVariables>
                <EnvironmentVariable Name="HttpGatewayPort" Value=""/>
                <EnvironmentVariable Name="BackendServiceName" Value=""/>
            </EnvironmentVariables>
        </CodePackage>
    </ServiceManifest>
```

<span data-ttu-id="b468d-200">Estas variables de entorno pueden reemplazarse en nivel de manifiesto de aplicación Hola:</span><span class="sxs-lookup"><span data-stu-id="b468d-200">These environment variables can be overridden at hello application manifest level:</span></span>

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <EnvironmentOverrides CodePackageRef="FrontendService.Code">
            <EnvironmentVariable Name="BackendServiceName" Value="[BackendSvc]"/>
            <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
        </EnvironmentOverrides>
    </ServiceManifestImport>
```

<span data-ttu-id="b468d-201">En el ejemplo anterior de hello, se especifica un valor explícito para hello `HttpGateway` variable de entorno (19000), aunque se establezca el valor de Hola para `BackendServiceName` parámetro mediante hello `[BackendSvc]` parámetro de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b468d-201">In hello previous example, we specified an explicit value for hello `HttpGateway` environment variable (19000), while we set hello value for `BackendServiceName` parameter via hello `[BackendSvc]` application parameter.</span></span> <span data-ttu-id="b468d-202">Estas opciones le permiten toospecify valor de Hola para `BackendServiceName`valor al implementar la aplicación hello y no tiene un valor fijo en el manifiesto de Hola.</span><span class="sxs-lookup"><span data-stu-id="b468d-202">These settings enable you toospecify hello value for `BackendServiceName`value when you deploy hello application and not have a fixed value in hello manifest.</span></span>

## <a name="configure-isolation-mode"></a><span data-ttu-id="b468d-203">Configuración del modo de aislamiento</span><span class="sxs-lookup"><span data-stu-id="b468d-203">Configure isolation mode</span></span>

<span data-ttu-id="b468d-204">Windows admite dos modos de aislamiento para contenedores: de proceso y de Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="b468d-204">Windows supports two isolation modes for containers - process and Hyper-V.</span></span>  <span data-ttu-id="b468d-205">Con el modo de aislamiento de procesos de hello, con todos los contenedores de Hola Hola mismo host máquina recurso compartido Hola kernel con el host de Hola.</span><span class="sxs-lookup"><span data-stu-id="b468d-205">With hello process isolation mode, all hello containers running on hello same host machine share hello kernel with hello host.</span></span> <span data-ttu-id="b468d-206">Con el modo de aislamiento de hello Hyper-V, los kernels de hello están aislados entre cada contenedor de Hyper-V y host de contenedor de Hola.</span><span class="sxs-lookup"><span data-stu-id="b468d-206">With hello Hyper-V isolation mode, hello kernels are isolated between each Hyper-V container and hello container host.</span></span> <span data-ttu-id="b468d-207">se especifica el modo de aislamiento de Hola Hola `ContainerHostPolicies` etiqueta en el archivo de manifiesto de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="b468d-207">hello isolation mode is specified in hello `ContainerHostPolicies` tag in hello application manifest file.</span></span>  <span data-ttu-id="b468d-208">modos de aislamiento de Hola que pueden especificarse son `process`, `hyperv`, y `default`.</span><span class="sxs-lookup"><span data-stu-id="b468d-208">hello isolation modes that can be specified are `process`, `hyperv`, and `default`.</span></span> <span data-ttu-id="b468d-209">Hola `default` el modo de aislamiento predeterminado es demasiado`process` en Windows Server hospeda y el valor predeterminado es demasiado`hyperv` en hosts de Windows 10.</span><span class="sxs-lookup"><span data-stu-id="b468d-209">hello `default` isolation mode defaults too`process` on Windows Server hosts, and defaults too`hyperv` on Windows 10 hosts.</span></span>  <span data-ttu-id="b468d-210">Hello fragmento de código siguiente muestra cómo se especifica el modo de aislamiento de hello en el archivo de manifiesto de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="b468d-210">hello following snippet shows how hello isolation mode is specified in hello application manifest file.</span></span>

```xml
   <ContainerHostPolicies CodePackageRef="NodeService.Code" Isolation="hyperv">
```


## <a name="complete-examples-for-application-and-service-manifest"></a><span data-ttu-id="b468d-211">Ejemplos completos de manifiesto de servicio y de aplicación</span><span class="sxs-lookup"><span data-stu-id="b468d-211">Complete examples for application and service manifest</span></span>

<span data-ttu-id="b468d-212">Este es un ejemplo de un manifiesto de aplicación:</span><span class="sxs-lookup"><span data-stu-id="b468d-212">An example application manifest follows:</span></span>

```xml
    <ApplicationManifest ApplicationTypeName="SimpleContainerApp" ApplicationTypeVersion="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <Description>A simple service container application</Description>
        <Parameters>
            <Parameter Name="ServiceInstanceCount" DefaultValue="3"></Parameter>
            <Parameter Name="BackEndSvcName" DefaultValue="bkend"></Parameter>
        </Parameters>
        <ServiceManifestImport>
            <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
            <EnvironmentOverrides CodePackageRef="FrontendService.Code">
                <EnvironmentVariable Name="BackendServiceName" Value="[BackendSvcName]"/>
                <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
            </EnvironmentOverrides>
            <Policies>
                <ResourceGovernancePolicy CodePackageRef="Code" CpuShares="500" MemoryInMB="1024" MemorySwapInMB="4084" MemoryReservationInMB="1024" />
                <ContainerHostPolicies CodePackageRef="FrontendService.Code">
                    <RepositoryCredentials AccountName="username" Password="****" PasswordEncrypted="true"/>
                    <PortBinding ContainerPort="8905" EndpointRef="Endpoint1"/>
                </ContainerHostPolicies>
            </Policies>
        </ServiceManifestImport>
    </ApplicationManifest>
```

<span data-ttu-id="b468d-213">A continuación se muestra un ejemplo de manifiesto de servicio (especificado en hello anterior manifiesto de aplicación):</span><span class="sxs-lookup"><span data-stu-id="b468d-213">An example service manifest (specified in hello preceding application manifest) follows:</span></span>

```xml
    <ServiceManifest Name="FrontendServicePackage" Version="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <Description> A service that implements a stateless front end in a container</Description>
        <ServiceTypes>
            <StatelessServiceType ServiceTypeName="StatelessFrontendService"  UseImplicitHost="true"/>
        </ServiceTypes>
        <CodePackage Name="FrontendService.Code" Version="1.0">
            <EntryPoint>
            <ContainerHost>
                <ImageName>myrepo/myimage:v1</ImageName>
                <Commands></Commands>
            </ContainerHost>
            </EntryPoint>
            <EnvironmentVariables>
                <EnvironmentVariable Name="HttpGatewayPort" Value=""/>
                <EnvironmentVariable Name="BackendServiceName" Value=""/>
            </EnvironmentVariables>
        </CodePackage>
        <ConfigPackage Name="FrontendService.Config" Version="1.0" />
        <DataPackage Name="FrontendService.Data" Version="1.0" />
        <Resources>
            <Endpoints>
                <Endpoint Name="Endpoint1" UriScheme="http" Port="80" Protocol="http"/>
            </Endpoints>
        </Resources>
    </ServiceManifest>
```

## <a name="next-steps"></a><span data-ttu-id="b468d-214">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b468d-214">Next steps</span></span>
<span data-ttu-id="b468d-215">Ahora que ha implementado un servicio en contenedores, obtenga información acerca de cómo toomanage su ciclo de vida leyendo [ciclo de vida de aplicación de Service Fabric](service-fabric-application-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="b468d-215">Now that you have deployed a containerized service, learn how toomanage its lifecycle by reading [Service Fabric application lifecycle](service-fabric-application-lifecycle.md).</span></span>

* [<span data-ttu-id="b468d-216">Información general: Service Fabric y contenedores</span><span class="sxs-lookup"><span data-stu-id="b468d-216">Overview of Service Fabric and containers</span></span>](service-fabric-containers-overview.md)
* <span data-ttu-id="b468d-217">Para un ejemplo, consulte los [ejemplos de código de contenedor de Service Fabric en GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)</span><span class="sxs-lookup"><span data-stu-id="b468d-217">For an example, checkout [Service Fabric container code samples on GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)</span></span>
