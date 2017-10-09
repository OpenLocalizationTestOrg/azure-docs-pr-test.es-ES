---
title: "Dispositivo SensorTag y puerta de enlace de Azure IoT: Lección 4: Table Storage | Microsoft Docs"
description: "Guardar mensajes Intel NUC tooyour centro de IoT, escribirlos tooAzure el almacenamiento de tabla y, a continuación, leerlos desde la nube de Hola."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: recuperar datos de la nube, servicio en la nube de iot
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 8ca78045-ad92-4a6a-90f1-05f9668e6f0e
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 29525b084eb4d6e6dfcb16d9b34f78f075d30b7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="read-messages-persisted-in-azure-table-storage"></a>Lectura de mensajes guardados en Azure Table Storage

## <a name="what-you-will-do"></a>Lo que hará

- Ejecutar la aplicación de ejemplo de puerta de enlace de hello en la puerta de enlace que envía el centro de IoT tooyour de mensajes.
- A continuación, ejecutar código de ejemplo en los mensajes de Hola host tooread de equipo en el almacenamiento de tabla de Azure. 

Si tiene problemas, buscar soluciones en hello [página solución de problemas](iot-hub-gateway-kit-c-troubleshooting.md).

## <a name="what-you-will-learn"></a>Lo qué aprenderá

¿Cómo toouse hello gulp herramienta toorun Hola ejemplo código tooread mensajes en el almacenamiento de tabla de Azure.

## <a name="what-you-need"></a>Lo que necesita

Deben tener correctamente hello las siguientes tareas:

- [Crear cuenta de almacenamiento de Azure de Hola y aplicación de Azure función hello](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md).
- [Ejecutar la aplicación de ejemplo de puerta de enlace de hello](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md).
- [Lectura de mensajes desde el IoT Hub](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md)

## <a name="get-your-azure-storage-connection-strings"></a>Obtener cadenas de conexión de Azure Storage

Al principio de esta lección, creó correctamente una cuenta de almacenamiento de Azure. cadena de conexión de hello tooget de cuenta de almacenamiento de Azure de hello, ejecute hello siguientes comandos:

* Enumere todas las cuentas de almacenamiento.

```bash
az storage account list -g iot-gateway --query [].name
```

* Obtenga la cadena de conexión de Azure Storage.

```bash
az storage account show-connection-string -g iot-gateway -n {storage name}
```

Usar puerta de enlace de iot como valor de Hola de `{resource group name}` si no cambia el valor de hello en la lección 2.

## <a name="configure-hello-device-connection"></a>Configurar conexión de dispositivo de Hola

Hola de actualización `config-azure.json` de archivos para que el código de ejemplo de Hola que se ejecuta en el equipo de host de hello puede leer el mensaje en el almacenamiento de tabla de Azure. tooconfigure Hola conexión del dispositivo, siga estos pasos:

1. Archivo de configuración de dispositivo abierto hello `config-azure.json` ejecutando Hola siguientes comandos:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-azure.json
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-azure.json
   ```

   ![configuración](media/iot-hub-gateway-kit-lessons/lesson4/config_azure.png)

2. Reemplace `[Azure storage connection string]` con hello cadena de conexión de almacenamiento de Azure que ha adquirido.

   `[IoT hub connection string]` ya se debe haber sustituido en la sección [Lectura de mensajes en Azure IoT Hub](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md) de la lección 3.

## <a name="read-messages-in-your-azure-table-storage"></a>Lectura de mensajes en Azure Table Storage

Ejecutar la aplicación de ejemplo de puerta de enlace de Hola y leer mensajes de almacenamiento de tabla de Azure, Hola siguiente comando:

```bash
gulp run --table-storage
```

El centro de IoT desencadena el mensaje de toosave de aplicación de función de Azure en el almacenamiento de la tabla de Azure cuando llega un mensaje nuevo.
Hola `gulp run` comando ejecuta la aplicación de ejemplo de puerta de enlace que envía el centro de IoT tooyour de mensajes. Con `table-storage` parámetro, también genera un Hola de tooreceive de proceso secundario guarda el mensaje en el almacenamiento de tabla de Azure.

mensajes de saludo que se envían y reciben son Hola mostrados al instante en todos los mismo ventana en la consola Hola equipo host. instancia de aplicación de ejemplo de Hola se cerrará automáticamente en 40 segundos.

   ![Lectura en Gulp](media/iot-hub-gateway-kit-lessons/lesson4/gulp_run_read_table.png)


## <a name="summary"></a>Resumen

Mensajes de saludo de tooread de código de ejemplo de Hola haya ejecutado en el almacenamiento de Azure tabla guardado por la aplicación de la función de Azure.
