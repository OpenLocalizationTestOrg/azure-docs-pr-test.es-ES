---
title: un dispositivo con borde de IoT de Azure (Windows) aaaSimulate | Documentos de Microsoft
description: "¿Cómo toouse borde de IoT de Azure en Windows toocreate un dispositivo simulado que envía telemetría a través de un centro de IoT de tooan de puerta de enlace de borde de IoT de Azure."
services: iot-hub
documentationcenter: 
author: chipalost
manager: timlt
editor: 
ms.assetid: 6a2aeda0-696a-4732-90e1-595d2e2fadc6
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/09/2017
ms.author: andbuc
ms.openlocfilehash: ddbe85eb956e9934e80e2e80e09f77b24cf54856
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-iot-edge-toosend-device-to-cloud-messages-with-a-simulated-device-windows"></a>Usar mensajes de dispositivo a la nube de Azure IoT borde toosend con un dispositivo simulado (Windows)

[!INCLUDE [iot-hub-iot-edge-simulated-selector](../../includes/iot-hub-iot-edge-simulated-selector.md)]

[!INCLUDE [iot-hub-iot-edge-install-build-windows](../../includes/iot-hub-iot-edge-install-build-windows.md)]

## <a name="how-toorun-hello-sample"></a>¿Cómo toorun Hola ejemplo

Hola **build.cmd** script genera su resultado en hello **generar** carpeta de la copia local de hello **iot borde** repositorio. Este resultado incluye cuatro módulos de borde IoT Hola utilizados en este ejemplo.

Hola lugares de la secuencia de comandos de compilación la:

* **Logger.dll** en hello **generar\\módulos\\registrador\\depurar** carpeta.
* **iothub.dll** en hello **generar\\módulos\\el centro de IOT\\depurar** carpeta.
* **identidad\_map.dll** en hello **generar\\módulos\\identitymap\\depurar** carpeta.
* **simulada\_device.dll** en hello **generar\\módulos\\simulada\_dispositivo\\depurar** carpeta.

Usar estas rutas de acceso para hello **ruta de acceso del módulo** valores tal y como se muestra en el siguiente archivo de configuración de JSON de hello:

Hola simulado\_dispositivo\_nube\_cargar\_proceso de ejemplo toma el archivo de configuración de hello ruta de acceso tooa JSON como un argumento de línea de comandos. siguiente archivo JSON de ejemplo Hola se proporciona una en el repositorio SDK de hello en **ejemplos\\simulada\_dispositivo\_nube\_cargar\_ejemplo\\src\\ simulada\_dispositivo\_nube\_cargar\_ejemplo\_win.json**. Este archivo de configuración funciona tal cual a menos que modifique Hola compilar hello de la secuencia de comandos tooplace IoT borde módulos o archivos ejecutables en ubicaciones no predeterminadas de ejemplo.

> [!NOTE]
> las rutas de acceso del módulo hello son el directorio relativa toohello donde simula Hola\_dispositivo\_nube\_cargar\_sample.exe se encuentra. archivo de configuración de JSON de ejemplo de Hola tiene como valor predeterminado toowriting too'deviceCloudUploadGatewaylog.log' en el directorio de trabajo actual.

En un editor de texto, abra el archivo hello **ejemplos\\simulada\_dispositivo\_nube\_cargar\_ejemplo\\src\\simulada\_dispositivo \_nube\_cargar\_win.json** en su copia local de hello **iot borde** repositorio. Este archivo configura los módulos de hello borde IoT de puerta de enlace de ejemplo de Hola:

* Hola **el centro de IOT** módulo conecta el centro de IoT tooyour. Configurar centro de IoT de toosend datos tooyour. En concreto, un conjunto de hello **IoTHubName** toohello nombre de su centro de IoT de valor y establecer hello **IoTHubSuffix** valor demasiado**devices.net azure**. Conjunto hello **transporte** tooone de valor de: **HTTP**, **AMQP**, o **MQTT**. Actualmente, solo **HTTP** comparte una conexión TCP para todos los mensajes de dispositivo. Si establece el valor de hello demasiado**AMQP**, o **MQTT**, puerta de enlace de hello mantiene una tooIoT de conexión TCP concentrador independiente para cada dispositivo.
* Hola **asignación** módulo asigna las direcciones MAC de los identificadores de dispositivo simulado dispositivos tooyour centro de IoT Hola. Asegúrese de que **deviceId** Hola identificadores de coincidencia de valores de hello dos dispositivos agregados que hello y centro de IoT tooyour **deviceKey** valores contienen las claves de Hola de los dos dispositivos.
* Hola **BLE1** y **BLE2** módulos son dispositivos de hello simulada. Tenga en cuenta cómo direcciones MAC de módulo de hello coincidan con las direcciones de Hola Hola **asignación** módulo.
* Hola **registrador** módulo registra el archivo de tooa de actividad de puerta de enlace.
* Hola **ruta de acceso del módulo** valores se muestra en el siguiente ejemplo de Hola son directorio relativa toohello donde simula hello\_dispositivo\_nube\_cargar\_sample.exe se encuentra.
* Hola **vínculos** matriz final Hola de archivo JSON de hello conecta hello **BLE1** y **BLE2** módulos toohello **asignación** hello y módulo **asignación** módulo toohello **el centro de IOT** módulo. También garantiza que todos los mensajes se registran de forma hello **registrador** módulo.

```json
{
    "modules" :
    [
      {
        "name": "IotHub",
        "loader": {
          "name": "native",
          "entrypoint": {
            "module.path": "..\\..\\..\\modules\\iothub\\Debug\\iothub.dll"
          }
          },
          "args": {
            "IoTHubName": "<<insert here IoTHubName>>",
            "IoTHubSuffix": "<<insert here IoTHubSuffix>>",
            "Transport": "HTTP"
          }
        },
      {
        "name": "mapping",
        "loader": {
          "name": "native",
          "entrypoint": {
            "module.path": "..\\..\\..\\modules\\identitymap\\Debug\\identity_map.dll"
          }
          },
          "args": [
            {
              "macAddress": "01:01:01:01:01:01",
              "deviceId": "<<insert here deviceId>>",
              "deviceKey": "<<insert here deviceKey>>"
            },
            {
              "macAddress": "02:02:02:02:02:02",
              "deviceId": "<<insert here deviceId>>",
              "deviceKey": "<<insert here deviceKey>>"
            }
          ]
        },
      {
        "name": "BLE1",
        "loader": {
          "name": "native",
          "entrypoint": {
            "module.path": "..\\..\\..\\modules\\simulated_device\\Debug\\simulated_device.dll"
          }
          },
          "args": {
            "macAddress": "01:01:01:01:01:01"
          }
        },
      {
        "name": "BLE2",
        "loader": {
          "name": "native",
          "entrypoint": {
            "module.path": "..\\..\\..\\modules\\simulated_device\\Debug\\simulated_device.dll"
          }
          },
          "args": {
            "macAddress": "02:02:02:02:02:02"
          }
        },
      {
        "name": "Logger",
        "loader": {
          "name": "native",
          "entrypoint": {
            "module.path": "..\\..\\..\\modules\\logger\\Debug\\logger.dll"
          }
        },
        "args": {
          "filename": "deviceCloudUploadGatewaylog.log"
        }
      }
    ],
    "links" : [
        { "source" : "*", "sink" : "Logger" },
        { "source" : "BLE1", "sink" : "mapping" },
        { "source" : "BLE2", "sink" : "mapping" },
        { "source" : "mapping", "sink" : "IotHub" }
    ]
}
```

Guardar los cambios de hello realiza toohello archivo de configuración.

ejemplo de Hola a toorun:

1. En un símbolo del sistema, navegue toohello **generar** carpeta de la copia local de hello **iot borde** repositorio.
2. Ejecute el siguiente comando de hello:
   
    ```cmd
    samples\simulated_device_cloud_upload\Debug\simulated_device_cloud_upload_sample.exe ..\samples\simulated_device_cloud_upload\src\simulated_device_cloud_upload_win.json
    ```
3. Puede usar hello [explorador del dispositivo] [ lnk-device-explorer] o [el centro de IOT explorador] [ lnk-iothub-explorer] herramienta mensajes de saludo de toomonitor centro de IoT recibe de Hola puerta de enlace. Por ejemplo, mediante el centro de IOT explorador puede supervisar mensajes de dispositivo a la nube mediante el siguiente comando de hello:

    ```cmd
    iothub-explorer monitor-events --login "HostName={Your iot hub name}.azure-devices.net;SharedAccessKeyName=iothubowner;SharedAccessKey={Your IoT Hub key}"
    ```

## <a name="next-steps"></a>Pasos siguientes

toogain conocimientos avanzados de borde de IoT y experimento con algunos ejemplos de código, visite siguiente de hello tutoriales de desarrollador y recursos:

* [Envío de mensajes de un dispositivo físico a la nube con IoT Edge][lnk-physical-device]
* [Azure IoT Edge][lnk-iot-edge]

toofurther explorar las capacidades de Hola de centro de IoT, vea:

* [Guía para desarrolladores de IoT Hub][lnk-devguide]
* [Proteger la solución de IoT de hello masa][lnk-securing]

<!-- Links -->
[lnk-iot-edge]: https://github.com/Azure/iot-edge/
[lnk-physical-device]: iot-hub-iot-edge-physical-device.md
[lnk-devguide]: iot-hub-devguide.md
[lnk-securing]: iot-hub-security-ground-up.md
[lnk-device-explorer]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer
[lnk-iothub-explorer]: https://github.com/Azure/iothub-explorer/blob/master/readme.md