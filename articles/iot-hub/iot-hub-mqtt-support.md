---
title: "soporte técnico de Azure IoT Hub MQTT aaaUnderstand | Documentos de Microsoft"
description: "Desarrollador guía: compatibilidad para dispositivos que se conectan tooan centro de IoT dispositivo extremo mediante Hola protocolo MQTT. Incluye información sobre la compatibilidad integrada de MQTT en hello SDK de dispositivos de IoT de Azure."
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
ms.openlocfilehash: e461687963138987acdf1f4e0e34c453744ea191
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="communicate-with-your-iot-hub-using-hello-mqtt-protocol"></a>Comunicarse con el centro de IoT mediante Protocolo de hello MQTT

Centro de IoT permite toocommunicate de dispositivos con extremos de dispositivo de centro de IoT hello mediante hello [MQTT v3.1.1] [ lnk-mqtt-org] protocolo en el puerto 8883 o v3.1.1 MQTT a través del protocolo WebSocket en el puerto 443. Centro de IoT requiere todos los toobe de comunicación de dispositivos segura mediante el uso de TLS/SSL (por lo tanto, centro de IoT no es compatible con conexiones no seguras a través del puerto 1883).

## <a name="connecting-tooiot-hub"></a>Concentrador de conexión tooIoT

Un dispositivo puede usar Centro de IoT de hello MQTT protocolo tooconnect tooan mediante bibliotecas de Hola Hola [SDK de Azure IoT] [ lnk-device-sdks] o directamente con el protocolo MQTT Hola.

## <a name="using-hello-device-sdks"></a>Uso de dispositivo de hello SDK

[SDK de dispositivos] [ lnk-device-sdks] ese protocolo MQTT Hola de soporte técnico están disponibles para Java, Node.js, C, C# y Python. dispositivo de Hello SDK usar Hola estándar centro de IoT conexión cadena tooestablish un centro de IoT tooan de conexión. Protocolo MQTT de toouse hello, parámetro de protocolo de cliente de hello debe establecerse demasiado**MQTT**. De forma predeterminada, el dispositivo de hello SDK, conectar tooan centro de IoT con hello **CleanSession** marca se establece demasiado**0** y usar **QoS 1** de intercambio de mensajes con el centro de IoT Hola.

Cuando un dispositivo está conectado tooan centro de IoT, dispositivo Hola SDK proporcionan métodos que permiten mensajes de Hola dispositivo toosend tooand recibir mensajes de un centro de IoT.

Hello tabla siguiente contiene vínculos toocode ejemplos para cada idioma compatible y especifica Hola parámetro toouse tooestablish un concentrador de conexión tooIoT con hello MQTT protocolo.

| language | Parámetro de protocolo |
| --- | --- |
| [Node.js][lnk-sample-node] |azure-iot-device-mqtt |
| [Java][lnk-sample-java] |IotHubClientProtocol.MQTT |
| [C][lnk-sample-c] |MQTT_Protocol |
| [C#][lnk-sample-csharp] |TransportType.Mqtt |
| [Python][lnk-sample-python] |IoTHubTransportProvider.MQTT |

### <a name="migrating-a-device-app-from-amqp-toomqtt"></a>Migrar una aplicación de dispositivo de AMQP tooMQTT

Si usas hello [dispositivo SDK][lnk-device-sdks], cambiar de usar AMQP tooMQTT requiere cambiar el parámetro de protocolo de hello en la inicialización del cliente hello como se indicó anteriormente.

Al hacerlo, asegúrese de que hello toocheck siguientes elementos:

* AMQP devuelve errores para muchas condiciones, mientras que MQTT finaliza la conexión de Hola. Como resultado, la lógica de control de excepciones puede requerir algunos cambios.
* MQTT no admite hello *rechazar* operaciones cuando se reciben [mensajes en la nube al dispositivo][lnk-messaging]. Si la aplicación de back-end necesita tooreceive una respuesta de aplicación de dispositivo de hello, considere el uso de [dirigir métodos][lnk-methods].

## <a name="using-hello-mqtt-protocol-directly"></a>Directamente con el protocolo de hello MQTT
Si un dispositivo no puede usar el dispositivo de hello SDK, todavía se pueden conectar los puntos de conexión de un dispositivo público toohello mediante el protocolo MQTT hello en el puerto 8883. Hola **conectar** dispositivo Hola de paquetes debe usar Hola siguientes valores:

* Para hello **ClientId** campo, use hello **deviceId**.
* Para hello **nombre de usuario** campo, use `{iothubhostname}/{device_id}/api-version=2016-11-14`, donde {iothubhostname} es Hola CName completa del centro de IoT Hola.

    Por ejemplo, si hello es el nombre de su centro de IoT **contoso.azure devices.net** y si Hola nombre del dispositivo es **MyDevice01**, Hola completa **nombre de usuario** campo debe contener `contoso.azure-devices.net/MyDevice01/api-version=2016-11-14`.
* Para hello **contraseña** campo, use un token de SAS. formato de Hola de hello token SAS es igual Hola como para hello HTTP y protocolos AMQP:<br/>`SharedAccessSignature sig={signature-string}&se={expiry}&sr={URL-encoded-resourceURI}`.

    Para obtener más información acerca de cómo toogenerate tokens SAS, vea la sección de dispositivo de Hola de [tokens de seguridad usando el centro de IoT][lnk-sas-tokens].

    Al realizar pruebas, también puede utilizar hello [explorer dispositivo] [ lnk-device-explorer] tooquickly herramienta generar un token SAS que puede copiar y pegar en su propio código:

  1. Vaya toohello **administración** ficha **dispositivo explorador**.
  2. Haga clic en **Token de SAS** (parte superior derecha).
  3. En **SASTokenForm**, seleccione el dispositivo en hello **DeviceID** de lista desplegable. Establezca el valor para **TTL**.
  4. Haga clic en **generar** toocreate el token.

     token SAS que se genera Hello tiene esta estructura: `HostName={your hub name}.azure-devices.net;DeviceId=javadevice;SharedAccessSignature=SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`.

     Hola parte de este token toouse como hello **contraseña** tooconnect de campo mediante MQTT es: `SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`.

Para MQTT conectar y desconectar paquetes, centro de IoT emite un evento en hello **supervisión de Operations** canal con información adicional que puede ayudar a problemas de conectividad de tootroubleshoot.

### <a name="sending-device-to-cloud-messages"></a>Envío de mensajes de dispositivo a nube

Después de realizar una conexión correcta, un dispositivo puede enviar mensajes tooIoT concentrador mediante `devices/{device_id}/messages/events/` o `devices/{device_id}/messages/events/{property_bag}` como un **el nombre del tema**. Hola `{property_bag}` elemento permite mensajes de Hola dispositivo toosend con propiedades adicionales en un formato con codificación url. Por ejemplo:

```
RFC 2396-encoded(<PropertyName1>)=RFC 2396-encoded(<PropertyValue1>)&RFC 2396-encoded(<PropertyName2>)=RFC 2396-encoded(<PropertyValue2>)…
```

> [!NOTE]
> Esto `{property_bag}` elemento usa Hola misma codificación que para las cadenas de consulta de protocolo de hello HTTP.
>
>

También puede utilizar la aplicación de dispositivo de Hello `devices/{device_id}/messages/events/{property_bag}` como hello **será el nombre del tema** toodefine *mensajes* toobe reenviado como un mensaje de telemetría.

- IoT Hub no admite mensajes QoS 2. Si una aplicación de dispositivo publica un mensaje con **2 QoS**, centro de IoT se cierra la conexión de red de Hola.
- IoT Hub no retiene los mensajes de conservación. Si un dispositivo envía un mensaje con hello **conservar** marca establece too1, centro de IoT agrega hello **x-opt-conservar** toohello mensaje de la propiedad de aplicación. En este caso, en lugar de conservar Hola Retener mensaje, centro de IoT pasa toohello aplicación de back-end.
- IoT Hub solo admite una conexión MQTT activa por dispositivo. Cualquier nueva conexión MQTT en nombre de hello mismo Id. de dispositivo hace centro de IoT conexión existente de toodrop Hola.

Para obtener más información, consulte la [guía del desarrollador de mensajería][lnk-messaging].

### <a name="receiving-cloud-to-device-messages"></a>Recepción de mensajes de nube a dispositivo

mensajes de tooreceive centro de IoT, un dispositivo debe suscribirse con `devices/{device_id}/messages/devicebound/#` como un **tema filtro**. Hola comodín multinivel  **#**  Hola tema filtro se utiliza únicamente tooallow Hola propiedades adicionales del dispositivo tooreceive en el nombre del tema Hola. ¿Centro de IoT no permitir el uso de Hola de hello  **#**  o **?** caracteres comodín para el filtrado de subtemas. Como centro de IoT no es un agente de mensajería de publicación-suscripción de propósito general, solo admite nombres de temas de hello documentado y filtros de tema.

Hello dispositivo no recibirá ningún mensaje del centro de IoT, hasta que se ha suscrito correctamente extremo específico del dispositivo de tooits, representado por hello `devices/{device_id}/messages/devicebound/#` filtro de tema. Una vez establecida la suscripción es correcta, dispositivo Hola comienza a recibir mensajes de solo nube al dispositivo que se han enviado tooit tarde Hola de suscripción de Hola. Si se conecta el dispositivo de hello con **CleanSession** marca se establece demasiado**0**, suscripción Hola se conserva entre sesiones diferentes. Hola en este caso, la próxima vez que se conecta con **CleanSession 0** dispositivo Hola recibe mensajes pendientes que se han enviado tooit mientras estaba desconectado. Si utiliza el dispositivo de hello **CleanSession** marca se establece demasiado**1** sin embargo, no recibe ningún mensaje de centro de IoT hasta que se suscribe el punto de conexión tooits dispositivo.

Centro de IoT entrega mensajes con hello **el nombre del tema** `devices/{device_id}/messages/devicebound/`, o `devices/{device_id}/messages/devicebound/{property_bag}` si no hay ninguna propiedad de mensaje. `{property_bag}` contiene pares clave-valor con codificación URL de propiedades del mensaje. Solo propiedades de la aplicación y las propiedades establecidas por el usuario del sistema (como **messageId** o **correlationId**) se incluyen en la bolsa de propiedades de Hola. Nombres de propiedad del sistema tienen el prefijo de hello  **$** , propiedades de la aplicación usan el nombre original de la propiedad de hello con ningún prefijo.

Cuando una aplicación de dispositivo suscribe tema tooa con **QoS 2**, centro de IoT concede nivel máximo QoS 1 Hola **SUBACK** paquetes. Después de eso, centro de IoT entrega dispositivo toohello de mensajes con QoS 1.

### <a name="retrieving-a-device-twins-properties"></a>Recuperación de propiedades del dispositivo gemelo

En primer lugar, un dispositivo se suscribe demasiado`$iothub/twin/res/#`, las respuestas de la operación de tooreceive Hola. A continuación, envía un mensaje vacío tootopic `$iothub/twin/GET/?$rid={request id}`, con un valor rellenado para **Id. de solicitud**. servicio de hello, a continuación, envía un mensaje de respuesta que contiene los datos de hello dispositivo gemelas en tema `$iothub/twin/res/{status}/?$rid={request id}`, utilizando Hola mismo  **Id. de solicitud** como solicitud de saludo.

El identificador de la solicitud puede ser cualquier valor válido de propiedad de mensaje, según la [guía del desarrollador de mensajería de IoT Hub][lnk-messaging], y el estado se valida como entero.
cuerpo de respuesta de Hello contiene la sección de propiedades de Hola de gemelas de dispositivo de hello:

cuerpo de Hola de entrada del registro de hello identidad había limitado a toohello miembro de "propiedades", por ejemplo:

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

Hola códigos de estado posibles son:

|Estado | Descripción |
| ----- | ----------- |
| 200 | Correcto |
| 429 | Demasiadas solicitudes (limitadas), según el artículo sobre [limitaciones de IoT Hub][lnk-quotas] |
| 5** | Errores del servidor |

Para obtener más información, consulte la [guía para desarrolladores sobre dispositivos gemelos][lnk-devguide-twin].

### <a name="update-device-twins-reported-properties"></a>Actualización de las propiedades notificadas del dispositivo gemelo

Hello secuencia siguiente describe cómo un dispositivo actualiza Hola notificado propiedades en gemelas de dispositivo de hello en el centro de IoT:

1. Un dispositivo en primer lugar debe suscribirse toohello `$iothub/twin/res/#` las respuestas de la operación de tema tooreceive Hola centro de IoT.

1. Un dispositivo envía un mensaje que contiene Hola dispositivo gemelas actualización toohello `$iothub/twin/PATCH/properties/reported/?$rid={request id}` tema. Este mensaje incluye un valor de **identificador de solicitud**.

1. Hola servicio, a continuación, envía un mensaje de respuesta que contiene Hola nuevo valor de ETag de Hola colección de propiedades incluido en el tema `$iothub/twin/res/{status}/?$rid={request id}`. Este mensaje de respuesta utiliza Hola mismo **Id. de solicitud** como solicitud de saludo.

cuerpo del mensaje de solicitud de Hello contiene un documento JSON, que proporciona nuevos valores para propiedades incluidos (no se pueden modificar ninguna otra propiedad o metadatos).
Cada miembro en el documento JSON de hello actualiza o agrega a un miembro correspondiente Hola documento del doble del dispositivo de hello. Un conjunto de miembros demasiado`null`, eliminaciones Hola miembro de Hola que contiene el objeto. Por ejemplo:

        {
            "telemetrySendFrequency": "35m",
            "batteryLevel": 60
        }

Hola códigos de estado posibles son:

|Estado | Descripción |
| ----- | ----------- |
| 200 | Correcto |
| 400 | Solicitud incorrecta. JSON con formato incorrecto |
| 429 | Demasiadas solicitudes (limitadas), según el artículo sobre [limitaciones de IoT Hub][lnk-quotas] |
| 5** | Errores del servidor |

Para obtener más información, consulte la [guía para desarrolladores sobre dispositivos gemelos][lnk-devguide-twin].

### <a name="receiving-desired-properties-update-notifications"></a>Recepción de notificaciones de actualización de las propiedades deseadas

Cuando se conecta un dispositivo, centro de IoT envía tema de las notificaciones toohello `$iothub/twin/PATCH/properties/desired/?$version={new version}`, que incluyen contenido de Hola de actualización de hello realizada Hola solución back-end. Por ejemplo:

        {
            "telemetrySendFrequency": "5m",
            "route": null
        }

Para las actualizaciones de la propiedad, `null` valores decir Hola JSON del objeto miembro que se va a eliminar.


> [!IMPORTANT] 
> IoT Hub genera notificaciones de cambio solo si los dispositivos están conectados. Realizar seguro hello tooimplement [flujo de reconexión de dispositivo] [ lnk-devguide-twin-reconnection] tookeep Hola deseado propiedades sincronizados entre el centro de IoT y aplicación de dispositivo de hello.

Para obtener más información, consulte la [guía para desarrolladores sobre dispositivos gemelos][lnk-devguide-twin].

### <a name="respond-tooa-direct-method"></a>Método directo de responder tooa

En primer lugar, un dispositivo tiene toosubscribe demasiado`$iothub/methods/POST/#`. Centro de IoT envía el tema del método solicitudes toohello `$iothub/methods/POST/{method name}/?$rid={request id}`, con un valor JSON válido o con un cuerpo vacío.

toorespond, dispositivo Hola envía un mensaje con un valor JSON válido o un tema de toohello de cuerpo vacío `$iothub/methods/res/{status}/?$rid={request id}`, donde **Id. de solicitud** tiene toomatch Hola uno en el mensaje de solicitud de Hola y **estado** tiene toobe un entero .

Para obtener más información, consulte la [guía para desarrolladores sobre el método directo][lnk-methods].

### <a name="additional-considerations"></a>Consideraciones adicionales

Como una última consideración, si necesita el comportamiento del protocolo MQTT toocustomize hello en lado de hello en la nube, debe revisar hello [puerta de enlace de IoT de Azure protocolo] [ lnk-azure-protocol-gateway] que le permite toodeploy un alto rendimiento puerta de enlace de protocolo personalizado que se comunica directamente con el centro de IoT. puerta de enlace de protocolo de Hello IoT de Azure permite toocustomize Hola dispositivo protocolo tooaccommodate brownfield MQTT implementaciones u otros protocolos personalizados. Sin embargo, este enfoque requiere que se ejecute y se ponga en funcionamiento una puerta de enlace de protocolo personalizado.

## <a name="next-steps"></a>Pasos siguientes

toolearn más información acerca del protocolo MQTT hello, vea hello [documentación MQTT][lnk-mqtt-docs].

toolearn más información acerca de la planeación de la implementación del centro de IoT, vea:

* [Catálogo de dispositivos de Azure Certified for IoT][lnk-devices]
* [Compatibilidad con protocolos adicionales][lnk-protocols]
* [Comparación con Event Hubs][lnk-compare]
* [Escalado, alta disponibilidad y recuperación ante desastres][lnk-scaling]

toofurther explorar las capacidades de Hola de centro de IoT, vea:

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
