---
title: propiedades gemelas (nodo) del dispositivo de centro de IoT de Azure de aaaUse | Documentos de Microsoft
description: "Cómo los dispositivos del centro de IoT de Azure toouse gemelos tooconfigure dispositivos. Utilice hello Azure IoT SDK para Node.js tooimplement una aplicación de dispositivo simulado y una aplicación de servicio que modifica una configuración de dispositivo mediante un doble de dispositivo."
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: d0bcec50-26e6-40f0-8096-733b2f3071ec
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/13/2016
ms.author: elioda
ms.openlocfilehash: 7ebfe2dfa0876bf04fdbaceae55db76456523e8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-desired-properties-tooconfigure-devices-node"></a>Dispositivos de tooconfigure de propiedades de uso deseado (nodo)
[!INCLUDE [iot-hub-selector-twin-how-to-configure](../../includes/iot-hub-selector-twin-how-to-configure.md)]

Al final de Hola de este tutorial, tendrá dos aplicaciones de consola de Node.js:

* **SimulateDeviceConfiguration.js**, una aplicación de dispositivo simulado que espera una actualización de la configuración deseada e informa del estado de Hola de un proceso de actualización de configuración simulada.
* **SetDesiredConfigurationAndQuery.js**, una aplicación de back-end de Node.js, que establece Hola la configuración en un dispositivo deseado y consultas Hola el proceso de actualización de configuración.

> [!NOTE]
> artículo de Hello [SDK de Azure IoT] [ lnk-hub-sdks] proporciona información acerca de hello Azure IoT SDK que se puede usar toobuild aplicaciones de dispositivo y back-end.
> 
> 

toocomplete este tutorial necesita Hola siguiente:

* Node.js versión 0.10.x, o posteriores.
* Una cuenta de Azure activa. (En caso de no tenerla, puede crear una [cuenta gratuita][lnk-free-trial] en solo unos minutos).

Si ha seguido hello [empezar a trabajar con: los gemelos de dispositivo] [ lnk-twin-tutorial] tutorial, ya tiene un centro de IoT y una identidad de dispositivo llama **myDeviceId**; y puede omitir toohello [ Crear aplicación de dispositivo simulado de hello] [ lnk-how-to-configure-createapp] sección.

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-hello-simulated-device-app"></a>Crear aplicación de dispositivo simulado de hello
En esta sección, creará una aplicación de consola de Node.js que conecta el concentrador de tooyour como **myDeviceId**, espera a que una actualización de la configuración deseada y, a continuación, informa de las actualizaciones en el proceso de actualización de configuración de Hola simulada.

1. Cree una nueva carpeta vacía denominada **simulatedeviceconfiguration**. Hola **simulatedeviceconfiguration** carpeta, cree un nuevo archivo package.json mediante el siguiente comando en el símbolo del sistema de Hola. Acepte todos los valores predeterminados de hello:
   
    ```
    npm init
    ```
2. En el símbolo del sistema en hello **simulatedeviceconfiguration** carpeta, ejecute hello después comando tooinstall hello **dispositivos de iot de azure**, y **azure iot dispositivo-mqtt**paquete:
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. Con un editor de texto, cree un nuevo **SimulateDeviceConfiguration.js** archivo Hola **simulatedeviceconfiguration** carpeta.
4. Agregar Hola después código toohello **SimulateDeviceConfiguration.js** archivo y sustituya hello **{cadena de conexión de dispositivo}** marcador de posición con la cadena de conexión de dispositivo Hola copió cuando se crea hello **myDeviceId** identidad del dispositivo:
   
        'use strict';
        var Client = require('azure-iot-device').Client;
        var Protocol = require('azure-iot-device-mqtt').Mqtt;
   
        var connectionString = '{device connection string}';
        var client = Client.fromConnectionString(connectionString, Protocol);
   
        client.open(function(err) {
            if (err) {
                console.error('could not open IotHub client');
            } else {
                client.getTwin(function(err, twin) {
                    if (err) {
                        console.error('could not get twin');
                    } else {
                        console.log('retrieved device twin');
                        twin.properties.reported.telemetryConfig = {
                            configId: "0",
                            sendFrequency: "24h"
                        }
                        twin.on('properties.desired', function(desiredChange) {
                            console.log("received change: "+JSON.stringify(desiredChange));
                            var currentTelemetryConfig = twin.properties.reported.telemetryConfig;
                            if (desiredChange.telemetryConfig &&desiredChange.telemetryConfig.configId !== currentTelemetryConfig.configId) {
                                initConfigChange(twin);
                            }
                        });
                    }
                });
            }
        });
   
    Hola **cliente** objeto expone métodos toointeract necesarios de hello con: los gemelos de dispositivo del dispositivo de Hola. Hola código anterior, una vez que inicialice hello **cliente** objeto, recupera Hola gemelas de dispositivo para **myDeviceId**y asocia un controlador de actualización de hello en propiedades que desee. controlador de Hello comprueba que hay es una solicitud de cambio de la configuración real mediante la comparación de hello configIds, a continuación, invoca un método que inicia el cambio de configuración de Hola.
   
    Tenga en cuenta que para hello simplificar, código anterior hello usa el valor predeterminado codificado de forma rígida para la configuración inicial de Hola. Una aplicación real probablemente cargaría esa configuración desde un almacenamiento local.
   
   > [!IMPORTANT]
   > Eventos de cambio de propiedad deseada siempre se emiten una vez en la conexión del dispositivo, asegúrese de que toocheck que hay un cambio real en hello las propiedades adecuadas antes de realizar cualquier acción.
   > 
   > 
5. Agregar Hola siguientes métodos antes de hello `client.open()` invocación:
   
        var initConfigChange = function(twin) {
            var currentTelemetryConfig = twin.properties.reported.telemetryConfig;
            currentTelemetryConfig.pendingConfig = twin.properties.desired.telemetryConfig;
            currentTelemetryConfig.status = "Pending";
   
            var patch = {
            telemetryConfig: currentTelemetryConfig
            };
            twin.properties.reported.update(patch, function(err) {
                if (err) {
                    console.log('Could not report properties');
                } else {
                    console.log('Reported pending config change: ' + JSON.stringify(patch));
                    setTimeout(function() {completeConfigChange(twin);}, 60000);
                }
            });
        }
   
        var completeConfigChange =  function(twin) {
            var currentTelemetryConfig = twin.properties.reported.telemetryConfig;
            currentTelemetryConfig.configId = currentTelemetryConfig.pendingConfig.configId;
            currentTelemetryConfig.sendFrequency = currentTelemetryConfig.pendingConfig.sendFrequency;
            currentTelemetryConfig.status = "Success";
            delete currentTelemetryConfig.pendingConfig;
   
            var patch = {
                telemetryConfig: currentTelemetryConfig
            };
            patch.telemetryConfig.pendingConfig = null;
   
            twin.properties.reported.update(patch, function(err) {
                if (err) {
                    console.error('Error reporting properties: ' + err);
                } else {
                    console.log('Reported completed config change: ' + JSON.stringify(patch));
                }
            });
        };
   
    Hola **initConfigChange** método actualiza notifica las propiedades en objeto de gemelas dispositivo local de hello en solicitud de actualización de configuración de Hola y conjuntos de Hola estado demasiado**pendiente**, a continuación, las actualizaciones de Hola dispositivo gemelas en servicio Hola. Después de actualizar correctamente los gemelos de dispositivo de hello, simula un proceso de ejecución prolongada que finaliza en la ejecución de Hola de **completeConfigChange**. Este gemelas de dispositivo local método hello de actualizaciones del notificado propiedades establecer el estado de hello demasiado**correcto** y quitar hello **pendingConfig** objeto. A continuación, actualiza a gemelas de dispositivo de hello en el servicio de Hola.
   
    Tenga en cuenta que, ancho de banda toosave, indica que se actualizan propiedades especificando solo Hola propiedades toobe modificado (denominado **revisión** Hola por encima del código), en lugar de reemplazar todo el documento Hola.
   
   > [!NOTE]
   > Este tutorial no simula ningún comportamiento de las actualizaciones de configuración simultáneas. Algunos procesos de actualización de la configuración podrían ser capaz de tooaccommodate cambios de configuración de destino mientras se ejecuta la actualización de hello, otros podrían tener tooqueue ellos así como otros pudieron rechazar ellos con una condición de error. Asegúrese de tooconsider seguro Hola comportamiento deseado para el proceso de configuración específica y cómo agregar lógica adecuada de hello antes de iniciar el cambio de configuración de Hola.
   > 
   > 
6. Ejecute la aplicación de dispositivo de hello:
   
        node SimulateDeviceConfiguration.js
   
    Debe aparecer un mensaje Hola `retrieved device twin`. Mantenga la aplicación hello ejecutando.

## <a name="create-hello-service-app"></a>Crear aplicación de servicio de hello
En esta sección, aprenderá a crear una aplicación de consola de Node.js ese Hola actualizaciones *deseado propiedades* en hello dispositivo gemelas asociada **myDeviceId** con un nuevo objeto de configuración de telemetría. A continuación, consulta: los gemelos de dispositivo de hello almacenados en el centro de IoT de Hola y muestra diferenciar hello en hello deseado y notifica las configuraciones de dispositivo de Hola.

1. Cree una nueva carpeta vacía denominada **setdesiredandqueryapp**. Hola **setdesiredandqueryapp** carpeta, cree un nuevo archivo package.json mediante el siguiente comando en el símbolo del sistema de Hola. Acepte todos los valores predeterminados de hello:
   
    ```
    npm init
    ```
2. En el símbolo del sistema en hello **setdesiredandqueryapp** carpeta, ejecute hello después comando tooinstall hello **el centro de IOT de azure** paquete:
   
    ```
    npm install azure-iothub node-uuid --save
    ```
3. Con un editor de texto, cree un nuevo **SetDesiredAndQuery.js** archivo Hola **addtagsandqueryapp** carpeta.
4. Agregar Hola después código toohello **SetDesiredAndQuery.js** archivo y sustituya hello **{cadena de conexión de base de datos central de iot}** marcador de posición con hello copió cuando creó el centro de la cadena de conexión de centro de IoT :
   
        'use strict';
        var iothub = require('azure-iothub');
        var uuid = require('node-uuid');
        var connectionString = '{iot hub connection string}';
        var registry = iothub.Registry.fromConnectionString(connectionString);
   
        registry.getTwin('myDeviceId', function(err, twin){
            if (err) {
                console.error(err.constructor.name + ': ' + err.message);
            } else {
                var newConfigId = uuid.v4();
                var newFrequency = process.argv[2] || "5m";
                var patch = {
                    properties: {
                        desired: {
                            telemetryConfig: {
                                configId: newConfigId,
                                sendFrequency: newFrequency
                            }
                        }
                    }
                }
                twin.update(patch, function(err) {
                    if (err) {
                        console.error('Could not update twin: ' + err.constructor.name + ': ' + err.message);
                    } else {
                        console.log(twin.deviceId + ' twin updated successfully');
                    }
                });
                setInterval(queryTwins, 10000);
            }
        });

    Hola **registro** objeto expone métodos toointeract necesarios de hello con: los gemelos de dispositivo del servicio de Hola. Hola código anterior, una vez que inicialice hello **registro** objeto, recupera Hola gemelas de dispositivo para **myDeviceId**y actualiza sus propiedades deseados con un nuevo objeto de configuración de telemetría. Después de esto, llama hello **queryTwins** función eventos 10 segundos.

    > [!IMPORTANT]
    > Esta aplicación consulta IoT Hub cada 10 segundos con fines ilustrativos. Use consultas toogenerate orientadas al usuario informes a través de varios dispositivos y no toodetect cambios. Si la solución requiere notificaciones en tiempo real de eventos de dispositivo, use [notificaciones gemelas][lnk-twin-notifications].
    > 
    >.

1. Agregar Hola después el código justo antes de hello `registry.getDeviceTwin()` Hola de invocación tooimplement **queryTwins** función:
   
        var queryTwins = function() {
            var query = registry.createQuery("SELECT * FROM devices WHERE deviceId = 'myDeviceId'", 100);
            query.nextAsTwin(function(err, results) {
                if (err) {
                    console.error('Failed toofetch hello results: ' + err.message);
                } else {
                    console.log();
                    results.forEach(function(twin) {
                        var desiredConfig = twin.properties.desired.telemetryConfig;
                        var reportedConfig = twin.properties.reported.telemetryConfig;
                        console.log("Config report for: " + twin.deviceId);
                        console.log("Desired: ");
                        console.log(JSON.stringify(desiredConfig, null, 2));
                        console.log("Reported: ");
                        console.log(JSON.stringify(reportedConfig, null, 2));
                    });
                }
            });
        };
   
    consultas de código anteriores Hola Hola: los gemelos de dispositivo almacenados en el centro de IoT de Hola y Hola imprime deseado y notifica las configuraciones de telemetría. Consulte toohello [lenguaje de consultas del centro de IoT] [ lnk-query] toolearn cómo toogenerate enriquecido informes en todos los dispositivos.
2. Con **SimulateDeviceConfiguration.js** , ejecutar la aplicación hello con:
   
        node SetDesiredAndQuery.js 5m
   
    Debería ver Hola notificado configuración cambia de **correcto** demasiado**pendiente** demasiado**correcto** nuevo con activo nuevo Hola enviar frecuencia de cinco minutos en lugar de 24 horas.
   
   > [!IMPORTANT]
   > Hay un retraso de tooa minuto entre la operación de informe de dispositivo de Hola y el resultado de la consulta de Hola. Se trata de tooenable Hola consulta infraestructura toowork a gran escala. tooretrieve vistas coherentes de doble de un único dispositivo usan hello **getDeviceTwin** método Hola **registro** clase.
   > 
   > 

## <a name="next-steps"></a>Pasos siguientes
En este tutorial, establezca una configuración deseada como *deseado propiedades* desde una aplicación back-end y una toodetect de aplicación de dispositivo simulado que cambian y simular un proceso de actualización de varios pasos que se envían informes de su estado como se escribió * notifica propiedades* toohello gemelas de dispositivo.

Hola de uso después cómo toolearn de recursos para:

* enviar telemetría desde dispositivos con hello [empezar a trabajar con el centro de IoT] [ lnk-iothub-getstarted] tutorial,
* programar o realizar operaciones en conjuntos grandes de dispositivos Consulte hello [programación y los trabajos de difusión] [ lnk-schedule-jobs] tutorial.
* controlar los dispositivos de forma interactiva (por ejemplo, al activar un ventilador desde una aplicación controlada por el usuario), con hello [usar métodos directos] [ lnk-methods-tutorial] tutorial.

<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-twin-notifications]: iot-hub-devguide-device-twins.md#back-end-operations
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-dm-overview]: iot-hub-device-management-overview.md
[lnk-twin-tutorial]: iot-hub-node-node-twin-getstarted.md
[lnk-schedule-jobs]: iot-hub-node-node-schedule-jobs.md
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/
[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-iothub-getstarted]: iot-hub-node-node-getstarted.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md

[lnk-guid]: https://en.wikipedia.org/wiki/Globally_unique_identifier

[lnk-how-to-configure-createapp]: iot-hub-node-node-twin-how-to-configure.md#create-the-simulated-device-app
