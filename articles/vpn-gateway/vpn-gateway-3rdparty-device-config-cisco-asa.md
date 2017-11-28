---
title: "configuración de aaaSample - dispositivos Cisco ASA conectar las puertas de enlace VPN de tooAzure | Documentos de Microsoft"
description: "Este artículo proporciona un ejemplo de configuración para dispositivos Cisco ASA conectar las puertas de enlace VPN de tooAzure."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: 
ms.assetid: a8bfc955-de49-4172-95ac-5257e262d7ea
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/20/2017
ms.author: yushwang
ms.openlocfilehash: dad13e02afe8dad2379db750eb09602e08e8ea99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="sample-configuration-cisco-asa-device-ikev2no-bgp"></a><span data-ttu-id="7e915-103">Ejemplo de configuración: dispositivo Cisco ASA (IKEv2/no BGP)</span><span class="sxs-lookup"><span data-stu-id="7e915-103">Sample configuration: Cisco ASA device (IKEv2/no BGP)</span></span>
<span data-ttu-id="7e915-104">Este artículo proporciona ejemplos de configuraciones para dispositivos Cisco ASA conectar las puertas de enlace VPN de tooAzure.</span><span class="sxs-lookup"><span data-stu-id="7e915-104">This article provides sample configurations for Cisco ASA devices connecting tooAzure VPN gateways.</span></span>

## <a name="device-at-a-glance"></a><span data-ttu-id="7e915-105">Detalles del dispositivo</span><span class="sxs-lookup"><span data-stu-id="7e915-105">Device at a glance</span></span>

|                        |                                   |
| ---                    | ---                               |
| <span data-ttu-id="7e915-106">Fabricante del dispositivo</span><span class="sxs-lookup"><span data-stu-id="7e915-106">Device vendor</span></span>          | <span data-ttu-id="7e915-107">Cisco</span><span class="sxs-lookup"><span data-stu-id="7e915-107">Cisco</span></span>                             |
| <span data-ttu-id="7e915-108">Modelo de dispositivo</span><span class="sxs-lookup"><span data-stu-id="7e915-108">Device model</span></span>           | <span data-ttu-id="7e915-109">ASA (Adaptive Security Appliance)</span><span class="sxs-lookup"><span data-stu-id="7e915-109">ASA (Adaptive Security Appliance)</span></span> |
| <span data-ttu-id="7e915-110">Versión de destino</span><span class="sxs-lookup"><span data-stu-id="7e915-110">Target version</span></span>         | <span data-ttu-id="7e915-111">8.4+</span><span class="sxs-lookup"><span data-stu-id="7e915-111">8.4+</span></span>                              |
| <span data-ttu-id="7e915-112">Modelo probado</span><span class="sxs-lookup"><span data-stu-id="7e915-112">Tested model</span></span>           | <span data-ttu-id="7e915-113">ASA 5505</span><span class="sxs-lookup"><span data-stu-id="7e915-113">ASA 5505</span></span>                          |
| <span data-ttu-id="7e915-114">Versión probada</span><span class="sxs-lookup"><span data-stu-id="7e915-114">Tested version</span></span>         | <span data-ttu-id="7e915-115">9.2</span><span class="sxs-lookup"><span data-stu-id="7e915-115">9.2</span></span>                               |
| <span data-ttu-id="7e915-116">Versión de IKE</span><span class="sxs-lookup"><span data-stu-id="7e915-116">IKE version</span></span>            | <span data-ttu-id="7e915-117">**IKEv2**</span><span class="sxs-lookup"><span data-stu-id="7e915-117">**IKEv2**</span></span>                         |
| <span data-ttu-id="7e915-118">BGP</span><span class="sxs-lookup"><span data-stu-id="7e915-118">BGP</span></span>                    | <span data-ttu-id="7e915-119">**No**</span><span class="sxs-lookup"><span data-stu-id="7e915-119">**No**</span></span>                            |
| <span data-ttu-id="7e915-120">Tipo de puerta de enlace de VPN de Azure</span><span class="sxs-lookup"><span data-stu-id="7e915-120">Azure VPN gateway type</span></span> | <span data-ttu-id="7e915-121">Puerta de enlace de VPN **basada en rutas**</span><span class="sxs-lookup"><span data-stu-id="7e915-121">**Route-based** VPN gateway</span></span>       |
|                        |                                   |

> [!NOTE]
> 1. <span data-ttu-id="7e915-122">configuración de Hola a continuación conecta a un tooan de dispositivos Cisco ASA Azure **basadas en enrutamiento** puerta de enlace VPN mediante la directiva personalizada de IPsec/IKE con la opción "UserPolicyBasedTrafficSelectors", como se describe en [este artículo](vpn-gateway-connect-multiple-policybased-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="7e915-122">hello configuration below connects a Cisco ASA device tooan Azure **route-based** VPN gateway using custom IPsec/IKE policy with "UserPolicyBasedTrafficSelectors" option, as described in [this article](vpn-gateway-connect-multiple-policybased-rm-ps.md).</span></span>
> 2. <span data-ttu-id="7e915-123">Requiere ASA dispositivos toouse **IKEv2** con las configuraciones basadas en lista de acceso, no basada en VTI.</span><span class="sxs-lookup"><span data-stu-id="7e915-123">It requires ASA devices toouse **IKEv2** with access-list-based configurations, not VTI-based.</span></span>
> 3. <span data-ttu-id="7e915-124">Póngase en contacto con las especificaciones de proveedor de dispositivo VPN directiva de Hola de tooensure es compatible con los dispositivos VPN local.</span><span class="sxs-lookup"><span data-stu-id="7e915-124">Please consult with your VPN device vendor specifications tooensure hello policy is supported on your on-premises VPN devices.</span></span>

## <a name="vpn-device-requirements"></a><span data-ttu-id="7e915-125">Requisitos del dispositivo VPN</span><span class="sxs-lookup"><span data-stu-id="7e915-125">VPN device requirements</span></span>
<span data-ttu-id="7e915-126">Puertas de enlace VPN Azure usar túneles de VPN de S2S de tooestablish conjuntos de protocolo de IPsec/IKE estándares.</span><span class="sxs-lookup"><span data-stu-id="7e915-126">Azure VPN gateways use standard IPsec/IKE protocol suites tooestablish S2S VPN tunnels.</span></span> <span data-ttu-id="7e915-127">Consulte demasiado[dispositivos VPN sobre](vpn-gateway-about-vpn-devices.md) para hello detallado parámetros de protocolo IPsec/IKE y algoritmos criptográficos predeterminados para las puertas de enlace de VPN de Azure.</span><span class="sxs-lookup"><span data-stu-id="7e915-127">Refer too[About VPN devices](vpn-gateway-about-vpn-devices.md) for hello detailed IPsec/IKE protocol parameters and default cryptographic algorithms for Azure VPN gateways.</span></span> <span data-ttu-id="7e915-128">Puede especificar opcionalmente Hola exactamente la combinación de algoritmos criptográficos y las ventajas claves para una conexión específica, como se describe en [sobre los requisitos de cifrado](vpn-gateway-about-compliance-crypto.md).</span><span class="sxs-lookup"><span data-stu-id="7e915-128">You can optionally specify hello exact combination of cryptographic algorithms and key strengths for a specific connection as described in [About cryptographic requirements](vpn-gateway-about-compliance-crypto.md).</span></span> <span data-ttu-id="7e915-129">Si selecciona una combinación específica de algoritmos criptográficos y las ventajas claves, asegúrese de que usar correspondientes especificaciones de hello en los dispositivos VPN.</span><span class="sxs-lookup"><span data-stu-id="7e915-129">If you select a specific combination of cryptographic algorithms and key strengths, please make sure you use hello corresponding specifications on your VPN devices.</span></span>

## <a name="single-vpn-tunnel"></a><span data-ttu-id="7e915-130">Un solo túnel VPN</span><span class="sxs-lookup"><span data-stu-id="7e915-130">Single VPN tunnel</span></span>
<span data-ttu-id="7e915-131">Esta topología consta de un solo túnel VPN S2S entre una puerta de enlace de VPN de Azure y el dispositivo VPN local.</span><span class="sxs-lookup"><span data-stu-id="7e915-131">This topology consists of a single S2S VPN tunnel between an Azure VPN gateway and your on-premises VPN device.</span></span> <span data-ttu-id="7e915-132">Opcionalmente puede configurar BGP a través del túnel VPN de Hola.</span><span class="sxs-lookup"><span data-stu-id="7e915-132">You can optionally configure BGP across hello VPN tunnel.</span></span>

![túnel único](./media/vpn-gateway-3rdparty-device-config-cisco-asa/singletunnel.png)

<span data-ttu-id="7e915-134">Consulte demasiado[el programa de instalación único túnel](vpn-gateway-3rdparty-device-config-overview.md#singletunnel) para obtener, instrucciones paso a paso toobuild Hola configuraciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="7e915-134">Refer too[Single tunnel setup](vpn-gateway-3rdparty-device-config-overview.md#singletunnel) for detailed, step-by-step instructions toobuild hello Azure configurations.</span></span>

### <a name="network-and-vpn-gateway-information"></a><span data-ttu-id="7e915-135">Información de puerta de enlace de VPN y de red</span><span class="sxs-lookup"><span data-stu-id="7e915-135">Network and VPN gateway information</span></span>
<span data-ttu-id="7e915-136">En esta sección se indican los parámetros de Hola para hello en este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="7e915-136">This section list hello parameters for hello this sample.</span></span>

| <span data-ttu-id="7e915-137">**Parámetro**</span><span class="sxs-lookup"><span data-stu-id="7e915-137">**Parameter**</span></span>                | <span data-ttu-id="7e915-138">**Valor**</span><span class="sxs-lookup"><span data-stu-id="7e915-138">**Value**</span></span>                    |
| ---                          | ---                          |
| <span data-ttu-id="7e915-139">Prefijos de dirección de red virtual</span><span class="sxs-lookup"><span data-stu-id="7e915-139">VNet address prefixes</span></span>        | <span data-ttu-id="7e915-140">10.11.0.0/16</span><span class="sxs-lookup"><span data-stu-id="7e915-140">10.11.0.0/16</span></span><br><span data-ttu-id="7e915-141">10.12.0.0/16</span><span class="sxs-lookup"><span data-stu-id="7e915-141">10.12.0.0/16</span></span> |
| <span data-ttu-id="7e915-142">IP de la puerta de enlace de VPN de Azure</span><span class="sxs-lookup"><span data-stu-id="7e915-142">Azure VPN gateway IP</span></span>         | <span data-ttu-id="7e915-143">Azure_Gateway_Public_IP</span><span class="sxs-lookup"><span data-stu-id="7e915-143">Azure_Gateway_Public_IP</span></span>      |
| <span data-ttu-id="7e915-144">Prefijos de direcciones locales</span><span class="sxs-lookup"><span data-stu-id="7e915-144">On-premises address prefixes</span></span> | <span data-ttu-id="7e915-145">10.51.0.0/16</span><span class="sxs-lookup"><span data-stu-id="7e915-145">10.51.0.0/16</span></span><br><span data-ttu-id="7e915-146">10.52.0.0/16</span><span class="sxs-lookup"><span data-stu-id="7e915-146">10.52.0.0/16</span></span> |
| <span data-ttu-id="7e915-147">Dirección IP del dispositivo VPN local</span><span class="sxs-lookup"><span data-stu-id="7e915-147">On-premises VPN device IP</span></span>    | <span data-ttu-id="7e915-148">OnPrem_Device_Public_IP</span><span class="sxs-lookup"><span data-stu-id="7e915-148">OnPrem_Device_Public_IP</span></span>     |
| <span data-ttu-id="7e915-149">*ASN de BGP de red virtual</span><span class="sxs-lookup"><span data-stu-id="7e915-149">*VNet BGP ASN</span></span>                | <span data-ttu-id="7e915-150">65010</span><span class="sxs-lookup"><span data-stu-id="7e915-150">65010</span></span>                        |
| <span data-ttu-id="7e915-151">*Dirección IP del par BGP de Azure</span><span class="sxs-lookup"><span data-stu-id="7e915-151">*Azure BGP peer IP</span></span>           | <span data-ttu-id="7e915-152">10.12.255.30</span><span class="sxs-lookup"><span data-stu-id="7e915-152">10.12.255.30</span></span>                 |
| <span data-ttu-id="7e915-153">*ASN de BGP local</span><span class="sxs-lookup"><span data-stu-id="7e915-153">*On-premises BGP ASN</span></span>         | <span data-ttu-id="7e915-154">65050</span><span class="sxs-lookup"><span data-stu-id="7e915-154">65050</span></span>                        |
| <span data-ttu-id="7e915-155">*Dirección IP del par BGP local</span><span class="sxs-lookup"><span data-stu-id="7e915-155">*On-premises BGP peer IP</span></span>     | <span data-ttu-id="7e915-156">10.52.255.254</span><span class="sxs-lookup"><span data-stu-id="7e915-156">10.52.255.254</span></span>                |
|                              |                              |

* <span data-ttu-id="7e915-157">(*) Parámetros opcionales solo para BGP.</span><span class="sxs-lookup"><span data-stu-id="7e915-157">(*) Optional parameters for BGP only.</span></span>

### <a name="ipsecike-policy--parameters"></a><span data-ttu-id="7e915-158">Parámetros y directivas de IPsec o IKE</span><span class="sxs-lookup"><span data-stu-id="7e915-158">IPsec/IKE policy & parameters</span></span>

<span data-ttu-id="7e915-159">tabla de Hello siguiente contiene algoritmos de IPsec/IKE de Hola y parámetros utilizados en el ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="7e915-159">hello table below lists hello IPsec/IKE algorithms and parameters used in hello sample.</span></span> <span data-ttu-id="7e915-160">Consulte la toomake de especificaciones de dispositivo VPN que todos los algoritmos enumerados anteriormente son compatibles con los modelos de dispositivo VPN y las versiones de firmware.</span><span class="sxs-lookup"><span data-stu-id="7e915-160">Please consult your VPN device specifications toomake sure all algorithms listed above are supported by your VPN device models and firmware versions.</span></span>

| <span data-ttu-id="7e915-161">**IPsec o IKEv2**</span><span class="sxs-lookup"><span data-stu-id="7e915-161">**IPsec/IKEv2**</span></span>  | <span data-ttu-id="7e915-162">**Valor**</span><span class="sxs-lookup"><span data-stu-id="7e915-162">**Value**</span></span>                            |
| ---              | ---                                  |
| <span data-ttu-id="7e915-163">Cifrado IKEv2</span><span class="sxs-lookup"><span data-stu-id="7e915-163">IKEv2 Encryption</span></span> | <span data-ttu-id="7e915-164">AES256</span><span class="sxs-lookup"><span data-stu-id="7e915-164">AES256</span></span>                               |
| <span data-ttu-id="7e915-165">Integridad de IKEv2</span><span class="sxs-lookup"><span data-stu-id="7e915-165">IKEv2 Integrity</span></span>  | <span data-ttu-id="7e915-166">SHA384</span><span class="sxs-lookup"><span data-stu-id="7e915-166">SHA384</span></span>                               |
| <span data-ttu-id="7e915-167">Grupo DH</span><span class="sxs-lookup"><span data-stu-id="7e915-167">DH Group</span></span>         | <span data-ttu-id="7e915-168">DHGroup24</span><span class="sxs-lookup"><span data-stu-id="7e915-168">DHGroup24</span></span>                            |
| <span data-ttu-id="7e915-169">Cifrado IPsec</span><span class="sxs-lookup"><span data-stu-id="7e915-169">IPsec Encryption</span></span> | <span data-ttu-id="7e915-170">AES256</span><span class="sxs-lookup"><span data-stu-id="7e915-170">AES256</span></span>                               |
| <span data-ttu-id="7e915-171">Integridad de IPsec</span><span class="sxs-lookup"><span data-stu-id="7e915-171">IPsec Integrity</span></span>  | <span data-ttu-id="7e915-172">SHA1</span><span class="sxs-lookup"><span data-stu-id="7e915-172">SHA1</span></span>                                 |
| <span data-ttu-id="7e915-173">Grupo PFS</span><span class="sxs-lookup"><span data-stu-id="7e915-173">PFS Group</span></span>        | <span data-ttu-id="7e915-174">PFS24</span><span class="sxs-lookup"><span data-stu-id="7e915-174">PFS24</span></span>                                |
| <span data-ttu-id="7e915-175">Vigencia de SA (QM)</span><span class="sxs-lookup"><span data-stu-id="7e915-175">QM SA Lifetime</span></span>   | <span data-ttu-id="7e915-176">7200 segundos</span><span class="sxs-lookup"><span data-stu-id="7e915-176">7200 seconds</span></span>                         |
| <span data-ttu-id="7e915-177">Selector de tráfico</span><span class="sxs-lookup"><span data-stu-id="7e915-177">Traffic Selector</span></span> | <span data-ttu-id="7e915-178">UsePolicyBasedTrafficSelectors $True</span><span class="sxs-lookup"><span data-stu-id="7e915-178">UsePolicyBasedTrafficSelectors $True</span></span> |
| <span data-ttu-id="7e915-179">Clave previamente compartida</span><span class="sxs-lookup"><span data-stu-id="7e915-179">Pre-Shared Key</span></span>   | <span data-ttu-id="7e915-180">PreSharedKey</span><span class="sxs-lookup"><span data-stu-id="7e915-180">PreSharedKey</span></span>                         |
|                  |                                      |

- <span data-ttu-id="7e915-181">(*) En algunos dispositivos, la integridad de IPsec debe ser "null" si se usa AES GCM como algoritmo de cifrado de IPsec.</span><span class="sxs-lookup"><span data-stu-id="7e915-181">(*) On some device, IPsec integrity must be "null" if GCM-AES is used as IPsec encryption algorithm.</span></span>

### <a name="device-notes"></a><span data-ttu-id="7e915-182">Notas del dispositivo</span><span class="sxs-lookup"><span data-stu-id="7e915-182">Device notes</span></span>

>[!NOTE]
>
> 1. <span data-ttu-id="7e915-183">La compatibilidad con IKEv2 requiere ASA versión 8.4 y versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="7e915-183">IKEv2 support requires ASA version 8.4 and above.</span></span>
> 2. <span data-ttu-id="7e915-184">La compatibilidad con grupos DH y PFS superiores (por encima del Grupo 5) requiere la versión ASA 9.x.</span><span class="sxs-lookup"><span data-stu-id="7e915-184">Higher DH and PFS group support (beyond Group 5) requires ASA version 9.x.</span></span>
> 3. <span data-ttu-id="7e915-185">Cifrado IPsec con AES-GCM e integridad IPsec con compatibilidad con SHA-256, SHA-384, SHA-512 requiere la versión ASA 9.x en el hardware ASA más reciente; **no** se admite ASA 5505, 5510, 5520, 5540, 5550, 5580.</span><span class="sxs-lookup"><span data-stu-id="7e915-185">IPsec encryption with AES-GCM and IPsec integrity with SHA-256, SHA-384, SHA-512 support requires ASA version 9.x on newer ASA hardware; ASA 5505, 5510, 5520, 5540, 5550, 5580 are **not** supported.</span></span> <span data-ttu-id="7e915-186">(Compruebe Hola proveedor especificaciones tooconfirm.)</span><span class="sxs-lookup"><span data-stu-id="7e915-186">(Please check hello vendor specifications tooconfirm.)</span></span>
>


### <a name="sample-device-configurations"></a><span data-ttu-id="7e915-187">Ejemplos de configuraciones de dispositivo</span><span class="sxs-lookup"><span data-stu-id="7e915-187">Sample device configurations</span></span>
<span data-ttu-id="7e915-188">script de Hola siguiente proporciona un ejemplo de configuración en función de la topología de Hola y los parámetros mencionados anteriormente.</span><span class="sxs-lookup"><span data-stu-id="7e915-188">hello script below provides a sample configuration based on hello topology and parameters listed above.</span></span> <span data-ttu-id="7e915-189">configuración de un túnel VPN S2S Hola consta de hello siguientes componentes:</span><span class="sxs-lookup"><span data-stu-id="7e915-189">hello S2S VPN tunnel configuration consists of hello following parts:</span></span>

1. <span data-ttu-id="7e915-190">Interfaces y rutas</span><span class="sxs-lookup"><span data-stu-id="7e915-190">Interfaces & routes</span></span>
2. <span data-ttu-id="7e915-191">Listas de acceso</span><span class="sxs-lookup"><span data-stu-id="7e915-191">Access lists</span></span>
3. <span data-ttu-id="7e915-192">Directiva y parámetros de IKE (Fase 1 o Modo principal)</span><span class="sxs-lookup"><span data-stu-id="7e915-192">IKE policy and parameters (Phase 1 or Main Mode)</span></span>
4. <span data-ttu-id="7e915-193">Directiva y parámetros de IPsec (Fase 2 o Modo rápido)</span><span class="sxs-lookup"><span data-stu-id="7e915-193">IPsec policy and parameters (Phase 2 or Quick Mode)</span></span>
5. <span data-ttu-id="7e915-194">Otros parámetros (bloqueo MSS de TCP, etc.)</span><span class="sxs-lookup"><span data-stu-id="7e915-194">Other parameters (TCP MSS clamping, etc.)</span></span>

>[!IMPORTANT] 
><span data-ttu-id="7e915-195">Asegúrese de completar la configuración adicional de hello enumerada a continuación y reemplace los marcadores de posición de hello con valores reales de hello:</span><span class="sxs-lookup"><span data-stu-id="7e915-195">Please make sure you complete hello additional configuration listed below and replace hello placeholders with hello actual values:</span></span>
> 
> - <span data-ttu-id="7e915-196">Configuración de interfaz para interfaces internas y externas</span><span class="sxs-lookup"><span data-stu-id="7e915-196">Interface configuration for both inside and outside interfaces</span></span>
> - <span data-ttu-id="7e915-197">Rutas para las redes internas o privadas, y públicas o externas</span><span class="sxs-lookup"><span data-stu-id="7e915-197">Routes for your inside/private and outside/public networks</span></span>
> - <span data-ttu-id="7e915-198">Asegúrese de que todos los nombres y números de directiva son únicos en el dispositivo de Hola</span><span class="sxs-lookup"><span data-stu-id="7e915-198">Ensure all names and policy numbers are unique on hello device</span></span>
> - <span data-ttu-id="7e915-199">Asegúrese de que se admiten los algoritmos criptográficos de hello en el dispositivo</span><span class="sxs-lookup"><span data-stu-id="7e915-199">Ensure hello cryptographic algorithms are supported on your device</span></span>
> - <span data-ttu-id="7e915-200">Reemplace Hola siguientes marcadores de posición con valores reales de Hola</span><span class="sxs-lookup"><span data-stu-id="7e915-200">Replace hello following place holders with hello actual values</span></span>
>   - <span data-ttu-id="7e915-201">Nombre de la interfaz externa: "outside"</span><span class="sxs-lookup"><span data-stu-id="7e915-201">Outside interface name: "outside"</span></span>
>   - <span data-ttu-id="7e915-202">Azure_Gateway_Public_IP</span><span class="sxs-lookup"><span data-stu-id="7e915-202">Azure_Gateway_Public_IP</span></span>
>   - <span data-ttu-id="7e915-203">OnPrem_Device_Public_IP</span><span class="sxs-lookup"><span data-stu-id="7e915-203">OnPrem_Device_Public_IP</span></span>
>   - <span data-ttu-id="7e915-204">Pre_Shared_Key de IKE</span><span class="sxs-lookup"><span data-stu-id="7e915-204">IKE Pre_Shared_Key</span></span>
>   - <span data-ttu-id="7e915-205">Nombres de la red virtual y la puerta de enlace de red local (VNetName, LNGName)</span><span class="sxs-lookup"><span data-stu-id="7e915-205">VNet and local network gateway names (VNetName, LNGName)</span></span>
>   - <span data-ttu-id="7e915-206">Prefijos de direcciones de red de la red virtual y local</span><span class="sxs-lookup"><span data-stu-id="7e915-206">VNet and on-premises network address prefixes</span></span>
>   - <span data-ttu-id="7e915-207">Máscaras de red correctas</span><span class="sxs-lookup"><span data-stu-id="7e915-207">Proper netmasks</span></span>

#### <a name="sample-configuration"></a><span data-ttu-id="7e915-208">Configuración de ejemplo</span><span class="sxs-lookup"><span data-stu-id="7e915-208">Sample configuration</span></span>

```
! Sample ASA configuration for connecting tooAzure VPN gateway
!
! Tested hardware: ASA 5505
! Tested version:  ASA version 9.2(4)
!
! Replace hello following place holders with your actual values:
!   - Interface names - default are "outside" and "inside"
!   - <Azure_Gateway_Public_IP>
!   - <OnPrem_Device_Public_IP>
!   - <Pre_Shared_Key>
!   - <VNetName>*
!   - <LNGName>* ==> LocalNetworkGateway - hello Azure resource that represents the
!     on-premises network, specifies network prefixes, device public IP, BGP info, etc.
!   - <PrivateIPAddress> ==> Replace it with a private IP address if applicable
!   - <Netmask> ==> Replace it with appropriate netmasks
!   - <Nexthop> ==> Replace it with hello actual nexthop IP address
!
! (*) Must be unique names in hello device configuration
!
! ==> Interface & route configurations
!
!     > <OnPrem_Device_Public_IP> address on hello outside interface or vlan
!     > <PrivateIPAddress> on hello inside interface or vlan; e.g., 10.51.0.1/24
!     > Route tooconnect too<Azure_Gateway_Public_IP> address
!
!     > Example:
!
!       interface Ethernet0/0
!        switchport access vlan 2
!       exit
!
!       interface vlan 1
!        nameif inside
!        security-level 100
!        ip address <PrivateIPAddress> <Netmask>
!       exit
!
!       interface vlan 2
!        nameif outside
!        security-level 0
!        ip address <OnPrem_Device_Public_IP> <Netmask>
!       exit
!
!       route outside 0.0.0.0 0.0.0.0 <NextHop IP> 1
!
! ==> Access lists
!
!     > Most firewall devices deny all traffic by default. Create access lists to
!       (1) Allow S2S VPN tunnels between hello ASA and hello Azure gateway public IP address
!       (2) Construct traffic selectors as part of IPsec policy or proposal
!
access-list outside_access_in extended permit ip host <Azure_Gateway_Public_IP> host <OnPrem_Device_Public_IP>
!
!     > Object group that consists of all VNet prefixes (e.g., 10.11.0.0/16 &
!       10.12.0.0/16)
!
object-group network Azure-<VNetName>
 description Azure virtual network <VNetName> prefixes
 network-object 10.11.0.0 255.255.0.0
 network-object 10.12.0.0 255.255.0.0
exit
!
!     > Object group that corresponding toohello <LNGName> prefixes.
!       E.g., 10.51.0.0/16 and 10.52.0.0/16. Note that LNG = "local network gateway".
!       In Azure network resource, a local network gateway defines hello on-premises
!       network properties (address prefixes, VPN device IP, BGP ASN, etc.)
!
object-group network <LNGName>
 description On-Premises network <LNGName> prefixes
 network-object 10.51.0.0 255.255.0.0
 network-object 10.52.0.0 255.255.0.0
exit
!
!     > Specify hello access-list between hello Azure VNet and your on-premises network.
!       This access list defines hello IPsec SA traffic selectors.
!
access-list Azure-<VNetName>-acl extended permit ip object-group <LNGName> object-group Azure-<VNetName>
!
!     > No NAT required between hello on-premises network and Azure VNet
!
nat (inside,outside) source static <LNGName> <LNGName> destination static Azure-<VNetName> Azure-<VNetName>
!
! ==> IKEv2 configuration
!
!     > General IKEv2 configuration - enable IKEv2 for VPN
!
group-policy DfltGrpPolicy attributes
 vpn-tunnel-protocol ikev1 ikev2
exit
!
crypto isakmp identity address
crypto ikev2 enable outside
!
!     > Define IKEv2 Phase 1/Main Mode policy
!       - Make sure hello policy number is not used
!       - integrity and prf must be hello same
!       - DH group 14 and above require ASA version 9.x.
!
crypto ikev2 policy 1
 encryption       aes-256
 integrity        sha384
 prf              sha384
 group            24
 lifetime seconds 86400
exit
!
!     > Set connection type and pre-shared key
!
tunnel-group <Azure_Gateway_Public_IP> type ipsec-l2l
tunnel-group <Azure_Gateway_Public_IP> ipsec-attributes
 ikev2 remote-authentication pre-shared-key <Pre_Shared_Key> 
 ikev2 local-authentication  pre-shared-key <Pre_Shared_Key> 
exit
!
! ==> IPsec configuration
!
!     > IKEv2 Phase 2/Quick Mode proposal
!       - AES-GCM and SHA-2 requires ASA version 9.x on newer ASA models. ASA
!         5505, 5510, 5520, 5540, 5550, 5580 are not supported.
!       - ESP integrity must be null if AES-GCM is configured as ESP encryption
!
crypto ipsec ikev2 ipsec-proposal AES-256
 protocol esp encryption aes-256
 protocol esp integrity  sha-1
exit
!
!     > Set access list & traffic selectors, PFS, IPsec protposal, SA lifetime
!       - This sample uses "Azure-<VNetName>-map" as hello crypto map name
!       - ASA supports only one crypto map per interface, if you already have
!         an existing crypto map assigned tooyour outside interface, you must use
!         hello same crypto map name, but with a different sequence number for
!         this policy
!       - "match address" policy uses hello access-list "Azure-<VNetName>-acl" defined 
!         previously
!       - "ipsec-proposal" uses hello proposal "AES-256" defined previously 
!       - PFS groups 14 and beyond requires ASA version 9.x.
!
crypto map Azure-<VNetName>-map 1 match address Azure-<VNetName>-acl
crypto map Azure-<VNetName>-map 1 set pfs group24
crypto map Azure-<VNetName>-map 1 set peer <Azure_Gateway_Public_IP>
crypto map Azure-<VNetName>-map 1 set ikev2 ipsec-proposal AES-256
crypto map Azure-<VNetName>-map 1 set security-association lifetime seconds 7200
crypto map Azure-<VNetName>-map interface outside
!
! ==> Set TCP MSS too1350
!
sysopt connection tcpmss 1350
!
```

## <a name="simple-debugging-commands"></a><span data-ttu-id="7e915-209">Comandos de depuración simples</span><span class="sxs-lookup"><span data-stu-id="7e915-209">Simple debugging commands</span></span>

<span data-ttu-id="7e915-210">Estos son algunos comandos de ASA para fines de depuración:</span><span class="sxs-lookup"><span data-stu-id="7e915-210">Here are some ASA commands for debugging purposes:</span></span>

1. <span data-ttu-id="7e915-211">Mostrar Hola IPsec e IKE SA</span><span class="sxs-lookup"><span data-stu-id="7e915-211">Show hello IPsec and IKE SA's</span></span>
    - <span data-ttu-id="7e915-212">"show crypto ipsec sa"</span><span class="sxs-lookup"><span data-stu-id="7e915-212">"show crypto ipsec sa"</span></span>
    - <span data-ttu-id="7e915-213">"show crypto ikev2 sa"</span><span class="sxs-lookup"><span data-stu-id="7e915-213">"show crypto ikev2 sa"</span></span>
2. <span data-ttu-id="7e915-214">Al escribir el modo de depuración: Esto puede obtener con mucho ruido en la consola de Hola</span><span class="sxs-lookup"><span data-stu-id="7e915-214">Entering debug mode - this can get very noisy on hello console</span></span>
    - <span data-ttu-id="7e915-215">"debug crypto ikev2 platform <level>"</span><span class="sxs-lookup"><span data-stu-id="7e915-215">"debug crypto ikev2 platform <level>"</span></span>
    - <span data-ttu-id="7e915-216">"debug crypto ikev2 protocol <level>"</span><span class="sxs-lookup"><span data-stu-id="7e915-216">"debug crypto ikev2 protocol <level>"</span></span>
3. <span data-ttu-id="7e915-217">Enumerar configuraciones actuales</span><span class="sxs-lookup"><span data-stu-id="7e915-217">List current configurations</span></span>
    - <span data-ttu-id="7e915-218">"show ejecución" - muestra Hola configuraciones actuales en el dispositivo de hello; Puede usar Hola varios subcomandos toolist determinadas partes de configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="7e915-218">"show run" - shows hello current configurations on hello device; you can use hello various sub-commands toolist specific parts of hello configuration.</span></span> <span data-ttu-id="7e915-219">Por ejemplo, "show run crypto", "show run access-list", "show run tunnel-group", etc.</span><span class="sxs-lookup"><span data-stu-id="7e915-219">E.g., "show run crypto", "show run access-list", "show run tunnel-group", etc.</span></span>


## <a name="next-steps"></a><span data-ttu-id="7e915-220">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7e915-220">Next steps</span></span>
<span data-ttu-id="7e915-221">Vea [configuración activo / activo VPN las puertas de enlace para las conexiones de red virtual a red virtual y entre entornos](vpn-gateway-activeactive-rm-powershell.md) para las conexiones de red virtual a red virtual y pasos tooconfigure de activo / activo entre entornos.</span><span class="sxs-lookup"><span data-stu-id="7e915-221">See [Configuring Active-Active VPN Gateways for Cross-Premises and VNet-to-VNet Connections](vpn-gateway-activeactive-rm-powershell.md) for steps tooconfigure active-active cross-premises and VNet-to-VNet connections.</span></span>

