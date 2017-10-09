---
title: "una función que se integra con aplicaciones de Azure lógica aaaCreate | Documentos de Microsoft"
description: "Crear una función que se integra con las aplicaciones lógicas de Azure y Azure cognitivos servicios opiniones de tweet toocategorize y enviar notificaciones cuando opinión es deficiente."
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
ms.openlocfilehash: e176bd946af9a3684b3ad0e4b1bed1c3ee344019
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-that-integrates-with-azure-logic-apps"></a><span data-ttu-id="18e77-104">Creación de una función que se integre con Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="18e77-104">Create a function that integrates with Azure Logic Apps</span></span>

<span data-ttu-id="18e77-105">Funciones de Azure se integra con aplicaciones de Azure lógica de Hola Diseñador de aplicaciones de la lógica.</span><span class="sxs-lookup"><span data-stu-id="18e77-105">Azure Functions integrates with Azure Logic Apps in hello Logic Apps Designer.</span></span> <span data-ttu-id="18e77-106">Esta integración permite usar hello capacidad de ejecución de funciones en las orquestaciones con otros servicios de terceros y Azure.</span><span class="sxs-lookup"><span data-stu-id="18e77-106">This integration lets you use hello computing power of Functions in orchestrations with other Azure and third-party services.</span></span> 

<span data-ttu-id="18e77-107">Este tutorial muestra cómo las funciones toouse con lógica de aplicaciones y servicios de Azure cognitivos opiniones tooanalyze de entradas de Twitter.</span><span class="sxs-lookup"><span data-stu-id="18e77-107">This tutorial shows you how toouse Functions with Logic Apps and Azure Cognitive Services tooanalyze sentiment from Twitter posts.</span></span> <span data-ttu-id="18e77-108">Una función HTTP desencadenada clasifica tweets como verde, amarillo o rojo en función de puntuación de opiniones Hola.</span><span class="sxs-lookup"><span data-stu-id="18e77-108">An HTTP triggered function categorizes tweets as green, yellow, or red based on hello sentiment score.</span></span> <span data-ttu-id="18e77-109">Se envía un correo electrónico cuando se detecta una opinión deficiente.</span><span class="sxs-lookup"><span data-stu-id="18e77-109">An email is sent when poor sentiment is detected.</span></span> 

![imagen de los dos primeros pasos de una aplicación en el diseñador de Logic Apps](media/functions-twitter-email/designer1.png)

<span data-ttu-id="18e77-111">En este tutorial, aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="18e77-111">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="18e77-112">Cree una cuenta de Cognitive Services.</span><span class="sxs-lookup"><span data-stu-id="18e77-112">Create a Cognitive Services account.</span></span>
> * <span data-ttu-id="18e77-113">Crear una función que clasifica las opiniones de tweet.</span><span class="sxs-lookup"><span data-stu-id="18e77-113">Create a function that categorizes tweet sentiment.</span></span>
> * <span data-ttu-id="18e77-114">Crear una aplicación de lógica que se conecta tooTwitter.</span><span class="sxs-lookup"><span data-stu-id="18e77-114">Create a logic app that connects tooTwitter.</span></span>
> * <span data-ttu-id="18e77-115">Agregar aplicación de lógica de toohello de detección de opinión.</span><span class="sxs-lookup"><span data-stu-id="18e77-115">Add sentiment detection toohello logic app.</span></span> 
> * <span data-ttu-id="18e77-116">Se conectan Hola lógica aplicación toohello funcionan.</span><span class="sxs-lookup"><span data-stu-id="18e77-116">Connect hello logic app toohello function.</span></span>
> * <span data-ttu-id="18e77-117">Enviar un correo electrónico en función de la respuesta de Hola de función hello.</span><span class="sxs-lookup"><span data-stu-id="18e77-117">Send an email based on hello response from hello function.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="18e77-118">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="18e77-118">Prerequisites</span></span>

+ <span data-ttu-id="18e77-119">Una cuenta de [Twitter](https://twitter.com/) activa.</span><span class="sxs-lookup"><span data-stu-id="18e77-119">An active [Twitter](https://twitter.com/) account.</span></span> 
+ <span data-ttu-id="18e77-120">Una cuenta de [Outlook.com](https://outlook.com/) (para enviar las notificaciones).</span><span class="sxs-lookup"><span data-stu-id="18e77-120">An [Outlook.com](https://outlook.com/) account (for sending notifications).</span></span>
+ <span data-ttu-id="18e77-121">Este tema se utiliza como sus recursos de Hola de punto de partida creados en [crear la primera función de hello portal de Azure](functions-create-first-azure-function.md).</span><span class="sxs-lookup"><span data-stu-id="18e77-121">This topic uses as its starting point hello resources created in [Create your first function from hello Azure portal](functions-create-first-azure-function.md).</span></span>  
<span data-ttu-id="18e77-122">Si aún no lo ha hecho, complete estos toocreate ahora de pasos de la aplicación de la función.</span><span class="sxs-lookup"><span data-stu-id="18e77-122">If you haven't already done so, complete these steps now toocreate your function app.</span></span>

## <a name="create-a-cognitive-services-account"></a><span data-ttu-id="18e77-123">Creación de una cuenta de Cognitive Services</span><span class="sxs-lookup"><span data-stu-id="18e77-123">Create a Cognitive Services account</span></span>

<span data-ttu-id="18e77-124">Una cuenta de servicios cognitivos es necesario toodetect Hola opiniones de tweets de que se está supervisando.</span><span class="sxs-lookup"><span data-stu-id="18e77-124">A Cognitive Services account is required toodetect hello sentiment of tweets being monitored.</span></span>

1. <span data-ttu-id="18e77-125">Inicie sesión en toohello [portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="18e77-125">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>

2. <span data-ttu-id="18e77-126">Haga clic en hello **New** encontró el botón en la esquina izquierda superior de Hola de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="18e77-126">Click hello **New** button found on hello upper left-hand corner of hello Azure portal.</span></span>

3. <span data-ttu-id="18e77-127">Haga clic en **Datos y análisis** > **Cognitive Services**.</span><span class="sxs-lookup"><span data-stu-id="18e77-127">Click **Data + Analytics** > **Cognitive  Services**.</span></span> <span data-ttu-id="18e77-128">A continuación, usar la configuración de hello como especificado en la tabla de hello, acepte los términos de Hola y compruebe **toodashboard Pin**.</span><span class="sxs-lookup"><span data-stu-id="18e77-128">Then, use hello settings as specified in hello table, accept hello terms, and check **Pin toodashboard**.</span></span>

    ![Hoja para crear cuenta de Cognitive Services](media/functions-twitter-email/cog_svcs_account.png)

    | <span data-ttu-id="18e77-130">Configuración</span><span class="sxs-lookup"><span data-stu-id="18e77-130">Setting</span></span>      |  <span data-ttu-id="18e77-131">Valor sugerido</span><span class="sxs-lookup"><span data-stu-id="18e77-131">Suggested value</span></span>   | <span data-ttu-id="18e77-132">Descripción</span><span class="sxs-lookup"><span data-stu-id="18e77-132">Description</span></span>                                        |
    | --- | --- | --- |
    | <span data-ttu-id="18e77-133">**Name**</span><span class="sxs-lookup"><span data-stu-id="18e77-133">**Name**</span></span> | <span data-ttu-id="18e77-134">MyCognitiveServicesAccnt</span><span class="sxs-lookup"><span data-stu-id="18e77-134">MyCognitiveServicesAccnt</span></span> | <span data-ttu-id="18e77-135">Elija un nombre de cuenta único.</span><span class="sxs-lookup"><span data-stu-id="18e77-135">Choose a unique account name.</span></span> |
    | <span data-ttu-id="18e77-136">**Tipo de API**</span><span class="sxs-lookup"><span data-stu-id="18e77-136">**API type**</span></span> | <span data-ttu-id="18e77-137">Text Analytics API</span><span class="sxs-lookup"><span data-stu-id="18e77-137">Text Analytics API</span></span> | <span data-ttu-id="18e77-138">API usar texto tooanalyze.</span><span class="sxs-lookup"><span data-stu-id="18e77-138">API used tooanalyze text.</span></span>  |
    | <span data-ttu-id="18e77-139">**Ubicación**</span><span class="sxs-lookup"><span data-stu-id="18e77-139">**Location**</span></span> | <span data-ttu-id="18e77-140">Oeste de EE. UU.</span><span class="sxs-lookup"><span data-stu-id="18e77-140">West US</span></span> | <span data-ttu-id="18e77-141">Actualmente, solo está disponible **Oeste de EE. UU.** para análisis de texto.</span><span class="sxs-lookup"><span data-stu-id="18e77-141">Currently, only **West US** is available for text analytics.</span></span> |
    | <span data-ttu-id="18e77-142">**Plan de tarifa**</span><span class="sxs-lookup"><span data-stu-id="18e77-142">**Pricing tier**</span></span> | <span data-ttu-id="18e77-143">F0</span><span class="sxs-lookup"><span data-stu-id="18e77-143">F0</span></span> | <span data-ttu-id="18e77-144">Comience con el nivel más bajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="18e77-144">Start with hello lowest tier.</span></span> <span data-ttu-id="18e77-145">Si se queda sin llamadas, escalar tooa de nivel superior.</span><span class="sxs-lookup"><span data-stu-id="18e77-145">If you run out of calls, scale tooa higher tier.</span></span>|
    | <span data-ttu-id="18e77-146">**Grupos de recursos**</span><span class="sxs-lookup"><span data-stu-id="18e77-146">**Resource group**</span></span> | <span data-ttu-id="18e77-147">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="18e77-147">myResourceGroup</span></span> | <span data-ttu-id="18e77-148">Use Hola mismo grupo de recursos para todos los servicios en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="18e77-148">Use hello same resource group for all services in this tutorial.</span></span>|

4. <span data-ttu-id="18e77-149">Haga clic en **crear** toocreate su cuenta.</span><span class="sxs-lookup"><span data-stu-id="18e77-149">Click **Create** toocreate your account.</span></span> <span data-ttu-id="18e77-150">Una vez creada la cuenta de hello, haga clic en el nuevo panel de toohello anclados de cuenta de servicios cognitivos.</span><span class="sxs-lookup"><span data-stu-id="18e77-150">After hello account is created, click your new Cognitive Services account pinned toohello dashboard.</span></span> 

5. <span data-ttu-id="18e77-151">En la cuenta de hello, haga clic en **claves**y a continuación, copie el valor de Hola de **clave 1** y guárdelo.</span><span class="sxs-lookup"><span data-stu-id="18e77-151">In hello account, click **Keys**, and then copy hello value of **Key 1** and save it.</span></span> <span data-ttu-id="18e77-152">Utilice este tooyour de aplicación de lógica de hello tooconnect clave cuenta Services cognitivos.</span><span class="sxs-lookup"><span data-stu-id="18e77-152">You use this key tooconnect hello logic app tooyour Cognitive Services account.</span></span> 
 
    ![simétricas](media/functions-twitter-email/keys.png)

## <a name="create-hello-function"></a><span data-ttu-id="18e77-154">Crear función hello</span><span class="sxs-lookup"><span data-stu-id="18e77-154">Create hello function</span></span>

<span data-ttu-id="18e77-155">Funciones proporciona un toooffload excelente manera tareas de procesamiento en un flujo de trabajo de aplicaciones de la lógica.</span><span class="sxs-lookup"><span data-stu-id="18e77-155">Functions provides a great way toooffload processing tasks in a logic apps workflow.</span></span> <span data-ttu-id="18e77-156">Este tutorial usa un HTTP desencadena función tooprocess tweet opiniones las puntuaciones de servicios cognitivos y devolver un valor de categoría.</span><span class="sxs-lookup"><span data-stu-id="18e77-156">This tutorial uses an HTTP triggered function tooprocess tweet sentiment scores from Cognitive Services and return a category value.</span></span>  

1. <span data-ttu-id="18e77-157">Expanda la aplicación de la función, haga clic en hello  **+**  aparece al lado demasiado**funciones**, haga clic en hello **HTTPTrigger** plantilla.</span><span class="sxs-lookup"><span data-stu-id="18e77-157">Expand your function app, click hello **+** button next too**Functions**, click hello **HTTPTrigger** template.</span></span> <span data-ttu-id="18e77-158">Tipo de `CategorizeSentiment` para la función hello **nombre** y haga clic en **crear**.</span><span class="sxs-lookup"><span data-stu-id="18e77-158">Type `CategorizeSentiment` for hello function **Name** and click **Create**.</span></span>

    ![Hoja Instancias de Function App, Functions +](media/functions-twitter-email/add_fun.png)

2. <span data-ttu-id="18e77-160">Reemplace el contenido de Hola de archivo de hello run.csx con el siguiente código de hello, a continuación, haga clic en **guardar**:</span><span class="sxs-lookup"><span data-stu-id="18e77-160">Replace hello contents of hello run.csx file with hello following code, then click **Save**:</span></span>

    ```c#
    using System.Net;
    
    public static async Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
    {
        // hello sentiment category defaults too'GREEN'. 
        string category = "GREEN";
    
        // Get hello sentiment score from hello request body.
        double score = await req.Content.ReadAsAsync<double>();
        log.Info(string.Format("hello sentiment score received is '{0}'.",
                    score.ToString()));
    
        // Set hello category based on hello sentiment score.
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
    <span data-ttu-id="18e77-161">Este código de la función devuelve una categoría de color en función de puntuación de opiniones Hola recibidos en la solicitud de saludo.</span><span class="sxs-lookup"><span data-stu-id="18e77-161">This function code returns a color category based on hello sentiment score received in hello request.</span></span> 

3. <span data-ttu-id="18e77-162">función de hello tootest, haga clic en **prueba** en la ficha de prueba de Hola Hola tooexpand más a la derecha. Escriba un valor de `0.2` para hello **cuerpo de la solicitud**y, a continuación, haga clic en **ejecutar**.</span><span class="sxs-lookup"><span data-stu-id="18e77-162">tootest hello function, click **Test** at hello far right tooexpand hello Test tab. Type a value of `0.2` for hello **Request body**, and then click **Run**.</span></span> <span data-ttu-id="18e77-163">Un valor de **rojo** se devuelve en hello cuerpo de respuesta de Hola.</span><span class="sxs-lookup"><span data-stu-id="18e77-163">A value of **RED** is returned in hello body of hello response.</span></span> 

    ![Probar función hello en hello portal de Azure](./media/functions-twitter-email/test.png)

<span data-ttu-id="18e77-165">Ahora, tiene una función que clasifica las puntuaciones de opinión.</span><span class="sxs-lookup"><span data-stu-id="18e77-165">Now you have a function that categorizes sentiment scores.</span></span> <span data-ttu-id="18e77-166">A continuación, cree una aplicación lógica que integre la función con las cuentas de Twitter y Cognitive Services.</span><span class="sxs-lookup"><span data-stu-id="18e77-166">Next, you create a logic app that integrates your function with your Twitter and Cognitive Services accounts.</span></span> 

## <a name="create-a-logic-app"></a><span data-ttu-id="18e77-167">Creación de una aplicación lógica</span><span class="sxs-lookup"><span data-stu-id="18e77-167">Create a logic app</span></span>   

1. <span data-ttu-id="18e77-168">En el Hola portal de Azure, haga clic en hello **New** encontró el botón en la esquina izquierda superior de Hola de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="18e77-168">In hello Azure portal, click hello **New** button found on hello upper left-hand corner of hello Azure portal.</span></span>

2. <span data-ttu-id="18e77-169">Haga clic en **Integración empresarial** > **Aplicación lógica**.</span><span class="sxs-lookup"><span data-stu-id="18e77-169">Click **Enterprise Integration** > **Logic App**.</span></span> <span data-ttu-id="18e77-170">A continuación, usar la configuración de hello como especificado en la tabla de hello, compruebe **Pin toodashboard**y haga clic en **crear**.</span><span class="sxs-lookup"><span data-stu-id="18e77-170">Then, use hello settings as specified in hello table, check **Pin toodashboard**, and click **Create**.</span></span>
 
4. <span data-ttu-id="18e77-171">A continuación, escriba un **nombre** como `TweetSentiment`, usar la configuración de hello como se especifica en la tabla de hello, acepte los términos de Hola y comprobar **toodashboard Pin**.</span><span class="sxs-lookup"><span data-stu-id="18e77-171">Then, type a **Name** like `TweetSentiment`,  use hello settings as specified in hello table, accept hello terms, and check **Pin toodashboard**.</span></span>

    ![Crear aplicación lógica en hello portal de Azure](./media/functions-twitter-email/new_logicApp.png)

    | <span data-ttu-id="18e77-173">Configuración</span><span class="sxs-lookup"><span data-stu-id="18e77-173">Setting</span></span>      |  <span data-ttu-id="18e77-174">Valor sugerido</span><span class="sxs-lookup"><span data-stu-id="18e77-174">Suggested value</span></span>   | <span data-ttu-id="18e77-175">Descripción</span><span class="sxs-lookup"><span data-stu-id="18e77-175">Description</span></span>                                        |
    | ----------------- | ------------ | ------------- |
    | <span data-ttu-id="18e77-176">**Name**</span><span class="sxs-lookup"><span data-stu-id="18e77-176">**Name**</span></span> | <span data-ttu-id="18e77-177">TweetSentiment</span><span class="sxs-lookup"><span data-stu-id="18e77-177">TweetSentiment</span></span> | <span data-ttu-id="18e77-178">Elija un nombre adecuado para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="18e77-178">Choose an appropriate name for your app.</span></span> |
    | <span data-ttu-id="18e77-179">**Grupos de recursos**</span><span class="sxs-lookup"><span data-stu-id="18e77-179">**Resource group**</span></span> | <span data-ttu-id="18e77-180">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="18e77-180">myResourceGroup</span></span> | <span data-ttu-id="18e77-181">API usar texto tooanalyze.</span><span class="sxs-lookup"><span data-stu-id="18e77-181">API used tooanalyze text.</span></span>  |
    | <span data-ttu-id="18e77-182">**Ubicación**</span><span class="sxs-lookup"><span data-stu-id="18e77-182">**Location**</span></span> | <span data-ttu-id="18e77-183">Este de EE. UU.</span><span class="sxs-lookup"><span data-stu-id="18e77-183">East US</span></span> | <span data-ttu-id="18e77-184">Elija un tooyou de cierre de ubicación.</span><span class="sxs-lookup"><span data-stu-id="18e77-184">Choose a location close tooyou.</span></span> |
    | <span data-ttu-id="18e77-185">**Grupos de recursos**</span><span class="sxs-lookup"><span data-stu-id="18e77-185">**Resource group**</span></span> | <span data-ttu-id="18e77-186">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="18e77-186">myResourceGroup</span></span> | <span data-ttu-id="18e77-187">Elija Hola el mismo grupo de recursos existente como antes.</span><span class="sxs-lookup"><span data-stu-id="18e77-187">Choose hello same existing resource group as before.</span></span>|

4. <span data-ttu-id="18e77-188">Haga clic en **crear** toocreate la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="18e77-188">Click **Create** toocreate your logic app.</span></span> <span data-ttu-id="18e77-189">Después de crea la aplicación hello, haga clic en el nuevo panel de toohello anclados de aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="18e77-189">After hello app is created, click your new logic app pinned toohello dashboard.</span></span> <span data-ttu-id="18e77-190">A continuación, en hello lógica el Diseñador de aplicaciones, desplácese hacia abajo y haga clic en hello **en blanco de lógica de aplicación** plantilla.</span><span class="sxs-lookup"><span data-stu-id="18e77-190">Then in hello Logic Apps Designer, scroll down and click hello **Blank Logic App** template.</span></span> 

    ![Plantilla Aplicación lógica en blanco](media/functions-twitter-email/blank.png)

<span data-ttu-id="18e77-192">Ahora puede usar el Diseñador de aplicaciones de la lógica tooadd servicios y desencadenadores tooyour aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="18e77-192">You can now use hello Logic Apps Designer tooadd services and triggers tooyour app.</span></span>

## <a name="connect-tootwitter"></a><span data-ttu-id="18e77-193">Conectar tooTwitter</span><span class="sxs-lookup"><span data-stu-id="18e77-193">Connect tooTwitter</span></span>

<span data-ttu-id="18e77-194">En primer lugar, cree una cuenta de Twitter tooyour de conexión.</span><span class="sxs-lookup"><span data-stu-id="18e77-194">First, create a connection tooyour Twitter account.</span></span> <span data-ttu-id="18e77-195">aplicación de la lógica de Hello sondea tweets, que desencadenen hello toorun de aplicación.</span><span class="sxs-lookup"><span data-stu-id="18e77-195">hello logic app polls for tweets, which trigger hello app toorun.</span></span>

1. <span data-ttu-id="18e77-196">En el Diseñador de hello, haga clic en hello **Twitter** de servicio y haga clic en hello **cuando se registra un nuevo tweet** desencadenador.</span><span class="sxs-lookup"><span data-stu-id="18e77-196">In hello designer, click hello **Twitter** service, and click hello **When a new tweet is posted** trigger.</span></span> <span data-ttu-id="18e77-197">Inicie sesión en tooyour cuenta de Twitter y autorizar aplicaciones lógicas toouse tu cuenta.</span><span class="sxs-lookup"><span data-stu-id="18e77-197">Sign in tooyour Twitter account and authorize Logic Apps toouse your account.</span></span>

2. <span data-ttu-id="18e77-198">Use la configuración de desencadenador de Twitter de hello como se especifica en la tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="18e77-198">Use hello Twitter trigger settings as specified in hello table.</span></span> 

    ![Configuración del conector de Twitter](media/functions-twitter-email/azure_tweet.png)

    | <span data-ttu-id="18e77-200">Configuración</span><span class="sxs-lookup"><span data-stu-id="18e77-200">Setting</span></span>      |  <span data-ttu-id="18e77-201">Valor sugerido</span><span class="sxs-lookup"><span data-stu-id="18e77-201">Suggested value</span></span>   | <span data-ttu-id="18e77-202">Descripción</span><span class="sxs-lookup"><span data-stu-id="18e77-202">Description</span></span>                                        |
    | ----------------- | ------------ | ------------- |
    | <span data-ttu-id="18e77-203">**Texto de búsqueda**</span><span class="sxs-lookup"><span data-stu-id="18e77-203">**Search text**</span></span> | <span data-ttu-id="18e77-204">#Azure</span><span class="sxs-lookup"><span data-stu-id="18e77-204">#Azure</span></span> | <span data-ttu-id="18e77-205">Use una hashtag que sea lo suficientemente popular para toogenerate nueva tweets en intervalo de saludo elegido.</span><span class="sxs-lookup"><span data-stu-id="18e77-205">Use a hashtag that is popular enough for toogenerate new tweets in hello chosen interval.</span></span> <span data-ttu-id="18e77-206">Al utilizar el nivel gratuito de Hola y su hashtag es demasiado popular, puede usar rápidamente las transacciones de hello en su cuenta de servicios cognitivos.</span><span class="sxs-lookup"><span data-stu-id="18e77-206">When using hello Free tier and your hashtag is too popular, you can quickly use up hello transactions in your Cognitive Services account.</span></span> |
    | <span data-ttu-id="18e77-207">**Frecuencia**</span><span class="sxs-lookup"><span data-stu-id="18e77-207">**Frequency**</span></span> | <span data-ttu-id="18e77-208">Minuto</span><span class="sxs-lookup"><span data-stu-id="18e77-208">Minute</span></span> | <span data-ttu-id="18e77-209">unidad de frecuencia de Hello utilizada para el sondeo de Twitter.</span><span class="sxs-lookup"><span data-stu-id="18e77-209">hello frequency unit used for polling Twitter.</span></span>  |
    | <span data-ttu-id="18e77-210">**Intervalo**</span><span class="sxs-lookup"><span data-stu-id="18e77-210">**Interval**</span></span> | <span data-ttu-id="18e77-211">15</span><span class="sxs-lookup"><span data-stu-id="18e77-211">15</span></span> | <span data-ttu-id="18e77-212">tiempo de Hello transcurrido entre las solicitudes de Twitter, en unidades de frecuencia.</span><span class="sxs-lookup"><span data-stu-id="18e77-212">hello time elapsed between Twitter requests, in frequency units.</span></span> |

3.  <span data-ttu-id="18e77-213">Haga clic en **guardar** tooconnect tooyour cuenta de Twitter.</span><span class="sxs-lookup"><span data-stu-id="18e77-213">Click **Save** tooconnect tooyour Twitter account.</span></span> 

<span data-ttu-id="18e77-214">Ahora, la aplicación es tooTwitter conectado.</span><span class="sxs-lookup"><span data-stu-id="18e77-214">Now your app is connected tooTwitter.</span></span> <span data-ttu-id="18e77-215">A continuación, conectar opiniones de tootext análisis toodetect Hola de tweets recopilados.</span><span class="sxs-lookup"><span data-stu-id="18e77-215">Next, you connect tootext analytics toodetect hello sentiment of collected tweets.</span></span>

## <a name="add-sentiment-detection"></a><span data-ttu-id="18e77-216">Agregar la detección de opiniones</span><span class="sxs-lookup"><span data-stu-id="18e77-216">Add sentiment detection</span></span>

1. <span data-ttu-id="18e77-217">Haga clic en **Nuevo paso** y, a continuación, en **Agregar una acción**.</span><span class="sxs-lookup"><span data-stu-id="18e77-217">Click **New Step**, and then **Add an action**.</span></span>

    ![Nuevo paso y Agregar una acción](media/functions-twitter-email/new_step.png)

2. <span data-ttu-id="18e77-219">En **elegir una acción**, haga clic en **análisis de texto**y, a continuación, haga clic en hello **detectar opiniones** acción.</span><span class="sxs-lookup"><span data-stu-id="18e77-219">In **Choose an action**, click **Text Analytics**, and then click hello **Detect sentiment** action.</span></span>

    ![Detectar sentimiento](media/functions-twitter-email/detect_sent.png)

3. <span data-ttu-id="18e77-221">Escriba un nombre de conexión como `MyCognitiveServicesConnection`, pegue la clave de Hola para los servicios cognitivos cuenta que ha guardado y haga clic en **crear**.</span><span class="sxs-lookup"><span data-stu-id="18e77-221">Type a connection name such as `MyCognitiveServicesConnection`, paste hello key for your Cognitive Services account that you saved, and click **Create**.</span></span>  

4. <span data-ttu-id="18e77-222">Haga clic en **tooanalyze de texto** > **Tweet texto**y, a continuación, haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="18e77-222">Click **Text tooanalyze** > **Tweet text**, and then click **Save**.</span></span>  

    ![Detectar sentimiento](media/functions-twitter-email/ds_tta.png)

<span data-ttu-id="18e77-224">Ahora que se configura la detección de opinión, puede agregar una función de tooyour de conexión que usa Hola opiniones puntuación resultado.</span><span class="sxs-lookup"><span data-stu-id="18e77-224">Now that sentiment detection is configured, you can add a connection tooyour function that consumes hello sentiment score output.</span></span>

## <a name="connect-sentiment-output-tooyour-function"></a><span data-ttu-id="18e77-225">Conectar opiniones salida tooyour función</span><span class="sxs-lookup"><span data-stu-id="18e77-225">Connect sentiment output tooyour function</span></span>

1. <span data-ttu-id="18e77-226">Hola lógica el Diseñador de aplicaciones, haga clic en **nuevo paso** > **agregar una acción**y, a continuación, haga clic en **funciones de Azure**.</span><span class="sxs-lookup"><span data-stu-id="18e77-226">In hello Logic Apps Designer, click **New step** > **Add an action**, and then click **Azure Functions**.</span></span> 

2. <span data-ttu-id="18e77-227">Haga clic en **elegir una función de Azure**, seleccione hello **CategorizeSentiment** función que ha creado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="18e77-227">Click **Choose an Azure function**, select hello **CategorizeSentiment** function you created earlier.</span></span>  

    ![Cuadro de función de Azure que muestra Elegir una función de Azure](media/functions-twitter-email/choose_fun.png)

3. <span data-ttu-id="18e77-229">En **Cuerpo de la solicitud**, haga clic en **Puntuación** y, a continuación, en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="18e77-229">In **Request Body**, click **Score** and then **Save**.</span></span>

    ![Score](media/functions-twitter-email/trigger_score.png)

<span data-ttu-id="18e77-231">Ahora, la función se desencadena cuando se envía una puntuación de opinión de aplicación lógica de hello.</span><span class="sxs-lookup"><span data-stu-id="18e77-231">Now, your function is triggered when a sentiment score is sent from hello logic app.</span></span> <span data-ttu-id="18e77-232">Una categoría codificado por colores devuelto toohello lógica aplicación por función hello.</span><span class="sxs-lookup"><span data-stu-id="18e77-232">A color-coded category is returned toohello logic app by hello function.</span></span> <span data-ttu-id="18e77-233">A continuación, agregue una notificación de correo electrónico que se envía cuando el valor de una opinión de **rojo** devuelta por la función de Hola.</span><span class="sxs-lookup"><span data-stu-id="18e77-233">Next, you add an email notification that is sent when a sentiment value of **RED** is returned from hello function.</span></span> 

## <a name="add-email-notifications"></a><span data-ttu-id="18e77-234">Agregar notificaciones por correo electrónico</span><span class="sxs-lookup"><span data-stu-id="18e77-234">Add email notifications</span></span>

<span data-ttu-id="18e77-235">Hola última parte del flujo de trabajo de hello es tootrigger un correo electrónico cuando se usa para puntuar opiniones hello como _rojo_.</span><span class="sxs-lookup"><span data-stu-id="18e77-235">hello last part of hello workflow is tootrigger an email when hello sentiment is scored as _RED_.</span></span> <span data-ttu-id="18e77-236">Este tema utiliza un conector de Outlook.com.</span><span class="sxs-lookup"><span data-stu-id="18e77-236">This topic uses an Outlook.com connector.</span></span> <span data-ttu-id="18e77-237">Puede realizar similar pasos toouse un conector Gmail o Outlook de Office 365.</span><span class="sxs-lookup"><span data-stu-id="18e77-237">You can perform similar steps toouse a Gmail or Office 365 Outlook connector.</span></span>   

1. <span data-ttu-id="18e77-238">Hola lógica el Diseñador de aplicaciones, haga clic en **nuevo paso** > **agregar una condición**.</span><span class="sxs-lookup"><span data-stu-id="18e77-238">In hello Logic Apps Designer, click **New step** > **Add a condition**.</span></span> 

2. <span data-ttu-id="18e77-239">Haga clic en **Elegir un valor** y, a continuación, haga clic en **Cuerpo**.</span><span class="sxs-lookup"><span data-stu-id="18e77-239">Click **Choose a value**, then click **Body**.</span></span> <span data-ttu-id="18e77-240">Seleccione **Es igual a**, haga clic en **Elegir un valor**, escriba `RED` y haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="18e77-240">Select **is equal to**, click **Choose a value** and type `RED`, and click **Save**.</span></span> 

    ![Agregar una aplicación de lógica de toohello de condición.](media/functions-twitter-email/condition.png)

3. <span data-ttu-id="18e77-242">En **si es así, no hacen nada**, haga clic en **agregar una acción**, busque `outlook.com`, haga clic en **enviar un correo electrónico**e inicie sesión en tooyour cuenta de Outlook.com.</span><span class="sxs-lookup"><span data-stu-id="18e77-242">In **IF YES, DO NOTHING**, click **Add an action**, search for `outlook.com`, click **Send an email**, and sign in tooyour Outlook.com account.</span></span>
    
    ![Elegir una acción para la condición de Hola.](media/functions-twitter-email/outlook.png)

    > [!NOTE]
    > <span data-ttu-id="18e77-244">Si no tiene una cuenta de Outlook.com, puede elegir otro conector, como Gmail u Office 365 Outlook</span><span class="sxs-lookup"><span data-stu-id="18e77-244">If you don't have an Outlook.com account, you can choose another connector, such as Gmail or Office 365 Outlook</span></span>

4. <span data-ttu-id="18e77-245">Hola **enviar un correo electrónico** acción, usar la configuración de correo electrónico de hello como especificada en la tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="18e77-245">In hello **Send an email** action, use hello email settings as specified in hello table.</span></span> 

    ![Configurar el correo electrónico de hello para el envío de hello una acción de correo electrónico.](media/functions-twitter-email/sendemail.png)

    | <span data-ttu-id="18e77-247">Configuración</span><span class="sxs-lookup"><span data-stu-id="18e77-247">Setting</span></span>      |  <span data-ttu-id="18e77-248">Valor sugerido</span><span class="sxs-lookup"><span data-stu-id="18e77-248">Suggested value</span></span>   | <span data-ttu-id="18e77-249">Descripción</span><span class="sxs-lookup"><span data-stu-id="18e77-249">Description</span></span>  |
    | ----------------- | ------------ | ------------- |
    | <span data-ttu-id="18e77-250">**To**</span><span class="sxs-lookup"><span data-stu-id="18e77-250">**To**</span></span> | <span data-ttu-id="18e77-251">Escriba su dirección de correo electrónico</span><span class="sxs-lookup"><span data-stu-id="18e77-251">Type your email address</span></span> | <span data-ttu-id="18e77-252">dirección de correo electrónico de Hola que recibe la notificación de Hola.</span><span class="sxs-lookup"><span data-stu-id="18e77-252">hello email address that receives hello notification.</span></span> |
    | <span data-ttu-id="18e77-253">**Asunto**</span><span class="sxs-lookup"><span data-stu-id="18e77-253">**Subject**</span></span> | <span data-ttu-id="18e77-254">Detectada opinión de tweet negativa</span><span class="sxs-lookup"><span data-stu-id="18e77-254">Negative tweet sentiment detected</span></span>  | <span data-ttu-id="18e77-255">línea de asunto Hola de notificación de correo electrónico de Hola.</span><span class="sxs-lookup"><span data-stu-id="18e77-255">hello subject line of hello email notification.</span></span>  |
    | <span data-ttu-id="18e77-256">**Cuerpo**</span><span class="sxs-lookup"><span data-stu-id="18e77-256">**Body**</span></span> | <span data-ttu-id="18e77-257">Texto de tweet, ubicación</span><span class="sxs-lookup"><span data-stu-id="18e77-257">Tweet text, Location</span></span> | <span data-ttu-id="18e77-258">Haga clic en hello **Tweet texto** y **ubicación** parámetros.</span><span class="sxs-lookup"><span data-stu-id="18e77-258">Click hello **Tweet text** and **Location** parameters.</span></span> |

5.  <span data-ttu-id="18e77-259">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="18e77-259">Click **Save**.</span></span>

<span data-ttu-id="18e77-260">Ahora que ha finalizado el flujo de trabajo de hello, puede habilitar la aplicación de la lógica de hello y vea función hello en el trabajo.</span><span class="sxs-lookup"><span data-stu-id="18e77-260">Now that hello workflow is complete, you can enable hello logic app and see hello function at work.</span></span>

## <a name="test-hello-workflow"></a><span data-ttu-id="18e77-261">Flujo de trabajo de prueba Hola</span><span class="sxs-lookup"><span data-stu-id="18e77-261">Test hello workflow</span></span>

1. <span data-ttu-id="18e77-262">Hola diseñador la lógica de aplicación, haga clic en **ejecutar** toostart Hola aplicación.</span><span class="sxs-lookup"><span data-stu-id="18e77-262">In hello Logic App Designer, click **Run** toostart hello app.</span></span>

2. <span data-ttu-id="18e77-263">En la columna izquierda de hello, haga clic en **Introducción** toosee estado de Hola de aplicación lógica de hello.</span><span class="sxs-lookup"><span data-stu-id="18e77-263">In hello left column, click **Overview** toosee hello status of hello logic app.</span></span> 
 
    ![Estado de ejecución de la aplicación lógica](media/functions-twitter-email/over1.png)

3. <span data-ttu-id="18e77-265">(Opcional) Haga clic en uno de hello ejecuciones toosee detalles de ejecución de Hola.</span><span class="sxs-lookup"><span data-stu-id="18e77-265">(Optional) Click one of hello runs toosee details of hello execution.</span></span>

4. <span data-ttu-id="18e77-266">Paso tooyour función, ver los registros de Hola y compruebe que los valores de opinión se recibe y procesa.</span><span class="sxs-lookup"><span data-stu-id="18e77-266">Go tooyour function, view hello logs, and verify that sentiment values were received and processed.</span></span>
 
    ![Ver los registros de función](media/functions-twitter-email/sent.png)

5. <span data-ttu-id="18e77-268">Cuando se detecta una opinión potencialmente negativa, recibirá un correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="18e77-268">When a potentially negative sentiment is detected, you receive an email.</span></span> <span data-ttu-id="18e77-269">Si no ha recibido un correo electrónico, puede cambiar tooreturn de código de función de hello rojo cada vez:</span><span class="sxs-lookup"><span data-stu-id="18e77-269">If you haven't received an email, you can change hello function code tooreturn RED every time:</span></span>

        return req.CreateResponse(HttpStatusCode.OK, "RED");

    <span data-ttu-id="18e77-270">Después de comprobar las notificaciones de correo electrónico, cambiar código original de toohello inversa:</span><span class="sxs-lookup"><span data-stu-id="18e77-270">After you have verified email notifications, change back toohello original code:</span></span>

        return req.CreateResponse(HttpStatusCode.OK, category);

    > [!IMPORTANT]
    > <span data-ttu-id="18e77-271">Después de completar este tutorial, debe deshabilitar la aplicación de la lógica de hello.</span><span class="sxs-lookup"><span data-stu-id="18e77-271">After you have completed this tutorial, you should disable hello logic app.</span></span> <span data-ttu-id="18e77-272">Al deshabilitar la aplicación hello, no está cargada para las ejecuciones y utilizar las transacciones de hello en su cuenta de servicios cognitivos.</span><span class="sxs-lookup"><span data-stu-id="18e77-272">By disabling hello app, you avoid being charged for executions and using up hello transactions in your Cognitive Services account.</span></span>

<span data-ttu-id="18e77-273">Ahora, ha visto lo fácil que es toointegrate funciones en un flujo de trabajo de las aplicaciones lógicas.</span><span class="sxs-lookup"><span data-stu-id="18e77-273">Now you have seen how easy it is toointegrate Functions into a Logic Apps workflow.</span></span>

## <a name="disable-hello-logic-app"></a><span data-ttu-id="18e77-274">Deshabilitar la aplicación de la lógica de hello</span><span class="sxs-lookup"><span data-stu-id="18e77-274">Disable hello logic app</span></span>

<span data-ttu-id="18e77-275">aplicación de lógica de hello toodisable, haga clic en **Introducción** y, a continuación, haga clic en **deshabilitar** en la parte superior de Hola de pantalla de bienvenida.</span><span class="sxs-lookup"><span data-stu-id="18e77-275">toodisable hello logic app, click **Overview** and then click **Disable** at hello top of hello screen.</span></span> <span data-ttu-id="18e77-276">Esto detiene Hola aplicación de lógica de ejecución y gastos sin eliminar la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="18e77-276">This stops hello logic app from running and incurring charges without deleting hello app.</span></span> 

![Registros de la función](media/functions-twitter-email/disable-logic-app.png)

## <a name="next-steps"></a><span data-ttu-id="18e77-278">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="18e77-278">Next steps</span></span>

<span data-ttu-id="18e77-279">En este tutorial, ha aprendido cómo:</span><span class="sxs-lookup"><span data-stu-id="18e77-279">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="18e77-280">Cree una cuenta de Cognitive Services.</span><span class="sxs-lookup"><span data-stu-id="18e77-280">Create a Cognitive Services account.</span></span>
> * <span data-ttu-id="18e77-281">Crear una función que clasifica las opiniones de tweet.</span><span class="sxs-lookup"><span data-stu-id="18e77-281">Create a function that categorizes tweet sentiment.</span></span>
> * <span data-ttu-id="18e77-282">Crear una aplicación de lógica que se conecta tooTwitter.</span><span class="sxs-lookup"><span data-stu-id="18e77-282">Create a logic app that connects tooTwitter.</span></span>
> * <span data-ttu-id="18e77-283">Agregar aplicación de lógica de toohello de detección de opinión.</span><span class="sxs-lookup"><span data-stu-id="18e77-283">Add sentiment detection toohello logic app.</span></span> 
> * <span data-ttu-id="18e77-284">Se conectan Hola lógica aplicación toohello funcionan.</span><span class="sxs-lookup"><span data-stu-id="18e77-284">Connect hello logic app toohello function.</span></span>
> * <span data-ttu-id="18e77-285">Enviar un correo electrónico en función de la respuesta de Hola de función hello.</span><span class="sxs-lookup"><span data-stu-id="18e77-285">Send an email based on hello response from hello function.</span></span>

<span data-ttu-id="18e77-286">Avanzar toohello siguiente tutorial toolearn cómo toocreate una API sin servidor para la función.</span><span class="sxs-lookup"><span data-stu-id="18e77-286">Advance toohello next tutorial toolearn how toocreate a serverless API for your function.</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="18e77-287">Creación de una API sin servidor mediante Azure Functions</span><span class="sxs-lookup"><span data-stu-id="18e77-287">Create a serverless API using Azure Functions</span></span>](functions-create-serverless-api.md)

<span data-ttu-id="18e77-288">toolearn más información acerca de las aplicaciones lógicas, consulte [Azure Logic Apps](../logic-apps/logic-apps-what-are-logic-apps.md).</span><span class="sxs-lookup"><span data-stu-id="18e77-288">toolearn more about Logic Apps, see [Azure Logic Apps](../logic-apps/logic-apps-what-are-logic-apps.md).</span></span>

