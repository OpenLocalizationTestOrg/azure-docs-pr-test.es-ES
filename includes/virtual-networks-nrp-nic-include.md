## <a name="nic"></a><span data-ttu-id="7d8b3-101">NIC</span><span class="sxs-lookup"><span data-stu-id="7d8b3-101">NIC</span></span>
<span data-ttu-id="7d8b3-102">Un recurso de tarjeta (NIC) de interfaz de red proporciona conectividad tooan existente subred en un recurso de red virtual.</span><span class="sxs-lookup"><span data-stu-id="7d8b3-102">A network interface card (NIC) resource provides network connectivity tooan existing subnet in a VNet resource.</span></span> <span data-ttu-id="7d8b3-103">Aunque puede crear una NIC como un objeto independiente, necesita tooassociate se tooanother objeto tooactually proporcionar conectividad.</span><span class="sxs-lookup"><span data-stu-id="7d8b3-103">Although you can create a NIC as a stand alone object, you need tooassociate it tooanother object tooactually provide connectivity.</span></span> <span data-ttu-id="7d8b3-104">Una NIC puede ser tooconnect usa una subred VM tooa, una dirección IP pública o un equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="7d8b3-104">A NIC can be used tooconnect a VM tooa subnet, a public IP address, or a load balancer.</span></span>  

| <span data-ttu-id="7d8b3-105">Propiedad</span><span class="sxs-lookup"><span data-stu-id="7d8b3-105">Property</span></span> | <span data-ttu-id="7d8b3-106">Descripción</span><span class="sxs-lookup"><span data-stu-id="7d8b3-106">Description</span></span> | <span data-ttu-id="7d8b3-107">Valores de ejemplo</span><span class="sxs-lookup"><span data-stu-id="7d8b3-107">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7d8b3-108">**virtualMachine**</span><span class="sxs-lookup"><span data-stu-id="7d8b3-108">**virtualMachine**</span></span> |<span data-ttu-id="7d8b3-109">Hola VM NIC está asociado.</span><span class="sxs-lookup"><span data-stu-id="7d8b3-109">VM hello NIC is associated with.</span></span> |<span data-ttu-id="7d8b3-110">/subscriptions/{guid}/../Microsoft.Compute/virtualMachines/vm1</span><span class="sxs-lookup"><span data-stu-id="7d8b3-110">/subscriptions/{guid}/../Microsoft.Compute/virtualMachines/vm1</span></span> |
| <span data-ttu-id="7d8b3-111">**macAddress**</span><span class="sxs-lookup"><span data-stu-id="7d8b3-111">**macAddress**</span></span> |<span data-ttu-id="7d8b3-112">Dirección MAC para hello NIC</span><span class="sxs-lookup"><span data-stu-id="7d8b3-112">MAC address for hello NIC</span></span> |<span data-ttu-id="7d8b3-113">cualquier valor entre 4 y 30</span><span class="sxs-lookup"><span data-stu-id="7d8b3-113">any value between 4 and 30</span></span> |
| <span data-ttu-id="7d8b3-114">**networkSecurityGroup**</span><span class="sxs-lookup"><span data-stu-id="7d8b3-114">**networkSecurityGroup**</span></span> |<span data-ttu-id="7d8b3-115">NSG asociados toohello NIC</span><span class="sxs-lookup"><span data-stu-id="7d8b3-115">NSG associated toohello NIC</span></span> |<span data-ttu-id="7d8b3-116">/subscriptions/{guid}/../Microsoft.Network/networkSecurityGroups/myNSG1</span><span class="sxs-lookup"><span data-stu-id="7d8b3-116">/subscriptions/{guid}/../Microsoft.Network/networkSecurityGroups/myNSG1</span></span> |
| <span data-ttu-id="7d8b3-117">**dnsSettings**</span><span class="sxs-lookup"><span data-stu-id="7d8b3-117">**dnsSettings**</span></span> |<span data-ttu-id="7d8b3-118">Configuración de DNS para hello NIC</span><span class="sxs-lookup"><span data-stu-id="7d8b3-118">DNS settings for hello NIC</span></span> |<span data-ttu-id="7d8b3-119">Consulte [PIP](#Public-IP-address)</span><span class="sxs-lookup"><span data-stu-id="7d8b3-119">see [PIP](#Public-IP-address)</span></span> |

<span data-ttu-id="7d8b3-120">Una tarjeta de interfaz de red o NIC, representa una interfaz de red que puede ser la máquina virtual (VM) de tooa asociado.</span><span class="sxs-lookup"><span data-stu-id="7d8b3-120">A Network Interface Card, or NIC, represents a network interface that can be associated tooa virtual machine (VM).</span></span> <span data-ttu-id="7d8b3-121">Una máquina virtual puede tener una o varias NIC.</span><span class="sxs-lookup"><span data-stu-id="7d8b3-121">A VM can have one or more NICs.</span></span>

![NIC en una sola máquina virtual](./media/resource-groups-networking/Figure3.png)

### <a name="ip-configurations"></a><span data-ttu-id="7d8b3-123">Configuraciones IP</span><span class="sxs-lookup"><span data-stu-id="7d8b3-123">IP configurations</span></span>
<span data-ttu-id="7d8b3-124">NIC tienen un objeto secundario denominado **ipConfigurations** que contiene Hola propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="7d8b3-124">NICs have a child object named **ipConfigurations** containing hello following properties:</span></span>

| <span data-ttu-id="7d8b3-125">Propiedad</span><span class="sxs-lookup"><span data-stu-id="7d8b3-125">Property</span></span> | <span data-ttu-id="7d8b3-126">Descripción</span><span class="sxs-lookup"><span data-stu-id="7d8b3-126">Description</span></span> | <span data-ttu-id="7d8b3-127">Valores de ejemplo</span><span class="sxs-lookup"><span data-stu-id="7d8b3-127">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7d8b3-128">**subnet**</span><span class="sxs-lookup"><span data-stu-id="7d8b3-128">**subnet**</span></span> |<span data-ttu-id="7d8b3-129">Hola de subred NIC está conectada a.</span><span class="sxs-lookup"><span data-stu-id="7d8b3-129">Subnet hello NIC is onnected to.</span></span> |<span data-ttu-id="7d8b3-130">/subscriptions/{guid}/../Microsoft.Network/virtualNetworks/myvnet1/subnets/mysub1</span><span class="sxs-lookup"><span data-stu-id="7d8b3-130">/subscriptions/{guid}/../Microsoft.Network/virtualNetworks/myvnet1/subnets/mysub1</span></span> |
| <span data-ttu-id="7d8b3-131">**privateIPAddress**</span><span class="sxs-lookup"><span data-stu-id="7d8b3-131">**privateIPAddress**</span></span> |<span data-ttu-id="7d8b3-132">Dirección IP para hello NIC en la subred de Hola</span><span class="sxs-lookup"><span data-stu-id="7d8b3-132">IP address for hello NIC in hello subnet</span></span> |<span data-ttu-id="7d8b3-133">10.0.0.8</span><span class="sxs-lookup"><span data-stu-id="7d8b3-133">10.0.0.8</span></span> |
| <span data-ttu-id="7d8b3-134">**privateIPAllocationMethod**</span><span class="sxs-lookup"><span data-stu-id="7d8b3-134">**privateIPAllocationMethod**</span></span> |<span data-ttu-id="7d8b3-135">Método de asignación de direcciones IP</span><span class="sxs-lookup"><span data-stu-id="7d8b3-135">IP allocation method</span></span> |<span data-ttu-id="7d8b3-136">Dynamic o Static</span><span class="sxs-lookup"><span data-stu-id="7d8b3-136">Dynamic or Static</span></span> |
| <span data-ttu-id="7d8b3-137">**enableIPForwarding**</span><span class="sxs-lookup"><span data-stu-id="7d8b3-137">**enableIPForwarding**</span></span> |<span data-ttu-id="7d8b3-138">Si se puede usar Hola NIC para el enrutamiento</span><span class="sxs-lookup"><span data-stu-id="7d8b3-138">Whether hello NIC can be used for routing</span></span> |<span data-ttu-id="7d8b3-139">true o false</span><span class="sxs-lookup"><span data-stu-id="7d8b3-139">true or false</span></span> |
| <span data-ttu-id="7d8b3-140">**primary**</span><span class="sxs-lookup"><span data-stu-id="7d8b3-140">**primary**</span></span> |<span data-ttu-id="7d8b3-141">Si es Hola NIC Hola NIC principal para hello VM</span><span class="sxs-lookup"><span data-stu-id="7d8b3-141">Whether hello NIC is hello primary NIC for hello VM</span></span> |<span data-ttu-id="7d8b3-142">true o false</span><span class="sxs-lookup"><span data-stu-id="7d8b3-142">true or false</span></span> |
| <span data-ttu-id="7d8b3-143">**publicIPAddress**</span><span class="sxs-lookup"><span data-stu-id="7d8b3-143">**publicIPAddress**</span></span> |<span data-ttu-id="7d8b3-144">PIP asociada Hola NIC</span><span class="sxs-lookup"><span data-stu-id="7d8b3-144">PIP associated with hello NIC</span></span> |<span data-ttu-id="7d8b3-145">vea [Configuración de DNS](#DNS-settings)</span><span class="sxs-lookup"><span data-stu-id="7d8b3-145">see [DNS Settings](#DNS-settings)</span></span> |
| <span data-ttu-id="7d8b3-146">**loadBalancerBackendAddressPools**</span><span class="sxs-lookup"><span data-stu-id="7d8b3-146">**loadBalancerBackendAddressPools**</span></span> |<span data-ttu-id="7d8b3-147">Hacer copia de Hola de grupos de dirección final que está asociado a la NIC</span><span class="sxs-lookup"><span data-stu-id="7d8b3-147">Back end address pools hello NIC is associated with</span></span> | |
| <span data-ttu-id="7d8b3-148">**loadBalancerInboundNatRules**</span><span class="sxs-lookup"><span data-stu-id="7d8b3-148">**loadBalancerInboundNatRules**</span></span> |<span data-ttu-id="7d8b3-149">Entrada Hola de reglas NAT carga equilibrador A que NIC está asociado</span><span class="sxs-lookup"><span data-stu-id="7d8b3-149">Inbound load balancer NAT rules hello NIC is associated with</span></span> | |

<span data-ttu-id="7d8b3-150">Dirección IP pública de ejemplo en formato JSON:</span><span class="sxs-lookup"><span data-stu-id="7d8b3-150">Sample public IP address in JSON format:</span></span>

    {
        "name": "lb-nic1-be",
        "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/nrprg/providers/Microsoft.Network/networkInterfaces/lb-nic1-be",
        "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
        "type": "Microsoft.Network/networkInterfaces",
        "location": "eastus",
        "properties": {
            "provisioningState": "Succeeded",
            "resourceGuid": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
            "ipConfigurations": [
                {
                    "name": "NIC-config",
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/nrprg/providers/Microsoft.Network/networkInterfaces/lb-nic1-be/ipConfigurations/NIC-config",
                    "etag": "W/\"0027f1a2-3ac8-49de-b5d5-fd46550500b1\"",
                    "properties": {
                        "provisioningState": "Succeeded",
                        "privateIPAddress": "10.0.0.4",
                        "privateIPAllocationMethod": "Dynamic",
                        "subnet": {
                            "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/NRPRG/providers/Microsoft.Network/virtualNetworks/NRPVnet/subnets/NRPVnetSubnet"
                        },
                        "loadBalancerBackendAddressPools": [
                            {
                                "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool"
                            }
                        ],
                        "loadBalancerInboundNatRules": [
                            {
                                "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp1"
                            }
                        ]
                    }
                }
            ],
            "dnsSettings": { ... },
            "macAddress": "00-0D-3A-10-F1-29",
            "enableIPForwarding": false,
            "primary": true,
            "virtualMachine": {
                "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/nrprg/providers/Microsoft.Compute/virtualMachines/web1"
            }
        }
    }

### <a name="additional-resources"></a><span data-ttu-id="7d8b3-151">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="7d8b3-151">Additional resources</span></span>
* <span data-ttu-id="7d8b3-152">Hola de lectura [documentación de referencia de API de REST](https://msdn.microsoft.com/library/azure/mt163579.aspx) de NIC.</span><span class="sxs-lookup"><span data-stu-id="7d8b3-152">Read hello [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163579.aspx) for NICs.</span></span>

