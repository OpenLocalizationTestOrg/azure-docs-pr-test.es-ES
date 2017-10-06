---
title: extremos personalizados de aaaUnderstand centro de IoT de Azure | Documentos de Microsoft
description: "Guía del desarrollador - usar el enrutamiento las reglas de los puntos de conexión de toocustom de tooroute mensajes del dispositivo a la nube."
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
ms.openlocfilehash: daa9cfb35d0853e316bbf469b034d4dadbd4e85d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-message-routes-and-custom-endpoints-for-device-to-cloud-messages"></a>Uso de rutas de mensajes y de puntos de conexión personalizados para mensajes de dispositivo a nube

Centro de IoT permite tooroute [mensajes del dispositivo a la nube] [ lnk-device-to-cloud] tooIoT concentrador de extremos de servicio de acceso en función de propiedades de mensaje. Enrutamiento proporcionan reglas Hola flexibilidad toosend mensajes que necesitan toogo sin Hola necesitan para mensajes de tooprocess de servicios adicionales o toowrite de código adicional. Cada regla de enrutamiento que configure tiene Hola propiedades siguientes:

| Propiedad      | Descripción |
| ------------- | ----------- |
| **Name**      | Hola nombre único que identifica regla Hola. |
| **Origen**    | origen de Hola de los datos de hello secuencia toobe ha actuado en consecuencia. Por ejemplo, telemetría de dispositivo. |
| **Condition** | expresión de consulta de Hello para la regla de enrutamiento de Hola que se ejecuta en los encabezados y el cuerpo del mensaje de bienvenida y usar toodetermine si es una coincidencia para el punto de conexión de Hola. Para obtener más información sobre cómo crear una condición de ruta, consulte hello [referencia: lenguaje de consulta para: los gemelos de dispositivo y los trabajos][lnk-devguide-query-language]. |
| **Extremo**  | nombre de Hola de extremo de Hola donde centro de IoT envía mensajes que coinciden con la condición de Hola. Los extremos deben estar en hello misma región que el centro de IoT hello, en caso contrario, se le puede cobrar para escribe entre regiones. |

Un solo mensaje puede coincidir con la condición de hello en varias reglas de enrutamientos, en el que caso centro de IoT entrega Hola mensaje toohello punto de conexión asociado con cada regla coincidente. Centro de IoT deduplica automáticamente también entrega de mensajes, por lo que si un mensaje coincide con varias reglas que tengan Hola mismo destino, solo se escribe toothat destino una vez.

Un centro de IoT tiene un [punto de conexión integrado][lnk-built-in] predeterminado. Puede crear extremos personalizados tooroute mensajes tooby vincular otros servicios en el centro de toohello de suscripción. IoT Hub admite actualmente Event Hubs, colas de Service Bus y temas de Service Bus como puntos de conexión personalizados.

> [!WARNING]
> Las colas y los temas de Service Bus con **Sesiones** o **Detección de duplicados** habilitadas no son compatibles como puntos de conexión personalizados.

Para más información sobre cómo crear puntos de conexión personalizados en IoT Hub, consulte [Referencia: Puntos de conexión de IoT Hub][lnk-devguide-endpoints].

Para obtener más información sobre la lectura de puntos de conexión personalizados, consulte:

* Leer de [Event Hubs][lnk-getstarted-eh].
* Leer de [colas de Service Bus][lnk-getstarted-queue].
* Leer de [temas de Service Bus][lnk-getstarted-topic].

### <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre los puntos de conexión de IoT Hub, vea [Puntos de conexión de IoT Hub][lnk-devguide-endpoints].

Para obtener más información sobre el lenguaje de consulta de Hola utilizar reglas de enrutamiento de toodefine, consulte [lenguaje de consulta de centro de IoT para: los gemelos de dispositivo, los trabajos y el enrutamiento de mensajes][lnk-devguide-query-language].

Hola [mensajes de dispositivo a la nube del centro de IoT de proceso mediante las rutas de] [ lnk-d2c-tutorial] tutorial muestra cómo las reglas de enrutamiento toouse y extremos personalizados.

[lnk-built-in]: iot-hub-devguide-messages-read-builtin.md
[lnk-device-to-cloud]: iot-hub-devguide-messages-d2c.md
[lnk-devguide-query-language]: iot-hub-devguide-query-language.md
[lnk-devguide-endpoints]: iot-hub-devguide-endpoints.md
[lnk-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md
[lnk-getstarted-eh]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md
[lnk-getstarted-queue]: ../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md
[lnk-getstarted-topic]: ../service-bus-messaging/service-bus-dotnet-how-to-use-topics-subscriptions.md
