## <a name="set-up-azure-cli-for-azure-dns"></a><span data-ttu-id="4ad12-101">Configuración de la CLI de Azure para DNS de Azure</span><span class="sxs-lookup"><span data-stu-id="4ad12-101">Set up Azure CLI for Azure DNS</span></span>

### <a name="before-you-begin"></a><span data-ttu-id="4ad12-102">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="4ad12-102">Before you begin</span></span>

<span data-ttu-id="4ad12-103">Antes de comenzar con la configuración, compruebe que dispone de los elementos siguientes.</span><span class="sxs-lookup"><span data-stu-id="4ad12-103">Verify that you have the following items before beginning your configuration.</span></span>

* <span data-ttu-id="4ad12-104">Una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="4ad12-104">An Azure subscription.</span></span> <span data-ttu-id="4ad12-105">Si todavía no la tiene, puede activar sus [ventajas como suscriptor de MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) o registrarse para obtener una [cuenta gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4ad12-105">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="4ad12-106">Instale la versión más reciente de la CLI de Azure, disponible para Windows, Linux o Mac.</span><span class="sxs-lookup"><span data-stu-id="4ad12-106">Install the latest version of the Azure CLI, available for Windows, Linux, or MAC.</span></span> <span data-ttu-id="4ad12-107">Puede consultar mas información disponible en [Instalación de la CLI de Azure](../articles/cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="4ad12-107">More information is available at [Install the Azure CLI](../articles/cli-install-nodejs.md).</span></span>

### <a name="sign-in-to-your-azure-account"></a><span data-ttu-id="4ad12-108">Inicio de sesión en la cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="4ad12-108">Sign in to your Azure account</span></span>

<span data-ttu-id="4ad12-109">Abra una ventana de consola y autentíquese con sus credenciales.</span><span class="sxs-lookup"><span data-stu-id="4ad12-109">Open a console window and authenticate with your credentials.</span></span> <span data-ttu-id="4ad12-110">Para más información, consulte [Inicio de sesión en Azure desde la CLI de Azure](../articles/xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="4ad12-110">For more information, see [Log in to Azure from the Azure CLI](../articles/xplat-cli-connect.md)</span></span>

```azurecli
azure login
```

### <a name="switch-cli-mode"></a><span data-ttu-id="4ad12-111">Cambio del modo de CLI</span><span class="sxs-lookup"><span data-stu-id="4ad12-111">Switch CLI mode</span></span>

<span data-ttu-id="4ad12-112">La DNS de Azure usa el Administrador de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="4ad12-112">Azure DNS uses Azure Resource Manager.</span></span> <span data-ttu-id="4ad12-113">Asegúrese de cambiar al modo de CLI para usar los comandos de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="4ad12-113">Make sure you switch CLI mode to use Azure Resource Manager commands.</span></span>

```azurecli
azure config mode arm
```

### <a name="select-the-subscription"></a><span data-ttu-id="4ad12-114">Selección de la suscripción</span><span class="sxs-lookup"><span data-stu-id="4ad12-114">Select the subscription</span></span>

<span data-ttu-id="4ad12-115">Compruebe las suscripciones para la cuenta.</span><span class="sxs-lookup"><span data-stu-id="4ad12-115">Check the subscriptions for the account.</span></span>

```azurecli
azure account list
```

<span data-ttu-id="4ad12-116">Elección de la suscripción de Azure que se va a usar.</span><span class="sxs-lookup"><span data-stu-id="4ad12-116">Choose which of your Azure subscriptions to use.</span></span>

```azurecli
azure account set "subscription name"
```

### <a name="create-a-resource-group"></a><span data-ttu-id="4ad12-117">Crear un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="4ad12-117">Create a resource group</span></span>

<span data-ttu-id="4ad12-118">El Administrador de recursos de Azure requiere que todos los grupos de recursos especifiquen una ubicación.</span><span class="sxs-lookup"><span data-stu-id="4ad12-118">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="4ad12-119">Esta se utiliza como ubicación predeterminada para los recursos de ese grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="4ad12-119">This is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="4ad12-120">Sin embargo, puesto que todos los recursos DNS son globales y no regionales, la elección de la ubicación del grupo de recursos no incide en DNS de Azure.</span><span class="sxs-lookup"><span data-stu-id="4ad12-120">However, because all DNS resources are global, not regional, the choice of resource group location has no impact on Azure DNS.</span></span>

<span data-ttu-id="4ad12-121">Puede omitir este paso si utiliza un grupo de recursos existente.</span><span class="sxs-lookup"><span data-stu-id="4ad12-121">You can skip this step if you are using an existing resource group.</span></span>

```azurecli
azure group create -n myresourcegroup --location "West US"
```

### <a name="register-resource-provider"></a><span data-ttu-id="4ad12-122">Registro del proveedor de recursos</span><span class="sxs-lookup"><span data-stu-id="4ad12-122">Register resource provider</span></span>

<span data-ttu-id="4ad12-123">El proveedor de recursos Microsoft.Network administra el servicio DNS de Azure.</span><span class="sxs-lookup"><span data-stu-id="4ad12-123">The Azure DNS service is managed by the Microsoft.Network resource provider.</span></span> <span data-ttu-id="4ad12-124">La suscripción a Azure debe estar registrada para usar este proveedor de recursos antes de utilizar Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="4ad12-124">Your Azure subscription must be registered to use this resource provider before you can use Azure DNS.</span></span> <span data-ttu-id="4ad12-125">Se trata de una operación única para cada suscripción.</span><span class="sxs-lookup"><span data-stu-id="4ad12-125">This is a one-time operation for each subscription.</span></span>

```azurecli
azure provider register --namespace Microsoft.Network
```

