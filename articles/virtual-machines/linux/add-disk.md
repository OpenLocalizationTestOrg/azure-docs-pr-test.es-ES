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
# <a name="add-a-disk-tooa-linux-vm"></a><span data-ttu-id="b1405-104">Agregar una VM de Linux tooa de disco</span><span class="sxs-lookup"><span data-stu-id="b1405-104">Add a disk tooa Linux VM</span></span>
<span data-ttu-id="b1405-105">Este artículo muestra cómo tooattach una persistente disco tooyour VM para que se pueden conservar los datos: incluso si la máquina virtual se volverá a aprovisionar debido toomaintenance o cambiar el tamaño.</span><span class="sxs-lookup"><span data-stu-id="b1405-105">This article shows how tooattach a persistent disk tooyour VM so that you can preserve your data - even if your VM is reprovisioned due toomaintenance or resizing.</span></span> 

## <a name="quick-commands"></a><span data-ttu-id="b1405-106">Comandos rápidos</span><span class="sxs-lookup"><span data-stu-id="b1405-106">Quick Commands</span></span>
<span data-ttu-id="b1405-107">Hola siguientes en el ejemplo se asocia un `50`GB disco toohello máquina virtual denominada `myVM` en grupo de recursos de hello llamado `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="b1405-107">hello following example attaches a `50`GB disk toohello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

<span data-ttu-id="b1405-108">discos administrados por toouse:</span><span class="sxs-lookup"><span data-stu-id="b1405-108">toouse managed disks:</span></span>

```azurecli
az vm disk attach -g myResourceGroup --vm-name myVM --disk myDataDisk \
  --new --size-gb 50
```

<span data-ttu-id="b1405-109">discos toouse no administrado:</span><span class="sxs-lookup"><span data-stu-id="b1405-109">toouse unmanaged disks:</span></span>

```azurecli
az vm unmanaged-disk attach -g myResourceGroup -n myUnmanagedDisk --vm-name myVM \
  --new --size-gb 50
```

## <a name="attach-a-managed-disk"></a><span data-ttu-id="b1405-110">Conexión de un disco administrado</span><span class="sxs-lookup"><span data-stu-id="b1405-110">Attach a managed disk</span></span>

<span data-ttu-id="b1405-111">Uso de discos administrados permite toofocus en las máquinas virtuales y sus discos sin preocuparse de las cuentas de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="b1405-111">Using managed disks enables you toofocus on your VMs and their disks without worrying about Azure Storage accounts.</span></span> <span data-ttu-id="b1405-112">Puede crear y adjuntar un disco administrado rápidamente tooa VM con Hola el mismo grupo de recursos de Azure, o puede crear cualquier número de discos y, después, conéctelas.</span><span class="sxs-lookup"><span data-stu-id="b1405-112">You can quickly create and attach a managed disk tooa VM using hello same Azure resource group, or you can create any number of disks and then attach them.</span></span>


### <a name="attach-a-new-disk-tooa-vm"></a><span data-ttu-id="b1405-113">Adjuntar una nueva tooa de disco virtual</span><span class="sxs-lookup"><span data-stu-id="b1405-113">Attach a new disk tooa VM</span></span>

<span data-ttu-id="b1405-114">Si sólo necesita un disco nuevo en la máquina virtual, puede usar hello `az vm disk attach` comando.</span><span class="sxs-lookup"><span data-stu-id="b1405-114">If you just need a new disk on your VM, you can use hello `az vm disk attach` command.</span></span>

```azurecli
az vm disk attach -g myResourceGroup --vm-name myVM --disk myDataDisk \
  --new --size-gb 50
```

### <a name="attach-an-existing-disk"></a><span data-ttu-id="b1405-115">un disco existente</span><span class="sxs-lookup"><span data-stu-id="b1405-115">Attach an existing disk</span></span> 

<span data-ttu-id="b1405-116">En muchos casos conecta discos que ya se han creado.</span><span class="sxs-lookup"><span data-stu-id="b1405-116">In many cases you attach disks that have already been created.</span></span> <span data-ttu-id="b1405-117">En primer lugar buscar Id. de disco de hello y, a continuación, pasar esa toohello `az vm disk attach` comando.</span><span class="sxs-lookup"><span data-stu-id="b1405-117">You first find hello disk id and then pass that toohello `az vm disk attach` command.</span></span> <span data-ttu-id="b1405-118">Hello en el ejemplo siguiente se usa un disco creado con `az disk create -g myResourceGroup -n myDataDisk --size-gb 50`.</span><span class="sxs-lookup"><span data-stu-id="b1405-118">hello following example uses a disk created with `az disk create -g myResourceGroup -n myDataDisk --size-gb 50`.</span></span>

```azurecli
# find hello disk id
diskId=$(az disk show -g myResourceGroup -n myDataDisk --query 'id' -o tsv)
az vm disk attach -g myResourceGroup --vm-name myVM --disk $diskId
```

<span data-ttu-id="b1405-119">Hello salida es similar al siguiente hello (puede usar hello `-o table` opción de salida de hello tooany comando tooformat en):</span><span class="sxs-lookup"><span data-stu-id="b1405-119">hello output looks something like hello following (you can use hello `-o table` option tooany command tooformat hello output in ):</span></span>

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


## <a name="attach-an-unmanaged-disk"></a><span data-ttu-id="b1405-120">Conexión de un disco no administrado</span><span class="sxs-lookup"><span data-stu-id="b1405-120">Attach an unmanaged disk</span></span>

<span data-ttu-id="b1405-121">Adjuntar un disco nuevo es muy rápido si no le importa que crear un disco en hello la misma cuenta de almacenamiento que la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="b1405-121">Attaching a new disk is quick if you do not mind creating a disk in hello same storage account as your VM.</span></span> <span data-ttu-id="b1405-122">Tipo de `azure vm disk attach-new` toocreate y asociar un nuevo disco de GB para la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="b1405-122">Type `azure vm disk attach-new` toocreate and attach a new GB disk for your VM.</span></span> <span data-ttu-id="b1405-123">Si no identifica explícitamente una cuenta de almacenamiento, cualquier disco que crea se coloca en hello misma cuenta de almacenamiento donde reside el disco del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="b1405-123">If you do not explicitly identify a storage account, any disk you create is placed in hello same storage account where your OS disk resides.</span></span> <span data-ttu-id="b1405-124">Hola siguientes en el ejemplo se asocia un `50`GB disco toohello máquina virtual denominada `myVM` en grupo de recursos de hello llamado `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="b1405-124">hello following example attaches a `50`GB disk toohello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

```azurecli
az vm unmanaged-disk attach -g myResourceGroup -n myUnmanagedDisk --vm-name myVM \
  --new --size-gb 50
```

## <a name="connect-toohello-linux-vm-toomount-hello-new-disk"></a><span data-ttu-id="b1405-125">Conectar el nuevo disco de VM de Linux toomount hello toohello</span><span class="sxs-lookup"><span data-stu-id="b1405-125">Connect toohello Linux VM toomount hello new disk</span></span>
> [!NOTE]
> <span data-ttu-id="b1405-126">En este tema se conecta tooa VM mediante nombres de usuario y contraseñas.</span><span class="sxs-lookup"><span data-stu-id="b1405-126">This topic connects tooa VM using usernames and passwords.</span></span> <span data-ttu-id="b1405-127">toouse toocommunicate de pares de claves pública y privada con la máquina virtual, consulte [cómo tooUse SSH con Linux en Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b1405-127">toouse public and private key pairs toocommunicate with your VM, see [How tooUse SSH with Linux on Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 
> 
> 

<span data-ttu-id="b1405-128">Necesita tooSSH en su toopartition de máquina virtual de Azure, dar formato y montar el disco nuevo para la VM de Linux pueda usarlos.</span><span class="sxs-lookup"><span data-stu-id="b1405-128">You need tooSSH into your Azure VM toopartition, format, and mount your new disk so your Linux VM can use it.</span></span> <span data-ttu-id="b1405-129">Si no está familiarizado con la conexión con **ssh**, comando hello toma la forma de hello `ssh <username>@<FQDNofAzureVM> -p <hello ssh port>`y es similar a Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="b1405-129">If you're not familiar with connecting with **ssh**, hello command takes hello form `ssh <username>@<FQDNofAzureVM> -p <hello ssh port>`, and looks like hello following:</span></span>

```bash
ssh ops@mypublicdns.westus.cloudapp.azure.com -p 22
```

<span data-ttu-id="b1405-130">Salida</span><span class="sxs-lookup"><span data-stu-id="b1405-130">Output</span></span>

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

<span data-ttu-id="b1405-131">Ahora que está conectado tooyour VM, está listo tooattach un disco.</span><span class="sxs-lookup"><span data-stu-id="b1405-131">Now that you're connected tooyour VM, you're ready tooattach a disk.</span></span>  <span data-ttu-id="b1405-132">En primer lugar, busque Hola disco, mediante `dmesg | grep SCSI` (método hello usar toodiscover el nuevo disco puede variar).</span><span class="sxs-lookup"><span data-stu-id="b1405-132">First find hello disk, using `dmesg | grep SCSI` (hello method you use toodiscover your new disk may vary).</span></span> <span data-ttu-id="b1405-133">En este caso, es similar a lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="b1405-133">In this case, it looks something like:</span></span>

```bash
dmesg | grep SCSI
```

<span data-ttu-id="b1405-134">Salida</span><span class="sxs-lookup"><span data-stu-id="b1405-134">Output</span></span>

```bash
[    0.294784] SCSI subsystem initialized
[    0.573458] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 252)
[    7.110271] sd 2:0:0:0: [sda] Attached SCSI disk
[    8.079653] sd 3:0:1:0: [sdb] Attached SCSI disk
[ 1828.162306] sd 5:0:0:0: [sdc] Attached SCSI disk
```

<span data-ttu-id="b1405-135">y en caso de hello de este tema, Hola `sdc` disco es hello uno que queremos.</span><span class="sxs-lookup"><span data-stu-id="b1405-135">and in hello case of this topic, hello `sdc` disk is hello one that we want.</span></span> <span data-ttu-id="b1405-136">Disco de Hola de partición ahora con `sudo fdisk /dev/sdc` , suponiendo que en su caso Hola disco sea `sdc`y convertirlo en un disco principal en la partición 1 y Aceptar Hola otros valores predeterminados.</span><span class="sxs-lookup"><span data-stu-id="b1405-136">Now partition hello disk with `sudo fdisk /dev/sdc` -- assuming that in your case hello disk was `sdc`, and make it a primary disk on partition 1, and accept hello other defaults.</span></span>

```bash
sudo fdisk /dev/sdc
```

<span data-ttu-id="b1405-137">Salida</span><span class="sxs-lookup"><span data-stu-id="b1405-137">Output</span></span>

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

<span data-ttu-id="b1405-138">Crear partición Hola escribiendo `p` en símbolo del sistema de hello:</span><span class="sxs-lookup"><span data-stu-id="b1405-138">Create hello partition by typing `p` at hello prompt:</span></span>

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

<span data-ttu-id="b1405-139">Y escribir una partición de toohello de sistema de archivos mediante el uso de hello **mkfs** comando, especifique el nombre del dispositivo de hello y tipo de sistema de archivos.</span><span class="sxs-lookup"><span data-stu-id="b1405-139">And write a file system toohello partition by using hello **mkfs** command, specifying your filesystem type and hello device name.</span></span> <span data-ttu-id="b1405-140">En este tema, estamos usando `ext4` y `/dev/sdc1` mostrados anteriormente:</span><span class="sxs-lookup"><span data-stu-id="b1405-140">In this topic, we're using `ext4` and `/dev/sdc1` from above:</span></span>

```bash
sudo mkfs -t ext4 /dev/sdc1
```

<span data-ttu-id="b1405-141">Salida</span><span class="sxs-lookup"><span data-stu-id="b1405-141">Output</span></span>

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

<span data-ttu-id="b1405-142">Ahora se crea un directorio toomount Hola sistema de archivos mediante `mkdir`:</span><span class="sxs-lookup"><span data-stu-id="b1405-142">Now we create a directory toomount hello file system using `mkdir`:</span></span>

```bash
sudo mkdir /datadrive
```

<span data-ttu-id="b1405-143">Y montar Hola directorio mediante `mount`:</span><span class="sxs-lookup"><span data-stu-id="b1405-143">And you mount hello directory using `mount`:</span></span>

```bash
sudo mount /dev/sdc1 /datadrive
```

<span data-ttu-id="b1405-144">disco de datos de Hello ya está listo toouse como `/datadrive`.</span><span class="sxs-lookup"><span data-stu-id="b1405-144">hello data disk is now ready toouse as `/datadrive`.</span></span>

```bash
ls
```

<span data-ttu-id="b1405-145">Salida</span><span class="sxs-lookup"><span data-stu-id="b1405-145">Output</span></span>

```bash
bin   datadrive  etc   initrd.img  lib64       media  opt   root  sbin  sys  usr  vmlinuz
boot  dev        home  lib         lost+found  mnt    proc  run   srv   tmp  var
```

<span data-ttu-id="b1405-146">unidad de hello tooensure se vuelven a montar automáticamente después de reiniciar el equipo debe ser agregado toohello/etc/fstab archivo.</span><span class="sxs-lookup"><span data-stu-id="b1405-146">tooensure hello drive is remounted automatically after a reboot it must be added toohello /etc/fstab file.</span></span> <span data-ttu-id="b1405-147">Además, se recomienda encarecidamente que Hola UUID (identificador único universalmente de) se utiliza en/etc/fstab toorefer toohello de unidad en lugar del nombre de dispositivo de hello solo (como por ejemplo, `/dev/sdc1`).</span><span class="sxs-lookup"><span data-stu-id="b1405-147">In addition, it is highly recommended that hello UUID (Universally Unique IDentifier) is used in /etc/fstab toorefer toohello drive rather than just hello device name (such as, `/dev/sdc1`).</span></span> <span data-ttu-id="b1405-148">Si Hola SO detecta un error de disco durante el arranque, el uso de hello UUID evita disco incorrecto Hola está montada tooa la ubicación dada.</span><span class="sxs-lookup"><span data-stu-id="b1405-148">If hello OS detects a disk error during boot, using hello UUID avoids hello incorrect disk being mounted tooa given location.</span></span> <span data-ttu-id="b1405-149">A los discos de datos restantes se les asignarán después esos mismos identificadores de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="b1405-149">Remaining data disks would then be assigned those same device IDs.</span></span> <span data-ttu-id="b1405-150">toofind Hola UUID de la nueva unidad de hello, use hello **blkid** utilidad:</span><span class="sxs-lookup"><span data-stu-id="b1405-150">toofind hello UUID of hello new drive, use hello **blkid** utility:</span></span>

```bash
sudo -i blkid
```

<span data-ttu-id="b1405-151">salida de Hello tiene un aspecto similar siguiente toohello:</span><span class="sxs-lookup"><span data-stu-id="b1405-151">hello output looks similar toohello following:</span></span>

```bash
/dev/sda1: UUID="11111111-1b1b-1c1c-1d1d-1e1e1e1e1e1e" TYPE="ext4"
/dev/sdb1: UUID="22222222-2b2b-2c2c-2d2d-2e2e2e2e2e2e" TYPE="ext4"
/dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
```

> [!NOTE]
> <span data-ttu-id="b1405-152">Edición incorrectamente hello **/etcetera/fstab** archivo podría provocar un reinicio del sistema.</span><span class="sxs-lookup"><span data-stu-id="b1405-152">Improperly editing hello **/etc/fstab** file could result in an unbootable system.</span></span> <span data-ttu-id="b1405-153">Si no está seguro, consulte la documentación de la distribución de toohello para obtener información sobre cómo tooproperly editar este archivo.</span><span class="sxs-lookup"><span data-stu-id="b1405-153">If unsure, refer toohello distribution's documentation for information on how tooproperly edit this file.</span></span> <span data-ttu-id="b1405-154">También se recomienda que se crea una copia de seguridad del archivo/etc/fstab de hello antes de modificarla.</span><span class="sxs-lookup"><span data-stu-id="b1405-154">It is also recommended that a backup of hello /etc/fstab file is created before editing.</span></span>
> 
> 

<span data-ttu-id="b1405-155">A continuación, abra hello **/etcetera/fstab** archivo en un editor de texto:</span><span class="sxs-lookup"><span data-stu-id="b1405-155">Next, open hello **/etc/fstab** file in a text editor:</span></span>

```bash
sudo vi /etc/fstab
```

<span data-ttu-id="b1405-156">En este ejemplo, utilizamos Hola UUID valor para hello nueva **/dev/sdc1** dispositivo que se creó en los pasos anteriores de Hola y el punto de montaje de hello **/datadrive**.</span><span class="sxs-lookup"><span data-stu-id="b1405-156">In this example, we use hello UUID value for hello new **/dev/sdc1** device that was created in hello previous steps, and hello mountpoint **/datadrive**.</span></span> <span data-ttu-id="b1405-157">Agregar Hola siguiente línea toohello final de hello **/etcetera/fstab** archivo:</span><span class="sxs-lookup"><span data-stu-id="b1405-157">Add hello following line toohello end of hello **/etc/fstab** file:</span></span>

```bash
UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,nofail   1   2
```

> [!NOTE]
> <span data-ttu-id="b1405-158">Más adelante quitar un disco de datos sin necesidad de editar fstab podría producir Hola VM toofail tooboot.</span><span class="sxs-lookup"><span data-stu-id="b1405-158">Later removing a data disk without editing fstab could cause hello VM toofail tooboot.</span></span> <span data-ttu-id="b1405-159">Mayoría de las distribuciones proporciona cualquier hello `nofail` o `nobootwait` fstab opciones.</span><span class="sxs-lookup"><span data-stu-id="b1405-159">Most distributions provide either hello `nofail` and/or `nobootwait` fstab options.</span></span> <span data-ttu-id="b1405-160">Estas opciones permiten un tooboot sistema aunque hello tiene un error toomount al arrancar el sistema.</span><span class="sxs-lookup"><span data-stu-id="b1405-160">These options allow a system tooboot even if hello disk fails toomount at boot time.</span></span> <span data-ttu-id="b1405-161">Consulte la documentación de su distribución para obtener más información sobre estos parámetros.</span><span class="sxs-lookup"><span data-stu-id="b1405-161">Consult your distribution's documentation for more information on these parameters.</span></span>
> 
> <span data-ttu-id="b1405-162">Hola **nofail** opción garantiza que Hola VM inicie aunque Hola filesystem está dañado o disco hello no existe en tiempo de arranque.</span><span class="sxs-lookup"><span data-stu-id="b1405-162">hello **nofail** option ensures that hello VM starts even if hello filesystem is corrupt or hello disk does not exist at boot time.</span></span> <span data-ttu-id="b1405-163">Sin esta opción, se puede encontrar un comportamiento tal y como se describe en [no SSH tooLinux VM debido a errores de tooFSTAB](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/)</span><span class="sxs-lookup"><span data-stu-id="b1405-163">Without this option, you may encounter behavior as described in [Cannot SSH tooLinux VM due tooFSTAB errors](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/)</span></span>

### <a name="trimunmap-support-for-linux-in-azure"></a><span data-ttu-id="b1405-164">Compatibilidad de TRIM/UNMAP con Linux en Azure</span><span class="sxs-lookup"><span data-stu-id="b1405-164">TRIM/UNMAP support for Linux in Azure</span></span>
<span data-ttu-id="b1405-165">Algunos los kernels de Linux admiten TRIM y UNMAP operaciones toodiscard los bloques sin utilizar en el disco de Hola.</span><span class="sxs-lookup"><span data-stu-id="b1405-165">Some Linux kernels support TRIM/UNMAP operations toodiscard unused blocks on hello disk.</span></span> <span data-ttu-id="b1405-166">Esto es especialmente útil en almacenamiento estándar tooinform Azure que elimina páginas ya no son válidos y se pueden descartar.</span><span class="sxs-lookup"><span data-stu-id="b1405-166">This is primarily useful in standard storage tooinform Azure that deleted pages are no longer valid and can be discarded.</span></span> <span data-ttu-id="b1405-167">Esto puede suponer un ahorro de dinero si crea archivos grandes y, a continuación, los elimina.</span><span class="sxs-lookup"><span data-stu-id="b1405-167">This can save cost if you create large files and then delete them.</span></span>

<span data-ttu-id="b1405-168">Hay dos maneras tooenable TRIM se admiten en la VM de Linux.</span><span class="sxs-lookup"><span data-stu-id="b1405-168">There are two ways tooenable TRIM support in your Linux VM.</span></span> <span data-ttu-id="b1405-169">Como es habitual, consulte la distribución de hello enfoque recomendado:</span><span class="sxs-lookup"><span data-stu-id="b1405-169">As usual, consult your distribution for hello recommended approach:</span></span>

* <span data-ttu-id="b1405-170">Hola de uso `discard` montar opción en `/etc/fstab`, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="b1405-170">Use hello `discard` mount option in `/etc/fstab`, for example:</span></span>

    ```bash
    UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,discard   1   2
    ```
* <span data-ttu-id="b1405-171">En algunos Hola casos `discard` opción podría tener implicaciones de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="b1405-171">In some cases hello `discard` option may have performance implications.</span></span> <span data-ttu-id="b1405-172">Como alternativa, puede ejecutar hello `fstrim` comando manualmente desde la línea de comandos de hello, o agréguela tooyour crontab toorun con regularidad:</span><span class="sxs-lookup"><span data-stu-id="b1405-172">Alternatively, you can run hello `fstrim` command manually from hello command line, or add it tooyour crontab toorun regularly:</span></span>
  
    <span data-ttu-id="b1405-173">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="b1405-173">**Ubuntu**</span></span>
  
    ```bash
    sudo apt-get install util-linux
    sudo fstrim /datadrive
    ```
  
    <span data-ttu-id="b1405-174">**RHEL/CentOS**</span><span class="sxs-lookup"><span data-stu-id="b1405-174">**RHEL/CentOS**</span></span>

    ```bash
    sudo yum install util-linux
    sudo fstrim /datadrive
    ```

## <a name="troubleshooting"></a><span data-ttu-id="b1405-175">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="b1405-175">Troubleshooting</span></span>
[!INCLUDE [virtual-machines-linux-lunzero](../../../includes/virtual-machines-linux-lunzero.md)]

## <a name="next-steps"></a><span data-ttu-id="b1405-176">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b1405-176">Next Steps</span></span>
* <span data-ttu-id="b1405-177">Recuerde que el nuevo disco no es disponible toohello máquina virtual si se reinicia a menos que escriba esa información tooyour [fstab](http://en.wikipedia.org/wiki/Fstab) archivo.</span><span class="sxs-lookup"><span data-stu-id="b1405-177">Remember, that your new disk is not available toohello VM if it reboots unless you write that information tooyour [fstab](http://en.wikipedia.org/wiki/Fstab) file.</span></span>
* <span data-ttu-id="b1405-178">tooensure la VM de Linux está configurado correctamente, revisión hello [optimizar el rendimiento del equipo Linux](optimization.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) recomendaciones.</span><span class="sxs-lookup"><span data-stu-id="b1405-178">tooensure your Linux VM is configured correctly, review hello [Optimize your Linux machine performance](optimization.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) recommendations.</span></span>
* <span data-ttu-id="b1405-179">Amplíe la capacidad de almacenamiento mediante la adición de discos adicionales y [configure RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) para obtener un mayor rendimiento.</span><span class="sxs-lookup"><span data-stu-id="b1405-179">Expand your storage capacity by adding additional disks and [configure RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for additional performance.</span></span>

