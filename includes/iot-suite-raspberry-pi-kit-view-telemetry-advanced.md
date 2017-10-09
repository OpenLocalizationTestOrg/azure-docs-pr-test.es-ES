## <a name="view-hello-telemetry"></a>Vista Hola telemetría

Hola frambuesa Pi ahora está enviando la solución de supervisión remota de telemetría toohello. Puede ver la telemetría de hello en el panel de la solución de Hola. También puede enviar mensajes tooyour frambuesa Pi desde el panel de la solución de Hola.

- Vaya a Panel de solución toohello.
- Seleccione el dispositivo en hello **tooView dispositivo** lista desplegable.
- telemetría Hola de hello frambuesa Pi muestra en el panel de Hola.

![Mostrar la telemetría de hello frambuesa Pi][img-telemetry-display]

## <a name="initiate-hello-firmware-update"></a>Iniciar la actualización de firmware de Hola

proceso de actualización de firmware de Hello descarga e instala una versión actualizada de la aplicación de cliente de dispositivo de hello en hello frambuesa Pi. Para obtener más información sobre el proceso de actualización de firmware de hello, consulte Descripción de Hola de patrón de actualización de firmware de hello en [información general de administración de dispositivos con el centro de IoT][lnk-update-pattern].

Iniciar el proceso de actualización de firmware de hello invocando un método en el dispositivo de Hola. Este método es asincrónico y devuelve tan pronto como comienza el proceso de actualización de Hola. Hola dispositivo usa informó de solución de hello toonotify de propiedades sobre el progreso de Hola de actualización de Hola.

Invocar métodos en el instalador de plataforma de frambuesa desde el panel de la solución de Hola. Cuando Hola frambuesa Pi conecta primero toohello solución de supervisión remoto, se enviará información acerca de los métodos de hello es compatible con. 

[img-telemetry-display]: media/iot-suite-raspberry-pi-kit-view-telemetry-advanced/telemetry.png
[lnk-update-pattern]: ../articles/iot-hub/iot-hub-device-management-overview.md
