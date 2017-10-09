---
title: "Dispositivo simulado y puerta de enlace de Azure IoT: Lección 3: Ejecución de la aplicación de ejemplo | Microsoft Docs"
description: "Ejecutar un centro de IoT dispositivo simulado ejemplo aplicación toosend temperatura datos tooyour"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: toocloud de datos
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 5d051d99-9749-4150-b3c8-573b0bda9c52
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: bc2c97919e95e4e3977a8b6ac75162bf2b5017be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-and-run-a-simulated-device-sample-app"></a>Configuración y ejecución de una aplicación de ejemplo de dispositivo simulado

## <a name="what-you-will-do"></a>Lo que hará

- Repositorio de ejemplo de Hola de clonación.
- Utilice hello Azure CLI tooget su información de dispositivo lógico y el centro de IoT para aplicación de ejemplo de dispositivo simulado. Configure y ejecute la aplicación de ejemplo de Hola simulada dispositivos.

Si tiene problemas, buscar soluciones en hello [página solución de problemas](iot-hub-gateway-kit-c-sim-troubleshooting.md).

## <a name="what-you-will-learn"></a>Lo qué aprenderá

En este artículo, aprenderá lo siguiente:

- Cómo tooconfigure y ejecución Hola simulan la aplicación de ejemplo de dispositivo.

## <a name="what-you-need"></a>Lo que necesita

Debe haber completado correctamente los siguientes tutoriales:

- [Creación de una instancia de IoT Hub y registro del dispositivo](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)

## <a name="clone-hello-sample-repository-toohello-host-computer"></a>Equipo de host de clon Hola ejemplo repositorio toohello

repositorio de ejemplo de Hola tooclone, siga estos pasos en el equipo de host de hello:

1. Abra una ventana del símbolo del sistema en Windows o abra un terminal de macOS o Ubuntu.
2. Ejecute hello siguientes comandos:

   ```bash
   git clone https://github.com/Azure-samples/iot-hub-c-intel-nuc-gateway-getting-started
   cd iot-hub-c-intel-nuc-gateway-getting-started
   ```

## <a name="configure-hello-simulated-device-and-your-nuc"></a>Configurar dispositivo simulado de Hola y su NUC

1. Archivo de configuración abierto hello `config.json` en código de Visual Studio mediante la ejecución de hello siguiente comando:

   ```bash
   code config.json
   ```

2. Reemplazar `"has_sensortag": true` con `"has_sensortag": false`

   ![Configurar un dispositivo de SensorTag de TI si no lo tiene](media/iot-hub-gateway-kit-lessons/lesson3/config_no_sensortag.png)

3. Inicializar el archivo de configuración de hello ejecutando Hola siguientes comandos:

   ```bash
   cd Lesson3
   npm install
   gulp init
   ```

4. Abra `config-gateway.json` en código de Visual Studio mediante la ejecución de hello siguiente comando:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-gateway.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-gateway.json
   ```

5. Busque Hola después de la línea de código y reemplace `[device hostname or IP address]` con el nombre de host o dirección IP de hello NUC de Intel.
   ![captura de pantalla de puerta de enlace de configuración](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)

## <a name="get-hello-connection-string-of-your-iot-hub-logical-device"></a>Obtener la cadena de conexión de Hola de su dispositivo lógico de centro de IoT

Hola tooget cadena de conexión de base de datos central de IoT de Azure del dispositivo lógico, ejecute hello siguiente comando en el equipo de host de hello:

```bash
az iot device show-connection-string --hub-name {IoT hub name} --device-id mydevice --resource-group iot-gateway
```

`{IoT hub name}`es el nombre del centro de IoT Hola que ha usado. Usar puerta de enlace de iot como valor de Hola de `{resource group name}` y use mydevice como valor de Hola de `{device id}` si no cambia el valor de hello en la lección 2.

## <a name="configure-hello-simulated-device-cloud-upload-sample-application"></a>Configuración de aplicación de ejemplo de carga de hello simulada dispositivos en la nube

tooconfigure y ejecución Hola simular dispositivos nube cargar la aplicación de ejemplo, siga estos pasos en el equipo de host de hello:

1. Abra `config-sensortag.json` en código de Visual Studio mediante la ejecución de hello siguiente comando:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-sensortag.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-sensortag.json
   ```

   ![captura de sensortag configurado](media/iot-hub-gateway-kit-lessons/lesson3/config_simulated_device.png)

2. Asegúrese de hello después reemplazos en el código de hello:
   - Reemplace `[IoT hub name]` con el nombre del centro de IoT Hola.
   - Reemplace `[IoT device connection string]` con cadena de conexión de Hola de su dispositivo lógico de centro de IoT.

3. Ejecute la aplicación hello.

   Implementar y ejecutar la aplicación hello ejecutando Hola siguiente comando:

   ```bash
   gulp run
   ```

## <a name="verify-hello-sample-application-works"></a>Compruebe que funciona de aplicación de ejemplo de Hola

Ahora debería ver resultados similares a Hola siguientes:

![resultado de la aplicación de ejemplo del dispositivo simulado](media/iot-hub-gateway-kit-lessons/lesson3/gulp_run_simudev.png)

aplicación Hello envía temperatura datos tooyour centro de IoT, que tiene una validez de 40 segundos.

## <a name="summary"></a>Resumen

Ha configurado correctamente y ejecución Hola simula la aplicación de ejemplo de carga de nube de dispositivo que envía el centro de IoT de tooyour de datos con el dispositivo simulado.

## <a name="next-steps"></a>Pasos siguientes
[Lectura de mensajes en IoT Hub](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md)