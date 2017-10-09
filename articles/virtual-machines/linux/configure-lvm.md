---
title: "aaaConfigure LVM en una máquina virtual con Linux | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooconfigure LVM en Linux en Azure."
services: virtual-machines-linux
documentationcenter: na
author: szarkos
manager: timlt
editor: tysonn
tag: azure-service-management,azure-resource-manager
ms.assetid: 7f533725-1484-479d-9472-6b3098d0aecc
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: 8daf792d87c6bb3d91a2eddcd01cfab34fd28cff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-lvm-on-a-linux-vm-in-azure"></a>Configuración del LVM en una máquina virtual Linux en Azure
Este documento se describe cómo tooconfigure el Administrador de volúmenes lógicos (LVM) en la máquina virtual de Azure. Aunque es posible tooconfigure que LVM en cualquier disco conectado toohello virtual machine, de forma predeterminada en la nube mayoría imágenes no tendrán LVM configurado en hello disco del sistema operativo. Esto es tooprevent problemas con grupos de volúmenes duplicados si Hola disco del sistema operativo es alguna vez asociado tooanother VM de hello misma distribución y el tipo, es decir, durante un escenario de recuperación. Por lo tanto, se recomienda solo toouse LVM en discos de datos de Hola.

## <a name="linear-vs-striped-logical-volumes"></a>Volúmenes lógicos lineales frente a seccionados
LVM puede ser toocombine usa un número de discos físicos en un único volumen de almacenamiento. De forma predeterminada LVM suele crear volúmenes lógicos lineales, lo que significa que almacenamiento físico de Hola se concatena juntos. En este caso las operaciones de lectura/escritura normalmente solo se enviarán tooa uno de los discos. En cambio, también podemos crear un volumen seccionado lógico donde lecturas y escrituras son discos toomultiple distribuida contenidos en el grupo de volúmenes de hello (es decir, tooRAID0 similar). Por motivos de rendimiento, es probable que desee toostripe los volúmenes lógicos para que las lecturas y escrituras utilizan todos los discos de datos adjuntos.

Este documento se describe cómo toocombine datos de varios discos en un único grupo de volúmenes y, a continuación, crear un volumen seccionado lógico. Hola pasos son algo generalizado toowork con la mayoría de las distribuciones. Hola la mayoría de casos utilidades y flujos de trabajo para administrar LVM en Azure no son fundamentalmente diferentes de otros entornos. Como de costumbre, consulte a su proveedor de Linux con el fin de obtener la documentación y los procedimientos recomendados para usar el LVM en una distribución en particular.

## <a name="attaching-data-disks"></a>Conexión de discos de datos
Uno normalmente es conveniente toostart con dos o más discos de datos vacíos cuando se usa LVM. Según sus necesidades de E/S, puede elegir tooattach discos que están almacenados en el almacenamiento estándar, con una E/S de too500/ps por disco o el almacenamiento Premium con una E/S de too5000/ps por disco. En este artículo no entra en detalles acerca de cómo tooprovision y asociar la máquina virtual de datos discos tooa Linux. Vea artículo de Microsoft Azure hello [conectar un disco](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) para obtener instrucciones detalladas sobre cómo tooattach un datos vacíos disco de máquina virtual de Linux tooa en Azure.

## <a name="install-hello-lvm-utilities"></a>Instalar utilidades LVM Hola
* **Ubuntu**

    ```bash  
    sudo apt-get update
    sudo apt-get install lvm2
    ```

* **RHEL, CentOS y Oracle Linux**

    ```bash   
    sudo yum install lvm2
    ```

* **12 SLES y openSUSE**

    ```bash   
    sudo zypper install lvm2
    ```

* **SLES 11**

    ```bash   
    sudo zypper install lvm2
    ```

    En SLES11 también debe editar `/etc/sysconfig/lvm` y establecer `LVM_ACTIVATED_ON_DISCOVERED` demasiado "Habilitar":

    ```sh   
    LVM_ACTIVATED_ON_DISCOVERED="enable" 
    ```

## <a name="configure-lvm"></a>Configuración del LVM
En esta guía se presupone que ha adjuntado tres discos de datos, lo que nos referiremos tooas `/dev/sdc`, `/dev/sdd` y `/dev/sde`. Tenga en cuenta que estos pueden no ser siempre Hola mismos nombres de ruta de acceso en la máquina virtual. Puede ejecutar '`sudo fdisk -l`' o similar toolist comando los discos disponibles.

1. Preparar volúmenes físicos hello:

    ```bash    
    sudo pvcreate /dev/sd[cde]
    Physical volume "/dev/sdc" successfully created
    Physical volume "/dev/sdd" successfully created
    Physical volume "/dev/sde" successfully created
    ```

2. Cree un grupo de volúmenes. En este ejemplo estamos llamando a grupo de volúmenes de Hola `data-vg01`:

    ```bash    
    sudo vgcreate data-vg01 /dev/sd[cde]
    Volume group "data-vg01" successfully created
    ```

3. Crear volúmenes lógicos de Hola. Hello comando a continuación se creará un único volumen lógico llama `data-lv01` toospan Hola todo grupo de volumen, pero tenga en cuenta que también es posible toocreate varios volúmenes lógicos en el grupo de volúmenes de Hola.

    ```bash   
    sudo lvcreate --extents 100%FREE --stripes 3 --name data-lv01 data-vg01
    Logical volume "data-lv01" created.
    ```

4. Volumen lógico de Hola de formato

    ```bash  
    sudo mkfs -t ext4 /dev/data-vg01/data-lv01
    ```
   
   > [!NOTE]
   > En SLES11, utilice `-t ext3` en vez de ext4. SLES11 sólo es compatible con sistemas de archivos de tooext4 de acceso de solo lectura.

## <a name="add-hello-new-file-system-tooetcfstab"></a>Agregar Hola nuevo archivo sistema demasiado/etcetera/fstab
> [!IMPORTANT]
> Edición incorrectamente hello `/etc/fstab` archivo podría provocar un reinicio del sistema. Si no está seguro, por favor, consulte la documentación de la distribución de toohello para obtener información sobre cómo tooproperly editar este archivo. También es recomendable una copia de seguridad de hello `/etc/fstab` se crea el archivo antes de editar.

1. Crear punto de montaje de hello deseado para el nuevo sistema de archivos, por ejemplo:

    ```bash  
    sudo mkdir /data
    ```

2. Buscar ruta de acceso del volumen lógico Hola

    ```bash    
    lvdisplay
    --- Logical volume ---
    LV Path                /dev/data-vg01/data-lv01
    ....
    ```

3. Abra `/etc/fstab` en un editor de texto y agregue una entrada para el nuevo sistema de archivos hello, por ejemplo:

    ```bash    
    /dev/data-vg01/data-lv01  /data  ext4  defaults  0  2
    ```   
    A continuación, guarde y cierre `/etc/fstab`.

4. Probar esa hello `/etc/fstab` es correcta la entrada:

    ```bash    
    sudo mount -a
    ```

    Si este comando da como resultado un mensaje de error Compruebe la sintaxis de Hola Hola `/etc/fstab` archivo.
   
    A continuación ejecute hello `mount` está montado el sistema de archivos de comandos tooensure hello:

    ```bash    
    mount
    ......
    /dev/mapper/data--vg01-data--lv01 on /data type ext4 (rw)
    ```

5. (Opcional) Parámetros de arranque a prueba de errores en `/etc/fstab`
   
    Número de distribuciones incluye cualquier hello `nobootwait` o `nofail` montar los parámetros que se pueden agregar toohello `/etc/fstab` archivo. Estos parámetros permiten errores al montar un sistema de archivos determinado y permiten Hola Linux sistema toocontinue tooboot incluso si es sistema de archivos de tooproperly no se puede montar Hola RAID. Por favor, consulte la documentación de la distribución de tooyour para obtener más información acerca de estos parámetros.
   
    Ejemplo (Ubuntu):

    ```bash 
    /dev/data-vg01/data-lv01  /data  ext4  defaults,nobootwait  0  2
    ```

## <a name="trimunmap-support"></a>Compatibilidad con TRIM y UNMAP
Algunos los kernels de Linux admiten TRIM y UNMAP operaciones toodiscard los bloques sin utilizar en el disco de Hola. Estas operaciones son sobre todo útiles en almacenamiento estándar tooinform Azure que elimina páginas ya no son válidos y se pueden descartar. El descarte de páginas puede suponer un ahorro de dinero si crea archivos grandes y, a continuación, los elimina.

Hay dos maneras tooenable TRIM se admiten en la VM de Linux. Como es habitual, consulte la distribución de hello enfoque recomendado:

- Hola de uso `discard` montar opción en `/etc/fstab`, por ejemplo:

    ```bash 
    /dev/data-vg01/data-lv01  /data  ext4  defaults,discard  0  2
    ```

- En algunos Hola casos `discard` opción podría tener implicaciones de rendimiento. Como alternativa, puede ejecutar hello `fstrim` comando manualmente desde la línea de comandos de hello, o agréguela tooyour crontab toorun con regularidad:

    **Ubuntu**

    ```bash 
    # sudo apt-get install util-linux
    # sudo fstrim /datadrive
    ```

    **RHEL/CentOS**

    ```bash 
    # sudo yum install util-linux
    # sudo fstrim /datadrive
    ```
