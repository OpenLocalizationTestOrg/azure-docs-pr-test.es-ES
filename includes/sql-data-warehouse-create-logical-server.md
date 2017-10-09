### <a name="create-a-new-logical-sql-server-in-hello-azure-portal"></a><span data-ttu-id="db8fd-101">Crear un nuevo servidor SQL lógico Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="db8fd-101">Create a new logical SQL server in hello Azure portal</span></span>

1. <span data-ttu-id="db8fd-102">Haga clic en **Nuevo**, busque **servidor lógico**y, a continuación, pulse **ENTRAR**.</span><span class="sxs-lookup"><span data-stu-id="db8fd-102">Click **New**, search **logical server**, and then hit **ENTER**.</span></span>

    ![buscar servidor lógico](./media/sql-data-warehouse-create-logical-server/search-logical-server.png)
2. <span data-ttu-id="db8fd-104">Seleccione **SQL Server (servidor lógico)**</span><span class="sxs-lookup"><span data-stu-id="db8fd-104">Select **SQL server (logical server)**</span></span> 

    ![seleccionar servidor lógico](./media/sql-data-warehouse-create-logical-server/select-logical-server.png)
  
3. <span data-ttu-id="db8fd-106">Haga clic en **crear** hoja tooopen Hola de nuevo SQL Server (servidor lógico).</span><span class="sxs-lookup"><span data-stu-id="db8fd-106">Click **Create** tooopen hello new SQL Server (logical server) blade.</span></span>

   <span data-ttu-id="db8fd-107"><kbd>![abrir la hoja de servidor lógico](./media/sql-data-warehouse-create-logical-server/open-logical-server-blade.png) </kbd> <kbd> ![hoja de servidor lógico](./media/sql-data-warehouse-create-logical-server/logical-server-blade.png)</kbd></span><span class="sxs-lookup"><span data-stu-id="db8fd-107"><kbd> ![open logical server blade](./media/sql-data-warehouse-create-logical-server/open-logical-server-blade.png) </kbd> <kbd>![logical server blade](./media/sql-data-warehouse-create-logical-server/logical-server-blade.png) </kbd></span></span>
  
3. <span data-ttu-id="db8fd-108">En el cuadro de texto de nombre de servidor del módulo de SQL Server (servidor lógico) de hello, proporcione un nombre válido para el servidor lógico nuevo de Hola.</span><span class="sxs-lookup"><span data-stu-id="db8fd-108">In hello SQL Server (logical server) blade's server name text box, provide a valid name for hello new logical server.</span></span> <span data-ttu-id="db8fd-109">Una marca de verificación verde indica que ha proporcionado un nombre válido.</span><span class="sxs-lookup"><span data-stu-id="db8fd-109">A green check mark indicates that you have provided a valid name.</span></span>
    
    ![nuevo nombre de servidor](./media/sql-data-warehouse-create-logical-server/new-name-logical-server.png)

    > [!IMPORTANT]
    > <span data-ttu-id="db8fd-111">Hello nombre completo para el nuevo servidor será < nombreDeSuServidor >. database.windows.net.</span><span class="sxs-lookup"><span data-stu-id="db8fd-111">hello fully qualified name for your new server will be <your_server_name>.database.windows.net.</span></span>
    >
    
4. <span data-ttu-id="db8fd-112">En el cuadro de texto del inicio de sesión Hola de administración de servidor, proporcione un nombre de usuario de inicio de sesión de autenticación de SQL de Hola para este servidor.</span><span class="sxs-lookup"><span data-stu-id="db8fd-112">In hello Server admin login text box, provide a user name for hello SQL authentication login for this server.</span></span> <span data-ttu-id="db8fd-113">Este inicio de sesión se conoce como inicio de sesión principal del servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="db8fd-113">This login is known as hello server principal login.</span></span> <span data-ttu-id="db8fd-114">Una marca de verificación verde indica que ha proporcionado un nombre válido.</span><span class="sxs-lookup"><span data-stu-id="db8fd-114">A green check mark indicates that you have provided a valid name.</span></span>
    
    ![inicio de sesión de administrador de SQL](./media/sql-data-warehouse-create-logical-server/sql-admin-login.png)
5. <span data-ttu-id="db8fd-116">Hola **contraseña** y **Confirmar contraseña** cuadros de texto, proporcione una contraseña para la cuenta de inicio de sesión principal del servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="db8fd-116">In hello **Password** and **Confirm password** text boxes, provide a password for hello server principal login account.</span></span> <span data-ttu-id="db8fd-117">Una marca de verificación verde indica que ha proporcionado una contraseña válida.</span><span class="sxs-lookup"><span data-stu-id="db8fd-117">A green check mark indicates that you have provided a valid password.</span></span>
    
    ![contraseña del administrador de SQL](./media/sql-data-warehouse-create-logical-server/sql-admin-password.png)
6. <span data-ttu-id="db8fd-119">Seleccione una suscripción en el que tiene permiso toocreate objetos.</span><span class="sxs-lookup"><span data-stu-id="db8fd-119">Select a subscription in which you have permission toocreate objects.</span></span>

    ![suscripción](./media/sql-data-warehouse-create-logical-server/subscription.png)
7. <span data-ttu-id="db8fd-121">En el cuadro de texto de grupo de recursos de hello seleccione **crear nuevo** y, a continuación, en el cuadro de texto de grupo de recursos de hello, proporcione un nombre válido para el nuevo grupo de recursos hello (también puede usar un grupo de recursos existente si ya ha creado uno para sí mismo).</span><span class="sxs-lookup"><span data-stu-id="db8fd-121">In hello Resource group text box, select **Create new** and then, in hello resource group text box, provide a valid name for hello new resource group (you can also use an existing resource group if you have already created one for yourself).</span></span> <span data-ttu-id="db8fd-122">Una marca de verificación verde indica que ha proporcionado un nombre válido.</span><span class="sxs-lookup"><span data-stu-id="db8fd-122">A green check mark indicates that you have provided a valid name.</span></span>

    ![nuevo grupo de recursos](./media/sql-data-warehouse-create-logical-server/new-resource-group.png)

8. <span data-ttu-id="db8fd-124">Hola **ubicación** ubicación tooyour adecuado: por ejemplo, "Australia Oriental" del centro de cuadro de texto, seleccione una de datos.</span><span class="sxs-lookup"><span data-stu-id="db8fd-124">In hello **Location** text box, select a data center appropriate tooyour location - such as "Australia East".</span></span>
    
    ![ubicación del servidor](./media/sql-data-warehouse-create-logical-server/server-location.png)
    
    > [!TIP]
    > <span data-ttu-id="db8fd-126">Hola casilla **server tooaccess de permitir que los servicios de azure** no se puede cambiar en esta hoja.</span><span class="sxs-lookup"><span data-stu-id="db8fd-126">hello checkbox for **Allow azure services tooaccess server** cannot be changed on this blade.</span></span> <span data-ttu-id="db8fd-127">Puede cambiar esta configuración en la hoja de firewall del servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="db8fd-127">You can change this setting on hello server firewall blade.</span></span> <span data-ttu-id="db8fd-128">Para más información, consulte [Get started with security](../articles/sql-database/sql-database-manage-servers-portal.md) (Introducción a la seguridad).</span><span class="sxs-lookup"><span data-stu-id="db8fd-128">For more information, see [Get started with security](../articles/sql-database/sql-database-manage-servers-portal.md).</span></span>
    >
    
9. <span data-ttu-id="db8fd-129">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="db8fd-129">Click **Create**.</span></span>

    ![botón Crear](./media/sql-data-warehouse-create-logical-server/create.png)

