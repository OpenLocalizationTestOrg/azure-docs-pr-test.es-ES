---
title: aaaAbout requisitos de cifrado y las puertas de enlace de VPN de Azure | Documentos de Microsoft
description: "Este artículo describe los requisitos criptográficos y las puertas de enlace de VPN de Azure"
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: azure-resource-manager
ms.assetid: 238cd9b3-f1ce-4341-b18e-7390935604fa
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/22/2017
ms.author: yushwang
ms.openlocfilehash: af5f14d66beeea5316218f9788c4ad7876826162
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="about-cryptographic-requirements-and-azure-vpn-gateways"></a>Acerca de los requisitos criptográficos y las puertas de enlace de VPN de Azure

En este artículo se describe cómo se pueden configurar los requisitos de cifrado para los túneles de VPN de S2S entre entornos y las conexiones de red virtual a red virtual dentro de Azure de toosatisfy de puertas de enlace de VPN de Azure. 

## <a name="about-ipsec-and-ike-policy-parameters-for-azure-vpn-gateways"></a>Acerca de los parámetros de la directiva de IPsec e IKE para puertas de enlace de VPN de Azure
El protocolo IPsec e IKE estándar admite una gran variedad de algoritmos criptográficos en diversas combinaciones. Si los clientes no solicitan una combinación específica de algoritmos y parámetros criptográficos, las puertas de enlace de VPN de Azure usan un conjunto de propuestas predeterminadas. conjuntos de directivas de Hello predeterminados se eligieron toomaximize interoperabilidad con una amplia gama de dispositivos VPN de terceros en las configuraciones predeterminadas. Como resultado, las directivas de Hola y el número de Hola de propuestas no pueden cubrir todas las posibles combinaciones de algoritmos criptográficos disponibles y ventajas claves.

Hola directiva predeterminado establecido para la puerta de enlace VPN de Azure se muestra en el documento de hello: [dispositivos acerca de VPN y los parámetros de IPsec/IKE para las conexiones de puerta de enlace VPN de sitio a sitio](vpn-gateway-about-vpn-devices.md).

## <a name="cryptographic-requirements"></a>Requisitos criptográficos
Para las comunicaciones que requieren determinados algoritmos criptográficos o parámetros, normalmente debido a requisitos de seguridad o toocompliance, los clientes ahora pueden configurar su toouse de puertas de enlace de VPN de Azure una directiva personalizada de IPsec/IKE con concreto criptográfico algoritmos y ventajas claves, en lugar de conjuntos de directivas de hello predeterminado de Azure.

Por ejemplo, las directivas de modo principal de hello IKEv2 para puertas de enlace de VPN de Azure usan solo Diffie-Hellman grupo 2 (1024 bits), mientras que los clientes pueden necesitar toobe toospecify de grupos más seguro usar en IKE, como grupo 14 (2048 bits), 24 de grupo (grupo de MODP de 2048 bits) o ECP (elíptica curva grupos) 256 o 384 bits (grupo 19 y 20 de grupo, respectivamente). Requisitos similares aplican también las directivas de modo rápido de tooIPsec.

## <a name="custom-ipsecike-policy-with-azure-vpn-gateways"></a>Directiva personalizada de IPsec o IKE con puertas de enlace de VPN de Azure
Ahora las puertas de enlace de VPN de Azure admiten directivas de IPsec o IKE personalizadas y por conexión. Para una conexión de red virtual a red virtual o de sitio a sitio, puede elegir una combinación específica de algoritmos criptográficos de IPsec e IKE con nivel de clave de hello deseado, como se muestra en el siguiente ejemplo de Hola:

![ipsec-ike-policy](./media/vpn-gateway-about-compliance-crypto/ipsecikepolicy.png)

Puede crear una directiva de IPsec/IKE y aplicar tooa conexión nuevo o existente. 

### <a name="workflow"></a>Flujo de trabajo

1. Crear redes virtuales hello, puertas de enlace VPN o puertas de enlace de red local para la topología de conectividad como se describe en otras toodocuments cómo
2. Cree una directiva IPsec/IKE.
3. Puede aplicar directiva de hello cuando se crea una conexión de S2S o red virtual a red virtual
4. Si ya se creó la conexión de hello, puede aplicar o actualizar la conexión existente de hello directiva tooan


## <a name="ipsecike-policy-faq"></a>P+F sobre directivas de IPsec o IKE

[!INCLUDE [vpn-gateway-ipsecikepolicy-faq-include](../../includes/vpn-gateway-ipsecikepolicy-faq-include.md)]


## <a name="next-steps"></a>Pasos siguientes
Consulte [Configure IPsec/IKE policy](vpn-gateway-ipsecikepolicy-rm-powershell.md) (Configuración de la directiva de IPsec o IKE) para obtener instrucciones paso a paso acerca de cómo configurar directivas personalizadas de IPsec o IKE en una conexión.

Vea también [conectar varios dispositivos VPN basada en directivas](vpn-gateway-connect-multiple-policybased-rm-ps.md) toolearn más información acerca de hello UsePolicyBasedTrafficSelectors opción.
