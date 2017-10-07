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
# <a name="how-toocontainerize-your-service-fabric-reliable-services-and-reliable-actors-preview"></a>¿Cómo toocontainerize la confianza de tejido de servicio de servicios y Reliable Actors (versión preliminar)

Service Fabric admite la inclusión de microservicios de Service Fabric en contenedores (servicios basados en Reliable Services y Reliable Actors). Para más información, consulte [Service Fabric y los contenedores](service-fabric-containers-overview.md).


 Esta característica está en versión preliminar y este artículo proporciona Hola tooget de varios pasos en el servicio que se ejecuta dentro de un contenedor.  

> [!NOTE]
> Esta característica se encuentra en versión preliminar y no se admite en producción. Actualmente, esta característica solo funciona para Windows.

## <a name="steps-toocontainerize-your-service-fabric-application"></a>Los pasos toocontainerize su aplicación de servicio de Fabric

1. Abra la aplicación de Service Fabric en Visual Studio.

2. Agregar clase [SFBinaryLoader.cs](https://github.com/Azure/service-fabric-scripts-and-templates/blob/master/code/SFBinaryLoaderForContainers/SFBinaryLoader.cs) tooyour proyecto. código de Hello de esta clase es una aplicación auxiliar toocorrectly carga Hola Service Fabric en tiempo de ejecución los archivos binarios dentro de una aplicación cuando se ejecuta dentro de un contenedor.

3. Para cada paquete de código le gustaría toocontainerize, initialize Hola cargador en el punto de entrada del programa Hola. Agregue el constructor estático de Hola que se muestra en el siguiente archivo de punto de entrada de programa tooyour de fragmentos de código de hello.

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

4. Compile y [empaquete](service-fabric-package-apps.md#Package-App) el proyecto. toobuild y crear un paquete, haga clic en proyecto de aplicación de hello en el Explorador de soluciones y elija hello **paquete** comando.

5. Para cada paquete de código debe toocontainerize, ejecución Hola script de PowerShell [CreateDockerPackage.ps1](https://github.com/Azure/service-fabric-scripts-and-templates/blob/master/scripts/CodePackageToDockerPackage/CreateDockerPackage.ps1). uso de Hello es como sigue:
  ```powershell
    $codePackagePath = 'Path toohello code package toocontainerize.'
    $dockerPackageOutputDirectoryPath = 'Output path for hello generated docker folder.'
    $applicationExeName = 'Name of hello ode package executable.'
    CreateDockerPackage.ps1 -CodePackageDirectoryPath $codePackagePath -DockerPackageOutputDirectoryPath $dockerPackageOutputDirectoryPath -ApplicationExeName $applicationExeName
 ```
  script de Hola crea una carpeta con los artefactos de Docker en $dockerPackageOutputDirectoryPath. Modificar Hola genera Dockerfile tooexpose los puertos, ejecutar scripts de configuración etc. según sus necesidades.

6. A continuación hay demasiado[generar](service-fabric-get-started-containers.md#Build-Containers) y [inserción](service-fabric-get-started-containers.md#Push-Containers) el repositorio de tooyour del paquete de contenedor de Docker.

7. Modificar hello ApplicationManifest.xml y ServiceManifest.xml tooadd su imagen de contenedor, información del repositorio, la autenticación del registro y asignación de puerto al host. Para modificar los manifiestos de hello, consulte [crear una aplicación de contenedor de Azure Service Fabric](service-fabric-get-started-containers.md). definición de paquete de código de Hello en hello servicio necesidades manifiesto toobe reemplazado por la imagen de contenedor correspondiente. Asegúrese de que toochange Hola EntryPoint tooa ContainerHost tipo.

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

8. Agregar asignación de puerto para alojar hello para el replicador y el extremo de servicio. Puesto que ambas estos puertos se asignan en tiempo de ejecución por Service Fabric, hello ContainerPort se establece toozero toouse Hola le asignada el puerto para la asignación.

 ```xml
<Policies>
  <ContainerHostPolicies CodePackageRef="Code">
    <PortBinding ContainerPort="0" EndpointRef="ServiceEndpoint"/>
    <PortBinding ContainerPort="0" EndpointRef="ReplicatorEndpoint"/>
  </ContainerHostPolicies>
</Policies>
 ```

9. tootest esta aplicación, necesita toodeploy se tooa clúster que se está ejecutando la versión 5.7 o posterior. Además, se necesita tooedit y actualiza tooenable de configuración de clúster de hello esta característica de vista previa. Siga los pasos de hello en este [artículo](service-fabric-cluster-fabric-settings.md) configuración de hello tooadd aprecia aquí.
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
10. Siguiente [implementar](service-fabric-deploy-remove-applications.md) Hola editar clúster de toothis del paquete de aplicación.

Ahora debería tener una aplicación de Service Fabric en contenedores ejecutando el clúster.

## <a name="next-steps"></a>Pasos siguientes
* Más información acerca de cómo ejecutar [contenedores en Service Fabric](service-fabric-get-started-containers.md).
* Obtenga información acerca de Service Fabric hello [ciclo de vida de la aplicación](service-fabric-application-lifecycle.md).
