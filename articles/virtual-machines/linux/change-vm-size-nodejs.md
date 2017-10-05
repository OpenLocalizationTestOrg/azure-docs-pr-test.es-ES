---
title: "Cambio de tamaño de una máquina virtual Linux con la CLI de Azure 1.0 | Microsoft Docs"
description: "Escalado o reducción en vertical de una máquina virtual de Linux cambiando el tamaño de la VM."
services: virtual-machines-linux
documentationcenter: na
author: mikewasson
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/16/2016
ms.author: mwasson
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 72f5a3cd6463befd5108040ed166984281bfc5f0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="resize-a-linux-vm-with-azure-cli-10"></a><span data-ttu-id="ee575-103">Cambio de tamaño de una máquina virtual Linux con la CLI de Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="ee575-103">Resize a Linux VM with Azure CLI 1.0</span></span>

## <a name="overview"></a><span data-ttu-id="ee575-104">Información general</span><span class="sxs-lookup"><span data-stu-id="ee575-104">Overview</span></span>

<span data-ttu-id="ee575-105">Después de aprovisionar una máquina virtual (VM), puede escalarla o reducirla verticalmente cambiando su [tamaño][vm-sizes].</span><span class="sxs-lookup"><span data-stu-id="ee575-105">After you provision a virtual machine (VM), you can scale the VM up or down by changing the [VM size][vm-sizes].</span></span> <span data-ttu-id="ee575-106">En algunos casos, hay que desasignarla antes.</span><span class="sxs-lookup"><span data-stu-id="ee575-106">In some cases, you must deallocate the VM first.</span></span> <span data-ttu-id="ee575-107">Esto puede suceder si el nuevo tamaño no está disponible en el clúster de hardware que hospeda la VM.</span><span class="sxs-lookup"><span data-stu-id="ee575-107">This can happen if the new size is not available on the hardware cluster that is hosting the VM.</span></span>

<span data-ttu-id="ee575-108">Este artículo muestra cómo cambiar el tamaño de una VM de Linux mediante la [CLI de Azure][azure-cli].</span><span class="sxs-lookup"><span data-stu-id="ee575-108">This article shows how to resize a Linux VM using the [Azure CLI][azure-cli].</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="ee575-109">Versiones de la CLI para completar la tarea</span><span class="sxs-lookup"><span data-stu-id="ee575-109">CLI versions to complete the task</span></span>
<span data-ttu-id="ee575-110">Puede completar la tarea mediante una de las siguientes versiones de la CLI:</span><span class="sxs-lookup"><span data-stu-id="ee575-110">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="ee575-111">[CLI de Azure 1.0](#resize-a-linux-vm): la CLI para los modelos de implementación clásico y de Resource Manager (este artículo)</span><span class="sxs-lookup"><span data-stu-id="ee575-111">[Azure CLI 1.0](#resize-a-linux-vm) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="ee575-112">[CLI de Azure 2.0](change-vm-size.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json): la CLI de última generación para el modelo de implementación de administración de recursos</span><span class="sxs-lookup"><span data-stu-id="ee575-112">[Azure CLI 2.0](change-vm-size.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span></span>


## <a name="resize-a-linux-vm"></a><span data-ttu-id="ee575-113">Cambio de tamaño de una VM de Linux</span><span class="sxs-lookup"><span data-stu-id="ee575-113">Resize a Linux VM</span></span>
<span data-ttu-id="ee575-114">Para cambiar el tamaño de una máquina virtual, realice los pasos siguientes.</span><span class="sxs-lookup"><span data-stu-id="ee575-114">To resize a VM, perform the following steps.</span></span>

1. <span data-ttu-id="ee575-115">Ejecute el siguiente comando de la CLI:</span><span class="sxs-lookup"><span data-stu-id="ee575-115">Run the following CLI command.</span></span> <span data-ttu-id="ee575-116">Este comando muestra los tamaños de máquina virtual que están disponibles en el clúster de hardware donde se hospeda la VM.</span><span class="sxs-lookup"><span data-stu-id="ee575-116">This command lists the VM sizes that are available on the hardware cluster where the VM is hosted.</span></span>
   
    ```azurecli
    azure vm sizes -g myResourceGroup --vm-name myVM
    ```
2. <span data-ttu-id="ee575-117">Si se muestra el tamaño deseado, ejecute el comando siguiente para cambiar el tamaño de la VM.</span><span class="sxs-lookup"><span data-stu-id="ee575-117">If the desired size is listed, run the following command to resize the VM.</span></span>
   
    ```azurecli
    azure vm set -g myResourceGroup --vm-size <new-vm-size> -n myVM  \
        --enable-boot-diagnostics
        --boot-diagnostics-storage-uri https://mystorageaccount.blob.core.windows.net/ 
    ```
   
    <span data-ttu-id="ee575-118">La máquina virtual se reiniciará durante este proceso.</span><span class="sxs-lookup"><span data-stu-id="ee575-118">The VM will restart during this process.</span></span> <span data-ttu-id="ee575-119">Tras reiniciar, se reasignarán los discos del SO y de datos.</span><span class="sxs-lookup"><span data-stu-id="ee575-119">After the restart, your existing OS and data disks will be remapped.</span></span> <span data-ttu-id="ee575-120">Se perderá todo lo que haya en el disco temporal.</span><span class="sxs-lookup"><span data-stu-id="ee575-120">Anything on the temporary disk will be lost.</span></span>
   
    <span data-ttu-id="ee575-121">Al usar la opción `--enable-boot-diagnostics`, se habilita el [diagnóstico de arranque][boot-diagnostics], que permite registrar cualquier error relacionado con el inicio.</span><span class="sxs-lookup"><span data-stu-id="ee575-121">Use the `--enable-boot-diagnostics` option enables [boot diagnostics][boot-diagnostics], to log any errors related to startup.</span></span>
3. <span data-ttu-id="ee575-122">Si, por el contrario, no aparece el tamaño deseado, ejecute los siguientes comandos para desasignar la máquina virtual, cambiar su tamaño y reiniciarla.</span><span class="sxs-lookup"><span data-stu-id="ee575-122">Otherwise, if the desired size is not listed, run the following commands to deallocate the VM, resize it, and then restart the VM.</span></span>
   
    ```azurecli
    azure vm deallocate -g myResourceGroup myVM
    azure vm set -g myResourceGroup --vm-size <new-vm-size> -n myVM \
        --enable-boot-diagnostics --boot-diagnostics-storage-uri \
        https://mystorageaccount.blob.core.windows.net/ 
    azure vm start -g myResourceGroup myVM
    ```
   
   > [!WARNING]
   > <span data-ttu-id="ee575-123">Al desasignar la máquina virtual, también se liberan todas las direcciones IP dinámicas asignadas a ella.</span><span class="sxs-lookup"><span data-stu-id="ee575-123">Deallocating the VM also releases any dynamic IP addresses assigned to the VM.</span></span> <span data-ttu-id="ee575-124">Esto no afecta a los discos del SO y de datos.</span><span class="sxs-lookup"><span data-stu-id="ee575-124">The OS and data disks are not affected.</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="ee575-125">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ee575-125">Next steps</span></span>
<span data-ttu-id="ee575-126">Para obtener una mayor escalabilidad, ejecute varias instancias de VM y escálelas horizontalmente.</span><span class="sxs-lookup"><span data-stu-id="ee575-126">For additional scalability, run multiple VM instances and scale out.</span></span> <span data-ttu-id="ee575-127">Para obtener más información, consulte [Escalado automático de máquinas de Linux en un conjunto de escalado de máquinas virtuales][scale-set].</span><span class="sxs-lookup"><span data-stu-id="ee575-127">For more information, see [Automatically scale Linux machines in a Virtual Machine Scale Set][scale-set].</span></span> 

<!-- links -->

[azure-cli]:../../cli-install-nodejs.md
[boot-diagnostics]: https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/
[scale-set]: ../../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md 
[vm-sizes]:sizes.md
