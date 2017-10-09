---
title: Hola a aaaReceive eventos desde los centros de eventos de Azure mediante .NET Framework | Documentos de Microsoft
description: Siga este tutorial tooreceive eventos desde los centros de eventos de Azure con hello .NET Framework.
services: event-hubs
documentationcenter: 
author: sethmanheim
manager: timlt
editor: 
ms.assetid: c4974bd3-2a79-48a1-aa3b-8ee2d6655b28
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/12/2017
ms.author: sethm
ms.openlocfilehash: a88c3feeacfd3de9622dbb86e25222e861750204
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="receive-events-from-azure-event-hubs-using-hello-net-framework"></a>Recibir eventos desde los centros de eventos de Azure con hello .NET Framework

## <a name="introduction"></a>Introducción

Event Hubs es un servicio que procesa grandes cantidades de datos de eventos (telemetría) desde aplicaciones y dispositivos conectados. Después de recopilar datos en los centros de eventos, puede almacenar datos de hello mediante un clúster de almacenamiento o transformar mediante un proveedor de análisis en tiempo real. Esta capacidad de procesamiento y la colección de eventos a gran escala es un componente clave de arquitecturas de aplicación moderna incluidos Hola Internet de las cosas (IoT).

Este tutorial muestra cómo toowrite de .NET Framework consola aplicación que recibe los mensajes de un concentrador de eventos con hello  **[Host procesador de eventos][EventProcessorHost]**. eventos de toosend mediante Hola .NET Framework, vea hello [enviar eventos tooAzure centros de eventos mediante .NET Framework hello](event-hubs-dotnet-framework-getstarted-send.md) el artículo, o haga clic en el idioma envío adecuado de hello en la tabla de contenido izquierdo de Hola.

Hola [Host procesador de eventos] [ EventProcessorHost] es una clase .NET que simplifica la reciba los eventos de los centros de eventos mediante la administración de los puntos de control persistentes y paralelo recibe de los centros de eventos. Con hello [Host procesador de eventos][Event Processor Host], puede dividir los eventos de varios receptores, incluso cuando se hospeda en distintos nodos. Este ejemplo se muestra cómo hello toouse [Host procesador de eventos] [ EventProcessorHost] para un único receptor. Hola [escalar horizontalmente el procesamiento de eventos] [ Scale out Event Processing with Event Hubs] ejemplo muestra cómo hello toouse [Host procesador de eventos] [ EventProcessorHost] con varios receptores.

## <a name="prerequisites"></a>Requisitos previos

toocomplete este tutorial, necesita Hola siguiendo los requisitos previos:

* [Microsoft Visual Studio 2015 o una versión superior](http://visualstudio.com). capturas de pantalla de Hello en este tutorial utilizan Visual Studio de 2017.
* Una cuenta de Azure activa. En caso de no tener ninguna, puede crear una cuenta gratuita en tan solo unos minutos. Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/free/).

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a>Creación de un espacio de nombres de Event Hubs y un centro de eventos

Hola primer paso es hello toouse [portal de Azure](https://portal.azure.com) toocreate un espacio de nombres del tipo centros de eventos y obtener Hola credenciales de administración de la aplicación necesita toocommunicate con el concentrador de eventos de Hola. toocreate un espacio de nombres y el concentrador de eventos, siga el procedimiento de hello en [este artículo](event-hubs-create.md), a continuación, continúe con hello sigue los pasos de este tutorial.

## <a name="create-an-azure-storage-account"></a>Creación de una cuenta de almacenamiento de Azure

Hola toouse [Host procesador de eventos][EventProcessorHost], debe tener un [cuenta de almacenamiento de Azure][Azure Storage account]:

1. Inicie sesión en toohello [portal de Azure][Azure portal]y haga clic en **New** en hello parte superior izquierda de la pantalla de bienvenida.
2. Haga clic en **Storage** y luego en **Cuenta de Storage**.
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage1.png)
3. Hola **crear cuenta de almacenamiento** hoja, escriba un nombre para la cuenta de almacenamiento de Hola. Elija una suscripción de Azure, el grupo de recursos y la ubicación en el recurso que hello toocreate. A continuación, haga clic en **Crear**.
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage2.png)
4. Hola lista de cuentas de almacenamiento, haga clic en hello recién creado la cuenta de almacenamiento.
5. En la hoja de la cuenta de almacenamiento de hello, haga clic en **las claves de acceso**. Copiar valor de Hola de **key1** toouse más adelante en este tutorial.
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage3.png)

## <a name="create-a-receiver-console-application"></a>Creación de una aplicación de consola de destinatario

1. En Visual Studio, cree un nuevo proyecto de aplicación de escritorio de Visual C# con hello **aplicación de consola** plantilla de proyecto. Proyecto de hello Name **receptor**.
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-receiver-csharp1.png)
2. En el Explorador de soluciones, haga clic en hello **receptor** del proyecto y, a continuación, haga clic en **administrar paquetes de NuGet para la solución**.
3. Haga clic en hello **examinar** y, después, busque `Microsoft Azure Service Bus Event Hub - EventProcessorHost`. Haga clic en **instalar**y acepte los términos de Hola de uso.
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-eph-csharp1.png)
   
    Visual Studio descarga, instala y agrega una referencia toohello [centro de eventos de Bus de servicio de Azure - paquete de EventProcessorHost NuGet](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost), con todas sus dependencias.
4. Menú contextual hello **receptor** proyecto de equipo y haga clic en **agregar**y, a continuación, haga clic en **clase**. Hola nueva clase el nombre **SimpleEventProcessor**y, a continuación, haga clic en **agregar** clase de hello toocreate.
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-receiver-csharp2.png)
5. Agregue Hola siguiendo las instrucciones al principio de hello del archivo de SimpleEventProcessor.cs de hello:
    
  ```csharp
  using Microsoft.ServiceBus.Messaging;
  using System.Diagnostics;
  ```
    
  A continuación, sustituya Hola siguiente código en el cuerpo de Hola de clase hello:
    
  ```csharp
  class SimpleEventProcessor : IEventProcessor
  {
    Stopwatch checkpointStopWatch;
    
    async Task IEventProcessor.CloseAsync(PartitionContext context, CloseReason reason)
    {
        Console.WriteLine("Processor Shutting Down. Partition '{0}', Reason: '{1}'.", context.Lease.PartitionId, reason);
        if (reason == CloseReason.Shutdown)
        {
            await context.CheckpointAsync();
        }
    }
    
    Task IEventProcessor.OpenAsync(PartitionContext context)
    {
        Console.WriteLine("SimpleEventProcessor initialized.  Partition: '{0}', Offset: '{1}'", context.Lease.PartitionId, context.Lease.Offset);
        this.checkpointStopWatch = new Stopwatch();
        this.checkpointStopWatch.Start();
        return Task.FromResult<object>(null);
    }
    
    async Task IEventProcessor.ProcessEventsAsync(PartitionContext context, IEnumerable<EventData> messages)
    {
        foreach (EventData eventData in messages)
        {
            string data = Encoding.UTF8.GetString(eventData.GetBytes());
    
            Console.WriteLine(string.Format("Message received.  Partition: '{0}', Data: '{1}'",
                context.Lease.PartitionId, data));
        }
    
        //Call checkpoint every 5 minutes, so that worker can resume processing from 5 minutes back if it restarts.
        if (this.checkpointStopWatch.Elapsed > TimeSpan.FromMinutes(5))
        {
            await context.CheckpointAsync();
            this.checkpointStopWatch.Restart();
        }
    }
  }
  ```
    
  Esta clase se denomina por hello **EventProcessorHost** eventos de tooprocess recibidos desde el concentrador de eventos de Hola. Hola `SimpleEventProcessor` clase utiliza un método de punto de comprobación de cronómetro tooperiodically llamada hello en hello **EventProcessorHost** contexto. Este proceso garantiza que, si se reinicia el receptor de hello, pierde no más de cinco minutos de trabajo de procesamiento.
6. Hola **programa** de clases, agregue los siguientes hello `using` declaración en la parte superior de hello del archivo hello:
    
  ```csharp
  using Microsoft.ServiceBus.Messaging;
  ```
    
  A continuación, reemplace hello `Main` método Hola `Program` clase con el siguiente código de hello, sustituyendo el nombre del centro de eventos de Hola y conexiones de nivel de espacio de nombres de Hola de cadena que se guardó anteriormente y Hola cuenta de almacenamiento y la clave que ha copiado en hello secciones anteriores. 
    
  ```csharp
  static void Main(string[] args)
  {
    string eventHubConnectionString = "{Event Hubs namespace connection string}";
    string eventHubName = "{Event Hub name}";
    string storageAccountName = "{storage account name}";
    string storageAccountKey = "{storage account key}";
    string storageConnectionString = string.Format("DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}", storageAccountName, storageAccountKey);
    
    string eventProcessorHostName = Guid.NewGuid().ToString();
    EventProcessorHost eventProcessorHost = new EventProcessorHost(eventProcessorHostName, eventHubName, EventHubConsumerGroup.DefaultGroupName, eventHubConnectionString, storageConnectionString);
    Console.WriteLine("Registering EventProcessor...");
    var options = new EventProcessorOptions();
    options.ExceptionReceived += (sender, e) => { Console.WriteLine(e.Exception); };
    eventProcessorHost.RegisterEventProcessorAsync<SimpleEventProcessor>(options).Wait();
    
    Console.WriteLine("Receiving. Press enter key toostop worker.");
    Console.ReadLine();
    eventProcessorHost.UnregisterEventProcessorAsync().Wait();
  }
  ```

7. Ejecutar programa hello y asegúrese de que no hay ningún error.
  
¡Enhorabuena! Ahora ha recibido mensajes de un concentrador de eventos mediante Hola Host procesador de eventos.


> [!NOTE]
> Este tutorial usa una sola instancia de [EventProcessorHost][EventProcessorHost]. tooincrease rendimiento, se recomienda ejecutar varias instancias de [EventProcessorHost][EventProcessorHost], tal y como se muestra en hello [escala espera de procesamiento de eventos] [escala espera de procesamiento de eventos] ejemplo. En esos casos, hello diversas instancias automáticamente coordinan entre sí eventos de tooload saldo Hola recibido. Si desea que el proceso de varios receptores tooeach *todos los* Hola eventos, debe usar hello **ConsumerGroup** concepto. Cuando se reciben eventos de equipos diferentes, podría ser útil toospecify nombres para [EventProcessorHost] [ EventProcessorHost] instancias basadas en máquinas de hello (o roles) en que se implementan. Para obtener más información acerca de estos temas, vea hello [información general de los centros de eventos] [ Event Hubs overview] hello y [Guía de programación de los centros de eventos] [ Event Hubs Programming Guide] temas.
> 
> 

## <a name="next-steps"></a>Pasos siguientes

Ahora que ha creado una aplicación que crea un centro de eventos y envía y recibe datos, puede aprender más visitando Hola siguientes vínculos:

* [Event​Processor​Host Class][Event Processor Host] (Clase EventProcessor​Host)
* [Información general de Event Hubs][Event Hubs overview]
* [Preguntas más frecuentes sobre Event Hubs](event-hubs-faq.md)

<!-- Images. -->
[19]: ./media/event-hubs-csharp-ephcs-getstarted/create-eh-proj1.png
[20]: ./media/event-hubs-csharp-ephcs-getstarted/create-eh-proj2.png
[21]: ./media/event-hubs-csharp-ephcs-getstarted/run-csharp-ephcs1.png
[22]: ./media/event-hubs-csharp-ephcs-getstarted/run-csharp-ephcs2.png

<!-- Links -->
[EventProcessorHost]: https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost
[Event Hubs overview]: event-hubs-what-is-event-hubs.md
[Scale out Event Processing with Event Hubs]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3
[Event Hubs Programming Guide]: event-hubs-programming-guide.md
[Azure Storage account]:../storage/common/storage-create-storage-account.md
[Event Processor Host]: /dotnet/api/microsoft.servicebus.messaging.eventprocessorhost
[Azure portal]: https://portal.azure.com
