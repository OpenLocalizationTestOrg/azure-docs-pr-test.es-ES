### <span data-ttu-id="8226c-101"><a name="noconnection"></a>prefijos de direcciones en la IP de la puerta de enlace de red local toomodify - no hay ninguna conexión de puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="8226c-101"><a name="noconnection"></a>toomodify local network gateway IP address prefixes - no gateway connection</span></span>

<span data-ttu-id="8226c-102">prefijos de dirección adicional tooadd:</span><span class="sxs-lookup"><span data-stu-id="8226c-102">tooadd additional address prefixes:</span></span>

```powershell
$local = Get-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName `
Set-AzureRmLocalNetworkGateway -LocalNetworkGateway $local `
-AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24')
```

<span data-ttu-id="8226c-103">prefijos de direcciones de tooremove:</span><span class="sxs-lookup"><span data-stu-id="8226c-103">tooremove address prefixes:</span></span><br>
<span data-ttu-id="8226c-104">Omitir los prefijos de Hola que ya no necesite.</span><span class="sxs-lookup"><span data-stu-id="8226c-104">Leave out hello prefixes that you no longer need.</span></span> <span data-ttu-id="8226c-105">En este ejemplo, ya no necesitamos prefijo 20.0.0.0/24 (de ejemplo de Hola anterior), por lo que se actualice la puerta de enlace de red local de hello, sin incluir ese prefijo.</span><span class="sxs-lookup"><span data-stu-id="8226c-105">In this example, we no longer need prefix 20.0.0.0/24 (from hello previous example), so we update hello local network gateway, excluding that prefix.</span></span>

```powershell
$local = Get-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName `
Set-AzureRmLocalNetworkGateway -LocalNetworkGateway $local `
-AddressPrefix @('10.0.0.0/24','30.0.0.0/24')
```

### <span data-ttu-id="8226c-106"><a name="withconnection"></a>toomodify red local puerta de enlace prefijos de direcciones IP: conexión de puerta de enlace existente</span><span class="sxs-lookup"><span data-stu-id="8226c-106"><a name="withconnection"></a>toomodify local network gateway IP address prefixes - existing gateway connection</span></span>

<span data-ttu-id="8226c-107">Si tiene una conexión de puerta de enlace y desea tooadd o quitar prefijos de direcciones IP de hello contenidos en la puerta de enlace de red local, deberá hello toodo siguiendo los pasos en orden.</span><span class="sxs-lookup"><span data-stu-id="8226c-107">If you have a gateway connection and want tooadd or remove hello IP address prefixes contained in your local network gateway, you need toodo hello following steps, in order.</span></span> <span data-ttu-id="8226c-108">Esto tendrá como resultado un tiempo de inactividad para la conexión VPN.</span><span class="sxs-lookup"><span data-stu-id="8226c-108">This results in some downtime for your VPN connection.</span></span> <span data-ttu-id="8226c-109">Cuando se modifica prefijos de direcciones IP, no es necesario puerta de enlace VPN toodelete Hola.</span><span class="sxs-lookup"><span data-stu-id="8226c-109">When modifying IP address prefixes, you don't need toodelete hello VPN gateway.</span></span> <span data-ttu-id="8226c-110">Solo necesita conexión de hello tooremove.</span><span class="sxs-lookup"><span data-stu-id="8226c-110">You only need tooremove hello connection.</span></span>


1. <span data-ttu-id="8226c-111">Quitar conexión de Hola.</span><span class="sxs-lookup"><span data-stu-id="8226c-111">Remove hello connection.</span></span>

  ```powershell
  Remove-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName -ResourceGroupName MyRGName
  ```
2. <span data-ttu-id="8226c-112">Modifique los prefijos de direcciones de hello para la puerta de enlace de red local.</span><span class="sxs-lookup"><span data-stu-id="8226c-112">Modify hello address prefixes for your local network gateway.</span></span>
   
  <span data-ttu-id="8226c-113">Establecer variable de Hola para hello LocalNetworkGateway.</span><span class="sxs-lookup"><span data-stu-id="8226c-113">Set hello variable for hello LocalNetworkGateway.</span></span>

  ```powershell
  $local = Get-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName
  ```
   
  <span data-ttu-id="8226c-114">Modifique los prefijos de Hola.</span><span class="sxs-lookup"><span data-stu-id="8226c-114">Modify hello prefixes.</span></span>
   
  ```powershell
  Set-AzureRmLocalNetworkGateway -LocalNetworkGateway $local `
  -AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24')
  ```
3. <span data-ttu-id="8226c-115">Crear conexiones de Hola.</span><span class="sxs-lookup"><span data-stu-id="8226c-115">Create hello connection.</span></span> <span data-ttu-id="8226c-116">En este ejemplo, vamos a configurar un tipo de conexión de IPsec.</span><span class="sxs-lookup"><span data-stu-id="8226c-116">In this example, we configure an IPsec connection type.</span></span> <span data-ttu-id="8226c-117">Cuando se vuelve a crear la conexión, use el tipo de conexión de Hola que se especifica para la configuración.</span><span class="sxs-lookup"><span data-stu-id="8226c-117">When you recreate your connection, use hello connection type that is specified for your configuration.</span></span> <span data-ttu-id="8226c-118">Para los tipos de conexión adicionales, vea hello [cmdlet de PowerShell](https://msdn.microsoft.com/library/mt603611.aspx) página.</span><span class="sxs-lookup"><span data-stu-id="8226c-118">For additional connection types, see hello [PowerShell cmdlet](https://msdn.microsoft.com/library/mt603611.aspx) page.</span></span>
   
  <span data-ttu-id="8226c-119">Establecer variable de Hola para hello VirtualNetworkGateway.</span><span class="sxs-lookup"><span data-stu-id="8226c-119">Set hello variable for hello VirtualNetworkGateway.</span></span>

  ```powershell
  $gateway1 = Get-AzureRmVirtualNetworkGateway -Name RMGateway  -ResourceGroupName MyRGName
  ```
   
  <span data-ttu-id="8226c-120">Crear conexiones de Hola.</span><span class="sxs-lookup"><span data-stu-id="8226c-120">Create hello connection.</span></span> <span data-ttu-id="8226c-121">Este ejemplo utiliza la variable de hello $local que establece en el paso 2.</span><span class="sxs-lookup"><span data-stu-id="8226c-121">This example uses hello variable $local that you set in step 2.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName `
  -ResourceGroupName MyRGName -Location 'West US' `
  -VirtualNetworkGateway1 $gateway1 -LocalNetworkGateway2 $local `
  -ConnectionType IPsec `
  -RoutingWeight 10 -SharedKey 'abc123'
  ```