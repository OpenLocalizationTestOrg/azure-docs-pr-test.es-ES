---
title: "Dispositivo simulado y puerta de enlace de Azure IoT: Lección 3: Lectura de mensajes | Microsoft Docs"
description: "Ejecutar código de ejemplo en los mensajes de saludo de tooread de equipo de host desde el centro de IoT."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "datos en la nube hello, recopilación de datos en la nube, servicio de nube de iot, datos de iot"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 5a6ec9c1-d83c-41c1-beaf-7c0d3395d77f
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 540575724bb5cdac4db581a226d8a02a59004d8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="read-messages-from-your-iot-hub"></a>Lectura de mensajes en IoT Hub

## <a name="what-you-will-do"></a>Lo que hará

- Ejecutar código de ejemplo en el host de equipo tooread mensajes desde el centro de IoT.

Si tiene problemas, buscar soluciones en hello [página solución de problemas](iot-hub-gateway-kit-c-sim-troubleshooting.md).

## <a name="what-you-will-learn"></a>Lo qué aprenderá

¿Cómo toouse hello gulp mensajes de tooread herramienta desde el centro de IoT.

## <a name="what-you-need"></a>Lo que necesita

- ejemplo de Hola a dispositivo simulado en [configurar y ejecutar una nube del dispositivo simulado cargar la aplicación de ejemplo](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md).

## <a name="get-your-iot-hub-and-device-connection-strings"></a>Obtención de las cadenas de conexión de IoT Hub y del dispositivo

cadena de conexión de dispositivo de Hello participa en el centro de IoT de dispositivo simulado tooconnect tooyour. Hola cadena de conexión de base de datos central de IoT es registro, identidad toohello tooconnect usado en los dispositivos de Hola de IoT hub toomanage que se permiten tooconnect tooyour IoT hub.

- Lista de todos los centros de IoT. en el grupo de recursos si ejecuta Hola siguiente comando:

   ```bash
   az iot hub list -g iot-gateway --query [].name
   ```

   Use `iot-gateway` como valor de Hola de `{resource group name}` si no cambia.
- Obtener la cadena de conexión de base de datos central de hello IoT ejecutando el siguiente comando de hello:

   ```bash
   az iot hub show-connection-string --name {my hub name} -g iot-gateway
   ```

   `{my hub name}`es el nombre de Hola que especificó en la lección 2.

## <a name="configure-hello-device-connection-for-hello-sample-code"></a>Configurar conexión de dispositivo de hello para el código de ejemplo de Hola

Actualizar configuraciones de conexión de IoT hub- and dispositivo en `config-azure.json` realizando Hola pasos:

1. Abra `config-azure.json` en código de Visual Studio mediante la ejecución de hello siguiente comando en una ventana de consola:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-azure.json
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-azure.json
   ```

2. Realizar Hola después reemplazos en hello `config-azure.json` archivo:

   ![captura de pantalla de configuración de azure](media/iot-hub-gateway-kit-lessons/lesson3/config_azure.png)

   Reemplace `[IoT hub connection string]` con hello cadena de conexión de base de datos central de IoT.

## <a name="read-messages-from-your-iot-hub"></a>Lectura de mensajes en IoT Hub

Ejecutar aplicación de ejemplo de Hola simulada dispositivos y leer mensajes de centro de IoT por hello siguiente comando:

```bash
gulp run --iot-hub
```

comando de Hola ejecuta una aplicación Hola que envíe el centro de IoT de mensajes tooyour cada 2 segundos. También genera un mensaje de saludo de tooreceive de proceso secundario.

mensajes de saludo que se envían y reciben son Hola mostrados al instante en todos los mismo ventana en la consola Hola equipo host. se cerrará la aplicación Hello en 40 segundos.

![Aplicación de ejemplo simulada con mensajes enviados y recibidos](media/iot-hub-gateway-kit-lessons/lesson3/gulp_run_read_hub_simudev.png)

## <a name="summary"></a>Resumen

Ha ejecutado correctamente el centro de IoT tooyour datos de toosend de la aplicación de ejemplo de Hola con dispositivo simulado. También ha leído los mensajes de saludo que se han enviado tooyour centro de IoT.

## <a name="next-steps"></a>Pasos siguientes
[Creación de una instancia de Azure Function App y una cuenta de Azure Storage](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md)


