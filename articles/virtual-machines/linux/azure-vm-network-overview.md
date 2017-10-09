---
title: "aaaAzure y visión general de red de VM de Linux | Documentos de Microsoft"
description: "Información general sobre las redes de máquina virtual con Linux y Azure."
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: vlivech
manager: timlt
editor: 
ms.assetid: b5420e35-0463-4456-9803-6142db150f2e
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 10/25/2016
ms.author: v-livech
ms.openlocfilehash: c3de2dc583c62160e10c0e97e96fef49b9eaffbf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-and-linux-vm-network-overview"></a>Información general sobre las redes de máquina virtual con Linux y Azure
## <a name="virtual-networks"></a>Redes virtuales
Una red virtual (VNet) es una representación de su propia red en la nube de Hola. Es un aislamiento lógico de hello nube de Azure dedicada tooyour suscripción. Puede controlar completamente bloques de direcciones IP de hello, configuración de DNS, las directivas de seguridad y tablas de rutas dentro de esta red. También puede segmentar aún más la red virtual en subredes e iniciar máquinas virtuales de IaaS de Azure (VM) o servicios en la nube (instancias de rol de PaaS). Además, puede conectarse hello tooyour local red virtual mediante una de las opciones de conectividad de hello disponibles en Azure. Básicamente, puede expandir su tooAzure de red, con control total sobre los bloques de direcciones IP con la ventaja de Hola de escala empresarial que proporciona Azure.

* [Información general sobre redes virtuales](../../virtual-network/virtual-networks-overview.md)

toocreate una red virtual mediante el uso de Hola CLI de Azure, vaya toofollow aquí Hola tutorial.

* [¿Cómo toocreate una red virtual utilizando Hola CLI de Azure](../../virtual-network/virtual-networks-create-vnet-arm-cli.md)

## <a name="network-security-groups"></a>Grupos de seguridad de red
Grupo de seguridad de red (NSG) contiene una lista de reglas de lista de Control de acceso (ACL) que permiten o deniegan el tráfico de red tooyour instancias de máquina virtual en una red Virtual. Los NSG se pueden asociar con las subredes o las instancias individuales de máquina virtual dentro de esa subred. Cuando un NSG está asociado a una subred, las reglas de ACL de hello aplican tooall instancias de máquina virtual de hello en esa subred. Además, el tráfico tooan máquina virtual individual se puede restringir aún más mediante asociar un NSG directamente toothat máquina virtual.

* [¿Qué es un grupo de seguridad de red?](../../virtual-network/virtual-networks-nsg.md)
* [Cómo toocreate NSG en Hola CLI de Azure](../../virtual-network/virtual-networks-create-nsg-arm-cli.md)

## <a name="user-defined-routes"></a>Rutas definidas por el usuario
Cuando se agrega la red virtual de máquinas virtuales (VM) tooa (VNet) en Azure, observará que hello las máquinas virtuales son capaz de toocommunicate entre sí a través de la red hello, automáticamente. No es necesario toospecify una puerta de enlace, incluso aunque hello las máquinas virtuales están en subredes diferentes. Hello mismo sirve para la comunicación de hello las máquinas virtuales toohello Internet pública y la red local de tooyour incluso cuando el propietario de una conexión híbrida de Azure tooyour centro de datos está presente.

* [¿Qué son las rutas definidas por el usuario y el reenvío IP?](../../virtual-network/virtual-networks-udr-overview.md)
* [Crear un UDR Hola CLI de Azure](../../virtual-network/virtual-network-create-udr-arm-cli.md)

## <a name="associating-a-fqdn-tooyour-linux-vm"></a>Asociar un tooyour FQDN VM de Linux
Cuando se crea una máquina virtual (VM) en hello portal de Azure mediante el modelo de implementación de administrador de recursos de hello, una dirección IP pública recursos para la máquina virtual de Hola se crean automáticamente. Utilice este Hola acceso de tooremotely de dirección IP virtual. Aunque el portal de hello no crea un nombre de dominio completo o FQDN, de forma predeterminada, puede agregar uno una vez que se crea Hola VM.

* [Crear un nombre de dominio completo en hello portal de Azure](portal-create-fqdn.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="network-interfaces"></a>Interfaces de red
Una interfaz de red (NIC) es la interconexión Hola entre una máquina Virtual (VM) y Hola subyacente de la red de software. Este artículo se explica qué interfaz de red y cómo se utiliza en el modelo de implementación de hello Azure Resource Manager.

* [Interfaces de red virtual](../../virtual-network/virtual-network-network-interface.md)

## <a name="virtual-nics-and-dns-labeling"></a>NIC virtuales y etiquetado de DNS
Si dispone de un servidor que necesita toobe persistentes, pero que el servidor se trata como ganado y se cierra y se implementa con frecuencia, deseará toouse DNS etiquetado en el nombre NIC toopersist hello en hello red virtual.  Con hello siguiendo el tutorial configurará una NIC de forma persistente con nombre con una dirección IP estática.

* [Crear un entorno completo de Linux mediante Hola CLI de Azure](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="virtual-network-gateways"></a>Puertas de enlace de red virtual
Se utiliza una puerta de enlace de red virtual toosend el tráfico de red entre redes virtuales de Azure y ubicaciones locales y también entre redes virtuales dentro de Azure (VNet a VNet). Cuando se configura una puerta de enlace de VPN, debe crear y configurar una puerta de enlace de red virtual y una conexión de puerta de enlace de red virtual.

* [Acerca de VPN Gateway](../../vpn-gateway/vpn-gateway-about-vpngateways.md)

## <a name="internal-load-balancing"></a>Equilibrio de carga interno
Azure Load Balancer es un equilibrador de carga de nivel 4 (TCP y UDP) equilibrador de carga de Hello proporciona alta disponibilidad mediante la distribución de tráfico entrante entre instancias de servicio de estado de servicios en la nube o máquinas virtuales en un conjunto de equilibrador de carga. Azure Load Balancer también pueden presentar prestar servicios en varios puertos, varias direcciones IP o ambos.

* [Creación de un equilibrador de carga interno mediante Hola CLI de Azure](../../load-balancer/load-balancer-get-started-internet-arm-cli.md)

