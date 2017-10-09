## <a name="prepare-tooauthenticate-azure-resource-manager-requests"></a><span data-ttu-id="1eb72-101">Preparar tooauthenticate solicitudes del Administrador de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="1eb72-101">Prepare tooauthenticate Azure Resource Manager requests</span></span>
<span data-ttu-id="1eb72-102">Debe autenticar todas las operaciones de Hola que se realizan en los recursos con hello [Azure Resource Manager] [ lnk-authenticate-arm] con Azure Active Directory (AD).</span><span class="sxs-lookup"><span data-stu-id="1eb72-102">You must authenticate all hello operations that you perform on resources using hello [Azure Resource Manager][lnk-authenticate-arm] with Azure Active Directory (AD).</span></span> <span data-ttu-id="1eb72-103">Hola tooconfigure de manera más sencilla es toouse PowerShell o CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="1eb72-103">hello easiest way tooconfigure this is toouse PowerShell or Azure CLI.</span></span>

<span data-ttu-id="1eb72-104">Instalar hello [cmdlets de PowerShell de Azure] [ lnk-powershell-install] antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="1eb72-104">Install hello [Azure PowerShell cmdlets][lnk-powershell-install] before you continue.</span></span>

<span data-ttu-id="1eb72-105">Hola siguientes pasos muestran cómo tooset la autenticación de contraseña para una aplicación de AD con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1eb72-105">hello following steps show how tooset up password authentication for an AD application using PowerShell.</span></span> <span data-ttu-id="1eb72-106">Puede ejecutar estos comandos en una sesión de PowerShell estándar.</span><span class="sxs-lookup"><span data-stu-id="1eb72-106">You can run these commands in a standard PowerShell session.</span></span>

1. <span data-ttu-id="1eb72-107">Inicie sesión en tooyour suscripción de Azure con hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="1eb72-107">Log in tooyour Azure subscription using hello following command:</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

1. <span data-ttu-id="1eb72-108">Si tiene varias suscripciones de Azure, iniciar sesión en tooAzure concede acceso tooall hello Azure suscripciones asociadas con sus credenciales.</span><span class="sxs-lookup"><span data-stu-id="1eb72-108">If you have multiple Azure subscriptions, signing in tooAzure grants you access tooall hello Azure subscriptions associated with your credentials.</span></span> <span data-ttu-id="1eb72-109">Usar hello siguiente comando toolist hello Azure suscripciones disponibles para usted toouse:</span><span class="sxs-lookup"><span data-stu-id="1eb72-109">Use hello following command toolist hello Azure subscriptions available for you toouse:</span></span>

    ```powershell
    Get-AzureRMSubscription
    ```

    <span data-ttu-id="1eb72-110">Usar hello después de suscripción de tooselect de comando que desea toouse toorun Hola comandos toomanage su centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="1eb72-110">Use hello following command tooselect subscription that you want toouse toorun hello commands toomanage your IoT hub.</span></span> <span data-ttu-id="1eb72-111">Puede usar el nombre de la suscripción de Hola o Id. de salida de hello del comando anterior hello:</span><span class="sxs-lookup"><span data-stu-id="1eb72-111">You can use either hello subscription name or ID from hello output of hello previous command:</span></span>

    ```powershell
    Select-AzureRMSubscription `
        -SubscriptionName "{your subscription name}"
    ```

2. <span data-ttu-id="1eb72-112">Anote los valores de **TenantId** y **SubscriptionId**.</span><span class="sxs-lookup"><span data-stu-id="1eb72-112">Make a note of your **TenantId** and **SubscriptionId**.</span></span> <span data-ttu-id="1eb72-113">Los necesitará más adelante.</span><span class="sxs-lookup"><span data-stu-id="1eb72-113">You need them later.</span></span>
3. <span data-ttu-id="1eb72-114">Cree una nueva aplicación de Azure Active Directory mediante Hola siguiente comando, reemplazando los marcadores de posición de hello:</span><span class="sxs-lookup"><span data-stu-id="1eb72-114">Create a new Azure Active Directory application using hello following command, replacing hello place holders:</span></span>
   
   * <span data-ttu-id="1eb72-115">**{Nombre para mostrar}**: nombre para mostrar de la aplicación, por ejemplo, **MySampleApp**.</span><span class="sxs-lookup"><span data-stu-id="1eb72-115">**{Display name}:** a display name for your application such as **MySampleApp**</span></span>
   * <span data-ttu-id="1eb72-116">**{URL de la página de inicio}:** Hola como dirección URL de página de inicio de saludo de la aplicación **http://mysampleapp/home**.</span><span class="sxs-lookup"><span data-stu-id="1eb72-116">**{Home page URL}:** hello URL of hello home page of your app such as **http://mysampleapp/home**.</span></span> <span data-ttu-id="1eb72-117">Esta dirección URL no es necesario toopoint real de tooa la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1eb72-117">This URL does not need toopoint tooa real application.</span></span>
   * <span data-ttu-id="1eb72-118">**{Identificador de aplicación}**: identificador único, por ejemplo, **http://mysampleapp**.</span><span class="sxs-lookup"><span data-stu-id="1eb72-118">**{Application identifier}:** A unique identifier such as **http://mysampleapp**.</span></span> <span data-ttu-id="1eb72-119">Esta dirección URL no es necesario toopoint real de tooa la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1eb72-119">This URL does not need toopoint tooa real application.</span></span>
   * <span data-ttu-id="1eb72-120">**{Password}:** una contraseña que se utiliza tooauthenticate con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1eb72-120">**{Password}:** A password that you use tooauthenticate with your app.</span></span>
     
     ```powershell
     New-AzureRmADApplication -DisplayName {Display name} -HomePage {Home page URL} -IdentifierUris {Application identifier} -Password {Password}
     ```
4. <span data-ttu-id="1eb72-121">Tome nota de hello **ApplicationId** de aplicación Hola que ha creado.</span><span class="sxs-lookup"><span data-stu-id="1eb72-121">Make a note of hello **ApplicationId** of hello application you created.</span></span> <span data-ttu-id="1eb72-122">Lo necesitará más adelante.</span><span class="sxs-lookup"><span data-stu-id="1eb72-122">You need this later.</span></span>
5. <span data-ttu-id="1eb72-123">Crear una nueva entidad de servicio con hello siguiente comando, reemplazando **{MyApplicationId}** con hello **ApplicationId** del paso anterior hello:</span><span class="sxs-lookup"><span data-stu-id="1eb72-123">Create a new service principal using hello following command, replacing **{MyApplicationId}** with hello **ApplicationId** from hello previous step:</span></span>
   
    ```powershell
    New-AzureRmADServicePrincipal -ApplicationId {MyApplicationId}
    ```
6. <span data-ttu-id="1eb72-124">Configurar una asignación de roles con hello siguiente comando, reemplazando **{MyApplicationId}** con su **ApplicationId**.</span><span class="sxs-lookup"><span data-stu-id="1eb72-124">Set up a role assignment using hello following command, replacing **{MyApplicationId}** with your **ApplicationId**.</span></span>
   
    ```powershell
    New-AzureRmRoleAssignment -RoleDefinitionName Owner -ServicePrincipalName {MyApplicationId}
    ```

<span data-ttu-id="1eb72-125">Ahora ha terminado de crear aplicación de Azure AD de Hola que le permite tooauthenticate desde su aplicación personalizada de C#.</span><span class="sxs-lookup"><span data-stu-id="1eb72-125">You have now finished creating hello Azure AD application that enables you tooauthenticate from your custom C# application.</span></span> <span data-ttu-id="1eb72-126">Necesita Hola siguiendo los valores más adelante en este tutorial:</span><span class="sxs-lookup"><span data-stu-id="1eb72-126">You need hello following values later in this tutorial:</span></span>

* <span data-ttu-id="1eb72-127">TenantId</span><span class="sxs-lookup"><span data-stu-id="1eb72-127">TenantId</span></span>
* <span data-ttu-id="1eb72-128">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="1eb72-128">SubscriptionId</span></span>
* <span data-ttu-id="1eb72-129">ApplicationId</span><span class="sxs-lookup"><span data-stu-id="1eb72-129">ApplicationId</span></span>
* <span data-ttu-id="1eb72-130">Password</span><span class="sxs-lookup"><span data-stu-id="1eb72-130">Password</span></span>

[lnk-authenticate-arm]: https://msdn.microsoft.com/library/azure/dn790557.aspx
[lnk-powershell-install]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps
