---
title: aaaService tejido e implementar contenedores de Linux | Documentos de Microsoft
description: "Hello y Service Fabric el uso de aplicaciones de microservicio de toodeploy de contenedores de Linux. Este artículo describen las capacidades de hello Service Fabric proporciona contenedores y cómo toodeploy imagen de un contenedor de Linux en un clúster"
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: 4ba99103-6064-429d-ba17-82861b6ddb11
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 6/29/2017
ms.author: msfussell
ms.openlocfilehash: e28f99a145b0594d871b0ec0566233a7ad235ce8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-linux-container-tooservice-fabric"></a><span data-ttu-id="a374b-104">Implementar un tooService de contenedor Linux tejido</span><span class="sxs-lookup"><span data-stu-id="a374b-104">Deploy a Linux container tooService Fabric</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a374b-105">Implementación de un contenedor de Windows</span><span class="sxs-lookup"><span data-stu-id="a374b-105">Deploy Windows Container</span></span>](service-fabric-deploy-container.md)
> * [<span data-ttu-id="a374b-106">Implementar un contenedor de Linux</span><span class="sxs-lookup"><span data-stu-id="a374b-106">Deploy Linux Container</span></span>](service-fabric-deploy-container-linux.md)
>
>

<span data-ttu-id="a374b-107">Este artículo lo guiará a través de la creación de servicios de contenedor en contenedores de Docker en Linux.</span><span class="sxs-lookup"><span data-stu-id="a374b-107">This article walks you through building containerized services in Docker containers on Linux.</span></span>

<span data-ttu-id="a374b-108">Service Fabric tiene varias funcionalidades de contenedor que le ayudarán a crear aplicaciones que se componen de microservicios en contenedores.</span><span class="sxs-lookup"><span data-stu-id="a374b-108">Service Fabric has several container capabilities that help you with building applications that are composed of microservices that are containerized.</span></span> <span data-ttu-id="a374b-109">Son los llamados servicios en contenedores.</span><span class="sxs-lookup"><span data-stu-id="a374b-109">These services are called containerized services.</span></span>

<span data-ttu-id="a374b-110">incluyen capacidades de Hello;</span><span class="sxs-lookup"><span data-stu-id="a374b-110">hello capabilities include;</span></span>

* <span data-ttu-id="a374b-111">Activación e implementación de la imagen de contenedor</span><span class="sxs-lookup"><span data-stu-id="a374b-111">Container image deployment and activation</span></span>
* <span data-ttu-id="a374b-112">Regulador de recursos</span><span class="sxs-lookup"><span data-stu-id="a374b-112">Resource governance</span></span>
* <span data-ttu-id="a374b-113">Autenticación de repositorio</span><span class="sxs-lookup"><span data-stu-id="a374b-113">Repository authentication</span></span>
* <span data-ttu-id="a374b-114">Asignación de puertos de puerto del contenedor toohost</span><span class="sxs-lookup"><span data-stu-id="a374b-114">Container port toohost port mapping</span></span>
* <span data-ttu-id="a374b-115">Detección y comunicación entre contenedores</span><span class="sxs-lookup"><span data-stu-id="a374b-115">Container-to-container discovery and communication</span></span>
* <span data-ttu-id="a374b-116">Capacidad tooconfigure y establecer variables de entorno</span><span class="sxs-lookup"><span data-stu-id="a374b-116">Ability tooconfigure and set environment variables</span></span>

## <a name="packaging-a-docker-container-with-yeoman"></a><span data-ttu-id="a374b-117">Empaquetado de un contenedor de Docker con Yeoman</span><span class="sxs-lookup"><span data-stu-id="a374b-117">Packaging a docker container with yeoman</span></span>
<span data-ttu-id="a374b-118">Al empaquetar un contenedor en Linux, puede elegir cualquier toouse una plantilla de yeoman o [crear paquete de aplicación Hola manualmente](#manually).</span><span class="sxs-lookup"><span data-stu-id="a374b-118">When packaging a container on Linux, you can choose either toouse a yeoman template or [create hello application package manually](#manually).</span></span>

<span data-ttu-id="a374b-119">Una aplicación de Service Fabric puede contener uno o varios contenedores, cada uno con un rol específico en la entrega de la funcionalidad de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="a374b-119">A Service Fabric application can contain one or more containers, each with a specific role in delivering hello application's functionality.</span></span> <span data-ttu-id="a374b-120">Hola servicio SDK de tejido para Linux incluye un [Yeoman](http://yeoman.io/) generador que hace más fácil toocreate la aplicación y agregar una imagen de contenedor.</span><span class="sxs-lookup"><span data-stu-id="a374b-120">hello Service Fabric SDK for Linux includes a [Yeoman](http://yeoman.io/) generator that makes it easy toocreate your application and add a container image.</span></span> <span data-ttu-id="a374b-121">Vamos a usar Yeoman toocreate llama a una aplicación con un único contenedor de Docker *SimpleContainerApp*.</span><span class="sxs-lookup"><span data-stu-id="a374b-121">Let's use Yeoman toocreate an application with a single Docker container called *SimpleContainerApp*.</span></span> <span data-ttu-id="a374b-122">Puede agregar más servicios más adelante mediante la edición de archivos de manifiesto de hello generado.</span><span class="sxs-lookup"><span data-stu-id="a374b-122">You can add more services later by editing hello generated manifest files.</span></span>

## <a name="install-docker-on-your-development-box"></a><span data-ttu-id="a374b-123">Instalación de un contenedor de Docker en el cuadro de desarrollo</span><span class="sxs-lookup"><span data-stu-id="a374b-123">Install Docker on your development box</span></span>

<span data-ttu-id="a374b-124">Siguiente ejecución Hola comandos docker tooinstall en el cuadro de desarrollo de Linux (si está usando imágenes vagrant hello en OSX, ya está instalado docker):</span><span class="sxs-lookup"><span data-stu-id="a374b-124">Run hello following commands tooinstall docker on your Linux development box (if you are using hello vagrant image on OSX, docker is already installed):</span></span>

```bash
    sudo apt-get install wget
    wget -qO- https://get.docker.io/ | sh
```

## <a name="create-hello-application"></a><span data-ttu-id="a374b-125">Crear aplicación hello</span><span class="sxs-lookup"><span data-stu-id="a374b-125">Create hello application</span></span>
1. <span data-ttu-id="a374b-126">En un terminal, escriba `yo azuresfcontainer`.</span><span class="sxs-lookup"><span data-stu-id="a374b-126">In a terminal, type `yo azuresfcontainer`.</span></span>
2. <span data-ttu-id="a374b-127">Dé nombre a la aplicación; por ejemplo, mycontainerap.</span><span class="sxs-lookup"><span data-stu-id="a374b-127">Name your application - for example, mycontainerap</span></span>
3. <span data-ttu-id="a374b-128">Proporcionar Hola URL de imagen de contenedor de Hola desde un repositorio de DockerHub.</span><span class="sxs-lookup"><span data-stu-id="a374b-128">Provide hello URL for hello container image from a DockerHub repo.</span></span> <span data-ttu-id="a374b-129">Hola imagen parámetro toma Hola formulario [repositorio] / [nombre de imagen]</span><span class="sxs-lookup"><span data-stu-id="a374b-129">hello image parameter takes hello form [repo]/[image name]</span></span>
4. <span data-ttu-id="a374b-130">Si Hola imagen no tiene un carga de trabajo-punto de entrada definido, deberá tooexplicitly especificar comandos de entrada con un conjunto delimitado por comas de toorun de comandos en el contenedor de hello, que se mantendrá el contenedor de Hola que se ejecuta después del inicio.</span><span class="sxs-lookup"><span data-stu-id="a374b-130">If hello image does not have a workload entry-point defined, then you need tooexplicitly specify input commands with a comma-delimited set of commands toorun inside hello container, which will keep hello container running after startup.</span></span>

![Generador Yeoman de Service Fabric para contenedores][sf-yeoman]

## <a name="deploy-hello-application"></a><span data-ttu-id="a374b-132">Implementar la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="a374b-132">Deploy hello application</span></span>

### <a name="using-xplat-cli"></a><span data-ttu-id="a374b-133">Uso de la CLI multiplataforma</span><span class="sxs-lookup"><span data-stu-id="a374b-133">Using XPlat CLI</span></span>
<span data-ttu-id="a374b-134">Una vez que se compila la aplicación hello, puede implementarlo toohello clúster local con hello CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="a374b-134">Once hello application is built, you can deploy it toohello local cluster using hello Azure CLI.</span></span>

1. <span data-ttu-id="a374b-135">Conectar el clúster de Service Fabric local toohello.</span><span class="sxs-lookup"><span data-stu-id="a374b-135">Connect toohello local Service Fabric cluster.</span></span>

    ```bash
    azure servicefabric cluster connect
    ```

2. <span data-ttu-id="a374b-136">Hola usar script de instalación proporcionado por el almacén de imágenes del clúster toohello del paquete en hello plantilla toocopy aplicación hello, registrar el tipo de aplicación Hola y cree una instancia de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="a374b-136">Use hello install script provided in hello template toocopy hello application package toohello cluster's image store, register hello application type, and create an instance of hello application.</span></span>

    ```bash
    ./install.sh
    ```

3. <span data-ttu-id="a374b-137">Abra un explorador y navegue tooService Fabric Explorer en el Explorador de http://localhost:19080 / (sustituya localhost con la dirección IP privada de Hola de hello VM si usa a Vagrant en Mac OS X).</span><span class="sxs-lookup"><span data-stu-id="a374b-137">Open a browser and navigate tooService Fabric Explorer at http://localhost:19080/Explorer (replace localhost with hello private IP of hello VM if using Vagrant on Mac OS X).</span></span>
4. <span data-ttu-id="a374b-138">Expanda el nodo de aplicaciones de hello y observe que ahora hay una entrada para el tipo de aplicación y otro para hello primera instancia de ese tipo.</span><span class="sxs-lookup"><span data-stu-id="a374b-138">Expand hello Applications node and note that there is now an entry for your application type and another for hello first instance of that type.</span></span>
5. <span data-ttu-id="a374b-139">Usar scripts de desinstalación de hello proporcionado en la instancia de la aplicación de hello plantilla toodelete hello y anular el registro del tipo de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="a374b-139">Use hello uninstall script provided in hello template toodelete hello application instance and unregister hello application type.</span></span>

    ```bash
    ./uninstall.sh
    ```

### <a name="using-azure-cli-20"></a><span data-ttu-id="a374b-140">Uso de la CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="a374b-140">Using Azure CLI 2.0</span></span>

<span data-ttu-id="a374b-141">Consulte la documentación de referencia de hello sobre la administración de un [ciclo de vida de aplicación mediante Hola CLI de Azure 2.0](service-fabric-application-lifecycle-azure-cli-2-0.md).</span><span class="sxs-lookup"><span data-stu-id="a374b-141">See hello reference doc on managing an [application life cycle using hello Azure CLI 2.0](service-fabric-application-lifecycle-azure-cli-2-0.md).</span></span>

<span data-ttu-id="a374b-142">Para una aplicación de ejemplo, [Hola de extracción del repositorio código de contenedor de Service Fabric los ejemplos en GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)</span><span class="sxs-lookup"><span data-stu-id="a374b-142">For an example application, [checkout hello Service Fabric container code samples on GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)</span></span>

## <a name="adding-more-services-tooan-existing-application"></a><span data-ttu-id="a374b-143">Agregar más servicios tooan existente aplicación</span><span class="sxs-lookup"><span data-stu-id="a374b-143">Adding more services tooan existing application</span></span>

<span data-ttu-id="a374b-144">tooadd otro contenedor de servicio aplicación tooan ya creado mediante `yo`, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="a374b-144">tooadd another container service tooan application already created using `yo`, perform hello following steps:</span></span>

1. <span data-ttu-id="a374b-145">Cambiar toohello raíz del directorio de aplicación existente de Hola.</span><span class="sxs-lookup"><span data-stu-id="a374b-145">Change directory toohello root of hello existing application.</span></span>  <span data-ttu-id="a374b-146">Por ejemplo, `cd ~/YeomanSamples/MyApplication`si `MyApplication` es aplicación Hola creado por Yeoman.</span><span class="sxs-lookup"><span data-stu-id="a374b-146">For example, `cd ~/YeomanSamples/MyApplication`, if `MyApplication` is hello application created by Yeoman.</span></span>
2. <span data-ttu-id="a374b-147">Ejecute `yo azuresfcontainer:AddService`</span><span class="sxs-lookup"><span data-stu-id="a374b-147">Run `yo azuresfcontainer:AddService`</span></span>

<a id="manually"></a>

## <a name="manually-package-and-deploy-a-container-image"></a><span data-ttu-id="a374b-148">Empaquetado e implementación manual de una imagen de contenedor</span><span class="sxs-lookup"><span data-stu-id="a374b-148">Manually package and deploy a container image</span></span>
<span data-ttu-id="a374b-149">proceso de Hola de empaquetar manualmente un servicio en contenedores se basa en hello pasos:</span><span class="sxs-lookup"><span data-stu-id="a374b-149">hello process of manually packaging a containerized service is based on hello following steps:</span></span>

1. <span data-ttu-id="a374b-150">Publicar el repositorio de tooyour de contenedores de Hola.</span><span class="sxs-lookup"><span data-stu-id="a374b-150">Publish hello containers tooyour repository.</span></span>
2. <span data-ttu-id="a374b-151">Crear estructura de directorios de paquetes de saludo.</span><span class="sxs-lookup"><span data-stu-id="a374b-151">Create hello package directory structure.</span></span>
3. <span data-ttu-id="a374b-152">Edite el archivo de manifiesto de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="a374b-152">Edit hello service manifest file.</span></span>
4. <span data-ttu-id="a374b-153">Edite el archivo de manifiesto de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="a374b-153">Edit hello application manifest file.</span></span>

## <a name="deploy-and-activate-a-container-image"></a><span data-ttu-id="a374b-154">Implementación y activación de una imagen de contenedor</span><span class="sxs-lookup"><span data-stu-id="a374b-154">Deploy and activate a container image</span></span>
<span data-ttu-id="a374b-155">Hola Service Fabric [modelo de aplicación](service-fabric-application-model.md), un contenedor representa un host de aplicación en la que varios servicios se colocan las réplicas.</span><span class="sxs-lookup"><span data-stu-id="a374b-155">In hello Service Fabric [application model](service-fabric-application-model.md), a container represents an application host in which multiple service replicas are placed.</span></span> <span data-ttu-id="a374b-156">toodeploy y activar un contenedor, el nombre de hello put de imagen del contenedor hello en un `ContainerHost` elemento en el manifiesto del servicio Hola.</span><span class="sxs-lookup"><span data-stu-id="a374b-156">toodeploy and activate a container, put hello name of hello container image into a `ContainerHost` element in hello service manifest.</span></span>

<span data-ttu-id="a374b-157">En el manifiesto del servicio hello, agregue un `ContainerHost` Hola punto de entrada.</span><span class="sxs-lookup"><span data-stu-id="a374b-157">In hello service manifest, add a `ContainerHost` for hello entry point.</span></span> <span data-ttu-id="a374b-158">A continuación, el conjunto de hello `ImageName` toobe nombre de Hola de repositorio de contenedor de Hola y de imagen.</span><span class="sxs-lookup"><span data-stu-id="a374b-158">Then set hello `ImageName` toobe hello name of hello container repository and image.</span></span> <span data-ttu-id="a374b-159">Hello manifiesto parcial siguiente muestra un ejemplo de cómo se denomina contenedor de hello toodeploy `myimage:v1` desde un repositorio, denominado `myrepo`:</span><span class="sxs-lookup"><span data-stu-id="a374b-159">hello following partial manifest shows an example of how toodeploy hello container called `myimage:v1` from a repository called `myrepo`:</span></span>

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

<span data-ttu-id="a374b-160">Puede proporcionar los comandos de entrada mediante la especificación de hello opcional `Commands` elemento con un conjunto delimitado por comas de toorun de comandos en el contenedor de Hola.</span><span class="sxs-lookup"><span data-stu-id="a374b-160">You can provide input commands by specifying hello optional `Commands` element with a comma-delimited set of commands toorun inside hello container.</span></span>

> [!NOTE]
> <span data-ttu-id="a374b-161">Si Hola imagen no tiene un carga de trabajo-punto de entrada definido, deberá tooexplicitly especificar comandos entradas dentro de `Commands` elemento con un conjunto delimitado por comas de toorun de comandos en el contenedor de hello, que se mantendrá el contenedor de Hola que se ejecuta después de inicio.</span><span class="sxs-lookup"><span data-stu-id="a374b-161">If hello image does not have a workload entry-point defined, then you need tooexplicitly specify input commands inside `Commands` element with a comma-delimited set of commands toorun inside hello container, which will keep hello container running after startup.</span></span>

## <a name="understand-resource-governance"></a><span data-ttu-id="a374b-162">Descripción de la regulación de recursos</span><span class="sxs-lookup"><span data-stu-id="a374b-162">Understand resource governance</span></span>
<span data-ttu-id="a374b-163">La regulación de recursos es una funcionalidad de contenedor de Hola que limita los recursos de Hola que Hola contenedor puede utilizar en el host de Hola.</span><span class="sxs-lookup"><span data-stu-id="a374b-163">Resource governance is a capability of hello container that restricts hello resources that hello container can use on hello host.</span></span> <span data-ttu-id="a374b-164">Hola `ResourceGovernancePolicy`, que se especifica en el manifiesto de aplicación Hola es los límites de recursos de toodeclare usado para un paquete de código de servicio.</span><span class="sxs-lookup"><span data-stu-id="a374b-164">hello `ResourceGovernancePolicy`, which is specified in hello application manifest is used toodeclare resource limits for a service code package.</span></span> <span data-ttu-id="a374b-165">Se pueden establecer límites de recursos para hello recursos siguientes:</span><span class="sxs-lookup"><span data-stu-id="a374b-165">Resource limits can be set for hello following resources:</span></span>

* <span data-ttu-id="a374b-166">Memoria</span><span class="sxs-lookup"><span data-stu-id="a374b-166">Memory</span></span>
* <span data-ttu-id="a374b-167">MemorySwap</span><span class="sxs-lookup"><span data-stu-id="a374b-167">MemorySwap</span></span>
* <span data-ttu-id="a374b-168">CpuShares (peso relativo de CPU)</span><span class="sxs-lookup"><span data-stu-id="a374b-168">CpuShares (CPU relative weight)</span></span>
* <span data-ttu-id="a374b-169">MemoryReservationInMB</span><span class="sxs-lookup"><span data-stu-id="a374b-169">MemoryReservationInMB</span></span>  
* <span data-ttu-id="a374b-170">BlkioWeight (peso relativo de BlockIO).</span><span class="sxs-lookup"><span data-stu-id="a374b-170">BlkioWeight (BlockIO relative weight).</span></span>

> [!NOTE]
> <span data-ttu-id="a374b-171">En una versión futura, se incluirá compatibilidad para especificar límites de E/S de bloques como IOP, BPS de lectura/escritura y mucho más.</span><span class="sxs-lookup"><span data-stu-id="a374b-171">In a future release, support for specifying specific block IO limits such as IOPs, read/write BPS, and others will be included.</span></span>
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

## <a name="authenticate-a-repository"></a><span data-ttu-id="a374b-172">Autenticación de un repositorio</span><span class="sxs-lookup"><span data-stu-id="a374b-172">Authenticate a repository</span></span>
<span data-ttu-id="a374b-173">toodownload un contenedor, es posible que tenga repositorio de contenedor de toohello tooprovide las credenciales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="a374b-173">toodownload a container, you might have tooprovide sign-in credentials toohello container repository.</span></span> <span data-ttu-id="a374b-174">Hola inicio de sesión credenciales, especificadas en el manifiesto de aplicación Hola, son utilizados toospecify Hola inicio de sesión en la información o clave SSH, para descargar la imagen de contenedor de Hola Hola repositorio de imágenes.</span><span class="sxs-lookup"><span data-stu-id="a374b-174">hello sign-in credentials, specified in hello application manifest, are used toospecify hello sign-in information, or SSH key, for downloading hello container image from hello image repository.</span></span> <span data-ttu-id="a374b-175">Hello en el ejemplo siguiente se muestra una cuenta llamada *Usuarioprueba* junto con la contraseña de hello en texto no cifrado (*no* recomendado):</span><span class="sxs-lookup"><span data-stu-id="a374b-175">hello following example shows an account called *TestUser* along with hello password in clear text (*not* recommended):</span></span>

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

<span data-ttu-id="a374b-176">Se recomienda que cifre la contraseña hello mediante un certificado que ha implementado la máquina toohello.</span><span class="sxs-lookup"><span data-stu-id="a374b-176">We recommend that you encrypt hello password by using a certificate that's deployed toohello machine.</span></span>

<span data-ttu-id="a374b-177">Hello en el ejemplo siguiente se muestra una cuenta llamada *Usuarioprueba*, donde contraseña hello se cifró mediante el uso de un certificado denominado *MyCert*.</span><span class="sxs-lookup"><span data-stu-id="a374b-177">hello following example shows an account called *TestUser*, where hello password was encrypted by using a certificate called *MyCert*.</span></span> <span data-ttu-id="a374b-178">Puede usar hello `Invoke-ServiceFabricEncryptText` texto PowerShell comando toocreate hello secreto cifrado de contraseña de Hola.</span><span class="sxs-lookup"><span data-stu-id="a374b-178">You can use hello `Invoke-ServiceFabricEncryptText` PowerShell command toocreate hello secret cipher text for hello password.</span></span> <span data-ttu-id="a374b-179">Para obtener más información, vea el artículo de hello [administrar secretos en aplicaciones de Service Fabric](service-fabric-application-secret-management.md).</span><span class="sxs-lookup"><span data-stu-id="a374b-179">For more information, see hello article [Managing secrets in Service Fabric applications](service-fabric-application-secret-management.md).</span></span>

<span data-ttu-id="a374b-180">clave privada de Hello del certificado de Hola que ha utilizado la contraseña de hello toodecrypt debe ser implementado toohello equipo local en un método fuera de banda.</span><span class="sxs-lookup"><span data-stu-id="a374b-180">hello private key of hello certificate that's used toodecrypt hello password must be deployed toohello local machine in an out-of-band method.</span></span> <span data-ttu-id="a374b-181">(en Azure esto se logra mediante Azure Resource Manager). A continuación, cuando Service Fabric implementa la máquina de toohello de paquete de servicio de hello, puede descifrar el secreto de Hola.</span><span class="sxs-lookup"><span data-stu-id="a374b-181">(In Azure, this method is Azure Resource Manager.) Then, when Service Fabric deploys hello service package toohello machine, it can decrypt hello secret.</span></span> <span data-ttu-id="a374b-182">Mediante el secreto de hello junto con el nombre de la cuenta de hello, a continuación, se pueda autenticar con el repositorio de contenedor de Hola.</span><span class="sxs-lookup"><span data-stu-id="a374b-182">By using hello secret along with hello account name, it can then authenticate with hello container repository.</span></span>

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

## <a name="configure-container-port-to-host-port-mapping"></a><span data-ttu-id="a374b-183">Configuración de la asignación de puerto a host de contenedor</span><span class="sxs-lookup"><span data-stu-id="a374b-183">Configure container port-to-host port mapping</span></span>
<span data-ttu-id="a374b-184">Puede configurar una toocommunicate de puerto que se utiliza de host con el contenedor de hello especificando un `PortBinding` en el manifiesto de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="a374b-184">You can configure a host port used toocommunicate with hello container by specifying a `PortBinding` in hello application manifest.</span></span> <span data-ttu-id="a374b-185">Hola puerto enlace mapas Hola puerto toowhich Hola servicio está escuchando en hello contenedor tooa puerto en el host de Hola.</span><span class="sxs-lookup"><span data-stu-id="a374b-185">hello port binding maps hello port toowhich hello service is listening inside hello container tooa port on hello host.</span></span>

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

## <a name="configure-container-to-container-discovery-and-communication"></a><span data-ttu-id="a374b-186">Configuración de detección y comunicación entre contenedores</span><span class="sxs-lookup"><span data-stu-id="a374b-186">Configure container-to-container discovery and communication</span></span>
<span data-ttu-id="a374b-187">Mediante el uso de hello `PortBinding` directiva, puede asignar un puerto de contenedor tooan `Endpoint` en el manifiesto del servicio Hola.</span><span class="sxs-lookup"><span data-stu-id="a374b-187">By using hello `PortBinding` policy, you can map a container port tooan `Endpoint` in hello service manifest.</span></span> <span data-ttu-id="a374b-188">Hola extremo `Endpoint1` puede especificar un puerto fijo (por ejemplo, el puerto 80).</span><span class="sxs-lookup"><span data-stu-id="a374b-188">hello endpoint `Endpoint1` can specify a fixed port (for example, port 80).</span></span> <span data-ttu-id="a374b-189">También no puede especificar ningún puerto en absoluto, en cuyo caso se elige un puerto aleatorio del intervalo de puertos de aplicaciones del clúster de Hola para usted.</span><span class="sxs-lookup"><span data-stu-id="a374b-189">It can also specify no port at all, in which case a random port from hello cluster's application port range is chosen for you.</span></span>

<span data-ttu-id="a374b-190">Si especifica un punto de conexión, utilizando hello `Endpoint` etiqueta en el manifiesto del servicio Hola de un contenedor de invitado, Service Fabric automáticamente puede publicar este servicio de nombres de punto de conexión toohello.</span><span class="sxs-lookup"><span data-stu-id="a374b-190">If you specify an endpoint, using hello `Endpoint` tag in hello service manifest of a guest container, Service Fabric can automatically publish this endpoint toohello Naming service.</span></span> <span data-ttu-id="a374b-191">Otros servicios que se ejecutan en el clúster de hello, por tanto, pueden detectar este contenedor mediante consultas REST de hello en resolver.</span><span class="sxs-lookup"><span data-stu-id="a374b-191">Other services that are running in hello cluster can thus discover this container using hello REST queries for resolving.</span></span>

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

<span data-ttu-id="a374b-192">Registrando con servicio de nomenclatura de hello, puede hacer fácilmente un contenedor a la comunicación en el código de hello dentro de su contenedor mediante el uso de hello [proxy inverso](service-fabric-reverseproxy.md).</span><span class="sxs-lookup"><span data-stu-id="a374b-192">By registering with hello Naming service, you can easily do container-to-container communication in hello code within your container by using hello [reverse proxy](service-fabric-reverseproxy.md).</span></span> <span data-ttu-id="a374b-193">La comunicación se realiza proporcionando el puerto de escucha de http de proxy inverso de Hola y el nombre de hello de servicios de Hola que desee toocommunicate con como variables de entorno.</span><span class="sxs-lookup"><span data-stu-id="a374b-193">Communication is performed by providing hello reverse proxy http listening port and hello name of hello services that you want toocommunicate with as environment variables.</span></span> <span data-ttu-id="a374b-194">Para obtener más información, vea la sección siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="a374b-194">For more information, see hello next section.</span></span>

## <a name="configure-and-set-environment-variables"></a><span data-ttu-id="a374b-195">Configuración y establecimiento de variables de entorno</span><span class="sxs-lookup"><span data-stu-id="a374b-195">Configure and set environment variables</span></span>
<span data-ttu-id="a374b-196">Las variables de entorno se pueden especificar para cada paquete de código en el manifiesto del servicio hello, tanto para los servicios que se implementan en contenedores o para los servicios que se implementan como archivos ejecutables de procesos e invitados.</span><span class="sxs-lookup"><span data-stu-id="a374b-196">Environment variables can be specified for each code package in hello service manifest, both for services that are deployed in containers or for services that are deployed as processes/guest executables.</span></span> <span data-ttu-id="a374b-197">Estos valores de variable de entorno se pueden invalidar específicamente en el manifiesto de aplicación Hola o especificados durante la implementación como parámetros de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a374b-197">These environment variable values can be overridden specifically in hello application manifest or specified during deployment as application parameters.</span></span>

<span data-ttu-id="a374b-198">Hello fragmento XML de manifiesto de servicio siguiente muestra un ejemplo de cómo toospecify las variables de entorno para un paquete de código:</span><span class="sxs-lookup"><span data-stu-id="a374b-198">hello following service manifest XML snippet shows an example of how toospecify environment variables for a code package:</span></span>

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

<span data-ttu-id="a374b-199">Estas variables de entorno pueden reemplazarse en nivel de manifiesto de aplicación Hola:</span><span class="sxs-lookup"><span data-stu-id="a374b-199">These environment variables can be overridden at hello application manifest level:</span></span>

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <EnvironmentOverrides CodePackageRef="FrontendService.Code">
            <EnvironmentVariable Name="BackendServiceName" Value="[BackendSvc]"/>
            <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
        </EnvironmentOverrides>
    </ServiceManifestImport>
```

<span data-ttu-id="a374b-200">En el ejemplo anterior de hello, se especifica un valor explícito para hello `HttpGateway` variable de entorno (19000), aunque se establezca el valor de Hola para `BackendServiceName` parámetro mediante hello `[BackendSvc]` parámetro de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a374b-200">In hello previous example, we specified an explicit value for hello `HttpGateway` environment variable (19000), while we set hello value for `BackendServiceName` parameter via hello `[BackendSvc]` application parameter.</span></span> <span data-ttu-id="a374b-201">Estas opciones le permiten toospecify valor de Hola para `BackendServiceName`valor al implementar la aplicación hello y no tiene un valor fijo en el manifiesto de Hola.</span><span class="sxs-lookup"><span data-stu-id="a374b-201">These settings enable you toospecify hello value for `BackendServiceName`value when you deploy hello application and not have a fixed value in hello manifest.</span></span>

## <a name="complete-examples-for-application-and-service-manifest"></a><span data-ttu-id="a374b-202">Ejemplos completos de manifiesto de servicio y de aplicación</span><span class="sxs-lookup"><span data-stu-id="a374b-202">Complete examples for application and service manifest</span></span>

<span data-ttu-id="a374b-203">Este es un ejemplo de un manifiesto de aplicación:</span><span class="sxs-lookup"><span data-stu-id="a374b-203">An example application manifest follows:</span></span>

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

<span data-ttu-id="a374b-204">A continuación se muestra un ejemplo de manifiesto de servicio (especificado en hello anterior manifiesto de aplicación):</span><span class="sxs-lookup"><span data-stu-id="a374b-204">An example service manifest (specified in hello preceding application manifest) follows:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="a374b-205">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a374b-205">Next steps</span></span>
<span data-ttu-id="a374b-206">Ahora que ha implementado un servicio en contenedores, obtenga información acerca de cómo toomanage su ciclo de vida leyendo [ciclo de vida de aplicación de Service Fabric](service-fabric-application-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="a374b-206">Now that you have deployed a containerized service, learn how toomanage its lifecycle by reading [Service Fabric application lifecycle](service-fabric-application-lifecycle.md).</span></span>

* [<span data-ttu-id="a374b-207">Información general: Service Fabric y contenedores</span><span class="sxs-lookup"><span data-stu-id="a374b-207">Overview of Service Fabric and containers</span></span>](service-fabric-containers-overview.md)
* [<span data-ttu-id="a374b-208">Interactuar con los clústeres de Service Fabric usando Hola CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="a374b-208">Interacting with Service Fabric clusters using hello Azure CLI</span></span>](service-fabric-azure-cli.md)

<!-- Images -->
[sf-yeoman]: ./media/service-fabric-deploy-container-linux/sf-container-yeoman1.png

## <a name="related-articles"></a><span data-ttu-id="a374b-209">Artículos relacionados</span><span class="sxs-lookup"><span data-stu-id="a374b-209">Related articles</span></span>

* <span data-ttu-id="a374b-210">[Getting started with Service Fabric and Azure CLI 2.0](service-fabric-azure-cli-2-0.md) (Introducción a Service Fabric y la CLI de Azure 2.0)</span><span class="sxs-lookup"><span data-stu-id="a374b-210">[Getting started with Service Fabric and Azure CLI 2.0](service-fabric-azure-cli-2-0.md)</span></span>
* <span data-ttu-id="a374b-211">[Getting started with Service Fabric XPlat CLI](service-fabric-azure-cli.md) (Introducción a la CLI de XPlat de Service Fabric)</span><span class="sxs-lookup"><span data-stu-id="a374b-211">[Getting started with Service Fabric XPlat CLI](service-fabric-azure-cli.md)</span></span>
