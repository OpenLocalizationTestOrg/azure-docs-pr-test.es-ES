## <a name="customize-and-extend-hello-device-management-actions"></a>Personalizar y extender las acciones de administración de dispositivos de Hola

Las soluciones de IoT pueden expandir conjunto definido de Hola de patrones de la administración de dispositivos o habilitar modelos personalizados mediante gemelas de dispositivo de Hola y primitivas de método en la nube al dispositivo. Otros ejemplos de acciones de administración de dispositivos son el restablecimiento de fábrica, la actualización de firmware, la actualización de software, la administración de energía, la administración de conectividad y red, y el cifrado de datos.

## <a name="device-maintenance-windows"></a>Ventanas de mantenimiento del dispositivo

Por lo general, configure las acciones de tooperform de dispositivos a la vez que minimiza las interrupciones y tiempo de inactividad. Ventanas de mantenimiento de dispositivo son una hora de hello toodefine de patrón de uso frecuente cuando un dispositivo debe actualizar su configuración. Las soluciones de back-end pueden usar propiedades de hello deseado de hello dispositivo gemelas toodefine y activar una directiva en el dispositivo que permite una ventana de mantenimiento. Cuando un dispositivo recibe la directiva de ventana de mantenimiento de hello, puede usar Hola notificado propiedad del estado Hola dispositivo gemelas tooreport Hola de directiva de Hola. aplicaciones de back-end de Hello, a continuación, pueden usar dispositivos gemelas consultas tooattest toocompliance de dispositivos y cada directiva.

## <a name="next-steps"></a>Pasos siguientes

En este tutorial, ha utilizado un tootrigger método directo reiniciar el equipo remoto en un dispositivo. Se usa Hola propiedades notificado tooreport Hola reiniciar última hora del dispositivo de Hola y Hola de hello consultado dispositivo gemelas toodiscover reiniciar última hora del dispositivo de Hola de nube de Hola.

toocontinue Introducción a centro de IoT y patrones de la administración de dispositivos como el remoto a través de la actualización de firmware de aire hello, vea:

[Tutorial: Cómo toodo un firmware actualizar][lnk-fwupdate]

toolearn cómo tooextend llama a su método de programación y de solución de IoT en varios dispositivos, vea hello [programación y los trabajos de difusión] [ lnk-tutorial-jobs] tutorial.

toocontinue Introducción a centro de IoT, consulte [introducción con borde IoT][lnk-iot-edge].

[lnk-fwupdate]: ../articles/iot-hub/iot-hub-node-node-firmware-update.md
[lnk-tutorial-jobs]: ../articles/iot-hub/iot-hub-node-node-schedule-jobs.md
[lnk-iot-edge]: ../articles/iot-hub/iot-hub-linux-iot-edge-get-started.md