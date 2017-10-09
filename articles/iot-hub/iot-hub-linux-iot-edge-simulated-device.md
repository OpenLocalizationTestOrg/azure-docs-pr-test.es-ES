---
title: aaaSimulate un dispositivo con borde de IoT de Azure (Linux) | Documentos de Microsoft
description: "Cómo toouse borde de IoT de Azure en Linux toocreate un dispositivo simulado que envía telemetría a través de un borde de IoT centro de IoT tooan de puerta de enlace."
services: iot-hub
documentationcenter: 
author: chipalost
manager: timlt
editor: 
ms.assetid: 11e7bf28-ee3d-48d6-a386-eb506c7a31cf
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/09/2017
ms.author: andbuc
ms.openlocfilehash: 168fb8eda8671d02c63073bdf36dfcd88b397fe2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-iot-edge-toosend-device-to-cloud-messages-with-a-simulated-device-linux"></a>Usar mensajes de dispositivo a la nube de Azure IoT borde toosend con un dispositivo simulado (Linux)

[!INCLUDE [iot-hub-iot-edge-simulated-selector](../../includes/iot-hub-iot-edge-simulated-selector.md)]

[!INCLUDE [iot-hub-iot-edge-install-build-linux](../../includes/iot-hub-iot-edge-install-build-linux.md)]

## <a name="how-toorun-hello-sample"></a>¿Cómo toorun Hola ejemplo

Hola **build.sh** script genera su resultado en hello **generar** carpeta de la copia local de hello **iot borde** repositorio. Este resultado incluye cuatro módulos de borde IoT Hola utilizados en este ejemplo.

Hola lugares de la secuencia de comandos de compilación la:

* **liblogger.SO** en hello **compilación/módulos/registrador** carpeta.
* **libiothub.SO** en hello **compilación/módulos/el centro de IOT** carpeta.
* **lib\_identidad\_map.so** en hello **compilación/módulos/identitymap** carpeta.
* **libsimulated\_device.so** en hello **compilación/módulos/simuladas\_dispositivo** carpeta.

Usar estas rutas de acceso para hello **ruta de acceso del módulo** valores tal y como se muestra en el siguiente archivo de configuración de JSON de hello:

Hola simulado\_dispositivo\_nube\_cargar\_proceso de ejemplo toma el archivo de configuración de hello ruta de acceso tooa JSON como un argumento de línea de comandos. siguiente archivo JSON de ejemplo Hola se proporciona una en el repositorio SDK de hello en **ejemplos\\simulada\_dispositivo\_nube\_cargar\_ejemplo\\src\\ simulada\_dispositivo\_nube\_cargar\_ejemplo\_lin.json**. Este archivo de configuración funciona tal cual a menos que modifique Hola compilar hello de la secuencia de comandos tooplace IoT borde módulos o archivos ejecutables en ubicaciones no predeterminadas de ejemplo.

> [!NOTE]
> las rutas de acceso del módulo de Hello son toohello relativa directorio desde donde se ejecuta Hola simulado\_dispositivo\_nube\_cargar\_ejecutable de ejemplo, no es directorio Hola donde se encuentra el ejecutable de Hola. archivo de configuración de JSON de ejemplo de Hola tiene como valor predeterminado toowriting too'deviceCloudUploadGatewaylog.log' en el directorio de trabajo actual.

En un editor de texto, abra el archivo hello **ejemplos/simuladas\_dispositivo\_nube\_cargar\_ejemplo/src/simuladas\_dispositivo\_nube\_cargar\_lin.json** en su copia local de hello **iot borde** repositorio. Este archivo configura los módulos de hello borde IoT de puerta de enlace de ejemplo de Hola:

* Hola **el centro de IOT** módulo conecta el centro de IoT tooyour. Configurar centro de IoT de toosend datos tooyour. En concreto, un conjunto de hello **IoTHubName** toohello nombre de su centro de IoT de valor y establecer hello **IoTHubSuffix** valor demasiado**devices.net azure**. Conjunto hello **transporte** tooone de valor de: **HTTP**, **AMQP**, o **MQTT**. Actualmente, solo **HTTP** comparte una conexión TCP para todos los mensajes de dispositivo. Si establece el valor de hello demasiado**AMQP**, o **MQTT**, puerta de enlace de hello mantiene una tooIoT de conexión TCP concentrador independiente para cada dispositivo.
* Hola **asignación** módulo asigna las direcciones MAC de los identificadores de dispositivo simulado dispositivos tooyour centro de IoT Hola. Asegúrese de que **deviceId** Hola identificadores de coincidencia de valores de hello dos dispositivos agregados que hello y centro de IoT tooyour **deviceKey** valores contienen las claves de Hola de los dos dispositivos.
* Hola **BLE1** y **BLE2** módulos son dispositivos de hello simulada. Tenga en cuenta cómo su MAC aborda coincidencia Hola direcciones en hello **asignación** módulo.
* Hola **registrador** módulo registra el archivo de tooa de actividad de puerta de enlace.
* Hola **ruta de acceso del módulo** valores que se muestran en el ejemplo de Hola supongamos que ejecuta el ejemplo de Hola de hello **generar** carpeta de la copia local de hello **iot borde** repositorio.
* Hola **vínculos** matriz final Hola de archivo JSON de hello conecta hello **BLE1** y **BLE2** módulos toohello **asignación** hello y módulo **asignación** módulo toohello **el centro de IOT** módulo. También garantiza que todos los mensajes se registran de forma hello **registrador** módulo.

```json
{
    "modules": [
        {
            "name": "IotHub",
          "loader": {
            "name": "native",
            "entrypoint": {
              "module.path": "./modules/iothub/libiothub.so"
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
              "module.path": "./modules/identitymap/libidentity_map.so"
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
              "module.path": "./modules/simulated_device/libsimulated_device.so"
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
              "module.path": "./modules/simulated_device/libsimulated_device.so"
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
              "module.path": "./modules/logger/liblogger.so"
            }
            },
            "args": {
              "filename": "deviceCloudUploadGatewaylog.log"
            }
          }
    ],
    "links": [
        {
            "source": "*",
            "sink": "Logger"
        },
        {
            "source": "BLE1",
            "sink": "mapping"
        },
        {
            "source": "BLE2",
            "sink": "mapping"
        },
        {
            "source": "mapping",
            "sink": "IotHub"
        }
    ]
}
```

Guardar los cambios de hello realiza toohello archivo de configuración.

ejemplo de Hola a toorun:

1. En el shell, navegue toohello **iot-borde/compilación** carpeta.
2. Ejecute el siguiente comando de hello:
   
    ```sh
    ./samples/simulated_device_cloud_upload/simulated_device_cloud_upload_sample ../samples/simulated_device_cloud_upload/src/simulated_device_cloud_upload_lin.json
    ```
3. Puede usar hello [explorador del dispositivo] [ lnk-device-explorer] o [el centro de IOT explorador] [ lnk-iothub-explorer] herramienta mensajes de saludo de toomonitor centro de IoT recibe de Hola puerta de enlace. Por ejemplo, mediante el centro de IOT explorador puede supervisar mensajes de dispositivo a la nube mediante el siguiente comando de hello:

    ```sh
    iothub-explorer monitor-events --login "HostName={Your iot hub name}.azure-devices.net;SharedAccessKeyName=iothubowner;SharedAccessKey={Your IoT Hub key}"
    ```

## <a name="next-steps"></a>Pasos siguientes

toogain conocimientos avanzados de borde de IoT de Azure y experimento con algunos ejemplos de código, visite siguiente de hello tutoriales de desarrollador y recursos:

* [Envío de mensajes de un dispositivo físico a la nube con Azure IoT Edge][lnk-physical-device]
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
