## <a name="create-a-device-identity"></a>Creación de una identidad de dispositivo

En esta sección, utilice una herramienta de Node.js denominada [el centro de IOT explorador] [ iot-hub-explorer] toocreate una identidad de dispositivo para este tutorial. Los identificadores de dispositivos distinguen mayúsculas de minúsculas.

1. Ejecute hello siguiente en su entorno de línea de comandos:

    `npm install -g iothub-explorer@latest`

1. A continuación, ejecute hello después de concentrador de comando toologin tooyour. SUBSTITUTE `{iot hub connection string}` con hello cadena de conexión de centro de IoT copió anteriormente:

    `iothub-explorer login "{iot hub connection string}"`

1. Por último, cree una nueva identidad de dispositivo llama `myDeviceId` con el comando hello:

    `iothub-explorer create myDeviceId --connection-string`

   [!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

Tome nota de cadena de conexión de dispositivo de Hola de resultado de hello. Esta cadena de conexión de dispositivo se usa por aplicación tooconnect tooyour centro de IoT de hello dispositivo como un dispositivo.

![][img-identity]

Consulte demasiado[Introducción a centro de IoT] [ lnk-getstarted] tooprogrammatically crear identidades de dispositivos.

<!-- images and links -->
[img-identity]: media/iot-hub-get-started-create-device-identity/devidentity.png

[iot-hub-explorer]: https://github.com/Azure/iothub-explorer/blob/master/readme.md

[lnk-getstarted]: ../articles/iot-hub/iot-hub-csharp-csharp-getstarted.md
