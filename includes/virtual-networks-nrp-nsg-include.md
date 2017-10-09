## <a name="network-security-group"></a><span data-ttu-id="0d50e-101">Grupo de seguridad de red (NSG)</span><span class="sxs-lookup"><span data-stu-id="0d50e-101">Network Security Group</span></span>
<span data-ttu-id="0d50e-102">Un recurso NSG permite la creación de hello de límite de seguridad para las cargas de trabajo, mediante la implementación de permitir y denegar las reglas.</span><span class="sxs-lookup"><span data-stu-id="0d50e-102">An NSG resource enables hello creation of security boundary for workloads, by implementing allow and deny rules.</span></span> <span data-ttu-id="0d50e-103">Estas reglas se pueden aplicar tooa máquina virtual, una NIC o una subred.</span><span class="sxs-lookup"><span data-stu-id="0d50e-103">Such rules can be applied tooa VM, a NIC, or a subnet.</span></span>

| <span data-ttu-id="0d50e-104">Propiedad</span><span class="sxs-lookup"><span data-stu-id="0d50e-104">Property</span></span> | <span data-ttu-id="0d50e-105">Descripción</span><span class="sxs-lookup"><span data-stu-id="0d50e-105">Description</span></span> | <span data-ttu-id="0d50e-106">Valores de ejemplo</span><span class="sxs-lookup"><span data-stu-id="0d50e-106">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0d50e-107">**subredes**</span><span class="sxs-lookup"><span data-stu-id="0d50e-107">**subnets**</span></span> |<span data-ttu-id="0d50e-108">Lista de identificadores de subred hello NSG se aplica a.</span><span class="sxs-lookup"><span data-stu-id="0d50e-108">List of subnet ids hello NSG is applied to.</span></span> |<span data-ttu-id="0d50e-109">/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd</span><span class="sxs-lookup"><span data-stu-id="0d50e-109">/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd</span></span> |
| <span data-ttu-id="0d50e-110">**securityRules**</span><span class="sxs-lookup"><span data-stu-id="0d50e-110">**securityRules**</span></span> |<span data-ttu-id="0d50e-111">Lista de reglas de seguridad que componen hello NSG</span><span class="sxs-lookup"><span data-stu-id="0d50e-111">List of security rules that make up hello NSG</span></span> |<span data-ttu-id="0d50e-112">Consulte la [regla de seguridad](#Security-rule) que tiene a continuación</span><span class="sxs-lookup"><span data-stu-id="0d50e-112">See [Security rule](#Security-rule) below</span></span> |
| <span data-ttu-id="0d50e-113">**defaultSecurityRules**</span><span class="sxs-lookup"><span data-stu-id="0d50e-113">**defaultSecurityRules**</span></span> |<span data-ttu-id="0d50e-114">Lista de reglas de seguridad predeterminadas presentes en cada Grupo de seguridad de red</span><span class="sxs-lookup"><span data-stu-id="0d50e-114">List of default security rules present in every NSG</span></span> |<span data-ttu-id="0d50e-115">Consulte las [reglas de seguridad predeterminadas](#Default-security-rules) que tiene a continuación</span><span class="sxs-lookup"><span data-stu-id="0d50e-115">See [Default security rules](#Default-security-rules) below</span></span> |

* <span data-ttu-id="0d50e-116">**Regla de seguridad** : un grupo de seguridad de red puede contener varias reglas de seguridad definidas.</span><span class="sxs-lookup"><span data-stu-id="0d50e-116">**Security rule** - An NSG can have multiple security rules defined.</span></span> <span data-ttu-id="0d50e-117">Cada regla puede permitir o denegar distintos tipos de tráfico.</span><span class="sxs-lookup"><span data-stu-id="0d50e-117">Each rule can allow or deny different types of traffic.</span></span>

### <a name="security-rule"></a><span data-ttu-id="0d50e-118">regla de seguridad</span><span class="sxs-lookup"><span data-stu-id="0d50e-118">Security rule</span></span>
<span data-ttu-id="0d50e-119">Una regla de seguridad es un recurso secundario de un NSG que contiene propiedades de Hola a continuación.</span><span class="sxs-lookup"><span data-stu-id="0d50e-119">A security rule is a child resource of an NSG containing hello properties below.</span></span>

| <span data-ttu-id="0d50e-120">Propiedad</span><span class="sxs-lookup"><span data-stu-id="0d50e-120">Property</span></span> | <span data-ttu-id="0d50e-121">Descripción</span><span class="sxs-lookup"><span data-stu-id="0d50e-121">Description</span></span> | <span data-ttu-id="0d50e-122">Valores de ejemplo</span><span class="sxs-lookup"><span data-stu-id="0d50e-122">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0d50e-123">**descripción**</span><span class="sxs-lookup"><span data-stu-id="0d50e-123">**description**</span></span> |<span data-ttu-id="0d50e-124">Descripción de regla de Hola</span><span class="sxs-lookup"><span data-stu-id="0d50e-124">Description for hello rule</span></span> |<span data-ttu-id="0d50e-125">Permite el tráfico entrante para todas las máquinas virtuales en la subred X</span><span class="sxs-lookup"><span data-stu-id="0d50e-125">Allow inbound traffic for all VMs in subnet X</span></span> |
| <span data-ttu-id="0d50e-126">**protocolo**</span><span class="sxs-lookup"><span data-stu-id="0d50e-126">**protocol**</span></span> |<span data-ttu-id="0d50e-127">Toomatch de protocolo para la regla de Hola</span><span class="sxs-lookup"><span data-stu-id="0d50e-127">Protocol toomatch for hello rule</span></span> |<span data-ttu-id="0d50e-128">TCP, UDP o *.</span><span class="sxs-lookup"><span data-stu-id="0d50e-128">TCP, UDP, or *</span></span> |
| <span data-ttu-id="0d50e-129">**sourcePortRange**</span><span class="sxs-lookup"><span data-stu-id="0d50e-129">**sourcePortRange**</span></span> |<span data-ttu-id="0d50e-130">Toomatch de intervalo de puerto de origen para la regla de Hola</span><span class="sxs-lookup"><span data-stu-id="0d50e-130">Source port range toomatch for hello rule</span></span> |<span data-ttu-id="0d50e-131">80, 100-200, *</span><span class="sxs-lookup"><span data-stu-id="0d50e-131">80, 100-200, *</span></span> |
| <span data-ttu-id="0d50e-132">**destinationPortRange**</span><span class="sxs-lookup"><span data-stu-id="0d50e-132">**destinationPortRange**</span></span> |<span data-ttu-id="0d50e-133">Toomatch de intervalo de puerto de destino para la regla de Hola</span><span class="sxs-lookup"><span data-stu-id="0d50e-133">Destination port range toomatch for hello rule</span></span> |<span data-ttu-id="0d50e-134">80, 100-200, *</span><span class="sxs-lookup"><span data-stu-id="0d50e-134">80, 100-200, *</span></span> |
| <span data-ttu-id="0d50e-135">**sourceAddressPrefix**</span><span class="sxs-lookup"><span data-stu-id="0d50e-135">**sourceAddressPrefix**</span></span> |<span data-ttu-id="0d50e-136">Toomatch de prefijo de dirección de origen para la regla de Hola</span><span class="sxs-lookup"><span data-stu-id="0d50e-136">Source address prefix toomatch for hello rule</span></span> |<span data-ttu-id="0d50e-137">10.10.10.1, 10.10.10.0/24, VirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="0d50e-137">10.10.10.1, 10.10.10.0/24, VirtualNetwork</span></span> |
| <span data-ttu-id="0d50e-138">**destinationAddressPrefix**</span><span class="sxs-lookup"><span data-stu-id="0d50e-138">**destinationAddressPrefix**</span></span> |<span data-ttu-id="0d50e-139">Toomatch de prefijo de dirección de destino para la regla de Hola</span><span class="sxs-lookup"><span data-stu-id="0d50e-139">Destination address prefix toomatch for hello rule</span></span> |<span data-ttu-id="0d50e-140">10.10.10.1, 10.10.10.0/24, VirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="0d50e-140">10.10.10.1, 10.10.10.0/24, VirtualNetwork</span></span> |
| <span data-ttu-id="0d50e-141">**dirección**</span><span class="sxs-lookup"><span data-stu-id="0d50e-141">**direction**</span></span> |<span data-ttu-id="0d50e-142">Dirección del tráfico toomatch de regla de Hola</span><span class="sxs-lookup"><span data-stu-id="0d50e-142">Direction of traffic toomatch for hello rule</span></span> |<span data-ttu-id="0d50e-143">entrada o salida</span><span class="sxs-lookup"><span data-stu-id="0d50e-143">inbound or outbound</span></span> |
| <span data-ttu-id="0d50e-144">**prioridad**</span><span class="sxs-lookup"><span data-stu-id="0d50e-144">**priority**</span></span> |<span data-ttu-id="0d50e-145">Prioridad de la regla de Hola.</span><span class="sxs-lookup"><span data-stu-id="0d50e-145">Priority for hello rule.</span></span> <span data-ttu-id="0d50e-146">Las reglas se comprueban según su orden de prioridad; una vez se aplica una regla, no se prueban más reglas para realizar la coincidencia.</span><span class="sxs-lookup"><span data-stu-id="0d50e-146">Rules are checked int he order of priority, once a rule applies, no more rules are tested for matching.</span></span> |<span data-ttu-id="0d50e-147">10, 100, 65000</span><span class="sxs-lookup"><span data-stu-id="0d50e-147">10, 100, 65000</span></span> |
| <span data-ttu-id="0d50e-148">**acceso**</span><span class="sxs-lookup"><span data-stu-id="0d50e-148">**access**</span></span> |<span data-ttu-id="0d50e-149">Tipo de acceso tooapply si coincide con la regla de Hola</span><span class="sxs-lookup"><span data-stu-id="0d50e-149">Type of access tooapply if hello rule matches</span></span> |<span data-ttu-id="0d50e-150">permitir o denegar</span><span class="sxs-lookup"><span data-stu-id="0d50e-150">allow or deny</span></span> |

<span data-ttu-id="0d50e-151">Grupo de seguridad de red de ejemplo en formato JSON:</span><span class="sxs-lookup"><span data-stu-id="0d50e-151">Sample NSG in JSON format:</span></span>

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

### <a name="default-security-rules"></a><span data-ttu-id="0d50e-152">reglas de seguridad predeterminadas</span><span class="sxs-lookup"><span data-stu-id="0d50e-152">Default security rules</span></span>

<span data-ttu-id="0d50e-153">Reglas de seguridad predeterminadas tienen Hola mismas propiedades disponibles en las reglas de seguridad.</span><span class="sxs-lookup"><span data-stu-id="0d50e-153">Default security rules have hello same properties available in security rules.</span></span> <span data-ttu-id="0d50e-154">Existen tooprovide la conectividad básica entre los recursos que tienen los NSG aplicados toothem.</span><span class="sxs-lookup"><span data-stu-id="0d50e-154">They exist tooprovide basic connectivity between resources that have NSGs applied toothem.</span></span> <span data-ttu-id="0d50e-155">Asegúrese de que sabe qué [reglas de seguridad predeterminadas](../articles/virtual-network/virtual-networks-nsg.md#default-rules) existen.</span><span class="sxs-lookup"><span data-stu-id="0d50e-155">Make sure you know which [default security rules](../articles/virtual-network/virtual-networks-nsg.md#default-rules) exist.</span></span>

### <a name="additional-resources"></a><span data-ttu-id="0d50e-156">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="0d50e-156">Additional resources</span></span>
* <span data-ttu-id="0d50e-157">Obtenga más información acerca de los [Grupos de seguridad de red](../articles/virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="0d50e-157">Get more information about [NSGs](../articles/virtual-network/virtual-networks-nsg.md).</span></span>
* <span data-ttu-id="0d50e-158">Hola de lectura [documentación de referencia de API de REST](https://msdn.microsoft.com/library/azure/mt163615.aspx) para NSG.</span><span class="sxs-lookup"><span data-stu-id="0d50e-158">Read hello [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163615.aspx) for NSGs.</span></span>
* <span data-ttu-id="0d50e-159">Hola de lectura [documentación de referencia de API de REST](https://msdn.microsoft.com/library/azure/mt163580.aspx) para reglas de seguridad.</span><span class="sxs-lookup"><span data-stu-id="0d50e-159">Read hello [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163580.aspx) for security rules.</span></span>
