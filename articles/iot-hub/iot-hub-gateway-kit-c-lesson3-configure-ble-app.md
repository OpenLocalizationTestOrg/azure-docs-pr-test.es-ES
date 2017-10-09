---
title: "Dispositivo SensorTag y puerta de enlace de Azure IoT: Lección 3: Ejecución de la aplicación de ejemplo | Microsoft Docs"
description: "Ejecutar un datos de tooreceive habilitar la aplicación de ejemplo de Bilitar SensorTag y desde el centro de IoT."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Habilitar aplicación, aplicación monitor de sensor, recopilación de datos de sensor, datos de los sensores, toocloud de datos de sensor"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: b33e53a1-1df7-4412-ade1-45185aec5bef
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 4a8acdeadd402ffc82d3b766e1ec03a77ddcebb1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-and-run-a-ble-sample-application"></a>Configuración y ejecución de la aplicación de ejemplo BLE

## <a name="what-you-will-do"></a>Lo que hará

- Repositorio de ejemplo de Hola de clonación. 
- Configurar la conectividad de hello entre SensorTag y NUC de Intel. 
- Utilice hello Azure CLI tooget del centro de IoT y la información de SensorTag para una aplicación de ejemplo Bilitar (Bluetooth baja energía). Configurar y ejecutar la aplicación de ejemplo de Hola BLE. 

Si tiene problemas, buscar soluciones en hello [página solución de problemas](iot-hub-gateway-kit-c-troubleshooting.md).

## <a name="what-you-will-learn"></a>Lo qué aprenderá

En este artículo, aprenderá lo siguiente:

- ¿Cómo tooconfigure y ejecución Hola habilitar aplicación de ejemplo.

## <a name="what-you-need"></a>Lo que necesita

Debe haber completado correctamente los siguientes tutoriales:

- [Cree un IoT Hub y registre SensorTag](iot-hub-gateway-kit-c-lesson2-register-device.md)

## <a name="clone-hello-sample-repository-toohello-host-computer"></a>Equipo de host de clon Hola ejemplo repositorio toohello

repositorio de ejemplo de Hola tooclone, siga estos pasos en el equipo de host de hello:

1. Abra una ventana del símbolo del sistema en Windows o abra un terminal de macOS o Ubuntu.
2. Ejecute hello siguientes comandos:

   ```bash
   git clone https://github.com/Azure-samples/iot-hub-c-intel-nuc-gateway-getting-started
   cd iot-hub-c-intel-nuc-gateway-getting-started
   ```

## <a name="set-up-hello-connectivity-between-sensortag-and-intel-nuc"></a>Configurar la conectividad de hello entre SensorTag y NUC de Intel

tooset la conectividad de hello, siga estos pasos en el equipo de host de hello:

1. Inicializar el archivo de configuración de hello ejecutando Hola siguientes comandos:

   ```bash
   cd Lesson3
   npm install
   gulp init
   ```

2. Abra `config-gateway.json` en código de Visual Studio mediante la ejecución de hello siguiente comando:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-gateway.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-gateway.json
   ```

3. Busque Hola después de la línea de código y reemplace `[device hostname or IP address]` con el nombre de host o dirección IP de Hola de NUC de Intel.
   ![captura de pantalla de puerta de enlace de configuración](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)

4. Instalar herramientas auxiliares en Intel NUC ejecutando Hola siguiente comando:

   ```bash
   gulp install-tools
   ```

5. Activar SensorTag presionando el botón de encendido de hello como después de la imagen de Hola y Hola que debe parpadear LED verde.

   ![activar SensorTag](media/iot-hub-gateway-kit-lessons/lesson3/turn on_off sensortag.jpg)

6. Examinar SensorTag dispositivos mediante la ejecución de hello siguientes comandos:

   ```bash
   gulp discover-sensortag
   ```

7. Probar la conectividad de hello entre hello SensorTag y NUC de Intel mediante la ejecución de hello siguiente comando:

   ```bash
   gulp test-connectivity --mac {mac address}
   ```

   Reemplace `{mac address}` con dirección MAC que obtuvo en el paso anterior de Hola Hola.

## <a name="get-hello-connection-string-of-sensortag"></a>Obtener la cadena de conexión de Hola de SensorTag

Hola tooget cadena de conexión de base de datos central de IoT de Azure de SensorTag, ejecute hello siguiente comando en el equipo de host de hello:

```bash
az iot device show-connection-string --hub-name {IoT hub name} --device-id mydevice --resource-group iot-gateway
```

`{IoT hub name}`es el nombre del centro de IoT Hola que ha usado. Usar puerta de enlace de iot como valor de Hola de `{resource group name}` y use mydevice como valor de Hola de `{device id}` si no cambia el valor de hello en la lección 2.

## <a name="configure-hello-ble-sample-application"></a>Configurar la aplicación de ejemplo de Hola BLE

tooconfigure y ejecución Hola aplicación de ejemplo BLE, siga estos pasos en el equipo de host de hello:

1. Abra `config-sensortag.json` en código de Visual Studio mediante la ejecución de hello siguiente comando:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-sensortag.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-sensortag.json
   ```

   ![captura de sensortag configurado](media/iot-hub-gateway-kit-lessons/lesson3/config_sensortag.png)

2. Asegúrese de hello después reemplazos en el código de hello:
   - Reemplace `[IoT hub name]` con el nombre del centro de IoT Hola que ha usado.
   - Reemplace `[IoT device connection string]` con cadena de conexión de Hola de SensorTag que ha adquirido.
   - Reemplace `[device_mac_address]` con hello dirección MAC de hello SensorTag que ha adquirido.

3. Ejecute la aplicación de ejemplo de Hola BLE.

   Hola toorun aplicación de ejemplo BLE, siga estos pasos en el equipo de host de hello:

   1. Active SensorTag.

   2. Implementar y ejecutar la aplicación de ejemplo de Hola BLE en Intel NUC ejecutando el siguiente comando de hello:
   
      ```bash
      gulp run
      ```

## <a name="verify-that-hello-ble-sample-application-works"></a>Compruebe que la aplicación de ejemplo de Hola Bilitar funciona

Ahora debería ver una salida similar Hola siguiente:

![Resultado de la aplicación de ejemplo BLE](media/iot-hub-gateway-kit-lessons/lesson3/BLE_running.png)

aplicación de ejemplo de Hola mantiene la recopilación de datos de temperatura y enviarlo tooyour centro de IoT. aplicación de ejemplo de Hola finaliza automáticamente después de enviar 40 segundos.

## <a name="summary"></a>Resumen

Correctamente ha configurar la conectividad de hello entre SensorTag y NUC de Intel y ejecutar una aplicación de ejemplo Bilitar que recopila y envía los datos SensorTag tooyour centro de IoT. Está listo toolearn cómo tooverify que ha recibido su centro de IoT Hola datos.

## <a name="next-steps"></a>Pasos siguientes
[Lectura de mensajes en IoT Hub](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md)