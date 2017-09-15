## <a name="set-up-azure-powershell-for-azure-dns"></a><span data-ttu-id="7d8f7-101">Configuración de Azure PowerShell para Azure DNS</span><span class="sxs-lookup"><span data-stu-id="7d8f7-101">Set up Azure PowerShell for Azure DNS</span></span>

### <a name="before-you-begin"></a><span data-ttu-id="7d8f7-102">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="7d8f7-102">Before you begin</span></span>

<span data-ttu-id="7d8f7-103">Antes de comenzar con la configuración, compruebe que dispone de los elementos siguientes.</span><span class="sxs-lookup"><span data-stu-id="7d8f7-103">Verify that you have the following items before beginning your configuration.</span></span>

* <span data-ttu-id="7d8f7-104">Una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="7d8f7-104">An Azure subscription.</span></span> <span data-ttu-id="7d8f7-105">Si todavía no la tiene, puede activar sus [ventajas como suscriptor de MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) o registrarse para obtener una [cuenta gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7d8f7-105">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="7d8f7-106">Necesitará instalar la versión más reciente de los cmdlets de PowerShell de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="7d8f7-106">You need to install the latest version of the Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="7d8f7-107">Para más información, vea [Instalación y configuración de Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="7d8f7-107">For more information, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span>

### <a name="sign-in-to-your-azure-account"></a><span data-ttu-id="7d8f7-108">Inicio de sesión en la cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="7d8f7-108">Sign in to your Azure account</span></span>

<span data-ttu-id="7d8f7-109">Abre la consola de PowerShell y conéctate a tu cuenta.</span><span class="sxs-lookup"><span data-stu-id="7d8f7-109">Open your PowerShell console and connect to your account.</span></span> <span data-ttu-id="7d8f7-110">Para más información, consulte [Uso de PowerShell con Resource Manager](../articles/azure-resource-manager/powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="7d8f7-110">For more information, see [Using PowerShell with Resource Manager](../articles/azure-resource-manager/powershell-azure-resource-manager.md).</span></span>

```powershell
Login-AzureRmAccount
```

### <a name="select-the-subscription"></a><span data-ttu-id="7d8f7-111">Selección de la suscripción</span><span class="sxs-lookup"><span data-stu-id="7d8f7-111">Select the subscription</span></span>
 
<span data-ttu-id="7d8f7-112">Compruebe las suscripciones para la cuenta.</span><span class="sxs-lookup"><span data-stu-id="7d8f7-112">Check the subscriptions for the account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="7d8f7-113">Elección de la suscripción de Azure que se va a usar.</span><span class="sxs-lookup"><span data-stu-id="7d8f7-113">Choose which of your Azure subscriptions to use.</span></span>

```powershell
Select-AzureRmSubscription -SubscriptionName "your_subscription_name"
```

### <a name="create-a-resource-group"></a><span data-ttu-id="7d8f7-114">Crear un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="7d8f7-114">Create a resource group</span></span>

<span data-ttu-id="7d8f7-115">El Administrador de recursos de Azure requiere que todos los grupos de recursos especifiquen una ubicación.</span><span class="sxs-lookup"><span data-stu-id="7d8f7-115">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="7d8f7-116">Esta ubicación se utiliza como ubicación predeterminada para los recursos de ese grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="7d8f7-116">This location is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="7d8f7-117">Sin embargo, puesto que todos los recursos DNS son globales y no regionales, la elección de la ubicación del grupo de recursos no incide en DNS de Azure.</span><span class="sxs-lookup"><span data-stu-id="7d8f7-117">However, because all DNS resources are global, not regional, the choice of resource group location has no impact on Azure DNS.</span></span>

<span data-ttu-id="7d8f7-118">Puede omitir este paso si utiliza un grupo de recursos existente.</span><span class="sxs-lookup"><span data-stu-id="7d8f7-118">You can skip this step if you are using an existing resource group.</span></span>

```powershell
New-AzureRmResourceGroup -Name MyAzureResourceGroup -location "West US"
```

### <a name="register-resource-provider"></a><span data-ttu-id="7d8f7-119">Registro del proveedor de recursos</span><span class="sxs-lookup"><span data-stu-id="7d8f7-119">Register resource provider</span></span>

<span data-ttu-id="7d8f7-120">El proveedor de recursos Microsoft.Network administra el servicio DNS de Azure.</span><span class="sxs-lookup"><span data-stu-id="7d8f7-120">The Azure DNS service is managed by the Microsoft.Network resource provider.</span></span> <span data-ttu-id="7d8f7-121">La suscripción a Azure debe estar registrada para usar este proveedor de recursos antes de utilizar Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="7d8f7-121">Your Azure subscription must be registered to use this resource provider before you can use Azure DNS.</span></span> <span data-ttu-id="7d8f7-122">Se trata de una operación única para cada suscripción.</span><span class="sxs-lookup"><span data-stu-id="7d8f7-122">This is a one-time operation for each subscription.</span></span>

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Network
```