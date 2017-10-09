---
title: Ejemplo de secuencia de comandos de CLI - aaaAzure crear una VM de Linux con NLB | Documentos de Microsoft
description: "Ejemplo de script de la CLI de Azure: creación de una máquina virtual Linux con NLB"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/27/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 79b245c1268734fead313b34c120f74ab2330d4b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-highly-available-vm"></a><span data-ttu-id="241e0-103">Creación de una máquina virtual de alta disponibilidad</span><span class="sxs-lookup"><span data-stu-id="241e0-103">Create a highly available VM</span></span>

<span data-ttu-id="241e0-104">Este ejemplo de secuencia de comandos crea todo lo necesario toorun varias máquinas virtuales de Ubuntu configurado en una alta disponibilidad y de carga equilibrada de configuración.</span><span class="sxs-lookup"><span data-stu-id="241e0-104">This script sample creates everything needed toorun several Ubuntu virtual machines configured in a highly available and load balanced configuration.</span></span> <span data-ttu-id="241e0-105">Después de ejecutar script de Hola, tendrá tres máquinas virtuales, tooan Unidos a un conjunto de disponibilidad de Azure y es accesible a través de un equilibrador de carga de Azure.</span><span class="sxs-lookup"><span data-stu-id="241e0-105">After running hello script, you will have three virtual machines, joined tooan Azure Availability Set, and accessible through an Azure Load Balancer.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="241e0-106">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="241e0-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-nlb/create-vm-nlb.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a><span data-ttu-id="241e0-107">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="241e0-107">Clean up deployment</span></span> 

<span data-ttu-id="241e0-108">Ejecute hello después el grupo de recursos de comando tooremove hello, la VM y todos ellos relacionados con recursos.</span><span class="sxs-lookup"><span data-stu-id="241e0-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="241e0-109">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="241e0-109">Script explanation</span></span>

<span data-ttu-id="241e0-110">Este script utiliza Hola después comandos toocreate un grupo de recursos, máquina virtual, conjunto de disponibilidad, equilibrador de carga y todos los recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="241e0-110">This script uses hello following commands toocreate a resource group, virtual machine, availability set, load balancer, and all related resources.</span></span> <span data-ttu-id="241e0-111">Cada comando de documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="241e0-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="241e0-112">Comando</span><span class="sxs-lookup"><span data-stu-id="241e0-112">Command</span></span> | <span data-ttu-id="241e0-113">Notas</span><span class="sxs-lookup"><span data-stu-id="241e0-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="241e0-114">az group create</span><span class="sxs-lookup"><span data-stu-id="241e0-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="241e0-115">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="241e0-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="241e0-116">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="241e0-116">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="241e0-117">Crea una red virtual y una subred de Azure.</span><span class="sxs-lookup"><span data-stu-id="241e0-117">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="241e0-118">az network public-ip create</span><span class="sxs-lookup"><span data-stu-id="241e0-118">az network public-ip create</span></span>](https://docs.microsoft.com/cli/azure/network/public-ip#create) | <span data-ttu-id="241e0-119">Crea una dirección IP pública con una dirección IP estática y un nombre DNS asociado.</span><span class="sxs-lookup"><span data-stu-id="241e0-119">Creates a public IP address with a static IP address and an associated DNS name.</span></span> |
| [<span data-ttu-id="241e0-120">az network lb create</span><span class="sxs-lookup"><span data-stu-id="241e0-120">az network lb create</span></span>](https://docs.microsoft.com/cli/azure/network/lb#create) | <span data-ttu-id="241e0-121">Crea un equilibrador de carga de red de Azure (NLB).</span><span class="sxs-lookup"><span data-stu-id="241e0-121">Creates an Azure Network Load Balancer (NLB).</span></span> |
| [<span data-ttu-id="241e0-122">az network lb probe create</span><span class="sxs-lookup"><span data-stu-id="241e0-122">az network lb probe create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/probe#create) | <span data-ttu-id="241e0-123">Crea un sondeo de NLB.</span><span class="sxs-lookup"><span data-stu-id="241e0-123">Creates an NLB probe.</span></span> <span data-ttu-id="241e0-124">Una prueba de NLB es toomonitor usado en cada máquina virtual en el conjunto NLB de Hola.</span><span class="sxs-lookup"><span data-stu-id="241e0-124">An NLB probe is used toomonitor each VM in hello NLB set.</span></span> <span data-ttu-id="241e0-125">Si ninguna máquina virtual deja de estar accesible, el tráfico no es toohello enrutado máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="241e0-125">If any VM becomes inaccessible, traffic is not routed toohello VM.</span></span> |
| [<span data-ttu-id="241e0-126">az network lb rule create</span><span class="sxs-lookup"><span data-stu-id="241e0-126">az network lb rule create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | <span data-ttu-id="241e0-127">Crea una regla de NLB.</span><span class="sxs-lookup"><span data-stu-id="241e0-127">Creates an NLB rule.</span></span> <span data-ttu-id="241e0-128">En este ejemplo, se crea una regla para el puerto 80.</span><span class="sxs-lookup"><span data-stu-id="241e0-128">In this sample, a rule is created for port 80.</span></span> <span data-ttu-id="241e0-129">Como el tráfico HTTP llega al Hola NLB, es tooport enrutado 80 una de las máquinas virtuales de hello en el conjunto NLB de Hola.</span><span class="sxs-lookup"><span data-stu-id="241e0-129">As HTTP traffic arrives at hello NLB, it is routed tooport 80 one of hello VMs in hello NLB set.</span></span> |
| [<span data-ttu-id="241e0-130">az network lb inbound-nat-rule create</span><span class="sxs-lookup"><span data-stu-id="241e0-130">az network lb inbound-nat-rule create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/inbound-nat-rule#create) | <span data-ttu-id="241e0-131">Crea una regla de traducción de direcciones de red (NAT) de NLB.</span><span class="sxs-lookup"><span data-stu-id="241e0-131">Creates an NLB Network Address Translation (NAT) rule.</span></span>  <span data-ttu-id="241e0-132">Las reglas NAT asignan un puerto de hello puerto tooa NLB en una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="241e0-132">NAT rules map a port of hello NLB tooa port on a VM.</span></span> <span data-ttu-id="241e0-133">En este ejemplo, se crea una regla NAT para SSH tráfico tooeach VM en el conjunto NLB de Hola.</span><span class="sxs-lookup"><span data-stu-id="241e0-133">In this sample, a NAT rule is created for SSH traffic tooeach VM in hello NLB set.</span></span>  |
| [<span data-ttu-id="241e0-134">az network nsg create</span><span class="sxs-lookup"><span data-stu-id="241e0-134">az network nsg create</span></span>](https://docs.microsoft.com/cli/azure/network/nsg#create) | <span data-ttu-id="241e0-135">Crea un grupo de seguridad de red (NSG), que es un límite de seguridad entre Hola internet y hello las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="241e0-135">Creates a network security group (NSG), which is a security boundary between hello internet and hello virtual machine.</span></span> |
| [<span data-ttu-id="241e0-136">az network nsg rule create</span><span class="sxs-lookup"><span data-stu-id="241e0-136">az network nsg rule create</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#create) | <span data-ttu-id="241e0-137">Crea un tooallow de regla NSG el tráfico entrante.</span><span class="sxs-lookup"><span data-stu-id="241e0-137">Creates an NSG rule tooallow inbound traffic.</span></span> <span data-ttu-id="241e0-138">En este ejemplo, el puerto 22 está abierto al tráfico SSH.</span><span class="sxs-lookup"><span data-stu-id="241e0-138">In this sample, port 22 is opened for SSH traffic.</span></span> |
| [<span data-ttu-id="241e0-139">az network nic create</span><span class="sxs-lookup"><span data-stu-id="241e0-139">az network nic create</span></span>](https://docs.microsoft.com/cli/azure/network/nic#create) | <span data-ttu-id="241e0-140">Crea una tarjeta de red virtual y lo adjunta toohello de red virtual, subred y NSG.</span><span class="sxs-lookup"><span data-stu-id="241e0-140">Creates a virtual network card and attaches it toohello virtual network, subnet, and NSG.</span></span> |
| [<span data-ttu-id="241e0-141">az vm availability-set create</span><span class="sxs-lookup"><span data-stu-id="241e0-141">az vm availability-set create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | <span data-ttu-id="241e0-142">Crea un conjunto de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="241e0-142">Creates an availability set.</span></span> <span data-ttu-id="241e0-143">Conjuntos de disponibilidad de garantizan la disponibilidad de las aplicaciones repartir hello las máquinas virtuales entre recursos físicos de forma que si se produce el error, no se realiza el conjunto completo de Hola.</span><span class="sxs-lookup"><span data-stu-id="241e0-143">Availability sets ensure application uptime by spreading hello virtual machines across physical resources such that if failure occurs, hello entire set is not effected.</span></span> |
| [<span data-ttu-id="241e0-144">az vm create</span><span class="sxs-lookup"><span data-stu-id="241e0-144">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | <span data-ttu-id="241e0-145">Crea la máquina virtual de Hola y lo conecta toohello tarjeta de red, red virtual, subred y NSG.</span><span class="sxs-lookup"><span data-stu-id="241e0-145">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="241e0-146">Este comando también especifica toobe de imagen de máquina virtual de hello usa y credenciales administrativas.</span><span class="sxs-lookup"><span data-stu-id="241e0-146">This command also specifies hello virtual machine image toobe used and administrative credentials.</span></span>  |
| [<span data-ttu-id="241e0-147">az group delete</span><span class="sxs-lookup"><span data-stu-id="241e0-147">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="241e0-148">Elimina un grupo de recursos, incluidos todos los recursos anidados.</span><span class="sxs-lookup"><span data-stu-id="241e0-148">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="241e0-149">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="241e0-149">Next steps</span></span>

<span data-ttu-id="241e0-150">Para obtener más información sobre Hola CLI de Azure, consulte [documentación de Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="241e0-150">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="241e0-151">Ejemplos de secuencias de comandos CLI de máquina virtual adicional pueden encontrarse en hello [documentación de Azure VM de Linux](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="241e0-151">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
