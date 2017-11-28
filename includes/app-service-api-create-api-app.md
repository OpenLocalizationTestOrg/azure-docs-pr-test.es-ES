
<span data-ttu-id="93c84-101">Crear una [aplicación de API](../articles/app-service-api/app-service-api-apps-why-best-platform.md) en el `myAppServicePlan`plan de App Service con el comando [az webapp create](/cli/azure/appservice/web#create).</span><span class="sxs-lookup"><span data-stu-id="93c84-101">Create a [API app](../articles/app-service-api/app-service-api-apps-why-best-platform.md) in the `myAppServicePlan` App Service plan with the [az webapp create](/cli/azure/appservice/web#create) command.</span></span> 

<span data-ttu-id="93c84-102">La aplicación web ofrece un espacio de hospedaje para la API y proporciona una dirección URL para que pueda ver la aplicación implementada.</span><span class="sxs-lookup"><span data-stu-id="93c84-102">The web app provides a hosting space for your API and provides a URL to view the deployed app.</span></span>

<span data-ttu-id="93c84-103">En el siguiente comando, reemplace  *\<app_name >* por un nombre único.</span><span class="sxs-lookup"><span data-stu-id="93c84-103">In the following command, replace *\<app_name>* with a unique name.</span></span> <span data-ttu-id="93c84-104">Si `<app_name>` no es único, obtendrá el mensaje de error "Ya existe un sitio web con el nombre especificado <app_name>".</span><span class="sxs-lookup"><span data-stu-id="93c84-104">If `<app_name>` is not unique, you get the error message "Website with given name <app_name> already exists."</span></span> <span data-ttu-id="93c84-105">La dirección URL predeterminada de la aplicación web es `https://<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="93c84-105">The default URL of the web app is `https://<app_name>.azurewebsites.net`.</span></span> 

```azurecli-interactive
az webapp create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan
```

<span data-ttu-id="93c84-106">Cuando se ha creado la aplicación web, la CLI de Azure muestra información similar a la del ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="93c84-106">When the web app has been created, the Azure CLI shows information similar to the following example:</span></span>

```json
{
  "availabilityState": "Normal",
  "clientAffinityEnabled": true,
  "clientCertEnabled": false,
  "cloningInfo": null,
  "containerSize": 0,
  "dailyMemoryTimeQuota": 0,
  "defaultHostName": "<app_name>.azurewebsites.net",
  "enabled": true,
  "enabledHostNames": [
    "<app_name>.azurewebsites.net",
    "<app_name>.scm.azurewebsites.net"
  ],
  "gatewaySiteName": null,
  "hostNameSslStates": [
    {
      "hostType": "Standard",
      "name": "<app_name>.azurewebsites.net",
      "sslState": "Disabled",
      "thumbprint": null,
      "toUpdate": null,
      "virtualIp": null
    }
    < JSON data removed for brevity. >
}
```