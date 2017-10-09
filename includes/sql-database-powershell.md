
## <a name="start-your-powershell-session"></a>Inicio de una sesión de PowerShell
En primer lugar, debe haber Hola más reciente de Azure PowerShell instalado y en ejecución. Para obtener información detallada, vea [cómo tooinstall y configurar Azure PowerShell](/powershell/azureps-cmdlets-docs).

> [!NOTE]
> Muchas características nuevas de la base de datos SQL solo se admiten cuando se usa hello [modelo de implementación de Azure Resource Manager](../articles/azure-resource-manager/resource-group-overview.md), por lo que los ejemplos utilizan hello [cmdlets de PowerShell de base de datos de SQL Azure](https://msdn.microsoft.com/library/azure/mt574084\(v=azure.300\).aspx) para el Administrador de recursos . modelo de implementación de administración (clásico) de servicio de Hello [cmdlets de administración de servicios de base de datos de SQL Azure](https://msdn.microsoft.com/library/azure/dn546723\(v=azure.300\).aspx) se admiten por compatibilidad con versiones anteriores, pero se recomienda usar Hola cmdlets del Administrador de recursos.
> 
> 

Ejecute hello [ **agregar AzureRmAccount** ](https://msdn.microsoft.com/library/azure/mt619267\(v=azure.300\).aspx) cmdlet y aparecerá una pantalla de inicio de sesión tooenter sus credenciales. Use Hola mismo credenciales que use toosign en toohello portal de Azure.

```PowerShell
Add-AzureRmAccount
```

Si tiene varias suscripciones, use hello [ **conjunto AzureRmContext** ](https://msdn.microsoft.com/library/azure/mt619263\(v=azure.300\).aspx) tooselect cmdlet qué suscripción se debe usar la sesión de PowerShell. toosee qué suscripción Hola PowerShell actual está usando la sesión, ejecute [ **Get AzureRmContext**](https://msdn.microsoft.com/library/azure/mt619265\(v=azure.300\).aspx). ejecutar todas las suscripciones de toosee [ **Get AzureRmSubscription**](https://msdn.microsoft.com/library/azure/mt619284\(v=azure.300\).aspx).

```PowerShell
Set-AzureRmContext -SubscriptionId '4cac86b0-1e56-bbbb-aaaa-000000000000'
```
