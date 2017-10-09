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
# <a name="convert-a-linux-virtual-machine-from-unmanaged-disks-toomanaged-disks"></a>Convertir una máquina virtual Linux de discos de toomanaged de discos no administrado

Si tienes existentes máquinas virtuales (VM) de Linux que usan discos no administrados, puede convertir discos de toouse administrado de máquinas virtuales de Hola a través de hello [discos de Azure administrados](../windows/managed-disks-overview.md) servicio. Este proceso convierte disco Hola OS y los discos de datos adjunto.

Este artículo muestra cómo tooconvert máquinas virtuales mediante el uso de Hola CLI de Azure. Si necesita tooinstall o actualizarlo, consulte [instalar Azure CLI 2.0](/cli/azure/install-azure-cli). 

## <a name="before-you-begin"></a>Antes de empezar

[!INCLUDE [virtual-machines-common-convert-disks-considerations](../../../includes/virtual-machines-common-convert-disks-considerations.md)]


## <a name="convert-single-instance-vms"></a>Conversión de máquinas virtuales de instancia única
Esta sección tratan cómo tooconvert instancia única máquinas virtuales de Azure de código no discos toomanaged discos. (Si las máquinas virtuales están en un conjunto de disponibilidad, consulte la sección siguiente de Hola.) Puede usar este discos de toostandard administrado de discos de máquinas virtuales desde los discos de toopremium administrado de discos premium (SSD) no administrada, o desde estándar (HDD) no administradas de proceso tooconvert Hola.

1. Desasignar Hola VM utilizando [cancelar la asignación de máquina virtual az](/cli/azure/vm#deallocate). Hello en el ejemplo siguiente se desasigna Hola máquina virtual denominada `myVM` en grupo de recursos de hello llamado `myResourceGroup`:

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

2. Convertir discos de máquinas virtuales hello toomanaged mediante [convertir vm az](/cli/azure/vm#convert). Hola siguiendo el proceso convierte Hola máquina virtual denominada `myVM`, incluyendo disco Hola OS y los discos de datos:

    ```azurecli
    az vm convert --resource-group myResourceGroup --name myVM
    ```

3. Iniciar Hola VM después de discos de toomanaged de conversión de hello mediante [inicio de vm az](/cli/azure/vm#start). Hola siguiendo el ejemplo inicia Hola máquina virtual denominada `myVM` en grupo de recursos de hello llamado `myResourceGroup`.

    ```azurecli
    az vm start --resource-group myResourceGroup --name myVM
    ```

## <a name="convert-vms-in-an-availability-set"></a>Conversión de VM de un conjunto de disponibilidad

Si máquinas virtuales de Hola que quieres tooconvert toomanaged discos están en un conjunto de disponibilidad, primero debe tooconvert Hola disponibilidad conjunto tooa administrado conjunto de disponibilidad.

Todas las máquinas virtuales en el conjunto de disponibilidad de hello deben desasignarse antes de convertir el conjunto de disponibilidad de Hola. Tooconvert plan todos los discos de toomanaged de máquinas virtuales después de la disponibilidad de hello configurarse automáticamente ha sido convertido tooa administrado conjunto de disponibilidad. A continuación, inicie todas las máquinas virtuales de Hola y seguir funcionando con normalidad.

1. Enumere todas las máquinas virtuales de un conjunto de disponibilidad con [az vm availability-set list](/cli/azure/vm/availability-set#list). Hello en el ejemplo siguiente se enumera todas las máquinas virtuales en conjunto con nombre de la disponibilidad de hello `myAvailabilitySet` en grupo de recursos de hello llamado `myResourceGroup`:

    ```azurecli
    az vm availability-set show \
        --resource-group myResourceGroup \
        --name myAvailabilitySet \
        --query [virtualMachines[*].id] \
        --output table
    ```

2. Cancela la asignación de todas las máquinas virtuales de hello mediante el uso de [cancelar la asignación de máquina virtual az](/cli/azure/vm#deallocate). Hello en el ejemplo siguiente se desasigna Hola máquina virtual denominada `myVM` en grupo de recursos de hello llamado `myResourceGroup`:

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

3. Convertir el conjunto mediante el uso de disponibilidad de hello [convert de conjunto de disponibilidad de vm az](/cli/azure/vm/availability-set#convert). Hello en el ejemplo siguiente se convierte conjunto con nombre de la disponibilidad de hello `myAvailabilitySet` en grupo de recursos de hello llamado `myResourceGroup`:

    ```azurecli
    az vm availability-set convert \
        --resource-group myResourceGroup \
        --name myAvailabilitySet
    ```

4. Convertir todos los discos de toomanaged de las máquinas virtuales de hello mediante [convertir vm az](/cli/azure/vm#convert). Hola siguiendo el proceso convierte Hola máquina virtual denominada `myVM`, incluyendo disco Hola OS y los discos de datos:

    ```azurecli
    az vm convert --resource-group myResourceGroup --name myVM
    ```

5. Iniciar todas las máquinas virtuales de hello después de discos de toomanaged de conversión de hello mediante [inicio de vm az](/cli/azure/vm#start). Hola siguiendo el ejemplo inicia Hola máquina virtual denominada `myVM` en grupo de recursos de hello llamado `myResourceGroup`:

    ```azurecli
    az vm start --resource-group myResourceGroup --name myVM
    ```

## <a name="next-steps"></a>Pasos siguientes
Para más información sobre las opciones de almacenamiento, vea [Introducción a Azure Managed Disks](../windows/managed-disks-overview.md).
