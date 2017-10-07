---
title: "Connect Arduino (C) tooAzure IoT - lección 3: ejecutar el ejemplo | Documentos de Microsoft"
description: "Implemente y ejecute un tooAdafruit de aplicación de ejemplo Wi-Fi de desvanecimiento M0 que envía el centro de IoT tooyour de mensajes y parpadea Hola LED."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: servicio de nube de IOT, arduino enviar datos toocloud
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 92cce319-2b17-4c9b-889d-deac959e3e7c
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: ddca015a3655f8a1a9de2a00e718ec0d28a5affb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-toosend-device-to-cloud-messages"></a>Ejecutar un toosend de la aplicación de ejemplo mensajes del dispositivo a la nube
## <a name="what-you-will-do"></a>Lo que hará
En este artículo le mostrará cómo toodeploy y ejecute una aplicación de ejemplo en su Arduino de Wi-Fi Adafruit compacto M0 ese centro de IoT envía mensajes tooyour del panel.

Si tiene problemas, buscar soluciones en hello [solución de problemas de página][troubleshooting].

## <a name="what-you-will-learn"></a>Lo qué aprenderá
Obtendrá información sobre cómo hello toouse gulp toodeploy de herramienta y ejecutar la aplicación de Arduino de ejemplo de Hola en el panel de Arduino.

## <a name="what-you-need"></a>Lo que necesita
* Antes de iniciar esta tarea, debe haber completado correctamente [crear una aplicación de Azure de función y un centro de IoT de almacenamiento cuenta tooprocess y el almacén de mensajes][process-and-store-iot-hub-messages].

## <a name="get-your-iot-hub-and-device-connection-strings"></a>Obtención de las cadenas de conexión de IoT Hub y del dispositivo
Hola la cadena de conexión de dispositivo es tooconnect usado en su centro de IoT Arduino tooyour de panel. cadena de conexión de base de datos central de Hello IoT es tooconnect usado su identidad de dispositivos de IoT hub toohello que representa su Arduino del panel de centro de IoT Hola.

* Lista de todos los centros de IoT. en el grupo de recursos si ejecuta Hola siguiente comando de CLI de Azure:

```bash
az iot hub list -g iot-sample --query [].name
```

Use `iot-sample` como valor de Hola de `{resource group name}` si no cambia el valor de Hola.

* Obtener la cadena de conexión de base de datos central de hello IoT ejecutando el siguiente comando de CLI de Azure de hello:

```bash
az iot hub show-connection-string --name {my hub name}
```

`{my hub name}`es el nombre de Hola que especificó cuando creó el centro de IoT y había registrado en el panel de Arduino.

* Obtener la cadena de conexión de dispositivo de hello ejecutando Hola siguiente comando:

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id mym0wifi
```

Use `mym0wifi` como valor de Hola de `{device id}` si no cambia el valor de Hola.
## <a name="configure-hello-device-connection"></a>Configurar conexión de dispositivo de Hola
tooconfigure Hola conexión del dispositivo, siga estos pasos:

1. Obtener el puerto serie de hello de dispositivo de hello con cli de detección de dispositivos de hello:

   ```bash
   devdisco list --usb
   ```

   Debe ver un resultado similar siguiente toohello y encontrar Hola usb puerto COM de su placa de Arduino:

   ![Detección de dispositivos][device-discovery]

2. Archivo abierto hello `config.json` en Hola carpeta lección y agregar valor Hola de hello encuentra el número de puerto COM:

   ```json
   {
       "device_port" : "COM1"
   }
   ```

   ![config.json][config-json]

   > [!NOTE]
   > Para el puerto de hello COM, en la plataforma Windows, tiene un formato de hello `COM1, COM2, ...`. En macOS o Ubuntu, empieza por `/dev/`.

3. Inicializar el archivo de configuración de hello ejecutando Hola siguientes comandos:

   ```bash
   npm install
   gulp init
   gulp install-tools
   ```
4. Archivo de configuración de dispositivos de hello abierto `config-arduino.json` en código de Visual Studio mediante la ejecución de hello siguiente comando:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-arduino.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-arduino.json
   ```

   ![config-arduino.json][config-arduino-json]

5. Realizar Hola después reemplazos en hello `config-arduino.json` archivo:

   * Reemplace **[Wi-Fi SSID]** con el SSID de Wi-Fi que conectado toohello Internet.
   * Reemplace **[Wi-Fi password]** por su contraseña de Wi-Fi. Quite la cadena de hello si su Wi-Fi no requiere una contraseña.
   * Reemplace **[cadena de conexión de dispositivos de IoT]** con hello `device connection string` obtenidas.
   * Reemplace **[cadena de conexión de base de datos central de IoT]** con hello `iot hub connection string` obtenidas.

   > [!NOTE]
   > `azure_storage_connection_string` no es necesario en este artículo. Déjelo como está.

## <a name="deploy-and-run-hello-sample-application"></a>Implementar y ejecutar la aplicación de ejemplo de Hola
Implementar y ejecutar la aplicación de ejemplo de Hola en el panel de Arduino ejecutando Hola siguiente comando:

```bash
gulp run
# You can monitor hello serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

> [!NOTE]
> Hello predeterminado gulp tarea ejecuta `install-tools` y `run` las tareas de forma secuencial. Cuando se [implementar aplicación de intermitencia hello][deployed-the-blink-app], ejecutar estas tareas por separado.

## <a name="verify-that-hello-sample-application-works"></a>Compruebe que la aplicación de ejemplo de Hola funciona
Debería ver Hola GPIO #0 a bordo LED parpadea cada dos segundos. Cada vez que Hola LED parpadea, aplicación de ejemplo de Hola envía un centro de IoT tooyour de mensaje y comprueba que ese mensaje Hola se ha enviado correctamente tooyour centro de IoT. Además, cada mensaje recibido por el centro de IoT Hola se imprime en la ventana de la consola de Hola. aplicación de ejemplo de Hola finaliza automáticamente después de enviar 20 mensajes.

![Aplicación de ejemplo con mensajes enviados y recibidos][sample-application-with-sent-and-received-messages]

## <a name="summary"></a>Resumen
Ha implementado y ejecutar aplicación de ejemplo de Hola nueva parpadeo en su centro de IoT Arduino panel toosend mensajes del dispositivo a la nube tooyour. Ahora, supervisar los mensajes tal y como se escriben toohello cuenta de almacenamiento.

## <a name="next-steps"></a>Pasos siguientes
[Lectura de los mensajes que se conservan en Azure Storage][read-messages-persisted-in-azure-storage]
<!-- Images and links -->

[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-deploy-resource-manager-template.md
[device-discovery]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/device_discovery.png
[config-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-config-mac.png
[config-arduino-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/config-arduino.png
[deployed-the-blink-app]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-deploy-blink-app.md
[sample-application-with-sent-and-received-messages]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/gulp_run_arduino.png
[read-messages-persisted-in-azure-storage]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-read-table-storage.md