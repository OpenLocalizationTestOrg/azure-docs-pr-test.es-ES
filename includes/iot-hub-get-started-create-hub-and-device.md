## <a name="create-an-iot-hub"></a>Crear un centro de IoT

1. Hola [portal de Azure](https://portal.azure.com/), haga clic en **New** > **Internet de las cosas** > **centro de IoT**.

   ![Crear un centro de IoT en hello portal de Azure](../articles/iot-hub/media/iot-hub-create-hub-and-device/1_create-azure-iot-hub-portal.png)
2. Hola **centro de IoT** panel, escriba la siguiente información para su centro de IoT de Hola:

     **Nombre**: escriba Hola nombre de su centro de IoT. Si el nombre de Hola que escribió es válida, aparece una marca de verificación verde.

     **Nivel de precios y de escala**: Hola seleccione **F1 - libre** capa. Esta opción es suficiente para esta demostración. Para obtener más información, vea hello [nivel de precios y escala](https://azure.microsoft.com/pricing/details/iot-hub/).

     **Grupo de recursos**: crear un centro de IoT de recursos grupo toohost Hola o utilizar uno existente. Para obtener más información, consulte [grupos de recursos de uso toomanage los recursos de Azure](../articles/azure-resource-manager/resource-group-portal.md).

     **Ubicación**: seleccione Hola más cercano tooyou ubicación donde se crea el centro de IoT Hola.

     **PIN toodashboard**: seleccione esta opción para el centro de IoT tooyour de fácil acceso desde el panel de Hola.

   ![Escriba información toocreate su centro de IoT](../articles/iot-hub/media/iot-hub-create-hub-and-device/2_fill-in-fields-for-azure-iot-hub-portal.png)

   [!INCLUDE [iot-hub-pii-note-naming-hub](iot-hub-pii-note-naming-hub.md)]

3. Haga clic en **Crear**. El centro de IoT podría tardar toocreate unos minutos. Puede ver el progreso en hello **notificaciones** panel.

   ![Ver las notificaciones de progreso para el centro de IoT](../articles/iot-hub/media/iot-hub-create-hub-and-device/3_notification-azure-iot-hub-creation-progress-portal.png)

4. Después de crea el centro de IoT, haga clic en él en el panel de Hola. Tome nota de hello **Hostname**y, a continuación, haga clic en **directivas de acceso compartido**.

   ![Obtener nombre de host de Hola de su centro de IoT](../articles/iot-hub/media/iot-hub-create-hub-and-device/4_get-azure-iot-hub-hostname-portal.png)

5. Hola **directivas de acceso compartido** panel, haga clic en hello **iothubowner** directiva y, a continuación, copia y ha anotado de hello **cadena de conexión** de su centro de IoT. Para obtener más información, consulte [tooIoT de acceso de Control concentrador](../articles/iot-hub/iot-hub-devguide-security.md).

> [!NOTE] 
En este tutorial de configuración, no necesita esta cadena de conexión iothubowner. Sin embargo, puede necesitarlo para algunos de los tutoriales de hello en diferentes escenarios de IoT después de completar esta instalación.

   ![Obtener la cadena de conexión del centro de IoT](../articles/iot-hub/media/iot-hub-create-hub-and-device/5_get-azure-iot-hub-connection-string-portal.png)

## <a name="register-a-device-in-hello-iot-hub-for-your-device"></a>Registrar un dispositivo en el centro de IoT de hello para el dispositivo

1. Hola [portal de Azure](https://portal.azure.com/), abra el centro de IoT.

2. Haga clic en **Explorador de dispositivos**.
3. En el panel del explorador de dispositivo de hello, haga clic en **agregar** tooadd un centro de IoT tooyour de dispositivo. A continuación, Hola siguientes:

   **Id. de dispositivo**: escriba el identificador de Hola de nuevo dispositivo de Hola. Los identificadores de dispositivos distinguen mayúsculas de minúsculas.

   **Tipo de autenticación**: seleccione **Clave simétrica**.

   **Generar claves automáticamente**: active esta casilla de verificación.

   **Conectar dispositivo tooIoT concentrador**: haga clic en **habilitar**.

   ![Agregar un dispositivo en el Explorador de dispositivos de su centro de IoT Hola](../articles/iot-hub/media/iot-hub-create-hub-and-device/6_add-device-in-azure-iot-hub-device-explorer-portal.png)

   [!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

4. Haga clic en **Guardar**.
5. Una vez creado el dispositivo de hello, abrir el dispositivo de Hola Hola **dispositivo explorador** panel.
6. Tome nota de la clave principal de Hola de cadena de conexión de Hola.

   ![Obtener la cadena de conexión de dispositivo de Hola](../articles/iot-hub/media/iot-hub-create-hub-and-device/7_get-device-connection-string-in-device-explorer-portal.png)
