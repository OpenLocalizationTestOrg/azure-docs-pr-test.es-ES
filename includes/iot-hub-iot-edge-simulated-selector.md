> [!div class="op_single_selector"]
> * [Linux](../articles/iot-hub/iot-hub-linux-iot-edge-simulated-device.md)
> * [Windows](../articles/iot-hub/iot-hub-windows-iot-edge-simulated-device.md)

En este tutorial de hello [ejemplo en la nube de dispositivo simulado cargar] muestra cómo toouse [Azure IoT borde] [ lnk-sdk] toosend tooIoT de telemetría de dispositivo para la nube concentrador de simulada dispositivos.

En este tutorial, se describen los siguientes procedimientos:

* **Arquitectura**: obtener información arquitectónica sobre hello [ejemplo en la nube de dispositivo simulado cargar].
* **Compile y ejecute**: Hola pasos necesarios toobuild y ejemplo de Hola de ejecución.

## <a name="architecture"></a>Arquitectura

Hola [ejemplo en la nube de dispositivo simulado cargar] muestra cómo toocreate una puerta de enlace que envía la telemetría de simula centro de IoT tooan de dispositivos. Un dispositivo no sea capaz de tooconnect directamente tooIoT concentrador porque el dispositivo de hello:

* No usa un protocolo de comunicaciones que entienda IoT Hub.
* No es lo suficientemente inteligente como tooremember Hola identidad asignan tooit IoT hub.

Una puerta de enlace de IoT borde puede resolver estos problemas en hello siguientes maneras:

* puerta de enlace de Hello entiende protocolo Hola Hola dispositivo usado, recibe la telemetría de dispositivo para la nube de dispositivo de Hola y reenvía esos tooIoT mensajes concentrador mediante un protocolo entendido por centro de IoT Hola.

* puerta de enlace de Hello asigna toodevices de identidades de centro de IoT y actúa como un servidor proxy cuando un dispositivo envía mensajes tooIoT concentrador.

Hola siguiente diagrama muestra Hola componentes principales de ejemplo de Hola, incluidos Hola módulos IoT borde:

![][1]

módulos de Hello no pasar los mensajes directamente tooeach otro. módulos de Hello publican a broker interna de mensajes tooan que ofrece toohello de mensajes de Hola otros módulos mediante un mecanismo de suscripción. Para más información, consulte [Introducción a Azure IoT Edge][lnk-gw-getstarted].

### <a name="protocol-ingestion-module"></a>Módulo de ingesta de protocolos

Este módulo es hello punto de partida para recibir datos de los dispositivos, a través de puerta de enlace de Hola y en la nube de Hola. En el ejemplo de Hola Hola módulo:

1. Crea datos de temperatura simulados. Si usa dispositivos físicos, módulo de hello lee datos de los dispositivos físicos.
1. Crea un mensaje.
1. Coloca los datos de temperatura de hello simulado en el contenido del mensaje de Hola.
1. Agrega una propiedad con un mensaje de toohello de dirección MAC falsa.
1. Hace que toohello disponible siguiente módulo de mensaje de Hola en cadena Hola.

módulo de Hello denominado **ingesta de protocolo X** en Hola se denomina diagrama anterior **dispositivo simulado** en el código fuente de Hola.

### <a name="mac-lt-gt-iot-hub-id-module"></a>Módulo de identificación MAC &lt;-&gt; IoT Hub

Este módulo busca los mensajes que tienen una propiedad de dirección de Mac. En el ejemplo de Hola, módulo de ingesta de hello protocol agrega propiedad de dirección MAC de Hola. Si el módulo de hello encuentra este tipo de propiedad, agrega otra propiedad con un mensaje de toohello clave de dispositivo de centro de IoT. módulo de Hello, a continuación, crea toohello disponible siguiente módulo de mensaje de Hola en cadena Hola.

desarrollador de Hello configura una asignación entre las direcciones MAC y dispositivos de centro de IoT identidades tooassociate Hola simulada con identidades de dispositivos del centro de IoT. Programador de Hello agrega asignación Hola manualmente como parte de la configuración del módulo Hola.

> [!NOTE]
> En este ejemplo se usa una dirección MAC como identificador único del dispositivo y se correlaciona con una identidad de dispositivo del Centro de IoT. Sin embargo, puede escribir su propio módulo para que utilice un identificador único diferente. Por ejemplo, los dispositivos pueden tener números de serie exclusivos o datos de telemetría de saludo pueden incluir un nombre de dispositivo incrustado único.

### <a name="iot-hub-communication-module"></a>Módulo de comunicación del Centro de IoT

Este módulo toma los mensajes con un centro de IoT propiedad de clave de dispositivo que haya sido asignado por el módulo anterior Hola. módulo de Hello envía mensajes de bienvenida del contenido tooIoT concentrador mediante Hola protocolo HTTP. HTTP es uno de hello tres protocolos entienden por centro de IoT.

En lugar de abrir una conexión para cada dispositivo simulado, este módulo abre una única conexión HTTP Hola puerta de enlace toohello centro de IoT. módulo hello multiplexes, a continuación, las conexiones desde todos los dispositivos de hello simulada través de esa conexión. Este enfoque permite a una sola puerta de enlace tooconnect muchos más dispositivos.

## <a name="before-you-get-started"></a>Antes de comenzar

Antes de comenzar, realice los siguientes pasos:

* [Crear un centro de IoT] [ lnk-create-hub] en su suscripción de Azure, se necesita Hola nombre de su toocomplete de base de datos central en este tutorial. Si no tiene ninguna, puede crear una [cuenta gratuita][lnk-free-trial] en tan solo unos minutos.
* Agregue el centro de IoT de dos dispositivos tooyour y tome nota de sus identificadores y las claves de dispositivo. Puede usar hello [explorador del dispositivo] [ lnk-device-explorer] o [el centro de IOT explorador] [ lnk-iothub-explorer] herramienta tooadd su centro de IoT de toohello de dispositivos que creó en hello anterior paso a paso y recuperar sus claves.

![][2]

<!-- Images -->
[1]: media/iot-hub-iot-edge-simulated-selector/image1.png
[2]: media/iot-hub-iot-edge-simulated-selector/image2.png

<!-- Links -->
[ejemplo en la nube de dispositivo simulado cargar]: https://github.com/Azure/iot-edge/blob/master/samples/simulated_device_cloud_upload/README.md
[lnk-sdk]: https://github.com/Azure/iot-edge
[lnk-gw-getstarted]: ../articles/iot-hub/iot-hub-linux-iot-edge-get-started.md
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-device-explorer]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer
[lnk-iothub-explorer]: https://github.com/Azure/iothub-explorer/blob/master/readme.md
[lnk-create-hub]: ../articles/iot-hub/iot-hub-create-through-portal.md