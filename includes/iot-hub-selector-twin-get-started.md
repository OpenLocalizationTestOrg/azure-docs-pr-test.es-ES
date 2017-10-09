> [!div class="op_single_selector"]
> * [Node.js](../articles/iot-hub/iot-hub-node-node-twin-getstarted.md)
> * [C#/Node.js](../articles/iot-hub/iot-hub-csharp-node-twin-getstarted.md)
> * [C#](../articles/iot-hub/iot-hub-csharp-csharp-twin-getstarted.md)
> * [Java](../articles/iot-hub/iot-hub-java-java-twin-getstarted.md)

Los dispositivos gemelos son documentos JSON que almacenan información sobre el estado de los dispositivos (metadatos, configuraciones y condiciones). Centro de IoT conserva a un gemelas de dispositivo para cada dispositivo que se conecta tooit.

Use los dispositivos gemelos para:

* Almacenar metadatos del dispositivo desde el back-end de la solución.
* Notificar la información de estado actual, como capacidades disponibles y las condiciones (por ejemplo, hello conectividad método usado) desde la aplicación de dispositivo.
* Sincronizar el estado de Hola de flujos de trabajo de larga duración (por ejemplo, las actualizaciones de firmware y configuración) entre una aplicación de dispositivo y una aplicación de back-end.
* Consultar los metadatos, la configuración o el estado del dispositivo.

> [!NOTE]
> Los dispositivos gemelos están diseñados para la sincronización y para consultar las condiciones y configuraciones del dispositivo. Obtener más información acerca de cuándo: los gemelos de toouse dispositivo se encuentra en [comprender: los gemelos de dispositivo][lnk-twins].

Los dispositivos gemelos se almacenan en un IoT Hub y contienen:

* *etiquetas*, metadatos del dispositivo solo puedan acceder aquellos Hola solución back-end;
* *las propiedades adecuadas*, objetos JSON modificables por solución Hola realizar copia de final y observable Hola del dispositivo; y
* *notifica las propiedades*, los objetos JSON modificables por aplicación de dispositivo de hello y legibles por hello solución back-end. Las etiquetas y propiedades no pueden contener matrices, pero se pueden anidar objetos.

![][img-twin]

Además, Hola solución back-end puede consultar en función de todos los Hola por encima de los datos: los gemelos de dispositivo.
Consulte demasiado[comprender: los gemelos de dispositivo] [ lnk-twins] para obtener más información acerca de: los gemelos de dispositivo y toohello [lenguaje de consultas del centro de IoT] [ lnk-query] referencia Para consultar.

> [!NOTE]
> En este momento, son accesibles únicamente desde dispositivos que se conectan tooIoT concentrador: los gemelos de dispositivo mediante el protocolo MQTT Hola. Consulte toohello [compatibilidad MQTT] [ lnk-devguide-mqtt] artículo para obtener instrucciones sobre cómo toouse de aplicación de dispositivo existente de tooconvert MQTT.

En este tutorial se muestra cómo realizar las siguientes acciones:

* Crear una aplicación de back-end que agrega *etiquetas* tooa gemelas de dispositivo y una aplicación de dispositivo simulado que informa de su conectividad de canal como un *notificado propiedad* en gemelas de dispositivo de Hola.
* Consultar dispositivos desde la aplicación de back-end se utilizan filtros en etiquetas de Hola y propiedades que creó anteriormente.

<!-- images -->
[img-twin]: media/iot-hub-selector-twin-get-started/twin.png

<!-- links -->
[lnk-query]: ../articles/iot-hub/iot-hub-devguide-query-language.md
[lnk-twins]: ../articles/iot-hub/iot-hub-devguide-device-twins.md
[lnk-d2c]: ../articles/iot-hub/iot-hub-devguide-messaging.md#device-to-cloud-messages
[lnk-methods]: ../articles/iot-hub/iot-hub-devguide-direct-methods.md
[lnk-devguide-mqtt]: ../articles/iot-hub/iot-hub-mqtt-support.md