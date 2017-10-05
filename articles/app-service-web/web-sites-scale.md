---
title: Escalado vertical de aplicaciones en Azure | Microsoft Docs
description: "Aprenda a escalar verticalmente una aplicación del Servicio de aplicaciones de Azure para agregar capacidad y características."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: mollybos
ms.assetid: f7091b25-b2b6-48da-8d4a-dcf9b7baccab
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2016
ms.author: cephalin
ms.openlocfilehash: 75ddbacbd4dd14597b786d26f0730477f6c85811
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="scale-up-an-app-in-azure"></a><span data-ttu-id="a54b6-103">Escalado vertical de aplicaciones en Azure</span><span class="sxs-lookup"><span data-stu-id="a54b6-103">Scale up an app in Azure</span></span>
<span data-ttu-id="a54b6-104">En este artículo se muestra cómo escalar aplicaciones en el Servicio de aplicaciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="a54b6-104">This article shows you how to scale your app in Azure App Service.</span></span> <span data-ttu-id="a54b6-105">Existen dos flujos de trabajo para escalar aplicaciones, el escalado vertical y el escalado horizontal, y en este artículo se explica el flujo de trabajo para escalar verticalmente.</span><span class="sxs-lookup"><span data-stu-id="a54b6-105">There are two workflows for scaling, scale up and scale out, and this article explains the scale up workflow.</span></span>

* <span data-ttu-id="a54b6-106">[Escalado vertical](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): obtenga más CPU, memoria, espacio en disco y características adicionales como máquinas virtuales exclusivas, dominios y certificados personalizados, espacios de ensayo, autoescala y mucho más.</span><span class="sxs-lookup"><span data-stu-id="a54b6-106">[Scale up](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): Get more CPU, memory, disk space, and extra features like dedicated virtual machines (VMs), custom domains and certificates, staging slots, autoscaling, and more.</span></span> <span data-ttu-id="a54b6-107">Para escalar verticalmente, se cambia el plan de tarifa del plan del Servicio de aplicaciones al que pertenece la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a54b6-107">You scale up by changing the pricing tier of the App Service plan that your app belongs to.</span></span>
* <span data-ttu-id="a54b6-108">[Escalado horizontal](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): se aumenta el número de instancias de máquina virtual que ejecutan la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a54b6-108">[Scale out](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): Increase the number of VM instances that run your app.</span></span>
  <span data-ttu-id="a54b6-109">Se puede escalar horizontalmente a un máximo de 20 instancias, según el plan de tarifa.</span><span class="sxs-lookup"><span data-stu-id="a54b6-109">You can scale out to as many as 20 instances, depending on your pricing tier.</span></span> <span data-ttu-id="a54b6-110">[entornos del Servicio de aplicaciones](../app-service/app-service-app-service-environments-readme.md) del nivel **Premium** tier will further del nivelcrease your scale-out count to 50 del nivelstances.</span><span class="sxs-lookup"><span data-stu-id="a54b6-110">[App Service Environments](../app-service/app-service-app-service-environments-readme.md) in **Premium** tier will further increase your scale-out count to 50 instances.</span></span> <span data-ttu-id="a54b6-111">Para más información sobre el escalado horizontal, consulte [Escalado del número de instancias de forma manual o automática](../monitoring-and-diagnostics/insights-how-to-scale.md).</span><span class="sxs-lookup"><span data-stu-id="a54b6-111">For more information about scaling out, see [Scale instance count manually or automatically](../monitoring-and-diagnostics/insights-how-to-scale.md).</span></span> <span data-ttu-id="a54b6-112">En ese artículo aprenderá a utilizar el escalado automático, que consiste en escalar el número de instancias automáticamente en función de las programaciones y reglas predefinidas.</span><span class="sxs-lookup"><span data-stu-id="a54b6-112">There you will find out how to use autoscaling, which is to scale instance count automatically based on predefined rules and schedules.</span></span>

<span data-ttu-id="a54b6-113">La configuración de escalado tarda solo unos segundos en aplicarse y afecta a todas las aplicaciones del [plan del Servicio de aplicaciones](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a54b6-113">The scale settings take only seconds to apply and affect all apps in your [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span>
<span data-ttu-id="a54b6-114">No hay que modificar el código ni volver a implementar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a54b6-114">They do not require you to change your code or redeploy your application.</span></span>

<span data-ttu-id="a54b6-115">Para obtener información de los precios y características de planes del Servicio de aplicaciones individuales, consulte [Precios del Servicio de aplicaciones](https://azure.microsoft.com/pricing/details/web-sites/).</span><span class="sxs-lookup"><span data-stu-id="a54b6-115">For information about the pricing and features of individual App Service plans, see [App Service Pricing Details](https://azure.microsoft.com/pricing/details/web-sites/).</span></span>  

> [!NOTE]
> <span data-ttu-id="a54b6-116">Antes de cambiar un plan del Servicio de aplicaciones con el nivel **Gratis** a uno superior, primero debe quitar los [límites de gasto](https://azure.microsoft.com/pricing/spending-limits/) vigentes de la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="a54b6-116">Before you switch an App Service plan from the **Free** tier, you must first remove the [spending limits](https://azure.microsoft.com/pricing/spending-limits/) in place for your Azure subscription.</span></span> <span data-ttu-id="a54b6-117">Para ver o cambiar opciones para la suscripción a Azure App Service, consulte [Suscripciones a Microsoft Azure][azuresubscriptions].</span><span class="sxs-lookup"><span data-stu-id="a54b6-117">To view or change options for your Microsoft Azure App Service subscription, see [Microsoft Azure Subscriptions][azuresubscriptions].</span></span>
> 
> 

<a name="scalingsharedorbasic"></a>
<a name="scalingstandard"></a>

## <a name="scale-up-your-pricing-tier"></a><span data-ttu-id="a54b6-118">Escalado vertical del plan de tarifa</span><span class="sxs-lookup"><span data-stu-id="a54b6-118">Scale up your pricing tier</span></span>
1. <span data-ttu-id="a54b6-119">En el explorador, abra [Azure Portal][portal].</span><span class="sxs-lookup"><span data-stu-id="a54b6-119">In your browser, open the [Azure portal][portal].</span></span>
2. <span data-ttu-id="a54b6-120">En la hoja de la aplicación, haga clic en **Toda la configuración** y en **Escalar verticalmente**.</span><span class="sxs-lookup"><span data-stu-id="a54b6-120">In your app's blade, click **All settings**, and then click **Scale Up**.</span></span>
   
    ![Desplácese para escalar verticalmente la aplicación de Azure.][ChooseWHP]
3. <span data-ttu-id="a54b6-122">Elija el nivel y, después, haga clic en **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="a54b6-122">Choose your tier, and then click **Select**.</span></span>
   
    <span data-ttu-id="a54b6-123">La pestaña **Notificaciones** emitirá el mensaje **CORRECTO** en color verde indicando que se ha completado con éxito una vez finalizada la operación.</span><span class="sxs-lookup"><span data-stu-id="a54b6-123">The **Notifications** tab will flash a green **SUCCESS** after the operation is complete.</span></span>

<a name="ScalingSQLServer"></a>

## <a name="scale-related-resources"></a><span data-ttu-id="a54b6-124">Recursos relacionados con el escalado</span><span class="sxs-lookup"><span data-stu-id="a54b6-124">Scale related resources</span></span>
<span data-ttu-id="a54b6-125">Si su aplicación depende de otros servicios, como Base de datos SQL o Almacenamiento de Azure, también puede escalar verticalmente estos recursos según sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="a54b6-125">If your app depends on other services, such as Azure SQL Database or Azure Storage, you can also scale up those resources based on your needs.</span></span> <span data-ttu-id="a54b6-126">Debe tener en cuenta que no se escalan con el plan del Servicio de aplicaciones y que esta operación debe realizarse por separado.</span><span class="sxs-lookup"><span data-stu-id="a54b6-126">These resources are not scaled with the App Service plan and must be scaled separately.</span></span>

1. <span data-ttu-id="a54b6-127">En **Essentials**, haga clic en el vínculo **Grupo de recursos**.</span><span class="sxs-lookup"><span data-stu-id="a54b6-127">In **Essentials**, click the **Resource group** link.</span></span>
   
    ![Escalado vertical de recursos relacionados con la aplicación de Azure](./media/web-sites-scale/RGEssentialsLink.png)
2. <span data-ttu-id="a54b6-129">Después, en la parte **Resume**n de la hoja **Grupo de recursos**, haga clic en uno de los recursos que quiera escalar.</span><span class="sxs-lookup"><span data-stu-id="a54b6-129">In the **Summary** part of the **Resource group** blade, click a resource that you want to scale.</span></span> <span data-ttu-id="a54b6-130">En la captura de pantalla siguiente se muestra un recurso de Base de datos SQL y uno de Almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="a54b6-130">The following screenshot shows a SQL Database resource and an Azure Storage resource.</span></span>
   
    ![Desplácese a la hoja del grupo de recursos para escalar verticalmente la aplicación de Azure.](./media/web-sites-scale/ResourceGroup.png)
3. <span data-ttu-id="a54b6-132">Para un recurso de SQL Database, haga clic en **Configuración** > **Nivel de precios** para escalar el plan de tarifa.</span><span class="sxs-lookup"><span data-stu-id="a54b6-132">For a SQL Database resource, click **Settings** > **Pricing tier** to scale the pricing tier.</span></span>
   
    ![Escalado vertical del back-end de Base de datos SQL de la aplicación de Azure](./media/web-sites-scale/ScaleDatabase.png)
   
    <span data-ttu-id="a54b6-134">También puede activar la [replicación geográfica](../sql-database/sql-database-geo-replication-overview.md) de su instancia de Base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="a54b6-134">You can also turn on [geo-replication](../sql-database/sql-database-geo-replication-overview.md) for your SQL Database instance.</span></span>
   
    <span data-ttu-id="a54b6-135">Para un recurso de Azure Storage, haga clic en **Configuración** > **Configuración** para escalar verticalmente las opciones de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="a54b6-135">For an Azure Storage resource, click **Settings** > **Configuration** to scale up your storage options.</span></span>
   
    ![Escalado vertical de la cuenta de Almacenamiento de Azure que utiliza la aplicación de Azure](./media/web-sites-scale/ScaleStorage.png)

<a name="devfeatures"></a>

## <a name="learn-about-developer-features"></a><span data-ttu-id="a54b6-137">Más información sobre las características del desarrollador</span><span class="sxs-lookup"><span data-stu-id="a54b6-137">Learn about developer features</span></span>
<span data-ttu-id="a54b6-138">Según el nivel de precios, se encuentran disponibles las siguientes características orientadas al desarrollador:</span><span class="sxs-lookup"><span data-stu-id="a54b6-138">Depending on the pricing tier, the following developer-oriented features are available:</span></span>

### <a name="bitness"></a><span data-ttu-id="a54b6-139">Valor de bits</span><span class="sxs-lookup"><span data-stu-id="a54b6-139">Bitness</span></span>
* <span data-ttu-id="a54b6-140">Los modos **Básico**, **Estándar** y **Premium** son compatibles con aplicaciones de 32 y 64 bits.</span><span class="sxs-lookup"><span data-stu-id="a54b6-140">The **Basic**, **Standard**, and **Premium** tiers support 64-bit and 32-bit applications.</span></span>
* <span data-ttu-id="a54b6-141">Los niveles de plan **Gratis** y **Compartido** solo son compatibles con aplicaciones de 32 bits.</span><span class="sxs-lookup"><span data-stu-id="a54b6-141">The **Free** and **Shared** plan tiers support 32-bit applications only.</span></span>

### <a name="debugger-support"></a><span data-ttu-id="a54b6-142">Compatibilidad con el depurador</span><span class="sxs-lookup"><span data-stu-id="a54b6-142">Debugger support</span></span>
* <span data-ttu-id="a54b6-143">La compatibilidad con el depurador está disponible para los modos **Gratis**, **Compartido** y **Básico** en una conexión por cada plan de App Services.</span><span class="sxs-lookup"><span data-stu-id="a54b6-143">Debugger support is available for the **Free**, **Shared**, and **Basic** modes at one connection per App Service plan.</span></span>
* <span data-ttu-id="a54b6-144">La compatibilidad con el depurador está disponible para los modos **Estándar** y **Premium** en cinco conexiones simultáneas por cada plan de App Services.</span><span class="sxs-lookup"><span data-stu-id="a54b6-144">Debugger support is available for the **Standard** and **Premium** modes at five concurrent connections per App Service plan.</span></span>

<a name="OtherFeatures"></a>

## <a name="learn-about-other-features"></a><span data-ttu-id="a54b6-145">Más información sobre otras características</span><span class="sxs-lookup"><span data-stu-id="a54b6-145">Learn about other features</span></span>
* <span data-ttu-id="a54b6-146">Para obtener información detallada sobre todas las características restantes en los planes de Servicios de aplicaciones, incluido el precio y las características de interés para todos los usuarios (incluidos los desarrolladores), consulte [Detalles de precios de Servicios de aplicaciones](https://azure.microsoft.com/pricing/details/web-sites/).</span><span class="sxs-lookup"><span data-stu-id="a54b6-146">For detailed information about all of the remaining features in the App Service plans, including pricing and features of interest to all users (including developers), see [App Service Pricing Details](https://azure.microsoft.com/pricing/details/web-sites/).</span></span>

> [!NOTE]
> <span data-ttu-id="a54b6-147">Si desea empezar a trabajar con el Servicio de aplicaciones de Azure antes de inscribirse para abrir una cuenta de Azure, vaya a [Prueba del Servicio de aplicaciones](https://azure.microsoft.com/try/app-service/) , donde podrá crear inmediatamente una aplicación web de inicio de corta duración en el Servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="a54b6-147">If you want to get started with Azure App Service before you sign up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/) where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="a54b6-148">No es necesario proporcionar ninguna tarjeta de crédito ni asumir ningún compromiso.</span><span class="sxs-lookup"><span data-stu-id="a54b6-148">No credit cards are required and there are no commitments.</span></span>
> 
> 

<a name="Next Steps"></a>

## <a name="next-steps"></a><span data-ttu-id="a54b6-149">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a54b6-149">Next steps</span></span>
* <span data-ttu-id="a54b6-150">Para comenzar con Azure, vea [Evaluación gratuita de Microsoft Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a54b6-150">To get started with Azure, see [Microsoft Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="a54b6-151">Para obtener información sobre el precio, soporte técnico y Acuerdo de Nivel de Servicio, consulte los siguientes vínculos.</span><span class="sxs-lookup"><span data-stu-id="a54b6-151">For information about pricing, support, and SLA, visit the following links.</span></span>
  
    [<span data-ttu-id="a54b6-152">Detalles de precios de Transferencias de datos</span><span class="sxs-lookup"><span data-stu-id="a54b6-152">Data Transfers Pricing Details</span></span>](https://azure.microsoft.com/pricing/details/data-transfers/)
  
    [<span data-ttu-id="a54b6-153">Planes de soporte técnico de Azure</span><span class="sxs-lookup"><span data-stu-id="a54b6-153">Microsoft Azure Support Plans</span></span>](https://azure.microsoft.com/support/plans/)
  
    [<span data-ttu-id="a54b6-154">Contratos de nivel de servicio</span><span class="sxs-lookup"><span data-stu-id="a54b6-154">Service Level Agreements</span></span>](https://azure.microsoft.com/support/legal/sla/)
  
    [<span data-ttu-id="a54b6-155">Detalles de precios de Base de datos SQL</span><span class="sxs-lookup"><span data-stu-id="a54b6-155">SQL Database Pricing Details</span></span>](https://azure.microsoft.com/pricing/details/sql-database/)
  
    <span data-ttu-id="a54b6-156">[Tamaños de máquinas virtuales y servicios en la nube de Microsoft Azure][vmsizes]</span><span class="sxs-lookup"><span data-stu-id="a54b6-156">[Virtual Machine and Cloud Service Sizes for Microsoft Azure][vmsizes]</span></span>
  
    [<span data-ttu-id="a54b6-157">Detalles de precios del Servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="a54b6-157">App Service Pricing Details</span></span>](https://azure.microsoft.com/pricing/details/app-service/)
  
    [<span data-ttu-id="a54b6-158">Detalles de precios de Servicios de aplicaciones: las conexiones SSL</span><span class="sxs-lookup"><span data-stu-id="a54b6-158">App Service Pricing Details - SSL Connections</span></span>](https://azure.microsoft.com/pricing/details/web-sites/#ssl-connections)
* <span data-ttu-id="a54b6-159">Para obtener información sobre las prácticas recomendadas de Servicios de aplicaciones de Azure, incluida la creación de una arquitectura resistente y escalable, consulte [Prácticas recomendadas: Aplicaciones web del Servicio de aplicaciones de Azure](http://blogs.msdn.com/b/windowsazure/archive/2014/02/10/best-practices-windows-azure-websites-waws.aspx).</span><span class="sxs-lookup"><span data-stu-id="a54b6-159">For information about Azure App Service best practices, including building a scalable and resilient architecture, see [Best Practices: Azure App Service Web Apps](http://blogs.msdn.com/b/windowsazure/archive/2014/02/10/best-practices-windows-azure-websites-waws.aspx).</span></span>
* <span data-ttu-id="a54b6-160">Para ver vídeos sobre cómo escalar aplicaciones del Servicio de aplicaciones, consulte los siguientes recursos:</span><span class="sxs-lookup"><span data-stu-id="a54b6-160">For videos about scaling App Service apps, see the following resources:</span></span>
  
  * [<span data-ttu-id="a54b6-161">Cuándo escalar sitios web de Azure: con Stefan Schackow</span><span class="sxs-lookup"><span data-stu-id="a54b6-161">When to Scale Azure Websites - with Stefan Schackow</span></span>](https://azure.microsoft.com/resources/videos/azure-web-sites-free-vs-standard-scaling/)
  * [<span data-ttu-id="a54b6-162">Escalación automática de sitios web de Azure mediante CPU o programación: con Stefan Schackow</span><span class="sxs-lookup"><span data-stu-id="a54b6-162">Auto Scaling Azure Websites, CPU or Scheduled - with Stefan Schackow</span></span>](https://azure.microsoft.com/resources/videos/auto-scaling-azure-web-sites/)
  * [<span data-ttu-id="a54b6-163">Escalación de sitios web de Azure: con Stefan Schackow</span><span class="sxs-lookup"><span data-stu-id="a54b6-163">How Azure Websites Scale - with Stefan Schackow</span></span>](https://azure.microsoft.com/resources/videos/how-azure-web-sites-scale/)

<!-- LINKS -->
[vmsizes]:/pricing/details/app-service/
[SQLaccountsbilling]:http://go.microsoft.com/fwlink/?LinkId=234930
[azuresubscriptions]:http://go.microsoft.com/fwlink/?LinkID=235288
[portal]: https://portal.azure.com/

<!-- IMAGES -->
[ChooseWHP]: ./media/web-sites-scale/scale1ChooseWHP.png
[ChooseBasicInstances]: ./media/web-sites-scale/scale2InstancesBasic.png
[SaveButton]: ./media/web-sites-scale/05SaveButton.png
[BasicComplete]: ./media/web-sites-scale/06BasicComplete.png
[ScaleStandard]: ./media/web-sites-scale/scale3InstancesStandard.png
[Autoscale]: ./media/web-sites-scale/scale4AutoScale.png
[SetTargetMetrics]: ./media/web-sites-scale/scale5AutoScaleTargetMetrics.png
[SetFirstRule]: ./media/web-sites-scale/scale6AutoScaleFirstRule.png
[SetSecondRule]: ./media/web-sites-scale/scale7AutoScaleSecondRule.png
[SetThirdRule]: ./media/web-sites-scale/scale8AutoScaleThirdRule.png
[SetRulesFinal]: ./media/web-sites-scale/scale9AutoScaleFinal.png
[ResourceGroup]: ./media/web-sites-scale/scale10ResourceGroup.png
[ScaleDatabase]: ./media/web-sites-scale/scale11SQLScale.png
[GeoReplication]: ./media/web-sites-scale/scale12SQLGeoReplication.png
