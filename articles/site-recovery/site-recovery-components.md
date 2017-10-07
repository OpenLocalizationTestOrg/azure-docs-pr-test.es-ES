---
title: "¿aaaHow funciona de la recuperación del sitio? | Microsoft Docs"
description: "Este artículo proporciona información general sobre la arquitectura de Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: c413efcd-d750-4b22-b34b-15bcaa03934a
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/14/2017
ms.author: raynew
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: site-recovery-azure-to-azure-architecture
ms.openlocfilehash: ff1580d0fe294148dc0c621728491e6119c3048a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-azure-site-recovery-work-for-on-premises-infrastructure"></a>Funcionamiento de Azure Site Recovery en una infraestructura local

> [!div class="op_single_selector"]
> * [Replicación de máquinas virtuales de Azure](site-recovery-azure-to-azure-architecture.md)
> * [Replicación de máquinas locales](site-recovery-components.md)

Este artículo describe la arquitectura subyacente de hello [Azure Site Recovery](site-recovery-overview.md) servicios y los componentes de Hola que facilitan el trabajan para la replicación de las cargas de trabajo de tooAzure local.

Registrar cualquier comentario a la parte inferior de este artículo, o en Hola de hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="replicate-tooazure"></a>Replicar tooAzure

Puede replicar y proteger siguiente de hello en tooAzure de infraestructura local:

- **VMware**: máquinas virtuales de VMware locales que se ejecutan en un [host compatible](site-recovery-support-matrix-to-azure.md#support-for-datacenter-management-servers). Puede replicar máquinas virtuales de VMware que se ejecutan en [sistemas operativos compatibles](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions).
- **Hyper-V**: máquinas virtuales de Hyper-V locales que se ejecutan en [hosts compatibles](site-recovery-support-matrix-to-azure.md#support-for-datacenter-management-servers).
- **Máquinas físicas**: servidores físicos locales que ejecutan Windows o Linux en [sistemas operativos compatibles](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions). Puede replicar máquinas virtuales de Hyper-V que ejecuten cualquier sistema operativo invitado [compatible con Hyper-V y Azure](https://technet.microsoft.com/en-us/windows-server-docs/compute/hyper-v/supported-windows-guest-operating-systems-for-hyper-v-on-windows).

## <a name="vmware-tooazure"></a>TooAzure de VMware

Esto es lo necesita para la replicación de máquinas virtuales VMware tooAzure.

Ámbito | Componente | Detalles
--- | --- | ---
**Servidor de configuración** | Un solo servidor de administración (máquina virtual de VMware) ejecuta todos los componentes locales (servidor de configuración, servidor de procesos y servidor de destino principal). | servidor de configuración de Hello coordina las comunicaciones entre local y Azure y administra la replicación de datos.
 **Servidor de proceso**:  | Se instala de forma predeterminada en el servidor de configuración de Hola. | Actúa como puerta de enlace de replicación. Recibe datos de replicación, optimiza con almacenamiento en caché, la compresión y cifrado y lo envía tooAzure almacenamiento.<br/><br/> servidor de procesos de Hello también controla la instalación de inserción de las máquinas de tooprotected de servicio de movilidad de Hola y realiza la detección automática de máquinas virtuales de VMware.<br/><br/> A medida que crece la implementación puede agregar toohandle de servidores adicionales proceso dedicado independiente aumentar volúmenes de tráfico de replicación.
 **Servidor de destino principal** | Se instala de forma predeterminada en el servidor de configuración local de Hola. | Controla los datos de replicación durante la conmutación por recuperación desde Azure.<br/><br/> Si los volúmenes de tráfico de la conmutación por recuperación son altos, puede implementar un servidor de destino maestro independiente para la conmutación por recuperación.
**Servidores de VMware** | Máquinas virtuales de VMware se hospedan en servidores de vSphere ESXi y se recomienda un vCenter hosts de servidor toomanage Hola. | Agregue el almacén de servicios de recuperación de tooyour de servidores de VMware.<br/><br/>
**Máquinas replicadas** | servicio de movilidad de Hola se instalará en cada máquina virtual que desee tooreplicate de VMware. Se puede instalar manualmente en cada equipo o con una instalación de inserción Hola del servidor de procesos.| -

**Figura 1: VMware tooAzure componentes**

![Componentes](./media/site-recovery-components/arch-enhanced.png)

### <a name="replication-process"></a>Proceso de replicación

1. Configurar la implementación de hello, incluidos los componentes de Azure y un almacén de servicios de recuperación. En el almacén de hello especificar origen de replicación de Hola y de destino, configurar el servidor de configuración de hello, agregar servidores de VMware, cree una directiva de replicación, implementación el servicio de movilidad de hello, habilitan la replicación y ejecutan una prueba de conmutación por error.
2.  Máquinas empiece a replicar con arreglo a la directiva de replicación de hello y una copia inicial de datos de hello es almacenamiento tooAzure replicada.
4. La replicación de diferencias cambios tooAzure comienza después de que finalice la replicación inicial de Hola. Las marcas de revisión de una máquina se conservan en un archivo .hrl.
    - Replicación de máquinas comunican con el servidor de configuración de hello en el puerto HTTPS 443 entrante para la administración de replicación.
    - Replicación máquinas envían servidor de procesos de toohello de datos de replicación en el puerto HTTPS 9443 entrante (puede estar configurado).
    - servidor de configuración de Hello organiza la administración de la replicación con Azure en el puerto HTTPS 443 saliente.
    - servidor de procesos de Hello recibe datos de máquinas de origen, optimiza y cifra y lo envía tooAzure almacenamiento en el puerto 443 saliente.
    - Si habilita la coherencia entre varias VM, a continuación, equipos del grupo de replicación de hello comunican entre sí a través del puerto 20004. La implementación de varias máquinas virtuales se usa si agrupa varias máquinas en grupos de replicación que tienen puntos de recuperación coherentes con los bloqueos y coherentes con la aplicación cuando conmutan por error. Esto es útil si las máquinas ejecutan Hola la misma carga de trabajo y necesita toobe coherente.
5. Tráfico está replicada tooAzure extremos públicos de almacenamiento, en Hola internet. Como alternativa, puede usar el [emparejamiento público](https://docs.microsoft.com/en-us/azure/expressroute/expressroute-circuit-peerings#public-peering) de Azure ExpressRoute. No se admite la replicación del tráfico a través de una VPN de sitio a sitio desde un tooAzure de sitio local.

**Figura 2: VMware tooAzure replicación**

![Mejorada](./media/site-recovery-components/v2a-architecture-henry.png)

### <a name="failover-and-failback"></a>Conmutación por error y conmutación por recuperación

1. Después de comprobar que la conmutación por error funciona según lo previsto, puede ejecutar las conmutaciones por error no planeada tooAzure según sea necesario. No se admite la conmutación por error planeada.
2. Puede conmutar por error un único equipo, o crear [planes de recuperación](site-recovery-create-recovery-plans.md), toofail a varias máquinas virtuales.
3. Cuando se ejecuta una conmutación por error, las máquinas virtuales de la réplica se crean en Azure. Confirmar toostart una conmutación por error al acceder a cargas de trabajo de Hola de réplica de hello VM de Azure.
4. Cuando el sitio local principal esté disponible de nuevo, podrá realizar una conmutación por recuperación. Configurar una infraestructura de conmutación por recuperación, empiece a replicar máquina Hola de hello sitio secundario toohello principal y ejecutar una conmutación por error no planeada desde el sitio secundario de Hola. Tras confirmar esta conmutación por error, datos será local atrás y necesitará tooenable replicación tooAzure de nuevo. [Más información](site-recovery-failback-azure-to-vmware.md)

**Figura 3: VMware y conmutación por recuperación física**

![Conmutación por recuperación](./media/site-recovery-components/enhanced-failback.png)

## <a name="physical-tooazure"></a>TooAzure físico

Cuando se replica tooAzure de servidores física local, que utiliza la replicación también Hola mismo componentes y procesos como [tooAzure VMware](#vmware-replication-to-azure), pero tenga en cuenta estas diferencias:

- Puede usar un servidor físico para el servidor de configuración de hello, en lugar de una VM de VMware
- Necesitará una infraestructura de VMware local para la conmutación por recuperación. No se producirá un error de máquina física tooa atrás.

## <a name="hyper-v-tooazure"></a>TooAzure de Hyper-V

### <a name="replication-process"></a>Proceso de replicación

1. Configurar Hola componentes de Azure. Se recomienda que configure las cuentas de almacenamiento y de red antes de comenzar la implementación de Site Recovery.
2. Cree un almacén de servicios de replicación para Site Recovery y configure el almacén, incluyendo:
    - Configuración de origen y destino. Si no está administrando hosts de Hyper-V en una nube VMM, para el destino de hello crea un contenedor de sitio de Hyper-V y agregar tooit de hosts de Hyper-V. Si los hosts de Hyper-V se administran en VMM, origen de hello es nube de VMM Hola. destino de Hello es Azure.
    - Instalación de hello proveedor de Azure Site Recovery y el agente de servicios de recuperación de Microsoft Azure Hola. Si tienes Hola VMM se instalará en el mismo proveedor y Hola agente en cada host de Hyper-V. Si no dispone de VMM, Hola proveedor y agente se instalan en cada host.
    - Crear una directiva de replicación de sitio de Hyper-V de Hola o de nube de VMM. Directiva de Hello es máquinas virtuales de tooall aplicado ubicadas en hosts en el sitio de Hola o en la nube.
    - Habilite la replicación de máquinas virtuales de Hyper-V. Se produce la replicación inicial según la configuración de directiva de replicación de Hola.
4. Se realiza el seguimiento de cambios de datos y la replicación de diferencias cambios tooAzure comienza después de que finalice la replicación inicial de Hola. Las marcas de revisión de un elemento se conservan en un archivo .hrl.
5. Ejecutar un toomake de conmutación por error de prueba seguro de que todo funciona.

### <a name="failover-and-failback-process"></a>Proceso de conmutación por error y conmutación por recuperación

1. Puede ejecutar planeada o no planeada [conmutación por error](site-recovery-failover.md) de tooAzure de máquinas virtuales de Hyper-V local. Si se ejecuta una conmutación por error planeada, las máquinas virtuales de origen se apagan tooensure sin pérdida de datos.
2. Puede conmutar por error un único equipo, o crear [planes de recuperación](site-recovery-create-recovery-plans.md) tooorchestrate conmutación por error de varias máquinas.
4. Después de ejecutar Hola conmutación por error, debe ser hello toosee capaz de crear máquinas virtuales de réplica en Azure. Puede asignar una toohello de dirección IP virtual pública si es necesario.
5. A continuación, confirma toostart de conmutación por error de hello obtiene acceso a cargas de trabajo de Hola desde réplica Hola VM de Azure.
6. Cuando el sitio local principal esté disponible de nuevo, podrá realizar una [conmutación por recuperación](site-recovery-failback-from-azure-to-hyper-v.md). Iniciar una conmutación por error planeada desde Azure toohello de sitio primario. Para una conmutación por error planeada, puede toofailback seleccione toohello misma máquina virtual o tooan una ubicación alternativa y sincronizar no cambios entre Azure y local, tooensure pérdida de datos. Cuando las máquinas virtuales se crean en local, confirmar Hola conmutación por error.

**Figura 4: Replicación de tooAzure del sitio de Hyper-V**

![Componentes](./media/site-recovery-components/arch-onprem-azure-hypervsite.png)

**Figura 5: Hyper-V en la replicación de tooAzure de nubes VMM**

![Componentes](./media/site-recovery-components/arch-onprem-onprem-azure-vmm.png)


## <a name="replicate-tooa-secondary-site"></a>Replicar tooa de sitio secundario

Puede replicar hello tooyour secundaria sitio siguiente:

- **VMware**: máquinas virtuales de VMware locales que se ejecutan en un [host compatible](site-recovery-support-matrix-to-sec-site.md#on-premises-servers). Puede replicar máquinas virtuales de VMware que se ejecutan en [sistemas operativos compatibles](site-recovery-support-matrix-to-sec-site.md#support-for-replicated-machine-os-versions).
- **Máquinas físicas**: servidores físicos locales que ejecutan Windows o Linux en [sistemas operativos compatibles](site-recovery-support-matrix-to-sec-site.md#support-for-replicated-machine-os-versions).
- **Hyper-V**: máquinas virtuales de Hyper-V locales que se ejecutan en [hosts de Hyper-V compatibles](site-recovery-support-matrix-to-sec-site.md#on-premises-servers) administrados en nubes de VMM y [hosts compatibles](site-recovery-support-matrix-to-azure.md#support-for-datacenter-management-servers). Puede replicar máquinas virtuales de Hyper-V que ejecuten cualquier sistema operativo invitado [compatible con Hyper-V y Azure](https://technet.microsoft.com/en-us/windows-server-docs/compute/hyper-v/supported-windows-guest-operating-systems-for-hyper-v-on-windows).


## <a name="vmwarephysical-tooa-secondary-site"></a>Sitio secundario tooa físicos/VMware

Replicar máquinas virtuales de VMware o sitio secundario de servidores físicos tooa con InMage Scout.

### <a name="components"></a>Componentes

**Ámbito** | **Componente** | **Detalles**
--- | --- | ---
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

**Figura 6: VMware tooVMware replicación**

![TooVMware de VMware](./media/site-recovery-components/vmware-to-vmware.png)



## <a name="hyper-v-tooa-secondary-site"></a>Sitio secundario de Hyper-V tooa

Esto es lo necesita para la replicación de sitio secundario de máquinas virtuales de Hyper-V tooa.


**Ámbito** | **Componente** | **Detalles**
--- | --- | ---
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

**Figura 7: La replicación de tooVMM VMM**

![Local tooon-local](./media/site-recovery-components/arch-onprem-onprem.png)

### <a name="failover-and-failback"></a>Conmutación por error y conmutación por recuperación

1. Puede ejecutar una [conmutación por error](site-recovery-failover.md), planeada o no, entre sitios locales. Si se ejecuta una conmutación por error planeada, las máquinas virtuales de origen se apagan tooensure sin pérdida de datos.
2. Puede conmutar por error un único equipo, o crear [planes de recuperación](site-recovery-create-recovery-plans.md) tooorchestrate conmutación por error de varias máquinas.
4. Si lleva a cabo un sitio secundario de conmutación por error imprevista tooa, después de máquinas de conmutación por error de hello en la ubicación secundaria hello no están habilitadas para protección o la replicación. Si ha ejecutado una conmutación por error planeada, después de la conmutación por error de hello, máquinas en la ubicación secundaria Hola están protegidas.
5. A continuación, confirmar Hola conmutación por error toostart acceso a Hola cargas de trabajo de VM de réplica de Hola.
6. Cuando el sitio primario vuelve a estar disponible, iniciar la replicación inversa tooreplicate de toohello de sitio secundario de hello principal. La replicación inversa pone hello las máquinas virtuales en un estado protegido, pero Hola centro de datos secundaria sigue siendo ubicación activa Hola.
7. sitio primario de hello toomake en ubicación activa Hola de nuevo, que se inicie una conmutación por error planeada de tooprimary secundaria, seguido por otra replicación inversa.


## <a name="next-steps"></a>Pasos siguientes

- [Obtener más información](site-recovery-hyper-v-azure-architecture.md) acerca de flujo de trabajo de replicación de Hyper-V de Hola.
- [Comprobación de los requisitos previos](site-recovery-prereq.md)
