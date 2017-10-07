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
# <a name="how-tooexpand-virtual-hard-disks-on-a-linux-vm-with-hello-azure-cli"></a>¿Cómo tooexpand de discos duros virtuales en una VM de Linux con Hola CLI de Azure
tamaño de disco duro virtual de Hello predeterminado para sistema operativo (SO) de hello suele 30 GB en una máquina virtual de Linux (VM) en Azure. También puede [agregar discos de datos](add-disk.md) tooprovide de espacio de almacenamiento adicional, pero que también le interese tooexpand un disco de datos existente. Este artículo detalla cómo tooexpand administra los discos para una VM de Linux con hello 2.0 de CLI de Azure. También puede expandir el disco del sistema operativo hello no administrada con hello [Azure CLI 1.0](expand-disks-nodejs.md).

> [!WARNING]
> Asegúrese siempre de realizar una copia de seguridad de los datos antes de cambiar el tamaño de los discos. Para más información, consulte [Copia de seguridad de máquinas virtuales Linux en Azure](tutorial-backup-vms.md).

## <a name="expand-disk"></a>Expansión del disco
Asegúrese de que tiene más reciente hello [CLI de Azure 2.0](/cli/azure/install-az-cli2) instalado y registrado en tooan cuenta de Azure mediante [inicio de sesión de az](/cli/azure/#login).

En este artículo se requiere una máquina virtual existente en Azure con al menos un disco de datos adjunto y preparado. Si no dispone de una máquina virtual que pueda usar, consulte la sección sobre la [creación y preparación de máquinas virtuales con discos de datos](tutorial-manage-disks.md#create-and-attach-disks).

Hola ejemplos siguientes, reemplace los nombres de parámetros de ejemplo con sus propios valores. Los nombres de parámetros de ejemplo incluyen *myResourceGroup* y *myVM*.

1. No se pueden realizar operaciones en los discos duros virtuales con hello VM ejecuta. Desasigne la máquina virtual con [az vm deallocate](/cli/azure/vm#deallocate). Hello en el ejemplo siguiente se desasigna Hola máquina virtual denominada *myVM* en grupo de recursos de hello llamado *myResourceGroup*:

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

    > [!NOTE]
    > `az vm stop`No libere los recursos de proceso de Hola. toorelease recursos de proceso, use `az vm deallocate`. Hola VM debe desasignarse tooexpand Hola disco duro.

2. Vea la lista de discos administrados de un grupo de recursos con [az disk list](/cli/azure/disk#list). Hello en el ejemplo siguiente se muestra una lista de discos administrados en grupo de recursos de hello llamado *myResourceGroup*:

    ```azurecli
    az disk list \
        --resource-group myResourceGroup \
        --query '[*].{Name:name,Gb:diskSizeGb,Tier:accountType}' \
        --output table
    ```

    Expandir disco requerido de hello con [actualización de disco az](/cli/azure/disk#update). Hello en el ejemplo siguiente se amplía con el nombre de disco administrado hello *myDataDisk* toobe *200*Gb de tamaño:

    ```azurecli
    az disk update \
        --resource-group myResourceGroup \
        --name myDataDisk \
        --size-gb 200
    ```

    > [!NOTE]
    > Cuando se expande un disco administrado, tamaño de hello actualizado es toohello asignado más próximo del tamaño de disco administrado. Para una tabla de tamaños de disco administrado disponibles de Hola y niveles, vea [administrar discos información general sobre Azure - precios y facturación](../windows/managed-disks-overview.md#pricing-and-billing).

3. Inicie la máquina virtual con [az vm start](/cli/azure/vm#start). Hola siguiendo el ejemplo inicia Hola máquina virtual denominada *myVM* en grupo de recursos de hello llamado *myResourceGroup*:

    ```azurecli
    az vm start --resource-group myResourceGroup --name myVM
    ```

4. SSH tooyour VM con las credenciales adecuadas de Hola. Puede obtener la dirección IP pública de saludo de la máquina virtual con [mostrar de la máquina virtual de az](/cli/azure/vm#show):

    ```azurecli
    az vm show --resource-group myResourceGroup --name myVM -d --query [publicIps] --o tsv
    ```

5. Hola toouse expande disco, es necesario filesystem y partición de tooexpand Hola subyacente.

    a. Si ya ha montado, desmontar disco hello:

    ```bash
    sudo umount /dev/sdc1
    ```

    b. Use `parted` tooview la información de disco y cambiar el tamaño de partición de hello:

    ```bash
    sudo parted /dev/sdc
    ```

    Ver información sobre el diseño de partición existente de hello con `print`. Hola de salida es similar toohello siguiente ejemplo, que se muestra en disco subyacente hello es 215Gb en tamaño:

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

    c. Expanda la partición de hello con `resizepart`. Escriba el número de partición de hello, *1*y un tamaño para la nueva partición de hello:

    ```bash
    (parted) resizepart
    Partition number? 1
    End?  [107GB]? 215GB
    ```

    d. tooexit, escriba`quit`

5. Con la partición de hello cambia de tamaño, comprobar la coherencia de la partición de hello con `e2fsck`:

    ```bash
    sudo e2fsck -f /dev/sdc1
    ```

6. Ahora el tamaño Hola filesystem con `resize2fs`:

    ```bash
    sudo resize2fs /dev/sdc1
    ```

7. Montaje Hola partición toohello deseado ubicación, como `/datadrive`:

    ```bash
    sudo mount /dev/sdc1 /datadrive
    ```

8. se ha cambiado el tamaño de disco de SO hello tooverify, use `df -h`. Hola siguiendo la salida de ejemplo muestra la unidad de datos de hello, *sdc1/dev/*, ahora es de 200 GB:

    ```bash
    Filesystem      Size   Used  Avail Use% Mounted on
    /dev/sdc1        197G   60M   187G   1% /datadrive
    ```

## <a name="next-steps"></a>Pasos siguientes
Si necesita almacenamiento adicional, también [agregar tooa de discos de datos VM de Linux](add-disk.md). Para obtener más información acerca del cifrado de disco, consulte [cifrar discos en una VM de Linux con hello Azure CLI](encrypt-disks.md).
