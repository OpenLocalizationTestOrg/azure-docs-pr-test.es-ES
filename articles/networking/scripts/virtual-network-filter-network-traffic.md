---
title: "ejemplo de secuencia de comandos CLI aaaAzure - tráfico de red de VM de filtro | Documentos de Microsoft"
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
ms.openlocfilehash: c2f14e54bc96c99420b4300d1c24a457ac8c948c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="filter-inbound-and-outbound-vm-network-traffic"></a><span data-ttu-id="790ec-103">Filtrar el tráfico de red de VM entrante y saliente</span><span class="sxs-lookup"><span data-stu-id="790ec-103">Filter inbound and outbound VM network traffic</span></span>

<span data-ttu-id="790ec-104">Este ejemplo de script crea una red virtual con subredes de front-end y back-end.</span><span class="sxs-lookup"><span data-stu-id="790ec-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="790ec-105">El tráfico de red entrante toohello la subred front-end es tooHTTP limitado, toohello Internet desde la subred de back-end de hello no se permite el tráfico de HTTPS y SSH, mientras saliente.</span><span class="sxs-lookup"><span data-stu-id="790ec-105">Inbound network traffic toohello front-end subnet is limited tooHTTP, HTTPS and SSH, while outbound traffic toohello Internet from hello back-end subnet is not permitted.</span></span> <span data-ttu-id="790ec-106">Después de ejecutar el script de Hola, tendrá una máquina virtual con dos NIC.</span><span class="sxs-lookup"><span data-stu-id="790ec-106">After running hello script, you will have one virtual machine with two NICs.</span></span> <span data-ttu-id="790ec-107">Cada NIC está conectado tooa otra subred.</span><span class="sxs-lookup"><span data-stu-id="790ec-107">Each NIC is connected tooa different subnet.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="790ec-108">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="790ec-108">Sample script</span></span>


[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/filter-network-traffic/filter-network-traffic.sh  "Filter VM network traffic")]

## <a name="clean-up-deployment"></a><span data-ttu-id="790ec-109">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="790ec-109">Clean up deployment</span></span> 

<span data-ttu-id="790ec-110">Ejecute hello después el grupo de recursos de comando tooremove hello, la VM y todos ellos relacionados con recursos.</span><span class="sxs-lookup"><span data-stu-id="790ec-110">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name MyResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="790ec-111">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="790ec-111">Script explanation</span></span>

<span data-ttu-id="790ec-112">Este script utiliza Hola después comandos toocreate un grupo de recursos, redes virtuales y grupos de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="790ec-112">This script uses hello following commands toocreate a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="790ec-113">Cada comando de la tabla de hello vincula documentación específica del toocommand.</span><span class="sxs-lookup"><span data-stu-id="790ec-113">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="790ec-114">Comando</span><span class="sxs-lookup"><span data-stu-id="790ec-114">Command</span></span> | <span data-ttu-id="790ec-115">Notas</span><span class="sxs-lookup"><span data-stu-id="790ec-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="790ec-116">az group create</span><span class="sxs-lookup"><span data-stu-id="790ec-116">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="790ec-117">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="790ec-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="790ec-118">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="790ec-118">az network vnet create</span></span>](/cli/azure/network/vnet#create) | <span data-ttu-id="790ec-119">Crea una subred de front-end y una red virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="790ec-119">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="790ec-120">az network subnet create</span><span class="sxs-lookup"><span data-stu-id="790ec-120">az network subnet create</span></span>](/cli/azure/network/vnet/subnet#create) | <span data-ttu-id="790ec-121">Crea una subred de back-end.</span><span class="sxs-lookup"><span data-stu-id="790ec-121">Creates a back-end subnet.</span></span> |
| [<span data-ttu-id="790ec-122">az network vnet subnet update</span><span class="sxs-lookup"><span data-stu-id="790ec-122">az network vnet subnet update</span></span>](/cli/azure/network/vnet/subnet#update) | <span data-ttu-id="790ec-123">Asocia los NSG toosubnets.</span><span class="sxs-lookup"><span data-stu-id="790ec-123">Associates NSGs toosubnets.</span></span> |
| [<span data-ttu-id="790ec-124">az network public-ip create</span><span class="sxs-lookup"><span data-stu-id="790ec-124">az network public-ip create</span></span>](/cli/azure/network/public-ip#create) | <span data-ttu-id="790ec-125">Crea un Hola de tooaccess VM pública para la dirección IP de hello Internet.</span><span class="sxs-lookup"><span data-stu-id="790ec-125">Creates a public IP address tooaccess hello VM from hello Internet.</span></span> |
| [<span data-ttu-id="790ec-126">az network nic create</span><span class="sxs-lookup"><span data-stu-id="790ec-126">az network nic create</span></span>](/cli/azure/network/nic#create) | <span data-ttu-id="790ec-127">Crea las interfaces de red virtual y los asocia subredes de la red virtual toohello front-end y back-end.</span><span class="sxs-lookup"><span data-stu-id="790ec-127">Creates virtual network interfaces and attaches them toohello virtual network's front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="790ec-128">az network nsg create</span><span class="sxs-lookup"><span data-stu-id="790ec-128">az network nsg create</span></span>](/cli/azure/network/nsg#create) | <span data-ttu-id="790ec-129">Crea grupos de seguridad de red (NSG) que son subredes de front-end y back-end de toohello asociado.</span><span class="sxs-lookup"><span data-stu-id="790ec-129">Creates network security groups (NSG) that are associated toohello front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="790ec-130">az network nsg rule create</span><span class="sxs-lookup"><span data-stu-id="790ec-130">az network nsg rule create</span></span>](/cli/azure/network/nsg/rule#create) |<span data-ttu-id="790ec-131">Crea reglas NSG que permiten o bloquear subredes toospecific de puertos específicos.</span><span class="sxs-lookup"><span data-stu-id="790ec-131">Creates NSG rules that allow or block specific ports toospecific subnets.</span></span> |
| [<span data-ttu-id="790ec-132">az vm create</span><span class="sxs-lookup"><span data-stu-id="790ec-132">az vm create</span></span>](/cli/azure/vm#create) | <span data-ttu-id="790ec-133">Crea las máquinas virtuales y adjunta un tooeach NIC virtual.</span><span class="sxs-lookup"><span data-stu-id="790ec-133">Creates virtual machines and attaches a NIC tooeach VM.</span></span> <span data-ttu-id="790ec-134">Este comando también especifica toouse de imagen de máquina virtual de Hola y credenciales administrativas.</span><span class="sxs-lookup"><span data-stu-id="790ec-134">This command also specifies hello virtual machine image toouse and administrative credentials.</span></span> |
| [<span data-ttu-id="790ec-135">az group delete</span><span class="sxs-lookup"><span data-stu-id="790ec-135">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="790ec-136">Elimina un grupo de recursos y todos los recursos que contiene.</span><span class="sxs-lookup"><span data-stu-id="790ec-136">Deletes a resource group and all resources it contains.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="790ec-137">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="790ec-137">Next steps</span></span>

<span data-ttu-id="790ec-138">Para obtener más información sobre Hola CLI de Azure, consulte [documentación de Azure CLI](/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="790ec-138">For more information on hello Azure CLI, see [Azure CLI documentation](/cli/azure/overview).</span></span>

<span data-ttu-id="790ec-139">Encontrará más ejemplos de secuencias de comandos CLI red Hola [documentación de introducción a las redes Azure](../cli-samples.md)</span><span class="sxs-lookup"><span data-stu-id="790ec-139">Additional networking CLI script samples can be found in hello [Azure Networking Overview documentation](../cli-samples.md)</span></span>
