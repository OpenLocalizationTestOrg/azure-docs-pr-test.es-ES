---
title: aaaCreate un entorno completo de Linux con hello 1.0 de CLI de Azure | Documentos de Microsoft
description: "Crear almacenamiento, una VM de Linux, una red virtual y subred, un equilibrador de carga, una NIC, una dirección IP pública y un grupo de seguridad de red, todo ello desde Hola descárguese de corriente mediante el uso de hello 1.0 de CLI de Azure."
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
ms.openlocfilehash: 7fe00e138704fe9c9a1c9b87a7dd1afd6174e527
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-complete-linux-environment-with-hello-azure-cli-10"></a><span data-ttu-id="4acab-103">Crear un entorno completo de Linux con hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="4acab-103">Create a complete Linux environment with hello Azure CLI 1.0</span></span>
<span data-ttu-id="4acab-104">En este artículo, vamos a crear una red sencilla con un equilibrador de carga y un par de máquinas virtuales útiles para el desarrollo y la computación simple.</span><span class="sxs-lookup"><span data-stu-id="4acab-104">In this article, we build a simple network with a load balancer and a pair of VMs that are useful for development and simple computing.</span></span> <span data-ttu-id="4acab-105">Le guían en el proceso de Hola por comando, hasta que haya trabajo dos, proteja toowhich de máquinas virtuales de Linux que puede conectarse desde cualquier lugar en hello Internet.</span><span class="sxs-lookup"><span data-stu-id="4acab-105">We walk through hello process command by command, until you have two working, secure Linux VMs toowhich you can connect from anywhere on hello Internet.</span></span> <span data-ttu-id="4acab-106">A continuación, puede mover en entornos y las redes complejas toomore.</span><span class="sxs-lookup"><span data-stu-id="4acab-106">Then you can move on toomore complex networks and environments.</span></span>

<span data-ttu-id="4acab-107">A lo largo de la manera de hello, información sobre jerarquía de dependencias de Hola que ofrece modelo de implementación del Administrador de recursos de Hola y sobre Cuánta energía proporciona.</span><span class="sxs-lookup"><span data-stu-id="4acab-107">Along hello way, you learn about hello dependency hierarchy that hello Resource Manager deployment model gives you, and about how much power it provides.</span></span> <span data-ttu-id="4acab-108">Después de ver cómo se crea el sistema de hello, puede volver a compilarlo mucho más rápidamente mediante el uso de [plantillas de Azure Resource Manager](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4acab-108">After you see how hello system is built, you can rebuild it much more quickly by using [Azure Resource Manager templates](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="4acab-109">Además, después de obtener información sobre cómo encajan partes de Hola de su entorno, crear plantillas tooautomate les hace más fácil.</span><span class="sxs-lookup"><span data-stu-id="4acab-109">Also, after you learn how hello parts of your environment fit together, creating templates tooautomate them becomes easier.</span></span>

<span data-ttu-id="4acab-110">entorno de Hello contiene:</span><span class="sxs-lookup"><span data-stu-id="4acab-110">hello environment contains:</span></span>

* <span data-ttu-id="4acab-111">Dos máquinas virtuales dentro de un conjunto de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="4acab-111">Two VMs inside an availability set.</span></span>
* <span data-ttu-id="4acab-112">Un equilibrador de carga con una regla de equilibrio de carga en el puerto 80.</span><span class="sxs-lookup"><span data-stu-id="4acab-112">A load balancer with a load-balancing rule on port 80.</span></span>
* <span data-ttu-id="4acab-113">Grupo de seguridad de red (NSG) reglas tooprotect la máquina virtual de tráfico no deseado.</span><span class="sxs-lookup"><span data-stu-id="4acab-113">Network security group (NSG) rules tooprotect your VM from unwanted traffic.</span></span>

<span data-ttu-id="4acab-114">toocreate este entorno personalizado, deberá hello más reciente [Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) en modo de administrador de recursos (`azure config mode arm`).</span><span class="sxs-lookup"><span data-stu-id="4acab-114">toocreate this custom environment, you need hello latest [Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) in Resource Manager mode (`azure config mode arm`).</span></span> <span data-ttu-id="4acab-115">También necesitará una herramienta de análisis JSON.</span><span class="sxs-lookup"><span data-stu-id="4acab-115">You also need a JSON parsing tool.</span></span> <span data-ttu-id="4acab-116">En este ejemplo se usa [jq](https://stedolan.github.io/jq/).</span><span class="sxs-lookup"><span data-stu-id="4acab-116">This example uses [jq](https://stedolan.github.io/jq/).</span></span>


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="4acab-117">Tarea CLI versiones toocomplete hello</span><span class="sxs-lookup"><span data-stu-id="4acab-117">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="4acab-118">Puede completar la tarea hello mediante uno de hello después de las versiones CLI:</span><span class="sxs-lookup"><span data-stu-id="4acab-118">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="4acab-119">[Azure 1.0 de CLI](#quick-commands) – nuestro CLI para hello clásico y recursos administración modelos de implementación (en este artículo)</span><span class="sxs-lookup"><span data-stu-id="4acab-119">[Azure CLI 1.0](#quick-commands) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="4acab-120">[Azure 2.0 CLI](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -nuestro CLI de próxima generación para el modelo de implementación de administración de recursos de Hola</span><span class="sxs-lookup"><span data-stu-id="4acab-120">[Azure CLI 2.0](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="4acab-121">Comandos rápidos</span><span class="sxs-lookup"><span data-stu-id="4acab-121">Quick commands</span></span>
<span data-ttu-id="4acab-122">Si necesita tooquickly realizar la tarea hello, Hola después Hola de detalles de la sección base tooupload comandos tooAzure de una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="4acab-122">If you need tooquickly accomplish hello task, hello following section details hello base commands tooupload a VM tooAzure.</span></span> <span data-ttu-id="4acab-123">Obtener más información y el contexto de cada paso puede encontrarse en el resto de saludo del documento de hello, a partir de [aquí](#detailed-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="4acab-123">More detailed information and context for each step can be found in hello rest of hello document, starting [here](#detailed-walkthrough).</span></span>

<span data-ttu-id="4acab-124">Asegúrese de que dispone de [hello Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) iniciado la sesión y utilizar el modo de administrador de recursos:</span><span class="sxs-lookup"><span data-stu-id="4acab-124">Make sure that you have [hello Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) logged in and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="4acab-125">En hello en los ejemplos siguientes, reemplace los nombres de parámetros de ejemplo con sus propios valores.</span><span class="sxs-lookup"><span data-stu-id="4acab-125">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="4acab-126">Los nombres de parámetros de ejemplo incluyen `myResourceGroup`, `mystorageaccount` y `myVM`.</span><span class="sxs-lookup"><span data-stu-id="4acab-126">Example parameter names include `myResourceGroup`, `mystorageaccount`, and `myVM`.</span></span>

<span data-ttu-id="4acab-127">Crear grupo de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="4acab-127">Create hello resource group.</span></span> <span data-ttu-id="4acab-128">Hello en el ejemplo siguiente se crea un grupo de recursos denominado `myResourceGroup` en hello `westeurope` ubicación:</span><span class="sxs-lookup"><span data-stu-id="4acab-128">hello following example creates a resource group named `myResourceGroup` in hello `westeurope` location:</span></span>

```azurecli
azure group create -n myResourceGroup -l westeurope
```

<span data-ttu-id="4acab-129">Comprobar el grupo de recursos de hello mediante analizador JSON de hello:</span><span class="sxs-lookup"><span data-stu-id="4acab-129">Verify hello resource group by using hello JSON parser:</span></span>

```azurecli
azure group show myResourceGroup --json | jq '.'
```

<span data-ttu-id="4acab-130">Crear cuenta de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="4acab-130">Create hello storage account.</span></span> <span data-ttu-id="4acab-131">Hello en el ejemplo siguiente se crea una cuenta de almacenamiento denominada `mystorageaccount`.</span><span class="sxs-lookup"><span data-stu-id="4acab-131">hello following example creates a storage account named `mystorageaccount`.</span></span> <span data-ttu-id="4acab-132">(nombre de cuenta de almacenamiento de hello debe ser único, por lo que proporcionar su propio nombre único.)</span><span class="sxs-lookup"><span data-stu-id="4acab-132">(hello storage account name must be unique, so provide your own unique name.)</span></span>

```azurecli
azure storage account create -g myResourceGroup -l westeurope \
  --kind Storage --sku-name GRS mystorageaccount
```

<span data-ttu-id="4acab-133">Comprobar la cuenta de almacenamiento de hello mediante analizador JSON de hello:</span><span class="sxs-lookup"><span data-stu-id="4acab-133">Verify hello storage account by using hello JSON parser:</span></span>

```azurecli
azure storage account show -g myResourceGroup mystorageaccount --json | jq '.'
```

<span data-ttu-id="4acab-134">Crear red virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="4acab-134">Create hello virtual network.</span></span> <span data-ttu-id="4acab-135">Hello en el ejemplo siguiente se crea una red virtual denominada `myVnet`:</span><span class="sxs-lookup"><span data-stu-id="4acab-135">hello following example creates a virtual network named `myVnet`:</span></span>

```azurecli
azure network vnet create -g myResourceGroup -l westeurope\
  -n myVnet -a 192.168.0.0/16
```

<span data-ttu-id="4acab-136">Cree una subred.</span><span class="sxs-lookup"><span data-stu-id="4acab-136">Create a subnet.</span></span> <span data-ttu-id="4acab-137">Hello en el ejemplo siguiente se crea una subred denominada `mySubnet`:</span><span class="sxs-lookup"><span data-stu-id="4acab-137">hello following example creates a subnet named `mySubnet`:</span></span>

```azurecli
azure network vnet subnet create -g myResourceGroup \
  -e myVnet -n mySubnet -a 192.168.1.0/24
```

<span data-ttu-id="4acab-138">Comprobar Hola de red virtual y subred mediante el analizador JSON de hello:</span><span class="sxs-lookup"><span data-stu-id="4acab-138">Verify hello virtual network and subnet by using hello JSON parser:</span></span>

```azurecli
azure network vnet show myResourceGroup myVnet --json | jq '.'
```

<span data-ttu-id="4acab-139">Cree una IP pública.</span><span class="sxs-lookup"><span data-stu-id="4acab-139">Create a public IP.</span></span> <span data-ttu-id="4acab-140">Hello en el ejemplo siguiente se crea una IP pública denominada `myPublicIP` con el nombre DNS de Hola de `mypublicdns`.</span><span class="sxs-lookup"><span data-stu-id="4acab-140">hello following example creates a public IP named `myPublicIP` with hello DNS name of `mypublicdns`.</span></span> <span data-ttu-id="4acab-141">(nombre DNS de hello debe ser único, por lo que proporcionar su propio nombre único.)</span><span class="sxs-lookup"><span data-stu-id="4acab-141">(hello DNS name must be unique, so provide your own unique name.)</span></span>

```azurecli
azure network public-ip create -g myResourceGroup -l westeurope \
  -n myPublicIP  -d mypublicdns -a static -i 4
```

<span data-ttu-id="4acab-142">Crear el equilibrador de carga de Hola.</span><span class="sxs-lookup"><span data-stu-id="4acab-142">Create hello load balancer.</span></span> <span data-ttu-id="4acab-143">Hello en el ejemplo siguiente se crea un equilibrador de carga con el nombre `myLoadBalancer`:</span><span class="sxs-lookup"><span data-stu-id="4acab-143">hello following example creates a load balancer named `myLoadBalancer`:</span></span>

```azurecli
azure network lb create -g myResourceGroup -l westeurope -n myLoadBalancer
```

<span data-ttu-id="4acab-144">Crear un grupo IP front-end de equilibrador de carga de Hola y asociar IP pública Hola.</span><span class="sxs-lookup"><span data-stu-id="4acab-144">Create a front-end IP pool for hello load balancer, and associate hello public IP.</span></span> <span data-ttu-id="4acab-145">Hello en el ejemplo siguiente se crea un grupo IP front-end denominado `mySubnetPool`:</span><span class="sxs-lookup"><span data-stu-id="4acab-145">hello following example creates a front-end IP pool named `mySubnetPool`:</span></span>

```azurecli
azure network lb frontend-ip create -g myResourceGroup -l myLoadBalancer \
  -i myPublicIP -n myFrontEndPool
```

<span data-ttu-id="4acab-146">Crear grupo IP de back-end de Hola Hola equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="4acab-146">Create hello back-end IP pool for hello load balancer.</span></span> <span data-ttu-id="4acab-147">Hello en el ejemplo siguiente se crea un grupo IP de back-end denominado `myBackEndPool`:</span><span class="sxs-lookup"><span data-stu-id="4acab-147">hello following example creates a back-end IP pool named `myBackEndPool`:</span></span>

```azurecli
azure network lb address-pool create -g myResourceGroup -l myLoadBalancer \
  -n myBackEndPool
```

<span data-ttu-id="4acab-148">Crear reglas NAT (traducción) de dirección Hola equilibrador de carga de red de entrada de SSH.</span><span class="sxs-lookup"><span data-stu-id="4acab-148">Create SSH inbound network address translation (NAT) rules for hello load balancer.</span></span> <span data-ttu-id="4acab-149">Hello en el ejemplo siguiente se crea dos reglas de equilibrador de carga, `myLoadBalancerRuleSSH1` y `myLoadBalancerRuleSSH2`:</span><span class="sxs-lookup"><span data-stu-id="4acab-149">hello following example creates two load balancer rules, `myLoadBalancerRuleSSH1` and `myLoadBalancerRuleSSH2`:</span></span>

```azurecli
azure network lb inbound-nat-rule create -g myResourceGroup -l myLoadBalancer \
  -n myLoadBalancerRuleSSH1 -p tcp -f 4222 -b 22
azure network lb inbound-nat-rule create -g myResourceGroup -l myLoadBalancer \
  -n myLoadBalancerRuleSSH2 -p tcp -f 4223 -b 22
```

<span data-ttu-id="4acab-150">Crear sitio web de hello equilibrador de carga de reglas NAT de entrada para saludo.</span><span class="sxs-lookup"><span data-stu-id="4acab-150">Create hello web inbound NAT rules for hello load balancer.</span></span> <span data-ttu-id="4acab-151">Hello en el ejemplo siguiente se crea una regla de equilibrador de carga denominada `myLoadBalancerRuleWeb`:</span><span class="sxs-lookup"><span data-stu-id="4acab-151">hello following example creates a load balancer rule named `myLoadBalancerRuleWeb`:</span></span>

```azurecli
azure network lb rule create -g myResourceGroup -l myLoadBalancer \
  -n myLoadBalancerRuleWeb -p tcp -f 80 -b 80 \
  -t myFrontEndPool -o myBackEndPool
```

<span data-ttu-id="4acab-152">Crear el sondeo de estado del equilibrador de carga de Hola.</span><span class="sxs-lookup"><span data-stu-id="4acab-152">Create hello load balancer health probe.</span></span> <span data-ttu-id="4acab-153">Hello en el ejemplo siguiente se crea un sondeo TCP denominado `myHealthProbe`:</span><span class="sxs-lookup"><span data-stu-id="4acab-153">hello following example creates a TCP probe named `myHealthProbe`:</span></span>

```azurecli
azure network lb probe create -g myResourceGroup -l myLoadBalancer \
  -n myHealthProbe -p "tcp" -i 15 -c 4
```

<span data-ttu-id="4acab-154">Comprobar equilibrador de carga de hello, grupos de direcciones IP y las reglas de NAT mediante el analizador JSON de hello:</span><span class="sxs-lookup"><span data-stu-id="4acab-154">Verify hello load balancer, IP pools, and NAT rules by using hello JSON parser:</span></span>

```azurecli
azure network lb show -g myResourceGroup -n myLoadBalancer --json | jq '.'
```

<span data-ttu-id="4acab-155">Crear Hola primera interfaz tarjeta de red (NIC).</span><span class="sxs-lookup"><span data-stu-id="4acab-155">Create hello first network interface card (NIC).</span></span> <span data-ttu-id="4acab-156">Reemplace hello `#####-###-###` secciones con su propio identificador de suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="4acab-156">Replace hello `#####-###-###` sections with your own Azure subscription ID.</span></span> <span data-ttu-id="4acab-157">Su suscripción ID se indica en la salida de hello de **jq** al examinar los recursos de Hola que se va a crear.</span><span class="sxs-lookup"><span data-stu-id="4acab-157">Your subscription ID is noted in hello output of **jq** when you examine hello resources you are creating.</span></span> <span data-ttu-id="4acab-158">Su identificador de suscripción también puede verlo con `azure account list`.</span><span class="sxs-lookup"><span data-stu-id="4acab-158">You can also view your subscription ID with `azure account list`.</span></span>

<span data-ttu-id="4acab-159">Hello en el ejemplo siguiente se crea una NIC denominada `myNic1`:</span><span class="sxs-lookup"><span data-stu-id="4acab-159">hello following example creates a NIC named `myNic1`:</span></span>

```azurecli
azure network nic create -g myResourceGroup -l westeurope \
  -n myNic1 -m myVnet -k mySubnet \
  -d "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool" \
  -e "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1"
```

<span data-ttu-id="4acab-160">Crear NIC de hello segundo.</span><span class="sxs-lookup"><span data-stu-id="4acab-160">Create hello second NIC.</span></span> <span data-ttu-id="4acab-161">Hello en el ejemplo siguiente se crea una NIC denominada `myNic2`:</span><span class="sxs-lookup"><span data-stu-id="4acab-161">hello following example creates a NIC named `myNic2`:</span></span>

```azurecli
azure network nic create -g myResourceGroup -l westeurope \
  -n myNic2 -m myVnet -k mySubnet \
  -d "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool" \
  -e "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH2"
```

<span data-ttu-id="4acab-162">Comprobar Hola dos NIC mediante el analizador JSON de hello:</span><span class="sxs-lookup"><span data-stu-id="4acab-162">Verify hello two NICs by using hello JSON parser:</span></span>

```azurecli
azure network nic show myResourceGroup myNic1 --json | jq '.'
azure network nic show myResourceGroup myNic2 --json | jq '.'
```

<span data-ttu-id="4acab-163">Crear grupo de seguridad de red de Hola.</span><span class="sxs-lookup"><span data-stu-id="4acab-163">Create hello network security group.</span></span> <span data-ttu-id="4acab-164">Hello en el ejemplo siguiente se crea un grupo de seguridad de red denominado `myNetworkSecurityGroup`:</span><span class="sxs-lookup"><span data-stu-id="4acab-164">hello following example creates a network security group named `myNetworkSecurityGroup`:</span></span>

```azurecli
azure network nsg create -g myResourceGroup -l westeurope \
  -n myNetworkSecurityGroup
```

<span data-ttu-id="4acab-165">Agregue dos reglas de entrada para el grupo de seguridad de red de Hola.</span><span class="sxs-lookup"><span data-stu-id="4acab-165">Add two inbound rules for hello network security group.</span></span> <span data-ttu-id="4acab-166">Hello en el ejemplo siguiente se crea dos reglas, `myNetworkSecurityGroupRuleSSH` y `myNetworkSecurityGroupRuleHTTP`:</span><span class="sxs-lookup"><span data-stu-id="4acab-166">hello following example creates two rules, `myNetworkSecurityGroupRuleSSH` and `myNetworkSecurityGroupRuleHTTP`:</span></span>

```azurecli
azure network nsg rule create -p tcp -r inbound -y 1000 -u 22 -c allow \
  -g myResourceGroup -a myNetworkSecurityGroup -n myNetworkSecurityGroupRuleSSH
azure network nsg rule create -p tcp -r inbound -y 1001 -u 80 -c allow \
  -g myResourceGroup -a myNetworkSecurityGroup -n myNetworkSecurityGroupRuleHTTP
```

<span data-ttu-id="4acab-167">Comprobar grupo de seguridad de red de Hola y reglas de entrada mediante el analizador JSON de hello:</span><span class="sxs-lookup"><span data-stu-id="4acab-167">Verify hello network security group and inbound rules by using hello JSON parser:</span></span>

```azurecli
azure network nsg show -g myResourceGroup -n myNetworkSecurityGroup --json | jq '.'
```

<span data-ttu-id="4acab-168">Enlace de seguridad de la red de hello grupo toohello dos NIC:</span><span class="sxs-lookup"><span data-stu-id="4acab-168">Bind hello network security group toohello two NICs:</span></span>

```azurecli
azure network nic set -g myResourceGroup -o myNetworkSecurityGroup -n myNic1
azure network nic set -g myResourceGroup -o myNetworkSecurityGroup -n myNic2
```

<span data-ttu-id="4acab-169">Crear conjunto de disponibilidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="4acab-169">Create hello availability set.</span></span> <span data-ttu-id="4acab-170">Hello en el ejemplo siguiente se crea un conjunto con nombre de disponibilidad `myAvailabilitySet`:</span><span class="sxs-lookup"><span data-stu-id="4acab-170">hello following example creates an availability set named `myAvailabilitySet`:</span></span>

```azurecli
azure availset create -g myResourceGroup -l westeurope -n myAvailabilitySet
```

<span data-ttu-id="4acab-171">Crear Hola primera VM de Linux.</span><span class="sxs-lookup"><span data-stu-id="4acab-171">Create hello first Linux VM.</span></span> <span data-ttu-id="4acab-172">Hello en el ejemplo siguiente se crea una máquina virtual denominada `myVM1`:</span><span class="sxs-lookup"><span data-stu-id="4acab-172">hello following example creates a VM named `myVM1`:</span></span>

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

<span data-ttu-id="4acab-173">Crear hello segunda VM de Linux.</span><span class="sxs-lookup"><span data-stu-id="4acab-173">Create hello second Linux VM.</span></span> <span data-ttu-id="4acab-174">Hello en el ejemplo siguiente se crea una máquina virtual denominada `myVM2`:</span><span class="sxs-lookup"><span data-stu-id="4acab-174">hello following example creates a VM named `myVM2`:</span></span>

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

<span data-ttu-id="4acab-175">Use Hola JSON analizador tooverify que todo lo que se creó:</span><span class="sxs-lookup"><span data-stu-id="4acab-175">Use hello JSON parser tooverify that everything that was built:</span></span>

```azurecli
azure vm show -g myResourceGroup -n myVM1 --json | jq '.'
azure vm show -g myResourceGroup -n myVM2 --json | jq '.'
```

<span data-ttu-id="4acab-176">Exportar sus nuevo entorno tooa tooquickly volver a crear nuevas instancias de plantilla:</span><span class="sxs-lookup"><span data-stu-id="4acab-176">Export your new environment tooa template tooquickly re-create new instances:</span></span>

```azurecli
azure group export myResourceGroup
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="4acab-177">Tutorial detallado</span><span class="sxs-lookup"><span data-stu-id="4acab-177">Detailed walkthrough</span></span>
<span data-ttu-id="4acab-178">Hello pasos detallados que van a continuación explican lo que hace cada comando mientras se generan fuera de su entorno.</span><span class="sxs-lookup"><span data-stu-id="4acab-178">hello detailed steps that follow explain what each command is doing as you build out your environment.</span></span> <span data-ttu-id="4acab-179">Estos conceptos sirven de ayuda mientras crea sus propios entornos personalizados con fines de desarrollo o producción.</span><span class="sxs-lookup"><span data-stu-id="4acab-179">These concepts are helpful when you build your own custom environments for development or production.</span></span>

<span data-ttu-id="4acab-180">Asegúrese de que dispone de [hello Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) iniciado la sesión y utilizar el modo de administrador de recursos:</span><span class="sxs-lookup"><span data-stu-id="4acab-180">Make sure that you have [hello Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) logged in and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="4acab-181">En hello en los ejemplos siguientes, reemplace los nombres de parámetros de ejemplo con sus propios valores.</span><span class="sxs-lookup"><span data-stu-id="4acab-181">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="4acab-182">Los nombres de parámetros de ejemplo incluyen `myResourceGroup`, `mystorageaccount` y `myVM`.</span><span class="sxs-lookup"><span data-stu-id="4acab-182">Example parameter names include `myResourceGroup`, `mystorageaccount`, and `myVM`.</span></span>

## <a name="create-resource-groups-and-choose-deployment-locations"></a><span data-ttu-id="4acab-183">Creación de grupos de recursos y elección de las ubicaciones para la implementación</span><span class="sxs-lookup"><span data-stu-id="4acab-183">Create resource groups and choose deployment locations</span></span>
<span data-ttu-id="4acab-184">Grupos de recursos de Azure son entidades de lógica de implementación que contienen información y metadatos tooenable Hola lógica administración de la configuración de las implementaciones de recursos.</span><span class="sxs-lookup"><span data-stu-id="4acab-184">Azure resource groups are logical deployment entities that contain configuration information and metadata tooenable hello logical management of resource deployments.</span></span> <span data-ttu-id="4acab-185">Hello en el ejemplo siguiente se crea un grupo de recursos denominado `myResourceGroup` en hello `westeurope` ubicación:</span><span class="sxs-lookup"><span data-stu-id="4acab-185">hello following example creates a resource group named `myResourceGroup` in hello `westeurope` location:</span></span>

```azurecli
azure group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="4acab-186">Salida:</span><span class="sxs-lookup"><span data-stu-id="4acab-186">Output:</span></span>

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

## <a name="create-a-storage-account"></a><span data-ttu-id="4acab-187">Crear una cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="4acab-187">Create a storage account</span></span>
<span data-ttu-id="4acab-188">Necesita cuentas de almacenamiento para los discos de máquina virtual y para los discos de datos adicionales que desea que tooadd.</span><span class="sxs-lookup"><span data-stu-id="4acab-188">You need storage accounts for your VM disks and for any additional data disks that you want tooadd.</span></span> <span data-ttu-id="4acab-189">Las cuentas de almacenamiento se crean casi inmediatamente después de crear los grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="4acab-189">You create storage accounts almost immediately after you create resource groups.</span></span>

<span data-ttu-id="4acab-190">Aquí usamos hello `azure storage account create` comando, pasar la ubicación de Hola de cuenta de hello, grupo de recursos de Hola que controla la base de datos y tipo de Hola de compatibilidad de almacenamiento que desee.</span><span class="sxs-lookup"><span data-stu-id="4acab-190">Here we use hello `azure storage account create` command, passing hello location of hello account, hello resource group that controls it, and hello type of storage support you want.</span></span> <span data-ttu-id="4acab-191">Hello en el ejemplo siguiente se crea una cuenta de almacenamiento denominada `mystorageaccount`:</span><span class="sxs-lookup"><span data-stu-id="4acab-191">hello following example creates a storage account named `mystorageaccount`:</span></span>

```azurecli
azure storage account create \  
  --location westeurope \
  --resource-group myResourceGroup \
  --kind Storage --sku-name GRS \
  mystorageaccount
```

<span data-ttu-id="4acab-192">Salida:</span><span class="sxs-lookup"><span data-stu-id="4acab-192">Output:</span></span>

```azurecli
info:    Executing command storage account create
+ Creating storage account
info:    storage account create command OK
```

<span data-ttu-id="4acab-193">tooexamine nuestro recurso de grupo mediante el uso de hello `azure group show` command, vamos a usar hello [jq](https://stedolan.github.io/jq/) herramienta junto con hello `--json` opción de CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="4acab-193">tooexamine our resource group by using hello `azure group show` command, let's use hello [jq](https://stedolan.github.io/jq/) tool along with hello `--json` Azure CLI option.</span></span> <span data-ttu-id="4acab-194">(Puede usar **jsawk** o cualquier biblioteca de idioma que prefiera tooparse Hola JSON.)</span><span class="sxs-lookup"><span data-stu-id="4acab-194">(You can use **jsawk** or any language library you prefer tooparse hello JSON.)</span></span>

```azurecli
azure group show myResourceGroup --json | jq '.'
```

<span data-ttu-id="4acab-195">Salida:</span><span class="sxs-lookup"><span data-stu-id="4acab-195">Output:</span></span>

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

<span data-ttu-id="4acab-196">cuenta de almacenamiento tooinvestigate Hola utilizando Hola CLI, primero debe claves y nombres de cuenta de hello tooset.</span><span class="sxs-lookup"><span data-stu-id="4acab-196">tooinvestigate hello storage account by using hello CLI, you first need tooset hello account names and keys.</span></span> <span data-ttu-id="4acab-197">Reemplazar Hola nombre de cuenta de almacenamiento de Hola Hola siguiente ejemplo con un nombre que elija:</span><span class="sxs-lookup"><span data-stu-id="4acab-197">Replace hello name of hello storage account in hello following example with a name that you choose:</span></span>

```bash
export AZURE_STORAGE_CONNECTION_STRING="$(azure storage account connectionstring show mystorageaccount --resource-group myResourceGroup --json | jq -r '.string')"
```

<span data-ttu-id="4acab-198">Luego podrá ver la información de almacenamiento fácilmente:</span><span class="sxs-lookup"><span data-stu-id="4acab-198">Then you can view your storage information easily:</span></span>

```azurecli
azure storage container list
```

<span data-ttu-id="4acab-199">Salida:</span><span class="sxs-lookup"><span data-stu-id="4acab-199">Output:</span></span>

```azurecli
info:    Executing command storage container list
+ Getting storage containers
data:    Name  Public-Access  Last-Modified
data:    ----  -------------  -----------------------------
data:    vhds  Off            Sun, 27 Sep 2015 19:03:54 GMT
info:    storage container list command OK
```

## <a name="create-a-virtual-network-and-subnet"></a><span data-ttu-id="4acab-200">Creación de una red virtual y una subred</span><span class="sxs-lookup"><span data-stu-id="4acab-200">Create a virtual network and subnet</span></span>
<span data-ttu-id="4acab-201">A continuación va tooneed toocreate una red virtual que se ejecuta en Azure y una subred en la que puede crear las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="4acab-201">Next you're going tooneed toocreate a virtual network running in Azure and a subnet in which you can create your VMs.</span></span> <span data-ttu-id="4acab-202">Hello en el ejemplo siguiente se crea una red virtual denominada `myVnet` con hello `192.168.0.0/16` prefijo de dirección:</span><span class="sxs-lookup"><span data-stu-id="4acab-202">hello following example creates a virtual network named `myVnet` with hello `192.168.0.0/16` address prefix:</span></span>

```azurecli
azure network vnet create --resource-group myResourceGroup --location westeurope \
  --name myVnet --address-prefixes 192.168.0.0/16
```

<span data-ttu-id="4acab-203">Salida:</span><span class="sxs-lookup"><span data-stu-id="4acab-203">Output:</span></span>

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

<span data-ttu-id="4acab-204">De nuevo, vamos a usar la opción de json: Hola de `azure group show` y `jq` toosee cómo estamos creando nuestros recursos.</span><span class="sxs-lookup"><span data-stu-id="4acab-204">Again, let's use hello --json option of `azure group show` and `jq` toosee how we're building our resources.</span></span> <span data-ttu-id="4acab-205">Ya tenemos un recurso de `storageAccounts` y un recurso de `virtualNetworks`.</span><span class="sxs-lookup"><span data-stu-id="4acab-205">We now have a `storageAccounts` resource and a `virtualNetworks` resource.</span></span>  

```azurecli
azure group show myResourceGroup --json | jq '.'
```

<span data-ttu-id="4acab-206">Salida:</span><span class="sxs-lookup"><span data-stu-id="4acab-206">Output:</span></span>

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

<span data-ttu-id="4acab-207">Ahora vamos a crear una subred en hello `myVnet` red virtual en qué Hola se implementan máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="4acab-207">Now let's create a subnet in hello `myVnet` virtual network into which hello VMs are deployed.</span></span> <span data-ttu-id="4acab-208">Usamos hello `azure network vnet subnet create` comando, junto con los recursos de hello ya hemos creado: Hola `myResourceGroup` hello y grupo de recursos `myVnet` red virtual.</span><span class="sxs-lookup"><span data-stu-id="4acab-208">We use hello `azure network vnet subnet create` command, along with hello resources we've already created: hello `myResourceGroup` resource group and hello `myVnet` virtual network.</span></span> <span data-ttu-id="4acab-209">En el siguiente ejemplo de Hola, agregamos con el nombre de subred de hello `mySubnet` con prefijo de dirección de subred Hola `192.168.1.0/24`:</span><span class="sxs-lookup"><span data-stu-id="4acab-209">In hello following example, we add hello subnet named `mySubnet` with hello subnet address prefix of `192.168.1.0/24`:</span></span>

```azurecli
azure network vnet subnet create --resource-group myResourceGroup \
  --vnet-name myVnet --name mySubnet --address-prefix 192.168.1.0/24
```

<span data-ttu-id="4acab-210">Salida:</span><span class="sxs-lookup"><span data-stu-id="4acab-210">Output:</span></span>

```azurecli
info:    Executing command network vnet subnet create
+ Looking up hello subnet "mySubnet"
+ Creating subnet "mySubnet"
+ Looking up hello subnet "mySubnet"
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet
data:    Type                            : Microsoft.Network/virtualNetworks/subnets
data:    ProvisioningState               : Succeeded
data:    Name                            : mySubnet
data:    Address prefix                  : 192.168.1.0/24
data:
info:    network vnet subnet create command OK
```

<span data-ttu-id="4acab-211">Porque la subred de hello es, lógicamente, dentro de la red virtual de hello, adentrarnos para obtener información de subred de hello con un comando ligeramente diferente.</span><span class="sxs-lookup"><span data-stu-id="4acab-211">Because hello subnet is logically inside hello virtual network, we look for hello subnet information with a slightly different command.</span></span> <span data-ttu-id="4acab-212">se utiliza el comando Hello es `azure network vnet show`, pero continuamos salida JSON de hello tooexamine utilizando `jq`.</span><span class="sxs-lookup"><span data-stu-id="4acab-212">hello command we use is `azure network vnet show`, but we continue tooexamine hello JSON output by using `jq`.</span></span>

```azurecli
azure network vnet show myResourceGroup myVnet --json | jq '.'
```

<span data-ttu-id="4acab-213">Salida:</span><span class="sxs-lookup"><span data-stu-id="4acab-213">Output:</span></span>

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

## <a name="create-a-public-ip-address"></a><span data-ttu-id="4acab-214">Crear una dirección IP pública</span><span class="sxs-lookup"><span data-stu-id="4acab-214">Create a public IP address</span></span>
<span data-ttu-id="4acab-215">Ahora vamos a crear la dirección IP pública hello (PIP) que asignamos tooyour equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="4acab-215">Now let's create hello public IP address (PIP) that we assign tooyour load balancer.</span></span> <span data-ttu-id="4acab-216">Le permite tooconnect tooyour máquinas virtuales de hello Internet mediante el uso de hello `azure network public-ip create` comando.</span><span class="sxs-lookup"><span data-stu-id="4acab-216">It enables you tooconnect tooyour VMs from hello Internet by using hello `azure network public-ip create` command.</span></span> <span data-ttu-id="4acab-217">Debido a la dirección predeterminada hello es dinámica, creamos una entrada DNS con nombre en hello **cloudapp.azure.com** dominio mediante el uso de hello `--domain-name-label` opción.</span><span class="sxs-lookup"><span data-stu-id="4acab-217">Because hello default address is dynamic, we create a named DNS entry in hello **cloudapp.azure.com** domain by using hello `--domain-name-label` option.</span></span> <span data-ttu-id="4acab-218">Hello en el ejemplo siguiente se crea una IP pública denominada `myPublicIP` con el nombre DNS de Hola de `mypublicdns`.</span><span class="sxs-lookup"><span data-stu-id="4acab-218">hello following example creates a public IP named `myPublicIP` with hello DNS name of `mypublicdns`.</span></span> <span data-ttu-id="4acab-219">Como nombre DNS de hello debe ser único, proporcionar su propio nombre DNS único:</span><span class="sxs-lookup"><span data-stu-id="4acab-219">Because hello DNS name must be unique, you provide your own unique DNS name:</span></span>

```azurecli
azure network public-ip create --resource-group myResourceGroup \
  --location westeurope --name myPublicIP --domain-name-label mypublicdns
```

<span data-ttu-id="4acab-220">Salida:</span><span class="sxs-lookup"><span data-stu-id="4acab-220">Output:</span></span>

```azurecli
info:    Executing command network public-ip create
+ Looking up hello public ip "myPublicIP"
+ Creating public ip address "myPublicIP"
+ Looking up hello public ip "myPublicIP"
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

<span data-ttu-id="4acab-221">Hello dirección IP pública también es un recurso de nivel superior, por lo que puede verla con `azure group show`.</span><span class="sxs-lookup"><span data-stu-id="4acab-221">hello public IP address is also a top-level resource, so you can see it with `azure group show`.</span></span>

```azurecli
azure group show myResourceGroup --json | jq '.'
```

<span data-ttu-id="4acab-222">Salida:</span><span class="sxs-lookup"><span data-stu-id="4acab-222">Output:</span></span>

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

<span data-ttu-id="4acab-223">Puede investigar más detalles de recursos, incluidos el nombre de dominio completo (FQDN) de hello del subdominio de hello, mediante el uso de hello completa `azure network public-ip show` comando.</span><span class="sxs-lookup"><span data-stu-id="4acab-223">You can investigate more resource details, including hello fully qualified domain name (FQDN) of hello subdomain, by using hello complete `azure network public-ip show` command.</span></span> <span data-ttu-id="4acab-224">se ha asignado el recurso de dirección IP público Hola lógicamente, pero todavía no se ha asignado una dirección específica.</span><span class="sxs-lookup"><span data-stu-id="4acab-224">hello public IP address resource has been allocated logically, but a specific address has not yet been assigned.</span></span> <span data-ttu-id="4acab-225">tooobtain una dirección IP, que vaya tooneed un equilibrador de carga, que todavía no hemos creado.</span><span class="sxs-lookup"><span data-stu-id="4acab-225">tooobtain an IP address, you're going tooneed a load balancer, which we have not yet created.</span></span>

```azurecli
azure network public-ip show myResourceGroup myPublicIP --json | jq '.'
```

<span data-ttu-id="4acab-226">Salida:</span><span class="sxs-lookup"><span data-stu-id="4acab-226">Output:</span></span>

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

## <a name="create-a-load-balancer-and-ip-pools"></a><span data-ttu-id="4acab-227">Creación de un equilibrador de carga y grupos de direcciones IP</span><span class="sxs-lookup"><span data-stu-id="4acab-227">Create a load balancer and IP pools</span></span>
<span data-ttu-id="4acab-228">Cuando se crea un equilibrador de carga, permite el tráfico toodistribute en varias máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="4acab-228">When you create a load balancer, it enables you toodistribute traffic across multiple VMs.</span></span> <span data-ttu-id="4acab-229">También proporciona aplicaciones de tooyour de redundancia mediante la ejecución de varias máquinas virtuales que responden a las solicitudes de toouser en caso de hello de mantenimiento o cargas pesadas.</span><span class="sxs-lookup"><span data-stu-id="4acab-229">It also provides redundancy tooyour application by running multiple VMs that respond toouser requests in hello event of maintenance or heavy loads.</span></span> <span data-ttu-id="4acab-230">Hello en el ejemplo siguiente se crea un equilibrador de carga con el nombre `myLoadBalancer`:</span><span class="sxs-lookup"><span data-stu-id="4acab-230">hello following example creates a load balancer named `myLoadBalancer`:</span></span>

```azurecli
azure network lb create --resource-group myResourceGroup --location westeurope \
  --name myLoadBalancer
```

<span data-ttu-id="4acab-231">Salida:</span><span class="sxs-lookup"><span data-stu-id="4acab-231">Output:</span></span>

```azurecli
info:    Executing command network lb create
+ Looking up hello load balancer "myLoadBalancer"
+ Creating load balancer "myLoadBalancer"
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer
data:    Name                            : myLoadBalancer
data:    Type                            : Microsoft.Network/loadBalancers
data:    Location                        : westeurope
data:    Provisioning state              : Succeeded
info:    network lb create command OK
```

<span data-ttu-id="4acab-232">Nuestro equilibrador de carga está bastante vacío, así que vamos a crear algunos grupos de direcciones IP.</span><span class="sxs-lookup"><span data-stu-id="4acab-232">Our load balancer is fairly empty, so let's create some IP pools.</span></span> <span data-ttu-id="4acab-233">Queremos toocreate dos grupos de direcciones IP para el equilibrador de carga, uno para el front-end de hello y otro para back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="4acab-233">We want toocreate two IP pools for our load balancer, one for hello front end and one for hello back end.</span></span> <span data-ttu-id="4acab-234">grupo de direcciones IP de front-end de Hello es sean visible públicamente.</span><span class="sxs-lookup"><span data-stu-id="4acab-234">hello front-end IP pool is publicly visible.</span></span> <span data-ttu-id="4acab-235">También es Hola ubicación toowhich que asignamos Hola PIP que hemos creado con anterioridad.</span><span class="sxs-lookup"><span data-stu-id="4acab-235">It's also hello location toowhich we assign hello PIP that we created earlier.</span></span> <span data-ttu-id="4acab-236">A continuación, utilizamos grupo back-end de hello como una ubicación para nuestro tooconnect de máquinas virtuales a.</span><span class="sxs-lookup"><span data-stu-id="4acab-236">Then we use hello back-end pool as a location for our VMs tooconnect to.</span></span> <span data-ttu-id="4acab-237">De este modo, el tráfico de hello puedan fluir a través de toohello de equilibrador de carga de hello las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="4acab-237">That way, hello traffic can flow through hello load balancer toohello VMs.</span></span>

<span data-ttu-id="4acab-238">En primer lugar, vamos a crear nuestro grupo IP de front-end.</span><span class="sxs-lookup"><span data-stu-id="4acab-238">First, let's create our front-end IP pool.</span></span> <span data-ttu-id="4acab-239">Hello en el ejemplo siguiente se crea un grupo de servidor front-end denominado `myFrontEndPool`:</span><span class="sxs-lookup"><span data-stu-id="4acab-239">hello following example creates a front-end pool named `myFrontEndPool`:</span></span>

```azurecli
azure network lb frontend-ip create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --public-ip-name myPublicIP \
  --name myFrontEndPool
```

<span data-ttu-id="4acab-240">Salida:</span><span class="sxs-lookup"><span data-stu-id="4acab-240">Output:</span></span>

```azurecli
info:    Executing command network lb frontend-ip create
+ Looking up hello load balancer "myLoadBalancer"
+ Looking up hello public ip "myPublicIP"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myFrontEndPool
data:    Provisioning state              : Succeeded
data:    Private IP allocation method    : Dynamic
data:    Public IP address id            : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP
info:    network lb mySubnet-ip create command OK
```

<span data-ttu-id="4acab-241">Tenga en cuenta cómo se usa hello `--public-ip-name` cambiar toopass Hola `myPublicIP` que hemos creado con anterioridad.</span><span class="sxs-lookup"><span data-stu-id="4acab-241">Note how we used hello `--public-ip-name` switch toopass in hello `myPublicIP` that we created earlier.</span></span> <span data-ttu-id="4acab-242">Asignar dirección IP pública de hello equilibrador de carga de dirección toohello permite tooreach las máquinas virtuales a través de Internet de Hola.</span><span class="sxs-lookup"><span data-stu-id="4acab-242">Assigning hello public IP address toohello load balancer allows you tooreach your VMs across hello Internet.</span></span>

<span data-ttu-id="4acab-243">Después, vamos a crear nuestro el grupo IP, esta vez para el tráfico de back-end.</span><span class="sxs-lookup"><span data-stu-id="4acab-243">Next, let's create our second IP pool, this time for our back-end traffic.</span></span> <span data-ttu-id="4acab-244">Hello en el ejemplo siguiente se crea un grupo de back-end denominado `myBackEndPool`:</span><span class="sxs-lookup"><span data-stu-id="4acab-244">hello following example creates a back-end pool named `myBackEndPool`:</span></span>

```azurecli
azure network lb address-pool create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myBackEndPool
```

<span data-ttu-id="4acab-245">Salida:</span><span class="sxs-lookup"><span data-stu-id="4acab-245">Output:</span></span>

```azurecli
info:    Executing command network lb address-pool create
+ Looking up hello load balancer "myLoadBalancer"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myBackEndPool
data:    Provisioning state              : Succeeded
info:    network lb address-pool create command OK
```

<span data-ttu-id="4acab-246">Podemos ver cómo el equilibrador de carga está realizando consultando con `azure network lb show` y examinar los resultados JSON de hello:</span><span class="sxs-lookup"><span data-stu-id="4acab-246">We can see how our load balancer is doing by looking with `azure network lb show` and examining hello JSON output:</span></span>

```azurecli
azure network lb show myResourceGroup myLoadBalancer --json | jq '.'
```

<span data-ttu-id="4acab-247">Salida:</span><span class="sxs-lookup"><span data-stu-id="4acab-247">Output:</span></span>

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

## <a name="create-load-balancer-nat-rules"></a><span data-ttu-id="4acab-248">Creación de reglas NAT del equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="4acab-248">Create load balancer NAT rules</span></span>
<span data-ttu-id="4acab-249">tooget el tráfico que fluye a través de nuestro equilibrador de carga, necesitamos toocreate reglas NAT (traducción) de direcciones de red que especifican acciones de entrada o de salida.</span><span class="sxs-lookup"><span data-stu-id="4acab-249">tooget traffic flowing through our load balancer, we need toocreate network address translation (NAT) rules that specify either inbound or outbound actions.</span></span> <span data-ttu-id="4acab-250">Puede especificar Hola protocolo toouse, a continuación, asignar puertos externos toointernal puertos según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="4acab-250">You can specify hello protocol toouse, then map external ports toointernal ports as desired.</span></span> <span data-ttu-id="4acab-251">Para nuestro entorno, vamos a crear algunas reglas que permiten SSH a través de nuestro tooour de equilibrador de carga de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="4acab-251">For our environment, let's create some rules that allow SSH through our load balancer tooour VMs.</span></span> <span data-ttu-id="4acab-252">Configuramos toodirect tooTCP puerto 22 de TCP puertos 4222 y 4223 en nuestra máquinas virtuales (que crearemos más adelante).</span><span class="sxs-lookup"><span data-stu-id="4acab-252">We set up TCP ports 4222 and 4223 toodirect tooTCP port 22 on our VMs (which we create later).</span></span> <span data-ttu-id="4acab-253">Hello en el ejemplo siguiente se crea una regla denominada `myLoadBalancerRuleSSH1` toomap TCP puerto 4222 tooport 22:</span><span class="sxs-lookup"><span data-stu-id="4acab-253">hello following example creates a rule named `myLoadBalancerRuleSSH1` toomap TCP port 4222 tooport 22:</span></span>

```azurecli
azure network lb inbound-nat-rule create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myLoadBalancerRuleSSH1 \
  --protocol tcp --frontend-port 4222 --backend-port 22
```

<span data-ttu-id="4acab-254">Salida:</span><span class="sxs-lookup"><span data-stu-id="4acab-254">Output:</span></span>

```azurecli
info:    Executing command network lb inbound-nat-rule create
+ Looking up hello load balancer "myLoadBalancer"
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

<span data-ttu-id="4acab-255">Repita el procedimiento de hello para la segunda regla NAT de SSH.</span><span class="sxs-lookup"><span data-stu-id="4acab-255">Repeat hello procedure for your second NAT rule for SSH.</span></span> <span data-ttu-id="4acab-256">Hello en el ejemplo siguiente se crea una regla denominada `myLoadBalancerRuleSSH2` toomap TCP puerto 4223 tooport 22:</span><span class="sxs-lookup"><span data-stu-id="4acab-256">hello following example creates a rule named `myLoadBalancerRuleSSH2` toomap TCP port 4223 tooport 22:</span></span>

```azurecli
azure network lb inbound-nat-rule create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myLoadBalancerRuleSSH2 --protocol tcp \
  --frontend-port 4223 --backend-port 22
```

<span data-ttu-id="4acab-257">También vamos a seguir adelante y crear una regla NAT para el puerto TCP 80 para el tráfico de web, enlazar regla hello tooour grupos de direcciones IP.</span><span class="sxs-lookup"><span data-stu-id="4acab-257">Let's also go ahead and create a NAT rule for TCP port 80 for web traffic, hooking hello rule up tooour IP pools.</span></span> <span data-ttu-id="4acab-258">Si se enlazó Hola regla tooan de direcciones IP, en lugar de enlazar Hola regla tooour máquinas virtuales individualmente, podemos agregar o quitar las máquinas virtuales del grupo de direcciones IP de Hola.</span><span class="sxs-lookup"><span data-stu-id="4acab-258">If we hook up hello rule tooan IP pool, instead of hooking up hello rule tooour VMs individually, we can add or remove VMs from hello IP pool.</span></span> <span data-ttu-id="4acab-259">equilibrador de carga de Hello ajusta automáticamente flujo Hola de tráfico.</span><span class="sxs-lookup"><span data-stu-id="4acab-259">hello load balancer automatically adjusts hello flow of traffic.</span></span> <span data-ttu-id="4acab-260">Hello en el ejemplo siguiente se crea una regla denominada `myLoadBalancerRuleWeb` toomap TCP puerto 80 tooport 80:</span><span class="sxs-lookup"><span data-stu-id="4acab-260">hello following example creates a rule named `myLoadBalancerRuleWeb` toomap TCP port 80 tooport 80:</span></span>

```azurecli
azure network lb rule create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myLoadBalancerRuleWeb --protocol tcp \
  --frontend-port 80 --backend-port 80 --frontend-ip-name myFrontEndPool \
  --backend-address-pool-name myBackEndPool
```

<span data-ttu-id="4acab-261">Salida:</span><span class="sxs-lookup"><span data-stu-id="4acab-261">Output:</span></span>

```azurecli
info:    Executing command network lb rule create
+ Looking up hello load balancer "myLoadBalancer"
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

## <a name="create-a-load-balancer-health-probe"></a><span data-ttu-id="4acab-262">Creación del sondeo de estado de un equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="4acab-262">Create a load balancer health probe</span></span>
<span data-ttu-id="4acab-263">Un estado de sondeo periódicamente comprobaciones en hello las máquinas virtuales que están detrás de nuestro toomake de equilibrador de carga que encuentra operativo y responde toorequests tal como se define.</span><span class="sxs-lookup"><span data-stu-id="4acab-263">A health probe periodically checks on hello VMs that are behind our load balancer toomake sure they're operating and responding toorequests as defined.</span></span> <span data-ttu-id="4acab-264">Si no es así, que se quitan del tooensure de operación que los usuarios no están dirigidas toothem.</span><span class="sxs-lookup"><span data-stu-id="4acab-264">If not, they're removed from operation tooensure that users aren't being directed toothem.</span></span> <span data-ttu-id="4acab-265">Puede definir las comprobaciones personalizadas para el sondeo de estado de hello, junto con los intervalos y los valores de tiempo de espera.</span><span class="sxs-lookup"><span data-stu-id="4acab-265">You can define custom checks for hello health probe, along with intervals and timeout values.</span></span> <span data-ttu-id="4acab-266">Para más información sobre los sondeos de estado, consulte [Sondeos del Equilibrador de carga](../../load-balancer/load-balancer-custom-probe-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4acab-266">For more information about health probes, see [Load Balancer probes](../../load-balancer/load-balancer-custom-probe-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="4acab-267">Hello en el ejemplo siguiente se crea un TCP mantenimiento sondea con nombre `myHealthProbe`:</span><span class="sxs-lookup"><span data-stu-id="4acab-267">hello following example creates a TCP health probed named `myHealthProbe`:</span></span>

```azurecli
azure network lb probe create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myHealthProbe --protocol "tcp" \
  --interval 15 --count 4
```

<span data-ttu-id="4acab-268">Salida:</span><span class="sxs-lookup"><span data-stu-id="4acab-268">Output:</span></span>

```azurecli
info:    Executing command network lb probe create
warn:    Using default probe port: 80
+ Looking up hello load balancer "myLoadBalancer"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myHealthProbe
data:    Provisioning state              : Succeeded
data:    Protocol                        : Tcp
data:    Port                            : 80
data:    Interval in seconds             : 15
data:    Number of probes                : 4
info:    network lb probe create command OK
```

<span data-ttu-id="4acab-269">Aquí, especificamos un intervalo de 15 segundos para las comprobaciones de estado.</span><span class="sxs-lookup"><span data-stu-id="4acab-269">Here, we specified an interval of 15 seconds for our health checks.</span></span> <span data-ttu-id="4acab-270">Se puede perder un máximo de cuatro sondeos (un minuto) antes de equilibrador de carga de hello tiene en cuenta que hospedan Hola deja de funcionar.</span><span class="sxs-lookup"><span data-stu-id="4acab-270">We can miss a maximum of four probes (one minute) before hello load balancer considers that hello host is no longer functioning.</span></span>

## <a name="verify-hello-load-balancer"></a><span data-ttu-id="4acab-271">Compruebe el equilibrador de carga de Hola</span><span class="sxs-lookup"><span data-stu-id="4acab-271">Verify hello load balancer</span></span>
<span data-ttu-id="4acab-272">Ahora se realiza la configuración de equilibrador de carga de Hola.</span><span class="sxs-lookup"><span data-stu-id="4acab-272">Now hello load balancer configuration is done.</span></span> <span data-ttu-id="4acab-273">Estos son los pasos de hello que llevados a cabo:</span><span class="sxs-lookup"><span data-stu-id="4acab-273">Here are hello steps you took:</span></span>

1. <span data-ttu-id="4acab-274">Creó un equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="4acab-274">You created a load balancer.</span></span>
2. <span data-ttu-id="4acab-275">Ha creado un grupo IP de front-end y asignado un tooit IP pública.</span><span class="sxs-lookup"><span data-stu-id="4acab-275">You created a front-end IP pool and assigned a public IP tooit.</span></span>
3. <span data-ttu-id="4acab-276">Creó un grupo de direcciones IP back-end al que pueden conectarse las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="4acab-276">You created a back-end IP pool that VMs can connect to.</span></span>
4. <span data-ttu-id="4acab-277">Crear reglas NAT que permiten a las máquinas virtuales toohello SSH para la administración, junto con una regla que permita el puerto TCP 80 para nuestra aplicación web.</span><span class="sxs-lookup"><span data-stu-id="4acab-277">You created NAT rules that allow SSH toohello VMs for management, along with a rule that allows TCP port 80 for our web app.</span></span>
5. <span data-ttu-id="4acab-278">Ha agregado un Hola de comprobación de mantenimiento sondeo tooperiodically máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="4acab-278">You added a health probe tooperiodically check hello VMs.</span></span> <span data-ttu-id="4acab-279">Este sondeo de estado se asegura de que los usuarios no intentan tooaccess una máquina virtual que ya no está funcionando o que sirve al contenido.</span><span class="sxs-lookup"><span data-stu-id="4acab-279">This health probe ensures that users don't try tooaccess a VM that is no longer functioning or serving content.</span></span>

<span data-ttu-id="4acab-280">Revisemos cuál es ahora el aspecto del equilibrador de carga:</span><span class="sxs-lookup"><span data-stu-id="4acab-280">Let's review what your load balancer looks like now:</span></span>

```azurecli
azure network lb show --resource-group myResourceGroup \
  --name myLoadBalancer --json | jq '.'
```

<span data-ttu-id="4acab-281">Salida:</span><span class="sxs-lookup"><span data-stu-id="4acab-281">Output:</span></span>

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

## <a name="create-an-nic-toouse-with-hello-linux-vm"></a><span data-ttu-id="4acab-282">Crear un toouse NIC con hello VM de Linux</span><span class="sxs-lookup"><span data-stu-id="4acab-282">Create an NIC toouse with hello Linux VM</span></span>
<span data-ttu-id="4acab-283">NIC están disponibles mediante programación porque puede aplicar reglas tootheir uso.</span><span class="sxs-lookup"><span data-stu-id="4acab-283">NICs are programmatically available because you can apply rules tootheir use.</span></span> <span data-ttu-id="4acab-284">También puede tener más de una.</span><span class="sxs-lookup"><span data-stu-id="4acab-284">You can also have more than one.</span></span> <span data-ttu-id="4acab-285">En el siguiente de hello `azure network nic create` de comandos, enlazar grupo de direcciones IP de hello NIC toohello carga back-end y asociarlo con hello tráfico SSH de toopermit de regla NAT.</span><span class="sxs-lookup"><span data-stu-id="4acab-285">In hello following `azure network nic create` command, you hook up hello NIC toohello load back-end IP pool and associate it with hello NAT rule toopermit SSH traffic.</span></span>

<span data-ttu-id="4acab-286">Reemplace hello `#####-###-###` secciones con su propio identificador de suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="4acab-286">Replace hello `#####-###-###` sections with your own Azure subscription ID.</span></span> <span data-ttu-id="4acab-287">Su suscripción ID se indica en la salida de hello de `jq` al examinar los recursos de Hola que se va a crear.</span><span class="sxs-lookup"><span data-stu-id="4acab-287">Your subscription ID is noted in hello output of `jq` when you examine hello resources you are creating.</span></span> <span data-ttu-id="4acab-288">Su identificador de suscripción también puede verlo con `azure account list`.</span><span class="sxs-lookup"><span data-stu-id="4acab-288">You can also view your subscription ID with `azure account list`.</span></span>

<span data-ttu-id="4acab-289">Hello en el ejemplo siguiente se crea una NIC denominada `myNic1`:</span><span class="sxs-lookup"><span data-stu-id="4acab-289">hello following example creates a NIC named `myNic1`:</span></span>

```azurecli
azure network nic create --resource-group myResourceGroup --location westeurope \
  --subnet-vnet-name myVnet --subnet-name mySubnet --name myNic1 \
  --lb-address-pool-ids /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool \
  --lb-inbound-nat-rule-ids /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1
```

<span data-ttu-id="4acab-290">Salida:</span><span class="sxs-lookup"><span data-stu-id="4acab-290">Output:</span></span>

```azurecli
info:    Executing command network nic create
+ Looking up hello subnet "mySubnet"
+ Looking up hello network interface "myNic1"
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

<span data-ttu-id="4acab-291">Puede ver detalles de hello examinando recursos Hola directamente.</span><span class="sxs-lookup"><span data-stu-id="4acab-291">You can see hello details by examining hello resource directly.</span></span> <span data-ttu-id="4acab-292">Examinar recursos de hello mediante hello `azure network nic show` comando:</span><span class="sxs-lookup"><span data-stu-id="4acab-292">You examine hello resource by using hello `azure network nic show` command:</span></span>

```azurecli
azure network nic show myResourceGroup myNic1 --json | jq '.'
```

<span data-ttu-id="4acab-293">Salida:</span><span class="sxs-lookup"><span data-stu-id="4acab-293">Output:</span></span>

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

<span data-ttu-id="4acab-294">Ahora creamos Hola segundo NIC, enlazar en el grupo de direcciones IP de back-end de tooour de nuevo.</span><span class="sxs-lookup"><span data-stu-id="4acab-294">Now we create hello second NIC, hooking in tooour back-end IP pool again.</span></span> <span data-ttu-id="4acab-295">Esta regla NAT de tiempo Hola segunda permite el tráfico SSH.</span><span class="sxs-lookup"><span data-stu-id="4acab-295">This time hello second NAT rule permits SSH traffic.</span></span> <span data-ttu-id="4acab-296">Hello en el ejemplo siguiente se crea una NIC denominada `myNic2`:</span><span class="sxs-lookup"><span data-stu-id="4acab-296">hello following example creates a NIC named `myNic2`:</span></span>

```azurecli
azure network nic create --resource-group myResourceGroup --location westeurope \
  --subnet-vnet-name myVnet --subnet-name mySubnet --name myNic2 \
  --lb-address-pool-ids  /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool \
  --lb-inbound-nat-rule-ids /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH2
```

## <a name="create-a-network-security-group-and-rules"></a><span data-ttu-id="4acab-297">Creación de un grupo de seguridad de red (NSG) y las reglas</span><span class="sxs-lookup"><span data-stu-id="4acab-297">Create a network security group and rules</span></span>
<span data-ttu-id="4acab-298">Ahora se crea un grupo de seguridad de red y Hola entrantes reglas que rigen tener acceso a la NIC de toohello.</span><span class="sxs-lookup"><span data-stu-id="4acab-298">Now we create a network security group and hello inbound rules that govern access toohello NIC.</span></span> <span data-ttu-id="4acab-299">Un grupo de seguridad de red puede ser aplicada tooa NIC o subred.</span><span class="sxs-lookup"><span data-stu-id="4acab-299">A network security group can be applied tooa NIC or subnet.</span></span> <span data-ttu-id="4acab-300">Definir el flujo de hello toocontrol de reglas de tráfico de dentro y fuera de las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="4acab-300">You define rules toocontrol hello flow of traffic in and out of your VMs.</span></span> <span data-ttu-id="4acab-301">Hello en el ejemplo siguiente se crea un grupo de seguridad de red denominado `myNetworkSecurityGroup`:</span><span class="sxs-lookup"><span data-stu-id="4acab-301">hello following example creates a network security group named `myNetworkSecurityGroup`:</span></span>

```azurecli
azure network nsg create --resource-group myResourceGroup --location westeurope \
  --name myNetworkSecurityGroup
```

<span data-ttu-id="4acab-302">Vamos a agregar regla de entrada de Hola de hello NSG tooallow conexiones entrantes en el puerto 22 (SSH de toosupport).</span><span class="sxs-lookup"><span data-stu-id="4acab-302">Let's add hello inbound rule for hello NSG tooallow inbound connections on port 22 (toosupport SSH).</span></span> <span data-ttu-id="4acab-303">Hello en el ejemplo siguiente se crea una regla denominada `myNetworkSecurityGroupRuleSSH` tooallow TCP en el puerto 22:</span><span class="sxs-lookup"><span data-stu-id="4acab-303">hello following example creates a rule named `myNetworkSecurityGroupRuleSSH` tooallow TCP on port 22:</span></span>

```azurecli
azure network nsg rule create --resource-group myResourceGroup \
  --nsg-name myNetworkSecurityGroup --protocol tcp --direction inbound \
  --priority 1000 --destination-port-range 22 --access allow \
  --name myNetworkSecurityGroupRuleSSH
```

<span data-ttu-id="4acab-304">Ahora vamos a agregar regla de entrada de Hola de hello NSG tooallow conexiones entrantes en el puerto 80 (tráfico de web toosupport).</span><span class="sxs-lookup"><span data-stu-id="4acab-304">Now let's add hello inbound rule for hello NSG tooallow inbound connections on port 80 (toosupport web traffic).</span></span> <span data-ttu-id="4acab-305">Hello en el ejemplo siguiente se crea una regla denominada `myNetworkSecurityGroupRuleHTTP` tooallow TCP en el puerto 80:</span><span class="sxs-lookup"><span data-stu-id="4acab-305">hello following example creates a rule named `myNetworkSecurityGroupRuleHTTP` tooallow TCP on port 80:</span></span>

```azurecli
azure network nsg rule create --resource-group myResourceGroup \
  --nsg-name myNetworkSecurityGroup --protocol tcp --direction inbound \
  --priority 1001 --destination-port-range 80 --access allow \
  --name myNetworkSecurityGroupRuleHTTP
```

> [!NOTE]
> <span data-ttu-id="4acab-306">regla de entrada de Hello es un filtro para las conexiones de red de entrada.</span><span class="sxs-lookup"><span data-stu-id="4acab-306">hello inbound rule is a filter for inbound network connections.</span></span> <span data-ttu-id="4acab-307">En este ejemplo, se enlaza hello NSG toohello NIC virtual de máquinas virtuales, lo que significa que cualquier tooport solicitud 22 se pasa a través de toohello NIC en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="4acab-307">In this example, we bind hello NSG toohello VMs virtual NIC, which means that any request tooport 22 is passed through toohello NIC on our VM.</span></span> <span data-ttu-id="4acab-308">Esta regla de entrada es sobre una conexión de red y no sobre un punto de conexión, como en el caso de las implementaciones clásicas.</span><span class="sxs-lookup"><span data-stu-id="4acab-308">This inbound rule is about a network connection, and not about an endpoint, which is what it would be about in classic deployments.</span></span> <span data-ttu-id="4acab-309">tooopen un puerto, debe dejar hello `--source-port-range` establecido demasiado '\*' tooaccept (valor predeterminado de hello) entrada las solicitudes de **cualquier** solicitando el puerto.</span><span class="sxs-lookup"><span data-stu-id="4acab-309">tooopen a port, you must leave hello `--source-port-range` set too'\*' (hello default value) tooaccept inbound requests from **any** requesting port.</span></span> <span data-ttu-id="4acab-310">Los puertos suelen ser dinámicos.</span><span class="sxs-lookup"><span data-stu-id="4acab-310">Ports are typically dynamic.</span></span>
>
>

## <a name="bind-toohello-nic"></a><span data-ttu-id="4acab-311">Enlazar toohello NIC</span><span class="sxs-lookup"><span data-stu-id="4acab-311">Bind toohello NIC</span></span>
<span data-ttu-id="4acab-312">Enlazar hello NSG toohello NIC.</span><span class="sxs-lookup"><span data-stu-id="4acab-312">Bind hello NSG toohello NICs.</span></span> <span data-ttu-id="4acab-313">Necesitamos tooconnect nuestro NIC con nuestro grupo de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="4acab-313">We need tooconnect our NICs with our network security group.</span></span> <span data-ttu-id="4acab-314">Ejecutar ambos comandos, toohook tanto de nuestro NIC:</span><span class="sxs-lookup"><span data-stu-id="4acab-314">Run both commands, toohook up both of our NICs:</span></span>

```azurecli
azure network nic set --resource-group myResourceGroup --name myNic1 \
  --network-security-group-name myNetworkSecurityGroup
```

```azurecli
azure network nic set --resource-group myResourceGroup --name myNic2 \
  --network-security-group-name myNetworkSecurityGroup
```

## <a name="create-an-availability-set"></a><span data-ttu-id="4acab-315">Crear un conjunto de disponibilidad</span><span class="sxs-lookup"><span data-stu-id="4acab-315">Create an availability set</span></span>
<span data-ttu-id="4acab-316">Los conjuntos de disponibilidad ayudan a propagar las máquinas virtuales a los dominios de error y dominios de actualización.</span><span class="sxs-lookup"><span data-stu-id="4acab-316">Availability sets help spread your VMs across fault domains and upgrade domains.</span></span> <span data-ttu-id="4acab-317">Vamos a crear un conjunto de disponibilidad para sus máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="4acab-317">Let's create an availability set for your VMs.</span></span> <span data-ttu-id="4acab-318">Hello en el ejemplo siguiente se crea un conjunto con nombre de disponibilidad `myAvailabilitySet`:</span><span class="sxs-lookup"><span data-stu-id="4acab-318">hello following example creates an availability set named `myAvailabilitySet`:</span></span>

```azurecli
azure availset create --resource-group myResourceGroup --location westeurope
  --name myAvailabilitySet
```

<span data-ttu-id="4acab-319">Los dominios de error definen un grupo de máquinas virtuales que comparten una fuente de alimentación común y un conmutador de red.</span><span class="sxs-lookup"><span data-stu-id="4acab-319">Fault domains define a grouping of virtual machines that share a common power source and network switch.</span></span> <span data-ttu-id="4acab-320">De forma predeterminada, máquinas virtuales de Hola que estén configuradas en el conjunto de disponibilidad están separadas a través de dominios de error toothree.</span><span class="sxs-lookup"><span data-stu-id="4acab-320">By default, hello virtual machines that are configured within your availability set are separated across up toothree fault domains.</span></span> <span data-ttu-id="4acab-321">idea Hello es que un problema de hardware en uno de estos dominios de error no afecta a cada máquina virtual que se ejecuta la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4acab-321">hello idea is that a hardware issue in one of these fault domains does not affect every VM that is running your app.</span></span> <span data-ttu-id="4acab-322">Azure distribuye automáticamente las máquinas virtuales entre dominios de error de hello cuando se coloquen en un conjunto de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="4acab-322">Azure automatically distributes VMs across hello fault domains when placing them in an availability set.</span></span>

<span data-ttu-id="4acab-323">Dominios de actualización indican los grupos de máquinas virtuales y el hardware físico subyacente que puede reiniciarse en hello mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="4acab-323">Upgrade domains indicate groups of virtual machines and underlying physical hardware that can be rebooted at hello same time.</span></span> <span data-ttu-id="4acab-324">orden de Hello en el que se reinician los dominios de actualización no puede ser secuencial durante el mantenimiento planeado, pero se reinicia solo una actualización a la vez.</span><span class="sxs-lookup"><span data-stu-id="4acab-324">hello order in which upgrade domains are rebooted might not be sequential during planned maintenance, but only one upgrade is rebooted at a time.</span></span> <span data-ttu-id="4acab-325">De nuevo, Azure distribuye automáticamente las máquinas virtuales en los dominios de actualización al incluirlos en un sitio de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="4acab-325">Again, Azure automatically distributes your VMs across upgrade domains when placing them in an availability site.</span></span>

<span data-ttu-id="4acab-326">Obtenga más información sobre [administrar la disponibilidad de Hola de máquinas virtuales](manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4acab-326">Read more about [managing hello availability of VMs](manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="create-hello-linux-vms"></a><span data-ttu-id="4acab-327">Crear máquinas virtuales de Linux de Hola</span><span class="sxs-lookup"><span data-stu-id="4acab-327">Create hello Linux VMs</span></span>
<span data-ttu-id="4acab-328">Ha creado los recursos de red y almacenamiento de hello máquinas virtuales toosupport accesible desde Internet.</span><span class="sxs-lookup"><span data-stu-id="4acab-328">You've created hello storage and network resources toosupport Internet-accessible VMs.</span></span> <span data-ttu-id="4acab-329">Ahora crearemos dichas máquinas virtuales y las protegeremos con una clave SSH sin contraseña.</span><span class="sxs-lookup"><span data-stu-id="4acab-329">Now let's create those VMs and secure them with an SSH key that doesn't have a password.</span></span> <span data-ttu-id="4acab-330">En este caso, vamos toocreate una VM Ubuntu según hello LTS más reciente.</span><span class="sxs-lookup"><span data-stu-id="4acab-330">In this case, we're going toocreate an Ubuntu VM based on hello most recent LTS.</span></span> <span data-ttu-id="4acab-331">Vamos a buscar esa información de la imagen mediante `azure vm image list`, tal como se describe en el artículo sobre cómo [buscar imágenes de máquina virtual de Azure](../windows/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4acab-331">We locate that image information by using `azure vm image list`, as described in [finding Azure VM images](../windows/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="4acab-332">Se selecciona una imagen mediante el comando de hello `azure vm image list westeurope canonical | grep LTS`.</span><span class="sxs-lookup"><span data-stu-id="4acab-332">We selected an image by using hello command `azure vm image list westeurope canonical | grep LTS`.</span></span> <span data-ttu-id="4acab-333">En este caso, usamos `canonical:UbuntuServer:16.04.0-LTS:16.04.201608150`.</span><span class="sxs-lookup"><span data-stu-id="4acab-333">In this case, we use `canonical:UbuntuServer:16.04.0-LTS:16.04.201608150`.</span></span> <span data-ttu-id="4acab-334">Último campo hello, pasamos `latest` para que en un futuro Hola obtenemos siempre compilación más reciente de Hola.</span><span class="sxs-lookup"><span data-stu-id="4acab-334">For hello last field, we pass `latest` so that in hello future we always get hello most recent build.</span></span> <span data-ttu-id="4acab-335">(cadena Hola usamos es `canonical:UbuntuServer:16.04.0-LTS:16.04.201608150`).</span><span class="sxs-lookup"><span data-stu-id="4acab-335">(hello string we use is `canonical:UbuntuServer:16.04.0-LTS:16.04.201608150`).</span></span>

<span data-ttu-id="4acab-336">Este paso siguiente es familiar tooanyone que ya ha creado un ssh clave de rsa pública y privada emparejar en Linux o Mac usando **ssh-keygen - t rsa -b 2048**.</span><span class="sxs-lookup"><span data-stu-id="4acab-336">This next step is familiar tooanyone who has already created an ssh rsa public and private key pair on Linux or Mac by using **ssh-keygen -t rsa -b 2048**.</span></span> <span data-ttu-id="4acab-337">Si no tiene ningún par de claves de certificado en el directorio `~/.ssh` , puede crearlas:</span><span class="sxs-lookup"><span data-stu-id="4acab-337">If you do not have any certificate key pairs in your `~/.ssh` directory, you can create them:</span></span>

* <span data-ttu-id="4acab-338">Automáticamente, mediante el uso de hello `azure vm create --generate-ssh-keys` opción.</span><span class="sxs-lookup"><span data-stu-id="4acab-338">Automatically, by using hello `azure vm create --generate-ssh-keys` option.</span></span>
* <span data-ttu-id="4acab-339">Manualmente, mediante [Hola instrucciones toocreate ellos usted mismo](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4acab-339">Manually, by using [hello instructions toocreate them yourself](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="4acab-340">Como alternativa, puede usar hello `--admin-password` método tooauthenticate las conexiones SSH después Hola máquina virtual se crea.</span><span class="sxs-lookup"><span data-stu-id="4acab-340">Alternatively, you can use hello `--admin-password` method tooauthenticate your SSH connections after hello VM is created.</span></span> <span data-ttu-id="4acab-341">Este método suele ser menos seguro.</span><span class="sxs-lookup"><span data-stu-id="4acab-341">This method is typically less secure.</span></span>

<span data-ttu-id="4acab-342">Creamos Hola VM si se ponen todos nuestros recursos e información junto con hello `azure vm create` comando:</span><span class="sxs-lookup"><span data-stu-id="4acab-342">We create hello VM by bringing all our resources and information together with hello `azure vm create` command:</span></span>

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

<span data-ttu-id="4acab-343">Salida:</span><span class="sxs-lookup"><span data-stu-id="4acab-343">Output:</span></span>

```azurecli
info:    Executing command vm create
+ Looking up hello VM "myVM1"
info:    Verifying hello public key SSH file: /home/ahmet/.ssh/id_rsa.pub
info:    Using hello VM Size "Standard_DS1"
info:    hello [OS, Data] Disk or image configuration requires storage account
+ Looking up hello storage account mystorageaccount
+ Looking up hello availability set "myAvailabilitySet"
info:    Found an Availability set "myAvailabilitySet"
+ Looking up hello NIC "myNic1"
info:    Found an existing NIC "myNic1"
info:    Found an IP configuration with virtual network subnet id "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet" in hello NIC "myNic1"
info:    This is an NIC without publicIP configured
info:    hello storage URI 'https://mystorageaccount.blob.core.windows.net/' will be used for boot diagnostics settings, and it can be overwritten by hello parameter input of '--boot-diagnostics-storage-uri'.
info:    vm create command OK
```

<span data-ttu-id="4acab-344">Puede conectar tooyour VM inmediatamente mediante las claves SSH de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="4acab-344">You can connect tooyour VM immediately by using your default SSH keys.</span></span> <span data-ttu-id="4acab-345">Asegúrese de que especifique el puerto adecuado de hello puesto que estamos pasando a través del equilibrador de carga de Hola.</span><span class="sxs-lookup"><span data-stu-id="4acab-345">Make sure that you specify hello appropriate port since we're passing through hello load balancer.</span></span> <span data-ttu-id="4acab-346">(Para la primera VM, configuramos Hola NAT regla tooforward puerto 4222 tooour VM.)</span><span class="sxs-lookup"><span data-stu-id="4acab-346">(For our first VM, we set up hello NAT rule tooforward port 4222 tooour VM.)</span></span>

```bash
ssh ops@mypublicdns.westeurope.cloudapp.azure.com -p 4222
```

<span data-ttu-id="4acab-347">Salida:</span><span class="sxs-lookup"><span data-stu-id="4acab-347">Output:</span></span>

```bash
hello authenticity of host '[mypublicdns.westeurope.cloudapp.azure.com]:4222 ([xx.xx.xx.xx]:4222)' can't be established.
ECDSA key fingerprint is 94:2d:d0:ce:6b:fb:7f:ad:5b:3c:78:93:75:82:12:f9.
Are you sure you want toocontinue connecting (yes/no)? yes
Warning: Permanently added '[mypublicdns.westeurope.cloudapp.azure.com]:4222,[xx.xx.xx.xx]:4222' (ECDSA) toohello list of known hosts.
Welcome tooUbuntu 16.04.1 LTS (GNU/Linux 4.4.0-34-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  Get cloud support with Ubuntu Advantage Cloud Guest:
    http://www.ubuntu.com/business/services/cloud

0 packages can be updated.
0 updates are security updates.

ops@myVM1:~$
```

<span data-ttu-id="4acab-348">Voy a crear la segunda máquina virtual en hello misma manera:</span><span class="sxs-lookup"><span data-stu-id="4acab-348">Go ahead and create your second VM in hello same manner:</span></span>

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

<span data-ttu-id="4acab-349">Y ahora puede usar hello `azure vm show myResourceGroup myVM1` comando tooexamine lo que ha creado.</span><span class="sxs-lookup"><span data-stu-id="4acab-349">And you can now use hello `azure vm show myResourceGroup myVM1` command tooexamine what you've created.</span></span> <span data-ttu-id="4acab-350">Llegados a este punto, ejecuta las máquinas virtuales con Ubuntu detrás de un equilibrador de carga en Azure en las que solo puede iniciar sesión con el par de claves SSH (porque las contraseñas están deshabilitadas).</span><span class="sxs-lookup"><span data-stu-id="4acab-350">At this point, you're running your Ubuntu VMs behind a load balancer in Azure that you can sign into only with your SSH key pair (because passwords are disabled).</span></span> <span data-ttu-id="4acab-351">Puede instalar nginx o httpd, implementar una aplicación web y ver el tráfico de hello fluyen a través de hello tooboth de equilibrador de carga de máquinas virtuales de Hola.</span><span class="sxs-lookup"><span data-stu-id="4acab-351">You can install nginx or httpd, deploy a web app, and see hello traffic flow through hello load balancer tooboth of hello VMs.</span></span>

```azurecli
azure vm show --resource-group myResourceGroup --name myVM1
```

<span data-ttu-id="4acab-352">Salida:</span><span class="sxs-lookup"><span data-stu-id="4acab-352">Output:</span></span>

```azurecli
info:    Executing command vm show
+ Looking up hello VM "TestVM1"
+ Looking up hello NIC "myNic1"
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


## <a name="export-hello-environment-as-a-template"></a><span data-ttu-id="4acab-353">Entorno de Hola de exportación como plantilla</span><span class="sxs-lookup"><span data-stu-id="4acab-353">Export hello environment as a template</span></span>
<span data-ttu-id="4acab-354">Ahora que ha creado este entorno, ¿qué ocurre si desea toocreate un entorno de desarrollo adicional con hello mismos parámetros o un entorno de producción que coincida con él?</span><span class="sxs-lookup"><span data-stu-id="4acab-354">Now that you have built out this environment, what if you want toocreate an additional development environment with hello same parameters, or a production environment that matches it?</span></span> <span data-ttu-id="4acab-355">Administrador de recursos usa plantillas JSON que definen todos los parámetros de Hola para su entorno.</span><span class="sxs-lookup"><span data-stu-id="4acab-355">Resource Manager uses JSON templates that define all hello parameters for your environment.</span></span> <span data-ttu-id="4acab-356">Puede crear entornos enteros haciendo referencia a esta plantilla JSON.</span><span class="sxs-lookup"><span data-stu-id="4acab-356">You build out entire environments by referencing this JSON template.</span></span> <span data-ttu-id="4acab-357">También puede [generar plantillas JSON de forma manual](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) o exportar una plantilla JSON de entorno toocreate Hola existente para usted:</span><span class="sxs-lookup"><span data-stu-id="4acab-357">You can [build JSON templates manually](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or export an existing environment toocreate hello JSON template for you:</span></span>

```azurecli
azure group export --name myResourceGroup
```

<span data-ttu-id="4acab-358">Este comando crea hello `myResourceGroup.json` archivo en el directorio de trabajo actual.</span><span class="sxs-lookup"><span data-stu-id="4acab-358">This command creates hello `myResourceGroup.json` file in your current working directory.</span></span> <span data-ttu-id="4acab-359">Cuando se crea un entorno de esta plantilla, le pediremos todos los nombres de recursos de hello, incluidos los nombres de hello para el equilibrador de carga de hello, interfaces de red o máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="4acab-359">When you create an environment from this template, you are prompted for all hello resource names, including hello names for hello load balancer, network interfaces, or VMs.</span></span> <span data-ttu-id="4acab-360">Puede rellenar estos nombres en el archivo de plantilla mediante la adición de hello `-p` o `--includeParameterDefaultValue` toohello parámetro `azure group export` comando que se mostró anteriormente.</span><span class="sxs-lookup"><span data-stu-id="4acab-360">You can populate these names in your template file by adding hello `-p` or `--includeParameterDefaultValue` parameter toohello `azure group export` command that was shown earlier.</span></span> <span data-ttu-id="4acab-361">Editar los nombres de recursos JSON plantilla toospecify hello, o [crear un archivo parameters.json](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) que especifica los nombres de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="4acab-361">Edit your JSON template toospecify hello resource names, or [create a parameters.json file](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) that specifies hello resource names.</span></span>

<span data-ttu-id="4acab-362">toocreate un entorno a partir de la plantilla:</span><span class="sxs-lookup"><span data-stu-id="4acab-362">toocreate an environment from your template:</span></span>

```azurecli
azure group deployment create --resource-group myNewResourceGroup \
  --template-file myResourceGroup.json
```

<span data-ttu-id="4acab-363">Es recomendable tooread [más información acerca de cómo toodeploy de plantillas de](../../resource-group-template-deploy-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4acab-363">You might want tooread [more about how toodeploy from templates](../../resource-group-template-deploy-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="4acab-364">Obtenga información acerca de cómo usar el archivo de parámetros de hello tooincrementally entornos de actualización y tener acceso a plantillas desde una sola ubicación de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="4acab-364">Learn about how tooincrementally update environments, use hello parameters file, and access templates from a single storage location.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4acab-365">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4acab-365">Next steps</span></span>
<span data-ttu-id="4acab-366">Ahora está listo toobegin trabajar con varios componentes de red y máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="4acab-366">Now you're ready toobegin working with multiple networking components and VMs.</span></span> <span data-ttu-id="4acab-367">Puede usar este toobuild de entorno de ejemplo horizontalmente la aplicación con los componentes principales de hello introducidos aquí.</span><span class="sxs-lookup"><span data-stu-id="4acab-367">You can use this sample environment toobuild out your application by using hello core components introduced here.</span></span>
