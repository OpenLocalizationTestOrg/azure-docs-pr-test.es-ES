---
title: "aaaOpen puertos tooa máquina virtual mediante PowerShell de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooopen un puerto o cree una máquina virtual de Windows de punto de conexión tooyour con modo de implementación de administrador de recursos de Azure de Hola y PowerShell de Azure"
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: cf45f7d8-451a-48ab-8419-730366d54f1e
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 08/21/2017
ms.author: iainfou
ms.openlocfilehash: c1817a0c447ae4ce7a1ce2a1fc6927bedf2dacb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooopen-ports-and-endpoints-tooa-vm-in-azure-using-powershell"></a><span data-ttu-id="72f5c-103">¿Cómo tooopen puertos y los puntos de conexión tooa VM en Azure con PowerShell</span><span class="sxs-lookup"><span data-stu-id="72f5c-103">How tooopen ports and endpoints tooa VM in Azure using PowerShell</span></span>
[!INCLUDE [virtual-machines-common-nsg-quickstart](../../../includes/virtual-machines-common-nsg-quickstart.md)]

## <a name="quick-commands"></a><span data-ttu-id="72f5c-104">Comandos rápidos</span><span class="sxs-lookup"><span data-stu-id="72f5c-104">Quick commands</span></span>
<span data-ttu-id="72f5c-105">Grupo de seguridad de red de toocreate y reglas de ACL tiene [versión más reciente de Hola de PowerShell de Azure instalado](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="72f5c-105">toocreate a Network Security Group and ACL rules you need [hello latest version of Azure PowerShell installed](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="72f5c-106">También puede [realizar estos pasos con el portal de Azure hello](nsg-quickstart-portal.md).</span><span class="sxs-lookup"><span data-stu-id="72f5c-106">You can also [perform these steps using hello Azure portal](nsg-quickstart-portal.md).</span></span>

<span data-ttu-id="72f5c-107">Inicie sesión en tooyour cuenta de Azure:</span><span class="sxs-lookup"><span data-stu-id="72f5c-107">Log in tooyour Azure account:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="72f5c-108">En hello en los ejemplos siguientes, reemplace los nombres de parámetros de ejemplo con sus propios valores.</span><span class="sxs-lookup"><span data-stu-id="72f5c-108">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="72f5c-109">Los nombres de parámetro de ejemplo incluían *myResourceGroup*, *myNetworkSecurityGroup* y *myVnet*.</span><span class="sxs-lookup"><span data-stu-id="72f5c-109">Example parameter names included *myResourceGroup*, *myNetworkSecurityGroup*, and *myVnet*.</span></span>

<span data-ttu-id="72f5c-110">Creación de una regla con [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig).</span><span class="sxs-lookup"><span data-stu-id="72f5c-110">Create a rule with [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig).</span></span> <span data-ttu-id="72f5c-111">Hello en el ejemplo siguiente se crea una regla denominada *myNetworkSecurityGroupRule* tooallow *tcp* tráfico en el puerto *80*:</span><span class="sxs-lookup"><span data-stu-id="72f5c-111">hello following example creates a rule named *myNetworkSecurityGroupRule* tooallow *tcp* traffic on port *80*:</span></span>

```powershell
$httprule = New-AzureRmNetworkSecurityRuleConfig `
    -Name "myNetworkSecurityGroupRule" `
    -Description "Allow HTTP" `
    -Access "Allow" `
    -Protocol "Tcp" `
    -Direction "Inbound" `
    -Priority "100" `
    -SourceAddressPrefix "Internet" `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 80
```

<span data-ttu-id="72f5c-112">A continuación, cree el grupo de seguridad de red con [AzureRmNetworkSecurityGroup New](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) y asignar Hola HTTP regla que acaba de crear como sigue.</span><span class="sxs-lookup"><span data-stu-id="72f5c-112">Next, create your Network Security group with [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) and assign hello HTTP rule you just created as follows.</span></span> <span data-ttu-id="72f5c-113">Hello en el ejemplo siguiente se crea un grupo de seguridad de red denominado *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="72f5c-113">hello following example creates a Network Security Group named *myNetworkSecurityGroup*:</span></span>

```powershell
$nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName "myResourceGroup" `
    -Location "EastUS" `
    -Name "myNetworkSecurityGroup" `
    -SecurityRules $httprule
```

<span data-ttu-id="72f5c-114">Ahora vamos a asignar la subred de tooa del grupo de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="72f5c-114">Now let's assign your Network Security Group tooa subnet.</span></span> <span data-ttu-id="72f5c-115">Hello en el ejemplo siguiente se asigna una red virtual existente denominada *myVnet* toohello variable *$vnet* con [AzureRmVirtualNetwork Get](/powershell/module/azurerm.network/get-azurermvirtualnetwork):</span><span class="sxs-lookup"><span data-stu-id="72f5c-115">hello following example assigns an existing virtual network named *myVnet* toohello variable *$vnet* with [Get-AzureRmVirtualNetwork](/powershell/module/azurerm.network/get-azurermvirtualnetwork):</span></span>

```powershell
$vnet = Get-AzureRmVirtualNetwork `
    -ResourceGroupName "myResourceGroup" `
    -Name "myVnet"
```

<span data-ttu-id="72f5c-116">Asocie el grupo de seguridad de red con la subred con [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig).</span><span class="sxs-lookup"><span data-stu-id="72f5c-116">Associate your Network Security Group with your subnet with [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig).</span></span> <span data-ttu-id="72f5c-117">Hello en el ejemplo siguiente se asocia con el nombre de subred de hello *mySubnet* con su grupo de seguridad de red:</span><span class="sxs-lookup"><span data-stu-id="72f5c-117">hello following example associates hello subnet named *mySubnet* with your Network Security Group:</span></span>

```powershell
$subnetPrefix = $vnet.Subnets|?{$_.Name -eq 'mySubnet'}

Set-AzureRmVirtualNetworkSubnetConfig `
    -VirtualNetwork $vnet `
    -Name "mySubnet" `
    -AddressPrefix $subnetPrefix.AddressPrefix `
    -NetworkSecurityGroup $nsg
```

<span data-ttu-id="72f5c-118">Por último, actualizar la red virtual con [AzureRmVirtualNetwork conjunto](/powershell/module/azurerm.network/set-azurermvirtualnetwork) en orden para el efecto de tootake de cambios:</span><span class="sxs-lookup"><span data-stu-id="72f5c-118">Finally, update your virtual network with [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork) in order for your changes tootake effect:</span></span>

```powershell
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```


## <a name="more-information-on-network-security-groups"></a><span data-ttu-id="72f5c-119">Más información sobre los grupos de seguridad de red</span><span class="sxs-lookup"><span data-stu-id="72f5c-119">More information on Network Security Groups</span></span>
<span data-ttu-id="72f5c-120">Hola de comandos rápido aquí le permite tooget seguridad y en ejecución con tooyour del flujo de tráfico máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="72f5c-120">hello quick commands here allow you tooget up and running with traffic flowing tooyour VM.</span></span> <span data-ttu-id="72f5c-121">Grupos de seguridad de red proporcionan muchas características excepcionales y granularidad para controlar acceso a los recursos tooyour.</span><span class="sxs-lookup"><span data-stu-id="72f5c-121">Network Security Groups provide many great features and granularity for controlling access tooyour resources.</span></span> <span data-ttu-id="72f5c-122">Puede leer más sobre la [creación de un grupo de seguridad de red y las reglas de ACL aquí](tutorial-virtual-network.md#manage-internal-traffic).</span><span class="sxs-lookup"><span data-stu-id="72f5c-122">You can read more about [creating a Network Security Group and ACL rules here](tutorial-virtual-network.md#manage-internal-traffic).</span></span>

<span data-ttu-id="72f5c-123">Para las aplicaciones web de alta disponibilidad, debe colocar las máquinas virtuales detrás de una instancia de Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="72f5c-123">For highly available web applications, you should place your VMs behind an Azure Load Balancer.</span></span> <span data-ttu-id="72f5c-124">equilibrador de carga de Hello distribuye el tráfico tooVMs, con un grupo de seguridad de red que proporciona filtrado de tráfico.</span><span class="sxs-lookup"><span data-stu-id="72f5c-124">hello load balancer distributes traffic tooVMs, with a Network Security Group that provides traffic filtering.</span></span> <span data-ttu-id="72f5c-125">Para obtener más información, consulte [cómo equilibrar tooload Linux virtual máquinas en Azure toocreate una aplicación de alta disponibilidad](tutorial-load-balancer.md).</span><span class="sxs-lookup"><span data-stu-id="72f5c-125">For more information, see [How tooload balance Linux virtual machines in Azure toocreate a highly available application](tutorial-load-balancer.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="72f5c-126">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="72f5c-126">Next steps</span></span>
<span data-ttu-id="72f5c-127">En este ejemplo, ha creado el tráfico de tooallow HTTP de una regla sencilla.</span><span class="sxs-lookup"><span data-stu-id="72f5c-127">In this example, you created a simple rule tooallow HTTP traffic.</span></span> <span data-ttu-id="72f5c-128">Puede encontrar información sobre cómo crear entornos más detallados en hello siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="72f5c-128">You can find information on creating more detailed environments in hello following articles:</span></span>

* [<span data-ttu-id="72f5c-129">Información general sobre Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="72f5c-129">Azure Resource Manager overview</span></span>](../../azure-resource-manager/resource-group-overview.md)
* [<span data-ttu-id="72f5c-130">¿Qué es un grupo de seguridad de red?</span><span class="sxs-lookup"><span data-stu-id="72f5c-130">What is a Network Security Group (NSG)?</span></span>](../../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="72f5c-131">Información general de Azure Resource Manager para equilibradores de carga</span><span class="sxs-lookup"><span data-stu-id="72f5c-131">Azure Resource Manager Overview for Load Balancers</span></span>](../../load-balancer/load-balancer-arm.md)

