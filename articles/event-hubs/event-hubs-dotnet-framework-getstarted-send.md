---
title: "Envío de eventos a Azure Event Hubs mediante .NET Framework | Microsoft Docs"
description: "Introducción al envío de eventos a Event Hubs mediante .NET Framework"
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
ms.openlocfilehash: 4eb0e7bcc14722010121c2a5945509d6ed736f4f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="send-events-to-azure-event-hubs-using-the-net-framework"></a><span data-ttu-id="1f955-103">Envío de eventos a Azure Event Hubs mediante .NET Framework</span><span class="sxs-lookup"><span data-stu-id="1f955-103">Send events to Azure Event Hubs using the .NET Framework</span></span>

## <a name="introduction"></a><span data-ttu-id="1f955-104">Introducción</span><span class="sxs-lookup"><span data-stu-id="1f955-104">Introduction</span></span>

<span data-ttu-id="1f955-105">Event Hubs es un servicio que procesa grandes cantidades de datos de eventos (telemetría) desde aplicaciones y dispositivos conectados.</span><span class="sxs-lookup"><span data-stu-id="1f955-105">Event Hubs is a service that processes large amounts of event data (telemetry) from connected devices and applications.</span></span> <span data-ttu-id="1f955-106">Después de recopilar datos en Centros de eventos, puede almacenarlos mediante un clúster de almacenamiento o transformarlos por medio de un proveedor de análisis en tiempo real.</span><span class="sxs-lookup"><span data-stu-id="1f955-106">After you collect data into Event Hubs, you can store the data using a storage cluster or transform it using a real-time analytics provider.</span></span> <span data-ttu-id="1f955-107">Esta funcionalidad de recopilación y procesamiento de eventos a gran escala es un componente clave de las modernas arquitecturas de aplicaciones, entre las que se incluye Internet de las cosas (IoT).</span><span class="sxs-lookup"><span data-stu-id="1f955-107">This large-scale event collection and processing capability is a key component of modern application architectures including the Internet of Things (IoT).</span></span>

<span data-ttu-id="1f955-108">En este tutorial se muestra cómo usar [Azure Portal](https://portal.azure.com) para crear un centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="1f955-108">This tutorial shows how to use the [Azure portal](https://portal.azure.com) to create an event hub.</span></span> <span data-ttu-id="1f955-109">También muestra cómo enviar eventos a un centro de eventos mediante una aplicación de consola escrita en C# con .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="1f955-109">It also shows how to send events to an event hub using a console application written in C# using the .NET Framework.</span></span> <span data-ttu-id="1f955-110">Para recibir eventos mediante .NET Framework, consulte el artículo [Get started with Event Hubs using the .NET Framework](event-hubs-dotnet-framework-getstarted-receive-eph.md) (Introducción al uso de .NET Framework por parte de Event Hubs) o haga clic en el idioma de recepción correspondiente en la tabla de contenido de la izquierda.</span><span class="sxs-lookup"><span data-stu-id="1f955-110">To receive events using the .NET Framework, see the [Receive events using the .NET Framework](event-hubs-dotnet-framework-getstarted-receive-eph.md) article, or click the appropriate receiving language in the left-hand table of contents.</span></span>

<span data-ttu-id="1f955-111">Para completar este tutorial, debe cumplir los siguientes requisitos previos:</span><span class="sxs-lookup"><span data-stu-id="1f955-111">To complete this tutorial, you need the following prerequisites:</span></span>

* <span data-ttu-id="1f955-112">[Microsoft Visual Studio 2015 o una versión superior](http://visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="1f955-112">[Microsoft Visual Studio 2015 or higher](http://visualstudio.com).</span></span> <span data-ttu-id="1f955-113">En las capturas de pantalla de este tutorial se usa Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="1f955-113">The screen shots in this tutorial use Visual Studio 2017.</span></span>
* <span data-ttu-id="1f955-114">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="1f955-114">An active Azure account.</span></span> <span data-ttu-id="1f955-115">En caso de no tener ninguna, puede crear una cuenta gratuita en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="1f955-115">If you don't have one, you can create a free account in just a couple of minutes.</span></span> <span data-ttu-id="1f955-116">Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="1f955-116">For details, see [Azure Free Trial](https://azure.microsoft.com/free/).</span></span>

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a><span data-ttu-id="1f955-117">Creación de un espacio de nombres de Event Hubs y un centro de eventos</span><span class="sxs-lookup"><span data-stu-id="1f955-117">Create an Event Hubs namespace and an event hub</span></span>

<span data-ttu-id="1f955-118">El primer paso consiste en usar [Azure Portal](https://portal.azure.com) para crear un espacio de nombres de tipo Event Hubs y obtener las credenciales de administración que la aplicación necesita para comunicarse con el centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="1f955-118">The first step is to use the [Azure portal](https://portal.azure.com) to create a namespace of type Event Hubs, and obtain the management credentials your application needs to communicate with the event hub.</span></span> <span data-ttu-id="1f955-119">Para crear un espacio de nombres y un centro de eventos, siga el procedimiento de [este artículo](event-hubs-create.md) y después continúe con los siguientes pasos siguientes del tutorial.</span><span class="sxs-lookup"><span data-stu-id="1f955-119">To create a namespace and event hub, follow the procedure in [this article](event-hubs-create.md), then proceed with the following steps in this tutorial.</span></span>

## <a name="create-a-sender-console-application"></a><span data-ttu-id="1f955-120">Creación de una aplicación de consola de remitente</span><span class="sxs-lookup"><span data-stu-id="1f955-120">Create a sender console application</span></span>

<span data-ttu-id="1f955-121">En esta sección se escribirá una aplicación de consola Windows que envía eventos al centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="1f955-121">In this section, you'll write a Windows console app that sends events to your event hub.</span></span>

1. <span data-ttu-id="1f955-122">En Visual Studio, cree un nuevo proyecto de aplicación de escritorio de Visual C# con la plantilla de proyecto **Aplicación de consola** .</span><span class="sxs-lookup"><span data-stu-id="1f955-122">In Visual Studio, create a new Visual C# Desktop App project using the **Console Application** project template.</span></span> <span data-ttu-id="1f955-123">Asigne al proyecto el nombre **Remitente**.</span><span class="sxs-lookup"><span data-stu-id="1f955-123">Name the project **Sender**.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-send/create-sender-csharp1.png)
2. <span data-ttu-id="1f955-124">En el Explorador de soluciones, haga clic con el botón derecho en el proyecto **Remitente** y luego haga clic en **Administrar paquetes NuGet para la solución**.</span><span class="sxs-lookup"><span data-stu-id="1f955-124">In Solution Explorer, right-click the **Sender** project, and then click **Manage NuGet Packages for Solution**.</span></span> 
3. <span data-ttu-id="1f955-125">Haga clic en la pestaña **Examinar** y luego busque `Microsoft Azure Service Bus`.</span><span class="sxs-lookup"><span data-stu-id="1f955-125">Click the **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="1f955-126">Haga clic en **Instalar**y acepte las condiciones de uso.</span><span class="sxs-lookup"><span data-stu-id="1f955-126">Click **Install**, and accept the terms of use.</span></span> 
   
    ![](./media/event-hubs-dotnet-framework-getstarted-send/create-sender-csharp2.png)
   
    <span data-ttu-id="1f955-127">Visual Studio descarga, instala y agrega una referencia al [paquete NuGet de la biblioteca del Bus de servicio de Azure](https://www.nuget.org/packages/WindowsAzure.ServiceBus).</span><span class="sxs-lookup"><span data-stu-id="1f955-127">Visual Studio downloads, installs, and adds a reference to the [Azure Service Bus library NuGet package](https://www.nuget.org/packages/WindowsAzure.ServiceBus).</span></span>
4. <span data-ttu-id="1f955-128">Agregue las siguientes instrucciones `using` al principio del archivo **Program.cs** :</span><span class="sxs-lookup"><span data-stu-id="1f955-128">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
  ```csharp
  using System.Threading;
  using Microsoft.ServiceBus.Messaging;
  ```
5. <span data-ttu-id="1f955-129">Agregue los siguientes campos a la clase **Program**; para ello, sustituya los valores del marcador de posición por el nombre del centro de eventos creado en la sección anterior y la cadena de conexión de nivel del espacio de nombres que ha guardado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="1f955-129">Add the following fields to the **Program** class, substituting the placeholder values with the name of the event hub you created in the previous section, and the namespace-level connection string you saved previously.</span></span>
   
  ```csharp
  static string eventHubName = "{Event Hub name}";
  static string connectionString = "{send connection string}";
  ```
6. <span data-ttu-id="1f955-130">Agregue el método siguiente a la clase **Program** :</span><span class="sxs-lookup"><span data-stu-id="1f955-130">Add the following method to the **Program** class:</span></span>
   
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
   
  <span data-ttu-id="1f955-131">Este método envía continuamente los eventos al centro de eventos con un retraso de 200 ms.</span><span class="sxs-lookup"><span data-stu-id="1f955-131">This method continuously sends events to your event hub with a 200-ms delay.</span></span>
7. <span data-ttu-id="1f955-132">Por último, agregue las líneas siguientes al método **Main** :</span><span class="sxs-lookup"><span data-stu-id="1f955-132">Finally, add the following lines to the **Main** method:</span></span>
   
  ```csharp
  Console.WriteLine("Press Ctrl-C to stop the sender process");
  Console.WriteLine("Press Enter to start now");
  Console.ReadLine();
  SendingRandomMessages();
  ```
8. <span data-ttu-id="1f955-133">Ejecute el programa y asegúrese de que no hay ningún error.</span><span class="sxs-lookup"><span data-stu-id="1f955-133">Run the program, and ensure that there are no errors.</span></span>
  
<span data-ttu-id="1f955-134">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="1f955-134">Congratulations!</span></span> <span data-ttu-id="1f955-135">Ha enviado mensajes a un centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="1f955-135">You have now sent messages to an event hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1f955-136">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1f955-136">Next steps</span></span>
<span data-ttu-id="1f955-137">Ahora que ha creado una aplicación de trabajo que crea un centro de eventos y envía datos, puede pasar a los siguientes escenarios:</span><span class="sxs-lookup"><span data-stu-id="1f955-137">Now that you've built a working application that creates an event hub and sends data, you can move on to the following scenarios:</span></span>

* [<span data-ttu-id="1f955-138">Recepción de eventos mediante el Host de procesador de eventos</span><span class="sxs-lookup"><span data-stu-id="1f955-138">Receive events using the Event Processor Host</span></span>](event-hubs-dotnet-framework-getstarted-receive-eph.md)
* [<span data-ttu-id="1f955-139">Referencia del Host del procesador de eventos</span><span class="sxs-lookup"><span data-stu-id="1f955-139">Event Processor Host reference</span></span>](/dotnet/api/microsoft.servicebus.messaging.eventprocessorhost)
* [<span data-ttu-id="1f955-140">Información general de Event Hubs</span><span class="sxs-lookup"><span data-stu-id="1f955-140">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)

<!-- Images. -->
[19]: ./media/event-hubs-csharp-ephcs-getstarted/create-eh-proj1.png
[20]: ./media/event-hubs-csharp-ephcs-getstarted/create-eh-proj2.png
[21]: ./media/event-hubs-csharp-ephcs-getstarted/run-csharp-ephcs1.png
[22]: ./media/event-hubs-csharp-ephcs-getstarted/run-csharp-ephcs2.png

