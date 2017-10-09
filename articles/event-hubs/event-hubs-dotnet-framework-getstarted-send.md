---
title: los concentradores de eventos de aaaSend eventos tooAzure con Hola .NET Framework | Documentos de Microsoft
description: Empezar a enviar los eventos de centros de tooEvent con hello .NET Framework
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
ms.openlocfilehash: 05514546a6094096e4a3c800db058190076de80a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="send-events-tooazure-event-hubs-using-hello-net-framework"></a>Enviar eventos tooAzure centros de eventos mediante Hola .NET Framework

## <a name="introduction"></a>Introducción

Event Hubs es un servicio que procesa grandes cantidades de datos de eventos (telemetría) desde aplicaciones y dispositivos conectados. Después de recopilar datos en los centros de eventos, puede almacenar datos de hello mediante un clúster de almacenamiento o transformar mediante un proveedor de análisis en tiempo real. Esta capacidad de procesamiento y la colección de eventos a gran escala es un componente clave de arquitecturas de aplicación moderna incluidos Hola Internet de las cosas (IoT).

Este tutorial se muestra cómo hello toouse [portal de Azure](https://portal.azure.com) toocreate un concentrador de eventos. También muestra cómo el concentrador de eventos de tooan toosend eventos mediante una aplicación de consola escrita en C# con Hola .NET Framework. eventos de tooreceive mediante Hola .NET Framework, vea hello [recibir eventos mediante .NET Framework hello](event-hubs-dotnet-framework-getstarted-receive-eph.md) artículo o haga clic en idioma apropiado de recepción hello en tabla izquierda de Hola de contenido.

toocomplete este tutorial, necesita Hola siguiendo los requisitos previos:

* [Microsoft Visual Studio 2015 o una versión superior](http://visualstudio.com). capturas de pantalla de Hello en este tutorial utilizan Visual Studio de 2017.
* Una cuenta de Azure activa. En caso de no tener ninguna, puede crear una cuenta gratuita en tan solo unos minutos. Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/free/).

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a>Creación de un espacio de nombres de Event Hubs y un centro de eventos

Hola primer paso es hello toouse [portal de Azure](https://portal.azure.com) toocreate un espacio de nombres del tipo centros de eventos y obtener Hola credenciales de administración de la aplicación necesita toocommunicate con el concentrador de eventos de Hola. toocreate un espacio de nombres y el concentrador de eventos, siga el procedimiento de hello en [este artículo](event-hubs-create.md), a continuación, continúe con hello sigue los pasos de este tutorial.

## <a name="create-a-sender-console-application"></a>Creación de una aplicación de consola de remitente

En esta sección, se escribirá una aplicación de consola de Windows que envía el concentrador de eventos de tooyour de eventos.

1. En Visual Studio, cree un nuevo proyecto de aplicación de escritorio de Visual C# con hello **aplicación de consola** plantilla de proyecto. Proyecto de hello Name **remitente**.
   
    ![](./media/event-hubs-dotnet-framework-getstarted-send/create-sender-csharp1.png)
2. En el Explorador de soluciones, haga clic en hello **remitente** del proyecto y, a continuación, haga clic en **administrar paquetes de NuGet para la solución**. 
3. Haga clic en hello **examinar** y, después, busque `Microsoft Azure Service Bus`. Haga clic en **instalar**y acepte los términos de Hola de uso. 
   
    ![](./media/event-hubs-dotnet-framework-getstarted-send/create-sender-csharp2.png)
   
    Visual Studio descarga, instala y agrega una referencia toohello [paquete de NuGet de biblioteca de Service Bus de Azure](https://www.nuget.org/packages/WindowsAzure.ServiceBus).
4. Agregue los siguiente hello `using` las instrucciones en la parte superior de Hola de hello **Program.cs** archivo:
   
  ```csharp
  using System.Threading;
  using Microsoft.ServiceBus.Messaging;
  ```
5. Agregar Hola después campos toohello **programa** (clase), sustituyendo los valores de marcador de posición de Hola por nombre de Hola de concentrador de eventos de Hola que creó en la sección anterior de Hola y cadena de conexión en el nivel de espacio de nombres de Hola que guardó anteriormente.
   
  ```csharp
  static string eventHubName = "{Event Hub name}";
  static string connectionString = "{send connection string}";
  ```
6. Agregar Hola siguiendo el método toohello **programa** clase:
   
  ```csharp
  static void SendingRandomMessages()
  {
      var eventHubClient = EventHubClient.CreateFromConnectionString(connectionString, eventHubName);
      while (true)
      {
          try
          {
              var message = Guid.NewGuid().ToString();
              Console.WriteLine("{0} > Sending message: {1}", DateTime.Now, message);
              eventHubClient.Send(new EventData(Encoding.UTF8.GetBytes(message)));
          }
          catch (Exception exception)
          {
              Console.ForegroundColor = ConsoleColor.Red;
              Console.WriteLine("{0} > Exception: {1}", DateTime.Now, exception.Message);
              Console.ResetColor();
          }
   
          Thread.Sleep(200);
      }
  }
  ```
   
  Este método envía continuamente concentrador de eventos de tooyour de eventos con un retraso de ms de 200.
7. Por último, agregue Hola después líneas toohello **Main** método:
   
  ```csharp
  Console.WriteLine("Press Ctrl-C toostop hello sender process");
  Console.WriteLine("Press Enter toostart now");
  Console.ReadLine();
  SendingRandomMessages();
  ```
8. Ejecutar programa hello y asegúrese de que no hay ningún error.
  
¡Enhorabuena! Ahora ha enviado el concentrador de eventos de tooan de mensajes.

## <a name="next-steps"></a>Pasos siguientes
Ahora que ha creado una aplicación que crea un centro de eventos y envía los datos, puede mover en toohello los escenarios siguientes:

* [Recibir eventos mediante Hola Host procesador de eventos](event-hubs-dotnet-framework-getstarted-receive-eph.md)
* [Referencia del Host del procesador de eventos](/dotnet/api/microsoft.servicebus.messaging.eventprocessorhost)
* [Información general de Event Hubs](event-hubs-what-is-event-hubs.md)

<!-- Images. -->
[19]: ./media/event-hubs-csharp-ephcs-getstarted/create-eh-proj1.png
[20]: ./media/event-hubs-csharp-ephcs-getstarted/create-eh-proj2.png
[21]: ./media/event-hubs-csharp-ephcs-getstarted/run-csharp-ephcs1.png
[22]: ./media/event-hubs-csharp-ephcs-getstarted/run-csharp-ephcs2.png

