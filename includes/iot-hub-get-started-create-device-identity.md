## <a name="create-a-device-identity"></a><span data-ttu-id="b8389-101">Creación de una identidad de dispositivo</span><span class="sxs-lookup"><span data-stu-id="b8389-101">Create a device identity</span></span>

<span data-ttu-id="b8389-102">En esta sección, se usa una herramienta de Node.js llamada [iothub-explorer][iot-hub-explorer] para crear una identidad de dispositivo para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="b8389-102">In this section, you use a Node.js tool called [iothub-explorer][iot-hub-explorer] to create a device identity for this tutorial.</span></span> <span data-ttu-id="b8389-103">Los identificadores de dispositivos distinguen mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="b8389-103">Device IDs are case sensitive.</span></span>

1. <span data-ttu-id="b8389-104">En el entorno de línea de comandos, ejecute lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="b8389-104">Run the following in your command-line environment:</span></span>

    `npm install -g iothub-explorer@latest`

1. <span data-ttu-id="b8389-105">Ahora, ejecute el siguiente comando para iniciar sesión en el centro.</span><span class="sxs-lookup"><span data-stu-id="b8389-105">Then, run the following command to login to your hub.</span></span> <span data-ttu-id="b8389-106">Sustituya `{iot hub connection string}` por la cadena de conexión de IoT Hub que copió anteriormente:</span><span class="sxs-lookup"><span data-stu-id="b8389-106">Substitute `{iot hub connection string}` with the IoT Hub connection string you previously copied:</span></span>

    `iothub-explorer login "{iot hub connection string}"`

1. <span data-ttu-id="b8389-107">Por último, cree una nueva identidad de dispositivo llamada `myDeviceId` con el comando:</span><span class="sxs-lookup"><span data-stu-id="b8389-107">Finally, create a new device identity called `myDeviceId` with the command:</span></span>

    `iothub-explorer create myDeviceId --connection-string`

   [!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

<span data-ttu-id="b8389-108">Anote la cadena de conexión de dispositivo del resultado.</span><span class="sxs-lookup"><span data-stu-id="b8389-108">Make a note of the device connection string from the result.</span></span> <span data-ttu-id="b8389-109">La aplicación de dispositivo usa esta cadena de conexión de dispositivo para conectarse a su instancia de IoT Hub como un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="b8389-109">This device connection string is used by the device app to connect to your IoT Hub as a device.</span></span>

![][img-identity]

<span data-ttu-id="b8389-110">Consulte [Introducción a IoT Hub][lnk-getstarted] para crear identidades de dispositivo mediante programación.</span><span class="sxs-lookup"><span data-stu-id="b8389-110">Refer to [Getting started with IoT Hub][lnk-getstarted] to programmatically create device identities.</span></span>

<!-- images and links -->
[img-identity]: media/iot-hub-get-started-create-device-identity/devidentity.png

[iot-hub-explorer]: https://github.com/Azure/iothub-explorer/blob/master/readme.md

[lnk-getstarted]: ../articles/iot-hub/iot-hub-csharp-csharp-getstarted.md
