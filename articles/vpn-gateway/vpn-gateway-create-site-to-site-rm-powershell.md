---
title: 'Conectar su tooan de red local red virtual de Azure: VPN de sitio a sitio: PowerShell | Documentos de Microsoft'
description: "Una conexión de IPsec desde el entorno local de red tooan red virtual de Azure a través de toocreate de pasos Hola Internet pública. Estos pasos le ayudarán a crear una conexión de VPN Gateway de sitio a sitio entre locales mediante PowerShell."
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
ms.openlocfilehash: cb8db1dab3a5488816a7f7e8e63908a4c02f55db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vnet-with-a-site-to-site-vpn-connection-using-powershell"></a><span data-ttu-id="308f8-104">Creación de una red virtual con una conexión VPN de sitio a sitio mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="308f8-104">Create a VNet with a Site-to-Site VPN connection using PowerShell</span></span>

<span data-ttu-id="308f8-105">Este artículo muestra cómo toouse conexión de puerta de enlace VPN de PowerShell toocreate un sitio a sitio desde el entorno local de red toohello red virtual.</span><span class="sxs-lookup"><span data-stu-id="308f8-105">This article shows you how toouse PowerShell toocreate a Site-to-Site VPN gateway connection from your on-premises network toohello VNet.</span></span> <span data-ttu-id="308f8-106">pasos de Hello en este artículo aplican toohello modelo de implementación de administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="308f8-106">hello steps in this article apply toohello Resource Manager deployment model.</span></span> <span data-ttu-id="308f8-107">También puede crear esta configuración con una herramienta de implementación diferentes o un modelo de implementación seleccionando una opción diferente de hello lista siguiente:</span><span class="sxs-lookup"><span data-stu-id="308f8-107">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="308f8-108">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="308f8-108">Azure portal</span></span>](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="308f8-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="308f8-109">PowerShell</span></span>](vpn-gateway-create-site-to-site-rm-powershell.md)
> * [<span data-ttu-id="308f8-110">CLI</span><span class="sxs-lookup"><span data-stu-id="308f8-110">CLI</span></span>](vpn-gateway-howto-site-to-site-resource-manager-cli.md)
> * [<span data-ttu-id="308f8-111">Portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="308f8-111">Azure portal (classic)</span></span>](vpn-gateway-howto-site-to-site-classic-portal.md)
> * [<span data-ttu-id="308f8-112">Portal clásico (clásico)</span><span class="sxs-lookup"><span data-stu-id="308f8-112">Classic portal (classic)</span></span>](vpn-gateway-site-to-site-create.md)
> 
>


<span data-ttu-id="308f8-113">Una conexión de puerta de enlace VPN de sitio a sitio es tooconnect utilizado en sus instalaciones de red tooan red virtual de Azure a través de un túnel VPN de IPsec/IKE (IKEv1 o IKEv2).</span><span class="sxs-lookup"><span data-stu-id="308f8-113">A Site-to-Site VPN gateway connection is used tooconnect your on-premises network tooan Azure virtual network over an IPsec/IKE (IKEv1 or IKEv2) VPN tunnel.</span></span> <span data-ttu-id="308f8-114">Este tipo de conexión requiere una VPN dispositivo situado en local que tiene un tooit de dirección asignada de IP pública con orientación externa.</span><span class="sxs-lookup"><span data-stu-id="308f8-114">This type of connection requires a VPN device located on-premises that has an externally facing public IP address assigned tooit.</span></span> <span data-ttu-id="308f8-115">Para más información acerca de las puertas de enlace VPN, consulte [Acerca de VPN Gateway](vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="308f8-115">For more information about VPN gateways, see [About VPN gateway](vpn-gateway-about-vpngateways.md).</span></span>

![Diagrama de la conexión entre locales de VPN Gateway de sitio a sitio](./media/vpn-gateway-create-site-to-site-rm-powershell/site-to-site-diagram.png)

## <span data-ttu-id="308f8-117"><a name="before"></a>Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="308f8-117"><a name="before"></a>Before you begin</span></span>

<span data-ttu-id="308f8-118">Compruebe que se ha cumplido hello siguiendo criterios antes de comenzar la configuración:</span><span class="sxs-lookup"><span data-stu-id="308f8-118">Verify that you have met hello following criteria before beginning your configuration:</span></span>

* <span data-ttu-id="308f8-119">Asegúrese de que tiene un dispositivo VPN compatible y alguna persona tooconfigure capaz de él.</span><span class="sxs-lookup"><span data-stu-id="308f8-119">Make sure you have a compatible VPN device and someone who is able tooconfigure it.</span></span> <span data-ttu-id="308f8-120">Para más información acerca de los dispositivos VPN compatibles y su configuración, consulte [Acerca de los dispositivos VPN](vpn-gateway-about-vpn-devices.md).</span><span class="sxs-lookup"><span data-stu-id="308f8-120">For more information about compatible VPN devices and device configuration, see [About VPN Devices](vpn-gateway-about-vpn-devices.md).</span></span>
* <span data-ttu-id="308f8-121">Compruebe que tiene una dirección IPv4 pública externa para el dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="308f8-121">Verify that you have an externally facing public IPv4 address for your VPN device.</span></span> <span data-ttu-id="308f8-122">Esta dirección IP no puede estar detrás de un NAT.</span><span class="sxs-lookup"><span data-stu-id="308f8-122">This IP address cannot be located behind a NAT.</span></span>
* <span data-ttu-id="308f8-123">Si no está familiarizado con intervalos de direcciones IP de hello ubicados en configuración de red local, deberá toocoordinate con alguien que pueda proporcionarle estos detalles para usted.</span><span class="sxs-lookup"><span data-stu-id="308f8-123">If you are unfamiliar with hello IP address ranges located in your on-premises network configuration, you need toocoordinate with someone who can provide those details for you.</span></span> <span data-ttu-id="308f8-124">Al crear esta configuración, debe especificar prefijos para intervalo de direcciones IP con hello que Azure enrutará la ubicación de tooyour local.</span><span class="sxs-lookup"><span data-stu-id="308f8-124">When you create this configuration, you must specify hello IP address range prefixes that Azure will route tooyour on-premises location.</span></span> <span data-ttu-id="308f8-125">Ninguna de las subredes de saludo de la red local puede enumerar sobre el regazo con subredes de red virtual de Hola que desee tooconnect a.</span><span class="sxs-lookup"><span data-stu-id="308f8-125">None of hello subnets of your on-premises network can over lap with hello virtual network subnets that you want tooconnect to.</span></span>
* <span data-ttu-id="308f8-126">Instalar versión más reciente de Hola de hello cmdlets de PowerShell del Administrador de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="308f8-126">Install hello latest version of hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="308f8-127">Cmdlets de PowerShell se actualizan con frecuencia y, normalmente deberá tooupdate su funcionalidad característica más reciente de Hola de PowerShell cmdlets tooget.</span><span class="sxs-lookup"><span data-stu-id="308f8-127">PowerShell cmdlets are updated frequently and you will typically need tooupdate your PowerShell cmdlets tooget hello latest feature functionality.</span></span> <span data-ttu-id="308f8-128">Si no actualiza los cmdlets de PowerShell, pueden producir un error en los valores de hello especificados.</span><span class="sxs-lookup"><span data-stu-id="308f8-128">If you don't update your PowerShell cmdlets, hello values specified may fail.</span></span> <span data-ttu-id="308f8-129">Vea [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview) para obtener más información sobre cómo descargar e instalar los cmdlets de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="308f8-129">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for more information about downloading and installing PowerShell cmdlets.</span></span>

### <span data-ttu-id="308f8-130"><a name="example"></a>Valores del ejemplo</span><span class="sxs-lookup"><span data-stu-id="308f8-130"><a name="example"></a>Example values</span></span>

<span data-ttu-id="308f8-131">ejemplos de Hello en este artículo utiliza Hola después de valores.</span><span class="sxs-lookup"><span data-stu-id="308f8-131">hello examples in this article use hello following values.</span></span> <span data-ttu-id="308f8-132">Puede usar estos toocreate valores un entorno de prueba, o consulte toothem toobetter comprender los ejemplos de hello en este artículo.</span><span class="sxs-lookup"><span data-stu-id="308f8-132">You can use these values toocreate a test environment, or refer toothem toobetter understand hello examples in this article.</span></span>

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


## <span data-ttu-id="308f8-133"><a name="Login"></a>1. Conectar tooyour suscripción</span><span class="sxs-lookup"><span data-stu-id="308f8-133"><a name="Login"></a>1. Connect tooyour subscription</span></span>

[!INCLUDE [PowerShell login](../../includes/vpn-gateway-ps-login-include.md)]

## <span data-ttu-id="308f8-134"><a name="VNet"></a>2. Creación de una red virtual y una puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="308f8-134"><a name="VNet"></a>2. Create a virtual network and a gateway subnet</span></span>

<span data-ttu-id="308f8-135">Si no tiene una red virtual, créela.</span><span class="sxs-lookup"><span data-stu-id="308f8-135">If you don't already have a virtual network, create one.</span></span> <span data-ttu-id="308f8-136">Al crear una red virtual, asegúrese de que los espacios de direcciones de hello especificados no superponen con cualquiera de los espacios de direcciones de Hola que existen en la red local.</span><span class="sxs-lookup"><span data-stu-id="308f8-136">When creating a virtual network, make sure that hello address spaces you specify don't overlap any of hello address spaces that you have on your on-premises network.</span></span>

[!INCLUDE [About gateway subnets](../../includes/vpn-gateway-about-gwsubnet-include.md)]

[!INCLUDE [No NSG warning](../../includes/vpn-gateway-no-nsg-include.md)]

### <span data-ttu-id="308f8-137"><a name="vnet"></a>toocreate una red virtual y una subred de puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="308f8-137"><a name="vnet"></a>toocreate a virtual network and a gateway subnet</span></span>

<span data-ttu-id="308f8-138">Este ejemplo crea una red virtual y una subred de la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="308f8-138">This example creates a virtual network and a gateway subnet.</span></span> <span data-ttu-id="308f8-139">Si ya tiene una red virtual que necesita una subred de puerta de enlace para ver tooadd [tooadd una puerta de enlace subred tooa red virtual que ya ha creado](#gatewaysubnet).</span><span class="sxs-lookup"><span data-stu-id="308f8-139">If you already have a virtual network that you need tooadd a gateway subnet to, see [tooadd a gateway subnet tooa virtual network you have already created](#gatewaysubnet).</span></span>

<span data-ttu-id="308f8-140">Cree un grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="308f8-140">Create a resource group:</span></span>

```powershell
New-AzureRmResourceGroup -Name TestRG1 -Location 'East US'
```

<span data-ttu-id="308f8-141">Cree la red virtual.</span><span class="sxs-lookup"><span data-stu-id="308f8-141">Create your virtual network.</span></span>

1. <span data-ttu-id="308f8-142">Establecer variables de Hola.</span><span class="sxs-lookup"><span data-stu-id="308f8-142">Set hello variables.</span></span>

  ```powershell
  $subnet1 = New-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -AddressPrefix 10.11.0.0/27
  $subnet2 = New-AzureRmVirtualNetworkSubnetConfig -Name 'Subnet1' -AddressPrefix 10.11.1.0/28
  ```
2. <span data-ttu-id="308f8-143">Crear red virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="308f8-143">Create hello VNet.</span></span>

  ```powershell
  New-AzureRmVirtualNetwork -Name TestVNet1 -ResourceGroupName TestRG1 `
  -Location 'East US' -AddressPrefix 10.11.0.0/16 -Subnet $subnet1, $subnet2
  ```

### <span data-ttu-id="308f8-144"><a name="gatewaysubnet"></a>una red virtual de puerta de enlace subred tooa tooadd ya ha creado</span><span class="sxs-lookup"><span data-stu-id="308f8-144"><a name="gatewaysubnet"></a>tooadd a gateway subnet tooa virtual network you have already created</span></span>

1. <span data-ttu-id="308f8-145">Establecer variables de Hola.</span><span class="sxs-lookup"><span data-stu-id="308f8-145">Set hello variables.</span></span>

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG1 -Name TestVet1
  ```
2. <span data-ttu-id="308f8-146">Crear una subred de puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="308f8-146">Create hello gateway subnet.</span></span>

  ```powershell
  Add-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -AddressPrefix 10.11.0.0/27 -VirtualNetwork $vnet
  ```
3. <span data-ttu-id="308f8-147">Establecer configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="308f8-147">Set hello configuration.</span></span>

  ```powershell
  Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```

## <span data-ttu-id="308f8-148">3. <a name="localnet"></a>Crear puerta de enlace de red local de Hola</span><span class="sxs-lookup"><span data-stu-id="308f8-148">3. <a name="localnet"></a>Create hello local network gateway</span></span>

<span data-ttu-id="308f8-149">puerta de enlace de red local de Hello suele hacer referencia a ubicación de tooyour local.</span><span class="sxs-lookup"><span data-stu-id="308f8-149">hello local network gateway typically refers tooyour on-premises location.</span></span> <span data-ttu-id="308f8-150">Se asigne un nombre mediante el cual Azure puede consulte tooit y luego especifique la dirección IP de Hola a sitio Hola de hello local VPN dispositivo toowhich creará una conexión.</span><span class="sxs-lookup"><span data-stu-id="308f8-150">You give hello site a name by which Azure can refer tooit, then specify hello IP address of hello on-premises VPN device toowhich you will create a connection.</span></span> <span data-ttu-id="308f8-151">También especificar prefijos de direcciones IP de Hola que se enrutará a través del dispositivo VPN de toohello de puerta de enlace VPN de Hola.</span><span class="sxs-lookup"><span data-stu-id="308f8-151">You also specify hello IP address prefixes that will be routed through hello VPN gateway toohello VPN device.</span></span> <span data-ttu-id="308f8-152">Especifique los prefijos de direcciones Hola son prefijos de hello ubicados en la red local.</span><span class="sxs-lookup"><span data-stu-id="308f8-152">hello address prefixes you specify are hello prefixes located on your on-premises network.</span></span> <span data-ttu-id="308f8-153">Si cambia su red local, puede actualizar fácilmente los prefijos de Hola.</span><span class="sxs-lookup"><span data-stu-id="308f8-153">If your on-premises network changes, you can easily update hello prefixes.</span></span>

<span data-ttu-id="308f8-154">Usar hello siguientes valores:</span><span class="sxs-lookup"><span data-stu-id="308f8-154">Use hello following values:</span></span>

* <span data-ttu-id="308f8-155">Hola *GatewayIPAddress* es la dirección IP de hello de dispositivo VPN local.</span><span class="sxs-lookup"><span data-stu-id="308f8-155">hello *GatewayIPAddress* is hello IP address of your on-premises VPN device.</span></span> <span data-ttu-id="308f8-156">El dispositivo VPN no se encuentra detrás de un NAT.</span><span class="sxs-lookup"><span data-stu-id="308f8-156">Your VPN device cannot be located behind a NAT.</span></span>
* <span data-ttu-id="308f8-157">Hola *AddressPrefix* es local de espacio de direcciones.</span><span class="sxs-lookup"><span data-stu-id="308f8-157">hello *AddressPrefix* is your on-premises address space.</span></span>

<span data-ttu-id="308f8-158">tooadd una puerta de enlace de red local con un prefijo de dirección única:</span><span class="sxs-lookup"><span data-stu-id="308f8-158">tooadd a local network gateway with a single address prefix:</span></span>

  ```powershell
  New-AzureRmLocalNetworkGateway -Name Site2 -ResourceGroupName TestRG1 `
  -Location 'East US' -GatewayIpAddress '23.99.221.164' -AddressPrefix '10.0.0.0/24'
  ```

<span data-ttu-id="308f8-159">tooadd una puerta de enlace de red local con varios prefijos de direcciones:</span><span class="sxs-lookup"><span data-stu-id="308f8-159">tooadd a local network gateway with multiple address prefixes:</span></span>

  ```powershell
  New-AzureRmLocalNetworkGateway -Name Site2 -ResourceGroupName TestRG1 `
  -Location 'East US' -GatewayIpAddress '23.99.221.164' -AddressPrefix @('10.0.0.0/24','20.0.0.0/24')
  ```

<span data-ttu-id="308f8-160">toomodify prefijos de direcciones IP para la puerta de enlace de red local:</span><span class="sxs-lookup"><span data-stu-id="308f8-160">toomodify IP address prefixes for your local network gateway:</span></span><br>
<span data-ttu-id="308f8-161">A veces los prefijos de la puerta de enlace de red local cambian.</span><span class="sxs-lookup"><span data-stu-id="308f8-161">Sometimes your local network gateway prefixes change.</span></span> <span data-ttu-id="308f8-162">Hola pasos seguir toomodify su dirección IP prefijos dependen de si ha creado una conexión de puerta de enlace VPN.</span><span class="sxs-lookup"><span data-stu-id="308f8-162">hello steps you take toomodify your IP address prefixes depend on whether you have created a VPN gateway connection.</span></span> <span data-ttu-id="308f8-163">Vea hello [prefijos de direcciones IP de modificar una puerta de enlace de red local](#modify) sección de este artículo.</span><span class="sxs-lookup"><span data-stu-id="308f8-163">See hello [Modify IP address prefixes for a local network gateway](#modify) section of this article.</span></span>

## <span data-ttu-id="308f8-164"><a name="PublicIP"></a>4. Solicite una dirección IP pública</span><span class="sxs-lookup"><span data-stu-id="308f8-164"><a name="PublicIP"></a>4. Request a Public IP address</span></span>

<span data-ttu-id="308f8-165">Una puerta de enlace VPN debe tener una dirección IP pública.</span><span class="sxs-lookup"><span data-stu-id="308f8-165">A VPN gateway must have a Public IP address.</span></span> <span data-ttu-id="308f8-166">Solicitar el recurso de dirección IP hello y, a continuación, hacer referencia tooit al crear la puerta de enlace de red virtual.</span><span class="sxs-lookup"><span data-stu-id="308f8-166">You first request hello IP address resource, and then refer tooit when creating your virtual network gateway.</span></span> <span data-ttu-id="308f8-167">dirección IP de Hola se asigna dinámicamente toohello recursos cuando se crea la puerta de enlace VPN de Hola.</span><span class="sxs-lookup"><span data-stu-id="308f8-167">hello IP address is dynamically assigned toohello resource when hello VPN gateway is created.</span></span> <span data-ttu-id="308f8-168">Actualmente, VPN Gateway solo admite la asignación de direcciones IP públicas *dinámicas*.</span><span class="sxs-lookup"><span data-stu-id="308f8-168">VPN Gateway currently only supports *Dynamic* Public IP address allocation.</span></span> <span data-ttu-id="308f8-169">No se puede solicitar una asignación de direcciones IP públicas estáticas.</span><span class="sxs-lookup"><span data-stu-id="308f8-169">You cannot request a Static Public IP address assignment.</span></span> <span data-ttu-id="308f8-170">Sin embargo, esto no significa que se cambia la dirección IP de hello después de que se le ha asignado tooyour puerta de enlace VPN.</span><span class="sxs-lookup"><span data-stu-id="308f8-170">However, this does not mean that hello IP address changes after it has been assigned tooyour VPN gateway.</span></span> <span data-ttu-id="308f8-171">cambios en la dirección IP pública hello cuando se Hola puerta de enlace de única vez de Hola se elimina y vuelve a crear.</span><span class="sxs-lookup"><span data-stu-id="308f8-171">hello only time hello Public IP address changes is when hello gateway is deleted and re-created.</span></span> <span data-ttu-id="308f8-172">No cambia cuando se cambia el tamaño, se restablece o se realizan actualizaciones u otras operaciones de mantenimiento interno de una puerta de enlace VPN.</span><span class="sxs-lookup"><span data-stu-id="308f8-172">It doesn't change across resizing, resetting, or other internal maintenance/upgrades of your VPN gateway.</span></span>

<span data-ttu-id="308f8-173">Solicitar una dirección IP pública que se va a asignar la red virtual de tooyour puerta de enlace VPN.</span><span class="sxs-lookup"><span data-stu-id="308f8-173">Request a Public IP address that will be assigned tooyour virtual network VPN gateway.</span></span>

```powershell
$gwpip= New-AzureRmPublicIpAddress -Name gwpip -ResourceGroupName TestRG1 -Location 'East US' -AllocationMethod Dynamic
```

## <span data-ttu-id="308f8-174"><a name="GatewayIPConfig"></a>5. Crear configuración de direcciones IP de puerta de enlace de Hola</span><span class="sxs-lookup"><span data-stu-id="308f8-174"><a name="GatewayIPConfig"></a>5. Create hello gateway IP addressing configuration</span></span>

<span data-ttu-id="308f8-175">configuración de puerta de enlace de Hello define la subred de Hola y Hola toouse de dirección IP pública.</span><span class="sxs-lookup"><span data-stu-id="308f8-175">hello gateway configuration defines hello subnet and hello public IP address toouse.</span></span> <span data-ttu-id="308f8-176">Usar hello siguiendo el ejemplo toocreate la configuración de puerta de enlace:</span><span class="sxs-lookup"><span data-stu-id="308f8-176">Use hello following example toocreate your gateway configuration:</span></span>

```powershell
$vnet = Get-AzureRmVirtualNetwork -Name TestVNet1 -ResourceGroupName TestRG1
$subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -VirtualNetwork $vnet
$gwipconfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name gwipconfig1 -SubnetId $subnet.Id -PublicIpAddressId $gwpip.Id
```

## <span data-ttu-id="308f8-177"><a name="CreateGateway"></a>6. Crear puerta de enlace VPN de Hola</span><span class="sxs-lookup"><span data-stu-id="308f8-177"><a name="CreateGateway"></a>6. Create hello VPN gateway</span></span>

<span data-ttu-id="308f8-178">Crear puerta de enlace VPN de red virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="308f8-178">Create hello virtual network VPN gateway.</span></span> <span data-ttu-id="308f8-179">Crear una puerta de enlace VPN puede tardar hasta too45 minutos o más toocomplete.</span><span class="sxs-lookup"><span data-stu-id="308f8-179">Creating a VPN gateway can take up too45 minutes or more toocomplete.</span></span>

<span data-ttu-id="308f8-180">Usar hello siguientes valores:</span><span class="sxs-lookup"><span data-stu-id="308f8-180">Use hello following values:</span></span>

* <span data-ttu-id="308f8-181">Hola *- el GatewayType* para un sitio a sitio es configuración *Vpn*.</span><span class="sxs-lookup"><span data-stu-id="308f8-181">hello *-GatewayType* for a Site-to-Site configuration is *Vpn*.</span></span> <span data-ttu-id="308f8-182">tipo de puerta de enlace de Hello siempre es configuración toohello específico que va a implementar.</span><span class="sxs-lookup"><span data-stu-id="308f8-182">hello gateway type is always specific toohello configuration that you are implementing.</span></span> <span data-ttu-id="308f8-183">Por ejemplo, otras configuraciones de puerta de enlace pueden requerir GatewayType ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="308f8-183">For example, other gateway configurations may require -GatewayType ExpressRoute.</span></span>
* <span data-ttu-id="308f8-184">Hola *- VpnType* puede ser *RouteBased* (llamada tooas una puerta de enlace dinámico en algunos documentos), o *PolicyBased* (denominada tooas una puerta de enlace estática en algunos documentos ).</span><span class="sxs-lookup"><span data-stu-id="308f8-184">hello *-VpnType* can be *RouteBased* (referred tooas a Dynamic Gateway in some documentation), or *PolicyBased* (referred tooas a Static Gateway in some documentation).</span></span> <span data-ttu-id="308f8-185">Para más información sobre los tipos de Puertas de enlace de VPN, consulte [Información acerca de VPN Gateway](vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="308f8-185">For more information about VPN gateway types, see [About VPN Gateway](vpn-gateway-about-vpngateways.md).</span></span>
* <span data-ttu-id="308f8-186">Seleccione Hola SKU de puerta de enlace que desea toouse.</span><span class="sxs-lookup"><span data-stu-id="308f8-186">Select hello Gateway SKU that you want toouse.</span></span> <span data-ttu-id="308f8-187">Hay limitaciones de configuración para determinadas SKU.</span><span class="sxs-lookup"><span data-stu-id="308f8-187">There are configuration limitations for certain SKUs.</span></span> <span data-ttu-id="308f8-188">Consulte [SKU de puertas de enlace](vpn-gateway-about-vpn-gateway-settings.md#gwsku) para más información.</span><span class="sxs-lookup"><span data-stu-id="308f8-188">For more information, see [Gateway SKUs](vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span></span> <span data-ttu-id="308f8-189">Si se produce un error al crear la puerta de enlace VPN de hello sobre hello - GatewaySku, compruebe que ha instalado la versión más reciente de Hola Hola de cmdlets de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="308f8-189">If you get an error when creating hello VPN gateway regarding hello -GatewaySku, verify that you have installed hello latest version of hello PowerShell cmdlets.</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name VNet1GW -ResourceGroupName TestRG1 `
-Location 'East US' -IpConfigurations $gwipconfig -GatewayType Vpn `
-VpnType RouteBased -GatewaySku VpnGw1
```

## <span data-ttu-id="308f8-190"><a name="ConfigureVPNDevice"></a>7. Configurar el dispositivo VPN</span><span class="sxs-lookup"><span data-stu-id="308f8-190"><a name="ConfigureVPNDevice"></a>7. Configure your VPN device</span></span>

<span data-ttu-id="308f8-191">Red local de las conexiones de sitio a sitio tooan requieren un dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="308f8-191">Site-to-Site connections tooan on-premises network require a VPN device.</span></span> <span data-ttu-id="308f8-192">En este paso, se configura el dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="308f8-192">In this step, you configure your VPN device.</span></span> <span data-ttu-id="308f8-193">Al configurar el dispositivo VPN, necesita Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="308f8-193">When configuring your VPN device, you need hello following:</span></span>

- <span data-ttu-id="308f8-194">Una clave compartida.</span><span class="sxs-lookup"><span data-stu-id="308f8-194">A shared key.</span></span> <span data-ttu-id="308f8-195">Esto es Hola mismo compartido clave que se especifique al crear la conexión VPN de sitio a sitio.</span><span class="sxs-lookup"><span data-stu-id="308f8-195">This is hello same shared key that you specify when creating your Site-to-Site VPN connection.</span></span> <span data-ttu-id="308f8-196">En estos ejemplos se utiliza una clave compartida básica.</span><span class="sxs-lookup"><span data-stu-id="308f8-196">In our examples, we use a basic shared key.</span></span> <span data-ttu-id="308f8-197">Se recomienda que generar un toouse clave más compleja.</span><span class="sxs-lookup"><span data-stu-id="308f8-197">We recommend that you generate a more complex key toouse.</span></span>
- <span data-ttu-id="308f8-198">Hola dirección IP pública de la puerta de enlace de red virtual.</span><span class="sxs-lookup"><span data-stu-id="308f8-198">hello Public IP address of your virtual network gateway.</span></span> <span data-ttu-id="308f8-199">Puede ver la dirección IP pública hello mediante Hola portal de Azure, PowerShell o CLI.</span><span class="sxs-lookup"><span data-stu-id="308f8-199">You can view hello public IP address by using hello Azure portal, PowerShell, or CLI.</span></span> <span data-ttu-id="308f8-200">Hola toofind dirección IP pública de la puerta de enlace de red virtual con PowerShell, el siguiente ejemplo de Hola de uso:</span><span class="sxs-lookup"><span data-stu-id="308f8-200">toofind hello Public IP address of your virtual network gateway using PowerShell, use hello following example:</span></span>

  ```powershell
  Get-AzureRmPublicIpAddress -Name GW1PublicIP -ResourceGroupName TestRG1
  ```

[!INCLUDE [Configure VPN device](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]


## <span data-ttu-id="308f8-201"><a name="CreateConnection"></a>8. Crear la conexión de VPN de Hola</span><span class="sxs-lookup"><span data-stu-id="308f8-201"><a name="CreateConnection"></a>8. Create hello VPN connection</span></span>

<span data-ttu-id="308f8-202">A continuación, cree la conexión de VPN de sitio a sitio de hello entre la puerta de enlace de red virtual y el dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="308f8-202">Next, create hello Site-to-Site VPN connection between your virtual network gateway and your VPN device.</span></span> <span data-ttu-id="308f8-203">Ser seguro tooreplace Hola valores por los suyos propios.</span><span class="sxs-lookup"><span data-stu-id="308f8-203">Be sure tooreplace hello values with your own.</span></span> <span data-ttu-id="308f8-204">clave compartida de Hello debe coincidir con valor de Hola que utilizó para la configuración del dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="308f8-204">hello shared key must match hello value you used for your VPN device configuration.</span></span> <span data-ttu-id="308f8-205">Tenga en cuenta que hello '-ConnectionType' para el sitio a sitio es *IPsec*.</span><span class="sxs-lookup"><span data-stu-id="308f8-205">Notice that hello '-ConnectionType' for Site-to-Site is *IPsec*.</span></span>

1. <span data-ttu-id="308f8-206">Establecer variables de Hola.</span><span class="sxs-lookup"><span data-stu-id="308f8-206">Set hello variables.</span></span>
  ```powershell
  $gateway1 = Get-AzureRmVirtualNetworkGateway -Name VNet1GW -ResourceGroupName TestRG1
  $local = Get-AzureRmLocalNetworkGateway -Name Site2 -ResourceGroupName TestRG1
  ```

2. <span data-ttu-id="308f8-207">Crear conexiones de Hola.</span><span class="sxs-lookup"><span data-stu-id="308f8-207">Create hello connection.</span></span>
  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name VNet1toSite2 -ResourceGroupName TestRG1 `
  -Location 'East US' -VirtualNetworkGateway1 $gateway1 -LocalNetworkGateway2 $local `
  -ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
  ```

<span data-ttu-id="308f8-208">Después de un valor bajo al Hola se establecerá la conexión.</span><span class="sxs-lookup"><span data-stu-id="308f8-208">After a short while, hello connection will be established.</span></span>

## <span data-ttu-id="308f8-209"><a name="toverify"></a>9. Compruebe la conexión de VPN de Hola</span><span class="sxs-lookup"><span data-stu-id="308f8-209"><a name="toverify"></a>9. Verify hello VPN connection</span></span>

<span data-ttu-id="308f8-210">Hay unos tooverify de maneras diferentes de la conexión VPN.</span><span class="sxs-lookup"><span data-stu-id="308f8-210">There are a few different ways tooverify your VPN connection.</span></span>

[!INCLUDE [Verify connection](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <span data-ttu-id="308f8-211"><a name="connectVM"></a>máquina virtual de tooconnect tooa</span><span class="sxs-lookup"><span data-stu-id="308f8-211"><a name="connectVM"></a>tooconnect tooa virtual machine</span></span>

[!INCLUDE [Connect tooa VM](../../includes/vpn-gateway-connect-vm-s2s-include.md)]


## <span data-ttu-id="308f8-212"><a name="modify"></a>Modificación de los prefijos las direcciones IP de una puerta de enlace de red local</span><span class="sxs-lookup"><span data-stu-id="308f8-212"><a name="modify"></a>Modify IP address prefixes for a local network gateway</span></span>

<span data-ttu-id="308f8-213">Si cambian los prefijos de direcciones IP de Hola que desee enrutar tooyour ubicación, puede modificar la puerta de enlace de red local de Hola.</span><span class="sxs-lookup"><span data-stu-id="308f8-213">If hello IP address prefixes that you want routed tooyour on-premises location change, you can modify hello local network gateway.</span></span> <span data-ttu-id="308f8-214">Se proporcionan dos conjuntos de instrucciones:</span><span class="sxs-lookup"><span data-stu-id="308f8-214">Two sets of instructions are provided.</span></span> <span data-ttu-id="308f8-215">instrucciones de Hola que elija dependen de si ya ha creado la conexión de puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="308f8-215">hello instructions you choose depend on whether you have already created your gateway connection.</span></span>

[!INCLUDE [Modify prefixes](../../includes/vpn-gateway-modify-ip-prefix-rm-include.md)]

## <span data-ttu-id="308f8-216"><a name="modifygwipaddress"></a>Modificar la dirección IP de puerta de enlace de hello una puerta de enlace de red local</span><span class="sxs-lookup"><span data-stu-id="308f8-216"><a name="modifygwipaddress"></a>Modify hello gateway IP address for a local network gateway</span></span>

[!INCLUDE [Modify gateway IP address](../../includes/vpn-gateway-modify-lng-gateway-ip-rm-include.md)]

## <a name="next-steps"></a><span data-ttu-id="308f8-217">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="308f8-217">Next steps</span></span>

*  <span data-ttu-id="308f8-218">Una vez completada la conexión, puede agregar redes virtuales de máquinas virtuales tooyour.</span><span class="sxs-lookup"><span data-stu-id="308f8-218">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="308f8-219">Consulte [Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute) para más información.</span><span class="sxs-lookup"><span data-stu-id="308f8-219">For more information, see [Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span></span>
* <span data-ttu-id="308f8-220">Para obtener información sobre BGP, consulte hello [información general de BGP](vpn-gateway-bgp-overview.md) y [cómo tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span><span class="sxs-lookup"><span data-stu-id="308f8-220">For information about BGP, see hello [BGP Overview](vpn-gateway-bgp-overview.md) and [How tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span></span>
