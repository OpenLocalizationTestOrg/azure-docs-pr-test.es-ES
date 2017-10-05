---
title: "Creación de una función que se integre con Azure Logic Apps | Microsoft Docs"
description: "Creación de una función que se integre con Azure Logic Apps y Azure Cognitive Services para categorizar las opiniones de tweet y enviar notificaciones en caso de que las opiniones sean negativas."
services: functions, logic-apps, cognitive-services
keywords: "flujo de trabajo, aplicaciones de nube, servicios en la nube, procesos empresariales, integración de sistemas, integración de aplicaciones empresariales, EAI"
documentationcenter: 
author: ggailey777
manager: erikre
editor: 
ms.assetid: 60495cc5-1638-4bf0-8174-52786d227734
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 4a5dc668e21c5328b308c8f5852aaa922232374d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-function-that-integrates-with-azure-logic-apps"></a><span data-ttu-id="18ee4-104">Creación de una función que se integre con Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="18ee4-104">Create a function that integrates with Azure Logic Apps</span></span>

<span data-ttu-id="18ee4-105">Azure Functions se integra con Azure Logic Apps en el diseñador de Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="18ee4-105">Azure Functions integrates with Azure Logic Apps in the Logic Apps Designer.</span></span> <span data-ttu-id="18ee4-106">Esta integración permite usar la capacidad de proceso de Azure Functions en las orquestaciones con otros servicios de Azure y de terceros.</span><span class="sxs-lookup"><span data-stu-id="18ee4-106">This integration lets you use the computing power of Functions in orchestrations with other Azure and third-party services.</span></span> 

<span data-ttu-id="18ee4-107">Este tutorial muestra cómo utilizar Functions con Logic Apps y Azure Cognitive Services para analizar opiniones de entradas de Twitter.</span><span class="sxs-lookup"><span data-stu-id="18ee4-107">This tutorial shows you how to use Functions with Logic Apps and Azure Cognitive Services to analyze sentiment from Twitter posts.</span></span> <span data-ttu-id="18ee4-108">Una función desencadenada por HTTP clasifica los tweets en verde, amarillo o rojo en función de la puntuación de la opinión.</span><span class="sxs-lookup"><span data-stu-id="18ee4-108">An HTTP triggered function categorizes tweets as green, yellow, or red based on the sentiment score.</span></span> <span data-ttu-id="18ee4-109">Se envía un correo electrónico cuando se detecta una opinión deficiente.</span><span class="sxs-lookup"><span data-stu-id="18ee4-109">An email is sent when poor sentiment is detected.</span></span> 

![imagen de los dos primeros pasos de una aplicación en el diseñador de Logic Apps](media/functions-twitter-email/designer1.png)

<span data-ttu-id="18ee4-111">En este tutorial, aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="18ee4-111">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="18ee4-112">Cree una cuenta de Cognitive Services.</span><span class="sxs-lookup"><span data-stu-id="18ee4-112">Create a Cognitive Services account.</span></span>
> * <span data-ttu-id="18ee4-113">Crear una función que clasifica las opiniones de tweet.</span><span class="sxs-lookup"><span data-stu-id="18ee4-113">Create a function that categorizes tweet sentiment.</span></span>
> * <span data-ttu-id="18ee4-114">Crear una aplicación de lógica que se conecta a Twitter.</span><span class="sxs-lookup"><span data-stu-id="18ee4-114">Create a logic app that connects to Twitter.</span></span>
> * <span data-ttu-id="18ee4-115">Agregar detección de opiniones a la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="18ee4-115">Add sentiment detection to the logic app.</span></span> 
> * <span data-ttu-id="18ee4-116">Conectar la aplicación lógica a la función.</span><span class="sxs-lookup"><span data-stu-id="18ee4-116">Connect the logic app to the function.</span></span>
> * <span data-ttu-id="18ee4-117">Enviar un correo electrónico en función de la respuesta de la función.</span><span class="sxs-lookup"><span data-stu-id="18ee4-117">Send an email based on the response from the function.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="18ee4-118">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="18ee4-118">Prerequisites</span></span>

+ <span data-ttu-id="18ee4-119">Una cuenta de [Twitter](https://twitter.com/) activa.</span><span class="sxs-lookup"><span data-stu-id="18ee4-119">An active [Twitter](https://twitter.com/) account.</span></span> 
+ <span data-ttu-id="18ee4-120">Una cuenta de [Outlook.com](https://outlook.com/) (para enviar las notificaciones).</span><span class="sxs-lookup"><span data-stu-id="18ee4-120">An [Outlook.com](https://outlook.com/) account (for sending notifications).</span></span>
+ <span data-ttu-id="18ee4-121">Este tema usa como punto de inicio los recursos creados en [Creación de su primera función desde Azure Portal](functions-create-first-azure-function.md).</span><span class="sxs-lookup"><span data-stu-id="18ee4-121">This topic uses as its starting point the resources created in [Create your first function from the Azure portal](functions-create-first-azure-function.md).</span></span>  
<span data-ttu-id="18ee4-122">Si aún no lo hecho, lleve a cabo estos pasos ahora para crear la aplicación de función.</span><span class="sxs-lookup"><span data-stu-id="18ee4-122">If you haven't already done so, complete these steps now to create your function app.</span></span>

## <a name="create-a-cognitive-services-account"></a><span data-ttu-id="18ee4-123">Creación de una cuenta de Cognitive Services</span><span class="sxs-lookup"><span data-stu-id="18ee4-123">Create a Cognitive Services account</span></span>

<span data-ttu-id="18ee4-124">Se requiere una cuenta de Cognitive Services para detectar el sentimiento de los tweets que se están supervisando.</span><span class="sxs-lookup"><span data-stu-id="18ee4-124">A Cognitive Services account is required to detect the sentiment of tweets being monitored.</span></span>

1. <span data-ttu-id="18ee4-125">Inicie sesión en el [Portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="18ee4-125">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>

2. <span data-ttu-id="18ee4-126">Haga clic en el botón **Nuevo** de la esquina superior izquierda de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="18ee4-126">Click the **New** button found on the upper left-hand corner of the Azure portal.</span></span>

3. <span data-ttu-id="18ee4-127">Haga clic en **Datos y análisis** > **Cognitive Services**.</span><span class="sxs-lookup"><span data-stu-id="18ee4-127">Click **Data + Analytics** > **Cognitive  Services**.</span></span> <span data-ttu-id="18ee4-128">A continuación, utilice la configuración de acuerdo con lo especificado en la tabla, acepte los términos y active **Anclar al panel**.</span><span class="sxs-lookup"><span data-stu-id="18ee4-128">Then, use the settings as specified in the table, accept the terms, and check **Pin to dashboard**.</span></span>

    ![Hoja para crear cuenta de Cognitive Services](media/functions-twitter-email/cog_svcs_account.png)

    | <span data-ttu-id="18ee4-130">Configuración</span><span class="sxs-lookup"><span data-stu-id="18ee4-130">Setting</span></span>      |  <span data-ttu-id="18ee4-131">Valor sugerido</span><span class="sxs-lookup"><span data-stu-id="18ee4-131">Suggested value</span></span>   | <span data-ttu-id="18ee4-132">Descripción</span><span class="sxs-lookup"><span data-stu-id="18ee4-132">Description</span></span>                                        |
    | --- | --- | --- |
    | <span data-ttu-id="18ee4-133">**Name**</span><span class="sxs-lookup"><span data-stu-id="18ee4-133">**Name**</span></span> | <span data-ttu-id="18ee4-134">MyCognitiveServicesAccnt</span><span class="sxs-lookup"><span data-stu-id="18ee4-134">MyCognitiveServicesAccnt</span></span> | <span data-ttu-id="18ee4-135">Elija un nombre de cuenta único.</span><span class="sxs-lookup"><span data-stu-id="18ee4-135">Choose a unique account name.</span></span> |
    | <span data-ttu-id="18ee4-136">**Tipo de API**</span><span class="sxs-lookup"><span data-stu-id="18ee4-136">**API type**</span></span> | <span data-ttu-id="18ee4-137">Text Analytics API</span><span class="sxs-lookup"><span data-stu-id="18ee4-137">Text Analytics API</span></span> | <span data-ttu-id="18ee4-138">API que se utiliza para analizar el texto.</span><span class="sxs-lookup"><span data-stu-id="18ee4-138">API used to analyze text.</span></span>  |
    | <span data-ttu-id="18ee4-139">**Ubicación**</span><span class="sxs-lookup"><span data-stu-id="18ee4-139">**Location**</span></span> | <span data-ttu-id="18ee4-140">Oeste de EE. UU.</span><span class="sxs-lookup"><span data-stu-id="18ee4-140">West US</span></span> | <span data-ttu-id="18ee4-141">Actualmente, solo está disponible **Oeste de EE. UU.** para análisis de texto.</span><span class="sxs-lookup"><span data-stu-id="18ee4-141">Currently, only **West US** is available for text analytics.</span></span> |
    | <span data-ttu-id="18ee4-142">**Plan de tarifa**</span><span class="sxs-lookup"><span data-stu-id="18ee4-142">**Pricing tier**</span></span> | <span data-ttu-id="18ee4-143">F0</span><span class="sxs-lookup"><span data-stu-id="18ee4-143">F0</span></span> | <span data-ttu-id="18ee4-144">Comience con la tarifa más baja.</span><span class="sxs-lookup"><span data-stu-id="18ee4-144">Start with the lowest tier.</span></span> <span data-ttu-id="18ee4-145">Si se queda sin llamadas, aumente a un nivel superior.</span><span class="sxs-lookup"><span data-stu-id="18ee4-145">If you run out of calls, scale to a higher tier.</span></span>|
    | <span data-ttu-id="18ee4-146">**Grupos de recursos**</span><span class="sxs-lookup"><span data-stu-id="18ee4-146">**Resource group**</span></span> | <span data-ttu-id="18ee4-147">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="18ee4-147">myResourceGroup</span></span> | <span data-ttu-id="18ee4-148">Utilice el mismo grupo de recursos para todos los servicios de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="18ee4-148">Use the same resource group for all services in this tutorial.</span></span>|

4. <span data-ttu-id="18ee4-149">Haga clic en **Crear** para crear la cuenta.</span><span class="sxs-lookup"><span data-stu-id="18ee4-149">Click **Create** to create your account.</span></span> <span data-ttu-id="18ee4-150">Una vez creada la cuenta, haga clic en la nueva cuenta de Cognitive Services anclada al panel.</span><span class="sxs-lookup"><span data-stu-id="18ee4-150">After the account is created, click your new Cognitive Services account pinned to the dashboard.</span></span> 

5. <span data-ttu-id="18ee4-151">En la cuenta, haga clic en **Claves** y, a continuación, copie el valor de **Clave 1** y guárdelo.</span><span class="sxs-lookup"><span data-stu-id="18ee4-151">In the account, click **Keys**, and then copy the value of **Key 1** and save it.</span></span> <span data-ttu-id="18ee4-152">Esta clave se utiliza para conectar la aplicación lógica a la cuenta de Cognitive Services.</span><span class="sxs-lookup"><span data-stu-id="18ee4-152">You use this key to connect the logic app to your Cognitive Services account.</span></span> 
 
    ![simétricas](media/functions-twitter-email/keys.png)

## <a name="create-the-function"></a><span data-ttu-id="18ee4-154">Creación de la función</span><span class="sxs-lookup"><span data-stu-id="18ee4-154">Create the function</span></span>

<span data-ttu-id="18ee4-155">Functions proporciona una excelente manera de descargar tareas de procesamiento en un flujo de trabajo de aplicaciones lógicas.</span><span class="sxs-lookup"><span data-stu-id="18ee4-155">Functions provides a great way to offload processing tasks in a logic apps workflow.</span></span> <span data-ttu-id="18ee4-156">Este tutorial utiliza una función desencadenada por HTTP de Cognitive Services para procesar las puntuaciones de opinión de los tweet y devolver un valor de clasificación.</span><span class="sxs-lookup"><span data-stu-id="18ee4-156">This tutorial uses an HTTP triggered function to process tweet sentiment scores from Cognitive Services and return a category value.</span></span>  

1. <span data-ttu-id="18ee4-157">Expanda la aplicación de función, haga clic en el botón **+** junto a **Funciones** y haga clic en la plantilla **HTTPTrigger**.</span><span class="sxs-lookup"><span data-stu-id="18ee4-157">Expand your function app, click the **+** button next to **Functions**, click the **HTTPTrigger** template.</span></span> <span data-ttu-id="18ee4-158">Escriba `CategorizeSentiment` como **Nombre** de la función y haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="18ee4-158">Type `CategorizeSentiment` for the function **Name** and click **Create**.</span></span>

    ![Hoja Instancias de Function App, Functions +](media/functions-twitter-email/add_fun.png)

2. <span data-ttu-id="18ee4-160">Reemplace el contenido del archivo run.csx por el código siguiente y haga clic en **Guardar**:</span><span class="sxs-lookup"><span data-stu-id="18ee4-160">Replace the contents of the run.csx file with the following code, then click **Save**:</span></span>

    ```c#
    using System.Net;
    
    public static async Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
    {
        // The sentiment category defaults to 'GREEN'. 
        string category = "GREEN";
    
        // Get the sentiment score from the request body.
        double score = await req.Content.ReadAsAsync<double>();
        log.Info(string.Format("The sentiment score received is '{0}'.",
                    score.ToString()));
    
        // Set the category based on the sentiment score.
        if (score < .3)
        {
            category = "RED";
        }
        else if (score < .6)
        {
            category = "YELLOW";
        }
        return req.CreateResponse(HttpStatusCode.OK, category);
    }
    ```
    <span data-ttu-id="18ee4-161">El código de la función devuelve una clasificación de color basada en la puntuación de la opinión recibida en la solicitud.</span><span class="sxs-lookup"><span data-stu-id="18ee4-161">This function code returns a color category based on the sentiment score received in the request.</span></span> 

3. <span data-ttu-id="18ee4-162">Para probar la función, haga clic en **Probar** a la derecha para expandir la pestaña de pruebas. Escriba un valor de `0.2` en el **Cuerpo de la solicitud** y, a continuación, haga clic en **Ejecutar**.</span><span class="sxs-lookup"><span data-stu-id="18ee4-162">To test the function, click **Test** at the far right to expand the Test tab. Type a value of `0.2` for the **Request body**, and then click **Run**.</span></span> <span data-ttu-id="18ee4-163">Devuelve un valor **RED** (rojo) en el cuerpo de la respuesta.</span><span class="sxs-lookup"><span data-stu-id="18ee4-163">A value of **RED** is returned in the body of the response.</span></span> 

    ![Prueba de la función en Azure Portal](./media/functions-twitter-email/test.png)

<span data-ttu-id="18ee4-165">Ahora, tiene una función que clasifica las puntuaciones de opinión.</span><span class="sxs-lookup"><span data-stu-id="18ee4-165">Now you have a function that categorizes sentiment scores.</span></span> <span data-ttu-id="18ee4-166">A continuación, cree una aplicación lógica que integre la función con las cuentas de Twitter y Cognitive Services.</span><span class="sxs-lookup"><span data-stu-id="18ee4-166">Next, you create a logic app that integrates your function with your Twitter and Cognitive Services accounts.</span></span> 

## <a name="create-a-logic-app"></a><span data-ttu-id="18ee4-167">Creación de una aplicación lógica</span><span class="sxs-lookup"><span data-stu-id="18ee4-167">Create a logic app</span></span>   

1. <span data-ttu-id="18ee4-168">En Azure Portal, haga clic en el botón **Nuevo** de la esquina superior izquierda de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="18ee4-168">In the Azure portal, click the **New** button found on the upper left-hand corner of the Azure portal.</span></span>

2. <span data-ttu-id="18ee4-169">Haga clic en **Integración empresarial** > **Aplicación lógica**.</span><span class="sxs-lookup"><span data-stu-id="18ee4-169">Click **Enterprise Integration** > **Logic App**.</span></span> <span data-ttu-id="18ee4-170">A continuación, utilice la configuración como se especifica en la tabla, active **Anclar al panel** y haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="18ee4-170">Then, use the settings as specified in the table, check **Pin to dashboard**, and click **Create**.</span></span>
 
4. <span data-ttu-id="18ee4-171">Después, en **Nombre**, escriba `TweetSentiment`; use la configuración como se especifica en la tabla, acepte los términos y active **Anclar al panel**.</span><span class="sxs-lookup"><span data-stu-id="18ee4-171">Then, type a **Name** like `TweetSentiment`,  use the settings as specified in the table, accept the terms, and check **Pin to dashboard**.</span></span>

    ![Creación de una aplicación lógica en Azure Portal](./media/functions-twitter-email/new_logicApp.png)

    | <span data-ttu-id="18ee4-173">Configuración</span><span class="sxs-lookup"><span data-stu-id="18ee4-173">Setting</span></span>      |  <span data-ttu-id="18ee4-174">Valor sugerido</span><span class="sxs-lookup"><span data-stu-id="18ee4-174">Suggested value</span></span>   | <span data-ttu-id="18ee4-175">Descripción</span><span class="sxs-lookup"><span data-stu-id="18ee4-175">Description</span></span>                                        |
    | ----------------- | ------------ | ------------- |
    | <span data-ttu-id="18ee4-176">**Name**</span><span class="sxs-lookup"><span data-stu-id="18ee4-176">**Name**</span></span> | <span data-ttu-id="18ee4-177">TweetSentiment</span><span class="sxs-lookup"><span data-stu-id="18ee4-177">TweetSentiment</span></span> | <span data-ttu-id="18ee4-178">Elija un nombre adecuado para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="18ee4-178">Choose an appropriate name for your app.</span></span> |
    | <span data-ttu-id="18ee4-179">**Grupos de recursos**</span><span class="sxs-lookup"><span data-stu-id="18ee4-179">**Resource group**</span></span> | <span data-ttu-id="18ee4-180">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="18ee4-180">myResourceGroup</span></span> | <span data-ttu-id="18ee4-181">API que se utiliza para analizar el texto.</span><span class="sxs-lookup"><span data-stu-id="18ee4-181">API used to analyze text.</span></span>  |
    | <span data-ttu-id="18ee4-182">**Ubicación**</span><span class="sxs-lookup"><span data-stu-id="18ee4-182">**Location**</span></span> | <span data-ttu-id="18ee4-183">Este de EE. UU.</span><span class="sxs-lookup"><span data-stu-id="18ee4-183">East US</span></span> | <span data-ttu-id="18ee4-184">Elija una ubicación cercana a usted.</span><span class="sxs-lookup"><span data-stu-id="18ee4-184">Choose a location close to you.</span></span> |
    | <span data-ttu-id="18ee4-185">**Grupos de recursos**</span><span class="sxs-lookup"><span data-stu-id="18ee4-185">**Resource group**</span></span> | <span data-ttu-id="18ee4-186">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="18ee4-186">myResourceGroup</span></span> | <span data-ttu-id="18ee4-187">Elija el mismo grupo de recursos existente que antes.</span><span class="sxs-lookup"><span data-stu-id="18ee4-187">Choose the same existing resource group as before.</span></span>|

4. <span data-ttu-id="18ee4-188">Haga clic en **Crear** para crear la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="18ee4-188">Click **Create** to create your logic app.</span></span> <span data-ttu-id="18ee4-189">Una vez creada la aplicación, haga clic en la nueva aplicación lógica anclada al panel.</span><span class="sxs-lookup"><span data-stu-id="18ee4-189">After the app is created, click your new logic app pinned to the dashboard.</span></span> <span data-ttu-id="18ee4-190">A continuación, en el diseñador de Logic Apps, desplácese hacia abajo y haga clic en la plantilla **Aplicación lógica en blanco**.</span><span class="sxs-lookup"><span data-stu-id="18ee4-190">Then in the Logic Apps Designer, scroll down and click the **Blank Logic App** template.</span></span> 

    ![Plantilla Aplicación lógica en blanco](media/functions-twitter-email/blank.png)

<span data-ttu-id="18ee4-192">Ahora puede usar el diseñador de Logic Apps para agregar servicios y desencadenadores a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="18ee4-192">You can now use the Logic Apps Designer to add services and triggers to your app.</span></span>

## <a name="connect-to-twitter"></a><span data-ttu-id="18ee4-193">Conexión a Twitter</span><span class="sxs-lookup"><span data-stu-id="18ee4-193">Connect to Twitter</span></span>

<span data-ttu-id="18ee4-194">En primer lugar, cree una conexión a la cuenta de Twitter.</span><span class="sxs-lookup"><span data-stu-id="18ee4-194">First, create a connection to your Twitter account.</span></span> <span data-ttu-id="18ee4-195">La aplicación lógica sondea si hay tweets, que desencadenan la ejecución de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="18ee4-195">The logic app polls for tweets, which trigger the app to run.</span></span>

1. <span data-ttu-id="18ee4-196">En el diseñador, haga clic en el servicio **Twitter** y haga clic en el desencadenador **Cuando se publica un nuevo tweet**.</span><span class="sxs-lookup"><span data-stu-id="18ee4-196">In the designer, click the **Twitter** service, and click the **When a new tweet is posted** trigger.</span></span> <span data-ttu-id="18ee4-197">Inicie sesión en su cuenta de Twitter y autorice a Logic Apps para usar su cuenta.</span><span class="sxs-lookup"><span data-stu-id="18ee4-197">Sign in to your Twitter account and authorize Logic Apps to use your account.</span></span>

2. <span data-ttu-id="18ee4-198">Use la configuración del desencadenador de Twitter como se especifica en la tabla.</span><span class="sxs-lookup"><span data-stu-id="18ee4-198">Use the Twitter trigger settings as specified in the table.</span></span> 

    ![Configuración del conector de Twitter](media/functions-twitter-email/azure_tweet.png)

    | <span data-ttu-id="18ee4-200">Configuración</span><span class="sxs-lookup"><span data-stu-id="18ee4-200">Setting</span></span>      |  <span data-ttu-id="18ee4-201">Valor sugerido</span><span class="sxs-lookup"><span data-stu-id="18ee4-201">Suggested value</span></span>   | <span data-ttu-id="18ee4-202">Descripción</span><span class="sxs-lookup"><span data-stu-id="18ee4-202">Description</span></span>                                        |
    | ----------------- | ------------ | ------------- |
    | <span data-ttu-id="18ee4-203">**Texto de búsqueda**</span><span class="sxs-lookup"><span data-stu-id="18ee4-203">**Search text**</span></span> | <span data-ttu-id="18ee4-204">#Azure</span><span class="sxs-lookup"><span data-stu-id="18ee4-204">#Azure</span></span> | <span data-ttu-id="18ee4-205">Use un hashtag lo suficientemente popular como para generar nuevos tweets en el intervalo elegido.</span><span class="sxs-lookup"><span data-stu-id="18ee4-205">Use a hashtag that is popular enough for to generate new tweets in the chosen interval.</span></span> <span data-ttu-id="18ee4-206">Si utiliza el nivel Gratis y su hashtag es demasiado popular, puede agotar rápidamente las transacciones de la cuenta de Cognitive Services.</span><span class="sxs-lookup"><span data-stu-id="18ee4-206">When using the Free tier and your hashtag is too popular, you can quickly use up the transactions in your Cognitive Services account.</span></span> |
    | <span data-ttu-id="18ee4-207">**Frecuencia**</span><span class="sxs-lookup"><span data-stu-id="18ee4-207">**Frequency**</span></span> | <span data-ttu-id="18ee4-208">Minuto</span><span class="sxs-lookup"><span data-stu-id="18ee4-208">Minute</span></span> | <span data-ttu-id="18ee4-209">La unidad de frecuencia utilizada para el sondeo de Twitter.</span><span class="sxs-lookup"><span data-stu-id="18ee4-209">The frequency unit used for polling Twitter.</span></span>  |
    | <span data-ttu-id="18ee4-210">**Intervalo**</span><span class="sxs-lookup"><span data-stu-id="18ee4-210">**Interval**</span></span> | <span data-ttu-id="18ee4-211">15</span><span class="sxs-lookup"><span data-stu-id="18ee4-211">15</span></span> | <span data-ttu-id="18ee4-212">El tiempo transcurrido entre solicitudes a Twitter, en unidades de frecuencia.</span><span class="sxs-lookup"><span data-stu-id="18ee4-212">The time elapsed between Twitter requests, in frequency units.</span></span> |

3.  <span data-ttu-id="18ee4-213">Haga clic en **Guardar** para conectarse a su cuenta de Twitter.</span><span class="sxs-lookup"><span data-stu-id="18ee4-213">Click **Save** to connect to your Twitter account.</span></span> 

<span data-ttu-id="18ee4-214">Ahora la aplicación está conectada a Twitter.</span><span class="sxs-lookup"><span data-stu-id="18ee4-214">Now your app is connected to Twitter.</span></span> <span data-ttu-id="18ee4-215">A continuación, va a conectar a análisis de texto para detectar la opinión de los tweets recopilados.</span><span class="sxs-lookup"><span data-stu-id="18ee4-215">Next, you connect to text analytics to detect the sentiment of collected tweets.</span></span>

## <a name="add-sentiment-detection"></a><span data-ttu-id="18ee4-216">Agregar la detección de opiniones</span><span class="sxs-lookup"><span data-stu-id="18ee4-216">Add sentiment detection</span></span>

1. <span data-ttu-id="18ee4-217">Haga clic en **Nuevo paso** y, a continuación, en **Agregar una acción**.</span><span class="sxs-lookup"><span data-stu-id="18ee4-217">Click **New Step**, and then **Add an action**.</span></span>

    ![Nuevo paso y Agregar una acción](media/functions-twitter-email/new_step.png)

2. <span data-ttu-id="18ee4-219">En **Elegir una acción**, haga clic en **Análisis de texto** y, a continuación, haga clic en la acción **Detectar opiniones**.</span><span class="sxs-lookup"><span data-stu-id="18ee4-219">In **Choose an action**, click **Text Analytics**, and then click the **Detect sentiment** action.</span></span>

    ![Detectar sentimiento](media/functions-twitter-email/detect_sent.png)

3. <span data-ttu-id="18ee4-221">Escriba un nombre de conexión como `MyCognitiveServicesConnection`, pegue la clave para la cuenta de Cognitive Services que ha guardado y haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="18ee4-221">Type a connection name such as `MyCognitiveServicesConnection`, paste the key for your Cognitive Services account that you saved, and click **Create**.</span></span>  

4. <span data-ttu-id="18ee4-222">Haga clic en **Texto para analizar** > **Texto de Tweet** y, a continuación, haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="18ee4-222">Click **Text to analyze** > **Tweet text**, and then click **Save**.</span></span>  

    ![Detectar sentimiento](media/functions-twitter-email/ds_tta.png)

<span data-ttu-id="18ee4-224">Una vez configurada la detección de opinión, puede agregar una conexión a la función que consume los resultados de la puntuación de la opinión.</span><span class="sxs-lookup"><span data-stu-id="18ee4-224">Now that sentiment detection is configured, you can add a connection to your function that consumes the sentiment score output.</span></span>

## <a name="connect-sentiment-output-to-your-function"></a><span data-ttu-id="18ee4-225">Conexión de la salida de opiniones con la función</span><span class="sxs-lookup"><span data-stu-id="18ee4-225">Connect sentiment output to your function</span></span>

1. <span data-ttu-id="18ee4-226">En el diseñador de Logic Apps, haga clic en **Nuevo paso** > **Agregar una acción** y, a continuación, haga clic en **Azure Functions**.</span><span class="sxs-lookup"><span data-stu-id="18ee4-226">In the Logic Apps Designer, click **New step** > **Add an action**, and then click **Azure Functions**.</span></span> 

2. <span data-ttu-id="18ee4-227">Haga clic en **Elegir una función de Azure** y seleccione la función **CategorizeSentiment** que ha creado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="18ee4-227">Click **Choose an Azure function**, select the **CategorizeSentiment** function you created earlier.</span></span>  

    ![Cuadro de función de Azure que muestra Elegir una función de Azure](media/functions-twitter-email/choose_fun.png)

3. <span data-ttu-id="18ee4-229">En **Cuerpo de la solicitud**, haga clic en **Puntuación** y, a continuación, en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="18ee4-229">In **Request Body**, click **Score** and then **Save**.</span></span>

    ![Score](media/functions-twitter-email/trigger_score.png)

<span data-ttu-id="18ee4-231">Ahora, la función se desencadena cuando se envía una puntuación de opiniones desde la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="18ee4-231">Now, your function is triggered when a sentiment score is sent from the logic app.</span></span> <span data-ttu-id="18ee4-232">La función devuelve una clasificación de códigos de color a la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="18ee4-232">A color-coded category is returned to the logic app by the function.</span></span> <span data-ttu-id="18ee4-233">A continuación, agregue una notificación por correo electrónico que se envía cuando la función devuelve un valor de opinión de **RED** (rojo).</span><span class="sxs-lookup"><span data-stu-id="18ee4-233">Next, you add an email notification that is sent when a sentiment value of **RED** is returned from the function.</span></span> 

## <a name="add-email-notifications"></a><span data-ttu-id="18ee4-234">Agregar notificaciones por correo electrónico</span><span class="sxs-lookup"><span data-stu-id="18ee4-234">Add email notifications</span></span>

<span data-ttu-id="18ee4-235">La última parte del flujo de trabajo consiste en desencadenar el envío de un correo electrónico cuando la opinión obtiene una puntuación _RED_ (rojo).</span><span class="sxs-lookup"><span data-stu-id="18ee4-235">The last part of the workflow is to trigger an email when the sentiment is scored as _RED_.</span></span> <span data-ttu-id="18ee4-236">Este tema utiliza un conector de Outlook.com.</span><span class="sxs-lookup"><span data-stu-id="18ee4-236">This topic uses an Outlook.com connector.</span></span> <span data-ttu-id="18ee4-237">Puede realizar pasos similares para utilizar un conector de Gmail o de Office 365 Outlook.</span><span class="sxs-lookup"><span data-stu-id="18ee4-237">You can perform similar steps to use a Gmail or Office 365 Outlook connector.</span></span>   

1. <span data-ttu-id="18ee4-238">En el diseñador de Logic Apps, haga clic en **Nuevo paso** > **Agregar una condición**.</span><span class="sxs-lookup"><span data-stu-id="18ee4-238">In the Logic Apps Designer, click **New step** > **Add a condition**.</span></span> 

2. <span data-ttu-id="18ee4-239">Haga clic en **Elegir un valor** y, a continuación, haga clic en **Cuerpo**.</span><span class="sxs-lookup"><span data-stu-id="18ee4-239">Click **Choose a value**, then click **Body**.</span></span> <span data-ttu-id="18ee4-240">Seleccione **Es igual a**, haga clic en **Elegir un valor**, escriba `RED` y haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="18ee4-240">Select **is equal to**, click **Choose a value** and type `RED`, and click **Save**.</span></span> 

    ![Agregar una condición a la aplicación lógica.](media/functions-twitter-email/condition.png)

3. <span data-ttu-id="18ee4-242">En **IF YES, DO NOTHING** (en caso afirmativo, no hacer nada), haga clic en **Agregar una acción**, busque `outlook.com`, haga clic en **Enviar un correo electrónico** e inicie sesión en su cuenta de Outlook.com.</span><span class="sxs-lookup"><span data-stu-id="18ee4-242">In **IF YES, DO NOTHING**, click **Add an action**, search for `outlook.com`, click **Send an email**, and sign in to your Outlook.com account.</span></span>
    
    ![Elegir una acción para la condición.](media/functions-twitter-email/outlook.png)

    > [!NOTE]
    > <span data-ttu-id="18ee4-244">Si no tiene una cuenta de Outlook.com, puede elegir otro conector, como Gmail u Office 365 Outlook</span><span class="sxs-lookup"><span data-stu-id="18ee4-244">If you don't have an Outlook.com account, you can choose another connector, such as Gmail or Office 365 Outlook</span></span>

4. <span data-ttu-id="18ee4-245">En la acción **Enviar un correo electrónico**, use la configuración de correo electrónico que se especifica en la tabla.</span><span class="sxs-lookup"><span data-stu-id="18ee4-245">In the **Send an email** action, use the email settings as specified in the table.</span></span> 

    ![Configure el correo electrónico para la acción de envío de correo electrónico.](media/functions-twitter-email/sendemail.png)

    | <span data-ttu-id="18ee4-247">Configuración</span><span class="sxs-lookup"><span data-stu-id="18ee4-247">Setting</span></span>      |  <span data-ttu-id="18ee4-248">Valor sugerido</span><span class="sxs-lookup"><span data-stu-id="18ee4-248">Suggested value</span></span>   | <span data-ttu-id="18ee4-249">Descripción</span><span class="sxs-lookup"><span data-stu-id="18ee4-249">Description</span></span>  |
    | ----------------- | ------------ | ------------- |
    | <span data-ttu-id="18ee4-250">**To**</span><span class="sxs-lookup"><span data-stu-id="18ee4-250">**To**</span></span> | <span data-ttu-id="18ee4-251">Escriba su dirección de correo electrónico</span><span class="sxs-lookup"><span data-stu-id="18ee4-251">Type your email address</span></span> | <span data-ttu-id="18ee4-252">La dirección de correo electrónico que recibe la notificación.</span><span class="sxs-lookup"><span data-stu-id="18ee4-252">The email address that receives the notification.</span></span> |
    | <span data-ttu-id="18ee4-253">**Asunto**</span><span class="sxs-lookup"><span data-stu-id="18ee4-253">**Subject**</span></span> | <span data-ttu-id="18ee4-254">Detectada opinión de tweet negativa</span><span class="sxs-lookup"><span data-stu-id="18ee4-254">Negative tweet sentiment detected</span></span>  | <span data-ttu-id="18ee4-255">La línea de asunto de la notificación de correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="18ee4-255">The subject line of the email notification.</span></span>  |
    | <span data-ttu-id="18ee4-256">**Cuerpo**</span><span class="sxs-lookup"><span data-stu-id="18ee4-256">**Body**</span></span> | <span data-ttu-id="18ee4-257">Texto de tweet, ubicación</span><span class="sxs-lookup"><span data-stu-id="18ee4-257">Tweet text, Location</span></span> | <span data-ttu-id="18ee4-258">Haga clic en los parámetros **Texto de tweet** y **Ubicación**.</span><span class="sxs-lookup"><span data-stu-id="18ee4-258">Click the **Tweet text** and **Location** parameters.</span></span> |

5.  <span data-ttu-id="18ee4-259">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="18ee4-259">Click **Save**.</span></span>

<span data-ttu-id="18ee4-260">Ahora que el flujo de trabajo se ha completado, puede habilitar la aplicación lógica y comprobar la ejecución de la función.</span><span class="sxs-lookup"><span data-stu-id="18ee4-260">Now that the workflow is complete, you can enable the logic app and see the function at work.</span></span>

## <a name="test-the-workflow"></a><span data-ttu-id="18ee4-261">Probar el flujo de trabajo</span><span class="sxs-lookup"><span data-stu-id="18ee4-261">Test the workflow</span></span>

1. <span data-ttu-id="18ee4-262">En el diseñador de Logic Apps, haga clic en **Ejecutar** para iniciar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="18ee4-262">In the Logic App Designer, click **Run** to start the app.</span></span>

2. <span data-ttu-id="18ee4-263">En la columna izquierda, haga clic en **Información general** para ver el estado de la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="18ee4-263">In the left column, click **Overview** to see the status of the logic app.</span></span> 
 
    ![Estado de ejecución de la aplicación lógica](media/functions-twitter-email/over1.png)

3. <span data-ttu-id="18ee4-265">(Opcional) Haga clic en una de las ejecuciones para ver los detalles de la ejecución.</span><span class="sxs-lookup"><span data-stu-id="18ee4-265">(Optional) Click one of the runs to see details of the execution.</span></span>

4. <span data-ttu-id="18ee4-266">Vaya a la función, vea los registros y compruebe que los valores de opinión se reciben y procesan.</span><span class="sxs-lookup"><span data-stu-id="18ee4-266">Go to your function, view the logs, and verify that sentiment values were received and processed.</span></span>
 
    ![Ver los registros de función](media/functions-twitter-email/sent.png)

5. <span data-ttu-id="18ee4-268">Cuando se detecta una opinión potencialmente negativa, recibirá un correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="18ee4-268">When a potentially negative sentiment is detected, you receive an email.</span></span> <span data-ttu-id="18ee4-269">Si no ha recibido un correo electrónico, puede cambiar el código de la función para devolver siempre RED (rojo):</span><span class="sxs-lookup"><span data-stu-id="18ee4-269">If you haven't received an email, you can change the function code to return RED every time:</span></span>

        return req.CreateResponse(HttpStatusCode.OK, "RED");

    <span data-ttu-id="18ee4-270">Después de comprobar las notificaciones de correo electrónico, vuelva a cambiar al código original:</span><span class="sxs-lookup"><span data-stu-id="18ee4-270">After you have verified email notifications, change back to the original code:</span></span>

        return req.CreateResponse(HttpStatusCode.OK, category);

    > [!IMPORTANT]
    > <span data-ttu-id="18ee4-271">Después de completar este tutorial, debe deshabilitar la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="18ee4-271">After you have completed this tutorial, you should disable the logic app.</span></span> <span data-ttu-id="18ee4-272">Al deshabilitar la aplicación, evita recibir cargos por ejecuciones y agotar las transacciones de la cuenta de Cognitive Services.</span><span class="sxs-lookup"><span data-stu-id="18ee4-272">By disabling the app, you avoid being charged for executions and using up the transactions in your Cognitive Services account.</span></span>

<span data-ttu-id="18ee4-273">Ya ha visto lo fácil que es integrar Functions en un flujo de trabajo de Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="18ee4-273">Now you have seen how easy it is to integrate Functions into a Logic Apps workflow.</span></span>

## <a name="disable-the-logic-app"></a><span data-ttu-id="18ee4-274">Deshabilitar la aplicación lógica</span><span class="sxs-lookup"><span data-stu-id="18ee4-274">Disable the logic app</span></span>

<span data-ttu-id="18ee4-275">Para deshabilitar la aplicación lógica, haga clic en **Información general** y, a continuación, haga clic en **Deshabilitar** en la parte superior de la pantalla.</span><span class="sxs-lookup"><span data-stu-id="18ee4-275">To disable the logic app, click **Overview** and then click **Disable** at the top of the screen.</span></span> <span data-ttu-id="18ee4-276">Esto detiene la ejecución de la aplicación lógica y evita incurrir en cargos sin eliminar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="18ee4-276">This stops the logic app from running and incurring charges without deleting the app.</span></span> 

![Registros de la función](media/functions-twitter-email/disable-logic-app.png)

## <a name="next-steps"></a><span data-ttu-id="18ee4-278">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="18ee4-278">Next steps</span></span>

<span data-ttu-id="18ee4-279">En este tutorial, ha aprendido cómo:</span><span class="sxs-lookup"><span data-stu-id="18ee4-279">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="18ee4-280">Cree una cuenta de Cognitive Services.</span><span class="sxs-lookup"><span data-stu-id="18ee4-280">Create a Cognitive Services account.</span></span>
> * <span data-ttu-id="18ee4-281">Crear una función que clasifica las opiniones de tweet.</span><span class="sxs-lookup"><span data-stu-id="18ee4-281">Create a function that categorizes tweet sentiment.</span></span>
> * <span data-ttu-id="18ee4-282">Crear una aplicación de lógica que se conecta a Twitter.</span><span class="sxs-lookup"><span data-stu-id="18ee4-282">Create a logic app that connects to Twitter.</span></span>
> * <span data-ttu-id="18ee4-283">Agregar detección de opiniones a la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="18ee4-283">Add sentiment detection to the logic app.</span></span> 
> * <span data-ttu-id="18ee4-284">Conectar la aplicación lógica a la función.</span><span class="sxs-lookup"><span data-stu-id="18ee4-284">Connect the logic app to the function.</span></span>
> * <span data-ttu-id="18ee4-285">Enviar un correo electrónico en función de la respuesta de la función.</span><span class="sxs-lookup"><span data-stu-id="18ee4-285">Send an email based on the response from the function.</span></span>

<span data-ttu-id="18ee4-286">Continúe con el siguiente tutorial para aprender a crear una API sin servidor para la función.</span><span class="sxs-lookup"><span data-stu-id="18ee4-286">Advance to the next tutorial to learn how to create a serverless API for your function.</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="18ee4-287">Creación de una API sin servidor mediante Azure Functions</span><span class="sxs-lookup"><span data-stu-id="18ee4-287">Create a serverless API using Azure Functions</span></span>](functions-create-serverless-api.md)

<span data-ttu-id="18ee4-288">Para más información acerca de Logic Apps, consulte [Azure Logic Apps](../logic-apps/logic-apps-what-are-logic-apps.md).</span><span class="sxs-lookup"><span data-stu-id="18ee4-288">To learn more about Logic Apps, see [Azure Logic Apps](../logic-apps/logic-apps-what-are-logic-apps.md).</span></span>

