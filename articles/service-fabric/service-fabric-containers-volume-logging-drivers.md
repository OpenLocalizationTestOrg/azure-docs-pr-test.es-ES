---
title: Crear vista previa en el tejido de Docker servicio aaaAzure | Documentos de Microsoft
description: "Azure Service Fabric acepta Docker Compose toomake de formato sea más fáciles contenedores de exsiting tooorchestrate mediante Service Fabric. Esta compatibilidad se encuentra actualmente en versión preliminar."
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
ms.openlocfilehash: 824044fd698f0ed94c4212722bc82187905315dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="specifying-volume-plugins-and-logging-drivers-for-your-container"></a>Especificación de los complementos de volumen y los controladores de registro para el contenedor

Service Fabric admite la determinación de los [complementos de volumen de Docker](https://docs.docker.com/engine/extend/plugins_volume/) y de los [controladores de registro de Docker](https://docs.docker.com/engine/admin/logging/overview/) para Container Service. Hola complementos se especifican en el manifiesto de aplicación Hola tal como se muestra en hello después de manifiesto:


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

En el anterior ejemplo de Hola Hola `Source` etiqueta para hello `Volume` hace referencia a la carpeta de origen toohello. carpeta de origen de Hello podría ser una carpeta en hello máquina virtual que hospeda contenedores de Hola o un almacén persistente remoto. Hola `Destination` etiqueta es la ubicación de Hola Hola `Source` toowithin asignadas Hola ejecuta contenedor. 

Al especificar un complemento de volumen, Service Fabric crea automáticamente el volumen Hola con parámetros de hello especificados. Hola `Source` etiqueta es el nombre de hello del volumen de Hola y Hola `Driver` etiqueta Especifica Hola volumen controlador complemento. Opciones pueden especificarse mediante hello `DriverOption` etiqueta como se muestra en el siguiente fragmento de código de hello:

```xml
<Volume Source="myvolume1" Destination="c:\testmountlocation4" Driver="azurefile" IsReadOnly="true">
           <DriverOption Name="share" Value="models"/>
</Volume>
```

Si se especifica un controlador de registro de Docker, es necesario toodeploy hello toohandle agentes (o contenedores) inicia sesión en el clúster de Hola.  Hola `DriverOption` etiqueta puede ser también las opciones de controlador del registro de toospecify usado.

Consulte toohello después de clúster de Service Fabric tooa de artículos toodeploy contenedores:


[Implementación de un contenedor en Service Fabric](service-fabric-deploy-container.md)

