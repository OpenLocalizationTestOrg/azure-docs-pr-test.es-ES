---
title: aaaHow tooresize una VM de Linux con hello 1.0 de CLI de Azure | Documentos de Microsoft
description: "¿Cómo tooscale seguridad o reduzca verticalmente una máquina virtual de Linux, cambiando Hola tamaño de máquina virtual."
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
ms.openlocfilehash: 43dd955dc2f2dd9d1b2da07ecbfbf2459bcaa4d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="resize-a-linux-vm-with-azure-cli-10"></a><span data-ttu-id="6cb1a-103">Cambio de tamaño de una máquina virtual Linux con la CLI de Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="6cb1a-103">Resize a Linux VM with Azure CLI 1.0</span></span>

## <a name="overview"></a><span data-ttu-id="6cb1a-104">Información general</span><span class="sxs-lookup"><span data-stu-id="6cb1a-104">Overview</span></span>

<span data-ttu-id="6cb1a-105">Después de aprovisionar una máquina virtual (VM), puede escalar Hola VM hacia arriba o hacia abajo cambiando hello [tamaño de máquina virtual][vm-sizes].</span><span class="sxs-lookup"><span data-stu-id="6cb1a-105">After you provision a virtual machine (VM), you can scale hello VM up or down by changing hello [VM size][vm-sizes].</span></span> <span data-ttu-id="6cb1a-106">En algunos casos, debe desasignar Hola VM en primer lugar.</span><span class="sxs-lookup"><span data-stu-id="6cb1a-106">In some cases, you must deallocate hello VM first.</span></span> <span data-ttu-id="6cb1a-107">Esto puede ocurrir si no está disponible en clúster de hardware de Hola que hospeda Hola VM nuevo tamaño de Hola.</span><span class="sxs-lookup"><span data-stu-id="6cb1a-107">This can happen if hello new size is not available on hello hardware cluster that is hosting hello VM.</span></span>

<span data-ttu-id="6cb1a-108">Este artículo se muestra cómo tooresize una VM de Linux con hello [CLI de Azure][azure-cli].</span><span class="sxs-lookup"><span data-stu-id="6cb1a-108">This article shows how tooresize a Linux VM using hello [Azure CLI][azure-cli].</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="6cb1a-109">Tarea CLI versiones toocomplete hello</span><span class="sxs-lookup"><span data-stu-id="6cb1a-109">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="6cb1a-110">Puede completar la tarea hello mediante uno de hello después de las versiones CLI:</span><span class="sxs-lookup"><span data-stu-id="6cb1a-110">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="6cb1a-111">[Azure 1.0 de CLI](#resize-a-linux-vm) – nuestro CLI para hello clásico y recursos administración modelos de implementación (en este artículo)</span><span class="sxs-lookup"><span data-stu-id="6cb1a-111">[Azure CLI 1.0](#resize-a-linux-vm) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="6cb1a-112">[Azure 2.0 CLI](change-vm-size.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -nuestro CLI de próxima generación para el modelo de implementación de administración de recursos de Hola</span><span class="sxs-lookup"><span data-stu-id="6cb1a-112">[Azure CLI 2.0](change-vm-size.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>


## <a name="resize-a-linux-vm"></a><span data-ttu-id="6cb1a-113">Cambio de tamaño de una VM de Linux</span><span class="sxs-lookup"><span data-stu-id="6cb1a-113">Resize a Linux VM</span></span>
<span data-ttu-id="6cb1a-114">tooresize una máquina virtual, realice Hola pasos.</span><span class="sxs-lookup"><span data-stu-id="6cb1a-114">tooresize a VM, perform hello following steps.</span></span>

1. <span data-ttu-id="6cb1a-115">Ejecute el siguiente comando CLI de Hola.</span><span class="sxs-lookup"><span data-stu-id="6cb1a-115">Run hello following CLI command.</span></span> <span data-ttu-id="6cb1a-116">Este comando muestra los tamaños de máquinas virtuales de Hola que están disponibles en el clúster de hardware de Hola donde hello VM se hospeda.</span><span class="sxs-lookup"><span data-stu-id="6cb1a-116">This command lists hello VM sizes that are available on hello hardware cluster where hello VM is hosted.</span></span>
   
    ```azurecli
    azure vm sizes -g myResourceGroup --vm-name myVM
    ```
2. <span data-ttu-id="6cb1a-117">Si Hola deseado se muestra el tamaño, ejecute hello después comando tooresize hello VM.</span><span class="sxs-lookup"><span data-stu-id="6cb1a-117">If hello desired size is listed, run hello following command tooresize hello VM.</span></span>
   
    ```azurecli
    azure vm set -g myResourceGroup --vm-size <new-vm-size> -n myVM  \
        --enable-boot-diagnostics
        --boot-diagnostics-storage-uri https://mystorageaccount.blob.core.windows.net/ 
    ```
   
    <span data-ttu-id="6cb1a-118">Hola VM se reiniciará durante este proceso.</span><span class="sxs-lookup"><span data-stu-id="6cb1a-118">hello VM will restart during this process.</span></span> <span data-ttu-id="6cb1a-119">Después del reinicio de hello, el sistema operativo existente y los discos de datos se volverán a asignar.</span><span class="sxs-lookup"><span data-stu-id="6cb1a-119">After hello restart, your existing OS and data disks will be remapped.</span></span> <span data-ttu-id="6cb1a-120">Cualquier cosa en disco temporal de Hola se perderá.</span><span class="sxs-lookup"><span data-stu-id="6cb1a-120">Anything on hello temporary disk will be lost.</span></span>
   
    <span data-ttu-id="6cb1a-121">Hola de uso `--enable-boot-diagnostics` opción habilita [diagnósticos de arranque][boot-diagnostics], toolog cualquier toostartup relacionados con errores.</span><span class="sxs-lookup"><span data-stu-id="6cb1a-121">Use hello `--enable-boot-diagnostics` option enables [boot diagnostics][boot-diagnostics], toolog any errors related toostartup.</span></span>
3. <span data-ttu-id="6cb1a-122">En caso contrario, si Hola deseado no se especifica tamaño, ejecute hello siga los comandos toodeallocate Hola VM, cambiar su tamaño y, a continuación, reiniciar Hola VM.</span><span class="sxs-lookup"><span data-stu-id="6cb1a-122">Otherwise, if hello desired size is not listed, run hello following commands toodeallocate hello VM, resize it, and then restart hello VM.</span></span>
   
    ```azurecli
    azure vm deallocate -g myResourceGroup myVM
    azure vm set -g myResourceGroup --vm-size <new-vm-size> -n myVM \
        --enable-boot-diagnostics --boot-diagnostics-storage-uri \
        https://mystorageaccount.blob.core.windows.net/ 
    azure vm start -g myResourceGroup myVM
    ```
   
   > [!WARNING]
   > <span data-ttu-id="6cb1a-123">Hola desasignar VM también libera todas las direcciones IP dinámicas asignadas toohello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="6cb1a-123">Deallocating hello VM also releases any dynamic IP addresses assigned toohello VM.</span></span> <span data-ttu-id="6cb1a-124">Hola OS y discos de datos no se ven afectados.</span><span class="sxs-lookup"><span data-stu-id="6cb1a-124">hello OS and data disks are not affected.</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="6cb1a-125">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6cb1a-125">Next steps</span></span>
<span data-ttu-id="6cb1a-126">Para obtener una mayor escalabilidad, ejecute varias instancias de VM y escálelas horizontalmente. Para obtener más información, consulte [Escalado automático de máquinas de Linux en un conjunto de escalado de máquinas virtuales][scale-set].</span><span class="sxs-lookup"><span data-stu-id="6cb1a-126">For additional scalability, run multiple VM instances and scale out. For more information, see [Automatically scale Linux machines in a Virtual Machine Scale Set][scale-set].</span></span> 

<!-- links -->

[azure-cli]:../../cli-install-nodejs.md
[boot-diagnostics]: https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/
[scale-set]: ../../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md 
[vm-sizes]:sizes.md
