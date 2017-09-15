## <a name="network-security-group"></a><span data-ttu-id="68f5a-101">Grupo de seguridad de red (NSG)</span><span class="sxs-lookup"><span data-stu-id="68f5a-101">Network Security Group</span></span>
<span data-ttu-id="68f5a-102">Un recurso de grupo de seguridad de red permite la creación de un límite de seguridad para las cargas de trabajo mediante la implementación de reglas de permiso y denegación.</span><span class="sxs-lookup"><span data-stu-id="68f5a-102">An NSG resource enables the creation of security boundary for workloads, by implementing allow and deny rules.</span></span> <span data-ttu-id="68f5a-103">Estas reglas pueden aplicarse a una máquina virtual, una NIC o una subred.</span><span class="sxs-lookup"><span data-stu-id="68f5a-103">Such rules can be applied to a VM, a NIC, or a subnet.</span></span>

| <span data-ttu-id="68f5a-104">Propiedad</span><span class="sxs-lookup"><span data-stu-id="68f5a-104">Property</span></span> | <span data-ttu-id="68f5a-105">Descripción</span><span class="sxs-lookup"><span data-stu-id="68f5a-105">Description</span></span> | <span data-ttu-id="68f5a-106">Valores de ejemplo</span><span class="sxs-lookup"><span data-stu-id="68f5a-106">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="68f5a-107">**subredes**</span><span class="sxs-lookup"><span data-stu-id="68f5a-107">**subnets**</span></span> |<span data-ttu-id="68f5a-108">Lista de identificadores de subred a los cuales se aplica el grupo de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="68f5a-108">List of subnet ids the NSG is applied to.</span></span> |<span data-ttu-id="68f5a-109">/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd</span><span class="sxs-lookup"><span data-stu-id="68f5a-109">/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd</span></span> |
| <span data-ttu-id="68f5a-110">**securityRules**</span><span class="sxs-lookup"><span data-stu-id="68f5a-110">**securityRules**</span></span> |<span data-ttu-id="68f5a-111">Lista de reglas de seguridad que constituyen el Grupo de seguridad de red</span><span class="sxs-lookup"><span data-stu-id="68f5a-111">List of security rules that make up the NSG</span></span> |<span data-ttu-id="68f5a-112">Consulte la [regla de seguridad](#Security-rule) que tiene a continuación</span><span class="sxs-lookup"><span data-stu-id="68f5a-112">See [Security rule](#Security-rule) below</span></span> |
| <span data-ttu-id="68f5a-113">**defaultSecurityRules**</span><span class="sxs-lookup"><span data-stu-id="68f5a-113">**defaultSecurityRules**</span></span> |<span data-ttu-id="68f5a-114">Lista de reglas de seguridad predeterminadas presentes en cada Grupo de seguridad de red</span><span class="sxs-lookup"><span data-stu-id="68f5a-114">List of default security rules present in every NSG</span></span> |<span data-ttu-id="68f5a-115">Consulte las [reglas de seguridad predeterminadas](#Default-security-rules) que tiene a continuación</span><span class="sxs-lookup"><span data-stu-id="68f5a-115">See [Default security rules](#Default-security-rules) below</span></span> |

* <span data-ttu-id="68f5a-116">**Regla de seguridad** : un grupo de seguridad de red puede contener varias reglas de seguridad definidas.</span><span class="sxs-lookup"><span data-stu-id="68f5a-116">**Security rule** - An NSG can have multiple security rules defined.</span></span> <span data-ttu-id="68f5a-117">Cada regla puede permitir o denegar distintos tipos de tráfico.</span><span class="sxs-lookup"><span data-stu-id="68f5a-117">Each rule can allow or deny different types of traffic.</span></span>

### <a name="security-rule"></a><span data-ttu-id="68f5a-118">regla de seguridad</span><span class="sxs-lookup"><span data-stu-id="68f5a-118">Security rule</span></span>
<span data-ttu-id="68f5a-119">Una regla de seguridad es un recurso secundario de un Grupo de seguridad de red que contiene las siguientes propiedades.</span><span class="sxs-lookup"><span data-stu-id="68f5a-119">A security rule is a child resource of an NSG containing the properties below.</span></span>

| <span data-ttu-id="68f5a-120">Propiedad</span><span class="sxs-lookup"><span data-stu-id="68f5a-120">Property</span></span> | <span data-ttu-id="68f5a-121">Descripción</span><span class="sxs-lookup"><span data-stu-id="68f5a-121">Description</span></span> | <span data-ttu-id="68f5a-122">Valores de ejemplo</span><span class="sxs-lookup"><span data-stu-id="68f5a-122">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="68f5a-123">**descripción**</span><span class="sxs-lookup"><span data-stu-id="68f5a-123">**description**</span></span> |<span data-ttu-id="68f5a-124">Descripción de la regla</span><span class="sxs-lookup"><span data-stu-id="68f5a-124">Description for the rule</span></span> |<span data-ttu-id="68f5a-125">Permite el tráfico entrante para todas las máquinas virtuales en la subred X</span><span class="sxs-lookup"><span data-stu-id="68f5a-125">Allow inbound traffic for all VMs in subnet X</span></span> |
| <span data-ttu-id="68f5a-126">**protocolo**</span><span class="sxs-lookup"><span data-stu-id="68f5a-126">**protocol**</span></span> |<span data-ttu-id="68f5a-127">Protocolo que debe coincidir con la regla</span><span class="sxs-lookup"><span data-stu-id="68f5a-127">Protocol to match for the rule</span></span> |<span data-ttu-id="68f5a-128">TCP, UDP o *.</span><span class="sxs-lookup"><span data-stu-id="68f5a-128">TCP, UDP, or *</span></span> |
| <span data-ttu-id="68f5a-129">**sourcePortRange**</span><span class="sxs-lookup"><span data-stu-id="68f5a-129">**sourcePortRange**</span></span> |<span data-ttu-id="68f5a-130">Intervalo del puerto de origen que debe coincidir con la regla</span><span class="sxs-lookup"><span data-stu-id="68f5a-130">Source port range to match for the rule</span></span> |<span data-ttu-id="68f5a-131">80, 100-200, *</span><span class="sxs-lookup"><span data-stu-id="68f5a-131">80, 100-200, *</span></span> |
| <span data-ttu-id="68f5a-132">**destinationPortRange**</span><span class="sxs-lookup"><span data-stu-id="68f5a-132">**destinationPortRange**</span></span> |<span data-ttu-id="68f5a-133">Intervalo del puerto de destino que debe coincidir con la regla</span><span class="sxs-lookup"><span data-stu-id="68f5a-133">Destination port range to match for the rule</span></span> |<span data-ttu-id="68f5a-134">80, 100-200, *</span><span class="sxs-lookup"><span data-stu-id="68f5a-134">80, 100-200, *</span></span> |
| <span data-ttu-id="68f5a-135">**sourceAddressPrefix**</span><span class="sxs-lookup"><span data-stu-id="68f5a-135">**sourceAddressPrefix**</span></span> |<span data-ttu-id="68f5a-136">Prefijo de la dirección de origen que debe coincidir con la regla</span><span class="sxs-lookup"><span data-stu-id="68f5a-136">Source address prefix to match for the rule</span></span> |<span data-ttu-id="68f5a-137">10.10.10.1, 10.10.10.0/24, VirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="68f5a-137">10.10.10.1, 10.10.10.0/24, VirtualNetwork</span></span> |
| <span data-ttu-id="68f5a-138">**destinationAddressPrefix**</span><span class="sxs-lookup"><span data-stu-id="68f5a-138">**destinationAddressPrefix**</span></span> |<span data-ttu-id="68f5a-139">Prefijo de la dirección de destino que debe coincidir con la regla</span><span class="sxs-lookup"><span data-stu-id="68f5a-139">Destination address prefix to match for the rule</span></span> |<span data-ttu-id="68f5a-140">10.10.10.1, 10.10.10.0/24, VirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="68f5a-140">10.10.10.1, 10.10.10.0/24, VirtualNetwork</span></span> |
| <span data-ttu-id="68f5a-141">**dirección**</span><span class="sxs-lookup"><span data-stu-id="68f5a-141">**direction**</span></span> |<span data-ttu-id="68f5a-142">Dirección del tráfico que debe coincidir con la regla</span><span class="sxs-lookup"><span data-stu-id="68f5a-142">Direction of traffic to match for the rule</span></span> |<span data-ttu-id="68f5a-143">entrada o salida</span><span class="sxs-lookup"><span data-stu-id="68f5a-143">inbound or outbound</span></span> |
| <span data-ttu-id="68f5a-144">**prioridad**</span><span class="sxs-lookup"><span data-stu-id="68f5a-144">**priority**</span></span> |<span data-ttu-id="68f5a-145">Prioridad de la regla.</span><span class="sxs-lookup"><span data-stu-id="68f5a-145">Priority for the rule.</span></span> <span data-ttu-id="68f5a-146">Las reglas se comprueban según su orden de prioridad; una vez se aplica una regla, no se prueban más reglas para realizar la coincidencia.</span><span class="sxs-lookup"><span data-stu-id="68f5a-146">Rules are checked int he order of priority, once a rule applies, no more rules are tested for matching.</span></span> |<span data-ttu-id="68f5a-147">10, 100, 65000</span><span class="sxs-lookup"><span data-stu-id="68f5a-147">10, 100, 65000</span></span> |
| <span data-ttu-id="68f5a-148">**acceso**</span><span class="sxs-lookup"><span data-stu-id="68f5a-148">**access**</span></span> |<span data-ttu-id="68f5a-149">Tipo de acceso que se debe aplicar si coincide con la regla</span><span class="sxs-lookup"><span data-stu-id="68f5a-149">Type of access to apply if the rule matches</span></span> |<span data-ttu-id="68f5a-150">permitir o denegar</span><span class="sxs-lookup"><span data-stu-id="68f5a-150">allow or deny</span></span> |

<span data-ttu-id="68f5a-151">Grupo de seguridad de red de ejemplo en formato JSON:</span><span class="sxs-lookup"><span data-stu-id="68f5a-151">Sample NSG in JSON format:</span></span>

    {
        "name": "NSG-BackEnd",
        "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd",
        "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
        "type": "Microsoft.Network/networkSecurityGroups",
        "location": "westus",
        "tags": {
            "displayName": "NSG - Front End"
        },
        "properties": {
            "provisioningState": "Succeeded",
            "resourceGuid": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
            "securityRules": [
                {
                    "name": "rdp-rule",
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd/securityRules/rdp-rule",
                    "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
                    "properties": {
                        "provisioningState": "Succeeded",
                        "description": "Allow RDP",
                        "protocol": "Tcp",
                        "sourcePortRange": "*",
                        "destinationPortRange": "3389",
                        "sourceAddressPrefix": "Internet",
                        "destinationAddressPrefix": "*",
                        "access": "Allow",
                        "priority": 100,
                        "direction": "Inbound"
                    }
                }
            ],
            "defaultSecurityRules": [
                { [...],
            "subnets": [
                {
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd"
                }
            ]
        }
    }

### <a name="default-security-rules"></a><span data-ttu-id="68f5a-152">reglas de seguridad predeterminadas</span><span class="sxs-lookup"><span data-stu-id="68f5a-152">Default security rules</span></span>

<span data-ttu-id="68f5a-153">Las reglas de seguridad predeterminadas tienen las mismas propiedades disponibles en las reglas de seguridad.</span><span class="sxs-lookup"><span data-stu-id="68f5a-153">Default security rules have the same properties available in security rules.</span></span> <span data-ttu-id="68f5a-154">Existen para proporcionar una conexión básica entre aquellos recursos que tengan los Grupos de seguridad de red aplicados.</span><span class="sxs-lookup"><span data-stu-id="68f5a-154">They exist to provide basic connectivity between resources that have NSGs applied to them.</span></span> <span data-ttu-id="68f5a-155">Asegúrese de que sabe qué [reglas de seguridad predeterminadas](../articles/virtual-network/virtual-networks-nsg.md#default-rules) existen.</span><span class="sxs-lookup"><span data-stu-id="68f5a-155">Make sure you know which [default security rules](../articles/virtual-network/virtual-networks-nsg.md#default-rules) exist.</span></span>

### <a name="additional-resources"></a><span data-ttu-id="68f5a-156">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="68f5a-156">Additional resources</span></span>
* <span data-ttu-id="68f5a-157">Obtenga más información acerca de los [Grupos de seguridad de red](../articles/virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="68f5a-157">Get more information about [NSGs](../articles/virtual-network/virtual-networks-nsg.md).</span></span>
* <span data-ttu-id="68f5a-158">Lea la [documentación de referencia de la API de REST](https://msdn.microsoft.com/library/azure/mt163615.aspx) para obtener información sobre los Grupos de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="68f5a-158">Read the [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163615.aspx) for NSGs.</span></span>
* <span data-ttu-id="68f5a-159">Lea la [documentación de referencia de la API de REST](https://msdn.microsoft.com/library/azure/mt163580.aspx) para obtener información sobre las reglas de seguridad.</span><span class="sxs-lookup"><span data-stu-id="68f5a-159">Read the [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163580.aspx) for security rules.</span></span>
