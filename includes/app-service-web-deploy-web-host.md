### <a name="app-service-plan"></a>Plan de App Service
Crea el plan de servicio de Hola para hospedar la aplicación web de hello. Proporcionar nombre hello del plan de Hola a través de hello **hostingPlanName** parámetro. ubicación de Hello del plan de hello es Hola misma ubicación que se usa para el grupo de recursos de Hola. tamaño de capa y de trabajo de precios Hola se especifican en hello **sku** y **workerSize** parámetros

    {
      "apiVersion": "2015-08-01",
      "name": "[parameters('hostingPlanName')]",
      "type": "Microsoft.Web/serverfarms",
      "location": "[resourceGroup().location]",
      "sku": {
        "name": "[parameters('sku')]",
        "capacity": "[parameters('workerSize')]"
      },
      "properties": {
        "name": "[parameters('hostingPlanName')]"
      }
    },

