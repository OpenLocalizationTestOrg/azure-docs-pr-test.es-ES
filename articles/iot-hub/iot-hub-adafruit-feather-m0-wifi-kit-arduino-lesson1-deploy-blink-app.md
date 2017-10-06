---
title: "Conectar Arduino tooAzure IoT - lección 1: implementar la aplicación | Documentos de Microsoft"
description: "Clonar Arduino aplicación de ejemplo de Hola desde GitHub y ejecutar gulp toodeploy esta tooyour aplicación Adafruit compacto M0 Wi-Fi. Esta aplicación de ejemplo parpadea Hola GPIO"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "proyectos de LED de Arduino, intermitencia del LED de Arduino, código de intermitencia del LED de Arduino, programa de intermitencia del LED de Arduino, ejemplo de intermitencia en Arduino"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: b0a7d076-d580-4686-9f7d-c0712750b615
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 5bf8e4ae88e070aeacf34bfc43b8d2daeeb1a2fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-hello-blink-application"></a>Crear e implementar la aplicación de hello parpadeo
## <a name="what-you-will-do"></a>Lo que hará
Clonar Arduino aplicación de ejemplo de Hola desde GitHub y usar hello gulp herramienta toodeploy Hola ejemplo aplicación tooyour Adafruit compacto M0 Wi-Fi Arduino panel. aplicación de ejemplo Hola Hola parpadea GPIO número 13 en barod LED cada dos segundos.

Si tiene problemas, buscar soluciones en hello [solución de problemas de página][troubleshooting-page].

## <a name="what-you-will-learn"></a>Lo qué aprenderá
* La ejecución hello y toodeploy aplicación en el panel de Arduino de ejemplo.

## <a name="what-you-need"></a>Lo que necesita
Debe haber completado correctamente hello las siguientes operaciones:

* [Configuración del dispositivo][configure-your-device]
* [Obtener herramientas de Hola][get-the-tools]

## <a name="open-hello-sample-application"></a>Aplicación de ejemplo de Hola abierto
Hola tooopen aplicación de ejemplo, siga estos pasos:

1. Clonar el repositorio de ejemplo de Hola desde GitHub ejecutando Hola siguiente comando:

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-c-feather-m0-getting-started.git
   ```
2. Abra la aplicación de ejemplo de Hola en código de Visual Studio mediante la ejecución de hello siguientes comandos:

   ```bash
   cd iot-hub-c-feather-m0-getting-started
   cd Lesson1
   code .
   ```

   ![Estructura del repositorio][repo-structure]

Hola `app.ino` archivo Hola `app` subcarpeta es el archivo de origen de la clave de Hola que contiene Hola código toocontrol Hola LED.

### <a name="install-application-dependencies"></a>Instalación de las dependencias de aplicaciones
Instalar bibliotecas de Hola y otros módulos que necesita para la aplicación de ejemplo de Hola ejecutando el siguiente comando de hello:

```bash
npm install
```

## <a name="configure-hello-device-connection"></a>Configurar conexión de dispositivo de Hola
tooconfigure Hola conexión del dispositivo, siga estos pasos:

1. Obtener el puerto serie de hello de dispositivo de hello con cli de detección de dispositivos de hello:

   ```bash
   devdisco list --usb
   ```

   Debe ver un resultado que es similar siguiente toohello y encontrar Hola usb puerto COM de su placa de Arduino: ![detección de dispositivos][device-discovery]

2. Archivo abierto hello `config.json` en Hola carpeta lección y agregar valor Hola de hello encuentra el número de puerto COM:

   ```json
   {
       "device_port" : "COM1"
   }
   ```
   ![config.json][config-json]
   > [!NOTE]
   > Para el puerto de hello COM, en la plataforma Windows, tiene un formato de hello `COM1, COM2, ...`. En macOS o Ubuntu, empieza por `/dev/`.

## <a name="deploy-and-run-hello-sample-application"></a>Implementar y ejecutar la aplicación de ejemplo de Hola
### <a name="install-hello-required-tools-for-your-arduino-board"></a>Instalar las herramientas de hello necesario para el panel de Arduino

Instale hello centro de IoT de Azure SDK para el panel de Arduino con hello siguiente comando:

```bash
gulp install-tools
```

Esta tarea puede tardar un toocomplete mucho tiempo, dependiendo de la conexión de red.

> [!NOTE]
> Salga de Hola que ejecuta la instancia de Arduino IDE cuando se ejecuta tareas gulp: `install-tools`, `run`.

### <a name="deploy-and-run-hello-sample-app"></a>Implementar y ejecutar la aplicación de ejemplo de Hola
Implementar y ejecutar la aplicación de ejemplo de Hola ejecutando Hola siguiente comando:

```bash
gulp run

# You can monitor hello serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

### <a name="verify-hello-app-works"></a>Compruebe que funciona de la aplicación de Hola
Si no ve Hola LED parpadea, vea hello [Guía de solución de problemas] [ troubleshooting-page] para soluciones toocommon problemas.

![Intermitencia del LED][led-blinking]

## <a name="summary"></a>Resumen
Ha instalado Hola requerido herramientas toowork con el panel de Arduino e implementado un Hola ejemplo aplicación tooyour Arduino panel tooblink LED. Ahora puede crear, implementar y ejecutar otra aplicación de ejemplo que se conecta su tooAzure de panel Arduino toosend centro de IoT y recibir mensajes.

## <a name="next-steps"></a>Pasos siguientes
[Obtener hello Azure tools][get-the-azure-tools]

<!-- Images and links -->

[troubleshooting-page]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[configure-your-device]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-configure-your-device.md
[get-the-tools]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-win32.md
[repo-structure]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-blink-arduino-mac.png
[device-discovery]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/device_discovery.png
[config-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-config-mac.png
[led-blinking]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/led_blinking.png
[get-the-azure-tools]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-win32.md