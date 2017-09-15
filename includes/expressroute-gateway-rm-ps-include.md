<span data-ttu-id="a3f3c-101">Los pasos de esta tarea usan una red virtual que se basa en los valores de la siguiente lista de referencia de configuración.</span><span class="sxs-lookup"><span data-stu-id="a3f3c-101">The steps for this task use a VNet based on the values in the following configuration reference list.</span></span> <span data-ttu-id="a3f3c-102">En esta lista también se enumeran nombres y valores de configuración adicionales.</span><span class="sxs-lookup"><span data-stu-id="a3f3c-102">Additional settings and names are also outlined in this list.</span></span> <span data-ttu-id="a3f3c-103">No se utiliza esta lista directamente en ninguno de los pasos, aunque se agregan variables basadas en los valores que aparecen en ella.</span><span class="sxs-lookup"><span data-stu-id="a3f3c-103">We don't use this list directly in any of the steps, although we do add variables based on the values in this list.</span></span> <span data-ttu-id="a3f3c-104">Puede copiar la lista para utilizarla como referencia y reemplazar los valores por los suyos propios.</span><span class="sxs-lookup"><span data-stu-id="a3f3c-104">You can copy the list to use as a reference, replacing the values with your own.</span></span>

<span data-ttu-id="a3f3c-105">**Lista de referencia de configuración**</span><span class="sxs-lookup"><span data-stu-id="a3f3c-105">**Configuration reference list**</span></span>

* <span data-ttu-id="a3f3c-106">Nombre de red virtual = "TestVNet"</span><span class="sxs-lookup"><span data-stu-id="a3f3c-106">Virtual Network Name = "TestVNet"</span></span>
* <span data-ttu-id="a3f3c-107">Espacio de direcciones de red virtual = 192.168.0.0/16</span><span class="sxs-lookup"><span data-stu-id="a3f3c-107">Virtual Network address space = 192.168.0.0/16</span></span>
* <span data-ttu-id="a3f3c-108">Grupo de recursos: "TestRG"</span><span class="sxs-lookup"><span data-stu-id="a3f3c-108">Resource Group = "TestRG"</span></span>
* <span data-ttu-id="a3f3c-109">Nombre de subred 1 = "FrontEnd"</span><span class="sxs-lookup"><span data-stu-id="a3f3c-109">Subnet1 Name = "FrontEnd"</span></span> 
* <span data-ttu-id="a3f3c-110">Espacio de direcciones de subred 1 = "192.168.1.0/24"</span><span class="sxs-lookup"><span data-stu-id="a3f3c-110">Subnet1 address space = "192.168.1.0/24"</span></span>
* <span data-ttu-id="a3f3c-111">Nombre de subred de puerta de enlace: "GatewaySubnet" (siempre debe asignar a las subredes de puerta de enlace el nombre *GatewaySubnet*).</span><span class="sxs-lookup"><span data-stu-id="a3f3c-111">Gateway Subnet name: "GatewaySubnet" You must always name a gateway subnet *GatewaySubnet*.</span></span>
* <span data-ttu-id="a3f3c-112">Espacio de direcciones de subred de puerta de enlace = "192.168.200.0/26"</span><span class="sxs-lookup"><span data-stu-id="a3f3c-112">Gateway Subnet address space = "192.168.200.0/26"</span></span>
* <span data-ttu-id="a3f3c-113">Región = "East US"</span><span class="sxs-lookup"><span data-stu-id="a3f3c-113">Region = "East US"</span></span>
* <span data-ttu-id="a3f3c-114">Nombre de puerta de enlace = "GW"</span><span class="sxs-lookup"><span data-stu-id="a3f3c-114">Gateway Name = "GW"</span></span>
* <span data-ttu-id="a3f3c-115">Nombre de IP de puerta de enlace = "GWIP"</span><span class="sxs-lookup"><span data-stu-id="a3f3c-115">Gateway IP Name = "GWIP"</span></span>
* <span data-ttu-id="a3f3c-116">Nombre de configuración de IP de puerta de enlace = "gwipconf"</span><span class="sxs-lookup"><span data-stu-id="a3f3c-116">Gateway IP configuration Name = "gwipconf"</span></span>
* <span data-ttu-id="a3f3c-117">Tipo = "ExpressRoute" (este tipo es obligatorio para una configuración de ExpressRoute).</span><span class="sxs-lookup"><span data-stu-id="a3f3c-117">Type = "ExpressRoute" This type is required for an ExpressRoute configuration.</span></span>
* <span data-ttu-id="a3f3c-118">Nombre de IP pública de puerta de enlace = "gwpip"</span><span class="sxs-lookup"><span data-stu-id="a3f3c-118">Gateway Public IP Name = "gwpip"</span></span>

## <a name="add-a-gateway"></a><span data-ttu-id="a3f3c-119">Adición de una puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="a3f3c-119">Add a gateway</span></span>
1. <span data-ttu-id="a3f3c-120">Conéctese a su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="a3f3c-120">Connect to your Azure Subscription.</span></span>

  ```powershell 
  Login-AzureRmAccount
  Get-AzureRmSubscription 
  Select-AzureRmSubscription -SubscriptionName "Name of subscription"
  ```
2. <span data-ttu-id="a3f3c-121">Declare las variables para este ejercicio.</span><span class="sxs-lookup"><span data-stu-id="a3f3c-121">Declare your variables for this exercise.</span></span> <span data-ttu-id="a3f3c-122">No olvide editar el ejemplo para reflejar la configuración que desea utilizar.</span><span class="sxs-lookup"><span data-stu-id="a3f3c-122">Be sure to edit the sample to reflect the settings that you want to use.</span></span>

  ```powershell 
  $RG = "TestRG"
  $Location = "East US"
  $GWName = "GW"
  $GWIPName = "GWIP"
  $GWIPconfName = "gwipconf"
  $VNetName = "TestVNet"
  ```
3. <span data-ttu-id="a3f3c-123">Almacene el objeto de red virtual como una variable.</span><span class="sxs-lookup"><span data-stu-id="a3f3c-123">Store the virtual network object as a variable.</span></span>

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG
  ```
4. <span data-ttu-id="a3f3c-124">Agregue una subred de puerta de enlace a su red virtual.</span><span class="sxs-lookup"><span data-stu-id="a3f3c-124">Add a gateway subnet to your Virtual Network.</span></span> <span data-ttu-id="a3f3c-125">A la subred de puerta de enlace debe asignarle el nombre "GatewaySubnet".</span><span class="sxs-lookup"><span data-stu-id="a3f3c-125">The gateway subnet must be named "GatewaySubnet".</span></span> <span data-ttu-id="a3f3c-126">Se recomienda que cree una subred de puerta de enlace con un valor /27 o mayor (/26, /25, etc.).</span><span class="sxs-lookup"><span data-stu-id="a3f3c-126">You should create a gateway subnet that is /27 or larger (/26, /25, etc.).</span></span>

  ```powershell
  Add-AzureRmVirtualNetworkSubnetConfig -Name GatewaySubnet -VirtualNetwork $vnet -AddressPrefix 192.168.200.0/26
  ```
5. <span data-ttu-id="a3f3c-127">Establezca la configuración.</span><span class="sxs-lookup"><span data-stu-id="a3f3c-127">Set the configuration.</span></span>

  ```powershell
  Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
6. <span data-ttu-id="a3f3c-128">Almacene la subred de puerta de enlace como una variable.</span><span class="sxs-lookup"><span data-stu-id="a3f3c-128">Store the gateway subnet as a variable.</span></span>

  ```powershell
  $subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -VirtualNetwork $vnet
  ```
7. <span data-ttu-id="a3f3c-129">Pida una dirección IP pública.</span><span class="sxs-lookup"><span data-stu-id="a3f3c-129">Request a public IP address.</span></span> <span data-ttu-id="a3f3c-130">La dirección IP se solicita antes de crear la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="a3f3c-130">The IP address is requested before creating the gateway.</span></span> <span data-ttu-id="a3f3c-131">No puede especificar la dirección IP que desea usar; se asigna una dinámicamente.</span><span class="sxs-lookup"><span data-stu-id="a3f3c-131">You cannot specify the IP address that you want to use; it’s dynamically allocated.</span></span> <span data-ttu-id="a3f3c-132">Utilizará esta dirección IP en la siguiente sección de configuración.</span><span class="sxs-lookup"><span data-stu-id="a3f3c-132">You'll use this IP address in the next configuration section.</span></span> <span data-ttu-id="a3f3c-133">El valor de AllocationMethod debe ser Dynamic.</span><span class="sxs-lookup"><span data-stu-id="a3f3c-133">The AllocationMethod must be Dynamic.</span></span>

  ```powershell
  $pip = New-AzureRmPublicIpAddress -Name $GWIPName  -ResourceGroupName $RG -Location $Location -AllocationMethod Dynamic
  ```
8. <span data-ttu-id="a3f3c-134">Cree la configuración para su puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="a3f3c-134">Create the configuration for your gateway.</span></span> <span data-ttu-id="a3f3c-135">La configuración de puerta de enlace define la subred y la dirección IP pública.</span><span class="sxs-lookup"><span data-stu-id="a3f3c-135">The gateway configuration defines the subnet and the public IP address to use.</span></span> <span data-ttu-id="a3f3c-136">En este paso, se especifica la configuración que se utilizará al crear la puerta de enlace,</span><span class="sxs-lookup"><span data-stu-id="a3f3c-136">In this step, you are specifying the configuration that will be used when you create the gateway.</span></span> <span data-ttu-id="a3f3c-137">pero no se crea realmente el objeto de puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="a3f3c-137">This step does not actually create the gateway object.</span></span> <span data-ttu-id="a3f3c-138">Use el ejemplo siguiente para crear la configuración de la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="a3f3c-138">Use the sample below to create your gateway configuration.</span></span>

  ```powershell
  $ipconf = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName -Subnet $subnet -PublicIpAddress $pip
  ```
9. <span data-ttu-id="a3f3c-139">Cree la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="a3f3c-139">Create the gateway.</span></span> <span data-ttu-id="a3f3c-140">En este paso, el elemento **-GatewayType** resulta especialmente importante.</span><span class="sxs-lookup"><span data-stu-id="a3f3c-140">In this step, the **-GatewayType** is especially important.</span></span> <span data-ttu-id="a3f3c-141">Debe utilizar el valor **ExpressRoute**.</span><span class="sxs-lookup"><span data-stu-id="a3f3c-141">You must use the value **ExpressRoute**.</span></span> <span data-ttu-id="a3f3c-142">Después de ejecutar estos cmdlets, la puerta de enlace puede tardar 45 minutos o más en crearse.</span><span class="sxs-lookup"><span data-stu-id="a3f3c-142">After running these cmdlets, the gateway can take 45 minutes or more to create.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG -Location $Location -IpConfigurations $ipconf -GatewayType Expressroute -GatewaySku Standard
  ```

## <a name="verify-the-gateway-was-created"></a><span data-ttu-id="a3f3c-143">Comprobación de la creación de la puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="a3f3c-143">Verify the gateway was created</span></span>
<span data-ttu-id="a3f3c-144">Utilice los siguientes comandos para comprobar si se ha creado la puerta de enlace:</span><span class="sxs-lookup"><span data-stu-id="a3f3c-144">Use the following commands to verify that the gateway has been created:</span></span>

```powershell
Get-AzureRmVirtualNetworkGateway -ResourceGroupName $RG
```

## <a name="resize-a-gateway"></a><span data-ttu-id="a3f3c-145">Cambio del tamaño de una puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="a3f3c-145">Resize a gateway</span></span>
<span data-ttu-id="a3f3c-146">Hay varias [SKU de puerta de enlace](../articles/expressroute/expressroute-about-virtual-network-gateways.md).</span><span class="sxs-lookup"><span data-stu-id="a3f3c-146">There are a number of [Gateway SKUs](../articles/expressroute/expressroute-about-virtual-network-gateways.md).</span></span> <span data-ttu-id="a3f3c-147">Puede utilizar el siguiente comando para cambiar en cualquier momento la SKU de puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="a3f3c-147">You can use the following command to change the Gateway SKU at any time.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a3f3c-148">Este comando no funciona para la puerta de enlace de UltraPerformance.</span><span class="sxs-lookup"><span data-stu-id="a3f3c-148">This command doesn't work for UltraPerformance gateway.</span></span> <span data-ttu-id="a3f3c-149">Para cambiar la puerta de enlace a una puerta de enlace de UltraPerformance, quite primero la puerta de enlace de ExpressRoute existente y, después, cree una nueva puerta de enlace de UltraPerformance.</span><span class="sxs-lookup"><span data-stu-id="a3f3c-149">To change your gateway to an UltraPerformance gateway, first remove the existing ExpressRoute gateway, and then create a new UltraPerformance gateway.</span></span> <span data-ttu-id="a3f3c-150">Para degradar la puerta de enlace desde una puerta de enlace de UltraPerformance, quite primero la puerta de enlace de UltraPerformance existente y, después, cree una nueva puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="a3f3c-150">To downgrade your gateway from an UltraPerformance gateway, first remove the UltraPerformance gateway, and then create a new gateway.</span></span>
> 
> 

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
Resize-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -GatewaySku HighPerformance
```

## <a name="remove-a-gateway"></a><span data-ttu-id="a3f3c-151">Eliminación de una puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="a3f3c-151">Remove a gateway</span></span>
<span data-ttu-id="a3f3c-152">Para quitar una puerta de enlace, use el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="a3f3c-152">Use the following command to remove a gateway:</span></span>

```powershell
Remove-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
```