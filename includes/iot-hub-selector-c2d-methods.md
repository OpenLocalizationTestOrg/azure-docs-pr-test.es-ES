> [!div class="op_single_selector"]
> * [Node.js](../articles/iot-hub/iot-hub-node-node-direct-methods.md)
> * [C#/Node.js](../articles/iot-hub/iot-hub-csharp-node-direct-methods.md)
> * [C#](../articles/iot-hub/iot-hub-csharp-csharp-direct-methods.md)
> * [Java](../articles/iot-hub/iot-hub-java-java-direct-methods.md)

Azure IoT Hub es un servicio totalmente administrado que permite la comunicación bidireccional confiable y segura entre millones de dispositivos y un back-end de la solución. Tutoriales anteriores ([empezar a trabajar con el centro de IoT] y [enviar mensajes en la nube al dispositivo con el centro de IoT]) ilustran Hola dispositivo a la nube y en la nube al dispositivo funcionalidad de mensajería básica de centro de IoT. Centro de IoT, también podrá Hola métodos de no perdurables tooinvoke de capacidad en los dispositivos de la nube de Hola. Dirigir métodos representan una interacción de solicitud y respuesta con un tooan similar de dispositivo HTTP llamar en que se realizan correctamente o se producirá un error inmediatamente (después de un tiempo de espera especificado por el usuario) usuario de hello toolet saber estado Hola de llamada de Hola. [Invocar un método directo en un dispositivo] [ lnk-devguide-methods] describe métodos directos con más detalle y se ofrecen consejos sobre cuándo toouse dirigir métodos en lugar de mensajes en la nube al dispositivo o propiedades que desee.

En este tutorial se muestra cómo realizar las siguientes acciones:

* Usar hello toocreate portal Azure un centro de IoT y cree una identidad de dispositivo en el centro de IoT.
* Crear una aplicación de dispositivo simulado que tiene un método directo que se puede llamar en nube Hola.
* Crear una aplicación de consola que llama a un método directo en la aplicación de dispositivo simulado de hello a través de su centro de IoT.

> [!NOTE]
> En este momento, métodos directos son solo admiten los dispositivos que se conectan tooIoT concentrador mediante Hola protocolo MQTT. Consulte toohello [compatibilidad MQTT] [ lnk-devguide-mqtt] artículo para obtener instrucciones sobre cómo toouse de aplicación de dispositivo existente de tooconvert MQTT.


[lnk-devguide-methods]: ../articles/iot-hub/iot-hub-devguide-direct-methods.md
[lnk-devguide-mqtt]: ../articles/iot-hub/iot-hub-mqtt-support.md

[enviar mensajes en la nube al dispositivo con el centro de IoT]: ../articles/iot-hub/iot-hub-csharp-csharp-c2d.md
[empezar a trabajar con el centro de IoT]: ../articles/iot-hub/iot-hub-node-node-getstarted.md