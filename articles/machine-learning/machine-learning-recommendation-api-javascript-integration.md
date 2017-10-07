---
title: "Recomendaciones de Machine Learning: integración con JavaScript | Microsoft Docs"
description: "Recomendaciones de Azure Machine Learning: integración con JavaScript (documentación)"
services: machine-learning
documentationcenter: 
author: LuisCabrer
manager: jhubbard
editor: cgronlun
ms.assetid: bbbb5bb6-489d-4a62-a2ae-f36237e9e2e1
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 03/31/2017
ms.author: luisca
ROBOTS: NOINDEX
redirect_url: machine-learning-datamarket-deprecation
redirect_document_id: True
ms.openlocfilehash: 4c5f0eee4aa04ce823321d52985374c52850f0d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-machine-learning-recommendations---javascript-integration"></a><span data-ttu-id="047fb-103">Recomendaciones de Aprendizaje automático de Azure: Integración con JavaScript</span><span class="sxs-lookup"><span data-stu-id="047fb-103">Azure Machine Learning Recommendations - JavaScript Integration</span></span>
> [!NOTE]
> <span data-ttu-id="047fb-104">Debería empezar a usar Hola recomendaciones API cognitivos servicio en lugar de esta versión.</span><span class="sxs-lookup"><span data-stu-id="047fb-104">You should start using hello Recommendations API Cognitive Service instead of this version.</span></span> <span data-ttu-id="047fb-105">Hola recomendaciones cognitivos servicio va a sustituir este servicio y todas las características nuevas de Hola se van a desarrollar no existe.</span><span class="sxs-lookup"><span data-stu-id="047fb-105">hello Recommendations Cognitive Service will be replacing this service, and all hello new features will be developed there.</span></span> <span data-ttu-id="047fb-106">Tiene nuevas funcionalidades como compatibilidad con procesamientos por lotes, un explorador de API más eficaz, una interfaz de API más limpia, una experiencia de facturación y suscripción más coherente, etc.</span><span class="sxs-lookup"><span data-stu-id="047fb-106">It has new capabilities like batching support, a better API Explorer, a cleaner API surface, more consistent signup/billing experience, etc.</span></span>
> <span data-ttu-id="047fb-107">Obtenga más información sobre [migrar toohello nuevo servicio cognitivos](http://aka.ms/recomigrate)</span><span class="sxs-lookup"><span data-stu-id="047fb-107">Learn more about [Migrating toohello new Cognitive Service](http://aka.ms/recomigrate)</span></span>
> 
> 

<span data-ttu-id="047fb-108">Este documento describir cómo toointegrate su sitio mediante JavaScript.</span><span class="sxs-lookup"><span data-stu-id="047fb-108">This document depict how toointegrate your site using JavaScript.</span></span> <span data-ttu-id="047fb-109">Hola JavaScript permite toosend eventos de adquisición de datos y las recomendaciones de tooconsume una vez que se genera un modelo de recomendación.</span><span class="sxs-lookup"><span data-stu-id="047fb-109">hello JavaScript enables you toosend Data Acquisition events and tooconsume recommendations once you build a recommendation model.</span></span> <span data-ttu-id="047fb-110">Todas las operaciones que se realizan a través de JS se pueden realizar también desde el servidor.</span><span class="sxs-lookup"><span data-stu-id="047fb-110">All operations done via JS can be also done from server side.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="1-general-overview"></a><span data-ttu-id="047fb-111">1. Información general</span><span class="sxs-lookup"><span data-stu-id="047fb-111">1. General Overview</span></span>
<span data-ttu-id="047fb-112">La integración de su sitio con recomendaciones de Aprendizaje automático de Azure consta de 2 fases:</span><span class="sxs-lookup"><span data-stu-id="047fb-112">Integrating your site with Azure ML Recommendations consist on 2 Phases:</span></span>

1. <span data-ttu-id="047fb-113">Enviar eventos a las recomendaciones de Aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="047fb-113">Send Events into Azure ML Recommendations.</span></span> <span data-ttu-id="047fb-114">Esto le permitirá toobuild un modelo de recomendación.</span><span class="sxs-lookup"><span data-stu-id="047fb-114">This will enable toobuild a recommendation model.</span></span>
2. <span data-ttu-id="047fb-115">Utilizar las recomendaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="047fb-115">Consume hello recommendations.</span></span> <span data-ttu-id="047fb-116">Después de que se crea el modelo de hello pueden consumir las recomendaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="047fb-116">After hello model is built you can consume hello recommendations.</span></span> <span data-ttu-id="047fb-117">(Este documento no explica cómo toobuild un modelo, leer Hola tooget de guía de inicio rápido para obtener más información acerca de cómo).</span><span class="sxs-lookup"><span data-stu-id="047fb-117">(This document does not explain how toobuild a model, read hello quick start guide tooget more information on how).</span></span>

<span data-ttu-id="047fb-118"><ins>Fase I</ins></span><span class="sxs-lookup"><span data-stu-id="047fb-118"><ins>Phase I</ins></span></span>

<span data-ttu-id="047fb-119">Hola primera fase que se inserta en las páginas html de una pequeña biblioteca de JavaScript que permite Hola eventos toosend de página cuando se producen en la página html hello en servidores de recomendaciones de aprendizaje automático de Azure (a través del mercado de datos):</span><span class="sxs-lookup"><span data-stu-id="047fb-119">In hello first phase you insert into your html pages a small JavaScript library that enables hello page toosend events as they occur on hello html page into Azure ML Recommendations servers (via Data Market):</span></span>

![Dibujo1][1]

<span data-ttu-id="047fb-121"><ins>Fase II</ins></span><span class="sxs-lookup"><span data-stu-id="047fb-121"><ins>Phase II</ins></span></span>

<span data-ttu-id="047fb-122">Hola segunda fase cuando desee tooshow recomendaciones de hello en página Hola selecciona una de hello siguientes opciones:</span><span class="sxs-lookup"><span data-stu-id="047fb-122">In hello second phase when you want tooshow hello recommendations on hello page you select one of hello following options:</span></span>

<span data-ttu-id="047fb-123">1. el servidor (en la fase de hello de la representación de página) llama a las recomendaciones de tooget de servidor de recomendaciones de aprendizaje automático de Azure (a través de mercado de datos).</span><span class="sxs-lookup"><span data-stu-id="047fb-123">1.Your server (on hello phase of page rendering) calls Azure ML Recommendations Server (via Data Market) tooget recommendations.</span></span> <span data-ttu-id="047fb-124">resultados de Hello incluyen una lista de Id. de elementos. El servidor necesita resultados de hello tooenrich con hello los elementos de metadatos (por ejemplo, imágenes, descripción) y enviar Hola creado página toohello explorador.</span><span class="sxs-lookup"><span data-stu-id="047fb-124">hello results include a list of items id. Your server needs tooenrich hello results with hello items Meta data (e.g. images, description) and send hello created page toohello browser.</span></span>

![Dibujo2][2]

<span data-ttu-id="047fb-126">2. hello otra opción es archivo JavaScript toouse Hola pequeño de fase uno tooget una simple lista de elementos recomendados.</span><span class="sxs-lookup"><span data-stu-id="047fb-126">2.hello other option is toouse hello small JavaScript file from phase one tooget a simple list of recommended items.</span></span> <span data-ttu-id="047fb-127">datos de Hello recibidos aquí están más simple de hello en la primera opción de Hola.</span><span class="sxs-lookup"><span data-stu-id="047fb-127">hello data received here is leaner than hello one in hello first option.</span></span>

![Dibujo3][3]

## <a name="2-prerequisites"></a><span data-ttu-id="047fb-129">2. Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="047fb-129">2. Prerequisites</span></span>
1. <span data-ttu-id="047fb-130">Crear un modelo nuevo mediante las API de Hola.</span><span class="sxs-lookup"><span data-stu-id="047fb-130">Create a new model using hello APIs.</span></span> <span data-ttu-id="047fb-131">Consulte la Guía de inicio rápido de hello acerca de cómo toodo lo.</span><span class="sxs-lookup"><span data-stu-id="047fb-131">See hello Quick start guide on how toodo it.</span></span>
2. <span data-ttu-id="047fb-132">Codifique &lt;dataMarketUser&gt;:&lt;dataMarketKey&gt; mediante base64.</span><span class="sxs-lookup"><span data-stu-id="047fb-132">Encode your &lt;dataMarketUser&gt;:&lt;dataMarketKey&gt; with base64.</span></span> <span data-ttu-id="047fb-133">(Esto se usará para hello autenticación básica tooenable Hola JS código toocall Hola API).</span><span class="sxs-lookup"><span data-stu-id="047fb-133">(This will be used for hello basic authentication tooenable hello JS code toocall hello APIs).</span></span>

## <a name="3-send-data-acquisition-events-using-javascript"></a><span data-ttu-id="047fb-134">3. Envíe eventos de adquisición de datos con JavaScript.</span><span class="sxs-lookup"><span data-stu-id="047fb-134">3. Send Data Acquisition events using JavaScript</span></span>
<span data-ttu-id="047fb-135">Hola pasos facilitar enviar eventos:</span><span class="sxs-lookup"><span data-stu-id="047fb-135">hello following steps facilitate sending events:</span></span>

1. <span data-ttu-id="047fb-136">Incluya la biblioteca de JQuery en su código.</span><span class="sxs-lookup"><span data-stu-id="047fb-136">Include JQuery library in your code.</span></span> <span data-ttu-id="047fb-137">Puede descargarlo de nuget en hello después de la dirección URL.</span><span class="sxs-lookup"><span data-stu-id="047fb-137">You can download it from nuget in hello following URL.</span></span>
   
     <span data-ttu-id="047fb-138">http://www.nuget.org/packages/jQuery/1.8.2</span><span class="sxs-lookup"><span data-stu-id="047fb-138">http://www.nuget.org/packages/jQuery/1.8.2</span></span>
2. <span data-ttu-id="047fb-139">Incluir Hola biblioteca de secuencia de comandos de Java de recomendaciones de hello después de la dirección URL: http://aka.ms/RecoJSLib1</span><span class="sxs-lookup"><span data-stu-id="047fb-139">Include hello Recommendations Java Script library from hello following URL: http://aka.ms/RecoJSLib1</span></span>
3. <span data-ttu-id="047fb-140">Inicializar la biblioteca de recomendaciones de aprendizaje automático de Azure con los parámetros adecuados de Hola.</span><span class="sxs-lookup"><span data-stu-id="047fb-140">Initialize Azure ML Recommendations library with hello appropriate parameters.</span></span>
   
     <span data-ttu-id="047fb-141"><script>AzureMLRecommendationsStart ("<base64encoding of username:key>", "< model_id >"); </script> 
4. Eventos de envío Hola apropiado.</span><span class="sxs-lookup"><span data-stu-id="047fb-141"><script> AzureMLRecommendationsStart("<base64encoding of username:key>", "<model_id>"); </script>
4. Send hello appropriate event.</span></span> <span data-ttu-id="047fb-142">Consulte la sección detallada a continuación respecto a todos los tipos de eventos (ejemplo de evento de clic)  <script> if (typeof AzureMLRecommendationsEvent=="undefined") {</span><span class="sxs-lookup"><span data-stu-id="047fb-142">See detailed section below on all type of events (example of click event)  <script> if (typeof AzureMLRecommendationsEvent=="undefined") {</span></span>         
                     <span data-ttu-id="047fb-143">AzureMLRecommendationsEvent = []; } AzureMLRecommendationsEvent.push({ event: "click", item: "18321116" }); </script></span><span class="sxs-lookup"><span data-stu-id="047fb-143">AzureMLRecommendationsEvent = []; } AzureMLRecommendationsEvent.push({ event: "click", item: "18321116" }); </script></span></span>

### <a name="31----limitations-and-browser-support"></a><span data-ttu-id="047fb-144">3.1.</span><span class="sxs-lookup"><span data-stu-id="047fb-144">3.1.</span></span>    <span data-ttu-id="047fb-145">Limitaciones y compatibilidad con exploradores</span><span class="sxs-lookup"><span data-stu-id="047fb-145">Limitations and Browser Support</span></span>
<span data-ttu-id="047fb-146">Esta es una implementación de referencia y se proporciona tal cual.</span><span class="sxs-lookup"><span data-stu-id="047fb-146">This is a reference implementation and it is given as is.</span></span> <span data-ttu-id="047fb-147">Debe admitir todos los exploradores principales.</span><span class="sxs-lookup"><span data-stu-id="047fb-147">It should support all major browsers.</span></span>

### <a name="32----type-of-events"></a><span data-ttu-id="047fb-148">3.2.</span><span class="sxs-lookup"><span data-stu-id="047fb-148">3.2.</span></span>    <span data-ttu-id="047fb-149">Tipos de eventos</span><span class="sxs-lookup"><span data-stu-id="047fb-149">Type of Events</span></span>
<span data-ttu-id="047fb-150">Hay 5 tipos de eventos que admite la biblioteca de Hola: haga clic en, haga clic en la recomendación, agregar tooShop carro, quitar de carro de la tienda y compra.</span><span class="sxs-lookup"><span data-stu-id="047fb-150">There are 5 types of event that hello library supports: Click, Recommendation Click, Add tooShop Cart, Remove from Shop Cart and Purchase.</span></span> <span data-ttu-id="047fb-151">Hay un evento adicional que es el contexto de usuario de Hola tooset utilizados llamado inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="047fb-151">There is an additional event that is used tooset hello user context called Login.</span></span>

#### <a name="321-click-event"></a><span data-ttu-id="047fb-152">3.2.1.</span><span class="sxs-lookup"><span data-stu-id="047fb-152">3.2.1.</span></span> <span data-ttu-id="047fb-153">Evento de clic</span><span class="sxs-lookup"><span data-stu-id="047fb-153">Click Event</span></span>
<span data-ttu-id="047fb-154">Este evento se debe utilizar cada vez que un usuario hace clic en un elemento.</span><span class="sxs-lookup"><span data-stu-id="047fb-154">This event should be used any time a user clicked on an item.</span></span> <span data-ttu-id="047fb-155">Normalmente cuando el usuario hace clic en un elemento se abre una nueva página en los detalles de artículo de hello; en esta página debe activarse este evento.</span><span class="sxs-lookup"><span data-stu-id="047fb-155">Usually when user clicks on an item a new page is opened with hello item details; in this page this event should be triggered.</span></span>

<span data-ttu-id="047fb-156">Parámetros:</span><span class="sxs-lookup"><span data-stu-id="047fb-156">Parameters:</span></span>

* <span data-ttu-id="047fb-157">event (cadena, obligatorio) - “click”</span><span class="sxs-lookup"><span data-stu-id="047fb-157">event (string, mandatory) - “click”</span></span>
* <span data-ttu-id="047fb-158">elemento (string, obligatorio): identificador único del elemento de Hola</span><span class="sxs-lookup"><span data-stu-id="047fb-158">item (string, mandatory) - Unique identifier of hello item</span></span>
* <span data-ttu-id="047fb-159">itemName (cadena, opcional) nombre de Hola de elemento de Hola</span><span class="sxs-lookup"><span data-stu-id="047fb-159">itemName (string, optional) - hello name of hello item</span></span>
* <span data-ttu-id="047fb-160">Descripción de producto (string, opcional): descripción de Hola de elemento de Hola</span><span class="sxs-lookup"><span data-stu-id="047fb-160">itemDescription (string, optional) - hello description of hello item</span></span>
* <span data-ttu-id="047fb-161">itemCategory (cadena, opcional) categoría de Hola de elemento de Hola</span><span class="sxs-lookup"><span data-stu-id="047fb-161">itemCategory (string, optional) - hello category of hello item</span></span>
  
        <script>
            if (typeof AzureMLRecommendationsEvent == "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: "click", item: "3111718" });
        </script>

<span data-ttu-id="047fb-162">O con datos opcionales:</span><span class="sxs-lookup"><span data-stu-id="047fb-162">Or with optional data:</span></span>

        <script>
            if (typeof AzureMLRecommendationsEvent === "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "click", item: "3111718", itemName: "Plane", itemDescription: "It is a big plane", itemCategory: "Aviation"});
        </script>


#### <a name="322-recommendation-click-event"></a><span data-ttu-id="047fb-163">3.2.2.</span><span class="sxs-lookup"><span data-stu-id="047fb-163">3.2.2.</span></span> <span data-ttu-id="047fb-164">Ejemplo de Recommendation Click:</span><span class="sxs-lookup"><span data-stu-id="047fb-164">Recommendation Click Event</span></span>
<span data-ttu-id="047fb-165">Este evento se debe utilizar cada vez que un usuario hace clic en un elemento que se recibió de las recomendaciones de Aprendizaje automático de Azure como un elemento recomendado.</span><span class="sxs-lookup"><span data-stu-id="047fb-165">This event should be used any time a user clicked on an item that was received from Azure ML Recommendations as a recommended item.</span></span> <span data-ttu-id="047fb-166">Normalmente cuando el usuario hace clic en un elemento se abre una nueva página en los detalles de artículo de hello; en esta página debe activarse este evento.</span><span class="sxs-lookup"><span data-stu-id="047fb-166">Usually when user clicks on an item a new page is opened with hello item details; in this page this event should be triggered.</span></span>

<span data-ttu-id="047fb-167">Parámetros:</span><span class="sxs-lookup"><span data-stu-id="047fb-167">Parameters:</span></span>

* <span data-ttu-id="047fb-168">event (cadena, obligatorio) - “recommendationclick”</span><span class="sxs-lookup"><span data-stu-id="047fb-168">event (string, mandatory) - “recommendationclick”</span></span>
* <span data-ttu-id="047fb-169">elemento (string, obligatorio): identificador único del elemento de Hola</span><span class="sxs-lookup"><span data-stu-id="047fb-169">item (string, mandatory) - Unique identifier of hello item</span></span>
* <span data-ttu-id="047fb-170">itemName (cadena, opcional) nombre de Hola de elemento de Hola</span><span class="sxs-lookup"><span data-stu-id="047fb-170">itemName (string, optional) - hello name of hello item</span></span>
* <span data-ttu-id="047fb-171">Descripción de producto (string, opcional): descripción de Hola de elemento de Hola</span><span class="sxs-lookup"><span data-stu-id="047fb-171">itemDescription (string, optional) - hello description of hello item</span></span>
* <span data-ttu-id="047fb-172">itemCategory (cadena, opcional) categoría de Hola de elemento de Hola</span><span class="sxs-lookup"><span data-stu-id="047fb-172">itemCategory (string, optional) - hello category of hello item</span></span>
* <span data-ttu-id="047fb-173">valores de inicialización (matriz de cadenas, opcional) - Hola inicializaciones que genera la consulta de la recomendación de Hola.</span><span class="sxs-lookup"><span data-stu-id="047fb-173">seeds (string array, optional) - hello seeds that generated hello recommendation query.</span></span>
* <span data-ttu-id="047fb-174">recoList (matriz de cadenas, opcional) - Hola resultado de solicitud de recomendación de Hola que generó el elemento de Hola que se hizo clic.</span><span class="sxs-lookup"><span data-stu-id="047fb-174">recoList (string array, optional) - hello result of hello recommendation request that generated hello item that was clicked.</span></span>
  
        <script>
            if (typeof AzureMLRecommendationsEvent=="undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "recommendationclick", item: "18899918" });
        </script>

<span data-ttu-id="047fb-175">O con datos opcionales:</span><span class="sxs-lookup"><span data-stu-id="047fb-175">Or with optional data:</span></span>

        <script>
            if (typeof AzureMLRecommendationsEvent == "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: eventName, item: "198", itemName: "Plane2", itemDescription: "It is a big plane2", itemCategory: "Default2", seeds: ["Seed1", "Seed2"], recoList: ["199", "198", "197"]                 });
        </script>


#### <a name="323-add-shopping-cart-event"></a><span data-ttu-id="047fb-176">3.2.3.</span><span class="sxs-lookup"><span data-stu-id="047fb-176">3.2.3.</span></span> <span data-ttu-id="047fb-177">Agregar eventos de carro de la compra</span><span class="sxs-lookup"><span data-stu-id="047fb-177">Add Shopping Cart Event</span></span>
<span data-ttu-id="047fb-178">Este evento debe usarse cuando el usuario de hello agrega un toohello elemento carro de la compra.</span><span class="sxs-lookup"><span data-stu-id="047fb-178">This event should be used when hello user add an item toohello shopping cart.</span></span>
<span data-ttu-id="047fb-179">Parámetros:</span><span class="sxs-lookup"><span data-stu-id="047fb-179">Parameters:</span></span>

* <span data-ttu-id="047fb-180">event (cadena, obligatorio) - "addshopcart"</span><span class="sxs-lookup"><span data-stu-id="047fb-180">event (string, mandatory) - “addshopcart”</span></span>
* <span data-ttu-id="047fb-181">elemento (string, obligatorio): identificador único del elemento de Hola</span><span class="sxs-lookup"><span data-stu-id="047fb-181">item (string, mandatory) - Unique identifier of hello item</span></span>
* <span data-ttu-id="047fb-182">itemName (cadena, opcional) nombre de Hola de elemento de Hola</span><span class="sxs-lookup"><span data-stu-id="047fb-182">itemName (string, optional) - hello name of hello item</span></span>
* <span data-ttu-id="047fb-183">Descripción de producto (string, opcional): descripción de Hola de elemento de Hola</span><span class="sxs-lookup"><span data-stu-id="047fb-183">itemDescription (string, optional) - hello description of hello item</span></span>
* <span data-ttu-id="047fb-184">itemCategory (cadena, opcional) categoría de Hola de elemento de Hola</span><span class="sxs-lookup"><span data-stu-id="047fb-184">itemCategory (string, optional) - hello category of hello item</span></span>
  
        <script>
            if (typeof AzureMLRecommendationsEvent == "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "addshopcart", item: "13221118" });
        </script>

#### <a name="324-remove-shopping-cart-event"></a><span data-ttu-id="047fb-185">3.2.4.</span><span class="sxs-lookup"><span data-stu-id="047fb-185">3.2.4.</span></span> <span data-ttu-id="047fb-186">Quitar eventos de carro de la compra</span><span class="sxs-lookup"><span data-stu-id="047fb-186">Remove Shopping Cart Event</span></span>
<span data-ttu-id="047fb-187">Este evento debe usarse cuando el usuario de hello quita un carro de la compra toohello elemento.</span><span class="sxs-lookup"><span data-stu-id="047fb-187">This event should be used when hello user removes an item toohello shopping cart.</span></span>

<span data-ttu-id="047fb-188">Parámetros:</span><span class="sxs-lookup"><span data-stu-id="047fb-188">Parameters:</span></span>

* <span data-ttu-id="047fb-189">event (cadena, obligatorio) - "removeshopcart"</span><span class="sxs-lookup"><span data-stu-id="047fb-189">event (string, mandatory) - “removeshopcart”</span></span>
* <span data-ttu-id="047fb-190">elemento (string, obligatorio): identificador único del elemento de Hola</span><span class="sxs-lookup"><span data-stu-id="047fb-190">item (string, mandatory) - Unique identifier of hello item</span></span>
* <span data-ttu-id="047fb-191">itemName (cadena, opcional) nombre de Hola de elemento de Hola</span><span class="sxs-lookup"><span data-stu-id="047fb-191">itemName (string, optional) - hello name of hello item</span></span>
* <span data-ttu-id="047fb-192">Descripción de producto (string, opcional): descripción de Hola de elemento de Hola</span><span class="sxs-lookup"><span data-stu-id="047fb-192">itemDescription (string, optional) - hello description of hello item</span></span>
* <span data-ttu-id="047fb-193">itemCategory (cadena, opcional) categoría de Hola de elemento de Hola</span><span class="sxs-lookup"><span data-stu-id="047fb-193">itemCategory (string, optional) - hello category of hello item</span></span>
  
        <script>
            if (typeof AzureMLRecommendationsEvent=="undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: "removeshopcart", item: "111118" });
        </script>

#### <a name="325-purchase-event"></a><span data-ttu-id="047fb-194">3.2.5.</span><span class="sxs-lookup"><span data-stu-id="047fb-194">3.2.5.</span></span> <span data-ttu-id="047fb-195">Evento de compra</span><span class="sxs-lookup"><span data-stu-id="047fb-195">Purchase Event</span></span>
<span data-ttu-id="047fb-196">Este evento debe usarse cuando el usuario de hello adquirió su carro de la compra.</span><span class="sxs-lookup"><span data-stu-id="047fb-196">This event should be used when hello user purchased his shopping cart.</span></span>

<span data-ttu-id="047fb-197">Parámetros:</span><span class="sxs-lookup"><span data-stu-id="047fb-197">Parameters:</span></span>

* <span data-ttu-id="047fb-198">event (cadena) - "purchase"</span><span class="sxs-lookup"><span data-stu-id="047fb-198">event (string) - “purchase”</span></span>
* <span data-ttu-id="047fb-199">items ( Purchased[] ) - Matriz con una entrada por cada elemento comprado.</span><span class="sxs-lookup"><span data-stu-id="047fb-199">items ( Purchased[] ) - Array holding an entry for each item purchased.</span></span><br><br>
  <span data-ttu-id="047fb-200">Formato de elemento comprado:</span><span class="sxs-lookup"><span data-stu-id="047fb-200">Purchased format:</span></span>
  * <span data-ttu-id="047fb-201">elemento (cadena): identificador único del elemento de Hola.</span><span class="sxs-lookup"><span data-stu-id="047fb-201">item (string) - Unique identifier of hello item.</span></span>
  * <span data-ttu-id="047fb-202">count (entero o cadena) - Número de elementos que se compraron.</span><span class="sxs-lookup"><span data-stu-id="047fb-202">count (int or string) - number of items that were purchased.</span></span>
  * <span data-ttu-id="047fb-203">precio (float o cadena) - field opcional: Hola precio del elemento de Hola.</span><span class="sxs-lookup"><span data-stu-id="047fb-203">price (float or string) - optional field - hello price of hello item.</span></span>

<span data-ttu-id="047fb-204">ejemplo de Hola siguiente muestra la compra de 3 elementos (33, 34, 35), dos con todos los campos rellena (elemento, recuento, precio) y otra (elemento 34) sin un precio.</span><span class="sxs-lookup"><span data-stu-id="047fb-204">hello example below shows purchase of 3 items (33, 34, 35), two with all fields populated (item, count, price) and one (item 34) without a price.</span></span>

        <script>
            if ( typeof AzureMLRecommendationsEvent == "undefined"){ AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: "purchase", items: [{ item: "33", count: "1", price: "10" }, { item: "34", count: "2" }, { item: "35", count: "1", price: "210" }] });
        </script>

#### <a name="326-user-login-event"></a><span data-ttu-id="047fb-205">3.2.6.</span><span class="sxs-lookup"><span data-stu-id="047fb-205">3.2.6.</span></span> <span data-ttu-id="047fb-206">Evento de inicio de sesión de usuario</span><span class="sxs-lookup"><span data-stu-id="047fb-206">User Login Event</span></span>
<span data-ttu-id="047fb-207">Azure evento de recomendaciones de aprendizaje automático biblioteca crea y utiliza una cookie en los eventos de tooidentify de orden que proviene de Hola mismo explorador.</span><span class="sxs-lookup"><span data-stu-id="047fb-207">Azure ML Recommendations Event library creates and use a cookie in order tooidentify events that came from hello same browser.</span></span> <span data-ttu-id="047fb-208">Modelo de orden tooimprove Hola recomendaciones de aprendizaje automático de Azure de resultados permite tooset una identificación única de usuario que reemplazará el uso de cookies de Hola.</span><span class="sxs-lookup"><span data-stu-id="047fb-208">In order tooimprove hello model results Azure ML Recommendations enables tooset a user unique identification that will override hello cookie usage.</span></span>

<span data-ttu-id="047fb-209">Este evento se debe utilizar después el sitio de tooyour de inicio de sesión de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="047fb-209">This event should be used after hello user login tooyour site.</span></span>

<span data-ttu-id="047fb-210">Parámetros:</span><span class="sxs-lookup"><span data-stu-id="047fb-210">Parameters:</span></span>

* <span data-ttu-id="047fb-211">event (cadena) - "userlogin"</span><span class="sxs-lookup"><span data-stu-id="047fb-211">event (string) - “userlogin”</span></span>
* <span data-ttu-id="047fb-212">usuario (cadena) de identificación único del usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="047fb-212">user (string) - unique identification of hello user.</span></span>
  
        <script>
            if (typeof AzureMLRecommendationsEvent=="undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "userlogin", user: “ABCD10AA” });
        </script>

## <a name="4-consume-recommendations-via-javascript"></a><span data-ttu-id="047fb-213">4. Consumir recomendaciones a través de JavaScript</span><span class="sxs-lookup"><span data-stu-id="047fb-213">4. Consume Recommendations via JavaScript</span></span>
<span data-ttu-id="047fb-214">página Web del cliente de hello desencadenan código de Hello que consume la recomendación de Hola por algunos eventos de JavaScript.</span><span class="sxs-lookup"><span data-stu-id="047fb-214">hello code that consumes hello recommendation is triggered by some JavaScript event by hello client’s webpage.</span></span> <span data-ttu-id="047fb-215">respuesta de la recomendación de Hello incluye Hola recomendadas identificadores de elementos, sus nombres y sus clasificaciones.</span><span class="sxs-lookup"><span data-stu-id="047fb-215">hello recommendation response includes hello recommended items Ids, their names and their ratings.</span></span> <span data-ttu-id="047fb-216">Es mejor toouse esta opción solo para una visualización de la lista de hello recomendada elementos - más complejos de control (por ejemplo, para agregar metadatos de elemento de Hola) se debe realizar en la integración del lado servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="047fb-216">It’s best toouse this option only for a list display of hello recommended items - more complex handling (such as adding hello item’s metadata) should be done on hello server side integration.</span></span>

### <a name="41-consume-recommendations"></a><span data-ttu-id="047fb-217">4.1 Recomendaciones de uso</span><span class="sxs-lookup"><span data-stu-id="047fb-217">4.1 Consume Recommendations</span></span>
<span data-ttu-id="047fb-218">recomendaciones de tooconsume que necesita tooinclude Hola requiere bibliotecas de JavaScript en la página y toocall AzureMLRecommendationsStart.</span><span class="sxs-lookup"><span data-stu-id="047fb-218">tooconsume recommendations you need tooinclude hello required JavaScript libraries in your page and toocall AzureMLRecommendationsStart.</span></span> <span data-ttu-id="047fb-219">Consulte la sección 2.</span><span class="sxs-lookup"><span data-stu-id="047fb-219">See section 2.</span></span>

<span data-ttu-id="047fb-220">recomendaciones de tooconsume para uno o más elementos necesita toocall llama a un método: AzureMLRecommendationsGetI2IRecommendation.</span><span class="sxs-lookup"><span data-stu-id="047fb-220">tooconsume recommendations for one or more items you need toocall a method called: AzureMLRecommendationsGetI2IRecommendation.</span></span>

<span data-ttu-id="047fb-221">Parámetros:</span><span class="sxs-lookup"><span data-stu-id="047fb-221">Parameters:</span></span>

* <span data-ttu-id="047fb-222">Una o más elementos tooget recomendaciones para los elementos (matriz de cadenas).</span><span class="sxs-lookup"><span data-stu-id="047fb-222">items (array of strings) - One or more items tooget recommendations for.</span></span> <span data-ttu-id="047fb-223">Si consume una compilación Fbt, aquí solo puede establecer un elemento.</span><span class="sxs-lookup"><span data-stu-id="047fb-223">If you consume an Fbt build then you can set here only one item.</span></span>
* <span data-ttu-id="047fb-224">numberOfResults (entero) - Número de resultados requeridos.</span><span class="sxs-lookup"><span data-stu-id="047fb-224">numberOfResults (int) - number of required results.</span></span>
* <span data-ttu-id="047fb-225">includeMetadata (un valor booleano, opcional) - si establece too'true' indica que se debe rellenar ese campo de metadatos de hello en el resultado de hello.</span><span class="sxs-lookup"><span data-stu-id="047fb-225">includeMetadata (boolean, optional) - if set too‘true’ indicates that hello metadata field must be populated in hello result.</span></span>
* <span data-ttu-id="047fb-226">Devuelve la función: una función que controlará las recomendaciones de Hola de procesamiento.</span><span class="sxs-lookup"><span data-stu-id="047fb-226">Processing function - a function that will handle hello recommendations returned.</span></span> <span data-ttu-id="047fb-227">Hola datos se devuelven como una matriz de:</span><span class="sxs-lookup"><span data-stu-id="047fb-227">hello data is returned as an array of:</span></span>
  * <span data-ttu-id="047fb-228">item - Identificador único del elemento</span><span class="sxs-lookup"><span data-stu-id="047fb-228">Item - item unique id</span></span>
  * <span data-ttu-id="047fb-229">name - Nombre del elemento (si existe en el catálogo)</span><span class="sxs-lookup"><span data-stu-id="047fb-229">name - item name (if exist in catalog)</span></span>
  * <span data-ttu-id="047fb-230">rating - Clasificación de recomendación</span><span class="sxs-lookup"><span data-stu-id="047fb-230">rating - recommendation rating</span></span>
  * <span data-ttu-id="047fb-231">metadatos: una cadena que representa los metadatos de Hola de elemento de Hola</span><span class="sxs-lookup"><span data-stu-id="047fb-231">metadata - a string that represents hello metadata of hello item</span></span>

<span data-ttu-id="047fb-232">Ejemplo: Hola después el código solicita 8 recomendaciones para el elemento "64f6eb0d-947a-4c18-a16c-888da9e228ba" (y especificando no includeMetadata - implícitamente dice que no hay metadatos están necesario),, a continuación, concatenar los resultados de hello en un búfer.</span><span class="sxs-lookup"><span data-stu-id="047fb-232">Example: hello following code requests 8 recommendations for item "64f6eb0d-947a-4c18-a16c-888da9e228ba" (and by not specifying includeMetadata - it implicitly says that no metadata is required), it then concatenate hello results into a buffer.</span></span>

        <script>
             var reco = AzureMLRecommendationsGetI2IRecommendation(["64f6eb0d-947a-4c18-a16c-888da9e228ba"], 8, false, function (reco) {
                 var buff = "";
                 for (var ii = 0; ii < reco.length; ii++) {
                       buff += reco[ii].item + "," + reco[ii].name + "," + reco[ii].rating + "\n";
                 }
                 alert(buff);
            });
        </script>


[1]: ./media/machine-learning-recommendation-api-javascript-integration/Drawing1.png
[2]: ./media/machine-learning-recommendation-api-javascript-integration/Drawing2.png
[3]: ./media/machine-learning-recommendation-api-javascript-integration/Drawing3.png
