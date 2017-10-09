---
title: "asignación de aaaNetwork entre dos regiones de Azure en Azure Site Recovery | Documentos de Microsoft"
description: "Azure Site Recovery coordina la replicación hello, conmutación por error y recuperación de máquinas virtuales y servidores físicos. Obtenga información acerca de la conmutación por error tooAzure o un centro de datos secundaria."
services: site-recovery
documentationcenter: 
author: prateek9us
manager: gauravd
editor: 
ms.assetid: 44813a48-c680-4581-a92e-cecc57cc3b1e
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 08/11/2017
ms.author: pratshar
ms.openlocfilehash: 4f80c44e3f94eaf446bc01a7041d91fe34aa78d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="network-mapping-between-two-azure-regions"></a>Asignación de red entre dos regiones de Azure


Este artículo se describe cómo toomap Azure redes virtuales de dos regiones de Azure entre sí. Asignación de red garantiza que cuando se crea la máquina virtual replicada en el destino de hello región de Azure, se crea en red virtual de Hola que sea asignada toovirtual red de máquina virtual de origen Hola.  

## <a name="prerequisites"></a>Requisitos previos
Antes de asignar redes, asegúrese de haber creado [redes virtuales de Azure](../virtual-network/virtual-networks-overview.md) en las regiones de Azure de origen y destino.

## <a name="map-networks"></a>Asignar redes

toomap una red virtual de Azure en red virtual de una región de Azure tooanother en otra región, vaya tooSite recuperación infraestructura -> asignación de red (para máquinas virtuales de Azure) y crear una asignación de red.

![Asignación de red](./media/site-recovery-network-mapping-azure-to-azure/network-mapping1.png)


Hola ejemplo siguiente mi máquina virtual se está ejecutando en la región Este de Asia y se va a replica tooSoutheast Asia.

Seleccione la red de origen y de destino de hello y, a continuación, haga clic en Aceptar toocreate una asignación de red de Asia oriental tooSoutheast Asia.

![Asignación de red](./media/site-recovery-network-mapping-azure-to-azure/network-mapping2.png)


Hola mismo lo toocreate una asignación de red de tooEast sudeste de Asia oriental.  
![Asignación de red](./media/site-recovery-network-mapping-azure-to-azure/network-mapping3.png)


## <a name="mapping-network-when-enabling-replication"></a>Asignación de red al habilitar la replicación

Si no se realizó la asignación de red al que esté replicando una máquina virtual para hello primera hora formulario una región de Azure tooanother, a continuación, puede elegir red de destino como parte del programa Hola mismo proceso. Recuperación del sitio crea las asignaciones de red de área de tootarget de región de origen y de destino región toosource otra en función de esta selección.   

![Asignación de red](./media/site-recovery-network-mapping-azure-to-azure/network-mapping4.png)

De forma predeterminada, Site Recovery crea una red en la región de destino de Hola que sea idéntico toohello red de origen y mediante la adición de '-asr' como nombre de red de origen de hello toohello sufijo. Puede elegir una red ya creada si hace clic en Personalizar.

![Asignación de red](./media/site-recovery-network-mapping-azure-to-azure/network-mapping5.png)


Si ya se realizó la asignación de red de hello, no se puede cambiar la red virtual de destino de hello mientras habilita la replicación. toochange, modifique la asignación de red existente.  

![Asignación de red](./media/site-recovery-network-mapping-azure-to-azure/network-mapping6.png)

![Asignación de red](./media/site-recovery-network-mapping-azure-to-azure/modify-network-mapping.png)

> [!IMPORTANT]
> Si modifica una asignación de red de la región 1 tooregion-2, asegúrese de que se modifique la asignación de red de Hola de región 2 tooregion-1 también.
>
>


## <a name="subnet-selection"></a>Selección de subred
Subred de máquina virtual de destino de Hola se selecciona basándose en nombre de Hola de subred de Hola de máquina virtual de origen Hola. Si no hay una subred de hello igual de nombre que el de la máquina virtual de origen de hello disponible en la red de destino de hello, se ha seleccionado para la máquina virtual de destino de Hola. Si no hay ninguna subred con hello mismo nombre de red de destino de hello, a continuación, se elige alfabéticamente primera subred Hola subred de destino. Puede modificar esta subred, vaya a configuración de red de máquina virtual de Hola y tooCompute.

![Modificar la subred](./media/site-recovery-network-mapping-azure-to-azure/modify-subnet.png)


## <a name="ip-address"></a>Dirección IP

Dirección IP para cada interfaz de red de Hola Hola máquina virtual de destino se elige como se indica a continuación:

### <a name="dhcp"></a>DHCP
Si la interfaz de red de Hola de máquina virtual de origen Hola utiliza DHCP, interfaz de red de máquina virtual de destino de hello también se establece como DHCP.

### <a name="static-ip"></a>IP estática
Si la interfaz de red de Hola de máquina virtual de origen Hola utiliza direcciones IP estáticas, interfaz de red de máquina virtual de destino de hello también se establece toouse direcciones IP estáticas. La IP estática se elige como se indica a continuación:

#### <a name="same-address-space"></a>Mismo espacio de direcciones

Si dispone de subred de origen de Hola y subred de destino de Hola Hola mismo espacio de direcciones, dirección IP de destino se establece igual que IP Hola Hola interfaz de red de máquina virtual de origen Hola. Si la misma dirección de IP no está disponible, algunas la dirección IP disponible se establece como dirección IP de destino de Hola.

#### <a name="different-address-space"></a>Distinto espacio de direcciones

Si la subred de origen de Hola y subred de destino de hello tienen espacio de direcciones diferentes, dirección IP de destino se establece como cualquier dirección IP disponible en la subred de destino de Hola.

Puede modificar dirección IP de destino de hello en cada interfaz de red, vaya a configuración de red de máquina virtual de Hola y tooCompute.

## <a name="next-steps"></a>Pasos siguientes

- Más información sobre [Networking guidance for replicating Azure VMs](site-recovery-azure-to-azure-networking-guidance.md) (Instrucciones de redes para la replicación de máquinas virtuales de Azure).
