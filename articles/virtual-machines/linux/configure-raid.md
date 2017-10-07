---
title: "aaaConfigure RAID de software en una máquina virtual con Linux | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse mdadm tooconfigure RAID en Linux en Azure."
services: virtual-machines-linux
documentationcenter: na
author: rickstercdn
manager: timlt
editor: tysonn
tag: azure-service-management,azure-resource-manager
ms.assetid: f3cb2786-bda6-4d2c-9aaf-2db80f490feb
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: rclaus
ms.openlocfilehash: f06e2679d953faf88ffee9991226cdb3cc1cbdb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-software-raid-on-linux"></a>Configuración del software RAID en Linux
Es un común escenario toouse RAID de software en máquinas virtuales de Linux en Azure toopresent discos varios datos adjuntos como un único dispositivo RAID. Normalmente esto puede ser usado tooimprove rendimiento y permiten una mejora en el rendimiento en comparación con toousing solo un único disco.

## <a name="attaching-data-disks"></a>Conexión de discos de datos
Dos o más discos de datos vacíos son necesario tooconfigure un dispositivo RAID.  Hola principal razón para crear un dispositivo RAID es tooimprove rendimiento de la E/S de disco.  Según sus necesidades de E/S, puede elegir tooattach discos que están almacenados en el almacenamiento estándar, con una E/S de too500/ps por disco o el almacenamiento Premium con una E/S de too5000/ps por disco. En este artículo no entra en detalles acerca de cómo tooprovision y asociar la máquina virtual de datos discos tooa Linux.  Consulte el artículo de Microsoft Azure hello [conectar un disco](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) para obtener instrucciones detalladas sobre cómo tooattach un datos vacíos disco de máquina virtual de Linux tooa en Azure.

## <a name="install-hello-mdadm-utility"></a>Instalar la utilidad de hello mdadm
* **Ubuntu**
```bash
sudo apt-get update
sudo apt-get install mdadm
```

* **CentOS y Oracle Linux**
```bash
sudo yum install mdadm
```

* **SLES y openSUSE**
```bash  
zypper install mdadm
```

## <a name="create-hello-disk-partitions"></a>Crear particiones de disco de Hola
En este ejemplo, vamos a crear una única partición de disco en /dev/sdc. nueva partición de disco Hola se llamará /dev/sdc1.

1. Iniciar `fdisk` toobegin la creación de particiones

    ```bash
    sudo fdisk /dev/sdc
    Device contains neither a valid DOS partition table, nor Sun, SGI or OSF disklabel
    Building a new DOS disklabel with disk identifier 0xa34cb70c.
    Changes will remain in memory only, until you decide toowrite them.
    After that, of course, hello previous content won't be recoverable.

    WARNING: DOS-compatible mode is deprecated. It's strongly recommended to
                    switch off hello mode (command 'c') and change display units to
                    sectors (command 'u').
    ```

2. Presione ' n ' en hello prompt toocreate una  **n** partición ew:

    ```bash
    Command (m for help): n
    ```

3. A continuación, presione "p" toocreate una **p**partición primario:

    ```bash 
    Command action
            e   extended
            p   primary partition (1-4)
    ```

4. Presione '1' número de partición de tooselect 1:

    ```bash
    Partition number (1-4): 1
    ```

5. Seleccione Hola punto inicial de la nueva partición de hello, o presione `<enter>` partición tooaccept Hola predeterminada tooplace hello en principio de Hola de espacio libre de hello en unidad de hello:

    ```bash   
    First cylinder (1-1305, default 1):
    Using default value 1
    ```

6. Seleccione Hola tamaño de partición de hello, por ejemplo el tipo '+10G' toocreate una partición de 10 gigabytes. O bien, presione `<enter>` crear una única partición que abarca la totalidad del disco hello:

    ```bash   
    Last cylinder, +cylinders or +size{K,M,G} (1-1305, default 1305): 
    Using default value 1305
    ```

7. A continuación, cambie el identificador de Hola y **t**ipo de partición de Hola desde predeterminado Hola Id. '83' (Linux) tooID 'fd' (auto de raid de Linux):

    ```bash  
    Command (m for help): t
    Selected partition 1
    Hex code (type L toolist codes): fd
    ```

8. Por último, escribir la unidad de toohello de tabla de partición de Hola y salir de fdisk:

    ```bash   
    Command (m for help): w
    hello partition table has been altered!
    ```

## <a name="create-hello-raid-array"></a>Crear la matriz RAID Hola
1. Hola después will de ejemplo "bandas" (nivel RAID 0) tres particiones ubicadas en tres discos de datos independiente (sdc1, sdd1, sde1).  Después de ejecutar este comando, se creará un nuevo dispositivo RAID llamado **/dev/md127** . Tenga en cuenta también que si estos datos discos se previamente parte de otra matriz RAID inactivo puede ser necesario tooadd hello `--force` toohello parámetro `mdadm` comando:

    ```bash  
    sudo mdadm --create /dev/md127 --level 0 --raid-devices 3 \
        /dev/sdc1 /dev/sdd1 /dev/sde1
    ```

2. Crear el sistema de archivos de hello en dispositivo RAID nuevo de Hola
   
    a. **CentOS, Oracle Linux, SLES 12, openSUSE y Ubuntu**

    ```bash   
    sudo mkfs -t ext4 /dev/md127
    ```
   
    b. **SLES 11**

    ```bash
    sudo mkfs -t ext3 /dev/md127
    ```
   
    c. **SLES 11**: habilitar boot.md y crear mdadm.conf

    ```bash
    sudo -i chkconfig --add boot.md
    sudo echo 'DEVICE /dev/sd*[0-9]' >> /etc/mdadm.conf
    ```
   
   > [!NOTE]
   > Es posible que sea necesario reiniciar después de realizar estos cambios en los sistemas SUSE. Este paso *no* es necesario en SLES 12.
   > 
   > 

## <a name="add-hello-new-file-system-tooetcfstab"></a>Agregar Hola nuevo archivo sistema demasiado/etcetera/fstab
> [!IMPORTANT]
> Incorrectamente Editar archivo/etc/fstab de hello podría provocar un reinicio del sistema. Si no está seguro, consulte la documentación de la distribución de toohello para obtener información sobre cómo tooproperly editar este archivo. También se recomienda que se crea una copia de seguridad del archivo/etc/fstab de hello antes de modificarla.

1. Crear punto de montaje de hello deseado para el nuevo sistema de archivos, por ejemplo:

    ```bash
    sudo mkdir /data
    ```
2. Al editar/etc/fstab, Hola **UUID** debe ser tooreference usado Hola sistema en lugar de hello dispositivo nombre de archivo.  Hola de uso `blkid` toodetermine Hola UUID de utilidad para el nuevo sistema de archivos de hello:

    ```bash   
    sudo /sbin/blkid
    ...........
    /dev/md127: UUID="aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee" TYPE="ext4"
    ```

3. Abra/etc/fstab en un editor de texto y agregue una entrada para el nuevo sistema de archivos hello, por ejemplo:

    ```bash   
    UUID=aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext4  defaults  0  2
    ```
   
    O bien, en **SLES 11**:

    ```bash
    /dev/disk/by-uuid/aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext3  defaults  0  2
    ```
   
    A continuación, guarde y cierre /etc/fstab.

4. Prueba que es correcta la entrada / etc/fstab hello:

    ```bash  
    sudo mount -a
    ```

    Si este comando da como resultado un mensaje de error, compruebe la sintaxis de hello en el archivo/etc/fstab de hello.
   
    A continuación ejecute hello `mount` está montado el sistema de archivos de comandos tooensure hello:

    ```bash   
    mount
    .................
    /dev/md127 on /data type ext4 (rw)
    ```

5. (Opcional) Parámetros de arranque a prueba de errores
   
    **Configuración de fstab**
   
    Número de distribuciones incluye cualquier hello `nobootwait` o `nofail` parámetros que se pueden agregar archivo toohello/etcetera/fstab de montaje. Estos parámetros permiten errores al montar un sistema de archivos determinado y permiten Hola Linux sistema toocontinue tooboot incluso si es sistema de archivos de tooproperly no se puede montar Hola RAID. Consulte la documentación de la distribución de tooyour para obtener más información acerca de estos parámetros.
   
    Ejemplo (Ubuntu):

    ```bash  
    UUID=aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext4  defaults,nobootwait  0  2
    ```   

    **Parámetros de inicio de Linux**
   
    En suma toohello por encima de los parámetros, Hola parámetro kernel "`bootdegraded=true`" pueden permitir Hola sistema tooboot incluso si Hola RAID se percibe como dañado o degradado, por ejemplo, si una unidad de datos sin darse cuenta se quita de la máquina virtual de Hola. De manera predeterminada, esto podría resultar en un sistema no iniciable.
   
    Por favor, consulte la documentación de la distribución de tooyour en cómo tooproperly editar parámetros de kernel. Por ejemplo, en muchas distribuciones (CentOS, Oracle Linux SLES 11) estos parámetros pueden agregarse manualmente toohello "`/boot/grub/menu.lst`" archivo.  En Ubuntu, ejecute este parámetro puede agregarse toohello `GRUB_CMDLINE_LINUX_DEFAULT` variable en "/ etcetera/predeterminado/grub".


## <a name="trimunmap-support"></a>Compatibilidad con TRIM y UNMAP
Algunos los kernels de Linux admiten TRIM y UNMAP operaciones toodiscard los bloques sin utilizar en el disco de Hola. Estas operaciones son sobre todo útiles en almacenamiento estándar tooinform Azure que elimina páginas ya no son válidos y se pueden descartar. El descarte de páginas puede suponer un ahorro de dinero si crea archivos grandes y, a continuación, los elimina.

> [!NOTE]
> RAID no puede emitir comandos de descarte si se establece el tamaño de fragmento de hello para la matriz de Hola que no requiere herramientas predeterminado de hello (512KB). Esto es porque Hola desasignar granularidad en hello Host también es 512KB. Si ha modificado el tamaño del fragmento de la matriz de Hola a través del mdadm `--chunk=` parámetro y, a continuación, RECORTE/anular la asignación de solicitudes pueden omitirse kernel Hola.

Hay dos maneras tooenable TRIM se admiten en la VM de Linux. Como es habitual, consulte la distribución de hello enfoque recomendado:

- Hola de uso `discard` montar opción en `/etc/fstab`, por ejemplo:

    ```bash
    UUID=aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext4  defaults,discard  0  2
    ```

- En algunos Hola casos `discard` opción podría tener implicaciones de rendimiento. Como alternativa, puede ejecutar hello `fstrim` comando manualmente desde la línea de comandos de hello, o agréguela tooyour crontab toorun con regularidad:

    **Ubuntu**

    ```bash
    # sudo apt-get install util-linux
    # sudo fstrim /data
    ```

    **RHEL/CentOS**
    ```bash
    # sudo yum install util-linux
    # sudo fstrim /data
    ```
