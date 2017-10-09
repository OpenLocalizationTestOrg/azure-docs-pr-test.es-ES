---
title: "aaaGet partió gemelos de dispositivo del centro de IoT de Azure (nodo) | Documentos de Microsoft"
description: "¿Cómo toouse centro de IoT de Azure dispositivo: los gemelos tooadd etiquetas y, a continuación, utilice una consulta de centro de IoT. Utilice hello Azure IoT SDK para Node.js tooimplement Hola simulada del dispositivo y una aplicación de servicio que agrega las etiquetas de Hola y ejecuta Hola consultas del centro de IoT."
services: iot-hub
documentationcenter: node
author: fsautomata
manager: timlt
editor: 
ms.assetid: 314c88e4-cce1-441c-b75a-d2e08e39ae7d
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: elioda
ms.openlocfilehash: d60b8c3de85e9285e496b86e27d4ee31a0554a1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-device-twins-node"></a>Introducción a los dispositivos gemelos (Node)
[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

Al final de Hola de este tutorial, tendrá dos aplicaciones de consola de Node.js:

* **AddTagsAndQuery.js**, una aplicación Node.js de back-end diseñada para ejecutarse desde el back-end, que agrega etiquetas y consulta dispositivos gemelos.
* **TwinSimulatedDevice.js**, una aplicación Node.js que simula un dispositivo que conecta el centro de IoT tooyour con la identidad del dispositivo Hola creado anteriormente e informa acerca de su condición de conectividad.

> [!NOTE]
> artículo de Hello [SDK de Azure IoT] [ lnk-hub-sdks] proporciona información acerca de hello Azure IoT SDK que se puede usar toobuild aplicaciones de dispositivo y back-end.
> 
> 

toocomplete este tutorial necesita Hola siguiente:

* Node.js versión 0.10.x, o posteriores.
* Una cuenta de Azure activa. (En caso de no tenerla, puede crear una [cuenta gratuita][lnk-free-trial] en solo unos minutos).

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-hello-service-app"></a>Crear aplicación de servicio de hello
En esta sección, creará una aplicación de consola de Node.js que agrega gemelas de dispositivo de toohello ubicación metadatos asociados a **myDeviceId**. A continuación, consulta: los gemelos de hello dispositivo almacenan en Centro de IoT Hola seleccionar dispositivos de hello ubicados en hello nos y, a continuación, Hola que dependen de una conexión de telefonía móvil.

1. Cree una nueva carpeta vacía denominada **addtagsandqueryapp**. Hola **addtagsandqueryapp** carpeta, cree un nuevo archivo package.json mediante el siguiente comando en el símbolo del sistema de Hola. Acepte todos los valores predeterminados de hello:
   
    ```
    npm init
    ```
2. En el símbolo del sistema en hello **addtagsandqueryapp** carpeta, ejecute hello después comando tooinstall hello **el centro de IOT de azure** paquete:
   
    ```
    npm install azure-iothub --save
    ```
3. Con un editor de texto, cree un nuevo **AddTagsAndQuery.js** archivo Hola **addtagsandqueryapp** carpeta.
4. Agregar Hola después código toohello **AddTagsAndQuery.js** archivo y sustituya hello **{cadena de conexión de base de datos central de iot}** marcador de posición con hello copió cuando creó el centro de la cadena de conexión de centro de IoT:
   
        'use strict';
        var iothub = require('azure-iothub');
        var connectionString = '{iot hub connection string}';
        var registry = iothub.Registry.fromConnectionString(connectionString);
   
        registry.getTwin('myDeviceId', function(err, twin){
            if (err) {
                console.error(err.constructor.name + ': ' + err.message);
            } else {
                var patch = {
                    tags: {
                        location: {
                            region: 'US',
                            plant: 'Redmond43'
                      }
                    }
                };
   
                twin.update(patch, function(err) {
                  if (err) {
                    console.error('Could not update twin: ' + err.constructor.name + ': ' + err.message);
                  } else {
                    console.log(twin.deviceId + ' twin updated successfully');
                    queryTwins();
                  }
                });
            }
        });
   
    Hola **registro** objeto expone métodos toointeract necesarios de hello con: los gemelos de dispositivo del servicio de Hola. código anterior Hola inicializa por primera vez hello **registro** objeto, a continuación, recupera Hola gemelas de dispositivo para **myDeviceId**y por último actualiza sus etiquetas con información de ubicación de hello deseado.
   
    Después de hello actualizar Hola etiquetas Hola llamadas **queryTwins** (función).
5. Agregar Hola siguiente código al final de Hola de **AddTagsAndQuery.js** tooimplement hello **queryTwins** función:
   
        var queryTwins = function() {
            var query = registry.createQuery("SELECT * FROM devices WHERE tags.location.plant = 'Redmond43'", 100);
            query.nextAsTwin(function(err, results) {
                if (err) {
                    console.error('Failed toofetch hello results: ' + err.message);
                } else {
                    console.log("Devices in Redmond43: " + results.map(function(twin) {return twin.deviceId}).join(','));
                }
            });
   
            query = registry.createQuery("SELECT * FROM devices WHERE tags.location.plant = 'Redmond43' AND properties.reported.connectivity.type = 'cellular'", 100);
            query.nextAsTwin(function(err, results) {
                if (err) {
                    console.error('Failed toofetch hello results: ' + err.message);
                } else {
                    console.log("Devices in Redmond43 using cellular network: " + results.map(function(twin) {return twin.deviceId}).join(','));
                }
            });
        };
   
    código de Hello anterior ejecuta dos consultas: Hola primero selecciona solo Hola dispositivo: los gemelos de dispositivos que se encuentran en hello **Redmond43** planta Hola segundo perfecciona Hola consulta tooselect solo Hola dispositivos y que también están conectados a través de red de telefonía móvil.
   
    Tenga en cuenta ese código Hola anterior, cuando crea hello **consulta** de objetos, especifica un número máximo de documentos devueltos. Hola **consulta** objeto contiene un **hasMoreResults** propiedad booleana que se puede usar hello tooinvoke **nextAsTwin** métodos varias veces tooretrieve todos los resultados. Un método llamado **siguiente** está disponible para los resultados que no son dispositivos gemelos, por ejemplo, los resultados de consultas de agregación.
6. Ejecutar la aplicación hello con:
   
        node AddTagsAndQuery.js
   
    Debería ver un dispositivo en los resultados de Hola para hello formular de consulta para todos los dispositivos ubicados en **Redmond43** y ninguno para consulta de Hola que restringe Hola resultados toodevices que usan una red móvil.
   
    ![][1]

En la sección siguiente Hola crear una aplicación de dispositivo que contiene información de conectividad de Hola y cambios Hola resultado de consulta de hello en la sección anterior de Hola.

## <a name="create-hello-device-app"></a>Crear aplicación de dispositivo de hello
En esta sección, creará una aplicación de consola de Node.js que conecta el concentrador de tooyour como **myDeviceId**y, a continuación, las actualizaciones de su gemelas de dispositivo del notificado información de Hola de toocontain de propiedades que está conectado mediante una red de telefonía móvil.

> [!NOTE]
> En este momento, son accesibles únicamente desde dispositivos que se conectan tooIoT concentrador: los gemelos de dispositivo mediante el protocolo MQTT Hola. Consulte toohello [compatibilidad MQTT] [ lnk-devguide-mqtt] artículo para obtener instrucciones sobre cómo toouse de aplicación de dispositivo existente de tooconvert MQTT.
> 
> 

1. Cree una nueva carpeta vacía denominada **reportconnectivity**. Hola **reportconnectivity** carpeta, cree un nuevo archivo package.json mediante el siguiente comando en el símbolo del sistema de Hola. Acepte todos los valores predeterminados de hello:
   
    ```
    npm init
    ```
2. En el símbolo del sistema en hello **reportconnectivity** carpeta, ejecute hello después comando tooinstall hello **dispositivos de iot de azure**, y **azure-iot-dispositivo-mqtt** paquete :
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. Con un editor de texto, cree un nuevo **ReportConnectivity.js** archivo Hola **reportconnectivity** carpeta.
4. Agregar Hola después código toohello **ReportConnectivity.js** archivo y sustituya hello **{cadena de conexión de dispositivo}** marcador de posición con la cadena de conexión de dispositivo de Hola que copió al crear Hola **myDeviceId** identidad del dispositivo:
   
        'use strict';
        var Client = require('azure-iot-device').Client;
        var Protocol = require('azure-iot-device-mqtt').Mqtt;
   
        var connectionString = '{device connection string}';
        var client = Client.fromConnectionString(connectionString, Protocol);
   
        client.open(function(err) {
        if (err) {
            console.error('could not open IotHub client');
        }  else {
            console.log('client opened');
   
            client.getTwin(function(err, twin) {
            if (err) {
                console.error('could not get twin');
            } else {
                var patch = {
                    connectivity: {
                        type: 'cellular'
                    }
                };
   
                twin.properties.reported.update(patch, function(err) {
                    if (err) {
                        console.error('could not update twin');
                    } else {
                        console.log('twin state reported');
                        process.exit();
                    }
                });
            }
            });
        }
        });
   
    Hola **cliente** objeto expone todos los métodos de hello requieren toointeract con: los gemelos de dispositivo del dispositivo de Hola. Hola código anterior, una vez que inicialice hello **cliente** objeto, recupera Hola gemelas de dispositivo para **myDeviceId** y actualiza su propiedad incluido con información de conectividad de Hola.
5. Ejecutar la aplicación de dispositivo de hello
   
        node ReportConnectivity.js
   
    Debe aparecer un mensaje Hola `twin state reported`.
6. Ahora que hello dispositivo había notificado su información de conectividad, debe aparecer en las dos consultas. Vaya en hello **addtagsandqueryapp** Hola de carpeta y ejecutar las consultas de nuevo:
   
        node AddTagsAndQuery.js
   
    Esta vez **myDeviceId** debe aparecer en los resultados de ambas consulta.
   
    ![][3]

## <a name="next-steps"></a>Pasos siguientes
En este tutorial, configura un nuevo centro de IoT Hola portal de Azure y, a continuación, crea una identidad de dispositivo en el registro de identidad del centro de IoT Hola. Agrega los metadatos del dispositivo como etiquetas desde una aplicación de back-end y una información de conectividad del dispositivo de tooreport de aplicación de dispositivo simulado se escribió en gemelas de dispositivo de Hola. También habrá aprendido cómo tooquery esta información mediante el lenguaje de consulta de hello centro de IoT similar a SQL.

Hola de uso después cómo toolearn de recursos para:

* enviar telemetría desde dispositivos con hello [empezar a trabajar con el centro de IoT] [ lnk-iothub-getstarted] tutorial,
* configurar dispositivos mediante propiedades que desee del doble del dispositivo con hello [uso deseado propiedades de dispositivos con tooconfigure] [ lnk-twin-how-to-configure] tutorial,
* controlar los dispositivos de forma interactiva (por ejemplo, al activar un ventilador desde una aplicación controlada por el usuario), con hello [usar métodos directos] [ lnk-methods-tutorial] tutorial.

<!-- images -->
[1]: media/iot-hub-node-node-twin-getstarted/service1.png
[3]: media/iot-hub-node-node-twin-getstarted/service2.png

<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[lnk-d2c]: iot-hub-devguide-messaging.md#device-to-cloud-messages
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-identity]: iot-hub-devguide-identity-registry.md

[lnk-iothub-getstarted]: iot-hub-node-node-getstarted.md
[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/

[lnk-twin-how-to-configure]: iot-hub-node-node-twin-how-to-configure.md
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md

[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
