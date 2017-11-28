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
# <a name="configure-software-raid-on-linux"></a><span data-ttu-id="53296-103">Configuración del software RAID en Linux</span><span class="sxs-lookup"><span data-stu-id="53296-103">Configure Software RAID on Linux</span></span>
<span data-ttu-id="53296-104">Es un común escenario toouse RAID de software en máquinas virtuales de Linux en Azure toopresent discos varios datos adjuntos como un único dispositivo RAID.</span><span class="sxs-lookup"><span data-stu-id="53296-104">It's a common scenario toouse software RAID on Linux virtual machines in Azure toopresent multiple attached data disks as a single RAID device.</span></span> <span data-ttu-id="53296-105">Normalmente esto puede ser usado tooimprove rendimiento y permiten una mejora en el rendimiento en comparación con toousing solo un único disco.</span><span class="sxs-lookup"><span data-stu-id="53296-105">Typically this can be used tooimprove performance and allow for improved throughput compared toousing just a single disk.</span></span>

## <a name="attaching-data-disks"></a><span data-ttu-id="53296-106">Conexión de discos de datos</span><span class="sxs-lookup"><span data-stu-id="53296-106">Attaching data disks</span></span>
<span data-ttu-id="53296-107">Dos o más discos de datos vacíos son necesario tooconfigure un dispositivo RAID.</span><span class="sxs-lookup"><span data-stu-id="53296-107">Two or more empty data disks are needed tooconfigure a RAID device.</span></span>  <span data-ttu-id="53296-108">Hola principal razón para crear un dispositivo RAID es tooimprove rendimiento de la E/S de disco.</span><span class="sxs-lookup"><span data-stu-id="53296-108">hello primary reason for creating a RAID device is tooimprove performance of your disk IO.</span></span>  <span data-ttu-id="53296-109">Según sus necesidades de E/S, puede elegir tooattach discos que están almacenados en el almacenamiento estándar, con una E/S de too500/ps por disco o el almacenamiento Premium con una E/S de too5000/ps por disco.</span><span class="sxs-lookup"><span data-stu-id="53296-109">Based on your IO needs, you can choose tooattach disks that are stored in our Standard Storage, with up too500 IO/ps per disk or our Premium storage with up too5000 IO/ps per disk.</span></span> <span data-ttu-id="53296-110">En este artículo no entra en detalles acerca de cómo tooprovision y asociar la máquina virtual de datos discos tooa Linux.</span><span class="sxs-lookup"><span data-stu-id="53296-110">This article does not go into detail on how tooprovision and attach data disks tooa Linux virtual machine.</span></span>  <span data-ttu-id="53296-111">Consulte el artículo de Microsoft Azure hello [conectar un disco](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) para obtener instrucciones detalladas sobre cómo tooattach un datos vacíos disco de máquina virtual de Linux tooa en Azure.</span><span class="sxs-lookup"><span data-stu-id="53296-111">See hello Microsoft Azure article [attach a disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for detailed instructions on how tooattach an empty data disk tooa Linux virtual machine on Azure.</span></span>

## <a name="install-hello-mdadm-utility"></a><span data-ttu-id="53296-112">Instalar la utilidad de hello mdadm</span><span class="sxs-lookup"><span data-stu-id="53296-112">Install hello mdadm utility</span></span>
* <span data-ttu-id="53296-113">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="53296-113">**Ubuntu**</span></span>
```bash
sudo apt-get update
sudo apt-get install mdadm
```

* <span data-ttu-id="53296-114">**CentOS y Oracle Linux**</span><span class="sxs-lookup"><span data-stu-id="53296-114">**CentOS & Oracle Linux**</span></span>
```bash
sudo yum install mdadm
```

* <span data-ttu-id="53296-115">**SLES y openSUSE**</span><span class="sxs-lookup"><span data-stu-id="53296-115">**SLES and openSUSE**</span></span>
```bash  
zypper install mdadm
```

## <a name="create-hello-disk-partitions"></a><span data-ttu-id="53296-116">Crear particiones de disco de Hola</span><span class="sxs-lookup"><span data-stu-id="53296-116">Create hello disk partitions</span></span>
<span data-ttu-id="53296-117">En este ejemplo, vamos a crear una única partición de disco en /dev/sdc.</span><span class="sxs-lookup"><span data-stu-id="53296-117">In this example, we create a single disk partition on /dev/sdc.</span></span> <span data-ttu-id="53296-118">nueva partición de disco Hola se llamará /dev/sdc1.</span><span class="sxs-lookup"><span data-stu-id="53296-118">hello new disk partition will be called /dev/sdc1.</span></span>

1. <span data-ttu-id="53296-119">Iniciar `fdisk` toobegin la creación de particiones</span><span class="sxs-lookup"><span data-stu-id="53296-119">Start `fdisk` toobegin creating partitions</span></span>

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

2. <span data-ttu-id="53296-120">Presione ' n ' en hello prompt toocreate una  **n** partición ew:</span><span class="sxs-lookup"><span data-stu-id="53296-120">Press 'n' at hello prompt toocreate a **n**ew partition:</span></span>

    ```bash
    Command (m for help): n
    ```

3. <span data-ttu-id="53296-121">A continuación, presione "p" toocreate una **p**partición primario:</span><span class="sxs-lookup"><span data-stu-id="53296-121">Next, press 'p' toocreate a **p**rimary partition:</span></span>

    ```bash 
    Command action
            e   extended
            p   primary partition (1-4)
    ```

4. <span data-ttu-id="53296-122">Presione '1' número de partición de tooselect 1:</span><span class="sxs-lookup"><span data-stu-id="53296-122">Press '1' tooselect partition number 1:</span></span>

    ```bash
    Partition number (1-4): 1
    ```

5. <span data-ttu-id="53296-123">Seleccione Hola punto inicial de la nueva partición de hello, o presione `<enter>` partición tooaccept Hola predeterminada tooplace hello en principio de Hola de espacio libre de hello en unidad de hello:</span><span class="sxs-lookup"><span data-stu-id="53296-123">Select hello starting point of hello new partition, or press `<enter>` tooaccept hello default tooplace hello partition at hello beginning of hello free space on hello drive:</span></span>

    ```bash   
    First cylinder (1-1305, default 1):
    Using default value 1
    ```

6. <span data-ttu-id="53296-124">Seleccione Hola tamaño de partición de hello, por ejemplo el tipo '+10G' toocreate una partición de 10 gigabytes.</span><span class="sxs-lookup"><span data-stu-id="53296-124">Select hello size of hello partition, for example type '+10G' toocreate a 10 gigabyte partition.</span></span> <span data-ttu-id="53296-125">O bien, presione `<enter>` crear una única partición que abarca la totalidad del disco hello:</span><span class="sxs-lookup"><span data-stu-id="53296-125">Or, press `<enter>` create a single partition that spans hello entire drive:</span></span>

    ```bash   
    Last cylinder, +cylinders or +size{K,M,G} (1-1305, default 1305): 
    Using default value 1305
    ```

7. <span data-ttu-id="53296-126">A continuación, cambie el identificador de Hola y **t**ipo de partición de Hola desde predeterminado Hola Id. '83' (Linux) tooID 'fd' (auto de raid de Linux):</span><span class="sxs-lookup"><span data-stu-id="53296-126">Next, change hello ID and **t**ype of hello partition from hello default ID '83' (Linux) tooID 'fd' (Linux raid auto):</span></span>

    ```bash  
    Command (m for help): t
    Selected partition 1
    Hex code (type L toolist codes): fd
    ```

8. <span data-ttu-id="53296-127">Por último, escribir la unidad de toohello de tabla de partición de Hola y salir de fdisk:</span><span class="sxs-lookup"><span data-stu-id="53296-127">Finally, write hello partition table toohello drive and exit fdisk:</span></span>

    ```bash   
    Command (m for help): w
    hello partition table has been altered!
    ```

## <a name="create-hello-raid-array"></a><span data-ttu-id="53296-128">Crear la matriz RAID Hola</span><span class="sxs-lookup"><span data-stu-id="53296-128">Create hello RAID array</span></span>
1. <span data-ttu-id="53296-129">Hola después will de ejemplo "bandas" (nivel RAID 0) tres particiones ubicadas en tres discos de datos independiente (sdc1, sdd1, sde1).</span><span class="sxs-lookup"><span data-stu-id="53296-129">hello following example will "stripe" (RAID level 0) three partitions located on three separate data disks (sdc1, sdd1, sde1).</span></span>  <span data-ttu-id="53296-130">Después de ejecutar este comando, se creará un nuevo dispositivo RAID llamado **/dev/md127** .</span><span class="sxs-lookup"><span data-stu-id="53296-130">After running this command a new RAID device called **/dev/md127** is created.</span></span> <span data-ttu-id="53296-131">Tenga en cuenta también que si estos datos discos se previamente parte de otra matriz RAID inactivo puede ser necesario tooadd hello `--force` toohello parámetro `mdadm` comando:</span><span class="sxs-lookup"><span data-stu-id="53296-131">Also note that if these data disks we previously part of another defunct RAID array it may be necessary tooadd hello `--force` parameter toohello `mdadm` command:</span></span>

    ```bash  
    sudo mdadm --create /dev/md127 --level 0 --raid-devices 3 \
        /dev/sdc1 /dev/sdd1 /dev/sde1
    ```

2. <span data-ttu-id="53296-132">Crear el sistema de archivos de hello en dispositivo RAID nuevo de Hola</span><span class="sxs-lookup"><span data-stu-id="53296-132">Create hello file system on hello new RAID device</span></span>
   
    <span data-ttu-id="53296-133">a.</span><span class="sxs-lookup"><span data-stu-id="53296-133">a.</span></span> <span data-ttu-id="53296-134">**CentOS, Oracle Linux, SLES 12, openSUSE y Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="53296-134">**CentOS, Oracle Linux, SLES 12, openSUSE, and Ubuntu**</span></span>

    ```bash   
    sudo mkfs -t ext4 /dev/md127
    ```
   
    <span data-ttu-id="53296-135">b.</span><span class="sxs-lookup"><span data-stu-id="53296-135">b.</span></span> <span data-ttu-id="53296-136">**SLES 11**</span><span class="sxs-lookup"><span data-stu-id="53296-136">**SLES 11**</span></span>

    ```bash
    sudo mkfs -t ext3 /dev/md127
    ```
   
    <span data-ttu-id="53296-137">c.</span><span class="sxs-lookup"><span data-stu-id="53296-137">c.</span></span> <span data-ttu-id="53296-138">**SLES 11**: habilitar boot.md y crear mdadm.conf</span><span class="sxs-lookup"><span data-stu-id="53296-138">**SLES 11** - enable boot.md and create mdadm.conf</span></span>

    ```bash
    sudo -i chkconfig --add boot.md
    sudo echo 'DEVICE /dev/sd*[0-9]' >> /etc/mdadm.conf
    ```
   
   > [!NOTE]
   > <span data-ttu-id="53296-139">Es posible que sea necesario reiniciar después de realizar estos cambios en los sistemas SUSE.</span><span class="sxs-lookup"><span data-stu-id="53296-139">A reboot may be required after making these changes on SUSE systems.</span></span> <span data-ttu-id="53296-140">Este paso *no* es necesario en SLES 12.</span><span class="sxs-lookup"><span data-stu-id="53296-140">This step is *not* required on SLES 12.</span></span>
   > 
   > 

## <a name="add-hello-new-file-system-tooetcfstab"></a><span data-ttu-id="53296-141">Agregar Hola nuevo archivo sistema demasiado/etcetera/fstab</span><span class="sxs-lookup"><span data-stu-id="53296-141">Add hello new file system too/etc/fstab</span></span>
> [!IMPORTANT]
> <span data-ttu-id="53296-142">Incorrectamente Editar archivo/etc/fstab de hello podría provocar un reinicio del sistema.</span><span class="sxs-lookup"><span data-stu-id="53296-142">Improperly editing hello /etc/fstab file could result in an unbootable system.</span></span> <span data-ttu-id="53296-143">Si no está seguro, consulte la documentación de la distribución de toohello para obtener información sobre cómo tooproperly editar este archivo.</span><span class="sxs-lookup"><span data-stu-id="53296-143">If unsure, refer toohello distribution's documentation for information on how tooproperly edit this file.</span></span> <span data-ttu-id="53296-144">También se recomienda que se crea una copia de seguridad del archivo/etc/fstab de hello antes de modificarla.</span><span class="sxs-lookup"><span data-stu-id="53296-144">It is also recommended that a backup of hello /etc/fstab file is created before editing.</span></span>

1. <span data-ttu-id="53296-145">Crear punto de montaje de hello deseado para el nuevo sistema de archivos, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="53296-145">Create hello desired mount point for your new file system, for example:</span></span>

    ```bash
    sudo mkdir /data
    ```
2. <span data-ttu-id="53296-146">Al editar/etc/fstab, Hola **UUID** debe ser tooreference usado Hola sistema en lugar de hello dispositivo nombre de archivo.</span><span class="sxs-lookup"><span data-stu-id="53296-146">When editing /etc/fstab, hello **UUID** should be used tooreference hello file system rather than hello device name.</span></span>  <span data-ttu-id="53296-147">Hola de uso `blkid` toodetermine Hola UUID de utilidad para el nuevo sistema de archivos de hello:</span><span class="sxs-lookup"><span data-stu-id="53296-147">Use hello `blkid` utility toodetermine hello UUID for hello new file system:</span></span>

    ```bash   
    sudo /sbin/blkid
    ...........
    /dev/md127: UUID="aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee" TYPE="ext4"
    ```

3. <span data-ttu-id="53296-148">Abra/etc/fstab en un editor de texto y agregue una entrada para el nuevo sistema de archivos hello, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="53296-148">Open /etc/fstab in a text editor and add an entry for hello new file system, for example:</span></span>

    ```bash   
    UUID=aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext4  defaults  0  2
    ```
   
    <span data-ttu-id="53296-149">O bien, en **SLES 11**:</span><span class="sxs-lookup"><span data-stu-id="53296-149">Or on **SLES 11**:</span></span>

    ```bash
    /dev/disk/by-uuid/aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext3  defaults  0  2
    ```
   
    <span data-ttu-id="53296-150">A continuación, guarde y cierre /etc/fstab.</span><span class="sxs-lookup"><span data-stu-id="53296-150">Then, save and close /etc/fstab.</span></span>

4. <span data-ttu-id="53296-151">Prueba que es correcta la entrada / etc/fstab hello:</span><span class="sxs-lookup"><span data-stu-id="53296-151">Test that hello /etc/fstab entry is correct:</span></span>

    ```bash  
    sudo mount -a
    ```

    <span data-ttu-id="53296-152">Si este comando da como resultado un mensaje de error, compruebe la sintaxis de hello en el archivo/etc/fstab de hello.</span><span class="sxs-lookup"><span data-stu-id="53296-152">If this command results in an error message, please check hello syntax in hello /etc/fstab file.</span></span>
   
    <span data-ttu-id="53296-153">A continuación ejecute hello `mount` está montado el sistema de archivos de comandos tooensure hello:</span><span class="sxs-lookup"><span data-stu-id="53296-153">Next run hello `mount` command tooensure hello file system is mounted:</span></span>

    ```bash   
    mount
    .................
    /dev/md127 on /data type ext4 (rw)
    ```

5. <span data-ttu-id="53296-154">(Opcional) Parámetros de arranque a prueba de errores</span><span class="sxs-lookup"><span data-stu-id="53296-154">(Optional) Failsafe Boot Parameters</span></span>
   
    <span data-ttu-id="53296-155">**Configuración de fstab**</span><span class="sxs-lookup"><span data-stu-id="53296-155">**fstab configuration**</span></span>
   
    <span data-ttu-id="53296-156">Número de distribuciones incluye cualquier hello `nobootwait` o `nofail` parámetros que se pueden agregar archivo toohello/etcetera/fstab de montaje.</span><span class="sxs-lookup"><span data-stu-id="53296-156">Many distributions include either hello `nobootwait` or `nofail` mount parameters that may be added toohello /etc/fstab file.</span></span> <span data-ttu-id="53296-157">Estos parámetros permiten errores al montar un sistema de archivos determinado y permiten Hola Linux sistema toocontinue tooboot incluso si es sistema de archivos de tooproperly no se puede montar Hola RAID.</span><span class="sxs-lookup"><span data-stu-id="53296-157">These parameters allow for failures when mounting a particular file system and allow hello Linux system toocontinue tooboot even if it is unable tooproperly mount hello RAID file system.</span></span> <span data-ttu-id="53296-158">Consulte la documentación de la distribución de tooyour para obtener más información acerca de estos parámetros.</span><span class="sxs-lookup"><span data-stu-id="53296-158">Refer tooyour distribution's documentation for more information on these parameters.</span></span>
   
    <span data-ttu-id="53296-159">Ejemplo (Ubuntu):</span><span class="sxs-lookup"><span data-stu-id="53296-159">Example (Ubuntu):</span></span>

    ```bash  
    UUID=aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext4  defaults,nobootwait  0  2
    ```   

    <span data-ttu-id="53296-160">**Parámetros de inicio de Linux**</span><span class="sxs-lookup"><span data-stu-id="53296-160">**Linux boot parameters**</span></span>
   
    <span data-ttu-id="53296-161">En suma toohello por encima de los parámetros, Hola parámetro kernel "`bootdegraded=true`" pueden permitir Hola sistema tooboot incluso si Hola RAID se percibe como dañado o degradado, por ejemplo, si una unidad de datos sin darse cuenta se quita de la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="53296-161">In addition toohello above parameters, hello kernel parameter "`bootdegraded=true`" can allow hello system tooboot even if hello RAID is perceived as damaged or degraded, for example if a data drive is inadvertently removed from hello virtual machine.</span></span> <span data-ttu-id="53296-162">De manera predeterminada, esto podría resultar en un sistema no iniciable.</span><span class="sxs-lookup"><span data-stu-id="53296-162">By default this could also result in a non-bootable system.</span></span>
   
    <span data-ttu-id="53296-163">Por favor, consulte la documentación de la distribución de tooyour en cómo tooproperly editar parámetros de kernel.</span><span class="sxs-lookup"><span data-stu-id="53296-163">Please refer tooyour distribution's documentation on how tooproperly edit kernel parameters.</span></span> <span data-ttu-id="53296-164">Por ejemplo, en muchas distribuciones (CentOS, Oracle Linux SLES 11) estos parámetros pueden agregarse manualmente toohello "`/boot/grub/menu.lst`" archivo.</span><span class="sxs-lookup"><span data-stu-id="53296-164">For example, in many distributions (CentOS, Oracle Linux, SLES 11) these parameters may be added manually toohello "`/boot/grub/menu.lst`" file.</span></span>  <span data-ttu-id="53296-165">En Ubuntu, ejecute este parámetro puede agregarse toohello `GRUB_CMDLINE_LINUX_DEFAULT` variable en "/ etcetera/predeterminado/grub".</span><span class="sxs-lookup"><span data-stu-id="53296-165">On Ubuntu this parameter can be added toohello `GRUB_CMDLINE_LINUX_DEFAULT` variable on "/etc/default/grub".</span></span>


## <a name="trimunmap-support"></a><span data-ttu-id="53296-166">Compatibilidad con TRIM y UNMAP</span><span class="sxs-lookup"><span data-stu-id="53296-166">TRIM/UNMAP support</span></span>
<span data-ttu-id="53296-167">Algunos los kernels de Linux admiten TRIM y UNMAP operaciones toodiscard los bloques sin utilizar en el disco de Hola.</span><span class="sxs-lookup"><span data-stu-id="53296-167">Some Linux kernels support TRIM/UNMAP operations toodiscard unused blocks on hello disk.</span></span> <span data-ttu-id="53296-168">Estas operaciones son sobre todo útiles en almacenamiento estándar tooinform Azure que elimina páginas ya no son válidos y se pueden descartar.</span><span class="sxs-lookup"><span data-stu-id="53296-168">These operations are primarily useful in standard storage tooinform Azure that deleted pages are no longer valid and can be discarded.</span></span> <span data-ttu-id="53296-169">El descarte de páginas puede suponer un ahorro de dinero si crea archivos grandes y, a continuación, los elimina.</span><span class="sxs-lookup"><span data-stu-id="53296-169">Discarding pages can save cost if you create large files and then delete them.</span></span>

> [!NOTE]
> <span data-ttu-id="53296-170">RAID no puede emitir comandos de descarte si se establece el tamaño de fragmento de hello para la matriz de Hola que no requiere herramientas predeterminado de hello (512KB).</span><span class="sxs-lookup"><span data-stu-id="53296-170">RAID may not issue discard commands if hello chunk size for hello array is set tooless than hello default (512KB).</span></span> <span data-ttu-id="53296-171">Esto es porque Hola desasignar granularidad en hello Host también es 512KB.</span><span class="sxs-lookup"><span data-stu-id="53296-171">This is because hello unmap granularity on hello Host is also 512KB.</span></span> <span data-ttu-id="53296-172">Si ha modificado el tamaño del fragmento de la matriz de Hola a través del mdadm `--chunk=` parámetro y, a continuación, RECORTE/anular la asignación de solicitudes pueden omitirse kernel Hola.</span><span class="sxs-lookup"><span data-stu-id="53296-172">If you modified hello array's chunk size via mdadm's `--chunk=` parameter, then TRIM/unmap requests may be ignored by hello kernel.</span></span>

<span data-ttu-id="53296-173">Hay dos maneras tooenable TRIM se admiten en la VM de Linux.</span><span class="sxs-lookup"><span data-stu-id="53296-173">There are two ways tooenable TRIM support in your Linux VM.</span></span> <span data-ttu-id="53296-174">Como es habitual, consulte la distribución de hello enfoque recomendado:</span><span class="sxs-lookup"><span data-stu-id="53296-174">As usual, consult your distribution for hello recommended approach:</span></span>

- <span data-ttu-id="53296-175">Hola de uso `discard` montar opción en `/etc/fstab`, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="53296-175">Use hello `discard` mount option in `/etc/fstab`, for example:</span></span>

    ```bash
    UUID=aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext4  defaults,discard  0  2
    ```

- <span data-ttu-id="53296-176">En algunos Hola casos `discard` opción podría tener implicaciones de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="53296-176">In some cases hello `discard` option may have performance implications.</span></span> <span data-ttu-id="53296-177">Como alternativa, puede ejecutar hello `fstrim` comando manualmente desde la línea de comandos de hello, o agréguela tooyour crontab toorun con regularidad:</span><span class="sxs-lookup"><span data-stu-id="53296-177">Alternatively, you can run hello `fstrim` command manually from hello command line, or add it tooyour crontab toorun regularly:</span></span>

    <span data-ttu-id="53296-178">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="53296-178">**Ubuntu**</span></span>

    ```bash
    # sudo apt-get install util-linux
    # sudo fstrim /data
    ```

    <span data-ttu-id="53296-179">**RHEL/CentOS**</span><span class="sxs-lookup"><span data-stu-id="53296-179">**RHEL/CentOS**</span></span>
    ```bash
    # sudo yum install util-linux
    # sudo fstrim /data
    ```
