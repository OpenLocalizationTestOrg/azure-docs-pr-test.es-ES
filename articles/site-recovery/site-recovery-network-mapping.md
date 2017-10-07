---
title: "aaaPlan la asignación de red para la replicación de máquina virtual de Hyper-V con Site Recovery | Documentos de Microsoft"
description: "Configurar la asignación de red para la replicación de máquina virtual de Hyper-V desde un tooAzure de centro de datos local o sitio secundario de tooa."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: tysonn
ms.assetid: fcaa2f52-489d-4c1c-865f-9e78e000b351
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/23/2017
ms.author: raynew
ms.openlocfilehash: 86199b5840ea10fd33630bcc75d14340a49e01bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="plan-network-mapping-for-hyper-v-vm-replication-with-site-recovery"></a>Planear la asignación de red para la replicación de máquinas virtuales de Hyper-V con Site Recovery



En este artículo le ayuda a toounderstand y el plan para la red durante la replicación de máquinas virtuales de Hyper-V tooAzure, o un sitio secundario de tooa de asignación, el uso de hello [servicio Azure Site Recovery](site-recovery-overview.md).

Después de leer este artículo registrar los comentarios de la parte inferior de Hola de este artículo, o hacer preguntas técnicas en hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="network-mapping-for-replication-tooazure"></a>Asignación de red para la replicación tooAzure

Asignación de red se utiliza al replicar tooAzure de máquinas virtuales de Hyper-V (que se administren en VMM). La asignación de red se produce entre redes de máquinas virtuales en un servidor VMM de origen y redes de Azure de destino. Asignación Hola siguientes:

- **Conexión de red**: garantiza que replicada máquinas virtuales de Azure están conectados toohello de red asignadas. Todas las máquinas que conmutar por error en hello misma red puede conectarse tooeach otra, aunque conmutado por error en los planes de recuperación diferente.
- **Puerta de enlace de red**: si se configura una puerta de enlace de red en red Azure de destino de hello, las máquinas virtuales pueden conectarse máquinas virtuales de tooother local.

Observe lo siguiente:

- Asignar un origen de red de VM de VMM tooan red virtual de Azure.
- Después de la conmutación por error máquinas virtuales de Azure en hello red de origen será red virtual de destino asignada toohello conectado.
- Agregan de nuevas máquinas virtuales conectadas toohello red de VM de origen toohello asigna red de Azure cuando se produce la replicación.
- Si la red de destino de hello tiene varias subredes y una de estas subredes se Hola mismo nombre que la subred en la máquina virtual de origen de Hola se encuentra, máquina virtual de réplica de hello conecta toothat subred de destino después de la conmutación por error.
- Si no hay ninguna subred de destino con un nombre coincidente, máquina virtual de hello conecta toohello primera subred de red de Hola.


## <a name="network-mapping-for-replication-tooa-secondary-datacenter"></a>Asignación de red para el centro de datos de replicación tooa secundario

Asignación de red se utiliza al replicar el centro de datos secundario tooa de máquinas virtuales de Hyper-V (administrado en System Center Virtual Machine Manager (VMM)). La asignación de red se produce entre redes de máquinas virtuales en un servidor VMM de origen y redes de máquinas virtuales en un servidor VMM de destino. Asignación Hola siguientes:

- **Conexión de red**: redes de máquinas virtuales se conecta tooappropriate después de la conmutación por error. VM de réplica de Hello será toohello conectado red de destino que está asignada toohello red de origen.
- **Una ubicación óptima**: óptimamente lugares Hola máquinas virtuales de réplica en los servidores de host de Hyper-V. Máquinas virtuales de réplica se colocan en hosts que pueden asignar Hola de acceso a redes de máquinas virtuales.
- **Ninguna asignación de red**: si no configura la asignación de red, las máquinas virtuales de réplica no estará conectado tooany redes de máquinas virtuales después de la conmutación por error.

Observe lo siguiente:

- Asignación de red se puede configurar entre redes de VM en dos servidores VMM o en un único servidor VMM si administra dos sitios Hola mismo servidor.
- Cuando se configura correctamente la asignación y está habilitada la replicación, una máquina virtual en la ubicación principal Hola será red tooa conectado y se conectará su réplica en la ubicación de destino de hello tooits asigna la red.
-
- Si redes se ha configurado correctamente en VMM, al seleccionar una red de VM de destino durante la asignación de red, nubes de origen VMM de Hola que usan la red de VM de origen Hola se mostrarán junto con redes de VM de destino disponibles de hello en nubes de destino de Hola que sirven para protección.
- Si la red de destino de hello tiene varias subredes y una de dichas subredes tiene Hola mismo nombre como Hola subred en qué Hola máquina virtual de origen se encuentra, a continuación, Hola máquina virtual de réplica será toothat conectado subred de destino después de la conmutación por error. Si no hay ninguna subred de destino con un nombre coincidente, máquina virtual de hello estará conectado toohello primera subred de red de Hola.



### <a name="example"></a>Ejemplo

Este es un ejemplo tooillustrate este mecanismo. Vamos a utilizar una organización con dos ubicaciones en Nueva York y Chicago.

**Ubicación** | **Servidor VMM** | **Redes de máquinas virtuales** | **Asignado a**
---|---|---|---
Nueva York | VMM-NewYork| VMNetwork1-NewYork | TooVMNetwork1-Chicago asignada
 |  | VMNetwork2-NewYork | No asignado
Chicago | VMM-Chicago| VMNetwork1-Chicago | TooVMNetwork1-NewYork asignada
 | | VMNetwork1-Chicago | No asignado

En este ejemplo:

- Cuando se crea una máquina virtual de réplica para cualquier máquina virtual que está conectado tooVMNetwork1-NewYork, estará conectado tooVMNetwork1-Chicago.
- Cuando se crea una máquina virtual de réplica para VMNetwork2-NewYork o VMNetwork2-Chicago, no estará conectada tooany red.

Aquí es cómo se configuran las nubes de VMM en nuestra organización de ejemplo y redes lógicas Hola asociadas a nubes de Hola.

#### <a name="cloud-protection-settings"></a>Configuración de la protección de la nube

**Nube protegida** | **Proteger nube** | **Red lógica (Nueva York)**  
---|---|---
GoldCloud1 | GoldCloud2 |
SilverCloud1| SilverCloud2 |
GoldCloud2 | <p>N/D</p><p></p> | <p>LogicalNetwork1-NewYork</p><p>LogicalNetwork1-Chicago</p>
SilverCloud2 | <p>N/D</p><p></p> | <p>LogicalNetwork1-NewYork</p><p>LogicalNetwork1-Chicago</p>

#### <a name="logical-and-vm-network-settings"></a>Configuración de la red lógica y máquinas virtuales

**Ubicación** | **Red lógica** | **Red de VM asociada**
---|---|---
Nueva York | LogicalNetwork1-NewYork | VMNetwork1-NewYork
Chicago | LogicalNetwork1-Chicago | VMNetwork1-Chicago
 | LogicalNetwork2Chicago | VMNetwork2-Chicago

#### <a name="target-network-settings"></a>Configuración de red de destino

Según estos valores, al seleccionar red de VM de destino de hello, hello en la tabla siguiente muestra las opciones de Hola que estarán disponibles.

**Selección** | **Nube protegida** | **Proteger nube** | **Red de destino disponible**
---|---|---|---
VMNetwork1-Chicago | SilverCloud1 | SilverCloud2 | Disponible
 | GoldCloud1 | GoldCloud2 | Disponible
VMNetwork2-Chicago | SilverCloud1 | SilverCloud2 | No disponible
 | GoldCloud1 | GoldCloud2 | Disponible


Si la red de destino de hello tiene varias subredes y una de dichas subredes tiene Hola mismo nombre como Hola subred en qué Hola máquina virtual de origen se encuentra, a continuación, Hola máquina virtual de réplica será toothat conectado subred de destino después de la conmutación por error. Si no hay ninguna subred de destino con un nombre coincidente, máquina virtual de hello estará conectado toohello primera subred de red de Hola.


#### <a name="failback-behavior"></a>Comportamiento de conmutación por recuperación

toosee lo que ocurre en el caso de hello de conmutación por recuperación (replicación inversa), vamos a suponer que VMNetwork1-NewYork está asignada tooVMNetwork1-Chicago, con hello después de la configuración.


**Máquina virtual** | **Red tooVM conectado**
---|---
VM1 | VMNetwork1-Network
VM2 (réplica de VM1) | VMNetwork1-Chicago

Con esta configuración, revisemos lo que ocurre en un par de escenarios posibles.

**Escenario** | **Resultado**
---|---
Ningún cambio hello en Propiedades de red de VM-2 después de la conmutación por error. | VM-1 permanece conectado toohello red de origen.
Las propiedades de red de VM-2 cambian después de la conmutación por error y está desconectada. | VM-1 se desconecta.
Propiedades de red de VM-2 cambian después de la conmutación por error y está conectado tooVMNetwork2-Chicago. | Si no está asignada VMNetwork2-Chicago, se desconectará VM-1.
Se cambia la asignación de redes de VMNetwork1-Chicago. | VM-1 será toohello conectado red ahora asignada tooVMNetwork1-Chicago.



## <a name="next-steps"></a>Pasos siguientes

Obtenga información acerca de [planear la infraestructura de red de hello](site-recovery-network-design.md).
