---
title: "Preguntas más frecuentes de IoT Suite aaaAzure | Documentos de Microsoft"
description: "Preguntas más frecuentes sobre el Conjunto de aplicaciones de IoT"
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: cb537749-a8a1-4e53-b3bf-f1b64a38188a
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: corywink
ms.openlocfilehash: cb39e24af6d1ce2afea554285512d05b2d7c721e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-for-iot-suite"></a><span data-ttu-id="d4c7f-103">Preguntas más frecuentes sobre el Conjunto de aplicaciones de IoT</span><span class="sxs-lookup"><span data-stu-id="d4c7f-103">Frequently asked questions for IoT Suite</span></span>

<span data-ttu-id="d4c7f-104">Vea también, Hola generador conectados específicos [preguntas más frecuentes sobre](iot-suite-faq-cf.md).</span><span class="sxs-lookup"><span data-stu-id="d4c7f-104">See also, hello connected factory specific [FAQ](iot-suite-faq-cf.md).</span></span>

### <a name="where-can-i-find-hello-source-code-for-hello-preconfigured-solutions"></a><span data-ttu-id="d4c7f-105">¿Dónde puedo encontrar el código fuente de Hola para soluciones de hello preconfigurado?</span><span class="sxs-lookup"><span data-stu-id="d4c7f-105">Where can I find hello source code for hello preconfigured solutions?</span></span>

<span data-ttu-id="d4c7f-106">código fuente de Hola se almacena en hello después de repositorios de GitHub:</span><span class="sxs-lookup"><span data-stu-id="d4c7f-106">hello source code is stored in hello following GitHub repositories:</span></span>
* <span data-ttu-id="d4c7f-107">[Solución preconfigurada de supervisión remota][lnk-remote-monitoring-github]</span><span class="sxs-lookup"><span data-stu-id="d4c7f-107">[Remote monitoring preconfigured solution][lnk-remote-monitoring-github]</span></span>
* <span data-ttu-id="d4c7f-108">[Solución preconfigurada de mantenimiento predictivo][lnk-predictive-maintenance-github]</span><span class="sxs-lookup"><span data-stu-id="d4c7f-108">[Predictive maintenance preconfigured solution][lnk-predictive-maintenance-github]</span></span>
* [<span data-ttu-id="d4c7f-109">Solución preconfigurada de fábrica conectada</span><span class="sxs-lookup"><span data-stu-id="d4c7f-109">Connected factory preconfigured solution</span></span>](https://github.com/Azure/azure-iot-connected-factory)

### <a name="how-do-i-update-toohello-latest-version-of-hello-remote-monitoring-preconfigured-solution-that-uses-hello-iot-hub-device-management-features"></a><span data-ttu-id="d4c7f-110">¿Cómo puedo actualizar toohello versión más reciente de la solución preconfigurada supervisión remota Hola que usa Hola características de administración de dispositivos de centro de IoT?</span><span class="sxs-lookup"><span data-stu-id="d4c7f-110">How do I update toohello latest version of hello remote monitoring preconfigured solution that uses hello IoT Hub device management features?</span></span>

* <span data-ttu-id="d4c7f-111">Si implementa una solución preconfigurada de sitio de https://www.azureiotsuite.com/ hello, siempre se implementa una nueva instancia de la versión más reciente de Hola de solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="d4c7f-111">If you deploy a preconfigured solution from hello https://www.azureiotsuite.com/ site, it always deploys a new instance of hello latest version of hello solution.</span></span>
* <span data-ttu-id="d4c7f-112">Si implementa una solución preconfigurada con línea de comandos de hello, puede actualizar una implementación existente con el nuevo código.</span><span class="sxs-lookup"><span data-stu-id="d4c7f-112">If you deploy a preconfigured solution using hello command line, you can update an existing deployment with new code.</span></span> <span data-ttu-id="d4c7f-113">Vea [implementación de nube] [ lnk-cloud-deployment] en hello GitHub [repositorio][lnk-remote-monitoring-github].</span><span class="sxs-lookup"><span data-stu-id="d4c7f-113">See [Cloud deployment][lnk-cloud-deployment] in hello GitHub [repository][lnk-remote-monitoring-github].</span></span>

### <a name="how-can-i-add-support-for-a-new-device-method-toohello-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="d4c7f-114">¿Cómo se puede agregar compatibilidad para un nuevo dispositivo método toohello solución preconfigurada de supervisión remota?</span><span class="sxs-lookup"><span data-stu-id="d4c7f-114">How can I add support for a new device method toohello remote monitoring preconfigured solution?</span></span>

<span data-ttu-id="d4c7f-115">Consulte la sección de hello [agregar compatibilidad con un simulador de toohello método nuevo] [ lnk-add-method] en hello [personalizar una solución preconfigurada] [ lnk-customize] artículo.</span><span class="sxs-lookup"><span data-stu-id="d4c7f-115">See hello section [Add support for a new method toohello simulator][lnk-add-method] in hello [Customize a preconfigured solution][lnk-customize] article.</span></span>

### <a name="hello-simulated-device-is-ignoring-my-desired-property-changes-why"></a><span data-ttu-id="d4c7f-116">dispositivo simulado Hola está omitiendo los cambios de la propiedad deseada, ¿por qué?</span><span class="sxs-lookup"><span data-stu-id="d4c7f-116">hello simulated device is ignoring my desired property changes, why?</span></span>
<span data-ttu-id="d4c7f-117">Hola supervisión remota preconfigurado soluciones, código de hello simulada del dispositivo solo usa hello **Desired.Config.TemperatureMeanValue** y **Desired.Config.TelemetryInterval** las propiedades adecuadas Hola tooupdate informó de propiedades.</span><span class="sxs-lookup"><span data-stu-id="d4c7f-117">In hello remote monitoring preconfigured solution, hello simulated device code only uses hello **Desired.Config.TemperatureMeanValue** and **Desired.Config.TelemetryInterval** desired properties tooupdate hello reported properties.</span></span> <span data-ttu-id="d4c7f-118">Todos los demás cambios de propiedades deseadas se omiten.</span><span class="sxs-lookup"><span data-stu-id="d4c7f-118">All other desired property change requests are ignored.</span></span>

### <a name="my-device-does-not-appear-in-hello-list-of-devices-in-hello-solution-dashboard-why"></a><span data-ttu-id="d4c7f-119">El dispositivo no aparece en la lista de Hola de dispositivos en el panel de la solución de hello, ¿por qué?</span><span class="sxs-lookup"><span data-stu-id="d4c7f-119">My device does not appear in hello list of devices in hello solution dashboard, why?</span></span>

<span data-ttu-id="d4c7f-120">lista de Hola de dispositivos en el panel de la solución de hello utiliza una lista de Hola de tooreturn de consulta de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="d4c7f-120">hello list of devices in hello solution dashboard uses a query tooreturn hello list of devices.</span></span> <span data-ttu-id="d4c7f-121">Actualmente, una consulta no puede devolver más de 10 000 dispositivos.</span><span class="sxs-lookup"><span data-stu-id="d4c7f-121">Currently, a query cannot return more than 10K devices.</span></span> <span data-ttu-id="d4c7f-122">Intente realizar los criterios de búsqueda de hello para la consulta más restrictiva.</span><span class="sxs-lookup"><span data-stu-id="d4c7f-122">Try making hello search criteria for your query more restrictive.</span></span>

### <a name="whats-hello-difference-between-deleting-a-resource-group-in-hello-azure-portal-and-clicking-delete-on-a-preconfigured-solution-in-azureiotsuitecom"></a><span data-ttu-id="d4c7f-123">¿Cuál es la diferencia de hello entre eliminar un grupo de recursos en hello Azure portal y haga clic en Eliminar en una solución preconfigurada en azureiotsuite.com?</span><span class="sxs-lookup"><span data-stu-id="d4c7f-123">What's hello difference between deleting a resource group in hello Azure portal and clicking delete on a preconfigured solution in azureiotsuite.com?</span></span>

* <span data-ttu-id="d4c7f-124">Si elimina la solución de hello preconfigurado en [azureiotsuite.com][lnk-azureiotsuite], eliminar todos los recursos de hello aprovisionados al crear soluciones de hello preconfigurado.</span><span class="sxs-lookup"><span data-stu-id="d4c7f-124">If you delete hello preconfigured solution in [azureiotsuite.com][lnk-azureiotsuite], you delete all hello resources that were provisioned when you created hello preconfigured solution.</span></span> <span data-ttu-id="d4c7f-125">Si ha agregado el grupo de recursos de toohello de recursos adicionales, también se eliminan estos recursos.</span><span class="sxs-lookup"><span data-stu-id="d4c7f-125">If you added additional resources toohello resource group, these resources are also deleted.</span></span> 
* <span data-ttu-id="d4c7f-126">Si elimina el grupo de recursos de Hola Hola [portal de Azure][lnk-azure-portal], sólo se eliminar recursos de hello en ese grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="d4c7f-126">If you delete hello resource group in hello [Azure portal][lnk-azure-portal], you only delete hello resources in that resource group.</span></span> <span data-ttu-id="d4c7f-127">También necesita toodelete aplicación de Azure Active Directory hello asociado a soluciones de hello preconfigurado en hello [portal de Azure clásico][lnk-classic-portal].</span><span class="sxs-lookup"><span data-stu-id="d4c7f-127">You also need toodelete hello Azure Active Directory application associated with hello preconfigured solution in hello [Azure classic portal][lnk-classic-portal].</span></span>

### <a name="how-many-iot-hub-instances-can-i-provision-in-a-subscription"></a><span data-ttu-id="d4c7f-128">¿Cuántas instancias del Centro de IoT se pueden aprovisionar en una suscripción?</span><span class="sxs-lookup"><span data-stu-id="d4c7f-128">How many IoT Hub instances can I provision in a subscription?</span></span>

<span data-ttu-id="d4c7f-129">De forma predeterminada, puede aprovisionar [10 centros de IoT Hub por suscripción][link-azuresublimits].</span><span class="sxs-lookup"><span data-stu-id="d4c7f-129">By default you can provision [10 IoT hubs per subscription][link-azuresublimits].</span></span> <span data-ttu-id="d4c7f-130">Puede crear un [incidencia de soporte técnico de Azure] [ link-azuresupportticket] tooraise este límite.</span><span class="sxs-lookup"><span data-stu-id="d4c7f-130">You can create an [Azure support ticket][link-azuresupportticket] tooraise this limit.</span></span> <span data-ttu-id="d4c7f-131">Como resultado, desde cada disposiciones de solución preconfigurada un nuevo centro de IoT, solo puede aprovisionar una too10 había preconfigurado soluciones en una suscripción determinada.</span><span class="sxs-lookup"><span data-stu-id="d4c7f-131">As a result, since every preconfigured solution provisions a new IoT Hub, you can only provision up too10 preconfigured solutions in a given subscription.</span></span> 

### <a name="how-many-azure-cosmos-db-instances-can-i-provision-in-a-subscription"></a><span data-ttu-id="d4c7f-132">¿Cuántas instancias de Azure Cosmos DB se pueden aprovisionar en una suscripción?</span><span class="sxs-lookup"><span data-stu-id="d4c7f-132">How many Azure Cosmos DB instances can I provision in a subscription?</span></span>

<span data-ttu-id="d4c7f-133">Cincuenta.</span><span class="sxs-lookup"><span data-stu-id="d4c7f-133">Fifty.</span></span> <span data-ttu-id="d4c7f-134">Puede crear un [incidencia de soporte técnico de Azure] [ link-azuresupportticket] tooraise Esto limitará, pero de forma predeterminada, solo puede aprovisionar 50 instancias de base de datos de Cosmos por suscripción.</span><span class="sxs-lookup"><span data-stu-id="d4c7f-134">You can create an [Azure support ticket][link-azuresupportticket] tooraise this limit, but by default, you can only provision 50 Cosmos DB instances per subscription.</span></span> 

### <a name="how-many-free-bing-maps-apis-can-i-provision-in-a-subscription"></a><span data-ttu-id="d4c7f-135">¿Cuántas API de Mapas de Bing gratis se pueden aprovisionar en una suscripción?</span><span class="sxs-lookup"><span data-stu-id="d4c7f-135">How many Free Bing Maps APIs can I provision in a subscription?</span></span>

<span data-ttu-id="d4c7f-136">Dos.</span><span class="sxs-lookup"><span data-stu-id="d4c7f-136">Two.</span></span> <span data-ttu-id="d4c7f-137">Solo puede crear dos planes de Mapas de Bing para empresa de nivel 1 de transacciones internas en una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="d4c7f-137">You can create only two Internal Transactions Level 1 Bing Maps for Enterprise plans in an Azure subscription.</span></span> <span data-ttu-id="d4c7f-138">solución de supervisión remota Hola se aprovisiona con plan Hola interno las transacciones de nivel 1 de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="d4c7f-138">hello remote monitoring solution is provisioned by default with hello Internal Transactions Level 1 plan.</span></span> <span data-ttu-id="d4c7f-139">Como resultado, solo puede aprovisionar tootwo remoto de supervisión de soluciones en una suscripción sin modificaciones.</span><span class="sxs-lookup"><span data-stu-id="d4c7f-139">As a result, you can only provision up tootwo remote monitoring solutions in a subscription with no modifications.</span></span>

### <a name="i-have-a-remote-monitoring-solution-deployment-with-a-static-map-how-do-i-add-an-interactive-bing-map"></a><span data-ttu-id="d4c7f-140">Tengo una implementación de soluciones de supervisión remota con un mapa estático, ¿cómo se puede agregar un mapa Bing interactivo?</span><span class="sxs-lookup"><span data-stu-id="d4c7f-140">I have a remote monitoring solution deployment with a static map, how do I add an interactive Bing map?</span></span>

1. <span data-ttu-id="d4c7f-141">Obtenga la QueryKey de Bing Maps API for Enterprise en [Azure Portal][lnk-azure-portal]:</span><span class="sxs-lookup"><span data-stu-id="d4c7f-141">Get your Bing Maps API for Enterprise QueryKey from [Azure portal][lnk-azure-portal]:</span></span> 
   
   1. <span data-ttu-id="d4c7f-142">Navegue toohello grupo de recursos donde es la API de Bing Maps para Enterprise en hello [portal de Azure][lnk-azure-portal].</span><span class="sxs-lookup"><span data-stu-id="d4c7f-142">Navigate toohello Resource Group where your Bing Maps API for Enterprise is in hello [Azure portal][lnk-azure-portal].</span></span>
   2. <span data-ttu-id="d4c7f-143">Haga clic en **Toda la configuración** y después en **Administración de claves**.</span><span class="sxs-lookup"><span data-stu-id="d4c7f-143">Click **All Settings**, then **Key Management**.</span></span> 
   3. <span data-ttu-id="d4c7f-144">Verá dos claves: **MasterKey** y **QueryKey**.</span><span class="sxs-lookup"><span data-stu-id="d4c7f-144">You can see two keys: **MasterKey** and **QueryKey**.</span></span> <span data-ttu-id="d4c7f-145">Copiar valor de Hola para **QueryKey**.</span><span class="sxs-lookup"><span data-stu-id="d4c7f-145">Copy hello value for **QueryKey**.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="d4c7f-146">¿No tiene una cuenta de la API de Mapas de Bing para empresa?</span><span class="sxs-lookup"><span data-stu-id="d4c7f-146">Don't have a Bing Maps API for Enterprise account?</span></span> <span data-ttu-id="d4c7f-147">Crear uno en hello [portal de Azure] [ lnk-azure-portal] haciendo clic en + nuevo, buscando la API de Bing Maps para Enterprise y seguir solicita toocreate.</span><span class="sxs-lookup"><span data-stu-id="d4c7f-147">Create one in hello [Azure portal][lnk-azure-portal] by clicking + New, searching for Bing Maps API for Enterprise and follow prompts toocreate.</span></span>
      > 
      > 
2. <span data-ttu-id="d4c7f-148">Deslice hacia abajo de código más reciente de Hola de hello [-IoT-remoto-supervisión de Azure][lnk-remote-monitoring-github].</span><span class="sxs-lookup"><span data-stu-id="d4c7f-148">Pull down hello latest code from hello [Azure-IoT-Remote-Monitoring][lnk-remote-monitoring-github].</span></span>
3. <span data-ttu-id="d4c7f-149">Ejecutar a una variable local o implementación Hola instrucciones de implementación de línea de comandos en carpeta de /docs/ de hello en el repositorio de hello en la nube.</span><span class="sxs-lookup"><span data-stu-id="d4c7f-149">Run a local or cloud deployment following hello command-line deployment guidance in hello /docs/ folder in hello repository.</span></span> 
4. <span data-ttu-id="d4c7f-150">Una vez se haya ejecutado una variable local o en la nube implementación, busque en la carpeta raíz para Hola *. archivo user.config creado durante la implementación.</span><span class="sxs-lookup"><span data-stu-id="d4c7f-150">After you've run a local or cloud deployment, look in your root folder for hello *.user.config file created during deployment.</span></span> <span data-ttu-id="d4c7f-151">Abra este archivo en un editor de texto.</span><span class="sxs-lookup"><span data-stu-id="d4c7f-151">Open this file in a text editor.</span></span> 
5. <span data-ttu-id="d4c7f-152">Valor de hello tooinclude copió desde de la línea de siguiente Hola de cambio su **QueryKey**:</span><span class="sxs-lookup"><span data-stu-id="d4c7f-152">Change hello following line tooinclude hello value you copied from your **QueryKey**:</span></span> 
   
   `<setting name="MapApiQueryKey" value="" />`

### <a name="can-i-create-a-preconfigured-solution-if-i-have-microsoft-azure-for-dreamspark"></a><span data-ttu-id="d4c7f-153">¿Puedo crear una solución preconfigurada si tengo Microsoft Azure para DreamSpark?</span><span class="sxs-lookup"><span data-stu-id="d4c7f-153">Can I create a preconfigured solution if I have Microsoft Azure for DreamSpark?</span></span>

<span data-ttu-id="d4c7f-154">En este momento, no se puede crear una solución preconfigurada con una cuenta de [Microsoft Azure para DreamSpark][lnk-dreamspark].</span><span class="sxs-lookup"><span data-stu-id="d4c7f-154">Currently, you cannot create a preconfigured solution with a [Microsoft Azure for DreamSpark][lnk-dreamspark] account.</span></span> <span data-ttu-id="d4c7f-155">Sin embargo, puede crear una [cuenta de evaluación gratuita de Azure][lnk-30daytrial] en un par de minutos, lo que le permite crear una solución preconfigurada.</span><span class="sxs-lookup"><span data-stu-id="d4c7f-155">However, you can create a [free trial account for Azure][lnk-30daytrial] in just a couple of minutes that enables you create a preconfigured solution.</span></span>

### <a name="can-i-create-a-preconfigured-solution-if-i-have-cloud-solution-provider-csp-subscription"></a><span data-ttu-id="d4c7f-156">¿Puedo crear una solución preconfigurada si tengo alguna suscripción del Proveedor de soluciones en la nube (CSP)?</span><span class="sxs-lookup"><span data-stu-id="d4c7f-156">Can I create a preconfigured solution if I have Cloud Solution Provider (CSP) subscription?</span></span>

<span data-ttu-id="d4c7f-157">En este momento, no se puede crear una solución preconfigurada con una suscripción del Proveedor de soluciones en la nube (CSP).</span><span class="sxs-lookup"><span data-stu-id="d4c7f-157">Currently, you cannot create a preconfigured solution with a Cloud Solution Provider (CSP) subscription.</span></span> <span data-ttu-id="d4c7f-158">Sin embargo, puede crear una [cuenta de evaluación gratuita de Azure][lnk-30daytrial] en un par de minutos, lo que le permite crear una solución preconfigurada.</span><span class="sxs-lookup"><span data-stu-id="d4c7f-158">However, you can create a [free trial account for Azure][lnk-30daytrial] in just a couple of minutes that enables you create a preconfigured solution.</span></span>

### <a name="how-do-i-delete-an-aad-tenant"></a><span data-ttu-id="d4c7f-159">¿Cómo se eliminan inquilinos de AAD?</span><span class="sxs-lookup"><span data-stu-id="d4c7f-159">How do I delete an AAD tenant?</span></span>

<span data-ttu-id="d4c7f-160">Consulte la entrada del blog de Eric Golpe [Walkthrough of Deleting an Azure AD Tenant][lnk-delete-aad-tennant] (Tutorial para la eliminación de inquilinos de Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d4c7f-160">See Eric Golpe's blog post [Walkthrough of Deleting an Azure AD Tenant][lnk-delete-aad-tennant].</span></span>

### <a name="next-steps"></a><span data-ttu-id="d4c7f-161">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d4c7f-161">Next steps</span></span>

<span data-ttu-id="d4c7f-162">También puede explorar algunas de hello otras características y capacidades de hello IoT preconfigurado soluciones:</span><span class="sxs-lookup"><span data-stu-id="d4c7f-162">You can also explore some of hello other features and capabilities of hello IoT Suite preconfigured solutions:</span></span>

* <span data-ttu-id="d4c7f-163">[Información general de la solución preconfigurada de mantenimiento predictivo][lnk-predictive-overview]</span><span class="sxs-lookup"><span data-stu-id="d4c7f-163">[Predictive maintenance preconfigured solution overview][lnk-predictive-overview]</span></span>
* [<span data-ttu-id="d4c7f-164">Introducción a la solución preconfigurada de fábrica conectada</span><span class="sxs-lookup"><span data-stu-id="d4c7f-164">Connected factory preconfigured solution overview</span></span>](iot-suite-connected-factory-overview.md)
* <span data-ttu-id="d4c7f-165">[Seguridad de IoT de hello masa][lnk-security-groundup]</span><span class="sxs-lookup"><span data-stu-id="d4c7f-165">[IoT security from hello ground up][lnk-security-groundup]</span></span>

[lnk-predictive-overview]: iot-suite-predictive-overview.md
[lnk-security-groundup]: securing-iot-ground-up.md

[link-azuresupportticket]: https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade 
[link-azuresublimits]: https://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/#iot-hub-limits
[lnk-azure-portal]: https://portal.azure.com
[lnk-azureiotsuite]: https://www.azureiotsuite.com/
[lnk-classic-portal]: https://manage.windowsazure.com
[lnk-remote-monitoring-github]: https://github.com/Azure/azure-iot-remote-monitoring 
[lnk-dreamspark]: https://www.dreamspark.com/Product/Product.aspx?productid=99 
[lnk-30daytrial]: https://azure.microsoft.com/free/
[lnk-delete-aad-tennant]: http://blogs.msdn.com/b/ericgolpe/archive/2015/04/30/walkthrough-of-deleting-an-azure-ad-tenant.aspx
[lnk-cloud-deployment]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/cloud-deployment.md
[lnk-add-method]: iot-suite-guidance-on-customizing-preconfigured-solutions.md#add-support-for-a-new-method-to-the-simulator
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-remote-monitoring-github]: https://github.com/Azure/azure-iot-remote-monitoring
[lnk-predictive-maintenance-github]: https://github.com/Azure/azure-iot-predictive-maintenance
