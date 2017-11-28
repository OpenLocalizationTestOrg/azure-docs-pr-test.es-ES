---
title: aaaExpand de discos duros virtuales en una VM de Linux en Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooexpand de discos duros virtuales en una VM de Linux con Hola 2.0 de CLI de Azure"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/21/2017
ms.author: iainfou
ms.openlocfilehash: 7c09a682cb4322c027e57667640e8f1f8e6612f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooexpand-virtual-hard-disks-on-a-linux-vm-with-hello-azure-cli"></a><span data-ttu-id="85c59-103">¿Cómo tooexpand de discos duros virtuales en una VM de Linux con Hola CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="85c59-103">How tooexpand virtual hard disks on a Linux VM with hello Azure CLI</span></span>
<span data-ttu-id="85c59-104">tamaño de disco duro virtual de Hello predeterminado para sistema operativo (SO) de hello suele 30 GB en una máquina virtual de Linux (VM) en Azure.</span><span class="sxs-lookup"><span data-stu-id="85c59-104">hello default virtual hard disk size for hello operating system (OS) is typically 30 GB on a Linux virtual machine (VM) in Azure.</span></span> <span data-ttu-id="85c59-105">También puede [agregar discos de datos](add-disk.md) tooprovide de espacio de almacenamiento adicional, pero que también le interese tooexpand un disco de datos existente.</span><span class="sxs-lookup"><span data-stu-id="85c59-105">You can [add data disks](add-disk.md) tooprovide for additional storage space, but you may also wish tooexpand an existing data disk.</span></span> <span data-ttu-id="85c59-106">Este artículo detalla cómo tooexpand administra los discos para una VM de Linux con hello 2.0 de CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="85c59-106">This article details how tooexpand managed disks for a Linux VM with hello Azure CLI 2.0.</span></span> <span data-ttu-id="85c59-107">También puede expandir el disco del sistema operativo hello no administrada con hello [Azure CLI 1.0](expand-disks-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="85c59-107">You can also expand hello unmanaged OS disk with hello [Azure CLI 1.0](expand-disks-nodejs.md).</span></span>

> [!WARNING]
> <span data-ttu-id="85c59-108">Asegúrese siempre de realizar una copia de seguridad de los datos antes de cambiar el tamaño de los discos.</span><span class="sxs-lookup"><span data-stu-id="85c59-108">Always make sure that you back up your data before you perform disk resize operations.</span></span> <span data-ttu-id="85c59-109">Para más información, consulte [Copia de seguridad de máquinas virtuales Linux en Azure](tutorial-backup-vms.md).</span><span class="sxs-lookup"><span data-stu-id="85c59-109">For more information, see [Back up Linux VMs in Azure](tutorial-backup-vms.md).</span></span>

## <a name="expand-disk"></a><span data-ttu-id="85c59-110">Expansión del disco</span><span class="sxs-lookup"><span data-stu-id="85c59-110">Expand disk</span></span>
<span data-ttu-id="85c59-111">Asegúrese de que tiene más reciente hello [CLI de Azure 2.0](/cli/azure/install-az-cli2) instalado y registrado en tooan cuenta de Azure mediante [inicio de sesión de az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="85c59-111">Make sure that you have hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="85c59-112">En este artículo se requiere una máquina virtual existente en Azure con al menos un disco de datos adjunto y preparado.</span><span class="sxs-lookup"><span data-stu-id="85c59-112">This article requires an existing VM in Azure with at least one data disk attached and prepared.</span></span> <span data-ttu-id="85c59-113">Si no dispone de una máquina virtual que pueda usar, consulte la sección sobre la [creación y preparación de máquinas virtuales con discos de datos](tutorial-manage-disks.md#create-and-attach-disks).</span><span class="sxs-lookup"><span data-stu-id="85c59-113">If you do not already have a VM that you can use, see [Create and prepare a VM with data disks](tutorial-manage-disks.md#create-and-attach-disks).</span></span>

<span data-ttu-id="85c59-114">Hola ejemplos siguientes, reemplace los nombres de parámetros de ejemplo con sus propios valores.</span><span class="sxs-lookup"><span data-stu-id="85c59-114">In hello following samples, replace example parameter names with your own values.</span></span> <span data-ttu-id="85c59-115">Los nombres de parámetros de ejemplo incluyen *myResourceGroup* y *myVM*.</span><span class="sxs-lookup"><span data-stu-id="85c59-115">Example parameter names include *myResourceGroup* and *myVM*.</span></span>

1. <span data-ttu-id="85c59-116">No se pueden realizar operaciones en los discos duros virtuales con hello VM ejecuta.</span><span class="sxs-lookup"><span data-stu-id="85c59-116">Operations on virtual hard disks cannot be performed with hello VM running.</span></span> <span data-ttu-id="85c59-117">Desasigne la máquina virtual con [az vm deallocate](/cli/azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="85c59-117">Deallocate your VM with [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="85c59-118">Hello en el ejemplo siguiente se desasigna Hola máquina virtual denominada *myVM* en grupo de recursos de hello llamado *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="85c59-118">hello following example deallocates hello VM named *myVM* in hello resource group named *myResourceGroup*:</span></span>

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

    > [!NOTE]
    > <span data-ttu-id="85c59-119">`az vm stop`No libere los recursos de proceso de Hola.</span><span class="sxs-lookup"><span data-stu-id="85c59-119">`az vm stop` does not release hello compute resources.</span></span> <span data-ttu-id="85c59-120">toorelease recursos de proceso, use `az vm deallocate`.</span><span class="sxs-lookup"><span data-stu-id="85c59-120">toorelease compute resources, use `az vm deallocate`.</span></span> <span data-ttu-id="85c59-121">Hola VM debe desasignarse tooexpand Hola disco duro.</span><span class="sxs-lookup"><span data-stu-id="85c59-121">hello VM must be deallocated tooexpand hello virtual hard disk.</span></span>

2. <span data-ttu-id="85c59-122">Vea la lista de discos administrados de un grupo de recursos con [az disk list](/cli/azure/disk#list).</span><span class="sxs-lookup"><span data-stu-id="85c59-122">View a list of managed disks in a resource group with [az disk list](/cli/azure/disk#list).</span></span> <span data-ttu-id="85c59-123">Hello en el ejemplo siguiente se muestra una lista de discos administrados en grupo de recursos de hello llamado *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="85c59-123">hello following example displays a list of managed disks in hello resource group named *myResourceGroup*:</span></span>

    ```azurecli
    az disk list \
        --resource-group myResourceGroup \
        --query '[*].{Name:name,Gb:diskSizeGb,Tier:accountType}' \
        --output table
    ```

    <span data-ttu-id="85c59-124">Expandir disco requerido de hello con [actualización de disco az](/cli/azure/disk#update).</span><span class="sxs-lookup"><span data-stu-id="85c59-124">Expand hello required disk with [az disk update](/cli/azure/disk#update).</span></span> <span data-ttu-id="85c59-125">Hello en el ejemplo siguiente se amplía con el nombre de disco administrado hello *myDataDisk* toobe *200*Gb de tamaño:</span><span class="sxs-lookup"><span data-stu-id="85c59-125">hello following example expands hello managed disk named *myDataDisk* toobe *200*Gb in size:</span></span>

    ```azurecli
    az disk update \
        --resource-group myResourceGroup \
        --name myDataDisk \
        --size-gb 200
    ```

    > [!NOTE]
    > <span data-ttu-id="85c59-126">Cuando se expande un disco administrado, tamaño de hello actualizado es toohello asignado más próximo del tamaño de disco administrado.</span><span class="sxs-lookup"><span data-stu-id="85c59-126">When you expand a managed disk, hello updated size is mapped toohello nearest managed disk size.</span></span> <span data-ttu-id="85c59-127">Para una tabla de tamaños de disco administrado disponibles de Hola y niveles, vea [administrar discos información general sobre Azure - precios y facturación](../windows/managed-disks-overview.md#pricing-and-billing).</span><span class="sxs-lookup"><span data-stu-id="85c59-127">For a table of hello available managed disk sizes and tiers, see [Azure Managed Disks Overview - Pricing and Billing](../windows/managed-disks-overview.md#pricing-and-billing).</span></span>

3. <span data-ttu-id="85c59-128">Inicie la máquina virtual con [az vm start](/cli/azure/vm#start).</span><span class="sxs-lookup"><span data-stu-id="85c59-128">Start your VM with [az vm start](/cli/azure/vm#start).</span></span> <span data-ttu-id="85c59-129">Hola siguiendo el ejemplo inicia Hola máquina virtual denominada *myVM* en grupo de recursos de hello llamado *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="85c59-129">hello following example starts hello VM named *myVM* in hello resource group named *myResourceGroup*:</span></span>

    ```azurecli
    az vm start --resource-group myResourceGroup --name myVM
    ```

4. <span data-ttu-id="85c59-130">SSH tooyour VM con las credenciales adecuadas de Hola.</span><span class="sxs-lookup"><span data-stu-id="85c59-130">SSH tooyour VM with hello appropriate credentials.</span></span> <span data-ttu-id="85c59-131">Puede obtener la dirección IP pública de saludo de la máquina virtual con [mostrar de la máquina virtual de az](/cli/azure/vm#show):</span><span class="sxs-lookup"><span data-stu-id="85c59-131">You can obtain hello public IP address of your VM with [az vm show](/cli/azure/vm#show):</span></span>

    ```azurecli
    az vm show --resource-group myResourceGroup --name myVM -d --query [publicIps] --o tsv
    ```

5. <span data-ttu-id="85c59-132">Hola toouse expande disco, es necesario filesystem y partición de tooexpand Hola subyacente.</span><span class="sxs-lookup"><span data-stu-id="85c59-132">toouse hello expanded disk, you need tooexpand hello underlying partition and filesystem.</span></span>

    <span data-ttu-id="85c59-133">a.</span><span class="sxs-lookup"><span data-stu-id="85c59-133">a.</span></span> <span data-ttu-id="85c59-134">Si ya ha montado, desmontar disco hello:</span><span class="sxs-lookup"><span data-stu-id="85c59-134">If already mounted, unmount hello disk:</span></span>

    ```bash
    sudo umount /dev/sdc1
    ```

    <span data-ttu-id="85c59-135">b.</span><span class="sxs-lookup"><span data-stu-id="85c59-135">b.</span></span> <span data-ttu-id="85c59-136">Use `parted` tooview la información de disco y cambiar el tamaño de partición de hello:</span><span class="sxs-lookup"><span data-stu-id="85c59-136">Use `parted` tooview disk information and resize hello partition:</span></span>

    ```bash
    sudo parted /dev/sdc
    ```

    <span data-ttu-id="85c59-137">Ver información sobre el diseño de partición existente de hello con `print`.</span><span class="sxs-lookup"><span data-stu-id="85c59-137">View information about hello existing partition layout with `print`.</span></span> <span data-ttu-id="85c59-138">Hola de salida es similar toohello siguiente ejemplo, que se muestra en disco subyacente hello es 215Gb en tamaño:</span><span class="sxs-lookup"><span data-stu-id="85c59-138">hello output is similar toohello following example, which shows hello underlying disk is 215Gb in size:</span></span>

    ```bash
    GNU Parted 3.2
    Using /dev/sdc1
    Welcome tooGNU Parted! Type 'help' tooview a list of commands.
    (parted) print
    Model: Unknown Msft Virtual Disk (scsi)
    Disk /dev/sdc1: 215GB
    Sector size (logical/physical): 512B/4096B
    Partition Table: loop
    Disk Flags:
    
    Number  Start  End    Size   File system  Flags
        1      0.00B  107GB  107GB  ext4
    ```

    <span data-ttu-id="85c59-139">c.</span><span class="sxs-lookup"><span data-stu-id="85c59-139">c.</span></span> <span data-ttu-id="85c59-140">Expanda la partición de hello con `resizepart`.</span><span class="sxs-lookup"><span data-stu-id="85c59-140">Expand hello partition with `resizepart`.</span></span> <span data-ttu-id="85c59-141">Escriba el número de partición de hello, *1*y un tamaño para la nueva partición de hello:</span><span class="sxs-lookup"><span data-stu-id="85c59-141">Enter hello partition number, *1*, and a size for hello new partition:</span></span>

    ```bash
    (parted) resizepart
    Partition number? 1
    End?  [107GB]? 215GB
    ```

    <span data-ttu-id="85c59-142">d.</span><span class="sxs-lookup"><span data-stu-id="85c59-142">d.</span></span> <span data-ttu-id="85c59-143">tooexit, escriba`quit`</span><span class="sxs-lookup"><span data-stu-id="85c59-143">tooexit, enter `quit`</span></span>

5. <span data-ttu-id="85c59-144">Con la partición de hello cambia de tamaño, comprobar la coherencia de la partición de hello con `e2fsck`:</span><span class="sxs-lookup"><span data-stu-id="85c59-144">With hello partition resized, verify hello partition consistency with `e2fsck`:</span></span>

    ```bash
    sudo e2fsck -f /dev/sdc1
    ```

6. <span data-ttu-id="85c59-145">Ahora el tamaño Hola filesystem con `resize2fs`:</span><span class="sxs-lookup"><span data-stu-id="85c59-145">Now resize hello filesystem with `resize2fs`:</span></span>

    ```bash
    sudo resize2fs /dev/sdc1
    ```

7. <span data-ttu-id="85c59-146">Montaje Hola partición toohello deseado ubicación, como `/datadrive`:</span><span class="sxs-lookup"><span data-stu-id="85c59-146">Mount hello partition toohello desired location, such as `/datadrive`:</span></span>

    ```bash
    sudo mount /dev/sdc1 /datadrive
    ```

8. <span data-ttu-id="85c59-147">se ha cambiado el tamaño de disco de SO hello tooverify, use `df -h`.</span><span class="sxs-lookup"><span data-stu-id="85c59-147">tooverify hello OS disk has been resized, use `df -h`.</span></span> <span data-ttu-id="85c59-148">Hola siguiendo la salida de ejemplo muestra la unidad de datos de hello, *sdc1/dev/*, ahora es de 200 GB:</span><span class="sxs-lookup"><span data-stu-id="85c59-148">hello following example output shows hello data drive, */dev/sdc1*, is now 200 GB:</span></span>

    ```bash
    Filesystem      Size   Used  Avail Use% Mounted on
    /dev/sdc1        197G   60M   187G   1% /datadrive
    ```

## <a name="next-steps"></a><span data-ttu-id="85c59-149">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="85c59-149">Next steps</span></span>
<span data-ttu-id="85c59-150">Si necesita almacenamiento adicional, también [agregar tooa de discos de datos VM de Linux](add-disk.md).</span><span class="sxs-lookup"><span data-stu-id="85c59-150">If you need additional storage, you also [add data disks tooa Linux VM](add-disk.md).</span></span> <span data-ttu-id="85c59-151">Para obtener más información acerca del cifrado de disco, consulte [cifrar discos en una VM de Linux con hello Azure CLI](encrypt-disks.md).</span><span class="sxs-lookup"><span data-stu-id="85c59-151">For more information about disk encryption, see [Encrypt disks on a Linux VM using hello Azure CLI](encrypt-disks.md).</span></span>
