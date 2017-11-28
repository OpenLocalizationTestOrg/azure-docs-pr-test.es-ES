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
# <a name="connect-your-simulated-device-tooyour-iot-hub-using-python"></a><span data-ttu-id="05041-104">Conectar el centro de IoT dispositivo simulado tooyour usa Python</span><span class="sxs-lookup"><span data-stu-id="05041-104">Connect your simulated device tooyour IoT hub using Python</span></span>
[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

<span data-ttu-id="05041-105">Al final de Hola de este tutorial, tendrá dos aplicaciones de Python:</span><span class="sxs-lookup"><span data-stu-id="05041-105">At hello end of this tutorial, you will have two Python apps:</span></span>

* <span data-ttu-id="05041-106">**CreateDeviceIdentity.py**, que crea una identidad de dispositivo y la clave de seguridad asociadas tooconnect la aplicación de dispositivo simulado.</span><span class="sxs-lookup"><span data-stu-id="05041-106">**CreateDeviceIdentity.py**, which creates a device identity and associated security key tooconnect your simulated device app.</span></span>
* <span data-ttu-id="05041-107">**SimulatedDevice.py**, tooyour centro de IoT que conecta con la identidad del dispositivo Hola creado anteriormente y periódicamente envía una telemetría mensaje cuando se utiliza el protocolo MQTT Hola.</span><span class="sxs-lookup"><span data-stu-id="05041-107">**SimulatedDevice.py**, which connects tooyour IoT hub with hello device identity created earlier, and periodically sends a telemetry message using hello MQTT protocol.</span></span>

> [!NOTE]
> <span data-ttu-id="05041-108">artículo de Hello [SDK de Azure IoT] [ lnk-hub-sdks] proporciona información acerca de hello Azure IoT SDK que puede usar ambos toorun aplicaciones toobuild en dispositivos y el back-end de soluciones.</span><span class="sxs-lookup"><span data-stu-id="05041-108">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both applications toorun on devices and your solution back end.</span></span>
> 
> 

<span data-ttu-id="05041-109">toocomplete este tutorial, necesita Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="05041-109">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="05041-110">[Python 2.x o 3.x][lnk-python-download].</span><span class="sxs-lookup"><span data-stu-id="05041-110">[Python 2.x or 3.x][lnk-python-download].</span></span> <span data-ttu-id="05041-111">Hacer seguro toouse Hola 32 ó 64 bits instalación según sea necesario por el programa de instalación.</span><span class="sxs-lookup"><span data-stu-id="05041-111">Make sure toouse hello 32-bit or 64-bit installation as required by your setup.</span></span> <span data-ttu-id="05041-112">Cuando se le solicite durante la instalación de hello, asegúrese de variable de entorno específicas de la plataforma de tooyour de Python de tooadd seguro.</span><span class="sxs-lookup"><span data-stu-id="05041-112">When prompted during hello installation, make sure tooadd Python tooyour platform-specific environment variable.</span></span> <span data-ttu-id="05041-113">Si usas Python 2.x, puede que necesite demasiado[instalar o actualizar *pip*, Python hello paquete sistema de administración de][lnk-install-pip].</span><span class="sxs-lookup"><span data-stu-id="05041-113">If you are using Python 2.x, you may need too[install or upgrade *pip*, hello Python package management system][lnk-install-pip].</span></span>
* <span data-ttu-id="05041-114">Si está usando Windows OS, entonces [paquete redistribuible de Visual C++] [ lnk-visual-c-redist] tooallow uso de Hola de archivos DLL nativos de Python.</span><span class="sxs-lookup"><span data-stu-id="05041-114">If you are using Windows OS, then [Visual C++ redistributable package][lnk-visual-c-redist] tooallow hello use of native DLLs from Python.</span></span>
* <span data-ttu-id="05041-115">[Node.js 4.0 o posterior][lnk-node-download].</span><span class="sxs-lookup"><span data-stu-id="05041-115">[Node.js 4.0 or later][lnk-node-download].</span></span> <span data-ttu-id="05041-116">Hacer seguro toouse Hola 32 ó 64 bits instalación según sea necesario por el programa de instalación.</span><span class="sxs-lookup"><span data-stu-id="05041-116">Make sure toouse hello 32-bit or 64-bit installation as required by your setup.</span></span> <span data-ttu-id="05041-117">Esto es necesario tooinstall hello [herramienta Explorador de centro de IoT][lnk-iot-hub-explorer].</span><span class="sxs-lookup"><span data-stu-id="05041-117">This is needed tooinstall hello [IoT Hub Explorer tool][lnk-iot-hub-explorer].</span></span>
* <span data-ttu-id="05041-118">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="05041-118">An active Azure account.</span></span> <span data-ttu-id="05041-119">Si no tiene ninguna, puede crear una [cuenta gratuita][lnk-free-trial] en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="05041-119">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>

> [!NOTE]
> <span data-ttu-id="05041-120">Hola *pip* empaqueta para su `azure-iothub-service-client` y `azure-iothub-device-client` están actualmente disponibles sólo para el sistema operativo Windows.</span><span class="sxs-lookup"><span data-stu-id="05041-120">hello *pip* packages for `azure-iothub-service-client` and `azure-iothub-device-client` are currently available only for Windows OS.</span></span> <span data-ttu-id="05041-121">Para Linux o Mac OS, consulte la sección toohello secciones específicas del sistema operativo Mac y Linux en hello [preparar el entorno de desarrollo para Python] [ lnk-python-devbox] post.</span><span class="sxs-lookup"><span data-stu-id="05041-121">For Linux/Mac OS, please refer toohello Linux and Mac OS-specific sections on hello [Prepare your development environment for Python][lnk-python-devbox] post.</span></span>
> 

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

<span data-ttu-id="05041-122">Ahora ha creado su instancia de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="05041-122">You have now created your IoT hub.</span></span> <span data-ttu-id="05041-123">Usar nombre de host del centro de IoT de Hola y Hola cadena de conexión de centro de IoT resto Hola de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="05041-123">Use hello IoT Hub host name and hello IoT Hub connection string in hello rest of this tutorial.</span></span>

> [!NOTE]
> <span data-ttu-id="05041-124">También puede crear fácilmente su centro de IoT en una línea de comandos mediante Hola Python o Node.js basado en CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="05041-124">You can also easily create your IoT hub on a command line, using hello Python or Node.js based Azure CLI.</span></span> <span data-ttu-id="05041-125">artículo de Hello [crear un centro de IoT con hello Azure CLI 2.0] [ lnk-azure-cli-hub] Hola pasos rápidos toodo por lo que se muestra.</span><span class="sxs-lookup"><span data-stu-id="05041-125">hello article [Create an IoT hub using hello Azure CLI 2.0][lnk-azure-cli-hub] shows you hello quick steps toodo so.</span></span> 
> 

## <a name="create-a-device-identity"></a><span data-ttu-id="05041-126">Creación de una identidad de dispositivo</span><span class="sxs-lookup"><span data-stu-id="05041-126">Create a device identity</span></span>
<span data-ttu-id="05041-127">Esta sección enumeran Hola pasos toocreate una aplicación de consola de Python, que crea una identidad de dispositivo en el registro de la identidad de Hola de su centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="05041-127">This section lists hello steps toocreate a Python console app, that creates a device identity in hello identity registry of your IoT hub.</span></span> <span data-ttu-id="05041-128">Un dispositivo solo puede conectarse tooIoT concentrador, si existe una entrada en el registro de la identidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="05041-128">A device can only connect tooIoT Hub if it has an entry in hello identity registry.</span></span> <span data-ttu-id="05041-129">Para obtener más información, vea hello **del registro de identidad** sección de hello [Guía del desarrollador de centro de IoT][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="05041-129">For more information, see hello **Identity Registry** section of hello [IoT Hub developer guide][lnk-devguide-identity].</span></span> <span data-ttu-id="05041-130">Al ejecutar esta aplicación de consola, se generará un identificador de dispositivo único y clave que el dispositivo pueda usar tooidentify propio cuando el dispositivo a la nube sitio envía mensajes tooIoT concentrador.</span><span class="sxs-lookup"><span data-stu-id="05041-130">When you run this console app, it generates a unique device ID and key that your device can use tooidentify itself when it sends device-to-cloud messages tooIoT Hub.</span></span>

1. <span data-ttu-id="05041-131">Abra un símbolo del sistema e instale hello **Azure IoT Hub servicio SDK para Python**.</span><span class="sxs-lookup"><span data-stu-id="05041-131">Open a command prompt and install hello **Azure IoT Hub Service SDK for Python**.</span></span> <span data-ttu-id="05041-132">Cierre el símbolo del sistema de hello después de instalar el SDK de Hola.</span><span class="sxs-lookup"><span data-stu-id="05041-132">Close hello command prompt after you install hello SDK.</span></span>

    ```
    pip install azure-iothub-service-client
    ```

2. <span data-ttu-id="05041-133">Cree un archivo de Python denominado **CreateDeviceIdentity.py**.</span><span class="sxs-lookup"><span data-stu-id="05041-133">Create a Python file named **CreateDeviceIdentity.py**.</span></span> <span data-ttu-id="05041-134">Abrir en [un editor/IDE de Python de su elección][lnk-python-ide-list], por ejemplo, Hola predeterminado [inactivo][lnk-idle].</span><span class="sxs-lookup"><span data-stu-id="05041-134">Open it in [a Python editor/IDE of your choice][lnk-python-ide-list], for example, hello default [IDLE][lnk-idle].</span></span>

3. <span data-ttu-id="05041-135">Agregue Hola siguientes módulos de código tooimport Hola necesaria de servicio Hola SDK:</span><span class="sxs-lookup"><span data-stu-id="05041-135">Add hello following code tooimport hello required modules from hello service SDK:</span></span>

    ```python
    import sys
    import iothub_service_client
    from iothub_service_client import IoTHubRegistryManager, IoTHubRegistryManagerAuthMethod
    from iothub_service_client import IoTHubDeviceStatus, IoTHubError
    ```
2. <span data-ttu-id="05041-136">Agregar Hola después de código, reemplace el marcador de posición de Hola para `[IoTHub Connection String]` con la cadena de conexión de hello para el centro de IoT de Hola que creó en la sección anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="05041-136">Add hello following code, replacing hello placeholder for `[IoTHub Connection String]` with hello connection string for hello IoT hub you created in hello previous section.</span></span> <span data-ttu-id="05041-137">Puede utilizar cualquier nombre como hello `DEVICE_ID`.</span><span class="sxs-lookup"><span data-stu-id="05041-137">You can use any name as hello `DEVICE_ID`.</span></span>
   
    ```python
    CONNECTION_STRING = "[IoTHub Connection String]"
    DEVICE_ID = "MyFirstPythonDevice"
    ```
   [!INCLUDE [iot-hub-pii-note-naming-device](../../includes/iot-hub-pii-note-naming-device.md)]

3. <span data-ttu-id="05041-138">Agregar Hola después de la función tooprint parte de información de dispositivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="05041-138">Add hello following function tooprint some of hello device information.</span></span>

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
3. <span data-ttu-id="05041-139">Agregar Hola después de la función toocreate Hola dispositivo identificación mediante Hola administrador del registro.</span><span class="sxs-lookup"><span data-stu-id="05041-139">Add hello following function toocreate hello device identification using hello Registry Manager.</span></span> 

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
4. <span data-ttu-id="05041-140">Por último, agregar la función principal de hello como se indica a continuación y guarde el archivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="05041-140">Finally, add hello main function as follows and save hello file.</span></span>

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
5. <span data-ttu-id="05041-141">En el símbolo de hello, ejecute hello **CreateDeviceIdentity.py** como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="05041-141">On hello command prompt, run hello **CreateDeviceIdentity.py** as follows:</span></span>

    ```python
    python CreateDeviceIdentity.py
    ```
6. <span data-ttu-id="05041-142">Debería ver el dispositivo simulado Hola obtener creado.</span><span class="sxs-lookup"><span data-stu-id="05041-142">You should see hello simulated device getting created.</span></span> <span data-ttu-id="05041-143">Tome nota de hello **deviceId** hello y **primaryKey** de este dispositivo.</span><span class="sxs-lookup"><span data-stu-id="05041-143">Note down hello **deviceId** and hello **primaryKey** of this device.</span></span> <span data-ttu-id="05041-144">Necesita estos valores más tarde cuando se crea una aplicación que se conecta tooIoT concentrador como un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="05041-144">You need these values later when you create an application that connects tooIoT Hub as a device.</span></span>

    ![Dispositivo creado][1]

> [!NOTE]
> <span data-ttu-id="05041-146">Hola del registro de identidad de centro de IoT solo almacena centro de IoT toohello de dispositivo identidades tooenable un acceso seguro.</span><span class="sxs-lookup"><span data-stu-id="05041-146">hello IoT Hub identity registry only stores device identities tooenable secure access toohello IoT hub.</span></span> <span data-ttu-id="05041-147">Toouse de identificadores y las claves de dispositivo almacena como credenciales de seguridad y una marca de habilitado/deshabilitado que puede usar acceso toodisable para un dispositivo individual.</span><span class="sxs-lookup"><span data-stu-id="05041-147">It stores device IDs and keys toouse as security credentials and an enabled/disabled flag that you can use toodisable access for an individual device.</span></span> <span data-ttu-id="05041-148">Si la aplicación necesita toostore otros metadatos específicos del dispositivo, debe usar un almacén específico de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="05041-148">If your application needs toostore other device-specific metadata, it should use an application-specific store.</span></span> <span data-ttu-id="05041-149">Para obtener más información, vea hello [Guía del desarrollador de centro de IoT][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="05041-149">For more information, see hello [IoT Hub developer guide][lnk-devguide-identity].</span></span>
> 
> 


## <a name="create-a-simulated-device-app"></a><span data-ttu-id="05041-150">Creación de una aplicación de dispositivo simulado</span><span class="sxs-lookup"><span data-stu-id="05041-150">Create a simulated device app</span></span>
<span data-ttu-id="05041-151">Esta sección enumeran Hola pasos toocreate una aplicación de consola de Python, que simula un dispositivo y envía el centro de IoT tooyour de mensajes del dispositivo a la nube.</span><span class="sxs-lookup"><span data-stu-id="05041-151">This section lists hello steps toocreate a Python console app, that simulates a device and sends device-to-cloud messages tooyour IoT hub.</span></span>

1. <span data-ttu-id="05041-152">Abra un nuevo símbolo e instale hello Azure IoT Hub dispositivo SDK para Python como se indica a continuación.</span><span class="sxs-lookup"><span data-stu-id="05041-152">Open a new command prompt and install hello Azure IoT Hub Device SDK for Python as follows.</span></span> <span data-ttu-id="05041-153">Cierre el símbolo de hello después de la instalación de Hola.</span><span class="sxs-lookup"><span data-stu-id="05041-153">Close hello command prompt after hello installation.</span></span>

    ```
    pip install azure-iothub-device-client
    ```
2. <span data-ttu-id="05041-154">Cree un archivo y llámelo **SimulatedDevice.py**.</span><span class="sxs-lookup"><span data-stu-id="05041-154">Create a file named **SimulatedDevice.py**.</span></span> <span data-ttu-id="05041-155">Ábralo en el editor/IDE de Python que prefiera (por ejemplo, IDLE).</span><span class="sxs-lookup"><span data-stu-id="05041-155">Open this file in a Python editor/IDE of your choice (for example, IDLE).</span></span>

3. <span data-ttu-id="05041-156">Agregar Hola siguientes módulos de código tooimport Hola necesario de dispositivo de hello SDK.</span><span class="sxs-lookup"><span data-stu-id="05041-156">Add hello following code tooimport hello required modules from hello device SDK.</span></span>

    ```python
    import random
    import time
    import sys
    import iothub_client
    from iothub_client import IoTHubClient, IoTHubClientError, IoTHubTransportProvider, IoTHubClientResult
    from iothub_client import IoTHubMessage, IoTHubMessageDispositionResult, IoTHubError, DeviceMethodReturnValue
    ```
4. <span data-ttu-id="05041-157">Agregue el código siguiente de Hola y reemplace el marcador de posición de Hola para `[IoTHub Device Connection String]` con la cadena de conexión de hello para el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="05041-157">Add hello following code and replace hello placeholder for `[IoTHub Device Connection String]` with hello connection string for your device.</span></span> <span data-ttu-id="05041-158">cadena de conexión de dispositivo de Hello normalmente está en formato de Hola de `HostName=<hostName>;DeviceId=<deviceId>;SharedAccessKey=<primaryKey>`.</span><span class="sxs-lookup"><span data-stu-id="05041-158">hello device connection string is usually in hello format of `HostName=<hostName>;DeviceId=<deviceId>;SharedAccessKey=<primaryKey>`.</span></span> <span data-ttu-id="05041-159">Hola de uso **deviceId** y **primaryKey** de dispositivo de Hola que creó en Hola de hello anterior sección tooreplace `<deviceId>` y `<primaryKey>` respectivamente.</span><span class="sxs-lookup"><span data-stu-id="05041-159">Use hello **deviceId** and **primaryKey** of hello device you created in hello previous section tooreplace hello `<deviceId>` and `<primaryKey>` respectively.</span></span> <span data-ttu-id="05041-160">Reemplace `<hostName>` por el nombre de host de su instancia de IoT Hub, que normalmente aparece como `<IoT hub name>.azure-devices.net`.</span><span class="sxs-lookup"><span data-stu-id="05041-160">Replace `<hostName>` with your IoT hub's host name, usually as `<IoT hub name>.azure-devices.net`.</span></span>

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
5. <span data-ttu-id="05041-161">Agregar Hola después de una devolución de llamada de confirmación de envío del código toodefine.</span><span class="sxs-lookup"><span data-stu-id="05041-161">Add hello following code toodefine a send confirmation callback.</span></span> 

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
6. <span data-ttu-id="05041-162">Agregar Hola después código tooinitialize Hola de cliente de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="05041-162">Add hello following code tooinitialize hello device client.</span></span>

    ```python
    def iothub_client_init():
        # prepare iothub client
        client = IoTHubClient(CONNECTION_STRING, PROTOCOL)
        # set hello time until a message times out
        client.set_option("messageTimeout", MESSAGE_TIMEOUT)
        client.set_option("logtrace", 0)
        return client
    ```
7. <span data-ttu-id="05041-163">Agregar función tooformat del siguiente hello y enviar un mensaje desde el centro de IoT tooyour dispositivo simulado.</span><span class="sxs-lookup"><span data-stu-id="05041-163">Add hello following function tooformat and send a message from your simulated device tooyour IoT hub.</span></span>

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
8. <span data-ttu-id="05041-164">Finalmente, agregue la función main de Hola.</span><span class="sxs-lookup"><span data-stu-id="05041-164">Finally, add hello main function.</span></span> 

    ```python
    if __name__ == '__main__':
        print ( "Simulating a device using hello Azure IoT Hub Device SDK for Python" )
        print ( "    Protocol %s" % PROTOCOL )
        print ( "    Connection string=%s" % CONNECTION_STRING )

        iothub_client_telemetry_sample_run()
    ```
9. <span data-ttu-id="05041-165">Guarde y cierre hello **SimulatedDevice.py** archivo.</span><span class="sxs-lookup"><span data-stu-id="05041-165">Save and close hello **SimulatedDevice.py** file.</span></span> <span data-ttu-id="05041-166">Se está ahora listo toorun esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="05041-166">You are now ready toorun this app.</span></span>

> [!NOTE]
> <span data-ttu-id="05041-167">tookeep cosas simples, este tutorial no implementa ninguna directiva de reintento.</span><span class="sxs-lookup"><span data-stu-id="05041-167">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="05041-168">En el código de producción, debe implementar directivas de reintento (por ejemplo, un retroceso exponencial), como se indica en el artículo de MSDN de hello [control de errores transitorios][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="05041-168">In production code, you should implement retry policies (such as an exponential backoff), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="receive-messages-from-your-simulated-device"></a><span data-ttu-id="05041-169">Recepción de mensajes procedentes del dispositivo simulado</span><span class="sxs-lookup"><span data-stu-id="05041-169">Receive messages from your simulated device</span></span>
<span data-ttu-id="05041-170">mensajes de telemetría de tooreceive desde el dispositivo, deberá toouse un [centros de eventos][lnk-event-hubs-overview]-compatible extremo expuesto por hello centro de IoT, que lee los mensajes de Hola dispositivo a la nube.</span><span class="sxs-lookup"><span data-stu-id="05041-170">tooreceive telemetry messages from your device, you need toouse an [Event Hubs][lnk-event-hubs-overview]-compatible endpoint exposed by hello IoT Hub, which reads hello device-to-cloud messages.</span></span> <span data-ttu-id="05041-171">Hola de lectura [empezar a trabajar con concentradores de eventos] [ lnk-eventhubs-tutorial] tutorial para obtener información sobre cómo tooprocess mensajes desde los centros de eventos para el punto de conexión del su centro de IoT concentrador de eventos-compatible.</span><span class="sxs-lookup"><span data-stu-id="05041-171">Read hello [Get Started with Event Hubs][lnk-eventhubs-tutorial] tutorial for information on how tooprocess messages from Event Hubs for your IoT hub's Event Hub-compatible endpoint.</span></span> <span data-ttu-id="05041-172">Centros de eventos no admiten telemetría en Python aún, por lo que puede crear un [Node.js](iot-hub-node-node-getstarted.md#D2C_node) o un [.NET](iot-hub-csharp-csharp-getstarted.md#D2C_csharp) mensajes tooread Hola dispositivo a la nube de la aplicación de consola basada en los centros de eventos desde el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="05041-172">Event Hubs does not support telemetry in Python yet, so you can either create a [Node.js](iot-hub-node-node-getstarted.md#D2C_node) or a [.NET](iot-hub-csharp-csharp-getstarted.md#D2C_csharp) Event Hubs-based console app tooread hello device-to-cloud messages from IoT Hub.</span></span> <span data-ttu-id="05041-173">Este tutorial muestra cómo puede utilizar hello [herramienta Explorador de centro de IoT] [ lnk-iot-hub-explorer] tooread estos mensajes del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="05041-173">This tutorial shows how you can use hello [IoT Hub Explorer tool][lnk-iot-hub-explorer] tooread these device messages.</span></span>

1. <span data-ttu-id="05041-174">Abra un símbolo del sistema e instale Hola IoT Hub explorador.</span><span class="sxs-lookup"><span data-stu-id="05041-174">Open a command prompt and install hello IoT Hub Explorer.</span></span> 

    ```
    npm install -g iothub-explorer
    ```

2. <span data-ttu-id="05041-175">Ejecute hello siguiente comando en el símbolo del sistema de hello, supervisión toobegin Hola mensajes de dispositivo a la nube del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="05041-175">Run hello following command on hello command prompt, toobegin monitoring hello device-to-cloud messages from your device.</span></span> <span data-ttu-id="05041-176">Usar cadena de conexión del su centro de IoT marcador de posición de hello después `--login`.</span><span class="sxs-lookup"><span data-stu-id="05041-176">Use your IoT hub's connection string in hello placeholder after `--login`.</span></span>

    ```
    iothub-explorer monitor-events MyFirstPythonDevice --login "[IoTHub connection string]"
    ```

3. <span data-ttu-id="05041-177">Abra un nuevo símbolo del sistema y desplácese directory toohello que contiene hello **SimulatedDevice.py** archivo.</span><span class="sxs-lookup"><span data-stu-id="05041-177">Open a new command prompt and navigate toohello directory containing hello **SimulatedDevice.py** file.</span></span>

4. <span data-ttu-id="05041-178">Ejecute hello **SimulatedDevice.py** archivo que envía periódicamente centro de IoT de tooyour de datos de telemetría.</span><span class="sxs-lookup"><span data-stu-id="05041-178">Run hello **SimulatedDevice.py** file, which periodically sends telemetry data tooyour IoT hub.</span></span> 
   
    ```
    python SimulatedDevice.py
    ```
5. <span data-ttu-id="05041-179">Observe los mensajes de dispositivo de hello en hello símbolo del sistema ejecutando Hola IoT Hub explorador desde la sección anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="05041-179">Observe hello device messages on hello command prompt running hello IoT Hub Explorer from hello previous section.</span></span> 

    ![Mensajes de Python del dispositivo a la nube][2]

## <a name="next-steps"></a><span data-ttu-id="05041-181">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="05041-181">Next steps</span></span>
<span data-ttu-id="05041-182">En este tutorial, configura un nuevo centro de IoT Hola portal de Azure y, a continuación, crea una identidad de dispositivo en el registro de identidad del centro de IoT Hola.</span><span class="sxs-lookup"><span data-stu-id="05041-182">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="05041-183">Usar este dispositivo identidad tooenable Hola simulada dispositivos aplicación toosend mensajes del dispositivo a la nube toohello centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="05041-183">You used this device identity tooenable hello simulated device app toosend device-to-cloud messages toohello IoT hub.</span></span> <span data-ttu-id="05041-184">Observar los mensajes de saludo recibidos por centro de IoT Hola con ayuda de Hola de herramienta del explorador de centro de IoT Hola.</span><span class="sxs-lookup"><span data-stu-id="05041-184">You observed hello messages received by hello IoT hub with hello help of hello IoT Hub Explorer tool.</span></span> 

<span data-ttu-id="05041-185">Hola tooexplore SDK de Python para el uso del centro de IoT de Azure en profundidad, visite [este repositorio de Git concentrador][lnk-python-github].</span><span class="sxs-lookup"><span data-stu-id="05041-185">tooexplore hello Python SDK for Azure IoT Hub usage in depth, visit [this Git Hub repo][lnk-python-github].</span></span> <span data-ttu-id="05041-186">tooreview capacidades de mensajería de Hola de hello Azure IoT Hub servicio SDK para Python, puede descargar y ejecutar [iothub_messaging_sample.py][lnk-messaging-sample].</span><span class="sxs-lookup"><span data-stu-id="05041-186">tooreview hello messaging capabilities of hello Azure IoT Hub Service SDK for Python, you can download and run [iothub_messaging_sample.py][lnk-messaging-sample].</span></span> <span data-ttu-id="05041-187">Para usar hello Azure IoT Hub dispositivo SDK para Python la simulación de lado del dispositivo, puede descargar y ejecutar hello [iothub_client_sample.py][lnk-client-sample].</span><span class="sxs-lookup"><span data-stu-id="05041-187">For device side simulation using hello Azure IoT Hub Device SDK for Python, you can download and run hello [iothub_client_sample.py][lnk-client-sample].</span></span>

<span data-ttu-id="05041-188">toocontinue introducción con el centro de IoT y tooexplore otros escenarios de IoT, vea:</span><span class="sxs-lookup"><span data-stu-id="05041-188">toocontinue getting started with IoT Hub and tooexplore other IoT scenarios, see:</span></span>

* <span data-ttu-id="05041-189">[Conexión del dispositivo][lnk-connect-device]</span><span class="sxs-lookup"><span data-stu-id="05041-189">[Connecting your device][lnk-connect-device]</span></span>
* <span data-ttu-id="05041-190">[Introducción a la administración de dispositivos][lnk-device-management]</span><span class="sxs-lookup"><span data-stu-id="05041-190">[Getting started with device management][lnk-device-management]</span></span>
* <span data-ttu-id="05041-191">[Introducción a Azure IoT Edge][lnk-iot-edge]</span><span class="sxs-lookup"><span data-stu-id="05041-191">[Getting started with Azure IoT Edge][lnk-iot-edge]</span></span>

<span data-ttu-id="05041-192">toolearn tooextend mensajes de dispositivo a la nube de su solución y proceso de IoT a escala, vea hello [procesar mensajes del dispositivo a la nube] [ lnk-process-d2c-tutorial] tutorial.</span><span class="sxs-lookup"><span data-stu-id="05041-192">toolearn how tooextend your IoT solution and process device-to-cloud messages at scale, see hello [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span>
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
