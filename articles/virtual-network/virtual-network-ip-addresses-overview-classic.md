---
title: "tipos de direcciones de aaaIP en Azure (clásica) | Documentos de Microsoft"
description: "Obtenga información sobre las direcciones IP públicas y privadas (clásica) en Azure."
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
tags: azure-service-management
ms.assetid: 2f8664ab-2daf-43fa-bbeb-be9773efc978
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/11/2016
ms.author: jdial
ms.openlocfilehash: 7e09a5ad5b5f2d55329152b5d843de3c4455d1b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="ip-address-types-and-allocation-methods-classic-in-azure"></a>Tipos de direcciones IP y métodos de asignación (clásico) en Azure
Puede asignar recursos IP direcciones tooAzure toocommunicate con otros recursos de Azure, la red local y Hola Internet. Hay dos tipos de direcciones IP que puede usar en Azure: públicas y privadas.

Las direcciones IP públicas se usan para la comunicación con Internet, incluidos los servicios orientados al público Azure Hola.

Las direcciones IP privadas se usan para la comunicación dentro de una red virtual (VNet), un servicio de nube y la red local cuando se usa una puerta de enlace VPN o tooextend de circuito de ExpressRoute tooAzure de su red.

> [!IMPORTANT]
> Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../resource-manager-deployment-model.md).  Este artículo incluye el uso de modelo de implementación clásica de Hola. Microsoft recomienda que las implementaciones más recientes usen Resource Manager. Obtenga información acerca de las direcciones IP en el Administrador de recursos por leer hello [direcciones IP](virtual-network-ip-addresses-overview-arm.md) artículo.

## <a name="public-ip-addresses"></a>Direcciones IP públicas
Las direcciones IP públicas permiten toocommunicate de recursos de Azure con Internet y Azure servicios orientados al público como [Azure Redis Cache](https://azure.microsoft.com/services/cache/), [centros de eventos de Azure](https://azure.microsoft.com/services/event-hubs/), [bases de datos SQL](../sql-database/sql-database-technical-overview.md), y [almacenamiento de Azure](../storage/common/storage-introduction.md).

Una dirección IP pública está asociada con hello siguientes tipos de recursos:

* Servicios en la nube
* Máquinas virtuales (VM) IaaS
* Instancias de rol PaaS
* Puertas de enlace de VPN
* Puertas de enlace de aplicaciones

### <a name="allocation-method"></a>Método de asignación
Cuando una dirección IP pública necesita toobe asignado tooan recursos de Azure, es *dinámicamente* asignada desde un grupo de IP pública disponible dirección dentro de recurso de Hola de hello ubicación se crea. Esta dirección IP se libera cuando se detiene el recurso de Hola. En caso de un servicio de nube, esto sucede cuando se detienen todas las instancias de rol de hello, que puede evitarse mediante el uso de un *estático* (reservado) dirección IP (vea [servicios en la nube](#Cloud-services)).

> [!NOTE]
> lista de Hola de intervalos IP desde el que las direcciones IP públicas se asignan recursos tooAzure se publica en [intervalos de direcciones IP del centro de datos de Azure](https://www.microsoft.com/download/details.aspx?id=41653).
> 
> 

### <a name="dns-hostname-resolution"></a>Resolución de nombres de host DNS
Cuando se crea un servicio de nube o una VM de IaaS, deberá tooprovide un nombre DNS del servicio de nube que es único en todos los recursos de Azure. Esto crea una asignación en hello servidores DNS administrados de Azure para *dnsname*. cloudapp.net toohello dirección IP pública recursos Hola. Por ejemplo, cuando crea un servicio de nube con un nombre DNS del servicio de nube de **contoso**, nombre de dominio completo de hello (FQDN) **contoso.cloudapp.net** se resuelve la dirección IP pública de tooa (VIP) de servicio de nube de Hola. Puede usar este toocreate FQDN un CNAME de dominio personalizado que apunte toohello la dirección IP pública de Azure.

### <a name="cloud-services"></a>Servicios en la nube
Un servicio de nube siempre tiene una IP pública que se hace referencia tooas una dirección IP virtual (VIP) de direcciones. Puede crear extremos en una nube servicio tooassociate distintos puertos en los puertos de toointernal VIP de hello en máquinas virtuales e instancias de rol Hola del servicio en nube. 

Un servicio de nube puede contener varias máquinas virtuales de IaaS o instancias de rol PaaS, todas se exponen a través de Hola mismo VIP de servicio de nube. También puede asignar [varios servicios de nube VIP tooa](../load-balancer/load-balancer-multivip.md), lo que permite escenarios de multi-VIP como entorno de varios inquilinos con sitios Web basados en SSL.

Puede asegurarse de dirección IP pública de Hola de un servicio de nube permanece Hola mismo, incluso cuando todas las instancias de rol de Hola se detienen, mediante el uso de un *estático* dirección IP pública, que se hace referencia tooas [IP reservada](virtual-networks-reserved-public-ip.md). Puede crear un recurso IP estático (reservado) en una ubicación concreta y asignar tooany servicio de nube en esa ubicación. No puede especificar la dirección IP real de hello para la dirección IP reservada de hello, se asigna desde el grupo de direcciones IP disponibles en la ubicación de Hola se crea. Esta dirección IP no se libera hasta que la elimine explícitamente.

Direcciones IP públicas (reservadas) estáticas se utilizan normalmente en escenarios de Hola donde un servicio de nube:

* requiere la instalación de toobe de reglas de firewall por los usuarios finales.
* depende de la resolución de nombres DNS externa, y una dirección IP dinámica requeriría actualizar registros A.
* consume servicios web externos que usan el modelo de seguridad basado en IP.
* usa la dirección IP de tooan vinculado de certificados SSL.

> [!NOTE]
> Cuando se crea una máquina virtual clásica, Azure crea un *servicio en la nube* de contenedor, que tiene una dirección IP virtual (VIP). Cuando se realiza la creación de Hola a través del portal, valor predeterminado RDP o SSH *extremo* se configura mediante el portal de Hola para que pueda conectarse toohello máquina virtual a través de la dirección VIP de servicio de nube de Hola. Se pueden reservar esta dirección VIP de servicio de nube que proporciona eficazmente un toohello de tooconnect máquina virtual reservada para la dirección IP. Puede configurar más puntos de conexión para abrir puertos adicionales.
> 
> 

### <a name="iaas-vms-and-paas-role-instances"></a>Instancias de rol PaaS y máquinas virtuales IaaS
Puede asignar un complemento público direcciones IP directamente tooan IaaS [VM](../virtual-machines/virtual-machines-linux-about.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) o instancia de rol PaaS dentro de un servicio de nube. Se trata de una dirección IP pública de nivel de instancia de que se hace referencia tooas ([ILPIP](virtual-networks-instance-level-public-ip.md)). Esta dirección IP pública solo puede ser dinámica.

> [!NOTE]
> Esto es diferente de hello VIP del servicio de nube de hello, que es un contenedor para instancias de rol de VM de IaaS o PaaS, puesto que un servicio de nube puede contener varias máquinas virtuales de IaaS, o instancias de rol PaaS, todas se exponen a través de hello mismo VIP de servicio de nube.
> 
> 

### <a name="vpn-gateways"></a>Puertas de enlace de VPN
A [puerta de enlace VPN](../vpn-gateway/vpn-gateway-about-vpngateways.md) puede ser tooconnect usa una red virtual de Azure tooother redes de redes virtuales de Azure o de forma local. Una puerta de enlace VPN se asigna una dirección IP pública *dinámicamente*, que permite la comunicación con la red remota Hola.

### <a name="application-gateways"></a>Puertas de enlace de aplicaciones
Un Azure [puerta de enlace de aplicaciones](../application-gateway/application-gateway-introduction.md) puede utilizarse para Layer7 tráfico de red de tooroute de equilibrio de carga basado en HTTP. Puerta de enlace de aplicaciones se asigna una dirección IP pública *dinámicamente*, que actúa como Hola VIP con equilibrio de carga.

### <a name="at-a-glance"></a>En un vistazo
tabla de Hello siguiente muestra cada tipo de recurso con los métodos de asignación posible de hello (dinámico o estático) y capacidad tooassign varias direcciones IP públicas.

| Recurso | Dinámica | estática | Varias direcciones IP |
| --- | --- | --- | --- |
| servicio en la nube |Sí |Sí |Sí |
| Instancia del rol PaaS o VM IaaS |Sí |No |No |
| puerta de enlace de VPN |Sí |No |No |
| puerta de enlace de aplicaciones |Sí |No |No |

## <a name="private-ip-addresses"></a>Direcciones IP privadas
Las direcciones IP privadas permiten toocommunicate de recursos de Azure con otros recursos en un servicio de nube o un [red virtual](virtual-networks-overview.md)(VNet), o red de tooon local (a través de una puerta de enlace VPN o circuito de ExpressRoute), sin usar un Dirección IP accesible de Internet.

En el modelo de implementación clásico de Azure, se puede asignar a una dirección IP privada toohello recursos de Azure siguientes:

* Instancias de rol PaaS y máquinas virtuales IaaS
* Equilibrador de carga interno
* puerta de enlace de aplicaciones

### <a name="iaas-vms-and-paas-role-instances"></a>Instancias de rol PaaS y máquinas virtuales IaaS
Las máquinas virtuales (VM) creadas con el modelo de implementación clásica de hello siempre se colocan en un servicio de nube, instancias de rol tooPaaS similar. comportamiento de Hola de direcciones IP privadas, por tanto, son similares para estos recursos.

Es importante toonote que un servicio de nube puede ser implementado de dos maneras:

* Como un servicio en la nube *independiente* , donde no está dentro de una red virtual.
* Como parte de una red virtual.

#### <a name="allocation-method"></a>Método de asignación
En caso de un *independiente* servicio, get de recursos asignada una dirección IP privada en la nube *dinámicamente* intervalo de direcciones de IP privada de hello Azure del centro de datos. Se puede utilizar solo para la comunicación con otras máquinas virtuales dentro de hello mismo servicio en la nube. Cuando se detiene e inicia el recurso de hello, puede cambiar esta dirección IP.

En el caso de un servicio de nube implementado en una red virtual, obtener privados recursos de direcciones IP asignado desde el intervalo de direcciones de Hola de hello asociado subredes (según lo especificado en su configuración de red). Esta dirección IP privada puede utilizarse para la comunicación entre todas las máquinas virtuales dentro de hello red virtual.

Además, en caso de servicios en la nube dentro de una red virtual, se asigna una dirección IP privada *dinámicamente* (con DHCP) de forma predeterminada. Puede cambiar cuando se detiene e inicia el recurso de Hola. Hola tooensure Hola IP dirección permanece igual, deberá tooset método de asignación de hello demasiado*estático*y proporcione una dirección IP válida dentro del intervalo de direcciones de hello correspondiente.

Las direcciones IP privadas estáticas se suelen usar para:

* Máquinas virtuales que actúan como controladores de dominio o servidores DNS.
* Máquinas virtuales que requieren reglas de firewall que usan direcciones IP.
* Máquinas virtuales que ejecutan servicios a los que se accede desde otras aplicaciones a través de una dirección IP.

#### <a name="internal-dns-hostname-resolution"></a>Resolución de nombre de host DNS internos
Todas las máquinas virtuales de Azure e instancias de rol PaaS se configuran con [servidores DNS administrados por Azure](virtual-networks-name-resolution-for-vms-and-role-instances.md#azure-provided-name-resolution) de forma predeterminada, a menos que se configuren explícitamente servidores DNS personalizados. Estos servidores DNS proporcionan resolución de nombres interna para las máquinas virtuales e instancias de rol que residen dentro de Hola mismo servicio en la nube o red virtual.

Cuando se crea una máquina virtual, se agregan a una asignación para la dirección IP privada de tooits de nombre de host de hello servidores DNS administrados de Azure de toohello. En el caso de una VM de varias NIC, se asigna el nombre de host de hello toohello de dirección IP privada de NIC de hello principal. Sin embargo, esta información de asignación es tooresources restringido en hello mismo nube servicio o una red virtual.

En caso de un *independiente* servicio, en la nube será capaz de tooresolve los nombres de host de todas las instancias de máquinas virtuales o el rol de hello mismo sólo del servicio de nube. En el caso de un servicio de nube en una red virtual, será capaz de tooresolve los nombres de host de todas las instancias de máquinas virtuales o el rol de Hola de hello red virtual.

### <a name="internal-load-balancers-ilb--application-gateways"></a>Equilibradores de carga internos (ILB) y puertas de enlace de aplicaciones
Puede asignar una toohello de dirección IP privada **front-end** configuración de un [equilibrador de carga interno de Azure](../load-balancer/load-balancer-internal-overview.md) (ILB) o un [puerta de enlace de aplicaciones de Azure](../application-gateway/application-gateway-introduction.md). Esta dirección IP privada actúa como un extremo interno, accesible recursos toohello solo dentro de su red virtual (VNet) y redes remotas Hola conectado toohello red virtual. Puede asignar ya sea una dinámica o estática privada configuración dirección IP toohello front-end. También puede asignar varios privada IP direcciones tooenable multi-vip escenarios.

### <a name="at-a-glance"></a>En un vistazo
tabla de Hello siguiente muestra cada tipo de recurso con los métodos de asignación posible de hello (dinámico o estático) y capacidad tooassign varias direcciones IP privadas.

| Recurso | Dinámica | estática | Varias direcciones IP |
| --- | --- | --- | --- |
| Máquina virtual (en un servicio en la nube *independiente* ) |Sí |Sí |Sí |
| Instancia de rol PaaS (en un servicio en la nube *independiente* ) |Sí |No |Sí |
| Instancia de rol PaaS o VM (en una red virtual) |Sí |Sí |Sí |
| Front-end de equilibrador de carga interno |Sí |Sí |Sí |
| Front-end de Puerta de enlace de aplicaciones |Sí |Sí |Sí |

## <a name="limits"></a>límites
tabla de Hola a continuación muestran los límites de hello impuestos en IP addressing en Azure por suscripción. También puede [póngase en contacto con soporte técnico](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade) límites predeterminados del hello tooincrease seguridad toohello límites máximos en función de sus necesidades empresariales.

|  | Límite predeterminado | Límite máximo |
| --- | --- | --- |
| Direcciones IP públicas (dinámicas) |5 |ponerse en contacto con el servicio de soporte técnico |
| Direcciones IP públicas reservadas |20 |ponerse en contacto con el servicio de soporte técnico |
| VIP pública por implementación (servicio en la nube) |5 |ponerse en contacto con el servicio de soporte técnico |
| VIP privada (ILB) por implementación (servicio en la nube) |1 |1 |

Asegúrese de leer el conjunto completo de Hola de [límites para las redes](../azure-subscription-service-limits.md#networking-limits) en Azure.

## <a name="pricing"></a>Precios
En la mayoría de los casos, las direcciones IP públicas son gratis. Hay un cargo nominal toouse adicionales o estáticas direcciones IP públicas. Asegúrese de que comprende hello [estructura de precios de direcciones IP públicas](https://azure.microsoft.com/pricing/details/ip-addresses/).

## <a name="differences-between-resource-manager-and-classic-deployments"></a>Diferencias entre la implementación del Administración de recursos y la implementación clásica
A continuación se muestra una comparación de características de direccionamiento de IP en el Administrador de recursos y el modelo de implementación clásica de Hola.

|  | Recurso | Clásico | Resource Manager |
| --- | --- | --- | --- |
| **Dirección IP pública** |***VM*** |Que se hace referencia tooas un ILPIP (solo dinámico) |Conoce tooas una IP pública (dinámico o estático) |
|  ||Tooan asignado IaaS VM o una instancia de rol PaaS |NIC de la máquina virtual toohello asociado | |
|  |***Equilibrador de carga accesible desde Internet*** |Conoce tooas VIP (dinámico) o la dirección IP reservada (estático) |Conoce tooas una IP pública (dinámico o estático) | |
|  ||Servicio de nube tooa asignado |Configuración de front-end del equilibrador de carga de toohello asociado | |
|  | | | |
| **Dirección IP privada** |***VM*** |Tooas que se hace referencia una DIP |Conoce tooas una dirección IP privada |
|  ||Tooan asignado IaaS VM o una instancia de rol PaaS |NIC de la máquina virtual toohello asignado | |
|  |***Equilibrador de carga interno (ILB)*** |Toohello asignado ILB (dinámico o estático) |Configuración de front-end del ILB toohello asignado (dinámico o estático) | |

## <a name="next-steps"></a>Pasos siguientes
* [Implementar una máquina virtual con una dirección IP privada estática](virtual-networks-static-private-ip-classic-pportal.md) utilizando Hola portal de Azure.

