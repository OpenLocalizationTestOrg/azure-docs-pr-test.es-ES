---
title: "Centros de notificaciones: arquitectura de inserción empresarial"
description: Instrucciones de uso de los Centros de notificaciones de Azure en un entorno de empresa
services: notification-hubs
documentationcenter: 
author: ysxu
manager: erikre
editor: 
ms.assetid: 903023e9-9347-442a-924b-663af85e05c6
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: ae7c1c9644ecfe7fe4ad6e332cc0683a3b5df22f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="enterprise-push-architectural-guidance"></a><span data-ttu-id="d0c17-103">Instrucciones sobre arquitectura de inserción empresarial</span><span class="sxs-lookup"><span data-stu-id="d0c17-103">Enterprise push architectural guidance</span></span>
<span data-ttu-id="d0c17-104">En la actualidad, las empresas están pasando cada vez más hacia la creación de aplicaciones móviles para sus usuarios finales (externos) o para los empleados (internos).</span><span class="sxs-lookup"><span data-stu-id="d0c17-104">Enterprises today are gradually moving towards creating mobile applications for either their end users (external) or for the employees (internal).</span></span> <span data-ttu-id="d0c17-105">Disponen de sistemas back-end como grandes sistemas (mainframes) o algunas aplicaciones de línea de negocio (LoB) que deben estar integradas en la arquitectura de aplicaciones móviles.</span><span class="sxs-lookup"><span data-stu-id="d0c17-105">They have existing backend systems in place be it mainframes or some LoB applications which must be integrated into the mobile application architecture.</span></span> <span data-ttu-id="d0c17-106">En esta guía hablaremos acerca de la mejor manera de realizar esta integración y recomendaremos soluciones posibles a escenarios comunes.</span><span class="sxs-lookup"><span data-stu-id="d0c17-106">This guide will talk about how best to do this integration recommending possible solution to common scenarios.</span></span>

<span data-ttu-id="d0c17-107">Un requisito frecuente es el envío de notificaciones de inserción a los usuarios a través de su aplicación móvil cuando se produce un evento de interés en los sistemas back-end.</span><span class="sxs-lookup"><span data-stu-id="d0c17-107">A frequent requirement is for sending push notification to the users through their mobile application when an event of interest occurs in the backend systems.</span></span> <span data-ttu-id="d0c17-108">Por ejemplo,</span><span class="sxs-lookup"><span data-stu-id="d0c17-108">E.g.</span></span> <span data-ttu-id="d0c17-109">el cliente de un banco que tiene la aplicación del banco en su iPhone desea recibir una notificación cuando se efectúe un cargo por encima de un importe determinado desde su cuenta, o un escenario de intranet en el que un empleado del departamento financiero que tiene una aplicación de aprobación de presupuestos en su Windows Phone desea recibir una notificación cuando obtenga una solicitud de aprobación.</span><span class="sxs-lookup"><span data-stu-id="d0c17-109">a bank customer who has the bank's banking app on her iPhone wants to be notified when a debit is made above a certain amount from her account or an intranet scenario where an employee from finance department who has a budget approval app on his Windows Phone wants to be notified when he gets an approval request.</span></span>

<span data-ttu-id="d0c17-110">El procesamiento de la cuenta bancaria o de la solicitud de aprobación se realiza probablemente en algún sistema back-end que debe iniciar una inserción al usuario.</span><span class="sxs-lookup"><span data-stu-id="d0c17-110">The bank account or approval processing is likely to be done in some backend system which must initiate a push to the user.</span></span> <span data-ttu-id="d0c17-111">Podría haber muchos sistemas back-end de este tipo que deben crear todos el mismo tipo de lógica para implementar la inserción cuando un evento desencadena una notificación.</span><span class="sxs-lookup"><span data-stu-id="d0c17-111">There may be multiple such backend systems which must all build the same kind of logic to implement push when an event triggers a notification.</span></span> <span data-ttu-id="d0c17-112">Aquí la complejidad reside en la integración de varios back-ends juntos con un único sistema de inserción donde los usuarios finales podrían haberse suscrito a diferentes notificaciones e incluso podría haber varias aplicaciones móviles, por ejemplo, en el caso de aplicaciones móviles de intranet donde una aplicación móvil puede querer recibir notificaciones de varios de estos sistemas back-end.</span><span class="sxs-lookup"><span data-stu-id="d0c17-112">The complexity here lies in integrating several backend systems together with a single push system where the end users may have subscribed to different notifications and there may even be multiple mobile applications e.g. in the case of intranet mobile apps where one mobile application may want to receive notifications from multiple such backend systems.</span></span> <span data-ttu-id="d0c17-113">Los sistemas back-end no conocen o no necesitan conocer la semántica/tecnología de inserción, de modo que una solución común aquí ha sido tradicionalmente introducir un componente que sondea los sistemas back-end en busca de eventos de interés y que es responsable de enviar los mensajes de inserción al cliente.</span><span class="sxs-lookup"><span data-stu-id="d0c17-113">The backend systems do not know or need to know of push semantics/technology so a common solution here traditionally has been to introduce a component which polls the backend systems for any events of interest and is responsible for sending the push messages to the client.</span></span>
<span data-ttu-id="d0c17-114">Aquí hablaremos de una solución mejor incluso usando el modelo de temas y suscripciones del Bus de servicio de Azure, que reducirá la complejidad y hará que la solución sea escalable.</span><span class="sxs-lookup"><span data-stu-id="d0c17-114">Here we will talk about an even better solution using Azure Service Bus - Topic/Subscription model which will reduce the complexity while making the solution scalable.</span></span>

<span data-ttu-id="d0c17-115">Esta es la arquitectura general de la solución (generalizada con varias aplicaciones móviles pero igualmente aplicable cuando solo hay una aplicación móvil).</span><span class="sxs-lookup"><span data-stu-id="d0c17-115">Here is the general architecture of the solution (generalized with multiple mobile apps but equally applicable when there is only one mobile app)</span></span>

## <a name="architecture"></a><span data-ttu-id="d0c17-116">Arquitectura</span><span class="sxs-lookup"><span data-stu-id="d0c17-116">Architecture</span></span>
![][1]

<span data-ttu-id="d0c17-117">La pieza clave en este diagrama arquitectónico es el Bus de servicio de Azure que proporciona un modelo de programación de temas y suscripciones (se puede obtener más información al respecto en [Programación Pub/Sub de Service Bus]).</span><span class="sxs-lookup"><span data-stu-id="d0c17-117">The key piece in this architectural diagram is Azure Service Bus which provides a topics/subscriptions programming model (more on it at [Service Bus Pub/Sub programming]).</span></span> <span data-ttu-id="d0c17-118">El receptor, en este caso el back-end móvil (normalmente el [servicio móvil de Azure], que iniciarán una inserción en las aplicaciones móviles) no recibe los mensajes directamente de los sistemas back-end si no que nosotros disponemos de una capa de abstracción intermedia que proporciona [Azure Service Bus] que permite que el back-end móvil reciba mensajes de uno o varios sistemas back-end.</span><span class="sxs-lookup"><span data-stu-id="d0c17-118">The receiver, which in this case, is the Mobile backend (typically [Azure Mobile Service], which will initiate a push to the mobile apps) does not receive messages directly from the backend systems but instead we have an intermediate abstraction layer provided by [Azure Service Bus] which enables mobile backend to receive messages from one or more backend systems.</span></span> <span data-ttu-id="d0c17-119">Se debe crear un tema de Bus de servicio para cada uno de los sistemas back-end, por ejemplo, Cuentas, RR.HH., Finanzas, que son básicamente "temas" de interés que iniciarán mensajes para enviarse como notificaciones de inserción.</span><span class="sxs-lookup"><span data-stu-id="d0c17-119">A Service Bus Topic needs to be created for each of the backend systems e.g. Account, HR, Finance which are basically "topics" of interest which will initiate messages to be sent as push notification.</span></span> <span data-ttu-id="d0c17-120">Los sistemas back-end enviarán mensajes a estos temas.</span><span class="sxs-lookup"><span data-stu-id="d0c17-120">The backend systems will send messages to these topics.</span></span> <span data-ttu-id="d0c17-121">Un back-end móvil puede suscribirse a uno o varios de estos temas mediante la creación de una suscripción al Bus de servicio.</span><span class="sxs-lookup"><span data-stu-id="d0c17-121">A Mobile Backend can subscribe to one or more such topics by creating a Service Bus subscription.</span></span> <span data-ttu-id="d0c17-122">Esto permitirá al back-end móvil recibir una notificación del sistema back-end correspondiente.</span><span class="sxs-lookup"><span data-stu-id="d0c17-122">This will entitle the mobile backend to receive a notification from the corresponding backend system.</span></span> <span data-ttu-id="d0c17-123">El back-end móvil sigue escuchando mensajes en sus suscripciones y, en cuanto llega uno, da la vuelta y lo envía como notificación a su centro de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="d0c17-123">Mobile backend continues to listen for messages on their subscriptions and as soon as a message arrives, it turns back and sends it as notification to its notification hub.</span></span> <span data-ttu-id="d0c17-124">Los centros de notificaciones entregan finalmente el mensaje a la aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="d0c17-124">Notification hubs then eventually delivers the message to the mobile app.</span></span> <span data-ttu-id="d0c17-125">Así que, resumiendo, tenemos los siguientes componentes clave:</span><span class="sxs-lookup"><span data-stu-id="d0c17-125">So to summarize the key components, we have:</span></span>

1. <span data-ttu-id="d0c17-126">Sistema back-end (sistema LoB o heredado)</span><span class="sxs-lookup"><span data-stu-id="d0c17-126">Backend systems (LoB/Legacy systems)</span></span>
   * <span data-ttu-id="d0c17-127">Crea el tema del Bus de servicio</span><span class="sxs-lookup"><span data-stu-id="d0c17-127">Creates Service Bus Topic</span></span>
   * <span data-ttu-id="d0c17-128">Envía el mensaje</span><span class="sxs-lookup"><span data-stu-id="d0c17-128">Sends Message</span></span>
2. <span data-ttu-id="d0c17-129">Back-end móvil</span><span class="sxs-lookup"><span data-stu-id="d0c17-129">Mobile backend</span></span>
   * <span data-ttu-id="d0c17-130">Crea la suscripción al servicio</span><span class="sxs-lookup"><span data-stu-id="d0c17-130">Creates Service Subscription</span></span>
   * <span data-ttu-id="d0c17-131">Recibe el mensaje (del sistema back-end)</span><span class="sxs-lookup"><span data-stu-id="d0c17-131">Receives Message (from Backend system)</span></span>
   * <span data-ttu-id="d0c17-132">Envía una notificación a los clientes (a través del Centro de notificaciones de Azure)</span><span class="sxs-lookup"><span data-stu-id="d0c17-132">Sends notification to clients (via Azure Notification Hub)</span></span>
3. <span data-ttu-id="d0c17-133">Aplicación móvil</span><span class="sxs-lookup"><span data-stu-id="d0c17-133">Mobile Application</span></span>
   * <span data-ttu-id="d0c17-134">Recibe y muestra notificaciones</span><span class="sxs-lookup"><span data-stu-id="d0c17-134">Receives and display notification</span></span>

### <a name="benefits"></a><span data-ttu-id="d0c17-135">Ventajas:</span><span class="sxs-lookup"><span data-stu-id="d0c17-135">Benefits:</span></span>
1. <span data-ttu-id="d0c17-136">La separación entre el receptor (aplicación/servicio móvil a través del Centro de notificaciones) y el emisor (sistemas back-end) permite la integración de sistemas back-end adicionales con cambios mínimos.</span><span class="sxs-lookup"><span data-stu-id="d0c17-136">The decoupling between the receiver (mobile app/service via Notification Hub) and sender (backend systems) enables additional backend systems being integrated with minimal change.</span></span>
2. <span data-ttu-id="d0c17-137">Esto hace también que en el escenario de varias aplicaciones móviles, sea posible recibir eventos de uno o varios sistemas back-end.</span><span class="sxs-lookup"><span data-stu-id="d0c17-137">This also makes the scenario of multiple mobile apps being able to receive events from one or more backend systems.</span></span>  

## <a name="sample"></a><span data-ttu-id="d0c17-138">Sample:</span><span class="sxs-lookup"><span data-stu-id="d0c17-138">Sample:</span></span>
### <a name="prerequisites"></a><span data-ttu-id="d0c17-139">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="d0c17-139">Prerequisites</span></span>
<span data-ttu-id="d0c17-140">Para familiarizarse con los conceptos, así como con los pasos comunes de creación y configuración, debe realizar los siguientes tutoriales:</span><span class="sxs-lookup"><span data-stu-id="d0c17-140">You should complete the following tutorials to familiarize with the concepts as well as common creation & configuration steps:</span></span>

1. <span data-ttu-id="d0c17-141">[Programación Pub/Sub de Service Bus]: en él se explican los detalles de trabajar con temas y suscripciones de Service Bus, cómo crear un espacio de nombres que contenga temas o suscripciones y cómo enviar y recibir mensajes de ellos.</span><span class="sxs-lookup"><span data-stu-id="d0c17-141">[Service Bus Pub/Sub programming] - This explains the details of working with Service Bus Topics/Subscriptions, how to create a namespace to contain topics/subscriptions, how to send & receive messages from them.</span></span>
2. <span data-ttu-id="d0c17-142">[tutorial sobre Centros de notificaciones: Windows Universal] : en este tutorial se explica cómo configurar una aplicación de la Tienda Windows y usar los Centros de notificaciones para registrar y, después, recibir notificaciones.</span><span class="sxs-lookup"><span data-stu-id="d0c17-142">[Notification Hubs - Windows Universal tutorial] - This explains how to set up a Windows Store app and use Notification Hubs to register and then receive notifications.</span></span>

### <a name="sample-code"></a><span data-ttu-id="d0c17-143">Código de ejemplo</span><span class="sxs-lookup"><span data-stu-id="d0c17-143">Sample code</span></span>
<span data-ttu-id="d0c17-144">El código de ejemplo completo está disponible en [Ejemplos de centro de notificaciones].</span><span class="sxs-lookup"><span data-stu-id="d0c17-144">The full sample code is available at [Notification Hub Samples].</span></span> <span data-ttu-id="d0c17-145">Se divide en tres componentes:</span><span class="sxs-lookup"><span data-stu-id="d0c17-145">It is split into three components:</span></span>

1. <span data-ttu-id="d0c17-146">**EnterprisePushBackendSystem**</span><span class="sxs-lookup"><span data-stu-id="d0c17-146">**EnterprisePushBackendSystem**</span></span>
   
    <span data-ttu-id="d0c17-147">a.</span><span class="sxs-lookup"><span data-stu-id="d0c17-147">a.</span></span> <span data-ttu-id="d0c17-148">Este proyecto usa el paquete de NuGet *WindowsAzure.ServiceBus* y se basa en la [Programación Pub/Sub de Service Bus].</span><span class="sxs-lookup"><span data-stu-id="d0c17-148">This project uses the *WindowsAzure.ServiceBus* Nuget package and is  based on [Service Bus Pub/Sub programming].</span></span>
   
    <span data-ttu-id="d0c17-149">b.</span><span class="sxs-lookup"><span data-stu-id="d0c17-149">b.</span></span> <span data-ttu-id="d0c17-150">Se trata de una aplicación de consola C# sencilla para simular un sistema LoB que inicia el mensaje que se entrega a la aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="d0c17-150">This is a simple C# console app to simulate an LoB system which initiates the message to be delivered to the mobile app.</span></span>
   
        static void Main(string[] args)
        {
            string connectionString =
                CloudConfigurationManager.GetSetting("Microsoft.ServiceBus.ConnectionString");
   
            // Create the topic where we will send notifications
            CreateTopic(connectionString);
   
            // Send message
            SendMessage(connectionString);
        }
   
    <span data-ttu-id="d0c17-151">c.</span><span class="sxs-lookup"><span data-stu-id="d0c17-151">c.</span></span> <span data-ttu-id="d0c17-152">`CreateTopic` se usa para crear el tema del Bus de servicio al que se enviarán los mensajes.</span><span class="sxs-lookup"><span data-stu-id="d0c17-152">`CreateTopic` is used to create the Service Bus topic where we will send messages.</span></span>
   
        public static void CreateTopic(string connectionString)
        {
            // Create the topic if it does not exist already
   
            var namespaceManager =
                NamespaceManager.CreateFromConnectionString(connectionString);
   
            if (!namespaceManager.TopicExists(sampleTopic))
            {
                namespaceManager.CreateTopic(sampleTopic);
            }
        }
   
    <span data-ttu-id="d0c17-153">d.</span><span class="sxs-lookup"><span data-stu-id="d0c17-153">d.</span></span> <span data-ttu-id="d0c17-154">`SendMessage` se usa para enviar los mensajes a este tema del Bus de servicio.</span><span class="sxs-lookup"><span data-stu-id="d0c17-154">`SendMessage` is used to send the messages to this Service Bus Topic.</span></span> <span data-ttu-id="d0c17-155">En este ejemplo, simplemente enviaremos un conjunto de mensajes aleatorios al tema de manera periódica.</span><span class="sxs-lookup"><span data-stu-id="d0c17-155">Here we are simply sending a set of random messages to the topic periodically for the purpose of the sample.</span></span> <span data-ttu-id="d0c17-156">Normalmente, habrá un sistema back-end que enviará los mensajes cuando se produzca un evento.</span><span class="sxs-lookup"><span data-stu-id="d0c17-156">Normally there will be a backend system which will send messages when an event occurs.</span></span>
   
        public static void SendMessage(string connectionString)
        {
            TopicClient client =
                TopicClient.CreateFromConnectionString(connectionString, sampleTopic);
   
            // Sends random messages every 10 seconds to the topic
            string[] messages =
            {
                "Employee Id '{0}' has joined.",
                "Employee Id '{0}' has left.",
                "Employee Id '{0}' has switched to a different team."
            };
   
            while (true)
            {
                Random rnd = new Random();
                string employeeId = rnd.Next(10000, 99999).ToString();
                string notification = String.Format(messages[rnd.Next(0,messages.Length)], employeeId);
   
                // Send Notification
                BrokeredMessage message = new BrokeredMessage(notification);
                client.Send(message);
   
                Console.WriteLine("{0} Message sent - '{1}'", DateTime.Now, notification);
   
                System.Threading.Thread.Sleep(new TimeSpan(0, 0, 10));
            }
        }
2. <span data-ttu-id="d0c17-157">**ReceiveAndSendNotification**</span><span class="sxs-lookup"><span data-stu-id="d0c17-157">**ReceiveAndSendNotification**</span></span>
   
    <span data-ttu-id="d0c17-158">a.</span><span class="sxs-lookup"><span data-stu-id="d0c17-158">a.</span></span> <span data-ttu-id="d0c17-159">Este proyecto usa los paquetes de NuGet *WindowsAzure.ServiceBus* y *Microsoft.Web.WebJobs.Publish* y se basa en la [Programación Pub/Sub de Service Bus].</span><span class="sxs-lookup"><span data-stu-id="d0c17-159">This project uses the *WindowsAzure.ServiceBus* and *Microsoft.Web.WebJobs.Publish* Nuget packages and is based on [Service Bus Pub/Sub programming].</span></span>
   
    <span data-ttu-id="d0c17-160">b.</span><span class="sxs-lookup"><span data-stu-id="d0c17-160">b.</span></span> <span data-ttu-id="d0c17-161">Se trata de otra consola de aplicación C# que ejecutaremos como un [trabajo web de Azure] dado que se tiene que ejecutar continuamente para escuchar mensajes de los sistemas LoB/back-end.</span><span class="sxs-lookup"><span data-stu-id="d0c17-161">This is another C# console app which we will run as an [Azure WebJob] since it has to run continuously to listen for messages from the LoB/backend systems.</span></span> <span data-ttu-id="d0c17-162">Formará parte de su back-end móvil.</span><span class="sxs-lookup"><span data-stu-id="d0c17-162">This will be part of your Mobile backend.</span></span>
   
        static void Main(string[] args)
        {
            string connectionString =
                     CloudConfigurationManager.GetSetting("Microsoft.ServiceBus.ConnectionString");
   
            // Create the subscription which will receive messages
            CreateSubscription(connectionString);
   
            // Receive message
            ReceiveMessageAndSendNotification(connectionString);
        }
   
    <span data-ttu-id="d0c17-163">c.</span><span class="sxs-lookup"><span data-stu-id="d0c17-163">c.</span></span> <span data-ttu-id="d0c17-164">`CreateSubscription` se usa para crear una suscripción de Service Bus para el tema donde el sistema back-end enviará mensajes.</span><span class="sxs-lookup"><span data-stu-id="d0c17-164">`CreateSubscription` is used to create a Service Bus subscription for the topic where the backend system will send messages.</span></span> <span data-ttu-id="d0c17-165">Según el escenario empresarial, este componente creará una o varias suscripciones a temas correspondientes (por ejemplo, puede que algunos reciban mensajes del sistema de RR. PP., otros del sistema de Finanzas, etc.)</span><span class="sxs-lookup"><span data-stu-id="d0c17-165">Depending on the business scenario, this component will create one or more subscriptions to corresponding topics (e.g. some may be receiving messages from HR system, some from Finance system, and so on)</span></span>
   
        static void CreateSubscription(string connectionString)
        {
            // Create the subscription if it does not exist already
            var namespaceManager =
                NamespaceManager.CreateFromConnectionString(connectionString);
   
            if (!namespaceManager.SubscriptionExists(sampleTopic, sampleSubscription))
            {
                namespaceManager.CreateSubscription(sampleTopic, sampleSubscription);
            }
        }
   
    <span data-ttu-id="d0c17-166">d.</span><span class="sxs-lookup"><span data-stu-id="d0c17-166">d.</span></span> <span data-ttu-id="d0c17-167">ReceiveMessageAndSendNotification se usa para leer el mensaje del tema mediante su suscripción y, si la lectura se realiza correctamente, entonces se crea una notificación (en el escenario de ejemplo, una notificación del sistema nativa de Windows) para su envío a la aplicación móvil mediante los Centros de notificaciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="d0c17-167">ReceiveMessageAndSendNotification is used to read the message from the topic using its subscription and if the read is successful then craft a notification (in the sample scenario a Windows native toast notification) to be sent to the mobile application using Azure Notification Hubs.</span></span>
   
        static void ReceiveMessageAndSendNotification(string connectionString)
        {
            // Initialize the Notification Hub
            string hubConnectionString = CloudConfigurationManager.GetSetting
                    ("Microsoft.NotificationHub.ConnectionString");
            hub = NotificationHubClient.CreateClientFromConnectionString
                    (hubConnectionString, "enterprisepushservicehub");
   
            SubscriptionClient Client =
                SubscriptionClient.CreateFromConnectionString
                        (connectionString, sampleTopic, sampleSubscription);
   
            Client.Receive();
   
            // Continuously process messages received from the subscription
            while (true)
            {
                BrokeredMessage message = Client.Receive();
                var toastMessage = @"<toast><visual><binding template=""ToastText01""><text id=""1"">{messagepayload}</text></binding></visual></toast>";
   
                if (message != null)
                {
                    try
                    {
                        Console.WriteLine(message.MessageId);
                        Console.WriteLine(message.SequenceNumber);
                        string messageBody = message.GetBody<string>();
                        Console.WriteLine("Body: " + messageBody + "\n");
   
                        toastMessage = toastMessage.Replace("{messagepayload}", messageBody);
                        SendNotificationAsync(toastMessage);
   
                        // Remove message from subscription
                        message.Complete();
                    }
                    catch (Exception)
                    {
                        // Indicate a problem, unlock message in subscription
                        message.Abandon();
                    }
                }
            }
        }
        static async void SendNotificationAsync(string message)
        {
            await hub.SendWindowsNativeNotificationAsync(message);
        }
   
    <span data-ttu-id="d0c17-168">e.</span><span class="sxs-lookup"><span data-stu-id="d0c17-168">e.</span></span> <span data-ttu-id="d0c17-169">Para publicar esto como un **trabajo web**, haga clic con el botón derecho en la solución en Visual Studio y seleccione **Publicar como trabajo web**.</span><span class="sxs-lookup"><span data-stu-id="d0c17-169">For publishing this as a **WebJob**, right click on the solution in Visual Studio and select **Publish as WebJob**</span></span>
   
    ![][2]
   
    <span data-ttu-id="d0c17-170">f.</span><span class="sxs-lookup"><span data-stu-id="d0c17-170">f.</span></span> <span data-ttu-id="d0c17-171">Seleccione su perfil de publicación y cree un nuevo sitio web de Azure, si aún no existe, que hospede este trabajo web. Cuando tenga el sitio web, haga clic en **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="d0c17-171">Select your publishing profile and create a new Azure WebSite if it doesnt exist already which will host this WebJob and once you have the WebSite then **Publish**.</span></span>
   
    ![][3]
   
    <span data-ttu-id="d0c17-172">g.</span><span class="sxs-lookup"><span data-stu-id="d0c17-172">g.</span></span> <span data-ttu-id="d0c17-173">Configure el trabajo como "Ejecutar continuamente", de modo que cuando inicie sesión en el [Portal de Azure clásico] vea algo parecido a esto:</span><span class="sxs-lookup"><span data-stu-id="d0c17-173">Configure the job to be "Run Continuously" so that when you log in to the [Azure Classic Portal] you should see something like the following:</span></span>
   
    ![][4]
3. <span data-ttu-id="d0c17-174">**EnterprisePushMobileApp**</span><span class="sxs-lookup"><span data-stu-id="d0c17-174">**EnterprisePushMobileApp**</span></span>
   
    <span data-ttu-id="d0c17-175">a.</span><span class="sxs-lookup"><span data-stu-id="d0c17-175">a.</span></span> <span data-ttu-id="d0c17-176">Se trata de una aplicación de la Tienda Windows que recibirá notificaciones del sistema del trabajo web que se ejecuta como parte de su back-end móvil y las mostrará.</span><span class="sxs-lookup"><span data-stu-id="d0c17-176">This is a Windows Store application which will receive toast notifications from the WebJob running as part of your Mobile backend and display it.</span></span> <span data-ttu-id="d0c17-177">Se basa en el [tutorial sobre Centros de notificaciones: Windows Universal].</span><span class="sxs-lookup"><span data-stu-id="d0c17-177">This is based on [Notification Hubs - Windows Universal tutorial].</span></span>  
   
    <span data-ttu-id="d0c17-178">b.</span><span class="sxs-lookup"><span data-stu-id="d0c17-178">b.</span></span> <span data-ttu-id="d0c17-179">Asegúrese de que su aplicación está habilitada para recibir notificaciones del sistema.</span><span class="sxs-lookup"><span data-stu-id="d0c17-179">Ensure that your application is enabled to receive toast notifications.</span></span>
   
    <span data-ttu-id="d0c17-180">c.</span><span class="sxs-lookup"><span data-stu-id="d0c17-180">c.</span></span> <span data-ttu-id="d0c17-181">Asegúrese de que se llama al siguiente código de registro de los Centros de notificaciones al inicio de la aplicación (después de sustituir los valores de *HubName* y *DefaultListenSharedAccessSignature*:</span><span class="sxs-lookup"><span data-stu-id="d0c17-181">Ensure that the following Notification Hubs registration code is being called at the App start up (after replacing the *HubName* and *DefaultListenSharedAccessSignature*:</span></span>
   
        private async void InitNotificationsAsync()
        {
            var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();
   
            var hub = new NotificationHub("[HubName]", "[DefaultListenSharedAccessSignature]");
            var result = await hub.RegisterNativeAsync(channel.Uri);
   
            // Displays the registration ID so you know it was successful
            if (result.RegistrationId != null)
            {
                var dialog = new MessageDialog("Registration successful: " + result.RegistrationId);
                dialog.Commands.Add(new UICommand("OK"));
                await dialog.ShowAsync();
            }
        }

### <a name="running-sample"></a><span data-ttu-id="d0c17-182">Ejecución del ejemplo:</span><span class="sxs-lookup"><span data-stu-id="d0c17-182">Running sample:</span></span>
1. <span data-ttu-id="d0c17-183">Asegúrese de que su trabajo web se ejecuta correctamente y está programado como "Ejecutar continuamente".</span><span class="sxs-lookup"><span data-stu-id="d0c17-183">Ensure that your WebJob is running successfully and scheduled to "Run Continuously".</span></span>
2. <span data-ttu-id="d0c17-184">Ejecute **EnterprisePushMobileApp** , que iniciará la aplicación de la Tienda Windows.</span><span class="sxs-lookup"><span data-stu-id="d0c17-184">Run the **EnterprisePushMobileApp** which will start the Windows Store app.</span></span>
3. <span data-ttu-id="d0c17-185">Ejecute la aplicación de consola **EnterprisePushBackendSystem** , que simulará el back-end LoB e iniciará el envío de mensajes, de modo que verá que aparecen notificaciones del sistema como las siguientes:</span><span class="sxs-lookup"><span data-stu-id="d0c17-185">Run the **EnterprisePushBackendSystem** console application which will simulate the LoB backend and will start sending messages and you should see toast notifications appearing like the following:</span></span>
   
    ![][5]
4. <span data-ttu-id="d0c17-186">Los mensajes se enviaron originalmente a temas del Bus de servicio, los cuales son supervisadas por las suscripciones del Bus de servicio en el trabajo web.</span><span class="sxs-lookup"><span data-stu-id="d0c17-186">The messages were originally sent to Service Bus topics which was being monitored by Service Bus subscriptions in your Web Job.</span></span> <span data-ttu-id="d0c17-187">Cuando se recibe un mensaje, se crea una notificación y se envía a la aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="d0c17-187">Once a message was received, a notification was created and sent to the mobile app.</span></span> <span data-ttu-id="d0c17-188">Puede examinar los registros del trabajo web para confirmar el procesamiento en el vínculo Registros en el [Portal de Azure clásico] correspondiente a su trabajo web:</span><span class="sxs-lookup"><span data-stu-id="d0c17-188">You can look through the WebJob logs to confirm the processing when you go to the Logs link in [Azure Classic Portal] for your Web Job:</span></span>
   
    ![][6]

<!-- Images -->
[1]: ./media/notification-hubs-enterprise-push-architecture/architecture.png
[2]: ./media/notification-hubs-enterprise-push-architecture/WebJobsContextMenu.png
[3]: ./media/notification-hubs-enterprise-push-architecture/PublishAsWebJob.png
[4]: ./media/notification-hubs-enterprise-push-architecture/WebJob.png
[5]: ./media/notification-hubs-enterprise-push-architecture/Notifications.png
[6]: ./media/notification-hubs-enterprise-push-architecture/WebJobsLog.png

<!-- Links -->
<span data-ttu-id="d0c17-189">[Ejemplos de centro de notificaciones]: https://github.com/Azure/azure-notificationhubs-samples</span><span class="sxs-lookup"><span data-stu-id="d0c17-189">[Notification Hub Samples]: https://github.com/Azure/azure-notificationhubs-samples</span></span>
<span data-ttu-id="d0c17-190">[servicio móvil de Azure]: http://azure.microsoft.com/documentation/services/mobile-services/</span><span class="sxs-lookup"><span data-stu-id="d0c17-190">[Azure Mobile Service]: http://azure.microsoft.com/documentation/services/mobile-services/</span></span>
<span data-ttu-id="d0c17-191">[Azure Service Bus]: http://azure.microsoft.com/documentation/articles/fundamentals-service-bus-hybrid-solutions/</span><span class="sxs-lookup"><span data-stu-id="d0c17-191">[Azure Service Bus]: http://azure.microsoft.com/documentation/articles/fundamentals-service-bus-hybrid-solutions/</span></span>
<span data-ttu-id="d0c17-192">[Programación Pub/Sub de Service Bus]: http://azure.microsoft.com/documentation/articles/service-bus-dotnet-how-to-use-topics-subscriptions/</span><span class="sxs-lookup"><span data-stu-id="d0c17-192">[Service Bus Pub/Sub programming]: http://azure.microsoft.com/documentation/articles/service-bus-dotnet-how-to-use-topics-subscriptions/</span></span>
<span data-ttu-id="d0c17-193">[trabajo web de Azure]: http://azure.microsoft.com/documentation/articles/web-sites-create-web-jobs/</span><span class="sxs-lookup"><span data-stu-id="d0c17-193">[Azure WebJob]: http://azure.microsoft.com/documentation/articles/web-sites-create-web-jobs/</span></span>
<span data-ttu-id="d0c17-194">[tutorial sobre Centros de notificaciones: Windows Universal]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-get-started/</span><span class="sxs-lookup"><span data-stu-id="d0c17-194">[Notification Hubs - Windows Universal tutorial]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-get-started/</span></span>
<span data-ttu-id="d0c17-195">[Portal de Azure clásico]: https://manage.windowsazure.com/</span><span class="sxs-lookup"><span data-stu-id="d0c17-195">[Azure Classic Portal]: https://manage.windowsazure.com/</span></span>
