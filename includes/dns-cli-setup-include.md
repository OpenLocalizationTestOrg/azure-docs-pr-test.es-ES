## <a name="set-up-azure-cli-for-azure-dns"></a><span data-ttu-id="8b0b7-101">Configuración de la CLI de Azure para DNS de Azure</span><span class="sxs-lookup"><span data-stu-id="8b0b7-101">Set up Azure CLI for Azure DNS</span></span>

### <a name="before-you-begin"></a><span data-ttu-id="8b0b7-102">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="8b0b7-102">Before you begin</span></span>

<span data-ttu-id="8b0b7-103">Compruebe que dispone de hello siguientes elementos antes de comenzar la configuración.</span><span class="sxs-lookup"><span data-stu-id="8b0b7-103">Verify that you have hello following items before beginning your configuration.</span></span>

* <span data-ttu-id="8b0b7-104">Una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="8b0b7-104">An Azure subscription.</span></span> <span data-ttu-id="8b0b7-105">Si todavía no la tiene, puede activar sus [ventajas como suscriptor de MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) o registrarse para obtener una [cuenta gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8b0b7-105">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="8b0b7-106">Instale Hola la versión más reciente de hello CLI de Azure, disponible para Windows, Linux o Mac.</span><span class="sxs-lookup"><span data-stu-id="8b0b7-106">Install hello latest version of hello Azure CLI, available for Windows, Linux, or MAC.</span></span> <span data-ttu-id="8b0b7-107">Hay disponible más información en [Install hello Azure CLI](../articles/cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="8b0b7-107">More information is available at [Install hello Azure CLI](../articles/cli-install-nodejs.md).</span></span>

### <a name="sign-in-tooyour-azure-account"></a><span data-ttu-id="8b0b7-108">Inicie sesión en tooyour cuenta de Azure</span><span class="sxs-lookup"><span data-stu-id="8b0b7-108">Sign in tooyour Azure account</span></span>

<span data-ttu-id="8b0b7-109">Abra una ventana de consola y autentíquese con sus credenciales.</span><span class="sxs-lookup"><span data-stu-id="8b0b7-109">Open a console window and authenticate with your credentials.</span></span> <span data-ttu-id="8b0b7-110">Para obtener más información, vea [sesión tooAzure de hello CLI de Azure](../articles/xplat-cli-connect.md)</span><span class="sxs-lookup"><span data-stu-id="8b0b7-110">For more information, see [Log in tooAzure from hello Azure CLI](../articles/xplat-cli-connect.md)</span></span>

```azurecli
azure login
```

### <a name="switch-cli-mode"></a><span data-ttu-id="8b0b7-111">Cambio del modo de CLI</span><span class="sxs-lookup"><span data-stu-id="8b0b7-111">Switch CLI mode</span></span>

<span data-ttu-id="8b0b7-112">La DNS de Azure usa el Administrador de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="8b0b7-112">Azure DNS uses Azure Resource Manager.</span></span> <span data-ttu-id="8b0b7-113">Asegúrese de que cambiar comandos de CLI modo toouse Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="8b0b7-113">Make sure you switch CLI mode toouse Azure Resource Manager commands.</span></span>

```azurecli
azure config mode arm
```

### <a name="select-hello-subscription"></a><span data-ttu-id="8b0b7-114">Seleccione la suscripción de Hola</span><span class="sxs-lookup"><span data-stu-id="8b0b7-114">Select hello subscription</span></span>

<span data-ttu-id="8b0b7-115">Compruebe las suscripciones de hello para la cuenta de hello.</span><span class="sxs-lookup"><span data-stu-id="8b0b7-115">Check hello subscriptions for hello account.</span></span>

```azurecli
azure account list
```

<span data-ttu-id="8b0b7-116">Elija qué su toouse de las suscripciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="8b0b7-116">Choose which of your Azure subscriptions toouse.</span></span>

```azurecli
azure account set "subscription name"
```

### <a name="create-a-resource-group"></a><span data-ttu-id="8b0b7-117">Crear un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="8b0b7-117">Create a resource group</span></span>

<span data-ttu-id="8b0b7-118">Azure Resource Manager requiere que todos los grupos de recursos especifiquen una ubicación.</span><span class="sxs-lookup"><span data-stu-id="8b0b7-118">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="8b0b7-119">Esto se utiliza como ubicación predeterminada de Hola para recursos de ese grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="8b0b7-119">This is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="8b0b7-120">Sin embargo, dado que todos los recursos DNS son globales, no regionales, elección de Hola de ubicación del grupo de recursos tiene ningún impacto en el DNS de Azure.</span><span class="sxs-lookup"><span data-stu-id="8b0b7-120">However, because all DNS resources are global, not regional, hello choice of resource group location has no impact on Azure DNS.</span></span>

<span data-ttu-id="8b0b7-121">Puede omitir este paso si utiliza un grupo de recursos existente.</span><span class="sxs-lookup"><span data-stu-id="8b0b7-121">You can skip this step if you are using an existing resource group.</span></span>

```azurecli
azure group create -n myresourcegroup --location "West US"
```

### <a name="register-resource-provider"></a><span data-ttu-id="8b0b7-122">Registro del proveedor de recursos</span><span class="sxs-lookup"><span data-stu-id="8b0b7-122">Register resource provider</span></span>

<span data-ttu-id="8b0b7-123">Hola servicio DNS de Azure se administra mediante el proveedor de recursos de Microsoft.Network Hola.</span><span class="sxs-lookup"><span data-stu-id="8b0b7-123">hello Azure DNS service is managed by hello Microsoft.Network resource provider.</span></span> <span data-ttu-id="8b0b7-124">Su suscripción de Azure debe estar registrado toouse este proveedor de recursos antes de que se puede usar DNS de Azure.</span><span class="sxs-lookup"><span data-stu-id="8b0b7-124">Your Azure subscription must be registered toouse this resource provider before you can use Azure DNS.</span></span> <span data-ttu-id="8b0b7-125">Se trata de una operación única para cada suscripción.</span><span class="sxs-lookup"><span data-stu-id="8b0b7-125">This is a one-time operation for each subscription.</span></span>

```azurecli
azure provider register --namespace Microsoft.Network
```

