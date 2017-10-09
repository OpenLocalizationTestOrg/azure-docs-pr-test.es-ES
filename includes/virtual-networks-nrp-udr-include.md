## <a name="route-tables"></a><span data-ttu-id="ffa2e-101">Tablas de ruta</span><span class="sxs-lookup"><span data-stu-id="ffa2e-101">Route tables</span></span>
<span data-ttu-id="ffa2e-102">Recursos de la tabla de enrutamiento contiene toodefine rutas utiliza cómo fluye el tráfico dentro de su infraestructura de Azure.</span><span class="sxs-lookup"><span data-stu-id="ffa2e-102">Route table resources contains routes used toodefine how traffic flows within your Azure infrastructure.</span></span> <span data-ttu-id="ffa2e-103">Puede usar toosend de rutas (UDR) definidos por el usuario de todo el tráfico de subred determinada tooa dispositivo virtual, como un sistema de detección de intrusión o de firewall (ID).</span><span class="sxs-lookup"><span data-stu-id="ffa2e-103">You can use user defined routes (UDR) toosend all traffic from a given subnet tooa virtual appliance, such as a firewall or intrusion detection system (IDS).</span></span> <span data-ttu-id="ffa2e-104">Puede asociar un toosubnets de la tabla de ruta.</span><span class="sxs-lookup"><span data-stu-id="ffa2e-104">You can associate a route table toosubnets.</span></span> 

<span data-ttu-id="ffa2e-105">Tablas de rutas contienen Hola propiedades siguientes.</span><span class="sxs-lookup"><span data-stu-id="ffa2e-105">Route tables contain hello following properties.</span></span>

| <span data-ttu-id="ffa2e-106">Propiedad</span><span class="sxs-lookup"><span data-stu-id="ffa2e-106">Property</span></span> | <span data-ttu-id="ffa2e-107">Descripción</span><span class="sxs-lookup"><span data-stu-id="ffa2e-107">Description</span></span> | <span data-ttu-id="ffa2e-108">Valores de ejemplo</span><span class="sxs-lookup"><span data-stu-id="ffa2e-108">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ffa2e-109">**rutas**</span><span class="sxs-lookup"><span data-stu-id="ffa2e-109">**routes**</span></span> |<span data-ttu-id="ffa2e-110">Colección de usuario definido por las rutas en la tabla de rutas de Hola</span><span class="sxs-lookup"><span data-stu-id="ffa2e-110">Collection of user defined routes in hello route table</span></span> |<span data-ttu-id="ffa2e-111">Consulte las [rutas definidas por el usuario](#User-defined-routes)</span><span class="sxs-lookup"><span data-stu-id="ffa2e-111">see [user defined routes](#User-defined-routes)</span></span> |
| <span data-ttu-id="ffa2e-112">**subredes**</span><span class="sxs-lookup"><span data-stu-id="ffa2e-112">**subnets**</span></span> |<span data-ttu-id="ffa2e-113">Se aplica demasiado la colección de tabla de rutas de Hola de subredes</span><span class="sxs-lookup"><span data-stu-id="ffa2e-113">Collection of subnets hello route table is applied too</span></span>|<span data-ttu-id="ffa2e-114">consulte [subredes](#Subnets)</span><span class="sxs-lookup"><span data-stu-id="ffa2e-114">see [subnets](#Subnets)</span></span> |

### <a name="user-defined-routes"></a><span data-ttu-id="ffa2e-115">rutas definidas por el usuario</span><span class="sxs-lookup"><span data-stu-id="ffa2e-115">User defined routes</span></span>
<span data-ttu-id="ffa2e-116">Puede crear toospecify UDRs dónde se debería enviar tráfico, en función de su dirección de destino.</span><span class="sxs-lookup"><span data-stu-id="ffa2e-116">You can create UDRs toospecify where traffic should be sent to, based on its destination address.</span></span> <span data-ttu-id="ffa2e-117">Una ruta se puede considerar como definición de puerta de enlace predeterminada de hello en función de la dirección de destino de Hola de un paquete de red.</span><span class="sxs-lookup"><span data-stu-id="ffa2e-117">You can think of a route as hello default gateway definition based on hello destination address of a network packet.</span></span>

<span data-ttu-id="ffa2e-118">UDRs contienen Hola propiedades siguientes.</span><span class="sxs-lookup"><span data-stu-id="ffa2e-118">UDRs contain hello following properties.</span></span> 

| <span data-ttu-id="ffa2e-119">Propiedad</span><span class="sxs-lookup"><span data-stu-id="ffa2e-119">Property</span></span> | <span data-ttu-id="ffa2e-120">Descripción</span><span class="sxs-lookup"><span data-stu-id="ffa2e-120">Description</span></span> | <span data-ttu-id="ffa2e-121">Valores de ejemplo</span><span class="sxs-lookup"><span data-stu-id="ffa2e-121">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ffa2e-122">**addressPrefix**</span><span class="sxs-lookup"><span data-stu-id="ffa2e-122">**addressPrefix**</span></span> |<span data-ttu-id="ffa2e-123">Prefijo de dirección o dirección IP completa destino Hola</span><span class="sxs-lookup"><span data-stu-id="ffa2e-123">Address prefix, or full IP address for hello destination</span></span> |<span data-ttu-id="ffa2e-124">192.168.1.0/24, 192.168.1.101</span><span class="sxs-lookup"><span data-stu-id="ffa2e-124">192.168.1.0/24, 192.168.1.101</span></span> |
| <span data-ttu-id="ffa2e-125">**nextHopType**</span><span class="sxs-lookup"><span data-stu-id="ffa2e-125">**nextHopType**</span></span> |<span data-ttu-id="ffa2e-126">Tipo de dispositivo Hola tráfico se enviará demasiado</span><span class="sxs-lookup"><span data-stu-id="ffa2e-126">Type of device hello traffic will be sent too</span></span>|<span data-ttu-id="ffa2e-127">VirtualAppliance, puerta de enlace VPN, Internet</span><span class="sxs-lookup"><span data-stu-id="ffa2e-127">VirtualAppliance, VPN Gateway, Internet</span></span> |
| <span data-ttu-id="ffa2e-128">**nextHopIpAddress**</span><span class="sxs-lookup"><span data-stu-id="ffa2e-128">**nextHopIpAddress**</span></span> |<span data-ttu-id="ffa2e-129">Dirección IP de próximo salto de Hola</span><span class="sxs-lookup"><span data-stu-id="ffa2e-129">IP address for hello next hop</span></span> |<span data-ttu-id="ffa2e-130">192.168.1.4</span><span class="sxs-lookup"><span data-stu-id="ffa2e-130">192.168.1.4</span></span> |

<span data-ttu-id="ffa2e-131">Tabla de ruta de ejemplo en formato JSON:</span><span class="sxs-lookup"><span data-stu-id="ffa2e-131">Sample route table in JSON format:</span></span>

    {
        "name": "UDR-BackEnd",
        "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/routeTables/UDR-BackEnd",
        "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
        "type": "Microsoft.Network/routeTables",
        "location": "westus",
        "properties": {
            "provisioningState": "Succeeded",
            "routes": [
                {
                    "name": "RouteToFrontEnd",
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/routeTables/UDR-BackEnd/routes/RouteToFrontEnd",
                    "etag": "W/\"v\"",
                    "properties": {
                        "provisioningState": "Succeeded",
                        "addressPrefix": "192.168.1.0/24",
                        "nextHopType": "VirtualAppliance",
                        "nextHopIpAddress": "192.168.0.4"
                    }
                }
            ],
            "subnets": [
                {
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/BackEnd"
                }
            ]
        }
    }

### <a name="additional-resources"></a><span data-ttu-id="ffa2e-132">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="ffa2e-132">Additional resources</span></span>
* <span data-ttu-id="ffa2e-133">Obtenga más información acerca de las [Rutas definidas por el usuario](../articles/virtual-network/virtual-networks-udr-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ffa2e-133">Get more information about [UDRs](../articles/virtual-network/virtual-networks-udr-overview.md).</span></span>
* <span data-ttu-id="ffa2e-134">Hola de lectura [documentación de referencia de API de REST](https://msdn.microsoft.com/library/azure/mt502549.aspx) para tablas de rutas.</span><span class="sxs-lookup"><span data-stu-id="ffa2e-134">Read hello [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt502549.aspx) for route tables.</span></span>
* <span data-ttu-id="ffa2e-135">Hola de lectura [documentación de referencia de API de REST](https://msdn.microsoft.com/library/azure/mt502539.aspx) para el usuario definido rutas (UDRs).</span><span class="sxs-lookup"><span data-stu-id="ffa2e-135">Read hello [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt502539.aspx) for user defined routes (UDRs).</span></span>

