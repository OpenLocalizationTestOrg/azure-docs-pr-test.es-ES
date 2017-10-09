---
title: "aaaConvert una máquina virtual de Linux en Azure de código no discos toomanaged discos - Azure administrados | Documentos de Microsoft"
description: "¿Cómo tooconvert una VM Linux de discos no administrado toomanaged discos mediante el uso de CLI de Azure 2.0 en el modelo de implementación del Administrador de recursos de Hola"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 06/23/2017
ms.author: iainfou
ms.openlocfilehash: 1b94da11deab46f344e28ab4491cf220506b6347
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="convert-a-linux-virtual-machine-from-unmanaged-disks-toomanaged-disks"></a><span data-ttu-id="37f4e-103">Convertir una máquina virtual Linux de discos de toomanaged de discos no administrado</span><span class="sxs-lookup"><span data-stu-id="37f4e-103">Convert a Linux virtual machine from unmanaged disks toomanaged disks</span></span>

<span data-ttu-id="37f4e-104">Si tienes existentes máquinas virtuales (VM) de Linux que usan discos no administrados, puede convertir discos de toouse administrado de máquinas virtuales de Hola a través de hello [discos de Azure administrados](../windows/managed-disks-overview.md) servicio.</span><span class="sxs-lookup"><span data-stu-id="37f4e-104">If you have existing Linux virtual machines (VMs) that use unmanaged disks, you can convert hello VMs toouse managed disks through hello [Azure Managed Disks](../windows/managed-disks-overview.md) service.</span></span> <span data-ttu-id="37f4e-105">Este proceso convierte disco Hola OS y los discos de datos adjunto.</span><span class="sxs-lookup"><span data-stu-id="37f4e-105">This process converts both hello OS disk and any attached data disks.</span></span>

<span data-ttu-id="37f4e-106">Este artículo muestra cómo tooconvert máquinas virtuales mediante el uso de Hola CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="37f4e-106">This article shows you how tooconvert VMs by using hello Azure CLI.</span></span> <span data-ttu-id="37f4e-107">Si necesita tooinstall o actualizarlo, consulte [instalar Azure CLI 2.0](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="37f4e-107">If you need tooinstall or upgrade it, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="37f4e-108">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="37f4e-108">Before you begin</span></span>

[!INCLUDE [virtual-machines-common-convert-disks-considerations](../../../includes/virtual-machines-common-convert-disks-considerations.md)]


## <a name="convert-single-instance-vms"></a><span data-ttu-id="37f4e-109">Conversión de máquinas virtuales de instancia única</span><span class="sxs-lookup"><span data-stu-id="37f4e-109">Convert single-instance VMs</span></span>
<span data-ttu-id="37f4e-110">Esta sección tratan cómo tooconvert instancia única máquinas virtuales de Azure de código no discos toomanaged discos.</span><span class="sxs-lookup"><span data-stu-id="37f4e-110">This section covers how tooconvert single-instance Azure VMs from unmanaged disks toomanaged disks.</span></span> <span data-ttu-id="37f4e-111">(Si las máquinas virtuales están en un conjunto de disponibilidad, consulte la sección siguiente de Hola.) Puede usar este discos de toostandard administrado de discos de máquinas virtuales desde los discos de toopremium administrado de discos premium (SSD) no administrada, o desde estándar (HDD) no administradas de proceso tooconvert Hola.</span><span class="sxs-lookup"><span data-stu-id="37f4e-111">(If your VMs are in an availability set, see hello next section.) You can use this process tooconvert hello VMs from premium (SSD) unmanaged disks toopremium managed disks, or from standard (HDD) unmanaged disks toostandard managed disks.</span></span>

1. <span data-ttu-id="37f4e-112">Desasignar Hola VM utilizando [cancelar la asignación de máquina virtual az](/cli/azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="37f4e-112">Deallocate hello VM by using [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="37f4e-113">Hello en el ejemplo siguiente se desasigna Hola máquina virtual denominada `myVM` en grupo de recursos de hello llamado `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="37f4e-113">hello following example deallocates hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

2. <span data-ttu-id="37f4e-114">Convertir discos de máquinas virtuales hello toomanaged mediante [convertir vm az](/cli/azure/vm#convert).</span><span class="sxs-lookup"><span data-stu-id="37f4e-114">Convert hello VM toomanaged disks by using [az vm convert](/cli/azure/vm#convert).</span></span> <span data-ttu-id="37f4e-115">Hola siguiendo el proceso convierte Hola máquina virtual denominada `myVM`, incluyendo disco Hola OS y los discos de datos:</span><span class="sxs-lookup"><span data-stu-id="37f4e-115">hello following process converts hello VM named `myVM`, including hello OS disk and any data disks:</span></span>

    ```azurecli
    az vm convert --resource-group myResourceGroup --name myVM
    ```

3. <span data-ttu-id="37f4e-116">Iniciar Hola VM después de discos de toomanaged de conversión de hello mediante [inicio de vm az](/cli/azure/vm#start).</span><span class="sxs-lookup"><span data-stu-id="37f4e-116">Start hello VM after hello conversion toomanaged disks by using [az vm start](/cli/azure/vm#start).</span></span> <span data-ttu-id="37f4e-117">Hola siguiendo el ejemplo inicia Hola máquina virtual denominada `myVM` en grupo de recursos de hello llamado `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="37f4e-117">hello following example starts hello VM named `myVM` in hello resource group named `myResourceGroup`.</span></span>

    ```azurecli
    az vm start --resource-group myResourceGroup --name myVM
    ```

## <a name="convert-vms-in-an-availability-set"></a><span data-ttu-id="37f4e-118">Conversión de VM de un conjunto de disponibilidad</span><span class="sxs-lookup"><span data-stu-id="37f4e-118">Convert VMs in an availability set</span></span>

<span data-ttu-id="37f4e-119">Si máquinas virtuales de Hola que quieres tooconvert toomanaged discos están en un conjunto de disponibilidad, primero debe tooconvert Hola disponibilidad conjunto tooa administrado conjunto de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="37f4e-119">If hello VMs that you want tooconvert toomanaged disks are in an availability set, you first need tooconvert hello availability set tooa managed availability set.</span></span>

<span data-ttu-id="37f4e-120">Todas las máquinas virtuales en el conjunto de disponibilidad de hello deben desasignarse antes de convertir el conjunto de disponibilidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="37f4e-120">All VMs in hello availability set must be deallocated before you convert hello availability set.</span></span> <span data-ttu-id="37f4e-121">Tooconvert plan todos los discos de toomanaged de máquinas virtuales después de la disponibilidad de hello configurarse automáticamente ha sido convertido tooa administrado conjunto de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="37f4e-121">Plan tooconvert all VMs toomanaged disks after hello availability set itself has been converted tooa managed availability set.</span></span> <span data-ttu-id="37f4e-122">A continuación, inicie todas las máquinas virtuales de Hola y seguir funcionando con normalidad.</span><span class="sxs-lookup"><span data-stu-id="37f4e-122">Then, start all hello VMs and continue operating as normal.</span></span>

1. <span data-ttu-id="37f4e-123">Enumere todas las máquinas virtuales de un conjunto de disponibilidad con [az vm availability-set list](/cli/azure/vm/availability-set#list).</span><span class="sxs-lookup"><span data-stu-id="37f4e-123">List all VMs in an availability set by using [az vm availability-set list](/cli/azure/vm/availability-set#list).</span></span> <span data-ttu-id="37f4e-124">Hello en el ejemplo siguiente se enumera todas las máquinas virtuales en conjunto con nombre de la disponibilidad de hello `myAvailabilitySet` en grupo de recursos de hello llamado `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="37f4e-124">hello following example lists all VMs in hello availability set named `myAvailabilitySet` in hello resource group named `myResourceGroup`:</span></span>

    ```azurecli
    az vm availability-set show \
        --resource-group myResourceGroup \
        --name myAvailabilitySet \
        --query [virtualMachines[*].id] \
        --output table
    ```

2. <span data-ttu-id="37f4e-125">Cancela la asignación de todas las máquinas virtuales de hello mediante el uso de [cancelar la asignación de máquina virtual az](/cli/azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="37f4e-125">Deallocate all hello VMs by using [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="37f4e-126">Hello en el ejemplo siguiente se desasigna Hola máquina virtual denominada `myVM` en grupo de recursos de hello llamado `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="37f4e-126">hello following example deallocates hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

3. <span data-ttu-id="37f4e-127">Convertir el conjunto mediante el uso de disponibilidad de hello [convert de conjunto de disponibilidad de vm az](/cli/azure/vm/availability-set#convert).</span><span class="sxs-lookup"><span data-stu-id="37f4e-127">Convert hello availability set by using [az vm availability-set convert](/cli/azure/vm/availability-set#convert).</span></span> <span data-ttu-id="37f4e-128">Hello en el ejemplo siguiente se convierte conjunto con nombre de la disponibilidad de hello `myAvailabilitySet` en grupo de recursos de hello llamado `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="37f4e-128">hello following example converts hello availability set named `myAvailabilitySet` in hello resource group named `myResourceGroup`:</span></span>

    ```azurecli
    az vm availability-set convert \
        --resource-group myResourceGroup \
        --name myAvailabilitySet
    ```

4. <span data-ttu-id="37f4e-129">Convertir todos los discos de toomanaged de las máquinas virtuales de hello mediante [convertir vm az](/cli/azure/vm#convert).</span><span class="sxs-lookup"><span data-stu-id="37f4e-129">Convert all hello VMs toomanaged disks by using [az vm convert](/cli/azure/vm#convert).</span></span> <span data-ttu-id="37f4e-130">Hola siguiendo el proceso convierte Hola máquina virtual denominada `myVM`, incluyendo disco Hola OS y los discos de datos:</span><span class="sxs-lookup"><span data-stu-id="37f4e-130">hello following process converts hello VM named `myVM`, including hello OS disk and any data disks:</span></span>

    ```azurecli
    az vm convert --resource-group myResourceGroup --name myVM
    ```

5. <span data-ttu-id="37f4e-131">Iniciar todas las máquinas virtuales de hello después de discos de toomanaged de conversión de hello mediante [inicio de vm az](/cli/azure/vm#start).</span><span class="sxs-lookup"><span data-stu-id="37f4e-131">Start all hello VMs after hello conversion toomanaged disks by using [az vm start](/cli/azure/vm#start).</span></span> <span data-ttu-id="37f4e-132">Hola siguiendo el ejemplo inicia Hola máquina virtual denominada `myVM` en grupo de recursos de hello llamado `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="37f4e-132">hello following example starts hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

    ```azurecli
    az vm start --resource-group myResourceGroup --name myVM
    ```

## <a name="next-steps"></a><span data-ttu-id="37f4e-133">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="37f4e-133">Next steps</span></span>
<span data-ttu-id="37f4e-134">Para más información sobre las opciones de almacenamiento, vea [Introducción a Azure Managed Disks](../windows/managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="37f4e-134">For more information about storage options, see [Azure Managed Disks overview](../windows/managed-disks-overview.md).</span></span>
