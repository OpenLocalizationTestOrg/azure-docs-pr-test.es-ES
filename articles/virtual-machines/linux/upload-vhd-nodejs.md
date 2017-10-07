---
title: aaaUpload una imagen personalizada de Linux con 1.0 de CLI de Azure | Documentos de Microsoft
description: "Crear y cargar un tooAzure de disco duro virtual (VHD) con una imagen personalizada de Linux con modelo de implementación del Administrador de recursos de Hola y Hola 1.0 de CLI de Azure."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: a8c7818f-eb65-409e-aa91-ce5ae975c564
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 10/10/2016
ms.author: iainfou
ms.openlocfilehash: 0bbd232debee1e632233d1c010e388dbc1548bf3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="upload-and-create-a-linux-vm-from-custom-disk-image-by-using-hello-azure-cli-10"></a><span data-ttu-id="dc5ff-103">Cargar y crear una VM Linux de imagen de disco personalizado mediante el uso de hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="dc5ff-103">Upload and create a Linux VM from custom disk image by using hello Azure CLI 1.0</span></span>
<span data-ttu-id="dc5ff-104">Este artículo muestra cómo tooupload un uso de disco duro virtual (VHD) tooAzure Hola modelo de implementación del Administrador de recursos y crear máquinas virtuales de Linux desde su imagen personalizada.</span><span class="sxs-lookup"><span data-stu-id="dc5ff-104">This article shows you how tooupload a virtual hard disk (VHD) tooAzure using hello Resource Manager deployment model and create Linux VMs from this custom image.</span></span> <span data-ttu-id="dc5ff-105">Esta funcionalidad le permite tooinstall y configurar una distribución de Linux tooyour requisitos y, a continuación, usar ese archivo VHD tooquickly crear máquinas virtuales de Azure (VM).</span><span class="sxs-lookup"><span data-stu-id="dc5ff-105">This functionality allows you tooinstall and configure a Linux distro tooyour requirements and then use that VHD tooquickly create Azure virtual machines (VMs).</span></span>


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="dc5ff-106">Tarea CLI versiones toocomplete hello</span><span class="sxs-lookup"><span data-stu-id="dc5ff-106">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="dc5ff-107">Puede completar la tarea hello mediante uno de hello después de las versiones CLI:</span><span class="sxs-lookup"><span data-stu-id="dc5ff-107">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="dc5ff-108">[Azure 1.0 de CLI](#quick-commands) – nuestro CLI para hello clásico y recursos administración modelos de implementación (en este artículo)</span><span class="sxs-lookup"><span data-stu-id="dc5ff-108">[Azure CLI 1.0](#quick-commands) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="dc5ff-109">[Azure 2.0 CLI](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -nuestro CLI de próxima generación para el modelo de implementación de administración de recursos de Hola</span><span class="sxs-lookup"><span data-stu-id="dc5ff-109">[Azure CLI 2.0](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="dc5ff-110">Comandos rápidos</span><span class="sxs-lookup"><span data-stu-id="dc5ff-110">Quick commands</span></span>
<span data-ttu-id="dc5ff-111">Si necesita tooquickly realizar la tarea hello, Hola después Hola de detalles de la sección base tooupload comandos tooAzure de una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="dc5ff-111">If you need tooquickly accomplish hello task, hello following section details hello base commands tooupload a VM tooAzure.</span></span> <span data-ttu-id="dc5ff-112">Obtener más información y el contexto de cada paso se encuentran rest Hola de documento de hello, [a partir de aquí](#requirements).</span><span class="sxs-lookup"><span data-stu-id="dc5ff-112">More detailed information and context for each step can be found hello rest of hello document, [starting here](#requirements).</span></span>

<span data-ttu-id="dc5ff-113">Asegúrese de que dispone de [hello Azure CLI 1.0](../../cli-install-nodejs.md) iniciado la sesión y utilizar el modo de administrador de recursos:</span><span class="sxs-lookup"><span data-stu-id="dc5ff-113">Make sure that you have [hello Azure CLI 1.0](../../cli-install-nodejs.md) logged in and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="dc5ff-114">En hello en los ejemplos siguientes, reemplace los nombres de parámetros de ejemplo con sus propios valores.</span><span class="sxs-lookup"><span data-stu-id="dc5ff-114">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="dc5ff-115">Nombres de parámetros de ejemplo incluidos `myResourceGroup`, `mystorageaccount` y `myimages`.</span><span class="sxs-lookup"><span data-stu-id="dc5ff-115">Example parameter names included `myResourceGroup`, `mystorageaccount`, and `myimages`.</span></span>

<span data-ttu-id="dc5ff-116">En primer lugar, cree un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="dc5ff-116">First, create a resource group.</span></span> <span data-ttu-id="dc5ff-117">Hello en el ejemplo siguiente se crea un grupo de recursos denominado `myResourceGroup` en hello `WestUs` ubicación:</span><span class="sxs-lookup"><span data-stu-id="dc5ff-117">hello following example creates a resource group named `myResourceGroup` in hello `WestUs` location:</span></span>

```azurecli
azure group create myResourceGroup --location "WestUS"
```

<span data-ttu-id="dc5ff-118">Crear un toohold de cuenta de almacenamiento de los discos virtuales.</span><span class="sxs-lookup"><span data-stu-id="dc5ff-118">Create a storage account toohold your virtual disks.</span></span> <span data-ttu-id="dc5ff-119">Hello en el ejemplo siguiente se crea una cuenta de almacenamiento denominada `mystorageaccount`:</span><span class="sxs-lookup"><span data-stu-id="dc5ff-119">hello following example creates a storage account named `mystorageaccount`:</span></span>

```azurecli
azure storage account create mystorageaccount --resource-group myResourceGroup \
    --location "WestUS" --kind Storage --sku-name PLRS
```

<span data-ttu-id="dc5ff-120">Lista de claves de acceso de hello para la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="dc5ff-120">List hello access keys for your storage account.</span></span> <span data-ttu-id="dc5ff-121">Tome nota de `key1`:</span><span class="sxs-lookup"><span data-stu-id="dc5ff-121">Make a note of `key1`:</span></span>

```azurecli
azure storage account keys list mystorageaccount --resource-group myResourceGroup
```

<span data-ttu-id="dc5ff-122">Crear un contenedor dentro de su cuenta de almacenamiento con la clave de almacenamiento de hello que ha adquirido.</span><span class="sxs-lookup"><span data-stu-id="dc5ff-122">Create a container within your storage account using hello storage key you obtained.</span></span> <span data-ttu-id="dc5ff-123">Hello en el ejemplo siguiente se crea un contenedor denominado `myimages` mediante el valor de clave de almacenamiento de Hola de `key1`:</span><span class="sxs-lookup"><span data-stu-id="dc5ff-123">hello following example creates a container named `myimages` using hello storage key value from `key1`:</span></span>

```azurecli
azure storage container create --account-name mystorageaccount \
    --account-key key1 --container myimages
```

<span data-ttu-id="dc5ff-124">Por último, cargar el contenedor de toohello de disco duro virtual que creó.</span><span class="sxs-lookup"><span data-stu-id="dc5ff-124">Finally, upload your VHD toohello container you created.</span></span> <span data-ttu-id="dc5ff-125">Especificar la ruta de acceso local de hello tooyour VHD en `/path/to/disk/mydisk.vhd`:</span><span class="sxs-lookup"><span data-stu-id="dc5ff-125">Specify hello local path tooyour VHD under `/path/to/disk/mydisk.vhd`:</span></span>

```azurecli
azure storage blob upload --blobtype page --account-name mystorageaccount \
    --account-key key1 --container myimages /path/to/disk/mydisk.vhd
```

<span data-ttu-id="dc5ff-126">Ahora puede crear una máquina virtual desde el disco virtual cargado [mediante plantillas de Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd).</span><span class="sxs-lookup"><span data-stu-id="dc5ff-126">You can now create a VM from your uploaded virtual disk [using a Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd).</span></span> <span data-ttu-id="dc5ff-127">También puede usar Hola CLI mediante la especificación de disco de hello URI tooyour (`--image-urn`).</span><span class="sxs-lookup"><span data-stu-id="dc5ff-127">You can also use hello CLI by specifying hello URI tooyour disk (`--image-urn`).</span></span> <span data-ttu-id="dc5ff-128">Hello en el ejemplo siguiente se crea una máquina virtual denominada `myVM` con disco virtual Hola cargado previamente:</span><span class="sxs-lookup"><span data-stu-id="dc5ff-128">hello following example creates a VM named `myVM` using hello virtual disk previously uploaded:</span></span>

```azurecli
azure vm create myVM -l "WestUS" --resource-group myResourceGroup \
    --image-urn https://mystorageaccount.blob.core.windows.net/myimages/mydisk.vhd
```

<span data-ttu-id="dc5ff-129">cuenta de almacenamiento de destino de Hello tiene toobe Hola igual como donde cargar el disco virtual para.</span><span class="sxs-lookup"><span data-stu-id="dc5ff-129">hello destination storage account has toobe hello same as where you uploaded your virtual disk to.</span></span> <span data-ttu-id="dc5ff-130">También necesita toospecify o responder a peticiones de, todos los parámetros adicionales requeridos por Hola de Hola `azure vm create` comando como la red virtual, la dirección IP pública, nombre de usuario y las claves de SSH.</span><span class="sxs-lookup"><span data-stu-id="dc5ff-130">You also need toospecify, or answer prompts for, all hello additional parameters required by hello `azure vm create` command such as virtual network, public IP address, username, and SSH keys.</span></span> <span data-ttu-id="dc5ff-131">Puede leer más sobre hello [disponibles parámetros del Administrador de recursos de CLI](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).</span><span class="sxs-lookup"><span data-stu-id="dc5ff-131">You can read more about hello [available CLI Resource Manager parameters](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).</span></span>

## <a name="requirements"></a><span data-ttu-id="dc5ff-132">Requisitos</span><span class="sxs-lookup"><span data-stu-id="dc5ff-132">Requirements</span></span>
<span data-ttu-id="dc5ff-133">Hola toocomplete siguiendo los pasos, debe:</span><span class="sxs-lookup"><span data-stu-id="dc5ff-133">toocomplete hello following steps, you need:</span></span>

* <span data-ttu-id="dc5ff-134">**Sistema operativo Linux instalado en un archivo .vhd** -instalar un [distribución de Linux están aprobados Azure](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (o consulte [información para las distribuciones no aprobadas](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa disco virtual en hello VHD formato.</span><span class="sxs-lookup"><span data-stu-id="dc5ff-134">**Linux operating system installed in a .vhd file** - Install an [Azure-endorsed Linux distribution](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (or see [information for non-endorsed distributions](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa virtual disk in hello VHD format.</span></span> <span data-ttu-id="dc5ff-135">Varias herramientas existen toocreate una máquina virtual y el disco duro virtual:</span><span class="sxs-lookup"><span data-stu-id="dc5ff-135">Multiple tools exist toocreate a VM and VHD:</span></span>
  * <span data-ttu-id="dc5ff-136">Instalar y configurar [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) o [KVM](http://www.linux-kvm.org/page/RunningKVM), teniendo cuidado de toouse del disco duro virtual como el formato de imagen.</span><span class="sxs-lookup"><span data-stu-id="dc5ff-136">Install and configure [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) or [KVM](http://www.linux-kvm.org/page/RunningKVM), taking care toouse VHD as your image format.</span></span> <span data-ttu-id="dc5ff-137">Si es necesario, puede [convertir una imagen](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) con `qemu-img convert`.</span><span class="sxs-lookup"><span data-stu-id="dc5ff-137">If needed, you can [convert an image](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) using `qemu-img convert`.</span></span>
  * <span data-ttu-id="dc5ff-138">También puede usar Hyper-V [en Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) o [en Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="dc5ff-138">You can also use Hyper-V [on Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) or [on Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="dc5ff-139">no se admite el formato VHDX más reciente de Hello en Azure.</span><span class="sxs-lookup"><span data-stu-id="dc5ff-139">hello newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="dc5ff-140">Cuando se crea una máquina virtual, especifique VHD como formato de Hola.</span><span class="sxs-lookup"><span data-stu-id="dc5ff-140">When you create a VM, specify VHD as hello format.</span></span> <span data-ttu-id="dc5ff-141">Si es necesario, se puede convertir VHDX discos tooVHD con [ `qemu-img convert` ](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) o hello [ `Convert-VHD` ](https://technet.microsoft.com/library/hh848454.aspx) cmdlet de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="dc5ff-141">If needed, you can convert VHDX disks tooVHD using [`qemu-img convert`](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) or hello [`Convert-VHD`](https://technet.microsoft.com/library/hh848454.aspx) PowerShell cmdlet.</span></span> <span data-ttu-id="dc5ff-142">Además, Azure no permite cargar discos duros virtuales dinámicos, por lo que necesita tooconvert tal toostatic discos VHD antes de cargar.</span><span class="sxs-lookup"><span data-stu-id="dc5ff-142">Further, Azure does not support uploading dynamic VHDs, so you need tooconvert such disks toostatic VHDs before uploading.</span></span> <span data-ttu-id="dc5ff-143">Puede usar herramientas como [utilidades de disco duro virtual de Azure para ir](https://github.com/Microsoft/azure-vhd-utils-for-go) tooconvert discos dinámicos durante el proceso de Hola de carga tooAzure.</span><span class="sxs-lookup"><span data-stu-id="dc5ff-143">You can use tools such as [Azure VHD Utilities for GO](https://github.com/Microsoft/azure-vhd-utils-for-go) tooconvert dynamic disks during hello process of uploading tooAzure.</span></span>
> 
> 

* <span data-ttu-id="dc5ff-144">Creado a partir de la imagen personalizada de las máquinas virtuales deben residir en hello misma cuenta de almacenamiento que la propia imagen de Hola</span><span class="sxs-lookup"><span data-stu-id="dc5ff-144">VMs created from your custom image must reside in hello same storage account as hello image itself</span></span>
  * <span data-ttu-id="dc5ff-145">Crear un toohold de cuenta y el contenedor de almacenamiento tanto la imagen personalizada y crear máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="dc5ff-145">Create a storage account and container toohold both your custom image and created VMs</span></span>
  * <span data-ttu-id="dc5ff-146">Una vez que haya creado todas las máquinas virtuales, puede eliminar su imagen de forma segura.</span><span class="sxs-lookup"><span data-stu-id="dc5ff-146">After you have created all your VMs, you can safely delete your image</span></span>

<span data-ttu-id="dc5ff-147">Asegúrese de que dispone de [hello Azure CLI 1.0](../../cli-install-nodejs.md) iniciado la sesión y utilizar el modo de administrador de recursos:</span><span class="sxs-lookup"><span data-stu-id="dc5ff-147">Make sure that you have [hello Azure CLI 1.0](../../cli-install-nodejs.md) logged in and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="dc5ff-148">En hello en los ejemplos siguientes, reemplace los nombres de parámetros de ejemplo con sus propios valores.</span><span class="sxs-lookup"><span data-stu-id="dc5ff-148">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="dc5ff-149">Nombres de parámetros de ejemplo incluidos `myResourceGroup`, `mystorageaccount` y `myimages`.</span><span class="sxs-lookup"><span data-stu-id="dc5ff-149">Example parameter names included `myResourceGroup`, `mystorageaccount`, and `myimages`.</span></span>

<span data-ttu-id="dc5ff-150"><a id="prepimage"></a></span><span class="sxs-lookup"><span data-stu-id="dc5ff-150"><a id="prepimage"> </a></span></span>

## <a name="prepare-hello-image-toobe-uploaded"></a><span data-ttu-id="dc5ff-151">Preparar Hola imagen toobe cargado</span><span class="sxs-lookup"><span data-stu-id="dc5ff-151">Prepare hello image toobe uploaded</span></span>
<span data-ttu-id="dc5ff-152">Azure admite varias distribuciones Linux (consulte [Distribuciones aprobadas](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span><span class="sxs-lookup"><span data-stu-id="dc5ff-152">Azure supports various Linux distributions (see [Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span></span> <span data-ttu-id="dc5ff-153">Hola siguientes artículos guiarle por cómo tooprepare Hola diversas distribuciones de Linux que se admiten en Azure:</span><span class="sxs-lookup"><span data-stu-id="dc5ff-153">hello following articles guide you through how tooprepare hello various Linux distributions that are supported on Azure:</span></span>

* <span data-ttu-id="dc5ff-154">**[Distribuciones basadas en CentOS](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="dc5ff-154">**[CentOS-based Distributions](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="dc5ff-155">**[Debian Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="dc5ff-155">**[Debian Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="dc5ff-156">**[Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="dc5ff-156">**[Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="dc5ff-157">**[Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="dc5ff-157">**[Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="dc5ff-158">**[SLES y openSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="dc5ff-158">**[SLES & openSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="dc5ff-159">**[Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="dc5ff-159">**[Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="dc5ff-160">**[Otras distribuciones no aprobadas](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="dc5ff-160">**[Other - Non-Endorsed Distributions](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>

<span data-ttu-id="dc5ff-161">Consulte también hello  **[notas sobre la instalación de Linux](create-upload-generic.md#general-linux-installation-notes)**  para obtener más sugerencias sobre cómo preparar imágenes de Linux de Azure.</span><span class="sxs-lookup"><span data-stu-id="dc5ff-161">Also see hello **[Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes)** for more general tips on preparing Linux images for Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="dc5ff-162">Hola [plataforma Windows Azure SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/) aplica tooVMs ejecutando Linux sólo cuando uno de hello están aprobados distribuciones se utilizan con los detalles de configuración de hello tal como se especifica en 'Admite versiones' en [Linux en Azure aprobadas Distribuciones](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="dc5ff-162">hello [Azure platform SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/) applies tooVMs running Linux only when one of hello endorsed distributions is used with hello configuration details as specified under 'Supported Versions' in [Linux on Azure-Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


## <a name="create-a-resource-group"></a><span data-ttu-id="dc5ff-163">Crear un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="dc5ff-163">Create a resource group</span></span>
<span data-ttu-id="dc5ff-164">Grupos de recursos lógicamente reunir todos los toosupport de recursos de Azure de hello las máquinas virtuales, como una red virtual Hola y el almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="dc5ff-164">Resource groups logically bring together all hello Azure resources toosupport your virtual machines, such as hello virtual networking and storage.</span></span> <span data-ttu-id="dc5ff-165">Lea más sobre [grupos de recursos de Azure aquí](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="dc5ff-165">Read more about [Azure resource groups here](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="dc5ff-166">Antes de cargar la imagen de disco personalizado y crear máquinas virtuales, primero debe toocreate un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="dc5ff-166">Before uploading your custom disk image and creating VMs, you first need toocreate a resource group.</span></span> 

<span data-ttu-id="dc5ff-167">Hello en el ejemplo siguiente se crea un grupo de recursos denominado `myResourceGroup` en hello `WestUS` ubicación:</span><span class="sxs-lookup"><span data-stu-id="dc5ff-167">hello following example creates a resource group named `myResourceGroup` in hello `WestUS` location:</span></span>

```azurecli
azure group create myResourceGroup --location "WestUS"
```

## <a name="create-a-storage-account"></a><span data-ttu-id="dc5ff-168">Crear una cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="dc5ff-168">Create a storage account</span></span>
<span data-ttu-id="dc5ff-169">Las máquinas virtuales se almacenan como blobs en páginas dentro de una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="dc5ff-169">VMs are stored as page blobs within a storage account.</span></span> <span data-ttu-id="dc5ff-170">Lea más sobre [almacenamiento de blobs de Azure aquí](../../storage/common/storage-introduction.md#blob-storage).</span><span class="sxs-lookup"><span data-stu-id="dc5ff-170">Read more about [Azure blob storage here](../../storage/common/storage-introduction.md#blob-storage).</span></span> <span data-ttu-id="dc5ff-171">Creará una cuenta de almacenamiento para la imagen de disco personalizada y las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="dc5ff-171">You create a storage account for your custom disk image and VMs.</span></span> <span data-ttu-id="dc5ff-172">Todas las máquinas virtuales que se crean desde su toobe de necesidad de imagen de disco personalizado en hello la misma cuenta de almacenamiento que esa imagen.</span><span class="sxs-lookup"><span data-stu-id="dc5ff-172">Any VMs that you create from your custom disk image need toobe in hello same storage account as that image.</span></span>

<span data-ttu-id="dc5ff-173">Hello en el ejemplo siguiente se crea una cuenta de almacenamiento denominada `mystorageaccount` en grupo de recursos de hello creado anteriormente:</span><span class="sxs-lookup"><span data-stu-id="dc5ff-173">hello following example creates a storage account named `mystorageaccount` in hello resource group previously created:</span></span>

```azurecli
azure storage account create mystorageaccount --resource-group myResourceGroup \
    --location "WestUS" --kind Storage --sku-name PLRS
```

## <a name="list-storage-account-keys"></a><span data-ttu-id="dc5ff-174">Enumerar claves de cuentas de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="dc5ff-174">List storage account keys</span></span>
<span data-ttu-id="dc5ff-175">Azure genera dos claves de acceso de 512 bits para cada cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="dc5ff-175">Azure generates two 512-bit access keys for each storage account.</span></span> <span data-ttu-id="dc5ff-176">Estas teclas de acceso se utilizan para autenticar la cuenta de almacenamiento de toohello, como toocarry operaciones de escritura de salida.</span><span class="sxs-lookup"><span data-stu-id="dc5ff-176">These access keys are used when authenticating toohello storage account, such as toocarry out write operations.</span></span> <span data-ttu-id="dc5ff-177">Obtenga más información sobre [administrar acceso toostorage aquí](../../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="dc5ff-177">Read more about [managing access toostorage here](../../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span> <span data-ttu-id="dc5ff-178">Puede ver las teclas de acceso con hello `azure storage account keys list` comando.</span><span class="sxs-lookup"><span data-stu-id="dc5ff-178">You can view access keys with hello `azure storage account keys list` command.</span></span>

<span data-ttu-id="dc5ff-179">Ver las teclas de acceso de Hola Hola cuenta de almacenamiento que creó:</span><span class="sxs-lookup"><span data-stu-id="dc5ff-179">View hello access keys for hello storage account you created:</span></span>

```azurecli
azure storage account keys list mystorageaccount --resource-group myResourceGroup
```

<span data-ttu-id="dc5ff-180">es similar a la salida de Hello:</span><span class="sxs-lookup"><span data-stu-id="dc5ff-180">hello output is similar to:</span></span>

```azurecli
info:    Executing command storage account keys list
+ Getting storage account keys
data:    Name  Key                                                                                       Permissions
data:    ----  ----------------------------------------------------------------------------------------  -----------
data:    key1  d4XAvZzlGAgWdvhlWfkZ9q4k9bYZkXkuPCJ15NTsQOeDeowCDAdB80r9zA/tUINApdSGQ94H9zkszYyxpe8erw==  Full
data:    key2  Ww0T7g4UyYLaBnLYcxIOTVziGAAHvU+wpwuPvK4ZG0CDFwu/mAxS/YYvAQGHocq1w7/3HcalbnfxtFdqoXOw8g==  Full
info:    storage account keys list command OK

```
<span data-ttu-id="dc5ff-181">Tome nota del `key1` tal y como se va a utilizar se toointeract con su cuenta de almacenamiento en los pasos siguientes de Hola.</span><span class="sxs-lookup"><span data-stu-id="dc5ff-181">Make a note of `key1` as you will use it toointeract with your storage account in hello next steps.</span></span>

## <a name="create-a-storage-container"></a><span data-ttu-id="dc5ff-182">Creación de un contenedor de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="dc5ff-182">Create a storage container</span></span>
<span data-ttu-id="dc5ff-183">Hola igual que crear directorios distintos toologically organizar el sistema de archivos local, crear contenedores dentro de un tooorganize de cuenta de almacenamiento, las imágenes y discos virtuales.</span><span class="sxs-lookup"><span data-stu-id="dc5ff-183">In hello same way that you create different directories toologically organize your local file system, you create containers within a storage account tooorganize your virtual disks and images.</span></span> <span data-ttu-id="dc5ff-184">Una cuenta de almacenamiento puede contener un número cualquiera de contenedores.</span><span class="sxs-lookup"><span data-stu-id="dc5ff-184">A storage account can contain any number of containers.</span></span> 

<span data-ttu-id="dc5ff-185">Hello en el ejemplo siguiente se crea un contenedor denominado `myimages`, especificar la clave de acceso de hello obtenido en el paso anterior de hello (`key1`):</span><span class="sxs-lookup"><span data-stu-id="dc5ff-185">hello following example creates a container named `myimages`, specifying hello access key obtained in hello previous step (`key1`):</span></span>

```azurecli
azure storage container create --account-name mystorageaccount \
    --account-key key1 --container myimages
```

## <a name="upload-vhd"></a><span data-ttu-id="dc5ff-186">Carga de VHD</span><span class="sxs-lookup"><span data-stu-id="dc5ff-186">Upload VHD</span></span>
<span data-ttu-id="dc5ff-187">Ahora, en realidad, puede cargar la imagen de disco personalizada.</span><span class="sxs-lookup"><span data-stu-id="dc5ff-187">Now you can actually upload your custom disk image.</span></span> <span data-ttu-id="dc5ff-188">Al igual que con todos los discos virtuales usados por las máquinas virtuales, cargará y almacenará la imagen de disco personalizada como un blob en páginas.</span><span class="sxs-lookup"><span data-stu-id="dc5ff-188">As with all virtual disks used by VMs, you upload and store your custom disk image as a page blob.</span></span>

<span data-ttu-id="dc5ff-189">Especifique la clave de acceso, el contenedor de Hola que creó en el paso anterior de Hola y Hola, a continuación, la imagen de disco personalizada toohello de ruta de acceso en el equipo local:</span><span class="sxs-lookup"><span data-stu-id="dc5ff-189">Specify your access key, hello container you created in hello previous step, and then hello path toohello custom disk image on your local computer:</span></span>

```azurecli
azure storage blob upload --blobtype page --account-name mystorageaccount \
    --account-key key1 --container myimages /path/to/disk/mydisk.vhd
```

## <a name="create-vm-from-custom-image"></a><span data-ttu-id="dc5ff-190">Creación de una máquina virtual a partir de una imagen personalizada</span><span class="sxs-lookup"><span data-stu-id="dc5ff-190">Create VM from custom image</span></span>
<span data-ttu-id="dc5ff-191">Al crear máquinas virtuales desde su imagen de disco personalizado, especifique la imagen de disco de toohello URI de Hola.</span><span class="sxs-lookup"><span data-stu-id="dc5ff-191">When you create VMs from your custom disk image, specify hello URI toohello disk image.</span></span> <span data-ttu-id="dc5ff-192">Asegúrese de que Hola coincidencias de cuenta de almacenamiento de destino donde se almacena la imagen de disco personalizada.</span><span class="sxs-lookup"><span data-stu-id="dc5ff-192">Ensure that hello destination storage account matches where your custom disk image is stored.</span></span> <span data-ttu-id="dc5ff-193">Puede crear la máquina virtual con la plantilla de CLI de Azure o el Administrador de recursos JSON Hola.</span><span class="sxs-lookup"><span data-stu-id="dc5ff-193">You can create your VM using hello Azure CLI or Resource Manager JSON template.</span></span>

### <a name="create-a-vm-using-hello-azure-cli"></a><span data-ttu-id="dc5ff-194">Crear una máquina virtual mediante Hola CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="dc5ff-194">Create a VM using hello Azure CLI</span></span>
<span data-ttu-id="dc5ff-195">Especificar hello `--image-urn` parámetro con hello `azure vm create` imagen de disco personalizada de comando toopoint tooyour.</span><span class="sxs-lookup"><span data-stu-id="dc5ff-195">You specify hello `--image-urn` parameter with hello `azure vm create` command toopoint tooyour custom disk image.</span></span> <span data-ttu-id="dc5ff-196">Asegúrese de que `--storage-account-name` coincidencias Hola cuenta de almacenamiento donde se almacena la imagen de disco personalizada.</span><span class="sxs-lookup"><span data-stu-id="dc5ff-196">Ensure that `--storage-account-name` matches hello storage account where your custom disk image is stored.</span></span> <span data-ttu-id="dc5ff-197">No es necesario toouse Hola mismo contenedor como Hola toostore de imagen de disco personalizada las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="dc5ff-197">You do not have toouse hello same container as hello custom disk image toostore your VMs.</span></span> <span data-ttu-id="dc5ff-198">Realizar toocreate seguro de los contenedores adicionales en hello misma manera que Hola pasos anteriores antes de cargar las imágenes de disco personalizadas.</span><span class="sxs-lookup"><span data-stu-id="dc5ff-198">Make sure toocreate any additional containers in hello same way as hello earlier steps before uploading your custom disk images.</span></span>

<span data-ttu-id="dc5ff-199">Hello en el ejemplo siguiente se crea una máquina virtual denominada `myVM` desde la imagen de disco personalizado:</span><span class="sxs-lookup"><span data-stu-id="dc5ff-199">hello following example creates a VM named `myVM` from your custom disk image:</span></span>

```azurecli
azure vm create myVM -l "WestUS" --resource-group myResourceGroup \
    --image-urn https://mystorageaccount.blob.core.windows.net/myimages/mydisk.vhd
    --storage-account-name mystorageaccount
```

<span data-ttu-id="dc5ff-200">Todavía necesita toospecify o responder a peticiones de, todos los parámetros adicionales requeridos por Hola de Hola `azure vm create` comando como la red virtual, la dirección IP pública, nombre de usuario y las claves de SSH.</span><span class="sxs-lookup"><span data-stu-id="dc5ff-200">You still need toospecify, or answer prompts for, all hello additional parameters required by hello `azure vm create` command such as virtual network, public IP address, username, and SSH keys.</span></span> <span data-ttu-id="dc5ff-201">Obtener más información acerca de hello [disponibles parámetros del Administrador de recursos de CLI](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).</span><span class="sxs-lookup"><span data-stu-id="dc5ff-201">Read more about hello [available CLI Resource Manager parameters](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).</span></span>

### <a name="create-a-vm-using-a-json-template"></a><span data-ttu-id="dc5ff-202">Creación de una máquina virtual con una plantilla JSON</span><span class="sxs-lookup"><span data-stu-id="dc5ff-202">Create a VM using a JSON template</span></span>
<span data-ttu-id="dc5ff-203">Plantillas de administrador de recursos de Azure son archivos de JavaScript Object Notation (JSON) que definen el entorno de hello desea toobuild.</span><span class="sxs-lookup"><span data-stu-id="dc5ff-203">Azure Resource Manager templates are JavaScript Object Notation (JSON) files that define hello environment you wish toobuild.</span></span> <span data-ttu-id="dc5ff-204">plantillas de Hola se desglosan en proveedores de recursos de toodifferent como compute o red.</span><span class="sxs-lookup"><span data-stu-id="dc5ff-204">hello templates are broken down in toodifferent resource providers such as compute or network.</span></span> <span data-ttu-id="dc5ff-205">Puede usar las plantillas existentes o escribir las suyas propias.</span><span class="sxs-lookup"><span data-stu-id="dc5ff-205">You can use existing templates or write your own.</span></span> <span data-ttu-id="dc5ff-206">Lea más sobre el [uso de Resource Manager y las plantillas](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="dc5ff-206">Read more about [using Resource Manager and templates](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="dc5ff-207">Dentro de hello `Microsoft.Compute/virtualMachines` proveedor de la plantilla, tendrá un `storageProfile` nodo que contiene los detalles de configuración de hello para la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="dc5ff-207">Within hello `Microsoft.Compute/virtualMachines` provider of your template, you have a `storageProfile` node that contains hello configuration details for your VM.</span></span> <span data-ttu-id="dc5ff-208">Hola dos parámetros principales tooedit son hello `image` y `vhd` URI que señalan a imágenes de disco personalizadas tooyour y disco virtual de la máquina virtual nueva.</span><span class="sxs-lookup"><span data-stu-id="dc5ff-208">hello two main parameters tooedit are hello `image` and `vhd` URIs that point tooyour custom disk image and your new VM's virtual disk.</span></span> <span data-ttu-id="dc5ff-209">siguiente Hello muestra un ejemplo de Hola JSON para el uso de una imagen de disco personalizado:</span><span class="sxs-lookup"><span data-stu-id="dc5ff-209">hello following shows an example of hello JSON for using a custom disk image:</span></span>

```json
"storageProfile": {
          "osDisk": {
            "name": "myVM",
            "osType": "Linux",
            "caching": "ReadWrite",
            "createOption": "FromImage",
            "image": {
              "uri": "https://mystorageaccount.blob.core.windows.net/myimages/mydisk.vhd"
            },
            "vhd": {
              "uri": "https://mystorageaccount.blob.core.windows.net/vhds/newvmname.vhd"
            }
          }
```

<span data-ttu-id="dc5ff-210">Puede usar [esta toocreate de plantilla existente una máquina virtual desde una imagen personalizada](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) o leer acerca de [crear sus propias plantillas de Azure Resource Manager](../../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="dc5ff-210">You can use [this existing template toocreate a VM from a custom image](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) or read about [creating your own Azure Resource Manager templates](../../azure-resource-manager/resource-group-authoring-templates.md).</span></span> 

<span data-ttu-id="dc5ff-211">Una vez que tenga una plantilla configurada, crear las máquinas virtuales con hello `azure group deployment create` comando.</span><span class="sxs-lookup"><span data-stu-id="dc5ff-211">Once you have a template configured, you create your VMs using hello `azure group deployment create` command.</span></span> <span data-ttu-id="dc5ff-212">Especificar Hola URI de la plantilla JSON con hello `--template-uri` parámetro:</span><span class="sxs-lookup"><span data-stu-id="dc5ff-212">Specify hello URI of your JSON template with hello `--template-uri` parameter:</span></span>

```azurecli
azure group deployment create --resource-group myResourceGroup
    --template-uri https://uri.to.template/mytemplate.json
```

<span data-ttu-id="dc5ff-213">Si tiene un archivo JSON que se almacena localmente en el equipo, puede usar hello `--template-file` parámetro en su lugar:</span><span class="sxs-lookup"><span data-stu-id="dc5ff-213">If you have a JSON file stored locally on your computer, you can use hello `--template-file` parameter instead:</span></span>

```azurecli
azure group deployment create --resource-group myResourceGroup
    --template-file /path/to/mytemplate.json
```


## <a name="next-steps"></a><span data-ttu-id="dc5ff-214">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="dc5ff-214">Next steps</span></span>
<span data-ttu-id="dc5ff-215">Después de haber preparado y cargado el disco virtual personalizado, puede leer más sobre el [uso de Resource Manager y las plantillas](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="dc5ff-215">After you have prepared and uploaded your custom virtual disk, you can read more about [using Resource Manager and templates](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="dc5ff-216">Puede que también desee demasiado[agregar un disco de datos](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooyour nuevas máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="dc5ff-216">You may also want too[add a data disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooyour new VMs.</span></span> <span data-ttu-id="dc5ff-217">Si tiene aplicaciones que se ejecutan en las máquinas virtuales que necesite tooaccess, asegúrese de demasiado[puertos abiertos y los puntos de conexión](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="dc5ff-217">If you have applications running on your VMs that you need tooaccess, be sure too[open ports and endpoints](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

