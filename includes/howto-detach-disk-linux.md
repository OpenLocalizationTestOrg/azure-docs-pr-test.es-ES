<span data-ttu-id="8c2e2-101">Cuando ya no necesita un disco de datos es tooa adjunto un equipo virtual (VM), puede separar fácilmente.</span><span class="sxs-lookup"><span data-stu-id="8c2e2-101">When you no longer need a data disk that's attached tooa virtual machine (VM), you can easily detach it.</span></span> <span data-ttu-id="8c2e2-102">Cuando se separa un disco de hello VM, disco de hello no es eliminen del almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="8c2e2-102">When you detach a disk from hello VM, hello disk is not removed it from storage.</span></span> <span data-ttu-id="8c2e2-103">Si desea volver a datos existentes de toouse hello en el disco de hello, puede adjuntarla toohello misma máquina virtual, u otro.</span><span class="sxs-lookup"><span data-stu-id="8c2e2-103">If you want toouse hello existing data on hello disk again, you can reattach it toohello same VM, or another one.</span></span>  

> [!NOTE]
> <span data-ttu-id="8c2e2-104">Una máquina virtual en Azure utiliza distintos tipos de discos, como un disco del sistema operativo, un disco temporal local y discos de datos opcionales.</span><span class="sxs-lookup"><span data-stu-id="8c2e2-104">A VM in Azure uses different types of disks - an operating system disk, a local temporary disk, and optional data disks.</span></span> <span data-ttu-id="8c2e2-105">Para más información, consulte [Acerca de los discos y los discos duros virtuales para Virtual Machines](../articles/virtual-machines/linux/about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8c2e2-105">For details, see [About Disks and VHDs for Virtual Machines](../articles/virtual-machines/linux/about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="8c2e2-106">No se puede separar un disco del sistema operativo, a menos que también se eliminarán Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="8c2e2-106">You cannot detach an operating system disk unless you also delete hello VM.</span></span>

## <a name="find-hello-disk"></a><span data-ttu-id="8c2e2-107">Encuentra el disco de Hola</span><span class="sxs-lookup"><span data-stu-id="8c2e2-107">Find hello disk</span></span>
<span data-ttu-id="8c2e2-108">Para poder separar un disco de una máquina virtual debe toofind out Hola número LUN, que es un identificador de hello disco toobe desconectado.</span><span class="sxs-lookup"><span data-stu-id="8c2e2-108">Before you can detach a disk from a VM you need toofind out hello LUN number, which is an identifier for hello disk toobe detached.</span></span> <span data-ttu-id="8c2e2-109">toodo que, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="8c2e2-109">toodo that, follow these steps:</span></span>

1. <span data-ttu-id="8c2e2-110">Abra la CLI de Azure y [conectar tooyour suscripción de Azure](../articles/xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="8c2e2-110">Open Azure CLI and [connect tooyour Azure subscription](../articles/xplat-cli-connect.md).</span></span> <span data-ttu-id="8c2e2-111">Procure estar en el modo de administración de servicios de Azure (`azure config mode asm`).</span><span class="sxs-lookup"><span data-stu-id="8c2e2-111">Make sure you are in Azure Service Management mode (`azure config mode asm`).</span></span>
2. <span data-ttu-id="8c2e2-112">Averigüe qué discos están conectado tooyour máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="8c2e2-112">Find out which disks are attached tooyour VM.</span></span> <span data-ttu-id="8c2e2-113">Hello en el ejemplo siguiente se enumera los discos de máquina virtual denominada Hola `myVM`:</span><span class="sxs-lookup"><span data-stu-id="8c2e2-113">hello following example lists disks for hello VM named `myVM`:</span></span>

    ```azurecli
    azure vm disk list myVM
    ```

    <span data-ttu-id="8c2e2-114">Hola de salida es similar toohello siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="8c2e2-114">hello output is similar toohello following example:</span></span>

    ```azurecli
    * Fetching disk images
    * Getting virtual machines
    * Getting VM disks
      data:    Lun  Size(GB)  Blob-Name                         OS
      data:    ---  --------  --------------------------------  -----
      data:         30        ubuntuVM-2645b8030676c8f8.vhd  Linux
      data:    0    30        myDataDisk.vhd
      info:    vm disk list command OK
    ```

3. <span data-ttu-id="8c2e2-115">Tenga en cuenta Hola LUN o hello **número de unidad lógica** para el disco de Hola que desea toodetach.</span><span class="sxs-lookup"><span data-stu-id="8c2e2-115">Note hello LUN or hello **logical unit number** for hello disk that you want toodetach.</span></span>

## <a name="remove-operating-system-references-toohello-disk"></a><span data-ttu-id="8c2e2-116">Quitar el disco del sistema operativo referencias toohello</span><span class="sxs-lookup"><span data-stu-id="8c2e2-116">Remove operating system references toohello disk</span></span>
<span data-ttu-id="8c2e2-117">Antes de separar disco Hola de invitado de Linux de hello, debe asegurarse de que todas las particiones de disco de hello no están en uso.</span><span class="sxs-lookup"><span data-stu-id="8c2e2-117">Before detaching hello disk from hello Linux guest, you should make sure that all partitions on hello disk are not in use.</span></span> <span data-ttu-id="8c2e2-118">Asegúrese de ese sistema operativo de hello no intenta tooremount tras un reinicio.</span><span class="sxs-lookup"><span data-stu-id="8c2e2-118">Ensure that hello operating system does not attempt tooremount them after a reboot.</span></span> <span data-ttu-id="8c2e2-119">Estos pasos deshacer configuración Hola probablemente creó cuando [adjuntar](../articles/virtual-machines/linux/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) disco Hola.</span><span class="sxs-lookup"><span data-stu-id="8c2e2-119">These steps undo hello configuration you likely created when [attaching](../articles/virtual-machines/linux/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) hello disk.</span></span>

1. <span data-ttu-id="8c2e2-120">Hola de uso `lsscsi` identificador de disco de comando toodiscover Hola.</span><span class="sxs-lookup"><span data-stu-id="8c2e2-120">Use hello `lsscsi` command toodiscover hello disk identifier.</span></span> <span data-ttu-id="8c2e2-121">`lsscsi` puede instalarse mediante `yum install lsscsi` (en distribuciones basadas en Red Hat) o mediante `apt-get install lsscsi` (en distribuciones basadas en Debian).</span><span class="sxs-lookup"><span data-stu-id="8c2e2-121">`lsscsi` can be installed by either `yum install lsscsi` (on Red Hat based distributions) or `apt-get install lsscsi` (on Debian based distributions).</span></span> <span data-ttu-id="8c2e2-122">Puede encontrar el identificador de disco de Hola que está buscando utilizando el número LUN de Hola.</span><span class="sxs-lookup"><span data-stu-id="8c2e2-122">You can find hello disk identifier you are looking for by using hello LUN number.</span></span> <span data-ttu-id="8c2e2-123">último número de Hola de tupla de hello en cada fila es hello LUN.</span><span class="sxs-lookup"><span data-stu-id="8c2e2-123">hello last number in hello tuple in each row is hello LUN.</span></span> <span data-ttu-id="8c2e2-124">Hola siguiente ejemplo de `lsscsi`, LUN 0 se asigna demasiado  */dev/sdc*</span><span class="sxs-lookup"><span data-stu-id="8c2e2-124">In hello following example from `lsscsi`, LUN 0 maps too*/dev/sdc*</span></span>

    ```bash
    [1:0:0:0]    cd/dvd  Msft     Virtual CD/ROM   1.0   /dev/sr0
    [2:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sda
    [3:0:1:0]    disk    Msft     Virtual Disk     1.0   /dev/sdb
    [5:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sdc
    ```

2. <span data-ttu-id="8c2e2-125">Use `fdisk -l <disk>` particiones de hello toodiscover asociadas Hola disco toobe desconectado.</span><span class="sxs-lookup"><span data-stu-id="8c2e2-125">Use `fdisk -l <disk>` toodiscover hello partitions associated with hello disk toobe detached.</span></span> <span data-ttu-id="8c2e2-126">Hello en el ejemplo siguiente se muestra la salida de hello para `/dev/sdc`:</span><span class="sxs-lookup"><span data-stu-id="8c2e2-126">hello following example shows hello output for `/dev/sdc`:</span></span>

    ```bash
    Disk /dev/sdc: 1098.4 GB, 1098437885952 bytes, 2145386496 sectors
    Units = sectors of 1 * 512 = 512 bytes
    Sector size (logical/physical): 512 bytes / 512 bytes
    I/O size (minimum/optimal): 512 bytes / 512 bytes
    Disk label type: dos
    Disk identifier: 0x5a1d2a1a
    
        Device Boot      Start         End      Blocks   Id  System
    /dev/sdc1            2048  2145386495  1072692224   83  Linux
    ```

3. <span data-ttu-id="8c2e2-127">Desmonte cada partición de disco de Hola.</span><span class="sxs-lookup"><span data-stu-id="8c2e2-127">Unmount each partition listed for hello disk.</span></span> <span data-ttu-id="8c2e2-128">desmonta de Hello en el ejemplo siguiente se `/dev/sdc1`:</span><span class="sxs-lookup"><span data-stu-id="8c2e2-128">hello following example unmounts `/dev/sdc1`:</span></span>

    ```bash
    sudo umount /dev/sdc1
    ```

4. <span data-ttu-id="8c2e2-129">Hola de uso `blkid` comando toodiscovery hello UUID de todas las particiones.</span><span class="sxs-lookup"><span data-stu-id="8c2e2-129">Use hello `blkid` command toodiscovery hello UUIDs for all partitions.</span></span> <span data-ttu-id="8c2e2-130">Hola de salida es similar toohello siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="8c2e2-130">hello output is similar toohello following example:</span></span>

    ```bash
    /dev/sda1: UUID="11111111-1b1b-1c1c-1d1d-1e1e1e1e1e1e" TYPE="ext4"
    /dev/sdb1: UUID="22222222-2b2b-2c2c-2d2d-2e2e2e2e2e2e" TYPE="ext4"
    /dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
    ```

5. <span data-ttu-id="8c2e2-131">Eliminar las entradas en hello **/etcetera/fstab** archivo asociado a las rutas de acceso de dispositivo de Hola o UUID para todas las particiones de hello disco toobe desconectado.</span><span class="sxs-lookup"><span data-stu-id="8c2e2-131">Remove entries in hello **/etc/fstab** file associated with either hello device paths or UUIDs for all partitions for hello disk toobe detached.</span></span>  <span data-ttu-id="8c2e2-132">Las entradas de este ejemplo podrían ser:</span><span class="sxs-lookup"><span data-stu-id="8c2e2-132">Entries for this example might be:</span></span>

    ```sh  
   UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults   1   2
   ```

    <span data-ttu-id="8c2e2-133">o</span><span class="sxs-lookup"><span data-stu-id="8c2e2-133">or</span></span>
   
   ```sh   
   /dev/sdc1   /datadrive   ext4   defaults   1   2
   ```

## <a name="detach-hello-disk"></a><span data-ttu-id="8c2e2-134">Desconectar el disco de Hola</span><span class="sxs-lookup"><span data-stu-id="8c2e2-134">Detach hello disk</span></span>
<span data-ttu-id="8c2e2-135">Después de encontrar el número LUN de Hola de disco de Hola y referencias de sistema operativo de hello quitado, está listo toodetach:</span><span class="sxs-lookup"><span data-stu-id="8c2e2-135">After you find hello LUN number of hello disk and removed hello operating system references, you're ready toodetach it:</span></span>

1. <span data-ttu-id="8c2e2-136">Desconectar el disco seleccionado de hello de la máquina virtual de hello mediante la ejecución de comando hello `azure vm disk detach
   <virtual-machine-name> <LUN>`.</span><span class="sxs-lookup"><span data-stu-id="8c2e2-136">Detach hello selected disk from hello virtual machine by running hello command `azure vm disk detach
<virtual-machine-name> <LUN>`.</span></span> <span data-ttu-id="8c2e2-137">Hello en el ejemplo siguiente se separa LUN `0` de hello máquina virtual denominada `myVM`:</span><span class="sxs-lookup"><span data-stu-id="8c2e2-137">hello following example detaches LUN `0` from hello VM named `myVM`:</span></span>
   
    ```azurecli
    azure vm disk detach myVM 0
    ```

2. <span data-ttu-id="8c2e2-138">Puede comprobar si el disco de hello obtuvo separado mediante la ejecución de `azure vm disk list` nuevo.</span><span class="sxs-lookup"><span data-stu-id="8c2e2-138">You can check if hello disk got detached by running `azure vm disk list` again.</span></span> <span data-ttu-id="8c2e2-139">Después de las comprobaciones de ejemplo de Hola Hola máquina virtual denominada `myVM`:</span><span class="sxs-lookup"><span data-stu-id="8c2e2-139">hello following example checks hello VM named `myVM`:</span></span>
   
    ```azurecli
    azure vm disk list myVM
    ```

    <span data-ttu-id="8c2e2-140">Hola de salida es similar toohello siguiente ejemplo, que se muestra en disco de datos de hello ya no está conectado:</span><span class="sxs-lookup"><span data-stu-id="8c2e2-140">hello output is similar toohello following example, which shows hello data disk is no longer attached:</span></span>

    ```azurecli
    info:    Executing command vm disk list
   
   * Fetching disk images
   * Getting virtual machines
   * Getting VM disks
     data:    Lun  Size(GB)  Blob-Name                         OS
     data:    ---  --------  --------------------------------  -----
     data:         30        ubuntuVM-2645b8030676c8f8.vhd  Linux
     info:    vm disk list command OK
    ```

<span data-ttu-id="8c2e2-141">disco Hola separada permanece en el almacenamiento pero ya no es máquina virtual de tooa adjunto.</span><span class="sxs-lookup"><span data-stu-id="8c2e2-141">hello detached disk remains in storage but is no longer attached tooa virtual machine.</span></span>

