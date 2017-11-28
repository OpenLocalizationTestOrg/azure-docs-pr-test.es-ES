---
title: aaaOpen puertos tooa VM de Linux con 1.0 de CLI de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooopen un puerto o cree una VM de Linux tooyour de punto de conexión mediante la implementación del Administrador de recursos de Azure Hola modelar y Hola 1.0 de CLI de Azure"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 337c37d151f527b43d4852291159b2f70a00accc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="opening-ports-and-endpoints-tooa-linux-vm-in-azure-using-hello-azure-cli-10"></a><span data-ttu-id="86b0b-103">Abrir puertos y los puntos de conexión tooa VM de Linux en Azure mediante Hola 1.0 de CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="86b0b-103">Opening ports and endpoints tooa Linux VM in Azure using hello Azure CLI 1.0</span></span>
<span data-ttu-id="86b0b-104">Abrir un puerto, o crear un punto de conexión, tooa máquina virtual (VM) de Azure mediante la creación de un filtro de red en una subred o una interfaz de red de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="86b0b-104">You open a port, or create an endpoint, tooa virtual machine (VM) in Azure by creating a network filter on a subnet or VM network interface.</span></span> <span data-ttu-id="86b0b-105">Estos filtros, que controlan el tráfico entrante y saliente, se coloca en un recurso de grupo de seguridad de red conectado toohello que recibe el tráfico de Hola.</span><span class="sxs-lookup"><span data-stu-id="86b0b-105">You place these filters, which control both inbound and outbound traffic, on a Network Security Group attached toohello resource that receives hello traffic.</span></span> <span data-ttu-id="86b0b-106">Vamos a usar un ejemplo común de tráfico web en el puerto 80.</span><span class="sxs-lookup"><span data-stu-id="86b0b-106">Let's use a common example of web traffic on port 80.</span></span> <span data-ttu-id="86b0b-107">Este artículo muestra cómo tooopen un puerto tooa VM con Hola 1.0 de CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="86b0b-107">This article shows you how tooopen a port tooa VM using hello Azure CLI 1.0.</span></span>


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="86b0b-108">Tarea CLI versiones toocomplete hello</span><span class="sxs-lookup"><span data-stu-id="86b0b-108">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="86b0b-109">Puede completar la tarea hello mediante uno de hello después de las versiones CLI:</span><span class="sxs-lookup"><span data-stu-id="86b0b-109">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="86b0b-110">[Azure 1.0 de CLI](#quick-commands) – nuestro CLI para hello clásico y recursos administración modelos de implementación (en este artículo)</span><span class="sxs-lookup"><span data-stu-id="86b0b-110">[Azure CLI 1.0](#quick-commands) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="86b0b-111">[Azure 2.0 CLI](nsg-quickstart.md) -nuestro CLI de próxima generación para el modelo de implementación de administración de recursos de Hola</span><span class="sxs-lookup"><span data-stu-id="86b0b-111">[Azure CLI 2.0](nsg-quickstart.md) - our next generation CLI for hello resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="86b0b-112">Comandos rápidos</span><span class="sxs-lookup"><span data-stu-id="86b0b-112">Quick commands</span></span>
<span data-ttu-id="86b0b-113">toocreate un grupo de seguridad de red y las reglas que necesita [hello Azure CLI 1.0](../../cli-install-nodejs.md) instalada y utiliza el modo de administrador de recursos:</span><span class="sxs-lookup"><span data-stu-id="86b0b-113">toocreate a Network Security Group and rules you need [hello Azure CLI 1.0](../../cli-install-nodejs.md) installed and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="86b0b-114">En hello en los ejemplos siguientes, reemplace los nombres de parámetros de ejemplo con sus propios valores.</span><span class="sxs-lookup"><span data-stu-id="86b0b-114">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="86b0b-115">Los nombres de parámetro de ejemplo incluían *myResourceGroup*, *myNetworkSecurityGroup* y *myVnet*.</span><span class="sxs-lookup"><span data-stu-id="86b0b-115">Example parameter names included *myResourceGroup*, *myNetworkSecurityGroup*, and *myVnet*.</span></span>

<span data-ttu-id="86b0b-116">Cree el grupo de seguridad de red y escriba sus propios nombres y su propia ubicación según sea adecuado.</span><span class="sxs-lookup"><span data-stu-id="86b0b-116">Create your Network Security Group, entering your own names and location appropriately.</span></span> <span data-ttu-id="86b0b-117">Hello en el ejemplo siguiente se crea un grupo de seguridad de red denominado *myNetworkSecurityGroup* en hello *eastus* ubicación:</span><span class="sxs-lookup"><span data-stu-id="86b0b-117">hello following example creates a Network Security Group named *myNetworkSecurityGroup* in hello *eastus* location:</span></span>

```azurecli
azure network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

<span data-ttu-id="86b0b-118">Agregar un servidor Web tooyour de tráfico de regla tooallow HTTP (o ajustar para su propia situación, como conectividad de acceso o de base de datos SSH).</span><span class="sxs-lookup"><span data-stu-id="86b0b-118">Add a rule tooallow HTTP traffic tooyour webserver (or adjust for your own scenario, such as SSH access or database connectivity).</span></span> <span data-ttu-id="86b0b-119">Hello en el ejemplo siguiente se crea una regla denominada *myNetworkSecurityGroupRule* tooallow TCP de tráfico en el puerto 80:</span><span class="sxs-lookup"><span data-stu-id="86b0b-119">hello following example creates a rule named *myNetworkSecurityGroupRule* tooallow TCP traffic on port 80:</span></span>

```azurecli
azure network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --protocol tcp \
    --direction inbound \
    --priority 1000 \
    --destination-port-range 80 \
    --access allow
```

<span data-ttu-id="86b0b-120">Asociar Hola grupo de seguridad de red con la interfaz de red de la máquina virtual (NIC).</span><span class="sxs-lookup"><span data-stu-id="86b0b-120">Associate hello Network Security Group with your VM's network interface (NIC).</span></span> <span data-ttu-id="86b0b-121">Hello en el ejemplo siguiente se asocia un NIC existente denominado *myNic* con grupo de seguridad de red denominado hello *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="86b0b-121">hello following example associates an existing NIC named *myNic* with hello Network Security Group named *myNetworkSecurityGroup*:</span></span>

```azurecli
azure network nic set \
    --resource-group myResourceGroup \
    --network-security-group-name myNetworkSecurityGroup \
    --name myNic
```

<span data-ttu-id="86b0b-122">Como alternativa, puede asociar el grupo de seguridad de red con una subred de red virtual en lugar de simplemente toohello interfaz de red en una sola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="86b0b-122">Alternatively, you can associate your Network Security Group with a virtual network subnet rather than just toohello network interface on a single VM.</span></span> <span data-ttu-id="86b0b-123">Hello en el ejemplo siguiente se asocia una subred existente denominada *mySubnet* en hello *myVnet* red virtual con hello grupo de seguridad de red denominado *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="86b0b-123">hello following example associates an existing subnet named *mySubnet* in hello *myVnet* virtual network with hello Network Security Group named *myNetworkSecurityGroup*:</span></span>

```azurecli
azure network vnet subnet set \
    --resource-group myResourceGroup \
    --network-security-group-name myNetworkSecurityGroup \
    --vnet-name myVnet --name mySubnet
```

## <a name="more-information-on-network-security-groups"></a><span data-ttu-id="86b0b-124">Más información sobre los grupos de seguridad de red</span><span class="sxs-lookup"><span data-stu-id="86b0b-124">More information on Network Security Groups</span></span>
<span data-ttu-id="86b0b-125">Hola de comandos rápido aquí le permite tooget seguridad y en ejecución con tooyour del flujo de tráfico máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="86b0b-125">hello quick commands here allow you tooget up and running with traffic flowing tooyour VM.</span></span> <span data-ttu-id="86b0b-126">Grupos de seguridad de red proporcionan muchas características excepcionales y granularidad para controlar acceso a los recursos tooyour.</span><span class="sxs-lookup"><span data-stu-id="86b0b-126">Network Security Groups provide many great features and granularity for controlling access tooyour resources.</span></span> <span data-ttu-id="86b0b-127">Puede leer más sobre la [creación de un grupo de seguridad de red y las reglas de ACL aquí](../../virtual-network/virtual-networks-create-nsg-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="86b0b-127">You can read more about [creating a Network Security Group and ACL rules here](../../virtual-network/virtual-networks-create-nsg-arm-cli.md).</span></span>

<span data-ttu-id="86b0b-128">Los grupos de seguridad de red y las reglas de ACL también se pueden definir como parte de las plantillas de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="86b0b-128">You can define Network Security Groups and ACL rules as part of Azure Resource Manager templates.</span></span> <span data-ttu-id="86b0b-129">Más información sobre la [creación de grupos de seguridad de red con plantillas](../../virtual-network/virtual-networks-create-nsg-arm-template.md).</span><span class="sxs-lookup"><span data-stu-id="86b0b-129">Read more about [creating Network Security Groups with templates](../../virtual-network/virtual-networks-create-nsg-arm-template.md).</span></span>

<span data-ttu-id="86b0b-130">Si necesita toouse toomap de reenvío de puerto un puerto interno de tooan único puerto externo en la máquina virtual, use un equilibrador de carga y las reglas de traducción de direcciones de red (NAT).</span><span class="sxs-lookup"><span data-stu-id="86b0b-130">If you need toouse port-forwarding toomap a unique external port tooan internal port on your VM, use a load balancer and Network Address Translation (NAT) rules.</span></span> <span data-ttu-id="86b0b-131">Por ejemplo, puede desee tooexpose el puerto TCP 8080 externamente y tener el tráfico dirigido tooTCP puerto 80 en una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="86b0b-131">For example, you may want tooexpose TCP port 8080 externally and have traffic directed tooTCP port 80 on a VM.</span></span> <span data-ttu-id="86b0b-132">Puede aprender sobre la [creación de un equilibrador de carga accesible desde Internet](../../load-balancer/load-balancer-get-started-internet-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="86b0b-132">You can learn about [creating an Internet-facing load balancer](../../load-balancer/load-balancer-get-started-internet-arm-cli.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="86b0b-133">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="86b0b-133">Next steps</span></span>
<span data-ttu-id="86b0b-134">En este ejemplo, ha creado el tráfico de tooallow HTTP de una regla sencilla.</span><span class="sxs-lookup"><span data-stu-id="86b0b-134">In this example, you created a simple rule tooallow HTTP traffic.</span></span> <span data-ttu-id="86b0b-135">Puede encontrar información sobre cómo crear entornos más detallados en hello siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="86b0b-135">You can find information on creating more detailed environments in hello following articles:</span></span>

* [<span data-ttu-id="86b0b-136">Información general sobre Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="86b0b-136">Azure Resource Manager overview</span></span>](../../azure-resource-manager/resource-group-overview.md)
* [<span data-ttu-id="86b0b-137">¿Qué es un grupo de seguridad de red?</span><span class="sxs-lookup"><span data-stu-id="86b0b-137">What is a Network Security Group (NSG)?</span></span>](../../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="86b0b-138">Información general de Azure Resource Manager para equilibradores de carga</span><span class="sxs-lookup"><span data-stu-id="86b0b-138">Azure Resource Manager Overview for Load Balancers</span></span>](../../load-balancer/load-balancer-arm.md)

