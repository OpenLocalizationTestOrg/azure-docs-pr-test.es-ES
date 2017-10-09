<span data-ttu-id="7bf32-101">Crear un plan de servicio de aplicaciones con hello [Crear plan de servicio de aplicaciones az](/cli/azure/appservice/plan#create) comando.</span><span class="sxs-lookup"><span data-stu-id="7bf32-101">Create an App Service plan with hello [az appservice plan create](/cli/azure/appservice/plan#create) command.</span></span>

[!INCLUDE [app-service-plan](app-service-plan.md)]

<span data-ttu-id="7bf32-102">Hello en el ejemplo siguiente se crea un plan de servicio de aplicaciones denominado `myAppServicePlan` en hello **libre** nivel de precios:</span><span class="sxs-lookup"><span data-stu-id="7bf32-102">hello following example creates an App Service plan named `myAppServicePlan` in hello **Free** pricing tier:</span></span>

```azurecli-interactive
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku FREE
```

<span data-ttu-id="7bf32-103">Cuando se ha creado el plan de servicio de aplicación Hola, Hola CLI de Azure muestra información toohello similar siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="7bf32-103">When hello App Service plan has been created, hello Azure CLI shows information similar toohello following example:</span></span>

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