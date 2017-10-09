<span data-ttu-id="78575-101">Debe crear una red virtual y una subred de puerta de enlace en primer lugar, antes de trabajar en hello siguiente las tareas.</span><span class="sxs-lookup"><span data-stu-id="78575-101">You must create a VNet and a gateway subnet first, before working on hello following tasks.</span></span> <span data-ttu-id="78575-102">Vea el artículo de hello [configurar una red Virtual con el portal clásico de hello](../articles/expressroute/expressroute-howto-vnet-portal-classic.md) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="78575-102">See hello article [Configure a Virtual Network using hello classic portal](../articles/expressroute/expressroute-howto-vnet-portal-classic.md) for more information.</span></span>   

## <a name="add-a-gateway"></a><span data-ttu-id="78575-103">Adición de una puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="78575-103">Add a gateway</span></span>
<span data-ttu-id="78575-104">Use el comando de hello debajo toocreate una puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="78575-104">Use hello command below toocreate a gateway.</span></span> <span data-ttu-id="78575-105">Ser seguro toosubstitute todos los valores de sus propios.</span><span class="sxs-lookup"><span data-stu-id="78575-105">Be sure toosubstitute any values for your own.</span></span>

    New-AzureVirtualNetworkGateway -VNetName "MyAzureVNET" -GatewayName "ERGateway" -GatewayType Dedicated -GatewaySKU  Standard

## <a name="verify-hello-gateway-was-created"></a><span data-ttu-id="78575-106">Compruebe que se creó la puerta de enlace de Hola</span><span class="sxs-lookup"><span data-stu-id="78575-106">Verify hello gateway was created</span></span>
<span data-ttu-id="78575-107">Se ha creado el comando de Hola de uso siguiente tooverify que Hola puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="78575-107">Use hello command below tooverify that hello gateway has been created.</span></span> <span data-ttu-id="78575-108">Este comando también recupera el Id. de puerta de enlace de hello, que necesita para otras operaciones.</span><span class="sxs-lookup"><span data-stu-id="78575-108">This command also retrieves hello gateway ID, which you need for other operations.</span></span>

    Get-AzureVirtualNetworkGateway

## <a name="resize-a-gateway"></a><span data-ttu-id="78575-109">Cambio del tamaño de una puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="78575-109">Resize a gateway</span></span>
<span data-ttu-id="78575-110">Hay varias [SKU de puerta de enlace](../articles/expressroute/expressroute-about-virtual-network-gateways.md).</span><span class="sxs-lookup"><span data-stu-id="78575-110">There are a number of [Gateway SKUs](../articles/expressroute/expressroute-about-virtual-network-gateways.md).</span></span> <span data-ttu-id="78575-111">Puede usar Hola después comando toochange hello SKU de puerta de enlace en cualquier momento.</span><span class="sxs-lookup"><span data-stu-id="78575-111">You can use hello following command toochange hello Gateway SKU at any time.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="78575-112">Este comando no funciona para la puerta de enlace de UltraPerformance.</span><span class="sxs-lookup"><span data-stu-id="78575-112">This command doesn't work for UltraPerformance gateway.</span></span> <span data-ttu-id="78575-113">toochange la puerta de enlace de puerta de enlace tooan UltraPerformance, primero quite Hola existente de la puerta de enlace ExpressRoute y, a continuación, crear una nueva puerta de enlace de UltraPerformance.</span><span class="sxs-lookup"><span data-stu-id="78575-113">toochange your gateway tooan UltraPerformance gateway, first remove hello existing ExpressRoute gateway, and then create a new UltraPerformance gateway.</span></span> <span data-ttu-id="78575-114">toodowngrade la puerta de enlace de una puerta de enlace UltraPerformance, quite primero Hola UltraPerformance puerta de enlace y, a continuación, cree una nueva puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="78575-114">toodowngrade your gateway from an UltraPerformance gateway, first remove hello UltraPerformance gateway, and then create a new gateway.</span></span> 
> 
> 

    Resize-AzureVirtualNetworkGateway -GatewayId <Gateway ID> -GatewaySKU HighPerformance

## <a name="remove-a-gateway"></a><span data-ttu-id="78575-115">Eliminación de una puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="78575-115">Remove a gateway</span></span>
<span data-ttu-id="78575-116">Usar comandos de hello debajo tooremove una puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="78575-116">Use hello command below tooremove a gateway</span></span>

    Remove-AzureVirtualNetworkGateway -GatewayId <Gateway ID>