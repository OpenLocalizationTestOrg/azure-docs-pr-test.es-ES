---
title: aaaUpload un tooAzure de disco duro virtual generalizado ejemplo de Script de PowerShell | Documentos de Microsoft
description: "PowerShell tooupload un tooAzure de disco duro virtual generalizado de secuencia de comandos de ejemplo y crear una nueva máquina virtual con el modelo de implementación de administrador de recursos de Hola y discos administrados."
services: virtual-machines-windows
documentationcenter: virtual-machines
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/18/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 72b4ff09eb7a6ba1604b9d5cbac51e60eded7545
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="sample-script-tooupload-a-vhd-tooazure-and-create-a-new-vm"></a><span data-ttu-id="4025a-103">Ejemplo de script tooupload un tooAzure VHD y crear una nueva máquina virtual</span><span class="sxs-lookup"><span data-stu-id="4025a-103">Sample script tooupload a VHD tooAzure and create a new VM</span></span>

<span data-ttu-id="4025a-104">Este script toma un archivo .vhd local de una máquina virtual generalizada y carga tooAzure, crea una imagen de disco administrado y usa hello toocreate una nueva máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="4025a-104">This script takes a local .vhd file from a generalized VM and uploads it tooAzure, creates a Managed Disk image and uses hello toocreate a new VM.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="4025a-105">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="4025a-105">Sample script</span></span>

```powershell
# Provide values for hello variables
$resourceGroup = 'myResourceGroup'
$location = 'EastUS'
$storageaccount = 'mystorageaccount'
$storageType = 'Standard_LRS'
$containername = 'mycontainer'
$localPath = 'C:\Users\Public\Documents\Hyper-V\VHDs\generalized.vhd'
$vmName = 'myVM'
$imageName = 'myImage'
$vhdName = 'myUploadedVhd.vhd'
$diskSizeGB = '128'
$subnetName = 'mySubnet'
$vnetName = 'myVnet'
$ipName = 'myPip'
$nicName = 'myNic'
$nsgName = 'myNsg'
$ruleName = 'myRdpRule'
$vmName = 'myVM'
$computerName = 'myComputerName'
$vmSize = 'Standard_DS1_v2'

# Get hello username and password toobe used for hello administrators account on hello VM. 
# This is used when connecting toohello VM using RDP.

$cred = Get-Credential

# Upload hello VHD
New-AzureRmResourceGroup -Name $resourceGroup -Location $location
New-AzureRmStorageAccount -ResourceGroupName $resourceGroup -Name $storageAccount -Location $location `
    -SkuName $storageType -Kind "Storage"
$urlOfUploadedImageVhd = ('https://' + $storageaccount + '.blob.core.windows.net/' + $containername + '/' + $vhdName)
Add-AzureRmVhd -ResourceGroupName $resourceGroup -Destination $urlOfUploadedImageVhd `
    -LocalFilePath $localPath

# Note: Uploading hello VHD may take awhile!

# Create a managed image from hello uploaded VHD 
$imageConfig = New-AzureRmImageConfig -Location $location
$imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsType Windows -OsState Generalized `
    -BlobUri $urlOfUploadedImageVhd
$image = New-AzureRmImage -ImageName $imageName -ResourceGroupName $resourceGroup -Image $imageConfig
 
# Create hello networking resources
$singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
$vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $resourceGroup -Location $location `
    -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
$pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $resourceGroup -Location $location `
    -AllocationMethod Dynamic
$nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $resourceGroup -Location $location `
    -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name $ruleName -Description 'Allow RDP' -Access Allow `
    -Protocol Tcp -Direction Inbound -Priority 110 -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $resourceGroup -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $resourceGroup -Name $vnetName

# Start building hello VM configuration
$vm = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize

# Set hello VM image as source image for hello new VM
$vm = Set-AzureRmVMSourceImage -VM $vm -Id $image.Id

# Finish hello VM configuration and add hello NIC.
$vm = Set-AzureRmVMOSDisk -VM $vm  -DiskSizeInGB $diskSizeGB -CreateOption FromImage -Caching ReadWrite
$vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName $computerName -Credential $cred `
    -ProvisionVMAgent -EnableAutoUpdate
$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id

# Create hello VM
New-AzureRmVM -VM $vm -ResourceGroupName $resourceGroup -Location $location

# Verify that hello VM was created
$vmList = Get-AzureRmVM -ResourceGroupName $resourceGroup
$vmList.Name


```


<!-- 
[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-iis/create-windows-vm-iis.ps1 "Create VM IIS")] -->

## <a name="clean-up-deployment"></a><span data-ttu-id="4025a-106">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="4025a-106">Clean up deployment</span></span> 

<span data-ttu-id="4025a-107">Ejecute hello después el grupo de recursos de comando tooremove hello, la VM y todos ellos relacionados con recursos.</span><span class="sxs-lookup"><span data-stu-id="4025a-107">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name $resourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="4025a-108">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="4025a-108">Script explanation</span></span>

<span data-ttu-id="4025a-109">Este script utiliza Hola después de la implementación de comandos toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="4025a-109">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="4025a-110">Cada elemento de la documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="4025a-110">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="4025a-111">Comando</span><span class="sxs-lookup"><span data-stu-id="4025a-111">Command</span></span>                                                                                                             | <span data-ttu-id="4025a-112">Notas</span><span class="sxs-lookup"><span data-stu-id="4025a-112">Notes</span></span>                                                                                                                                                                                |
|---------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [<span data-ttu-id="4025a-113">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="4025a-113">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup)                           | <span data-ttu-id="4025a-114">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="4025a-114">Creates a resource group in which all resources are stored.</span></span>                                                                                                                          |
| [<span data-ttu-id="4025a-115">New-AzureRmStorageAccount</span><span class="sxs-lookup"><span data-stu-id="4025a-115">New-AzureRmStorageAccount</span></span>](/powershell/module/azurerm.resources/new-azurermstorageaccount)                         | <span data-ttu-id="4025a-116">Crea una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="4025a-116">Creates a storage account.</span></span>                                                                                                                                                           |
| [<span data-ttu-id="4025a-117">Add-AzureRmVhd</span><span class="sxs-lookup"><span data-stu-id="4025a-117">Add-AzureRmVhd</span></span>](/powershell/module/azurerm.resources/add-azurermvhd)                                               | <span data-ttu-id="4025a-118">Carga un disco duro virtual de un blob de tooa de máquina virtual local en una cuenta de almacenamiento en la nube de Azure.</span><span class="sxs-lookup"><span data-stu-id="4025a-118">Uploads a virtual hard disk from an on-premises virtual machine tooa blob in a cloud storage account in Azure.</span></span>                                                                       |
| [<span data-ttu-id="4025a-119">New-AzureRmImageConfig</span><span class="sxs-lookup"><span data-stu-id="4025a-119">New-AzureRmImageConfig</span></span>](/powershell/module/azurerm.resources/new-azurermimageconfig)                               | <span data-ttu-id="4025a-120">Crea un objeto de imagen configurable.</span><span class="sxs-lookup"><span data-stu-id="4025a-120">Creates a configurable image object.</span></span>                                                                                                                                                 |
| [<span data-ttu-id="4025a-121">Set-AzureRmImageOsDisk</span><span class="sxs-lookup"><span data-stu-id="4025a-121">Set-AzureRmImageOsDisk</span></span>](/powershell/module/azurerm.resources/set-azurermimageosdisk)                               | <span data-ttu-id="4025a-122">Establece las propiedades del disco de sistema operativo de hello en un objeto de imagen.</span><span class="sxs-lookup"><span data-stu-id="4025a-122">Sets hello operating system disk properties on an image object.</span></span>                                                                                                                        |
| [<span data-ttu-id="4025a-123">New-AzureRmImage</span><span class="sxs-lookup"><span data-stu-id="4025a-123">New-AzureRmImage</span></span>](/powershell/module/azurerm.resources/new-azurermimage)                                           | <span data-ttu-id="4025a-124">Crea una nueva imagen.</span><span class="sxs-lookup"><span data-stu-id="4025a-124">Creates a new image.</span></span>                                                                                                                                                                 |
| [<span data-ttu-id="4025a-125">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="4025a-125">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.resources/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="4025a-126">Crea una configuración de subred.</span><span class="sxs-lookup"><span data-stu-id="4025a-126">Creates a subnet configuration.</span></span> <span data-ttu-id="4025a-127">Esta configuración se utiliza con el proceso de creación de red virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="4025a-127">This configuration is used with hello virtual network creation process.</span></span>                                                                                |
| [<span data-ttu-id="4025a-128">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="4025a-128">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.resources/new-azurermvirtualnetwork)                         | <span data-ttu-id="4025a-129">Crea una red virtual.</span><span class="sxs-lookup"><span data-stu-id="4025a-129">Creates a virtual network.</span></span>                                                                                                                                                           |
| [<span data-ttu-id="4025a-130">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="4025a-130">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.resources/new-azurermpublicipaddress)                       | <span data-ttu-id="4025a-131">Crea una dirección IP pública.</span><span class="sxs-lookup"><span data-stu-id="4025a-131">Creates a public IP address.</span></span>                                                                                                                                                         |
| [<span data-ttu-id="4025a-132">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="4025a-132">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.resources/new-azurermnetworkinterface)                     | <span data-ttu-id="4025a-133">Crea una interfaz de red.</span><span class="sxs-lookup"><span data-stu-id="4025a-133">Creates a network interface.</span></span>                                                                                                                                                         |
| [<span data-ttu-id="4025a-134">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="4025a-134">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.resources/new-azurermnetworksecurityruleconfig)   | <span data-ttu-id="4025a-135">Crea configuración de regla de grupo de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="4025a-135">Creates a network security group rule configuration.</span></span> <span data-ttu-id="4025a-136">Esta configuración es toocreate usa una regla de NSG cuando se crea hello NSG.</span><span class="sxs-lookup"><span data-stu-id="4025a-136">This configuration is used toocreate an NSG rule when hello NSG is created.</span></span>                                                       |
| [<span data-ttu-id="4025a-137">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="4025a-137">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.resources/new-azurermnetworksecuritygroup)             | <span data-ttu-id="4025a-138">Crea un grupo de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="4025a-138">Creates a network security group.</span></span>                                                                                                                                                    |
| [<span data-ttu-id="4025a-139">Get-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="4025a-139">Get-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.resources/get-azurermvirtualnetwork)                         | <span data-ttu-id="4025a-140">Obtiene una red virtual en un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="4025a-140">Gets a virtual network in a resource group.</span></span>                                                                                                                                          |
| [<span data-ttu-id="4025a-141">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="4025a-141">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.resources/new-azurermvmconfig)                                     | <span data-ttu-id="4025a-142">Crea una configuración de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="4025a-142">Creates a VM configuration.</span></span> <span data-ttu-id="4025a-143">Esta configuración incluye diversa información, como el nombre de la máquina virtual, sistema el operativo y las credenciales administrativas.</span><span class="sxs-lookup"><span data-stu-id="4025a-143">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="4025a-144">configuración de Hola se utiliza durante la creación de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="4025a-144">hello configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="4025a-145">Set-AzureRmVMSourceImage</span><span class="sxs-lookup"><span data-stu-id="4025a-145">Set-AzureRmVMSourceImage</span></span>](/powershell/module/azurerm.resources/set-azurermvmsourceimage)                           | <span data-ttu-id="4025a-146">Especifica una imagen para una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="4025a-146">Specifies an image for a virtual machine.</span></span>                                                                                                                                            |
| [<span data-ttu-id="4025a-147">Set-AzureRmVMOSDisk</span><span class="sxs-lookup"><span data-stu-id="4025a-147">Set-AzureRmVMOSDisk</span></span>](/powershell/module/azurerm.resources/set-azurermvmosdisk)                                     | <span data-ttu-id="4025a-148">Establece las propiedades del disco de sistema operativo de hello en una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="4025a-148">Sets hello operating system disk properties on a virtual machine.</span></span>                                                                                                                      |
| [<span data-ttu-id="4025a-149">Set-AzureRmVMOperatingSystem</span><span class="sxs-lookup"><span data-stu-id="4025a-149">Set-AzureRmVMOperatingSystem</span></span>](/powershell/module/azurerm.resources/set-azurermvmoperatingsystem)                   | <span data-ttu-id="4025a-150">Establece las propiedades del disco de sistema operativo de hello en una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="4025a-150">Sets hello operating system disk properties on a virtual machine.</span></span>                                                                                                                      |
| [<span data-ttu-id="4025a-151">Add-AzureRmVMNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="4025a-151">Add-AzureRmVMNetworkInterface</span></span>](/powershell/module/azurerm.resources/add-azurermvmnetworkinterface)                 | <span data-ttu-id="4025a-152">Agrega una máquina virtual de red interfaz tooa.</span><span class="sxs-lookup"><span data-stu-id="4025a-152">Adds a network interface tooa virtual machine.</span></span>                                                                                                                                       |
| [<span data-ttu-id="4025a-153">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="4025a-153">New-AzureRmVM</span></span>](/powershell/module/azurerm.resources/new-azurermvm)                                                 | <span data-ttu-id="4025a-154">Cree una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="4025a-154">Create a virtual machine.</span></span>                                                                                                                                                            |
| [<span data-ttu-id="4025a-155">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="4025a-155">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup)                     | <span data-ttu-id="4025a-156">Quita un grupo de recursos y todos los recursos incluidos en él.</span><span class="sxs-lookup"><span data-stu-id="4025a-156">Removes a resource group and all resources contained within.</span></span>                                                                                                                         |

## <a name="next-steps"></a><span data-ttu-id="4025a-157">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4025a-157">Next steps</span></span>

<span data-ttu-id="4025a-158">Para obtener más información sobre el módulo de PowerShell de Azure de hello, consulte [documentación de Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="4025a-158">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="4025a-159">Ejemplos de secuencias de comandos de PowerShell de máquina virtual adicional pueden encontrarse en hello [documentación de la máquina virtual de Windows Azure](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4025a-159">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
