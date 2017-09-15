## <a name="nic"></a><span data-ttu-id="55bad-101">NIC</span><span class="sxs-lookup"><span data-stu-id="55bad-101">NIC</span></span>
<span data-ttu-id="55bad-102">Un recurso de tarjeta de interfaz de red (NIC) proporciona conectividad de red a una subred existente en un recurso de red virtual.</span><span class="sxs-lookup"><span data-stu-id="55bad-102">A network interface card (NIC) resource provides network connectivity to an existing subnet in a VNet resource.</span></span> <span data-ttu-id="55bad-103">Aunque puede crear un NIC como un objeto independiente, debe asociarlo a otro objeto para, realmente, proporcionar conectividad.</span><span class="sxs-lookup"><span data-stu-id="55bad-103">Although you can create a NIC as a stand alone object, you need to associate it to another object to actually provide connectivity.</span></span> <span data-ttu-id="55bad-104">Una NIC se puede usar para conectar una VM a una subred, a una dirección IP pública o a un equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="55bad-104">A NIC can be used to connect a VM to a subnet, a public IP address, or a load balancer.</span></span>  

| <span data-ttu-id="55bad-105">Propiedad</span><span class="sxs-lookup"><span data-stu-id="55bad-105">Property</span></span> | <span data-ttu-id="55bad-106">Descripción</span><span class="sxs-lookup"><span data-stu-id="55bad-106">Description</span></span> | <span data-ttu-id="55bad-107">Valores de ejemplo</span><span class="sxs-lookup"><span data-stu-id="55bad-107">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="55bad-108">**virtualMachine**</span><span class="sxs-lookup"><span data-stu-id="55bad-108">**virtualMachine**</span></span> |<span data-ttu-id="55bad-109">VM a la que se asocia la NIC.</span><span class="sxs-lookup"><span data-stu-id="55bad-109">VM the NIC is associated with.</span></span> |<span data-ttu-id="55bad-110">/subscriptions/{guid}/../Microsoft.Compute/virtualMachines/vm1</span><span class="sxs-lookup"><span data-stu-id="55bad-110">/subscriptions/{guid}/../Microsoft.Compute/virtualMachines/vm1</span></span> |
| <span data-ttu-id="55bad-111">**macAddress**</span><span class="sxs-lookup"><span data-stu-id="55bad-111">**macAddress**</span></span> |<span data-ttu-id="55bad-112">Dirección MAC de la NIC</span><span class="sxs-lookup"><span data-stu-id="55bad-112">MAC address for the NIC</span></span> |<span data-ttu-id="55bad-113">cualquier valor entre 4 y 30</span><span class="sxs-lookup"><span data-stu-id="55bad-113">any value between 4 and 30</span></span> |
| <span data-ttu-id="55bad-114">**networkSecurityGroup**</span><span class="sxs-lookup"><span data-stu-id="55bad-114">**networkSecurityGroup**</span></span> |<span data-ttu-id="55bad-115">Grupo de seguridad de red asociado a la NIC</span><span class="sxs-lookup"><span data-stu-id="55bad-115">NSG associated to the NIC</span></span> |<span data-ttu-id="55bad-116">/subscriptions/{guid}/../Microsoft.Network/networkSecurityGroups/myNSG1</span><span class="sxs-lookup"><span data-stu-id="55bad-116">/subscriptions/{guid}/../Microsoft.Network/networkSecurityGroups/myNSG1</span></span> |
| <span data-ttu-id="55bad-117">**dnsSettings**</span><span class="sxs-lookup"><span data-stu-id="55bad-117">**dnsSettings**</span></span> |<span data-ttu-id="55bad-118">Configuración de DNS para la NIC</span><span class="sxs-lookup"><span data-stu-id="55bad-118">DNS settings for the NIC</span></span> |<span data-ttu-id="55bad-119">Consulte [PIP](#Public-IP-address)</span><span class="sxs-lookup"><span data-stu-id="55bad-119">see [PIP](#Public-IP-address)</span></span> |

<span data-ttu-id="55bad-120">La tarjeta de interfaz de red, o NIC, representa una interfaz de red que se puede asociar a una máquina virtual (VM).</span><span class="sxs-lookup"><span data-stu-id="55bad-120">A Network Interface Card, or NIC, represents a network interface that can be associated to a virtual machine (VM).</span></span> <span data-ttu-id="55bad-121">Una máquina virtual puede tener una o varias NIC.</span><span class="sxs-lookup"><span data-stu-id="55bad-121">A VM can have one or more NICs.</span></span>

![NIC en una sola máquina virtual](./media/resource-groups-networking/Figure3.png)

### <a name="ip-configurations"></a><span data-ttu-id="55bad-123">Configuraciones IP</span><span class="sxs-lookup"><span data-stu-id="55bad-123">IP configurations</span></span>
<span data-ttu-id="55bad-124">Las NIC tienen un objeto secundario llamado **ipConfigurations** que contiene las propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="55bad-124">NICs have a child object named **ipConfigurations** containing the following properties:</span></span>

| <span data-ttu-id="55bad-125">Propiedad</span><span class="sxs-lookup"><span data-stu-id="55bad-125">Property</span></span> | <span data-ttu-id="55bad-126">Descripción</span><span class="sxs-lookup"><span data-stu-id="55bad-126">Description</span></span> | <span data-ttu-id="55bad-127">Valores de ejemplo</span><span class="sxs-lookup"><span data-stu-id="55bad-127">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="55bad-128">**subnet**</span><span class="sxs-lookup"><span data-stu-id="55bad-128">**subnet**</span></span> |<span data-ttu-id="55bad-129">Subred a la que está conectada la NIC</span><span class="sxs-lookup"><span data-stu-id="55bad-129">Subnet the NIC is onnected to.</span></span> |<span data-ttu-id="55bad-130">/subscriptions/{guid}/../Microsoft.Network/virtualNetworks/myvnet1/subnets/mysub1</span><span class="sxs-lookup"><span data-stu-id="55bad-130">/subscriptions/{guid}/../Microsoft.Network/virtualNetworks/myvnet1/subnets/mysub1</span></span> |
| <span data-ttu-id="55bad-131">**privateIPAddress**</span><span class="sxs-lookup"><span data-stu-id="55bad-131">**privateIPAddress**</span></span> |<span data-ttu-id="55bad-132">Dirección IP de la NIC en la subred</span><span class="sxs-lookup"><span data-stu-id="55bad-132">IP address for the NIC in the subnet</span></span> |<span data-ttu-id="55bad-133">10.0.0.8</span><span class="sxs-lookup"><span data-stu-id="55bad-133">10.0.0.8</span></span> |
| <span data-ttu-id="55bad-134">**privateIPAllocationMethod**</span><span class="sxs-lookup"><span data-stu-id="55bad-134">**privateIPAllocationMethod**</span></span> |<span data-ttu-id="55bad-135">Método de asignación de direcciones IP</span><span class="sxs-lookup"><span data-stu-id="55bad-135">IP allocation method</span></span> |<span data-ttu-id="55bad-136">Dynamic o Static</span><span class="sxs-lookup"><span data-stu-id="55bad-136">Dynamic or Static</span></span> |
| <span data-ttu-id="55bad-137">**enableIPForwarding**</span><span class="sxs-lookup"><span data-stu-id="55bad-137">**enableIPForwarding**</span></span> |<span data-ttu-id="55bad-138">Si la NIC se puede usar para el enrutamiento</span><span class="sxs-lookup"><span data-stu-id="55bad-138">Whether the NIC can be used for routing</span></span> |<span data-ttu-id="55bad-139">true o false</span><span class="sxs-lookup"><span data-stu-id="55bad-139">true or false</span></span> |
| <span data-ttu-id="55bad-140">**primary**</span><span class="sxs-lookup"><span data-stu-id="55bad-140">**primary**</span></span> |<span data-ttu-id="55bad-141">Si la NIC es la NIC principal para la VM</span><span class="sxs-lookup"><span data-stu-id="55bad-141">Whether the NIC is the primary NIC for the VM</span></span> |<span data-ttu-id="55bad-142">true o false</span><span class="sxs-lookup"><span data-stu-id="55bad-142">true or false</span></span> |
| <span data-ttu-id="55bad-143">**publicIPAddress**</span><span class="sxs-lookup"><span data-stu-id="55bad-143">**publicIPAddress**</span></span> |<span data-ttu-id="55bad-144">PIP asociado a la NIC.</span><span class="sxs-lookup"><span data-stu-id="55bad-144">PIP associated with the NIC</span></span> |<span data-ttu-id="55bad-145">vea [Configuración de DNS](#DNS-settings)</span><span class="sxs-lookup"><span data-stu-id="55bad-145">see [DNS Settings](#DNS-settings)</span></span> |
| <span data-ttu-id="55bad-146">**loadBalancerBackendAddressPools**</span><span class="sxs-lookup"><span data-stu-id="55bad-146">**loadBalancerBackendAddressPools**</span></span> |<span data-ttu-id="55bad-147">Grupos de direcciones de back-end a los que se asocia la NIC</span><span class="sxs-lookup"><span data-stu-id="55bad-147">Back end address pools the NIC is associated with</span></span> | |
| <span data-ttu-id="55bad-148">**loadBalancerInboundNatRules**</span><span class="sxs-lookup"><span data-stu-id="55bad-148">**loadBalancerInboundNatRules**</span></span> |<span data-ttu-id="55bad-149">Reglas NAT del equilibrador de carga de entrada a las que está asociada la NIC</span><span class="sxs-lookup"><span data-stu-id="55bad-149">Inbound load balancer NAT rules the NIC is associated with</span></span> | |

<span data-ttu-id="55bad-150">Dirección IP pública de ejemplo en formato JSON:</span><span class="sxs-lookup"><span data-stu-id="55bad-150">Sample public IP address in JSON format:</span></span>

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

### <a name="additional-resources"></a><span data-ttu-id="55bad-151">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="55bad-151">Additional resources</span></span>
* <span data-ttu-id="55bad-152">Lea la [documentación de referencia de la API de REST](https://msdn.microsoft.com/library/azure/mt163579.aspx) para obtener información sobre las NIC.</span><span class="sxs-lookup"><span data-stu-id="55bad-152">Read the [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163579.aspx) for NICs.</span></span>

