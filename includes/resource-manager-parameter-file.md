<span data-ttu-id="fe11f-101">Si usas un valores de parámetro de parámetro archivo toopass durante la implementación, debe toocreate un archivo JSON con un toohello similar formato ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="fe11f-101">If you use a parameter file toopass parameter values during deployment, you need toocreate a JSON file with a format similar toohello following example:</span></span>

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

<span data-ttu-id="fe11f-102">tamaño de Hello del archivo de parámetros de hello no puede ser más de 64 KB.</span><span class="sxs-lookup"><span data-stu-id="fe11f-102">hello size of hello parameter file cannot be more than 64 KB.</span></span>

<span data-ttu-id="fe11f-103">Si necesita tooprovide un valor confidencial para un parámetro (por ejemplo, una contraseña), agregue ese almacén de claves de tooa de valor.</span><span class="sxs-lookup"><span data-stu-id="fe11f-103">If you need tooprovide a sensitive value for a parameter (such as a password), add that value tooa key vault.</span></span> <span data-ttu-id="fe11f-104">Recuperar el almacén de claves de Hola durante la implementación, como se muestra en el ejemplo anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="fe11f-104">Retrieve hello key vault during deployment as shown in hello previous example.</span></span> <span data-ttu-id="fe11f-105">Para más información, consulte [Paso de valores seguros durante la implementación](../articles/azure-resource-manager/resource-manager-keyvault-parameter.md).</span><span class="sxs-lookup"><span data-stu-id="fe11f-105">For more information, see [Pass secure values during deployment](../articles/azure-resource-manager/resource-manager-keyvault-parameter.md).</span></span> 

