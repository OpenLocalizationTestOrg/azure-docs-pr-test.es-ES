---
title: 'Configurar una directiva de IPsec o IKE para conexiones VPN de sitio a sitio o de red virtual a red virtual: Azure Resource Manager: PowerShell | Microsoft Docs'
description: "Este artículo le guiará a la hora de configurar una directiva de IPsec o IKE para conexiones de sitio a sitio o de red virtual a red virtual con puertas de enlace de VPN de Azure mediante Azure Resource Manager y PowerShell."
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
ms.date: 05/12/2017
ms.author: yushwang
ms.openlocfilehash: f8d2e29276efdec7071f2aa0d463b1abd64a5253
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-ipsecike-policy-for-s2s-vpn-or-vnet-to-vnet-connections"></a><span data-ttu-id="2d60b-103">Configurar una directiva de IPsec o IKE para conexiones VPN de sitio a sitio o de red virtual a red virtual</span><span class="sxs-lookup"><span data-stu-id="2d60b-103">Configure IPsec/IKE policy for S2S VPN or VNet-to-VNet connections</span></span>

<span data-ttu-id="2d60b-104">Este artículo le guiará a través de hello pasos tooconfigure directiva IPsec/IKE para las conexiones VPN de sitio a sitio o red virtual a red virtual con el modelo de implementación del Administrador de recursos de Hola y PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2d60b-104">This article walks you through hello steps tooconfigure IPsec/IKE policy for Site-to-Site VPN or VNet-to-VNet connections using hello Resource Manager deployment model and PowerShell.</span></span>

## <span data-ttu-id="2d60b-105"><a name="about"></a>Acerca de los parámetros de la directiva de IPsec e IKE para Azure VPN gateway</span><span class="sxs-lookup"><span data-stu-id="2d60b-105"><a name="about"></a>About IPsec and IKE policy parameters for Azure VPN gateways</span></span>
<span data-ttu-id="2d60b-106">El protocolo IPsec e IKE estándar admite una gran variedad de algoritmos criptográficos en diversas combinaciones.</span><span class="sxs-lookup"><span data-stu-id="2d60b-106">IPsec and IKE protocol standard supports a wide range of cryptographic algorithms in various combinations.</span></span> <span data-ttu-id="2d60b-107">Consulte demasiado[sobre los requisitos cifrados y las puertas de enlace de VPN de Azure](vpn-gateway-about-compliance-crypto.md) toosee cómo esto puede ayudar a garantizar la conectividad de red virtual a red virtual y entre entornos satisface sus requisitos de cumplimiento o seguridad.</span><span class="sxs-lookup"><span data-stu-id="2d60b-107">Refer too[About cryptographic requirements and Azure VPN gateways](vpn-gateway-about-compliance-crypto.md) toosee how this can help ensuring cross-premises and VNet-to-VNet connectivity satisfy your compliance or security requirements.</span></span>

<span data-ttu-id="2d60b-108">Este artículo proporciona instrucciones toocreate y configurar una directiva de IPsec/IKE y aplicar la conexión nueva o existente de tooa:</span><span class="sxs-lookup"><span data-stu-id="2d60b-108">This article provides instructions toocreate and configure an IPsec/IKE policy and apply tooa new or existing connection:</span></span>

* [<span data-ttu-id="2d60b-109">Parte 1 - toocreate de flujo de trabajo y establecer una directiva de IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="2d60b-109">Part 1 - Workflow toocreate and set IPsec/IKE policy</span></span>](#workflow)
* [<span data-ttu-id="2d60b-110">Parte 2: algoritmos criptográficos y niveles de clave admitidos</span><span class="sxs-lookup"><span data-stu-id="2d60b-110">Part 2 - Supported cryptographic algorithms and key strengths</span></span>](#params)
* [<span data-ttu-id="2d60b-111">Parte 3: crear una conexión VPN de sitio a sitio con una directiva de IPsec o IKE</span><span class="sxs-lookup"><span data-stu-id="2d60b-111">Part 3 - Create a new S2S VPN connection with IPsec/IKE policy</span></span>](#crossprem)
* [<span data-ttu-id="2d60b-112">Parte 4: crear una conexión de red virtual a red virtual con una directiva de IPsec o IKE</span><span class="sxs-lookup"><span data-stu-id="2d60b-112">Part 4 - Create a new VNet-to-VNet connection with IPsec/IKE policy</span></span>](#vnet2vnet)
* [<span data-ttu-id="2d60b-113">Parte 5: administrar (crear, agregar, quitar) una directiva de IPsec o IKE para una conexión</span><span class="sxs-lookup"><span data-stu-id="2d60b-113">Part 5 - Manage (create, add, remove) IPsec/IKE policy for a connection</span></span>](#managepolicy)

> [!IMPORTANT]
> 1. <span data-ttu-id="2d60b-114">Tenga en cuenta que la directiva IPsec/IKE solo funciona en hello siguiendo las SKU de puerta de enlace:</span><span class="sxs-lookup"><span data-stu-id="2d60b-114">Note that IPsec/IKE policy only works on hello following gateway SKUs:</span></span>
>    * <span data-ttu-id="2d60b-115">***VpnGw1, VpnGw2, VpnGw3*** (basadas en enrutamiento)</span><span class="sxs-lookup"><span data-stu-id="2d60b-115">***VpnGw1, VpnGw2, VpnGw3*** (route-based)</span></span>
>    * <span data-ttu-id="2d60b-116">***Standard*** y ***HighPerformance*** (basadas en enrutamiento)</span><span class="sxs-lookup"><span data-stu-id="2d60b-116">***Standard*** and ***HighPerformance*** (route-based)</span></span>
> 2. <span data-ttu-id="2d60b-117">Solo se puede especificar ***una*** combinación de directivas para una conexión dada.</span><span class="sxs-lookup"><span data-stu-id="2d60b-117">You can only specify ***one*** policy combination for a given connection.</span></span>
> 3. <span data-ttu-id="2d60b-118">Es preciso especificar todos los algoritmos y parámetros de IKE (modo principal) e IPsec (modo rápido).</span><span class="sxs-lookup"><span data-stu-id="2d60b-118">You must specify all algorithms and parameters for both IKE (Main Mode) and IPsec (Quick Mode).</span></span> <span data-ttu-id="2d60b-119">No se permite la especificación de una directiva parcial.</span><span class="sxs-lookup"><span data-stu-id="2d60b-119">Partial policy specification is not allowed.</span></span>
> 4. <span data-ttu-id="2d60b-120">Consulte las especificaciones de proveedor de dispositivo VPN directiva de Hola de tooensure es compatible con los dispositivos VPN local.</span><span class="sxs-lookup"><span data-stu-id="2d60b-120">Consult with your VPN device vendor specifications tooensure hello policy is supported on your on-premises VPN devices.</span></span> <span data-ttu-id="2d60b-121">S2S o las conexiones de red virtual a red virtual no se pueden establecer si las directivas de hello son incompatibles.</span><span class="sxs-lookup"><span data-stu-id="2d60b-121">S2S or VNet-to-VNet connections cannot establish if hello policies are incompatible.</span></span>

## <span data-ttu-id="2d60b-122"><a name ="workflow"></a>Parte 1 - toocreate de flujo de trabajo y establecer una directiva de IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="2d60b-122"><a name ="workflow"></a>Part 1 - Workflow toocreate and set IPsec/IKE policy</span></span>
<span data-ttu-id="2d60b-123">En esta sección describe el flujo de trabajo de Hola a toocreate y actualización de la directiva de IPsec/IKE con el en una conexión VPN S2S o red virtual a red virtual:</span><span class="sxs-lookup"><span data-stu-id="2d60b-123">This section outlines hello workflow toocreate and update IPsec/IKE policy on a S2S VPN or VNet-to-VNet connection:</span></span>
1. <span data-ttu-id="2d60b-124">Crear una red virtual y una puerta de enlace de VPN</span><span class="sxs-lookup"><span data-stu-id="2d60b-124">Create a virtual network and a VPN gateway</span></span>
2. <span data-ttu-id="2d60b-125">Crear una puerta de enlace de red local para la conexión entre locales, u otra red virtual y puerta de enlace para la conexión de red virtual a red virtual</span><span class="sxs-lookup"><span data-stu-id="2d60b-125">Create a local network gateway for cross premises connection, or another virtual network and gateway for VNet-to-VNet connection</span></span>
3. <span data-ttu-id="2d60b-126">Crear una directiva de IPsec o IKE con los algoritmos y parámetros seleccionados</span><span class="sxs-lookup"><span data-stu-id="2d60b-126">Create an IPsec/IKE policy with selected algorithms and parameters</span></span>
4. <span data-ttu-id="2d60b-127">Crear una conexión (VNet2VNet o IPsec) con la directiva de IPsec/IKE Hola</span><span class="sxs-lookup"><span data-stu-id="2d60b-127">Create a connection (IPsec or VNet2VNet) with hello IPsec/IKE policy</span></span>
5. <span data-ttu-id="2d60b-128">Agregar, actualizar o quitar una directiva de IPsec o IKE para una conexión existente</span><span class="sxs-lookup"><span data-stu-id="2d60b-128">Add/update/remove an IPsec/IKE policy for an existing connection</span></span>

<span data-ttu-id="2d60b-129">instrucciones de Hello en este artículo le ayuda a instalar y configurar las directivas de IPsec/IKE tal y como se muestra en el diagrama de hello:</span><span class="sxs-lookup"><span data-stu-id="2d60b-129">hello instructions in this article helps you set up and configure IPsec/IKE policies as shown in hello diagram:</span></span>

![ipsec-ike-policy](./media/vpn-gateway-ipsecikepolicy-rm-powershell/ipsecikepolicy.png)

## <span data-ttu-id="2d60b-131"><a name ="params"></a>Parte 2: algoritmos criptográficos y niveles de clave admitidos</span><span class="sxs-lookup"><span data-stu-id="2d60b-131"><a name ="params"></a>Part 2 - Supported cryptographic algorithms & key strengths</span></span>

<span data-ttu-id="2d60b-132">Hello tabla siguiente enumeran Hola admitido los algoritmos criptográficos y ventajas claves configurables por los clientes de hello:</span><span class="sxs-lookup"><span data-stu-id="2d60b-132">hello following table lists hello supported cryptographic algorithms and key strengths configurable by hello customers:</span></span>

| <span data-ttu-id="2d60b-133">**IPsec o IKEv2**</span><span class="sxs-lookup"><span data-stu-id="2d60b-133">**IPsec/IKEv2**</span></span>  | <span data-ttu-id="2d60b-134">**Opciones**</span><span class="sxs-lookup"><span data-stu-id="2d60b-134">**Options**</span></span>    |
| ---  | --- 
| <span data-ttu-id="2d60b-135">Cifrado IKEv2</span><span class="sxs-lookup"><span data-stu-id="2d60b-135">IKEv2 Encryption</span></span> | <span data-ttu-id="2d60b-136">AES256, AES192, AES128, DES3, DES</span><span class="sxs-lookup"><span data-stu-id="2d60b-136">AES256, AES192, AES128, DES3, DES</span></span>  
| <span data-ttu-id="2d60b-137">Integridad de IKEv2</span><span class="sxs-lookup"><span data-stu-id="2d60b-137">IKEv2 Integrity</span></span>  | <span data-ttu-id="2d60b-138">SHA384, SHA256, SHA1, MD5</span><span class="sxs-lookup"><span data-stu-id="2d60b-138">SHA384, SHA256, SHA1, MD5</span></span>  |
| <span data-ttu-id="2d60b-139">Grupo DH</span><span class="sxs-lookup"><span data-stu-id="2d60b-139">DH Group</span></span>         | <span data-ttu-id="2d60b-140">DHGroup24, ECP384, ECP256, DHGroup14, DHGroup2048, DHGroup2, DHGroup1, No</span><span class="sxs-lookup"><span data-stu-id="2d60b-140">DHGroup24, ECP384, ECP256, DHGroup14, DHGroup2048, DHGroup2, DHGroup1, None</span></span> |
| <span data-ttu-id="2d60b-141">Cifrado IPsec</span><span class="sxs-lookup"><span data-stu-id="2d60b-141">IPsec Encryption</span></span> | <span data-ttu-id="2d60b-142">GCMAES256, GCMAES192, GCMAES128, AES256, AES192, AES128, DES3, DES, No</span><span class="sxs-lookup"><span data-stu-id="2d60b-142">GCMAES256, GCMAES192, GCMAES128, AES256, AES192, AES128, DES3, DES, None</span></span>    |
| <span data-ttu-id="2d60b-143">Integridad de IPsec</span><span class="sxs-lookup"><span data-stu-id="2d60b-143">IPsec Integrity</span></span>  | <span data-ttu-id="2d60b-144">GCMASE256, GCMAES192, GCMAES128, SHA256, SHA1, MD5</span><span class="sxs-lookup"><span data-stu-id="2d60b-144">GCMASE256, GCMAES192, GCMAES128, SHA256, SHA1, MD5</span></span> |
| <span data-ttu-id="2d60b-145">Grupo PFS</span><span class="sxs-lookup"><span data-stu-id="2d60b-145">PFS Group</span></span>        | <span data-ttu-id="2d60b-146">PFS24, ECP384, ECP256, PFS2048, PFS2, PFS1, No</span><span class="sxs-lookup"><span data-stu-id="2d60b-146">PFS24, ECP384, ECP256, PFS2048, PFS2, PFS1, None</span></span> 
| <span data-ttu-id="2d60b-147">Vigencia de SA QM</span><span class="sxs-lookup"><span data-stu-id="2d60b-147">QM SA Lifetime</span></span>   | <span data-ttu-id="2d60b-148">(**Opcional**: Se usan los valores predeterminados si no se especifica ningún valor)</span><span class="sxs-lookup"><span data-stu-id="2d60b-148">(**Optional**: default values are used if not specified)</span></span><br><span data-ttu-id="2d60b-149">Segundos (entero; **mín. 300**/predeterminado 27000 segundos)</span><span class="sxs-lookup"><span data-stu-id="2d60b-149">Seconds (integer; **min. 300**/default 27000 seconds)</span></span><br><span data-ttu-id="2d60b-150">KBytes (entero; **mín. 1024**/predeterminado 102400000 KBytes)</span><span class="sxs-lookup"><span data-stu-id="2d60b-150">KBytes (integer; **min. 1024**/default 102400000 KBytes)</span></span>   |
| <span data-ttu-id="2d60b-151">Selector de tráfico</span><span class="sxs-lookup"><span data-stu-id="2d60b-151">Traffic Selector</span></span> | <span data-ttu-id="2d60b-152">UsePolicyBasedTrafficSelectors** ($True/$False; **Opcional**, valor predeterminado $False si no se especifica)</span><span class="sxs-lookup"><span data-stu-id="2d60b-152">UsePolicyBasedTrafficSelectors** ($True/$False; **Optional**, default $False if not specified)</span></span>    |
|  |  |

> [!IMPORTANT]
> 1. <span data-ttu-id="2d60b-153">**Si GCMAES se utiliza para el algoritmo de cifrado de IPsec, debe seleccionar Hola mismo algoritmo GCMAES y longitud de clave para la integridad de IPsec; Por ejemplo, si se usa GCMAES128 para ambos**</span><span class="sxs-lookup"><span data-stu-id="2d60b-153">**If GCMAES is used as for IPsec Encryption algorithm, you must select hello same GCMAES algorithm and key length for IPsec Integrity; for example, using GCMAES128 for both**</span></span>
> 2. <span data-ttu-id="2d60b-154">Duración de la SA de modo principal IKEv2 se fija en 28.800 segundos en puertas de enlace de VPN de Azure Hola</span><span class="sxs-lookup"><span data-stu-id="2d60b-154">IKEv2 Main Mode SA lifetime is fixed at 28,800 seconds on hello Azure VPN gateways</span></span>
> 3. <span data-ttu-id="2d60b-155">Establecer "UsePolicyBasedTrafficSelectors" demasiado$ True en una conexión se configurará Hola VPN de Azure puerta de enlace tooconnect toopolicy firewall basado en VPN local.</span><span class="sxs-lookup"><span data-stu-id="2d60b-155">Setting "UsePolicyBasedTrafficSelectors" too$True on a connection will configure hello Azure VPN gateway tooconnect toopolicy-based VPN firewall on premises.</span></span> <span data-ttu-id="2d60b-156">Si habilita PolicyBasedTrafficSelectors, deberá tooensure que el dispositivo VPN tiene los selectores de tráfico coincidente Hola definidos con todas las combinaciones de los prefijos de (puerta de enlace de red local) de la red local de prefijos de red virtual de Azure de hello, en lugar de-hacia cualquier.</span><span class="sxs-lookup"><span data-stu-id="2d60b-156">If you enable PolicyBasedTrafficSelectors, you need tooensure your VPN device has hello matching traffic selectors defined with all combinations of your on-premises network (local network gateway) prefixes to/from hello Azure virtual network prefixes, instead of any-to-any.</span></span> <span data-ttu-id="2d60b-157">Por ejemplo, si los prefijos de red local son 10.1.0.0/16 y 10.2.0.0/16 y los prefijos de red virtual son 192.168.0.0/16 y 172.16.0.0/16, necesita hello toospecify siguiendo los selectores de tráfico:</span><span class="sxs-lookup"><span data-stu-id="2d60b-157">For example, if your on-premises network prefixes are 10.1.0.0/16 and 10.2.0.0/16, and your virtual network prefixes are 192.168.0.0/16 and 172.16.0.0/16, you need toospecify hello following traffic selectors:</span></span>
>    * <span data-ttu-id="2d60b-158">10.1.0.0/16 <====> 192.168.0.0/16</span><span class="sxs-lookup"><span data-stu-id="2d60b-158">10.1.0.0/16 <====> 192.168.0.0/16</span></span>
>    * <span data-ttu-id="2d60b-159">10.1.0.0/16 <====> 172.16.0.0/16</span><span class="sxs-lookup"><span data-stu-id="2d60b-159">10.1.0.0/16 <====> 172.16.0.0/16</span></span>
>    * <span data-ttu-id="2d60b-160">10.2.0.0/16 <====> 192.168.0.0/16</span><span class="sxs-lookup"><span data-stu-id="2d60b-160">10.2.0.0/16 <====> 192.168.0.0/16</span></span>
>    * <span data-ttu-id="2d60b-161">10.2.0.0/16 <====> 172.16.0.0/16</span><span class="sxs-lookup"><span data-stu-id="2d60b-161">10.2.0.0/16 <====> 172.16.0.0/16</span></span>

<span data-ttu-id="2d60b-162">Para obtener más información sobre los selectores de tráfico basados en directivas, consulte [Connect multiple on-premises policy-based VPN devices](vpn-gateway-connect-multiple-policybased-rm-ps.md) (Conectar varios dispositivos VPN basados en directivas locales).</span><span class="sxs-lookup"><span data-stu-id="2d60b-162">For more information regarding policy-based traffic selectors, see [Connect multiple on-premises policy-based VPN devices](vpn-gateway-connect-multiple-policybased-rm-ps.md).</span></span>

<span data-ttu-id="2d60b-163">Hola tabla siguiente se muestran Hola correspondientes grupos Diffie-Hellman admitidos por la directiva personalizada de hello:</span><span class="sxs-lookup"><span data-stu-id="2d60b-163">hello following table lists hello corresponding Diffie-Hellman Groups supported by hello custom policy:</span></span>

| <span data-ttu-id="2d60b-164">**Grupo Diffie-Hellman**</span><span class="sxs-lookup"><span data-stu-id="2d60b-164">**Diffie-Hellman Group**</span></span>  | <span data-ttu-id="2d60b-165">**Grupo DH**</span><span class="sxs-lookup"><span data-stu-id="2d60b-165">**DHGroup**</span></span>              | <span data-ttu-id="2d60b-166">**Grupo PFS**</span><span class="sxs-lookup"><span data-stu-id="2d60b-166">**PFSGroup**</span></span> | <span data-ttu-id="2d60b-167">**Longitud de clave**</span><span class="sxs-lookup"><span data-stu-id="2d60b-167">**Key length**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="2d60b-168">1</span><span class="sxs-lookup"><span data-stu-id="2d60b-168">1</span></span>                         | <span data-ttu-id="2d60b-169">DHGroup1</span><span class="sxs-lookup"><span data-stu-id="2d60b-169">DHGroup1</span></span>                 | <span data-ttu-id="2d60b-170">PFS1</span><span class="sxs-lookup"><span data-stu-id="2d60b-170">PFS1</span></span>         | <span data-ttu-id="2d60b-171">MODP de 768 bits</span><span class="sxs-lookup"><span data-stu-id="2d60b-171">768-bit MODP</span></span>   |
| <span data-ttu-id="2d60b-172">2</span><span class="sxs-lookup"><span data-stu-id="2d60b-172">2</span></span>                         | <span data-ttu-id="2d60b-173">DHGroup2</span><span class="sxs-lookup"><span data-stu-id="2d60b-173">DHGroup2</span></span>                 | <span data-ttu-id="2d60b-174">PFS2</span><span class="sxs-lookup"><span data-stu-id="2d60b-174">PFS2</span></span>         | <span data-ttu-id="2d60b-175">MODP de 1024 bits</span><span class="sxs-lookup"><span data-stu-id="2d60b-175">1024-bit MODP</span></span>  |
| <span data-ttu-id="2d60b-176">14</span><span class="sxs-lookup"><span data-stu-id="2d60b-176">14</span></span>                        | <span data-ttu-id="2d60b-177">DHGroup14</span><span class="sxs-lookup"><span data-stu-id="2d60b-177">DHGroup14</span></span><br><span data-ttu-id="2d60b-178">DHGroup2048</span><span class="sxs-lookup"><span data-stu-id="2d60b-178">DHGroup2048</span></span> | <span data-ttu-id="2d60b-179">PFS2048</span><span class="sxs-lookup"><span data-stu-id="2d60b-179">PFS2048</span></span>      | <span data-ttu-id="2d60b-180">MODP de 2048 bits</span><span class="sxs-lookup"><span data-stu-id="2d60b-180">2048-bit MODP</span></span>  |
| <span data-ttu-id="2d60b-181">19</span><span class="sxs-lookup"><span data-stu-id="2d60b-181">19</span></span>                        | <span data-ttu-id="2d60b-182">ECP256</span><span class="sxs-lookup"><span data-stu-id="2d60b-182">ECP256</span></span>                   | <span data-ttu-id="2d60b-183">ECP256</span><span class="sxs-lookup"><span data-stu-id="2d60b-183">ECP256</span></span>       | <span data-ttu-id="2d60b-184">ECP de 256 bits</span><span class="sxs-lookup"><span data-stu-id="2d60b-184">256-bit ECP</span></span>    |
| <span data-ttu-id="2d60b-185">20 |</span><span class="sxs-lookup"><span data-stu-id="2d60b-185">20</span></span>                        | <span data-ttu-id="2d60b-186">ECP384</span><span class="sxs-lookup"><span data-stu-id="2d60b-186">ECP384</span></span>                   | <span data-ttu-id="2d60b-187">ECP284</span><span class="sxs-lookup"><span data-stu-id="2d60b-187">ECP284</span></span>       | <span data-ttu-id="2d60b-188">ECP de 384 bits</span><span class="sxs-lookup"><span data-stu-id="2d60b-188">384-bit ECP</span></span>    |
| <span data-ttu-id="2d60b-189">24</span><span class="sxs-lookup"><span data-stu-id="2d60b-189">24</span></span>                        | <span data-ttu-id="2d60b-190">DHGroup24</span><span class="sxs-lookup"><span data-stu-id="2d60b-190">DHGroup24</span></span>                | <span data-ttu-id="2d60b-191">PFS24</span><span class="sxs-lookup"><span data-stu-id="2d60b-191">PFS24</span></span>        | <span data-ttu-id="2d60b-192">MODP de 2048 bits</span><span class="sxs-lookup"><span data-stu-id="2d60b-192">2048-bit MODP</span></span>  |

<span data-ttu-id="2d60b-193">Consulte demasiado[RFC3526](https://tools.ietf.org/html/rfc3526) y [RFC5114](https://tools.ietf.org/html/rfc5114) para obtener más detalles.</span><span class="sxs-lookup"><span data-stu-id="2d60b-193">Refer too[RFC3526](https://tools.ietf.org/html/rfc3526) and [RFC5114](https://tools.ietf.org/html/rfc5114) for more details.</span></span>

## <span data-ttu-id="2d60b-194"><a name ="crossprem"></a>Parte 3: crear una conexión VPN de sitio a sitio con una directiva de IPsec o IKE</span><span class="sxs-lookup"><span data-stu-id="2d60b-194"><a name ="crossprem"></a>Part 3 - Create a new S2S VPN connection with IPsec/IKE policy</span></span>

<span data-ttu-id="2d60b-195">En esta sección le guiará por los pasos de Hola de creación de una conexión VPN de S2S con una directiva de IPsec/IKE.</span><span class="sxs-lookup"><span data-stu-id="2d60b-195">This section walks you through hello steps of creating a S2S VPN connection with an IPsec/IKE policy.</span></span> <span data-ttu-id="2d60b-196">Hello pasos siguientes crean Hola conexión tal y como se muestra en el diagrama de hello:</span><span class="sxs-lookup"><span data-stu-id="2d60b-196">hello following steps create hello connection as shown in hello diagram:</span></span>

![s2s-policy](./media/vpn-gateway-ipsecikepolicy-rm-powershell/s2spolicy.png)

<span data-ttu-id="2d60b-198">Consulte [Creación de una conexión VPN de sitio a sitio](vpn-gateway-create-site-to-site-rm-powershell.md) para obtener instrucciones detalladas sobre cómo crear una conexión VPN de sitio a sitio.</span><span class="sxs-lookup"><span data-stu-id="2d60b-198">See [Create a S2S VPN connection](vpn-gateway-create-site-to-site-rm-powershell.md) for more detailed step-by-step instructions for creating a S2S VPN connection.</span></span>

### <span data-ttu-id="2d60b-199"><a name="before"></a>Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="2d60b-199"><a name="before"></a>Before you begin</span></span>

* <span data-ttu-id="2d60b-200">Compruebe que tiene una suscripción a Azure.</span><span class="sxs-lookup"><span data-stu-id="2d60b-200">Verify that you have an Azure subscription.</span></span> <span data-ttu-id="2d60b-201">Si todavía no la tiene, puede activar sus [ventajas como suscriptor de MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) o registrarse para obtener una [cuenta gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2d60b-201">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="2d60b-202">Instalar cmdlets de PowerShell del Administrador de recursos de Azure de Hola.</span><span class="sxs-lookup"><span data-stu-id="2d60b-202">Install hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="2d60b-203">Vea [información general de Azure PowerShell](/powershell/azure/overview) para obtener más información acerca de cómo instalar los cmdlets de PowerShell de Hola.</span><span class="sxs-lookup"><span data-stu-id="2d60b-203">See [Overview of Azure PowerShell](/powershell/azure/overview) for more information about installing hello PowerShell cmdlets.</span></span>

### <span data-ttu-id="2d60b-204"><a name="createvnet1"></a>Paso 1: crear la red virtual de hello, la puerta de enlace VPN y la puerta de enlace de red local</span><span class="sxs-lookup"><span data-stu-id="2d60b-204"><a name="createvnet1"></a>Step 1 - Create hello virtual network, VPN gateway, and local network gateway</span></span>

#### <a name="1-declare-your-variables"></a><span data-ttu-id="2d60b-205">1. Declaración de las variables</span><span class="sxs-lookup"><span data-stu-id="2d60b-205">1. Declare your variables</span></span>

<span data-ttu-id="2d60b-206">Para este ejercicio, se empieza por declarar las variables.</span><span class="sxs-lookup"><span data-stu-id="2d60b-206">For this exercise, we start by declaring our variables.</span></span> <span data-ttu-id="2d60b-207">Ser seguro de valores de hello tooreplace con su propio cuando se configura para la producción.</span><span class="sxs-lookup"><span data-stu-id="2d60b-207">Be sure tooreplace hello values with your own when configuring for production.</span></span>

```powershell
$Sub1          = "<YourSubscriptionName>"
$RG1           = "TestPolicyRG1"
$Location1     = "East US 2"
$VNetName1     = "TestVNet1"
$FESubName1    = "FrontEnd"
$BESubName1    = "Backend"
$GWSubName1    = "GatewaySubnet"
$VNetPrefix11  = "10.11.0.0/16"
$VNetPrefix12  = "10.12.0.0/16"
$FESubPrefix1  = "10.11.0.0/24"
$BESubPrefix1  = "10.12.0.0/24"
$GWSubPrefix1  = "10.12.255.0/27"
$DNS1          = "8.8.8.8"
$GWName1       = "VNet1GW"
$GW1IPName1    = "VNet1GWIP1"
$GW1IPconf1    = "gw1ipconf1"
$Connection16  = "VNet1toSite6"

$LNGName6      = "Site6"
$LNGPrefix61   = "10.61.0.0/16"
$LNGPrefix62   = "10.62.0.0/16"
$LNGIP6        = "131.107.72.22"
```

#### <a name="2-connect-tooyour-subscription-and-create-a-new-resource-group"></a><span data-ttu-id="2d60b-208">2. Conectar tooyour suscripción y crear un nuevo grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="2d60b-208">2. Connect tooyour subscription and create a new resource group</span></span>

<span data-ttu-id="2d60b-209">Asegúrese de que cambie hello toouse de modo tooPowerShell cmdlets del Administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="2d60b-209">Make sure you switch tooPowerShell mode toouse hello Resource Manager cmdlets.</span></span> <span data-ttu-id="2d60b-210">Para obtener más información, consulte [Uso de Windows PowerShell con el Administrador de recursos](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="2d60b-210">For more information, see [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="2d60b-211">Abra la consola de PowerShell y conectar con tooyour cuenta.</span><span class="sxs-lookup"><span data-stu-id="2d60b-211">Open your PowerShell console and connect tooyour account.</span></span> <span data-ttu-id="2d60b-212">Usar hello después toohelp de ejemplo que conectarse:</span><span class="sxs-lookup"><span data-stu-id="2d60b-212">Use hello following sample toohelp you connect:</span></span>

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="3-create-hello-virtual-network-vpn-gateway-and-local-network-gateway"></a><span data-ttu-id="2d60b-213">3. Crear red virtual de hello, la puerta de enlace VPN y la puerta de enlace de red local</span><span class="sxs-lookup"><span data-stu-id="2d60b-213">3. Create hello virtual network, VPN gateway, and local network gateway</span></span>

<span data-ttu-id="2d60b-214">Hola según muestra crea la red virtual de hello, TestVNet1, con tres subredes y puerta de enlace VPN de Hola.</span><span class="sxs-lookup"><span data-stu-id="2d60b-214">hello following sample creates hello virtual network, TestVNet1, with three subnets, and hello VPN gateway.</span></span> <span data-ttu-id="2d60b-215">Al reemplazar valores, es importante que siempre asigne el nombre GatewaySubnet a la subred de la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="2d60b-215">When substituting values, it's important that you always name your gateway subnet specifically GatewaySubnet.</span></span> <span data-ttu-id="2d60b-216">Si usa otro, se produce un error al crear la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="2d60b-216">If you name it something else, your gateway creation fails.</span></span>

```powershell
$fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1
$besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
$gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1

New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1

$gw1pip1    = New-AzureRmPublicIpAddress -Name $GW1IPName1 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic
$vnet1      = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
$subnet1    = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
$gw1ipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW1IPconf1 -Subnet $subnet1 -PublicIpAddress $gw1pip1

New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 -Location $Location1 -IpConfigurations $gw1ipconf1 -GatewayType Vpn -VpnType RouteBased -GatewaySku HighPerformance

New-AzureRmLocalNetworkGateway -Name $LNGName6 -ResourceGroupName $RG1 -Location $Location1 -GatewayIpAddress $LNGIP6 -AddressPrefix $LNGPrefix61,$LNGPrefix62
```

### <span data-ttu-id="2d60b-217"><a name="s2sconnection"></a>Paso 2: Creación de una conexión VPN de sitio a sitio con una directiva IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="2d60b-217"><a name="s2sconnection"></a>Step 2 - Create a S2S VPN connection with an IPsec/IKE policy</span></span>

#### <a name="1-create-an-ipsecike-policy"></a><span data-ttu-id="2d60b-218">1. Cree una directiva IPsec/IKE.</span><span class="sxs-lookup"><span data-stu-id="2d60b-218">1. Create an IPsec/IKE policy</span></span>

<span data-ttu-id="2d60b-219">Hola siguiente secuencia de comandos de ejemplo crea una directiva de IPsec/IKE con hello siguientes algoritmos y parámetros:</span><span class="sxs-lookup"><span data-stu-id="2d60b-219">hello following sample script creates an IPsec/IKE policy with hello following algorithms and parameters:</span></span>

* <span data-ttu-id="2d60b-220">IKEv2: AES256, SHA384, DHGroup24</span><span class="sxs-lookup"><span data-stu-id="2d60b-220">IKEv2: AES256, SHA384, DHGroup24</span></span>
* <span data-ttu-id="2d60b-221">IPsec: AES256, SHA256, PFS24, vigencia de SA de 7200 segundos y 2048 KB</span><span class="sxs-lookup"><span data-stu-id="2d60b-221">IPsec: AES256, SHA256, PFS24, SA Lifetime 7200 seconds & 2048KB</span></span>

```powershell
$ipsecpolicy6 = New-AzureRmIpsecPolicy -IkeEncryption AES256 -IkeIntegrity SHA384 -DhGroup DHGroup24 -IpsecEncryption AES256 -IpsecIntegrity SHA256 -PfsGroup PFS24 -SALifeTimeSeconds 7200 -SADataSizeKilobytes 2048
```

<span data-ttu-id="2d60b-222">Si usas GCMAES para IPsec, debe utilizar Hola mismo algoritmo GCMAES y longitud de clave para el cifrado de IPsec y la integridad, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="2d60b-222">If you use GCMAES for IPsec, you must use hello same GCMAES algorithm and key length for both IPsec encryption and integrity, for example:</span></span>

* <span data-ttu-id="2d60b-223">IKEv2: AES256, SHA384, DHGroup24</span><span class="sxs-lookup"><span data-stu-id="2d60b-223">IKEv2: AES256, SHA384, DHGroup24</span></span>
* <span data-ttu-id="2d60b-224">IPsec: **GCMAES256, GCMAES256**, PFS24, vigencia de SA de 7200 segundos y 2048 KB</span><span class="sxs-lookup"><span data-stu-id="2d60b-224">IPsec: **GCMAES256, GCMAES256**, PFS24, SA Lifetime 7200 seconds & 2048KB</span></span>

```powershell
$ipsecpolicy6 = New-AzureRmIpsecPolicy -IkeEncryption AES256 -IkeIntegrity SHA384 -DhGroup DHGroup24 -IpsecEncryption GCMAES256 -IpsecIntegrity GCMAES256 -PfsGroup PFS24 -SALifeTimeSeconds 7200 -SADataSizeKilobytes 2048
```

#### <a name="2-create-hello-s2s-vpn-connection-with-hello-ipsecike-policy"></a><span data-ttu-id="2d60b-225">2. Crear la conexión de VPN de S2S de hello con hello directiva IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="2d60b-225">2. Create hello S2S VPN connection with hello IPsec/IKE policy</span></span>

<span data-ttu-id="2d60b-226">Crear una conexión VPN de S2S y aplicar la directiva de IPsec/IKE Hola creado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="2d60b-226">Create an S2S VPN connection and apply hello IPsec/IKE policy created earlier.</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng6 = Get-AzureRmLocalNetworkGateway  -Name $LNGName6 -ResourceGroupName $RG1

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng6 -Location $Location1 -ConnectionType IPsec -IpsecPolicies $ipsecpolicy6 -SharedKey 'AzureA1b2C3'
```

<span data-ttu-id="2d60b-227">Opcionalmente, puede agregar "-UsePolicyBasedTrafficSelectors $True" toohello crear conexión cmdlet tooenable VPN de Azure puerta de enlace tooconnect toopolicy dispositivos basados en VPN local, como se describió anteriormente.</span><span class="sxs-lookup"><span data-stu-id="2d60b-227">You can optionally add "-UsePolicyBasedTrafficSelectors $True" toohello create connection cmdlet tooenable Azure VPN gateway tooconnect toopolicy-based VPN devices on premises, as described above.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2d60b-228">Una vez que una directiva de IPsec/IKE se especifica en una conexión, puerta de enlace de VPN de Azure de hello sólo enviará o Aceptar la propuesta de IPsec/IKE Hola con algoritmos criptográficos especificados y ventajas claves de esa conexión en particular.</span><span class="sxs-lookup"><span data-stu-id="2d60b-228">Once an IPsec/IKE policy is specified on a connection, hello Azure VPN gateway will only send or accept hello IPsec/IKE proposal with specified cryptographic algorithms and key strengths on that particular connection.</span></span> <span data-ttu-id="2d60b-229">Asegúrese de que el dispositivo VPN local para la conexión de hello usa o acepta la combinación de la directiva exacta de hello, en caso contrario, no se establecerá el túnel de VPN de S2S de Hola.</span><span class="sxs-lookup"><span data-stu-id="2d60b-229">Make sure your on-premises VPN device for hello connection uses or accepts hello exact policy combination, otherwise hello S2S VPN tunnel will not establish.</span></span>


## <span data-ttu-id="2d60b-230"><a name ="vnet2vnet"></a>Parte 4: crear una conexión de red virtual a red virtual con una directiva de IPsec o IKE</span><span class="sxs-lookup"><span data-stu-id="2d60b-230"><a name ="vnet2vnet"></a>Part 4 - Create a new VNet-to-VNet connection with IPsec/IKE policy</span></span>

<span data-ttu-id="2d60b-231">pasos de Hola de creación de una conexión de red virtual a red virtual con una directiva de IPsec/IKE son similar toothat de una conexión VPN de S2S.</span><span class="sxs-lookup"><span data-stu-id="2d60b-231">hello steps of creating a VNet-to-VNet connection with an IPsec/IKE policy are similar toothat of a S2S VPN connection.</span></span> <span data-ttu-id="2d60b-232">Hello secuencias de comandos de ejemplo siguientes crean Hola conexión tal y como se muestra en el diagrama de hello:</span><span class="sxs-lookup"><span data-stu-id="2d60b-232">hello following sample scripts create hello connection as shown in hello diagram:</span></span>

![v2v-policy](./media/vpn-gateway-ipsecikepolicy-rm-powershell/v2vpolicy.png)

<span data-ttu-id="2d60b-234">Consulte [Creación de una conexión de red virtual a red virtual](vpn-gateway-vnet-vnet-rm-ps.md) para conocer los pasos detallados para crear una conexión de red virtual a red virtual.</span><span class="sxs-lookup"><span data-stu-id="2d60b-234">See [Create a VNet-to-VNet connection](vpn-gateway-vnet-vnet-rm-ps.md) for more detailed steps for creating a VNet-to-VNet connection.</span></span> <span data-ttu-id="2d60b-235">Debe completar [parte 3](#crossprem) toocreate TestVNet1 y configurar Hola puerta de enlace VPN.</span><span class="sxs-lookup"><span data-stu-id="2d60b-235">You must complete [Part 3](#crossprem) toocreate and configure TestVNet1 and hello VPN Gateway.</span></span>

### <span data-ttu-id="2d60b-236"><a name="createvnet2"></a>Paso 1: crear la segunda red virtual de Hola y puerta de enlace VPN</span><span class="sxs-lookup"><span data-stu-id="2d60b-236"><a name="createvnet2"></a>Step 1 - Create hello second virtual network and VPN gateway</span></span>

#### <a name="1-declare-your-variables"></a><span data-ttu-id="2d60b-237">1. Declaración de las variables</span><span class="sxs-lookup"><span data-stu-id="2d60b-237">1. Declare your variables</span></span>

<span data-ttu-id="2d60b-238">Ser seguro tooreplace valores de hello con hello las que desea que toouse para la configuración.</span><span class="sxs-lookup"><span data-stu-id="2d60b-238">Be sure tooreplace hello values with hello ones that you want toouse for your configuration.</span></span>

```powershell
$RG2          = "TestPolicyRG2"
$Location2    = "East US 2"
$VNetName2    = "TestVNet2"
$FESubName2   = "FrontEnd"
$BESubName2   = "Backend"
$GWSubName2   = "GatewaySubnet"
$VNetPrefix21 = "10.21.0.0/16"
$VNetPrefix22 = "10.22.0.0/16"
$FESubPrefix2 = "10.21.0.0/24"
$BESubPrefix2 = "10.22.0.0/24"
$GWSubPrefix2 = "10.22.255.0/27"
$DNS2         = "8.8.8.8"
$GWName2      = "VNet2GW"
$GW2IPName1   = "VNet2GWIP1"
$GW2IPconf1   = "gw2ipconf1"
$Connection21 = "VNet2toVNet1"
$Connection12 = "VNet1toVNet2"
```

#### <a name="2-create-hello-second-virtual-network-and-vpn-gateway-in-hello-new-resource-group"></a><span data-ttu-id="2d60b-239">2. Crear la segunda red virtual de Hola y puerta de enlace VPN en el nuevo grupo de recursos Hola</span><span class="sxs-lookup"><span data-stu-id="2d60b-239">2. Create hello second virtual network and VPN gateway in hello new resource group</span></span>

```powershell
New-AzureRmResourceGroup -Name $RG2 -Location $Location2

$fesub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName2 -AddressPrefix $FESubPrefix2
$besub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName2 -AddressPrefix $BESubPrefix2
$gwsub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName2 -AddressPrefix $GWSubPrefix2

New-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2 -Location $Location2 -AddressPrefix $VNetPrefix21,$VNetPrefix22 -Subnet $fesub2,$besub2,$gwsub2

$gw2pip1    = New-AzureRmPublicIpAddress -Name $GW2IPName1 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic
$vnet2      = Get-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2
$subnet2    = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet2
$gw2ipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW2IPconf1 -Subnet $subnet2 -PublicIpAddress $gw2pip1

New-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2 -Location $Location2 -IpConfigurations $gw2ipconf1 -GatewayType Vpn -VpnType RouteBased -GatewaySku HighPerformance
```

### <a name="step-2---create-a-vnet-tovnet-connection-with-hello-ipsecike-policy"></a><span data-ttu-id="2d60b-240">Paso 2: crear una conexión de red virtual toVNet con hello directiva IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="2d60b-240">Step 2 - Create a VNet-toVNet connection with hello IPsec/IKE policy</span></span>

<span data-ttu-id="2d60b-241">Toohello similar conexión VPN S2S, cree una directiva de IPsec/IKE, a continuación, se aplican toopolicy toohello nueva conexión.</span><span class="sxs-lookup"><span data-stu-id="2d60b-241">Similar toohello S2S VPN connection, create an IPsec/IKE policy then apply toopolicy toohello new connection.</span></span>

#### <a name="1-create-an-ipsecike-policy"></a><span data-ttu-id="2d60b-242">1. Cree una directiva IPsec/IKE.</span><span class="sxs-lookup"><span data-stu-id="2d60b-242">1. Create an IPsec/IKE policy</span></span>

<span data-ttu-id="2d60b-243">Hola siguiente secuencia de comandos de ejemplo crea una directiva de IPsec/IKE diferente con hello siguientes algoritmos y parámetros:</span><span class="sxs-lookup"><span data-stu-id="2d60b-243">hello following sample script creates a different IPsec/IKE policy with hello following algorithms and parameters:</span></span>
* <span data-ttu-id="2d60b-244">IKEv2: AES128, SHA1, DHGroup14</span><span class="sxs-lookup"><span data-stu-id="2d60b-244">IKEv2: AES128, SHA1, DHGroup14</span></span>
* <span data-ttu-id="2d60b-245">IPsec: GCMAES128, GCMAES128, PFS14, vigencia de SA de 7200 segundos y 4096 KB</span><span class="sxs-lookup"><span data-stu-id="2d60b-245">IPsec: GCMAES128, GCMAES128, PFS14, SA Lifetime 7200 seconds & 4096KB</span></span>

```powershell
$ipsecpolicy2 = New-AzureRmIpsecPolicy -IkeEncryption AES128 -IkeIntegrity SHA1 -DhGroup DHGroup14 -IpsecEncryption GCMAES128 -IpsecIntegrity GCMAES128 -PfsGroup PFS14 -SALifeTimeSeconds 7200 -SADataSizeKilobytes 4096
```

#### <a name="2-create-vnet-to-vnet-connections-with-hello-ipsecike-policy"></a><span data-ttu-id="2d60b-246">2. Crear conexiones de red virtual a red virtual con hello directiva IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="2d60b-246">2. Create VNet-to-VNet connections with hello IPsec/IKE policy</span></span>

<span data-ttu-id="2d60b-247">Crear una conexión de red virtual a red virtual y aplicar directivas de IPsec/IKE de Hola que ha creado.</span><span class="sxs-lookup"><span data-stu-id="2d60b-247">Create a VNet-to-VNet connection and apply hello IPsec/IKE policy you created.</span></span> <span data-ttu-id="2d60b-248">En este ejemplo, las puertas de enlace se encuentran en hello misma suscripción.</span><span class="sxs-lookup"><span data-stu-id="2d60b-248">In this example, both gateways are in hello same subscription.</span></span> <span data-ttu-id="2d60b-249">Por lo que es posible toocreate y configurar las conexiones con Hola misma directiva de IPsec/IKE Hola misma sesión de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2d60b-249">So it is possible toocreate and configure both connections with hello same IPsec/IKE policy in hello same PowerShell session.</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$vnet2gw = Get-AzureRmVirtualNetworkGateway -Name $GWName2  -ResourceGroupName $RG2

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection12 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet2gw -Location $Location1 -ConnectionType Vnet2Vnet -IpsecPolicies $ipsecpolicy2 -SharedKey 'AzureA1b2C3'

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection21 -ResourceGroupName $RG2 -VirtualNetworkGateway1 $vnet2gw -VirtualNetworkGateway2 $vnet1gw -Location $Location2 -ConnectionType Vnet2Vnet -IpsecPolicies $ipsecpolicy2 -SharedKey 'AzureA1b2C3'
```

> [!IMPORTANT]
> <span data-ttu-id="2d60b-250">Una vez que una directiva de IPsec/IKE se especifica en una conexión, puerta de enlace de VPN de Azure de hello sólo enviará o Aceptar la propuesta de IPsec/IKE Hola con algoritmos criptográficos especificados y ventajas claves de esa conexión en particular.</span><span class="sxs-lookup"><span data-stu-id="2d60b-250">Once an IPsec/IKE policy is specified on a connection, hello Azure VPN gateway will only send or accept hello IPsec/IKE proposal with specified cryptographic algorithms and key strengths on that particular connection.</span></span> <span data-ttu-id="2d60b-251">Asegúrese de hello seguro de las directivas IPsec para las conexiones son Hola mismo, en caso contrario, no se establecerá la conexión de red virtual a red virtual.</span><span class="sxs-lookup"><span data-stu-id="2d60b-251">Make sure hello IPsec policies for both connections are hello same, otherwise the VNet-to-VNet connection will not establish.</span></span>

<span data-ttu-id="2d60b-252">Después de completar estos pasos, se establece la conexión de hello en unos minutos y, tendrá Hola siguiendo la topología de red tal y como se muestra en el principio de hello:</span><span class="sxs-lookup"><span data-stu-id="2d60b-252">After completing these steps, hello connection is established in a few minutes, and you will have hello following network topology as shown in hello beginning:</span></span>

![ipsec-ike-policy](./media/vpn-gateway-ipsecikepolicy-rm-powershell/ipsecikepolicy.png)


## <span data-ttu-id="2d60b-254"><a name ="managepolicy"></a>Parte 5: actualizar una directiva de IPsec o IKE para una conexión</span><span class="sxs-lookup"><span data-stu-id="2d60b-254"><a name ="managepolicy"></a>Part 5 - Update IPsec/IKE policy for a connection</span></span>

<span data-ttu-id="2d60b-255">Hola última sección muestra cómo toomanage directiva IPsec/IKE para una conexión de S2S o red virtual a red virtual existente.</span><span class="sxs-lookup"><span data-stu-id="2d60b-255">hello last section shows you how toomanage IPsec/IKE policy for an existing S2S or VNet-to-VNet connection.</span></span> <span data-ttu-id="2d60b-256">ejercicio Hola siguiente le guiará por las siguientes operaciones en una conexión de Hola:</span><span class="sxs-lookup"><span data-stu-id="2d60b-256">hello exercise below walks you through hello following operations on a connection:</span></span>

1. <span data-ttu-id="2d60b-257">Mostrar directiva de IPsec/IKE Hola de una conexión</span><span class="sxs-lookup"><span data-stu-id="2d60b-257">Show hello IPsec/IKE policy of a connection</span></span>
2. <span data-ttu-id="2d60b-258">Agregar o actualizar la conexión de tooa de directiva de IPsec/IKE Hola</span><span class="sxs-lookup"><span data-stu-id="2d60b-258">Add or update hello IPsec/IKE policy tooa connection</span></span>
3. <span data-ttu-id="2d60b-259">Quitar la directiva de IPsec/IKE de Hola de una conexión</span><span class="sxs-lookup"><span data-stu-id="2d60b-259">Remove hello IPsec/IKE policy from a connection</span></span>

<span data-ttu-id="2d60b-260">Hello mismos pasos aplican tooboth S2S y conexiones de red virtual a red virtual.</span><span class="sxs-lookup"><span data-stu-id="2d60b-260">hello same steps apply tooboth S2S and VNet-to-VNet connections.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2d60b-261">La directiva de IPsec o IKE solo se admite en las puertas de enlace de VPN basadas en rutas *Standard* y *HighPerformance*.</span><span class="sxs-lookup"><span data-stu-id="2d60b-261">IPsec/IKE policy is supported on *Standard* and *HighPerformance* route-based VPN gateways only.</span></span> <span data-ttu-id="2d60b-262">No funciona en la puerta de enlace de hello básico SKU o puerta de enlace VPN basada en directivas de Hola.</span><span class="sxs-lookup"><span data-stu-id="2d60b-262">It does not work on hello Basic gateway SKU or hello policy-based VPN gateway.</span></span>

#### <a name="1-show-hello-ipsecike-policy-of-a-connection"></a><span data-ttu-id="2d60b-263">1. Mostrar directiva de IPsec/IKE Hola de una conexión</span><span class="sxs-lookup"><span data-stu-id="2d60b-263">1. Show hello IPsec/IKE policy of a connection</span></span>

<span data-ttu-id="2d60b-264">Hola de ejemplo siguiente muestra cómo tooget Hola configurado en una conexión de directiva de IPsec/IKE.</span><span class="sxs-lookup"><span data-stu-id="2d60b-264">hello following example shows how tooget hello IPsec/IKE policy configured on a connection.</span></span> <span data-ttu-id="2d60b-265">las secuencias de comandos de Hello seguir de ejercicios de hello anteriores.</span><span class="sxs-lookup"><span data-stu-id="2d60b-265">hello scripts also continue from hello exercises above.</span></span>

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1
$connection6.IpsecPolicies
```

<span data-ttu-id="2d60b-266">último comando de Hello enumera directiva IPsec/IKE actual Hola configurado en conexión hello, si hay alguno.</span><span class="sxs-lookup"><span data-stu-id="2d60b-266">hello last command lists hello current IPsec/IKE policy configured on hello connection, if there is any.</span></span> <span data-ttu-id="2d60b-267">Después de la salida de ejemplo de Hola es por conexión hello:</span><span class="sxs-lookup"><span data-stu-id="2d60b-267">hello following sample output is for hello connection:</span></span>

```powershell
SALifeTimeSeconds   : 3600
SADataSizeKilobytes : 2048
IpsecEncryption     : AES256
IpsecIntegrity      : SHA256
IkeEncryption       : AES256
IkeIntegrity        : SHA384
DhGroup             : DHGroup24
PfsGroup            : PFS24
```

<span data-ttu-id="2d60b-268">Si no hay ninguna directiva de IPsec/IKE configurada, Hola comando (PS > $connection6.policy) obtiene vacío devuelto.</span><span class="sxs-lookup"><span data-stu-id="2d60b-268">If there is no IPsec/IKE policy configured, hello command (PS> $connection6.policy) gets an empty return.</span></span> <span data-ttu-id="2d60b-269">No significa IPsec/IKE no está configurado en la conexión de hello, pero que no hay ninguna directiva de IPsec/IKE personalizada.</span><span class="sxs-lookup"><span data-stu-id="2d60b-269">It does not mean IPsec/IKE is not configured on hello connection, but that there is no custom IPsec/IKE policy.</span></span> <span data-ttu-id="2d60b-270">conexión real de Hello usa directiva predeterminada de hello negociado entre el dispositivo VPN en local y Hola puerta de enlace VPN de Azure.</span><span class="sxs-lookup"><span data-stu-id="2d60b-270">hello actual connection uses hello default policy negotiated between your on-premises VPN device and hello Azure VPN gateway.</span></span>

#### <a name="2-add-or-update-an-ipsecike-policy-for-a-connection"></a><span data-ttu-id="2d60b-271">2. Agregar o actualizar una directiva de IPsec o IKE para una conexión</span><span class="sxs-lookup"><span data-stu-id="2d60b-271">2. Add or update an IPsec/IKE policy for a connection</span></span>

<span data-ttu-id="2d60b-272">Hola pasos tooadd una nueva directiva o actualización de una directiva existente en una conexión son Hola mismo: crear una nueva directiva, a continuación, aplicar la nueva conexión de toohello directiva Hola.</span><span class="sxs-lookup"><span data-stu-id="2d60b-272">hello steps tooadd a new policy or update an existing policy on a connection are hello same: create a new policy then apply hello new policy toohello connection.</span></span>

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1

$newpolicy6   = New-AzureRmIpsecPolicy -IkeEncryption AES128 -IkeIntegrity SHA1 -DhGroup DHGroup14 -IpsecEncryption GCMAES128 -IpsecIntegrity GCMAES128 -PfsGroup None -SALifeTimeSeconds 3600 -SADataSizeKilobytes 2048

Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6 -IpsecPolicies $newpolicy6
```

<span data-ttu-id="2d60b-273">tooenable "UsePolicyBasedTrafficSelectors" al conectar tooan locales dispositivo VPN basada en directivas, agregar Hola "-UsePolicyBaseTrafficSelectors" parámetro toohello cmdlet, o establézcala demasiado opción Hola de $ toodisable False:</span><span class="sxs-lookup"><span data-stu-id="2d60b-273">tooenable "UsePolicyBasedTrafficSelectors" when connecting tooan on-premises policy-based VPN device, add hello "-UsePolicyBaseTrafficSelectors" parameter toohello cmdlet, or set it too$False toodisable hello option:</span></span>

```powershell
Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6 -IpsecPolicies $newpolicy6 -UsePolicyBasedTrafficSelectors $True
```

<span data-ttu-id="2d60b-274">Puede obtener la conexión de hello nuevo toocheck si se actualiza la directiva de Hola.</span><span class="sxs-lookup"><span data-stu-id="2d60b-274">You can get hello connection again toocheck if hello policy is updated.</span></span>

```powershell
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1
$connection6.IpsecPolicies
```

<span data-ttu-id="2d60b-275">Debería ver resultados de Hola desde la última línea hello, como se muestra en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="2d60b-275">You should see hello output from hello last line, as shown in hello following example:</span></span>

```powershell
SALifeTimeSeconds   : 3600
SADataSizeKilobytes : 2048
IpsecEncryption     : GCMAES128
IpsecIntegrity      : GCMAES128
IkeEncryption       : AES128
IkeIntegrity        : SHA1
DhGroup             : DHGroup14--
PfsGroup            : None
```

#### <a name="3-remove-an-ipsecike-policy-from-a-connection"></a><span data-ttu-id="2d60b-276">3. Eliminar una directiva de IPsec o IKE de una conexión</span><span class="sxs-lookup"><span data-stu-id="2d60b-276">3. Remove an IPsec/IKE policy from a connection</span></span>

<span data-ttu-id="2d60b-277">Una vez que quita la directiva personalizada de Hola desde una conexión, puerta de enlace de VPN de Azure de hello vuelve atrás toohello [lista predeterminada de las propuestas de IPsec/IKE](vpn-gateway-about-vpn-devices.md) y vuelve a negociar nuevo con el dispositivo VPN local.</span><span class="sxs-lookup"><span data-stu-id="2d60b-277">Once you remove hello custom policy from a connection, hello Azure VPN gateway reverts back toohello [default list of IPsec/IKE proposals](vpn-gateway-about-vpn-devices.md) and renegotiates again with your on-premises VPN device.</span></span>

```powershell
$RG1           = "TestPolicyRG1"
$Connection16  = "VNet1toSite6"
$connection6   = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1

$currentpolicy = $connection6.IpsecPolicies[0]
$connection6.IpsecPolicies.Remove($currentpolicy)

Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6
```

<span data-ttu-id="2d60b-278">Puede usar Hola mismo toocheck de secuencia de comandos si se ha quitado la directiva de Hola de conexión de Hola.</span><span class="sxs-lookup"><span data-stu-id="2d60b-278">You can use hello same script toocheck if hello policy has been removed from hello connection.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2d60b-279">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2d60b-279">Next steps</span></span>

<span data-ttu-id="2d60b-280">Para obtener información sobre los selectores de tráfico basados en directivas, vea [Connect multiple on-premises policy-based VPN devices](vpn-gateway-connect-multiple-policybased-rm-ps.md) (Conectar varios dispositivos VPN basados en directivas locales).</span><span class="sxs-lookup"><span data-stu-id="2d60b-280">See [Connect multiple on-premises policy-based VPN devices](vpn-gateway-connect-multiple-policybased-rm-ps.md) for more details regarding policy-based traffic selectors.</span></span>

<span data-ttu-id="2d60b-281">Una vez completada la conexión, puede agregar redes virtuales de máquinas virtuales tooyour.</span><span class="sxs-lookup"><span data-stu-id="2d60b-281">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="2d60b-282">Consulte [Creación de una máquina virtual que ejecuta Windows en el Portal de Azure](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) para ver los pasos.</span><span class="sxs-lookup"><span data-stu-id="2d60b-282">See [Create a Virtual Machine](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for steps.</span></span>
