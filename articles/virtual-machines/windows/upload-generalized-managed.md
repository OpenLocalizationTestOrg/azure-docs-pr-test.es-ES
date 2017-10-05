---
title: "Creación de una VM de Azure administrada a partir de un VHD local generalizado | Microsoft Docs"
description: "Cargue un VHD generalizado en Azure y úselo para crear máquinas virtuales nuevas en el modelo de implementación de Resource Manager."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: cynthn
ms.openlocfilehash: d802ba16ecb4e32e2adb7be3a8e99c72a1625841
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="upload-a-generalized-vhd-and-use-it-to-create-new-vms-in-azure"></a><span data-ttu-id="bd3ea-103">Carga de un VHD generalizado y su uso para crear máquinas virtuales nuevas en Azure</span><span class="sxs-lookup"><span data-stu-id="bd3ea-103">Upload a generalized VHD and use it to create new VMs in Azure</span></span>

<span data-ttu-id="bd3ea-104">En este tema se explica cómo usar PowerShell para cargar un VHD de una máquina virtual generalizada en Azure, crear una imagen a partir del VHD y crear una máquina virtual nueva desde esa imagen.</span><span class="sxs-lookup"><span data-stu-id="bd3ea-104">This topic walks you through using PowerShell to upload a VHD of a generalized VM to Azure, create an image from the VHD and create a new VM from that image.</span></span> <span data-ttu-id="bd3ea-105">Puede cargar un VHD exportado de una herramienta de visualización local o desde otra nube.</span><span class="sxs-lookup"><span data-stu-id="bd3ea-105">You can upload a VHD exported from an on-premises virtualization tool or from another cloud.</span></span> <span data-ttu-id="bd3ea-106">Usar [Managed Disks](managed-disks-overview.md) para la nueva VM simplifica la administración de la VM y proporciona una mejor disponibilidad cuando la VM se encuentra en un conjunto de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="bd3ea-106">Using [Managed Disks](managed-disks-overview.md) for the new VM simplifies the VM managment and provides better availability when the VM is placed in an availability set.</span></span> 

<span data-ttu-id="bd3ea-107">Si desea usar un script de ejemplo, consulte [Script de ejemplo para cargar un disco duro virtual en Azure y crear una máquina virtual nueva](../scripts/virtual-machines-windows-powershell-upload-generalized-script.md)</span><span class="sxs-lookup"><span data-stu-id="bd3ea-107">If you want to use a sample script, see [Sample script to upload a VHD to Azure and create a new VM](../scripts/virtual-machines-windows-powershell-upload-generalized-script.md)</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="bd3ea-108">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="bd3ea-108">Before you begin</span></span>

- <span data-ttu-id="bd3ea-109">Antes de cargar los VHD en Azure, debe consultar [Preparación de un VHD o un VHDX de Windows antes de cargarlo en Azure](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="bd3ea-109">Before uploading any VHD to Azure, you should follow [Prepare a Windows VHD or VHDX to upload to Azure](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>
- <span data-ttu-id="bd3ea-110">Revise [Plan for the migration to Managed Disks](on-prem-to-azure.md#plan-for-the-migration-to-managed-disks) (Planeación de la migración a Managed Disks) antes de comenzar la migración a [Managed Disks](managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bd3ea-110">Review [Plan for the migration to Managed Disks](on-prem-to-azure.md#plan-for-the-migration-to-managed-disks) before starting your migration to [Managed Disks](managed-disks-overview.md).</span></span>
- <span data-ttu-id="bd3ea-111">Asegúrese de que tiene la última versión del módulo AzureRM.Compute de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bd3ea-111">Make sure that you have the latest version of the AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="bd3ea-112">Ejecute el siguiente comando para realizar la instalación.</span><span class="sxs-lookup"><span data-stu-id="bd3ea-112">Run the following command to install it.</span></span>

    ```powershell
    Install-Module AzureRM.Compute -RequiredVersion 2.6.0
    ```
    <span data-ttu-id="bd3ea-113">Para más información, consulte [Azure PowerShell Versioning](/powershell/azure/overview) (Control de versiones de Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="bd3ea-113">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


## <a name="generalize-the-windows-vm-using-sysprep"></a><span data-ttu-id="bd3ea-114">Generalización de VM con Windows mediante Sysprep</span><span class="sxs-lookup"><span data-stu-id="bd3ea-114">Generalize the Windows VM using Sysprep</span></span>

<span data-ttu-id="bd3ea-115">Entre otras características, Sysprep elimina toda la información personal de la cuenta y prepara, entre otras cosas, la máquina para usarse como imagen.</span><span class="sxs-lookup"><span data-stu-id="bd3ea-115">Sysprep removes all your personal account information, among other things, and prepares the machine to be used as an image.</span></span> <span data-ttu-id="bd3ea-116">Para obtener más información sobre Sysprep, vea [Uso de Sysprep: Introducción](http://technet.microsoft.com/library/bb457073.aspx).</span><span class="sxs-lookup"><span data-stu-id="bd3ea-116">For details about Sysprep, see [How to Use Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span>

<span data-ttu-id="bd3ea-117">Asegúrese de que los roles de servidor que se ejecutan en la máquina sean compatibles con Sysprep.</span><span class="sxs-lookup"><span data-stu-id="bd3ea-117">Make sure the server roles running on the machine are supported by Sysprep.</span></span> <span data-ttu-id="bd3ea-118">Para más información, consulte [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span><span class="sxs-lookup"><span data-stu-id="bd3ea-118">For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bd3ea-119">Si ejecuta Sysprep antes de cargar el VHD en Azure por primera vez, asegúrese de que tiene [preparada la máquina virtual](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) antes de ejecutar Sysprep.</span><span class="sxs-lookup"><span data-stu-id="bd3ea-119">If you are running Sysprep before uploading your VHD to Azure for the first time, make sure you have [prepared your VM](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before running Sysprep.</span></span> 
> 
> 

1. <span data-ttu-id="bd3ea-120">Inicie sesión en la máquina virtual de Windows.</span><span class="sxs-lookup"><span data-stu-id="bd3ea-120">Sign in to the Windows virtual machine.</span></span>
2. <span data-ttu-id="bd3ea-121">Abra una ventana del símbolo del sistema como administrador.</span><span class="sxs-lookup"><span data-stu-id="bd3ea-121">Open the Command Prompt window as an administrator.</span></span> <span data-ttu-id="bd3ea-122">Cambie el directorio a **%windir%\system32\sysprep** y, después, ejecute `sysprep.exe`.</span><span class="sxs-lookup"><span data-stu-id="bd3ea-122">Change the directory to **%windir%\system32\sysprep**, and then run `sysprep.exe`.</span></span>
3. <span data-ttu-id="bd3ea-123">En **Herramienta de preparación del sistema**, seleccione **Iniciar la Configuración rápida (OOBE)** y asegúrese de que la casilla **Generalizar** está activada.</span><span class="sxs-lookup"><span data-stu-id="bd3ea-123">In the **System Preparation Tool** dialog box, select **Enter System Out-of-Box Experience (OOBE)**, and make sure that the **Generalize** check box is selected.</span></span>
4. <span data-ttu-id="bd3ea-124">En **Opciones de apagado**, seleccione **Apagar**.</span><span class="sxs-lookup"><span data-stu-id="bd3ea-124">In **Shutdown Options**, select **Shutdown**.</span></span>
5. <span data-ttu-id="bd3ea-125">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="bd3ea-125">Click **OK**.</span></span>
   
    ![Iniciar Sysprep](./media/upload-generalized-managed/sysprepgeneral.png)
6. <span data-ttu-id="bd3ea-127">Cuando Sysprep finaliza, apaga la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="bd3ea-127">When Sysprep completes, it shuts down the virtual machine.</span></span> <span data-ttu-id="bd3ea-128">No reinicie la VM.</span><span class="sxs-lookup"><span data-stu-id="bd3ea-128">Do not restart the VM.</span></span>



## <a name="log-in-to-azure"></a><span data-ttu-id="bd3ea-129">Inicie sesión en Azure.</span><span class="sxs-lookup"><span data-stu-id="bd3ea-129">Log in to Azure</span></span>
<span data-ttu-id="bd3ea-130">Si todavía no la ha instalado la versión 1.4 de PowerShell u otra superior, consulte [Cómo instalar y configurar Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="bd3ea-130">If you don't already have PowerShell version 1.4 or above installed, read [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

1. <span data-ttu-id="bd3ea-131">Abra Azure PowerShell e inicie sesión en la cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="bd3ea-131">Open Azure PowerShell and sign in to your Azure account.</span></span> <span data-ttu-id="bd3ea-132">Se abrirá una ventana emergente para que escriba sus credenciales de cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="bd3ea-132">A pop-up window opens for you to enter your Azure account credentials.</span></span>
   
    ```powershell
    Login-AzureRmAccount
    ```
2. <span data-ttu-id="bd3ea-133">Obtenga los identificadores de suscripción para las suscripciones disponibles.</span><span class="sxs-lookup"><span data-stu-id="bd3ea-133">Get the subscription IDs for your available subscriptions.</span></span>
   
    ```powershell
    Get-AzureRmSubscription
    ```
3. <span data-ttu-id="bd3ea-134">Establezca la suscripción correcta con el identificador de suscripción.</span><span class="sxs-lookup"><span data-stu-id="bd3ea-134">Set the correct subscription using the subscription ID.</span></span> <span data-ttu-id="bd3ea-135">Reemplace *<subscriptionID>* por el identificador de la suscripción correcta.</span><span class="sxs-lookup"><span data-stu-id="bd3ea-135">Replace *<subscriptionID>* with the ID of the correct subscription.</span></span>
   
    ```powershell
    Select-AzureRmSubscription -SubscriptionId "<subscriptionID>"
    ```

## <a name="get-the-storage-account"></a><span data-ttu-id="bd3ea-136">Obtención de la cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="bd3ea-136">Get the storage account</span></span>
<span data-ttu-id="bd3ea-137">Necesita una cuenta de almacenamiento de Azure para almacenar la imagen de VM cargada.</span><span class="sxs-lookup"><span data-stu-id="bd3ea-137">You need a storage account in Azure to store the uploaded VM image.</span></span> <span data-ttu-id="bd3ea-138">Puede usar una cuenta de almacenamiento existente o crear una nueva.</span><span class="sxs-lookup"><span data-stu-id="bd3ea-138">You can either use an existing storage account or create a new one.</span></span> 

<span data-ttu-id="bd3ea-139">Si va a usar el VHD para crear un disco administrado para una VM, la ubicación de la cuenta de almacenamiento debe ser la misma ubicación donde va a crear la VM.</span><span class="sxs-lookup"><span data-stu-id="bd3ea-139">If you will be using the VHD to create a managed disk for a VM, the storage account location must be same the location where you will be creating the VM.</span></span>

<span data-ttu-id="bd3ea-140">Para mostrar las cuentas de almacenamiento disponibles, escriba:</span><span class="sxs-lookup"><span data-stu-id="bd3ea-140">To show the available storage accounts, type:</span></span>

```powershell
Get-AzureRmStorageAccount
```

<span data-ttu-id="bd3ea-141">Si desea utilizar una cuenta de almacenamiento existente, puede continuar con la sección [Carga de la imagen de VM en la cuenta de almacenamiento](#upload-the-vm-vhd-to-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="bd3ea-141">If you want to use an existing storage account, proceed to the [Upload the VM image](#upload-the-vm-vhd-to-your-storage-account) section.</span></span>

<span data-ttu-id="bd3ea-142">Si necesita crear una nueva cuenta de almacenamiento, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="bd3ea-142">If you need to create a storage account, follow these steps:</span></span>

1. <span data-ttu-id="bd3ea-143">Necesita el nombre del grupo de recursos donde se debe crear la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="bd3ea-143">You need the name of the resource group where the storage account should be created.</span></span> <span data-ttu-id="bd3ea-144">Para averiguar todos los grupos de recursos que están en la suscripción, escriba:</span><span class="sxs-lookup"><span data-stu-id="bd3ea-144">To find out all the resource groups that are in your subscription, type:</span></span>
   
    ```powershell
    Get-AzureRmResourceGroup
    ```

    <span data-ttu-id="bd3ea-145">Para crear un grupo de recursos denominado **myResourceGroup** en la región **Este de EE. UU.**, escriba:</span><span class="sxs-lookup"><span data-stu-id="bd3ea-145">To create a resource group named **myResourceGroup** in the **East US** region, type:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "East US"
    ```

2. <span data-ttu-id="bd3ea-146">Cree una cuenta de almacenamiento denominada **mystorageaccount** en este grupo de recursos con el cmdlet [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount):</span><span class="sxs-lookup"><span data-stu-id="bd3ea-146">Create a storage account named **mystorageaccount** in this resource group by using the [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:</span></span>
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "East US"`
        -SkuName "Standard_LRS" -Kind "Storage"
    ```
   
    <span data-ttu-id="bd3ea-147">Los valores válidos para - SkuName son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="bd3ea-147">Valid values for -SkuName are:</span></span>
   
   * <span data-ttu-id="bd3ea-148">**Standard_LRS**: Almacenamiento con redundancia local.</span><span class="sxs-lookup"><span data-stu-id="bd3ea-148">**Standard_LRS** - Locally redundant storage.</span></span> 
   * <span data-ttu-id="bd3ea-149">**Standard_ZRS**: Almacenamiento con redundancia de zona.</span><span class="sxs-lookup"><span data-stu-id="bd3ea-149">**Standard_ZRS** - Zone redundant storage.</span></span>
   * <span data-ttu-id="bd3ea-150">**Standard_GRS**: Almacenamiento con redundancia geográfica.</span><span class="sxs-lookup"><span data-stu-id="bd3ea-150">**Standard_GRS** - Geo redundant storage.</span></span> 
   * <span data-ttu-id="bd3ea-151">**Standard_RAGRS**: Almacenamiento con redundancia geográfica con acceso de lectura.</span><span class="sxs-lookup"><span data-stu-id="bd3ea-151">**Standard_RAGRS** - Read access geo redundant storage.</span></span> 
   * <span data-ttu-id="bd3ea-152">**Premium_LRS**: Almacenamiento con redundancia local premium.</span><span class="sxs-lookup"><span data-stu-id="bd3ea-152">**Premium_LRS** - Premium locally redundant storage.</span></span> 

## <a name="upload-the-vhd-to-your-storage-account"></a><span data-ttu-id="bd3ea-153">Carga del VHD en la cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="bd3ea-153">Upload the VHD to your storage account</span></span>

<span data-ttu-id="bd3ea-154">Use el cmdlet [Add-AzureRmVhd](https://msdn.microsoft.com/library/mt603554.aspx) para cargar el VHD en un contenedor de su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="bd3ea-154">Use the [Add-AzureRmVhd](https://msdn.microsoft.com/library/mt603554.aspx) cmdlet to upload the VHD to a container in your storage account.</span></span> <span data-ttu-id="bd3ea-155">En este ejemplo se carga el archivo *myVHD.vhd* de *"C:\Users\Public\Documents\Virtual hard disks\"* para una cuenta de almacenamiento denominada *mystorageaccount* en el grupo de recursos *myResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="bd3ea-155">This example uploads the file *myVHD.vhd* from *"C:\Users\Public\Documents\Virtual hard disks\"* to a storage account named *mystorageaccount* in the *myResourceGroup* resource group.</span></span> <span data-ttu-id="bd3ea-156">El archivo se colocará en el contenedor llamado *mycontainer* y el nuevo nombre de archivo será *myUploadedVHD.vhd*.</span><span class="sxs-lookup"><span data-stu-id="bd3ea-156">The file will be placed into the container named *mycontainer* and the new file name will be *myUploadedVHD.vhd*.</span></span>

```powershell
$rgName = "myResourceGroup"
$urlOfUploadedImageVhd = "https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd"
Add-AzureRmVhd -ResourceGroupName $rgName -Destination $urlOfUploadedImageVhd `
    -LocalFilePath "C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd"
```


<span data-ttu-id="bd3ea-157">Si se realiza correctamente, obtendrá una respuesta similar a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="bd3ea-157">If successful, you get a response that looks similar to this:</span></span>

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

<span data-ttu-id="bd3ea-158">Dependiendo de la conexión de red y del tamaño del archivo VHD, este comando tardará algún tiempo en completarse.</span><span class="sxs-lookup"><span data-stu-id="bd3ea-158">Depending on your network connection and the size of your VHD file, this command may take a while to complete</span></span>

<span data-ttu-id="bd3ea-159">Guarde la ruta de acceso del **URI de destino** para usarla más adelante si va a crear un disco administrado o una nueva VM usando el VHD cargado.</span><span class="sxs-lookup"><span data-stu-id="bd3ea-159">Save the **Destination URI** path to use later if you are going to create a managed disk or a new VM using the uploaded VHD.</span></span>

### <a name="other-options-for-uploading-a-vhd"></a><span data-ttu-id="bd3ea-160">Otras opciones para cargar un disco duro virtual</span><span class="sxs-lookup"><span data-stu-id="bd3ea-160">Other options for uploading a VHD</span></span>
 
 
<span data-ttu-id="bd3ea-161">También puede cargar un VHD en la cuenta de almacenamiento mediante uno de los siguientes medios:</span><span class="sxs-lookup"><span data-stu-id="bd3ea-161">You can also upload a VHD to your storage account using one of the following:</span></span>

- [<span data-ttu-id="bd3ea-162">AzCopy</span><span class="sxs-lookup"><span data-stu-id="bd3ea-162">AzCopy</span></span>](http://aka.ms/downloadazcopy)
- [<span data-ttu-id="bd3ea-163">API de tipo Copy Blob de Almacenamiento Azure</span><span class="sxs-lookup"><span data-stu-id="bd3ea-163">Azure Storage Copy Blob API</span></span>](https://msdn.microsoft.com/library/azure/dd894037.aspx)
- [<span data-ttu-id="bd3ea-164">Blobs de carga de Azure Storage Explorer</span><span class="sxs-lookup"><span data-stu-id="bd3ea-164">Azure Storage Explorer Uploading Blobs</span></span>](https://azurestorageexplorer.codeplex.com/)
- [<span data-ttu-id="bd3ea-165">Referencia de la API de REST de servicios de importación y exportación de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="bd3ea-165">Storage Import/Export Service REST API Reference</span></span>](https://msdn.microsoft.com/library/dn529096.aspx)
-   <span data-ttu-id="bd3ea-166">Se recomienda utilizar el servicio Import/Export si se calcula que el tiempo de carga va a ser superior a siete días.</span><span class="sxs-lookup"><span data-stu-id="bd3ea-166">We recommend using Import/Export Service if estimated uploading time is longer than 7 days.</span></span> <span data-ttu-id="bd3ea-167">Puede usar [DataTransferSpeedCalculator](https://github.com/Azure-Samples/storage-dotnet-import-export-job-management/blob/master/DataTransferSpeedCalculator.html) para calcular el tiempo a partir del tamaño de los datos y la unidad de transferencia.</span><span class="sxs-lookup"><span data-stu-id="bd3ea-167">You can use [DataTransferSpeedCalculator](https://github.com/Azure-Samples/storage-dotnet-import-export-job-management/blob/master/DataTransferSpeedCalculator.html) to estimate the time from data size and transfer unit.</span></span> 
    <span data-ttu-id="bd3ea-168">Import/Export se puede usar para realizar copias en una cuenta de almacenamiento estándar.</span><span class="sxs-lookup"><span data-stu-id="bd3ea-168">Import/Export can be used to copy to a standard storage account.</span></span> <span data-ttu-id="bd3ea-169">Para copiar desde el almacenamiento estándar a una cuenta de Almacenamiento premium, use una herramienta como AzCopy.</span><span class="sxs-lookup"><span data-stu-id="bd3ea-169">You will need to copy from standard storage to premium storage account using a tool like AzCopy.</span></span>


## <a name="create-a-managed-image-from-the-uploaded-vhd"></a><span data-ttu-id="bd3ea-170">Creación de una imagen administrada desde el VHD cargado</span><span class="sxs-lookup"><span data-stu-id="bd3ea-170">Create a managed image from the uploaded VHD</span></span> 

<span data-ttu-id="bd3ea-171">Cree una imagen administrada con el VHD del SO generalizado.</span><span class="sxs-lookup"><span data-stu-id="bd3ea-171">Create a managed image using your generalized OS VHD.</span></span> <span data-ttu-id="bd3ea-172">Reemplace los valores por su propia información.</span><span class="sxs-lookup"><span data-stu-id="bd3ea-172">Replace the values with your own information.</span></span>


1.  <span data-ttu-id="bd3ea-173">En primer lugar, establezca los parámetros comunes:</span><span class="sxs-lookup"><span data-stu-id="bd3ea-173">First, set the common parameters:</span></span>

    ```powershell
    $vmName = "myVM"
    $computerName = "myComputer"
    $vmSize = "Standard_DS1_v2"
    $location = "East US" 
    $imageName = "yourImageName"
    ```

4.  <span data-ttu-id="bd3ea-174">Cree la imagen con el VHD del SO generalizado.</span><span class="sxs-lookup"><span data-stu-id="bd3ea-174">Create the image using your generalized OS VHD.</span></span>

    ```powershell
    $imageConfig = New-AzureRmImageConfig -Location $location
    $imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsType Windows -OsState Generalized -BlobUri $urlOfUploadedImageVhd
    $image = New-AzureRmImage -ImageName $imageName -ResourceGroupName $rgName -Image $imageConfig
    ```

## <a name="create-a-virtual-network"></a><span data-ttu-id="bd3ea-175">Crear una red virtual</span><span class="sxs-lookup"><span data-stu-id="bd3ea-175">Create a virtual network</span></span>
<span data-ttu-id="bd3ea-176">Cree la red virtual y la subred de la [red virtual](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bd3ea-176">Create the vNet and subnet of the [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

1. <span data-ttu-id="bd3ea-177">Cree la subred.</span><span class="sxs-lookup"><span data-stu-id="bd3ea-177">Create the subnet.</span></span> <span data-ttu-id="bd3ea-178">Este ejemplo crea una subred denominada *mySubnet* con el prefijo de dirección *10.0.0.0/24*.</span><span class="sxs-lookup"><span data-stu-id="bd3ea-178">This example creates a subnet named *mySubnet* with the address prefix of *10.0.0.0/24*.</span></span>  
   
    ```powershell
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. <span data-ttu-id="bd3ea-179">Creación de la red virtual.</span><span class="sxs-lookup"><span data-stu-id="bd3ea-179">Create the virtual network.</span></span> <span data-ttu-id="bd3ea-180">Este ejemplo crea una red virtual denominada *myVnet* con el prefijo de dirección *10.0.0.0/16*.</span><span class="sxs-lookup"><span data-stu-id="bd3ea-180">This example creates a virtual network named *myVnet* with the address prefix of *10.0.0.0/16*.</span></span>  
   
    ```powershell
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

## <a name="create-a-public-ip-address-and-network-interface"></a><span data-ttu-id="bd3ea-181">Creación de una dirección IP y una interfaz de red</span><span class="sxs-lookup"><span data-stu-id="bd3ea-181">Create a public IP address and network interface</span></span>

<span data-ttu-id="bd3ea-182">Para permitir la comunicación con la máquina virtual en la red virtual, necesitará una [dirección IP pública](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) y una interfaz de red.</span><span class="sxs-lookup"><span data-stu-id="bd3ea-182">To enable communication with the virtual machine in the virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

1. <span data-ttu-id="bd3ea-183">Cree una dirección IP pública.</span><span class="sxs-lookup"><span data-stu-id="bd3ea-183">Create a public IP address.</span></span> <span data-ttu-id="bd3ea-184">Este ejemplo crea una dirección IP pública denominada "*myPip*".</span><span class="sxs-lookup"><span data-stu-id="bd3ea-184">This example creates a public IP address named *myPip*.</span></span> 
   
    ```powershell
    $ipName = "myPip"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. <span data-ttu-id="bd3ea-185">Cree la NIC.</span><span class="sxs-lookup"><span data-stu-id="bd3ea-185">Create the NIC.</span></span> <span data-ttu-id="bd3ea-186">Este ejemplo crea una NIC denominada "**myNic**".</span><span class="sxs-lookup"><span data-stu-id="bd3ea-186">This example creates a NIC named **myNic**.</span></span> 
   
    ```powershell
    $nicName = "myNic"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName -Location $location `
        -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

## <a name="create-the-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="bd3ea-187">Creación del grupo de seguridad de red y las reglas de RDP</span><span class="sxs-lookup"><span data-stu-id="bd3ea-187">Create the network security group and an RDP rule</span></span>

<span data-ttu-id="bd3ea-188">Para poder iniciar sesión en la VM mediante RDP, debe tener una regla de seguridad de red (NSG) que permita el acceso RDP en el puerto 3389.</span><span class="sxs-lookup"><span data-stu-id="bd3ea-188">To be able to log in to your VM using RDP, you need to have a network security rule (NSG) that allows RDP access on port 3389.</span></span> 

<span data-ttu-id="bd3ea-189">Este ejemplo crea un NSG denominado"*myNsg*" que contiene una regla llamada "*myRdpRule*" que permita el tráfico RDP en el puerto 3389.</span><span class="sxs-lookup"><span data-stu-id="bd3ea-189">This example creates an NSG named *myNsg* that contains a rule called *myRdpRule* that allows RDP traffic over port 3389.</span></span> <span data-ttu-id="bd3ea-190">Para obtener más información sobre NSG, consulte [Apertura de puertos para una máquina virtual en Azure mediante PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="bd3ea-190">For more information about NSGs, see [Opening ports to a VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

```powershell
$nsgName = "myNsg"
$ruleName = "myRdpRule"
$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name $ruleName -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389

$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
```


## <a name="create-a-variable-for-the-virtual-network"></a><span data-ttu-id="bd3ea-191">Creación de una variable para la red virtual</span><span class="sxs-lookup"><span data-stu-id="bd3ea-191">Create a variable for the virtual network</span></span>

<span data-ttu-id="bd3ea-192">Cree una variable para la red virtual completada.</span><span class="sxs-lookup"><span data-stu-id="bd3ea-192">Create a variable for the completed virtual network.</span></span> 

```powershell
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName

```

## <a name="get-the-credentials-for-the-vm"></a><span data-ttu-id="bd3ea-193">Obtención de las credenciales para la VM</span><span class="sxs-lookup"><span data-stu-id="bd3ea-193">Get the credentials for the VM</span></span>

<span data-ttu-id="bd3ea-194">El siguiente cmdlet abrirá una ventana en la que escribirá un nuevo nombre de usuario y una contraseña que se usará como la cuenta de administrador local para tener acceso remoto a la VM.</span><span class="sxs-lookup"><span data-stu-id="bd3ea-194">The following cmdlet will open a window where you will enter a new user name and password to use as the local administrator account for remotely accessing the VM.</span></span> 

```powershell
$cred = Get-Credential
```

## <a name="add-the-vm-name-and-size-to-the-vm-configuration"></a><span data-ttu-id="bd3ea-195">Agregue el nombre y el tamaño de la VM a la configuración de la VM.</span><span class="sxs-lookup"><span data-stu-id="bd3ea-195">Add the VM name and size to the VM configuration.</span></span>

```powershell
$vm = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize
```

## <a name="set-the-vm-image-as-source-image-for-the-new-vm"></a><span data-ttu-id="bd3ea-196">Establecimiento de la imagen de VM como imagen de origen para la nueva VM</span><span class="sxs-lookup"><span data-stu-id="bd3ea-196">Set the VM image as source image for the new VM</span></span>

<span data-ttu-id="bd3ea-197">Establezca la imagen de origen con el identificador de la imagen de VM administrada.</span><span class="sxs-lookup"><span data-stu-id="bd3ea-197">Set the source image using the ID of the managed VM image.</span></span>

```powershell
$vm = Set-AzureRmVMSourceImage -VM $vm -Id $image.Id
```

## <a name="set-the-os-configuration-and-add-the-nic"></a><span data-ttu-id="bd3ea-198">Establezca la configuración del SO y agregue la NIC.</span><span class="sxs-lookup"><span data-stu-id="bd3ea-198">Set the OS configuration and add the NIC.</span></span>

<span data-ttu-id="bd3ea-199">Escriba el tipo de almacenamiento (PremiumLRS o StandardLRS) y el tamaño del disco del SO.</span><span class="sxs-lookup"><span data-stu-id="bd3ea-199">Enter the storage type (PremiumLRS or StandardLRS) and the size of the OS disk.</span></span> <span data-ttu-id="bd3ea-200">Este ejemplo establece el tipo de cuenta en *PremiumLRS*, el tamaño del disco en *128 GB* y el almacenamiento en caché en disco en *ReadWrite*.</span><span class="sxs-lookup"><span data-stu-id="bd3ea-200">This example sets the account type to *PremiumLRS*, the disk size to *128 GB* and disk caching to *ReadWrite*.</span></span>

```powershell
$vm = Set-AzureRmVMOSDisk -VM $vm -DiskSizeInGB 128 `
-CreateOption FromImage -Caching ReadWrite

$vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName $computerName `
-Credential $cred -ProvisionVMAgent -EnableAutoUpdate

$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

## <a name="create-the-vm"></a><span data-ttu-id="bd3ea-201">Creación de la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="bd3ea-201">Create the VM</span></span>

<span data-ttu-id="bd3ea-202">Cree la nueva máquina virtual con la configuración almacenada en la variable **$vm**.</span><span class="sxs-lookup"><span data-stu-id="bd3ea-202">Create the new VM using the configuration stored in the **$vm** variable.</span></span>

```powershell
New-AzureRmVM -VM $vm -ResourceGroupName $rgName -Location $location
```

## <a name="verify-that-the-vm-was-created"></a><span data-ttu-id="bd3ea-203">Comprobación de que se creó la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="bd3ea-203">Verify that the VM was created</span></span>
<span data-ttu-id="bd3ea-204">Cuando finalice, debería ver la máquina virtual recién creada en el [Azure Portal](https://portal.azure.com), en **Examinar** > **Máquinas virtuales** o mediante los comandos de PowerShell siguientes:</span><span class="sxs-lookup"><span data-stu-id="bd3ea-204">When complete, you should see the newly created VM in the [Azure portal](https://portal.azure.com) under **Browse** > **Virtual machines**, or by using the following PowerShell commands:</span></span>

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="bd3ea-205">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="bd3ea-205">Next steps</span></span>

<span data-ttu-id="bd3ea-206">Para iniciar sesión en la nueva máquina virtual, examine la máquina virtual en el [Portal](https://portal.azure.com), haga clic en **Conectar**y abra el archivo RDP del Escritorio remoto.</span><span class="sxs-lookup"><span data-stu-id="bd3ea-206">To sign in to your new virtual machine, browse to the VM in the [portal](https://portal.azure.com), click **Connect**, and open the Remote Desktop RDP file.</span></span> <span data-ttu-id="bd3ea-207">Utilice las credenciales de cuenta de la máquina virtual original para iniciar sesión en la nueva máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="bd3ea-207">Use the account credentials of your original virtual machine to sign in to your new virtual machine.</span></span> <span data-ttu-id="bd3ea-208">Para más información, consulte [Conexión a una máquina virtual de Azure donde se ejecuta Windows Server e inicio de sesión en ella](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="bd3ea-208">For more information, see [How to connect and log on to an Azure virtual machine running Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

