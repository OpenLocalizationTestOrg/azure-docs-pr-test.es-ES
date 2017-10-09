---
title: aaaGuide toocreating un servicio de datos para hello Marketplace | Documentos de Microsoft
description: "Instrucciones detalladas de cómo toocreate, certificar e implementar un servicio de datos para la venta en hello Azure Marketplace."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 96194198-6991-43b4-918e-ee337e250339
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: hascipio; avikova
ms.openlocfilehash: 0220d357ae0ec89e7d4f6399605850e57c646f73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="data-service-publishing-guide-for-hello-azure-marketplace"></a><span data-ttu-id="cf0ca-103">Guía de publicación de servicio de datos para hello Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="cf0ca-103">Data Service Publishing Guide for hello Azure Marketplace</span></span>
> [!IMPORTANT]
> <span data-ttu-id="cf0ca-104">**En este momento, ya no se pueden incorporar nuevos editores del Servicio de datos. No se aprobarán nuevos servicios de datos para mostrarse en lista.**</span><span class="sxs-lookup"><span data-stu-id="cf0ca-104">**At this time we are no longer onboarding any new Data Service publishers. New dataservices will not get approved for listing.**</span></span> <span data-ttu-id="cf0ca-105">Si tiene una aplicación de negocio de SaaS desea toopublish en AppSource encontrará información más [aquí](https://appsource.microsoft.com/partners).</span><span class="sxs-lookup"><span data-stu-id="cf0ca-105">If you have a SaaS business application you would like toopublish on AppSource you can find more information [here](https://appsource.microsoft.com/partners).</span></span> <span data-ttu-id="cf0ca-106">Si tiene aplicaciones IaaS o desarrollador del servicio quiere como toopublish en Azure Marketplace también puede encontrar más información [aquí](https://azure.microsoft.com/marketplace/programs/certified/).</span><span class="sxs-lookup"><span data-stu-id="cf0ca-106">If you have an IaaS applications or developer service you would like toopublish on Azure Marketplace you can find more information [here](https://azure.microsoft.com/marketplace/programs/certified/).</span></span>
> 
> 

<span data-ttu-id="cf0ca-107">Después de completar el paso 1, de hello [creación de cuentas y el registro](marketplace-publishing-accounts-creation-registration.md), se le guiará a través de hello [General técnica](marketplace-publishing-pre-requisites.md) y [requisitos técnicos](marketplace-publishing-data-service-creation-prerequisites.md) de un servicio de datos se ofrecen en Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="cf0ca-107">After completing hello step 1, [Account Creation and Registration](marketplace-publishing-accounts-creation-registration.md), we guided you through hello [General Non-Technical](marketplace-publishing-pre-requisites.md) and [Technical Requirements](marketplace-publishing-data-service-creation-prerequisites.md) of a Data Service offer on Azure Marketplace.</span></span> <span data-ttu-id="cf0ca-108">Ahora se le guiará por los pasos de Hola para crear una oferta de servicio de datos en hello [Portal de publicación] [ link-pubportal] para hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="cf0ca-108">Now we will walk you through hello steps for creating a Data Service offer on hello [Publishing Portal][link-pubportal] for hello Azure Marketplace.</span></span>

## <a name="1----login-toohello-publishing-portal"></a><span data-ttu-id="cf0ca-109">1.    Inicio de sesión toohello Portal de publicación.</span><span class="sxs-lookup"><span data-stu-id="cf0ca-109">1.    Login toohello Publishing Portal.</span></span>
<span data-ttu-id="cf0ca-110">Vaya demasiado[https://publish.windowsazure.com](https://publish.windowsazure.com.)</span><span class="sxs-lookup"><span data-stu-id="cf0ca-110">Go too[https://publish.windowsazure.com](https://publish.windowsazure.com.)</span></span>

<span data-ttu-id="cf0ca-111">**Para la primera hora inicio de sesión tooPublishing Portal, usar hello misma cuenta con la que generar perfiles de vendedor de su empresa se ha registrado en el Centro para desarrolladores.**</span><span class="sxs-lookup"><span data-stu-id="cf0ca-111">**For first time login tooPublishing Portal, use hello same account with which your company’s Seller Profile was registered in Developer Center.**</span></span>  <span data-ttu-id="cf0ca-112">(Más adelante puede agregar a cualquier empleado de la empresa como Coadministrador en hello Portal de publicación).</span><span class="sxs-lookup"><span data-stu-id="cf0ca-112">(Later you can add any employee of your company as a co-admin in hello Publishing Portal).</span></span>

<span data-ttu-id="cf0ca-113">Haga clic en hello **publicar los servicios de datos** icono si éste es el primer inicio de sesión hello en el portal de publicación de Hola.</span><span class="sxs-lookup"><span data-stu-id="cf0ca-113">Click on hello **Publish a Data Services** tile if this is hello first login into hello publishing portal.</span></span>

## <a name="2----choose-data-services-in-hello-navigation-menu-on-hello-left-side"></a><span data-ttu-id="cf0ca-114">2.    Elija **Data Services** en el menú de navegación Hola Hola lado izquierdo.</span><span class="sxs-lookup"><span data-stu-id="cf0ca-114">2.    Choose **Data Services** in hello navigation menu on hello left side.</span></span>
  ![dibujo](media/marketplace-publishing-data-service-creation/pubportal-main-nav.png)

## <a name="3----create-a-new-data-service"></a><span data-ttu-id="cf0ca-116">3.    Creación de un nuevo servicio de datos</span><span class="sxs-lookup"><span data-stu-id="cf0ca-116">3.    Create a New Data Service</span></span>
<span data-ttu-id="cf0ca-117">Rellene el título de hello para la oferta de servicio de datos nueva y haga clic en "+" en hello derecho.</span><span class="sxs-lookup"><span data-stu-id="cf0ca-117">Fill in hello title for your new Data Service Offer and click on “+” on hello right.</span></span>

  ![dibujo](media/marketplace-publishing-data-service-creation/step-3.png)

## <a name="4----review-hello-sub-menu-under-hello-newly-created-data-service-in-hello-navigation-menu"></a><span data-ttu-id="cf0ca-119">4.    Submenú Hola revisión en hello recién creado del servicio de datos de menú de navegación de Hola.</span><span class="sxs-lookup"><span data-stu-id="cf0ca-119">4.    Review hello sub-menu under hello newly created Data Service in hello navigation menu.</span></span>
<span data-ttu-id="cf0ca-120">Haga clic en hello **tutorial** pestaña y revise todos los pasos necesarios necesarios toopublish correctamente Hola servicio de datos en hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="cf0ca-120">Click on hello **Walkthrough** tab and review all necessary steps needed toopublish properly hello Data Service on hello Azure Marketplace.</span></span>

> [!TIP]
> <span data-ttu-id="cf0ca-121">Siempre puede haga clic en vínculos de hello en la página del "Tutorial" Hola o utilizar las pestañas en el submenú de la oferta de servicio de datos de hello en el lado izquierdo de Hola.</span><span class="sxs-lookup"><span data-stu-id="cf0ca-121">You always can click on hello links in hello “Walkthrough” page or use tabs on hello Data Service offer’s sub-menu on hello left side.</span></span>
> 
> 

## <a name="5----create-a-new-plan"></a><span data-ttu-id="cf0ca-122">5.    Creación de un nuevo plan</span><span class="sxs-lookup"><span data-stu-id="cf0ca-122">5.    Create a new Plan.</span></span>
### <a name="offers-plans-transactions"></a><span data-ttu-id="cf0ca-123">Ofertas, Planes, Transacciones</span><span class="sxs-lookup"><span data-stu-id="cf0ca-123">Offers, Plans, transactions.</span></span>
<span data-ttu-id="cf0ca-124">Cada Oferta puede tener varios Planes, pero debe tener al menos un (1) Plan.</span><span class="sxs-lookup"><span data-stu-id="cf0ca-124">Each Offer can have multiple Plans, but must have at least one (1) Plan.</span></span> <span data-ttu-id="cf0ca-125">Cuando los usuarios finales suscriben tooyour oferta se suscriben para una Plan del oferta de hello.</span><span class="sxs-lookup"><span data-stu-id="cf0ca-125">When end-users subscribe tooyour offer they subscribe for one of hello offer’s Plan.</span></span> <span data-ttu-id="cf0ca-126">Cada plan define cómo se realizarán los usuarios finales pueden toouse capaz de su servicio.</span><span class="sxs-lookup"><span data-stu-id="cf0ca-126">Each plan defines how end-users will be able toouse your service.</span></span>

<span data-ttu-id="cf0ca-127">Actualmente Azure Marketplace admite transacciones de suscripción mensual según modelo solo para los servicios de datos, es decir, los usuarios finales pagará cargos mensuales según el precio de toohello de plan concreto de Hola que suscritos tooand será capaz de tooconsume cada número de mes de transacción definida por el plan de Hola.</span><span class="sxs-lookup"><span data-stu-id="cf0ca-127">Currently Azure Marketplace support only Monthly Subscription Transaction Based model for Data Services, i.e. end-users will pay monthly fee according toohello price of hello specific plan they subscribed tooand will be able tooconsume each month number of transaction defined by hello plan.</span></span>

<span data-ttu-id="cf0ca-128">Cada transacción normalmente definido como el número de registros que devolverá el servicio de datos basado en consulta de hello enviado toohello servicio.</span><span class="sxs-lookup"><span data-stu-id="cf0ca-128">Each Transaction usually defined as number of records your Data Service will return based on hello query sent toohello Service.</span></span> <span data-ttu-id="cf0ca-129">valor predeterminado de Hello es 100.</span><span class="sxs-lookup"><span data-stu-id="cf0ca-129">hello default is 100.</span></span> <span data-ttu-id="cf0ca-130">Número de transacciones devuelto será tooeach consulta número de registros dividido entre 100 y redondea al entero más próximo toohello.</span><span class="sxs-lookup"><span data-stu-id="cf0ca-130">Number of transactions returned tooeach query will be number of records divided by 100 and rounded up toohello closest integer.</span></span>

<span data-ttu-id="cf0ca-131">Es el servicio de Azure Marketplace capa responsabilidad toomonitor (metros) número de transacciones utilizados por cada consulta.</span><span class="sxs-lookup"><span data-stu-id="cf0ca-131">It’s Azure Marketplace Service layer responsibility toomonitor (meter) number of transactions consumed by each query.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cf0ca-132">Los usuarios finales que alcanza el límite de transacciones de Hola durante el mes de Hola se bloqueará impide continuar servicio de hello toouse hasta el final de su ciclo de suscripción mensual.</span><span class="sxs-lookup"><span data-stu-id="cf0ca-132">End-Users which reached hello transaction limit during hello month will be blocked from continuing toouse hello service until end of their monthly subscription cycle.</span></span>
> 
> <span data-ttu-id="cf0ca-133">Hola plan o uno de los planes de hello puede (pero no debe) incluye un número ilimitado de transacciones.</span><span class="sxs-lookup"><span data-stu-id="cf0ca-133">hello plan or one of hello plans can (but not must) include unlimited number of transactions.</span></span>
> 
> 

### <a name="create-a-plan"></a><span data-ttu-id="cf0ca-134">Cree un plan.</span><span class="sxs-lookup"><span data-stu-id="cf0ca-134">Create a plan.</span></span>
1. <span data-ttu-id="cf0ca-135">Haga clic en **"+"** toohello siguiente "Agregar un nuevo plan".</span><span class="sxs-lookup"><span data-stu-id="cf0ca-135">Click on **“+”** next toohello “Add a new plan”.</span></span>
2. <span data-ttu-id="cf0ca-136">Elija una de las opciones de hello: **Unlimited** o **limitado** el uso de este plan.</span><span class="sxs-lookup"><span data-stu-id="cf0ca-136">Choose one of hello options: **Unlimited** or **Limited** usage for this plan.</span></span>  <span data-ttu-id="cf0ca-137">Si limitado, a continuación, proporciona Hola número de transacciones Hola plan le permitirá tooconsume en un mes.</span><span class="sxs-lookup"><span data-stu-id="cf0ca-137">If Limited then provide hello number of transaction hello plan will allow tooconsume in a month.</span></span>
   
    ![dibujo](media/marketplace-publishing-data-service-creation/step-5.1.png)  
   
    <span data-ttu-id="cf0ca-139">Portal de publicación también sugerirá "Identificador de Plan de", que será usado toocommunicate toohello los usuarios finales Hola nombre del plan de Hola Hola interfaz de usuario de y también la usan hello tooidentify de servicio de mercado Hola Plan.</span><span class="sxs-lookup"><span data-stu-id="cf0ca-139">Publishing Portal will also suggest “Plan Identifier”, which will be used toocommunicate toohello end-users hello name of hello plan in hello UI and also used by hello Market Place Service tooidentify hello Plan.</span></span> <span data-ttu-id="cf0ca-140">Puede cambiar Hola "Identificador de Plan" Si desea.</span><span class="sxs-lookup"><span data-stu-id="cf0ca-140">You can change hello “Plan Identifier” if you want.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="cf0ca-141">Hola "Identificador de Plan" debe ser único dentro de ámbito de Hola de cada oferta.</span><span class="sxs-lookup"><span data-stu-id="cf0ca-141">hello “Plan Identifier” must be unique within hello scope of each offer.</span></span> <span data-ttu-id="cf0ca-142">Como muchos otros identificadores usados en Hola Plan de Portal de publicación se bloqueará el identificador después de hello primer tooproduction de publicación y no estará toochange capaz de este identificador.</span><span class="sxs-lookup"><span data-stu-id="cf0ca-142">As many other Identifiers used in hello Publishing Portal Plan identifier will be locked after hello first publishing tooproduction and you will not be able toochange this identifier.</span></span>
   > 
   > 
3. <span data-ttu-id="cf0ca-143">Haga clic en tooaccept su elección.</span><span class="sxs-lookup"><span data-stu-id="cf0ca-143">Click tooaccept your choice.</span></span>
4. <span data-ttu-id="cf0ca-144">A continuación, se le harán algunas preguntas adicionales sobre el Plan recién creado.</span><span class="sxs-lookup"><span data-stu-id="cf0ca-144">Then you will be asked few additional questions regarding your newly created Plan.</span></span>
   
    ![dibujo](media/marketplace-publishing-data-service-creation/step-5.2.png)

| <span data-ttu-id="cf0ca-146">Pregunta</span><span class="sxs-lookup"><span data-stu-id="cf0ca-146">Question</span></span> | <span data-ttu-id="cf0ca-147">Significado</span><span class="sxs-lookup"><span data-stu-id="cf0ca-147">Significance</span></span> |
| --- | --- |
| <span data-ttu-id="cf0ca-148">**¿Este Plan es gratuito y está disponible en todo el mundo?**</span><span class="sxs-lookup"><span data-stu-id="cf0ca-148">**This Plan is free and available world-wide?**</span></span> |<span data-ttu-id="cf0ca-149">Puede crear un plan completamente gratuito.</span><span class="sxs-lookup"><span data-stu-id="cf0ca-149">You can create a completely free-of-charge plan.</span></span> <span data-ttu-id="cf0ca-150">Si su Hola previsto sólo para esta oferta: significa que se va a publicar "Ofrecen libre" Hola Marketplace.</span><span class="sxs-lookup"><span data-stu-id="cf0ca-150">If it’s hello only plan for this offer – it means that you are publishing “Free Offer” in hello Marketplace.</span></span> <span data-ttu-id="cf0ca-151">Si es solo para una (de pocas) Plan, Hola le ofrece un toolearn de los usuarios finales de opción toooffer más información sobre el servicio con un número relativamente pequeño de transacciones al mes.</span><span class="sxs-lookup"><span data-stu-id="cf0ca-151">If it’s only for one (of few) Plan, hello it gives you an option toooffer end-users toolearn more about your service with a relatively small number of transactions per month.</span></span>  <span data-ttu-id="cf0ca-152">Si la respuesta de hello es "Sí", no se pedirá ningún preguntas más.</span><span class="sxs-lookup"><span data-stu-id="cf0ca-152">If hello answer is "Yes," then no further questions will be asked.</span></span> |

> [!NOTE]
> <span data-ttu-id="cf0ca-153">Los usuarios finales siempre puede actualizar toohello planes de pago.</span><span class="sxs-lookup"><span data-stu-id="cf0ca-153">End users can always upgrade toohello paid plans.</span></span>
> 
> 

| <span data-ttu-id="cf0ca-154">Pregunta</span><span class="sxs-lookup"><span data-stu-id="cf0ca-154">Question</span></span> | <span data-ttu-id="cf0ca-155">Significado</span><span class="sxs-lookup"><span data-stu-id="cf0ca-155">Significance</span></span> |
| --- | --- |
| <span data-ttu-id="cf0ca-156">**¿Hay una versión de evaluación gratuita disponible?**</span><span class="sxs-lookup"><span data-stu-id="cf0ca-156">**Is free trial available?**</span></span> |<span data-ttu-id="cf0ca-157">Puede elegir entre "No prueba" en absoluto o proporcionar una opción toouse su Plan para "Un mes".</span><span class="sxs-lookup"><span data-stu-id="cf0ca-157">You can choose between “No Trial” at all or give an option toouse your Plan for “One Month”.</span></span> <span data-ttu-id="cf0ca-158">Publicadores como toouse este beneficios opción tooprovide los usuarios finales Hola posibilidad toounderstand Hola de hello ofrecen de forma gratuita durante un mes.</span><span class="sxs-lookup"><span data-stu-id="cf0ca-158">Publishers like toouse this option tooprovide end-users hello possibility toounderstand hello benefits of hello offer for free for one month.</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="cf0ca-159">Los usuarios finales solo será capaz de toopurchase una prueba gratuita si ha establecido el instrumento de pago por ejemplo, tarjeta de crédito, contrato enterprise.</span><span class="sxs-lookup"><span data-stu-id="cf0ca-159">End-users will only be able toopurchase a free trial if they have established payment instrument e.g. credit card, enterprise agreement.</span></span>
> 
> <span data-ttu-id="cf0ca-160">Después de un mes de prueba gratuita de hello, Azure Marketplace iniciará cobrar a los clientes precio Hola hasta fecha de Hola de su suscripción de hello, a menos que el cliente de hello iniciada cancelación de suscripción de Hola.</span><span class="sxs-lookup"><span data-stu-id="cf0ca-160">After one month of hello free trial, Azure Marketplace will start charging customers hello price as of hello date of hello subscription, unless hello customer initiated hello subscription cancellation.</span></span> <span data-ttu-id="cf0ca-161">No se proporcionará ninguna notificación especial toohello los usuarios finales.</span><span class="sxs-lookup"><span data-stu-id="cf0ca-161">No special notification will be provided toohello end-users.</span></span>
> 
> 

| <span data-ttu-id="cf0ca-162">Pregunta</span><span class="sxs-lookup"><span data-stu-id="cf0ca-162">Question</span></span> | <span data-ttu-id="cf0ca-163">Significado</span><span class="sxs-lookup"><span data-stu-id="cf0ca-163">Significance</span></span> |
| --- | --- |
| <span data-ttu-id="cf0ca-164">**¿Este plan necesita un toopurchase de código de promoción?**</span><span class="sxs-lookup"><span data-stu-id="cf0ca-164">**This plan requires a promotion code toopurchase?**</span></span> |<span data-ttu-id="cf0ca-165">Publicadores tienen un tootheir de acceso de toolimit opción planes de servicio al proporcionar un código especial, denominado a "A Promocode" toospecific customers.</span><span class="sxs-lookup"><span data-stu-id="cf0ca-165">Publishers have an option toolimit access tootheir Service Plans by providing a special code, called “A Promocode” toospecific customers.</span></span> <span data-ttu-id="cf0ca-166">Solo los usuarios finales que tendrán este Promocode será capaz de toosubscribe toohello Plan.</span><span class="sxs-lookup"><span data-stu-id="cf0ca-166">Only end-users which will have this Promocode will be able toosubscribe toohello Plan.</span></span> <span data-ttu-id="cf0ca-167">Si elige "No", acepta que todos los usuarios de región de Hola donde ofrecen Hola están disponible (vea [Guía de contenido de Marketing de Marketplace](marketplace-publishing-push-to-staging.md) para obtener más detalles) será capaz de toosubscribe toothis plan.</span><span class="sxs-lookup"><span data-stu-id="cf0ca-167">If you choose “No”, then you agree that everyone from hello region where hello offer is available (See [Marketplace Marketing Content Guide](marketplace-publishing-push-to-staging.md) for more details) will be able toosubscribe toothis plan.</span></span> <span data-ttu-id="cf0ca-168">No se le harán más preguntas.</span><span class="sxs-lookup"><span data-stu-id="cf0ca-168">No further questions will be asked.</span></span> |
| <span data-ttu-id="cf0ca-169">**¿Ocultar también este plan a cualquier persona que no tenga un código de promoción válido?**</span><span class="sxs-lookup"><span data-stu-id="cf0ca-169">**Also hide this plan from anyone who doesn’t have a valid promotion code?**</span></span> |<span data-ttu-id="cf0ca-170">Si Hola respuesta toohello anterior pregunta es "Sí" hello publicador tiene una opción toocompletely suprimir este plan desde que aparecen en hello interfaz de usuario de hello Marketplace.</span><span class="sxs-lookup"><span data-stu-id="cf0ca-170">If hello answer toohello previous question is “Yes” hello Publisher has an option toocompletely remove this plan from appearing in hello UI of hello Marketplace.</span></span> <span data-ttu-id="cf0ca-171">Significa que, los clientes no podrán ver este plan en la página de detalles de la oferta de Hola.</span><span class="sxs-lookup"><span data-stu-id="cf0ca-171">It means, customers will not see this plan in hello Offer’s details page.</span></span> <span data-ttu-id="cf0ca-172">Los usuarios finales que recibirán un toopurchase promocode, serán tooit toosubscribe capaz de usar este promocode.</span><span class="sxs-lookup"><span data-stu-id="cf0ca-172">End-users which will receive a promocode toopurchase it, will be able toosubscribe tooit using this promocode.</span></span> |

## <a name="6----create-your-marketplace-marketing-content"></a><span data-ttu-id="cf0ca-173">6.    Creación de contenido de marketing de Marketplace</span><span class="sxs-lookup"><span data-stu-id="cf0ca-173">6.    Create your Marketplace marketing content</span></span>
<span data-ttu-id="cf0ca-174">Para cómo tooprovide información necesaria en **Marketing, precios, compatibilidad y categorías** pestañas, visitan [Guía de contenido de Marketing de Marketplace](marketplace-publishing-push-to-staging.md) que es común artefactos tooall publicados en hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="cf0ca-174">For How tooprovide information required in **Marketing, Pricing, Support and Categories** tabs please visit [Marketplace Marketing Content Guide](marketplace-publishing-push-to-staging.md) which is common tooall artifacts published in hello Azure Marketplace.</span></span>  

## <a name="7----connect-your-offer-tooyour-service-sql-azure-based-or-web-service-based"></a><span data-ttu-id="cf0ca-175">7.    Conectar su tooyour de oferta de servicio (en función de SQL Azure o en función de servicio de Web).</span><span class="sxs-lookup"><span data-stu-id="cf0ca-175">7.    Connect your offer tooyour Service (SQL Azure based or Web Service based).</span></span>
<span data-ttu-id="cf0ca-176">Haga clic en hello **Data Services** submenú.</span><span class="sxs-lookup"><span data-stu-id="cf0ca-176">Click on hello **Data Services** sub-menu.</span></span>

<span data-ttu-id="cf0ca-177">En la mitad superior de Hola de página Hola se le preguntará de oferta de hello tooprovide **Namespace**.</span><span class="sxs-lookup"><span data-stu-id="cf0ca-177">On hello upper half of hello page you’ll be asked tooprovide hello offer’s **Namespace**.</span></span>  

  ![dibujo](media/marketplace-publishing-data-service-creation/step-7.png)

<span data-ttu-id="cf0ca-179">Hola por debajo de la pregunta definirá cómo Hola publicador va tooexpose recién creado oferta tooAzure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="cf0ca-179">hello below question will define how hello Publisher is going tooexpose newly created offer tooAzure Marketplace.</span></span> <span data-ttu-id="cf0ca-180">(Para obtener más información, vea hello [Guía de requisitos previos Technical Data Services](marketplace-publishing-data-service-creation-prerequisites.md)).</span><span class="sxs-lookup"><span data-stu-id="cf0ca-180">(For more details see hello [Data Services Technical Prerequisite Guide](marketplace-publishing-data-service-creation-prerequisites.md)).</span></span>

  ![dibujo](media/marketplace-publishing-data-service-creation/step-7.2.png)

<span data-ttu-id="cf0ca-182">**Publicar Hola servicio de basado en base de datos**</span><span class="sxs-lookup"><span data-stu-id="cf0ca-182">**Publishing hello Database based service**</span></span>

<span data-ttu-id="cf0ca-183">Haga clic en **Base de datos**.</span><span class="sxs-lookup"><span data-stu-id="cf0ca-183">Click on **Database**.</span></span> <span data-ttu-id="cf0ca-184">Hola después de la página se mostrará:</span><span class="sxs-lookup"><span data-stu-id="cf0ca-184">hello following page will appear:</span></span>

  ![dibujo](media/marketplace-publishing-data-service-creation/step-7.3.png)

<span data-ttu-id="cf0ca-186">toocreate una asignación de CSDL para hello conjunto de datos se basa en hello base de datos de SQL Azure:</span><span class="sxs-lookup"><span data-stu-id="cf0ca-186">toocreate a CSDL mapping for hello Dataset based on hello SQL Azure DB:</span></span>

  ![dibujo](media/marketplace-publishing-data-service-creation/step-7.4.png)

<span data-ttu-id="cf0ca-188">Y, a continuación, para cada tabla</span><span class="sxs-lookup"><span data-stu-id="cf0ca-188">And then for each table</span></span>

  ![dibujo](media/marketplace-publishing-data-service-creation/step-7.5.png)

  ![dibujo](media/marketplace-publishing-data-service-creation/step-7.6.png)

<span data-ttu-id="cf0ca-191">Si Servicio web</span><span class="sxs-lookup"><span data-stu-id="cf0ca-191">If Web Service</span></span>

  ![dibujo](media/marketplace-publishing-data-service-creation/step-7.7.png)

> [!IMPORTANT]
> <span data-ttu-id="cf0ca-193">Lectura [asignación existente web tooOData de servicio a través de CSDL](marketplace-publishing-data-service-creation-odata-mapping.md) para obtener instrucciones detalladas y ejemplos para crear un servicio Web de CSDL.</span><span class="sxs-lookup"><span data-stu-id="cf0ca-193">Read [Mapping an existing web service tooOData through CSDL](marketplace-publishing-data-service-creation-odata-mapping.md) for detailed instructions and examples for creating a CSDL Web Service.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="cf0ca-194">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="cf0ca-194">Next Steps</span></span>
<span data-ttu-id="cf0ca-195">Ahora que ha creado su oferta de servicio de datos, asegúrese de completar las instrucciones de Hola Hola [Guía de contenido de Marketing de Marketplace](marketplace-publishing-push-to-staging.md) antes de continuar demasiado[probando el servicio de datos de almacenamiento provisional](marketplace-publishing-data-service-test-in-staging.md).</span><span class="sxs-lookup"><span data-stu-id="cf0ca-195">Now that you've created your Data Service offer, please ensure that you complete hello instructions in hello [Marketplace Marketing Content Guide](marketplace-publishing-push-to-staging.md) before you move forward too[Testing your Data Service in Staging](marketplace-publishing-data-service-test-in-staging.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="cf0ca-196">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="cf0ca-196">See Also</span></span>
* [<span data-ttu-id="cf0ca-197">Introducción: Cómo toopublish una toohello de oferta de Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="cf0ca-197">Getting Started: How toopublish an offer toohello Azure Marketplace</span></span>](marketplace-publishing-getting-started.md)
* <span data-ttu-id="cf0ca-198">Si está interesado en conocer Hola proceso general de asignación de OData y su propósito, lea este artículo [asignación de OData del servicio de datos](marketplace-publishing-data-service-creation-odata-mapping.md) tooreview definiciones, estructuras e instrucciones.</span><span class="sxs-lookup"><span data-stu-id="cf0ca-198">If you are interested in understanding hello overall OData mapping process and purpose, read this article [Data Service OData Mapping](marketplace-publishing-data-service-creation-odata-mapping.md) tooreview definitions, structures, and instructions.</span></span>
* <span data-ttu-id="cf0ca-199">Si está interesado en el aprendizaje y nodos de descripción Hola específicos y sus parámetros, lea este artículo [nodos de asignación de datos de servicio OData](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) para las definiciones y explicaciones, ejemplos y contexto de casos de uso.</span><span class="sxs-lookup"><span data-stu-id="cf0ca-199">If you are interested in learning and understanding hello specific nodes and their parameters, read this article [Data Service OData Mapping Nodes](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) for definitions and explanations, examples, and use case context.</span></span>
* <span data-ttu-id="cf0ca-200">Si está interesado en Revisar ejemplos, lea este artículo [ejemplos de asignación de datos de servicios OData](marketplace-publishing-data-service-creation-odata-mapping-examples.md) toosee código de ejemplo y comprender la sintaxis del código y el contexto.</span><span class="sxs-lookup"><span data-stu-id="cf0ca-200">If you are interested in reviewing examples, read this article [Data Service OData Mapping Examples](marketplace-publishing-data-service-creation-odata-mapping-examples.md) toosee sample code and understand code syntax and context.</span></span>

[link-pubportal]:https://publish.windowsazure.com
