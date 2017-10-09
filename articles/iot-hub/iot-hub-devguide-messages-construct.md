---
title: formato de mensaje de aaaUnderstand centro de IoT de Azure | Documentos de Microsoft
description: "Guía del desarrollador - formato de hello describe y el contenido esperado de mensajes del centro de IoT."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 3fc5f1a3-3711-4611-9897-d4db079b4250
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: dobett
ms.openlocfilehash: 3b1567e47bc32f70c0c252996648c4035ae81243
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-read-iot-hub-messages"></a>Creación y lectura de mensajes de IoT Hub

toosupport interoperabilidad sin problemas a través de protocolos, centro de IoT define un formato de mensaje común para todos los protocolos de dispositivo. Este formato de mensaje se usa tanto para mensajes [dispositivo a nube][lnk-d2c] como para [nube a dispositivo][lnk-c2d]. Un [mensaje IoT Hub][lnk-messaging] consta de:

* Un conjunto de *propiedades del sistema*. Propiedades que IoT Hub interpreta o establece. Este conjunto es el predeterminado.
* Un conjunto de *propiedades de la aplicación*. Un diccionario de propiedades de la cadena que se puede definir la aplicación hello y acceso, sin necesidad de cuerpo del mensaje de Hola toodeserialize. Centro de IoT nunca modifica estas propiedades.
* Un cuerpo binario opaco.

Los nombres de propiedad solo pueden contener caracteres alfanuméricos ASCII y ``{'!', '#', '$', '%, '&', "'", '*', '*', '+', '-', '.', '^', '_', '`', '|', '~'}`` cuando realiza las siguientes acciones:

* Enviar mensajes de dispositivo a la nube mediante el protocolo HTTP Hola.
* Envío de mensajes de nube a dispositivo.

Para obtener más información acerca de cómo tooencode y descodificar los mensajes enviados mediante diferentes protocolos, vea [SDK de Azure IoT][lnk-sdks].

Hello en la tabla siguiente enumera conjunto Hola de propiedades del sistema en los mensajes de centro de IoT.

| Propiedad | Description |
| --- | --- |
| MessageId |Un identificador configurable por el usuario para mensaje de saludo utilizado para patrones de solicitud y respuesta. Formato: Una cadena entre mayúsculas y minúsculas (arriba too128 caracteres) de caracteres alfanuméricos ASCII 7 bits + `{'-', ':',’.', '+', '%', '_', '#', '*', '?', '!', '(', ')', ',', '=', '@', ';', '$', '''}`. |
| Número de secuencia |Un número (único para cada dispositivo a la cola) asignado por mensaje de centro de IoT tooeach en la nube al dispositivo. |
| demasiado|Un destino especificado en los mensajes [de la nube al dispositivo][lnk-c2d]. |
| ExpiryTimeUtc |Fecha y hora de la expiración del mensaje. |
| EnqueuedTime |Fecha y hora hello [en la nube al dispositivo] [ lnk-c2d] centro de IoT recibió el mensaje. |
| CorrelationId |Una propiedad de cadena en un mensaje de respuesta que contiene normalmente Hola MessageId de solicitud de hello, en los patrones de solicitud y respuesta. |
| UserId |Un identificador usado origen de hello toospecify de mensajes. Cuando se generan mensajes por centro de IoT, se establece demasiado`{iot hub name}`. |
| Ack |Un generador de mensajes de comentarios. Esta propiedad se utiliza en los mensajes de comentarios de los mensajes en la nube al dispositivo toorequest centro de IoT toogenerate como resultado de consumo de Hola de los mensajes de bienvenida del dispositivo Hola. Los valores posibles: **ninguno** (valor predeterminado): se genera ningún mensaje de comentarios, **positivo**: recibir un mensaje de respuesta si se ha completado el mensaje de bienvenida, **negativo**: recibir un mensaje de comentarios si mensaje Hola expirado (o se ha alcanzado el número máximo de entregas) sin que se va a completar por dispositivo de hello, o **completa**: positivos y negativos. Para más información, consulte [Comentarios de mensajes][lnk-feedback]. |
| ConnectionDeviceId |Un identificador establecido por Centro de IoT en los mensajes de dispositivo a nube. Contiene hello **deviceId** del dispositivo de Hola que envía el mensaje de bienvenida. |
| ConnectionDeviceGenerationId |Un identificador establecido por Centro de IoT en los mensajes de dispositivo a nube. Contiene hello **generationId** (como por [propiedades de identidad de dispositivo][lnk-device-properties]) del dispositivo de Hola que envía el mensaje de bienvenida. |
| ConnectionAuthMethod |Un método de autenticación establecido por Centro de IoT en los mensajes de dispositivo a nube. Esta propiedad contiene información sobre Hola autenticación método utilizado tooauthenticate Hola dispositivo que envía mensajes de bienvenida. Para obtener más información, consulte [dispositivo toocloud contra la suplantación de identidad][lnk-antispoofing]. |

## <a name="message-size"></a>Tamaño del mensaje

Centro de IoT mide el tamaño de los mensajes de una manera independiente del protocolo, teniendo en cuenta solo carga real de Hola. tamaño de Hello en bytes se calcula sumando Hola de siguientes hello:

* tamaño del texto Hello en bytes.
* tamaño de Hello en bytes de todos los valores de Hola Hola sistema de propiedades de mensaje.
* tamaño de Hello en bytes de todos los valores y nombres de propiedad de usuario.

Valores y nombres de propiedad son caracteres de tooASCII limitado, por lo que la longitud de Hola de las cadenas de hello es igual a tamaño de hello en bytes.

## <a name="next-steps"></a>Pasos siguientes

Para obtener información acerca de los límites de tamaño de mensaje IoT Hub, consulte [Cuotas y limitación de IoT Hub][lnk-quotas].

toolearn toocreate y leer mensajes de centro de IoT en varios lenguajes de programación, vea hello [Introducción] [ lnk-get-started] tutoriales.

[lnk-messaging]: iot-hub-devguide-messaging.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-get-started]: iot-hub-get-started.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-c2d]: iot-hub-devguide-messages-c2d.md
[lnk-d2c]: iot-hub-devguide-messages-d2c.md
[lnk-feedback]: iot-hub-devguide-messages-c2d.md#message-feedback
[lnk-device-properties]: iot-hub-devguide-identity-registry.md#device-identity-properties
[lnk-antispoofing]: iot-hub-devguide-messages-d2c.md#anti-spoofing-properties
