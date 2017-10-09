## <a name="create-an-iot-hub"></a>Crear un centro de IoT
Crear un centro de IoT para su tooconnect de aplicación de dispositivo simulado para. Hello pasos siguientes muestran cómo toocomplete esta tarea al usar Hola portal de Azure.

1. Inicie sesión en toohello [portal de Azure][lnk-portal].
1. Hola Jumpbar, haga clic en **New** > **Internet de las cosas** > **centro de IoT**.
   
    ![Barra de accesos del Portal de Azure][1]
1. Hola **centro de IoT** hoja, elija Configuración de hello para el centro de IoT.
   
    ![Hoja del Centro de IoT][2]
   
   1. Hola **nombre** cuadro, escriba un nombre para el centro de IoT. Si hello **nombre** es válida y está disponible, aparece una marca de verificación verde en hello **nombre** cuadro.
    [!INCLUDE [iot-hub-pii-note-naming-hub](iot-hub-pii-note-naming-hub.md)]
   
   1. Seleccione un [plan de tarifa y escalado][lnk-pricing]. Este tutorial no requiere ningún nivel determinado. Para este tutorial, use el nivel gratuito de F1 de Hola.
   1. En **Grupo de recursos**, cree un grupo de recursos o seleccione uno existente. Para obtener más información, consulte [utilizando recurso agrupa los recursos de Azure de toomanage][lnk-resource-groups].
   1. En **ubicación**, seleccione Hola toohost de ubicación de su centro de IoT. Para este tutorial, elija la ubicación más cercana.
1. Cuando haya elegido las opciones de configuración del Centro de IoT, haga clic en **Crear**.  Puede tardar unos minutos para Azure toocreate su centro de IoT. estado de hello toocheck, puede supervisar el progreso de hello en el panel de inicio de Hola o en el panel de las notificaciones de Hola.
   
    ![Estado del nuevo Centro de IoT][3]
1. Cuando se ha creado correctamente el centro de IoT hello, haga clic en nuevo icono de hello para el centro de IoT en hoja de hello tooopen portal Azure de hello para el nuevo centro de IoT Hola. Tome nota de hello **Hostname**y, a continuación, haga clic en **directivas de acceso compartido**.
   
    ![Nueva hoja del Centro de IoT][4]
1. Hola **directivas de acceso compartido** hoja, haga clic en hello **iothubowner** directiva y, a continuación, copie y tome nota de la cadena de conexión de centro de IoT Hola Hola **iothubowner** hoja. Para obtener más información, consulte [el control de acceso] [ lnk-access-control] Hola "Guía del desarrollador de centro de IoT".
   
    ![Hoja de directivas de acceso compartido][5]

<!-- Images. -->
[1]: ./media/iot-hub-get-started-create-hub/create-iot-hub1.png
[2]: ./media/iot-hub-get-started-create-hub/create-iot-hub2.png
[3]: ./media/iot-hub-get-started-create-hub/create-iot-hub3.png
[4]: ./media/iot-hub-get-started-create-hub/create-iot-hub4.png
[5]: ./media/iot-hub-get-started-create-hub/create-iot-hub5.png

<!-- Links -->
[lnk-resource-groups]: ../articles/azure-resource-manager/resource-group-portal.md
[lnk-portal]: https://portal.azure.com/
[lnk-pricing]: https://azure.microsoft.com/pricing/details/iot-hub/
[lnk-access-control]: ../articles/iot-hub/iot-hub-devguide-security.md
