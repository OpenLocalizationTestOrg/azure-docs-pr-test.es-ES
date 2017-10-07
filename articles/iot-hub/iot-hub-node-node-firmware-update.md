---
title: "actualización de firmware de aaaDevice con el centro de IoT de Azure (nodo) | Documentos de Microsoft"
description: "Cómo actualizar toouse la administración de dispositivos en el centro de IoT de Azure tooinitiate un firmware del dispositivo. Utilice hello Azure IoT SDK para Node.js tooimplement una aplicación de dispositivo simulado y una aplicación de servicio que desencadena la actualización de firmware de Hola."
services: iot-hub
documentationcenter: .net
author: juanjperez
manager: timlt
editor: 
ms.assetid: 70b84258-bc9f-43b1-b7cf-de1bb715f2cf
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/06/2017
ms.author: juanpere
ms.openlocfilehash: 99d4b369e7aba334bf713e0c657e6e5d227fb691
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-device-management-tooinitiate-a-device-firmware-update-nodenode"></a>Use Administración de dispositivo tooinitiate una actualización de firmware del dispositivo (nodo)
[!INCLUDE [iot-hub-selector-firmware-update](../../includes/iot-hub-selector-firmware-update.md)]

## <a name="introduction"></a>Introducción
Hola [empezar a trabajar con la administración de dispositivos] [ lnk-dm-getstarted] tutorial, ha visto cómo hello toouse [gemelas dispositivo] [ lnk-devtwin] y [directo métodos] [ lnk-c2dmethod] tooremotely primitivas reiniciar un dispositivo. Este tutorial se utiliza Hola mismos tipos primitivos de centro de IoT y proporciona orientación y muestra cómo toodo un extremo a otro simula la actualización de firmware.  Este patrón se utiliza en la implementación de actualización de firmware de Hola de ejemplo de Hola Intel Edison dispositivo.

En este tutorial se muestra cómo realizar las siguientes acciones:

* Crear una aplicación de consola de Node.js que llama a métodos directas de hello firmwareUpdate en aplicación del dispositivo simulado de hello a través de su centro de IoT.
* Cree una aplicación de dispositivo simulado que implemente un método directo **firmwareUpdate**. Este método inicia un proceso de varias fase que espera a que la imagen de firmware de hello toodownload, descarga la imagen de firmware de Hola y por último, se aplica la imagen de firmware Hola. Durante cada fase de actualización de hello, Hola dispositivo usa Hola notifica propiedades tooreport en progreso.

Al final de Hola de este tutorial, tiene dos aplicaciones de consola de Node.js:

**dmpatterns_fwupdate_service.js**, que llama a un método directo en la aplicación de dispositivo simulado de hello, muestra la respuesta de Hola y periódicamente (cada 500 ms) hello muestra actualizado notificado propiedades.

**dmpatterns_fwupdate_device.js**, centro de IoT tooyour que conecta con la identidad del dispositivo Hola creado anteriormente, recibe un método directo firmwareUpdate, se ejecuta a través de un proceso de varios Estados toosimulate un incluidos de actualización de firmware: esperando Hola Descargar imagen, descarga la nueva imagen de hello y, por último, aplicar imagen de Hola.

toocomplete este tutorial, necesita Hola siguientes:

* Node.js versión 0.12.x o posteriores. <br/>  [Preparar el entorno de desarrollo] [ lnk-dev-setup] describe cómo tooinstall Node.js para este tutorial en Windows o Linux.
* Una cuenta de Azure activa. (En caso de no tenerla, puede crear una [cuenta gratuita][lnk-free-trial] en solo unos minutos).

Siga hello [empezar a trabajar con la administración de dispositivos](iot-hub-node-node-device-management-get-started.md) artículo toocreate su centro de IoT y obtener la cadena de conexión de centro de IoT.

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-firmware-update-on-hello-device-using-a-direct-method"></a>Desencadenar una actualización de firmware remoto en dispositivo Hola utilizando un método directo
En esta sección, creará una aplicación de consola de Node.js que inicia una actualización de firmware remota en un dispositivo. aplicación Hello usa una actualización de hello tooinitiate método directo y usa dispositivos gemelas consultas tooperiodically obtener estado de Hola de actualización de firmware active Hola.

1. Cree una carpeta vacía denominada **triggerfwupdateondevice**.  Hola **triggerfwupdateondevice** carpeta, cree un archivo de package.json mediante Hola siguiente comando en el símbolo del sistema.  Acepte todos los valores predeterminados de hello:
   
    ```
    npm init
    ```
2. En el símbolo del sistema en hello **triggerfwupdateondevice** carpeta, ejecute hello después comando tooinstall hello **centro de iot de azure** y **azure-iot-dispositivo-mqtt** dispositivo Paquetes SDK:
   
    ```
    npm install azure-iothub --save
    ```
3. Con un editor de texto, cree un **dmpatterns_getstarted_service.js** archivo Hola **triggerfwupdateondevice** carpeta.
4. Agregar siguiente hello 'requiere' instrucciones al principio de Hola de hello **dmpatterns_getstarted_service.js** archivo:
   
    ```
    'use strict';
   
    var Registry = require('azure-iothub').Registry;
    var Client = require('azure-iothub').Client;
    ```
5. Agregue Hola siguiendo las declaraciones de variable y reemplace los valores de marcador de posición de hello:
   
    ```
    var connectionString = '{device_connectionstring}';
    var registry = Registry.fromConnectionString(connectionString);
    var client = Client.fromConnectionString(connectionString);
    var deviceToUpdate = 'myDeviceId';
    ```
6. Agregar siguiente Hola función toofind y mostrar el valor de Hola de hello firmwareUpdate informa de la propiedad.
   
    ```
    var queryTwinFWUpdateReported = function() {
        registry.getTwin(deviceToUpdate, function(err, twin){
            if (err) {
              console.error('Could not query twins: ' + err.constructor.name + ': ' + err.message);
            } else {
              console.log((JSON.stringify(twin.properties.reported.iothubDM.firmwareUpdate)) + "\n");
            }
        });
    };
    ```
7. Agregue Hola después de la función tooinvoke hello firmwareUpdate método tooreboot Hola dispositivo de destino:
   
    ```
    var startFirmwareUpdateDevice = function() {
      var params = {
          fwPackageUri: 'https://secureurl'
      };
   
      var methodName = "firmwareUpdate";
      var payloadData =  JSON.stringify(params);
   
      var methodParams = {
        methodName: methodName,
        payload: payloadData,
        timeoutInSeconds: 30
      };
   
      client.invokeDeviceMethod(deviceToUpdate, methodParams, function(err, result) {
        if (err) {
          console.error('Could not start hello firmware update on hello device: ' + err.message)
        } 
      });
    };
    ```
8. Por último, siguiente de hello Agregar función secuencia de actualización de firmware de toocode toostart hello y comienzan a mostrarse los periódicamente Hola notificado propiedades:
   
    ```
    startFirmwareUpdateDevice();
    setInterval(queryTwinFWUpdateReported, 500);
    ```
9. Guarde y cierre hello **dmpatterns_fwupdate_service.js** archivo.

[!INCLUDE [iot-hub-device-firmware-update](../../includes/iot-hub-device-firmware-update.md)]

## <a name="run-hello-apps"></a>Ejecutar aplicaciones de Hola
Ya estás listo toorun Hola aplicaciones.

1. En línea de comandos de Hola Hola **manageddevice** carpeta, ejecute hello después toobegin comando realizar escuchas de método directo de reinicio de Hola.
   
    ```
    node dmpatterns_fwupdate_device.js
    ```
2. En línea de comandos de Hola Hola **triggerfwupdateondevice** carpeta, ejecute hello después comando tootrigger Hola remoto de reinicio y de consulta de Hola de hello dispositivo gemelas toofind reiniciar última hora.
   
    ```
    node dmpatterns_fwupdate_service.js
    ```
3. Consulte dispositivo respuesta toohello directo método hello en la consola de Hola.

## <a name="next-steps"></a>Pasos siguientes
En este tutorial, ha utilizado un tootrigger método directo un control remoto actualización de firmware en un dispositivo y Hola usado informó sobre el progreso de hello toofollow de propiedades de actualización de firmware de Hola.

toolearn cómo tooextend llama a su método de programación y de solución de IoT en varios dispositivos, vea hello [programación y los trabajos de difusión] [ lnk-tutorial-jobs] tutorial.

[lnk-devtwin]: iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: iot-hub-devguide-direct-methods.md
[lnk-dm-getstarted]: iot-hub-node-node-device-management-get-started.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
