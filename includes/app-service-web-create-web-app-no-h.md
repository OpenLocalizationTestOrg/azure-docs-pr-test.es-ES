<span data-ttu-id="e0b0c-101">Crear un [aplicación web](../articles/app-service-web/app-service-web-overview.md) en hello `myAppServicePlan` plan de servicio de aplicaciones con hello [crear webapp az](/cli/azure/webapp#create) comando.</span><span class="sxs-lookup"><span data-stu-id="e0b0c-101">Create a [web app](../articles/app-service-web/app-service-web-overview.md) in hello `myAppServicePlan` App Service plan with hello [az webapp create](/cli/azure/webapp#create) command.</span></span> 

<span data-ttu-id="e0b0c-102">aplicación web de Hello proporciona un espacio de alojamiento para el código y proporciona una aplicación Hola implementado de tooview de dirección URL.</span><span class="sxs-lookup"><span data-stu-id="e0b0c-102">hello web app provides a hosting space for your code and provides a URL tooview hello deployed app.</span></span>

<span data-ttu-id="e0b0c-103">Hola siguiente comando, reemplace  *\<app_name >* con un nombre único (los caracteres válidos son `a-z`, `0-9`, y `-`).</span><span class="sxs-lookup"><span data-stu-id="e0b0c-103">In hello following command, replace *\<app_name>* with a unique name (valid characters are `a-z`, `0-9`, and `-`).</span></span> <span data-ttu-id="e0b0c-104">Si `<app_name>` es no es único, aparece el mensaje de error de Hola "Sitio Web con el nombre especificado < app_name > ya existe".</span><span class="sxs-lookup"><span data-stu-id="e0b0c-104">If `<app_name>` is not unique, you get hello error message "Website with given name <app_name> already exists."</span></span> <span data-ttu-id="e0b0c-105">Hola predeterminado es la dirección URL de aplicación web de hello `https://<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="e0b0c-105">hello default URL of hello web app is `https://<app_name>.azurewebsites.net`.</span></span> 

```azurecli-interactive
az webapp create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan
```

<span data-ttu-id="e0b0c-106">Cuando se ha creado la aplicación web de hello, Hola CLI de Azure muestra información toohello similar siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="e0b0c-106">When hello web app has been created, hello Azure CLI shows information similar toohello following example:</span></span>

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

<span data-ttu-id="e0b0c-107">Examinar toohello sitio toosee su aplicación web recién creado.</span><span class="sxs-lookup"><span data-stu-id="e0b0c-107">Browse toohello site toosee your newly created web app.</span></span>

```bash
http://<app_name>.azurewebsites.net
```
