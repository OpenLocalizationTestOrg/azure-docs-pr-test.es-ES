---
title: "Versión preliminar de Azure Service Fabric Docker Compose | Microsoft Docs"
description: "Azure Service Fabric acepta el formato de Docker Compose para facilitar la orquestación de los contenedores existentes mediante Service Fabric. Esta compatibilidad se encuentra actualmente en versión preliminar."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: ab49c4b9-74a8-4907-b75b-8d2ee84c6d90
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: b12ef95add6347621f7d4865fac46568f91a1e12
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="specifying-volume-plugins-and-logging-drivers-for-your-container"></a><span data-ttu-id="623be-104">Especificación de los complementos de volumen y los controladores de registro para el contenedor</span><span class="sxs-lookup"><span data-stu-id="623be-104">Specifying volume plugins and logging drivers for your container</span></span>

<span data-ttu-id="623be-105">Service Fabric admite la determinación de los [complementos de volumen de Docker](https://docs.docker.com/engine/extend/plugins_volume/) y de los [controladores de registro de Docker](https://docs.docker.com/engine/admin/logging/overview/) para Container Service.</span><span class="sxs-lookup"><span data-stu-id="623be-105">Service Fabric supports specifying [Docker volume plugins](https://docs.docker.com/engine/extend/plugins_volume/) and [Docker logging drivers](https://docs.docker.com/engine/admin/logging/overview/) for your container service.</span></span> <span data-ttu-id="623be-106">Los complementos se especifican en el manifiesto de aplicación, como se muestra en el siguiente manifiesto:</span><span class="sxs-lookup"><span data-stu-id="623be-106">The plugins are specified in the application manifest as shown in the following manifest:</span></span>


```xml
?xml version="1.0" encoding="UTF-8"?>
<ApplicationManifest ApplicationTypeName="WinNodeJsApp" ApplicationTypeVersion="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
    <Description>Calculator Application</Description>
    <Parameters>
        <Parameter Name="ServiceInstanceCount" DefaultValue="3"></Parameter>
      <Parameter Name="MyCpuShares" DefaultValue="3"></Parameter>
    </Parameters>
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="NodeServicePackage" ServiceManifestVersion="1.0"/>
     <Policies>
       <ContainerHostPolicies CodePackageRef="NodeService.Code" Isolation="hyperv"> 
        <PortBinding ContainerPort="8905" EndpointRef="Endpoint1"/>
        <RepositoryCredentials PasswordEncrypted="false" Password="****" AccountName="test"/>
        <LogConfig Driver="etwlogs" >
          <DriverOption Name="test" Value="vale"/>
        </LogConfig>
        <Volume Source="c:\workspace" Destination="c:\testmountlocation1" IsReadOnly="false"></Volume>
        <Volume Source="d:\myfolder" Destination="c:\testmountlocation2" IsReadOnly="true"> </Volume>
        <Volume Source="myexternalvolume" Destination="c:\testmountlocation3" Driver="sf" IsReadOnly="true"></Volume>
       </ContainerHostPolicies>
   </Policies>
    </ServiceManifestImport>
    <ServiceTemplates>
        <StatelessService ServiceTypeName="StatelessNodeService" InstanceCount="5">
            <SingletonPartition></SingletonPartition>
        </StatelessService>
    </ServiceTemplates>
</ApplicationManifest>
```

<span data-ttu-id="623be-107">En el ejemplo anterior, la etiqueta `Source` de `Volume` hace referencia a la carpeta de origen.</span><span class="sxs-lookup"><span data-stu-id="623be-107">In the preceding example, the `Source` tag for the `Volume` refers to the source folder.</span></span> <span data-ttu-id="623be-108">La carpeta de origen puede ser una carpeta de la máquina virtual que hospeda los contenedores o un almacén remoto persistente.</span><span class="sxs-lookup"><span data-stu-id="623be-108">The source folder could be a folder in the VM that hosts the containers or a persistent remote store.</span></span> <span data-ttu-id="623be-109">La etiqueta `Destination` es la ubicación a la que `Source` está asignado dentro del contenedor en ejecución.</span><span class="sxs-lookup"><span data-stu-id="623be-109">The `Destination` tag is the location that the `Source` is mapped to within the running container.</span></span> 

<span data-ttu-id="623be-110">Al especificar un complemento de volumen, Service Fabric crea automáticamente el volumen con los parámetros especificados.</span><span class="sxs-lookup"><span data-stu-id="623be-110">When specifying a volume plugin, Service Fabric automatically creates the volume using the parameters specified.</span></span> <span data-ttu-id="623be-111">La etiqueta `Source` es el nombre del volumen y la etiqueta `Driver` especifica el complemento de controlador del volumen.</span><span class="sxs-lookup"><span data-stu-id="623be-111">The `Source` tag is the name of the volume, and the `Driver` tag specifies the volume driver plugin.</span></span> <span data-ttu-id="623be-112">Las opciones pueden especificarse mediante la etiqueta `DriverOption`, como se muestra en el fragmento de código siguiente:</span><span class="sxs-lookup"><span data-stu-id="623be-112">Options can be specified using the `DriverOption` tag as shown in the following snippet:</span></span>

```xml
<Volume Source="myvolume1" Destination="c:\testmountlocation4" Driver="azurefile" IsReadOnly="true">
           <DriverOption Name="share" Value="models"/>
</Volume>
```

<span data-ttu-id="623be-113">Si se especifica un controlador de registro de Docker, es necesario implementar agentes o contenedores para controlar los registros en el clúster.</span><span class="sxs-lookup"><span data-stu-id="623be-113">If a Docker log driver is specified, it is necessary to deploy agents (or containers) to handle the logs in the cluster.</span></span>  <span data-ttu-id="623be-114">La etiqueta `DriverOption` además se puede usar para especificar opciones del controlador de registro.</span><span class="sxs-lookup"><span data-stu-id="623be-114">The `DriverOption` tag can be used to specify log driver options as well.</span></span>

<span data-ttu-id="623be-115">Consulte los artículos siguientes para implementar contenedores en un clúster de Service Fabric:</span><span class="sxs-lookup"><span data-stu-id="623be-115">Refer to the following articles to deploy containers to a Service Fabric cluster:</span></span>


[<span data-ttu-id="623be-116">Implementación de un contenedor en Service Fabric</span><span class="sxs-lookup"><span data-stu-id="623be-116">Deploy a container on Service Fabric</span></span>](service-fabric-deploy-container.md)

