### <a name="app-service-plan"></a><span data-ttu-id="62a5b-101">Plan de App Service</span><span class="sxs-lookup"><span data-stu-id="62a5b-101">App Service plan</span></span>
<span data-ttu-id="62a5b-102">Crea el plan de servicio de Hola para hospedar la aplicación web de hello.</span><span class="sxs-lookup"><span data-stu-id="62a5b-102">Creates hello service plan for hosting hello web app.</span></span> <span data-ttu-id="62a5b-103">Proporcionar nombre hello del plan de Hola a través de hello **hostingPlanName** parámetro.</span><span class="sxs-lookup"><span data-stu-id="62a5b-103">You provide hello name of hello plan through hello **hostingPlanName** parameter.</span></span> <span data-ttu-id="62a5b-104">ubicación de Hello del plan de hello es Hola misma ubicación que se usa para el grupo de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="62a5b-104">hello location of hello plan is hello same location used for hello resource group.</span></span> <span data-ttu-id="62a5b-105">tamaño de capa y de trabajo de precios Hola se especifican en hello **sku** y **workerSize** parámetros</span><span class="sxs-lookup"><span data-stu-id="62a5b-105">hello pricing tier and worker size are specified in hello **sku** and **workerSize** parameters</span></span>

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

