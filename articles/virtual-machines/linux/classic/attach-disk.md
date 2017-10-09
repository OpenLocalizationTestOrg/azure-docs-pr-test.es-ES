---
title: aaaAttach un tooa de disco Linux VM en Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooattach datos de un disco tooa Linux VM mediante la implementación de hello clásico modelo e inicializar disco Hola para que esté preparada para su uso"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 4901384d-2a6f-4f46-bba0-337a348b7f87
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: c76d8479ac2b522d2b6df658cd28f242473f30ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooattach-a-data-disk-tooa-linux-virtual-machine"></a>¿Cómo tooAttach una máquina Virtual Linux tooa de disco de datos
> [!IMPORTANT] 
> Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../../../resource-manager-deployment-model.md). Este artículo tratan con modelo de implementación de hello clásico. Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola. Vea cómo demasiado[conectar un disco de datos mediante el modelo de implementación del Administrador de recursos de hello](../add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Puede adjuntar discos vacíos y los discos que contienen datos tooyour máquinas virtuales de Azure. Ambos tipos de discos son archivos .vhd que residen en una cuenta de almacenamiento de Azure. Como con la adición de cualquier equipo de Linux tooa de disco, después de conectar el disco de hello es necesario tooinitialize y darle formato para que esté preparada para su uso. Este artículo se detallan adjuntar discos vacíos y los discos que ya contiene datos tooyour máquinas virtuales, así como la toothen inicializar y formatear un disco nuevo.

> [!NOTE]
> Es una mejor toouse práctica uno o más separados toostore de discos de datos de una máquina virtual. Al crear una máquina virtual de Azure, esta cuenta con un disco para el sistema operativo y un disco temporal. **No utilice datos persistentes de hello disco temporal toostore.** Como indica el nombre de hello, proporciona solo el almacenamiento temporal. No ofrece redundancia o copias de seguridad porque no reside en el almacenamiento de Azure.
> disco temporal de Hola se suele estar a cargo Hola agente Linux de Azure y monta automáticamente demasiado**/mnt/resource** (o **/mnt** en Ubuntu imágenes). En Hola otro lado, un disco de datos podría denominarse kernel de Linux Hola algo parecido a `/dev/sdc`, y deberá toopartition, dar formato y montar este recurso. Vea hello [Guía de usuario de agente de Linux de Azure] [ Agent] para obtener más información.
> 
> 

[!INCLUDE [howto-attach-disk-windows-linux](../../../../includes/howto-attach-disk-linux.md)]

## <a name="initialize-a-new-data-disk-in-linux"></a>un nuevo disco de datos en Linux
1. SSH tooyour máquina virtual. Para obtener más información, consulte [cómo toolog en la máquina virtual de tooa ejecutan Linux][Logon].
2. A continuación debe identificador de dispositivo de hello toofind para tooinitialize de disco de datos de Hola. Hay dos toodo de maneras que:
   
    a) registros de Grep para los dispositivos SCSI en hello, como se muestra en el siguiente comando de hello:
   
    ```bash
    sudo grep SCSI /var/log/messages
    ```
   
    Para distribuciones de Ubuntu recientes, puede que necesite toouse `sudo grep SCSI /var/log/syslog` porque registro demasiado`/var/log/messages` pueden deshabilitarse de forma predeterminada.
   
    Puede encontrar el identificador de Hola Hola última del disco de datos que se agregó en los mensajes de saludo que se muestran.
   
    ![Obtener mensajes de Hola disco](./media/attach-disk/scsidisklog.png)
   
    OR
   
    b) Hola usar `lsscsi` toofind comando out Id. de dispositivo de Hola. `lsscsi` pueden instalarse, ya sea `yum install lsscsi` (Red Hat según las distribuciones) o `apt-get install lsscsi` (Debian según las distribuciones). Se puede encontrar un disco de Hola que está buscando por su *lun* o **número de unidad lógica**. Por ejemplo, hello *lun* para discos de hello adjuntó pueden verse fácilmente desde `azure vm disk list <virtual-machine>` como:

    ```azurecli
    azure vm disk list myVM
    ```

    salida de Hello es siguiente de toohello similar:

    ```azurecli
    info:    Executing command vm disk list
    + Fetching disk images
    + Getting virtual machines
    + Getting VM disks
    data:    Lun  Size(GB)  Blob-Name                         OS
    data:    ---  --------  --------------------------------  -----
    data:         30        myVM-2645b8030676c8f8.vhd  Linux
    data:    0    100       myVM-76f7ee1ef0f6dddc.vhd
    info:    vm disk list command OK
    ```
   
    Comparar estos datos con salida de hello de `lsscsi` Hola mismo ejemplo máquina virtual:
   
    ```bash
    [1:0:0:0]    cd/dvd  Msft     Virtual CD/ROM   1.0   /dev/sr0
    [2:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sda
    [3:0:1:0]    disk    Msft     Virtual Disk     1.0   /dev/sdb
    [5:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sdc
    ```
   
    último número de Hola de tupla de hello en cada fila es hello *lun*. Vea `man lsscsi` para obtener más información.
3. En el símbolo del sistema de hello, escriba lo siguiente Hola comando toocreate el dispositivo:
   
    ```bash
    sudo fdisk /dev/sdc
    ```

4. Cuando se le solicite, escriba  **n**  toocreate una partición.

    ![Crear dispositivo](./media/attach-disk/fdisknewpartition.png)

5. Cuando se le solicite, escriba **p** toomake Hola Hola principal de particiones. Tipo de **1** toomake Hola primera partición y, a continuación, escriba escriba el valor predeterminado de tooaccept Hola para cilindro de Hola. En algunos sistemas, puede mostrar primero los valores predeterminados de Hola de Hola y Hola sectores último, en lugar de los cilindros Hola. Puede elegir tooaccept estos valores predeterminados.

    ![Crear partición](./media/attach-disk/fdisknewpartdetails.png)


6. Tipo de **p** detalles de hello toosee acerca del disco de Hola se particiona.

    ![Enumerar la información del disco](./media/attach-disk/fdiskpartitiondetails.png)


7. Tipo de **w** toowrite la configuración de Hola de discos de Hola.

    ![Escribir los cambios de disco Hola](./media/attach-disk/fdiskwritedisk.png)

8. Ahora puede crear sistema de archivos de hello en la nueva partición de Hola. Anexar Hola número toohello dispositivo Id. de partición (en el siguiente ejemplo de Hola `/dev/sdc1`). Hello en el ejemplo siguiente se crea una partición de ext4 en /dev/sdc1:
   
    ```bash
    sudo mkfs -t ext4 /dev/sdc1
    ```
   
    ![Crear sistema de archivos](./media/attach-disk/mkfsext4.png)
   
   > [!NOTE]
   > Los sistemas SUSE Linux Enterprise 11 únicamente admiten acceso de solo lectura a sistemas de archivos ext4. Para estos sistemas, se recomienda tooformat Hola nuevo sistema de archivos como ext3 en lugar de ext4.

9. Realice un directorio toomount Hola nuevo sistema de archivos, como se indica a continuación:
   
    ```bash
    sudo mkdir /datadrive
    ```

10. Por último, se puede montar unidad hello, como se indica a continuación:
   
    ```bash
    sudo mount /dev/sdc1 /datadrive
    ```
   
    disco de datos de Hello ya está listo toouse como **/datadrive**.
   
    ![Crear disco de Hola de directorio y montaje Hola](./media/attach-disk/mkdirandmount.png)

11. Agregue Hola nueva unidad demasiado/etcetera/fstab:
   
    unidad de hello tooensure se vuelven a montar automáticamente después de reiniciar el equipo debe ser agregado toohello/etc/fstab archivo. Además, se recomienda que Hola UUID (identificador único universalmente de) se utiliza en/etc/fstab toorefer toohello unidad en lugar de simplemente Hola nombre del dispositivo (es decir, /dev/sdc1). Uso de hello UUID evita está montada tooa ubicación dada si Hola SO detecta un error de disco durante el arranque y los discos de datos restantes, a continuación, que se va a asignaron los identificadores de dispositivo de disco incorrecta Hola. toofind Hola UUID de la nueva unidad de hello, puede usar hello **blkid** utilidad:
   
    ```bash
    sudo -i blkid
    ```
   
    salida de Hello tiene un aspecto similar toohello siguiente ejemplo:
   
    ```bash
    /dev/sda1: UUID="11111111-1b1b-1c1c-1d1d-1e1e1e1e1e1e" TYPE="ext4"
    /dev/sdb1: UUID="22222222-2b2b-2c2c-2d2d-2e2e2e2e2e2e" TYPE="ext4"
    /dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
    ```

    > [!NOTE]
    > Edición incorrectamente hello **/etcetera/fstab** archivo podría provocar un reinicio del sistema. Si no está seguro, consulte la documentación de la distribución de toohello para obtener información sobre cómo tooproperly editar este archivo. También se recomienda que se crea una copia de seguridad del archivo/etc/fstab de hello antes de modificarla.

    A continuación, abra hello **/etcetera/fstab** archivo en un editor de texto:

    ```bash
    sudo vi /etc/fstab
    ```

    En este ejemplo, utilizamos Hola UUID valor para hello nueva **/dev/sdc1** dispositivo que se creó en los pasos anteriores de Hola y el punto de montaje de hello **/datadrive**. Agregar Hola siguiente línea toohello final de hello **/etcetera/fstab** archivo:

    ```sh
    UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,nofail   1   2
    ```

    O bien, en sistemas basados en SuSE Linux que necesite toouse un formato ligeramente diferente:

    ```sh
    /dev/disk/by-uuid/33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext3   defaults,nofail   1   2
    ```

    > [!NOTE]
    > Hola `nofail` opción garantiza que Hola VM inicie aunque Hola filesystem está dañado o disco hello no existe en tiempo de arranque. Sin esta opción, se puede encontrar un comportamiento tal y como se describe en [no SSH tooLinux VM debido a errores de tooFSTAB](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/).

    Ahora puede probar que el sistema de archivos de hello está montado correctamente al desmontar y, a continuación, vuelva a montar el sistema de archivos de hello, es decir, con el punto de montaje del ejemplo de Hola `/datadrive` creado en hello los pasos anteriores:

    ```bash
    sudo umount /datadrive
    sudo mount /datadrive
    ```

    Si hello `mount` comando produce un error, compruebe Hola/etcetera/fstab archivo para ver la sintaxis correcta. Si se crean particiones o unidades de datos adicionales, especifíquelas también en /etc/fstab por separado.

    Asegúrese de unidad de hello grabable mediante este comando:

    ```bash
    sudo chmod go+w /datadrive
    ```

    > [!NOTE]
    > Quitar posteriormente un disco de datos sin necesidad de editar fstab podría producir Hola VM toofail tooboot. Si se trata de un hecho frecuente, mayoría de las distribuciones proporciona cualquier hello `nofail` o `nobootwait` fstab opciones que permiten una tooboot sistema aunque hello tiene un error toomount al arrancar el sistema. Consulte la documentación de su distribución para obtener más información sobre estos parámetros.

### <a name="trimunmap-support-for-linux-in-azure"></a>Compatibilidad de TRIM/UNMAP con Linux en Azure
Algunos los kernels de Linux admiten TRIM y UNMAP operaciones toodiscard los bloques sin utilizar en el disco de Hola. Estas operaciones son sobre todo útiles en almacenamiento estándar tooinform Azure que elimina páginas ya no son válidos y se pueden descartar. El descarte de páginas puede suponer un ahorro de dinero si crea archivos grandes y, a continuación, los elimina.

Hay dos maneras tooenable TRIM se admiten en la VM de Linux. Como es habitual, consulte la distribución de hello enfoque recomendado:

* Hola de uso `discard` montar opción en `/etc/fstab`, por ejemplo:

    ```sh
    UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,discard   1   2
    ```

* En algunos Hola casos `discard` opción podría tener implicaciones de rendimiento. Como alternativa, puede ejecutar hello `fstrim` comando manualmente desde la línea de comandos de hello, o agréguela tooyour crontab toorun con regularidad:
  
    **Ubuntu**
  
    ```bash
    sudo apt-get install util-linux
    sudo fstrim /datadrive
    ```
  
    **RHEL/CentOS**
  
    ```bash
    sudo yum install util-linux
    sudo fstrim /datadrive
    ```

## <a name="troubleshooting"></a>Solución de problemas
[!INCLUDE [virtual-machines-linux-lunzero](../../../../includes/virtual-machines-linux-lunzero.md)]

## <a name="next-steps"></a>Pasos siguientes
Puede leer más sobre el uso de la VM de Linux en hello siguientes artículos:

* [¿Cómo toolog en la máquina virtual de tooa ejecutan Linux][Logon]
* [¿Cómo toodetach un disco de una máquina virtual Linux](detach-disk.md)
* [Usar Hola CLI de Azure con modelo de implementación de hello clásico](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)
* [Configuración de RAID en una máquina virtual Linux en Azure](../configure-raid.md)
* [Configuración del LVM en una máquina virtual Linux en Azure](../configure-lvm.md)

<!--Link references-->
[Agent]:../agent-user-guide.md
[Logon]:../mac-create-ssh-keys.md
