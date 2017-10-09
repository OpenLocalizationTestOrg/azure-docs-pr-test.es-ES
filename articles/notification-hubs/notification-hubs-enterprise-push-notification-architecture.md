---
title: "aaaNotification concentradores - arquitectura de inserción de Enterprise"
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
ms.openlocfilehash: c3afb83de1ba0882bf99e10f38cca40cb42d07a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="enterprise-push-architectural-guidance"></a><span data-ttu-id="81068-103">Instrucciones sobre arquitectura de inserción empresarial</span><span class="sxs-lookup"><span data-stu-id="81068-103">Enterprise push architectural guidance</span></span>
<span data-ttu-id="81068-104">Hoy en día, las empresas están gradualmente empezando a crear aplicaciones móviles para cualquiera de sus usuarios finales (externo) o para los empleados de hello (internos).</span><span class="sxs-lookup"><span data-stu-id="81068-104">Enterprises today are gradually moving towards creating mobile applications for either their end users (external) or for hello employees (internal).</span></span> <span data-ttu-id="81068-105">Tienen los sistemas back-end existentes en su lugar puede grandes sistemas o algunas aplicaciones de LoB que deben estar integrados en Hola arquitectura de aplicaciones móviles.</span><span class="sxs-lookup"><span data-stu-id="81068-105">They have existing backend systems in place be it mainframes or some LoB applications which must be integrated into hello mobile application architecture.</span></span> <span data-ttu-id="81068-106">Esta guía que trataremos más toodo la mejor manera de esta integración recomendar soluciones posibles escenarios de toocommon.</span><span class="sxs-lookup"><span data-stu-id="81068-106">This guide will talk about how best toodo this integration recommending possible solution toocommon scenarios.</span></span>

<span data-ttu-id="81068-107">Un requisito frecuente es para el envío de los usuarios de toohello de notificación a través de sus aplicaciones móviles de inserción cuando se produce un evento de interés en sistemas de back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="81068-107">A frequent requirement is for sending push notification toohello users through their mobile application when an event of interest occurs in hello backend systems.</span></span> <span data-ttu-id="81068-108">Por ejemplo,</span><span class="sxs-lookup"><span data-stu-id="81068-108">E.g.</span></span> <span data-ttu-id="81068-109">un cliente de un banco con aplicación de banca del banco de hello en su iPhone desea toobe una notificación cuando se realiza un débito por encima de una determinada cantidad de su cuenta de usuario o un escenario de intranet donde desea que un empleado del departamento de finanzas que tiene una aplicación de aprobación de presupuesto en su Windows Phone toobe una notificación cuando recibe una solicitud de aprobación.</span><span class="sxs-lookup"><span data-stu-id="81068-109">a bank customer who has hello bank's banking app on her iPhone wants toobe notified when a debit is made above a certain amount from her account or an intranet scenario where an employee from finance department who has a budget approval app on his Windows Phone wants toobe notified when he gets an approval request.</span></span>

<span data-ttu-id="81068-110">cuenta bancaria de Hola o procesamiento de aprobación es probable toobe realizado en algún sistema de back-end que debe iniciarse ni un usuario de toohello de inserción.</span><span class="sxs-lookup"><span data-stu-id="81068-110">hello bank account or approval processing is likely toobe done in some backend system which must initiate a push toohello user.</span></span> <span data-ttu-id="81068-111">Puede haber varios tal back-end sistemas que deben generar todos Hola mismo tipo de inserción de lógica tooimplement cuando un evento desencadena una notificación.</span><span class="sxs-lookup"><span data-stu-id="81068-111">There may be multiple such backend systems which must all build hello same kind of logic tooimplement push when an event triggers a notification.</span></span> <span data-ttu-id="81068-112">complejidad de Hello aquí radica en integrar varios sistemas de back-end junto con un sistema de inserción única donde hello a los usuarios finales pueden ha suscrito toodifferent notificaciones y puede incluso tener varias aplicaciones móviles, por ejemplo, en caso de hello de aplicaciones móviles de intranet en una aplicación móvil puede tooreceive notificaciones desde varios tales sistemas back-end.</span><span class="sxs-lookup"><span data-stu-id="81068-112">hello complexity here lies in integrating several backend systems together with a single push system where hello end users may have subscribed toodifferent notifications and there may even be multiple mobile applications e.g. in hello case of intranet mobile apps where one mobile application may want tooreceive notifications from multiple such backend systems.</span></span> <span data-ttu-id="81068-113">sistemas de back-end de Hello no conoce o no necesita tooknow de semántica y la tecnología de inserción para que una solución habitual aquí ha sido tradicionalmente toointroduce un componente que sondea los sistemas de back-end de Hola para todos los eventos de interés y es responsable de enviar mensajes de inserción de Hola cliente toohello.</span><span class="sxs-lookup"><span data-stu-id="81068-113">hello backend systems do not know or need tooknow of push semantics/technology so a common solution here traditionally has been toointroduce a component which polls hello backend systems for any events of interest and is responsible for sending hello push messages toohello client.</span></span>
<span data-ttu-id="81068-114">A continuación hablaremos sobre una solución aún mejor con Bus de servicio de Azure - modelo de tema/suscripción que reducirá la complejidad de hello al realizar la solución de hello escalable.</span><span class="sxs-lookup"><span data-stu-id="81068-114">Here we will talk about an even better solution using Azure Service Bus - Topic/Subscription model which will reduce hello complexity while making hello solution scalable.</span></span>

<span data-ttu-id="81068-115">Aquí es arquitectura general de Hola de solución de hello (generalizado con varias aplicaciones móviles aunque aplicarse cuando hay solo una aplicación móvil)</span><span class="sxs-lookup"><span data-stu-id="81068-115">Here is hello general architecture of hello solution (generalized with multiple mobile apps but equally applicable when there is only one mobile app)</span></span>

## <a name="architecture"></a><span data-ttu-id="81068-116">Arquitectura</span><span class="sxs-lookup"><span data-stu-id="81068-116">Architecture</span></span>
![][1]

<span data-ttu-id="81068-117">Hola clave en este diagrama de arquitectura es Service Bus de Azure que proporciona un modelo de programación de temas/suscripciones (más información sobre la en [programación de Bus de servicio Pub/Sub]).</span><span class="sxs-lookup"><span data-stu-id="81068-117">hello key piece in this architectural diagram is Azure Service Bus which provides a topics/subscriptions programming model (more on it at [Service Bus Pub/Sub programming]).</span></span> <span data-ttu-id="81068-118">receptor de Hello, lo que en este caso, es back-end de hello móvil (normalmente [servicios móviles de Azure], que iniciará una inserción toohello las aplicaciones móviles) no recibe mensajes directamente desde sistemas de back-end de hello pero en su lugar, tenemos un capa de abstracción intermedio proporcionada por [Service Bus de Azure] que permite que los mensajes de tooreceive móvil de back-end de uno o varios sistemas de back-end.</span><span class="sxs-lookup"><span data-stu-id="81068-118">hello receiver, which in this case, is hello Mobile backend (typically [Azure Mobile Service], which will initiate a push toohello mobile apps) does not receive messages directly from hello backend systems but instead we have an intermediate abstraction layer provided by [Azure Service Bus] which enables mobile backend tooreceive messages from one or more backend systems.</span></span> <span data-ttu-id="81068-119">Un tema de Bus de servicio debe toobe creado para cada uno de los sistemas de back-end de hello p. ej., cuenta, recursos humanos, finanzas que básicamente son "temas" de interés que se iniciará la toobe de mensajes enviado como notificación de inserción.</span><span class="sxs-lookup"><span data-stu-id="81068-119">A Service Bus Topic needs toobe created for each of hello backend systems e.g. Account, HR, Finance which are basically "topics" of interest which will initiate messages toobe sent as push notification.</span></span> <span data-ttu-id="81068-120">sistemas de back-end de Hello enviará mensajes temas toothese.</span><span class="sxs-lookup"><span data-stu-id="81068-120">hello backend systems will send messages toothese topics.</span></span> <span data-ttu-id="81068-121">Un móvil de back-end puede suscribirse tooone o más temas mediante la creación de una suscripción de Bus de servicio.</span><span class="sxs-lookup"><span data-stu-id="81068-121">A Mobile Backend can subscribe tooone or more such topics by creating a Service Bus subscription.</span></span> <span data-ttu-id="81068-122">Esto le da derecho Hola móvil de back-end tooreceive una notificación de sistema de back-end de hello correspondiente.</span><span class="sxs-lookup"><span data-stu-id="81068-122">This will entitle hello mobile backend tooreceive a notification from hello corresponding backend system.</span></span> <span data-ttu-id="81068-123">Móvil back-end continúa toolisten para los mensajes en sus suscripciones y tan pronto como llega un mensaje, vuelve atrás y lo envía como centro de notificaciones de tooits de notificación.</span><span class="sxs-lookup"><span data-stu-id="81068-123">Mobile backend continues toolisten for messages on their subscriptions and as soon as a message arrives, it turns back and sends it as notification tooits notification hub.</span></span> <span data-ttu-id="81068-124">Centros de notificaciones, a continuación, entrega finalmente toohello de mensaje Hola aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="81068-124">Notification hubs then eventually delivers hello message toohello mobile app.</span></span> <span data-ttu-id="81068-125">Componentes clave de toosummarize hello, tenemos:</span><span class="sxs-lookup"><span data-stu-id="81068-125">So toosummarize hello key components, we have:</span></span>

1. <span data-ttu-id="81068-126">Sistema back-end (sistema LoB o heredado)</span><span class="sxs-lookup"><span data-stu-id="81068-126">Backend systems (LoB/Legacy systems)</span></span>
   * <span data-ttu-id="81068-127">Crea el tema del Bus de servicio</span><span class="sxs-lookup"><span data-stu-id="81068-127">Creates Service Bus Topic</span></span>
   * <span data-ttu-id="81068-128">Envía el mensaje</span><span class="sxs-lookup"><span data-stu-id="81068-128">Sends Message</span></span>
2. <span data-ttu-id="81068-129">Back-end móvil</span><span class="sxs-lookup"><span data-stu-id="81068-129">Mobile backend</span></span>
   * <span data-ttu-id="81068-130">Crea la suscripción al servicio</span><span class="sxs-lookup"><span data-stu-id="81068-130">Creates Service Subscription</span></span>
   * <span data-ttu-id="81068-131">Recibe el mensaje (del sistema back-end)</span><span class="sxs-lookup"><span data-stu-id="81068-131">Receives Message (from Backend system)</span></span>
   * <span data-ttu-id="81068-132">Envía notificación tooclients (a través del centro de notificaciones de Azure)</span><span class="sxs-lookup"><span data-stu-id="81068-132">Sends notification tooclients (via Azure Notification Hub)</span></span>
3. <span data-ttu-id="81068-133">Aplicación móvil</span><span class="sxs-lookup"><span data-stu-id="81068-133">Mobile Application</span></span>
   * <span data-ttu-id="81068-134">Recibe y muestra notificaciones</span><span class="sxs-lookup"><span data-stu-id="81068-134">Receives and display notification</span></span>

### <a name="benefits"></a><span data-ttu-id="81068-135">Ventajas:</span><span class="sxs-lookup"><span data-stu-id="81068-135">Benefits:</span></span>
1. <span data-ttu-id="81068-136">Hola desasociación entre Hola receptor (aplicación/Servicio móvil a través del centro de notificaciones) y el emisor (sistemas back-end) permite que los sistemas adicionales de back-end se integra con cambios mínimos.</span><span class="sxs-lookup"><span data-stu-id="81068-136">hello decoupling between hello receiver (mobile app/service via Notification Hub) and sender (backend systems) enables additional backend systems being integrated with minimal change.</span></span>
2. <span data-ttu-id="81068-137">Esto hará que el escenario Hola de varias aplicaciones móviles que se va a tooreceive capaz de eventos de uno o varios sistemas de back-end.</span><span class="sxs-lookup"><span data-stu-id="81068-137">This also makes hello scenario of multiple mobile apps being able tooreceive events from one or more backend systems.</span></span>  

## <a name="sample"></a><span data-ttu-id="81068-138">Sample:</span><span class="sxs-lookup"><span data-stu-id="81068-138">Sample:</span></span>
### <a name="prerequisites"></a><span data-ttu-id="81068-139">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="81068-139">Prerequisites</span></span>
<span data-ttu-id="81068-140">Debe completar Hola después toofamiliarize tutoriales con conceptos de hello, así como pasos comunes de creación y configuración:</span><span class="sxs-lookup"><span data-stu-id="81068-140">You should complete hello following tutorials toofamiliarize with hello concepts as well as common creation & configuration steps:</span></span>

1. <span data-ttu-id="81068-141">[programación de Bus de servicio Pub/Sub] -esto detalles Hola de trabajar con temas de Bus de servicio/suscripciones, explica cómo toocreate un espacio de nombres toocontain temas/suscripciones, cómo toosend & recibir mensajes de ellos.</span><span class="sxs-lookup"><span data-stu-id="81068-141">[Service Bus Pub/Sub programming] - This explains hello details of working with Service Bus Topics/Subscriptions, how toocreate a namespace toocontain topics/subscriptions, how toosend & receive messages from them.</span></span>
2. <span data-ttu-id="81068-142">[Centros de notificaciones - tutorial universales de Windows] -explica cómo tooset una copia de seguridad una aplicación de la tienda de Windows y usar tooregister centros de notificaciones y, a continuación, recibir notificaciones.</span><span class="sxs-lookup"><span data-stu-id="81068-142">[Notification Hubs - Windows Universal tutorial] - This explains how tooset up a Windows Store app and use Notification Hubs tooregister and then receive notifications.</span></span>

### <a name="sample-code"></a><span data-ttu-id="81068-143">Código de ejemplo</span><span class="sxs-lookup"><span data-stu-id="81068-143">Sample code</span></span>
<span data-ttu-id="81068-144">está disponible en el código de ejemplo completo de Hello [ejemplos de concentrador de notificación].</span><span class="sxs-lookup"><span data-stu-id="81068-144">hello full sample code is available at [Notification Hub Samples].</span></span> <span data-ttu-id="81068-145">Se divide en tres componentes:</span><span class="sxs-lookup"><span data-stu-id="81068-145">It is split into three components:</span></span>

1. <span data-ttu-id="81068-146">**EnterprisePushBackendSystem**</span><span class="sxs-lookup"><span data-stu-id="81068-146">**EnterprisePushBackendSystem**</span></span>
   
    <span data-ttu-id="81068-147">a.</span><span class="sxs-lookup"><span data-stu-id="81068-147">a.</span></span> <span data-ttu-id="81068-148">Este proyecto usa hello *WindowsAzure.ServiceBus* paquete de Nuget y se basa en [programación de Bus de servicio Pub/Sub].</span><span class="sxs-lookup"><span data-stu-id="81068-148">This project uses hello *WindowsAzure.ServiceBus* Nuget package and is  based on [Service Bus Pub/Sub programming].</span></span>
   
    <span data-ttu-id="81068-149">b.</span><span class="sxs-lookup"><span data-stu-id="81068-149">b.</span></span> <span data-ttu-id="81068-150">Se trata de una simple C# consola aplicación toosimulate un sistema de LoB que inicia toobe de mensaje de Hola entregado toohello de aplicaciones móviles.</span><span class="sxs-lookup"><span data-stu-id="81068-150">This is a simple C# console app toosimulate an LoB system which initiates hello message toobe delivered toohello mobile app.</span></span>
   
        static void Main(string[] args)
        {
            string connectionString =
                CloudConfigurationManager.GetSetting("Microsoft.ServiceBus.ConnectionString");
   
            // Create hello topic where we will send notifications
            CreateTopic(connectionString);
   
            // Send message
            SendMessage(connectionString);
        }
   
    <span data-ttu-id="81068-151">c.</span><span class="sxs-lookup"><span data-stu-id="81068-151">c.</span></span> <span data-ttu-id="81068-152">`CreateTopic`es tema de Bus de servicio de hello toocreate utilizado que se enviará mensajes.</span><span class="sxs-lookup"><span data-stu-id="81068-152">`CreateTopic` is used toocreate hello Service Bus topic where we will send messages.</span></span>
   
        public static void CreateTopic(string connectionString)
        {
            // Create hello topic if it does not exist already
   
            var namespaceManager =
                NamespaceManager.CreateFromConnectionString(connectionString);
   
            if (!namespaceManager.TopicExists(sampleTopic))
            {
                namespaceManager.CreateTopic(sampleTopic);
            }
        }
   
    <span data-ttu-id="81068-153">d.</span><span class="sxs-lookup"><span data-stu-id="81068-153">d.</span></span> <span data-ttu-id="81068-154">`SendMessage`es utilizado toosend Hola mensajes toothis tema de Bus de servicio.</span><span class="sxs-lookup"><span data-stu-id="81068-154">`SendMessage` is used toosend hello messages toothis Service Bus Topic.</span></span> <span data-ttu-id="81068-155">Aquí se simplemente envía un conjunto de tema de toohello mensajes aleatorios periódicamente con el fin de Hola de ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="81068-155">Here we are simply sending a set of random messages toohello topic periodically for hello purpose of hello sample.</span></span> <span data-ttu-id="81068-156">Normalmente, habrá un sistema back-end que enviará los mensajes cuando se produzca un evento.</span><span class="sxs-lookup"><span data-stu-id="81068-156">Normally there will be a backend system which will send messages when an event occurs.</span></span>
   
        public static void SendMessage(string connectionString)
        {
            TopicClient client =
                TopicClient.CreateFromConnectionString(connectionString, sampleTopic);
   
            // Sends random messages every 10 seconds toohello topic
            string[] messages =
            {
                "Employee Id '{0}' has joined.",
                "Employee Id '{0}' has left.",
                "Employee Id '{0}' has switched tooa different team."
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
2. <span data-ttu-id="81068-157">**ReceiveAndSendNotification**</span><span class="sxs-lookup"><span data-stu-id="81068-157">**ReceiveAndSendNotification**</span></span>
   
    <span data-ttu-id="81068-158">a.</span><span class="sxs-lookup"><span data-stu-id="81068-158">a.</span></span> <span data-ttu-id="81068-159">Este proyecto usa hello *WindowsAzure.ServiceBus* y *Microsoft.Web.WebJobs.Publish* Nuget empaqueta y se basa en [programación de Bus de servicio Pub/Sub].</span><span class="sxs-lookup"><span data-stu-id="81068-159">This project uses hello *WindowsAzure.ServiceBus* and *Microsoft.Web.WebJobs.Publish* Nuget packages and is based on [Service Bus Pub/Sub programming].</span></span>
   
    <span data-ttu-id="81068-160">b.</span><span class="sxs-lookup"><span data-stu-id="81068-160">b.</span></span> <span data-ttu-id="81068-161">Se trata de otra consola aplicación de C# que se ejecutarán como un [WebJob de Azure] porque tiene toorun continuamente toolisten para los mensajes procedentes de sistemas de LoB/back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="81068-161">This is another C# console app which we will run as an [Azure WebJob] since it has toorun continuously toolisten for messages from hello LoB/backend systems.</span></span> <span data-ttu-id="81068-162">Formará parte de su back-end móvil.</span><span class="sxs-lookup"><span data-stu-id="81068-162">This will be part of your Mobile backend.</span></span>
   
        static void Main(string[] args)
        {
            string connectionString =
                     CloudConfigurationManager.GetSetting("Microsoft.ServiceBus.ConnectionString");
   
            // Create hello subscription which will receive messages
            CreateSubscription(connectionString);
   
            // Receive message
            ReceiveMessageAndSendNotification(connectionString);
        }
   
    <span data-ttu-id="81068-163">c.</span><span class="sxs-lookup"><span data-stu-id="81068-163">c.</span></span> <span data-ttu-id="81068-164">`CreateSubscription`es toocreate usa una suscripción de Bus de servicio para el tema de Hola donde el sistema de back-end de hello enviará mensajes.</span><span class="sxs-lookup"><span data-stu-id="81068-164">`CreateSubscription` is used toocreate a Service Bus subscription for hello topic where hello backend system will send messages.</span></span> <span data-ttu-id="81068-165">Según el escenario de negocio de hello, este componente creará una o varias suscripciones temas toocorresponding (por ejemplo, algunos pueden estar recibiendo mensajes de sistema de recursos humanos, algunas del sistema de finanzas y así sucesivamente)</span><span class="sxs-lookup"><span data-stu-id="81068-165">Depending on hello business scenario, this component will create one or more subscriptions toocorresponding topics (e.g. some may be receiving messages from HR system, some from Finance system, and so on)</span></span>
   
        static void CreateSubscription(string connectionString)
        {
            // Create hello subscription if it does not exist already
            var namespaceManager =
                NamespaceManager.CreateFromConnectionString(connectionString);
   
            if (!namespaceManager.SubscriptionExists(sampleTopic, sampleSubscription))
            {
                namespaceManager.CreateSubscription(sampleTopic, sampleSubscription);
            }
        }
   
    <span data-ttu-id="81068-166">d.</span><span class="sxs-lookup"><span data-stu-id="81068-166">d.</span></span> <span data-ttu-id="81068-167">ReceiveMessageAndSendNotification es tooread usa el mensaje de saludo de tema de hello mediante su suscripción y si Hola de lectura se realiza correctamente, a continuación, elaborar un móvil de toohello de toobe enviado notificación (en el escenario de muestra de Hola una notificación del sistema nativo de Windows) aplicación que utiliza los centros de notificaciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="81068-167">ReceiveMessageAndSendNotification is used tooread hello message from hello topic using its subscription and if hello read is successful then craft a notification (in hello sample scenario a Windows native toast notification) toobe sent toohello mobile application using Azure Notification Hubs.</span></span>
   
        static void ReceiveMessageAndSendNotification(string connectionString)
        {
            // Initialize hello Notification Hub
            string hubConnectionString = CloudConfigurationManager.GetSetting
                    ("Microsoft.NotificationHub.ConnectionString");
            hub = NotificationHubClient.CreateClientFromConnectionString
                    (hubConnectionString, "enterprisepushservicehub");
   
            SubscriptionClient Client =
                SubscriptionClient.CreateFromConnectionString
                        (connectionString, sampleTopic, sampleSubscription);
   
            Client.Receive();
   
            // Continuously process messages received from hello subscription
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
   
    <span data-ttu-id="81068-168">e.</span><span class="sxs-lookup"><span data-stu-id="81068-168">e.</span></span> <span data-ttu-id="81068-169">Para publicar este elemento como un **WebJob**, haga clic con el botón secundario en la solución de hello en Visual Studio y seleccione **publicar como trabajos Web**</span><span class="sxs-lookup"><span data-stu-id="81068-169">For publishing this as a **WebJob**, right click on hello solution in Visual Studio and select **Publish as WebJob**</span></span>
   
    ![][2]
   
    <span data-ttu-id="81068-170">f.</span><span class="sxs-lookup"><span data-stu-id="81068-170">f.</span></span> <span data-ttu-id="81068-171">Seleccione el perfil de publicación y cree un nuevo sitio Web de Azure si no existe ya que va a hospedar este trabajo Web y una vez que tenga, a continuación, sitio Web de hello **publicar**.</span><span class="sxs-lookup"><span data-stu-id="81068-171">Select your publishing profile and create a new Azure WebSite if it doesnt exist already which will host this WebJob and once you have hello WebSite then **Publish**.</span></span>
   
    ![][3]
   
    <span data-ttu-id="81068-172">g.</span><span class="sxs-lookup"><span data-stu-id="81068-172">g.</span></span> <span data-ttu-id="81068-173">Configurar hello toobe de trabajo "Ejecutar continuamente" de modo que cuando inicia una sesión toohello [Portal clásico de Azure] debería ver algo parecido a Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="81068-173">Configure hello job toobe "Run Continuously" so that when you log in toohello [Azure Classic Portal] you should see something like hello following:</span></span>
   
    ![][4]
3. <span data-ttu-id="81068-174">**EnterprisePushMobileApp**</span><span class="sxs-lookup"><span data-stu-id="81068-174">**EnterprisePushMobileApp**</span></span>
   
    <span data-ttu-id="81068-175">a.</span><span class="sxs-lookup"><span data-stu-id="81068-175">a.</span></span> <span data-ttu-id="81068-176">Se trata de una aplicación de Windows Store que recibirá las notificaciones de la ejecución de trabajo Web de hello como parte de su back-end móvil y mostrarla.</span><span class="sxs-lookup"><span data-stu-id="81068-176">This is a Windows Store application which will receive toast notifications from hello WebJob running as part of your Mobile backend and display it.</span></span> <span data-ttu-id="81068-177">Se basa en el [Centros de notificaciones - tutorial universales de Windows].</span><span class="sxs-lookup"><span data-stu-id="81068-177">This is based on [Notification Hubs - Windows Universal tutorial].</span></span>  
   
    <span data-ttu-id="81068-178">b.</span><span class="sxs-lookup"><span data-stu-id="81068-178">b.</span></span> <span data-ttu-id="81068-179">Asegúrese de que la aplicación está habilitado tooreceive recibir notificaciones del sistema.</span><span class="sxs-lookup"><span data-stu-id="81068-179">Ensure that your application is enabled tooreceive toast notifications.</span></span>
   
    <span data-ttu-id="81068-180">c.</span><span class="sxs-lookup"><span data-stu-id="81068-180">c.</span></span> <span data-ttu-id="81068-181">Asegúrese de que se llama a ese Hola después el código de registro de los centros de notificaciones en hello Iniciar aplicación (después de reemplazar hello *HubName* y *DefaultListenSharedAccessSignature*:</span><span class="sxs-lookup"><span data-stu-id="81068-181">Ensure that hello following Notification Hubs registration code is being called at hello App start up (after replacing hello *HubName* and *DefaultListenSharedAccessSignature*:</span></span>
   
        private async void InitNotificationsAsync()
        {
            var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();
   
            var hub = new NotificationHub("[HubName]", "[DefaultListenSharedAccessSignature]");
            var result = await hub.RegisterNativeAsync(channel.Uri);
   
            // Displays hello registration ID so you know it was successful
            if (result.RegistrationId != null)
            {
                var dialog = new MessageDialog("Registration successful: " + result.RegistrationId);
                dialog.Commands.Add(new UICommand("OK"));
                await dialog.ShowAsync();
            }
        }

### <a name="running-sample"></a><span data-ttu-id="81068-182">Ejecución del ejemplo:</span><span class="sxs-lookup"><span data-stu-id="81068-182">Running sample:</span></span>
1. <span data-ttu-id="81068-183">Asegúrese de que su trabajo Web se esté ejecutando correctamente y programa demasiado "Ejecutar continuamente".</span><span class="sxs-lookup"><span data-stu-id="81068-183">Ensure that your WebJob is running successfully and scheduled too"Run Continuously".</span></span>
2. <span data-ttu-id="81068-184">Ejecute hello **EnterprisePushMobileApp** que iniciará la aplicación de la tienda de Windows hello.</span><span class="sxs-lookup"><span data-stu-id="81068-184">Run hello **EnterprisePushMobileApp** which will start hello Windows Store app.</span></span>
3. <span data-ttu-id="81068-185">Ejecute hello **EnterprisePushBackendSystem** aplicación de consola que simulará back-end de hello LoB y se iniciará el envío de mensajes y debería ver las notificaciones que aparecen como Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="81068-185">Run hello **EnterprisePushBackendSystem** console application which will simulate hello LoB backend and will start sending messages and you should see toast notifications appearing like hello following:</span></span>
   
    ![][5]
4. <span data-ttu-id="81068-186">mensajes de saludo enviados originalmente tooService temas de Bus que se está supervisando por suscripciones del Bus de servicio en el trabajo Web.</span><span class="sxs-lookup"><span data-stu-id="81068-186">hello messages were originally sent tooService Bus topics which was being monitored by Service Bus subscriptions in your Web Job.</span></span> <span data-ttu-id="81068-187">Una vez que se recibió un mensaje, se crea una notificación y se envía toohello de aplicaciones móviles.</span><span class="sxs-lookup"><span data-stu-id="81068-187">Once a message was received, a notification was created and sent toohello mobile app.</span></span> <span data-ttu-id="81068-188">Puede buscar a través de hello WebJob registros tooconfirm Hola procesamiento cuando vaya toohello vinculan registros en [Portal clásico de Azure] para su trabajo Web:</span><span class="sxs-lookup"><span data-stu-id="81068-188">You can look through hello WebJob logs tooconfirm hello processing when you go toohello Logs link in [Azure Classic Portal] for your Web Job:</span></span>
   
    ![][6]

<!-- Images -->
[1]: ./media/notification-hubs-enterprise-push-architecture/architecture.png
[2]: ./media/notification-hubs-enterprise-push-architecture/WebJobsContextMenu.png
[3]: ./media/notification-hubs-enterprise-push-architecture/PublishAsWebJob.png
[4]: ./media/notification-hubs-enterprise-push-architecture/WebJob.png
[5]: ./media/notification-hubs-enterprise-push-architecture/Notifications.png
[6]: ./media/notification-hubs-enterprise-push-architecture/WebJobsLog.png

<!-- Links -->
[ejemplos de concentrador de notificación]: https://github.com/Azure/azure-notificationhubs-samples
[servicios móviles de Azure]: http://azure.microsoft.com/documentation/services/mobile-services/
[Service Bus de Azure]: http://azure.microsoft.com/documentation/articles/fundamentals-service-bus-hybrid-solutions/
[programación de Bus de servicio Pub/Sub]: http://azure.microsoft.com/documentation/articles/service-bus-dotnet-how-to-use-topics-subscriptions/
[WebJob de Azure]: http://azure.microsoft.com/documentation/articles/web-sites-create-web-jobs/
[Centros de notificaciones - tutorial universales de Windows]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-get-started/
[Portal clásico de Azure]: https://manage.windowsazure.com/
