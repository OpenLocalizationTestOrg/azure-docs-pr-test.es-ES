---
title: "Service Fabric e implementación de contenedores en Linux | Microsoft Docs"
description: "Service Fabric y el uso de contenedores de Linux para implementar aplicaciones de microservicios. En este artículo se describen las funcionalidades que ofrece Service Fabric para los contenedores y cómo implementar una imagen de contenedor de Linux en un clúster"
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
ms.openlocfilehash: 9dcec753e5f999a1bac07276373c0c25f89ec58d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-a-linux-container-to-service-fabric"></a><span data-ttu-id="7d002-104">Implementar un contenedor de Linux en Service Fabric</span><span class="sxs-lookup"><span data-stu-id="7d002-104">Deploy a Linux container to Service Fabric</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7d002-105">Implementación de un contenedor de Windows</span><span class="sxs-lookup"><span data-stu-id="7d002-105">Deploy Windows Container</span></span>](service-fabric-deploy-container.md)
> * [<span data-ttu-id="7d002-106">Implementar un contenedor de Linux</span><span class="sxs-lookup"><span data-stu-id="7d002-106">Deploy Linux Container</span></span>](service-fabric-deploy-container-linux.md)
>
>

<span data-ttu-id="7d002-107">Este artículo lo guiará a través de la creación de servicios de contenedor en contenedores de Docker en Linux.</span><span class="sxs-lookup"><span data-stu-id="7d002-107">This article walks you through building containerized services in Docker containers on Linux.</span></span>

<span data-ttu-id="7d002-108">Service Fabric tiene varias funcionalidades de contenedor que le ayudarán a crear aplicaciones que se componen de microservicios en contenedores.</span><span class="sxs-lookup"><span data-stu-id="7d002-108">Service Fabric has several container capabilities that help you with building applications that are composed of microservices that are containerized.</span></span> <span data-ttu-id="7d002-109">Son los llamados servicios en contenedores.</span><span class="sxs-lookup"><span data-stu-id="7d002-109">These services are called containerized services.</span></span>

<span data-ttu-id="7d002-110">Entre estas funcionalidades, cabe destacar:</span><span class="sxs-lookup"><span data-stu-id="7d002-110">The capabilities include;</span></span>

* <span data-ttu-id="7d002-111">Activación e implementación de la imagen de contenedor</span><span class="sxs-lookup"><span data-stu-id="7d002-111">Container image deployment and activation</span></span>
* <span data-ttu-id="7d002-112">Regulador de recursos</span><span class="sxs-lookup"><span data-stu-id="7d002-112">Resource governance</span></span>
* <span data-ttu-id="7d002-113">Autenticación de repositorio</span><span class="sxs-lookup"><span data-stu-id="7d002-113">Repository authentication</span></span>
* <span data-ttu-id="7d002-114">Asignación de puerto a host de contenedor</span><span class="sxs-lookup"><span data-stu-id="7d002-114">Container port to host port mapping</span></span>
* <span data-ttu-id="7d002-115">Detección y comunicación entre contenedores</span><span class="sxs-lookup"><span data-stu-id="7d002-115">Container-to-container discovery and communication</span></span>
* <span data-ttu-id="7d002-116">Capacidad de configurar y establecer variables de entorno</span><span class="sxs-lookup"><span data-stu-id="7d002-116">Ability to configure and set environment variables</span></span>

## <a name="packaging-a-docker-container-with-yeoman"></a><span data-ttu-id="7d002-117">Empaquetado de un contenedor de Docker con Yeoman</span><span class="sxs-lookup"><span data-stu-id="7d002-117">Packaging a docker container with yeoman</span></span>
<span data-ttu-id="7d002-118">Al empaquetar un contenedor en Linux, puede usar una plantilla de Yeoman o [crear el paquete de aplicación manualmente](#manually).</span><span class="sxs-lookup"><span data-stu-id="7d002-118">When packaging a container on Linux, you can choose either to use a yeoman template or [create the application package manually](#manually).</span></span>

<span data-ttu-id="7d002-119">Una aplicación de Service Fabric puede contener uno o varios contenedores, cada uno de ellos con un rol específico en la prestación de la funcionalidad de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7d002-119">A Service Fabric application can contain one or more containers, each with a specific role in delivering the application's functionality.</span></span> <span data-ttu-id="7d002-120">El SDK de Service Fabric para Linux incluye un generador [Yeoman](http://yeoman.io/) que permite crear fácilmente la aplicación y agregar una imagen de contenedor.</span><span class="sxs-lookup"><span data-stu-id="7d002-120">The Service Fabric SDK for Linux includes a [Yeoman](http://yeoman.io/) generator that makes it easy to create your application and add a container image.</span></span> <span data-ttu-id="7d002-121">Vamos a usar Yeoman para crear una aplicación con un único contenedor de Docker denominado "*SimpleContainerApp*".</span><span class="sxs-lookup"><span data-stu-id="7d002-121">Let's use Yeoman to create an application with a single Docker container called *SimpleContainerApp*.</span></span> <span data-ttu-id="7d002-122">Puede agregar más servicios más adelante editando los archivos de manifiesto generados.</span><span class="sxs-lookup"><span data-stu-id="7d002-122">You can add more services later by editing the generated manifest files.</span></span>

## <a name="install-docker-on-your-development-box"></a><span data-ttu-id="7d002-123">Instalación de un contenedor de Docker en el cuadro de desarrollo</span><span class="sxs-lookup"><span data-stu-id="7d002-123">Install Docker on your development box</span></span>

<span data-ttu-id="7d002-124">Ejecute los comandos siguientes para instalar el contenedor de Docker en el cuadro de desarrollo de Linux (si utiliza la imagen de Vagrant en OSX, el contenedor de Docker ya estará instalado):</span><span class="sxs-lookup"><span data-stu-id="7d002-124">Run the following commands to install docker on your Linux development box (if you are using the vagrant image on OSX, docker is already installed):</span></span>

```bash
    sudo apt-get install wget
    wget -qO- https://get.docker.io/ | sh
```

## <a name="create-the-application"></a><span data-ttu-id="7d002-125">Creación de la aplicación</span><span class="sxs-lookup"><span data-stu-id="7d002-125">Create the application</span></span>
1. <span data-ttu-id="7d002-126">En un terminal, escriba `yo azuresfcontainer`.</span><span class="sxs-lookup"><span data-stu-id="7d002-126">In a terminal, type `yo azuresfcontainer`.</span></span>
2. <span data-ttu-id="7d002-127">Dé nombre a la aplicación; por ejemplo, mycontainerap.</span><span class="sxs-lookup"><span data-stu-id="7d002-127">Name your application - for example, mycontainerap</span></span>
3. <span data-ttu-id="7d002-128">Proporcione la dirección URL de la imagen de contenedor desde un repositorio de DockerHub.</span><span class="sxs-lookup"><span data-stu-id="7d002-128">Provide the URL for the container image from a DockerHub repo.</span></span> <span data-ttu-id="7d002-129">El parámetro de imagen toma la forma [repositorio]/[nombre de la imagen]</span><span class="sxs-lookup"><span data-stu-id="7d002-129">The image parameter takes the form [repo]/[image name]</span></span>
4. <span data-ttu-id="7d002-130">Si la imagen no tiene ningún punto de entrada de carga de trabajo definido, debe especificar explícitamente comandos de entrada con un conjunto delimitado por comas de comandos que se ejecutarán dentro del contenedor, lo que mantendrá el contenedor en ejecución después del inicio.</span><span class="sxs-lookup"><span data-stu-id="7d002-130">If the image does not have a workload entry-point defined, then you need to explicitly specify input commands with a comma-delimited set of commands to run inside the container, which will keep the container running after startup.</span></span>

![Generador Yeoman de Service Fabric para contenedores][sf-yeoman]

## <a name="deploy-the-application"></a><span data-ttu-id="7d002-132">Implementación de la aplicación</span><span class="sxs-lookup"><span data-stu-id="7d002-132">Deploy the application</span></span>

### <a name="using-xplat-cli"></a><span data-ttu-id="7d002-133">Uso de la CLI multiplataforma</span><span class="sxs-lookup"><span data-stu-id="7d002-133">Using XPlat CLI</span></span>
<span data-ttu-id="7d002-134">Una vez compilada la aplicación, puede implementarla en el clúster local mediante la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="7d002-134">Once the application is built, you can deploy it to the local cluster using the Azure CLI.</span></span>

1. <span data-ttu-id="7d002-135">Conéctese al clúster de Service Fabric local.</span><span class="sxs-lookup"><span data-stu-id="7d002-135">Connect to the local Service Fabric cluster.</span></span>

    ```bash
    azure servicefabric cluster connect
    ```

2. <span data-ttu-id="7d002-136">Use el script de instalación proporcionado en la plantilla para copiar el paquete de aplicación en el almacén de imágenes del clúster, registrar el tipo de aplicación y crear una instancia de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7d002-136">Use the install script provided in the template to copy the application package to the cluster's image store, register the application type, and create an instance of the application.</span></span>

    ```bash
    ./install.sh
    ```

3. <span data-ttu-id="7d002-137">Abra un explorador y vaya a Service Fabric Explorer en http://localhost:19080/Explorer (reemplace localhost por la dirección IP privada de la VM si usa Vagrant en Mac OS X).</span><span class="sxs-lookup"><span data-stu-id="7d002-137">Open a browser and navigate to Service Fabric Explorer at http://localhost:19080/Explorer (replace localhost with the private IP of the VM if using Vagrant on Mac OS X).</span></span>
4. <span data-ttu-id="7d002-138">Expanda el nodo Applications y observe que ahora hay una entrada para su tipo de aplicación y otra para la primera instancia de ese tipo.</span><span class="sxs-lookup"><span data-stu-id="7d002-138">Expand the Applications node and note that there is now an entry for your application type and another for the first instance of that type.</span></span>
5. <span data-ttu-id="7d002-139">Para eliminar la instancia de aplicación y anular el registro del tipo de aplicación, utilice el script de desinstalación proporcionado en la plantilla.</span><span class="sxs-lookup"><span data-stu-id="7d002-139">Use the uninstall script provided in the template to delete the application instance and unregister the application type.</span></span>

    ```bash
    ./uninstall.sh
    ```

### <a name="using-azure-cli-20"></a><span data-ttu-id="7d002-140">Uso de la CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="7d002-140">Using Azure CLI 2.0</span></span>

<span data-ttu-id="7d002-141">Consulte la documentación de referencia sobre la administración de un [ciclo de vida de aplicación mediante la CLI de Azure 2.0](service-fabric-application-lifecycle-azure-cli-2-0.md).</span><span class="sxs-lookup"><span data-stu-id="7d002-141">See the reference doc on managing an [application life cycle using the Azure CLI 2.0](service-fabric-application-lifecycle-azure-cli-2-0.md).</span></span>

<span data-ttu-id="7d002-142">Para ver una aplicación de ejemplo, [eche un vistazo a los ejemplos de código de contenedor de Service Fabric en GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers).</span><span class="sxs-lookup"><span data-stu-id="7d002-142">For an example application, [checkout the Service Fabric container code samples on GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)</span></span>

## <a name="adding-more-services-to-an-existing-application"></a><span data-ttu-id="7d002-143">Incorporación de más servicios a una aplicación existente</span><span class="sxs-lookup"><span data-stu-id="7d002-143">Adding more services to an existing application</span></span>

<span data-ttu-id="7d002-144">Para agregar otro servicio de contenedor a una aplicación ya creada mediante `yo`, realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="7d002-144">To add another container service to an application already created using `yo`, perform the following steps:</span></span>

1. <span data-ttu-id="7d002-145">Cambie el directorio al directorio raíz de la aplicación existente.</span><span class="sxs-lookup"><span data-stu-id="7d002-145">Change directory to the root of the existing application.</span></span>  <span data-ttu-id="7d002-146">Por ejemplo, `cd ~/YeomanSamples/MyApplication`, si `MyApplication` es la aplicación creada por Yeoman.</span><span class="sxs-lookup"><span data-stu-id="7d002-146">For example, `cd ~/YeomanSamples/MyApplication`, if `MyApplication` is the application created by Yeoman.</span></span>
2. <span data-ttu-id="7d002-147">Ejecute `yo azuresfcontainer:AddService`</span><span class="sxs-lookup"><span data-stu-id="7d002-147">Run `yo azuresfcontainer:AddService`</span></span>

<a id="manually"></a>

## <a name="manually-package-and-deploy-a-container-image"></a><span data-ttu-id="7d002-148">Empaquetado e implementación manual de una imagen de contenedor</span><span class="sxs-lookup"><span data-stu-id="7d002-148">Manually package and deploy a container image</span></span>
<span data-ttu-id="7d002-149">El proceso de empaquetado manual de un servicio en contenedor se basa en los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="7d002-149">The process of manually packaging a containerized service is based on the following steps:</span></span>

1. <span data-ttu-id="7d002-150">Publicar los contenedores en el repositorio.</span><span class="sxs-lookup"><span data-stu-id="7d002-150">Publish the containers to your repository.</span></span>
2. <span data-ttu-id="7d002-151">Crear la estructura de directorios del paquete.</span><span class="sxs-lookup"><span data-stu-id="7d002-151">Create the package directory structure.</span></span>
3. <span data-ttu-id="7d002-152">Editar el archivo de manifiesto de servicio.</span><span class="sxs-lookup"><span data-stu-id="7d002-152">Edit the service manifest file.</span></span>
4. <span data-ttu-id="7d002-153">Editar el archivo de manifiesto de aplicación.</span><span class="sxs-lookup"><span data-stu-id="7d002-153">Edit the application manifest file.</span></span>

## <a name="deploy-and-activate-a-container-image"></a><span data-ttu-id="7d002-154">Implementación y activación de una imagen de contenedor</span><span class="sxs-lookup"><span data-stu-id="7d002-154">Deploy and activate a container image</span></span>
<span data-ttu-id="7d002-155">En el [modelo de aplicación](service-fabric-application-model.md)de Service Fabric, un contenedor representa un host de la aplicación en el que se colocan varias réplicas de servicio.</span><span class="sxs-lookup"><span data-stu-id="7d002-155">In the Service Fabric [application model](service-fabric-application-model.md), a container represents an application host in which multiple service replicas are placed.</span></span> <span data-ttu-id="7d002-156">Para implementar y activar un contenedor, ponga el nombre de la imagen de contenedor en un elemento `ContainerHost` en el manifiesto de servicio.</span><span class="sxs-lookup"><span data-stu-id="7d002-156">To deploy and activate a container, put the name of the container image into a `ContainerHost` element in the service manifest.</span></span>

<span data-ttu-id="7d002-157">En el manifiesto de servicio, añada un elemento `ContainerHost` para el punto de entrada.</span><span class="sxs-lookup"><span data-stu-id="7d002-157">In the service manifest, add a `ContainerHost` for the entry point.</span></span> <span data-ttu-id="7d002-158">A continuación, establezca el elemento `ImageName` como nombre de la imagen y el repositorio del contenedor.</span><span class="sxs-lookup"><span data-stu-id="7d002-158">Then set the `ImageName` to be the name of the container repository and image.</span></span> <span data-ttu-id="7d002-159">El siguiente manifiesto parcial muestra un ejemplo de cómo implementar el contenedor llamado `myimage:v1` desde un repositorio denominado `myrepo`:</span><span class="sxs-lookup"><span data-stu-id="7d002-159">The following partial manifest shows an example of how to deploy the container called `myimage:v1` from a repository called `myrepo`:</span></span>

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

<span data-ttu-id="7d002-160">Puede proporcionar los comandos de entrada especificando el elemento opcional `Commands` con un conjunto de comandos delimitados por comas que se ejecutarán dentro del contenedor.</span><span class="sxs-lookup"><span data-stu-id="7d002-160">You can provide input commands by specifying the optional `Commands` element with a comma-delimited set of commands to run inside the container.</span></span>

> [!NOTE]
> <span data-ttu-id="7d002-161">Si la imagen no tiene ningún punto de entrada de carga de trabajo definido, debe especificar explícitamente comandos de entrada dentro del elemento `Commands` con un conjunto delimitado por comas de comandos que se ejecutarán dentro del contenedor, lo que mantendrá el contenedor en ejecución después del inicio.</span><span class="sxs-lookup"><span data-stu-id="7d002-161">If the image does not have a workload entry-point defined, then you need to explicitly specify input commands inside `Commands` element with a comma-delimited set of commands to run inside the container, which will keep the container running after startup.</span></span>

## <a name="understand-resource-governance"></a><span data-ttu-id="7d002-162">Descripción de la regulación de recursos</span><span class="sxs-lookup"><span data-stu-id="7d002-162">Understand resource governance</span></span>
<span data-ttu-id="7d002-163">La regulación de recursos es una funcionalidad del contenedor que permite restringir los recursos que puede usar el contenedor en el host.</span><span class="sxs-lookup"><span data-stu-id="7d002-163">Resource governance is a capability of the container that restricts the resources that the container can use on the host.</span></span> <span data-ttu-id="7d002-164">El elemento `ResourceGovernancePolicy`, especificado en el manifiesto de la aplicación, se utiliza para declarar los límites de recursos para un paquete de código de servicio.</span><span class="sxs-lookup"><span data-stu-id="7d002-164">The `ResourceGovernancePolicy`, which is specified in the application manifest is used to declare resource limits for a service code package.</span></span> <span data-ttu-id="7d002-165">Es posible establecer límites para los siguientes recursos:</span><span class="sxs-lookup"><span data-stu-id="7d002-165">Resource limits can be set for the following resources:</span></span>

* <span data-ttu-id="7d002-166">Memoria</span><span class="sxs-lookup"><span data-stu-id="7d002-166">Memory</span></span>
* <span data-ttu-id="7d002-167">MemorySwap</span><span class="sxs-lookup"><span data-stu-id="7d002-167">MemorySwap</span></span>
* <span data-ttu-id="7d002-168">CpuShares (peso relativo de CPU)</span><span class="sxs-lookup"><span data-stu-id="7d002-168">CpuShares (CPU relative weight)</span></span>
* <span data-ttu-id="7d002-169">MemoryReservationInMB</span><span class="sxs-lookup"><span data-stu-id="7d002-169">MemoryReservationInMB</span></span>  
* <span data-ttu-id="7d002-170">BlkioWeight (peso relativo de BlockIO).</span><span class="sxs-lookup"><span data-stu-id="7d002-170">BlkioWeight (BlockIO relative weight).</span></span>

> [!NOTE]
> <span data-ttu-id="7d002-171">En una versión futura, se incluirá compatibilidad para especificar límites de E/S de bloques como IOP, BPS de lectura/escritura y mucho más.</span><span class="sxs-lookup"><span data-stu-id="7d002-171">In a future release, support for specifying specific block IO limits such as IOPs, read/write BPS, and others will be included.</span></span>
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

## <a name="authenticate-a-repository"></a><span data-ttu-id="7d002-172">Autenticación de un repositorio</span><span class="sxs-lookup"><span data-stu-id="7d002-172">Authenticate a repository</span></span>
<span data-ttu-id="7d002-173">Para descargar un contenedor, puede que tenga que proporcionar credenciales de inicio de sesión para el repositorio de contenedor.</span><span class="sxs-lookup"><span data-stu-id="7d002-173">To download a container, you might have to provide sign-in credentials to the container repository.</span></span> <span data-ttu-id="7d002-174">Las credenciales de inicio de sesión incluidas en el manifiesto de la aplicación se usan para especificar la información de inicio de sesión, o clave SSH, para descargar la imagen del contenedor desde el repositorio de imágenes.</span><span class="sxs-lookup"><span data-stu-id="7d002-174">The sign-in credentials, specified in the application manifest, are used to specify the sign-in information, or SSH key, for downloading the container image from the image repository.</span></span> <span data-ttu-id="7d002-175">En el ejemplo siguiente se muestra una cuenta llamada *TestUser* junto con la contraseña no cifrada (*no* recomendado):</span><span class="sxs-lookup"><span data-stu-id="7d002-175">The following example shows an account called *TestUser* along with the password in clear text (*not* recommended):</span></span>

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

<span data-ttu-id="7d002-176">Se recomienda cifrar la contraseña mediante un certificado implementado en la máquina.</span><span class="sxs-lookup"><span data-stu-id="7d002-176">We recommend that you encrypt the password by using a certificate that's deployed to the machine.</span></span>

<span data-ttu-id="7d002-177">El ejemplo siguiente muestra una cuenta denominada *TestUser* con la contraseña cifrada mediante un certificado llamado *MyCert*.</span><span class="sxs-lookup"><span data-stu-id="7d002-177">The following example shows an account called *TestUser*, where the password was encrypted by using a certificate called *MyCert*.</span></span> <span data-ttu-id="7d002-178">Puede usar el comando de PowerShell `Invoke-ServiceFabricEncryptText` para crear el texto cifrado secreto de la contraseña.</span><span class="sxs-lookup"><span data-stu-id="7d002-178">You can use the `Invoke-ServiceFabricEncryptText` PowerShell command to create the secret cipher text for the password.</span></span> <span data-ttu-id="7d002-179">Para más información, consulte el artículo [Administración de secretos en aplicaciones de Service Fabric](service-fabric-application-secret-management.md).</span><span class="sxs-lookup"><span data-stu-id="7d002-179">For more information, see the article [Managing secrets in Service Fabric applications](service-fabric-application-secret-management.md).</span></span>

<span data-ttu-id="7d002-180">La clave privada del certificado que se usa para descifrar la contraseña se debe implementar en la máquina local con un método fuera de banda</span><span class="sxs-lookup"><span data-stu-id="7d002-180">The private key of the certificate that's used to decrypt the password must be deployed to the local machine in an out-of-band method.</span></span> <span data-ttu-id="7d002-181">(en Azure esto se logra mediante Azure Resource Manager). Posteriormente, cuando Service Fabric implementa el paquete de servicio en la máquina, es capaz de descifrar el secreto.</span><span class="sxs-lookup"><span data-stu-id="7d002-181">(In Azure, this method is Azure Resource Manager.) Then, when Service Fabric deploys the service package to the machine, it can decrypt the secret.</span></span> <span data-ttu-id="7d002-182">Al usar el secreto junto con el nombre de cuenta, puede autenticarse con el repositorio de contenedor.</span><span class="sxs-lookup"><span data-stu-id="7d002-182">By using the secret along with the account name, it can then authenticate with the container repository.</span></span>

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

## <a name="configure-container-port-to-host-port-mapping"></a><span data-ttu-id="7d002-183">Configuración de la asignación de puerto a host de contenedor</span><span class="sxs-lookup"><span data-stu-id="7d002-183">Configure container port-to-host port mapping</span></span>
<span data-ttu-id="7d002-184">Puede configurar un puerto de host utilizado para comunicarse con el contenedor mediante la especificación de un elemento `PortBinding` en el manifiesto de aplicación.</span><span class="sxs-lookup"><span data-stu-id="7d002-184">You can configure a host port used to communicate with the container by specifying a `PortBinding` in the application manifest.</span></span> <span data-ttu-id="7d002-185">El enlace de puerto asigna el puerto que el servicio está escuchando dentro del contenedor a un puerto en el host.</span><span class="sxs-lookup"><span data-stu-id="7d002-185">The port binding maps the port to which the service is listening inside the container to a port on the host.</span></span>

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

## <a name="configure-container-to-container-discovery-and-communication"></a><span data-ttu-id="7d002-186">Configuración de detección y comunicación entre contenedores</span><span class="sxs-lookup"><span data-stu-id="7d002-186">Configure container-to-container discovery and communication</span></span>
<span data-ttu-id="7d002-187">Mediante el uso de la directiva `PortBinding`, puede asignar un puerto de contenedor a un `Endpoint` en el manifiesto de servicio.</span><span class="sxs-lookup"><span data-stu-id="7d002-187">By using the `PortBinding` policy, you can map a container port to an `Endpoint` in the service manifest.</span></span> <span data-ttu-id="7d002-188">El punto de conexión `Endpoint1` puede especificar un puerto fijo (por ejemplo, el puerto 80).</span><span class="sxs-lookup"><span data-stu-id="7d002-188">The endpoint `Endpoint1` can specify a fixed port (for example, port 80).</span></span> <span data-ttu-id="7d002-189">También puede no especificar ningún puerto, en cuyo caso se elegirá un puerto aleatorio del intervalo de puertos de la aplicación del clúster.</span><span class="sxs-lookup"><span data-stu-id="7d002-189">It can also specify no port at all, in which case a random port from the cluster's application port range is chosen for you.</span></span>

<span data-ttu-id="7d002-190">Si especifica un punto de conexión, al usar la etiqueta `Endpoint` en el manifiesto de servicio de un contenedor invitado, Service Fabric puede publicar automáticamente este punto de conexión en el servicio de nombres.</span><span class="sxs-lookup"><span data-stu-id="7d002-190">If you specify an endpoint, using the `Endpoint` tag in the service manifest of a guest container, Service Fabric can automatically publish this endpoint to the Naming service.</span></span> <span data-ttu-id="7d002-191">De este modo, otros servicios que se ejecutan en el clúster podrán detectar que este contenedor usa las consultas REST para la resolución.</span><span class="sxs-lookup"><span data-stu-id="7d002-191">Other services that are running in the cluster can thus discover this container using the REST queries for resolving.</span></span>

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

<span data-ttu-id="7d002-192">Al registrarse con el servicio de nombres, se puede establecer fácilmente la comunicación de contenedor a contenedor en el código dentro del contenedor mediante el [proxy inverso](service-fabric-reverseproxy.md).</span><span class="sxs-lookup"><span data-stu-id="7d002-192">By registering with the Naming service, you can easily do container-to-container communication in the code within your container by using the [reverse proxy](service-fabric-reverseproxy.md).</span></span> <span data-ttu-id="7d002-193">La comunicación se establece al proporcionar el puerto de escucha http de proxy inverso y el nombre de los servicios con los que desea comunicarse como variables de entorno.</span><span class="sxs-lookup"><span data-stu-id="7d002-193">Communication is performed by providing the reverse proxy http listening port and the name of the services that you want to communicate with as environment variables.</span></span> <span data-ttu-id="7d002-194">Para más información, consulte la siguiente sección.</span><span class="sxs-lookup"><span data-stu-id="7d002-194">For more information, see the next section.</span></span>

## <a name="configure-and-set-environment-variables"></a><span data-ttu-id="7d002-195">Configuración y establecimiento de variables de entorno</span><span class="sxs-lookup"><span data-stu-id="7d002-195">Configure and set environment variables</span></span>
<span data-ttu-id="7d002-196">Las variables de entorno se pueden especificar para cada paquete de código en el manifiesto de servicio, tanto para los servicios implementados en contenedores como para los servicios implementados como archivos ejecutables de procesos o invitados.</span><span class="sxs-lookup"><span data-stu-id="7d002-196">Environment variables can be specified for each code package in the service manifest, both for services that are deployed in containers or for services that are deployed as processes/guest executables.</span></span> <span data-ttu-id="7d002-197">Estos valores de variables de entorno se pueden invalidar específicamente en el manifiesto de aplicación o se pueden especificar durante la implementación como parámetros de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7d002-197">These environment variable values can be overridden specifically in the application manifest or specified during deployment as application parameters.</span></span>

<span data-ttu-id="7d002-198">El siguiente fragmento de código XML del manifiesto de servicio muestra un ejemplo de cómo especificar variables de entorno para un paquete de código:</span><span class="sxs-lookup"><span data-stu-id="7d002-198">The following service manifest XML snippet shows an example of how to specify environment variables for a code package:</span></span>

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

<span data-ttu-id="7d002-199">Estas variables de entorno se pueden invalidar en el nivel del manifiesto de aplicación:</span><span class="sxs-lookup"><span data-stu-id="7d002-199">These environment variables can be overridden at the application manifest level:</span></span>

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <EnvironmentOverrides CodePackageRef="FrontendService.Code">
            <EnvironmentVariable Name="BackendServiceName" Value="[BackendSvc]"/>
            <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
        </EnvironmentOverrides>
    </ServiceManifestImport>
```

<span data-ttu-id="7d002-200">En el ejemplo anterior, se ha especificado un valor explícito para la variable de entorno `HttpGateway` (19000), mientras que el valor del parámetro `BackendServiceName` se ha establecido a través del parámetro de la aplicación `[BackendSvc]`.</span><span class="sxs-lookup"><span data-stu-id="7d002-200">In the previous example, we specified an explicit value for the `HttpGateway` environment variable (19000), while we set the value for `BackendServiceName` parameter via the `[BackendSvc]` application parameter.</span></span> <span data-ttu-id="7d002-201">Esta configuración permite especificar el valor de `BackendServiceName` al implementar la aplicación sin necesidad de tener un valor fijo en el manifiesto.</span><span class="sxs-lookup"><span data-stu-id="7d002-201">These settings enable you to specify the value for `BackendServiceName`value when you deploy the application and not have a fixed value in the manifest.</span></span>

## <a name="complete-examples-for-application-and-service-manifest"></a><span data-ttu-id="7d002-202">Ejemplos completos de manifiesto de servicio y de aplicación</span><span class="sxs-lookup"><span data-stu-id="7d002-202">Complete examples for application and service manifest</span></span>

<span data-ttu-id="7d002-203">Este es un ejemplo de un manifiesto de aplicación:</span><span class="sxs-lookup"><span data-stu-id="7d002-203">An example application manifest follows:</span></span>

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

<span data-ttu-id="7d002-204">Este es un ejemplo de manifiesto de servicio (especificado en el manifiesto de aplicación anterior):</span><span class="sxs-lookup"><span data-stu-id="7d002-204">An example service manifest (specified in the preceding application manifest) follows:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="7d002-205">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7d002-205">Next steps</span></span>
<span data-ttu-id="7d002-206">Ahora que ha implementado un servicio en contenedor, consulte [Ciclo de vida de la aplicación de Service Fabric](service-fabric-application-lifecycle.md) para saber cómo administrar su ciclo de vida.</span><span class="sxs-lookup"><span data-stu-id="7d002-206">Now that you have deployed a containerized service, learn how to manage its lifecycle by reading [Service Fabric application lifecycle](service-fabric-application-lifecycle.md).</span></span>

* [<span data-ttu-id="7d002-207">Información general: Service Fabric y contenedores</span><span class="sxs-lookup"><span data-stu-id="7d002-207">Overview of Service Fabric and containers</span></span>](service-fabric-containers-overview.md)
* [<span data-ttu-id="7d002-208">Interactuación con los clústeres de Service Fabric mediante la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="7d002-208">Interacting with Service Fabric clusters using the Azure CLI</span></span>](service-fabric-azure-cli.md)

<!-- Images -->
[sf-yeoman]: ./media/service-fabric-deploy-container-linux/sf-container-yeoman1.png

## <a name="related-articles"></a><span data-ttu-id="7d002-209">Artículos relacionados</span><span class="sxs-lookup"><span data-stu-id="7d002-209">Related articles</span></span>

* <span data-ttu-id="7d002-210">[Getting started with Service Fabric and Azure CLI 2.0](service-fabric-azure-cli-2-0.md) (Introducción a Service Fabric y la CLI de Azure 2.0)</span><span class="sxs-lookup"><span data-stu-id="7d002-210">[Getting started with Service Fabric and Azure CLI 2.0](service-fabric-azure-cli-2-0.md)</span></span>
* <span data-ttu-id="7d002-211">[Getting started with Service Fabric XPlat CLI](service-fabric-azure-cli.md) (Introducción a la CLI de XPlat de Service Fabric)</span><span class="sxs-lookup"><span data-stu-id="7d002-211">[Getting started with Service Fabric XPlat CLI](service-fabric-azure-cli.md)</span></span>
