## <a name="setting-up-powershell-for-resource-manager-templates"></a><span data-ttu-id="e3269-101">Configuración de PowerShell para plantillas del Administrador de recursos</span><span class="sxs-lookup"><span data-stu-id="e3269-101">Setting up PowerShell for Resource Manager templates</span></span>
<span data-ttu-id="e3269-102">Para poder usar Azure PowerShell con el Administrador de recursos, debe tener las versiones adecuadas de Windows PowerShell y PowerShell de Azure.</span><span class="sxs-lookup"><span data-stu-id="e3269-102">Before you can use Azure PowerShell with Resource Manager, you will need to have the right Windows PowerShell and Azure PowerShell versions.</span></span>

### <a name="verify-powershell-versions"></a><span data-ttu-id="e3269-103">Comprobar las versiones de PowerShell</span><span class="sxs-lookup"><span data-stu-id="e3269-103">Verify PowerShell versions</span></span>
<span data-ttu-id="e3269-104">Compruebe que tiene Windows PowerShell, versión 3.0 o 4.0.</span><span class="sxs-lookup"><span data-stu-id="e3269-104">Verify you have Windows PowerShell version 3.0 or 4.0.</span></span> <span data-ttu-id="e3269-105">Para buscar la versión de Windows PowerShell, escriba este comando en un símbolo del sistema de Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e3269-105">To find the version of Windows PowerShell, type this command at a Windows PowerShell command prompt.</span></span>

    $PSVersionTable

<span data-ttu-id="e3269-106">Recibirá el siguiente tipo de información:</span><span class="sxs-lookup"><span data-stu-id="e3269-106">You will receive the following type of information:</span></span>

    Name                           Value
    ----                           -----
    PSVersion                      3.0
    WSManStackVersion              3.0
    SerializationVersion           1.1.0.1
    CLRVersion                     4.0.30319.18444
    BuildVersion                   6.2.9200.16481
    PSCompatibleVersions           {1.0, 2.0, 3.0}
    PSRemotingProtocolVersion      2.2


<span data-ttu-id="e3269-107">Compruebe que el valor de **PSVersion** es 3.0 o 4.0.</span><span class="sxs-lookup"><span data-stu-id="e3269-107">Verify that the value of **PSVersion** is 3.0 or 4.0.</span></span> <span data-ttu-id="e3269-108">Si no es así, consulte [Windows Management Framework 3.0](http://www.microsoft.com/download/details.aspx?id=34595) o [Windows Management Framework 4.0](http://www.microsoft.com/download/details.aspx?id=40855).</span><span class="sxs-lookup"><span data-stu-id="e3269-108">If not, see [Windows Management Framework 3.0](http://www.microsoft.com/download/details.aspx?id=34595) or [Windows Management Framework 4.0](http://www.microsoft.com/download/details.aspx?id=40855).</span></span>

### <a name="set-your-azure-account-and-subscription"></a><span data-ttu-id="e3269-109">Definición de su cuenta y suscripción de Azure</span><span class="sxs-lookup"><span data-stu-id="e3269-109">Set your Azure account and subscription</span></span>
<span data-ttu-id="e3269-110">Si todavía no tiene una suscripción de Azure, puede activar sus [beneficios de suscripción a MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) o bien registrarse para obtener una [evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e3269-110">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

<span data-ttu-id="e3269-111">Abra un símbolo del sistema de Azure PowerShell e inicie sesión en Azure con este comando.</span><span class="sxs-lookup"><span data-stu-id="e3269-111">Open an Azure PowerShell command prompt and log on to Azure with this command.</span></span>

    Login-AzureRmAccount

<span data-ttu-id="e3269-112">Si tiene varias suscripciones de Azure, puede enumerarlas con este comando.</span><span class="sxs-lookup"><span data-stu-id="e3269-112">If you have multiple Azure subscriptions, you can list your Azure subscriptions with this command.</span></span>

    Get-AzureRmSubscription

<span data-ttu-id="e3269-113">Recibirá el siguiente tipo de información:</span><span class="sxs-lookup"><span data-stu-id="e3269-113">You will receive the following type of information:</span></span>

    SubscriptionId            : fd22919d-eaca-4f2b-841a-e4ac6770g92e
    SubscriptionName          : Visual Studio Ultimate with MSDN
    Environment               : AzureCloud
    SupportedModes            : AzureServiceManagement,AzureResourceManager
    DefaultAccount            : johndoe@contoso.com
    Accounts                  : {johndoe@contoso.com}
    IsDefault                 : True
    IsCurrent                 : True
    CurrentStorageAccountName :
    TenantId                  : 32fa88b4-86f1-419f-93ab-2d7ce016dba7

<span data-ttu-id="e3269-114">Puede establecer la suscripción actual de Azure ejecutando estos comandos en el símbolo del sistema de Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e3269-114">You can set the current Azure subscription by running these commands at the Azure PowerShell command prompt.</span></span> <span data-ttu-id="e3269-115">Reemplace todo el contenido dentro de las comillas, incluidos los caracteres < y >, por los nombres correctos.</span><span class="sxs-lookup"><span data-stu-id="e3269-115">Replace everything within the quotes, including the < and > characters, with the correct name.</span></span>

    $subscr="<SubscriptionName from the display of Get-AzureRmSubscription>"
    Select-AzureRmSubscription -SubscriptionName $subscr -Current

<span data-ttu-id="e3269-116">Para más información acerca de las cuentas y suscripciones de Azure, consulte [Conexión a su suscripción](/powershell/azureps-cmdlets-docs#step-3-connect).</span><span class="sxs-lookup"><span data-stu-id="e3269-116">For more information about Azure subscriptions and accounts, see [How to: Connect to your subscription](/powershell/azureps-cmdlets-docs#step-3-connect).</span></span>

