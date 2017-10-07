---
title: aaaGet a trabajar con el centro de IoT de Azure (Python) | Documentos de Microsoft
description: "Obtenga información acerca de cómo toosend dispositivo a la nube mensajes tooAzure centro de IoT con IoT SDK para Python. Crear dispositivo simulado y tooregister de aplicaciones de servicio, el dispositivo, enviar mensajes y leer los mensajes de centro de IoT."
services: iot-hub
author: dsk-2015
manager: timlt
editor: 
ms.service: iot-hub
ms.devlang: python
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: dkshir
ms.custom: na
ms.openlocfilehash: aa23e792fb144202e121274723bcfaeae0c04723
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-simulated-device-tooyour-iot-hub-using-python"></a>Conectar el centro de IoT dispositivo simulado tooyour usa Python
[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

Al final de Hola de este tutorial, tendrá dos aplicaciones de Python:

* **CreateDeviceIdentity.py**, que crea una identidad de dispositivo y la clave de seguridad asociadas tooconnect la aplicación de dispositivo simulado.
* **SimulatedDevice.py**, tooyour centro de IoT que conecta con la identidad del dispositivo Hola creado anteriormente y periódicamente envía una telemetría mensaje cuando se utiliza el protocolo MQTT Hola.

> [!NOTE]
> artículo de Hello [SDK de Azure IoT] [ lnk-hub-sdks] proporciona información acerca de hello Azure IoT SDK que puede usar ambos toorun aplicaciones toobuild en dispositivos y el back-end de soluciones.
> 
> 

toocomplete este tutorial, necesita Hola siguientes:

* [Python 2.x o 3.x][lnk-python-download]. Hacer seguro toouse Hola 32 ó 64 bits instalación según sea necesario por el programa de instalación. Cuando se le solicite durante la instalación de hello, asegúrese de variable de entorno específicas de la plataforma de tooyour de Python de tooadd seguro. Si usas Python 2.x, puede que necesite demasiado[instalar o actualizar *pip*, Python hello paquete sistema de administración de][lnk-install-pip].
* Si está usando Windows OS, entonces [paquete redistribuible de Visual C++] [ lnk-visual-c-redist] tooallow uso de Hola de archivos DLL nativos de Python.
* [Node.js 4.0 o posterior][lnk-node-download]. Hacer seguro toouse Hola 32 ó 64 bits instalación según sea necesario por el programa de instalación. Esto es necesario tooinstall hello [herramienta Explorador de centro de IoT][lnk-iot-hub-explorer].
* Una cuenta de Azure activa. Si no tiene ninguna, puede crear una [cuenta gratuita][lnk-free-trial] en tan solo unos minutos.

> [!NOTE]
> Hola *pip* empaqueta para su `azure-iothub-service-client` y `azure-iothub-device-client` están actualmente disponibles sólo para el sistema operativo Windows. Para Linux o Mac OS, consulte la sección toohello secciones específicas del sistema operativo Mac y Linux en hello [preparar el entorno de desarrollo para Python] [ lnk-python-devbox] post.
> 

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

Ahora ha creado su instancia de IoT Hub. Usar nombre de host del centro de IoT de Hola y Hola cadena de conexión de centro de IoT resto Hola de este tutorial.

> [!NOTE]
> También puede crear fácilmente su centro de IoT en una línea de comandos mediante Hola Python o Node.js basado en CLI de Azure. artículo de Hello [crear un centro de IoT con hello Azure CLI 2.0] [ lnk-azure-cli-hub] Hola pasos rápidos toodo por lo que se muestra. 
> 

## <a name="create-a-device-identity"></a>Creación de una identidad de dispositivo
Esta sección enumeran Hola pasos toocreate una aplicación de consola de Python, que crea una identidad de dispositivo en el registro de la identidad de Hola de su centro de IoT. Un dispositivo solo puede conectarse tooIoT concentrador, si existe una entrada en el registro de la identidad de Hola. Para obtener más información, vea hello **del registro de identidad** sección de hello [Guía del desarrollador de centro de IoT][lnk-devguide-identity]. Al ejecutar esta aplicación de consola, se generará un identificador de dispositivo único y clave que el dispositivo pueda usar tooidentify propio cuando el dispositivo a la nube sitio envía mensajes tooIoT concentrador.

1. Abra un símbolo del sistema e instale hello **Azure IoT Hub servicio SDK para Python**. Cierre el símbolo del sistema de hello después de instalar el SDK de Hola.

    ```
    pip install azure-iothub-service-client
    ```

2. Cree un archivo de Python denominado **CreateDeviceIdentity.py**. Abrir en [un editor/IDE de Python de su elección][lnk-python-ide-list], por ejemplo, Hola predeterminado [inactivo][lnk-idle].

3. Agregue Hola siguientes módulos de código tooimport Hola necesaria de servicio Hola SDK:

    ```python
    import sys
    import iothub_service_client
    from iothub_service_client import IoTHubRegistryManager, IoTHubRegistryManagerAuthMethod
    from iothub_service_client import IoTHubDeviceStatus, IoTHubError
    ```
2. Agregar Hola después de código, reemplace el marcador de posición de Hola para `[IoTHub Connection String]` con la cadena de conexión de hello para el centro de IoT de Hola que creó en la sección anterior de Hola. Puede utilizar cualquier nombre como hello `DEVICE_ID`.
   
    ```python
    CONNECTION_STRING = "[IoTHub Connection String]"
    DEVICE_ID = "MyFirstPythonDevice"
    ```
   [!INCLUDE [iot-hub-pii-note-naming-device](../../includes/iot-hub-pii-note-naming-device.md)]

3. Agregar Hola después de la función tooprint parte de información de dispositivo de Hola.

    ```python
    def print_device_info(title, iothub_device):
        print ( title + ":" )
        print ( "iothubDevice.deviceId                    = {0}".format(iothub_device.deviceId) )
        print ( "iothubDevice.primaryKey                  = {0}".format(iothub_device.primaryKey) )
        print ( "iothubDevice.secondaryKey                = {0}".format(iothub_device.secondaryKey) )
        print ( "iothubDevice.connectionState             = {0}".format(iothub_device.connectionState) )
        print ( "iothubDevice.status                      = {0}".format(iothub_device.status) )
        print ( "iothubDevice.lastActivityTime            = {0}".format(iothub_device.lastActivityTime) )
        print ( "iothubDevice.cloudToDeviceMessageCount   = {0}".format(iothub_device.cloudToDeviceMessageCount) )
        print ( "iothubDevice.isManaged                   = {0}".format(iothub_device.isManaged) )
        print ( "iothubDevice.authMethod                  = {0}".format(iothub_device.authMethod) )
        print ( "" )
    ```
3. Agregar Hola después de la función toocreate Hola dispositivo identificación mediante Hola administrador del registro. 

    ```python
    def iothub_createdevice():
        try:
            iothub_registry_manager = IoTHubRegistryManager(CONNECTION_STRING)
            auth_method = IoTHubRegistryManagerAuthMethod.SHARED_PRIVATE_KEY
            new_device = iothub_registry_manager.create_device(DEVICE_ID, "", "", auth_method)
            print_device_info("CreateDevice", new_device)

        except IoTHubError as iothub_error:
            print ( "Unexpected error {0}".format(iothub_error) )
            return
        except KeyboardInterrupt:
            print ( "iothub_createdevice stopped" )
    ```
4. Por último, agregar la función principal de hello como se indica a continuación y guarde el archivo de Hola.

    ```python
    if __name__ == '__main__':
        print ( "" )
        print ( "Python {0}".format(sys.version) )
        print ( "Creating device using hello Azure IoT Hub Service SDK for Python" )
        print ( "" )
        print ( "    Connection string = {0}".format(CONNECTION_STRING) )
        print ( "    Device ID         = {0}".format(DEVICE_ID) )

        iothub_createdevice()
    ```
5. En el símbolo de hello, ejecute hello **CreateDeviceIdentity.py** como se indica a continuación:

    ```python
    python CreateDeviceIdentity.py
    ```
6. Debería ver el dispositivo simulado Hola obtener creado. Tome nota de hello **deviceId** hello y **primaryKey** de este dispositivo. Necesita estos valores más tarde cuando se crea una aplicación que se conecta tooIoT concentrador como un dispositivo.

    ![Dispositivo creado][1]

> [!NOTE]
> Hola del registro de identidad de centro de IoT solo almacena centro de IoT toohello de dispositivo identidades tooenable un acceso seguro. Toouse de identificadores y las claves de dispositivo almacena como credenciales de seguridad y una marca de habilitado/deshabilitado que puede usar acceso toodisable para un dispositivo individual. Si la aplicación necesita toostore otros metadatos específicos del dispositivo, debe usar un almacén específico de la aplicación. Para obtener más información, vea hello [Guía del desarrollador de centro de IoT][lnk-devguide-identity].
> 
> 


## <a name="create-a-simulated-device-app"></a>Creación de una aplicación de dispositivo simulado
Esta sección enumeran Hola pasos toocreate una aplicación de consola de Python, que simula un dispositivo y envía el centro de IoT tooyour de mensajes del dispositivo a la nube.

1. Abra un nuevo símbolo e instale hello Azure IoT Hub dispositivo SDK para Python como se indica a continuación. Cierre el símbolo de hello después de la instalación de Hola.

    ```
    pip install azure-iothub-device-client
    ```
2. Cree un archivo y llámelo **SimulatedDevice.py**. Ábralo en el editor/IDE de Python que prefiera (por ejemplo, IDLE).

3. Agregar Hola siguientes módulos de código tooimport Hola necesario de dispositivo de hello SDK.

    ```python
    import random
    import time
    import sys
    import iothub_client
    from iothub_client import IoTHubClient, IoTHubClientError, IoTHubTransportProvider, IoTHubClientResult
    from iothub_client import IoTHubMessage, IoTHubMessageDispositionResult, IoTHubError, DeviceMethodReturnValue
    ```
4. Agregue el código siguiente de Hola y reemplace el marcador de posición de Hola para `[IoTHub Device Connection String]` con la cadena de conexión de hello para el dispositivo. cadena de conexión de dispositivo de Hello normalmente está en formato de Hola de `HostName=<hostName>;DeviceId=<deviceId>;SharedAccessKey=<primaryKey>`. Hola de uso **deviceId** y **primaryKey** de dispositivo de Hola que creó en Hola de hello anterior sección tooreplace `<deviceId>` y `<primaryKey>` respectivamente. Reemplace `<hostName>` por el nombre de host de su instancia de IoT Hub, que normalmente aparece como `<IoT hub name>.azure-devices.net`.

    ```python
    # String containing Hostname, Device Id & Device Key in hello format
    CONNECTION_STRING = "[IoTHub Device Connection String]"
    # choose HTTP, AMQP or MQTT as transport protocol
    PROTOCOL = IoTHubTransportProvider.MQTT
    MESSAGE_TIMEOUT = 10000
    AVG_WIND_SPEED = 10.0
    SEND_CALLBACKS = 0
    MSG_TXT = "{\"deviceId\": \"MyFirstPythonDevice\",\"windSpeed\": %.2f}"    
    ```
5. Agregar Hola después de una devolución de llamada de confirmación de envío del código toodefine. 

    ```python
    def send_confirmation_callback(message, result, user_context):
        global SEND_CALLBACKS
        print ( "Confirmation[%d] received for message with result = %s" % (user_context, result) )
        map_properties = message.properties()
        print ( "    message_id: %s" % message.message_id )
        print ( "    correlation_id: %s" % message.correlation_id )
        key_value_pair = map_properties.get_internals()
        print ( "    Properties: %s" % key_value_pair )
        SEND_CALLBACKS += 1
        print ( "    Total calls confirmed: %d" % SEND_CALLBACKS )
    ```
6. Agregar Hola después código tooinitialize Hola de cliente de dispositivo.

    ```python
    def iothub_client_init():
        # prepare iothub client
        client = IoTHubClient(CONNECTION_STRING, PROTOCOL)
        # set hello time until a message times out
        client.set_option("messageTimeout", MESSAGE_TIMEOUT)
        client.set_option("logtrace", 0)
        return client
    ```
7. Agregar función tooformat del siguiente hello y enviar un mensaje desde el centro de IoT tooyour dispositivo simulado.

    ```python
    def iothub_client_telemetry_sample_run():

        try:
            client = iothub_client_init()
            print ( "IoT Hub device sending periodic messages, press Ctrl-C tooexit" )
            message_counter = 0

            while True:
                msg_txt_formatted = MSG_TXT % (AVG_WIND_SPEED + (random.random() * 4 + 2))
                # messages can be encoded as string or bytearray
                if (message_counter & 1) == 1:
                    message = IoTHubMessage(bytearray(msg_txt_formatted, 'utf8'))
                else:
                    message = IoTHubMessage(msg_txt_formatted)
                # optional: assign ids
                message.message_id = "message_%d" % message_counter
                message.correlation_id = "correlation_%d" % message_counter
                # optional: assign properties
                prop_map = message.properties()
                prop_text = "PropMsg_%d" % message_counter
                prop_map.add("Property", prop_text)

                client.send_event_async(message, send_confirmation_callback, message_counter)
                print ( "IoTHubClient.send_event_async accepted message [%d] for transmission tooIoT Hub." % message_counter )

                status = client.get_send_status()
                print ( "Send status: %s" % status )
                time.sleep(30)

                status = client.get_send_status()
                print ( "Send status: %s" % status )

                message_counter += 1

        except IoTHubError as iothub_error:
            print ( "Unexpected error %s from IoTHub" % iothub_error )
            return
        except KeyboardInterrupt:
            print ( "IoTHubClient sample stopped" )
    ```
8. Finalmente, agregue la función main de Hola. 

    ```python
    if __name__ == '__main__':
        print ( "Simulating a device using hello Azure IoT Hub Device SDK for Python" )
        print ( "    Protocol %s" % PROTOCOL )
        print ( "    Connection string=%s" % CONNECTION_STRING )

        iothub_client_telemetry_sample_run()
    ```
9. Guarde y cierre hello **SimulatedDevice.py** archivo. Se está ahora listo toorun esta aplicación.

> [!NOTE]
> tookeep cosas simples, este tutorial no implementa ninguna directiva de reintento. En el código de producción, debe implementar directivas de reintento (por ejemplo, un retroceso exponencial), como se indica en el artículo de MSDN de hello [control de errores transitorios][lnk-transient-faults].
> 
> 

## <a name="receive-messages-from-your-simulated-device"></a>Recepción de mensajes procedentes del dispositivo simulado
mensajes de telemetría de tooreceive desde el dispositivo, deberá toouse un [centros de eventos][lnk-event-hubs-overview]-compatible extremo expuesto por hello centro de IoT, que lee los mensajes de Hola dispositivo a la nube. Hola de lectura [empezar a trabajar con concentradores de eventos] [ lnk-eventhubs-tutorial] tutorial para obtener información sobre cómo tooprocess mensajes desde los centros de eventos para el punto de conexión del su centro de IoT concentrador de eventos-compatible. Centros de eventos no admiten telemetría en Python aún, por lo que puede crear un [Node.js](iot-hub-node-node-getstarted.md#D2C_node) o un [.NET](iot-hub-csharp-csharp-getstarted.md#D2C_csharp) mensajes tooread Hola dispositivo a la nube de la aplicación de consola basada en los centros de eventos desde el centro de IoT. Este tutorial muestra cómo puede utilizar hello [herramienta Explorador de centro de IoT] [ lnk-iot-hub-explorer] tooread estos mensajes del dispositivo.

1. Abra un símbolo del sistema e instale Hola IoT Hub explorador. 

    ```
    npm install -g iothub-explorer
    ```

2. Ejecute hello siguiente comando en el símbolo del sistema de hello, supervisión toobegin Hola mensajes de dispositivo a la nube del dispositivo. Usar cadena de conexión del su centro de IoT marcador de posición de hello después `--login`.

    ```
    iothub-explorer monitor-events MyFirstPythonDevice --login "[IoTHub connection string]"
    ```

3. Abra un nuevo símbolo del sistema y desplácese directory toohello que contiene hello **SimulatedDevice.py** archivo.

4. Ejecute hello **SimulatedDevice.py** archivo que envía periódicamente centro de IoT de tooyour de datos de telemetría. 
   
    ```
    python SimulatedDevice.py
    ```
5. Observe los mensajes de dispositivo de hello en hello símbolo del sistema ejecutando Hola IoT Hub explorador desde la sección anterior de Hola. 

    ![Mensajes de Python del dispositivo a la nube][2]

## <a name="next-steps"></a>Pasos siguientes
En este tutorial, configura un nuevo centro de IoT Hola portal de Azure y, a continuación, crea una identidad de dispositivo en el registro de identidad del centro de IoT Hola. Usar este dispositivo identidad tooenable Hola simulada dispositivos aplicación toosend mensajes del dispositivo a la nube toohello centro de IoT. Observar los mensajes de saludo recibidos por centro de IoT Hola con ayuda de Hola de herramienta del explorador de centro de IoT Hola. 

Hola tooexplore SDK de Python para el uso del centro de IoT de Azure en profundidad, visite [este repositorio de Git concentrador][lnk-python-github]. tooreview capacidades de mensajería de Hola de hello Azure IoT Hub servicio SDK para Python, puede descargar y ejecutar [iothub_messaging_sample.py][lnk-messaging-sample]. Para usar hello Azure IoT Hub dispositivo SDK para Python la simulación de lado del dispositivo, puede descargar y ejecutar hello [iothub_client_sample.py][lnk-client-sample].

toocontinue introducción con el centro de IoT y tooexplore otros escenarios de IoT, vea:

* [Conexión del dispositivo][lnk-connect-device]
* [Introducción a la administración de dispositivos][lnk-device-management]
* [Introducción a Azure IoT Edge][lnk-iot-edge]

toolearn tooextend mensajes de dispositivo a la nube de su solución y proceso de IoT a escala, vea hello [procesar mensajes del dispositivo a la nube] [ lnk-process-d2c-tutorial] tutorial.
[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]

<!-- Images. -->
[1]: ./media/iot-hub-python-getstarted/createdevice.png
[2]: ./media/iot-hub-python-getstarted/sendd2cmessage.png

<!-- Links -->
[lnk-python-download]: https://www.python.org/downloads/
[lnk-visual-c-redist]: http://www.microsoft.com/download/confirmation.aspx?id=48145
[lnk-node-download]: https://nodejs.org/en/download/
[lnk-install-pip]: https://pip.pypa.io/en/stable/installing/
[lnk-azure-cli-hub]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-create-using-cli
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-idle]: https://docs.python.org/3/library/idle.html
[lnk-python-ide-list]: https://wiki.python.org/moin/IntegratedDevelopmentEnvironments
[lnk-iot-hub-explorer]: https://github.com/Azure/iothub-explorer
[lnk-python-github]: https://github.com/Azure/azure-iot-sdk-python
[lnk-messaging-sample]: https://github.com/Azure/azure-iot-sdk-python/blob/master/service/samples/iothub_messaging_sample.py
[lnk-client-sample]: https://github.com/Azure/azure-iot-sdk-python/blob/master/device/samples/iothub_client_sample.py

[lnk-eventhubs-tutorial]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md
[lnk-devguide-identity]: iot-hub-devguide-identity-registry.md
[lnk-event-hubs-overview]: ../event-hubs/event-hubs-overview.md
[lnk-python-devbox]: https://github.com/Azure/azure-iot-sdk-python/blob/master/doc/python-devbox-setup.md

[lnk-process-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/
