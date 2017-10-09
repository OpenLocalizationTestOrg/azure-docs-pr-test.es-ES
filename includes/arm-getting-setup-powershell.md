## <a name="setting-up-powershell-for-resource-manager-templates"></a>Configuración de PowerShell para plantillas del Administrador de recursos
Para poder usar Azure PowerShell con el Administrador de recursos, deberá toohave Hola Windows PowerShell y PowerShell de Azure versiones adecuadas.

### <a name="verify-powershell-versions"></a>Comprobar las versiones de PowerShell
Compruebe que tiene Windows PowerShell, versión 3.0 o 4.0. versión de hello toofind de Windows PowerShell, escriba este comando en un símbolo del sistema de Windows PowerShell.

    $PSVersionTable

Recibirá el mensaje Hola después del tipo de información:

    Name                           Value
    ----                           -----
    PSVersion                      3.0
    WSManStackVersion              3.0
    SerializationVersion           1.1.0.1
    CLRVersion                     4.0.30319.18444
    BuildVersion                   6.2.9200.16481
    PSCompatibleVersions           {1.0, 2.0, 3.0}
    PSRemotingProtocolVersion      2.2


Compruebe que el valor de hello **PSVersion** es 3.0 o 4.0. Si no es así, consulte [Windows Management Framework 3.0](http://www.microsoft.com/download/details.aspx?id=34595) o [Windows Management Framework 4.0](http://www.microsoft.com/download/details.aspx?id=40855).

### <a name="set-your-azure-account-and-subscription"></a>Definición de su cuenta y suscripción de Azure
Si todavía no tiene una suscripción de Azure, puede activar sus [beneficios de suscripción a MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) o bien registrarse para obtener una [evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/).

Abra un símbolo del sistema de PowerShell de Azure y tooAzure con este comando de inicio de sesión.

    Login-AzureRmAccount

Si tiene varias suscripciones de Azure, puede enumerarlas con este comando.

    Get-AzureRmSubscription

Recibirá el mensaje Hola después del tipo de información:

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

Puede establecer la suscripción actual de Azure Hola ejecutando estos comandos en línea de comandos de PowerShell de Azure Hola. Reemplace todo el contenido de las comillas de hello, incluidos Hola < y > caracteres, con el nombre correcto de Hola.

    $subscr="<SubscriptionName from hello display of Get-AzureRmSubscription>"
    Select-AzureRmSubscription -SubscriptionName $subscr -Current

Para obtener más información acerca de las cuentas y suscripciones de Azure, consulte [Cómo: conectar tooyour suscripción](/powershell/azureps-cmdlets-docs#step-3-connect).

