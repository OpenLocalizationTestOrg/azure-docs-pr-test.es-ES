---
title: "aaaPrepare recursos de VMware para replicación tooAzure con Azure Site Recovery local | Documentos de Microsoft"
description: "Resume los pasos de Hola que necesita para la replicación de las cargas de trabajo que se ejecuta en máquinas virtuales VMware tooAzure storage"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 6aba0e89-ad7c-467e-9db2-cfb3bfe4c7d6
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 09d81f15f6ee764135a62f5555e458c55fa30048
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="step-6-prepare-on-premises-vmware-replication-tooazure"></a>Paso 6: Preparar tooAzure de replicación de VMware locales

Utilice instrucciones de hello en este toointeract de servidores de VMware de artículo tooprepare local con Azure Site Recovery y preparar las máquinas virtuales de VMWare para la instalación del programa Hola a servicio de movilidad. agente del servicio de movilidad de Hello debe instalarse en todas las máquinas virtuales de local que desea que tooreplicate tooAzure.

## <a name="prepare-for-automatic-discovery"></a>Preparación para la detección automática

Site Recovery detecta automáticamente las máquinas virtuales en ejecución en los hosts de vSphere ESXi (con o sin un servidor vCenter). Para la detección automática, servidores y las necesidades de recuperación de sitio un hosts tooaccess de cuenta:

1. toouse una cuenta dedicada, cree un rol (en el nivel de vCenter hello, con permisos de hello descritas en hello tabla siguiente. Asígnele un nombre como **Azure_Site_Recovery**.
2. A continuación, cree un usuario en el servidor de host/vCenter vSphere de Hola y asignar a Hola rol toohello usuario. Especifique esta cuenta de usuario durante la implementación de Site Recovery.


### <a name="vmware-account-permissions"></a>Permisos de cuenta de VMware

Recuperación del sitio necesita acceso tooVMware para tooautomatically de servidor de proceso de hello detectar máquinas virtuales y conmutación por error y conmutación por recuperación de máquinas virtuales.

- **Migrar**: si solo desea toomigrate tooAzure de máquinas virtuales VMware, sin nunca producen errores en ellos volver, puede usar una cuenta de VMware con un rol de solo lectura. Este rol puede ejecutar la conmutación por error, pero no puede apagar las máquinas de origen protegidas. Esto no es necesario para la migración.
- **Replicación/recuperación**: si desea que la cuenta de hello de toodeploy replicación completa (replicate, conmutación por error, conmutación por recuperación) debe ser capaz de toorun operaciones como la creación y eliminación de discos, encendido etcetera de máquinas virtuales.
- **Detección automática**: se requiere al menos una cuenta de solo lectura.


**Task** | **Cuenta/rol necesarios** | **Permisos** | **Detalles**
--- | --- | --- | ---
**El servidor de procesos detecta automáticamente máquinas virtuales de VMware** | Necesita al menos un usuario de solo lectura. | Objeto de centro de datos –> propagar tooChild objeto, rol = solo lectura | Usuario asignado a nivel de centro de datos y tiene acceso tooall Hola objetos en el centro de datos de Hola.<br/><br/> acceso toorestrict, asignar Hola **sin acceso** rol con hello **propagar toochild** objeto, los objetos secundarios toohello (hosts de vSphere, almacenes de datos, las máquinas virtuales y redes).
**Conmutación por error** | Necesita al menos un usuario de solo lectura. | Objeto de centro de datos –> propagar tooChild objeto, rol = solo lectura | Usuario asignado a nivel de centro de datos y tiene acceso tooall Hola objetos en el centro de datos de Hola.<br/><br/> acceso toorestrict, asignar Hola **sin acceso** rol con hello **propagar toochild** toohello los objetos secundarios (hosts de vSphere, almacenes de datos, las máquinas virtuales y redes) del objeto.<br/><br/> Es útil para la migración, pero no para la replicación completa, la conmutación por error o la conmutación por recuperación.
**Conmutación por error y conmutación por recuperación** | Se recomienda crear un rol (Azure_Site_Recovery) con los permisos necesario de hello y, a continuación, asignar Hola rol tooa VMware usuario o grupo | Objeto de centro de datos –> propagar tooChild objeto, rol = Azure_Site_Recovery<br/><br/> Almacén de datos -> Asignar espacio, examinar almacén de datos, operaciones de archivo de bajo nivel, quitar archivo, actualizar archivos de máquina virtual<br/><br/> Red -> Asignación de red<br/><br/> Recursos -> grupo de VM asignar tooresource, migrar apagado de máquina virtual, migrar encendidos VM<br/><br/> Tareas -> Crear tarea, actualizar tarea<br/><br/> Máquina virtual -> Configuración<br/><br/> Máquina virtual -> Interactuar -> Responder a pregunta, conexión de dispositivos, configurar soporte de CD, Configurar soporte de disquete, apagar, encender, instalación de herramientas de VMware<br/><br/> Máquina virtual -> Inventario -> Crear, registrar, anular registro<br/><br/> Máquina virtual -> Aprovisionamiento -> Permitir descarga de máquina virtual, permitir carga de archivos de máquina virtual<br/><br/> Máquina virtual -> Instantáneas -> Quitar instantáneas | Usuario asignado a nivel de centro de datos y tiene acceso tooall Hola objetos en el centro de datos de Hola.<br/><br/> acceso toorestrict, asignar Hola **sin acceso** rol con hello **propagar toochild** objeto, los objetos secundarios toohello (hosts de vSphere, almacenes de datos, las máquinas virtuales y redes).


## <a name="prepare-for-push-installation-of-hello-mobility-service"></a>Preparar para la instalación por inserción del servicio de movilidad de Hola

servicio de movilidad de Hello debe estar instalado en todas las máquinas virtuales que desee tooreplicate. Hay una serie de formas tooinstall Hola servicio, incluida la instalación manual, la instalación de inserción Hola recuperación del sitio del servidor de procesos y la instalación mediante métodos como System Center Configuration Manager.

Si desea que la instalación de inserción toouse, deberá tooprepare una cuenta que Site Recovery puede usar tooaccess Hola máquina virtual.

- Puede usar una cuenta local o de dominio.
- Para Windows, si no usa una cuenta de dominio, debe toodisable control de acceso de usuarios remotos en el equipo local de Hola. toodo, Hola registrar con **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System**, agregar una entrada DWORD hello **LocalAccountTokenFilterPolicy**, con un valor de 1.
- Si desea que entrada de registro de hello tooadd de Windows desde una CLI, escriba:``REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1.``
- Para Linux, la cuenta de hello debe ser raíz Hola servidor de origen Linux.



## <a name="next-steps"></a>Pasos siguientes

Vaya demasiado[paso 7: crear un almacén](vmware-walkthrough-create-vault.md)
