---
title: "Ejemplo de script de la CLI de Azure: redirigir el tráfico a través de una aplicación virtual de red | Microsoft Docs"
description: "Ejemplo de script de la CLI de Azure: redirigir el tráfico a través de una aplicación virtual de red de firewall."
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
ms.openlocfilehash: 78091b515c00591a4af8d807945475b6be50188a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="route-traffic-through-a-network-virtual-appliance"></a><span data-ttu-id="6fe47-103">Redirigir el tráfico a través de una aplicación virtual de red</span><span class="sxs-lookup"><span data-stu-id="6fe47-103">Route traffic through a network virtual appliance</span></span>

<span data-ttu-id="6fe47-104">Este ejemplo de script crea una red virtual con subredes de front-end y back-end.</span><span class="sxs-lookup"><span data-stu-id="6fe47-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="6fe47-105">También crea una VM con el reenvío IP habilitado para redirigir el tráfico entre las dos subredes.</span><span class="sxs-lookup"><span data-stu-id="6fe47-105">It also creates a VM with IP forwarding enabled to route traffic between the two subnets.</span></span> <span data-ttu-id="6fe47-106">Después de ejecutar el script puede implementar software de red, como una aplicación de firewall, en la VM.</span><span class="sxs-lookup"><span data-stu-id="6fe47-106">After running the script you can deploy network software, such as a firewall application, to the VM.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


## <a name="sample-script"></a><span data-ttu-id="6fe47-107">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="6fe47-107">Sample script</span></span>


<span data-ttu-id="6fe47-108">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/route-traffic-through-nva/route-traffic-through-nva.sh "Redirigir el tráfico a través de una aplicación virtual de red")]</span><span class="sxs-lookup"><span data-stu-id="6fe47-108">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/route-traffic-through-nva/route-traffic-through-nva.sh "Route traffic through a network virtual appliance")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="6fe47-109">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="6fe47-109">Clean up deployment</span></span> 

<span data-ttu-id="6fe47-110">Ejecute el siguiente comando para quitar el grupo de recursos, la máquina virtual y todos los recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="6fe47-110">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name MyResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="6fe47-111">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="6fe47-111">Script explanation</span></span>

<span data-ttu-id="6fe47-112">Este script usa los siguientes comandos para crear un grupo de recursos, una red virtual y grupos de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="6fe47-112">This script uses the following commands to create a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="6fe47-113">Cada comando de la tabla crea un vínculo a documentación específica del comando.</span><span class="sxs-lookup"><span data-stu-id="6fe47-113">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="6fe47-114">Comando</span><span class="sxs-lookup"><span data-stu-id="6fe47-114">Command</span></span> | <span data-ttu-id="6fe47-115">Notas</span><span class="sxs-lookup"><span data-stu-id="6fe47-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="6fe47-116">az group create</span><span class="sxs-lookup"><span data-stu-id="6fe47-116">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="6fe47-117">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="6fe47-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="6fe47-118">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="6fe47-118">az network vnet create</span></span>](/cli/azure/network/vnet#create) | <span data-ttu-id="6fe47-119">Crea una subred de front-end y una red virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="6fe47-119">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="6fe47-120">az network subnet create</span><span class="sxs-lookup"><span data-stu-id="6fe47-120">az network subnet create</span></span>](/cli/azure/network/vnet/subnet#create) | <span data-ttu-id="6fe47-121">Crea subredes de back-end y de red perimetral.</span><span class="sxs-lookup"><span data-stu-id="6fe47-121">Creates back-end and DMZ subnets.</span></span> |
| [<span data-ttu-id="6fe47-122">az network public-ip create</span><span class="sxs-lookup"><span data-stu-id="6fe47-122">az network public-ip create</span></span>](/cli/azure/network/public-ip#create) | <span data-ttu-id="6fe47-123">Crea una dirección IP pública para acceder a la VM desde Internet.</span><span class="sxs-lookup"><span data-stu-id="6fe47-123">Creates a public IP address to access the VM from the Internet.</span></span> |
| [<span data-ttu-id="6fe47-124">az network nic create</span><span class="sxs-lookup"><span data-stu-id="6fe47-124">az network nic create</span></span>](/cli/azure/network/nic#create) | <span data-ttu-id="6fe47-125">Crea una interfaz de red virtual y habilita el reenvío IP para ella.</span><span class="sxs-lookup"><span data-stu-id="6fe47-125">Creates a virtual network interface and enable IP forwarding for it.</span></span> |
| [<span data-ttu-id="6fe47-126">az network nsg create</span><span class="sxs-lookup"><span data-stu-id="6fe47-126">az network nsg create</span></span>](/cli/azure/network/nsg#create) | <span data-ttu-id="6fe47-127">Crea un grupo de seguridad de red (NSG).</span><span class="sxs-lookup"><span data-stu-id="6fe47-127">Creates a network security group (NSG).</span></span> |
| [<span data-ttu-id="6fe47-128">az network nsg rule create</span><span class="sxs-lookup"><span data-stu-id="6fe47-128">az network nsg rule create</span></span>](/cli/azure/network/nsg/rule#create) | <span data-ttu-id="6fe47-129">Crea reglas NSG que permiten puertos HTTP y HTTPS entrantes en la VM.</span><span class="sxs-lookup"><span data-stu-id="6fe47-129">Creates NSG rules that allow HTTP and HTTPS ports inbound to the VM.</span></span> |
| [<span data-ttu-id="6fe47-130">az network vnet subnet update</span><span class="sxs-lookup"><span data-stu-id="6fe47-130">az network vnet subnet update</span></span>](/cli/azure/network/vnet/subnet#update)| <span data-ttu-id="6fe47-131">Asocia los NSG y tablas de rutas a las subredes.</span><span class="sxs-lookup"><span data-stu-id="6fe47-131">Associates the NSGs and route tables to subnets.</span></span> |
| [<span data-ttu-id="6fe47-132">az network route-table create</span><span class="sxs-lookup"><span data-stu-id="6fe47-132">az network route-table create</span></span>](/cli/azure/network/route-table#create)| <span data-ttu-id="6fe47-133">Crea una tabla de rutas para todas las rutas.</span><span class="sxs-lookup"><span data-stu-id="6fe47-133">Creates a route table for all routes.</span></span> |
| [<span data-ttu-id="6fe47-134">az network route-table route create</span><span class="sxs-lookup"><span data-stu-id="6fe47-134">az network route-table route create</span></span>](/cli/azure/network/route-table/route#create)| <span data-ttu-id="6fe47-135">Crea rutas para redirigir el tráfico entre subredes e Internet a través de la VM.</span><span class="sxs-lookup"><span data-stu-id="6fe47-135">Creates routes to route traffic between subnets and the Internet through the VM.</span></span> |
| [<span data-ttu-id="6fe47-136">az vm create</span><span class="sxs-lookup"><span data-stu-id="6fe47-136">az vm create</span></span>](/cli/azure/vm#create) | <span data-ttu-id="6fe47-137">Crea una máquina virtual y conecta la NIC a ella.</span><span class="sxs-lookup"><span data-stu-id="6fe47-137">Creates a virtual machine and attaches the NIC to it.</span></span> <span data-ttu-id="6fe47-138">Este comando también especifica la imagen de máquina virtual que se usará y las credenciales administrativas.</span><span class="sxs-lookup"><span data-stu-id="6fe47-138">This command also specifies the virtual machine image to use and administrative credentials.</span></span> |
| [<span data-ttu-id="6fe47-139">az group delete</span><span class="sxs-lookup"><span data-stu-id="6fe47-139">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="6fe47-140">Elimina un grupo de recursos y todos los recursos que contiene.</span><span class="sxs-lookup"><span data-stu-id="6fe47-140">Deletes a resource group and all resources it contains.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="6fe47-141">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6fe47-141">Next steps</span></span>

<span data-ttu-id="6fe47-142">Para más información sobre la CLI de Azure, consulte la [documentación de la CLI de Azure](/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="6fe47-142">For more information on the Azure CLI, see [Azure CLI documentation](/cli/azure/overview).</span></span>

<span data-ttu-id="6fe47-143">En la [documentación de la información general de redes de Azure](../cli-samples.md) puede encontrar ejemplos adicionales de script de la CLI de redes.</span><span class="sxs-lookup"><span data-stu-id="6fe47-143">Additional networking CLI script samples can be found in the [Azure Networking Overview documentation](../cli-samples.md)</span></span>