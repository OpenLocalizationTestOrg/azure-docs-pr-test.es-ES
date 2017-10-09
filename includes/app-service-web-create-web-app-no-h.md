Crear un [aplicación web](../articles/app-service-web/app-service-web-overview.md) en hello `myAppServicePlan` plan de servicio de aplicaciones con hello [crear webapp az](/cli/azure/webapp#create) comando. 

aplicación web de Hello proporciona un espacio de alojamiento para el código y proporciona una aplicación Hola implementado de tooview de dirección URL.

Hola siguiente comando, reemplace  *\<app_name >* con un nombre único (los caracteres válidos son `a-z`, `0-9`, y `-`). Si `<app_name>` es no es único, aparece el mensaje de error de Hola "Sitio Web con el nombre especificado < app_name > ya existe". Hola predeterminado es la dirección URL de aplicación web de hello `https://<app_name>.azurewebsites.net`. 

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

Examinar toohello sitio toosee su aplicación web recién creado.

```bash
http://<app_name>.azurewebsites.net
```
