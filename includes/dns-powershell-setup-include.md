## <a name="set-up-azure-powershell-for-azure-dns"></a>Configuración de Azure PowerShell para Azure DNS

### <a name="before-you-begin"></a>Antes de empezar

Compruebe que dispone de hello siguientes elementos antes de comenzar la configuración.

* Una suscripción de Azure. Si todavía no la tiene, puede activar sus [ventajas como suscriptor de MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) o registrarse para obtener una [cuenta gratuita](https://azure.microsoft.com/pricing/free-trial/).
* Necesita la versión más reciente de hello tooinstall de hello cmdlets de PowerShell del Administrador de recursos de Azure. Para obtener más información, consulte [cómo tooinstall y configurar Azure PowerShell](/powershell/azureps-cmdlets-docs).

### <a name="sign-in-tooyour-azure-account"></a>Inicie sesión en tooyour cuenta de Azure

Abra la consola de PowerShell y conectar con tooyour cuenta. Para más información, consulte [Uso de PowerShell con Resource Manager](../articles/azure-resource-manager/powershell-azure-resource-manager.md).

```powershell
Login-AzureRmAccount
```

### <a name="select-hello-subscription"></a>Seleccione la suscripción de Hola
 
Compruebe las suscripciones de hello para la cuenta de hello.

```powershell
Get-AzureRmSubscription
```

Elija qué su toouse de las suscripciones de Azure.

```powershell
Select-AzureRmSubscription -SubscriptionName "your_subscription_name"
```

### <a name="create-a-resource-group"></a>Crear un grupo de recursos

Azure Resource Manager requiere que todos los grupos de recursos especifiquen una ubicación. Esta ubicación se utiliza como ubicación predeterminada de Hola para recursos de ese grupo de recursos. Sin embargo, dado que todos los recursos DNS son globales, no regionales, elección de Hola de ubicación del grupo de recursos tiene ningún impacto en el DNS de Azure.

Puede omitir este paso si utiliza un grupo de recursos existente.

```powershell
New-AzureRmResourceGroup -Name MyAzureResourceGroup -location "West US"
```

### <a name="register-resource-provider"></a>Registro del proveedor de recursos

Hola servicio DNS de Azure se administra mediante el proveedor de recursos de Microsoft.Network Hola. Su suscripción de Azure debe estar registrado toouse este proveedor de recursos antes de que se puede usar DNS de Azure. Se trata de una operación única para cada suscripción.

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Network
```