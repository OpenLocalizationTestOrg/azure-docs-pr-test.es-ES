---
title: "Apertura de puertos para una máquina virtual Linux con la CLI de Azure 2.0 | Microsoft Docs"
description: "Más información sobre cómo abrir un puerto o crear un punto de conexión a la máquina virtual Linux mediante el modelo de implementación de Azure Resource Manager y la CLI de Azure 2.0"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: eef9842b-495a-46cf-99a6-74e49807e74e
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 08/21/2017
ms.author: iainfou
ms.openlocfilehash: d176187fe465264b5f433260de5178b48ca9dd4a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="open-ports-and-endpoints-to-a-linux-vm-with-the-azure-cli"></a><span data-ttu-id="01e64-103">Abrir puertos y puntos de conexión para una máquina virtual de Linux con la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="01e64-103">Open ports and endpoints to a Linux VM with the Azure CLI</span></span>
<span data-ttu-id="01e64-104">En Azure, se abre un puerto o se crea un punto de conexión a una máquina virtual creando un filtro de red en una subred o una interfaz de red de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="01e64-104">You open a port, or create an endpoint, to a virtual machine (VM) in Azure by creating a network filter on a subnet or VM network interface.</span></span> <span data-ttu-id="01e64-105">Estos filtros, que controlan el tráfico entrante y saliente, se colocan en un grupo de seguridad de red y se asocian al recurso que va a recibir dicho tráfico.</span><span class="sxs-lookup"><span data-stu-id="01e64-105">You place these filters, which control both inbound and outbound traffic, on a Network Security Group attached to the resource that receives the traffic.</span></span> <span data-ttu-id="01e64-106">Vamos a usar un ejemplo común de tráfico web en el puerto 80.</span><span class="sxs-lookup"><span data-stu-id="01e64-106">Let's use a common example of web traffic on port 80.</span></span> <span data-ttu-id="01e64-107">Este artículo muestra cómo abrir un puerto a una máquina virtual mediante la CLI de Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="01e64-107">This article shows you how to open a port to a VM with the Azure CLI 2.0.</span></span> <span data-ttu-id="01e64-108">También puede llevar a cabo estos pasos con la [CLI de Azure 1.0](nsg-quickstart-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="01e64-108">You can also perform these steps with the [Azure CLI 1.0](nsg-quickstart-nodejs.md).</span></span>


## <a name="quick-commands"></a><span data-ttu-id="01e64-109">Comandos rápidos</span><span class="sxs-lookup"><span data-stu-id="01e64-109">Quick commands</span></span>
<span data-ttu-id="01e64-110">Para crear reglas y un grupo de seguridad de red, necesita la [CLI de Azure 2.0](/cli/azure/install-az-cli2) más reciente instalada y con la sesión iniciada en una cuenta de Azure mediante [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="01e64-110">To create a Network Security Group and rules you need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="01e64-111">En los ejemplos siguientes, reemplace los nombres de parámetros de ejemplo por los suyos propios.</span><span class="sxs-lookup"><span data-stu-id="01e64-111">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="01e64-112">Los nombres de parámetro de ejemplo incluyen *myResourceGroup*, *myNetworkSecurityGroup* y *myVnet*.</span><span class="sxs-lookup"><span data-stu-id="01e64-112">Example parameter names include *myResourceGroup*, *myNetworkSecurityGroup*, and *myVnet*.</span></span>

<span data-ttu-id="01e64-113">Cree el grupo de seguridad de red con [az network nsg create](/cli/azure/network/nsg#create).</span><span class="sxs-lookup"><span data-stu-id="01e64-113">Create the network security group with [az network nsg create](/cli/azure/network/nsg#create).</span></span> <span data-ttu-id="01e64-114">En el ejemplo siguiente se crea un grupo de seguridad de red denominado *myNetworkSecurityGroup* en la ubicación *eastus*:</span><span class="sxs-lookup"><span data-stu-id="01e64-114">The following example creates a network security group named *myNetworkSecurityGroup* in the *eastus* location:</span></span>

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

<span data-ttu-id="01e64-115">Agregue una regla con [az network nsg rule create](/cli/azure/network/nsg/rule#create) que permita el tráfico HTTP hacia el servidor web (o adáptela a su propio escenario, por ejemplo, el acceso de SSH o la conectividad de base de datos).</span><span class="sxs-lookup"><span data-stu-id="01e64-115">Add a rule with [az network nsg rule create](/cli/azure/network/nsg/rule#create) to allow HTTP traffic to your webserver (or adjust for your own scenario, such as SSH access or database connectivity).</span></span> <span data-ttu-id="01e64-116">En el ejemplo siguiente, se crea una regla denominada *myNetworkSecurityGroupRule* para permitir el tráfico TCP en el puerto 80:</span><span class="sxs-lookup"><span data-stu-id="01e64-116">The following example creates a rule named *myNetworkSecurityGroupRule* to allow TCP traffic on port 80:</span></span>

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --protocol tcp \
    --priority 1000 \
    --destination-port-range 80
```

<span data-ttu-id="01e64-117">Asocie el grupo de seguridad de red con la interfaz de red (NIC) de la máquina virtual con [az network nic update](/cli/azure/network/nic#update).</span><span class="sxs-lookup"><span data-stu-id="01e64-117">Associate the Network Security Group with your VM's network interface (NIC) with [az network nic update](/cli/azure/network/nic#update).</span></span> <span data-ttu-id="01e64-118">En el ejemplo siguiente, se asocia una NIC existente denominada *myNic* con el grupo de seguridad de red llamado*myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="01e64-118">The following example associates an existing NIC named *myNic* with the Network Security Group named *myNetworkSecurityGroup*:</span></span>

```azurecli
az network nic update \
    --resource-group myResourceGroup \
    --name myNic \
    --network-security-group myNetworkSecurityGroup
```

<span data-ttu-id="01e64-119">Como alternativa, puede asociar el grupo de seguridad de red a una subred de red virtual con [az network vnet subnet update](/cli/azure/network/vnet/subnet#update), en lugar de únicamente a la interfaz de red en una única máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="01e64-119">Alternatively, you can associate your Network Security Group with a virtual network subnet with [az network vnet subnet update](/cli/azure/network/vnet/subnet#update) rather than just to the network interface on a single VM.</span></span> <span data-ttu-id="01e64-120">En el ejemplo siguiente, se asocia una subred existente denominado *mySubnet* de la red virtual *myVnet* con el grupo de seguridad de red llamado *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="01e64-120">The following example associates an existing subnet named *mySubnet* in the *myVnet* virtual network with the Network Security Group named *myNetworkSecurityGroup*:</span></span>

```azurecli
az network vnet subnet update \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnet \
    --network-security-group myNetworkSecurityGroup
```

## <a name="more-information-on-network-security-groups"></a><span data-ttu-id="01e64-121">Más información sobre los grupos de seguridad de red</span><span class="sxs-lookup"><span data-stu-id="01e64-121">More information on Network Security Groups</span></span>
<span data-ttu-id="01e64-122">Los comandos rápidos que se describen aquí le permiten ponerse a trabajar con el flujo de tráfico a la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="01e64-122">The quick commands here allow you to get up and running with traffic flowing to your VM.</span></span> <span data-ttu-id="01e64-123">Los grupos de seguridad de red proporcionan muchas características excelentes y un gran nivel de detalle para controlar el acceso a sus recursos.</span><span class="sxs-lookup"><span data-stu-id="01e64-123">Network Security Groups provide many great features and granularity for controlling access to your resources.</span></span> <span data-ttu-id="01e64-124">Puede leer más sobre la [creación de un grupo de seguridad de red y las reglas de ACL aquí](tutorial-virtual-network.md#secure-network-traffic).</span><span class="sxs-lookup"><span data-stu-id="01e64-124">You can read more about [creating a Network Security Group and ACL rules here](tutorial-virtual-network.md#secure-network-traffic).</span></span>

<span data-ttu-id="01e64-125">Para las aplicaciones web de alta disponibilidad, debe colocar las máquinas virtuales detrás de una instancia de Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="01e64-125">For highly available web applications, you should place your VMs behind an Azure Load Balancer.</span></span> <span data-ttu-id="01e64-126">El equilibrador de carga distribuye el tráfico a las máquinas virtuales, con un grupo de seguridad de red que proporciona el filtrado del tráfico.</span><span class="sxs-lookup"><span data-stu-id="01e64-126">The load balancer distributes traffic to VMs, with a Network Security Group that provides traffic filtering.</span></span> <span data-ttu-id="01e64-127">Para más información, consulte [Equilibrio de la carga de máquinas virtuales Linux en Azure para crear una aplicación de alta disponibilidad](tutorial-load-balancer.md).</span><span class="sxs-lookup"><span data-stu-id="01e64-127">For more information, see [How to load balance Linux virtual machines in Azure to create a highly available application](tutorial-load-balancer.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="01e64-128">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="01e64-128">Next steps</span></span>
<span data-ttu-id="01e64-129">En este ejemplo, se ha creado una regla sencilla para permitir tráfico HTTP.</span><span class="sxs-lookup"><span data-stu-id="01e64-129">In this example, you created a simple rule to allow HTTP traffic.</span></span> <span data-ttu-id="01e64-130">Puede encontrar información sobre la creación de entornos más detallados en los siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="01e64-130">You can find information on creating more detailed environments in the following articles:</span></span>

* [<span data-ttu-id="01e64-131">Información general sobre Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="01e64-131">Azure Resource Manager overview</span></span>](../../azure-resource-manager/resource-group-overview.md)
* [<span data-ttu-id="01e64-132">¿Qué es un grupo de seguridad de red?</span><span class="sxs-lookup"><span data-stu-id="01e64-132">What is a Network Security Group (NSG)?</span></span>](../../virtual-network/virtual-networks-nsg.md)
