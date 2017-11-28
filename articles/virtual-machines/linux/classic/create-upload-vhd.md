---
title: aaaCreate y cargar un VHD Linux tooAzure | Documentos de Microsoft
description: "Crear y cargar un Azure disco duro virtual (VHD) que contiene el sistema de operativo Linux Hola con modelo de implementación clásica de Hola"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 8058ff98-db03-4309-9bf4-69842bd64dd4
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 11/28/2016
ms.author: iainfou
ms.openlocfilehash: 77b01316386c4a6eb68c129fa68d42f0a8996edc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="creating-and-uploading-a-virtual-hard-disk-that-contains-hello-linux-operating-system"></a><span data-ttu-id="3bd06-103">Crear y cargar un disco duro Virtual que contiene Hola sistema operativo Linux</span><span class="sxs-lookup"><span data-stu-id="3bd06-103">Creating and Uploading a Virtual Hard Disk that Contains hello Linux Operating System</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="3bd06-104">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="3bd06-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="3bd06-105">Este artículo tratan con modelo de implementación de hello clásico.</span><span class="sxs-lookup"><span data-stu-id="3bd06-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="3bd06-106">Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="3bd06-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="3bd06-107">También puede [cargar una imagen de disco personalizada mediante Azure Resource Manager](../upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3bd06-107">You can also [upload a custom disk image using Azure Resource Manager](../upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="3bd06-108">Este artículo muestra cómo toocreate y cargar un disco duro virtual (VHD), por lo que puede usar como su propia imagen toocreate las máquinas virtuales en Azure.</span><span class="sxs-lookup"><span data-stu-id="3bd06-108">This article shows you how toocreate and upload a virtual hard disk (VHD) so you can use it as your own image toocreate virtual machines in Azure.</span></span> <span data-ttu-id="3bd06-109">Obtenga información acerca de cómo tooprepare sistema de operativo Hola por lo que puede usar toocreate varias máquinas virtuales basado en dicha imagen.</span><span class="sxs-lookup"><span data-stu-id="3bd06-109">Learn how tooprepare hello operating system so you can use it toocreate multiple virtual machines based on that image.</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="3bd06-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="3bd06-110">Prerequisites</span></span>
<span data-ttu-id="3bd06-111">Este artículo se supone que dispone de hello siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="3bd06-111">This article assumes that you have hello following items:</span></span>

* <span data-ttu-id="3bd06-112">**Sistema operativo Linux instalado en un archivo .vhd** -ha instalado un [distribución de Linux están aprobados Azure](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (o consulte [información para las distribuciones no aprobadas](../create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa de disco virtual en formato de disco duro virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="3bd06-112">**Linux operating system installed in a .vhd file** - You have installed an [Azure-endorsed Linux distribution](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (or see [information for non-endorsed distributions](../create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa virtual disk in hello VHD format.</span></span> <span data-ttu-id="3bd06-113">Varias herramientas existen toocreate una máquina virtual y el disco duro virtual:</span><span class="sxs-lookup"><span data-stu-id="3bd06-113">Multiple tools exist toocreate a VM and VHD:</span></span>
  * <span data-ttu-id="3bd06-114">Instalar y configurar [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) o [KVM](http://www.linux-kvm.org/page/RunningKVM), teniendo cuidado de toouse del disco duro virtual como el formato de imagen.</span><span class="sxs-lookup"><span data-stu-id="3bd06-114">Install and configure [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) or [KVM](http://www.linux-kvm.org/page/RunningKVM), taking care toouse VHD as your image format.</span></span> <span data-ttu-id="3bd06-115">Si es necesario, puede [convertir una imagen](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) con `qemu-img convert`.</span><span class="sxs-lookup"><span data-stu-id="3bd06-115">If needed, you can [convert an image](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) using `qemu-img convert`.</span></span>
  * <span data-ttu-id="3bd06-116">También puede usar Hyper-V [en Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) o [en Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="3bd06-116">You can also use Hyper-V [on Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) or [on Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="3bd06-117">no se admite el formato VHDX más reciente de Hello en Azure.</span><span class="sxs-lookup"><span data-stu-id="3bd06-117">hello newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="3bd06-118">Cuando se crea una máquina virtual, especifique VHD como formato de Hola.</span><span class="sxs-lookup"><span data-stu-id="3bd06-118">When you create a VM, specify VHD as hello format.</span></span> <span data-ttu-id="3bd06-119">Si es necesario, se puede convertir VHDX discos tooVHD con [ `qemu-img convert` ](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) o hello [ `Convert-VHD` ](https://technet.microsoft.com/library/hh848454.aspx) cmdlet de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3bd06-119">If needed, you can convert VHDX disks tooVHD using [`qemu-img convert`](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) or hello [`Convert-VHD`](https://technet.microsoft.com/library/hh848454.aspx) PowerShell cmdlet.</span></span> <span data-ttu-id="3bd06-120">Además, Azure no permite cargar discos duros virtuales dinámicos, por lo que necesita tooconvert tal toostatic discos VHD antes de cargar.</span><span class="sxs-lookup"><span data-stu-id="3bd06-120">Further, Azure does not support uploading dynamic VHDs, so you need tooconvert such disks toostatic VHDs before uploading.</span></span> <span data-ttu-id="3bd06-121">Puede usar herramientas como [utilidades de disco duro virtual de Azure para ir](https://github.com/Microsoft/azure-vhd-utils-for-go) tooconvert discos dinámicos durante el proceso de Hola de carga tooAzure.</span><span class="sxs-lookup"><span data-stu-id="3bd06-121">You can use tools such as [Azure VHD Utilities for GO](https://github.com/Microsoft/azure-vhd-utils-for-go) tooconvert dynamic disks during hello process of uploading tooAzure.</span></span>

* <span data-ttu-id="3bd06-122">**Interfaz de línea de comandos de Azure** -Hola de instalación más reciente [interfaz de línea de comandos de Azure](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) hello tooupload disco duro virtual.</span><span class="sxs-lookup"><span data-stu-id="3bd06-122">**Azure Command-line Interface** - Install hello latest [Azure Command-Line Interface](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) tooupload hello VHD.</span></span>

<span data-ttu-id="3bd06-123"><a id="prepimage"></a></span><span class="sxs-lookup"><span data-stu-id="3bd06-123"><a id="prepimage"> </a></span></span>

## <a name="step-1-prepare-hello-image-toobe-uploaded"></a><span data-ttu-id="3bd06-124">Paso 1: Preparar Hola imagen toobe cargado</span><span class="sxs-lookup"><span data-stu-id="3bd06-124">Step 1: Prepare hello image toobe uploaded</span></span>
<span data-ttu-id="3bd06-125">Azure admite varias distribuciones Linux (consulte [Distribuciones aprobadas](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span><span class="sxs-lookup"><span data-stu-id="3bd06-125">Azure supports various Linux distributions (see [Endorsed Distributions](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span></span> <span data-ttu-id="3bd06-126">Hola siguientes artículos le guiarán por cómo tooprepare Hola diversas distribuciones de Linux que se admiten en Azure.</span><span class="sxs-lookup"><span data-stu-id="3bd06-126">hello following articles guide you through how tooprepare hello various Linux distributions that are supported on Azure.</span></span> <span data-ttu-id="3bd06-127">Después de completar los pasos de Hola Hola siguiendo a guías, proceder vuelve aquí una vez que tenga un archivo de disco duro virtual que está listo tooupload tooAzure:</span><span class="sxs-lookup"><span data-stu-id="3bd06-127">After you complete hello steps in hello following guides, come back here once you have a VHD file that is ready tooupload tooAzure:</span></span>

* <span data-ttu-id="3bd06-128">**[Distribuciones basadas en CentOS](../create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="3bd06-128">**[CentOS-based Distributions](../create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="3bd06-129">**[Debian Linux](../debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="3bd06-129">**[Debian Linux](../debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="3bd06-130">**[Oracle Linux](../oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="3bd06-130">**[Oracle Linux](../oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="3bd06-131">**[Red Hat Enterprise Linux](../redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="3bd06-131">**[Red Hat Enterprise Linux](../redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="3bd06-132">**[SLES y openSUSE](../suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="3bd06-132">**[SLES & openSUSE](../suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="3bd06-133">**[Ubuntu](../create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="3bd06-133">**[Ubuntu](../create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="3bd06-134">**[Otras distribuciones no aprobadas](../create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="3bd06-134">**[Other - Non-Endorsed Distributions](../create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>

> [!NOTE]
> <span data-ttu-id="3bd06-135">Hola SLA de la plataforma Windows Azure aplica máquinas toovirtual ejecuta Hola se utiliza sistema operativo solo cuando uno de hello están aprobados distribuciones de Linux con detalles de configuración de hello tal como se especifica en 'Admite versiones' en [Azure-Endorsed distribuciones Linux en ](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3bd06-135">hello Azure platform SLA applies toovirtual machines running hello Linux OS only when one of hello endorsed distributions is used with hello configuration details as specified under 'Supported Versions' in [Linux on Azure-Endorsed Distributions](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="3bd06-136">Todas las distribuciones de Linux en la Galería de imágenes de Azure Hola son refrendadas distribuciones con la configuración necesaria de Hola.</span><span class="sxs-lookup"><span data-stu-id="3bd06-136">All Linux distributions in hello Azure image gallery are endorsed distributions with hello required configuration.</span></span>
> 
> 

<span data-ttu-id="3bd06-137">Consulte también hello  **[notas sobre la instalación de Linux](../create-upload-generic.md#general-linux-installation-notes)**  para obtener más sugerencias sobre cómo preparar imágenes de Linux de Azure.</span><span class="sxs-lookup"><span data-stu-id="3bd06-137">Also see hello **[Linux Installation Notes](../create-upload-generic.md#general-linux-installation-notes)** for more general tips on preparing Linux images for Azure.</span></span>

<span data-ttu-id="3bd06-138"><a id="connect"></a></span><span class="sxs-lookup"><span data-stu-id="3bd06-138"><a id="connect"> </a></span></span>

## <a name="step-2-prepare-hello-connection-tooazure"></a><span data-ttu-id="3bd06-139">Paso 2: Preparar Hola conexión tooAzure</span><span class="sxs-lookup"><span data-stu-id="3bd06-139">Step 2: Prepare hello connection tooAzure</span></span>
<span data-ttu-id="3bd06-140">Asegúrese de que se usa Hola CLI de Azure en el modelo de implementación clásica de hello (`azure config mode asm`), a continuación, inicie sesión en la cuenta de tooyour:</span><span class="sxs-lookup"><span data-stu-id="3bd06-140">Make sure you are using hello Azure CLI in hello classic deployment model (`azure config mode asm`), then log in tooyour account:</span></span>

```azurecli
azure login
```


<span data-ttu-id="3bd06-141"><a id="upload"></a></span><span class="sxs-lookup"><span data-stu-id="3bd06-141"><a id="upload"> </a></span></span>

## <a name="step-3-upload-hello-image-tooazure"></a><span data-ttu-id="3bd06-142">Paso 3: Cargar Hola imagen tooAzure</span><span class="sxs-lookup"><span data-stu-id="3bd06-142">Step 3: Upload hello image tooAzure</span></span>
<span data-ttu-id="3bd06-143">Necesita el archivo de disco duro virtual para una tooupload de cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="3bd06-143">You need a storage account tooupload your VHD file to.</span></span> <span data-ttu-id="3bd06-144">Puede seleccionar una cuenta de almacenamiento existente o [crear una nueva](../../../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="3bd06-144">You can either pick an existing storage account or [create a new one](../../../storage/common/storage-create-storage-account.md).</span></span>

<span data-ttu-id="3bd06-145">Utilizar imagen de hello Azure CLI tooupload hello mediante Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="3bd06-145">Use hello Azure CLI tooupload hello image by using hello following command:</span></span>

```azurecli
azure vm image create <ImageName> `
    --blob-url <BlobStorageURL>/<YourImagesFolder>/<VHDName> `
    --os Linux <PathToVHDFile>
```

<span data-ttu-id="3bd06-146">En el ejemplo de Hola anterior:</span><span class="sxs-lookup"><span data-stu-id="3bd06-146">In hello previous example:</span></span>

* <span data-ttu-id="3bd06-147">**BlobStorageURL** es dirección URL de Hola Hola cuenta de almacenamiento tiene previsto toouse</span><span class="sxs-lookup"><span data-stu-id="3bd06-147">**BlobStorageURL** is hello URL for hello storage account you plan toouse</span></span>
* <span data-ttu-id="3bd06-148">**YourImagesFolder** esté contenedor Hola dentro del almacenamiento de blobs donde desee toostore las imágenes</span><span class="sxs-lookup"><span data-stu-id="3bd06-148">**YourImagesFolder** is hello container within blob storage where you want toostore your images</span></span>
* <span data-ttu-id="3bd06-149">**VHDName** es Hola etiqueta que aparece en el portal tooidentify Hola disco duro.</span><span class="sxs-lookup"><span data-stu-id="3bd06-149">**VHDName** is hello label that appears in portal tooidentify hello virtual hard disk.</span></span>
* <span data-ttu-id="3bd06-150">**PathToVHDFile** es la ruta de acceso completa de Hola y el nombre de archivo .vhd de hello en su equipo.</span><span class="sxs-lookup"><span data-stu-id="3bd06-150">**PathToVHDFile** is hello full path and name of hello .vhd file on your machine.</span></span>

<span data-ttu-id="3bd06-151">Hola siguiente comando muestra un ejemplo completo:</span><span class="sxs-lookup"><span data-stu-id="3bd06-151">hello following command shows a complete example:</span></span>

```azurecli
azure vm image create myImage `
    --blob-url https://mystorage.blob.core.windows.net/vhds/myimage.vhd `
    --os Linux /home/ahmet/myimage.vhd
```

## <a name="step-4-create-a-vm-from-hello-image"></a><span data-ttu-id="3bd06-152">Paso 4: Crear una máquina virtual desde la imagen de Hola</span><span class="sxs-lookup"><span data-stu-id="3bd06-152">Step 4: Create a VM from hello image</span></span>
<span data-ttu-id="3bd06-153">Crear una VM con `azure vm create` Hola igual que una máquina virtual regular.</span><span class="sxs-lookup"><span data-stu-id="3bd06-153">You create a VM using `azure vm create` in hello same way as a regular VM.</span></span> <span data-ttu-id="3bd06-154">Especificar nombre de Hola se le asignó la imagen en el paso anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="3bd06-154">Specify hello name you gave your image in hello previous step.</span></span> <span data-ttu-id="3bd06-155">En el siguiente ejemplo de Hola, usamos hello **myImage** nombre de la imagen en el paso anterior de Hola:</span><span class="sxs-lookup"><span data-stu-id="3bd06-155">In hello following example, we use hello **myImage** image name given in hello previous step:</span></span>

```azurecli
azure vm create --userName ops --password P@ssw0rd! --vm-size Small --ssh `
    --location "West US" "myDeployedVM" myImage
```

<span data-ttu-id="3bd06-156">toocreate sus propias máquinas virtuales, proporcionar su propio nombre de usuario + el contraseña, la ubicación, el nombre DNS y el nombre de la imagen.</span><span class="sxs-lookup"><span data-stu-id="3bd06-156">toocreate your own VMs, provide your own username + password, location, DNS name, and image name.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3bd06-157">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3bd06-157">Next steps</span></span>
<span data-ttu-id="3bd06-158">Para obtener más información, consulte [referencia de CLI de Azure para el modelo de implementación clásica Azure hello](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="3bd06-158">For more information, see [Azure CLI reference for hello Azure classic deployment model](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span>

[Step 1: Prepare hello image toobe uploaded]:#prepimage
[Step 2: Prepare hello connection tooAzure]:#connect
[Step 3: Upload hello image tooAzure]:#upload
