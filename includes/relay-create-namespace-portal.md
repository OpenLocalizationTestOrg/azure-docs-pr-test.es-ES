1. <span data-ttu-id="6ebb8-101">Inicie sesión en toohello [portal de Azure][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="6ebb8-101">Log on toohello [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="6ebb8-102">En el panel de navegación izquierdo de hello del portal de hello, haga clic en **New**, a continuación, haga clic en **integración empresarial**y, a continuación, haga clic en **retransmisión**.</span><span class="sxs-lookup"><span data-stu-id="6ebb8-102">In hello left navigation pane of hello portal, click **New**, then click **Enterprise Integration**, and then click **Relay**.</span></span>
3. <span data-ttu-id="6ebb8-103">Hola **crear espacio de nombres** cuadro de diálogo, escriba un nombre de espacio de nombres.</span><span class="sxs-lookup"><span data-stu-id="6ebb8-103">In hello **Create namespace** dialog, enter a namespace name.</span></span> <span data-ttu-id="6ebb8-104">sistema de Hello comprueba inmediatamente toosee si Hola nombre está disponible.</span><span class="sxs-lookup"><span data-stu-id="6ebb8-104">hello system immediately checks toosee if hello name is available.</span></span>
4. <span data-ttu-id="6ebb8-105">Hola **suscripción** , a continuación, elija una suscripción de Azure en qué espacio de nombres de hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="6ebb8-105">In hello **Subscription** field, choose an Azure subscription in which toocreate hello namespace.</span></span>
5. <span data-ttu-id="6ebb8-106">Hola  **[grupo de recursos](../articles/azure-resource-manager/resource-group-portal.md)**  , a continuación, elija un grupo de recursos existente en qué Hola live espacio de nombres o cree uno nuevo.</span><span class="sxs-lookup"><span data-stu-id="6ebb8-106">In hello **[Resource group](../articles/azure-resource-manager/resource-group-portal.md)** field, choose an existing resource group in which hello namespace will live, or create a new one.</span></span>      
6. <span data-ttu-id="6ebb8-107">En **ubicación**, elegir Hola país o una región en la que se debe hospedar el espacio de nombres.</span><span class="sxs-lookup"><span data-stu-id="6ebb8-107">In **Location**, choose hello country or region in which your namespace should be hosted.</span></span>
   
    ![Crear un espacio de nombres][create-namespace]
7. <span data-ttu-id="6ebb8-109">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="6ebb8-109">Click **Create**.</span></span> <span data-ttu-id="6ebb8-110">sistema de Hello ahora crea el espacio de nombres y lo habilita.</span><span class="sxs-lookup"><span data-stu-id="6ebb8-110">hello system now creates your namespace and enables it.</span></span> <span data-ttu-id="6ebb8-111">Después de unos minutos, Hola sistema proporcione los recursos de su cuenta.</span><span class="sxs-lookup"><span data-stu-id="6ebb8-111">After a few minutes, hello system provisions resources for your account.</span></span>

### <a name="obtain-hello-management-credentials"></a><span data-ttu-id="6ebb8-112">Obtener las credenciales de administración de Hola</span><span class="sxs-lookup"><span data-stu-id="6ebb8-112">Obtain hello management credentials</span></span>
1. <span data-ttu-id="6ebb8-113">Hola lista de espacios de nombres, haga clic en hello que acaba de crear espacio de nombres.</span><span class="sxs-lookup"><span data-stu-id="6ebb8-113">In hello list of namespaces, click hello newly created namespace name.</span></span>
2. <span data-ttu-id="6ebb8-114">En la hoja de espacio de nombres de hello, haga clic en **directivas de acceso compartido**.</span><span class="sxs-lookup"><span data-stu-id="6ebb8-114">In hello namespace blade, click **Shared access policies**.</span></span>
3. <span data-ttu-id="6ebb8-115">Hola **directivas de acceso compartido** hoja, haga clic en **RootManageSharedAccessKey**.</span><span class="sxs-lookup"><span data-stu-id="6ebb8-115">In hello **Shared access policies** blade, click **RootManageSharedAccessKey**.</span></span>
   
    ![información de conexión][connection-info]
4. <span data-ttu-id="6ebb8-117">Hola **directiva: RootManageSharedAccessKey** hoja, haga clic en botón de copiar Hola siguiente demasiado**clave principal: cadena de conexión**, Portapapeles toocopy Hola conexión cadena tooyour para su uso posterior.</span><span class="sxs-lookup"><span data-stu-id="6ebb8-117">In hello **Policy: RootManageSharedAccessKey** blade, click hello copy button next too**Connection string–primary key**, toocopy hello connection string tooyour clipboard for later use.</span></span> <span data-ttu-id="6ebb8-118">Pegue este valor en el Bloc de notas o cualquier otra ubicación temporal.</span><span class="sxs-lookup"><span data-stu-id="6ebb8-118">Paste this value into Notepad or some other temporary location.</span></span>
   
    ![connection-string][connection-string]

5. <span data-ttu-id="6ebb8-120">Paso anterior repetición hello, copiar y pegar el valor de Hola de **clave principal** tooa ubicación temporal para su uso posterior.</span><span class="sxs-lookup"><span data-stu-id="6ebb8-120">Repeat hello previous step, copying and pasting hello value of **Primary key** tooa temporary location for later use.</span></span>  

<!--Image references-->

[create-namespace]: ./media/relay-create-namespace-portal/create-namespace.png
[connection-info]: ./media/relay-create-namespace-portal/connection-info.png
[connection-string]: ./media/relay-create-namespace-portal/connection-string.png
[Azure portal]: https://portal.azure.com
