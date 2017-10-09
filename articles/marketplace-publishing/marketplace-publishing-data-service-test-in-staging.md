---
title: aaaTesting ofrecer el servicio de datos para hello Marketplace | Documentos de Microsoft
description: "Comprender cómo tootest el servicio de datos ofrecen para hello Azure Marketplace."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: e861bd11-f74d-4d77-b4b5-23fb463644ad
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: hascipio; avikova
ms.openlocfilehash: 1b9c7027d8e0818b9bdee5cfca971bab25dd1959
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="testing-your-data-service-offer-in-staging"></a><span data-ttu-id="ef1dc-103">Probar su oferta de Servicio de datos en Ensayo</span><span class="sxs-lookup"><span data-stu-id="ef1dc-103">Testing your Data Service offer in Staging</span></span>
> [!IMPORTANT]
> <span data-ttu-id="ef1dc-104">**En este momento, ya no se pueden incorporar nuevos editores del Servicio de datos. No se aprobarán nuevos servicios de datos para mostrarse en lista.**</span><span class="sxs-lookup"><span data-stu-id="ef1dc-104">**At this time we are no longer onboarding any new Data Service publishers. New dataservices will not get approved for listing.**</span></span> <span data-ttu-id="ef1dc-105">Si tiene una aplicación de negocio de SaaS desea toopublish en AppSource encontrará información más [aquí](https://appsource.microsoft.com/partners).</span><span class="sxs-lookup"><span data-stu-id="ef1dc-105">If you have a SaaS business application you would like toopublish on AppSource you can find more information [here](https://appsource.microsoft.com/partners).</span></span> <span data-ttu-id="ef1dc-106">Si tiene aplicaciones IaaS o desarrollador del servicio quiere como toopublish en Azure Marketplace también puede encontrar más información [aquí](https://azure.microsoft.com/marketplace/programs/certified/).</span><span class="sxs-lookup"><span data-stu-id="ef1dc-106">If you have an IaaS applications or developer service you would like toopublish on Azure Marketplace you can find more information [here](https://azure.microsoft.com/marketplace/programs/certified/).</span></span>
> 
> 

<span data-ttu-id="ef1dc-107">Después de completar los dos primeros pasos de Hola de [crear su cuenta de Microsoft Developer](marketplace-publishing-accounts-creation-registration.md) y [crear la oferta de servicio de datos en el Portal de publicación](marketplace-publishing-data-service-creation.md) está listo para hacer que su oferta disponible en hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="ef1dc-107">After completing hello first two steps of [Creating your Microsoft Developer account](marketplace-publishing-accounts-creation-registration.md) and [Creating your Data Service Offer in Publishing Portal](marketplace-publishing-data-service-creation.md) you’re ready for making your offer available in hello Azure Marketplace.</span></span> <span data-ttu-id="ef1dc-108">En este tema le guían a través de hello en primer lugar, intermedio, paso llamado "ensayo"</span><span class="sxs-lookup"><span data-stu-id="ef1dc-108">This topic will walk you through hello first, intermediate, step called “Staging”</span></span>

<span data-ttu-id="ef1dc-109">Significa que la implementación de la oferta en privado "espacio aislado" donde puede probar y comprobar su funcionalidad antes de insertar tooproduction de almacenamiento provisional.</span><span class="sxs-lookup"><span data-stu-id="ef1dc-109">Staging means deploying your offer in a private "sandbox" where you can test and verify its functionality before pushing it tooproduction.</span></span> <span data-ttu-id="ef1dc-110">oferta de Hello aparecerá en ensayo tal como lo haría a tooa cliente que ha implementado.</span><span class="sxs-lookup"><span data-stu-id="ef1dc-110">hello offer will appear in staging just as it would tooa customer who has deployed it.</span></span>

## <a name="step-1-pushing-your-offer-toostaging"></a><span data-ttu-id="ef1dc-111">Paso 1.</span><span class="sxs-lookup"><span data-stu-id="ef1dc-111">Step 1.</span></span> <span data-ttu-id="ef1dc-112">Insertar su toostaging de oferta</span><span class="sxs-lookup"><span data-stu-id="ef1dc-112">Pushing your offer toostaging</span></span>
<span data-ttu-id="ef1dc-113">Insertar su toostaging oferta permite oferta de hello tootest antes de que esté disponible toofuture suscriptores.</span><span class="sxs-lookup"><span data-stu-id="ef1dc-113">Pushing your offer toostaging allows you tootest hello offer before it becomes available toofuture subscribers.</span></span>  <span data-ttu-id="ef1dc-114">Puede ver cómo aparecerá su oferta y funcionar para aquellos que se suscriban tooyour datos.</span><span class="sxs-lookup"><span data-stu-id="ef1dc-114">You can see how your offer will appear and function for those subscribing tooyour data.</span></span>  

  ![dibujo](media/marketplace-publishing-data-service-test-in-staging/step-1.1.png)

1. <span data-ttu-id="ef1dc-116">Inicio de sesión en hello [Portal de publicación](https://publish.windowsazure.com)</span><span class="sxs-lookup"><span data-stu-id="ef1dc-116">Login into hello [Publishing Portal](https://publish.windowsazure.com)</span></span>
2. <span data-ttu-id="ef1dc-117">Seleccione **Data Services** en la ventana de navegación izquierdo de hello</span><span class="sxs-lookup"><span data-stu-id="ef1dc-117">Select **Data Services** in hello left navigation window</span></span>
3. <span data-ttu-id="ef1dc-118">Seleccione la oferta que desee toopush toostaging.</span><span class="sxs-lookup"><span data-stu-id="ef1dc-118">Select your offer you want toopush toostaging.</span></span> <span data-ttu-id="ef1dc-119">Verá Hola por encima de la pantalla.</span><span class="sxs-lookup"><span data-stu-id="ef1dc-119">You will see hello above screen.</span></span>
4. <span data-ttu-id="ef1dc-120">Haga clic en **Push tooStaging** botón.</span><span class="sxs-lookup"><span data-stu-id="ef1dc-120">Click **Push tooStaging** button.</span></span>  
5. <span data-ttu-id="ef1dc-121">Si hay problemas con hello oferta que sea necesario toobe había completado toostaging toopushing anterior, verá una lista que se muestra.</span><span class="sxs-lookup"><span data-stu-id="ef1dc-121">If there are issues with hello offer that needed toobe completed prior toopushing toostaging, you will see a list displayed.</span></span>  <span data-ttu-id="ef1dc-122">Corrija estos elementos, haga clic en cada elemento de lista de Hola.</span><span class="sxs-lookup"><span data-stu-id="ef1dc-122">Correct these items by clicking on each item in hello list.</span></span> <span data-ttu-id="ef1dc-123">Cuando todas las correcciones realizadas, haga clic en **Push tooStaging** nuevamente en el botón.</span><span class="sxs-lookup"><span data-stu-id="ef1dc-123">When all corrections made, click **Push tooStaging** button again.</span></span>

<span data-ttu-id="ef1dc-124">Si no hay ningún problema con su oferta verá la ventana emergente de Hola a continuación.</span><span class="sxs-lookup"><span data-stu-id="ef1dc-124">If there are no issues with your offer you will see hello popup window below.</span></span>  

<span data-ttu-id="ef1dc-125">Si no estás planificación/no aprobado toosurface su oferta en el Portal de Azure (actualmente con una capacidad limitada), a continuación, ventana emergente de hello simplemente cierre.</span><span class="sxs-lookup"><span data-stu-id="ef1dc-125">If you’re not planning/not approved toosurface your offer in Azure Portal (currently has limited capacity), then just close hello pop-up window.</span></span>

<span data-ttu-id="ef1dc-126">tootest los datos del servicio en el Portal de Azure (en el portal de DataMarket de toohello de suma), necesitará un tootest de Id. de suscripción de Azure con.</span><span class="sxs-lookup"><span data-stu-id="ef1dc-126">tootest your Data Service in Azure Portal (in addition toohello DataMarket portal), you will need an Azure Subscription ID tootest with.</span></span>  <span data-ttu-id="ef1dc-127">Este identificador de suscripción identificará cuenta Hola que estará permitido tootest su oferta.</span><span class="sxs-lookup"><span data-stu-id="ef1dc-127">This Subscription ID will identify hello account that will be allowed tootest your offer.</span></span>  

<span data-ttu-id="ef1dc-128">Corte y pegue el identificador de la suscripción y haga clic en hello toocontinue de marca de verificación.</span><span class="sxs-lookup"><span data-stu-id="ef1dc-128">Cut and paste your Subscription ID and click hello checkmark toocontinue.</span></span>

  ![dibujo](media/marketplace-publishing-data-service-test-in-staging/step-1.2.png)

> [!NOTE]
> <span data-ttu-id="ef1dc-130">Estos identificadores de las suscripciones de Azure solo son necesarias para las pruebas y almacenamiento provisional en hello [Portal de administración de Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="ef1dc-130">These Azure subscriptions IDs are only required for testing and staging in hello [Azure Management Portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="ef1dc-131">No son necesario tootest en Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="ef1dc-131">They are not required tootest in Azure Marketplace.</span></span>
> 
> 

<span data-ttu-id="ef1dc-132">Hello siguiente pantalla que aparece muestra que la publicación está teniendo lugar mostrando Hola "en curso" icono resaltado amarillo abajo.</span><span class="sxs-lookup"><span data-stu-id="ef1dc-132">hello next screen that appears shows that publishing is taking place by displaying hello “In progress” icon highlighted yellow below.</span></span> <span data-ttu-id="ef1dc-133">Insertar toostaging tarda entre 10 minutos de too15.</span><span class="sxs-lookup"><span data-stu-id="ef1dc-133">Pushing toostaging takes between 10 too15 minutes.</span></span>  <span data-ttu-id="ef1dc-134">Si tarda más, primero actualice su explorador (presione F5 en Internet Explorer).</span><span class="sxs-lookup"><span data-stu-id="ef1dc-134">If it takes longer, first refresh your browser (press F5 in IE).</span></span>  <span data-ttu-id="ef1dc-135">En casos excepcionales de Hola donde su oferta todavía está presionando toostaging después de una hora, haga clic en contacto Hola nos vincular toolet nos sabe que existe un problema.</span><span class="sxs-lookup"><span data-stu-id="ef1dc-135">In hello rare cases where your offer is still pushing toostaging after an hour, click hello contact us link toolet us know that there is an issue.</span></span>

  ![dibujo](media/marketplace-publishing-data-service-test-in-staging/step-1.3.png)

<span data-ttu-id="ef1dc-137">Cuando completa la tooStaging de inserción de Hola Hola "en curso" icono dejará de mover y se actualizará el estado de hello demasiado "ensayo".</span><span class="sxs-lookup"><span data-stu-id="ef1dc-137">When hello Push tooStaging completes hello “In progress” icon will stop moving and hello status will be updated too“Staged”.</span></span>  <span data-ttu-id="ef1dc-138">Se está ahora listo tootest su oferta.</span><span class="sxs-lookup"><span data-stu-id="ef1dc-138">You are now ready tootest your offer.</span></span>  

## <a name="step-2-test-your-staged-offer-in-datamarket"></a><span data-ttu-id="ef1dc-139">Paso 2:</span><span class="sxs-lookup"><span data-stu-id="ef1dc-139">Step 2.</span></span> <span data-ttu-id="ef1dc-140">Probar su oferta almacenada provisionalmente en DataMarket</span><span class="sxs-lookup"><span data-stu-id="ef1dc-140">Test your staged offer in DataMarket</span></span>
<span data-ttu-id="ef1dc-141">Haga clic en el vínculo de hello texto hello **"ver su servicio se ofrecen en..."**</span><span class="sxs-lookup"><span data-stu-id="ef1dc-141">Click hello link following hello text **“See Your service offer at…”**</span></span> <span data-ttu-id="ef1dc-142">pantalla de bienvenida toodisplay que Hola suscriptor verá que su oferta pasa tooproduction y aparecerá en DataMarket.</span><span class="sxs-lookup"><span data-stu-id="ef1dc-142">toodisplay hello screen that hello subscriber will see when your offer goes tooproduction and will appear in DataMarket.</span></span>

  ![dibujo](media/marketplace-publishing-data-service-test-in-staging/step-2.2.png)

<span data-ttu-id="ef1dc-144">Probar o compruebe cada uno de hello 12 elementos marcados anteriormente tooensure todos los logotipos, precios/transacciones, texto, imágenes, documentación y vínculos son correctas y funcionen correctamente.</span><span class="sxs-lookup"><span data-stu-id="ef1dc-144">Test or verify each of hello 12 items marked above tooensure all logos, prices/transactions, text, images, documentation, and links are correct and working properly.</span></span>  <span data-ttu-id="ef1dc-145">Se trata de un tooensure buen momento los valores de prueba que especificó al crear la oferta se han reemplazado por valores reales.</span><span class="sxs-lookup"><span data-stu-id="ef1dc-145">This is a good time tooensure any test values you entered when creating your offer have been replaced with actual values.</span></span>

1. <span data-ttu-id="ef1dc-146">Logotipo de la oferta</span><span class="sxs-lookup"><span data-stu-id="ef1dc-146">Offer logo</span></span>
2. <span data-ttu-id="ef1dc-147">Nombre de la oferta</span><span class="sxs-lookup"><span data-stu-id="ef1dc-147">Offer name</span></span>
3. <span data-ttu-id="ef1dc-148">Sitio Web de la compañía de publicador nombre/vínculo tooyour</span><span class="sxs-lookup"><span data-stu-id="ef1dc-148">Publisher name/link tooyour company's website</span></span>
4. <span data-ttu-id="ef1dc-149">Categorías de búsqueda para su oferta</span><span class="sxs-lookup"><span data-stu-id="ef1dc-149">Search categories for your offer</span></span>
5. <span data-ttu-id="ef1dc-150">Suscriptores de tooassist de vínculo de soporte técnico de su oferta</span><span class="sxs-lookup"><span data-stu-id="ef1dc-150">Your offer's support link tooassist subscribers</span></span>
6. <span data-ttu-id="ef1dc-151">Descripción contextual de la oferta</span><span class="sxs-lookup"><span data-stu-id="ef1dc-151">Contextual description for your offer</span></span>
7. <span data-ttu-id="ef1dc-152">Plan de oferta que describe los detalles de la facturación</span><span class="sxs-lookup"><span data-stu-id="ef1dc-152">Offer plan depicting billing details</span></span>
8. <span data-ttu-id="ef1dc-153">Código de tooimplementation de vínculo</span><span class="sxs-lookup"><span data-stu-id="ef1dc-153">Link tooimplementation code</span></span>
9. <span data-ttu-id="ef1dc-154">Imágenes de ejemplo que ilustran el uso de los datos de la oferta</span><span class="sxs-lookup"><span data-stu-id="ef1dc-154">Sample images that illustrate use of offer data</span></span>
10. <span data-ttu-id="ef1dc-155">Metadatos de entrada/salida para cada servicio en la oferta de Hola</span><span class="sxs-lookup"><span data-stu-id="ef1dc-155">Input/Output metadata for each service within hello offer</span></span>
11. <span data-ttu-id="ef1dc-156">Términos de uso de la oferta</span><span class="sxs-lookup"><span data-stu-id="ef1dc-156">Offer's Terms of Use</span></span>
12. <span data-ttu-id="ef1dc-157">Vista previa de los datos de la oferta de Hola</span><span class="sxs-lookup"><span data-stu-id="ef1dc-157">Preview of hello offer's data</span></span>

<span data-ttu-id="ef1dc-158">Finalmente, compruebe el servicio de hello trabajará en hello Datamarket haciendo clic en el vínculo de Hola "Explorar este conjunto de datos".</span><span class="sxs-lookup"><span data-stu-id="ef1dc-158">Finally, check hello service will work through hello Datamarket by clicking hello link “EXPLORE THIS DATASET”.</span></span>  <span data-ttu-id="ef1dc-159">Se abrirá una nueva ventana de herramienta de hello llamamos "Explorador de servicios" para que pueda ver los resultados de Hola de una consulta en el servicio.</span><span class="sxs-lookup"><span data-stu-id="ef1dc-159">A new window will open in hello tool we call “Service Explorer” so you can preview hello results of a query against your service.</span></span>  <span data-ttu-id="ef1dc-160">En esta ventana, puede especificar Hola parámetros necesitan y ver resultados de hello muestra de una consulta en el servicio.</span><span class="sxs-lookup"><span data-stu-id="ef1dc-160">In this window, you can enter hello parameters needed and see hello results displayed from a query against your service.</span></span>   <span data-ttu-id="ef1dc-161">Además, muestra es Hola URL para la consulta.</span><span class="sxs-lookup"><span data-stu-id="ef1dc-161">Also, displayed is hello URL for your Query.</span></span>  

> [!NOTE]
> <span data-ttu-id="ef1dc-162">Ser seguro descripción textual de Hola de tooreview del servicio de hello muestra en la parte superior de Hola.</span><span class="sxs-lookup"><span data-stu-id="ef1dc-162">Be sure tooreview hello textual description of hello service displayed at hello top.</span></span>  <span data-ttu-id="ef1dc-163">Y si su oferta consta de más de un servicio llamar a, haga clic en las pestañas de hello en hello inferior tooswitch toohello siguiente servicio tooreview y prueban.</span><span class="sxs-lookup"><span data-stu-id="ef1dc-163">And if your offer consists of more than one service call, click hello tabs at hello bottom tooswitch toohello next service tooreview and test.</span></span>
> 
> 

## <a name="next-step"></a><span data-ttu-id="ef1dc-164">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="ef1dc-164">Next step</span></span>
<span data-ttu-id="ef1dc-165">Si está teniendo problemas y necesita ayuda para resolverlos, póngase en contacto con el [soporte técnico para publicadores de Azure](http://go.microsoft.com/fwlink/?LinkId=272975).</span><span class="sxs-lookup"><span data-stu-id="ef1dc-165">If you are having issues and need help resolving them please contact [Azure Publisher Support](http://go.microsoft.com/fwlink/?LinkId=272975).</span></span>

<span data-ttu-id="ef1dc-166">Si está satisfecho y toopublish preparado su oferta, lea hello [tooProduction tooPush de aprobación de solicitud](marketplace-publishing-push-to-production.md) documentación.</span><span class="sxs-lookup"><span data-stu-id="ef1dc-166">If you are satisfied and ready toopublish your offer please read hello [Request Approval tooPush tooProduction](marketplace-publishing-push-to-production.md) documentation.</span></span>

## <a name="see-also"></a><span data-ttu-id="ef1dc-167">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="ef1dc-167">See Also</span></span>
* [<span data-ttu-id="ef1dc-168">Introducción: Cómo toopublish una toohello de oferta de Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="ef1dc-168">Getting Started: How toopublish an offer toohello Azure Marketplace</span></span>](marketplace-publishing-getting-started.md)

