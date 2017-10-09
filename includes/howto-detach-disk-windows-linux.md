<span data-ttu-id="2149f-101">Cuando ya no necesita un disco de datos que es un equipo virtual tooa conectados, puede separar fácilmente.</span><span class="sxs-lookup"><span data-stu-id="2149f-101">When you no longer need a data disk that's attached tooa virtual machine, you can easily detach it.</span></span> <span data-ttu-id="2149f-102">Separar un disco quita el disco de saludo de la máquina virtual de hello, pero no elimina el disco de Hola Hola cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="2149f-102">Detaching a disk removes hello disk from hello virtual machine, but doesn't delete hello disk from hello Azure storage account.</span></span>

<span data-ttu-id="2149f-103">Si desea volver a datos existentes de toouse hello en el disco de hello, puede adjuntarla toohello misma máquina virtual, u otro.</span><span class="sxs-lookup"><span data-stu-id="2149f-103">If you want toouse hello existing data on hello disk again, you can reattach it toohello same virtual machine, or another one.</span></span>  

> [!NOTE]
> <span data-ttu-id="2149f-104">toodetach un disco del sistema operativo, primero debe máquina virtual de toodelete Hola.</span><span class="sxs-lookup"><span data-stu-id="2149f-104">toodetach an operating system disk, you first need toodelete hello virtual machine.</span></span>
>

## <a name="find-hello-disk"></a><span data-ttu-id="2149f-105">Encuentra el disco de Hola</span><span class="sxs-lookup"><span data-stu-id="2149f-105">Find hello disk</span></span>
<span data-ttu-id="2149f-106">Si no conoce el nombre hello de Hola disco o desea tooverify, antes de separarla, siga estos pasos.</span><span class="sxs-lookup"><span data-stu-id="2149f-106">If you don't know hello name of hello disk or want tooverify it before you detach it, follow these steps.</span></span>

1. <span data-ttu-id="2149f-107">Inicie sesión en toohello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2149f-107">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="2149f-108">Haga clic en **máquinas virtuales**, y, a continuación, seleccione Hola VM adecuado.</span><span class="sxs-lookup"><span data-stu-id="2149f-108">Click **Virtual Machines**, and then select hello appropriate VM.</span></span>

3. <span data-ttu-id="2149f-109">Haga clic en **discos** a lo largo de hello borde izquierdo del panel de la máquina virtual de hello, en **configuración**.</span><span class="sxs-lookup"><span data-stu-id="2149f-109">Click **Disks** along hello left edge of hello virtual machine dashboard, under **Settings**.</span></span>

 <span data-ttu-id="2149f-110">panel de la máquina virtual de Hello muestra hello nombre y tipo de todos los discos conectados.</span><span class="sxs-lookup"><span data-stu-id="2149f-110">hello virtual machine dashboard lists hello name and type of all attached disks.</span></span> <span data-ttu-id="2149f-111">Por ejemplo, esta pantalla muestra una máquina virtual con un disco de sistema operativo y un disco de datos:</span><span class="sxs-lookup"><span data-stu-id="2149f-111">For example, this screen shows a virtual machine with one operating system (OS) disk and one data disk:</span></span>

    ![Buscar disco de datos](./media/howto-detach-disk-windows-linux/vmwithdisklist.png)

## <a name="detach-hello-disk"></a><span data-ttu-id="2149f-113">Desconectar el disco de Hola</span><span class="sxs-lookup"><span data-stu-id="2149f-113">Detach hello disk</span></span>
1. <span data-ttu-id="2149f-114">En el portal de Azure hello, haga clic en **máquinas virtuales**y, a continuación, haga clic en nombre de Hola de máquina virtual de Hola que tiene un disco de datos de hello desea toodetach.</span><span class="sxs-lookup"><span data-stu-id="2149f-114">From hello Azure portal, click **Virtual Machines**, and then click hello name of hello virtual machine that has hello data disk you want toodetach.</span></span>

2. <span data-ttu-id="2149f-115">Haga clic en **discos** a lo largo de hello borde izquierdo del panel de la máquina virtual de hello, en **configuración**.</span><span class="sxs-lookup"><span data-stu-id="2149f-115">Click **Disks** along hello left edge of hello virtual machine dashboard, under **Settings**.</span></span>

3. <span data-ttu-id="2149f-116">Haga clic en el disco de Hola que desee toodetach.</span><span class="sxs-lookup"><span data-stu-id="2149f-116">Click hello disk you want toodetach.</span></span>

  ![Identificar Hola disco toodetach](./media/howto-detach-disk-windows-linux/disklist.png)

4. <span data-ttu-id="2149f-118">En la barra de comandos de hello, haga clic en **separar**.</span><span class="sxs-lookup"><span data-stu-id="2149f-118">From hello command bar, click **Detach**.</span></span>

  ![Busque Hola detach, comando](./media/howto-detach-disk-windows-linux/diskdetachcommand.png)

5. <span data-ttu-id="2149f-120">En la ventana de confirmación de hello, haga clic en **Sí** disco de hello toodetach.</span><span class="sxs-lookup"><span data-stu-id="2149f-120">In hello confirmation window, click **Yes** toodetach hello disk.</span></span>

  ![Confirmar desconectando el disco Hola](./media/howto-detach-disk-windows-linux/confirmdetach.png)

<span data-ttu-id="2149f-122">disco de Hello permanece en el almacenamiento pero ya no es máquina virtual de tooa adjunto.</span><span class="sxs-lookup"><span data-stu-id="2149f-122">hello disk remains in storage but is no longer attached tooa virtual machine.</span></span>
