---
title: aaaTroubleshoot Azure VPN de sitio a sitio se desconecta de forma intermitente | Documentos de Microsoft
description: "Obtenga información acerca de cómo tootroubleshoot Hola problema de conexión de VPN de sitio a sitio que Hola desconectado con regularidad."
services: vpn-gateway
documentationcenter: na
author: chadmath
manager: cshepard
editor: 
tags: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/21/2017
ms.author: genli
ms.openlocfilehash: 1ce3c4ff9d8f650312e45f33b760ebcc6597fc13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-site-to-site-vpn-disconnects-intermittently"></a><span data-ttu-id="38f3b-103">Solución de problemas: la VPN de sitio a sitio de Azure se desconecta intermitentemente</span><span class="sxs-lookup"><span data-stu-id="38f3b-103">Troubleshooting: Azure Site-to-Site VPN disconnects intermittently</span></span>

<span data-ttu-id="38f3b-104">Puede experimentar problemas de Hola que una conexión de Azure de Microsoft Point-to-Site VPN nueva o existente no es estable o desconecta con regularidad.</span><span class="sxs-lookup"><span data-stu-id="38f3b-104">You might experience hello problem that a new or existing Microsoft Azure Point-to-Site VPN connection is not stable or disconnects regularly.</span></span> <span data-ttu-id="38f3b-105">Este artículo se proporcionan pasos toohelp identificar y resolver Hola causa del problema de Hola de solución de problemas.</span><span class="sxs-lookup"><span data-stu-id="38f3b-105">This article provides troubleshoot steps toohelp you identify and resolve hello cause of hello problem.</span></span> 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="troubleshooting-steps"></a><span data-ttu-id="38f3b-106">Pasos para solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="38f3b-106">Troubleshooting steps</span></span>

### <a name="prerequisite-step"></a><span data-ttu-id="38f3b-107">Paso de requisito previo</span><span class="sxs-lookup"><span data-stu-id="38f3b-107">Prerequisite step</span></span>

<span data-ttu-id="38f3b-108">Seleccione el tipo de saludo de puerta de enlace de red virtual de Azure:</span><span class="sxs-lookup"><span data-stu-id="38f3b-108">Check hello type of Azure  virtual network gateway:</span></span>

1. <span data-ttu-id="38f3b-109">Vaya demasiado[portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="38f3b-109">Go too[Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="38f3b-110">Comprobar hello **Introducción** página de puerta de enlace de red virtual de Hola para obtener información de tipo hello.</span><span class="sxs-lookup"><span data-stu-id="38f3b-110">Check hello **Overview** page of hello virtual network gateway for hello type information.</span></span>
    
    ![información general de Hola de puerta de enlace de Hola](media\vpn-gateway-troubleshoot-site-to-site-disconnected-intermittently\gatewayoverview.png)

### <a name="step-1-check-whether-hello-on-premises-vpn-device-is-validated"></a><span data-ttu-id="38f3b-112">Paso 1 Compruebe si se valida el dispositivo VPN en local de Hola</span><span class="sxs-lookup"><span data-stu-id="38f3b-112">Step 1 Check whether hello on-premises VPN device is validated</span></span>

1. <span data-ttu-id="38f3b-113">Compruebe si está usando una [versión del sistema operativo y dispositivo VPN validada](vpn-gateway-about-vpn-devices.md#devicetable).</span><span class="sxs-lookup"><span data-stu-id="38f3b-113">Check whether you are using a [validated VPN device and operating system version](vpn-gateway-about-vpn-devices.md#devicetable).</span></span> <span data-ttu-id="38f3b-114">Si no se valida el dispositivo VPN de hello, puede tener toocontact Hola dispositivo fabricante toosee si hay algún problema de compatibilidad.</span><span class="sxs-lookup"><span data-stu-id="38f3b-114">If hello VPN device is not validated, you may have toocontact hello device manufacturer toosee if there is any compatibility issue.</span></span>
2. <span data-ttu-id="38f3b-115">Asegúrese de que el dispositivo VPN Hola está configurado correctamente.</span><span class="sxs-lookup"><span data-stu-id="38f3b-115">Make sure that hello VPN device is correctly configured.</span></span> <span data-ttu-id="38f3b-116">Para obtener más información, vea [Edición de ejemplos de configuración de dispositivos](vpn-gateway-about-vpn-devices.md#editing).</span><span class="sxs-lookup"><span data-stu-id="38f3b-116">For more information, see [Editing device configuration samples](vpn-gateway-about-vpn-devices.md#editing).</span></span>

### <a name="step-2-check-hello-security-association-settingsfor-policy-based-azure-virtual-network-gateways"></a><span data-ttu-id="38f3b-117">Paso 2 parámetros de asociación de seguridad Hola de comprobación (para las puertas de enlace de red virtual Azure basada en directivas)</span><span class="sxs-lookup"><span data-stu-id="38f3b-117">Step 2 Check hello Security Association settings(for policy-based Azure virtual network gateways)</span></span>

1. <span data-ttu-id="38f3b-118">Asegúrese de que Hola red virtual, subredes y los intervalos de hello **puerta de enlace de red Local** definición en Microsoft Azure son los mismos que configuración de hello en dispositivo VPN de hello local.</span><span class="sxs-lookup"><span data-stu-id="38f3b-118">Make sure that hello virtual network, subnets and, ranges in hello **Local network gateway** definition in Microsoft Azure are same as hello configuration on hello on-premises VPN device.</span></span>
2. <span data-ttu-id="38f3b-119">Compruebe a que coinciden con la configuración de asociación de seguridad de Hola.</span><span class="sxs-lookup"><span data-stu-id="38f3b-119">Verify that hello Security Association settings match.</span></span>

### <a name="step-3-check-for-user-defined-routes-or-network-security-groups-on-gateway-subnet"></a><span data-ttu-id="38f3b-120">Paso 3: Comprobación de los grupos de seguridad de red o las rutas definidas por el usuario en la subred de puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="38f3b-120">Step 3 Check for User-Defined Routes or Network Security Groups on Gateway Subnet</span></span>

<span data-ttu-id="38f3b-121">Una ruta de subred de puerta de enlace de hello definido por el usuario se puede restringir el tráfico y lo que permite el tráfico restante.</span><span class="sxs-lookup"><span data-stu-id="38f3b-121">A user-defined route on hello gateway subnet may be restricting some traffic and allowing other traffic.</span></span> <span data-ttu-id="38f3b-122">Esto hace parecer que la conexión de VPN de hello es confiable para parte del tráfico y conveniente que otros usuarios.</span><span class="sxs-lookup"><span data-stu-id="38f3b-122">This makes it appear that hello VPN connection is unreliable for some traffic and good for others.</span></span> 

### <a name="step-4-check-hello-one-vpn-tunnel-per-subnet-pair-setting-for-policy-based-virtual-network-gateways"></a><span data-ttu-id="38f3b-123">Paso 4 verificación Hola "un túnel de VPN por cada par de subred" (para las puertas de enlace de red virtual basada en directivas)</span><span class="sxs-lookup"><span data-stu-id="38f3b-123">Step 4 Check hello "one VPN Tunnel per Subnet Pair" setting (for policy-based virtual network gateways)</span></span>

<span data-ttu-id="38f3b-124">Asegúrese de que el dispositivo VPN se establece toohave en local de ese hello **un túnel VPN por cada par de subred** para puertas de enlace de red virtual basada en directivas.</span><span class="sxs-lookup"><span data-stu-id="38f3b-124">Make sure that hello on-premises VPN device is set toohave **one VPN tunnel per subnet pair** for policy-based virtual network gateways.</span></span>

### <a name="step-5-check-for-security-association-limitation-for-policy-based-virtual-network-gateways"></a><span data-ttu-id="38f3b-125">Paso 5: Comprobación de la limitación de la asociación de seguridad (para puertas de enlace de red virtual basadas en directivas)</span><span class="sxs-lookup"><span data-stu-id="38f3b-125">Step 5 Check for Security Association Limitation (for policy-based virtual network gateways)</span></span>

<span data-ttu-id="38f3b-126">puerta de enlace de red virtual basada en directivas de Hello tiene un límite de 200 pares de asociación de seguridad de subred.</span><span class="sxs-lookup"><span data-stu-id="38f3b-126">hello Policy-based virtual network gateway has limit of 200 subnet Security Association pairs.</span></span> <span data-ttu-id="38f3b-127">Si multiplica por número de Hola de subredes de red virtual de Azure Hola número de subredes locales es mayor que 200, verá esporádicos subredes desconectar.</span><span class="sxs-lookup"><span data-stu-id="38f3b-127">If hello number of Azure virtual network subnets multiplied times by hello number of local subnets is greater than 200, you see sporadic subnets disconnecting.</span></span>

### <a name="step-6-check-on-premises-vpn-device-external-interface-address"></a><span data-ttu-id="38f3b-128">Paso 6: Comprobación de la dirección de la interfaz externa del dispositivo VPN local</span><span class="sxs-lookup"><span data-stu-id="38f3b-128">Step 6 Check on-premises VPN device external interface address</span></span>

- <span data-ttu-id="38f3b-129">Si hello orientado a la dirección IP del dispositivo VPN de hello Internet se incluye en hello **puerta de enlace de red Local** definición en Azure, puede experimentar desconexiones esporádicos.</span><span class="sxs-lookup"><span data-stu-id="38f3b-129">If hello Internet facing IP address of hello VPN device is included in hello **Local network gateway** definition in Azure, you may experience sporadic disconnections.</span></span>
- <span data-ttu-id="38f3b-130">Hello debe ser interfaz externa del dispositivo directamente en hello Internet.</span><span class="sxs-lookup"><span data-stu-id="38f3b-130">hello device's external interface must be directly on hello Internet.</span></span> <span data-ttu-id="38f3b-131">No debería haber ninguna traducción de direcciones de red (NAT) o un firewall entre Hola Internet y el dispositivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="38f3b-131">There should be no Network Address Translation (NAT) or firewall between hello Internet and hello device.</span></span>
-  <span data-ttu-id="38f3b-132">Si configura una dirección IP virtual toohave de agrupación en clústeres de servidor de seguridad, debe interrumpir clúster hello y exponer el dispositivo VPN de hello directamente tooa interfaz pública que Hola puerta de enlace puede comunicarse con.</span><span class="sxs-lookup"><span data-stu-id="38f3b-132">If you configure Firewall Clustering toohave a virtual IP, you must break hello cluster and expose hello VPN appliance directly tooa public interface that hello gateway can interface with.</span></span>

### <a name="step-7-check-whether-hello-on-premises-vpn-device-has-perfect-forward-secrecy-enabled"></a><span data-ttu-id="38f3b-133">Paso 7 Compruebe si el dispositivo VPN tiene confidencialidad directa perfecta habilitado a local de Hola</span><span class="sxs-lookup"><span data-stu-id="38f3b-133">Step 7 Check whether hello on-premises VPN device has Perfect Forward Secrecy enabled</span></span>

<span data-ttu-id="38f3b-134">Hola **confidencialidad directa perfecta** característica puede causar problemas de desconexión de Hola.</span><span class="sxs-lookup"><span data-stu-id="38f3b-134">hello **Perfect Forward Secrecy** feature can cause hello disconnection problems.</span></span> <span data-ttu-id="38f3b-135">Si el dispositivo VPN hello tiene **confidencialidad directa perfecta** habilitado, deshabilite la característica de Hola.</span><span class="sxs-lookup"><span data-stu-id="38f3b-135">If hello VPN device has **Perfect forward Secrecy** enabled, disable hello feature.</span></span> <span data-ttu-id="38f3b-136">A continuación, [actualizar directiva de IPsec de puerta de enlace de red virtual de hello](vpn-gateway-ipsecikepolicy-rm-powershell.md#managepolicy).</span><span class="sxs-lookup"><span data-stu-id="38f3b-136">Then [update hello virtual network gateway IPsec policy](vpn-gateway-ipsecikepolicy-rm-powershell.md#managepolicy).</span></span>

## <a name="next-steps"></a><span data-ttu-id="38f3b-137">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="38f3b-137">Next steps</span></span>

- [<span data-ttu-id="38f3b-138">Configurar una red virtual de sitio a sitio conexión tooa</span><span class="sxs-lookup"><span data-stu-id="38f3b-138">Configure a Site-to-Site connection tooa virtual network</span></span>](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
- [<span data-ttu-id="38f3b-139">Configuración de la directiva IPsec/IKE para conexiones VPN de sitio a sitio</span><span class="sxs-lookup"><span data-stu-id="38f3b-139">Configure IPsec/IKE policy for Site-to-Site VPN connections</span></span>](vpn-gateway-ipsecikepolicy-rm-powershell.md)

