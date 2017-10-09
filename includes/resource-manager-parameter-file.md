Si usas un valores de parámetro de parámetro archivo toopass durante la implementación, debe toocreate un archivo JSON con un toohello similar formato ejemplo siguiente:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "webSiteName": {
            "value": "ExampleSite"
        },
        "webSiteHostingPlanName": {
            "value": "DefaultPlan"
        },
        "webSiteLocation": {
            "value": "West US"
        },
        "adminPassword": {
            "reference": {
               "keyVault": {
                  "id": "/subscriptions/{guid}/resourceGroups/{group-name}/providers/Microsoft.KeyVault/vaults/{vault-name}"
               }, 
               "secretName": "sqlAdminPassword" 
            }   
        }
   }
}
```

tamaño de Hello del archivo de parámetros de hello no puede ser más de 64 KB.

Si necesita tooprovide un valor confidencial para un parámetro (por ejemplo, una contraseña), agregue ese almacén de claves de tooa de valor. Recuperar el almacén de claves de Hola durante la implementación, como se muestra en el ejemplo anterior de Hola. Para más información, consulte [Paso de valores seguros durante la implementación](../articles/azure-resource-manager/resource-manager-keyvault-parameter.md). 

