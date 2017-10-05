---
title: "Conexión de un disco a una VM de Linux en Azure | Microsoft Docs"
description: "Aprenda a conectar un disco de datos a una máquina virtual Linux mediante el modelo de implementación clásica y a inicializar el disco para que esté preparado para su uso."
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
ms.openlocfilehash: 017ba7197e11c2b222082833d5acabb9e542b762
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-attach-a-data-disk-to-a-linux-virtual-machine"></a><span data-ttu-id="dccb0-103">Acoplamiento de un disco de datos a una máquina virtual Linux</span><span class="sxs-lookup"><span data-stu-id="dccb0-103">How to Attach a Data Disk to a Linux Virtual Machine</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="dccb0-104">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="dccb0-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="dccb0-105">En este artículo se trata el modelo de implementación clásico.</span><span class="sxs-lookup"><span data-stu-id="dccb0-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="dccb0-106">Microsoft recomienda que las implementaciones más recientes usen el modelo del Administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="dccb0-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="dccb0-107">Consulte cómo [conectar un disco de datos mediante el modelo de implementación de Resource Manager](../add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="dccb0-107">See how to [attach a data disk using the Resource Manager deployment model](../add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="dccb0-108">Puede acoplar tanto discos vacíos como discos que contengan datos a las máquinas virtuales de Azure.</span><span class="sxs-lookup"><span data-stu-id="dccb0-108">You can attach both empty disks and disks that contain data to your Azure VMs.</span></span> <span data-ttu-id="dccb0-109">Ambos tipos de discos son archivos .vhd que residen en una cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="dccb0-109">Both types of disks are .vhd files that reside in an Azure storage account.</span></span> <span data-ttu-id="dccb0-110">Como sucede al agregar cualquier disco a una máquina Linux, después de acoplarlo, debe inicializarlo y formatearlo para que esté listo para su uso.</span><span class="sxs-lookup"><span data-stu-id="dccb0-110">As with adding any disk to a Linux machine, after you attach the disk you need to initialize and format it so it's ready for use.</span></span> <span data-ttu-id="dccb0-111">En este artículo se detalla cómo acoplar discos vacíos y discos que ya contengan datos a las máquinas virtuales, así como la forma de inicializar y formatear un disco nuevo.</span><span class="sxs-lookup"><span data-stu-id="dccb0-111">This article details attaching both empty disks and disks already containing data to your VMs, as well as how to then initialize and format a new disk.</span></span>

> [!NOTE]
> <span data-ttu-id="dccb0-112">Es recomendable utilizar uno o varios discos independientes para almacenar los datos de una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="dccb0-112">It's a best practice to use one or more separate disks to store a virtual machine's data.</span></span> <span data-ttu-id="dccb0-113">Al crear una máquina virtual de Azure, esta cuenta con un disco para el sistema operativo y un disco temporal.</span><span class="sxs-lookup"><span data-stu-id="dccb0-113">When you create an Azure virtual machine, it has an operating system disk and a temporary disk.</span></span> <span data-ttu-id="dccb0-114">**No utilice el disco temporal para almacenar datos permanentes.**</span><span class="sxs-lookup"><span data-stu-id="dccb0-114">**Do not use the temporary disk to store persistent data.**</span></span> <span data-ttu-id="dccb0-115">Como señala su nombre, esta ofrece únicamente almacenamiento temporal.</span><span class="sxs-lookup"><span data-stu-id="dccb0-115">As the name implies, it provides temporary storage only.</span></span> <span data-ttu-id="dccb0-116">No ofrece redundancia o copias de seguridad porque no reside en el almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="dccb0-116">It offers no redundancy or backup because it doesn't reside in Azure storage.</span></span>
> <span data-ttu-id="dccb0-117">El Agente de Linux de Azure normalmente administra el disco temporal, y este se monta automáticamente en **/mnt/resource** (o **/mnt** en las imágenes de Ubuntu).</span><span class="sxs-lookup"><span data-stu-id="dccb0-117">The temporary disk is typically managed by the Azure Linux Agent and automatically mounted to **/mnt/resource** (or **/mnt** on Ubuntu images).</span></span> <span data-ttu-id="dccb0-118">Por otro lado, el kernel de Linux podría denominar al disco de datos de forma similar a `/dev/sdc`, y los usuarios necesitan crear particiones, dar formato y montar ese recurso.</span><span class="sxs-lookup"><span data-stu-id="dccb0-118">On the other hand, a data disk might be named by the Linux kernel something like `/dev/sdc`, and you need to partition, format, and mount this resource.</span></span> <span data-ttu-id="dccb0-119">Consulte la [Guía de usuario del Agente de Linux de Azure][Agent] para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="dccb0-119">See the [Azure Linux Agent User Guide][Agent] for details.</span></span>
> 
> 

[!INCLUDE [howto-attach-disk-windows-linux](../../../../includes/howto-attach-disk-linux.md)]

## <a name="initialize-a-new-data-disk-in-linux"></a><span data-ttu-id="dccb0-120">un nuevo disco de datos en Linux</span><span class="sxs-lookup"><span data-stu-id="dccb0-120">Initialize a new data disk in Linux</span></span>
1. <span data-ttu-id="dccb0-121">SSH en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="dccb0-121">SSH to your VM.</span></span> <span data-ttu-id="dccb0-122">Para obtener más información, consulte [Inicio de sesión en una máquina virtual Linux][Logon].</span><span class="sxs-lookup"><span data-stu-id="dccb0-122">For more information, see [How to log on to a virtual machine running Linux][Logon].</span></span>
2. <span data-ttu-id="dccb0-123">A continuación deberá buscar el identificador de dispositivo para inicializar el disco de datos.</span><span class="sxs-lookup"><span data-stu-id="dccb0-123">Next you need to find the device identifier for the data disk to initialize.</span></span> <span data-ttu-id="dccb0-124">Existen dos formas de hacerlo:</span><span class="sxs-lookup"><span data-stu-id="dccb0-124">There are two ways to do that:</span></span>
   
    <span data-ttu-id="dccb0-125">(a) Busque con grep dispositivos SCSI en los registros, como se muestra en el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="dccb0-125">a) Grep for SCSI devices in the logs, such as in the following command:</span></span>
   
    ```bash
    sudo grep SCSI /var/log/messages
    ```
   
    <span data-ttu-id="dccb0-126">Para las distribuciones de Ubuntu recientes, puede que necesite usar `sudo grep SCSI /var/log/syslog` porque el inicio de sesión en `/var/log/messages` puede deshabilitarse de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="dccb0-126">For recent Ubuntu distributions, you may need to use `sudo grep SCSI /var/log/syslog` because logging to `/var/log/messages` might be disabled by default.</span></span>
   
    <span data-ttu-id="dccb0-127">Puede buscar el identificador del último disco de datos conectado en los mensajes que se muestran.</span><span class="sxs-lookup"><span data-stu-id="dccb0-127">You can find the identifier of the last data disk that was added in the messages that are displayed.</span></span>
   
    ![Obtener mensajes de disco](./media/attach-disk/scsidisklog.png)
   
    <span data-ttu-id="dccb0-129">OR</span><span class="sxs-lookup"><span data-stu-id="dccb0-129">OR</span></span>
   
    <span data-ttu-id="dccb0-130">b) Use el comando `lsscsi` para conocer el identificador de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="dccb0-130">b) Use the `lsscsi` command to find out the device id.</span></span> <span data-ttu-id="dccb0-131">`lsscsi` puede instalarse mediante `yum install lsscsi` (en distribuciones basadas en Red Hat) o mediante `apt-get install lsscsi` (en distribuciones basadas en Debian).</span><span class="sxs-lookup"><span data-stu-id="dccb0-131">`lsscsi` can be installed by either `yum install lsscsi` (on Red Hat based distributions) or `apt-get install lsscsi` (on Debian based distributions).</span></span> <span data-ttu-id="dccb0-132">Puede encontrar el disco que busca por su *lun* o **número de unidad lógica**.</span><span class="sxs-lookup"><span data-stu-id="dccb0-132">You can find the disk you are looking for by its *lun* or **logical unit number**.</span></span> <span data-ttu-id="dccb0-133">Por ejemplo, el *lun* de los discos que conectó puede verse fácilmente en `azure vm disk list <virtual-machine>`, de la manera siguiente:</span><span class="sxs-lookup"><span data-stu-id="dccb0-133">For example, the *lun* for the disks you attached can be easily seen from `azure vm disk list <virtual-machine>` as:</span></span>

    ```azurecli
    azure vm disk list myVM
    ```

    <span data-ttu-id="dccb0-134">La salida será similar a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="dccb0-134">The output is similar to the following:</span></span>

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
   
    <span data-ttu-id="dccb0-135">Compare estos datos con la salida de `lsscsi` para la misma máquina virtual de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="dccb0-135">Compare this data with the output of `lsscsi` for the same sample virtual machine:</span></span>
   
    ```bash
    [1:0:0:0]    cd/dvd  Msft     Virtual CD/ROM   1.0   /dev/sr0
    [2:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sda
    [3:0:1:0]    disk    Msft     Virtual Disk     1.0   /dev/sdb
    [5:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sdc
    ```
   
    <span data-ttu-id="dccb0-136">El último número de la tupla en cada fila es el *lun*.</span><span class="sxs-lookup"><span data-stu-id="dccb0-136">The last number in the tuple in each row is the *lun*.</span></span> <span data-ttu-id="dccb0-137">Vea `man lsscsi` para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="dccb0-137">See `man lsscsi` for more information.</span></span>
3. <span data-ttu-id="dccb0-138">En el símbolo del sistema, escriba el siguiente comando para crear el dispositivo:</span><span class="sxs-lookup"><span data-stu-id="dccb0-138">At the prompt, type the following command to create your device:</span></span>
   
    ```bash
    sudo fdisk /dev/sdc
    ```

4. <span data-ttu-id="dccb0-139">Cuando se le solicite, escriba  **n**  para crear una partición.</span><span class="sxs-lookup"><span data-stu-id="dccb0-139">When prompted, type **n** to create a partition.</span></span>

    ![Crear dispositivo](./media/attach-disk/fdisknewpartition.png)

5. <span data-ttu-id="dccb0-141">Cuando se le solicite, escriba **p** para que la partición sea la partición principal.</span><span class="sxs-lookup"><span data-stu-id="dccb0-141">When prompted, type **p** to make the partition the primary partition.</span></span> <span data-ttu-id="dccb0-142">Escriba **1** para que sea la primera partición y, a continuación, escriba "enter" para aceptar el valor predeterminado para el cilindro.</span><span class="sxs-lookup"><span data-stu-id="dccb0-142">Type **1** to make it the first partition, and then type enter to accept the default value for the cylinder.</span></span> <span data-ttu-id="dccb0-143">En algunos sistemas, puede mostrar los valores predeterminados del primer sector y el último sector, en lugar del cilindro.</span><span class="sxs-lookup"><span data-stu-id="dccb0-143">On some systems, it can show the default values of the first and the last sectors, instead of the cylinder.</span></span> <span data-ttu-id="dccb0-144">Puede aceptar estos valores predeterminados.</span><span class="sxs-lookup"><span data-stu-id="dccb0-144">You can choose to accept these defaults.</span></span>

    ![Crear partición](./media/attach-disk/fdisknewpartdetails.png)


6. <span data-ttu-id="dccb0-146">Escriba **p** para ver los detalles del disco en el que se va a crear la partición.</span><span class="sxs-lookup"><span data-stu-id="dccb0-146">Type **p** to see the details about the disk that is being partitioned.</span></span>

    ![Enumerar la información del disco](./media/attach-disk/fdiskpartitiondetails.png)


7. <span data-ttu-id="dccb0-148">Escriba **w** para escribir la configuración del disco.</span><span class="sxs-lookup"><span data-stu-id="dccb0-148">Type **w** to write the settings for the disk.</span></span>

    ![Escribir los cambios del disco](./media/attach-disk/fdiskwritedisk.png)

8. <span data-ttu-id="dccb0-150">Ahora puede crear el sistema de archivos en la nueva partición.</span><span class="sxs-lookup"><span data-stu-id="dccb0-150">Now you can create the file system on the new partition.</span></span> <span data-ttu-id="dccb0-151">Anexe el número de partición al id. de dispositivo (en el ejemplo siguiente, `/dev/sdc1`).</span><span class="sxs-lookup"><span data-stu-id="dccb0-151">Append the partition number to the device ID (in the following example `/dev/sdc1`).</span></span> <span data-ttu-id="dccb0-152">En el ejemplo siguiente se crea una partición de ext4 en /dev/sdc1:</span><span class="sxs-lookup"><span data-stu-id="dccb0-152">The following example creates an ext4 partition on /dev/sdc1:</span></span>
   
    ```bash
    sudo mkfs -t ext4 /dev/sdc1
    ```
   
    ![Crear sistema de archivos](./media/attach-disk/mkfsext4.png)
   
   > [!NOTE]
   > <span data-ttu-id="dccb0-154">Los sistemas SUSE Linux Enterprise 11 únicamente admiten acceso de solo lectura a sistemas de archivos ext4.</span><span class="sxs-lookup"><span data-stu-id="dccb0-154">SuSE Linux Enterprise 11 systems only support read-only access for ext4 file systems.</span></span> <span data-ttu-id="dccb0-155">Para estos sistemas, es recomendable dar formato al nuevo sistema de archivos como ext3 en vez de ext4.</span><span class="sxs-lookup"><span data-stu-id="dccb0-155">For these systems, it is recommended to format the new file system as ext3 rather than ext4.</span></span>

9. <span data-ttu-id="dccb0-156">Cree un directorio para montar el nuevo sistema de archivos como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="dccb0-156">Make a directory to mount the new file system, as follows:</span></span>
   
    ```bash
    sudo mkdir /datadrive
    ```

10. <span data-ttu-id="dccb0-157">Por último, se puede montar la unidad como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="dccb0-157">Finally you can mount the drive, as follows:</span></span>
   
    ```bash
    sudo mount /dev/sdc1 /datadrive
    ```
   
    <span data-ttu-id="dccb0-158">El disco de datos está ahora listo para usarse como **/datadrive**.</span><span class="sxs-lookup"><span data-stu-id="dccb0-158">The data disk is now ready to use as **/datadrive**.</span></span>
   
    ![Crear el directorio y montar el disco](./media/attach-disk/mkdirandmount.png)

11. <span data-ttu-id="dccb0-160">Agregue la nueva unidad a /etc/fstab:</span><span class="sxs-lookup"><span data-stu-id="dccb0-160">Add the new drive to /etc/fstab:</span></span>
   
    <span data-ttu-id="dccb0-161">Para asegurarse de que la unidad se vuelve a montar automáticamente después de reiniciar, debe agregarse al archivo /etc/fstab.</span><span class="sxs-lookup"><span data-stu-id="dccb0-161">To ensure the drive is remounted automatically after a reboot it must be added to the /etc/fstab file.</span></span> <span data-ttu-id="dccb0-162">Además, se recomienda encarecidamente que se use el UUID (identificador único global) en /etc/fstab para hacer referencia a la unidad en lugar de solo el nombre del dispositivo (es decir, /dev/sdc1).</span><span class="sxs-lookup"><span data-stu-id="dccb0-162">In addition, it is highly recommended that the UUID (Universally Unique IDentifier) is used in /etc/fstab to refer to the drive rather than just the device name (i.e. /dev/sdc1).</span></span> <span data-ttu-id="dccb0-163">El uso de UUID evita que el disco incorrecto se monte en una ubicación determinada si el sistema operativo detecta un error de disco durante el inicio y el resto de discos de datos se asignan a esos id. de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="dccb0-163">Using the UUID avoids the incorrect disk being mounted to a given location if the OS detects a disk error during boot and any remaining data disks then being assigned those device IDs.</span></span> <span data-ttu-id="dccb0-164">Para buscar el UUID de la unidad nueva, puede usar la utilidad **blkid**:</span><span class="sxs-lookup"><span data-stu-id="dccb0-164">To find the UUID of the new drive, you can use the **blkid** utility:</span></span>
   
    ```bash
    sudo -i blkid
    ```
   
    <span data-ttu-id="dccb0-165">La salida es similar a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="dccb0-165">The output looks similar to the following example:</span></span>
   
    ```bash
    /dev/sda1: UUID="11111111-1b1b-1c1c-1d1d-1e1e1e1e1e1e" TYPE="ext4"
    /dev/sdb1: UUID="22222222-2b2b-2c2c-2d2d-2e2e2e2e2e2e" TYPE="ext4"
    /dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
    ```

    > [!NOTE]
    > <span data-ttu-id="dccb0-166">La edición incorrecta del archivo **/etc/fstab** puede tener como resultado un sistema que no se pueda arrancar.</span><span class="sxs-lookup"><span data-stu-id="dccb0-166">Improperly editing the **/etc/fstab** file could result in an unbootable system.</span></span> <span data-ttu-id="dccb0-167">Si no está seguro, consulte la documentación de distribución para obtener información sobre cómo editar correctamente ese archivo.</span><span class="sxs-lookup"><span data-stu-id="dccb0-167">If unsure, refer to the distribution's documentation for information on how to properly edit this file.</span></span> <span data-ttu-id="dccb0-168">También se recomienda realizar una copia de seguridad del archivo /etc/fstab antes de editarlo.</span><span class="sxs-lookup"><span data-stu-id="dccb0-168">It is also recommended that a backup of the /etc/fstab file is created before editing.</span></span>

    <span data-ttu-id="dccb0-169">Después, abra el archivo **/etc/fstab** en un editor de texto:</span><span class="sxs-lookup"><span data-stu-id="dccb0-169">Next, open the **/etc/fstab** file in a text editor:</span></span>

    ```bash
    sudo vi /etc/fstab
    ```

    <span data-ttu-id="dccb0-170">En este ejemplo, usamos el valor de UUID para el nuevo dispositivo **/dev/sdc1** que se ha creado en los pasos anteriores y el punto de montaje **/datadrive**.</span><span class="sxs-lookup"><span data-stu-id="dccb0-170">In this example, we use the UUID value for the new **/dev/sdc1** device that was created in the previous steps, and the mountpoint **/datadrive**.</span></span> <span data-ttu-id="dccb0-171">Agregue la siguiente línea al final del archivo **/etc/fstab** :</span><span class="sxs-lookup"><span data-stu-id="dccb0-171">Add the following line to the end of the **/etc/fstab** file:</span></span>

    ```sh
    UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,nofail   1   2
    ```

    <span data-ttu-id="dccb0-172">O bien, en sistemas basados en SUSE Linux, es posible que tenga que utilizar un formato ligeramente diferente:</span><span class="sxs-lookup"><span data-stu-id="dccb0-172">Or, on systems based on SuSE Linux you may need to use a slightly different format:</span></span>

    ```sh
    /dev/disk/by-uuid/33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext3   defaults,nofail   1   2
    ```

    > [!NOTE]
    > <span data-ttu-id="dccb0-173">La opción `nofail` garantiza que la máquina virtual se inicia incluso si el sistema de archivos está dañado o el disco no existe al arrancar.</span><span class="sxs-lookup"><span data-stu-id="dccb0-173">The `nofail` option ensures that the VM starts even if the filesystem is corrupt or the disk does not exist at boot time.</span></span> <span data-ttu-id="dccb0-174">Sin esta opción, puede encontrarse con el comportamiento que se describe en [Cannot SSH to Linux VM due to FSTAB errors](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/) (No se puede conectar mediante SSH a una máquina virtual Linux debido a errores de FSTAB).</span><span class="sxs-lookup"><span data-stu-id="dccb0-174">Without this option, you may encounter behavior as described in [Cannot SSH to Linux VM due to FSTAB errors](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/).</span></span>

    <span data-ttu-id="dccb0-175">Ahora puede probar que el sistema de archivos está correctamente montado desmontando y volviendo a montar el sistema de archivos; es decir,</span><span class="sxs-lookup"><span data-stu-id="dccb0-175">You can now test that the file system is mounted properly by unmounting and then remounting the file system, i.e.</span></span> <span data-ttu-id="dccb0-176">usando el punto de montaje `/datadrive` creado en los pasos anteriores:</span><span class="sxs-lookup"><span data-stu-id="dccb0-176">using the example mount point `/datadrive` created in the earlier steps:</span></span>

    ```bash
    sudo umount /datadrive
    sudo mount /datadrive
    ```

    <span data-ttu-id="dccb0-177">Si el comando `mount` genera un error, compruebe la sintaxis correcta del archivo /etc/fstab.</span><span class="sxs-lookup"><span data-stu-id="dccb0-177">If the `mount` command produces an error, check the /etc/fstab file for correct syntax.</span></span> <span data-ttu-id="dccb0-178">Si se crean particiones o unidades de datos adicionales, especifíquelas también en /etc/fstab por separado.</span><span class="sxs-lookup"><span data-stu-id="dccb0-178">If additional data drives or partitions are created, enter them into /etc/fstab separately as well.</span></span>

    <span data-ttu-id="dccb0-179">Haga se pueda escribir en la unidad mediante este comando:</span><span class="sxs-lookup"><span data-stu-id="dccb0-179">Make the drive writable by using this command:</span></span>

    ```bash
    sudo chmod go+w /datadrive
    ```

    > [!NOTE]
    > <span data-ttu-id="dccb0-180">Posteriormente, la eliminación de un disco de datos sin editar fstab podría provocar un error en el inicio de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="dccb0-180">Subsequently removing a data disk without editing fstab could cause the VM to fail to boot.</span></span> <span data-ttu-id="dccb0-181">Si ocurre habitualmente, la mayoría de distribuciones proporcionan las opciones de fstab `nofail` o `nobootwait` que permite que el sistema se inicie incluso si el disco no se monta al arrancar.</span><span class="sxs-lookup"><span data-stu-id="dccb0-181">If this is a common occurrence, most distributions provide either the `nofail` and/or `nobootwait` fstab options that allow a system to boot even if the disk fails to mount at boot time.</span></span> <span data-ttu-id="dccb0-182">Consulte la documentación de su distribución para obtener más información sobre estos parámetros.</span><span class="sxs-lookup"><span data-stu-id="dccb0-182">Consult your distribution's documentation for more information on these parameters.</span></span>

### <a name="trimunmap-support-for-linux-in-azure"></a><span data-ttu-id="dccb0-183">Compatibilidad de TRIM/UNMAP con Linux en Azure</span><span class="sxs-lookup"><span data-stu-id="dccb0-183">TRIM/UNMAP support for Linux in Azure</span></span>
<span data-ttu-id="dccb0-184">Algunos kernels de Linux admiten operaciones TRIM/UNMAP para descartar bloques no usados del disco.</span><span class="sxs-lookup"><span data-stu-id="dccb0-184">Some Linux kernels support TRIM/UNMAP operations to discard unused blocks on the disk.</span></span> <span data-ttu-id="dccb0-185">Estas operaciones son especialmente útiles en el almacenamiento estándar para informar a Azure de que las páginas eliminadas ya no son válidas y se pueden descartar.</span><span class="sxs-lookup"><span data-stu-id="dccb0-185">These operations are primarily useful in standard storage to inform Azure that deleted pages are no longer valid and can be discarded.</span></span> <span data-ttu-id="dccb0-186">El descarte de páginas puede suponer un ahorro de dinero si crea archivos grandes y, a continuación, los elimina.</span><span class="sxs-lookup"><span data-stu-id="dccb0-186">Discarding pages can save cost if you create large files and then delete them.</span></span>

<span data-ttu-id="dccb0-187">Hay dos maneras de habilitar la compatibilidad con TRIM en su máquina virtual Linux.</span><span class="sxs-lookup"><span data-stu-id="dccb0-187">There are two ways to enable TRIM support in your Linux VM.</span></span> <span data-ttu-id="dccb0-188">Como es habitual, consulte la documentación de distribución para ver el enfoque recomendado:</span><span class="sxs-lookup"><span data-stu-id="dccb0-188">As usual, consult your distribution for the recommended approach:</span></span>

* <span data-ttu-id="dccb0-189">Use la opción de montaje `discard` en `/etc/fstab`, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="dccb0-189">Use the `discard` mount option in `/etc/fstab`, for example:</span></span>

    ```sh
    UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,discard   1   2
    ```

* <span data-ttu-id="dccb0-190">En algunos casos, la opción `discard` podría tener afectar al rendimiento.</span><span class="sxs-lookup"><span data-stu-id="dccb0-190">In some cases the `discard` option may have performance implications.</span></span> <span data-ttu-id="dccb0-191">Como alternativa, puede ejecutar el comando `fstrim` manualmente desde la línea de comandos o agregarlo a su crontab para ejecutar con regularidad:</span><span class="sxs-lookup"><span data-stu-id="dccb0-191">Alternatively, you can run the `fstrim` command manually from the command line, or add it to your crontab to run regularly:</span></span>
  
    <span data-ttu-id="dccb0-192">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="dccb0-192">**Ubuntu**</span></span>
  
    ```bash
    sudo apt-get install util-linux
    sudo fstrim /datadrive
    ```
  
    <span data-ttu-id="dccb0-193">**RHEL/CentOS**</span><span class="sxs-lookup"><span data-stu-id="dccb0-193">**RHEL/CentOS**</span></span>
  
    ```bash
    sudo yum install util-linux
    sudo fstrim /datadrive
    ```

## <a name="troubleshooting"></a><span data-ttu-id="dccb0-194">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="dccb0-194">Troubleshooting</span></span>
[!INCLUDE [virtual-machines-linux-lunzero](../../../../includes/virtual-machines-linux-lunzero.md)]

## <a name="next-steps"></a><span data-ttu-id="dccb0-195">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="dccb0-195">Next Steps</span></span>
<span data-ttu-id="dccb0-196">Puede leer más sobre el uso de la máquina virtual con Linux en los siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="dccb0-196">You can read more about using your Linux VM in the following articles:</span></span>

* <span data-ttu-id="dccb0-197">[Inicio de sesión en una máquina virtual con Linux][Logon]</span><span class="sxs-lookup"><span data-stu-id="dccb0-197">[How to log on to a virtual machine running Linux][Logon]</span></span>
* [<span data-ttu-id="dccb0-198">Desconexión de un disco de una máquina virtual de Linux</span><span class="sxs-lookup"><span data-stu-id="dccb0-198">How to detach a disk from a Linux virtual machine</span></span>](detach-disk.md)
* [<span data-ttu-id="dccb0-199">Comandos CLI de Azure en modo de Administración de servicios de Azure (asm)</span><span class="sxs-lookup"><span data-stu-id="dccb0-199">Using the Azure CLI with the Classic deployment model</span></span>](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)
* [<span data-ttu-id="dccb0-200">Configuración de RAID en una máquina virtual Linux en Azure</span><span class="sxs-lookup"><span data-stu-id="dccb0-200">Configure RAID on a Linux VM in Azure</span></span>](../configure-raid.md)
* [<span data-ttu-id="dccb0-201">Configuración del LVM en una máquina virtual Linux en Azure</span><span class="sxs-lookup"><span data-stu-id="dccb0-201">Configure LVM on a Linux VM in Azure</span></span>](../configure-lvm.md)

<!--Link references-->
[Agent]:../agent-user-guide.md
[Logon]:../mac-create-ssh-keys.md
