---
title: " Administración de un servidor VMware vCenter en Azure Site Recovery | Microsoft Docs"
description: "En este artículo se describe como agregar y administrar VMware vCenter en Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: AnoopVasudavan
manager: gauravd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: backup-recovery
ms.date: 06/29/2017
ms.author: anoopkv
ms.openlocfilehash: 5be995f137d0c0efaf3050b5366a107098cae15a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-vmware-vcenter-server-in-azure-site-recovery"></a>Administración de VMware vCenter Server en Azure Site Recovery
Este artículo describe Hola varias operaciones de recuperación del sitio que se pueden realizar en un VMware vCenter.

## <a name="prerequisites"></a>Requisitos previos

**Compatibilidad con un host de VMware vCenter y VMware vSphere ESX** | **Detalles** |
|--- | --- |
|**Servidores de VMware locales** | Uno o más servidores de VMware vSphere, con 6.0, 5.5 o 5.1 y las últimas actualizaciones. Servidores deben ubicarse en hello misma red que el servidor de configuración de hello (o servidor de procesos independiente).<br/><br/> Se recomienda un vCenter toomanage Servers, ejecuta 6.0 o 5.5 con las actualizaciones más recientes de Hola. Solo se admiten las características que estén disponibles en 5.5 cuando se implementa la versión 6.0.|

## <a name="prepare-an-account-for-automatic-discovery"></a>Preparación de una cuenta de detección automática
Recuperación del sitio necesita acceso tooVMware para tooautomatically de servidor de proceso de hello detectar máquinas virtuales y conmutación por error y conmutación por recuperación de máquinas virtuales.

* **Migrar**: si solo desea toomigrate tooAzure de máquinas virtuales de VMware, sin nunca producen errores en ellos atrás, puede usar una cuenta de VMware con un rol de solo lectura. Este rol puede ejecutar la conmutación por error, pero no puede apagar las máquinas de origen protegidas. Esto no es necesario para la migración.
* **Replicación/recuperación**: si desea que la cuenta de hello de toodeploy replicación completa (replicate, conmutación por error, conmutación por recuperación) debe ser capaz de toorun operaciones como la creación y eliminación de discos, encendiendo la máquina virtual.
* **Detección automática**: se requiere al menos una cuenta de solo lectura.


|**Tareas** | **Cuenta/rol necesarios** | **Permisos** | **Detalles**|
|--- | --- | --- | ---|
|**El servidor de procesos detecta automáticamente máquinas virtuales de VMware** | Necesita al menos un usuario de solo lectura. | Objeto de centro de datos –> propagar tooChild objeto, rol = solo lectura | Usuario asignado a nivel de centro de datos y tiene acceso tooall Hola objetos en el centro de datos de Hola.<br/><br/> acceso toorestrict, asignar Hola **sin acceso** rol con hello **propagar toochild** objeto, los objetos secundarios toohello (hosts de vSphere, almacenes de datos, máquinas virtuales y redes).|
|**Conmutación por error** | Necesita al menos un usuario de solo lectura. | Objeto de centro de datos –> propagar tooChild objeto, rol = solo lectura | Usuario asignado a nivel de centro de datos y tiene acceso tooall Hola objetos en el centro de datos de Hola.<br/><br/> acceso toorestrict, asignar Hola **sin acceso** rol con hello **propagar toochild** toohello los objetos secundarios (hosts de vSphere, almacenes de datos, máquinas virtuales y redes) del objeto.<br/><br/> Es útil para la migración, pero no para la replicación completa, la conmutación por error o la conmutación por recuperación.|
|**Conmutación por error y conmutación por recuperación** | Se recomienda crear un rol (AzureSiteRecoveryRole) con los permisos necesario de hello y, a continuación, asignar Hola rol tooa VMware usuario o grupo | Objeto de centro de datos –> propagar tooChild objeto, rol = AzureSiteRecoveryRole<br/><br/> Almacén de datos -> Asignar espacio, examinar almacén de datos, operaciones de archivo de bajo nivel, quitar archivo, actualizar archivos de máquina virtual<br/><br/> Red -> Asignación de red<br/><br/> Recursos -> grupo de VM asignar tooresource, migrar apagado de máquina virtual, migrar encendidos VM<br/><br/> Tareas -> Crear tarea, actualizar tarea<br/><br/> Máquina virtual -> Configuración<br/><br/> Máquina virtual -> Interactuar -> Responder a pregunta, conexión de dispositivos, configurar soporte de CD, Configurar soporte de disquete, apagar, encender, instalación de herramientas de VMware<br/><br/> Máquina virtual -> Inventario -> Crear, registrar, anular registro<br/><br/> Máquina virtual -> Aprovisionamiento -> Permitir descarga de máquina virtual, permitir carga de archivos de máquina virtual<br/><br/> Máquina virtual -> Instantáneas -> Quitar instantáneas | Usuario asignado a nivel de centro de datos y tiene acceso tooall Hola objetos en el centro de datos de Hola.<br/><br/> acceso toorestrict, asignar Hola **sin acceso** rol con hello **propagar toochild** objeto, los objetos secundarios toohello (hosts de vSphere, almacenes de datos, máquinas virtuales y redes).|

## <a name="create-an-account-tooconnect-toovmware-vcenter-server-vmware-vsphere-exsi-host"></a>Crear un servidor de cuenta tooconnect tooVMware vCenter o host de VMware vSphere EXSi
1. Inicio de sesión en hello Configuración servidor e inicie hello cspsconfigtool.exe mediante acceso directo de Hola se coloca en hello escritorio.
2. Haga clic en **agregar una cuenta de** en hello **administrar cuenta** ficha.

  ![add-account](./media/site-recovery-vmware-to-azure-manage-vcenter/addaccount.png)
3. Proporcionar detalles de la cuenta de hello y haga clic en Aceptar tooadd Hola cuenta. cuenta de Hello debe tener privilegios de hello enumerados en hello [preparar una cuenta para la detección automática](#prepare-an-account-for-automatic-discovery) sección.

  >[!NOTE]
  Se tarda unos 15 minutos para toobe de información de cuenta de hello que seguridad se sincronizó con el servicio de Site Recovery de Hola.


## <a name="associate-a-vmware-vcenter-vmware-vsphere-esx-host-add-vcenter"></a>Asociación de un host de VMware vCenter/VMware vSphere ESX (agregar vCenter)
* En Hola portal de Azure, vaya demasiado*YourRecoveryServicesVault* > **infraestructura del sitio de recuperación** > **servidores de configuración**  >  *ConfigurationServer*
* En la página de detalles del servidor de configuración de hello, haga clic en Hola + vCenter botón.

[!INCLUDE [site-recovery-add-vcenter](../../includes/site-recovery-add-vcenter.md)]

## <a name="modify-credentials-used-tooconnect-toohello-vcenter-server-vsphere-esxi-host"></a>Modificar las credenciales usadas tooconnect toohello vCenter server / vSphere ESXi host

1. Inicio de sesión en configuración de hello server e inicie cspsconfigtool.exe Hola
2. Haga clic en **agregar una cuenta de** en hello **administrar cuenta** ficha.

  ![add-account](./media/site-recovery-vmware-to-azure-manage-vcenter/addaccount.png)
3. Proporcione detalles de cuenta nueva de Hola y haga clic en Aceptar tooadd Hola cuenta. cuenta de Hello debe tener privilegios de hello enumerados en hello [preparar una cuenta para la detección automática](#prepare-an-account-for-automatic-discovery) sección.
4. En Hola portal de Azure, vaya demasiado*YourRecoveryServicesVault* > **infraestructura del sitio de recuperación** > **servidores de configuración**  >  *ConfigurationServer*
5. En la página de detalles del servidor de configuración de hello, haga clic en hello **la actualización del servidor** botón.
6. Cuando se completa el trabajo de servidor de actualización de hello, seleccione Hola vCenter Server tooopen Hola vCenter página de resumen.
7. Seleccione Hola recién agregado cuenta Hola **cuenta de host de servidor/vSphere vCenter** campo y haga clic en hello **guardar** botón.

  ![modify-account](./media/site-recovery-vmware-to-azure-manage-vcenter/modify-vcente-creds.png)

## <a name="delete-a-vcenter-in-azure-site-recovery"></a>Eliminación de un servidor vCenter en Azure Site Recovery
1. En Hola portal de Azure, vaya demasiado*YourRecoveryServicesVault* > **infraestructura del sitio de recuperación** > **servidores de configuración**  >  *ConfigurationServer*
2. En la página de detalles del servidor de configuración de Hola Hola vCenter página Seleccionar servidor tooopen Hola vCenter resumen.
3. Haga clic en hello **eliminar** botón toodelete Hola vCenter

  ![delete-account](./media/site-recovery-vmware-to-azure-manage-vcenter/delete-vcenter.png)

> [!NOTE]
Si necesita toomodify Hola vCenter dirección IP o FQDN, detalles de puerto, a continuación, se necesita un servidor vCenter hello toodelete y agregarlo de nuevo.
