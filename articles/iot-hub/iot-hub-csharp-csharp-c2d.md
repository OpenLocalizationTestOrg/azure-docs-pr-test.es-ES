---
title: mensajes de aaaCloud al dispositivo con Azure IoT Hub (. NET) | Documentos de Microsoft
description: "¿Cómo toosend en la nube al dispositivo mensajes tooa del dispositivo de un centro de IoT de Azure mediante hello Azure IoT SDK para. NET. Modificar una aplicación de dispositivo tooreceive los mensajes de nube al dispositivo y modificar un mensajes de aplicaciones back-end toosend hello en la nube al dispositivo."
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: a31c05ed-6ec0-40f3-99ab-8fdd28b1a89a
ms.service: iot-hub
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: elioda
ms.openlocfilehash: f6a7618b164d95c8ddaf28943f244aeeb568217f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="send-messages-from-hello-cloud-tooyour-device-with-iot-hub-net"></a>Enviar mensajes desde el dispositivo de tooyour hello en la nube con IoT Hub (. NET)
[!INCLUDE [iot-hub-selector-c2d](../../includes/iot-hub-selector-c2d.md)]

## <a name="introduction"></a>Introducción
IoT Hub de Azure es un servicio totalmente administrado que permite la comunicación bidireccional confiable y segura entre millones de dispositivos y una solución de back-end. Hola [empezar a trabajar con el centro de IoT] tutorial muestra cómo aprovisionar una identidad de dispositivo en ella toocreate un centro de IoT y codificar una aplicación para dispositivos que envía mensajes de dispositivo a la nube.

Este tutorial se basa en la [introducción al Centro de IoT]. En él se muestra cómo realizar las siguientes acciones:

* Desde el back-end de soluciones, enviar mensajes en la nube al dispositivo tooa dispositivo a través del centro de IoT.
* Reciba mensajes de nube a dispositivo en un dispositivo.
* En el back-end de soluciones, solicitar confirmación de entrega (*comentarios*) para mensajes envían tooa dispositivo desde el centro de IoT.

Puede encontrar más información sobre los mensajes en la nube al dispositivo en hello [Guía del desarrollador de centro de IoT][IoT Hub developer guide - C2D].

Al final de Hola de este tutorial, ejecute dos aplicaciones de consola. NET:

* **SimulatedDevice**, una versión modificada de la aplicación hello creado en [empezar a trabajar con el centro de IoT], que se conecta el centro de IoT tooyour y recibe los mensajes de la nube al dispositivo.
* **SendCloudToDevice**, que envía un mensaje en la nube a dispositivo toohello del dispositivo a través del centro de IoT y, a continuación, recibe la confirmación de entrega.

> [!NOTE]
> IoT Hub ofrece compatibilidad con SDK para muchas plataformas de dispositivos y lenguajes (incluido C, Java y Javascript), mediante [SDK de dispositivos IoT de Azure]. Para obtener instrucciones paso a paso sobre cómo tooconnect del su dispositivo toothis tutorial código y generalmente tooAzure centro de IoT, vea hello [Guía del desarrollador de centro de IoT].
> 
> 

toocomplete este tutorial, necesita Hola siguientes:

* Visual Studio 2015 o Visual Studio 2017
* Una cuenta de Azure activa. (En caso de no tenerla, puede crear una [cuenta gratuita][lnk-free-trial] en solo unos minutos).

## <a name="receive-messages-in-hello-device-app"></a>Recibir mensajes en la aplicación de dispositivo de hello
En esta sección, modificará la aplicación de dispositivo de Hola que creó en [empezar a trabajar con el centro de IoT] mensajes de nube al dispositivo tooreceive Hola centro de IoT.

1. En Visual Studio, en hello **SimulatedDevice** proyecto de equipo y agregar Hola siguiendo el método toohello **programa** clase.
   
        private static async void ReceiveC2dAsync()
        {
            Console.WriteLine("\nReceiving cloud toodevice messages from service");
            while (true)
            {
                Message receivedMessage = await deviceClient.ReceiveAsync();
                if (receivedMessage == null) continue;
   
                Console.ForegroundColor = ConsoleColor.Yellow;
                Console.WriteLine("Received message: {0}", Encoding.ASCII.GetString(receivedMessage.GetBytes()));
                Console.ResetColor();
   
                await deviceClient.CompleteAsync(receivedMessage);
            }
        }
   
    Hola `ReceiveAsync` método asincrónicamente devuelve mensajes de bienvenida recibido en el tiempo de Hola que se recibe por dispositivo de Hola. Devuelve *null* tras un período de tiempo de espera puede especificar (en este caso, se utiliza el predeterminado de Hola de un minuto). Cuando recibe la aplicación hello un *null*, debería continuar toowait si hay mensajes nuevos. Este requisito es motivo Hola Hola `if (receivedMessage == null) continue` línea.
   
    Hola llamada demasiado`CompleteAsync()` notifica al centro de IoT ese mensaje Hola se ha procesado correctamente. mensaje de saludo puede quitarse con seguridad de cola de dispositivo de Hola. Si hubo un problema de esa aplicación de dispositivo ha impedido Hola de completar el procesamiento de Hola de mensaje de bienvenida, centro de IoT lo entrega de nuevo. A continuación, es importante esa lógica en la aplicación de dispositivo de hello de procesamiento de mensajes es *idempotente*, de modo que recibir Hola mismo mensaje varias veces genera Hola el mismo resultado. Una aplicación también temporalmente puede abandonar un mensaje, lo que resulta en el centro de IoT conserva el mensaje de saludo en cola de Hola para su futura utilización. O bien, aplicación hello puede rechazar un mensaje, que quita de forma permanente los mensajes de bienvenida de cola de Hola. Para obtener más información acerca del ciclo de vida del mensaje en la nube al dispositivo de hello, vea hello [Guía del desarrollador de centro de IoT][IoT Hub developer guide - C2D].
   
   > [!NOTE]
   > Cuando se utiliza HTTP en lugar de MQTT o AMQP como transporte, Hola `ReceiveAsync` método vuelve inmediatamente. patrón de Hello admitida para los mensajes en la nube al dispositivo con HTTP es dispositivos conectados de forma intermitente que comprobación para mensajes con poca frecuencia (menor que cada 25 minutos). Emitir más HTTP recibe resultados en las solicitudes de centro de IoT limitación Hola. Para obtener más información acerca de las diferencias de hello entre soporte MQTT, AMQP y HTTP y la limitación de centro de IoT, vea hello [Guía del desarrollador de centro de IoT][IoT Hub developer guide - C2D].
   > 
   > 
2. Agregar Hola siguiente método Hola **Main** método, justo antes de hello `Console.ReadLine()` línea:
   
        ReceiveC2dAsync();

> [!NOTE]
> Por simplificar, este tutorial no implementa ninguna directiva de reintentos. En el código de producción, debe implementar directivas de reintento (por ejemplo, retroceso exponencial), como se indica en el artículo de MSDN de hello [control de errores transitorios].
> 
> 

## <a name="send-a-cloud-to-device-message"></a>Envío de mensajes de nube a dispositivo
En esta sección, se escribe una aplicación de consola .NET que envía mensajes en la nube al dispositivo toohello del dispositivo.

1. En la solución de Visual Studio actual hello, crear un proyecto de aplicación de escritorio de Visual C# mediante hello **aplicación de consola** plantilla de proyecto. Proyecto de hello Name **SendCloudToDevice**.
   
    ![Nuevo proyecto en Visual Studio][20]
2. En el Explorador de soluciones, haga clic en soluciones de hello y, a continuación, haga clic en **administrar paquetes de NuGet para la solución... **. 
   
    Esta acción abre hello **administrar paquetes de NuGet** ventana.
3. Busque **Microsoft.Azure.Devices**, haga clic en **instalar**y acepte los términos de Hola de uso. 
   
    Esta descarga, se instala y se agrega una referencia toohello [paquete de NuGet del SDK de servicios de Azure IoT].

4. Agregue los siguiente hello `using` declaración en la parte superior de Hola de hello **Program.cs** archivo:
   
        using Microsoft.Azure.Devices;
5. Agregar Hola después campos toohello **programa** clase. Sustituir el valor de marcador de posición de hello con la cadena de conexión de base de datos central de hello IoT desde [empezar a trabajar con el centro de IoT]:
   
        static ServiceClient serviceClient;
        static string connectionString = "{iot hub connection string}";
6. Agregar Hola siguiendo el método toohello **programa** clase:
   
        private async static Task SendCloudToDeviceMessageAsync()
        {
            var commandMessage = new Message(Encoding.ASCII.GetBytes("Cloud toodevice message."));
            await serviceClient.SendAsync("myFirstDevice", commandMessage);
        }
   
    Este método envía un nuevo dispositivo de toohello de mensaje en la nube al dispositivo con el Id. de hello, `myFirstDevice`. Cambiar este parámetro únicamente si se ha modificado desde Hola utilizada en [empezar a trabajar con el centro de IoT].
7. Por último, agregue Hola después líneas toohello **Main** método:
   
        Console.WriteLine("Send Cloud-to-Device message\n");
        serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
   
        Console.WriteLine("Press any key toosend a C2D message.");
        Console.ReadLine();
        SendCloudToDeviceMessageAsync().Wait();
        Console.ReadLine();
8. Desde Visual Studio, haga clic con el botón derecho en la solución y seleccione **Establecer proyectos de inicio**. Seleccione **proyectos de inicio múltiples**, a continuación, seleccione hello **iniciar** acción para **ReadDeviceToCloudMessages**, **SimulatedDevice**, y **SendCloudToDevice**.
9. Presione **F5**. Deberían iniciarse las tres aplicaciones. Seleccione hello **SendCloudToDevice** windows y presione **ENTRAR**. Debería ver con la aplicación de dispositivo de hello recibe el mensaje de saludo.
   
   ![Aplicación que recibe el mensaje][21]

## <a name="receive-delivery-feedback"></a>Recepción de comentarios de entrega
Es confirmaciones de entrega (o expiración) de posibles toorequest centro de IoT para cada mensaje en la nube al dispositivo. Esta tooeasily de back-end de soluciones de opción habilita Hola informar a la lógica de reintento o compensación. Para obtener más información sobre los comentarios de la nube al dispositivo, consulte hello [Guía del desarrollador de centro de IoT][IoT Hub developer guide - C2D].

En esta sección, se modifica hello **SendCloudToDevice** comentarios de toorequest la aplicación y recibir desde el centro de IoT.

1. En Visual Studio, en hello **SendCloudToDevice** proyecto de equipo y agregar Hola siguiendo el método toohello **programa** clase.
   
        private async static void ReceiveFeedbackAsync()
        {
            var feedbackReceiver = serviceClient.GetFeedbackReceiver();
   
            Console.WriteLine("\nReceiving c2d feedback from service");
            while (true)
            {
                var feedbackBatch = await feedbackReceiver.ReceiveAsync();
                if (feedbackBatch == null) continue;
   
                Console.ForegroundColor = ConsoleColor.Yellow;
                Console.WriteLine("Received feedback: {0}", string.Join(", ", feedbackBatch.Records.Select(f => f.StatusCode)));
                Console.ResetColor();
   
                await feedbackReceiver.CompleteAsync(feedbackBatch);
            }
        }
   
    Tenga en cuenta este patrón de recepción es Hola mismos mensajes de nube al dispositivo tooreceive usa uno de aplicación de dispositivo de hello.
2. Agregar Hola siguiente método Hola **Main** método, justo después de hello `serviceClient = ServiceClient.CreateFromConnectionString(connectionString)` línea:
   
        ReceiveFeedbackAsync();
3. comentarios de toorequest para la entrega de saludo del mensaje en la nube al dispositivo, tiene toospecify una propiedad en hello **SendCloudToDeviceMessageAsync** método. Agregar Hola después de línea, justo después de hello `var commandMessage = new Message(...);` línea:
   
        commandMessage.Ack = DeliveryAcknowledgement.Full;
4. Ejecutar aplicaciones de hello presionando **F5**. Debería ver que se inician las tres aplicaciones. Seleccione hello **SendCloudToDevice** windows y presione **ENTRAR**. Debería ver Hola de mensajes que se reciben por aplicación de dispositivo de hello y después de unos segundos, recibe el mensaje de Hola su **SendCloudToDevice** aplicación.
   
   ![Aplicación que recibe el mensaje][22]

> [!NOTE]
> Por simplificar, este tutorial no implementa ninguna directiva de reintentos. En el código de producción, debe implementar directivas de reintento (por ejemplo, retroceso exponencial), como se indica en el artículo de MSDN de hello [control de errores transitorios].
> 
> 

## <a name="next-steps"></a>Pasos siguientes
En este tutorial, se habrá aprendido cómo toosend y recibir mensajes en la nube al dispositivo. 

ver ejemplos de toosee de soluciones completas de-to-end que usar el centro de IoT, consulte [Azure IoT Suite].

toolearn más sobre el desarrollo de soluciones con el centro de IoT, vea hello [Guía del desarrollador de centro de IoT].

<!-- Images -->
[20]: ./media/iot-hub-csharp-csharp-c2d/create-identity-csharp1.png
[21]: ./media/iot-hub-csharp-csharp-c2d/sendc2d1.png
[22]: ./media/iot-hub-csharp-csharp-c2d/sendc2d2.png

<!-- Links -->

[paquete NuGet del SDK de Servicios IoT de Azure]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
[Transient Fault Handling]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[IoT Hub developer guide - C2D]: iot-hub-devguide-messaging.md

[Guía para desarrolladores de IoT Hub]: iot-hub-devguide.md
[Introducción al Centro de IoT]: iot-hub-csharp-csharp-getstarted.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[Documentación del Conjunto de aplicaciones de IoT]: https://docs.microsoft.com/en-us/azure/iot-suite/
[SDK de dispositivos IoT de Azure]: iot-hub-devguide-sdks.md