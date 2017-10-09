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
# <a name="about-cryptographic-requirements-and-azure-vpn-gateways"></a><span data-ttu-id="b83bc-103">Acerca de los requisitos criptográficos y las puertas de enlace de VPN de Azure</span><span class="sxs-lookup"><span data-stu-id="b83bc-103">About cryptographic requirements and Azure VPN gateways</span></span>

<span data-ttu-id="b83bc-104">En este artículo se describe cómo se pueden configurar los requisitos de cifrado para los túneles de VPN de S2S entre entornos y las conexiones de red virtual a red virtual dentro de Azure de toosatisfy de puertas de enlace de VPN de Azure.</span><span class="sxs-lookup"><span data-stu-id="b83bc-104">This article discusses how you can configure Azure VPN gateways toosatisfy your cryptographic requirements for both cross-premises S2S VPN tunnels and VNet-to-VNet connections within Azure.</span></span> 

## <a name="about-ipsec-and-ike-policy-parameters-for-azure-vpn-gateways"></a><span data-ttu-id="b83bc-105">Acerca de los parámetros de la directiva de IPsec e IKE para puertas de enlace de VPN de Azure</span><span class="sxs-lookup"><span data-stu-id="b83bc-105">About IPsec and IKE policy parameters for Azure VPN gateways</span></span>
<span data-ttu-id="b83bc-106">El protocolo IPsec e IKE estándar admite una gran variedad de algoritmos criptográficos en diversas combinaciones.</span><span class="sxs-lookup"><span data-stu-id="b83bc-106">IPsec and IKE protocol standard supports a wide range of cryptographic algorithms in various combinations.</span></span> <span data-ttu-id="b83bc-107">Si los clientes no solicitan una combinación específica de algoritmos y parámetros criptográficos, las puertas de enlace de VPN de Azure usan un conjunto de propuestas predeterminadas.</span><span class="sxs-lookup"><span data-stu-id="b83bc-107">If customers do not request a specific combination of cryptographic algorithms and parameters, Azure VPN gateways use a set of default proposals.</span></span> <span data-ttu-id="b83bc-108">conjuntos de directivas de Hello predeterminados se eligieron toomaximize interoperabilidad con una amplia gama de dispositivos VPN de terceros en las configuraciones predeterminadas.</span><span class="sxs-lookup"><span data-stu-id="b83bc-108">hello default policy sets were chosen toomaximize interoperability with a wide range of third-party VPN devices in default configurations.</span></span> <span data-ttu-id="b83bc-109">Como resultado, las directivas de Hola y el número de Hola de propuestas no pueden cubrir todas las posibles combinaciones de algoritmos criptográficos disponibles y ventajas claves.</span><span class="sxs-lookup"><span data-stu-id="b83bc-109">As a result, hello policies and hello number of proposals cannot cover all possible combinations of available cryptographic algorithms and key strengths.</span></span>

<span data-ttu-id="b83bc-110">Hola directiva predeterminado establecido para la puerta de enlace VPN de Azure se muestra en el documento de hello: [dispositivos acerca de VPN y los parámetros de IPsec/IKE para las conexiones de puerta de enlace VPN de sitio a sitio](vpn-gateway-about-vpn-devices.md).</span><span class="sxs-lookup"><span data-stu-id="b83bc-110">hello default policy set for Azure VPN gateway is listed in hello document: [About VPN devices and IPsec/IKE parameters for Site-to-Site VPN Gateway connections](vpn-gateway-about-vpn-devices.md).</span></span>

## <a name="cryptographic-requirements"></a><span data-ttu-id="b83bc-111">Requisitos criptográficos</span><span class="sxs-lookup"><span data-stu-id="b83bc-111">Cryptographic requirements</span></span>
<span data-ttu-id="b83bc-112">Para las comunicaciones que requieren determinados algoritmos criptográficos o parámetros, normalmente debido a requisitos de seguridad o toocompliance, los clientes ahora pueden configurar su toouse de puertas de enlace de VPN de Azure una directiva personalizada de IPsec/IKE con concreto criptográfico algoritmos y ventajas claves, en lugar de conjuntos de directivas de hello predeterminado de Azure.</span><span class="sxs-lookup"><span data-stu-id="b83bc-112">For communications that require specific cryptographic algorithms or parameters, typically due toocompliance or security requirements, customers can now configure their Azure VPN gateways toouse a custom IPsec/IKE policy with specific cryptographic algorithms and key strengths, rather than hello Azure default policy sets.</span></span>

<span data-ttu-id="b83bc-113">Por ejemplo, las directivas de modo principal de hello IKEv2 para puertas de enlace de VPN de Azure usan solo Diffie-Hellman grupo 2 (1024 bits), mientras que los clientes pueden necesitar toobe toospecify de grupos más seguro usar en IKE, como grupo 14 (2048 bits), 24 de grupo (grupo de MODP de 2048 bits) o ECP (elíptica curva grupos) 256 o 384 bits (grupo 19 y 20 de grupo, respectivamente).</span><span class="sxs-lookup"><span data-stu-id="b83bc-113">For example, hello IKEv2 main mode policies for Azure VPN gateways utilize only Diffie-Hellman Group 2 (1024 bits), whereas customers may need toospecify stronger groups toobe used in IKE, such as Group 14 (2048-bit), Group 24 (2048-bit MODP Group), or ECP (elliptic curve groups) 256 or 384 bit (Group 19 and Group 20, respectively).</span></span> <span data-ttu-id="b83bc-114">Requisitos similares aplican también las directivas de modo rápido de tooIPsec.</span><span class="sxs-lookup"><span data-stu-id="b83bc-114">Similar requirements apply tooIPsec quick mode policies as well.</span></span>

## <a name="custom-ipsecike-policy-with-azure-vpn-gateways"></a><span data-ttu-id="b83bc-115">Directiva personalizada de IPsec o IKE con puertas de enlace de VPN de Azure</span><span class="sxs-lookup"><span data-stu-id="b83bc-115">Custom IPsec/IKE policy with Azure VPN gateways</span></span>
<span data-ttu-id="b83bc-116">Ahora las puertas de enlace de VPN de Azure admiten directivas de IPsec o IKE personalizadas y por conexión.</span><span class="sxs-lookup"><span data-stu-id="b83bc-116">Azure VPN gateways now support per-connection, custom IPsec/IKE policy.</span></span> <span data-ttu-id="b83bc-117">Para una conexión de red virtual a red virtual o de sitio a sitio, puede elegir una combinación específica de algoritmos criptográficos de IPsec e IKE con nivel de clave de hello deseado, como se muestra en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="b83bc-117">For a Site-to-Site or VNet-to-VNet connection, you can choose a specific combination of cryptographic algorithms for IPsec and IKE with hello desired key strength, as shown in hello following example:</span></span>

![ipsec-ike-policy](./media/vpn-gateway-about-compliance-crypto/ipsecikepolicy.png)

<span data-ttu-id="b83bc-119">Puede crear una directiva de IPsec/IKE y aplicar tooa conexión nuevo o existente.</span><span class="sxs-lookup"><span data-stu-id="b83bc-119">You can create an IPsec/IKE policy and apply tooa new or existing connection.</span></span> 

### <a name="workflow"></a><span data-ttu-id="b83bc-120">Flujo de trabajo</span><span class="sxs-lookup"><span data-stu-id="b83bc-120">Workflow</span></span>

1. <span data-ttu-id="b83bc-121">Crear redes virtuales hello, puertas de enlace VPN o puertas de enlace de red local para la topología de conectividad como se describe en otras toodocuments cómo</span><span class="sxs-lookup"><span data-stu-id="b83bc-121">Create hello virtual networks, VPN gateways, or local network gateways for your connectivity topology as described in other how-toodocuments</span></span>
2. <span data-ttu-id="b83bc-122">Cree una directiva IPsec/IKE.</span><span class="sxs-lookup"><span data-stu-id="b83bc-122">Create an IPsec/IKE policy</span></span>
3. <span data-ttu-id="b83bc-123">Puede aplicar directiva de hello cuando se crea una conexión de S2S o red virtual a red virtual</span><span class="sxs-lookup"><span data-stu-id="b83bc-123">You can apply hello policy when you create a S2S or VNet-to-VNet connection</span></span>
4. <span data-ttu-id="b83bc-124">Si ya se creó la conexión de hello, puede aplicar o actualizar la conexión existente de hello directiva tooan</span><span class="sxs-lookup"><span data-stu-id="b83bc-124">If hello connection is already created, you can apply or update hello policy tooan existing connection</span></span>


## <a name="ipsecike-policy-faq"></a><span data-ttu-id="b83bc-125">P+F sobre directivas de IPsec o IKE</span><span class="sxs-lookup"><span data-stu-id="b83bc-125">IPsec/IKE policy FAQ</span></span>

[!INCLUDE [vpn-gateway-ipsecikepolicy-faq-include](../../includes/vpn-gateway-ipsecikepolicy-faq-include.md)]


## <a name="next-steps"></a><span data-ttu-id="b83bc-126">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b83bc-126">Next steps</span></span>
<span data-ttu-id="b83bc-127">Consulte [Configure IPsec/IKE policy](vpn-gateway-ipsecikepolicy-rm-powershell.md) (Configuración de la directiva de IPsec o IKE) para obtener instrucciones paso a paso acerca de cómo configurar directivas personalizadas de IPsec o IKE en una conexión.</span><span class="sxs-lookup"><span data-stu-id="b83bc-127">See [Configure IPsec/IKE policy](vpn-gateway-ipsecikepolicy-rm-powershell.md) for step-by-step instructions on configuring custom IPsec/IKE policy on a connection.</span></span>

<span data-ttu-id="b83bc-128">Vea también [conectar varios dispositivos VPN basada en directivas](vpn-gateway-connect-multiple-policybased-rm-ps.md) toolearn más información acerca de hello UsePolicyBasedTrafficSelectors opción.</span><span class="sxs-lookup"><span data-stu-id="b83bc-128">See also [Connect multiple policy-based VPN devices](vpn-gateway-connect-multiple-policybased-rm-ps.md) toolearn more about hello UsePolicyBasedTrafficSelectors option.</span></span>
