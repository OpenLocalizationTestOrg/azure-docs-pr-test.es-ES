---
title: "Configuración del software RAID en una máquina virtual Linux | Microsoft Docs"
description: Aprenda a utilizar mdadm para configurar RAID en Linux en Azure.
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
ms.openlocfilehash: 12f540a700fbf85e579e8aadc9f6def039299ff7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="configure-software-raid-on-linux"></a><span data-ttu-id="30372-103">Configuración del software RAID en Linux</span><span class="sxs-lookup"><span data-stu-id="30372-103">Configure Software RAID on Linux</span></span>
<span data-ttu-id="30372-104">Es un escenario habitual usar el software RAID en máquinas virtuales con Linux en Azure para presentar varios discos de datos conectados como un único dispositivo RAID.</span><span class="sxs-lookup"><span data-stu-id="30372-104">It's a common scenario to use software RAID on Linux virtual machines in Azure to present multiple attached data disks as a single RAID device.</span></span> <span data-ttu-id="30372-105">Se puede utilizar normalmente para aumentar el rendimiento y permitir una capacidad de proceso mejorada en comparación con el uso de un solo disco.</span><span class="sxs-lookup"><span data-stu-id="30372-105">Typically this can be used to improve performance and allow for improved throughput compared to using just a single disk.</span></span>

## <a name="attaching-data-disks"></a><span data-ttu-id="30372-106">Conexión de discos de datos</span><span class="sxs-lookup"><span data-stu-id="30372-106">Attaching data disks</span></span>
<span data-ttu-id="30372-107">Se necesitan dos o más discos de datos vacíos para configurar un dispositivo RAID.</span><span class="sxs-lookup"><span data-stu-id="30372-107">Two or more empty data disks are needed to configure a RAID device.</span></span>  <span data-ttu-id="30372-108">La razón principal para crear un dispositivo RAID es mejorar el rendimiento de la E/S de disco.</span><span class="sxs-lookup"><span data-stu-id="30372-108">The primary reason for creating a RAID device is to improve performance of your disk IO.</span></span>  <span data-ttu-id="30372-109">Según sus requisitos de E/S, puede decidir asociar discos que estén almacenados en nuestro almacenamiento estándar con hasta 500 E/S por segundo por disco o Almacenamiento Premium con hasta 5000 E/S por segundo por disco.</span><span class="sxs-lookup"><span data-stu-id="30372-109">Based on your IO needs, you can choose to attach disks that are stored in our Standard Storage, with up to 500 IO/ps per disk or our Premium storage with up to 5000 IO/ps per disk.</span></span> <span data-ttu-id="30372-110">En este artículo no entramaremos en detalles sobre cómo asociar discos de datos a una máquina virtual Linux.</span><span class="sxs-lookup"><span data-stu-id="30372-110">This article does not go into detail on how to provision and attach data disks to a Linux virtual machine.</span></span>  <span data-ttu-id="30372-111">Consulte el artículo de Microsoft Azure sobre la [conexión de un disco](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) para obtener instrucciones detalladas sobre cómo conectar un disco de datos vacío a una máquina virtual Linux en Azure.</span><span class="sxs-lookup"><span data-stu-id="30372-111">See the Microsoft Azure article [attach a disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for detailed instructions on how to attach an empty data disk to a Linux virtual machine on Azure.</span></span>

## <a name="install-the-mdadm-utility"></a><span data-ttu-id="30372-112">Instalación de la utilidad mdadm</span><span class="sxs-lookup"><span data-stu-id="30372-112">Install the mdadm utility</span></span>
* <span data-ttu-id="30372-113">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="30372-113">**Ubuntu**</span></span>
```bash
sudo apt-get update
sudo apt-get install mdadm
```

* <span data-ttu-id="30372-114">**CentOS y Oracle Linux**</span><span class="sxs-lookup"><span data-stu-id="30372-114">**CentOS & Oracle Linux**</span></span>
```bash
sudo yum install mdadm
```

* <span data-ttu-id="30372-115">**SLES y openSUSE**</span><span class="sxs-lookup"><span data-stu-id="30372-115">**SLES and openSUSE**</span></span>
```bash  
zypper install mdadm
```

## <a name="create-the-disk-partitions"></a><span data-ttu-id="30372-116">Creación de las particiones de disco</span><span class="sxs-lookup"><span data-stu-id="30372-116">Create the disk partitions</span></span>
<span data-ttu-id="30372-117">En este ejemplo, vamos a crear una única partición de disco en /dev/sdc.</span><span class="sxs-lookup"><span data-stu-id="30372-117">In this example, we create a single disk partition on /dev/sdc.</span></span> <span data-ttu-id="30372-118">Por tanto, la partición de disco nueva se llamará /dev/sdc1.</span><span class="sxs-lookup"><span data-stu-id="30372-118">The new disk partition will be called /dev/sdc1.</span></span>

1. <span data-ttu-id="30372-119">Inicie `fdisk` para empezar a crear particiones.</span><span class="sxs-lookup"><span data-stu-id="30372-119">Start `fdisk` to begin creating partitions</span></span>

    ```bash
    sudo fdisk /dev/sdc
    Device contains neither a valid DOS partition table, nor Sun, SGI or OSF disklabel
    Building a new DOS disklabel with disk identifier 0xa34cb70c.
    Changes will remain in memory only, until you decide to write them.
    After that, of course, the previous content won't be recoverable.

    WARNING: DOS-compatible mode is deprecated. It's strongly recommended to
                    switch off the mode (command 'c') and change display units to
                    sectors (command 'u').
    ```

2. <span data-ttu-id="30372-120">Presione ' n ' en el símbolo del sistema para crear un  **n** partición ew:</span><span class="sxs-lookup"><span data-stu-id="30372-120">Press 'n' at the prompt to create a **n**ew partition:</span></span>

    ```bash
    Command (m for help): n
    ```

3. <span data-ttu-id="30372-121">A continuación, presione "p" para crear una partición **p**rincipal:</span><span class="sxs-lookup"><span data-stu-id="30372-121">Next, press 'p' to create a **p**rimary partition:</span></span>

    ```bash 
    Command action
            e   extended
            p   primary partition (1-4)
    ```

4. <span data-ttu-id="30372-122">Presione "1" para seleccionar el número de la partición 1:</span><span class="sxs-lookup"><span data-stu-id="30372-122">Press '1' to select partition number 1:</span></span>

    ```bash
    Partition number (1-4): 1
    ```

5. <span data-ttu-id="30372-123">Seleccione el punto de partida de la partición nueva o presione `<enter>` para aceptar el valor predeterminado para colocar la partición al principio del espacio disponible en la unidad:</span><span class="sxs-lookup"><span data-stu-id="30372-123">Select the starting point of the new partition, or press `<enter>` to accept the default to place the partition at the beginning of the free space on the drive:</span></span>

    ```bash   
    First cylinder (1-1305, default 1):
    Using default value 1
    ```

6. <span data-ttu-id="30372-124">Seleccione el tamaño de la partición; por ejemplo, escriba "+10G" para crear una partición de 10 gigabytes.</span><span class="sxs-lookup"><span data-stu-id="30372-124">Select the size of the partition, for example type '+10G' to create a 10 gigabyte partition.</span></span> <span data-ttu-id="30372-125">O simplemente presione `<enter>` para crear una única partición que extienda la unidad completa:</span><span class="sxs-lookup"><span data-stu-id="30372-125">Or, press `<enter>` create a single partition that spans the entire drive:</span></span>

    ```bash   
    Last cylinder, +cylinders or +size{K,M,G} (1-1305, default 1305): 
    Using default value 1305
    ```

7. <span data-ttu-id="30372-126">A continuación, cambie el identificador y el **t**ipo de la partición del identificador predeterminado "83" (Linux) por el identificador "fd" (Linux raid auto):</span><span class="sxs-lookup"><span data-stu-id="30372-126">Next, change the ID and **t**ype of the partition from the default ID '83' (Linux) to ID 'fd' (Linux raid auto):</span></span>

    ```bash  
    Command (m for help): t
    Selected partition 1
    Hex code (type L to list codes): fd
    ```

8. <span data-ttu-id="30372-127">Por último, escriba la tabla de particiones en la unidad y cierre fdisk:</span><span class="sxs-lookup"><span data-stu-id="30372-127">Finally, write the partition table to the drive and exit fdisk:</span></span>

    ```bash   
    Command (m for help): w
    The partition table has been altered!
    ```

## <a name="create-the-raid-array"></a><span data-ttu-id="30372-128">Creación de la matriz RAID</span><span class="sxs-lookup"><span data-stu-id="30372-128">Create the RAID array</span></span>
1. <span data-ttu-id="30372-129">En el siguiente ejemplo, se "seccionan" (RAID nivel 0) tres particiones ubicadas en tres discos de datos independientes (sdc1, sdd1 y sde1).</span><span class="sxs-lookup"><span data-stu-id="30372-129">The following example will "stripe" (RAID level 0) three partitions located on three separate data disks (sdc1, sdd1, sde1).</span></span>  <span data-ttu-id="30372-130">Después de ejecutar este comando, se creará un nuevo dispositivo RAID llamado **/dev/md127** .</span><span class="sxs-lookup"><span data-stu-id="30372-130">After running this command a new RAID device called **/dev/md127** is created.</span></span> <span data-ttu-id="30372-131">Tenga en cuenta también que, si estos discos de datos formaban parte anteriormente de otra matriz RAID inactiva, puede ser necesario agregar el parámetro `--force` al comando `mdadm`:</span><span class="sxs-lookup"><span data-stu-id="30372-131">Also note that if these data disks we previously part of another defunct RAID array it may be necessary to add the `--force` parameter to the `mdadm` command:</span></span>

    ```bash  
    sudo mdadm --create /dev/md127 --level 0 --raid-devices 3 \
        /dev/sdc1 /dev/sdd1 /dev/sde1
    ```

2. <span data-ttu-id="30372-132">Cree el sistema de archivos en el nuevo dispositivo RAID.</span><span class="sxs-lookup"><span data-stu-id="30372-132">Create the file system on the new RAID device</span></span>
   
    <span data-ttu-id="30372-133">a.</span><span class="sxs-lookup"><span data-stu-id="30372-133">a.</span></span> <span data-ttu-id="30372-134">**CentOS, Oracle Linux, SLES 12, openSUSE y Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="30372-134">**CentOS, Oracle Linux, SLES 12, openSUSE, and Ubuntu**</span></span>

    ```bash   
    sudo mkfs -t ext4 /dev/md127
    ```
   
    <span data-ttu-id="30372-135">b.</span><span class="sxs-lookup"><span data-stu-id="30372-135">b.</span></span> <span data-ttu-id="30372-136">**SLES 11**</span><span class="sxs-lookup"><span data-stu-id="30372-136">**SLES 11**</span></span>

    ```bash
    sudo mkfs -t ext3 /dev/md127
    ```
   
    <span data-ttu-id="30372-137">c.</span><span class="sxs-lookup"><span data-stu-id="30372-137">c.</span></span> <span data-ttu-id="30372-138">**SLES 11**: habilitar boot.md y crear mdadm.conf</span><span class="sxs-lookup"><span data-stu-id="30372-138">**SLES 11** - enable boot.md and create mdadm.conf</span></span>

    ```bash
    sudo -i chkconfig --add boot.md
    sudo echo 'DEVICE /dev/sd*[0-9]' >> /etc/mdadm.conf
    ```
   
   > [!NOTE]
   > <span data-ttu-id="30372-139">Es posible que sea necesario reiniciar después de realizar estos cambios en los sistemas SUSE.</span><span class="sxs-lookup"><span data-stu-id="30372-139">A reboot may be required after making these changes on SUSE systems.</span></span> <span data-ttu-id="30372-140">Este paso *no* es necesario en SLES 12.</span><span class="sxs-lookup"><span data-stu-id="30372-140">This step is *not* required on SLES 12.</span></span>
   > 
   > 

## <a name="add-the-new-file-system-to-etcfstab"></a><span data-ttu-id="30372-141">Incorporación del nuevo sistema de archivos a /etc/fstab</span><span class="sxs-lookup"><span data-stu-id="30372-141">Add the new file system to /etc/fstab</span></span>
> [!IMPORTANT]
> <span data-ttu-id="30372-142">La edición incorrecta del archivo /etc/fstab puede tener como resultado un sistema que no se pueda arrancar.</span><span class="sxs-lookup"><span data-stu-id="30372-142">Improperly editing the /etc/fstab file could result in an unbootable system.</span></span> <span data-ttu-id="30372-143">Si no está seguro, consulte la documentación de distribución para obtener información sobre cómo editar correctamente ese archivo.</span><span class="sxs-lookup"><span data-stu-id="30372-143">If unsure, refer to the distribution's documentation for information on how to properly edit this file.</span></span> <span data-ttu-id="30372-144">También se recomienda realizar una copia de seguridad del archivo /etc/fstab antes de editarlo.</span><span class="sxs-lookup"><span data-stu-id="30372-144">It is also recommended that a backup of the /etc/fstab file is created before editing.</span></span>

1. <span data-ttu-id="30372-145">Cree el punto de montaje deseado para el nuevo sistema de archivos, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="30372-145">Create the desired mount point for your new file system, for example:</span></span>

    ```bash
    sudo mkdir /data
    ```
2. <span data-ttu-id="30372-146">Al editar /etc/fstab, el **UUID** debe usarse para hacer referencia al sistema de archivos en lugar de al nombre del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="30372-146">When editing /etc/fstab, the **UUID** should be used to reference the file system rather than the device name.</span></span>  <span data-ttu-id="30372-147">Use la utilidad `blkid` para determinar el UUID del nuevo sistema de archivos:</span><span class="sxs-lookup"><span data-stu-id="30372-147">Use the `blkid` utility to determine the UUID for the new file system:</span></span>

    ```bash   
    sudo /sbin/blkid
    ...........
    /dev/md127: UUID="aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee" TYPE="ext4"
    ```

3. <span data-ttu-id="30372-148">Abra /etc/fstab en un editor de texto y agregue una entrada al nuevo sistema de archivos, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="30372-148">Open /etc/fstab in a text editor and add an entry for the new file system, for example:</span></span>

    ```bash   
    UUID=aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext4  defaults  0  2
    ```
   
    <span data-ttu-id="30372-149">O bien, en **SLES 11**:</span><span class="sxs-lookup"><span data-stu-id="30372-149">Or on **SLES 11**:</span></span>

    ```bash
    /dev/disk/by-uuid/aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext3  defaults  0  2
    ```
   
    <span data-ttu-id="30372-150">A continuación, guarde y cierre /etc/fstab.</span><span class="sxs-lookup"><span data-stu-id="30372-150">Then, save and close /etc/fstab.</span></span>

4. <span data-ttu-id="30372-151">Pruebe que la entrada /etc/fstab sea correcta:</span><span class="sxs-lookup"><span data-stu-id="30372-151">Test that the /etc/fstab entry is correct:</span></span>

    ```bash  
    sudo mount -a
    ```

    <span data-ttu-id="30372-152">Si este comando genera un mensaje de error, compruebe la sintaxis del archivo /etc/fstab.</span><span class="sxs-lookup"><span data-stu-id="30372-152">If this command results in an error message, please check the syntax in the /etc/fstab file.</span></span>
   
    <span data-ttu-id="30372-153">A continuación, ejecute el comando `mount` para garantizar el montaje del sistema de archivos:</span><span class="sxs-lookup"><span data-stu-id="30372-153">Next run the `mount` command to ensure the file system is mounted:</span></span>

    ```bash   
    mount
    .................
    /dev/md127 on /data type ext4 (rw)
    ```

5. <span data-ttu-id="30372-154">(Opcional) Parámetros de arranque a prueba de errores</span><span class="sxs-lookup"><span data-stu-id="30372-154">(Optional) Failsafe Boot Parameters</span></span>
   
    <span data-ttu-id="30372-155">**Configuración de fstab**</span><span class="sxs-lookup"><span data-stu-id="30372-155">**fstab configuration**</span></span>
   
    <span data-ttu-id="30372-156">Muchas distribuciones incluyen los parámetros de montaje `nobootwait` o `nofail` que pueden agregarse al archivo /etc/fstab.</span><span class="sxs-lookup"><span data-stu-id="30372-156">Many distributions include either the `nobootwait` or `nofail` mount parameters that may be added to the /etc/fstab file.</span></span> <span data-ttu-id="30372-157">Estos parámetros admiten errores al montar un sistema de archivos concreto y permiten que el sistema Linux continúe iniciándose incluso aunque no pueda montar correctamente el sistema de archivos RAID.</span><span class="sxs-lookup"><span data-stu-id="30372-157">These parameters allow for failures when mounting a particular file system and allow the Linux system to continue to boot even if it is unable to properly mount the RAID file system.</span></span> <span data-ttu-id="30372-158">Consulte la documentación de su distribución para obtener más información sobre estos parámetros.</span><span class="sxs-lookup"><span data-stu-id="30372-158">Refer to your distribution's documentation for more information on these parameters.</span></span>
   
    <span data-ttu-id="30372-159">Ejemplo (Ubuntu):</span><span class="sxs-lookup"><span data-stu-id="30372-159">Example (Ubuntu):</span></span>

    ```bash  
    UUID=aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext4  defaults,nobootwait  0  2
    ```   

    <span data-ttu-id="30372-160">**Parámetros de inicio de Linux**</span><span class="sxs-lookup"><span data-stu-id="30372-160">**Linux boot parameters**</span></span>
   
    <span data-ttu-id="30372-161">Además de los parámetros anteriores, el parámetro de kernel`bootdegraded=true`puede permitir que el sistema se inicie incluso si RAID se percibe como dañado o degradado, por ejemplo si una unidad de datos se quita accidentalmente de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="30372-161">In addition to the above parameters, the kernel parameter "`bootdegraded=true`" can allow the system to boot even if the RAID is perceived as damaged or degraded, for example if a data drive is inadvertently removed from the virtual machine.</span></span> <span data-ttu-id="30372-162">De manera predeterminada, esto podría resultar en un sistema no iniciable.</span><span class="sxs-lookup"><span data-stu-id="30372-162">By default this could also result in a non-bootable system.</span></span>
   
    <span data-ttu-id="30372-163">Consulte la documentación sobre la distribución para obtener información acerca de cómo editar correctamente los parámetros de kernel.</span><span class="sxs-lookup"><span data-stu-id="30372-163">Please refer to your distribution's documentation on how to properly edit kernel parameters.</span></span> <span data-ttu-id="30372-164">Por ejemplo, en muchas distribuciones (CentOS, Oracle Linux y SLES 11), estos parámetros pueden agregarse manualmente al archivo "`/boot/grub/menu.lst`".</span><span class="sxs-lookup"><span data-stu-id="30372-164">For example, in many distributions (CentOS, Oracle Linux, SLES 11) these parameters may be added manually to the "`/boot/grub/menu.lst`" file.</span></span>  <span data-ttu-id="30372-165">En Ubuntu, este parámetro puede agregarse a la variable `GRUB_CMDLINE_LINUX_DEFAULT` en "/etc/default/grub".</span><span class="sxs-lookup"><span data-stu-id="30372-165">On Ubuntu this parameter can be added to the `GRUB_CMDLINE_LINUX_DEFAULT` variable on "/etc/default/grub".</span></span>


## <a name="trimunmap-support"></a><span data-ttu-id="30372-166">Compatibilidad con TRIM y UNMAP</span><span class="sxs-lookup"><span data-stu-id="30372-166">TRIM/UNMAP support</span></span>
<span data-ttu-id="30372-167">Algunos kernels de Linux admiten operaciones TRIM/UNMAP para descartar bloques no usados del disco.</span><span class="sxs-lookup"><span data-stu-id="30372-167">Some Linux kernels support TRIM/UNMAP operations to discard unused blocks on the disk.</span></span> <span data-ttu-id="30372-168">Estas operaciones son especialmente útiles en el almacenamiento estándar para informar a Azure de que las páginas eliminadas ya no son válidas y se pueden descartar.</span><span class="sxs-lookup"><span data-stu-id="30372-168">These operations are primarily useful in standard storage to inform Azure that deleted pages are no longer valid and can be discarded.</span></span> <span data-ttu-id="30372-169">El descarte de páginas puede suponer un ahorro de dinero si crea archivos grandes y, a continuación, los elimina.</span><span class="sxs-lookup"><span data-stu-id="30372-169">Discarding pages can save cost if you create large files and then delete them.</span></span>

> [!NOTE]
> <span data-ttu-id="30372-170">Es posible que RAID no pueda emitir comandos de descartar si el tamaño del fragmento de la matriz se establece en un valor inferior al predeterminado (512 kB).</span><span class="sxs-lookup"><span data-stu-id="30372-170">RAID may not issue discard commands if the chunk size for the array is set to less than the default (512KB).</span></span> <span data-ttu-id="30372-171">Esto se debe a que la granularidad de UNMAP del host también es de 512 kB.</span><span class="sxs-lookup"><span data-stu-id="30372-171">This is because the unmap granularity on the Host is also 512KB.</span></span> <span data-ttu-id="30372-172">Si ha modificado el tamaño del fragmento de la matriz a través del parámetro `--chunk=` de mdadm, el kernel puede pasar por alto las solicitudes de TRIM y UNMAP.</span><span class="sxs-lookup"><span data-stu-id="30372-172">If you modified the array's chunk size via mdadm's `--chunk=` parameter, then TRIM/unmap requests may be ignored by the kernel.</span></span>

<span data-ttu-id="30372-173">Hay dos maneras de habilitar la compatibilidad con TRIM en su máquina virtual Linux.</span><span class="sxs-lookup"><span data-stu-id="30372-173">There are two ways to enable TRIM support in your Linux VM.</span></span> <span data-ttu-id="30372-174">Como es habitual, consulte la documentación de distribución para ver el enfoque recomendado:</span><span class="sxs-lookup"><span data-stu-id="30372-174">As usual, consult your distribution for the recommended approach:</span></span>

- <span data-ttu-id="30372-175">Use la opción de montaje `discard` en `/etc/fstab`, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="30372-175">Use the `discard` mount option in `/etc/fstab`, for example:</span></span>

    ```bash
    UUID=aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext4  defaults,discard  0  2
    ```

- <span data-ttu-id="30372-176">En algunos casos, la opción `discard` podría tener afectar al rendimiento.</span><span class="sxs-lookup"><span data-stu-id="30372-176">In some cases the `discard` option may have performance implications.</span></span> <span data-ttu-id="30372-177">Como alternativa, puede ejecutar el comando `fstrim` manualmente desde la línea de comandos o agregarlo a su crontab para ejecutar con regularidad:</span><span class="sxs-lookup"><span data-stu-id="30372-177">Alternatively, you can run the `fstrim` command manually from the command line, or add it to your crontab to run regularly:</span></span>

    <span data-ttu-id="30372-178">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="30372-178">**Ubuntu**</span></span>

    ```bash
    # sudo apt-get install util-linux
    # sudo fstrim /data
    ```

    <span data-ttu-id="30372-179">**RHEL/CentOS**</span><span class="sxs-lookup"><span data-stu-id="30372-179">**RHEL/CentOS**</span></span>
    ```bash
    # sudo yum install util-linux
    # sudo fstrim /data
    ```
