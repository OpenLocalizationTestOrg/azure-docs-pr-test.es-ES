---
title: "mensajería aaaUnderstand centro de IoT de Azure en la nube al dispositivo | Documentos de Microsoft"
description: "Guía del desarrollador - cómo toouse en la nube al dispositivo con el centro de IoT de mensajería. Incluye información acerca del ciclo de vida del mensaje de Hola y opciones de configuración."
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
ms.openlocfilehash: 5c747b50163873d823556a8baa769c4b8f7f8c44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="send-cloud-to-device-messages-from-iot-hub"></a>Envío de mensajes de nube a dispositivo desde IoT Hub

toosend notificaciones unidireccional toohello del dispositivo desde el back-end de soluciones, enviar mensajes de nube para dispositivos de su dispositivo de tooyour IoT hub. Para obtener una explicación de otras opciones de nube a dispositivos compatibles con IoT Hub, consulte [Guía de comunicación de nube a dispositivo][lnk-c2d-guidance].

Se envían mensajes de la nube al dispositivo mediante un punto de conexión orientado al servicio (**/messages/devicebound**). Un dispositivo, a continuación, recibe mensajes de Hola a través de un extremo específico del dispositivo (**/devices/ {deviceId} / mensajes/devicebound**).

Cada mensaje en la nube al dispositivo destinada a un único dispositivo; establecer hello **a** propiedad demasiado**/devices/ {deviceId} / mensajes/devicebound**.

La cola de cada dispositivo puede contener como máximo 50 mensajes de la nube al dispositivo. Intentar toosend más toohello mensajes mismo dispositivo genera un error.

## <a name="hello-cloud-to-device-message-lifecycle"></a>Hola del ciclo de vida del mensaje en la nube a dispositivo

entrega del mensaje de al menos-una vez tooguarantee, centro de IoT conserva los mensajes de la nube al dispositivo en las colas por dispositivo. Dispositivos deben confirmar explícitamente *finalización* para tooremove centro de IoT de Hola cola. Esto garantiza la resistencia frente a errores de dispositivo y de conectividad.

Hello siguiente diagrama muestra gráfico de estado de ciclo de vida de Hola para un mensaje en la nube al dispositivo en el centro de IoT.

![Ciclo de vida de los mensajes de nube a dispositivo][img-lifecycle]

Cuando Hola servicio del centro de IoT envía un dispositivo de tooa de mensaje, el servicio de hello establece el estado del mensaje Hola demasiado**en cola**. Cuando un dispositivo desea demasiado*recibir* un mensaje, el centro de IoT *bloqueos* mensaje de bienvenida (estableciendo el estado de hello demasiado**Invisible**), que permite que otros subprocesos en hello dispositivo toostart recibir otros mensajes. Cuando un subproceso de dispositivo finaliza el procesamiento de Hola de un mensaje, notifica al centro de IoT por *completar* mensaje de saludo. Centro de IoT, a continuación, Establece el estado de hello demasiado**completado**.

Un dispositivo también puede hacer lo siguiente:

* *Rechazar* mensaje Hola, lo que hace el centro de IoT tooset que lo toohello **fallidos** estado. Dispositivos que se conectan a través de hello protocolo MQTT no pueden rechazar mensajes en la nube al dispositivo.
* *Abandonar* mensaje hello, que hace que centro de IoT tooput mensajes de bienvenida en cola de hello, con estado de hello establecido demasiado**en cola**.

Un subproceso podría producir errores tooprocess un mensaje sin notificárselo al centro de IoT. En este caso, automáticamente mensajes de transición de Hola **Invisible** estado atrás toohello **en cola** estado después de un *tiempo de espera de visibilidad (o bloqueo)*. valor predeterminado de Hola de este tiempo de espera es un minuto.

Puede pasar un mensaje de Hola **en cola** y **Invisible** Estados, Hola a lo sumo, número de veces especificado en hello **máximo de entregas** propiedad en el centro de IoT. Después de ese número de transiciones, centro de IoT establece estado Hola de mensaje de saludo demasiado**fallidos**. De forma similar, centro de IoT establece estado Hola de un mensaje demasiado**fallidos** después de la fecha de expiración (consulte [tiempo toolive][lnk-ttl]).

Hola [cómo mensajes toosend en la nube al dispositivo con el centro de IoT] [ lnk-c2d-tutorial] se muestra cómo toosend los mensajes en la nube al dispositivo de hello en la nube y reciban en un dispositivo.

Normalmente, un dispositivo completa un mensaje en la nube al dispositivo cuando Hola pérdida de mensaje de bienvenida no afecta la lógica de la aplicación hello. Por ejemplo, cuando Hola dispositivo conserva el contenido del mensaje Hola localmente o se ha ejecutado correctamente una operación. mensajes de bienvenida también podrían llevar información transitoria, cuyo pérdida no afecta a la funcionalidad de Hola de aplicación hello. A veces, para las tareas de ejecución prolongada, puede completar el mensaje de saludo en la nube al dispositivo después de guardar Hola descripción de la tarea en el almacenamiento local. A continuación, puede notificar a back-end de soluciones de hello con uno o más mensajes de dispositivo para la nube en diferentes fases de progreso de la tarea hello.

## <a name="message-expiration-time-toolive"></a>Caducidad del mensaje (tiempo toolive)

Cada mensaje de nube a dispositivo tiene una fecha de expiración. Esta hora se establece mediante el servicio de hello (Hola **ExpiryTimeUtc** propiedad), o por centro de IoT con hello predeterminada *tiempo toolive* especificada como una propiedad de centro de IoT. Consulte [Opciones de configuración de la nube al dispositivo][lnk-c2d-configuration].

Una ventaja de tootake forma común de expiración del mensaje y evitar el envío de mensajes toodisconnected dispositivos, es tooset toolive valores de hora corta. Este enfoque consigue Hola el mismo resultado que mantiene el estado de conexión de dispositivo de hello, pero más eficaz. Cuando se solicitan los reconocimientos de mensajes, centro de IoT notifica a los dispositivos tooreceive capaz de mensajes, y los dispositivos que no están en línea o se han producido un error.

## <a name="message-feedback"></a>Comentarios de mensajes

Cuando se envía un mensaje en la nube al dispositivo, servicio de hello puede solicitar la entrega de Hola de comentarios de cada mensaje con respecto a Hola estado final de ese mensaje.

| Propiedad Ack | Comportamiento |
| ------------ | -------- |
| **positive** | Centro de IoT genera un mensaje de comentarios si y solo si, mensaje de saludo en la nube al dispositivo alcanza hello **completado** estado. |
| **negative** | Centro de IoT genera un mensaje de comentarios, si y solo si, mensaje de saludo en la nube al dispositivo alcanza hello **fallidos** estado. |
| **full**     | IoT Hub genera un mensaje de comentarios en cualquiera de los casos. |

Si **confirmación** es **completa**y no recibirá un mensaje de comentarios, significa que ese mensaje de comentarios de Hola expirado. Hola servicio no puede saber qué mensaje original toohello problema. En la práctica, un servicio debe asegurarse de que puede procesar los comentarios de Hola antes de que expire. hora de expiración máximo de Hello es dos días, lo que permite una gran cantidad de tiempo tooget Hola servicio ejecutar de nuevo si se produce un error.

Como se explica en [Puntos de conexión][lnk-endpoints], IoT Hub envía los comentarios a través de un punto de conexión accesible desde el servicio (**/messages/servicebound/feedback**) en forma de mensajes. Hello semántica para recibir comentarios de Hola igual que para los mensajes en la nube al dispositivo y ha Hola mismo [Message Lifecycle-español][lnk-lifecycle]. Siempre que sea posible, comentarios de mensaje se realizan por lotes en un único mensaje, con hello siguiendo el formato:

| Propiedad     | Description |
| ------------ | ----------- |
| EnqueuedTime | Marca de tiempo que indica cuándo se creó el mensaje de bienvenida. |
| UserId       | `{iot hub name}` |
| ContentType  | `application/vnd.microsoft.iothub.feedback.json` |

cuerpo de Hello es una matriz JSON serializado de registros, cada uno con hello propiedades siguientes:

| Propiedad           | Description |
| ------------------ | ----------- |
| EnqueuedTimeUtc    | Marca de tiempo que indica cuándo se produjeron resultado de hello de mensaje de bienvenida. Por ejemplo, Hola dispositivo completada o mensaje Hola expirado. |
| OriginalMessageId  | **MessageId** de hello en la nube al dispositivo mensaje toowhich está relacionada con esta información de comentarios. |
| StatusCode         | Cadena necesaria. Se utiliza en los mensajes de comentarios generados por el Centro de IoT. <br/> "Success" <br/> "Expired" <br/> 'DeliveryCountExceeded' <br/> "Rejected" <br/> 'Purged' |
| Descripción        | Valores de cadena para **StatusCode**. |
| deviceId           | **Id. de dispositivo** hello dispositivo de destino de hello en la nube al dispositivo mensaje toowhich está relacionado con este elemento de comentarios. |
| DeviceGenerationId | **DeviceGenerationId** hello dispositivo de destino de hello en la nube al dispositivo mensaje toowhich está relacionado con este elemento de comentarios. |

debe especificar el servicio de Hello un **MessageId** para hello en la nube al dispositivo de mensajes toobe pueda toocorrelate sus comentarios con mensajes de bienvenida del original.

Hello en el ejemplo siguiente se muestra hello cuerpo de un mensaje de comentarios.

```json
[
  {
    "OriginalMessageId": "0987654321",
    "EnqueuedTimeUtc": "2015-07-28T16:24:48.789Z",
    "StatusCode": 0,
    "Description": "Success",
    "DeviceId": "123",
    "DeviceGenerationId": "abcdefghijklmnopqrstuvwxyz"
  },
  {
    ...
  },
  ...
]
```

## <a name="cloud-to-device-configuration-options"></a>Opciones de configuración de la nube al dispositivo

Cada centro de IoT expone Hola siguientes opciones de configuración para la mensajería de nube al dispositivo:

| Propiedad                  | Description | Intervalo y valor predeterminado |
| ------------------------- | ----------- | ----------------- |
| defaultTtlAsIso8601       | TTL predeterminado para los mensajes de nube a dispositivo. | Intervalo de ISO_8601 una too2D (1 minuto como mínimo). Valor predeterminado: 1 hora. |
| maxDeliveryCount          | Número máximo de entregas para las colas de nube a dispositivo por dispositivo. | 1 too100. Valor predeterminado: 10 |
| feedback.ttlAsIso8601     | Retención de mensajes de comentarios del límite de servicio. | Intervalo de ISO_8601 una too2D (1 minuto como mínimo). Valor predeterminado: 1 hora. |
| feedback.maxDeliveryCount |Número máximo de entregas para la cola de comentarios. | 1 too100. Valor predeterminado: 100. |

Para obtener más información acerca de cómo tooset estas opciones de configuración, consulte [centros de IoT crear][lnk-portal].

## <a name="next-steps"></a>Pasos siguientes

Para obtener información sobre SDK de hello puede utilizar mensajes de tooreceive en la nube al dispositivo, consulte [SDK de Azure IoT][lnk-sdks].

tootry espera recibir mensajes en la nube al dispositivo, consulte hello [enviar en la nube al dispositivo] [ lnk-c2d-tutorial] tutorial.

[img-lifecycle]: ./media/iot-hub-devguide-messages-c2d/lifecycle.png

[lnk-portal]: iot-hub-create-through-portal.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-ttl]: #message-expiration-time-to-live
[lnk-c2d-configuration]: #cloud-to-device-configuration-options
[lnk-lifecycle]: #message-lifecycle
[lnk-c2d-tutorial]: iot-hub-csharp-csharp-c2d.md
