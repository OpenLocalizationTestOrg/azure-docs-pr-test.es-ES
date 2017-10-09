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
# <a name="configure-lvm-on-a-linux-vm-in-azure"></a><span data-ttu-id="af534-103">Configuración del LVM en una máquina virtual Linux en Azure</span><span class="sxs-lookup"><span data-stu-id="af534-103">Configure LVM on a Linux VM in Azure</span></span>
<span data-ttu-id="af534-104">Este documento se describe cómo tooconfigure el Administrador de volúmenes lógicos (LVM) en la máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="af534-104">This document will discuss how tooconfigure Logical Volume Manager (LVM) in your Azure virtual machine.</span></span> <span data-ttu-id="af534-105">Aunque es posible tooconfigure que LVM en cualquier disco conectado toohello virtual machine, de forma predeterminada en la nube mayoría imágenes no tendrán LVM configurado en hello disco del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="af534-105">While it is feasible tooconfigure LVM on any disk attached toohello virtual machine, by default most cloud images will not have LVM configured on hello OS disk.</span></span> <span data-ttu-id="af534-106">Esto es tooprevent problemas con grupos de volúmenes duplicados si Hola disco del sistema operativo es alguna vez asociado tooanother VM de hello misma distribución y el tipo, es decir, durante un escenario de recuperación.</span><span class="sxs-lookup"><span data-stu-id="af534-106">This is tooprevent problems with duplicate volume groups if hello OS disk is ever attached tooanother VM of hello same distribution and type, i.e. during a recovery scenario.</span></span> <span data-ttu-id="af534-107">Por lo tanto, se recomienda solo toouse LVM en discos de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="af534-107">Therefore it is recommended only toouse LVM on hello data disks.</span></span>

## <a name="linear-vs-striped-logical-volumes"></a><span data-ttu-id="af534-108">Volúmenes lógicos lineales frente a seccionados</span><span class="sxs-lookup"><span data-stu-id="af534-108">Linear vs. striped logical volumes</span></span>
<span data-ttu-id="af534-109">LVM puede ser toocombine usa un número de discos físicos en un único volumen de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="af534-109">LVM can be used toocombine a number of physical disks into a single storage volume.</span></span> <span data-ttu-id="af534-110">De forma predeterminada LVM suele crear volúmenes lógicos lineales, lo que significa que almacenamiento físico de Hola se concatena juntos.</span><span class="sxs-lookup"><span data-stu-id="af534-110">By default LVM will usually create linear logical volumes, which means that hello physical storage is concatenated together.</span></span> <span data-ttu-id="af534-111">En este caso las operaciones de lectura/escritura normalmente solo se enviarán tooa uno de los discos.</span><span class="sxs-lookup"><span data-stu-id="af534-111">In this case read/write operations will typically only be sent tooa single disk.</span></span> <span data-ttu-id="af534-112">En cambio, también podemos crear un volumen seccionado lógico donde lecturas y escrituras son discos toomultiple distribuida contenidos en el grupo de volúmenes de hello (es decir, tooRAID0 similar).</span><span class="sxs-lookup"><span data-stu-id="af534-112">In contrast, we can also create striped logical volumes where reads and writes are distributed toomultiple disks contained in hello volume group (i.e. similar tooRAID0).</span></span> <span data-ttu-id="af534-113">Por motivos de rendimiento, es probable que desee toostripe los volúmenes lógicos para que las lecturas y escrituras utilizan todos los discos de datos adjuntos.</span><span class="sxs-lookup"><span data-stu-id="af534-113">For performance reasons it is likely you will want toostripe your logical volumes so that reads and writes utilize all your attached data disks.</span></span>

<span data-ttu-id="af534-114">Este documento se describe cómo toocombine datos de varios discos en un único grupo de volúmenes y, a continuación, crear un volumen seccionado lógico.</span><span class="sxs-lookup"><span data-stu-id="af534-114">This document will describe how toocombine several data disks into a single volume group, and then create a striped logical volume.</span></span> <span data-ttu-id="af534-115">Hola pasos son algo generalizado toowork con la mayoría de las distribuciones.</span><span class="sxs-lookup"><span data-stu-id="af534-115">hello steps below are somewhat generalized toowork with most distributions.</span></span> <span data-ttu-id="af534-116">Hola la mayoría de casos utilidades y flujos de trabajo para administrar LVM en Azure no son fundamentalmente diferentes de otros entornos.</span><span class="sxs-lookup"><span data-stu-id="af534-116">In most cases hello utilities and workflows for managing LVM on Azure are not fundamentally different than other environments.</span></span> <span data-ttu-id="af534-117">Como de costumbre, consulte a su proveedor de Linux con el fin de obtener la documentación y los procedimientos recomendados para usar el LVM en una distribución en particular.</span><span class="sxs-lookup"><span data-stu-id="af534-117">As usual, please also consult your Linux vendor for documentation and best practices for using LVM with your particular distribution.</span></span>

## <a name="attaching-data-disks"></a><span data-ttu-id="af534-118">Conexión de discos de datos</span><span class="sxs-lookup"><span data-stu-id="af534-118">Attaching data disks</span></span>
<span data-ttu-id="af534-119">Uno normalmente es conveniente toostart con dos o más discos de datos vacíos cuando se usa LVM.</span><span class="sxs-lookup"><span data-stu-id="af534-119">One will usually want toostart with two or more empty data disks when using LVM.</span></span> <span data-ttu-id="af534-120">Según sus necesidades de E/S, puede elegir tooattach discos que están almacenados en el almacenamiento estándar, con una E/S de too500/ps por disco o el almacenamiento Premium con una E/S de too5000/ps por disco.</span><span class="sxs-lookup"><span data-stu-id="af534-120">Based on your IO needs, you can choose tooattach disks that are stored in our Standard Storage, with up too500 IO/ps per disk or our Premium storage with up too5000 IO/ps per disk.</span></span> <span data-ttu-id="af534-121">En este artículo no entra en detalles acerca de cómo tooprovision y asociar la máquina virtual de datos discos tooa Linux.</span><span class="sxs-lookup"><span data-stu-id="af534-121">This article will not go into detail on how tooprovision and attach data disks tooa Linux virtual machine.</span></span> <span data-ttu-id="af534-122">Vea artículo de Microsoft Azure hello [conectar un disco](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) para obtener instrucciones detalladas sobre cómo tooattach un datos vacíos disco de máquina virtual de Linux tooa en Azure.</span><span class="sxs-lookup"><span data-stu-id="af534-122">Please see hello Microsoft Azure article [attach a disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for detailed instructions on how tooattach an empty data disk tooa Linux virtual machine on Azure.</span></span>

## <a name="install-hello-lvm-utilities"></a><span data-ttu-id="af534-123">Instalar utilidades LVM Hola</span><span class="sxs-lookup"><span data-stu-id="af534-123">Install hello LVM utilities</span></span>
* <span data-ttu-id="af534-124">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="af534-124">**Ubuntu**</span></span>

    ```bash  
    sudo apt-get update
    sudo apt-get install lvm2
    ```

* <span data-ttu-id="af534-125">**RHEL, CentOS y Oracle Linux**</span><span class="sxs-lookup"><span data-stu-id="af534-125">**RHEL, CentOS & Oracle Linux**</span></span>

    ```bash   
    sudo yum install lvm2
    ```

* <span data-ttu-id="af534-126">**12 SLES y openSUSE**</span><span class="sxs-lookup"><span data-stu-id="af534-126">**SLES 12 and openSUSE**</span></span>

    ```bash   
    sudo zypper install lvm2
    ```

* <span data-ttu-id="af534-127">**SLES 11**</span><span class="sxs-lookup"><span data-stu-id="af534-127">**SLES 11**</span></span>

    ```bash   
    sudo zypper install lvm2
    ```

    <span data-ttu-id="af534-128">En SLES11 también debe editar `/etc/sysconfig/lvm` y establecer `LVM_ACTIVATED_ON_DISCOVERED` demasiado "Habilitar":</span><span class="sxs-lookup"><span data-stu-id="af534-128">On SLES11 you must also edit `/etc/sysconfig/lvm` and set `LVM_ACTIVATED_ON_DISCOVERED` too"enable":</span></span>

    ```sh   
    LVM_ACTIVATED_ON_DISCOVERED="enable" 
    ```

## <a name="configure-lvm"></a><span data-ttu-id="af534-129">Configuración del LVM</span><span class="sxs-lookup"><span data-stu-id="af534-129">Configure LVM</span></span>
<span data-ttu-id="af534-130">En esta guía se presupone que ha adjuntado tres discos de datos, lo que nos referiremos tooas `/dev/sdc`, `/dev/sdd` y `/dev/sde`.</span><span class="sxs-lookup"><span data-stu-id="af534-130">In this guide we will assume you have attached three data disks, which we'll refer tooas `/dev/sdc`, `/dev/sdd` and `/dev/sde`.</span></span> <span data-ttu-id="af534-131">Tenga en cuenta que estos pueden no ser siempre Hola mismos nombres de ruta de acceso en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="af534-131">Note that these may not always be hello same path names in your VM.</span></span> <span data-ttu-id="af534-132">Puede ejecutar '`sudo fdisk -l`' o similar toolist comando los discos disponibles.</span><span class="sxs-lookup"><span data-stu-id="af534-132">You can run '`sudo fdisk -l`' or similar command toolist your available disks.</span></span>

1. <span data-ttu-id="af534-133">Preparar volúmenes físicos hello:</span><span class="sxs-lookup"><span data-stu-id="af534-133">Prepare hello physical volumes:</span></span>

    ```bash    
    sudo pvcreate /dev/sd[cde]
    Physical volume "/dev/sdc" successfully created
    Physical volume "/dev/sdd" successfully created
    Physical volume "/dev/sde" successfully created
    ```

2. <span data-ttu-id="af534-134">Cree un grupo de volúmenes.</span><span class="sxs-lookup"><span data-stu-id="af534-134">Create a volume group.</span></span> <span data-ttu-id="af534-135">En este ejemplo estamos llamando a grupo de volúmenes de Hola `data-vg01`:</span><span class="sxs-lookup"><span data-stu-id="af534-135">In this example we are calling hello volume group `data-vg01`:</span></span>

    ```bash    
    sudo vgcreate data-vg01 /dev/sd[cde]
    Volume group "data-vg01" successfully created
    ```

3. <span data-ttu-id="af534-136">Crear volúmenes lógicos de Hola.</span><span class="sxs-lookup"><span data-stu-id="af534-136">Create hello logical volume(s).</span></span> <span data-ttu-id="af534-137">Hello comando a continuación se creará un único volumen lógico llama `data-lv01` toospan Hola todo grupo de volumen, pero tenga en cuenta que también es posible toocreate varios volúmenes lógicos en el grupo de volúmenes de Hola.</span><span class="sxs-lookup"><span data-stu-id="af534-137">hello command below we will create a single logical volume called `data-lv01` toospan hello entire volume group, but note that it is also feasible toocreate multiple logical volumes in hello volume group.</span></span>

    ```bash   
    sudo lvcreate --extents 100%FREE --stripes 3 --name data-lv01 data-vg01
    Logical volume "data-lv01" created.
    ```

4. <span data-ttu-id="af534-138">Volumen lógico de Hola de formato</span><span class="sxs-lookup"><span data-stu-id="af534-138">Format hello logical volume</span></span>

    ```bash  
    sudo mkfs -t ext4 /dev/data-vg01/data-lv01
    ```
   
   > [!NOTE]
   > <span data-ttu-id="af534-139">En SLES11, utilice `-t ext3` en vez de ext4.</span><span class="sxs-lookup"><span data-stu-id="af534-139">With SLES11 use `-t ext3` instead of ext4.</span></span> <span data-ttu-id="af534-140">SLES11 sólo es compatible con sistemas de archivos de tooext4 de acceso de solo lectura.</span><span class="sxs-lookup"><span data-stu-id="af534-140">SLES11 only supports read-only access tooext4 filesystems.</span></span>

## <a name="add-hello-new-file-system-tooetcfstab"></a><span data-ttu-id="af534-141">Agregar Hola nuevo archivo sistema demasiado/etcetera/fstab</span><span class="sxs-lookup"><span data-stu-id="af534-141">Add hello new file system too/etc/fstab</span></span>
> [!IMPORTANT]
> <span data-ttu-id="af534-142">Edición incorrectamente hello `/etc/fstab` archivo podría provocar un reinicio del sistema.</span><span class="sxs-lookup"><span data-stu-id="af534-142">Improperly editing hello `/etc/fstab` file could result in an unbootable system.</span></span> <span data-ttu-id="af534-143">Si no está seguro, por favor, consulte la documentación de la distribución de toohello para obtener información sobre cómo tooproperly editar este archivo.</span><span class="sxs-lookup"><span data-stu-id="af534-143">If unsure, please refer toohello distribution's documentation for information on how tooproperly edit this file.</span></span> <span data-ttu-id="af534-144">También es recomendable una copia de seguridad de hello `/etc/fstab` se crea el archivo antes de editar.</span><span class="sxs-lookup"><span data-stu-id="af534-144">It is also recommended that a backup of hello `/etc/fstab` file is created before editing.</span></span>

1. <span data-ttu-id="af534-145">Crear punto de montaje de hello deseado para el nuevo sistema de archivos, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="af534-145">Create hello desired mount point for your new file system, for example:</span></span>

    ```bash  
    sudo mkdir /data
    ```

2. <span data-ttu-id="af534-146">Buscar ruta de acceso del volumen lógico Hola</span><span class="sxs-lookup"><span data-stu-id="af534-146">Locate hello logical volume path</span></span>

    ```bash    
    lvdisplay
    --- Logical volume ---
    LV Path                /dev/data-vg01/data-lv01
    ....
    ```

3. <span data-ttu-id="af534-147">Abra `/etc/fstab` en un editor de texto y agregue una entrada para el nuevo sistema de archivos hello, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="af534-147">Open `/etc/fstab` in a text editor and add an entry for hello new file system, for example:</span></span>

    ```bash    
    /dev/data-vg01/data-lv01  /data  ext4  defaults  0  2
    ```   
    <span data-ttu-id="af534-148">A continuación, guarde y cierre `/etc/fstab`.</span><span class="sxs-lookup"><span data-stu-id="af534-148">Then, save and close `/etc/fstab`.</span></span>

4. <span data-ttu-id="af534-149">Probar esa hello `/etc/fstab` es correcta la entrada:</span><span class="sxs-lookup"><span data-stu-id="af534-149">Test that hello `/etc/fstab` entry is correct:</span></span>

    ```bash    
    sudo mount -a
    ```

    <span data-ttu-id="af534-150">Si este comando da como resultado un mensaje de error Compruebe la sintaxis de Hola Hola `/etc/fstab` archivo.</span><span class="sxs-lookup"><span data-stu-id="af534-150">If this command results in an error message please check hello syntax in hello `/etc/fstab` file.</span></span>
   
    <span data-ttu-id="af534-151">A continuación ejecute hello `mount` está montado el sistema de archivos de comandos tooensure hello:</span><span class="sxs-lookup"><span data-stu-id="af534-151">Next run hello `mount` command tooensure hello file system is mounted:</span></span>

    ```bash    
    mount
    ......
    /dev/mapper/data--vg01-data--lv01 on /data type ext4 (rw)
    ```

5. <span data-ttu-id="af534-152">(Opcional) Parámetros de arranque a prueba de errores en `/etc/fstab`</span><span class="sxs-lookup"><span data-stu-id="af534-152">(Optional) Failsafe boot parameters in `/etc/fstab`</span></span>
   
    <span data-ttu-id="af534-153">Número de distribuciones incluye cualquier hello `nobootwait` o `nofail` montar los parámetros que se pueden agregar toohello `/etc/fstab` archivo.</span><span class="sxs-lookup"><span data-stu-id="af534-153">Many distributions include either hello `nobootwait` or `nofail` mount parameters that may be added toohello `/etc/fstab` file.</span></span> <span data-ttu-id="af534-154">Estos parámetros permiten errores al montar un sistema de archivos determinado y permiten Hola Linux sistema toocontinue tooboot incluso si es sistema de archivos de tooproperly no se puede montar Hola RAID.</span><span class="sxs-lookup"><span data-stu-id="af534-154">These parameters allow for failures when mounting a particular file system and allow hello Linux system toocontinue tooboot even if it is unable tooproperly mount hello RAID file system.</span></span> <span data-ttu-id="af534-155">Por favor, consulte la documentación de la distribución de tooyour para obtener más información acerca de estos parámetros.</span><span class="sxs-lookup"><span data-stu-id="af534-155">Please refer tooyour distribution's documentation for more information on these parameters.</span></span>
   
    <span data-ttu-id="af534-156">Ejemplo (Ubuntu):</span><span class="sxs-lookup"><span data-stu-id="af534-156">Example (Ubuntu):</span></span>

    ```bash 
    /dev/data-vg01/data-lv01  /data  ext4  defaults,nobootwait  0  2
    ```

## <a name="trimunmap-support"></a><span data-ttu-id="af534-157">Compatibilidad con TRIM y UNMAP</span><span class="sxs-lookup"><span data-stu-id="af534-157">TRIM/UNMAP support</span></span>
<span data-ttu-id="af534-158">Algunos los kernels de Linux admiten TRIM y UNMAP operaciones toodiscard los bloques sin utilizar en el disco de Hola.</span><span class="sxs-lookup"><span data-stu-id="af534-158">Some Linux kernels support TRIM/UNMAP operations toodiscard unused blocks on hello disk.</span></span> <span data-ttu-id="af534-159">Estas operaciones son sobre todo útiles en almacenamiento estándar tooinform Azure que elimina páginas ya no son válidos y se pueden descartar.</span><span class="sxs-lookup"><span data-stu-id="af534-159">These operations are primarily useful in standard storage tooinform Azure that deleted pages are no longer valid and can be discarded.</span></span> <span data-ttu-id="af534-160">El descarte de páginas puede suponer un ahorro de dinero si crea archivos grandes y, a continuación, los elimina.</span><span class="sxs-lookup"><span data-stu-id="af534-160">Discarding pages can save cost if you create large files and then delete them.</span></span>

<span data-ttu-id="af534-161">Hay dos maneras tooenable TRIM se admiten en la VM de Linux.</span><span class="sxs-lookup"><span data-stu-id="af534-161">There are two ways tooenable TRIM support in your Linux VM.</span></span> <span data-ttu-id="af534-162">Como es habitual, consulte la distribución de hello enfoque recomendado:</span><span class="sxs-lookup"><span data-stu-id="af534-162">As usual, consult your distribution for hello recommended approach:</span></span>

- <span data-ttu-id="af534-163">Hola de uso `discard` montar opción en `/etc/fstab`, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="af534-163">Use hello `discard` mount option in `/etc/fstab`, for example:</span></span>

    ```bash 
    /dev/data-vg01/data-lv01  /data  ext4  defaults,discard  0  2
    ```

- <span data-ttu-id="af534-164">En algunos Hola casos `discard` opción podría tener implicaciones de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="af534-164">In some cases hello `discard` option may have performance implications.</span></span> <span data-ttu-id="af534-165">Como alternativa, puede ejecutar hello `fstrim` comando manualmente desde la línea de comandos de hello, o agréguela tooyour crontab toorun con regularidad:</span><span class="sxs-lookup"><span data-stu-id="af534-165">Alternatively, you can run hello `fstrim` command manually from hello command line, or add it tooyour crontab toorun regularly:</span></span>

    <span data-ttu-id="af534-166">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="af534-166">**Ubuntu**</span></span>

    ```bash 
    # sudo apt-get install util-linux
    # sudo fstrim /datadrive
    ```

    <span data-ttu-id="af534-167">**RHEL/CentOS**</span><span class="sxs-lookup"><span data-stu-id="af534-167">**RHEL/CentOS**</span></span>

    ```bash 
    # sudo yum install util-linux
    # sudo fstrim /datadrive
    ```
