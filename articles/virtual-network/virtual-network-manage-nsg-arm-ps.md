---
title: aaaManage de red de grupos de seguridad - PowerShell de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toomanage red grupos de seguridad mediante PowerShell."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3706ce6c-d9ae-46cb-a048-f0a4e84dc5cc
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/14/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 930fe5e0827896ad67b24d84e41a5d3f898ba838
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-network-security-groups-using-powershell"></a><span data-ttu-id="90e71-103">Administración de grupos de seguridad de red mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="90e71-103">Manage network security groups using PowerShell</span></span>

[!INCLUDE [virtual-network-manage-arm-selectors-include.md](../../includes/virtual-network-manage-nsg-arm-selectors-include.md)]

[!INCLUDE [virtual-network-manage-nsg-intro-include.md](../../includes/virtual-network-manage-nsg-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="90e71-104">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="90e71-104">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="90e71-105">Este artículo incluye el uso de modelo de implementación de administrador de recursos de hello, que Microsoft recomienda para la mayoría de las nueva implementaciones en lugar del modelo de implementación clásica de Hola.</span><span class="sxs-lookup"><span data-stu-id="90e71-105">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello classic deployment model.</span></span>
>

[!INCLUDE [virtual-network-manage-nsg-arm-scenario-include.md](../../includes/virtual-network-manage-nsg-arm-scenario-include.md)]

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="retrieve-information"></a><span data-ttu-id="90e71-106">Recuperar información</span><span class="sxs-lookup"><span data-stu-id="90e71-106">Retrieve Information</span></span>
<span data-ttu-id="90e71-107">Puede consultar los NSG existentes, recuperar las reglas de un NSG existente y averiguar cuáles son los recursos a los que está asociado un NSG.</span><span class="sxs-lookup"><span data-stu-id="90e71-107">You can view your existing NSGs, retrieve rules for an existing NSG, and find out what resources an NSG is associated to.</span></span>

### <a name="view-existing-nsgs"></a><span data-ttu-id="90e71-108">Consultar los NSG existentes</span><span class="sxs-lookup"><span data-stu-id="90e71-108">View existing NSGs</span></span>
<span data-ttu-id="90e71-109">tooview todos los NSG existentes en una suscripción, ejecute hello `Get-AzureRmNetworkSecurityGroup` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="90e71-109">tooview all existing NSGs in a subscription, run hello `Get-AzureRmNetworkSecurityGroup` cmdlet.</span></span>

<span data-ttu-id="90e71-110">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="90e71-110">Expected result:</span></span>

    Name                 : NSG-BackEnd
    ResourceGroupName    : RG-NSG
    Location             : westus
    Id                   : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/
                           Microsoft.Network/networkSecurityGroups/NSG-BackEnd
    Etag                 : W/"[Id]"
    ResourceGuid         : [Id]
    ProvisioningState    : Succeeded
    Tags                 :                            
    SecurityRules        : [...]
    DefaultSecurityRules : [...]
    NetworkInterfaces    : [...]
    Subnets              : [...]

    Name                 : NSG-FrontEnd
    ResourceGroupName    : RG-NSG
    Location             : eastus
    Id                   : /subscriptions/[Subscription Id]/resourceGroups/NRP-RG/providers/
                           Microsoft.Network/networkSecurityGroups/NSG-FrontEnd
    Etag                 : W/"[Id]"
    ResourceGuid         : [Id]
    ProvisioningState    : Succeeded
    Tags                 : 
    SecurityRules        : [...]
    DefaultSecurityRules : [...]
    NetworkInterfaces    : [...]
    Subnets              : [...]

    Name                 : WEB1
    ResourceGroupName    : RG101
    Location             : eastus2
    Id                   : /subscriptions/[Subscription Id]/resourceGroups/RG101/providers/M
                           icrosoft.Network/networkSecurityGroups/WEB1
    Etag                 : W/"[Id]"
    ResourceGuid         : [Id]
    ProvisioningState    : Succeeded
    Tags                 : 
    SecurityRules        : [...]
    DefaultSecurityRules : [...]
    NetworkInterfaces    : [...]
    Subnets              : [...]


<span data-ttu-id="90e71-111">lista de hello tooview de NSG en un grupo de recursos específico, ejecute hello `Get-AzureRmNetworkSecurityGroup` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="90e71-111">tooview hello list of NSGs in a specific resource group, run hello `Get-AzureRmNetworkSecurityGroup` cmdlet.</span></span>

<span data-ttu-id="90e71-112">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="90e71-112">Expected output:</span></span>

    Name                 : NSG-BackEnd
    ResourceGroupName    : RG-NSG
    Location             : westus
    Id                   : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/
                           Microsoft.Network/networkSecurityGroups/NSG-BackEnd
    Etag                 : W/"[Id]"
    ResourceGuid         : [Id]
    ProvisioningState    : Succeeded
    Tags                 :                            
    SecurityRules        : [...]
    DefaultSecurityRules : [...]
    NetworkInterfaces    : [...]
    Subnets              : [...]

    Name                 : NSG-FrontEnd
    ResourceGroupName    : RG-NSG
    Location             : eastus
    Id                   : /subscriptions/[Subscription Id]/resourceGroups/NRP-RG/providers/
                           Microsoft.Network/networkSecurityGroups/NSG-FrontEnd
    Etag                 : W/"[Id]"
    ResourceGuid         : [Id]
    ProvisioningState    : Succeeded
    Tags                 : 
    SecurityRules        : [...]
    DefaultSecurityRules : [...]
    NetworkInterfaces    : [...]
    Subnets              : [...]

### <a name="list-all-rules-for-an-nsg"></a><span data-ttu-id="90e71-113">Mostrar todas las reglas de un NSG</span><span class="sxs-lookup"><span data-stu-id="90e71-113">List all rules for an NSG</span></span>
<span data-ttu-id="90e71-114">reglas de hello tooview de un NSG denominado **front-end de NSG**, escriba el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="90e71-114">tooview hello rules of an NSG named **NSG-FrontEnd**, enter hello following command:</span></span>

```powershell
Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd | Select SecurityRules -ExpandProperty SecurityRules
```

<span data-ttu-id="90e71-115">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="90e71-115">Expected output:</span></span>

    Name                     : rdp-rule
    Id                       : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/                           Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/rdp-rule
    Etag                     : W/"[Id]"
    ProvisioningState        : Succeeded
    Description              : Allow RDP
    Protocol                 : Tcp
    SourcePortRange          : *
    DestinationPortRange     : 3389
    SourceAddressPrefix      : Internet
    DestinationAddressPrefix : *
    Access                   : Allow
    Priority                 : 100
    Direction                : Inbound

    Name                     : web-rule
    Id                       : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/                           Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/web-rule
    Etag                     : W/"[Id]"
    ProvisioningState        : Succeeded
    Description              : Allow HTTP
    Protocol                 : Tcp
    SourcePortRange          : *
    DestinationPortRange     : 80
    SourceAddressPrefix      : Internet
    DestinationAddressPrefix : *
    Access                   : Allow
    Priority                 : 101
    Direction                : Inbound

> [!NOTE]
> <span data-ttu-id="90e71-116">También puede usar `Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name "NSG-FrontEnd" | Select DefaultSecurityRules -ExpandProperty DefaultSecurityRules` las reglas predeterminadas de toolist Hola de hello **front-end de NSG** NSG.</span><span class="sxs-lookup"><span data-stu-id="90e71-116">You can also use `Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name "NSG-FrontEnd" | Select DefaultSecurityRules -ExpandProperty DefaultSecurityRules` toolist hello default rules from hello **NSG-FrontEnd** NSG.</span></span>
> 

### <a name="view-nsgs-associations"></a><span data-ttu-id="90e71-117">Consultar las asociaciones de NSG</span><span class="sxs-lookup"><span data-stu-id="90e71-117">View NSGs associations</span></span>
<span data-ttu-id="90e71-118">tooview qué Hola recursos **front-end de NSG** NSG está asociado con la, hello ejecución del siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="90e71-118">tooview what resources hello **NSG-FrontEnd** NSG is associate with, run hello following command:</span></span>

```powershell
Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
```

<span data-ttu-id="90e71-119">Busque hello **NetworkInterfaces** y **subredes** propiedades tal y como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="90e71-119">Look for hello **NetworkInterfaces** and **Subnets** properties as shown below:</span></span>

    NetworkInterfaces    : []
    Subnets              : [
                             {
                               "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                               "IpConfigurations": []
                             }
                           ]

<span data-ttu-id="90e71-120">En el ejemplo anterior de hello, hello NSG no está asociado tooany interfaces de red (NIC); es subred tooa asociado con el nombre **front-end**.</span><span class="sxs-lookup"><span data-stu-id="90e71-120">In hello previous example, hello NSG is not associated tooany network interfaces (NICs); it is associated tooa subnet named **FrontEnd**.</span></span>

## <a name="manage-rules"></a><span data-ttu-id="90e71-121">Administrar las reglas</span><span class="sxs-lookup"><span data-stu-id="90e71-121">Manage rules</span></span>
<span data-ttu-id="90e71-122">Puede agregar tooan de reglas existente NSG, editar las reglas existentes y quitar las reglas.</span><span class="sxs-lookup"><span data-stu-id="90e71-122">You can add rules tooan existing NSG, edit existing rules, and remove rules.</span></span>

### <a name="add-a-rule"></a><span data-ttu-id="90e71-123">Agregar una regla</span><span class="sxs-lookup"><span data-stu-id="90e71-123">Add a rule</span></span>
<span data-ttu-id="90e71-124">tooadd una regla que permite **entrante** tráfico tooport **443** desde cualquier máquina toohello **front-end de NSG** NSG, Hola completa pasos:</span><span class="sxs-lookup"><span data-stu-id="90e71-124">tooadd a rule allowing **inbound** traffic tooport **443** from any machine toohello **NSG-FrontEnd** NSG, complete hello following steps:</span></span>

1. <span data-ttu-id="90e71-125">Comando hello tooretrieve existente NSG siguiente de ejecución hello y almacenarlo en una variable:</span><span class="sxs-lookup"><span data-stu-id="90e71-125">Run hello following command tooretrieve hello existing NSG and store it in a variable:</span></span>

    ```powershell   
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. <span data-ttu-id="90e71-126">Ejecute hello después comando tooadd un NSG de toohello de regla:</span><span class="sxs-lookup"><span data-stu-id="90e71-126">Run hello following command tooadd a rule toohello NSG:</span></span>

    ```powershell
    Add-AzureRmNetworkSecurityRuleConfig -NetworkSecurityGroup $nsg `
    -Name https-rule `
    -Description "Allow HTTPS" `
    -Access Allow `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 102 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 443
    ```

3. <span data-ttu-id="90e71-127">realizado los cambios de hello toosave toohello NSG, ejecute el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="90e71-127">toosave hello changes made toohello NSG, run hello following command:</span></span>

    ```powershell
    Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
    ```
    <span data-ttu-id="90e71-128">Resultado esperado que muestra hello solo las reglas de seguridad:</span><span class="sxs-lookup"><span data-stu-id="90e71-128">Expected output showing only hello security rules:</span></span>
   
        Name                 : NSG-FrontEnd
        ...
        SecurityRules        : [
                                 {
                                   "Name": "rdp-rule",
                                   ...
                                 },
                                 {
                                   "Name": "web-rule",
                                   ...
                                 },
                                 {
                                   "Name": "https-rule",
                                   "Etag": "W/\"[Id]\"",
                                   "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/https-rule",
                                   "Description": "Allow HTTPS",
                                   "Protocol": "Tcp",
                                   "SourcePortRange": "*",
                                   "DestinationPortRange": "443",
                                   "SourceAddressPrefix": "*",
                                   "DestinationAddressPrefix": "*",
                                   "Access": "Allow",
                                   "Priority": 102,
                                   "Direction": "Inbound",
                                   "ProvisioningState": "Succeeded"
                                 }
                               ]

### <a name="change-a-rule"></a><span data-ttu-id="90e71-129">Cambiar una regla</span><span class="sxs-lookup"><span data-stu-id="90e71-129">Change a rule</span></span>
<span data-ttu-id="90e71-130">regla de hello toochange creada anteriormente tooallow el tráfico entrante desde hello **Internet** solo, siga estos pasos Hola.</span><span class="sxs-lookup"><span data-stu-id="90e71-130">toochange hello rule created above tooallow inbound traffic from hello **Internet** only, follow hello steps below.</span></span>

1. <span data-ttu-id="90e71-131">Comando hello tooretrieve existente NSG siguiente de ejecución hello y almacenarlo en una variable:</span><span class="sxs-lookup"><span data-stu-id="90e71-131">Run hello following command tooretrieve hello existing NSG and store it in a variable:</span></span>

    ```powershell 
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. <span data-ttu-id="90e71-132">Ejecute hello siguiente comando con la nueva configuración de la regla de hello:</span><span class="sxs-lookup"><span data-stu-id="90e71-132">Run hello following command with hello new rule settings:</span></span>

    ```powershell
    Set-AzureRmNetworkSecurityRuleConfig -NetworkSecurityGroup $nsg `
    -Name https-rule `
    -Description "Allow HTTPS" `
    -Access Allow `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 102 `
    -SourceAddressPrefix Internet `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 443
    ```

3. <span data-ttu-id="90e71-133">realizado los cambios de hello toosave toohello NSG, ejecute el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="90e71-133">toosave hello changes made toohello NSG, run hello following command:</span></span>

    ```powershell
    Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
    ```

    <span data-ttu-id="90e71-134">Resultado esperado que muestra hello solo las reglas de seguridad:</span><span class="sxs-lookup"><span data-stu-id="90e71-134">Expected output showing only hello security rules:</span></span>
   
        Name                 : NSG-FrontEnd
        ...
        SecurityRules        : [
                                 {
                                   "Name": "rdp-rule",
                                   ...
                                 },
                                 {
                                   "Name": "web-rule",
                                   ...
                                 },
                                 {
                                   "Name": "https-rule",
                                   "Etag": "W/\"[Id]\"",
                                   "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/https-rule",
                                   "Description": "Allow HTTPS",
                                   "Protocol": "Tcp",
                                   "SourcePortRange": "*",
                                   "DestinationPortRange": "443",
                                   "SourceAddressPrefix": "Internet",
                                   "DestinationAddressPrefix": "*",
                                   "Access": "Allow",
                                   "Priority": 102,
                                   "Direction": "Inbound",
                                   "ProvisioningState": "Succeeded"
                                 }
                               ]

### <a name="delete-a-rule"></a><span data-ttu-id="90e71-135">Eliminar una regla</span><span class="sxs-lookup"><span data-stu-id="90e71-135">Delete a rule</span></span>
1. <span data-ttu-id="90e71-136">Comando hello tooretrieve existente NSG siguiente de ejecución hello y almacenarlo en una variable:</span><span class="sxs-lookup"><span data-stu-id="90e71-136">Run hello following command tooretrieve hello existing NSG and store it in a variable:</span></span>

    ```powershell
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. <span data-ttu-id="90e71-137">Ejecute hello siguiendo la regla de comando tooremove Hola de hello NSG:</span><span class="sxs-lookup"><span data-stu-id="90e71-137">Run hello following command tooremove hello rule from hello NSG:</span></span>

    ```powershell
    Remove-AzureRmNetworkSecurityRuleConfig -NetworkSecurityGroup $nsg -Name https-rule
    ```

3. <span data-ttu-id="90e71-138">Guarde los cambios realizados de hello toohello NSG, ejecutando el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="90e71-138">Save hello changes made toohello NSG, by running hello following command:</span></span>

    ```powershell
    Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
    ```

    <span data-ttu-id="90e71-139">Resultado esperado que muestra solo hello las reglas de seguridad, observe hello **regla https** ya no aparece:</span><span class="sxs-lookup"><span data-stu-id="90e71-139">Expected output showing only hello security rules, notice hello **https-rule** is no longer listed:</span></span>
   
        Name                 : NSG-FrontEnd
        ...
        SecurityRules        : [
                                 {
                                   "Name": "rdp-rule",
                                   ...
                                 },
                                 {
                                   "Name": "web-rule",
                                   ...
                                 }
                               ]

## <a name="manage-associations"></a><span data-ttu-id="90e71-140">Administrar las asociaciones</span><span class="sxs-lookup"><span data-stu-id="90e71-140">Manage associations</span></span>
<span data-ttu-id="90e71-141">Puede asociar un NSG toosubnets y NIC.</span><span class="sxs-lookup"><span data-stu-id="90e71-141">You can associate an NSG toosubnets and NICs.</span></span> <span data-ttu-id="90e71-142">También puede desasociar un NSG de cualquier recurso al que está asociado.</span><span class="sxs-lookup"><span data-stu-id="90e71-142">You can also dissociate an NSG from any resource it's associated to.</span></span>

### <a name="associate-an-nsg-tooa-nic"></a><span data-ttu-id="90e71-143">Asociar una NIC de NSG tooa</span><span class="sxs-lookup"><span data-stu-id="90e71-143">Associate an NSG tooa NIC</span></span>
<span data-ttu-id="90e71-144">Hola tooassociate **front-end de NSG** NSG toohello **TestNICWeb1** NIC, Hola completa pasos:</span><span class="sxs-lookup"><span data-stu-id="90e71-144">tooassociate hello **NSG-FrontEnd** NSG toohello **TestNICWeb1** NIC, complete hello following steps:</span></span>

1. <span data-ttu-id="90e71-145">Comando hello tooretrieve existente NSG siguiente de ejecución hello y almacenarlo en una variable:</span><span class="sxs-lookup"><span data-stu-id="90e71-145">Run hello following command tooretrieve hello existing NSG and store it in a variable:</span></span>

    ```powershell
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. <span data-ttu-id="90e71-146">Comando hello tooretrieve existente NIC siguiente de ejecución hello y almacenarlo en una variable:</span><span class="sxs-lookup"><span data-stu-id="90e71-146">Run hello following command tooretrieve hello existing NIC and store it in a variable:</span></span>

    ```powershell
    $nic = Get-AzureRmNetworkInterface -ResourceGroupName RG-NSG -Name TestNICWeb1
    ```

3. <span data-ttu-id="90e71-147">Conjunto hello **grupos** propiedad de hello **NIC** valor toohello variable del programa Hola a **NSG** variable, escribiendo el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="90e71-147">Set hello **NetworkSecurityGroup** property of hello **NIC** variable toohello value of hello **NSG** variable, by entering hello following command:</span></span>

    ```powershell
    $nic.NetworkSecurityGroup = $nsg
    ```

4. <span data-ttu-id="90e71-148">realizado los cambios de hello toosave toohello NIC, ejecute el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="90e71-148">toosave hello changes made toohello NIC, run hello following command:</span></span>

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $nic
    ```
   
    <span data-ttu-id="90e71-149">Hola de resultado esperado que se muestra solo **grupos** propiedad:</span><span class="sxs-lookup"><span data-stu-id="90e71-149">Expected output showing only hello **NetworkSecurityGroup** property:</span></span>
   
        NetworkSecurityGroup : {
                                 "SecurityRules": [],
                                 "DefaultSecurityRules": [],
                                 "NetworkInterfaces": [],
                                 "Subnets": [],
                                 "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd"
                               }

### <a name="dissociate-an-nsg-from-a-nic"></a><span data-ttu-id="90e71-150">Desasociar un NSG de una NIC</span><span class="sxs-lookup"><span data-stu-id="90e71-150">Dissociate an NSG from a NIC</span></span>
<span data-ttu-id="90e71-151">Hola toodissociate **front-end de NSG** NSG de hello **TestNICWeb1** NIC, Hola completa pasos:</span><span class="sxs-lookup"><span data-stu-id="90e71-151">toodissociate hello **NSG-FrontEnd** NSG from hello **TestNICWeb1** NIC, complete hello following steps:</span></span>

1. <span data-ttu-id="90e71-152">Comando hello tooretrieve existente NIC siguiente de ejecución hello y almacenarlo en una variable:</span><span class="sxs-lookup"><span data-stu-id="90e71-152">Run hello following command tooretrieve hello existing NIC and store it in a variable:</span></span>

    ```powershell
    $nic = Get-AzureRmNetworkInterface -ResourceGroupName RG-NSG -Name TestNICWeb1
    ```

2. <span data-ttu-id="90e71-153">Conjunto hello **grupos** propiedad de hello **NIC** variable demasiado**$null** ejecutando el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="90e71-153">Set hello **NetworkSecurityGroup** property of hello **NIC** variable too**$null** by running hello following command:</span></span>

    ```powershell
    $nic.NetworkSecurityGroup = $null
    ```

3. <span data-ttu-id="90e71-154">realizado los cambios de hello toosave toohello NIC, ejecute el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="90e71-154">toosave hello changes made toohello NIC, run hello following command:</span></span>

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $nic
    ```
   
    <span data-ttu-id="90e71-155">Hola de resultado esperado que se muestra solo **grupos** propiedad:</span><span class="sxs-lookup"><span data-stu-id="90e71-155">Expected output showing only hello **NetworkSecurityGroup** property:</span></span>
   
        NetworkSecurityGroup : null

### <a name="dissociate-an-nsg-from-a-subnet"></a><span data-ttu-id="90e71-156">Desasociar un NSG de una subred</span><span class="sxs-lookup"><span data-stu-id="90e71-156">Dissociate an NSG from a subnet</span></span>
<span data-ttu-id="90e71-157">Hola toodissociate **front-end de NSG** NSG de hello **front-end** subred, Hola completa pasos:</span><span class="sxs-lookup"><span data-stu-id="90e71-157">toodissociate hello **NSG-FrontEnd** NSG from hello **FrontEnd** subnet, complete hello following steps:</span></span>

1. <span data-ttu-id="90e71-158">Ejecute hello después comando tooretrieve hello existente de la red virtual y almacenarla en una variable:</span><span class="sxs-lookup"><span data-stu-id="90e71-158">Run hello following command tooretrieve hello existing VNet and store it in a variable:</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName RG-NSG -Name TestVNet
    ```

2. <span data-ttu-id="90e71-159">Ejecución hello siguientes comando tooretrieve hello **front-end** subred y almacenarlo en una variable:</span><span class="sxs-lookup"><span data-stu-id="90e71-159">Run hello following command tooretrieve hello **FrontEnd** subnet and store it in a variable:</span></span>

    ```powershell
    $subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd
    ```
 
3. <span data-ttu-id="90e71-160">Conjunto hello **grupos** propiedad de hello **subred** variable demasiado**$null** escribiendo el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="90e71-160">Set hello **NetworkSecurityGroup** property of hello **subnet** variable too**$null** by entering hello following command:</span></span>

    ```powershell
    $subnet.NetworkSecurityGroup = $null
    ```

4. <span data-ttu-id="90e71-161">realizan cambios de hello toosave toohello subred, ejecute el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="90e71-161">toosave hello changes made toohello subnet, run hello following command:</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

    <span data-ttu-id="90e71-162">Resultado esperado que muestran solo Hola propiedades de hello **front-end** subred.</span><span class="sxs-lookup"><span data-stu-id="90e71-162">Expected output showing only hello properties of hello **FrontEnd** subnet.</span></span> <span data-ttu-id="90e71-163">Observe que no hay una propiedad para **NetworkSecurityGroup**:</span><span class="sxs-lookup"><span data-stu-id="90e71-163">Notice there isn't a property for **NetworkSecurityGroup**:</span></span>
   
            ...
            Subnets           : [
                                  {
                                    "Name": "FrontEnd",
                                    "Etag": "W/\"[Id]\"",
                                    "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                                    "AddressPrefix": "192.168.1.0/24",
                                    "IpConfigurations": [
                                      {
                                        "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb2/ipConfigurations/ipconfig1"
                                      },
                                      {
                                        "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1/ipConfigurations/ipconfig1"
                                      }
                                    ],
                                    "ProvisioningState": "Succeeded"
                                  },
                                    ...
                                ]

### <a name="associate-an-nsg-tooa-subnet"></a><span data-ttu-id="90e71-164">Asociar una subred de tooa NSG</span><span class="sxs-lookup"><span data-stu-id="90e71-164">Associate an NSG tooa subnet</span></span>
<span data-ttu-id="90e71-165">Hola tooassociate **front-end de NSG** NSG toohello **FronEnd** subred nuevo, completa Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="90e71-165">tooassociate hello **NSG-FrontEnd** NSG toohello **FronEnd** subnet again, complete hello following steps:</span></span>

1. <span data-ttu-id="90e71-166">Ejecute hello después comando tooretrieve hello existente de la red virtual y almacenarla en una variable:</span><span class="sxs-lookup"><span data-stu-id="90e71-166">Run hello following command tooretrieve hello existing VNet and store it in a variable:</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName RG-NSG -Name TestVNet
    ```

2. <span data-ttu-id="90e71-167">Ejecución hello siguientes comando tooretrieve hello **front-end** subred y almacenarlo en una variable:</span><span class="sxs-lookup"><span data-stu-id="90e71-167">Run hello following command tooretrieve hello **FrontEnd** subnet and store it in a variable:</span></span>

    ```powershell
    $subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd
    ```
 
3. <span data-ttu-id="90e71-168">Comando hello tooretrieve existente NSG siguiente de ejecución hello y almacenarlo en una variable:</span><span class="sxs-lookup"><span data-stu-id="90e71-168">Run hello following command tooretrieve hello existing NSG and store it in a variable:</span></span>

    ```powershell
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

4. <span data-ttu-id="90e71-169">Conjunto hello **grupos** propiedad de hello **subred** variable demasiado**$null** ejecutando el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="90e71-169">Set hello **NetworkSecurityGroup** property of hello **subnet** variable too**$null** by running hello following command:</span></span>

    ```powershell
    $subnet.NetworkSecurityGroup = $nsg
    ```

5. <span data-ttu-id="90e71-170">realizan cambios de hello toosave toohello subred, ejecute el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="90e71-170">toosave hello changes made toohello subnet, run hello following command:</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

    <span data-ttu-id="90e71-171">Hola de resultado esperado que se muestra solo **grupos** propiedad de hello **front-end** subred:</span><span class="sxs-lookup"><span data-stu-id="90e71-171">Expected output showing only hello **NetworkSecurityGroup** property of hello **FrontEnd** subnet:</span></span>
   
        ...
        "NetworkSecurityGroup": {
                                  "SecurityRules": [],
                                  "DefaultSecurityRules": [],
                                  "NetworkInterfaces": [],
                                  "Subnets": [],
                                  "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd"
                                }
        ...

## <a name="delete-an-nsg"></a><span data-ttu-id="90e71-172">Eliminación de un grupo de seguridad de red</span><span class="sxs-lookup"><span data-stu-id="90e71-172">Delete an NSG</span></span>
<span data-ttu-id="90e71-173">Sólo se puede eliminar un NSG si no tiene asociados recursos tooany.</span><span class="sxs-lookup"><span data-stu-id="90e71-173">You can only delete an NSG if it's not associated tooany resource.</span></span> <span data-ttu-id="90e71-174">toodelete un NSG, siga estos pasos Hola.</span><span class="sxs-lookup"><span data-stu-id="90e71-174">toodelete an NSG, follow hello steps below.</span></span>

1. <span data-ttu-id="90e71-175">los recursos de hello toocheck asociados tooan NSG, ejecute hello `azure network nsg show` tal y como se muestra en [NSG vista asociaciones](#View-NSGs-associations).</span><span class="sxs-lookup"><span data-stu-id="90e71-175">toocheck hello resources associated tooan NSG, run hello `azure network nsg show` as shown in [View NSGs associations](#View-NSGs-associations).</span></span>
2. <span data-ttu-id="90e71-176">Si hello NSG está asociado tooany NIC, ejecute hello `azure network nic set` tal y como se muestra en [desasociar un NSG de una NIC](#Dissociate-an-NSG-from-a-NIC) para cada NIC.</span><span class="sxs-lookup"><span data-stu-id="90e71-176">If hello NSG is associated tooany NICs, run hello `azure network nic set` as shown in [Dissociate an NSG from a NIC](#Dissociate-an-NSG-from-a-NIC) for each NIC.</span></span> 
3. <span data-ttu-id="90e71-177">Si hello NSG está asociado tooany subred, ejecute hello `azure network vnet subnet set` tal y como se muestra en [desasociar un NSG de subred](#Dissociate-an-NSG-from-a-subnet) para cada subred.</span><span class="sxs-lookup"><span data-stu-id="90e71-177">If hello NSG is associated tooany subnet, run hello `azure network vnet subnet set` as shown in [Dissociate an NSG from a subnet](#Dissociate-an-NSG-from-a-subnet) for each subnet.</span></span>
4. <span data-ttu-id="90e71-178">Hola toodelete NSG, ejecute el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="90e71-178">toodelete hello NSG, run hello following command:</span></span>

    ```powershell
    Remove-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd -Force
    ```
   
   > [!NOTE]
   > <span data-ttu-id="90e71-179">Hola `-Force` parámetro garantiza la eliminación de hello tooconfirm no es necesario.</span><span class="sxs-lookup"><span data-stu-id="90e71-179">hello `-Force` parameter ensures you don't need tooconfirm hello deletion.</span></span>
   > 

## <a name="next-steps"></a><span data-ttu-id="90e71-180">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="90e71-180">Next steps</span></span>
* <span data-ttu-id="90e71-181">[Habilite el registro](virtual-network-nsg-manage-log.md) para los NSG.</span><span class="sxs-lookup"><span data-stu-id="90e71-181">[Enable logging](virtual-network-nsg-manage-log.md) for NSGs.</span></span>

