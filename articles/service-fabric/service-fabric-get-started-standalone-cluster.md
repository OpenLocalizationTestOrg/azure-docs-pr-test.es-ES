---
title: "aaaSet de un clúster de Azure Service Fabric independientes | Documentos de Microsoft"
description: "Crear un clúster de desarrollo independiente con tres nodos con hello mismo equipo. Después de completar la instalación, estará listo toocreate un clúster de varios equipo."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/06/2017
ms.author: dekapur
ms.openlocfilehash: e4d0ea9fc3b8475160bd8ed19fd3716463791cc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-service-fabric-standalone-cluster"></a>Creación del primer clúster independiente de Service Fabric
Puede crear un clúster de Service Fabric independientes en las máquinas virtuales o equipos que ejecutan Windows Server 2012 R2 o Windows Server 2016, local o en la nube de Hola. Este inicio rápido le ayuda a toocreate un clúster de desarrollo independiente en sólo unos minutos.  Cuando haya terminado, tendrá un clúster de tres nodos que se ejecuta en un único equipo y donde puede implementar aplicaciones.

## <a name="before-you-begin"></a>Antes de empezar
Tejido de servicio proporciona un programa de instalación de clústeres de paquete toocreate Service Fabric independientes.  [Descargar paquete de instalación de hello](http://go.microsoft.com/fwlink/?LinkId=730690).  Descomprima Hola carpeta setup del paquete tooa Hola equipo o máquina virtual donde estás configurando clúster de desarrollo de Hola.  contenido de Hola Hola del paquete de instalación se describe detalladamente [aquí](service-fabric-cluster-standalone-package-contents.md).

el Administrador de clústeres Hola implementar y configurar el clúster de hello debe tener privilegios de administrador en el equipo de Hola. No se puede instalar Service Fabric en un controlador de dominio.

## <a name="validate-hello-environment"></a>Valide el entorno de Hola
Hola *TestConfiguration.ps1* script en el paquete independiente de Hola se utiliza como un toovalidate de analizador de prácticas recomendada, si un clúster puede implementarse en un entorno determinado. [Preparación de la implementación](service-fabric-cluster-standalone-deployment-preparation.md) listas Hola requisitos previos y requisitos del entorno. Ejecute hello script tooverify si puede crear el clúster de desarrollo de hello:

```powershell
.\TestConfiguration.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json
```
## <a name="create-hello-cluster"></a>Crear clúster Hola
Varios archivos de configuración de clúster de ejemplo se instalan con el paquete de instalación de Hola. *ClusterConfig.Unsecure.DevCluster.json* es configuración de clúster más sencilla de hello: un clúster no seguro, tres nodos que se ejecute en un único equipo.  Otros archivos de configuración describen clústeres de una o varias máquinas con certificados X.509 o seguridad de Windows.  No necesita toomodify cualquiera de los valores de configuración de hello predeterminado para este tutorial, pero examine el archivo de configuración de Hola y familiarizarse con la configuración de Hola.  Hola **nodos** sección describen tres nodos de hello en clúster de Hola: nombre, dirección IP, [tipo de nodo, el dominio de error y el dominio de actualización](service-fabric-cluster-manifest.md#nodes-on-the-cluster).  Hola **propiedades** sección define hello [seguridad, nivel de confiabilidad, recopilación de diagnósticos y tipos de nodos](service-fabric-cluster-manifest.md#cluster-properties) para clúster Hola.

Este clúster no es seguro.  Cualquiera puede conectarse de forma anónima y realizar operaciones de administración, por lo que los clústeres de producción siempre deben protegerse mediante certificados X.509 o la seguridad de Windows.  Solo se configura con seguridad en el momento de creación de clúster y no es posible tooenable seguridad después de crear el clúster de Hola.  Lectura [proteger un clúster](service-fabric-cluster-security.md) toolearn más acerca de la seguridad de clúster de Service Fabric.  

clúster de desarrollo de tres nodos de hello toocreate, ejecute hello *CreateServiceFabricCluster.ps1* secuencia de comandos desde una sesión de PowerShell de administrador:

```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json -AcceptEULA
```

paquete de tiempo de ejecución de Service Fabric Hola automáticamente se descarga e instala en el momento de creación del clúster.

## <a name="connect-toohello-cluster"></a>Conectar el clúster toohello
Ahora se está ejecutando el clúster de desarrollo de tres nodos. Hola módulo ServiceFabric PowerShell se instala con hello en tiempo de ejecución.  Puede comprobar dicho clúster Hola se está ejecutando desde Hola mismo equipo o desde un equipo remoto con el tiempo de ejecución de hello Service Fabric.  Hola [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet establece un clúster de toohello de conexión.   

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint localhost:19000
```
Vea [clúster segura de conectar tooa](service-fabric-connect-to-secure-cluster.md) para obtener ejemplos de conexión de tooa de clúster. Después de la conexión de toohello de clúster, use hello [ServiceFabricNode Get](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) cmdlet toodisplay una lista de nodos en la información de clúster y el estado de Hola para cada nodo. **HealthState** debe ser *OK* para cada nodo.

```powershell
PS C:\temp\Microsoft.Azure.ServiceFabric.WindowsServer> Get-ServiceFabricNode |Format-Table

NodeDeactivationInfo NodeName IpAddressOrFQDN NodeType  CodeVersion  ConfigVersion NodeStatus NodeUpTime NodeDownTime HealthState
-------------------- -------- --------------- --------  -----------  ------------- ---------- ---------- ------------ -----------
                     vm2      localhost       NodeType2 5.6.220.9494 0                     Up 00:03:38   00:00:00              OK
                     vm1      localhost       NodeType1 5.6.220.9494 0                     Up 00:03:38   00:00:00              OK
                     vm0      localhost       NodeType0 5.6.220.9494 0                     Up 00:02:43   00:00:00              OK
```

## <a name="visualize-hello-cluster-using-service-fabric-explorer"></a>Visualizar el clúster de hello mediante el Explorador de Service Fabric
[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) es una buena herramienta para visualizar el clúster y administrar aplicaciones.  Explorador de Service Fabric es un servicio que se ejecuta en el clúster de hello, que puede tener acceso mediante un explorador navegando demasiado[http://localhost:19080/explorador](http://localhost:19080/Explorer). 

panel de clúster de Hello proporciona una visión general del clúster, incluido un resumen de la aplicación y el estado de nodo. vista de nodo de Hello muestra el diseño físico de Hola de clúster de Hola. Para un nodo determinado, puede comprobar qué aplicaciones tienen el código implementado en ese nodo.

![Service Fabric Explorer][service-fabric-explorer]

## <a name="remove-hello-cluster"></a>Quitar clúster Hola
tooremove un clúster, ejecute hello *RemoveServiceFabricCluster.ps1* script de PowerShell desde la carpeta del paquete hello y pase el archivo de configuración de hello ruta de acceso toohello JSON. También puede especificar una ubicación para el registro de hello de eliminación de Hola.

```powershell
# Removes Service Fabric cluster nodes from each computer in hello configuration file.
.\RemoveServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json -Force
```

tooremove Hola Service Fabric en tiempo de ejecución del equipo de hello, ejecute hello siguiente script de PowerShell de la carpeta de paquete de Hola.

```powershell
# Removes Service Fabric from hello current computer.
.\CleanFabric.ps1
```

## <a name="next-steps"></a>Pasos siguientes
Ahora que ha configurado un clúster de desarrollo independiente, intente Hola siguientes artículos:
* [Configure un clúster independiente con varias máquinas](service-fabric-cluster-creation-for-windows-server.md) y habilite la seguridad.
* [Implemente aplicaciones mediante PowerShell](service-fabric-deploy-remove-applications.md).

[service-fabric-explorer]: ./media/service-fabric-get-started-standalone-cluster/sfx.png
