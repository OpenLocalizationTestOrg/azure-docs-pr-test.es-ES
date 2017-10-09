---
title: mensajes de dispositivo a la nube de Azure IoT Hub aaaProcess mediante las rutas (. NET) | Documentos de Microsoft
description: "¿Cómo tooprocess mensajes de dispositivo a la nube del centro de IoT mediante las reglas de enrutamiento y los extremos personalizados toodispatch mensajes tooother servicios de back-end."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 5177bac9-722f-47ef-8a14-b201142ba4bc
ms.service: iot-hub
ms.devlang: csharp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: c1dd5be04ca30c65af2be466ba6c8c1858333154
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="process-iot-hub-device-to-cloud-messages-using-routes-net"></a>Procesamiento de mensajes de dispositivo a nube de IoT Hub mediante rutas (.NET)

[!INCLUDE [iot-hub-selector-process-d2c](../../includes/iot-hub-selector-process-d2c.md)]

Este tutorial se basa en hello [empezar a trabajar con el centro de IoT] tutorial. tutorial de Hello:

* Muestra cómo toouse enrutamiento mensajes del dispositivo a la nube de toodispatch las reglas de una manera fácil y de configuración.
* Muestra cómo tooisolate mensajes interactivo que requieren acción inmediata de solución de hello back-end para su posterior procesamiento. Por ejemplo, un dispositivo puede enviar un mensaje de alarma que desencadena la inserción de una incidencia en un sistema CRM. Por el contrario, los mensajes de punto de datos, como los datos de telemetría de temperatura, se envían a un motor de análisis.

Al final de Hola de este tutorial, ejecutar tres aplicaciones de consola. NET:

* **SimulatedDevice**, una versión modificada de la aplicación hello creado en hello [empezar a trabajar con el centro de IoT] tutorial envía mensajes de dispositivo a la nube de punto de datos cada segundo e interactivo dispositivo a la nube mensajes cada 10 segundos.
* **ReadDeviceToCloudMessages** que muestra Hola no críticos telemetría enviado por la aplicación de dispositivo.
* **ReadCriticalQueue** anular pone en cola mensajes críticos de saludo enviados por la aplicación de dispositivo de una cola de Bus de servicio. Esta cola es Centro de IoT toohello adjunto.

> [!NOTE]
> El Centro de IoT ofrece compatibilidad con el SDK para muchas plataformas de dispositivos y lenguajes, entre los que se incluyen C, Java y JavaScript. toolearn cómo tooreplace Hola dispositivo simulado en este tutorial con un dispositivo físico, vea hello [Centro para desarrolladores de Azure IoT].

toocomplete este tutorial, necesita Hola siguientes:

* Visual Studio 2015 o Visual Studio 2017.
* Una cuenta de Azure activa. <br/>En caso de no tener ninguna, puede crear una [cuenta gratuita](https://azure.microsoft.com/free/) en tan solo unos minutos.

También se dan por sentados ciertos conocimientos sobre [Azure Storage] y [Azure Service Bus].

## <a name="send-interactive-messages"></a>Envío de mensajes interactivos

Modificar la aplicación de dispositivo de Hola que creó en hello [empezar a trabajar con el centro de IoT] toooccasionally tutorial enviar mensajes interactivos.

En Visual Studio, en hello **SimulatedDevice** proyecto de equipo y reemplace hello `SendDeviceToCloudMessagesAsync` método con el siguiente código de hello:

```csharp
private static async void SendDeviceToCloudMessagesAsync()
{
    double minTemperature = 20;
    double minHumidity = 60;
    Random rand = new Random();

    while (true)
    {
        double currentTemperature = minTemperature + rand.NextDouble() * 15;
        double currentHumidity = minHumidity + rand.NextDouble() * 20;

        var telemetryDataPoint = new
        {
            deviceId = "myFirstDevice",
            temperature = currentTemperature,
            humidity = currentHumidity
        };
        var messageString = JsonConvert.SerializeObject(telemetryDataPoint);
        string levelValue;

        if (rand.NextDouble() > 0.7)
        {
            messageString = "This is a critical message";
            levelValue = "critical";
        }
        else
        {
            levelValue = "normal";
        }
        
        var message = new Message(Encoding.ASCII.GetBytes(messageString));
        message.Properties.Add("level", levelValue);
        
        await deviceClient.SendEventAsync(message);
        Console.WriteLine("{0} > Sent message: {1}", DateTime.Now, messageString);

        await Task.Delay(1000);
    }
}
```

Este método agrega al azar propiedad hello `"level": "critical"` toomessages enviados por dispositivo de hello, que simula un mensaje que requiere una acción inmediata por hello solución back-end. aplicación de dispositivo de Hello pasa esta información en las propiedades de mensaje de Hola, en lugar de en el cuerpo del mensaje Hola, para que ese centro de IoT pueda enrutar el destino del mensaje adecuado de toohello de mensaje de Hola.

> [!NOTE]
> Puede utilizar mensajes de tooroute de propiedades de mensaje para varios escenarios incluidos frío-path, además de procesamiento toohello ruta de acceso activa en el ejemplo se muestra aquí.

> [!NOTE]
> Para simplificar Hola simplicidad, este tutorial no implementa ninguna directiva de reintento. En el código de producción, debe implementar una directiva de reintentos como retroceso exponencial, tal como se sugiere en el artículo MSDN de hello [control de errores transitorios].

## <a name="route-messages-tooa-queue-in-your-iot-hub"></a>Cola de mensajes tooa de ruta en el centro de IoT

En esta sección:

* Creará una cola de Service Bus.
* Conéctelo tooyour centro de IoT.
* Configurar la cola de toohello IoT hub toosend mensajes basada en presencia de Hola de una propiedad de mensaje de bienvenida.

Para obtener más información acerca de cómo tooprocess mensajes desde las colas de Bus de servicio, consulte [empezar a trabajar con colas][Service Bus queue].

1. Cree una cola de Service Bus como se describe en [Introducción a las colas][Service Bus queue]. Hola cola debe ser Hola misma suscripción y región que el centro de IoT. Tome nota del nombre de espacio de nombres y la cola de Hola.

    > [!NOTE]
    > Las colas y los temas de Service Bus usados como puntos de conexión de IoT Hub no deben tener habilitadas las opciones **Sesiones** o **Detección de duplicados**. Si cualquiera de estas opciones están habilitada, el punto de conexión de hello aparece como **inaccesible** Hola portal de Azure.

2. En Hola portal de Azure, abra el centro de IoT y haga clic en **extremos**.
    
    ![Puntos de conexión en IoT Hub][30]

3. Hola **extremos** hoja, haga clic en **agregar** en Hola tooadd superior su centro de IoT tooyour de cola. El punto de conexión de nombre hello **CriticalQueue** y usar Hola listas desplegables tooselect **cola de Service Bus**, Hola espacio de nombres de Bus de servicio en el que reside la cola y Hola nombre de la cola. Cuando haya terminado, haga clic en **guardar** final Hola.
    
    ![Adición de un punto de conexión][31]
    
4. Ahora haga clic en **Routes** (Rutas) en IoT Hub. Haga clic en **agregar** en parte superior de Hola de hello hoja toocreate agrega una regla de enrutamiento que enruta los mensajes de cola que toohello se acaba. Seleccione **DeviceTelemetry** como origen de Hola de datos. Escriba `level="critical"` como condición de hello y elija la cola de Hola que acaba de agregar como un extremo personalizado como Hola extremo de la regla de enrutamiento. Cuando haya terminado, haga clic en **guardar** final Hola.
    
    ![Adición de una ruta][32]
    
    Asegúrese de que la ruta de reserva de Hola se establece demasiado**ON**. Este valor es la configuración predeterminada de Hola para un centro de IoT.
    
    ![Ruta de reserva][33]

## <a name="read-from-hello-queue-endpoint"></a>Leer desde el punto de conexión de hello cola

En esta sección, se leen mensajes de Hola de extremo de la cola de Hola.

1. En Visual Studio, agregue una solución actual de la toohello de proyectos Visual C# escritorio clásico de Windows, mediante el uso de hello **aplicación de consola (.NET Framework)** plantilla de proyecto. Proyecto de hello Name **ReadCriticalQueue**.

2. En el Explorador de soluciones, haga clic en hello **ReadCriticalQueue** del proyecto y, a continuación, haga clic en **administrar paquetes de NuGet**. Esta operación muestra hello **Administrador de paquetes de NuGet** ventana.

3. Busque **WindowsAzure.ServiceBus**, haga clic en **instalar**y acepte los términos de Hola de uso. Esta operación se descarga, se instala y agrega una referencia toohello Bus de servicio de Azure, con todas sus dependencias.

4. Agregue los siguiente hello **mediante** las instrucciones en la parte superior de Hola de hello **Program.cs** archivo:
   
    ```csharp
    using System.IO;
    using Microsoft.ServiceBus.Messaging;
    ```

5. Por último, agregue Hola después líneas toohello **Main** método. Sustituya la cadena de conexión de hello con **escuchar** permisos para hello cola:
   
    ```csharp
    Console.WriteLine("Receive critical messages. Ctrl-C tooexit.\n");
    var connectionString = "{service bus listen string}";
    var queueName = "{queue name}";
    
    var client = QueueClient.CreateFromConnectionString(connectionString, queueName);

    client.OnMessage(message =>
        {
            Stream stream = message.GetBody<Stream>();
            StreamReader reader = new StreamReader(stream, Encoding.ASCII);
            string s = reader.ReadToEnd();
            Console.WriteLine(String.Format("Message body: {0}", s));
        });
        
    Console.ReadLine();
    ```

## <a name="run-hello-applications"></a>Ejecutar aplicaciones de Hola
Ahora está listo toorun aplicaciones de Hola.

1. En el Explorador de soluciones de Visual Studio, haga clic con el botón derecho en la solución y seleccione **Establecer proyectos de inicio**. Seleccione **proyectos de inicio múltiples**, a continuación, seleccione **iniciar** como acción de Hola para hello **ReadDeviceToCloudMessages**, **SimulatedDevice**, y **ReadCriticalQueue** proyectos.
2. Presione **F5** toostart Hola tres aplicaciones de consola. Hola **ReadDeviceToCloudMessages** aplicación tiene solo no críticos mensajes enviados desde hello **SimulatedDevice** hello y aplicación **ReadCriticalQueue** aplicación sólo tiene mensajes críticos.
   
   ![Tres aplicaciones de consola][50]

## <a name="next-steps"></a>Pasos siguientes
En este tutorial, ha aprendido cómo tooreliably enviar mensajes del dispositivo a la nube mediante la funcionalidad de enrutamiento de mensajes de Hola de centro de IoT.

Hola [cómo mensajes toosend en la nube al dispositivo con el centro de IoT] [ lnk-c2d] muestra cómo toosend mensajes tooyour dispositivos desde el back-end de soluciones.

ver ejemplos de toosee de soluciones completas de-to-end que usar el centro de IoT, consulte [Azure IoT Suite][lnk-suite].

toolearn más sobre el desarrollo de soluciones con el centro de IoT, vea hello [Guía del desarrollador de centro de IoT].

toolearn más información acerca de enrutamiento de mensajes en el centro de IoT, consulte [enviar y recibir mensajes con el centro de IoT][lnk-devguide-messaging].

<!-- Images. -->
[50]: ./media/iot-hub-csharp-csharp-process-d2c/run1.png
[30]: ./media/iot-hub-csharp-csharp-process-d2c/click-endpoints.png
[31]: ./media/iot-hub-csharp-csharp-process-d2c/endpoint-creation.png
[32]: ./media/iot-hub-csharp-csharp-process-d2c/route-creation.png
[33]: ./media/iot-hub-csharp-csharp-process-d2c/fallback-route.png

<!-- Links -->
[Service Bus queue]: ../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md
[Azure Storage]: https://azure.microsoft.com/documentation/services/storage/
[Azure Service Bus]: https://azure.microsoft.com/documentation/services/service-bus/
[Guía del desarrollador de centro de IoT]: iot-hub-devguide.md
[empezar a trabajar con el centro de IoT]: iot-hub-csharp-csharp-getstarted.md
[lnk-devguide-messaging]: iot-hub-devguide-messaging.md
[Centro para desarrolladores de Azure IoT]: https://azure.microsoft.com/develop/iot
[control de errores transitorios]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-c2d]: iot-hub-csharp-csharp-process-d2c.md
[lnk-suite]: https://azure.microsoft.com/documentation/suites/iot-suite/
