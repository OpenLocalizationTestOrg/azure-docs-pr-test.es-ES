---
title: "Ejemplo de script de Azure PowerShell: crear una red para aplicaciones de niveles múltiples | Microsoft Docs"
description: "Ejemplo de script de Azure PowerShell: crear una red virtual para aplicaciones de niveles múltiples."
services: virtual-network
documentationcenter: virtual-network
author: georgewallace
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: powershell
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 05/16/2017
ms.author: gwallace
ms.openlocfilehash: ab49e78ef17b093d2bbe4e3276a1ece3a4247f91
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-network-for-multi-tier-applications"></a><span data-ttu-id="86a2c-103">Creación de una red para aplicaciones de niveles múltiples</span><span class="sxs-lookup"><span data-stu-id="86a2c-103">Create a network for multi-tier applications</span></span>

<span data-ttu-id="86a2c-104">Este ejemplo de script crea una red virtual con subredes de front-end y back-end.</span><span class="sxs-lookup"><span data-stu-id="86a2c-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="86a2c-105">El tráfico a la subred de front-end está limitado a HTTP y SSH, mientras que el tráfico a la subred de back-end está limitado a MySQL, al puerto 3306.</span><span class="sxs-lookup"><span data-stu-id="86a2c-105">Traffic to the front-end subnet is limited to HTTP and SSH, while traffic to the back-end subnet is limited to MySQL, port 3306.</span></span> <span data-ttu-id="86a2c-106">Después de ejecutar el script, tendrá dos máquinas virtuales, una en cada subred en la que puede implementar el servidor web y el software MySQL.</span><span class="sxs-lookup"><span data-stu-id="86a2c-106">After running the script, you will have two virtual machines, one in each subnet that you can deploy web server and MySQL software to.</span></span>

<span data-ttu-id="86a2c-107">Si es necesario, instale Azure PowerShell con la instrucción que se encuentra en la [Guía de Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/) y, luego, ejecute `Login-AzureRmAccount` para crear una conexión con Azure.</span><span class="sxs-lookup"><span data-stu-id="86a2c-107">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="86a2c-108">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="86a2c-108">Sample script</span></span>


<span data-ttu-id="86a2c-109">[!code-powershell[main](../../../powershell_scripts/virtual-network/virtual-network-multi-tier-application/virtual-network-multi-tier-application.ps1  "Red virtual para la aplicación de niveles múltiples")]</span><span class="sxs-lookup"><span data-stu-id="86a2c-109">[!code-powershell[main](../../../powershell_scripts/virtual-network/virtual-network-multi-tier-application/virtual-network-multi-tier-application.ps1  "Virtual network for multi-tier application")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="86a2c-110">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="86a2c-110">Clean up deployment</span></span> 

<span data-ttu-id="86a2c-111">Ejecute el siguiente comando para quitar el grupo de recursos, la máquina virtual y todos los recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="86a2c-111">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="86a2c-112">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="86a2c-112">Script explanation</span></span>

<span data-ttu-id="86a2c-113">Este script usa los siguientes comandos para crear un grupo de recursos, una red virtual y grupos de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="86a2c-113">This script uses the following commands to create a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="86a2c-114">Cada comando de la tabla crea un vínculo a documentación específica del comando.</span><span class="sxs-lookup"><span data-stu-id="86a2c-114">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="86a2c-115">Comando</span><span class="sxs-lookup"><span data-stu-id="86a2c-115">Command</span></span> | <span data-ttu-id="86a2c-116">Notas</span><span class="sxs-lookup"><span data-stu-id="86a2c-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="86a2c-117">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="86a2c-117">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="86a2c-118">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="86a2c-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="86a2c-119">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="86a2c-119">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="86a2c-120">Crea una subred de front-end y una red virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="86a2c-120">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="86a2c-121">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="86a2c-121">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="86a2c-122">Crea una subred de back-end.</span><span class="sxs-lookup"><span data-stu-id="86a2c-122">Creates a back-end subnet.</span></span> |
| [<span data-ttu-id="86a2c-123">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="86a2c-123">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="86a2c-124">Crea una dirección IP pública para acceder a la VM desde Internet.</span><span class="sxs-lookup"><span data-stu-id="86a2c-124">Creates a public IP address to access the VM from the Internet.</span></span> |
| [<span data-ttu-id="86a2c-125">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="86a2c-125">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="86a2c-126">Crea interfaces de red virtual y las asocia a subredes de front-end y back-end de la red virtual.</span><span class="sxs-lookup"><span data-stu-id="86a2c-126">Creates virtual network interfaces and attaches them to the virtual network's front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="86a2c-127">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="86a2c-127">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="86a2c-128">Crea grupos de seguridad de red (NSG) que están asociados a las subredes de front-end y back-end.</span><span class="sxs-lookup"><span data-stu-id="86a2c-128">Creates network security groups (NSG) that are associated to the front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="86a2c-129">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="86a2c-129">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) |<span data-ttu-id="86a2c-130">Crea reglas NSG que permiten o bloquean puertos específicos para subredes concretas.</span><span class="sxs-lookup"><span data-stu-id="86a2c-130">Creates NSG rules that allow or block specific ports to specific subnets.</span></span> |
| [<span data-ttu-id="86a2c-131">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="86a2c-131">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="86a2c-132">Crea máquinas virtuales se crea y asocia una NIC a cada VM.</span><span class="sxs-lookup"><span data-stu-id="86a2c-132">Creates virtual machines and attaches a NIC to each VM.</span></span> <span data-ttu-id="86a2c-133">Este comando también especifica la imagen de máquina virtual que se usará y las credenciales administrativas.</span><span class="sxs-lookup"><span data-stu-id="86a2c-133">This command also specifies the virtual machine image to use and administrative credentials.</span></span> |
| [<span data-ttu-id="86a2c-134">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="86a2c-134">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="86a2c-135">Elimina un grupo de recursos y todos los recursos que contiene.</span><span class="sxs-lookup"><span data-stu-id="86a2c-135">Deletes a resource group and all resources it contains.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="86a2c-136">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="86a2c-136">Next steps</span></span>

<span data-ttu-id="86a2c-137">Para más información sobre Azure PowerShell, consulte la [documentación de Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="86a2c-137">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="86a2c-138">En la [documentación de la información general de redes de Azure](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json) puede encontrar ejemplos adicionales de script de PowerShell de redes.</span><span class="sxs-lookup"><span data-stu-id="86a2c-138">Additional networking PowerShell script samples can be found in the [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>