---
title: "Dispositivo SensorTag y puerta de enlace de Azure IoT: Lección 3: Lectura de mensajes | Microsoft Docs"
description: "Ejecutar código de ejemplo en los mensajes de saludo de tooread de equipo de host desde el centro de IoT."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "datos en la nube hello, recopilación de datos en la nube, servicio de nube de iot, datos de iot"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: cc88be24-b5c0-4ef2-ba21-4e8f77f3e167
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: d3ffbe2e83f9d61c0088b8876a7f0eea62c1fbe1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="read-messages-from-your-iot-hub"></a>Lectura de mensajes en IoT Hub

## <a name="what-you-will-do"></a>Lo que hará

- Ejecutar código de ejemplo en el host de equipo tooread mensajes desde el centro de IoT.

Si tiene problemas, buscar soluciones en hello [página solución de problemas](iot-hub-gateway-kit-c-troubleshooting.md).

## <a name="what-you-will-learn"></a>Lo qué aprenderá

¿Cómo toouse hello gulp mensajes de tooread herramienta desde el centro de IoT.

## <a name="what-you-need"></a>Lo que necesita

- Hola aplicación de ejemplo Bilitar que se ejecutó correctamente en la lección 3.

## <a name="get-your-iot-hub-and-device-connection-strings"></a>Obtención de las cadenas de conexión de IoT Hub y del dispositivo

cadena de conexión de dispositivo de Hello participa en el centro de IoT de dispositivo (SensorTag de TI o dispositivo simulado) tooconnect tooyour. Hola cadena de conexión de base de datos central de IoT es registro, identidad toohello tooconnect usado en los dispositivos de Hola de IoT hub toomanage que se permiten tooconnect tooyour IoT hub.

- Lista de todos los centros de IoT. en el grupo de recursos si ejecuta Hola siguiente comando:

   ```bash
   az iot hub list -g iot-gateway --query [].name
   ```

   Use `iot-gateway` como valor de Hola de `{resource group name}` si no cambia el valor de Hola.
- Obtener la cadena de conexión de base de datos central de hello IoT ejecutando el siguiente comando de hello:

   ```bash
   az iot hub show-connection-string --name {my hub name} -g iot-gateway
   ```

   `{my hub name}`es el nombre de Hola que especificó en la lección 2.

## <a name="configure-hello-device-connection-for-hello-sample-code"></a>Configurar conexión de dispositivo de hello para el código de ejemplo de Hola

Archivo de configuración de dispositivo de actualización hello `config-azure.json` para que pueda leer mensajes desde el centro de IoT en el equipo host. toodo, siga estos pasos:

1. Abra `config-azure.json` en código de Visual Studio mediante la ejecución de hello siguiente comando en una ventana de consola:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-azure.json
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-azure.json
   ```

2. Realizar Hola después reemplazos en hello `config-azure.json` archivo:

   ![captura de pantalla de configuración de azure](media/iot-hub-gateway-kit-lessons/lesson3/config_azure.png)

   Reemplace `[IoT hub connection string]` con hello cadena de conexión de base de datos central de IoT que ha adquirido.

## <a name="read-messages-from-your-iot-hub"></a>Lectura de mensajes en IoT Hub

Si tiene un SensorTag de TI, asegúrese de que ya ha encendido su SensorTag. Ejecutar la aplicación de ejemplo de puerta de enlace de Hola y leer mensajes de centro de IoT por hello siguiente comando:

```bash
gulp run --iot-hub
```

comando de Hello ejecuta Hola Bilitar ejemplo de aplicación que lee y empaqueta los datos de temperatura del dispositivo simulado o SensorTag y envía el centro de IoT de hello mensaje tooyour cada 2 segundos. También genera un mensaje de saludo de tooreceive de proceso secundario.

mensajes de saludo que se envían y reciben son Hola mostrados al instante en todos los mismo ventana en la consola Hola equipo host. instancia de aplicación de ejemplo de Hola se cerrará automáticamente en 40 segundos.

![Aplicación de ejemplo BLE con mensajes enviados y recibidos](media/iot-hub-gateway-kit-lessons/lesson3/gulp_run_read_hub.png)

## <a name="summary"></a>Resumen

Ha ejecutado un tooread de código de ejemplo mensajes desde el centro de IoT. Ya está listo tooread mensajes de saludo que se almacenan en el almacenamiento de tabla de Azure.

## <a name="next-steps"></a>Pasos siguientes
[Creación de una instancia de Azure Function App y una cuenta de Azure Storage](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md)


