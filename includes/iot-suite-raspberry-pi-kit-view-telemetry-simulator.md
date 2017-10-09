## <a name="view-hello-telemetry"></a>Vista Hola telemetría

Hola frambuesa Pi ahora está enviando la solución de supervisión remota de telemetría toohello. Puede ver la telemetría de hello en el panel de la solución de Hola. También puede enviar mensajes tooyour frambuesa Pi desde el panel de la solución de Hola.

- Vaya a Panel de solución toohello.
- Seleccione el dispositivo en hello **tooView dispositivo** lista desplegable.
- telemetría Hola de hello frambuesa Pi muestra en el panel de Hola.

![Mostrar la telemetría de hello frambuesa Pi][img-telemetry-display]

## <a name="act-on-hello-device"></a>Actuar en dispositivo Hola

En el panel de la solución de hello, puede invocar métodos en el instalador de plataforma de frambuesa. Cuando Hola frambuesa Pi conecta toohello solución de supervisión remoto, se enviará información acerca de los métodos de hello es compatible con.

- En el panel de la solución de hello, haga clic en **dispositivos** toovisit hello **dispositivos** página. Seleccione el instalador de plataforma de frambuesa Hola **lista de dispositivos**. A continuación, elija **Métodos**:

    ![Lista de dispositivos en el panel][img-list-devices]

- En hello **invocar método** página, elija **LightBlink** en hello **método** lista desplegable.

- Elija **Invocar método**. simulador de Hello imprime un mensaje en la consola de hello en hello frambuesa Pi. aplicación de Hello en hello frambuesa Pi envía un panel de solución de toohello espera de confirmación:

    ![Mostrar el historial de métodos][img-method-history]

- Puede cambiar los LED de Hola activar y desactivar mediante hello **ChangeLightStatus** método con un **LightStatusValue** establecido demasiado**1** para en o **0** para desactivar.

> [!WARNING]
> Si deja Hola supervisión de solución que se ejecuta en su cuenta de Azure remota, se le facturará por vez Hola que se ejecuta. Para obtener más información acerca de cómo reducir el consumo de Hola se ejecuta la solución de supervisión remota, consulte [configurar Azure IoT conjunto preconfigurado soluciones para fines de demostración][lnk-demo-config]. Eliminar soluciones Hola preconfigurado de su cuenta de Azure cuando termine de usarlo.


[img-telemetry-display]: media/iot-suite-raspberry-pi-kit-view-telemetry-simulator/telemetry.png
[img-list-devices]: media/iot-suite-raspberry-pi-kit-view-telemetry-simulator/listdevices.png
[img-method-history]: media/iot-suite-raspberry-pi-kit-view-telemetry-simulator/methodhistory.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md