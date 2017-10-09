---
title: "aaaCreate un conjuntos para Windows de máquina Virtual de escala en Azure | Documentos de Microsoft"
description: "Creación e implementación de una aplicación de alta disponibilidad en VM Windows con un conjunto de escalado de máquinas virtuales"
services: virtual-machine-scale-sets
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: 
ms.topic: article
ms.date: 08/11/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: a3914571005c28a492c069d880992630851afae7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-scale-set-and-deploy-a-highly-available-app-on-windows"></a><span data-ttu-id="5d5f7-103">Creación de un conjunto de escalado de máquinas virtuales e implementación de una aplicación de alta disponibilidad en Windows</span><span class="sxs-lookup"><span data-stu-id="5d5f7-103">Create a Virtual Machine Scale Set and deploy a highly available app on Windows</span></span>
<span data-ttu-id="5d5f7-104">Un conjunto de escalas de máquina virtual permite toodeploy y administrar un conjunto de máquinas virtuales idénticos, la escala automática.</span><span class="sxs-lookup"><span data-stu-id="5d5f7-104">A virtual machine scale set allows you toodeploy and manage a set of identical, auto-scaling virtual machines.</span></span> <span data-ttu-id="5d5f7-105">Puede escalar el número de Hola de máquinas virtuales en el conjunto de escalas de hello manualmente, o definir tooautoscale reglas en función de uso de CPU, la demanda de memoria o el tráfico de red.</span><span class="sxs-lookup"><span data-stu-id="5d5f7-105">You can scale hello number of VMs in hello scale set manually, or define rules tooautoscale based on CPU usage, memory demand, or network traffic.</span></span> <span data-ttu-id="5d5f7-106">En este tutorial, implementará un conjunto de escalado de máquinas virtuales en Azure.</span><span class="sxs-lookup"><span data-stu-id="5d5f7-106">In this tutorial, you deploy a virtual machine scale set in Azure.</span></span> <span data-ttu-id="5d5f7-107">Aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="5d5f7-107">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="5d5f7-108">Usar la extensión de Script personalizado de hello toodefine un tooscale de sitio IIS</span><span class="sxs-lookup"><span data-stu-id="5d5f7-108">Use hello Custom Script Extension toodefine an IIS site tooscale</span></span>
> * <span data-ttu-id="5d5f7-109">Crear un equilibrador de carga para el conjunto de escalado</span><span class="sxs-lookup"><span data-stu-id="5d5f7-109">Create a load balancer for your scale set</span></span>
> * <span data-ttu-id="5d5f7-110">Crear un conjunto de escalado de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="5d5f7-110">Create a virtual machine scale set</span></span>
> * <span data-ttu-id="5d5f7-111">Aumentar o disminuir el número de Hola de instancias de un conjunto de escala</span><span class="sxs-lookup"><span data-stu-id="5d5f7-111">Increase or decrease hello number of instances in a scale set</span></span>
> * <span data-ttu-id="5d5f7-112">Crear reglas de escalado automático</span><span class="sxs-lookup"><span data-stu-id="5d5f7-112">Create autoscale rules</span></span>

<span data-ttu-id="5d5f7-113">Este tutorial requiere hello Azure PowerShell versión 3.6 o posterior del módulo.</span><span class="sxs-lookup"><span data-stu-id="5d5f7-113">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="5d5f7-114">Ejecutar ` Get-Module -ListAvailable AzureRM` toofind versión de Hola.</span><span class="sxs-lookup"><span data-stu-id="5d5f7-114">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="5d5f7-115">Si necesita tooupgrade, consulte [módulo instalar Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="5d5f7-115">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>


## <a name="scale-set-overview"></a><span data-ttu-id="5d5f7-116">Introducción al conjunto de escalado</span><span class="sxs-lookup"><span data-stu-id="5d5f7-116">Scale Set overview</span></span>
<span data-ttu-id="5d5f7-117">Conjuntos de escalas de utilizan conceptos similares, tal y como ha aprendido en el tutorial anterior Hola demasiado[crear máquinas virtuales de alta disponibilidad](tutorial-availability-sets.md).</span><span class="sxs-lookup"><span data-stu-id="5d5f7-117">Scale sets use similar concepts as you learned about in hello previous tutorial too[Create highly available VMs](tutorial-availability-sets.md).</span></span> <span data-ttu-id="5d5f7-118">Las VM de un conjunto de escalado se distribuyen entre los dominios de error y actualización como las VM en un conjunto de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="5d5f7-118">VMs in a scale set are distributed across fault and update domains just like VMs in an availability set.</span></span>

<span data-ttu-id="5d5f7-119">Las máquinas virtuales se crean según sea necesario en un conjunto de escalado.</span><span class="sxs-lookup"><span data-stu-id="5d5f7-119">VMs are created as needed in a scale set.</span></span> <span data-ttu-id="5d5f7-120">Definir toocontrol de reglas de escalado automático cómo y cuándo se agregan o se quitan del conjunto de escalas de hello las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="5d5f7-120">You define autoscale rules toocontrol how and when VMs are added or removed from hello scale set.</span></span> <span data-ttu-id="5d5f7-121">Estas reglas se pueden desencadenar en función de métricas como la carga de la CPU, el uso de la memoria o el tráfico de red.</span><span class="sxs-lookup"><span data-stu-id="5d5f7-121">These rules can trigger based on metrics such as CPU load, memory usage, or network traffic.</span></span>

<span data-ttu-id="5d5f7-122">Escala establece compatibilidad con seguridad too1, 000 máquinas virtuales cuando se usa una imagen de la plataforma Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="5d5f7-122">Scale sets support up too1,000 VMs when you use an Azure platform image.</span></span> <span data-ttu-id="5d5f7-123">Para las cargas de trabajo con importantes de instalación o los requisitos de personalización de máquina virtual, es recomendable demasiado[crear una imagen de máquina virtual personalizada](tutorial-custom-images.md).</span><span class="sxs-lookup"><span data-stu-id="5d5f7-123">For workloads with significant installation or VM customization requirements, you may wish too[Create a custom VM image](tutorial-custom-images.md).</span></span> <span data-ttu-id="5d5f7-124">Puede crear las máquinas virtuales de too100 en una escala establecida cuando se usa una imagen personalizada.</span><span class="sxs-lookup"><span data-stu-id="5d5f7-124">You can create up too100 VMs in a scale set when using a custom image.</span></span>


## <a name="create-an-app-tooscale"></a><span data-ttu-id="5d5f7-125">Crear una aplicación tooscale</span><span class="sxs-lookup"><span data-stu-id="5d5f7-125">Create an app tooscale</span></span>
<span data-ttu-id="5d5f7-126">Antes de poder crear un conjunto de escalado, cree un grupo de recursos con [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="5d5f7-126">Before you can create a scale set, create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="5d5f7-127">Hello en el ejemplo siguiente se crea un grupo de recursos denominado *myResourceGroupAutomate* en hello *EastUS* ubicación:</span><span class="sxs-lookup"><span data-stu-id="5d5f7-127">hello following example creates a resource group named *myResourceGroupAutomate* in hello *EastUS* location:</span></span>

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroupScaleSet -Location EastUS
```

<span data-ttu-id="5d5f7-128">En un tutorial anterior, ha aprendido cómo demasiado[configuración de máquina virtual automatizar](tutorial-automate-vm-deployment.md) utilizando Hola extensión de Script personalizado.</span><span class="sxs-lookup"><span data-stu-id="5d5f7-128">In an earlier tutorial, you learned how too[Automate VM configuration](tutorial-automate-vm-deployment.md) using hello Custom Script Extension.</span></span> <span data-ttu-id="5d5f7-129">Crear la configuración de un conjunto de escala, a continuación, aplicar un tooinstall de extensión de Script personalizado y configurar IIS:</span><span class="sxs-lookup"><span data-stu-id="5d5f7-129">Create a scale set configuration then apply a Custom Script Extension tooinstall and configure IIS:</span></span>

```powershell
# Create a config object
$vmssConfig = New-AzureRmVmssConfig `
    -Location EastUS `
    -SkuCapacity 2 `
    -SkuName Standard_DS2 `
    -UpgradePolicyMode Automatic

# Define hello script for your Custom Script Extension toorun
$publicSettings = @{
    "fileUris" = (,"https://raw.githubusercontent.com/iainfoulds/azure-samples/master/automate-iis.ps1");
    "commandToExecute" = "powershell -ExecutionPolicy Unrestricted -File automate-iis.ps1"
}

# Use Custom Script Extension tooinstall IIS and configure basic website
Add-AzureRmVmssExtension -VirtualMachineScaleSet $vmssConfig `
    -Name "customScript" `
    -Publisher "Microsoft.Compute" `
    -Type "CustomScriptExtension" `
    -TypeHandlerVersion 1.8 `
    -Setting $publicSettings
```

## <a name="create-scale-load-balancer"></a><span data-ttu-id="5d5f7-130">Creación de un equilibrador de carga de escalado</span><span class="sxs-lookup"><span data-stu-id="5d5f7-130">Create scale load balancer</span></span>
<span data-ttu-id="5d5f7-131">Un equilibrador de carga de Azure es un equilibrador de carga de nivel 4 (TCP, UDP) que proporciona una alta disponibilidad mediante la distribución del tráfico entrante entre máquinas virtuales con un estado correcto.</span><span class="sxs-lookup"><span data-stu-id="5d5f7-131">An Azure load balancer is a Layer-4 (TCP, UDP) load balancer that provides high availability by distributing incoming traffic among healthy VMs.</span></span> <span data-ttu-id="5d5f7-132">Un sondeo de estado de equilibrador de carga supervisa un puerto determinado en cada máquina virtual y sólo distribuye el tráfico tooan VM operativa.</span><span class="sxs-lookup"><span data-stu-id="5d5f7-132">A load balancer health probe monitors a given port on each VM and only distributes traffic tooan operational VM.</span></span> <span data-ttu-id="5d5f7-133">Para obtener más información, vea el tutorial siguiente hello en [cómo tooload equilibrar máquinas virtuales de Windows](tutorial-load-balancer.md).</span><span class="sxs-lookup"><span data-stu-id="5d5f7-133">For more information, see hello next tutorial on [How tooload balance Windows virtual machines](tutorial-load-balancer.md).</span></span>

<span data-ttu-id="5d5f7-134">Cree un equilibrador de carga que tenga una dirección IP pública y distribuye el tráfico web en el puerto 80:</span><span class="sxs-lookup"><span data-stu-id="5d5f7-134">Create a load balancer that has a public IP address and distributes web traffic on port 80:</span></span>

```powershell
# Create a public IP address
$publicIP = New-AzureRmPublicIpAddress `
  -ResourceGroupName myResourceGroupScaleSet `
  -Location EastUS `
  -AllocationMethod Static `
  -Name myPublicIP

# Create a frontend and backend IP pool
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig `
  -Name myFrontEndPool `
  -PublicIpAddress $publicIP
$backendPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name myBackEndPool

# Create hello load balancer
$lb = New-AzureRmLoadBalancer `
  -ResourceGroupName myResourceGroupScaleSet `
  -Name myLoadBalancer `
  -Location EastUS `
  -FrontendIpConfiguration $frontendIP `
  -BackendAddressPool $backendPool

# Create a load balancer health probe on port 80
Add-AzureRmLoadBalancerProbeConfig -Name myHealthProbe `
  -LoadBalancer $lb `
  -Protocol tcp `
  -Port 80 `
  -IntervalInSeconds 15 `
  -ProbeCount 2

# Create a load balancer rule toodistribute traffic on port 80
Add-AzureRmLoadBalancerRuleConfig `
  -Name myLoadBalancerRule `
  -LoadBalancer $lb `
  -FrontendIpConfiguration $lb.FrontendIpConfigurations[0] `
  -BackendAddressPool $lb.BackendAddressPools[0] `
  -Protocol Tcp `
  -FrontendPort 80 `
  -BackendPort 80

# Update hello load balancer configuration
Set-AzureRmLoadBalancer -LoadBalancer $lb
```

## <a name="create-a-scale-set"></a><span data-ttu-id="5d5f7-135">Creación de un conjunto de escalado</span><span class="sxs-lookup"><span data-stu-id="5d5f7-135">Create a scale set</span></span>
<span data-ttu-id="5d5f7-136">Ahora, cree un conjunto de escalado de máquinas virtuales con [New-AzureRmVmss](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="5d5f7-136">Now create a virtual machine scale set with [New-AzureRmVmss](/powershell/module/azurerm.compute/new-azurermvm).</span></span> <span data-ttu-id="5d5f7-137">Hello en el ejemplo siguiente se crea un conjunto con nombre de escalas *myScaleSet*:</span><span class="sxs-lookup"><span data-stu-id="5d5f7-137">hello following example creates a scale set named *myScaleSet*:</span></span>

```powershell
# Reference a virtual machine image from hello gallery
Set-AzureRmVmssStorageProfile $vmssConfig `
  -ImageReferencePublisher MicrosoftWindowsServer `
  -ImageReferenceOffer WindowsServer `
  -ImageReferenceSku 2016-Datacenter `
  -ImageReferenceVersion latest

# Set up information for authenticating with hello virtual machine
Set-AzureRmVmssOsProfile $vmssConfig `
  -AdminUsername azureuser `
  -AdminPassword P@ssword! `
  -ComputerNamePrefix myVM

# Create hello virtual network resources
$subnet = New-AzureRmVirtualNetworkSubnetConfig `
  -Name "mySubnet" `
  -AddressPrefix 10.0.0.0/24
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName "myResourceGroupScaleSet" `
  -Name "myVnet" `
  -Location "EastUS" `
  -AddressPrefix 10.0.0.0/16 `
  -Subnet $subnet
$ipConfig = New-AzureRmVmssIpConfig `
  -Name "myIPConfig" `
  -LoadBalancerBackendAddressPoolsId $lb.BackendAddressPools[0].Id `
  -SubnetId $vnet.Subnets[0].Id

# Attach hello virtual network toohello config object
Add-AzureRmVmssNetworkInterfaceConfiguration `
  -VirtualMachineScaleSet $vmssConfig `
  -Name "network-config" `
  -Primary $true `
  -IPConfiguration $ipConfig

# Create hello scale set with hello config object (this step might take a few minutes)
New-AzureRmVmss `
  -ResourceGroupName myResourceGroupScaleSet `
  -Name myScaleSet `
  -VirtualMachineScaleSet $vmssConfig
```

<span data-ttu-id="5d5f7-138">Toma toocreate unos minutos y configurará todos los recursos de conjunto de escala de Hola y máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="5d5f7-138">It takes a few minutes toocreate and configure all hello scale set resources and VMs.</span></span>


## <a name="test-your-app"></a><span data-ttu-id="5d5f7-139">Prueba de la aplicación</span><span class="sxs-lookup"><span data-stu-id="5d5f7-139">Test your app</span></span>
<span data-ttu-id="5d5f7-140">toosee el sitio Web IIS en acción, obtener la dirección IP pública de Hola de un equilibrador de carga con [AzureRmPublicIPAddress Get](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="5d5f7-140">toosee your IIS website in action, obtain hello public IP address of your load balancer with [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="5d5f7-141">Hello en el ejemplo siguiente se obtiene la dirección IP de Hola para *myPublicIP* creado como parte del conjunto de escalas de hello:</span><span class="sxs-lookup"><span data-stu-id="5d5f7-141">hello following example obtains hello IP address for *myPublicIP* created as part of hello scale set:</span></span>

```powershell
Get-AzureRmPublicIPAddress -ResourceGroupName myResourceGroupScaleSet -Name myPublicIP | select IpAddress
```

<span data-ttu-id="5d5f7-142">Escriba la dirección IP pública hello en el Explorador de web tooa.</span><span class="sxs-lookup"><span data-stu-id="5d5f7-142">Enter hello public IP address in tooa web browser.</span></span> <span data-ttu-id="5d5f7-143">se muestra la aplicación Hello, incluido Hola nombre de host de hello VM ese Hola la carga del tráfico de equilibrador distribuida para:</span><span class="sxs-lookup"><span data-stu-id="5d5f7-143">hello app is displayed, including hello hostname of hello VM that hello load balancer distributed traffic to:</span></span>

![Ejecución del sitio de IIS](./media/tutorial-create-vmss/running-iis-site.png)

<span data-ttu-id="5d5f7-145">escala de hello toosee establecida en acción, se puede forzar actualización su carga de hello web explorador toosee equilibrador de distribuir el tráfico entre todas las máquinas virtuales de hello ejecutando la aplicación.</span><span class="sxs-lookup"><span data-stu-id="5d5f7-145">toosee hello scale set in action, you can force-refresh your web browser toosee hello load balancer distribute traffic across all hello VMs running your app.</span></span>


## <a name="management-tasks"></a><span data-ttu-id="5d5f7-146">Tareas de administración</span><span class="sxs-lookup"><span data-stu-id="5d5f7-146">Management tasks</span></span>
<span data-ttu-id="5d5f7-147">A lo largo del ciclo de vida de Hola de conjunto de escalas de hello, puede que necesite toorun una o más tareas de administración.</span><span class="sxs-lookup"><span data-stu-id="5d5f7-147">Throughout hello lifecycle of hello scale set, you may need toorun one or more management tasks.</span></span> <span data-ttu-id="5d5f7-148">Además, puede que desee toocreate scripts que automaticen diversas tareas de ciclo de vida.</span><span class="sxs-lookup"><span data-stu-id="5d5f7-148">Additionally, you may want toocreate scripts that automate various lifecycle-tasks.</span></span> <span data-ttu-id="5d5f7-149">PowerShell de Azure proporciona una manera rápida toodo esas tareas.</span><span class="sxs-lookup"><span data-stu-id="5d5f7-149">Azure PowerShell provides a quick way toodo those tasks.</span></span> <span data-ttu-id="5d5f7-150">A continuación, presentamos algunas tareas comunes.</span><span class="sxs-lookup"><span data-stu-id="5d5f7-150">Here are a few common tasks.</span></span>

### <a name="view-vms-in-a-scale-set"></a><span data-ttu-id="5d5f7-151">Visualización de máquinas virtuales en un conjunto de escalado</span><span class="sxs-lookup"><span data-stu-id="5d5f7-151">View VMs in a scale set</span></span>
<span data-ttu-id="5d5f7-152">tooview una lista de máquinas virtuales en ejecución en la escala de conjunto, utilice [AzureRmVmssVM Get](/powershell/module/azurerm.compute/get-azurermvmssvm) como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="5d5f7-152">tooview a list of VMs running in your scale set, use [Get-AzureRmVmssVM](/powershell/module/azurerm.compute/get-azurermvmssvm) as follows:</span></span>

```powershell
# Get current scale set
$scaleset = Get-AzureRmVmss `
  -ResourceGroupName myResourceGroupScaleSet `
  -VMScaleSetName myScaleSet

# Loop through hello instanaces in your scale set
for ($i=1; $i -le ($scaleset.Sku.Capacity - 1); $i++) {
    Get-AzureRmVmssVM -ResourceGroupName myResourceGroupScaleSet `
      -VMScaleSetName myScaleSet `
      -InstanceId $i
}
```


### <a name="increase-or-decrease-vm-instances"></a><span data-ttu-id="5d5f7-153">Aumento o disminución de instancias de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="5d5f7-153">Increase or decrease VM instances</span></span>
<span data-ttu-id="5d5f7-154">número de hello toosee de instancias actualmente en una escala estableciste, use [Get AzureRmVmss](/powershell/module/azurerm.compute/get-azurermvmss) y realizar consultas sobre *sku.capacity*:</span><span class="sxs-lookup"><span data-stu-id="5d5f7-154">toosee hello number of instances you currently have in a scale set, use [Get-AzureRmVmss](/powershell/module/azurerm.compute/get-azurermvmss) and query on *sku.capacity*:</span></span>

```powershell
Get-AzureRmVmss -ResourceGroupName myResourceGroupScaleSet `
    -VMScaleSetName myScaleSet | `
    Select -ExpandProperty Sku
```

<span data-ttu-id="5d5f7-155">Puede, a continuación, manualmente aumentar o reducir el número de Hola de máquinas virtuales en la escala de hello establecida con [AzureRmVmss actualización](/powershell/module/azurerm.compute/update-azurermvmss).</span><span class="sxs-lookup"><span data-stu-id="5d5f7-155">You can then manually increase or decrease hello number of virtual machines in hello scale set with [Update-AzureRmVmss](/powershell/module/azurerm.compute/update-azurermvmss).</span></span> <span data-ttu-id="5d5f7-156">Hello en el ejemplo siguiente se establece Hola número de máquinas virtuales de la escala establecida demasiado*5*:</span><span class="sxs-lookup"><span data-stu-id="5d5f7-156">hello following example sets hello number of VMs in your scale set too*5*:</span></span>

```powershell
# Get current scale set
$scaleset = Get-AzureRmVmss `
  -ResourceGroupName myResourceGroupScaleSet `
  -VMScaleSetName myScaleSet

# Set and update hello capacity of your scale set
$scaleset.sku.capacity = 5
Update-AzureRmVmss -ResourceGroupName myResourceGroupScaleSet `
    -Name myScaleSet `
    -VirtualMachineScaleSet $scaleset
```

<span data-ttu-id="5d5f7-157">Si toma Hola de tooupdate de unos minutos un número especificado de instancias en el conjunto de escala.</span><span class="sxs-lookup"><span data-stu-id="5d5f7-157">If takes a few minutes tooupdate hello specified number of instances in your scale set.</span></span>


### <a name="configure-autoscale-rules"></a><span data-ttu-id="5d5f7-158">Configuración de reglas de escalado automático</span><span class="sxs-lookup"><span data-stu-id="5d5f7-158">Configure autoscale rules</span></span>
<span data-ttu-id="5d5f7-159">En lugar de establece manualmente escalar el número de Hola de instancias en la escala, definir reglas de escalado automático.</span><span class="sxs-lookup"><span data-stu-id="5d5f7-159">Rather than manually scaling hello number of instances in your scale set, you define autoscale rules.</span></span> <span data-ttu-id="5d5f7-160">Estas reglas supervisan Hola instancias en la escala de establecerán y responden según corresponda, basándose en las métricas y los umbrales que defina.</span><span class="sxs-lookup"><span data-stu-id="5d5f7-160">These rules monitor hello instances in your scale set and respond accordingly based on metrics and thresholds you define.</span></span> <span data-ttu-id="5d5f7-161">Hola siguiente ejemplo admita la ampliación horizontal número Hola de instancias en uno cuando la carga promedio de CPU de hello es mayor que 60% durante un período de 5 minutos.</span><span class="sxs-lookup"><span data-stu-id="5d5f7-161">hello following example scales out hello number of instances by one when hello average CPU load is greater than 60% over a 5 minute period.</span></span> <span data-ttu-id="5d5f7-162">Si carga de CPU promedio de hello, a continuación, cae por debajo de 30% durante un período de 5 minutos, instancias de Hola se escalan en una instancia:</span><span class="sxs-lookup"><span data-stu-id="5d5f7-162">If hello average CPU load then drops below 30% over a 5 minute period, hello instances are scaled in by one instance:</span></span>

```powershell
# Define your scale set information
$mySubscriptionId = (Get-AzureRmSubscription).Id
$myResourceGroup = "myResourceGroupScaleSet"
$myScaleSet = "myScaleSet"
$myLocation = "East US"

# Create a scale up rule tooincrease hello number instances after 60% average CPU usage exceeded for a 5 minute period
$myRuleScaleUp = New-AzureRmAutoscaleRule `
  -MetricName "Percentage CPU" `
  -MetricResourceId /subscriptions/$mySubscriptionId/resourceGroups/$myResourceGroup/providers/Microsoft.Compute/virtualMachineScaleSets/$myScaleSet `
  -Operator GreaterThan `
  -MetricStatistic Average `
  -Threshold 60 `
  -TimeGrain 00:01:00 `
  -TimeWindow 00:05:00 `
  -ScaleActionCooldown 00:05:00 `
  -ScaleActionDirection Increase `
  -ScaleActionValue 1

# Create a scale down rule toodecrease hello number of instances after 30% average CPU usage over a 5 minute period
$myRuleScaleDown = New-AzureRmAutoscaleRule `
  -MetricName "Percentage CPU" `
  -MetricResourceId /subscriptions/$mySubscriptionId/resourceGroups/$myResourceGroup/providers/Microsoft.Compute/virtualMachineScaleSets/$myScaleSet `
  -Operator LessThan `
  -MetricStatistic Average `
  -Threshold 30 `
  -TimeGrain 00:01:00 `
  -TimeWindow 00:05:00 `
  -ScaleActionCooldown 00:05:00 `
  -ScaleActionDirection Decrease `
  -ScaleActionValue 1

# Create a scale profile with your scale up and scale down rules
$myScaleProfile = New-AzureRmAutoscaleProfile `
  -DefaultCapacity 2  `
  -MaximumCapacity 10 `
  -MinimumCapacity 2 `
  -Rules $myRuleScaleUp,$myRuleScaleDown `
  -Name "autoprofile"

# Apply hello autoscale rules
Add-AzureRmAutoscaleSetting `
  -Location $myLocation `
  -Name "autosetting" `
  -ResourceGroup $myResourceGroup `
  -TargetResourceId /subscriptions/$mySubscriptionId/resourceGroups/$myResourceGroup/providers/Microsoft.Compute/virtualMachineScaleSets/$myScaleSet `
  -AutoscaleProfiles $myScaleProfile
```


## <a name="next-steps"></a><span data-ttu-id="5d5f7-163">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5d5f7-163">Next steps</span></span>
<span data-ttu-id="5d5f7-164">En este tutorial, ha creado un conjunto de escalado de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="5d5f7-164">In this tutorial, you created a virtual machine scale set.</span></span> <span data-ttu-id="5d5f7-165">Ha aprendido a:</span><span class="sxs-lookup"><span data-stu-id="5d5f7-165">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="5d5f7-166">Usar la extensión de Script personalizado de hello toodefine un tooscale de sitio IIS</span><span class="sxs-lookup"><span data-stu-id="5d5f7-166">Use hello Custom Script Extension toodefine an IIS site tooscale</span></span>
> * <span data-ttu-id="5d5f7-167">Crear un equilibrador de carga para el conjunto de escalado</span><span class="sxs-lookup"><span data-stu-id="5d5f7-167">Create a load balancer for your scale set</span></span>
> * <span data-ttu-id="5d5f7-168">Crear un conjunto de escalado de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="5d5f7-168">Create a virtual machine scale set</span></span>
> * <span data-ttu-id="5d5f7-169">Aumentar o disminuir el número de Hola de instancias de un conjunto de escala</span><span class="sxs-lookup"><span data-stu-id="5d5f7-169">Increase or decrease hello number of instances in a scale set</span></span>
> * <span data-ttu-id="5d5f7-170">Crear reglas de escalado automático</span><span class="sxs-lookup"><span data-stu-id="5d5f7-170">Create autoscale rules</span></span>

<span data-ttu-id="5d5f7-171">Avanzar toohello siguiente tutorial toolearn más información sobre los conceptos de máquinas virtuales de equilibrio de carga.</span><span class="sxs-lookup"><span data-stu-id="5d5f7-171">Advance toohello next tutorial toolearn more about load balancing concepts for virtual machines.</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="5d5f7-172">[Load balance virtual machines](tutorial-load-balancer.md) (Equilibrio de carga de máquinas virtuales)</span><span class="sxs-lookup"><span data-stu-id="5d5f7-172">[Load balance virtual machines](tutorial-load-balancer.md)</span></span>
