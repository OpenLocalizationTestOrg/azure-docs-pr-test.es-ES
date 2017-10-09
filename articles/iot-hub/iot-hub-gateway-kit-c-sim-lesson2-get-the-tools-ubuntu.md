---
title: "Dispositivo simulado y puerta de enlace de Azure IoT: Lección 2: Obtención de las herramientas (Ubuntu) | Microsoft Docs"
description: Instalar software de Hola y herramientas de hello en el equipo host ejecuta Ubuntu, crear un centro de IoT y registrar el dispositivo en el centro de IoT Hola.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "desarrollo de iot, software de iot, servicio en la nube de iot, software de internet de las cosas, cli de azure, instalar git en ubuntu, ejecución de gulp, instalar node js ubuntu"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: cf673154-ce67-4ed7-a9f7-2440301c6270
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 38c4d5d9cceec47758f0641cc26b631a7b19d37e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-ubuntu-1604"></a>Obtener herramientas de hello (Ubuntu 16.04)
> [!div class="op_single_selector"]
> * [Windows 7 o posterior](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)
> * [Ubuntu 16.04](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-ubuntu.md)
> * [macOS 10.10](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-mac.md)

## <a name="what-you-will-do"></a>Lo que hará

- Instale Git, Node.js, Gulp y Python.
- Instalar hello Azure interfaz de línea de comandos (CLI de Azure). 

Si tiene problemas, buscar soluciones en hello [página solución de problemas](iot-hub-gateway-kit-c-sim-troubleshooting.md).
## <a name="what-you-will-learn"></a>Lo qué aprenderá

En esta lección, aprenderá lo siguiente:

- ¿Cómo tooinstall Git y Node.js.
  - Git es un sistema de control de versiones distribuido de código abierto. aplicación de ejemplo de Hola en esta lección se almacena en Git.
  - Node.js es un entorno en tiempo de ejecución de JavaScript con un amplio ecosistema de paquetes.
- Cómo las herramientas de desarrollo toouse NPM tooinstall Node.js.
  - Hola mínima versión requerida del Node.js es 4.5 LTS.
  - NPM es uno de los administradores de paquetes de saludo para Node.js.
- Cómo tooinstall código Visual Studio.
  - Visual Studio Code es un editor de código fuente multiplataforma ligero pero eficaz para Windows, Linux y macOS. Ofrece un elevado nivel de compatibilidad para la depuración, control de Git insertado, resaltado de sintaxis, función inteligente de autocompletar código, fragmentos de código y refactorización de código.
- ¿Cómo tooinstall Hola CLI de Azure
  - Hola CLI de Azure proporciona una experiencia de línea de comandos multiplataforma de Azure. Puede trabaja directamente desde una línea de comandos tooprovision y administrar recursos.
- ¿Cómo toouse Hola toocreate de CLI de Azure de un centro de IoT.

## <a name="what-you-need"></a>Lo que necesita

- Un toodownload de conexión de Internet Hola herramientas y software.
- Un equipo que ejecute Ubuntu 16.04 o posterior

## <a name="install-git-and-nodejs"></a>Instalación de Git y Node.js

tooinstall Git y Node.js, siga estos pasos:

1. Presione `Ctrl + Alt + T` tooopen un terminal.
2. Ejecute hello siguientes comandos:

   ```bash
   sudo apt-get update
   curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
   sudo apt-get install -y nodejs
   sudo apt-get install git
   ```

## <a name="install-nodejs-development-tools"></a>Instalación de herramientas de desarrollo de Node.js

Usa [gulp.js](http://gulpjs.com/) tooautomate implementación y ejecución de secuencias de comandos.

gulp tooinstall, ejecute hello siguiente comando en terminal hello:

```bash
sudo npm install -g gulp
```

Si experimenta problemas con la instalación de hello, vea Hola [Guía de solución de problemas](iot-hub-gateway-kit-c-sim-troubleshooting.md) para soluciones toocommon problemas.

> [!Note]
> Nodo, NPM y Gulp son scripts de automatización necesarios toorun desarrollados en Node.js.

## <a name="install-hello-azure-cli"></a>Instalar Hola CLI de Azure

Hola tooinstall CLI de Azure, siga estos pasos:

1. Ejecute hello siga los comandos de terminal de hello:

   ```bash
   sudo apt-get update
   sudo apt-get install -y libssl-dev libffi-dev
   sudo apt-get install -y python-dev
   sudo apt-get install -y build-essential
   sudo apt-get install -y python-pip
   sudo pip install --upgrade azure-cli
   sudo pip install --upgrade azure-cli-iot
   ```

   instalación de Hello puede tardar 5 minutos.

2. Comprobar la instalación de hello ejecutando Hola siguiente comando:

   ```bash
   az iot -h
   ```
Debería ver la siguiente Hola de salida si la instalación de hello es correcta.
![Verificación de la instalación de la CLI de Azure](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_ubuntu.png)

### <a name="install-visual-studio-code"></a>Instalación de Visual Studio Code

Usar código de Visual Studio posteriormente en archivos de configuración del tutorial tooedit Hola.

[Descargue](https://code.visualstudio.com/docs/setup/linux) e instale Visual Studio Code.

## <a name="summary"></a>Resumen

Ha instalado todas las herramientas de hello necesario y el software en el equipo host. La siguiente tarea es toouse hello Azure CLI toocreate un centro de IoT y registrar el dispositivo en el centro de IoT.

## <a name="next-steps"></a>Pasos siguientes
[Creación de una instancia de IoT Hub y registro del dispositivo](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)
