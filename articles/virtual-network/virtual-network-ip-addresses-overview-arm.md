---
title: tipos de direcciones de aaaIP en Azure | Documentos de Microsoft
description: "Información acerca de direcciones IP públicas y privadas en Azure."
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
tags: azure-resource-manager
ms.assetid: 610b911c-f358-4cfe-ad82-8b61b87c3b7e
ms.service: virtual-network
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/27/2016
ms.author: jdial
ms.openlocfilehash: 402d3707c00f0b3bf3ef1febd5ade66223da74bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="ip-address-types-and-allocation-methods-in-azure"></a>Tipos de direcciones IP y métodos de asignación en Azure
Puede asignar recursos IP direcciones tooAzure toocommunicate con otros recursos de Azure, la red local y Hola Internet. Hay dos tipos de direcciones IP que puede usar en Azure:

* **Las direcciones IP públicas**: utilizado para la comunicación con Internet, incluidos los servicios orientados al público Azure hello
* **Direcciones IP privadas**: utilizado para la comunicación dentro de una red virtual (VNet) y sus instalaciones de red cuando se usa una puerta de enlace VPN o tooextend de circuito de ExpressRoute tooAzure de su red.

> [!NOTE]
> Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../resource-manager-deployment-model.md).  Este artículo incluye el uso de modelo de implementación de administrador de recursos de hello, que Microsoft recomienda para la mayoría de las nueva implementaciones en lugar de hello [modelo de implementación clásica](virtual-network-ip-addresses-overview-classic.md).
> 

Si está familiarizado con el modelo de implementación clásica de hello, compruebe hello [las diferencias en entre clásico de direcciones IP y el Administrador de recursos](virtual-network-ip-addresses-overview-classic.md#differences-between-resource-manager-and-classic-deployments).

## <a name="public-ip-addresses"></a>Direcciones IP públicas
Las direcciones IP públicas permiten toocommunicate de recursos de Azure con Internet y Azure servicios orientados al público como [Azure Redis Cache](https://azure.microsoft.com/services/cache/), [centros de eventos de Azure](https://azure.microsoft.com/services/event-hubs/), [bases de datos SQL](../sql-database/sql-database-technical-overview.md), y [almacenamiento de Azure](../storage/common/storage-introduction.md).

En el Administrador de recursos de Azure, una dirección [IP pública](resource-groups-networking.md#public-ip-address) es un recurso que cuenta con propiedades específicas. Puede asociar un recurso de dirección IP público a cualquiera de hello recursos siguientes:

* Máquinas virtuales (VM)
* Equilibradores de carga accesibles desde Internet
* Puertas de enlace de VPN
* Puertas de enlace de aplicaciones

### <a name="allocation-method"></a>Método de asignación
Existen dos métodos en el que una dirección IP se asigna tooa *público* recurso IP - *dinámica* o *estático*. método de asignación de Hello predeterminado es *dinámica*, donde es una dirección IP **no** asigna en tiempo de Hola de su creación. En su lugar, se asigna la dirección IP pública Hola al iniciar (o crear) recursos Hola asociado (por ejemplo, un equilibrador de carga o de máquina virtual). dirección IP de Hola se libera cuando detener (o eliminar) recursos Hola. Esto hace que toochange de dirección IP de hello cuando detiene e inicia un recurso.

dirección IP de tooensure Hola durante hello recursos asociados sigue estando Hola mismo, puede establecer el método de asignación de hello explícitamente demasiado*estático*. En este caso, la dirección IP se asigna de inmediato. Se libera solo al eliminar el recurso de Hola o cambiar su método de asignación también*dinámica*.

> [!NOTE]
> Incluso cuando se establece el método de asignación de hello demasiado*estático*, no se puede especificar Hola real IP dirección asignada toohello *recurso IP público*. En su lugar, se obtiene asignada desde un grupo de direcciones IP disponibles en la ubicación de Azure Hola recursos Hola se crean en.
>

Direcciones IP públicas estáticas se usan habitualmente en hello los escenarios siguientes:

* Los usuarios finales necesitan tooupdate toocommunicate de reglas de firewall con los recursos de Azure.
* La resolución de nombres DNS, en la que un cambio de dirección IP requeriría actualizar los registros D.
* Los recursos de Azure se comunican con otras aplicaciones o servicios que utilizan un modelo de seguridad basado en dirección IP.
* Use la dirección IP de tooan vinculado de certificados SSL.

> [!NOTE]
> lista de Hola de intervalos IP desde el que las direcciones IP públicas (dinámico o estático) se asignan recursos tooAzure se publica en [intervalos de direcciones IP del centro de datos de Azure](https://www.microsoft.com/download/details.aspx?id=41653).
>

### <a name="dns-hostname-resolution"></a>Resolución de nombres de host DNS
Puede especificar una etiqueta de nombre de dominio DNS para un recurso IP pública, que se crea una asignación para *domainnamelabel*. *ubicación*. cloudapp.azure.com toohello la dirección IP en servidores DNS administrados de Azure de Hola. Por ejemplo, si crea un recurso IP público con **contoso** como un *domainnamelabel* en hello **oeste de Estados Unidos** Azure *ubicación*, Hola nombre de dominio completo (FQDN) **contoso.westus.cloudapp.azure.com** resolverá toohello de dirección IP pública del recurso de Hola. Puede usar este toocreate FQDN un CNAME de dominio personalizado que apunte toohello la dirección IP pública de Azure.

> [!IMPORTANT]
> Cada etiqueta de nombre de dominio que se cree debe ser única dentro de su ubicación de Azure.  
>

### <a name="virtual-machines"></a>Máquinas virtuales
Puede asociar una dirección IP pública con una [Windows](../virtual-machines/windows/overview.md) o [Linux](../virtual-machines/virtual-machines-linux-about.md) VM asignando tooits **interfaz de red**. En caso de hello de una máquina virtual con varias interfaces de red, puede asignar toohello *principal* sólo la interfaz de red. Puede asignar una tooa de dirección IP pública VM estático o dinámico.

### <a name="internet-facing-load-balancers"></a>Equilibradores de carga accesibles desde Internet
Puede asociar una dirección IP pública con una [equilibrador de carga de Azure](../load-balancer/load-balancer-overview.md), asignando toohello equilibrador de carga **front-end** configuración. Esta dirección IP pública actúa como dirección IP virtual (VIP) de carga equilibrada. Puede asignar un estática pública IP dirección tooa equilibrador de carga front-end o dinámico. También puede asignar varios pública IP direcciones tooa equilibrador de carga front-end, lo que permite [multi-VIP](../load-balancer/load-balancer-multivip.md) escenarios como un entorno de varios inquilinos con sitios Web basados en SSL.

### <a name="vpn-gateways"></a>Puertas de enlace de VPN
[La puerta de enlace de VPN Azure](../vpn-gateway/vpn-gateway-about-vpngateways.md) es tooconnect usa una red de locales de redes virtuales de Azure o tooan de tooother de red virtual de Azure (VNet). Necesita tooassign una tooits de dirección IP pública **configuración IP** tooenable se toocommunicate con la red remota Hola. Actualmente, solo se puede asignar un *dinámica* puerta de enlace VPN de tooa pública dirección IP.

### <a name="application-gateways"></a>Puertas de enlace de aplicaciones
Puede asociar una dirección IP pública con un Azure [Application Gateway](../application-gateway/application-gateway-introduction.md), mediante la asignación de la puerta de enlace de toohello **front-end** configuración. Esta dirección IP pública actúa como VIP de carga equilibrada. Actualmente, solo se puede asignar un *dinámica* pública tooan aplicación puerta de enlace front-end configuración de dirección IP.

### <a name="at-a-glance"></a>De un vistazo
siguiente de la tabla de Hello muestra la propiedad específica de Hola a través del cual puede ser una dirección IP pública asociado tooa recurso de nivel superior y los métodos de asignación posible hello (dinámicos o estáticos) que se pueden usar.

| Recurso de nivel superior | Asociación de dirección IP | dinámico | estático |
| --- | --- | --- | --- |
| Máquina virtual |interfaz de red |Sí |Sí |
| Equilibrador de carga |Configuración de front-end |Sí |Sí |
| Puerta de enlace de VPN |Configuración de dirección IP de puerta de enlace |Sí |No |
| puerta de enlace de aplicaciones |Configuración de front-end |Sí |No |

## <a name="private-ip-addresses"></a>Direcciones IP privadas
Las direcciones IP privadas permiten toocommunicate de recursos de Azure con otros recursos en un [red virtual](virtual-networks-overview.md) o a una red local a través de una puerta de enlace VPN o un circuito de ExpressRoute, sin usar una dirección IP accesible de Internet.

En el modelo de implementación de hello Azure Resource Manager, una dirección IP privada es asociado toohello siguientes tipos de recursos de Azure:

* Máquinas virtuales
* Equilibradores de carga internos (ILB)
* Puertas de enlace de aplicaciones

### <a name="allocation-method"></a>Método de asignación
Se asigna una dirección IP privada de la dirección de hello rango de hello subred toowhich Hola recurso se adjunta. intervalo de direcciones de Hola de subred Hola propio es una parte del intervalo de direcciones de la red virtual de Hola.

Hay dos métodos de asignación de direcciones IP privadas: *dinámico* o *estático*. método de asignación de Hello predeterminado es *dinámica*, donde la dirección IP de Hola se asigna automáticamente de la subred del recurso de hello (mediante DHCP). Puede cambiar esta dirección IP cuando se detiene e inicia recursos Hola.

Puede establecer el método de asignación de hello demasiado*estático* Hola tooensure Hola IP dirección permanece igual. En este caso, también debe tooprovide una dirección IP válida que forma parte de la subred del recurso de Hola.

Las direcciones IP privadas estáticas se suelen usar para:

* Máquinas virtuales que actúan como controladores de dominio o servidores DNS.
* Recursos que requieren reglas de firewall que usan direcciones IP.
* Recursos a los que se accede desde otras aplicaciones o recursos a través de una dirección IP.

### <a name="virtual-machines"></a>Máquinas virtuales
Se asigna una dirección IP privada toohello **interfaz de red** de un [Windows](../virtual-machines/windows/overview.md) o [Linux](../virtual-machines/virtual-machines-linux-about.md) máquina virtual. En una máquina virtual de interfaz de varias redes, se asigna una dirección IP privada a cada una. Puede especificar el método de asignación de hello como dinámico o estático para una interfaz de red.

#### <a name="internal-dns-hostname-resolution-for-vms"></a>Resolución de nombres de host DNS internos (para máquinas virtuales)
Todas las máquinas virtuales de Azure se configuran con [servidores DNS administrados por Azure](virtual-networks-name-resolution-for-vms-and-role-instances.md#azure-provided-name-resolution) de forma predeterminada, a menos que se configuren explícitamente servidores DNS personalizados. Estos servidores DNS proporcionan resolución de nombres interna para máquinas virtuales que residen dentro de hello misma red virtual.

Cuando se crea una máquina virtual, se agregan a una asignación para la dirección IP privada de tooits de nombre de host de hello servidores DNS administrados de Azure de toohello. En el caso de una interfaz de red de la máquina virtual, se asigna el nombre de host de hello toohello de dirección IP privada de la interfaz de red principal de Hola.

Máquinas virtuales configuradas con servidores DNS administrados de Azure será capaz de tooresolve Hola nombres de host de todas las máquinas virtuales dentro de sus red virtual tootheir las direcciones IP privadas.

### <a name="internal-load-balancers-ilb--application-gateways"></a>Equilibradores de carga internos (ILB) y puertas de enlace de aplicaciones
Puede asignar una toohello de dirección IP privada **front-end** configuración de un [equilibrador de carga interno de Azure](../load-balancer/load-balancer-internal-overview.md) (ILB) o un [puerta de enlace de aplicaciones de Azure](../application-gateway/application-gateway-introduction.md). Esta dirección IP privada actúa como un extremo interno, accesible recursos toohello solo dentro de su red virtual (VNet) y redes remotas Hola conectado toohello red virtual. Puede asignar ya sea una dinámica o estática privada configuración dirección IP toohello front-end.

### <a name="at-a-glance"></a>De un vistazo
siguiente de la tabla de Hello muestra la propiedad específica de Hola a través del cual puede ser una dirección IP privada asociado tooa recurso de nivel superior y los métodos de asignación posible hello (dinámicos o estáticos) que se pueden usar.

| Recurso de nivel superior | Asociación de dirección IP | dinámico | estático |
| --- | --- | --- | --- |
| Máquina virtual |interfaz de red |Sí |Sí |
| Equilibrador de carga |Configuración de front-end |Sí |Sí |
| puerta de enlace de aplicaciones |Configuración de front-end |Sí |Sí |

## <a name="limits"></a>límites
límites impuestos en una dirección IP Hello se indican una en el conjunto completo de Hola de [límites para las redes](../azure-subscription-service-limits.md#networking-limits) en Azure. Estos límites son por región y suscripción. También puede [póngase en contacto con soporte técnico](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade) límites predeterminados del hello tooincrease seguridad toohello límites máximos en función de sus necesidades empresariales.

## <a name="pricing"></a>Precios
Las direcciones IP públicas pueden tener un precio simbólico. toolearn más información acerca de IP de direcciones de precios de Azure, revisión hello [precios de dirección IP](https://azure.microsoft.com/pricing/details/ip-addresses) página.

## <a name="next-steps"></a>Pasos siguientes
* [Implementar una máquina virtual con una dirección IP pública estática con hello portal de Azure](virtual-network-deploy-static-pip-arm-portal.md)
* [Implementar una máquina virtual con una dirección IP pública estática mediante una plantilla](virtual-network-deploy-static-pip-arm-template.md)
* [Implementar una máquina virtual con una dirección IP privada estática mediante Hola portal de Azure](virtual-networks-static-private-ip-arm-pportal.md)
