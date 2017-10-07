---
title: aaaOverview de BGP con puertas de enlace de VPN de Azure | Documentos de Microsoft
description: "Este artículo proporciona información general de BGP con puertas de enlace de VPN de Azure."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: 
ms.assetid: f8c3985c-c128-4f34-835c-0e88742bf36e
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/12/2017
ms.author: yushwang
ms.openlocfilehash: ced3f77ecd791c84fb72b96447e839be3bf94846
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-bgp-with-azure-vpn-gateways"></a>Información general de BGP con puertas de enlace de VPN de Azure
Este artículo proporciona información general de compatibilidad de BGP (Border Gateway Protocol) en las puertas de enlace de VPN de Azure.

BGP es frecuente en hello tooexchange enrutamiento y alcance de la información de Internet entre dos o más redes de protocolo de enrutamiento estándar Hola. Cuando se utiliza en el contexto de Hola de redes virtuales de Azure, BGP permite puertas de enlace de VPN de Azure de Hola y los dispositivos VPN local, que se llama a los pares BGP o vecinos, tooexchange "enruta" que influirán en las puertas de enlace en la disponibilidad de Hola y disponibilidad para los Agrega el prefijo toogo a través de las puertas de enlace de Hola o enrutadores implicados. BGP también puede habilitar el enrutamiento del tránsito entre varias redes mediante la propagación de las rutas de una puerta de enlace BGP aprende desde una BGP del mismo nivel tooall otros pares BGP. 

## <a name="why-use-bgp"></a>¿Por qué usar BGP?
BGP es una característica opcional que puede utilizar con puertas de enlace de VPN basadas en enrutamiento de Azure. También debe asegurarse de que los dispositivos VPN local admiten BGP antes de habilitar la característica de Hola. Puede seguir toouse puertas de enlace de VPN de Azure y los dispositivos VPN local sin BGP. Es Hola equivalente del uso de rutas estáticas (sin BGP) *frente a* con enrutamiento dinámico con BGP entre las redes y Azure.

Hay varias ventajas y nuevas funcionalidades con BGP:

### <a name="support-automatic-and-flexible-prefix-updates"></a>Uso de actualizaciones de prefijo flexible y automáticas
Con BGP, solo necesita toodeclare un prefijo mínimo tooa BGP del mismo nivel concreto a través de túnel de VPN con IPsec S2S Hola. Puede ser tan pequeño como un prefijo de host (/ 32) del programa Hola a la dirección IP BGP del mismo nivel del dispositivo VPN local. Puede controlar que local prefijos de red que desee tooadvertise tooAzure tooallow tooaccess de su red Virtual de Azure.

También puede anunciar prefijos mayores que pueden incluir algunos de los prefijos de dirección de red virtual, como un espacio de direcciones IP privado grande (por ejemplo, 10.0.0.0/8). Tenga en cuenta si los prefijos de hello no pueden coincidir con uno de los prefijos de red virtual. Se rechazarán los prefijos de red virtual de rutas tooyour idénticos.

### <a name="support-multiple-tunnels-between-a-vnet-and-an-on-premises-site-with-automatic-failover-based-on-bgp"></a>Uso de varios túneles entre una red virtual y un sitio local con la conmutación por error automática basada en BGP
Puede establecer varias conexiones entre la red virtual de Azure y los dispositivos VPN local Hola misma ubicación. Esta capacidad proporciona varios túneles (rutas) entre dos redes de hello en una configuración activo / activo. Si uno de los túneles de hello está desconectada, las rutas correspondientes de Hola se retirará a través de BGP y tráfico de Hola cambia automáticamente toohello restantes túneles.

Hola siguiente diagrama muestra un ejemplo sencillo de este programa de instalación de alta disponibilidad:

![Varias rutas de acceso activas](./media/vpn-gateway-bgp-overview/multiple-active-tunnels.png)

### <a name="support-transit-routing-between-your-on-premises-networks-and-multiple-azure-vnets"></a>Uso del enrutamiento de tránsito entre las redes locales y varias redes virtuales de Azure
BGP permite toolearn de varias puertas de enlace y propagar los prefijos de las redes diferentes, si están directa o indirectamente conectados. Esto puede permitir el enrutamiento de tránsito con puertas de enlace de VPN de Azure entre sitios locales o en varias redes virtuales de Azure.

Hello siguiente diagrama muestra un ejemplo de una topología de salto múltiples con varias rutas que puede tránsito tráfico entre redes de hello dos de local a través de las puertas de enlace de VPN de Azure en hello Microsoft Networks:

![Tránsito de múltiples saltos](./media/vpn-gateway-bgp-overview/full-mesh-transit.png)

## <a name="bgp-faq"></a>Preguntas más frecuentes de BGP
[!INCLUDE [vpn-gateway-bgp-faq-include](../../includes/vpn-gateway-bpg-faq-include.md)]

## <a name="next-steps"></a>Pasos siguientes
Vea [introducción con BGP en puertas de enlace de VPN de Azure](vpn-gateway-bgp-resource-manager-ps.md) para pasos tooconfigure BGP para las conexiones de red virtual a red virtual y entre entornos.

