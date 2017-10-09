---
title: aaaAdd una VM de disco tooLinux con Hola CLI de Azure | Documentos de Microsoft
description: "Obtenga información acerca de tooadd un tooyour de disco persistente VM de Linux con hello Azure CLI 1.0 y 2.0."
keywords: "máquina virtual de Linux, agregar disco de recursos"
services: virtual-machines-linux
documentationcenter: 
author: rickstercdn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 3005a066-7a84-4dc5-bdaa-574c75e6e411
ms.service: virtual-machines-linux
ms.topic: article
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.date: 02/02/2017
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0dc5236be62d96b70dd47a7f621f626a037e22aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-disk-tooa-linux-vm"></a>Agregar una VM de Linux tooa de disco
Este artículo muestra cómo tooattach una persistente disco tooyour VM para que se pueden conservar los datos: incluso si la máquina virtual se volverá a aprovisionar debido toomaintenance o cambiar el tamaño. 

## <a name="quick-commands"></a>Comandos rápidos
Hola siguientes en el ejemplo se asocia un `50`GB disco toohello máquina virtual denominada `myVM` en grupo de recursos de hello llamado `myResourceGroup`:

discos administrados por toouse:

```azurecli
az vm disk attach -g myResourceGroup --vm-name myVM --disk myDataDisk \
  --new --size-gb 50
```

discos toouse no administrado:

```azurecli
az vm unmanaged-disk attach -g myResourceGroup -n myUnmanagedDisk --vm-name myVM \
  --new --size-gb 50
```

## <a name="attach-a-managed-disk"></a>Conexión de un disco administrado

Uso de discos administrados permite toofocus en las máquinas virtuales y sus discos sin preocuparse de las cuentas de almacenamiento de Azure. Puede crear y adjuntar un disco administrado rápidamente tooa VM con Hola el mismo grupo de recursos de Azure, o puede crear cualquier número de discos y, después, conéctelas.


### <a name="attach-a-new-disk-tooa-vm"></a>Adjuntar una nueva tooa de disco virtual

Si sólo necesita un disco nuevo en la máquina virtual, puede usar hello `az vm disk attach` comando.

```azurecli
az vm disk attach -g myResourceGroup --vm-name myVM --disk myDataDisk \
  --new --size-gb 50
```

### <a name="attach-an-existing-disk"></a>un disco existente 

En muchos casos conecta discos que ya se han creado. En primer lugar buscar Id. de disco de hello y, a continuación, pasar esa toohello `az vm disk attach` comando. Hello en el ejemplo siguiente se usa un disco creado con `az disk create -g myResourceGroup -n myDataDisk --size-gb 50`.

```azurecli
# find hello disk id
diskId=$(az disk show -g myResourceGroup -n myDataDisk --query 'id' -o tsv)
az vm disk attach -g myResourceGroup --vm-name myVM --disk $diskId
```

Hello salida es similar al siguiente hello (puede usar hello `-o table` opción de salida de hello tooany comando tooformat en):

```json
{
  "accountType": "Standard_LRS",
  "creationData": {
    "createOption": "Empty",
    "imageReference": null,
    "sourceResourceId": null,
    "sourceUri": null,
    "storageAccountId": null
  },
  "diskSizeGb": 50,
  "encryptionSettings": null,
  "id": "/subscriptions/<guid>/resourceGroups/rasquill-script/providers/Microsoft.Compute/disks/myDataDisk",
  "location": "westus",
  "name": "myDataDisk",
  "osType": null,
  "ownerId": null,
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "tags": null,
  "timeCreated": "2017-02-02T23:35:47.708082+00:00",
  "type": "Microsoft.Compute/disks"
}
```


## <a name="attach-an-unmanaged-disk"></a>Conexión de un disco no administrado

Adjuntar un disco nuevo es muy rápido si no le importa que crear un disco en hello la misma cuenta de almacenamiento que la máquina virtual. Tipo de `azure vm disk attach-new` toocreate y asociar un nuevo disco de GB para la máquina virtual. Si no identifica explícitamente una cuenta de almacenamiento, cualquier disco que crea se coloca en hello misma cuenta de almacenamiento donde reside el disco del sistema operativo. Hola siguientes en el ejemplo se asocia un `50`GB disco toohello máquina virtual denominada `myVM` en grupo de recursos de hello llamado `myResourceGroup`:

```azurecli
az vm unmanaged-disk attach -g myResourceGroup -n myUnmanagedDisk --vm-name myVM \
  --new --size-gb 50
```

## <a name="connect-toohello-linux-vm-toomount-hello-new-disk"></a>Conectar el nuevo disco de VM de Linux toomount hello toohello
> [!NOTE]
> En este tema se conecta tooa VM mediante nombres de usuario y contraseñas. toouse toocommunicate de pares de claves pública y privada con la máquina virtual, consulte [cómo tooUse SSH con Linux en Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). 
> 
> 

Necesita tooSSH en su toopartition de máquina virtual de Azure, dar formato y montar el disco nuevo para la VM de Linux pueda usarlos. Si no está familiarizado con la conexión con **ssh**, comando hello toma la forma de hello `ssh <username>@<FQDNofAzureVM> -p <hello ssh port>`y es similar a Hola siguiente:

```bash
ssh ops@mypublicdns.westus.cloudapp.azure.com -p 22
```

Salida

```bash
hello authenticity of host 'mypublicdns.westus.cloudapp.azure.com (191.239.51.1)' can't be established.
ECDSA key fingerprint is bx:xx:xx:xx:xx:xx:xx:xx:xx:x:x:x:x:x:x:xx.
Are you sure you want toocontinue connecting (yes/no)? yes
Warning: Permanently added 'mypublicdns.westus.cloudapp.azure.com,191.239.51.1' (ECDSA) toohello list of known hosts.
ops@mypublicdns.westus.cloudapp.azure.com's password:
Welcome tooUbuntu 14.04.2 LTS (GNU/Linux 3.16.0-37-generic x86_64)

* Documentation:  https://help.ubuntu.com/

System information as of Fri May 22 21:02:32 UTC 2015

System load: 0.37              Memory usage: 2%   Processes:       207
Usage of /:  41.4% of 1.94GB   Swap usage:   0%   Users logged in: 0

Graph this data and manage this system at:
  https://landscape.canonical.com/

Get cloud support with Ubuntu Advantage Cloud Guest:
  http://www.ubuntu.com/business/services/cloud

0 packages can be updated.
0 updates are security updates.

hello programs included with hello Ubuntu system are free software;
hello exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, toohello extent permitted by
applicable law.

ops@myVM:~$
```

Ahora que está conectado tooyour VM, está listo tooattach un disco.  En primer lugar, busque Hola disco, mediante `dmesg | grep SCSI` (método hello usar toodiscover el nuevo disco puede variar). En este caso, es similar a lo siguiente:

```bash
dmesg | grep SCSI
```

Salida

```bash
[    0.294784] SCSI subsystem initialized
[    0.573458] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 252)
[    7.110271] sd 2:0:0:0: [sda] Attached SCSI disk
[    8.079653] sd 3:0:1:0: [sdb] Attached SCSI disk
[ 1828.162306] sd 5:0:0:0: [sdc] Attached SCSI disk
```

y en caso de hello de este tema, Hola `sdc` disco es hello uno que queremos. Disco de Hola de partición ahora con `sudo fdisk /dev/sdc` , suponiendo que en su caso Hola disco sea `sdc`y convertirlo en un disco principal en la partición 1 y Aceptar Hola otros valores predeterminados.

```bash
sudo fdisk /dev/sdc
```

Salida

```bash
Device contains neither a valid DOS partition table, nor Sun, SGI or OSF disklabel
Building a new DOS disklabel with disk identifier 0x2a59b123.
Changes will remain in memory only, until you decide toowrite them.
After that, of course, hello previous content won't be recoverable.

Warning: invalid flag 0x0000 of partition table 4 will be corrected by w(rite)

Command (m for help): n
Partition type:
   p   primary (0 primary, 0 extended, 4 free)
   e   extended
Select (default p): p
Partition number (1-4, default 1): 1
First sector (2048-10485759, default 2048):
Using default value 2048
Last sector, +sectors or +size{K,M,G} (2048-10485759, default 10485759):
Using default value 10485759
```

Crear partición Hola escribiendo `p` en símbolo del sistema de hello:

```bash
Command (m for help): p

Disk /dev/sdc: 5368 MB, 5368709120 bytes
255 heads, 63 sectors/track, 652 cylinders, total 10485760 sectors
Units = sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disk identifier: 0x2a59b123

   Device Boot      Start         End      Blocks   Id  System
/dev/sdc1            2048    10485759     5241856   83  Linux

Command (m for help): w
hello partition table has been altered!

Calling ioctl() toore-read partition table.
Syncing disks.
```

Y escribir una partición de toohello de sistema de archivos mediante el uso de hello **mkfs** comando, especifique el nombre del dispositivo de hello y tipo de sistema de archivos. En este tema, estamos usando `ext4` y `/dev/sdc1` mostrados anteriormente:

```bash
sudo mkfs -t ext4 /dev/sdc1
```

Salida

```bash
mke2fs 1.42.9 (4-Feb-2014)
Discarding device blocks: done
Filesystem label=
OS type: Linux
Block size=4096 (log=2)
Fragment size=4096 (log=2)
Stride=0 blocks, Stripe width=0 blocks
327680 inodes, 1310464 blocks
65523 blocks (5.00%) reserved for hello super user
First data block=0
Maximum filesystem blocks=1342177280
40 block groups
32768 blocks per group, 32768 fragments per group
8192 inodes per group
Superblock backups stored on blocks:
    32768, 98304, 163840, 229376, 294912, 819200, 884736
Allocating group tables: done
Writing inode tables: done
Creating journal (32768 blocks): done
Writing superblocks and filesystem accounting information: done
```

Ahora se crea un directorio toomount Hola sistema de archivos mediante `mkdir`:

```bash
sudo mkdir /datadrive
```

Y montar Hola directorio mediante `mount`:

```bash
sudo mount /dev/sdc1 /datadrive
```

disco de datos de Hello ya está listo toouse como `/datadrive`.

```bash
ls
```

Salida

```bash
bin   datadrive  etc   initrd.img  lib64       media  opt   root  sbin  sys  usr  vmlinuz
boot  dev        home  lib         lost+found  mnt    proc  run   srv   tmp  var
```

unidad de hello tooensure se vuelven a montar automáticamente después de reiniciar el equipo debe ser agregado toohello/etc/fstab archivo. Además, se recomienda encarecidamente que Hola UUID (identificador único universalmente de) se utiliza en/etc/fstab toorefer toohello de unidad en lugar del nombre de dispositivo de hello solo (como por ejemplo, `/dev/sdc1`). Si Hola SO detecta un error de disco durante el arranque, el uso de hello UUID evita disco incorrecto Hola está montada tooa la ubicación dada. A los discos de datos restantes se les asignarán después esos mismos identificadores de dispositivo. toofind Hola UUID de la nueva unidad de hello, use hello **blkid** utilidad:

```bash
sudo -i blkid
```

salida de Hello tiene un aspecto similar siguiente toohello:

```bash
/dev/sda1: UUID="11111111-1b1b-1c1c-1d1d-1e1e1e1e1e1e" TYPE="ext4"
/dev/sdb1: UUID="22222222-2b2b-2c2c-2d2d-2e2e2e2e2e2e" TYPE="ext4"
/dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
```

> [!NOTE]
> Edición incorrectamente hello **/etcetera/fstab** archivo podría provocar un reinicio del sistema. Si no está seguro, consulte la documentación de la distribución de toohello para obtener información sobre cómo tooproperly editar este archivo. También se recomienda que se crea una copia de seguridad del archivo/etc/fstab de hello antes de modificarla.
> 
> 

A continuación, abra hello **/etcetera/fstab** archivo en un editor de texto:

```bash
sudo vi /etc/fstab
```

En este ejemplo, utilizamos Hola UUID valor para hello nueva **/dev/sdc1** dispositivo que se creó en los pasos anteriores de Hola y el punto de montaje de hello **/datadrive**. Agregar Hola siguiente línea toohello final de hello **/etcetera/fstab** archivo:

```bash
UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,nofail   1   2
```

> [!NOTE]
> Más adelante quitar un disco de datos sin necesidad de editar fstab podría producir Hola VM toofail tooboot. Mayoría de las distribuciones proporciona cualquier hello `nofail` o `nobootwait` fstab opciones. Estas opciones permiten un tooboot sistema aunque hello tiene un error toomount al arrancar el sistema. Consulte la documentación de su distribución para obtener más información sobre estos parámetros.
> 
> Hola **nofail** opción garantiza que Hola VM inicie aunque Hola filesystem está dañado o disco hello no existe en tiempo de arranque. Sin esta opción, se puede encontrar un comportamiento tal y como se describe en [no SSH tooLinux VM debido a errores de tooFSTAB](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/)

### <a name="trimunmap-support-for-linux-in-azure"></a>Compatibilidad de TRIM/UNMAP con Linux en Azure
Algunos los kernels de Linux admiten TRIM y UNMAP operaciones toodiscard los bloques sin utilizar en el disco de Hola. Esto es especialmente útil en almacenamiento estándar tooinform Azure que elimina páginas ya no son válidos y se pueden descartar. Esto puede suponer un ahorro de dinero si crea archivos grandes y, a continuación, los elimina.

Hay dos maneras tooenable TRIM se admiten en la VM de Linux. Como es habitual, consulte la distribución de hello enfoque recomendado:

* Hola de uso `discard` montar opción en `/etc/fstab`, por ejemplo:

    ```bash
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
[!INCLUDE [virtual-machines-linux-lunzero](../../../includes/virtual-machines-linux-lunzero.md)]

## <a name="next-steps"></a>Pasos siguientes
* Recuerde que el nuevo disco no es disponible toohello máquina virtual si se reinicia a menos que escriba esa información tooyour [fstab](http://en.wikipedia.org/wiki/Fstab) archivo.
* tooensure la VM de Linux está configurado correctamente, revisión hello [optimizar el rendimiento del equipo Linux](optimization.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) recomendaciones.
* Amplíe la capacidad de almacenamiento mediante la adición de discos adicionales y [configure RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) para obtener un mayor rendimiento.

