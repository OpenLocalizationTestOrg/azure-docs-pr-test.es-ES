---
title: aaaHow toouse Service Bus de Azure con hello SDK de WebJobs
description: "Obtenga información acerca de cómo toouse colas de Service Bus de Azure y temas con Hola SDK de WebJobs."
services: app-service\web, service-bus
documentationcenter: .net
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: 2114a934-135b-42b8-871c-6cc040214e76
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/01/2016
ms.author: glenga
ms.openlocfilehash: cb801a9320a20c276da4f48c8941c09d3f09bb1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-service-bus-with-hello-webjobs-sdk"></a>Cómo toouse de Bus de servicio de Azure con Hola SDK de WebJobs
## <a name="overview"></a>Información general
Esta guía proporciona C# de ejemplos de código que muestran cómo tootrigger un proceso cuando se recibe un mensaje de Service Bus de Azure. uso de ejemplos de código de Hello [SDK de WebJobs](websites-dotnet-webjobs-sdk.md) versión 1.x.

Guía de Hola se supone que sabe [cómo cadenas toocreate un proyecto WebJob en Visual Studio con una conexión de esa cuenta de almacenamiento de punto tooyour](websites-dotnet-webjobs-sdk-get-started.md).

fragmentos de código de Hello solo muestran las funciones, no Hola código que crea hello `JobHost` objeto como en este ejemplo:

```
public class Program
{
   public static void Main()
   {
      JobHostConfiguration config = new JobHostConfiguration();
      config.UseServiceBus();
      JobHost host = new JobHost(config);
      host.RunAndBlock();
   }
}
```

A [ejemplo de código completo de Bus de servicio](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Program.cs) está en el repositorio de azure-webjobs-sdk-samples de hello en GitHub.com.

## <a id="prerequisites"></a> Requisitos previos
toowork con Bus de servicio tiene hello tooinstall [Microsoft.Azure.WebJobs.ServiceBus](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/) NuGet paquete además toohello otros paquetes de SDK de WebJobs. 

Tiene también la cadena de conexión de tooset hello AzureWebJobsServiceBus en cadenas de conexión de almacenamiento de toohello de adición.  Para hacer esto en hello `connectionStrings` sección del archivo App.config de hello, como se muestra en el siguiente ejemplo de Hola:

        <connectionStrings>
            <add name="AzureWebJobsDashboard" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="AzureWebJobsStorage" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="AzureWebJobsServiceBus" connectionString="Endpoint=sb://[yourServiceNamespace].servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[yourKey]"/>
        </connectionStrings>

Para un proyecto de ejemplo que incluye la configuración de la cadena de conexión de hello Bus de servicio en el archivo App.config de hello, consulte [ejemplo de Bus de servicio](https://github.com/Azure/azure-webjobs-sdk-samples/tree/master/BasicSamples/ServiceBus). 

las cadenas de conexión de Hello también pueden establecerse en entorno de Azure en tiempo de ejecución de hello, que invalida a continuación, configuración del archivo App.config hello cuando Hola trabajo Web se ejecuta en Azure; Para obtener más información, consulte [empezar a trabajar con hello SDK de WebJobs](websites-dotnet-webjobs-sdk-get-started.md#configure-the-web-app-to-use-your-azure-sql-database-and-storage-account).

## <a id="trigger"></a>¿Cómo se recibe tootrigger una función cuando un Bus de servicio cola de mensajes
llama a una función que Hola SDK de WebJobs toowrite cuando se recibe un mensaje de la cola, utilice hello `ServiceBusTrigger` atributo. constructor de atributos de Hello toma un parámetro que especifica el nombre de Hola de hello cola toopoll.

### <a name="how-servicebustrigger-works"></a>Cómo funciona ServiceBusTrigger
Hello SDK recibe un mensaje en `PeekLock` modo y llamadas `Complete` en el mensaje de bienvenida de si la función hello finaliza correctamente, o llamadas a `Abandon` si se produce un error en la función hello. Si se ejecuta más de hello función hello `PeekLock` tiempo de espera de bloqueo de Hola se renovará automáticamente.

Bus de servicio hace su propio control de la cola de mensajes dudosos que no puede ser controlado o configurado por hello SDK de WebJobs. 

### <a name="string-queue-message"></a>Mensajes en cola de cadena
Hello ejemplo de código siguiente lee un mensaje de la cola que contiene una cadena y escribe la cadena de hello toohello panel de SDK de WebJobs.

        public static void ProcessQueueMessage([ServiceBusTrigger("inputqueue")] string message, 
            TextWriter logger)
        {
            logger.WriteLine(message);
        }

**Nota:** si está creando Hola mensajes en cola en una aplicación que no utilice Hola SDK de WebJobs, asegúrese de tooset seguro [BrokeredMessage.ContentType](http://msdn.microsoft.com/library/microsoft.servicebus.messaging.brokeredmessage.contenttype.aspx) demasiado "text/plain".

### <a name="poco-queue-message"></a>Mensaje en cola de POCO
Hola SDK deserializará automáticamente un mensaje de la cola que contiene un valor JSON para un POCO [(objeto de CLR Plain Old](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) tipo. ejemplo de código siguiente Hello lee un mensaje de la cola que contiene un `BlobInformation` objeto que tiene un `BlobName` propiedad:

        public static void WriteLogPOCO([ServiceBusTrigger("inputqueue")] BlobInformation blobInfo,
            TextWriter logger)
        {
            logger.WriteLine("Queue message refers tooblob: " + blobInfo.BlobName);
        }

Para obtener ejemplos de código que muestra cómo las propiedades de toouse de hello POCO toowork con blobs y tablas de Hola igual, función, vea hello [versión de las colas de almacenamiento de información de este artículo](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#pocoblobs).

Si el código que crea el mensaje de bienvenida de cola no utiliza Hola SDK de WebJobs, utilice código toohello similar siguiente ejemplo:

        var client = QueueClient.CreateFromConnectionString(ConfigurationManager.ConnectionStrings["AzureWebJobsServiceBus"].ConnectionString, "blobadded");
        BlobInformation blobInformation = new BlobInformation () ;
        var message = new BrokeredMessage(blobInformation);
        client.Send(message);

### <a name="types-servicebustrigger-works-with"></a>Los tipos ServiceBusTrigger funcionan con
Además `string` y tipos POCO, puede usar hello `ServiceBusTrigger` atributo con una matriz de bytes o una `BrokeredMessage` objeto.

## <a id="create"></a>¿Cómo toocreate Bus de servicio cola de mensajes
una función que crea un nuevo mensaje de cola de toowrite usar hello `ServiceBus` atributo y pase un constructor de atributos de toohello de nombre de cola de Hola. 

### <a name="create-a-single-queue-message-in-a-non-async-function"></a>Crear un mensaje en cola único en una función no asincrónica
Hola siguiendo el ejemplo de código utiliza un toocreate de parámetro de salida un nuevo mensaje en cola Hola denominado "outputqueue" con el mismo contenido como Hola en cola Hola denominado "inputqueue" se recibió un mensaje de Hola.

        public static void CreateQueueMessage(
            [ServiceBusTrigger("inputqueue")] string queueMessage,
            [ServiceBus("outputqueue")] out string outputQueueMessage)
        {
            outputQueueMessage = queueMessage;
        }

parámetro de salida de Hello para la creación de un mensaje de la cola solo puede ser cualquiera de los siguientes tipos de hello:

* `string`
* `byte[]`
* `BrokeredMessage`
* Un tipo POCO serializable que define Seriado automáticamente como JSON.

Para los parámetros de tipo POCO, siempre se crea un mensaje de la cola cuando finaliza la función hello; Si el parámetro hello es null, Hola SDK crea un mensaje de cola que devolverá null cuando se recibe y deserializar los mensajes de bienvenida. Para Hola otros tipos, si el parámetro hello es null no se crea ningún mensaje de la cola.

### <a name="create-multiple-queue-messages-or-in-async-functions"></a>Crear varios mensajes en cola o en funciones asincrónicas
toocreate varios mensajes, usar hello `ServiceBus` atribuir a `ICollector<T>` o `IAsyncCollector<T>`, tal y como se muestra en el siguiente ejemplo de código de hello:

        public static void CreateQueueMessages(
            [ServiceBusTrigger("inputqueue")] string queueMessage,
            [ServiceBus("outputqueue")] ICollector<string> outputQueueMessage,
            TextWriter logger)
        {
            logger.WriteLine("Creating 2 messages in outputqueue");
            outputQueueMessage.Add(queueMessage + "1");
            outputQueueMessage.Add(queueMessage + "2");
        }

Cada mensaje de la cola se crea inmediatamente cuando hello `Add` se llama al método.

## <a id="topics"></a>¿Cómo toowork con temas de Bus de servicio
llama a una función que Hola SDK toowrite cuando se recibe un mensaje en un tema de Bus de servicio, use hello `ServiceBusTrigger` atributo con el constructor de Hola que toma el nombre del tema y nombre de la suscripción, como se muestra en el siguiente ejemplo de código de hello:

        public static void WriteLog([ServiceBusTrigger("outputtopic","subscription1")] string message,
            TextWriter logger)
        {
            logger.WriteLine("Topic message: " + message);
        }

toocreate un mensaje en un tema, use hello `ServiceBus` atributo con un hello de nombre de tema igual forma que se utiliza con un nombre de la cola.

## <a name="features-added-in-release-11"></a>Características agregadas en la versión 1.1
Hola siguientes características se agregaron en la versión 1.1:

* Se permite la personalización profunda del procesamiento de mensajes a través de `ServiceBusConfiguration.MessagingProvider`.
* `MessagingProvider`admite la personalización de hello Service Bus `MessagingFactory` y `NamespaceManager`.
* Un `MessageProcessor` patrón de estrategia le permite toospecify un procesador por cola/tema.
* La simultaneidad del procesamiento de mensajes se admite de manera predeterminada. 
* La personalización sencilla de `OnMessageOptions` a través de `ServiceBusConfiguration.MessageOptions`.
* Permitir [AccessRights](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Functions.cs#L71) toobe especificado en `ServiceBusTriggerAttribute` / `ServiceBusAttribute` (para escenarios donde puede que no tenga derechos de administración). Tenga en cuenta que WebJobs de Azure es temas sin administrar AccessRights y colas de tooautomatically no se puede aprovisionar inexistente.

## <a id="queues"></a>Temas relacionados cubiertos por las colas de almacenamiento de hello cómo-tooarticle
Para obtener información acerca de los escenarios de SDK de WebJobs tooService no específico del Bus, vea [cómo toouse Azure cola de almacenamiento con hello SDK de WebJobs](websites-dotnet-webjobs-sdk-storage-queues-how-to.md). 

Los temas tratados en dicho artículo Hola siguientes:

* Funciones asincrónicas
* Varias instancias
* Apagado correcto
* Utilizar atributos de SDK de WebJobs en el cuerpo de Hola de una función
* Establecer las cadenas de conexión de SDK de hello en el código
* Establecer valores para los parámetros del constructor del SDK de WebJobs en el código
* Desencadenar una función manualmente
* Escribir registros

## <a id="nextsteps"></a> Pasos siguientes
Esta guía proporciona código de ejemplos que muestran cómo toohandle escenarios comunes para trabajar con el Bus de servicio de Azure. Para obtener más información sobre cómo toouse WebJobs de Azure y Hola SDK de WebJobs, vea [Azure trabajos Web recomienda recursos](http://go.microsoft.com/fwlink/?linkid=390226).

