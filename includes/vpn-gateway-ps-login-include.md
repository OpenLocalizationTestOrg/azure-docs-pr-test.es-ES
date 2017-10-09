Antes de comenzar esta configuración, primero debe iniciar sesión en tooyour cuenta de Azure. Hola cmdlet le pide las credenciales de inicio de sesión de Hola para su cuenta de Azure. Después de iniciar sesión, descarga la configuración de la cuenta para que estén disponible tooAzure PowerShell. Para obtener más información, consulte [Uso de Windows PowerShell con el Administrador de recursos](../articles/powershell-azure-resource-manager.md).

toolog en, abra la consola de PowerShell con privilegios elevados y conectar con cuenta de tooyour. Usar hello después toohelp de ejemplo que se conecta:

```powershell
Login-AzureRmAccount
```

Si tiene varias suscripciones de Azure, compruebe las suscripciones de hello para la cuenta de hello.

```powershell
Get-AzureRmSubscription
```

Especifique que desea toouse de suscripción de Hola.

```powershell
Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"
 ```