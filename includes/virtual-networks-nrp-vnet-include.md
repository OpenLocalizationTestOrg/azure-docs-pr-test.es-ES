## <a name="virtual-network"></a><span data-ttu-id="62a90-101">Red virtual</span><span class="sxs-lookup"><span data-stu-id="62a90-101">Virtual Network</span></span>
<span data-ttu-id="62a90-102">Los recursos de redes virtuales (VNET) y de subredes le ayudarán a definir un límite de seguridad para las cargas de trabajo que se ejecuten en Azure.</span><span class="sxs-lookup"><span data-stu-id="62a90-102">Virtual Networks (VNET) and subnets resources help define a security boundary for workloads running in Azure.</span></span> <span data-ttu-id="62a90-103">Una red virtual se caracteriza por una colección de espacios de direcciones, también denominados bloques CIDR.</span><span class="sxs-lookup"><span data-stu-id="62a90-103">A VNet is characterized by a collection of address spaces, defined as CIDR blocks.</span></span> 

> [!NOTE]
> <span data-ttu-id="62a90-104">Los administradores de red ya están familiarizados con la notación CIDR.</span><span class="sxs-lookup"><span data-stu-id="62a90-104">Network administrators are familiar with CIDR notation.</span></span> <span data-ttu-id="62a90-105">Si no está familiarizado con el formato CIDR, [puede obtener más información](http://whatismyipaddress.com/cidr).</span><span class="sxs-lookup"><span data-stu-id="62a90-105">If you are not familiar with CIDR, [learn more about it](http://whatismyipaddress.com/cidr).</span></span>
> 
> 

![Redes virtuales con varias subredes](./media/resource-groups-networking/Figure4.png)

<span data-ttu-id="62a90-107">Redes virtuales contienen Hola propiedades siguientes.</span><span class="sxs-lookup"><span data-stu-id="62a90-107">VNets contain hello following properties.</span></span>

| <span data-ttu-id="62a90-108">Propiedad</span><span class="sxs-lookup"><span data-stu-id="62a90-108">Property</span></span> | <span data-ttu-id="62a90-109">Descripción</span><span class="sxs-lookup"><span data-stu-id="62a90-109">Description</span></span> | <span data-ttu-id="62a90-110">Valores de ejemplo</span><span class="sxs-lookup"><span data-stu-id="62a90-110">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="62a90-111">**addressSpace**</span><span class="sxs-lookup"><span data-stu-id="62a90-111">**addressSpace**</span></span> |<span data-ttu-id="62a90-112">Colección de prefijos de direcciones que constituyen Hola red virtual en la notación CIDR</span><span class="sxs-lookup"><span data-stu-id="62a90-112">Collection of address prefixes that make up hello VNet in CIDR notation</span></span> |<span data-ttu-id="62a90-113">192.168.0.0/16</span><span class="sxs-lookup"><span data-stu-id="62a90-113">192.168.0.0/16</span></span> |
| <span data-ttu-id="62a90-114">**subredes**</span><span class="sxs-lookup"><span data-stu-id="62a90-114">**subnets**</span></span> |<span data-ttu-id="62a90-115">Colección de subredes que componen Hola red virtual</span><span class="sxs-lookup"><span data-stu-id="62a90-115">Collection of subnets that make up hello VNet</span></span> |<span data-ttu-id="62a90-116">Consulte la información acerca de las [subredes](#Subnets) que tiene a continuación.</span><span class="sxs-lookup"><span data-stu-id="62a90-116">see [subnets](#Subnets) below.</span></span> |
| <span data-ttu-id="62a90-117">**ipAddress**</span><span class="sxs-lookup"><span data-stu-id="62a90-117">**ipAddress**</span></span> |<span data-ttu-id="62a90-118">Dirección IP asignada tooobject.</span><span class="sxs-lookup"><span data-stu-id="62a90-118">IP address assigned tooobject.</span></span> <span data-ttu-id="62a90-119">Se trata de una propiedad de solo lectura.</span><span class="sxs-lookup"><span data-stu-id="62a90-119">This is a read-only property.</span></span> |<span data-ttu-id="62a90-120">104.42.233.77</span><span class="sxs-lookup"><span data-stu-id="62a90-120">104.42.233.77</span></span> |

### <a name="subnets"></a><span data-ttu-id="62a90-121">Subredes</span><span class="sxs-lookup"><span data-stu-id="62a90-121">Subnets</span></span>
<span data-ttu-id="62a90-122">Una subred es un recurso secundario de una red virtual que le ayudará a definir segmentos de espacios de direcciones dentro de un bloque CIDR mediante prefijos de direcciones IP.</span><span class="sxs-lookup"><span data-stu-id="62a90-122">A subnet is a child resource of a VNet, and helps define segments of address spaces within a CIDR block, using IP address prefixes.</span></span> <span data-ttu-id="62a90-123">Pueden agregarse NIC toosubnets y tooVMs conectados, proporcionar conectividad para diversas cargas de trabajo.</span><span class="sxs-lookup"><span data-stu-id="62a90-123">NICs can be added toosubnets, and connected tooVMs, providing connectivity for various workloads.</span></span>

<span data-ttu-id="62a90-124">Subredes contienen Hola propiedades siguientes.</span><span class="sxs-lookup"><span data-stu-id="62a90-124">Subnets contain hello following properties.</span></span> 

| <span data-ttu-id="62a90-125">Propiedad</span><span class="sxs-lookup"><span data-stu-id="62a90-125">Property</span></span> | <span data-ttu-id="62a90-126">Descripción</span><span class="sxs-lookup"><span data-stu-id="62a90-126">Description</span></span> | <span data-ttu-id="62a90-127">Valores de ejemplo</span><span class="sxs-lookup"><span data-stu-id="62a90-127">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="62a90-128">**addressPrefix**</span><span class="sxs-lookup"><span data-stu-id="62a90-128">**addressPrefix**</span></span> |<span data-ttu-id="62a90-129">Prefijo de dirección única que componen la subred de hello en la notación CIDR</span><span class="sxs-lookup"><span data-stu-id="62a90-129">Single address prefix that make up hello subnet in CIDR notation</span></span> |<span data-ttu-id="62a90-130">192.168.1.0/24</span><span class="sxs-lookup"><span data-stu-id="62a90-130">192.168.1.0/24</span></span> |
| <span data-ttu-id="62a90-131">**networkSecurityGroup**</span><span class="sxs-lookup"><span data-stu-id="62a90-131">**networkSecurityGroup**</span></span> |<span data-ttu-id="62a90-132">NSG aplica toohello subred</span><span class="sxs-lookup"><span data-stu-id="62a90-132">NSG applied toohello subnet</span></span> |<span data-ttu-id="62a90-133">Consulte [Grupos de seguridad de red](#Network-Security-Group)</span><span class="sxs-lookup"><span data-stu-id="62a90-133">see [NSGs](#Network-Security-Group)</span></span> |
| <span data-ttu-id="62a90-134">**routeTable**</span><span class="sxs-lookup"><span data-stu-id="62a90-134">**routeTable**</span></span> |<span data-ttu-id="62a90-135">Tabla de ruta aplicado toohello subred</span><span class="sxs-lookup"><span data-stu-id="62a90-135">Route table applied toohello subnet</span></span> |<span data-ttu-id="62a90-136">Consulte [Enrutamiento definido por el usuario](#Route-table)</span><span class="sxs-lookup"><span data-stu-id="62a90-136">see [UDR](#Route-table)</span></span> |
| <span data-ttu-id="62a90-137">**ipConfigurations**</span><span class="sxs-lookup"><span data-stu-id="62a90-137">**ipConfigurations**</span></span> |<span data-ttu-id="62a90-138">Colección de objetos de configuración IP utilizada por NIC conectado toohello subred</span><span class="sxs-lookup"><span data-stu-id="62a90-138">Collection of IP configruation objects used by NICs connected toohello subnet</span></span> |<span data-ttu-id="62a90-139">Consulte [Enrutamiento definido por el usuario](#Route-table)</span><span class="sxs-lookup"><span data-stu-id="62a90-139">see [UDR](#Route-table)</span></span> |

<span data-ttu-id="62a90-140">Red virtual de ejemplo en formato JSON:</span><span class="sxs-lookup"><span data-stu-id="62a90-140">Sample VNet in JSON format:</span></span>

    {
        "name": "TestVNet",
        "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet",
        "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
        "type": "Microsoft.Network/virtualNetworks",
        "location": "westus",
        "tags": {
            "displayName": "VNet"
        },
        "properties": {
            "provisioningState": "Succeeded",
            "resourceGuid": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
            "addressSpace": {
                "addressPrefixes": [
                    "192.168.0.0/16"
                ]
            },
            "subnets": [
                {
                    "name": "FrontEnd",
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                    "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
                    "properties": {
                        "provisioningState": "Succeeded",
                        "addressPrefix": "192.168.1.0/24",
                        "networkSecurityGroup": {
                            "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd"
                        },
                        "routeTable": {
                            "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/routeTables/UDR-FrontEnd"
                        },
                        "ipConfigurations": [
                            {
                                "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICWEB1/ipConfigurations/ipconfig1"
                            },
                            ...]
                    }
                },
                ...]
        }
    }

### <a name="additional-resources"></a><span data-ttu-id="62a90-141">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="62a90-141">Additional resources</span></span>
* <span data-ttu-id="62a90-142">Obtenga más información acerca de las [Redes virtuales](../articles/virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="62a90-142">Get more information about [VNet](../articles/virtual-network/virtual-networks-overview.md).</span></span>
* <span data-ttu-id="62a90-143">Hola de lectura [documentación de referencia de API de REST](https://msdn.microsoft.com/library/azure/mt163650.aspx) para redes virtuales.</span><span class="sxs-lookup"><span data-stu-id="62a90-143">Read hello [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163650.aspx) for VNets.</span></span>
* <span data-ttu-id="62a90-144">Hola de lectura [documentación de referencia de API de REST](https://msdn.microsoft.com/library/azure/mt163618.aspx) para subredes.</span><span class="sxs-lookup"><span data-stu-id="62a90-144">Read hello [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163618.aspx) for Subnets.</span></span>

