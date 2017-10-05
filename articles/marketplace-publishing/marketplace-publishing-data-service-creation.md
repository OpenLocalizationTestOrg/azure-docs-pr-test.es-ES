---
title: "Guía para crear un servicio de datos en Marketplace | Microsoft Docs"
description: "Se ofrecen instrucciones detalladas sobre cómo crear, certificar e implementar un servicio de datos para la venta en Azure Marketplace."
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
ms.openlocfilehash: c0c9362f1c2e15c947aaaf7187f3383ad243140f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="data-service-publishing-guide-for-the-azure-marketplace"></a><span data-ttu-id="6d737-103">Guía de publicación de servicio de datos para Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="6d737-103">Data Service Publishing Guide for the Azure Marketplace</span></span>
> [!IMPORTANT]
> <span data-ttu-id="6d737-104">**En este momento, ya no se pueden incorporar nuevos editores del Servicio de datos. No se aprobarán nuevos servicios de datos para mostrarse en lista.**</span><span class="sxs-lookup"><span data-stu-id="6d737-104">**At this time we are no longer onboarding any new Data Service publishers. New dataservices will not get approved for listing.**</span></span> <span data-ttu-id="6d737-105">Si tiene una aplicación de negocio de SaaS que desea publicar en AppSource, puede encontrar más información [aquí](https://appsource.microsoft.com/partners).</span><span class="sxs-lookup"><span data-stu-id="6d737-105">If you have a SaaS business application you would like to publish on AppSource you can find more information [here](https://appsource.microsoft.com/partners).</span></span> <span data-ttu-id="6d737-106">Si tiene aplicaciones IaaS o un servicio de desarrollo que quiera publicar en Azure Marketplace, puede encontrar más información [aquí](https://azure.microsoft.com/marketplace/programs/certified/).</span><span class="sxs-lookup"><span data-stu-id="6d737-106">If you have an IaaS applications or developer service you would like to publish on Azure Marketplace you can find more information [here](https://azure.microsoft.com/marketplace/programs/certified/).</span></span>
> 
> 

<span data-ttu-id="6d737-107">Después de completar el paso 1, [Creación y registro de la cuenta](marketplace-publishing-accounts-creation-registration.md), le guiamos por los requisitos [no técnicos](marketplace-publishing-pre-requisites.md) y [técnicos](marketplace-publishing-data-service-creation-prerequisites.md) generales de una oferta de servicio de datos en Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="6d737-107">After completing the step 1, [Account Creation and Registration](marketplace-publishing-accounts-creation-registration.md), we guided you through the [General Non-Technical](marketplace-publishing-pre-requisites.md) and [Technical Requirements](marketplace-publishing-data-service-creation-prerequisites.md) of a Data Service offer on Azure Marketplace.</span></span> <span data-ttu-id="6d737-108">Ahora le guiaremos a través de los pasos para crear una oferta de servicio de datos en el [Portal de publicación][link-pubportal] de Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="6d737-108">Now we will walk you through the steps for creating a Data Service offer on the [Publishing Portal][link-pubportal] for the Azure Marketplace.</span></span>

## <a name="1----login-to-the-publishing-portal"></a><span data-ttu-id="6d737-109">1.    Inicie sesión en el Portal de publicación.</span><span class="sxs-lookup"><span data-stu-id="6d737-109">1.    Login to the Publishing Portal.</span></span>
<span data-ttu-id="6d737-110">Vaya a [https://publish.windowsazure.com](https://publish.windowsazure.com.)</span><span class="sxs-lookup"><span data-stu-id="6d737-110">Go to [https://publish.windowsazure.com](https://publish.windowsazure.com.)</span></span>

<span data-ttu-id="6d737-111">**Para el primer inicio de sesión en el Portal de publicación, use la misma cuenta con la que se registró el perfil de vendedor de la compañía en el Centro para desarrolladores.**</span><span class="sxs-lookup"><span data-stu-id="6d737-111">**For first time login to Publishing Portal, use the same account with which your company’s Seller Profile was registered in Developer Center.**</span></span>  <span data-ttu-id="6d737-112">(Posteriormente, puede agregar a cualquier empleado de la empresa como coadministrador en el Portal de publicación).</span><span class="sxs-lookup"><span data-stu-id="6d737-112">(Later you can add any employee of your company as a co-admin in the Publishing Portal).</span></span>

<span data-ttu-id="6d737-113">Haga clic en el icono **Publicar un servicio de datos** si se trata del primer inicio de sesión en el Portal de publicación.</span><span class="sxs-lookup"><span data-stu-id="6d737-113">Click on the **Publish a Data Services** tile if this is the first login into the publishing portal.</span></span>

## <a name="2----choose-data-services-in-the-navigation-menu-on-the-left-side"></a><span data-ttu-id="6d737-114">2.    Elija **Servicios de datos** en el menú de navegación del lado izquierdo.</span><span class="sxs-lookup"><span data-stu-id="6d737-114">2.    Choose **Data Services** in the navigation menu on the left side.</span></span>
  ![dibujo](media/marketplace-publishing-data-service-creation/pubportal-main-nav.png)

## <a name="3----create-a-new-data-service"></a><span data-ttu-id="6d737-116">3.    Creación de un nuevo servicio de datos</span><span class="sxs-lookup"><span data-stu-id="6d737-116">3.    Create a New Data Service</span></span>
<span data-ttu-id="6d737-117">Complete el título de la nueva oferta de servicio de datos y haga clic en el signo "+" de la derecha.</span><span class="sxs-lookup"><span data-stu-id="6d737-117">Fill in the title for your new Data Service Offer and click on “+” on the right.</span></span>

  ![dibujo](media/marketplace-publishing-data-service-creation/step-3.png)

## <a name="4----review-the-sub-menu-under-the-newly-created-data-service-in-the-navigation-menu"></a><span data-ttu-id="6d737-119">4.    Revise el submenú del servicio de datos recién creado en el menú de navegación.</span><span class="sxs-lookup"><span data-stu-id="6d737-119">4.    Review the sub-menu under the newly created Data Service in the navigation menu.</span></span>
<span data-ttu-id="6d737-120">Haga clic en la pestaña **Tutorial** y revise todos los pasos necesarios para publicar correctamente el servicio de datos en Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="6d737-120">Click on the **Walkthrough** tab and review all necessary steps needed to publish properly the Data Service on the Azure Marketplace.</span></span>

> [!TIP]
> <span data-ttu-id="6d737-121">Siempre puede hacer clic en los vínculos de la página "Tutorial" o usar las pestañas del submenú de la oferta del servicio de datos en el lado izquierdo.</span><span class="sxs-lookup"><span data-stu-id="6d737-121">You always can click on the links in the “Walkthrough” page or use tabs on the Data Service offer’s sub-menu on the left side.</span></span>
> 
> 

## <a name="5----create-a-new-plan"></a><span data-ttu-id="6d737-122">5.    Creación de un nuevo plan</span><span class="sxs-lookup"><span data-stu-id="6d737-122">5.    Create a new Plan.</span></span>
### <a name="offers-plans-transactions"></a><span data-ttu-id="6d737-123">Ofertas, Planes, Transacciones</span><span class="sxs-lookup"><span data-stu-id="6d737-123">Offers, Plans, transactions.</span></span>
<span data-ttu-id="6d737-124">Cada Oferta puede tener varios Planes, pero debe tener al menos un (1) Plan.</span><span class="sxs-lookup"><span data-stu-id="6d737-124">Each Offer can have multiple Plans, but must have at least one (1) Plan.</span></span> <span data-ttu-id="6d737-125">Cuando los usuarios finales se suscriben a su oferta, también lo hacen en uno de los planes de la oferta.</span><span class="sxs-lookup"><span data-stu-id="6d737-125">When end-users subscribe to your offer they subscribe for one of the offer’s Plan.</span></span> <span data-ttu-id="6d737-126">Cada plan define el modo en que los usuarios podrán hacer uso del servicio.</span><span class="sxs-lookup"><span data-stu-id="6d737-126">Each plan defines how end-users will be able to use your service.</span></span>

<span data-ttu-id="6d737-127">Actualmente, Azure Marketplace admite solo el modelo basado en transacciones de suscripciones mensuales para Servicios de datos; es decir, los usuarios finales pagarán una cuota mensual según el precio del plan específico al que se hayan suscrito y podrán consumir cada mes el número de transacciones definidas por el plan.</span><span class="sxs-lookup"><span data-stu-id="6d737-127">Currently Azure Marketplace support only Monthly Subscription Transaction Based model for Data Services, i.e. end-users will pay monthly fee according to the price of the specific plan they subscribed to and will be able to consume each month number of transaction defined by the plan.</span></span>

<span data-ttu-id="6d737-128">Cada Transacción se define normalmente como el número de registros que devolverá el Servicio de datos en función de la consulta enviada al Servicio.</span><span class="sxs-lookup"><span data-stu-id="6d737-128">Each Transaction usually defined as number of records your Data Service will return based on the query sent to the Service.</span></span> <span data-ttu-id="6d737-129">El valor predeterminado es 100.</span><span class="sxs-lookup"><span data-stu-id="6d737-129">The default is 100.</span></span> <span data-ttu-id="6d737-130">El número de transacciones devueltas para cada consulta será el número de registros dividido por 100 y redondeado al entero más cercano.</span><span class="sxs-lookup"><span data-stu-id="6d737-130">Number of transactions returned to each query will be number of records divided by 100 and rounded up to the closest integer.</span></span>

<span data-ttu-id="6d737-131">El nivel del Servicio de Azure Marketplace es quien se ocupa de supervisar (medir) el número de transacciones consumidas por cada consulta.</span><span class="sxs-lookup"><span data-stu-id="6d737-131">It’s Azure Marketplace Service layer responsibility to monitor (meter) number of transactions consumed by each query.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6d737-132">Los usuarios finales que alcancen el límite de transacciones durante el mes no podrán seguir utilizando el servicio hasta el final de su ciclo de suscripción mensual.</span><span class="sxs-lookup"><span data-stu-id="6d737-132">End-Users which reached the transaction limit during the month will be blocked from continuing to use the service until end of their monthly subscription cycle.</span></span>
> 
> <span data-ttu-id="6d737-133">El plan (o uno de los planes) puede (pero no es obligatorio) incluir un número ilimitado de transacciones.</span><span class="sxs-lookup"><span data-stu-id="6d737-133">The plan or one of the plans can (but not must) include unlimited number of transactions.</span></span>
> 
> 

### <a name="create-a-plan"></a><span data-ttu-id="6d737-134">Cree un plan.</span><span class="sxs-lookup"><span data-stu-id="6d737-134">Create a plan.</span></span>
1. <span data-ttu-id="6d737-135">Haga clic en **"+"** junto a "Agregar un nuevo plan".</span><span class="sxs-lookup"><span data-stu-id="6d737-135">Click on **“+”** next to the “Add a new plan”.</span></span>
2. <span data-ttu-id="6d737-136">Elija una de las opciones para el uso de este plan: **Ilimitado** o **Limitado**.</span><span class="sxs-lookup"><span data-stu-id="6d737-136">Choose one of the options: **Unlimited** or **Limited** usage for this plan.</span></span>  <span data-ttu-id="6d737-137">Si elige Limitado, indique a continuación el número de transacciones que el plan permitirá consumir en un mes.</span><span class="sxs-lookup"><span data-stu-id="6d737-137">If Limited then provide the number of transaction the plan will allow to consume in a month.</span></span>
   
    ![dibujo](media/marketplace-publishing-data-service-creation/step-5.1.png)  
   
    <span data-ttu-id="6d737-139">El Portal de publicación también le sugerirá el "Identificador del Plan", que se utilizará para comunicar a los usuarios finales el nombre del plan en la interfaz de usuario y también se utilizará por el servicio de Marketplace para identificar el Plan.</span><span class="sxs-lookup"><span data-stu-id="6d737-139">Publishing Portal will also suggest “Plan Identifier”, which will be used to communicate to the end-users the name of the plan in the UI and also used by the Market Place Service to identify the Plan.</span></span> <span data-ttu-id="6d737-140">Puede cambiar el "Identificador del Plan" si lo desea.</span><span class="sxs-lookup"><span data-stu-id="6d737-140">You can change the “Plan Identifier” if you want.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="6d737-141">El "Identificador del Plan" debe ser único dentro del ámbito de cada oferta.</span><span class="sxs-lookup"><span data-stu-id="6d737-141">The “Plan Identifier” must be unique within the scope of each offer.</span></span> <span data-ttu-id="6d737-142">Como muchos otros identificadores utilizados en el Portal de publicación, el Identificador del Plan se bloqueará tras la primera publicación en producción y ya no podrá cambiarlo.</span><span class="sxs-lookup"><span data-stu-id="6d737-142">As many other Identifiers used in the Publishing Portal Plan identifier will be locked after the first publishing to production and you will not be able to change this identifier.</span></span>
   > 
   > 
3. <span data-ttu-id="6d737-143">Haga clic para aceptar su elección.</span><span class="sxs-lookup"><span data-stu-id="6d737-143">Click to accept your choice.</span></span>
4. <span data-ttu-id="6d737-144">A continuación, se le harán algunas preguntas adicionales sobre el Plan recién creado.</span><span class="sxs-lookup"><span data-stu-id="6d737-144">Then you will be asked few additional questions regarding your newly created Plan.</span></span>
   
    ![dibujo](media/marketplace-publishing-data-service-creation/step-5.2.png)

| <span data-ttu-id="6d737-146">Pregunta</span><span class="sxs-lookup"><span data-stu-id="6d737-146">Question</span></span> | <span data-ttu-id="6d737-147">Significado</span><span class="sxs-lookup"><span data-stu-id="6d737-147">Significance</span></span> |
| --- | --- |
| <span data-ttu-id="6d737-148">**¿Este Plan es gratuito y está disponible en todo el mundo?**</span><span class="sxs-lookup"><span data-stu-id="6d737-148">**This Plan is free and available world-wide?**</span></span> |<span data-ttu-id="6d737-149">Puede crear un plan completamente gratuito.</span><span class="sxs-lookup"><span data-stu-id="6d737-149">You can create a completely free-of-charge plan.</span></span> <span data-ttu-id="6d737-150">Si es el único plan de esta oferta, eso significa que está publicando una "Oferta gratuita" en Marketplace.</span><span class="sxs-lookup"><span data-stu-id="6d737-150">If it’s the only plan for this offer – it means that you are publishing “Free Offer” in the Marketplace.</span></span> <span data-ttu-id="6d737-151">Si solo es para un Plan (o para unos pocos), se le dará la opción de ofrecer a los usuarios finales más información acerca del servicio con una cantidad relativamente reducida de transacciones al mes.</span><span class="sxs-lookup"><span data-stu-id="6d737-151">If it’s only for one (of few) Plan, the it gives you an option to offer end-users to learn more about your service with a relatively small number of transactions per month.</span></span>  <span data-ttu-id="6d737-152">Si la respuesta es "Sí", no se le harán más preguntas.</span><span class="sxs-lookup"><span data-stu-id="6d737-152">If the answer is "Yes," then no further questions will be asked.</span></span> |

> [!NOTE]
> <span data-ttu-id="6d737-153">Los usuarios finales siempre pueden actualizar a los planes de pago.</span><span class="sxs-lookup"><span data-stu-id="6d737-153">End users can always upgrade to the paid plans.</span></span>
> 
> 

| <span data-ttu-id="6d737-154">Pregunta</span><span class="sxs-lookup"><span data-stu-id="6d737-154">Question</span></span> | <span data-ttu-id="6d737-155">Significado</span><span class="sxs-lookup"><span data-stu-id="6d737-155">Significance</span></span> |
| --- | --- |
| <span data-ttu-id="6d737-156">**¿Hay una versión de evaluación gratuita disponible?**</span><span class="sxs-lookup"><span data-stu-id="6d737-156">**Is free trial available?**</span></span> |<span data-ttu-id="6d737-157">Puede elegir entre "Sin evaluación" o permitir el uso de su Plan durante "Un mes".</span><span class="sxs-lookup"><span data-stu-id="6d737-157">You can choose between “No Trial” at all or give an option to use your Plan for “One Month”.</span></span> <span data-ttu-id="6d737-158">A los publicadores le gusta utilizar esta opción para proporcionar a los usuarios finales la posibilidad de comprender las ventajas de la oferta de forma gratuita durante un mes.</span><span class="sxs-lookup"><span data-stu-id="6d737-158">Publishers like to use this option to provide end-users the possibility to understand the benefits of the offer for free for one month.</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="6d737-159">Los usuarios finales solo podrán adquirir una versión de evaluación gratuita si han configurado un instrumento de pago; por ejemplo, una tarjeta de crédito o un contrato Enterprise.</span><span class="sxs-lookup"><span data-stu-id="6d737-159">End-users will only be able to purchase a free trial if they have established payment instrument e.g. credit card, enterprise agreement.</span></span>
> 
> <span data-ttu-id="6d737-160">Transcurrido un mes tras el comienzo del período de la evaluación gratuita, Azure Marketplace empezará cobrar a los clientes el precio a partir de la fecha de la suscripción, a menos que el cliente inicie la cancelación de la suscripción.</span><span class="sxs-lookup"><span data-stu-id="6d737-160">After one month of the free trial, Azure Marketplace will start charging customers the price as of the date of the subscription, unless the customer initiated the subscription cancellation.</span></span> <span data-ttu-id="6d737-161">Los usuarios finales no recibirán ninguna notificación especial.</span><span class="sxs-lookup"><span data-stu-id="6d737-161">No special notification will be provided to the end-users.</span></span>
> 
> 

| <span data-ttu-id="6d737-162">Pregunta</span><span class="sxs-lookup"><span data-stu-id="6d737-162">Question</span></span> | <span data-ttu-id="6d737-163">Significado</span><span class="sxs-lookup"><span data-stu-id="6d737-163">Significance</span></span> |
| --- | --- |
| <span data-ttu-id="6d737-164">**¿Este plan requiere un código de promoción para comprar?**</span><span class="sxs-lookup"><span data-stu-id="6d737-164">**This plan requires a promotion code to purchase?**</span></span> |<span data-ttu-id="6d737-165">Los publicadores tienen una opción para limitar el acceso a sus Planes del servicio proporcionando un código especial, llamado "Promocode" a clientes específicos.</span><span class="sxs-lookup"><span data-stu-id="6d737-165">Publishers have an option to limit access to their Service Plans by providing a special code, called “A Promocode” to specific customers.</span></span> <span data-ttu-id="6d737-166">Solo los usuarios finales que tendrán este Promocode podrán suscribirse al Plan.</span><span class="sxs-lookup"><span data-stu-id="6d737-166">Only end-users which will have this Promocode will be able to subscribe to the Plan.</span></span> <span data-ttu-id="6d737-167">Si elige "No", acepta que todo el mundo de la región donde está disponible la oferta (vea la [Guía de contenido de marketing de Marketplace](marketplace-publishing-push-to-staging.md) para obtener más detalles) podrá suscribirse a este plan.</span><span class="sxs-lookup"><span data-stu-id="6d737-167">If you choose “No”, then you agree that everyone from the region where the offer is available (See [Marketplace Marketing Content Guide](marketplace-publishing-push-to-staging.md) for more details) will be able to subscribe to this plan.</span></span> <span data-ttu-id="6d737-168">No se le harán más preguntas.</span><span class="sxs-lookup"><span data-stu-id="6d737-168">No further questions will be asked.</span></span> |
| <span data-ttu-id="6d737-169">**¿Ocultar también este plan a cualquier persona que no tenga un código de promoción válido?**</span><span class="sxs-lookup"><span data-stu-id="6d737-169">**Also hide this plan from anyone who doesn’t have a valid promotion code?**</span></span> |<span data-ttu-id="6d737-170">Si la respuesta a la pregunta anterior es "Sí", el Publicador tiene la opción de hacer que este plan no aparezca en ninguna parte de la interfaz de usuario de Marketplace.</span><span class="sxs-lookup"><span data-stu-id="6d737-170">If the answer to the previous question is “Yes” the Publisher has an option to completely remove this plan from appearing in the UI of the Marketplace.</span></span> <span data-ttu-id="6d737-171">Esto implica que los usuarios no verán este plan en la página de detalles de la Oferta.</span><span class="sxs-lookup"><span data-stu-id="6d737-171">It means, customers will not see this plan in the Offer’s details page.</span></span> <span data-ttu-id="6d737-172">Los usuarios finales que reciban un Promocode para adquirirlo, podrán suscribirse a dicho plan utilizando ese código.</span><span class="sxs-lookup"><span data-stu-id="6d737-172">End-users which will receive a promocode to purchase it, will be able to subscribe to it using this promocode.</span></span> |

## <a name="6----create-your-marketplace-marketing-content"></a><span data-ttu-id="6d737-173">6.    Creación de contenido de marketing de Marketplace</span><span class="sxs-lookup"><span data-stu-id="6d737-173">6.    Create your Marketplace marketing content</span></span>
<span data-ttu-id="6d737-174">Para saber cómo proporcionar la información requerida en las pestañas de **marketing, establecimiento de precios, soporte técnico y categorías** , visite la [Guía de contenido de marketing de Marketplace](marketplace-publishing-push-to-staging.md) , que es común para todos los artefactos publicados en Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="6d737-174">For How to provide information required in **Marketing, Pricing, Support and Categories** tabs please visit [Marketplace Marketing Content Guide](marketplace-publishing-push-to-staging.md) which is common to all artifacts published in the Azure Marketplace.</span></span>  

## <a name="7----connect-your-offer-to-your-service-sql-azure-based-or-web-service-based"></a><span data-ttu-id="6d737-175">7.    Conecte la oferta al servicio (basado en SQL Azure o Servicio web).</span><span class="sxs-lookup"><span data-stu-id="6d737-175">7.    Connect your offer to your Service (SQL Azure based or Web Service based).</span></span>
<span data-ttu-id="6d737-176">Haga clic en el submenú **Servicios de datos** .</span><span class="sxs-lookup"><span data-stu-id="6d737-176">Click on the **Data Services** sub-menu.</span></span>

<span data-ttu-id="6d737-177">En la mitad superior de la página, se le pedirá que proporcione el **Espacio de nombres**de la oferta.</span><span class="sxs-lookup"><span data-stu-id="6d737-177">On the upper half of the page you’ll be asked to provide the offer’s **Namespace**.</span></span>  

  ![dibujo](media/marketplace-publishing-data-service-creation/step-7.png)

<span data-ttu-id="6d737-179">La siguiente pregunta definirá cómo expondrá el Publicador la oferta recién creada en Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="6d737-179">The below question will define how the Publisher is going to expose newly created offer to Azure Marketplace.</span></span> <span data-ttu-id="6d737-180">(Para obtener más detalles, consulte la [Guía de requisitos previos técnicos de Servicios de datos](marketplace-publishing-data-service-creation-prerequisites.md)).</span><span class="sxs-lookup"><span data-stu-id="6d737-180">(For more details see the [Data Services Technical Prerequisite Guide](marketplace-publishing-data-service-creation-prerequisites.md)).</span></span>

  ![dibujo](media/marketplace-publishing-data-service-creation/step-7.2.png)

<span data-ttu-id="6d737-182">**Publicación del servicio basado en Base de datos**</span><span class="sxs-lookup"><span data-stu-id="6d737-182">**Publishing the Database based service**</span></span>

<span data-ttu-id="6d737-183">Haga clic en **Base de datos**.</span><span class="sxs-lookup"><span data-stu-id="6d737-183">Click on **Database**.</span></span> <span data-ttu-id="6d737-184">Aparecerá la siguiente página:</span><span class="sxs-lookup"><span data-stu-id="6d737-184">The following page will appear:</span></span>

  ![dibujo](media/marketplace-publishing-data-service-creation/step-7.3.png)

<span data-ttu-id="6d737-186">Para crear una asignación de CSDL para el Conjunto de datos en función de la Base de datos de SQL Azure:</span><span class="sxs-lookup"><span data-stu-id="6d737-186">To create a CSDL mapping for the Dataset based on the SQL Azure DB:</span></span>

  ![dibujo](media/marketplace-publishing-data-service-creation/step-7.4.png)

<span data-ttu-id="6d737-188">Y, a continuación, para cada tabla</span><span class="sxs-lookup"><span data-stu-id="6d737-188">And then for each table</span></span>

  ![dibujo](media/marketplace-publishing-data-service-creation/step-7.5.png)

  ![dibujo](media/marketplace-publishing-data-service-creation/step-7.6.png)

<span data-ttu-id="6d737-191">Si Servicio web</span><span class="sxs-lookup"><span data-stu-id="6d737-191">If Web Service</span></span>

  ![dibujo](media/marketplace-publishing-data-service-creation/step-7.7.png)

> [!IMPORTANT]
> <span data-ttu-id="6d737-193">Lea [Asignación de un servicio web existente a OData mediante CSDL](marketplace-publishing-data-service-creation-odata-mapping.md) para obtener instrucciones detalladas y ejemplos para crear un Servicio web de CSDL.</span><span class="sxs-lookup"><span data-stu-id="6d737-193">Read [Mapping an existing web service to OData through CSDL](marketplace-publishing-data-service-creation-odata-mapping.md) for detailed instructions and examples for creating a CSDL Web Service.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="6d737-194">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6d737-194">Next Steps</span></span>
<span data-ttu-id="6d737-195">Ahora que ha creado la oferta de servicio de datos, asegúrese de completar las instrucciones de la [Guía de contenido de marketing de Marketplace](marketplace-publishing-push-to-staging.md) antes de avanzar a [Prueba del servicio de datos en ensayo](marketplace-publishing-data-service-test-in-staging.md).</span><span class="sxs-lookup"><span data-stu-id="6d737-195">Now that you've created your Data Service offer, please ensure that you complete the instructions in the [Marketplace Marketing Content Guide](marketplace-publishing-push-to-staging.md) before you move forward to [Testing your Data Service in Staging](marketplace-publishing-data-service-test-in-staging.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="6d737-196">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="6d737-196">See Also</span></span>
* [<span data-ttu-id="6d737-197">Introducción: cómo publicar una oferta en Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="6d737-197">Getting Started: How to publish an offer to the Azure Marketplace</span></span>](marketplace-publishing-getting-started.md)
* <span data-ttu-id="6d737-198">Si le interesa entender el proceso de asignación de OData y el propósito general, lea este artículo sobre [Asignación de OData del servicio de datos](marketplace-publishing-data-service-creation-odata-mapping.md) para revisar las definiciones, las estructuras y las instrucciones.</span><span class="sxs-lookup"><span data-stu-id="6d737-198">If you are interested in understanding the overall OData mapping process and purpose, read this article [Data Service OData Mapping](marketplace-publishing-data-service-creation-odata-mapping.md) to review definitions, structures, and instructions.</span></span>
* <span data-ttu-id="6d737-199">Si está interesado en aprender y comprender los nodos específicos y sus parámetros, lea este artículo sobre [Nodos de asignación de OData del servicio de datos](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) para ver definiciones y explicaciones, ejemplos y contexto de caso de uso.</span><span class="sxs-lookup"><span data-stu-id="6d737-199">If you are interested in learning and understanding the specific nodes and their parameters, read this article [Data Service OData Mapping Nodes](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) for definitions and explanations, examples, and use case context.</span></span>
* <span data-ttu-id="6d737-200">Si está interesado en revisar ejemplos, lea este artículo sobre [Ejemplos de asignación de OData del servicio de datos](marketplace-publishing-data-service-creation-odata-mapping-examples.md) para ver ejemplos de código y comprender el contexto y la sintaxis del código.</span><span class="sxs-lookup"><span data-stu-id="6d737-200">If you are interested in reviewing examples, read this article [Data Service OData Mapping Examples](marketplace-publishing-data-service-creation-odata-mapping-examples.md) to see sample code and understand code syntax and context.</span></span>

[link-pubportal]:https://publish.windowsazure.com
