---
title: "Preparación de la implementación de clúster de Service Fabric independientes aaaAzure | Documentos de Microsoft"
description: "Documentación relacionada con el entorno de hello toopreparing y crear configuración de clúster de hello, toobe considera toodeploying anterior un clúster diseñado para controlar una carga de trabajo de producción."
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
ms.date: 1/17/2017
ms.author: maburlik;chackdan
ms.openlocfilehash: e503c61a64b408af3f22bd75ab02f1c34ac9f380
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
<a id="preparemachines"></a>

## <a name="plan-and-prepare-your-service-fabric-standalone-cluster-deployment"></a>Planeamiento y preparación del desarrollo de un clúster independiente de Service Fabric
Realizar Hola siguiendo los pasos antes de crear el clúster.

### <a name="step-1-plan-your-cluster-infrastructure"></a>Paso 1: Planear la infraestructura de clúster
Está a punto toocreate un clúster de Service Fabric en los equipos que usted es el propietario, por lo que puede decidir qué tipos de errores que desee Hola toosurvive de clúster. Por ejemplo, ¿necesita líneas de alimentación independientes o si las conexiones a Internet suministrado máquinas toothese? Además, considere la posibilidad de seguridad física de Hola de estas máquinas. ¿Donde se encuentran las máquinas de Hola y quién debe toothem de acceso? Después de tomar estas decisiones, lógicamente puede asignar Hola máquinas toohello distintos dominios de error (consulte el paso 4). planeación para clústeres de producción de la infraestructura de Hello es más complicada que para los clústeres de prueba.

### <a name="step-2-prepare-hello-machines-toomeet-hello-prerequisites"></a>Paso 2: Preparar Hola máquinas toomeet requisitos previos de Hola
Requisitos previos para cada equipo que desea tooadd toohello clúster:

* Se recomiendan como mínimo 16 GB de RAM.
* Se recomiendan 40 GB de espacio disponible en disco como mínimo.
* Se recomienda una CPU de cuatro núcleos o más.
* Red segura de conectividad tooa o redes para todas las máquinas.
* Windows Server 2012 R2 o Windows Server 2016. 
* [.NET Framework 4.5.1 o posterior](https://www.microsoft.com/download/details.aspx?id=40773)(instalación completa).
* [Windows PowerShell 3.0](https://msdn.microsoft.com/powershell/scripting/setup/installing-windows-powershell).
* Hola [RemoteRegistry servicio](https://technet.microsoft.com/library/cc754820) debe ejecutarse en todas las máquinas de Hola.

Hello implementar y configurar el clúster de hello el Administrador de clústeres debe tener [privilegios de administrador](https://social.technet.microsoft.com/wiki/contents/articles/13436.windows-server-2012-how-to-add-an-account-to-a-local-administrator-group.aspx) en cada uno de los equipos de Hola. No se puede instalar Service Fabric en un controlador de dominio.

### <a name="step-3-determine-hello-initial-cluster-size"></a>Paso 3: Determinar el tamaño inicial del clúster de Hola
Cada nodo de un clúster de Service Fabric independiente tiene Hola Service Fabric en tiempo de ejecución implementa y es un miembro de clúster de Hola. En una implementación típica de producción, hay un nodo por cada instancia de sistema operativo (física o virtual). tamaño de clúster de Hello viene determinado por sus necesidades empresariales. Sin embargo, debe tener un tamaño mínimo de clúster de tres nodos (máquinas o máquinas virtuales).
Con fines de desarrollo, puede tener más de un nodo en una máquina determinada. En un entorno de producción, Service Fabric solo admite un nodo por máquina virtual o física.

### <a name="step-4-determine-hello-number-of-fault-domains-and-upgrade-domains"></a>Paso 4: Determinar el número de Hola de dominios de error y dominios de actualización
A *dominio de error* (FD) es una unidad física de error y es toohello directamente relacionados con la infraestructura física hello en centros de datos. Un dominio de error consta de componentes de hardware (equipos, conmutadores, redes, etc.) que comparten un único punto de error. Aunque no hay ninguna asignación 1:1 entre dominios de error y racks, en términos generales, cada bastidor puede considerarse un dominio de error. Al considerar nodos hello en el clúster, se recomienda encarecidamente que los nodos de Hola se distribuya entre al menos tres dominios de error.

Cuando se especifica FD en ClusterConfig.json, puede elegir nombre de Hola para cada FD. Service Fabric admite FD jerárquicos, así que puede reflejar la topología de infraestructura en ellos.  Por ejemplo, hello después FD es válida:

* "faultDomain": "fd:/Room1/Rack1/Machine1"
* "faultDomain": "fd:/FD1"
* "faultDomain": "fd:/Room1/Rack1/PDU1/M1"

Un *dominio de actualización* (UD) es una unidad lógica de nodos. Durante las actualizaciones de Service Fabric organiza (actualización de una aplicación o una actualización de clúster), todos los nodos de un UD se bajan actualización de hello tooperform mientras los nodos en otros ud permanecen disponibles tooserve solicitudes. Hello las actualizaciones de firmware realizan en los equipos no respetan ud, por lo que debe realizarlas uno equipos a la vez.

toothink de manera más sencilla de Hello acerca de estos conceptos es tooconsider FD como unidad de Hola de error no planeada y ud como unidad de Hola de mantenimiento planeado.

Cuando se especifica ud en ClusterConfig.json, puede elegir nombre de Hola para cada UD. Por ejemplo, hello siguiendo los nombres es válido:

* "upgradeDomain": "UD0"
* "upgradeDomain": "UD1A"
* "upgradeDomain": "DomainRed"
* "upgradeDomain": "Blue"

Para más información sobre los dominios de actualización y los dominios de error, vea [Descripción de un clúster de Service Fabric](service-fabric-cluster-resource-manager-cluster-description.md).

### <a name="step-5-download-hello-service-fabric-standalone-package-for-windows-server"></a>Paso 5: Descargar el paquete independiente de Service Fabric de Hola para Windows Server
[Descargar vínculo - paquete de independiente de Service Fabric - Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690) y descomprima el paquete de hello, cualquier implementación tooa de máquina que es no forma parte del clúster de Hola o tooone de máquinas de Hola que vayan a formar parte del clúster.

### <a name="step-6-modify-cluster-configuration"></a>Paso 6: Modificación de la configuración del clúster
toocreate un clúster independiente tiene toocreate independiente clúster ClusterConfig.json archivo de configuración, que describe la especificación de Hola de clúster de Hola. Puede basar el archivo de configuración de hello en plantillas de hello encontradas en hello siguiente vínculo. <br>
[Configuraciones de clúster independiente](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples)

Para obtener más información en las secciones de hello en este archivo, consulte [valores de configuración de clúster de Windows independiente](service-fabric-cluster-manifest.md).

Abrir uno de hello ClusterConfig.json archivos de paquete de hello descargado y modificar Hola después de la configuración:
| **Opciones de configuración.** | **Descripción** |
| --- | --- |
| **NodeTypes** |Tipos de nodos le permiten tooseparate los nodos del clúster en grupos distintos. Un clúster debe tener al menos un tipo NodeType. Todos los nodos de un grupo tienen Hola después características comunes: <br> **Nombre de** -éste es el nombre del tipo de nodo de Hola. <br>**Endpoint Ports** : diversos puntos de conexión (puertos) con nombre asociados a este tipo de nodo. Puede usar cualquier número de puerto que desea, siempre y cuando no están en conflicto con cualquier otra cosa en este manifiesto y ya no están en uso por cualquier otra aplicación que se ejecuta en la máquina de Hola/máquina virtual. <br> **Las propiedades de ubicación** -se describen las propiedades para este tipo de nodo que se usa como las restricciones de posición para los servicios del sistema Hola o los servicios. Estas propiedades son pares de clave y valor definidos por el usuario que proporcionan metadatos adicionales para un nodo determinado. Ejemplos de propiedades de nodo sería si el nodo de hello tiene una unidad de disco duro o tarjeta gráfica, número de Hola de ejes en su unidad de disco duro, núcleos y otras propiedades físicas. <br> **Capacidades** -capacidades de nodo definen nombre de Hola y la cantidad de un recurso concreto que un nodo concreto tiene disponibles para su consumo. Por ejemplo, un nodo puede definir que tenga capacidad para una métrica llamada "MemoryInMb" y 2048 MB de memoria disponible de forma predeterminada. Estas capacidades se usan en tooensure en tiempo de ejecución que los servicios que requieren una cantidad determinada de recursos se colocan en nodos de Hola que hayan necesarios dichos recursos disponibles en hello cantidades.<br>**IsPrimary** : si tiene más de uno NodeType definido Compruebe que sólo uno es tooprimary con el valor de Hola *true*, que es donde hello sistema de servicios de ejecución. Todos los demás tipos de nodo se deben establecer el valor de toohello *false* |
| **Nodos** |Estos son los detalles de Hola para cada uno de los nodos de Hola que forman parte del clúster de hello (tipo de nodo, nombre de nodo, dirección IP, dominio de error y dominio de actualización del nodo de hello). máquinas de Hello desea hello toobe de clúster creado en toobe necesidad que se muestran con sus direcciones IP. <br> Si usas hello se crea la misma dirección IP para todos los nodos de hello, a continuación, en un clúster de un solo cuadro, que puede utilizar para realizar pruebas. No use clústeres one-box para implementar cargas de trabajo de producción. |

Después de configuración de clúster de hello ha tenido todas las opciones configuradas toohello entorno, se puede probar en el entorno de clúster de hello (paso 7).

<a id="environmentsetup"></a>

### <a name="step-7-environment-setup"></a>Paso 7. Configuración del entorno

Cuando un administrador de clústeres configura un clúster de Service Fabric independiente, el entorno de hello es necesidades toobe prepararle Hola siguiendo criterios: <br>
1. usuario de Hello crear clúster Hola debe tener las máquinas de tooall de privilegios de seguridad de nivel de administrador que se muestran como nodos en el archivo de configuración del clúster de Hola.
2. Máquina de qué Hola se crea el clúster, así como los equipos cada nodo del clúster deben:
* Tener desinstalado el SDK de Service Fabric
* tener desinstalado el entorno de tiempo de ejecución de Service Fabric 
* Ha hello servicio Firewall de Windows (mpssvc) habilitado
* Ha habilitado el servicio de registro remoto (remoteregistry) Hola
* Tener habilitado el uso compartido de archivos (SMB)
* Tener abiertos los puertos necesarios, según los puertos de configuración del clúster
* Tener abiertos los puertos necesarios para Windows SMB y el servicio Registro remoto: 135, 137, 138, 139 y 445
* Tiene tooone de conectividad de red otro
3. Ninguna de las máquinas de nodo de clúster de hello debe ser un controlador de dominio.
4. Si Hola clúster toobe implementado es un clúster segura, validar requisitos previos están en colocar y están configurados correctamente en la configuración de Hola de seguridad necesarios Hola.
5. Si las máquinas del clúster hello no son accesibles desde internet, conjunto siguiente de Hola Hola clúster configuración:
* Deshabilite la telemetría: en *Propiedades*, establezca *"enableTelemetry" en false*
* Deshabilitar automática de descarga de la versión de Fabric & notificaciones de esa versión de clúster actual de hello está llegando al final del soporte técnico: en *propiedades* establecer *"fabricClusterAutoupgradeEnabled": false*
* O bien si el acceso a internet de red es limitados dominios enumerados toowhite, dominios Hola siguiente son necesarios para la actualización automática: download.microsoft.com go.microsoft.com

6. Establezca las exclusiones adecuadas del antivirus de Service Fabric:

| **Directorios excluidos del antivirus** |
| --- |
| Archivos de programa\Microsoft Service Fabric |
| FabricDataRoot (de la configuración del clúster) |
| FabricLogRoot (de la configuración del clúster) |

| **Procesos excluidos del antivirus** |
| --- |
| Fabric.exe |
| FabricHost.exe |
| FabricInstallerService.exe |
| FabricSetup.exe |
| FabricDeployer.exe |
| ImageBuilder.exe |
| FabricGateway.exe |
| FabricDCA.exe |
| FabricFAS.exe |
| FabricUOS.exe |
| FabricRM.exe |
| FileStoreService.exe |

### <a name="step-8-validate-environment-using-testconfiguration-script"></a>Paso 8. Validación del entorno mediante el script TestConfiguration
Hola TestConfiguration.ps1 script puede encontrarse en el paquete independiente de Hola. Es utiliza como un toovalidate de Best Practices Analyzer algunos de los criterios de hello anteriores y se deben usar como un toovalidate de comprobación de integridad si un clúster puede implementarse en un entorno determinado. Si se produce cualquier error, consulte la lista de toohello en [configuración del entorno](service-fabric-cluster-standalone-deployment-preparation.md) para solucionar el problema. 

Este script se puede ejecutar en cualquier equipo que tenga equipos Hola de tooall de acceso de administrador que se muestran como nodos en el archivo de configuración del clúster de Hola. máquina de Hola que este script se ejecuta en no tiene toobe parte del clúster de Hola.

```powershell
PS C:\temp\Microsoft.Azure.ServiceFabric.WindowsServer> .\TestConfiguration.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json
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

Actualmente este módulo de configuración de pruebas no valida la configuración de seguridad de Hola por lo que esto tiene toobe realiza de forma independiente.  

> [!NOTE]
> Estamos continuamente realizando mejoras toomake este módulo más sólido, por lo que si hay algún problema o falta el caso que cree no está asociada actualmente por TestConfiguration, háganoslo saber a través de nuestro [admiten canales](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-support).   
> 
> 

## <a name="next-steps"></a>Pasos siguientes
* [Creación de un clúster independiente con Windows Server](service-fabric-cluster-creation-for-windows-server.md)
