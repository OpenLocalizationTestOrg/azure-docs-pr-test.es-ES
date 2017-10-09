---
title: Ejemplo de secuencia de comandos de CLI - aaaAzure equilibra la carga de varios sitios Web con hello CLI de Azure | Documentos de Microsoft
description: "Ejemplo de secuencia de comandos CLI Azure - toohello de varios sitios Web se equilibra la carga misma máquina virtual"
services: load-balancer
documentationcenter: load-balancer
author: KumudD
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: load-balancer
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 07/07/2017
ms.author: kumud
ms.openlocfilehash: 136da5d1783fb9f9dc87f1ffad8eec7b95c6bd7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-multiple-websites"></a><span data-ttu-id="81b92-103">Equilibrio de carga entre varios sitios web</span><span class="sxs-lookup"><span data-stu-id="81b92-103">Load balance multiple websites</span></span>

<span data-ttu-id="81b92-104">Este ejemplo de script crea una red virtual con dos máquinas virtuales que son miembros de un conjunto de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="81b92-104">This script sample creates a virtual network with two virtual machines (VM) that are members of an availability set.</span></span> <span data-ttu-id="81b92-105">Un equilibrador de carga dirige el tráfico de dos direcciones IP toohello dos las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="81b92-105">A load balancer directs traffic for two separate IP addresses toohello two VMs.</span></span> <span data-ttu-id="81b92-106">Después de ejecutar script de Hola, podría implementar toohello de software de servidor web las máquinas virtuales y hospedar varios sitios web, cada uno con su propia dirección IP.</span><span class="sxs-lookup"><span data-stu-id="81b92-106">After running hello script, you could deploy web server software toohello VMs and host multiple web sites, each with its own IP address.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="81b92-107">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="81b92-107">Sample script</span></span>


[!code-azurecli-interactive[main](../../../cli_scripts/load-balancer/load-balance-multiple-web-sites-vm/load-balance-multiple-web-sites-vm.sh  "Load balance multiple web sites")]

## <a name="clean-up-deployment"></a><span data-ttu-id="81b92-108">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="81b92-108">Clean up deployment</span></span> 

<span data-ttu-id="81b92-109">Ejecute hello después el grupo de recursos de comando tooremove hello, la VM y todos ellos relacionados con recursos.</span><span class="sxs-lookup"><span data-stu-id="81b92-109">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="81b92-110">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="81b92-110">Script explanation</span></span>

<span data-ttu-id="81b92-111">Este script utiliza Hola siga los comandos del toocreate un grupo de recursos de red virtual, equilibrador de carga y todos ellos relacionados con recursos.</span><span class="sxs-lookup"><span data-stu-id="81b92-111">This script uses hello following commands toocreate a resource group, virtual network, load balancer, and all related resources.</span></span> <span data-ttu-id="81b92-112">Cada comando de documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="81b92-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="81b92-113">Comando</span><span class="sxs-lookup"><span data-stu-id="81b92-113">Command</span></span> | <span data-ttu-id="81b92-114">Notas</span><span class="sxs-lookup"><span data-stu-id="81b92-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="81b92-115">az group create</span><span class="sxs-lookup"><span data-stu-id="81b92-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="81b92-116">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="81b92-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="81b92-117">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="81b92-117">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="81b92-118">Crea una red virtual y una subred de Azure.</span><span class="sxs-lookup"><span data-stu-id="81b92-118">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="81b92-119">az network public-ip create</span><span class="sxs-lookup"><span data-stu-id="81b92-119">az network public-ip create</span></span>](https://docs.microsoft.com/cli/azure/network/public-ip#create) | <span data-ttu-id="81b92-120">Crea una dirección IP pública con una dirección IP estática y un nombre DNS asociado.</span><span class="sxs-lookup"><span data-stu-id="81b92-120">Creates a public IP address with a static IP address and an associated DNS name.</span></span> |
| [<span data-ttu-id="81b92-121">az network lb create</span><span class="sxs-lookup"><span data-stu-id="81b92-121">az network lb create</span></span>](https://docs.microsoft.com/cli/azure/network/lb#create) | <span data-ttu-id="81b92-122">Crea una instancia de Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="81b92-122">Creates an Azure Load Balancer.</span></span> |
| [<span data-ttu-id="81b92-123">az network lb probe create</span><span class="sxs-lookup"><span data-stu-id="81b92-123">az network lb probe create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/probe#create) | <span data-ttu-id="81b92-124">Crea un sondeo de equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="81b92-124">Creates a load balancer probe.</span></span> <span data-ttu-id="81b92-125">Un sondeo del equilibrador de carga es toomonitor usado en cada máquina virtual en el conjunto de equilibrador de carga de Hola.</span><span class="sxs-lookup"><span data-stu-id="81b92-125">A load balancer probe is used toomonitor each VM in hello load balancer set.</span></span> <span data-ttu-id="81b92-126">Si ninguna máquina virtual deja de estar accesible, el tráfico no es toohello enrutado máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="81b92-126">If any VM becomes inaccessible, traffic is not routed toohello VM.</span></span> |
| [<span data-ttu-id="81b92-127">az network lb rule create</span><span class="sxs-lookup"><span data-stu-id="81b92-127">az network lb rule create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | <span data-ttu-id="81b92-128">Crea una regla de equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="81b92-128">Creates a load balancer rule.</span></span> <span data-ttu-id="81b92-129">En este ejemplo, se crea una regla para el puerto 80.</span><span class="sxs-lookup"><span data-stu-id="81b92-129">In this sample, a rule is created for port 80.</span></span> <span data-ttu-id="81b92-130">Como el tráfico HTTP llega al equilibrador de carga de hello, es tooport enrutado 80 una de las máquinas virtuales de hello en el conjunto de equilibrador de carga de Hola.</span><span class="sxs-lookup"><span data-stu-id="81b92-130">As HTTP traffic arrives at hello load balancer, it is routed tooport 80 one of hello VMs in hello load balancer set.</span></span> |
| [<span data-ttu-id="81b92-131">az network lb frontend-ip create</span><span class="sxs-lookup"><span data-stu-id="81b92-131">az network lb frontend-ip create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/frontend-ip#create) | <span data-ttu-id="81b92-132">Crear una dirección IP de front-end para hello equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="81b92-132">Create a frontend IP address for hello Load Balancer.</span></span> |
| [<span data-ttu-id="81b92-133">az network lb address-pool create</span><span class="sxs-lookup"><span data-stu-id="81b92-133">az network lb address-pool create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/address-pool#create) | <span data-ttu-id="81b92-134">Crea un grupo de direcciones de back-end.</span><span class="sxs-lookup"><span data-stu-id="81b92-134">Creates a backend address pool.</span></span> |
| [<span data-ttu-id="81b92-135">az network nic create</span><span class="sxs-lookup"><span data-stu-id="81b92-135">az network nic create</span></span>](https://docs.microsoft.com/cli/azure/network/nic#create) | <span data-ttu-id="81b92-136">Crea una tarjeta de red virtual y lo adjunta toohello de red virtual y subred.</span><span class="sxs-lookup"><span data-stu-id="81b92-136">Creates a virtual network card and attaches it toohello virtual network, and subnet.</span></span> |
| [<span data-ttu-id="81b92-137">az vm availability-set create</span><span class="sxs-lookup"><span data-stu-id="81b92-137">az vm availability-set create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | <span data-ttu-id="81b92-138">Crea un conjunto de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="81b92-138">Creates an availability set.</span></span> <span data-ttu-id="81b92-139">Conjuntos de disponibilidad de garantizan la disponibilidad de las aplicaciones repartir hello las máquinas virtuales entre recursos físicos de forma que si se produce el error, no se realiza el conjunto completo de Hola.</span><span class="sxs-lookup"><span data-stu-id="81b92-139">Availability sets ensure application uptime by spreading hello virtual machines across physical resources such that if failure occurs, hello entire set is not effected.</span></span> |
| [<span data-ttu-id="81b92-140">az network nic ip-config create</span><span class="sxs-lookup"><span data-stu-id="81b92-140">az network nic ip-config create</span></span>](https://docs.microsoft.com/cli/azure/network/nic/ip-config#create) | <span data-ttu-id="81b92-141">Crea una configuración IP.</span><span class="sxs-lookup"><span data-stu-id="81b92-141">Creates an IP confiuration.</span></span> <span data-ttu-id="81b92-142">Debe tener la característica de hello Microsoft.Network/AllowMultipleIpConfigurationsPerNic habilitado para esta suscripción.</span><span class="sxs-lookup"><span data-stu-id="81b92-142">You must have hello Microsoft.Network/AllowMultipleIpConfigurationsPerNic feature enabled for your subscription.</span></span> <span data-ttu-id="81b92-143">Una sola configuración puede designarse como configuración IP primaria de Hola por NIC, con hello: marca de convertir en principal.</span><span class="sxs-lookup"><span data-stu-id="81b92-143">Only one configuration may be designated as hello primary IP configuration per NIC, using hello --make-primary flag.</span></span> |
| [<span data-ttu-id="81b92-144">az vm create</span><span class="sxs-lookup"><span data-stu-id="81b92-144">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | <span data-ttu-id="81b92-145">Crea la máquina virtual de Hola y lo conecta toohello tarjeta de red, red virtual, subred y NSG.</span><span class="sxs-lookup"><span data-stu-id="81b92-145">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="81b92-146">Este comando también especifica toobe de imagen de máquina virtual de hello usa y credenciales administrativas.</span><span class="sxs-lookup"><span data-stu-id="81b92-146">This command also specifies hello virtual machine image toobe used and administrative credentials.</span></span>  |
| [<span data-ttu-id="81b92-147">az group delete</span><span class="sxs-lookup"><span data-stu-id="81b92-147">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="81b92-148">Elimina un grupo de recursos, incluidos todos los recursos anidados.</span><span class="sxs-lookup"><span data-stu-id="81b92-148">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="81b92-149">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="81b92-149">Next steps</span></span>

<span data-ttu-id="81b92-150">Para obtener más información sobre Hola CLI de Azure, consulte [documentación de Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="81b92-150">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="81b92-151">Encontrará más ejemplos de secuencias de comandos CLI red Hola [documentación de introducción a las redes Azure](../cli-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="81b92-151">Additional networking CLI script samples can be found in hello [Azure Networking Overview documentation](../cli-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>
