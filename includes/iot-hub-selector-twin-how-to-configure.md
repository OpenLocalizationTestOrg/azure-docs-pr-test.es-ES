> [!div class="op_single_selector"]
> * [Node.js](../articles/iot-hub/iot-hub-node-node-twin-how-to-configure.md)
> * [C#/Node.js](../articles/iot-hub/iot-hub-csharp-node-twin-how-to-configure.md)
> * [C#](../articles/iot-hub/iot-hub-csharp-csharp-twin-how-to-configure.md)
> 
> 

## <a name="introduction"></a>Introducción

En [empezar a trabajar con: los gemelos de centro de IoT dispositivo][lnk-twin-tutorial], ha aprendido cómo tooset metadatos del dispositivo de nuevo la solución final utilizar *etiquetas*, informe de las condiciones del dispositivo desde una aplicación de dispositivo usar *notificado propiedades*y consultar esta información utilizando un lenguaje similar a SQL.

En este tutorial, obtendrá información sobre cómo toouse Hola del doble del dispositivo de hello *deseado propiedades* junto con *notificado propiedades*, tooremotely configurar aplicaciones para dispositivos. Más concretamente, este tutorial muestra cómo se notifican un gemelas de dispositivo y propiedades que desee habilitar una configuración de varios pasos de una aplicación de dispositivo y proporcionan Hola visibilidad toohello solución back-end de estado de Hola de esta operación a través de todos los dispositivos. Puede encontrar más información sobre el rol de Hola de configuraciones de dispositivos en [información general de administración de dispositivos con el centro de IoT][lnk-dm-overview].

En un nivel superior, utilizando: los gemelos de dispositivo permite Hola solución back-end toospecify Hola configuración deseada para los dispositivos de hello administrado, en lugar de enviar comandos específicos. Esto coloca el dispositivo de hello responsable de configurar Hola mejor manera tooupdate su configuración (muy importante en escenarios de IoT cuyas condiciones de dispositivo específico afecten a Hola capacidad tooimmediately ejecutar comandos específicos), al notificar continuamente toohello solución volver finalice el estado actual de Hola y posibles condiciones de error del proceso de actualización de Hola. Este patrón es toohello instrumental de administración de grandes conjuntos de dispositivos, puesto que permite Hola solución back-end toohave visibilidad completa del estado de Hola Hola del proceso de configuración en todos los dispositivos.

> [!NOTE]
> En aquellos escenarios en los que los dispositivos se controlen de forma más interactiva (activar un ventilador desde una aplicación controlada por el usuario), considere la posibilidad de usar [métodos directos][lnk-methods].
> 
> 

En este tutorial, cambios de back-end de soluciones de Hola Hola la configuración de telemetría de un dispositivo de destino y, como resultado de que, aplicación de dispositivo de hello sigue un tooapply de proceso en varias fases una configuración de actualización (por ejemplo, que requieren un reinicio del módulo de software, que este tutorial simula con un retraso simple).

Hola solución back-end almacena la configuración de hello en propiedades deseado del doble del dispositivo de Hola Hola siguiente forma:

        {
            ...
            "properties": {
                ...
                "desired": {
                    "telemetryConfig": {
                        "configId": "{id of hello configuration}",
                        "sendFrequency": "{config}"
                    }
                }
                ...
            }
            ...
        }

> [!NOTE]
> Puesto que las configuraciones pueden ser objetos complejos, normalmente se asignan identificadores únicos (hashes o [GUID][lnk-guid]) toosimplify sus comparaciones.
> 
> 

aplicación de dispositivo Hello notifica su configuración actual propiedad Hola deseado de la creación de reflejo **telemetryConfig** Hola notificado propiedades:

        {
            "properties": {
                ...
                "reported": {
                    "telemetryConfig": {
                        "changeId": "{id of hello current configuration}",
                        "sendFrequency": "{current configuration}",
                        "status": "Success",
                    }
                }
                ...
            }
        }

Tenga en cuenta cómo se notifica hello **telemetryConfig** tiene una propiedad adicional **estado**, usa el estado de hello tooreport Hola configuración del proceso de actualización.

Cuando se recibe una nueva configuración deseada, aplicación de dispositivo de hello notifica una configuración pendiente cambiando Hola información:

        {
            "properties": {
                ...
                "reported": {
                    "telemetryConfig": {
                        "changeId": "{id of hello current configuration}",
                        "sendFrequency": "{current configuration}",
                        "status": "Pending",
                        "pendingConfig": {
                            "changeId": "{id of hello pending configuration}",
                            "sendFrequency": "{pending configuration}"
                        }
                    }
                }
                ...
            }
        }

A continuación, en algún momento posterior, aplicación de dispositivo de hello notificará Hola éxito o error de esta operación actualizando Hola por encima de la propiedad.
Tenga en cuenta cómo Hola solución back-end es capaz, en cualquier momento, el estado de hello tooquery Hola del proceso de configuración en todos los dispositivos de Hola.

En este tutorial se muestra cómo realizar las siguientes acciones:

* Crear una aplicación de dispositivo simulado que recibe las actualizaciones de configuración de back-end de hello soluciones e informes de varias actualizaciones como *notificado propiedades* en configuración de hello el proceso de actualización.
* Cree una aplicación de back-end que las actualizaciones de Hola configuración deseada de un dispositivo y, a continuación, las consultas Hola proceso de actualización de configuración.

<!-- links -->

[lnk-methods]: ../articles/iot-hub/iot-hub-devguide-direct-methods.md
[lnk-dm-overview]: ../articles/iot-hub/iot-hub-device-management-overview.md
[lnk-twin-tutorial]: ../articles/iot-hub/iot-hub-node-node-twin-getstarted.md
[lnk-guid]: https://en.wikipedia.org/wiki/Globally_unique_identifier
