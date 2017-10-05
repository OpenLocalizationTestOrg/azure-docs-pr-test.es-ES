---
title: "Acerca de los requisitos criptográficos y las puertas de enlace de VPN de Azure | Microsoft Docs"
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
ms.openlocfilehash: c789e6c278fc0c58c64f5d96e57f94aee5a6cefc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="about-cryptographic-requirements-and-azure-vpn-gateways"></a><span data-ttu-id="6b7ab-103">Acerca de los requisitos criptográficos y las puertas de enlace de VPN de Azure</span><span class="sxs-lookup"><span data-stu-id="6b7ab-103">About cryptographic requirements and Azure VPN gateways</span></span>

<span data-ttu-id="6b7ab-104">En este artículo se explica cómo configurar puertas de enlace de VPN de Azure para satisfacer los requisitos criptográficos para los túneles de VPN de sitio a sitio entre entornos y las conexiones entre redes virtuales dentro de Azure.</span><span class="sxs-lookup"><span data-stu-id="6b7ab-104">This article discusses how you can configure Azure VPN gateways to satisfy your cryptographic requirements for both cross-premises S2S VPN tunnels and VNet-to-VNet connections within Azure.</span></span> 

## <a name="about-ipsec-and-ike-policy-parameters-for-azure-vpn-gateways"></a><span data-ttu-id="6b7ab-105">Acerca de los parámetros de la directiva de IPsec e IKE para puertas de enlace de VPN de Azure</span><span class="sxs-lookup"><span data-stu-id="6b7ab-105">About IPsec and IKE policy parameters for Azure VPN gateways</span></span>
<span data-ttu-id="6b7ab-106">El protocolo IPsec e IKE estándar admite una gran variedad de algoritmos criptográficos en diversas combinaciones.</span><span class="sxs-lookup"><span data-stu-id="6b7ab-106">IPsec and IKE protocol standard supports a wide range of cryptographic algorithms in various combinations.</span></span> <span data-ttu-id="6b7ab-107">Si los clientes no solicitan una combinación específica de algoritmos y parámetros criptográficos, las puertas de enlace de VPN de Azure usan un conjunto de propuestas predeterminadas.</span><span class="sxs-lookup"><span data-stu-id="6b7ab-107">If customers do not request a specific combination of cryptographic algorithms and parameters, Azure VPN gateways use a set of default proposals.</span></span> <span data-ttu-id="6b7ab-108">Los conjuntos de directivas predeterminados se eligieron para maximizar la interoperabilidad con una amplia gama de dispositivos VPN de terceros en las configuraciones predeterminadas.</span><span class="sxs-lookup"><span data-stu-id="6b7ab-108">The default policy sets were chosen to maximize interoperability with a wide range of third-party VPN devices in default configurations.</span></span> <span data-ttu-id="6b7ab-109">Como resultado, las directivas y el número de propuestas no pueden cubrir todas las posibles combinaciones de algoritmos criptográficos disponibles y puntos fuertes clave.</span><span class="sxs-lookup"><span data-stu-id="6b7ab-109">As a result, the policies and the number of proposals cannot cover all possible combinations of available cryptographic algorithms and key strengths.</span></span>

<span data-ttu-id="6b7ab-110">La directiva predeterminada establecida para la puerta de enlace de VPN de Azure se muestra en el documento: [Acerca de los dispositivos VPN y los parámetros de IPsec o IKE para conexiones de VPN Gateway de sitio a sitio](vpn-gateway-about-vpn-devices.md).</span><span class="sxs-lookup"><span data-stu-id="6b7ab-110">The default policy set for Azure VPN gateway is listed in the document: [About VPN devices and IPsec/IKE parameters for Site-to-Site VPN Gateway connections](vpn-gateway-about-vpn-devices.md).</span></span>

## <a name="cryptographic-requirements"></a><span data-ttu-id="6b7ab-111">Requisitos criptográficos</span><span class="sxs-lookup"><span data-stu-id="6b7ab-111">Cryptographic requirements</span></span>
<span data-ttu-id="6b7ab-112">Para las comunicaciones que requieren determinados algoritmos o parámetros criptográficos, normalmente debido a los requisitos de seguridad o de conformidad con normas, ahora los clientes pueden configurar sus puertas de enlace de VPN de Azure para usar una directiva personalizada de IPsec o IKE con determinados algoritmos criptográficos y puntos fuertes clave, en lugar de los conjuntos de directivas predeterminados de Azure.</span><span class="sxs-lookup"><span data-stu-id="6b7ab-112">For communications that require specific cryptographic algorithms or parameters, typically due to compliance or security requirements, customers can now configure their Azure VPN gateways to use a custom IPsec/IKE policy with specific cryptographic algorithms and key strengths, rather than the Azure default policy sets.</span></span>

<span data-ttu-id="6b7ab-113">Por ejemplo, las directivas de modo principal de IKEv2 para puertas de enlace de VPN de Azure usan solo Grupo Diffie-Hellman 2 (1024 bits), mientras que es posible que los clientes necesiten especificar grupos más sólidos para su uso en IKE, por ejemplo, Grupo 14 (2048 bits), Grupo 24 (grupo de MODP de 2048 bits) o ECP (grupos de curva elíptica) de 256 o 384 bits (Grupo 19 y Grupo 20, respectivamente).</span><span class="sxs-lookup"><span data-stu-id="6b7ab-113">For example, the IKEv2 main mode policies for Azure VPN gateways utilize only Diffie-Hellman Group 2 (1024 bits), whereas customers may need to specify stronger groups to be used in IKE, such as Group 14 (2048-bit), Group 24 (2048-bit MODP Group), or ECP (elliptic curve groups) 256 or 384 bit (Group 19 and Group 20, respectively).</span></span> <span data-ttu-id="6b7ab-114">También se aplican requisitos similares a las directivas de modo rápido de IPsec.</span><span class="sxs-lookup"><span data-stu-id="6b7ab-114">Similar requirements apply to IPsec quick mode policies as well.</span></span>

## <a name="custom-ipsecike-policy-with-azure-vpn-gateways"></a><span data-ttu-id="6b7ab-115">Directiva personalizada de IPsec o IKE con puertas de enlace de VPN de Azure</span><span class="sxs-lookup"><span data-stu-id="6b7ab-115">Custom IPsec/IKE policy with Azure VPN gateways</span></span>
<span data-ttu-id="6b7ab-116">Ahora las puertas de enlace de VPN de Azure admiten directivas de IPsec o IKE personalizadas y por conexión.</span><span class="sxs-lookup"><span data-stu-id="6b7ab-116">Azure VPN gateways now support per-connection, custom IPsec/IKE policy.</span></span> <span data-ttu-id="6b7ab-117">Para una conexión entre sitios o entre redes virtuales puede elegir una combinación específica de algoritmos criptográficos para IPsec e IKE con el nivel de clave deseado, como se muestra en el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="6b7ab-117">For a Site-to-Site or VNet-to-VNet connection, you can choose a specific combination of cryptographic algorithms for IPsec and IKE with the desired key strength, as shown in the following example:</span></span>

![ipsec-ike-policy](./media/vpn-gateway-about-compliance-crypto/ipsecikepolicy.png)

<span data-ttu-id="6b7ab-119">Puede crear una directiva de IPsec o IKE y aplicarla a una conexión nueva o existente.</span><span class="sxs-lookup"><span data-stu-id="6b7ab-119">You can create an IPsec/IKE policy and apply to a new or existing connection.</span></span> 

### <a name="workflow"></a><span data-ttu-id="6b7ab-120">Flujo de trabajo</span><span class="sxs-lookup"><span data-stu-id="6b7ab-120">Workflow</span></span>

1. <span data-ttu-id="6b7ab-121">Cree las redes virtuales, las puertas de enlace de VPN o las puertas de enlace de red local para su topología de conectividad, como se describe en otros documentos y procedimientos.</span><span class="sxs-lookup"><span data-stu-id="6b7ab-121">Create the virtual networks, VPN gateways, or local network gateways for your connectivity topology as described in other how-to documents</span></span>
2. <span data-ttu-id="6b7ab-122">Cree una directiva IPsec o IKE.</span><span class="sxs-lookup"><span data-stu-id="6b7ab-122">Create an IPsec/IKE policy</span></span>
3. <span data-ttu-id="6b7ab-123">Puede aplicar la directiva cuando se crea una conexión de S2S o entre redes virtuales</span><span class="sxs-lookup"><span data-stu-id="6b7ab-123">You can apply the policy when you create a S2S or VNet-to-VNet connection</span></span>
4. <span data-ttu-id="6b7ab-124">Si ya se ha creado la conexión, puede aplicar la directiva a una conexión existente o actualizarla.</span><span class="sxs-lookup"><span data-stu-id="6b7ab-124">If the connection is already created, you can apply or update the policy to an existing connection</span></span>


## <a name="ipsecike-policy-faq"></a><span data-ttu-id="6b7ab-125">P+F sobre directivas de IPsec o IKE</span><span class="sxs-lookup"><span data-stu-id="6b7ab-125">IPsec/IKE policy FAQ</span></span>

[!INCLUDE [vpn-gateway-ipsecikepolicy-faq-include](../../includes/vpn-gateway-ipsecikepolicy-faq-include.md)]


## <a name="next-steps"></a><span data-ttu-id="6b7ab-126">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6b7ab-126">Next steps</span></span>
<span data-ttu-id="6b7ab-127">Consulte [Configure IPsec/IKE policy](vpn-gateway-ipsecikepolicy-rm-powershell.md) (Configuración de la directiva de IPsec o IKE) para obtener instrucciones paso a paso acerca de cómo configurar directivas personalizadas de IPsec o IKE en una conexión.</span><span class="sxs-lookup"><span data-stu-id="6b7ab-127">See [Configure IPsec/IKE policy](vpn-gateway-ipsecikepolicy-rm-powershell.md) for step-by-step instructions on configuring custom IPsec/IKE policy on a connection.</span></span>

<span data-ttu-id="6b7ab-128">Consulte también [Conexión de varios dispositivos VPN basados en directivas](vpn-gateway-connect-multiple-policybased-rm-ps.md) para obtener más información sobre la opción UsePolicyBasedTrafficSelectors.</span><span class="sxs-lookup"><span data-stu-id="6b7ab-128">See also [Connect multiple policy-based VPN devices](vpn-gateway-connect-multiple-policybased-rm-ps.md) to learn more about the UsePolicyBasedTrafficSelectors option.</span></span>