## <a name="create-a-device-identity"></a>Creación de una identidad de dispositivo

En esta sección, utilice hello [portal de Azure] [ lnk-azure-portal] toocreate una identidad de dispositivo en el registro de la identidad de hello en el centro de IoT. Un dispositivo no puede conectar tooIoT concentrador a menos que tenga una entrada en el registro de la identidad de Hola. Para obtener más información, vea la sección de "Registro de identidad" de Hola de hello [Guía del desarrollador de centro de IoT][lnk-devguide-identity]. Hola **dispositivo explorador** de hello portal le ayudará a generar un identificador de dispositivo único y una clave que el dispositivo pueda usar tooidentify sí mismo cuando se conecta tooIoT concentrador. Los identificadores de dispositivos distinguen mayúsculas de minúsculas.

1. Asegúrese de que ha iniciado sesión toohello [portal de Azure][lnk-azure-portal].

1. Hola Jumpbar, haga clic en **todos los recursos** y se encuentra el recurso de centro de IoT.

    ![Navegar por el centro de Iot tooyour][img-find-iothub]

1. Cuando se abre el recurso de centro de IoT, haga clic en hello **dispositivo explorador** de herramientas y, a continuación, haga clic en **agregar** en la parte superior de Hola. Proporcione el nombre de hello para el nuevo dispositivo, como **myDeviceId**y haga clic en **guardar**.

    ![Creación de la identidad del dispositivo en el portal][img-create-device]

   Se crea una nueva identidad de dispositivo para su instancia de IoT Hub.

   [!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

1. Hola **dispositivo explorador**de lista de dispositivos, haga clic en el dispositivo de hello recién creado y tome nota de hello **cadena de conexión---clave principal**. 

    ![Cadena de conexión de dispositivo][img-connection-string]

> [!NOTE]
> Hola del registro de identidad de centro de IoT solo almacena centro de IoT toohello de dispositivo identidades tooenable un acceso seguro. Toouse de identificadores y las claves de dispositivo almacena como credenciales de seguridad y una marca de habilitado/deshabilitado que puede usar acceso toodisable para un dispositivo individual. Si la aplicación necesita toostore otros metadatos específicos del dispositivo, debe usar un almacén específico de la aplicación. Consulte la [guía para desarrolladores de IoT Hub][lnk-devguide-identity] para más información.

<!-- Images. -->
[img-find-iothub]: ./media/iot-hub-get-started-create-device-identity-portal/find-iothub.png
[img-create-device]: ./media/iot-hub-get-started-create-device-identity-portal/create-identity-portal.png
[img-connection-string]: ./media/iot-hub-get-started-create-device-identity-portal/device-connection-string.png


<!-- Links -->
[lnk-azure-portal]: https://portal.azure.com
[lnk-devguide-identity]: ../articles/iot-hub/iot-hub-devguide-identity-registry.md

