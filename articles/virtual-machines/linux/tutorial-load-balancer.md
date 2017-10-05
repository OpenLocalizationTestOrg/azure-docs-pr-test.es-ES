---
title: "Equilibrio de la carga de máquinas virtuales Linux en Azure | Microsoft Docs"
description: "Aprenda a usar Azure Load Balancer para crear una aplicación segura y con alta disponibilidad en tres máquinas virtuales Linux."
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
ms.openlocfilehash: 7b3a089d2f6386afcc46cbc4377594be0d758fc6
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-load-balance-linux-virtual-machines-in-azure-to-create-a-highly-available-application"></a><span data-ttu-id="d7f94-103">Equilibrio de la carga de máquinas virtuales Linux en Azure para crear una aplicación de alta disponibilidad</span><span class="sxs-lookup"><span data-stu-id="d7f94-103">How to load balance Linux virtual machines in Azure to create a highly available application</span></span>
<span data-ttu-id="d7f94-104">El equilibrio de carga proporciona un mayor nivel de disponibilidad al distribuir las solicitudes entrantes entre varias máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="d7f94-104">Load balancing provides a higher level of availability by spreading incoming requests across multiple virtual machines.</span></span> <span data-ttu-id="d7f94-105">En este tutorial, aprenderá sobre los distintos componentes de Azure Load Balancer que distribuyen el tráfico y proporcionan una alta disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="d7f94-105">In this tutorial, you learn about the different components of the Azure load balancer that distribute traffic and provide high availability.</span></span> <span data-ttu-id="d7f94-106">Aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="d7f94-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d7f94-107">Creación de un equilibrador de carga de Azure</span><span class="sxs-lookup"><span data-stu-id="d7f94-107">Create an Azure load balancer</span></span>
> * <span data-ttu-id="d7f94-108">Creación del sondeo de estado de un equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="d7f94-108">Create a load balancer health probe</span></span>
> * <span data-ttu-id="d7f94-109">Crear reglas de tráfico del equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="d7f94-109">Create load balancer traffic rules</span></span>
> * <span data-ttu-id="d7f94-110">Usar cloud-init para crear una aplicación básica de Node.js</span><span class="sxs-lookup"><span data-stu-id="d7f94-110">Use cloud-init to create a basic Node.js app</span></span>
> * <span data-ttu-id="d7f94-111">Crear máquinas virtuales y conectarlas a un equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="d7f94-111">Create virtual machines and attach to a load balancer</span></span>
> * <span data-ttu-id="d7f94-112">Ver un equilibrador de carga en acción</span><span class="sxs-lookup"><span data-stu-id="d7f94-112">View a load balancer in action</span></span>
> * <span data-ttu-id="d7f94-113">Agregar y quitar las máquinas virtuales de un equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="d7f94-113">Add and remove VMs from a load balancer</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="d7f94-114">Si decide instalar y usar la CLI localmente, para este tutorial es preciso que ejecute la CLI de Azure versión 2.0.4 o posterior.</span><span class="sxs-lookup"><span data-stu-id="d7f94-114">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="d7f94-115">Ejecute `az --version` para encontrar la versión.</span><span class="sxs-lookup"><span data-stu-id="d7f94-115">Run `az --version` to find the version.</span></span> <span data-ttu-id="d7f94-116">Si necesita instalarla o actualizarla, consulte [Instalación de la CLI de Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="d7f94-116">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="azure-load-balancer-overview"></a><span data-ttu-id="d7f94-117">Información general sobre Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="d7f94-117">Azure load balancer overview</span></span>
<span data-ttu-id="d7f94-118">Un equilibrador de carga de Azure es un equilibrador de carga de nivel 4 (TCP, UDP) que proporciona una alta disponibilidad mediante la distribución del tráfico entrante entre máquinas virtuales con un estado correcto.</span><span class="sxs-lookup"><span data-stu-id="d7f94-118">An Azure load balancer is a Layer-4 (TCP, UDP) load balancer that provides high availability by distributing incoming traffic among healthy VMs.</span></span> <span data-ttu-id="d7f94-119">Un sondeo de estado de equilibrador de carga supervisa un puerto determinado en cada máquina virtual y solo distribuye tráfico a una máquina virtual operativa.</span><span class="sxs-lookup"><span data-stu-id="d7f94-119">A load balancer health probe monitors a given port on each VM and only distributes traffic to an operational VM.</span></span>

<span data-ttu-id="d7f94-120">Se define una configuración de IP de front-end que contiene una o varias direcciones IP públicas.</span><span class="sxs-lookup"><span data-stu-id="d7f94-120">You define a front-end IP configuration that contains one or more public IP addresses.</span></span> <span data-ttu-id="d7f94-121">Esta configuración de IP de front-end permite que el equilibrador de carga y las aplicaciones sean accesibles a través de Internet.</span><span class="sxs-lookup"><span data-stu-id="d7f94-121">This front-end IP configuration allows your load balancer and applications to be accessible over the Internet.</span></span> 

<span data-ttu-id="d7f94-122">Las máquinas virtuales se conectarán a un equilibrador de carga mediante su tarjeta de interfaz de red (NIC) virtual.</span><span class="sxs-lookup"><span data-stu-id="d7f94-122">Virtual machines connect to a load balancer using their virtual network interface card (NIC).</span></span> <span data-ttu-id="d7f94-123">Para distribuir el tráfico a las máquinas virtuales, un grupo de direcciones de back-end contiene las direcciones IP de las tarjetas de interfaz de red (NIC) virtual conectadas al equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="d7f94-123">To distribute traffic to the VMs, a back-end address pool contains the IP addresses of the virtual (NICs) connected to the load balancer.</span></span>

<span data-ttu-id="d7f94-124">Para controlar el flujo de tráfico, se definen reglas de equilibrador de carga para determinados puertos y protocolos que se asignan a las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="d7f94-124">To control the flow of traffic, you define load balancer rules for specific ports and protocols that map to your VMs.</span></span>

<span data-ttu-id="d7f94-125">Si siguió el tutorial anterior para [crear un conjunto de escalado de máquinas virtuales](tutorial-create-vmss.md), se creó un equilibrador de carga automáticamente.</span><span class="sxs-lookup"><span data-stu-id="d7f94-125">If you followed the previous tutorial to [create a virtual machine scale set](tutorial-create-vmss.md), a load balancer was created for you.</span></span> <span data-ttu-id="d7f94-126">Todos estos componentes se configuraron automáticamente como parte del conjunto de escalado.</span><span class="sxs-lookup"><span data-stu-id="d7f94-126">All these components were configured for you as part of the scale set.</span></span>


## <a name="create-azure-load-balancer"></a><span data-ttu-id="d7f94-127">Creación del equilibrador de carga de Azure</span><span class="sxs-lookup"><span data-stu-id="d7f94-127">Create Azure load balancer</span></span>
<span data-ttu-id="d7f94-128">En esta sección se detalla cómo se puede crear y configurar cada componente del equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="d7f94-128">This section details how you can create and configure each component of the load balancer.</span></span> <span data-ttu-id="d7f94-129">Antes de poder crear el equilibrador de carga, cree un grupo de recursos con [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="d7f94-129">Before you can create your load balancer, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="d7f94-130">En el ejemplo siguiente, se crea un grupo de recursos denominado *myResourceGroupLoadBalancer* en la ubicación *eastus*:</span><span class="sxs-lookup"><span data-stu-id="d7f94-130">The following example creates a resource group named *myResourceGroupLoadBalancer* in the *eastus* location:</span></span>

```azurecli-interactive 
az group create --name myResourceGroupLoadBalancer --location eastus
```

### <a name="create-a-public-ip-address"></a><span data-ttu-id="d7f94-131">Crear una dirección IP pública</span><span class="sxs-lookup"><span data-stu-id="d7f94-131">Create a public IP address</span></span>
<span data-ttu-id="d7f94-132">Para obtener acceso a la aplicación en Internet, necesita una dirección IP pública para el equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="d7f94-132">To access your app on the Internet, you need a public IP address for the load balancer.</span></span> <span data-ttu-id="d7f94-133">Cree una dirección IP pública con [az network public-ip create](/cli/azure/network/public-ip#create).</span><span class="sxs-lookup"><span data-stu-id="d7f94-133">Create a public IP address with [az network public-ip create](/cli/azure/network/public-ip#create).</span></span> <span data-ttu-id="d7f94-134">En el ejemplo siguiente se crea una dirección IP pública denominada *myPublicIP* en el grupo de recursos *myResourceGroupLoadBalancer*:</span><span class="sxs-lookup"><span data-stu-id="d7f94-134">The following example creates a public IP address named *myPublicIP* in the *myResourceGroupLoadBalancer* resource group:</span></span>

```azurecli-interactive 
az network public-ip create \
    --resource-group myResourceGroupLoadBalancer \
    --name myPublicIP
```

### <a name="create-a-load-balancer"></a><span data-ttu-id="d7f94-135">Crear un equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="d7f94-135">Create a load balancer</span></span>
<span data-ttu-id="d7f94-136">Cree un equilibrador de carga con [az network lb create](/cli/azure/network/lb#create).</span><span class="sxs-lookup"><span data-stu-id="d7f94-136">Create a load balancer with [az network lb create](/cli/azure/network/lb#create).</span></span> <span data-ttu-id="d7f94-137">En el ejemplo siguiente se crea un equilibrador de carga llamado *myLoadBalancer* y se asigna la dirección *myPublicIP* a la configuración de IP de front-end:</span><span class="sxs-lookup"><span data-stu-id="d7f94-137">The following example creates a load balancer named *myLoadBalancer* and assigns the *myPublicIP* address to the front-end IP configuration:</span></span>

```azurecli-interactive 
az network lb create \
    --resource-group myResourceGroupLoadBalancer \
    --name myLoadBalancer \
    --frontend-ip-name myFrontEndPool \
    --backend-pool-name myBackEndPool \
    --public-ip-address myPublicIP
```

### <a name="create-a-health-probe"></a><span data-ttu-id="d7f94-138">Creación de un sondeo de estado</span><span class="sxs-lookup"><span data-stu-id="d7f94-138">Create a health probe</span></span>
<span data-ttu-id="d7f94-139">Para permitir que el equilibrador de carga supervise el estado de la aplicación, utilice un sondeo de estado.</span><span class="sxs-lookup"><span data-stu-id="d7f94-139">To allow the load balancer to monitor the status of your app, you use a health probe.</span></span> <span data-ttu-id="d7f94-140">El sondeo de estado agrega o quita de forma dinámica las máquinas virtuales de la rotación del equilibrador de carga en base a su respuesta a las comprobaciones de estado.</span><span class="sxs-lookup"><span data-stu-id="d7f94-140">The health probe dynamically adds or removes VMs from the load balancer rotation based on their response to health checks.</span></span> <span data-ttu-id="d7f94-141">De forma predeterminada, una máquina virtual se quita de la distribución del equilibrador de carga después de dos errores consecutivos en un intervalo de 15 segundos.</span><span class="sxs-lookup"><span data-stu-id="d7f94-141">By default, a VM is removed from the load balancer distribution after two consecutive failures at 15-second intervals.</span></span> <span data-ttu-id="d7f94-142">Cree un sondeo de estado en función de un protocolo o una página de comprobación de mantenimiento específica para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d7f94-142">You create a health probe based on a protocol or a specific health check page for your app.</span></span> 

<span data-ttu-id="d7f94-143">En el ejemplo siguiente se crea un sondeo de TCP.</span><span class="sxs-lookup"><span data-stu-id="d7f94-143">The following example creates a TCP probe.</span></span> <span data-ttu-id="d7f94-144">También se pueden crear sondeos HTTP personalizados para comprobaciones de estado más específicas.</span><span class="sxs-lookup"><span data-stu-id="d7f94-144">You can also create custom HTTP probes for more fine grained health checks.</span></span> <span data-ttu-id="d7f94-145">Al usar un sondeo HTTP personalizado, debe crear la página de comprobación de estado, por ejemplo *healthcheck.js*.</span><span class="sxs-lookup"><span data-stu-id="d7f94-145">When using a custom HTTP probe, you must create the health check page, such as *healthcheck.js*.</span></span> <span data-ttu-id="d7f94-146">El sondeo debe devolver una respuesta **HTTP 200 OK** para que el equilibrador de carga mantenga el host en rotación.</span><span class="sxs-lookup"><span data-stu-id="d7f94-146">The probe must return an **HTTP 200 OK** response for the load balancer to keep the host in rotation.</span></span>

<span data-ttu-id="d7f94-147">Para crear un sondeo de estado TCP, debe usar el comando [az network lb probe create](/cli/azure/network/lb/probe#create).</span><span class="sxs-lookup"><span data-stu-id="d7f94-147">To create a TCP health probe, you use [az network lb probe create](/cli/azure/network/lb/probe#create).</span></span> <span data-ttu-id="d7f94-148">En el ejemplo siguiente se crea un sondeo de TCP denominado *myHealthProbe*:</span><span class="sxs-lookup"><span data-stu-id="d7f94-148">The following example creates a health probe named *myHealthProbe*:</span></span>

```azurecli-interactive 
az network lb probe create \
    --resource-group myResourceGroupLoadBalancer \
    --lb-name myLoadBalancer \
    --name myHealthProbe \
    --protocol tcp \
    --port 80
```

### <a name="create-a-load-balancer-rule"></a><span data-ttu-id="d7f94-149">Creación de una regla de equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="d7f94-149">Create a load balancer rule</span></span>
<span data-ttu-id="d7f94-150">Las reglas de equilibrador de carga se utilizan para definir cómo se distribuye el tráfico a las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="d7f94-150">A load balancer rule is used to define how traffic is distributed to the VMs.</span></span> <span data-ttu-id="d7f94-151">Se define la configuración de IP front-end para el tráfico entrante y el grupo IP de back-end para recibir el tráfico, junto con el puerto de origen y destino requeridos.</span><span class="sxs-lookup"><span data-stu-id="d7f94-151">You define the front-end IP configuration for the incoming traffic and the back-end IP pool to receive the traffic, along with the required source and destination port.</span></span> <span data-ttu-id="d7f94-152">Para asegurarse de que solo las máquinas virtuales correctas reciban tráfico, también hay que definir el sondeo de estado que se va usar.</span><span class="sxs-lookup"><span data-stu-id="d7f94-152">To make sure only healthy VMs receive traffic, you also define the health probe to use.</span></span>

<span data-ttu-id="d7f94-153">Cree una regla de equilibrador de carga con [az network lb rule create](/cli/azure/network/lb/rule#create).</span><span class="sxs-lookup"><span data-stu-id="d7f94-153">Create a load balancer rule with [az network lb rule create](/cli/azure/network/lb/rule#create).</span></span> <span data-ttu-id="d7f94-154">En el ejemplo siguiente se crea una regla denominada *myLoadBalancerRule*, se usa el sondeo de estado *myHealthProbe* y se equilibra el tráfico en el puerto *80*:</span><span class="sxs-lookup"><span data-stu-id="d7f94-154">The following example creates a rule named *myLoadBalancerRule*, uses the *myHealthProbe* health probe, and balances traffic on port *80*:</span></span>

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


## <a name="configure-virtual-network"></a><span data-ttu-id="d7f94-155">Configuración de una red virtual</span><span class="sxs-lookup"><span data-stu-id="d7f94-155">Configure virtual network</span></span>
<span data-ttu-id="d7f94-156">Antes de implementar algunas máquinas virtuales y poder probar el equilibrador, cree los recursos de red virtual auxiliares.</span><span class="sxs-lookup"><span data-stu-id="d7f94-156">Before you deploy some VMs and can test your balancer, create the supporting virtual network resources.</span></span> <span data-ttu-id="d7f94-157">Para más información sobre las redes virtuales, consulte el tutorial [Administración de Azure Virtual Networks](tutorial-virtual-network.md).</span><span class="sxs-lookup"><span data-stu-id="d7f94-157">For more information about virtual networks, see the [Manage Azure Virtual Networks](tutorial-virtual-network.md) tutorial.</span></span>

### <a name="create-network-resources"></a><span data-ttu-id="d7f94-158">Crear recursos de red</span><span class="sxs-lookup"><span data-stu-id="d7f94-158">Create network resources</span></span>
<span data-ttu-id="d7f94-159">Cree la red virtual con el comando [az network vnet create](/cli/azure/network/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="d7f94-159">Create a virtual network with [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="d7f94-160">En el ejemplo siguiente se crea una red virtual denominada *myVnet* con una subred *mySubnet*:</span><span class="sxs-lookup"><span data-stu-id="d7f94-160">The following example creates a virtual network named *myVnet* with a subnet named *mySubnet*:</span></span>

```azurecli-interactive 
az network vnet create \
    --resource-group myResourceGroupLoadBalancer \
    --name myVnet \
    --subnet-name mySubnet
```

<span data-ttu-id="d7f94-161">Para agregar un grupo de seguridad de red, use el comando [az network nsg create](/cli/azure/network/nsg#create).</span><span class="sxs-lookup"><span data-stu-id="d7f94-161">To add a network security group, you use [az network nsg create](/cli/azure/network/nsg#create).</span></span> <span data-ttu-id="d7f94-162">En el ejemplo siguiente se crea un grupo de seguridad de red denominado *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="d7f94-162">The following example creates a network security group named *myNetworkSecurityGroup*:</span></span>

```azurecli-interactive 
az network nsg create \
    --resource-group myResourceGroupLoadBalancer \
    --name myNetworkSecurityGroup
```

<span data-ttu-id="d7f94-163">Cree una regla de grupo de seguridad de red con el comando [az network nsg rule create](/cli/azure/network/nsg/rule#create).</span><span class="sxs-lookup"><span data-stu-id="d7f94-163">Create a network security group rule with [az network nsg rule create](/cli/azure/network/nsg/rule#create).</span></span> <span data-ttu-id="d7f94-164">En el ejemplo siguiente se crea una regla grupo de seguridad de red denominada *myNetworkSecurityGroupRule*:</span><span class="sxs-lookup"><span data-stu-id="d7f94-164">The following example creates a network security group rule named *myNetworkSecurityGroupRule*:</span></span>

```azurecli-interactive 
az network nsg rule create \
    --resource-group myResourceGroupLoadBalancer \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --priority 1001 \
    --protocol tcp \
    --destination-port-range 80
```

<span data-ttu-id="d7f94-165">Las NIC virtuales se crean con el comando [az network nic create](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="d7f94-165">Virtual NICs are created with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="d7f94-166">En el ejemplo siguiente se crean tres NIC.</span><span class="sxs-lookup"><span data-stu-id="d7f94-166">The following example creates three virtual NICs.</span></span> <span data-ttu-id="d7f94-167">(Una NIC virtual para cada máquina virtual que cree para la aplicación en los pasos siguientes).</span><span class="sxs-lookup"><span data-stu-id="d7f94-167">(One virtual NIC for each VM you create for your app in the following steps).</span></span> <span data-ttu-id="d7f94-168">Puede crear NIC virtuales y máquinas virtuales adicionales en cualquier momento y agregarlas al equilibrador de carga:</span><span class="sxs-lookup"><span data-stu-id="d7f94-168">You can create additional virtual NICs and VMs at any time and add them to the load balancer:</span></span>

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

## <a name="create-virtual-machines"></a><span data-ttu-id="d7f94-169">Creación de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="d7f94-169">Create virtual machines</span></span>

### <a name="create-cloud-init-config"></a><span data-ttu-id="d7f94-170">Creación de cloud-init config</span><span class="sxs-lookup"><span data-stu-id="d7f94-170">Create cloud-init config</span></span>
<span data-ttu-id="d7f94-171">En un tutorial anterior sobre [cómo personalizar una máquina virtual Linux en el primer arranque](tutorial-automate-vm-deployment.md), aprendió a automatizar la personalización de máquinas virtuales con cloud-init.</span><span class="sxs-lookup"><span data-stu-id="d7f94-171">In a previous tutorial on [How to customize a Linux virtual machine on first boot](tutorial-automate-vm-deployment.md), you learned how to automate VM customization with cloud-init.</span></span> <span data-ttu-id="d7f94-172">Pues bien, el mismo archivo de configuración cloud-init puede usarlo para instalar NGINX y ejecutar una aplicación sencilla Node.js "Hello World".</span><span class="sxs-lookup"><span data-stu-id="d7f94-172">You can use the same cloud-init configuration file to install NGINX and run a simple 'Hello World' Node.js app.</span></span>

<span data-ttu-id="d7f94-173">En el shell actual, cree un archivo denominado "*cloud-init.txt*" y pegue la siguiente configuración.</span><span class="sxs-lookup"><span data-stu-id="d7f94-173">In your current shell, create a file named *cloud-init.txt* and paste the following configuration.</span></span> <span data-ttu-id="d7f94-174">Por ejemplo, cree el archivo en Cloud Shell, no en la máquina local.</span><span class="sxs-lookup"><span data-stu-id="d7f94-174">For example, create the file in the Cloud Shell not on your local machine.</span></span> <span data-ttu-id="d7f94-175">Escriba `sensible-editor cloud-init.txt` para crear el archivo y ver una lista de editores disponibles.</span><span class="sxs-lookup"><span data-stu-id="d7f94-175">Enter `sensible-editor cloud-init.txt` to create the file and see a list of available editors.</span></span> <span data-ttu-id="d7f94-176">Asegúrese de que todo el archivo cloud-init se copia correctamente, especialmente la primera línea:</span><span class="sxs-lookup"><span data-stu-id="d7f94-176">Make sure that the whole cloud-init file is copied correctly, especially the first line:</span></span>

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

### <a name="create-virtual-machines"></a><span data-ttu-id="d7f94-177">Creación de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="d7f94-177">Create virtual machines</span></span>
<span data-ttu-id="d7f94-178">Para mejorar la alta disponibilidad de la aplicación, coloque las máquinas virtuales en un conjunto de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="d7f94-178">To improve the high availability of your app, place your VMs in an availability set.</span></span> <span data-ttu-id="d7f94-179">Para más información sobre los conjuntos de disponibilidad, consulte el tutorial anterior [Creación de máquinas virtuales de alta disponibilidad](tutorial-availability-sets.md).</span><span class="sxs-lookup"><span data-stu-id="d7f94-179">For more information about availability sets, see the previous [How to create highly available virtual machines](tutorial-availability-sets.md) tutorial.</span></span>

<span data-ttu-id="d7f94-180">Cree el conjunto de disponibilidad con [az vm availability-set create](/cli/azure/vm/availability-set#create).</span><span class="sxs-lookup"><span data-stu-id="d7f94-180">Create an availability set with [az vm availability-set create](/cli/azure/vm/availability-set#create).</span></span> <span data-ttu-id="d7f94-181">En el ejemplo siguiente se crea un conjunto de disponibilidad denominado *myAvailabilitySet*:</span><span class="sxs-lookup"><span data-stu-id="d7f94-181">The following example creates an availability set named *myAvailabilitySet*:</span></span>

```azurecli-interactive 
az vm availability-set create \
    --resource-group myResourceGroupLoadBalancer \
    --name myAvailabilitySet
```

<span data-ttu-id="d7f94-182">Ahora puede crear las máquinas virtuales con el comando [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="d7f94-182">Now you can create the VMs with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="d7f94-183">El siguiente ejemplo crea tres máquinas virtuales y genera claves SSH si aún no existen:</span><span class="sxs-lookup"><span data-stu-id="d7f94-183">The following example creates three VMs and generates SSH keys if they do not already exist:</span></span>

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

<span data-ttu-id="d7f94-184">Hay tareas en segundo plano que continúan ejecutándose después de que la CLI de Azure vuelve a abrir el símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="d7f94-184">There are background tasks that continue to run after the Azure CLI returns you to the prompt.</span></span> <span data-ttu-id="d7f94-185">El parámetro `--no-wait` no espera a que se completen todas las tareas.</span><span class="sxs-lookup"><span data-stu-id="d7f94-185">The `--no-wait` parameter does not wait for all the tasks to complete.</span></span> <span data-ttu-id="d7f94-186">Es posible que tenga que esperar otros dos minutos antes de poder acceder a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d7f94-186">It may be another couple of minutes before you can access the app.</span></span> <span data-ttu-id="d7f94-187">El sondeo de estado del equilibrador de carga detecta automáticamente cuándo la aplicación se está ejecutando en cada máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="d7f94-187">The load balancer health probe automatically detects when the app is running on each VM.</span></span> <span data-ttu-id="d7f94-188">Una vez que la aplicación se esté ejecutando, la regla del equilibrador de carga empieza a distribuir el tráfico.</span><span class="sxs-lookup"><span data-stu-id="d7f94-188">Once the app is running, the load balancer rule starts to distribute traffic.</span></span>


## <a name="test-load-balancer"></a><span data-ttu-id="d7f94-189">Prueba del equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="d7f94-189">Test load balancer</span></span>
<span data-ttu-id="d7f94-190">Obtenga la dirección IP pública del equilibrador de carga con [az network public-ip show](/cli/azure/network/public-ip#show).</span><span class="sxs-lookup"><span data-stu-id="d7f94-190">Obtain the public IP address of your load balancer with [az network public-ip show](/cli/azure/network/public-ip#show).</span></span> <span data-ttu-id="d7f94-191">En el ejemplo siguiente se obtiene la dirección IP de *myPublicIP* que se ha creado anteriormente:</span><span class="sxs-lookup"><span data-stu-id="d7f94-191">The following example obtains the IP address for *myPublicIP* created earlier:</span></span>

```azurecli-interactive 
az network public-ip show \
    --resource-group myResourceGroupLoadBalancer \
    --name myPublicIP \
    --query [ipAddress] \
    --output tsv
```

<span data-ttu-id="d7f94-192">A continuación, puede escribir la dirección IP pública en un explorador web.</span><span class="sxs-lookup"><span data-stu-id="d7f94-192">You can then enter the public IP address in to a web browser.</span></span> <span data-ttu-id="d7f94-193">Recuerde que tendrán que pasar unos minutos para que las máquinas virtuales estén listas antes de que el equilibrador de carga comience a distribuir el tráfico a ellas.</span><span class="sxs-lookup"><span data-stu-id="d7f94-193">Remember - it takes a few minutes the the VMs to be ready before the load balancer starts to distribute traffic to them.</span></span> <span data-ttu-id="d7f94-194">Se muestra la aplicación, incluido el nombre de host de la máquina virtual a la que el equilibrador de carga distribuye el tráfico como en el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="d7f94-194">The app is displayed, including the hostname of the VM that the load balancer distributed traffic to as in the following example:</span></span>

![Ejecución de la aplicación Node.js](./media/tutorial-load-balancer/running-nodejs-app.png)

<span data-ttu-id="d7f94-196">Para ver cómo el equilibrador de carga distribuye el tráfico entre las tres máquinas virtuales que ejecutan la aplicación, puede realizar una actualización forzada del explorador web.</span><span class="sxs-lookup"><span data-stu-id="d7f94-196">To see the load balancer distribute traffic across all three VMs running your app, you can force-refresh your web browser.</span></span>


## <a name="add-and-remove-vms"></a><span data-ttu-id="d7f94-197">Agregar y quitar máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="d7f94-197">Add and remove VMs</span></span>
<span data-ttu-id="d7f94-198">Puede que tenga que realizar labores de mantenimiento de las máquinas virtuales que ejecutan la aplicación, como la instalación de actualizaciones del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="d7f94-198">You may need to perform maintenance on the VMs running your app, such as installing OS updates.</span></span> <span data-ttu-id="d7f94-199">Para gestionar un aumento de tráfico a la aplicación, tiene que agregar más máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="d7f94-199">To deal with increased traffic to your app, you may need to add additional VMs.</span></span> <span data-ttu-id="d7f94-200">Esta sección le muestra cómo quitar o agregar una máquina virtual desde el equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="d7f94-200">This section shows you how to remove or add a VM from the load balancer.</span></span>

### <a name="remove-a-vm-from-the-load-balancer"></a><span data-ttu-id="d7f94-201">Eliminación de una máquina virtual del equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="d7f94-201">Remove a VM from the load balancer</span></span>
<span data-ttu-id="d7f94-202">Puede quitar una máquina virtual del grupo de direcciones de back-end con el comando [az network nic ip-config address-pool remove](/cli/azure/network/nic/ip-config/address-pool#remove).</span><span class="sxs-lookup"><span data-stu-id="d7f94-202">You can remove a VM from the backend address pool with [az network nic ip-config address-pool remove](/cli/azure/network/nic/ip-config/address-pool#remove).</span></span> <span data-ttu-id="d7f94-203">En el ejemplo siguiente se quita la NIC virtual para **myVM2** de *myLoadBalancer*:</span><span class="sxs-lookup"><span data-stu-id="d7f94-203">The following example removes the virtual NIC for **myVM2** from *myLoadBalancer*:</span></span>

```azurecli-interactive 
az network nic ip-config address-pool remove \
    --resource-group myResourceGroupLoadBalancer \
    --nic-name myNic2 \
    --ip-config-name ipConfig1 \
    --lb-name myLoadBalancer \
    --address-pool myBackEndPool 
```

<span data-ttu-id="d7f94-204">Para ver cómo el equilibrador de carga distribuye el tráfico entre las dos máquinas virtuales que quedan que ejecutan la aplicación, puede realizar una actualización forzada del explorador web.</span><span class="sxs-lookup"><span data-stu-id="d7f94-204">To see the load balancer distribute traffic across the remaining two VMs running your app you can force-refresh your web browser.</span></span> <span data-ttu-id="d7f94-205">Ahora puede realizar tareas de mantenimiento en la máquina virtual, como instalar actualizaciones del sistema operativo o realizar un reinicio de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="d7f94-205">You can now perform maintenance on the VM, such as installing OS updates or performing a VM reboot.</span></span>

### <a name="add-a-vm-to-the-load-balancer"></a><span data-ttu-id="d7f94-206">Incorporación de una máquina virtual al equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="d7f94-206">Add a VM to the load balancer</span></span>
<span data-ttu-id="d7f94-207">Después de realizar el mantenimiento en una máquina virtual, o si necesita expandir la capacidad, puede agregar una máquina virtual al grupo de direcciones de back-end con el comando [az network nic ip-config address-pool add](/cli/azure/network/nic/ip-config/address-pool#add).</span><span class="sxs-lookup"><span data-stu-id="d7f94-207">After performing VM maintenance, or if you need to expand capacity, you can add a VM to the backend address pool with [az network nic ip-config address-pool add](/cli/azure/network/nic/ip-config/address-pool#add).</span></span> <span data-ttu-id="d7f94-208">En el ejemplo siguiente se agrega la NIC virtual para **myVM2** a *myLoadBalancer*:</span><span class="sxs-lookup"><span data-stu-id="d7f94-208">The following example adds the virtual NIC for **myVM2** to *myLoadBalancer*:</span></span>

```azurecli-interactive 
az network nic ip-config address-pool add \
    --resource-group myResourceGroupLoadBalancer \
    --nic-name myNic2 \
    --ip-config-name ipConfig1 \
    --lb-name myLoadBalancer \
    --address-pool myBackEndPool
```


## <a name="next-steps"></a><span data-ttu-id="d7f94-209">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d7f94-209">Next steps</span></span>
<span data-ttu-id="d7f94-210">En este tutorial, ha creado un equilibrador de carga y conectó máquinas virtuales a él.</span><span class="sxs-lookup"><span data-stu-id="d7f94-210">In this tutorial, you created a load balancer and attached VMs to it.</span></span> <span data-ttu-id="d7f94-211">Ha aprendido a:</span><span class="sxs-lookup"><span data-stu-id="d7f94-211">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d7f94-212">Creación de un equilibrador de carga de Azure</span><span class="sxs-lookup"><span data-stu-id="d7f94-212">Create an Azure load balancer</span></span>
> * <span data-ttu-id="d7f94-213">Creación del sondeo de estado de un equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="d7f94-213">Create a load balancer health probe</span></span>
> * <span data-ttu-id="d7f94-214">Crear reglas de tráfico del equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="d7f94-214">Create load balancer traffic rules</span></span>
> * <span data-ttu-id="d7f94-215">Usar cloud-init para crear una aplicación básica de Node.js</span><span class="sxs-lookup"><span data-stu-id="d7f94-215">Use cloud-init to create a basic Node.js app</span></span>
> * <span data-ttu-id="d7f94-216">Crear máquinas virtuales y conectarlas a un equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="d7f94-216">Create virtual machines and attach to a load balancer</span></span>
> * <span data-ttu-id="d7f94-217">Ver un equilibrador de carga en acción</span><span class="sxs-lookup"><span data-stu-id="d7f94-217">View a load balancer in action</span></span>
> * <span data-ttu-id="d7f94-218">Agregar y quitar las máquinas virtuales de un equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="d7f94-218">Add and remove VMs from a load balancer</span></span>

<span data-ttu-id="d7f94-219">Prosiga con el siguiente tutorial para aprender más sobre los componentes de red virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="d7f94-219">Advance to the next tutorial to learn more about Azure virtual network components.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d7f94-220">Administración de máquinas y redes virtuales</span><span class="sxs-lookup"><span data-stu-id="d7f94-220">Manage VMs and virtual networks</span></span>](tutorial-virtual-network.md)
