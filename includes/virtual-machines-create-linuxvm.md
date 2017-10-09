
1. <span data-ttu-id="feca9-101">Inicie sesión en tooyour suscripción de Azure siguiendo los pasos de hello enumerados en [conectar tooAzure de hello Azure CLI 1.0](../articles/xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="feca9-101">Sign in tooyour Azure subscription using hello steps listed in [Connect tooAzure from hello Azure CLI 1.0](../articles/xplat-cli-connect.md).</span></span>

2. <span data-ttu-id="feca9-102">Asegúrese de que está en el modo de implementación clásica hello como sigue:</span><span class="sxs-lookup"><span data-stu-id="feca9-102">Make sure you are in hello Classic deployment mode as follows:</span></span>

    ```azurecli
    azure config mode asm
    ```

3. <span data-ttu-id="feca9-103">Averiguar imagen de Linux de Hola que desea tooload de imágenes disponibles hello como sigue:</span><span class="sxs-lookup"><span data-stu-id="feca9-103">Find out hello Linux image that you want tooload from hello available images as follows:</span></span>

   ```azurecli   
    azure vm image list | grep "Linux"
    ```
   
    <span data-ttu-id="feca9-104">En una ventana de símbolo del sistema de Windows, use **find** en lugar de grep.</span><span class="sxs-lookup"><span data-stu-id="feca9-104">In a Windows command-prompt window, use **find** instead of grep.</span></span>
   
4. <span data-ttu-id="feca9-105">Use `azure vm create` toocreate una máquina virtual con la imagen de Linux Hola de lista anterior Hola.</span><span class="sxs-lookup"><span data-stu-id="feca9-105">Use `azure vm create` toocreate a VM with hello Linux image from hello previous list.</span></span> <span data-ttu-id="feca9-106">En este paso se crea un servicio en la nube y una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="feca9-106">This step creates a cloud service and storage account.</span></span> <span data-ttu-id="feca9-107">También puede conectar este servicio en la nube VM tooan existente con un `-c` opción.</span><span class="sxs-lookup"><span data-stu-id="feca9-107">You could also connect this VM tooan existing cloud service with a `-c` option.</span></span> <span data-ttu-id="feca9-108">Crear un toolog de punto de conexión SSH en la máquina virtual de Linux toohello con hello `-e` opción.</span><span class="sxs-lookup"><span data-stu-id="feca9-108">Create an SSH endpoint toolog in toohello Linux virtual machine with hello `-e` option.</span></span> <span data-ttu-id="feca9-109">Hello en el ejemplo siguiente se crea una máquina virtual denominada `myVM` con hello `Ubuntu-14_04_4-LTS` imagen Hola `West US` ubicación y agrega un nombre de usuario `ops`:</span><span class="sxs-lookup"><span data-stu-id="feca9-109">hello following example creates a VM named `myVM` using hello `Ubuntu-14_04_4-LTS` image in hello `West US` location, and adds a user name `ops`:</span></span>
   
    ```azurecli
    azure vm create myVM \
        b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB \
        -g ops -p P@ssw0rd! -z "Small" -e -l "West US"
    ```

    <span data-ttu-id="feca9-110">Hola de salida es similar toohello siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="feca9-110">hello output is similar toohello following example:</span></span>

    ```azurecli
    info:    Executing command vm create
    + Looking up image b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB
    + Looking up cloud service
    info:    cloud service myVM not found.
    + Creating cloud service
    + Retrieving storage accounts
    + Creating VM
    info:    vm create command OK
    ```
   
   > [!NOTE]
   > <span data-ttu-id="feca9-111">Para una máquina virtual de Linux, debe proporcionar hello `-e` opción `vm create`.</span><span class="sxs-lookup"><span data-stu-id="feca9-111">For a Linux virtual machine, you must provide hello `-e` option in `vm create`.</span></span> <span data-ttu-id="feca9-112">No es posible tooenable SSH una vez creada la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="feca9-112">It is not possible tooenable SSH after hello virtual machine has been created.</span></span> <span data-ttu-id="feca9-113">Para obtener más detalles sobre SSH, lea [cómo tooUse SSH con Linux en Azure](../articles/virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="feca9-113">For more details on SSH, read [How tooUse SSH with Linux on Azure](../articles/virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

5. <span data-ttu-id="feca9-114">Puede comprobar atributos Hola de hello VM mediante hello `azure vm show` comando.</span><span class="sxs-lookup"><span data-stu-id="feca9-114">You can verify hello attributes of hello VM by using hello `azure vm show` command.</span></span> <span data-ttu-id="feca9-115">Hello en el ejemplo siguiente se muestra información de máquina virtual denominada Hola `myVM`:</span><span class="sxs-lookup"><span data-stu-id="feca9-115">hello following example lists information for hello VM named `myVM`:</span></span>

    ```azurecli   
    azure vm show myVM
    ```

6. <span data-ttu-id="feca9-116">Inicie la máquina virtual con hello `azure vm start` comando como sigue:</span><span class="sxs-lookup"><span data-stu-id="feca9-116">Start your VM with hello `azure vm start` command as follows:</span></span>

    ```azurecli
    azure vm start myVM
    ```

## <a name="next-steps"></a><span data-ttu-id="feca9-117">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="feca9-117">Next steps</span></span>
<span data-ttu-id="feca9-118">Para obtener más información acerca de estos comandos de máquina virtual de Azure CLI 1.0, lea hello [hello mediante Azure CLI 1.0 con API de implementación clásica de hello](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="feca9-118">For details on all these Azure CLI 1.0 virtual machine commands, read hello [Using hello Azure CLI 1.0 with hello Classic deployment API](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span>

