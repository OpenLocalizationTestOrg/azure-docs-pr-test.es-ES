---
title: "Connect Arduino (C) tooAzure IoT - lección 3: almacenamiento de tablas | Documentos de Microsoft"
description: Supervisar mensajes de dispositivo a la nube de hello tal y como se escriben tooyour almacenamiento de tabla de Azure.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "datos en la nube hello, recopilación de datos en la nube, servicio de nube de iot, datos de iot"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 386083e0-0dbb-48c0-9ac2-4f8fb4590772
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 9fef18bc9e780e78d95f0c643a5f193125130a5b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="read-messages-persisted-in-azure-storage"></a>Lectura de los mensajes que se conservan en Azure Storage
## <a name="what-you-will-do"></a>Lo que hará
Mensajes de dispositivo para la nube de saludo de monitor que se envían desde el centro de IoT Adafruit compacto M0 Wi-Fi Arduino panel tooyour como mensajes de saludo se escriben tooyour almacenamiento de tabla de Azure.

Si tiene problemas, buscar soluciones en hello [solución de problemas de página][troubleshooting].

## <a name="what-you-will-learn"></a>Lo qué aprenderá
En este artículo, obtendrá información sobre cómo se guardan los mensajes de tooread de toouse Hola gulp tarea de mensaje de lectura en el almacenamiento de tabla de Azure.

## <a name="what-you-need"></a>Lo que necesita
Antes de iniciar este proceso, debe haber completado correctamente [ejecutar aplicación de ejemplo de Hola parpadeo Azure en el panel de Arduino][run-blink-application].

## <a name="read-new-messages-from-your-storage-account"></a>Lectura de mensajes nuevos de la cuenta de almacenamiento
En el artículo anterior de hello, ejecutó una aplicación de ejemplo en el panel de Arduino. aplicación de ejemplo de Hola envía centro de IoT de Azure de tooyour de mensajes. mensajes de saludo enviados tooyour centro de IoT se almacenan en el almacenamiento de la tabla de Azure a través de la aplicación de Azure función hello. Debe tooread mensajes de Hola almacenamiento de Azure conexión cadena desde el almacenamiento de tabla de Azure.

mensajes de tooread almacenados en el almacenamiento de tabla de Azure, siga estos pasos:

1. Obtener la cadena de conexión de hello ejecutando Hola siguientes comandos:

   ```bash
   az storage account list -g iot-sample --query [].name
   az storage account show-connection-string -g iot-sample -n {storage name}
   ```

   Hola primer comando recupera hello `storage name` que se usa en hello segunda comando tooget Hola cadena de conexión. Use `iot-sample` como valor de Hola de `{resource group name}` si no cambia el valor de Hola.
2. Archivo de configuración abierto hello `config-arduino.json` en código de Visual Studio mediante la ejecución de hello siguiente comando:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-arduino.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-arduino.json
   ```
3. Reemplace `[Azure storage connection string]` con la cadena de conexión de Hola que obtuvo en el paso 1.
4. Guardar hello `config-arduino.json` archivo.
5. Enviar mensajes de nuevo y leer desde el almacenamiento de tabla de Azure ejecutando el siguiente comando de hello:

   ```bash
   gulp run --read-storage

   # You can monitor hello serial port by running listen task:
   gulp listen

   # Or you can combine above two gulp tasks into one:
   gulp run --read-storage --listen
   ```

   Hello lógica para leer del almacenamiento de tabla de Azure está en hello `azure-table.js` archivo.

   ![Ejecución de Gulp: almacenamiento de lectura][gulp-run]

## <a name="summary"></a>Resumen
Ha conectado el centro de IoT Arduino tooyour de panel en la nube de hello correctamente y utiliza mensajes de Hola parpadeo ejemplo aplicación toosend dispositivo a la nube. También utiliza hello Azure función aplicación toostore entrantes IoT hub mensajes tooyour almacenamiento tabla de Azure. Ahora puede enviar mensajes de la nube al dispositivo desde la tooyour de centro de IoT Arduino panel.

## <a name="next-steps"></a>Pasos siguientes
[Envío de mensajes de nube a dispositivo][send-cloud-to-device-messages]
<!-- Images and links -->

[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[run-blink-application]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-run-azure-blink.md
[gulp-run]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/gulp_read_message_arduino.png
[send-cloud-to-device-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson4-send-cloud-to-device-messages.md