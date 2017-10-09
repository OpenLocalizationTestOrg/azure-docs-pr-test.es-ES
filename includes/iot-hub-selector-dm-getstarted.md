> [!div class="op_single_selector"]
> * [Dispositivo: Servicio Node.js: Node.js](../articles/iot-hub/iot-hub-node-node-device-management-get-started.md)
> * [Dispositivo: Servicio Node.js: C#](../articles/iot-hub/iot-hub-csharp-node-device-management-get-started.md)
> * [Dispositivo: Servicio de Java: Java](../articles/iot-hub/iot-hub-java-java-device-management-getstarted.md)

Aplicaciones de back-end pueden usar como tipos primitivos de centro de IoT de Azure, [gemelas dispositivo] [ lnk-devtwin] y [dirigir métodos][lnk-c2dmethod], tooremotely iniciar y supervisar acciones de administración de dispositivos en los dispositivos. Este tutorial muestra cómo una aplicación back-end y una aplicación de dispositivo pueden funcionar en conjunto tooinitiate y supervisar un reinicio del dispositivo remoto con el centro de IoT.

Utilice una acciones de administración de dispositivos de tooinitiate método directo (por ejemplo, reiniciar, restablecimiento de fábrica y actualización de firmware) desde una aplicación de back-end en la nube de Hola. dispositivo de Hello es responsable de:

* Control de solicitud del método hello enviado desde el centro de IoT.
* Iniciar acción específico del dispositivo correspondiente de hello en dispositivo Hola.
* Proporcionar actualizaciones de estado a través de *notificado propiedades* tooIoT concentrador.

Puede usar una aplicación de back-end en hello en la nube toorun dispositivo gemelas consultas tooreport en curso de Hola de las acciones de administración de dispositivos.

[lnk-devtwin]: ../articles/iot-hub/iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: ../articles/iot-hub/iot-hub-devguide-direct-methods.md
