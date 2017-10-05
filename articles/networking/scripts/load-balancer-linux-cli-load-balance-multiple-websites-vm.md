---
title: 'Ejemplo de script de la CLI Azure : equilibrio de carga entre varios sitios web con la CLI de Azure | Microsoft Docs'
description: "Ejemplo de script de la CLI Azure : equilibrio de carga entre varios sitios web con la misma máquina virtual"
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
ms.openlocfilehash: c5a584b33025122033b930822ae0a0864a7ec1cb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="load-balance-multiple-websites"></a><span data-ttu-id="efc99-103">Equilibrio de carga entre varios sitios web</span><span class="sxs-lookup"><span data-stu-id="efc99-103">Load balance multiple websites</span></span>

<span data-ttu-id="efc99-104">Este ejemplo de script crea una red virtual con dos máquinas virtuales que son miembros de un conjunto de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="efc99-104">This script sample creates a virtual network with two virtual machines (VM) that are members of an availability set.</span></span> <span data-ttu-id="efc99-105">Un equilibrador de carga dirige el tráfico de dos direcciones IP independientes a las dos máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="efc99-105">A load balancer directs traffic for two separate IP addresses to the two VMs.</span></span> <span data-ttu-id="efc99-106">Después de ejecutar el script, podría implementar software de servidor web en las máquinas virtuales y hospedar varios sitios web, cada uno con su propia dirección IP.</span><span class="sxs-lookup"><span data-stu-id="efc99-106">After running the script, you could deploy web server software to the VMs and host multiple web sites, each with its own IP address.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="efc99-107">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="efc99-107">Sample script</span></span>


<span data-ttu-id="efc99-108">[!code-azurecli-interactive[main](../../../cli_scripts/load-balancer/load-balance-multiple-web-sites-vm/load-balance-multiple-web-sites-vm.sh  "Equilibrio de carga entre varios sitios web")]</span><span class="sxs-lookup"><span data-stu-id="efc99-108">[!code-azurecli-interactive[main](../../../cli_scripts/load-balancer/load-balance-multiple-web-sites-vm/load-balance-multiple-web-sites-vm.sh  "Load balance multiple web sites")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="efc99-109">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="efc99-109">Clean up deployment</span></span> 

<span data-ttu-id="efc99-110">Ejecute el siguiente comando para quitar el grupo de recursos, la máquina virtual y todos los recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="efc99-110">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="efc99-111">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="efc99-111">Script explanation</span></span>

<span data-ttu-id="efc99-112">Este script usa los siguientes comandos para crear un grupo de recursos, una red virtual, un equilibrador de carga y todos los recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="efc99-112">This script uses the following commands to create a resource group, virtual network, load balancer, and all related resources.</span></span> <span data-ttu-id="efc99-113">Cada comando de la tabla crea un vínculo a documentación específica del comando.</span><span class="sxs-lookup"><span data-stu-id="efc99-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="efc99-114">Comando</span><span class="sxs-lookup"><span data-stu-id="efc99-114">Command</span></span> | <span data-ttu-id="efc99-115">Notas</span><span class="sxs-lookup"><span data-stu-id="efc99-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="efc99-116">az group create</span><span class="sxs-lookup"><span data-stu-id="efc99-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="efc99-117">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="efc99-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="efc99-118">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="efc99-118">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="efc99-119">Crea una red virtual y una subred de Azure.</span><span class="sxs-lookup"><span data-stu-id="efc99-119">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="efc99-120">az network public-ip create</span><span class="sxs-lookup"><span data-stu-id="efc99-120">az network public-ip create</span></span>](https://docs.microsoft.com/cli/azure/network/public-ip#create) | <span data-ttu-id="efc99-121">Crea una dirección IP pública con una dirección IP estática y un nombre DNS asociado.</span><span class="sxs-lookup"><span data-stu-id="efc99-121">Creates a public IP address with a static IP address and an associated DNS name.</span></span> |
| [<span data-ttu-id="efc99-122">az network lb create</span><span class="sxs-lookup"><span data-stu-id="efc99-122">az network lb create</span></span>](https://docs.microsoft.com/cli/azure/network/lb#create) | <span data-ttu-id="efc99-123">Crea una instancia de Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="efc99-123">Creates an Azure Load Balancer.</span></span> |
| [<span data-ttu-id="efc99-124">az network lb probe create</span><span class="sxs-lookup"><span data-stu-id="efc99-124">az network lb probe create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/probe#create) | <span data-ttu-id="efc99-125">Crea un sondeo de equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="efc99-125">Creates a load balancer probe.</span></span> <span data-ttu-id="efc99-126">Un sondeo de equilibrador de carga se usa para supervisar cada máquina virtual del conjunto de equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="efc99-126">A load balancer probe is used to monitor each VM in the load balancer set.</span></span> <span data-ttu-id="efc99-127">Si alguna máquina virtual deja de estar accesible, el tráfico no se enruta a la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="efc99-127">If any VM becomes inaccessible, traffic is not routed to the VM.</span></span> |
| [<span data-ttu-id="efc99-128">az network lb rule create</span><span class="sxs-lookup"><span data-stu-id="efc99-128">az network lb rule create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | <span data-ttu-id="efc99-129">Crea una regla de equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="efc99-129">Creates a load balancer rule.</span></span> <span data-ttu-id="efc99-130">En este ejemplo, se crea una regla para el puerto 80.</span><span class="sxs-lookup"><span data-stu-id="efc99-130">In this sample, a rule is created for port 80.</span></span> <span data-ttu-id="efc99-131">Según va llegando el tráfico HTTP al equilibrador de carga, se enruta al puerto 80 de una de las máquinas virtuales del conjunto de equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="efc99-131">As HTTP traffic arrives at the load balancer, it is routed to port 80 one of the VMs in the load balancer set.</span></span> |
| [<span data-ttu-id="efc99-132">az network lb frontend-ip create</span><span class="sxs-lookup"><span data-stu-id="efc99-132">az network lb frontend-ip create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/frontend-ip#create) | <span data-ttu-id="efc99-133">Crea una dirección IP de front-end para el equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="efc99-133">Create a frontend IP address for the Load Balancer.</span></span> |
| [<span data-ttu-id="efc99-134">az network lb address-pool create</span><span class="sxs-lookup"><span data-stu-id="efc99-134">az network lb address-pool create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/address-pool#create) | <span data-ttu-id="efc99-135">Crea un grupo de direcciones de back-end.</span><span class="sxs-lookup"><span data-stu-id="efc99-135">Creates a backend address pool.</span></span> |
| [<span data-ttu-id="efc99-136">az network nic create</span><span class="sxs-lookup"><span data-stu-id="efc99-136">az network nic create</span></span>](https://docs.microsoft.com/cli/azure/network/nic#create) | <span data-ttu-id="efc99-137">Crea una tarjeta de red virtual y la conecta con la red virtual y la subred.</span><span class="sxs-lookup"><span data-stu-id="efc99-137">Creates a virtual network card and attaches it to the virtual network, and subnet.</span></span> |
| [<span data-ttu-id="efc99-138">az vm availability-set create</span><span class="sxs-lookup"><span data-stu-id="efc99-138">az vm availability-set create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | <span data-ttu-id="efc99-139">Crea un conjunto de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="efc99-139">Creates an availability set.</span></span> <span data-ttu-id="efc99-140">Los conjuntos de disponibilidad garantizan la disponibilidad de las aplicaciones al repartir las máquinas virtuales entre los recursos físicos, de forma que si se produce un error, el conjunto no se verá afectado en su totalidad.</span><span class="sxs-lookup"><span data-stu-id="efc99-140">Availability sets ensure application uptime by spreading the virtual machines across physical resources such that if failure occurs, the entire set is not effected.</span></span> |
| [<span data-ttu-id="efc99-141">az network nic ip-config create</span><span class="sxs-lookup"><span data-stu-id="efc99-141">az network nic ip-config create</span></span>](https://docs.microsoft.com/cli/azure/network/nic/ip-config#create) | <span data-ttu-id="efc99-142">Crea una configuración IP.</span><span class="sxs-lookup"><span data-stu-id="efc99-142">Creates an IP confiuration.</span></span> <span data-ttu-id="efc99-143">Debe tener la característica de Microsoft.Network/AllowMultipleIpConfigurationsPerNic habilitada en su suscripción.</span><span class="sxs-lookup"><span data-stu-id="efc99-143">You must have the Microsoft.Network/AllowMultipleIpConfigurationsPerNic feature enabled for your subscription.</span></span> <span data-ttu-id="efc99-144">Solo se puede designar una configuración como configuración IP primaria por adaptador de red, mediante la marca --make-primary.</span><span class="sxs-lookup"><span data-stu-id="efc99-144">Only one configuration may be designated as the primary IP configuration per NIC, using the --make-primary flag.</span></span> |
| [<span data-ttu-id="efc99-145">az vm create</span><span class="sxs-lookup"><span data-stu-id="efc99-145">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | <span data-ttu-id="efc99-146">Crea la máquina virtual y la conecta con la tarjeta de red, la red virtual, la subred y el NSG.</span><span class="sxs-lookup"><span data-stu-id="efc99-146">Creates the virtual machine and connects it to the network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="efc99-147">Este comando también especifica la imagen de máquina virtual que se usará, y las credenciales administrativas.</span><span class="sxs-lookup"><span data-stu-id="efc99-147">This command also specifies the virtual machine image to be used and administrative credentials.</span></span>  |
| [<span data-ttu-id="efc99-148">az group delete</span><span class="sxs-lookup"><span data-stu-id="efc99-148">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="efc99-149">Elimina un grupo de recursos, incluidos todos los recursos anidados.</span><span class="sxs-lookup"><span data-stu-id="efc99-149">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="efc99-150">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="efc99-150">Next steps</span></span>

<span data-ttu-id="efc99-151">Para más información sobre la CLI de Azure, consulte la [documentación de la CLI de Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="efc99-151">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="efc99-152">En la [documentación de la información general de redes de Azure](../cli-samples.md?toc=%2fazure%2fnetworking%2ftoc.json) puede encontrar ejemplos adicionales de script de la CLI de redes.</span><span class="sxs-lookup"><span data-stu-id="efc99-152">Additional networking CLI script samples can be found in the [Azure Networking Overview documentation](../cli-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>
