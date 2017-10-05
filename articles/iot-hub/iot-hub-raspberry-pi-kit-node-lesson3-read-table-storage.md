---
featureFlags: usabilla
title: "Conexión de Raspberry Pi (Node) a Azure IoT: Lección 3: Table Storage | Microsoft Docs"
description: Supervise los mensajes del dispositivo a la nube a medida que se escriben en Azure Table Storage.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: recuperar datos de la nube, servicio en la nube de iot
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 9965bd54-61da-479b-aaad-5604850a2be5
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 60084906c05ff9e5396f8e2378d73f7ac939d8df
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="read-messages-persisted-in-azure-storage"></a>Lectura de los mensajes que se conservan en Azure Storage
## <a name="what-you-will-do"></a>Lo que hará
Va a supervisar los mensajes del dispositivo a la nube que se envían desde Raspberry Pi 3 a IoT Hub a medida que se escriben en Azure Table Storage. Si tiene problemas, busque soluciones en la [página de solución de problemas](iot-hub-raspberry-pi-kit-node-troubleshooting.md).

## <a name="what-you-will-learn"></a>Lo qué aprenderá
En este artículo, aprenderá a utilizar la tarea read-message de Gulp para leer los mensajes guardados en Azure Table Storage.

## <a name="what-you-need"></a>Lo que necesita
Antes de comenzar este procedimiento, debe de haber completado correctamente el tutorial sobre la [ejecución de una aplicación de ejemplo de Azure para activar el parpadeo en Raspberry Pi 3](iot-hub-raspberry-pi-kit-node-lesson3-run-azure-blink.md).

## <a name="read-new-messages-from-your-storage-account"></a>Lectura de mensajes nuevos de la cuenta de almacenamiento
En el artículo anterior, ejecutó una aplicación de ejemplo en Pi. La aplicación de ejemplo envío mensajes a IoT Hub de Azure. Los mensajes enviados a IoT Hub se almacenan en Azure Table Storage a través de Azure Function App. Para poder leer los mensajes de Azure Table Storage, necesita la cadena de conexión de Azure Storage.

Para leer los mensajes almacenados en Azure Table Storage, siga estos pasos:

1. Obtenga la cadena de conexión ejecutando el siguiente comando:

   ```bash
   az storage account list -g iot-sample --query [].name
   az storage account show-connection-string -g iot-sample -n {storage name}
   ```

   El primer comando recupera el elemento `storage name` que se utiliza en el segundo comando para obtener la cadena de conexión. Use `iot-sample` como valor de `{resource group name}`, si no lo modificó previamente.
2. Abra el archivo de configuración `config-raspberrypi.json` en Visual Studio Code con este comando:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-raspberrypi.json
   
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-raspberrypi.json
   ```
3. Reemplace `[Azure storage connection string]` por la cadena de conexión que obtuvo en el paso 1.
4. Guarde el archivo `config-raspberrypi.json`.
5. Vuelva a enviar los mensajes y léalos en Azure Table Storage mediante el siguiente comando:
   
   ```bash
   gulp run --read-storage
   ```
   
   La lógica para leer mensajes de Azure Table Storage se encuentra en el archivo `azure-table.js`.
   
    ![Ejecución de Gulp: almacenamiento de lectura](media/iot-hub-raspberry-pi-lessons/lesson3/gulp_read_message.png)

## <a name="summary"></a>Resumen
Ha conseguido conectar Pi a IoT Hub en la nube y utilizar la aplicación de ejemplo de activación del parpadeo para enviar mensajes del dispositivo a la nube. También ha utilizado Azure Function App para almacenar los mensajes entrantes de IoT Hub en Azure Table Storage. Ahora, puede enviar a Pi mensajes del dispositivo a la nube desde IoT Hub.

## <a name="next-steps"></a>Pasos siguientes
[Ejecución de una aplicación de ejemplo para recibir mensajes de la nube al dispositivo](iot-hub-raspberry-pi-kit-node-lesson4-send-cloud-to-device-messages.md)

