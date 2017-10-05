---
title: "Conexión de la red local a una red virtual de Azure: VPN de sitio a sitio: PowerShell | Microsoft Docs"
description: "Pasos para crear una conexión de IPsec desde la red local a una red virtual de Azure a través de la red pública de Internet. Estos pasos le ayudarán a crear una conexión de VPN Gateway de sitio a sitio entre locales mediante PowerShell."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: fcc2fda5-4493-4c15-9436-84d35adbda8e
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/09/2017
ms.author: cherylmc
ms.openlocfilehash: 27f4a8fb9a83b98e99df635bf4c80f6048ce348c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-vnet-with-a-site-to-site-vpn-connection-using-powershell"></a><span data-ttu-id="7444e-104">Creación de una red virtual con una conexión VPN de sitio a sitio mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="7444e-104">Create a VNet with a Site-to-Site VPN connection using PowerShell</span></span>

<span data-ttu-id="7444e-105">Este artículo muestra cómo usar PowerShell para crear una conexión de puerta de enlace VPN de sitio a sitio desde la red local a la red virtual.</span><span class="sxs-lookup"><span data-stu-id="7444e-105">This article shows you how to use PowerShell to create a Site-to-Site VPN gateway connection from your on-premises network to the VNet.</span></span> <span data-ttu-id="7444e-106">Los pasos descritos en este artículo se aplican al modelo de implementación de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="7444e-106">The steps in this article apply to the Resource Manager deployment model.</span></span> <span data-ttu-id="7444e-107">También se puede crear esta configuración con una herramienta o modelo de implementación distintos, mediante la selección de una opción diferente en la lista siguiente:</span><span class="sxs-lookup"><span data-stu-id="7444e-107">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from the following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="7444e-108">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="7444e-108">Azure portal</span></span>](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="7444e-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7444e-109">PowerShell</span></span>](vpn-gateway-create-site-to-site-rm-powershell.md)
> * [<span data-ttu-id="7444e-110">CLI</span><span class="sxs-lookup"><span data-stu-id="7444e-110">CLI</span></span>](vpn-gateway-howto-site-to-site-resource-manager-cli.md)
> * [<span data-ttu-id="7444e-111">Portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="7444e-111">Azure portal (classic)</span></span>](vpn-gateway-howto-site-to-site-classic-portal.md)
> * [<span data-ttu-id="7444e-112">Portal clásico (clásico)</span><span class="sxs-lookup"><span data-stu-id="7444e-112">Classic portal (classic)</span></span>](vpn-gateway-site-to-site-create.md)
> 
>


<span data-ttu-id="7444e-113">Se utiliza una conexión de puerta de enlace VPN de sitio a sitio para conectar su red local a una red virtual de Azure a través de un túnel VPN de IPsec/IKE (IKEv1 o IKEv2).</span><span class="sxs-lookup"><span data-stu-id="7444e-113">A Site-to-Site VPN gateway connection is used to connect your on-premises network to an Azure virtual network over an IPsec/IKE (IKEv1 or IKEv2) VPN tunnel.</span></span> <span data-ttu-id="7444e-114">Este tipo de conexión requiere un dispositivo VPN local que tenga una dirección IP pública asignada.</span><span class="sxs-lookup"><span data-stu-id="7444e-114">This type of connection requires a VPN device located on-premises that has an externally facing public IP address assigned to it.</span></span> <span data-ttu-id="7444e-115">Para más información acerca de las puertas de enlace VPN, consulte [Acerca de VPN Gateway](vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="7444e-115">For more information about VPN gateways, see [About VPN gateway](vpn-gateway-about-vpngateways.md).</span></span>

![Diagrama de la conexión entre locales de VPN Gateway de sitio a sitio](./media/vpn-gateway-create-site-to-site-rm-powershell/site-to-site-diagram.png)

## <span data-ttu-id="7444e-117"><a name="before"></a>Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="7444e-117"><a name="before"></a>Before you begin</span></span>

<span data-ttu-id="7444e-118">Antes de comenzar con la configuración, compruebe que se cumplen los criterios siguientes:</span><span class="sxs-lookup"><span data-stu-id="7444e-118">Verify that you have met the following criteria before beginning your configuration:</span></span>

* <span data-ttu-id="7444e-119">Asegúrese de tener un dispositivo VPN compatible y alguien que pueda configurarlo.</span><span class="sxs-lookup"><span data-stu-id="7444e-119">Make sure you have a compatible VPN device and someone who is able to configure it.</span></span> <span data-ttu-id="7444e-120">Para más información acerca de los dispositivos VPN compatibles y su configuración, consulte [Acerca de los dispositivos VPN](vpn-gateway-about-vpn-devices.md).</span><span class="sxs-lookup"><span data-stu-id="7444e-120">For more information about compatible VPN devices and device configuration, see [About VPN Devices](vpn-gateway-about-vpn-devices.md).</span></span>
* <span data-ttu-id="7444e-121">Compruebe que tiene una dirección IPv4 pública externa para el dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="7444e-121">Verify that you have an externally facing public IPv4 address for your VPN device.</span></span> <span data-ttu-id="7444e-122">Esta dirección IP no puede estar detrás de un NAT.</span><span class="sxs-lookup"><span data-stu-id="7444e-122">This IP address cannot be located behind a NAT.</span></span>
* <span data-ttu-id="7444e-123">Si no está familiarizado con los intervalos de direcciones IP ubicados en la red local, necesita trabajar con alguien que pueda proporcionarle estos detalles.</span><span class="sxs-lookup"><span data-stu-id="7444e-123">If you are unfamiliar with the IP address ranges located in your on-premises network configuration, you need to coordinate with someone who can provide those details for you.</span></span> <span data-ttu-id="7444e-124">Al crear esta configuración, debe especificar los prefijos del intervalo de direcciones IP al que Azure enrutará la ubicación local.</span><span class="sxs-lookup"><span data-stu-id="7444e-124">When you create this configuration, you must specify the IP address range prefixes that Azure will route to your on-premises location.</span></span> <span data-ttu-id="7444e-125">Ninguna de las subredes de la red local puede superponerse con las subredes de la red virtual a la que desea conectarse.</span><span class="sxs-lookup"><span data-stu-id="7444e-125">None of the subnets of your on-premises network can over lap with the virtual network subnets that you want to connect to.</span></span>
* <span data-ttu-id="7444e-126">Instale la versión más reciente de los cmdlets de PowerShell de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="7444e-126">Install the latest version of the Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="7444e-127">Los cmdlets de PowerShell se actualizan con frecuencia y, por lo general, deberá actualizar los cmdlets de PowerShell para obtener la funcionalidad más reciente de la característica.</span><span class="sxs-lookup"><span data-stu-id="7444e-127">PowerShell cmdlets are updated frequently and you will typically need to update your PowerShell cmdlets to get the latest feature functionality.</span></span> <span data-ttu-id="7444e-128">Si no actualiza los cmdlets de PowerShell, se pueden producir errores en los valores especificados.</span><span class="sxs-lookup"><span data-stu-id="7444e-128">If you don't update your PowerShell cmdlets, the values specified may fail.</span></span> <span data-ttu-id="7444e-129">Consulte [Cómo instalar y configurar Azure PowerShell](/powershell/azure/overview) para más información sobre cómo descargar e instalar los cmdlets de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7444e-129">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for more information about downloading and installing PowerShell cmdlets.</span></span>

### <span data-ttu-id="7444e-130"><a name="example"></a>Valores del ejemplo</span><span class="sxs-lookup"><span data-stu-id="7444e-130"><a name="example"></a>Example values</span></span>

<span data-ttu-id="7444e-131">Los ejemplos de este artículo utilizan los valores siguientes.</span><span class="sxs-lookup"><span data-stu-id="7444e-131">The examples in this article use the following values.</span></span> <span data-ttu-id="7444e-132">Puede usar estos valores para crear un entorno de prueba o hacer referencia a ellos para comprender mejor los ejemplos de este artículo.</span><span class="sxs-lookup"><span data-stu-id="7444e-132">You can use these values to create a test environment, or refer to them to better understand the examples in this article.</span></span>

```
#Example values

VnetName                = TestVNet1
ResourceGroup           = TestRG1
Location                = East US 
AddressSpace            = 10.11.0.0/16 
SubnetName              = Subnet1 
Subnet                  = 10.11.1.0/28 
GatewaySubnet           = 10.11.0.0/27
LocalNetworkGatewayName = Site2
LNG Public IP           = <VPN device IP address> 
Local Address Prefixes  = 10.0.0.0/24, 20.0.0.0/24
Gateway Name            = VNet1GW
PublicIP                = VNet1GWIP
Gateway IP Config       = gwipconfig1 
VPNType                 = RouteBased 
GatewayType             = Vpn 
ConnectionName          = VNet1toSite2

```


## <span data-ttu-id="7444e-133"><a name="Login"></a>1. su suscripción</span><span class="sxs-lookup"><span data-stu-id="7444e-133"><a name="Login"></a>1. Connect to your subscription</span></span>

[!INCLUDE [PowerShell login](../../includes/vpn-gateway-ps-login-include.md)]

## <span data-ttu-id="7444e-134"><a name="VNet"></a>2. Creación de una red virtual y una puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="7444e-134"><a name="VNet"></a>2. Create a virtual network and a gateway subnet</span></span>

<span data-ttu-id="7444e-135">Si no tiene una red virtual, créela.</span><span class="sxs-lookup"><span data-stu-id="7444e-135">If you don't already have a virtual network, create one.</span></span> <span data-ttu-id="7444e-136">Al crear una red virtual, compruebe que los espacios de direcciones especificados no se superponen con los espacios de direcciones que existen en la red local.</span><span class="sxs-lookup"><span data-stu-id="7444e-136">When creating a virtual network, make sure that the address spaces you specify don't overlap any of the address spaces that you have on your on-premises network.</span></span>

[!INCLUDE [About gateway subnets](../../includes/vpn-gateway-about-gwsubnet-include.md)]

[!INCLUDE [No NSG warning](../../includes/vpn-gateway-no-nsg-include.md)]

### <span data-ttu-id="7444e-137"><a name="vnet"></a>Para crear una red virtual y una subred de puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="7444e-137"><a name="vnet"></a>To create a virtual network and a gateway subnet</span></span>

<span data-ttu-id="7444e-138">Este ejemplo crea una red virtual y una subred de la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="7444e-138">This example creates a virtual network and a gateway subnet.</span></span> <span data-ttu-id="7444e-139">Si ya tiene una red virtual que necesite agregar a una subred de puerta de enlace, consulte [Para agregar una subred de puerta de enlace a una red virtual que ya ha creado](#gatewaysubnet).</span><span class="sxs-lookup"><span data-stu-id="7444e-139">If you already have a virtual network that you need to add a gateway subnet to, see [To add a gateway subnet to a virtual network you have already created](#gatewaysubnet).</span></span>

<span data-ttu-id="7444e-140">Cree un grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="7444e-140">Create a resource group:</span></span>

```powershell
New-AzureRmResourceGroup -Name TestRG1 -Location 'East US'
```

<span data-ttu-id="7444e-141">Cree la red virtual.</span><span class="sxs-lookup"><span data-stu-id="7444e-141">Create your virtual network.</span></span>

1. <span data-ttu-id="7444e-142">Establezca las variables.</span><span class="sxs-lookup"><span data-stu-id="7444e-142">Set the variables.</span></span>

  ```powershell
  $subnet1 = New-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -AddressPrefix 10.11.0.0/27
  $subnet2 = New-AzureRmVirtualNetworkSubnetConfig -Name 'Subnet1' -AddressPrefix 10.11.1.0/28
  ```
2. <span data-ttu-id="7444e-143">Cree la red virtual.</span><span class="sxs-lookup"><span data-stu-id="7444e-143">Create the VNet.</span></span>

  ```powershell
  New-AzureRmVirtualNetwork -Name TestVNet1 -ResourceGroupName TestRG1 `
  -Location 'East US' -AddressPrefix 10.11.0.0/16 -Subnet $subnet1, $subnet2
  ```

### <span data-ttu-id="7444e-144"><a name="gatewaysubnet"></a>Para agregar una subred de puerta de enlace a una red virtual que ya ha creado</span><span class="sxs-lookup"><span data-stu-id="7444e-144"><a name="gatewaysubnet"></a>To add a gateway subnet to a virtual network you have already created</span></span>

1. <span data-ttu-id="7444e-145">Establezca las variables.</span><span class="sxs-lookup"><span data-stu-id="7444e-145">Set the variables.</span></span>

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG1 -Name TestVet1
  ```
2. <span data-ttu-id="7444e-146">Cree la subred de la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="7444e-146">Create the gateway subnet.</span></span>

  ```powershell
  Add-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -AddressPrefix 10.11.0.0/27 -VirtualNetwork $vnet
  ```
3. <span data-ttu-id="7444e-147">Establezca la configuración.</span><span class="sxs-lookup"><span data-stu-id="7444e-147">Set the configuration.</span></span>

  ```powershell
  Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```

## <span data-ttu-id="7444e-148">3. <a name="localnet"></a>Creación de la puerta de enlace de red local</span><span class="sxs-lookup"><span data-stu-id="7444e-148">3. <a name="localnet"></a>Create the local network gateway</span></span>

<span data-ttu-id="7444e-149">La puerta de enlace de red local suele hacer referencia a la ubicación local.</span><span class="sxs-lookup"><span data-stu-id="7444e-149">The local network gateway typically refers to your on-premises location.</span></span> <span data-ttu-id="7444e-150">Asigne al sitio un nombre al que Azure pueda hacer referencia y, luego, especifique la dirección IP del dispositivo VPN local con la que creará una conexión.</span><span class="sxs-lookup"><span data-stu-id="7444e-150">You give the site a name by which Azure can refer to it, then specify the IP address of the on-premises VPN device to which you will create a connection.</span></span> <span data-ttu-id="7444e-151">Especifique también los prefijos de dirección IP que se enrutarán a través de la puerta de enlace VPN al dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="7444e-151">You also specify the IP address prefixes that will be routed through the VPN gateway to the VPN device.</span></span> <span data-ttu-id="7444e-152">Los prefijos de dirección que especifique son los prefijos que se encuentran en la red local.</span><span class="sxs-lookup"><span data-stu-id="7444e-152">The address prefixes you specify are the prefixes located on your on-premises network.</span></span> <span data-ttu-id="7444e-153">Puede actualizar fácilmente estos prefijos si cambia su red local.</span><span class="sxs-lookup"><span data-stu-id="7444e-153">If your on-premises network changes, you can easily update the prefixes.</span></span>

<span data-ttu-id="7444e-154">Use los valores siguientes:</span><span class="sxs-lookup"><span data-stu-id="7444e-154">Use the following values:</span></span>

* <span data-ttu-id="7444e-155">*GatewayIPAddress* es la dirección IP del dispositivo VPN local.</span><span class="sxs-lookup"><span data-stu-id="7444e-155">The *GatewayIPAddress* is the IP address of your on-premises VPN device.</span></span> <span data-ttu-id="7444e-156">El dispositivo VPN no se encuentra detrás de un NAT.</span><span class="sxs-lookup"><span data-stu-id="7444e-156">Your VPN device cannot be located behind a NAT.</span></span>
* <span data-ttu-id="7444e-157">*AddressPrefix* es el espacio de direcciones local.</span><span class="sxs-lookup"><span data-stu-id="7444e-157">The *AddressPrefix* is your on-premises address space.</span></span>

<span data-ttu-id="7444e-158">Para agregar una puerta de enlace de red local con un único prefijo de dirección:</span><span class="sxs-lookup"><span data-stu-id="7444e-158">To add a local network gateway with a single address prefix:</span></span>

  ```powershell
  New-AzureRmLocalNetworkGateway -Name Site2 -ResourceGroupName TestRG1 `
  -Location 'East US' -GatewayIpAddress '23.99.221.164' -AddressPrefix '10.0.0.0/24'
  ```

<span data-ttu-id="7444e-159">Para agregar una puerta de enlace de red local con varios prefijos de dirección:</span><span class="sxs-lookup"><span data-stu-id="7444e-159">To add a local network gateway with multiple address prefixes:</span></span>

  ```powershell
  New-AzureRmLocalNetworkGateway -Name Site2 -ResourceGroupName TestRG1 `
  -Location 'East US' -GatewayIpAddress '23.99.221.164' -AddressPrefix @('10.0.0.0/24','20.0.0.0/24')
  ```

<span data-ttu-id="7444e-160">Para modificar los prefijos de dirección IP de su puerta de enlace de red local:</span><span class="sxs-lookup"><span data-stu-id="7444e-160">To modify IP address prefixes for your local network gateway:</span></span><br>
<span data-ttu-id="7444e-161">A veces los prefijos de la puerta de enlace de red local cambian.</span><span class="sxs-lookup"><span data-stu-id="7444e-161">Sometimes your local network gateway prefixes change.</span></span> <span data-ttu-id="7444e-162">Los pasos necesarios para modificar los prefijos de las direcciones IP dependen de si creó una conexión de puerta de enlace de VPN.</span><span class="sxs-lookup"><span data-stu-id="7444e-162">The steps you take to modify your IP address prefixes depend on whether you have created a VPN gateway connection.</span></span> <span data-ttu-id="7444e-163">Consulte la sección [Para modificar los prefijos de dirección IP de una puerta de enlace de red local](#modify) de este artículo.</span><span class="sxs-lookup"><span data-stu-id="7444e-163">See the [Modify IP address prefixes for a local network gateway](#modify) section of this article.</span></span>

## <span data-ttu-id="7444e-164"><a name="PublicIP"></a>4. Solicite una dirección IP pública</span><span class="sxs-lookup"><span data-stu-id="7444e-164"><a name="PublicIP"></a>4. Request a Public IP address</span></span>

<span data-ttu-id="7444e-165">Una puerta de enlace VPN debe tener una dirección IP pública.</span><span class="sxs-lookup"><span data-stu-id="7444e-165">A VPN gateway must have a Public IP address.</span></span> <span data-ttu-id="7444e-166">Primero se solicita el recurso de la dirección IP y, después, se hace referencia a él al crear la puerta de enlace de red virtual.</span><span class="sxs-lookup"><span data-stu-id="7444e-166">You first request the IP address resource, and then refer to it when creating your virtual network gateway.</span></span> <span data-ttu-id="7444e-167">La dirección IP se asigna dinámicamente al recurso cuando se crea la puerta de enlace VPN.</span><span class="sxs-lookup"><span data-stu-id="7444e-167">The IP address is dynamically assigned to the resource when the VPN gateway is created.</span></span> <span data-ttu-id="7444e-168">Actualmente, VPN Gateway solo admite la asignación de direcciones IP públicas *dinámicas*.</span><span class="sxs-lookup"><span data-stu-id="7444e-168">VPN Gateway currently only supports *Dynamic* Public IP address allocation.</span></span> <span data-ttu-id="7444e-169">No se puede solicitar una asignación de direcciones IP públicas estáticas.</span><span class="sxs-lookup"><span data-stu-id="7444e-169">You cannot request a Static Public IP address assignment.</span></span> <span data-ttu-id="7444e-170">Sin embargo, esto no significa que la dirección IP cambia después de que se ha asignado a una puerta de enlace VPN.</span><span class="sxs-lookup"><span data-stu-id="7444e-170">However, this does not mean that the IP address changes after it has been assigned to your VPN gateway.</span></span> <span data-ttu-id="7444e-171">La única vez que la dirección IP pública cambia es cuando la puerta de enlace se elimina y se vuelve a crear.</span><span class="sxs-lookup"><span data-stu-id="7444e-171">The only time the Public IP address changes is when the gateway is deleted and re-created.</span></span> <span data-ttu-id="7444e-172">No cambia cuando se cambia el tamaño, se restablece o se realizan actualizaciones u otras operaciones de mantenimiento interno de una puerta de enlace VPN.</span><span class="sxs-lookup"><span data-stu-id="7444e-172">It doesn't change across resizing, resetting, or other internal maintenance/upgrades of your VPN gateway.</span></span>

<span data-ttu-id="7444e-173">Solicite una dirección IP pública que se asignará a la puerta de enlace VPN de la red virtual.</span><span class="sxs-lookup"><span data-stu-id="7444e-173">Request a Public IP address that will be assigned to your virtual network VPN gateway.</span></span>

```powershell
$gwpip= New-AzureRmPublicIpAddress -Name gwpip -ResourceGroupName TestRG1 -Location 'East US' -AllocationMethod Dynamic
```

## <span data-ttu-id="7444e-174"><a name="GatewayIPConfig"></a>5. Creación de la configuración de direccionamiento IP de la puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="7444e-174"><a name="GatewayIPConfig"></a>5. Create the gateway IP addressing configuration</span></span>

<span data-ttu-id="7444e-175">La configuración de puerta de enlace define la subred y la dirección IP pública.</span><span class="sxs-lookup"><span data-stu-id="7444e-175">The gateway configuration defines the subnet and the public IP address to use.</span></span> <span data-ttu-id="7444e-176">Use el ejemplo siguiente para crear la configuración de la puerta de enlace:</span><span class="sxs-lookup"><span data-stu-id="7444e-176">Use the following example to create your gateway configuration:</span></span>

```powershell
$vnet = Get-AzureRmVirtualNetwork -Name TestVNet1 -ResourceGroupName TestRG1
$subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -VirtualNetwork $vnet
$gwipconfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name gwipconfig1 -SubnetId $subnet.Id -PublicIpAddressId $gwpip.Id
```

## <span data-ttu-id="7444e-177"><a name="CreateGateway"></a>6. Creación de la puerta de enlace VPN</span><span class="sxs-lookup"><span data-stu-id="7444e-177"><a name="CreateGateway"></a>6. Create the VPN gateway</span></span>

<span data-ttu-id="7444e-178">Cree la puerta de enlace VPN de la red virtual.</span><span class="sxs-lookup"><span data-stu-id="7444e-178">Create the virtual network VPN gateway.</span></span> <span data-ttu-id="7444e-179">Crear una puerta de enlace VPN puede tardar 45 minutos o más en completarse.</span><span class="sxs-lookup"><span data-stu-id="7444e-179">Creating a VPN gateway can take up to 45 minutes or more to complete.</span></span>

<span data-ttu-id="7444e-180">Use los valores siguientes:</span><span class="sxs-lookup"><span data-stu-id="7444e-180">Use the following values:</span></span>

* <span data-ttu-id="7444e-181">El valor *-GatewayType* para una configuración de sitio a sitio es *Vpn*.</span><span class="sxs-lookup"><span data-stu-id="7444e-181">The *-GatewayType* for a Site-to-Site configuration is *Vpn*.</span></span> <span data-ttu-id="7444e-182">El tipo de puerta de enlace siempre es específico de la configuración que se va a implementar.</span><span class="sxs-lookup"><span data-stu-id="7444e-182">The gateway type is always specific to the configuration that you are implementing.</span></span> <span data-ttu-id="7444e-183">Por ejemplo, otras configuraciones de puerta de enlace pueden requerir GatewayType ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="7444e-183">For example, other gateway configurations may require -GatewayType ExpressRoute.</span></span>
* <span data-ttu-id="7444e-184">El valor de *-VpnType* puede ser *RouteBased* (la llamada puerta de enlace dinámica en algunos documentos) o *PolicyBased* (la llamada puerta de enlace estática en algunos documentos).</span><span class="sxs-lookup"><span data-stu-id="7444e-184">The *-VpnType* can be *RouteBased* (referred to as a Dynamic Gateway in some documentation), or *PolicyBased* (referred to as a Static Gateway in some documentation).</span></span> <span data-ttu-id="7444e-185">Para más información sobre los tipos de Puertas de enlace de VPN, consulte [Información acerca de VPN Gateway](vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="7444e-185">For more information about VPN gateway types, see [About VPN Gateway](vpn-gateway-about-vpngateways.md).</span></span>
* <span data-ttu-id="7444e-186">Seleccione la SKU de la puerta de enlace que desea utilizar.</span><span class="sxs-lookup"><span data-stu-id="7444e-186">Select the Gateway SKU that you want to use.</span></span> <span data-ttu-id="7444e-187">Hay limitaciones de configuración para determinadas SKU.</span><span class="sxs-lookup"><span data-stu-id="7444e-187">There are configuration limitations for certain SKUs.</span></span> <span data-ttu-id="7444e-188">Consulte [SKU de puertas de enlace](vpn-gateway-about-vpn-gateway-settings.md#gwsku) para más información.</span><span class="sxs-lookup"><span data-stu-id="7444e-188">For more information, see [Gateway SKUs](vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span></span> <span data-ttu-id="7444e-189">Si se produce un error al crear la puerta de enlace VPN con respecto a - GatewaySku, compruebe que tiene instalada la versión más reciente de los cmdlets de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7444e-189">If you get an error when creating the VPN gateway regarding the -GatewaySku, verify that you have installed the latest version of the PowerShell cmdlets.</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name VNet1GW -ResourceGroupName TestRG1 `
-Location 'East US' -IpConfigurations $gwipconfig -GatewayType Vpn `
-VpnType RouteBased -GatewaySku VpnGw1
```

## <span data-ttu-id="7444e-190"><a name="ConfigureVPNDevice"></a>7. Configurar el dispositivo VPN</span><span class="sxs-lookup"><span data-stu-id="7444e-190"><a name="ConfigureVPNDevice"></a>7. Configure your VPN device</span></span>

<span data-ttu-id="7444e-191">Las conexiones de sitio a sitio a una red local requieren un dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="7444e-191">Site-to-Site connections to an on-premises network require a VPN device.</span></span> <span data-ttu-id="7444e-192">En este paso, se configura el dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="7444e-192">In this step, you configure your VPN device.</span></span> <span data-ttu-id="7444e-193">Al configurar el dispositivo VPN, necesita lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="7444e-193">When configuring your VPN device, you need the following:</span></span>

- <span data-ttu-id="7444e-194">Una clave compartida.</span><span class="sxs-lookup"><span data-stu-id="7444e-194">A shared key.</span></span> <span data-ttu-id="7444e-195">Se trata de la misma clave compartida que se especifica al crear la conexión VPN de sitio a sitio.</span><span class="sxs-lookup"><span data-stu-id="7444e-195">This is the same shared key that you specify when creating your Site-to-Site VPN connection.</span></span> <span data-ttu-id="7444e-196">En estos ejemplos se utiliza una clave compartida básica.</span><span class="sxs-lookup"><span data-stu-id="7444e-196">In our examples, we use a basic shared key.</span></span> <span data-ttu-id="7444e-197">Se recomienda que genere y utilice una clave más compleja.</span><span class="sxs-lookup"><span data-stu-id="7444e-197">We recommend that you generate a more complex key to use.</span></span>
- <span data-ttu-id="7444e-198">La dirección IP pública de la puerta de enlace de red virtual.</span><span class="sxs-lookup"><span data-stu-id="7444e-198">The Public IP address of your virtual network gateway.</span></span> <span data-ttu-id="7444e-199">Puede ver la dirección IP pública mediante Azure Portal, PowerShell o la CLI.</span><span class="sxs-lookup"><span data-stu-id="7444e-199">You can view the public IP address by using the Azure portal, PowerShell, or CLI.</span></span> <span data-ttu-id="7444e-200">Para buscar la dirección IP pública de la puerta de enlace de red virtual con PowerShell, utilice el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="7444e-200">To find the Public IP address of your virtual network gateway using PowerShell, use the following example:</span></span>

  ```powershell
  Get-AzureRmPublicIpAddress -Name GW1PublicIP -ResourceGroupName TestRG1
  ```

[!INCLUDE [Configure VPN device](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]


## <span data-ttu-id="7444e-201"><a name="CreateConnection"></a>8. Creación de la conexión VPN</span><span class="sxs-lookup"><span data-stu-id="7444e-201"><a name="CreateConnection"></a>8. Create the VPN connection</span></span>

<span data-ttu-id="7444e-202">Ahora va a crear la conexión VPN de sitio a sitio entre la puerta de enlace de red virtual y el dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="7444e-202">Next, create the Site-to-Site VPN connection between your virtual network gateway and your VPN device.</span></span> <span data-ttu-id="7444e-203">Asegúrese de reemplazar los valores por los suyos.</span><span class="sxs-lookup"><span data-stu-id="7444e-203">Be sure to replace the values with your own.</span></span> <span data-ttu-id="7444e-204">La clave compartida debe coincidir con el valor usado para la configuración del dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="7444e-204">The shared key must match the value you used for your VPN device configuration.</span></span> <span data-ttu-id="7444e-205">Tenga en cuenta que el valor de '-ConnectionType' para la configuración sitio a sitio es *IPsec*.</span><span class="sxs-lookup"><span data-stu-id="7444e-205">Notice that the '-ConnectionType' for Site-to-Site is *IPsec*.</span></span>

1. <span data-ttu-id="7444e-206">Establezca las variables.</span><span class="sxs-lookup"><span data-stu-id="7444e-206">Set the variables.</span></span>
  ```powershell
  $gateway1 = Get-AzureRmVirtualNetworkGateway -Name VNet1GW -ResourceGroupName TestRG1
  $local = Get-AzureRmLocalNetworkGateway -Name Site2 -ResourceGroupName TestRG1
  ```

2. <span data-ttu-id="7444e-207">Cree la conexión.</span><span class="sxs-lookup"><span data-stu-id="7444e-207">Create the connection.</span></span>
  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name VNet1toSite2 -ResourceGroupName TestRG1 `
  -Location 'East US' -VirtualNetworkGateway1 $gateway1 -LocalNetworkGateway2 $local `
  -ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
  ```

<span data-ttu-id="7444e-208">Pasado un momento, se establecerá la conexión.</span><span class="sxs-lookup"><span data-stu-id="7444e-208">After a short while, the connection will be established.</span></span>

## <span data-ttu-id="7444e-209"><a name="toverify"></a>9. Comprobación de la conexión VPN</span><span class="sxs-lookup"><span data-stu-id="7444e-209"><a name="toverify"></a>9. Verify the VPN connection</span></span>

<span data-ttu-id="7444e-210">Hay varias maneras diferentes de comprobar la conexión VPN.</span><span class="sxs-lookup"><span data-stu-id="7444e-210">There are a few different ways to verify your VPN connection.</span></span>

[!INCLUDE [Verify connection](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <span data-ttu-id="7444e-211"><a name="connectVM"></a>Conexión a una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="7444e-211"><a name="connectVM"></a>To connect to a virtual machine</span></span>

[!INCLUDE [Connect to a VM](../../includes/vpn-gateway-connect-vm-s2s-include.md)]


## <span data-ttu-id="7444e-212"><a name="modify"></a>Modificación de los prefijos las direcciones IP de una puerta de enlace de red local</span><span class="sxs-lookup"><span data-stu-id="7444e-212"><a name="modify"></a>Modify IP address prefixes for a local network gateway</span></span>

<span data-ttu-id="7444e-213">Si cambian los prefijos de las direcciones IP que desea enrutar a una ubicación local, puede modificar la puerta de enlace de red local.</span><span class="sxs-lookup"><span data-stu-id="7444e-213">If the IP address prefixes that you want routed to your on-premises location change, you can modify the local network gateway.</span></span> <span data-ttu-id="7444e-214">Se proporcionan dos conjuntos de instrucciones:</span><span class="sxs-lookup"><span data-stu-id="7444e-214">Two sets of instructions are provided.</span></span> <span data-ttu-id="7444e-215">Las instrucciones que elija dependen de si ya se ha creado la conexión de la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="7444e-215">The instructions you choose depend on whether you have already created your gateway connection.</span></span>

[!INCLUDE [Modify prefixes](../../includes/vpn-gateway-modify-ip-prefix-rm-include.md)]

## <span data-ttu-id="7444e-216"><a name="modifygwipaddress"></a>Modificación de la dirección IP de una puerta de enlace de red local</span><span class="sxs-lookup"><span data-stu-id="7444e-216"><a name="modifygwipaddress"></a>Modify the gateway IP address for a local network gateway</span></span>

[!INCLUDE [Modify gateway IP address](../../includes/vpn-gateway-modify-lng-gateway-ip-rm-include.md)]

## <a name="next-steps"></a><span data-ttu-id="7444e-217">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7444e-217">Next steps</span></span>

*  <span data-ttu-id="7444e-218">Una vez completada la conexión, puede agregar máquinas virtuales a las redes virtuales.</span><span class="sxs-lookup"><span data-stu-id="7444e-218">Once your connection is complete, you can add virtual machines to your virtual networks.</span></span> <span data-ttu-id="7444e-219">Consulte [Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute) para más información.</span><span class="sxs-lookup"><span data-stu-id="7444e-219">For more information, see [Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span></span>
* <span data-ttu-id="7444e-220">Para más información acerca de BGP, consulte [Información general de BGP](vpn-gateway-bgp-overview.md) y [Configuración de BGP](vpn-gateway-bgp-resource-manager-ps.md).</span><span class="sxs-lookup"><span data-stu-id="7444e-220">For information about BGP, see the [BGP Overview](vpn-gateway-bgp-overview.md) and [How to configure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span></span>
