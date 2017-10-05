---
title: "Ejemplo de script de CLI de Azure: crear una red para aplicaciones de niveles múltiples| Microsoft Docs"
description: "Ejemplo de script de CLI de Azure: crear una red virtual para aplicaciones de niveles múltiples."
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
ms.openlocfilehash: de65d820f2d9eea49b58185c81d815675fd76740
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-network-for-multi-tier-applications"></a><span data-ttu-id="68f66-103">Creación de una red para aplicaciones de niveles múltiples</span><span class="sxs-lookup"><span data-stu-id="68f66-103">Create a network for multi-tier applications</span></span>

<span data-ttu-id="68f66-104">Este ejemplo de script crea una red virtual con subredes de front-end y back-end.</span><span class="sxs-lookup"><span data-stu-id="68f66-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="68f66-105">El tráfico a la subred de front-end está limitado a HTTP y SSH, mientras que el tráfico a la subred de back-end está limitado a MySQL, al puerto 3306.</span><span class="sxs-lookup"><span data-stu-id="68f66-105">Traffic to the front-end subnet is limited to HTTP and SSH, while traffic to the back-end subnet is limited to MySQL, port 3306.</span></span> <span data-ttu-id="68f66-106">Después de ejecutar el script, tendrá dos máquinas virtuales, una en cada subred en la que puede implementar el servidor web y el software MySQL.</span><span class="sxs-lookup"><span data-stu-id="68f66-106">After running the script, you will have two virtual machines, one in each subnet that you can deploy web server and MySQL software to.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


## <a name="sample-script"></a><span data-ttu-id="68f66-107">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="68f66-107">Sample script</span></span>


<span data-ttu-id="68f66-108">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/virtual-network-multi-tier-application/virtual-network-multi-tier-application.sh  "Red virtual para la aplicación de niveles múltiples")]</span><span class="sxs-lookup"><span data-stu-id="68f66-108">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/virtual-network-multi-tier-application/virtual-network-multi-tier-application.sh  "Virtual network for multi-tier application")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="68f66-109">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="68f66-109">Clean up deployment</span></span> 

<span data-ttu-id="68f66-110">Ejecute el siguiente comando para quitar el grupo de recursos, la máquina virtual y todos los recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="68f66-110">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name MyResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="68f66-111">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="68f66-111">Script explanation</span></span>

<span data-ttu-id="68f66-112">Este script usa los siguientes comandos para crear un grupo de recursos, una red virtual y grupos de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="68f66-112">This script uses the following commands to create a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="68f66-113">Cada comando de la tabla crea un vínculo a documentación específica del comando.</span><span class="sxs-lookup"><span data-stu-id="68f66-113">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="68f66-114">Comando</span><span class="sxs-lookup"><span data-stu-id="68f66-114">Command</span></span> | <span data-ttu-id="68f66-115">Notas</span><span class="sxs-lookup"><span data-stu-id="68f66-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="68f66-116">az group create</span><span class="sxs-lookup"><span data-stu-id="68f66-116">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="68f66-117">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="68f66-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="68f66-118">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="68f66-118">az network vnet create</span></span>](/cli/azure/network/vnet#create) | <span data-ttu-id="68f66-119">Crea una subred de front-end y una red virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="68f66-119">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="68f66-120">az network subnet create</span><span class="sxs-lookup"><span data-stu-id="68f66-120">az network subnet create</span></span>](/cli/azure/network/vnet/subnet#create) | <span data-ttu-id="68f66-121">Crea una subred de back-end.</span><span class="sxs-lookup"><span data-stu-id="68f66-121">Creates a back-end subnet.</span></span> |
| [<span data-ttu-id="68f66-122">az network public-ip create</span><span class="sxs-lookup"><span data-stu-id="68f66-122">az network public-ip create</span></span>](/cli/azure/network/public-ip#create) | <span data-ttu-id="68f66-123">Crea una dirección IP pública para acceder a la VM desde Internet.</span><span class="sxs-lookup"><span data-stu-id="68f66-123">Creates a public IP address to access the VM from the Internet.</span></span> |
| [<span data-ttu-id="68f66-124">az network nic create</span><span class="sxs-lookup"><span data-stu-id="68f66-124">az network nic create</span></span>](/cli/azure/network/nic#create) | <span data-ttu-id="68f66-125">Crea interfaces de red virtual y las asocia a subredes de front-end y back-end de la red virtual.</span><span class="sxs-lookup"><span data-stu-id="68f66-125">Creates virtual network interfaces and attaches them to the virtual network's front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="68f66-126">az network nsg create</span><span class="sxs-lookup"><span data-stu-id="68f66-126">az network nsg create</span></span>](/cli/azure/network/nsg#create) | <span data-ttu-id="68f66-127">Crea grupos de seguridad de red (NSG) que están asociados a las subredes de front-end y back-end.</span><span class="sxs-lookup"><span data-stu-id="68f66-127">Creates network security groups (NSG) that are associated to the front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="68f66-128">az network nsg rule create</span><span class="sxs-lookup"><span data-stu-id="68f66-128">az network nsg rule create</span></span>](/cli/azure/network/nsg/rule#create) |<span data-ttu-id="68f66-129">Crea reglas NSG que permiten o bloquean puertos específicos para subredes concretas.</span><span class="sxs-lookup"><span data-stu-id="68f66-129">Creates NSG rules that allow or block specific ports to specific subnets.</span></span> |
| [<span data-ttu-id="68f66-130">az vm create</span><span class="sxs-lookup"><span data-stu-id="68f66-130">az vm create</span></span>](/cli/azure/vm#create) | <span data-ttu-id="68f66-131">Crea máquinas virtuales se crea y asocia una NIC a cada VM.</span><span class="sxs-lookup"><span data-stu-id="68f66-131">Creates virtual machines and attaches a NIC to each VM.</span></span> <span data-ttu-id="68f66-132">Este comando también especifica la imagen de máquina virtual que se usará y las credenciales administrativas.</span><span class="sxs-lookup"><span data-stu-id="68f66-132">This command also specifies the virtual machine image to use and administrative credentials.</span></span> |
| [<span data-ttu-id="68f66-133">az group delete</span><span class="sxs-lookup"><span data-stu-id="68f66-133">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="68f66-134">Elimina un grupo de recursos y todos los recursos que contiene.</span><span class="sxs-lookup"><span data-stu-id="68f66-134">Deletes a resource group and all resources it contains.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="68f66-135">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="68f66-135">Next steps</span></span>

<span data-ttu-id="68f66-136">Para más información sobre la CLI de Azure, consulte la [documentación de la CLI de Azure](/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="68f66-136">For more information on the Azure CLI, see [Azure CLI documentation](/cli/azure/overview).</span></span>

<span data-ttu-id="68f66-137">En la [documentación de la información general de redes de Azure](../cli-samples.md) puede encontrar ejemplos adicionales de script de la CLI de redes.</span><span class="sxs-lookup"><span data-stu-id="68f66-137">Additional networking CLI script samples can be found in the [Azure Networking Overview documentation](../cli-samples.md)</span></span>