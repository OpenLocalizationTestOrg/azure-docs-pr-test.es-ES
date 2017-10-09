---
title: "Conectar Intel Edison (nodo) tooAzure IoT - lección 3: supervisar mensajes | Documentos de Microsoft"
description: Supervisar mensajes de dispositivo a la nube de hello tal y como se escriben tooyour almacenamiento de tabla de Azure.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "datos en la nube hello, recopilación de datos en la nube, servicio de nube de iot, datos de iot"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: fa2c7efe-7e34-4e39-bb70-015c15ac69ed
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 8f6371482123bc9aa12db55b38d3e8863645f981
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="read-messages-persisted-in-azure-storage"></a>Lectura de los mensajes que se conservan en Azure Storage
## <a name="what-you-will-do"></a>Lo que hará
Mensajes de dispositivo para la nube de saludo de monitor que se envían desde el centro de IoT de Intel Edison tooyour como mensajes de saludo se escriben tooyour almacenamiento de tabla de Azure. Si tiene problemas, buscar soluciones en hello [solución de problemas de página][troubleshooting].

## <a name="what-you-will-learn"></a>Lo qué aprenderá
En este artículo, obtendrá información sobre cómo se guardan los mensajes de tooread de toouse Hola gulp tarea de mensaje de lectura en el almacenamiento de tabla de Azure.

## <a name="what-you-need"></a>Lo que necesita
Antes de iniciar este proceso, debe haber completado correctamente [ejecutar aplicación de ejemplo de Hola Azure parpadeo en Intel Edison][run-the-azure-blink-sample-application-on-intel-edison].

## <a name="read-new-messages-from-your-storage-account"></a>Lectura de mensajes nuevos de la cuenta de almacenamiento
En el artículo anterior de hello, ejecutó una aplicación de ejemplo en Edison. aplicación de ejemplo de Hola envía centro de IoT de Azure de tooyour de mensajes. mensajes de saludo enviados tooyour centro de IoT se almacenan en el almacenamiento de la tabla de Azure a través de la aplicación de Azure función hello. Debe tooread mensajes de Hola almacenamiento de Azure conexión cadena desde el almacenamiento de tabla de Azure.

mensajes de tooread almacenados en el almacenamiento de tabla de Azure, siga estos pasos:

1. Obtener la cadena de conexión de hello ejecutando Hola siguientes comandos:

   ```bash
   az storage account list -g iot-sample --query [].name
   az storage account show-connection-string -g iot-sample -n {storage name}
   ```

   Hola primer comando recupera hello `storage name` que se usa en hello segunda comando tooget Hola cadena de conexión. Use `iot-sample` como valor de Hola de `{resource group name}` si no cambia el valor de Hola.
2. Archivo de configuración abierto hello `config-edison.json` en código de Visual Studio mediante la ejecución de hello siguiente comando:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-edison.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-edison.json
   ```
3. Reemplace `[Azure storage connection string]` con la cadena de conexión de Hola que obtuvo en el paso 1.
4. Guardar hello `config-edison.json` archivo.
5. Enviar mensajes de nuevo y leer desde el almacenamiento de tabla de Azure ejecutando el siguiente comando de hello:

   ```bash
   gulp run --read-storage
   ```

   Hello lógica para leer del almacenamiento de tabla de Azure está en hello `azure-table.js` archivo.

   ![Ejecución de Gulp: almacenamiento de lectura][gulp run]

## <a name="summary"></a>Resumen
Ha conectado el centro de IoT Edison tooyour en la nube de hello correctamente y usa mensajes de Hola parpadeo ejemplo aplicación toosend dispositivo a la nube. También utiliza hello Azure función aplicación toostore entrantes IoT hub mensajes tooyour almacenamiento tabla de Azure. Ahora puede enviar mensajes de la nube al dispositivo desde la tooEdison del centro de IoT.

## <a name="next-steps"></a>Pasos siguientes
[Ejecutar un tooreceive de la aplicación de ejemplo en la nube al dispositivo mensajes][receive-cloud-to-device-messages]
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[run-the-azure-blink-sample-application-on-intel-edison]: iot-hub-intel-edison-kit-node-lesson3-run-azure-blink.md
[gulp run]: media/iot-hub-intel-edison-lessons/lesson3/gulp_read_message.png
[receive-cloud-to-device-messages]: iot-hub-intel-edison-kit-node-lesson4-send-cloud-to-device-messages.md