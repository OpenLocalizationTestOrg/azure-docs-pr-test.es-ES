---
title: "aaaWhat toodo en caso de hello de una interrupción del servicio de Azure que afectan a las redes virtuales de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de qué toodo en caso de hello de una interrupción del servicio de Azure que afectan a las redes virtuales de Azure."
services: virtual-network
documentationcenter: 
author: NarayanAnnamalai
manager: jefco
editor: 
ms.assetid: ad260ab9-d873-43b3-8896-f9a1db9858a5
ms.service: virtual-network
ms.workload: virtual-network
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2016
ms.author: narayan;aglick
ms.openlocfilehash: db022d2a042d255cf8ec6afb68cd8436aeecfe08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="virtual-network--business-continuity"></a>Red virtual: continuidad del negocio
## <a name="overview"></a>Información general
Una red Virtual (VNet) es una representación lógica de la red en la nube de Hola. Permite toodefine su propio privada Hola de espacio y el segmento de la dirección IP de red en subredes. Redes virtuales que actúa como un toohost de límite de confianza los recursos de proceso como máquinas virtuales de Azure y servicios en la nube (roles web/trabajo). Una red virtual permite la comunicación de IP privada directa entre recursos de hello hospedados en ella. Una red Virtual también puede ser la red local de tooan vinculado a través de uno de opciones de hello híbrida como una puerta de enlace VPN o ExpressRoute.

Se crea una red virtual dentro de ámbito de Hola de una región. Puede crear redes virtuales con el mismo espacio de direcciones en dos regiones diferentes (es decir, este de EE. y US West pero no se puede conectar a tooone otro directamente). 

## <a name="business-continuity"></a>Continuidad del negocio
La aplicación puede sufrir diferentes formas de interrupción. Una región determinada podría quedar cortada completamente debido a catástrofes naturales tooa o un desastre parcial debido a errores en tooa varios dispositivos o servicios. impacto de Hello en hello servicio de red virtual es diferente en cada una de estas situaciones.

**P: ¿qué hacer en caso de hello de interrupción tooan toda una región? ¿es decir, si una región es completamente límite debido a catástrofes naturales tooa? ¿Qué ocurre toohello redes virtuales hospedadas en la región de hello?**

R: los recursos de red y Hola de Virtual Hola Hola afectado región sigue siendo accesible durante el tiempo de Hola Hola de interrupción del servicio.

![Diagrama de red virtual simple](./media/virtual-network-disaster-recovery-guidance/vnet.png)

**P: ¿qué se puede toodo volver a crear Hola la misma red Virtual en una región distinta?**

R: Una red virtual es un recurso bastante ligero. Puede invocar las API de Azure toocreate una red virtual con hello mismo espacio de direcciones en una región diferente. toore-crear hello mismo entorno que ya estaba presente en hello afectados región, tendrá que toomake API llamadas toore-implemente los servicios de nube (roles web/trabajo) y máquinas virtuales que había. También tendrá toospin una copia de seguridad una puerta de enlace de VPN y conectar la red de tooyour local si tiene conectividad local (como en una implementación híbrida).

Encontrará instrucciones de Hola para crear una red virtual [aquí](virtual-networks-create-vnet-arm-pportal.md). 

**P: ¿Es posible volver a crear una réplica de una red virtual de una región determinada en otra región de antemano?**

R: Sí, puede crear dos redes virtuales con hello IP privada mismo espacio de direcciones y recursos en dos regiones diferentes de hora. Si un cliente hospeda con conexión a servicios de red virtual de hello internet, podría configurar región toohello de Traffic Manager toogeo ruta tráfico que está activo. Sin embargo, un cliente no puede conectar dos redes virtuales con hello mismo dirección red local de espacio tootheir como daría lugar a problemas de enrutamiento. En tiempo de presentación de un desastre y la pérdida de una red virtual en una región, puede conectar un cliente Hola otra red virtual en la región disponible de hello con red de local de tootheir de espacio de dirección que coincida con.

Encontrará instrucciones de Hola para crear una red virtual [aquí](virtual-networks-create-vnet-arm-pportal.md).

