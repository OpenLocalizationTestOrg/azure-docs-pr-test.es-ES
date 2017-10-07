---
title: aaaOpen puertos tooa Linux VM con Azure CLI 2.0 | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooopen un puerto o cree una VM de Linux tooyour de punto de conexión mediante la implementación del Administrador de recursos de Azure Hola modelar y Hola 2.0 de CLI de Azure"
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
ms.openlocfilehash: c79b31206e97558171609cf033bb3cb3370777c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="open-ports-and-endpoints-tooa-linux-vm-with-hello-azure-cli"></a><span data-ttu-id="29120-103">Abrir puertos y los puntos de conexión tooa VM de Linux con hello CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="29120-103">Open ports and endpoints tooa Linux VM with hello Azure CLI</span></span>
<span data-ttu-id="29120-104">Abrir un puerto, o crear un punto de conexión, tooa máquina virtual (VM) de Azure mediante la creación de un filtro de red en una subred o una interfaz de red de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="29120-104">You open a port, or create an endpoint, tooa virtual machine (VM) in Azure by creating a network filter on a subnet or VM network interface.</span></span> <span data-ttu-id="29120-105">Estos filtros, que controlan el tráfico entrante y saliente, se coloca en un recurso de grupo de seguridad de red conectado toohello que recibe el tráfico de Hola.</span><span class="sxs-lookup"><span data-stu-id="29120-105">You place these filters, which control both inbound and outbound traffic, on a Network Security Group attached toohello resource that receives hello traffic.</span></span> <span data-ttu-id="29120-106">Vamos a usar un ejemplo común de tráfico web en el puerto 80.</span><span class="sxs-lookup"><span data-stu-id="29120-106">Let's use a common example of web traffic on port 80.</span></span> <span data-ttu-id="29120-107">Este artículo muestra cómo tooopen una tooa de puerto virtual con hello 2.0 de CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="29120-107">This article shows you how tooopen a port tooa VM with hello Azure CLI 2.0.</span></span> <span data-ttu-id="29120-108">También puede realizar estos pasos con hello [Azure CLI 1.0](nsg-quickstart-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="29120-108">You can also perform these steps with hello [Azure CLI 1.0](nsg-quickstart-nodejs.md).</span></span>


## <a name="quick-commands"></a><span data-ttu-id="29120-109">Comandos rápidos</span><span class="sxs-lookup"><span data-stu-id="29120-109">Quick commands</span></span>
<span data-ttu-id="29120-110">Grupo de seguridad de red de toocreate y reglas que necesita más reciente Hola [CLI de Azure 2.0](/cli/azure/install-az-cli2) instalado y registrado en tooan cuenta de Azure mediante [inicio de sesión de az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="29120-110">toocreate a Network Security Group and rules you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="29120-111">En hello en los ejemplos siguientes, reemplace los nombres de parámetros de ejemplo con sus propios valores.</span><span class="sxs-lookup"><span data-stu-id="29120-111">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="29120-112">Los nombres de parámetro de ejemplo incluyen *myResourceGroup*, *myNetworkSecurityGroup* y *myVnet*.</span><span class="sxs-lookup"><span data-stu-id="29120-112">Example parameter names include *myResourceGroup*, *myNetworkSecurityGroup*, and *myVnet*.</span></span>

<span data-ttu-id="29120-113">Crear grupo de seguridad de red de hello con [crear az red nsg](/cli/azure/network/nsg#create).</span><span class="sxs-lookup"><span data-stu-id="29120-113">Create hello network security group with [az network nsg create](/cli/azure/network/nsg#create).</span></span> <span data-ttu-id="29120-114">Hello en el ejemplo siguiente se crea un grupo de seguridad de red denominado *myNetworkSecurityGroup* en hello *eastus* ubicación:</span><span class="sxs-lookup"><span data-stu-id="29120-114">hello following example creates a network security group named *myNetworkSecurityGroup* in hello *eastus* location:</span></span>

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

<span data-ttu-id="29120-115">Agregar una regla con [crear regla de nsg de red az](/cli/azure/network/nsg/rule#create) tooallow HTTP tráfico tooyour webserver (o ajustar para su propia situación, como conectividad de acceso o de base de datos SSH).</span><span class="sxs-lookup"><span data-stu-id="29120-115">Add a rule with [az network nsg rule create](/cli/azure/network/nsg/rule#create) tooallow HTTP traffic tooyour webserver (or adjust for your own scenario, such as SSH access or database connectivity).</span></span> <span data-ttu-id="29120-116">Hello en el ejemplo siguiente se crea una regla denominada *myNetworkSecurityGroupRule* tooallow TCP de tráfico en el puerto 80:</span><span class="sxs-lookup"><span data-stu-id="29120-116">hello following example creates a rule named *myNetworkSecurityGroupRule* tooallow TCP traffic on port 80:</span></span>

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --protocol tcp \
    --priority 1000 \
    --destination-port-range 80
```

<span data-ttu-id="29120-117">Asociar Hola grupo de seguridad de red con la interfaz de red de la máquina virtual (NIC) a [actualizar la nic de red az](/cli/azure/network/nic#update).</span><span class="sxs-lookup"><span data-stu-id="29120-117">Associate hello Network Security Group with your VM's network interface (NIC) with [az network nic update](/cli/azure/network/nic#update).</span></span> <span data-ttu-id="29120-118">Hello en el ejemplo siguiente se asocia un NIC existente denominado *myNic* con grupo de seguridad de red denominado hello *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="29120-118">hello following example associates an existing NIC named *myNic* with hello Network Security Group named *myNetworkSecurityGroup*:</span></span>

```azurecli
az network nic update \
    --resource-group myResourceGroup \
    --name myNic \
    --network-security-group myNetworkSecurityGroup
```

<span data-ttu-id="29120-119">Como alternativa, puede asociar el grupo de seguridad de red con una subred de red virtual con [actualización de subred de red virtual de red az](/cli/azure/network/vnet/subnet#update) en lugar de simplemente toohello interfaz de red en una sola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="29120-119">Alternatively, you can associate your Network Security Group with a virtual network subnet with [az network vnet subnet update](/cli/azure/network/vnet/subnet#update) rather than just toohello network interface on a single VM.</span></span> <span data-ttu-id="29120-120">Hello en el ejemplo siguiente se asocia una subred existente denominada *mySubnet* en hello *myVnet* red virtual con hello grupo de seguridad de red denominado *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="29120-120">hello following example associates an existing subnet named *mySubnet* in hello *myVnet* virtual network with hello Network Security Group named *myNetworkSecurityGroup*:</span></span>

```azurecli
az network vnet subnet update \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnet \
    --network-security-group myNetworkSecurityGroup
```

## <a name="more-information-on-network-security-groups"></a><span data-ttu-id="29120-121">Más información sobre los grupos de seguridad de red</span><span class="sxs-lookup"><span data-stu-id="29120-121">More information on Network Security Groups</span></span>
<span data-ttu-id="29120-122">Hola de comandos rápido aquí le permite tooget seguridad y en ejecución con tooyour del flujo de tráfico máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="29120-122">hello quick commands here allow you tooget up and running with traffic flowing tooyour VM.</span></span> <span data-ttu-id="29120-123">Grupos de seguridad de red proporcionan muchas características excepcionales y granularidad para controlar acceso a los recursos tooyour.</span><span class="sxs-lookup"><span data-stu-id="29120-123">Network Security Groups provide many great features and granularity for controlling access tooyour resources.</span></span> <span data-ttu-id="29120-124">Puede leer más sobre la [creación de un grupo de seguridad de red y las reglas de ACL aquí](tutorial-virtual-network.md#secure-network-traffic).</span><span class="sxs-lookup"><span data-stu-id="29120-124">You can read more about [creating a Network Security Group and ACL rules here](tutorial-virtual-network.md#secure-network-traffic).</span></span>

<span data-ttu-id="29120-125">Para las aplicaciones web de alta disponibilidad, debe colocar las máquinas virtuales detrás de una instancia de Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="29120-125">For highly available web applications, you should place your VMs behind an Azure Load Balancer.</span></span> <span data-ttu-id="29120-126">equilibrador de carga de Hello distribuye el tráfico tooVMs, con un grupo de seguridad de red que proporciona filtrado de tráfico.</span><span class="sxs-lookup"><span data-stu-id="29120-126">hello load balancer distributes traffic tooVMs, with a Network Security Group that provides traffic filtering.</span></span> <span data-ttu-id="29120-127">Para obtener más información, consulte [cómo equilibrar tooload Linux virtual máquinas en Azure toocreate una aplicación de alta disponibilidad](tutorial-load-balancer.md).</span><span class="sxs-lookup"><span data-stu-id="29120-127">For more information, see [How tooload balance Linux virtual machines in Azure toocreate a highly available application](tutorial-load-balancer.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="29120-128">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="29120-128">Next steps</span></span>
<span data-ttu-id="29120-129">En este ejemplo, ha creado el tráfico de tooallow HTTP de una regla sencilla.</span><span class="sxs-lookup"><span data-stu-id="29120-129">In this example, you created a simple rule tooallow HTTP traffic.</span></span> <span data-ttu-id="29120-130">Puede encontrar información sobre cómo crear entornos más detallados en hello siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="29120-130">You can find information on creating more detailed environments in hello following articles:</span></span>

* [<span data-ttu-id="29120-131">Información general sobre Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="29120-131">Azure Resource Manager overview</span></span>](../../azure-resource-manager/resource-group-overview.md)
* [<span data-ttu-id="29120-132">¿Qué es un grupo de seguridad de red?</span><span class="sxs-lookup"><span data-stu-id="29120-132">What is a Network Security Group (NSG)?</span></span>](../../virtual-network/virtual-networks-nsg.md)
