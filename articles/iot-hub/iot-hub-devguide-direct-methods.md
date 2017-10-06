---
title: "aaaUnderstand centro de IoT de Azure dirigir métodos | Documentos de Microsoft"
description: "Guía del desarrollador - usar métodos directos tooinvoke código en los dispositivos desde una aplicación de servicio."
services: iot-hub
documentationcenter: .net
author: nberdy
manager: timlt
editor: 
ms.assetid: 9f0535f1-02e6-467a-9fc4-c0950702102d
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: nberdy
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0d15d44a0c3e1d1cda1669c1ed011c2f932e3d92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="understand-and-invoke-direct-methods-from-iot-hub"></a>Conocimiento e invocación de los métodos directos de IoT Hub
## <a name="overview"></a>Información general
Centro de IoT ofrece métodos directos tooinvoke de capacidad en los dispositivos de la nube de Hola. Métodos directos representan una interacción de solicitud y respuesta con un tooan similar de dispositivo HTTP llamar en que se realizan correctamente o se producirá un error inmediatamente (después de un tiempo de espera especificado por el usuario). Esto es útil para escenarios donde el curso de Hola de una acción inmediata es diferente en función de si el dispositivo de hello era capaz de toorespond, como el envío de un dispositivo de reactivación tooa SMS si un dispositivo está sin conexión (que se va a más cara que una llamada al método SMS).

Cada método de dispositivo se dirige a un único dispositivo. [Trabajos] [ lnk-devguide-jobs] proporcionan un tooinvoke de forma directa en varios dispositivos y programar la invocación del método de dispositivos desconectados.

Cualquier persona con permisos de **conexión de servicio** en IoT Hub pueden invocar un método en un dispositivo.

### <a name="when-toouse"></a>Cuando toouse
Métodos directos siguen un patrón de solicitud-respuesta y están diseñados para las comunicaciones que necesitan confirmación inmediata de su control normalmente interactivo de dispositivo de hello, por ejemplo tooturn en un ventilador de resultados.

Consulte demasiado[orientación para la comunicación en la nube para dispositivos] [ lnk-c2d-guidance] en caso de duda entre el uso de propiedades que desee, dirigir métodos o mensajes de la nube al dispositivo.

## <a name="method-lifecycle"></a>Ciclo de vida de los métodos
Métodos directos se implementan en dispositivos de Hola y pueden requerir cero o más entradas en hello método carga toocorrectly crear instancias. Se invoca un método directo mediante un URI orientado al servicio (`{iot hub}/twins/{device id}/methods/`). Un dispositivo recibe métodos directos a través de un tema MQTT específico del dispositivo (`$iothub/methods/POST/{method name}/`). Podemos admitimos métodos directos en protocolos de red del dispositivo adicionales en hello futuras.

> [!NOTE]
> Cuando se invoca un método directo en un dispositivo, valores y nombres de propiedad solo pueden contener US-ASCII imprimible alfanumérico, excepto los Hola siguiendo conjunto: ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``.
> 
> 

Dirigir métodos son sincrónicos y ya sea correctamente o producirá un error tras el período de tiempo de espera de hello (predeterminado: 30 segundos, puede establecer seguridad too3600 segundos). Métodos directos son útiles en escenarios interactivos donde desea un tooact de dispositivo si y solo si el dispositivo de hello es comandos en línea y la recepción, como activar una luz desde un teléfono. En estos casos, desea toosee un error o éxito inmediata para que servicio de nube de hello puede actuar en el resultado de hello tan pronto como sea posible. dispositivo de Hello puede devolver algunas cuerpo del mensaje como resultado del método hello, pero no es necesario para hello método toodo para. No hay ninguna garantía respecto al orden o la semántica de simultaneidad en las llamadas de método.

Método directo son solo HTTP del lado de la nube de Hola y MQTT solo desde el lado del dispositivo de Hola.

carga de Hello para el método solicitudes y respuestas es un documento JSON hacia arriba too8KB.

## <a name="reference-topics"></a>Temas de referencia:
Hello temas de referencia siguientes proporcionan más información sobre el uso de métodos directos.

## <a name="invoke-a-direct-method-from-a-back-end-app"></a>Invocación de un método directo desde una aplicación de back-end
### <a name="method-invocation"></a>Invocación de método
Las invocaciones de método directo en un dispositivo son llamadas HTTP compuestas por:

* Hola *URI* dispositivo toohello específico (`{iot hub}/twins/{device id}/methods/`)
* Hola POST *(método)*
* *Encabezados de* que contienen Hola authorization, Id., el tipo de contenido y la codificación de contenido de solicitud
* JSON transparente *cuerpo* Hola siguiendo el formato:

```
{
    "methodName": "reboot",
    "responseTimeoutInSeconds": 200,
    "payload": {
        "input1": "someInput",
        "input2": "anotherInput"
    }
}
```

El tiempo de espera se expresa en segundos. Si no se establece el tiempo de espera, el valor predeterminado es too30 segundos.

### <a name="response"></a>Response
aplicaciones de back-end de Hello recibe una respuesta que consta de:

* *Código de estado HTTP*, que se utiliza para errores procedentes de hello centro de IoT, incluido un error 404 para dispositivos no está conectado
* *Encabezados de* que contienen Hola ETag, Id., el tipo de contenido y la codificación de contenido de solicitud
* JSON *cuerpo* Hola siguiendo el formato:

```
{
    "status" : 201,
    "payload" : {...}
}
```

   Ambos `status` y `body` se proporcionan por dispositivo de Hola y usar toorespond con código de estado del dispositivo de Hola o descripción.

## <a name="handle-a-direct-method-on-a-device"></a>Control de un método directo en un dispositivo
### <a name="method-invocation"></a>Invocación de método
Dispositivos reciben las solicitudes de método directo en el tema de Hola MQTT:`$iothub/methods/POST/{method name}/?$rid={request id}`

cuerpo de Hello qué dispositivo Hola recibe es Hola siguiendo el formato:

```
{
    "input1": "someInput",
    "input2": "anotherInput"
}
```

Las solicitudes de método son QoS 0.

### <a name="response"></a>Response
dispositivo de Hello envía las respuestas demasiado`$iothub/methods/res/{status}/?$rid={request id}`, donde:

* Hola `status` propiedad es el estado proporcionado por el dispositivo de Hola de ejecución del método.
* Hola `$rid` propiedad es Id. de solicitud de saludo de la invocación del método hello recibida desde el centro de IoT.

cuerpo de Hola se establece por dispositivo de Hola y puede ser cualquier tipo de estado.

## <a name="additional-reference-material"></a>Material de referencia adicional
Otros temas de referencia en la Guía del desarrollador de centro de IoT Hola incluyen:

* [Los extremos del centro de IoT] [ lnk-endpoints] describe Hola varios extremos que cada centro de IoT expone las operaciones de tiempo de ejecución y administración.
* [Limitación y las cuotas] [ lnk-quotas] describe las cuotas de Hola que se aplican toohello servicio del centro de IoT y Hola limitación tooexpect de comportamiento cuando se usa el servicio de Hola.
* [SDK de dispositivos y servicios de Azure IoT] [ lnk-sdks] listas Hola lenguaje varios SDK que se puede usar cuando se desarrollan aplicaciones de dispositivos y servicios que interactúan con el centro de IoT.
* [Lenguaje de consulta de centro de IoT para: los gemelos de dispositivo, los trabajos y el enrutamiento de mensajes] [ lnk-query] describe Hola lenguaje de consultas del centro de IoT puede usar información de tooretrieve centro de IoT de: los gemelos de dispositivo y trabajos.
* [Compatibilidad de IoT Hub MQTT] [ lnk-devguide-mqtt] proporciona más información acerca del soporte técnico de centro de IoT para el protocolo MQTT Hola.

## <a name="next-steps"></a>Pasos siguientes
Ahora que ha aprendido cómo toouse métodos directos, puede que esté interesado en hello siguiente tema de la Guía de centro de IoT para desarrolladores:

* [Programación de trabajos en varios dispositivos][lnk-devguide-jobs]

Si desea que tootry algunos de los conceptos de hello descritos en este artículo, es posible que interesa Hola sigue tutorial del centro de IoT:

* [Use direct methods][lnk-methods-tutorial] (Uso de métodos directos)

<!-- links and images -->

[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md
[lnk-devguide-messages]: iot-hub-devguide-messaging.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
