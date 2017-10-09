---
title: aaaManage de red de grupos de seguridad - 1.0 de CLI de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toomanage grupos de seguridad de red mediante hello Azure interfaz de línea de comandos (CLI) 1.0."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/21/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 9a429f947abbcb5fa6adb40c84504f68efd5e20e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-network-security-groups-using-hello-azure-cli-10"></a><span data-ttu-id="30a62-103">Administrar grupos de seguridad de red mediante Hola 1.0 de CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="30a62-103">Manage network security groups using hello Azure CLI 1.0</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="30a62-104">Tarea CLI versiones toocomplete hello</span><span class="sxs-lookup"><span data-stu-id="30a62-104">CLI versions toocomplete hello task</span></span> 

<span data-ttu-id="30a62-105">Puede completar la tarea hello mediante uno de hello después de las versiones CLI:</span><span class="sxs-lookup"><span data-stu-id="30a62-105">You can complete hello task using one of hello following CLI versions:</span></span> 

- <span data-ttu-id="30a62-106">[Azure 1.0 de CLI](#View-existing-NSGs) – nuestro CLI para modelos de implementación de administración de recursos y clásico Hola</span><span class="sxs-lookup"><span data-stu-id="30a62-106">[Azure CLI 1.0](#View-existing-NSGs) – our CLI for hello classic and resource management deployment models</span></span> 
- <span data-ttu-id="30a62-107">[Azure 2.0 CLI](virtual-network-manage-nsg-arm-cli.md) -nuestro CLI de próxima generación para el modelo de implementación de administración de recursos de hello (en este artículo)</span><span class="sxs-lookup"><span data-stu-id="30a62-107">[Azure CLI 2.0](virtual-network-manage-nsg-arm-cli.md) - our next generation CLI for hello resource management deployment model (this article)</span></span>

[!INCLUDE [virtual-network-manage-nsg-intro-include.md](../../includes/virtual-network-manage-nsg-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="30a62-108">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="30a62-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="30a62-109">Este artículo incluye el uso de modelo de implementación de administrador de recursos de hello, que Microsoft recomienda para la mayoría de las nueva implementaciones en lugar del modelo de implementación clásica de Hola.</span><span class="sxs-lookup"><span data-stu-id="30a62-109">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello classic deployment model.</span></span>
> 

[!INCLUDE [virtual-network-manage-nsg-arm-scenario-include.md](../../includes/virtual-network-manage-nsg-arm-scenario-include.md)]

[!INCLUDE [azure-cli-prerequisites-include.md](../../includes/azure-cli-prerequisites-include.md)]

## <a name="retrieve-information"></a><span data-ttu-id="30a62-110">Recuperar información</span><span class="sxs-lookup"><span data-stu-id="30a62-110">Retrieve Information</span></span>
<span data-ttu-id="30a62-111">Puede consultar los NSG existentes, recuperar las reglas de un NSG existente y averiguar cuáles son los recursos a los que está asociado un NSG.</span><span class="sxs-lookup"><span data-stu-id="30a62-111">You can view your existing NSGs, retrieve rules for an existing NSG, and find out what resources an NSG is associated to.</span></span>

### <a name="view-existing-nsgs"></a><span data-ttu-id="30a62-112">Consultar los NSG existentes</span><span class="sxs-lookup"><span data-stu-id="30a62-112">View existing NSGs</span></span>
<span data-ttu-id="30a62-113">lista de hello tooview de NSG en un grupo de recursos específico, ejecute hello `azure network nsg list` comando tal y como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="30a62-113">tooview hello list of NSGs in a specific resource group, run hello `azure network nsg list` command as shown below.</span></span>

```azurecli
azure network nsg list --resource-group RG-NSG
```

<span data-ttu-id="30a62-114">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="30a62-114">Expected output:</span></span>

    info:    Executing command network nsg list
    + Getting hello network security groups
    data:    Name          Location
    data:    ------------  --------
    data:    NSG-BackEnd   westus
    data:    NSG-FrontEnd  westus
    info:    network nsg list command OK

### <a name="list-all-rules-for-an-nsg"></a><span data-ttu-id="30a62-115">Mostrar todas las reglas de un NSG</span><span class="sxs-lookup"><span data-stu-id="30a62-115">List all rules for an NSG</span></span>
<span data-ttu-id="30a62-116">reglas de hello tooview de un NSG denominado **front-end de NSG**, hello ejecute `azure network nsg show` comando tal y como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="30a62-116">tooview hello rules of an NSG named **NSG-FrontEnd**, run hello `azure network nsg show` command as shown below.</span></span> 

```azurecli
azure network nsg show --resource-group RG-NSG --name NSG-FrontEnd
```

<span data-ttu-id="30a62-117">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="30a62-117">Expected output:</span></span>

    info:    Executing command network nsg show
    + Looking up hello network security group "NSG-FrontEnd"
    data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd
    data:    Name                            : NSG-FrontEnd
    data:    Type                            : Microsoft.Network/networkSecurityGroups
    data:    Location                        : westus
    data:    Provisioning state              : Succeeded
    data:    Tags                            : displayName=NSG - Front End
    data:    Security group rules:
    data:    Name                           Source IP          Source Port  Destination IP  Destination Port  Protocol  Direction  Access  Priority
    data:    -----------------------------  -----------------  -----------  --------------  ----------------  --------  ---------  ------  --------
    data:    rdp-rule                       Internet           *            *               3389              Tcp       Inbound    Allow   100
    data:    web-rule                       Internet           *            *               80                Tcp       Inbound    Allow   101
    data:    AllowVnetInBound               VirtualNetwork     *            VirtualNetwork  *                 *         Inbound    Allow   65000
    data:    AllowAzureLoadBalancerInBound  AzureLoadBalancer  *            *               *                 *         Inbound    Allow   65001
    data:    DenyAllInBound                 *                  *            *               *                 *         Inbound    Deny    65500
    data:    AllowVnetOutBound              VirtualNetwork     *            VirtualNetwork  *                 *         Outbound   Allow   65000
    data:    AllowInternetOutBound          *                  *            Internet        *                 *         Outbound   Allow   65001
    data:    DenyAllOutBound                *                  *            *               *                 *         Outbound   Deny    65500
    info:    network nsg show command OK

> [!NOTE]
> <span data-ttu-id="30a62-118">También puede usar `azure network nsg rule list --resource-group RG-NSG --nsg-name NSG-FrontEnd` reglas de hello toolist de hello **front-end de NSG** NSG.</span><span class="sxs-lookup"><span data-stu-id="30a62-118">You can also use `azure network nsg rule list --resource-group RG-NSG --nsg-name NSG-FrontEnd` toolist hello rules from hello **NSG-FrontEnd** NSG.</span></span>
>

### <a name="view-nsg-associations"></a><span data-ttu-id="30a62-119">Consultar las asociaciones de NSG</span><span class="sxs-lookup"><span data-stu-id="30a62-119">View NSG associations</span></span>

<span data-ttu-id="30a62-120">tooview qué Hola recursos **front-end de NSG** NSG está asociado con la, ejecute hello `azure network nsg show` comando tal y como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="30a62-120">tooview what resources hello **NSG-FrontEnd** NSG is associate with, run hello `azure network nsg show` command as shown below.</span></span> <span data-ttu-id="30a62-121">Tenga en cuenta que Hola solo diferencia es el uso de Hola de hello **--json** parámetro.</span><span class="sxs-lookup"><span data-stu-id="30a62-121">Notice that hello only difference is hello use of hello **--json** parameter.</span></span>

```azurecli
azure network nsg show --resource-group RG-NSG --name NSG-FrontEnd --json
```

<span data-ttu-id="30a62-122">Busque hello **networkInterfaces** y **subredes** propiedades tal y como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="30a62-122">Look for hello **networkInterfaces** and **subnets** properties as shown below:</span></span>

    "networkInterfaces": [],
    ...
    "subnets": [
        {
            "id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd"
        }
    ],
    ...

<span data-ttu-id="30a62-123">En el ejemplo de Hola anterior, hello NSG no está asociado tooany interfaces de red (NIC) y es subred tooa asociado con el nombre **front-end**.</span><span class="sxs-lookup"><span data-stu-id="30a62-123">In hello example above, hello NSG is not associated tooany network interfaces (NICs), and it is associated tooa subnet named **FrontEnd**.</span></span>

## <a name="manage-rules"></a><span data-ttu-id="30a62-124">Administrar las reglas</span><span class="sxs-lookup"><span data-stu-id="30a62-124">Manage rules</span></span>
<span data-ttu-id="30a62-125">Puede agregar tooan de reglas existente NSG, editar las reglas existentes y quitar las reglas.</span><span class="sxs-lookup"><span data-stu-id="30a62-125">You can add rules tooan existing NSG, edit existing rules, and remove rules.</span></span>

### <a name="add-a-rule"></a><span data-ttu-id="30a62-126">Agregar una regla</span><span class="sxs-lookup"><span data-stu-id="30a62-126">Add a rule</span></span>
<span data-ttu-id="30a62-127">tooadd una regla que permite **entrada** tráfico tooport **443** desde cualquier máquina toohello **front-end de NSG** NSG, escriba el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="30a62-127">tooadd a rule allowing **inbound** traffic tooport **443** from any machine toohello **NSG-FrontEnd** NSG, enter hello following command:</span></span>

```azurecli
azure network nsg rule create --resource-group RG-NSG \
    --nsg-name NSG-FrontEnd \
    --name allow-https \
    --description "Allow access tooport 443 for HTTPS" \
    --protocol Tcp \
    --source-address-prefix * \
    --source-port-range * \
    --destination-address-prefix * \
    --destination-port-range 443 \
    --access Allow \
    --priority 102 \
    --direction Inbound
```

<span data-ttu-id="30a62-128">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="30a62-128">Expected output:</span></span>

    info:    Executing command network nsg rule create
    + Looking up hello network security rule "allow-https"
    + Creating a network security rule "allow-https"
    + Looking up hello network security group "NSG-FrontEnd"
    data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/allow-https
    data:    Name                            : allow-https
    data:    Type                            : Microsoft.Network/networkSecurityGroups/securityRules
    data:    Provisioning state              : Succeeded
    data:    Description                     : Allow access tooport 443 for HTTPS
    data:    Source IP                       : *
    data:    Source Port                     : *
    data:    Destination IP                  : *
    data:    Destination Port                : 443
    data:    Protocol                        : Tcp
    data:    Direction                       : Inbound
    data:    Access                          : Allow
    data:    Priority                        : 102
    info:    network nsg rule create command OK

### <a name="change-a-rule"></a><span data-ttu-id="30a62-129">Cambiar una regla</span><span class="sxs-lookup"><span data-stu-id="30a62-129">Change a rule</span></span>
<span data-ttu-id="30a62-130">regla de hello toochange creada anteriormente tooallow el tráfico entrante desde hello **Internet** único, ejecute hello comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="30a62-130">toochange hello rule created above tooallow inbound traffic from hello **Internet** only, run hello following command:</span></span>

```azurecli
azure network nsg rule set --resource-group RG-NSG \
    --nsg-name NSG-FrontEnd \
    --name allow-https \
    --source-address-prefix Internet
```

<span data-ttu-id="30a62-131">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="30a62-131">Expected output:</span></span>

    info:    Executing command network nsg rule set
    + Looking up hello network security group "NSG-FrontEnd"
    + Setting a network security rule "allow-https"
    + Looking up hello network security group "NSG-FrontEnd"
    data:    Id                              : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/allow-https
    data:    Name                            : allow-https
    data:    Type                            : Microsoft.Network/networkSecurityGroups/securityRules
    data:    Provisioning state              : Succeeded
    data:    Description                     : Allow access tooport 443 for HTTPS
    data:    Source IP                       : Internet
    data:    Source Port                     : *
    data:    Destination IP                  : *
    data:    Destination Port                : 443
    data:    Protocol                        : Tcp
    data:    Direction                       : Inbound
    data:    Access                          : Allow
    data:    Priority                        : 102
    info:    network nsg rule set command OK

### <a name="delete-a-rule"></a><span data-ttu-id="30a62-132">Eliminar una regla</span><span class="sxs-lookup"><span data-stu-id="30a62-132">Delete a rule</span></span>
<span data-ttu-id="30a62-133">regla de hello toodelete creada anteriormente, ejecute el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="30a62-133">toodelete hello rule created above, run hello following command:</span></span>

```azurecli
azure network nsg rule delete --resource-group RG-NSG \
    --nsg-name NSG-FrontEnd \
    --name allow-https \
    --quiet
```

> [!NOTE]
> <span data-ttu-id="30a62-134">Hola `--quiet` parámetro garantiza la eliminación de hello tooconfirm no es necesario.</span><span class="sxs-lookup"><span data-stu-id="30a62-134">hello `--quiet` parameter ensures you don't need tooconfirm hello deletion.</span></span>
>

<span data-ttu-id="30a62-135">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="30a62-135">Expected output:</span></span>

    info:    Executing command network nsg rule delete
    + Looking up hello network security group "NSG-FrontEnd"
    + Deleting network security rule "allow-https"
    info:    network nsg rule delete command OK

## <a name="manage-associations"></a><span data-ttu-id="30a62-136">Administrar las asociaciones</span><span class="sxs-lookup"><span data-stu-id="30a62-136">Manage associations</span></span>
<span data-ttu-id="30a62-137">Puede asociar un NSG toosubnets y NIC.</span><span class="sxs-lookup"><span data-stu-id="30a62-137">You can associate an NSG toosubnets and NICs.</span></span> <span data-ttu-id="30a62-138">También puede desasociar un NSG de cualquier recurso al que está asociado.</span><span class="sxs-lookup"><span data-stu-id="30a62-138">You can also dissociate an NSG from any resource it's associated to.</span></span>

### <a name="associate-an-nsg-tooa-nic"></a><span data-ttu-id="30a62-139">Asociar una NIC de NSG tooa</span><span class="sxs-lookup"><span data-stu-id="30a62-139">Associate an NSG tooa NIC</span></span>
<span data-ttu-id="30a62-140">Hola tooassociate **front-end de NSG** NSG toohello **TestNICWeb1** NIC, ejecute el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="30a62-140">tooassociate hello **NSG-FrontEnd** NSG toohello **TestNICWeb1** NIC, run hello following command:</span></span>

```azurecli
azure network nic set --resource-group RG-NSG \
    --name TestNICWeb1 \
    --network-security-group-name NSG-FrontEnd
```

<span data-ttu-id="30a62-141">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="30a62-141">Expected output:</span></span>

    info:    Executing command network nic set
    + Looking up hello network interface "TestNICWeb1"
    + Looking up hello network security group "NSG-FrontEnd"
    + Updating network interface "TestNICWeb1"
    + Looking up hello network interface "TestNICWeb1"
    data:    Id                              : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1
    data:    Name                            : TestNICWeb1
    data:    Type                            : Microsoft.Network/networkInterfaces
    data:    Location                        : westus
    data:    Provisioning state              : Succeeded
    data:    MAC address                     : 00-0D-3A-30-A1-F8
    data:    Enable IP forwarding            : false
    data:    Tags                            : displayName=NetworkInterfaces - Web
    data:    Network security group          : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd
    data:    Virtual machine                 : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/RG-NSG/providers/Microsoft.Compute/virtualMachines/Web1
    data:    IP configurations:
    data:      Name                          : ipconfig1
    data:      Provisioning state            : Succeeded
    data:      Public IP address             : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/RG-NSG/providers/Microsoft.Network/publicIPAddresses/TestPIPWeb1
    data:      Private IP address            : 192.168.1.5
    data:      Private IP Allocation Method  : Dynamic
    data:      Subnet                        : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd
    data:
    info:    network nic set command OK

### <a name="dissociate-an-nsg-from-a-nic"></a><span data-ttu-id="30a62-142">Desasociar un NSG de una NIC</span><span class="sxs-lookup"><span data-stu-id="30a62-142">Dissociate an NSG from a NIC</span></span>

<span data-ttu-id="30a62-143">Hola toodissociate **front-end de NSG** NSG de hello **TestNICWeb1** NIC, ejecute el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="30a62-143">toodissociate hello **NSG-FrontEnd** NSG from hello **TestNICWeb1** NIC, run hello following command:</span></span>

```azurecli
azure network nic set --resource-group RG-NSG --name TestNICWeb1 --network-security-group-id ""
```

> [!NOTE]
> <span data-ttu-id="30a62-144">Hola de aviso "" (vacío) valor de hello `network-security-group-id` parámetro.</span><span class="sxs-lookup"><span data-stu-id="30a62-144">Notice hello "" (empty) value for hello `network-security-group-id` parameter.</span></span> <span data-ttu-id="30a62-145">Es cómo quitar un NSG de tooan de asociación.</span><span class="sxs-lookup"><span data-stu-id="30a62-145">That is how you remove an association tooan NSG.</span></span> <span data-ttu-id="30a62-146">No puede hacer Hola igual con hello `network-security-group-name` parámetro.</span><span class="sxs-lookup"><span data-stu-id="30a62-146">You can't do hello same with hello `network-security-group-name` parameter.</span></span>
> 

<span data-ttu-id="30a62-147">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="30a62-147">Expected result:</span></span>

    info:    Executing command network nic set
    + Looking up hello network interface "TestNICWeb1"
    + Updating network interface "TestNICWeb1"
    + Looking up hello network interface "TestNICWeb1"
    data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1
    data:    Name                            : TestNICWeb1
    data:    Type                            : Microsoft.Network/networkInterfaces
    data:    Location                        : westus
    data:    Provisioning state              : Succeeded
    data:    MAC address                     : 00-0D-3A-30-A1-F8
    data:    Enable IP forwarding            : false
    data:    Tags                            : displayName=NetworkInterfaces - Web
    data:    Virtual machine                 : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Compute/virtualMachines/Web1
    data:    IP configurations:
    data:      Name                          : ipconfig1
    data:      Provisioning state            : Succeeded
    data:      Public IP address             : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/publicIPAddresses/TestPIPWeb1
    data:      Private IP address            : 192.168.1.5
    data:      Private IP Allocation Method  : Dynamic
    data:      Subnet                        : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd
    data:
    info:    network nic set command OK

### <a name="dissociate-an-nsg-from-a-subnet"></a><span data-ttu-id="30a62-148">Desasociar un NSG de una subred</span><span class="sxs-lookup"><span data-stu-id="30a62-148">Dissociate an NSG from a subnet</span></span>
<span data-ttu-id="30a62-149">Hola toodissociate **front-end de NSG** NSG de hello **front-end** subred, ejecute el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="30a62-149">toodissociate hello **NSG-FrontEnd** NSG from hello **FrontEnd** subnet, run hello following command:</span></span>

```azurecli
azure network vnet subnet set --resource-group RG-NSG \
    --vnet-name TestVNet \
    --name FrontEnd \
    --network-security-group-id ""
```

<span data-ttu-id="30a62-150">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="30a62-150">Expected output:</span></span>

    info:    Executing command network vnet subnet set
    + Looking up hello subnet "FrontEnd"
    + Setting subnet "FrontEnd"
    + Looking up hello subnet "FrontEnd"
    data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd
    data:    Type                            : Microsoft.Network/virtualNetworks/subnets
    data:    ProvisioningState               : Succeeded
    data:    Name                            : FrontEnd
    data:    Address prefix                  : 192.168.1.0/24
    data:    IP configurations:
    data:      /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb2/ipConfigurations/ipconfig1
    data:      /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1/ipConfigurations/ipconfig1
    data:
    info:    network vnet subnet set command OK

### <a name="associate-an-nsg-tooa-subnet"></a><span data-ttu-id="30a62-151">Asociar una subred de tooa NSG</span><span class="sxs-lookup"><span data-stu-id="30a62-151">Associate an NSG tooa subnet</span></span>
<span data-ttu-id="30a62-152">Hola tooassociate **front-end de NSG** NSG toohello **FronEnd** subred nuevo, ejecute hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="30a62-152">tooassociate hello **NSG-FrontEnd** NSG toohello **FronEnd** subnet again, run hello following command:</span></span>

```azurecli
azure network vnet subnet set --resource-group RG-NSG \
    --vnet-name TestVNet \
    --name FrontEnd \
    --network-security-group-name NSG-FronEnd
```

> [!NOTE]
> <span data-ttu-id="30a62-153">Hello comando anterior solo funciona porque hello **front-end de NSG** NSG está Hola mismo grupo de recursos como la red virtual de hello **TestVNet**.</span><span class="sxs-lookup"><span data-stu-id="30a62-153">hello command above only works because hello **NSG-FrontEnd** NSG is in hello same resource group as hello virtual network **TestVNet**.</span></span> <span data-ttu-id="30a62-154">Si hello NSG está en otro grupo de recursos, debe toouse hello `--network-security-group-id` parámetro en su lugar y proporcione el identificador completo de Hola para hello NSG.</span><span class="sxs-lookup"><span data-stu-id="30a62-154">If hello NSG is in a different resource group, you need toouse hello `--network-security-group-id` parameter instead, and provide hello full id for hello NSG.</span></span> <span data-ttu-id="30a62-155">Puede recuperar el Id. de hello ejecutando `azure network nsg show --resource-group RG-NSG --name NSG-FrontEnd --json` y buscando hello **identificador** propiedad.</span><span class="sxs-lookup"><span data-stu-id="30a62-155">You can retrieve hello id by running `azure network nsg show --resource-group RG-NSG --name NSG-FrontEnd --json` and looking for hello **id** property.</span></span> 
> 

<span data-ttu-id="30a62-156">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="30a62-156">Expected output:</span></span>

        info:    Executing command network vnet subnet set
        + Looking up hello subnet "FrontEnd"
        + Looking up hello network security group "NSG-FrontEnd"
        + Setting subnet "FrontEnd"
        + Looking up hello subnet "FrontEnd"
        data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd
        data:    Type                            : Microsoft.Network/virtualNetworks/subnets
        data:    ProvisioningState               : Succeeded
        data:    Name                            : FrontEnd
        data:    Address prefix                  : 192.168.1.0/24
        data:    Network security group          : [object Object]
        data:    IP configurations:
        data:      /subscriptions/[Subscription Id]resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb2/ipConfigurations/ipconfig1
        data:      /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1/ipConfigurations/ipconfig1
        data:
        info:    network vnet subnet set command OK

## <a name="delete-an-nsg"></a><span data-ttu-id="30a62-157">Eliminación de un grupo de seguridad de red</span><span class="sxs-lookup"><span data-stu-id="30a62-157">Delete an NSG</span></span>
<span data-ttu-id="30a62-158">Sólo se puede eliminar un NSG si no tiene asociados recursos tooany.</span><span class="sxs-lookup"><span data-stu-id="30a62-158">You can only delete an NSG if it's not associated tooany resource.</span></span> <span data-ttu-id="30a62-159">toodelete un NSG, siga estos pasos Hola.</span><span class="sxs-lookup"><span data-stu-id="30a62-159">toodelete an NSG, follow hello steps below.</span></span>

1. <span data-ttu-id="30a62-160">los recursos de hello toocheck asociados tooan NSG, ejecute hello `azure network nsg show` tal y como se muestra en [NSG vista asociaciones](#View-NSGs-associations).</span><span class="sxs-lookup"><span data-stu-id="30a62-160">toocheck hello resources associated tooan NSG, run hello `azure network nsg show` as shown in [View NSGs associations](#View-NSGs-associations).</span></span>
2. <span data-ttu-id="30a62-161">Si hello NSG está asociado tooany NIC, ejecute hello `azure network nic set` tal y como se muestra en [desasociar un NSG de una NIC](#Dissociate-an-NSG-from-a-NIC) para cada NIC.</span><span class="sxs-lookup"><span data-stu-id="30a62-161">If hello NSG is associated tooany NICs, run hello `azure network nic set` as shown in [Dissociate an NSG from a NIC](#Dissociate-an-NSG-from-a-NIC) for each NIC.</span></span> 
3. <span data-ttu-id="30a62-162">Si hello NSG está asociado tooany subred, ejecute hello `azure network vnet subnet set` tal y como se muestra en [desasociar un NSG de subred](#Dissociate-an-NSG-from-a-subnet) para cada subred.</span><span class="sxs-lookup"><span data-stu-id="30a62-162">If hello NSG is associated tooany subnet, run hello `azure network vnet subnet set` as shown in [Dissociate an NSG from a subnet](#Dissociate-an-NSG-from-a-subnet) for each subnet.</span></span>
4. <span data-ttu-id="30a62-163">Hola toodelete NSG, ejecute el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="30a62-163">toodelete hello NSG, run hello following command:</span></span>

    ```azurecli
    azure network nsg delete --resource-group RG-NSG --name NSG-FrontEnd --quiet
    ```

    <span data-ttu-id="30a62-164">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="30a62-164">Expected output:</span></span>

        info:    Executing command network nsg delete
        + Looking up hello network security group "NSG-FrontEnd"
        + Deleting network security group "NSG-FrontEnd"
        info:    network nsg delete command OK

## <a name="next-steps"></a><span data-ttu-id="30a62-165">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="30a62-165">Next steps</span></span>
* <span data-ttu-id="30a62-166">[Habilite el registro](virtual-network-nsg-manage-log.md) para los NSG.</span><span class="sxs-lookup"><span data-stu-id="30a62-166">[Enable logging](virtual-network-nsg-manage-log.md) for NSGs.</span></span>

