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
# <a name="how-tooattach-a-data-disk-tooa-linux-virtual-machine"></a><span data-ttu-id="7c043-103">¿Cómo tooAttach una máquina Virtual Linux tooa de disco de datos</span><span class="sxs-lookup"><span data-stu-id="7c043-103">How tooAttach a Data Disk tooa Linux Virtual Machine</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="7c043-104">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="7c043-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="7c043-105">Este artículo tratan con modelo de implementación de hello clásico.</span><span class="sxs-lookup"><span data-stu-id="7c043-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="7c043-106">Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="7c043-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="7c043-107">Vea cómo demasiado[conectar un disco de datos mediante el modelo de implementación del Administrador de recursos de hello](../add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7c043-107">See how too[attach a data disk using hello Resource Manager deployment model](../add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="7c043-108">Puede adjuntar discos vacíos y los discos que contienen datos tooyour máquinas virtuales de Azure.</span><span class="sxs-lookup"><span data-stu-id="7c043-108">You can attach both empty disks and disks that contain data tooyour Azure VMs.</span></span> <span data-ttu-id="7c043-109">Ambos tipos de discos son archivos .vhd que residen en una cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="7c043-109">Both types of disks are .vhd files that reside in an Azure storage account.</span></span> <span data-ttu-id="7c043-110">Como con la adición de cualquier equipo de Linux tooa de disco, después de conectar el disco de hello es necesario tooinitialize y darle formato para que esté preparada para su uso.</span><span class="sxs-lookup"><span data-stu-id="7c043-110">As with adding any disk tooa Linux machine, after you attach hello disk you need tooinitialize and format it so it's ready for use.</span></span> <span data-ttu-id="7c043-111">Este artículo se detallan adjuntar discos vacíos y los discos que ya contiene datos tooyour máquinas virtuales, así como la toothen inicializar y formatear un disco nuevo.</span><span class="sxs-lookup"><span data-stu-id="7c043-111">This article details attaching both empty disks and disks already containing data tooyour VMs, as well as how toothen initialize and format a new disk.</span></span>

> [!NOTE]
> <span data-ttu-id="7c043-112">Es una mejor toouse práctica uno o más separados toostore de discos de datos de una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="7c043-112">It's a best practice toouse one or more separate disks toostore a virtual machine's data.</span></span> <span data-ttu-id="7c043-113">Al crear una máquina virtual de Azure, esta cuenta con un disco para el sistema operativo y un disco temporal.</span><span class="sxs-lookup"><span data-stu-id="7c043-113">When you create an Azure virtual machine, it has an operating system disk and a temporary disk.</span></span> <span data-ttu-id="7c043-114">**No utilice datos persistentes de hello disco temporal toostore.**</span><span class="sxs-lookup"><span data-stu-id="7c043-114">**Do not use hello temporary disk toostore persistent data.**</span></span> <span data-ttu-id="7c043-115">Como indica el nombre de hello, proporciona solo el almacenamiento temporal.</span><span class="sxs-lookup"><span data-stu-id="7c043-115">As hello name implies, it provides temporary storage only.</span></span> <span data-ttu-id="7c043-116">No ofrece redundancia o copias de seguridad porque no reside en el almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="7c043-116">It offers no redundancy or backup because it doesn't reside in Azure storage.</span></span>
> <span data-ttu-id="7c043-117">disco temporal de Hola se suele estar a cargo Hola agente Linux de Azure y monta automáticamente demasiado**/mnt/resource** (o **/mnt** en Ubuntu imágenes).</span><span class="sxs-lookup"><span data-stu-id="7c043-117">hello temporary disk is typically managed by hello Azure Linux Agent and automatically mounted too**/mnt/resource** (or **/mnt** on Ubuntu images).</span></span> <span data-ttu-id="7c043-118">En Hola otro lado, un disco de datos podría denominarse kernel de Linux Hola algo parecido a `/dev/sdc`, y deberá toopartition, dar formato y montar este recurso.</span><span class="sxs-lookup"><span data-stu-id="7c043-118">On hello other hand, a data disk might be named by hello Linux kernel something like `/dev/sdc`, and you need toopartition, format, and mount this resource.</span></span> <span data-ttu-id="7c043-119">Vea hello [Guía de usuario de agente de Linux de Azure] [ Agent] para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="7c043-119">See hello [Azure Linux Agent User Guide][Agent] for details.</span></span>
> 
> 

[!INCLUDE [howto-attach-disk-windows-linux](../../../../includes/howto-attach-disk-linux.md)]

## <a name="initialize-a-new-data-disk-in-linux"></a><span data-ttu-id="7c043-120">un nuevo disco de datos en Linux</span><span class="sxs-lookup"><span data-stu-id="7c043-120">Initialize a new data disk in Linux</span></span>
1. <span data-ttu-id="7c043-121">SSH tooyour máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="7c043-121">SSH tooyour VM.</span></span> <span data-ttu-id="7c043-122">Para obtener más información, consulte [cómo toolog en la máquina virtual de tooa ejecutan Linux][Logon].</span><span class="sxs-lookup"><span data-stu-id="7c043-122">For more information, see [How toolog on tooa virtual machine running Linux][Logon].</span></span>
2. <span data-ttu-id="7c043-123">A continuación debe identificador de dispositivo de hello toofind para tooinitialize de disco de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="7c043-123">Next you need toofind hello device identifier for hello data disk tooinitialize.</span></span> <span data-ttu-id="7c043-124">Hay dos toodo de maneras que:</span><span class="sxs-lookup"><span data-stu-id="7c043-124">There are two ways toodo that:</span></span>
   
    <span data-ttu-id="7c043-125">a) registros de Grep para los dispositivos SCSI en hello, como se muestra en el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="7c043-125">a) Grep for SCSI devices in hello logs, such as in hello following command:</span></span>
   
    ```bash
    sudo grep SCSI /var/log/messages
    ```
   
    <span data-ttu-id="7c043-126">Para distribuciones de Ubuntu recientes, puede que necesite toouse `sudo grep SCSI /var/log/syslog` porque registro demasiado`/var/log/messages` pueden deshabilitarse de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="7c043-126">For recent Ubuntu distributions, you may need toouse `sudo grep SCSI /var/log/syslog` because logging too`/var/log/messages` might be disabled by default.</span></span>
   
    <span data-ttu-id="7c043-127">Puede encontrar el identificador de Hola Hola última del disco de datos que se agregó en los mensajes de saludo que se muestran.</span><span class="sxs-lookup"><span data-stu-id="7c043-127">You can find hello identifier of hello last data disk that was added in hello messages that are displayed.</span></span>
   
    ![Obtener mensajes de Hola disco](./media/attach-disk/scsidisklog.png)
   
    <span data-ttu-id="7c043-129">OR</span><span class="sxs-lookup"><span data-stu-id="7c043-129">OR</span></span>
   
    <span data-ttu-id="7c043-130">b) Hola usar `lsscsi` toofind comando out Id. de dispositivo de Hola. `lsscsi` pueden instalarse, ya sea `yum install lsscsi` (Red Hat según las distribuciones) o `apt-get install lsscsi` (Debian según las distribuciones).</span><span class="sxs-lookup"><span data-stu-id="7c043-130">b) Use hello `lsscsi` command toofind out hello device id. `lsscsi` can be installed by either `yum install lsscsi` (on Red Hat based distributions) or `apt-get install lsscsi` (on Debian based distributions).</span></span> <span data-ttu-id="7c043-131">Se puede encontrar un disco de Hola que está buscando por su *lun* o **número de unidad lógica**.</span><span class="sxs-lookup"><span data-stu-id="7c043-131">You can find hello disk you are looking for by its *lun* or **logical unit number**.</span></span> <span data-ttu-id="7c043-132">Por ejemplo, hello *lun* para discos de hello adjuntó pueden verse fácilmente desde `azure vm disk list <virtual-machine>` como:</span><span class="sxs-lookup"><span data-stu-id="7c043-132">For example, hello *lun* for hello disks you attached can be easily seen from `azure vm disk list <virtual-machine>` as:</span></span>

    ```azurecli
    azure vm disk list myVM
    ```

    <span data-ttu-id="7c043-133">salida de Hello es siguiente de toohello similar:</span><span class="sxs-lookup"><span data-stu-id="7c043-133">hello output is similar toohello following:</span></span>

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
   
    <span data-ttu-id="7c043-134">Comparar estos datos con salida de hello de `lsscsi` Hola mismo ejemplo máquina virtual:</span><span class="sxs-lookup"><span data-stu-id="7c043-134">Compare this data with hello output of `lsscsi` for hello same sample virtual machine:</span></span>
   
    ```bash
    [1:0:0:0]    cd/dvd  Msft     Virtual CD/ROM   1.0   /dev/sr0
    [2:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sda
    [3:0:1:0]    disk    Msft     Virtual Disk     1.0   /dev/sdb
    [5:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sdc
    ```
   
    <span data-ttu-id="7c043-135">último número de Hola de tupla de hello en cada fila es hello *lun*.</span><span class="sxs-lookup"><span data-stu-id="7c043-135">hello last number in hello tuple in each row is hello *lun*.</span></span> <span data-ttu-id="7c043-136">Vea `man lsscsi` para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="7c043-136">See `man lsscsi` for more information.</span></span>
3. <span data-ttu-id="7c043-137">En el símbolo del sistema de hello, escriba lo siguiente Hola comando toocreate el dispositivo:</span><span class="sxs-lookup"><span data-stu-id="7c043-137">At hello prompt, type hello following command toocreate your device:</span></span>
   
    ```bash
    sudo fdisk /dev/sdc
    ```

4. <span data-ttu-id="7c043-138">Cuando se le solicite, escriba  **n**  toocreate una partición.</span><span class="sxs-lookup"><span data-stu-id="7c043-138">When prompted, type **n** toocreate a partition.</span></span>

    ![Crear dispositivo](./media/attach-disk/fdisknewpartition.png)

5. <span data-ttu-id="7c043-140">Cuando se le solicite, escriba **p** toomake Hola Hola principal de particiones.</span><span class="sxs-lookup"><span data-stu-id="7c043-140">When prompted, type **p** toomake hello partition hello primary partition.</span></span> <span data-ttu-id="7c043-141">Tipo de **1** toomake Hola primera partición y, a continuación, escriba escriba el valor predeterminado de tooaccept Hola para cilindro de Hola.</span><span class="sxs-lookup"><span data-stu-id="7c043-141">Type **1** toomake it hello first partition, and then type enter tooaccept hello default value for hello cylinder.</span></span> <span data-ttu-id="7c043-142">En algunos sistemas, puede mostrar primero los valores predeterminados de Hola de Hola y Hola sectores último, en lugar de los cilindros Hola.</span><span class="sxs-lookup"><span data-stu-id="7c043-142">On some systems, it can show hello default values of hello first and hello last sectors, instead of hello cylinder.</span></span> <span data-ttu-id="7c043-143">Puede elegir tooaccept estos valores predeterminados.</span><span class="sxs-lookup"><span data-stu-id="7c043-143">You can choose tooaccept these defaults.</span></span>

    ![Crear partición](./media/attach-disk/fdisknewpartdetails.png)


6. <span data-ttu-id="7c043-145">Tipo de **p** detalles de hello toosee acerca del disco de Hola se particiona.</span><span class="sxs-lookup"><span data-stu-id="7c043-145">Type **p** toosee hello details about hello disk that is being partitioned.</span></span>

    ![Enumerar la información del disco](./media/attach-disk/fdiskpartitiondetails.png)


7. <span data-ttu-id="7c043-147">Tipo de **w** toowrite la configuración de Hola de discos de Hola.</span><span class="sxs-lookup"><span data-stu-id="7c043-147">Type **w** toowrite hello settings for hello disk.</span></span>

    ![Escribir los cambios de disco Hola](./media/attach-disk/fdiskwritedisk.png)

8. <span data-ttu-id="7c043-149">Ahora puede crear sistema de archivos de hello en la nueva partición de Hola.</span><span class="sxs-lookup"><span data-stu-id="7c043-149">Now you can create hello file system on hello new partition.</span></span> <span data-ttu-id="7c043-150">Anexar Hola número toohello dispositivo Id. de partición (en el siguiente ejemplo de Hola `/dev/sdc1`).</span><span class="sxs-lookup"><span data-stu-id="7c043-150">Append hello partition number toohello device ID (in hello following example `/dev/sdc1`).</span></span> <span data-ttu-id="7c043-151">Hello en el ejemplo siguiente se crea una partición de ext4 en /dev/sdc1:</span><span class="sxs-lookup"><span data-stu-id="7c043-151">hello following example creates an ext4 partition on /dev/sdc1:</span></span>
   
    ```bash
    sudo mkfs -t ext4 /dev/sdc1
    ```
   
    ![Crear sistema de archivos](./media/attach-disk/mkfsext4.png)
   
   > [!NOTE]
   > <span data-ttu-id="7c043-153">Los sistemas SUSE Linux Enterprise 11 únicamente admiten acceso de solo lectura a sistemas de archivos ext4.</span><span class="sxs-lookup"><span data-stu-id="7c043-153">SuSE Linux Enterprise 11 systems only support read-only access for ext4 file systems.</span></span> <span data-ttu-id="7c043-154">Para estos sistemas, se recomienda tooformat Hola nuevo sistema de archivos como ext3 en lugar de ext4.</span><span class="sxs-lookup"><span data-stu-id="7c043-154">For these systems, it is recommended tooformat hello new file system as ext3 rather than ext4.</span></span>

9. <span data-ttu-id="7c043-155">Realice un directorio toomount Hola nuevo sistema de archivos, como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="7c043-155">Make a directory toomount hello new file system, as follows:</span></span>
   
    ```bash
    sudo mkdir /datadrive
    ```

10. <span data-ttu-id="7c043-156">Por último, se puede montar unidad hello, como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="7c043-156">Finally you can mount hello drive, as follows:</span></span>
   
    ```bash
    sudo mount /dev/sdc1 /datadrive
    ```
   
    <span data-ttu-id="7c043-157">disco de datos de Hello ya está listo toouse como **/datadrive**.</span><span class="sxs-lookup"><span data-stu-id="7c043-157">hello data disk is now ready toouse as **/datadrive**.</span></span>
   
    ![Crear disco de Hola de directorio y montaje Hola](./media/attach-disk/mkdirandmount.png)

11. <span data-ttu-id="7c043-159">Agregue Hola nueva unidad demasiado/etcetera/fstab:</span><span class="sxs-lookup"><span data-stu-id="7c043-159">Add hello new drive too/etc/fstab:</span></span>
   
    <span data-ttu-id="7c043-160">unidad de hello tooensure se vuelven a montar automáticamente después de reiniciar el equipo debe ser agregado toohello/etc/fstab archivo.</span><span class="sxs-lookup"><span data-stu-id="7c043-160">tooensure hello drive is remounted automatically after a reboot it must be added toohello /etc/fstab file.</span></span> <span data-ttu-id="7c043-161">Además, se recomienda que Hola UUID (identificador único universalmente de) se utiliza en/etc/fstab toorefer toohello unidad en lugar de simplemente Hola nombre del dispositivo (es decir, /dev/sdc1).</span><span class="sxs-lookup"><span data-stu-id="7c043-161">In addition, it is highly recommended that hello UUID (Universally Unique IDentifier) is used in /etc/fstab toorefer toohello drive rather than just hello device name (i.e. /dev/sdc1).</span></span> <span data-ttu-id="7c043-162">Uso de hello UUID evita está montada tooa ubicación dada si Hola SO detecta un error de disco durante el arranque y los discos de datos restantes, a continuación, que se va a asignaron los identificadores de dispositivo de disco incorrecta Hola.</span><span class="sxs-lookup"><span data-stu-id="7c043-162">Using hello UUID avoids hello incorrect disk being mounted tooa given location if hello OS detects a disk error during boot and any remaining data disks then being assigned those device IDs.</span></span> <span data-ttu-id="7c043-163">toofind Hola UUID de la nueva unidad de hello, puede usar hello **blkid** utilidad:</span><span class="sxs-lookup"><span data-stu-id="7c043-163">toofind hello UUID of hello new drive, you can use hello **blkid** utility:</span></span>
   
    ```bash
    sudo -i blkid
    ```
   
    <span data-ttu-id="7c043-164">salida de Hello tiene un aspecto similar toohello siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="7c043-164">hello output looks similar toohello following example:</span></span>
   
    ```bash
    /dev/sda1: UUID="11111111-1b1b-1c1c-1d1d-1e1e1e1e1e1e" TYPE="ext4"
    /dev/sdb1: UUID="22222222-2b2b-2c2c-2d2d-2e2e2e2e2e2e" TYPE="ext4"
    /dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
    ```

    > [!NOTE]
    > <span data-ttu-id="7c043-165">Edición incorrectamente hello **/etcetera/fstab** archivo podría provocar un reinicio del sistema.</span><span class="sxs-lookup"><span data-stu-id="7c043-165">Improperly editing hello **/etc/fstab** file could result in an unbootable system.</span></span> <span data-ttu-id="7c043-166">Si no está seguro, consulte la documentación de la distribución de toohello para obtener información sobre cómo tooproperly editar este archivo.</span><span class="sxs-lookup"><span data-stu-id="7c043-166">If unsure, refer toohello distribution's documentation for information on how tooproperly edit this file.</span></span> <span data-ttu-id="7c043-167">También se recomienda que se crea una copia de seguridad del archivo/etc/fstab de hello antes de modificarla.</span><span class="sxs-lookup"><span data-stu-id="7c043-167">It is also recommended that a backup of hello /etc/fstab file is created before editing.</span></span>

    <span data-ttu-id="7c043-168">A continuación, abra hello **/etcetera/fstab** archivo en un editor de texto:</span><span class="sxs-lookup"><span data-stu-id="7c043-168">Next, open hello **/etc/fstab** file in a text editor:</span></span>

    ```bash
    sudo vi /etc/fstab
    ```

    <span data-ttu-id="7c043-169">En este ejemplo, utilizamos Hola UUID valor para hello nueva **/dev/sdc1** dispositivo que se creó en los pasos anteriores de Hola y el punto de montaje de hello **/datadrive**.</span><span class="sxs-lookup"><span data-stu-id="7c043-169">In this example, we use hello UUID value for hello new **/dev/sdc1** device that was created in hello previous steps, and hello mountpoint **/datadrive**.</span></span> <span data-ttu-id="7c043-170">Agregar Hola siguiente línea toohello final de hello **/etcetera/fstab** archivo:</span><span class="sxs-lookup"><span data-stu-id="7c043-170">Add hello following line toohello end of hello **/etc/fstab** file:</span></span>

    ```sh
    UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,nofail   1   2
    ```

    <span data-ttu-id="7c043-171">O bien, en sistemas basados en SuSE Linux que necesite toouse un formato ligeramente diferente:</span><span class="sxs-lookup"><span data-stu-id="7c043-171">Or, on systems based on SuSE Linux you may need toouse a slightly different format:</span></span>

    ```sh
    /dev/disk/by-uuid/33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext3   defaults,nofail   1   2
    ```

    > [!NOTE]
    > <span data-ttu-id="7c043-172">Hola `nofail` opción garantiza que Hola VM inicie aunque Hola filesystem está dañado o disco hello no existe en tiempo de arranque.</span><span class="sxs-lookup"><span data-stu-id="7c043-172">hello `nofail` option ensures that hello VM starts even if hello filesystem is corrupt or hello disk does not exist at boot time.</span></span> <span data-ttu-id="7c043-173">Sin esta opción, se puede encontrar un comportamiento tal y como se describe en [no SSH tooLinux VM debido a errores de tooFSTAB](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/).</span><span class="sxs-lookup"><span data-stu-id="7c043-173">Without this option, you may encounter behavior as described in [Cannot SSH tooLinux VM due tooFSTAB errors](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/).</span></span>

    <span data-ttu-id="7c043-174">Ahora puede probar que el sistema de archivos de hello está montado correctamente al desmontar y, a continuación, vuelva a montar el sistema de archivos de hello, es decir, con el punto de montaje del ejemplo de Hola `/datadrive` creado en hello los pasos anteriores:</span><span class="sxs-lookup"><span data-stu-id="7c043-174">You can now test that hello file system is mounted properly by unmounting and then remounting hello file system, i.e. using hello example mount point `/datadrive` created in hello earlier steps:</span></span>

    ```bash
    sudo umount /datadrive
    sudo mount /datadrive
    ```

    <span data-ttu-id="7c043-175">Si hello `mount` comando produce un error, compruebe Hola/etcetera/fstab archivo para ver la sintaxis correcta.</span><span class="sxs-lookup"><span data-stu-id="7c043-175">If hello `mount` command produces an error, check hello /etc/fstab file for correct syntax.</span></span> <span data-ttu-id="7c043-176">Si se crean particiones o unidades de datos adicionales, especifíquelas también en /etc/fstab por separado.</span><span class="sxs-lookup"><span data-stu-id="7c043-176">If additional data drives or partitions are created, enter them into /etc/fstab separately as well.</span></span>

    <span data-ttu-id="7c043-177">Asegúrese de unidad de hello grabable mediante este comando:</span><span class="sxs-lookup"><span data-stu-id="7c043-177">Make hello drive writable by using this command:</span></span>

    ```bash
    sudo chmod go+w /datadrive
    ```

    > [!NOTE]
    > <span data-ttu-id="7c043-178">Quitar posteriormente un disco de datos sin necesidad de editar fstab podría producir Hola VM toofail tooboot.</span><span class="sxs-lookup"><span data-stu-id="7c043-178">Subsequently removing a data disk without editing fstab could cause hello VM toofail tooboot.</span></span> <span data-ttu-id="7c043-179">Si se trata de un hecho frecuente, mayoría de las distribuciones proporciona cualquier hello `nofail` o `nobootwait` fstab opciones que permiten una tooboot sistema aunque hello tiene un error toomount al arrancar el sistema.</span><span class="sxs-lookup"><span data-stu-id="7c043-179">If this is a common occurrence, most distributions provide either hello `nofail` and/or `nobootwait` fstab options that allow a system tooboot even if hello disk fails toomount at boot time.</span></span> <span data-ttu-id="7c043-180">Consulte la documentación de su distribución para obtener más información sobre estos parámetros.</span><span class="sxs-lookup"><span data-stu-id="7c043-180">Consult your distribution's documentation for more information on these parameters.</span></span>

### <a name="trimunmap-support-for-linux-in-azure"></a><span data-ttu-id="7c043-181">Compatibilidad de TRIM/UNMAP con Linux en Azure</span><span class="sxs-lookup"><span data-stu-id="7c043-181">TRIM/UNMAP support for Linux in Azure</span></span>
<span data-ttu-id="7c043-182">Algunos los kernels de Linux admiten TRIM y UNMAP operaciones toodiscard los bloques sin utilizar en el disco de Hola.</span><span class="sxs-lookup"><span data-stu-id="7c043-182">Some Linux kernels support TRIM/UNMAP operations toodiscard unused blocks on hello disk.</span></span> <span data-ttu-id="7c043-183">Estas operaciones son sobre todo útiles en almacenamiento estándar tooinform Azure que elimina páginas ya no son válidos y se pueden descartar.</span><span class="sxs-lookup"><span data-stu-id="7c043-183">These operations are primarily useful in standard storage tooinform Azure that deleted pages are no longer valid and can be discarded.</span></span> <span data-ttu-id="7c043-184">El descarte de páginas puede suponer un ahorro de dinero si crea archivos grandes y, a continuación, los elimina.</span><span class="sxs-lookup"><span data-stu-id="7c043-184">Discarding pages can save cost if you create large files and then delete them.</span></span>

<span data-ttu-id="7c043-185">Hay dos maneras tooenable TRIM se admiten en la VM de Linux.</span><span class="sxs-lookup"><span data-stu-id="7c043-185">There are two ways tooenable TRIM support in your Linux VM.</span></span> <span data-ttu-id="7c043-186">Como es habitual, consulte la distribución de hello enfoque recomendado:</span><span class="sxs-lookup"><span data-stu-id="7c043-186">As usual, consult your distribution for hello recommended approach:</span></span>

* <span data-ttu-id="7c043-187">Hola de uso `discard` montar opción en `/etc/fstab`, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="7c043-187">Use hello `discard` mount option in `/etc/fstab`, for example:</span></span>

    ```sh
    UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,discard   1   2
    ```

* <span data-ttu-id="7c043-188">En algunos Hola casos `discard` opción podría tener implicaciones de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="7c043-188">In some cases hello `discard` option may have performance implications.</span></span> <span data-ttu-id="7c043-189">Como alternativa, puede ejecutar hello `fstrim` comando manualmente desde la línea de comandos de hello, o agréguela tooyour crontab toorun con regularidad:</span><span class="sxs-lookup"><span data-stu-id="7c043-189">Alternatively, you can run hello `fstrim` command manually from hello command line, or add it tooyour crontab toorun regularly:</span></span>
  
    <span data-ttu-id="7c043-190">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="7c043-190">**Ubuntu**</span></span>
  
    ```bash
    sudo apt-get install util-linux
    sudo fstrim /datadrive
    ```
  
    <span data-ttu-id="7c043-191">**RHEL/CentOS**</span><span class="sxs-lookup"><span data-stu-id="7c043-191">**RHEL/CentOS**</span></span>
  
    ```bash
    sudo yum install util-linux
    sudo fstrim /datadrive
    ```

## <a name="troubleshooting"></a><span data-ttu-id="7c043-192">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="7c043-192">Troubleshooting</span></span>
[!INCLUDE [virtual-machines-linux-lunzero](../../../../includes/virtual-machines-linux-lunzero.md)]

## <a name="next-steps"></a><span data-ttu-id="7c043-193">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7c043-193">Next Steps</span></span>
<span data-ttu-id="7c043-194">Puede leer más sobre el uso de la VM de Linux en hello siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="7c043-194">You can read more about using your Linux VM in hello following articles:</span></span>

* <span data-ttu-id="7c043-195">[¿Cómo toolog en la máquina virtual de tooa ejecutan Linux][Logon]</span><span class="sxs-lookup"><span data-stu-id="7c043-195">[How toolog on tooa virtual machine running Linux][Logon]</span></span>
* [<span data-ttu-id="7c043-196">¿Cómo toodetach un disco de una máquina virtual Linux</span><span class="sxs-lookup"><span data-stu-id="7c043-196">How toodetach a disk from a Linux virtual machine</span></span>](detach-disk.md)
* [<span data-ttu-id="7c043-197">Usar Hola CLI de Azure con modelo de implementación de hello clásico</span><span class="sxs-lookup"><span data-stu-id="7c043-197">Using hello Azure CLI with hello Classic deployment model</span></span>](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)
* [<span data-ttu-id="7c043-198">Configuración de RAID en una máquina virtual Linux en Azure</span><span class="sxs-lookup"><span data-stu-id="7c043-198">Configure RAID on a Linux VM in Azure</span></span>](../configure-raid.md)
* [<span data-ttu-id="7c043-199">Configuración del LVM en una máquina virtual Linux en Azure</span><span class="sxs-lookup"><span data-stu-id="7c043-199">Configure LVM on a Linux VM in Azure</span></span>](../configure-lvm.md)

<!--Link references-->
[Agent]:../agent-user-guide.md
[Logon]:../mac-create-ssh-keys.md
