---
title: "procesamiento en tiempo real de aaaStream análisis para las funciones de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse una función de Azure había conectada una cola de Bus de servicio, toopopulate una caché en Redis de Azure desde la salida de hello de un trabajo de análisis de transmisiones."
keywords: "flujo de datos, caché en redis, cola del bus de servicio"
services: stream-analytics
author: ryancrawcour
manager: jhubbard
documentationcenter: 
ms.assetid: d428bb33-4244-4001-b93d-c77bed816527
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/28/2017
ms.author: ryancraw
ms.openlocfilehash: 5ef4fe76c2cadf896a80eeaf421f010c315918af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toostore-data-from-azure-stream-analytics-in-an-azure-redis-cache-using-azure-functions"></a><span data-ttu-id="ea075-104">¿Cómo toostore datos de análisis de transmisiones de Azure en una caché en Redis de Azure mediante las funciones de Azure</span><span class="sxs-lookup"><span data-stu-id="ea075-104">How toostore data from Azure Stream Analytics in an Azure Redis Cache using Azure Functions</span></span>
<span data-ttu-id="ea075-105">Análisis de transmisiones de Azure le permite desarrollar e implementar soluciones de bajo coste toogain en tiempo real conocimientos dispositivos, sensores, infraestructura y las aplicaciones o cualquier flujo de datos rápidamente.</span><span class="sxs-lookup"><span data-stu-id="ea075-105">Azure Stream Analytics lets you rapidly develop and deploy low-cost solutions toogain real-time insights from devices, sensors, infrastructure, and applications, or any stream of data.</span></span> <span data-ttu-id="ea075-106">Permite varios casos de uso, como la administración y supervisión en tiempo real, comando y control, detección de fraudes, automóviles conectados y mucho más.</span><span class="sxs-lookup"><span data-stu-id="ea075-106">It enables various use cases such as real-time management and monitoring, command and control, fraud detection, connected cars and many more.</span></span> <span data-ttu-id="ea075-107">En muchos de estos escenarios, puede que desee datos toostore arroja análisis de transmisiones de Azure en un almacén de datos distribuidos como una caché en Redis de Azure.</span><span class="sxs-lookup"><span data-stu-id="ea075-107">In many such scenarios, you may want toostore data outputted by Azure Stream Analytics into a distributed data store such as an Azure Redis cache.</span></span>

<span data-ttu-id="ea075-108">Imaginemos que forma parte de una empresa de telecomunicaciones.</span><span class="sxs-lookup"><span data-stu-id="ea075-108">Suppose you are part of a telecommunications company.</span></span> <span data-ttu-id="ea075-109">Está tratando de fraude SIM toodetect donde varias llamadas procedentes de Hola misma identidad, en Hola mismo tiempo, pero en diferentes geográficamente ubicaciones.</span><span class="sxs-lookup"><span data-stu-id="ea075-109">You are trying toodetect SIM fraud where multiple calls coming from hello same identity, at hello same time, but in different geographically locations.</span></span> <span data-ttu-id="ea075-110">Tiene que almacenar todos los Hola posibles fraudulentas llamadas en una caché en Redis de Azure.</span><span class="sxs-lookup"><span data-stu-id="ea075-110">You are tasked with storing all hello potential fraudulent phone calls in an Azure Redis cache.</span></span> <span data-ttu-id="ea075-111">En este blog, le brindamos la orientación que necesita para poder completar fácilmente la tarea.</span><span class="sxs-lookup"><span data-stu-id="ea075-111">In this blog, we provide guidance on how you can easily complete your task.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="ea075-112">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="ea075-112">Prerequisites</span></span>
<span data-ttu-id="ea075-113">Hola completa [detección de fraudes en tiempo real] [ fraud-detection] ejemplo paso a paso para ASA</span><span class="sxs-lookup"><span data-stu-id="ea075-113">Complete hello [Real-time Fraud Detection][fraud-detection] walk-through for ASA</span></span>

## <a name="architecture-overview"></a><span data-ttu-id="ea075-114">Introducción a la arquitectura</span><span class="sxs-lookup"><span data-stu-id="ea075-114">Architecture Overview</span></span>
![Captura de pantalla de arquitectura](./media/stream-analytics-functions-redis/architecture-overview.png)

<span data-ttu-id="ea075-116">Como se muestra en hello anterior figura, análisis de transmisiones permite toobe de datos de entrada de transmisión por secuencias, consulta y envíe el resultado de tooan.</span><span class="sxs-lookup"><span data-stu-id="ea075-116">As shown in hello preceding figure, Stream Analytics allows streaming input data toobe queried and sent tooan output.</span></span> <span data-ttu-id="ea075-117">En función de la salida de hello, funciones de Azure puede desencadenar algún tipo de evento.</span><span class="sxs-lookup"><span data-stu-id="ea075-117">Based on hello output, Azure Functions can then trigger some type of event.</span></span> 

<span data-ttu-id="ea075-118">En este blog, céntrese en parte de las funciones de Azure Hola de esta canalización o más concretamente Hola desencadenamiento de un evento que almacena datos fraudulentas en la memoria caché de Hola.</span><span class="sxs-lookup"><span data-stu-id="ea075-118">In this blog, we focus on hello Azure Functions part of this pipeline, or more specifically hello triggering of an event that stores fraudulent data into hello cache.</span></span>
<span data-ttu-id="ea075-119">Después de completar hello [detección de fraudes en tiempo real] [ fraud-detection] tutorial, tendrá una entrada (un concentrador de eventos), una consulta y una salida (almacenamiento de blobs) ya configurado y en ejecución.</span><span class="sxs-lookup"><span data-stu-id="ea075-119">After completing hello [Real-time Fraud Detection][fraud-detection] tutorial, you have an input (an event hub), a query, and an output (blob storage) already configured and running.</span></span> <span data-ttu-id="ea075-120">En este blog, cambiamos Hola salida toouse una cola de Bus de servicio en su lugar.</span><span class="sxs-lookup"><span data-stu-id="ea075-120">In this blog, we change hello output toouse a Service Bus Queue instead.</span></span> <span data-ttu-id="ea075-121">A continuación, nos conectamos a una cola de toothis de función de Azure.</span><span class="sxs-lookup"><span data-stu-id="ea075-121">After that, we connect an Azure Function toothis queue.</span></span> 

## <a name="create-and-connect-a-service-bus-queue-output"></a><span data-ttu-id="ea075-122">Creación y conexión de una salida de cola del Bus de servicio</span><span class="sxs-lookup"><span data-stu-id="ea075-122">Create and connect a Service Bus Queue output</span></span>
<span data-ttu-id="ea075-123">toocreate una cola de Bus de servicio, siga los pasos 1 y 2 de la sección de .NET de hello en [empezar a trabajar con colas de Service Bus][servicebus-getstarted].</span><span class="sxs-lookup"><span data-stu-id="ea075-123">toocreate a Service Bus Queue, follow steps 1 and 2 of hello .NET section in [Get Started with Service Bus Queues][servicebus-getstarted].</span></span>
<span data-ttu-id="ea075-124">Ahora vamos a conectar hello toohello análisis de transmisiones trabajo en cola que se creó en hello anterior tutorial de detección de fraudes.</span><span class="sxs-lookup"><span data-stu-id="ea075-124">Now let's connect hello queue toohello Stream Analytics job that was created in hello earlier fraud detection walk-through.</span></span>

1. <span data-ttu-id="ea075-125">Hola portal de Azure, vaya toohello **salidas** hoja de su trabajo y seleccione **agregar** al principio de Hola de página de Hola.</span><span class="sxs-lookup"><span data-stu-id="ea075-125">In hello Azure portal, go toohello **Outputs** blade of your job and select **Add** at hello top of hello page.</span></span>
   
    ![Agregar salidas](./media/stream-analytics-functions-redis/adding-outputs.png)
2. <span data-ttu-id="ea075-127">Elija **cola de Service Bus** como hello **receptor** y siga las instrucciones de hello en pantalla de bienvenida.</span><span class="sxs-lookup"><span data-stu-id="ea075-127">Choose **Service Bus Queue** as hello **Sink** and follow hello instructions on hello screen.</span></span> <span data-ttu-id="ea075-128">Seguro de espacio de nombres de hello toochoose de hello cola de Bus de servicio creará en [empezar a trabajar con colas de Service Bus][servicebus-getstarted].</span><span class="sxs-lookup"><span data-stu-id="ea075-128">Be sure toochoose hello namespace of hello Service Bus Queue you created in [Get Started with Service Bus Queues][servicebus-getstarted].</span></span> <span data-ttu-id="ea075-129">Cuando haya terminado, haga clic en el botón "secundario" Hola.</span><span class="sxs-lookup"><span data-stu-id="ea075-129">Click hello "right" button when you are finished.</span></span>
3. <span data-ttu-id="ea075-130">Especifique Hola siguientes valores:</span><span class="sxs-lookup"><span data-stu-id="ea075-130">Specify hello following values:</span></span>
   
   * <span data-ttu-id="ea075-131">**Formato del serializador de eventos**: JSON</span><span class="sxs-lookup"><span data-stu-id="ea075-131">**Event Serializer Format**: JSON</span></span>
   * <span data-ttu-id="ea075-132">**Codificación**: UTF8</span><span class="sxs-lookup"><span data-stu-id="ea075-132">**Encoding**: UTF8</span></span>
   * <span data-ttu-id="ea075-133">**FORMATO**: separado por líneas</span><span class="sxs-lookup"><span data-stu-id="ea075-133">**FORMAT**: Line separated</span></span>
4. <span data-ttu-id="ea075-134">Haga clic en hello **crear** botón tooadd este origen y tooverify que análisis de transmisiones puede conectarse correctamente toohello cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="ea075-134">Click hello **Create** button tooadd this source and tooverify that Stream Analytics can successfully connect toohello storage account.</span></span>
5. <span data-ttu-id="ea075-135">Hola **consulta** ficha, reemplace la consulta actual Hola por siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="ea075-135">In hello **Query** tab, replace hello current query with hello following.</span></span> <span data-ttu-id="ea075-136">Reemplazar * [su nombre de BUS de servicio] * con el nombre de la salida de hello que creó en el paso 3.</span><span class="sxs-lookup"><span data-stu-id="ea075-136">Replace *[YOUR SERVICE BUS NAME] * with hello output name you created in step 3.</span></span> 
   
    ```    
   
        SELECT 
            System.Timestamp as Time, CS1.CallingIMSI, CS1.CallingNum as CallingNum1, 
            CS2.CallingNum as CallingNum2, CS1.SwitchNum as Switch1, CS2.SwitchNum as Switch2
   
        INTO [YOUR SERVICE BUS NAME]
   
        FROM CallStream CS1 TIMESTAMP BY CallRecTime
        JOIN CallStream CS2 TIMESTAMP BY CallRecTime
            ON CS1.CallingIMSI = CS2.CallingIMSI AND DATEDIFF(ss, CS1, CS2) BETWEEN 1 AND 5
   
        WHERE CS1.SwitchNum != CS2.SwitchNum
   
    ```

## <a name="create-an-azure-redis-cache"></a><span data-ttu-id="ea075-137">Creación de una instancia de Caché en Redis de Azure</span><span class="sxs-lookup"><span data-stu-id="ea075-137">Create an Azure Redis Cache</span></span>
<span data-ttu-id="ea075-138">Crear una caché en Redis de Azure siguiendo la sección de .NET de hello en [cómo tooUse Azure Redis Cache] [ use-rediscache] hasta que llama a sección hello ***configurar clientes de caché de hello***.</span><span class="sxs-lookup"><span data-stu-id="ea075-138">Create an Azure Redis cache by following hello .NET section in [How tooUse Azure Redis Cache][use-rediscache] until hello section called ***Configure hello cache clients***.</span></span>
<span data-ttu-id="ea075-139">Una vez que finalice, tendrá una nueva instancia de Caché en Redis.</span><span class="sxs-lookup"><span data-stu-id="ea075-139">Once complete, you have a new Redis Cache.</span></span> <span data-ttu-id="ea075-140">En **toda la configuración de**, seleccione **las claves de acceso** y tome nota de hello ***cadena de conexión principal***.</span><span class="sxs-lookup"><span data-stu-id="ea075-140">Under **All settings**, select **Access keys** and note down hello ***Primary connection string***.</span></span>

![Captura de pantalla de arquitectura](./media/stream-analytics-functions-redis/redis-cache-keys.png)

## <a name="create-an-azure-function"></a><span data-ttu-id="ea075-142">Creación de una Función de Azure</span><span class="sxs-lookup"><span data-stu-id="ea075-142">Create an Azure Function</span></span>
<span data-ttu-id="ea075-143">Siga [crear su primera función Azure] [ functions-getstarted] tooget tutorial a trabajar con funciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="ea075-143">Follow [Create your first Azure Function][functions-getstarted] tutorial tooget started with Azure Functions.</span></span> <span data-ttu-id="ea075-144">Si ya tiene una función de Azure que debería como toouse y luego pase demasiado[tooRedis memoria caché de escritura](#Writing-to-Redis-Cache)</span><span class="sxs-lookup"><span data-stu-id="ea075-144">If you already have an Azure function you would like toouse, then skip ahead too[Writing tooRedis Cache](#Writing-to-Redis-Cache)</span></span>

1. <span data-ttu-id="ea075-145">En el portal de hello, seleccione Servicios de aplicaciones de navegación izquierdo de hello, a continuación, haga clic en el sitio Web de aplicación de la función Azure aplicación nombre tooget toohello la función.</span><span class="sxs-lookup"><span data-stu-id="ea075-145">In hello portal, select App Services from hello left-hand navigation, then click your Azure function app name tooget toohello Function's app website.</span></span>
    <span data-ttu-id="ea075-146">![Captura de pantalla de lista de funciones de App Services](./media/stream-analytics-functions-redis/app-services-function-list.png)</span><span class="sxs-lookup"><span data-stu-id="ea075-146">![Screenshot of app services function list](./media/stream-analytics-functions-redis/app-services-function-list.png)</span></span>
2. <span data-ttu-id="ea075-147">Haga clic en **Nueva función > ServiceBusQueueTrigger – C#**.</span><span class="sxs-lookup"><span data-stu-id="ea075-147">Click **New Function > ServiceBusQueueTrigger – C#**.</span></span> <span data-ttu-id="ea075-148">Para hello campos siguientes, siga estas instrucciones:</span><span class="sxs-lookup"><span data-stu-id="ea075-148">For hello following fields, follow these instructions:</span></span>
   
   * <span data-ttu-id="ea075-149">**Nombre de la cola**: Hola mismo nombre como nombre de Hola que especificó al crear cola de hello en [empezar a trabajar con colas de Service Bus] [ servicebus-getstarted] (no el nombre de Hola Hola del bus de servicio).</span><span class="sxs-lookup"><span data-stu-id="ea075-149">**Queue name**: hello same name as hello name you entered when you created hello queue in [Get Started with Service Bus Queues][servicebus-getstarted] (not hello name of hello service bus).</span></span> <span data-ttu-id="ea075-150">Asegúrese de que usar cola de Hola que está conectado toohello análisis de transmisiones de salida.</span><span class="sxs-lookup"><span data-stu-id="ea075-150">Make sure you use hello queue that is connected toohello Stream Analytics output.</span></span>
   * <span data-ttu-id="ea075-151">**Conexión de Service Bus**: seleccione **Agregar una cadena de conexión**.</span><span class="sxs-lookup"><span data-stu-id="ea075-151">**Service Bus connection**: Select **Add a connection string**.</span></span> <span data-ttu-id="ea075-152">cadena de conexión de hello toofind, vaya toohello portal clásico, seleccione **Service Bus**, Hola bus de servicio que creó, y **información de conexión** final Hola de pantalla de bienvenida.</span><span class="sxs-lookup"><span data-stu-id="ea075-152">toofind hello connection string, go toohello classic portal, select **Service Bus**, hello service bus you created, and **CONNECTION INFORMATION** at hello bottom of hello screen.</span></span> <span data-ttu-id="ea075-153">Asegúrese de que se encuentra en la pantalla principal de bienvenida en esta página.</span><span class="sxs-lookup"><span data-stu-id="ea075-153">Make sure you are on hello main screen on this page.</span></span> <span data-ttu-id="ea075-154">Copie y pegue la cadena de conexión de Hola.</span><span class="sxs-lookup"><span data-stu-id="ea075-154">Copy and paste hello connection string.</span></span> <span data-ttu-id="ea075-155">Sentirse tooenter libre cualquier nombre de la conexión.</span><span class="sxs-lookup"><span data-stu-id="ea075-155">Feel free tooenter any connection name.</span></span>
     
       ![Captura de pantalla de conexión del Bus de servicio](./media/stream-analytics-functions-redis/servicebus-connection.png)
   * <span data-ttu-id="ea075-157">**AccessRights**: elija **Administrar**.</span><span class="sxs-lookup"><span data-stu-id="ea075-157">**AccessRights**: Choose **Manage**</span></span>
3. <span data-ttu-id="ea075-158">Haga clic en **Crear**</span><span class="sxs-lookup"><span data-stu-id="ea075-158">Click **Create**</span></span>

## <a name="writing-tooredis-cache"></a><span data-ttu-id="ea075-159">TooRedis caché de escritura</span><span class="sxs-lookup"><span data-stu-id="ea075-159">Writing tooRedis Cache</span></span>
<span data-ttu-id="ea075-160">Creamos una función de Azure que lee desde una cola del Bus de servicio.</span><span class="sxs-lookup"><span data-stu-id="ea075-160">We have now created an Azure Function that reads from a Service Bus Queue.</span></span> <span data-ttu-id="ea075-161">Lo único que queda toodo es usar nuestro toowrite función este toohello datos caché en Redis.</span><span class="sxs-lookup"><span data-stu-id="ea075-161">All that is left toodo is use our Function toowrite this data toohello Redis Cache.</span></span> 

1. <span data-ttu-id="ea075-162">Seleccione el recién creado **ServiceBusQueueTrigger**y haga clic en **función de la configuración de la aplicación** en hello esquina superior derecha.</span><span class="sxs-lookup"><span data-stu-id="ea075-162">Select your newly created **ServiceBusQueueTrigger**, and click **Function app settings** on hello top right corner.</span></span> <span data-ttu-id="ea075-163">Seleccione **ir tooApp servicio Configuración > Configuración > configuración de la aplicación**</span><span class="sxs-lookup"><span data-stu-id="ea075-163">Select **Go tooApp Service Settings > Settings > Application settings**</span></span>
2. <span data-ttu-id="ea075-164">Hola sección cadenas de conexión, cree un nombre en hello **nombre** sección.</span><span class="sxs-lookup"><span data-stu-id="ea075-164">In hello Connection strings section, create a name in hello **Name** section.</span></span> <span data-ttu-id="ea075-165">Pegue la cadena de conexión principal de Hola que encontró en hello **crear una caché en Redis** recorra hello **valor** sección.</span><span class="sxs-lookup"><span data-stu-id="ea075-165">Paste hello primary connection string you found in hello **Create a Redis Cache** step into hello **Value** section.</span></span> <span data-ttu-id="ea075-166">Seleccione **Personalizado** donde aparece **SQL Database**.</span><span class="sxs-lookup"><span data-stu-id="ea075-166">Select **Custom** where it says **SQL Database**.</span></span>
3. <span data-ttu-id="ea075-167">Haga clic en **guardar** en la parte superior de Hola.</span><span class="sxs-lookup"><span data-stu-id="ea075-167">Click **Save** at hello top.</span></span>
   
    ![Captura de pantalla de conexión del Bus de servicio](./media/stream-analytics-functions-redis/function-connection-string.png)
4. <span data-ttu-id="ea075-169">Ahora vuelva toohello configuración de servicio de la aplicación y seleccione **Herramientas > Editor de aplicación de servicio (vista previa) > en > vaya**.</span><span class="sxs-lookup"><span data-stu-id="ea075-169">Now go back toohello App Service Settings and select **Tools > App Service Editor (Preview) > On > Go**.</span></span>
   
    ![Captura de pantalla de conexión del Bus de servicio](./media/stream-analytics-functions-redis/app-service-editor.png)
5. <span data-ttu-id="ea075-171">En un editor de su elección, cree un archivo JSON denominado **project.json** con Hola siguiente y guárdelo en disco local tooyour.</span><span class="sxs-lookup"><span data-stu-id="ea075-171">In an editor of your choice, create a JSON file named **project.json** with hello following and save it tooyour local disk.</span></span>
   
        {
            "frameworks": {
                "net46": {
                    "dependencies": {
                        "StackExchange.Redis":"1.1.603",
                        "Newtonsoft.Json": "9.0.1"
                    }
                }
            }
        }
6. <span data-ttu-id="ea075-172">Cargar este archivo en el directorio raíz de saludo de la función (no WWWROOT).</span><span class="sxs-lookup"><span data-stu-id="ea075-172">Upload this file into hello root directory of your function (not WWWROOT).</span></span> <span data-ttu-id="ea075-173">Debería ver un archivo denominado **project.lock.json** aparecen automáticamente, confirmando que Hola Nuget paquetes "StackExchange.Redis" y "Newtonsoft.Json" se han importado.</span><span class="sxs-lookup"><span data-stu-id="ea075-173">You should see a file named **project.lock.json** automatically appear, confirming that hello Nuget packages “StackExchange.Redis” and “Newtonsoft.Json” have been imported.</span></span>
7. <span data-ttu-id="ea075-174">Hola **run.csx** archivo, reemplace el código generados previamente Hola con el siguiente código de hello.</span><span class="sxs-lookup"><span data-stu-id="ea075-174">In hello **run.csx** file, replace hello pre-generated code with hello following code.</span></span> <span data-ttu-id="ea075-175">En función de lazyConnection hello, reemplace "CONN NAME" con el nombre de Hola que creó en el paso 2 de **almacenar datos en caché en Redis hello**.</span><span class="sxs-lookup"><span data-stu-id="ea075-175">In hello lazyConnection function, replace “CONN NAME” with hello name you created in step 2 of **Store data into hello Redis cache**.</span></span>

````

    using System;
    using System.Threading.Tasks;
    using StackExchange.Redis;
    using Newtonsoft.Json;
    using System.Configuration;

    public static void Run(string myQueueItem, TraceWriter log)
    {
        log.Info($"Function processed message: {myQueueItem}");

        // Connection refers tooa property that returns a ConnectionMultiplexer
        IDatabase db = Connection.GetDatabase();
        log.Info($"Created database {db}");

        // Parse JSON and extract hello time
        var message = JsonConvert.DeserializeObject<dynamic>(myQueueItem);
        string time = message.time;
        string callingnum1 = message.callingnum1;

        // Perform cache operations using hello cache object...
        // Simple put of integral data types into hello cache
        string key = time + " - " + callingnum1;
        db.StringSet(key, myQueueItem);
        log.Info($"Object put in database. Key is {key} and value is {myQueueItem}");

        // Simple get of data types from hello cache
        string value = db.StringGet(key);
        log.Info($"Database got: {value}"); 
    }

    // Connect toohello Service Bus
    private static Lazy<ConnectionMultiplexer> lazyConnection = 
        new Lazy<ConnectionMultiplexer>(() =>
            {
                var cnn = ConfigurationManager.ConnectionStrings["CONN NAME"].ConnectionString
                return ConnectionMultiplexer.Connect();
            });

    public static ConnectionMultiplexer Connection
    {
        get
        {
            return lazyConnection.Value;
        }
    }

````

## <a name="start-hello-stream-analytics-job"></a><span data-ttu-id="ea075-176">Iniciar el trabajo de análisis de transmisiones de Hola</span><span class="sxs-lookup"><span data-stu-id="ea075-176">Start hello Stream Analytics job</span></span>
1. <span data-ttu-id="ea075-177">Inicie la aplicación de hello telcodatagen.exe.</span><span class="sxs-lookup"><span data-stu-id="ea075-177">Start hello telcodatagen.exe application.</span></span> <span data-ttu-id="ea075-178">uso de Hello es como sigue:````telcodatagen.exe [#NumCDRsPerHour] [SIM Card Fraud Probability] [#DurationHours]````</span><span class="sxs-lookup"><span data-stu-id="ea075-178">hello usage is as follows: ````telcodatagen.exe [#NumCDRsPerHour] [SIM Card Fraud Probability] [#DurationHours]````</span></span>
2. <span data-ttu-id="ea075-179">En la hoja de trabajo de análisis de transmisiones de hello en el portal de hello, haga clic en **iniciar** al principio de Hola de página de Hola.</span><span class="sxs-lookup"><span data-stu-id="ea075-179">From hello Stream Analytics Job blade in hello portal, click **Start** at hello top of hello page.</span></span>
   
    ![Captura de pantalla de Iniciar trabajo](./media/stream-analytics-functions-redis/starting-job.png)
3. <span data-ttu-id="ea075-181">Hola **Start job** hoja que aparece, seleccione **ahora** y, a continuación, haga clic en hello **iniciar** situado en la parte inferior de Hola de pantalla de bienvenida.</span><span class="sxs-lookup"><span data-stu-id="ea075-181">In hello **Start job** blade that appears, select **Now** and then click hello **Start** button at hello bottom of hello screen.</span></span> <span data-ttu-id="ea075-182">estado del trabajo Hola cambia tooStarting y tarde tooRunning de cambios.</span><span class="sxs-lookup"><span data-stu-id="ea075-182">hello job status changes tooStarting and after some time changes tooRunning.</span></span>
   
    ![Captura de pantalla de selección de tiempo de Iniciar trabajo](./media/stream-analytics-functions-redis/start-job-time.png)

## <a name="run-solution-and-check-results"></a><span data-ttu-id="ea075-184">Ejecución de la solución y comprobación de los resultados</span><span class="sxs-lookup"><span data-stu-id="ea075-184">Run solution and check results</span></span>
<span data-ttu-id="ea075-185">Volviendo a tooyour **ServiceBusQueueTrigger** página, ahora debería ver las instrucciones de registro.</span><span class="sxs-lookup"><span data-stu-id="ea075-185">Going back tooyour **ServiceBusQueueTrigger** page, you should now see log statements.</span></span> <span data-ttu-id="ea075-186">Estos registros se muestran que se obtuvo algo Hola cola de Bus de servicio, póngalo en la base de datos de hello y captura usando tiempo hello como clave de Hola!</span><span class="sxs-lookup"><span data-stu-id="ea075-186">These logs show that you got something from hello Service Bus Queue, put it into hello database, and fetched it out using hello time as hello key!</span></span>

<span data-ttu-id="ea075-187">tooverify que los datos están en la memoria caché de Redis, ir a página de caché de Redis tooyour en el nuevo portal de hello (como se muestra en hello anterior [crear una caché en Redis de Azure](#Create-an-Azure-Redis-Cache) paso) y seleccione consola.</span><span class="sxs-lookup"><span data-stu-id="ea075-187">tooverify that your data is in your Redis cache, go tooyour Redis cache page in hello new portal (as shown in hello preceding [Create an Azure Redis Cache](#Create-an-Azure-Redis-Cache) step) and select Console.</span></span>

<span data-ttu-id="ea075-188">Ahora puede escribir Redis comandos tooconfirm que los datos se están en realidad en caché de Hola.</span><span class="sxs-lookup"><span data-stu-id="ea075-188">Now you can write Redis commands tooconfirm that data is in fact in hello cache.</span></span>

![Captura de pantalla de Consola de Redis](./media/stream-analytics-functions-redis/redis-console.png)

## <a name="next-steps"></a><span data-ttu-id="ea075-190">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ea075-190">Next steps</span></span>
<span data-ttu-id="ea075-191">Nos complace sobre cosas de hello nuevas funciones de Azure y análisis de transmisiones pueden hacer conjuntamente y esperamos que esto desbloquea nuevas posibilidades para usted.</span><span class="sxs-lookup"><span data-stu-id="ea075-191">We’re excited about hello new things Azure Functions and Stream analytics can do together, and we hope this unlocks new possibilities for you.</span></span> <span data-ttu-id="ea075-192">Si tiene comentarios sobre la acción que realizará a continuación, cree Hola libre toouse [UserVoice de Azure sitio](https://feedback.azure.com/forums/270577-stream-analytics).</span><span class="sxs-lookup"><span data-stu-id="ea075-192">If you have any feedback on what you want next, feel free toouse hello [Azure UserVoice site](https://feedback.azure.com/forums/270577-stream-analytics).</span></span>

<span data-ttu-id="ea075-193">Si es nuevo Microsoft Azure, le invitamos tootry alejar por registrarse para una [libre de la cuenta de prueba de Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ea075-193">If you are new Microsoft Azure, we invite you tootry it out by signing up for a [free Azure trial account](https://azure.microsoft.com/pricing/free-trial/).</span></span> <span data-ttu-id="ea075-194">Si está tooStream nuevo análisis, le invitamos demasiado[crear su primer trabajo de análisis de transmisiones](stream-analytics-create-a-job.md).</span><span class="sxs-lookup"><span data-stu-id="ea075-194">If you are new tooStream Analytics, then we invite you too[create your first Stream Analytics job](stream-analytics-create-a-job.md).</span></span>

<span data-ttu-id="ea075-195">Si necesita ayuda o tiene alguna pregunta, publíquela en [MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics) o en los foros de [Stackoverflow](http://stackoverflow.com/questions/tagged/azure-stream-analytics).</span><span class="sxs-lookup"><span data-stu-id="ea075-195">If you need any help or have questions, post on [MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics) or [Stackoverflow](http://stackoverflow.com/questions/tagged/azure-stream-analytics) forums.</span></span> 

<span data-ttu-id="ea075-196">También puede ver Hola recursos siguientes:</span><span class="sxs-lookup"><span data-stu-id="ea075-196">You can also see hello following resources:</span></span>

* [<span data-ttu-id="ea075-197">Azure Functions developer reference</span><span class="sxs-lookup"><span data-stu-id="ea075-197">Azure Functions developer reference</span></span>](../azure-functions/functions-reference.md)
* [<span data-ttu-id="ea075-198">Referencia para desarrolladores de C# de Funciones de Azure</span><span class="sxs-lookup"><span data-stu-id="ea075-198">Azure Functions C# developer reference</span></span>](../azure-functions/functions-reference-csharp.md)
* [<span data-ttu-id="ea075-199">Referencia para desarrolladores de F# de Azure Functions</span><span class="sxs-lookup"><span data-stu-id="ea075-199">Azure Functions F# developer reference</span></span>](../azure-functions/functions-reference-fsharp.md)
* [<span data-ttu-id="ea075-200">Referencia para desarrolladores de NodeJS de Funciones de Azure</span><span class="sxs-lookup"><span data-stu-id="ea075-200">Azure Functions NodeJS developer reference</span></span>](../azure-functions/functions-reference.md)
* [<span data-ttu-id="ea075-201">Enlaces y desencadenadores de las Funciones de azure</span><span class="sxs-lookup"><span data-stu-id="ea075-201">Azure Functions triggers and bindings</span></span>](../azure-functions/functions-triggers-bindings.md)
* [<span data-ttu-id="ea075-202">Cómo toomonitor Redis de Azure almacenan en caché</span><span class="sxs-lookup"><span data-stu-id="ea075-202">How toomonitor Azure Redis Cache</span></span>](../redis-cache/cache-how-to-monitor.md)

<span data-ttu-id="ea075-203">Siga toostay actualizada sobre todas las últimas noticias de Hola y otras características, [ @AzureStreaming ](https://twitter.com/AzureStreaming) en Twitter.</span><span class="sxs-lookup"><span data-stu-id="ea075-203">toostay up-to-date on all hello latest news and features, follow [@AzureStreaming](https://twitter.com/AzureStreaming) on Twitter.</span></span>

[fraud-detection]: stream-analytics-real-time-fraud-detection.md
[servicebus-getstarted]: ../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md
[use-rediscache]: ../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md
[functions-getstarted]: ../azure-functions/functions-create-first-azure-function.md
