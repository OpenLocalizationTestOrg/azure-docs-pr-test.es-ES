---
title: aaaUpload o copia una VM de Linux personalizado con 2.0 de CLI de Azure | Documentos de Microsoft
description: "Cargar o copiar una máquina virtual personalizada utilizando el modelo de implementación del Administrador de recursos de Hola y Hola 2.0 de CLI de Azure"
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
ms.date: 07/06/2017
ms.author: cynthn
ms.openlocfilehash: 79af897120a6ba7f4a427ba6c7d0c31b7b870bd7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-linux-vm-from-custom-disk-with-hello-azure-cli-20"></a><span data-ttu-id="f3176-103">Crear una VM Linux desde disco personalizado con hello 2.0 de CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="f3176-103">Create a Linux VM from custom disk with hello Azure CLI 2.0</span></span>

<!-- rename toocreate-vm-specialized -->

<span data-ttu-id="f3176-104">Este artículo muestra cómo tooupload un disco duro virtual (VHD) personalizado o copiar un un disco duro virtual existente en Azure y crear nuevas máquinas virtuales de Linux (VM) desde el disco de saludo personalizado.</span><span class="sxs-lookup"><span data-stu-id="f3176-104">This article shows you how tooupload a customized virtual hard disk (VHD) or copy a an existing VHD in Azure and create new Linux virtual machines (VMs) from hello custom disk.</span></span> <span data-ttu-id="f3176-105">Puede instalar y configurar una distribución de Linux tooyour requisitos y, a continuación, usar ese archivo VHD tooquickly crear una nueva máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="f3176-105">You can install and configure a Linux distro tooyour requirements and then use that VHD tooquickly create a new Azure virtual machine.</span></span>

<span data-ttu-id="f3176-106">Si desea toocreate varias máquinas virtuales desde el disco personalizado, debe crear una imagen de la máquina virtual o un disco duro virtual.</span><span class="sxs-lookup"><span data-stu-id="f3176-106">If you want toocreate multiple VMs from your customized disk, you should create an image from your VM or VHD.</span></span> <span data-ttu-id="f3176-107">Para obtener más información, consulte [crear una imagen personalizada de una máquina virtual de Azure con hello CLI](tutorial-custom-images.md).</span><span class="sxs-lookup"><span data-stu-id="f3176-107">For more information, see [Create a custom image of an Azure VM using hello CLI](tutorial-custom-images.md).</span></span>

<span data-ttu-id="f3176-108">Tiene dos opciones:</span><span class="sxs-lookup"><span data-stu-id="f3176-108">You have two options:</span></span>
* [<span data-ttu-id="f3176-109">Carga de un disco duro virtual</span><span class="sxs-lookup"><span data-stu-id="f3176-109">Upload a VHD</span></span>](#option-1-upload-a-specialized-vhd)
* [<span data-ttu-id="f3176-110">Copia de una máquina virtual de Azure existente</span><span class="sxs-lookup"><span data-stu-id="f3176-110">Copy an existing Azure VM</span></span>](#option-2-copy-an-existing-azure-vm)

## <a name="quick-commands"></a><span data-ttu-id="f3176-111">Comandos rápidos</span><span class="sxs-lookup"><span data-stu-id="f3176-111">Quick commands</span></span>

<span data-ttu-id="f3176-112">Al crear una nueva máquina virtual mediante [crear vm az](/cli/azure/vm#create) desde un disco personalizado o especializado **adjuntar** disco hello (--adjuntar-os-disk) en lugar de especificar una imagen personalizada o marketplace (--imagen).</span><span class="sxs-lookup"><span data-stu-id="f3176-112">When creating a new VM using [az vm create](/cli/azure/vm#create) from a customized or specialized disk you **attach** hello disk (--attach-os-disk) instead of specifying a custom or marketplace image (--image).</span></span> <span data-ttu-id="f3176-113">Hello en el ejemplo siguiente se crea una máquina virtual denominada *myVM* mediante Hola administrado disco llamado *myManagedDisk* creado a partir de un VHD personalizado:</span><span class="sxs-lookup"><span data-stu-id="f3176-113">hello following example creates a VM named *myVM* using hello managed disk named *myManagedDisk* created from your customized VHD:</span></span>

```azurecli
az vm create --resource-group myResourceGroup --location eastus --name myVM \
   --os-type linux --attach-os-disk myManagedDisk
```

## <a name="requirements"></a><span data-ttu-id="f3176-114">Requisitos</span><span class="sxs-lookup"><span data-stu-id="f3176-114">Requirements</span></span>
<span data-ttu-id="f3176-115">Hola toocomplete siguiendo los pasos, debe:</span><span class="sxs-lookup"><span data-stu-id="f3176-115">toocomplete hello following steps, you need:</span></span>

* <span data-ttu-id="f3176-116">Una máquina virtual Linux que se ha preparado para su uso en Azure.</span><span class="sxs-lookup"><span data-stu-id="f3176-116">A Linux virtual machine that has been prepared for use in Azure.</span></span> <span data-ttu-id="f3176-117">Hola [preparar Hola VM](#prepare-the-vm) sección de este artículo trata sobre cómo toofind distribución información específica acerca de cómo instalar Hola agente de Linux de Azure (waagent) que es necesario para hello VM toowork correctamente en Azure y para toobe pueda tooconnect tooit mediante SSH.</span><span class="sxs-lookup"><span data-stu-id="f3176-117">hello [Prepare hello VM](#prepare-the-vm) section of this article covers how toofind distro specific information on installing hello Azure Linux Agent (waagent) which is required for hello VM toowork properly in Azure and for you toobe able tooconnect tooit using SSH.</span></span>
* <span data-ttu-id="f3176-118">archivo de disco duro virtual de Hello desde una existente [distribución de Linux están aprobados Azure](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (o consulte [información para las distribuciones no aprobadas](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa disco virtual en formato de disco duro virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="f3176-118">hello VHD file from an existing [Azure-endorsed Linux distribution](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (or see [information for non-endorsed distributions](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa virtual disk in hello VHD format.</span></span> <span data-ttu-id="f3176-119">Varias herramientas existen toocreate una máquina virtual y el disco duro virtual:</span><span class="sxs-lookup"><span data-stu-id="f3176-119">Multiple tools exist toocreate a VM and VHD:</span></span>
  * <span data-ttu-id="f3176-120">Instalar y configurar [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) o [KVM](http://www.linux-kvm.org/page/RunningKVM), teniendo cuidado de toouse del disco duro virtual como el formato de imagen.</span><span class="sxs-lookup"><span data-stu-id="f3176-120">Install and configure [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) or [KVM](http://www.linux-kvm.org/page/RunningKVM), taking care toouse VHD as your image format.</span></span> <span data-ttu-id="f3176-121">Si es necesario, puede [convertir una imagen](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) con **qemu-img convert**.</span><span class="sxs-lookup"><span data-stu-id="f3176-121">If needed, you can [convert an image](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) using **qemu-img convert**.</span></span>
  * <span data-ttu-id="f3176-122">También puede usar Hyper-V [en Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) o [en Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="f3176-122">You can also use Hyper-V [on Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) or [on Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="f3176-123">no se admite el formato VHDX más reciente de Hello en Azure.</span><span class="sxs-lookup"><span data-stu-id="f3176-123">hello newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="f3176-124">Cuando se crea una máquina virtual, especifique VHD como formato de Hola.</span><span class="sxs-lookup"><span data-stu-id="f3176-124">When you create a VM, specify VHD as hello format.</span></span> <span data-ttu-id="f3176-125">Si es necesario, se puede convertir VHDX discos tooVHD con [convertir img qemu](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) o hello [Convert-VHD](https://technet.microsoft.com/library/hh848454.aspx) cmdlet de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f3176-125">If needed, you can convert VHDX disks tooVHD using [qemu-img convert](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) or hello [Convert-VHD](https://technet.microsoft.com/library/hh848454.aspx) PowerShell cmdlet.</span></span> <span data-ttu-id="f3176-126">Además, Azure no permite cargar discos duros virtuales dinámicos, por lo que necesita tooconvert tal toostatic discos VHD antes de cargar.</span><span class="sxs-lookup"><span data-stu-id="f3176-126">Further, Azure does not support uploading dynamic VHDs, so you need tooconvert such disks toostatic VHDs before uploading.</span></span> <span data-ttu-id="f3176-127">Puede usar herramientas como [utilidades de disco duro virtual de Azure para ir](https://github.com/Microsoft/azure-vhd-utils-for-go) tooconvert discos dinámicos durante el proceso de Hola de carga tooAzure.</span><span class="sxs-lookup"><span data-stu-id="f3176-127">You can use tools such as [Azure VHD Utilities for GO](https://github.com/Microsoft/azure-vhd-utils-for-go) tooconvert dynamic disks during hello process of uploading tooAzure.</span></span>
> 
> 


* <span data-ttu-id="f3176-128">Asegúrese de que tiene más reciente hello [CLI de Azure 2.0](/cli/azure/install-az-cli2) instalado y registrado en tooan cuenta de Azure mediante [inicio de sesión de az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="f3176-128">Make sure that you have hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="f3176-129">En hello en los ejemplos siguientes, reemplace los nombres de parámetros de ejemplo con sus propios valores.</span><span class="sxs-lookup"><span data-stu-id="f3176-129">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="f3176-130">Los nombres de parámetro de ejemplo incluyen *myResourceGroup*, *mystorageaccount* y *mydisks*.</span><span class="sxs-lookup"><span data-stu-id="f3176-130">Example parameter names included *myResourceGroup*, *mystorageaccount*, and *mydisks*.</span></span>

<span data-ttu-id="f3176-131"><a id="prepimage"></a></span><span class="sxs-lookup"><span data-stu-id="f3176-131"><a id="prepimage"> </a></span></span>

## <a name="prepare-hello-vm"></a><span data-ttu-id="f3176-132">Preparar Hola VM</span><span class="sxs-lookup"><span data-stu-id="f3176-132">Prepare hello VM</span></span>

<span data-ttu-id="f3176-133">Azure admite varias distribuciones Linux (consulte [Distribuciones aprobadas](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span><span class="sxs-lookup"><span data-stu-id="f3176-133">Azure supports various Linux distributions (see [Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span></span> <span data-ttu-id="f3176-134">Hola siguientes artículos guiarle por cómo tooprepare Hola diversas distribuciones de Linux que se admiten en Azure:</span><span class="sxs-lookup"><span data-stu-id="f3176-134">hello following articles guide you through how tooprepare hello various Linux distributions that are supported on Azure:</span></span>

* [<span data-ttu-id="f3176-135">Distribuciones basadas en CentOS</span><span class="sxs-lookup"><span data-stu-id="f3176-135">CentOS-based Distributions</span></span>](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="f3176-136">Debian Linux</span><span class="sxs-lookup"><span data-stu-id="f3176-136">Debian Linux</span></span>](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="f3176-137">Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="f3176-137">Oracle Linux</span></span>](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="f3176-138">Red Hat Enterprise Linux</span><span class="sxs-lookup"><span data-stu-id="f3176-138">Red Hat Enterprise Linux</span></span>](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="f3176-139">SLES y openSUSE</span><span class="sxs-lookup"><span data-stu-id="f3176-139">SLES & openSUSE</span></span>](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="f3176-140">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="f3176-140">Ubuntu</span></span>](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="f3176-141">Otras distribuciones no aprobadas</span><span class="sxs-lookup"><span data-stu-id="f3176-141">Other - Non-Endorsed Distributions</span></span>](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

<span data-ttu-id="f3176-142">Consulte también hello [notas sobre la instalación de Linux](create-upload-generic.md#general-linux-installation-notes) para obtener más sugerencias sobre cómo preparar imágenes de Linux de Azure.</span><span class="sxs-lookup"><span data-stu-id="f3176-142">Also see hello [Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more general tips on preparing Linux images for Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="f3176-143">Hola [plataforma Windows Azure SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/) aplica tooVMs ejecutando Linux sólo cuando uno de hello están aprobados distribuciones se utilizan con los detalles de configuración de hello tal como se especifica en 'Admite versiones' en [Linux en Azure aprobadas Distribuciones](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f3176-143">hello [Azure platform SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/) applies tooVMs running Linux only when one of hello endorsed distributions is used with hello configuration details as specified under 'Supported Versions' in [Linux on Azure-Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
> 
> 

## <a name="option-1-upload-a-vhd"></a><span data-ttu-id="f3176-144">Opción 1: Cargar un disco duro virtual</span><span class="sxs-lookup"><span data-stu-id="f3176-144">Option 1: Upload a VHD</span></span>

<span data-ttu-id="f3176-145">Puede cargar un VHD personalizado que se esté ejecutando en un equipo local o que se haya exportado desde otra nube.</span><span class="sxs-lookup"><span data-stu-id="f3176-145">You can upload a customized VHD that you have running on a local machine or that you exported from another cloud.</span></span> <span data-ttu-id="f3176-146">toouse Hola VHD toocreate una nueva máquina virtual de Azure, necesita almacenamiento de tooa de disco duro virtual de hello tooupload cuenta y crear un disco administrado desde Hola VHD.</span><span class="sxs-lookup"><span data-stu-id="f3176-146">toouse hello VHD toocreate a new Azure VM, you need tooupload hello VHD tooa storage account and create a managed disk from hello VHD.</span></span> 

### <a name="create-a-resource-group"></a><span data-ttu-id="f3176-147">Crear un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="f3176-147">Create a resource group</span></span>

<span data-ttu-id="f3176-148">Antes de cargar el disco personalizado y crear máquinas virtuales, primero debe toocreate un grupo de recursos con [crear grupo az](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="f3176-148">Before uploading your custom disk and creating VMs, you first need toocreate a resource group with [az group create](/cli/azure/group#create).</span></span>

<span data-ttu-id="f3176-149">Hello en el ejemplo siguiente se crea un grupo de recursos denominado *myResourceGroup* en hello *eastus* ubicación: [información general de discos administrado de Azure](../windows/managed-disks-overview.md)</span><span class="sxs-lookup"><span data-stu-id="f3176-149">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location: [Azure Managed Disks overview](../windows/managed-disks-overview.md)</span></span>
```azurecli
az group create \
    --name myResourceGroup \
    --location eastus
```

### <a name="create-a-storage-account"></a><span data-ttu-id="f3176-150">Crear una cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="f3176-150">Create a storage account</span></span>

<span data-ttu-id="f3176-151">Cree una cuenta de almacenamiento para el disco personalizado y las máquinas virtuales con [az storage account create](/cli/azure/storage/account#create).</span><span class="sxs-lookup"><span data-stu-id="f3176-151">Create a storage account for your custom disk and VMs with [az storage account create](/cli/azure/storage/account#create).</span></span> 

<span data-ttu-id="f3176-152">Hello en el ejemplo siguiente se crea una cuenta de almacenamiento denominada *mystorageaccount* en grupo de recursos de hello creado anteriormente:</span><span class="sxs-lookup"><span data-stu-id="f3176-152">hello following example creates a storage account named *mystorageaccount* in hello resource group previously created:</span></span>

```azurecli
az storage account create \
    --resource-group myResourceGroup \
    --location eastus \
    --name mystorageaccount \
    --kind Storage \
    --sku Standard_LRS
```

### <a name="list-storage-account-keys"></a><span data-ttu-id="f3176-153">Enumerar claves de cuentas de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="f3176-153">List storage account keys</span></span>
<span data-ttu-id="f3176-154">Azure genera dos claves de acceso de 512 bits para cada cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="f3176-154">Azure generates two 512-bit access keys for each storage account.</span></span> <span data-ttu-id="f3176-155">Estas teclas de acceso se utilizan para autenticar la cuenta de almacenamiento toohello, al igual que lleve a cabo operaciones de escritura.</span><span class="sxs-lookup"><span data-stu-id="f3176-155">These access keys are used when authenticating toohello storage account, like carrying out write operations.</span></span> <span data-ttu-id="f3176-156">Obtenga más información sobre [administrar acceso toostorage aquí](../../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="f3176-156">Read more about [managing access toostorage here](../../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span> <span data-ttu-id="f3176-157">Ver las teclas de acceso de hello con [lista de claves de cuenta de almacenamiento az](/cli/azure/storage/account/keys#list).</span><span class="sxs-lookup"><span data-stu-id="f3176-157">You view hello access keys with [az storage account keys list](/cli/azure/storage/account/keys#list).</span></span>

<span data-ttu-id="f3176-158">Ver las teclas de acceso de Hola Hola cuenta de almacenamiento que creó:</span><span class="sxs-lookup"><span data-stu-id="f3176-158">View hello access keys for hello storage account you created:</span></span>

```azurecli
az storage account keys list \
    --resource-group myResourceGroup \
    --account-name mystorageaccount
```

<span data-ttu-id="f3176-159">es similar a la salida de Hello:</span><span class="sxs-lookup"><span data-stu-id="f3176-159">hello output is similar to:</span></span>

```azurecli
info:    Executing command storage account keys list
+ Getting storage account keys
data:    Name  Key                                                                                       Permissions
data:    ----  ----------------------------------------------------------------------------------------  -----------
data:    key1  d4XAvZzlGAgWdvhlWfkZ9q4k9bYZkXkuPCJ15NTsQOeDeowCDAdB80r9zA/tUINApdSGQ94H9zkszYyxpe8erw==  Full
data:    key2  Ww0T7g4UyYLaBnLYcxIOTVziGAAHvU+wpwuPvK4ZG0CDFwu/mAxS/YYvAQGHocq1w7/3HcalbnfxtFdqoXOw8g==  Full
info:    storage account keys list command OK
```
<span data-ttu-id="f3176-160">Tome nota del **key1** tal y como se va a utilizar se toointeract con su cuenta de almacenamiento en los pasos siguientes de Hola.</span><span class="sxs-lookup"><span data-stu-id="f3176-160">Make a note of **key1** as you will use it toointeract with your storage account in hello next steps.</span></span>

### <a name="create-a-storage-container"></a><span data-ttu-id="f3176-161">Creación de un contenedor de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="f3176-161">Create a storage container</span></span>
<span data-ttu-id="f3176-162">Hola igual que crear directorios distintos toologically organizar el sistema de archivos local, crear contenedores dentro de un tooorganize de cuenta de almacenamiento de los discos.</span><span class="sxs-lookup"><span data-stu-id="f3176-162">In hello same way that you create different directories toologically organize your local file system, you create containers within a storage account tooorganize your disks.</span></span> <span data-ttu-id="f3176-163">Una cuenta de almacenamiento puede contener un número cualquiera de contenedores.</span><span class="sxs-lookup"><span data-stu-id="f3176-163">A storage account can contain any number of containers.</span></span> <span data-ttu-id="f3176-164">Cree un contenedor con [az storage container create](/cli/azure/storage/container#create).</span><span class="sxs-lookup"><span data-stu-id="f3176-164">Create a container with [az storage container create](/cli/azure/storage/container#create).</span></span>

<span data-ttu-id="f3176-165">Hello en el ejemplo siguiente se crea un contenedor denominado *mydisks*:</span><span class="sxs-lookup"><span data-stu-id="f3176-165">hello following example creates a container named *mydisks*:</span></span>

```azurecli
az storage container create \
    --account-name mystorageaccount \
    --name mydisks
```

### <a name="upload-hello-vhd"></a><span data-ttu-id="f3176-166">Cargar Hola VHD</span><span class="sxs-lookup"><span data-stu-id="f3176-166">Upload hello VHD</span></span>
<span data-ttu-id="f3176-167">Ahora puede cargar su disco personalizado con [az storage blob upload](/cli/azure/storage/blob#upload).</span><span class="sxs-lookup"><span data-stu-id="f3176-167">Now upload your custom disk with [az storage blob upload](/cli/azure/storage/blob#upload).</span></span> <span data-ttu-id="f3176-168">Cargue y almacene el disco personalizado como un blob en páginas.</span><span class="sxs-lookup"><span data-stu-id="f3176-168">You upload and store your custom disk as a page blob.</span></span>

<span data-ttu-id="f3176-169">Especifique la clave de acceso, el contenedor de Hola que creó en el paso anterior de hello y, a continuación, Hola disco personalizado de toohello de ruta de acceso en el equipo local:</span><span class="sxs-lookup"><span data-stu-id="f3176-169">Specify your access key, hello container you created in hello previous step, and then hello path toohello custom disk on your local computer:</span></span>

```azurecli
az storage blob upload --account-name mystorageaccount \
    --account-key key1 \
    --container-name mydisks \
    --type page \
    --file /path/to/disk/mydisk.vhd \
    --name myDisk.vhd
```
<span data-ttu-id="f3176-170">Hola cargar VHD puede tardar un rato.</span><span class="sxs-lookup"><span data-stu-id="f3176-170">Uploading hello VHD may take a while.</span></span>

### <a name="create-a-managed-disk"></a><span data-ttu-id="f3176-171">Creación de un disco administrado</span><span class="sxs-lookup"><span data-stu-id="f3176-171">Create a managed disk</span></span>


<span data-ttu-id="f3176-172">Crear un disco administrado del uso de disco duro virtual de hello [crear disco az](/cli/azure/disk#create).</span><span class="sxs-lookup"><span data-stu-id="f3176-172">Create a managed disk from hello VHD using [az disk create](/cli/azure/disk#create).</span></span> <span data-ttu-id="f3176-173">Hello en el ejemplo siguiente se crea un disco administrado llamado *myManagedDisk* de hello VHD cargado tooyour denominada cuenta de almacenamiento y contenedor:</span><span class="sxs-lookup"><span data-stu-id="f3176-173">hello following example creates a managed disk named *myManagedDisk* from hello VHD you uploaded tooyour named storage account and container:</span></span>

```azurecli
az disk create \
    --resource-group myResourceGroup \
    --name myManagedDisk \
  --source https://mystorageaccount.blob.core.windows.net/mydisks/myDisk.vhd
```
## <a name="option-2-copy-an-existing-vm"></a><span data-ttu-id="f3176-174">Opción 2: Copiar una máquina virtual existente</span><span class="sxs-lookup"><span data-stu-id="f3176-174">Option 2: Copy an existing VM</span></span>

<span data-ttu-id="f3176-175">También puede crear Hola personalizada VM en Azure y, a continuación, copiar el disco de SO de Hola y adjuntarlo tooa nueva VM toocreate otra copia.</span><span class="sxs-lookup"><span data-stu-id="f3176-175">You can also create hello customized VM in Azure and then copy hello OS disk and attach it tooa new VM toocreate another copy.</span></span> <span data-ttu-id="f3176-176">Esto es correcto para la prueba, pero si desea toouse una VM de Azure existente como modelo de Hola para varias máquinas virtuales nuevas, realmente debe crear un **imagen** en su lugar.</span><span class="sxs-lookup"><span data-stu-id="f3176-176">This is fine for testing, but if you want toouse an existing Azure VM as hello model for multiple new VMs, you really should create an **image** instead.</span></span> <span data-ttu-id="f3176-177">Para obtener más información acerca de cómo crear una imagen de una máquina virtual de Azure existente, vea [crear una imagen personalizada de una máquina virtual de Azure con hello CLI](tutorial-custom-images.md)</span><span class="sxs-lookup"><span data-stu-id="f3176-177">For more information about creating an image from an existing Azure VM, see [Create a custom image of an Azure VM using hello CLI](tutorial-custom-images.md)</span></span>

### <a name="create-a-snapshot"></a><span data-ttu-id="f3176-178">Crear una instantánea</span><span class="sxs-lookup"><span data-stu-id="f3176-178">Create a snapshot</span></span>

<span data-ttu-id="f3176-179">En este ejemplo se crea una instantánea de una máquina virtual denominada *myVM* en el grupo de recursos *myResourceGroup* y se crea una instantánea denominada *osDiskSnapshot*.</span><span class="sxs-lookup"><span data-stu-id="f3176-179">This example creates a snapshot of a VM named *myVM* in resource group *myResourceGroup* and creates a snapshot named *osDiskSnapshot*.</span></span>

```azure-cli
osDiskId=$(az vm show -g myResourceGroup -n myVM --query "storageProfile.osDisk.managedDisk.id" -o tsv)
az snapshot create \
    -g myResourceGroup \
    --source "$osDiskId" \
    --name osDiskSnapshot
```
###  <a name="create-hello-managed-disk"></a><span data-ttu-id="f3176-180">Crear disco administrado Hola</span><span class="sxs-lookup"><span data-stu-id="f3176-180">Create hello managed disk</span></span>

<span data-ttu-id="f3176-181">Crear un nuevo disco administrado desde la instantánea de Hola.</span><span class="sxs-lookup"><span data-stu-id="f3176-181">Create a new managed disk from hello snapshot.</span></span>

<span data-ttu-id="f3176-182">Obtener Id. de Hola de instantánea de Hola.</span><span class="sxs-lookup"><span data-stu-id="f3176-182">Get hello ID of hello snapshot.</span></span> <span data-ttu-id="f3176-183">En este ejemplo, se denomina instantánea hello *osDiskSnapshot* y se encuentra en hello *myResourceGroup* grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="f3176-183">In this example, hello snapshot is named *osDiskSnapshot* and it is in hello *myResourceGroup* resource group.</span></span>

```azure-cli
snapshotId=$(az snapshot show --name osDiskSnapshot --resource-group myResourceGroup --query [id] -o tsv)
```

<span data-ttu-id="f3176-184">Crear disco administrado Hola.</span><span class="sxs-lookup"><span data-stu-id="f3176-184">Create hello managed disk.</span></span> <span data-ttu-id="f3176-185">En este ejemplo se va a crear un disco administrado denominado *myManagedDisk* a partir de la instantánea, que tiene un tamaño de 128 GB de almacenamiento estándar.</span><span class="sxs-lookup"><span data-stu-id="f3176-185">In this example, we will create a managed disk named *myManagedDisk* from our snapshot, that is 128GB in size in standard storage.</span></span>

```azure-cli
az disk create \
    --resource-group myResourceGroup \
    --name myManagedDisk \
    --sku Standard_LRS \
    --size-gb 128 \
    --source $snapshotId
```

## <a name="create-hello-vm"></a><span data-ttu-id="f3176-186">Crear hello VM</span><span class="sxs-lookup"><span data-stu-id="f3176-186">Create hello VM</span></span>

<span data-ttu-id="f3176-187">Ahora, cree la máquina virtual con [crear vm az](/cli/azure/vm#create) y adjuntar (--adjuntar-os-disk) Hola administrados disco como disco de SO Hola.</span><span class="sxs-lookup"><span data-stu-id="f3176-187">Now, create your VM with [az vm create](/cli/azure/vm#create) and attach (--attach-os-disk) hello managed disk as hello OS disk.</span></span> <span data-ttu-id="f3176-188">Hello en el ejemplo siguiente se crea una máquina virtual denominada *myNewVM* mediante Hola administrado disco creado a partir de su disco duro virtual cargado:</span><span class="sxs-lookup"><span data-stu-id="f3176-188">hello following example creates a VM named *myNewVM* using hello managed disk created from your uploaded VHD:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNewVM \
    --os-type linux \
    --attach-os-disk myManagedDisk
```

<span data-ttu-id="f3176-189">Debe ser capaz de tooSSH en hello VM con credenciales de Hola desde una VM de origen Hola.</span><span class="sxs-lookup"><span data-stu-id="f3176-189">You should be able tooSSH into hello VM using hello credentials from hello source VM.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="f3176-190">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f3176-190">Next steps</span></span>
<span data-ttu-id="f3176-191">Después de haber preparado y cargado el disco virtual personalizado, puede leer más sobre el [uso de Resource Manager y las plantillas](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f3176-191">After you have prepared and uploaded your custom virtual disk, you can read more about [using Resource Manager and templates](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="f3176-192">Puede que también desee demasiado[agregar un disco de datos](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooyour nuevas máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="f3176-192">You may also want too[add a data disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooyour new VMs.</span></span> <span data-ttu-id="f3176-193">Si tiene aplicaciones que se ejecutan en las máquinas virtuales que necesite tooaccess, asegúrese de demasiado[puertos abiertos y los puntos de conexión](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f3176-193">If you have applications running on your VMs that you need tooaccess, be sure too[open ports and endpoints](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

