---
title: "arquitectura de hello aaaReview para tooAzure de replicación de servidor físico con Azure Site Recovery | Documentos de Microsoft"
description: "Este artículo proporciona información general de componentes y arquitectura que se usa cuando se replican local tooAzure de servidores físicos con hello servicio Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 09c9b136-35f5-465e-8d0f-f4c5d5d9f880
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 4f334c181fa6f0821adf978ebe9dbd7d36a3c753
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="step-1-review-hello-architecture-for-physical-server-replication-tooazure"></a>Paso 1: Revisar la arquitectura de Hola para tooAzure de replicación del servidor físico

Este artículo describe los componentes de Hola y procesos que se utilizan cuando se replica en local tooAzure de servidores físicos de Windows o Linux, mediante hello [Azure Site Recovery](site-recovery-overview.md) servicio.

Registrar los comentarios de la parte inferior de Hola de este artículo, o formular alguna pregunta en hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="architectural-components"></a>Componentes de la arquitectura

tabla de Hello resume componentes Hola que necesita.

**Componente** | **Requisito** | **Detalles**
--- | --- | ---
**Las tablas de Azure** | Se necesita una cuenta de Azure, una cuenta de Azure Storage y una red de Azure. | Los datos replicados se almacenan en la cuenta de almacenamiento de Hola y máquinas virtuales de Azure se crean con datos saludo replican Cuando se produce la conmutación por error. Máquinas virtuales de Azure conectan toohello red virtual de Azure cuando se crean.
**Servidor de configuración** | Un único servidor de administración (servidor físico o VM de VMware) que se ejecuta todos los Hola local componentes de Site Recovery en local. Estos incluyen un servidor de configuración, un servidor de procesos y un servidor de destino maestro. | componente de servidor de configuración de Hello coordina las comunicaciones entre local y Azure y administra la replicación de datos.
 **Servidor de proceso**  | Se instala de forma predeterminada en el servidor de configuración de Hola. | Actúa como puerta de enlace de replicación. Recibe datos de replicación, optimiza con almacenamiento en caché, la compresión y cifrado y lo envía tooAzure almacenamiento.<br/><br/> servidor de procesos de Hello también controla la instalación de inserción de las máquinas de tooprotected de servicio de movilidad de Hola.<br/><br/> Puede agregar servidores de proceso dedicado independiente adicionales, toohandle aumentar volúmenes de tráfico de replicación.
 **Servidor de destino principal** | Se instala de forma predeterminada en el servidor de configuración local de Hola. | Controla los datos de replicación durante la conmutación por recuperación desde Azure.<br/><br/> Si los volúmenes de tráfico de la conmutación por recuperación son altos, puede implementar un servidor de destino maestro independiente para la conmutación por recuperación.
**Servidores replicados** | Hello componente del servicio de movilidad está instalado en cada servidor de Windows/Linux desea tooreplicate. Se puede instalar manualmente en cada equipo o con una instalación de inserción Hola del servidor de procesos.
**Conmutación por recuperación** | Para la conmutación por recuperación se requiere una infraestructura de VMware. No se producirá un error de servidor físico de back-tooa.


**Figura 1: TooAzure físico componentes**

![Componentes](./media/physical-walkthrough-architecture/arch-enhanced.png)

## <a name="replication-process"></a>Proceso de replicación

1. Configurar la implementación de hello, incluidos los componentes de Azure y local. En el almacén de servicios de recuperación de hello, especificar origen de replicación de Hola y de destino, configurar el servidor de configuración de hello, crear una directiva de replicación, implementación el servicio de movilidad de hello, habilitan la replicación y ejecutan una prueba de conmutación por error.
2.  Replicar máquinas con arreglo a la directiva de replicación de hello y una copia inicial de datos de hello es almacenamiento tooAzure replicada.
4. Una vez finalizada la replicación inicial, comienza la replicación de diferencias cambios tooAzure. Las marcas de revisión de una máquina se conservan en un archivo .hrl.
    - Replicación de máquinas comunican con el servidor de configuración de hello en el puerto HTTPS 443 entrante para la administración de replicación.
    - Replicación máquinas envían servidor de procesos de toohello de datos de replicación en el puerto HTTPS 9443 entrante (pueden modificarse).
    - servidor de configuración de Hello organiza la administración de la replicación con Azure en el puerto HTTPS 443 saliente.
    - servidor de procesos de Hello recibe datos de máquinas de origen, optimiza y cifra y lo envía tooAzure almacenamiento en el puerto 443 saliente.
    - Si habilita la coherencia entre varias VM, a continuación, equipos del grupo de replicación de hello comunican entre sí a través del puerto 20004. La implementación de varias máquinas virtuales se usa si agrupa varias máquinas en grupos de replicación que tienen puntos de recuperación coherentes con los bloqueos y coherentes con la aplicación cuando conmutan por error. Esto es útil si las máquinas ejecutan Hola la misma carga de trabajo y necesita toobe coherente.
5. Tráfico está replicada tooAzure extremos públicos de almacenamiento, en Hola internet. Como alternativa, puede usar el [emparejamiento público](../expressroute/expressroute-circuit-peerings.md#public-peering) de Azure ExpressRoute. No se admite la replicación del tráfico a través de una VPN de sitio a sitio desde un tooAzure de sitio local.

**Figura 2: TooAzure físico replicación**

![Mejorada](./media/physical-walkthrough-architecture/v2a-architecture-henry.png)

## <a name="failover-and-failback-process"></a>Proceso de conmutación por error y conmutación por recuperación

Después de comprobar que la conmutación por error funciona según lo previsto, puede ejecutar las conmutaciones por error no planeada tooAzure según sea necesario. Cuando se ejecuta una conmutación por error, se crean máquinas virtuales de Azure a partir de los datos replicados. Luego, cuando el sitio local principal esté disponible de nuevo, podrá realizar una conmutación por recuperación. Observe lo siguiente:

- No se admite la conmutación por error planeada.
- Puede conmutar por error un único equipo, o crear [planes de recuperación](site-recovery-create-recovery-plans.md), toofail en varios equipos juntos.
- Confirmar toostart una conmutación por error al acceder a cargas de trabajo de Hola de réplica de hello VM de Azure.
- Al sitio primario de hello esté disponible de nuevo, replicar máquina Hola de sitio primario de hello toohello secundaria. A continuación, ejecute una conmutación por error no planeada desde el sitio secundario de Hola. Tras confirmar esta conmutación por error, datos será local atrás y necesitará tooenable replicación tooAzure de nuevo.

Entre los componentes de la conmutación por recuperación se incluyen:

- **Servidor de procesos temporales en Azure**: necesita tooset un tooact de máquina virtual de Azure como un servidor de procesos, la replicación de toohandle de Azure. Dicha máquina virtual se puede eliminar cuando finalice la conmutación por recuperación.
- **Conexión VPN**: necesita una conexión VPN (o ExpressRoute de Azure) de sitio local de hello Azure red toohello.
- **Servidor de destino maestro local independiente**: servidor de destino maestro local hello (que se instala de forma predeterminada en el servidor de configuración de hello) controla la conmutación por recuperación. Si se realiza la conmutación por recuperación en grandes volúmenes de tráfico, debe configurar un servidor de destino maestro local independiente para este propósito.
- **Directiva de conmutación por recuperación**: necesita una directiva de conmutación por recuperación. Esta se crea automáticamente al crear la directiva de replicación.
- **Infraestructura de VMware**: debe realizar conmutación por recuperación tooan VM de VMware locales. Esto significa que necesita una infraestructura de VMware en local, incluso si replica tooAzure de servidores físicos locales.

**Ilustración 3: Conmutación por recuperación de servidor físico**

![Conmutación por recuperación](./media/physical-walkthrough-architecture/enhanced-failback.png)


## <a name="next-steps"></a>Pasos siguientes

Vaya demasiado[paso 2: comprobar los requisitos previos y limitaciones](physical-walkthrough-prerequisites.md)
