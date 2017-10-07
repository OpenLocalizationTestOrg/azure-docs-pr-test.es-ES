---
title: notificaciones de trabajo de servicios multimedia toomonitor almacenamiento de cola de Azure aaaUse con. NET | Documentos de Microsoft
description: "Obtenga información acerca de cómo las notificaciones del trabajo toomonitor de almacenamiento de cola de Azure toouse servicios multimedia. ejemplo de código de Hello está escrito en C# y usa Hola SDK de servicios multimedia para. NET."
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
ms.openlocfilehash: e4068621ada00d763133dc0d01cfc666b53f8b1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-queue-storage-toomonitor-media-services-job-notifications-with-net"></a>Usar notificaciones de trabajos de servicios multimedia de toomonitor de almacenamiento de cola de Azure con .NET
Al ejecutar trabajos de codificación, a menudo requieren un progreso del trabajo de manera tootrack. Puede configurar las notificaciones de servicios multimedia toodeliver demasiado[almacenamiento de cola de Azure](../storage/storage-dotnet-how-to-use-queues.md). Puede supervisar el progreso del trabajo al obtener las notificaciones de hello almacenamiento en la cola. 

Mensajes entregados tooQueue almacenamiento pueden tener acceso desde cualquier lugar Hola a todos. Hola arquitectura de mensajería de almacenamiento de cola es altamente escalable y confiable. El sondeo de mensajes en Queue Storage es preferible a otros métodos.

Un escenario habitual para escuchar las notificaciones de servicios de tooMedia es si va a desarrollar un sistema de administración de contenido que debe tooperform alguna tarea adicional después de un trabajo de codificación completa (por ejemplo, el paso siguiente de hello tootrigger en un flujo de trabajo o toopublish contenido).

Este tema muestra cómo los mensajes de notificación tooget del almacenamiento de cola.  

## <a name="considerations"></a>Consideraciones
Tenga en cuenta los siguiente de hello al desarrollar aplicaciones de servicios multimedia que utilizan el almacenamiento de cola:

* Queue Storage no ofrece ninguna garantía de entrega ordenada de tipo primero en entrar, primero en salir (FIFO). Para obtener más información, consulte [Colas de Azure y Colas de Bus de servicio de Azure: comparación y diferencias](https://msdn.microsoft.com/library/azure/hh767287.aspx).
* Queue Storage no es un servicio de inserción. Tener cola de hello toopoll.
* Puede tener cualquier número de colas. Para obtener más información, consulte la [API de REST del servicio de cola](https://docs.microsoft.com/rest/api/storageservices/Queue-Service-REST-API).
* Almacenamiento de la cola tiene algunas limitaciones y detalles toobe en cuenta. Estas se describen en [Colas de Azure y de Azure Service Bus: comparación y diferencias](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-azure-and-service-bus-queues-compared-contrasted).

## <a name="net-code-example"></a>Ejemplo de código .NET

ejemplo de código de Hello en esta sección Hola siguientes:

1. Define hello **EncodingJobMessage** clase que se asigna el formato de mensaje de notificación toohello. código de Hello deserializa los mensajes recibidos desde la cola de hello en objetos de hello **EncodingJobMessage** tipo.
2. Cargas Hola servicios multimedia y la información de cuenta de almacenamiento de archivo app.config de hello. ejemplo de código de Hello usa este Hola de toocreate información **CloudMediaContext** y **CloudQueue** objetos.
3. Crea la cola de Hola que recibe los mensajes de notificación sobre Hola trabajo de codificación.
4. Crea el extremo que está asignado toohello cola de notificación de Hola.
5. Asocia el trabajo de toohello de extremo de notificación de Hola y envía el trabajo de codificación de Hola. Puede tener varias notificaciones adjuntados dos puntos finales tooa trabajo.
6. Pasadas **NotificationJobState.FinalStatesOnly** toohello **AddNew** método. (En este ejemplo, estamos solo interesados en Estados finales del procesamiento de trabajos de Hola.)

        job.JobNotificationSubscriptions.AddNew(NotificationJobState.FinalStatesOnly, _notificationEndPoint);
7. Si se pasa **NotificationJobState.All**, obtendrá todas Hola siguiendo las notificaciones de cambio de estado: en cola, programada, procesamiento y terminado. Sin embargo, como se indicó anteriormente, Queue Storage no garantiza la entrega ordenada. mensajes de tooorder, usar hello **marca de tiempo** propiedad (definidos en hello **EncodingJobMessage** tipo en el siguiente ejemplo de Hola). Los mensajes duplicados son posibles. toocheck duplicados, utilice hello **propiedad ETag** (definidos en hello **EncodingJobMessage** tipo). También es posible que se omitan algunas notificaciones de cambio de estado.
8. Espera a que Hola trabajo tooget toohello terminado de estado mediante la comprobación de cola de hello cada 10 segundos. Elimina los mensajes una vez que se hayan procesado.
9. Elimina la cola de Hola y Hola de extremo de notificación.

> [!NOTE]
> Hola toomonitor de la manera recomendada que es el estado de un trabajo escucha los mensajes toonotification, como se muestra en el siguiente ejemplo de Hola.
>
> O bien, podría comprobar estado del trabajo mediante el uso de hello **IJob.State** propiedad.  Es posible que llegue un mensaje de notificación sobre la finalización de un trabajo antes de estado de hello en **IJob** se establece demasiado**finalizado**. Hola **IJob.State** propiedad refleja el estado preciso de hello con un breve lapso de tiempo.
>
>

### <a name="create-and-configure-a-visual-studio-project"></a>Creación y configuración de un proyecto de Visual Studio

1. Configurar el entorno de desarrollo y rellenar el archivo app.config de hello con información de conexión, como se describe en [desarrollo de servicios multimedia con .NET](media-services-dotnet-how-to-use.md). 
2. Cree una nueva carpeta (carpeta puede estar en cualquier parte en la unidad local) y copie un archivo. mp4 que se desean tooencode y el flujo o descarga progresiva. En este ejemplo, se utiliza la ruta de acceso de Hola "C:\Media".

### <a name="code"></a>Código

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

        // Type of hello event. Valid values are
        // JobStateChange and NotificationEndpointRegistration.
        public String EventType { get; set; }

        // ETag is used toohelp hello customer detect if
        // hello message is a duplicate of another message previously sent.
        public String ETag { get; set; }

        // Time of occurrence of hello event.
        public String TimeStamp { get; set; }

        // Collection of values specific toohello event.

        // For hello JobStateChange event hello values are:
        //     JobId - Id of hello Job that triggered hello notification.
        //     NewState- hello new state of hello Job. Valid values are:
        //          Scheduled, Processing, Canceling, Cancelled, Error, Finished
        //     OldState- hello old state of hello Job. Valid values are:
        //          Scheduled, Processing, Canceling, Cancelled, Error, Finished

        // For hello NotificationEndpointRegistration event hello values are:
        //     NotificationEndpointId- Id of hello NotificationEndpoint
        //          that triggered hello notification.
        //     State- hello state of hello Endpoint.
        //          Valid values are: Registered and Unregistered.

        public IDictionary<string, object> Properties { get; set; }
    }

    class Program
    {

        // Read values from hello App.config file.
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

            // Create hello context.
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            // Create hello queue that will be receiving hello notification messages.
            _queue = CreateQueue(_StorageConnectionString, endPointAddress);

            // Create hello notification point that is mapped toohello queue.
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

            // Create hello queue client
            CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

            // Retrieve a reference tooa queue
            CloudQueue queue = queueClient.GetQueueReference(endPointAddress);

            // Create hello queue if it doesn't already exist
            queue.CreateIfNotExists();

            return queue;
        }


        public static IJob SubmitEncodingJobWithNotificationEndPoint(string inputMediaFilePath)
        {
            // Declare a new job.
            IJob job = _context.Jobs.Create("My MP4 tooSmooth Streaming encoding job");

            //Create an encrypted asset and upload hello mp4.
            IAsset asset = CreateAssetAndUploadSingleFile(AssetCreationOptions.StorageEncrypted,
                inputMediaFilePath);

            // Get a media processor reference, and pass tooit hello name of the
            // processor toouse for hello specific task.
            IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

            // Create a task with hello conversion details, using a configuration file.
            ITask task = job.Tasks.AddNew("My encoding Task",
                processor,
                "Adaptive Streaming",
                Microsoft.WindowsAzure.MediaServices.Client.TaskOptions.None);

            // Specify hello input asset toobe encoded.
            task.InputAssets.Add(asset);

            // Add an output asset toocontain hello results of hello job.
            task.OutputAssets.AddNew("Output asset",
                AssetCreationOptions.None);

            // Add a notification point toohello job. You can add multiple notification points.  
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
                // Specify how often you want tooget messages from hello queue.
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

                        // Display hello message information.
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
                    // Delete hello message after we've read it.
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
Hola anterior hello en el ejemplo se produce después de salida. Los valores variarán.

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
        JobName: My MP4 tooSmooth Streaming encoding job
        NewState: Finished
        OldState: Processing
        AccountName: westeuropewamsaccount
    job with Id: nb:jid:UUID:526291de-f166-be47-b62a-11ffe6d4be54 reached expected
    State: Finished


## <a name="next-step"></a>Paso siguiente
Consulte las rutas de aprendizaje de Servicios multimedia.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Envío de comentarios
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
