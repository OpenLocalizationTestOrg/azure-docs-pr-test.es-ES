---
title: aaaUsing .NET clase bibliotecas con funciones de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooauthor bibliotecas de clases de .NET para usar con funciones de Azure"
services: functions
documentationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: "azure functions, funciones, procesamiento de eventos, proceso dinámico, arquitectura sin servidor"
ms.assetid: 9f5db0c2-a88e-4fa8-9b59-37a7096fc828
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 06/09/2017
ms.author: donnam
ms.openlocfilehash: 4e0fd954b554006ba1d8ecc47403a9fb1c67c3b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-net-class-libraries-with-azure-functions"></a>Utilizar bibliotecas de clases de .NET con Azure Functions

Además tooscript archivos, las funciones de Azure es compatible con la publicación de una biblioteca de clases como implementación de Hola para una o más funciones. Le recomendamos que use hello [Azure funciones de Visual Studio de 2017 Tools](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/).

## <a name="prerequisites"></a>Requisitos previos 

Este artículo tiene Hola siguiendo los requisitos previos:

- [Versión preliminar de Visual Studio 2017 15.3](https://www.visualstudio.com/vs/preview/). Instalar las cargas de trabajo de hello **ASP.NET y desarrollo web** y **desarrollo Azure**.
- [Herramientas de Azure Functions para Visual Studio 2017](https://marketplace.visualstudio.com/items?itemName=AndrewBHall-MSFT.AzureFunctionToolsforVisualStudio2017)

## <a name="functions-class-library-project"></a>Proyecto de biblioteca de clases de Functions

En Visual Studio, cree un nuevo proyecto de Azure Functions. nueva plantilla de proyecto Hola crea archivos de hello *host.json* y *local.settings.json*. Puede [personalizar la configuración en tiempo de ejecución de Azure Functions en host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json). 

archivo hello *local.settings.json* almacena la configuración de aplicación, las cadenas de conexión y configuración de herramientas básicas de las funciones de Azure. toolearn más información acerca de su estructura, vea [código y probar las funciones de Azure localmente](functions-run-local.md#local-settings).

### <a name="functionname-attribute"></a>Atributo FunctionName

atributo de Hello [ `FunctionNameAttribute` ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/FunctionNameAttribute.cs) marca un método como un punto de entrada de función. Se debe utilizar exactamente con un desencadenador y 0 o más enlaces de entrada y salida.

### <a name="conversion-toofunctionjson"></a>Conversión toofunction.json

Cuando se compila un proyecto de las funciones de Azure, genera un archivo `function.json` en el directorio de hello con el mismo nombre de función hello definido por `[FunctionName]`. Especifica los desencadenadores y los enlaces y puntos toohello el archivo de ensamblado de proyecto.

Esta conversión se realiza por paquete de NuGet hello [Microsoft\.NET\.Sdk\.funciones](http://www.nuget.org/packages/Microsoft.NET.Sdk.Functions). Hola origen está disponible en el repositorio de GitHub de hello [azure\-funciones\-frente a\-generar\-sdk](https://github.com/Azure/azure-functions-vs-build-sdk).

## <a name="triggers-and-bindings"></a>Desencadenadores y enlaces

Hello tabla siguiente enumeran los desencadenadores de Hola y enlaces que están disponibles en un proyecto de biblioteca de clases de las funciones de Azure. Todos los atributos no están en el espacio de nombres de hello `Microsoft.Azure.WebJobs`.

| Enlace | Atributo | Paquete de NuGet |
|------   | ------    | ------        |
| [Desencadenador de almacenamiento de blobs, entrada, salida](#blob-storage) | [BlobAttribute], [StorageAccountAttribute] | [Microsoft.Azure.WebJobs] | [Almacenamiento de blobs] |
| [Enlaces de entrada y salida de Cosmos DB](#cosmos-db) | [DocumentDBAttribute] | [Microsoft.Azure.WebJobs.Extensions.DocumentDB] | 
| [Desencadenador y salida de Event Hubs](#event-hub) | [EventHubTriggerAttribute], [EventHubAttribute] | [Microsoft.Azure.WebJobs.ServiceBus] |
| [Entrada y salida de archivos externos](#api-hub) | [ApiHubFileAttribute] | [Microsoft.Azure.WebJobs.Extensions.ApiHub] |
| [Desencadenador HTTP y webhook](#http) | [HttpTriggerAttribute] | [Microsoft.Azure.WebJobs.Extensions.Http] |
| [Entrada y salida de Mobile Apps](#mobile-apps) | [MobileTableAttribute] | [Microsoft.Azure.WebJobs.Extensions.MobileApps] | 
| [Salida de Notification Hubs](#nh) | [NotificationHubAttribute] | [Microsoft.Azure.WebJobs.Extensions.NotificationHubs] | 
| [Desencadenador y salida de Queue Storage](#queue) | [QueueAttribute], [StorageAccountAttribute] | [Microsoft.Azure.WebJobs] | 
| [Salida de SendGrid](#sendgrid) | [SendGridAttribute] | [Microsoft.Azure.WebJobs.Extensions.SendGrid] | 
| [Desencadenador y salida de Service Bus](#service-bus) | [ServiceBusAttribute], [ServiceBusAccountAttribute] | [Microsoft.Azure.WebJobs.ServiceBus]
| [Entrada y salida de Table Storage](#table) | [TableAttribute], [StorageAccountAttribute] | [Microsoft.Azure.WebJobs] | 
| [Desencadenador de temporizador](#timer) | [TimerTriggerAttribute] | [Microsoft.Azure.WebJobs.Extensions] | 
| [Salida de Twilio](#twilio) | [TwilioSmsAttribute] | [Microsoft.Azure.WebJobs.Extensions.Twilio] | 

<a name="blob-storage"></a>

### <a name="blob-storage-trigger-input-and-output-bindings"></a>Desencadenador y enlaces de entrada y salida de Blob Storage

Azure Functions admite desencadenador y enlaces de entrada y salida para Azure Blob Storage. Para más información sobre las expresiones de enlace y los metadatos, consulte [Enlaces de Blob Storage de Azure Functions](functions-bindings-storage-blob.md).

Se define un desencadenador de blob con hello `[BlobTrigger]` atributo. Puede usar el atributo de hello `[StorageAccount]` cuenta de almacenamiento de hello toodefine utilizado por una función completa o clase.

```csharp
[StorageAccount("AzureWebJobsStorage")]
[FunctionName("BlobTriggerCSharp")]        
public static void Run([BlobTrigger("samples-workitems/{name}")] Stream myBlob, string name, TraceWriter log)
{
    log.Info($"C# Blob trigger function Processed blob\n Name:{name} \n Size: {myBlob.Length} Bytes");
}
```

BLOB de entrada y salida se definen mediante hello `[Blob]` atributo, junto con un `FileAccess` que indica el parámetro de lectura o escritura. Hola siguiente ejemplo se usa un desencadenador de blob y enlace de salida de blobs.

```csharp
[FunctionName("ResizeImage")]
[StorageAccount("AzureWebJobsStorage")]
public static void Run(
    [BlobTrigger("sample-images/{name}")] Stream image, 
    [Blob("sample-images-sm/{name}", FileAccess.Write)] Stream imageSmall, 
    [Blob("sample-images-md/{name}", FileAccess.Write)] Stream imageMedium)
{
    var imageBuilder = ImageResizer.ImageBuilder.Current;
    var size = imageDimensionsTable[ImageSize.Small];

    imageBuilder.Build(image, imageSmall,
        new ResizeSettings(size.Item1, size.Item2, FitMode.Max, null), false);

    image.Position = 0;
    size = imageDimensionsTable[ImageSize.Medium];

    imageBuilder.Build(image, imageMedium,
        new ResizeSettings(size.Item1, size.Item2, FitMode.Max, null), false);
}

public enum ImageSize { ExtraSmall, Small, Medium }

private static Dictionary<ImageSize, (int, int)> imageDimensionsTable = new Dictionary<ImageSize, (int, int)>() {
    { ImageSize.ExtraSmall, (320, 200) },
    { ImageSize.Small,      (640, 400) },
    { ImageSize.Medium,     (800, 600) }
};
```        

<a name="cosmos-db"></a>

### <a name="cosmos-db-input-and-output-bindings"></a>Enlaces de entrada y salida de Cosmos DB

Azure Functions admite enlaces de entrada y salida para Cosmos DB. vea toolearn más información acerca de características de Hola de enlace, la base de datos de Cosmos hello [enlaces de base de datos de Azure funciones Cosmos](functions-bindings-documentdb.md).

toobind tooa documento de Cosmos DB, utilice el atributo de hello `[DocumentDB]` en paquete de NuGet hello [Microsoft.Azure.WebJobs.Extensions.DocumentDB]. Hola siguiente ejemplo tiene un desencadenador de cola y una API de documentos que el enlace de salida:

```csharp
[FunctionName("QueueToDocDB")]        
public static void Run(
    [QueueTrigger("myqueue-items", Connection = "AzureWebJobsStorage")] string myQueueItem, 
    [DocumentDB("ToDoList", "Items", ConnectionStringSetting = "DocDBConnection")] out dynamic document)
{
    document = new { Text = myQueueItem, id = Guid.NewGuid() };
}

```

<a name="event-hub"></a>

### <a name="event-hubs-trigger-and-output"></a>Desencadenador y salida de Event Hubs

Azure Functions admite enlaces de desencadenador y salida para Event Hubs. Para más información, consulte [Enlaces de Event Hub de Azure Functions](functions-bindings-event-hubs.md).

Hola tipos `[Microsoft.Azure.WebJobs.ServiceBus.EventHubTriggerAttribute]` y `[Microsoft.Azure.WebJobs.ServiceBus.EventHubAttribute]` se definen en el paquete de NuGet hello [Microsoft.Azure.WebJobs.ServiceBus]. 

Hello en el ejemplo siguiente se usa un desencadenador de concentrador de eventos:

```csharp
[FunctionName("EventHubTriggerCSharp")]
public static void Run([EventHubTrigger("samples-workitems", Connection = "EventHubConnection")] string myEventHubMessage, TraceWriter log)
{
    log.Info($"C# Event Hub trigger function processed a message: {myEventHubMessage}");
}
```

Hello en el ejemplo siguiente se tiene un concentrador de eventos de salida, utilizando el valor devuelto del método hello como salida de hello:

```csharp
[FunctionName("EventHubOutput")]
[return: EventHub("outputEventHubMessage", Connection = "EventHubConnection")]
public static string Run([TimerTrigger("0 */5 * * * *")] TimerInfo myTimer, TraceWriter log)
{
    log.Info($"C# Timer trigger function executed at: {DateTime.Now}");
    return $"{DateTime.Now}";
}
```

<a name="api-hub"></a>

### <a name="external-file-input-and-output"></a>Entrada y salida de archivo externo

Azure Functions admite enlaces de desencadenador, entrada y salida para archivos externos, como Google Drive, Dropbox y OneDrive. más información, consulte toolearn [enlaces del archivo externo de las funciones de Azure](functions-bindings-external-file.md). Hola atributos `[ExternalFileTrigger]` y `[ExternalFile]` se definen en el paquete de NuGet hello [Microsoft.Azure.WebJobs.Extensions.ApiHub].

Hola el ejemplo de C# siguiente se muestra un archivo externo de entrada y salida de enlace. copias de código de Hello Hola archivo de salida de toohello de archivo de entrada.

```csharp
[StorageAccount("MyStorageConnection")]
[FunctionName("ExternalFile")]
[return: ApiHubFile("MyFileConnection", "samples-workitems/{queueTrigger}-Copy", FileAccess.Write)]
public static string Run([QueueTrigger("myqueue-items")] string myQueueItem, 
    [ApiHubFile("MyFileConnection", "samples-workitems/{queueTrigger}", FileAccess.Read)] string myInputFile, 
    TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    return myInputFile;
}
```

<a name="http"></a>

### <a name="http-and-webhooks"></a>HTTP y webhooks

Hola de uso `HttpTrigger` webhook o el desencadenador de toodefine HTTP de atributo. Este atributo se define en el paquete de NuGet hello [Microsoft.Azure.WebJobs.Extensions.Http]. Puede personalizar el nivel de autorización de hello, tipo de webhook, ruta y métodos. Hello en el ejemplo siguiente se define un desencadenador HTTP con la autenticación anónima y _genericJson_ webhook tipo.

```csharp
[FunctionName("HttpTriggerCSharp")]
public static HttpResponseMessage Run([HttpTrigger(AuthorizationLevel.Anonymous, WebHookType = "genericJson")] HttpRequestMessage req)
{
    return req.CreateResponse(HttpStatusCode.OK);
}
```

<a name="mobile-apps"></a>

### <a name="mobile-apps-input-and-output"></a>Entrada y salida de Mobile Apps

Azure Functions admite enlaces de entrada y salida para Mobile Apps. más información, consulte toolearn [enlaces de aplicaciones móviles de Azure funciones](functions-bindings-mobile-apps.md). atributo de Hello `[MobileTable]` se define en el paquete de NuGet hello [Microsoft.Azure.WebJobs.Extensions.MobileApps].

Hello en el ejemplo siguiente se muestra un aplicaciones móviles de enlace de salida:

```csharp
[FunctionName("MobileAppsOutput")]        
[return: MobileTable(ApiKeySetting = "MyMobileAppKey", TableName = "MyTable", MobileAppUriSetting = "MyMobileAppUri")]
public static object Run([QueueTrigger("myqueue-items", Connection = "AzureWebJobsStorage")] string myQueueItem, TraceWriter log)
{
    return new { Text = $"I'm running in a C# function! {myQueueItem}" };
}
```

<a name="nh"></a>

### <a name="notification-hubs-output"></a>Salida de Notification Hubs

Azure Functions admite un enlace de salida para Notification Hubs. más información, consulte toolearn [enlace de salida del centro de notificaciones de las funciones de Azure](functions-bindings-notification-hubs.md). atributo de Hello `[NotificationHub]` se define en el paquete de NuGet hello [Microsoft.Azure.WebJobs.Extensions.NotificationHubs].

<a name="queue"></a>

### <a name="queue-storage-trigger-and-output"></a>Desencadenador y salida de Queue Storage

Azure Functions admite desencadenador y enlaces de salida para Azure Queues. Para más información, consulte [Enlaces de Queue Storage de Azure Functions](functions-bindings-storage-queue.md).

Hello en el ejemplo siguiente se muestra la función de hello toouse tipo de valor devuelto con una salida de cola de enlace, el uso de hello `[Queue]` atributo. toodefine un desencadenador de cola, usar hello `[QueueTrigger]` atributo.

```csharp
[StorageAccount("AzureWebJobsStorage")]
public static class QueueFunctions
{
    // HTTP trigger with queue output binding
    [FunctionName("QueueOutput")]
    [return: Queue("myqueue-items")]
    public static string QueueOutput([HttpTrigger] dynamic input,  TraceWriter log)
    {
        log.Info($"C# function processed: {input.Text}");
        return input.Text;
    }

    // Queue trigger
    [FunctionName("QueueTrigger")]
    [StorageAccount("AzureWebJobsStorage")]
    public static void QueueTrigger([QueueTrigger("myqueue-items")] string myQueueItem, TraceWriter log)
    {
        log.Info($"C# function processed: {myQueueItem}");
    }
}

```

<a name="sendgrid"></a>

### <a name="sendgrid-output"></a>Salida de SendGrid

Azure Functions admite un enlace de salida de SendGrid para el envío de correo electrónico mediante programación. más información, consulte toolearn [SendGrid de funciones de Azure enlaces](functions-bindings-sendgrid.md).

atributo de Hello `[SendGrid]` se define en el paquete de NuGet hello [Microsoft.Azure.WebJobs.Extensions.SendGrid].

Hello siguiente es un ejemplo del uso de un desencadenador de cola de Bus de servicio y un enlace de salida de SendGrid mediante `SendGridMessage`:

```csharp
[FunctionName("SendEmail")]
public static void Run(
    [ServiceBusTrigger("myqueue", AccessRights.Manage, Connection = "ServiceBusConnection")] OutgoingEmail email,
    [SendGrid] out SendGridMessage message)
{
    message = new SendGridMessage();
    message.AddTo(email.To);
    message.AddContent("text/html", email.Body);
    message.SetFrom(new EmailAddress(email.From));
    message.SetSubject(email.Subject);
}

public class OutgoingEmail
{
    public string too{ get; set; }
    public string From { get; set; }
    public string Subject { get; set; }
    public string Body { get; set; }
}
```

<a name="service-bus"></a>

### <a name="service-bus-trigger-and-output"></a>Desencadenador y salida de Service Bus

Azure Functions admite enlaces de desencadenador y salida para colas y temas de Service Bus. Para más información sobre la configuración de enlaces, consulte [Enlaces de Service Bus de Azure Functions](functions-bindings-service-bus.md).

Hola atributos `[ServiceBusTrigger]` y `[ServiceBus]` se definen en el paquete de NuGet hello [Microsoft.Azure.WebJobs.ServiceBus]. 

Hola te mostramos un ejemplo de un desencadenador de cola de Bus de servicio:

```csharp
[FunctionName("ServiceBusQueueTriggerCSharp")]                    
public static void Run([ServiceBusTrigger("myqueue", AccessRights.Manage, Connection = "ServiceBusConnection")] string myQueueItem, TraceWriter log)
{
    log.Info($"C# ServiceBus queue trigger function processed message: {myQueueItem}");
}
```

Hola te mostramos un ejemplo de una salida de Bus de servicio de enlace, utilizando el tipo de valor devuelto de método hello como salida de hello:

```csharp
[FunctionName("ServiceBusOutput")]
[return: ServiceBus("myqueue", Connection = "ServiceBusConnection")]
public static string ServiceBusOutput([HttpTrigger] dynamic input, TraceWriter log)
{
    log.Info($"C# function processed: {input.Text}");
    return input.Text;
}
```        

<a name="table"></a>

### <a name="table-storage-input-and-output"></a>Entrada y salida de Table Storage

Azure Functions admite enlaces de entrada y salida para Table Storage de Azure. más información, consulte toolearn [enlaces de almacenamiento de tabla de funciones de Azure](functions-bindings-storage-table.md).

Hello siguiente ejemplo es una clase con dos funciones, que muestra la salida de almacenamiento de tabla y los enlaces de entrada. 

```csharp
[StorageAccount("AzureWebJobsStorage")]
public class TableStorage
{
    public class MyPoco
    {
        public string PartitionKey { get; set; }
        public string RowKey { get; set; }
        public string Text { get; set; }
    }

    [FunctionName("TableOutput")]
    [return: Table("MyTable")]
    public static MyPoco TableOutput([HttpTrigger] dynamic input, TraceWriter log)
    {
        log.Info($"C# http trigger function processed: {input.Text}");
        return new MyPoco { PartitionKey = "Http", RowKey = Guid.NewGuid().ToString(), Text = input.Text };
    }

    // use hello metadata parameter "queueTrigger" toobind hello queue payload
    [FunctionName("TableInput")]
    public static void TableInput([QueueTrigger("table-items")] string input, [Table("MyTable", "Http", "{queueTrigger}")] MyPoco poco, TraceWriter log)
    {
        log.Info($"C# function processed: {poco.Text}");
    }
}

```

<a name="timer"></a>

### <a name="timer-trigger"></a>Desencadenador de temporizador

Azure Functions incluye un enlace a un desencadenador de temporizador que le permite ejecutar su código de función según una programación definida. toolearn más información acerca de características de hello del enlace de hello, consulte [programar la ejecución del código con las funciones de Azure](functions-bindings-timer.md).

Plan de consumo de hello, puede definir programaciones con un [expresión CRON](http://en.wikipedia.org/wiki/Cron#CRON_expression). Si utiliza un plan de App Service, también puede usar una cadena TimeSpan. 

Hola de ejemplo siguiente define un desencadenador de temporizador que se ejecuta cada 5 minutos:

```csharp
[FunctionName("TimerTriggerCSharp")]
public static void Run([TimerTrigger("0 */5 * * * *")]TimerInfo myTimer, TraceWriter log)
{
    log.Info($"C# Timer trigger function executed at: {DateTime.Now}");
}
```

<a name="twilio"></a>

### <a name="twilio-output"></a>Salida de Twilio

Azure funciones es compatible con Twilio habían salida enlaces tooenable los mensajes de texto SMS de toosend de funciones. más información, consulte toolearn [enlace de salida de SMS enviar mensajes desde las funciones de Azure mediante Twilio hello](functions-bindings-twilio.md). 

atributo de Hello `[TwilioSms]` se define en el paquete de hello [Microsoft.Azure.WebJobs.Extensions.Twilio].

Hello ejemplo C# siguiente utiliza una cola de desencadenador y un Twilio el enlace de salida:

```csharp
[FunctionName("QueueTwilio")]
[return: TwilioSms(AccountSidSetting = "TwilioAccountSid", AuthTokenSetting = "TwilioAuthToken", From = "+1425XXXXXXX" )]
public static SMSMessage Run([QueueTrigger("myqueue-items", Connection = "AzureWebJobsStorage")] JObject order, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {order}");

    var message = new SMSMessage()
    {
        Body = $"Hello {order["name"]}, thanks for your order!",
        too= order["mobileNumber"].ToString()
    };

    return message;
}
```

## <a name="next-steps"></a>Pasos siguientes

Para más información sobre el uso de Azure Functions en C# de scripting, consulte [Referencia para desarrolladores de C\# de script de Azure Functions](functions-reference-csharp.md).

[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]


<!-- NuGet packages --> 
[Microsoft.Azure.WebJobs]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs/2.1.0-beta1
[Microsoft.Azure.WebJobs.Extensions.DocumentDB]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.DocumentDB/1.1.0-beta1
[Microsoft.Azure.WebJobs.ServiceBus]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/2.1.0-beta1
[Microsoft.Azure.WebJobs.Extensions.MobileApps]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.MobileApps/1.1.0-beta1
[Microsoft.Azure.WebJobs.Extensions.NotificationHubs]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.NotificationHubs/1.1.0-beta1
[Microsoft.Azure.WebJobs.ServiceBus]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/2.1.0-beta1
[Microsoft.Azure.WebJobs.Extensions.SendGrid]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.SendGrid/2.1.0-beta1
[Microsoft.Azure.WebJobs.Extensions.Http]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.Http/1.0.0-beta1
[Microsoft.Azure.WebJobs.Extensions.BotFramework]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.BotFramework/1.0.15-beta
[Microsoft.Azure.WebJobs.Extensions.ApiHub]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.ApiHub/1.0.0-beta4
[Microsoft.Azure.WebJobs.Extensions.Twilio]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.Twilio/1.1.0-beta1
[Microsoft.Azure.WebJobs.Extensions]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions/2.1.0-beta1


<!-- Links toosource --> 
[DocumentDBAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.DocumentDB/DocumentDBAttribute.cs
[EventHubAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubAttribute.cs
[EventHubTriggerAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubTriggerAttribute.cs
[MobileTableAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs
[NotificationHubAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.NotificationHubs/NotificationHubAttribute.cs 
[ServiceBusAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAttribute.cs
[ServiceBusAccountAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs
[QueueAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/QueueAttribute.cs
[StorageAccountAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs
[BlobAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs
[TableAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/TableAttribute.cs
[TwilioSmsAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.Twilio/TwilioSMSAttribute.cs
[SendGridAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.SendGrid/SendGridAttribute.cs
[HttpTriggerAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/dev/src/WebJobs.Extensions.Http/HttpTriggerAttribute.cs
[ApiHubFileAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.ApiHub/ApiHubFileAttribute.cs
[TimerTriggerAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions/Extensions/Timers/TimerTriggerAttribute.cs
