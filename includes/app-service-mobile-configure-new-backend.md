
1. <span data-ttu-id="0d5b5-101">Haga clic en hello **servicios de aplicaciones** botón, seleccione el back-end de aplicaciones móviles, seleccione **inicio rápido**y, a continuación, seleccione la plataforma de cliente (iOS, Android, Xamarin, Cordova).</span><span class="sxs-lookup"><span data-stu-id="0d5b5-101">Click hello **App Services** button, select your Mobile Apps back end, select **Quickstart**, and then select your client platform (iOS, Android, Xamarin, Cordova).</span></span>

    ![Azure Portal con inicio rápido de Mobile Apps resaltado][quickstart]

2. <span data-ttu-id="0d5b5-103">Si no hay configurada una conexión de base de datos, cree uno mediante acciones Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="0d5b5-103">If a database connection is not configured, create one by doing hello following:</span></span>

    ![Portal de Azure con aplicaciones de Mobile Connect toodatabase][connect]

    <span data-ttu-id="0d5b5-105">a.</span><span class="sxs-lookup"><span data-stu-id="0d5b5-105">a.</span></span> <span data-ttu-id="0d5b5-106">Cree una nueva instancia y un nuevo servidor de SQL Database.</span><span class="sxs-lookup"><span data-stu-id="0d5b5-106">Create a new SQL database and server.</span></span>

    ![Azure Portal con Mobile Apps: creación de una nueva base de datos y un nuevo servidor][server]

    <span data-ttu-id="0d5b5-108">b.</span><span class="sxs-lookup"><span data-stu-id="0d5b5-108">b.</span></span> <span data-ttu-id="0d5b5-109">Espere hasta que la conexión de datos de Hola se creó correctamente.</span><span class="sxs-lookup"><span data-stu-id="0d5b5-109">Wait until hello data connection is successfully created.</span></span>

    ![Notificación de Azure Portal de la creación correcta de conexión de datos][notification]

    <span data-ttu-id="0d5b5-111">c.</span><span class="sxs-lookup"><span data-stu-id="0d5b5-111">c.</span></span> <span data-ttu-id="0d5b5-112">La conexión de datos debe haberse creado correctamente.</span><span class="sxs-lookup"><span data-stu-id="0d5b5-112">Data connection must be successful.</span></span>

    ![Notificación de Azure Portal: "Ya tiene una conexión de datos"][already-connection]

3. <span data-ttu-id="0d5b5-114">En **2. Crear una API de tabla**, seleccione Node.js para **Lenguaje de back-end**.</span><span class="sxs-lookup"><span data-stu-id="0d5b5-114">Under **2. Create a table API**, select Node.js for **Backend language**.</span></span> 
 
4. <span data-ttu-id="0d5b5-115">Acepte la confirmación de hello y, a continuación, seleccione **TodoItem crear tabla**.</span><span class="sxs-lookup"><span data-stu-id="0d5b5-115">Accept hello acknowledgment, and then select **Create TodoItem table**.</span></span>  
    <span data-ttu-id="0d5b5-116">Esta acción crea una nueva tabla de elementos pendientes en la base de datos.</span><span class="sxs-lookup"><span data-stu-id="0d5b5-116">This action creates a new to-do item table in your database.</span></span> 

    >[!IMPORTANT]
    > <span data-ttu-id="0d5b5-117">Cambiar un tooNode.js de back-end existente, sobrescribe todo el contenido.</span><span class="sxs-lookup"><span data-stu-id="0d5b5-117">Switching an existing back end tooNode.js overwrites all contents.</span></span> <span data-ttu-id="0d5b5-118">toocreate un back-end de .NET en su lugar, vea [trabajar con servidor hello back-end de .NET SDK para aplicaciones móviles][instructions].</span><span class="sxs-lookup"><span data-stu-id="0d5b5-118">toocreate a .NET back end instead, see [Work with hello .NET back-end server SDK for Mobile Apps][instructions].</span></span>

<!-- Images. -->
[quickstart]: ./media/app-service-mobile-configure-new-backend/quickstart.png
[connect]: ./media/app-service-mobile-configure-new-backend/connect-to-bd.png
[notification]: ./media/app-service-mobile-configure-new-backend/notification-data-connection-create.png
[server]: ./media/app-service-mobile-configure-new-backend/create-new-server.png
[already-connection]: ./media/app-service-mobile-configure-new-backend/already-connection.png

<!-- URLs -->
[instructions]: ../articles/app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#create-app
