<span data-ttu-id="72dd8-101">toobegin uso del Bus de servicio pone en cola en Azure, primero debe crear un espacio de nombres con un nombre que sea único a través de Azure.</span><span class="sxs-lookup"><span data-stu-id="72dd8-101">toobegin using Service Bus queues in Azure, you must first create a namespace with a name that is unique across Azure.</span></span> <span data-ttu-id="72dd8-102">Un espacio de nombres proporciona un contenedor con un ámbito para el desvío de recursos del bus de servicio en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="72dd8-102">A namespace provides a scoping container for addressing Service Bus resources within your application.</span></span>

<span data-ttu-id="72dd8-103">toocreate un espacio de nombres:</span><span class="sxs-lookup"><span data-stu-id="72dd8-103">toocreate a namespace:</span></span>

1. <span data-ttu-id="72dd8-104">Inicie sesión en toohello [portal de Azure][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="72dd8-104">Log on toohello [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="72dd8-105">En el panel de navegación izquierdo de hello del portal de hello, haga clic en **New**, a continuación, haga clic en **integración empresarial**y, a continuación, haga clic en **Bus de servicio**.</span><span class="sxs-lookup"><span data-stu-id="72dd8-105">In hello left navigation pane of hello portal, click **New**, then click **Enterprise Integration**, and then click **Service Bus**.</span></span>
3. <span data-ttu-id="72dd8-106">Hola **crear espacio de nombres** cuadro de diálogo, escriba un nombre de espacio de nombres.</span><span class="sxs-lookup"><span data-stu-id="72dd8-106">In hello **Create namespace** dialog, enter a namespace name.</span></span> <span data-ttu-id="72dd8-107">sistema de Hello comprueba inmediatamente toosee si Hola nombre está disponible.</span><span class="sxs-lookup"><span data-stu-id="72dd8-107">hello system immediately checks toosee if hello name is available.</span></span>
4. <span data-ttu-id="72dd8-108">Después de realizar el nombre de espacio de nombres de hello seguro está disponible, elija Hola tarifa (Basic, Standard o Premium).</span><span class="sxs-lookup"><span data-stu-id="72dd8-108">After making sure hello namespace name is available, choose hello pricing tier (Basic, Standard, or Premium).</span></span>
5. <span data-ttu-id="72dd8-109">Hola **suscripción** , a continuación, elija una suscripción de Azure en qué espacio de nombres de hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="72dd8-109">In hello **Subscription** field, choose an Azure subscription in which toocreate hello namespace.</span></span>
6. <span data-ttu-id="72dd8-110">Hola **grupo de recursos** , a continuación, elija un grupo de recursos existente en qué Hola live espacio de nombres o cree uno nuevo.</span><span class="sxs-lookup"><span data-stu-id="72dd8-110">In hello **Resource group** field, choose an existing resource group in which hello namespace will live, or create a new one.</span></span>      
7. <span data-ttu-id="72dd8-111">En **ubicación**, elegir Hola país o una región en la que se debe hospedar el espacio de nombres.</span><span class="sxs-lookup"><span data-stu-id="72dd8-111">In **Location**, choose hello country or region in which your namespace should be hosted.</span></span>
   
    ![Crear un espacio de nombres][create-namespace]
8. <span data-ttu-id="72dd8-113">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="72dd8-113">Click **Create**.</span></span> <span data-ttu-id="72dd8-114">sistema de Hello ahora crea el espacio de nombres y lo habilita.</span><span class="sxs-lookup"><span data-stu-id="72dd8-114">hello system now creates your namespace and enables it.</span></span> <span data-ttu-id="72dd8-115">Es posible que tenga toowait unos minutos hasta que proporcione los recursos del sistema Hola para su cuenta.</span><span class="sxs-lookup"><span data-stu-id="72dd8-115">You might have toowait several minutes as hello system provisions resources for your account.</span></span>

### <a name="obtain-hello-management-credentials"></a><span data-ttu-id="72dd8-116">Obtener las credenciales de administración de Hola</span><span class="sxs-lookup"><span data-stu-id="72dd8-116">Obtain hello management credentials</span></span>

1. <span data-ttu-id="72dd8-117">Hola lista de espacios de nombres, haga clic en hello que acaba de crear espacio de nombres.</span><span class="sxs-lookup"><span data-stu-id="72dd8-117">In hello list of namespaces, click hello newly created namespace name.</span></span>
2. <span data-ttu-id="72dd8-118">En la hoja de espacio de nombres de hello, haga clic en **directivas de acceso compartido**.</span><span class="sxs-lookup"><span data-stu-id="72dd8-118">In hello namespace blade, click **Shared access policies**.</span></span>
3. <span data-ttu-id="72dd8-119">Hola **directivas de acceso compartido** hoja, haga clic en **RootManageSharedAccessKey**.</span><span class="sxs-lookup"><span data-stu-id="72dd8-119">In hello **Shared access policies** blade, click **RootManageSharedAccessKey**.</span></span>
   
    ![información de conexión][connection-info]
4. <span data-ttu-id="72dd8-121">Hola **directiva: RootManageSharedAccessKey** hoja, haga clic en botón de copiar Hola siguiente demasiado**clave principal: cadena de conexión**, Portapapeles toocopy Hola conexión cadena tooyour para su uso posterior.</span><span class="sxs-lookup"><span data-stu-id="72dd8-121">In hello **Policy: RootManageSharedAccessKey** blade, click hello copy button next too**Connection string–primary key**, toocopy hello connection string tooyour clipboard for later use.</span></span> <span data-ttu-id="72dd8-122">Pegue este valor en el Bloc de notas o cualquier otra ubicación temporal.</span><span class="sxs-lookup"><span data-stu-id="72dd8-122">Paste this value into Notepad or some other temporary location.</span></span>
   
    ![connection-string][connection-string]

5. <span data-ttu-id="72dd8-124">Paso anterior repetición hello, copiar y pegar el valor de Hola de **clave principal** tooa ubicación temporal para su uso posterior.</span><span class="sxs-lookup"><span data-stu-id="72dd8-124">Repeat hello previous step, copying and pasting hello value of **Primary key** tooa temporary location for later use.</span></span>

<!--Image references-->

[create-namespace]: ./media/service-bus-create-namespace-portal/create-namespace.png
[connection-info]: ./media/service-bus-create-namespace-portal/connection-info.png
[connection-string]: ./media/service-bus-create-namespace-portal/connection-string.png
[Azure portal]: https://portal.azure.com
