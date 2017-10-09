## <a name="setting-up-powershell-for-resource-manager-templates"></a><span data-ttu-id="631ff-101">Configuración de PowerShell para plantillas del Administrador de recursos</span><span class="sxs-lookup"><span data-stu-id="631ff-101">Setting up PowerShell for Resource Manager templates</span></span>
<span data-ttu-id="631ff-102">Para poder usar Azure PowerShell con el Administrador de recursos, deberá toohave Hola Windows PowerShell y PowerShell de Azure versiones adecuadas.</span><span class="sxs-lookup"><span data-stu-id="631ff-102">Before you can use Azure PowerShell with Resource Manager, you will need toohave hello right Windows PowerShell and Azure PowerShell versions.</span></span>

### <a name="verify-powershell-versions"></a><span data-ttu-id="631ff-103">Comprobar las versiones de PowerShell</span><span class="sxs-lookup"><span data-stu-id="631ff-103">Verify PowerShell versions</span></span>
<span data-ttu-id="631ff-104">Compruebe que tiene Windows PowerShell, versión 3.0 o 4.0.</span><span class="sxs-lookup"><span data-stu-id="631ff-104">Verify you have Windows PowerShell version 3.0 or 4.0.</span></span> <span data-ttu-id="631ff-105">versión de hello toofind de Windows PowerShell, escriba este comando en un símbolo del sistema de Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="631ff-105">toofind hello version of Windows PowerShell, type this command at a Windows PowerShell command prompt.</span></span>

    $PSVersionTable

<span data-ttu-id="631ff-106">Recibirá el mensaje Hola después del tipo de información:</span><span class="sxs-lookup"><span data-stu-id="631ff-106">You will receive hello following type of information:</span></span>

    Name                           Value
    ----                           -----
    PSVersion                      3.0
    WSManStackVersion              3.0
    SerializationVersion           1.1.0.1
    CLRVersion                     4.0.30319.18444
    BuildVersion                   6.2.9200.16481
    PSCompatibleVersions           {1.0, 2.0, 3.0}
    PSRemotingProtocolVersion      2.2


<span data-ttu-id="631ff-107">Compruebe que el valor de hello **PSVersion** es 3.0 o 4.0.</span><span class="sxs-lookup"><span data-stu-id="631ff-107">Verify that hello value of **PSVersion** is 3.0 or 4.0.</span></span> <span data-ttu-id="631ff-108">Si no es así, consulte [Windows Management Framework 3.0](http://www.microsoft.com/download/details.aspx?id=34595) o [Windows Management Framework 4.0](http://www.microsoft.com/download/details.aspx?id=40855).</span><span class="sxs-lookup"><span data-stu-id="631ff-108">If not, see [Windows Management Framework 3.0](http://www.microsoft.com/download/details.aspx?id=34595) or [Windows Management Framework 4.0](http://www.microsoft.com/download/details.aspx?id=40855).</span></span>

### <a name="set-your-azure-account-and-subscription"></a><span data-ttu-id="631ff-109">Definición de su cuenta y suscripción de Azure</span><span class="sxs-lookup"><span data-stu-id="631ff-109">Set your Azure account and subscription</span></span>
<span data-ttu-id="631ff-110">Si todavía no tiene una suscripción de Azure, puede activar sus [beneficios de suscripción a MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) o bien registrarse para obtener una [evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="631ff-110">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

<span data-ttu-id="631ff-111">Abra un símbolo del sistema de PowerShell de Azure y tooAzure con este comando de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="631ff-111">Open an Azure PowerShell command prompt and log on tooAzure with this command.</span></span>

    Login-AzureRmAccount

<span data-ttu-id="631ff-112">Si tiene varias suscripciones de Azure, puede enumerarlas con este comando.</span><span class="sxs-lookup"><span data-stu-id="631ff-112">If you have multiple Azure subscriptions, you can list your Azure subscriptions with this command.</span></span>

    Get-AzureRmSubscription

<span data-ttu-id="631ff-113">Recibirá el mensaje Hola después del tipo de información:</span><span class="sxs-lookup"><span data-stu-id="631ff-113">You will receive hello following type of information:</span></span>

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

<span data-ttu-id="631ff-114">Puede establecer la suscripción actual de Azure Hola ejecutando estos comandos en línea de comandos de PowerShell de Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="631ff-114">You can set hello current Azure subscription by running these commands at hello Azure PowerShell command prompt.</span></span> <span data-ttu-id="631ff-115">Reemplace todo el contenido de las comillas de hello, incluidos Hola < y > caracteres, con el nombre correcto de Hola.</span><span class="sxs-lookup"><span data-stu-id="631ff-115">Replace everything within hello quotes, including hello < and > characters, with hello correct name.</span></span>

    $subscr="<SubscriptionName from hello display of Get-AzureRmSubscription>"
    Select-AzureRmSubscription -SubscriptionName $subscr -Current

<span data-ttu-id="631ff-116">Para obtener más información acerca de las cuentas y suscripciones de Azure, consulte [Cómo: conectar tooyour suscripción](/powershell/azureps-cmdlets-docs#step-3-connect).</span><span class="sxs-lookup"><span data-stu-id="631ff-116">For more information about Azure subscriptions and accounts, see [How to: Connect tooyour subscription](/powershell/azureps-cmdlets-docs#step-3-connect).</span></span>

