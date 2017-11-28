---
title: "Creación de una máquina virtual a partir de un disco especializado en Azure | Microsoft Docs"
description: "Cree una máquina virtual mediante la asociación de un disco no administrado especializado en el modelo de implementación del administrador de recursos."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3b7d3cd5-e3d7-4041-a2a7-0290447458ea
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: cynthn
ms.openlocfilehash: 974d89aa96cba94fedfd1acbaf4f1d30ac8e6257
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-vm-from-a-specialized-vhd-in-a-storage-account"></a><span data-ttu-id="cef1b-103">Crear una máquina virtual a partir de un VHD especializado en una cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="cef1b-103">Create a VM from a specialized VHD in a storage account</span></span>

<span data-ttu-id="cef1b-104">Cree una máquina virtual mediante la asociación de un disco no administrado especializado como disco del sistema operativo mediante PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cef1b-104">Create a new VM by attaching a specialized unmanaged disk as the OS disk using Powershell.</span></span> <span data-ttu-id="cef1b-105">Un disco especializado es una copia del VHD de una máquina virtual existente que mantiene las cuentas de usuario, las aplicaciones y otros datos de estado de la máquina virtual original.</span><span class="sxs-lookup"><span data-stu-id="cef1b-105">A specialized disk is a copy of VHD from an existing VM that maintains the user accounts, applications and other state data from your original VM.</span></span> 

<span data-ttu-id="cef1b-106">Tiene dos opciones:</span><span class="sxs-lookup"><span data-stu-id="cef1b-106">You have two options:</span></span>
* [<span data-ttu-id="cef1b-107">Carga de un disco duro virtual</span><span class="sxs-lookup"><span data-stu-id="cef1b-107">Upload a VHD</span></span>](create-vm-specialized.md#option-1-upload-a-specialized-vhd)
* [<span data-ttu-id="cef1b-108">Copiar el VHD de una máquina virtual de Azure existente</span><span class="sxs-lookup"><span data-stu-id="cef1b-108">Copy the VHD of an existing Azure VM</span></span>](create-vm-specialized.md#option-2-copy-an-existing-azure-vm)

## <a name="before-you-begin"></a><span data-ttu-id="cef1b-109">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="cef1b-109">Before you begin</span></span>
<span data-ttu-id="cef1b-110">Si usa PowerShell, asegúrese de que tiene la versión más reciente del módulo de PowerShell AzureRM.Compute.</span><span class="sxs-lookup"><span data-stu-id="cef1b-110">If you use PowerShell, make sure that you have the latest version of the AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="cef1b-111">Ejecute el siguiente comando para instalarla.</span><span class="sxs-lookup"><span data-stu-id="cef1b-111">Run the following command to install it.</span></span>

```powershell
Install-Module AzureRM.Compute 
```
<span data-ttu-id="cef1b-112">Para más información, consulte [Azure PowerShell Versioning](/powershell/azure/overview) (Control de versiones de Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="cef1b-112">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


## <a name="option-1-upload-a-specialized-vhd"></a><span data-ttu-id="cef1b-113">Opción 1: Cargar un VHD especializado</span><span class="sxs-lookup"><span data-stu-id="cef1b-113">Option 1: Upload a specialized VHD</span></span>

<span data-ttu-id="cef1b-114">Puede cargar el VHD de una máquina virtual especializada creada con una herramienta de virtualización local, como Hyper-V, o de una máquina virtual exportada desde otra nube.</span><span class="sxs-lookup"><span data-stu-id="cef1b-114">You can upload the VHD from a specialized VM created with an on-premises virtualization tool, like Hyper-V, or a VM exported from another cloud.</span></span>

### <a name="prepare-the-vm"></a><span data-ttu-id="cef1b-115">Preparación de la VM</span><span class="sxs-lookup"><span data-stu-id="cef1b-115">Prepare the VM</span></span>
<span data-ttu-id="cef1b-116">Puede cargar un VHD especializado que se haya creado con una máquina virtual local o un VHD exportado desde otra nube.</span><span class="sxs-lookup"><span data-stu-id="cef1b-116">You can upload a specialized VHD that was created using an on-premises VM or a VHD exported from another cloud.</span></span> <span data-ttu-id="cef1b-117">Un disco duro virtual especializado mantiene las cuentas de usuario, las aplicaciones y otros datos de estado de la máquina virtual original.</span><span class="sxs-lookup"><span data-stu-id="cef1b-117">A specialized VHD maintains the user accounts, applications and other state data from your original VM.</span></span> <span data-ttu-id="cef1b-118">Si tiene previsto usar el VHD como está para crear una nueva VM, asegúrese de completar los pasos siguientes.</span><span class="sxs-lookup"><span data-stu-id="cef1b-118">If you intend to use the VHD as-is to create a new VM, ensure the following steps are completed.</span></span> 
  
  * <span data-ttu-id="cef1b-119">[Preparar de un VHD de Windows para cargar en Azure](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="cef1b-119">[Prepare a Windows VHD to upload to Azure](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="cef1b-120">**No** generalice la VM mediante Sysprep.</span><span class="sxs-lookup"><span data-stu-id="cef1b-120">**Do not** generalize the VM using Sysprep.</span></span>
  * <span data-ttu-id="cef1b-121">Quite todas las herramientas de virtualización de invitado y los agentes instalados en la VM (es decir, herramientas de VMware).</span><span class="sxs-lookup"><span data-stu-id="cef1b-121">Remove any guest virtualization tools and agents that are installed on the VM (i.e. VMware tools).</span></span>
  * <span data-ttu-id="cef1b-122">Asegúrese de que la VM se configura para extraer su dirección IP y la configuración de DNS a través de DHCP.</span><span class="sxs-lookup"><span data-stu-id="cef1b-122">Ensure the VM is configured to pull its IP address and DNS settings via DHCP.</span></span> <span data-ttu-id="cef1b-123">Esto garantiza que el servidor obtiene una dirección IP dentro de la red virtual cuando se inicia.</span><span class="sxs-lookup"><span data-stu-id="cef1b-123">This ensures that the server obtains an IP address within the VNet when it starts up.</span></span> 


### <a name="get-the-storage-account"></a><span data-ttu-id="cef1b-124">Obtención de la cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="cef1b-124">Get the storage account</span></span>
<span data-ttu-id="cef1b-125">Necesita una cuenta de almacenamiento de Azure para almacenar la imagen de VM cargada.</span><span class="sxs-lookup"><span data-stu-id="cef1b-125">You need a storage account in Azure to store the uploaded VM image.</span></span> <span data-ttu-id="cef1b-126">Puede usar una cuenta de almacenamiento existente o crear una nueva.</span><span class="sxs-lookup"><span data-stu-id="cef1b-126">You can either use an existing storage account or create a new one.</span></span> 

<span data-ttu-id="cef1b-127">Para mostrar las cuentas de almacenamiento disponibles, escriba:</span><span class="sxs-lookup"><span data-stu-id="cef1b-127">To show the available storage accounts, type:</span></span>

```powershell
Get-AzureRmStorageAccount
```

<span data-ttu-id="cef1b-128">Si desea utilizar una cuenta de almacenamiento existente, puede continuar con la sección [Carga de la imagen de VM en la cuenta de almacenamiento](#upload-the-vm-vhd-to-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="cef1b-128">If you want to use an existing storage account, proceed to the [Upload the VM image](#upload-the-vm-vhd-to-your-storage-account) section.</span></span>

<span data-ttu-id="cef1b-129">Si necesita crear una nueva cuenta de almacenamiento, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="cef1b-129">If you need to create a storage account, follow these steps:</span></span>

1. <span data-ttu-id="cef1b-130">Necesita el nombre del grupo de recursos donde se debe crear la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="cef1b-130">You need the name of the resource group where the storage account should be created.</span></span> <span data-ttu-id="cef1b-131">Para averiguar todos los grupos de recursos que están en la suscripción, escriba:</span><span class="sxs-lookup"><span data-stu-id="cef1b-131">To find out all the resource groups that are in your subscription, type:</span></span>
   
    ```powershell
    Get-AzureRmResourceGroup
    ```

    <span data-ttu-id="cef1b-132">Para crear un grupo de recursos denominado **myResourceGroup** en la región **Oeste de EE. UU.**, escriba:</span><span class="sxs-lookup"><span data-stu-id="cef1b-132">To create a resource group named **myResourceGroup** in the **West US** region, type:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "West US"
    ```

2. <span data-ttu-id="cef1b-133">Cree una cuenta de almacenamiento denominada **mystorageaccount** en este grupo de recursos con el cmdlet [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount):</span><span class="sxs-lookup"><span data-stu-id="cef1b-133">Create a storage account named **mystorageaccount** in this resource group by using the [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:</span></span>
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "West US" `
        -SkuName "Standard_LRS" -Kind "Storage"
    ```
   
### <a name="upload-the-vhd-to-your-storage-account"></a><span data-ttu-id="cef1b-134">Carga del VHD en la cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="cef1b-134">Upload the VHD to your storage account</span></span>
<span data-ttu-id="cef1b-135">Utilice el cmdlet [Add-AzureRmVhd](/powershell/module/azurerm.compute/add-azurermvhd) para cargar la imagen en un contenedor de su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="cef1b-135">Use the [Add-AzureRmVhd](/powershell/module/azurerm.compute/add-azurermvhd) cmdlet to upload the image to a container in your storage account.</span></span> <span data-ttu-id="cef1b-136">En este ejemplo se carga el archivo **myVHD.vhd** de `"C:\Users\Public\Documents\Virtual hard disks\"` para una cuenta de almacenamiento denominada **mystorageaccount** en el grupo de recursos **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="cef1b-136">This example uploads the file **myVHD.vhd** from `"C:\Users\Public\Documents\Virtual hard disks\"` to a storage account named **mystorageaccount** in the **myResourceGroup** resource group.</span></span> <span data-ttu-id="cef1b-137">El archivo se colocará en el contenedor llamado **mycontainer** y el nuevo nombre de archivo será **myUploadedVHD.vhd**.</span><span class="sxs-lookup"><span data-stu-id="cef1b-137">The file will be placed into the container named **mycontainer** and the new file name will be **myUploadedVHD.vhd**.</span></span>

```powershell
$rgName = "myResourceGroup"
$urlOfUploadedImageVhd = "https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd"
Add-AzureRmVhd -ResourceGroupName $rgName -Destination $urlOfUploadedImageVhd `
    -LocalFilePath "C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd"
```


<span data-ttu-id="cef1b-138">Si se realiza correctamente, obtendrá una respuesta similar a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="cef1b-138">If successful, you get a response that looks similar to this:</span></span>

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

<span data-ttu-id="cef1b-139">En función de la conexión de red y del tamaño del archivo VHD, este comando tardará algún tiempo en completarse.</span><span class="sxs-lookup"><span data-stu-id="cef1b-139">Depending on your network connection and the size of your VHD file, this command may take a while to complete.</span></span>


## <a name="option-2-copy-the-vhd-from-an-existing-azure-vm"></a><span data-ttu-id="cef1b-140">Opción 2: copiar el VHD de una máquina virtual de Azure existente</span><span class="sxs-lookup"><span data-stu-id="cef1b-140">Option 2: Copy the VHD from an existing Azure VM</span></span>

<span data-ttu-id="cef1b-141">Puede copiar un VHD a otra cuenta de almacenamiento para que se use al crear una máquina virtual duplicada.</span><span class="sxs-lookup"><span data-stu-id="cef1b-141">You can copy a VHD to another storage account to use when creating a new, duplicate VM.</span></span>

### <a name="before-you-begin"></a><span data-ttu-id="cef1b-142">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="cef1b-142">Before you begin</span></span>
<span data-ttu-id="cef1b-143">Asegúrese de todo esto:</span><span class="sxs-lookup"><span data-stu-id="cef1b-143">Make sure that you:</span></span>

* <span data-ttu-id="cef1b-144">Tener información sobre las **cuentas de almacenamiento de origen y de destino**.</span><span class="sxs-lookup"><span data-stu-id="cef1b-144">Have information about the **source and destination storage accounts**.</span></span> <span data-ttu-id="cef1b-145">Para la máquina virtual de origen, necesitará los nombres del contenedor y la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="cef1b-145">For the source VM, you need to have the storage account and container names.</span></span> <span data-ttu-id="cef1b-146">Normalmente, el nombre del contenedor será **vhds**.</span><span class="sxs-lookup"><span data-stu-id="cef1b-146">Usually, the container name will be **vhds**.</span></span> <span data-ttu-id="cef1b-147">También debe tener una cuenta de almacenamiento de destino.</span><span class="sxs-lookup"><span data-stu-id="cef1b-147">You also need to have a destination storage account.</span></span> <span data-ttu-id="cef1b-148">Si todavía no tiene una, puede crearla con el portal (**Más servicios** > Cuentas de almacenamiento > Agregar) o el cmdlet [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount).</span><span class="sxs-lookup"><span data-stu-id="cef1b-148">If you don't already have one, you can create one using either the portal (**More Services** > Storage accounts > Add) or using the [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet.</span></span> 
* <span data-ttu-id="cef1b-149">Tener descargada e instalada la [herramienta AzCopy](../../storage/common/storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="cef1b-149">Have downloaded and installed the [AzCopy tool](../../storage/common/storage-use-azcopy.md).</span></span> 

### <a name="deallocate-the-vm"></a><span data-ttu-id="cef1b-150">Desasignación de la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="cef1b-150">Deallocate the VM</span></span>
<span data-ttu-id="cef1b-151">Desasigne la máquina virtual para liberar espacio en el VHD que se va a copiar.</span><span class="sxs-lookup"><span data-stu-id="cef1b-151">Deallocate the VM, which frees up the VHD to be copied.</span></span> 

* <span data-ttu-id="cef1b-152">**Portal**: haga clic en **Máquinas virtuales** > **myVM** > Detener</span><span class="sxs-lookup"><span data-stu-id="cef1b-152">**Portal**: Click **Virtual machines** > **myVM** > Stop</span></span>
* <span data-ttu-id="cef1b-153">**PowerShell**: use [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) para detener (desasignar) la máquina virtual denominada **myVM** del grupo de recursos **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="cef1b-153">**Powershell**: Use [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) to stop (deallocate) the VM named **myVM** in resource group **myResourceGroup**.</span></span>

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroup -Name myVM
```

<span data-ttu-id="cef1b-154">El **estado** de la máquina virtual en Azure Portal cambia de **Detenido** a **Detenido (desasignado)**.</span><span class="sxs-lookup"><span data-stu-id="cef1b-154">The **Status** for the VM in the Azure portal changes from **Stopped** to **Stopped (deallocated)**.</span></span>

### <a name="get-the-storage-account-urls"></a><span data-ttu-id="cef1b-155">Obtención de las URL de las cuentas de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="cef1b-155">Get the storage account URLs</span></span>
<span data-ttu-id="cef1b-156">Necesita las URL de las cuentas de almacenamiento de origen y de destino.</span><span class="sxs-lookup"><span data-stu-id="cef1b-156">You need the URLs of the source and destination storage accounts.</span></span> <span data-ttu-id="cef1b-157">Las direcciones URL se verán así: `https://<storageaccount>.blob.core.windows.net/<containerName>/`.</span><span class="sxs-lookup"><span data-stu-id="cef1b-157">The URLs look like: `https://<storageaccount>.blob.core.windows.net/<containerName>/`.</span></span> <span data-ttu-id="cef1b-158">Si ya conoce el nombre de la cuenta de almacenamiento y el contenedor, puede reemplazar simplemente la información entre corchetes para crear la dirección URL.</span><span class="sxs-lookup"><span data-stu-id="cef1b-158">If you already know the storage account and container name, you can just replace the information between the brackets to create your URL.</span></span> 

<span data-ttu-id="cef1b-159">Puede usar Azure Portal o Azure PowerShell para obtener la URL:</span><span class="sxs-lookup"><span data-stu-id="cef1b-159">You can use the Azure portal or Azure Powershell to get the URL:</span></span>

* <span data-ttu-id="cef1b-160">**Portal**: haga clic en **>** para ir a **Más servicios** > **Cuentas de almacenamiento** > *cuenta de almacenamiento* > **Blobs**. El archivo VHD de origen estará probablemente en el contenedor **vhds**.</span><span class="sxs-lookup"><span data-stu-id="cef1b-160">**Portal**: Click the **>** for **More services** > **Storage accounts** > *storage account* > **Blobs** and your source VHD file is probably in the **vhds** container.</span></span> <span data-ttu-id="cef1b-161">Haga clic en la opción **Propiedades** del contenedor y copie el texto etiquetado como **Dirección URL**.</span><span class="sxs-lookup"><span data-stu-id="cef1b-161">Click **Properties** for the container, and copy the text labeled **URL**.</span></span> <span data-ttu-id="cef1b-162">Necesitará las direcciones URL de los contenedores de origen y de destino.</span><span class="sxs-lookup"><span data-stu-id="cef1b-162">You'll need the URLs of both the source and destination containers.</span></span> 
* <span data-ttu-id="cef1b-163">**PowerShell**: use [Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) para obtener la información de la máquina virtual denominada **myVM** del grupo de recursos **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="cef1b-163">**Powershell**: Use [Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) to get the information for VM named **myVM** in the resource group **myResourceGroup**.</span></span> <span data-ttu-id="cef1b-164">En los resultados, busque la sección **Perfil de almacenamiento** del **URI del VHD**.</span><span class="sxs-lookup"><span data-stu-id="cef1b-164">In the results, look in the **Storage profile** section for the **Vhd Uri**.</span></span> <span data-ttu-id="cef1b-165">La primera parte del URI es la dirección URL al contenedor, y la última, el nombre del VHD del sistema operativo de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="cef1b-165">The first part of the Uri is the URL to the container and the last part is the OS VHD name for the VM.</span></span>

```powershell
Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
``` 

## <a name="get-the-storage-access-keys"></a><span data-ttu-id="cef1b-166">Obtención de las claves de acceso de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="cef1b-166">Get the storage access keys</span></span>
<span data-ttu-id="cef1b-167">Busque las claves de acceso de las cuentas de almacenamiento de origen y de destino.</span><span class="sxs-lookup"><span data-stu-id="cef1b-167">Find the access keys for the source and destination storage accounts.</span></span> <span data-ttu-id="cef1b-168">Para más información acerca de las claves de acceso, consulte [Acerca de las cuentas de almacenamiento de Azure](../../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="cef1b-168">For more information about access keys, see [About Azure storage accounts](../../storage/common/storage-create-storage-account.md).</span></span>

* <span data-ttu-id="cef1b-169">**Portal**: haga clic en **Más servicios** > **Cuentas de almacenamiento** > *cuenta de almacenamiento* > **Claves de acceso**.</span><span class="sxs-lookup"><span data-stu-id="cef1b-169">**Portal**: Click **More services** > **Storage accounts** > *storage account* > **Access keys**.</span></span> <span data-ttu-id="cef1b-170">Copie la clave etiquetada como **clave1**.</span><span class="sxs-lookup"><span data-stu-id="cef1b-170">Copy the key labeled as **key1**.</span></span>
* <span data-ttu-id="cef1b-171">**PowerShell**: use [Get-AzureRmStorageAccountKey](/powershell/module/azurerm.storage/get-azurermstorageaccountkey) para obtener la clave de almacenamiento de la cuenta de almacenamiento **mystorageaccount** del grupo de recursos **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="cef1b-171">**Powershell**: Use [Get-AzureRmStorageAccountKey](/powershell/module/azurerm.storage/get-azurermstorageaccountkey) to get the storage key for the storage account **mystorageaccount** in the resource group **myResourceGroup**.</span></span> <span data-ttu-id="cef1b-172">Copie la clave etiquetada como **clave1**.</span><span class="sxs-lookup"><span data-stu-id="cef1b-172">Copy the key labeled **key1**.</span></span>

```powershell
Get-AzureRmStorageAccountKey -Name mystorageaccount -ResourceGroupName myResourceGroup
```

### <a name="copy-the-vhd"></a><span data-ttu-id="cef1b-173">Copia del VHD</span><span class="sxs-lookup"><span data-stu-id="cef1b-173">Copy the VHD</span></span>
<span data-ttu-id="cef1b-174">Puede copiar archivos entre cuentas de almacenamiento con AzCopy.</span><span class="sxs-lookup"><span data-stu-id="cef1b-174">You can copy files between storage accounts using AzCopy.</span></span> <span data-ttu-id="cef1b-175">Para el contenedor de destino, si el contenedor especificado no existe, se creará automáticamente.</span><span class="sxs-lookup"><span data-stu-id="cef1b-175">For the destination container, if the specified container doesn't exist, it will be created for you.</span></span> 

<span data-ttu-id="cef1b-176">Para usar AzCopy, abra una ventana de comandos en el equipo local y navegue hasta la carpeta donde está instalada dicha herramienta.</span><span class="sxs-lookup"><span data-stu-id="cef1b-176">To use AzCopy, open a command prompt on your local machine and navigate to the folder where AzCopy is installed.</span></span> <span data-ttu-id="cef1b-177">Será similar a *C:\Archivos de programa (x86)\Microsoft SDKs\Azure\AzCopy*.</span><span class="sxs-lookup"><span data-stu-id="cef1b-177">It will be similar to *C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy*.</span></span> 

<span data-ttu-id="cef1b-178">Para copiar todos los archivos dentro de un contenedor, use el modificador **/S**.</span><span class="sxs-lookup"><span data-stu-id="cef1b-178">To copy all of the files within a container, you use the **/S** switch.</span></span> <span data-ttu-id="cef1b-179">Esto puede utilizarse para copiar el VHD del sistema operativo y todos los discos de datos si están en el mismo contenedor.</span><span class="sxs-lookup"><span data-stu-id="cef1b-179">This can be used to copy the OS VHD and all of the data disks if they are in the same container.</span></span> <span data-ttu-id="cef1b-180">En este ejemplo se muestra cómo copiar todos los archivos del contenedor **mysourcecontainer** de la cuenta de almacenamiento **mysourcestorageaccount** en el contenedor **mydestinationcontainer** de la cuenta de almacenamiento **mydestinationstorageaccount**.</span><span class="sxs-lookup"><span data-stu-id="cef1b-180">This example shows how to copy all of the files in the container **mysourcecontainer** in storage account **mysourcestorageaccount** to the container **mydestinationcontainer** in the **mydestinationstorageaccount** storage account.</span></span> <span data-ttu-id="cef1b-181">Reemplace los nombres de las cuentas de almacenamiento y los contenedores por los suyos.</span><span class="sxs-lookup"><span data-stu-id="cef1b-181">Replace the names of the storage accounts and containers with your own.</span></span> <span data-ttu-id="cef1b-182">Reemplace `<sourceStorageAccountKey1>` y `<destinationStorageAccountKey1>` por sus propias claves.</span><span class="sxs-lookup"><span data-stu-id="cef1b-182">Replace `<sourceStorageAccountKey1>` and `<destinationStorageAccountKey1>` with your own keys.</span></span>

```
AzCopy /Source:https://mysourcestorageaccount.blob.core.windows.net/mysourcecontainer `
    /Dest:https://mydestinationatorageaccount.blob.core.windows.net/mydestinationcontainer `
    /SourceKey:<sourceStorageAccountKey1> /DestKey:<destinationStorageAccountKey1> /S
```

<span data-ttu-id="cef1b-183">Si solo quiere copiar un VHD específico en un contenedor con varios archivos, también puede especificar el nombre de archivo con el modificador /Pattern.</span><span class="sxs-lookup"><span data-stu-id="cef1b-183">If you only want to copy a specific VHD in a container with multiple files, you can also specify the file name using the /Pattern switch.</span></span> <span data-ttu-id="cef1b-184">En este ejemplo, solo se copiará el archivo denominado "**myFileName.vhd**".</span><span class="sxs-lookup"><span data-stu-id="cef1b-184">In this example, only the file named **myFileName.vhd** will be copied.</span></span>

```
AzCopy /Source:https://mysourcestorageaccount.blob.core.windows.net/mysourcecontainer `
  /Dest:https://mydestinationatorageaccount.blob.core.windows.net/mydestinationcontainer `
  /SourceKey:<sourceStorageAccountKey1> /DestKey:<destinationStorageAccountKey1> `
  /Pattern:myFileName.vhd
```


<span data-ttu-id="cef1b-185">Cuando haya finalizado, obtendrá un mensaje parecido a este:</span><span class="sxs-lookup"><span data-stu-id="cef1b-185">When it is finished, you will get a message that looks something like:</span></span>

```
Finished 2 of total 2 file(s).
[2016/10/07 17:37:41] Transfer summary:
-----------------
Total files transferred: 2
Transfer successfully:   2
Transfer skipped:        0
Transfer failed:         0
Elapsed time:            00.00:13:07
```

### <a name="troubleshooting"></a><span data-ttu-id="cef1b-186">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="cef1b-186">Troubleshooting</span></span>
* <span data-ttu-id="cef1b-187">Cuando use AZCopy, si ve el error El servidor no pudo autenticar la solicitud, asegúrese de que el valor del encabezado de autenticación tenga el formato correcto, incluida la firma,</span><span class="sxs-lookup"><span data-stu-id="cef1b-187">When you use AZCopy, if you see the error "Server failed to authenticate the request", make sure the value of the Authorization header is formed correctly including the signature.</span></span> <span data-ttu-id="cef1b-188">y, si usa la clave 2 o la clave de almacenamiento secundaria, pruebe a utilizar la clave de almacenamiento principal o 1.</span><span class="sxs-lookup"><span data-stu-id="cef1b-188">If you are using Key 2 or the secondary storage key, try using the primary or 1st storage key.</span></span>

## <a name="create-the-new-vm"></a><span data-ttu-id="cef1b-189">Creación de la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="cef1b-189">Create the new VM</span></span> 

<span data-ttu-id="cef1b-190">Debe crear recursos de red y otros recursos de máquina virtual para que los use la nueva máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="cef1b-190">You need to create networking and other VM resources to be used by the new VM.</span></span>

### <a name="create-the-subnet-and-vnet"></a><span data-ttu-id="cef1b-191">Creación de la subred y la red virtual</span><span class="sxs-lookup"><span data-stu-id="cef1b-191">Create the subNet and vNet</span></span>

<span data-ttu-id="cef1b-192">Cree la red virtual y la subred de la [red virtual](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="cef1b-192">Create the vNet and subNet of the [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

1. <span data-ttu-id="cef1b-193">Cree la subred.</span><span class="sxs-lookup"><span data-stu-id="cef1b-193">Create the subNet.</span></span> <span data-ttu-id="cef1b-194">En este ejemplo se crea una subred llamada **mySubNet**, en el grupo de recursos **myResourceGroup** y se establece el prefijo de la dirección de subred en **10.0.0.0/24**.</span><span class="sxs-lookup"><span data-stu-id="cef1b-194">This example creates a subnet named **mySubNet**, in the resource group **myResourceGroup**, and sets the subnet address prefix to **10.0.0.0/24**.</span></span>
   
    ```powershell
    $rgName = "myResourceGroup"
    $subnetName = "mySubNet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. <span data-ttu-id="cef1b-195">Cree la red virtual.</span><span class="sxs-lookup"><span data-stu-id="cef1b-195">Create the vNet.</span></span> <span data-ttu-id="cef1b-196">En este ejemplo se establece el nombre de la red virtual en **myVnetName**, la ubicación en **Oeste de EE. UU.** y el prefijo de dirección de la red virtual en **10.0.0.0/16**.</span><span class="sxs-lookup"><span data-stu-id="cef1b-196">This example sets the virtual network name to be **myVnetName**, the location to **West US**, and the address prefix for the virtual network to **10.0.0.0/16**.</span></span> 
   
    ```powershell
    $location = "West US"
    $vnetName = "myVnetName"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

### <a name="create-a-public-ip-address-and-nic"></a><span data-ttu-id="cef1b-197">Creación de una dirección IP pública y una NIC</span><span class="sxs-lookup"><span data-stu-id="cef1b-197">Create a public IP address and NIC</span></span>
<span data-ttu-id="cef1b-198">Para permitir la comunicación con la máquina virtual en la red virtual, necesitará una [dirección IP pública](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) y una interfaz de red.</span><span class="sxs-lookup"><span data-stu-id="cef1b-198">To enable communication with the virtual machine in the virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

1. <span data-ttu-id="cef1b-199">Cree la dirección IP pública.</span><span class="sxs-lookup"><span data-stu-id="cef1b-199">Create the public IP.</span></span> <span data-ttu-id="cef1b-200">En este ejemplo, el nombre de la dirección IP pública se establece en **myIP**.</span><span class="sxs-lookup"><span data-stu-id="cef1b-200">In this example, the public IP address name is set to **myIP**.</span></span>
   
    ```powershell
    $ipName = "myIP"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. <span data-ttu-id="cef1b-201">Cree la NIC.</span><span class="sxs-lookup"><span data-stu-id="cef1b-201">Create the NIC.</span></span> <span data-ttu-id="cef1b-202">En este ejemplo, el nombre de la NIC se establece en **myNicName**.</span><span class="sxs-lookup"><span data-stu-id="cef1b-202">In this example, the NIC name is set to **myNicName**.</span></span>
   
    ```powershell
    $nicName = "myNicName"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName `
    -Location $location -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

### <a name="create-the-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="cef1b-203">Creación del grupo de seguridad de red y las reglas de RDP</span><span class="sxs-lookup"><span data-stu-id="cef1b-203">Create the network security group and an RDP rule</span></span>
<span data-ttu-id="cef1b-204">Para poder iniciar sesión en la máquina virtual mediante RDP, debe tener una regla de seguridad que permita el acceso RDP en el puerto 3389.</span><span class="sxs-lookup"><span data-stu-id="cef1b-204">To be able to log in to your VM using RDP, you need to have an security rule that allows RDP access on port 3389.</span></span> <span data-ttu-id="cef1b-205">Como el disco duro virtual de la nueva máquina virtual se creó a partir de una máquina virtual especializada existente, después de crear la máquina virtual puede usar una cuenta existente de la máquina virtual de origen que tenga permiso para iniciar sesión mediante RDP.</span><span class="sxs-lookup"><span data-stu-id="cef1b-205">Because the VHD for the new VM was created from an existing specialized VM, after the VM is created you can use an existing account from the source virtual machine that had permission to log on using RDP.</span></span>
<span data-ttu-id="cef1b-206">En este ejemplo se establece el nombre de NSG en **myNsg** y el nombre de la regla de RDP en **myRdpRule**.</span><span class="sxs-lookup"><span data-stu-id="cef1b-206">This example sets the NSG name to **myNsg** and the RDP rule name to **myRdpRule**.</span></span>

```powershell
$nsgName = "myNsg"

$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
    
```

<span data-ttu-id="cef1b-207">Para más información sobre puntos de conexión y reglas NSG, consulte [Apertura de puertos para una máquina virtual en Azure mediante PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="cef1b-207">For more information about endpoints and NSG rules, see [Opening ports to a VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

### <a name="set-the-vm-name-and-size"></a><span data-ttu-id="cef1b-208">Establecimiento del nombre de VM y el tamaño</span><span class="sxs-lookup"><span data-stu-id="cef1b-208">Set the VM name and size</span></span>

<span data-ttu-id="cef1b-209">Este ejemplo establece el nombre de VM en "myVM" y el tamaño de VM en "Standard_A2".</span><span class="sxs-lookup"><span data-stu-id="cef1b-209">This example sets the VM name to "myVM" and the VM size to "Standard_A2".</span></span>
```powershell
$vmName = "myVM"
$vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize "Standard_A2"
```

### <a name="add-the-nic"></a><span data-ttu-id="cef1b-210">Incorporación de la NIC</span><span class="sxs-lookup"><span data-stu-id="cef1b-210">Add the NIC</span></span>
    
```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic.Id
```
    
    
### <a name="configure-the-os-disk"></a><span data-ttu-id="cef1b-211">Configuración del disco del SO</span><span class="sxs-lookup"><span data-stu-id="cef1b-211">Configure the OS disk</span></span>

1. <span data-ttu-id="cef1b-212">Establezca el URI para el VHD que ha cargado o copiado.</span><span class="sxs-lookup"><span data-stu-id="cef1b-212">Set the URI for the VHD that you uploaded or copied.</span></span> <span data-ttu-id="cef1b-213">En este ejemplo, el archivo de VHD denominado **myOsDisk.vhd** se mantiene en una cuenta de almacenamiento llamada **myStorageAccount** en un contenedor denominado **myContainer**.</span><span class="sxs-lookup"><span data-stu-id="cef1b-213">In this example, the VHD file named **myOsDisk.vhd** is kept in a storage account named **myStorageAccount** in a container named **myContainer**.</span></span>

    ```powershell
    $osDiskUri = "https://myStorageAccount.blob.core.windows.net/myContainer/myOsDisk.vhd"
    ```
2. <span data-ttu-id="cef1b-214">Agregue el disco del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="cef1b-214">Add the OS disk.</span></span> <span data-ttu-id="cef1b-215">En este ejemplo, cuando se crea el disco del SO, el término "osDisk" se agrega al nombre de VM para crear el nombre del disco de SO.</span><span class="sxs-lookup"><span data-stu-id="cef1b-215">In this example, when the OS disk is created, the term "osDisk" is appened to the VM name to create the OS disk name.</span></span> <span data-ttu-id="cef1b-216">En este ejemplo también se especifica que este VHD basado en Windows debería asociarse a la VM como el disco del SO.</span><span class="sxs-lookup"><span data-stu-id="cef1b-216">This example also specifies that this Windows-based VHD should be attached to the VM as the OS disk.</span></span>
    
    ```powershell
    $osDiskName = $vmName + "osDisk"
    $vm = Set-AzureRmVMOSDisk -VM $vm -Name $osDiskName -VhdUri $osDiskUri -CreateOption attach -Windows
    ```

<span data-ttu-id="cef1b-217">Opcional: si tiene discos de datos que necesitan estar conectados a la VM, agregue los discos de datos mediante el uso de las direcciones URL de VHD de datos y el número de unidad lógica (LUN) correspondiente.</span><span class="sxs-lookup"><span data-stu-id="cef1b-217">Optional: If you have data disks that need to be attached to the VM, add the data disks by using the URLs of data VHDs and the appropriate Logical Unit Number (Lun).</span></span>

```powershell
$dataDiskName = $vmName + "dataDisk"
$vm = Add-AzureRmVMDataDisk -VM $vm -Name $dataDiskName -VhdUri $dataDiskUri -Lun 1 -CreateOption attach
```

<span data-ttu-id="cef1b-218">Cuando se use una cuenta de almacenamiento, las direcciones URL de los discos de datos y del sistema operativo tienen un formato similar al siguiente: `https://StorageAccountName.blob.core.windows.net/BlobContainerName/DiskName.vhd`.</span><span class="sxs-lookup"><span data-stu-id="cef1b-218">When using a storage account, the data and operating system disk URLs look something like this: `https://StorageAccountName.blob.core.windows.net/BlobContainerName/DiskName.vhd`.</span></span> <span data-ttu-id="cef1b-219">Para encontrarla en el portal, diríjase al contenedor de almacenamiento de destino, haga clic en el VHD de datos o del sistema operativo que se ha copiado y copie el contenido de la dirección URL.</span><span class="sxs-lookup"><span data-stu-id="cef1b-219">You can find this on the portal by browsing to the target storage container, clicking the operating system or data VHD that was copied, and then copying the contents of the URL.</span></span>


### <a name="complete-the-vm"></a><span data-ttu-id="cef1b-220">Completar la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="cef1b-220">Complete the VM</span></span> 

<span data-ttu-id="cef1b-221">Cree la máquina virtual con las configuraciones que acaba de crear.</span><span class="sxs-lookup"><span data-stu-id="cef1b-221">Create the VM using the configurations that we just created.</span></span>

```powershell
#Create the new VM
New-AzureRmVM -ResourceGroupName $rgName -Location $location -VM $vm
```

<span data-ttu-id="cef1b-222">Si este comando es correcto, verá un resultado similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="cef1b-222">If this command was successful, you'll see output like this:</span></span>

```powershell
RequestId IsSuccessStatusCode StatusCode ReasonPhrase
--------- ------------------- ---------- ------------
                         True         OK OK   

```

### <a name="verify-that-the-vm-was-created"></a><span data-ttu-id="cef1b-223">Comprobación de que se creó la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="cef1b-223">Verify that the VM was created</span></span>
<span data-ttu-id="cef1b-224">Debería ver la máquina virtual recién creada en el [portal de Azure](https://portal.azure.com), en **Examinar** > **Máquinas virtuales** o mediante los comandos de PowerShell siguientes:</span><span class="sxs-lookup"><span data-stu-id="cef1b-224">You should see the newly created VM either in the [Azure portal](https://portal.azure.com), under **Browse** > **Virtual machines**, or by using the following PowerShell commands:</span></span>

```powershell
$vmList = Get-AzureRmVM -ResourceGroupName $rgName
$vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="cef1b-225">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="cef1b-225">Next steps</span></span>
<span data-ttu-id="cef1b-226">Para iniciar sesión en la nueva máquina virtual, examine la máquina virtual en el [Portal](https://portal.azure.com), haga clic en **Conectar**y abra el archivo RDP del Escritorio remoto.</span><span class="sxs-lookup"><span data-stu-id="cef1b-226">To sign in to your new virtual machine, browse to the VM in the [portal](https://portal.azure.com), click **Connect**, and open the Remote Desktop RDP file.</span></span> <span data-ttu-id="cef1b-227">Utilice las credenciales de cuenta de la máquina virtual original para iniciar sesión en la nueva máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="cef1b-227">Use the account credentials of your original virtual machine to sign in to your new virtual machine.</span></span> <span data-ttu-id="cef1b-228">Para más información, consulte [Conexión a una máquina virtual de Azure donde se ejecuta Windows Server e inicio de sesión en ella](connect-logon.md).</span><span class="sxs-lookup"><span data-stu-id="cef1b-228">For more information, see [How to connect and log on to an Azure virtual machine running Windows](connect-logon.md).</span></span>

