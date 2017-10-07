---
title: "Conectar Intel Edison (nodo) tooAzure IoT - lección 1: implementar la aplicación | Documentos de Microsoft"
description: "Clonar aplicación de ejemplo C hello desde GitHub y ejecute gulp toodeploy este panel Intel Edison tooyour de aplicación. Esta aplicación de ejemplo parpadea Hola LED conectado toohello panel cada dos segundos."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "proyectos de LED de Arduino, intermitencia del LED de Arduino, código de intermitencia del LED de Arduino, programa de intermitencia del LED de Arduino, ejemplo de intermitencia en Arduino"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: ed2c21d0-c72c-4ac2-9e70-347e9a0711c0
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: bc03c7e45bd1ba9e9b2c8f2fec70a1be647e96b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-hello-blink-application"></a>Crear e implementar la aplicación de hello parpadeo
## <a name="what-you-will-do"></a>Lo que hará
Clonar aplicación de ejemplo C hello desde GitHub y usar el ejemplo hello de aplicación para la herramienta de gulp hello toodeploy, tooIntel Edison. aplicación de ejemplo de Hola parpadea Hola LED conectado toohello panel cada dos segundos. Si tiene problemas, buscar soluciones en hello [solución de problemas de página][troubleshooting].

## <a name="what-you-will-learn"></a>Lo qué aprenderá
* La ejecución hello y toodeploy aplicación en Edison de ejemplo.

## <a name="what-you-need"></a>Lo que necesita
Debe haber completado correctamente hello las siguientes operaciones:

* [Configuración del dispositivo][configure-your-device]
* [Obtener herramientas de Hola][get-the-tools]

## <a name="open-hello-sample-application"></a>Aplicación de ejemplo de Hola abierto
Hola tooopen aplicación de ejemplo, siga estos pasos:

1. Clonar el repositorio de ejemplo de Hola desde GitHub ejecutando Hola siguiente comando:

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-node-edison-getting-started.git
   ```
2. Abra la aplicación de ejemplo de Hola en código de Visual Studio mediante la ejecución de hello siguientes comandos:

   ```bash
   cd iot-hub-node-edison-getting-started
   cd Lesson1
   code .
   ```

   ![Estructura del repositorio][repo-structure]

archivo de Hello en hello `app` subcarpeta es el archivo de origen de la clave de Hola que contiene Hola código toocontrol Hola LED.

### <a name="install-application-dependencies"></a>Instalación de las dependencias de aplicaciones
Instalar bibliotecas de Hola y otros módulos que necesita para la aplicación de ejemplo de Hola ejecutando el siguiente comando de hello:

```bash
npm install
```

## <a name="configure-hello-device-connection"></a>Configurar conexión de dispositivo de Hola
tooconfigure Hola conexión del dispositivo, siga estos pasos:

1. Generar archivo de configuración de dispositivo de hello ejecutando Hola siguiente comando:

   ```bash
   gulp init
   ```

   archivo de configuración de Hello `config-edison.json` contiene las credenciales de usuario de hello usar toolog en tooEdison. pérdida de hello tooavoid de credenciales de usuario, se genera el archivo de configuración de hello en subcarpeta hello `.iot-hub-getting-started` de la carpeta particular de hello en el equipo.

2. Abra el archivo de configuración de dispositivo de hello en código de Visual Studio mediante la ejecución de hello siguiente comando:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-edison.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-edison.json
   ```

3. Reemplace el marcador de posición de hello `[device hostname or IP address]` y `[device password]` con la dirección IP de Hola y la contraseña que ha marcado hacia abajo en la lección anterior.

   ![Config.json](media/iot-hub-intel-edison-lessons/lesson1/vscode-config-mac.png)

¡Enhorabuena! Primera aplicación de ejemplo Hola para Edison que ha creado correctamente.

## <a name="deploy-and-run-hello-sample-application"></a>Implementar y ejecutar la aplicación de ejemplo de Hola

### <a name="deploy-and-run-hello-sample-app"></a>Implementar y ejecutar la aplicación de ejemplo de Hola
Implementar y ejecutar la aplicación de ejemplo de Hola ejecutando Hola siguiente comando:

```bash
gulp deploy && gulp run
```

### <a name="verify-hello-app-works"></a>Compruebe que funciona de la aplicación de Hola
aplicación de ejemplo de Hola finaliza automáticamente después de hello LED parpadea para 20 veces. Si no ve Hola LED parpadea, vea hello [Guía de solución de problemas] [ troubleshooting] para soluciones toocommon problemas.

![Intermitencia del LED][led-blinking]

## <a name="summary"></a>Resumen
Ha instalado Hola requerido herramientas toowork con Edison e implementado un Hola de tooblink tooEdison de aplicación de ejemplo LED. Ahora puede crear, implementar y ejecutar otra aplicación de ejemplo que se conecta Edison tooAzure toosend centro de IoT y recibir mensajes.

## <a name="next-steps"></a>Pasos siguientes
[Obtener hello Azure tools][get-the-azure-tools]

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[Configure-your-device]: iot-hub-intel-edison-kit-node-lesson1-configure-your-device.md
[get-the-tools]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-win32.md
[repo-structure]: media/iot-hub-intel-edison-lessons/lesson1/repo_structure.png
[led-blinking]: media/iot-hub-intel-edison-lessons/lesson1/led_blinking.png
[get-the-azure-tools]: iot-hub-intel-edison-kit-node-lesson2-get-azure-tools-win32.md
