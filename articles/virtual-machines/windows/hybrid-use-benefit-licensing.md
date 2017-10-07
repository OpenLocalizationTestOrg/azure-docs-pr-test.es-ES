---
title: "aaaAzure híbrido ventaja de uso para cliente de Windows y Windows Server | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toomaximize su toobring de ventajas de Windows Software Assurance local licencias tooAzure"
services: virtual-machines-windows
documentationcenter: 
author: kmouss
manager: timlt
editor: 
ms.assetid: 332583b6-15a3-4efb-80c3-9082587828b0
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 5/26/2017
ms.author: xujing
ms.openlocfilehash: f24487320a60132aaf766a31f3e6f3726d4a3bd1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-hybrid-use-benefit-for-windows-server-and-windows-client"></a><span data-ttu-id="be29f-103">Ventaja de uso híbrido de Azure para Windows Server y cliente de Windows</span><span class="sxs-lookup"><span data-stu-id="be29f-103">Azure Hybrid Use Benefit for Windows Server and Windows Client</span></span>
<span data-ttu-id="be29f-104">Para los clientes con Software Assurance, ventaja de uso de Azure híbrida permite toouse sus licencias de Windows Server y cliente de Windows local y las máquinas de virtuales de Windows ejecución en Azure a bajo costo.</span><span class="sxs-lookup"><span data-stu-id="be29f-104">For customers with Software Assurance, Azure Hybrid Use Benefit allows you toouse your on-premises Windows Server and Windows Client licenses and run Windows virtual machines in Azure at a reduced cost.</span></span> <span data-ttu-id="be29f-105">La ventaja de uso híbrido de Azure para Windows Server incluye Windows Server 2008R2, Windows Server 2012, Windows Server 2012R2 y Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="be29f-105">Azure Hybrid Use Benefit for Windows Server includes Windows Server 2008R2, Windows Server 2012, Windows Server 2012R2, and Windows Server 2016.</span></span> <span data-ttu-id="be29f-106">Ventaja de uso híbrido de Azure para cliente de Windows incluye Windows 10.</span><span class="sxs-lookup"><span data-stu-id="be29f-106">Azure Hybrid Use Benefit for Windows Client includes Windows 10.</span></span> <span data-ttu-id="be29f-107">Para obtener más información, vea hello [página licencias de beneficio de uso de Azure híbrida](https://azure.microsoft.com/pricing/hybrid-use-benefit/).</span><span class="sxs-lookup"><span data-stu-id="be29f-107">For more information, please see hello [Azure Hybrid Use Benefit licensing page](https://azure.microsoft.com/pricing/hybrid-use-benefit/).</span></span>

>[!IMPORTANT]
><span data-ttu-id="be29f-108">Azure híbrida uso ventajas para cliente de Windows está actualmente en vista previa con imagen de Windows 10 de hello en hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="be29f-108">Azure Hybrid Use Benefits for Windows Client is currently in Preview using hello Windows 10 image in hello Azure Marketplace.</span></span> <span data-ttu-id="be29f-109">Solo los clientes de Enterprise con Windows 10 Enterprise E3/E5 por usuario o VDA de Windows por usuario (licencias de suscripción de usuario o licencias de suscripción de usuario de complemento) ("licencias aplicables") son válidos.</span><span class="sxs-lookup"><span data-stu-id="be29f-109">Only Enterprise customers with Windows 10 Enterprise E3/E5 per user or Windows VDA per user (User Subscription Licenses or Add-on User Subscription Licenses) (“Qualifying Licenses”) are eligible.</span></span>
>
>

## <a name="ways-toouse-azure-hybrid-use-benefit"></a><span data-ttu-id="be29f-110">Formas toouse ventaja de usar híbrida de Azure</span><span class="sxs-lookup"><span data-stu-id="be29f-110">Ways toouse Azure Hybrid Use Benefit</span></span>
<span data-ttu-id="be29f-111">Hay un par de maneras toodeploy máquinas virtuales de Windows con hello ventaja de usar híbrida de Azure:</span><span class="sxs-lookup"><span data-stu-id="be29f-111">There are a couple of different ways toodeploy Windows VMs with hello Azure Hybrid Use Benefit:</span></span>

1. <span data-ttu-id="be29f-112">Puede implementar máquinas virtuales a partir de [imágenes concretas de Marketplace](#deploy-a-vm-using-the-azure-marketplace) preconfiguradas con la ventaja de uso híbrido de Azure: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 y Windows Server 2008 SP1.</span><span class="sxs-lookup"><span data-stu-id="be29f-112">You can deploy VMs from [specific Marketplace images](#deploy-a-vm-using-the-azure-marketplace) that are pre-configured with Azure Hybrid Use Benefit - Windows Server 2016, Windows Server 2012R2, Windows Server 2012 and Windows Server 2008SP1.</span></span>
2. <span data-ttu-id="be29f-113">Puede [cargar una máquina virtual personalizada](#upload-a-windows-vhd) e [implementar mediante una plantilla de Resource Manager](#deploy-a-vm-via-resource-manager) o [Azure PowerShell](#detailed-powershell-deployment-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="be29f-113">You can [upload a custom VM](#upload-a-windows-vhd) and [deploy using a Resource Manager template](#deploy-a-vm-via-resource-manager) or [Azure PowerShell](#detailed-powershell-deployment-walkthrough).</span></span>

## <a name="deploy-a-vm-using-hello-azure-marketplace"></a><span data-ttu-id="be29f-114">Implementar una máquina virtual mediante hello Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="be29f-114">Deploy a VM using hello Azure Marketplace</span></span>
<span data-ttu-id="be29f-115">Las imágenes siguientes están disponibles en hello Marketplace configurado previamente con la ventaja de usar híbrida de Azure: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 y Windows Server 2008SP1.</span><span class="sxs-lookup"><span data-stu-id="be29f-115">Following images are available in hello Marketplace pre-configured with Azure Hybrid Use Benefit: Windows Server 2016, Windows Server 2012R2, Windows Server 2012 and Windows Server 2008SP1.</span></span> <span data-ttu-id="be29f-116">Estas imágenes se pueden implementar directamente de hello portal de Azure, las plantillas de administrador de recursos o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="be29f-116">These images can be deployed directly from hello Azure portal, Resource Manager templates, or Azure PowerShell.</span></span>

<span data-ttu-id="be29f-117">Puede implementar estas imágenes directamente desde Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="be29f-117">You can deploy these images directly from hello Azure portal.</span></span> <span data-ttu-id="be29f-118">Para su uso en las plantillas de administrador de recursos y con Azure PowerShell, vea lista Hola de imágenes de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="be29f-118">For use in Resource Manager templates and with Azure PowerShell, view hello list of images as follows:</span></span>

<span data-ttu-id="be29f-119">Para Windows Server:</span><span class="sxs-lookup"><span data-stu-id="be29f-119">For Windows Server:</span></span>
```powershell
Get-AzureRmVMImagesku -Location westus -PublisherName MicrosoftWindowsServer -Offer WindowsServer
```
- <span data-ttu-id="be29f-120">2016-Datacenter versión 2016.127.20170406 o superior</span><span class="sxs-lookup"><span data-stu-id="be29f-120">2016-Datacenter version 2016.127.20170406 or above</span></span>

- <span data-ttu-id="be29f-121">2012-R2-Datacenter versión 4.127.20170406 o superior</span><span class="sxs-lookup"><span data-stu-id="be29f-121">2012-R2-Datacenter version 4.127.20170406 or above</span></span>

- <span data-ttu-id="be29f-122">2012-Datacenter versión 3.127.20170406 o superior</span><span class="sxs-lookup"><span data-stu-id="be29f-122">2012-Datacenter version 3.127.20170406 or above</span></span>

- <span data-ttu-id="be29f-123">2008-R2-SP1 versión 2.127.20170406 o superior</span><span class="sxs-lookup"><span data-stu-id="be29f-123">2008-R2-SP1 version 2.127.20170406 or above</span></span>

<span data-ttu-id="be29f-124">Para cliente de Windows:</span><span class="sxs-lookup"><span data-stu-id="be29f-124">For Windows Client:</span></span>
```powershell
Get-AzureRMVMImageSku -Location "West US" -Publisher "MicrosoftWindowsServer" `
    -Offer "Windows-HUB"
```

## <a name="upload-a-windows-server-vhd"></a><span data-ttu-id="be29f-125">Carga de un VHD de Windows Server</span><span class="sxs-lookup"><span data-stu-id="be29f-125">Upload a Windows Server VHD</span></span>
<span data-ttu-id="be29f-126">toodeploy una VM de Windows Server en Azure, primero debe toocreate un disco duro virtual que contiene la compilación de Windows base.</span><span class="sxs-lookup"><span data-stu-id="be29f-126">toodeploy a Windows Server VM in Azure, you first need toocreate a VHD that contains your base Windows build.</span></span> <span data-ttu-id="be29f-127">Este disco duro virtual debe estar preparado correctamente a través de Sysprep para poder cargar tooAzure.</span><span class="sxs-lookup"><span data-stu-id="be29f-127">This VHD must be appropriately prepared via Sysprep before you upload it tooAzure.</span></span> <span data-ttu-id="be29f-128">También puede [leer más acerca de los requisitos de disco duro virtual de Hola y el proceso de Sysprep](upload-generalized-managed.md) y [compatibilidad con Sysprep para Roles de servidor](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles).</span><span class="sxs-lookup"><span data-stu-id="be29f-128">You can [read more about hello VHD requirements and Sysprep process](upload-generalized-managed.md) and [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles).</span></span> <span data-ttu-id="be29f-129">Respaldar Hola VM antes de ejecutar Sysprep.</span><span class="sxs-lookup"><span data-stu-id="be29f-129">Back up hello VM before running Sysprep.</span></span> 

<span data-ttu-id="be29f-130">Asegúrese de que tiene [instalado y está configurado hello más reciente Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="be29f-130">Make sure you have [installed and configured hello latest Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="be29f-131">Una vez que ha preparado el disco duro virtual, cargarlo Hola VHD tooyour almacenamiento de Azure cuenta con hello `Add-AzureRmVhd` cmdlet como sigue:</span><span class="sxs-lookup"><span data-stu-id="be29f-131">Once you have prepared your VHD, upload hello VHD tooyour Azure Storage account using hello `Add-AzureRmVhd` cmdlet as follows:</span></span>

```powershell
Add-AzureRmVhd -ResourceGroupName "myResourceGroup" -LocalFilePath "C:\Path\To\myvhd.vhd" `
    -Destination "https://mystorageaccount.blob.core.windows.net/vhds/myvhd.vhd"
```

> [!NOTE]
> <span data-ttu-id="be29f-132">Microsoft SQL Server, SharePoint Server y Dynamics también pueden utilizar una concesión de licencias de Software Assurance.</span><span class="sxs-lookup"><span data-stu-id="be29f-132">Microsoft SQL Server, SharePoint Server, and Dynamics can also utilize your Software Assurance licensing.</span></span> <span data-ttu-id="be29f-133">Imagen de Windows Server tooprepare Hola todavía es necesario al instalar los componentes de aplicación y proporciona las claves de licencia según corresponda y, a continuación, cargar tooAzure de imagen de disco de Hola.</span><span class="sxs-lookup"><span data-stu-id="be29f-133">You still need tooprepare hello Windows Server image by installing your application components and providing license keys accordingly, then uploading hello disk image tooAzure.</span></span> <span data-ttu-id="be29f-134">Revise la documentación adecuada de Hola para ejecutar Sysprep con la aplicación, como [consideraciones para instalar SQL Server con Sysprep](https://msdn.microsoft.com/library/ee210754.aspx) o [generar una imagen de referencia de SharePoint Server 2016 (Sysprep)](http://social.technet.microsoft.com/wiki/contents/articles/33789.build-a-sharepoint-server-2016-reference-image-sysprep.aspx).</span><span class="sxs-lookup"><span data-stu-id="be29f-134">Review hello appropriate documentation for running Sysprep with your application, such as [Considerations for Installing SQL Server using Sysprep](https://msdn.microsoft.com/library/ee210754.aspx) or [Build a SharePoint Server 2016 Reference Image (Sysprep)](http://social.technet.microsoft.com/wiki/contents/articles/33789.build-a-sharepoint-server-2016-reference-image-sysprep.aspx).</span></span>
>
>

<span data-ttu-id="be29f-135">También puede obtener más información [Hola VHD tooAzure proceso de carga](upload-generalized-managed.md#upload-the-vhd-to-your-storage-account)</span><span class="sxs-lookup"><span data-stu-id="be29f-135">You can also read more about [uploading hello VHD tooAzure process](upload-generalized-managed.md#upload-the-vhd-to-your-storage-account)</span></span>


## <a name="deploy-a-vm-via-resource-manager-template"></a><span data-ttu-id="be29f-136">Implementación de una máquina virtual a través de una plantilla de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="be29f-136">Deploy a VM via Resource Manager Template</span></span>
<span data-ttu-id="be29f-137">En las plantillas de Resource Manager, se puede especificar un parámetro adicional para `licenseType` .</span><span class="sxs-lookup"><span data-stu-id="be29f-137">Within your Resource Manager templates, an additional parameter for `licenseType` can be specified.</span></span> <span data-ttu-id="be29f-138">En [Creación de plantillas de Azure Resource Manager](../../resource-group-authoring-templates.md), puede encontrar más información al respecto.</span><span class="sxs-lookup"><span data-stu-id="be29f-138">You can read more about [authoring Azure Resource Manager templates](../../resource-group-authoring-templates.md).</span></span> <span data-ttu-id="be29f-139">Una vez que tenga su tooAzure VHD cargado, modificar, el Administrador de recursos tooinclude Hola licencia tipo de plantilla como parte del programa Hola a proveedor de proceso e implementar la plantilla de forma habitual:</span><span class="sxs-lookup"><span data-stu-id="be29f-139">Once you have your VHD uploaded tooAzure, edit you Resource Manager template tooinclude hello license type as part of hello compute provider and deploy your template as normal:</span></span>

<span data-ttu-id="be29f-140">Para Windows Server:</span><span class="sxs-lookup"><span data-stu-id="be29f-140">For Windows Server:</span></span>
```json
"properties": {  
   "licenseType": "Windows_Server",
   "hardwareProfile": {
        "vmSize": "[variables('vmSize')]"
   }
```

<span data-ttu-id="be29f-141">Para con la imagen de Marketplace de Azure solo pueden ser toouse de cliente de Windows:</span><span class="sxs-lookup"><span data-stu-id="be29f-141">For Windows Client toouse with Azure Marketplace Image only:</span></span>
```json
"properties": {  
   "licenseType": "Windows_Client",
   "hardwareProfile": {
        "vmSize": "[variables('vmSize')]"
   }
```

## <a name="deploy-a-vm-via-powershell-quickstart"></a><span data-ttu-id="be29f-142">Implementación de una máquina virtual a través del inicio rápido de PowerShell</span><span class="sxs-lookup"><span data-stu-id="be29f-142">Deploy a VM via PowerShell quickstart</span></span>
<span data-ttu-id="be29f-143">Cuando se implementa una máquina virtual de Windows Server mediante PowerShell, se dispone de un parámetro adicional para `-LicenseType`.</span><span class="sxs-lookup"><span data-stu-id="be29f-143">When deploying your Windows Server VM via PowerShell, you have an additional parameter for `-LicenseType`.</span></span> <span data-ttu-id="be29f-144">Una vez que tenga su tooAzure VHD cargado, crear una VM con `New-AzureRmVM` y especificar el tipo de licencia de hello como sigue:</span><span class="sxs-lookup"><span data-stu-id="be29f-144">Once you have your VHD uploaded tooAzure, you create a VM using `New-AzureRmVM` and specify hello licensing type as follows:</span></span>

<span data-ttu-id="be29f-145">Para Windows Server:</span><span class="sxs-lookup"><span data-stu-id="be29f-145">For Windows Server:</span></span>
```powershell
New-AzureRmVM -ResourceGroupName "myResourceGroup" -Location "West US" -VM $vm -LicenseType "Windows_Server"
```

<span data-ttu-id="be29f-146">Para con la imagen de Marketplace de Azure solo pueden ser toouse de cliente de Windows:</span><span class="sxs-lookup"><span data-stu-id="be29f-146">For Windows Client toouse with Azure Marketplace Image only:</span></span>
```powershell
New-AzureRmVM -ResourceGroupName "myResourceGroup" -Location "West US" -VM $vm -LicenseType "Windows_Client"
```

<span data-ttu-id="be29f-147">También puede [leer un tutorial más detallado sobre la implementación de una máquina virtual en Azure a través de PowerShell](hybrid-use-benefit-licensing.md#detailed-powershell-deployment-walkthrough) siguiente o leer una guía más descriptiva en Hola pasos diferentes demasiado[crear una máquina virtual de Windows mediante el Administrador de recursos y PowerShell](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="be29f-147">You can [read a more detailed walkthrough on deploying a VM in Azure via PowerShell](hybrid-use-benefit-licensing.md#detailed-powershell-deployment-walkthrough) below, or read a more descriptive guide on hello different steps too[create a Windows VM using Resource Manager and PowerShell](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


## <a name="verify-your-vm-is-utilizing-hello-licensing-benefit"></a><span data-ttu-id="be29f-148">Compruebe que la máquina virtual está utilizando la ventaja de licencias de Hola</span><span class="sxs-lookup"><span data-stu-id="be29f-148">Verify your VM is utilizing hello licensing benefit</span></span>
<span data-ttu-id="be29f-149">Una vez que se ha implementado la máquina virtual a través de PowerShell de Hola o método de implementación del Administrador de recursos, comprobar el tipo de licencia de hello con `Get-AzureRmVM` como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="be29f-149">Once you have deployed your VM through either hello PowerShell or Resource Manager deployment method, verify hello license type with `Get-AzureRmVM` as follows:</span></span>

```powershell
Get-AzureRmVM -ResourceGroup "myResourceGroup" -Name "myVM"
```

<span data-ttu-id="be29f-150">Hola de salida es similar toohello siguiente ejemplo para Windows Server:</span><span class="sxs-lookup"><span data-stu-id="be29f-150">hello output is similar toohello following example for Windows Server:</span></span>

```powershell
Type                     : Microsoft.Compute/virtualMachines
Location                 : westus
LicenseType              : Windows_Server
```

<span data-ttu-id="be29f-151">Este resultado se compara con las Hola que VM siguiente implementa sin licencias ventaja de usar híbrida de Azure, como una máquina virtual implementada directamente desde Hola Galería de Azure:</span><span class="sxs-lookup"><span data-stu-id="be29f-151">This output contrasts with hello following VM deployed without Azure Hybrid Use Benefit licensing, such as a VM deployed straight from hello Azure Gallery:</span></span>

```powershell
Type                     : Microsoft.Compute/virtualMachines
Location                 : westus
LicenseType              :
```

## <a name="detailed-powershell-deployment-walkthrough"></a><span data-ttu-id="be29f-152">Tutorial de implementación de PowerShell detallado</span><span class="sxs-lookup"><span data-stu-id="be29f-152">Detailed PowerShell deployment walkthrough</span></span>
<span data-ttu-id="be29f-153">siguiente Hola había detallada mostrar pasos de PowerShell una implementación completa de una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="be29f-153">hello following detailed PowerShell steps show a full deployment of a VM.</span></span> <span data-ttu-id="be29f-154">Puede leer más contexto como cmdlets real toohello y diferentes componentes que se creen en [crear una máquina virtual de Windows mediante el Administrador de recursos y PowerShell](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="be29f-154">You can read more context as toohello actual cmdlets and different components being created in [Create a Windows VM using Resource Manager and PowerShell](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="be29f-155">Con estos pasos, crea el grupo de recursos, la cuenta de almacenamiento y las redes virtuales, definirá la máquina virtual y, por último, la creará.</span><span class="sxs-lookup"><span data-stu-id="be29f-155">You step through creating your resource group, storage account, and virtual networking, then define your VM and finally create your VM.</span></span>

<span data-ttu-id="be29f-156">En primer lugar, obtenga credenciales de forma segura, establezca una ubicación y defina un nombre para el grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="be29f-156">First, securely obtain credentials, set a location, and resource group name:</span></span>

```powershell
$cred = Get-Credential
$location = "West US"
$resourceGroupName = "myResourceGroup"
```

<span data-ttu-id="be29f-157">Cree una dirección IP pública:</span><span class="sxs-lookup"><span data-stu-id="be29f-157">Create a public IP:</span></span>

```powershell
$publicIPName = "myPublicIP"
$publicIP = New-AzureRmPublicIpAddress -Name $publicIPName -ResourceGroupName $resourceGroupName `
    -Location $location -AllocationMethod "Dynamic"
```

<span data-ttu-id="be29f-158">Defina la subred, la NIC y la red virtual:</span><span class="sxs-lookup"><span data-stu-id="be29f-158">Define your subnet, NIC, and VNET:</span></span>

```powershell
$subnetName = "mySubnet"
$nicName = "myNIC"
$vnetName = "myVnet"
$subnetconfig = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/8
$vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $resourceGroupName -Location $location `
    -AddressPrefix 10.0.0.0/8 -Subnet $subnetconfig
$nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $resourceGroupName -Location $location `
    -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $publicIP.Id
```

<span data-ttu-id="be29f-159">Asigne un nombre a la máquina virtual y cree una configuración de máquina virtual:</span><span class="sxs-lookup"><span data-stu-id="be29f-159">Name your VM and create a VM config:</span></span>

```powershell
$vmName = "myVM"
$vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize "Standard_A1"
```

<span data-ttu-id="be29f-160">Defina el sistema operativo:</span><span class="sxs-lookup"><span data-stu-id="be29f-160">Define your OS:</span></span>

```powershell
$computerName = "myVM"
$vm = Set-AzureRmVMOperatingSystem -VM $vmConfig -Windows -ComputerName $computerName -Credential $cred `
    -ProvisionVMAgent -EnableAutoUpdate
```

<span data-ttu-id="be29f-161">Agregue su toohello NIC virtual:</span><span class="sxs-lookup"><span data-stu-id="be29f-161">Add your NIC toohello VM:</span></span>

```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

<span data-ttu-id="be29f-162">Definir toouse de cuenta de almacenamiento de hello:</span><span class="sxs-lookup"><span data-stu-id="be29f-162">Define hello storage account toouse:</span></span>

```powershell
$storageAcc = Get-AzureRmStorageAccount -ResourceGroupName $resourceGroupName -AccountName mystorageaccount
```

<span data-ttu-id="be29f-163">Cargar un VHD, preparado adecuadamente y asociar tooyour máquina virtual para su uso:</span><span class="sxs-lookup"><span data-stu-id="be29f-163">Upload your VHD, suitably prepared, and attach tooyour VM for use:</span></span>

```powershell
$osDiskName = "licensing.vhd"
$osDiskUri = '{0}vhds/{1}{2}.vhd' -f $storageAcc.PrimaryEndpoints.Blob.ToString(), $vmName.ToLower(), $osDiskName
$urlOfUploadedImageVhd = "https://mystorageaccount.blob.core.windows.net/vhd/myvhd.vhd"
$vm = Set-AzureRmVMOSDisk -VM $vm -Name $osDiskName -VhdUri $osDiskUri -CreateOption FromImage `
    -SourceImageUri $urlOfUploadedImageVhd -Windows
```

<span data-ttu-id="be29f-164">Finalmente, cree la máquina virtual y definir Hola licencias tipo tooutilize ventaja de usar híbrida de Azure:</span><span class="sxs-lookup"><span data-stu-id="be29f-164">Finally, create your VM and define hello licensing type tooutilize Azure Hybrid Use Benefit:</span></span>

<span data-ttu-id="be29f-165">Para Windows Server:</span><span class="sxs-lookup"><span data-stu-id="be29f-165">For Windows Server:</span></span>
```powershell
New-AzureRmVM -ResourceGroupName $resourceGroupName -Location $location -VM $vm -LicenseType "Windows_Server"
```

## <a name="deploy-a-virtual-machine-scale-set-via-resource-manager-template"></a><span data-ttu-id="be29f-166">Implemente un conjunto de escalado de máquinas virtuales con una plantilla de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="be29f-166">Deploy a virtual machine scale set via Resource Manager template</span></span>
<span data-ttu-id="be29f-167">En las plantillas de Resource Manager del conjunto de escalado de máquinas virtuales, se puede especificar un parámetro adicional para `licenseType`.</span><span class="sxs-lookup"><span data-stu-id="be29f-167">Within your VMSS Resource Manager templates, an additional parameter for `licenseType` must be specified.</span></span> <span data-ttu-id="be29f-168">En [Creación de plantillas de Azure Resource Manager](../../resource-group-authoring-templates.md), puede encontrar más información al respecto.</span><span class="sxs-lookup"><span data-stu-id="be29f-168">You can read more about [authoring Azure Resource Manager templates](../../resource-group-authoring-templates.md).</span></span> <span data-ttu-id="be29f-169">Editar la propiedad Resource Manager plantilla tooinclude Hola licenseType como parte de virtualMachineProfile del conjunto de escalas de Hola e implementar la plantilla como normal: vea el ejemplo siguiente utiliza la imagen de Windows Server 2016:</span><span class="sxs-lookup"><span data-stu-id="be29f-169">Edit your Resource Manager template tooinclude hello licenseType property as part of hello scale set’s virtualMachineProfile and deploy your template as normal - see example below using 2016 Windows Server image:</span></span>


```json
"virtualMachineProfile": {
    "storageProfile": {
        "osDisk": {
            "createOption": "FromImage"
        },
        "imageReference": {
            "publisher": "MicrosoftWindowsServer",
            "offer": "WindowsServer",
            "sku": "2016-Datacenter",
            "version": "latest"
        }
    },
    "licenseType": "Windows_Server",
    "osProfile": {
            "computerNamePrefix": "[parameters('vmssName')]",
            "adminUsername": "[parameters('adminUsername')]",
            "adminPassword": "[parameters('adminPassword')]"
    }
```

> [!NOTE]
> <span data-ttu-id="be29f-170">Próximamente estará disponible la compatibilidad para implementar un conjunto de escalado de máquinas virtuales con ventajas AHUB a través de PowerShell y otras herramientas SDK.</span><span class="sxs-lookup"><span data-stu-id="be29f-170">Support for deploying a virtual machine scale set with AHUB benefits through PowerShell and other SDK tools is coming soon.</span></span>
>

## <a name="next-steps"></a><span data-ttu-id="be29f-171">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="be29f-171">Next steps</span></span>
<span data-ttu-id="be29f-172">Más información sobre las [ventajas del uso híbrido de Azure](https://azure.microsoft.com/pricing/hybrid-use-benefit/).</span><span class="sxs-lookup"><span data-stu-id="be29f-172">Read more about [Azure Hybrid Use Benefit licensing](https://azure.microsoft.com/pricing/hybrid-use-benefit/).</span></span>

<span data-ttu-id="be29f-173">Más información sobre el [uso de plantillas de Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="be29f-173">Learn more about [using Resource Manager templates](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="be29f-174">Obtenga más información sobre [ventaja de usar híbrida de Azure y Azure Site Recovery Asegúrese de migración de aplicaciones tooAzure aún más rentable](https://azure.microsoft.com/blog/hybrid-use-benefit-migration-with-asr/).</span><span class="sxs-lookup"><span data-stu-id="be29f-174">Learn more about [Azure Hybrid Use Benefit and Azure Site Recovery make migrating applications tooAzure even more cost-effective](https://azure.microsoft.com/blog/hybrid-use-benefit-migration-with-asr/).</span></span>
