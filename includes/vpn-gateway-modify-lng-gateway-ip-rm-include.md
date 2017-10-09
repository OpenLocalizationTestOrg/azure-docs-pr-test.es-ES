### <span data-ttu-id="9503c-101"><a name="gwipnoconnection"></a>puerta de enlace de la red local de hello toomodify 'GatewayIpAddress': no hay ninguna conexión de puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="9503c-101"><a name="gwipnoconnection"></a> toomodify hello local network gateway 'GatewayIpAddress' - no gateway connection</span></span>

<span data-ttu-id="9503c-102">Si el dispositivo VPN de Hola que desea tooconnect toohas cambia su dirección IP pública, debe toomodify tooreflect de puerta de enlace de red local de Hola que cambian.</span><span class="sxs-lookup"><span data-stu-id="9503c-102">If hello VPN device that you want tooconnect toohas changed its public IP address, you need toomodify hello local network gateway tooreflect that change.</span></span> <span data-ttu-id="9503c-103">Utilice toomodify de ejemplo de Hola una puerta de enlace de red local que no tiene una conexión de puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="9503c-103">Use hello example toomodify a local network gateway that does not have a gateway connection.</span></span>

<span data-ttu-id="9503c-104">Cuando se modifica este valor, también puede modificar los prefijos de direcciones de hello en hello mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="9503c-104">When modifying this value, you can also modify hello address prefixes at hello same time.</span></span> <span data-ttu-id="9503c-105">Ser seguro toouse Hola existente nombre de la puerta de enlace de red local en la configuración actual de orden toooverwrite Hola.</span><span class="sxs-lookup"><span data-stu-id="9503c-105">Be sure toouse hello existing name of your local network gateway in order toooverwrite hello current settings.</span></span> <span data-ttu-id="9503c-106">Si utiliza un nombre diferente, puede crear una nueva puerta de enlace de red local, en lugar de sobrescribir Hola uno ya existente.</span><span class="sxs-lookup"><span data-stu-id="9503c-106">If you use a different name, you create a new local network gateway, instead of overwriting hello existing one.</span></span>

```powershell
New-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName `
-Location "West US" -AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24') `
-GatewayIpAddress "5.4.3.2" -ResourceGroupName MyRGName
```

### <span data-ttu-id="9503c-107"><a name="gwipwithconnection"></a>puerta de enlace de la red local de hello toomodify 'GatewayIpAddress' - conexión de puerta de enlace existente</span><span class="sxs-lookup"><span data-stu-id="9503c-107"><a name="gwipwithconnection"></a>toomodify hello local network gateway 'GatewayIpAddress' - existing gateway connection</span></span>

<span data-ttu-id="9503c-108">Si el dispositivo VPN de Hola que desea tooconnect toohas cambia su dirección IP pública, debe toomodify tooreflect de puerta de enlace de red local de Hola que cambian.</span><span class="sxs-lookup"><span data-stu-id="9503c-108">If hello VPN device that you want tooconnect toohas changed its public IP address, you need toomodify hello local network gateway tooreflect that change.</span></span> <span data-ttu-id="9503c-109">Si la puerta de enlace ya existe una conexión, primero debe conexión de hello tooremove.</span><span class="sxs-lookup"><span data-stu-id="9503c-109">If a gateway connection already exists, you first need tooremove hello connection.</span></span> <span data-ttu-id="9503c-110">Después de quita la conexión de hello, puede modificar la dirección IP de puerta de enlace de Hola y volver a crear una nueva conexión.</span><span class="sxs-lookup"><span data-stu-id="9503c-110">After hello connection is removed, you can modify hello gateway IP address and recreate a new connection.</span></span> <span data-ttu-id="9503c-111">También puede modificar los prefijos de direcciones de hello en hello mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="9503c-111">You can also modify hello address prefixes at hello same time.</span></span> <span data-ttu-id="9503c-112">Esto tendrá como resultado un tiempo de inactividad para la conexión VPN.</span><span class="sxs-lookup"><span data-stu-id="9503c-112">This results in some downtime for your VPN connection.</span></span> <span data-ttu-id="9503c-113">Cuando se modifica la dirección IP de puerta de enlace de hello, no necesita la puerta de enlace VPN toodelete Hola.</span><span class="sxs-lookup"><span data-stu-id="9503c-113">When modifying hello gateway IP address, you don't need toodelete hello VPN gateway.</span></span> <span data-ttu-id="9503c-114">Solo necesita conexión de hello tooremove.</span><span class="sxs-lookup"><span data-stu-id="9503c-114">You only need tooremove hello connection.</span></span>
 

1. <span data-ttu-id="9503c-115">Quitar conexión de Hola.</span><span class="sxs-lookup"><span data-stu-id="9503c-115">Remove hello connection.</span></span> <span data-ttu-id="9503c-116">Puede encontrar Hola nombre de la conexión mediante el cmdlet de hello 'Get-AzureRmVirtualNetworkGatewayConnection'.</span><span class="sxs-lookup"><span data-stu-id="9503c-116">You can find hello name of your connection by using hello 'Get-AzureRmVirtualNetworkGatewayConnection' cmdlet.</span></span>

  ```powershell
  Remove-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName `
  -ResourceGroupName MyRGName
  ```
2. <span data-ttu-id="9503c-117">Modifique el valor de 'GatewayIpAddress' hello.</span><span class="sxs-lookup"><span data-stu-id="9503c-117">Modify hello 'GatewayIpAddress' value.</span></span> <span data-ttu-id="9503c-118">También puede modificar los prefijos de direcciones de hello en hello mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="9503c-118">You can also modify hello address prefixes at hello same time.</span></span> <span data-ttu-id="9503c-119">Ser seguro toouse Hola existente nombre de la configuración actual de red local puerta de enlace toooverwrite Hola.</span><span class="sxs-lookup"><span data-stu-id="9503c-119">Be sure toouse hello existing name of your local network gateway toooverwrite hello current settings.</span></span> <span data-ttu-id="9503c-120">Si no lo hace, puede crear una nueva puerta de enlace de red local, en lugar de sobrescribir Hola uno ya existente.</span><span class="sxs-lookup"><span data-stu-id="9503c-120">If you don't, you create a new local network gateway, instead of overwriting hello existing one.</span></span>

  ```powershell
  New-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName `
  -Location "West US" -AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24') `
  -GatewayIpAddress "104.40.81.124" -ResourceGroupName MyRGName
  ```
3. <span data-ttu-id="9503c-121">Crear conexiones de Hola.</span><span class="sxs-lookup"><span data-stu-id="9503c-121">Create hello connection.</span></span> <span data-ttu-id="9503c-122">En este ejemplo, vamos a configurar un tipo de conexión de IPsec.</span><span class="sxs-lookup"><span data-stu-id="9503c-122">In this example, we configure an IPsec connection type.</span></span> <span data-ttu-id="9503c-123">Cuando se vuelve a crear la conexión, use el tipo de conexión de Hola que se especifica para la configuración.</span><span class="sxs-lookup"><span data-stu-id="9503c-123">When you recreate your connection, use hello connection type that is specified for your configuration.</span></span> <span data-ttu-id="9503c-124">Para los tipos de conexión adicionales, vea hello [cmdlet de PowerShell](https://msdn.microsoft.com/library/mt603611.aspx) página.</span><span class="sxs-lookup"><span data-stu-id="9503c-124">For additional connection types, see hello [PowerShell cmdlet](https://msdn.microsoft.com/library/mt603611.aspx) page.</span></span>  <span data-ttu-id="9503c-125">nombre de tooobtain hello VirtualNetworkGateway, puede ejecutar hello 'Get-AzureRmVirtualNetworkGateway' cmdlet.</span><span class="sxs-lookup"><span data-stu-id="9503c-125">tooobtain hello VirtualNetworkGateway name, you can run hello 'Get-AzureRmVirtualNetworkGateway' cmdlet.</span></span>
   
    <span data-ttu-id="9503c-126">Establecer variables de Hola.</span><span class="sxs-lookup"><span data-stu-id="9503c-126">Set hello variables.</span></span>

  ```powershell
  $local = Get-AzureRMLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName `
  $vnetgw = Get-AzureRmVirtualNetworkGateway -Name RMGateway -ResourceGroupName MyRGName
  ```
   
    <span data-ttu-id="9503c-127">Crear conexiones de Hola.</span><span class="sxs-lookup"><span data-stu-id="9503c-127">Create hello connection.</span></span>

  ```powershell 
  New-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName -ResourceGroupName MyRGName `
  -Location "West US" `
  -VirtualNetworkGateway1 $vnetgw `
  -LocalNetworkGateway2 $local `
  -ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
  ```