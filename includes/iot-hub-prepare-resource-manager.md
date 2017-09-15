## <a name="prepare-to-authenticate-azure-resource-manager-requests"></a><span data-ttu-id="0138b-101">Prepararse para autenticar solicitudes de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="0138b-101">Prepare to authenticate Azure Resource Manager requests</span></span>
<span data-ttu-id="0138b-102">Debe autenticar todas las operaciones que se realizan en los recursos mediante [Azure Resource Manager][lnk-authenticate-arm] con Azure Active Directory (AD).</span><span class="sxs-lookup"><span data-stu-id="0138b-102">You must authenticate all the operations that you perform on resources using the [Azure Resource Manager][lnk-authenticate-arm] with Azure Active Directory (AD).</span></span> <span data-ttu-id="0138b-103">La manera más sencilla de configurar esto es usar PowerShell o CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="0138b-103">The easiest way to configure this is to use PowerShell or Azure CLI.</span></span>

<span data-ttu-id="0138b-104">Instale los [cmdlets de Azure PowerShell][lnk-powershell-install] antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="0138b-104">Install the [Azure PowerShell cmdlets][lnk-powershell-install] before you continue.</span></span>

<span data-ttu-id="0138b-105">En los pasos siguientes se muestra cómo configurar la autenticación de contraseña para una aplicación de AD mediante PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0138b-105">The following steps show how to set up password authentication for an AD application using PowerShell.</span></span> <span data-ttu-id="0138b-106">Puede ejecutar estos comandos en una sesión de PowerShell estándar.</span><span class="sxs-lookup"><span data-stu-id="0138b-106">You can run these commands in a standard PowerShell session.</span></span>

1. <span data-ttu-id="0138b-107">Inicie sesión en su suscripción de Azure con el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="0138b-107">Log in to your Azure subscription using the following command:</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

1. <span data-ttu-id="0138b-108">Si tiene varias suscripciones de Azure, el inicio de sesión en Azure le concede acceso a todas las suscripciones de Azure asociadas a sus credenciales.</span><span class="sxs-lookup"><span data-stu-id="0138b-108">If you have multiple Azure subscriptions, signing in to Azure grants you access to all the Azure subscriptions associated with your credentials.</span></span> <span data-ttu-id="0138b-109">Use el siguiente comando para mostrar las suscripciones de Azure que están disponibles para su uso:</span><span class="sxs-lookup"><span data-stu-id="0138b-109">Use the following command to list the Azure subscriptions available for you to use:</span></span>

    ```powershell
    Get-AzureRMSubscription
    ```

    <span data-ttu-id="0138b-110">Use el siguiente comando para seleccionar la suscripción que desea usar para ejecutar los comandos para administrar su centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="0138b-110">Use the following command to select subscription that you want to use to run the commands to manage your IoT hub.</span></span> <span data-ttu-id="0138b-111">Puede usar el nombre de la suscripción o el identificador de la salida del comando anterior:</span><span class="sxs-lookup"><span data-stu-id="0138b-111">You can use either the subscription name or ID from the output of the previous command:</span></span>

    ```powershell
    Select-AzureRMSubscription `
        -SubscriptionName "{your subscription name}"
    ```

2. <span data-ttu-id="0138b-112">Anote los valores de **TenantId** y **SubscriptionId**.</span><span class="sxs-lookup"><span data-stu-id="0138b-112">Make a note of your **TenantId** and **SubscriptionId**.</span></span> <span data-ttu-id="0138b-113">Los necesitará más adelante.</span><span class="sxs-lookup"><span data-stu-id="0138b-113">You need them later.</span></span>
3. <span data-ttu-id="0138b-114">Cree una nueva aplicación de Azure Active Directory con el siguiente comando, reemplazando los marcadores de posición:</span><span class="sxs-lookup"><span data-stu-id="0138b-114">Create a new Azure Active Directory application using the following command, replacing the place holders:</span></span>
   
   * <span data-ttu-id="0138b-115">**{Nombre para mostrar}**: nombre para mostrar de la aplicación, por ejemplo, **MySampleApp**.</span><span class="sxs-lookup"><span data-stu-id="0138b-115">**{Display name}:** a display name for your application such as **MySampleApp**</span></span>
   * <span data-ttu-id="0138b-116">**{Dirección URL de la página principal}**: la dirección URL de la página principal de la aplicación, por ejemplo, **http://mysampleapp/home**.</span><span class="sxs-lookup"><span data-stu-id="0138b-116">**{Home page URL}:** the URL of the home page of your app such as **http://mysampleapp/home**.</span></span> <span data-ttu-id="0138b-117">Esta dirección URL no tiene que señalar a una aplicación real.</span><span class="sxs-lookup"><span data-stu-id="0138b-117">This URL does not need to point to a real application.</span></span>
   * <span data-ttu-id="0138b-118">**{Identificador de aplicación}**: identificador único, por ejemplo, **http://mysampleapp**.</span><span class="sxs-lookup"><span data-stu-id="0138b-118">**{Application identifier}:** A unique identifier such as **http://mysampleapp**.</span></span> <span data-ttu-id="0138b-119">Esta dirección URL no tiene que señalar a una aplicación real.</span><span class="sxs-lookup"><span data-stu-id="0138b-119">This URL does not need to point to a real application.</span></span>
   * <span data-ttu-id="0138b-120">**{Contraseña}:** una contraseña que se usa para autenticarse en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0138b-120">**{Password}:** A password that you use to authenticate with your app.</span></span>
     
     ```powershell
     New-AzureRmADApplication -DisplayName {Display name} -HomePage {Home page URL} -IdentifierUris {Application identifier} -Password {Password}
     ```
4. <span data-ttu-id="0138b-121">Anote el **ApplicationId** de la aplicación que ha creado.</span><span class="sxs-lookup"><span data-stu-id="0138b-121">Make a note of the **ApplicationId** of the application you created.</span></span> <span data-ttu-id="0138b-122">Lo necesitará más adelante.</span><span class="sxs-lookup"><span data-stu-id="0138b-122">You need this later.</span></span>
5. <span data-ttu-id="0138b-123">Cree una nueva entidad de servicio con el comando siguiente, reemplazando **{MyApplicationId}** por el valor de **ApplicationId** del paso anterior:</span><span class="sxs-lookup"><span data-stu-id="0138b-123">Create a new service principal using the following command, replacing **{MyApplicationId}** with the **ApplicationId** from the previous step:</span></span>
   
    ```powershell
    New-AzureRmADServicePrincipal -ApplicationId {MyApplicationId}
    ```
6. <span data-ttu-id="0138b-124">Configure una asignación de rol con el comando siguiente, reemplazando **{MyApplicationId}** por su valor de **ApplicationId**.</span><span class="sxs-lookup"><span data-stu-id="0138b-124">Set up a role assignment using the following command, replacing **{MyApplicationId}** with your **ApplicationId**.</span></span>
   
    ```powershell
    New-AzureRmRoleAssignment -RoleDefinitionName Owner -ServicePrincipalName {MyApplicationId}
    ```

<span data-ttu-id="0138b-125">Ahora ha terminado de crear la aplicación de Azure AD que le permitirá autenticarse desde su aplicación de C# personalizada.</span><span class="sxs-lookup"><span data-stu-id="0138b-125">You have now finished creating the Azure AD application that enables you to authenticate from your custom C# application.</span></span> <span data-ttu-id="0138b-126">En este tutorial necesitará más adelante los siguientes valores:</span><span class="sxs-lookup"><span data-stu-id="0138b-126">You need the following values later in this tutorial:</span></span>

* <span data-ttu-id="0138b-127">TenantId</span><span class="sxs-lookup"><span data-stu-id="0138b-127">TenantId</span></span>
* <span data-ttu-id="0138b-128">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="0138b-128">SubscriptionId</span></span>
* <span data-ttu-id="0138b-129">ApplicationId</span><span class="sxs-lookup"><span data-stu-id="0138b-129">ApplicationId</span></span>
* <span data-ttu-id="0138b-130">Password</span><span class="sxs-lookup"><span data-stu-id="0138b-130">Password</span></span>

[lnk-authenticate-arm]: https://msdn.microsoft.com/library/azure/dn790557.aspx
[lnk-powershell-install]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps
