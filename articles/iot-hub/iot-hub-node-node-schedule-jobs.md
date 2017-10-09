---
title: trabajos de aaaSchedule con el centro de IoT de Azure (nodo) | Documentos de Microsoft
description: "¿Cómo tooschedule un centro de IoT de Azure trabajo tooinvoke un método directo en varios dispositivos. Utilice hello Azure IoT SDK para aplicaciones de dispositivos de Node.js tooimplement Hola simulado y un trabajo de Hola de toorun de aplicación de servicio."
services: iot-hub
documentationcenter: .net
author: juanjperez
manager: timlt
editor: 
ms.assetid: 2233356e-b005-4765-ae41-3a4872bda943
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/30/2016
ms.author: juanpere
ms.openlocfilehash: be293362447fbcddaa3433b66f208f22545fe0c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="schedule-and-broadcast-jobs-node"></a>Programación y difusión de trabajos (Node)

[!INCLUDE [iot-hub-selector-schedule-jobs](../../includes/iot-hub-selector-schedule-jobs.md)]

Centro de IoT de Azure es un servicio completamente administrado que permite un toocreate de aplicaciones back-end y los trabajos de seguimiento que el programa y actualización millones de dispositivos.  Los trabajos pueden utilizarse para hello siguientes acciones:

* Actualizar las propiedades deseadas
* Actualizar etiquetas
* Invocar métodos directos

Conceptualmente, un trabajo contiene una de estas acciones y pistas Hola progreso de la ejecución con un conjunto de dispositivos, que se define mediante una consulta de gemelas de dispositivo.  Por ejemplo, una aplicación de back-end puede utilizar un trabajo tooinvoke un método de reinicio en 10.000 dispositivos, especificado por una consulta de gemelas de dispositivo y programada en el futuro.  Esa aplicación, a continuación, puede seguir el progreso de cada uno de los dispositivos de recepción y ejecutar el método de reinicio de Hola.

Más información sobre estas funcionalidades en estos artículos:

* Gemelos de dispositivo y propiedades: [empezar a trabajar con: los gemelos de dispositivo] [ lnk-get-started-twin] y [Tutorial: cómo toouse dispositivo dos propiedades][lnk-twin-props]
* Métodos directos: [Guía del desarrollador de IoT Hub: métodos directos][lnk-dev-methods] y [Tutorial: Uso de métodos directos][lnk-c2d-methods]

En este tutorial se muestra cómo realizar las siguientes acciones:

* Crear una aplicación de dispositivo simulado que tiene un método directo que permite **lockDoor** que puede llamarse mediante Hola solución back-end.
* Crear una aplicación de consola Node.js ese Hola llamadas **lockDoor** método directo en aplicación de dispositivo simulado de hello mediante un Hola de trabajo y las actualizaciones de las propiedades con un trabajo del dispositivo adecuadas.

Al final de Hola de este tutorial, tiene dos aplicaciones de consola de Node.js:

**simDevice.js**, que se conecta el centro de IoT tooyour con la identidad del dispositivo hello y recibe un **lockDoor** método directo.

**scheduleJobService.js**, que llama a un método directo en el dispositivo de Hola de aplicación y la actualización del dispositivo simulado Hola propiedades deseadas de gemelas con un trabajo.

toocomplete este tutorial, necesita Hola siguientes:

* Node.js versión 0.12.x o posteriores. <br/>  [Preparar el entorno de desarrollo] [ lnk-dev-setup] describe cómo tooinstall Node.js para este tutorial en Windows o Linux.
* Una cuenta de Azure activa. (En caso de no tenerla, puede crear una [cuenta gratuita][lnk-free-trial] en solo unos minutos).

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a>Creación de una aplicación de dispositivo simulado
En esta sección, creará una aplicación de consola de Node.js que responde tooa método directo llamado a la nube de hello, lo que desencadena un reinicio del dispositivo simulado y utiliza Hola notificado propiedades tooenable dispositivos gemelas consultas tooidentify dispositivos y cuando reinició por última vez.

1. Cree una nueva carpeta vacía denominada **simDevice**.  Hola **simDevice** carpeta, cree un archivo de package.json mediante Hola siguiente comando en el símbolo del sistema.  Acepte todos los valores predeterminados de hello:
   
    ```
    npm init
    ```
2. En el símbolo del sistema en hello **simDevice** carpeta, ejecute hello después comando tooinstall hello **dispositivos de iot de azure** paquete del SDK de dispositivo y **azure-iot-dispositivo-mqtt** paquete:
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. Con un editor de texto, cree un nuevo **simDevice.js** archivo Hola **simDevice** carpeta.
4. Agregar siguiente hello 'requiere' instrucciones al principio de Hola de hello **simDevice.js** archivo:
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
5. Agregar un **connectionString** variable y utilizar toocreate un **cliente** instancia.  
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId={yourdeviceid};SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```
6. Agregar Hola después Hola de función toohandle **lockDoor** método.
   
    ```
    var onLockDoor = function(request, response) {
   
        // Respond hello cloud app for hello direct method
        response.send(200, function(err) {
            if (!err) {
                console.error('An error occured when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.');
            }
        });
   
        console.log('Locking Door!');
    };
    ```
7. Agregar Hola siguiente controlador de hello tooregister de código de hello **lockDoor** método.
   
    ```
    client.open(function(err) {
        if (err) {
            console.error('Could not connect tooIotHub client.');
        }  else {
            console.log('Client connected tooIoT Hub. Register handler for lockDoor direct method.');
            client.onDeviceMethod('lockDoor', onLockDoor);
        }
    });
    ```
8. Guarde y cierre hello **simDevice.js** archivo.

> [!NOTE]
> tookeep cosas simples, este tutorial no implementa ninguna directiva de reintento. En el código de producción, debe implementar directivas de reintento (por ejemplo, un retroceso exponencial), como se indica en el artículo de MSDN de hello [control de errores transitorios][lnk-transient-faults].
> 
> 

## <a name="schedule-jobs-for-calling-a-direct-method-and-updating-a-device-twins-properties"></a>Programación de trabajos para llamar un método directo y actualización de las propiedades de un dispositivo gemelo
En esta sección, creará una aplicación de consola de Node.js que inicia un equipo remoto **lockDoor** en un dispositivo mediante las propiedades de un directo método y actualización Hola dispositivo gemelas.

1. Cree una nueva carpeta vacía denominada **scheduleJobService**.  Hola **scheduleJobService** carpeta, cree un archivo de package.json mediante Hola siguiente comando en el símbolo del sistema.  Acepte todos los valores predeterminados de hello:
   
    ```
    npm init
    ```
2. En el símbolo del sistema en hello **scheduleJobService** carpeta, ejecute hello después comando tooinstall hello **el centro de IOT de azure** paquete del SDK de dispositivo y **azure iot dispositivo-mqtt**paquete:
   
    ```
    npm install azure-iothub uuid --save
    ```
3. Con un editor de texto, cree un nuevo **scheduleJobService.js** archivo Hola **scheduleJobService** carpeta.
4. Agregar siguiente hello 'requiere' instrucciones al principio de Hola de hello **dmpatterns_gscheduleJobServiceetstarted_service.js** archivo:
   
    ```
    'use strict';
   
    var uuid = require('uuid');
    var JobClient = require('azure-iothub').JobClient;
    ```
5. Agregue Hola siguiendo las declaraciones de variable y reemplace los valores de marcador de posición de hello:
   
    ```
    var connectionString = '{iothubconnectionstring}';
    var queryCondition = "deviceId IN ['myDeviceId']";
    var startTime = new Date();
    var maxExecutionTimeInSeconds =  3600;
    var jobClient = JobClient.fromConnectionString(connectionString);
    ```
6. Agregue Hola después de la función que será usado toomonitor Hola ejecución del trabajo de hello:
   
    ```
    function monitorJob (jobId, callback) {
        var jobMonitorInterval = setInterval(function() {
            jobClient.getJob(jobId, function(err, result) {
            if (err) {
                console.error('Could not get job status: ' + err.message);
            } else {
                console.log('Job: ' + jobId + ' - status: ' + result.status);
                if (result.status === 'completed' || result.status === 'failed' || result.status === 'cancelled') {
                clearInterval(jobMonitorInterval);
                callback(null, result);
                }
            }
            });
        }, 5000);
    }
    ```
7. Agregue Hola siguiendo el trabajo de hello tooschedule de código que llama el método de dispositivo de hello:
   
    ```
    var methodParams = {
        methodName: 'lockDoor',
        payload: null,
        responseTimeoutInSeconds: 15 // Timeout after 15 seconds if device is unable tooprocess method
    };
   
    var methodJobId = uuid.v4();
    console.log('scheduling Device Method job with id: ' + methodJobId);
    jobClient.scheduleDeviceMethod(methodJobId,
                                queryCondition,
                                methodParams,
                                startTime,
                                maxExecutionTimeInSeconds,
                                function(err) {
        if (err) {
            console.error('Could not schedule device method job: ' + err.message);
        } else {
            monitorJob(methodJobId, function(err, result) {
                if (err) {
                    console.error('Could not monitor device method job: ' + err.message);
                } else {
                    console.log(JSON.stringify(result, null, 2));
                }
            });
        }
    });
    ```
8. Agregue Hola después a gemelas de código tooschedule Hola trabajo tooupdate Hola dispositivo:
   
    ```
    var twinPatch = {
        etag: '*',
        desired: {
            building: '43',
            floor: 3
        }
    };
   
    var twinJobId = uuid.v4();
   
    console.log('scheduling Twin Update job with id: ' + twinJobId);
    jobClient.scheduleTwinUpdate(twinJobId,
                                queryCondition,
                                twinPatch,
                                startTime,
                                maxExecutionTimeInSeconds,
                                function(err) {
        if (err) {
            console.error('Could not schedule twin update job: ' + err.message);
        } else {
            monitorJob(twinJobId, function(err, result) {
                if (err) {
                    console.error('Could not monitor twin update job: ' + err.message);
                } else {
                    console.log(JSON.stringify(result, null, 2));
                }
            });
        }
    });
    ```
9. Guarde y cierre hello **scheduleJobService.js** archivo.

## <a name="run-hello-applications"></a>Ejecutar aplicaciones de Hola
Ya estás listo toorun aplicaciones de Hola.

1. En línea de comandos de Hola Hola **simDevice** carpeta, ejecute hello después toobegin comando realizar escuchas de método directo de reinicio de Hola.
   
    ```
    node simDevice.js
    ```
2. En línea de comandos de Hola Hola **scheduleJobService** carpeta, ejecute hello después comando tootrigger Hola trabajos toolock Hola puerta y actualización Hola gemelas
   
    ```
    node scheduleJobService.js
    ```
3. Consulte dispositivo respuesta toohello directo método hello en la consola de Hola.

## <a name="next-steps"></a>Pasos siguientes
En este tutorial, ha utilizado un trabajo tooschedule un dispositivo de tooa método directo y actualización de Hola de las propiedades del doble del dispositivo de Hola.

toocontinue Introducción a centro de IoT y patrones de la administración de dispositivos como el remoto a través de la actualización de firmware de aire hello, vea:

[Tutorial: Cómo toodo un firmware actualizar][lnk-fwupdate]

toocontinue Introducción a centro de IoT, consulte [Introducción a Azure IoT borde][lnk-iot-edge].

[lnk-get-started-twin]: iot-hub-node-node-twin-getstarted.md
[lnk-twin-props]: iot-hub-node-node-twin-how-to-configure.md
[lnk-c2d-methods]: iot-hub-node-node-direct-methods.md
[lnk-dev-methods]: iot-hub-devguide-direct-methods.md
[lnk-fwupdate]: iot-hub-node-node-firmware-update.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
