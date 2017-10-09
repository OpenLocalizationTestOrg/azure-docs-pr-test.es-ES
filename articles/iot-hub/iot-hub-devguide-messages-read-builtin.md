---
title: "punto de conexión integrado de aaaUnderstand Hola centro de IoT de Azure | Documentos de Microsoft"
description: "Guía del desarrollador: describe cómo toouse Hola integrados, mensajes de dispositivo a la nube de leer de punto de conexión compatible de concentrador de eventos."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: dobett
ms.openlocfilehash: 15484c1b1828151ffcae5f4a1407264374223da1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="read-device-to-cloud-messages-from-hello-built-in-endpoint"></a>Leer los mensajes de dispositivo para la nube de extremo predefinido Hola

De forma predeterminada, los mensajes son el punto de conexión de toohello enrutado integrados a nivel de servicio (**mensajes de eventos**), que es compatible con [centros de eventos][lnk-event-hubs]. Este punto de conexión está actualmente solo exponen mediante hello [AMQP] [ lnk-amqp] protocolo en el puerto 5671. Un centro de IoT expone Hola tras propiedades tooenable se toocontrol Hola extremo de mensajería compatible de concentrador de eventos predefinido **mensajes de eventos**.

| Propiedad            | Descripción |
| ------------------- | ----------- |
| **Número de particiones** | Establezca esta propiedad en el número de hello toodefine de creación de [particiones] [ lnk-event-hub-partitions] para la recopilación de eventos de dispositivo a la nube. |
| **Tiempo de retención**  | Esta propiedad especifica cuánto tiempo, en días, IoT Hub conserva los mensajes. valor predeterminado de Hello es un día, pero puede ser mayor tooseven días. |

Centro de IoT también permite toomanage grupos de consumidores en hello integrada dispositivo a la nube extremo de recepción.

De forma predeterminada, todos los mensajes que no coinciden de forma explícita una regla de enrutamiento de mensajes se escriben toohello punto de conexión integrados. Si deshabilita esta ruta de reserva, los mensajes que no cumplen explícitamente ninguna reglas de enrutamiento de mensajes se quitan.

Puede modificar el tiempo de retención de hello, ya sea mediante programación a través de hello [API de REST de proveedor de recursos de centro de IoT][lnk-resource-provider-apis], o mediante el uso de hello [portal de Azure] [ lnk-management-portal].

Centro de IoT expone hello **mensajes de eventos** mensajes de dispositivo a la nube de hello tooread recibidos por el centro de servicios de extremo predefinido para el back-end. Se trata de eventos concentrador compatible, lo que le permite toouse cualquier servicio de centros de eventos de hello mecanismos hello es compatible con para leer los mensajes.

## <a name="read-from-hello-built-in-endpoint"></a>Leer desde el punto de conexión integrados de Hola

Cuando usas hello [SDK del Bus de servicio de Azure para .NET] [ lnk-servicebus-sdk] o hello [centros de eventos - Host procesador de eventos][lnk-eventprocessorhost], puede usar cualquier conexión de centro de IoT cadenas con los permisos correctos de Hola. A continuación, utilice **mensajes de eventos** como nombre de concentrador de eventos de Hola.

Cuando usas SDK (o integraciones de producto) que no son conscientes de centro de IoT, debe recuperar un punto de conexión compatible de concentrador de eventos y un nombre de concentrador de eventos-compatible con opciones de configuración de centro de IoT de hello en hello [portal de Azure] [ lnk-management-portal]:

1. En la hoja de centro de IoT de hello, haga clic en **extremos**.
1. Hola **extremos integrados** sección, haga clic en **eventos**. Hello hoja contiene Hola siguientes valores: **punto de conexión de concentrador de eventos-compatible con**, **nombre de concentrador de eventos-compatible con**, **particiones**, **detiempoderetención**, y **grupos de consumidores**.

    ![Configuración de dispositivo a nube][img-eventhubcompatible]

Hola IoT Hub SDK requiere Hola nombre de punto de conexión de centro de IoT, que es **mensajes de eventos** tal y como se muestra en hello **extremos** hoja.

Si requiere Hola SDK que usa un **Hostname** o **Namespace** valor, quite el esquema de Hola Hola **punto de conexión de concentrador de eventos-compatible con**. Por ejemplo, si el punto de conexión compatible de concentrador de eventos es **sb://iothub-ns-myiothub-1234.servicebus.windows.net/**, hello **Hostname** sería  **el centro de IOT-ns-myiothub-1234.servicebus.windows.net**, hello y **Namespace** sería **el centro de IOT-ns-myiothub-1234**.

A continuación, puede usar cualquier directiva de acceso compartido que tiene hello **ServiceConnect** toohello tooconnect de permisos especificado concentrador de eventos.

Si necesita toobuild una cadena de conexión de concentrador de eventos mediante el uso de la información anterior de hello, use Hola siguiente patrón:

`Endpoint={Event Hub-compatible endpoint};SharedAccessKeyName={iot hub policy name};SharedAccessKey={iot hub policy key}`

SDK de Hello e integraciones que pueden usar con los puntos de conexión compatible de concentrador de eventos que expone el centro de IoT incluye elementos de Hola Hola lista siguiente:

* [Cliente de Event Hubs de Java](https://github.com/hdinsight/eventhubs-client).
* [Spout de Apache Storm](../hdinsight/hdinsight-storm-develop-csharp-event-hub-topology.md). Puede ver hello [apetezca charlar un origen](https://github.com/apache/storm/tree/master/external/storm-eventhubs) en GitHub.
* [Integración de Apache Spark](../hdinsight/hdinsight-apache-spark-eventhub-streaming.md).

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre los puntos de conexión de IoT Hub, vea [Puntos de conexión de IoT Hub][lnk-endpoints].

Hola [Introducción] [ lnk-get-started] los tutoriales muestra cómo toosend mensajes de dispositivo para la nube de simulación dispositivos y leen los mensajes de Hola de extremo predefinido Hola. Para obtener información más detallada, vea hello [mensajes de dispositivo a la nube del centro de IoT de proceso mediante las rutas de] [ lnk-d2c-tutorial] tutorial.

Si desea que tooroute su dispositivo a la nube mensajes toocustom extremos, vea [utilizar las rutas de mensajes y los extremos personalizados para los mensajes de dispositivo para la nube][lnk-custom].

[img-eventhubcompatible]: ./media/iot-hub-devguide-messages-read-builtin/eventhubcompatible.png

[lnk-custom]: iot-hub-devguide-messages-read-custom.md
[lnk-get-started]: iot-hub-get-started.md
[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-resource-provider-apis]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-event-hubs]: http://azure.microsoft.com/documentation/services/event-hubs/
[lnk-management-portal]: https://portal.azure.com
[lnk-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md
[lnk-event-hub-partitions]: ../event-hubs/event-hubs-features.md#partitions
[lnk-servicebus-sdk]: https://www.nuget.org/packages/WindowsAzure.ServiceBus
[lnk-eventprocessorhost]: http://blogs.msdn.com/b/servicebus/archive/2015/01/16/event-processor-host-best-practices-part-1.aspx
[lnk-amqp]: https://www.amqp.org/
