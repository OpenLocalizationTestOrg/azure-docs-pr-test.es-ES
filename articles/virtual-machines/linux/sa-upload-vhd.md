---
title: un disco de Linux personalizado con Azure CLI 2.0 aaaUpload | Documentos de Microsoft
description: "Crear y cargar un tooAzure de disco duro virtual (VHD) mediante el modelo de implementación del Administrador de recursos de Hola y Hola 2.0 de CLI de Azure"
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: a8c7818f-eb65-409e-aa91-ce5ae975c564
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 07/10/2017
ms.author: cynthn
ms.openlocfilehash: cf8556ab4dfe6c4e5eff4e99fe1ddc44393f774c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="upload-and-create-a-linux-vm-from-custom-disk-with-hello-azure-cli-20"></a><span data-ttu-id="f76f9-103">Cargar y crear una VM Linux desde disco personalizado con hello 2.0 de CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="f76f9-103">Upload and create a Linux VM from custom disk with hello Azure CLI 2.0</span></span>
<span data-ttu-id="f76f9-104">Este artículo muestra cómo tooupload una tooan de disco duro virtual (VHD) el almacenamiento de Azure cuenta con hello 2.0 de CLI de Azure y crear máquinas virtuales de Linux desde este disco personalizado.</span><span class="sxs-lookup"><span data-stu-id="f76f9-104">This article shows you how tooupload a virtual hard disk (VHD) tooan Azure storage account with hello Azure CLI 2.0 and create Linux VMs from this custom disk.</span></span> <span data-ttu-id="f76f9-105">También puede realizar estos pasos con hello [Azure CLI 1.0](upload-vhd-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f76f9-105">You can also perform these steps with hello [Azure CLI 1.0](upload-vhd-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="f76f9-106">Esta funcionalidad le permite tooinstall y configurar una distribución de Linux tooyour requisitos y, a continuación, usar ese archivo VHD tooquickly crear máquinas virtuales de Azure (VM).</span><span class="sxs-lookup"><span data-stu-id="f76f9-106">This functionality allows you tooinstall and configure a Linux distro tooyour requirements and then use that VHD tooquickly create Azure virtual machines (VMs).</span></span>

<span data-ttu-id="f76f9-107">En este tema usa las cuentas de almacenamiento para hello finales discos duros virtuales, pero también puede realizar estos pasos con [discos administrados por](upload-vhd.md).</span><span class="sxs-lookup"><span data-stu-id="f76f9-107">This topic uses storage accounts for hello final VHDs, but you can also do these steps using [managed disks](upload-vhd.md).</span></span> 

## <a name="quick-commands"></a><span data-ttu-id="f76f9-108">Comandos rápidos</span><span class="sxs-lookup"><span data-stu-id="f76f9-108">Quick commands</span></span>
<span data-ttu-id="f76f9-109">Si necesita tooquickly realizar la tarea hello, Hola después Hola de detalles de la sección base tooupload comandos tooAzure de un disco duro virtual.</span><span class="sxs-lookup"><span data-stu-id="f76f9-109">If you need tooquickly accomplish hello task, hello following section details hello base commands tooupload a VHD tooAzure.</span></span> <span data-ttu-id="f76f9-110">Obtener más información y el contexto de cada paso se encuentran rest Hola de documento de hello, [a partir de aquí](#requirements).</span><span class="sxs-lookup"><span data-stu-id="f76f9-110">More detailed information and context for each step can be found hello rest of hello document, [starting here](#requirements).</span></span>

<span data-ttu-id="f76f9-111">Asegúrese de que tiene más reciente hello [CLI de Azure 2.0](/cli/azure/install-az-cli2) instalado y registrado en tooan cuenta de Azure mediante [inicio de sesión de az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="f76f9-111">Make sure that you have hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="f76f9-112">En hello en los ejemplos siguientes, reemplace los nombres de parámetros de ejemplo con sus propios valores.</span><span class="sxs-lookup"><span data-stu-id="f76f9-112">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="f76f9-113">Nombres de parámetros de ejemplo incluidos `myResourceGroup`, `mystorageaccount` y `mydisks`.</span><span class="sxs-lookup"><span data-stu-id="f76f9-113">Example parameter names included `myResourceGroup`, `mystorageaccount`, and `mydisks`.</span></span>

<span data-ttu-id="f76f9-114">En primer lugar, cree un grupo de recursos con [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="f76f9-114">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="f76f9-115">Hello en el ejemplo siguiente se crea un grupo de recursos denominado `myResourceGroup` en hello `WestUs` ubicación:</span><span class="sxs-lookup"><span data-stu-id="f76f9-115">hello following example creates a resource group named `myResourceGroup` in hello `WestUs` location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

<span data-ttu-id="f76f9-116">Crear un toohold de cuenta de almacenamiento de los discos virtuales con [crear cuenta de almacenamiento az](/cli/azure/storage/account#create).</span><span class="sxs-lookup"><span data-stu-id="f76f9-116">Create a storage account toohold your virtual disks with [az storage account create](/cli/azure/storage/account#create).</span></span> <span data-ttu-id="f76f9-117">Hello en el ejemplo siguiente se crea una cuenta de almacenamiento denominada `mystorageaccount`:</span><span class="sxs-lookup"><span data-stu-id="f76f9-117">hello following example creates a storage account named `mystorageaccount`:</span></span>

```azurecli
az storage account create --resource-group myResourceGroup --location westus \
  --name mystorageaccount --kind Storage --sku Standard_LRS
```

<span data-ttu-id="f76f9-118">Lista de claves de acceso de Hola para su cuenta de almacenamiento con [lista de claves de cuenta de almacenamiento az](/cli/azure/storage/account/keys#list).</span><span class="sxs-lookup"><span data-stu-id="f76f9-118">List hello access keys for your storage account with [az storage account keys list](/cli/azure/storage/account/keys#list).</span></span> <span data-ttu-id="f76f9-119">Tome nota de `key1`:</span><span class="sxs-lookup"><span data-stu-id="f76f9-119">Make a note of `key1`:</span></span>

```azurecli
az storage account keys list --resource-group myResourceGroup --account-name mystorageaccount
```

<span data-ttu-id="f76f9-120">Crear un contenedor dentro de su cuenta de almacenamiento con la clave de almacenamiento de hello obtenido con [crear contenedor de almacenamiento az](/cli/azure/storage/container#create).</span><span class="sxs-lookup"><span data-stu-id="f76f9-120">Create a container within your storage account using hello storage key you obtained with [az storage container create](/cli/azure/storage/container#create).</span></span> <span data-ttu-id="f76f9-121">Hello en el ejemplo siguiente se crea un contenedor denominado `mydisks` mediante el valor de clave de almacenamiento de Hola de `key1`:</span><span class="sxs-lookup"><span data-stu-id="f76f9-121">hello following example creates a container named `mydisks` using hello storage key value from `key1`:</span></span>

```azurecli
az storage container create --account-name mystorageaccount \
    --account-key key1 --name mydisks
```

<span data-ttu-id="f76f9-122">Por último, cargar el contenedor de toohello de disco duro virtual que creó con [carga de blobs de almacenamiento az](/cli/azure/storage/blob#upload).</span><span class="sxs-lookup"><span data-stu-id="f76f9-122">Finally, upload your VHD toohello container you created with [az storage blob upload](/cli/azure/storage/blob#upload).</span></span> <span data-ttu-id="f76f9-123">Especificar la ruta de acceso local de hello tooyour VHD en `/path/to/disk/mydisk.vhd`:</span><span class="sxs-lookup"><span data-stu-id="f76f9-123">Specify hello local path tooyour VHD under `/path/to/disk/mydisk.vhd`:</span></span>

```azurecli
az storage blob upload --account-name mystorageaccount \
    --account-key key1 --container-name mydisks --type page \
    --file /path/to/disk/mydisk.vhd --name myDisk.vhd
```

<span data-ttu-id="f76f9-124">Especifique Hola URI tooyour disco (`--image`) con [crear vm az](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="f76f9-124">Specify hello URI tooyour disk (`--image`) with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="f76f9-125">Hello en el ejemplo siguiente se crea una máquina virtual denominada `myVM` con disco virtual Hola cargado previamente:</span><span class="sxs-lookup"><span data-stu-id="f76f9-125">hello following example creates a VM named `myVM` using hello virtual disk previously uploaded:</span></span>

```azurecli
az vm create --resource-group myResourceGroup --location westus \
    --name myVM --storage-account mystorageaccount --os-type linux \
    --admin-username azureuser --ssh-key-value ~/.ssh/id_rsa.pub \
    --image https://mystorageaccount.blob.core.windows.net/mydisk/myDisks.vhd \
    --use-unmanaged-disk
```

<span data-ttu-id="f76f9-126">cuenta de almacenamiento de destino de Hello tiene toobe Hola igual como donde cargar el disco virtual para.</span><span class="sxs-lookup"><span data-stu-id="f76f9-126">hello destination storage account has toobe hello same as where you uploaded your virtual disk to.</span></span> <span data-ttu-id="f76f9-127">También necesita toospecify o responder a peticiones de, todos los parámetros adicionales requeridos por Hola de Hola **crear vm az** comando como la red virtual, la dirección IP pública, nombre de usuario y las claves de SSH.</span><span class="sxs-lookup"><span data-stu-id="f76f9-127">You also need toospecify, or answer prompts for, all hello additional parameters required by hello **az vm create** command such as virtual network, public IP address, username, and SSH keys.</span></span> <span data-ttu-id="f76f9-128">Puede leer más sobre hello [disponibles parámetros del Administrador de recursos de CLI](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).</span><span class="sxs-lookup"><span data-stu-id="f76f9-128">You can read more about hello [available CLI Resource Manager parameters](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).</span></span>

## <a name="requirements"></a><span data-ttu-id="f76f9-129">Requisitos</span><span class="sxs-lookup"><span data-stu-id="f76f9-129">Requirements</span></span>
<span data-ttu-id="f76f9-130">Hola toocomplete siguiendo los pasos, debe:</span><span class="sxs-lookup"><span data-stu-id="f76f9-130">toocomplete hello following steps, you need:</span></span>

* <span data-ttu-id="f76f9-131">**Sistema operativo Linux instalado en un archivo .vhd** -instalar un [distribución de Linux están aprobados Azure](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (o consulte [información para las distribuciones no aprobadas](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa disco virtual en hello VHD formato.</span><span class="sxs-lookup"><span data-stu-id="f76f9-131">**Linux operating system installed in a .vhd file** - Install an [Azure-endorsed Linux distribution](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (or see [information for non-endorsed distributions](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa virtual disk in hello VHD format.</span></span> <span data-ttu-id="f76f9-132">Varias herramientas existen toocreate una máquina virtual y el disco duro virtual:</span><span class="sxs-lookup"><span data-stu-id="f76f9-132">Multiple tools exist toocreate a VM and VHD:</span></span>
  * <span data-ttu-id="f76f9-133">Instalar y configurar [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) o [KVM](http://www.linux-kvm.org/page/RunningKVM), teniendo cuidado de toouse del disco duro virtual como el formato de imagen.</span><span class="sxs-lookup"><span data-stu-id="f76f9-133">Install and configure [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) or [KVM](http://www.linux-kvm.org/page/RunningKVM), taking care toouse VHD as your image format.</span></span> <span data-ttu-id="f76f9-134">Si es necesario, puede [convertir una imagen](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) con `qemu-img convert`.</span><span class="sxs-lookup"><span data-stu-id="f76f9-134">If needed, you can [convert an image](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) using `qemu-img convert`.</span></span>
  * <span data-ttu-id="f76f9-135">También puede usar Hyper-V [en Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) o [en Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="f76f9-135">You can also use Hyper-V [on Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) or [on Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="f76f9-136">no se admite el formato VHDX más reciente de Hello en Azure.</span><span class="sxs-lookup"><span data-stu-id="f76f9-136">hello newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="f76f9-137">Cuando se crea una máquina virtual, especifique VHD como formato de Hola.</span><span class="sxs-lookup"><span data-stu-id="f76f9-137">When you create a VM, specify VHD as hello format.</span></span> <span data-ttu-id="f76f9-138">Si es necesario, se puede convertir VHDX discos tooVHD con [ `qemu-img convert` ](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) o hello [ `Convert-VHD` ](https://technet.microsoft.com/library/hh848454.aspx) cmdlet de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f76f9-138">If needed, you can convert VHDX disks tooVHD using [`qemu-img convert`](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) or hello [`Convert-VHD`](https://technet.microsoft.com/library/hh848454.aspx) PowerShell cmdlet.</span></span> <span data-ttu-id="f76f9-139">Además, Azure no permite cargar discos duros virtuales dinámicos, por lo que necesita tooconvert tal toostatic discos VHD antes de cargar.</span><span class="sxs-lookup"><span data-stu-id="f76f9-139">Further, Azure does not support uploading dynamic VHDs, so you need tooconvert such disks toostatic VHDs before uploading.</span></span> <span data-ttu-id="f76f9-140">Puede usar herramientas como [utilidades de disco duro virtual de Azure para ir](https://github.com/Microsoft/azure-vhd-utils-for-go) tooconvert discos dinámicos durante el proceso de Hola de carga tooAzure.</span><span class="sxs-lookup"><span data-stu-id="f76f9-140">You can use tools such as [Azure VHD Utilities for GO](https://github.com/Microsoft/azure-vhd-utils-for-go) tooconvert dynamic disks during hello process of uploading tooAzure.</span></span>
> 
> 

* <span data-ttu-id="f76f9-141">Máquinas virtuales creadas a partir del disco personalizado deben residir en hello misma cuenta de almacenamiento como el propio disco Hola</span><span class="sxs-lookup"><span data-stu-id="f76f9-141">VMs created from your custom disk must reside in hello same storage account as hello disk itself</span></span>
  * <span data-ttu-id="f76f9-142">Crear un toohold de cuenta y el contenedor de almacenamiento del disco personalizado y creado las máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="f76f9-142">Create a storage account and container toohold both your custom disk and created VMs</span></span>
  * <span data-ttu-id="f76f9-143">Una vez que haya creado todas las máquinas virtuales, puede eliminar el disco de forma segura.</span><span class="sxs-lookup"><span data-stu-id="f76f9-143">After you have created all your VMs, you can safely delete your disk</span></span>

<span data-ttu-id="f76f9-144">Asegúrese de que tiene más reciente hello [CLI de Azure 2.0](/cli/azure/install-az-cli2) instalado y registrado en tooan cuenta de Azure mediante [inicio de sesión de az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="f76f9-144">Make sure that you have hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="f76f9-145">En hello en los ejemplos siguientes, reemplace los nombres de parámetros de ejemplo con sus propios valores.</span><span class="sxs-lookup"><span data-stu-id="f76f9-145">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="f76f9-146">Nombres de parámetros de ejemplo incluidos `myResourceGroup`, `mystorageaccount` y `mydisks`.</span><span class="sxs-lookup"><span data-stu-id="f76f9-146">Example parameter names included `myResourceGroup`, `mystorageaccount`, and `mydisks`.</span></span>

<span data-ttu-id="f76f9-147"><a id="prepimage"></a></span><span class="sxs-lookup"><span data-stu-id="f76f9-147"><a id="prepimage"> </a></span></span>

## <a name="prepare-hello-disk-toobe-uploaded"></a><span data-ttu-id="f76f9-148">Preparar Hola disco toobe cargado</span><span class="sxs-lookup"><span data-stu-id="f76f9-148">Prepare hello disk toobe uploaded</span></span>
<span data-ttu-id="f76f9-149">Azure admite varias distribuciones Linux (consulte [Distribuciones aprobadas](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span><span class="sxs-lookup"><span data-stu-id="f76f9-149">Azure supports various Linux distributions (see [Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span></span> <span data-ttu-id="f76f9-150">Hola siguientes artículos guiarle por cómo tooprepare Hola diversas distribuciones de Linux que se admiten en Azure:</span><span class="sxs-lookup"><span data-stu-id="f76f9-150">hello following articles guide you through how tooprepare hello various Linux distributions that are supported on Azure:</span></span>

* <span data-ttu-id="f76f9-151">**[Distribuciones basadas en CentOS](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="f76f9-151">**[CentOS-based Distributions](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="f76f9-152">**[Debian Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="f76f9-152">**[Debian Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="f76f9-153">**[Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="f76f9-153">**[Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="f76f9-154">**[Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="f76f9-154">**[Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="f76f9-155">**[SLES y openSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="f76f9-155">**[SLES & openSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="f76f9-156">**[Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="f76f9-156">**[Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="f76f9-157">**[Otras distribuciones no aprobadas](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="f76f9-157">**[Other - Non-Endorsed Distributions](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>

<span data-ttu-id="f76f9-158">Consulte también hello  **[notas sobre la instalación de Linux](create-upload-generic.md#general-linux-installation-notes)**  para obtener más sugerencias sobre cómo preparar imágenes de Linux de Azure.</span><span class="sxs-lookup"><span data-stu-id="f76f9-158">Also see hello **[Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes)** for more general tips on preparing Linux images for Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="f76f9-159">Hola [plataforma Windows Azure SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/) aplica tooVMs ejecutando Linux sólo cuando uno de hello están aprobados distribuciones se utilizan con los detalles de configuración de hello tal como se especifica en 'Admite versiones' en [Linux en Azure aprobadas Distribuciones](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f76f9-159">hello [Azure platform SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/) applies tooVMs running Linux only when one of hello endorsed distributions is used with hello configuration details as specified under 'Supported Versions' in [Linux on Azure-Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
> 
> 

## <a name="create-a-resource-group"></a><span data-ttu-id="f76f9-160">Crear un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="f76f9-160">Create a resource group</span></span>
<span data-ttu-id="f76f9-161">Grupos de recursos lógicamente reunir todos los toosupport de recursos de Azure de hello las máquinas virtuales, como una red virtual Hola y el almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="f76f9-161">Resource groups logically bring together all hello Azure resources toosupport your virtual machines, such as hello virtual networking and storage.</span></span> <span data-ttu-id="f76f9-162">Para más información acerca de los grupos de recursos, consulte [Información general de Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f76f9-162">For more information resource groups, see [resource groups overview](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="f76f9-163">Antes de cargar el disco personalizado y crear máquinas virtuales, primero debe toocreate un grupo de recursos con [crear grupo az](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="f76f9-163">Before uploading your custom disk and creating VMs, you first need toocreate a resource group with [az group create](/cli/azure/group#create).</span></span>

<span data-ttu-id="f76f9-164">Hello en el ejemplo siguiente se crea un grupo de recursos denominado `myResourceGroup` en hello `westus` ubicación:</span><span class="sxs-lookup"><span data-stu-id="f76f9-164">hello following example creates a resource group named `myResourceGroup` in hello `westus` location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

## <a name="create-a-storage-account"></a><span data-ttu-id="f76f9-165">Crear una cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="f76f9-165">Create a storage account</span></span>

<span data-ttu-id="f76f9-166">Cree una cuenta de almacenamiento para el disco personalizado y las máquinas virtuales con [az storage account create](/cli/azure/storage/account#create).</span><span class="sxs-lookup"><span data-stu-id="f76f9-166">Create a storage account for your custom disk and VMs with [az storage account create](/cli/azure/storage/account#create).</span></span> <span data-ttu-id="f76f9-167">Todas las máquinas virtuales con discos no administrados que se crean desde su toobe de necesidad de disco personalizado en hello misma cuenta de almacenamiento que dicho disco.</span><span class="sxs-lookup"><span data-stu-id="f76f9-167">Any VMs with unmanaged disks that you create from your custom disk need toobe in hello same storage account as that disk.</span></span> 

<span data-ttu-id="f76f9-168">Hello en el ejemplo siguiente se crea una cuenta de almacenamiento denominada `mystorageaccount` en grupo de recursos de hello creado anteriormente:</span><span class="sxs-lookup"><span data-stu-id="f76f9-168">hello following example creates a storage account named `mystorageaccount` in hello resource group previously created:</span></span>

```azurecli
az storage account create --resource-group myResourceGroup --location westus \
  --name mystorageaccount --kind Storage --sku Standard_LRS
```

## <a name="list-storage-account-keys"></a><span data-ttu-id="f76f9-169">Enumerar claves de cuentas de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="f76f9-169">List storage account keys</span></span>
<span data-ttu-id="f76f9-170">Azure genera dos claves de acceso de 512 bits para cada cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="f76f9-170">Azure generates two 512-bit access keys for each storage account.</span></span> <span data-ttu-id="f76f9-171">Estas teclas de acceso se utilizan para autenticar la cuenta de almacenamiento de toohello, como toocarry operaciones de escritura de salida.</span><span class="sxs-lookup"><span data-stu-id="f76f9-171">These access keys are used when authenticating toohello storage account, such as toocarry out write operations.</span></span> <span data-ttu-id="f76f9-172">Obtenga más información sobre [administrar acceso toostorage aquí](../../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="f76f9-172">Read more about [managing access toostorage here](../../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span> <span data-ttu-id="f76f9-173">Ver las teclas de acceso de hello con [lista de claves de cuenta de almacenamiento az](/cli/azure/storage/account/keys#list).</span><span class="sxs-lookup"><span data-stu-id="f76f9-173">You view hello access keys with [az storage account keys list](/cli/azure/storage/account/keys#list).</span></span>

<span data-ttu-id="f76f9-174">Ver las teclas de acceso de Hola Hola cuenta de almacenamiento que creó:</span><span class="sxs-lookup"><span data-stu-id="f76f9-174">View hello access keys for hello storage account you created:</span></span>

```azurecli
az storage account keys list --resource-group myResourceGroup --account-name mystorageaccount
```

<span data-ttu-id="f76f9-175">es similar a la salida de Hello:</span><span class="sxs-lookup"><span data-stu-id="f76f9-175">hello output is similar to:</span></span>

```azurecli
info:    Executing command storage account keys list
+ Getting storage account keys
data:    Name  Key                                                                                       Permissions
data:    ----  ----------------------------------------------------------------------------------------  -----------
data:    key1  d4XAvZzlGAgWdvhlWfkZ9q4k9bYZkXkuPCJ15NTsQOeDeowCDAdB80r9zA/tUINApdSGQ94H9zkszYyxpe8erw==  Full
data:    key2  Ww0T7g4UyYLaBnLYcxIOTVziGAAHvU+wpwuPvK4ZG0CDFwu/mAxS/YYvAQGHocq1w7/3HcalbnfxtFdqoXOw8g==  Full
info:    storage account keys list command OK
```
<span data-ttu-id="f76f9-176">Tome nota del `key1` tal y como se va a utilizar se toointeract con su cuenta de almacenamiento en los pasos siguientes de Hola.</span><span class="sxs-lookup"><span data-stu-id="f76f9-176">Make a note of `key1` as you will use it toointeract with your storage account in hello next steps.</span></span>

## <a name="create-a-storage-container"></a><span data-ttu-id="f76f9-177">Creación de un contenedor de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="f76f9-177">Create a storage container</span></span>
<span data-ttu-id="f76f9-178">Hola igual que crear directorios distintos toologically organizar el sistema de archivos local, crear contenedores dentro de un tooorganize de cuenta de almacenamiento de los discos.</span><span class="sxs-lookup"><span data-stu-id="f76f9-178">In hello same way that you create different directories toologically organize your local file system, you create containers within a storage account tooorganize your disks.</span></span> <span data-ttu-id="f76f9-179">Una cuenta de almacenamiento puede contener un número cualquiera de contenedores.</span><span class="sxs-lookup"><span data-stu-id="f76f9-179">A storage account can contain any number of containers.</span></span> <span data-ttu-id="f76f9-180">Cree un contenedor con [az storage container create](/cli/azure/storage/container#create).</span><span class="sxs-lookup"><span data-stu-id="f76f9-180">Create a container with [az storage container create](/cli/azure/storage/container#create).</span></span>

<span data-ttu-id="f76f9-181">Hello en el ejemplo siguiente se crea un contenedor denominado `mydisks`:</span><span class="sxs-lookup"><span data-stu-id="f76f9-181">hello following example creates a container named `mydisks`:</span></span>

```azurecli
az storage container create \
    --account-name mystorageaccount \
    --name mydisks
```

## <a name="upload-vhd"></a><span data-ttu-id="f76f9-182">Carga de VHD</span><span class="sxs-lookup"><span data-stu-id="f76f9-182">Upload VHD</span></span>
<span data-ttu-id="f76f9-183">Ahora puede cargar su disco personalizado con [az storage blob upload](/cli/azure/storage/blob#upload).</span><span class="sxs-lookup"><span data-stu-id="f76f9-183">Now upload your custom disk with [az storage blob upload](/cli/azure/storage/blob#upload).</span></span> <span data-ttu-id="f76f9-184">Cargue y almacene el disco personalizado como un blob en páginas.</span><span class="sxs-lookup"><span data-stu-id="f76f9-184">You upload and store your custom disk as a page blob.</span></span>

<span data-ttu-id="f76f9-185">Especifique la clave de acceso, el contenedor de Hola que creó en el paso anterior de hello y, a continuación, Hola disco personalizado de toohello de ruta de acceso en el equipo local:</span><span class="sxs-lookup"><span data-stu-id="f76f9-185">Specify your access key, hello container you created in hello previous step, and then hello path toohello custom disk on your local computer:</span></span>

```azurecli
az storage blob upload --account-name mystorageaccount \
    --account-key key1 --container-name mydisks --type page \
    --file /path/to/disk/mydisk.vhd --name myDisk.vhd
```

## <a name="create-hello-vm"></a><span data-ttu-id="f76f9-186">Crear hello VM</span><span class="sxs-lookup"><span data-stu-id="f76f9-186">Create hello VM</span></span>
<span data-ttu-id="f76f9-187">toocreate una máquina virtual con discos no administrados, especifique el disco de tooyour URI de hello (`--image`) con [crear vm az](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="f76f9-187">toocreate a VM with unmanaged disks, specify hello URI tooyour disk (`--image`) with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="f76f9-188">Hello en el ejemplo siguiente se crea una máquina virtual denominada `myVM` con disco virtual Hola cargado previamente:</span><span class="sxs-lookup"><span data-stu-id="f76f9-188">hello following example creates a VM named `myVM` using hello virtual disk previously uploaded:</span></span>

<span data-ttu-id="f76f9-189">Especificar hello `--image` parámetro con [crear vm az](/cli/azure/vm#create) toopoint tooyour personalizado disco.</span><span class="sxs-lookup"><span data-stu-id="f76f9-189">You specify hello `--image` parameter with [az vm create](/cli/azure/vm#create) toopoint tooyour custom disk.</span></span> <span data-ttu-id="f76f9-190">Asegúrese de que `--storage-account` coincidencias Hola cuenta de almacenamiento donde se almacena el disco personalizado.</span><span class="sxs-lookup"><span data-stu-id="f76f9-190">Ensure that `--storage-account` matches hello storage account where your custom disk is stored.</span></span> <span data-ttu-id="f76f9-191">No es necesario toouse Hola mismo contenedor como Hola disco personalizada toostore las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="f76f9-191">You do not have toouse hello same container as hello custom disk toostore your VMs.</span></span> <span data-ttu-id="f76f9-192">Realizar toocreate seguro de los contenedores adicionales en hello misma manera que Hola pasos anteriores antes de cargar el disco personalizado.</span><span class="sxs-lookup"><span data-stu-id="f76f9-192">Make sure toocreate any additional containers in hello same way as hello earlier steps before uploading your custom disk.</span></span>

<span data-ttu-id="f76f9-193">Hello en el ejemplo siguiente se crea una máquina virtual denominada `myVM` desde el disco personalizado:</span><span class="sxs-lookup"><span data-stu-id="f76f9-193">hello following example creates a VM named `myVM` from your custom disk:</span></span>

```azurecli
az vm create --resource-group myResourceGroup --location westus \
    --name myVM --storage-account mystorageaccount --os-type linux \
    --admin-username azureuser --ssh-key-value ~/.ssh/id_rsa.pub \
    --image https://mystorageaccount.blob.core.windows.net/mydisks/myDisk.vhd \
    --use-unmanaged-disk
```

<span data-ttu-id="f76f9-194">Todavía necesita toospecify o responder a peticiones de, todos los parámetros adicionales requeridos por Hola de Hola **crear vm az** comando como nombre de usuario y las claves SSH.</span><span class="sxs-lookup"><span data-stu-id="f76f9-194">You still need toospecify, or answer prompts for, all hello additional parameters required by hello **az vm create** command such as username and SSH keys.</span></span>


## <a name="resource-manager-template"></a><span data-ttu-id="f76f9-195">Plantilla de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f76f9-195">Resource Manager template</span></span>
<span data-ttu-id="f76f9-196">Plantillas de administrador de recursos de Azure son archivos de JavaScript Object Notation (JSON) que definen el entorno de hello desea toobuild.</span><span class="sxs-lookup"><span data-stu-id="f76f9-196">Azure Resource Manager templates are JavaScript Object Notation (JSON) files that define hello environment you wish toobuild.</span></span> <span data-ttu-id="f76f9-197">plantillas de Hola se desglosan en proveedores de recursos de toodifferent como compute o red.</span><span class="sxs-lookup"><span data-stu-id="f76f9-197">hello templates are broken down in toodifferent resource providers such as compute or network.</span></span> <span data-ttu-id="f76f9-198">Puede usar las plantillas existentes o escribir las suyas propias.</span><span class="sxs-lookup"><span data-stu-id="f76f9-198">You can use existing templates or write your own.</span></span> <span data-ttu-id="f76f9-199">Lea más sobre el [uso de Resource Manager y las plantillas](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f76f9-199">Read more about [using Resource Manager and templates](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="f76f9-200">Dentro de hello `Microsoft.Compute/virtualMachines` proveedor de la plantilla, tendrá un `storageProfile` nodo que contiene los detalles de configuración de hello para la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="f76f9-200">Within hello `Microsoft.Compute/virtualMachines` provider of your template, you have a `storageProfile` node that contains hello configuration details for your VM.</span></span> <span data-ttu-id="f76f9-201">Hola dos parámetros principales tooedit son hello `image` y `vhd` URI que apuntan al disco personalizada tooyour y disco virtual de la máquina virtual nueva.</span><span class="sxs-lookup"><span data-stu-id="f76f9-201">hello two main parameters tooedit are hello `image` and `vhd` URIs that point tooyour custom disk and your new VM's virtual disk.</span></span> <span data-ttu-id="f76f9-202">siguiente Hello muestra un ejemplo de Hola JSON para usar un disco personalizado:</span><span class="sxs-lookup"><span data-stu-id="f76f9-202">hello following shows an example of hello JSON for using a custom disk:</span></span>

```json
"storageProfile": {
          "osDisk": {
            "name": "myVM",
            "osType": "Linux",
            "caching": "ReadWrite",
            "createOption": "FromImage",
            "image": {
              "uri": "https://mystorageaccount.blob.core.windows.net/mydisks/myDisk.vhd"
            },
            "vhd": {
              "uri": "https://mystorageaccount.blob.core.windows.net/vhds/newvmname.vhd"
            }
          }
```

<span data-ttu-id="f76f9-203">Puede usar [esta toocreate de plantilla existente una máquina virtual desde una imagen personalizada](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) o leer acerca de [crear sus propias plantillas de Azure Resource Manager](../../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="f76f9-203">You can use [this existing template toocreate a VM from a custom image](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) or read about [creating your own Azure Resource Manager templates](../../azure-resource-manager/resource-group-authoring-templates.md).</span></span> 

<span data-ttu-id="f76f9-204">Una vez que tenga una plantilla configurada, utilice [Crear implementación de grupo az](/cli/azure/group/deployment#create) toocreate las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="f76f9-204">Once you have a template configured, use [az group deployment create](/cli/azure/group/deployment#create) toocreate your VMs.</span></span> <span data-ttu-id="f76f9-205">Especificar Hola URI de la plantilla JSON con hello `--template-uri` parámetro:</span><span class="sxs-lookup"><span data-stu-id="f76f9-205">Specify hello URI of your JSON template with hello `--template-uri` parameter:</span></span>

```azurecli
az group deployment create --resource-group myNewResourceGroup \
  --template-uri https://uri.to.template/mytemplate.json
```

<span data-ttu-id="f76f9-206">Si tiene un archivo JSON que se almacena localmente en el equipo, puede usar hello `--template-file` parámetro en su lugar:</span><span class="sxs-lookup"><span data-stu-id="f76f9-206">If you have a JSON file stored locally on your computer, you can use hello `--template-file` parameter instead:</span></span>

```azurecli
az group deployment create --resource-group myNewResourceGroup \
  --template-file /path/to/mytemplate.json
```


## <a name="next-steps"></a><span data-ttu-id="f76f9-207">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f76f9-207">Next steps</span></span>
<span data-ttu-id="f76f9-208">Después de haber preparado y cargado el disco virtual personalizado, puede leer más sobre el [uso de Resource Manager y las plantillas](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f76f9-208">After you have prepared and uploaded your custom virtual disk, you can read more about [using Resource Manager and templates](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="f76f9-209">Puede que también desee demasiado[agregar un disco de datos](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooyour nuevas máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="f76f9-209">You may also want too[add a data disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooyour new VMs.</span></span> <span data-ttu-id="f76f9-210">Si tiene aplicaciones que se ejecutan en las máquinas virtuales que necesite tooaccess, asegúrese de demasiado[puertos abiertos y los puntos de conexión](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f76f9-210">If you have applications running on your VMs that you need tooaccess, be sure too[open ports and endpoints](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

