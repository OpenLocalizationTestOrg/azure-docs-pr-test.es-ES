---
title: "Dispositivo SensorTag y puerta de enlace de Azure IoT: Lección 2: Obtención de las herramientas (macOS) | Microsoft Docs"
description: Instalar las herramientas en el equipo Mac, crear un centro de IoT y registrar el dispositivo en el centro de IoT Hola.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: desarrollo de iot, software de iot, servicio en la nube de iot, software de internet de las cosas, cli de azure, instalar python mac, instalar git en mac, ejecutar gulp, instalar node js mac
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 94e538ef-9857-4023-9c3c-e92a0be7c395
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 44bce452690e18e6c803df564fdafcdda7f41c8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-macos"></a>Obtener herramientas de hello (MacOS)
> [!div class="op_single_selector"]
> * [Windows 7 o posterior](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)
> * [Ubuntu 16.04](iot-hub-gateway-kit-c-lesson2-get-the-tools-ubuntu.md)
> * [macOS 10.10](iot-hub-gateway-kit-c-lesson2-get-the-tools-mac.md)

## <a name="what-you-will-do"></a>Lo que hará

- Instale Git, Node.js, Gulp y Python.
- Instalar hello Azure interfaz de línea de comandos (CLI de Azure). 

Si tiene problemas, buscar soluciones en hello [página solución de problemas](iot-hub-gateway-kit-c-troubleshooting.md).

## <a name="what-you-will-learn"></a>Lo qué aprenderá

En esta lección, aprenderá lo siguiente:

- Cómo tooinstall [Git](https://git-scm.com/) y [Node.js](https://nodejs.org/en/).
  - Git es un sistema de control de versiones distribuido de código abierto. aplicación de ejemplo de Hola en esta lección se almacena en Git.
  - Node.js es un entorno en tiempo de ejecución de JavaScript con un amplio ecosistema de paquetes.
- Cómo toouse [NPM](https://www.npmjs.com/) tooinstall Node.js las herramientas de desarrollo.
  - Hola mínima versión requerida del Node.js es 4.5 LTS.
  - NPM es uno de los administradores de paquetes de saludo para Node.js.
- Cómo tooinstall código Visual Studio.
  - Visual Studio Code es un editor de código fuente multiplataforma ligero pero eficaz para Windows, Linux y macOS. Ofrece un elevado nivel de compatibilidad para la depuración, control de Git insertado, resaltado de sintaxis, función inteligente de autocompletar código, fragmentos de código y refactorización de código.
- ¿Cómo tooinstall Python.
  - Python es un lenguaje de programación general, muy usado, destinado a fines genéricos, interpretado y dinámico.
- ¿Cómo tooinstall Hola CLI de Azure.
  - Hola CLI de Azure proporciona una experiencia de línea de comandos multiplataforma de Azure. Puede trabaja directamente desde una línea de comandos tooprovision y administrar recursos.
- ¿Cómo toouse Hola toocreate de CLI de Azure de un centro de IoT.

## <a name="what-you-need"></a>Lo que necesita

- Un toodownload de conexión de Internet Hola herramientas y software.
- Un equipo Mac con OS X Yosemite (10.10) o posterior.

## <a name="install-git-and-nodejs"></a>Instalación de Git y Node.js

tooinstall Git y Node.js, use la utilidad de administración de paquetes de Homebrew Hola siguiendo estos pasos:

1. [Descargue](http://brew.sh/) e instale Homebrew. Si ya ha instalado Homebrew, vaya toostep 2.
   1. Presione `Cmd + Space` y escriba `Terminal` tooopen un terminal.
   2. Ejecute el siguiente comando de hello:

      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```

2. Instale Git y Node.js con hello siguiente comando:

    ```bash
    brew install node git
    ```

## <a name="install-nodejs-development-tools"></a>Instalación de herramientas de desarrollo de Node.js

Usa [gulp.js](http://gulpjs.com/) tooautomate implementación y ejecución de secuencias de comandos.

gulp tooinstall, ejecute hello siguiente comando en terminal hello:

```bash
npm install -g gulp
```

Si experimenta problemas con la instalación de hello, vea Hola [Guía de solución de problemas](iot-hub-gateway-kit-c-troubleshooting.md) para soluciones toocommon problemas.

> [!Note]
> Nodo, NPM y Gulp son scripts de automatización necesarios toorun desarrollados en Node.js.

## <a name="install-python"></a>Instalación de Python

Aunque Mac OS X incluye Python 2.7 de serie, se recomienda instalar Python mediante Homebrew. Consulte [Installing Python on Mac OS X](http://docs.python-guide.org/en/latest/starting/install/osx/) (Instalación de Python en Mac OS X).

Instalar Python y pip ejecutando Hola siguiente comando:

```bash
brew install python
```

## <a name="install-hello-azure-cli"></a>Instalar Hola CLI de Azure

Hola tooinstall CLI de Azure, siga estos pasos:

1. Ejecute hello siga los comandos de terminal de hello:
   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
   instalación de Hello puede tardar 5 minutos.

2. Comprobar la instalación de hello ejecutando Hola siguiente comando:
   ```bash
   az iot -h
   ```
   Debería ver la siguiente Hola de salida si la instalación de hello es correcta.

   ![Verificación de la instalación de la CLI de Azure](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_osx.png)

## <a name="install-visual-studio-code"></a>Instalación de Visual Studio Code

Usar código de Visual Studio posteriormente en archivos de configuración del tutorial tooedit Hola.

[Descargue](https://code.visualstudio.com/docs/setup/osx) e instale Visual Studio Code.

## <a name="summary"></a>Resumen

Ha instalado todas las herramientas de hello necesario y el software en el equipo Mac. La siguiente tarea es toouse hello Azure CLI toocreate un centro de IoT y registrar el dispositivo en el centro de IoT.

## <a name="next-steps"></a>Pasos siguientes
[Creación de una instancia de IoT Hub y registro del dispositivo](iot-hub-gateway-kit-c-lesson2-register-device.md)
