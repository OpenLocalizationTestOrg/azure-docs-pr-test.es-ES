---
title: "Información sobre Azure MQTT con IoT Hub | Microsoft Docs"
description: "Guía del desarrollador: compatibilidad con dispositivos que se conectan a un punto de conexión orientado a dispositivos IoT Hub mediante el protocolo MQTT. Incluye información sobre la compatibilidad integrada de MQTT de los SDK de dispositivo IoT de Azure."
services: iot-hub
documentationcenter: .net
author: kdotchkoff
manager: timlt
editor: 
ms.assetid: 1d71c27c-b466-4a40-b95b-d6550cf85144
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/11/2017
ms.author: kdotchko
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: eab70c1aa9c49a137c2ac1012449d57915fb0d27
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="communicate-with-your-iot-hub-using-the-mqtt-protocol"></a>Comunicación con la instancia de IoT Hub mediante el protocolo MQTT

IoT Hub permite a los dispositivos comunicarse con los puntos de conexión de dispositivos de IoT Hub utilizando el protocolo [MQTT v3.1.1][lnk-mqtt-org] en el puerto 8883 o MQTT v3.1.1 sobre el protocolo WebSocket en el puerto 443. IoT Hub requiere que toda la comunicación del dispositivo se proteja mediante TLS/SSL (por lo tanto, IoT Hub no es compatible con conexiones no seguras en el puerto 1883).

## <a name="connecting-to-iot-hub"></a>Conexión al Centro de IoT

Un dispositivo puede conectarse a un centro de IoT mediante el protocolo MQTT, ya sea mediante las bibliotecas de los [SDK de Azure IoT][lnk-device-sdks] o directamente mediante el protocolo MQTT.

## <a name="using-the-device-sdks"></a>Uso de los SDK de dispositivo

Los [SDK de dispositivo][lnk-device-sdks] compatibles con el protocolo MQTT están disponibles para Java, Node.js, C, C# y Python. Los SDK de dispositivo usan la cadena de conexión de IoT Hub estándar para establecer una conexión a un centro de IoT. Para utilizar el protocolo MQTT, el parámetro de protocolo de cliente debe establecerse en **MQTT**. De forma predeterminada, los SDK de dispositivo se conectan a un centro de IoT con la marca **CleanSession** establecida en **0** y usan **QoS 1** para el intercambio de mensajes con el centro de IoT.

Cuando un dispositivo se conecta a un centro de IoT, los SDK de dispositivo proporcionan métodos que permiten al dispositivo enviar y recibir mensajes desde un centro de IoT.

La tabla siguiente contiene vínculos a ejemplos de código para cada idioma admitido y especifica el parámetro que se debe utilizar para establecer una conexión con el Centro de IoT mediante el protocolo MQTT.

| Idioma | Parámetro de protocolo |
| --- | --- |
| [Node.js][lnk-sample-node] |azure-iot-device-mqtt |
| [Java][lnk-sample-java] |IotHubClientProtocol.MQTT |
| [C][lnk-sample-c] |MQTT_Protocol |
| [C#][lnk-sample-csharp] |TransportType.Mqtt |
| [Python][lnk-sample-python] |IoTHubTransportProvider.MQTT |

### <a name="migrating-a-device-app-from-amqp-to-mqtt"></a>Migración de una aplicación de dispositivo de AMQP a MQTT

Si usa los [SDK de dispositivo][lnk-device-sdks], el cambio de AMQP a MQTT requiere modificar el parámetro de protocolo en la inicialización del cliente como se indicó anteriormente.

Al hacerlo, asegúrese de comprobar los elementos siguientes:

* AMQP devuelve errores para muchas condiciones, mientras que MQTT finaliza la conexión. Como resultado, la lógica de control de excepciones puede requerir algunos cambios.
* MQTT no admite las operaciones *rechazar* al recibir [mensajes de la nube al dispositivo][lnk-messaging]. Si su aplicación de back-end tiene que recibir una respuesta de la aplicación del dispositivo, considere los [métodos directos][lnk-methods].

## <a name="using-the-mqtt-protocol-directly"></a>Uso del protocolo MQTT directamente
Si un dispositivo no puede usar los SDK de dispositivo, tendrá la posibilidad de conectarse a los puntos de conexión públicos del dispositivo mediante el protocolo MQTT en el puerto 8883. En el paquete **CONNECT** el dispositivo debe usar los siguientes valores:

* Para el campo **ClientId**, use **deviceId**.
* Para el campo **Nombre de usuario** use `{iothubhostname}/{device_id}/api-version=2016-11-14`, donde {iothubhostname} es el CName completo de IoT Hub.

    Por ejemplo, si el nombre de su centro IoT es **contoso.azure-devices.net** y si el nombre del dispositivo es **MyDevice01**, el campo **Nombre de usuario** completo debe contener `contoso.azure-devices.net/MyDevice01/api-version=2016-11-14`.
* Para el campo **Contraseña** , use un token SAS. El formato del token de SAS es el mismo que para los protocolos HTTP y AMQP:<br/>`SharedAccessSignature sig={signature-string}&se={expiry}&sr={URL-encoded-resourceURI}`.

    Para más información sobre cómo generar tokens de SAS, consulte la sección sobre el [uso de tokens de seguridad de IoT Hub][lnk-sas-tokens].

    Al realizar la prueba, también puede utilizar la herramienta [Explorador de dispositivos][lnk-device-explorer] para generar rápidamente un token SAS que puede copiar y pegar en su propio código:

  1. Vaya a la pestaña **Administración** del **Explorador de dispositivos**.
  2. Haga clic en **Token de SAS** (parte superior derecha).
  3. En **SASTokenForm**, seleccione el dispositivo en el menú desplegable **DeviceID**. Establezca el valor para **TTL**.
  4. Haga clic en **Generar** para crear el token.

     El token de SAS que ha generado tiene esta estructura: `HostName={your hub name}.azure-devices.net;DeviceId=javadevice;SharedAccessSignature=SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`.

     La parte de este token que se debe usar como el campo **Password** para conectarse con MQTT es: `SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`.

Para paquetes de conexión y desconexión de MQTT, IoT Hub emite un evento sobre el canal **Supervisión de operaciones** con información adicional que puede ayudarle a solucionar problemas de conectividad.

### <a name="sending-device-to-cloud-messages"></a>Envío de mensajes de dispositivo a nube

Después de realizar con éxito una conexión, un dispositivo puede enviar mensajes a un centro IoT mediante `devices/{device_id}/messages/events/` o `devices/{device_id}/messages/events/{property_bag}` como un **Nombre del tema**. El elemento `{property_bag}` permite al dispositivo enviar mensajes con propiedades adicionales en un formato con codificación URL. Por ejemplo:

```
RFC 2396-encoded(<PropertyName1>)=RFC 2396-encoded(<PropertyValue1>)&RFC 2396-encoded(<PropertyName2>)=RFC 2396-encoded(<PropertyValue2>)…
```

> [!NOTE]
> Este elemento `{property_bag}` usa la misma codificación que se utiliza para las cadenas de consulta en el protocolo HTTP.
>
>

La aplicación del dispositivo también puede utilizar `devices/{device_id}/messages/events/{property_bag}` como el **nombre del tema Will** para definir los *mensajes Will* que se reenviarán como un mensaje de telemetría.

- IoT Hub no admite mensajes QoS 2. Si una aplicación de dispositivo publica un mensaje con **QoS 2**, el IoT Hub cierra la conexión de red.
- IoT Hub no retiene los mensajes de conservación. Si un dispositivo envía un mensaje con la marca **RETAIN** establecida en 1, el IoT Hub agrega la propiedad de aplicación **x-opt-retain** al mensaje. En este caso, en lugar de retener el mensaje de conservación, IoT Hub lo pasa a la aplicación de back-end.
- IoT Hub solo admite una conexión MQTT activa por dispositivo. Todas las conexiones MQTT nuevas en nombre del mismo identificador de dispositivo provocarán que IoT Hub cierre la existente.

Para obtener más información, consulte la [guía del desarrollador de mensajería][lnk-messaging].

### <a name="receiving-cloud-to-device-messages"></a>Recepción de mensajes de nube a dispositivo

Para recibir mensajes de IoT Hub, un dispositivo debe suscribirse usando `devices/{device_id}/messages/devicebound/#` como un **filtro de tema**. El comodín de varios niveles **#** en el filtro de tema solo se utiliza para permitir que el dispositivo reciba propiedades adicionales en el nombre del tema. ¿IoT Hub no permite el uso de **#** o **?** caracteres comodín para el filtrado de subtemas. Puesto que IoT Hub no es un agente de mensajería de publicación-suscripción de propósito general, solo admite los filtros de tema y los nombres de tema documentados.

El dispositivo no recibe ningún mensaje desde IoT Hub hasta que se suscribe correctamente al punto de conexión específico del dispositivo, representado por el filtro del tema `devices/{device_id}/messages/devicebound/#`. Después de que se establece una suscripción correcta, el dispositivo comienza a recibir solo los mensajes de la nube al dispositivo que se han enviado a él después de la hora de la suscripción. Si el dispositivo se conecta con la marca **CleanSession** establecida en **0**, la suscripción se conserva entre distintas sesiones. En este caso, la próxima vez que se conecta con **CleanSession 0**, el dispositivo recibe mensajes pendientes que se han enviado a él mientras estaba desconectado. Si el dispositivo usa la marca **CleanSession** establecida en **1**, no recibe los mensajes de IoT Hub hasta que se suscribe al punto de conexión del dispositivo.

IoT Hub entrega los mensajes con el **Nombre del tema** `devices/{device_id}/messages/devicebound/`, o `devices/{device_id}/messages/devicebound/{property_bag}` si hay alguna propiedad de mensaje. `{property_bag}` contiene pares clave-valor con codificación URL de propiedades del mensaje. Las propiedades de la aplicación y del sistema configuradas por el usuario (como **messageId** o **correlationId**) son las únicas que se incluyen en el paquete de propiedades. Los nombres de propiedad del sistema tienen el prefijo **$**; las propiedades de aplicaciones utilizan el nombre de propiedad original sin prefijo.

Cuando una aplicación de dispositivo se suscribe a un tema con **QoS 2**, IoT Hub concede el QoS de nivel 1 (el máximo) en el paquete **SUBACK**. Después de eso, IoT Hub envía mensajes al dispositivo con QoS 1.

### <a name="retrieving-a-device-twins-properties"></a>Recuperación de propiedades del dispositivo gemelo

En primer lugar, un dispositivo se suscribe a `$iothub/twin/res/#` para recibir las respuestas de la operación. A continuación, envía un mensaje en blanco al tema `$iothub/twin/GET/?$rid={request id}`, con un valor en **request id**. El servicio envía entonces un mensaje de respuesta que contiene los datos del dispositivo gemelo del tema `$iothub/twin/res/{status}/?$rid={request id}`, usando el mismo **identificador de solicitud** que la solicitud.

El identificador de la solicitud puede ser cualquier valor válido de propiedad de mensaje, según la [guía del desarrollador de mensajería de IoT Hub][lnk-messaging], y el estado se valida como entero.
El cuerpo de la respuesta contiene la sección de propiedades del dispositivo gemelo:

El cuerpo de la entrada del registro de identidad limitado al miembro "properties", p. ej.:

        {
            "properties": {
                "desired": {
                    "telemetrySendFrequency": "5m",
                    "$version": 12
                },
                "reported": {
                    "telemetrySendFrequency": "5m",
                    "batteryLevel": 55,
                    "$version": 123
                }
            }
        }

Los códigos de estado posibles son:

|Estado | Descripción |
| ----- | ----------- |
| 200 | Correcto |
| 429 | Demasiadas solicitudes (limitadas), según el artículo sobre [limitaciones de IoT Hub][lnk-quotas] |
| 5** | Errores del servidor |

Para obtener más información, consulte la [guía para desarrolladores sobre dispositivos gemelos][lnk-devguide-twin].

### <a name="update-device-twins-reported-properties"></a>Actualización de las propiedades notificadas del dispositivo gemelo

La secuencia siguiente describe cómo un dispositivo actualiza las propiedades notificadas en el dispositivo gemelo de IoT Hub:

1. En primer lugar, un dispositivo debe suscribirse al tema `$iothub/twin/res/#` para recibir las respuestas de la operación de IoT Hub.

1. Un dispositivo envía un mensaje que contiene la actualización del dispositivo gemelo al tema `$iothub/twin/PATCH/properties/reported/?$rid={request id}`. Este mensaje incluye un valor de **identificador de solicitud**.

1. Después, el servicio envía un mensaje de respuesta que contiene el nuevo valor de ETag de la colección de propiedades notificadas del tema `$iothub/twin/res/{status}/?$rid={request id}`. Este mensaje de respuesta usa el mismo **identificador de solicitud** que la solicitud.

El cuerpo del mensaje de solicitud contiene un documento JSON que proporciona nuevos valores para propiedades notificadas (no se pueden modificar otras propiedad ni metadatos).
En el documento JSON, cada miembro actualiza o agrega al miembro correspondiente en el documento del dispositivo gemelo. La configuración de un miembro en `null`, elimina el miembro del objeto contenedor. Por ejemplo:

        {
            "telemetrySendFrequency": "35m",
            "batteryLevel": 60
        }

Los códigos de estado posibles son:

|Estado | Descripción |
| ----- | ----------- |
| 200 | Correcto |
| 400 | Solicitud incorrecta. JSON con formato incorrecto |
| 429 | Demasiadas solicitudes (limitadas), según el artículo sobre [limitaciones de IoT Hub][lnk-quotas] |
| 5** | Errores del servidor |

Para obtener más información, consulte la [guía para desarrolladores sobre dispositivos gemelos][lnk-devguide-twin].

### <a name="receiving-desired-properties-update-notifications"></a>Recepción de notificaciones de actualización de las propiedades deseadas

Cuando se conecta un dispositivo, IoT Hub envía notificaciones al tema `$iothub/twin/PATCH/properties/desired/?$version={new version}`, que contiene la actualización realizada por la solución de back-end. Por ejemplo:

        {
            "telemetrySendFrequency": "5m",
            "route": null
        }

Para las actualizaciones de propiedad, los valores `null` significan que se elimina el miembro del objeto JSON.


> [!IMPORTANT] 
> IoT Hub genera notificaciones de cambio solo si los dispositivos están conectados. Asegúrese de implementar el [flujo de reconexión de dispositivos][lnk-devguide-twin-reconnection] para mantener las propiedades que desee sincronizadas entre IoT Hub y la aplicación del dispositivo.

Para obtener más información, consulte la [guía para desarrolladores sobre dispositivos gemelos][lnk-devguide-twin].

### <a name="respond-to-a-direct-method"></a>Respuesta a un método directo

En primer lugar, tiene que suscribirse un dispositivo a `$iothub/methods/POST/#`. IoT Hub envía solicitudes de método al tema `$iothub/methods/POST/{method name}/?$rid={request id}`, con un valor JSON válido o un cuerpo vacío.

Para responder, el dispositivo envía un mensaje con un valor JSON válido o un cuerpo vacío al tema `$iothub/methods/res/{status}/?$rid={request id}`, donde **request id** tiene que coincidir con el mensaje de solicitud y **status** debe ser un entero.

Para obtener más información, consulte la [guía para desarrolladores sobre el método directo][lnk-methods].

### <a name="additional-considerations"></a>Consideraciones adicionales

Como consideración final, si necesita personalizar el comportamiento del protocolo MQTT en el lado de la nube, debe revisar la [puerta de enlace de protocolos de IoT de Azure][lnk-azure-protocol-gateway] que le permite implementar una puerta de enlace de protocolo personalizado de alto rendimiento que interactúa directamente con IoT Hub. La puerta de enlace de protocolos de IoT de Azure le permite personalizar el protocolo del dispositivo para dar cabida a las implementaciones de MQTT de Brownfield u otros protocolos personalizados. Sin embargo, este enfoque requiere que se ejecute y se ponga en funcionamiento una puerta de enlace de protocolo personalizado.

## <a name="next-steps"></a>Pasos siguientes

Para más información sobre el protocolo MQTT, consulte la [documentación de MQTT][lnk-mqtt-docs].

Para más información acerca de planificación de la implementación del Centro de IoT, consulte:

* [Catálogo de dispositivos de Azure Certified for IoT][lnk-devices]
* [Compatibilidad con protocolos adicionales][lnk-protocols]
* [Comparación con Event Hubs][lnk-compare]
* [Escalado, alta disponibilidad y recuperación ante desastres][lnk-scaling]

Para explorar aún más las funcionalidades de Centro de IoT, consulte:

* [Guía para desarrolladores de IoT Hub][lnk-devguide]
* [Simular un dispositivo con Azure IoT Edge][lnk-iotedge]

[lnk-device-sdks]: https://github.com/Azure/azure-iot-sdks
[lnk-mqtt-org]: http://mqtt.org/
[lnk-mqtt-docs]: http://mqtt.org/documentation
[lnk-sample-node]: https://github.com/Azure/azure-iot-sdk-node/blob/master/device/samples/simple_sample_device.js
[lnk-sample-java]: https://github.com/Azure/azure-iot-sdk-java/tree/master/device/samples/send-receive-sample/src/main/java/samples/com/microsoft/azure/iothub/SendReceive.java
[lnk-sample-c]: https://github.com/Azure/azure-iot-sdk-c/tree/master/iothub_client/samples/iothub_client_sample_mqtt
[lnk-sample-csharp]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/device/samples
[lnk-sample-python]: https://github.com/Azure/azure-iot-sdk-python/tree/master/device/samples
[lnk-device-explorer]: https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer
[lnk-sas-tokens]: iot-hub-devguide-security.md#use-sas-tokens-in-a-device-app
[lnk-azure-protocol-gateway]: iot-hub-protocol-gateway.md

[lnk-devices]: https://catalog.azureiotsuite.com/
[lnk-protocols]: iot-hub-protocol-gateway.md
[lnk-compare]: iot-hub-compare-event-hubs.md
[lnk-scaling]: iot-hub-scaling.md
[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md

[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-messaging]: iot-hub-devguide-messaging.md

[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-devguide-twin-reconnection]: iot-hub-devguide-device-twins.md#device-reconnection-flow
[lnk-devguide-twin]: iot-hub-devguide-device-twins.md
