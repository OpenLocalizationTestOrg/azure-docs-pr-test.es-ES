---
title: "aaaPlan de red para la replicación de Hyper-V (withSystem Center VMM) tooAzure con Azure Site Recovery | Documentos de Microsoft"
description: "Este artículo describe la planificación de red necesaria al replicar máquinas virtuales de Hyper-V (con VMM) tooAzure"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 41c3c83e-6b1a-496a-8179-498c552ef0c7
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: 51ca8b939b6f96880f83599ea8009eb0bfa5b957
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="step-4-plan-networking-for-hyper-v-with-vmm-tooazure-replication"></a>Paso 4: Planear la red para la replicación de Hyper-V (con VMM) tooAzure

Después de realizar [planeamiento de capacidad](vmm-to-azure-walkthrough-capacity.md) (si está realizando una implementación completa), leer este toolearn artículo sobre planeación de consideraciones al replicar locales máquinas virtuales de Hyper-V en System Center Virtual Machine Manager (VMM) de una red nubes tooAzure, con hello [Azure Site Recovery](site-recovery-overview.md) servicio.

Registrar los comentarios de la parte inferior de Hola de este artículo, o formular alguna pregunta en hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="network-mapping-for-replication-tooazure"></a>Asignación de red para la replicación tooAzure

Asignación de red se utiliza al replicar tooAzure de máquinas virtuales de Hyper-V (que se administren en VMM). La asignación de red se produce entre redes de máquinas virtuales en un servidor VMM de origen y redes de Azure de destino. Asignación Hola siguientes:

- **Conexión de red**: después de la conmutación por error, todas las máquinas virtuales de Azure replicados son redes de Azure asignada de toohello conectado. Todas las máquinas que conmutar por error en hello misma red puede conectarse tooeach otra, aunque conmutado por error en los planes de recuperación diferente.
- **Puerta de enlace de red**: si se configura una puerta de enlace de red en red Azure de destino de hello, las máquinas virtuales pueden conectarse red de máquinas virtuales Hola asignado local tooother local.

### <a name="prepare-vmm-for-network-mapping"></a>Preparar VMM para la asignación de red

Para preparar VMM para la asignación de red, siga estos pasos:

1. Si no tiene uno, preparar una [red lógica de VMM](https://docs.microsoft.com/system-center/vmm/network-logical) asociado a la nube de hello en qué Hola Hyper-V están ubicados los hosts.
2. Si no tiene uno, crea un [red de VM](https://docs.microsoft.com/system-center/vmm/network-virtual) toohello vinculado red lógica que preparó anteriormente.
3. Conectar máquinas virtuales en Hyper-V server/clúster de hosts en hello nube de VMM, red de VM toohello Hola.

 
Observe lo siguiente: 
- Se agregan nuevas máquinas virtuales conectadas red de VM de origen toohello toohello asigna red de Azure cuando se produce la replicación.
- Si la red de destino de hello tiene varias subredes y una de estas subredes se Hola mismo nombre que la subred en la máquina virtual de origen de Hola se encuentra, máquina virtual de réplica de hello conecta toothat subred de destino después de la conmutación por error.
- Si no hay ninguna subred de destino con un nombre coincidente, máquina virtual de hello conecta toohello primera subred de red de Hola.
- Preparar una red de Azure y configurar asignaciones de red, como implementar el escenario de Hola.

## <a name="connecting-tooazure-vms-after-failover"></a>Conectar máquinas virtuales de tooAzure después de la conmutación por error

Al planear su estrategia de conmutación por error y replicación, uno de preguntas clave hello es cómo tooconnect toohello máquina virtual de Azure después de la conmutación por error. Hay un par de opciones al diseñar la estrategia de red para máquinas virtuales de réplica de Azure:

- **Usar una dirección IP diferente**: se puede seleccionar toouse un intervalo de direcciones IP diferente para saludo replica red de VM de Azure. En este Hola escenario VM Obtiene una nueva dirección IP después de la conmutación por error y se requiere una actualización DNS.
- **Conservar Hola la misma dirección IP**: es recomendable toouse Hola mismo intervalo de direcciones IP como que en sus instalaciones principales de red, para hello Azure red después de la conmutación por error.  Mantener Hola simplifica la mismas direcciones IP recuperación Hola al reducir los problemas de red después de la conmutación por error. Sin embargo, cuando se está replicando tooAzure, necesitará tooupdate rutas con la nueva ubicación de direcciones IP de Hola de hello después de la conmutación por error.


## <a name="retain-ip-addresses"></a>Conservación de las direcciones IP

Recuperación de sitio proporciona las direcciones IP de hello capacidad tooretain fijada cuando se conmuta tooAzure, con una subred de conmutación por error.

Con la conmutación por error de subredes, una subred específica está presente en el sitio 1 o en el sitio 2, pero nunca en ambos sitios simultáneamente. En orden toomaintain Hola espacio de direcciones IP en el caso de hello de una conmutación por error, mediante programación se encargará de subredes de Hola Hola enrutador infraestructura toomove de tooanother de un sitio. Durante la conmutación por error, movimiento de subredes de hello con hello había asociado máquinas virtuales protegidas. Hola principal inconveniente es que en caso de hello de un error, tienes subred completa de toomove Hola.



### <a name="failover-example"></a>Ejemplo de conmutación por error

Veamos un ejemplo de tooAzure de conmutación por error.

- Una compañía ficticia, Woodgrove Bank, tiene una infraestructura local que hospeda sus aplicaciones empresariales. Las aplicaciones móviles se hospedan en Azure.
- Una conexión de sitio a sitio (VPN) entre hello red virtual de Azure y la red perimetral de hello local proporciona conectividad entre las máquinas virtuales de Woodgrove Bank en servidores Azure y local.
- Esto significa que VPN que Hola red virtual de la compañía en Azure aparece como una extensión de su red local.
- Woodgrove desea toouse Site Recovery tooreplicate local las cargas de trabajo tooAzure.
 - Woodgrove tiene toodeal con aplicaciones y configuraciones que dependen de las direcciones IP codificado de forma rígida y, por tanto, necesitan tooretain las direcciones IP para sus aplicaciones después de la conmutación por error tooAzure.
 - Woodgrove asigna direcciones IP desde intervalo 172.16.1.0/24, 172.16.2.0/24 tooits recursos que se ejecutan en Azure.


Woodgrove toobe capaz de tooreplicate su tooAzure de máquinas virtuales mientras conserva Hola IP direcciones, aquí es qué compañía Hola necesita toodo:

1. Cree una red virtual de Azure. Debe ser una extensión de hello red local para que las aplicaciones puedan conmutarse por error sin problemas.
2. Azure permite tooadd sitio a sitio VPN conectividad, además conectividad de sitio de toopoint toohello las redes virtuales creadas en Azure.
3. Al configurar la conexión de sitio a sitio hello, en hello Azure de red, puede enrutar tráfico toohello ubicación (red local) solo si el intervalo de direcciones IP de hello es diferente de intervalo de direcciones IP de hello en local.
    - Esto se debe a que Azure no admite subredes estiradas. Por lo que si tiene subred 192.168.1.0/24 local, no se puede agregar una red local 192.168.1.0/24 Hola red de Azure.
    - Esto es lo esperado porque Azure no sabe que hay máquinas virtuales activas en la subred de Hola y esa subred Hola se está creando para solo la recuperación ante desastres.
    - toobe toocorrectly puede redirigir el tráfico de red fuera de un subredes hello Azure en red de Hola y Hola de red local no debe entrar en conflicto.

![Antes de la conmutación por error de la subred](./media/vmm-to-azure-walkthrough-network/network-design7.png)

### <a name="before-failover"></a>Antes de la conmutación por error

1. Cree una red adicional (por ejemplo, una red de recuperación). Se trata de red de hello en el que no se pudo a máquinas virtuales se crean.
2. tooensure que Hola dirección IP para una máquina virtual se conserva después de una conmutación por error, en Propiedades de la máquina virtual de hello > **configurar**, especifique Hola misma dirección IP que Hola VM tiene en el servidor local y haga clic en **guardar**.
3. Cuando se conmuta Hola VM, Azure Site Recovery asignará Hola proporcionada tooit de dirección IP.

    ![Propiedades de red](./media/vmm-to-azure-walkthrough-network/network-design8.png)

4. Una vez se activa el desencadenador y hello las máquinas virtuales se crean en Azure con la dirección IP de hello necesario conmutación por error, puede conectarse toohello de red mediante un [Vnet tooVnet vonnection](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md). Esta acción puede ejecutarse mediante scripts.
5. Rutas necesitan toobe modificado de forma adecuada, tooreflect ese 192.168.1.0/24 ahora se movió tooAzure.

    ![Después de la conmutación por error de la subred](./media/vmm-to-azure-walkthrough-network/network-design9.png)

### <a name="after-failover"></a>Después de la conmutación por error

Si no dispone de una red de Azure tal y como se ilustra arriba, puede crear una conexión VPN de sitio a sitio entre el sitio primario y Azure después de la conmutación por error.

## <a name="change-ip-addresses"></a>Cambiar las direcciones IP

Esto [entrada de blog](http://azure.microsoft.com/blog/2014/09/04/networking-infrastructure-setup-for-microsoft-azure-as-a-disaster-recovery-site/) explica cómo aborda tooset seguridad hello Azure infraestructura de red cuando no se necesitan tooretain IP después de la conmutación por error. Empieza con una descripción de la aplicación, se centra en cómo tooset la red local y en Azure y concluye con información sobre la ejecución de las conmutaciones por error.  

## <a name="next-steps"></a>Pasos siguientes

Vaya demasiado[paso 5: preparar Azure](vmm-to-azure-walkthrough-prepare-azure.md)
