---
title: "Eliminación de una puerta de enlace de red virtual: PowerShell y Azure Resource Manager | Microsoft Docs"
description: "Elimine una puerta de enlace de red virtual mediante PowerShell en el modelo de implementación de Resource Manager."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: 
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/20/2017
ms.author: cherylmc
ms.openlocfilehash: 4d0f085423d5bd60b24d88649ee1d77bcd1d009f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="delete-a-virtual-network-gateway-using-powershell"></a><span data-ttu-id="6b113-103">Eliminación de una puerta de enlace de red virtual mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="6b113-103">Delete a virtual network gateway using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6b113-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="6b113-104">Azure portal</span></span>](vpn-gateway-delete-vnet-gateway-portal.md)
> * [<span data-ttu-id="6b113-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6b113-105">PowerShell</span></span>](vpn-gateway-delete-vnet-gateway-powershell.md)
> * [<span data-ttu-id="6b113-106">PowerShell (clásico)</span><span class="sxs-lookup"><span data-stu-id="6b113-106">PowerShell (classic)</span></span>](vpn-gateway-delete-vnet-gateway-classic-powershell.md)
>
>

<span data-ttu-id="6b113-107">Hay un par de enfoques que puede adoptar cuando desee eliminar una puerta de enlace de red virtual correspondiente a una configuración de puerta de enlace VPN.</span><span class="sxs-lookup"><span data-stu-id="6b113-107">There are a couple of different approaches you can take when you want to delete a virtual network gateway for a VPN gateway configuration.</span></span>

- <span data-ttu-id="6b113-108">Si quiere eliminar todo el contenido y volver a empezar, como en el caso de un entorno de prueba, puede eliminar el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="6b113-108">If you want to delete everything and start over, as in the case of a test environment, you can delete the resource group.</span></span> <span data-ttu-id="6b113-109">Cuando se elimina un grupo de recursos, se quitan todos los recursos de él.</span><span class="sxs-lookup"><span data-stu-id="6b113-109">When you delete a resource group, it deletes all the resources within the group.</span></span> <span data-ttu-id="6b113-110">Este método solo se recomienda si no desea conservar los recursos del grupo en cuestión.</span><span class="sxs-lookup"><span data-stu-id="6b113-110">This is method is only recommended if you don't want to keep any of the resources in the resource group.</span></span> <span data-ttu-id="6b113-111">Con este enfoque no podrá eliminar de forma selectiva solo unos pocos recursos.</span><span class="sxs-lookup"><span data-stu-id="6b113-111">You can't selectively delete only a few resources using this approach.</span></span>

- <span data-ttu-id="6b113-112">Si desea mantener algunos de los recursos en el grupo de recursos, será algo más complicado eliminar una puerta de enlace de red virtual.</span><span class="sxs-lookup"><span data-stu-id="6b113-112">If you want to keep some of the resources in your resource group, deleting a virtual network gateway becomes slightly more complicated.</span></span> <span data-ttu-id="6b113-113">Antes de poder eliminar la puerta de enlace de red virtual, primero debe quitar todos los recursos que dependen de la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="6b113-113">Before you can delete the virtual network gateway, you must first delete any resources that are dependent on the gateway.</span></span> <span data-ttu-id="6b113-114">Los pasos que seguirá dependerán del tipo de conexiones que creó y de los recursos dependientes de cada conexión.</span><span class="sxs-lookup"><span data-stu-id="6b113-114">The steps you follow depend on the type of connections that you created and the dependent resources for each connection.</span></span>

## <a name="before-beginning"></a><span data-ttu-id="6b113-115">Antes de comenzar</span><span class="sxs-lookup"><span data-stu-id="6b113-115">Before beginning</span></span>

### <a name="1-download-the-latest-azure-resource-manager-powershell-cmdlets"></a><span data-ttu-id="6b113-116">1. Descargue la versión más reciente de los cmdlets de PowerShell de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="6b113-116">1. Download the latest Azure Resource Manager PowerShell cmdlets.</span></span>

<span data-ttu-id="6b113-117">Descargue e instale la versión más reciente de los cmdlets de PowerShell de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="6b113-117">Download and install the latest version of the Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="6b113-118">Consulte [Cómo instalar y configurar Azure PowerShell](/powershell/azure/overview) para obtener más información sobre cómo instalar y configurar los cmdlets de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6b113-118">For more information about downloading and installing PowerShell cmdlets, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

### <a name="2-connect-to-your-azure-account"></a><span data-ttu-id="6b113-119">2. Conéctese a su cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="6b113-119">2. Connect to your Azure account.</span></span>

<span data-ttu-id="6b113-120">Abre la consola de PowerShell y conéctate a tu cuenta.</span><span class="sxs-lookup"><span data-stu-id="6b113-120">Open your PowerShell console and connect to your account.</span></span> <span data-ttu-id="6b113-121">Use el siguiente ejemplo para conectarse:</span><span class="sxs-lookup"><span data-stu-id="6b113-121">Use the following example to help you connect:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="6b113-122">Compruebe las suscripciones para la cuenta.</span><span class="sxs-lookup"><span data-stu-id="6b113-122">Check the subscriptions for the account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="6b113-123">Si tiene varias suscripciones, seleccione la que quera usar.</span><span class="sxs-lookup"><span data-stu-id="6b113-123">If you have more than one subscription, specify the subscription that you want to use.</span></span>

```powershell
Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"
```

## <span data-ttu-id="6b113-124"><a name="S2S"></a>Eliminación de una VPN de sitio a sitio</span><span class="sxs-lookup"><span data-stu-id="6b113-124"><a name="S2S"></a>Delete a Site-to-Site VPN gateway</span></span>

<span data-ttu-id="6b113-125">Para eliminar una puerta de enlace de red virtual correspondiente a una configuración de S2S, primero debe eliminar cada recurso que pertenece a la puerta de enlace de red virtual.</span><span class="sxs-lookup"><span data-stu-id="6b113-125">To delete a virtual network gateway for a S2S configuration, you must first delete each resource that pertains to the virtual network gateway.</span></span> <span data-ttu-id="6b113-126">Los recursos deben eliminarse en un orden determinado debido a las dependencias.</span><span class="sxs-lookup"><span data-stu-id="6b113-126">Resources must be deleted in a certain order due to dependencies.</span></span> <span data-ttu-id="6b113-127">Cuando se trabaja con los ejemplos siguientes, deben especificarse algunos de los valores, mientras que otros son un resultado de salida.</span><span class="sxs-lookup"><span data-stu-id="6b113-127">When working with the examples below, some of the values must be specified, while other values are an output result.</span></span> <span data-ttu-id="6b113-128">Los siguientes valores específicos de los ejemplos se utilizan para fines de demostración:</span><span class="sxs-lookup"><span data-stu-id="6b113-128">We use the following specific values in the examples for demonstration purposes:</span></span>

<span data-ttu-id="6b113-129">Nombre de la red virtual: VNet1</span><span class="sxs-lookup"><span data-stu-id="6b113-129">VNet name: VNet1</span></span><br>
<span data-ttu-id="6b113-130">Nombre del grupo de recursos: RG1</span><span class="sxs-lookup"><span data-stu-id="6b113-130">Resource Group name: RG1</span></span><br>
<span data-ttu-id="6b113-131">Nombre de la puerta de enlace de red virtual: GW1</span><span class="sxs-lookup"><span data-stu-id="6b113-131">Virtual network gateway name: GW1</span></span><br>

<span data-ttu-id="6b113-132">Los siguientes pasos se aplican al modelo de implementación de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="6b113-132">The following steps apply to the Resource Manager deployment model.</span></span>

### <a name="1-get-the-virtual-network-gateway-that-you-want-to-delete"></a><span data-ttu-id="6b113-133">1. Obtenga la puerta de enlace de red virtual que quiera eliminar.</span><span class="sxs-lookup"><span data-stu-id="6b113-133">1. Get the virtual network gateway that you want to delete.</span></span>

```powershell
$Gateway=get-azurermvirtualnetworkgateway -Name "GW1" -ResourceGroupName "RG1"
```

### <a name="2-check-to-see-if-the-virtual-network-gateway-has-any-connections"></a><span data-ttu-id="6b113-134">2. Compruebe si la puerta de enlace de red virtual tiene todas las conexiones.</span><span class="sxs-lookup"><span data-stu-id="6b113-134">2. Check to see if the virtual network gateway has any connections.</span></span>

```powershell
get-azurermvirtualnetworkgatewayconnection -ResourceGroupName "RG1" | where-object {$_.VirtualNetworkGateway1.Id -eq $GW.Id}
$Conns=get-azurermvirtualnetworkgatewayconnection -ResourceGroupName "RG1" | where-object {$_.VirtualNetworkGateway1.Id -eq $GW.Id}
```

### <a name="3-delete-all-connections"></a><span data-ttu-id="6b113-135">3. Elimine todas las conexiones.</span><span class="sxs-lookup"><span data-stu-id="6b113-135">3. Delete all connections.</span></span>

<span data-ttu-id="6b113-136">Se le pedirá que confirme la eliminación de cada una de las conexiones.</span><span class="sxs-lookup"><span data-stu-id="6b113-136">You may be prompted to confirm the deletion of each of the connections.</span></span>

```powershell
$Conns | ForEach-Object {Remove-AzureRmVirtualNetworkGatewayConnection -Name $_.name -ResourceGroupName $_.ResourceGroupName}
```

### <a name="4-delete-the-virtual-network-gateway"></a><span data-ttu-id="6b113-137">4. Elimine la puerta de enlace de red virtual.</span><span class="sxs-lookup"><span data-stu-id="6b113-137">4. Delete the virtual network gateway.</span></span>

<span data-ttu-id="6b113-138">Se le pedirá que confirme la eliminación de la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="6b113-138">You may be prompted to confirm the deletion of the gateway.</span></span> <span data-ttu-id="6b113-139">Si tiene una configuración P2S en esta red virtual además de la configuración S2S, eliminando la puerta de enlace de red virtual se desconectarán automáticamente todos los clientes P2S sin previo aviso.</span><span class="sxs-lookup"><span data-stu-id="6b113-139">If you have a P2S configuration to this VNet in addition to your S2S configuration, deleting the virtual network gateway will automatically disconnect all P2S clients without warning.</span></span>


```powershell
Remove-AzureRmVirtualNetworkGateway -Name "GW1" -ResourceGroupName "RG1"
```

<span data-ttu-id="6b113-140">En este momento, la puerta de enlace de virtual se ha eliminado.</span><span class="sxs-lookup"><span data-stu-id="6b113-140">At this point, your virtual network gateway has been deleted.</span></span> <span data-ttu-id="6b113-141">Puede usar los pasos siguientes para eliminar los recursos que ya no se usan.</span><span class="sxs-lookup"><span data-stu-id="6b113-141">You can use the next steps to delete any resources that are no longer being used.</span></span>

### <a name="5-delete-the-local-network-gateways"></a><span data-ttu-id="6b113-142">5. Elimine las puertas de enlace de red locales.</span><span class="sxs-lookup"><span data-stu-id="6b113-142">5 Delete the local network gateways.</span></span>

<span data-ttu-id="6b113-143">Obtenga la lista de las puertas de enlace de red locales correspondientes.</span><span class="sxs-lookup"><span data-stu-id="6b113-143">Get the list of the corresponding local network gateways.</span></span>

```powershell
$LNG=Get-AzureRmLocalNetworkGateway -ResourceGroupName "RG1" | where-object {$_.Id -In $Conns.LocalNetworkGateway2.Id}
```

<span data-ttu-id="6b113-144">Elimine las puertas de enlace de red locales.</span><span class="sxs-lookup"><span data-stu-id="6b113-144">Delete the local network gateways.</span></span> <span data-ttu-id="6b113-145">Se le pedirá que confirme la eliminación de cada una de las puertas de enlace de red locales.</span><span class="sxs-lookup"><span data-stu-id="6b113-145">You may be prompted to confirm the deletion of each of the local network gateway.</span></span>

```powershell
$LNG | ForEach-Object {Remove-AzureRmLocalNetworkGateway -Name $_.Name -ResourceGroupName $_.ResourceGroupName}
```

### <a name="6-delete-the-public-ip-address-resources"></a><span data-ttu-id="6b113-146">6. Elimine los recursos de dirección IP pública.</span><span class="sxs-lookup"><span data-stu-id="6b113-146">6. Delete the Public IP address resources.</span></span>

<span data-ttu-id="6b113-147">Obtenga las configuraciones de direcciones IP de la puerta de enlace de red virtual.</span><span class="sxs-lookup"><span data-stu-id="6b113-147">Get the IP configurations of the virtual network gateway.</span></span>

```powershell
$GWIpConfigs = $Gateway.IpConfigurations
```

<span data-ttu-id="6b113-148">Obtenga la lista de recursos de direcciones IP públicas que se usan para esta puerta de enlace de red virtual.</span><span class="sxs-lookup"><span data-stu-id="6b113-148">Get the list of Public IP address resources used for this virtual network gateway.</span></span> <span data-ttu-id="6b113-149">Si la puerta de enlace de red virtual era activa-activa, verá dos direcciones IP públicas.</span><span class="sxs-lookup"><span data-stu-id="6b113-149">If the virtual network gateway was active-active, you will see two Public IP addresses.</span></span>

```powershell
$PubIP=Get-AzureRmPublicIpAddress | where-object {$_.Id -In $GWIpConfigs.PublicIpAddress.Id}
```

<span data-ttu-id="6b113-150">Elimine los recursos de IP pública.</span><span class="sxs-lookup"><span data-stu-id="6b113-150">Delete the Public IP resources.</span></span>

```powershell
$PubIP | foreach-object {remove-azurermpublicIpAddress -Name $_.Name -ResourceGroupName "RG1"}
```

### <a name="7-delete-the-gateway-subnet-and-set-the-configuration"></a><span data-ttu-id="6b113-151">7. Elimine la subred de puerta de enlace y establezca la configuración.</span><span class="sxs-lookup"><span data-stu-id="6b113-151">7. Delete the gateway subnet and set the configuration.</span></span>

```powershell
$GWSub = Get-AzureRmVirtualNetwork -ResourceGroupName "RG1" -Name "VNet1" | Remove-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet"
Set-AzureRmVirtualNetwork -VirtualNetwork $GWSub
```

## <span data-ttu-id="6b113-152"><a name="v2v"></a>Eliminación de una puerta de enlace VPN de red virtual a red virtual</span><span class="sxs-lookup"><span data-stu-id="6b113-152"><a name="v2v"></a>Delete a VNet-to-VNet VPN gateway</span></span>

<span data-ttu-id="6b113-153">Para eliminar una puerta de enlace de red virtual correspondiente a una configuración de V2V, primero debe eliminar cada recurso que pertenece a la puerta de enlace de red virtual.</span><span class="sxs-lookup"><span data-stu-id="6b113-153">To delete a virtual network gateway for a V2V configuration, you must first delete each resource that pertains to the virtual network gateway.</span></span> <span data-ttu-id="6b113-154">Los recursos deben eliminarse en un orden determinado debido a las dependencias.</span><span class="sxs-lookup"><span data-stu-id="6b113-154">Resources must be deleted in a certain order due to dependencies.</span></span> <span data-ttu-id="6b113-155">Cuando se trabaja con los ejemplos siguientes, deben especificarse algunos de los valores, mientras que otros son un resultado de salida.</span><span class="sxs-lookup"><span data-stu-id="6b113-155">When working with the examples below, some of the values must be specified, while other values are an output result.</span></span> <span data-ttu-id="6b113-156">Los siguientes valores específicos de los ejemplos se utilizan para fines de demostración:</span><span class="sxs-lookup"><span data-stu-id="6b113-156">We use the following specific values in the examples for demonstration purposes:</span></span>

<span data-ttu-id="6b113-157">Nombre de la red virtual: VNet1</span><span class="sxs-lookup"><span data-stu-id="6b113-157">VNet name: VNet1</span></span><br>
<span data-ttu-id="6b113-158">Nombre del grupo de recursos: RG1</span><span class="sxs-lookup"><span data-stu-id="6b113-158">Resource Group name: RG1</span></span><br>
<span data-ttu-id="6b113-159">Nombre de la puerta de enlace de red virtual: GW1</span><span class="sxs-lookup"><span data-stu-id="6b113-159">Virtual network gateway name: GW1</span></span><br>

<span data-ttu-id="6b113-160">Los siguientes pasos se aplican al modelo de implementación de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="6b113-160">The following steps apply to the Resource Manager deployment model.</span></span>

### <a name="1-get-the-virtual-network-gateway-that-you-want-to-delete"></a><span data-ttu-id="6b113-161">1. Obtenga la puerta de enlace de red virtual que quiera eliminar.</span><span class="sxs-lookup"><span data-stu-id="6b113-161">1. Get the virtual network gateway that you want to delete.</span></span>

```powershell
$Gateway=get-azurermvirtualnetworkgateway -Name "GW1" -ResourceGroupName "RG1"
```

### <a name="2-check-to-see-if-the-virtual-network-gateway-has-any-connections"></a><span data-ttu-id="6b113-162">2. Compruebe si la puerta de enlace de red virtual tiene todas las conexiones.</span><span class="sxs-lookup"><span data-stu-id="6b113-162">2. Check to see if the virtual network gateway has any connections.</span></span>

```powershell
get-azurermvirtualnetworkgatewayconnection -ResourceGroupName "RG1" | where-object {$_.VirtualNetworkGateway1.Id -eq $GW.Id}
```
 
<span data-ttu-id="6b113-163">Puede haber otra conexión a la puerta de enlace de red virtual que forman parte de otro grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="6b113-163">There may be other connections to the virtual network gateway that are part of a different resource group.</span></span> <span data-ttu-id="6b113-164">Busque conexiones adicionales en cada grupo de recursos extra.</span><span class="sxs-lookup"><span data-stu-id="6b113-164">Check for additional connections in each additional resource group.</span></span> <span data-ttu-id="6b113-165">En este ejemplo, vamos a comprobar las conexiones desde RG2.</span><span class="sxs-lookup"><span data-stu-id="6b113-165">In this example, we are checking for connections from RG2.</span></span> <span data-ttu-id="6b113-166">Ejecute este comando en cada grupo de recursos que tenga que puede estar conectado a la puerta de enlace de red virtual.</span><span class="sxs-lookup"><span data-stu-id="6b113-166">Run this for each resource group that you have which may have a connection to the virtual network gateway.</span></span>

```powershell
get-azurermvirtualnetworkgatewayconnection -ResourceGroupName "RG2" | where-object {$_.VirtualNetworkGateway2.Id -eq $GW.Id}
```

### <a name="3-get-the-list-of-connections-in-both-directions"></a><span data-ttu-id="6b113-167">3. Obtenga la lista de conexiones en ambas direcciones.</span><span class="sxs-lookup"><span data-stu-id="6b113-167">3. Get the list of connections in both directions.</span></span>

<span data-ttu-id="6b113-168">Como se trata de una configuración de red virtual a red virtual, necesita la lista de conexiones en ambas direcciones.</span><span class="sxs-lookup"><span data-stu-id="6b113-168">Because this is a VNet-to-VNet configuration, you need the list of connections in both directions.</span></span>

```powershell
$ConnsL=get-azurermvirtualnetworkgatewayconnection -ResourceGroupName "RG1" | where-object {$_.VirtualNetworkGateway1.Id -eq $GW.Id}
```
 
<span data-ttu-id="6b113-169">En este ejemplo, vamos a comprobar las conexiones desde RG2.</span><span class="sxs-lookup"><span data-stu-id="6b113-169">In this example, we are checking for connections from RG2.</span></span> <span data-ttu-id="6b113-170">Ejecute este comando en cada grupo de recursos que tenga que puede estar conectado a la puerta de enlace de red virtual.</span><span class="sxs-lookup"><span data-stu-id="6b113-170">Run this for each resource group that you have which may have a connection to the virtual network gateway.</span></span>

```powershell
 $ConnsR=get-azurermvirtualnetworkgatewayconnection -ResourceGroupName "<NameOfResourceGroup2>" | where-object {$_.VirtualNetworkGateway2.Id -eq $GW.Id}
 ```

### <a name="4-delete-all-connections"></a><span data-ttu-id="6b113-171">4. Elimine todas las conexiones.</span><span class="sxs-lookup"><span data-stu-id="6b113-171">4. Delete all connections.</span></span>

<span data-ttu-id="6b113-172">Se le pedirá que confirme la eliminación de cada una de las conexiones.</span><span class="sxs-lookup"><span data-stu-id="6b113-172">You may be prompted to confirm the deletion of each of the connections.</span></span>

```powershell
$ConnsL | ForEach-Object {Remove-AzureRmVirtualNetworkGatewayConnection -Name $_.name -ResourceGroupName $_.ResourceGroupName}
$ConnsR | ForEach-Object {Remove-AzureRmVirtualNetworkGatewayConnection -Name $_.name -ResourceGroupName $_.ResourceGroupName}
```

### <a name="5-delete-the-virtual-network-gateway"></a><span data-ttu-id="6b113-173">5. Elimine la puerta de enlace de red virtual.</span><span class="sxs-lookup"><span data-stu-id="6b113-173">5. Delete the virtual network gateway.</span></span>

<span data-ttu-id="6b113-174">Se le pedirá que confirme la eliminación de la puerta de enlace de red virtual.</span><span class="sxs-lookup"><span data-stu-id="6b113-174">You may be prompted to confirm the deletion of the virtual network gateway.</span></span> <span data-ttu-id="6b113-175">Si tiene una configuración P2S en esta red virtual además de la configuración V2V, eliminando la puerta de enlace de red virtual se desconectarán automáticamente todos los clientes P2S sin previo aviso.</span><span class="sxs-lookup"><span data-stu-id="6b113-175">If you have P2S configurations to your VNets in addition to your V2V configuration, deleting the virtual network gateways will automatically disconnect all P2S clients without warning.</span></span>

```powershell
Remove-AzureRmVirtualNetworkGateway -Name "GW1" -ResourceGroupName "RG1"
```

<span data-ttu-id="6b113-176">En este momento, la puerta de enlace de virtual se ha eliminado.</span><span class="sxs-lookup"><span data-stu-id="6b113-176">At this point, your virtual network gateway has been deleted.</span></span> <span data-ttu-id="6b113-177">Puede usar los pasos siguientes para eliminar los recursos que ya no se usan.</span><span class="sxs-lookup"><span data-stu-id="6b113-177">You can use the next steps to delete any resources that are no longer being used.</span></span>

### <a name="6-delete-the-public-ip-address-resources"></a><span data-ttu-id="6b113-178">6. Elimine los recursos de dirección IP pública.</span><span class="sxs-lookup"><span data-stu-id="6b113-178">6. Delete the Public IP address resources</span></span>

<span data-ttu-id="6b113-179">Obtenga las configuraciones de direcciones IP de la puerta de enlace de red virtual.</span><span class="sxs-lookup"><span data-stu-id="6b113-179">Get the IP configurations of the virtual network gateway.</span></span>

```powershell
$GWIpConfigs = $Gateway.IpConfigurations
```

<span data-ttu-id="6b113-180">Obtenga la lista de recursos de direcciones IP públicas que se usan para esta puerta de enlace de red virtual.</span><span class="sxs-lookup"><span data-stu-id="6b113-180">Get the list of Public IP address resources used for this virtual network gateway.</span></span> <span data-ttu-id="6b113-181">Si la puerta de enlace de red virtual era activa-activa, verá dos direcciones IP públicas.</span><span class="sxs-lookup"><span data-stu-id="6b113-181">If the virtual network gateway was active-active, you will see two Public IP addresses.</span></span>

```powershell
$PubIP=Get-AzureRmPublicIpAddress | where-object {$_.Id -In $GWIpConfigs.PublicIpAddress.Id}
```

<span data-ttu-id="6b113-182">Elimine los recursos de IP pública.</span><span class="sxs-lookup"><span data-stu-id="6b113-182">Delete the Public IP resources.</span></span> <span data-ttu-id="6b113-183">Se le pedirá que confirme la eliminación de la dirección IP pública.</span><span class="sxs-lookup"><span data-stu-id="6b113-183">You may be prompted to confirm the deletion of the Public IP.</span></span>

```powershell
$PubIP | foreach-object {remove-azurermpublicIpAddress -Name $_.Name -ResourceGroupName "<NameOfResourceGroup1>"}
```

### <a name="7-delete-the-gateway-subnet-and-set-the-configuration"></a><span data-ttu-id="6b113-184">7. Elimine la subred de puerta de enlace y establezca la configuración.</span><span class="sxs-lookup"><span data-stu-id="6b113-184">7. Delete the gateway subnet and set the configuration.</span></span>

```powershell
$GWSub = Get-AzureRmVirtualNetwork -ResourceGroupName "RG1" -Name "VNet1" | Remove-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet"
Set-AzureRmVirtualNetwork -VirtualNetwork $GWSub
```

## <span data-ttu-id="6b113-185"><a name="deletep2s"></a>Eliminación de una puerta de enlace VPN de sitio a sitio</span><span class="sxs-lookup"><span data-stu-id="6b113-185"><a name="deletep2s"></a>Delete a Point-to-Site VPN gateway</span></span>

<span data-ttu-id="6b113-186">Para eliminar una puerta de enlace de red virtual correspondiente a una configuración de P2S, primero debe eliminar cada recurso que pertenece a la puerta de enlace de red virtual.</span><span class="sxs-lookup"><span data-stu-id="6b113-186">To delete a virtual network gateway for a P2S configuration, you must first delete each resource that pertains to the virtual network gateway.</span></span> <span data-ttu-id="6b113-187">Los recursos deben eliminarse en un orden determinado debido a las dependencias.</span><span class="sxs-lookup"><span data-stu-id="6b113-187">Resources must be deleted in a certain order due to dependencies.</span></span> <span data-ttu-id="6b113-188">Cuando se trabaja con los ejemplos siguientes, deben especificarse algunos de los valores, mientras que otros son un resultado de salida.</span><span class="sxs-lookup"><span data-stu-id="6b113-188">When working with the examples below, some of the values must be specified, while other values are an output result.</span></span> <span data-ttu-id="6b113-189">Los siguientes valores específicos de los ejemplos se utilizan para fines de demostración:</span><span class="sxs-lookup"><span data-stu-id="6b113-189">We use the following specific values in the examples for demonstration purposes:</span></span>

<span data-ttu-id="6b113-190">Nombre de la red virtual: VNet1</span><span class="sxs-lookup"><span data-stu-id="6b113-190">VNet name: VNet1</span></span><br>
<span data-ttu-id="6b113-191">Nombre del grupo de recursos: RG1</span><span class="sxs-lookup"><span data-stu-id="6b113-191">Resource Group name: RG1</span></span><br>
<span data-ttu-id="6b113-192">Nombre de la puerta de enlace de red virtual: GW1</span><span class="sxs-lookup"><span data-stu-id="6b113-192">Virtual network gateway name: GW1</span></span><br>

<span data-ttu-id="6b113-193">Los siguientes pasos se aplican al modelo de implementación de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="6b113-193">The following steps apply to the Resource Manager deployment model.</span></span>


>[!NOTE]
> <span data-ttu-id="6b113-194">Cuando se elimina la puerta de enlace VPN, se desconectarán todos los clientes conectados de la red virtual sin previo aviso.</span><span class="sxs-lookup"><span data-stu-id="6b113-194">When you delete the VPN gateway, all connected clients will be disconnected from the VNet without warning.</span></span>
>
>

### <a name="1-get-the-virtual-network-gateway-that-you-want-to-delete"></a><span data-ttu-id="6b113-195">1. Obtenga la puerta de enlace de red virtual que quiera eliminar.</span><span class="sxs-lookup"><span data-stu-id="6b113-195">1. Get the virtual network gateway that you want to delete.</span></span>

```powershell
$Gateway=get-azurermvirtualnetworkgateway -Name "GW1" -ResourceGroupName "RG1"
```

### <a name="2-delete-the-virtual-network-gateway"></a><span data-ttu-id="6b113-196">2. Elimine la puerta de enlace de red virtual.</span><span class="sxs-lookup"><span data-stu-id="6b113-196">2. Delete the virtual network gateway.</span></span>

<span data-ttu-id="6b113-197">Se le pedirá que confirme la eliminación de la puerta de enlace de red virtual.</span><span class="sxs-lookup"><span data-stu-id="6b113-197">You may be prompted to confirm the deletion of the virtual network gateway.</span></span>

```powershell
Remove-AzureRmVirtualNetworkGateway -Name "GW1" -ResourceGroupName "RG1"
```

<span data-ttu-id="6b113-198">En este momento, la puerta de enlace de virtual se ha eliminado.</span><span class="sxs-lookup"><span data-stu-id="6b113-198">At this point, your virtual network gateway has been deleted.</span></span> <span data-ttu-id="6b113-199">Puede usar los pasos siguientes para eliminar los recursos que ya no se usan.</span><span class="sxs-lookup"><span data-stu-id="6b113-199">You can use the next steps to delete any resources that are no longer being used.</span></span>

### <a name="3-delete-the-public-ip-address-resources"></a><span data-ttu-id="6b113-200">3. Elimine los recursos de dirección IP pública.</span><span class="sxs-lookup"><span data-stu-id="6b113-200">3. Delete the Public IP address resources</span></span>

<span data-ttu-id="6b113-201">Obtenga las configuraciones de direcciones IP de la puerta de enlace de red virtual.</span><span class="sxs-lookup"><span data-stu-id="6b113-201">Get the IP configurations of the virtual network gateway.</span></span>

```powershell
$GWIpConfigs = $Gateway.IpConfigurations
```

<span data-ttu-id="6b113-202">Obtenga la lista de direcciones IP públicas que se usan para esta puerta de enlace de red virtual.</span><span class="sxs-lookup"><span data-stu-id="6b113-202">Get the list of Public IP addresses used for this virtual network gateway.</span></span> <span data-ttu-id="6b113-203">Si la puerta de enlace de red virtual era activa-activa, verá dos direcciones IP públicas.</span><span class="sxs-lookup"><span data-stu-id="6b113-203">If the virtual network gateway was active-active, you will see two Public IP addresses.</span></span>

```powershell
$PubIP=Get-AzureRmPublicIpAddress | where-object {$_.Id -In $GWIpConfigs.PublicIpAddress.Id}
```

<span data-ttu-id="6b113-204">Elimine las direcciones IP públicas.</span><span class="sxs-lookup"><span data-stu-id="6b113-204">Delete the Public IPs.</span></span> <span data-ttu-id="6b113-205">Se le pedirá que confirme la eliminación de la dirección IP pública.</span><span class="sxs-lookup"><span data-stu-id="6b113-205">You may be prompted to confirm the deletion of the Public IP.</span></span>

```powershell
$PubIP | foreach-object {remove-azurermpublicIpAddress -Name $_.Name -ResourceGroupName "<NameOfResourceGroup1>"}
```

### <a name="4-delete-the-gateway-subnet-and-set-the-configuration"></a><span data-ttu-id="6b113-206">4. Elimine la subred de puerta de enlace y establezca la configuración.</span><span class="sxs-lookup"><span data-stu-id="6b113-206">4. Delete the gateway subnet and set the configuration.</span></span>

```powershell
$GWSub = Get-AzureRmVirtualNetwork -ResourceGroupName "RG1" -Name "VNet1" | Remove-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet"
Set-AzureRmVirtualNetwork -VirtualNetwork $GWSub
```

## <span data-ttu-id="6b113-207"><a name="delete"></a>Eliminación de una puerta de enlace VPN mediante la eliminación del grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="6b113-207"><a name="delete"></a>Delete a VPN gateway by deleting the resource group</span></span>

<span data-ttu-id="6b113-208">Si no desea mantener ninguno de los recursos del grupo, sino que desea empezar de nuevo, puede eliminar dicho grupo al completo.</span><span class="sxs-lookup"><span data-stu-id="6b113-208">If you are not concerned about keeping any of your resources in the resource group and you just want to start over, you can delete an entire resource group.</span></span> <span data-ttu-id="6b113-209">Se trata de una forma rápida de quitarlos todos.</span><span class="sxs-lookup"><span data-stu-id="6b113-209">This is a quick way to remove everything.</span></span> <span data-ttu-id="6b113-210">Los siguientes pasos se aplican solo al modelo de implementación de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="6b113-210">The following steps apply only to the Resource Manager deployment model.</span></span>

### <a name="1-get-a-list-of-all-the-resource-groups-in-your-subscription"></a><span data-ttu-id="6b113-211">1. Obtenga una lista de todos los grupos de recursos de la suscripción:</span><span class="sxs-lookup"><span data-stu-id="6b113-211">1. Get a list of all the resource groups in your subscription.</span></span>

```powershell
Get-AzureRmResourceGroup
```

### <a name="2-locate-the-resource-group-that-you-want-to-delete"></a><span data-ttu-id="6b113-212">2. Localice el grupo de recursos que desea eliminar.</span><span class="sxs-lookup"><span data-stu-id="6b113-212">2. Locate the resource group that you want to delete.</span></span>

<span data-ttu-id="6b113-213">Localice el grupo de recursos que quiera eliminar y vea la lista de recursos de dicho grupo.</span><span class="sxs-lookup"><span data-stu-id="6b113-213">Locate the resource group that you want to delete and view the list of resources in that resource group.</span></span> <span data-ttu-id="6b113-214">En el ejemplo, el nombre del grupo de recursos es RG 1.</span><span class="sxs-lookup"><span data-stu-id="6b113-214">In the example, the name of the resource group is RG1.</span></span> <span data-ttu-id="6b113-215">Modifique el ejemplo para recuperar una lista de todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="6b113-215">Modify the example to retrieve a list of all the resources.</span></span>

```powershell
Find-AzureRmResource -ResourceGroupNameContains RG1
```

### <a name="3-verify-the-resources-in-the-list"></a><span data-ttu-id="6b113-216">3. Compruebe los recursos de la lista.</span><span class="sxs-lookup"><span data-stu-id="6b113-216">3. Verify the resources in the list.</span></span>

<span data-ttu-id="6b113-217">Cuando se devuelve la lista, revísela para comprobar que desea eliminar todos los recursos del grupo de recursos, así como dicho grupo.</span><span class="sxs-lookup"><span data-stu-id="6b113-217">When the list is returned, review it to verify that you want to delete all the resources in the resource group, as well as the resource group itself.</span></span> <span data-ttu-id="6b113-218">Si desea mantener algunos de los recursos del grupo de recursos, utilice los pasos de las secciones anteriores de este artículo para eliminar la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="6b113-218">If you want to keep some of the resources in the resource group, use the steps in the earlier sections of this article to delete your gateway.</span></span>

### <a name="4-delete-the-resource-group-and-resources"></a><span data-ttu-id="6b113-219">4. Elimine el grupo de recursos y los recursos.</span><span class="sxs-lookup"><span data-stu-id="6b113-219">4. Delete the resource group and resources.</span></span>

<span data-ttu-id="6b113-220">Para eliminar el grupo de recursos y todos los recursos de este, modifique el ejemplo y ejecútelo.</span><span class="sxs-lookup"><span data-stu-id="6b113-220">To delete the resource group and all the resource contained in the resource group, modify the example and run.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name RG1
```

### <a name="5-check-the-status"></a><span data-ttu-id="6b113-221">5. Compruebe el estado.</span><span class="sxs-lookup"><span data-stu-id="6b113-221">5. Check the status.</span></span>

<span data-ttu-id="6b113-222">Azure tarda unos minutos en eliminar todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="6b113-222">It takes some time for Azure to delete all the resources.</span></span> <span data-ttu-id="6b113-223">Puede comprobar el estado de su grupo de recursos con este cmdlet.</span><span class="sxs-lookup"><span data-stu-id="6b113-223">You can check the status of your resource group by using this cmdlet.</span></span>

```powershell
Get-AzureRmResourceGroup -ResourceGroupName RG1
```

<span data-ttu-id="6b113-224">El resultado que se devuelve se muestra "Correcto".</span><span class="sxs-lookup"><span data-stu-id="6b113-224">The result that is returned shows 'Succeeded'.</span></span>

```
ResourceGroupName : RG1
Location          : eastus
ProvisioningState : Succeeded
```