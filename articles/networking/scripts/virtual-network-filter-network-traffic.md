---
title: "Ejemplo de script de la CLI de Azure: filtrar el tráfico de red de VM | Microsoft Docs"
description: "Ejemplo de script de la CLI de Azure: filtrar el tráfico de red de VM entrante y saliente."
services: virtual-network
documentationcenter: virtual-network
author: jimdial
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 07/07/2017
ms.author: jdial
ms.openlocfilehash: 68ee013cff4e0be15af30239e0314f779f50177a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="filter-inbound-and-outbound-vm-network-traffic"></a><span data-ttu-id="ecaf3-103">Filtrar el tráfico de red de VM entrante y saliente</span><span class="sxs-lookup"><span data-stu-id="ecaf3-103">Filter inbound and outbound VM network traffic</span></span>

<span data-ttu-id="ecaf3-104">Este ejemplo de script crea una red virtual con subredes de front-end y back-end.</span><span class="sxs-lookup"><span data-stu-id="ecaf3-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="ecaf3-105">El tráfico de red entrante hacia la subred de front-end se limita a HTTP, HTTPS y SSH, mientras que el tráfico saliente hacia Internet desde la subred back-end no se permite.</span><span class="sxs-lookup"><span data-stu-id="ecaf3-105">Inbound network traffic to the front-end subnet is limited to HTTP, HTTPS and SSH, while outbound traffic to the Internet from the back-end subnet is not permitted.</span></span> <span data-ttu-id="ecaf3-106">Después de ejecutar el script, tendrá una máquina virtual con dos NIC.</span><span class="sxs-lookup"><span data-stu-id="ecaf3-106">After running the script, you will have one virtual machine with two NICs.</span></span> <span data-ttu-id="ecaf3-107">Cada NIC se conecta a una subred diferente.</span><span class="sxs-lookup"><span data-stu-id="ecaf3-107">Each NIC is connected to a different subnet.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="ecaf3-108">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="ecaf3-108">Sample script</span></span>


<span data-ttu-id="ecaf3-109">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/filter-network-traffic/filter-network-traffic.sh  "Filtrar el tráfico de red de VM")]</span><span class="sxs-lookup"><span data-stu-id="ecaf3-109">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/filter-network-traffic/filter-network-traffic.sh  "Filter VM network traffic")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="ecaf3-110">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="ecaf3-110">Clean up deployment</span></span> 

<span data-ttu-id="ecaf3-111">Ejecute el siguiente comando para quitar el grupo de recursos, la máquina virtual y todos los recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="ecaf3-111">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name MyResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="ecaf3-112">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="ecaf3-112">Script explanation</span></span>

<span data-ttu-id="ecaf3-113">Este script usa los siguientes comandos para crear un grupo de recursos, una red virtual y grupos de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="ecaf3-113">This script uses the following commands to create a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="ecaf3-114">Cada comando de la tabla crea un vínculo a documentación específica del comando.</span><span class="sxs-lookup"><span data-stu-id="ecaf3-114">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="ecaf3-115">Comando</span><span class="sxs-lookup"><span data-stu-id="ecaf3-115">Command</span></span> | <span data-ttu-id="ecaf3-116">Notas</span><span class="sxs-lookup"><span data-stu-id="ecaf3-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="ecaf3-117">az group create</span><span class="sxs-lookup"><span data-stu-id="ecaf3-117">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="ecaf3-118">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="ecaf3-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="ecaf3-119">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="ecaf3-119">az network vnet create</span></span>](/cli/azure/network/vnet#create) | <span data-ttu-id="ecaf3-120">Crea una subred de front-end y una red virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="ecaf3-120">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="ecaf3-121">az network subnet create</span><span class="sxs-lookup"><span data-stu-id="ecaf3-121">az network subnet create</span></span>](/cli/azure/network/vnet/subnet#create) | <span data-ttu-id="ecaf3-122">Crea una subred de back-end.</span><span class="sxs-lookup"><span data-stu-id="ecaf3-122">Creates a back-end subnet.</span></span> |
| [<span data-ttu-id="ecaf3-123">az network vnet subnet update</span><span class="sxs-lookup"><span data-stu-id="ecaf3-123">az network vnet subnet update</span></span>](/cli/azure/network/vnet/subnet#update) | <span data-ttu-id="ecaf3-124">Asocia NSG a subredes.</span><span class="sxs-lookup"><span data-stu-id="ecaf3-124">Associates NSGs to subnets.</span></span> |
| [<span data-ttu-id="ecaf3-125">az network public-ip create</span><span class="sxs-lookup"><span data-stu-id="ecaf3-125">az network public-ip create</span></span>](/cli/azure/network/public-ip#create) | <span data-ttu-id="ecaf3-126">Crea una dirección IP pública para acceder a la VM desde Internet.</span><span class="sxs-lookup"><span data-stu-id="ecaf3-126">Creates a public IP address to access the VM from the Internet.</span></span> |
| [<span data-ttu-id="ecaf3-127">az network nic create</span><span class="sxs-lookup"><span data-stu-id="ecaf3-127">az network nic create</span></span>](/cli/azure/network/nic#create) | <span data-ttu-id="ecaf3-128">Crea interfaces de red virtual y las asocia a subredes de front-end y back-end de la red virtual.</span><span class="sxs-lookup"><span data-stu-id="ecaf3-128">Creates virtual network interfaces and attaches them to the virtual network's front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="ecaf3-129">az network nsg create</span><span class="sxs-lookup"><span data-stu-id="ecaf3-129">az network nsg create</span></span>](/cli/azure/network/nsg#create) | <span data-ttu-id="ecaf3-130">Crea grupos de seguridad de red (NSG) que están asociados a las subredes de front-end y back-end.</span><span class="sxs-lookup"><span data-stu-id="ecaf3-130">Creates network security groups (NSG) that are associated to the front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="ecaf3-131">az network nsg rule create</span><span class="sxs-lookup"><span data-stu-id="ecaf3-131">az network nsg rule create</span></span>](/cli/azure/network/nsg/rule#create) |<span data-ttu-id="ecaf3-132">Crea reglas NSG que permiten o bloquean puertos específicos para subredes concretas.</span><span class="sxs-lookup"><span data-stu-id="ecaf3-132">Creates NSG rules that allow or block specific ports to specific subnets.</span></span> |
| [<span data-ttu-id="ecaf3-133">az vm create</span><span class="sxs-lookup"><span data-stu-id="ecaf3-133">az vm create</span></span>](/cli/azure/vm#create) | <span data-ttu-id="ecaf3-134">Crea máquinas virtuales se crea y asocia una NIC a cada VM.</span><span class="sxs-lookup"><span data-stu-id="ecaf3-134">Creates virtual machines and attaches a NIC to each VM.</span></span> <span data-ttu-id="ecaf3-135">Este comando también especifica la imagen de máquina virtual que se usará y las credenciales administrativas.</span><span class="sxs-lookup"><span data-stu-id="ecaf3-135">This command also specifies the virtual machine image to use and administrative credentials.</span></span> |
| [<span data-ttu-id="ecaf3-136">az group delete</span><span class="sxs-lookup"><span data-stu-id="ecaf3-136">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="ecaf3-137">Elimina un grupo de recursos y todos los recursos que contiene.</span><span class="sxs-lookup"><span data-stu-id="ecaf3-137">Deletes a resource group and all resources it contains.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="ecaf3-138">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ecaf3-138">Next steps</span></span>

<span data-ttu-id="ecaf3-139">Para más información sobre la CLI de Azure, consulte la [documentación de la CLI de Azure](/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ecaf3-139">For more information on the Azure CLI, see [Azure CLI documentation](/cli/azure/overview).</span></span>

<span data-ttu-id="ecaf3-140">En la [documentación de la información general de redes de Azure](../cli-samples.md) puede encontrar ejemplos adicionales de script de la CLI de redes.</span><span class="sxs-lookup"><span data-stu-id="ecaf3-140">Additional networking CLI script samples can be found in the [Azure Networking Overview documentation](../cli-samples.md)</span></span>