### <a name="create-a-new-logical-sql-server-in-the-azure-portal"></a><span data-ttu-id="02d21-101">Creación un nuevo servidor SQL lógico en Azure Portal</span><span class="sxs-lookup"><span data-stu-id="02d21-101">Create a new logical SQL server in the Azure portal</span></span>

1. <span data-ttu-id="02d21-102">Haga clic en **Nuevo**, busque **servidor lógico**y, a continuación, pulse **ENTRAR**.</span><span class="sxs-lookup"><span data-stu-id="02d21-102">Click **New**, search **logical server**, and then hit **ENTER**.</span></span>

    ![buscar servidor lógico](./media/sql-data-warehouse-create-logical-server/search-logical-server.png)
2. <span data-ttu-id="02d21-104">Seleccione **SQL Server (servidor lógico)**</span><span class="sxs-lookup"><span data-stu-id="02d21-104">Select **SQL server (logical server)**</span></span> 

    ![seleccionar servidor lógico](./media/sql-data-warehouse-create-logical-server/select-logical-server.png)
  
3. <span data-ttu-id="02d21-106">Haga clic en **Crear** para abrir la nueva hoja SQL Server (servidor lógico).</span><span class="sxs-lookup"><span data-stu-id="02d21-106">Click **Create** to open the new SQL Server (logical server) blade.</span></span>

   <span data-ttu-id="02d21-107"><kbd>![abrir la hoja de servidor lógico](./media/sql-data-warehouse-create-logical-server/open-logical-server-blade.png) </kbd> <kbd> ![hoja de servidor lógico](./media/sql-data-warehouse-create-logical-server/logical-server-blade.png)</kbd></span><span class="sxs-lookup"><span data-stu-id="02d21-107"><kbd> ![open logical server blade](./media/sql-data-warehouse-create-logical-server/open-logical-server-blade.png) </kbd> <kbd>![logical server blade](./media/sql-data-warehouse-create-logical-server/logical-server-blade.png) </kbd></span></span>
  
3. <span data-ttu-id="02d21-108">En la hoja SQL Server (servidor lógico), en el cuadro de texto Nombre de servidor, proporcione un nombre válido para el nuevo servidor lógico.</span><span class="sxs-lookup"><span data-stu-id="02d21-108">In the SQL Server (logical server) blade's server name text box, provide a valid name for the new logical server.</span></span> <span data-ttu-id="02d21-109">Una marca de verificación verde indica que ha proporcionado un nombre válido.</span><span class="sxs-lookup"><span data-stu-id="02d21-109">A green check mark indicates that you have provided a valid name.</span></span>
    
    ![nuevo nombre de servidor](./media/sql-data-warehouse-create-logical-server/new-name-logical-server.png)

    > [!IMPORTANT]
    > <span data-ttu-id="02d21-111">El nombre completo del nuevo servidor será <nombreDeSuServidor >.database.windows.net.</span><span class="sxs-lookup"><span data-stu-id="02d21-111">The fully qualified name for your new server will be <your_server_name>.database.windows.net.</span></span>
    >
    
4. <span data-ttu-id="02d21-112">En el cuadro de texto de inicio de sesión del administrador del servidor, proporcione un nombre de usuario para el inicio de sesión de autenticación de SQL para este servidor.</span><span class="sxs-lookup"><span data-stu-id="02d21-112">In the Server admin login text box, provide a user name for the SQL authentication login for this server.</span></span> <span data-ttu-id="02d21-113">Este inicio de sesión se conoce como el inicio de sesión de la entidad de seguridad del servidor.</span><span class="sxs-lookup"><span data-stu-id="02d21-113">This login is known as the server principal login.</span></span> <span data-ttu-id="02d21-114">Una marca de verificación verde indica que ha proporcionado un nombre válido.</span><span class="sxs-lookup"><span data-stu-id="02d21-114">A green check mark indicates that you have provided a valid name.</span></span>
    
    ![inicio de sesión de administrador de SQL](./media/sql-data-warehouse-create-logical-server/sql-admin-login.png)
5. <span data-ttu-id="02d21-116">En los cuadros de texto **Contraseña** y **Confirmar contraseña**, escriba una contraseña para la cuenta de inicio de sesión de la entidad de seguridad del servidor.</span><span class="sxs-lookup"><span data-stu-id="02d21-116">In the **Password** and **Confirm password** text boxes, provide a password for the server principal login account.</span></span> <span data-ttu-id="02d21-117">Una marca de verificación verde indica que ha proporcionado una contraseña válida.</span><span class="sxs-lookup"><span data-stu-id="02d21-117">A green check mark indicates that you have provided a valid password.</span></span>
    
    ![contraseña del administrador de SQL](./media/sql-data-warehouse-create-logical-server/sql-admin-password.png)
6. <span data-ttu-id="02d21-119">Seleccione una suscripción en la que tenga permiso para crear objetos.</span><span class="sxs-lookup"><span data-stu-id="02d21-119">Select a subscription in which you have permission to create objects.</span></span>

    ![suscripción](./media/sql-data-warehouse-create-logical-server/subscription.png)
7. <span data-ttu-id="02d21-121">En el cuadro de texto Grupo de recursos, seleccione **Crear nuevo** y, en el cuadro de texto del grupo de recursos, proporcione un nombre válido para el nuevo grupo de recursos (también puede usar un grupo de recursos existente si ya ha creado uno para sí mismo).</span><span class="sxs-lookup"><span data-stu-id="02d21-121">In the Resource group text box, select **Create new** and then, in the resource group text box, provide a valid name for the new resource group (you can also use an existing resource group if you have already created one for yourself).</span></span> <span data-ttu-id="02d21-122">Una marca de verificación verde indica que ha proporcionado un nombre válido.</span><span class="sxs-lookup"><span data-stu-id="02d21-122">A green check mark indicates that you have provided a valid name.</span></span>

    ![nuevo grupo de recursos](./media/sql-data-warehouse-create-logical-server/new-resource-group.png)

8. <span data-ttu-id="02d21-124">En el cuadro de texto **Ubicación**, seleccione un centro de datos adecuado para su ubicación; por ejemplo, "Este de Australia".</span><span class="sxs-lookup"><span data-stu-id="02d21-124">In the **Location** text box, select a data center appropriate to your location - such as "Australia East".</span></span>
    
    ![ubicación del servidor](./media/sql-data-warehouse-create-logical-server/server-location.png)
    
    > [!TIP]
    > <span data-ttu-id="02d21-126">La casilla de verificación **Permitir que los servicios de Azure accedan al servidor** no se puede cambiar en esta hoja.</span><span class="sxs-lookup"><span data-stu-id="02d21-126">The checkbox for **Allow azure services to access server** cannot be changed on this blade.</span></span> <span data-ttu-id="02d21-127">Puede cambiar esta configuración en la hoja del firewall del servidor.</span><span class="sxs-lookup"><span data-stu-id="02d21-127">You can change this setting on the server firewall blade.</span></span> <span data-ttu-id="02d21-128">Para más información, consulte [Get started with security](../articles/sql-database/sql-database-manage-servers-portal.md) (Introducción a la seguridad).</span><span class="sxs-lookup"><span data-stu-id="02d21-128">For more information, see [Get started with security](../articles/sql-database/sql-database-manage-servers-portal.md).</span></span>
    >
    
9. <span data-ttu-id="02d21-129">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="02d21-129">Click **Create**.</span></span>

    ![botón Crear](./media/sql-data-warehouse-create-logical-server/create.png)

