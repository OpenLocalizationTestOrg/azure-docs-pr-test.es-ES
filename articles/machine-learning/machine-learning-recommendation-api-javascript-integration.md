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
redirect_document_id: TRUE
ms.openlocfilehash: 8f27962d097bffc2a03de80244ae41d6573a4bf3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="azure-machine-learning-recommendations---javascript-integration"></a><span data-ttu-id="ef466-103">Recomendaciones de Aprendizaje automático de Azure: Integración con JavaScript</span><span class="sxs-lookup"><span data-stu-id="ef466-103">Azure Machine Learning Recommendations - JavaScript Integration</span></span>
> [!NOTE]
> <span data-ttu-id="ef466-104">Debe empezar a utilizar el servicio Cognitive Services de la API de Recomendaciones en lugar de esta versión.</span><span class="sxs-lookup"><span data-stu-id="ef466-104">You should start using the Recommendations API Cognitive Service instead of this version.</span></span> <span data-ttu-id="ef466-105">El servicio Cognitive Services de Recomendaciones va a sustituir a este servicio y todas las características nuevas se desarrollarán en esta nueva versión.</span><span class="sxs-lookup"><span data-stu-id="ef466-105">The Recommendations Cognitive Service will be replacing this service, and all the new features will be developed there.</span></span> <span data-ttu-id="ef466-106">Tiene nuevas funcionalidades como compatibilidad con procesamientos por lotes, un explorador de API más eficaz, una interfaz de API más limpia, una experiencia de facturación y suscripción más coherente, etc.</span><span class="sxs-lookup"><span data-stu-id="ef466-106">It has new capabilities like batching support, a better API Explorer, a cleaner API surface, more consistent signup/billing experience, etc.</span></span>
> <span data-ttu-id="ef466-107">Obtenga más información sobre cómo [migrar al nuevo servicio Cognitive Services](http://aka.ms/recomigrate)</span><span class="sxs-lookup"><span data-stu-id="ef466-107">Learn more about [Migrating to the new Cognitive Service](http://aka.ms/recomigrate)</span></span>
> 
> 

<span data-ttu-id="ef466-108">Este documento describe cómo integrar su sitio mediante JavaScript.</span><span class="sxs-lookup"><span data-stu-id="ef466-108">This document depict how to integrate your site using JavaScript.</span></span> <span data-ttu-id="ef466-109">El código JavaScript le permite enviar eventos de adquisición de datos y consumir recomendaciones una vez que se crea un modelo de recomendación.</span><span class="sxs-lookup"><span data-stu-id="ef466-109">The JavaScript enables you to send Data Acquisition events and to consume recommendations once you build a recommendation model.</span></span> <span data-ttu-id="ef466-110">Todas las operaciones que se realizan a través de JS se pueden realizar también desde el servidor.</span><span class="sxs-lookup"><span data-stu-id="ef466-110">All operations done via JS can be also done from server side.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="1-general-overview"></a><span data-ttu-id="ef466-111">1. Información general</span><span class="sxs-lookup"><span data-stu-id="ef466-111">1. General Overview</span></span>
<span data-ttu-id="ef466-112">La integración de su sitio con recomendaciones de Aprendizaje automático de Azure consta de 2 fases:</span><span class="sxs-lookup"><span data-stu-id="ef466-112">Integrating your site with Azure ML Recommendations consist on 2 Phases:</span></span>

1. <span data-ttu-id="ef466-113">Enviar eventos a las recomendaciones de Aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="ef466-113">Send Events into Azure ML Recommendations.</span></span> <span data-ttu-id="ef466-114">Esto le permitirá crear un modelo de recomendación.</span><span class="sxs-lookup"><span data-stu-id="ef466-114">This will enable to build a recommendation model.</span></span>
2. <span data-ttu-id="ef466-115">Use las recomendaciones.</span><span class="sxs-lookup"><span data-stu-id="ef466-115">Consume the recommendations.</span></span> <span data-ttu-id="ef466-116">Una vez generado el modelo, puede utilizar las recomendaciones.</span><span class="sxs-lookup"><span data-stu-id="ef466-116">After the model is built you can consume the recommendations.</span></span> <span data-ttu-id="ef466-117">(Este documento no explica cómo crear un modelo; lea la Guía de inicio rápido para obtener más información acerca de cómo).</span><span class="sxs-lookup"><span data-stu-id="ef466-117">(This document does not explain how to build a model, read the quick start guide to get more information on how).</span></span>

<span data-ttu-id="ef466-118"><ins>Fase I</ins></span><span class="sxs-lookup"><span data-stu-id="ef466-118"><ins>Phase I</ins></span></span>

<span data-ttu-id="ef466-119">En la primera fase, insertará en sus páginas html una pequeña biblioteca de JavaScript que permita a la página enviar eventos a medida que se producen en la página html en servidores de recomendaciones de Aprendizaje automático de Azure (a través del mercado de datos):</span><span class="sxs-lookup"><span data-stu-id="ef466-119">In the first phase you insert into your html pages a small JavaScript library that enables the page to send events as they occur on the html page into Azure ML Recommendations servers (via Data Market):</span></span>

![Dibujo1][1]

<span data-ttu-id="ef466-121"><ins>Fase II</ins></span><span class="sxs-lookup"><span data-stu-id="ef466-121"><ins>Phase II</ins></span></span>

<span data-ttu-id="ef466-122">En la segunda fase, si desea mostrar las recomendaciones en la página, seleccione una de las siguientes opciones:</span><span class="sxs-lookup"><span data-stu-id="ef466-122">In the second phase when you want to show the recommendations on the page you select one of the following options:</span></span>

<span data-ttu-id="ef466-123">1. Su servidor (en la fase de representación de la página) llama al servidor de recomendaciones de Aprendizaje automático de Azure (a través de mercado de datos) para obtener recomendaciones.</span><span class="sxs-lookup"><span data-stu-id="ef466-123">1.Your server (on the phase of page rendering) calls Azure ML Recommendations Server (via Data Market) to get recommendations.</span></span> <span data-ttu-id="ef466-124">Los resultados incluyen una lista de id. de elementos.</span><span class="sxs-lookup"><span data-stu-id="ef466-124">The results include a list of items id.</span></span> <span data-ttu-id="ef466-125">El servidor necesita enriquecer los resultados con los elementos de metadatos (por ejemplo, imágenes, descripción) y enviar la página creada al explorador.</span><span class="sxs-lookup"><span data-stu-id="ef466-125">Your server needs to enrich the results with the items Meta data (e.g. images, description) and send the created page to the browser.</span></span>

![Dibujo2][2]

<span data-ttu-id="ef466-127">2. La otra opción es utilizar el archivo de JavaScript pequeño de la fase uno para obtener una lista de elementos recomendados.</span><span class="sxs-lookup"><span data-stu-id="ef466-127">2.The other option is to use the small JavaScript file from phase one to get a simple list of recommended items.</span></span> <span data-ttu-id="ef466-128">Los datos recibidos son más simples que los que aparecen en la primera opción.</span><span class="sxs-lookup"><span data-stu-id="ef466-128">The data received here is leaner than the one in the first option.</span></span>

![Dibujo3][3]

## <a name="2-prerequisites"></a><span data-ttu-id="ef466-130">2. Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="ef466-130">2. Prerequisites</span></span>
1. <span data-ttu-id="ef466-131">Cree un modelo nuevo mediante las API.</span><span class="sxs-lookup"><span data-stu-id="ef466-131">Create a new model using the APIs.</span></span> <span data-ttu-id="ef466-132">Vea la Guía de inicio rápido para saber cómo hacerlo.</span><span class="sxs-lookup"><span data-stu-id="ef466-132">See the Quick start guide on how to do it.</span></span>
2. <span data-ttu-id="ef466-133">Codifique &lt;dataMarketUser&gt;:&lt;dataMarketKey&gt; mediante base64.</span><span class="sxs-lookup"><span data-stu-id="ef466-133">Encode your &lt;dataMarketUser&gt;:&lt;dataMarketKey&gt; with base64.</span></span> <span data-ttu-id="ef466-134">(Esto se utilizará para la autenticación básica para permitir que el código JS llame a las API).</span><span class="sxs-lookup"><span data-stu-id="ef466-134">(This will be used for the basic authentication to enable the JS code to call the APIs).</span></span>

## <a name="3-send-data-acquisition-events-using-javascript"></a><span data-ttu-id="ef466-135">3. Envíe eventos de adquisición de datos con JavaScript.</span><span class="sxs-lookup"><span data-stu-id="ef466-135">3. Send Data Acquisition events using JavaScript</span></span>
<span data-ttu-id="ef466-136">Los siguientes pasos permiten enviar eventos:</span><span class="sxs-lookup"><span data-stu-id="ef466-136">The following steps facilitate sending events:</span></span>

1. <span data-ttu-id="ef466-137">Incluya la biblioteca de JQuery en su código.</span><span class="sxs-lookup"><span data-stu-id="ef466-137">Include JQuery library in your code.</span></span> <span data-ttu-id="ef466-138">Puede descargarlo desde nuget en la siguiente dirección URL.</span><span class="sxs-lookup"><span data-stu-id="ef466-138">You can download it from nuget in the following URL.</span></span>
   
     <span data-ttu-id="ef466-139">http://www.nuget.org/packages/jQuery/1.8.2</span><span class="sxs-lookup"><span data-stu-id="ef466-139">http://www.nuget.org/packages/jQuery/1.8.2</span></span>
2. <span data-ttu-id="ef466-140">Incluya la biblioteca de recomendaciones de Java Script que encontrará en la siguiente dirección URL: http://aka.ms/RecoJSLib1.</span><span class="sxs-lookup"><span data-stu-id="ef466-140">Include the Recommendations Java Script library from the following URL: http://aka.ms/RecoJSLib1</span></span>
3. <span data-ttu-id="ef466-141">Inicialice la biblioteca de recomendaciones de Aprendizaje automático de Azure con los parámetros adecuados.</span><span class="sxs-lookup"><span data-stu-id="ef466-141">Initialize Azure ML Recommendations library with the appropriate parameters.</span></span>
   
     <span data-ttu-id="ef466-142"><script> AzureMLRecommendationsStart("<base64encoding of username:key>", "<model_id>"); </script>
4. Envíe el evento adecuado.</span><span class="sxs-lookup"><span data-stu-id="ef466-142"><script> AzureMLRecommendationsStart("<base64encoding of username:key>", "<model_id>"); </script>
4. Send the appropriate event.</span></span> <span data-ttu-id="ef466-143">Consulte la sección detallada a continuación respecto a todos los tipos de eventos (ejemplo de evento de clic)  <script> if (typeof AzureMLRecommendationsEvent=="undefined") {</span><span class="sxs-lookup"><span data-stu-id="ef466-143">See detailed section below on all type of events (example of click event)  <script> if (typeof AzureMLRecommendationsEvent=="undefined") {</span></span>         
                     <span data-ttu-id="ef466-144">AzureMLRecommendationsEvent = []; } AzureMLRecommendationsEvent.push({ event: "click", item: "18321116" }); </script></span><span class="sxs-lookup"><span data-stu-id="ef466-144">AzureMLRecommendationsEvent = []; } AzureMLRecommendationsEvent.push({ event: "click", item: "18321116" }); </script></span></span>

### <a name="31----limitations-and-browser-support"></a><span data-ttu-id="ef466-145">3.1.</span><span class="sxs-lookup"><span data-stu-id="ef466-145">3.1.</span></span>    <span data-ttu-id="ef466-146">Limitaciones y compatibilidad con exploradores</span><span class="sxs-lookup"><span data-stu-id="ef466-146">Limitations and Browser Support</span></span>
<span data-ttu-id="ef466-147">Esta es una implementación de referencia y se proporciona tal cual.</span><span class="sxs-lookup"><span data-stu-id="ef466-147">This is a reference implementation and it is given as is.</span></span> <span data-ttu-id="ef466-148">Debe admitir todos los exploradores principales.</span><span class="sxs-lookup"><span data-stu-id="ef466-148">It should support all major browsers.</span></span>

### <a name="32----type-of-events"></a><span data-ttu-id="ef466-149">3.2.</span><span class="sxs-lookup"><span data-stu-id="ef466-149">3.2.</span></span>    <span data-ttu-id="ef466-150">Tipos de eventos</span><span class="sxs-lookup"><span data-stu-id="ef466-150">Type of Events</span></span>
<span data-ttu-id="ef466-151">Hay cinco tipos de eventos que admite la biblioteca: hacer clic, clic de recomendación, agregar al carro de la compra , quitar del carro de la compra y comprar.</span><span class="sxs-lookup"><span data-stu-id="ef466-151">There are 5 types of event that the library supports: Click, Recommendation Click, Add to Shop Cart, Remove from Shop Cart and Purchase.</span></span> <span data-ttu-id="ef466-152">Hay un evento adicional que se utiliza para establecer el contexto de usuario denominado Inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="ef466-152">There is an additional event that is used to set the user context called Login.</span></span>

#### <a name="321-click-event"></a><span data-ttu-id="ef466-153">3.2.1.</span><span class="sxs-lookup"><span data-stu-id="ef466-153">3.2.1.</span></span> <span data-ttu-id="ef466-154">Evento de clic</span><span class="sxs-lookup"><span data-stu-id="ef466-154">Click Event</span></span>
<span data-ttu-id="ef466-155">Este evento se debe utilizar cada vez que un usuario hace clic en un elemento.</span><span class="sxs-lookup"><span data-stu-id="ef466-155">This event should be used any time a user clicked on an item.</span></span> <span data-ttu-id="ef466-156">Normalmente, cuando el usuario hace clic en un elemento, se abre una nueva página con los detalles de dicho elemento; en esta página, debería activarse este evento.</span><span class="sxs-lookup"><span data-stu-id="ef466-156">Usually when user clicks on an item a new page is opened with the item details; in this page this event should be triggered.</span></span>

<span data-ttu-id="ef466-157">Parámetros:</span><span class="sxs-lookup"><span data-stu-id="ef466-157">Parameters:</span></span>

* <span data-ttu-id="ef466-158">event (cadena, obligatorio) - “click”</span><span class="sxs-lookup"><span data-stu-id="ef466-158">event (string, mandatory) - “click”</span></span>
* <span data-ttu-id="ef466-159">item (cadena, obligatorio) - Identificador único del elemento</span><span class="sxs-lookup"><span data-stu-id="ef466-159">item (string, mandatory) - Unique identifier of the item</span></span>
* <span data-ttu-id="ef466-160">itemName (cadena, opcional) - El nombre del elemento</span><span class="sxs-lookup"><span data-stu-id="ef466-160">itemName (string, optional) - the name of the item</span></span>
* <span data-ttu-id="ef466-161">itemDescription (cadena, opcional) - Descripción del elemento</span><span class="sxs-lookup"><span data-stu-id="ef466-161">itemDescription (string, optional) - the description of the item</span></span>
* <span data-ttu-id="ef466-162">itemCategory (cadena, opcional) - La categoría del elemento</span><span class="sxs-lookup"><span data-stu-id="ef466-162">itemCategory (string, optional) - the category of the item</span></span>
  
        <script>
            if (typeof AzureMLRecommendationsEvent == "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: "click", item: "3111718" });
        </script>

<span data-ttu-id="ef466-163">O con datos opcionales:</span><span class="sxs-lookup"><span data-stu-id="ef466-163">Or with optional data:</span></span>

        <script>
            if (typeof AzureMLRecommendationsEvent === "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "click", item: "3111718", itemName: "Plane", itemDescription: "It is a big plane", itemCategory: "Aviation"});
        </script>


#### <a name="322-recommendation-click-event"></a><span data-ttu-id="ef466-164">3.2.2.</span><span class="sxs-lookup"><span data-stu-id="ef466-164">3.2.2.</span></span> <span data-ttu-id="ef466-165">Ejemplo de Recommendation Click:</span><span class="sxs-lookup"><span data-stu-id="ef466-165">Recommendation Click Event</span></span>
<span data-ttu-id="ef466-166">Este evento se debe utilizar cada vez que un usuario hace clic en un elemento que se recibió de las recomendaciones de Aprendizaje automático de Azure como un elemento recomendado.</span><span class="sxs-lookup"><span data-stu-id="ef466-166">This event should be used any time a user clicked on an item that was received from Azure ML Recommendations as a recommended item.</span></span> <span data-ttu-id="ef466-167">Normalmente, cuando el usuario hace clic en un elemento, se abre una nueva página con los detalles de dicho elemento; en esta página, debería activarse este evento.</span><span class="sxs-lookup"><span data-stu-id="ef466-167">Usually when user clicks on an item a new page is opened with the item details; in this page this event should be triggered.</span></span>

<span data-ttu-id="ef466-168">Parámetros:</span><span class="sxs-lookup"><span data-stu-id="ef466-168">Parameters:</span></span>

* <span data-ttu-id="ef466-169">event (cadena, obligatorio) - “recommendationclick”</span><span class="sxs-lookup"><span data-stu-id="ef466-169">event (string, mandatory) - “recommendationclick”</span></span>
* <span data-ttu-id="ef466-170">item (cadena, obligatorio) - Identificador único del elemento</span><span class="sxs-lookup"><span data-stu-id="ef466-170">item (string, mandatory) - Unique identifier of the item</span></span>
* <span data-ttu-id="ef466-171">itemName (cadena, opcional) - El nombre del elemento</span><span class="sxs-lookup"><span data-stu-id="ef466-171">itemName (string, optional) - the name of the item</span></span>
* <span data-ttu-id="ef466-172">itemDescription (cadena, opcional) - Descripción del elemento</span><span class="sxs-lookup"><span data-stu-id="ef466-172">itemDescription (string, optional) - the description of the item</span></span>
* <span data-ttu-id="ef466-173">itemCategory (cadena, opcional) - La categoría del elemento</span><span class="sxs-lookup"><span data-stu-id="ef466-173">itemCategory (string, optional) - the category of the item</span></span>
* <span data-ttu-id="ef466-174">seeds (matriz de cadena, opcional) - Los valores de inicialización que generaron la consulta de recomendación.</span><span class="sxs-lookup"><span data-stu-id="ef466-174">seeds (string array, optional) - the seeds that generated the recommendation query.</span></span>
* <span data-ttu-id="ef466-175">recoList (matriz de cadena, opcional) - El resultado de la solicitud de recomendación que generó el elemento en el que se hizo clic.</span><span class="sxs-lookup"><span data-stu-id="ef466-175">recoList (string array, optional) - the result of the recommendation request that generated the item that was clicked.</span></span>
  
        <script>
            if (typeof AzureMLRecommendationsEvent=="undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "recommendationclick", item: "18899918" });
        </script>

<span data-ttu-id="ef466-176">O con datos opcionales:</span><span class="sxs-lookup"><span data-stu-id="ef466-176">Or with optional data:</span></span>

        <script>
            if (typeof AzureMLRecommendationsEvent == "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: eventName, item: "198", itemName: "Plane2", itemDescription: "It is a big plane2", itemCategory: "Default2", seeds: ["Seed1", "Seed2"], recoList: ["199", "198", "197"]                 });
        </script>


#### <a name="323-add-shopping-cart-event"></a><span data-ttu-id="ef466-177">3.2.3.</span><span class="sxs-lookup"><span data-stu-id="ef466-177">3.2.3.</span></span> <span data-ttu-id="ef466-178">Agregar eventos de carro de la compra</span><span class="sxs-lookup"><span data-stu-id="ef466-178">Add Shopping Cart Event</span></span>
<span data-ttu-id="ef466-179">Este evento se debe usar cuando el usuario agrega un elemento al carro de la compra.</span><span class="sxs-lookup"><span data-stu-id="ef466-179">This event should be used when the user add an item to the shopping cart.</span></span>
<span data-ttu-id="ef466-180">Parámetros:</span><span class="sxs-lookup"><span data-stu-id="ef466-180">Parameters:</span></span>

* <span data-ttu-id="ef466-181">event (cadena, obligatorio) - "addshopcart"</span><span class="sxs-lookup"><span data-stu-id="ef466-181">event (string, mandatory) - “addshopcart”</span></span>
* <span data-ttu-id="ef466-182">item (cadena, obligatorio) - Identificador único del elemento</span><span class="sxs-lookup"><span data-stu-id="ef466-182">item (string, mandatory) - Unique identifier of the item</span></span>
* <span data-ttu-id="ef466-183">itemName (cadena, opcional) - El nombre del elemento</span><span class="sxs-lookup"><span data-stu-id="ef466-183">itemName (string, optional) - the name of the item</span></span>
* <span data-ttu-id="ef466-184">itemDescription (cadena, opcional) - Descripción del elemento</span><span class="sxs-lookup"><span data-stu-id="ef466-184">itemDescription (string, optional) - the description of the item</span></span>
* <span data-ttu-id="ef466-185">itemCategory (cadena, opcional) - La categoría del elemento</span><span class="sxs-lookup"><span data-stu-id="ef466-185">itemCategory (string, optional) - the category of the item</span></span>
  
        <script>
            if (typeof AzureMLRecommendationsEvent == "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "addshopcart", item: "13221118" });
        </script>

#### <a name="324-remove-shopping-cart-event"></a><span data-ttu-id="ef466-186">3.2.4.</span><span class="sxs-lookup"><span data-stu-id="ef466-186">3.2.4.</span></span> <span data-ttu-id="ef466-187">Quitar eventos de carro de la compra</span><span class="sxs-lookup"><span data-stu-id="ef466-187">Remove Shopping Cart Event</span></span>
<span data-ttu-id="ef466-188">Este evento se debe usar cuando el usuario quita un elemento del carro de la compra.</span><span class="sxs-lookup"><span data-stu-id="ef466-188">This event should be used when the user removes an item to the shopping cart.</span></span>

<span data-ttu-id="ef466-189">Parámetros:</span><span class="sxs-lookup"><span data-stu-id="ef466-189">Parameters:</span></span>

* <span data-ttu-id="ef466-190">event (cadena, obligatorio) - "removeshopcart"</span><span class="sxs-lookup"><span data-stu-id="ef466-190">event (string, mandatory) - “removeshopcart”</span></span>
* <span data-ttu-id="ef466-191">item (cadena, obligatorio) - Identificador único del elemento</span><span class="sxs-lookup"><span data-stu-id="ef466-191">item (string, mandatory) - Unique identifier of the item</span></span>
* <span data-ttu-id="ef466-192">itemName (cadena, opcional) - El nombre del elemento</span><span class="sxs-lookup"><span data-stu-id="ef466-192">itemName (string, optional) - the name of the item</span></span>
* <span data-ttu-id="ef466-193">itemDescription (cadena, opcional) - Descripción del elemento</span><span class="sxs-lookup"><span data-stu-id="ef466-193">itemDescription (string, optional) - the description of the item</span></span>
* <span data-ttu-id="ef466-194">itemCategory (cadena, opcional) - La categoría del elemento</span><span class="sxs-lookup"><span data-stu-id="ef466-194">itemCategory (string, optional) - the category of the item</span></span>
  
        <script>
            if (typeof AzureMLRecommendationsEvent=="undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: "removeshopcart", item: "111118" });
        </script>

#### <a name="325-purchase-event"></a><span data-ttu-id="ef466-195">3.2.5.</span><span class="sxs-lookup"><span data-stu-id="ef466-195">3.2.5.</span></span> <span data-ttu-id="ef466-196">Evento de compra</span><span class="sxs-lookup"><span data-stu-id="ef466-196">Purchase Event</span></span>
<span data-ttu-id="ef466-197">Este evento se debe usar cuando el usuario ha comprado su carro de la compra.</span><span class="sxs-lookup"><span data-stu-id="ef466-197">This event should be used when the user purchased his shopping cart.</span></span>

<span data-ttu-id="ef466-198">Parámetros:</span><span class="sxs-lookup"><span data-stu-id="ef466-198">Parameters:</span></span>

* <span data-ttu-id="ef466-199">event (cadena) - "purchase"</span><span class="sxs-lookup"><span data-stu-id="ef466-199">event (string) - “purchase”</span></span>
* <span data-ttu-id="ef466-200">items ( Purchased[] ) - Matriz con una entrada por cada elemento comprado.</span><span class="sxs-lookup"><span data-stu-id="ef466-200">items ( Purchased[] ) - Array holding an entry for each item purchased.</span></span><br><br>
  <span data-ttu-id="ef466-201">Formato de elemento comprado:</span><span class="sxs-lookup"><span data-stu-id="ef466-201">Purchased format:</span></span>
  * <span data-ttu-id="ef466-202">item (cadena) - Identificador único del elemento</span><span class="sxs-lookup"><span data-stu-id="ef466-202">item (string) - Unique identifier of the item.</span></span>
  * <span data-ttu-id="ef466-203">count (entero o cadena) - Número de elementos que se compraron.</span><span class="sxs-lookup"><span data-stu-id="ef466-203">count (int or string) - number of items that were purchased.</span></span>
  * <span data-ttu-id="ef466-204">price (flotante o cadena) - Campo opcional; precio del elemento.</span><span class="sxs-lookup"><span data-stu-id="ef466-204">price (float or string) - optional field - the price of the item.</span></span>

<span data-ttu-id="ef466-205">El ejemplo siguiente muestra la compra de 3 elementos (33, 34, 35), dos con todos los campos (elemento, cantidad, precio) y uno (elemento 34) sin precio.</span><span class="sxs-lookup"><span data-stu-id="ef466-205">The example below shows purchase of 3 items (33, 34, 35), two with all fields populated (item, count, price) and one (item 34) without a price.</span></span>

        <script>
            if ( typeof AzureMLRecommendationsEvent == "undefined"){ AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: "purchase", items: [{ item: "33", count: "1", price: "10" }, { item: "34", count: "2" }, { item: "35", count: "1", price: "210" }] });
        </script>

#### <a name="326-user-login-event"></a><span data-ttu-id="ef466-206">3.2.6.</span><span class="sxs-lookup"><span data-stu-id="ef466-206">3.2.6.</span></span> <span data-ttu-id="ef466-207">Evento de inicio de sesión de usuario</span><span class="sxs-lookup"><span data-stu-id="ef466-207">User Login Event</span></span>
<span data-ttu-id="ef466-208">La biblioteca de eventos de recomendaciones de Aprendizaje automático de Azure crea y utiliza una cookie para identificar los eventos que provienen del mismo explorador.</span><span class="sxs-lookup"><span data-stu-id="ef466-208">Azure ML Recommendations Event library creates and use a cookie in order to identify events that came from the same browser.</span></span> <span data-ttu-id="ef466-209">Para mejorar los resultados del modelo, las recomendaciones de Aprendizaje automático de Azure permiten establecer una identificación única de usuario que omitirá el uso de cookies.</span><span class="sxs-lookup"><span data-stu-id="ef466-209">In order to improve the model results Azure ML Recommendations enables to set a user unique identification that will override the cookie usage.</span></span>

<span data-ttu-id="ef466-210">Este evento se debe utilizar después del inicio de sesión de usuario en su sitio.</span><span class="sxs-lookup"><span data-stu-id="ef466-210">This event should be used after the user login to your site.</span></span>

<span data-ttu-id="ef466-211">Parámetros:</span><span class="sxs-lookup"><span data-stu-id="ef466-211">Parameters:</span></span>

* <span data-ttu-id="ef466-212">event (cadena) - "userlogin"</span><span class="sxs-lookup"><span data-stu-id="ef466-212">event (string) - “userlogin”</span></span>
* <span data-ttu-id="ef466-213">user (cadena) - Identificación único del usuario.</span><span class="sxs-lookup"><span data-stu-id="ef466-213">user (string) - unique identification of the user.</span></span>
  
        <script>
            if (typeof AzureMLRecommendationsEvent=="undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "userlogin", user: “ABCD10AA” });
        </script>

## <a name="4-consume-recommendations-via-javascript"></a><span data-ttu-id="ef466-214">4. Consumir recomendaciones a través de JavaScript</span><span class="sxs-lookup"><span data-stu-id="ef466-214">4. Consume Recommendations via JavaScript</span></span>
<span data-ttu-id="ef466-215">El código que consume la recomendación se activa por algunos eventos de JavaScript en la página web del cliente.</span><span class="sxs-lookup"><span data-stu-id="ef466-215">The code that consumes the recommendation is triggered by some JavaScript event by the client’s webpage.</span></span> <span data-ttu-id="ef466-216">La respuesta de recomendación incluye los identificadores de elementos recomendados, sus nombres y sus clasificaciones.</span><span class="sxs-lookup"><span data-stu-id="ef466-216">The recommendation response includes the recommended items Ids, their names and their ratings.</span></span> <span data-ttu-id="ef466-217">Es preferible utilizar esta opción solo para una visualización de la lista de los elementos recomendados: debe realizarse un control más complejo (por ejemplo, para agregar los metadatos del elemento) en la integración del lado servidor.</span><span class="sxs-lookup"><span data-stu-id="ef466-217">It’s best to use this option only for a list display of the recommended items - more complex handling (such as adding the item’s metadata) should be done on the server side integration.</span></span>

### <a name="41-consume-recommendations"></a><span data-ttu-id="ef466-218">4.1 Recomendaciones de uso</span><span class="sxs-lookup"><span data-stu-id="ef466-218">4.1 Consume Recommendations</span></span>
<span data-ttu-id="ef466-219">Para consumir recomendaciones, deberá incluir las bibliotecas JavaScript requeridas en la página y llamar a AzureMLRecommendationsStart.</span><span class="sxs-lookup"><span data-stu-id="ef466-219">To consume recommendations you need to include the required JavaScript libraries in your page and to call AzureMLRecommendationsStart.</span></span> <span data-ttu-id="ef466-220">Consulte la sección 2.</span><span class="sxs-lookup"><span data-stu-id="ef466-220">See section 2.</span></span>

<span data-ttu-id="ef466-221">Para consumir recomendaciones para uno o varios elementos, debe llamar a un método denominado: AzureMLRecommendationsGetI2IRecommendation.</span><span class="sxs-lookup"><span data-stu-id="ef466-221">To consume recommendations for one or more items you need to call a method called: AzureMLRecommendationsGetI2IRecommendation.</span></span>

<span data-ttu-id="ef466-222">Parámetros:</span><span class="sxs-lookup"><span data-stu-id="ef466-222">Parameters:</span></span>

* <span data-ttu-id="ef466-223">items (matriz de cadenas) - Uno o varios elementos para los que obtener recomendaciones.</span><span class="sxs-lookup"><span data-stu-id="ef466-223">items (array of strings) - One or more items to get recommendations for.</span></span> <span data-ttu-id="ef466-224">Si consume una compilación Fbt, aquí solo puede establecer un elemento.</span><span class="sxs-lookup"><span data-stu-id="ef466-224">If you consume an Fbt build then you can set here only one item.</span></span>
* <span data-ttu-id="ef466-225">numberOfResults (entero) - Número de resultados requeridos.</span><span class="sxs-lookup"><span data-stu-id="ef466-225">numberOfResults (int) - number of required results.</span></span>
* <span data-ttu-id="ef466-226">includeMetadata (booleano, opcional) - Si se establece en ‘true’ indica que el campo de metadatos se debe rellenar en el resultado.</span><span class="sxs-lookup"><span data-stu-id="ef466-226">includeMetadata (boolean, optional) - if set to ‘true’ indicates that the metadata field must be populated in the result.</span></span>
* <span data-ttu-id="ef466-227">Función de procesamiento - Una función que controlará las recomendaciones devueltas.</span><span class="sxs-lookup"><span data-stu-id="ef466-227">Processing function - a function that will handle the recommendations returned.</span></span> <span data-ttu-id="ef466-228">Los datos se devuelven como una matriz de:</span><span class="sxs-lookup"><span data-stu-id="ef466-228">The data is returned as an array of:</span></span>
  * <span data-ttu-id="ef466-229">item - Identificador único del elemento</span><span class="sxs-lookup"><span data-stu-id="ef466-229">Item - item unique id</span></span>
  * <span data-ttu-id="ef466-230">name - Nombre del elemento (si existe en el catálogo)</span><span class="sxs-lookup"><span data-stu-id="ef466-230">name - item name (if exist in catalog)</span></span>
  * <span data-ttu-id="ef466-231">rating - Clasificación de recomendación</span><span class="sxs-lookup"><span data-stu-id="ef466-231">rating - recommendation rating</span></span>
  * <span data-ttu-id="ef466-232">metadata - Una cadena que representa los metadatos del elemento</span><span class="sxs-lookup"><span data-stu-id="ef466-232">metadata - a string that represents the metadata of the item</span></span>

<span data-ttu-id="ef466-233">Ejemplo: El siguiente código solicita 8 recomendaciones para el elemento "64f6eb0d-947a-4c18-a16c-888da9e228ba" (y al no especificar includeMetadata, se indica implícitamente que no se requieren metadatos), y luego concatena los resultados en un búfer.</span><span class="sxs-lookup"><span data-stu-id="ef466-233">Example: The following code requests 8 recommendations for item "64f6eb0d-947a-4c18-a16c-888da9e228ba" (and by not specifying includeMetadata - it implicitly says that no metadata is required), it then concatenate the results into a buffer.</span></span>

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
