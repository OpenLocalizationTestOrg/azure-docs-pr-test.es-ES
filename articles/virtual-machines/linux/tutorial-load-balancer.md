---
title: "aaaHow tooload equilibrar máquinas virtuales de Linux en Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse hello Azure carga equilibrador toocreate una aplicación de alta disponibilidad y segura entre tres máquinas virtuales de Linux"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/11/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: f01752c3caec3489ee13e63000775769f3236e11
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooload-balance-linux-virtual-machines-in-azure-toocreate-a-highly-available-application"></a><span data-ttu-id="eeb5c-103">¿Cómo tooload equilibrar máquinas virtuales de Linux en Azure toocreate una aplicación de alta disponibilidad</span><span class="sxs-lookup"><span data-stu-id="eeb5c-103">How tooload balance Linux virtual machines in Azure toocreate a highly available application</span></span>
<span data-ttu-id="eeb5c-104">El equilibrio de carga proporciona un mayor nivel de disponibilidad al distribuir las solicitudes entrantes entre varias máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="eeb5c-104">Load balancing provides a higher level of availability by spreading incoming requests across multiple virtual machines.</span></span> <span data-ttu-id="eeb5c-105">En este tutorial, aprenderá acerca de los componentes diferentes Hola Hola Azure del equilibrador de carga que distribución el tráfico y proporcionan una alta disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="eeb5c-105">In this tutorial, you learn about hello different components of hello Azure load balancer that distribute traffic and provide high availability.</span></span> <span data-ttu-id="eeb5c-106">Aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="eeb5c-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="eeb5c-107">Creación de un equilibrador de carga de Azure</span><span class="sxs-lookup"><span data-stu-id="eeb5c-107">Create an Azure load balancer</span></span>
> * <span data-ttu-id="eeb5c-108">Creación del sondeo de estado de un equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="eeb5c-108">Create a load balancer health probe</span></span>
> * <span data-ttu-id="eeb5c-109">Crear reglas de tráfico del equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="eeb5c-109">Create load balancer traffic rules</span></span>
> * <span data-ttu-id="eeb5c-110">Usar en la nube init toocreate una aplicación básica de Node.js</span><span class="sxs-lookup"><span data-stu-id="eeb5c-110">Use cloud-init toocreate a basic Node.js app</span></span>
> * <span data-ttu-id="eeb5c-111">Crear máquinas virtuales y adjuntar tooa equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="eeb5c-111">Create virtual machines and attach tooa load balancer</span></span>
> * <span data-ttu-id="eeb5c-112">Ver un equilibrador de carga en acción</span><span class="sxs-lookup"><span data-stu-id="eeb5c-112">View a load balancer in action</span></span>
> * <span data-ttu-id="eeb5c-113">Agregar y quitar las máquinas virtuales de un equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="eeb5c-113">Add and remove VMs from a load balancer</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="eeb5c-114">Si elige tooinstall y usar hello CLI localmente, este tutorial requiere que se ejecuta la versión de CLI de Azure de hello 2.0.4 o versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="eeb5c-114">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="eeb5c-115">Ejecutar `az --version` toofind versión de Hola.</span><span class="sxs-lookup"><span data-stu-id="eeb5c-115">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="eeb5c-116">Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="eeb5c-116">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="azure-load-balancer-overview"></a><span data-ttu-id="eeb5c-117">Información general sobre Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="eeb5c-117">Azure load balancer overview</span></span>
<span data-ttu-id="eeb5c-118">Un equilibrador de carga de Azure es un equilibrador de carga de nivel 4 (TCP, UDP) que proporciona una alta disponibilidad mediante la distribución del tráfico entrante entre máquinas virtuales con un estado correcto.</span><span class="sxs-lookup"><span data-stu-id="eeb5c-118">An Azure load balancer is a Layer-4 (TCP, UDP) load balancer that provides high availability by distributing incoming traffic among healthy VMs.</span></span> <span data-ttu-id="eeb5c-119">Un sondeo de estado de equilibrador de carga supervisa un puerto determinado en cada máquina virtual y sólo distribuye el tráfico tooan VM operativa.</span><span class="sxs-lookup"><span data-stu-id="eeb5c-119">A load balancer health probe monitors a given port on each VM and only distributes traffic tooan operational VM.</span></span>

<span data-ttu-id="eeb5c-120">Se define una configuración de IP de front-end que contiene una o varias direcciones IP públicas.</span><span class="sxs-lookup"><span data-stu-id="eeb5c-120">You define a front-end IP configuration that contains one or more public IP addresses.</span></span> <span data-ttu-id="eeb5c-121">Esta configuración de IP de front-end permite que su toobe de aplicaciones y el equilibrador de carga puede tener acceso a través de Internet de Hola.</span><span class="sxs-lookup"><span data-stu-id="eeb5c-121">This front-end IP configuration allows your load balancer and applications toobe accessible over hello Internet.</span></span> 

<span data-ttu-id="eeb5c-122">Máquinas virtuales se conectarán tooa equilibrador de carga con la tarjeta de interfaz de red virtual (NIC).</span><span class="sxs-lookup"><span data-stu-id="eeb5c-122">Virtual machines connect tooa load balancer using their virtual network interface card (NIC).</span></span> <span data-ttu-id="eeb5c-123">toodistribute tráfico toohello máquinas virtuales, un grupo de direcciones de back-end contiene direcciones IP de Hola Hola virtual (NIC) toohello conectados del equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="eeb5c-123">toodistribute traffic toohello VMs, a back-end address pool contains hello IP addresses of hello virtual (NICs) connected toohello load balancer.</span></span>

<span data-ttu-id="eeb5c-124">flujo de hello toocontrol de tráfico, defina reglas de equilibrador de carga para determinados puertos y protocolos que se asignan tooyour las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="eeb5c-124">toocontrol hello flow of traffic, you define load balancer rules for specific ports and protocols that map tooyour VMs.</span></span>

<span data-ttu-id="eeb5c-125">Si ha seguido tutorial anterior Hola demasiado[crear un conjunto de escalas de máquina virtual](tutorial-create-vmss.md), se creó un equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="eeb5c-125">If you followed hello previous tutorial too[create a virtual machine scale set](tutorial-create-vmss.md), a load balancer was created for you.</span></span> <span data-ttu-id="eeb5c-126">Todos estos componentes se configuran automáticamente como parte del conjunto de escalas de Hola.</span><span class="sxs-lookup"><span data-stu-id="eeb5c-126">All these components were configured for you as part of hello scale set.</span></span>


## <a name="create-azure-load-balancer"></a><span data-ttu-id="eeb5c-127">Creación del equilibrador de carga de Azure</span><span class="sxs-lookup"><span data-stu-id="eeb5c-127">Create Azure load balancer</span></span>
<span data-ttu-id="eeb5c-128">Esta sección detalla cómo puede crear y configurar cada componente Hola de equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="eeb5c-128">This section details how you can create and configure each component of hello load balancer.</span></span> <span data-ttu-id="eeb5c-129">Antes de poder crear el equilibrador de carga, cree un grupo de recursos con [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="eeb5c-129">Before you can create your load balancer, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="eeb5c-130">Hello en el ejemplo siguiente se crea un grupo de recursos denominado *myResourceGroupLoadBalancer* en hello *eastus* ubicación:</span><span class="sxs-lookup"><span data-stu-id="eeb5c-130">hello following example creates a resource group named *myResourceGroupLoadBalancer* in hello *eastus* location:</span></span>

```azurecli-interactive 
az group create --name myResourceGroupLoadBalancer --location eastus
```

### <a name="create-a-public-ip-address"></a><span data-ttu-id="eeb5c-131">Crear una dirección IP pública</span><span class="sxs-lookup"><span data-stu-id="eeb5c-131">Create a public IP address</span></span>
<span data-ttu-id="eeb5c-132">tooaccess Hola de la aplicación en Internet, necesita una dirección IP pública para el equilibrador de carga de Hola.</span><span class="sxs-lookup"><span data-stu-id="eeb5c-132">tooaccess your app on hello Internet, you need a public IP address for hello load balancer.</span></span> <span data-ttu-id="eeb5c-133">Cree una dirección IP pública con [az network public-ip create](/cli/azure/network/public-ip#create).</span><span class="sxs-lookup"><span data-stu-id="eeb5c-133">Create a public IP address with [az network public-ip create](/cli/azure/network/public-ip#create).</span></span> <span data-ttu-id="eeb5c-134">Hello en el ejemplo siguiente se crea una dirección IP pública denominada *myPublicIP* en hello *myResourceGroupLoadBalancer* grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="eeb5c-134">hello following example creates a public IP address named *myPublicIP* in hello *myResourceGroupLoadBalancer* resource group:</span></span>

```azurecli-interactive 
az network public-ip create \
    --resource-group myResourceGroupLoadBalancer \
    --name myPublicIP
```

### <a name="create-a-load-balancer"></a><span data-ttu-id="eeb5c-135">Crear un equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="eeb5c-135">Create a load balancer</span></span>
<span data-ttu-id="eeb5c-136">Cree un equilibrador de carga con [az network lb create](/cli/azure/network/lb#create).</span><span class="sxs-lookup"><span data-stu-id="eeb5c-136">Create a load balancer with [az network lb create](/cli/azure/network/lb#create).</span></span> <span data-ttu-id="eeb5c-137">Hello en el ejemplo siguiente se crea un equilibrador de carga con el nombre *myLoadBalancer* asigna hello y *myPublicIP* configuración de IP de front-end de dirección toohello:</span><span class="sxs-lookup"><span data-stu-id="eeb5c-137">hello following example creates a load balancer named *myLoadBalancer* and assigns hello *myPublicIP* address toohello front-end IP configuration:</span></span>

```azurecli-interactive 
az network lb create \
    --resource-group myResourceGroupLoadBalancer \
    --name myLoadBalancer \
    --frontend-ip-name myFrontEndPool \
    --backend-pool-name myBackEndPool \
    --public-ip-address myPublicIP
```

### <a name="create-a-health-probe"></a><span data-ttu-id="eeb5c-138">Creación de un sondeo de estado</span><span class="sxs-lookup"><span data-stu-id="eeb5c-138">Create a health probe</span></span>
<span data-ttu-id="eeb5c-139">tooallow Hola equilibrador toomonitor Hola estado de carga de la aplicación, utilice un sondeo de estado.</span><span class="sxs-lookup"><span data-stu-id="eeb5c-139">tooallow hello load balancer toomonitor hello status of your app, you use a health probe.</span></span> <span data-ttu-id="eeb5c-140">sondeo de estado de Hello dinámicamente agrega o quita las máquinas virtuales de rotación del equilibrador de carga de hello en función de sus comprobaciones de toohealth de respuesta.</span><span class="sxs-lookup"><span data-stu-id="eeb5c-140">hello health probe dynamically adds or removes VMs from hello load balancer rotation based on their response toohealth checks.</span></span> <span data-ttu-id="eeb5c-141">De forma predeterminada, una máquina virtual se quita de la distribución de equilibrador de carga de hello después de dos errores consecutivos en intervalos de 15 segundos.</span><span class="sxs-lookup"><span data-stu-id="eeb5c-141">By default, a VM is removed from hello load balancer distribution after two consecutive failures at 15-second intervals.</span></span> <span data-ttu-id="eeb5c-142">Cree un sondeo de estado en función de un protocolo o una página de comprobación de mantenimiento específica para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="eeb5c-142">You create a health probe based on a protocol or a specific health check page for your app.</span></span> 

<span data-ttu-id="eeb5c-143">Hola siguiente ejemplo crea un sondeo TCP.</span><span class="sxs-lookup"><span data-stu-id="eeb5c-143">hello following example creates a TCP probe.</span></span> <span data-ttu-id="eeb5c-144">También se pueden crear sondeos HTTP personalizados para comprobaciones de estado más específicas.</span><span class="sxs-lookup"><span data-stu-id="eeb5c-144">You can also create custom HTTP probes for more fine grained health checks.</span></span> <span data-ttu-id="eeb5c-145">Al utilizar un sondeo HTTP personalizado, debe crear página de comprobación de mantenimiento de hello, como *healthcheck.js*.</span><span class="sxs-lookup"><span data-stu-id="eeb5c-145">When using a custom HTTP probe, you must create hello health check page, such as *healthcheck.js*.</span></span> <span data-ttu-id="eeb5c-146">sondeo de Hello debe devolver un **HTTP 200 OK** respuesta para host Hola carga equilibrador tookeep Hola de rotación.</span><span class="sxs-lookup"><span data-stu-id="eeb5c-146">hello probe must return an **HTTP 200 OK** response for hello load balancer tookeep hello host in rotation.</span></span>

<span data-ttu-id="eeb5c-147">toocreate un sondeo de estado TCP, use [crear la prueba de carga equilibrada de red az](/cli/azure/network/lb/probe#create).</span><span class="sxs-lookup"><span data-stu-id="eeb5c-147">toocreate a TCP health probe, you use [az network lb probe create](/cli/azure/network/lb/probe#create).</span></span> <span data-ttu-id="eeb5c-148">Hello en el ejemplo siguiente se crea un sondeo de estado denominado *myHealthProbe*:</span><span class="sxs-lookup"><span data-stu-id="eeb5c-148">hello following example creates a health probe named *myHealthProbe*:</span></span>

```azurecli-interactive 
az network lb probe create \
    --resource-group myResourceGroupLoadBalancer \
    --lb-name myLoadBalancer \
    --name myHealthProbe \
    --protocol tcp \
    --port 80
```

### <a name="create-a-load-balancer-rule"></a><span data-ttu-id="eeb5c-149">Creación de una regla de equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="eeb5c-149">Create a load balancer rule</span></span>
<span data-ttu-id="eeb5c-150">Una regla de equilibrador de carga es toodefine usado cómo tráfico es distribuida toohello máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="eeb5c-150">A load balancer rule is used toodefine how traffic is distributed toohello VMs.</span></span> <span data-ttu-id="eeb5c-151">Definir configuración de IP front-end de hello para el tráfico entrante de Hola y Hola back-end grupo tooreceive Hola tráfico IP, junto con el origen de hello necesarios y el puerto de destino.</span><span class="sxs-lookup"><span data-stu-id="eeb5c-151">You define hello front-end IP configuration for hello incoming traffic and hello back-end IP pool tooreceive hello traffic, along with hello required source and destination port.</span></span> <span data-ttu-id="eeb5c-152">toomake seguro que solo las máquinas virtuales correcto reciban tráfico, también definir toouse de sondeo de estado de Hola.</span><span class="sxs-lookup"><span data-stu-id="eeb5c-152">toomake sure only healthy VMs receive traffic, you also define hello health probe toouse.</span></span>

<span data-ttu-id="eeb5c-153">Cree una regla de equilibrador de carga con [az network lb rule create](/cli/azure/network/lb/rule#create).</span><span class="sxs-lookup"><span data-stu-id="eeb5c-153">Create a load balancer rule with [az network lb rule create](/cli/azure/network/lb/rule#create).</span></span> <span data-ttu-id="eeb5c-154">Hello en el ejemplo siguiente se crea una regla denominada *myLoadBalancerRule*, usa hello *myHealthProbe* sondeo de estado y equilibra el tráfico en el puerto *80*:</span><span class="sxs-lookup"><span data-stu-id="eeb5c-154">hello following example creates a rule named *myLoadBalancerRule*, uses hello *myHealthProbe* health probe, and balances traffic on port *80*:</span></span>

```azurecli-interactive 
az network lb rule create \
    --resource-group myResourceGroupLoadBalancer \
    --lb-name myLoadBalancer \
    --name myLoadBalancerRule \
    --protocol tcp \
    --frontend-port 80 \
    --backend-port 80 \
    --frontend-ip-name myFrontEndPool \
    --backend-pool-name myBackEndPool \
    --probe-name myHealthProbe
```


## <a name="configure-virtual-network"></a><span data-ttu-id="eeb5c-155">Configuración de una red virtual</span><span class="sxs-lookup"><span data-stu-id="eeb5c-155">Configure virtual network</span></span>
<span data-ttu-id="eeb5c-156">Antes de implementar algunas máquinas virtuales y puede probar su equilibrador, crear Hola compatibilidad con recursos de red virtual.</span><span class="sxs-lookup"><span data-stu-id="eeb5c-156">Before you deploy some VMs and can test your balancer, create hello supporting virtual network resources.</span></span> <span data-ttu-id="eeb5c-157">Para obtener más información sobre las redes virtuales, vea hello [administrar redes virtuales de Azure](tutorial-virtual-network.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="eeb5c-157">For more information about virtual networks, see hello [Manage Azure Virtual Networks](tutorial-virtual-network.md) tutorial.</span></span>

### <a name="create-network-resources"></a><span data-ttu-id="eeb5c-158">Crear recursos de red</span><span class="sxs-lookup"><span data-stu-id="eeb5c-158">Create network resources</span></span>
<span data-ttu-id="eeb5c-159">Cree la red virtual con el comando [az network vnet create](/cli/azure/network/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="eeb5c-159">Create a virtual network with [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="eeb5c-160">Hello en el ejemplo siguiente se crea una red virtual denominada *myVnet* con una subred denominada *mySubnet*:</span><span class="sxs-lookup"><span data-stu-id="eeb5c-160">hello following example creates a virtual network named *myVnet* with a subnet named *mySubnet*:</span></span>

```azurecli-interactive 
az network vnet create \
    --resource-group myResourceGroupLoadBalancer \
    --name myVnet \
    --subnet-name mySubnet
```

<span data-ttu-id="eeb5c-161">tooadd un grupo de seguridad de red, use [crear az red nsg](/cli/azure/network/nsg#create).</span><span class="sxs-lookup"><span data-stu-id="eeb5c-161">tooadd a network security group, you use [az network nsg create](/cli/azure/network/nsg#create).</span></span> <span data-ttu-id="eeb5c-162">Hello en el ejemplo siguiente se crea un grupo de seguridad de red denominado *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="eeb5c-162">hello following example creates a network security group named *myNetworkSecurityGroup*:</span></span>

```azurecli-interactive 
az network nsg create \
    --resource-group myResourceGroupLoadBalancer \
    --name myNetworkSecurityGroup
```

<span data-ttu-id="eeb5c-163">Cree una regla de grupo de seguridad de red con el comando [az network nsg rule create](/cli/azure/network/nsg/rule#create).</span><span class="sxs-lookup"><span data-stu-id="eeb5c-163">Create a network security group rule with [az network nsg rule create](/cli/azure/network/nsg/rule#create).</span></span> <span data-ttu-id="eeb5c-164">Hello en el ejemplo siguiente se crea una regla de grupo de seguridad de red denominada *myNetworkSecurityGroupRule*:</span><span class="sxs-lookup"><span data-stu-id="eeb5c-164">hello following example creates a network security group rule named *myNetworkSecurityGroupRule*:</span></span>

```azurecli-interactive 
az network nsg rule create \
    --resource-group myResourceGroupLoadBalancer \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --priority 1001 \
    --protocol tcp \
    --destination-port-range 80
```

<span data-ttu-id="eeb5c-165">Las NIC virtuales se crean con el comando [az network nic create](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="eeb5c-165">Virtual NICs are created with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="eeb5c-166">Hello en el ejemplo siguiente se crea tres NIC virtuales.</span><span class="sxs-lookup"><span data-stu-id="eeb5c-166">hello following example creates three virtual NICs.</span></span> <span data-ttu-id="eeb5c-167">(Una NIC virtual para cada máquina virtual crea para la aplicación Hola siguiendo los pasos).</span><span class="sxs-lookup"><span data-stu-id="eeb5c-167">(One virtual NIC for each VM you create for your app in hello following steps).</span></span> <span data-ttu-id="eeb5c-168">Puede crear NIC virtuales adicionales y las máquinas virtuales en cualquier momento y agregarlos toohello equilibrador de carga:</span><span class="sxs-lookup"><span data-stu-id="eeb5c-168">You can create additional virtual NICs and VMs at any time and add them toohello load balancer:</span></span>

```bash
for i in `seq 1 3`; do
    az network nic create \
        --resource-group myResourceGroupLoadBalancer \
        --name myNic$i \
        --vnet-name myVnet \
        --subnet mySubnet \
        --network-security-group myNetworkSecurityGroup \
        --lb-name myLoadBalancer \
        --lb-address-pools myBackEndPool
done
```

## <a name="create-virtual-machines"></a><span data-ttu-id="eeb5c-169">Creación de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="eeb5c-169">Create virtual machines</span></span>

### <a name="create-cloud-init-config"></a><span data-ttu-id="eeb5c-170">Creación de cloud-init config</span><span class="sxs-lookup"><span data-stu-id="eeb5c-170">Create cloud-init config</span></span>
<span data-ttu-id="eeb5c-171">En un tutorial anterior en [cómo toocustomize una máquina virtual de Linux en el primer arranque](tutorial-automate-vm-deployment.md), también habrá aprendido cómo tooautomate personalización de máquina virtual con init de la nube.</span><span class="sxs-lookup"><span data-stu-id="eeb5c-171">In a previous tutorial on [How toocustomize a Linux virtual machine on first boot](tutorial-automate-vm-deployment.md), you learned how tooautomate VM customization with cloud-init.</span></span> <span data-ttu-id="eeb5c-172">Puede usar Hola mismo tooinstall de archivo de configuración de nube init NGINX y ejecutar una aplicación sencilla de Node.js de "Hello World".</span><span class="sxs-lookup"><span data-stu-id="eeb5c-172">You can use hello same cloud-init configuration file tooinstall NGINX and run a simple 'Hello World' Node.js app.</span></span>

<span data-ttu-id="eeb5c-173">En el shell actual, cree un archivo denominado *init.txt nube* y pegar Hola siguiente configuración.</span><span class="sxs-lookup"><span data-stu-id="eeb5c-173">In your current shell, create a file named *cloud-init.txt* and paste hello following configuration.</span></span> <span data-ttu-id="eeb5c-174">Por ejemplo, crear archivo hello en hello Shell en la nube, no en el equipo local.</span><span class="sxs-lookup"><span data-stu-id="eeb5c-174">For example, create hello file in hello Cloud Shell not on your local machine.</span></span> <span data-ttu-id="eeb5c-175">Escriba `sensible-editor cloud-init.txt` toocreate Hola archivo y ver una lista de editores disponibles.</span><span class="sxs-lookup"><span data-stu-id="eeb5c-175">Enter `sensible-editor cloud-init.txt` toocreate hello file and see a list of available editors.</span></span> <span data-ttu-id="eeb5c-176">Asegúrese de que ese archivo de nube-init todo Hola se copia correctamente, especialmente Hola primera línea:</span><span class="sxs-lookup"><span data-stu-id="eeb5c-176">Make sure that hello whole cloud-init file is copied correctly, especially hello first line:</span></span>

```yaml
#cloud-config
package_upgrade: true
packages:
  - nginx
  - nodejs
  - npm
write_files:
  - owner: www-data:www-data
  - path: /etc/nginx/sites-available/default
    content: |
      server {
        listen 80;
        location / {
          proxy_pass http://localhost:3000;
          proxy_http_version 1.1;
          proxy_set_header Upgrade $http_upgrade;
          proxy_set_header Connection keep-alive;
          proxy_set_header Host $host;
          proxy_cache_bypass $http_upgrade;
        }
      }
  - owner: azureuser:azureuser
  - path: /home/azureuser/myapp/index.js
    content: |
      var express = require('express')
      var app = express()
      var os = require('os');
      app.get('/', function (req, res) {
        res.send('Hello World from host ' + os.hostname() + '!')
      })
      app.listen(3000, function () {
        console.log('Hello world app listening on port 3000!')
      })
runcmd:
  - service nginx restart
  - cd "/home/azureuser/myapp"
  - npm init
  - npm install express -y
  - nodejs index.js
```

### <a name="create-virtual-machines"></a><span data-ttu-id="eeb5c-177">Creación de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="eeb5c-177">Create virtual machines</span></span>
<span data-ttu-id="eeb5c-178">alta disponibilidad de Hola de tooimprove de la aplicación, coloque las máquinas virtuales en un conjunto de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="eeb5c-178">tooimprove hello high availability of your app, place your VMs in an availability set.</span></span> <span data-ttu-id="eeb5c-179">Para obtener más información acerca de los conjuntos de disponibilidad, vea Hola anterior [cómo máquinas virtuales de alta disponibilidad toocreate](tutorial-availability-sets.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="eeb5c-179">For more information about availability sets, see hello previous [How toocreate highly available virtual machines](tutorial-availability-sets.md) tutorial.</span></span>

<span data-ttu-id="eeb5c-180">Cree el conjunto de disponibilidad con [az vm availability-set create](/cli/azure/vm/availability-set#create).</span><span class="sxs-lookup"><span data-stu-id="eeb5c-180">Create an availability set with [az vm availability-set create](/cli/azure/vm/availability-set#create).</span></span> <span data-ttu-id="eeb5c-181">Hello en el ejemplo siguiente se crea un conjunto con nombre de disponibilidad *myAvailabilitySet*:</span><span class="sxs-lookup"><span data-stu-id="eeb5c-181">hello following example creates an availability set named *myAvailabilitySet*:</span></span>

```azurecli-interactive 
az vm availability-set create \
    --resource-group myResourceGroupLoadBalancer \
    --name myAvailabilitySet
```

<span data-ttu-id="eeb5c-182">Ahora puede crear máquinas virtuales de hello con [crear vm az](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="eeb5c-182">Now you can create hello VMs with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="eeb5c-183">Hello en el ejemplo siguiente se crea tres máquinas virtuales y genera claves de SSH si aún no existen:</span><span class="sxs-lookup"><span data-stu-id="eeb5c-183">hello following example creates three VMs and generates SSH keys if they do not already exist:</span></span>

```bash
for i in `seq 1 3`; do
    az vm create \
        --resource-group myResourceGroupLoadBalancer \
        --name myVM$i \
        --availability-set myAvailabilitySet \
        --nics myNic$i \
        --image UbuntuLTS \
        --admin-username azureuser \
        --generate-ssh-keys \
        --custom-data cloud-init.txt \
        --no-wait
done
```

<span data-ttu-id="eeb5c-184">Hay tareas en segundo plano que continúan toorun después de hello CLI de Azure devuelve toohello símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="eeb5c-184">There are background tasks that continue toorun after hello Azure CLI returns you toohello prompt.</span></span> <span data-ttu-id="eeb5c-185">Hola `--no-wait` parámetro no esperar todos Hola toocomplete de tareas.</span><span class="sxs-lookup"><span data-stu-id="eeb5c-185">hello `--no-wait` parameter does not wait for all hello tasks toocomplete.</span></span> <span data-ttu-id="eeb5c-186">Es posible que otro par de minutos antes de que se puede tener acceso a la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="eeb5c-186">It may be another couple of minutes before you can access hello app.</span></span> <span data-ttu-id="eeb5c-187">Hello sondeo de estado del equilibrador de carga detecta automáticamente cuando se ejecuta la aplicación hello en cada máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="eeb5c-187">hello load balancer health probe automatically detects when hello app is running on each VM.</span></span> <span data-ttu-id="eeb5c-188">Una vez que se ejecuta la aplicación hello, regla de equilibrador de carga de hello inicia toodistribute tráfico.</span><span class="sxs-lookup"><span data-stu-id="eeb5c-188">Once hello app is running, hello load balancer rule starts toodistribute traffic.</span></span>


## <a name="test-load-balancer"></a><span data-ttu-id="eeb5c-189">Prueba del equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="eeb5c-189">Test load balancer</span></span>
<span data-ttu-id="eeb5c-190">Obtener dirección IP pública de Hola de un equilibrador de carga con [show de public-ip de red az](/cli/azure/network/public-ip#show).</span><span class="sxs-lookup"><span data-stu-id="eeb5c-190">Obtain hello public IP address of your load balancer with [az network public-ip show](/cli/azure/network/public-ip#show).</span></span> <span data-ttu-id="eeb5c-191">Hello en el ejemplo siguiente se obtiene la dirección IP de Hola para *myPublicIP* creado anteriormente:</span><span class="sxs-lookup"><span data-stu-id="eeb5c-191">hello following example obtains hello IP address for *myPublicIP* created earlier:</span></span>

```azurecli-interactive 
az network public-ip show \
    --resource-group myResourceGroupLoadBalancer \
    --name myPublicIP \
    --query [ipAddress] \
    --output tsv
```

<span data-ttu-id="eeb5c-192">A continuación, puede escribir la dirección IP pública hello en el Explorador de web tooa.</span><span class="sxs-lookup"><span data-stu-id="eeb5c-192">You can then enter hello public IP address in tooa web browser.</span></span> <span data-ttu-id="eeb5c-193">Recuerde: tarda unos minutos Estados de Hola de Hola de máquinas virtuales toobe listo antes de equilibrador de carga de hello inicia toodistribute tráfico toothem.</span><span class="sxs-lookup"><span data-stu-id="eeb5c-193">Remember - it takes a few minutes hello hello VMs toobe ready before hello load balancer starts toodistribute traffic toothem.</span></span> <span data-ttu-id="eeb5c-194">se muestra la aplicación Hello, incluyendo hostname Hola de hello VM ese equilibrador de carga de hello distribuye tooas de tráfico en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="eeb5c-194">hello app is displayed, including hello hostname of hello VM that hello load balancer distributed traffic tooas in hello following example:</span></span>

![Ejecución de la aplicación Node.js](./media/tutorial-load-balancer/running-nodejs-app.png)

<span data-ttu-id="eeb5c-196">equilibrador de carga de hello toosee distribuir el tráfico entre todas las tres VM que se ejecuta la aplicación, se puede forzar actualización el explorador web.</span><span class="sxs-lookup"><span data-stu-id="eeb5c-196">toosee hello load balancer distribute traffic across all three VMs running your app, you can force-refresh your web browser.</span></span>


## <a name="add-and-remove-vms"></a><span data-ttu-id="eeb5c-197">Agregar y quitar máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="eeb5c-197">Add and remove VMs</span></span>
<span data-ttu-id="eeb5c-198">Puede que necesite tooperform mantenimiento en hello máquinas virtuales que ejecutan la aplicación, como la instalación de actualizaciones del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="eeb5c-198">You may need tooperform maintenance on hello VMs running your app, such as installing OS updates.</span></span> <span data-ttu-id="eeb5c-199">toodeal con un aumento del tráfico tooyour aplicación, puede que necesite tooadd máquinas virtuales adicionales.</span><span class="sxs-lookup"><span data-stu-id="eeb5c-199">toodeal with increased traffic tooyour app, you may need tooadd additional VMs.</span></span> <span data-ttu-id="eeb5c-200">Esta sección muestra cómo tooremove o agregar una máquina virtual desde el equilibrador de carga de Hola.</span><span class="sxs-lookup"><span data-stu-id="eeb5c-200">This section shows you how tooremove or add a VM from hello load balancer.</span></span>

### <a name="remove-a-vm-from-hello-load-balancer"></a><span data-ttu-id="eeb5c-201">Quitar una máquina virtual de equilibrador de carga de Hola</span><span class="sxs-lookup"><span data-stu-id="eeb5c-201">Remove a VM from hello load balancer</span></span>
<span data-ttu-id="eeb5c-202">Puede quitar una máquina virtual del grupo de direcciones de back-end de hello con [az red nic ip-config-grupo de direcciones quitar](/cli/azure/network/nic/ip-config/address-pool#remove).</span><span class="sxs-lookup"><span data-stu-id="eeb5c-202">You can remove a VM from hello backend address pool with [az network nic ip-config address-pool remove](/cli/azure/network/nic/ip-config/address-pool#remove).</span></span> <span data-ttu-id="eeb5c-203">Hola siguiente ejemplo quita Hola NIC virtual para **myVM2** de *myLoadBalancer*:</span><span class="sxs-lookup"><span data-stu-id="eeb5c-203">hello following example removes hello virtual NIC for **myVM2** from *myLoadBalancer*:</span></span>

```azurecli-interactive 
az network nic ip-config address-pool remove \
    --resource-group myResourceGroupLoadBalancer \
    --nic-name myNic2 \
    --ip-config-name ipConfig1 \
    --lb-name myLoadBalancer \
    --address-pool myBackEndPool 
```

<span data-ttu-id="eeb5c-204">equilibrador de carga de hello toosee distribuir el tráfico entre Hola otras dos máquinas virtuales que ejecutan la aplicación puede forzar actualización el explorador web.</span><span class="sxs-lookup"><span data-stu-id="eeb5c-204">toosee hello load balancer distribute traffic across hello remaining two VMs running your app you can force-refresh your web browser.</span></span> <span data-ttu-id="eeb5c-205">Ahora puede realizar el mantenimiento en Hola de máquina virtual, como instalar actualizaciones del sistema operativo o realizar un reinicio de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="eeb5c-205">You can now perform maintenance on hello VM, such as installing OS updates or performing a VM reboot.</span></span>

### <a name="add-a-vm-toohello-load-balancer"></a><span data-ttu-id="eeb5c-206">Agregar un equilibrador de carga de toohello VM</span><span class="sxs-lookup"><span data-stu-id="eeb5c-206">Add a VM toohello load balancer</span></span>
<span data-ttu-id="eeb5c-207">Después de realizar el mantenimiento de la máquina virtual, o si necesita capacidad de tooexpand, puede agregar un grupo de direcciones de back-end VM toohello con [agregar az red nic ip-config-grupo de direcciones](/cli/azure/network/nic/ip-config/address-pool#add).</span><span class="sxs-lookup"><span data-stu-id="eeb5c-207">After performing VM maintenance, or if you need tooexpand capacity, you can add a VM toohello backend address pool with [az network nic ip-config address-pool add](/cli/azure/network/nic/ip-config/address-pool#add).</span></span> <span data-ttu-id="eeb5c-208">Hello en el ejemplo siguiente se agrega Hola NIC virtual para **myVM2** demasiado*myLoadBalancer*:</span><span class="sxs-lookup"><span data-stu-id="eeb5c-208">hello following example adds hello virtual NIC for **myVM2** too*myLoadBalancer*:</span></span>

```azurecli-interactive 
az network nic ip-config address-pool add \
    --resource-group myResourceGroupLoadBalancer \
    --nic-name myNic2 \
    --ip-config-name ipConfig1 \
    --lb-name myLoadBalancer \
    --address-pool myBackEndPool
```


## <a name="next-steps"></a><span data-ttu-id="eeb5c-209">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="eeb5c-209">Next steps</span></span>
<span data-ttu-id="eeb5c-210">En este tutorial, ha creado un equilibrador de carga y adjunta tooit de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="eeb5c-210">In this tutorial, you created a load balancer and attached VMs tooit.</span></span> <span data-ttu-id="eeb5c-211">Ha aprendido a:</span><span class="sxs-lookup"><span data-stu-id="eeb5c-211">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="eeb5c-212">Creación de un equilibrador de carga de Azure</span><span class="sxs-lookup"><span data-stu-id="eeb5c-212">Create an Azure load balancer</span></span>
> * <span data-ttu-id="eeb5c-213">Creación del sondeo de estado de un equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="eeb5c-213">Create a load balancer health probe</span></span>
> * <span data-ttu-id="eeb5c-214">Crear reglas de tráfico del equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="eeb5c-214">Create load balancer traffic rules</span></span>
> * <span data-ttu-id="eeb5c-215">Usar en la nube init toocreate una aplicación básica de Node.js</span><span class="sxs-lookup"><span data-stu-id="eeb5c-215">Use cloud-init toocreate a basic Node.js app</span></span>
> * <span data-ttu-id="eeb5c-216">Crear máquinas virtuales y adjuntar tooa equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="eeb5c-216">Create virtual machines and attach tooa load balancer</span></span>
> * <span data-ttu-id="eeb5c-217">Ver un equilibrador de carga en acción</span><span class="sxs-lookup"><span data-stu-id="eeb5c-217">View a load balancer in action</span></span>
> * <span data-ttu-id="eeb5c-218">Agregar y quitar las máquinas virtuales de un equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="eeb5c-218">Add and remove VMs from a load balancer</span></span>

<span data-ttu-id="eeb5c-219">Avanzar toohello siguiente tutorial toolearn más información acerca de los componentes de red virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="eeb5c-219">Advance toohello next tutorial toolearn more about Azure virtual network components.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="eeb5c-220">Administración de máquinas y redes virtuales</span><span class="sxs-lookup"><span data-stu-id="eeb5c-220">Manage VMs and virtual networks</span></span>](tutorial-virtual-network.md)
