---
title: "Connect Raspberry PI (C) tooAzure IoT - lección 1: implementar la aplicación | Documentos de Microsoft"
description: "Clonar aplicación de ejemplo C hello desde GitHub y gulp toodeploy este panel de tooyour frambuesa Pi 3 de la aplicación. Esta aplicación de ejemplo parpadea Hola LED conectado toohello panel cada dos segundos."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: intermitencia de led de raspberry pi, led intermitente con raspberry pi
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: f601d1e1-2bc3-4cc5-a6b1-0467e5304dcf
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: e90c3360c4de1873313db19561c781eb21dbf1d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-hello-blink-application"></a>Crear e implementar la aplicación de hello parpadeo
## <a name="what-you-will-do"></a>Lo que hará
Clonar aplicación de C de ejemplo de Hola desde GitHub y usar hello gulp herramienta toodeploy Hola ejemplo aplicación tooRaspberry 3 de Pi. aplicación de ejemplo de Hola parpadea Hola LED conectado toohello panel cada dos segundos. Si tiene problemas, buscar soluciones en hello [página solución de problemas](iot-hub-raspberry-pi-kit-c-troubleshooting.md).

## <a name="what-you-will-learn"></a>Lo qué aprenderá
En este artículo, aprenderá lo siguiente:

* ¿Cómo toouse hello `device-discover-cli` tooretrieve de herramienta de la red sobre Pi.
* La ejecución hello y toodeploy aplicación sobre Pi de ejemplo.
* ¿Cómo toodeploy y depurar las aplicaciones ejecutando de forma remota en Pi.

## <a name="what-you-need"></a>Lo que necesita
Debe haber completado correctamente hello las siguientes operaciones:

* [Configuración del dispositivo](iot-hub-raspberry-pi-kit-c-lesson1-configure-your-device.md)
* [Obtener herramientas de Hola](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)

## <a name="obtain-hello-ip-address-and-host-name-of-pi"></a>Obtener nombre de host y dirección IP de Hola de Pi
Abra un símbolo del sistema en Windows o un terminal de Mac OS o Ubuntu y, a continuación, ejecute el siguiente comando de hello:

```bash
devdisco list --eth
```

Debería ver un resultado similar siguiente toohello:

![Detección de dispositivos](media/iot-hub-raspberry-pi-lessons/lesson1/device_discovery.png)

Tome nota de hello `IP address` y `hostname` de Pi. Necesitará esta información posteriormente en este artículo.

> [!NOTE]
> Asegúrese de que ese Pi está conectado toohello misma red que el equipo. Por ejemplo, si el equipo está conectado tooa red inalámbrica mientras Pi es tooa conectado por cable de red, no verá Hola IP dirección en la salida de hello devdisco.

## <a name="open-hello-sample-application"></a>Aplicación de ejemplo de Hola abierto
Hola tooopen aplicación de ejemplo, siga estos pasos:

1. Clonar el repositorio de ejemplo de Hola desde GitHub ejecutando Hola siguiente comando:
   
    ```bash
    git clone https://github.com/Azure-Samples/iot-hub-c-raspberrypi-getting-started.git
    ```
2. Abra la aplicación de ejemplo de Hola en código de Visual Studio mediante la ejecución de hello siguientes comandos:
   
    ```bash
    cd iot-hub-c-raspberrypi-getting-started
    cd Lesson1
    code .
    ```

![Estructura del repositorio](media/iot-hub-raspberry-pi-lessons/lesson1/vscode-blink-c-mac.png)

Hola `main.c` archivo Hola `app` subcarpeta es el archivo de origen de la clave de Hola que contiene Hola código toocontrol Hola LED.

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
   
   archivo de configuración de Hello `config-raspberrypi.json` contiene las credenciales de usuario de hello usar toolog en tooPi. pérdida de hello tooavoid de credenciales de usuario, se genera el archivo de configuración de hello en subcarpeta hello `.iot-hub-getting-started` de la carpeta particular de hello en el equipo.

2. Abra el archivo de configuración de dispositivo de hello en código de Visual Studio mediante la ejecución de hello siguiente comando:
   
   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-raspberrypi.json
   
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-raspberrypi.json
   ```

3. Reemplace el marcador de posición de hello `[device hostname or IP address]` con dirección IP de Hola o nombre de host de hello obtenido anteriormente en "Obtener Hola IP dirección y nombre de host de Pi."
   
   ![Config.json](media/iot-hub-raspberry-pi-lessons/lesson1/vscode-config-mac.png)

> [!NOTE]
> Puede usar la clave SSH en lugar del nombre de usuario y contraseña al conectar tooRaspberry Pi. En Ordenar toodo esto tendrá toogenerate Hola clave utilizando **ssh-keygen** y **ssh-copy-Id. pi @\<dirección del dispositivo\>**.
>
> En Windows, estos comandos están disponibles en **Git Bash**.
>
> En Mac OS necesita toorun **cerveza instalar ssh-copy-id**.
>
> Después de cargar correctamente Hola clave toohello frambuesa Pi, reemplace **device_password** con **device_key_path** propiedad en **raspberrypi.json config**.
>
> Las líneas actualizadas deben presentar el siguiente aspecto:
> ```javascript
> "device_user_name": "pi",
> "device_key_path": "id_rsa",
> ```

¡Enhorabuena! Ha creado correctamente la primera aplicación de ejemplo hello de Pi.

## <a name="deploy-and-run-hello-sample-application"></a>Implementar y ejecutar la aplicación de ejemplo de Hola
### <a name="install-hello-azure-iot-hub-sdk-on-pi"></a>Instalar hello Azure IoT Hub SDK en Pi
Instale hello Azure IoT Hub SDK sobre Pi con hello siguiente comando:

```bash
gulp install-tools
```

Esta tarea puede tardar unos Hola de toocomplete minutos primera vez que lo ejecute.

### <a name="deploy-and-run-hello-sample-app"></a>Implementar y ejecutar la aplicación de ejemplo de Hola
Implementar y ejecutar la aplicación de ejemplo de Hola ejecutando Hola siguiente comando:

```bash
gulp deploy && gulp run
```

### <a name="verify-hello-app-works"></a>Compruebe que funciona de la aplicación de Hola
aplicación de ejemplo de Hola finaliza automáticamente después de hello LED parpadea para 20 veces. Si no ve Hola LED parpadea, vea hello [Guía de solución de problemas](iot-hub-raspberry-pi-kit-c-troubleshooting.md) para soluciones toocommon problemas.
![Intermitencia del LED](media/iot-hub-raspberry-pi-lessons/lesson1/led_blinking.jpg)

## <a name="summary"></a>Resumen
Ha instalado Hola requerido herramientas toowork con Pi e implementado un Hola de tooblink tooPi de aplicación de ejemplo LED. Ahora puede crear, implementar y ejecutar otra aplicación de ejemplo que se conecta Pi tooAzure toosend centro de IoT y recibir mensajes.

## <a name="next-steps"></a>Pasos siguientes
[Obtención de las herramientas de Azure](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-win32.md)

