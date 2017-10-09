---
title: "supervisión de operaciones de centro de IoT aaaAzure | Documentos de Microsoft"
description: "Cómo las operaciones de centro de IoT de Azure toouse supervisión toomonitor Hola estado de las operaciones en el centro de IoT en tiempo real."
services: iot-hub
documentationcenter: 
author: nberdy
manager: timlt
editor: 
ms.assetid: a299f3a5-b14d-4586-9c3b-44aea14ed013
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: nberdy
ms.openlocfilehash: a0b233ef2d9bd0827e19fa30fdbdd49b2b61b813
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="iot-hub-operations-monitoring"></a>Supervisión de operaciones de IoT Hub

Supervisión de operaciones de centro de IoT permite toomonitor Hola estado de las operaciones en el centro de IoT en tiempo real. IoT Hub realiza el seguimiento de eventos a través de varias categorías de operaciones. Puede optar por enviar eventos de uno o más categorías tooan punto de conexión de su centro de IoT para su procesamiento. Puede supervisar los datos de Hola para errores o establecer un procesamiento más complejo basándose en patrones de datos.

IoT Hub supervisa seis categorías de eventos:

* Operaciones de identidad de dispositivos
* Telemetría de dispositivo
* Mensajes de nube a dispositivo
* Conexiones
* Cargas de archivos
* Enrutamiento de mensajes

## <a name="how-tooenable-operations-monitoring"></a>La supervisión de operaciones de tooenable

1. Cree un Centro de IoT. Encontrará instrucciones sobre cómo toocreate un centro de IoT en hello [Introducción] [ lnk-get-started] guía.

1. Abra la hoja de Hola de su centro de IoT. Desde allí, haga clic en **Supervisión de operaciones**.

    ![Supervisión de configuración en el portal de Hola de operaciones de acceso][1]

1. Seleccione Hola supervisión categorías desea toomonitor y, a continuación, haga clic en **guardar**. Hello eventos están disponibles para leer del punto de conexión de hello compatible con el concentrador de eventos enumerado en **configuración de supervisión**. Hello centro de IoT se denomina `messages/operationsmonitoringevents`.

    ![Configurar operaciones de supervisión en la instancia de IoT Hub][2]

> [!NOTE]
> Seleccionar **detallado** supervisión de hello **conexiones** categoría hace centro de IoT toogenerate mensajes de diagnóstico adicionales. Para todas las demás categorías, Hola **detallado** cantidad Hola de centro de IoT de la información de cambios de configuración incluyen en cada mensaje de error.

## <a name="event-categories-and-how-toouse-them"></a>Categorías de eventos y cómo toouse ellos

Cada categoría de supervisión de operaciones realiza el seguimiento de un tipo diferente de interacción con IoT Hub, y cada categoría de supervisión tiene un esquema que define cómo se estructuran los eventos de esa categoría.

### <a name="device-identity-operations"></a>Operaciones de identidad de dispositivos

categoría de las operaciones de identidad de dispositivo de Hello realiza un seguimiento de errores que se producen al intentar toocreate, actualizar o eliminar una entrada de registro de la identidad de su centro de IoT. El seguimiento de esta categoría resulta útil para los escenarios de aprovisionamiento.

```json
{
    "time": "UTC timestamp",
        "operationName": "create",
        "category": "DeviceIdentityOperations",
        "level": "Error",
        "statusCode": 4XX,
        "statusDescription": "MessageDescription",
        "deviceId": "device-ID",
        "durationMs": 1234,
        "userAgent": "userAgent",
        "sharedAccessPolicy": "accessPolicy"
}
```

### <a name="device-telemetry"></a>Telemetría de dispositivo

categoría de telemetría de dispositivo de Hello realiza un seguimiento de errores que se producen en el centro de IoT de Hola y canalización de telemetría toohello relacionados. Esta categoría incluye los errores que se producen al enviar eventos de telemetría (por ejemplo, la limitación) y recibir eventos de telemetría (por ejemplo, un lector no autorizado). Esta categoría no puede capturar errores causados por el código que se ejecuta en el propio dispositivo Hola.

```json
{
        "messageSizeInBytes": 1234,
        "batching": 0,
        "protocol": "Amqp",
        "authType": "{\"scope\":\"device\",\"type\":\"sas\",\"issuer\":\"iothub\"}",
        "time": "UTC timestamp",
        "operationName": "ingress",
        "category": "DeviceTelemetry",
        "level": "Error",
        "statusCode": 4XX,
        "statusType": 4XX001,
        "statusDescription": "MessageDescription",
        "deviceId": "device-ID",
        "EventProcessedUtcTime": "UTC timestamp",
        "PartitionId": 1,
        "EventEnqueuedUtcTime": "UTC timestamp"
}
```

### <a name="cloud-to-device-commands"></a>Comandos de nube a dispositivo

categoría de comandos en la nube al dispositivo de Hello realiza un seguimiento de errores que se producen en el centro de IoT de Hola y canalización de mensaje en la nube a dispositivo toohello relacionados. Esta categoría incluye errores que se producen al enviar mensajes de nube a dispositivo (por ejemplo, un remitente no autorizado), recibir mensajes de nube a dispositivo (por ejemplo, el número de entregas superado) y recibir mensajes de nube a dispositivo (por ejemplo, comentarios expirados). Esta categoría no detecta errores desde un dispositivo que controla incorrectamente un mensaje en la nube al dispositivo si el mensaje de saludo en la nube al dispositivo se ha entregado correctamente.

```json
{
    "messageSizeInBytes": 1234,
    "authType": "{\"scope\":\"hub\",\"type\":\"sas\",\"issuer\":\"iothub\"}",
    "deliveryAcknowledgement": 0,
    "protocol": "Amqp",
    "time": " UTC timestamp",
    "operationName": "ingress",
    "category": "C2DCommands",
    "level": "Error",
    "statusCode": 4XX,
    "statusType": 4XX001,
    "statusDescription": "MessageDescription",
    "deviceId": "device-ID",
    "EventProcessedUtcTime": "UTC timestamp",
    "PartitionId": 1,
    "EventEnqueuedUtcTime": “UTC timestamp"
}
```

### <a name="connections"></a>Conexiones

categoría de las conexiones de Hello realiza un seguimiento de errores que se producen cuando los dispositivos conectarán o desconexión de un centro de IoT. El seguimiento de esta categoría resulta útil para identificar intentos de conexión no autorizados y para realizar el seguimiento de las situaciones en que una conexión se pierde para los dispositivos en las áreas de conectividad deficiente.

```json
{
    "durationMs": 1234,
    "authType": "{\"scope\":\"hub\",\"type\":\"sas\",\"issuer\":\"iothub\"}",
    "protocol": "Amqp",
    "time": " UTC timestamp",
    "operationName": "deviceConnect",
    "category": "Connections",
    "level": "Error",
    "statusCode": 4XX,
    "statusType": 4XX001,
    "statusDescription": "MessageDescription",
    "deviceId": "device-ID"
}
```

### <a name="file-uploads"></a>Cargas de archivos

categoría de carga de archivo Hello realiza un seguimiento de errores que se producen en el centro de IoT de Hola y funcionalidad de carga de toofile relacionados. Esta categoría incluye lo siguiente:

* Errores que se producen con hello URI de SAS, como cuándo expira antes de que un dispositivo notifica al concentrador de Hola de una carga completada.
* No se pudo cargas notificadas por dispositivo de Hola.
* Errores que se producen cuando no se encuentra un archivo en el almacenamiento durante la creación del mensaje de notificación de IoT Hub.

Esta categoría no puede capturar los errores ocurridos directamente al dispositivo de hello está cargando un archivo toostorage.

```json
{
    "authType": "{\"scope\":\"hub\",\"type\":\"sas\",\"issuer\":\"iothub\"}",
    "protocol": "HTTP",
    "time": " UTC timestamp",
    "operationName": "ingress",
    "category": "fileUpload",
    "level": "Error",
    "statusCode": 4XX,
    "statusType": 4XX001,
    "statusDescription": "MessageDescription",
    "deviceId": "device-ID",
    "blobUri": "http//bloburi.com",
    "durationMs": 1234
}
```

### <a name="message-routing"></a>Enrutamiento de mensajes

categoría de enrutamiento de mensajes de Hola realiza un seguimiento de errores que se producen durante la evaluación de la ruta de mensajes y el estado de punto de conexión según lo percibido por centro de IoT. Esta categoría incluye eventos, como cuando se evalúa como una regla demasiado "undefined", al centro de IoT marca un punto de conexión como cola y cualquier otro error recibido de un punto de conexión. Esta categoría no incluye errores específicos acerca de los mensajes de Hola a sí mismos (por ejemplo, el dispositivo errores de limitación), que se notifican en la categoría de "telemetría de dispositivo" Hola.

```json
{
    "messageSizeInBytes": 1234,
    "time": "UTC timestamp",
    "operationName": "ingress",
    "category": "routes",
    "level": "Error",
    "deviceId": "device-ID",
    "messageId": "ID of message",
    "routeName": "myroute",
    "endpointName": "myendpoint",
    "details": "ExternalEndpointDisabled"
}
```

## <a name="view-events"></a>Ver eventos

Puede usar hello *el centro de IOT explorador* tooquickly de la herramienta de prueba que el centro de IoT está generando eventos de supervisión. Hola tooinstall herramienta, consulte las instrucciones de Hola Hola [el centro de IOT explorador] [ lnk-iothub-explorer] repositorio de GitHub.

1. Realizar Hola seguro **conexiones** supervisión categoría se establece demasiado**detallado** en el portal de Hola.

1. En una línea de comandos, ejecute hello siguientes tooread de comando de hello extremo de supervisión:

    ```
    iothub-explorer monitor-ops --login {your iothubowner connection string}
    ```

1. En otro símbolo, ejecute hello después comando toosimulate un dispositivo que envía mensajes de dispositivo para la nube:

    ```
    iothub-explorer simulate-device {your device name} --send "My test message" --login {your iothubowner connection string}
    ```

1. símbolo primera Hello muestra eventos de supervisión de hello tooyour centro de IoT se conecta el dispositivo simulado Hola.

## <a name="connect-toohello-monitoring-endpoint"></a>Conectar toohello extremo de supervisión

Hola supervisión de extremo en el centro de IoT es un punto de conexión compatible de concentrador de eventos. Puede utilizar cualquier mecanismo que funciona con los concentradores de eventos tooread supervisión mensajes desde este punto de conexión. Hello en el ejemplo siguiente crea un lector básico que no es adecuado para una implementación de alto rendimiento. Para obtener más información acerca de cómo tooprocess mensajes desde los centros de eventos, vea hello [empezar a trabajar con concentradores de eventos] [ lnk-eventhubs-tutorial] tutorial.

extremo de supervisión de toohello tooconnect, se necesita un nombre de punto de conexión de hello y cadena de conexión. Hola siguientes pasos muestra cómo toofind Hola valores necesarios en el portal de hello:

1. En el portal de hello, navegue tooyour hoja de recursos del centro de IoT.

1. Elija **supervisión de operaciones**y tome nota de hello **nombre de concentrador de eventos-compatible con** y **punto de conexión de concentrador de eventos-compatible con** valores:

    ![Valores del punto de conexión compatible con centro de eventos][img-endpoints]

1. Elija **Directivas de acceso compartido** y, a continuación, elija **servicio**. Tome nota de hello **clave principal** valor:

    ![Clave principal de directiva de acceso compartido del servicio][img-service-key]

Hello siguiente ejemplo de código de C# procede desde Visual Studio **escritorio clásico de Windows** aplicación de consola de C#. proyecto de Hello tiene hello **WindowsAzure.ServiceBus** instalado el paquete de NuGet.

* Reemplace el marcador de posición de cadena de conexión de hello con una cadena de conexión que utiliza hello **punto de conexión de concentrador de eventos-compatible con** y el servicio **clave principal** valores que anotó anteriormente como se muestra en la siguiente Hola ejemplo:

    ```cs
    "Endpoint={your Event Hub-compatible endpoint};SharedAccessKeyName=service;SharedAccessKey={your service primary key value}"
    ```

* Reemplace Hola supervisión de marcador de posición de nombre de punto de conexión con hello **nombre de concentrador de eventos-compatible con** valor que anotó anteriormente.

```cs
class Program
{
    static string connectionString = "{your monitoring endpoint connection string}";
    static string monitoringEndpointName = "{your monitoring endpoint name}";
    static EventHubClient eventHubClient;

    static void Main(string[] args)
    {
        Console.WriteLine("Monitoring. Press Enter key tooexit.\n");

        eventHubClient = EventHubClient.CreateFromConnectionString(connectionString, monitoringEndpointName);
        var d2cPartitions = eventHubClient.GetRuntimeInformation().PartitionIds;
        CancellationTokenSource cts = new CancellationTokenSource();
        var tasks = new List<Task>();

        foreach (string partition in d2cPartitions)
        {
            tasks.Add(ReceiveMessagesFromDeviceAsync(partition, cts.Token));
        }

        Console.ReadLine();
        Console.WriteLine("Exiting...");
        cts.Cancel();
        Task.WaitAll(tasks.ToArray());
    }

    private static async Task ReceiveMessagesFromDeviceAsync(string partition, CancellationToken ct)
    {
        var eventHubReceiver = eventHubClient.GetDefaultConsumerGroup().CreateReceiver(partition, DateTime.UtcNow);
        while (true)
        {
            if (ct.IsCancellationRequested)
            {
                await eventHubReceiver.CloseAsync();
                break;
            }

            EventData eventData = await eventHubReceiver.ReceiveAsync(new TimeSpan(0,0,10));

            if (eventData != null)
            {
                string data = Encoding.UTF8.GetString(eventData.GetBytes());
                Console.WriteLine("Message received. Partition: {0} Data: '{1}'", partition, data);
            }
        }
    }
}
```

## <a name="next-steps"></a>Pasos siguientes
toofurther explorar las capacidades de Hola de centro de IoT, vea:

* [Guía para desarrolladores de IoT Hub][lnk-devguide]
* [Simular un dispositivo con Azure IoT Edge][lnk-iotedge]

<!-- Links and images -->
[1]: media/iot-hub-operations-monitoring/enable-OM-1.png
[2]: media/iot-hub-operations-monitoring/enable-OM-2.png
[img-endpoints]: media/iot-hub-operations-monitoring/monitoring-endpoint.png
[img-service-key]: media/iot-hub-operations-monitoring/service-key.png

[lnk-get-started]: iot-hub-csharp-csharp-getstarted.md
[lnk-diagnostic-metrics]: iot-hub-metrics.md
[lnk-scaling]: iot-hub-scaling.md
[lnk-dr]: iot-hub-ha-dr.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
[lnk-iothub-explorer]: https://github.com/azure/iothub-explorer
[lnk-eventhubs-tutorial]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md