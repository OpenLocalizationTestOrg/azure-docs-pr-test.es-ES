---
title: "¿aaaHow funciona local machine replicación tooa local secundario sitio en Azure Site Recovery? | Microsoft Docs"
description: "Este artículo proporciona información general de componentes y arquitectura que se usa al replicar locales máquinas virtuales y el sitio secundario de tooa de servidores físicos con hello servicio Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: c413efcd-d750-4b22-b34b-15bcaa03934a
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/29/2017
ms.author: raynew
ms.openlocfilehash: 097a3f43446fec69ed7f9e0b7f11e8d11f41cc6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-on-premises-machine-replication-tooa-secondary-site-work-in-site-recovery"></a>¿Cómo equipo local la replicación tooa sitio secundario trabajo en Site Recovery?

Este artículo describen los componentes de Hola y procesos que tienen lugar cuando se replican de forma local máquinas virtuales y servidores físicos tooAzure, con hello [Azure Site Recovery](site-recovery-overview.md) servicio.

Puede replicar hello tooa local secundario sitio siguiente:
- Máquinas virtuales de Hyper-V locales en hosts independientes y clústeres de Hyper-V que se administran en nubes de System Center Virtual Machine Manager (VMM).
- Máquinas virtuales de VMware locales y servidores físicos de Windows y Linux. En este escenario, la replicación se administra con Scout.

Registrar cualquier comentario a la parte inferior de este artículo, o en Hola de hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="replicate-hyper-v-vms-tooa-secondary-on-premises-site"></a>Replicar sitio local secundario de máquinas virtuales de Hyper-V tooa


### <a name="architectural-components"></a>Componentes de la arquitectura

Esto es lo necesita para la replicación de sitio secundario de máquinas virtuales de Hyper-V tooa.

**Componente** | **Ubicación** | **Detalles**
--- | --- | ---
**Las tablas de Azure** | Necesita una cuenta de Microsoft. |
**Servidor VMM** | Se recomienda un servidor VMM en el sitio primario de hello y otro en el sitio secundario de Hola | Cada servidor VMM debe ser toohello conectado internet.<br/><br/> Cada servidor debe tener al menos una nube privada VMM, con el conjunto de perfiles de capacidad de Hyper-V de Hola.<br/><br/> Instale hello Azure Site Recovery Provider en servidor VMM de Hola. coordina Hello proveedor y organiza la replicación con hello servicio Site Recovery a través de Hola internet. Las comunicaciones entre el proveedor de Hola y de Azure son seguro y está cifrado.
**Servidor de Hyper-V** |  Uno o varios servidores Hyper-V host Hola principales y secundarias en nubes de VMM.<br/><br/> Servidores deben estar conectado toohello internet.<br/><br/> Datos se replican entre Hola principales y secundarios Hyper-V host servidores a través de LAN de Hola o VPN, con la autenticación Kerberos o certificados.  
**Máquinas virtuales de Hyper-V** | Si se encuentra en el servidor de host de Hyper-V de origen Hola. | servidor de host de origen de Hello debe tener al menos una máquina virtual que desea tooreplicate.

### <a name="replication-process"></a>Proceso de replicación

1. Configurar Hola cuenta de Azure.
2. Cree un almacén de servicios de replicación para Site Recovery y configure el almacén, incluyendo:

    - origen de replicación de Hola y de destino (sitios primarios y secundarios).
    - Instalación de hello proveedor de Azure Site Recovery y el agente de servicios de recuperación de Microsoft Azure Hola. Hola proveedor está instalado en servidores VMM y el agente de hello en cada host de Hyper-V.
    - Cree una directiva de replicación para la nube de VMM de origen. Directiva de Hello es aplicado tooall máquinas virtuales ubicadas en hosts en la nube de Hola.
    - Habilite la replicación de máquinas virtuales de Hyper-V. Se produce la replicación inicial según la configuración de directiva de replicación de Hola.
4. Se realiza el seguimiento de cambios de datos y replicación de diferencias cambia toobegins después de que finalice la replicación inicial de Hola. Las marcas de revisión de un elemento se conservan en un archivo .hrl.
5. Ejecutar un toomake de conmutación por error de prueba seguro de que todo funciona.

**Figura 1: La replicación de tooVMM VMM**

![Local tooon-local](./media/site-recovery-components/arch-onprem-onprem.png)

### <a name="failover-and-failback-process"></a>Proceso de conmutación por error y conmutación por recuperación

1. Puede ejecutar una [conmutación por error](site-recovery-failover.md), planeada o no, entre sitios locales. Si se ejecuta una conmutación por error planeada, las máquinas virtuales de origen se apagan tooensure sin pérdida de datos.
2. Puede conmutar por error un único equipo, o crear [planes de recuperación](site-recovery-create-recovery-plans.md) tooorchestrate conmutación por error de varias máquinas.
4. Si lleva a cabo un sitio secundario de conmutación por error imprevista tooa, después de máquinas de conmutación por error de hello en la ubicación secundaria hello no están habilitadas para protección o la replicación. Si ha ejecutado una conmutación por error planeada, después de la conmutación por error de hello, máquinas en la ubicación secundaria Hola están protegidas.
5. A continuación, confirmar Hola conmutación por error toostart acceso a Hola cargas de trabajo de VM de réplica de Hola.
6. Cuando el sitio primario vuelve a estar disponible, iniciar la replicación inversa tooreplicate de toohello de sitio secundario de hello principal. La replicación inversa pone hello las máquinas virtuales en un estado protegido, pero Hola centro de datos secundaria sigue siendo ubicación activa Hola.
7. sitio primario de hello toomake en ubicación activa Hola de nuevo, que se inicie una conmutación por error planeada de tooprimary secundaria, seguido por otra replicación inversa.




## <a name="replicate-vmware-vmsphysical-servers-tooa-secondary-site"></a>Replicar sitio secundario del tooa de servidores físicos o máquinas virtuales de VMware

Replicar máquinas virtuales de VMware o un sitio secundario del tooa servidores físicos con InMage Scout, mediante estos componentes arquitectónicos:


### <a name="architectural-components"></a>Componentes de la arquitectura

**Componente** | **Ubicación** | **Detalles**
--- | --- | ---
**Las tablas de Azure** | InMage Scout. | tooobtain InMage Scout necesita una suscripción a Azure.<br/><br/> Después de crear un almacén de servicios de recuperación, InMage Scout de descargar e instalar tooset de las actualizaciones más reciente de Hola la implementación de Hola.
**Servidor de proceso** | Ubicado en el sitio principal. | Implementar Hola proceso servidor toohandle almacenamiento en caché, la compresión y la optimización de datos.<br/><br/> También controla la instalación de inserción de hello toomachines agente unificado que desee tooprotect.
**Servidor de configuración** | Ubicado en el sitio secundario. | administra el servidor de configuración de Hello, configurar y supervisar la implementación, ya sea mediante el sitio Web de administración de Hola o la consola de vContinuum Hola.
**Servidor de vContinuum** | Opcional. Instalado en hello misma ubicación que el servidor de configuración de Hola. | Proporciona una consola para administrar y supervisar su entorno protegido.
**Servidor de destino principal** | Ubicado en el sitio secundario de Hola | servidor de destino maestro Hello contiene los datos replicados. Recibe datos de servidor de procesos de hello, crea una máquina de réplica en el sitio secundario de Hola y contiene puntos de retención de datos de Hola.<br/><br/> número de Hola de servidores de destino maestro que se necesitan depende de número de Hola de máquinas que se va a proteger.<br/><br/> Si desea que el sitio primario de toofail toohello atrás, necesitará un servidor de destino maestro se demasiado. Hello unificado agente está instalado en este servidor.
**Servidor de VMware ESX/ESXi y vCenter** |  Las máquinas virtuales se hospedan en hosts ESX/ESXi. Los hosts se administran con un servidor vCenter. | Es necesario un tooreplicate de infraestructura de VMware máquinas virtuales VMware.
**Máquinas virtuales y servidores físicos** |  Unified agente instalado en máquinas virtuales de VMware y servidores físicos que desee tooreplicate. | agente de Hello actúa como un proveedor de comunicación entre todos los componentes de Hola de.


### <a name="replication-process"></a>Proceso de replicación

1. Puedes configuración servidores de componentes de hello en cada sitio (configuración, proceso de destino maestro) e instalar Hola unificado agente en equipos que desea tooreplicate.
2. Después de la replicación inicial, el agente de hello en cada equipo envía servidor de procesos de toohello de cambios de replicación de diferencias.
3. servidor de procesos de Hello optimiza datos hello y transfiere el servidor de destino maestro toohello en el sitio secundario de Hola. servidor de configuración de Hello administra el proceso de replicación de Hola.

**Figura 2: VMware tooVMware replicación**

![TooVMware de VMware](./media/site-recovery-components/vmware-to-vmware.png)


## <a name="next-steps"></a>Pasos siguientes

Hola de revisión [matriz de compatibilidad](site-recovery-support-matrix-to-sec-site.md)
