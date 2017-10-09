---
title: disco de SO aaaExpand en VM de Linux con hello 1.0 de CLI de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooexpand Hola disco virtual del sistema operativo (SO) en una VM de Linux con hello Azure CLI 1.0 y modelo de implementación del Administrador de recursos de Hola"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 0db78c0b86b48b2c5358611e11bb0b7ad781a559
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="expand-os-disk-on-a-linux-vm-using-hello-azure-cli-with-hello-azure-cli-10"></a><span data-ttu-id="1e56c-103">Expanda el disco del sistema operativo en una VM de Linux con hello Azure CLI Hola 1.0 de CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="1e56c-103">Expand OS disk on a Linux VM using hello Azure CLI with hello Azure CLI 1.0</span></span>
<span data-ttu-id="1e56c-104">tamaño de disco duro virtual de Hello predeterminado para sistema operativo (SO) de hello suele 30 GB en una máquina virtual de Linux (VM) en Azure.</span><span class="sxs-lookup"><span data-stu-id="1e56c-104">hello default virtual hard disk size for hello operating system (OS) is typically 30 GB on a Linux virtual machine (VM) in Azure.</span></span> <span data-ttu-id="1e56c-105">También puede [agregar discos de datos](add-disk.md) tooprovide de espacio de almacenamiento adicional, pero que también le interese disco de SO hello tooexpand.</span><span class="sxs-lookup"><span data-stu-id="1e56c-105">You can [add data disks](add-disk.md) tooprovide for additional storage space, but you may also wish tooexpand hello OS disk.</span></span> <span data-ttu-id="1e56c-106">Este artículo detalla cómo tooexpand Hola OS en disco para una VM de Linux con discos no administrados con hello 1.0 de CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="1e56c-106">This article details how tooexpand hello OS disk for a Linux VM using unmanaged disks with hello Azure CLI 1.0.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="1e56c-107">Tarea CLI versiones toocomplete hello</span><span class="sxs-lookup"><span data-stu-id="1e56c-107">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="1e56c-108">Puede completar la tarea hello mediante uno de hello después de las versiones CLI:</span><span class="sxs-lookup"><span data-stu-id="1e56c-108">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="1e56c-109">[Azure 1.0 de CLI](#prerequisites) – nuestro CLI para hello clásico y recursos administración modelos de implementación (en este artículo)</span><span class="sxs-lookup"><span data-stu-id="1e56c-109">[Azure CLI 1.0](#prerequisites) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="1e56c-110">[Azure 2.0 CLI](expand-disks.md) -nuestro CLI de próxima generación para el modelo de implementación de administración de recursos de Hola</span><span class="sxs-lookup"><span data-stu-id="1e56c-110">[Azure CLI 2.0](expand-disks.md) - our next generation CLI for hello resource management deployment model</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1e56c-111">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="1e56c-111">Prerequisites</span></span>
<span data-ttu-id="1e56c-112">Necesita hello [más reciente Azure CLI 1.0](../../cli-install-nodejs.md) instalado y registrado en tooan [cuenta de Azure](https://azure.microsoft.com/pricing/free-trial/) utilizando el modo de administrador de recursos de hello como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="1e56c-112">You need hello [latest Azure CLI 1.0](../../cli-install-nodejs.md) installed and logged in tooan [Azure account](https://azure.microsoft.com/pricing/free-trial/) using hello Resource Manager mode as follows:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="1e56c-113">Hola ejemplos siguientes, reemplace los nombres de parámetros de ejemplo con sus propios valores.</span><span class="sxs-lookup"><span data-stu-id="1e56c-113">In hello following samples, replace example parameter names with your own values.</span></span> <span data-ttu-id="1e56c-114">Los nombres de parámetros de ejemplo incluyen *myResourceGroup* y *myVM*.</span><span class="sxs-lookup"><span data-stu-id="1e56c-114">Example parameter names include *myResourceGroup* and *myVM*.</span></span>

## <a name="expand-os-disk"></a><span data-ttu-id="1e56c-115">Expansión del disco del sistema operativo</span><span class="sxs-lookup"><span data-stu-id="1e56c-115">Expand OS disk</span></span>

1. <span data-ttu-id="1e56c-116">No se pueden realizar operaciones en los discos duros virtuales con hello VM ejecuta.</span><span class="sxs-lookup"><span data-stu-id="1e56c-116">Operations on virtual hard disks cannot be performed with hello VM running.</span></span> <span data-ttu-id="1e56c-117">detiene Hello en el ejemplo siguiente se y desasigna Hola máquina virtual denominada *myVM* en grupo de recursos de hello llamado *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="1e56c-117">hello following example stops and deallocates hello VM named *myVM* in hello resource group named *myResourceGroup*:</span></span>

    ```azurecli
    azure vm deallocate --resource-group myResourceGroup --name myVM
    ```

    > [!NOTE]
    > <span data-ttu-id="1e56c-118">`azure vm stop`No libere los recursos de proceso de Hola.</span><span class="sxs-lookup"><span data-stu-id="1e56c-118">`azure vm stop` does not release hello compute resources.</span></span> <span data-ttu-id="1e56c-119">toorelease recursos de proceso, use `azure vm deallocate`.</span><span class="sxs-lookup"><span data-stu-id="1e56c-119">toorelease compute resources, use `azure vm deallocate`.</span></span> <span data-ttu-id="1e56c-120">Hola VM debe desasignarse tooexpand Hola disco duro.</span><span class="sxs-lookup"><span data-stu-id="1e56c-120">hello VM must be deallocated tooexpand hello virtual hard disk.</span></span>

2. <span data-ttu-id="1e56c-121">Actualizar Hola tamaño del disco de sistema operativo de hello no administrada con hello `azure vm set` comando.</span><span class="sxs-lookup"><span data-stu-id="1e56c-121">Update hello size of hello unmanaged OS disk using hello `azure vm set` command.</span></span> <span data-ttu-id="1e56c-122">Después de las actualizaciones de ejemplo de Hola Hola máquina virtual denominada *myVM* en grupo de recursos de hello llamado *myResourceGroup* toobe *50* GB:</span><span class="sxs-lookup"><span data-stu-id="1e56c-122">hello following example updates hello VM named *myVM* in hello resource group named *myResourceGroup* toobe *50* GB:</span></span>

    ```azurecli
    azure vm set \
        --resource-group myResourceGroup \
        --name myVM \
        --new-os-disk-size 50
    ```

3. <span data-ttu-id="1e56c-123">Inicie la máquina virtual como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="1e56c-123">Start your VM as follows:</span></span>

    ```azurecli
    azure vm start --resource-group myResourceGroup --name myVM
    ```

4. <span data-ttu-id="1e56c-124">SSH tooyour VM con las credenciales adecuadas de Hola.</span><span class="sxs-lookup"><span data-stu-id="1e56c-124">SSH tooyour VM with hello appropriate credentials.</span></span> <span data-ttu-id="1e56c-125">se ha cambiado el tamaño de disco de SO hello tooverify, use `df -h`.</span><span class="sxs-lookup"><span data-stu-id="1e56c-125">tooverify hello OS disk has been resized, use `df -h`.</span></span> <span data-ttu-id="1e56c-126">Después de la salida de ejemplo de Hola muestra la partición primaria de Hola (*/dev/sda1*) ahora es de 50 GB:</span><span class="sxs-lookup"><span data-stu-id="1e56c-126">hello following example output shows hello primary partition (*/dev/sda1*) is now 50 GB:</span></span>

    ```bash
    Filesystem      Size  Used Avail Use% Mounted on
    udev            1.7G     0  1.7G   0% /dev
    tmpfs           344M  5.0M  340M   2% /run
    /dev/sda1        49G  1.3G   48G   3% /
    ```

## <a name="next-steps"></a><span data-ttu-id="1e56c-127">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1e56c-127">Next steps</span></span>
<span data-ttu-id="1e56c-128">Si necesita almacenamiento adicional, también [agregar tooa de discos de datos VM de Linux](add-disk.md).</span><span class="sxs-lookup"><span data-stu-id="1e56c-128">If you need additional storage, you also [add data disks tooa Linux VM](add-disk.md).</span></span> <span data-ttu-id="1e56c-129">Para obtener más información acerca del cifrado de disco, consulte [cifrar discos en una VM de Linux con hello Azure CLI](encrypt-disks.md).</span><span class="sxs-lookup"><span data-stu-id="1e56c-129">For more information about disk encryption, see [Encrypt disks on a Linux VM using hello Azure CLI](encrypt-disks.md).</span></span>
