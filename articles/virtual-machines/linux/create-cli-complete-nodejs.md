---
title: "Creación de un entorno de Linux completo con la CLI de Azure 1.0 | Microsoft Docs"
description: "Cree almacenamiento, una máquina virtual Linux, una red virtual y subred, un equilibrador de carga, una NIC, una dirección IP pública, un grupo de seguridad de red, todo desde el principio mediante la CLI de Azure 1.0."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4ba4060b-ce95-4747-a735-1d7c68597a1a
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: 201ccd523e49d638ace50fbc0ffdceb705b35473
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-complete-linux-environment-with-the-azure-cli-10"></a><span data-ttu-id="1844b-103">Creación de un entorno de Linux completo con la CLI de Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="1844b-103">Create a complete Linux environment with the Azure CLI 1.0</span></span>
<span data-ttu-id="1844b-104">En este artículo, vamos a crear una red sencilla con un equilibrador de carga y un par de máquinas virtuales útiles para el desarrollo y la computación simple.</span><span class="sxs-lookup"><span data-stu-id="1844b-104">In this article, we build a simple network with a load balancer and a pair of VMs that are useful for development and simple computing.</span></span> <span data-ttu-id="1844b-105">Lo vamos a guiar por el proceso comando a comando, hasta que tenga funcionando dos máquinas virtuales Linux seguras a las que se pueda conectar desde cualquier parte de Internet.</span><span class="sxs-lookup"><span data-stu-id="1844b-105">We walk through the process command by command, until you have two working, secure Linux VMs to which you can connect from anywhere on the Internet.</span></span> <span data-ttu-id="1844b-106">Luego, podrá pasar a redes y entornos más complejos.</span><span class="sxs-lookup"><span data-stu-id="1844b-106">Then you can move on to more complex networks and environments.</span></span>

<span data-ttu-id="1844b-107">Tras su lectura, conocerá la jerarquía de dependencias que ofrece el modelo de implementación de Resource Manager y la potencia que proporciona.</span><span class="sxs-lookup"><span data-stu-id="1844b-107">Along the way, you learn about the dependency hierarchy that the Resource Manager deployment model gives you, and about how much power it provides.</span></span> <span data-ttu-id="1844b-108">Cuando vea cómo se compila el sistema, puede recompilarlo mucho más rápido mediante [plantillas de Azure Resource Manager](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1844b-108">After you see how the system is built, you can rebuild it much more quickly by using [Azure Resource Manager templates](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="1844b-109">Además, cuando vea cómo encajan las distintas partes del entorno, la creación de plantillas para automatizarlas se volverá más fácil.</span><span class="sxs-lookup"><span data-stu-id="1844b-109">Also, after you learn how the parts of your environment fit together, creating templates to automate them becomes easier.</span></span>

<span data-ttu-id="1844b-110">El entorno contiene:</span><span class="sxs-lookup"><span data-stu-id="1844b-110">The environment contains:</span></span>

* <span data-ttu-id="1844b-111">Dos máquinas virtuales dentro de un conjunto de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="1844b-111">Two VMs inside an availability set.</span></span>
* <span data-ttu-id="1844b-112">Un equilibrador de carga con una regla de equilibrio de carga en el puerto 80.</span><span class="sxs-lookup"><span data-stu-id="1844b-112">A load balancer with a load-balancing rule on port 80.</span></span>
* <span data-ttu-id="1844b-113">Reglas de grupo de seguridad de red (NSG) para proteger la máquina virtual del tráfico no deseado.</span><span class="sxs-lookup"><span data-stu-id="1844b-113">Network security group (NSG) rules to protect your VM from unwanted traffic.</span></span>

<span data-ttu-id="1844b-114">Para crear este entorno personalizado, es preciso tener la versión más reciente de la [CLI de Azure 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) en modo de Resource Manager (`azure config mode arm`).</span><span class="sxs-lookup"><span data-stu-id="1844b-114">To create this custom environment, you need the latest [Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) in Resource Manager mode (`azure config mode arm`).</span></span> <span data-ttu-id="1844b-115">También necesitará una herramienta de análisis JSON.</span><span class="sxs-lookup"><span data-stu-id="1844b-115">You also need a JSON parsing tool.</span></span> <span data-ttu-id="1844b-116">En este ejemplo se usa [jq](https://stedolan.github.io/jq/).</span><span class="sxs-lookup"><span data-stu-id="1844b-116">This example uses [jq](https://stedolan.github.io/jq/).</span></span>


## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="1844b-117">Versiones de la CLI para completar la tarea</span><span class="sxs-lookup"><span data-stu-id="1844b-117">CLI versions to complete the task</span></span>
<span data-ttu-id="1844b-118">Puede completar la tarea mediante una de las siguientes versiones de la CLI:</span><span class="sxs-lookup"><span data-stu-id="1844b-118">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="1844b-119">[CLI de Azure 1.0](#quick-commands): la CLI para los modelos de implementación clásico y de Resource Manager (este artículo)</span><span class="sxs-lookup"><span data-stu-id="1844b-119">[Azure CLI 1.0](#quick-commands) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="1844b-120">[CLI de Azure 2.0](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json): la CLI de última generación para el modelo de implementación de administración de recursos</span><span class="sxs-lookup"><span data-stu-id="1844b-120">[Azure CLI 2.0](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="1844b-121">Comandos rápidos</span><span class="sxs-lookup"><span data-stu-id="1844b-121">Quick commands</span></span>
<span data-ttu-id="1844b-122">Si necesita realizar rápidamente la tarea, en la siguiente sección se detallan los comandos base para cargar una máquina virtual en Azure.</span><span class="sxs-lookup"><span data-stu-id="1844b-122">If you need to quickly accomplish the task, the following section details the base commands to upload a VM to Azure.</span></span> <span data-ttu-id="1844b-123">En el resto del documento puede encontrar información más detallada y el contexto de cada paso, comenzando [aquí](#detailed-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="1844b-123">More detailed information and context for each step can be found in the rest of the document, starting [here](#detailed-walkthrough).</span></span>

<span data-ttu-id="1844b-124">Asegúrese de haber iniciado sesión en la [CLI de Azure](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 1.0 y que usa el modo de Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="1844b-124">Make sure that you have [the Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) logged in and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="1844b-125">En los ejemplos siguientes, reemplace los nombres de parámetros de ejemplo por los suyos propios.</span><span class="sxs-lookup"><span data-stu-id="1844b-125">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="1844b-126">Los nombres de parámetros de ejemplo incluyen `myResourceGroup`, `mystorageaccount` y `myVM`.</span><span class="sxs-lookup"><span data-stu-id="1844b-126">Example parameter names include `myResourceGroup`, `mystorageaccount`, and `myVM`.</span></span>

<span data-ttu-id="1844b-127">Cree el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="1844b-127">Create the resource group.</span></span> <span data-ttu-id="1844b-128">En el ejemplo siguiente se crea un grupo de recursos denominado `myResourceGroup` en la ubicación `westeurope`:</span><span class="sxs-lookup"><span data-stu-id="1844b-128">The following example creates a resource group named `myResourceGroup` in the `westeurope` location:</span></span>

```azurecli
azure group create -n myResourceGroup -l westeurope
```

<span data-ttu-id="1844b-129">Compruebe el grupo de recursos mediante el analizador JSON:</span><span class="sxs-lookup"><span data-stu-id="1844b-129">Verify the resource group by using the JSON parser:</span></span>

```azurecli
azure group show myResourceGroup --json | jq '.'
```

<span data-ttu-id="1844b-130">Cree la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="1844b-130">Create the storage account.</span></span> <span data-ttu-id="1844b-131">En el ejemplo siguiente se crea una cuenta de almacenamiento denominada `mystorageaccount`.</span><span class="sxs-lookup"><span data-stu-id="1844b-131">The following example creates a storage account named `mystorageaccount`.</span></span> <span data-ttu-id="1844b-132">El nombre de la cuenta de almacenamiento debe ser único, así que indique su propio nombre único.</span><span class="sxs-lookup"><span data-stu-id="1844b-132">(The storage account name must be unique, so provide your own unique name.)</span></span>

```azurecli
azure storage account create -g myResourceGroup -l westeurope \
  --kind Storage --sku-name GRS mystorageaccount
```

<span data-ttu-id="1844b-133">Compruebe la cuenta de almacenamiento mediante el analizador JSON:</span><span class="sxs-lookup"><span data-stu-id="1844b-133">Verify the storage account by using the JSON parser:</span></span>

```azurecli
azure storage account show -g myResourceGroup mystorageaccount --json | jq '.'
```

<span data-ttu-id="1844b-134">Creación de la red virtual.</span><span class="sxs-lookup"><span data-stu-id="1844b-134">Create the virtual network.</span></span> <span data-ttu-id="1844b-135">En el ejemplo siguiente se crea una red virtual denominada `myVnet`:</span><span class="sxs-lookup"><span data-stu-id="1844b-135">The following example creates a virtual network named `myVnet`:</span></span>

```azurecli
azure network vnet create -g myResourceGroup -l westeurope\
  -n myVnet -a 192.168.0.0/16
```

<span data-ttu-id="1844b-136">Cree una subred.</span><span class="sxs-lookup"><span data-stu-id="1844b-136">Create a subnet.</span></span> <span data-ttu-id="1844b-137">En el ejemplo siguiente se crea una subred denominada `mySubnet`:</span><span class="sxs-lookup"><span data-stu-id="1844b-137">The following example creates a subnet named `mySubnet`:</span></span>

```azurecli
azure network vnet subnet create -g myResourceGroup \
  -e myVnet -n mySubnet -a 192.168.1.0/24
```

<span data-ttu-id="1844b-138">Compruebe la red virtual y la subred mediante el analizador JSON:</span><span class="sxs-lookup"><span data-stu-id="1844b-138">Verify the virtual network and subnet by using the JSON parser:</span></span>

```azurecli
azure network vnet show myResourceGroup myVnet --json | jq '.'
```

<span data-ttu-id="1844b-139">Cree una IP pública.</span><span class="sxs-lookup"><span data-stu-id="1844b-139">Create a public IP.</span></span> <span data-ttu-id="1844b-140">En el ejemplo siguiente se crea una IP pública denominada `myPublicIP` con el nombre DNS `mypublicdns`.</span><span class="sxs-lookup"><span data-stu-id="1844b-140">The following example creates a public IP named `myPublicIP` with the DNS name of `mypublicdns`.</span></span> <span data-ttu-id="1844b-141">El nombre DNS debe ser único, así que indique su propio nombre único.</span><span class="sxs-lookup"><span data-stu-id="1844b-141">(The DNS name must be unique, so provide your own unique name.)</span></span>

```azurecli
azure network public-ip create -g myResourceGroup -l westeurope \
  -n myPublicIP  -d mypublicdns -a static -i 4
```

<span data-ttu-id="1844b-142">Cree el equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="1844b-142">Create the load balancer.</span></span> <span data-ttu-id="1844b-143">En el ejemplo siguiente se crea un equilibrador de carga denominado `myLoadBalancer`:</span><span class="sxs-lookup"><span data-stu-id="1844b-143">The following example creates a load balancer named `myLoadBalancer`:</span></span>

```azurecli
azure network lb create -g myResourceGroup -l westeurope -n myLoadBalancer
```

<span data-ttu-id="1844b-144">Cree un grupo IP de front-end para el equilibrador de carga y asocie la IP pública.</span><span class="sxs-lookup"><span data-stu-id="1844b-144">Create a front-end IP pool for the load balancer, and associate the public IP.</span></span> <span data-ttu-id="1844b-145">En el siguiente ejemplo se crea un grupo IP de front-end denominado `mySubnetPool`:</span><span class="sxs-lookup"><span data-stu-id="1844b-145">The following example creates a front-end IP pool named `mySubnetPool`:</span></span>

```azurecli
azure network lb frontend-ip create -g myResourceGroup -l myLoadBalancer \
  -i myPublicIP -n myFrontEndPool
```

<span data-ttu-id="1844b-146">Cree el grupo IP de back-end para el equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="1844b-146">Create the back-end IP pool for the load balancer.</span></span> <span data-ttu-id="1844b-147">En el siguiente ejemplo se crea un grupo IP de back-end denominado `myBackEndPool`:</span><span class="sxs-lookup"><span data-stu-id="1844b-147">The following example creates a back-end IP pool named `myBackEndPool`:</span></span>

```azurecli
azure network lb address-pool create -g myResourceGroup -l myLoadBalancer \
  -n myBackEndPool
```

<span data-ttu-id="1844b-148">Cree reglas NAT (traducción de direcciones de red) de entrada de SSH para el equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="1844b-148">Create SSH inbound network address translation (NAT) rules for the load balancer.</span></span> <span data-ttu-id="1844b-149">En el ejemplo siguiente se crean dos reglas del equilibrador de carga, `myLoadBalancerRuleSSH1` y `myLoadBalancerRuleSSH2`:</span><span class="sxs-lookup"><span data-stu-id="1844b-149">The following example creates two load balancer rules, `myLoadBalancerRuleSSH1` and `myLoadBalancerRuleSSH2`:</span></span>

```azurecli
azure network lb inbound-nat-rule create -g myResourceGroup -l myLoadBalancer \
  -n myLoadBalancerRuleSSH1 -p tcp -f 4222 -b 22
azure network lb inbound-nat-rule create -g myResourceGroup -l myLoadBalancer \
  -n myLoadBalancerRuleSSH2 -p tcp -f 4223 -b 22
```

<span data-ttu-id="1844b-150">Cree las reglas NAT de entrada web para el equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="1844b-150">Create the web inbound NAT rules for the load balancer.</span></span> <span data-ttu-id="1844b-151">En el ejemplo siguiente se crea un regla del equilibrador de carga denominada `myLoadBalancerRuleWeb`:</span><span class="sxs-lookup"><span data-stu-id="1844b-151">The following example creates a load balancer rule named `myLoadBalancerRuleWeb`:</span></span>

```azurecli
azure network lb rule create -g myResourceGroup -l myLoadBalancer \
  -n myLoadBalancerRuleWeb -p tcp -f 80 -b 80 \
  -t myFrontEndPool -o myBackEndPool
```

<span data-ttu-id="1844b-152">Cree el sondeo de estado del equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="1844b-152">Create the load balancer health probe.</span></span> <span data-ttu-id="1844b-153">En el ejemplo siguiente se crea un sondeo de TCP denominado `myHealthProbe`:</span><span class="sxs-lookup"><span data-stu-id="1844b-153">The following example creates a TCP probe named `myHealthProbe`:</span></span>

```azurecli
azure network lb probe create -g myResourceGroup -l myLoadBalancer \
  -n myHealthProbe -p "tcp" -i 15 -c 4
```

<span data-ttu-id="1844b-154">Compruebe el equilibrador de carga, los grupos de direcciones IP y las reglas NAT mediante el analizador JSON:</span><span class="sxs-lookup"><span data-stu-id="1844b-154">Verify the load balancer, IP pools, and NAT rules by using the JSON parser:</span></span>

```azurecli
azure network lb show -g myResourceGroup -n myLoadBalancer --json | jq '.'
```

<span data-ttu-id="1844b-155">Cree la primera tarjeta de interfaz de red (NIC).</span><span class="sxs-lookup"><span data-stu-id="1844b-155">Create the first network interface card (NIC).</span></span> <span data-ttu-id="1844b-156">Reemplace las secciones `#####-###-###` por su propio identificador de suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="1844b-156">Replace the `#####-###-###` sections with your own Azure subscription ID.</span></span> <span data-ttu-id="1844b-157">Su identificador de suscripción se indica en la salida de **jq** al examinar los recursos que va a crear.</span><span class="sxs-lookup"><span data-stu-id="1844b-157">Your subscription ID is noted in the output of **jq** when you examine the resources you are creating.</span></span> <span data-ttu-id="1844b-158">Su identificador de suscripción también puede verlo con `azure account list`.</span><span class="sxs-lookup"><span data-stu-id="1844b-158">You can also view your subscription ID with `azure account list`.</span></span>

<span data-ttu-id="1844b-159">En el ejemplo siguiente se crea una tarjeta de interfaz de red denominada `myNic1`:</span><span class="sxs-lookup"><span data-stu-id="1844b-159">The following example creates a NIC named `myNic1`:</span></span>

```azurecli
azure network nic create -g myResourceGroup -l westeurope \
  -n myNic1 -m myVnet -k mySubnet \
  -d "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool" \
  -e "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1"
```

<span data-ttu-id="1844b-160">Cree la segunda tarjeta de interfaz de red.</span><span class="sxs-lookup"><span data-stu-id="1844b-160">Create the second NIC.</span></span> <span data-ttu-id="1844b-161">En el ejemplo siguiente se crea una tarjeta de interfaz de red denominada `myNic2`:</span><span class="sxs-lookup"><span data-stu-id="1844b-161">The following example creates a NIC named `myNic2`:</span></span>

```azurecli
azure network nic create -g myResourceGroup -l westeurope \
  -n myNic2 -m myVnet -k mySubnet \
  -d "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool" \
  -e "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH2"
```

<span data-ttu-id="1844b-162">Compruebe las dos tarjeta de interfaz de red con el analizador JSON:</span><span class="sxs-lookup"><span data-stu-id="1844b-162">Verify the two NICs by using the JSON parser:</span></span>

```azurecli
azure network nic show myResourceGroup myNic1 --json | jq '.'
azure network nic show myResourceGroup myNic2 --json | jq '.'
```

<span data-ttu-id="1844b-163">Cree el grupo de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="1844b-163">Create the network security group.</span></span> <span data-ttu-id="1844b-164">En el ejemplo siguiente, se crea un grupo de seguridad de red denominado `myNetworkSecurityGroup`:</span><span class="sxs-lookup"><span data-stu-id="1844b-164">The following example creates a network security group named `myNetworkSecurityGroup`:</span></span>

```azurecli
azure network nsg create -g myResourceGroup -l westeurope \
  -n myNetworkSecurityGroup
```

<span data-ttu-id="1844b-165">Agregue dos reglas de entrada para el grupo de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="1844b-165">Add two inbound rules for the network security group.</span></span> <span data-ttu-id="1844b-166">En el ejemplo siguiente se crean dos reglas, `myNetworkSecurityGroupRuleSSH` y `myNetworkSecurityGroupRuleHTTP`:</span><span class="sxs-lookup"><span data-stu-id="1844b-166">The following example creates two rules, `myNetworkSecurityGroupRuleSSH` and `myNetworkSecurityGroupRuleHTTP`:</span></span>

```azurecli
azure network nsg rule create -p tcp -r inbound -y 1000 -u 22 -c allow \
  -g myResourceGroup -a myNetworkSecurityGroup -n myNetworkSecurityGroupRuleSSH
azure network nsg rule create -p tcp -r inbound -y 1001 -u 80 -c allow \
  -g myResourceGroup -a myNetworkSecurityGroup -n myNetworkSecurityGroupRuleHTTP
```

<span data-ttu-id="1844b-167">Compruebe el grupo de seguridad de red y las reglas de entrada mediante el analizador JSON:</span><span class="sxs-lookup"><span data-stu-id="1844b-167">Verify the network security group and inbound rules by using the JSON parser:</span></span>

```azurecli
azure network nsg show -g myResourceGroup -n myNetworkSecurityGroup --json | jq '.'
```

<span data-ttu-id="1844b-168">Enlace el grupo de seguridad de red a las dos tarjetas de interfaz de red:</span><span class="sxs-lookup"><span data-stu-id="1844b-168">Bind the network security group to the two NICs:</span></span>

```azurecli
azure network nic set -g myResourceGroup -o myNetworkSecurityGroup -n myNic1
azure network nic set -g myResourceGroup -o myNetworkSecurityGroup -n myNic2
```

<span data-ttu-id="1844b-169">Cree el conjunto de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="1844b-169">Create the availability set.</span></span> <span data-ttu-id="1844b-170">En el ejemplo siguiente se crea un conjunto de disponibilidad denominado `myAvailabilitySet`:</span><span class="sxs-lookup"><span data-stu-id="1844b-170">The following example creates an availability set named `myAvailabilitySet`:</span></span>

```azurecli
azure availset create -g myResourceGroup -l westeurope -n myAvailabilitySet
```

<span data-ttu-id="1844b-171">Cree la primera máquina virtual Linux.</span><span class="sxs-lookup"><span data-stu-id="1844b-171">Create the first Linux VM.</span></span> <span data-ttu-id="1844b-172">En el ejemplo siguiente se crea una máquina virtual denominada `myVM1`:</span><span class="sxs-lookup"><span data-stu-id="1844b-172">The following example creates a VM named `myVM1`:</span></span>

```azurecli
azure vm create \
    --resource-group myResourceGroup \
    --name myVM1 \
    --location westeurope \
    --os-type linux \
    --availset-name myAvailabilitySet \
    --nic-name myNic1 \
    --vnet-name myVnet \
    --vnet-subnet-name mySubnet \
    --storage-account-name mystorageaccount \
    --image-urn canonical:UbuntuServer:16.04.0-LTS:latest \
    --ssh-publickey-file ~/.ssh/id_rsa.pub \
    --admin-username azureuser
```

<span data-ttu-id="1844b-173">Cree la segunda máquina virtual Linux.</span><span class="sxs-lookup"><span data-stu-id="1844b-173">Create the second Linux VM.</span></span> <span data-ttu-id="1844b-174">En el ejemplo siguiente se crea una máquina virtual denominada `myVM2`:</span><span class="sxs-lookup"><span data-stu-id="1844b-174">The following example creates a VM named `myVM2`:</span></span>

```azurecli
azure vm create \
    --resource-group myResourceGroup \
    --name myVM2 \
    --location westeurope \
    --os-type linux \
    --availset-name myAvailabilitySet \
    --nic-name myNic2 \
    --vnet-name myVnet \
    --vnet-subnet-name mySubnet \
    --storage-account-name mystorageaccount \
    --image-urn canonical:UbuntuServer:16.04.0-LTS:latest \
    --ssh-publickey-file ~/.ssh/id_rsa.pub \
    --admin-username azureuser
```

<span data-ttu-id="1844b-175">Use el analizador JSON para comprobar todo lo que se creó:</span><span class="sxs-lookup"><span data-stu-id="1844b-175">Use the JSON parser to verify that everything that was built:</span></span>

```azurecli
azure vm show -g myResourceGroup -n myVM1 --json | jq '.'
azure vm show -g myResourceGroup -n myVM2 --json | jq '.'
```

<span data-ttu-id="1844b-176">Exporte el entorno compilado a una plantilla para volver a crear rápidamente nuevas instancias:</span><span class="sxs-lookup"><span data-stu-id="1844b-176">Export your new environment to a template to quickly re-create new instances:</span></span>

```azurecli
azure group export myResourceGroup
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="1844b-177">Tutorial detallado</span><span class="sxs-lookup"><span data-stu-id="1844b-177">Detailed walkthrough</span></span>
<span data-ttu-id="1844b-178">A través de los pasos detallados que aparecen a continuación se explica lo que hace cada comando mientras crea su entorno.</span><span class="sxs-lookup"><span data-stu-id="1844b-178">The detailed steps that follow explain what each command is doing as you build out your environment.</span></span> <span data-ttu-id="1844b-179">Estos conceptos sirven de ayuda mientras crea sus propios entornos personalizados con fines de desarrollo o producción.</span><span class="sxs-lookup"><span data-stu-id="1844b-179">These concepts are helpful when you build your own custom environments for development or production.</span></span>

<span data-ttu-id="1844b-180">Asegúrese de haber iniciado sesión en la [CLI de Azure](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 1.0 y que usa el modo de Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="1844b-180">Make sure that you have [the Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) logged in and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="1844b-181">En los ejemplos siguientes, reemplace los nombres de parámetros de ejemplo por los suyos propios.</span><span class="sxs-lookup"><span data-stu-id="1844b-181">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="1844b-182">Los nombres de parámetros de ejemplo incluyen `myResourceGroup`, `mystorageaccount` y `myVM`.</span><span class="sxs-lookup"><span data-stu-id="1844b-182">Example parameter names include `myResourceGroup`, `mystorageaccount`, and `myVM`.</span></span>

## <a name="create-resource-groups-and-choose-deployment-locations"></a><span data-ttu-id="1844b-183">Creación de grupos de recursos y elección de las ubicaciones para la implementación</span><span class="sxs-lookup"><span data-stu-id="1844b-183">Create resource groups and choose deployment locations</span></span>
<span data-ttu-id="1844b-184">Los grupos de recursos de Azure son entidades de implementación lógicas que contienen información de configuración y metadatos que permiten la administración lógica de las implementaciones de recursos.</span><span class="sxs-lookup"><span data-stu-id="1844b-184">Azure resource groups are logical deployment entities that contain configuration information and metadata to enable the logical management of resource deployments.</span></span> <span data-ttu-id="1844b-185">En el ejemplo siguiente se crea un grupo de recursos denominado `myResourceGroup` en la ubicación `westeurope`:</span><span class="sxs-lookup"><span data-stu-id="1844b-185">The following example creates a resource group named `myResourceGroup` in the `westeurope` location:</span></span>

```azurecli
azure group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="1844b-186">Salida:</span><span class="sxs-lookup"><span data-stu-id="1844b-186">Output:</span></span>

```azurecli                        
info:    Executing command group create
+ Getting resource group myResourceGroup
+ Creating resource group myResourceGroup
info:    Created resource group myResourceGroup
data:    Id:                  /subscriptions/guid/resourceGroups/myResourceGroup
data:    Name:                myResourceGroup
data:    Location:            westeurope
data:    Provisioning State:  Succeeded
data:    Tags: null
data:
info:    group create command OK
```

## <a name="create-a-storage-account"></a><span data-ttu-id="1844b-187">Crear una cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="1844b-187">Create a storage account</span></span>
<span data-ttu-id="1844b-188">Las cuentas de almacenamiento son necesarias tanto para los discos de su máquina virtual como para cualquier otro disco de datos adicionales que desee agregar.</span><span class="sxs-lookup"><span data-stu-id="1844b-188">You need storage accounts for your VM disks and for any additional data disks that you want to add.</span></span> <span data-ttu-id="1844b-189">Las cuentas de almacenamiento se crean casi inmediatamente después de crear los grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="1844b-189">You create storage accounts almost immediately after you create resource groups.</span></span>

<span data-ttu-id="1844b-190">Aquí se usa el comando `azure storage account create` , que pasa la ubicación de la cuenta, el grupo de recursos que la controla y el tipo de soporte de almacenamiento que quiere.</span><span class="sxs-lookup"><span data-stu-id="1844b-190">Here we use the `azure storage account create` command, passing the location of the account, the resource group that controls it, and the type of storage support you want.</span></span> <span data-ttu-id="1844b-191">En el ejemplo siguiente se crea una cuenta de almacenamiento denominada `mystorageaccount`:</span><span class="sxs-lookup"><span data-stu-id="1844b-191">The following example creates a storage account named `mystorageaccount`:</span></span>

```azurecli
azure storage account create \  
  --location westeurope \
  --resource-group myResourceGroup \
  --kind Storage --sku-name GRS \
  mystorageaccount
```

<span data-ttu-id="1844b-192">Salida:</span><span class="sxs-lookup"><span data-stu-id="1844b-192">Output:</span></span>

```azurecli
info:    Executing command storage account create
+ Creating storage account
info:    storage account create command OK
```

<span data-ttu-id="1844b-193">Para examinar nuestro grupo de recursos mediante el comando `azure group show`, vamos a usar la herramienta [jq](https://stedolan.github.io/jq/) junto con la opción `--json` de la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="1844b-193">To examine our resource group by using the `azure group show` command, let's use the [jq](https://stedolan.github.io/jq/) tool along with the `--json` Azure CLI option.</span></span> <span data-ttu-id="1844b-194">(Para analizar el código JSON se puede usar **jsawk** o cualquier biblioteca de idioma que prefiera).</span><span class="sxs-lookup"><span data-stu-id="1844b-194">(You can use **jsawk** or any language library you prefer to parse the JSON.)</span></span>

```azurecli
azure group show myResourceGroup --json | jq '.'
```

<span data-ttu-id="1844b-195">Salida:</span><span class="sxs-lookup"><span data-stu-id="1844b-195">Output:</span></span>

```json
{
  "tags": {},
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup",
  "name": "myResourceGroup",
  "provisioningState": "Succeeded",
  "location": "westeurope",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "resources": [
    {
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Storage/storageAccounts/mystorageaccount",
      "name": "mystorageaccount",
      "type": "storageAccounts",
      "location": "westeurope",
      "tags": null
    }
  ],
  "permissions": [
    {
      "actions": [
        "*"
      ],
      "notActions": []
    }
  ]
}
```

<span data-ttu-id="1844b-196">Para investigar la cuenta de almacenamiento mediante la CLI, en primer lugar será preciso establecer primero los nombres y claves de la cuenta.</span><span class="sxs-lookup"><span data-stu-id="1844b-196">To investigate the storage account by using the CLI, you first need to set the account names and keys.</span></span> <span data-ttu-id="1844b-197">Reemplace el nombre de la cuenta de almacenamiento en el siguiente ejemplo por un nombre de su elección:</span><span class="sxs-lookup"><span data-stu-id="1844b-197">Replace the name of the storage account in the following example with a name that you choose:</span></span>

```bash
export AZURE_STORAGE_CONNECTION_STRING="$(azure storage account connectionstring show mystorageaccount --resource-group myResourceGroup --json | jq -r '.string')"
```

<span data-ttu-id="1844b-198">Luego podrá ver la información de almacenamiento fácilmente:</span><span class="sxs-lookup"><span data-stu-id="1844b-198">Then you can view your storage information easily:</span></span>

```azurecli
azure storage container list
```

<span data-ttu-id="1844b-199">Salida:</span><span class="sxs-lookup"><span data-stu-id="1844b-199">Output:</span></span>

```azurecli
info:    Executing command storage container list
+ Getting storage containers
data:    Name  Public-Access  Last-Modified
data:    ----  -------------  -----------------------------
data:    vhds  Off            Sun, 27 Sep 2015 19:03:54 GMT
info:    storage container list command OK
```

## <a name="create-a-virtual-network-and-subnet"></a><span data-ttu-id="1844b-200">Creación de una red virtual y una subred</span><span class="sxs-lookup"><span data-stu-id="1844b-200">Create a virtual network and subnet</span></span>
<span data-ttu-id="1844b-201">Después va a necesitar crear una red virtual que se ejecute en Azure y una subred en la que pueda crear sus máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="1844b-201">Next you're going to need to create a virtual network running in Azure and a subnet in which you can create your VMs.</span></span> <span data-ttu-id="1844b-202">En el ejemplo siguiente se crea una red virtual denominada `myVnet` con un prefijo de la dirección `192.168.0.0/16`:</span><span class="sxs-lookup"><span data-stu-id="1844b-202">The following example creates a virtual network named `myVnet` with the `192.168.0.0/16` address prefix:</span></span>

```azurecli
azure network vnet create --resource-group myResourceGroup --location westeurope \
  --name myVnet --address-prefixes 192.168.0.0/16
```

<span data-ttu-id="1844b-203">Salida:</span><span class="sxs-lookup"><span data-stu-id="1844b-203">Output:</span></span>

```azurecli
info:    Executing command network vnet create
+ Looking up virtual network "myVnet"
+ Creating virtual network "myVnet"
+ Loading virtual network state
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet
data:    Name                            : myVnet
data:    Type                            : Microsoft.Network/virtualNetworks
data:    Location                        : westeurope
data:    ProvisioningState               : Succeeded
data:    Address prefixes:
data:      192.168.0.0/16
info:    network vnet create command OK
```

<span data-ttu-id="1844b-204">Una vez más, vamos a usar la opción --json de `azure group show` y `jq` para ver cómo creamos nuestros recursos.</span><span class="sxs-lookup"><span data-stu-id="1844b-204">Again, let's use the --json option of `azure group show` and `jq` to see how we're building our resources.</span></span> <span data-ttu-id="1844b-205">Ya tenemos un recurso de `storageAccounts` y un recurso de `virtualNetworks`.</span><span class="sxs-lookup"><span data-stu-id="1844b-205">We now have a `storageAccounts` resource and a `virtualNetworks` resource.</span></span>  

```azurecli
azure group show myResourceGroup --json | jq '.'
```

<span data-ttu-id="1844b-206">Salida:</span><span class="sxs-lookup"><span data-stu-id="1844b-206">Output:</span></span>

```json
{
  "tags": {},
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup",
  "name": "myResourceGroup",
  "provisioningState": "Succeeded",
  "location": "westeurope",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "resources": [
    {
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet",
      "name": "myVnet",
      "type": "virtualNetworks",
      "location": "westeurope",
      "tags": null
    },
    {
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Storage/storageAccounts/mystorageaccount",
      "name": "mystorageaccount",
      "type": "storageAccounts",
      "location": "westeurope",
      "tags": null
    }
  ],
  "permissions": [
    {
      "actions": [
        "*"
      ],
      "notActions": []
    }
  ]
}
```

<span data-ttu-id="1844b-207">Ahora vamos a crear una subred en la red virtual `myVnet` en la que se implementan las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="1844b-207">Now let's create a subnet in the `myVnet` virtual network into which the VMs are deployed.</span></span> <span data-ttu-id="1844b-208">Vamos a usar el comando `azure network vnet subnet create`, junto con los recursos que ya hemos creado: el grupo de recursos `myResourceGroup` y la red virtual `myVnet`.</span><span class="sxs-lookup"><span data-stu-id="1844b-208">We use the `azure network vnet subnet create` command, along with the resources we've already created: the `myResourceGroup` resource group and the `myVnet` virtual network.</span></span> <span data-ttu-id="1844b-209">En el ejemplo siguiente, se agrega la subred denominada `mySubnet` con el prefijo de dirección de subred `192.168.1.0/24`:</span><span class="sxs-lookup"><span data-stu-id="1844b-209">In the following example, we add the subnet named `mySubnet` with the subnet address prefix of `192.168.1.0/24`:</span></span>

```azurecli
azure network vnet subnet create --resource-group myResourceGroup \
  --vnet-name myVnet --name mySubnet --address-prefix 192.168.1.0/24
```

<span data-ttu-id="1844b-210">Salida:</span><span class="sxs-lookup"><span data-stu-id="1844b-210">Output:</span></span>

```azurecli
info:    Executing command network vnet subnet create
+ Looking up the subnet "mySubnet"
+ Creating subnet "mySubnet"
+ Looking up the subnet "mySubnet"
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet
data:    Type                            : Microsoft.Network/virtualNetworks/subnets
data:    ProvisioningState               : Succeeded
data:    Name                            : mySubnet
data:    Address prefix                  : 192.168.1.0/24
data:
info:    network vnet subnet create command OK
```

<span data-ttu-id="1844b-211">Dado que la subred está lógicamente dentro de la red virtual, buscamos la información de la subred con un comando un poco diferente.</span><span class="sxs-lookup"><span data-stu-id="1844b-211">Because the subnet is logically inside the virtual network, we look for the subnet information with a slightly different command.</span></span> <span data-ttu-id="1844b-212">El comando que usamos es `azure network vnet show`, pero continuamos examinando la salida JSON mediante `jq`.</span><span class="sxs-lookup"><span data-stu-id="1844b-212">The command we use is `azure network vnet show`, but we continue to examine the JSON output by using `jq`.</span></span>

```azurecli
azure network vnet show myResourceGroup myVnet --json | jq '.'
```

<span data-ttu-id="1844b-213">Salida:</span><span class="sxs-lookup"><span data-stu-id="1844b-213">Output:</span></span>

```json
{
  "subnets": [
    {
      "ipConfigurations": [],
      "addressPrefix": "192.168.1.0/24",
      "provisioningState": "Succeeded",
      "name": "mySubnet",
      "etag": "W/\"974f3e2c-028e-4b35-832b-a4b16ad25eb6\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet"
    }
  ],
  "tags": {},
  "addressSpace": {
    "addressPrefixes": [
      "192.168.0.0/16"
    ]
  },
  "dhcpOptions": {
    "dnsServers": []
  },
  "provisioningState": "Succeeded",
  "etag": "W/\"974f3e2c-028e-4b35-832b-a4b16ad25eb6\"",
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet",
  "name": "myVnet",
  "location": "westeurope"
}
```

## <a name="create-a-public-ip-address"></a><span data-ttu-id="1844b-214">Crear una dirección IP pública</span><span class="sxs-lookup"><span data-stu-id="1844b-214">Create a public IP address</span></span>
<span data-ttu-id="1844b-215">Ahora, vamos a crear la dirección IP pública (PIP) que asignamos a su equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="1844b-215">Now let's create the public IP address (PIP) that we assign to your load balancer.</span></span> <span data-ttu-id="1844b-216">Le permite conectarse a sus máquinas virtuales desde Internet mediante el comando `azure network public-ip create` .</span><span class="sxs-lookup"><span data-stu-id="1844b-216">It enables you to connect to your VMs from the Internet by using the `azure network public-ip create` command.</span></span> <span data-ttu-id="1844b-217">Dado que la dirección predeterminada es dinámica, creamos una entrada DNS con nombre en el dominio **cloudapp.azure.com** con la opción `--domain-name-label`.</span><span class="sxs-lookup"><span data-stu-id="1844b-217">Because the default address is dynamic, we create a named DNS entry in the **cloudapp.azure.com** domain by using the `--domain-name-label` option.</span></span> <span data-ttu-id="1844b-218">En el ejemplo siguiente se crea una IP pública denominada `myPublicIP` con el nombre DNS `mypublicdns`.</span><span class="sxs-lookup"><span data-stu-id="1844b-218">The following example creates a public IP named `myPublicIP` with the DNS name of `mypublicdns`.</span></span> <span data-ttu-id="1844b-219">Como el nombre DNS debe ser único, especifique su propio nombre DNS único:</span><span class="sxs-lookup"><span data-stu-id="1844b-219">Because the DNS name must be unique, you provide your own unique DNS name:</span></span>

```azurecli
azure network public-ip create --resource-group myResourceGroup \
  --location westeurope --name myPublicIP --domain-name-label mypublicdns
```

<span data-ttu-id="1844b-220">Salida:</span><span class="sxs-lookup"><span data-stu-id="1844b-220">Output:</span></span>

```azurecli
info:    Executing command network public-ip create
+ Looking up the public ip "myPublicIP"
+ Creating public ip address "myPublicIP"
+ Looking up the public ip "myPublicIP"
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP
data:    Name                            : myPublicIP
data:    Type                            : Microsoft.Network/publicIPAddresses
data:    Location                        : westeurope
data:    Provisioning state              : Succeeded
data:    Allocation method               : Dynamic
data:    Idle timeout                    : 4
data:    Domain name label               : mypublicdns
data:    FQDN                            : mypublicdns.westeurope.cloudapp.azure.com
info:    network public-ip create command OK
```

<span data-ttu-id="1844b-221">La dirección IP pública también es un recurso de nivel superior, por lo que se puede ver con `azure group show`.</span><span class="sxs-lookup"><span data-stu-id="1844b-221">The public IP address is also a top-level resource, so you can see it with `azure group show`.</span></span>

```azurecli
azure group show myResourceGroup --json | jq '.'
```

<span data-ttu-id="1844b-222">Salida:</span><span class="sxs-lookup"><span data-stu-id="1844b-222">Output:</span></span>

```json
{
"tags": {},
"id": "/subscriptions/guid/resourceGroups/myResourceGroup",
"name": "myResourceGroup",
"provisioningState": "Succeeded",
"location": "westeurope",
"properties": {
    "provisioningState": "Succeeded"
},
"resources": [
    {
    "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP",
    "name": "myPublicIP",
    "type": "publicIPAddresses",
    "location": "westeurope",
    "tags": null
    },
    {
    "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet",
    "name": "myVnet",
    "type": "virtualNetworks",
    "location": "westeurope",
    "tags": null
    },
    {
    "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Storage/storageAccounts/mystorageaccount",
    "name": "mystorageaccount",
    "type": "storageAccounts",
    "location": "westeurope",
    "tags": null
    }
],
"permissions": [
    {
    "actions": [
        "*"
    ],
    "notActions": []
    }
]
}
```

<span data-ttu-id="1844b-223">Puede investigar más detalles del recurso, incluido el nombre de dominio completo (FQDN) del subdominio, mediante el comando `azure network public-ip show` completo.</span><span class="sxs-lookup"><span data-stu-id="1844b-223">You can investigate more resource details, including the fully qualified domain name (FQDN) of the subdomain, by using the complete `azure network public-ip show` command.</span></span> <span data-ttu-id="1844b-224">El recurso de la dirección IP pública se ha asignado de forma lógica, pero aún no hay ninguna dirección específica asignada.</span><span class="sxs-lookup"><span data-stu-id="1844b-224">The public IP address resource has been allocated logically, but a specific address has not yet been assigned.</span></span> <span data-ttu-id="1844b-225">Para obtener una dirección IP, va a necesitar un equilibrador de carga, que todavía no se ha creado.</span><span class="sxs-lookup"><span data-stu-id="1844b-225">To obtain an IP address, you're going to need a load balancer, which we have not yet created.</span></span>

```azurecli
azure network public-ip show myResourceGroup myPublicIP --json | jq '.'
```

<span data-ttu-id="1844b-226">Salida:</span><span class="sxs-lookup"><span data-stu-id="1844b-226">Output:</span></span>

```json
{
"tags": {},
"publicIpAllocationMethod": "Dynamic",
"dnsSettings": {
    "domainNameLabel": "mypublicdns",
    "fqdn": "mypublicdns.westeurope.cloudapp.azure.com"
},
"idleTimeoutInMinutes": 4,
"provisioningState": "Succeeded",
"etag": "W/\"c63154b3-1130-49b9-a887-877d74d5ebc5\"",
"id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP",
"name": "myPublicIP",
"location": "westeurope"
}
```

## <a name="create-a-load-balancer-and-ip-pools"></a><span data-ttu-id="1844b-227">Creación de un equilibrador de carga y grupos de direcciones IP</span><span class="sxs-lookup"><span data-stu-id="1844b-227">Create a load balancer and IP pools</span></span>
<span data-ttu-id="1844b-228">Al crear un equilibrador de carga, puede distribuir el tráfico en varias máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="1844b-228">When you create a load balancer, it enables you to distribute traffic across multiple VMs.</span></span> <span data-ttu-id="1844b-229">También proporciona redundancia a la aplicación mediante la ejecución de varias máquinas virtuales que responden a las solicitudes de los usuarios en caso de que haya tareas de mantenimiento o cargas elevadas.</span><span class="sxs-lookup"><span data-stu-id="1844b-229">It also provides redundancy to your application by running multiple VMs that respond to user requests in the event of maintenance or heavy loads.</span></span> <span data-ttu-id="1844b-230">En el ejemplo siguiente se crea un equilibrador de carga denominado `myLoadBalancer`:</span><span class="sxs-lookup"><span data-stu-id="1844b-230">The following example creates a load balancer named `myLoadBalancer`:</span></span>

```azurecli
azure network lb create --resource-group myResourceGroup --location westeurope \
  --name myLoadBalancer
```

<span data-ttu-id="1844b-231">Salida:</span><span class="sxs-lookup"><span data-stu-id="1844b-231">Output:</span></span>

```azurecli
info:    Executing command network lb create
+ Looking up the load balancer "myLoadBalancer"
+ Creating load balancer "myLoadBalancer"
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer
data:    Name                            : myLoadBalancer
data:    Type                            : Microsoft.Network/loadBalancers
data:    Location                        : westeurope
data:    Provisioning state              : Succeeded
info:    network lb create command OK
```

<span data-ttu-id="1844b-232">Nuestro equilibrador de carga está bastante vacío, así que vamos a crear algunos grupos de direcciones IP.</span><span class="sxs-lookup"><span data-stu-id="1844b-232">Our load balancer is fairly empty, so let's create some IP pools.</span></span> <span data-ttu-id="1844b-233">Deseamos crear dos grupos IP para nuestro equilibrador de carga: uno para el front-end y otro para el back-end.</span><span class="sxs-lookup"><span data-stu-id="1844b-233">We want to create two IP pools for our load balancer, one for the front end and one for the back end.</span></span> <span data-ttu-id="1844b-234">El grupo de direcciones IP front-end se ve de forma pública.</span><span class="sxs-lookup"><span data-stu-id="1844b-234">The front-end IP pool is publicly visible.</span></span> <span data-ttu-id="1844b-235">También es la ubicación a la que asignamos la PIP creada antes.</span><span class="sxs-lookup"><span data-stu-id="1844b-235">It's also the location to which we assign the PIP that we created earlier.</span></span> <span data-ttu-id="1844b-236">A continuación, usamos el grupo back-end como ubicación de conexión para nuestras máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="1844b-236">Then we use the back-end pool as a location for our VMs to connect to.</span></span> <span data-ttu-id="1844b-237">De este modo, el tráfico puede fluir a través del equilibrador de carga hacia las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="1844b-237">That way, the traffic can flow through the load balancer to the VMs.</span></span>

<span data-ttu-id="1844b-238">En primer lugar, vamos a crear nuestro grupo IP de front-end.</span><span class="sxs-lookup"><span data-stu-id="1844b-238">First, let's create our front-end IP pool.</span></span> <span data-ttu-id="1844b-239">En el siguiente ejemplo se crea un grupo de front-end denominado `myFrontEndPool`:</span><span class="sxs-lookup"><span data-stu-id="1844b-239">The following example creates a front-end pool named `myFrontEndPool`:</span></span>

```azurecli
azure network lb frontend-ip create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --public-ip-name myPublicIP \
  --name myFrontEndPool
```

<span data-ttu-id="1844b-240">Salida:</span><span class="sxs-lookup"><span data-stu-id="1844b-240">Output:</span></span>

```azurecli
info:    Executing command network lb frontend-ip create
+ Looking up the load balancer "myLoadBalancer"
+ Looking up the public ip "myPublicIP"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myFrontEndPool
data:    Provisioning state              : Succeeded
data:    Private IP allocation method    : Dynamic
data:    Public IP address id            : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP
info:    network lb mySubnet-ip create command OK
```

<span data-ttu-id="1844b-241">Tenga en cuenta cómo se ha usado el modificador `--public-ip-name` para pasar el `myPublicIP` creado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="1844b-241">Note how we used the `--public-ip-name` switch to pass in the `myPublicIP` that we created earlier.</span></span> <span data-ttu-id="1844b-242">Asignar la dirección IP pública al equilibrador de carga le permite comunicarse con sus máquinas virtuales a través de Internet.</span><span class="sxs-lookup"><span data-stu-id="1844b-242">Assigning the public IP address to the load balancer allows you to reach your VMs across the Internet.</span></span>

<span data-ttu-id="1844b-243">Después, vamos a crear nuestro el grupo IP, esta vez para el tráfico de back-end.</span><span class="sxs-lookup"><span data-stu-id="1844b-243">Next, let's create our second IP pool, this time for our back-end traffic.</span></span> <span data-ttu-id="1844b-244">En el siguiente ejemplo se crea un grupo de back-end denominado `myBackEndPool`:</span><span class="sxs-lookup"><span data-stu-id="1844b-244">The following example creates a back-end pool named `myBackEndPool`:</span></span>

```azurecli
azure network lb address-pool create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myBackEndPool
```

<span data-ttu-id="1844b-245">Salida:</span><span class="sxs-lookup"><span data-stu-id="1844b-245">Output:</span></span>

```azurecli
info:    Executing command network lb address-pool create
+ Looking up the load balancer "myLoadBalancer"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myBackEndPool
data:    Provisioning state              : Succeeded
info:    network lb address-pool create command OK
```

<span data-ttu-id="1844b-246">Podemos ver cómo está el equilibrador de carga buscando la salida JSON con `azure network lb show` y examinándolo:</span><span class="sxs-lookup"><span data-stu-id="1844b-246">We can see how our load balancer is doing by looking with `azure network lb show` and examining the JSON output:</span></span>

```azurecli
azure network lb show myResourceGroup myLoadBalancer --json | jq '.'
```

<span data-ttu-id="1844b-247">Salida:</span><span class="sxs-lookup"><span data-stu-id="1844b-247">Output:</span></span>

```json
{
  "etag": "W/\"29c38649-77d6-43ff-ab8f-977536b0047c\"",
  "provisioningState": "Succeeded",
  "resourceGuid": "f1446acb-09ba-44d9-b8b6-849d9983dc09",
  "outboundNatRules": [],
  "inboundNatPools": [],
  "inboundNatRules": [],
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer",
  "name": "myLoadBalancer",
  "type": "Microsoft.Network/loadBalancers",
  "location": "westeurope",
  "mySubnetIPConfigurations": [
    {
      "etag": "W/\"29c38649-77d6-43ff-ab8f-977536b0047c\"",
      "name": "myFrontEndPool",
      "provisioningState": "Succeeded",
      "publicIPAddress": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP"
      },
      "privateIPAllocationMethod": "Dynamic",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
    }
  ],
  "backendAddressPools": [
    {
      "etag": "W/\"29c38649-77d6-43ff-ab8f-977536b0047c\"",
      "name": "myBackEndPool",
      "provisioningState": "Succeeded",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool"
    }
  ],
  "loadBalancingRules": [],
  "probes": []
}
```

## <a name="create-load-balancer-nat-rules"></a><span data-ttu-id="1844b-248">Creación de reglas NAT del equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="1844b-248">Create load balancer NAT rules</span></span>
<span data-ttu-id="1844b-249">Para que el tráfico fluya a través de nuestro equilibrador de carga, es preciso crear reglas NAT (traducción de direcciones de red) que especifiquen acciones de entrada o de salida.</span><span class="sxs-lookup"><span data-stu-id="1844b-249">To get traffic flowing through our load balancer, we need to create network address translation (NAT) rules that specify either inbound or outbound actions.</span></span> <span data-ttu-id="1844b-250">Puede determinar el protocolo que va a usarse y, luego, asignar los puertos externos a los internos que desee.</span><span class="sxs-lookup"><span data-stu-id="1844b-250">You can specify the protocol to use, then map external ports to internal ports as desired.</span></span> <span data-ttu-id="1844b-251">Para nuestro entorno, vamos a crear algunas reglas que habiliten SSH en nuestras máquinas virtuales a través de nuestro equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="1844b-251">For our environment, let's create some rules that allow SSH through our load balancer to our VMs.</span></span> <span data-ttu-id="1844b-252">Configuramos los puertos TCP 4222 y 4223 para dirigir el tráfico al puerto TCP 22 de nuestras máquinas virtuales (que crearemos más adelante).</span><span class="sxs-lookup"><span data-stu-id="1844b-252">We set up TCP ports 4222 and 4223 to direct to TCP port 22 on our VMs (which we create later).</span></span> <span data-ttu-id="1844b-253">En el ejemplo siguiente, se crea una regla denominada `myLoadBalancerRuleSSH1` para asignar el tráfico del puerto TCP 4222 al puerto 22:</span><span class="sxs-lookup"><span data-stu-id="1844b-253">The following example creates a rule named `myLoadBalancerRuleSSH1` to map TCP port 4222 to port 22:</span></span>

```azurecli
azure network lb inbound-nat-rule create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myLoadBalancerRuleSSH1 \
  --protocol tcp --frontend-port 4222 --backend-port 22
```

<span data-ttu-id="1844b-254">Salida:</span><span class="sxs-lookup"><span data-stu-id="1844b-254">Output:</span></span>

```azurecli
info:    Executing command network lb inbound-nat-rule create
+ Looking up the load balancer "myLoadBalancer"
warn:    Using default enable floating ip: false
warn:    Using default idle timeout: 4
warn:    Using default mySubnet IP configuration "myFrontEndPool"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myLoadBalancerRuleSSH1
data:    Provisioning state              : Succeeded
data:    Protocol                        : Tcp
data:    mySubnet port                   : 4222
data:    Backend port                    : 22
data:    Enable floating IP              : false
data:    Idle timeout in minutes         : 4
data:    mySubnet IP configuration id    : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool
info:    network lb inbound-nat-rule create command OK
```

<span data-ttu-id="1844b-255">Repita el procedimiento con la segunda regla NAT para SSH.</span><span class="sxs-lookup"><span data-stu-id="1844b-255">Repeat the procedure for your second NAT rule for SSH.</span></span> <span data-ttu-id="1844b-256">En el ejemplo siguiente se crea una regla denominada `myLoadBalancerRuleSSH2` para asignar el tráfico del puerto TCP 4223 al puerto 22:</span><span class="sxs-lookup"><span data-stu-id="1844b-256">The following example creates a rule named `myLoadBalancerRuleSSH2` to map TCP port 4223 to port 22:</span></span>

```azurecli
azure network lb inbound-nat-rule create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myLoadBalancerRuleSSH2 --protocol tcp \
  --frontend-port 4223 --backend-port 22
```

<span data-ttu-id="1844b-257">Continuemos y creemos una regla NAT para el puerto TCP 80 para tráfico web, que enlaza la regla a nuestros grupos IP.</span><span class="sxs-lookup"><span data-stu-id="1844b-257">Let's also go ahead and create a NAT rule for TCP port 80 for web traffic, hooking the rule up to our IP pools.</span></span> <span data-ttu-id="1844b-258">Si enlazamos la regla a un grupo de direcciones IP, en lugar de enlazarla a nuestras máquinas virtuales individualmente, podemos agregar o quitar máquinas virtuales del grupo de direcciones IP.</span><span class="sxs-lookup"><span data-stu-id="1844b-258">If we hook up the rule to an IP pool, instead of hooking up the rule to our VMs individually, we can add or remove VMs from the IP pool.</span></span> <span data-ttu-id="1844b-259">El equilibrador de carga ajusta automáticamente el flujo de tráfico.</span><span class="sxs-lookup"><span data-stu-id="1844b-259">The load balancer automatically adjusts the flow of traffic.</span></span> <span data-ttu-id="1844b-260">En el ejemplo siguiente, se crea una regla denominada `myLoadBalancerRuleWeb` para asignar el tráfico del puerto TCP 80 al puerto 80:</span><span class="sxs-lookup"><span data-stu-id="1844b-260">The following example creates a rule named `myLoadBalancerRuleWeb` to map TCP port 80 to port 80:</span></span>

```azurecli
azure network lb rule create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myLoadBalancerRuleWeb --protocol tcp \
  --frontend-port 80 --backend-port 80 --frontend-ip-name myFrontEndPool \
  --backend-address-pool-name myBackEndPool
```

<span data-ttu-id="1844b-261">Salida:</span><span class="sxs-lookup"><span data-stu-id="1844b-261">Output:</span></span>

```azurecli
info:    Executing command network lb rule create
+ Looking up the load balancer "myLoadBalancer"
warn:    Using default idle timeout: 4
warn:    Using default enable floating ip: false
warn:    Using default load distribution: Default
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myLoadBalancerRuleWeb
data:    Provisioning state              : Succeeded
data:    Protocol                        : Tcp
data:    mySubnet port                   : 80
data:    Backend port                    : 80
data:    Enable floating IP              : false
data:    Load distribution               : Default
data:    Idle timeout in minutes         : 4
data:    mySubnet IP configuration id    : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool
data:    Backend address pool id         : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool
info:    network lb rule create command OK
```

## <a name="create-a-load-balancer-health-probe"></a><span data-ttu-id="1844b-262">Creación del sondeo de estado de un equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="1844b-262">Create a load balancer health probe</span></span>
<span data-ttu-id="1844b-263">Una acción de sondeo de estado comprueba periódicamente las máquinas virtuales que están detrás de nuestro equilibrador de carga para asegurarse de que funcionan y responden a las solicitudes, tal como se define.</span><span class="sxs-lookup"><span data-stu-id="1844b-263">A health probe periodically checks on the VMs that are behind our load balancer to make sure they're operating and responding to requests as defined.</span></span> <span data-ttu-id="1844b-264">De lo contrario, se quitarán de la operación para asegurarse de que no se redirigen los usuarios a dichas máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="1844b-264">If not, they're removed from operation to ensure that users aren't being directed to them.</span></span> <span data-ttu-id="1844b-265">Puede definir comprobaciones personalizadas para el sondeo de estado, junto con intervalos y valores de tiempo de espera.</span><span class="sxs-lookup"><span data-stu-id="1844b-265">You can define custom checks for the health probe, along with intervals and timeout values.</span></span> <span data-ttu-id="1844b-266">Para más información sobre los sondeos de estado, consulte [Sondeos del Equilibrador de carga](../../load-balancer/load-balancer-custom-probe-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1844b-266">For more information about health probes, see [Load Balancer probes](../../load-balancer/load-balancer-custom-probe-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="1844b-267">En el ejemplo siguiente se crea un sondeo del estado del TCP denominado `myHealthProbe`:</span><span class="sxs-lookup"><span data-stu-id="1844b-267">The following example creates a TCP health probed named `myHealthProbe`:</span></span>

```azurecli
azure network lb probe create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myHealthProbe --protocol "tcp" \
  --interval 15 --count 4
```

<span data-ttu-id="1844b-268">Salida:</span><span class="sxs-lookup"><span data-stu-id="1844b-268">Output:</span></span>

```azurecli
info:    Executing command network lb probe create
warn:    Using default probe port: 80
+ Looking up the load balancer "myLoadBalancer"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myHealthProbe
data:    Provisioning state              : Succeeded
data:    Protocol                        : Tcp
data:    Port                            : 80
data:    Interval in seconds             : 15
data:    Number of probes                : 4
info:    network lb probe create command OK
```

<span data-ttu-id="1844b-269">Aquí, especificamos un intervalo de 15 segundos para las comprobaciones de estado.</span><span class="sxs-lookup"><span data-stu-id="1844b-269">Here, we specified an interval of 15 seconds for our health checks.</span></span> <span data-ttu-id="1844b-270">Podemos perder un máximo de cuatro sondeos (un minuto) antes de que el equilibrador de carga considere que el host ha dejado de funcionar.</span><span class="sxs-lookup"><span data-stu-id="1844b-270">We can miss a maximum of four probes (one minute) before the load balancer considers that the host is no longer functioning.</span></span>

## <a name="verify-the-load-balancer"></a><span data-ttu-id="1844b-271">Comprobación del equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="1844b-271">Verify the load balancer</span></span>
<span data-ttu-id="1844b-272">Ahora se ha realizado la configuración del equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="1844b-272">Now the load balancer configuration is done.</span></span> <span data-ttu-id="1844b-273">Estos son los pasos adoptados:</span><span class="sxs-lookup"><span data-stu-id="1844b-273">Here are the steps you took:</span></span>

1. <span data-ttu-id="1844b-274">Creó un equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="1844b-274">You created a load balancer.</span></span>
2. <span data-ttu-id="1844b-275">Creó un grupo de direcciones IP front-end y asignó una dirección IP pública al mismo.</span><span class="sxs-lookup"><span data-stu-id="1844b-275">You created a front-end IP pool and assigned a public IP to it.</span></span>
3. <span data-ttu-id="1844b-276">Creó un grupo de direcciones IP back-end al que pueden conectarse las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="1844b-276">You created a back-end IP pool that VMs can connect to.</span></span>
4. <span data-ttu-id="1844b-277">Creó reglas NAT que permiten SSH en las máquinas virtuales con fines de administración, junto con una regla que permite el puerto TCP 80 en nuestra aplicación web.</span><span class="sxs-lookup"><span data-stu-id="1844b-277">You created NAT rules that allow SSH to the VMs for management, along with a rule that allows TCP port 80 for our web app.</span></span>
5. <span data-ttu-id="1844b-278">Agregó un sondeo de estado para comprobar periódicamente las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="1844b-278">You added a health probe to periodically check the VMs.</span></span> <span data-ttu-id="1844b-279">Este sondeo de estado garantiza que los usuarios no intenten acceder a una máquina virtual que ya no funciona ni proporciona contenido.</span><span class="sxs-lookup"><span data-stu-id="1844b-279">This health probe ensures that users don't try to access a VM that is no longer functioning or serving content.</span></span>

<span data-ttu-id="1844b-280">Revisemos cuál es ahora el aspecto del equilibrador de carga:</span><span class="sxs-lookup"><span data-stu-id="1844b-280">Let's review what your load balancer looks like now:</span></span>

```azurecli
azure network lb show --resource-group myResourceGroup \
  --name myLoadBalancer --json | jq '.'
```

<span data-ttu-id="1844b-281">Salida:</span><span class="sxs-lookup"><span data-stu-id="1844b-281">Output:</span></span>

```json
{
  "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
  "provisioningState": "Succeeded",
  "resourceGuid": "f1446acb-09ba-44d9-b8b6-849d9983dc09",
  "outboundNatRules": [],
  "inboundNatPools": [],
  "inboundNatRules": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myLoadBalancerRuleSSH1",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1",
      "mySubnetIPConfiguration": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
      },
      "protocol": "Tcp",
      "mySubnetPort": 4222,
      "backendPort": 22,
      "idleTimeoutInMinutes": 4,
      "enableFloatingIP": false,
      "provisioningState": "Succeeded"
    },
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myLoadBalancerRuleSSH2",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH2",
      "mySubnetIPConfiguration": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
      },
      "protocol": "Tcp",
      "mySubnetPort": 4223,
      "backendPort": 22,
      "idleTimeoutInMinutes": 4,
      "enableFloatingIP": false,
      "provisioningState": "Succeeded"
    }
  ],
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer",
  "name": "myLoadBalancer",
  "type": "Microsoft.Network/loadBalancers",
  "location": "westeurope",
  "mySubnetIPConfigurations": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myFrontEndPool",
      "provisioningState": "Succeeded",
      "publicIPAddress": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP"
      },
      "privateIPAllocationMethod": "Dynamic",
      "loadBalancingRules": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/loadBalancingRules/myLoadBalancerRuleWeb"
        }
      ],
      "inboundNatRules": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1"
        },
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH2"
        }
      ],
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
    }
  ],
  "backendAddressPools": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myBackEndPool",
      "provisioningState": "Succeeded",
      "loadBalancingRules": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/loadBalancingRules/myLoadBalancerRuleWeb"
        }
      ],
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool"
    }
  ],
  "loadBalancingRules": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myLoadBalancerRuleWeb",
      "provisioningState": "Succeeded",
      "enableFloatingIP": false,
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/loadBalancingRules/myLoadBalancerRuleWeb",
      "mySubnetIPConfiguration": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
      },
      "backendAddressPool": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool"
      },
      "protocol": "Tcp",
      "loadDistribution": "Default",
      "mySubnetPort": 80,
      "backendPort": 80,
      "idleTimeoutInMinutes": 4
    }
  ],
  "probes": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myHealthProbe",
      "provisioningState": "Succeeded",
      "numberOfProbes": 4,
      "intervalInSeconds": 15,
      "port": 80,
      "protocol": "Tcp",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/probes/myHealthProbe"
    }
  ]
}
```

## <a name="create-an-nic-to-use-with-the-linux-vm"></a><span data-ttu-id="1844b-282">Creación de una NIC para usarla con la máquina virtual Linux</span><span class="sxs-lookup"><span data-stu-id="1844b-282">Create an NIC to use with the Linux VM</span></span>
<span data-ttu-id="1844b-283">Las NIC están disponibles de manera programática porque puede aplicar reglas a su uso.</span><span class="sxs-lookup"><span data-stu-id="1844b-283">NICs are programmatically available because you can apply rules to their use.</span></span> <span data-ttu-id="1844b-284">También puede tener más de una.</span><span class="sxs-lookup"><span data-stu-id="1844b-284">You can also have more than one.</span></span> <span data-ttu-id="1844b-285">En el siguiente comando `azure network nic create` se enlaza la NIC al grupo de direcciones IP back-end de carga y se asocia a la regla NAT para permitir el tráfico SSH.</span><span class="sxs-lookup"><span data-stu-id="1844b-285">In the following `azure network nic create` command, you hook up the NIC to the load back-end IP pool and associate it with the NAT rule to permit SSH traffic.</span></span>

<span data-ttu-id="1844b-286">Reemplace las secciones `#####-###-###` por su propio identificador de suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="1844b-286">Replace the `#####-###-###` sections with your own Azure subscription ID.</span></span> <span data-ttu-id="1844b-287">Su identificador de suscripción se indica en la salida de `jq` al examinar los recursos que va a crear.</span><span class="sxs-lookup"><span data-stu-id="1844b-287">Your subscription ID is noted in the output of `jq` when you examine the resources you are creating.</span></span> <span data-ttu-id="1844b-288">Su identificador de suscripción también puede verlo con `azure account list`.</span><span class="sxs-lookup"><span data-stu-id="1844b-288">You can also view your subscription ID with `azure account list`.</span></span>

<span data-ttu-id="1844b-289">En el ejemplo siguiente se crea una tarjeta de interfaz de red denominada `myNic1`:</span><span class="sxs-lookup"><span data-stu-id="1844b-289">The following example creates a NIC named `myNic1`:</span></span>

```azurecli
azure network nic create --resource-group myResourceGroup --location westeurope \
  --subnet-vnet-name myVnet --subnet-name mySubnet --name myNic1 \
  --lb-address-pool-ids /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool \
  --lb-inbound-nat-rule-ids /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1
```

<span data-ttu-id="1844b-290">Salida:</span><span class="sxs-lookup"><span data-stu-id="1844b-290">Output:</span></span>

```azurecli
info:    Executing command network nic create
+ Looking up the subnet "mySubnet"
+ Looking up the network interface "myNic1"
+ Creating network interface "myNic1"
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNic1
data:    Name                            : myNic1
data:    Type                            : Microsoft.Network/networkInterfaces
data:    Location                        : westeurope
data:    Provisioning state              : Succeeded
data:    Enable IP forwarding            : false
data:    IP configurations:
data:      Name                          : Nic-IP-config
data:      Provisioning state            : Succeeded
data:      Private IP address            : 192.168.1.4
data:      Private IP allocation method  : Dynamic
data:      Subnet                        : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet
data:      Load balancer backend address pools:
data:        Id                          : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool
data:      Load balancer inbound NAT rules:
data:        Id                          : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1
data:
info:    network nic create command OK
```

<span data-ttu-id="1844b-291">Para ver los detalles, examine directamente el recurso.</span><span class="sxs-lookup"><span data-stu-id="1844b-291">You can see the details by examining the resource directly.</span></span> <span data-ttu-id="1844b-292">Examine el recurso mediante el comando `azure network nic show` :</span><span class="sxs-lookup"><span data-stu-id="1844b-292">You examine the resource by using the `azure network nic show` command:</span></span>

```azurecli
azure network nic show myResourceGroup myNic1 --json | jq '.'
```

<span data-ttu-id="1844b-293">Salida:</span><span class="sxs-lookup"><span data-stu-id="1844b-293">Output:</span></span>

```json
{
  "etag": "W/\"fc1eaaa1-ee55-45bd-b847-5a08c7f4264a\"",
  "provisioningState": "Succeeded",
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNic1",
  "name": "myNic1",
  "type": "Microsoft.Network/networkInterfaces",
  "location": "westeurope",
  "ipConfigurations": [
    {
      "etag": "W/\"fc1eaaa1-ee55-45bd-b847-5a08c7f4264a\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNic1/ipConfigurations/Nic-IP-config",
      "loadBalancerBackendAddressPools": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool"
        }
      ],
      "loadBalancerInboundNatRules": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1"
        }
      ],
      "privateIPAddress": "192.168.1.4",
      "privateIPAllocationMethod": "Dynamic",
      "subnet": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet"
      },
      "provisioningState": "Succeeded",
      "name": "Nic-IP-config"
    }
  ],
  "dnsSettings": {
    "appliedDnsServers": [],
    "dnsServers": []
  },
  "enableIPForwarding": false,
  "resourceGuid": "a20258b8-6361-45f6-b1b4-27ffed28798c"
}
```

<span data-ttu-id="1844b-294">Ahora vamos a crear la segunda NIC, que, de nuevo, se enlaza a nuestro grupo de direcciones IP back-end.</span><span class="sxs-lookup"><span data-stu-id="1844b-294">Now we create the second NIC, hooking in to our back-end IP pool again.</span></span> <span data-ttu-id="1844b-295">Esta vez, la segunda regla NAT permite el tráfico SSH.</span><span class="sxs-lookup"><span data-stu-id="1844b-295">This time the second NAT rule permits SSH traffic.</span></span> <span data-ttu-id="1844b-296">En el ejemplo siguiente se crea una tarjeta de interfaz de red denominada `myNic2`:</span><span class="sxs-lookup"><span data-stu-id="1844b-296">The following example creates a NIC named `myNic2`:</span></span>

```azurecli
azure network nic create --resource-group myResourceGroup --location westeurope \
  --subnet-vnet-name myVnet --subnet-name mySubnet --name myNic2 \
  --lb-address-pool-ids  /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool \
  --lb-inbound-nat-rule-ids /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH2
```

## <a name="create-a-network-security-group-and-rules"></a><span data-ttu-id="1844b-297">Creación de un grupo de seguridad de red (NSG) y las reglas</span><span class="sxs-lookup"><span data-stu-id="1844b-297">Create a network security group and rules</span></span>
<span data-ttu-id="1844b-298">Ahora creamos un grupo de seguridad de red y las reglas de entrada que rigen el acceso a la tarjeta de interfaz de red.</span><span class="sxs-lookup"><span data-stu-id="1844b-298">Now we create a network security group and the inbound rules that govern access to the NIC.</span></span> <span data-ttu-id="1844b-299">Un grupo de seguridad de red puede aplicarse a una tarjeta de interfaz de red o a una subred.</span><span class="sxs-lookup"><span data-stu-id="1844b-299">A network security group can be applied to a NIC or subnet.</span></span> <span data-ttu-id="1844b-300">Defina reglas para controlar el flujo de tráfico que entra y sale de las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="1844b-300">You define rules to control the flow of traffic in and out of your VMs.</span></span> <span data-ttu-id="1844b-301">En el ejemplo siguiente, se crea un grupo de seguridad de red denominado `myNetworkSecurityGroup`:</span><span class="sxs-lookup"><span data-stu-id="1844b-301">The following example creates a network security group named `myNetworkSecurityGroup`:</span></span>

```azurecli
azure network nsg create --resource-group myResourceGroup --location westeurope \
  --name myNetworkSecurityGroup
```

<span data-ttu-id="1844b-302">Vamos a agregar la regla de entrada del NSG para permitir conexiones de entrada en el puerto 22 (para admitir SSH).</span><span class="sxs-lookup"><span data-stu-id="1844b-302">Let's add the inbound rule for the NSG to allow inbound connections on port 22 (to support SSH).</span></span> <span data-ttu-id="1844b-303">En el ejemplo siguiente, se crea una regla denominada `myNetworkSecurityGroupRuleSSH` para permitir TCP en el puerto 22:</span><span class="sxs-lookup"><span data-stu-id="1844b-303">The following example creates a rule named `myNetworkSecurityGroupRuleSSH` to allow TCP on port 22:</span></span>

```azurecli
azure network nsg rule create --resource-group myResourceGroup \
  --nsg-name myNetworkSecurityGroup --protocol tcp --direction inbound \
  --priority 1000 --destination-port-range 22 --access allow \
  --name myNetworkSecurityGroupRuleSSH
```

<span data-ttu-id="1844b-304">Ahora vamos a agregar la regla de entrada del NSG para permitir conexiones de entrada en el puerto 80 (para admitir el tráfico web).</span><span class="sxs-lookup"><span data-stu-id="1844b-304">Now let's add the inbound rule for the NSG to allow inbound connections on port 80 (to support web traffic).</span></span> <span data-ttu-id="1844b-305">En el ejemplo siguiente, se crea una regla denominada `myNetworkSecurityGroupRuleHTTP` para permitir TCP en el puerto 80:</span><span class="sxs-lookup"><span data-stu-id="1844b-305">The following example creates a rule named `myNetworkSecurityGroupRuleHTTP` to allow TCP on port 80:</span></span>

```azurecli
azure network nsg rule create --resource-group myResourceGroup \
  --nsg-name myNetworkSecurityGroup --protocol tcp --direction inbound \
  --priority 1001 --destination-port-range 80 --access allow \
  --name myNetworkSecurityGroupRuleHTTP
```

> [!NOTE]
> <span data-ttu-id="1844b-306">La regla de entrada es un filtro para las conexiones de red entrantes.</span><span class="sxs-lookup"><span data-stu-id="1844b-306">The inbound rule is a filter for inbound network connections.</span></span> <span data-ttu-id="1844b-307">En este ejemplo, enlazamos el NSG a la NIC virtual de las máquinas virtuales, lo que significa que cualquier solicitud que se realice al puerto 22 se pasa a la NIC de nuestra máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="1844b-307">In this example, we bind the NSG to the VMs virtual NIC, which means that any request to port 22 is passed through to the NIC on our VM.</span></span> <span data-ttu-id="1844b-308">Esta regla de entrada es sobre una conexión de red y no sobre un punto de conexión, como en el caso de las implementaciones clásicas.</span><span class="sxs-lookup"><span data-stu-id="1844b-308">This inbound rule is about a network connection, and not about an endpoint, which is what it would be about in classic deployments.</span></span> <span data-ttu-id="1844b-309">Para abrir un puerto, es preciso dejar `--source-port-range` establecido en "\*" (el valor predeterminado) para aceptar las solicitudes entrantes de **cualquier** puerto solicitante.</span><span class="sxs-lookup"><span data-stu-id="1844b-309">To open a port, you must leave the `--source-port-range` set to '\*' (the default value) to accept inbound requests from **any** requesting port.</span></span> <span data-ttu-id="1844b-310">Los puertos suelen ser dinámicos.</span><span class="sxs-lookup"><span data-stu-id="1844b-310">Ports are typically dynamic.</span></span>
>
>

## <a name="bind-to-the-nic"></a><span data-ttu-id="1844b-311">Enlace a la NIC</span><span class="sxs-lookup"><span data-stu-id="1844b-311">Bind to the NIC</span></span>
<span data-ttu-id="1844b-312">Enlace el NSG a las tarjetas de interfaz de red.</span><span class="sxs-lookup"><span data-stu-id="1844b-312">Bind the NSG to the NICs.</span></span> <span data-ttu-id="1844b-313">Necesitamos conectar nuestras tarjetas de interfaz de red con nuestro grupo de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="1844b-313">We need to connect our NICs with our network security group.</span></span> <span data-ttu-id="1844b-314">Ejecute ambos comandos para enlazar nuestras dos tarjetas de interfaz de red:</span><span class="sxs-lookup"><span data-stu-id="1844b-314">Run both commands, to hook up both of our NICs:</span></span>

```azurecli
azure network nic set --resource-group myResourceGroup --name myNic1 \
  --network-security-group-name myNetworkSecurityGroup
```

```azurecli
azure network nic set --resource-group myResourceGroup --name myNic2 \
  --network-security-group-name myNetworkSecurityGroup
```

## <a name="create-an-availability-set"></a><span data-ttu-id="1844b-315">Crear un conjunto de disponibilidad</span><span class="sxs-lookup"><span data-stu-id="1844b-315">Create an availability set</span></span>
<span data-ttu-id="1844b-316">Los conjuntos de disponibilidad ayudan a propagar las máquinas virtuales a los dominios de error y dominios de actualización.</span><span class="sxs-lookup"><span data-stu-id="1844b-316">Availability sets help spread your VMs across fault domains and upgrade domains.</span></span> <span data-ttu-id="1844b-317">Vamos a crear un conjunto de disponibilidad para sus máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="1844b-317">Let's create an availability set for your VMs.</span></span> <span data-ttu-id="1844b-318">En el ejemplo siguiente se crea un conjunto de disponibilidad denominado `myAvailabilitySet`:</span><span class="sxs-lookup"><span data-stu-id="1844b-318">The following example creates an availability set named `myAvailabilitySet`:</span></span>

```azurecli
azure availset create --resource-group myResourceGroup --location westeurope
  --name myAvailabilitySet
```

<span data-ttu-id="1844b-319">Los dominios de error definen un grupo de máquinas virtuales que comparten una fuente de alimentación común y un conmutador de red.</span><span class="sxs-lookup"><span data-stu-id="1844b-319">Fault domains define a grouping of virtual machines that share a common power source and network switch.</span></span> <span data-ttu-id="1844b-320">De manera predeterminada, las máquinas virtuales configuradas dentro de su conjunto de disponibilidad se separan en hasta tres dominios de error.</span><span class="sxs-lookup"><span data-stu-id="1844b-320">By default, the virtual machines that are configured within your availability set are separated across up to three fault domains.</span></span> <span data-ttu-id="1844b-321">La idea es que un problema de hardware en uno de estos dominios de error no afecte a cada máquina virtual que ejecute la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1844b-321">The idea is that a hardware issue in one of these fault domains does not affect every VM that is running your app.</span></span> <span data-ttu-id="1844b-322">Azure distribuye automáticamente las máquinas virtuales en los dominios de error al incluirlos en un conjunto de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="1844b-322">Azure automatically distributes VMs across the fault domains when placing them in an availability set.</span></span>

<span data-ttu-id="1844b-323">Los dominios de actualización indican grupos de máquinas virtuales y hardware físico subyacente que se pueden reiniciar al mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="1844b-323">Upgrade domains indicate groups of virtual machines and underlying physical hardware that can be rebooted at the same time.</span></span> <span data-ttu-id="1844b-324">Es posible que el orden de reinicio de los dominios de actualización no sea secuencial durante el mantenimiento planeado, pero solo se reinicia una actualización cada vez.</span><span class="sxs-lookup"><span data-stu-id="1844b-324">The order in which upgrade domains are rebooted might not be sequential during planned maintenance, but only one upgrade is rebooted at a time.</span></span> <span data-ttu-id="1844b-325">De nuevo, Azure distribuye automáticamente las máquinas virtuales en los dominios de actualización al incluirlos en un sitio de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="1844b-325">Again, Azure automatically distributes your VMs across upgrade domains when placing them in an availability site.</span></span>

<span data-ttu-id="1844b-326">Lea más sobre cómo [administrar la disponibilidad de las máquinas virtuales](manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1844b-326">Read more about [managing the availability of VMs](manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="create-the-linux-vms"></a><span data-ttu-id="1844b-327">Creación de las máquinas virtuales Linux</span><span class="sxs-lookup"><span data-stu-id="1844b-327">Create the Linux VMs</span></span>
<span data-ttu-id="1844b-328">Ha creado los recursos de almacenamiento y de red necesarios para dar soporte a máquinas virtuales con acceso a Internet.</span><span class="sxs-lookup"><span data-stu-id="1844b-328">You've created the storage and network resources to support Internet-accessible VMs.</span></span> <span data-ttu-id="1844b-329">Ahora crearemos dichas máquinas virtuales y las protegeremos con una clave SSH sin contraseña.</span><span class="sxs-lookup"><span data-stu-id="1844b-329">Now let's create those VMs and secure them with an SSH key that doesn't have a password.</span></span> <span data-ttu-id="1844b-330">En este caso, vamos a crear una máquina virtual con Ubuntu basada en la LTM más reciente.</span><span class="sxs-lookup"><span data-stu-id="1844b-330">In this case, we're going to create an Ubuntu VM based on the most recent LTS.</span></span> <span data-ttu-id="1844b-331">Vamos a buscar esa información de la imagen mediante `azure vm image list`, tal como se describe en el artículo sobre cómo [buscar imágenes de máquina virtual de Azure](../windows/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1844b-331">We locate that image information by using `azure vm image list`, as described in [finding Azure VM images](../windows/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="1844b-332">Hemos seleccionado una imagen mediante el comando `azure vm image list westeurope canonical | grep LTS`.</span><span class="sxs-lookup"><span data-stu-id="1844b-332">We selected an image by using the command `azure vm image list westeurope canonical | grep LTS`.</span></span> <span data-ttu-id="1844b-333">En este caso, usamos `canonical:UbuntuServer:16.04.0-LTS:16.04.201608150`.</span><span class="sxs-lookup"><span data-stu-id="1844b-333">In this case, we use `canonical:UbuntuServer:16.04.0-LTS:16.04.201608150`.</span></span> <span data-ttu-id="1844b-334">Para el último campo, pasamos `latest` para que en el futuro siempre obtengamos la compilación más reciente.</span><span class="sxs-lookup"><span data-stu-id="1844b-334">For the last field, we pass `latest` so that in the future we always get the most recent build.</span></span> <span data-ttu-id="1844b-335">(La cadena que usamos es `canonical:UbuntuServer:16.04.0-LTS:16.04.201608150`).</span><span class="sxs-lookup"><span data-stu-id="1844b-335">(The string we use is `canonical:UbuntuServer:16.04.0-LTS:16.04.201608150`).</span></span>

<span data-ttu-id="1844b-336">El siguiente paso resultará familiar para quien ya haya creado un par de claves pública y privada ssh-rsa en Linux o Mac mediante **ssh-keygen -t rsa -b 2048**.</span><span class="sxs-lookup"><span data-stu-id="1844b-336">This next step is familiar to anyone who has already created an ssh rsa public and private key pair on Linux or Mac by using **ssh-keygen -t rsa -b 2048**.</span></span> <span data-ttu-id="1844b-337">Si no tiene ningún par de claves de certificado en el directorio `~/.ssh` , puede crearlas:</span><span class="sxs-lookup"><span data-stu-id="1844b-337">If you do not have any certificate key pairs in your `~/.ssh` directory, you can create them:</span></span>

* <span data-ttu-id="1844b-338">Automáticamente, mediante la opción `azure vm create --generate-ssh-keys` .</span><span class="sxs-lookup"><span data-stu-id="1844b-338">Automatically, by using the `azure vm create --generate-ssh-keys` option.</span></span>
* <span data-ttu-id="1844b-339">Manualmente, mediante [las instrucciones para crearlas usted mismo](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1844b-339">Manually, by using [the instructions to create them yourself](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="1844b-340">Como alternativa, puede usar el método `--admin-password` para autenticar sus conexiones SSH una vez creada la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="1844b-340">Alternatively, you can use the `--admin-password` method to authenticate your SSH connections after the VM is created.</span></span> <span data-ttu-id="1844b-341">Este método suele ser menos seguro.</span><span class="sxs-lookup"><span data-stu-id="1844b-341">This method is typically less secure.</span></span>

<span data-ttu-id="1844b-342">Creamos la máquina virtual, para lo que reunimos toda nuestra información y recursos con el comando `azure vm create` :</span><span class="sxs-lookup"><span data-stu-id="1844b-342">We create the VM by bringing all our resources and information together with the `azure vm create` command:</span></span>

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM1 \
  --location westeurope \
  --os-type linux \
  --availset-name myAvailabilitySet \
  --nic-name myNic1 \
  --vnet-name myVnet \
  --vnet-subnet-name mySubnet \
  --storage-account-name mystorageaccount \
  --image-urn canonical:UbuntuServer:16.04.0-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username azureuser
```

<span data-ttu-id="1844b-343">Salida:</span><span class="sxs-lookup"><span data-stu-id="1844b-343">Output:</span></span>

```azurecli
info:    Executing command vm create
+ Looking up the VM "myVM1"
info:    Verifying the public key SSH file: /home/ahmet/.ssh/id_rsa.pub
info:    Using the VM Size "Standard_DS1"
info:    The [OS, Data] Disk or image configuration requires storage account
+ Looking up the storage account mystorageaccount
+ Looking up the availability set "myAvailabilitySet"
info:    Found an Availability set "myAvailabilitySet"
+ Looking up the NIC "myNic1"
info:    Found an existing NIC "myNic1"
info:    Found an IP configuration with virtual network subnet id "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet" in the NIC "myNic1"
info:    This is an NIC without publicIP configured
info:    The storage URI 'https://mystorageaccount.blob.core.windows.net/' will be used for boot diagnostics settings, and it can be overwritten by the parameter input of '--boot-diagnostics-storage-uri'.
info:    vm create command OK
```

<span data-ttu-id="1844b-344">Puede conectarse de inmediato a la máquina virtual con las claves SSH predeterminadas.</span><span class="sxs-lookup"><span data-stu-id="1844b-344">You can connect to your VM immediately by using your default SSH keys.</span></span> <span data-ttu-id="1844b-345">Asegúrese de especificar el puerto adecuado, ya que las estamos pasando a través del equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="1844b-345">Make sure that you specify the appropriate port since we're passing through the load balancer.</span></span> <span data-ttu-id="1844b-346">Para nuestra primera máquina virtual, configuramos la regla NAT para reenviar el puerto 4222 a nuestra máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="1844b-346">(For our first VM, we set up the NAT rule to forward port 4222 to our VM.)</span></span>

```bash
ssh ops@mypublicdns.westeurope.cloudapp.azure.com -p 4222
```

<span data-ttu-id="1844b-347">Salida:</span><span class="sxs-lookup"><span data-stu-id="1844b-347">Output:</span></span>

```bash
The authenticity of host '[mypublicdns.westeurope.cloudapp.azure.com]:4222 ([xx.xx.xx.xx]:4222)' can't be established.
ECDSA key fingerprint is 94:2d:d0:ce:6b:fb:7f:ad:5b:3c:78:93:75:82:12:f9.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added '[mypublicdns.westeurope.cloudapp.azure.com]:4222,[xx.xx.xx.xx]:4222' (ECDSA) to the list of known hosts.
Welcome to Ubuntu 16.04.1 LTS (GNU/Linux 4.4.0-34-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  Get cloud support with Ubuntu Advantage Cloud Guest:
    http://www.ubuntu.com/business/services/cloud

0 packages can be updated.
0 updates are security updates.

ops@myVM1:~$
```

<span data-ttu-id="1844b-348">Continúe y cree su segunda máquina virtual de la misma manera:</span><span class="sxs-lookup"><span data-stu-id="1844b-348">Go ahead and create your second VM in the same manner:</span></span>

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM2 \
  --location westeurope \
  --os-type linux \
  --availset-name myAvailabilitySet \
  --nic-name myNic2 \
  --vnet-name myVnet \
  --vnet-subnet-name mySubnet \
  --storage-account-name mystorageaccount \
  --image-urn canonical:UbuntuServer:16.04.0-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username azureuser
```

<span data-ttu-id="1844b-349">Ya puede usar el comando `azure vm show myResourceGroup myVM1` para examinar lo que ha creado.</span><span class="sxs-lookup"><span data-stu-id="1844b-349">And you can now use the `azure vm show myResourceGroup myVM1` command to examine what you've created.</span></span> <span data-ttu-id="1844b-350">Llegados a este punto, ejecuta las máquinas virtuales con Ubuntu detrás de un equilibrador de carga en Azure en las que solo puede iniciar sesión con el par de claves SSH (porque las contraseñas están deshabilitadas).</span><span class="sxs-lookup"><span data-stu-id="1844b-350">At this point, you're running your Ubuntu VMs behind a load balancer in Azure that you can sign into only with your SSH key pair (because passwords are disabled).</span></span> <span data-ttu-id="1844b-351">Puede instalar nginx o httpd, implementar una aplicación web y ver cómo fluye el tráfico a las dos máquinas virtuales a través del equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="1844b-351">You can install nginx or httpd, deploy a web app, and see the traffic flow through the load balancer to both of the VMs.</span></span>

```azurecli
azure vm show --resource-group myResourceGroup --name myVM1
```

<span data-ttu-id="1844b-352">Salida:</span><span class="sxs-lookup"><span data-stu-id="1844b-352">Output:</span></span>

```azurecli
info:    Executing command vm show
+ Looking up the VM "TestVM1"
+ Looking up the NIC "myNic1"
data:    Id                              :/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM1
data:    ProvisioningState               :Succeeded
data:    Name                            :myVM1
data:    Location                        :westeurope
data:    Type                            :Microsoft.Compute/virtualMachines
data:
data:    Hardware Profile:
data:      Size                          :Standard_DS1
data:
data:    Storage Profile:
data:      Image reference:
data:        Publisher                   :canonical
data:        Offer                       :UbuntuServer
data:        Sku                         :16.04.0-LTS
data:        Version                     :latest
data:
data:      OS Disk:
data:        OSType                      :Linux
data:        Name                        :clib45a8b650f4428a1-os-1471973896525
data:        Caching                     :ReadWrite
data:        CreateOption                :FromImage
data:        Vhd:
data:          Uri                       :https://mystorageaccount.blob.core.windows.net/vhds/clib45a8b650f4428a1-os-1471973896525.vhd
data:
data:    OS Profile:
data:      Computer Name                 :myVM1
data:      User Name                     :ops
data:      Linux Configuration:
data:        Disable Password Auth       :true
data:
data:    Network Profile:
data:      Network Interfaces:
data:        Network Interface #1:
data:          Primary                   :true
data:          MAC Address               :00-0D-3A-24-D4-AA
data:          Provisioning State        :Succeeded
data:          Name                      :LmyNic1
data:          Location                  :westeurope
data:
data:    AvailabilitySet:
data:      Id                            :/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Compute/availabilitySets/myAvailabilitySet
data:
data:    Diagnostics Profile:
data:      BootDiagnostics Enabled       :true
data:      BootDiagnostics StorageUri    :https://mystorageaccount.blob.core.windows.net/
data:
data:      Diagnostics Instance View:
info:    vm show command OK

```


## <a name="export-the-environment-as-a-template"></a><span data-ttu-id="1844b-353">Exportación del entorno como una plantilla</span><span class="sxs-lookup"><span data-stu-id="1844b-353">Export the environment as a template</span></span>
<span data-ttu-id="1844b-354">Ahora que ha creado este entorno, ¿y si quiere crear un entorno de desarrollo adicional con los mismos parámetros o un entorno de producción correspondiente?</span><span class="sxs-lookup"><span data-stu-id="1844b-354">Now that you have built out this environment, what if you want to create an additional development environment with the same parameters, or a production environment that matches it?</span></span> <span data-ttu-id="1844b-355">Resource Manager usa plantillas JSON que definen todos los parámetros de su entorno.</span><span class="sxs-lookup"><span data-stu-id="1844b-355">Resource Manager uses JSON templates that define all the parameters for your environment.</span></span> <span data-ttu-id="1844b-356">Puede crear entornos enteros haciendo referencia a esta plantilla JSON.</span><span class="sxs-lookup"><span data-stu-id="1844b-356">You build out entire environments by referencing this JSON template.</span></span> <span data-ttu-id="1844b-357">Puede [compilar plantillas JSON manualmente](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) o exportar un entorno existente para que la plantilla JSON se cree automáticamente:</span><span class="sxs-lookup"><span data-stu-id="1844b-357">You can [build JSON templates manually](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or export an existing environment to create the JSON template for you:</span></span>

```azurecli
azure group export --name myResourceGroup
```

<span data-ttu-id="1844b-358">Este comando crea el archivo `myResourceGroup.json` en el directorio de trabajo actual.</span><span class="sxs-lookup"><span data-stu-id="1844b-358">This command creates the `myResourceGroup.json` file in your current working directory.</span></span> <span data-ttu-id="1844b-359">Al crear un entorno a partir de esta plantilla, se le piden todos los nombres de recursos, incluidos los del equilibrador de carga, las interfaces de red o las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="1844b-359">When you create an environment from this template, you are prompted for all the resource names, including the names for the load balancer, network interfaces, or VMs.</span></span> <span data-ttu-id="1844b-360">Para rellenar estos nombres en el archivo de plantilla, agregue el parámetro `-p` o `--includeParameterDefaultValue` al comando `azure group export` mostrado antes.</span><span class="sxs-lookup"><span data-stu-id="1844b-360">You can populate these names in your template file by adding the `-p` or `--includeParameterDefaultValue` parameter to the `azure group export` command that was shown earlier.</span></span> <span data-ttu-id="1844b-361">Edite su plantilla JSON para especificar los nombres de recursos o [cree un archivo parameters.json](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) que especifique los nombres de recursos.</span><span class="sxs-lookup"><span data-stu-id="1844b-361">Edit your JSON template to specify the resource names, or [create a parameters.json file](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) that specifies the resource names.</span></span>

<span data-ttu-id="1844b-362">Para crear un entorno a partir de la plantilla:</span><span class="sxs-lookup"><span data-stu-id="1844b-362">To create an environment from your template:</span></span>

```azurecli
azure group deployment create --resource-group myNewResourceGroup \
  --template-file myResourceGroup.json
```

<span data-ttu-id="1844b-363">Es posible que quiera leer [más sobre cómo realizar implementaciones desde plantillas](../../resource-group-template-deploy-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1844b-363">You might want to read [more about how to deploy from templates](../../resource-group-template-deploy-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="1844b-364">Obtenga información sobre cómo actualizar los entornos de manera incremental, usar el archivo de parámetros y tener acceso a las plantillas desde una única ubicación de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="1844b-364">Learn about how to incrementally update environments, use the parameters file, and access templates from a single storage location.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1844b-365">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1844b-365">Next steps</span></span>
<span data-ttu-id="1844b-366">Ya está listo para empezar a trabajar con varios componentes de red y máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="1844b-366">Now you're ready to begin working with multiple networking components and VMs.</span></span> <span data-ttu-id="1844b-367">Puede usar este entorno de ejemplo para crear la aplicación con los componentes principales aquí presentados.</span><span class="sxs-lookup"><span data-stu-id="1844b-367">You can use this sample environment to build out your application by using the core components introduced here.</span></span>
