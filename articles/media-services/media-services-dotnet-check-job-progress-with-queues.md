---
title: Uso de Azure Queue Storage para supervisar las notificaciones sobre trabajos de Media Services | Microsoft Docs
description: "Descubra cómo usar el almacenamiento en cola de Azure para supervisar las notificaciones sobre trabajos de Servicios multimedia. El ejemplo de código está escrito en C# y utiliza el SDK de Servicios multimedia para .NET."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: f535d0b5-f86c-465f-81c6-177f4f490987
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/14/2017
ms.author: juliako
ms.openlocfilehash: 5ee89d0ae4c3c56d164aff4e321ee99f015ba4fb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-queue-storage-to-monitor-media-services-job-notifications-with-net"></a><span data-ttu-id="d5592-104">Uso del almacenamiento en cola de Azure para supervisar las notificaciones sobre trabajos de Servicios multimedia con .NET</span><span class="sxs-lookup"><span data-stu-id="d5592-104">Use Azure Queue storage to monitor Media Services job notifications with .NET</span></span>
<span data-ttu-id="d5592-105">Al ejecutar trabajos de codificación, muchas veces se requiere una forma de hacer un seguimiento del progreso del trabajo.</span><span class="sxs-lookup"><span data-stu-id="d5592-105">When you run encoding jobs, you often require a way to track job progress.</span></span> <span data-ttu-id="d5592-106">Puede configurar Media Services para entregar notificaciones a [Azure Queue Storage](../storage/storage-dotnet-how-to-use-queues.md).</span><span class="sxs-lookup"><span data-stu-id="d5592-106">You can configure Media Services to deliver notifications to [Azure Queue storage](../storage/storage-dotnet-how-to-use-queues.md).</span></span> <span data-ttu-id="d5592-107">Puede supervisar el progreso del trabajo obteniendo notificaciones desde Queue Storage.</span><span class="sxs-lookup"><span data-stu-id="d5592-107">You can monitor job progress by getting notifications from the Queue storage.</span></span> 

<span data-ttu-id="d5592-108">Se puede obtener acceso a los mensajes entregados al almacenamiento de cola desde cualquier lugar del mundo.</span><span class="sxs-lookup"><span data-stu-id="d5592-108">Messages delivered to Queue storage can be accessed from anywhere in the world.</span></span> <span data-ttu-id="d5592-109">La arquitectura de mensajería de Queue Storage es fiable y altamente escalable.</span><span class="sxs-lookup"><span data-stu-id="d5592-109">The Queue storage messaging architecture is reliable and highly scalable.</span></span> <span data-ttu-id="d5592-110">El sondeo de mensajes en Queue Storage es preferible a otros métodos.</span><span class="sxs-lookup"><span data-stu-id="d5592-110">Polling Queue storage for messages is recommended over using other methods.</span></span>

<span data-ttu-id="d5592-111">Un escenario común para escuchar notificaciones de Media Services es si va a desarrollar un sistema de administración de contenido que necesita realizar alguna tarea adicional después de que se complete un trabajo de codificación (por ejemplo, para desencadenar el siguiente paso del flujo de trabajo o publicar contenido).</span><span class="sxs-lookup"><span data-stu-id="d5592-111">One common scenario for listening to Media Services notifications is if you are developing a content management system that needs to perform some additional task after an encoding job completes (for example, to trigger the next step in a workflow, or to publish content).</span></span>

<span data-ttu-id="d5592-112">En este tema se muestra cómo obtener mensajes de notificación de Queue Storage.</span><span class="sxs-lookup"><span data-stu-id="d5592-112">This topic shows how to get notification messages from Queue storage.</span></span>  

## <a name="considerations"></a><span data-ttu-id="d5592-113">Consideraciones</span><span class="sxs-lookup"><span data-stu-id="d5592-113">Considerations</span></span>
<span data-ttu-id="d5592-114">Tenga en cuenta lo siguiente al desarrollar aplicaciones de Media Services que usen Queue Storage:</span><span class="sxs-lookup"><span data-stu-id="d5592-114">Consider the following when developing Media Services applications that use Queue storage:</span></span>

* <span data-ttu-id="d5592-115">Queue Storage no ofrece ninguna garantía de entrega ordenada de tipo primero en entrar, primero en salir (FIFO).</span><span class="sxs-lookup"><span data-stu-id="d5592-115">Queue storage does not provide a guarantee of first-in-first-out (FIFO) ordered delivery.</span></span> <span data-ttu-id="d5592-116">Para obtener más información, consulte [Colas de Azure y Colas de Bus de servicio de Azure: comparación y diferencias](https://msdn.microsoft.com/library/azure/hh767287.aspx).</span><span class="sxs-lookup"><span data-stu-id="d5592-116">For more information, see [Azure Queues and Azure Service Bus Queues Compared and Contrasted](https://msdn.microsoft.com/library/azure/hh767287.aspx).</span></span>
* <span data-ttu-id="d5592-117">Queue Storage no es un servicio de inserción.</span><span class="sxs-lookup"><span data-stu-id="d5592-117">Queue storage is not a push service.</span></span> <span data-ttu-id="d5592-118">Tiene que sondear la cola.</span><span class="sxs-lookup"><span data-stu-id="d5592-118">You have to poll the queue.</span></span>
* <span data-ttu-id="d5592-119">Puede tener cualquier número de colas.</span><span class="sxs-lookup"><span data-stu-id="d5592-119">You can have any number of queues.</span></span> <span data-ttu-id="d5592-120">Para obtener más información, consulte la [API de REST del servicio de cola](https://docs.microsoft.com/rest/api/storageservices/Queue-Service-REST-API).</span><span class="sxs-lookup"><span data-stu-id="d5592-120">For more information, see [Queue Service REST API](https://docs.microsoft.com/rest/api/storageservices/Queue-Service-REST-API).</span></span>
* <span data-ttu-id="d5592-121">Queue Storage tiene algunas limitaciones y particularidades que deben tenerse en cuenta.</span><span class="sxs-lookup"><span data-stu-id="d5592-121">Queue storage has some limitations and specifics to be aware of.</span></span> <span data-ttu-id="d5592-122">Estas se describen en [Colas de Azure y de Azure Service Bus: comparación y diferencias](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-azure-and-service-bus-queues-compared-contrasted).</span><span class="sxs-lookup"><span data-stu-id="d5592-122">These are described in [Azure Queues and Azure Service Bus Queues Compared and Contrasted](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-azure-and-service-bus-queues-compared-contrasted).</span></span>

## <a name="net-code-example"></a><span data-ttu-id="d5592-123">Ejemplo de código .NET</span><span class="sxs-lookup"><span data-stu-id="d5592-123">.NET code example</span></span>

<span data-ttu-id="d5592-124">El ejemplo de código de esta sección realiza lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="d5592-124">The code example in this section does the following:</span></span>

1. <span data-ttu-id="d5592-125">Define la clase **EncodingJobMessage** que se asigna al formato de mensaje de notificación.</span><span class="sxs-lookup"><span data-stu-id="d5592-125">Defines the **EncodingJobMessage** class that maps to the notification message format.</span></span> <span data-ttu-id="d5592-126">El código deserializa los mensajes recibidos de la cola en objetos del tipo **EncodingJobMessage** .</span><span class="sxs-lookup"><span data-stu-id="d5592-126">The code deserializes messages received from the queue into objects of the **EncodingJobMessage** type.</span></span>
2. <span data-ttu-id="d5592-127">Carga la información de cuenta de almacenamiento y Servicios multimedia del archivo app.config.</span><span class="sxs-lookup"><span data-stu-id="d5592-127">Loads the Media Services and Storage account information from the app.config file.</span></span> <span data-ttu-id="d5592-128">El ejemplo de código usa esta información para crear los objetos **CloudMediaContext** y **CloudQueue**.</span><span class="sxs-lookup"><span data-stu-id="d5592-128">The code example uses this information to create the **CloudMediaContext** and **CloudQueue** objects.</span></span>
3. <span data-ttu-id="d5592-129">Crea la cola que va a recibir los mensajes de notificación sobre el trabajo de codificación.</span><span class="sxs-lookup"><span data-stu-id="d5592-129">Creates the queue that receives notification messages about the encoding job.</span></span>
4. <span data-ttu-id="d5592-130">Crea el extremo de notificación que se asigna a la cola.</span><span class="sxs-lookup"><span data-stu-id="d5592-130">Creates the notification end point that is mapped to the queue.</span></span>
5. <span data-ttu-id="d5592-131">Adjunta el extremo de notificación al trabajo y envía el trabajo de codificación.</span><span class="sxs-lookup"><span data-stu-id="d5592-131">Attaches the notification end point to the job and submits the encoding job.</span></span> <span data-ttu-id="d5592-132">Puede tener varios extremos de notificación adjuntos a un trabajo.</span><span class="sxs-lookup"><span data-stu-id="d5592-132">You can have multiple notification end points attached to a job.</span></span>
6. <span data-ttu-id="d5592-133">Pasa **NotificationJobState.FinalStatesOnly** al método **AddNew**</span><span class="sxs-lookup"><span data-stu-id="d5592-133">Passes **NotificationJobState.FinalStatesOnly** to the **AddNew** method.</span></span> <span data-ttu-id="d5592-134">(en este ejemplo, solo nos interesan los estados finales del procesamiento del trabajo).</span><span class="sxs-lookup"><span data-stu-id="d5592-134">(In this example, we are only interested in final states of the job processing.)</span></span>

        job.JobNotificationSubscriptions.AddNew(NotificationJobState.FinalStatesOnly, _notificationEndPoint);
7. <span data-ttu-id="d5592-135">Si se pasa **NotificationJobState.All**, se obtienen todas las notificaciones de cambio de estado siguientes: en cola, programado, procesando y finalizado.</span><span class="sxs-lookup"><span data-stu-id="d5592-135">If you pass **NotificationJobState.All**, you get all of the following state change notifications: queued, scheduled, processing, and finished.</span></span> <span data-ttu-id="d5592-136">Sin embargo, como se indicó anteriormente, Queue Storage no garantiza la entrega ordenada.</span><span class="sxs-lookup"><span data-stu-id="d5592-136">However, as noted earlier, Queue storage does not guarantee ordered delivery.</span></span> <span data-ttu-id="d5592-137">Para ordenar los mensajes, utilice la propiedad **Timestamp** (definida en el tipo **EncodingJobMessage** en el ejemplo siguiente).</span><span class="sxs-lookup"><span data-stu-id="d5592-137">To order messages, use the **Timestamp** property (defined on the **EncodingJobMessage** type in the example below).</span></span> <span data-ttu-id="d5592-138">Los mensajes duplicados son posibles.</span><span class="sxs-lookup"><span data-stu-id="d5592-138">Duplicate messages are possible.</span></span> <span data-ttu-id="d5592-139">Para comprobar si existen duplicados, utilice la **propiedad ETag** (definida en el tipo de **EncodingJobMessage**).</span><span class="sxs-lookup"><span data-stu-id="d5592-139">To check for duplicates, use the **ETag property** (defined on the **EncodingJobMessage** type).</span></span> <span data-ttu-id="d5592-140">También es posible que se omitan algunas notificaciones de cambio de estado.</span><span class="sxs-lookup"><span data-stu-id="d5592-140">It is also possible that some state change notifications get skipped.</span></span>
8. <span data-ttu-id="d5592-141">Espera a que el trabajo llegue al estado Finalizado comprobando la cola cada 10 segundos.</span><span class="sxs-lookup"><span data-stu-id="d5592-141">Waits for the job to get to the finished state by checking the queue every 10 seconds.</span></span> <span data-ttu-id="d5592-142">Elimina los mensajes una vez que se hayan procesado.</span><span class="sxs-lookup"><span data-stu-id="d5592-142">Deletes messages after they have been processed.</span></span>
9. <span data-ttu-id="d5592-143">Elimina la cola y el extremo de notificación.</span><span class="sxs-lookup"><span data-stu-id="d5592-143">Deletes the queue and the notification end point.</span></span>

> [!NOTE]
> <span data-ttu-id="d5592-144">La manera recomendada de supervisar el estado de un trabajo es escuchar los mensajes de notificación, tal como se muestra en el ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="d5592-144">The recommended way to monitor a job’s state is by listening to notification messages, as shown in the following example.</span></span>
>
> <span data-ttu-id="d5592-145">Como alternativa, puede comprobar el estado de un trabajo mediante el uso de la propiedad **IJob.State** .</span><span class="sxs-lookup"><span data-stu-id="d5592-145">Alternatively, you could check on a job’s state by using the **IJob.State** property.</span></span>  <span data-ttu-id="d5592-146">Es posible que llegue un mensaje de notificación sobre la finalización de un trabajo antes de que el estado en **IJob** se establezca en **Finalizado**.</span><span class="sxs-lookup"><span data-stu-id="d5592-146">A notification message about a job’s completion may arrive before the state on **IJob** is set to **Finished**.</span></span> <span data-ttu-id="d5592-147">La propiedad **IJob.State** refleja el estado exacto con un ligero retraso.</span><span class="sxs-lookup"><span data-stu-id="d5592-147">The **IJob.State**  property reflects the accurate state with a slight delay.</span></span>
>
>

### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="d5592-148">Creación y configuración de un proyecto de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d5592-148">Create and configure a Visual Studio project</span></span>

1. <span data-ttu-id="d5592-149">Configure el entorno de desarrollo y rellene el archivo app.config con la información de la conexión, como se describe en [Desarrollo de Media Services con .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="d5592-149">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 
2. <span data-ttu-id="d5592-150">Cree una carpeta nueva (la carpeta puede estar en cualquier lugar del disco duro) y copie el archivo .mp4 o .wmv que desea codificar para reproducirlo en streaming o descargarlo progresivamente.</span><span class="sxs-lookup"><span data-stu-id="d5592-150">Create a new folder (folder can be anywhere on your local drive) and copy an .mp4 file that you want to encode and stream or progressively download.</span></span> <span data-ttu-id="d5592-151">En este ejemplo, se usa la ruta de acceso "C:\Media".</span><span class="sxs-lookup"><span data-stu-id="d5592-151">In this example, the "C:\Media" path is used.</span></span>

### <a name="code"></a><span data-ttu-id="d5592-152">Código</span><span class="sxs-lookup"><span data-stu-id="d5592-152">Code</span></span>

```
using System;
using System.Linq;
using System.Configuration;
using System.IO;
using System.Threading;
using System.Collections.Generic;
using Microsoft.WindowsAzure.MediaServices.Client;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Queue;
using System.Runtime.Serialization.Json;

namespace JobNotification
{
    public class EncodingJobMessage
    {
        // MessageVersion is used for version control.
        public String MessageVersion { get; set; }

        // Type of the event. Valid values are
        // JobStateChange and NotificationEndpointRegistration.
        public String EventType { get; set; }

        // ETag is used to help the customer detect if
        // the message is a duplicate of another message previously sent.
        public String ETag { get; set; }

        // Time of occurrence of the event.
        public String TimeStamp { get; set; }

        // Collection of values specific to the event.

        // For the JobStateChange event the values are:
        //     JobId - Id of the Job that triggered the notification.
        //     NewState- The new state of the Job. Valid values are:
        //          Scheduled, Processing, Canceling, Cancelled, Error, Finished
        //     OldState- The old state of the Job. Valid values are:
        //          Scheduled, Processing, Canceling, Cancelled, Error, Finished

        // For the NotificationEndpointRegistration event the values are:
        //     NotificationEndpointId- Id of the NotificationEndpoint
        //          that triggered the notification.
        //     State- The state of the Endpoint.
        //          Valid values are: Registered and Unregistered.

        public IDictionary<string, object> Properties { get; set; }
    }

    class Program
    {

        // Read values from the App.config file.
        private static readonly string _AADTenantDomain =
            ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
            ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];
        private static readonly string _StorageConnectionString = 
            ConfigurationManager.AppSettings["StorageConnectionString"];

        private static CloudMediaContext _context = null;
        private static CloudQueue _queue = null;
        private static INotificationEndPoint _notificationEndPoint = null;

        private static readonly string _singleInputMp4Path =
            Path.GetFullPath(@"C:\Media\BigBuckBunny.mp4");

        static void Main(string[] args)
        {
            string endPointAddress = Guid.NewGuid().ToString();

            // Create the context.
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            // Create the queue that will be receiving the notification messages.
            _queue = CreateQueue(_StorageConnectionString, endPointAddress);

            // Create the notification point that is mapped to the queue.
            _notificationEndPoint =
                    _context.NotificationEndPoints.Create(
                    Guid.NewGuid().ToString(), NotificationEndPointType.AzureQueue, endPointAddress);


            if (_notificationEndPoint != null)
            {
                IJob job = SubmitEncodingJobWithNotificationEndPoint(_singleInputMp4Path);
                WaitForJobToReachedFinishedState(job.Id);
            }

            // Clean up.
            _queue.Delete();
            _notificationEndPoint.Delete();
        }


        static public CloudQueue CreateQueue(string storageAccountConnectionString, string endPointAddress)
        {
            CloudStorageAccount storageAccount = CloudStorageAccount.Parse(storageAccountConnectionString);

            // Create the queue client
            CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

            // Retrieve a reference to a queue
            CloudQueue queue = queueClient.GetQueueReference(endPointAddress);

            // Create the queue if it doesn't already exist
            queue.CreateIfNotExists();

            return queue;
        }


        public static IJob SubmitEncodingJobWithNotificationEndPoint(string inputMediaFilePath)
        {
            // Declare a new job.
            IJob job = _context.Jobs.Create("My MP4 to Smooth Streaming encoding job");

            //Create an encrypted asset and upload the mp4.
            IAsset asset = CreateAssetAndUploadSingleFile(AssetCreationOptions.StorageEncrypted,
                inputMediaFilePath);

            // Get a media processor reference, and pass to it the name of the
            // processor to use for the specific task.
            IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

            // Create a task with the conversion details, using a configuration file.
            ITask task = job.Tasks.AddNew("My encoding Task",
                processor,
                "Adaptive Streaming",
                Microsoft.WindowsAzure.MediaServices.Client.TaskOptions.None);

            // Specify the input asset to be encoded.
            task.InputAssets.Add(asset);

            // Add an output asset to contain the results of the job.
            task.OutputAssets.AddNew("Output asset",
                AssetCreationOptions.None);

            // Add a notification point to the job. You can add multiple notification points.  
            job.JobNotificationSubscriptions.AddNew(NotificationJobState.FinalStatesOnly,
                _notificationEndPoint);

            job.Submit();

            return job;
        }

        public static void WaitForJobToReachedFinishedState(string jobId)
        {
            int expectedState = (int)JobState.Finished;
            int timeOutInSeconds = 600;

            bool jobReachedExpectedState = false;
            DateTime startTime = DateTime.Now;
            int jobState = -1;

            while (!jobReachedExpectedState)
            {
                // Specify how often you want to get messages from the queue.
                Thread.Sleep(TimeSpan.FromSeconds(10));

                foreach (var message in _queue.GetMessages(10))
                {
                    using (Stream stream = new MemoryStream(message.AsBytes))
                    {
                        DataContractJsonSerializerSettings settings = new DataContractJsonSerializerSettings();
                        settings.UseSimpleDictionaryFormat = true;
                        DataContractJsonSerializer ser = new DataContractJsonSerializer(typeof(EncodingJobMessage), settings);
                        EncodingJobMessage encodingJobMsg = (EncodingJobMessage)ser.ReadObject(stream);

                        Console.WriteLine();

                        // Display the message information.
                        Console.WriteLine("EventType: {0}", encodingJobMsg.EventType);
                        Console.WriteLine("MessageVersion: {0}", encodingJobMsg.MessageVersion);
                        Console.WriteLine("ETag: {0}", encodingJobMsg.ETag);
                        Console.WriteLine("TimeStamp: {0}", encodingJobMsg.TimeStamp);
                        foreach (var property in encodingJobMsg.Properties)
                        {
                            Console.WriteLine("    {0}: {1}", property.Key, property.Value);
                        }

                        // We are only interested in messages
                        // where EventType is "JobStateChange".
                        if (encodingJobMsg.EventType == "JobStateChange")
                        {
                            string JobId = (String)encodingJobMsg.Properties.Where(j => j.Key == "JobId").FirstOrDefault().Value;
                            if (JobId == jobId)
                            {
                                string oldJobStateStr = (String)encodingJobMsg.Properties.
                                                            Where(j => j.Key == "OldState").FirstOrDefault().Value;
                                string newJobStateStr = (String)encodingJobMsg.Properties.
                                                            Where(j => j.Key == "NewState").FirstOrDefault().Value;

                                JobState oldJobState = (JobState)Enum.Parse(typeof(JobState), oldJobStateStr);
                                JobState newJobState = (JobState)Enum.Parse(typeof(JobState), newJobStateStr);

                                if (newJobState == (JobState)expectedState)
                                {
                                    Console.WriteLine("job with Id: {0} reached expected state: {1}",
                                        jobId, newJobState);
                                    jobReachedExpectedState = true;
                                    break;
                                }
                            }
                        }
                    }
                    // Delete the message after we've read it.
                    _queue.DeleteMessage(message);
                }

                // Wait until timeout
                TimeSpan timeDiff = DateTime.Now - startTime;
                bool timedOut = (timeDiff.TotalSeconds > timeOutInSeconds);
                if (timedOut)
                {
                    Console.WriteLine(@"Timeout for checking job notification messages,
                                        latest found state ='{0}', wait time = {1} secs",
                        jobState,
                        timeDiff.TotalSeconds);

                    throw new TimeoutException();
                }
            }
        }

        static private IAsset CreateAssetAndUploadSingleFile(AssetCreationOptions assetCreationOptions, string singleFilePath)
        {
            var asset = _context.Assets.Create("UploadSingleFile_" + DateTime.UtcNow.ToString(),
                assetCreationOptions);

            var fileName = Path.GetFileName(singleFilePath);

            var assetFile = asset.AssetFiles.Create(fileName);

            Console.WriteLine("Created assetFile {0}", assetFile.Name);
            Console.WriteLine("Upload {0}", assetFile.Name);

            assetFile.Upload(singleFilePath);
            Console.WriteLine("Done uploading of {0}", assetFile.Name);

            return asset;
        }

        static private IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
        {
            var processor = _context.MediaProcessors.Where(p => p.Name == mediaProcessorName).
                ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();

            if (processor == null)
                throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));

            return processor;
        }
    }
}
```
<span data-ttu-id="d5592-153">El ejemplo anterior genera el siguiente resultado.</span><span class="sxs-lookup"><span data-stu-id="d5592-153">The preceding example produced the following output.</span></span> <span data-ttu-id="d5592-154">Los valores variarán.</span><span class="sxs-lookup"><span data-stu-id="d5592-154">Your values will vary.</span></span>

    Created assetFile BigBuckBunny.mp4
    Upload BigBuckBunny.mp4
    Done uploading of BigBuckBunny.mp4

    EventType: NotificationEndPointRegistration
    MessageVersion: 1.0
    ETag: e0238957a9b25bdf3351a88e57978d6a81a84527fad03bc23861dbe28ab293f6
    TimeStamp: 2013-05-14T20:22:37
        NotificationEndPointId: nb:nepid:UUID:d6af9412-2488-45b2-ba1f-6e0ade6dbc27
        State: Registered
        Name: dde957b2-006e-41f2-9869-a978870ac620
        Created: 2013-05-14T20:22:35

    EventType: JobStateChange
    MessageVersion: 1.0
    ETag: 4e381f37c2d844bde06ace650310284d6928b1e50101d82d1b56220cfcb6076c
    TimeStamp: 2013-05-14T20:24:40
        JobId: nb:jid:UUID:526291de-f166-be47-b62a-11ffe6d4be54
        JobName: My MP4 to Smooth Streaming encoding job
        NewState: Finished
        OldState: Processing
        AccountName: westeuropewamsaccount
    job with Id: nb:jid:UUID:526291de-f166-be47-b62a-11ffe6d4be54 reached expected
    State: Finished


## <a name="next-step"></a><span data-ttu-id="d5592-155">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="d5592-155">Next step</span></span>
<span data-ttu-id="d5592-156">Consulte las rutas de aprendizaje de Servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="d5592-156">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="d5592-157">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="d5592-157">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
