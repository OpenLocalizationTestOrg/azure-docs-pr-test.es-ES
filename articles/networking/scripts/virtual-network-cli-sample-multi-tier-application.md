---
title: 'secuencia de comandos CLI aaaAzure de ejemplo: crear una red para aplicaciones de varios niveles | Documentos de Microsoft'
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
ms.openlocfilehash: deeb3f459499cebd1b8ded6a299eb759d49cf08d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-network-for-multi-tier-applications"></a><span data-ttu-id="b6531-103">Creación de una red para aplicaciones de niveles múltiples</span><span class="sxs-lookup"><span data-stu-id="b6531-103">Create a network for multi-tier applications</span></span>

<span data-ttu-id="b6531-104">Este ejemplo de script crea una red virtual con subredes de front-end y back-end.</span><span class="sxs-lookup"><span data-stu-id="b6531-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="b6531-105">Subred de tráfico toohello front-end es tooHTTP limitado y SSH, al tráfico toohello subred back-end es tooMySQL limitado, puerto 3306.</span><span class="sxs-lookup"><span data-stu-id="b6531-105">Traffic toohello front-end subnet is limited tooHTTP and SSH, while traffic toohello back-end subnet is limited tooMySQL, port 3306.</span></span> <span data-ttu-id="b6531-106">Después de ejecutar script de Hola, tendrá dos máquinas virtuales, uno en cada subred que se pueden implementar el servidor web y el software MySQL.</span><span class="sxs-lookup"><span data-stu-id="b6531-106">After running hello script, you will have two virtual machines, one in each subnet that you can deploy web server and MySQL software to.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


## <a name="sample-script"></a><span data-ttu-id="b6531-107">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="b6531-107">Sample script</span></span>


[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/virtual-network-multi-tier-application/virtual-network-multi-tier-application.sh  "Virtual network for multi-tier application")]

## <a name="clean-up-deployment"></a><span data-ttu-id="b6531-108">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="b6531-108">Clean up deployment</span></span> 

<span data-ttu-id="b6531-109">Ejecute hello después el grupo de recursos de comando tooremove hello, la VM y todos ellos relacionados con recursos.</span><span class="sxs-lookup"><span data-stu-id="b6531-109">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name MyResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="b6531-110">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="b6531-110">Script explanation</span></span>

<span data-ttu-id="b6531-111">Este script utiliza Hola después comandos toocreate un grupo de recursos, redes virtuales y grupos de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="b6531-111">This script uses hello following commands toocreate a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="b6531-112">Cada comando de la tabla de hello vincula documentación específica del toocommand.</span><span class="sxs-lookup"><span data-stu-id="b6531-112">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="b6531-113">Comando</span><span class="sxs-lookup"><span data-stu-id="b6531-113">Command</span></span> | <span data-ttu-id="b6531-114">Notas</span><span class="sxs-lookup"><span data-stu-id="b6531-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="b6531-115">az group create</span><span class="sxs-lookup"><span data-stu-id="b6531-115">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="b6531-116">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="b6531-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="b6531-117">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="b6531-117">az network vnet create</span></span>](/cli/azure/network/vnet#create) | <span data-ttu-id="b6531-118">Crea una subred de front-end y una red virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="b6531-118">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="b6531-119">az network subnet create</span><span class="sxs-lookup"><span data-stu-id="b6531-119">az network subnet create</span></span>](/cli/azure/network/vnet/subnet#create) | <span data-ttu-id="b6531-120">Crea una subred de back-end.</span><span class="sxs-lookup"><span data-stu-id="b6531-120">Creates a back-end subnet.</span></span> |
| [<span data-ttu-id="b6531-121">az network public-ip create</span><span class="sxs-lookup"><span data-stu-id="b6531-121">az network public-ip create</span></span>](/cli/azure/network/public-ip#create) | <span data-ttu-id="b6531-122">Crea un Hola de tooaccess VM pública para la dirección IP de hello Internet.</span><span class="sxs-lookup"><span data-stu-id="b6531-122">Creates a public IP address tooaccess hello VM from hello Internet.</span></span> |
| [<span data-ttu-id="b6531-123">az network nic create</span><span class="sxs-lookup"><span data-stu-id="b6531-123">az network nic create</span></span>](/cli/azure/network/nic#create) | <span data-ttu-id="b6531-124">Crea las interfaces de red virtual y los asocia subredes de la red virtual toohello front-end y back-end.</span><span class="sxs-lookup"><span data-stu-id="b6531-124">Creates virtual network interfaces and attaches them toohello virtual network's front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="b6531-125">az network nsg create</span><span class="sxs-lookup"><span data-stu-id="b6531-125">az network nsg create</span></span>](/cli/azure/network/nsg#create) | <span data-ttu-id="b6531-126">Crea grupos de seguridad de red (NSG) que son subredes de front-end y back-end de toohello asociado.</span><span class="sxs-lookup"><span data-stu-id="b6531-126">Creates network security groups (NSG) that are associated toohello front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="b6531-127">az network nsg rule create</span><span class="sxs-lookup"><span data-stu-id="b6531-127">az network nsg rule create</span></span>](/cli/azure/network/nsg/rule#create) |<span data-ttu-id="b6531-128">Crea reglas NSG que permiten o bloquear subredes toospecific de puertos específicos.</span><span class="sxs-lookup"><span data-stu-id="b6531-128">Creates NSG rules that allow or block specific ports toospecific subnets.</span></span> |
| [<span data-ttu-id="b6531-129">az vm create</span><span class="sxs-lookup"><span data-stu-id="b6531-129">az vm create</span></span>](/cli/azure/vm#create) | <span data-ttu-id="b6531-130">Crea las máquinas virtuales y adjunta un tooeach NIC virtual.</span><span class="sxs-lookup"><span data-stu-id="b6531-130">Creates virtual machines and attaches a NIC tooeach VM.</span></span> <span data-ttu-id="b6531-131">Este comando también especifica toouse de imagen de máquina virtual de Hola y credenciales administrativas.</span><span class="sxs-lookup"><span data-stu-id="b6531-131">This command also specifies hello virtual machine image toouse and administrative credentials.</span></span> |
| [<span data-ttu-id="b6531-132">az group delete</span><span class="sxs-lookup"><span data-stu-id="b6531-132">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="b6531-133">Elimina un grupo de recursos y todos los recursos que contiene.</span><span class="sxs-lookup"><span data-stu-id="b6531-133">Deletes a resource group and all resources it contains.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="b6531-134">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b6531-134">Next steps</span></span>

<span data-ttu-id="b6531-135">Para obtener más información sobre Hola CLI de Azure, consulte [documentación de Azure CLI](/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b6531-135">For more information on hello Azure CLI, see [Azure CLI documentation](/cli/azure/overview).</span></span>

<span data-ttu-id="b6531-136">Encontrará más ejemplos de secuencias de comandos CLI red Hola [documentación de introducción a las redes Azure](../cli-samples.md)</span><span class="sxs-lookup"><span data-stu-id="b6531-136">Additional networking CLI script samples can be found in hello [Azure Networking Overview documentation](../cli-samples.md)</span></span>
