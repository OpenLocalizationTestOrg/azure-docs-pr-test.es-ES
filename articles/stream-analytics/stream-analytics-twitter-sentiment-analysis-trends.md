---
title: "análisis de opinión de Twitter de tiempo aaaReal con análisis de transmisiones de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse análisis de transmisiones para el análisis de opinión de Twitter en tiempo real. Guía paso a paso de toodata de generación de eventos en un panel en tiempo real."
keywords: "análisis de tendencias de twitter en tiempo real, análisis de opiniones, análisis de medios sociales, ejemplo de análisis de tendencias"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 42068691-074b-4c3b-a527-acafa484fda2
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: jeffstok
ms.openlocfilehash: 157790caa7ea6f5570dd9c9d3bd9694d437eb4c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="real-time-twitter-sentiment-analysis-in-azure-stream-analytics"></a><span data-ttu-id="4902c-105">Análisis de sentimiento de Twitter en tiempo real en Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="4902c-105">Real-time Twitter sentiment analysis in Azure Stream Analytics</span></span>

<span data-ttu-id="4902c-106">Obtenga información acerca de cómo Twitter toobuild una solución de análisis de opiniones para el análisis de los medios sociales si se ponen en tiempo real de los eventos en los centros de eventos de Azure.</span><span class="sxs-lookup"><span data-stu-id="4902c-106">Learn how toobuild a sentiment analysis solution for social media analytics by bringing real-time Twitter events into Azure Event Hubs.</span></span> <span data-ttu-id="4902c-107">A continuación, puede escribir un análisis de transmisiones de Azure consultar tooanalyze Hola datos y cualquier almacén Hola resultados para su uso posterior o usar un panel y [Power BI](https://powerbi.com/) tooprovide información en tiempo real.</span><span class="sxs-lookup"><span data-stu-id="4902c-107">You can then write an Azure Stream Analytics query tooanalyze hello data and either store hello results for later use or use a dashboard and [Power BI](https://powerbi.com/) tooprovide insights in real time.</span></span>

<span data-ttu-id="4902c-108">Las herramientas de análisis de las redes sociales ayudan a las organizaciones a comprender los temas que son tendencias.</span><span class="sxs-lookup"><span data-stu-id="4902c-108">Social media analytics tools help organizations understand trending topics.</span></span> <span data-ttu-id="4902c-109">Los temas que son tendencias son asuntos y actitudes con un gran volumen de entradas en las redes sociales.</span><span class="sxs-lookup"><span data-stu-id="4902c-109">Trending topics are subjects and attitudes that have a high volume of posts in social media.</span></span> <span data-ttu-id="4902c-110">Análisis de opiniones, que también se denomina *minería de datos de opinión*, usa medios sociales análisis herramientas toodetermine actitudes de un producto, idea y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="4902c-110">Sentiment analysis, which is also called *opinion mining*, uses social media analytics tools toodetermine attitudes toward a product, idea, and so on.</span></span> 

<span data-ttu-id="4902c-111">Análisis de tendencias de Twitter en tiempo real es un buen ejemplo de una herramienta de análisis, porque el modelo de suscripción de hello hashtag permite palabras clave de toospecific de toolisten (hashtags) y desarrollar análisis de opiniones de hello fuente de distribución.</span><span class="sxs-lookup"><span data-stu-id="4902c-111">Real-time Twitter trend analysis is a great example of an analytics tool, because hello hashtag subscription model enables you toolisten toospecific keywords (hashtags) and develop sentiment analysis of hello feed.</span></span>

## <a name="scenario-social-media-sentiment-analysis-in-real-time"></a><span data-ttu-id="4902c-112">Escenario: Análisis de opinión de redes sociales en tiempo real</span><span class="sxs-lookup"><span data-stu-id="4902c-112">Scenario: Social media sentiment analysis in real time</span></span>

<span data-ttu-id="4902c-113">Una empresa que tiene un sitio Web de noticias multimedia está interesada en obtener una ventaja con respecto a sus competidores ya que presenta el contenido del sitio que es importante de inmediato tooits lectores.</span><span class="sxs-lookup"><span data-stu-id="4902c-113">A company that has a news media website is interested in gaining an advantage over its competitors by featuring site content that is immediately relevant tooits readers.</span></span> <span data-ttu-id="4902c-114">empresa Hola utiliza el análisis de los medios sociales en temas que son relevantes tooreaders realizando análisis de opiniones en tiempo real de los datos de Twitter.</span><span class="sxs-lookup"><span data-stu-id="4902c-114">hello company uses social media analysis on topics that are relevant tooreaders by doing real-time sentiment analysis of Twitter data.</span></span>

<span data-ttu-id="4902c-115">tooidentify temas tendencias en tiempo real en Twitter, Hola empresa necesidades de análisis en tiempo real acerca del volumen de tweet de Hola y opiniones de los temas claves.</span><span class="sxs-lookup"><span data-stu-id="4902c-115">tooidentify trending topics in real time on Twitter, hello company needs real-time analytics about hello tweet volume and sentiment for key topics.</span></span> <span data-ttu-id="4902c-116">En otras palabras, la necesidad de hello es un motor de análisis de análisis de opiniones que se basa en esta fuente de distribución de los medios sociales.</span><span class="sxs-lookup"><span data-stu-id="4902c-116">In other words, hello need is a sentiment analysis analytics engine that's based on this social media feed.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4902c-117">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="4902c-117">Prerequisites</span></span>
<span data-ttu-id="4902c-118">En este tutorial, utilice una aplicación cliente que se conecta tooTwitter y busca tweets que tienen ciertas hashtags (lo que se puede establecer).</span><span class="sxs-lookup"><span data-stu-id="4902c-118">In this tutorial, you use a client application that connects tooTwitter and looks for tweets that have certain hashtags (which you can set).</span></span> <span data-ttu-id="4902c-119">En orden toorun Hola aplicación y analizar Hola tweets mediante el análisis de transmisión por secuencias de Azure, debe disponer de hello siguiente:</span><span class="sxs-lookup"><span data-stu-id="4902c-119">In order toorun hello application and analyze hello tweets using Azure Streaming Analytics, you must have hello following:</span></span>

* <span data-ttu-id="4902c-120">Una suscripción de Azure</span><span class="sxs-lookup"><span data-stu-id="4902c-120">An Azure subscription</span></span>
* <span data-ttu-id="4902c-121">Una cuenta de Twitter</span><span class="sxs-lookup"><span data-stu-id="4902c-121">A Twitter account</span></span> 
* <span data-ttu-id="4902c-122">Una aplicación de Twitter, hello y [token de acceso de OAuth](https://dev.twitter.com/oauth/overview/application-owner-access-tokens) para esa aplicación.</span><span class="sxs-lookup"><span data-stu-id="4902c-122">A Twitter application, and hello [OAuth access token](https://dev.twitter.com/oauth/overview/application-owner-access-tokens) for that application.</span></span> <span data-ttu-id="4902c-123">Se proporcionan instrucciones de alto nivel sobre cómo toocreate una aplicación de Twitter más tarde.</span><span class="sxs-lookup"><span data-stu-id="4902c-123">We provide high-level instructions for how toocreate a Twitter application later.</span></span>
* <span data-ttu-id="4902c-124">fuente de aplicación de TwitterWPFClient Hello, que lee Hola Twitter.</span><span class="sxs-lookup"><span data-stu-id="4902c-124">hello TwitterWPFClient application, which reads hello Twitter feed.</span></span> <span data-ttu-id="4902c-125">tooget esta aplicación, descarga hello [TwitterWPFClient.zip](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TwitterClient/TwitterWPFClient.zip) de GitHub de archivos y, a continuación, descomprima el paquete de hello en una carpeta en el equipo.</span><span class="sxs-lookup"><span data-stu-id="4902c-125">tooget this application, download hello [TwitterWPFClient.zip](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TwitterClient/TwitterWPFClient.zip) file from GitHub and then unzip hello package into a folder on your computer.</span></span> <span data-ttu-id="4902c-126">Si desea que el código fuente de toosee hello y ejecutar aplicación hello en un depurador, puede obtener el código fuente de Hola de [GitHub](https://aka.ms/azure-stream-analytics-telcogenerator).</span><span class="sxs-lookup"><span data-stu-id="4902c-126">If you want toosee hello source code and run hello application in a debugger, you can get hello source code from [GitHub](https://aka.ms/azure-stream-analytics-telcogenerator).</span></span> 

## <a name="create-an-event-hub-for-streaming-analytics-input"></a><span data-ttu-id="4902c-127">Creación de un centro de eventos para la entrada de Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="4902c-127">Create an event hub for Streaming Analytics input</span></span>

<span data-ttu-id="4902c-128">aplicación de ejemplo de Hola genera eventos y los envía tooan concentrador de eventos de Azure.</span><span class="sxs-lookup"><span data-stu-id="4902c-128">hello sample application generates events and pushes them tooan Azure event hub.</span></span> <span data-ttu-id="4902c-129">Los concentradores de eventos de Azure son método hello preferido de recopilación de eventos para el análisis de transmisiones.</span><span class="sxs-lookup"><span data-stu-id="4902c-129">Azure event hubs are hello preferred method of event ingestion for Stream Analytics.</span></span> <span data-ttu-id="4902c-130">Para obtener más información, vea hello [documentación de los centros de eventos de Azure](../event-hubs/event-hubs-what-is-event-hubs.md).</span><span class="sxs-lookup"><span data-stu-id="4902c-130">For more information, see hello [Azure Event Hubs documentation](../event-hubs/event-hubs-what-is-event-hubs.md).</span></span>


### <a name="create-an-event-hub-namespace-and-event-hub"></a><span data-ttu-id="4902c-131">Creación de un espacio de nombres del centro de eventos y un centro de eventos</span><span class="sxs-lookup"><span data-stu-id="4902c-131">Create an event hub namespace and event hub</span></span>
<span data-ttu-id="4902c-132">En este procedimiento, primero cree un espacio de nombres del centro de eventos y, a continuación, agregue un espacio de nombres de toothat de concentrador de eventos.</span><span class="sxs-lookup"><span data-stu-id="4902c-132">In this procedure, you first create an event hub namespace, and then you add an event hub toothat namespace.</span></span> <span data-ttu-id="4902c-133">Los espacios de nombres del concentrador de eventos se utilizan instancias de bus de eventos relacionados con el grupo de toologically.</span><span class="sxs-lookup"><span data-stu-id="4902c-133">Event hub namespaces are used toologically group related event bus instances.</span></span> 

1. <span data-ttu-id="4902c-134">Inicie sesión en toohello portal de Azure y haga clic en **New** > **Internet de las cosas** > **concentrador de eventos**.</span><span class="sxs-lookup"><span data-stu-id="4902c-134">Log  in toohello Azure portal and click **New** > **Internet of Things** > **Event Hub**.</span></span> 

2. <span data-ttu-id="4902c-135">Hola **crear espacio de nombres** hoja, escriba un nombre de espacio de nombres como `<yourname>-socialtwitter-eh-ns`.</span><span class="sxs-lookup"><span data-stu-id="4902c-135">In hello **Create namespace** blade, enter a namespace name such as `<yourname>-socialtwitter-eh-ns`.</span></span> <span data-ttu-id="4902c-136">Puede utilizar cualquier nombre de espacio de nombres de hello, pero Hola nombre debe ser válido para una dirección URL y debe ser único en Azure.</span><span class="sxs-lookup"><span data-stu-id="4902c-136">You can use any name for hello namespace, but hello name must be valid for a URL and it must be unique across Azure.</span></span> 
    
3. <span data-ttu-id="4902c-137">Seleccione una suscripción y cree o elija un grupo de recursos. Luego haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="4902c-137">Select a subscription and create or choose a resource group, then click **Create**.</span></span> 

    ![Creación de un espacio de nombres del centro de eventos](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-eventhub-namespace.png)
 
4. <span data-ttu-id="4902c-139">Cuando el espacio de nombres de hello ha terminado de implementar, buscar espacio de nombres del concentrador de eventos de hello en la lista de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="4902c-139">When hello namespace has finished deploying, find hello event hub namespace in your list of Azure resources.</span></span> 

5. <span data-ttu-id="4902c-140">Haga clic en nuevo espacio de nombres Hola y en la hoja de espacio de nombres de hello, haga clic en  **+ &nbsp;concentrador de eventos**.</span><span class="sxs-lookup"><span data-stu-id="4902c-140">Click hello new namespace, and in hello namespace blade, click **+&nbsp;Event Hub**.</span></span> 

    ![<span data-ttu-id="4902c-141">botón de agregar el concentrador de eventos de Hola para crear un nuevo centro de eventos</span><span class="sxs-lookup"><span data-stu-id="4902c-141">hello Add Event Hub button for creating a new event hub</span></span> ](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-eventhub-button.png)    
 
6. <span data-ttu-id="4902c-142">Nuevo centro de eventos de nombre hello `socialtwitter-eh`.</span><span class="sxs-lookup"><span data-stu-id="4902c-142">Name hello new event hub `socialtwitter-eh`.</span></span> <span data-ttu-id="4902c-143">Puede usar otro nombre.</span><span class="sxs-lookup"><span data-stu-id="4902c-143">You can use a different name.</span></span> <span data-ttu-id="4902c-144">Si lo hace, tome nota del mismo, porque necesita Hola nombre más adelante.</span><span class="sxs-lookup"><span data-stu-id="4902c-144">If you do, make a note of it, because you need hello name later.</span></span> <span data-ttu-id="4902c-145">No es necesario tooset cualquier otra opción de concentrador de eventos de Hola.</span><span class="sxs-lookup"><span data-stu-id="4902c-145">You don't need tooset any other options for hello event hub.</span></span>

    ![Hoja para la creación de un centro de eventos](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-eventhub.png)
 
7. <span data-ttu-id="4902c-147">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="4902c-147">Click **Create**.</span></span>


### <a name="grant-access-toohello-event-hub"></a><span data-ttu-id="4902c-148">Centro de eventos de conceder acceso toohello</span><span class="sxs-lookup"><span data-stu-id="4902c-148">Grant access toohello event hub</span></span>

<span data-ttu-id="4902c-149">Antes de que un proceso puede enviar el concentrador de eventos de datos tooan, centro de eventos de hello debe tener una directiva que permita el acceso adecuado.</span><span class="sxs-lookup"><span data-stu-id="4902c-149">Before a process can send data tooan event hub, hello event hub must have a policy that allows appropriate access.</span></span> <span data-ttu-id="4902c-150">Directiva de acceso de Hello genera una cadena de conexión que incluya la información de autorización.</span><span class="sxs-lookup"><span data-stu-id="4902c-150">hello access policy produces a connection string that includes authorization information.</span></span>

1.  <span data-ttu-id="4902c-151">En la hoja de espacio de nombres de evento de hello, haga clic en **centros de eventos** y, a continuación, haga clic en nombre de Hola de su nuevo concentrador de eventos.</span><span class="sxs-lookup"><span data-stu-id="4902c-151">In hello event namespace blade, click **Event Hubs** and then click hello name of your new event hub.</span></span>

2.  <span data-ttu-id="4902c-152">En la hoja de concentrador de eventos de hello, haga clic en **directivas de acceso compartido** y, a continuación, haga clic en  **+ &nbsp;agregar**.</span><span class="sxs-lookup"><span data-stu-id="4902c-152">In hello event hub blade, click **Shared access policies** and then click **+&nbsp;Add**.</span></span>

    >[!NOTE]
    ><span data-ttu-id="4902c-153">Asegúrese de que está trabajando con el concentrador de eventos de hello, no Hola eventos concentrador espacio de nombres.</span><span class="sxs-lookup"><span data-stu-id="4902c-153">Make sure you're working with hello event hub, not hello event hub namespace.</span></span>

3.  <span data-ttu-id="4902c-154">Agregue una directiva denominada `socialtwitter-access` y, en **Notificación**, seleccione **Administrar**.</span><span class="sxs-lookup"><span data-stu-id="4902c-154">Add a policy named `socialtwitter-access` and for **Claim**, select **Manage**.</span></span>

    ![Hoja para la creación de una directiva de acceso al centro de eventos](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-shared-access-policy-manage.png)
 
4.  <span data-ttu-id="4902c-156">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="4902c-156">Click **Create**.</span></span>

5.  <span data-ttu-id="4902c-157">Después de que se ha implementado la directiva de hello, haga clic en la lista de Hola de directivas de acceso compartido.</span><span class="sxs-lookup"><span data-stu-id="4902c-157">After hello policy has been deployed, click it in hello list of shared access policies.</span></span>

6.  <span data-ttu-id="4902c-158">Cuadro de búsqueda Hola etiquetado **clave principal de la cadena de conexión** y haga clic en la cadena de conexión de hello copia botón siguiente toohello.</span><span class="sxs-lookup"><span data-stu-id="4902c-158">Find hello box labeled **CONNECTION STRING-PRIMARY KEY** and click hello copy button next toohello connection string.</span></span> 
    
    ![Copiar la clave de cadena de conexión principal de Hola Hola directiva de acceso](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-shared-access-policy-copy-connection-string.png)
 
7.  <span data-ttu-id="4902c-160">Pegue la cadena de conexión de hello en un editor de texto.</span><span class="sxs-lookup"><span data-stu-id="4902c-160">Paste hello connection string into a text editor.</span></span> <span data-ttu-id="4902c-161">Necesita esta cadena de conexión para la sección siguiente de hello, después de realizar algunos tooit pequeñas modificaciones.</span><span class="sxs-lookup"><span data-stu-id="4902c-161">You need this connection string for hello next section, after you make some small edits tooit.</span></span>

    <span data-ttu-id="4902c-162">cadena de conexión de Hello tiene el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="4902c-162">hello connection string looks like this:</span></span>

        Endpoint=sb://YOURNAME-socialtwitter-eh-ns.servicebus.windows.net/;SharedAccessKeyName=socialtwitter-access;SharedAccessKey=Gw2NFZw6r...FxKbXaC2op6a0ZsPkI=;EntityPath=socialtwitter-eh

    <span data-ttu-id="4902c-163">Tenga en cuenta que la cadena de conexión de hello contiene varios pares de clave y valor, separados por punto y coma: `Endpoint`, `SharedAccessKeyName`, `SharedAccessKey`, y `EntityPath`.</span><span class="sxs-lookup"><span data-stu-id="4902c-163">Notice that hello connection string contains multiple key-value pairs, separated with semicolons: `Endpoint`, `SharedAccessKeyName`, `SharedAccessKey`, and `EntityPath`.</span></span>  

    > [!NOTE]
    > <span data-ttu-id="4902c-164">Para la seguridad, se han quitado los elementos de cadena de conexión de hello en el ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="4902c-164">For security, parts of hello connection string in hello example have been removed.</span></span>

8.  <span data-ttu-id="4902c-165">En el editor de texto hello, quitar hello `EntityPath` par de cadena de conexión de hello (no olvide tooremove Hola por punto y coma que lo precede).</span><span class="sxs-lookup"><span data-stu-id="4902c-165">In hello text editor, remove hello `EntityPath` pair from hello connection string (don't forget tooremove hello semicolon that precedes it).</span></span> <span data-ttu-id="4902c-166">Cuando haya terminado, cadena de conexión de hello tiene este aspecto:</span><span class="sxs-lookup"><span data-stu-id="4902c-166">When you're done, hello connection string looks like this:</span></span>

        Endpoint=sb://YOURNAME-socialtwitter-eh-ns.servicebus.windows.net/;SharedAccessKeyName=socialtwitter-access;SharedAccessKey=Gw2NFZw6r...FxKbXaC2op6a0ZsPkI=


## <a name="configure-and-start-hello-twitter-client-application"></a><span data-ttu-id="4902c-167">Configurar e iniciar la aplicación de cliente de Twitter de hello</span><span class="sxs-lookup"><span data-stu-id="4902c-167">Configure and start hello Twitter client application</span></span>
<span data-ttu-id="4902c-168">aplicación de cliente de Hello obtiene eventos tweet directamente de Twitter.</span><span class="sxs-lookup"><span data-stu-id="4902c-168">hello client application gets tweet events directly from Twitter.</span></span> <span data-ttu-id="4902c-169">En orden toodo lo, necesita Hola de toocall de permiso de Twitter API de transmisión por secuencias.</span><span class="sxs-lookup"><span data-stu-id="4902c-169">In order toodo so, it needs permission toocall hello Twitter Streaming APIs.</span></span> <span data-ttu-id="4902c-170">tooconfigure permiso, crear una aplicación en Twitter, lo que genera credenciales exclusivas (por ejemplo, un token de OAuth).</span><span class="sxs-lookup"><span data-stu-id="4902c-170">tooconfigure that permission, you create an application in Twitter, which generates unique credentials (such as an OAuth token).</span></span> <span data-ttu-id="4902c-171">A continuación, puede configurar toouse de aplicación de cliente de hello en estas credenciales cuando se realizan llamadas de API.</span><span class="sxs-lookup"><span data-stu-id="4902c-171">You can then configure hello client application toouse these credentials when it makes API calls.</span></span> 

### <a name="create-a-twitter-application"></a><span data-ttu-id="4902c-172">Crear una aplicación de Twitter</span><span class="sxs-lookup"><span data-stu-id="4902c-172">Create a Twitter application</span></span>
<span data-ttu-id="4902c-173">Si no dispone de una aplicación de Twitter que pueda usar para este tutorial, puede crear una.</span><span class="sxs-lookup"><span data-stu-id="4902c-173">If you do not already have a Twitter application that you can use for this tutorial, you can create one.</span></span> <span data-ttu-id="4902c-174">Ya debe tener una cuenta de Twitter.</span><span class="sxs-lookup"><span data-stu-id="4902c-174">You must already have a Twitter account.</span></span>

> [!NOTE]
> <span data-ttu-id="4902c-175">puede cambiar el proceso exacto de Hello en Twitter para crear una aplicación y obtener el token, secretos y las claves de Hola.</span><span class="sxs-lookup"><span data-stu-id="4902c-175">hello exact process in Twitter for creating an application and getting hello keys, secrets, and token might change.</span></span> <span data-ttu-id="4902c-176">Si estas instrucciones no coincide con lo que se ve en el sitio de Twitter de hello, consulte la documentación del desarrollador de Twitter de toohello.</span><span class="sxs-lookup"><span data-stu-id="4902c-176">If these instructions don't match what you see on hello Twitter site, refer toohello Twitter developer documentation.</span></span>

1. <span data-ttu-id="4902c-177">Vaya toohello [página de administración de aplicaciones de Twitter](https://apps.twitter.com/).</span><span class="sxs-lookup"><span data-stu-id="4902c-177">Go toohello [Twitter application management page](https://apps.twitter.com/).</span></span> 

2. <span data-ttu-id="4902c-178">Cree una aplicación.</span><span class="sxs-lookup"><span data-stu-id="4902c-178">Create a new application.</span></span> 

    * <span data-ttu-id="4902c-179">Dirección URL del sitio Web de hello, especifique una dirección URL válida.</span><span class="sxs-lookup"><span data-stu-id="4902c-179">For hello website URL, specify a valid URL.</span></span> <span data-ttu-id="4902c-180">No tiene toobe un sitio en vivo.</span><span class="sxs-lookup"><span data-stu-id="4902c-180">It does not have toobe a live site.</span></span> <span data-ttu-id="4902c-181">(No puede especificar simplemente `localhost`).</span><span class="sxs-lookup"><span data-stu-id="4902c-181">(You can't specify just `localhost`.)</span></span>
    * <span data-ttu-id="4902c-182">Deje en blanco campo de devolución de llamada de Hola.</span><span class="sxs-lookup"><span data-stu-id="4902c-182">Leave hello callback field blank.</span></span> <span data-ttu-id="4902c-183">aplicación de cliente de Hola que utiliza para este tutorial no requiere las devoluciones de llamada.</span><span class="sxs-lookup"><span data-stu-id="4902c-183">hello client application you use for this tutorial doesn't require callbacks.</span></span>

    ![Creación de una aplicación en Twitter](./media/stream-analytics-twitter-sentiment-analysis-trends/create-twitter-application.png)

3. <span data-ttu-id="4902c-185">Opcionalmente, cambie los permisos de la aplicación hello solo tooread.</span><span class="sxs-lookup"><span data-stu-id="4902c-185">Optionally, change hello application's permissions tooread-only.</span></span>

4. <span data-ttu-id="4902c-186">Cuando se crea la aplicación hello, vaya toohello **claves y Tokens de acceso** página.</span><span class="sxs-lookup"><span data-stu-id="4902c-186">When hello application is created, go toohello **Keys and Access Tokens** page.</span></span>

5. <span data-ttu-id="4902c-187">Haga clic en el botón de hello toogenerate un token de acceso y el secreto del token de acceso.</span><span class="sxs-lookup"><span data-stu-id="4902c-187">Click hello button toogenerate an access token and access token secret.</span></span>

<span data-ttu-id="4902c-188">Mantenga esta información útil, ya que necesitará en el procedimiento siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="4902c-188">Keep this information handy, because you will need it in hello next procedure.</span></span>

>[!NOTE]
><span data-ttu-id="4902c-189">Hola claves y secretos de aplicación de Twitter de hello proporcionan la cuenta de acceso de Twitter tooyour.</span><span class="sxs-lookup"><span data-stu-id="4902c-189">hello keys and secrets for hello Twitter application provide access tooyour Twitter account.</span></span> <span data-ttu-id="4902c-190">Tratar esta información como confidencial, Hola igual a como lo hace la contraseña de Twitter.</span><span class="sxs-lookup"><span data-stu-id="4902c-190">Treat this information as sensitive, hello same as you do your Twitter password.</span></span> <span data-ttu-id="4902c-191">Por ejemplo, no inserte esta información en una aplicación que se asigne tooothers.</span><span class="sxs-lookup"><span data-stu-id="4902c-191">For example, don't embed this information in an application that you give tooothers.</span></span> 


### <a name="configure-hello-client-application"></a><span data-ttu-id="4902c-192">Configurar la aplicación de cliente hello</span><span class="sxs-lookup"><span data-stu-id="4902c-192">Configure hello client application</span></span>
<span data-ttu-id="4902c-193">Hemos creado una aplicación de cliente que se conecte mediante datos de tooTwitter [API de transmisión por secuencias de Twitter](https://dev.twitter.com/streaming/overview) eventos de tweet toocollect sobre un conjunto específico de temas.</span><span class="sxs-lookup"><span data-stu-id="4902c-193">We've created a client application that connects tooTwitter data using [Twitter's Streaming APIs](https://dev.twitter.com/streaming/overview) toocollect tweet events about a specific set of topics.</span></span> <span data-ttu-id="4902c-194">aplicación Hello usa hello [Sentiment140](http://help.sentiment140.com/) herramienta de código abierto, que asigna Hola después tweet de opiniones valor tooeach:</span><span class="sxs-lookup"><span data-stu-id="4902c-194">hello application uses hello [Sentiment140](http://help.sentiment140.com/) open source tool, which assigns hello following sentiment value tooeach tweet:</span></span>

* <span data-ttu-id="4902c-195">0 = negativo</span><span class="sxs-lookup"><span data-stu-id="4902c-195">0 = negative</span></span>
* <span data-ttu-id="4902c-196">2 = neutral</span><span class="sxs-lookup"><span data-stu-id="4902c-196">2 = neutral</span></span>
* <span data-ttu-id="4902c-197">4 = positivo</span><span class="sxs-lookup"><span data-stu-id="4902c-197">4 = positive</span></span>

<span data-ttu-id="4902c-198">Después de eventos de tweet Hola se han asignado un valor de opinión, se insertan concentrador de eventos de toohello que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="4902c-198">After hello tweet events have been assigned a sentiment value, they are pushed toohello event hub that you created earlier.</span></span>

<span data-ttu-id="4902c-199">Antes de que se ejecute la aplicación hello, requiere cierta información del usuario, como las claves de Twitter de Hola y cadena de conexión de concentrador de eventos de Hola.</span><span class="sxs-lookup"><span data-stu-id="4902c-199">Before hello application runs, it requires certain information from you, like hello Twitter keys and hello event hub connection string.</span></span> <span data-ttu-id="4902c-200">Puede proporcionar información de configuración de Hola de las siguientes maneras:</span><span class="sxs-lookup"><span data-stu-id="4902c-200">You can provide hello configuration information in these ways:</span></span>

* <span data-ttu-id="4902c-201">Ejecutar la aplicación hello y, a continuación, utilice claves de hello tooenter interfaz de usuario de la aplicación hello, secretos y cadena de conexión.</span><span class="sxs-lookup"><span data-stu-id="4902c-201">Run hello application, and then use hello application's UI tooenter hello keys, secrets, and connection string.</span></span> <span data-ttu-id="4902c-202">Si lo hace, se utiliza la información de configuración de hello en la sesión actual, pero no se guarda.</span><span class="sxs-lookup"><span data-stu-id="4902c-202">If you do this, hello configuration information is used for your current session, but it isn't saved.</span></span>
* <span data-ttu-id="4902c-203">Edite el archivo .config de la aplicación hello y establecer los valores hello no existe.</span><span class="sxs-lookup"><span data-stu-id="4902c-203">Edit hello application's .config file and set hello values there.</span></span> <span data-ttu-id="4902c-204">Este enfoque conserva la información de configuración de hello, pero también significa que esta información potencialmente confidencial se almacena en texto sin formato en el equipo.</span><span class="sxs-lookup"><span data-stu-id="4902c-204">This approach persists hello configuration information, but it also means that this potentially sensitive information is stored in plain text on your computer.</span></span>

<span data-ttu-id="4902c-205">Hello siguiente procedimiento documenta ambos enfoques.</span><span class="sxs-lookup"><span data-stu-id="4902c-205">hello following procedure documents both approaches.</span></span> 

1. <span data-ttu-id="4902c-206">Asegúrese de que ha descargado y descomprimido hello [TwitterWPFClient.zip](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TwitterClient/TwitterWPFClient.zip) aplicación, como se muestra en los requisitos previos de Hola.</span><span class="sxs-lookup"><span data-stu-id="4902c-206">Make sure you've downloaded and unzipped hello [TwitterWPFClient.zip](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TwitterClient/TwitterWPFClient.zip) application, as listed in hello prerequisites.</span></span>

2. <span data-ttu-id="4902c-207">valores de hello tooset en tiempo de ejecución (y solo para hello sesión actual), ejecute hello `TwitterWPFClient.exe` aplicación.</span><span class="sxs-lookup"><span data-stu-id="4902c-207">tooset hello values at run time (and only for hello current session), run hello `TwitterWPFClient.exe` application.</span></span> <span data-ttu-id="4902c-208">Cuando solicite aplicación hello, escriba Hola siguientes valores:</span><span class="sxs-lookup"><span data-stu-id="4902c-208">When hello application prompts you, enter hello following values:</span></span>

    * <span data-ttu-id="4902c-209">Hola clave de consumidor de Twitter (clave de API).</span><span class="sxs-lookup"><span data-stu-id="4902c-209">hello Twitter Consumer Key (API Key).</span></span>
    * <span data-ttu-id="4902c-210">Hola secreto de consumidor de Twitter (secreto de API).</span><span class="sxs-lookup"><span data-stu-id="4902c-210">hello Twitter Consumer Secret (API Secret).</span></span>
    * <span data-ttu-id="4902c-211">Hola Token de acceso de Twitter.</span><span class="sxs-lookup"><span data-stu-id="4902c-211">hello Twitter Access Token.</span></span>
    * <span data-ttu-id="4902c-212">Hola secreto del Token de acceso de Twitter.</span><span class="sxs-lookup"><span data-stu-id="4902c-212">hello Twitter Access Token Secret.</span></span>
    * <span data-ttu-id="4902c-213">información de la cadena de conexión Hola que guardó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="4902c-213">hello connection string information that you saved earlier.</span></span> <span data-ttu-id="4902c-214">Asegúrese de que usar cadena de conexión de Hola que quitan hello `EntityPath` par clave-valor de.</span><span class="sxs-lookup"><span data-stu-id="4902c-214">Make sure that you use hello connection string that you removed hello `EntityPath` key-value pair from.</span></span>
    * <span data-ttu-id="4902c-215">Hola Twitter palabras clave que desea toodetermine opinión de.</span><span class="sxs-lookup"><span data-stu-id="4902c-215">hello Twitter keywords that you want toodetermine sentiment for.</span></span>

   ![Aplicación de TwitterWpfClient en ejecución, mostrando los valores difuminados](./media/stream-analytics-twitter-sentiment-analysis-trends/wpfclientlines.png)

3. <span data-ttu-id="4902c-217">valores de hello tooset de forma persistente, usan un archivo de texto del editor tooopen hello TwitterWpfClient.exe.config.</span><span class="sxs-lookup"><span data-stu-id="4902c-217">tooset hello values persistently, use a text editor tooopen hello TwitterWpfClient.exe.config file.</span></span> <span data-ttu-id="4902c-218">A continuación, en hello `<appSettings>` elemento, hacer esto:</span><span class="sxs-lookup"><span data-stu-id="4902c-218">Then in hello `<appSettings>` element, do this:</span></span>

    * <span data-ttu-id="4902c-219">Establecer `oauth_consumer_key` toohello clave de consumidor de Twitter (clave de API).</span><span class="sxs-lookup"><span data-stu-id="4902c-219">Set `oauth_consumer_key` toohello Twitter Consumer Key (API Key).</span></span> 
    * <span data-ttu-id="4902c-220">Establecer `oauth_consumer_secret` toohello secreto de consumidor de Twitter (secreto de API).</span><span class="sxs-lookup"><span data-stu-id="4902c-220">Set `oauth_consumer_secret` toohello Twitter Consumer Secret (API Secret).</span></span>
    * <span data-ttu-id="4902c-221">Establecer `oauth_token` toohello Token de acceso de Twitter.</span><span class="sxs-lookup"><span data-stu-id="4902c-221">Set `oauth_token` toohello Twitter Access Token.</span></span>
    * <span data-ttu-id="4902c-222">Establecer `oauth_token_secret` toohello secreto del Token de acceso de Twitter.</span><span class="sxs-lookup"><span data-stu-id="4902c-222">Set `oauth_token_secret` toohello Twitter Access Token Secret.</span></span>

    <span data-ttu-id="4902c-223">Más adelante en hello `<appSettings>` elemento, realice estos cambios:</span><span class="sxs-lookup"><span data-stu-id="4902c-223">Later in hello `<appSettings>` element, make these changes:</span></span>

    * <span data-ttu-id="4902c-224">Establecer `EventHubName` toohello nombre de centro de eventos (es decir, el valor de toohello de ruta de acceso de hello entidad).</span><span class="sxs-lookup"><span data-stu-id="4902c-224">Set `EventHubName` toohello event hub name (that is, toohello value of hello entity path).</span></span>
    * <span data-ttu-id="4902c-225">Establecer `EventHubNameConnectionString` toohello cadena de conexión.</span><span class="sxs-lookup"><span data-stu-id="4902c-225">Set `EventHubNameConnectionString` toohello connection string.</span></span> <span data-ttu-id="4902c-226">Asegúrese de que usar cadena de conexión de Hola que quitan hello `EntityPath` par clave-valor de.</span><span class="sxs-lookup"><span data-stu-id="4902c-226">Make sure that you use hello connection string that you removed hello `EntityPath` key-value pair from.</span></span>

    <span data-ttu-id="4902c-227">Hola `<appSettings>` sección aspecto Hola siguiente ejemplo.</span><span class="sxs-lookup"><span data-stu-id="4902c-227">hello `<appSettings>` section looks like hello following example.</span></span> <span data-ttu-id="4902c-228">(Para mayor claridad y seguridad, se han ajustado algunas líneas y se han quitado algunos caracteres).</span><span class="sxs-lookup"><span data-stu-id="4902c-228">(For clarity and security, we wrapped some lines and removed some characters.)</span></span>

    ![Archivo de configuración de aplicación TwitterWpfClient en un editor de texto, que muestra las claves de Twitter de Hola y secretos e información de cadena de conexión de concentrador de eventos de Hola](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-tiwtter-app-config.png)
 
4. <span data-ttu-id="4902c-230">Si ya no ha iniciado la aplicación hello, ejecute TwitterWpfClient.exe ahora.</span><span class="sxs-lookup"><span data-stu-id="4902c-230">If you didn't already start hello application, run TwitterWpfClient.exe now.</span></span> 

5. <span data-ttu-id="4902c-231">Haga clic en medios sociales del toocollect de botón Inicio verde Hola.</span><span class="sxs-lookup"><span data-stu-id="4902c-231">Click hello green start button toocollect social sentiment.</span></span> <span data-ttu-id="4902c-232">Ver eventos de Tweet con hello **registroen**, **tema**, y **SentimentScore** valores que se va a enviar tooyour concentrador de eventos.</span><span class="sxs-lookup"><span data-stu-id="4902c-232">You see Tweet events with hello **CreatedAt**, **Topic**, and **SentimentScore** values being sent tooyour event hub.</span></span>

    ![Aplicación de TwitterWpfClient en ejecución, mostrando una lista de tweets](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-twitter-app-listing.png)

    >[!NOTE]
    ><span data-ttu-id="4902c-234">Si ve errores y no ve una secuencia de tweets de muestra en la parte inferior de Hola de ventana hello, vuelva a comprobar los secretos y las claves de Hola.</span><span class="sxs-lookup"><span data-stu-id="4902c-234">If you see errors, and you don't see a stream of tweets displayed in hello lower part of hello window, double-check hello keys and secrets.</span></span> <span data-ttu-id="4902c-235">Compruebe también la cadena de conexión de hello (asegúrese de que no incluyen hello `EntityPath` clave y valor.)</span><span class="sxs-lookup"><span data-stu-id="4902c-235">Also check hello connection string (make sure that it does not include hello `EntityPath` key and value.)</span></span>


## <a name="create-a-stream-analytics-job"></a><span data-ttu-id="4902c-236">Creación de un trabajo de Análisis de transmisiones</span><span class="sxs-lookup"><span data-stu-id="4902c-236">Create a Stream Analytics job</span></span>

<span data-ttu-id="4902c-237">Ahora que están transmitiendo por secuencias de eventos de tweet en tiempo real de Twitter, puede configurar una tooanalyze de trabajo de análisis de transmisiones estos eventos en tiempo real.</span><span class="sxs-lookup"><span data-stu-id="4902c-237">Now that tweet events are streaming in real time from Twitter, you can set up a Stream Analytics job tooanalyze these events in real time.</span></span>

1. <span data-ttu-id="4902c-238">Hola portal de Azure, haga clic en **New** > **Internet de las cosas** > **trabajo de análisis de transmisiones**.</span><span class="sxs-lookup"><span data-stu-id="4902c-238">In hello Azure portal, click **New** > **Internet of Things** > **Stream Analytics job**.</span></span>

2. <span data-ttu-id="4902c-239">Nombre de trabajo de hello `socialtwitter-sa-job` y especifique una suscripción, el grupo de recursos y la ubicación.</span><span class="sxs-lookup"><span data-stu-id="4902c-239">Name hello job `socialtwitter-sa-job` and specify a subscription, resource group, and location.</span></span>

    <span data-ttu-id="4902c-240">Es una buena idea tooplace Hola hello y trabajo Centro de eventos en hello misma región para optimizar el rendimiento y lo que no hay tootransfer datos entre regiones.</span><span class="sxs-lookup"><span data-stu-id="4902c-240">It's a good idea tooplace hello job and hello event hub in hello same region for best performance and so that you don't pay tootransfer data between regions.</span></span>

    ![Creación de un trabajo de Stream Analytics](./media/stream-analytics-twitter-sentiment-analysis-trends/newjob.png)

3. <span data-ttu-id="4902c-242">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="4902c-242">Click **Create**.</span></span>

    <span data-ttu-id="4902c-243">se crea el trabajo de Hola y portal de hello muestra detalles del trabajo.</span><span class="sxs-lookup"><span data-stu-id="4902c-243">hello job is created and hello portal displays job details.</span></span>


## <a name="specify-hello-job-input"></a><span data-ttu-id="4902c-244">Especificar la entrada de trabajo de Hola</span><span class="sxs-lookup"><span data-stu-id="4902c-244">Specify hello job input</span></span>

1. <span data-ttu-id="4902c-245">En el trabajo de análisis de transmisiones, en **trabajo topología** en medio de Hola de hoja de trabajo de hello, haga clic en **entradas**.</span><span class="sxs-lookup"><span data-stu-id="4902c-245">In your Stream Analytics job, under **Job Topology** in hello middle of hello job blade, click **Inputs**.</span></span> 

2. <span data-ttu-id="4902c-246">Hola **entradas** hoja, haga clic en  **+ &nbsp;agregar** y, a continuación, rellene hoja Hola con estos valores:</span><span class="sxs-lookup"><span data-stu-id="4902c-246">In hello **Inputs** blade, click **+&nbsp;Add** and then fill out hello blade with these values:</span></span>

    * <span data-ttu-id="4902c-247">**Alias de entrada**: usar el nombre de hello `TwitterStream`.</span><span class="sxs-lookup"><span data-stu-id="4902c-247">**Input alias**: Use hello name `TwitterStream`.</span></span> <span data-ttu-id="4902c-248">Si usa otro nombre, anótelo porque lo necesitará más adelante.</span><span class="sxs-lookup"><span data-stu-id="4902c-248">If you use a different name, make a note of it because you need it later.</span></span>
    * <span data-ttu-id="4902c-249">**Tipo de origen**: seleccione **Flujo de datos**.</span><span class="sxs-lookup"><span data-stu-id="4902c-249">**Source type**: Select **Data stream**.</span></span>
    * <span data-ttu-id="4902c-250">**Origen**: seleccione **Centro de eventos**.</span><span class="sxs-lookup"><span data-stu-id="4902c-250">**Source**: Select **Event hub**.</span></span>
    * <span data-ttu-id="4902c-251">**Opción de importación**: seleccione **Usar centro de eventos de la suscripción actual**.</span><span class="sxs-lookup"><span data-stu-id="4902c-251">**Import option**: Select **Use event hub from current subscription**.</span></span> 
    * <span data-ttu-id="4902c-252">**Espacio de nombres de bus de servicio**: seleccione el espacio de nombres de la base de datos central de eventos de Hola que creó anteriormente (`<yourname>-socialtwitter-eh-ns`).</span><span class="sxs-lookup"><span data-stu-id="4902c-252">**Service bus namespace**: Select hello event hub namespace that you created earlier (`<yourname>-socialtwitter-eh-ns`).</span></span>
    * <span data-ttu-id="4902c-253">**Centro de eventos**: Centro de eventos de hello Select que creó anteriormente (`socialtwitter-eh`).</span><span class="sxs-lookup"><span data-stu-id="4902c-253">**Event hub**: Select hello event hub that you created earlier (`socialtwitter-eh`).</span></span>
    * <span data-ttu-id="4902c-254">**Nombre de directiva de centro de eventos**: seleccione la directiva de acceso de Hola que creó anteriormente (`socialtwitter-access`).</span><span class="sxs-lookup"><span data-stu-id="4902c-254">**Event hub policy name**: Select hello access policy that you created earlier (`socialtwitter-access`).</span></span>

    ![Creación de una entrada del trabajo de Stream Analytics](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-twitter-new-input.png)

3. <span data-ttu-id="4902c-256">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="4902c-256">Click **Create**.</span></span>


## <a name="specify-hello-job-query"></a><span data-ttu-id="4902c-257">Especifique la consulta de la tarea hello</span><span class="sxs-lookup"><span data-stu-id="4902c-257">Specify hello job query</span></span>

<span data-ttu-id="4902c-258">Stream Analytics admite un modelo de consulta declarativa simple que describe las transformaciones.</span><span class="sxs-lookup"><span data-stu-id="4902c-258">Stream Analytics supports a simple, declarative query model that describes transformations.</span></span> <span data-ttu-id="4902c-259">toolearn más información acerca del lenguaje de hello, vea hello [referencia de lenguaje de consulta de análisis de transmisiones de Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx).</span><span class="sxs-lookup"><span data-stu-id="4902c-259">toolearn more about hello language, see hello [Azure Stream Analytics Query Language Reference](https://msdn.microsoft.com/library/azure/dn834998.aspx).</span></span>  <span data-ttu-id="4902c-260">Este tutorial le ayuda a crear y probar varias consultas sobre datos de Twitter.</span><span class="sxs-lookup"><span data-stu-id="4902c-260">This tutorial helps you author and test several queries over Twitter data.</span></span>

<span data-ttu-id="4902c-261">número de hello toocompare de menciones entre los temas, puede usar un [ventana de saltos de tamaño constante](https://msdn.microsoft.com/library/azure/dn835055.aspx) recuento de hello tooget de menciones por tema cada cinco segundos.</span><span class="sxs-lookup"><span data-stu-id="4902c-261">toocompare hello number of mentions among topics, you can use a [Tumbling window](https://msdn.microsoft.com/library/azure/dn835055.aspx) tooget hello count of mentions by topic every five seconds.</span></span>

1. <span data-ttu-id="4902c-262">Hola cerrar **entradas** hoja si no lo ha hecho ya.</span><span class="sxs-lookup"><span data-stu-id="4902c-262">Close hello **Inputs** blade if you haven't already.</span></span>

2. <span data-ttu-id="4902c-263">En la hoja de trabajo de hello, haga clic en hello **consulta** cuadro.</span><span class="sxs-lookup"><span data-stu-id="4902c-263">In hello job blade, click hello **Query** box.</span></span> <span data-ttu-id="4902c-264">Azure muestra entradas de Hola y salidas que se configuran para el trabajo de Hola y le permite crear una consulta que permite transforman flujo de entrada de hello mientras envía toohello salida.</span><span class="sxs-lookup"><span data-stu-id="4902c-264">Azure lists hello inputs and outputs that are configured for hello job, and lets you create a query that lets you transform hello input stream as it is sent toohello output.</span></span>

3. <span data-ttu-id="4902c-265">Asegúrese de que se ejecuta dicha aplicación TwitterWpfClient Hola.</span><span class="sxs-lookup"><span data-stu-id="4902c-265">Make sure that hello TwitterWpfClient application is running.</span></span> 

3. <span data-ttu-id="4902c-266">Hola **consulta** hoja, haga clic en hello puntos siguiente toohello `TwitterStream` de entrada y, a continuación, seleccione **datos a partir de datos de ejemplo**.</span><span class="sxs-lookup"><span data-stu-id="4902c-266">In hello **Query** blade, click hello dots next toohello `TwitterStream` input and then select **Sample data from input**.</span></span>

    ![Menú Opciones toouse datos de ejemplo de Hola entrada de trabajo de análisis de transmisión por secuencias, con "Datos de ejemplo de entrada" seleccionados](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-sample-data-from-input.png)

    <span data-ttu-id="4902c-268">Se abrirá una hoja que le permite especificar la cantidad tooget de datos de ejemplo, definido en términos de cuánto tiempo tooread hello secuencia de entrada.</span><span class="sxs-lookup"><span data-stu-id="4902c-268">This opens a blade that lets you specify how much sample data tooget, defined in terms of how long tooread hello input stream.</span></span>

4. <span data-ttu-id="4902c-269">Establecer **minutos** too3 y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="4902c-269">Set **Minutes** too3 and then click **OK**.</span></span> 
    
    ![Opciones de muestreo de flujo de entrada de hello, con "3 minutos" seleccionados.](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-input-create-sample-data.png)

    <span data-ttu-id="4902c-271">Azure muestrea los datos del flujo de entrada de hello correspondientes a tres minutos y le avisa cuando los datos de ejemplo de Hola están listos.</span><span class="sxs-lookup"><span data-stu-id="4902c-271">Azure samples 3 minutes' worth of data from hello input stream and notifies you when hello sample data is ready.</span></span> <span data-ttu-id="4902c-272">(Tardará unos minutos).</span><span class="sxs-lookup"><span data-stu-id="4902c-272">(This takes a short while.)</span></span> 

    <span data-ttu-id="4902c-273">datos de ejemplo de Hola se almacenan temporalmente y están disponibles mientras tiene la ventana de consulta de hello abierto.</span><span class="sxs-lookup"><span data-stu-id="4902c-273">hello sample data is stored temporarily and is available while you have hello query window open.</span></span> <span data-ttu-id="4902c-274">Si cierra la ventana de consulta de hello, se descartan los datos de ejemplo de Hola y tiene toocreate un nuevo conjunto de datos de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="4902c-274">If you close hello query window, hello sample data is discarded, and you have toocreate a new set of sample data.</span></span> 

5. <span data-ttu-id="4902c-275">Cambie la consulta de hello en hello código editor toohello que sigue:</span><span class="sxs-lookup"><span data-stu-id="4902c-275">Change hello query in hello code editor toohello following:</span></span>

    ```
    SELECT System.Timestamp as Time, Topic, COUNT(*)
    FROM TwitterStream TIMESTAMP BY CreatedAt
    GROUP BY TUMBLINGWINDOW(s, 5), Topic
    ```

    <span data-ttu-id="4902c-276">Si no usó `TwitterStream` como Hola alias para la entrada de hello, sustituya su alias para `TwitterStream` en consulta Hola.</span><span class="sxs-lookup"><span data-stu-id="4902c-276">If didn't use `TwitterStream` as hello alias for hello input, substitute your alias for `TwitterStream` in hello query.</span></span>  

    <span data-ttu-id="4902c-277">Esta consulta utiliza hello **TIMESTAMP BY** toospecify un campo de marca de tiempo en hello carga toobe utilizado en el cálculo temporal Hola de palabra clave.</span><span class="sxs-lookup"><span data-stu-id="4902c-277">This query uses hello **TIMESTAMP BY** keyword toospecify a timestamp field in hello payload toobe used in hello temporal computation.</span></span> <span data-ttu-id="4902c-278">Si no se especifica este campo, operación basada en ventanas de Hola se realiza mediante el tiempo de Hola que cada evento llegaron al concentrador de eventos de Hola.</span><span class="sxs-lookup"><span data-stu-id="4902c-278">If this field isn't specified, hello windowing operation is performed by using hello time that each event arrived at hello event hub.</span></span> <span data-ttu-id="4902c-279">Obtenga más información en la sección de Hola "hora de llegada frente a tiempo de aplicación" de [referencia de consulta de análisis de transmisiones](https://msdn.microsoft.com/library/azure/dn834998.aspx).</span><span class="sxs-lookup"><span data-stu-id="4902c-279">Learn more in hello "Arrival Time vs Application Time" section of [Stream Analytics Query Reference](https://msdn.microsoft.com/library/azure/dn834998.aspx).</span></span>

    <span data-ttu-id="4902c-280">Esta consulta también tiene acceso a una marca de tiempo para el fin de Hola de cada ventana mediante hello **System.Timestamp** propiedad.</span><span class="sxs-lookup"><span data-stu-id="4902c-280">This query also accesses a timestamp for hello end of each window by using hello **System.Timestamp** property.</span></span>

5. <span data-ttu-id="4902c-281">Haga clic en **Probar**.</span><span class="sxs-lookup"><span data-stu-id="4902c-281">Click **Test**.</span></span> <span data-ttu-id="4902c-282">Hola consulta se ejecuta con datos de Hola que realizó el muestreo.</span><span class="sxs-lookup"><span data-stu-id="4902c-282">hello query runs against hello data that you sampled.</span></span>
    
6. <span data-ttu-id="4902c-283">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="4902c-283">Click **Save**.</span></span> <span data-ttu-id="4902c-284">Esto ahorra consulta hello como parte del trabajo de análisis de transmisión por secuencias de Hola.</span><span class="sxs-lookup"><span data-stu-id="4902c-284">This saves hello query as part of hello Streaming Analytics job.</span></span> <span data-ttu-id="4902c-285">(No guardar los datos de ejemplo de Hola.)</span><span class="sxs-lookup"><span data-stu-id="4902c-285">(It doesn't save hello sample data.)</span></span>


## <a name="experiment-using-different-fields-from-hello-stream"></a><span data-ttu-id="4902c-286">Experimentar con distintos campos de secuencia de Hola</span><span class="sxs-lookup"><span data-stu-id="4902c-286">Experiment using different fields from hello stream</span></span> 

<span data-ttu-id="4902c-287">Hello tabla siguiente enumeran los campos de Hola que forman parte del programa Hola a datos de transmisión por secuencias de JSON.</span><span class="sxs-lookup"><span data-stu-id="4902c-287">hello following table lists hello fields that are part of hello JSON streaming data.</span></span> <span data-ttu-id="4902c-288">Sentirse tooexperiment disponible en el editor de consultas Hola.</span><span class="sxs-lookup"><span data-stu-id="4902c-288">Feel free tooexperiment in hello query editor.</span></span>

|<span data-ttu-id="4902c-289">Propiedad JSON</span><span class="sxs-lookup"><span data-stu-id="4902c-289">JSON property</span></span> | <span data-ttu-id="4902c-290">Definición</span><span class="sxs-lookup"><span data-stu-id="4902c-290">Definition</span></span>|
|--- | ---|
|<span data-ttu-id="4902c-291">CreatedAt</span><span class="sxs-lookup"><span data-stu-id="4902c-291">CreatedAt</span></span> | <span data-ttu-id="4902c-292">tiempo de Hola se creó ese tweet Hola</span><span class="sxs-lookup"><span data-stu-id="4902c-292">hello time that hello tweet was created</span></span>|
|<span data-ttu-id="4902c-293">Tema.</span><span class="sxs-lookup"><span data-stu-id="4902c-293">Topic</span></span> | <span data-ttu-id="4902c-294">tema de Hola que coincide con hello especificados (palabra clave)</span><span class="sxs-lookup"><span data-stu-id="4902c-294">hello topic that matches hello specified keyword</span></span>|
|<span data-ttu-id="4902c-295">SentimentScore</span><span class="sxs-lookup"><span data-stu-id="4902c-295">SentimentScore</span></span> | <span data-ttu-id="4902c-296">puntuación de opinión de Hola de Sentiment140</span><span class="sxs-lookup"><span data-stu-id="4902c-296">hello sentiment score from Sentiment140</span></span>|
|<span data-ttu-id="4902c-297">Autor</span><span class="sxs-lookup"><span data-stu-id="4902c-297">Author</span></span> | <span data-ttu-id="4902c-298">identificador de Twitter de Hola que envían tweet Hola</span><span class="sxs-lookup"><span data-stu-id="4902c-298">hello Twitter handle that sent hello tweet</span></span>|
|<span data-ttu-id="4902c-299">Texto</span><span class="sxs-lookup"><span data-stu-id="4902c-299">Text</span></span> | <span data-ttu-id="4902c-300">cuerpo total de Hola de tweet Hola</span><span class="sxs-lookup"><span data-stu-id="4902c-300">hello full body of hello tweet</span></span>|


## <a name="create-an-output-sink"></a><span data-ttu-id="4902c-301">Creación de un receptor de salida</span><span class="sxs-lookup"><span data-stu-id="4902c-301">Create an output sink</span></span>

<span data-ttu-id="4902c-302">Ahora ha definido un flujo de eventos, una entrada tooingest de concentrador de eventos y un tooperform consulta una transformación en secuencia Hola.</span><span class="sxs-lookup"><span data-stu-id="4902c-302">You have now defined an event stream, an event hub input tooingest events, and a query tooperform a transformation over hello stream.</span></span> <span data-ttu-id="4902c-303">Hola último paso es toodefine un receptor de salida para el trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="4902c-303">hello last step is toodefine an output sink for hello job.</span></span>  

<span data-ttu-id="4902c-304">En este tutorial, escribe Hola agregado tweet eventos desde Hola trabajo consulta tooAzure almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="4902c-304">In this tutorial, you write hello aggregated tweet events from hello job query tooAzure Blob storage.</span></span>  <span data-ttu-id="4902c-305">También puede insertar su tooAzure de resultados de la base de datos de SQL, almacenamiento de tabla de Azure, los concentradores de eventos, o Power BI, dependiendo de la aplicación necesita.</span><span class="sxs-lookup"><span data-stu-id="4902c-305">You can also push your results tooAzure SQL Database, Azure Table storage, Event Hubs, or Power BI, depending on your application needs.</span></span>

## <a name="specify-hello-job-output"></a><span data-ttu-id="4902c-306">Especificar la salida del trabajo Hola</span><span class="sxs-lookup"><span data-stu-id="4902c-306">Specify hello job output</span></span>

1. <span data-ttu-id="4902c-307">Hola **trabajo topología** sección, haga clic en hello **salida** cuadro.</span><span class="sxs-lookup"><span data-stu-id="4902c-307">In hello **Job Topology** section, click hello **Output** box.</span></span> 

2. <span data-ttu-id="4902c-308">Hola **salidas** hoja, haga clic en  **+ &nbsp;agregar** y, a continuación, rellene hoja Hola con estos valores:</span><span class="sxs-lookup"><span data-stu-id="4902c-308">In hello **Outputs** blade, click **+&nbsp;Add** and then fill out hello blade with these values:</span></span>

    * <span data-ttu-id="4902c-309">**Alias de salida**: usar el nombre de hello `TwitterStream-Output`.</span><span class="sxs-lookup"><span data-stu-id="4902c-309">**Output alias**: Use hello name `TwitterStream-Output`.</span></span> 
    * <span data-ttu-id="4902c-310">**Receptor**: seleccione **Blob Storage**.</span><span class="sxs-lookup"><span data-stu-id="4902c-310">**Sink**: Select **Blob storage**.</span></span>
    * <span data-ttu-id="4902c-311">**Opciones de importación**: seleccione **Usar almacenamiento de blobs de la suscripción actual**.</span><span class="sxs-lookup"><span data-stu-id="4902c-311">**Import options**: Select **Use blob storage from current subscription**.</span></span>
    * <span data-ttu-id="4902c-312">**Cuenta de Storage**.</span><span class="sxs-lookup"><span data-stu-id="4902c-312">**Storage account**.</span></span> <span data-ttu-id="4902c-313">Seleccione **Crear una nueva cuenta de almacenamiento**.</span><span class="sxs-lookup"><span data-stu-id="4902c-313">Select **Create a new storage account.**</span></span>
    * <span data-ttu-id="4902c-314">**Cuenta de Storage** (segundo cuadro).</span><span class="sxs-lookup"><span data-stu-id="4902c-314">**Storage account** (second box).</span></span> <span data-ttu-id="4902c-315">Escriba `YOURNAMEsa`, donde `YOURNAME` sea su nombre u otra cadena única.</span><span class="sxs-lookup"><span data-stu-id="4902c-315">Enter `YOURNAMEsa`, where `YOURNAME` is your name or another unique string.</span></span> <span data-ttu-id="4902c-316">nombre de Hello puede usar solo letras minúsculas y números, y debe ser único en Azure.</span><span class="sxs-lookup"><span data-stu-id="4902c-316">hello name can use only lowercase letters and numbers, and it must be unique across Azure.</span></span> 
    * <span data-ttu-id="4902c-317">**Contenedor**.</span><span class="sxs-lookup"><span data-stu-id="4902c-317">**Container**.</span></span> <span data-ttu-id="4902c-318">Escriba `socialtwitter`.</span><span class="sxs-lookup"><span data-stu-id="4902c-318">Enter `socialtwitter`.</span></span>
    <span data-ttu-id="4902c-319">nombre de cuenta de almacenamiento de Hola y el nombre del contenedor son tooprovide junto usa un URI para el almacenamiento de blobs de hello, similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="4902c-319">hello storage account name and container name are used together tooprovide a URI for hello blob storage, like this:</span></span> 

    `http://YOURNAMEsa.blob.core.windows.net/socialtwitter/...`
    
    ![Hoja "Nueva salida" del trabajo de Stream Analytics](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-output-blob-storage.png)
    
4. <span data-ttu-id="4902c-321">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="4902c-321">Click **Create**.</span></span> 

    <span data-ttu-id="4902c-322">Azure crea la cuenta de almacenamiento de Hola y genera una clave automáticamente.</span><span class="sxs-lookup"><span data-stu-id="4902c-322">Azure creates hello storage account and generates a key automatically.</span></span> 

5. <span data-ttu-id="4902c-323">Hola cerrar **salidas** hoja.</span><span class="sxs-lookup"><span data-stu-id="4902c-323">Close hello **Outputs** blade.</span></span> 


## <a name="start-hello-job"></a><span data-ttu-id="4902c-324">Iniciar el trabajo de Hola</span><span class="sxs-lookup"><span data-stu-id="4902c-324">Start hello job</span></span>

<span data-ttu-id="4902c-325">Se especifican una entrada de trabajo, la consulta y la salida.</span><span class="sxs-lookup"><span data-stu-id="4902c-325">A job input, query, and output are specified.</span></span> <span data-ttu-id="4902c-326">Son trabajo de análisis de transmisiones de hello toostart listo.</span><span class="sxs-lookup"><span data-stu-id="4902c-326">You are ready toostart hello Stream Analytics job.</span></span>

1. <span data-ttu-id="4902c-327">Asegúrese de que se ejecuta dicha aplicación TwitterWpfClient Hola.</span><span class="sxs-lookup"><span data-stu-id="4902c-327">Make sure that hello TwitterWpfClient application is running.</span></span> 

2. <span data-ttu-id="4902c-328">En la hoja de trabajo de hello, haga clic en **iniciar**.</span><span class="sxs-lookup"><span data-stu-id="4902c-328">In hello job blade, click **Start**.</span></span>

    ![Iniciar el trabajo de análisis de transmisiones de Hola](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-sa-job-start-output.png)

3. <span data-ttu-id="4902c-330">Hola **Start job** hoja, para **hora de inicio de salida del trabajo**, seleccione **ahora** y, a continuación, haga clic en **iniciar**.</span><span class="sxs-lookup"><span data-stu-id="4902c-330">In hello **Start job** blade, for **Job output start time**, select **Now** and then click **Start**.</span></span> 

    !["Iniciar el trabajo" hoja de trabajo de análisis de transmisiones de Hola](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-sa-job-start-job-blade.png)

    <span data-ttu-id="4902c-332">Azure le avisa cuando ha iniciado el trabajo de Hola y de hoja de trabajo de hello, estado de Hola se muestra como **ejecutando**.</span><span class="sxs-lookup"><span data-stu-id="4902c-332">Azure notifies you when hello job has started, and in hello job blade, hello status is displayed as **Running**.</span></span>

    ![Trabajo en ejecución](./media/stream-analytics-twitter-sentiment-analysis-trends/jobrunning.png)

## <a name="view-output-for-sentiment-analysis"></a><span data-ttu-id="4902c-334">Consulta de la salida del análisis de opinión</span><span class="sxs-lookup"><span data-stu-id="4902c-334">View output for sentiment analysis</span></span>

<span data-ttu-id="4902c-335">Después de que el trabajo ha empezado a ejecutarse y está procesando transmisiones en tiempo real de Twitter de hello, puede ver la salida de hello para el análisis de opiniones.</span><span class="sxs-lookup"><span data-stu-id="4902c-335">After your job has started running and is processing hello real-time Twitter stream, you can view hello output for sentiment analysis.</span></span>

<span data-ttu-id="4902c-336">Puede usar una herramienta como [Azure Storage Explorer](https://http://storageexplorer.com/) o [explorador Azure](http://www.cerebrata.com/products/azure-explorer/introduction) tooview su trabajo de salida en tiempo real.</span><span class="sxs-lookup"><span data-stu-id="4902c-336">You can use a tool like [Azure Storage Explorer](https://http://storageexplorer.com/) or [Azure Explorer](http://www.cerebrata.com/products/azure-explorer/introduction) tooview your job output in real time.</span></span> <span data-ttu-id="4902c-337">Desde aquí, puede usar [Power BI](https://powerbi.com/) tooextend su tooinclude de aplicación un panel personalizado, como se muestra en la siguiente captura de pantalla de Hola Hola:</span><span class="sxs-lookup"><span data-stu-id="4902c-337">From here, you can use [Power BI](https://powerbi.com/) tooextend your application tooinclude a customized dashboard like hello one shown in hello following screenshot:</span></span>

![Power BI](./media/stream-analytics-twitter-sentiment-analysis-trends/power-bi.png)


## <a name="create-another-query-tooidentify-trending-topics"></a><span data-ttu-id="4902c-339">Cree otra consulta tooidentify tendencias temas</span><span class="sxs-lookup"><span data-stu-id="4902c-339">Create another query tooidentify trending topics</span></span>

<span data-ttu-id="4902c-340">Puede usar la opinión de Twitter toounderstand de otra consulta se basa en un [ventana deslizante](https://msdn.microsoft.com/library/azure/dn835051.aspx).</span><span class="sxs-lookup"><span data-stu-id="4902c-340">Another query you can use toounderstand Twitter sentiment is based on a [Sliding Window](https://msdn.microsoft.com/library/azure/dn835051.aspx).</span></span> <span data-ttu-id="4902c-341">tooidentify temas tendencias, busca temas que cruzan un valor de umbral para menciones en un período de tiempo especificado.</span><span class="sxs-lookup"><span data-stu-id="4902c-341">tooidentify trending topics, you look for topics that cross a threshold value for mentions in a specified amount of time.</span></span>

<span data-ttu-id="4902c-342">Para fines de Hola de este tutorial, busque los temas que se mencionan más de 20 veces en hello últimos 5 segundos.</span><span class="sxs-lookup"><span data-stu-id="4902c-342">For hello purposes of this tutorial, you check for topics that are mentioned more than 20 times in hello last 5 seconds.</span></span>

1. <span data-ttu-id="4902c-343">En la hoja de trabajo de hello, haga clic en **detener** trabajo de hello toostop.</span><span class="sxs-lookup"><span data-stu-id="4902c-343">In hello job blade, click **Stop** toostop hello job.</span></span> 

2. <span data-ttu-id="4902c-344">Hola **trabajo topología** sección, haga clic en hello **consulta** cuadro.</span><span class="sxs-lookup"><span data-stu-id="4902c-344">In hello **Job Topology** section, click hello **Query** box.</span></span> 

3. <span data-ttu-id="4902c-345">Cambiar Hola consulta toohello a continuación:</span><span class="sxs-lookup"><span data-stu-id="4902c-345">Change hello query toohello following:</span></span>

    ```    
    SELECT System.Timestamp as Time, Topic, COUNT(*) as Mentions
    FROM TwitterStream TIMESTAMP BY CreatedAt
    GROUP BY SLIDINGWINDOW(s, 5), topic
    HAVING COUNT(*) > 20
    ```

4. <span data-ttu-id="4902c-346">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="4902c-346">Click **Save**.</span></span>

5. <span data-ttu-id="4902c-347">Asegúrese de que se ejecuta dicha aplicación TwitterWpfClient Hola.</span><span class="sxs-lookup"><span data-stu-id="4902c-347">Make sure that hello TwitterWpfClient application is running.</span></span> 

6. <span data-ttu-id="4902c-348">Haga clic en **iniciar** trabajo de hello toorestart mediante Hola nueva consulta.</span><span class="sxs-lookup"><span data-stu-id="4902c-348">Click **Start** toorestart hello job using hello new query.</span></span>


## <a name="get-support"></a><span data-ttu-id="4902c-349">Obtención de soporte técnico</span><span class="sxs-lookup"><span data-stu-id="4902c-349">Get support</span></span>
<span data-ttu-id="4902c-350">Para obtener más ayuda, pruebe nuestro [foro de Análisis de transmisiones de Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="4902c-350">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4902c-351">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4902c-351">Next steps</span></span>
* [<span data-ttu-id="4902c-352">Introducción tooAzure análisis de transmisiones</span><span class="sxs-lookup"><span data-stu-id="4902c-352">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="4902c-353">Introducción al uso de Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="4902c-353">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="4902c-354">Escalación de trabajos de Análisis de transmisiones de Azure</span><span class="sxs-lookup"><span data-stu-id="4902c-354">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="4902c-355">Referencia del lenguaje de consulta de Análisis de transmisiones de Azure</span><span class="sxs-lookup"><span data-stu-id="4902c-355">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="4902c-356">Referencia de API de REST de administración de Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="4902c-356">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
