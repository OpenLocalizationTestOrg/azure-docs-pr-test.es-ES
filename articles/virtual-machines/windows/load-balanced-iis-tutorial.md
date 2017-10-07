---
title: "aaaTutorial - compilación una aplicación de alta disponibilidad en máquinas virtuales de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate una aplicación segura y de alta disponibilidad a través de tres máquinas virtuales de Windows con un equilibrador de carga en Azure"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 03/30/2017
ms.author: davidmu
ms.openlocfilehash: f9eff96be4f3999651c4108f0334e4eaa1a39c0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-load-balanced-highly-available-application-on-windows-virtual-machines-in-azure"></a><span data-ttu-id="27d2c-103">Compilación de una aplicación de alta disponibilidad y carga equilibrada en máquinas virtuales Windows en Azure</span><span class="sxs-lookup"><span data-stu-id="27d2c-103">Build a load balanced, highly available application on Windows virtual machines in Azure</span></span>

<span data-ttu-id="27d2c-104">En este tutorial, creará una aplicación de alta disponibilidad que sea resistente toomaintenance eventos.</span><span class="sxs-lookup"><span data-stu-id="27d2c-104">In this tutorial, you create a highly available application that is resilient toomaintenance events.</span></span> <span data-ttu-id="27d2c-105">aplicación Hello usa un equilibrador de carga, un conjunto de disponibilidad y tres máquinas virtuales de Windows (VM).</span><span class="sxs-lookup"><span data-stu-id="27d2c-105">hello app uses a load balancer, an availability set, and three Windows virtual machines (VMs).</span></span> <span data-ttu-id="27d2c-106">Este tutorial instala IIS, aunque puede utilizar este tutorial toodeploy un marco de aplicación diferente usando Hola directrices y los mismos componentes de alta disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="27d2c-106">This tutorial installs IIS, though you can use this tutorial toodeploy a different application framework using hello same high availability components and guidelines.</span></span> 

## <a name="step-1---azure-prerequisites"></a><span data-ttu-id="27d2c-107">Paso 1: Requisitos previos de Azure</span><span class="sxs-lookup"><span data-stu-id="27d2c-107">Step 1 - Azure prerequisites</span></span>

<span data-ttu-id="27d2c-108">toocomplete este tutorial, asegúrese de que ha instalado hello más reciente [Azure PowerShell](/powershell/azure/overview) módulo.</span><span class="sxs-lookup"><span data-stu-id="27d2c-108">toocomplete this tutorial, make sure that you have installed hello latest [Azure PowerShell](/powershell/azure/overview) module.</span></span>

<span data-ttu-id="27d2c-109">En primer lugar, inicie sesión en tooyour suscripción de Azure con el comando de inicio de sesión AzureRmAccount hello y siga hello en pantalla instrucciones.</span><span class="sxs-lookup"><span data-stu-id="27d2c-109">First, log in tooyour Azure subscription with hello Login-AzureRmAccount command and follow hello on-screen directions.</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="27d2c-110">Un grupo de recursos de Azure es un contenedor lógico en el que se implementan y se administran los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="27d2c-110">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="27d2c-111">Para poder crear otros recursos de Azure, necesita toocreate un grupo de recursos con [AzureRmResourceGroup nuevo](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="27d2c-111">Before you can create any other Azure resources, you need toocreate a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="27d2c-112">Hello en el ejemplo siguiente se crea un grupo de recursos denominado `myResourceGroup` en hello `westeurope` región:</span><span class="sxs-lookup"><span data-stu-id="27d2c-112">hello following example creates a resource group named `myResourceGroup` in hello `westeurope` region:</span></span> 

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroup -Location westeurope
```

## <a name="step-2---create-availability-set"></a><span data-ttu-id="27d2c-113">Paso 2: Creación de un conjunto de disponibilidad</span><span class="sxs-lookup"><span data-stu-id="27d2c-113">Step 2 - Create availability set</span></span>

<span data-ttu-id="27d2c-114">Las máquinas virtuales se pueden crear en dominios de error lógico y actualización.</span><span class="sxs-lookup"><span data-stu-id="27d2c-114">Virtual machines can be created across logical fault and update domains.</span></span> <span data-ttu-id="27d2c-115">Cada dominio lógico representa una parte del hardware en el centro de datos Azure Hola subyacente.</span><span class="sxs-lookup"><span data-stu-id="27d2c-115">Each logical domain represents a portion of hardware in hello underlying Azure datacenter.</span></span> <span data-ttu-id="27d2c-116">Cuando crea dos o más máquinas virtuales, los recursos de proceso y almacenamiento se distribuyen en estos dominios.</span><span class="sxs-lookup"><span data-stu-id="27d2c-116">When you create two or more VMs, your compute and storage resources are distributed across these domains.</span></span> <span data-ttu-id="27d2c-117">Esta distribución mantiene la disponibilidad de saludo de la aplicación si un componente de hardware necesita mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="27d2c-117">This distribution maintains hello availability of your app if a hardware component needs maintenance.</span></span> <span data-ttu-id="27d2c-118">Los conjuntos de disponibilidad le permiten definir estos dominios de error lógico y actualización.</span><span class="sxs-lookup"><span data-stu-id="27d2c-118">Availability sets let you define these logical fault and update domains.</span></span>

<span data-ttu-id="27d2c-119">Cree un conjunto de disponibilidad con [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span><span class="sxs-lookup"><span data-stu-id="27d2c-119">Create an availability set with [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span></span> <span data-ttu-id="27d2c-120">Hello en el ejemplo siguiente se crea un conjunto con nombre de disponibilidad `myAvailabilitySet`:</span><span class="sxs-lookup"><span data-stu-id="27d2c-120">hello following example creates an availability set named `myAvailabilitySet`:</span></span>

```powershell
$availabilitySet = New-AzureRmAvailabilitySet `
  -ResourceGroupName myResourceGroup `
  -Name myAvailabilitySet `
  -Location westeurope `
  -Managed `
  -PlatformFaultDomainCount 3 `
  -PlatformUpdateDomainCount 2
```

## <a name="step-3---create-load-balancer"></a><span data-ttu-id="27d2c-121">Paso 3: Creación de un equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="27d2c-121">Step 3 - Create load balancer</span></span>

<span data-ttu-id="27d2c-122">Un equilibrador de carga de Azure distribuye el tráfico a través de un conjunto de máquinas virtuales definidas usando reglas de equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="27d2c-122">An Azure load balancer distributes traffic across a set of defined VMs using load balancer rules.</span></span> <span data-ttu-id="27d2c-123">Un sondeo de estado supervisa un puerto determinado en cada máquina virtual y sólo distribuye el tráfico tooan VM operativa.</span><span class="sxs-lookup"><span data-stu-id="27d2c-123">A health probe monitors a given port on each VM and only distributes traffic tooan operational VM.</span></span>

### <a name="create-public-ip-address"></a><span data-ttu-id="27d2c-124">Creación de una dirección IP pública</span><span class="sxs-lookup"><span data-stu-id="27d2c-124">Create public IP address</span></span>

<span data-ttu-id="27d2c-125">tooaccess la aplicación en hello Internet, asignar un equilibrador de carga de toohello de dirección IP público.</span><span class="sxs-lookup"><span data-stu-id="27d2c-125">tooaccess your app on hello Internet, assign a public IP address toohello load balancer.</span></span> <span data-ttu-id="27d2c-126">Cree una dirección IP pública con [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="27d2c-126">Create a public IP address with [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress).</span></span> <span data-ttu-id="27d2c-127">Hello en el ejemplo siguiente se crea una dirección IP pública denominada `myPublicIP`:</span><span class="sxs-lookup"><span data-stu-id="27d2c-127">hello following example creates a public IP address named `myPublicIP`:</span></span>

```powershell
$pip = New-AzureRmPublicIpAddress `
  -ResourceGroupName myResourceGroup `
  -Location westeurope `
  -AllocationMethod Static `
  -Name myPublicIP
```

### <a name="create-load-balancer"></a><span data-ttu-id="27d2c-128">Creación de un equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="27d2c-128">Create load balancer</span></span>

<span data-ttu-id="27d2c-129">Cree una dirección IP de front-end con [New-AzureRmLoadBalancerFrontendIpConfig](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig).</span><span class="sxs-lookup"><span data-stu-id="27d2c-129">Create a frontend IP address with [New-AzureRmLoadBalancerFrontendIpConfig](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig).</span></span> <span data-ttu-id="27d2c-130">Hello en el ejemplo siguiente se crea una dirección IP de front-end denominada `myFrontEndPool`:</span><span class="sxs-lookup"><span data-stu-id="27d2c-130">hello following example creates a frontend IP address named `myFrontEndPool`:</span></span> 

```powershell
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig -Name myFrontEndPool -PublicIpAddress $pip
```

<span data-ttu-id="27d2c-131">Cree un grupo de direcciones de back-end con [New-AzureRmLoadBalancerBackendAddressPoolConfig](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig).</span><span class="sxs-lookup"><span data-stu-id="27d2c-131">Create a backend address pool with [New-AzureRmLoadBalancerBackendAddressPoolConfig](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig).</span></span> <span data-ttu-id="27d2c-132">Hello en el ejemplo siguiente se crea un grupo de direcciones de back-end denominado `myBackEndPool`:</span><span class="sxs-lookup"><span data-stu-id="27d2c-132">hello following example creates a backend address pool named `myBackEndPool`:</span></span>

```powershell
$backendPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name myBackEndPool
```

<span data-ttu-id="27d2c-133">A continuación, cree el equilibrador de carga de hello con [AzureRmLoadBalancer nuevo](/powershell/module/azurerm.network/new-azurermloadbalancer).</span><span class="sxs-lookup"><span data-stu-id="27d2c-133">Now, create hello load balancer with [New-AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer).</span></span> <span data-ttu-id="27d2c-134">Hello en el ejemplo siguiente se crea un equilibrador de carga con el nombre `myLoadBalancer` con hello `myPublicIP` dirección:</span><span class="sxs-lookup"><span data-stu-id="27d2c-134">hello following example creates a load balancer named `myLoadBalancer` using hello `myPublicIP` address:</span></span>

```powershell
$lb = New-AzureRmLoadBalancer `
  -ResourceGroupName myResourceGroup `
  -Name myLoadBalancer `
  -Location westeurope `
  -FrontendIpConfiguration $frontendIP `
  -BackendAddressPool $backendPool
```

### <a name="create-health-probe"></a><span data-ttu-id="27d2c-135">Creación de un sondeo de estado</span><span class="sxs-lookup"><span data-stu-id="27d2c-135">Create health probe</span></span>

<span data-ttu-id="27d2c-136">tooallow Hola equilibrador toomonitor Hola estado de carga de la aplicación, utilice un sondeo de estado.</span><span class="sxs-lookup"><span data-stu-id="27d2c-136">tooallow hello load balancer toomonitor hello status of your app, you use a health probe.</span></span> <span data-ttu-id="27d2c-137">sondeo de estado de Hello dinámicamente agrega o quita las máquinas virtuales de rotación del equilibrador de carga de hello en función de sus comprobaciones de toohealth de respuesta.</span><span class="sxs-lookup"><span data-stu-id="27d2c-137">hello health probe dynamically adds or removes VMs from hello load balancer rotation based on their response toohealth checks.</span></span> <span data-ttu-id="27d2c-138">De forma predeterminada, una máquina virtual se quita de la distribución de equilibrador de carga de hello después de dos errores consecutivos en intervalos de 15 segundos.</span><span class="sxs-lookup"><span data-stu-id="27d2c-138">By default, a VM is removed from hello load balancer distribution after two consecutive failures at 15-second intervals.</span></span>

<span data-ttu-id="27d2c-139">Cree un sondeo de estado con [Add-AzureRmLoadBalancerProbeConfig](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig).</span><span class="sxs-lookup"><span data-stu-id="27d2c-139">Create a health probe with [Add-AzureRmLoadBalancerProbeConfig](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig).</span></span> <span data-ttu-id="27d2c-140">Hello en el ejemplo siguiente se crea un sondeo de estado denominado `myHealthProbe` que supervisa cada máquina virtual:</span><span class="sxs-lookup"><span data-stu-id="27d2c-140">hello following example creates a health probe named `myHealthProbe` that monitors each VM:</span></span>

```powershell
Add-AzureRmLoadBalancerProbeConfig -Name myHealthProbe `
  -LoadBalancer $lb `
  -Protocol tcp `
  -Port 80 `
  -IntervalInSeconds 15 `
  -ProbeCount 2
```

### <a name="create-load-balancer-rule"></a><span data-ttu-id="27d2c-141">Creación de reglas del equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="27d2c-141">Create load balancer rule</span></span>

<span data-ttu-id="27d2c-142">Una regla de equilibrador de carga es toodefine usado cómo tráfico es distribuida toohello máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="27d2c-142">A load balancer rule is used toodefine how traffic is distributed toohello VMs.</span></span>

<span data-ttu-id="27d2c-143">Cree una regla del equilibrador de carga con [Add-AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig).</span><span class="sxs-lookup"><span data-stu-id="27d2c-143">Create a load balancer rule with [Add-AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig).</span></span> <span data-ttu-id="27d2c-144">Hello en el ejemplo siguiente se crea una regla de equilibrador de carga denominada `myLoadBalancerRule` y equilibra el tráfico en el puerto `80`:</span><span class="sxs-lookup"><span data-stu-id="27d2c-144">hello following example creates a load balancer rule named `myLoadBalancerRule` and balances traffic on port `80`:</span></span>

```powershell
Add-AzureRmLoadBalancerRuleConfig -Name myLoadBalancerRule `
  -LoadBalancer $lb `
  -FrontendIpConfiguration $lb.FrontendIpConfigurations[0] `
  -BackendAddressPool $lb.BackendAddressPools[0] `
  -Protocol Tcp `
  -FrontendPort 80 `
  -BackendPort 80
```

<span data-ttu-id="27d2c-145">Actualizar el equilibrador de carga de hello con [AzureRmLoadBalancer conjunto](/powershell/module/azurerm.network/set-azurermloadbalancer):</span><span class="sxs-lookup"><span data-stu-id="27d2c-145">Update hello load balancer with [Set-AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):</span></span>

```powershell
Set-AzureRmLoadBalancer -LoadBalancer $lb
```

## <a name="step-4---configure-networking"></a><span data-ttu-id="27d2c-146">Paso 4: Configuración de las redes</span><span class="sxs-lookup"><span data-stu-id="27d2c-146">Step 4 - Configure networking</span></span>

<span data-ttu-id="27d2c-147">Cada máquina virtual tiene uno o más virtual tarjetas de red (NIC) que se conectan tooa de red virtual.</span><span class="sxs-lookup"><span data-stu-id="27d2c-147">Each VM has one or more virtual network interface cards (NICs) that connect tooa virtual network.</span></span> <span data-ttu-id="27d2c-148">Esta red virtual se protege el tráfico toofilter basándose en reglas de acceso definidas.</span><span class="sxs-lookup"><span data-stu-id="27d2c-148">This virtual network is secured toofilter traffic based on defined access rules.</span></span>

### <a name="create-virtual-network"></a><span data-ttu-id="27d2c-149">Creación de una red virtual</span><span class="sxs-lookup"><span data-stu-id="27d2c-149">Create virtual network</span></span>

<span data-ttu-id="27d2c-150">Primero, cree una subred con [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig).</span><span class="sxs-lookup"><span data-stu-id="27d2c-150">First, configure a subnet with [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig).</span></span> <span data-ttu-id="27d2c-151">Hello en el ejemplo siguiente se crea una subred denominada `mySubnet`:</span><span class="sxs-lookup"><span data-stu-id="27d2c-151">hello following example creates a subnet named `mySubnet`:</span></span>

```powershell
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name mySubnet -AddressPrefix 192.168.1.0/24
```

<span data-ttu-id="27d2c-152">tooyour de conectividad de red de tooprovide las máquinas virtuales, cree una red virtual con [AzureRmVirtualNetwork nuevo](/powershell/module/azurerm.network/new-azurermvirtualnetwork).</span><span class="sxs-lookup"><span data-stu-id="27d2c-152">tooprovide network connectivity tooyour VMs, create a virtual network with [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork).</span></span> <span data-ttu-id="27d2c-153">Hello en el ejemplo siguiente se crea una red virtual denominada `myVnet` con `mySubnet`:</span><span class="sxs-lookup"><span data-stu-id="27d2c-153">hello following example creates a virtual network named `myVnet` with `mySubnet`:</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myResourceGroup `
  -Location westeurope `
  -Name myVnet `
  -AddressPrefix 192.168.0.0/16 `
  -Subnet $subnetConfig
```

### <a name="configure-network-security"></a><span data-ttu-id="27d2c-154">Configuración de la seguridad de red</span><span class="sxs-lookup"><span data-stu-id="27d2c-154">Configure network security</span></span>

<span data-ttu-id="27d2c-155">Un [grupo de seguridad de red](../../virtual-network/virtual-networks-nsg.md) de Azure controla el tráfico entrante y saliente para una o varias máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="27d2c-155">An Azure [network security group](../../virtual-network/virtual-networks-nsg.md) (NSG) controls inbound and outbound traffic for one or many virtual machines.</span></span> <span data-ttu-id="27d2c-156">Las reglas del grupo de seguridad de red permiten o deniegan el tráfico de red en un puerto específico o en un intervalo de puertos.</span><span class="sxs-lookup"><span data-stu-id="27d2c-156">Network security group rules allow or deny network traffic on a specific port or port range.</span></span> <span data-ttu-id="27d2c-157">Estas reglas también pueden incluir un prefijo de dirección de origen para que solo el tráfico que se origine en un origen predefinido pueda comunicarse con una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="27d2c-157">These rules can also include a source address prefix so that only traffic originating at a predefined source can communicate with a virtual machine.</span></span>

<span data-ttu-id="27d2c-158">tooallow web tooreach de tráfico de la aplicación, cree una regla de grupo de seguridad de red con [AzureRmNetworkSecurityRuleConfig nuevo](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig).</span><span class="sxs-lookup"><span data-stu-id="27d2c-158">tooallow web traffic tooreach your app, create a network security group rule with [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig).</span></span> <span data-ttu-id="27d2c-159">Hello en el ejemplo siguiente se crea una regla de grupo de seguridad de red denominada `myNetworkSecurityGroupRule`:</span><span class="sxs-lookup"><span data-stu-id="27d2c-159">hello following example creates a network security group rule named `myNetworkSecurityGroupRule`:</span></span>

```powershell
$nsgRule = New-AzureRmNetworkSecurityRuleConfig `
  -Name myNetworkSecurityGroupRule `
  -Protocol Tcp `
  -Direction Inbound `
  -Priority 1001 `
  -SourceAddressPrefix * `
  -SourcePortRange * `
  -DestinationAddressPrefix * `
  -DestinationPortRange 80 `
  -Access Allow
```

<span data-ttu-id="27d2c-160">Cree un grupo de seguridad de red con [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup).</span><span class="sxs-lookup"><span data-stu-id="27d2c-160">Create a network security group with [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup).</span></span> <span data-ttu-id="27d2c-161">Hello en el ejemplo siguiente se crea un NSG denominado `myNetworkSecurityGroup`:</span><span class="sxs-lookup"><span data-stu-id="27d2c-161">hello following example creates an NSG named `myNetworkSecurityGroup`:</span></span>

```powershell
$nsg = New-AzureRmNetworkSecurityGroup `
  -ResourceGroupName myResourceGroup `
  -Location westeurope `
  -Name myNetworkSecurityGroup `
  -SecurityRules $nsgRule
```

<span data-ttu-id="27d2c-162">Agregar subred toohello grupo de seguridad de red de hello con [AzureRmVirtualNetworkSubnetConfig conjunto](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig):</span><span class="sxs-lookup"><span data-stu-id="27d2c-162">Add hello network security group toohello subnet with [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig):</span></span>

```powershell
Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet `
  -Name mySubnet `
  -NetworkSecurityGroup $nsg `
  -AddressPrefix 192.168.1.0/24
```

<span data-ttu-id="27d2c-163">Red virtual de Hola de actualización con [AzureRmVirtualNetwork conjunto](/powershell/module/azurerm.network/set-azurermvirtualnetwork):</span><span class="sxs-lookup"><span data-stu-id="27d2c-163">Update hello virtual network with [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork):</span></span>

```powershell
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```

### <a name="create-virtual-network-interface-cards"></a><span data-ttu-id="27d2c-164">Creación de las tarjetas de interfaz de red virtual</span><span class="sxs-lookup"><span data-stu-id="27d2c-164">Create virtual network interface cards</span></span>

<span data-ttu-id="27d2c-165">Cargar la función equilibradores con recursos NIC virtual hello en lugar de Hola VM real.</span><span class="sxs-lookup"><span data-stu-id="27d2c-165">Load balancers function with hello virtual NIC resource rather than hello actual VM.</span></span> <span data-ttu-id="27d2c-166">Hello NIC virtual está conectado toohello equilibrador de carga y, a continuación, asociará tooa máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="27d2c-166">hello virtual NIC is connected toohello load balancer, and then attached tooa VM.</span></span>

<span data-ttu-id="27d2c-167">Cree una NIC virtual con [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span><span class="sxs-lookup"><span data-stu-id="27d2c-167">Create a virtual NIC with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span></span> <span data-ttu-id="27d2c-168">Hello en el ejemplo siguiente se crea tres NIC virtuales.</span><span class="sxs-lookup"><span data-stu-id="27d2c-168">hello following example creates three virtual NICs.</span></span> <span data-ttu-id="27d2c-169">(Una NIC virtual para cada máquina virtual debe crear para la aplicación Hola siguiendo los pasos):</span><span class="sxs-lookup"><span data-stu-id="27d2c-169">(One virtual NIC for each VM you create for your app in hello following steps):</span></span>


```powershell
for ($i=1; $i -le 3; $i++)
{
   New-AzureRmNetworkInterface -ResourceGroupName myResourceGroup `
     -Name myNic$i `
     -Location westeurope `
     -Subnet $vnet.Subnets[0] `
     -LoadBalancerBackendAddressPool $lb.BackendAddressPools[0]
}

```

## <a name="step-5---create-virtual-machines"></a><span data-ttu-id="27d2c-170">Paso 5: Creación de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="27d2c-170">Step 5 - Create virtual machines</span></span>

<span data-ttu-id="27d2c-171">Con todos los hello subyacente componentes en su lugar, ahora puede crear toorun de máquinas virtuales de alta disponibilidad la aplicación.</span><span class="sxs-lookup"><span data-stu-id="27d2c-171">With all hello underlying components in place, you can now create highly available VMs toorun your app.</span></span> 

<span data-ttu-id="27d2c-172">Obtener nombre de usuario de Hola y la contraseña necesarios para la cuenta de administrador de hello en hello la máquina virtual con [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span><span class="sxs-lookup"><span data-stu-id="27d2c-172">Get hello username and password needed for hello administrator account on hello virtual machine with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="27d2c-173">Crear máquinas virtuales de hello con [New-AzureRmVMConfig](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/new-azurermvmconfig), [AzureRmVMOperatingSystem conjunto](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmoperatingsystem), [conjunto AzureRmVMSourceImage](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmsourceimage), [Set-AzureRmVMOSDisk](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmosdisk), [AzureRmVMNetworkInterface agregar](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/add-azurermvmnetworkinterface), y [nueva AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="27d2c-173">Create hello VMs with [New-AzureRmVMConfig](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/new-azurermvmconfig), [Set-AzureRmVMOperatingSystem](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmoperatingsystem), [Set-AzureRmVMSourceImage](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmsourceimage), [Set-AzureRmVMOSDisk](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmosdisk), [Add-AzureRmVMNetworkInterface](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/add-azurermvmnetworkinterface), and [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> <span data-ttu-id="27d2c-174">Hola siguiente ejemplo crea tres máquinas virtuales:</span><span class="sxs-lookup"><span data-stu-id="27d2c-174">hello following example creates three VMs:</span></span>

```powershell
for ($i=1; $i -le 3; $i++)
{
   $vm = New-AzureRmVMConfig -VMName myVM$i -VMSize Standard_D1 -AvailabilitySetId $availabilitySet.Id
   $vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName myVM$i -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
   $vm = Set-AzureRmVMSourceImage -VM $vm -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2016-Datacenter -Version latest
   $vm = Set-AzureRmVMOSDisk -VM $vm -Name myOsDisk$i -StorageAccountType StandardLRS -DiskSizeInGB 128 -CreateOption FromImage -Caching ReadWrite
   $nic = Get-AzureRmNetworkInterface -ResourceGroupName myResourceGroup -Name myNic$i
   $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
   New-AzureRmVM -ResourceGroupName myResourceGroup -Location westeurope -VM $vm
}

```

<span data-ttu-id="27d2c-175">Toma varios toocreate minutos y configurar todas las tres máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="27d2c-175">It takes several minutes toocreate and configure all three VMs.</span></span> <span data-ttu-id="27d2c-176">Hello sondeo de estado del equilibrador de carga detecta automáticamente cuando se ejecuta la aplicación hello en cada máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="27d2c-176">hello load balancer health probe automatically detects when hello app is running on each VM.</span></span> <span data-ttu-id="27d2c-177">Una vez que se ejecuta la aplicación hello, regla de equilibrador de carga de hello inicia toodistribute tráfico.</span><span class="sxs-lookup"><span data-stu-id="27d2c-177">Once hello app is running, hello load balancer rule starts toodistribute traffic.</span></span>

### <a name="install-hello-app"></a><span data-ttu-id="27d2c-178">Instalar la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="27d2c-178">Install hello app</span></span> 

<span data-ttu-id="27d2c-179">Las extensiones de máquina virtual de Azure son tareas de configuración de máquina virtual de tooautomate usado como instalar aplicaciones y configurar el sistema operativo de Hola.</span><span class="sxs-lookup"><span data-stu-id="27d2c-179">Azure virtual machine extensions are used tooautomate virtual machine configuration tasks such as installing applications and configuring hello operating system.</span></span> <span data-ttu-id="27d2c-180">Hola [extensión de script personalizado para Windows](./../virtual-machines-windows-extensions-customscript.md) es toorun usa cualquier script de PowerShell en la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="27d2c-180">hello [custom script extension for Windows](./../virtual-machines-windows-extensions-customscript.md) is used toorun any PowerShell script on hello virtual machine.</span></span> <span data-ttu-id="27d2c-181">script de Hola se pueda almacenar en almacenamiento de Azure, cualquier extremo HTTP accesible, o incrustado en la configuración de la extensión de hello secuencia de comandos personalizada.</span><span class="sxs-lookup"><span data-stu-id="27d2c-181">hello script can be stored in Azure storage, any accessible HTTP endpoint, or embedded in hello custom script extension configuration.</span></span> <span data-ttu-id="27d2c-182">Cuando se utiliza la extensión de script personalizado de hello, agente de máquina virtual de Azure de hello administra la ejecución de script de Hola.</span><span class="sxs-lookup"><span data-stu-id="27d2c-182">When using hello custom script extension, hello Azure VM agent manages hello script execution.</span></span>

<span data-ttu-id="27d2c-183">Use [AzureRmVMExtension conjunto](/powershell/module/azurerm.compute/set-azurermvmextension) extensión de script personalizado de tooinstall Hola.</span><span class="sxs-lookup"><span data-stu-id="27d2c-183">Use [Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) tooinstall hello custom script extension.</span></span> <span data-ttu-id="27d2c-184">Hola se ejecuta la extensión `powershell Add-WindowsFeature Web-Server` servidor Web IIS de Hola tooinstall:</span><span class="sxs-lookup"><span data-stu-id="27d2c-184">hello extension runs `powershell Add-WindowsFeature Web-Server` tooinstall hello IIS webserver:</span></span>

```powershell
for ($i=1; $i -le 3; $i++)
{
   Set-AzureRmVMExtension -ResourceGroupName myResourceGroup `
     -ExtensionName IIS `
     -VMName myVM$i `
     -Publisher Microsoft.Compute `
     -ExtensionType CustomScriptExtension `
     -TypeHandlerVersion 1.4 `
     -SettingString '{"commandToExecute":"powershell Add-WindowsFeature Web-Server"}' `
     -Location westeurope
}
```

### <a name="test-your-app"></a><span data-ttu-id="27d2c-185">Prueba de la aplicación</span><span class="sxs-lookup"><span data-stu-id="27d2c-185">Test your app</span></span>

<span data-ttu-id="27d2c-186">Obtener dirección IP pública de Hola de un equilibrador de carga con [AzureRmPublicIPAddress Get](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="27d2c-186">Obtain hello public IP address of your load balancer with [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="27d2c-187">Hello en el ejemplo siguiente se obtiene la dirección IP de Hola para `myPublicIP` creado anteriormente:</span><span class="sxs-lookup"><span data-stu-id="27d2c-187">hello following example obtains hello IP address for `myPublicIP` created earlier:</span></span>

```powershell
Get-AzureRmPublicIPAddress -ResourceGroupName myResourceGroup -Name myPublicIP | select IpAddress
```

<span data-ttu-id="27d2c-188">Escriba la dirección IP pública hello en el Explorador de web tooa.</span><span class="sxs-lookup"><span data-stu-id="27d2c-188">Enter hello public IP address in tooa web browser.</span></span> <span data-ttu-id="27d2c-189">Con la regla NSG hello en su lugar, se muestra el sitio Web IIS de hello predeterminado.</span><span class="sxs-lookup"><span data-stu-id="27d2c-189">With hello NSG rule in place, hello default IIS website is displayed.</span></span> 

![Sitio predeterminado de IIS](media/load-balanced-iis-tutorial/iis.png)

## <a name="step-6--management-tasks"></a><span data-ttu-id="27d2c-191">Paso 6: Tareas de administración</span><span class="sxs-lookup"><span data-stu-id="27d2c-191">Step 6 – Management tasks</span></span>

<span data-ttu-id="27d2c-192">Puede que necesite tooperform mantenimiento en hello máquinas virtuales que ejecutan la aplicación, como la instalación de actualizaciones del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="27d2c-192">You may need tooperform maintenance on hello VMs running your app, such as installing OS updates.</span></span> <span data-ttu-id="27d2c-193">toodeal con un aumento del tráfico tooyour aplicación, puede que necesite tooadd máquinas virtuales adicionales.</span><span class="sxs-lookup"><span data-stu-id="27d2c-193">toodeal with increased traffic tooyour app, you may need tooadd additional VMs.</span></span> <span data-ttu-id="27d2c-194">Esta sección muestra cómo tooremove o agregar una máquina virtual desde el equilibrador de carga de Hola.</span><span class="sxs-lookup"><span data-stu-id="27d2c-194">This section shows you how tooremove or add a VM from hello load balancer.</span></span> 

### <a name="remove-a-vm-from-hello-load-balancer"></a><span data-ttu-id="27d2c-195">Quitar una máquina virtual de equilibrador de carga de Hola</span><span class="sxs-lookup"><span data-stu-id="27d2c-195">Remove a VM from hello load balancer</span></span>

<span data-ttu-id="27d2c-196">Quitar una máquina virtual del grupo de direcciones de back-end de hello mediante el restablecimiento de la propiedad de LoadBalancerBackendAddressPools Hola de tarjeta de interfaz de red de Hola.</span><span class="sxs-lookup"><span data-stu-id="27d2c-196">Remove a VM from hello backend address pool by resetting hello LoadBalancerBackendAddressPools property of hello network interface card.</span></span>

<span data-ttu-id="27d2c-197">Obtener la tarjeta de interfaz de red de hello con [AzureRmNetworkInterface Get](/powershell/module/azurerm.network/get-azurermnetworkinterface):</span><span class="sxs-lookup"><span data-stu-id="27d2c-197">Get hello network interface card with [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface):</span></span>

```powershell
$nic = Get-AzureRmNetworkInterface -ResourceGroupName myResourceGroup -Name myNic2
``` 

<span data-ttu-id="27d2c-198">Establecer la propiedad de LoadBalancerBackendAddressPools de Hola de tarjeta de interfaz de red de hello demasiado null$:</span><span class="sxs-lookup"><span data-stu-id="27d2c-198">Set hello LoadBalancerBackendAddressPools property of hello network interface card too$null:</span></span>

```powershell
$nic.Ipconfigurations[0].LoadBalancerBackendAddressPools=$null
```

<span data-ttu-id="27d2c-199">Tarjeta de interfaz de red de Hola de actualización:</span><span class="sxs-lookup"><span data-stu-id="27d2c-199">Update hello network interface card:</span></span>

```powershell
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

### <a name="add-a-vm-toohello-load-balancer"></a><span data-ttu-id="27d2c-200">Agregar un equilibrador de carga de toohello VM</span><span class="sxs-lookup"><span data-stu-id="27d2c-200">Add a VM toohello load balancer</span></span>

<span data-ttu-id="27d2c-201">Después de realizar el mantenimiento de la máquina virtual o si necesita capacidad de tooexpand, agregar Hola NIC de un grupo de direcciones de back-end VM toohello Hola de equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="27d2c-201">After performing VM maintenance, or if you need tooexpand capacity, adding hello NIC of a VM toohello backend address pool of hello load balancer.</span></span>

<span data-ttu-id="27d2c-202">Obtener el equilibrador de carga de hello:</span><span class="sxs-lookup"><span data-stu-id="27d2c-202">Get hello load balancer:</span></span>

```powershell
$lb = Get-AzureRMLoadBalancer -ResourceGroupName myResourceGroup -Name myLoadBalancer 
```

<span data-ttu-id="27d2c-203">Agregar grupo de direcciones de back-end de Hola de tarjeta de interfaz de red de toohello equilibrador de carga de hello:</span><span class="sxs-lookup"><span data-stu-id="27d2c-203">Add hello backend address pool of hello load balancer toohello network interface card:</span></span>

```powershell
$nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$lb.BackendAddressPools[0]
```

<span data-ttu-id="27d2c-204">Tarjeta de interfaz de red de Hola de actualización:</span><span class="sxs-lookup"><span data-stu-id="27d2c-204">Update hello network interface card:</span></span>

```powershell
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

## <a name="next-steps"></a><span data-ttu-id="27d2c-205">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="27d2c-205">Next Steps</span></span>

<span data-ttu-id="27d2c-206">Ejemplos – [Scripts de ejemplo de Azure Virtual Machine PowerShell](./../virtual-machines-windows-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="27d2c-206">Samples – [Azure Virtual Machine PowerShell sample scripts](./../virtual-machines-windows-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>
