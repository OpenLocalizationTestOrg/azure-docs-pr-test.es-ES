## <a name="set-up-azure-powershell-for-azure-dns"></a><span data-ttu-id="ff55d-101">Configuración de Azure PowerShell para Azure DNS</span><span class="sxs-lookup"><span data-stu-id="ff55d-101">Set up Azure PowerShell for Azure DNS</span></span>

### <a name="before-you-begin"></a><span data-ttu-id="ff55d-102">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="ff55d-102">Before you begin</span></span>

<span data-ttu-id="ff55d-103">Compruebe que dispone de hello siguientes elementos antes de comenzar la configuración.</span><span class="sxs-lookup"><span data-stu-id="ff55d-103">Verify that you have hello following items before beginning your configuration.</span></span>

* <span data-ttu-id="ff55d-104">Una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="ff55d-104">An Azure subscription.</span></span> <span data-ttu-id="ff55d-105">Si todavía no la tiene, puede activar sus [ventajas como suscriptor de MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) o registrarse para obtener una [cuenta gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ff55d-105">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="ff55d-106">Necesita la versión más reciente de hello tooinstall de hello cmdlets de PowerShell del Administrador de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="ff55d-106">You need tooinstall hello latest version of hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="ff55d-107">Para obtener más información, consulte [cómo tooinstall y configurar Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="ff55d-107">For more information, see [How tooinstall and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span>

### <a name="sign-in-tooyour-azure-account"></a><span data-ttu-id="ff55d-108">Inicie sesión en tooyour cuenta de Azure</span><span class="sxs-lookup"><span data-stu-id="ff55d-108">Sign in tooyour Azure account</span></span>

<span data-ttu-id="ff55d-109">Abra la consola de PowerShell y conectar con tooyour cuenta.</span><span class="sxs-lookup"><span data-stu-id="ff55d-109">Open your PowerShell console and connect tooyour account.</span></span> <span data-ttu-id="ff55d-110">Para más información, consulte [Uso de PowerShell con Resource Manager](../articles/azure-resource-manager/powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="ff55d-110">For more information, see [Using PowerShell with Resource Manager](../articles/azure-resource-manager/powershell-azure-resource-manager.md).</span></span>

```powershell
Login-AzureRmAccount
```

### <a name="select-hello-subscription"></a><span data-ttu-id="ff55d-111">Seleccione la suscripción de Hola</span><span class="sxs-lookup"><span data-stu-id="ff55d-111">Select hello subscription</span></span>
 
<span data-ttu-id="ff55d-112">Compruebe las suscripciones de hello para la cuenta de hello.</span><span class="sxs-lookup"><span data-stu-id="ff55d-112">Check hello subscriptions for hello account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="ff55d-113">Elija qué su toouse de las suscripciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="ff55d-113">Choose which of your Azure subscriptions toouse.</span></span>

```powershell
Select-AzureRmSubscription -SubscriptionName "your_subscription_name"
```

### <a name="create-a-resource-group"></a><span data-ttu-id="ff55d-114">Crear un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="ff55d-114">Create a resource group</span></span>

<span data-ttu-id="ff55d-115">Azure Resource Manager requiere que todos los grupos de recursos especifiquen una ubicación.</span><span class="sxs-lookup"><span data-stu-id="ff55d-115">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="ff55d-116">Esta ubicación se utiliza como ubicación predeterminada de Hola para recursos de ese grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="ff55d-116">This location is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="ff55d-117">Sin embargo, dado que todos los recursos DNS son globales, no regionales, elección de Hola de ubicación del grupo de recursos tiene ningún impacto en el DNS de Azure.</span><span class="sxs-lookup"><span data-stu-id="ff55d-117">However, because all DNS resources are global, not regional, hello choice of resource group location has no impact on Azure DNS.</span></span>

<span data-ttu-id="ff55d-118">Puede omitir este paso si utiliza un grupo de recursos existente.</span><span class="sxs-lookup"><span data-stu-id="ff55d-118">You can skip this step if you are using an existing resource group.</span></span>

```powershell
New-AzureRmResourceGroup -Name MyAzureResourceGroup -location "West US"
```

### <a name="register-resource-provider"></a><span data-ttu-id="ff55d-119">Registro del proveedor de recursos</span><span class="sxs-lookup"><span data-stu-id="ff55d-119">Register resource provider</span></span>

<span data-ttu-id="ff55d-120">Hola servicio DNS de Azure se administra mediante el proveedor de recursos de Microsoft.Network Hola.</span><span class="sxs-lookup"><span data-stu-id="ff55d-120">hello Azure DNS service is managed by hello Microsoft.Network resource provider.</span></span> <span data-ttu-id="ff55d-121">Su suscripción de Azure debe estar registrado toouse este proveedor de recursos antes de que se puede usar DNS de Azure.</span><span class="sxs-lookup"><span data-stu-id="ff55d-121">Your Azure subscription must be registered toouse this resource provider before you can use Azure DNS.</span></span> <span data-ttu-id="ff55d-122">Se trata de una operación única para cada suscripción.</span><span class="sxs-lookup"><span data-stu-id="ff55d-122">This is a one-time operation for each subscription.</span></span>

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Network
```