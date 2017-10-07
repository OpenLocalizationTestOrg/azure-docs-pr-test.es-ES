---
title: "circuitos ExpressRoute aaaMoving de tooResource clásico Manager | Documentos de Microsoft"
description: "Esta página proporciona una visión general de lo que necesita tooknow sobre Protocolo de puente hello clásico y modelos de implementación del Administrador de recursos de Hola."
documentationcenter: na
services: expressroute
author: ganesr
manager: carmonm
editor: 
ms.assetid: bdf01217-1a98-4ec0-a08e-d84fd37f78af
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/02/2017
ms.author: ganesr
ms.openlocfilehash: c901d2cda01aec409b528d29fc937ac6afaea511
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="moving-expressroute-circuits-from-hello-classic-toohello-resource-manager-deployment-model"></a>Mover los circuitos ExpressRoute de hello clásico toohello modelo de implementación del Administrador de recursos
Este artículo proporciona información general sobre lo que significa que toomove un circuito de ExpressRoute de Azure de hello clásico toohello modelo de implementación de Azure Resource Manager.

Puede usar una redes de toovirtual del tooconnect del circuito de ExpressRoute único que se implementan tanto en los modelos de implementación de administrador de recursos Hola y Hola clásico. Un circuito ExpressRoute, independientemente de cómo se crea, ahora puede vincular toovirtual redes a través de ambos modelos de implementación.

![Un circuito ExpressRoute que vincula toovirtual redes a través de ambos modelos de implementación](./media/expressroute-move/expressroute-move-1.png)

## <a name="expressroute-circuits-that-are-created-in-hello-classic-deployment-model"></a>Circuitos ExpressRoute que se crean en el modelo de implementación clásica de Hola
Circuitos ExpressRoute que se crean en el modelo de implementación clásica de hello necesitan toobe movido toohello el Administrador de recursos implementación modelo primera tooenable conectividad tooboth Hola hello y clásico Administrador de recursos modelos de implementación. Mientras se traslada una conexión, no se producen pérdida de conectividad ni interrupciones. Todos los vínculos de red circuito a virtual en el modelo de implementación clásica de hello (dentro Hola misma suscripción y entre suscripciones) se conservan.

Una vez Hola movimiento se completó correctamente, Hola circuito ExpressRoute busca, lleva a cabo y se siente exactamente igual que un circuito de ExpressRoute que se creó en el modelo de implementación del Administrador de recursos de Hola. Ahora puede crear conexiones de redes de toovirtual en el modelo de implementación del Administrador de recursos de Hola.

Después de un circuito ExpressRoute ha sido movido toohello modelo de implementación de administrador de recursos, puede administrar Hola de ciclo de vida de hello circuito ExpressRoute únicamente mediante el modelo de implementación del Administrador de recursos de Hola. Esto significa que puede realizar operaciones, como agregar, actualizar o eliminar emparejamientos, actualizar propiedades de circuito (por ejemplo, el ancho de banda, SKU y tipo de facturación) y eliminar circuitos solo en el modelo de implementación de administrador de recursos de Hola. Consulte la sección de toohello por debajo de circuitos que se crean en el modelo de implementación de administrador de recursos de Hola para obtener más información sobre cómo administrar modelos de implementación de acceso tooboth.

No es necesario tooinvolve mover su hello tooperform de proveedor de conectividad.

## <a name="expressroute-circuits-that-are-created-in-hello-resource-manager-deployment-model"></a>Circuitos ExpressRoute que se crean en el modelo de implementación del Administrador de recursos de Hola
Puede habilitar los circuitos ExpressRoute que se crean en toobe de modelo de implementación de administrador de recursos de hello accesibles desde ambos modelos de implementación. Cualquier circuito de ExpressRoute en su suscripción puede ser habilitado toobe acceso desde ambos modelos de implementación.

* Circuitos ExpressRoute que se crearon en el modelo de implementación del Administrador de recursos de hello no tiene modelo de implementación clásica de toohello de acceso de forma predeterminada.
* Circuitos ExpressRoute que se han movido desde el modelo de implementación del Administrador de recursos de hello implementación clásica modelo toohello son accesibles desde ambos modelos de implementación de forma predeterminada.
* Un circuito ExpressRoute siempre tiene el modelo de implementación en el Administrador de recursos de toohello de acceso, independientemente de si se creó en el Administrador de recursos de Hola o modelo de implementación clásica. Esto significa que se pueden crear conexiones toovirtual redes creadas en Hola modelo de implementación del Administrador de recursos siguiendo las instrucciones en [cómo redes virtuales toolink](expressroute-howto-linkvnet-arm.md).
* Modelo de implementación clásica de toohello de acceso se controla mediante hello **allowClassicOperations** parámetro Hola circuito de ExpressRoute.

> [!IMPORTANT]
> Todas las cuotas que se documentan en hello [límites de servicio](../azure-subscription-service-limits.md) página se aplica. Por ejemplo, un circuito estándar puede tener como máximo 10 vínculos/conexiones de red virtual a través de hello clásico y modelos de implementación del Administrador de recursos de Hola.
> 
> 

## <a name="controlling-access-toohello-classic-deployment-model"></a>Controlar el modelo de implementación clásica de toohello de acceso
Para habilitar una red de toovirtual único de toolink circuito de ExpressRoute en ambos modelos de implementación, configuración hello **allowClassicOperations** parámetro de hello circuito de ExpressRoute.

Establecer **allowClassicOperations** tooTRUE permite toolink redes virtuales desde ambos toohello de modelos de implementación circuito de ExpressRoute. Es posible vincular redes toovirtual en el modelo de implementación clásica de hello indicados en estas instrucciones en [cómo toolink las redes virtuales en Hola modelo de implementación clásica](expressroute-howto-linkvnet-classic.md). Es posible vincular redes toovirtual en el modelo de implementación del Administrador de recursos de hello indicados en estas instrucciones en [cómo toolink las redes virtuales en Hola modelo de implementación del Administrador de recursos](expressroute-howto-linkvnet-arm.md).

Establecer **allowClassicOperations** tooFALSE bloques acceder a toohello circuito de modelo de implementación clásica de Hola. Sin embargo, se conservan todos los vínculos de red virtual en el modelo de implementación clásica de Hola. En este caso, no es visible en el modelo de implementación clásica de Hola Hola circuito de ExpressRoute.

## <a name="supported-operations-in-hello-classic-deployment-model"></a>Operaciones admitidas en el modelo de implementación clásica de Hola
las siguientes operaciones clásicas de Hola se admite en una ExpressRoute circuit cuando **allowClassicOperations** se establece tooTRUE:

* Obtener información del circuito ExpressRoute
* Red virtual de creación/actualización/get/eliminación vincula tooclassic las redes virtuales
* Crear, actualizar, obtener y eliminar autorizaciones de vínculo de red virtual para la conectividad entre suscripciones

No se puede realizar las siguientes operaciones clásicas de hello cuando **allowClassicOperations** se establece tooTRUE:

* Crear, actualizar, obtener y eliminar emparejamientos de Border Gateway Protocol (BGP) para emparejamientos públicos y privados de Azure y emparejamientos de Microsoft
* Eliminar circuitos ExpressRoute

## <a name="communication-between-hello-classic-and-hello-resource-manager-deployment-models"></a>Comunicación entre Hola clásico y modelos de implementación del Administrador de recursos de Hola
Hola circuito ExpressRoute actúa como un puente entre Hola clásico y modelos de implementación del Administrador de recursos de Hola. El tráfico entre máquinas virtuales en redes virtuales en el modelo de implementación clásica de Hola y los de las redes virtuales en los flujos de modelo de implementación de administrador de recursos de Hola a través de ExpressRoute si ambas redes virtuales están vinculado toohello mismo circuito de ExpressRoute.

Rendimiento global está limitado por la capacidad de rendimiento de Hola de puerta de enlace de red virtual de Hola. Tráfico no entra en las redes del proveedor de conectividad de Hola o las redes en esos casos. Flujo de tráfico entre redes virtuales hello es totalmente contenida dentro de la red de Microsoft de Hola.

## <a name="access-tooazure-public-and-microsoft-peering-resources"></a>Acceso tooAzure público y recursos de emparejamiento de Microsoft
Puede continuar recursos tooaccess que suelen ser accesibles a través de pares públicos de Azure y Microsoft emparejamiento sin ninguna interrupción.  

## <a name="whats-supported"></a>Lo que se admite
En esta sección se describe lo que se admite para los circuitos ExpressRoute:

* Puede usar un único ExpressRoute circuito tooaccess redes virtuales que se implementan en los modelos de implementación de administrador de recursos Hola y Hola clásico.
* Puede mover un circuito ExpressRoute de hello clásico toohello modelo de implementación del Administrador de recursos. Después de haberse movido, Hola circuito ExpressRoute busca, se siente y se comporta como cualquier otro circuito de ExpressRoute que se crea en el modelo de implementación del Administrador de recursos de Hola.
* Puede mover sólo el circuito de ExpressRoute Hola. Los vínculos del circuito, las redes virtuales y las puertas de enlace de VPN no se trasladan mediante esta operación.
* Después de un circuito ExpressRoute ha sido movido toohello modelo de implementación de administrador de recursos, puede administrar Hola de ciclo de vida de hello circuito ExpressRoute únicamente mediante el modelo de implementación del Administrador de recursos de Hola. Esto significa que puede realizar operaciones, como agregar, actualizar o eliminar emparejamientos, actualizar propiedades de circuito (por ejemplo, el ancho de banda, SKU y tipo de facturación) y eliminar circuitos solo en el modelo de implementación de administrador de recursos de Hola.
* Hola circuito ExpressRoute actúa como un puente entre Hola clásico y modelos de implementación del Administrador de recursos de Hola. El tráfico entre máquinas virtuales en redes virtuales en el modelo de implementación clásica de Hola y los de las redes virtuales en los flujos de modelo de implementación de administrador de recursos de Hola a través de ExpressRoute si ambas redes virtuales están vinculado toohello mismo circuito de ExpressRoute.
* Se admite la conectividad entre suscripciones en hello clásico y modelos de implementación del Administrador de recursos de Hola.
* Después de mover un circuito ExpressRoute de modelo de hello modelo clásico toohello Azure Resource Manager, puede [migrar Hola redes virtuales vinculadas toohello circuito de ExpressRoute](expressroute-migration-classic-resource-manager.md).

## <a name="whats-not-supported"></a>Lo que no se admite
En esta sección se describe lo que no se admite para los circuitos ExpressRoute:

* Administrar el ciclo de vida de Hola de un circuito de ExpressRoute de modelo de implementación clásica de Hola.
* Soporte de Control de acceso (RBAC) basada en roles para el modelo de implementación clásica de Hola. No se puede realizar RBAC controles tooa circuito en el modelo de implementación clásica de Hola. Cualquier administrador o coadministrator de suscripción de hello puede vincular o desvincular el circuito de toohello de redes virtuales.

## <a name="configuration"></a>Configuración
Siga las instrucciones de Hola que se describen en [mover un circuito ExpressRoute de modelo de implementación de administrador de recursos de hello toohello clásico](expressroute-howto-move-arm.md).

## <a name="next-steps"></a>Pasos siguientes
* [Migrar Hola redes virtuales vinculadas toohello circuito de ExpressRoute del Hola modelo clásico toohello Azure Resource Manager](expressroute-migration-classic-resource-manager.md)
* Para obtener información sobre los flujos de trabajo, consulte [Flujos de trabajo de aprovisionamiento de circuitos y estados de circuito de ExpressRoute](expressroute-workflows.md).
* tooconfigure la conexión ExpressRoute:
  
  * [Creación de un circuito ExpressRoute](expressroute-howto-circuit-arm.md)
  * [Configuración del enrutamiento](expressroute-howto-routing-arm.md)
  * [Vincular un circuito de ExpressRoute de tooan de red virtual](expressroute-howto-linkvnet-arm.md)

