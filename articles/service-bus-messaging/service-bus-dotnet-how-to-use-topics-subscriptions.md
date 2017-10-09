---
title: aaaGet a trabajar con temas de Service Bus de Azure y las suscripciones | Documentos de Microsoft
description: "Escriba una aplicación de consola en C# que use los temas y las suscripciones de mensajería de Service Bus."
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: hero-article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 06/30/2017
ms.author: sethm
ms.openlocfilehash: 619d602599d97ecff2ded0681a383b19f1a8b7ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-service-bus-topics"></a><span data-ttu-id="5a5ea-103">Introducción a las colas de Service Bus</span><span class="sxs-lookup"><span data-stu-id="5a5ea-103">Get started with Service Bus topics</span></span>

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

## <a name="what-will-be-accomplished"></a><span data-ttu-id="5a5ea-104">Lo que se logrará</span><span class="sxs-lookup"><span data-stu-id="5a5ea-104">What will be accomplished</span></span>

<span data-ttu-id="5a5ea-105">Este tutorial trata Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="5a5ea-105">This tutorial covers hello following steps:</span></span>

1. <span data-ttu-id="5a5ea-106">Crear un espacio de nombres de Bus de servicio, mediante Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="5a5ea-106">Create a Service Bus namespace, using hello Azure portal.</span></span>
2. <span data-ttu-id="5a5ea-107">Crear un tema de Bus de servicio, mediante Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="5a5ea-107">Create a Service Bus topic, using hello Azure portal.</span></span>
3. <span data-ttu-id="5a5ea-108">Crear un tema de toothat de la suscripción de Bus de servicio, mediante Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="5a5ea-108">Create a Service Bus subscription toothat topic, using hello Azure portal.</span></span>
4. <span data-ttu-id="5a5ea-109">Escribir una toosend de aplicación de consola en un tema de toohello de mensaje.</span><span class="sxs-lookup"><span data-stu-id="5a5ea-109">Write a console application toosend a message toohello topic.</span></span>
5. <span data-ttu-id="5a5ea-110">Escribir una tooreceive de aplicación de consola que el mensaje de suscripción de Hola.</span><span class="sxs-lookup"><span data-stu-id="5a5ea-110">Write a console application tooreceive that message from hello subscription.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5a5ea-111">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="5a5ea-111">Prerequisites</span></span>

1. <span data-ttu-id="5a5ea-112">[Visual Studio 2015 o posterior](http://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="5a5ea-112">[Visual Studio 2015 or higher](http://www.visualstudio.com).</span></span> <span data-ttu-id="5a5ea-113">ejemplos de Hello en este tutorial utiliza Visual Studio de 2017.</span><span class="sxs-lookup"><span data-stu-id="5a5ea-113">hello examples in this tutorial use Visual Studio 2017.</span></span>
2. <span data-ttu-id="5a5ea-114">Una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="5a5ea-114">An Azure subscription.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-hello-azure-portal"></a><span data-ttu-id="5a5ea-115">1. Crear un espacio de nombres mediante Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="5a5ea-115">1. Create a namespace using hello Azure portal</span></span>

<span data-ttu-id="5a5ea-116">Si ya ha creado un espacio de nombres de mensajería de Bus de servicio, consulte el toohello [crear un tema mediante el portal de Azure hello](#2-create-a-topic-using-the-azure-portal) sección.</span><span class="sxs-lookup"><span data-stu-id="5a5ea-116">If you have already created a Service Bus Messaging namespace, jump toohello [Create a topic using hello Azure portal](#2-create-a-topic-using-the-azure-portal) section.</span></span>

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="2-create-a-topic-using-hello-azure-portal"></a><span data-ttu-id="5a5ea-117">2. Crear un tema mediante Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="5a5ea-117">2. Create a topic using hello Azure portal</span></span>

1. <span data-ttu-id="5a5ea-118">Inicie sesión en toohello [portal de Azure][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="5a5ea-118">Log on toohello [Azure portal][azure-portal].</span></span>
2. <span data-ttu-id="5a5ea-119">En el panel de navegación izquierdo de hello del portal de hello, haga clic en **Service Bus** (si no ve **Service Bus**, haga clic en **más servicios**).</span><span class="sxs-lookup"><span data-stu-id="5a5ea-119">In hello left navigation pane of hello portal, click **Service Bus** (if you don't see **Service Bus**, click **More services**).</span></span>
3. <span data-ttu-id="5a5ea-120">Haga clic en el espacio de nombres de hello en el que le gustaría tema de hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="5a5ea-120">Click hello namespace in which you would like toocreate hello topic.</span></span> <span data-ttu-id="5a5ea-121">aparece la hoja de información general del espacio de nombres de Hello:</span><span class="sxs-lookup"><span data-stu-id="5a5ea-121">hello namespace overview blade appears:</span></span>
   
    ![de un tema][createtopic1]
4. <span data-ttu-id="5a5ea-123">Hola **espacio de nombres de Bus de servicio** hoja, haga clic en **temas**, a continuación, haga clic en **Agregar tema**.</span><span class="sxs-lookup"><span data-stu-id="5a5ea-123">In hello **Service Bus namespace** blade, click **Topics**, then click **Add topic**.</span></span>
   
    ![Seleccionar temas][createtopic2]
5. <span data-ttu-id="5a5ea-125">Escriba un nombre para el tema de Hola y desactive la opción hello **habilitar las particiones** opción.</span><span class="sxs-lookup"><span data-stu-id="5a5ea-125">Enter a name for hello topic, and uncheck hello **Enable partitioning** option.</span></span> <span data-ttu-id="5a5ea-126">Deje Hola otras opciones con sus valores predeterminados.</span><span class="sxs-lookup"><span data-stu-id="5a5ea-126">Leave hello other options with their default values.</span></span>
   
    ![Seleccionar Nuevo][createtopic3]
6. <span data-ttu-id="5a5ea-128">En la parte inferior de Hola de hoja de hello, haga clic en **crear**.</span><span class="sxs-lookup"><span data-stu-id="5a5ea-128">At hello bottom of hello blade, click **Create**.</span></span>

## <a name="3-create-a-subscription-toohello-topic"></a><span data-ttu-id="5a5ea-129">3. Crear un tema de toohello de suscripción</span><span class="sxs-lookup"><span data-stu-id="5a5ea-129">3. Create a subscription toohello topic</span></span>

1. <span data-ttu-id="5a5ea-130">En panel de recursos del portal de hello, haga clic en el espacio de nombres de Hola que creó en el paso 1 y luego haga clic en el nombre del tema de Hola que creó en el paso 2.</span><span class="sxs-lookup"><span data-stu-id="5a5ea-130">In hello portal resources pane, click hello namespace you created in step 1, then click name of hello topic you created in step 2.</span></span>
2. <span data-ttu-id="5a5ea-131">Un principio Hola del panel de información general de hello, haga clic en hello además de iniciar sesión a continuación demasiado**suscripción** tooadd un tema de toothis de suscripción.</span><span class="sxs-lookup"><span data-stu-id="5a5ea-131">A hello top of hello overview pane, click hello plus sign next too**Subscription** tooadd a subscription toothis topic.</span></span>

    ![Creación de una suscripción][createtopic4]

3. <span data-ttu-id="5a5ea-133">Escriba un nombre para la suscripción de Hola.</span><span class="sxs-lookup"><span data-stu-id="5a5ea-133">Enter a name for hello subscription.</span></span> <span data-ttu-id="5a5ea-134">Deje Hola otras opciones con sus valores predeterminados.</span><span class="sxs-lookup"><span data-stu-id="5a5ea-134">Leave hello other options with their default values.</span></span>

## <a name="4-send-messages-toohello-topic"></a><span data-ttu-id="5a5ea-135">4. Enviar tema toohello de mensajes</span><span class="sxs-lookup"><span data-stu-id="5a5ea-135">4. Send messages toohello topic</span></span>

<span data-ttu-id="5a5ea-136">tema de toohello de toosend mensajes, se escribe una aplicación de consola de C# con Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5a5ea-136">toosend messages toohello topic, we write a C# console application using Visual Studio.</span></span>

### <a name="create-a-console-application"></a><span data-ttu-id="5a5ea-137">Creación de una aplicación de consola</span><span class="sxs-lookup"><span data-stu-id="5a5ea-137">Create a console application</span></span>

<span data-ttu-id="5a5ea-138">Inicie Visual Studio y cree un nuevo proyecto **Console app (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="5a5ea-138">Launch Visual Studio and create a new **Console app (.NET Framework)** project.</span></span>

### <a name="add-hello-service-bus-nuget-package"></a><span data-ttu-id="5a5ea-139">Agregar paquete de NuGet de Bus de servicio de Hola</span><span class="sxs-lookup"><span data-stu-id="5a5ea-139">Add hello Service Bus NuGet package</span></span>

1. <span data-ttu-id="5a5ea-140">Haga clic en proyecto de hello recién creado y seleccione **administrar paquetes de NuGet**.</span><span class="sxs-lookup"><span data-stu-id="5a5ea-140">Right-click hello newly created project and select **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="5a5ea-141">Haga clic en hello **examinar** ficha, busque **Microsoft Azure Service Bus**y, a continuación, seleccione hello **WindowsAzure.ServiceBus** elemento.</span><span class="sxs-lookup"><span data-stu-id="5a5ea-141">Click hello **Browse** tab, search for **Microsoft Azure Service Bus**, and then select hello **WindowsAzure.ServiceBus** item.</span></span> <span data-ttu-id="5a5ea-142">Haga clic en **instalar** toocomplete Hola instalación, a continuación, cierre este cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5a5ea-142">Click **Install** toocomplete hello installation, then close this dialog box.</span></span>
   
    ![Seleccionar un paquete NuGet][nuget-pkg]

### <a name="write-some-code-toosend-a-message-toohello-topic"></a><span data-ttu-id="5a5ea-144">Escriba algún código toosend un tema de toohello de mensaje</span><span class="sxs-lookup"><span data-stu-id="5a5ea-144">Write some code toosend a message toohello topic</span></span>

1. <span data-ttu-id="5a5ea-145">Agregue los siguiente hello `using` parte superior de toohello de instrucción del archivo Program.cs de Hola.</span><span class="sxs-lookup"><span data-stu-id="5a5ea-145">Add hello following `using` statement toohello top of hello Program.cs file.</span></span>
   
    ```csharp
    using Microsoft.ServiceBus.Messaging;
    ```
2. <span data-ttu-id="5a5ea-146">Agregar Hola después código toohello `Main` método.</span><span class="sxs-lookup"><span data-stu-id="5a5ea-146">Add hello following code toohello `Main` method.</span></span> <span data-ttu-id="5a5ea-147">Conjunto hello `connectionString` cadena de conexión de la variable toohello que se obtuvo al crear el espacio de nombres de Hola y establecer `topicName` toohello nombre que usó al crear tema Hola.</span><span class="sxs-lookup"><span data-stu-id="5a5ea-147">Set hello `connectionString` variable toohello connection string that you obtained when creating hello namespace, and set `topicName` toohello name that you used when creating hello topic.</span></span>
   
    ```csharp
    var connectionString = "<your connection string>";
    var topicName = "<your topic name>";
   
    var client = TopicClient.CreateFromConnectionString(connectionString, topicName);
    var message = new BrokeredMessage("This is a test message!");

    Console.WriteLine(String.Format("Message body: {0}", message.GetBody<String>()));
    Console.WriteLine(String.Format("Message id: {0}", message.MessageId));

    client.Send(message);

    Console.WriteLine("Message successfully sent! Press ENTER tooexit program");
    Console.ReadLine();
    ```
   
    <span data-ttu-id="5a5ea-148">Así debería ser el archivo Program.cs.</span><span class="sxs-lookup"><span data-stu-id="5a5ea-148">Here is what your Program.cs file should look like.</span></span>
   
    ```csharp
    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;
    using Microsoft.ServiceBus.Messaging;

    namespace tsend
    {
        class Program
        {
            static void Main(string[] args)
            {
                var connectionString = "Endpoint=sb://<your namespace>.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=<your key>";
                var topicName = "<your topic name>";

                var client = TopicClient.CreateFromConnectionString(connectionString, topicName);
                var message = new BrokeredMessage("This is a test message!");

                Console.WriteLine(String.Format("Message body: {0}", message.GetBody<String>()));
                Console.WriteLine(String.Format("Message id: {0}", message.MessageId));

                client.Send(message);

                Console.WriteLine("Message successfully sent! Press ENTER tooexit program");
                Console.ReadLine();
            }
        }
    }
    ```
3. <span data-ttu-id="5a5ea-149">Ejecutar programa hello y comprobar Hola portal de Azure: haga clic en nombre de hello del tema en el espacio de nombres de hello **Introducción** hoja.</span><span class="sxs-lookup"><span data-stu-id="5a5ea-149">Run hello program, and check hello Azure portal: click hello name of your topic in hello namespace **Overview** blade.</span></span> <span data-ttu-id="5a5ea-150">tema de Hello **Essentials** hoja se muestra.</span><span class="sxs-lookup"><span data-stu-id="5a5ea-150">hello topic **Essentials** blade is displayed.</span></span> <span data-ttu-id="5a5ea-151">En suscripciones de hello cerca de la parte inferior de Hola de hoja de hello, tenga en cuenta que hello **número de mensajes** valor para cada suscripción ahora debe ser 1.</span><span class="sxs-lookup"><span data-stu-id="5a5ea-151">In hello subscription(s) listed near hello bottom of hello blade, notice that hello **Message Count** value for each subscription should now be 1.</span></span> <span data-ttu-id="5a5ea-152">Cada vez que se ejecute la aplicación del remitente Hola sin tener que recuperar mensajes de saludo (como se describe en la sección siguiente de hello), este valor se incrementa en 1.</span><span class="sxs-lookup"><span data-stu-id="5a5ea-152">Each time you run hello sender application without retrieving hello messages (as described in hello next section), this value increases by 1.</span></span> <span data-ttu-id="5a5ea-153">Tenga en cuenta también ese tamaño actual de Hola de Hola Hola de incrementos de tema **actual** valor en hello **Essentials** hoja cada vez aplicación hello agrega una mensaje toohello/suscripción al tema.</span><span class="sxs-lookup"><span data-stu-id="5a5ea-153">Also note that hello current size of hello topic increments hello **Current** value on hello **Essentials** blade each time hello app adds a message toohello topic/subscription.</span></span>
   
      ![Tamaño del mensaje][topic-message]

## <a name="5-receive-messages-from-hello-subscription"></a><span data-ttu-id="5a5ea-155">5. Recibir mensajes de Hola suscripción</span><span class="sxs-lookup"><span data-stu-id="5a5ea-155">5. Receive messages from hello subscription</span></span>

1. <span data-ttu-id="5a5ea-156">Hola tooreceive o mensajes que acabamos de enviar, cree una nueva aplicación de consola y agregue un paquete de NuGet de Bus de servicio de referencia toohello, aplicación remitente similar de toohello anterior.</span><span class="sxs-lookup"><span data-stu-id="5a5ea-156">tooreceive hello message or messages you just sent, create a new console application and add a reference toohello Service Bus NuGet package, similar toohello previous sender application.</span></span>
2. <span data-ttu-id="5a5ea-157">Agregue los siguiente hello `using` parte superior de toohello de instrucción del archivo Program.cs de Hola.</span><span class="sxs-lookup"><span data-stu-id="5a5ea-157">Add hello following `using` statement toohello top of hello Program.cs file.</span></span>
   
    ```csharp
    using Microsoft.ServiceBus.Messaging;
    ```
3. <span data-ttu-id="5a5ea-158">Agregar Hola después código toohello `Main` método.</span><span class="sxs-lookup"><span data-stu-id="5a5ea-158">Add hello following code toohello `Main` method.</span></span> <span data-ttu-id="5a5ea-159">Conjunto hello `connectionString` toohello variable conexión cadena que se obtuvo al crear el espacio de nombres de Hola y establecer `topicName` nombre toohello que usó al crear tema Hola.</span><span class="sxs-lookup"><span data-stu-id="5a5ea-159">Set hello `connectionString` variable toohello connection string you obtained when creating hello namespace, and set `topicName` toohello name that you used when creating hello topic.</span></span>
   
    ```csharp
    var connectionString = "<your connection string>";
    var topicName = "<your topic name>";
   
    var client = SubscriptionClient.CreateFromConnectionString(connectionString, topicName, "<your subscription name>");
   
    client.OnMessage(message =>
    {
      Console.WriteLine(String.Format("Message body: {0}", message.GetBody<String>()));
      Console.WriteLine(String.Format("Message id: {0}", message.MessageId));
    });
   
    Console.WriteLine("Press ENTER tooexit program");
    Console.ReadLine();
    ```
   
    <span data-ttu-id="5a5ea-160">Este es el aspecto que debería tener el archivo Program.cs:</span><span class="sxs-lookup"><span data-stu-id="5a5ea-160">Here is what your Program.cs file should look like:</span></span>
   
    ```csharp
    using System;
    using Microsoft.ServiceBus.Messaging;
   
    namespace GettingStartedWithTopics
    {
      class Program
      {
        static void Main(string[] args)
        {
          var connectionString = "Endpoint=sb://<your namespace>.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=<your key>";;
          var topicName = "<your topic name>";
   
          var client = SubscriptionClient.CreateFromConnectionString(connectionString, topicName, "<your subscription name>");
   
          client.OnMessage(message =>
          {
            Console.WriteLine(String.Format("Message body: {0}", message.GetBody<String>()));
            Console.WriteLine(String.Format("Message id: {0}", message.MessageId));
          });

          Console.WriteLine("Press ENTER tooexit program");   
          Console.ReadLine();
        }
      }
    }
    ```
4. <span data-ttu-id="5a5ea-161">Ejecutar programa hello y visite el portal de Hola de nuevo.</span><span class="sxs-lookup"><span data-stu-id="5a5ea-161">Run hello program, and check hello portal again.</span></span> <span data-ttu-id="5a5ea-162">Tenga en cuenta que hello **número de mensajes** y **actual** valores ahora son 0.</span><span class="sxs-lookup"><span data-stu-id="5a5ea-162">Notice that hello **Message Count** and **Current** values are now 0.</span></span>
   
    ![Longitud del tema][topic-message-receive]

<span data-ttu-id="5a5ea-164">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="5a5ea-164">Congratulations!</span></span> <span data-ttu-id="5a5ea-165">Ya ha creado un tema y una suscripción, ha enviado un mensaje y ha recibido dicho mensaje.</span><span class="sxs-lookup"><span data-stu-id="5a5ea-165">You have now created a topic and subscription, sent a message, and received that message.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5a5ea-166">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5a5ea-166">Next steps</span></span>

<span data-ttu-id="5a5ea-167">Visite nuestro [repositorio de GitHub con ejemplos](https://github.com/Azure/azure-service-bus/tree/master/samples) que muestran algunas de las características de mensajería de Bus de servicio más avanzadas de Hola.</span><span class="sxs-lookup"><span data-stu-id="5a5ea-167">Check out our [GitHub repository with samples](https://github.com/Azure/azure-service-bus/tree/master/samples) that demonstrate some of hello more advanced features of Service Bus messaging.</span></span>

<!--Image references-->

[nuget-pkg]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/nuget-package.png
[topic-message]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/topic-message.png
[topic-message-receive]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/topic-message-receive.png
[createtopic1]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/create-topic1.png
[createtopic2]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/create-topic2.png
[createtopic3]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/create-topic3.png
[createtopic4]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/create-topic4.png
[github-samples]: https://github.com/Azure-Samples/azure-servicebus-messaging-samples
[azure-portal]: https://portal.azure.com
