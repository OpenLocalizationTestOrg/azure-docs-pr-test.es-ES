---
title: "aaaScale seguridad de una aplicación en Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooscale seguridad de una aplicación en la capacidad de tooadd de servicio de aplicaciones de Azure y características."
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
ms.openlocfilehash: 97f46f77aeef95aec90d38e8396a023820e3caeb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="scale-up-an-app-in-azure"></a><span data-ttu-id="28c9c-103">Escalado vertical de aplicaciones en Azure</span><span class="sxs-lookup"><span data-stu-id="28c9c-103">Scale up an app in Azure</span></span>
<span data-ttu-id="28c9c-104">Este artículo muestra cómo tooscale la aplicación de servicio de aplicaciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="28c9c-104">This article shows you how tooscale your app in Azure App Service.</span></span> <span data-ttu-id="28c9c-105">Hay dos flujos de trabajo para la escala de escala, seguridad y escalado horizontal y este artículo explica Hola de escalado vertical flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="28c9c-105">There are two workflows for scaling, scale up and scale out, and this article explains hello scale up workflow.</span></span>

* <span data-ttu-id="28c9c-106">[Escalado vertical](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): obtenga más CPU, memoria, espacio en disco y características adicionales como máquinas virtuales exclusivas, dominios y certificados personalizados, espacios de ensayo, autoescala y mucho más.</span><span class="sxs-lookup"><span data-stu-id="28c9c-106">[Scale up](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): Get more CPU, memory, disk space, and extra features like dedicated virtual machines (VMs), custom domains and certificates, staging slots, autoscaling, and more.</span></span> <span data-ttu-id="28c9c-107">Escalar verticalmente cambiando Hola tarifa del plan de servicio de aplicaciones al que pertenece la aplicación.</span><span class="sxs-lookup"><span data-stu-id="28c9c-107">You scale up by changing hello pricing tier of the App Service plan that your app belongs to.</span></span>
* <span data-ttu-id="28c9c-108">[Escalar horizontalmente](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): aumentar Hola número de instancias de máquina virtual que ejecuta la aplicación.</span><span class="sxs-lookup"><span data-stu-id="28c9c-108">[Scale out](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): Increase hello number of VM instances that run your app.</span></span>
  <span data-ttu-id="28c9c-109">Puede escalar horizontalmente tooas muchas como 20 instancias, según el nivel de precios.</span><span class="sxs-lookup"><span data-stu-id="28c9c-109">You can scale out tooas many as 20 instances, depending on your pricing tier.</span></span> <span data-ttu-id="28c9c-110">[Entornos del servicio de aplicación](../app-service/app-service-app-service-environments-readme.md) en **Premium** capa aumentarán las instancias de too50 de recuento de escalabilidad horizontal.</span><span class="sxs-lookup"><span data-stu-id="28c9c-110">[App Service Environments](../app-service/app-service-app-service-environments-readme.md) in **Premium** tier will further increase your scale-out count too50 instances.</span></span> <span data-ttu-id="28c9c-111">Para más información sobre el escalado horizontal, consulte [Escalado del número de instancias de forma manual o automática](../monitoring-and-diagnostics/insights-how-to-scale.md).</span><span class="sxs-lookup"><span data-stu-id="28c9c-111">For more information about scaling out, see [Scale instance count manually or automatically](../monitoring-and-diagnostics/insights-how-to-scale.md).</span></span> <span data-ttu-id="28c9c-112">Allí encontrará espera cómo toouse escalado automático, que es el número de instancias de tooscale automáticamente en función de reglas predefinidas y las programaciones.</span><span class="sxs-lookup"><span data-stu-id="28c9c-112">There you will find out how toouse autoscaling, which is tooscale instance count automatically based on predefined rules and schedules.</span></span>

<span data-ttu-id="28c9c-113">Hola escala configuración toman sólo segundos tooapply y afecta a todas las aplicaciones en su [plan de servicio de aplicaciones](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span><span class="sxs-lookup"><span data-stu-id="28c9c-113">hello scale settings take only seconds tooapply and affect all apps in your [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span>
<span data-ttu-id="28c9c-114">No se requieren toochange el código o volver a implementar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="28c9c-114">They do not require you toochange your code or redeploy your application.</span></span>

<span data-ttu-id="28c9c-115">Para obtener información sobre precios de Hola y las características de los planes de servicio de aplicaciones individuales, consulte [detalles de precios de servicio de aplicación](https://azure.microsoft.com/pricing/details/web-sites/).</span><span class="sxs-lookup"><span data-stu-id="28c9c-115">For information about hello pricing and features of individual App Service plans, see [App Service Pricing Details](https://azure.microsoft.com/pricing/details/web-sites/).</span></span>  

> [!NOTE]
> <span data-ttu-id="28c9c-116">Antes de cambiar un plan de servicio de aplicaciones de hello **libre** nivel, primero debe quitar hello [los límites de gastos](https://azure.microsoft.com/pricing/spending-limits/) en su lugar para la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="28c9c-116">Before you switch an App Service plan from hello **Free** tier, you must first remove hello [spending limits](https://azure.microsoft.com/pricing/spending-limits/) in place for your Azure subscription.</span></span> <span data-ttu-id="28c9c-117">tooview o cambiar opciones de la suscripción de servicio de aplicaciones de Microsoft Azure, vea [suscripciones de Microsoft Azure][azuresubscriptions].</span><span class="sxs-lookup"><span data-stu-id="28c9c-117">tooview or change options for your Microsoft Azure App Service subscription, see [Microsoft Azure Subscriptions][azuresubscriptions].</span></span>
> 
> 

<a name="scalingsharedorbasic"></a>
<a name="scalingstandard"></a>

## <a name="scale-up-your-pricing-tier"></a><span data-ttu-id="28c9c-118">Escalado vertical del plan de tarifa</span><span class="sxs-lookup"><span data-stu-id="28c9c-118">Scale up your pricing tier</span></span>
1. <span data-ttu-id="28c9c-119">En el explorador, abra hello [portal de Azure][portal].</span><span class="sxs-lookup"><span data-stu-id="28c9c-119">In your browser, open hello [Azure portal][portal].</span></span>
2. <span data-ttu-id="28c9c-120">En la hoja de la aplicación, haga clic en **Toda la configuración** y en **Escalar verticalmente**.</span><span class="sxs-lookup"><span data-stu-id="28c9c-120">In your app's blade, click **All settings**, and then click **Scale Up**.</span></span>
   
    ![Navegue tooscale seguridad de la aplicación de Azure.][ChooseWHP]
3. <span data-ttu-id="28c9c-122">Elija el nivel y, después, haga clic en **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="28c9c-122">Choose your tier, and then click **Select**.</span></span>
   
    <span data-ttu-id="28c9c-123">Hola **notificaciones** ficha parpadeará en un color verde **correcto** una vez completada la operación de Hola.</span><span class="sxs-lookup"><span data-stu-id="28c9c-123">hello **Notifications** tab will flash a green **SUCCESS** after hello operation is complete.</span></span>

<a name="ScalingSQLServer"></a>

## <a name="scale-related-resources"></a><span data-ttu-id="28c9c-124">Recursos relacionados con el escalado</span><span class="sxs-lookup"><span data-stu-id="28c9c-124">Scale related resources</span></span>
<span data-ttu-id="28c9c-125">Si su aplicación depende de otros servicios, como Base de datos SQL o Almacenamiento de Azure, también puede escalar verticalmente estos recursos según sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="28c9c-125">If your app depends on other services, such as Azure SQL Database or Azure Storage, you can also scale up those resources based on your needs.</span></span> <span data-ttu-id="28c9c-126">Estos recursos no se escalan con hello plan de servicio de aplicaciones y se deben escalar por separado.</span><span class="sxs-lookup"><span data-stu-id="28c9c-126">These resources are not scaled with hello App Service plan and must be scaled separately.</span></span>

1. <span data-ttu-id="28c9c-127">En **Essentials**, haga clic en hello **grupo de recursos** vínculo.</span><span class="sxs-lookup"><span data-stu-id="28c9c-127">In **Essentials**, click hello **Resource group** link.</span></span>
   
    ![Escalado vertical de recursos relacionados con la aplicación de Azure](./media/web-sites-scale/RGEssentialsLink.png)
2. <span data-ttu-id="28c9c-129">Hola **resumen** forma parte de hello **grupo de recursos** hoja, haga clic en un recurso que desea tooscale.</span><span class="sxs-lookup"><span data-stu-id="28c9c-129">In hello **Summary** part of hello **Resource group** blade, click a resource that you want tooscale.</span></span> <span data-ttu-id="28c9c-130">Hola siguiente captura de pantalla muestra un recurso de base de datos SQL y un recurso de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="28c9c-130">hello following screenshot shows a SQL Database resource and an Azure Storage resource.</span></span>
   
    ![Navegue tooresource grupo hoja tooscale seguridad de la aplicación de Azure](./media/web-sites-scale/ResourceGroup.png)
3. <span data-ttu-id="28c9c-132">Para un recurso de base de datos SQL, haga clic en **configuración** > **tarifa** hello tooscale nivel de precios.</span><span class="sxs-lookup"><span data-stu-id="28c9c-132">For a SQL Database resource, click **Settings** > **Pricing tier** tooscale hello pricing tier.</span></span>
   
    ![Escalar verticalmente el back-end de base de datos SQL de hello para la aplicación de Azure](./media/web-sites-scale/ScaleDatabase.png)
   
    <span data-ttu-id="28c9c-134">También puede activar la [replicación geográfica](../sql-database/sql-database-geo-replication-overview.md) de su instancia de Base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="28c9c-134">You can also turn on [geo-replication](../sql-database/sql-database-geo-replication-overview.md) for your SQL Database instance.</span></span>
   
    <span data-ttu-id="28c9c-135">Para un recurso de almacenamiento de Azure, haga clic en **configuración** > **configuración** tooscale una de las opciones de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="28c9c-135">For an Azure Storage resource, click **Settings** > **Configuration** tooscale up your storage options.</span></span>
   
    ![Escalar verticalmente la cuenta de almacenamiento de Azure de hello utilizado por la aplicación de Azure](./media/web-sites-scale/ScaleStorage.png)

<a name="devfeatures"></a>

## <a name="learn-about-developer-features"></a><span data-ttu-id="28c9c-137">Más información sobre las características del desarrollador</span><span class="sxs-lookup"><span data-stu-id="28c9c-137">Learn about developer features</span></span>
<span data-ttu-id="28c9c-138">Función Hola tarifa hello siguientes orientadas al desarrollador características están disponibles:</span><span class="sxs-lookup"><span data-stu-id="28c9c-138">Depending on hello pricing tier, hello following developer-oriented features are available:</span></span>

### <a name="bitness"></a><span data-ttu-id="28c9c-139">Valor de bits</span><span class="sxs-lookup"><span data-stu-id="28c9c-139">Bitness</span></span>
* <span data-ttu-id="28c9c-140">Hola **básica**, **estándar**, y **Premium** niveles admiten aplicaciones de 64 bits y 32 bits.</span><span class="sxs-lookup"><span data-stu-id="28c9c-140">hello **Basic**, **Standard**, and **Premium** tiers support 64-bit and 32-bit applications.</span></span>
* <span data-ttu-id="28c9c-141">Hola **libre** y **Shared** plan niveles admiten sólo las aplicaciones de 32 bits.</span><span class="sxs-lookup"><span data-stu-id="28c9c-141">hello **Free** and **Shared** plan tiers support 32-bit applications only.</span></span>

### <a name="debugger-support"></a><span data-ttu-id="28c9c-142">Compatibilidad con el depurador</span><span class="sxs-lookup"><span data-stu-id="28c9c-142">Debugger support</span></span>
* <span data-ttu-id="28c9c-143">Compatibilidad del depurador está disponible para hello **libre**, **Shared**, y **básica** modos en una conexión por cada plan de servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="28c9c-143">Debugger support is available for hello **Free**, **Shared**, and **Basic** modes at one connection per App Service plan.</span></span>
* <span data-ttu-id="28c9c-144">Compatibilidad del depurador está disponible para hello **estándar** y **Premium** modos en cinco conexiones simultáneas por plan de servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="28c9c-144">Debugger support is available for hello **Standard** and **Premium** modes at five concurrent connections per App Service plan.</span></span>

<a name="OtherFeatures"></a>

## <a name="learn-about-other-features"></a><span data-ttu-id="28c9c-145">Más información sobre otras características</span><span class="sxs-lookup"><span data-stu-id="28c9c-145">Learn about other features</span></span>
* <span data-ttu-id="28c9c-146">Para obtener información detallada acerca de todos los de hello restantes características Hola servicio de aplicaciones de planes, incluido el precio y características de interés tooall los usuarios (incluidos los desarrolladores), consulte [detalles de precios de servicio de aplicación](https://azure.microsoft.com/pricing/details/web-sites/).</span><span class="sxs-lookup"><span data-stu-id="28c9c-146">For detailed information about all of hello remaining features in hello App Service plans, including pricing and features of interest tooall users (including developers), see [App Service Pricing Details](https://azure.microsoft.com/pricing/details/web-sites/).</span></span>

> [!NOTE]
> <span data-ttu-id="28c9c-147">Si desea tooget iniciado con el servicio de aplicación de Azure antes de registrarse para una cuenta de Azure, vaya demasiado[pruebe el servicio de aplicaciones](https://azure.microsoft.com/try/app-service/) donde puede crear inmediatamente una aplicación web de inicio de corta duración en el servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="28c9c-147">If you want tooget started with Azure App Service before you sign up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/) where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="28c9c-148">No es necesario proporcionar ninguna tarjeta de crédito ni asumir ningún compromiso.</span><span class="sxs-lookup"><span data-stu-id="28c9c-148">No credit cards are required and there are no commitments.</span></span>
> 
> 

<a name="Next Steps"></a>

## <a name="next-steps"></a><span data-ttu-id="28c9c-149">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="28c9c-149">Next steps</span></span>
* <span data-ttu-id="28c9c-150">tooget a trabajar con Azure, consulte [evaluación gratuita de Microsoft Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="28c9c-150">tooget started with Azure, see [Microsoft Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="28c9c-151">Para obtener información sobre los precios, soporte técnico y SLA, visitan Hola siguientes vínculos.</span><span class="sxs-lookup"><span data-stu-id="28c9c-151">For information about pricing, support, and SLA, visit hello following links.</span></span>
  
    [<span data-ttu-id="28c9c-152">Detalles de precios de Transferencias de datos</span><span class="sxs-lookup"><span data-stu-id="28c9c-152">Data Transfers Pricing Details</span></span>](https://azure.microsoft.com/pricing/details/data-transfers/)
  
    [<span data-ttu-id="28c9c-153">Planes de soporte técnico de Azure</span><span class="sxs-lookup"><span data-stu-id="28c9c-153">Microsoft Azure Support Plans</span></span>](https://azure.microsoft.com/support/plans/)
  
    [<span data-ttu-id="28c9c-154">Contratos de nivel de servicio</span><span class="sxs-lookup"><span data-stu-id="28c9c-154">Service Level Agreements</span></span>](https://azure.microsoft.com/support/legal/sla/)
  
    [<span data-ttu-id="28c9c-155">Detalles de precios de Base de datos SQL</span><span class="sxs-lookup"><span data-stu-id="28c9c-155">SQL Database Pricing Details</span></span>](https://azure.microsoft.com/pricing/details/sql-database/)
  
    <span data-ttu-id="28c9c-156">[Tamaños de máquinas virtuales y servicios en la nube de Microsoft Azure][vmsizes]</span><span class="sxs-lookup"><span data-stu-id="28c9c-156">[Virtual Machine and Cloud Service Sizes for Microsoft Azure][vmsizes]</span></span>
  
    [<span data-ttu-id="28c9c-157">Detalles de precios del Servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="28c9c-157">App Service Pricing Details</span></span>](https://azure.microsoft.com/pricing/details/app-service/)
  
    [<span data-ttu-id="28c9c-158">Detalles de precios de Servicios de aplicaciones: las conexiones SSL</span><span class="sxs-lookup"><span data-stu-id="28c9c-158">App Service Pricing Details - SSL Connections</span></span>](https://azure.microsoft.com/pricing/details/web-sites/#ssl-connections)
* <span data-ttu-id="28c9c-159">Para obtener información sobre las prácticas recomendadas de Servicios de aplicaciones de Azure, incluida la creación de una arquitectura resistente y escalable, consulte [Prácticas recomendadas: Aplicaciones web del Servicio de aplicaciones de Azure](http://blogs.msdn.com/b/windowsazure/archive/2014/02/10/best-practices-windows-azure-websites-waws.aspx).</span><span class="sxs-lookup"><span data-stu-id="28c9c-159">For information about Azure App Service best practices, including building a scalable and resilient architecture, see [Best Practices: Azure App Service Web Apps](http://blogs.msdn.com/b/windowsazure/archive/2014/02/10/best-practices-windows-azure-websites-waws.aspx).</span></span>
* <span data-ttu-id="28c9c-160">Para ver vídeos acerca de cómo escalar aplicaciones de servicio de aplicaciones, vea Hola recursos siguientes:</span><span class="sxs-lookup"><span data-stu-id="28c9c-160">For videos about scaling App Service apps, see hello following resources:</span></span>
  
  * [<span data-ttu-id="28c9c-161">Cuando tooScale sitios Web de Azure - con Stefan Schackow</span><span class="sxs-lookup"><span data-stu-id="28c9c-161">When tooScale Azure Websites - with Stefan Schackow</span></span>](https://azure.microsoft.com/resources/videos/azure-web-sites-free-vs-standard-scaling/)
  * [<span data-ttu-id="28c9c-162">Escalación automática de sitios web de Azure mediante CPU o programación: con Stefan Schackow</span><span class="sxs-lookup"><span data-stu-id="28c9c-162">Auto Scaling Azure Websites, CPU or Scheduled - with Stefan Schackow</span></span>](https://azure.microsoft.com/resources/videos/auto-scaling-azure-web-sites/)
  * [<span data-ttu-id="28c9c-163">Escalación de sitios web de Azure: con Stefan Schackow</span><span class="sxs-lookup"><span data-stu-id="28c9c-163">How Azure Websites Scale - with Stefan Schackow</span></span>](https://azure.microsoft.com/resources/videos/how-azure-web-sites-scale/)

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
