### <span data-ttu-id="a8c2a-101"><a name="noconnection"></a>Para modificar los prefijos de dirección IP de la puerta de enlace de red local (sin conexión de puerta de enlace)</span><span class="sxs-lookup"><span data-stu-id="a8c2a-101"><a name="noconnection"></a>To modify local network gateway IP address prefixes - no gateway connection</span></span>

<span data-ttu-id="a8c2a-102">Para agregar prefijos de dirección adicionales:</span><span class="sxs-lookup"><span data-stu-id="a8c2a-102">To add additional address prefixes:</span></span>

```powershell
$local = Get-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName `
Set-AzureRmLocalNetworkGateway -LocalNetworkGateway $local `
-AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24')
```

<span data-ttu-id="a8c2a-103">Para quitar prefijos de dirección:</span><span class="sxs-lookup"><span data-stu-id="a8c2a-103">To remove address prefixes:</span></span><br>
<span data-ttu-id="a8c2a-104">Omita los prefijos que ya no necesite.</span><span class="sxs-lookup"><span data-stu-id="a8c2a-104">Leave out the prefixes that you no longer need.</span></span> <span data-ttu-id="a8c2a-105">En este ejemplo, ya no necesitamos prefijo 20.0.0.0/24 (del ejemplo anterior), por lo que se actualiza la puerta de enlace de la red local, sin incluir ese prefijo.</span><span class="sxs-lookup"><span data-stu-id="a8c2a-105">In this example, we no longer need prefix 20.0.0.0/24 (from the previous example), so we update the local network gateway, excluding that prefix.</span></span>

```powershell
$local = Get-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName `
Set-AzureRmLocalNetworkGateway -LocalNetworkGateway $local `
-AddressPrefix @('10.0.0.0/24','30.0.0.0/24')
```

### <span data-ttu-id="a8c2a-106"><a name="withconnection"></a>Para modificar los prefijos de dirección IP de la puerta de enlace de red local (conexión de puerta de enlace existente)</span><span class="sxs-lookup"><span data-stu-id="a8c2a-106"><a name="withconnection"></a>To modify local network gateway IP address prefixes - existing gateway connection</span></span>

<span data-ttu-id="a8c2a-107">Si tiene una conexión de puerta de enlace y desea agregar o quitar los prefijos de dirección IP contenidos en la puerta de enlace de red local, tendrá que realizar los pasos siguientes en orden.</span><span class="sxs-lookup"><span data-stu-id="a8c2a-107">If you have a gateway connection and want to add or remove the IP address prefixes contained in your local network gateway, you need to do the following steps, in order.</span></span> <span data-ttu-id="a8c2a-108">Esto tendrá como resultado un tiempo de inactividad para la conexión VPN.</span><span class="sxs-lookup"><span data-stu-id="a8c2a-108">This results in some downtime for your VPN connection.</span></span> <span data-ttu-id="a8c2a-109">Al modificar los prefijos de dirección IP, no es necesario eliminar la puerta de enlace VPN.</span><span class="sxs-lookup"><span data-stu-id="a8c2a-109">When modifying IP address prefixes, you don't need to delete the VPN gateway.</span></span> <span data-ttu-id="a8c2a-110">Basta con quitar la conexión.</span><span class="sxs-lookup"><span data-stu-id="a8c2a-110">You only need to remove the connection.</span></span>


1. <span data-ttu-id="a8c2a-111">Cierre la conexión.</span><span class="sxs-lookup"><span data-stu-id="a8c2a-111">Remove the connection.</span></span>

  ```powershell
  Remove-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName -ResourceGroupName MyRGName
  ```
2. <span data-ttu-id="a8c2a-112">Modifique los prefijos de dirección de su puerta de enlace de red local.</span><span class="sxs-lookup"><span data-stu-id="a8c2a-112">Modify the address prefixes for your local network gateway.</span></span>
   
  <span data-ttu-id="a8c2a-113">Establezca la variable para LocalNetworkGateway.</span><span class="sxs-lookup"><span data-stu-id="a8c2a-113">Set the variable for the LocalNetworkGateway.</span></span>

  ```powershell
  $local = Get-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName
  ```
   
  <span data-ttu-id="a8c2a-114">Modifique los prefijos.</span><span class="sxs-lookup"><span data-stu-id="a8c2a-114">Modify the prefixes.</span></span>
   
  ```powershell
  Set-AzureRmLocalNetworkGateway -LocalNetworkGateway $local `
  -AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24')
  ```
3. <span data-ttu-id="a8c2a-115">Cree la conexión.</span><span class="sxs-lookup"><span data-stu-id="a8c2a-115">Create the connection.</span></span> <span data-ttu-id="a8c2a-116">En este ejemplo, vamos a configurar un tipo de conexión de IPsec.</span><span class="sxs-lookup"><span data-stu-id="a8c2a-116">In this example, we configure an IPsec connection type.</span></span> <span data-ttu-id="a8c2a-117">Cuando se vuelva a crear la conexión, use el tipo de conexión que se especifica para la configuración.</span><span class="sxs-lookup"><span data-stu-id="a8c2a-117">When you recreate your connection, use the connection type that is specified for your configuration.</span></span> <span data-ttu-id="a8c2a-118">Para otros tipos de conexión, consulte la página de [cmdlets de PowerShell](https://msdn.microsoft.com/library/mt603611.aspx) .</span><span class="sxs-lookup"><span data-stu-id="a8c2a-118">For additional connection types, see the [PowerShell cmdlet](https://msdn.microsoft.com/library/mt603611.aspx) page.</span></span>
   
  <span data-ttu-id="a8c2a-119">Establezca la variable para VirtualNetworkGateway.</span><span class="sxs-lookup"><span data-stu-id="a8c2a-119">Set the variable for the VirtualNetworkGateway.</span></span>

  ```powershell
  $gateway1 = Get-AzureRmVirtualNetworkGateway -Name RMGateway  -ResourceGroupName MyRGName
  ```
   
  <span data-ttu-id="a8c2a-120">Cree la conexión.</span><span class="sxs-lookup"><span data-stu-id="a8c2a-120">Create the connection.</span></span> <span data-ttu-id="a8c2a-121">Este ejemplo utiliza la variable $local que se estableció en el paso 2.</span><span class="sxs-lookup"><span data-stu-id="a8c2a-121">This example uses the variable $local that you set in step 2.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName `
  -ResourceGroupName MyRGName -Location 'West US' `
  -VirtualNetworkGateway1 $gateway1 -LocalNetworkGateway2 $local `
  -ConnectionType IPsec `
  -RoutingWeight 10 -SharedKey 'abc123'
  ```