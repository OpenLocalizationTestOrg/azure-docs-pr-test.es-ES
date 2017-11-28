---
title: "Carga de un VHD generalizado para crear varias máquinas virtuales en Azure | Microsoft Docs"
description: "Cargue un VHD generalizado en una cuenta de Azure Storage a fin de crear una máquina virtual de Windows para usarla con el modelo de implementación de Resource Manager."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: cynthn
ms.openlocfilehash: e6fc49855b449a7723a7f8a0c1c41516b3a44ee5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="upload-a-generalized-vhd-to-azure-to-create-a-new-vm"></a><span data-ttu-id="3c1ae-103">Carga de un VHD generalizado en Azure para crear una máquina virtual nueva</span><span class="sxs-lookup"><span data-stu-id="3c1ae-103">Upload a generalized VHD to Azure to create a new VM</span></span>

<span data-ttu-id="3c1ae-104">En este tema se explica cómo cargar un disco no administrado generalizado en una cuenta de almacenamiento para crear después una máquina virtual nueva con el disco cargado.</span><span class="sxs-lookup"><span data-stu-id="3c1ae-104">This topic covers uploading a generalized unmanaged disk to a storage account and then creating a new VM using the uploaded disk.</span></span> <span data-ttu-id="3c1ae-105">Con Sysprep se elimina toda la información personal de la cuenta de una imagen de un VHD generalizado.</span><span class="sxs-lookup"><span data-stu-id="3c1ae-105">A generalized VHD image has had all of your personal account information removed using Sysprep.</span></span> 

<span data-ttu-id="3c1ae-106">Si desea crear una máquina virtual a partir de un VHD especializado en una cuenta de almacenamiento, consulte [Crear una VM a partir de un VHD especializado](sa-create-vm-specialized.md).</span><span class="sxs-lookup"><span data-stu-id="3c1ae-106">If you want to create a VM from a specialized VHD in a storage account, see [Create a VM from a specialized VHD](sa-create-vm-specialized.md).</span></span>

<span data-ttu-id="3c1ae-107">En este tema se aborda cómo usar las cuentas de almacenamiento, pero se recomienda a los clientes que utilicen Managed Disks.</span><span class="sxs-lookup"><span data-stu-id="3c1ae-107">This topic covers using storage accounts, but we recommend customers move to using Managed Disks instead.</span></span> <span data-ttu-id="3c1ae-108">Para ver un tutorial completo sobre cómo preparar, cargar y crear una nueva máquina virtual con Managed Disks, vea [Creación de una VM nueva a partir de un VHD generalizado cargado en Azure a través de Managed Disks](upload-generalized-managed.md).</span><span class="sxs-lookup"><span data-stu-id="3c1ae-108">For a complete walk-through of how to prepare, upload and create a new VM using managed disks, see [Create a new VM from a generalized VHD uploaded to Azure using Managed Disks](upload-generalized-managed.md).</span></span>



## <a name="prepare-the-vm"></a><span data-ttu-id="3c1ae-109">Preparación de la VM</span><span class="sxs-lookup"><span data-stu-id="3c1ae-109">Prepare the VM</span></span>

<span data-ttu-id="3c1ae-110">La información personal de la cuenta se elimina de un VHD generalizado mediante Sysprep.</span><span class="sxs-lookup"><span data-stu-id="3c1ae-110">A generalized VHD has had all of your personal account information removed using Sysprep.</span></span> <span data-ttu-id="3c1ae-111">Si tiene previsto usar VHD como una imagen desde la que crear nuevas VM, debe:</span><span class="sxs-lookup"><span data-stu-id="3c1ae-111">If you intend to use the VHD as an image to create new VMs from, you should:</span></span>
  
  * <span data-ttu-id="3c1ae-112">[Preparar de un VHD de Windows para cargar en Azure](prepare-for-upload-vhd-image.md).</span><span class="sxs-lookup"><span data-stu-id="3c1ae-112">[Prepare a Windows VHD to upload to Azure](prepare-for-upload-vhd-image.md).</span></span> 
  * <span data-ttu-id="3c1ae-113">Generalización de una máquina virtual con Sysprep</span><span class="sxs-lookup"><span data-stu-id="3c1ae-113">Generalize the virtual machine using Sysprep</span></span>

### <a name="generalize-a-windows-virtual-machine-using-sysprep"></a><span data-ttu-id="3c1ae-114">Generalización de una máquina virtual Windows con Sysprep</span><span class="sxs-lookup"><span data-stu-id="3c1ae-114">Generalize a Windows virtual machine using Sysprep</span></span>
<span data-ttu-id="3c1ae-115">En esta sección se muestra cómo generalizar la máquina virtual Windows para usarla como imagen.</span><span class="sxs-lookup"><span data-stu-id="3c1ae-115">This section shows you how to generalize your Windows virtual machine for use as an image.</span></span> <span data-ttu-id="3c1ae-116">Entre otras características, Sysprep elimina toda la información personal de la cuenta y prepara, entre otras cosas, la máquina para usarse como imagen.</span><span class="sxs-lookup"><span data-stu-id="3c1ae-116">Sysprep removes all your personal account information, among other things, and prepares the machine to be used as an image.</span></span> <span data-ttu-id="3c1ae-117">Para obtener más información sobre Sysprep, vea [Uso de Sysprep: Introducción](http://technet.microsoft.com/library/bb457073.aspx).</span><span class="sxs-lookup"><span data-stu-id="3c1ae-117">For details about Sysprep, see [How to Use Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span>

<span data-ttu-id="3c1ae-118">Asegúrese de que los roles de servidor que se ejecutan en la máquina sean compatibles con Sysprep.</span><span class="sxs-lookup"><span data-stu-id="3c1ae-118">Make sure the server roles running on the machine are supported by Sysprep.</span></span> <span data-ttu-id="3c1ae-119">Para más información, consulte [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span><span class="sxs-lookup"><span data-stu-id="3c1ae-119">For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3c1ae-120">Si ejecuta Sysprep antes de cargar el VHD en Azure por primera vez, asegúrese de que tiene [preparada la máquina virtual](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) antes de ejecutar Sysprep.</span><span class="sxs-lookup"><span data-stu-id="3c1ae-120">If you are running Sysprep before uploading your VHD to Azure for the first time, make sure you have [prepared your VM](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before running Sysprep.</span></span> 
> 
> 

1. <span data-ttu-id="3c1ae-121">Inicie sesión en la máquina virtual de Windows.</span><span class="sxs-lookup"><span data-stu-id="3c1ae-121">Sign in to the Windows virtual machine.</span></span>
2. <span data-ttu-id="3c1ae-122">Abra una ventana del símbolo del sistema como administrador.</span><span class="sxs-lookup"><span data-stu-id="3c1ae-122">Open the Command Prompt window as an administrator.</span></span> <span data-ttu-id="3c1ae-123">Cambie el directorio a **%windir%\system32\sysprep** y, después, ejecute `sysprep.exe`.</span><span class="sxs-lookup"><span data-stu-id="3c1ae-123">Change the directory to **%windir%\system32\sysprep**, and then run `sysprep.exe`.</span></span>
3. <span data-ttu-id="3c1ae-124">En **Herramienta de preparación del sistema**, seleccione **Iniciar la Configuración rápida (OOBE)** y asegúrese de que la casilla **Generalizar** está activada.</span><span class="sxs-lookup"><span data-stu-id="3c1ae-124">In the **System Preparation Tool** dialog box, select **Enter System Out-of-Box Experience (OOBE)**, and make sure that the **Generalize** check box is selected.</span></span>
4. <span data-ttu-id="3c1ae-125">En **Opciones de apagado**, seleccione **Apagar**.</span><span class="sxs-lookup"><span data-stu-id="3c1ae-125">In **Shutdown Options**, select **Shutdown**.</span></span>
5. <span data-ttu-id="3c1ae-126">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="3c1ae-126">Click **OK**.</span></span>
   
    ![Iniciar Sysprep](./media/upload-generalized-managed/sysprepgeneral.png)
6. <span data-ttu-id="3c1ae-128">Cuando Sysprep finaliza, apaga la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="3c1ae-128">When Sysprep completes, it shuts down the virtual machine.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="3c1ae-129">No reinicie la máquina virtual hasta que haya terminado de cargar el VHD en Azure o de crear una imagen de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="3c1ae-129">Do not restart the VM until you are done uploading the VHD to Azure or creating an image from the VM.</span></span> <span data-ttu-id="3c1ae-130">Si la máquina virtual se reinicia accidentalmente, ejecute Sysprep para generalizarla de nuevo.</span><span class="sxs-lookup"><span data-stu-id="3c1ae-130">If the VM accidentally gets restarted, run Sysprep to generalize it again.</span></span>
> 
> 


## <a name="upload-the-vhd"></a><span data-ttu-id="3c1ae-131">Carga del disco duro virtual</span><span class="sxs-lookup"><span data-stu-id="3c1ae-131">Upload the VHD</span></span>

<span data-ttu-id="3c1ae-132">Cargue el VHD en una cuenta de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="3c1ae-132">Upload the VHD to an Azure storage account.</span></span>

### <a name="log-in-to-azure"></a><span data-ttu-id="3c1ae-133">Inicie sesión en Azure.</span><span class="sxs-lookup"><span data-stu-id="3c1ae-133">Log in to Azure</span></span>
<span data-ttu-id="3c1ae-134">Si todavía no la ha instalado la versión 1.4 de PowerShell u otra superior, consulte [Cómo instalar y configurar Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="3c1ae-134">If you don't already have PowerShell version 1.4 or above installed, read [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

1. <span data-ttu-id="3c1ae-135">Abra Azure PowerShell e inicie sesión en la cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="3c1ae-135">Open Azure PowerShell and sign in to your Azure account.</span></span> <span data-ttu-id="3c1ae-136">Se abrirá una ventana emergente para que escriba sus credenciales de cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="3c1ae-136">A pop-up window opens for you to enter your Azure account credentials.</span></span>
   
    ```powershell
    Login-AzureRmAccount
    ```
2. <span data-ttu-id="3c1ae-137">Obtenga los identificadores de suscripción para las suscripciones disponibles.</span><span class="sxs-lookup"><span data-stu-id="3c1ae-137">Get the subscription IDs for your available subscriptions.</span></span>
   
    ```powershell
    Get-AzureRmSubscription
    ```
3. <span data-ttu-id="3c1ae-138">Establezca la suscripción correcta con el identificador de suscripción.</span><span class="sxs-lookup"><span data-stu-id="3c1ae-138">Set the correct subscription using the subscription ID.</span></span> <span data-ttu-id="3c1ae-139">Reemplace `<subscriptionID>` con el identificador de la suscripción correcta.</span><span class="sxs-lookup"><span data-stu-id="3c1ae-139">Replace `<subscriptionID>` with the ID of the correct subscription.</span></span>
   
    ```powershell
    Select-AzureRmSubscription -SubscriptionId "<subscriptionID>"
    ```

### <a name="get-the-storage-account"></a><span data-ttu-id="3c1ae-140">Obtención de la cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="3c1ae-140">Get the storage account</span></span>
<span data-ttu-id="3c1ae-141">Necesita una cuenta de almacenamiento de Azure para almacenar la imagen de VM cargada.</span><span class="sxs-lookup"><span data-stu-id="3c1ae-141">You need a storage account in Azure to store the uploaded VM image.</span></span> <span data-ttu-id="3c1ae-142">Puede usar una cuenta de almacenamiento existente o crear una nueva.</span><span class="sxs-lookup"><span data-stu-id="3c1ae-142">You can either use an existing storage account or create a new one.</span></span> 

<span data-ttu-id="3c1ae-143">Para mostrar las cuentas de almacenamiento disponibles, escriba:</span><span class="sxs-lookup"><span data-stu-id="3c1ae-143">To show the available storage accounts, type:</span></span>

```powershell
Get-AzureRmStorageAccount
```

<span data-ttu-id="3c1ae-144">Si desea utilizar una cuenta de almacenamiento existente, puede continuar con la sección [Carga de la imagen de VM en la cuenta de almacenamiento](#upload-the-vm-vhd-to-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="3c1ae-144">If you want to use an existing storage account, proceed to the [Upload the VM image](#upload-the-vm-vhd-to-your-storage-account) section.</span></span>

<span data-ttu-id="3c1ae-145">Si necesita crear una nueva cuenta de almacenamiento, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="3c1ae-145">If you need to create a storage account, follow these steps:</span></span>

1. <span data-ttu-id="3c1ae-146">Necesita el nombre del grupo de recursos donde se debe crear la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="3c1ae-146">You need the name of the resource group where the storage account should be created.</span></span> <span data-ttu-id="3c1ae-147">Para averiguar todos los grupos de recursos que están en la suscripción, escriba:</span><span class="sxs-lookup"><span data-stu-id="3c1ae-147">To find out all the resource groups that are in your subscription, type:</span></span>
   
    ```powershell
    Get-AzureRmResourceGroup
    ```

    <span data-ttu-id="3c1ae-148">Para crear un grupo de recursos denominado **myResourceGroup** en la región **Oeste de EE. UU.**, escriba:</span><span class="sxs-lookup"><span data-stu-id="3c1ae-148">To create a resource group named **myResourceGroup** in the **West US** region, type:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "West US"
    ```

2. <span data-ttu-id="3c1ae-149">Cree una cuenta de almacenamiento denominada **mystorageaccount** en este grupo de recursos con el cmdlet [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount):</span><span class="sxs-lookup"><span data-stu-id="3c1ae-149">Create a storage account named **mystorageaccount** in this resource group by using the [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:</span></span>
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "West US" `
        -SkuName "Standard_LRS" -Kind "Storage"
    ```
 
### <a name="start-the-upload"></a><span data-ttu-id="3c1ae-150">Inicio de la carga</span><span class="sxs-lookup"><span data-stu-id="3c1ae-150">Start the upload</span></span> 

<span data-ttu-id="3c1ae-151">Utilice el cmdlet [Add-AzureRmVhd](/powershell/module/azurerm.compute/add-azurermvhd) para cargar la imagen en un contenedor de su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="3c1ae-151">Use the [Add-AzureRmVhd](/powershell/module/azurerm.compute/add-azurermvhd) cmdlet to upload the image to a container in your storage account.</span></span> <span data-ttu-id="3c1ae-152">En este ejemplo se carga el archivo **myVHD.vhd** de `"C:\Users\Public\Documents\Virtual hard disks\"` para una cuenta de almacenamiento denominada **mystorageaccount** en el grupo de recursos **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="3c1ae-152">This example uploads the file **myVHD.vhd** from `"C:\Users\Public\Documents\Virtual hard disks\"` to a storage account named **mystorageaccount** in the **myResourceGroup** resource group.</span></span> <span data-ttu-id="3c1ae-153">El archivo se colocará en el contenedor llamado **mycontainer** y el nuevo nombre de archivo será **myUploadedVHD.vhd**.</span><span class="sxs-lookup"><span data-stu-id="3c1ae-153">The file will be placed into the container named **mycontainer** and the new file name will be **myUploadedVHD.vhd**.</span></span>

```powershell
$rgName = "myResourceGroup"
$urlOfUploadedImageVhd = "https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd"
Add-AzureRmVhd -ResourceGroupName $rgName -Destination $urlOfUploadedImageVhd `
    -LocalFilePath "C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd"
```


<span data-ttu-id="3c1ae-154">Si se realiza correctamente, obtendrá una respuesta similar a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="3c1ae-154">If successful, you get a response that looks similar to this:</span></span>

```powershell
MD5 hash is being calculated for the file C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd.
MD5 hash calculation is completed.
Elapsed time for the operation: 00:03:35
Creating new page blob of size 53687091712...
Elapsed time for upload: 01:12:49

LocalFilePath           DestinationUri
-------------           --------------
C:\Users\Public\Doc...  https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd
```

<span data-ttu-id="3c1ae-155">Dependiendo de la conexión de red y del tamaño del archivo VHD, este comando puede tardar algún tiempo en completarse.</span><span class="sxs-lookup"><span data-stu-id="3c1ae-155">Depending on your network connection and the size of your VHD file, this command may take a while to complete.</span></span>


## <a name="create-a-new-vm"></a><span data-ttu-id="3c1ae-156">Creación de una máquina virtual nueva</span><span class="sxs-lookup"><span data-stu-id="3c1ae-156">Create a new VM</span></span> 

<span data-ttu-id="3c1ae-157">Ya puede usar el VHD cargado para crear una nueva máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="3c1ae-157">You can now use the uploaded VHD to create a new VM.</span></span> 

### <a name="set-the-uri-of-the-vhd"></a><span data-ttu-id="3c1ae-158">Establecimiento del URI del VHD</span><span class="sxs-lookup"><span data-stu-id="3c1ae-158">Set the URI of the VHD</span></span>

<span data-ttu-id="3c1ae-159">El URI para el VHD que se usará está en el formato: https://**mystorageaccount**.blob.core.windows.net/**mycontainer**/**MyVhdName**.vhd.</span><span class="sxs-lookup"><span data-stu-id="3c1ae-159">The URI for the VHD to use is in the format: https://**mystorageaccount**.blob.core.windows.net/**mycontainer**/**MyVhdName**.vhd.</span></span> <span data-ttu-id="3c1ae-160">En este ejemplo, el VHD denominado "**myVHD**" es la cuenta de almacenamiento **mystorageaccount** del contenedor **mycontainer**.</span><span class="sxs-lookup"><span data-stu-id="3c1ae-160">In this example the VHD named **myVHD** is in the storage account **mystorageaccount** in the container **mycontainer**.</span></span>

```powershell
$imageURI = "https://mystorageaccount.blob.core.windows.net/mycontainer/myVhd.vhd"
```


### <a name="create-a-virtual-network"></a><span data-ttu-id="3c1ae-161">Crear una red virtual</span><span class="sxs-lookup"><span data-stu-id="3c1ae-161">Create a virtual network</span></span>
<span data-ttu-id="3c1ae-162">Cree la red virtual y la subred de la [red virtual](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3c1ae-162">Create the vNet and subnet of the [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

1. <span data-ttu-id="3c1ae-163">Cree la subred.</span><span class="sxs-lookup"><span data-stu-id="3c1ae-163">Create the subnet.</span></span> <span data-ttu-id="3c1ae-164">El ejemplo siguiente crea una subred denominada "**mySubnet**" en el grupo de recursos "**myResourceGroup**" con el prefijo de dirección **10.0.0.0/24**.</span><span class="sxs-lookup"><span data-stu-id="3c1ae-164">The following sample creates a subnet named **mySubnet** in the resource group **myResourceGroup** with the address prefix of **10.0.0.0/24**.</span></span>  
   
    ```powershell
    $rgName = "myResourceGroup"
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. <span data-ttu-id="3c1ae-165">Creación de la red virtual.</span><span class="sxs-lookup"><span data-stu-id="3c1ae-165">Create the virtual network.</span></span> <span data-ttu-id="3c1ae-166">El ejemplo siguiente crea una red virtual denominada "**myVnet**" en la ubicación **oeste de EE. UU.** con el prefijo de dirección **10.0.0.0/16**.</span><span class="sxs-lookup"><span data-stu-id="3c1ae-166">The following sample creates a virtual network named **myVnet** in the **West US** location with the address prefix of **10.0.0.0/16**.</span></span>  
   
    ```powershell
    $location = "West US"
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

### <a name="create-a-public-ip-address-and-network-interface"></a><span data-ttu-id="3c1ae-167">Creación de una dirección IP y una interfaz de red</span><span class="sxs-lookup"><span data-stu-id="3c1ae-167">Create a public IP address and network interface</span></span>
<span data-ttu-id="3c1ae-168">Para permitir la comunicación con la máquina virtual en la red virtual, necesitará una [dirección IP pública](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) y una interfaz de red.</span><span class="sxs-lookup"><span data-stu-id="3c1ae-168">To enable communication with the virtual machine in the virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

1. <span data-ttu-id="3c1ae-169">Cree una dirección IP pública.</span><span class="sxs-lookup"><span data-stu-id="3c1ae-169">Create a public IP address.</span></span> <span data-ttu-id="3c1ae-170">Este ejemplo crea una dirección IP pública denominada "**myPip**".</span><span class="sxs-lookup"><span data-stu-id="3c1ae-170">This example creates a public IP address named **myPip**.</span></span> 
   
    ```powershell
    $ipName = "myPip"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. <span data-ttu-id="3c1ae-171">Cree la NIC.</span><span class="sxs-lookup"><span data-stu-id="3c1ae-171">Create the NIC.</span></span> <span data-ttu-id="3c1ae-172">Este ejemplo crea una NIC denominada "**myNic**".</span><span class="sxs-lookup"><span data-stu-id="3c1ae-172">This example creates a NIC named **myNic**.</span></span> 
   
    ```powershell
    $nicName = "myNic"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName -Location $location `
        -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

### <a name="create-the-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="3c1ae-173">Creación del grupo de seguridad de red y las reglas de RDP</span><span class="sxs-lookup"><span data-stu-id="3c1ae-173">Create the network security group and an RDP rule</span></span>
<span data-ttu-id="3c1ae-174">Para poder iniciar sesión en la máquina virtual mediante RDP, debe tener una regla de seguridad que permita el acceso RDP en el puerto 3389.</span><span class="sxs-lookup"><span data-stu-id="3c1ae-174">To be able to log in to your VM using RDP, you need to have a security rule that allows RDP access on port 3389.</span></span> 

<span data-ttu-id="3c1ae-175">Este ejemplo crea un NSG denominado"**myNsg**" que contiene una regla llamada "**myRdpRule**" que permita el tráfico RDP en el puerto 3389.</span><span class="sxs-lookup"><span data-stu-id="3c1ae-175">This example creates an NSG named **myNsg** that contains a rule called **myRdpRule** that allows RDP traffic over port 3389.</span></span> <span data-ttu-id="3c1ae-176">Para obtener más información sobre NSG, consulte [Apertura de puertos para una máquina virtual en Azure mediante PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3c1ae-176">For more information about NSGs, see [Opening ports to a VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

```powershell
$nsgName = "myNsg"

$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389

$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
```


### <a name="create-a-variable-for-the-virtual-network"></a><span data-ttu-id="3c1ae-177">Creación de una variable para la red virtual</span><span class="sxs-lookup"><span data-stu-id="3c1ae-177">Create a variable for the virtual network</span></span>
<span data-ttu-id="3c1ae-178">Cree una variable para la red virtual completada.</span><span class="sxs-lookup"><span data-stu-id="3c1ae-178">Create a variable for the completed virtual network.</span></span> 

```powershell
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName
```

### <a name="create-the-vm"></a><span data-ttu-id="3c1ae-179">Creación de la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="3c1ae-179">Create the VM</span></span>
<span data-ttu-id="3c1ae-180">En el siguiente script de PowerShell se muestra cómo establecer las configuraciones de máquina virtual y usar la imagen de máquina virtual cargada como origen para la nueva instalación.</span><span class="sxs-lookup"><span data-stu-id="3c1ae-180">The following PowerShell script shows how to set up the virtual machine configurations and use the uploaded VM image as the source for the new installation.</span></span>



```powershell
# Enter a new user name and password to use as the local administrator account 
    # for remotely accessing the VM.
    $cred = Get-Credential

    # Name of the storage account where the VHD is located. This example sets the 
    # storage account name as "myStorageAccount"
    $storageAccName = "myStorageAccount"

    # Name of the virtual machine. This example sets the VM name as "myVM".
    $vmName = "myVM"

    # Size of the virtual machine. This example creates "Standard_D2_v2" sized VM. 
    # See the VM sizes documentation for more information: 
    # https://azure.microsoft.com/documentation/articles/virtual-machines-windows-sizes/
    $vmSize = "Standard_D2_v2"

    # Computer name for the VM. This examples sets the computer name as "myComputer".
    $computerName = "myComputer"

    # Name of the disk that holds the OS. This example sets the 
    # OS disk name as "myOsDisk"
    $osDiskName = "myOsDisk"

    # Assign a SKU name. This example sets the SKU name as "Standard_LRS"
    # Valid values for -SkuName are: Standard_LRS - locally redundant storage, Standard_ZRS - zone redundant
    # storage, Standard_GRS - geo redundant storage, Standard_RAGRS - read access geo redundant storage,
    # Premium_LRS - premium locally redundant storage. 
    $skuName = "Standard_LRS"

    # Get the storage account where the uploaded image is stored
    $storageAcc = Get-AzureRmStorageAccount -ResourceGroupName $rgName -AccountName $storageAccName

    # Set the VM name and size
    $vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize

    #Set the Windows operating system configuration and add the NIC
    $vm = Set-AzureRmVMOperatingSystem -VM $vmConfig -Windows -ComputerName $computerName `
        -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id

    # Create the OS disk URI
    $osDiskUri = '{0}vhds/{1}-{2}.vhd' `
        -f $storageAcc.PrimaryEndpoints.Blob.ToString(), $vmName.ToLower(), $osDiskName

    # Configure the OS disk to be created from the existing VHD image (-CreateOption fromImage).
    $vm = Set-AzureRmVMOSDisk -VM $vm -Name $osDiskName -VhdUri $osDiskUri `
        -CreateOption fromImage -SourceImageUri $imageURI -Windows

    # Create the new VM
    New-AzureRmVM -ResourceGroupName $rgName -Location $location -VM $vm
```

## <a name="verify-that-the-vm-was-created"></a><span data-ttu-id="3c1ae-181">Comprobación de que se creó la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="3c1ae-181">Verify that the VM was created</span></span>
<span data-ttu-id="3c1ae-182">Cuando finalice, debería ver la máquina virtual recién creada en el [Azure Portal](https://portal.azure.com), en **Examinar** > **Máquinas virtuales** o mediante los comandos de PowerShell siguientes:</span><span class="sxs-lookup"><span data-stu-id="3c1ae-182">When complete, you should see the newly created VM in the [Azure portal](https://portal.azure.com) under **Browse** > **Virtual machines**, or by using the following PowerShell commands:</span></span>

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="3c1ae-183">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3c1ae-183">Next steps</span></span>
<span data-ttu-id="3c1ae-184">Para administrar la nueva máquina virtual de Azure PowerShell, consulte [Administración de máquinas virtuales de Azure con Resource Manager y PowerShell](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3c1ae-184">To manage your new virtual machine with Azure PowerShell, see [Manage virtual machines using Azure Resource Manager and PowerShell](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


