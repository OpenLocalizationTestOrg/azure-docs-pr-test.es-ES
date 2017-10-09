<span data-ttu-id="d6c7e-101">Antes de comenzar esta configuración, primero debe iniciar sesión en tooyour cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="d6c7e-101">Before beginning this configuration, you must log in tooyour Azure account.</span></span> <span data-ttu-id="d6c7e-102">Hola cmdlet le pide las credenciales de inicio de sesión de Hola para su cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="d6c7e-102">hello cmdlet prompts you for hello login credentials for your Azure account.</span></span> <span data-ttu-id="d6c7e-103">Después de iniciar sesión, descarga la configuración de la cuenta para que estén disponible tooAzure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d6c7e-103">After logging in, it downloads your account settings so they are available tooAzure PowerShell.</span></span> <span data-ttu-id="d6c7e-104">Para obtener más información, consulte [Uso de Windows PowerShell con el Administrador de recursos](../articles/powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="d6c7e-104">For more information, see [Using Windows PowerShell with Resource Manager](../articles/powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="d6c7e-105">toolog en, abra la consola de PowerShell con privilegios elevados y conectar con cuenta de tooyour.</span><span class="sxs-lookup"><span data-stu-id="d6c7e-105">toolog in, open your PowerShell console with elevated privileges, and connect tooyour account.</span></span> <span data-ttu-id="d6c7e-106">Usar hello después toohelp de ejemplo que se conecta:</span><span class="sxs-lookup"><span data-stu-id="d6c7e-106">Use hello following example toohelp you connect:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="d6c7e-107">Si tiene varias suscripciones de Azure, compruebe las suscripciones de hello para la cuenta de hello.</span><span class="sxs-lookup"><span data-stu-id="d6c7e-107">If you have multiple Azure subscriptions, check hello subscriptions for hello account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="d6c7e-108">Especifique que desea toouse de suscripción de Hola.</span><span class="sxs-lookup"><span data-stu-id="d6c7e-108">Specify hello subscription that you want toouse.</span></span>

```powershell
Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"
 ```