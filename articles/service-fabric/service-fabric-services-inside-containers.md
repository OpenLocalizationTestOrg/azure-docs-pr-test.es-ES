---
title: "aaaHow toocontainerize su microservicios Azure Service Fabric (versión preliminar)"
description: "Azure Service Fabric ha agregado nuevos toocontainerize funcionalidad su microservicios Service Fabric. Esta funcionalidad actualmente está en su versión preliminar."
services: service-fabric
documentationcenter: .net
author: anmolah
manager: anmolah
editor: anmolah
ms.assetid: 0b41efb3-4063-4600-89f5-b077ea81fa3a
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/04/2017
ms.author: anmola
ms.openlocfilehash: 6edaff73c0828707c7fa736669ba8084663d31ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocontainerize-your-service-fabric-reliable-services-and-reliable-actors-preview"></a><span data-ttu-id="e2c7d-104">¿Cómo toocontainerize la confianza de tejido de servicio de servicios y Reliable Actors (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="e2c7d-104">How toocontainerize your Service Fabric Reliable Services and Reliable Actors (Preview)</span></span>

<span data-ttu-id="e2c7d-105">Service Fabric admite la inclusión de microservicios de Service Fabric en contenedores (servicios basados en Reliable Services y Reliable Actors).</span><span class="sxs-lookup"><span data-stu-id="e2c7d-105">Service Fabric supports containerizing Service Fabric microservices (Reliable Services, and Reliable Actor based services).</span></span> <span data-ttu-id="e2c7d-106">Para más información, consulte [Service Fabric y los contenedores](service-fabric-containers-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e2c7d-106">For more information, see [service fabric containers](service-fabric-containers-overview.md).</span></span>


 <span data-ttu-id="e2c7d-107">Esta característica está en versión preliminar y este artículo proporciona Hola tooget de varios pasos en el servicio que se ejecuta dentro de un contenedor.</span><span class="sxs-lookup"><span data-stu-id="e2c7d-107">This feature is in preview and this article provides hello various steps tooget your service running inside a container.</span></span>  

> [!NOTE]
> <span data-ttu-id="e2c7d-108">Esta característica se encuentra en versión preliminar y no se admite en producción.</span><span class="sxs-lookup"><span data-stu-id="e2c7d-108">This feature is in preview and is not supported in production.</span></span> <span data-ttu-id="e2c7d-109">Actualmente, esta característica solo funciona para Windows.</span><span class="sxs-lookup"><span data-stu-id="e2c7d-109">Currently this feature only works for Windows.</span></span>

## <a name="steps-toocontainerize-your-service-fabric-application"></a><span data-ttu-id="e2c7d-110">Los pasos toocontainerize su aplicación de servicio de Fabric</span><span class="sxs-lookup"><span data-stu-id="e2c7d-110">Steps toocontainerize your Service Fabric Application</span></span>

1. <span data-ttu-id="e2c7d-111">Abra la aplicación de Service Fabric en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e2c7d-111">Open your Service Fabric application in Visual Studio.</span></span>

2. <span data-ttu-id="e2c7d-112">Agregar clase [SFBinaryLoader.cs](https://github.com/Azure/service-fabric-scripts-and-templates/blob/master/code/SFBinaryLoaderForContainers/SFBinaryLoader.cs) tooyour proyecto.</span><span class="sxs-lookup"><span data-stu-id="e2c7d-112">Add class [SFBinaryLoader.cs](https://github.com/Azure/service-fabric-scripts-and-templates/blob/master/code/SFBinaryLoaderForContainers/SFBinaryLoader.cs) tooyour project.</span></span> <span data-ttu-id="e2c7d-113">código de Hello de esta clase es una aplicación auxiliar toocorrectly carga Hola Service Fabric en tiempo de ejecución los archivos binarios dentro de una aplicación cuando se ejecuta dentro de un contenedor.</span><span class="sxs-lookup"><span data-stu-id="e2c7d-113">hello code in this class is a helper toocorrectly load hello Service Fabric runtime binaries inside your application when running inside a container.</span></span>

3. <span data-ttu-id="e2c7d-114">Para cada paquete de código le gustaría toocontainerize, initialize Hola cargador en el punto de entrada del programa Hola.</span><span class="sxs-lookup"><span data-stu-id="e2c7d-114">For each code package you would like toocontainerize, initialize hello loader at hello program entry point.</span></span> <span data-ttu-id="e2c7d-115">Agregue el constructor estático de Hola que se muestra en el siguiente archivo de punto de entrada de programa tooyour de fragmentos de código de hello.</span><span class="sxs-lookup"><span data-stu-id="e2c7d-115">Add hello static constructor shown in hello following code snippet tooyour program entry point file.</span></span>

  ```csharp
  namespace MyApplication
  {
      internal static class Program
      {
          static Program()
          {
              SFBinaryLoader.Initialize();
          }

          /// <summary>
          /// This is hello entry point of hello service host process.
          /// </summary>
          private static void Main()
          {
  ```

4. <span data-ttu-id="e2c7d-116">Compile y [empaquete](service-fabric-package-apps.md#Package-App) el proyecto.</span><span class="sxs-lookup"><span data-stu-id="e2c7d-116">Build and [package](service-fabric-package-apps.md#Package-App) your project.</span></span> <span data-ttu-id="e2c7d-117">toobuild y crear un paquete, haga clic en proyecto de aplicación de hello en el Explorador de soluciones y elija hello **paquete** comando.</span><span class="sxs-lookup"><span data-stu-id="e2c7d-117">toobuild and create a package, right-click hello application project in Solution Explorer and choose hello **Package** command.</span></span>

5. <span data-ttu-id="e2c7d-118">Para cada paquete de código debe toocontainerize, ejecución Hola script de PowerShell [CreateDockerPackage.ps1](https://github.com/Azure/service-fabric-scripts-and-templates/blob/master/scripts/CodePackageToDockerPackage/CreateDockerPackage.ps1).</span><span class="sxs-lookup"><span data-stu-id="e2c7d-118">For every code package you need toocontainerize, run hello PowerShell script [CreateDockerPackage.ps1](https://github.com/Azure/service-fabric-scripts-and-templates/blob/master/scripts/CodePackageToDockerPackage/CreateDockerPackage.ps1).</span></span> <span data-ttu-id="e2c7d-119">uso de Hello es como sigue:</span><span class="sxs-lookup"><span data-stu-id="e2c7d-119">hello usage is as follows:</span></span>
  ```powershell
    $codePackagePath = 'Path toohello code package toocontainerize.'
    $dockerPackageOutputDirectoryPath = 'Output path for hello generated docker folder.'
    $applicationExeName = 'Name of hello ode package executable.'
    CreateDockerPackage.ps1 -CodePackageDirectoryPath $codePackagePath -DockerPackageOutputDirectoryPath $dockerPackageOutputDirectoryPath -ApplicationExeName $applicationExeName
 ```
  <span data-ttu-id="e2c7d-120">script de Hola crea una carpeta con los artefactos de Docker en $dockerPackageOutputDirectoryPath.</span><span class="sxs-lookup"><span data-stu-id="e2c7d-120">hello script creates a folder with Docker artifacts at $dockerPackageOutputDirectoryPath.</span></span> <span data-ttu-id="e2c7d-121">Modificar Hola genera Dockerfile tooexpose los puertos, ejecutar scripts de configuración etc. según sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="e2c7d-121">Modify hello generated Dockerfile tooexpose any ports, run setup scripts etc. based on your needs.</span></span>

6. <span data-ttu-id="e2c7d-122">A continuación hay demasiado[generar](service-fabric-get-started-containers.md#Build-Containers) y [inserción](service-fabric-get-started-containers.md#Push-Containers) el repositorio de tooyour del paquete de contenedor de Docker.</span><span class="sxs-lookup"><span data-stu-id="e2c7d-122">Next you need too[build](service-fabric-get-started-containers.md#Build-Containers) and [push](service-fabric-get-started-containers.md#Push-Containers) your Docker container package tooyour repository.</span></span>

7. <span data-ttu-id="e2c7d-123">Modificar hello ApplicationManifest.xml y ServiceManifest.xml tooadd su imagen de contenedor, información del repositorio, la autenticación del registro y asignación de puerto al host.</span><span class="sxs-lookup"><span data-stu-id="e2c7d-123">Modify hello ApplicationManifest.xml and ServiceManifest.xml tooadd your container image, repository information, registry authentication, and port-to-host mapping.</span></span> <span data-ttu-id="e2c7d-124">Para modificar los manifiestos de hello, consulte [crear una aplicación de contenedor de Azure Service Fabric](service-fabric-get-started-containers.md).</span><span class="sxs-lookup"><span data-stu-id="e2c7d-124">For modifying hello manifests, see [Create an Azure Service Fabric container application](service-fabric-get-started-containers.md).</span></span> <span data-ttu-id="e2c7d-125">definición de paquete de código de Hello en hello servicio necesidades manifiesto toobe reemplazado por la imagen de contenedor correspondiente.</span><span class="sxs-lookup"><span data-stu-id="e2c7d-125">hello code package definition in hello service manifest needs toobe replaced with corresponding container image.</span></span> <span data-ttu-id="e2c7d-126">Asegúrese de que toochange Hola EntryPoint tooa ContainerHost tipo.</span><span class="sxs-lookup"><span data-stu-id="e2c7d-126">Make sure toochange hello EntryPoint tooa ContainerHost type.</span></span>

  ```xml
<!-- Code package is your service executable. -->
<CodePackage Name="Code" Version="1.0.0">
  <EntryPoint>
    <!-- Follow this link for more information about deploying Windows containers tooService Fabric: https://aka.ms/sfguestcontainers -->
    <ContainerHost>
      <ImageName>myregistry.azurecr.io/samples/helloworldapp</ImageName>
    </ContainerHost>
  </EntryPoint>
  <!-- Pass environment variables tooyour container: -->    
</CodePackage>
  ```

8. <span data-ttu-id="e2c7d-127">Agregar asignación de puerto para alojar hello para el replicador y el extremo de servicio.</span><span class="sxs-lookup"><span data-stu-id="e2c7d-127">Add hello port-to-host mapping for your replicator and service endpoint.</span></span> <span data-ttu-id="e2c7d-128">Puesto que ambas estos puertos se asignan en tiempo de ejecución por Service Fabric, hello ContainerPort se establece toozero toouse Hola le asignada el puerto para la asignación.</span><span class="sxs-lookup"><span data-stu-id="e2c7d-128">Since both these ports are assigned at runtime by Service Fabric, hello ContainerPort is set toozero toouse hello assigned port for mapping.</span></span>

 ```xml
<Policies>
  <ContainerHostPolicies CodePackageRef="Code">
    <PortBinding ContainerPort="0" EndpointRef="ServiceEndpoint"/>
    <PortBinding ContainerPort="0" EndpointRef="ReplicatorEndpoint"/>
  </ContainerHostPolicies>
</Policies>
 ```

9. <span data-ttu-id="e2c7d-129">tootest esta aplicación, necesita toodeploy se tooa clúster que se está ejecutando la versión 5.7 o posterior.</span><span class="sxs-lookup"><span data-stu-id="e2c7d-129">tootest this application, you need toodeploy it tooa cluster that is running version 5.7 or higher.</span></span> <span data-ttu-id="e2c7d-130">Además, se necesita tooedit y actualiza tooenable de configuración de clúster de hello esta característica de vista previa.</span><span class="sxs-lookup"><span data-stu-id="e2c7d-130">In addition, you need tooedit and update hello cluster settings tooenable this preview feature.</span></span> <span data-ttu-id="e2c7d-131">Siga los pasos de hello en este [artículo](service-fabric-cluster-fabric-settings.md) configuración de hello tooadd aprecia aquí.</span><span class="sxs-lookup"><span data-stu-id="e2c7d-131">Follow hello steps in this [article](service-fabric-cluster-fabric-settings.md) tooadd hello setting shown next.</span></span>
```
      {
        "name": "Hosting",
        "parameters": [
          {
            "name": "FabricContainerAppsEnabled",
            "value": "true"
          }
        ]
      }
```
10. <span data-ttu-id="e2c7d-132">Siguiente [implementar](service-fabric-deploy-remove-applications.md) Hola editar clúster de toothis del paquete de aplicación.</span><span class="sxs-lookup"><span data-stu-id="e2c7d-132">Next [deploy](service-fabric-deploy-remove-applications.md) hello edited application package toothis cluster.</span></span>

<span data-ttu-id="e2c7d-133">Ahora debería tener una aplicación de Service Fabric en contenedores ejecutando el clúster.</span><span class="sxs-lookup"><span data-stu-id="e2c7d-133">You should now have a containerized Service Fabric application running your cluster.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e2c7d-134">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e2c7d-134">Next steps</span></span>
* <span data-ttu-id="e2c7d-135">Más información acerca de cómo ejecutar [contenedores en Service Fabric](service-fabric-get-started-containers.md).</span><span class="sxs-lookup"><span data-stu-id="e2c7d-135">Learn more about running [containers on Service Fabric](service-fabric-get-started-containers.md).</span></span>
* <span data-ttu-id="e2c7d-136">Obtenga información acerca de Service Fabric hello [ciclo de vida de la aplicación](service-fabric-application-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="e2c7d-136">Learn about hello Service Fabric [application life-cycle](service-fabric-application-lifecycle.md).</span></span>
