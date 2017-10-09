---
title: "aaaCreating una imagen de máquina virtual local para hello Azure Marketplace | Documentos de Microsoft"
description: "Entender y ejecutar Hola pasos toocreate una imagen de máquina virtual local e implementar toohello Azure Marketplace para que otros lo toopurchase."
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
ms.openlocfilehash: c7a265330f1e494db8d0e981a38ee00d85746bb1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="develop-an-on-premises-virtual-machine-image-for-hello-azure-marketplace"></a><span data-ttu-id="c4842-103">Desarrollar una imagen de máquina virtual local para hello Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="c4842-103">Develop an on-premises virtual machine image for hello Azure Marketplace</span></span>
<span data-ttu-id="c4842-104">Se recomienda encarecidamente que desarrollar Azure discos duros virtuales (VHD) directamente en la nube de hello mediante Protocolo de escritorio remoto.</span><span class="sxs-lookup"><span data-stu-id="c4842-104">We strongly recommend that you develop Azure virtual hard disks (VHDs) directly in hello cloud by using Remote Desktop Protocol.</span></span> <span data-ttu-id="c4842-105">Sin embargo, si es necesario, es posible toodownload un disco duro virtual y desarrollar mediante la infraestructura local.</span><span class="sxs-lookup"><span data-stu-id="c4842-105">However, if you must, it is possible toodownload a VHD and develop it by using on-premises infrastructure.</span></span>  

<span data-ttu-id="c4842-106">Para el desarrollo local, debe descargar el sistema de operativo Hola VHD de hello creado máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c4842-106">For on-premises development, you must download hello operating system VHD of hello created VM.</span></span> <span data-ttu-id="c4842-107">Estos pasos tendrán lugar como parte del paso 3.3, arriba.</span><span class="sxs-lookup"><span data-stu-id="c4842-107">These steps would take place as part of step 3.3, above.</span></span>  

## <a name="download-a-vhd-image"></a><span data-ttu-id="c4842-108">Descargar una imagen de disco duro virtual</span><span class="sxs-lookup"><span data-stu-id="c4842-108">Download a VHD image</span></span>
### <a name="locate-a-blob-url"></a><span data-ttu-id="c4842-109">Búsqueda de la dirección URL de blob</span><span class="sxs-lookup"><span data-stu-id="c4842-109">Locate a blob URL</span></span>
<span data-ttu-id="c4842-110">Hola toodownload de orden VHD, buscar dirección URL de blob de hello para el disco del sistema operativo de Hola.</span><span class="sxs-lookup"><span data-stu-id="c4842-110">In order toodownload hello VHD, first locate hello blob URL for hello operating system disk.</span></span>

<span data-ttu-id="c4842-111">Buscar la dirección URL de blob de Hola de hello nueva [portal de Microsoft Azure](https://portal.azure.com):</span><span class="sxs-lookup"><span data-stu-id="c4842-111">Locate hello blob URL from hello new [Microsoft Azure portal](https://portal.azure.com):</span></span>

1. <span data-ttu-id="c4842-112">Vaya demasiado**examinar** > **máquinas virtuales**, y, a continuación, seleccione Hola implementa VM.</span><span class="sxs-lookup"><span data-stu-id="c4842-112">Go too**Browse** > **VMs**, and then select hello deployed VM.</span></span>
2. <span data-ttu-id="c4842-113">En **configurar**, seleccione hello **discos** icono, que abre una hoja de discos de Hola.</span><span class="sxs-lookup"><span data-stu-id="c4842-113">Under **Configure**, select hello **Disks** tile, which opens hello Disks blade.</span></span>
   
   ![dibujo](media/marketplace-publishing-vm-image-creation-on-premise/img01.png)
3. <span data-ttu-id="c4842-115">Seleccione hello **disco del sistema operativo**, que abre otra hoja que se muestra las propiedades de disco, incluida la ubicación del VHD Hola.</span><span class="sxs-lookup"><span data-stu-id="c4842-115">Select hello **OS Disk**, which opens another blade that displays disk properties, including hello VHD location.</span></span>
4. <span data-ttu-id="c4842-116">Copie esta dirección URL de blob.</span><span class="sxs-lookup"><span data-stu-id="c4842-116">Copy this blob URL.</span></span>
   
   ![dibujo](media/marketplace-publishing-vm-image-creation-on-premise/img02.png)
5. <span data-ttu-id="c4842-118">Ahora, eliminar Hola implementa VM sin eliminar los discos de copia de seguridad de Hola.</span><span class="sxs-lookup"><span data-stu-id="c4842-118">Now, delete hello deployed VM without deleting hello backing disks.</span></span> <span data-ttu-id="c4842-119">También puede detener Hola VM en lugar de eliminarlo.</span><span class="sxs-lookup"><span data-stu-id="c4842-119">You can also stop hello VM instead of deleting it.</span></span> <span data-ttu-id="c4842-120">Descargar VHD del sistema operativo hello cuando Hola máquina virtual se está ejecutando.</span><span class="sxs-lookup"><span data-stu-id="c4842-120">Do not download hello operating system VHD when hello VM is running.</span></span>
   
   ![dibujo](media/marketplace-publishing-vm-image-creation-on-premise/img03.png)

### <a name="download-a-vhd"></a><span data-ttu-id="c4842-122">Descarga de un disco duro virtual</span><span class="sxs-lookup"><span data-stu-id="c4842-122">Download a VHD</span></span>
<span data-ttu-id="c4842-123">Una vez que sepa Hola URL del blob, puede descargar Hola VHD mediante hello [portal de Azure](http://manage.windowsazure.com/) o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c4842-123">After you know hello blob URL, you can download hello VHD by using hello [Azure portal](http://manage.windowsazure.com/) or PowerShell.</span></span>  

> [!NOTE]
> <span data-ttu-id="c4842-124">En tiempo de saludo de la creación de esta guía, toodownload de funcionalidad de hello un disco duro virtual aún no está presente en el nuevo portal de Microsoft Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="c4842-124">At hello time of this guide’s creation, hello functionality toodownload a VHD is not yet present in hello new Microsoft Azure portal.</span></span>  
> 
> 

<span data-ttu-id="c4842-125">**Descargar Hola VHD del sistema operativo a través de hello actual [portal de Azure](http://manage.windowsazure.com/)**</span><span class="sxs-lookup"><span data-stu-id="c4842-125">**Download hello operating system VHD via hello current [Azure portal](http://manage.windowsazure.com/)**</span></span>

1. <span data-ttu-id="c4842-126">Inicie sesión en toohello portal de Azure si aún no lo ha hecho.</span><span class="sxs-lookup"><span data-stu-id="c4842-126">Sign in toohello Azure portal if you have not done so already.</span></span>
2. <span data-ttu-id="c4842-127">Haga clic en hello **almacenamiento** ficha.</span><span class="sxs-lookup"><span data-stu-id="c4842-127">Click hello **Storage** tab.</span></span>
3. <span data-ttu-id="c4842-128">Seleccione la cuenta de almacenamiento de hello en qué Hola se almacena el disco duro virtual.</span><span class="sxs-lookup"><span data-stu-id="c4842-128">Select hello storage account within which hello VHD is stored.</span></span>
   
   ![dibujo](media/marketplace-publishing-vm-image-creation-on-premise/img04.png)
4. <span data-ttu-id="c4842-130">De este modo se muestran las propiedades de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="c4842-130">This displays storage account properties.</span></span> <span data-ttu-id="c4842-131">Seleccione hello **contenedores** ficha.</span><span class="sxs-lookup"><span data-stu-id="c4842-131">Select hello **Containers** tab.</span></span>
   
   ![dibujo](media/marketplace-publishing-vm-image-creation-on-premise/img05.png)
5. <span data-ttu-id="c4842-133">Seleccionar contenedor de hello en qué Hola se almacena el disco duro virtual.</span><span class="sxs-lookup"><span data-stu-id="c4842-133">Select hello container in which hello VHD is stored.</span></span> <span data-ttu-id="c4842-134">De forma predeterminada, cuando se creó desde el portal de hello, Hola VHD se almacena en un contenedor de discos duros virtuales.</span><span class="sxs-lookup"><span data-stu-id="c4842-134">By default, when created from hello portal, hello VHD is stored in a vhds container.</span></span>
   
   ![dibujo](media/marketplace-publishing-vm-image-creation-on-premise/img06.png)
6. <span data-ttu-id="c4842-136">Seleccione VHD de sistema operativo correcto de hello comparando toohello de dirección URL de hello uno que guardó.</span><span class="sxs-lookup"><span data-stu-id="c4842-136">Select hello correct operating system VHD by comparing hello URL toohello one you saved.</span></span>
7. <span data-ttu-id="c4842-137">Haga clic en **Descargar**.</span><span class="sxs-lookup"><span data-stu-id="c4842-137">Click **Download**.</span></span>
   
   ![dibujo](media/marketplace-publishing-vm-image-creation-on-premise/img07.png)

### <a name="download-a-vhd-by-using-powershell"></a><span data-ttu-id="c4842-139">Descarga de un disco duro virtual mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="c4842-139">Download a VHD by using PowerShell</span></span>
<span data-ttu-id="c4842-140">Además toousing Hola portal de Azure, puede usar hello [Save-AzureVhd](http://msdn.microsoft.com/library/dn495297.aspx) sistema de operativo de cmdlet toodownload Hola VHD.</span><span class="sxs-lookup"><span data-stu-id="c4842-140">In addition toousing hello Azure portal, you can use hello [Save-AzureVhd](http://msdn.microsoft.com/library/dn495297.aspx) cmdlet toodownload hello operating system VHD.</span></span>

        Save-AzureVhd –Source <storageURIOfVhd> `
        -LocalFilePath <diskLocationOnWorkstation> `
        -StorageKey <keyForStorageAccount>
<span data-ttu-id="c4842-141">Por ejemplo, Save-AzureVhd -Source “https://baseimagevm.blob.core.windows.net/vhds/BaseImageVM-6820cq00-BaseImageVM-os-1411003770191.vhd” -LocalFilePath “C:\Users\Administrator\Desktop\baseimagevm.vhd” -StorageKey <String></span><span class="sxs-lookup"><span data-stu-id="c4842-141">For example, Save-AzureVhd -Source “https://baseimagevm.blob.core.windows.net/vhds/BaseImageVM-6820cq00-BaseImageVM-os-1411003770191.vhd” -LocalFilePath “C:\Users\Administrator\Desktop\baseimagevm.vhd” -StorageKey <String></span></span>

> [!NOTE]
> <span data-ttu-id="c4842-142">**Save-AzureVhd** también tiene un **NumberOfThreads** opción que se puede usar tooincrease paralelismo toomake Hola mejor uso del ancho de banda disponible para su descarga Hola.</span><span class="sxs-lookup"><span data-stu-id="c4842-142">**Save-AzureVhd** also has a **NumberOfThreads** option that can be used tooincrease parallelism toomake hello best use of available bandwidth for hello download.</span></span>
> 
> 

## <a name="upload-vhds-tooan-azure-storage-account"></a><span data-ttu-id="c4842-143">Cargar la cuenta de almacenamiento de Azure de tooan de discos duros virtuales</span><span class="sxs-lookup"><span data-stu-id="c4842-143">Upload VHDs tooan Azure storage account</span></span>
<span data-ttu-id="c4842-144">Si prepara los discos duros virtuales locales, deberá tooupload en un almacenamiento de la cuenta en Azure.</span><span class="sxs-lookup"><span data-stu-id="c4842-144">If you prepared your VHDs on-premises, you need tooupload them into a storage account in Azure.</span></span> <span data-ttu-id="c4842-145">Este paso tendrá lugar después de crear su disco duro virtual de forma local, pero antes de obtener la certificación para la imagen de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c4842-145">This step takes place after creating your VHD on-premises but before obtaining certification for your VM image.</span></span>

### <a name="create-a-storage-account-and-container"></a><span data-ttu-id="c4842-146">Creación de una cuenta de almacenamiento y un contenedor</span><span class="sxs-lookup"><span data-stu-id="c4842-146">Create a storage account and container</span></span>
<span data-ttu-id="c4842-147">Se recomienda que los discos duros virtuales se carga en una cuenta de almacenamiento en una región de Estados Unidos de Hola.</span><span class="sxs-lookup"><span data-stu-id="c4842-147">We recommend that VHDs be uploaded into a storage account in a region in hello United States.</span></span> <span data-ttu-id="c4842-148">Todos los discos duros virtuales de un SKU único deben colocarse en un contenedor único dentro de una cuenta de almacenamiento única.</span><span class="sxs-lookup"><span data-stu-id="c4842-148">All VHDs for a single SKU should be placed in a single container within a single storage account.</span></span>

<span data-ttu-id="c4842-149">toocreate una cuenta de almacenamiento, puede usar hello [portal de Microsoft Azure](https://portal.azure.com/), PowerShell, o la herramienta de línea de comandos de Linux Hola.</span><span class="sxs-lookup"><span data-stu-id="c4842-149">toocreate a storage account, you can use hello [Microsoft Azure portal](https://portal.azure.com/), PowerShell, or hello Linux command-line tool.</span></span>  

<span data-ttu-id="c4842-150">**Crear una cuenta de almacenamiento desde el portal de Microsoft Azure Hola**</span><span class="sxs-lookup"><span data-stu-id="c4842-150">**Create a storage account from hello Microsoft Azure portal**</span></span>

1. <span data-ttu-id="c4842-151">Haga clic en **Nuevo**.</span><span class="sxs-lookup"><span data-stu-id="c4842-151">Click **New**.</span></span>
2. <span data-ttu-id="c4842-152">Seleccione **Almacenamiento**.</span><span class="sxs-lookup"><span data-stu-id="c4842-152">Select **Storage**.</span></span>
3. <span data-ttu-id="c4842-153">Rellene el nombre de cuenta de almacenamiento de hello y, a continuación, seleccione una ubicación.</span><span class="sxs-lookup"><span data-stu-id="c4842-153">Fill in hello storage account name, and then select a location.</span></span>
   
   ![dibujo](media/marketplace-publishing-vm-image-creation-on-premise/img08.png)
4. <span data-ttu-id="c4842-155">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="c4842-155">Click **Create**.</span></span>
5. <span data-ttu-id="c4842-156">hoja de Hola para hello creado la cuenta de almacenamiento debe estar abierto.</span><span class="sxs-lookup"><span data-stu-id="c4842-156">hello blade for hello created storage account should be open.</span></span> <span data-ttu-id="c4842-157">Si no es así, seleccione **Examinar** > **Cuentas de almacenamiento**.</span><span class="sxs-lookup"><span data-stu-id="c4842-157">If not, select **Browse** > **Storage Accounts**.</span></span> <span data-ttu-id="c4842-158">En hello almacenamiento cuenta de hoja, seleccione la cuenta de almacenamiento de hello creada.</span><span class="sxs-lookup"><span data-stu-id="c4842-158">On hello Storage account blade, select hello storage account created.</span></span>
6. <span data-ttu-id="c4842-159">Seleccione **Contenedores**.</span><span class="sxs-lookup"><span data-stu-id="c4842-159">Select **Containers**.</span></span>
   
   ![dibujo](media/marketplace-publishing-vm-image-creation-on-premise/img09.png) 
7. <span data-ttu-id="c4842-161">En la hoja de contenedores de hello, seleccione **agregar**y, a continuación, escriba un permisos del contenedor de hello y nombre de contenedor.</span><span class="sxs-lookup"><span data-stu-id="c4842-161">On hello Containers blade, select **Add**, and then enter a container name and hello container permissions.</span></span> <span data-ttu-id="c4842-162">Seleccione **Privado** para los permisos del contenedor.</span><span class="sxs-lookup"><span data-stu-id="c4842-162">Select **Private** for container permissions.</span></span>

> [!TIP]
> <span data-ttu-id="c4842-163">Le recomendamos que cree un contenedor por SKU que tiene previsto toopublish.</span><span class="sxs-lookup"><span data-stu-id="c4842-163">We recommend that you create one container per SKU that you are planning toopublish.</span></span>
> 
> 

  ![dibujo](media/marketplace-publishing-vm-image-creation-on-premise/img10.png)

### <a name="create-a-storage-account-by-using-powershell"></a><span data-ttu-id="c4842-165">Creación de una cuenta de almacenamiento mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="c4842-165">Create a storage account by using PowerShell</span></span>
<span data-ttu-id="c4842-166">Uso de PowerShell, crear una cuenta de almacenamiento mediante el uso de hello [AzureStorageAccount New](http://msdn.microsoft.com/library/dn495115.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c4842-166">Using PowerShell, create a storage account by using hello [New-AzureStorageAccount](http://msdn.microsoft.com/library/dn495115.aspx) cmdlet.</span></span>

        New-AzureStorageAccount -StorageAccountName “mystorageaccount” -Location “West US”

<span data-ttu-id="c4842-167">A continuación, puede crear un contenedor dentro de esa cuenta de almacenamiento mediante hello [NewAzureStorageContainer](http://msdn.microsoft.com/library/dn495291.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c4842-167">Then you can create a container within that storage account by using hello [NewAzureStorageContainer](http://msdn.microsoft.com/library/dn495291.aspx) cmdlet.</span></span>

        New-AzureStorageContainer -Name “containername” -Permission “Off”

> [!NOTE]
> <span data-ttu-id="c4842-168">Estos comandos dan por hecho que ese contexto de cuenta de almacenamiento actual de hello ya se ha establecido en PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c4842-168">Those commands assume that hello current storage account context has already been set in PowerShell.</span></span>   <span data-ttu-id="c4842-169">Consulte demasiado[configurar Azure PowerShell](marketplace-publishing-powershell-setup.md) para obtener más detalles sobre el programa de instalación de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c4842-169">Refer too[Setting up Azure PowerShell](marketplace-publishing-powershell-setup.md) for more details on PowerShell setup.</span></span>  
> 
> ### <a name="create-a-storage-account-by-using-hello-command-line-tool-for-mac-and-linux"></a><span data-ttu-id="c4842-170">Crear una cuenta de almacenamiento mediante la herramienta de línea de comandos de Hola para Mac y Linux</span><span class="sxs-lookup"><span data-stu-id="c4842-170">Create a storage account by using hello command-line tool for Mac and Linux</span></span>
> <span data-ttu-id="c4842-171">En la [Herramienta de línea de comandos de Linux](../virtual-machines/linux/cli-manage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), cree una cuenta de almacenamiento de la manera siguiente.</span><span class="sxs-lookup"><span data-stu-id="c4842-171">From [Linux command-line tool](../virtual-machines/linux/cli-manage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), create a storage account as follows.</span></span>
> 
> 

        azure storage account create mystorageaccount --location "West US"

<span data-ttu-id="c4842-172">Cree un contenedor de la manera siguiente.</span><span class="sxs-lookup"><span data-stu-id="c4842-172">Create a container as follows.</span></span>

        azure storage container create containername --account-name mystorageaccount --accountkey <accountKey>

## <a name="upload-a-vhd"></a><span data-ttu-id="c4842-173">Carga de un disco duro virtual</span><span class="sxs-lookup"><span data-stu-id="c4842-173">Upload a VHD</span></span>
<span data-ttu-id="c4842-174">Después de crean cuenta de almacenamiento de Hola y de contenedor, puede cargar el VHD preparada.</span><span class="sxs-lookup"><span data-stu-id="c4842-174">After hello storage account and container are created, you can upload your prepared VHDs.</span></span> <span data-ttu-id="c4842-175">Puede usar otras herramientas de administración de almacenamiento de Azure, herramienta de línea de comandos de Linux de Hola o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c4842-175">You can use PowerShell, hello Linux command-line tool, or other Azure Storage management tools.</span></span>

### <a name="upload-a-vhd-via-powershell"></a><span data-ttu-id="c4842-176">Cargar un disco duro virtual a través de PowerShell</span><span class="sxs-lookup"><span data-stu-id="c4842-176">Upload a VHD via PowerShell</span></span>
<span data-ttu-id="c4842-177">Hola de uso [Add-AzureVhd](http://msdn.microsoft.com/library/dn495173.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c4842-177">Use hello [Add-AzureVhd](http://msdn.microsoft.com/library/dn495173.aspx) cmdlet.</span></span>

        Add-AzureVhd –Destination “http://mystorageaccount.blob.core.windows.net/containername/vmsku.vhd” -LocalFilePath “C:\Users\Administrator\Desktop\vmsku.vhd”

### <a name="upload-a-vhd-by-using-hello-command-line-tool-for-mac-and-linux"></a><span data-ttu-id="c4842-178">Cargar un disco duro virtual mediante la herramienta de línea de comandos de Hola para Mac y Linux</span><span class="sxs-lookup"><span data-stu-id="c4842-178">Upload a VHD by using hello command-line tool for Mac and Linux</span></span>
<span data-ttu-id="c4842-179">Con hello [herramienta de línea de comandos de Linux](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2), utilice Hola siguiente: crear la imagen de máquina virtual de azure <image name> --ubicación <Location of hello data center> --sistema operativo Linux<LocationOfLocalVHD></span><span class="sxs-lookup"><span data-stu-id="c4842-179">With hello [Linux command-line tool](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2), use hello following: azure vm image create <image name> --location <Location of hello data center> --OS Linux <LocationOfLocalVHD></span></span>

## <a name="see-also"></a><span data-ttu-id="c4842-180">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="c4842-180">See also</span></span>
* [<span data-ttu-id="c4842-181">Crear una imagen de máquina virtual para hello Marketplace</span><span class="sxs-lookup"><span data-stu-id="c4842-181">Creating a virtual machine image for hello Marketplace</span></span>](marketplace-publishing-vm-image-creation.md)
* [<span data-ttu-id="c4842-182">Configuración de Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="c4842-182">Setting up Azure PowerShell</span></span>](marketplace-publishing-powershell-setup.md)

