---
title: "Service Fabric e implementación de contenedores | Microsoft Docs"
description: "Service Fabric y el uso de contenedores para implementar aplicaciones de microservicios. En este artículo se describen las funcionalidades que ofrece Service Fabric para los contenedores y cómo implementar una imagen de contenedor de Windows en un clúster."
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
ms.openlocfilehash: 25d6b056421e71fa70ed20a39589f77dbbc25c69
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-a-windows-container-to-service-fabric"></a><span data-ttu-id="c9d88-104">Implementación de un contenedor de Windows en Service Fabric</span><span class="sxs-lookup"><span data-stu-id="c9d88-104">Deploy a Windows container to Service Fabric</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c9d88-105">Implementación de un contenedor de Windows</span><span class="sxs-lookup"><span data-stu-id="c9d88-105">Deploy Windows Container</span></span>](service-fabric-deploy-container.md)
> * [<span data-ttu-id="c9d88-106">Implementación de un contenedor de Docker</span><span class="sxs-lookup"><span data-stu-id="c9d88-106">Deploy Docker Container</span></span>](service-fabric-deploy-container-linux.md)
> 
> 

<span data-ttu-id="c9d88-107">Este artículo le guiará a través del proceso de creación de servicios de contenedor en contenedores de Windows.</span><span class="sxs-lookup"><span data-stu-id="c9d88-107">This article walks you through the process of building containerized services in Windows containers.</span></span>

<span data-ttu-id="c9d88-108">Service Fabric tiene varias funcionalidades que le ayudarán a crear aplicaciones compuestas de microservicios que se ejecutan en contenedores.</span><span class="sxs-lookup"><span data-stu-id="c9d88-108">Service Fabric has several capabilities that help you with building applications that are composed of microservices running inside containers.</span></span> 

<span data-ttu-id="c9d88-109">Entre estas funcionalidades, cabe destacar:</span><span class="sxs-lookup"><span data-stu-id="c9d88-109">The capabilities include:</span></span>

* <span data-ttu-id="c9d88-110">Activación e implementación de la imagen de contenedor</span><span class="sxs-lookup"><span data-stu-id="c9d88-110">Container image deployment and activation</span></span>
* <span data-ttu-id="c9d88-111">Regulador de recursos</span><span class="sxs-lookup"><span data-stu-id="c9d88-111">Resource governance</span></span>
* <span data-ttu-id="c9d88-112">Autenticación de repositorio</span><span class="sxs-lookup"><span data-stu-id="c9d88-112">Repository authentication</span></span>
* <span data-ttu-id="c9d88-113">Asignación de puerto a host de contenedor</span><span class="sxs-lookup"><span data-stu-id="c9d88-113">Container port-to-host port mapping</span></span>
* <span data-ttu-id="c9d88-114">Detección y comunicación entre contenedores</span><span class="sxs-lookup"><span data-stu-id="c9d88-114">Container-to-container discovery and communication</span></span>
* <span data-ttu-id="c9d88-115">Capacidad de configurar y establecer variables de entorno</span><span class="sxs-lookup"><span data-stu-id="c9d88-115">Ability to configure and set environment variables</span></span>

<span data-ttu-id="c9d88-116">Echemos un vistazo a cada una de las funcionalidades al empaquetar un servicio en contenedor que desea incluir en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c9d88-116">Let's look at how each of capabilities works when you're packaging a containerized service to be included in your application.</span></span>

## <a name="package-a-windows-container"></a><span data-ttu-id="c9d88-117">Empaquetado de un contenedor de Windows</span><span class="sxs-lookup"><span data-stu-id="c9d88-117">Package a Windows container</span></span>
<span data-ttu-id="c9d88-118">Al empaquetar un contenedor, puede usar una plantilla de proyecto de Visual Studio o [crear el paquete de aplicación manualmente](#manually).</span><span class="sxs-lookup"><span data-stu-id="c9d88-118">When you package a container, you can choose to use either a Visual Studio project template or [create the application package manually](#manually).</span></span>  <span data-ttu-id="c9d88-119">Con Visual Studio, la estructura del paquete de aplicación y los archivos de manifiesto se crean mediante la plantilla para nuevos proyectos.</span><span class="sxs-lookup"><span data-stu-id="c9d88-119">When you use Visual Studio, the application package structure and manifest files are created by the New Project template for you.</span></span>

> [!TIP]
> <span data-ttu-id="c9d88-120">La forma más sencilla de empaquetar una imagen de contenedor en un servicio es mediante Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c9d88-120">The easiest way to package an existing container image into a service is to use Visual Studio.</span></span>

## <a name="use-visual-studio-to-package-an-existing-container-image"></a><span data-ttu-id="c9d88-121">Uso de Visual Studio para empaquetar una imagen de contenedor existente</span><span class="sxs-lookup"><span data-stu-id="c9d88-121">Use Visual Studio to package an existing container image</span></span>
<span data-ttu-id="c9d88-122">Visual Studio proporciona una plantilla de servicio de Service Fabric para ayudarle a implementar un contenedor en un clúster de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="c9d88-122">Visual Studio provides a Service Fabric service template to help you deploy a container to a Service Fabric cluster.</span></span>

1. <span data-ttu-id="c9d88-123">Seleccione **Archivo** > **Nuevo proyecto** y cree una aplicación de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="c9d88-123">Choose **File** > **New Project**, and create a Service Fabric application.</span></span>
2. <span data-ttu-id="c9d88-124">Elija **Contenedor invitado** como la plantilla de servicio.</span><span class="sxs-lookup"><span data-stu-id="c9d88-124">Choose **Guest Container** as the service template.</span></span>
3. <span data-ttu-id="c9d88-125">Elija el **Nombre de imagen** y proporcione la ruta de acceso a la imagen en el repositorio de contenedores.</span><span class="sxs-lookup"><span data-stu-id="c9d88-125">Choose **Image Name** and provide the path to the image in your container repository.</span></span> <span data-ttu-id="c9d88-126">Por ejemplo, `myrepo/myimage:v1` en https://hub.docker.com</span><span class="sxs-lookup"><span data-stu-id="c9d88-126">For example, `myrepo/myimage:v1` in https://hub.docker.com</span></span>
4. <span data-ttu-id="c9d88-127">Asigne un nombre a su servicio y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="c9d88-127">Give your service a name, and click **OK**.</span></span>
5. <span data-ttu-id="c9d88-128">Si el servicio en contenedores necesita un punto de conexión para establecer comunicación, ahora podrá agregar el protocolo, el puerto y el tipo al archivo ServiceManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="c9d88-128">If your containerized service needs an endpoint for communication, you can now add the protocol, port, and type to the ServiceManifest.xml file.</span></span> <span data-ttu-id="c9d88-129">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="c9d88-129">For example:</span></span> 
     
    `<Endpoint Name="MyContainerServiceEndpoint" Protocol="http" Port="80" UriScheme="http" PathSuffix="myapp/" Type="Input" />`
    
    <span data-ttu-id="c9d88-130">Si se especifica `UriScheme`, Service Fabric registra automáticamente el punto de conexión del contenedor con el servicio de nombres de Service Fabric para facilitar la detección.</span><span class="sxs-lookup"><span data-stu-id="c9d88-130">By providing the `UriScheme`, Service Fabric automatically registers the container endpoint with the Naming service for discoverability.</span></span> <span data-ttu-id="c9d88-131">El puerto puede fijarse (como se muestra en el ejemplo anterior) o asignarse dinámicamente.</span><span class="sxs-lookup"><span data-stu-id="c9d88-131">The port can either be fixed (as shown in the preceding example) or dynamically allocated.</span></span> <span data-ttu-id="c9d88-132">Si no se especifica un puerto, se asigna dinámicamente desde el intervalo de puertos de la aplicación (como ocurre con cualquier otro servicio).</span><span class="sxs-lookup"><span data-stu-id="c9d88-132">If you don't specify a port, it is dynamically allocated from the application port range (as would happen with any service).</span></span>
    <span data-ttu-id="c9d88-133">También puede configurar la asignación de puerto a host del contenedor si especifica una directiva `PortBinding` en el manifiesto de aplicación.</span><span class="sxs-lookup"><span data-stu-id="c9d88-133">You also need to configure the container to host port mapping by specifying a `PortBinding` policy in the application manifest.</span></span> <span data-ttu-id="c9d88-134">Para más información, consulte [Configuración de la asignación de puerto a host del contenedor](#Portsection).</span><span class="sxs-lookup"><span data-stu-id="c9d88-134">For more information, see [Configure container to host port mapping](#Portsection).</span></span>
6. <span data-ttu-id="c9d88-135">Si el contenedor necesita la regulación de los recursos, agregue una directiva `ResourceGovernancePolicy`.</span><span class="sxs-lookup"><span data-stu-id="c9d88-135">If your container needs resource governance then add a `ResourceGovernancePolicy`.</span></span>
8. <span data-ttu-id="c9d88-136">Si el contenedor necesita autenticarse con un repositorio privado, agregue `RepositoryCredentials`.</span><span class="sxs-lookup"><span data-stu-id="c9d88-136">If your container needs to authenticate with a private repository, then add `RepositoryCredentials`.</span></span>
7. <span data-ttu-id="c9d88-137">Si utiliza una máquina con Windows Server 2016 compatible con el contenedor habilitado, puede usar la acción de empaquetar y publicar para la implementación del clúster local.</span><span class="sxs-lookup"><span data-stu-id="c9d88-137">If you are running on a Windows Server 2016 machine with container support enabled, you can use the package and publish action to deploy to your local cluster.</span></span> 
8. <span data-ttu-id="c9d88-138">Cuando esté listo puede publicar la aplicación en un clúster remoto o comprobar la solución en el control de código fuente.</span><span class="sxs-lookup"><span data-stu-id="c9d88-138">When ready, you can publish the application to a remote cluster or check in the solution to source control.</span></span> 

<span data-ttu-id="c9d88-139">Para un ejemplo, consulte los [ejemplos de código de contenedor de Service Fabric en GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers).</span><span class="sxs-lookup"><span data-stu-id="c9d88-139">For an example, checkout the [Service Fabric container code samples on GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)</span></span>

## <a name="creating-a-windows-server-2016-cluster"></a><span data-ttu-id="c9d88-140">Creación de un clúster de Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="c9d88-140">Creating a Windows Server 2016 cluster</span></span>
<span data-ttu-id="c9d88-141">Para implementar la aplicación en contenedores, debe crear un clúster que ejecute Windows Server 2016 con la compatibilidad con contenedores habilitada.</span><span class="sxs-lookup"><span data-stu-id="c9d88-141">To deploy your containerized application, you need to create a cluster running Windows Server 2016 with container support enabled.</span></span> <span data-ttu-id="c9d88-142">El clúster puede ejecutarse localmente o implementarse en Azure mediante Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c9d88-142">Your cluster may be running locally, or deployed via Azure Resource Manager in Azure.</span></span> 

<span data-ttu-id="c9d88-143">Para implementar un clúster con Azure Resource Manager, elija la opción de imagen **Windows Server 2016 with Containers** (Windows Server 2016 con contenedores) en Azure.</span><span class="sxs-lookup"><span data-stu-id="c9d88-143">To deploy a cluster using Azure Resource Manager, choose the **Windows Server 2016 with Containers** image option in Azure.</span></span> <span data-ttu-id="c9d88-144">Vea el artículo [Creación de un clúster de Service Fabric con Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).</span><span class="sxs-lookup"><span data-stu-id="c9d88-144">See the article [Create a Service Fabric cluster by using Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).</span></span> <span data-ttu-id="c9d88-145">Asegúrese de usar la configuración de Azure Resource Manager siguiente:</span><span class="sxs-lookup"><span data-stu-id="c9d88-145">Ensure that you use the following Azure Resource Manager settings:</span></span>

```xml
"vmImageOffer": { "type": "string","defaultValue": "WindowsServer"     },
"vmImageSku": { "defaultValue": "2016-Datacenter-with-Containers","type": "string"     },
"vmImageVersion": { "defaultValue": "latest","type": "string"     },  
```
<span data-ttu-id="c9d88-146">También puede usar la [plantilla de cinco nodos de Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype) para crear un clúster.</span><span class="sxs-lookup"><span data-stu-id="c9d88-146">You can also use the [Five Node Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype) to create a cluster.</span></span> <span data-ttu-id="c9d88-147">Como alternativa, lea una [entrada de blog](https://loekd.blogspot.com/2017/01/running-windows-containers-on-azure.html) de la comunidad sobre el uso de Service Fabric y los contenedores de Windows.</span><span class="sxs-lookup"><span data-stu-id="c9d88-147">Alternatively read a community [blog post](https://loekd.blogspot.com/2017/01/running-windows-containers-on-azure.html) on using Service Fabric and Windows containers.</span></span>

<a id="manually"></a>

## <a name="manually-package-and-deploy-a-container-image"></a><span data-ttu-id="c9d88-148">Empaquetado e implementación manual de una imagen de contenedor</span><span class="sxs-lookup"><span data-stu-id="c9d88-148">Manually package and deploy a container image</span></span>
<span data-ttu-id="c9d88-149">El proceso de empaquetado manual de un servicio en contenedor se basa en los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="c9d88-149">The process of manually packaging a containerized service is based on the following steps:</span></span>

1. <span data-ttu-id="c9d88-150">Publicar los contenedores en el repositorio.</span><span class="sxs-lookup"><span data-stu-id="c9d88-150">Publish the containers to your repository.</span></span>
2. <span data-ttu-id="c9d88-151">Crear la estructura de directorios del paquete.</span><span class="sxs-lookup"><span data-stu-id="c9d88-151">Create the package directory structure.</span></span>
3. <span data-ttu-id="c9d88-152">Editar el archivo de manifiesto de servicio.</span><span class="sxs-lookup"><span data-stu-id="c9d88-152">Edit the service manifest file.</span></span>
4. <span data-ttu-id="c9d88-153">Editar el archivo de manifiesto de aplicación.</span><span class="sxs-lookup"><span data-stu-id="c9d88-153">Edit the application manifest file.</span></span>

## <a name="deploy-and-activate-a-container-image"></a><span data-ttu-id="c9d88-154">Implementación y activación de una imagen de contenedor</span><span class="sxs-lookup"><span data-stu-id="c9d88-154">Deploy and activate a container image</span></span>
<span data-ttu-id="c9d88-155">En el [modelo de aplicación](service-fabric-application-model.md)de Service Fabric, un contenedor representa un host de la aplicación en el que se colocan varias réplicas de servicio.</span><span class="sxs-lookup"><span data-stu-id="c9d88-155">In the Service Fabric [application model](service-fabric-application-model.md), a container represents an application host in which multiple service replicas are placed.</span></span> <span data-ttu-id="c9d88-156">Para implementar y activar un contenedor, ponga el nombre de la imagen de contenedor en un elemento `ContainerHost` en el manifiesto de servicio.</span><span class="sxs-lookup"><span data-stu-id="c9d88-156">To deploy and activate a container, put the name of the container image into a `ContainerHost` element in the service manifest.</span></span>

<span data-ttu-id="c9d88-157">En el manifiesto de servicio, añada un elemento `ContainerHost` para el punto de entrada.</span><span class="sxs-lookup"><span data-stu-id="c9d88-157">In the service manifest, add a `ContainerHost` for the entry point.</span></span> <span data-ttu-id="c9d88-158">A continuación, establezca el elemento `ImageName` como nombre de la imagen y el repositorio del contenedor.</span><span class="sxs-lookup"><span data-stu-id="c9d88-158">Then set the `ImageName` to be the name of the container repository and image.</span></span> <span data-ttu-id="c9d88-159">El siguiente manifiesto parcial muestra un ejemplo de cómo implementar el contenedor llamado `myimage:v1` desde un repositorio denominado `myrepo`:</span><span class="sxs-lookup"><span data-stu-id="c9d88-159">The following partial manifest shows an example of how to deploy the container called `myimage:v1` from a repository called `myrepo`:</span></span>

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

<span data-ttu-id="c9d88-160">Puede especificar comandos opcionales para que se ejecuten al iniciar el contenedor en el elemento `Commands`.</span><span class="sxs-lookup"><span data-stu-id="c9d88-160">You can specify optional commands to run upon starting the container under the `Commands` element.</span></span> <span data-ttu-id="c9d88-161">Separe los distintos comandos con comas.</span><span class="sxs-lookup"><span data-stu-id="c9d88-161">For multiple commands, comma-delimit them.</span></span> 

## <a name="understand-resource-governance"></a><span data-ttu-id="c9d88-162">Descripción de la regulación de recursos</span><span class="sxs-lookup"><span data-stu-id="c9d88-162">Understand resource governance</span></span>
<span data-ttu-id="c9d88-163">La regulación de recursos es una funcionalidad del contenedor que permite restringir los recursos que puede usar el contenedor en el host.</span><span class="sxs-lookup"><span data-stu-id="c9d88-163">Resource governance is a capability of the container that restricts the resources that the container can use on the host.</span></span> <span data-ttu-id="c9d88-164">El elemento `ResourceGovernancePolicy`, especificado en el manifiesto de la aplicación, se utiliza para declarar los límites de recursos para un paquete de código de servicio.</span><span class="sxs-lookup"><span data-stu-id="c9d88-164">The `ResourceGovernancePolicy`, which is specified in the application manifest is used to declare resource limits for a service code package.</span></span> <span data-ttu-id="c9d88-165">Es posible establecer límites para los siguientes recursos:</span><span class="sxs-lookup"><span data-stu-id="c9d88-165">Resource limits can be set for the following resources:</span></span>

* <span data-ttu-id="c9d88-166">Memoria</span><span class="sxs-lookup"><span data-stu-id="c9d88-166">Memory</span></span>
* <span data-ttu-id="c9d88-167">MemorySwap</span><span class="sxs-lookup"><span data-stu-id="c9d88-167">MemorySwap</span></span>
* <span data-ttu-id="c9d88-168">CpuShares (peso relativo de CPU)</span><span class="sxs-lookup"><span data-stu-id="c9d88-168">CpuShares (CPU relative weight)</span></span>
* <span data-ttu-id="c9d88-169">MemoryReservationInMB</span><span class="sxs-lookup"><span data-stu-id="c9d88-169">MemoryReservationInMB</span></span>  
* <span data-ttu-id="c9d88-170">BlkioWeight (peso relativo de BlockIO).</span><span class="sxs-lookup"><span data-stu-id="c9d88-170">BlkioWeight (BlockIO relative weight).</span></span>

> [!NOTE]
> <span data-ttu-id="c9d88-171">Para una versión futura se ha planeado la compatibilidad para especificar límites de E/S de bloques como IOP, BPS de lectura/escritura y mucho más.</span><span class="sxs-lookup"><span data-stu-id="c9d88-171">Support for specifying specific block IO limits such as IOPs, read/write BPS, and others are planned for a future release.</span></span>
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

## <a name="authenticate-a-repository"></a><span data-ttu-id="c9d88-172">Autenticación de un repositorio</span><span class="sxs-lookup"><span data-stu-id="c9d88-172">Authenticate a repository</span></span>
<span data-ttu-id="c9d88-173">Para descargar un contenedor, puede que tenga que proporcionar credenciales de inicio de sesión para el repositorio de contenedor.</span><span class="sxs-lookup"><span data-stu-id="c9d88-173">To download a container, you might have to provide sign-in credentials to the container repository.</span></span> <span data-ttu-id="c9d88-174">Las credenciales de inicio de sesión incluidas en el manifiesto de la aplicación se usan para especificar la información de inicio de sesión, o clave SSH, para descargar la imagen del contenedor desde el repositorio de imágenes.</span><span class="sxs-lookup"><span data-stu-id="c9d88-174">The sign-in credentials, specified in the application manifest, are used to specify the sign-in information, or SSH key, for downloading the container image from the image repository.</span></span> <span data-ttu-id="c9d88-175">En el ejemplo siguiente se muestra una cuenta llamada *TestUser* junto con la contraseña no cifrada (*no* recomendado):</span><span class="sxs-lookup"><span data-stu-id="c9d88-175">The following example shows an account called *TestUser* along with the password in clear text (*not* recommended):</span></span>

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

<span data-ttu-id="c9d88-176">Se recomienda cifrar la contraseña mediante un certificado implementado en la máquina.</span><span class="sxs-lookup"><span data-stu-id="c9d88-176">We recommend that you encrypt the password by using a certificate that's deployed to the machine.</span></span>

<span data-ttu-id="c9d88-177">El ejemplo siguiente muestra una cuenta denominada *TestUser* con la contraseña cifrada mediante un certificado llamado *MyCert*.</span><span class="sxs-lookup"><span data-stu-id="c9d88-177">The following example shows an account called *TestUser*, where the password was encrypted by using a certificate called *MyCert*.</span></span> <span data-ttu-id="c9d88-178">Puede usar el comando de PowerShell `Invoke-ServiceFabricEncryptText` para crear el texto cifrado secreto de la contraseña.</span><span class="sxs-lookup"><span data-stu-id="c9d88-178">You can use the `Invoke-ServiceFabricEncryptText` PowerShell command to create the secret cipher text for the password.</span></span> <span data-ttu-id="c9d88-179">Para más información, consulte el artículo [Administración de secretos en aplicaciones de Service Fabric](service-fabric-application-secret-management.md).</span><span class="sxs-lookup"><span data-stu-id="c9d88-179">For more information, see the article [Managing secrets in Service Fabric applications](service-fabric-application-secret-management.md).</span></span>

<span data-ttu-id="c9d88-180">La clave privada del certificado que se usa para descifrar la contraseña se debe implementar en la máquina local con un método fuera de banda</span><span class="sxs-lookup"><span data-stu-id="c9d88-180">The private key of the certificate that's used to decrypt the password must be deployed to the local machine in an out-of-band method.</span></span> <span data-ttu-id="c9d88-181">(en Azure esto se logra mediante Azure Resource Manager). Posteriormente, cuando Service Fabric implementa el paquete de servicio en la máquina, es capaz de descifrar el secreto.</span><span class="sxs-lookup"><span data-stu-id="c9d88-181">(In Azure, this method is Azure Resource Manager.) Then, when Service Fabric deploys the service package to the machine, it can decrypt the secret.</span></span> <span data-ttu-id="c9d88-182">Al usar el secreto junto con el nombre de cuenta, puede autenticarse con el repositorio de contenedor.</span><span class="sxs-lookup"><span data-stu-id="c9d88-182">By using the secret along with the account name, it can then authenticate with the container repository.</span></span>

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

## <span data-ttu-id="c9d88-183"><a name ="Portsection"></a> Configuración de la asignación de puerto a host del contenedor</span><span class="sxs-lookup"><span data-stu-id="c9d88-183"><a name ="Portsection"></a> Configure container to host port mapping</span></span>
<span data-ttu-id="c9d88-184">Puede configurar un puerto de host utilizado para comunicarse con el contenedor mediante la especificación de un elemento `PortBinding` en el manifiesto de aplicación.</span><span class="sxs-lookup"><span data-stu-id="c9d88-184">You can configure a host port used to communicate with the container by specifying a `PortBinding` in the application manifest.</span></span> <span data-ttu-id="c9d88-185">El enlace de puerto asigna el puerto que el servicio está escuchando dentro del contenedor a un puerto en el host.</span><span class="sxs-lookup"><span data-stu-id="c9d88-185">The port binding maps the port to which the service is listening inside the container to a port on the host.</span></span>

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

## <a name="configure-container-to-container-discovery-and-communication"></a><span data-ttu-id="c9d88-186">Configuración de detección y comunicación entre contenedores</span><span class="sxs-lookup"><span data-stu-id="c9d88-186">Configure container-to-container discovery and communication</span></span>
<span data-ttu-id="c9d88-187">Puede usar el elemento `PortBinding` para asignar un puerto del contenedor a un punto de conexión del manifiesto de servicio.</span><span class="sxs-lookup"><span data-stu-id="c9d88-187">You can use the `PortBinding` element to map a container port to an endpoint in the service manifest.</span></span> <span data-ttu-id="c9d88-188">En el ejemplo siguiente, el punto de conexión `Endpoint1` especifica un puerto fijo, 8905.</span><span class="sxs-lookup"><span data-stu-id="c9d88-188">In the following example, the endpoint `Endpoint1` specifies a fixed port, 8905.</span></span> <span data-ttu-id="c9d88-189">También puede no especificar ningún puerto, en cuyo caso se elegirá un puerto aleatorio del intervalo de puertos de la aplicación del clúster.</span><span class="sxs-lookup"><span data-stu-id="c9d88-189">It can also specify no port at all, in which case a random port from the cluster's application port range is chosen for you.</span></span>


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
<span data-ttu-id="c9d88-190">Si especifica un punto de conexión, al usar la etiqueta `Endpoint` en el manifiesto de servicio de un contenedor invitado, Service Fabric puede publicar automáticamente este punto de conexión en el servicio de nombres.</span><span class="sxs-lookup"><span data-stu-id="c9d88-190">If you specify an endpoint, using the `Endpoint` tag in the service manifest of a guest container, Service Fabric can automatically publish this endpoint to the Naming service.</span></span> <span data-ttu-id="c9d88-191">De este modo, otros servicios que se ejecutan en el clúster podrán detectar que este contenedor usa las consultas REST para la resolución.</span><span class="sxs-lookup"><span data-stu-id="c9d88-191">Other services that are running in the cluster can thus discover this container using the REST queries for resolving.</span></span>

<span data-ttu-id="c9d88-192">Al registrarse con el servicio de nombres, se puede establecer la comunicación de contenedor a contenedor dentro del contenedor mediante el [proxy inverso](service-fabric-reverseproxy.md).</span><span class="sxs-lookup"><span data-stu-id="c9d88-192">By registering with the Naming service, you can perform container-to-container communication within your container by using the [reverse proxy](service-fabric-reverseproxy.md).</span></span> <span data-ttu-id="c9d88-193">La comunicación se establece al proporcionar el puerto de escucha http de proxy inverso y el nombre de los servicios con los que desea comunicarse como variables de entorno.</span><span class="sxs-lookup"><span data-stu-id="c9d88-193">Communication is performed by providing the reverse proxy http listening port and the name of the services that you want to communicate with as environment variables.</span></span> <span data-ttu-id="c9d88-194">Para más información, consulte la siguiente sección.</span><span class="sxs-lookup"><span data-stu-id="c9d88-194">For more information, see the next section.</span></span> 

## <a name="configure-and-set-environment-variables"></a><span data-ttu-id="c9d88-195">Configuración y establecimiento de variables de entorno</span><span class="sxs-lookup"><span data-stu-id="c9d88-195">Configure and set environment variables</span></span>
<span data-ttu-id="c9d88-196">En el manifiesto de servicio, las variables de entorno se pueden especificar para cada paquete de código.</span><span class="sxs-lookup"><span data-stu-id="c9d88-196">Environment variables can be specified for each code package in the service manifest.</span></span> <span data-ttu-id="c9d88-197">Esta característica está disponible para todos los servicios, con independencia de si se implementan como contenedores, procesos o archivos ejecutables de invitado.</span><span class="sxs-lookup"><span data-stu-id="c9d88-197">This feature is available for all services irrespective of whether they are deployed as containers or processes or guest executables.</span></span> <span data-ttu-id="c9d88-198">Estos valores de variable de entorno se invalidan en el manifiesto de aplicación o se especifican durante la implementación como parámetros de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c9d88-198">You can override environment variable values in the application manifest or specify them during deployment as application parameters.</span></span>

<span data-ttu-id="c9d88-199">El siguiente fragmento de código XML del manifiesto de servicio muestra un ejemplo de cómo especificar variables de entorno para un paquete de código:</span><span class="sxs-lookup"><span data-stu-id="c9d88-199">The following service manifest XML snippet shows an example of how to specify environment variables for a code package:</span></span>

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

<span data-ttu-id="c9d88-200">Estas variables de entorno se pueden invalidar en el nivel del manifiesto de aplicación:</span><span class="sxs-lookup"><span data-stu-id="c9d88-200">These environment variables can be overridden at the application manifest level:</span></span>

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <EnvironmentOverrides CodePackageRef="FrontendService.Code">
            <EnvironmentVariable Name="BackendServiceName" Value="[BackendSvc]"/>
            <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
        </EnvironmentOverrides>
    </ServiceManifestImport>
```

<span data-ttu-id="c9d88-201">En el ejemplo anterior, se ha especificado un valor explícito para la variable de entorno `HttpGateway` (19000), mientras que el valor del parámetro `BackendServiceName` se ha establecido a través del parámetro de la aplicación `[BackendSvc]`.</span><span class="sxs-lookup"><span data-stu-id="c9d88-201">In the previous example, we specified an explicit value for the `HttpGateway` environment variable (19000), while we set the value for `BackendServiceName` parameter via the `[BackendSvc]` application parameter.</span></span> <span data-ttu-id="c9d88-202">Esta configuración permite especificar el valor de `BackendServiceName` al implementar la aplicación sin necesidad de tener un valor fijo en el manifiesto.</span><span class="sxs-lookup"><span data-stu-id="c9d88-202">These settings enable you to specify the value for `BackendServiceName`value when you deploy the application and not have a fixed value in the manifest.</span></span>

## <a name="configure-isolation-mode"></a><span data-ttu-id="c9d88-203">Configuración del modo de aislamiento</span><span class="sxs-lookup"><span data-stu-id="c9d88-203">Configure isolation mode</span></span>

<span data-ttu-id="c9d88-204">Windows admite dos modos de aislamiento para contenedores: de proceso y de Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="c9d88-204">Windows supports two isolation modes for containers - process and Hyper-V.</span></span>  <span data-ttu-id="c9d88-205">Con el modo de aislamiento de proceso, todos los contenedores que se ejecutan en la misma máquina host comparten el kernel con el host.</span><span class="sxs-lookup"><span data-stu-id="c9d88-205">With the process isolation mode, all the containers running on the same host machine share the kernel with the host.</span></span> <span data-ttu-id="c9d88-206">Con el modo de aislamiento de Hyper-V, los kernels se aíslan entre los contenedores de Hyper-V y el host del contenedor.</span><span class="sxs-lookup"><span data-stu-id="c9d88-206">With the Hyper-V isolation mode, the kernels are isolated between each Hyper-V container and the container host.</span></span> <span data-ttu-id="c9d88-207">El modo de aislamiento se especifica en la etiqueta `ContainerHostPolicies` del archivo de manifiesto de aplicación.</span><span class="sxs-lookup"><span data-stu-id="c9d88-207">The isolation mode is specified in the `ContainerHostPolicies` tag in the application manifest file.</span></span>  <span data-ttu-id="c9d88-208">Los modos de aislamiento que se pueden especificar son `process`, `hyperv` y `default`.</span><span class="sxs-lookup"><span data-stu-id="c9d88-208">The isolation modes that can be specified are `process`, `hyperv`, and `default`.</span></span> <span data-ttu-id="c9d88-209">`default` es `process` en los hosts de Windows Server y `hyperv` en los hosts de Windows 10 de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="c9d88-209">The `default` isolation mode defaults to `process` on Windows Server hosts, and defaults to `hyperv` on Windows 10 hosts.</span></span>  <span data-ttu-id="c9d88-210">El siguiente fragmento de código muestra cómo el modo de aislamiento se especifica en el archivo de manifiesto de aplicación.</span><span class="sxs-lookup"><span data-stu-id="c9d88-210">The following snippet shows how the isolation mode is specified in the application manifest file.</span></span>

```xml
   <ContainerHostPolicies CodePackageRef="NodeService.Code" Isolation="hyperv">
```


## <a name="complete-examples-for-application-and-service-manifest"></a><span data-ttu-id="c9d88-211">Ejemplos completos de manifiesto de servicio y de aplicación</span><span class="sxs-lookup"><span data-stu-id="c9d88-211">Complete examples for application and service manifest</span></span>

<span data-ttu-id="c9d88-212">Este es un ejemplo de un manifiesto de aplicación:</span><span class="sxs-lookup"><span data-stu-id="c9d88-212">An example application manifest follows:</span></span>

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

<span data-ttu-id="c9d88-213">Este es un ejemplo de manifiesto de servicio (especificado en el manifiesto de aplicación anterior):</span><span class="sxs-lookup"><span data-stu-id="c9d88-213">An example service manifest (specified in the preceding application manifest) follows:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="c9d88-214">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c9d88-214">Next steps</span></span>
<span data-ttu-id="c9d88-215">Ahora que ha implementado un servicio en contenedor, consulte [Ciclo de vida de la aplicación de Service Fabric](service-fabric-application-lifecycle.md) para saber cómo administrar su ciclo de vida.</span><span class="sxs-lookup"><span data-stu-id="c9d88-215">Now that you have deployed a containerized service, learn how to manage its lifecycle by reading [Service Fabric application lifecycle](service-fabric-application-lifecycle.md).</span></span>

* [<span data-ttu-id="c9d88-216">Información general: Service Fabric y contenedores</span><span class="sxs-lookup"><span data-stu-id="c9d88-216">Overview of Service Fabric and containers</span></span>](service-fabric-containers-overview.md)
* <span data-ttu-id="c9d88-217">Para un ejemplo, consulte los [ejemplos de código de contenedor de Service Fabric en GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)</span><span class="sxs-lookup"><span data-stu-id="c9d88-217">For an example, checkout [Service Fabric container code samples on GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)</span></span>
