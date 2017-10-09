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
# <a name="expand-os-disk-on-a-linux-vm-using-hello-azure-cli-with-hello-azure-cli-10"></a>Expanda el disco del sistema operativo en una VM de Linux con hello Azure CLI Hola 1.0 de CLI de Azure
tamaño de disco duro virtual de Hello predeterminado para sistema operativo (SO) de hello suele 30 GB en una máquina virtual de Linux (VM) en Azure. También puede [agregar discos de datos](add-disk.md) tooprovide de espacio de almacenamiento adicional, pero que también le interese disco de SO hello tooexpand. Este artículo detalla cómo tooexpand Hola OS en disco para una VM de Linux con discos no administrados con hello 1.0 de CLI de Azure.

## <a name="cli-versions-toocomplete-hello-task"></a>Tarea CLI versiones toocomplete hello
Puede completar la tarea hello mediante uno de hello después de las versiones CLI:

- [Azure 1.0 de CLI](#prerequisites) – nuestro CLI para hello clásico y recursos administración modelos de implementación (en este artículo)
- [Azure 2.0 CLI](expand-disks.md) -nuestro CLI de próxima generación para el modelo de implementación de administración de recursos de Hola

## <a name="prerequisites"></a>Requisitos previos
Necesita hello [más reciente Azure CLI 1.0](../../cli-install-nodejs.md) instalado y registrado en tooan [cuenta de Azure](https://azure.microsoft.com/pricing/free-trial/) utilizando el modo de administrador de recursos de hello como se indica a continuación:

```azurecli
azure config mode arm
```

Hola ejemplos siguientes, reemplace los nombres de parámetros de ejemplo con sus propios valores. Los nombres de parámetros de ejemplo incluyen *myResourceGroup* y *myVM*.

## <a name="expand-os-disk"></a>Expansión del disco del sistema operativo

1. No se pueden realizar operaciones en los discos duros virtuales con hello VM ejecuta. detiene Hello en el ejemplo siguiente se y desasigna Hola máquina virtual denominada *myVM* en grupo de recursos de hello llamado *myResourceGroup*:

    ```azurecli
    azure vm deallocate --resource-group myResourceGroup --name myVM
    ```

    > [!NOTE]
    > `azure vm stop`No libere los recursos de proceso de Hola. toorelease recursos de proceso, use `azure vm deallocate`. Hola VM debe desasignarse tooexpand Hola disco duro.

2. Actualizar Hola tamaño del disco de sistema operativo de hello no administrada con hello `azure vm set` comando. Después de las actualizaciones de ejemplo de Hola Hola máquina virtual denominada *myVM* en grupo de recursos de hello llamado *myResourceGroup* toobe *50* GB:

    ```azurecli
    azure vm set \
        --resource-group myResourceGroup \
        --name myVM \
        --new-os-disk-size 50
    ```

3. Inicie la máquina virtual como se indica a continuación:

    ```azurecli
    azure vm start --resource-group myResourceGroup --name myVM
    ```

4. SSH tooyour VM con las credenciales adecuadas de Hola. se ha cambiado el tamaño de disco de SO hello tooverify, use `df -h`. Después de la salida de ejemplo de Hola muestra la partición primaria de Hola (*/dev/sda1*) ahora es de 50 GB:

    ```bash
    Filesystem      Size  Used Avail Use% Mounted on
    udev            1.7G     0  1.7G   0% /dev
    tmpfs           344M  5.0M  340M   2% /run
    /dev/sda1        49G  1.3G   48G   3% /
    ```

## <a name="next-steps"></a>Pasos siguientes
Si necesita almacenamiento adicional, también [agregar tooa de discos de datos VM de Linux](add-disk.md). Para obtener más información acerca del cifrado de disco, consulte [cifrar discos en una VM de Linux con hello Azure CLI](encrypt-disks.md).
