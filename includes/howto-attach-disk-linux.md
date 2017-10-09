
<span data-ttu-id="c9555-101">Para más información acerca de los discos, consulte [Acerca de los discos y los discos duros virtuales para Virtual Machines](../articles/virtual-machines/linux/about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c9555-101">For more information about disks, see [About Disks and VHDs for Virtual Machines](../articles/virtual-machines/linux/about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<a id="attachempty"></a>

## <a name="attach-an-empty-disk"></a><span data-ttu-id="c9555-102">Conectar un disco vacío</span><span class="sxs-lookup"><span data-stu-id="c9555-102">Attach an empty disk</span></span>
1. <span data-ttu-id="c9555-103">Abra 1.0 de CLI de Azure y [conectar tooyour suscripción de Azure](../articles/xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="c9555-103">Open Azure CLI 1.0 and [connect tooyour Azure subscription](../articles/xplat-cli-connect.md).</span></span> <span data-ttu-id="c9555-104">Procure estar en el modo de administración de servicios de Azure (`azure config mode asm`).</span><span class="sxs-lookup"><span data-stu-id="c9555-104">Make sure you are in Azure Service Management mode (`azure config mode asm`).</span></span>
2. <span data-ttu-id="c9555-105">Escriba `azure vm disk attach-new` toocreate y adjuntar un disco nuevo, como se muestra en el siguiente ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="c9555-105">Enter `azure vm disk attach-new` toocreate and attach a new disk as shown in hello following example.</span></span> <span data-ttu-id="c9555-106">Reemplace *myVM* con el nombre de la máquina Virtual de Linux de Hola y especifique el tamaño de Hola de disco de hello en GB, que es *100GB* en este ejemplo:</span><span class="sxs-lookup"><span data-stu-id="c9555-106">Replace *myVM* with hello name of your Linux Virtual Machine and specify hello size of hello disk in GB, which is *100GB* in this example:</span></span>

    ```azurecli
    azure vm disk attach-new myVM 100
    ```

3. <span data-ttu-id="c9555-107">Después de que se crea y asocia disco de datos de hello, aparece en la salida de hello de `azure vm disk list <virtual-machine-name>` tal y como se muestra en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="c9555-107">After hello data disk is created and attached, it's listed in hello output of `azure vm disk list <virtual-machine-name>` as shown in hello following example:</span></span>
   
    ```azurecli
    azure vm disk list TestVM
    ```

    <span data-ttu-id="c9555-108">Hola de salida es similar toohello siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="c9555-108">hello output is similar toohello following example:</span></span>

    ```bash
    info:    Executing command vm disk list
   
   * Fetching disk images
   * Getting virtual machines
   * Getting VM disks
     data:    Lun  Size(GB)  Blob-Name                         OS
     data:    ---  --------  --------------------------------  -----
     data:         30        myVM-2645b8030676c8f8.vhd  Linux
     data:    0    100       myVM-76f7ee1ef0f6dddc.vhd
     info:    vm disk list command OK
    ```

<a id="attachexisting"></a>

## <a name="attach-an-existing-disk"></a><span data-ttu-id="c9555-109">un disco existente</span><span class="sxs-lookup"><span data-stu-id="c9555-109">Attach an existing disk</span></span>
<span data-ttu-id="c9555-110">El acoplamiento de un disco existente requiere que disponga de un .vhd disponible en la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="c9555-110">Attaching an existing disk requires that you have a .vhd available in a storage account.</span></span>

1. <span data-ttu-id="c9555-111">Abra 1.0 de CLI de Azure y [conectar tooyour suscripción de Azure](../articles/xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="c9555-111">Open Azure CLI 1.0 and [connect tooyour Azure subscription](../articles/xplat-cli-connect.md).</span></span> <span data-ttu-id="c9555-112">Procure estar en el modo de administración de servicios de Azure (`azure config mode asm`).</span><span class="sxs-lookup"><span data-stu-id="c9555-112">Make sure you are in Azure Service Management mode (`azure config mode asm`).</span></span>
2. <span data-ttu-id="c9555-113">Compruebe si Hola VHD desea tooattach ya está cargado tooyour suscripción de Azure:</span><span class="sxs-lookup"><span data-stu-id="c9555-113">Check if hello VHD you want tooattach is already uploaded tooyour Azure subscription:</span></span>
   
    ```azurecli
    azure vm disk list
    ```

    <span data-ttu-id="c9555-114">Hola de salida es similar toohello siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="c9555-114">hello output is similar toohello following example:</span></span>

    ```azurecli
     info:    Executing command vm disk list
   
   * Fetching disk images
     data:    Name                                          OS
     data:    --------------------------------------------  -----
     data:    myTestVhd                                     Linux
     data:    TestVM-ubuntuVMasm-0-201508060029150744  Linux
     data:    TestVM-ubuntuVMasm-0-201508060040530369
     info:    vm disk list command OK
    ```

3. <span data-ttu-id="c9555-115">Si no encuentra el disco de Hola que desee toouse, puede cargar una suscripción de tooyour de disco duro virtual local mediante `azure vm disk create` o `azure vm disk upload`.</span><span class="sxs-lookup"><span data-stu-id="c9555-115">If you don't find hello disk that you want toouse, you may upload a local VHD tooyour subscription by using `azure vm disk create` or `azure vm disk upload`.</span></span> <span data-ttu-id="c9555-116">Un ejemplo de `disk create` sería como en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="c9555-116">An example of `disk create` would be as in hello following example:</span></span>
   
    ```azurecli
    azure vm disk create myVhd .\TempDisk\test.VHD -l "East US" -o Linux
    ```

    <span data-ttu-id="c9555-117">Hola de salida es similar toohello siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="c9555-117">hello output is similar toohello following example:</span></span>

    ```azurecli
    info:    Executing command vm disk create
    + Retrieving storage accounts
    info:    VHD size : 10 GB
    info:    Uploading 10485760.5 KB
    Requested:100.0% Completed:100.0% Running:   0 Time:   25s Speed:    82 KB/s
    info:    Finishing computing MD5 hash, 16% is complete.
    info:    https://mystorageaccount.blob.core.windows.net/disks/myVHD.vhd was
    uploaded successfully
    info:    vm disk create command OK
    ```
   
   <span data-ttu-id="c9555-118">También puede usar `azure vm disk upload` tooupload una cuenta de almacenamiento específico de tooa de disco duro virtual.</span><span class="sxs-lookup"><span data-stu-id="c9555-118">You may also use `azure vm disk upload` tooupload a VHD tooa specific storage account.</span></span> <span data-ttu-id="c9555-119">Leer más información acerca de hello comandos toomanage los discos de datos de la máquina virtual de Azure [aquí](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="c9555-119">Read more about hello commands toomanage your Azure virtual machine data disks [over here](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span>

4. <span data-ttu-id="c9555-120">Ahora adjuntar Hola había deseado de máquina virtual de tooyour de disco duro virtual:</span><span class="sxs-lookup"><span data-stu-id="c9555-120">Now you attach hello desired VHD tooyour virtual machine:</span></span>
   
    ```azurecli
    azure vm disk attach myVM myVhd
    ```
   
   <span data-ttu-id="c9555-121">Asegúrese de que tooreplace *myVM* con el nombre de saludo de la máquina virtual, y *myVHD* con el disco duro virtual deseado.</span><span class="sxs-lookup"><span data-stu-id="c9555-121">Make sure tooreplace *myVM* with hello name of your virtual machine, and *myVHD* with your desired VHD.</span></span>

5. <span data-ttu-id="c9555-122">Puede comprobar disco hello es toohello adjunta la máquina virtual con `azure vm disk list <virtual-machine-name>`:</span><span class="sxs-lookup"><span data-stu-id="c9555-122">You can verify hello disk is attached toohello virtual machine with `azure vm disk list <virtual-machine-name>`:</span></span>
   
    ```azurecli
    azure vm disk list myVM
    ```

    <span data-ttu-id="c9555-123">Hola de salida es similar toohello siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="c9555-123">hello output is similar toohello following example:</span></span>

    ```azurecli
     info:    Executing command vm disk list
   
   * Fetching disk images
   * Getting virtual machines
   * Getting VM disks
     data:    Lun  Size(GB)  Blob-Name                         OS
     data:    ---  --------  --------------------------------  -----
     data:         30        TestVM-2645b8030676c8f8.vhd  Linux
     data:    1    10        test.VHD
     data:    0    100        TestVM-76f7ee1ef0f6dddc.vhd
     info:    vm disk list command OK
    ```

> [!NOTE]
> <span data-ttu-id="c9555-124">Después de agregar un disco de datos, podrá necesita toolog en la máquina virtual de toohello e inicializar disco Hola para máquina virtual de hello pueda usar disco hello para el almacenamiento (vea Hola siguiendo los pasos para obtener más información en toodo inicializar disco hello).</span><span class="sxs-lookup"><span data-stu-id="c9555-124">After you add a data disk, you'll need toolog on toohello virtual machine and initialize hello disk so hello virtual machine can use hello disk for storage (see hello following steps for more information on how toodo initialize hello disk).</span></span>
> 
> 

