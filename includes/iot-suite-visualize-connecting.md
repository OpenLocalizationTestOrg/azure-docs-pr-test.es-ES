## <a name="view-device-telemetry-in-hello-dashboard"></a>Vista de telemetría de dispositivo en el panel de Hola
panel de Hola Hola habilita solución telemetría hello tooview tooIoT concentrador de envío de los dispositivos de supervisión remota.

1. En el explorador, el valor devuelto toohello panel de solución supervisión remoto, haga clic en **dispositivos** en hello panel izquierdo toonavigate toohello **lista de dispositivos**.
2. Hola **lista de dispositivos**, debería ver que Hola estado del dispositivo es **ejecutando**. Si no es así, haga clic en **Habilitar dispositivo** en hello **detalles del dispositivo** panel.
   
    ![Ver el estado del dispositivo][18]
3. Haga clic en **panel** tooreturn toohello panel, seleccione el dispositivo en hello **tooView dispositivo** tooview de la lista desplegable la telemetría. Hola la telemetría de aplicación de ejemplo de Hola es 50 unidades de temperatura interna, 55 unidades de temperatura externo y las 50 unidades de humedad.
   
    ![Ver la telemetría de dispositivo][img-telemetry]

## <a name="invoke-a-method-on-your-device"></a>Invocar un método en el dispositivo
panel de Hello en la solución de supervisión remoto hello permite tooinvoke métodos en los dispositivos a través del centro de IoT. Por ejemplo, en hello remoto de solución de supervisión puede invocar un toosimulate método reiniciar un dispositivo.

1. En hello remoto solución panel de supervisión, haga clic en **dispositivos** en hello panel izquierdo toonavigate toohello **lista de dispositivos**.
2. Haga clic en **Id. de dispositivo** para el dispositivo en hello **lista de dispositivos**.
3. Hola **detalles del dispositivo** del panel, haga clic en **métodos**.
   
    ![Métodos de dispositivo][13]
4. Hola **método** lista desplegable, seleccione **InitiateFirmwareUpdate**y, a continuación, en **FWPACKAGEURI** escriba una dirección URL ficticia. Haga clic en **invocar método** toocall método de hello en dispositivo Hola.
   
    ![Invocar un método de dispositivo][14]
   

5. Verá un mensaje en la consola de Hola que se ejecute el código de dispositivo cuando el dispositivo de hello controla método hello. resultados de Hello del método hello se agregan toohello historial en el portal de solución de hello:

    ![Ver el historial de métodos][img-method-history]

## <a name="next-steps"></a>Pasos siguientes
artículo de Hello [personalizar soluciones preconfiguradas] [ lnk-customize] describe algunas maneras puede extender este ejemplo. Entre las posibles extensiones se incluyen el uso de sensores reales y la implementación de comandos adicionales.

Puede aprender más acerca de hello [permisos en el sitio de hello azureiotsuite.com][lnk-permissions].

[13]: ./media/iot-suite-visualize-connecting/suite4.png
[14]: ./media/iot-suite-visualize-connecting/suite7-1.png
[18]: ./media/iot-suite-visualize-connecting/suite10.png
[img-telemetry]: ./media/iot-suite-visualize-connecting/telemetry.png
[img-method-history]: ./media/iot-suite-visualize-connecting/history.png
[lnk-customize]: ../articles/iot-suite/iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-permissions]: ../articles/iot-suite/iot-suite-permissions.md
