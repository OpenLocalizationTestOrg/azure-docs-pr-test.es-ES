
Crear un [aplicación de API](../articles/app-service-api/app-service-api-apps-why-best-platform.md) en hello `myAppServicePlan` plan de servicio de aplicaciones con hello [crear webapp az](/cli/azure/appservice/web#create) comando. 

aplicación web de Hello proporciona un espacio de hospedaje para la API y proporciona una aplicación Hola implementado de tooview de dirección URL.

Hola siguiente comando, reemplace  *\<app_name >* con un nombre único. Si `<app_name>` es no es único, aparece el mensaje de error de Hola "Sitio Web con el nombre especificado < app_name > ya existe". Hola predeterminado es la dirección URL de aplicación web de hello `https://<app_name>.azurewebsites.net`. 

```azurecli-interactive
az webapp create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan
```

Cuando se ha creado la aplicación web de hello, Hola CLI de Azure muestra información toohello similar siguiente ejemplo:

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