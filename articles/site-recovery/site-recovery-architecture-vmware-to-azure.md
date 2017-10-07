---
title: "¿aaaHow funciona VMware replicación tooAzure en Azure Site Recovery? | Microsoft Docs"
description: "Este artículo proporciona información general de componentes y arquitectura que se usa al replicar locales máquinas virtuales de VMware y servidores físicos tooAzure con hello servicio Azure Site Recovery"
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
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: vmware-walkthrough-architecture
ms.openlocfilehash: f0fb834f8b251640f97e4d0163b2b9e54de691e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-vmware-replication-tooazure-work-in-site-recovery"></a>¿Cómo funciona VMware replicación tooAzure en Site Recovery?

Este artículo describen los componentes de Hola y procesos que tienen lugar cuando se replican de forma local tooAzure de máquinas virtuales y servidores físicos de Windows o Linux, VMware mediante hello [Azure Site Recovery](site-recovery-overview.md) servicio.

Cuando se replica tooAzure de servidores física local, que utiliza la replicación también Hola mismo componentes y procesos como la replicación de VM de VMware, con estas diferencias:

- Puede usar un servidor físico para el servidor de configuración de hello, en lugar de una VM de VMware.
- Necesitará una infraestructura de VMware local para la conmutación por recuperación. No se producirá un error de máquina física tooa atrás.

Registrar los comentarios de la parte inferior de Hola de este artículo, o formular alguna pregunta en hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="architectural-components"></a>Componentes de la arquitectura

Hay una serie de componentes implicados al replicar las máquinas virtuales de VMware y servidores físicos tooAzure.

**Componente** | **Ubicación** | **Detalles**
--- | --- | ---
**Las tablas de Azure** | En Azure, necesitará una cuenta de Azure, una cuenta de Azure Storage y una red de Azure. | Los datos replicados se almacenan en la cuenta de almacenamiento de Hola y máquinas virtuales de Azure se crean con datos saludo replican Cuando se produce la conmutación por error desde el sitio local. Hola máquinas virtuales de Azure Conéctese toohello red virtual de Azure cuando se crean.
**Servidor de configuración** | Un único servidor de administración (VMWare VM) que se ejecuta todos los componentes locales de Hola que son necesarios para la implementación de hello, incluido el servidor de configuración de hello, el servidor de proceso de servidor de destino maestro local | componente de servidor de configuración de Hello coordina las comunicaciones entre local y Azure y administra la replicación de datos.
 **Servidor de proceso**:  | Se instala de forma predeterminada en el servidor de configuración de Hola. | Actúa como puerta de enlace de replicación. Recibe datos de replicación, optimiza con almacenamiento en caché, la compresión y cifrado y lo envía tooAzure almacenamiento.<br/><br/> servidor de procesos de Hello también controla la instalación de inserción de las máquinas de tooprotected de servicio de movilidad de Hola y realiza la detección automática de máquinas virtuales de VMware.<br/><br/> A medida que crece la implementación puede agregar toohandle de servidores adicionales proceso dedicado independiente aumentar volúmenes de tráfico de replicación.
 **Servidor de destino principal** | Se instala de forma predeterminada en el servidor de configuración local de Hola. | Controla los datos de replicación durante la conmutación por recuperación desde Azure.<br/><br/> Si los volúmenes de tráfico de la conmutación por recuperación son altos, puede implementar un servidor de destino maestro independiente para la conmutación por recuperación.
**Servidores de VMware** | Máquinas virtuales de VMware se hospedan en servidores de vSphere ESXi y se recomienda un vCenter hosts de servidor toomanage Hola. | Agregue el almacén de servicios de recuperación de tooyour de servidores de VMware.
**Máquinas replicadas** | servicio de movilidad de Hola se instalará en cada máquina virtual que desee tooreplicate de VMware. Se puede instalar manualmente en cada equipo o con una instalación de inserción Hola del servidor de procesos.

Obtenga información acerca de los requisitos previos de implementación de Hola y requisitos para cada uno de estos componentes en hello [matriz de compatibilidad](site-recovery-support-matrix-to-azure.md).

**Figura 1: VMware tooAzure componentes**

![Componentes](./media/site-recovery-components/arch-enhanced.png)

## <a name="replication-process"></a>Proceso de replicación

1. Configurar la implementación de hello, incluidos los componentes de Azure y un almacén de servicios de recuperación. En el almacén de hello especificar origen de replicación de Hola y de destino, configurar el servidor de configuración de hello, agregar servidores de VMware, cree una directiva de replicación, implementación el servicio de movilidad de hello, habilitan la replicación y ejecutan una prueba de conmutación por error.
2.  Máquinas empiece a replicar con arreglo a la directiva de replicación de hello y una copia inicial de datos de hello es almacenamiento tooAzure replicada.
4. La replicación de diferencias cambios tooAzure comienza después de que finalice la replicación inicial de Hola. Las marcas de revisión de una máquina se conservan en un archivo .hrl.
    - Replicación de máquinas comunican con el servidor de configuración de hello en el puerto HTTPS 443 entrante para la administración de replicación.
    - Replicación máquinas envían servidor de procesos de toohello de datos de replicación en el puerto HTTPS 9443 entrante (puede estar configurado).
    - servidor de configuración de Hello organiza la administración de la replicación con Azure en el puerto HTTPS 443 saliente.
    - servidor de procesos de Hello recibe datos de máquinas de origen, optimiza y cifra y lo envía tooAzure almacenamiento en el puerto 443 saliente.
    - Si habilita la coherencia entre varias VM, a continuación, equipos del grupo de replicación de hello comunican entre sí a través del puerto 20004. La implementación de varias máquinas virtuales se usa si agrupa varias máquinas en grupos de replicación que tienen puntos de recuperación coherentes con los bloqueos y coherentes con la aplicación cuando conmutan por error. Esto es útil si las máquinas ejecutan Hola la misma carga de trabajo y necesita toobe coherente.
5. Tráfico está replicada tooAzure extremos públicos de almacenamiento, en Hola internet. Como alternativa, puede usar el [emparejamiento público](../expressroute/expressroute-circuit-peerings.md#public-peering) de Azure ExpressRoute. No se admite la replicación del tráfico a través de una VPN de sitio a sitio desde un tooAzure de sitio local.

**Figura 2: VMware tooAzure replicación**

![Mejorada](./media/site-recovery-components/v2a-architecture-henry.png)

## <a name="failover-and-failback-process"></a>Proceso de conmutación por error y conmutación por recuperación

1. Después de comprobar que la conmutación por error funciona según lo previsto, puede ejecutar las conmutaciones por error no planeada tooAzure según sea necesario. No se admite la conmutación por error planeada.
2. Puede conmutar por error un único equipo, o crear [planes de recuperación](site-recovery-create-recovery-plans.md), toofail a varias máquinas virtuales.
3. Cuando se ejecuta una conmutación por error, las máquinas virtuales de la réplica se crean en Azure. Confirmar toostart una conmutación por error al acceder a cargas de trabajo de Hola de réplica de hello VM de Azure.
4. Cuando el sitio local principal esté disponible de nuevo, podrá realizar una conmutación por recuperación. Configurar una infraestructura de conmutación por recuperación, empiece a replicar máquina Hola de hello sitio secundario toohello principal y ejecutar una conmutación por error no planeada desde el sitio secundario de Hola. Tras confirmar esta conmutación por error, datos será local atrás y necesitará tooenable replicación tooAzure de nuevo. [Más información](site-recovery-failback-azure-to-vmware.md)

Hay varios requisitos para la conmutación por recuperación:


- **Servidor de procesos temporales en Azure**: si desea que toofail de Azure después de la conmutación por error, necesitará tooset una VM de Azure configurado como un servidor de procesos, replicación de toohandle de Azure. Dicha máquina virtual se puede eliminar cuando finalice la conmutación por recuperación.
- **Conexión VPN**: conmutación por recuperación necesitará una conexión VPN (o ExpressRoute de Azure) configurar de sitio local de hello Azure red toohello.
- **Servidor de destino maestro local independiente**: servidor de destino maestro local Hola controla la conmutación por recuperación. servidor de destino maestro Hola se instala de forma predeterminada en el servidor de administración de hello, pero si está experimentando problemas volver mayores volúmenes de tráfico debe configurar un servidor de destino maestro local independiente para este propósito.
- **Directiva de conmutación por recuperación**: tooreplicate atrás tooyour sitio local, deberá aplicar una directiva de conmutación por recuperación. Esta se crea automáticamente al crear la directiva de replicación.
- **Infraestructura de VMware**: debe realizar conmutación por recuperación tooan VM de VMware locales. Esto significa que necesita una infraestructura de VMware en local, incluso si replica tooAzure de servidores físicos locales.

**Figura 3: VMware y conmutación por recuperación física**

![Conmutación por recuperación](./media/site-recovery-components/enhanced-failback.png)


## <a name="next-steps"></a>Pasos siguientes

Hola de revisión [matriz de compatibilidad](site-recovery-support-matrix-to-azure.md)
