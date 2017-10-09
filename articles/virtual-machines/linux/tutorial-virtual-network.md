---
title: "aaaAzure redes virtuales y máquinas virtuales de Linux | Documentos de Microsoft"
description: "Tutorial: administrar redes virtuales de Azure y máquinas virtuales de Linux con hello CLI de Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/10/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 57e6bd4de16f0e31d53dc67bf50dc5730d43712b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-virtual-networks-and-linux-virtual-machines-with-hello-azure-cli"></a><span data-ttu-id="acd04-103">Administrar redes virtuales de Azure y máquinas virtuales de Linux con hello CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="acd04-103">Manage Azure Virtual Networks and Linux Virtual Machines with hello Azure CLI</span></span>

<span data-ttu-id="acd04-104">Las máquinas virtuales de Azure utilizan las redes de Azure para la comunicación de red interna y externa.</span><span class="sxs-lookup"><span data-stu-id="acd04-104">Azure virtual machines use Azure networking for internal and external network communication.</span></span> <span data-ttu-id="acd04-105">Este tutorial le guía a través de la implementación de dos máquinas virtuales y la configuración de redes de Azure para estas máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="acd04-105">This tutorial walks through deploying two virtual machines and configuring Azure networking for these VMs.</span></span> <span data-ttu-id="acd04-106">ejemplos de Hello en este tutorial se supone que hello las máquinas virtuales hospedan una aplicación web con una base de datos back-end, sin embargo, no se implementa una aplicación de tutorial de Hola.</span><span class="sxs-lookup"><span data-stu-id="acd04-106">hello examples in this tutorial assume that hello VMs are hosting a web application with a database back-end, however an application is not deployed in hello tutorial.</span></span> <span data-ttu-id="acd04-107">En este tutorial, aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="acd04-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="acd04-108">Implementar una red virtual</span><span class="sxs-lookup"><span data-stu-id="acd04-108">Deploy a virtual network</span></span>
> * <span data-ttu-id="acd04-109">Crear una subred dentro de una red virtual</span><span class="sxs-lookup"><span data-stu-id="acd04-109">Create a subnet within a virtual network</span></span>
> * <span data-ttu-id="acd04-110">Conectar máquinas virtuales tooa subred</span><span class="sxs-lookup"><span data-stu-id="acd04-110">Attach virtual machines tooa subnet</span></span>
> * <span data-ttu-id="acd04-111">Administrar direcciones IP públicas de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="acd04-111">Manage virtual machine public IP addresses</span></span>
> * <span data-ttu-id="acd04-112">Proteger el tráfico entrante de Internet</span><span class="sxs-lookup"><span data-stu-id="acd04-112">Secure incoming internet traffic</span></span>
> * <span data-ttu-id="acd04-113">Proteger el tráfico de tooVM VM</span><span class="sxs-lookup"><span data-stu-id="acd04-113">Secure VM tooVM traffic</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="acd04-114">Si elige tooinstall y usar hello CLI localmente, este tutorial requiere que se ejecuta la versión de CLI de Azure de hello 2.0.4 o versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="acd04-114">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="acd04-115">Ejecutar `az --version` toofind versión de Hola.</span><span class="sxs-lookup"><span data-stu-id="acd04-115">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="acd04-116">Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="acd04-116">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="vm-networking-overview"></a><span data-ttu-id="acd04-117">Introducción a las redes de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="acd04-117">VM networking overview</span></span>

<span data-ttu-id="acd04-118">Redes virtuales de Azure habilitar las conexiones de red segura entre las máquinas virtuales, Hola internet y otros servicios de Azure como base de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="acd04-118">Azure virtual networks enable secure network connections between virtual machines, hello internet, and other Azure services such as Azure SQL database.</span></span> <span data-ttu-id="acd04-119">Las redes virtuales se dividen en segmentos lógicos llamados subredes.</span><span class="sxs-lookup"><span data-stu-id="acd04-119">Virtual networks are broken down into logical segments called subnets.</span></span> <span data-ttu-id="acd04-120">Se utilizan subredes toocontrol flujo de red y como un límite de seguridad.</span><span class="sxs-lookup"><span data-stu-id="acd04-120">Subnets are used toocontrol network flow, and as a security boundary.</span></span> <span data-ttu-id="acd04-121">Al implementar una máquina virtual, por lo general incluye una interfaz de red virtual, subred tooa adjunto.</span><span class="sxs-lookup"><span data-stu-id="acd04-121">When deploying a VM, it generally includes a virtual network interface, which is attached tooa subnet.</span></span>

## <a name="deploy-virtual-network"></a><span data-ttu-id="acd04-122">Implementación de una red virtual</span><span class="sxs-lookup"><span data-stu-id="acd04-122">Deploy virtual network</span></span>

<span data-ttu-id="acd04-123">Para este tutorial, se crea una única red virtual con dos subredes:</span><span class="sxs-lookup"><span data-stu-id="acd04-123">For this tutorial, a single virtual network is created with two subnets.</span></span> <span data-ttu-id="acd04-124">una subred de front-end para hospedar una aplicación web y una subred de back-end para hospedar un servidor de bases de datos.</span><span class="sxs-lookup"><span data-stu-id="acd04-124">A front-end subnet for hosting a web application, and a back-end subnet for hosting a database server.</span></span>

<span data-ttu-id="acd04-125">Antes de poder crear una red virtual, cree un grupo de recursos con [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="acd04-125">Before you can create a virtual network, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="acd04-126">Hello en el ejemplo siguiente se crea un grupo de recursos denominado *myRGNetwork* en ubicación de eastus Hola.</span><span class="sxs-lookup"><span data-stu-id="acd04-126">hello following example creates a resource group named *myRGNetwork* in hello eastus location.</span></span>

```azurecli-interactive 
az group create --name myRGNetwork --location eastus
```

### <a name="create-virtual-network"></a><span data-ttu-id="acd04-127">Creación de una red virtual</span><span class="sxs-lookup"><span data-stu-id="acd04-127">Create virtual network</span></span>

<span data-ttu-id="acd04-128">Nos Hola [crear red virtual de red az](/cli/azure/network/vnet#create) comando toocreate una red virtual.</span><span class="sxs-lookup"><span data-stu-id="acd04-128">Us hello [az network vnet create](/cli/azure/network/vnet#create) command toocreate a virtual network.</span></span> <span data-ttu-id="acd04-129">En este ejemplo, se denomina red hello *mvVnet* y se le asigna un prefijo de dirección de *10.0.0.0/16*.</span><span class="sxs-lookup"><span data-stu-id="acd04-129">In this example, hello network is named *mvVnet* and is given an address prefix of *10.0.0.0/16*.</span></span> <span data-ttu-id="acd04-130">También se crea una subred con el nombre de *mySubnetFrontEnd* y un prefijo de *10.0.1.0/24*.</span><span class="sxs-lookup"><span data-stu-id="acd04-130">A subnet is also created with a name of *mySubnetFrontEnd* and a prefix of *10.0.1.0/24*.</span></span> <span data-ttu-id="acd04-131">Más adelante en este tutorial una VM front-end está conectado toothis subred.</span><span class="sxs-lookup"><span data-stu-id="acd04-131">Later in this tutorial a front-end VM is connected toothis subnet.</span></span> 

```azurecli-interactive 
az network vnet create \
  --resource-group myRGNetwork \
  --name myVnet \
  --address-prefix 10.0.0.0/16 \
  --subnet-name mySubnetFrontEnd \
  --subnet-prefix 10.0.1.0/24
```

### <a name="create-subnet"></a><span data-ttu-id="acd04-132">Creación de una subred</span><span class="sxs-lookup"><span data-stu-id="acd04-132">Create subnet</span></span>

<span data-ttu-id="acd04-133">Una subred nueva se agrega la red virtual de toohello con hello [crear subredes de red virtual de red az](/cli/azure/network/vnet/subnet#create) comando.</span><span class="sxs-lookup"><span data-stu-id="acd04-133">A new subnet is added toohello virtual network using hello [az network vnet subnet create](/cli/azure/network/vnet/subnet#create) command.</span></span> <span data-ttu-id="acd04-134">En este ejemplo, se denomina subred hello *mySubnetBackEnd* y se le asigna un prefijo de dirección de *10.0.2.0/24*.</span><span class="sxs-lookup"><span data-stu-id="acd04-134">In this example, hello subnet is named *mySubnetBackEnd* and is given an address prefix of *10.0.2.0/24*.</span></span> <span data-ttu-id="acd04-135">Esta subred se usa con todos los servicios back-end.</span><span class="sxs-lookup"><span data-stu-id="acd04-135">This subnet is used with all back-end services.</span></span>

```azurecli-interactive 
az network vnet subnet create \
  --resource-group myRGNetwork \
  --vnet-name myVnet \
  --name mySubnetBackEnd \
  --address-prefix 10.0.2.0/24
```

<span data-ttu-id="acd04-136">Entonces, se ha creado una red y se ha segmentado en dos subredes, una para servicios front-end y otra para servicios back-end.</span><span class="sxs-lookup"><span data-stu-id="acd04-136">At this point, a network has been created and segmented into two subnets, one for front-end services, and another for back-end services.</span></span> <span data-ttu-id="acd04-137">En la siguiente sección hello, máquinas virtuales se crean y toothese subredes conectadas.</span><span class="sxs-lookup"><span data-stu-id="acd04-137">In hello next section, virtual machines are created and connected toothese subnets.</span></span>

## <a name="understand-public-ip-address"></a><span data-ttu-id="acd04-138">Información sobre la dirección IP pública</span><span class="sxs-lookup"><span data-stu-id="acd04-138">Understand public IP address</span></span>

<span data-ttu-id="acd04-139">Una dirección IP pública permite pueden tener acceso a recursos de Azure toobe Hola internet.</span><span class="sxs-lookup"><span data-stu-id="acd04-139">A public IP address allows Azure resources toobe accessible on hello internet.</span></span> <span data-ttu-id="acd04-140">En esta sección del tutorial de hello, una máquina virtual se crea toodemonstrate cómo aborda toowork con la dirección IP pública.</span><span class="sxs-lookup"><span data-stu-id="acd04-140">In this section of hello tutorial, a VM is created toodemonstrate how toowork with public IP addresses.</span></span>

### <a name="allocation-method"></a><span data-ttu-id="acd04-141">Método de asignación</span><span class="sxs-lookup"><span data-stu-id="acd04-141">Allocation method</span></span>

<span data-ttu-id="acd04-142">Una dirección IP pública puede asignarse ya sea de forma dinámica o estática.</span><span class="sxs-lookup"><span data-stu-id="acd04-142">A public IP address can be allocated as either dynamic or static.</span></span> <span data-ttu-id="acd04-143">De forma predeterminada, la dirección IP pública se asigna dinámicamente.</span><span class="sxs-lookup"><span data-stu-id="acd04-143">By default, public IP address dynamically allocated.</span></span> <span data-ttu-id="acd04-144">Las direcciones IP dinámicas se liberan al desasignar una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="acd04-144">Dynamic IP addresses are released when a VM is deallocated.</span></span> <span data-ttu-id="acd04-145">Este comportamiento provoca toochange de dirección IP de Hola durante cualquier operación que incluya una cancelación de asignación de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="acd04-145">This behavior causes hello IP address toochange during any operation that includes a VM deallocation.</span></span>

<span data-ttu-id="acd04-146">se puede establecer el método de asignación de Hello toostatic, lo que garantiza que la dirección IP de Hola permanecen asignados tooa máquina virtual, incluso durante un estado de asignación ha sido cancelado.</span><span class="sxs-lookup"><span data-stu-id="acd04-146">hello allocation method can be set toostatic, which ensures that hello IP address remain assigned tooa VM, even during a deallocated state.</span></span> <span data-ttu-id="acd04-147">Cuando se usa una dirección IP asignada estáticamente, no se puede especificar la dirección IP hello en sí misma.</span><span class="sxs-lookup"><span data-stu-id="acd04-147">When using a statically allocated IP address, hello IP address itself cannot be specified.</span></span> <span data-ttu-id="acd04-148">sino que se asigna desde un grupo de direcciones disponibles.</span><span class="sxs-lookup"><span data-stu-id="acd04-148">Instead, it is allocated from a pool of available addresses.</span></span>

### <a name="dynamic-allocation"></a><span data-ttu-id="acd04-149">Asignación dinámica</span><span class="sxs-lookup"><span data-stu-id="acd04-149">Dynamic allocation</span></span>

<span data-ttu-id="acd04-150">Al crear una máquina virtual con hello [crear vm az](/cli/azure/vm#create) comando, método de asignación de hello predeterminado público IP dirección es dinámico.</span><span class="sxs-lookup"><span data-stu-id="acd04-150">When creating a VM with hello [az vm create](/cli/azure/vm#create) command, hello default public IP address allocation method is dynamic.</span></span> <span data-ttu-id="acd04-151">En el siguiente ejemplo de Hola, se crea una máquina virtual con una dirección IP dinámica.</span><span class="sxs-lookup"><span data-stu-id="acd04-151">In hello following example, a VM is created with a dynamic IP address.</span></span> 

```azurecli-interactive 
az vm create \
  --resource-group myRGNetwork \
  --name myFrontEndVM \
  --vnet-name myVnet \
  --subnet mySubnetFrontEnd \
  --nsg myNSGFrontEnd \
  --public-ip-address myFrontEndIP \
  --image UbuntuLTS \
  --generate-ssh-keys
```

### <a name="static-allocation"></a><span data-ttu-id="acd04-152">Asignación estática</span><span class="sxs-lookup"><span data-stu-id="acd04-152">Static allocation</span></span>

<span data-ttu-id="acd04-153">Al crear una máquina virtual mediante hello [crear vm az](/cli/azure/vm#create) de comando, se incluyen hello `--public-ip-address-allocation static` argumento tooassign una dirección IP pública estática.</span><span class="sxs-lookup"><span data-stu-id="acd04-153">When creating a virtual machine using hello [az vm create](/cli/azure/vm#create) command, include hello `--public-ip-address-allocation static` argument tooassign a static public IP address.</span></span> <span data-ttu-id="acd04-154">Esta operación no está demostrada en este tutorial, sin embargo en la sección siguiente de hello una dirección IP asignada dinámicamente es tooa modificado estáticamente dirección asignada.</span><span class="sxs-lookup"><span data-stu-id="acd04-154">This operation is not demonstrated in this tutorial, however in hello next section a dynamically allocated IP address is changed tooa statically allocated address.</span></span> 

### <a name="change-allocation-method"></a><span data-ttu-id="acd04-155">Cambio del método de asignación</span><span class="sxs-lookup"><span data-stu-id="acd04-155">Change allocation method</span></span>

<span data-ttu-id="acd04-156">se puede cambiar el método de asignación de direcciones IP de Hello mediante hello [actualizar la ip pública de red az](/cli/azure/network/public-ip#update) comando.</span><span class="sxs-lookup"><span data-stu-id="acd04-156">hello IP address allocation method can be changed using hello [az network public-ip update](/cli/azure/network/public-ip#update) command.</span></span> <span data-ttu-id="acd04-157">En este ejemplo, método de asignación de direcciones IP de hello VM front-end se cambia de Hola toostatic.</span><span class="sxs-lookup"><span data-stu-id="acd04-157">In this example, hello IP address allocation method of hello front-end VM is changed toostatic.</span></span>

<span data-ttu-id="acd04-158">En primer lugar, desasignar Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="acd04-158">First, deallocate hello VM.</span></span>

```azurecli-interactive 
az vm deallocate --resource-group myRGNetwork --name myFrontEndVM
```

<span data-ttu-id="acd04-159">Hola de uso [actualizar la ip pública de red az](/cli/azure/network/public-ip#update) método de asignación de hello tooupdate de comandos.</span><span class="sxs-lookup"><span data-stu-id="acd04-159">Use hello [az network public-ip update](/cli/azure/network/public-ip#update) command tooupdate hello allocation method.</span></span> <span data-ttu-id="acd04-160">En este caso, Hola `--allocation-method` se establece demasiado*estático*.</span><span class="sxs-lookup"><span data-stu-id="acd04-160">In this case, hello `--allocation-method` is being set too*static*.</span></span>

```azurecli-interactive 
az network public-ip update --resource-group myRGNetwork --name myFrontEndIP --allocation-method static
```

<span data-ttu-id="acd04-161">Iniciar VM Hola.</span><span class="sxs-lookup"><span data-stu-id="acd04-161">Start hello VM.</span></span>

```azurecli-interactive 
az vm start --resource-group myRGNetwork --name myFrontEndVM --no-wait
```

### <a name="no-public-ip-address"></a><span data-ttu-id="acd04-162">Sin dirección IP pública</span><span class="sxs-lookup"><span data-stu-id="acd04-162">No public IP address</span></span>

<span data-ttu-id="acd04-163">A menudo, una máquina virtual no es necesario toobe accesible a través de internet de Hola.</span><span class="sxs-lookup"><span data-stu-id="acd04-163">Often, a VM does not need toobe accessible over hello internet.</span></span> <span data-ttu-id="acd04-164">una máquina virtual sin una dirección IP pública, use hello toocreate `--public-ip-address ""` argumento con un conjunto vacío de comillas dobles.</span><span class="sxs-lookup"><span data-stu-id="acd04-164">toocreate a VM without a public IP address, use hello `--public-ip-address ""` argument with an empty set of double quotes.</span></span> <span data-ttu-id="acd04-165">Esta configuración se muestra más adelante en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="acd04-165">This configuration is demonstrated later in this tutorial</span></span>

## <a name="secure-network-traffic"></a><span data-ttu-id="acd04-166">Protegen el tráfico de red.</span><span class="sxs-lookup"><span data-stu-id="acd04-166">Secure network traffic</span></span>

<span data-ttu-id="acd04-167">Un grupo de seguridad de red (NSG) contiene una lista de reglas de seguridad que permiten o deniegan tooresources de tráfico de red conectados a redes virtuales tooAzure (VNet).</span><span class="sxs-lookup"><span data-stu-id="acd04-167">A network security group (NSG) contains a list of security rules that allow or deny network traffic tooresources connected tooAzure Virtual Networks (VNet).</span></span> <span data-ttu-id="acd04-168">Los NSG pueden toosubnets asociado o interfaces de red individuales.</span><span class="sxs-lookup"><span data-stu-id="acd04-168">NSGs can be associated toosubnets or individual network interfaces.</span></span> <span data-ttu-id="acd04-169">Cuando un NSG está asociado a una interfaz de red, se aplica solo Hola asociados máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="acd04-169">When an NSG is associated with a network interface, it applies only hello associated VM.</span></span> <span data-ttu-id="acd04-170">Cuando un NSG está asociado tooa subred, Hola reglas aplican tooall recursos toohello conectado subred.</span><span class="sxs-lookup"><span data-stu-id="acd04-170">When an NSG is associated tooa subnet, hello rules apply tooall resources connected toohello subnet.</span></span> 

### <a name="network-security-group-rules"></a><span data-ttu-id="acd04-171">Reglas del grupo de seguridad de red</span><span class="sxs-lookup"><span data-stu-id="acd04-171">Network security group rules</span></span>

<span data-ttu-id="acd04-172">Las reglas de NSG definen puertos de redes a través de los que se permite o deniega el tráfico.</span><span class="sxs-lookup"><span data-stu-id="acd04-172">NSG rules define networking ports over which traffic is allowed or denied.</span></span> <span data-ttu-id="acd04-173">las reglas de Hello pueden incluir intervalos de direcciones IP de origen y destino para que controle el tráfico entre sistemas específicos o subredes.</span><span class="sxs-lookup"><span data-stu-id="acd04-173">hello rules can include source and destination IP address ranges so that traffic is controlled between specific systems or subnets.</span></span> <span data-ttu-id="acd04-174">Las reglas de NSG también incluyen una prioridad (entre 1 y 4096).</span><span class="sxs-lookup"><span data-stu-id="acd04-174">NSG rules also include a priority (between 1—and 4096).</span></span> <span data-ttu-id="acd04-175">Las reglas se evalúan en orden de Hola de prioridad.</span><span class="sxs-lookup"><span data-stu-id="acd04-175">Rules are evaluated in hello order of priority.</span></span> <span data-ttu-id="acd04-176">Una regla con una prioridad de 100 se evalúa antes que una regla con prioridad de 200.</span><span class="sxs-lookup"><span data-stu-id="acd04-176">A rule with a priority of 100 is evaluated before a rule with priority 200.</span></span>

<span data-ttu-id="acd04-177">Todos los grupos de seguridad de red contienen un conjunto de reglas predeterminadas.</span><span class="sxs-lookup"><span data-stu-id="acd04-177">All NSGs contain a set of default rules.</span></span> <span data-ttu-id="acd04-178">no se puede eliminar las reglas predeterminadas de Hello, pero dado que se asignan prioridad más baja de hello, pueden reemplazarse por reglas de Hola que cree.</span><span class="sxs-lookup"><span data-stu-id="acd04-178">hello default rules cannot be deleted, but because they are assigned hello lowest priority, they can be overridden by hello rules that you create.</span></span>

- <span data-ttu-id="acd04-179">**Red virtual:** el tráfico que se origina y termina en una red virtual se permite en las direcciones tanto de entrada como de salida.</span><span class="sxs-lookup"><span data-stu-id="acd04-179">**Virtual network** - Traffic originating and ending in a virtual network is allowed both in inbound and outbound directions.</span></span>
- <span data-ttu-id="acd04-180">**Internet:** se permite el tráfico saliente pero se bloquea el entrante.</span><span class="sxs-lookup"><span data-stu-id="acd04-180">**Internet** - Outbound traffic is allowed, but inbound traffic is blocked.</span></span>
- <span data-ttu-id="acd04-181">**El equilibrador de carga** -estado hello tooprobe de equilibrador de carga de Azure permiten de las máquinas virtuales y las instancias de rol.</span><span class="sxs-lookup"><span data-stu-id="acd04-181">**Load balancer** - Allow Azure’s load balancer tooprobe hello health of your VMs and role instances.</span></span> <span data-ttu-id="acd04-182">Si no va a usar un conjunto con equilibrio de carga, puede invalidar esta regla.</span><span class="sxs-lookup"><span data-stu-id="acd04-182">If you are not using a load balanced set, you can override this rule.</span></span>

### <a name="create-network-security-groups"></a><span data-ttu-id="acd04-183">Creación de grupos de seguridad de red</span><span class="sxs-lookup"><span data-stu-id="acd04-183">Create network security groups</span></span>

<span data-ttu-id="acd04-184">Un grupo de seguridad de red se puede crear en hello mismo tiempo como una máquina virtual mediante hello [crear vm az](/cli/azure/vm#create) comando.</span><span class="sxs-lookup"><span data-stu-id="acd04-184">A network security group can be created at hello same time as a VM using hello [az vm create](/cli/azure/vm#create) command.</span></span> <span data-ttu-id="acd04-185">Al hacerlo, hello NSG está asociado a la interfaz de red de máquinas virtuales de hello y una regla de NSG tooallow creados de forma automática un tráfico en el puerto *22* de cualquier origen.</span><span class="sxs-lookup"><span data-stu-id="acd04-185">When doing so, hello NSG is associated with hello VMs network interface and an NSG rule is auto created tooallow traffic on port *22* from any source.</span></span> <span data-ttu-id="acd04-186">Anteriormente en este tutorial, hello NSG front-end fue creado automáticamente con Hola VM front-end.</span><span class="sxs-lookup"><span data-stu-id="acd04-186">Earlier in this tutorial, hello front-end NSG was auto-created with hello front-end VM.</span></span> <span data-ttu-id="acd04-187">También se crea automáticamente una regla de NSG para el puerto 22.</span><span class="sxs-lookup"><span data-stu-id="acd04-187">An NSG rule was also auto created for port 22.</span></span> 

<span data-ttu-id="acd04-188">En algunos casos, puede ser útil toopre-crear un NSG, como cuando no se deben crear reglas predeterminadas de SSH o cuando hello NSG debe ser subred tooa adjunto.</span><span class="sxs-lookup"><span data-stu-id="acd04-188">In some cases, it may be helpful toopre-create an NSG, such as when default SSH rules should not be created, or when hello NSG should be attached tooa subnet.</span></span> 

<span data-ttu-id="acd04-189">Hola de uso [crear az red nsg](/cli/azure/network/nsg#create) comando toocreate un grupo de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="acd04-189">Use hello [az network nsg create](/cli/azure/network/nsg#create) command toocreate a network security group.</span></span>

```azurecli-interactive 
az network nsg create --resource-group myRGNetwork --name myNSGBackEnd
```

<span data-ttu-id="acd04-190">En lugar de asociación de interfaz de red de hello NSG tooa, está asociado a una subred.</span><span class="sxs-lookup"><span data-stu-id="acd04-190">Instead of associating hello NSG tooa network interface, it is associated with a subnet.</span></span> <span data-ttu-id="acd04-191">En esta configuración, todas las máquinas virtuales que está adjunto toohello subred hereda reglas NSG Hola.</span><span class="sxs-lookup"><span data-stu-id="acd04-191">In this configuration, any VM that is attached toohello subnet inherits hello NSG rules.</span></span>

<span data-ttu-id="acd04-192">Actualizar Hola subred existente denominado *mySubnetBackEnd* con Hola nuevo NSG.</span><span class="sxs-lookup"><span data-stu-id="acd04-192">Update hello existing subnet named *mySubnetBackEnd* with hello new NSG.</span></span>

```azurecli-interactive 
az network vnet subnet update \
  --resource-group myRGNetwork \
  --vnet-name myVnet \
  --name mySubnetBackEnd \
  --network-security-group myNSGBackEnd
```

<span data-ttu-id="acd04-193">Ahora cree una máquina virtual, que está adjunto toohello *mySubnetBackEnd*.</span><span class="sxs-lookup"><span data-stu-id="acd04-193">Now create a virtual machine, which is attached toohello *mySubnetBackEnd*.</span></span> <span data-ttu-id="acd04-194">Tenga en cuenta que hello `--nsg` argumento tiene un valor de comillas dobles vacías.</span><span class="sxs-lookup"><span data-stu-id="acd04-194">Notice that hello `--nsg` argument has a value of empty double quotes.</span></span> <span data-ttu-id="acd04-195">Un NSG no es necesario toobe creado con hello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="acd04-195">An NSG does not need toobe created with hello VM.</span></span> <span data-ttu-id="acd04-196">Hola VM es la subred de back-end toohello adjunto, que está protegido con hello NSG de back-end ha creado previamente.</span><span class="sxs-lookup"><span data-stu-id="acd04-196">hello VM is attached toohello back-end subnet, which is protected with hello pre-created back-end NSG.</span></span> <span data-ttu-id="acd04-197">Esta NSG aplica toohello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="acd04-197">This NSG applies toohello VM.</span></span> <span data-ttu-id="acd04-198">Además, tenga en cuenta aquí que hello `--public-ip-address` argumento tiene un valor de comillas dobles vacías.</span><span class="sxs-lookup"><span data-stu-id="acd04-198">Also, notice here that hello `--public-ip-address` argument has a value of empty double quotes.</span></span> <span data-ttu-id="acd04-199">Esta configuración crea una máquina virtual sin una dirección IP pública.</span><span class="sxs-lookup"><span data-stu-id="acd04-199">This configuration creates a VM without a public IP address.</span></span> 

```azurecli-interactive 
az vm create \
  --resource-group myRGNetwork \
  --name myBackEndVM \
  --vnet-name myVnet \
  --subnet mySubnetBackEnd \
  --public-ip-address "" \
  --nsg "" \
  --image UbuntuLTS \
  --generate-ssh-keys
```

### <a name="secure-incoming-traffic"></a><span data-ttu-id="acd04-200">Protección del tráfico entrante</span><span class="sxs-lookup"><span data-stu-id="acd04-200">Secure incoming traffic</span></span>

<span data-ttu-id="acd04-201">Cuando hello front-end se crea la VM, se creó una regla NSG tooallow el tráfico entrante en el puerto 22.</span><span class="sxs-lookup"><span data-stu-id="acd04-201">When hello front-end VM was created, an NSG rule was created tooallow incoming traffic on port 22.</span></span> <span data-ttu-id="acd04-202">Esta regla permite las conexiones de SSH toohello VM.</span><span class="sxs-lookup"><span data-stu-id="acd04-202">This rule allows SSH connections toohello VM.</span></span> <span data-ttu-id="acd04-203">En este ejemplo, también se debería permitir el tráfico en el puerto *80*.</span><span class="sxs-lookup"><span data-stu-id="acd04-203">For this example, traffic should also be allowed on port *80*.</span></span> <span data-ttu-id="acd04-204">Esta configuración permite que un toobe de aplicación web tiene acceso en hello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="acd04-204">This configuration allows a web application toobe accessed on hello VM.</span></span>

<span data-ttu-id="acd04-205">Hola de uso [crear regla de nsg de red az](/cli/azure/network/nsg/rule#create) toocreate una regla para el puerto de comando *80*.</span><span class="sxs-lookup"><span data-stu-id="acd04-205">Use hello [az network nsg rule create](/cli/azure/network/nsg/rule#create) command toocreate a rule for port *80*.</span></span>

```azurecli-interactive 
az network nsg rule create \
  --resource-group myRGNetwork \
  --nsg-name myNSGFrontEnd \
  --name http \
  --access allow \
  --protocol Tcp \
  --direction Inbound \
  --priority 200 \
  --source-address-prefix "*" \
  --source-port-range "*" \
  --destination-address-prefix "*" \
  --destination-port-range 80
```

<span data-ttu-id="acd04-206">Hello VM front-end ahora solo es accesible en el puerto *22* y el puerto *80*.</span><span class="sxs-lookup"><span data-stu-id="acd04-206">hello front-end VM is now only accessible on port *22* and port *80*.</span></span> <span data-ttu-id="acd04-207">El resto del tráfico entrante se bloquea en el grupo de seguridad de red de Hola.</span><span class="sxs-lookup"><span data-stu-id="acd04-207">All other incoming traffic is blocked at hello network security group.</span></span> <span data-ttu-id="acd04-208">Puede ser útil toovisualize las configuraciones de reglas de hello NSG.</span><span class="sxs-lookup"><span data-stu-id="acd04-208">It may be helpful toovisualize hello NSG rule configurations.</span></span> <span data-ttu-id="acd04-209">Configuración de reglas NSG Hola devuelto con hello [lista de reglas de red az](/cli/azure/network/nsg/rule#list) comando.</span><span class="sxs-lookup"><span data-stu-id="acd04-209">Return hello NSG rule configuration with hello [az network rule list](/cli/azure/network/nsg/rule#list) command.</span></span> 

```azurecli-interactive 
az network nsg rule list --resource-group myRGNetwork --nsg-name myNSGFrontEnd --output table
```

<span data-ttu-id="acd04-210">Salida:</span><span class="sxs-lookup"><span data-stu-id="acd04-210">Output:</span></span>

```azurecli-interactive 
Access    DestinationAddressPrefix      DestinationPortRange  Direction    Name                 Priority  Protocol    ProvisioningState    ResourceGroup    SourceAddressPrefix    SourcePortRange
--------  --------------------------  ----------------------  -----------  -----------------  ----------  ----------  -------------------  ---------------  ---------------------  -----------------
Allow     *                                               22  Inbound      default-allow-ssh        1000  Tcp         Succeeded            myRGNetwork      *                      *
Allow     *                                               80  Inbound      http                      200  Tcp         Succeeded            myRGNetwork      *                      *
```

### <a name="secure-vm-toovm-traffic"></a><span data-ttu-id="acd04-211">Proteger el tráfico de tooVM VM</span><span class="sxs-lookup"><span data-stu-id="acd04-211">Secure VM tooVM traffic</span></span>

<span data-ttu-id="acd04-212">También pueden aplicar reglas del grupo de seguridad de red entre máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="acd04-212">Network security group rules can also apply between VMs.</span></span> <span data-ttu-id="acd04-213">En este ejemplo, hello VM front-end debe toocommunicate con Hola VM back-end en el puerto *22* y *3306*.</span><span class="sxs-lookup"><span data-stu-id="acd04-213">For this example, hello front-end VM needs toocommunicate with hello back-end VM on port *22* and *3306*.</span></span> <span data-ttu-id="acd04-214">Esta configuración permite que las conexiones de SSH de Hola VM front-end y también permiten que una aplicación en hello toocommunicate front-end de máquina virtual con una base de datos de MySQL de back-end.</span><span class="sxs-lookup"><span data-stu-id="acd04-214">This configuration allows SSH connections from hello front-end VM, and also allow an application on hello front-end VM toocommunicate with a back-end MySQL database.</span></span> <span data-ttu-id="acd04-215">Se debe bloquear todo el tráfico entre Hola front-end y back-end las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="acd04-215">All other traffic should be blocked between hello front-end and back-end virtual machines.</span></span>

<span data-ttu-id="acd04-216">Hola de uso [crear regla de nsg de red az](/cli/azure/network/nsg/rule#create) comando toocreate una regla para el puerto 22.</span><span class="sxs-lookup"><span data-stu-id="acd04-216">Use hello [az network nsg rule create](/cli/azure/network/nsg/rule#create) command toocreate a rule for port 22.</span></span> <span data-ttu-id="acd04-217">Tenga en cuenta que hello `--source-address-prefix` argumento especifica un valor de *10.0.1.0/24*.</span><span class="sxs-lookup"><span data-stu-id="acd04-217">Notice that hello `--source-address-prefix` argument specifies a value of *10.0.1.0/24*.</span></span> <span data-ttu-id="acd04-218">Esta configuración garantiza que se permite únicamente el tráfico de subred de front-end de Hola a través de hello NSG.</span><span class="sxs-lookup"><span data-stu-id="acd04-218">This configuration ensures that only traffic from hello front-end subnet is allowed through hello NSG.</span></span>

```azurecli-interactive 
az network nsg rule create \
  --resource-group myRGNetwork \
  --nsg-name myNSGBackEnd \
  --name SSH \
  --access Allow \
  --protocol Tcp \
  --direction Inbound \
  --priority 100 \
  --source-address-prefix 10.0.1.0/24 \
  --source-port-range "*" \
  --destination-address-prefix "*" \
  --destination-port-range "22"
```

<span data-ttu-id="acd04-219">Ahora, agregue una regla para el tráfico de MySQL en el puerto 3306.</span><span class="sxs-lookup"><span data-stu-id="acd04-219">Now add a rule for MySQL traffic on port 3306.</span></span>

```azurecli-interactive 
az network nsg rule create \
  --resource-group myRGNetwork \
  --nsg-name myNSGBackEnd \
  --name MySQL \
  --access Allow \
  --protocol Tcp \
  --direction Inbound \
  --priority 200 \
  --source-address-prefix 10.0.1.0/24 \
  --source-port-range "*" \
  --destination-address-prefix "*" \
  --destination-port-range "3306"
```

<span data-ttu-id="acd04-220">Por último, porque los NSG tienen una regla predeterminada que permite todo el tráfico entre máquinas virtuales en hello misma red virtual, puede puede crear una regla para hello back-end NSG tooblock todo el tráfico.</span><span class="sxs-lookup"><span data-stu-id="acd04-220">Finally, because NSGs have a default rule allowing all traffic between VMs in hello same VNet, a rule can be created for hello back-end NSGs tooblock all traffic.</span></span> <span data-ttu-id="acd04-221">Tenga en cuenta aquí que hello `--priority` se le asigna un valor de *300*, que es menor que ambos Hola reglas de NSG y MySQL.</span><span class="sxs-lookup"><span data-stu-id="acd04-221">Notice here that hello `--priority` is given a value of *300*, which is lower that both hello NSG and MySQL rules.</span></span> <span data-ttu-id="acd04-222">Esta configuración garantiza que todavía se permite el tráfico SSH y MySQL a través de hello NSG.</span><span class="sxs-lookup"><span data-stu-id="acd04-222">This configuration ensures that SSH and MySQL traffic is still allowed through hello NSG.</span></span>

```azurecli-interactive 
az network nsg rule create \
  --resource-group myRGNetwork \
  --nsg-name myNSGBackEnd \
  --name denyAll \
  --access Deny \
  --protocol Tcp \
  --direction Inbound \
  --priority 300 \
  --source-address-prefix "*" \
  --source-port-range "*" \
  --destination-address-prefix "*" \
  --destination-port-range "*"
```

<span data-ttu-id="acd04-223">Hello VM back-end ahora solo es accesible en el puerto *22* y el puerto *3306* de subred de front-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="acd04-223">hello back-end VM is now only accessible on port *22* and port *3306* from hello front-end subnet.</span></span> <span data-ttu-id="acd04-224">El resto del tráfico entrante se bloquea en el grupo de seguridad de red de Hola.</span><span class="sxs-lookup"><span data-stu-id="acd04-224">All other incoming traffic is blocked at hello network security group.</span></span> <span data-ttu-id="acd04-225">Puede ser útil toovisualize las configuraciones de reglas de hello NSG.</span><span class="sxs-lookup"><span data-stu-id="acd04-225">It may be helpful toovisualize hello NSG rule configurations.</span></span> <span data-ttu-id="acd04-226">Configuración de reglas NSG Hola devuelto con hello [lista de reglas de red az](/cli/azure/network/nsg/rule#list) comando.</span><span class="sxs-lookup"><span data-stu-id="acd04-226">Return hello NSG rule configuration with hello [az network rule list](/cli/azure/network/nsg/rule#list) command.</span></span> 

```azurecli-interactive 
az network nsg rule list --resource-group myRGNetwork --nsg-name myNSGBackEnd --output table
```

<span data-ttu-id="acd04-227">Salida:</span><span class="sxs-lookup"><span data-stu-id="acd04-227">Output:</span></span>

```azurecli-interactive 
Access    DestinationAddressPrefix    DestinationPortRange    Direction    Name       Priority  Protocol    ProvisioningState    ResourceGroup    SourceAddressPrefix    SourcePortRange
--------  --------------------------  ----------------------  -----------  -------  ----------  ----------  -------------------  ---------------  ---------------------  -----------------
Allow     *                           22                      Inbound      SSH             100  Tcp         Succeeded            myRGNetwork      10.0.1.0/24            *
Allow     *                           3306                    Inbound      MySQL           200  Tcp         Succeeded            myRGNetwork      10.0.1.0/24            *
Deny      *                           *                       Inbound      denyAll         300  Tcp         Succeeded            myRGNetwork      *                      *
```

## <a name="next-steps"></a><span data-ttu-id="acd04-228">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="acd04-228">Next steps</span></span>

<span data-ttu-id="acd04-229">En este tutorial, ha creado y protege las redes de Azure como máquinas toovirtual relacionados.</span><span class="sxs-lookup"><span data-stu-id="acd04-229">In this tutorial, you created and secured Azure networks as related toovirtual machines.</span></span> <span data-ttu-id="acd04-230">Ha aprendido a:</span><span class="sxs-lookup"><span data-stu-id="acd04-230">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="acd04-231">Implementar una red virtual</span><span class="sxs-lookup"><span data-stu-id="acd04-231">Deploy a virtual network</span></span>
> * <span data-ttu-id="acd04-232">Crear una subred dentro de una red virtual</span><span class="sxs-lookup"><span data-stu-id="acd04-232">Create a subnet within a virtual network</span></span>
> * <span data-ttu-id="acd04-233">Conectar máquinas virtuales tooa subred</span><span class="sxs-lookup"><span data-stu-id="acd04-233">Attach virtual machines tooa subnet</span></span>
> * <span data-ttu-id="acd04-234">Administrar direcciones IP públicas de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="acd04-234">Manage virtual machine public IP addresses</span></span>
> * <span data-ttu-id="acd04-235">Proteger el tráfico entrante de Internet</span><span class="sxs-lookup"><span data-stu-id="acd04-235">Secure incoming internet traffic</span></span>
> * <span data-ttu-id="acd04-236">Proteger el tráfico de tooVM VM</span><span class="sxs-lookup"><span data-stu-id="acd04-236">Secure VM tooVM traffic</span></span>

<span data-ttu-id="acd04-237">Avanzar toohello toolearn de tutorial siguiente sobre la protección de datos en máquinas virtuales mediante copia de seguridad de Azure.</span><span class="sxs-lookup"><span data-stu-id="acd04-237">Advance toohello next tutorial toolearn about securing data on virtual machines using Azure backup.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="acd04-238">Copia de seguridad de máquinas virtuales Linux en Azure</span><span class="sxs-lookup"><span data-stu-id="acd04-238">Back up Linux virtual machines in Azure</span></span>](./tutorial-backup-vms.md)
