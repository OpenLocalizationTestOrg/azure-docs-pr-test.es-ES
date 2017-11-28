---
title: "Creación de una imagen de máquina virtual de forma local para Azure Marketplace | Microsoft Docs"
description: "Entienda y ejecute los pasos para crear una imagen de máquina virtual de forma local e impleméntela en Azure Marketplace para que otros usuarios la compren."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 26dfbd5a-8685-4b19-987e-c20ca60540ec
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Azure
ms.workload: na
ms.date: 04/29/2016
ms.author: hascipio; v-divte
ms.openlocfilehash: 8f6b9a9293dc149586e6e5fd55028170ea825b07
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="develop-an-on-premises-virtual-machine-image-for-the-azure-marketplace"></a><span data-ttu-id="8d9c6-103">Desarrollo de una imagen de máquina virtual de forma local para Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="8d9c6-103">Develop an on-premises virtual machine image for the Azure Marketplace</span></span>
<span data-ttu-id="8d9c6-104">Se recomienda encarecidamente que desarrolle discos duros virtuales de Azure (VHD) directamente en la nube mediante el uso del Protocolo de escritorio remoto.</span><span class="sxs-lookup"><span data-stu-id="8d9c6-104">We strongly recommend that you develop Azure virtual hard disks (VHDs) directly in the cloud by using Remote Desktop Protocol.</span></span> <span data-ttu-id="8d9c6-105">Sin embargo, si es necesario, es posible descargar un disco duro virtual y desarrollarlo mediante infraestructura local.</span><span class="sxs-lookup"><span data-stu-id="8d9c6-105">However, if you must, it is possible to download a VHD and develop it by using on-premises infrastructure.</span></span>  

<span data-ttu-id="8d9c6-106">Para el desarrollo local, debe descargar el disco duro virtual del sistema operativo de la máquina virtual creada.</span><span class="sxs-lookup"><span data-stu-id="8d9c6-106">For on-premises development, you must download the operating system VHD of the created VM.</span></span> <span data-ttu-id="8d9c6-107">Estos pasos tendrán lugar como parte del paso 3.3, arriba.</span><span class="sxs-lookup"><span data-stu-id="8d9c6-107">These steps would take place as part of step 3.3, above.</span></span>  

## <a name="download-a-vhd-image"></a><span data-ttu-id="8d9c6-108">Descargar una imagen de disco duro virtual</span><span class="sxs-lookup"><span data-stu-id="8d9c6-108">Download a VHD image</span></span>
### <a name="locate-a-blob-url"></a><span data-ttu-id="8d9c6-109">Búsqueda de la dirección URL de blob</span><span class="sxs-lookup"><span data-stu-id="8d9c6-109">Locate a blob URL</span></span>
<span data-ttu-id="8d9c6-110">Para descargar el disco duro virtual, busque primero la dirección URL de blob del disco del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="8d9c6-110">In order to download the VHD, first locate the blob URL for the operating system disk.</span></span>

<span data-ttu-id="8d9c6-111">Busque la dirección URL de blob en el nuevo [Portal de Microsoft Azure](https://portal.azure.com):</span><span class="sxs-lookup"><span data-stu-id="8d9c6-111">Locate the blob URL from the new [Microsoft Azure portal](https://portal.azure.com):</span></span>

1. <span data-ttu-id="8d9c6-112">Vaya a **Examinar** > **Máquinas virtuales**, y seleccione la máquina virtual implementada.</span><span class="sxs-lookup"><span data-stu-id="8d9c6-112">Go to **Browse** > **VMs**, and then select the deployed VM.</span></span>
2. <span data-ttu-id="8d9c6-113">En **Configurar**, seleccione el icono **Discos**, lo cual abre la hoja Discos.</span><span class="sxs-lookup"><span data-stu-id="8d9c6-113">Under **Configure**, select the **Disks** tile, which opens the Disks blade.</span></span>
   
   ![dibujo](media/marketplace-publishing-vm-image-creation-on-premise/img01.png)
3. <span data-ttu-id="8d9c6-115">Seleccione el **Disco del sistema operativo**, que abre otra hoja que muestra las propiedades del disco, incluida la ubicación del disco duro virtual.</span><span class="sxs-lookup"><span data-stu-id="8d9c6-115">Select the **OS Disk**, which opens another blade that displays disk properties, including the VHD location.</span></span>
4. <span data-ttu-id="8d9c6-116">Copie esta dirección URL de blob.</span><span class="sxs-lookup"><span data-stu-id="8d9c6-116">Copy this blob URL.</span></span>
   
   ![dibujo](media/marketplace-publishing-vm-image-creation-on-premise/img02.png)
5. <span data-ttu-id="8d9c6-118">Ahora, elimine la máquina virtual implementada sin eliminar los discos de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="8d9c6-118">Now, delete the deployed VM without deleting the backing disks.</span></span> <span data-ttu-id="8d9c6-119">También puede detener la máquina virtual en lugar de eliminarla.</span><span class="sxs-lookup"><span data-stu-id="8d9c6-119">You can also stop the VM instead of deleting it.</span></span> <span data-ttu-id="8d9c6-120">No descargue el disco duro virtual del sistema operativo cuando se esté ejecutando la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="8d9c6-120">Do not download the operating system VHD when the VM is running.</span></span>
   
   ![dibujo](media/marketplace-publishing-vm-image-creation-on-premise/img03.png)

### <a name="download-a-vhd"></a><span data-ttu-id="8d9c6-122">Descarga de un disco duro virtual</span><span class="sxs-lookup"><span data-stu-id="8d9c6-122">Download a VHD</span></span>
<span data-ttu-id="8d9c6-123">Una vez que conozca la dirección URL de blob, podrá descargar el disco duro virtual mediante el [Portal de Azure](http://manage.windowsazure.com/) o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8d9c6-123">After you know the blob URL, you can download the VHD by using the [Azure portal](http://manage.windowsazure.com/) or PowerShell.</span></span>  

> [!NOTE]
> <span data-ttu-id="8d9c6-124">En el momento de la creación de esta guía, la funcionalidad para descargar un disco duro virtual no está todavía presente en el nuevo Portal de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="8d9c6-124">At the time of this guide’s creation, the functionality to download a VHD is not yet present in the new Microsoft Azure portal.</span></span>  
> 
> 

<span data-ttu-id="8d9c6-125">**Descarga del disco duro virtual del sistema operativo a través de la versión actual de [Azure Portal](http://manage.windowsazure.com/)**</span><span class="sxs-lookup"><span data-stu-id="8d9c6-125">**Download the operating system VHD via the current [Azure portal](http://manage.windowsazure.com/)**</span></span>

1. <span data-ttu-id="8d9c6-126">Si aún no lo ha hecho, inicie sesión en el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="8d9c6-126">Sign in to the Azure portal if you have not done so already.</span></span>
2. <span data-ttu-id="8d9c6-127">Haga clic en la pestaña **Almacenamiento** .</span><span class="sxs-lookup"><span data-stu-id="8d9c6-127">Click the **Storage** tab.</span></span>
3. <span data-ttu-id="8d9c6-128">Seleccione la cuenta de almacenamiento donde se almacena el disco duro virtual.</span><span class="sxs-lookup"><span data-stu-id="8d9c6-128">Select the storage account within which the VHD is stored.</span></span>
   
   ![dibujo](media/marketplace-publishing-vm-image-creation-on-premise/img04.png)
4. <span data-ttu-id="8d9c6-130">De este modo se muestran las propiedades de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="8d9c6-130">This displays storage account properties.</span></span> <span data-ttu-id="8d9c6-131">Seleccione la pestaña **Contenedores** .</span><span class="sxs-lookup"><span data-stu-id="8d9c6-131">Select the **Containers** tab.</span></span>
   
   ![dibujo](media/marketplace-publishing-vm-image-creation-on-premise/img05.png)
5. <span data-ttu-id="8d9c6-133">Seleccione el contenedor donde se almacena el disco duro virtual.</span><span class="sxs-lookup"><span data-stu-id="8d9c6-133">Select the container in which the VHD is stored.</span></span> <span data-ttu-id="8d9c6-134">De forma predeterminada, al crearse en el Portal, el disco duro virtual se almacena en un contenedor de discos duros virtuales.</span><span class="sxs-lookup"><span data-stu-id="8d9c6-134">By default, when created from the portal, the VHD is stored in a vhds container.</span></span>
   
   ![dibujo](media/marketplace-publishing-vm-image-creation-on-premise/img06.png)
6. <span data-ttu-id="8d9c6-136">Seleccione el disco duro virtual del sistema operativo correcto comparando la dirección URL con la que ha guardado.</span><span class="sxs-lookup"><span data-stu-id="8d9c6-136">Select the correct operating system VHD by comparing the URL to the one you saved.</span></span>
7. <span data-ttu-id="8d9c6-137">Haga clic en **Descargar**.</span><span class="sxs-lookup"><span data-stu-id="8d9c6-137">Click **Download**.</span></span>
   
   ![dibujo](media/marketplace-publishing-vm-image-creation-on-premise/img07.png)

### <a name="download-a-vhd-by-using-powershell"></a><span data-ttu-id="8d9c6-139">Descarga de un disco duro virtual mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="8d9c6-139">Download a VHD by using PowerShell</span></span>
<span data-ttu-id="8d9c6-140">Además de utilizar el Portal de Azure, puede usar el cmdlet [Save-AzureVhd](http://msdn.microsoft.com/library/dn495297.aspx) para descargar el disco duro virtual del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="8d9c6-140">In addition to using the Azure portal, you can use the [Save-AzureVhd](http://msdn.microsoft.com/library/dn495297.aspx) cmdlet to download the operating system VHD.</span></span>

        Save-AzureVhd –Source <storageURIOfVhd> `
        -LocalFilePath <diskLocationOnWorkstation> `
        -StorageKey <keyForStorageAccount>
<span data-ttu-id="8d9c6-141">Por ejemplo, Save-AzureVhd -Source “https://baseimagevm.blob.core.windows.net/vhds/BaseImageVM-6820cq00-BaseImageVM-os-1411003770191.vhd” -LocalFilePath “C:\Users\Administrator\Desktop\baseimagevm.vhd” -StorageKey <String></span><span class="sxs-lookup"><span data-stu-id="8d9c6-141">For example, Save-AzureVhd -Source “https://baseimagevm.blob.core.windows.net/vhds/BaseImageVM-6820cq00-BaseImageVM-os-1411003770191.vhd” -LocalFilePath “C:\Users\Administrator\Desktop\baseimagevm.vhd” -StorageKey <String></span></span>

> [!NOTE]
> <span data-ttu-id="8d9c6-142">**Save-AzureVhd** también tiene la opción **NumberOfThreads**, que puede utilizarse para aumentar el paralelismo para aprovechar al máximo el ancho de banda disponible para la descarga.</span><span class="sxs-lookup"><span data-stu-id="8d9c6-142">**Save-AzureVhd** also has a **NumberOfThreads** option that can be used to increase parallelism to make the best use of available bandwidth for the download.</span></span>
> 
> 

## <a name="upload-vhds-to-an-azure-storage-account"></a><span data-ttu-id="8d9c6-143">Cargar discos duros virtuales a una cuenta de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="8d9c6-143">Upload VHDs to an Azure storage account</span></span>
<span data-ttu-id="8d9c6-144">Si ha preparado sus discos duros virtuales de forma local, debe cargarlos en una cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="8d9c6-144">If you prepared your VHDs on-premises, you need to upload them into a storage account in Azure.</span></span> <span data-ttu-id="8d9c6-145">Este paso tendrá lugar después de crear su disco duro virtual de forma local, pero antes de obtener la certificación para la imagen de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="8d9c6-145">This step takes place after creating your VHD on-premises but before obtaining certification for your VM image.</span></span>

### <a name="create-a-storage-account-and-container"></a><span data-ttu-id="8d9c6-146">Creación de una cuenta de almacenamiento y un contenedor</span><span class="sxs-lookup"><span data-stu-id="8d9c6-146">Create a storage account and container</span></span>
<span data-ttu-id="8d9c6-147">Se recomienda que los discos duros virtuales se carguen en una cuenta de almacenamiento en una región de Estados Unidos.</span><span class="sxs-lookup"><span data-stu-id="8d9c6-147">We recommend that VHDs be uploaded into a storage account in a region in the United States.</span></span> <span data-ttu-id="8d9c6-148">Todos los discos duros virtuales de un SKU único deben colocarse en un contenedor único dentro de una cuenta de almacenamiento única.</span><span class="sxs-lookup"><span data-stu-id="8d9c6-148">All VHDs for a single SKU should be placed in a single container within a single storage account.</span></span>

<span data-ttu-id="8d9c6-149">Para crear una cuenta de almacenamiento, puede utilizar el [Portal de Microsoft Azure](https://portal.azure.com/), PowerShell o la herramienta de línea de comandos de Linux.</span><span class="sxs-lookup"><span data-stu-id="8d9c6-149">To create a storage account, you can use the [Microsoft Azure portal](https://portal.azure.com/), PowerShell, or the Linux command-line tool.</span></span>  

<span data-ttu-id="8d9c6-150">**Creación de una cuenta de almacenamiento en el Portal de Microsoft Azure**</span><span class="sxs-lookup"><span data-stu-id="8d9c6-150">**Create a storage account from the Microsoft Azure portal**</span></span>

1. <span data-ttu-id="8d9c6-151">Haga clic en **Nuevo**.</span><span class="sxs-lookup"><span data-stu-id="8d9c6-151">Click **New**.</span></span>
2. <span data-ttu-id="8d9c6-152">Seleccione **Almacenamiento**.</span><span class="sxs-lookup"><span data-stu-id="8d9c6-152">Select **Storage**.</span></span>
3. <span data-ttu-id="8d9c6-153">Indique un nombre para la cuenta de almacenamiento y luego seleccione una ubicación.</span><span class="sxs-lookup"><span data-stu-id="8d9c6-153">Fill in the storage account name, and then select a location.</span></span>
   
   ![dibujo](media/marketplace-publishing-vm-image-creation-on-premise/img08.png)
4. <span data-ttu-id="8d9c6-155">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="8d9c6-155">Click **Create**.</span></span>
5. <span data-ttu-id="8d9c6-156">La hoja de la cuenta de almacenamiento creada debe estar abierta.</span><span class="sxs-lookup"><span data-stu-id="8d9c6-156">The blade for the created storage account should be open.</span></span> <span data-ttu-id="8d9c6-157">Si no es así, seleccione **Examinar** > **Cuentas de almacenamiento**.</span><span class="sxs-lookup"><span data-stu-id="8d9c6-157">If not, select **Browse** > **Storage Accounts**.</span></span> <span data-ttu-id="8d9c6-158">En la hoja Cuenta de almacenamiento, seleccione la cuenta de almacenamiento creada.</span><span class="sxs-lookup"><span data-stu-id="8d9c6-158">On the Storage account blade, select the storage account created.</span></span>
6. <span data-ttu-id="8d9c6-159">Seleccione **Contenedores**.</span><span class="sxs-lookup"><span data-stu-id="8d9c6-159">Select **Containers**.</span></span>
   
   ![dibujo](media/marketplace-publishing-vm-image-creation-on-premise/img09.png) 
7. <span data-ttu-id="8d9c6-161">En la hoja Contenedores, seleccione **Agregar**y escriba un nombre de contenedor y los permisos de este.</span><span class="sxs-lookup"><span data-stu-id="8d9c6-161">On the Containers blade, select **Add**, and then enter a container name and the container permissions.</span></span> <span data-ttu-id="8d9c6-162">Seleccione **Privado** para los permisos del contenedor.</span><span class="sxs-lookup"><span data-stu-id="8d9c6-162">Select **Private** for container permissions.</span></span>

> [!TIP]
> <span data-ttu-id="8d9c6-163">Se recomienda crear un contenedor por SKU que pretende publicar.</span><span class="sxs-lookup"><span data-stu-id="8d9c6-163">We recommend that you create one container per SKU that you are planning to publish.</span></span>
> 
> 

  ![dibujo](media/marketplace-publishing-vm-image-creation-on-premise/img10.png)

### <a name="create-a-storage-account-by-using-powershell"></a><span data-ttu-id="8d9c6-165">Creación de una cuenta de almacenamiento mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="8d9c6-165">Create a storage account by using PowerShell</span></span>
<span data-ttu-id="8d9c6-166">Con PowerShell, cree una cuenta de almacenamiento mediante el cmdlet [New-AzureStorageAccount](http://msdn.microsoft.com/library/dn495115.aspx) .</span><span class="sxs-lookup"><span data-stu-id="8d9c6-166">Using PowerShell, create a storage account by using the [New-AzureStorageAccount](http://msdn.microsoft.com/library/dn495115.aspx) cmdlet.</span></span>

        New-AzureStorageAccount -StorageAccountName “mystorageaccount” -Location “West US”

<span data-ttu-id="8d9c6-167">A continuación, puede crear un contenedor dentro de esa cuenta de almacenamiento, con el cmdlet [NewAzureStorageContainer](http://msdn.microsoft.com/library/dn495291.aspx) .</span><span class="sxs-lookup"><span data-stu-id="8d9c6-167">Then you can create a container within that storage account by using the [NewAzureStorageContainer](http://msdn.microsoft.com/library/dn495291.aspx) cmdlet.</span></span>

        New-AzureStorageContainer -Name “containername” -Permission “Off”

> [!NOTE]
> <span data-ttu-id="8d9c6-168">Esos comandos asumen que ya se ha establecido el contexto de la cuenta de almacenamiento actual en PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8d9c6-168">Those commands assume that the current storage account context has already been set in PowerShell.</span></span>   <span data-ttu-id="8d9c6-169">Consulte [Configuración de Azure PowerShell](marketplace-publishing-powershell-setup.md) para obtener más detalles sobre la configuración de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8d9c6-169">Refer to [Setting up Azure PowerShell](marketplace-publishing-powershell-setup.md) for more details on PowerShell setup.</span></span>  
> 
> ### <a name="create-a-storage-account-by-using-the-command-line-tool-for-mac-and-linux"></a><span data-ttu-id="8d9c6-170">Creación de una cuenta de almacenamiento con la herramienta de línea de comandos para Mac y Linux</span><span class="sxs-lookup"><span data-stu-id="8d9c6-170">Create a storage account by using the command-line tool for Mac and Linux</span></span>
> <span data-ttu-id="8d9c6-171">En la [Herramienta de línea de comandos de Linux](../virtual-machines/linux/cli-manage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), cree una cuenta de almacenamiento de la manera siguiente.</span><span class="sxs-lookup"><span data-stu-id="8d9c6-171">From [Linux command-line tool](../virtual-machines/linux/cli-manage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), create a storage account as follows.</span></span>
> 
> 

        azure storage account create mystorageaccount --location "West US"

<span data-ttu-id="8d9c6-172">Cree un contenedor de la manera siguiente.</span><span class="sxs-lookup"><span data-stu-id="8d9c6-172">Create a container as follows.</span></span>

        azure storage container create containername --account-name mystorageaccount --accountkey <accountKey>

## <a name="upload-a-vhd"></a><span data-ttu-id="8d9c6-173">Carga de un disco duro virtual</span><span class="sxs-lookup"><span data-stu-id="8d9c6-173">Upload a VHD</span></span>
<span data-ttu-id="8d9c6-174">Una vez creados la cuenta de almacenamiento y el contenedor, puede cargar sus discos duros virtuales preparados.</span><span class="sxs-lookup"><span data-stu-id="8d9c6-174">After the storage account and container are created, you can upload your prepared VHDs.</span></span> <span data-ttu-id="8d9c6-175">Es posible usar PowerShell, la herramienta de línea de comandos de Linux u otras herramientas de administración de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="8d9c6-175">You can use PowerShell, the Linux command-line tool, or other Azure Storage management tools.</span></span>

### <a name="upload-a-vhd-via-powershell"></a><span data-ttu-id="8d9c6-176">Cargar un disco duro virtual a través de PowerShell</span><span class="sxs-lookup"><span data-stu-id="8d9c6-176">Upload a VHD via PowerShell</span></span>
<span data-ttu-id="8d9c6-177">Use el cmdlet [Add-AzureVhd](http://msdn.microsoft.com/library/dn495173.aspx) .</span><span class="sxs-lookup"><span data-stu-id="8d9c6-177">Use the [Add-AzureVhd](http://msdn.microsoft.com/library/dn495173.aspx) cmdlet.</span></span>

        Add-AzureVhd –Destination “http://mystorageaccount.blob.core.windows.net/containername/vmsku.vhd” -LocalFilePath “C:\Users\Administrator\Desktop\vmsku.vhd”

### <a name="upload-a-vhd-by-using-the-command-line-tool-for-mac-and-linux"></a><span data-ttu-id="8d9c6-178">Carga de un disco duro virtual con la herramienta de línea de comandos para Mac y Linux</span><span class="sxs-lookup"><span data-stu-id="8d9c6-178">Upload a VHD by using the command-line tool for Mac and Linux</span></span>
<span data-ttu-id="8d9c6-179">Con la [Herramienta de línea de comandos de Linux](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2), utilice lo siguiente: azure vm image create <image name> --location <Location of the data center> --OS Linux <LocationOfLocalVHD></span><span class="sxs-lookup"><span data-stu-id="8d9c6-179">With the [Linux command-line tool](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2), use the following: azure vm image create <image name> --location <Location of the data center> --OS Linux <LocationOfLocalVHD></span></span>

## <a name="see-also"></a><span data-ttu-id="8d9c6-180">Consulte también</span><span class="sxs-lookup"><span data-stu-id="8d9c6-180">See also</span></span>
* [<span data-ttu-id="8d9c6-181">Creación de una imagen de máquina virtual para Marketplace</span><span class="sxs-lookup"><span data-stu-id="8d9c6-181">Creating a virtual machine image for the Marketplace</span></span>](marketplace-publishing-vm-image-creation.md)
* [<span data-ttu-id="8d9c6-182">Configuración de Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="8d9c6-182">Setting up Azure PowerShell</span></span>](marketplace-publishing-powershell-setup.md)

