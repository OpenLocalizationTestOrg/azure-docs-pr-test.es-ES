---
title: 'aaaAzure ejemplo de script de PowerShell: crear una red para aplicaciones de varios niveles | Documentos de Microsoft'
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
ms.openlocfilehash: 46d6d16dc5dbc8be467359f31346f017727b1abe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-network-for-multi-tier-applications"></a><span data-ttu-id="38700-103">Creación de una red para aplicaciones de niveles múltiples</span><span class="sxs-lookup"><span data-stu-id="38700-103">Create a network for multi-tier applications</span></span>

<span data-ttu-id="38700-104">Este ejemplo de script crea una red virtual con subredes de front-end y back-end.</span><span class="sxs-lookup"><span data-stu-id="38700-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="38700-105">Subred de tráfico toohello front-end es tooHTTP limitado y SSH, al tráfico toohello subred back-end es tooMySQL limitado, puerto 3306.</span><span class="sxs-lookup"><span data-stu-id="38700-105">Traffic toohello front-end subnet is limited tooHTTP and SSH, while traffic toohello back-end subnet is limited tooMySQL, port 3306.</span></span> <span data-ttu-id="38700-106">Después de ejecutar script de Hola, tendrá dos máquinas virtuales, uno en cada subred que se pueden implementar el servidor web y el software MySQL.</span><span class="sxs-lookup"><span data-stu-id="38700-106">After running hello script, you will have two virtual machines, one in each subnet that you can deploy web server and MySQL software to.</span></span>

<span data-ttu-id="38700-107">Si es necesario, instale hello Azure PowerShell con hello instrucción se encuentra en hello [Guía de Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/)y, a continuación, ejecute `Login-AzureRmAccount` toocreate una conexión con Azure.</span><span class="sxs-lookup"><span data-stu-id="38700-107">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="38700-108">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="38700-108">Sample script</span></span>


[!code-powershell[main](../../../powershell_scripts/virtual-network/virtual-network-multi-tier-application/virtual-network-multi-tier-application.ps1  "Virtual network for multi-tier application")]

## <a name="clean-up-deployment"></a><span data-ttu-id="38700-109">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="38700-109">Clean up deployment</span></span> 

<span data-ttu-id="38700-110">Ejecute hello después el grupo de recursos de comando tooremove hello, la VM y todos ellos relacionados con recursos.</span><span class="sxs-lookup"><span data-stu-id="38700-110">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="38700-111">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="38700-111">Script explanation</span></span>

<span data-ttu-id="38700-112">Este script utiliza Hola después comandos toocreate un grupo de recursos, redes virtuales y grupos de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="38700-112">This script uses hello following commands toocreate a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="38700-113">Cada comando de la tabla de hello vincula documentación específica del toocommand.</span><span class="sxs-lookup"><span data-stu-id="38700-113">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="38700-114">Comando</span><span class="sxs-lookup"><span data-stu-id="38700-114">Command</span></span> | <span data-ttu-id="38700-115">Notas</span><span class="sxs-lookup"><span data-stu-id="38700-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="38700-116">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="38700-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="38700-117">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="38700-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="38700-118">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="38700-118">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="38700-119">Crea una subred de front-end y una red virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="38700-119">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="38700-120">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="38700-120">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="38700-121">Crea una subred de back-end.</span><span class="sxs-lookup"><span data-stu-id="38700-121">Creates a back-end subnet.</span></span> |
| [<span data-ttu-id="38700-122">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="38700-122">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="38700-123">Crea un Hola de tooaccess VM pública para la dirección IP de hello Internet.</span><span class="sxs-lookup"><span data-stu-id="38700-123">Creates a public IP address tooaccess hello VM from hello Internet.</span></span> |
| [<span data-ttu-id="38700-124">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="38700-124">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="38700-125">Crea las interfaces de red virtual y los asocia subredes de la red virtual toohello front-end y back-end.</span><span class="sxs-lookup"><span data-stu-id="38700-125">Creates virtual network interfaces and attaches them toohello virtual network's front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="38700-126">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="38700-126">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="38700-127">Crea grupos de seguridad de red (NSG) que son subredes de front-end y back-end de toohello asociado.</span><span class="sxs-lookup"><span data-stu-id="38700-127">Creates network security groups (NSG) that are associated toohello front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="38700-128">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="38700-128">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) |<span data-ttu-id="38700-129">Crea reglas NSG que permiten o bloquear subredes toospecific de puertos específicos.</span><span class="sxs-lookup"><span data-stu-id="38700-129">Creates NSG rules that allow or block specific ports toospecific subnets.</span></span> |
| [<span data-ttu-id="38700-130">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="38700-130">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="38700-131">Crea las máquinas virtuales y adjunta un tooeach NIC virtual.</span><span class="sxs-lookup"><span data-stu-id="38700-131">Creates virtual machines and attaches a NIC tooeach VM.</span></span> <span data-ttu-id="38700-132">Este comando también especifica toouse de imagen de máquina virtual de Hola y credenciales administrativas.</span><span class="sxs-lookup"><span data-stu-id="38700-132">This command also specifies hello virtual machine image toouse and administrative credentials.</span></span> |
| [<span data-ttu-id="38700-133">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="38700-133">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="38700-134">Elimina un grupo de recursos y todos los recursos que contiene.</span><span class="sxs-lookup"><span data-stu-id="38700-134">Deletes a resource group and all resources it contains.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="38700-135">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="38700-135">Next steps</span></span>

<span data-ttu-id="38700-136">Para obtener más información sobre hello Azure PowerShell, consulte [documentación de Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="38700-136">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="38700-137">Encontrará ejemplos de script de PowerShell de red adicionales en hello [documentación de introducción a las redes Azure](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="38700-137">Additional networking PowerShell script samples can be found in hello [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>
