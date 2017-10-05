---
title: "Inclusión de los microservicios de Azure Service Fabric en contenedores (versión preliminar)"
description: "Azure Service Fabric ha agregado una nueva funcionalidad para incluir los microservicios de Service Fabric en contenedores. Esta funcionalidad actualmente está en su versión preliminar."
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
ms.openlocfilehash: 6f8ad0bad8d1ae861e6b72f7e1a32ab0675813c2
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-containerize-your-service-fabric-reliable-services-and-reliable-actors-preview"></a><span data-ttu-id="61051-104">Inclusión de Reliable Services y Reliable Actors de Service Fabric en contenedores (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="61051-104">How to containerize your Service Fabric Reliable Services and Reliable Actors (Preview)</span></span>

<span data-ttu-id="61051-105">Service Fabric admite la inclusión de microservicios de Service Fabric en contenedores (servicios basados en Reliable Services y Reliable Actors).</span><span class="sxs-lookup"><span data-stu-id="61051-105">Service Fabric supports containerizing Service Fabric microservices (Reliable Services, and Reliable Actor based services).</span></span> <span data-ttu-id="61051-106">Para más información, consulte [Service Fabric y los contenedores](service-fabric-containers-overview.md).</span><span class="sxs-lookup"><span data-stu-id="61051-106">For more information, see [service fabric containers](service-fabric-containers-overview.md).</span></span>


 <span data-ttu-id="61051-107">Esta característica se encuentra en versión preliminar y en este artículo se proporcionan los distintos pasos para que el servicio se ejecute dentro de un contenedor.</span><span class="sxs-lookup"><span data-stu-id="61051-107">This feature is in preview and this article provides the various steps to get your service running inside a container.</span></span>  

> [!NOTE]
> <span data-ttu-id="61051-108">Esta característica se encuentra en versión preliminar y no se admite en producción.</span><span class="sxs-lookup"><span data-stu-id="61051-108">This feature is in preview and is not supported in production.</span></span> <span data-ttu-id="61051-109">Actualmente, esta característica solo funciona para Windows.</span><span class="sxs-lookup"><span data-stu-id="61051-109">Currently this feature only works for Windows.</span></span>

## <a name="steps-to-containerize-your-service-fabric-application"></a><span data-ttu-id="61051-110">Pasos para incluir la aplicación de Service Fabric en contenedores</span><span class="sxs-lookup"><span data-stu-id="61051-110">Steps to containerize your Service Fabric Application</span></span>

1. <span data-ttu-id="61051-111">Abra la aplicación de Service Fabric en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="61051-111">Open your Service Fabric application in Visual Studio.</span></span>

2. <span data-ttu-id="61051-112">Agregue la clase [SFBinaryLoader.cs](https://github.com/Azure/service-fabric-scripts-and-templates/blob/master/code/SFBinaryLoaderForContainers/SFBinaryLoader.cs) al proyecto.</span><span class="sxs-lookup"><span data-stu-id="61051-112">Add class [SFBinaryLoader.cs](https://github.com/Azure/service-fabric-scripts-and-templates/blob/master/code/SFBinaryLoaderForContainers/SFBinaryLoader.cs) to your project.</span></span> <span data-ttu-id="61051-113">El código de esta clase es una aplicación auxiliar para cargar correctamente los archivos binarios del entorno en tiempo de ejecución de Service Fabric dentro de la aplicación cuando se ejecuta dentro de un contenedor.</span><span class="sxs-lookup"><span data-stu-id="61051-113">The code in this class is a helper to correctly load the Service Fabric runtime binaries inside your application when running inside a container.</span></span>

3. <span data-ttu-id="61051-114">Para cada paquete de código que le gustaría incluir en contenedores, inicialice el cargador en el punto de entrada del programa.</span><span class="sxs-lookup"><span data-stu-id="61051-114">For each code package you would like to containerize, initialize the loader at the program entry point.</span></span> <span data-ttu-id="61051-115">Agregue el constructor estático que se muestra en el siguiente fragmento de código al archivo de punto de entrada del programa.</span><span class="sxs-lookup"><span data-stu-id="61051-115">Add the static constructor shown in the following code snippet to your program entry point file.</span></span>

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
          /// This is the entry point of the service host process.
          /// </summary>
          private static void Main()
          {
  ```

4. <span data-ttu-id="61051-116">Compile y [empaquete](service-fabric-package-apps.md#Package-App) el proyecto.</span><span class="sxs-lookup"><span data-stu-id="61051-116">Build and [package](service-fabric-package-apps.md#Package-App) your project.</span></span> <span data-ttu-id="61051-117">Para compilar y crear un paquete, haga clic con el botón derecho en el proyecto de aplicación en el Explorador de soluciones y elija el comando **Empaquetar**.</span><span class="sxs-lookup"><span data-stu-id="61051-117">To build and create a package, right-click the application project in Solution Explorer and choose the **Package** command.</span></span>

5. <span data-ttu-id="61051-118">Para cada paquete de código que necesite incluir en contenedores, ejecute el script de PowerShell [CreateDockerPackage.ps1](https://github.com/Azure/service-fabric-scripts-and-templates/blob/master/scripts/CodePackageToDockerPackage/CreateDockerPackage.ps1).</span><span class="sxs-lookup"><span data-stu-id="61051-118">For every code package you need to containerize, run the PowerShell script [CreateDockerPackage.ps1](https://github.com/Azure/service-fabric-scripts-and-templates/blob/master/scripts/CodePackageToDockerPackage/CreateDockerPackage.ps1).</span></span> <span data-ttu-id="61051-119">El uso es como sigue:</span><span class="sxs-lookup"><span data-stu-id="61051-119">The usage is as follows:</span></span>
  ```powershell
    $codePackagePath = 'Path to the code package to containerize.'
    $dockerPackageOutputDirectoryPath = 'Output path for the generated docker folder.'
    $applicationExeName = 'Name of the ode package executable.'
    CreateDockerPackage.ps1 -CodePackageDirectoryPath $codePackagePath -DockerPackageOutputDirectoryPath $dockerPackageOutputDirectoryPath -ApplicationExeName $applicationExeName
 ```
  <span data-ttu-id="61051-120">El script crea una carpeta con los artefactos de Docker en $dockerPackageOutputDirectoryPath.</span><span class="sxs-lookup"><span data-stu-id="61051-120">The script creates a folder with Docker artifacts at $dockerPackageOutputDirectoryPath.</span></span> <span data-ttu-id="61051-121">Modifique el archivo de Docker generado para exponer los puertos, ejecutar scripts de configuración, etc. según sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="61051-121">Modify the generated Dockerfile to expose any ports, run setup scripts etc. based on your needs.</span></span>

6. <span data-ttu-id="61051-122">A continuación, necesita [compilar](service-fabric-get-started-containers.md#Build-Containers) e [insertar](service-fabric-get-started-containers.md#Push-Containers) el paquete de contenedor de Docker en el repositorio.</span><span class="sxs-lookup"><span data-stu-id="61051-122">Next you need to [build](service-fabric-get-started-containers.md#Build-Containers) and [push](service-fabric-get-started-containers.md#Push-Containers) your Docker container package to your repository.</span></span>

7. <span data-ttu-id="61051-123">Modifique los archivos ApplicationManifest.xml y ServiceManifest.xml para agregar la imagen del contenedor, la información del repositorio, la autenticación del registro y la asignación de puerto al host.</span><span class="sxs-lookup"><span data-stu-id="61051-123">Modify the ApplicationManifest.xml and ServiceManifest.xml to add your container image, repository information, registry authentication, and port-to-host mapping.</span></span> <span data-ttu-id="61051-124">Para modificar los manifiestos, consulte [Cree la primera aplicación contenedora en Service Fabric en Windows](service-fabric-get-started-containers.md).</span><span class="sxs-lookup"><span data-stu-id="61051-124">For modifying the manifests, see [Create an Azure Service Fabric container application](service-fabric-get-started-containers.md).</span></span> <span data-ttu-id="61051-125">La definición de paquete de código en el manifiesto de servicio debe reemplazarse por la imagen de contenedor correspondiente.</span><span class="sxs-lookup"><span data-stu-id="61051-125">The code package definition in the service manifest needs to be replaced with corresponding container image.</span></span> <span data-ttu-id="61051-126">Asegúrese de cambiar EntryPoint a un tipo ContainerHost.</span><span class="sxs-lookup"><span data-stu-id="61051-126">Make sure to change the EntryPoint to a ContainerHost type.</span></span>

  ```xml
<!-- Code package is your service executable. -->
<CodePackage Name="Code" Version="1.0.0">
  <EntryPoint>
    <!-- Follow this link for more information about deploying Windows containers to Service Fabric: https://aka.ms/sfguestcontainers -->
    <ContainerHost>
      <ImageName>myregistry.azurecr.io/samples/helloworldapp</ImageName>
    </ContainerHost>
  </EntryPoint>
  <!-- Pass environment variables to your container: -->    
</CodePackage>
  ```

8. <span data-ttu-id="61051-127">Agregue la asignación de host a puerto para el replicador y el punto de conexión de servicio.</span><span class="sxs-lookup"><span data-stu-id="61051-127">Add the port-to-host mapping for your replicator and service endpoint.</span></span> <span data-ttu-id="61051-128">Puesto que Service Fabric asigna ambos puertos en tiempo de ejecución, ContainerPort se establece en cero para usar el puerto asignado para la asignación.</span><span class="sxs-lookup"><span data-stu-id="61051-128">Since both these ports are assigned at runtime by Service Fabric, the ContainerPort is set to zero to use the assigned port for mapping.</span></span>

 ```xml
<Policies>
  <ContainerHostPolicies CodePackageRef="Code">
    <PortBinding ContainerPort="0" EndpointRef="ServiceEndpoint"/>
    <PortBinding ContainerPort="0" EndpointRef="ReplicatorEndpoint"/>
  </ContainerHostPolicies>
</Policies>
 ```

9. <span data-ttu-id="61051-129">Para probar esta aplicación, debe implementarla en un clúster que esté ejecutando la versión 5.7 o posterior.</span><span class="sxs-lookup"><span data-stu-id="61051-129">To test this application, you need to deploy it to a cluster that is running version 5.7 or higher.</span></span> <span data-ttu-id="61051-130">Además, debe editar y actualizar la configuración del clúster para habilitar esta característica de versión preliminar.</span><span class="sxs-lookup"><span data-stu-id="61051-130">In addition, you need to edit and update the cluster settings to enable this preview feature.</span></span> <span data-ttu-id="61051-131">Siga los pasos de este [artículo](service-fabric-cluster-fabric-settings.md) para agregar la configuración que se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="61051-131">Follow the steps in this [article](service-fabric-cluster-fabric-settings.md) to add the setting shown next.</span></span>
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
10. <span data-ttu-id="61051-132">Después, [implemente](service-fabric-deploy-remove-applications.md) el paquete de aplicación editado en este clúster.</span><span class="sxs-lookup"><span data-stu-id="61051-132">Next [deploy](service-fabric-deploy-remove-applications.md) the edited application package to this cluster.</span></span>

<span data-ttu-id="61051-133">Ahora debería tener una aplicación de Service Fabric en contenedores ejecutando el clúster.</span><span class="sxs-lookup"><span data-stu-id="61051-133">You should now have a containerized Service Fabric application running your cluster.</span></span>

## <a name="next-steps"></a><span data-ttu-id="61051-134">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="61051-134">Next steps</span></span>
* <span data-ttu-id="61051-135">Más información acerca de cómo ejecutar [contenedores en Service Fabric](service-fabric-get-started-containers.md).</span><span class="sxs-lookup"><span data-stu-id="61051-135">Learn more about running [containers on Service Fabric](service-fabric-get-started-containers.md).</span></span>
* <span data-ttu-id="61051-136">Más información acerca del [ciclo de vida de aplicaciones](service-fabric-application-lifecycle.md) de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="61051-136">Learn about the Service Fabric [application life-cycle](service-fabric-application-lifecycle.md).</span></span>
