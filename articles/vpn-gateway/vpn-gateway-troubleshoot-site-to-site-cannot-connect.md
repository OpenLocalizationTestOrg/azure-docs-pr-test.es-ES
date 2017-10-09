---
title: "aaaTroubleshoot una conexión de VPN de sitio a sitio Azure que no se puede conectar | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tootroubleshoot una conexión de VPN de sitio a sitio que de repente deja de funcionar y no se puede volver a conectar."
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
ms.openlocfilehash: 632c75bfcfb93a532eeead2855d43e6614569a99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-an-azure-site-to-site-vpn-connection-cannot-connect-and-stops-working"></a><span data-ttu-id="a9e06-103">Solución de problemas: la conexión VPN de sitio a sitio de Azure no puede conectarse y deja de funcionar</span><span class="sxs-lookup"><span data-stu-id="a9e06-103">Troubleshooting: An Azure site-to-site VPN connection cannot connect and stops working</span></span>

<span data-ttu-id="a9e06-104">Después de configurar una conexión de VPN de sitio a sitio entre una red local y una red virtual de Azure, Hola conexión VPN de repente deja de funcionar y no se puede volver a conectar.</span><span class="sxs-lookup"><span data-stu-id="a9e06-104">After you configure a site-to-site VPN connection between an on-premises network and an Azure virtual network, hello VPN connection suddenly stops working and cannot be reconnected.</span></span> <span data-ttu-id="a9e06-105">Este artículo proporciona toohelp de pasos de solución de problemas para resolver este problema.</span><span class="sxs-lookup"><span data-stu-id="a9e06-105">This article provides troubleshooting steps toohelp you resolve this problem.</span></span> 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="troubleshooting-steps"></a><span data-ttu-id="a9e06-106">Pasos para solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="a9e06-106">Troubleshooting steps</span></span>

<span data-ttu-id="a9e06-107">problema de hello tooresolve, en primer lugar intente demasiado[puerta de enlace de VPN de Azure de Hola de restablecimiento](vpn-gateway-resetgw-classic.md) y restablecer el túnel de hello de dispositivo VPN de hello local.</span><span class="sxs-lookup"><span data-stu-id="a9e06-107">tooresolve hello problem, first try too[reset hello Azure VPN gateway](vpn-gateway-resetgw-classic.md) and reset hello tunnel from hello on-premises VPN device.</span></span> <span data-ttu-id="a9e06-108">Si persiste el problema de hello, siga estos hacen que hello tooidentify pasos de problema de Hola.</span><span class="sxs-lookup"><span data-stu-id="a9e06-108">If hello problem persists, follow these steps tooidentify hello cause of hello problem.</span></span>

### <a name="prerequisite-step"></a><span data-ttu-id="a9e06-109">Paso de requisito previo</span><span class="sxs-lookup"><span data-stu-id="a9e06-109">Prerequisite step</span></span>

<span data-ttu-id="a9e06-110">Comprobar el tipo de saludo de puerta de enlace de VPN de Azure de Hola.</span><span class="sxs-lookup"><span data-stu-id="a9e06-110">Check hello type of hello Azure VPN gateway.</span></span>

1. <span data-ttu-id="a9e06-111">Vaya toohello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a9e06-111">Go toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="a9e06-112">Comprobar hello **Introducción** página de puerta de enlace VPN de Hola para obtener información de tipo hello.</span><span class="sxs-lookup"><span data-stu-id="a9e06-112">Check hello **Overview** page of hello VPN gateway for hello type information.</span></span>
    
    ![Información general de puerta de enlace de Hola](media\vpn-gateway-troubleshoot-site-to-site-cannot-connect\gatewayoverview.png)

### <a name="step-1-check-whether-hello-on-premises-vpn-device-is-validated"></a><span data-ttu-id="a9e06-114">Paso 1.</span><span class="sxs-lookup"><span data-stu-id="a9e06-114">Step 1.</span></span> <span data-ttu-id="a9e06-115">Compruebe si se valida el dispositivo VPN de hello local</span><span class="sxs-lookup"><span data-stu-id="a9e06-115">Check whether hello on-premises VPN device is validated</span></span>

1. <span data-ttu-id="a9e06-116">Compruebe si está usando una [versión del sistema operativo y dispositivo VPN validada](vpn-gateway-about-vpn-devices.md#devicetable).</span><span class="sxs-lookup"><span data-stu-id="a9e06-116">Check whether you are using a [validated VPN device and operating system version](vpn-gateway-about-vpn-devices.md#devicetable).</span></span> <span data-ttu-id="a9e06-117">Si Hola dispositivo no es un dispositivo VPN validado, podría tener toocontact Hola dispositivo fabricante toosee si hay un problema de compatibilidad.</span><span class="sxs-lookup"><span data-stu-id="a9e06-117">If hello device is not a validated VPN device, you might have toocontact hello device manufacturer toosee if there is a compatibility issue.</span></span>

2. <span data-ttu-id="a9e06-118">Asegúrese de que el dispositivo VPN Hola está configurado correctamente.</span><span class="sxs-lookup"><span data-stu-id="a9e06-118">Make sure that hello VPN device is correctly configured.</span></span> <span data-ttu-id="a9e06-119">Para más información, consulte [Ejemplos de edición de configuración de dispositivos](/vpn-gateway-about-vpn-devices.md#editing).</span><span class="sxs-lookup"><span data-stu-id="a9e06-119">For more information, see [Edit device configuration samples](/vpn-gateway-about-vpn-devices.md#editing).</span></span>

### <a name="step-2-verify-hello-shared-key"></a><span data-ttu-id="a9e06-120">Paso 2:</span><span class="sxs-lookup"><span data-stu-id="a9e06-120">Step 2.</span></span> <span data-ttu-id="a9e06-121">Compruebe la clave compartida de Hola</span><span class="sxs-lookup"><span data-stu-id="a9e06-121">Verify hello shared key</span></span>

<span data-ttu-id="a9e06-122">Compare la clave compartida de Hola Hola local VPN dispositivo toohello VPN de red Virtual de Azure toomake seguro de que coinciden con las claves de Hola.</span><span class="sxs-lookup"><span data-stu-id="a9e06-122">Compare hello shared key for hello on-premises VPN device toohello Azure Virtual Network VPN toomake sure that hello keys match.</span></span> 

<span data-ttu-id="a9e06-123">tooview Hola una clave compartida para hello conexión VPN de Azure, use uno de los siguientes métodos de hello:</span><span class="sxs-lookup"><span data-stu-id="a9e06-123">tooview hello shared key for hello Azure VPN connection, use one of hello following methods:</span></span>

<span data-ttu-id="a9e06-124">**Portal de Azure**</span><span class="sxs-lookup"><span data-stu-id="a9e06-124">**Azure portal**</span></span>

1. <span data-ttu-id="a9e06-125">Vaya toohello conexión de sitio a sitio de puerta de enlace VPN que ha creado.</span><span class="sxs-lookup"><span data-stu-id="a9e06-125">Go toohello VPN gateway site-to-site connection that you created.</span></span>

2. <span data-ttu-id="a9e06-126">Hola **configuración** sección, haga clic en **clave compartida**.</span><span class="sxs-lookup"><span data-stu-id="a9e06-126">In hello **Settings** section, click **Shared key**.</span></span>
    
    ![Clave compartida](media/vpn-gateway-troubleshoot-site-to-site-cannot-connect/sharedkey.png)

<span data-ttu-id="a9e06-128">**Azure PowerShell**</span><span class="sxs-lookup"><span data-stu-id="a9e06-128">**Azure PowerShell**</span></span>

<span data-ttu-id="a9e06-129">Para el modelo de implementación de hello Azure Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="a9e06-129">For hello Azure Resource Manager deployment model:</span></span>

    Get-AzureRmVirtualNetworkGatewayConnectionSharedKey -Name <Connection name> -ResourceGroupName <Resource group name>

<span data-ttu-id="a9e06-130">Para el modelo de implementación clásica de hello:</span><span class="sxs-lookup"><span data-stu-id="a9e06-130">For hello classic deployment model:</span></span>

    Get-AzureVNetGatewayKey -VNetName -LocalNetworkSiteName

### <a name="step-3-verify-hello-vpn-peer-ips"></a><span data-ttu-id="a9e06-131">Paso 3:</span><span class="sxs-lookup"><span data-stu-id="a9e06-131">Step 3.</span></span> <span data-ttu-id="a9e06-132">Comprobar del mismo nivel de hello VPN direcciones IP</span><span class="sxs-lookup"><span data-stu-id="a9e06-132">Verify hello VPN peer IPs</span></span>

-   <span data-ttu-id="a9e06-133">Hola definición de IP en hello **puerta de enlace de red Local** objeto en Azure debe coincidir con la IP del dispositivo local Hola.</span><span class="sxs-lookup"><span data-stu-id="a9e06-133">hello IP definition in hello **Local Network Gateway** object in Azure should match hello on-premises device IP.</span></span>
-   <span data-ttu-id="a9e06-134">definición de IP de puerta de enlace de Azure que está establecido en Hola Hola local dispositivo debe coincidir con la IP de puerta de enlace de Azure de Hola.</span><span class="sxs-lookup"><span data-stu-id="a9e06-134">hello Azure gateway IP definition that is set on hello on-premises device should match hello Azure gateway IP.</span></span>

### <a name="step-4-check-udr-and-nsgs-on-hello-gateway-subnet"></a><span data-ttu-id="a9e06-135">Paso 4</span><span class="sxs-lookup"><span data-stu-id="a9e06-135">Step 4.</span></span> <span data-ttu-id="a9e06-136">Compruebe UDR y NSG de subred de puerta de enlace de Hola</span><span class="sxs-lookup"><span data-stu-id="a9e06-136">Check UDR and NSGs on hello gateway subnet</span></span>

<span data-ttu-id="a9e06-137">Busque y quite enrutamiento definido por el usuario (UDR) o grupos de seguridad de red (NSG) en la subred de puerta de enlace de hello y, a continuación, el resultado de hello de pruebas.</span><span class="sxs-lookup"><span data-stu-id="a9e06-137">Check for and remove user-defined routing (UDR) or Network Security Groups (NSGs) on hello gateway subnet, and then test hello result.</span></span> <span data-ttu-id="a9e06-138">Si se resuelve el problema de hello, validar la configuración de Hola que aplica UDR o NSG.</span><span class="sxs-lookup"><span data-stu-id="a9e06-138">If hello problem is resolved, validate hello settings that UDR or NSG applied.</span></span>

### <a name="step-5-check-hello-on-premises-vpn-device-external-interface-address"></a><span data-ttu-id="a9e06-139">Paso 5.</span><span class="sxs-lookup"><span data-stu-id="a9e06-139">Step 5.</span></span> <span data-ttu-id="a9e06-140">Hola de comprobación de dirección de interfaz externa del dispositivo VPN local</span><span class="sxs-lookup"><span data-stu-id="a9e06-140">Check hello on-premises VPN device external interface address</span></span>

- <span data-ttu-id="a9e06-141">Si se incluye Hola dirección IP de conexión a Internet del dispositivo VPN de hello en hello **red Local** definición en Azure, podría experimentar desconexiones esporádicos.</span><span class="sxs-lookup"><span data-stu-id="a9e06-141">If hello Internet-facing IP address of hello VPN device is included in hello **Local network** definition in Azure, you might experience sporadic disconnections.</span></span>
- <span data-ttu-id="a9e06-142">Hello debe ser interfaz externa del dispositivo directamente en hello Internet.</span><span class="sxs-lookup"><span data-stu-id="a9e06-142">hello device's external interface must be directly on hello Internet.</span></span> <span data-ttu-id="a9e06-143">No debería haber ningún firewall entre Hola Internet y el dispositivo de Hola o traducción de direcciones de red.</span><span class="sxs-lookup"><span data-stu-id="a9e06-143">There should be no network address translation or firewall between hello Internet and hello device.</span></span>
- <span data-ttu-id="a9e06-144">tooconfigure firewall toohave agrupación en clústeres una dirección IP virtual, debe interrumpir clúster hello y exponer el dispositivo VPN de hello directamente la interfaz pública de tooa esa puerta de enlace de hello puede comunicarse con.</span><span class="sxs-lookup"><span data-stu-id="a9e06-144">tooconfigure firewall clustering toohave a virtual IP, you must break hello cluster and expose hello VPN appliance directly tooa public interface that hello gateway can interface with.</span></span>

### <a name="step-6-verify-that-hello-subnets-match-exactly-azure-policy-based-gateways"></a><span data-ttu-id="a9e06-145">Paso 6.</span><span class="sxs-lookup"><span data-stu-id="a9e06-145">Step 6.</span></span> <span data-ttu-id="a9e06-146">Compruebe que las subredes de hello coinciden exactamente (Azure basada en directivas con puertas de enlace)</span><span class="sxs-lookup"><span data-stu-id="a9e06-146">Verify that hello subnets match exactly (Azure policy-based gateways)</span></span>

-   <span data-ttu-id="a9e06-147">Compruebe que las subredes de hello coinciden exactamente entre Hola red virtual de Azure y las definiciones de local de hello red virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="a9e06-147">Verify that hello subnets match exactly between hello Azure virtual network and on-premises definitions for hello Azure virtual network.</span></span>
-   <span data-ttu-id="a9e06-148">Compruebe que las subredes de hello coinciden exactamente entre hello **puerta de enlace de red Local** y definiciones de red local de hello en local.</span><span class="sxs-lookup"><span data-stu-id="a9e06-148">Verify that hello subnets match exactly between hello **Local Network Gateway** and on-premises definitions for hello on-premises network.</span></span>

### <a name="step-7-verify-hello-azure-gateway-health-probe"></a><span data-ttu-id="a9e06-149">Paso 7.</span><span class="sxs-lookup"><span data-stu-id="a9e06-149">Step 7.</span></span> <span data-ttu-id="a9e06-150">Compruebe el sondeo de estado de Azure de la puerta de enlace de Hola</span><span class="sxs-lookup"><span data-stu-id="a9e06-150">Verify hello Azure gateway health probe</span></span>

1. <span data-ttu-id="a9e06-151">Vaya toohello [sondeo de estado](https://&lt;YourVirtualNetworkGatewayIP&gt;:8081/healthprobe).</span><span class="sxs-lookup"><span data-stu-id="a9e06-151">Go toohello [health probe](https://&lt;YourVirtualNetworkGatewayIP&gt;:8081/healthprobe).</span></span>

2. <span data-ttu-id="a9e06-152">Haga clic en a través de advertencia de certificado de Hola.</span><span class="sxs-lookup"><span data-stu-id="a9e06-152">Click through hello certificate warning.</span></span>
3. <span data-ttu-id="a9e06-153">Si recibe una respuesta, la puerta de enlace VPN de Hola se considera correcta.</span><span class="sxs-lookup"><span data-stu-id="a9e06-153">If you receive a response, hello VPN gateway is considered healthy.</span></span> <span data-ttu-id="a9e06-154">Si no recibe una respuesta, puerta de enlace de hello no sea correcto o un NSG de subred de puerta de enlace de hello está causando el problema de Hola.</span><span class="sxs-lookup"><span data-stu-id="a9e06-154">If you don't receive a response, hello gateway might not be healthy or an NSG on hello gateway subnet is causing hello problem.</span></span> <span data-ttu-id="a9e06-155">Hola después de texto es una respuesta de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="a9e06-155">hello following text is a sample response:</span></span>

    <span data-ttu-id="a9e06-156">&lt;?xml version="1.0"?&gt; <string xmlns="http://schemas.microsoft.com/2003/10/Serialization/">Primary Instance: GatewayTenantWorker_IN_1 GatewayTenantVersion: 14.7.24.6&lt;/string&gt;</span><span class="sxs-lookup"><span data-stu-id="a9e06-156">&lt;?xml version="1.0"?>  <string xmlns="http://schemas.microsoft.com/2003/10/Serialization/">Primary Instance: GatewayTenantWorker_IN_1 GatewayTenantVersion: 14.7.24.6</string&gt;</span></span>

### <a name="step-8-check-whether-hello-on-premises-vpn-device-has-hello-perfect-forward-secrecy-feature-enabled"></a><span data-ttu-id="a9e06-157">Paso 8.</span><span class="sxs-lookup"><span data-stu-id="a9e06-157">Step 8.</span></span> <span data-ttu-id="a9e06-158">Compruebe si Hola local dispositivo VPN tenga habilitada la característica de confidencialidad directa total de Hola</span><span class="sxs-lookup"><span data-stu-id="a9e06-158">Check whether hello on-premises VPN device has hello perfect forward secrecy feature enabled</span></span>

<span data-ttu-id="a9e06-159">características de confidencialidad directa total Hola pueden causar problemas de desconexión.</span><span class="sxs-lookup"><span data-stu-id="a9e06-159">hello perfect forward secrecy feature can cause disconnection problems.</span></span> <span data-ttu-id="a9e06-160">Si el dispositivo VPN de hello tiene confidencialidad directa total habilitada, deshabilite la característica de Hola.</span><span class="sxs-lookup"><span data-stu-id="a9e06-160">If hello VPN device has perfect forward secrecy enabled, disable hello feature.</span></span> <span data-ttu-id="a9e06-161">A continuación, actualice la directiva de IPsec de puerta de enlace VPN de Hola.</span><span class="sxs-lookup"><span data-stu-id="a9e06-161">Then update hello VPN gateway IPsec policy.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a9e06-162">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a9e06-162">Next steps</span></span>

-   [<span data-ttu-id="a9e06-163">Configurar una red virtual de tooa de conexión de sitio a sitio</span><span class="sxs-lookup"><span data-stu-id="a9e06-163">Configure a site-to-site connection tooa virtual network</span></span>](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
-   [<span data-ttu-id="a9e06-164">Configuración de una directiva IPsec/IKE para conexiones VPN de sitio a sitio</span><span class="sxs-lookup"><span data-stu-id="a9e06-164">Configure an IPsec/IKE policy for site-to-site VPN connections</span></span>](vpn-gateway-ipsecikepolicy-rm-powershell.md)
