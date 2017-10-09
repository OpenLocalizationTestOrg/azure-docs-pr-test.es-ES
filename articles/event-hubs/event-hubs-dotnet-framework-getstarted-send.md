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
# <a name="send-events-tooazure-event-hubs-using-hello-net-framework"></a><span data-ttu-id="4a492-103">Enviar eventos tooAzure centros de eventos mediante Hola .NET Framework</span><span class="sxs-lookup"><span data-stu-id="4a492-103">Send events tooAzure Event Hubs using hello .NET Framework</span></span>

## <a name="introduction"></a><span data-ttu-id="4a492-104">Introducción</span><span class="sxs-lookup"><span data-stu-id="4a492-104">Introduction</span></span>

<span data-ttu-id="4a492-105">Event Hubs es un servicio que procesa grandes cantidades de datos de eventos (telemetría) desde aplicaciones y dispositivos conectados.</span><span class="sxs-lookup"><span data-stu-id="4a492-105">Event Hubs is a service that processes large amounts of event data (telemetry) from connected devices and applications.</span></span> <span data-ttu-id="4a492-106">Después de recopilar datos en los centros de eventos, puede almacenar datos de hello mediante un clúster de almacenamiento o transformar mediante un proveedor de análisis en tiempo real.</span><span class="sxs-lookup"><span data-stu-id="4a492-106">After you collect data into Event Hubs, you can store hello data using a storage cluster or transform it using a real-time analytics provider.</span></span> <span data-ttu-id="4a492-107">Esta capacidad de procesamiento y la colección de eventos a gran escala es un componente clave de arquitecturas de aplicación moderna incluidos Hola Internet de las cosas (IoT).</span><span class="sxs-lookup"><span data-stu-id="4a492-107">This large-scale event collection and processing capability is a key component of modern application architectures including hello Internet of Things (IoT).</span></span>

<span data-ttu-id="4a492-108">Este tutorial se muestra cómo hello toouse [portal de Azure](https://portal.azure.com) toocreate un concentrador de eventos.</span><span class="sxs-lookup"><span data-stu-id="4a492-108">This tutorial shows how toouse hello [Azure portal](https://portal.azure.com) toocreate an event hub.</span></span> <span data-ttu-id="4a492-109">También muestra cómo el concentrador de eventos de tooan toosend eventos mediante una aplicación de consola escrita en C# con Hola .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="4a492-109">It also shows how toosend events tooan event hub using a console application written in C# using hello .NET Framework.</span></span> <span data-ttu-id="4a492-110">eventos de tooreceive mediante Hola .NET Framework, vea hello [recibir eventos mediante .NET Framework hello](event-hubs-dotnet-framework-getstarted-receive-eph.md) artículo o haga clic en idioma apropiado de recepción hello en tabla izquierda de Hola de contenido.</span><span class="sxs-lookup"><span data-stu-id="4a492-110">tooreceive events using hello .NET Framework, see hello [Receive events using hello .NET Framework](event-hubs-dotnet-framework-getstarted-receive-eph.md) article, or click hello appropriate receiving language in hello left-hand table of contents.</span></span>

<span data-ttu-id="4a492-111">toocomplete este tutorial, necesita Hola siguiendo los requisitos previos:</span><span class="sxs-lookup"><span data-stu-id="4a492-111">toocomplete this tutorial, you need hello following prerequisites:</span></span>

* <span data-ttu-id="4a492-112">[Microsoft Visual Studio 2015 o una versión superior](http://visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="4a492-112">[Microsoft Visual Studio 2015 or higher](http://visualstudio.com).</span></span> <span data-ttu-id="4a492-113">capturas de pantalla de Hello en este tutorial utilizan Visual Studio de 2017.</span><span class="sxs-lookup"><span data-stu-id="4a492-113">hello screen shots in this tutorial use Visual Studio 2017.</span></span>
* <span data-ttu-id="4a492-114">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="4a492-114">An active Azure account.</span></span> <span data-ttu-id="4a492-115">En caso de no tener ninguna, puede crear una cuenta gratuita en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="4a492-115">If you don't have one, you can create a free account in just a couple of minutes.</span></span> <span data-ttu-id="4a492-116">Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="4a492-116">For details, see [Azure Free Trial](https://azure.microsoft.com/free/).</span></span>

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a><span data-ttu-id="4a492-117">Creación de un espacio de nombres de Event Hubs y un centro de eventos</span><span class="sxs-lookup"><span data-stu-id="4a492-117">Create an Event Hubs namespace and an event hub</span></span>

<span data-ttu-id="4a492-118">Hola primer paso es hello toouse [portal de Azure](https://portal.azure.com) toocreate un espacio de nombres del tipo centros de eventos y obtener Hola credenciales de administración de la aplicación necesita toocommunicate con el concentrador de eventos de Hola.</span><span class="sxs-lookup"><span data-stu-id="4a492-118">hello first step is toouse hello [Azure portal](https://portal.azure.com) toocreate a namespace of type Event Hubs, and obtain hello management credentials your application needs toocommunicate with hello event hub.</span></span> <span data-ttu-id="4a492-119">toocreate un espacio de nombres y el concentrador de eventos, siga el procedimiento de hello en [este artículo](event-hubs-create.md), a continuación, continúe con hello sigue los pasos de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="4a492-119">toocreate a namespace and event hub, follow hello procedure in [this article](event-hubs-create.md), then proceed with hello following steps in this tutorial.</span></span>

## <a name="create-a-sender-console-application"></a><span data-ttu-id="4a492-120">Creación de una aplicación de consola de remitente</span><span class="sxs-lookup"><span data-stu-id="4a492-120">Create a sender console application</span></span>

<span data-ttu-id="4a492-121">En esta sección, se escribirá una aplicación de consola de Windows que envía el concentrador de eventos de tooyour de eventos.</span><span class="sxs-lookup"><span data-stu-id="4a492-121">In this section, you'll write a Windows console app that sends events tooyour event hub.</span></span>

1. <span data-ttu-id="4a492-122">En Visual Studio, cree un nuevo proyecto de aplicación de escritorio de Visual C# con hello **aplicación de consola** plantilla de proyecto.</span><span class="sxs-lookup"><span data-stu-id="4a492-122">In Visual Studio, create a new Visual C# Desktop App project using hello **Console Application** project template.</span></span> <span data-ttu-id="4a492-123">Proyecto de hello Name **remitente**.</span><span class="sxs-lookup"><span data-stu-id="4a492-123">Name hello project **Sender**.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-send/create-sender-csharp1.png)
2. <span data-ttu-id="4a492-124">En el Explorador de soluciones, haga clic en hello **remitente** del proyecto y, a continuación, haga clic en **administrar paquetes de NuGet para la solución**.</span><span class="sxs-lookup"><span data-stu-id="4a492-124">In Solution Explorer, right-click hello **Sender** project, and then click **Manage NuGet Packages for Solution**.</span></span> 
3. <span data-ttu-id="4a492-125">Haga clic en hello **examinar** y, después, busque `Microsoft Azure Service Bus`.</span><span class="sxs-lookup"><span data-stu-id="4a492-125">Click hello **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="4a492-126">Haga clic en **instalar**y acepte los términos de Hola de uso.</span><span class="sxs-lookup"><span data-stu-id="4a492-126">Click **Install**, and accept hello terms of use.</span></span> 
   
    ![](./media/event-hubs-dotnet-framework-getstarted-send/create-sender-csharp2.png)
   
    <span data-ttu-id="4a492-127">Visual Studio descarga, instala y agrega una referencia toohello [paquete de NuGet de biblioteca de Service Bus de Azure](https://www.nuget.org/packages/WindowsAzure.ServiceBus).</span><span class="sxs-lookup"><span data-stu-id="4a492-127">Visual Studio downloads, installs, and adds a reference toohello [Azure Service Bus library NuGet package](https://www.nuget.org/packages/WindowsAzure.ServiceBus).</span></span>
4. <span data-ttu-id="4a492-128">Agregue los siguiente hello `using` las instrucciones en la parte superior de Hola de hello **Program.cs** archivo:</span><span class="sxs-lookup"><span data-stu-id="4a492-128">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
  ```csharp
  using System.Threading;
  using Microsoft.ServiceBus.Messaging;
  ```
5. <span data-ttu-id="4a492-129">Agregar Hola después campos toohello **programa** (clase), sustituyendo los valores de marcador de posición de Hola por nombre de Hola de concentrador de eventos de Hola que creó en la sección anterior de Hola y cadena de conexión en el nivel de espacio de nombres de Hola que guardó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="4a492-129">Add hello following fields toohello **Program** class, substituting hello placeholder values with hello name of hello event hub you created in hello previous section, and hello namespace-level connection string you saved previously.</span></span>
   
  ```csharp
  static string eventHubName = "{Event Hub name}";
  static string connectionString = "{send connection string}";
  ```
6. <span data-ttu-id="4a492-130">Agregar Hola siguiendo el método toohello **programa** clase:</span><span class="sxs-lookup"><span data-stu-id="4a492-130">Add hello following method toohello **Program** class:</span></span>
   
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
   
  <span data-ttu-id="4a492-131">Este método envía continuamente concentrador de eventos de tooyour de eventos con un retraso de ms de 200.</span><span class="sxs-lookup"><span data-stu-id="4a492-131">This method continuously sends events tooyour event hub with a 200-ms delay.</span></span>
7. <span data-ttu-id="4a492-132">Por último, agregue Hola después líneas toohello **Main** método:</span><span class="sxs-lookup"><span data-stu-id="4a492-132">Finally, add hello following lines toohello **Main** method:</span></span>
   
  ```csharp
  Console.WriteLine("Press Ctrl-C toostop hello sender process");
  Console.WriteLine("Press Enter toostart now");
  Console.ReadLine();
  SendingRandomMessages();
  ```
8. <span data-ttu-id="4a492-133">Ejecutar programa hello y asegúrese de que no hay ningún error.</span><span class="sxs-lookup"><span data-stu-id="4a492-133">Run hello program, and ensure that there are no errors.</span></span>
  
<span data-ttu-id="4a492-134">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="4a492-134">Congratulations!</span></span> <span data-ttu-id="4a492-135">Ahora ha enviado el concentrador de eventos de tooan de mensajes.</span><span class="sxs-lookup"><span data-stu-id="4a492-135">You have now sent messages tooan event hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4a492-136">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4a492-136">Next steps</span></span>
<span data-ttu-id="4a492-137">Ahora que ha creado una aplicación que crea un centro de eventos y envía los datos, puede mover en toohello los escenarios siguientes:</span><span class="sxs-lookup"><span data-stu-id="4a492-137">Now that you've built a working application that creates an event hub and sends data, you can move on toohello following scenarios:</span></span>

* [<span data-ttu-id="4a492-138">Recibir eventos mediante Hola Host procesador de eventos</span><span class="sxs-lookup"><span data-stu-id="4a492-138">Receive events using hello Event Processor Host</span></span>](event-hubs-dotnet-framework-getstarted-receive-eph.md)
* [<span data-ttu-id="4a492-139">Referencia del Host del procesador de eventos</span><span class="sxs-lookup"><span data-stu-id="4a492-139">Event Processor Host reference</span></span>](/dotnet/api/microsoft.servicebus.messaging.eventprocessorhost)
* [<span data-ttu-id="4a492-140">Información general de Event Hubs</span><span class="sxs-lookup"><span data-stu-id="4a492-140">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)

<!-- Images. -->
[19]: ./media/event-hubs-csharp-ephcs-getstarted/create-eh-proj1.png
[20]: ./media/event-hubs-csharp-ephcs-getstarted/create-eh-proj2.png
[21]: ./media/event-hubs-csharp-ephcs-getstarted/run-csharp-ephcs1.png
[22]: ./media/event-hubs-csharp-ephcs-getstarted/run-csharp-ephcs2.png

