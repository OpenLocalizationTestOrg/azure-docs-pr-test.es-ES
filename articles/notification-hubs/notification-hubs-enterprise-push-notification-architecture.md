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
# <a name="enterprise-push-architectural-guidance"></a>Instrucciones sobre arquitectura de inserción empresarial
Hoy en día, las empresas están gradualmente empezando a crear aplicaciones móviles para cualquiera de sus usuarios finales (externo) o para los empleados de hello (internos). Tienen los sistemas back-end existentes en su lugar puede grandes sistemas o algunas aplicaciones de LoB que deben estar integrados en Hola arquitectura de aplicaciones móviles. Esta guía que trataremos más toodo la mejor manera de esta integración recomendar soluciones posibles escenarios de toocommon.

Un requisito frecuente es para el envío de los usuarios de toohello de notificación a través de sus aplicaciones móviles de inserción cuando se produce un evento de interés en sistemas de back-end de Hola. Por ejemplo, un cliente de un banco con aplicación de banca del banco de hello en su iPhone desea toobe una notificación cuando se realiza un débito por encima de una determinada cantidad de su cuenta de usuario o un escenario de intranet donde desea que un empleado del departamento de finanzas que tiene una aplicación de aprobación de presupuesto en su Windows Phone toobe una notificación cuando recibe una solicitud de aprobación.

cuenta bancaria de Hola o procesamiento de aprobación es probable toobe realizado en algún sistema de back-end que debe iniciarse ni un usuario de toohello de inserción. Puede haber varios tal back-end sistemas que deben generar todos Hola mismo tipo de inserción de lógica tooimplement cuando un evento desencadena una notificación. complejidad de Hello aquí radica en integrar varios sistemas de back-end junto con un sistema de inserción única donde hello a los usuarios finales pueden ha suscrito toodifferent notificaciones y puede incluso tener varias aplicaciones móviles, por ejemplo, en caso de hello de aplicaciones móviles de intranet en una aplicación móvil puede tooreceive notificaciones desde varios tales sistemas back-end. sistemas de back-end de Hello no conoce o no necesita tooknow de semántica y la tecnología de inserción para que una solución habitual aquí ha sido tradicionalmente toointroduce un componente que sondea los sistemas de back-end de Hola para todos los eventos de interés y es responsable de enviar mensajes de inserción de Hola cliente toohello.
A continuación hablaremos sobre una solución aún mejor con Bus de servicio de Azure - modelo de tema/suscripción que reducirá la complejidad de hello al realizar la solución de hello escalable.

Aquí es arquitectura general de Hola de solución de hello (generalizado con varias aplicaciones móviles aunque aplicarse cuando hay solo una aplicación móvil)

## <a name="architecture"></a>Arquitectura
![][1]

Hola clave en este diagrama de arquitectura es Service Bus de Azure que proporciona un modelo de programación de temas/suscripciones (más información sobre la en [programación de Bus de servicio Pub/Sub]). receptor de Hello, lo que en este caso, es back-end de hello móvil (normalmente [servicios móviles de Azure], que iniciará una inserción toohello las aplicaciones móviles) no recibe mensajes directamente desde sistemas de back-end de hello pero en su lugar, tenemos un capa de abstracción intermedio proporcionada por [Service Bus de Azure] que permite que los mensajes de tooreceive móvil de back-end de uno o varios sistemas de back-end. Un tema de Bus de servicio debe toobe creado para cada uno de los sistemas de back-end de hello p. ej., cuenta, recursos humanos, finanzas que básicamente son "temas" de interés que se iniciará la toobe de mensajes enviado como notificación de inserción. sistemas de back-end de Hello enviará mensajes temas toothese. Un móvil de back-end puede suscribirse tooone o más temas mediante la creación de una suscripción de Bus de servicio. Esto le da derecho Hola móvil de back-end tooreceive una notificación de sistema de back-end de hello correspondiente. Móvil back-end continúa toolisten para los mensajes en sus suscripciones y tan pronto como llega un mensaje, vuelve atrás y lo envía como centro de notificaciones de tooits de notificación. Centros de notificaciones, a continuación, entrega finalmente toohello de mensaje Hola aplicación móvil. Componentes clave de toosummarize hello, tenemos:

1. Sistema back-end (sistema LoB o heredado)
   * Crea el tema del Bus de servicio
   * Envía el mensaje
2. Back-end móvil
   * Crea la suscripción al servicio
   * Recibe el mensaje (del sistema back-end)
   * Envía notificación tooclients (a través del centro de notificaciones de Azure)
3. Aplicación móvil
   * Recibe y muestra notificaciones

### <a name="benefits"></a>Ventajas:
1. Hola desasociación entre Hola receptor (aplicación/Servicio móvil a través del centro de notificaciones) y el emisor (sistemas back-end) permite que los sistemas adicionales de back-end se integra con cambios mínimos.
2. Esto hará que el escenario Hola de varias aplicaciones móviles que se va a tooreceive capaz de eventos de uno o varios sistemas de back-end.  

## <a name="sample"></a>Sample:
### <a name="prerequisites"></a>Requisitos previos
Debe completar Hola después toofamiliarize tutoriales con conceptos de hello, así como pasos comunes de creación y configuración:

1. [programación de Bus de servicio Pub/Sub] -esto detalles Hola de trabajar con temas de Bus de servicio/suscripciones, explica cómo toocreate un espacio de nombres toocontain temas/suscripciones, cómo toosend & recibir mensajes de ellos.
2. [Centros de notificaciones - tutorial universales de Windows] -explica cómo tooset una copia de seguridad una aplicación de la tienda de Windows y usar tooregister centros de notificaciones y, a continuación, recibir notificaciones.

### <a name="sample-code"></a>Código de ejemplo
está disponible en el código de ejemplo completo de Hello [ejemplos de concentrador de notificación]. Se divide en tres componentes:

1. **EnterprisePushBackendSystem**
   
    a. Este proyecto usa hello *WindowsAzure.ServiceBus* paquete de Nuget y se basa en [programación de Bus de servicio Pub/Sub].
   
    b. Se trata de una simple C# consola aplicación toosimulate un sistema de LoB que inicia toobe de mensaje de Hola entregado toohello de aplicaciones móviles.
   
        static void Main(string[] args)
        {
            string connectionString =
                CloudConfigurationManager.GetSetting("Microsoft.ServiceBus.ConnectionString");
   
            // Create hello topic where we will send notifications
            CreateTopic(connectionString);
   
            // Send message
            SendMessage(connectionString);
        }
   
    c. `CreateTopic`es tema de Bus de servicio de hello toocreate utilizado que se enviará mensajes.
   
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
   
    d. `SendMessage`es utilizado toosend Hola mensajes toothis tema de Bus de servicio. Aquí se simplemente envía un conjunto de tema de toohello mensajes aleatorios periódicamente con el fin de Hola de ejemplo de Hola. Normalmente, habrá un sistema back-end que enviará los mensajes cuando se produzca un evento.
   
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
2. **ReceiveAndSendNotification**
   
    a. Este proyecto usa hello *WindowsAzure.ServiceBus* y *Microsoft.Web.WebJobs.Publish* Nuget empaqueta y se basa en [programación de Bus de servicio Pub/Sub].
   
    b. Se trata de otra consola aplicación de C# que se ejecutarán como un [WebJob de Azure] porque tiene toorun continuamente toolisten para los mensajes procedentes de sistemas de LoB/back-end de Hola. Formará parte de su back-end móvil.
   
        static void Main(string[] args)
        {
            string connectionString =
                     CloudConfigurationManager.GetSetting("Microsoft.ServiceBus.ConnectionString");
   
            // Create hello subscription which will receive messages
            CreateSubscription(connectionString);
   
            // Receive message
            ReceiveMessageAndSendNotification(connectionString);
        }
   
    c. `CreateSubscription`es toocreate usa una suscripción de Bus de servicio para el tema de Hola donde el sistema de back-end de hello enviará mensajes. Según el escenario de negocio de hello, este componente creará una o varias suscripciones temas toocorresponding (por ejemplo, algunos pueden estar recibiendo mensajes de sistema de recursos humanos, algunas del sistema de finanzas y así sucesivamente)
   
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
   
    d. ReceiveMessageAndSendNotification es tooread usa el mensaje de saludo de tema de hello mediante su suscripción y si Hola de lectura se realiza correctamente, a continuación, elaborar un móvil de toohello de toobe enviado notificación (en el escenario de muestra de Hola una notificación del sistema nativo de Windows) aplicación que utiliza los centros de notificaciones de Azure.
   
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
   
    e. Para publicar este elemento como un **WebJob**, haga clic con el botón secundario en la solución de hello en Visual Studio y seleccione **publicar como trabajos Web**
   
    ![][2]
   
    f. Seleccione el perfil de publicación y cree un nuevo sitio Web de Azure si no existe ya que va a hospedar este trabajo Web y una vez que tenga, a continuación, sitio Web de hello **publicar**.
   
    ![][3]
   
    g. Configurar hello toobe de trabajo "Ejecutar continuamente" de modo que cuando inicia una sesión toohello [Portal clásico de Azure] debería ver algo parecido a Hola siguiente:
   
    ![][4]
3. **EnterprisePushMobileApp**
   
    a. Se trata de una aplicación de Windows Store que recibirá las notificaciones de la ejecución de trabajo Web de hello como parte de su back-end móvil y mostrarla. Se basa en el [Centros de notificaciones - tutorial universales de Windows].  
   
    b. Asegúrese de que la aplicación está habilitado tooreceive recibir notificaciones del sistema.
   
    c. Asegúrese de que se llama a ese Hola después el código de registro de los centros de notificaciones en hello Iniciar aplicación (después de reemplazar hello *HubName* y *DefaultListenSharedAccessSignature*:
   
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

### <a name="running-sample"></a>Ejecución del ejemplo:
1. Asegúrese de que su trabajo Web se esté ejecutando correctamente y programa demasiado "Ejecutar continuamente".
2. Ejecute hello **EnterprisePushMobileApp** que iniciará la aplicación de la tienda de Windows hello.
3. Ejecute hello **EnterprisePushBackendSystem** aplicación de consola que simulará back-end de hello LoB y se iniciará el envío de mensajes y debería ver las notificaciones que aparecen como Hola siguiente:
   
    ![][5]
4. mensajes de saludo enviados originalmente tooService temas de Bus que se está supervisando por suscripciones del Bus de servicio en el trabajo Web. Una vez que se recibió un mensaje, se crea una notificación y se envía toohello de aplicaciones móviles. Puede buscar a través de hello WebJob registros tooconfirm Hola procesamiento cuando vaya toohello vinculan registros en [Portal clásico de Azure] para su trabajo Web:
   
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
