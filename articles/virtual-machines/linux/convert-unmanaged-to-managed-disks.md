---
title: "Conversión de una máquina virtual Linux en Azure con discos no administrados a discos administrados - Azure Managed Disks | Microsoft Docs"
description: "Conversión de una máquina virtual Linux con discos no administrados en discos administrados mediante la CLI de Azure 2.0 en el modelo de implementación de Resource Manager"
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
ms.openlocfilehash: 94f8e3330fb2d6547811315fcfdb8ced338e0247
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="convert-a-linux-virtual-machine-from-unmanaged-disks-to-managed-disks"></a><span data-ttu-id="668e8-103">Conversión de una máquina virtual Linux con discos no administrados en discos administrados</span><span class="sxs-lookup"><span data-stu-id="668e8-103">Convert a Linux virtual machine from unmanaged disks to managed disks</span></span>

<span data-ttu-id="668e8-104">Si ya dispone de máquinas virtuales Linux que usan discos no administrados, puede convertirlas para usar discos administrados mediante el servicio [Azure Managed Disks](../windows/managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="668e8-104">If you have existing Linux virtual machines (VMs) that use unmanaged disks, you can convert the VMs to use managed disks through the [Azure Managed Disks](../windows/managed-disks-overview.md) service.</span></span> <span data-ttu-id="668e8-105">Este proceso convierte el disco del SO y los discos de datos conectados.</span><span class="sxs-lookup"><span data-stu-id="668e8-105">This process converts both the OS disk and any attached data disks.</span></span>

<span data-ttu-id="668e8-106">En este artículo se muestra cómo convertir máquinas virtuales con la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="668e8-106">This article shows you how to convert VMs by using the Azure CLI.</span></span> <span data-ttu-id="668e8-107">Si necesita instalarla o actualizarla, consulte [Instalación de la CLI de Azure 2.0](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="668e8-107">If you need to install or upgrade it, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="668e8-108">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="668e8-108">Before you begin</span></span>

[!INCLUDE [virtual-machines-common-convert-disks-considerations](../../../includes/virtual-machines-common-convert-disks-considerations.md)]


## <a name="convert-single-instance-vms"></a><span data-ttu-id="668e8-109">Conversión de máquinas virtuales de instancia única</span><span class="sxs-lookup"><span data-stu-id="668e8-109">Convert single-instance VMs</span></span>
<span data-ttu-id="668e8-110">En esta sección se explica cómo convertir máquinas virtuales de Azure de instancia única de Unmanaged Disks a Managed Disks.</span><span class="sxs-lookup"><span data-stu-id="668e8-110">This section covers how to convert single-instance Azure VMs from unmanaged disks to managed disks.</span></span> <span data-ttu-id="668e8-111">(Si las máquinas virtuales se encuentran en un conjunto de disponibilidad, consulte la sección siguiente). Puede usar este proceso para convertir las máquinas virtuales de discos no administrados premium (SDD) a discos administrados premium, o bien de discos no administrados estándar (HDD) a discos administrados estándar.</span><span class="sxs-lookup"><span data-stu-id="668e8-111">(If your VMs are in an availability set, see the next section.) You can use this process to convert the VMs from premium (SSD) unmanaged disks to premium managed disks, or from standard (HDD) unmanaged disks to standard managed disks.</span></span>

1. <span data-ttu-id="668e8-112">Desasigne la máquina virtual mediante [az vm deallocate](/cli/azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="668e8-112">Deallocate the VM by using [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="668e8-113">En el ejemplo siguiente se desasigna la VM `myVM` en el grupo de recursos denominado `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="668e8-113">The following example deallocates the VM named `myVM` in the resource group named `myResourceGroup`:</span></span>

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

2. <span data-ttu-id="668e8-114">Convierta la máquina virtual en discos administrados con [az vm convert](/cli/azure/vm#convert).</span><span class="sxs-lookup"><span data-stu-id="668e8-114">Convert the VM to managed disks by using [az vm convert](/cli/azure/vm#convert).</span></span> <span data-ttu-id="668e8-115">El proceso siguiente convierte la máquina virtual denominada `myVM`, incluidos el disco del SO y todos los discos de datos:</span><span class="sxs-lookup"><span data-stu-id="668e8-115">The following process converts the VM named `myVM`, including the OS disk and any data disks:</span></span>

    ```azurecli
    az vm convert --resource-group myResourceGroup --name myVM
    ```

3. <span data-ttu-id="668e8-116">Inicie la máquina virtual después de la conversión a discos administrados con [az vm start](/cli/azure/vm#start).</span><span class="sxs-lookup"><span data-stu-id="668e8-116">Start the VM after the conversion to managed disks by using [az vm start](/cli/azure/vm#start).</span></span> <span data-ttu-id="668e8-117">En el ejemplo siguiente se inicia la VM llamada `myVM` en el grupo de recursos `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="668e8-117">The following example starts the VM named `myVM` in the resource group named `myResourceGroup`.</span></span>

    ```azurecli
    az vm start --resource-group myResourceGroup --name myVM
    ```

## <a name="convert-vms-in-an-availability-set"></a><span data-ttu-id="668e8-118">Conversión de VM de un conjunto de disponibilidad</span><span class="sxs-lookup"><span data-stu-id="668e8-118">Convert VMs in an availability set</span></span>

<span data-ttu-id="668e8-119">Si las VM que desea convertir en discos administrados se encuentran en un conjunto de disponibilidad, primero debe convertir el conjunto de disponibilidad en un conjunto de disponibilidad administrado.</span><span class="sxs-lookup"><span data-stu-id="668e8-119">If the VMs that you want to convert to managed disks are in an availability set, you first need to convert the availability set to a managed availability set.</span></span>

<span data-ttu-id="668e8-120">Todas las VM del conjunto de disponibilidad deben desasignarse antes de convertir el conjunto de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="668e8-120">All VMs in the availability set must be deallocated before you convert the availability set.</span></span> <span data-ttu-id="668e8-121">Planee la conversión de todas las máquinas virtuales a discos administrados después de haber convertido el propio conjunto de disponibilidad en un conjunto de disponibilidad administrado.</span><span class="sxs-lookup"><span data-stu-id="668e8-121">Plan to convert all VMs to managed disks after the availability set itself has been converted to a managed availability set.</span></span> <span data-ttu-id="668e8-122">Después, inicie todas las máquinas virtuales y siga trabajando con normalidad.</span><span class="sxs-lookup"><span data-stu-id="668e8-122">Then, start all the VMs and continue operating as normal.</span></span>

1. <span data-ttu-id="668e8-123">Enumere todas las máquinas virtuales de un conjunto de disponibilidad con [az vm availability-set list](/cli/azure/vm/availability-set#list).</span><span class="sxs-lookup"><span data-stu-id="668e8-123">List all VMs in an availability set by using [az vm availability-set list](/cli/azure/vm/availability-set#list).</span></span> <span data-ttu-id="668e8-124">En el ejemplo siguiente se enumeran todas las VM del conjunto de disponibilidad `myAvailabilitySet` en el grupo de recursos denominado `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="668e8-124">The following example lists all VMs in the availability set named `myAvailabilitySet` in the resource group named `myResourceGroup`:</span></span>

    ```azurecli
    az vm availability-set show \
        --resource-group myResourceGroup \
        --name myAvailabilitySet \
        --query [virtualMachines[*].id] \
        --output table
    ```

2. <span data-ttu-id="668e8-125">Desasigne todas las máquinas virtuales con [az vm deallocate](/cli/azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="668e8-125">Deallocate all the VMs by using [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="668e8-126">En el ejemplo siguiente se desasigna la VM `myVM` en el grupo de recursos denominado `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="668e8-126">The following example deallocates the VM named `myVM` in the resource group named `myResourceGroup`:</span></span>

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

3. <span data-ttu-id="668e8-127">Convierta el conjunto de disponibilidad con [az vm availability-set convert](/cli/azure/vm/availability-set#convert).</span><span class="sxs-lookup"><span data-stu-id="668e8-127">Convert the availability set by using [az vm availability-set convert](/cli/azure/vm/availability-set#convert).</span></span> <span data-ttu-id="668e8-128">En el ejemplo siguiente se convierte el conjunto de disponibilidad `myAvailabilitySet` en el grupo de recursos denominado `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="668e8-128">The following example converts the availability set named `myAvailabilitySet` in the resource group named `myResourceGroup`:</span></span>

    ```azurecli
    az vm availability-set convert \
        --resource-group myResourceGroup \
        --name myAvailabilitySet
    ```

4. <span data-ttu-id="668e8-129">Convierta todas las máquinas virtuales a discos administrados con [az vm convert](/cli/azure/vm#convert).</span><span class="sxs-lookup"><span data-stu-id="668e8-129">Convert all the VMs to managed disks by using [az vm convert](/cli/azure/vm#convert).</span></span> <span data-ttu-id="668e8-130">El proceso siguiente convierte la máquina virtual denominada `myVM`, incluidos el disco del SO y todos los discos de datos:</span><span class="sxs-lookup"><span data-stu-id="668e8-130">The following process converts the VM named `myVM`, including the OS disk and any data disks:</span></span>

    ```azurecli
    az vm convert --resource-group myResourceGroup --name myVM
    ```

5. <span data-ttu-id="668e8-131">Inicie todas las máquinas virtuales después de la conversión a discos administrados con [az vm start](/cli/azure/vm#start).</span><span class="sxs-lookup"><span data-stu-id="668e8-131">Start all the VMs after the conversion to managed disks by using [az vm start](/cli/azure/vm#start).</span></span> <span data-ttu-id="668e8-132">En el ejemplo siguiente se inicia la máquina virtual llamada `myVM` en el grupo de recursos `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="668e8-132">The following example starts the VM named `myVM` in the resource group named `myResourceGroup`:</span></span>

    ```azurecli
    az vm start --resource-group myResourceGroup --name myVM
    ```

## <a name="next-steps"></a><span data-ttu-id="668e8-133">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="668e8-133">Next steps</span></span>
<span data-ttu-id="668e8-134">Para más información sobre las opciones de almacenamiento, vea [Introducción a Azure Managed Disks](../windows/managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="668e8-134">For more information about storage options, see [Azure Managed Disks overview](../windows/managed-disks-overview.md).</span></span>
