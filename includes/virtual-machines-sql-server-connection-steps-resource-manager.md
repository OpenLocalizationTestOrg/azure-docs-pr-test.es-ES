### <a name="configure-a-dns-label-for-hello-public-ip-address"></a><span data-ttu-id="ff8a8-101">Configuración de una etiqueta de DNS para la dirección IP pública Hola</span><span class="sxs-lookup"><span data-stu-id="ff8a8-101">Configure a DNS Label for hello public IP address</span></span>

<span data-ttu-id="ff8a8-102">tooconnect toohello motor de base de datos de SQL Server de hello Internet, considere la posibilidad de crear una etiqueta de DNS para la dirección IP pública.</span><span class="sxs-lookup"><span data-stu-id="ff8a8-102">tooconnect toohello SQL Server Database Engine from hello Internet, consider creating a DNS Label for your public IP address.</span></span> <span data-ttu-id="ff8a8-103">Puede conectarse mediante la dirección IP, pero Hola etiqueta DNS crea un registro que sea más fácil tooidentify y resúmenes Hola subyacente la dirección IP pública.</span><span class="sxs-lookup"><span data-stu-id="ff8a8-103">You can connect by IP address, but hello DNS Label creates an A Record that is easier tooidentify and abstracts hello underlying public IP address.</span></span>

> [!NOTE]
> <span data-ttu-id="ff8a8-104">Etiquetas de DNS no son necesarias si piensa tooonly conectar toohello SQL Server instancia dentro de hello misma red Virtual o solo localmente.</span><span class="sxs-lookup"><span data-stu-id="ff8a8-104">DNS Labels are not required if you plan tooonly connect toohello SQL Server instance within hello same Virtual Network or only locally.</span></span>

<span data-ttu-id="ff8a8-105">toocreate una etiqueta de DNS, seleccione primero **máquinas virtuales** en el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="ff8a8-105">toocreate a DNS Label, first select **Virtual machines** in hello portal.</span></span> <span data-ttu-id="ff8a8-106">Seleccione su toobring de VM de SQL Server sus propiedades.</span><span class="sxs-lookup"><span data-stu-id="ff8a8-106">Select your SQL Server VM toobring up its properties.</span></span>

1. <span data-ttu-id="ff8a8-107">En información general de máquina virtual de hello, seleccione su **dirección IP pública**.</span><span class="sxs-lookup"><span data-stu-id="ff8a8-107">In hello virtual machine overview, select your **Public IP address**.</span></span>

    ![dirección ip pública](./media/virtual-machines-sql-server-connection-steps/rm-public-ip-address.png)

1. <span data-ttu-id="ff8a8-109">En Propiedades de hello para la dirección IP pública, expanda **configuración**.</span><span class="sxs-lookup"><span data-stu-id="ff8a8-109">In hello properties for your Public IP address, expand **Configuration**.</span></span>

1. <span data-ttu-id="ff8a8-110">Escriba un nombre para la etiqueta DNS.</span><span class="sxs-lookup"><span data-stu-id="ff8a8-110">Enter a DNS Label name.</span></span> <span data-ttu-id="ff8a8-111">Este nombre es un registro que pueden ser utilizados tooconnect tooyour VM de SQL Server por nombre en lugar de por dirección IP directamente.</span><span class="sxs-lookup"><span data-stu-id="ff8a8-111">This name is an A Record that can be used tooconnect tooyour SQL Server VM by name instead of by IP Address directly.</span></span>

1. <span data-ttu-id="ff8a8-112">Haga clic en hello **guardar** botón.</span><span class="sxs-lookup"><span data-stu-id="ff8a8-112">Click hello **Save** button.</span></span>

    ![etiqueta dns](./media/virtual-machines-sql-server-connection-steps/rm-dns-label.png)

### <a name="connect-toohello-database-engine-from-another-computer"></a><span data-ttu-id="ff8a8-114">Conectar toohello motor de base de datos desde otro equipo</span><span class="sxs-lookup"><span data-stu-id="ff8a8-114">Connect toohello Database Engine from another computer</span></span>

1. <span data-ttu-id="ff8a8-115">En un equipo conectado toohello internet, abra SQL Server Management Studio (SSMS).</span><span class="sxs-lookup"><span data-stu-id="ff8a8-115">On a computer connected toohello internet, open SQL Server Management Studio (SSMS).</span></span> <span data-ttu-id="ff8a8-116">Si no tiene SQL Server Management Studio, puede descargarla [aquí](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span><span class="sxs-lookup"><span data-stu-id="ff8a8-116">If you do not have SQL Server Management Studio, you can download it [here](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span></span>

1. <span data-ttu-id="ff8a8-117">Hola **conectar tooServer** o **conectar tooDatabase motor** cuadro de diálogo, editar hello **nombre del servidor** valor.</span><span class="sxs-lookup"><span data-stu-id="ff8a8-117">In hello **Connect tooServer** or **Connect tooDatabase Engine** dialog box, edit hello **Server name** value.</span></span> <span data-ttu-id="ff8a8-118">Escriba la dirección IP de Hola o nombre DNS completo de la máquina virtual de hello (determinado en la tarea anterior de hello).</span><span class="sxs-lookup"><span data-stu-id="ff8a8-118">Enter hello IP address or full DNS name of hello virtual machine (determined in hello previous task).</span></span> <span data-ttu-id="ff8a8-119">También puede agregar una coma y proporcionar el puerto TCP de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="ff8a8-119">You can also add a comma and provide SQL Server's TCP port.</span></span> <span data-ttu-id="ff8a8-120">Por ejemplo: `mysqlvmlabel.eastus.cloudapp.azure.com,1433`.</span><span class="sxs-lookup"><span data-stu-id="ff8a8-120">For example, `mysqlvmlabel.eastus.cloudapp.azure.com,1433`.</span></span>

1. <span data-ttu-id="ff8a8-121">Hola **autenticación** cuadro, seleccione **autenticación de SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="ff8a8-121">In hello **Authentication** box, select **SQL Server Authentication**.</span></span>

1. <span data-ttu-id="ff8a8-122">Hola **inicio de sesión** cuadro, escriba un nombre Hola de un inicio de sesión SQL válido.</span><span class="sxs-lookup"><span data-stu-id="ff8a8-122">In hello **Login** box, type hello name of a valid SQL login.</span></span>

1. <span data-ttu-id="ff8a8-123">Hola **contraseña** cuadro, escriba la contraseña de inicio de sesión de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="ff8a8-123">In hello **Password** box, type hello password of hello login.</span></span>

1. <span data-ttu-id="ff8a8-124">Haga clic en **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="ff8a8-124">Click **Connect**.</span></span>

    ![conexión ssms](./media/virtual-machines-sql-server-connection-steps/rm-ssms-connect.png)