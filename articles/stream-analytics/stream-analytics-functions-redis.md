---
title: Procesamiento en tiempo real de Stream Analytics para Azure Functions | Microsoft Docs
description: "Obtenga información sobre cómo usar una función de Azure conectada a una cola del Bus de servicio para rellenar una instancia de Caché en Redis de Azure desde la salida de un trabajo de Análisis de transmisiones."
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
ms.openlocfilehash: ad14cc858ff513573e2718a26a9ab5c524e1adc6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-store-data-from-azure-stream-analytics-in-an-azure-redis-cache-using-azure-functions"></a><span data-ttu-id="252cc-104">Almacenamiento de datos desde Análisis de transmisiones de Azure en Caché en Redis de Azure con Funciones de Azure</span><span class="sxs-lookup"><span data-stu-id="252cc-104">How to store data from Azure Stream Analytics in an Azure Redis Cache using Azure Functions</span></span>
<span data-ttu-id="252cc-105">Análisis de transmisiones de Azure permite desarrollar e implementar rápidamente soluciones de bajo costo para obtener información en tiempo real de dispositivos, sensores, infraestructura y aplicaciones o cualquier transmisión de datos.</span><span class="sxs-lookup"><span data-stu-id="252cc-105">Azure Stream Analytics lets you rapidly develop and deploy low-cost solutions to gain real-time insights from devices, sensors, infrastructure, and applications, or any stream of data.</span></span> <span data-ttu-id="252cc-106">Permite varios casos de uso, como la administración y supervisión en tiempo real, comando y control, detección de fraudes, automóviles conectados y mucho más.</span><span class="sxs-lookup"><span data-stu-id="252cc-106">It enables various use cases such as real-time management and monitoring, command and control, fraud detection, connected cars and many more.</span></span> <span data-ttu-id="252cc-107">En muchos de estos escenarios, puede que desee almacenar datos generados por Análisis de transmisiones de Azure en un almacén de datos distribuidos, como Caché en Redis de Azure.</span><span class="sxs-lookup"><span data-stu-id="252cc-107">In many such scenarios, you may want to store data outputted by Azure Stream Analytics into a distributed data store such as an Azure Redis cache.</span></span>

<span data-ttu-id="252cc-108">Imaginemos que forma parte de una empresa de telecomunicaciones.</span><span class="sxs-lookup"><span data-stu-id="252cc-108">Suppose you are part of a telecommunications company.</span></span> <span data-ttu-id="252cc-109">Intenta detectar un fraude de SIM en el que varias llamadas se originan en la misma identidad y al mismo tiempo, pero en ubicaciones geográficas distintas.</span><span class="sxs-lookup"><span data-stu-id="252cc-109">You are trying to detect SIM fraud where multiple calls coming from the same identity, at the same time, but in different geographically locations.</span></span> <span data-ttu-id="252cc-110">Su tarea es almacenar todas las llamadas telefónicas potencialmente fraudulentas en una instancia de Caché en Redis de Azure.</span><span class="sxs-lookup"><span data-stu-id="252cc-110">You are tasked with storing all the potential fraudulent phone calls in an Azure Redis cache.</span></span> <span data-ttu-id="252cc-111">En este blog, le brindamos la orientación que necesita para poder completar fácilmente la tarea.</span><span class="sxs-lookup"><span data-stu-id="252cc-111">In this blog, we provide guidance on how you can easily complete your task.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="252cc-112">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="252cc-112">Prerequisites</span></span>
<span data-ttu-id="252cc-113">Completar el tutorial [Detección de fraudes en tiempo real][fraud-detection] para ASA</span><span class="sxs-lookup"><span data-stu-id="252cc-113">Complete the [Real-time Fraud Detection][fraud-detection] walk-through for ASA</span></span>

## <a name="architecture-overview"></a><span data-ttu-id="252cc-114">Introducción a la arquitectura</span><span class="sxs-lookup"><span data-stu-id="252cc-114">Architecture Overview</span></span>
![Captura de pantalla de arquitectura](./media/stream-analytics-functions-redis/architecture-overview.png)

<span data-ttu-id="252cc-116">Tal como se muestra en la ilustración anterior, Análisis de transmisiones permite consultar la transmisión de datos de entrada y enviarlos a una salida.</span><span class="sxs-lookup"><span data-stu-id="252cc-116">As shown in the preceding figure, Stream Analytics allows streaming input data to be queried and sent to an output.</span></span> <span data-ttu-id="252cc-117">Según el resultado, Funciones de Azure puede desencadenar algún tipo de evento.</span><span class="sxs-lookup"><span data-stu-id="252cc-117">Based on the output, Azure Functions can then trigger some type of event.</span></span> 

<span data-ttu-id="252cc-118">En este blog, nos centramos en la parte de esta canalización que corresponde a Funciones de Azure, o más específicamente, en cómo desencadenar un evento que almacena datos fraudulentos en la caché.</span><span class="sxs-lookup"><span data-stu-id="252cc-118">In this blog, we focus on the Azure Functions part of this pipeline, or more specifically the triggering of an event that stores fraudulent data into the cache.</span></span>
<span data-ttu-id="252cc-119">Una vez que complete el tutorial [Detección de fraudes en tiempo real][fraud-detection], tiene una entrada (un centro de eventos), una consulta y una salida (almacenamiento de blobs) ya configuradas y en ejecución.</span><span class="sxs-lookup"><span data-stu-id="252cc-119">After completing the [Real-time Fraud Detection][fraud-detection] tutorial, you have an input (an event hub), a query, and an output (blob storage) already configured and running.</span></span> <span data-ttu-id="252cc-120">En este blog, cambiamos la salida para usar en su lugar una cola del Bus de servicio.</span><span class="sxs-lookup"><span data-stu-id="252cc-120">In this blog, we change the output to use a Service Bus Queue instead.</span></span> <span data-ttu-id="252cc-121">Luego, conectamos una Función de Azure con esta cola.</span><span class="sxs-lookup"><span data-stu-id="252cc-121">After that, we connect an Azure Function to this queue.</span></span> 

## <a name="create-and-connect-a-service-bus-queue-output"></a><span data-ttu-id="252cc-122">Creación y conexión de una salida de cola del Bus de servicio</span><span class="sxs-lookup"><span data-stu-id="252cc-122">Create and connect a Service Bus Queue output</span></span>
<span data-ttu-id="252cc-123">Para crear una cola de Service Bus, siga los pasos 1 y 2 de la sección .NET que aparece en [Introducción a las colas de Service Bus][servicebus-getstarted].</span><span class="sxs-lookup"><span data-stu-id="252cc-123">To create a Service Bus Queue, follow steps 1 and 2 of the .NET section in [Get Started with Service Bus Queues][servicebus-getstarted].</span></span>
<span data-ttu-id="252cc-124">Ahora vamos a conectar la cola con el trabajo de Análisis de transmisiones que se creó en el anterior tutorial de detección de fraudes.</span><span class="sxs-lookup"><span data-stu-id="252cc-124">Now let's connect the queue to the Stream Analytics job that was created in the earlier fraud detection walk-through.</span></span>

1. <span data-ttu-id="252cc-125">En Azure Portal, vaya a la hoja **Salidas** del trabajo y seleccione **Agregar** en la parte superior de la página.</span><span class="sxs-lookup"><span data-stu-id="252cc-125">In the Azure portal, go to the **Outputs** blade of your job and select **Add** at the top of the page.</span></span>
   
    ![Agregar salidas](./media/stream-analytics-functions-redis/adding-outputs.png)
2. <span data-ttu-id="252cc-127">Elija **Cola de Service Bus** en **Receptor** y siga las instrucciones que aparecen en la pantalla.</span><span class="sxs-lookup"><span data-stu-id="252cc-127">Choose **Service Bus Queue** as the **Sink** and follow the instructions on the screen.</span></span> <span data-ttu-id="252cc-128">Asegúrese de elegir el espacio de nombres de la cola de Service Bus que creó en [Introducción a las colas de Service Bus][servicebus-getstarted].</span><span class="sxs-lookup"><span data-stu-id="252cc-128">Be sure to choose the namespace of the Service Bus Queue you created in [Get Started with Service Bus Queues][servicebus-getstarted].</span></span> <span data-ttu-id="252cc-129">Haga clic en el botón "Correcto" cuando termine.</span><span class="sxs-lookup"><span data-stu-id="252cc-129">Click the "right" button when you are finished.</span></span>
3. <span data-ttu-id="252cc-130">Especifique los siguientes valores:</span><span class="sxs-lookup"><span data-stu-id="252cc-130">Specify the following values:</span></span>
   
   * <span data-ttu-id="252cc-131">**Formato del serializador de eventos**: JSON</span><span class="sxs-lookup"><span data-stu-id="252cc-131">**Event Serializer Format**: JSON</span></span>
   * <span data-ttu-id="252cc-132">**Codificación**: UTF8</span><span class="sxs-lookup"><span data-stu-id="252cc-132">**Encoding**: UTF8</span></span>
   * <span data-ttu-id="252cc-133">**FORMATO**: separado por líneas</span><span class="sxs-lookup"><span data-stu-id="252cc-133">**FORMAT**: Line separated</span></span>
4. <span data-ttu-id="252cc-134">Haga clic en el botón **Crear** para agregar este origen y comprobar que Análisis de transmisiones puede conectarse correctamente a la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="252cc-134">Click the **Create** button to add this source and to verify that Stream Analytics can successfully connect to the storage account.</span></span>
5. <span data-ttu-id="252cc-135">En la pestaña **Consulta** , reemplace la consulta actual por la siguiente.</span><span class="sxs-lookup"><span data-stu-id="252cc-135">In the **Query** tab, replace the current query with the following.</span></span> <span data-ttu-id="252cc-136">Reemplace *[EL NOMBRE DE SERVICE BUS] * por el nombre de la salida que creó en el paso 3.</span><span class="sxs-lookup"><span data-stu-id="252cc-136">Replace *[YOUR SERVICE BUS NAME] * with the output name you created in step 3.</span></span> 
   
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

## <a name="create-an-azure-redis-cache"></a><span data-ttu-id="252cc-137">Creación de una instancia de Caché en Redis de Azure</span><span class="sxs-lookup"><span data-stu-id="252cc-137">Create an Azure Redis Cache</span></span>
<span data-ttu-id="252cc-138">Para crear una instancia de Caché en Redis de Azure, siga la sección .NET de [Uso de Caché en Redis de Azure][use-rediscache] hasta la sección llamada ***Configuración de los clientes de caché***.</span><span class="sxs-lookup"><span data-stu-id="252cc-138">Create an Azure Redis cache by following the .NET section in [How to Use Azure Redis Cache][use-rediscache] until the section called ***Configure the cache clients***.</span></span>
<span data-ttu-id="252cc-139">Una vez que finalice, tendrá una nueva instancia de Caché en Redis.</span><span class="sxs-lookup"><span data-stu-id="252cc-139">Once complete, you have a new Redis Cache.</span></span> <span data-ttu-id="252cc-140">En **Toda la configuración**, seleccione **Claves de acceso** y anote el contenido de ***Cadena de conexión principal***.</span><span class="sxs-lookup"><span data-stu-id="252cc-140">Under **All settings**, select **Access keys** and note down the ***Primary connection string***.</span></span>

![Captura de pantalla de arquitectura](./media/stream-analytics-functions-redis/redis-cache-keys.png)

## <a name="create-an-azure-function"></a><span data-ttu-id="252cc-142">Creación de una Función de Azure</span><span class="sxs-lookup"><span data-stu-id="252cc-142">Create an Azure Function</span></span>
<span data-ttu-id="252cc-143">Siga el tutorial [Creación de su primera función de Azure][functions-getstarted] para comenzar a trabajar con Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="252cc-143">Follow [Create your first Azure Function][functions-getstarted] tutorial to get started with Azure Functions.</span></span> <span data-ttu-id="252cc-144">Si ya cuenta con una función de Azure que desea usar, omita este paso y vaya a [Escritura en Caché en Redis](#Writing-to-Redis-Cache)</span><span class="sxs-lookup"><span data-stu-id="252cc-144">If you already have an Azure function you would like to use, then skip ahead to [Writing to Redis Cache](#Writing-to-Redis-Cache)</span></span>

1. <span data-ttu-id="252cc-145">En el portal, seleccione App Services en el menú de navegación de la izquierda y haga clic en el nombre de la Function App de Azure para ir al sitio web de esta.</span><span class="sxs-lookup"><span data-stu-id="252cc-145">In the portal, select App Services from the left-hand navigation, then click your Azure function app name to get to the Function's app website.</span></span>
    <span data-ttu-id="252cc-146">![Captura de pantalla de lista de funciones de App Services](./media/stream-analytics-functions-redis/app-services-function-list.png)</span><span class="sxs-lookup"><span data-stu-id="252cc-146">![Screenshot of app services function list](./media/stream-analytics-functions-redis/app-services-function-list.png)</span></span>
2. <span data-ttu-id="252cc-147">Haga clic en **Nueva función > ServiceBusQueueTrigger – C#**.</span><span class="sxs-lookup"><span data-stu-id="252cc-147">Click **New Function > ServiceBusQueueTrigger – C#**.</span></span> <span data-ttu-id="252cc-148">Siga estas instrucciones en los siguientes campos:</span><span class="sxs-lookup"><span data-stu-id="252cc-148">For the following fields, follow these instructions:</span></span>
   
   * <span data-ttu-id="252cc-149">**Nombre de cola**: el mismo nombre que escribió cuando creó la cola en [Introducción a las colas de Service Bus][servicebus-getstarted] (no el nombre del bus de servicio).</span><span class="sxs-lookup"><span data-stu-id="252cc-149">**Queue name**: The same name as the name you entered when you created the queue in [Get Started with Service Bus Queues][servicebus-getstarted] (not the name of the service bus).</span></span> <span data-ttu-id="252cc-150">Asegúrese de usar la cola que está conectada con la salida de Análisis de transmisiones.</span><span class="sxs-lookup"><span data-stu-id="252cc-150">Make sure you use the queue that is connected to the Stream Analytics output.</span></span>
   * <span data-ttu-id="252cc-151">**Conexión de Service Bus**: seleccione **Agregar una cadena de conexión**.</span><span class="sxs-lookup"><span data-stu-id="252cc-151">**Service Bus connection**: Select **Add a connection string**.</span></span> <span data-ttu-id="252cc-152">Para encontrar la cadena de conexión, vaya al portal clásico, seleccione **Service Bus**, el bus de servicio que creó y luego **INFORMACIÓN DE CONEXIÓN** en la parte inferior de la pantalla.</span><span class="sxs-lookup"><span data-stu-id="252cc-152">To find the connection string, go to the classic portal, select **Service Bus**, the service bus you created, and **CONNECTION INFORMATION** at the bottom of the screen.</span></span> <span data-ttu-id="252cc-153">Asegúrese de estar en la pantalla principal de esta página.</span><span class="sxs-lookup"><span data-stu-id="252cc-153">Make sure you are on the main screen on this page.</span></span> <span data-ttu-id="252cc-154">Copie y pegue la cadena de conexión.</span><span class="sxs-lookup"><span data-stu-id="252cc-154">Copy and paste the connection string.</span></span> <span data-ttu-id="252cc-155">Puede escribir cualquier nombre de conexión.</span><span class="sxs-lookup"><span data-stu-id="252cc-155">Feel free to enter any connection name.</span></span>
     
       ![Captura de pantalla de conexión del Bus de servicio](./media/stream-analytics-functions-redis/servicebus-connection.png)
   * <span data-ttu-id="252cc-157">**AccessRights**: elija **Administrar**.</span><span class="sxs-lookup"><span data-stu-id="252cc-157">**AccessRights**: Choose **Manage**</span></span>
3. <span data-ttu-id="252cc-158">Haga clic en **Crear**</span><span class="sxs-lookup"><span data-stu-id="252cc-158">Click **Create**</span></span>

## <a name="writing-to-redis-cache"></a><span data-ttu-id="252cc-159">Escritura en Caché en Redis</span><span class="sxs-lookup"><span data-stu-id="252cc-159">Writing to Redis Cache</span></span>
<span data-ttu-id="252cc-160">Creamos una función de Azure que lee desde una cola del Bus de servicio.</span><span class="sxs-lookup"><span data-stu-id="252cc-160">We have now created an Azure Function that reads from a Service Bus Queue.</span></span> <span data-ttu-id="252cc-161">Todo lo que queda por hacer es usar la función para escribir estos datos en Caché en Redis.</span><span class="sxs-lookup"><span data-stu-id="252cc-161">All that is left to do is use our Function to write this data to the Redis Cache.</span></span> 

1. <span data-ttu-id="252cc-162">Seleccione la función **ServiceBusQueueTrigger** que acaba de crear y haga clic en **Configuración de Function App** en la esquina superior derecha.</span><span class="sxs-lookup"><span data-stu-id="252cc-162">Select your newly created **ServiceBusQueueTrigger**, and click **Function app settings** on the top right corner.</span></span> <span data-ttu-id="252cc-163">Seleccione **Ir a Configuración de App Service > Configuración > Configuración de la aplicación**.</span><span class="sxs-lookup"><span data-stu-id="252cc-163">Select **Go to App Service Settings > Settings > Application settings**</span></span>
2. <span data-ttu-id="252cc-164">En la sección Cadenas de conexión, cree un nombre en la sección **Nombre** .</span><span class="sxs-lookup"><span data-stu-id="252cc-164">In the Connection strings section, create a name in the **Name** section.</span></span> <span data-ttu-id="252cc-165">Pegue la cadena de conexión principal que encontró en el paso **Creación de una instancia de Redis Cache** en la sección **Valor**.</span><span class="sxs-lookup"><span data-stu-id="252cc-165">Paste the primary connection string you found in the **Create a Redis Cache** step into the **Value** section.</span></span> <span data-ttu-id="252cc-166">Seleccione **Personalizado** donde aparece **SQL Database**.</span><span class="sxs-lookup"><span data-stu-id="252cc-166">Select **Custom** where it says **SQL Database**.</span></span>
3. <span data-ttu-id="252cc-167">Haga clic en **Guardar** en la parte superior.</span><span class="sxs-lookup"><span data-stu-id="252cc-167">Click **Save** at the top.</span></span>
   
    ![Captura de pantalla de conexión del Bus de servicio](./media/stream-analytics-functions-redis/function-connection-string.png)
4. <span data-ttu-id="252cc-169">Vuelva a Configuración de App Service y seleccione **Herramientas > Editor de App Service (versión preliminar) > Activar > Ir**.</span><span class="sxs-lookup"><span data-stu-id="252cc-169">Now go back to the App Service Settings and select **Tools > App Service Editor (Preview) > On > Go**.</span></span>
   
    ![Captura de pantalla de conexión del Bus de servicio](./media/stream-analytics-functions-redis/app-service-editor.png)
5. <span data-ttu-id="252cc-171">En un editor de su preferencia, cree un archivo JSON llamado **project.json** que incluya lo siguiente y guárdelo en el disco local.</span><span class="sxs-lookup"><span data-stu-id="252cc-171">In an editor of your choice, create a JSON file named **project.json** with the following and save it to your local disk.</span></span>
   
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
6. <span data-ttu-id="252cc-172">Cargue este archivo en el directorio raíz de la función (no en WWWROOT).</span><span class="sxs-lookup"><span data-stu-id="252cc-172">Upload this file into the root directory of your function (not WWWROOT).</span></span> <span data-ttu-id="252cc-173">Debería aparecer automáticamente un archivo llamado **project.lock.json** ,con la confirmación de que se importaron los paquetes NuGet "StackExchange.Redis" y "Newtonsoft.Json".</span><span class="sxs-lookup"><span data-stu-id="252cc-173">You should see a file named **project.lock.json** automatically appear, confirming that the Nuget packages “StackExchange.Redis” and “Newtonsoft.Json” have been imported.</span></span>
7. <span data-ttu-id="252cc-174">En el archivo **run.csx** , reemplace el código generado previamente por el código siguiente.</span><span class="sxs-lookup"><span data-stu-id="252cc-174">In the **run.csx** file, replace the pre-generated code with the following code.</span></span> <span data-ttu-id="252cc-175">En la función lazyConnection, reemplace "CONN NAME" por el nombre que creó en el paso 2 de **Almacenamiento de datos en Caché en Redis**.</span><span class="sxs-lookup"><span data-stu-id="252cc-175">In the lazyConnection function, replace “CONN NAME” with the name you created in step 2 of **Store data into the Redis cache**.</span></span>

````

    using System;
    using System.Threading.Tasks;
    using StackExchange.Redis;
    using Newtonsoft.Json;
    using System.Configuration;

    public static void Run(string myQueueItem, TraceWriter log)
    {
        log.Info($"Function processed message: {myQueueItem}");

        // Connection refers to a property that returns a ConnectionMultiplexer
        IDatabase db = Connection.GetDatabase();
        log.Info($"Created database {db}");

        // Parse JSON and extract the time
        var message = JsonConvert.DeserializeObject<dynamic>(myQueueItem);
        string time = message.time;
        string callingnum1 = message.callingnum1;

        // Perform cache operations using the cache object...
        // Simple put of integral data types into the cache
        string key = time + " - " + callingnum1;
        db.StringSet(key, myQueueItem);
        log.Info($"Object put in database. Key is {key} and value is {myQueueItem}");

        // Simple get of data types from the cache
        string value = db.StringGet(key);
        log.Info($"Database got: {value}"); 
    }

    // Connect to the Service Bus
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

## <a name="start-the-stream-analytics-job"></a><span data-ttu-id="252cc-176">Inicio del trabajo de Análisis de transmisiones</span><span class="sxs-lookup"><span data-stu-id="252cc-176">Start the Stream Analytics job</span></span>
1. <span data-ttu-id="252cc-177">Inicie la aplicación telcodatagen.exe.</span><span class="sxs-lookup"><span data-stu-id="252cc-177">Start the telcodatagen.exe application.</span></span> <span data-ttu-id="252cc-178">Se usa de esta manera: ````telcodatagen.exe [#NumCDRsPerHour] [SIM Card Fraud Probability] [#DurationHours]````</span><span class="sxs-lookup"><span data-stu-id="252cc-178">The usage is as follows: ````telcodatagen.exe [#NumCDRsPerHour] [SIM Card Fraud Probability] [#DurationHours]````</span></span>
2. <span data-ttu-id="252cc-179">En la hoja del trabajo de Análisis de transmisiones del portal, haga clic en **Iniciar** en la parte superior de la página.</span><span class="sxs-lookup"><span data-stu-id="252cc-179">From the Stream Analytics Job blade in the portal, click **Start** at the top of the page.</span></span>
   
    ![Captura de pantalla de Iniciar trabajo](./media/stream-analytics-functions-redis/starting-job.png)
3. <span data-ttu-id="252cc-181">En la hoja **Iniciar trabajo** que aparece, seleccione **Ahora** y haga clic en el botón **Iniciar** en la parte inferior de la pantalla.</span><span class="sxs-lookup"><span data-stu-id="252cc-181">In the **Start job** blade that appears, select **Now** and then click the **Start** button at the bottom of the screen.</span></span> <span data-ttu-id="252cc-182">El estado del trabajo cambia a Iniciando y, luego de un tiempo, cambia a En ejecución.</span><span class="sxs-lookup"><span data-stu-id="252cc-182">The job status changes to Starting and after some time changes to Running.</span></span>
   
    ![Captura de pantalla de selección de tiempo de Iniciar trabajo](./media/stream-analytics-functions-redis/start-job-time.png)

## <a name="run-solution-and-check-results"></a><span data-ttu-id="252cc-184">Ejecución de la solución y comprobación de los resultados</span><span class="sxs-lookup"><span data-stu-id="252cc-184">Run solution and check results</span></span>
<span data-ttu-id="252cc-185">Vuelva a la página **ServiceBusQueueTrigger** , donde debería ver instrucciones de registro.</span><span class="sxs-lookup"><span data-stu-id="252cc-185">Going back to your **ServiceBusQueueTrigger** page, you should now see log statements.</span></span> <span data-ttu-id="252cc-186">Estos registros muestran que obtuvo algún elemento de la cola del Bus de servicio, lo puso en la base de datos y lo recuperó con el tiempo como clave.</span><span class="sxs-lookup"><span data-stu-id="252cc-186">These logs show that you got something from the Service Bus Queue, put it into the database, and fetched it out using the time as the key!</span></span>

<span data-ttu-id="252cc-187">Para comprobar que los datos están en la Caché en Redis, vaya a la página de Caché en Redis del portal nuevo (como aparece en el paso anterior, [Creación de una instancia de Caché en Redis de Azure](#Create-an-Azure-Redis-Cache) ) y seleccione Consola.</span><span class="sxs-lookup"><span data-stu-id="252cc-187">To verify that your data is in your Redis cache, go to your Redis cache page in the new portal (as shown in the preceding [Create an Azure Redis Cache](#Create-an-Azure-Redis-Cache) step) and select Console.</span></span>

<span data-ttu-id="252cc-188">Ahora puede escribir comandos de Redis para confirmar que los datos están, de hecho, en la caché.</span><span class="sxs-lookup"><span data-stu-id="252cc-188">Now you can write Redis commands to confirm that data is in fact in the cache.</span></span>

![Captura de pantalla de Consola de Redis](./media/stream-analytics-functions-redis/redis-console.png)

## <a name="next-steps"></a><span data-ttu-id="252cc-190">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="252cc-190">Next steps</span></span>
<span data-ttu-id="252cc-191">Estamos entusiasmados con las nuevas acciones que Análisis de transmisiones y Funciones de Azure pueden hacer en conjunto. Además, esperamos que esta unión le brinde nuevas posibilidades.</span><span class="sxs-lookup"><span data-stu-id="252cc-191">We’re excited about the new things Azure Functions and Stream analytics can do together, and we hope this unlocks new possibilities for you.</span></span> <span data-ttu-id="252cc-192">Si tiene comentarios sobre lo que espera a continuación, no dude en usar el [sitio de Azure UserVoice](https://feedback.azure.com/forums/270577-stream-analytics).</span><span class="sxs-lookup"><span data-stu-id="252cc-192">If you have any feedback on what you want next, feel free to use the [Azure UserVoice site](https://feedback.azure.com/forums/270577-stream-analytics).</span></span>

<span data-ttu-id="252cc-193">Si es primera vez que usa Microsoft Azure, le invitamos a probarlo y registrarse para obtener una [cuenta de evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="252cc-193">If you are new Microsoft Azure, we invite you to try it out by signing up for a [free Azure trial account](https://azure.microsoft.com/pricing/free-trial/).</span></span> <span data-ttu-id="252cc-194">Si es primera vez que usa Análisis de transmisiones, le invitamos a [crear su primer trabajo de Análisis de transmisiones](stream-analytics-create-a-job.md).</span><span class="sxs-lookup"><span data-stu-id="252cc-194">If you are new to Stream Analytics, then we invite you to [create your first Stream Analytics job](stream-analytics-create-a-job.md).</span></span>

<span data-ttu-id="252cc-195">Si necesita ayuda o tiene alguna pregunta, publíquela en [MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics) o en los foros de [Stackoverflow](http://stackoverflow.com/questions/tagged/azure-stream-analytics).</span><span class="sxs-lookup"><span data-stu-id="252cc-195">If you need any help or have questions, post on [MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics) or [Stackoverflow](http://stackoverflow.com/questions/tagged/azure-stream-analytics) forums.</span></span> 

<span data-ttu-id="252cc-196">También puede consultar los siguientes recursos:</span><span class="sxs-lookup"><span data-stu-id="252cc-196">You can also see the following resources:</span></span>

* [<span data-ttu-id="252cc-197">Referencia para desarrolladores de Funciones de Azure</span><span class="sxs-lookup"><span data-stu-id="252cc-197">Azure Functions developer reference</span></span>](../azure-functions/functions-reference.md)
* [<span data-ttu-id="252cc-198">Referencia para desarrolladores de C# de Funciones de Azure</span><span class="sxs-lookup"><span data-stu-id="252cc-198">Azure Functions C# developer reference</span></span>](../azure-functions/functions-reference-csharp.md)
* [<span data-ttu-id="252cc-199">Referencia para desarrolladores de F# de Azure Functions</span><span class="sxs-lookup"><span data-stu-id="252cc-199">Azure Functions F# developer reference</span></span>](../azure-functions/functions-reference-fsharp.md)
* [<span data-ttu-id="252cc-200">Referencia para desarrolladores de NodeJS de Funciones de Azure</span><span class="sxs-lookup"><span data-stu-id="252cc-200">Azure Functions NodeJS developer reference</span></span>](../azure-functions/functions-reference.md)
* [<span data-ttu-id="252cc-201">Enlaces y desencadenadores de las Funciones de azure</span><span class="sxs-lookup"><span data-stu-id="252cc-201">Azure Functions triggers and bindings</span></span>](../azure-functions/functions-triggers-bindings.md)
* [<span data-ttu-id="252cc-202">Supervisión de Caché en Redis de Azure</span><span class="sxs-lookup"><span data-stu-id="252cc-202">How to monitor Azure Redis Cache</span></span>](../redis-cache/cache-how-to-monitor.md)

<span data-ttu-id="252cc-203">Para mantenerse al día con las noticias y características más recientes, siga la cuenta [@AzureStreaming](https://twitter.com/AzureStreaming) en Twitter.</span><span class="sxs-lookup"><span data-stu-id="252cc-203">To stay up-to-date on all the latest news and features, follow [@AzureStreaming](https://twitter.com/AzureStreaming) on Twitter.</span></span>

[fraud-detection]: stream-analytics-real-time-fraud-detection.md
[servicebus-getstarted]: ../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md
[use-rediscache]: ../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md
[functions-getstarted]: ../azure-functions/functions-create-first-azure-function.md
