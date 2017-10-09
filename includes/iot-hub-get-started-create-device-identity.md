## <a name="create-a-device-identity"></a><span data-ttu-id="b4d85-101">Creación de una identidad de dispositivo</span><span class="sxs-lookup"><span data-stu-id="b4d85-101">Create a device identity</span></span>

<span data-ttu-id="b4d85-102">En esta sección, utilice una herramienta de Node.js denominada [el centro de IOT explorador] [ iot-hub-explorer] toocreate una identidad de dispositivo para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="b4d85-102">In this section, you use a Node.js tool called [iothub-explorer][iot-hub-explorer] toocreate a device identity for this tutorial.</span></span> <span data-ttu-id="b4d85-103">Los identificadores de dispositivos distinguen mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="b4d85-103">Device IDs are case sensitive.</span></span>

1. <span data-ttu-id="b4d85-104">Ejecute hello siguiente en su entorno de línea de comandos:</span><span class="sxs-lookup"><span data-stu-id="b4d85-104">Run hello following in your command-line environment:</span></span>

    `npm install -g iothub-explorer@latest`

1. <span data-ttu-id="b4d85-105">A continuación, ejecute hello después de concentrador de comando toologin tooyour.</span><span class="sxs-lookup"><span data-stu-id="b4d85-105">Then, run hello following command toologin tooyour hub.</span></span> <span data-ttu-id="b4d85-106">SUBSTITUTE `{iot hub connection string}` con hello cadena de conexión de centro de IoT copió anteriormente:</span><span class="sxs-lookup"><span data-stu-id="b4d85-106">Substitute `{iot hub connection string}` with hello IoT Hub connection string you previously copied:</span></span>

    `iothub-explorer login "{iot hub connection string}"`

1. <span data-ttu-id="b4d85-107">Por último, cree una nueva identidad de dispositivo llama `myDeviceId` con el comando hello:</span><span class="sxs-lookup"><span data-stu-id="b4d85-107">Finally, create a new device identity called `myDeviceId` with hello command:</span></span>

    `iothub-explorer create myDeviceId --connection-string`

   [!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

<span data-ttu-id="b4d85-108">Tome nota de cadena de conexión de dispositivo de Hola de resultado de hello.</span><span class="sxs-lookup"><span data-stu-id="b4d85-108">Make a note of hello device connection string from hello result.</span></span> <span data-ttu-id="b4d85-109">Esta cadena de conexión de dispositivo se usa por aplicación tooconnect tooyour centro de IoT de hello dispositivo como un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="b4d85-109">This device connection string is used by hello device app tooconnect tooyour IoT Hub as a device.</span></span>

![][img-identity]

<span data-ttu-id="b4d85-110">Consulte demasiado[Introducción a centro de IoT] [ lnk-getstarted] tooprogrammatically crear identidades de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="b4d85-110">Refer too[Getting started with IoT Hub][lnk-getstarted] tooprogrammatically create device identities.</span></span>

<!-- images and links -->
[img-identity]: media/iot-hub-get-started-create-device-identity/devidentity.png

[iot-hub-explorer]: https://github.com/Azure/iothub-explorer/blob/master/readme.md

[lnk-getstarted]: ../articles/iot-hub/iot-hub-csharp-csharp-getstarted.md
