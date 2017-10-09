<span data-ttu-id="96de2-101">pasos de Hola para esta tarea, use una red virtual basan en valores Hola Hola después de la lista de referencias de configuración.</span><span class="sxs-lookup"><span data-stu-id="96de2-101">hello steps for this task use a VNet based on hello values in hello following configuration reference list.</span></span> <span data-ttu-id="96de2-102">En esta lista también se enumeran nombres y valores de configuración adicionales.</span><span class="sxs-lookup"><span data-stu-id="96de2-102">Additional settings and names are also outlined in this list.</span></span> <span data-ttu-id="96de2-103">No usamos esta lista directamente en cualquiera de los pasos de hello, aunque se agregue variables basadas en valores de hello en esta lista.</span><span class="sxs-lookup"><span data-stu-id="96de2-103">We don't use this list directly in any of hello steps, although we do add variables based on hello values in this list.</span></span> <span data-ttu-id="96de2-104">Puede copiar hello toouse de lista como referencia, reemplazando los valores de hello con sus propios.</span><span class="sxs-lookup"><span data-stu-id="96de2-104">You can copy hello list toouse as a reference, replacing hello values with your own.</span></span>

<span data-ttu-id="96de2-105">**Lista de referencia de configuración**</span><span class="sxs-lookup"><span data-stu-id="96de2-105">**Configuration reference list**</span></span>

* <span data-ttu-id="96de2-106">Nombre de red virtual = "TestVNet"</span><span class="sxs-lookup"><span data-stu-id="96de2-106">Virtual Network Name = "TestVNet"</span></span>
* <span data-ttu-id="96de2-107">Espacio de direcciones de red virtual = 192.168.0.0/16</span><span class="sxs-lookup"><span data-stu-id="96de2-107">Virtual Network address space = 192.168.0.0/16</span></span>
* <span data-ttu-id="96de2-108">Grupo de recursos: "TestRG"</span><span class="sxs-lookup"><span data-stu-id="96de2-108">Resource Group = "TestRG"</span></span>
* <span data-ttu-id="96de2-109">Nombre de subred 1 = "FrontEnd"</span><span class="sxs-lookup"><span data-stu-id="96de2-109">Subnet1 Name = "FrontEnd"</span></span> 
* <span data-ttu-id="96de2-110">Espacio de direcciones de subred 1 = "192.168.1.0/24"</span><span class="sxs-lookup"><span data-stu-id="96de2-110">Subnet1 address space = "192.168.1.0/24"</span></span>
* <span data-ttu-id="96de2-111">Nombre de subred de puerta de enlace: "GatewaySubnet" (siempre debe asignar a las subredes de puerta de enlace el nombre *GatewaySubnet*).</span><span class="sxs-lookup"><span data-stu-id="96de2-111">Gateway Subnet name: "GatewaySubnet" You must always name a gateway subnet *GatewaySubnet*.</span></span>
* <span data-ttu-id="96de2-112">Espacio de direcciones de subred de puerta de enlace = "192.168.200.0/26"</span><span class="sxs-lookup"><span data-stu-id="96de2-112">Gateway Subnet address space = "192.168.200.0/26"</span></span>
* <span data-ttu-id="96de2-113">Región = "East US"</span><span class="sxs-lookup"><span data-stu-id="96de2-113">Region = "East US"</span></span>
* <span data-ttu-id="96de2-114">Nombre de puerta de enlace = "GW"</span><span class="sxs-lookup"><span data-stu-id="96de2-114">Gateway Name = "GW"</span></span>
* <span data-ttu-id="96de2-115">Nombre de IP de puerta de enlace = "GWIP"</span><span class="sxs-lookup"><span data-stu-id="96de2-115">Gateway IP Name = "GWIP"</span></span>
* <span data-ttu-id="96de2-116">Nombre de configuración de IP de puerta de enlace = "gwipconf"</span><span class="sxs-lookup"><span data-stu-id="96de2-116">Gateway IP configuration Name = "gwipconf"</span></span>
* <span data-ttu-id="96de2-117">Tipo = "ExpressRoute" (este tipo es obligatorio para una configuración de ExpressRoute).</span><span class="sxs-lookup"><span data-stu-id="96de2-117">Type = "ExpressRoute" This type is required for an ExpressRoute configuration.</span></span>
* <span data-ttu-id="96de2-118">Nombre de IP pública de puerta de enlace = "gwpip"</span><span class="sxs-lookup"><span data-stu-id="96de2-118">Gateway Public IP Name = "gwpip"</span></span>

## <a name="add-a-gateway"></a><span data-ttu-id="96de2-119">Adición de una puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="96de2-119">Add a gateway</span></span>
1. <span data-ttu-id="96de2-120">Conectar tooyour suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="96de2-120">Connect tooyour Azure Subscription.</span></span>

  ```powershell 
  Login-AzureRmAccount
  Get-AzureRmSubscription 
  Select-AzureRmSubscription -SubscriptionName "Name of subscription"
  ```
2. <span data-ttu-id="96de2-121">Declare las variables para este ejercicio.</span><span class="sxs-lookup"><span data-stu-id="96de2-121">Declare your variables for this exercise.</span></span> <span data-ttu-id="96de2-122">Ser tooedit seguro de que desea toouse una Hola ejemplo tooreflect Hola configuración.</span><span class="sxs-lookup"><span data-stu-id="96de2-122">Be sure tooedit hello sample tooreflect hello settings that you want toouse.</span></span>

  ```powershell 
  $RG = "TestRG"
  $Location = "East US"
  $GWName = "GW"
  $GWIPName = "GWIP"
  $GWIPconfName = "gwipconf"
  $VNetName = "TestVNet"
  ```
3. <span data-ttu-id="96de2-123">Almacenar objetos de red virtual de hello como una variable.</span><span class="sxs-lookup"><span data-stu-id="96de2-123">Store hello virtual network object as a variable.</span></span>

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG
  ```
4. <span data-ttu-id="96de2-124">Agregue un tooyour de subred de puerta de enlace red Virtual.</span><span class="sxs-lookup"><span data-stu-id="96de2-124">Add a gateway subnet tooyour Virtual Network.</span></span> <span data-ttu-id="96de2-125">subred de puerta de enlace de Hello debe denominarse "GatewaySubnet".</span><span class="sxs-lookup"><span data-stu-id="96de2-125">hello gateway subnet must be named "GatewaySubnet".</span></span> <span data-ttu-id="96de2-126">Se recomienda que cree una subred de puerta de enlace con un valor /27 o mayor (/26, /25, etc.).</span><span class="sxs-lookup"><span data-stu-id="96de2-126">You should create a gateway subnet that is /27 or larger (/26, /25, etc.).</span></span>

  ```powershell
  Add-AzureRmVirtualNetworkSubnetConfig -Name GatewaySubnet -VirtualNetwork $vnet -AddressPrefix 192.168.200.0/26
  ```
5. <span data-ttu-id="96de2-127">Establecer configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="96de2-127">Set hello configuration.</span></span>

  ```powershell
  Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
6. <span data-ttu-id="96de2-128">Almacenar la subred de puerta de enlace de hello como una variable.</span><span class="sxs-lookup"><span data-stu-id="96de2-128">Store hello gateway subnet as a variable.</span></span>

  ```powershell
  $subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -VirtualNetwork $vnet
  ```
7. <span data-ttu-id="96de2-129">Pida una dirección IP pública.</span><span class="sxs-lookup"><span data-stu-id="96de2-129">Request a public IP address.</span></span> <span data-ttu-id="96de2-130">se requiere una dirección IP Hola antes de crear la puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="96de2-130">hello IP address is requested before creating hello gateway.</span></span> <span data-ttu-id="96de2-131">No se puede especificar la dirección IP de Hola que desee toouse; se asigna dinámicamente.</span><span class="sxs-lookup"><span data-stu-id="96de2-131">You cannot specify hello IP address that you want toouse; it’s dynamically allocated.</span></span> <span data-ttu-id="96de2-132">Usará esta dirección IP en la sección de configuración siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="96de2-132">You'll use this IP address in hello next configuration section.</span></span> <span data-ttu-id="96de2-133">Hola AllocationMethod debe ser dinámicos.</span><span class="sxs-lookup"><span data-stu-id="96de2-133">hello AllocationMethod must be Dynamic.</span></span>

  ```powershell
  $pip = New-AzureRmPublicIpAddress -Name $GWIPName  -ResourceGroupName $RG -Location $Location -AllocationMethod Dynamic
  ```
8. <span data-ttu-id="96de2-134">Crear configuración de hello para la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="96de2-134">Create hello configuration for your gateway.</span></span> <span data-ttu-id="96de2-135">configuración de puerta de enlace de Hello define la subred de Hola y Hola toouse de dirección IP pública.</span><span class="sxs-lookup"><span data-stu-id="96de2-135">hello gateway configuration defines hello subnet and hello public IP address toouse.</span></span> <span data-ttu-id="96de2-136">En este paso, está especificando la configuración de Hola que se usará al crear puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="96de2-136">In this step, you are specifying hello configuration that will be used when you create hello gateway.</span></span> <span data-ttu-id="96de2-137">Este paso no crea objetos de puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="96de2-137">This step does not actually create hello gateway object.</span></span> <span data-ttu-id="96de2-138">Use la configuración de puerta de enlace de ejemplo de Hola a continuación toocreate.</span><span class="sxs-lookup"><span data-stu-id="96de2-138">Use hello sample below toocreate your gateway configuration.</span></span>

  ```powershell
  $ipconf = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName -Subnet $subnet -PublicIpAddress $pip
  ```
9. <span data-ttu-id="96de2-139">Crear puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="96de2-139">Create hello gateway.</span></span> <span data-ttu-id="96de2-140">En este paso, Hola **- el GatewayType** es especialmente importante.</span><span class="sxs-lookup"><span data-stu-id="96de2-140">In this step, hello **-GatewayType** is especially important.</span></span> <span data-ttu-id="96de2-141">Debe utilizar el valor de hello **ExpressRoute**.</span><span class="sxs-lookup"><span data-stu-id="96de2-141">You must use hello value **ExpressRoute**.</span></span> <span data-ttu-id="96de2-142">Después de ejecutar estos cmdlets, puerta de enlace de hello puede tardar 45 minutos o más toocreate.</span><span class="sxs-lookup"><span data-stu-id="96de2-142">After running these cmdlets, hello gateway can take 45 minutes or more toocreate.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG -Location $Location -IpConfigurations $ipconf -GatewayType Expressroute -GatewaySku Standard
  ```

## <a name="verify-hello-gateway-was-created"></a><span data-ttu-id="96de2-143">Compruebe que se creó la puerta de enlace de Hola</span><span class="sxs-lookup"><span data-stu-id="96de2-143">Verify hello gateway was created</span></span>
<span data-ttu-id="96de2-144">Usar hello siga los comandos tooverify que Hola puerta de enlace se ha creado:</span><span class="sxs-lookup"><span data-stu-id="96de2-144">Use hello following commands tooverify that hello gateway has been created:</span></span>

```powershell
Get-AzureRmVirtualNetworkGateway -ResourceGroupName $RG
```

## <a name="resize-a-gateway"></a><span data-ttu-id="96de2-145">Cambio del tamaño de una puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="96de2-145">Resize a gateway</span></span>
<span data-ttu-id="96de2-146">Hay varias [SKU de puerta de enlace](../articles/expressroute/expressroute-about-virtual-network-gateways.md).</span><span class="sxs-lookup"><span data-stu-id="96de2-146">There are a number of [Gateway SKUs](../articles/expressroute/expressroute-about-virtual-network-gateways.md).</span></span> <span data-ttu-id="96de2-147">Puede usar Hola después comando toochange hello SKU de puerta de enlace en cualquier momento.</span><span class="sxs-lookup"><span data-stu-id="96de2-147">You can use hello following command toochange hello Gateway SKU at any time.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="96de2-148">Este comando no funciona para la puerta de enlace de UltraPerformance.</span><span class="sxs-lookup"><span data-stu-id="96de2-148">This command doesn't work for UltraPerformance gateway.</span></span> <span data-ttu-id="96de2-149">toochange la puerta de enlace de puerta de enlace tooan UltraPerformance, primero quite Hola existente de la puerta de enlace ExpressRoute y, a continuación, crear una nueva puerta de enlace de UltraPerformance.</span><span class="sxs-lookup"><span data-stu-id="96de2-149">toochange your gateway tooan UltraPerformance gateway, first remove hello existing ExpressRoute gateway, and then create a new UltraPerformance gateway.</span></span> <span data-ttu-id="96de2-150">toodowngrade la puerta de enlace de una puerta de enlace UltraPerformance, quite primero Hola UltraPerformance puerta de enlace y, a continuación, cree una nueva puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="96de2-150">toodowngrade your gateway from an UltraPerformance gateway, first remove hello UltraPerformance gateway, and then create a new gateway.</span></span>
> 
> 

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
Resize-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -GatewaySku HighPerformance
```

## <a name="remove-a-gateway"></a><span data-ttu-id="96de2-151">Eliminación de una puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="96de2-151">Remove a gateway</span></span>
<span data-ttu-id="96de2-152">Usar hello después tooremove una puerta de enlace de comando:</span><span class="sxs-lookup"><span data-stu-id="96de2-152">Use hello following command tooremove a gateway:</span></span>

```powershell
Remove-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
```