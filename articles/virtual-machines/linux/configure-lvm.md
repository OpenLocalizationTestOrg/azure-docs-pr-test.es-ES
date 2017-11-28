---
title: "Configuración de LVM en una máquina virtual que ejecuta Linux | Microsoft Docs"
description: Aprenda a configurar LVM en Linux en Azure.
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
ms.openlocfilehash: 7926627aaa3f0da935131f491d927ab5cb4b35c9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="configure-lvm-on-a-linux-vm-in-azure"></a><span data-ttu-id="21fa4-103">Configuración del LVM en una máquina virtual Linux en Azure</span><span class="sxs-lookup"><span data-stu-id="21fa4-103">Configure LVM on a Linux VM in Azure</span></span>
<span data-ttu-id="21fa4-104">Este documento describe cómo configurar el administrador de volúmenes lógicos (LVM, Logical Volume Manager) en una máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="21fa4-104">This document will discuss how to configure Logical Volume Manager (LVM) in your Azure virtual machine.</span></span> <span data-ttu-id="21fa4-105">Aunque el LVM se puede configurar en cualquier disco conectado a la máquina virtual, de forma predeterminada, la mayoría de las imágenes de nube no tendrá el LVM configurado en el disco del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="21fa4-105">While it is feasible to configure LVM on any disk attached to the virtual machine, by default most cloud images will not have LVM configured on the OS disk.</span></span> <span data-ttu-id="21fa4-106">El motivo es evitar problemas con los grupos de volúmenes duplicados si el disco del sistema operativo se conecta en algún momento a otra máquina virtual de la misma distribución y tipo, es decir, durante un escenario de recuperación.</span><span class="sxs-lookup"><span data-stu-id="21fa4-106">This is to prevent problems with duplicate volume groups if the OS disk is ever attached to another VM of the same distribution and type, i.e. during a recovery scenario.</span></span> <span data-ttu-id="21fa4-107">Por lo tanto, se recomienda usar el LVM únicamente en los discos de datos.</span><span class="sxs-lookup"><span data-stu-id="21fa4-107">Therefore it is recommended only to use LVM on the data disks.</span></span>

## <a name="linear-vs-striped-logical-volumes"></a><span data-ttu-id="21fa4-108">Volúmenes lógicos lineales frente a seccionados</span><span class="sxs-lookup"><span data-stu-id="21fa4-108">Linear vs. striped logical volumes</span></span>
<span data-ttu-id="21fa4-109">El LVM se puede utilizar para combinar diversos discos físicos en un único volumen de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="21fa4-109">LVM can be used to combine a number of physical disks into a single storage volume.</span></span> <span data-ttu-id="21fa4-110">De forma predeterminada, el LVM suele crear volúmenes lógicos lineales, lo que significa que el almacenamiento físico se concatena todo junto.</span><span class="sxs-lookup"><span data-stu-id="21fa4-110">By default LVM will usually create linear logical volumes, which means that the physical storage is concatenated together.</span></span> <span data-ttu-id="21fa4-111">En este caso, las operaciones de lectura y escritura normalmente solo se enviarán a un único disco.</span><span class="sxs-lookup"><span data-stu-id="21fa4-111">In this case read/write operations will typically only be sent to a single disk.</span></span> <span data-ttu-id="21fa4-112">En cambio, también podemos crear volúmenes lógicos seccionados en los que las lecturas y escrituras se distribuyan en varios discos del grupo de volúmenes (es decir, similar a RAID0).</span><span class="sxs-lookup"><span data-stu-id="21fa4-112">In contrast, we can also create striped logical volumes where reads and writes are distributed to multiple disks contained in the volume group (i.e. similar to RAID0).</span></span> <span data-ttu-id="21fa4-113">Por motivos de rendimiento, es probable que deba seccionar los volúmenes lógicos para que las lecturas y escrituras utilicen todos los discos de datos conectados.</span><span class="sxs-lookup"><span data-stu-id="21fa4-113">For performance reasons it is likely you will want to stripe your logical volumes so that reads and writes utilize all your attached data disks.</span></span>

<span data-ttu-id="21fa4-114">Este documento describe cómo combinar varios discos de datos en un único grupo de volúmenes y crear un volumen lógico seccionado.</span><span class="sxs-lookup"><span data-stu-id="21fa4-114">This document will describe how to combine several data disks into a single volume group, and then create a striped logical volume.</span></span> <span data-ttu-id="21fa4-115">Los pasos siguientes están en cierto modo generalizados para que funcionen con la mayoría de las distribuciones.</span><span class="sxs-lookup"><span data-stu-id="21fa4-115">The steps below are somewhat generalized to work with most distributions.</span></span> <span data-ttu-id="21fa4-116">En la mayoría de los casos, las utilidades y los flujos de trabajo para la administración de LVM en Azure no se diferencian en esencia de los de otros entornos.</span><span class="sxs-lookup"><span data-stu-id="21fa4-116">In most cases the utilities and workflows for managing LVM on Azure are not fundamentally different than other environments.</span></span> <span data-ttu-id="21fa4-117">Como de costumbre, consulte a su proveedor de Linux con el fin de obtener la documentación y los procedimientos recomendados para usar el LVM en una distribución en particular.</span><span class="sxs-lookup"><span data-stu-id="21fa4-117">As usual, please also consult your Linux vendor for documentation and best practices for using LVM with your particular distribution.</span></span>

## <a name="attaching-data-disks"></a><span data-ttu-id="21fa4-118">Conexión de discos de datos</span><span class="sxs-lookup"><span data-stu-id="21fa4-118">Attaching data disks</span></span>
<span data-ttu-id="21fa4-119">Normalmente, cuando utilice el LVM, conviene comenzar al menos dos discos de datos vacíos.</span><span class="sxs-lookup"><span data-stu-id="21fa4-119">One will usually want to start with two or more empty data disks when using LVM.</span></span> <span data-ttu-id="21fa4-120">Según sus requisitos de E/S, puede decidir asociar discos que estén almacenados en nuestro almacenamiento estándar con hasta 500 E/S por segundo por disco o Almacenamiento Premium con hasta 5000 E/S por segundo por disco.</span><span class="sxs-lookup"><span data-stu-id="21fa4-120">Based on your IO needs, you can choose to attach disks that are stored in our Standard Storage, with up to 500 IO/ps per disk or our Premium storage with up to 5000 IO/ps per disk.</span></span> <span data-ttu-id="21fa4-121">En este artículo no entramaremos en detalles sobre cómo asociar discos de datos a una máquina virtual Linux.</span><span class="sxs-lookup"><span data-stu-id="21fa4-121">This article will not go into detail on how to provision and attach data disks to a Linux virtual machine.</span></span> <span data-ttu-id="21fa4-122">Consulte el artículo de Microsoft Azure sobre la [conexión de un disco](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) para obtener instrucciones detalladas sobre cómo conectar un disco de datos vacío a una máquina virtual Linux en Azure.</span><span class="sxs-lookup"><span data-stu-id="21fa4-122">Please see the Microsoft Azure article [attach a disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for detailed instructions on how to attach an empty data disk to a Linux virtual machine on Azure.</span></span>

## <a name="install-the-lvm-utilities"></a><span data-ttu-id="21fa4-123">Instalación de las utilidades del LVM</span><span class="sxs-lookup"><span data-stu-id="21fa4-123">Install the LVM utilities</span></span>
* <span data-ttu-id="21fa4-124">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="21fa4-124">**Ubuntu**</span></span>

    ```bash  
    sudo apt-get update
    sudo apt-get install lvm2
    ```

* <span data-ttu-id="21fa4-125">**RHEL, CentOS y Oracle Linux**</span><span class="sxs-lookup"><span data-stu-id="21fa4-125">**RHEL, CentOS & Oracle Linux**</span></span>

    ```bash   
    sudo yum install lvm2
    ```

* <span data-ttu-id="21fa4-126">**12 SLES y openSUSE**</span><span class="sxs-lookup"><span data-stu-id="21fa4-126">**SLES 12 and openSUSE**</span></span>

    ```bash   
    sudo zypper install lvm2
    ```

* <span data-ttu-id="21fa4-127">**SLES 11**</span><span class="sxs-lookup"><span data-stu-id="21fa4-127">**SLES 11**</span></span>

    ```bash   
    sudo zypper install lvm2
    ```

    <span data-ttu-id="21fa4-128">En SLES11 también debe editar `/etc/sysconfig/lvm` y establecer `LVM_ACTIVATED_ON_DISCOVERED` en "habilitar":</span><span class="sxs-lookup"><span data-stu-id="21fa4-128">On SLES11 you must also edit `/etc/sysconfig/lvm` and set `LVM_ACTIVATED_ON_DISCOVERED` to "enable":</span></span>

    ```sh   
    LVM_ACTIVATED_ON_DISCOVERED="enable" 
    ```

## <a name="configure-lvm"></a><span data-ttu-id="21fa4-129">Configuración del LVM</span><span class="sxs-lookup"><span data-stu-id="21fa4-129">Configure LVM</span></span>
<span data-ttu-id="21fa4-130">En esta guía, se presupone la conexión de tres discos de datos, a los que se llamará `/dev/sdc`, `/dev/sdd` y `/dev/sde`.</span><span class="sxs-lookup"><span data-stu-id="21fa4-130">In this guide we will assume you have attached three data disks, which we'll refer to as `/dev/sdc`, `/dev/sdd` and `/dev/sde`.</span></span> <span data-ttu-id="21fa4-131">Tenga en cuenta que estos podrían no presentar siempre los mismos nombres de ruta de acceso en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="21fa4-131">Note that these may not always be the same path names in your VM.</span></span> <span data-ttu-id="21fa4-132">Puede ejecutar`sudo fdisk -l`o un comando similar para ver la lista de los discos disponibles.</span><span class="sxs-lookup"><span data-stu-id="21fa4-132">You can run '`sudo fdisk -l`' or similar command to list your available disks.</span></span>

1. <span data-ttu-id="21fa4-133">Prepare los volúmenes físicos:</span><span class="sxs-lookup"><span data-stu-id="21fa4-133">Prepare the physical volumes:</span></span>

    ```bash    
    sudo pvcreate /dev/sd[cde]
    Physical volume "/dev/sdc" successfully created
    Physical volume "/dev/sdd" successfully created
    Physical volume "/dev/sde" successfully created
    ```

2. <span data-ttu-id="21fa4-134">Cree un grupo de volúmenes.</span><span class="sxs-lookup"><span data-stu-id="21fa4-134">Create a volume group.</span></span> <span data-ttu-id="21fa4-135">En este ejemplo, el grupo de volúmenes se llamará `data-vg01`:</span><span class="sxs-lookup"><span data-stu-id="21fa4-135">In this example we are calling the volume group `data-vg01`:</span></span>

    ```bash    
    sudo vgcreate data-vg01 /dev/sd[cde]
    Volume group "data-vg01" successfully created
    ```

3. <span data-ttu-id="21fa4-136">Cree los volúmenes lógicos.</span><span class="sxs-lookup"><span data-stu-id="21fa4-136">Create the logical volume(s).</span></span> <span data-ttu-id="21fa4-137">El comando siguiente creará un único volumen lógico llamado `data-lv01` para abarcar todo el grupo de volúmenes, pero tenga en cuenta que también se pueden crear varios volúmenes lógicos dentro del grupo de volúmenes.</span><span class="sxs-lookup"><span data-stu-id="21fa4-137">The command below we will create a single logical volume called `data-lv01` to span the entire volume group, but note that it is also feasible to create multiple logical volumes in the volume group.</span></span>

    ```bash   
    sudo lvcreate --extents 100%FREE --stripes 3 --name data-lv01 data-vg01
    Logical volume "data-lv01" created.
    ```

4. <span data-ttu-id="21fa4-138">Formatee el volumen lógico.</span><span class="sxs-lookup"><span data-stu-id="21fa4-138">Format the logical volume</span></span>

    ```bash  
    sudo mkfs -t ext4 /dev/data-vg01/data-lv01
    ```
   
   > [!NOTE]
   > <span data-ttu-id="21fa4-139">En SLES11, utilice `-t ext3` en vez de ext4.</span><span class="sxs-lookup"><span data-stu-id="21fa4-139">With SLES11 use `-t ext3` instead of ext4.</span></span> <span data-ttu-id="21fa4-140">SLES11 admite únicamente el acceso de solo lectura a los sistemas de archivos ext4.</span><span class="sxs-lookup"><span data-stu-id="21fa4-140">SLES11 only supports read-only access to ext4 filesystems.</span></span>

## <a name="add-the-new-file-system-to-etcfstab"></a><span data-ttu-id="21fa4-141">Incorporación del nuevo sistema de archivos a /etc/fstab</span><span class="sxs-lookup"><span data-stu-id="21fa4-141">Add the new file system to /etc/fstab</span></span>
> [!IMPORTANT]
> <span data-ttu-id="21fa4-142">La edición incorrecta del archivo `/etc/fstab` puede tener como resultado un sistema que no se pueda arrancar.</span><span class="sxs-lookup"><span data-stu-id="21fa4-142">Improperly editing the `/etc/fstab` file could result in an unbootable system.</span></span> <span data-ttu-id="21fa4-143">Si no está seguro, consulte la documentación de distribución para obtener información sobre cómo editar correctamente ese archivo.</span><span class="sxs-lookup"><span data-stu-id="21fa4-143">If unsure, please refer to the distribution's documentation for information on how to properly edit this file.</span></span> <span data-ttu-id="21fa4-144">También se recomienda realizar una copia de seguridad del archivo `/etc/fstab` antes de editarlo.</span><span class="sxs-lookup"><span data-stu-id="21fa4-144">It is also recommended that a backup of the `/etc/fstab` file is created before editing.</span></span>

1. <span data-ttu-id="21fa4-145">Cree el punto de montaje deseado para el nuevo sistema de archivos, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="21fa4-145">Create the desired mount point for your new file system, for example:</span></span>

    ```bash  
    sudo mkdir /data
    ```

2. <span data-ttu-id="21fa4-146">Busque la ruta de acceso del volumen lógico.</span><span class="sxs-lookup"><span data-stu-id="21fa4-146">Locate the logical volume path</span></span>

    ```bash    
    lvdisplay
    --- Logical volume ---
    LV Path                /dev/data-vg01/data-lv01
    ....
    ```

3. <span data-ttu-id="21fa4-147">Abra `/etc/fstab` en un editor de texto y agregue una entrada al nuevo sistema de archivos, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="21fa4-147">Open `/etc/fstab` in a text editor and add an entry for the new file system, for example:</span></span>

    ```bash    
    /dev/data-vg01/data-lv01  /data  ext4  defaults  0  2
    ```   
    <span data-ttu-id="21fa4-148">A continuación, guarde y cierre `/etc/fstab`.</span><span class="sxs-lookup"><span data-stu-id="21fa4-148">Then, save and close `/etc/fstab`.</span></span>

4. <span data-ttu-id="21fa4-149">Compruebe que la entrada `/etc/fstab` es correcta:</span><span class="sxs-lookup"><span data-stu-id="21fa4-149">Test that the `/etc/fstab` entry is correct:</span></span>

    ```bash    
    sudo mount -a
    ```

    <span data-ttu-id="21fa4-150">Si este comando genera un mensaje de error, compruebe la sintaxis del archivo `/etc/fstab`.</span><span class="sxs-lookup"><span data-stu-id="21fa4-150">If this command results in an error message please check the syntax in the `/etc/fstab` file.</span></span>
   
    <span data-ttu-id="21fa4-151">A continuación, ejecute el comando `mount` para garantizar el montaje del sistema de archivos:</span><span class="sxs-lookup"><span data-stu-id="21fa4-151">Next run the `mount` command to ensure the file system is mounted:</span></span>

    ```bash    
    mount
    ......
    /dev/mapper/data--vg01-data--lv01 on /data type ext4 (rw)
    ```

5. <span data-ttu-id="21fa4-152">(Opcional) Parámetros de arranque a prueba de errores en `/etc/fstab`</span><span class="sxs-lookup"><span data-stu-id="21fa4-152">(Optional) Failsafe boot parameters in `/etc/fstab`</span></span>
   
    <span data-ttu-id="21fa4-153">Muchas distribuciones incluyen los parámetros de montaje `nobootwait` o `nofail` que pueden agregarse al archivo `/etc/fstab`.</span><span class="sxs-lookup"><span data-stu-id="21fa4-153">Many distributions include either the `nobootwait` or `nofail` mount parameters that may be added to the `/etc/fstab` file.</span></span> <span data-ttu-id="21fa4-154">Estos parámetros admiten errores al montar un sistema de archivos concreto y permiten que el sistema Linux continúe iniciándose incluso aunque no pueda montar correctamente el sistema de archivos RAID.</span><span class="sxs-lookup"><span data-stu-id="21fa4-154">These parameters allow for failures when mounting a particular file system and allow the Linux system to continue to boot even if it is unable to properly mount the RAID file system.</span></span> <span data-ttu-id="21fa4-155">Consulte la documentación de su distribución para obtener más información sobre estos parámetros.</span><span class="sxs-lookup"><span data-stu-id="21fa4-155">Please refer to your distribution's documentation for more information on these parameters.</span></span>
   
    <span data-ttu-id="21fa4-156">Ejemplo (Ubuntu):</span><span class="sxs-lookup"><span data-stu-id="21fa4-156">Example (Ubuntu):</span></span>

    ```bash 
    /dev/data-vg01/data-lv01  /data  ext4  defaults,nobootwait  0  2
    ```

## <a name="trimunmap-support"></a><span data-ttu-id="21fa4-157">Compatibilidad con TRIM y UNMAP</span><span class="sxs-lookup"><span data-stu-id="21fa4-157">TRIM/UNMAP support</span></span>
<span data-ttu-id="21fa4-158">Algunos kernels de Linux admiten operaciones TRIM/UNMAP para descartar bloques no usados del disco.</span><span class="sxs-lookup"><span data-stu-id="21fa4-158">Some Linux kernels support TRIM/UNMAP operations to discard unused blocks on the disk.</span></span> <span data-ttu-id="21fa4-159">Estas operaciones son especialmente útiles en el almacenamiento estándar para informar a Azure de que las páginas eliminadas ya no son válidas y se pueden descartar.</span><span class="sxs-lookup"><span data-stu-id="21fa4-159">These operations are primarily useful in standard storage to inform Azure that deleted pages are no longer valid and can be discarded.</span></span> <span data-ttu-id="21fa4-160">El descarte de páginas puede suponer un ahorro de dinero si crea archivos grandes y, a continuación, los elimina.</span><span class="sxs-lookup"><span data-stu-id="21fa4-160">Discarding pages can save cost if you create large files and then delete them.</span></span>

<span data-ttu-id="21fa4-161">Hay dos maneras de habilitar la compatibilidad con TRIM en su máquina virtual Linux.</span><span class="sxs-lookup"><span data-stu-id="21fa4-161">There are two ways to enable TRIM support in your Linux VM.</span></span> <span data-ttu-id="21fa4-162">Como es habitual, consulte la documentación de distribución para ver el enfoque recomendado:</span><span class="sxs-lookup"><span data-stu-id="21fa4-162">As usual, consult your distribution for the recommended approach:</span></span>

- <span data-ttu-id="21fa4-163">Use la opción de montaje `discard` en `/etc/fstab`, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="21fa4-163">Use the `discard` mount option in `/etc/fstab`, for example:</span></span>

    ```bash 
    /dev/data-vg01/data-lv01  /data  ext4  defaults,discard  0  2
    ```

- <span data-ttu-id="21fa4-164">En algunos casos, la opción `discard` podría tener afectar al rendimiento.</span><span class="sxs-lookup"><span data-stu-id="21fa4-164">In some cases the `discard` option may have performance implications.</span></span> <span data-ttu-id="21fa4-165">Como alternativa, puede ejecutar el comando `fstrim` manualmente desde la línea de comandos o agregarlo a su crontab para ejecutar con regularidad:</span><span class="sxs-lookup"><span data-stu-id="21fa4-165">Alternatively, you can run the `fstrim` command manually from the command line, or add it to your crontab to run regularly:</span></span>

    <span data-ttu-id="21fa4-166">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="21fa4-166">**Ubuntu**</span></span>

    ```bash 
    # sudo apt-get install util-linux
    # sudo fstrim /datadrive
    ```

    <span data-ttu-id="21fa4-167">**RHEL/CentOS**</span><span class="sxs-lookup"><span data-stu-id="21fa4-167">**RHEL/CentOS**</span></span>

    ```bash 
    # sudo yum install util-linux
    # sudo fstrim /datadrive
    ```
