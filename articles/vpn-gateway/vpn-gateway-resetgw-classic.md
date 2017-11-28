---
title: "Restablecer un tooreestablish de puerta de enlace de VPN de Azure túneles IPsec | Documentos de Microsoft"
description: "Este artículo le guiará a través de restablecimiento de los puerta de enlace de VPN de Azure los túneles IPsec tooreestablish. las puertas de enlace tooVPN en hello clásico y modelos de implementación del Administrador de recursos de Hola aplica el artículo de Hola."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 79d77cb8-d175-4273-93ac-712d7d45b1fe
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/24/2017
ms.author: cherylmc
ms.openlocfilehash: 84dd741f0bebd6b18cb235216a68a88da5fe17b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="reset-a-vpn-gateway"></a><span data-ttu-id="bb3f2-104">Restablecimiento de una puerta de enlace de VPN</span><span class="sxs-lookup"><span data-stu-id="bb3f2-104">Reset a VPN Gateway</span></span>

<span data-ttu-id="bb3f2-105">Restablecer una puerta de enlace de VPN de Azure es útil si se pierde la conectividad VPN entre locales en uno o varios túneles VPN de sitio a sitio.</span><span class="sxs-lookup"><span data-stu-id="bb3f2-105">Resetting an Azure VPN gateway is helpful if you lose cross-premises VPN connectivity on one or more Site-to-Site VPN tunnels.</span></span> <span data-ttu-id="bb3f2-106">En esta situación, los dispositivos VPN local son todo funciona correctamente, pero son tooestablish imposibilidad de túneles de IPsec con puertas de enlace de VPN de Azure de Hola.</span><span class="sxs-lookup"><span data-stu-id="bb3f2-106">In this situation, your on-premises VPN devices are all working correctly, but are not able tooestablish IPsec tunnels with hello Azure VPN gateways.</span></span> <span data-ttu-id="bb3f2-107">Este artículo lo ayuda a restablecer la puerta de enlace de VPN.</span><span class="sxs-lookup"><span data-stu-id="bb3f2-107">This article helps you reset your VPN gateway.</span></span>

### <a name="what-happens-during-a-reset"></a><span data-ttu-id="bb3f2-108">¿Qué ocurre durante el restablecimiento?</span><span class="sxs-lookup"><span data-stu-id="bb3f2-108">What happens during a reset?</span></span>

<span data-ttu-id="bb3f2-109">Una puerta de enlace de VPN se compone de dos instancias de VM que se ejecutan en una configuración de modo de espera activo.</span><span class="sxs-lookup"><span data-stu-id="bb3f2-109">A VPN gateway is composed of two VM instances running in an active-standby configuration.</span></span> <span data-ttu-id="bb3f2-110">Si se restablece la puerta de enlace de hello, se reinicia la puerta de enlace de hello, y, a continuación, vuelve a aplicar Hola entre entornos tooit configuraciones.</span><span class="sxs-lookup"><span data-stu-id="bb3f2-110">When you reset hello gateway, it reboots hello gateway, and then reapplies hello cross-premises configurations tooit.</span></span> <span data-ttu-id="bb3f2-111">puerta de enlace de Hello mantiene Hola la dirección IP pública ya tiene.</span><span class="sxs-lookup"><span data-stu-id="bb3f2-111">hello gateway keeps hello public IP address it already has.</span></span> <span data-ttu-id="bb3f2-112">Esto significa que no necesita configuración del enrutador VPN tooupdate Hola con una nueva dirección IP pública para la puerta de enlace VPN de Azure.</span><span class="sxs-lookup"><span data-stu-id="bb3f2-112">This means you won’t need tooupdate hello VPN router configuration with a new public IP address for Azure VPN gateway.</span></span>

<span data-ttu-id="bb3f2-113">Cuando se emite la puerta de enlace de hello comando tooreset hello, instancias activas actuales de Hola de puerta de enlace de VPN de Azure Hola se reinicia inmediatamente.</span><span class="sxs-lookup"><span data-stu-id="bb3f2-113">When you issue hello command tooreset hello gateway, hello current active instance of hello Azure VPN gateway is rebooted immediately.</span></span> <span data-ttu-id="bb3f2-114">Habrá un breve intervalo durante la conmutación por error de Hola de hello instancias activas (está reiniciando), instancia de toohello en espera.</span><span class="sxs-lookup"><span data-stu-id="bb3f2-114">There will be a brief gap during hello failover from hello active instance (being rebooted), toohello standby instance.</span></span> <span data-ttu-id="bb3f2-115">espacio de Hello debe ser inferior a un minuto.</span><span class="sxs-lookup"><span data-stu-id="bb3f2-115">hello gap should be less than one minute.</span></span>

<span data-ttu-id="bb3f2-116">Si no se restaura la conexión de hello después del primer reinicio de hello, problema Hola mismo nuevo comando tooreboot Hola segunda VM instancia (Hola nueva active puerta de enlace).</span><span class="sxs-lookup"><span data-stu-id="bb3f2-116">If hello connection is not restored after hello first reboot, issue hello same command again tooreboot hello second VM instance (hello new active gateway).</span></span> <span data-ttu-id="bb3f2-117">Si dos reinicios de hello están solicitada tooback atrás, habrá un período más largo ligeramente donde se están reiniciando ambas instancias VM (activos y en espera).</span><span class="sxs-lookup"><span data-stu-id="bb3f2-117">If hello two reboots are requested back tooback, there will be a slightly longer period where both VM instances (active and standby) are being rebooted.</span></span> <span data-ttu-id="bb3f2-118">Esto hará que un intervalo más largo en la conectividad VPN de hello, seguridad too2 too4 minutos para los reinicios de las máquinas virtuales toocomplete Hola.</span><span class="sxs-lookup"><span data-stu-id="bb3f2-118">This will cause a longer gap on hello VPN connectivity, up too2 too4 minutes for VMs toocomplete hello reboots.</span></span>

<span data-ttu-id="bb3f2-119">Después de dos reinicios, si sigue experimentando problemas de conectividad entre entornos, abra una solicitud de soporte técnico de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="bb3f2-119">After two reboots, if you are still experiencing cross-premises connectivity problems, please open a support request from hello Azure portal.</span></span>

## <span data-ttu-id="bb3f2-120"><a name="before"></a>Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="bb3f2-120"><a name="before"></a>Before you begin</span></span>

<span data-ttu-id="bb3f2-121">Antes de restablecer la puerta de enlace, compruebe los elementos clave de hello enumeran a continuación para cada túnel VPN de IPsec sitio a sitio (S2S).</span><span class="sxs-lookup"><span data-stu-id="bb3f2-121">Before you reset your gateway, verify hello key items listed below for each IPsec Site-to-Site (S2S) VPN tunnel.</span></span> <span data-ttu-id="bb3f2-122">Si hay alguna incoherencia en los elementos de hello producirá disconnect Hola de túneles VPN S2S.</span><span class="sxs-lookup"><span data-stu-id="bb3f2-122">Any mismatch in hello items will result in hello disconnect of S2S VPN tunnels.</span></span> <span data-ttu-id="bb3f2-123">Comprobar y corregir las configuraciones de Hola para su entorno local y puertas de enlace VPN de Azure evita reinicios innecesarios y las interrupciones de Hola otras conexiones de trabajo en puertas de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="bb3f2-123">Verifying and correcting hello configurations for your on-premises and Azure VPN gateways saves you from unnecessary reboots and disruptions for hello other working connections on hello gateways.</span></span>

<span data-ttu-id="bb3f2-124">Compruebe los siguientes elementos antes de restablecer la puerta de enlace de hello:</span><span class="sxs-lookup"><span data-stu-id="bb3f2-124">Verify hello following items before resetting your gateway:</span></span>

* <span data-ttu-id="bb3f2-125">Hola Internet IP direcciones (VIP) para ambos puerta de enlace de VPN de Azure de Hola y puerta de enlace VPN están configurados correctamente en ambas directivas VPN Hola hello y Azure local a local de Hola.</span><span class="sxs-lookup"><span data-stu-id="bb3f2-125">hello Internet IP addresses (VIPs) for both hello Azure VPN gateway and hello on-premises VPN gateway are configured correctly in both hello Azure and hello on-premises VPN policies.</span></span>
* <span data-ttu-id="bb3f2-126">clave compartida previamente de Hello debe ser Hola lo mismo en puertas de enlace VPN de Azure y local.</span><span class="sxs-lookup"><span data-stu-id="bb3f2-126">hello pre-shared key must be hello same on both Azure and on-premises VPN gateways.</span></span>
* <span data-ttu-id="bb3f2-127">Si aplica la configuración de IPsec/IKE específica, como cifrado, algoritmos hash y PFS (confidencialidad directa perfecta), asegúrese de ambos hello Azure y puertas de enlace VPN local tienen Hola misma configuración.</span><span class="sxs-lookup"><span data-stu-id="bb3f2-127">If you apply specific IPsec/IKE configuration, such as encryption, hashing algorithms, and PFS (Perfect Forward Secrecy), ensure both hello Azure and on-premises VPN gateways have hello same configurations.</span></span>

## <span data-ttu-id="bb3f2-128"><a name="portal"></a>Azure Portal</span><span class="sxs-lookup"><span data-stu-id="bb3f2-128"><a name="portal"></a>Azure portal</span></span>

<span data-ttu-id="bb3f2-129">Puede restablecer una puerta de enlace de VPN de administrador de recursos mediante Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="bb3f2-129">You can reset a Resource Manager VPN gateway using hello Azure portal.</span></span> <span data-ttu-id="bb3f2-130">Si desea tooreset una puerta de enlace clásico, vea hello [PowerShell](#resetclassic) pasos.</span><span class="sxs-lookup"><span data-stu-id="bb3f2-130">If you want tooreset a classic gateway, see hello [PowerShell](#resetclassic) steps.</span></span>

### <a name="resource-manager-deployment-model"></a><span data-ttu-id="bb3f2-131">Modelo de implementación del Administrador de recursos</span><span class="sxs-lookup"><span data-stu-id="bb3f2-131">Resource Manager deployment model</span></span>

1. <span data-ttu-id="bb3f2-132">Abra hello [portal de Azure](https://portal.azure.com) y navegar por el enlace de red virtual del Administrador de recursos toohello que desea tooreset.</span><span class="sxs-lookup"><span data-stu-id="bb3f2-132">Open hello [Azure portal](https://portal.azure.com) and navigate toohello Resource Manager virtual network gateway that you want tooreset.</span></span>
2. <span data-ttu-id="bb3f2-133">En la hoja de Hola para puerta de enlace de red virtual de hello, haga clic en 'Restablecer'.</span><span class="sxs-lookup"><span data-stu-id="bb3f2-133">On hello blade for hello virtual network gateway, click 'Reset'.</span></span>

  ![Hoja de restablecimiento de puerta de enlace de VPN](./media/vpn-gateway-howto-reset-gateway/reset-vpn-gateway-portal.png)
3. <span data-ttu-id="bb3f2-135">En hello restablecer hoja, haga clic en hello **restablecer** botón.</span><span class="sxs-lookup"><span data-stu-id="bb3f2-135">On hello Reset blade, click hello **Reset** button.</span></span>

## <span data-ttu-id="bb3f2-136"><a name="ps"></a>PowerShell</span><span class="sxs-lookup"><span data-stu-id="bb3f2-136"><a name="ps"></a>PowerShell</span></span>

### <a name="resource-manager-deployment-model"></a><span data-ttu-id="bb3f2-137">Modelo de implementación del Administrador de recursos</span><span class="sxs-lookup"><span data-stu-id="bb3f2-137">Resource Manager deployment model</span></span>

<span data-ttu-id="bb3f2-138">Hola cmdlet para restablecer una puerta de enlace es **AzureRmVirtualNetworkGateway restablecimiento**.</span><span class="sxs-lookup"><span data-stu-id="bb3f2-138">hello cmdlet for resetting a gateway is **Reset-AzureRmVirtualNetworkGateway**.</span></span> <span data-ttu-id="bb3f2-139">Antes de realizar un restablecimiento, asegúrese de que tiene Hola versión más reciente de hello [cmdlets de PowerShell del Administrador de recursos](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0).</span><span class="sxs-lookup"><span data-stu-id="bb3f2-139">Before performing a reset, make sure you have hello latest version of hello [Resource Manager PowerShell cmdlets](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0).</span></span> <span data-ttu-id="bb3f2-140">Hello en el ejemplo siguiente se restablece una puerta de enlace de red virtual denominado VNet1GW en el grupo de recursos de Hola TestRG1:</span><span class="sxs-lookup"><span data-stu-id="bb3f2-140">hello following example resets a virtual network gateway named VNet1GW in hello TestRG1 resource group:</span></span>

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name VNet1GW -ResourceGroup TestRG1
Reset-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw
```

<span data-ttu-id="bb3f2-141">Resultado:</span><span class="sxs-lookup"><span data-stu-id="bb3f2-141">Result:</span></span>

<span data-ttu-id="bb3f2-142">Cuando reciba un resultado devuelto, puede asumir Hola puerta de enlace se restableció correctamente.</span><span class="sxs-lookup"><span data-stu-id="bb3f2-142">When you receive a return result, you can assume hello gateway reset was successful.</span></span> <span data-ttu-id="bb3f2-143">Sin embargo, hay nada en el resultado devuelto Hola que indica explícitamente que Hola se restableció correctamente.</span><span class="sxs-lookup"><span data-stu-id="bb3f2-143">However, there is nothing in hello return result that indicates explicitly that hello reset was successful.</span></span> <span data-ttu-id="bb3f2-144">Si desea que toolook estrechamente en hello historial toosee exactamente cuando restablecimiento de puerta de enlace de Hola se ha producido, puede ver esa información en hello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="bb3f2-144">If you want toolook closely at hello history toosee exactly when hello gateway reset occurred, you can view that information in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="bb3f2-145">En el portal de hello, navegue demasiado**"GatewayName" -> mantenimiento de recursos**.</span><span class="sxs-lookup"><span data-stu-id="bb3f2-145">In hello portal, navigate too**'GatewayName' -> Resource Health**.</span></span>

### <span data-ttu-id="bb3f2-146"><a name="resetclassic"></a>Modelo de implementación clásica</span><span class="sxs-lookup"><span data-stu-id="bb3f2-146"><a name="resetclassic"></a>Classic deployment model</span></span>

<span data-ttu-id="bb3f2-147">Hola cmdlet para restablecer una puerta de enlace es **Reset-AzureVNetGateway**.</span><span class="sxs-lookup"><span data-stu-id="bb3f2-147">hello cmdlet for resetting a gateway is **Reset-AzureVNetGateway**.</span></span> <span data-ttu-id="bb3f2-148">Antes de realizar un restablecimiento, asegúrese de que tiene Hola versión más reciente de hello [cmdlets de PowerShell Service Management (SM)](https://docs.microsoft.com/powershell/azure/install-azure-ps?view=azuresmps-3.7.0).</span><span class="sxs-lookup"><span data-stu-id="bb3f2-148">Before performing a reset, make sure you have hello latest version of hello [Service Management (SM) PowerShell cmdlets](https://docs.microsoft.com/powershell/azure/install-azure-ps?view=azuresmps-3.7.0).</span></span> <span data-ttu-id="bb3f2-149">Hello en el ejemplo siguiente se restablece puerta de enlace de Hola para una red virtual denominada "ContosoVNet":</span><span class="sxs-lookup"><span data-stu-id="bb3f2-149">hello following example resets hello gateway for a virtual network named "ContosoVNet":</span></span>

```powershell
Reset-AzureVNetGateway –VnetName “ContosoVNet”
```

<span data-ttu-id="bb3f2-150">Resultado:</span><span class="sxs-lookup"><span data-stu-id="bb3f2-150">Result:</span></span>

```powershell
Error          :
HttpStatusCode : OK
Id             : f1600632-c819-4b2f-ac0e-f4126bec1ff8
Status         : Successful
RequestId      : 9ca273de2c4d01e986480ce1ffa4d6d9
StatusCode     : OK
```

## <span data-ttu-id="bb3f2-151"><a name="cli"></a>Azure CLI</span><span class="sxs-lookup"><span data-stu-id="bb3f2-151"><a name="cli"></a>Azure CLI</span></span>

<span data-ttu-id="bb3f2-152">puerta de enlace de tooreset hello, use hello [restablece az red red virtual de puerta de enlace](https://docs.microsoft.com/cli/azure/network/vnet-gateway#reset) comando.</span><span class="sxs-lookup"><span data-stu-id="bb3f2-152">tooreset hello gateway, use hello [az network vnet-gateway reset](https://docs.microsoft.com/cli/azure/network/vnet-gateway#reset) command.</span></span> <span data-ttu-id="bb3f2-153">Hello en el ejemplo siguiente se restablece una puerta de enlace de red virtual denominado VNet5GW en el grupo de recursos de Hola TestRG5:</span><span class="sxs-lookup"><span data-stu-id="bb3f2-153">hello following example resets a virtual network gateway named VNet5GW in hello TestRG5 resource group:</span></span>

```azurecli
az network vnet-gateway reset -n VNet5GW -g TestRG5
```

<span data-ttu-id="bb3f2-154">Resultado:</span><span class="sxs-lookup"><span data-stu-id="bb3f2-154">Result:</span></span>

<span data-ttu-id="bb3f2-155">Cuando reciba un resultado devuelto, puede asumir Hola puerta de enlace se restableció correctamente.</span><span class="sxs-lookup"><span data-stu-id="bb3f2-155">When you receive a return result, you can assume hello gateway reset was successful.</span></span> <span data-ttu-id="bb3f2-156">Sin embargo, hay nada en el resultado devuelto Hola que indica explícitamente que Hola se restableció correctamente.</span><span class="sxs-lookup"><span data-stu-id="bb3f2-156">However, there is nothing in hello return result that indicates explicitly that hello reset was successful.</span></span> <span data-ttu-id="bb3f2-157">Si desea que toolook estrechamente en hello historial toosee exactamente cuando restablecimiento de puerta de enlace de Hola se ha producido, puede ver esa información en hello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="bb3f2-157">If you want toolook closely at hello history toosee exactly when hello gateway reset occurred, you can view that information in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="bb3f2-158">En el portal de hello, navegue demasiado**"GatewayName" -> mantenimiento de recursos**.</span><span class="sxs-lookup"><span data-stu-id="bb3f2-158">In hello portal, navigate too**'GatewayName' -> Resource Health**.</span></span>
