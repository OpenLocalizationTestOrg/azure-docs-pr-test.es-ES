
## <a name="start-your-powershell-session"></a>Inicio de una sesión de PowerShell
En primer lugar debe toohave hello más reciente [Azure PowerShell](http://msdn.microsoft.com/library/mt619274.aspx) instalado y en ejecución. Para obtener información detallada, vea [cómo tooinstall y configurar Azure PowerShell](/powershell/azureps-cmdlets-docs).

> [!NOTE]
> Hola ejemplos de este tema usan [modelo de implementación de Azure Resource Manager](../articles/azure-resource-manager/resource-group-overview.md), por lo que los ejemplos utilizan hello [cmdlets de Azure Resource Manager](http://msdn.microsoft.com/library/azure/mt125356.aspx). 
> 
> 

Ejecute hello [ **agregar AzureRmAccount** ](http://msdn.microsoft.com/library/mt619267.aspx) cmdlet y se le presentará un inicio de sesión en la pantalla tooenter sus credenciales. Use Hola mismo credenciales que use toosign en toohello portal de Azure.

    Add-AzureRmAccount

Si tiene varias suscripciones usar hello [ **conjunto AzureRmContext** ](http://msdn.microsoft.com/library/mt619263.aspx) tooselect cmdlet qué suscripción se debe usar la sesión de PowerShell. toosee qué suscripción Hola PowerShell actual está usando la sesión, ejecute [ **Get AzureRmContext**](http://msdn.microsoft.com/library/mt619265.aspx). ejecutar todas las suscripciones de toosee [ **Get AzureRmSubscription**](http://msdn.microsoft.com/library/mt619284.aspx).

    Set-AzureRmContext -SubscriptionId '4cac86b0-1e56-bbbb-aaaa-000000000000'

