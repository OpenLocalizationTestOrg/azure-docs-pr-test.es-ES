---
title: "conjunto de aaaCreate una escala de la máquina virtual de Azure | Documentos de Microsoft"
description: "Cree e implemente un conjunto de escalado de máquinas virtuales Linux o Windows de Azure con la CLI de Azure, PowerShell, una plantilla o Visual Studio."
services: virtual-machine-scale-sets
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 07/21/2017
ms.author: adegeo
ms.openlocfilehash: 73de25c1dd2424e64655b3accfea848926e72f69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-a-virtual-machine-scale-set"></a><span data-ttu-id="9af35-103">Creación e implementación de un conjunto de escalado de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="9af35-103">Create and deploy a virtual machine scale set</span></span>
<span data-ttu-id="9af35-104">Conjuntos de escalas de máquina virtual hacen más sencillo para usted toodeploy y administran máquinas virtuales idénticas como un conjunto.</span><span class="sxs-lookup"><span data-stu-id="9af35-104">Virtual machine scale sets make it easy for you toodeploy and manage identical virtual machines as a set.</span></span> <span data-ttu-id="9af35-105">Los conjuntos de escala proporcionan una capa de proceso altamente escalable y personalizable para aplicaciones de gran escala y admiten imágenes de la plataforma Windows, imágenes de la plataforma Linux, imágenes personalizadas y extensiones.</span><span class="sxs-lookup"><span data-stu-id="9af35-105">Scale sets provide a highly scalable and customizable compute layer for hyperscale applications, and they support Windows platform images, Linux platform images, custom images, and extensions.</span></span> <span data-ttu-id="9af35-106">Para más información sobre los conjuntos de escalado, consulte [Conjuntos de escalado de máquinas virtuales](virtual-machine-scale-sets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9af35-106">For more information about scale sets, see [Virtual machine scale sets](virtual-machine-scale-sets-overview.md).</span></span>

<span data-ttu-id="9af35-107">Este tutorial muestra cómo toocreate una escala de máquinas virtuales establece **sin** utilizando Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="9af35-107">This tutorial shows you how toocreate a virtual machine scale set **without** using hello Azure portal.</span></span> <span data-ttu-id="9af35-108">Para obtener información acerca de cómo toouse Hola portal de Azure, consulte [cómo toocreate configuración de escalas de máquina virtual con hello portal de Azure](virtual-machine-scale-sets-portal-create.md).</span><span class="sxs-lookup"><span data-stu-id="9af35-108">For information about how toouse hello Azure portal, see [How toocreate a virtual machine scale set with hello Azure portal](virtual-machine-scale-sets-portal-create.md).</span></span>

>[!NOTE]
><span data-ttu-id="9af35-109">Para más información sobre los recursos de Azure Resource Manager, consulte [Implementación mediante Azure Resource Manager frente al modelo clásico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="9af35-109">For more information about Azure Resource Manager resources, see [Azure Resource Manager vs. classic deployment](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>

## <a name="sign-in-tooazure"></a><span data-ttu-id="9af35-110">Inicie sesión en tooAzure</span><span class="sxs-lookup"><span data-stu-id="9af35-110">Sign in tooAzure</span></span>

<span data-ttu-id="9af35-111">Si utiliza una escala de toocreate 2.0 de CLI de Azure o Azure PowerShell establecido, primero debe toosign en tooyour suscripción.</span><span class="sxs-lookup"><span data-stu-id="9af35-111">If you're using Azure CLI 2.0 or Azure PowerShell toocreate a scale set, you first need toosign in tooyour subscription.</span></span>

<span data-ttu-id="9af35-112">Para obtener más información acerca de cómo tooinstall, configurar e inicie sesión en tooAzure con Azure CLI o PowerShell, consulte [Getting Started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md) o [empezar a trabajar con cmdlets de PowerShell de Azure](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="9af35-112">For more information about how tooinstall, set up, and sign in tooAzure with Azure CLI or PowerShell, see [Getting Started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md) or [Get started with Azure PowerShell cmdlets](/powershell/azure/overview).</span></span>

```azurecli
az login
```

```powershell
Login-AzureRmAccount
```

## <a name="create-a-resource-group"></a><span data-ttu-id="9af35-113">Crear un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="9af35-113">Create a resource group</span></span>

<span data-ttu-id="9af35-114">En primer lugar debe toocreate está asociado a un grupo de recursos que establecer escalas de máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="9af35-114">You first need toocreate a resource group that hello virtual machine scale set is associated with.</span></span>

```azurecli
az group create --location westus2 --name MyResourceGroup1
```

```powershell
New-AzureRmResourceGroup -Location westus2 -Name MyResourceGroup1
```

## <a name="create-from-azure-cli"></a><span data-ttu-id="9af35-115">Creación desde la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="9af35-115">Create from Azure CLI</span></span>

<span data-ttu-id="9af35-116">Con la CLI de Azure, puede crear un conjunto de escalado de máquinas virtuales con un mínimo de esfuerzo.</span><span class="sxs-lookup"><span data-stu-id="9af35-116">With Azure CLI, you can create a virtual machine scale set with minimal effort.</span></span> <span data-ttu-id="9af35-117">Si omite los valores predeterminados, se los proporcionaremos.</span><span class="sxs-lookup"><span data-stu-id="9af35-117">If you omit default values, they are provided for you.</span></span> <span data-ttu-id="9af35-118">Por ejemplo, si no especifica información de ninguna red virtual, se creará una.</span><span class="sxs-lookup"><span data-stu-id="9af35-118">For example, if you don't specify any virtual network information, a virtual network is created for you.</span></span> <span data-ttu-id="9af35-119">Si se omite Hola siguientes piezas, se crean automáticamente:</span><span class="sxs-lookup"><span data-stu-id="9af35-119">If you omit hello following parts, they are created for you:</span></span> 
- <span data-ttu-id="9af35-120">Un equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="9af35-120">A load balancer</span></span>
- <span data-ttu-id="9af35-121">Una red virtual</span><span class="sxs-lookup"><span data-stu-id="9af35-121">A virtual network</span></span>
- <span data-ttu-id="9af35-122">Una dirección IP pública</span><span class="sxs-lookup"><span data-stu-id="9af35-122">A public IP address</span></span>

<span data-ttu-id="9af35-123">Al elegir hello imagen de máquina virtual que desea toouse en conjunto de escalas de máquina virtual de hello, tiene algunas opciones:</span><span class="sxs-lookup"><span data-stu-id="9af35-123">When choosing hello virtual machine image that you want toouse on hello virtual machine scale set, you have a few choices:</span></span>

- <span data-ttu-id="9af35-124">URN</span><span class="sxs-lookup"><span data-stu-id="9af35-124">URN</span></span>  
<span data-ttu-id="9af35-125">identificador de Hola de un recurso:</span><span class="sxs-lookup"><span data-stu-id="9af35-125">hello identifier of a resource:</span></span>  
<span data-ttu-id="9af35-126">**Win2012R2Datacenter**</span><span class="sxs-lookup"><span data-stu-id="9af35-126">**Win2012R2Datacenter**</span></span>

- <span data-ttu-id="9af35-127">Alias de URN</span><span class="sxs-lookup"><span data-stu-id="9af35-127">URN alias</span></span>  
<span data-ttu-id="9af35-128">nombre descriptivo de Hola de un URN:</span><span class="sxs-lookup"><span data-stu-id="9af35-128">hello friendly name of a URN:</span></span>  
<span data-ttu-id="9af35-129">**MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest**</span><span class="sxs-lookup"><span data-stu-id="9af35-129">**MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest**</span></span>

- <span data-ttu-id="9af35-130">Identificador de recurso personalizado</span><span class="sxs-lookup"><span data-stu-id="9af35-130">Custom resource id</span></span>  
<span data-ttu-id="9af35-131">tooan de ruta de acceso de Hello recursos de Azure:</span><span class="sxs-lookup"><span data-stu-id="9af35-131">hello path tooan Azure resource:</span></span>  
<span data-ttu-id="9af35-132">**/subscriptions/subscription-guid/resourceGroups/MyResourceGroup/providers/Microsoft.Compute/images/MyImage**</span><span class="sxs-lookup"><span data-stu-id="9af35-132">**/subscriptions/subscription-guid/resourceGroups/MyResourceGroup/providers/Microsoft.Compute/images/MyImage**</span></span>

- <span data-ttu-id="9af35-133">Recurso web</span><span class="sxs-lookup"><span data-stu-id="9af35-133">Web resource</span></span>  
<span data-ttu-id="9af35-134">Hola tooan de ruta de acceso URI de HTTP:</span><span class="sxs-lookup"><span data-stu-id="9af35-134">hello path tooan HTTP URI:</span></span>  
<span data-ttu-id="9af35-135">**http://contoso.blob.core.windows.net/vhds/osdiskimage.vhd**</span><span class="sxs-lookup"><span data-stu-id="9af35-135">**http://contoso.blob.core.windows.net/vhds/osdiskimage.vhd**</span></span>

>[!TIP]
><span data-ttu-id="9af35-136">Puede encontrar una lista de las imágenes disponibles con `az vm image list`.</span><span class="sxs-lookup"><span data-stu-id="9af35-136">You can get a list of available images with `az vm image list`.</span></span>

<span data-ttu-id="9af35-137">conjunto de escalas de máquina virtual de toocreate, debe especificar siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="9af35-137">toocreate a virtual machine scale set, you must specify hello following:</span></span>

- <span data-ttu-id="9af35-138">Grupos de recursos</span><span class="sxs-lookup"><span data-stu-id="9af35-138">Resource group</span></span> 
- <span data-ttu-id="9af35-139">Nombre</span><span class="sxs-lookup"><span data-stu-id="9af35-139">Name</span></span>
- <span data-ttu-id="9af35-140">Imagen del sistema operativo</span><span class="sxs-lookup"><span data-stu-id="9af35-140">Operating system image</span></span>
- <span data-ttu-id="9af35-141">Información de autenticación</span><span class="sxs-lookup"><span data-stu-id="9af35-141">Authentication information</span></span> 
 
<span data-ttu-id="9af35-142">Hola de ejemplo siguiente crea un conjunto de escalas de máquina virtual básica (este paso puede tardar unos minutos).</span><span class="sxs-lookup"><span data-stu-id="9af35-142">hello following example creates a basic virtual machine scale set (this step might take a few minutes).</span></span>

```azurecli
az vmss create --resource-group MyResourceGroup1 --name MyScaleSet --image UbuntuLTS --authentication-type password --admin-username azureuser --admin-password P@ssw0rd!
```

<span data-ttu-id="9af35-143">Una vez que finalice el comando hello tendrá la escala de máquinas virtuales establecer creado.</span><span class="sxs-lookup"><span data-stu-id="9af35-143">Once hello command finishes you will now have your virtual machine scale set created.</span></span> <span data-ttu-id="9af35-144">Deberá tooget dirección IP de Hola de máquina virtual de Hola para que puedan conectarse tooit.</span><span class="sxs-lookup"><span data-stu-id="9af35-144">You may need tooget hello IP address of hello virtual machine so that you can connect tooit.</span></span> <span data-ttu-id="9af35-145">Puede obtener mucha información distinta acerca de la máquina virtual de hello (incluida la dirección IP de hello) con el siguiente comando de Hola.</span><span class="sxs-lookup"><span data-stu-id="9af35-145">You can get a lot of different information about hello virtual machine (including hello IP address) with hello following command.</span></span> 

```azurecli
az vmss list-instance-connection-info --resource-group MyResourceGroup1 --name MyScaleSet
```

## <a name="create-from-powershell"></a><span data-ttu-id="9af35-146">Creación desde PowerShell</span><span class="sxs-lookup"><span data-stu-id="9af35-146">Create from PowerShell</span></span>

<span data-ttu-id="9af35-147">PowerShell es más complicado toouse de CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="9af35-147">PowerShell is more complicated toouse than Azure CLI.</span></span> <span data-ttu-id="9af35-148">Mientras que la CLI de Azure proporciona valores predeterminados para los recursos relacionados con las redes (como equilibradores de carga, direcciones IP y redes virtuales), PowerShell no lo hace.</span><span class="sxs-lookup"><span data-stu-id="9af35-148">While Azure CLI provides defaults for networking-related resources (such as load balancers, IP addresses, and virtual networks), PowerShell does not.</span></span> <span data-ttu-id="9af35-149">Además, hacer referencia a una imagen con PowerShell también es un poco más complicado.</span><span class="sxs-lookup"><span data-stu-id="9af35-149">Referencing an image with PowerShell is a slightly more complicated too.</span></span> <span data-ttu-id="9af35-150">Puede obtener imágenes con hello siguientes cmdlets:</span><span class="sxs-lookup"><span data-stu-id="9af35-150">You can get images with hello following cmdlets:</span></span>

1. <span data-ttu-id="9af35-151">Get-AzureRMVMImagePublisher</span><span class="sxs-lookup"><span data-stu-id="9af35-151">Get-AzureRMVMImagePublisher</span></span>
2. <span data-ttu-id="9af35-152">Get-AzureRMVMImageOffer</span><span class="sxs-lookup"><span data-stu-id="9af35-152">Get-AzureRMVMImageOffer</span></span>
3. <span data-ttu-id="9af35-153">Get-AzureRmVMImageSku</span><span class="sxs-lookup"><span data-stu-id="9af35-153">Get-AzureRmVMImageSku</span></span>

<span data-ttu-id="9af35-154">se puede canalizar Hola cmdlets funcionan en secuencia.</span><span class="sxs-lookup"><span data-stu-id="9af35-154">hello cmdlets work can be piped in sequence.</span></span> <span data-ttu-id="9af35-155">Este es un ejemplo de cómo tooget todas las imágenes de hello **West US 2** región con un publicador que tiene el nombre de hello **microsoft** en ella.</span><span class="sxs-lookup"><span data-stu-id="9af35-155">Here is an example of how tooget all images for hello **West US 2** region with a publisher that has hello name **microsoft** in it.</span></span>

```powershell
Get-AzureRMVMImagePublisher -Location WestUS2 | Where-Object PublisherName -Like *microsoft* | Get-AzureRMVMImageOffer | Get-AzureRmVMImageSku | Select-Object PublisherName, Offer, Skus
```

```
PublisherName              Offer                    Skus
-------------              -----                    ----
microsoft-ads              linux-data-science-vm    linuxdsvm
microsoft-ads              standard-data-science-vm standard-data-science-vm
MicrosoftAzureSiteRecovery Process-Server           Windows-2012-R2-Datacenter
MicrosoftBizTalkServer     BizTalk-Server           2013-R2-Enterprise
MicrosoftBizTalkServer     BizTalk-Server           2013-R2-Standard
MicrosoftBizTalkServer     BizTalk-Server           2016-Developer
MicrosoftBizTalkServer     BizTalk-Server           2016-Enterprise
...
```

<span data-ttu-id="9af35-156">flujo de trabajo de Hola para crear un conjunto de escalas de máquina virtual es como sigue:</span><span class="sxs-lookup"><span data-stu-id="9af35-156">hello workflow for creating a virtual machine scale set is as follows:</span></span>

1. <span data-ttu-id="9af35-157">Crear un objeto de configuración que contiene información sobre el conjunto de escalas de Hola.</span><span class="sxs-lookup"><span data-stu-id="9af35-157">Create a config object that holds information about hello scale set.</span></span>
2. <span data-ttu-id="9af35-158">Imagen SO base de referencia Hola.</span><span class="sxs-lookup"><span data-stu-id="9af35-158">Reference hello base OS image.</span></span>
3. <span data-ttu-id="9af35-159">Configurar el sistema operativo de hello: autenticación, el prefijo del nombre de máquina virtual y usuario/pass.</span><span class="sxs-lookup"><span data-stu-id="9af35-159">Configure hello operating system settings: authentication, VM name prefix, and user/pass.</span></span>
4. <span data-ttu-id="9af35-160">Configure las redes.</span><span class="sxs-lookup"><span data-stu-id="9af35-160">Configure networking.</span></span>
5. <span data-ttu-id="9af35-161">Crear conjunto de escalas de Hola.</span><span class="sxs-lookup"><span data-stu-id="9af35-161">Create hello scale set.</span></span>

<span data-ttu-id="9af35-162">En este ejemplo se crean un conjunto de escalado básico de dos instancias con Windows Server 2016 instalado.</span><span class="sxs-lookup"><span data-stu-id="9af35-162">This example creates a basic two-instance scale set for a computer that has Windows Server 2016 installed.</span></span>

```powershell
# Resource group name from above
$rg = "MyResourceGroup1"
$location = "WestUS2"

# Create a config object
$vmssConfig = New-AzureRmVmssConfig -Location $location -SkuCapacity 2 -SkuName Standard_A0  -UpgradePolicyMode Automatic

# Reference a virtual machine image from hello gallery
Set-AzureRmVmssStorageProfile $vmssConfig -ImageReferencePublisher MicrosoftWindowsServer -ImageReferenceOffer WindowsServer -ImageReferenceSku 2016-Datacenter -ImageReferenceVersion latest

# Set up information for authenticating with hello virtual machine
Set-AzureRmVmssOsProfile $vmssConfig -AdminUsername azureuser -AdminPassword P@ssw0rd! -ComputerNamePrefix myvmssvm

# Create hello virtual network resources

## Basics
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name "my-subnet" -AddressPrefix 10.0.0.0/24
$vnet = New-AzureRmVirtualNetwork -Name "my-network" -ResourceGroupName $rg -Location $location -AddressPrefix 10.0.0.0/16 -Subnet $subnet

## Load balancer
$publicIP = New-AzureRmPublicIpAddress -Name "PublicIP" -ResourceGroupName $rg -Location $location -AllocationMethod Static -DomainNameLabel "myuniquedomain"
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig -Name "LB-Frontend" -PublicIpAddress $publicIP
$backendPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name "LB-backend"
$probe = New-AzureRmLoadBalancerProbeConfig -Name "HealthProbe" -Protocol Tcp -Port 80 -IntervalInSeconds 15 -ProbeCount 2
$inboundNATRule1= New-AzureRmLoadBalancerRuleConfig -Name "webserver" -FrontendIpConfiguration $frontendIP -Protocol Tcp -FrontendPort 80 -BackendPort 80 -IdleTimeoutInMinutes 15 -Probe $probe -BackendAddressPool $backendPool
$inboundNATPool1 = New-AzureRmLoadBalancerInboundNatPoolConfig -Name "RDP" -FrontendIpConfigurationId $frontendIP.Id -Protocol TCP -FrontendPortRangeStart 53380 -FrontendPortRangeEnd 53390 -BackendPort 3389

New-AzureRmLoadBalancer -ResourceGroupName $rg -Name "LB1" -Location $location -FrontendIpConfiguration $frontendIP -LoadBalancingRule $inboundNATRule1 -InboundNatPool $inboundNATPool1 -BackendAddressPool $backendPool -Probe $probe

## IP address config
$ipConfig = New-AzureRmVmssIpConfig -Name "my-ipaddress" -LoadBalancerBackendAddressPoolsId $backendPool.Id -SubnetId $vnet.Subnets[0].Id -LoadBalancerInboundNatPoolsId $inboundNATPool1.Id

# Attach hello virtual network toohello IP object
Add-AzureRmVmssNetworkInterfaceConfiguration -VirtualMachineScaleSet $vmssConfig -Name "network-config" -Primary $true -IPConfiguration $ipConfig

# Create hello scale set with hello config object (this step might take a few minutes)
New-AzureRmVmss -ResourceGroupName $rg -Name "MyScaleSet1" -VirtualMachineScaleSet $vmssConfig
```

### <a name="using-a-custom-virtual-machine-image"></a><span data-ttu-id="9af35-163">Uso de una imagen de máquina virtual personalizada</span><span class="sxs-lookup"><span data-stu-id="9af35-163">Using a custom virtual machine image</span></span>
<span data-ttu-id="9af35-164">Si va a crear una escala establecida desde su propia imagen personalizada en lugar de hacer referencia a una imagen de máquina virtual desde la Galería de hello, Hola _AzureRmVmssStorageProfile conjunto_ comando sería similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="9af35-164">If you are creating a scale set from your own custom image, instead of referencing a virtual machine image from hello gallery, hello _Set-AzureRmVmssStorageProfile_ command would look like this:</span></span>
```PowerShell
Set-AzureRmVmssStorageProfile -OsDiskCreateOption FromImage -ManagedDisk PremiumLRS -OsDiskCaching "None" -OsDiskOsType Linux -ImageReferenceId (Get-AzureRmImage -ImageName $VMImage -ResourceGroupName $rg).id
```

## <a name="create-from-a-template"></a><span data-ttu-id="9af35-165">Creación desde una plantilla</span><span class="sxs-lookup"><span data-stu-id="9af35-165">Create from a template</span></span>

<span data-ttu-id="9af35-166">Puede implementar un conjunto de escalado de máquinas virtuales con una plantilla de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="9af35-166">You can deploy a virtual machine scale set by using an Azure Resource Manager template.</span></span> <span data-ttu-id="9af35-167">Puede crear su propia plantilla o usar uno de hello [repositorio de plantilla](https://azure.microsoft.com/resources/templates/?term=vmss).</span><span class="sxs-lookup"><span data-stu-id="9af35-167">You can create your own template or use one from hello [template repository](https://azure.microsoft.com/resources/templates/?term=vmss).</span></span> <span data-ttu-id="9af35-168">Estas plantillas se pueden implementar directamente tooyour suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="9af35-168">These templates can be deployed directly tooyour Azure subscription.</span></span>

>[!NOTE]
><span data-ttu-id="9af35-169">toocreate su propia plantilla, se crea un archivo de texto JSON.</span><span class="sxs-lookup"><span data-stu-id="9af35-169">toocreate your own template, you create a JSON text file.</span></span> <span data-ttu-id="9af35-170">Para obtener información general acerca de cómo toocreate y personalizar una plantilla, consulte [plantillas de Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="9af35-170">For general information about how toocreate and customize a template, see [Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="9af35-171">[GitHub](https://github.com/gatneil/mvss/tree/minimum-viable-scale-set) tiene una plantilla de ejemplo a su disposición.</span><span class="sxs-lookup"><span data-stu-id="9af35-171">A sample template is available [on GitHub](https://github.com/gatneil/mvss/tree/minimum-viable-scale-set).</span></span> <span data-ttu-id="9af35-172">Para obtener más información acerca de cómo ver toocreate y use ese ejemplo, [conjunto de escala viable mínimo](.\virtual-machine-scale-sets-mvss-start.md).</span><span class="sxs-lookup"><span data-stu-id="9af35-172">For more information about how toocreate and use that sample, see [Minimum viable scale set](.\virtual-machine-scale-sets-mvss-start.md).</span></span>

## <a name="create-from-visual-studio"></a><span data-ttu-id="9af35-173">Creación desde Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9af35-173">Create from Visual Studio</span></span>

<span data-ttu-id="9af35-174">Con Visual Studio, puede crear un proyecto del grupo de recursos de Azure y agregar que plantilla tooit de conjuntos de escalas de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9af35-174">With Visual Studio, you can create an Azure resource group project and add a virtual machine scale set template tooit.</span></span> <span data-ttu-id="9af35-175">Puede elegir si desea que tooimport desde GitHub o hello Galería de aplicaciones Web de Azure.</span><span class="sxs-lookup"><span data-stu-id="9af35-175">You can choose whether you want tooimport it from GitHub or hello Azure Web Application Gallery.</span></span> <span data-ttu-id="9af35-176">También se genera un script de PowerShell de implementación.</span><span class="sxs-lookup"><span data-stu-id="9af35-176">A deployment PowerShell script is also generated for you.</span></span> <span data-ttu-id="9af35-177">Para obtener más información, consulte [cómo toocreate configuración de escalas de máquina virtual con Visual Studio](virtual-machine-scale-sets-vs-create.md).</span><span class="sxs-lookup"><span data-stu-id="9af35-177">For more information, see [How toocreate a virtual machine scale set with Visual Studio](virtual-machine-scale-sets-vs-create.md).</span></span>

## <a name="create-from-hello-azure-portal"></a><span data-ttu-id="9af35-178">Crear a partir de hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="9af35-178">Create from hello Azure portal</span></span>

<span data-ttu-id="9af35-179">Hola portal de Azure proporciona una manera cómoda de tooquickly crear un conjunto de escala.</span><span class="sxs-lookup"><span data-stu-id="9af35-179">hello Azure portal provides a convenient way tooquickly create a scale set.</span></span> <span data-ttu-id="9af35-180">Para obtener más información, consulte [cómo toocreate configuración de escalas de máquina virtual con hello portal de Azure](virtual-machine-scale-sets-portal-create.md).</span><span class="sxs-lookup"><span data-stu-id="9af35-180">For more information, see [How toocreate a virtual machine scale set with hello Azure portal](virtual-machine-scale-sets-portal-create.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9af35-181">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9af35-181">Next steps</span></span>

<span data-ttu-id="9af35-182">Más información sobre los [discos de datos](virtual-machine-scale-sets-attached-disks.md).</span><span class="sxs-lookup"><span data-stu-id="9af35-182">Learn more about [data disks](virtual-machine-scale-sets-attached-disks.md).</span></span>

<span data-ttu-id="9af35-183">Obtenga información acerca de cómo demasiado[administre las aplicaciones](virtual-machine-scale-sets-deploy-app.md).</span><span class="sxs-lookup"><span data-stu-id="9af35-183">Learn how too[manage your apps](virtual-machine-scale-sets-deploy-app.md).</span></span>
