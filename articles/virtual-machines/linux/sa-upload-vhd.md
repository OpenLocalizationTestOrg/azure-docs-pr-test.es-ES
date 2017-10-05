---
title: Carga de un disco de Linux personalizado con la CLI de Azure 2.0 | Microsoft Docs
description: "Creación y carga en Azure de un disco duro virtual (VHD) mediante el modelo de implementación de Resource Manager y la CLI de Azure 2.0"
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
ms.openlocfilehash: 9159960af396e89f373da711e0cc46fdd996ab83
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="upload-and-create-a-linux-vm-from-custom-disk-with-the-azure-cli-20"></a><span data-ttu-id="6d1be-103">Carga y creación de una máquina virtual Linux a partir de un disco personalizado mediante la CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="6d1be-103">Upload and create a Linux VM from custom disk with the Azure CLI 2.0</span></span>
<span data-ttu-id="6d1be-104">En este artículo se muestra cómo cargar un disco duro virtual en una cuenta de almacenamiento de Azure mediante la CLI de Azure 2.0 y cómo crear máquinas virtuales Linux desde este disco personalizado.</span><span class="sxs-lookup"><span data-stu-id="6d1be-104">This article shows you how to upload a virtual hard disk (VHD) to an Azure storage account with the Azure CLI 2.0 and create Linux VMs from this custom disk.</span></span> <span data-ttu-id="6d1be-105">También puede llevar a cabo estos pasos con la [CLI de Azure 1.0](upload-vhd-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6d1be-105">You can also perform these steps with the [Azure CLI 1.0](upload-vhd-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="6d1be-106">Esta funcionalidad le permite instalar y configurar una distribución de Linux según sus requisitos y después utilizar ese disco duro virtual para crear rápidamente máquinas virtuales de Azure.</span><span class="sxs-lookup"><span data-stu-id="6d1be-106">This functionality allows you to install and configure a Linux distro to your requirements and then use that VHD to quickly create Azure virtual machines (VMs).</span></span>

<span data-ttu-id="6d1be-107">En este tema se usan las cuentas de almacenamiento de los discos duros virtuales finales, pero también puede seguir estos pasos con [discos administrados](upload-vhd.md).</span><span class="sxs-lookup"><span data-stu-id="6d1be-107">This topic uses storage accounts for the final VHDs, but you can also do these steps using [managed disks](upload-vhd.md).</span></span> 

## <a name="quick-commands"></a><span data-ttu-id="6d1be-108">Comandos rápidos</span><span class="sxs-lookup"><span data-stu-id="6d1be-108">Quick commands</span></span>
<span data-ttu-id="6d1be-109">Si necesita realizar rápidamente la tarea, en la siguiente sección se detallan los comandos base para cargar un disco duro virtual en Azure.</span><span class="sxs-lookup"><span data-stu-id="6d1be-109">If you need to quickly accomplish the task, the following section details the base commands to upload a VHD to Azure.</span></span> <span data-ttu-id="6d1be-110">Se puede encontrar información más detallada y contexto para cada paso en el resto del documento, [comenzando aquí](#requirements).</span><span class="sxs-lookup"><span data-stu-id="6d1be-110">More detailed information and context for each step can be found the rest of the document, [starting here](#requirements).</span></span>

<span data-ttu-id="6d1be-111">Asegúrese de que ha instalado la última versión de la [CLI de Azure 2.0](/cli/azure/install-az-cli2) y de que ha iniciado sesión en una cuenta de Azure con [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="6d1be-111">Make sure that you have the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="6d1be-112">En los ejemplos siguientes, reemplace los nombres de parámetros de ejemplo por los suyos propios.</span><span class="sxs-lookup"><span data-stu-id="6d1be-112">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="6d1be-113">Nombres de parámetros de ejemplo incluidos `myResourceGroup`, `mystorageaccount` y `mydisks`.</span><span class="sxs-lookup"><span data-stu-id="6d1be-113">Example parameter names included `myResourceGroup`, `mystorageaccount`, and `mydisks`.</span></span>

<span data-ttu-id="6d1be-114">En primer lugar, cree un grupo de recursos con [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="6d1be-114">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="6d1be-115">En el ejemplo siguiente se crea un grupo de recursos denominado `myResourceGroup` en la ubicación `WestUs`:</span><span class="sxs-lookup"><span data-stu-id="6d1be-115">The following example creates a resource group named `myResourceGroup` in the `WestUs` location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

<span data-ttu-id="6d1be-116">Cree una cuenta de almacenamiento que contenga los discos virtuales con [az storage account create](/cli/azure/storage/account#create).</span><span class="sxs-lookup"><span data-stu-id="6d1be-116">Create a storage account to hold your virtual disks with [az storage account create](/cli/azure/storage/account#create).</span></span> <span data-ttu-id="6d1be-117">En el ejemplo siguiente se crea una cuenta de almacenamiento denominada `mystorageaccount`:</span><span class="sxs-lookup"><span data-stu-id="6d1be-117">The following example creates a storage account named `mystorageaccount`:</span></span>

```azurecli
az storage account create --resource-group myResourceGroup --location westus \
  --name mystorageaccount --kind Storage --sku Standard_LRS
```

<span data-ttu-id="6d1be-118">Cree una lista de las claves de acceso de la cuenta de almacenamiento con [az storage account keys list](/cli/azure/storage/account/keys#list).</span><span class="sxs-lookup"><span data-stu-id="6d1be-118">List the access keys for your storage account with [az storage account keys list](/cli/azure/storage/account/keys#list).</span></span> <span data-ttu-id="6d1be-119">Tome nota de `key1`:</span><span class="sxs-lookup"><span data-stu-id="6d1be-119">Make a note of `key1`:</span></span>

```azurecli
az storage account keys list --resource-group myResourceGroup --account-name mystorageaccount
```

<span data-ttu-id="6d1be-120">Cree un contenedor en su cuenta de almacenamiento mediante la clave de almacenamiento que obtuvo con [az storage container create](/cli/azure/storage/container#create).</span><span class="sxs-lookup"><span data-stu-id="6d1be-120">Create a container within your storage account using the storage key you obtained with [az storage container create](/cli/azure/storage/container#create).</span></span> <span data-ttu-id="6d1be-121">En el ejemplo siguiente se crea un contenedor denominado `mydisks` con el valor de clave de almacenamiento de `key1`:</span><span class="sxs-lookup"><span data-stu-id="6d1be-121">The following example creates a container named `mydisks` using the storage key value from `key1`:</span></span>

```azurecli
az storage container create --account-name mystorageaccount \
    --account-key key1 --name mydisks
```

<span data-ttu-id="6d1be-122">Por último, cargue el disco duro virtual en el contenedor que creó con [az storage blob upload](/cli/azure/storage/blob#upload).</span><span class="sxs-lookup"><span data-stu-id="6d1be-122">Finally, upload your VHD to the container you created with [az storage blob upload](/cli/azure/storage/blob#upload).</span></span> <span data-ttu-id="6d1be-123">Especifique la ruta de acceso local para el disco duro virtual en `/path/to/disk/mydisk.vhd`:</span><span class="sxs-lookup"><span data-stu-id="6d1be-123">Specify the local path to your VHD under `/path/to/disk/mydisk.vhd`:</span></span>

```azurecli
az storage blob upload --account-name mystorageaccount \
    --account-key key1 --container-name mydisks --type page \
    --file /path/to/disk/mydisk.vhd --name myDisk.vhd
```

<span data-ttu-id="6d1be-124">Especifique el URI del disco (`--image`) con [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="6d1be-124">Specify the URI to your disk (`--image`) with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="6d1be-125">En el ejemplo siguiente se crea una máquina virtual denominada `myVM` con el disco virtual cargado anteriormente:</span><span class="sxs-lookup"><span data-stu-id="6d1be-125">The following example creates a VM named `myVM` using the virtual disk previously uploaded:</span></span>

```azurecli
az vm create --resource-group myResourceGroup --location westus \
    --name myVM --storage-account mystorageaccount --os-type linux \
    --admin-username azureuser --ssh-key-value ~/.ssh/id_rsa.pub \
    --image https://mystorageaccount.blob.core.windows.net/mydisk/myDisks.vhd \
    --use-unmanaged-disk
```

<span data-ttu-id="6d1be-126">La cuenta de almacenamiento de destino debe ser la misma cuenta donde cargó su disco virtual.</span><span class="sxs-lookup"><span data-stu-id="6d1be-126">The destination storage account has to be the same as where you uploaded your virtual disk to.</span></span> <span data-ttu-id="6d1be-127">También debe especificar todos los parámetros adicionales requeridos, o responder a sus avisos, por el comando **az vm create**, como la red virtual, la dirección IP pública, el nombre de usuario y las claves SSH.</span><span class="sxs-lookup"><span data-stu-id="6d1be-127">You also need to specify, or answer prompts for, all the additional parameters required by the **az vm create** command such as virtual network, public IP address, username, and SSH keys.</span></span> <span data-ttu-id="6d1be-128">Puede leer más sobre los [parámetros disponibles de Resource Manager de la CLI](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).</span><span class="sxs-lookup"><span data-stu-id="6d1be-128">You can read more about the [available CLI Resource Manager parameters](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).</span></span>

## <a name="requirements"></a><span data-ttu-id="6d1be-129">Requisitos</span><span class="sxs-lookup"><span data-stu-id="6d1be-129">Requirements</span></span>
<span data-ttu-id="6d1be-130">Para completar los pasos siguientes, necesita:</span><span class="sxs-lookup"><span data-stu-id="6d1be-130">To complete the following steps, you need:</span></span>

* <span data-ttu-id="6d1be-131">**Sistema operativo Linux instalado en un archivo .vhd**: instale una [distribución de Linux aprobada por Azure](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (o consulte la [información para distribuciones no aprobadas](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) en un disco virtual en el formato VHD.</span><span class="sxs-lookup"><span data-stu-id="6d1be-131">**Linux operating system installed in a .vhd file** - Install an [Azure-endorsed Linux distribution](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (or see [information for non-endorsed distributions](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) to a virtual disk in the VHD format.</span></span> <span data-ttu-id="6d1be-132">Existen varias herramientas para crear una máquina virtual y archivos VHD:</span><span class="sxs-lookup"><span data-stu-id="6d1be-132">Multiple tools exist to create a VM and VHD:</span></span>
  * <span data-ttu-id="6d1be-133">Instale y configure [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) o [KVM](http://www.linux-kvm.org/page/RunningKVM), teniendo cuidado de usar VHD como formato de imagen.</span><span class="sxs-lookup"><span data-stu-id="6d1be-133">Install and configure [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) or [KVM](http://www.linux-kvm.org/page/RunningKVM), taking care to use VHD as your image format.</span></span> <span data-ttu-id="6d1be-134">Si es necesario, puede [convertir una imagen](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) con `qemu-img convert`.</span><span class="sxs-lookup"><span data-stu-id="6d1be-134">If needed, you can [convert an image](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) using `qemu-img convert`.</span></span>
  * <span data-ttu-id="6d1be-135">También puede usar Hyper-V [en Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) o [en Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="6d1be-135">You can also use Hyper-V [on Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) or [on Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="6d1be-136">el reciente formato VHDX no se admite en Azure.</span><span class="sxs-lookup"><span data-stu-id="6d1be-136">The newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="6d1be-137">Al crear una máquina virtual, especifique un VHD como formato.</span><span class="sxs-lookup"><span data-stu-id="6d1be-137">When you create a VM, specify VHD as the format.</span></span> <span data-ttu-id="6d1be-138">Si es necesario, puede convertir discos VHDX a VHD mediante [`qemu-img convert`](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) o el cmdlet de PowerShell [`Convert-VHD`](https://technet.microsoft.com/library/hh848454.aspx).</span><span class="sxs-lookup"><span data-stu-id="6d1be-138">If needed, you can convert VHDX disks to VHD using [`qemu-img convert`](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) or the [`Convert-VHD`](https://technet.microsoft.com/library/hh848454.aspx) PowerShell cmdlet.</span></span> <span data-ttu-id="6d1be-139">Además, Azure no permite cargar VHD dinámicos, por lo que tendrá que convertir estos discos a VHD estáticos antes de cargarlos.</span><span class="sxs-lookup"><span data-stu-id="6d1be-139">Further, Azure does not support uploading dynamic VHDs, so you need to convert such disks to static VHDs before uploading.</span></span> <span data-ttu-id="6d1be-140">Puede usar herramientas como, por ejemplo, [Azure VHD Utilities for GO](https://github.com/Microsoft/azure-vhd-utils-for-go) para convertir discos dinámicos durante el proceso de carga en Azure.</span><span class="sxs-lookup"><span data-stu-id="6d1be-140">You can use tools such as [Azure VHD Utilities for GO](https://github.com/Microsoft/azure-vhd-utils-for-go) to convert dynamic disks during the process of uploading to Azure.</span></span>
> 
> 

* <span data-ttu-id="6d1be-141">Las máquinas virtuales creadas desde el disco personalizado deben residir en la misma cuenta de almacenamiento que el propio disco.</span><span class="sxs-lookup"><span data-stu-id="6d1be-141">VMs created from your custom disk must reside in the same storage account as the disk itself</span></span>
  * <span data-ttu-id="6d1be-142">Cree una cuenta de almacenamiento y un contenedor para almacenar el disco personalizado y las máquinas virtuales creadas.</span><span class="sxs-lookup"><span data-stu-id="6d1be-142">Create a storage account and container to hold both your custom disk and created VMs</span></span>
  * <span data-ttu-id="6d1be-143">Una vez que haya creado todas las máquinas virtuales, puede eliminar el disco de forma segura.</span><span class="sxs-lookup"><span data-stu-id="6d1be-143">After you have created all your VMs, you can safely delete your disk</span></span>

<span data-ttu-id="6d1be-144">Asegúrese de que ha instalado la última versión de la [CLI de Azure 2.0](/cli/azure/install-az-cli2) y de que ha iniciado sesión en una cuenta de Azure con [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="6d1be-144">Make sure that you have the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="6d1be-145">En los ejemplos siguientes, reemplace los nombres de parámetros de ejemplo por los suyos propios.</span><span class="sxs-lookup"><span data-stu-id="6d1be-145">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="6d1be-146">Nombres de parámetros de ejemplo incluidos `myResourceGroup`, `mystorageaccount` y `mydisks`.</span><span class="sxs-lookup"><span data-stu-id="6d1be-146">Example parameter names included `myResourceGroup`, `mystorageaccount`, and `mydisks`.</span></span>

<span data-ttu-id="6d1be-147"><a id="prepimage"> </a></span><span class="sxs-lookup"><span data-stu-id="6d1be-147"><a id="prepimage"> </a></span></span>

## <a name="prepare-the-disk-to-be-uploaded"></a><span data-ttu-id="6d1be-148">Preparación del disco que se va a cargar</span><span class="sxs-lookup"><span data-stu-id="6d1be-148">Prepare the disk to be uploaded</span></span>
<span data-ttu-id="6d1be-149">Azure admite varias distribuciones Linux (consulte [Distribuciones aprobadas](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span><span class="sxs-lookup"><span data-stu-id="6d1be-149">Azure supports various Linux distributions (see [Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span></span> <span data-ttu-id="6d1be-150">Los artículos siguientes le guiarán en el proceso de preparación de las distintas distribuciones de Linux admitidas en Azure:</span><span class="sxs-lookup"><span data-stu-id="6d1be-150">The following articles guide you through how to prepare the various Linux distributions that are supported on Azure:</span></span>

* <span data-ttu-id="6d1be-151">**[Distribuciones basadas en CentOS](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="6d1be-151">**[CentOS-based Distributions](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="6d1be-152">**[Debian Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="6d1be-152">**[Debian Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="6d1be-153">**[Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="6d1be-153">**[Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="6d1be-154">**[Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="6d1be-154">**[Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="6d1be-155">**[SLES y openSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="6d1be-155">**[SLES & openSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="6d1be-156">**[Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="6d1be-156">**[Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="6d1be-157">**[Otras distribuciones no aprobadas](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="6d1be-157">**[Other - Non-Endorsed Distributions](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>

<span data-ttu-id="6d1be-158">Consulte también las **[notas de instalación de Linux](create-upload-generic.md#general-linux-installation-notes)** para más sugerencias generales sobre la preparación de imágenes de Linux para Azure.</span><span class="sxs-lookup"><span data-stu-id="6d1be-158">Also see the **[Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes)** for more general tips on preparing Linux images for Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="6d1be-159">El [Acuerdo de Nivel de Servicio de la plataforma Azure](https://azure.microsoft.com/support/legal/sla/virtual-machines/) se aplica a las máquinas virtuales que ejecutan Linux solo cuando una de las distribuciones aprobadas se use con los detalles de la configuración según se indica en la sección "Versiones admitidas" en [Linux en distribuciones aprobadas por Azure](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6d1be-159">The [Azure platform SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/) applies to VMs running Linux only when one of the endorsed distributions is used with the configuration details as specified under 'Supported Versions' in [Linux on Azure-Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
> 
> 

## <a name="create-a-resource-group"></a><span data-ttu-id="6d1be-160">Crear un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="6d1be-160">Create a resource group</span></span>
<span data-ttu-id="6d1be-161">Los grupos de recursos reúnen de forma lógica todos los recursos de Azure que admiten sus máquinas virtuales, como el almacenamiento y las redes virtuales.</span><span class="sxs-lookup"><span data-stu-id="6d1be-161">Resource groups logically bring together all the Azure resources to support your virtual machines, such as the virtual networking and storage.</span></span> <span data-ttu-id="6d1be-162">Para más información acerca de los grupos de recursos, consulte [Información general de Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6d1be-162">For more information resource groups, see [resource groups overview](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="6d1be-163">Antes de cargar el disco personalizado y crear máquinas virtuales, es preciso crear un grupo de recursos con [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="6d1be-163">Before uploading your custom disk and creating VMs, you first need to create a resource group with [az group create](/cli/azure/group#create).</span></span>

<span data-ttu-id="6d1be-164">En el ejemplo siguiente se crea un grupo de recursos denominado `myResourceGroup` en la ubicación `westus`:</span><span class="sxs-lookup"><span data-stu-id="6d1be-164">The following example creates a resource group named `myResourceGroup` in the `westus` location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

## <a name="create-a-storage-account"></a><span data-ttu-id="6d1be-165">Crear una cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="6d1be-165">Create a storage account</span></span>

<span data-ttu-id="6d1be-166">Cree una cuenta de almacenamiento para el disco personalizado y las máquinas virtuales con [az storage account create](/cli/azure/storage/account#create).</span><span class="sxs-lookup"><span data-stu-id="6d1be-166">Create a storage account for your custom disk and VMs with [az storage account create](/cli/azure/storage/account#create).</span></span> <span data-ttu-id="6d1be-167">Todas las máquinas virtuales que cree con discos no administrados deben estar en la misma cuenta de almacenamiento que ese disco.</span><span class="sxs-lookup"><span data-stu-id="6d1be-167">Any VMs with unmanaged disks that you create from your custom disk need to be in the same storage account as that disk.</span></span> 

<span data-ttu-id="6d1be-168">En el ejemplo siguiente se crea una cuenta de almacenamiento denominada `mystorageaccount` en el grupo de recursos que creó anteriormente:</span><span class="sxs-lookup"><span data-stu-id="6d1be-168">The following example creates a storage account named `mystorageaccount` in the resource group previously created:</span></span>

```azurecli
az storage account create --resource-group myResourceGroup --location westus \
  --name mystorageaccount --kind Storage --sku Standard_LRS
```

## <a name="list-storage-account-keys"></a><span data-ttu-id="6d1be-169">Enumerar claves de cuentas de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="6d1be-169">List storage account keys</span></span>
<span data-ttu-id="6d1be-170">Azure genera dos claves de acceso de 512 bits para cada cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="6d1be-170">Azure generates two 512-bit access keys for each storage account.</span></span> <span data-ttu-id="6d1be-171">Estas claves de acceso se usan al autenticar en la cuenta de almacenamiento, como la realización de operaciones de escritura.</span><span class="sxs-lookup"><span data-stu-id="6d1be-171">These access keys are used when authenticating to the storage account, such as to carry out write operations.</span></span> <span data-ttu-id="6d1be-172">Lea más sobre [administración del acceso al almacenamiento aquí](../../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="6d1be-172">Read more about [managing access to storage here](../../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span> <span data-ttu-id="6d1be-173">Vea las teclas de acceso con [az storage account keys list](/cli/azure/storage/account/keys#list).</span><span class="sxs-lookup"><span data-stu-id="6d1be-173">You view the access keys with [az storage account keys list](/cli/azure/storage/account/keys#list).</span></span>

<span data-ttu-id="6d1be-174">Consulte las claves de acceso de la cuenta de almacenamiento que ha creado:</span><span class="sxs-lookup"><span data-stu-id="6d1be-174">View the access keys for the storage account you created:</span></span>

```azurecli
az storage account keys list --resource-group myResourceGroup --account-name mystorageaccount
```

<span data-ttu-id="6d1be-175">La salida es parecida a esta:</span><span class="sxs-lookup"><span data-stu-id="6d1be-175">The output is similar to:</span></span>

```azurecli
info:    Executing command storage account keys list
+ Getting storage account keys
data:    Name  Key                                                                                       Permissions
data:    ----  ----------------------------------------------------------------------------------------  -----------
data:    key1  d4XAvZzlGAgWdvhlWfkZ9q4k9bYZkXkuPCJ15NTsQOeDeowCDAdB80r9zA/tUINApdSGQ94H9zkszYyxpe8erw==  Full
data:    key2  Ww0T7g4UyYLaBnLYcxIOTVziGAAHvU+wpwuPvK4ZG0CDFwu/mAxS/YYvAQGHocq1w7/3HcalbnfxtFdqoXOw8g==  Full
info:    storage account keys list command OK
```
<span data-ttu-id="6d1be-176">Tome nota de `key1` , pues el objetivo de su uso será interactuar con su cuenta de almacenamiento en los siguientes pasos.</span><span class="sxs-lookup"><span data-stu-id="6d1be-176">Make a note of `key1` as you will use it to interact with your storage account in the next steps.</span></span>

## <a name="create-a-storage-container"></a><span data-ttu-id="6d1be-177">Creación de un contenedor de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="6d1be-177">Create a storage container</span></span>
<span data-ttu-id="6d1be-178">De la misma manera que crea directorios distintos para organizar de forma lógica el sistema de archivos local, crea contenedores dentro de una cuenta de almacenamiento para organizar los discos.</span><span class="sxs-lookup"><span data-stu-id="6d1be-178">In the same way that you create different directories to logically organize your local file system, you create containers within a storage account to organize your disks.</span></span> <span data-ttu-id="6d1be-179">Una cuenta de almacenamiento puede contener un número cualquiera de contenedores.</span><span class="sxs-lookup"><span data-stu-id="6d1be-179">A storage account can contain any number of containers.</span></span> <span data-ttu-id="6d1be-180">Cree un contenedor con [az storage container create](/cli/azure/storage/container#create).</span><span class="sxs-lookup"><span data-stu-id="6d1be-180">Create a container with [az storage container create](/cli/azure/storage/container#create).</span></span>

<span data-ttu-id="6d1be-181">En el ejemplo siguiente se crea un contenedor llamado `mydisks`:</span><span class="sxs-lookup"><span data-stu-id="6d1be-181">The following example creates a container named `mydisks`:</span></span>

```azurecli
az storage container create \
    --account-name mystorageaccount \
    --name mydisks
```

## <a name="upload-vhd"></a><span data-ttu-id="6d1be-182">Carga de VHD</span><span class="sxs-lookup"><span data-stu-id="6d1be-182">Upload VHD</span></span>
<span data-ttu-id="6d1be-183">Ahora puede cargar su disco personalizado con [az storage blob upload](/cli/azure/storage/blob#upload).</span><span class="sxs-lookup"><span data-stu-id="6d1be-183">Now upload your custom disk with [az storage blob upload](/cli/azure/storage/blob#upload).</span></span> <span data-ttu-id="6d1be-184">Cargue y almacene el disco personalizado como un blob en páginas.</span><span class="sxs-lookup"><span data-stu-id="6d1be-184">You upload and store your custom disk as a page blob.</span></span>

<span data-ttu-id="6d1be-185">Especifique la clave de acceso, el contenedor que creó en el paso anterior y, a continuación, la ruta de acceso al disco personalizado del equipo local:</span><span class="sxs-lookup"><span data-stu-id="6d1be-185">Specify your access key, the container you created in the previous step, and then the path to the custom disk on your local computer:</span></span>

```azurecli
az storage blob upload --account-name mystorageaccount \
    --account-key key1 --container-name mydisks --type page \
    --file /path/to/disk/mydisk.vhd --name myDisk.vhd
```

## <a name="create-the-vm"></a><span data-ttu-id="6d1be-186">Creación de la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="6d1be-186">Create the VM</span></span>
<span data-ttu-id="6d1be-187">Para crear una máquina virtual con discos no administrados, especifique el URI en el disco (`--image`) con [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="6d1be-187">To create a VM with unmanaged disks, specify the URI to your disk (`--image`) with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="6d1be-188">En el ejemplo siguiente se crea una máquina virtual denominada `myVM` con el disco virtual cargado anteriormente:</span><span class="sxs-lookup"><span data-stu-id="6d1be-188">The following example creates a VM named `myVM` using the virtual disk previously uploaded:</span></span>

<span data-ttu-id="6d1be-189">Especifique el parámetro `--image` con [az vm create](/cli/azure/vm#create) para apuntar al disco personalizado.</span><span class="sxs-lookup"><span data-stu-id="6d1be-189">You specify the `--image` parameter with [az vm create](/cli/azure/vm#create) to point to your custom disk.</span></span> <span data-ttu-id="6d1be-190">Asegúrese de que `--storage-account` coincide con la cuenta de almacenamiento donde se almacena el disco personalizado.</span><span class="sxs-lookup"><span data-stu-id="6d1be-190">Ensure that `--storage-account` matches the storage account where your custom disk is stored.</span></span> <span data-ttu-id="6d1be-191">No es necesario utilizar el mismo contenedor que disco personalizado para almacenar las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="6d1be-191">You do not have to use the same container as the custom disk to store your VMs.</span></span> <span data-ttu-id="6d1be-192">Asegúrese de crear contenedores adicionales siguiendo los pasos anteriores antes de cargar el disco personalizado.</span><span class="sxs-lookup"><span data-stu-id="6d1be-192">Make sure to create any additional containers in the same way as the earlier steps before uploading your custom disk.</span></span>

<span data-ttu-id="6d1be-193">En el ejemplo siguiente se crea una máquina virtual denominada `myVM` a partir del disco personalizado:</span><span class="sxs-lookup"><span data-stu-id="6d1be-193">The following example creates a VM named `myVM` from your custom disk:</span></span>

```azurecli
az vm create --resource-group myResourceGroup --location westus \
    --name myVM --storage-account mystorageaccount --os-type linux \
    --admin-username azureuser --ssh-key-value ~/.ssh/id_rsa.pub \
    --image https://mystorageaccount.blob.core.windows.net/mydisks/myDisk.vhd \
    --use-unmanaged-disk
```

<span data-ttu-id="6d1be-194">También debe especificar todos los parámetros adicionales que requiere el comando **az vm create**, como el nombre de usuario y las claves SSH, así como responder a sus indicaciones.</span><span class="sxs-lookup"><span data-stu-id="6d1be-194">You still need to specify, or answer prompts for, all the additional parameters required by the **az vm create** command such as username and SSH keys.</span></span>


## <a name="resource-manager-template"></a><span data-ttu-id="6d1be-195">Plantilla de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="6d1be-195">Resource Manager template</span></span>
<span data-ttu-id="6d1be-196">Las plantillas de Azure Resource Manager son archivos de Notación de objetos JavaScript (JSON) que definen el entorno que desea crear.</span><span class="sxs-lookup"><span data-stu-id="6d1be-196">Azure Resource Manager templates are JavaScript Object Notation (JSON) files that define the environment you wish to build.</span></span> <span data-ttu-id="6d1be-197">Las plantillas se desglosan en distintos proveedores de recursos, tales como proceso o red.</span><span class="sxs-lookup"><span data-stu-id="6d1be-197">The templates are broken down in to different resource providers such as compute or network.</span></span> <span data-ttu-id="6d1be-198">Puede usar las plantillas existentes o escribir las suyas propias.</span><span class="sxs-lookup"><span data-stu-id="6d1be-198">You can use existing templates or write your own.</span></span> <span data-ttu-id="6d1be-199">Lea más sobre el [uso de Resource Manager y las plantillas](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6d1be-199">Read more about [using Resource Manager and templates](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="6d1be-200">Dentro del proveedor `Microsoft.Compute/virtualMachines` de la plantilla, tendrá un nodo `storageProfile` que contiene los detalles de configuración de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="6d1be-200">Within the `Microsoft.Compute/virtualMachines` provider of your template, you have a `storageProfile` node that contains the configuration details for your VM.</span></span> <span data-ttu-id="6d1be-201">Los dos parámetros principales para modificar son los URI `image` y `vhd` que apuntan al disco personalizado y el disco virtual de la nueva máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="6d1be-201">The two main parameters to edit are the `image` and `vhd` URIs that point to your custom disk and your new VM's virtual disk.</span></span> <span data-ttu-id="6d1be-202">A continuación se muestra un ejemplo de JSON para el uso de un disco personalizado:</span><span class="sxs-lookup"><span data-stu-id="6d1be-202">The following shows an example of the JSON for using a custom disk:</span></span>

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

<span data-ttu-id="6d1be-203">Puede usar [esta plantilla existente para crear una máquina virtual desde una imagen personalizada](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) o leer más sobre la [creación de sus propias plantillas de Azure Resource Manager](../../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="6d1be-203">You can use [this existing template to create a VM from a custom image](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) or read about [creating your own Azure Resource Manager templates](../../azure-resource-manager/resource-group-authoring-templates.md).</span></span> 

<span data-ttu-id="6d1be-204">Una vez que tenga una plantilla configurada, utilice [az group deployment create](/cli/azure/group/deployment#create) para crear las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="6d1be-204">Once you have a template configured, use [az group deployment create](/cli/azure/group/deployment#create) to create your VMs.</span></span> <span data-ttu-id="6d1be-205">Especifique el URI de la plantilla JSON con el parámetro `--template-uri` :</span><span class="sxs-lookup"><span data-stu-id="6d1be-205">Specify the URI of your JSON template with the `--template-uri` parameter:</span></span>

```azurecli
az group deployment create --resource-group myNewResourceGroup \
  --template-uri https://uri.to.template/mytemplate.json
```

<span data-ttu-id="6d1be-206">Si tiene un archivo JSON almacenado localmente en el equipo, puede usar el parámetro `--template-file` en su lugar:</span><span class="sxs-lookup"><span data-stu-id="6d1be-206">If you have a JSON file stored locally on your computer, you can use the `--template-file` parameter instead:</span></span>

```azurecli
az group deployment create --resource-group myNewResourceGroup \
  --template-file /path/to/mytemplate.json
```


## <a name="next-steps"></a><span data-ttu-id="6d1be-207">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6d1be-207">Next steps</span></span>
<span data-ttu-id="6d1be-208">Después de haber preparado y cargado el disco virtual personalizado, puede leer más sobre el [uso de Resource Manager y las plantillas](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6d1be-208">After you have prepared and uploaded your custom virtual disk, you can read more about [using Resource Manager and templates](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="6d1be-209">También es posible que quiera [agregar un disco de datos](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) a las nuevas máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="6d1be-209">You may also want to [add a data disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) to your new VMs.</span></span> <span data-ttu-id="6d1be-210">Si tiene aplicaciones que se ejecutan en las máquinas virtuales a las que necesite tener acceso, asegúrese de [abrir puertos y puntos de conexión](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6d1be-210">If you have applications running on your VMs that you need to access, be sure to [open ports and endpoints](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

