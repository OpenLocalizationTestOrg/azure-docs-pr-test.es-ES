---
title: "aaaCreating escalas de máquina Virtual establece mediante cmdlets de PowerShell | Documentos de Microsoft"
description: "Empezar a crear y administrar los primeros conjuntos de escalado de máquina virtual de Azure con cmdlets de Azure PowerShell"
services: virtual-machines-windows
documentationcenter: 
author: danielsollondon
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 430d9d64-1f35-48f0-a4fd-9b69910ffa59
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/21/2017
ms.author: danielsollondon
ms.openlocfilehash: 7979be367d04c904b60d78849c1b751a52cc8caf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="creating-virtual-machine-scale-sets-using-powershell-cmdlets"></a><span data-ttu-id="a5129-103">Creación de conjuntos de escalado de máquina virtual con cmdlets de PowerShell</span><span class="sxs-lookup"><span data-stu-id="a5129-103">Creating Virtual Machine Scale Sets using PowerShell cmdlets</span></span>
<span data-ttu-id="a5129-104">Este artículo le guía a través de un ejemplo de cómo toocreate una escala de máquinas virtuales establece (VMSS).</span><span class="sxs-lookup"><span data-stu-id="a5129-104">This article walks through an example of how toocreate a Virtual Machine scale set (VMSS).</span></span> <span data-ttu-id="a5129-105">Crea un conjunto de escalado de tres nodos, con redes y almacenamiento asociados.</span><span class="sxs-lookup"><span data-stu-id="a5129-105">It creates a scale set of three nodes, with associated Networking and Storage.</span></span>

## <a name="first-steps"></a><span data-ttu-id="a5129-106">Primeros pasos</span><span class="sxs-lookup"><span data-stu-id="a5129-106">First Steps</span></span>
<span data-ttu-id="a5129-107">Asegúrese de tener instalado hello más reciente Azure PowerShell módulo, toomake dispone de los cmdlets de PowerShell de hello necesario toomaintain y crear conjuntos de escalas de.</span><span class="sxs-lookup"><span data-stu-id="a5129-107">Ensure you have hello latest Azure PowerShell module installed, toomake sure you have hello PowerShell commandlets needed toomaintain, and create scale sets.</span></span>
<span data-ttu-id="a5129-108">Vaya a herramientas de línea de comandos de toohello [aquí](http://aka.ms/webpi-azps) para Hola más reciente de los módulos de Azure disponibles.</span><span class="sxs-lookup"><span data-stu-id="a5129-108">Go toohello command line tools [here](http://aka.ms/webpi-azps) for hello latest available Azure Modules.</span></span>

<span data-ttu-id="a5129-109">toofind VMSS relacionados con los cmdlets, use la cadena de búsqueda de hello \*VMSS\*.</span><span class="sxs-lookup"><span data-stu-id="a5129-109">toofind VMSS related commandlets, use hello search string \*VMSS\*.</span></span> <span data-ttu-id="a5129-110">Por ejemplo, _gcm *vmss*_.</span><span class="sxs-lookup"><span data-stu-id="a5129-110">For example, _gcm *vmss*_</span></span>

## <a name="creating-a-vmss"></a><span data-ttu-id="a5129-111">Creación de un VMSS</span><span class="sxs-lookup"><span data-stu-id="a5129-111">Creating a VMSS</span></span>
#### <a name="create-resource-group"></a><span data-ttu-id="a5129-112">Crear grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="a5129-112">Create Resource Group</span></span>
```
$loc = 'westus';
$rgname = 'mynewrgwu';
  New-AzureRmResourceGroup -Name $rgname -Location $loc -Force;
```

### <a name="create-networking-vnet--subnet"></a><span data-ttu-id="a5129-113">Crear redes (VNET o subred)</span><span class="sxs-lookup"><span data-stu-id="a5129-113">Create Networking (VNET / Subnet)</span></span>
#### <a name="subnet-specification"></a><span data-ttu-id="a5129-114">Especificación de subred</span><span class="sxs-lookup"><span data-stu-id="a5129-114">Subnet Specification</span></span>
```
$subnetName = 'websubnet'
  $subnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix "10.0.0.0/24";
```

#### <a name="vnet-specification"></a><span data-ttu-id="a5129-115">Especificación de VNET</span><span class="sxs-lookup"><span data-stu-id="a5129-115">VNET Specification</span></span>
```
$vnet = New-AzureRmVirtualNetwork -Force -Name ('vnet' + $rgname) -ResourceGroupName $rgname -Location $loc -AddressPrefix "10.0.0.0/16" -Subnet $subnet;
$vnet = Get-AzureRmVirtualNetwork -Name ('vnet' + $rgname) -ResourceGroupName $rgname;

# In this case assume hello new subnet is hello only one
$subnetId = $vnet.Subnets[0].Id;
```

#### <a name="create-public-ip-resource-tooallow-external-access"></a><span data-ttu-id="a5129-116">Crear el recurso de IP pública tooAllow acceso externo</span><span class="sxs-lookup"><span data-stu-id="a5129-116">Create Public IP Resource tooAllow External Access</span></span>
<span data-ttu-id="a5129-117">Se trata de enlazado toohello equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="a5129-117">This will be bound toohello Load Balancer.</span></span>

```
$pubip = New-AzureRmPublicIpAddress -Force -Name ('pubip' + $rgname) -ResourceGroupName $rgname -Location $loc -AllocationMethod Dynamic -DomainNameLabel ('pubip' + $rgname);
$pubip = Get-AzureRmPublicIpAddress -Name ('pubip' + $rgname) -ResourceGroupName $rgname;
```

#### <a name="create-load-balancer"></a><span data-ttu-id="a5129-118">Cree un equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="a5129-118">Create Load Balancer</span></span>
```
$frontendName = 'fe' + $rgname
$backendAddressPoolName = 'bepool' + $rgname
$probeName = 'vmssprobe' + $rgname
$inboundNatPoolName = 'innatpool' + $rgname
$lbruleName = 'lbrule' + $rgname
$lbName = 'vmsslb' + $rgname

# Bind Public IP tooLoad Balancer
$frontend = New-AzureRmLoadBalancerFrontendIpConfig -Name $frontendName -PublicIpAddress $pubip
```

#### <a name="configure-load-balancer"></a><span data-ttu-id="a5129-119">Configurar el equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="a5129-119">Configure Load Balancer</span></span>
<span data-ttu-id="a5129-120">Crear configuración de grupo de direcciones de back-end, esto va a compartirse entre NIC Hola de máquinas virtuales de hello en el conjunto de escalas de Hola.</span><span class="sxs-lookup"><span data-stu-id="a5129-120">Create Backend Address Pool Config, this will be shared by hello NICs of hello VMs in hello scale set.</span></span>

```
$backendAddressPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name $backendAddressPoolName
```

<span data-ttu-id="a5129-121">Establece el puerto de sondeo con equilibrio de carga, cambiar la configuración de hello según corresponda para su aplicación.</span><span class="sxs-lookup"><span data-stu-id="a5129-121">Set Load Balanced Probe Port, change hello settings as appropriate for your application.</span></span>

```
$probe = New-AzureRmLoadBalancerProbeConfig -Name $probeName -RequestPath healthcheck.aspx -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2
```

<span data-ttu-id="a5129-122">Crear un grupo NAT entrante para una conexión directa enrutada (no carga equilibrada) toohello máquinas virtuales en la escala de hello establecido por medio de hello equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="a5129-122">Create an inbound NAT pool for direct routed connectivity (not load balanced) toohello VMs in hello scale set via hello Load Balancer.</span></span> <span data-ttu-id="a5129-123">Esto es toodemonstrate con RDP y no puede ser necesario en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a5129-123">This is toodemonstrate using RDP and may not be required in your application.</span></span>

```
$frontendpoolrangestart = 3360
$frontendpoolrangeend = 3370
$backendvmport = 3389
$inboundNatPool = New-AzureRmLoadBalancerInboundNatPoolConfig -Name $inboundNatPoolName -FrontendIPConfigurationId `
$frontend.Id -Protocol Tcp -FrontendPortRangeStart $frontendpoolrangestart -FrontendPortRangeEnd $frontendpoolrangeend -BackendPort $backendvmport;
```

<span data-ttu-id="a5129-124">Crear Hola regla de equilibrio de carga, en este ejemplo se muestra en carga equilibrio puerto 80 solicitudes, usando la configuración de Hola de los pasos anteriores.</span><span class="sxs-lookup"><span data-stu-id="a5129-124">Create hello Load Balanced Rule, this example shows load balancing port 80 requests, using hello settings from previous steps.</span></span>

```
$protocol = 'Tcp'
$feLBPort = 80
$beLBPort = 80

$lbrule = New-AzureRmLoadBalancerRuleConfig -Name $lbruleName `
-FrontendIPConfiguration $frontend -BackendAddressPool $backendAddressPool `
-Probe $probe -Protocol $protocol -FrontendPort $feLBPort -BackendPort $beLBPort `
-IdleTimeoutInMinutes 15 -EnableFloatingIP -LoadDistribution SourceIP -Verbose;
```

<span data-ttu-id="a5129-125">Cree el equilibrador de carga con la configuración.</span><span class="sxs-lookup"><span data-stu-id="a5129-125">Create Load Balancer with configuration.</span></span>

```
$actualLb = New-AzureRmLoadBalancer -Name $lbName -ResourceGroupName $rgname -Location $loc `
-FrontendIpConfiguration $frontend -BackendAddressPool $backendAddressPool `
-Probe $probe -LoadBalancingRule $lbrule -InboundNatPool $inboundNatPool -Verbose;
```

<span data-ttu-id="a5129-126">Compruebe la configuración de carga Equilibrada, compruebe la carga equilibrada puerto configuraciones, tenga en cuenta que no verá que se crean las reglas de NAT de entrada hasta hello las máquinas virtuales en el conjunto de escalas de Hola.</span><span class="sxs-lookup"><span data-stu-id="a5129-126">Check  LB settings, check load balanced port configs, note, you will not see Inbound NAT rules until hello VMs in hello scale set are created.</span></span>

```
$expectedLb = Get-AzureRmLoadBalancer -Name $lbName -ResourceGroupName $rgname
```

##### <a name="configure-and-create-hello-scale-set"></a><span data-ttu-id="a5129-127">Configurar y crear Hola escala configurada</span><span class="sxs-lookup"><span data-stu-id="a5129-127">Configure and Create hello scale set</span></span>
<span data-ttu-id="a5129-128">Tenga en cuenta que esta infraestructura en el ejemplo se muestra cómo distribuir tooset seguridad y tráfico de web de escala en el conjunto de escalas de hello, pero Hola imágenes de máquinas virtuales especificadas aquí no tiene ningún servicio web instalado.</span><span class="sxs-lookup"><span data-stu-id="a5129-128">Note, this infrastructure example shows how tooset up distribute and scale web traffic across hello scale set, but hello VMs Images specified here do not have any web services installed.</span></span>

```
# specify scale set Name
$vmssName = 'vmss' + $rgname;

## specify VMSS specific details
$adminUsername = 'azadmin';
$adminPassword = "Password1234!";

$PublisherName = 'MicrosoftWindowsServer'
$Offer         = 'WindowsServer'
$Sku          = '2012-R2-Datacenter'
$Version       = 'latest'
$vmNamePrefix = 'winvmss'

###add an extension
$extname = 'BGInfo';
$publisher = 'Microsoft.Compute';
$exttype = 'BGInfo';
$extver = '2.1';
```

<span data-ttu-id="a5129-129">Enlazar tooLoad NIC equilibrador y subred</span><span class="sxs-lookup"><span data-stu-id="a5129-129">Bind NIC tooLoad Balancer and Subnet</span></span>

```
$ipCfg = New-AzureRmVmssIPConfig -Name 'nic' `
-LoadBalancerInboundNatPoolsId $actualLb.InboundNatPools[0].Id `
-LoadBalancerBackendAddressPoolsId $actualLb.BackendAddressPools[0].Id `
-SubnetId $subnetId;
```

<span data-ttu-id="a5129-130">Crear la configuración del conjunto de escalado</span><span class="sxs-lookup"><span data-stu-id="a5129-130">Create scale set Config</span></span>

```
# Specify number of nodes
$numberofnodes = 3

$vmss = New-AzureRmVmssConfig -Location $loc -SkuCapacity $numberofnodes -SkuName 'Standard_A2' -UpgradePolicyMode 'automatic' `
    | Add-AzureRmVmssNetworkInterfaceConfiguration -Name $subnetName -Primary $true -IPConfiguration $ipCfg `
    | Set-AzureRmVmssOSProfile -ComputerNamePrefix $vmNamePrefix -AdminUsername $adminUsername -AdminPassword $adminPassword `
    | Set-AzureRmVmssStorageProfile -OsDiskCreateOption 'FromImage' -OsDiskCaching 'None' `
    -ImageReferenceOffer $Offer -ImageReferenceSku $Sku -ImageReferenceVersion $Version `
    -ImageReferencePublisher $PublisherName `
    | Add-AzureRmVmssExtension -Name $extname -Publisher $publisher -Type $exttype -TypeHandlerVersion $extver -AutoUpgradeMinorVersion $true
```

<span data-ttu-id="a5129-131">Compilar la configuración del conjunto de escalado</span><span class="sxs-lookup"><span data-stu-id="a5129-131">Build scale set configuration</span></span>

```
New-AzureRmVmss -ResourceGroupName $rgname -Name $vmssName -VirtualMachineScaleSet $vmss -Verbose;
```

<span data-ttu-id="a5129-132">Ahora ha creado el conjunto de escalas de Hola.</span><span class="sxs-lookup"><span data-stu-id="a5129-132">Now you have created hello scale set.</span></span> <span data-ttu-id="a5129-133">Puede probar conexión toohello máquinas virtuales individuales mediante RDP en este ejemplo:</span><span class="sxs-lookup"><span data-stu-id="a5129-133">You can test connecting toohello individual VM using RDP in this example:</span></span>

```
VM0 : pubipmynewrgwu.westus.cloudapp.azure.com:3360
VM1 : pubipmynewrgwu.westus.cloudapp.azure.com:3361
VM2 : pubipmynewrgwu.westus.cloudapp.azure.com:3362
```
