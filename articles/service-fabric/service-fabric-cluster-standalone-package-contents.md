---
title: Paquete de Service Fabric independientes para Windows Server aaaAzure | Documentos de Microsoft
description: "Descripción y el contenido del paquete de hello Azure Service Fabric independientes para Windows Server."
services: service-fabric
documentationcenter: .net
author: maburlik
manager: timlt
editor: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/10/2017
ms.author: chackdan;maburlik
ms.openlocfilehash: e4c6cb9128d659144e559fcad06bb78c9969dd60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="contents-of-service-fabric-standalone-package-for-windows-server"></a>Contenido del paquete independiente de Service Fabric para Windows Server
Hola [descargado](http://go.microsoft.com/fwlink/?LinkId=730690) paquete independiente de tejido de servicio, encontrará Hola siguientes archivos:

| **Nombre de archivo** | **Descripción breve** |
| --- | --- |
| CreateServiceFabricCluster.ps1 |Un script de PowerShell que crea el clúster de hello mediante configuración de hello en ClusterConfig.json. |
| RemoveServiceFabricCluster.ps1 |Un script de PowerShell que quita un clúster con configuración de hello en ClusterConfig.json. |
| AddNode.ps1 |Un script de PowerShell para agregar un nodo existente de tooan implementa clústeres de máquina actual Hola. |
| RemoveNode.ps1 |Un script de PowerShell para quitar un nodo de una existente implementa clústeres de máquina actual Hola. |
| CleanFabric.ps1 |Un script de PowerShell para la limpieza de una instalación de Service Fabric máquina actual Hola independiente. Las instalaciones anteriores de MSI se deben quitar mediante sus propios desinstaladores asociados. |
| TestConfiguration.ps1 |Un script de PowerShell para analizar la infraestructura de hello como se especifica en hello Cluster.json. |
| DownloadServiceFabricRuntimePackage.ps1 |Un script de PowerShell que se usa para descargar el paquete en tiempo de ejecución más reciente de hello fuera de banda, para escenarios donde hello implementar máquina no está conectado toohello internet. |
| DeploymentComponentsAutoextractor.exe |Archivo que contiene los componentes de implementación autoextraíble utiliza Hola scripts de paquete independiente. |
| EULA_ENU.txt |términos de licencia de Hola para hello el uso de paquete de Windows Server de Microsoft Azure Service Fabric independiente. También puede [descargar una copia del CLUF de hello](http://go.microsoft.com/fwlink/?LinkID=733084) ahora. |
| Readme.txt |Un vínculo toohello versión notas e instrucciones básicas para la instalación. Es un subconjunto de instrucciones de hello en este documento. |
| ThirdPartyNotice.rtf |Aviso de software de terceros que se encuentra en el paquete de saludo. |
| Tools\Microsoft.Azure.ServiceFabric.WindowsServer.SupportPackage.zip |StandaloneLogCollector.exe que se ejecuta en petición toocollect y carga el seguimiento de los registros de tooMicrosoft con el fin de soporte técnico. |
| Tools\ServiceFabricUpdateService.zip |Utiliza una herramienta tooenable la actualización automática de código para los clústeres que no tienen acceso a internet. [aquí](service-fabric-cluster-upgrade-windows-server.md)|

**Plantillas** 
| **Nombre de archivo** | **Descripción breve** |
| --- | --- |
| ClusterConfig.Unsecure.DevCluster.json |Un archivo de ejemplo de configuración de clúster que contiene la configuración de Hola para una no seguro, tres nodos, solo el equipo (o máquina virtual) clúster de desarrollo, incluida la información de Hola para cada nodo de clúster de Hola. |
| ClusterConfig.Unsecure.MultiMachine.json |Un archivo de ejemplo de configuración de clúster que contiene la configuración de Hola para un clúster no seguro, varios equipos (o máquina virtual), incluida la información de Hola para cada máquina en clúster de Hola. |
| ClusterConfig.Windows.DevCluster.json |Un archivo de ejemplo de configuración de clúster que contiene todos los clúster de desarrollo de configuración para un único equipo seguro y tres nodos, (o la máquina virtual) de hello, incluida la información de Hola para cada nodo que está en clúster de Hola. clúster de Hello está protegido mediante [identidades de Windows](https://msdn.microsoft.com/library/ff649396.aspx). |
| ClusterConfig.Windows.MultiMachine.json |Un archivo de ejemplo de configuración de clúster que contiene toda la configuración para un clúster de varios equipos (o máquinas virtuales) seguro, utilizando la seguridad de Windows, incluida la información de Hola para cada máquina que se encuentra en clúster segura Hola Hola. clúster de Hello está protegido mediante [identidades de Windows](https://msdn.microsoft.com/library/ff649396.aspx). |
| ClusterConfig.x509.DevCluster.json |Un archivo de ejemplo de configuración de clúster que contiene todos los valores de hello para un seguro, tres nodos, solo el equipo (o máquina virtual) clúster de desarrollo, incluida la información de Hola para cada nodo de clúster de Hola. Hello clúster se protege utilizando x509 certificados. |
| ClusterConfig.x509.MultiMachine.json |Un archivo de ejemplo de configuración de clúster que contiene todos los valores de hello para hello seguros, clúster de varios equipos (o máquinas virtuales), incluida la información de Hola para cada nodo de clúster segura Hola. Hello clúster se protege utilizando x509 certificados. |
| ClusterConfig.gMSA.Windows.MultiMachine.json |Un archivo de ejemplo de configuración de clúster que contiene todos los valores de hello para hello seguros, clúster de varios equipos (o máquinas virtuales), incluida la información de Hola para cada nodo de clúster segura Hola. Hello clúster se protege utilizando [cuentas de servicio administradas de grupo](https://technet.microsoft.com/en-us/library/jj128431(v=ws.11).aspx). |

## <a name="cluster-configuration-samples"></a>Ejemplos de configuración del clúster
Las versiones más recientes de plantillas de configuración de clúster pueden encontrarse en la página de GitHub de hello: [ejemplos de configuración de clúster independiente](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples).

## <a name="independent-runtime-package"></a>Paquete del entorno en tiempo de ejecución independiente
paquete en tiempo de ejecución más reciente de Hola se descarga automáticamente durante la implementación de clúster de [vínculo Download - servicio de Fabric en tiempo de ejecución - Windows Server](https://go.microsoft.com/fwlink/?linkid=839354).

## <a name="related"></a>Temas relacionados
* [Creación de un clúster de Azure Service Fabric independiente](service-fabric-cluster-creation-for-windows-server.md)
* [Escenarios de seguridad de los clústeres de Service Fabric](service-fabric-windows-cluster-windows-security.md)
