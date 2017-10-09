---
title: "un clúster de Azure Service Fabric independientes aaaCreate | Documentos de Microsoft"
description: "Cree un clúster de Azure Service Fabric en cualquier máquina (física o virtual) que ejecute Windows Server, ya sea local o en una nube."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 31349169-de19-4be6-8742-ca20ac41eb9e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/10/2017
ms.author: chackdan;maburlik;dekapur
ms.openlocfilehash: 444970816290a0448d88a8b2082c75eb7a64cb44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-standalone-cluster-running-on-windows-server"></a>Creación de un clúster independiente con Windows Server
Puede usar Azure Service Fabric toocreate Service Fabric clústeres en las máquinas virtuales o equipos que ejecutan Windows Server. Es decir, podrá implementar y ejecutar aplicaciones de Service Fabric en cualquier entorno donde haya un conjunto de equipos con Windows Server que estén conectados entre sí, ya sea de manera local o con algún proveedor de servicios en la nube. Service Fabric proporciona un toocreate de paquete de instalación de clústeres de Service Fabric denominada paquete de Windows Server de hello independiente.

En este artículo le guiará por los pasos de Hola para crear un clúster de Service Fabric independientes.

> [!NOTE]
> Este paquete de Windows Server independiente está disponible en el mercado y puede usarse para las implementaciones de producción. Además, puede contener nuevas características de Service Fabric que están en versión preliminar. Desplácese hacia abajo demasiado"[incluidos en este paquete de características de vista previa](#previewfeatures_anchor)." sección de la lista de Hola de características de vista previa de Hola. También puede [descargar una copia del CLUF de hello](http://go.microsoft.com/fwlink/?LinkID=733084) ahora.
> 
> 

<a id="getsupport"></a>

## <a name="get-support-for-hello-service-fabric-for-windows-server-package"></a>Obtener soporte técnico para el paquete de hello Service Fabric para Windows Server
* Preguntarme Comunidad Hola paquete independiente de Service Fabric de Hola para Windows Server en hello [foro de Azure Service Fabric](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=AzureServiceFabric?).
* Abra una incidencia para obtener [soporte técnico profesional para Service Fabric](http://support.microsoft.com/oas/default.aspx?prid=16146).  Más información sobre el soporte técnico profesional de Microsoft[aquí](https://support.microsoft.com/en-us/gp/offerprophone?wa=wsignin1.0).
* También puede obtener soporte técnico para este paquete como parte del [soporte técnico Premier de Microsoft](https://support.microsoft.com/en-us/premier).
* Para más información, consulte [Opciones de soporte técnico de Azure Service Fabric](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-support).
* registros de toocollect por motivos de compatibilidad, ejecute hello [compilador de registros de Service Fabric independientes](service-fabric-cluster-standalone-package-contents.md).

<a id="downloadpackage"></a>

## <a name="download-hello-service-fabric-for-windows-server-package"></a>Descargar paquete de hello Service Fabric para Windows Server
clúster de hello toocreate, use el paquete de hello Service Fabric para Windows Server (Windows Server 2012 R2 y versiones más recientes) encontrar aquí: <br>
[Vínculo de descarga del paquete independiente de Service Fabric de Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690)

Buscar detalles sobre el contenido del paquete de hello [aquí](service-fabric-cluster-standalone-package-contents.md).

paquete de Hello Service Fabric en tiempo de ejecución se descarga automáticamente en tiempo de creación del clúster. Si la implementación desde un equipo no conectado toohello internet, descargue paquete en tiempo de ejecución de hello fuera de banda desde aquí: <br>
[Vínculo de descarga del entorno de tiempo de ejecución de Service Fabric para Windows Server](https://go.microsoft.com/fwlink/?linkid=839354)

Puede encontrar ejemplos de configuración de clúster independiente en: <br>
[Ejemplos de configuración de clúster independiente](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples)

<a id="createcluster"></a>

## <a name="create-hello-cluster"></a>Crear clúster Hola
Service Fabric puede ser clúster de desarrollo de una máquina de tooa implementado mediante el uso de hello *ClusterConfig.Unsecure.DevCluster.json* los archivos incluidos en [ejemplos](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples).

Desempaquetar máquina de hello independiente paquete tooyour, equipo local del toohello de archivo de copia Hola ejemplo configuración y luego Hola ejecución *CreateServiceFabricCluster.ps1* secuencia de comandos a través de una sesión de PowerShell de administrador de hello independiente carpeta de paquete:
### <a name="step-1a-create-an-unsecured-local-development-cluster"></a>Paso 1A: Creación de un clúster de desarrollo local poco seguro
```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json -AcceptEULA
```

Vea Hola sección de configuración del entorno en [planear y preparar la implementación de clúster](service-fabric-cluster-standalone-deployment-preparation.md) para obtener más información de solución de problemas.

Si ya ha terminado de ejecutar escenarios de desarrollo, puede quitar clúster de Service Fabric Hola de máquina de hello consultando toosteps en la sección "[quitar un clúster](#removecluster_anchor)". 

### <a name="step-1b-create-a-multi-machine-cluster"></a>Paso 1B: Creación de un clúster de varias máquinas
Después de haber pasado a través de planeación de Hola y detallan de los pasos de preparación en hello siguiente vínculo, está listo toocreate su clúster de producción mediante el archivo de configuración de clúster. <br>
[Plan and prepare your cluster deployment](service-fabric-cluster-standalone-deployment-preparation.md) (Planeamiento y preparación del desarrollo del clúster)

1. Validar archivo de configuración de Hola que haya escrito mediante la ejecución de hello *TestConfiguration.ps1* secuencia de comandos de la carpeta de paquete de hello independiente:  

    ```powershell
    .\TestConfiguration.ps1 -ClusterConfigFilePath .\ClusterConfig.json
    ```

    El resultado debería ser parecido al que se muestra a continuación. Si el campo de hello inferior "Correcto" aparece como "True", han pasado las comprobaciones de integridad y clúster Hola busca toobe pueden implementar en función de la configuración de entrada de Hola.

    ```
    Trace folder already exists. Traces will be written tooexisting trace folder: C:\temp\Microsoft.Azure.ServiceFabric.WindowsServer\DeploymentTraces
    Running Best Practices Analyzer...
    Best Practices Analyzer completed successfully.
    
    LocalAdminPrivilege        : True
    IsJsonValid                : True
    IsCabValid                 : True
    RequiredPortsOpen          : True
    RemoteRegistryAvailable    : True
    FirewallAvailable          : True
    RpcCheckPassed             : True
    NoConflictingInstallations : True
    FabricInstallable          : True
    Passed                     : True
    ```

2. Crear clúster hello: ejecute hello *CreateServiceFabricCluster.ps1* clúster de secuencia de comandos toodeploy Hola Service Fabric a través de cada máquina en la configuración de Hola. 
    ```powershell
    .\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.json -AcceptEULA
    ```

> [!NOTE]
> Los seguimientos de implementación se escriben toohello VM/máquina en la que se ejecutó el script de PowerShell de CreateServiceFabricCluster.ps1 de Hola. Estos pueden encontrarse en la subcarpeta de hello DeploymentTraces, basada en directorio Hola desde qué Hola se ejecutó la secuencia de comandos. toosee si Service Fabric se ha había implementado correctamente tooa máquina, buscar archivos de hello instalado en directorio de FabricDataRoot hello, como se detalla en el archivo de configuración del clúster de hello FabricSettings sección (de c:\ProgramData\SF de forma predeterminada). También, los procesos FabricHost.exe y Fabric.exe se pueden ver ejecutando el Administrador de tareas.
> 
> 

### <a name="step-1c-create-an-offline-internet-disconnected-cluster"></a>Paso 1C: Creación de un clúster sin conexión (desconectado de internet)
paquete de Hello Service Fabric en tiempo de ejecución se descarga automáticamente durante la creación del clúster. Al implementar un clúster toomachines no conectado toohello internet, deberá hello toodownload Service Fabric en tiempo de ejecución del paquete por separado y proporcionar hello tooit de ruta de acceso en la creación del clúster.
se puede descargar por separado Hello paquete en tiempo de ejecución, desde otro equipo conectado toohello internet, en [vínculo Download - servicio de Fabric en tiempo de ejecución - Windows Server](https://go.microsoft.com/fwlink/?linkid=839354). Copiar hello toowhere de paquete en tiempo de ejecución va a implementar el clúster sin conexión de Hola de y crea clúster hello mediante la ejecución de `CreateServiceFabricCluster.ps1` con hello `-FabricRuntimePackagePath` parámetro incluido, tal y como se muestra a continuación: 

```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.json -FabricRuntimePackagePath .\MicrosoftAzureServiceFabric.cab
```
donde `.\ClusterConfig.json` y `.\MicrosoftAzureServiceFabric.cab` son configuración de clúster toohello de hello las rutas de acceso y el archivo .cab de hello en tiempo de ejecución, respectivamente.


### <a name="step-2-connect-toohello-cluster"></a>Paso 2: Conectar toohello clúster
clúster de tooconnect tooa segura, consulte [Service fabric conectarse clúster toosecure](service-fabric-connect-to-secure-cluster.md).

tooconnect tooan clúster, ejecute el siguiente comando de PowerShell de hello:

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <*IPAddressofaMachine*>:<Client connection end point port>
```
Ejemplo:
```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint 192.13.123.2345:19000
```
### <a name="step-3-bring-up-service-fabric-explorer"></a>Paso 3: Incorporación de Service Fabric Explorer
Ahora puede conectarse toohello clúster con Service Fabric Explorer ya sea directamente a uno de los equipos de hello con http://localhost:19080/Explorer/index.html o de forma remota con http://<*IPAddressofaMachine*>: 19080 / Explorer/index.HTML.

## <a name="add-and-remove-nodes"></a>Agregar y quitar nodos
Puede agregar o quitar clúster de Service Fabric de nodos tooyour independiente, ya que cambien las necesidades empresariales. Vea [agregar o quitar nodos tooa Service Fabric independientes clúster](service-fabric-cluster-windows-server-add-remove-nodes.md) para obtener pasos detallados.

<a id="removecluster" name="removecluster_anchor"></a>
## <a name="remove-a-cluster"></a>Eliminación de un clúster
tooremove un clúster, ejecute hello *RemoveServiceFabricCluster.ps1* script de PowerShell desde la carpeta del paquete hello y pase el archivo de configuración de hello ruta de acceso toohello JSON. También puede especificar una ubicación para el registro de hello de eliminación de Hola.

Este script se puede ejecutar en cualquier equipo que tenga equipos Hola de tooall de acceso de administrador que se muestran como nodos en el archivo de configuración del clúster de Hola. máquina de Hola que este script se ejecuta en no tiene toobe parte del clúster de Hola.

```
# Removes Service Fabric from each machine in hello configuration
.\RemoveServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.json -Force
```

```
# Removes Service Fabric from hello current machine
.\CleanFabric.ps1
```

<a id="telemetry"></a>

## <a name="telemetry-data-collected-and-how-tooopt-out-of-it"></a>Datos de telemetría recopilados y cómo tooopt fuera de ella
De forma predeterminada, el producto de Hola recopila telemetría en hello Service Fabric uso tooimprove Hola del producto. Hola analizador de procedimientos recomendados que se ejecuta como parte del programa de instalación de hello comprueba si hay conectividad demasiado[https://vortex.data.microsoft.com/collect/v1](https://vortex.data.microsoft.com/collect/v1). Si no está accesible, se produce un error en el programa de instalación de Hola a menos que rechazar telemetría.

1. canalización de telemetría Hello intenta hello tooupload después de datos demasiado[https://vortex.data.microsoft.com/collect/v1](https://vortex.data.microsoft.com/collect/v1) una vez al día. Es una carga de mejor esfuerzo y no tiene ningún efecto en la funcionalidad de clúster de Hola. telemetría Hola solo se envía desde el nodo de Hola que se ejecuta Hola principal del Administrador de conmutación por error. Ningún otro nodo envía telemetría.
2. telemetría Hola consta de siguiente hello:

* Número de servicios
* Número de ServiceTypes
* Número de aplicaciones
* Número de ApplicationUpgrades
* Número de FailoverUnits
* Número de InBuildFailoverUnits
* Número de UnhealthyFailoverUnits
* Número de réplicas
* Número de InBuildReplicas
* Número de StandByReplicas
* Número de OfflineReplicas
* CommonQueueLength
* QueryQueueLength
* FailoverUnitQueueLength
* CommitQueueLength
* Número de nodos
* IsContextComplete: True/False
* ClusterId: se trata de un GUID generado aleatoriamente para cada clúster
* ServiceFabricVersion
* Dirección IP de máquina virtual de Hola o una máquina de qué Hola se carga la telemetría

telemetría toodisable, agregue la Hola siguiente demasiado*propiedades* en la configuración del clúster: *enableTelemetry: false*.

<a id="previewfeatures" name="previewfeatures_anchor"></a>

## <a name="preview-features-included-in-this-package"></a>Características de versión preliminar incluidas en este paquete
Ninguno.


> [!NOTE]
> A partir de hello nueva [versión de GA de clúster de hello independiente para Windows Server (versión 5.3.204.x)](https://azure.microsoft.com/blog/azure-service-fabric-for-windows-server-now-ga/), puede actualizar las versiones de toofuture de clúster, manual o automáticamente. Consulte demasiado[actualizar una versión independiente del clúster de Service Fabric](service-fabric-cluster-upgrade-windows-server.md) documento para obtener más información.
> 
> 

## <a name="next-steps"></a>Pasos siguientes
* [Implementación y eliminación de aplicaciones con PowerShell](service-fabric-deploy-remove-applications.md)
* [Opciones de configuración de clústeres de Windows independientes](service-fabric-cluster-manifest.md)
* [Agregar o quitar el clúster de Service Fabric de nodos tooa independiente](service-fabric-cluster-windows-server-add-remove-nodes.md)
* [Actualización de nodos de un clúster de Service Fabric independiente](service-fabric-cluster-upgrade-windows-server.md)
* [Creación de un clúster de Service Fabric independiente con máquinas virtuales de Azure con Windows](service-fabric-cluster-creation-with-windows-azure-vms.md)
* [Proteger un clúster independiente en Windows mediante la seguridad de Windows](service-fabric-windows-cluster-windows-security.md)
* [Protección de un clúster de Windows independiente mediante certificados](service-fabric-windows-cluster-x509-security.md)

<!--Image references-->
[Trusted Zone]: ./media/service-fabric-cluster-creation-for-windows-server/TrustedZone.png
