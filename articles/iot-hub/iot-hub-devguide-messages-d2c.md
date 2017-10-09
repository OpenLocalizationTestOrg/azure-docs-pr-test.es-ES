---
title: "mensajería de dispositivo para la nube de Azure IoT Hub aaaUnderstand | Documentos de Microsoft"
description: "Guía del desarrollador - cómo toouse dispositivo a la nube con el centro de IoT de mensajería. Incluye información sobre enviar datos de telemetría y no telemtry y el uso de enrutar los mensajes toodeliver."
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
ms.openlocfilehash: 07dc8a6be747365c7efbc528ab2762b0d9790758
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="send-device-to-cloud-messages-tooiot-hub"></a>Enviar mensajes del dispositivo a la nube tooIoT concentrador

toosend telemetría de series temporales y las alertas de los dispositivos tooyour solución back-end, enviar mensajes de dispositivo a la nube desde el centro de IoT tooyour de dispositivo. Para obtener una explicación de otras opciones de dispositivo a nube compatibles con IoT Hub, consulte [Guía de comunicación de dispositivo a nube][lnk-d2c-guidance].

Los mensajes del dispositivo a la nube se envían a través de un punto de conexión orientado al dispositivo (**/devices/{IdDeDispositivo}/messages/events**). Reglas de enrutamiento, a continuación, enrutar el tooone de mensajes de extremos de acceso de servicio de hello en el centro de IoT. Las reglas de enrutamiento utilizan encabezados de Hola y el cuerpo de mensajes del dispositivo a la nube de Hola que fluyen a través de su toodetermine de base de datos central donde tooroute ellos. De forma predeterminada, los mensajes son el punto de conexión de toohello enrutado integrados a nivel de servicio (**mensajes de eventos**), que es compatible con [centros de eventos][lnk-event-hubs]. Por lo tanto, puede usar el estándar de [integración de los centros de eventos y los SDK] [ lnk-compatible-endpoint] tooreceive mensajes de dispositivo para la nube en la solución de back-end.

IoT Hub implementa mensajería de dispositivo a nube mediante un patrón de mensajería de streaming. Mensajes de dispositivo para la nube del centro de IoT son más parecidos a [centros de eventos] [ lnk-event-hubs] *eventos* de [Service Bus] [ lnk-servicebus] *mensajes* en que hay un gran volumen de eventos que se pasan a través del servicio Hola que puede leerse mediante varios lectores.

Dispositivo a la nube con el centro de IoT de mensajería tiene Hola siguientes características:

* Mensajes del dispositivo a la nube son durables y retenido en valor predeterminado de un centro de IoT **mensajes de eventos** punto de conexión para los días de tooseven.
* Mensajes del dispositivo a la nube pueden ser como máximo de 256 KB y se pueden agrupar en lotes toooptimize envía. Los lotes pueden tener un tamaño máximo de 256 KB.
* Como se explica en hello [tooIoT de acceso de Control concentrador] [ lnk-devguide-security] sección, centro de IoT habilita por dispositivo autenticación y control de acceso.
* Centro de IoT permite toocreate too10 personalizado extremos. Los mensajes se entregan los puntos de conexión de toohello basados en rutas configuradas en el centro de IoT. Para obtener más información, consulte [Reglas de enrutamiento](#routing-rules).
* IoT Hub habilita millones de dispositivos conectados al mismo tiempo (consulte [Cuotas y limitación][lnk-quotas]).
* IoT Hub no permite el particionamiento arbitrario. Los mensajes de dispositivo a nube se dividen en particiones en función de su valor de **deviceId**de origen.

Para obtener más información acerca de las diferencias de hello entre Hola centro de IoT y los servicios de los centros de eventos, vea [comparación al centro de IoT de Azure y concentradores de eventos de Azure][lnk-comparison].

## <a name="send-non-telemetry-traffic"></a>Envío de tráfico sin telemetría

A menudo, además los puntos de datos de tootelemetry, dispositivos la envían mensajes y las solicitudes que requieran la ejecución independiente y el control en hello solución back-end. Por ejemplo, las alertas críticas que deben desencadenar una acción específica en hello back-end. Puede escribir fácilmente un [regla de enrutamiento] [ lnk-devguide-custom] toosend estos tipos de punto de conexión de mensajes tooan dedicado procesamiento tootheir basado en cualquier un encabezado de mensaje de bienvenida o un valor en el cuerpo del mensaje de Hola.

Para obtener más información acerca de tooprocess de manera mejor de hello este tipo de mensaje, vea hello [Tutorial: cómo tooprocess mensajes del dispositivo a la nube de centro de IoT] [ lnk-d2c-tutorial] tutorial.

## <a name="route-device-to-cloud-messages"></a>Enrutamiento de mensajes de dispositivo a nube

Tiene dos opciones para las aplicaciones de back-end de tooyour de enrutamiento mensajes del dispositivo a la nube:

* Usar Hola integrada [punto de conexión de concentrador de eventos-compatible con] [ lnk-compatible-endpoint] tooenable aplicaciones back-end tooread Hola dispositivo a la nube mensajes que recibe el concentrador de Hola. toolearn sobre Hola integrados concentrador de eventos-compatible con punto de conexión, consulte [leer los mensajes de dispositivo para la nube de punto de conexión integrados de hello][lnk-devguide-builtin].
* Usar enrutamiento de los extremos de toocustom reglas toosend mensajes en el centro de IoT. Extremos personalizados permiten que los mensajes de dispositivo para la nube de tooread de aplicaciones back-end con los concentradores de eventos, colas de Service Bus o temas de Bus de servicio. toolearn acerca de los puntos de conexión de enrutamientos y personalizados, vea [usar extremos personalizados y las reglas de enrutamiento para mensajes del dispositivo a la nube][lnk-devguide-custom].

## <a name="anti-spoofing-properties"></a>Propiedades contra la suplantación

tooavoid dispositivo de suplantación de identidad en mensajes de dispositivo a la nube, centro de IoT marcas de todos los mensajes con hello propiedades siguientes:

* **ConnectionDeviceId**
* **ConnectionDeviceGenerationId**
* **ConnectionAuthMethod**

Hello primero dos contienen hello **deviceId** y **generationId** de hello procedentes de dispositivos, como por [propiedades de identidad de dispositivo][lnk-device-properties].

Hola **ConnectionAuthMethod** propiedad contiene un objeto JSON serializado, con hello propiedades siguientes:

```json
{
  "scope": "{ hub | device}",
  "type": "{ symkey | sas}",
  "issuer": "iothub"
}
```

## <a name="next-steps"></a>Pasos siguientes

Para obtener información sobre SDK de hello puede utilizar mensajes de dispositivo a la nube de toosend, consulte [SDK de Azure IoT][lnk-sdks].

Hola [Introducción] [ lnk-get-started] los tutoriales muestra cómo toosend dispositivo a la nube mensajes desde los dispositivos físicos y simulados. Para obtener información más detallada, vea hello [mensajes de dispositivo a la nube del centro de IoT de proceso mediante las rutas de] [ lnk-d2c-tutorial] tutorial.

[lnk-devguide-builtin]: iot-hub-devguide-messages-read-builtin.md
[lnk-devguide-custom]: iot-hub-devguide-messages-read-custom.md
[lnk-comparison]: iot-hub-compare-event-hubs.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md
[lnk-get-started]: iot-hub-get-started.md

[lnk-event-hubs]: http://azure.microsoft.com/documentation/services/event-hubs/
[lnk-servicebus]: http://azure.microsoft.com/documentation/services/service-bus/
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-compatible-endpoint]: iot-hub-devguide-messages-read-builtin.md
[lnk-device-properties]: iot-hub-devguide-identity-registry.md#device-identity-properties
[lnk-devguide-security]: iot-hub-devguide-security.md
[lnk-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md
