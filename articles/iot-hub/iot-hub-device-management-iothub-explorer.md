---
title: "aaaAzure administración de dispositivos de IoT con el centro de IOT explorador | Documentos de Microsoft"
description: "Usar Hola el centro de IOT-Explorador de CLI para la administración de dispositivos del centro de IoT de Azure, que ofrece métodos directos de Hola y opciones de administración de propiedades deseadas de hello gemelas."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "administración de dispositivos de azure iot, administración de dispositivos de azure iot hub, iot de administración de dispositivos, administración de dispositivos de iot hub"
ms.assetid: b34f799a-fc14-41b9-bf45-54751163fffe
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/12/2017
ms.author: xshi
ms.openlocfilehash: e0a5e6120db5c4fb12f7f8b605a56e0e4aad9217
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-iothub-explorer-for-azure-iot-hub-device-management"></a>Uso de iothub-explorer para la administración de dispositivos de Azure IoT Hub

![Diagrama integral](media/iot-hub-get-started-e2e-diagram/2.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

[el centro de IOT explorador](https://github.com/azure/iothub-explorer) es una herramienta CLI que se ejecute en un identidades de dispositivos de toomanage de equipo de host en el registro de centro de IoT. Se trata con opciones de administración que se puede usar tooperform de varias tareas.

| Opción de administración          | Tarea                                                                                                                            |
|----------------------------|---------------------------------------------------------------------------------------------------------------------------------|
| Métodos directos             | Hacer que un dispositivo actúan como iniciar o detener el envío de mensajes o reiniciar el dispositivo de Hola.                                        |
| Propiedades deseadas de dispositivos gemelos    | Poner un dispositivo en determinados Estados, por ejemplo, configurar un toogreen LED o configuración de telemetría de hello interval too30 minutos de envío.         |
| Propiedades notificadas de dispositivos gemelos   | Obtener Hola notifica el estado de un dispositivo. Por ejemplo, el dispositivo de Hola informa Hola que LED parpadea ahora.                                    |
| Etiquetas de dispositivos gemelos                  | Almacenar metadatos específicos del dispositivo en la nube de Hola. Por ejemplo, hello ubicación de implementación de una máquina expendedora.                         |
| Mensajes de nube a dispositivo   | Enviar dispositivo tooa de notificaciones. Por ejemplo, "es muy probable que toorain hoy en día. No olvide toobring paraguas."              |
| Consultas de dispositivos gemelos        | Consultar todos los dispositivos: los gemelos tooretrieve las condiciones arbitrario, como identificar los dispositivos de Hola que están disponibles para su uso. |

Para obtener más explicación acerca de las diferencias de hello e instrucciones sobre el uso de estas opciones, consulte [Guía de comunicación de dispositivos a la nube](iot-hub-devguide-d2c-guidance.md) y [orientación para la comunicación en la nube para dispositivos](iot-hub-devguide-c2d-guidance.md).

> [!NOTE]
> Los dispositivos gemelos son documentos JSON que almacenan información sobre el estado de los dispositivos (metadatos, configuraciones y condiciones). Centro de IoT conserva a un gemelas de dispositivo para cada dispositivo que se conecta tooit. Para más información acerca de los dispositivos gemelos, consulte [Introducción a los dispositivos gemelos](iot-hub-node-node-twin-getstarted.md).

## <a name="what-you-learn"></a>Conocimientos que adquirirá

Aprenderá a usar iothub-explorer con distintas opciones de administración en su máquina de desarrollo.

## <a name="what-you-do"></a>Qué debe hacer

Ejecute iothub-explorer con distintas opciones de administración.

## <a name="what-you-need"></a>Lo que necesita

- Tutorial [configurar su dispositivo](iot-hub-raspberry-pi-kit-node-get-started.md) completado donde abordan las Hola según los requisitos:
  - Una suscripción de Azure activa.
  - Un centro de Azure IoT en su suscripción.
  - Una aplicación de cliente que envía el centro de IoT de Azure de tooyour de mensajes.
- Asegúrese de que el dispositivo se está ejecutando con la aplicación de cliente de Hola durante este tutorial.
- iothub-explorer, [instale iothub-explorer](https://github.com/azure/iothub-explorer) en la máquina de desarrollo.

## <a name="connect-tooyour-iot-hub"></a>Conectar el centro de IoT tooyour

Conecte el centro de IoT tooyour mediante la ejecución Hola siguiente comando:

```bash
iothub-explorer login <your IoT hub connection string>
```

## <a name="use-iothub-explorer-with-direct-methods"></a>Uso de iothub-explorer con métodos directos

Invocar hello `start` método en el centro de IoT de hello dispositivo aplicación toosend mensajes tooyour ejecutando Hola siguiente comando:

```bash
iothub-explorer device-method <your device Id> start
```

Invocar hello `stop` método hello dispositivo aplicación toostop enviando mensajes centro de IoT tooyour ejecutando el siguiente comando de hello:

```bash
iothub-explorer device-method <your device Id> stop
```

## <a name="use-iothub-explorer-with-twins-desired-properties"></a>Use iothub-explorer con las propiedades deseadas de los dispositivos gemelos

Establecer un intervalo de la propiedad deseada = 3000 ejecutando Hola siguiente comando:

```bash
iothub-explorer update-twin <your device id> {\"properties\":{\"desired\":{\"interval\":3000}}}
```

El dispositivo puede leer esta propiedad.

## <a name="use-iothub-explorer-with-twins-reported-properties"></a>Use iothub-explorer con las propiedades notificadas de los dispositivos gemelos

Obtengan hello notificadas propiedades de dispositivo de hello ejecutando Hola siguiente comando:

```bash
iothub-explorer get-twin <your device id>
```

Una de las propiedades de hello es $metadata. $lastUpdated que muestra Hola última hora de este dispositivo envía o recibe un mensaje.

## <a name="use-iothub-explorer-with-twins-tags"></a>Uso de iothub-explorer con etiquetas de dispositivos gemelos

Mostrar etiquetas de Hola y las propiedades de dispositivo de Hola ejecutando Hola siguiente comando:

```bash
iothub-explorer get-twin <your device id>
```

Agregar un rol de campo = dispositivo de toohello de temperatura y humedad ejecutando Hola siguiente comando:

```bash
iothub-explorer update-twin <your device id> "{\"tags\":{\"role\":\"temperature&humidity\"}}"

```

## <a name="use-iothub-explorer-with-cloud-to-device-messages"></a>Uso de iothub-explorer con mensajes de la nube al dispositivo

Enviar un dispositivo de toohello de mensaje "¡Hello World" mediante la ejecución de hello siguiente comando:

```bash
iothub-explorer send <device-id> "Hello World"
```

Vea [utilizar el centro de IOT explorador toosend y recibir mensajes entre el dispositivo y el centro de IoT](iot-hub-explorer-cloud-device-messaging.md) para un escenario real del uso de este comando.

## <a name="use-iothub-explorer-with-device-twins-queries"></a>Uso de iothub-explorer con consultas de dispositivos gemelos

Consultar dispositivos con una etiqueta de rol = 'temperatura y humedad' ejecutando Hola siguiente comando:

```bash
iothub-explorer query-twin "SELECT * FROM devices WHERE tags.role = 'temperature&humidity'"
```

Consultar todos los dispositivos excepto los que tienen una etiqueta de rol = 'temperatura y humedad' ejecutando Hola siguiente comando:

```bash
iothub-explorer query-twin "SELECT * FROM devices WHERE tags.role != 'temperature&humidity'"
```

## <a name="next-steps"></a>Pasos siguientes

Ha aprendido cómo toouse el centro de IOT-explorador con distintas opciones de administración.

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
