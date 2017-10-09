Crear un plan de servicio de aplicaciones con hello [Crear plan de servicio de aplicaciones az](/cli/azure/appservice/plan#create) comando.

[!INCLUDE [app-service-plan](app-service-plan.md)]

Hello en el ejemplo siguiente se crea un plan de servicio de aplicaciones denominado `myAppServicePlan` en hello **libre** nivel de precios:

```azurecli-interactive
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku FREE
```

Cuando se ha creado el plan de servicio de aplicación Hola, Hola CLI de Azure muestra información toohello similar siguiente ejemplo:

```json
{ 
  "adminSiteName": null,
  "appServicePlanName": "myAppServicePlan",
  "geoRegion": "West Europe",
  "hostingEnvironmentProfile": null,
  "id": "/subscriptions/0000-0000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan",
  "kind": "app",
  "location": "West Europe",
  "maximumNumberOfWorkers": 1,
  "name": "myAppServicePlan",
  < JSON data removed for brevity. >
  "targetWorkerSizeId": 0,
  "type": "Microsoft.Web/serverfarms",
  "workerTierName": null
} 
```