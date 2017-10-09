---
title: "intercambio de tráfico de red Virtual aaaAzure | Documentos de Microsoft"
description: "Más información sobre el emparejamiento de redes virtuales en Azure."
services: virtual-network
documentationcenter: na
author: NarayanAnnamalai
manager: jefco
editor: tysonn
ms.assetid: eb0ba07d-5fee-4db0-b1cb-a569b7060d2a
ms.service: virtual-network
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/17/2017
ms.author: narayan
ms.openlocfilehash: 46a14b416a7d4389f79a3cd7c55e388b5d312577
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="virtual-network-peering"></a>Emparejamiento de redes virtuales de Azure
Intercambio de tráfico de red virtual permite tooconnect dos redes virtuales en Hola misma región a través de Hola red troncal de Azure. Una vez emparejar, aparecen las dos redes virtuales de Hola que, para fines de conectividad. las redes virtuales Hola dos todavía se administran como recursos independientes, pero máquinas virtuales de hello emparejar las redes virtuales pueden comunicarse entre sí directamente, mediante el uso de direcciones IP privadas.

el tráfico entre máquinas virtuales en Hola Hola emparejar las redes virtuales se enruta a través de la infraestructura de Azure, igual se enruta el tráfico entre máquinas virtuales en Hola Hola misma red virtual. Algunas de las ventajas de hello del uso de intercambio de tráfico de red virtual son:

* Baja latencia, conexión de gran ancho de banda entre los recursos de redes virtuales diferentes.
* Hola capacidad toouse los recursos como los dispositivos de red y puertas de enlace VPN como puntos de tránsito en una red virtual peered.
* Hola capacidad toopeer dos redes virtuales creadas a través del modelo de implementación de Azure Resource Manager Hola o toopeer una red virtual que se creó mediante la tooa del Administrador de recursos de red virtual que se creó mediante el modelo de implementación clásica de Hola. Hola de lectura [modelos de implementación de Azure comprender](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artículo toolearn más información acerca de las diferencias de hello entre los modelos de implementación de Azure Hola dos.

## <a name="requirements-constraints"></a>Requisitos y restricciones

* Hello emparejar las redes virtuales deben existir en hello misma región de Azure. Puede conectar redes virtuales en diferentes regiones de Azure mediante una instancia de [VPN Gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md?toc=%2fazure%2fvirtual-network%2ftoc.json#V2V).
* Hello emparejar las redes virtuales deben tener espacios de direcciones IP no se superponen.
* No se pueden agregar espacios de direcciones a una red virtual ni eliminarse de esta una vez que una red virtual se empareja con otra red virtual.
* El emparejamiento de red virtual se realiza entre dos redes virtuales. No hay ninguna relación transitiva derivada entre emparejamientos. Por ejemplo, si virtualNetworkA está emparejada con virtualNetworkB y virtualNetworkB está emparejada con virtualNetworkC, virtualNetworkA es *no* toovirtualNetworkC emparejar.
* Puede explorar las redes virtuales que existen en dos suscripciones distintas, como el tiempo de un usuario con privilegios (vea [permisos específicos](create-peering-different-deployment-models-subscriptions.md#permissions)) de ambos suscripciones autoriza emparejamiento hello, y las suscripciones de hello son toohello asociado mismo Inquilino de Azure Active Directory. Puede usar un [puerta de enlace VPN](../vpn-gateway/vpn-gateway-about-vpngateways.md?toc=%2fazure%2fvirtual-network%2ftoc.json#V2V) tooconnect redes virtuales en las suscripciones asociadas toodifferent inquilinos de Active Directory.
* Redes virtuales se pueden emparejar si ambos se crean a través del modelo de implementación del Administrador de recursos de Hola o si se crea una red virtual a través del modelo de implementación del Administrador de recursos de Hola y Hola otro se crea a través del modelo de implementación clásica de Hola. Dos redes virtuales creadas a través del modelo de implementación clásica de hello no pueden ser emparejar tooeach otro, sin embargo. Puede usar un [puerta de enlace VPN](../vpn-gateway/vpn-gateway-about-vpngateways.md?toc=%2fazure%2fvirtual-network%2ftoc.json#V2V) tooconnect dos redes virtuales creadas a través del modelo de implementación clásica de Hola.
* Aunque la comunicación entre máquinas virtuales en redes virtuales emparejar hello no tiene ninguna restricción de ancho de banda adicional, no hay un ancho de banda de red máximo según el tamaño de la máquina virtual de Hola que sigue siendo aplicable. más información acerca de ancho de banda de red máximo para tamaños de máquina virtual diferente, leer hello toolearn [Windows](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) o [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artículos de tamaños de máquina virtual.
* La resolución de nombres DNS internos que proporciona Azure para las máquinas virtuales no funciona en las redes virtuales emparejadas. Máquinas virtuales tienen nombres DNS internos que se puede resolver sólo dentro de la red virtual local de Hola. Obstante, puede configurar redes virtuales de máquinas virtuales conectadas toopeered como servidores DNS para una red virtual. Para obtener más información, lea hello [resolución de nombres con su propio servidor DNS](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server) artículo.

![Emparejamiento básico de red virtual](./media/virtual-networks-peering-overview/figure01.png)

## <a name="connectivity"></a>Conectividad
Después de que estén al mismo nivel dos redes virtuales, recursos de cualquier red virtual se pueden conectar directamente con los recursos de red virtual de emparejar Hola. redes virtuales Hola dos tienen el nivel de IP completa conectividad.

latencia de red de Hola de ida y vuelta entre dos máquinas virtuales en redes virtuales emparejar es Hola igual que para un recorrido de ida y dentro de una única red virtual. rendimiento de la red de Hola se basa en el ancho de banda de Hola que se permite para la máquina virtual de hello, tamaño proporcional tooits. No hay ninguna restricción adicional en el ancho de banda de emparejamiento de Hola.

el tráfico entre máquinas virtuales en redes virtuales emparejar Hola se enruta directamente a través de hello Azure infraestructura de back-end, no a través de una puerta de enlace.

Red virtual de máquinas virtuales conectadas tooa puede tener acceso a los extremos con equilibrio de carga internos hello en la red virtual de emparejar Hola. Grupos de seguridad de red pueden aplicarse en redes virtuales de red virtual tooblock acceso tooother o subredes, si lo desea.

Al configurar el intercambio de tráfico de red virtual, puede abrir o cerrar reglas de grupo de seguridad de red de hello entre redes virtuales Hola. Si abre completa conectividad entre redes virtuales emparejar (que es la opción predeterminada de hello), puede aplicar red seguridad grupos toospecific subredes o máquinas virtuales tooblock o denegar el acceso específico. toolearn Obtenga más información sobre grupos de seguridad de red leer hello [información general de grupos de seguridad de red](virtual-networks-nsg.md) artículo.

## <a name="service-chaining"></a>Encadenamiento de servicios
Puede configurar rutas definidas por el usuario que máquinas toovirtual punto en redes virtuales emparejar como Hola "próximo salto" IP dirección tooenable encadenamiento de servicios. El encadenamiento de servicio permite el tráfico del toodirect, desde un dispositivo virtual de tooa de red virtual en una red virtual peered a través de las rutas definidas por el usuario.

Puede generar también eficazmente los entornos de tipo de concentrador y radio, donde concentrador Hola puede hospedar los componentes de infraestructura, como un dispositivo virtual de la red. A continuación, pueden del mismo nivel todas las redes virtuales de hello radio con red virtual de base de datos central de Hola. Tráfico pueda fluir a través de los dispositivos de red virtual que se ejecutan en la red virtual de base de datos central de Hola. En resumen, el intercambio de tráfico de red virtual permite Hola IP dirección del próximo salto en toobe de ruta de hello definido por el usuario Hola la dirección IP de una máquina virtual en la red virtual de hello emparejar. más información acerca de las rutas definidas por el usuario, leer hello toolearn [información general de las rutas definidas por el usuario](virtual-networks-udr-overview.md) artículo.

## <a name="gateways-and-on-premises-connectivity"></a>Puertas de enlace y conectividad local
Cada red virtual, independientemente de si se está emparejada con otra red virtual, todavía puede tener su propia puerta de enlace y usar red local de tooconnect tooan. También puede configurar [conexiones de red a virtual de red Virtual](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md?toc=%2fazure%2fvirtual-network%2ftoc.json) mediante el uso de las puertas de enlace, incluso aunque estén al mismo nivel en redes virtuales Hola.

Cuando se configuran ambas opciones para la interconectividad de red virtual, el tráfico entre redes virtuales Hola Hola fluye a través de la configuración de emparejamiento de hello (es decir, mediante Hola red troncal de Azure).

Cuando las redes virtuales estén al mismo nivel, también puede configurar puerta de enlace de hello en la red virtual de hello emparejar como una red de tránsito punto tooan local. En este caso, la red virtual de Hola que está usando una puerta de enlace remota no puede tener su propia puerta de enlace. Una red virtual no puede tener más de una puerta de enlace. puerta de enlace de Hola puede tener una puerta de enlace local o remoto (Hola emparejar red virtual), como se muestra en hello después de imagen:

![Tránsito de emparejamiento de VNET](./media/virtual-networks-peering-overview/figure02.png)

Tránsito de puerta de enlace no se admite en la relación de emparejamiento de hello entre redes virtuales creadas a través de diferentes modelos de implementación. Ambas redes virtuales en la relación de emparejamiento de hello deben haber creado mediante el Administrador de recursos para un toowork de tránsito de puerta de enlace.

Cuando estén al mismo nivel en redes virtuales de Hola que comparten una sola conexión de ExpressRoute de Azure, tráfico de hello entre ellos pasa a través de la relación de emparejamiento de hello (es decir, mediante Hola red troncal de Azure). Todavía puede usar las puertas de enlace locales en cada circuito de red virtual tooconnect toohello local. Como alternativa, puede utilizar una puerta de enlace compartida y configurar el tránsito para la conectividad local.

## <a name="provisioning"></a>Aprovisionamiento
El emparejamiento de red virtual es una operación que requiere privilegios. Es una función independiente en el espacio de nombres de hello VirtualNetworks. Un usuario puede indicarse tooauthorize emparejamiento a derechos específicos. Un usuario que tenga acceso de lectura y escritura toohello virtual red hereda automáticamente estos derechos.

Un usuario que ya sea un administrador o un usuario con privilegios de capacidad de emparejamiento de hello puede iniciar una operación de intercambio de tráfico en otra red virtual. Si hay una solicitud de búsqueda de coincidencias para el emparejamiento en Hola otro lado, y si se cumplen los requisitos, se establece el emparejamiento de Hola.

## <a name="limits"></a>límites
Hay límites en hello número de emparejamientos que se permiten en una única red virtual. Para obtener más información, consulte hello [el límite de red Azure](../azure-subscription-service-limits.md#networking-limits).

## <a name="pricing"></a>Precios
Hay un cargo nominal para el tráfico de entrada y salida que utiliza un emparejamiento de red virtual. Para obtener más información, vea hello [página de precios](https://azure.microsoft.com/pricing/details/virtual-network).

## <a name="next-steps"></a>Pasos siguientes

* Realice el tutorial de emparejamiento de redes virtuales. Un intercambio de tráfico de red virtual se crea entre redes virtuales creadas a través de hello mismo o diferentes modelos de implementación que existen en Hola suscripciones iguales o distintas. Completar un tutorial para uno de hello los escenarios siguientes:
 
    |Modelo de implementación de Azure  | La suscripción  |
    |---------|---------|
    |Ambas mediante Resource Manager |[La misma](virtual-network-create-peering.md)|
    | |[Diferente](create-peering-different-subscriptions.md)|
    |Una mediante Resource Manager y la otra clásica     |[La misma](create-peering-different-deployment-models.md)|
    | |[Diferente](create-peering-different-deployment-models-subscriptions.md)|

* Obtenga información acerca de cómo toocreate un [topología de red de concentrador y radio](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering) 
* Obtenga información acerca de todos los [configuración de intercambio de tráfico de red virtual y cómo toochange ellos](virtual-network-manage-peering.md)
