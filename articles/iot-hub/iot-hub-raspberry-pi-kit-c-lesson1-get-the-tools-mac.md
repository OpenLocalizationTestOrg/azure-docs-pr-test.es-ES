---
title: "Connect Raspberry PI (C) tooAzure IoT - lección 1: obtener herramientas (macOS) | Documentos de Microsoft"
description: "Descargue e instale las herramientas que necesitan Hola y el software para la primera aplicación de ejemplo hello de Pi en macOS."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "desarrollo de iot, software de iot, software de internet de las cosas, instalar git en mac, ejecución de gulp, instalar node js mac"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: fc6bd2c8-a847-4bf5-818f-6f7f9a6835ee
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 68ee44945dd69edcdf61ab3da4c80379c0ef955d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-macos-1010"></a>Obtener herramientas de hello (macOS 10.10)
> [!div class="op_single_selector"]
> * [Windows 7 o posterior](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)
> * [Ubuntu 16.04](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-ubuntu.md)
> * [macOS 10.10](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-mac.md)

## <a name="what-you-will-do"></a>Lo que hará
Descargar herramientas de desarrollo de Hola y el software de hello para la primera aplicación de ejemplo hello para el 3 de frambuesa Pi. Si tiene problemas, buscar soluciones en hello [página solución de problemas](iot-hub-raspberry-pi-kit-c-troubleshooting.md).

> [!NOTE]
> Aunque hello programming language de la lógica principal de hello es C, herramientas de Node.js se usan en los dispositivos de toodiscover lecciones hello y compilación e implementación aplicaciones de ejemplo.

## <a name="what-you-will-learn"></a>Lo qué aprenderá
En este artículo, aprenderá lo siguiente:

* ¿Cómo tooinstall Git y Node.js.
  * [Git](https://git-scm.com) es un sistema de control de versiones distribuido de código. aplicación de ejemplo de Hola para este artículo se almacena en Git.
  * [Node.js](https://nodejs.org/en/) es un entorno de tiempo de ejecución de JavaScript con un amplio ecosistema de paquetes.
* ¿Cómo toouse NPM tooinstall adicionales Node.js las herramientas de desarrollo.
  * Hola mínima versión requerida del Node.js es 4.5 LTS.
  * [NPM](https://www.npmjs.com) es uno de hello administradores de paquetes para Node.js.

## <a name="what-you-need"></a>Lo que necesita
toocomplete esta operación, debe:

* Un toodownload de conexión de Internet Hola herramientas de desarrollo y Hola software.
* Un equipo Mac que ejecute macOS Yosemite (10.10) o posterior

## <a name="install-git-and-nodejs"></a>Instalación de Git y Node.js
tooinstall Git y Node.js, usar hello [Homebrew](http://brew.sh) utilidad de administración del paquete, siga estos pasos:

1. Instale Homebrew. Si ya ha instalado Homebrew, vaya toostep 2.
   
   1. Presione `Cmd + Space` y escriba `Terminal` tooopen un terminal.
   2. Ejecute el siguiente comando de hello:
      
      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```
2. Instale Git y Node.js con hello siguiente comando:
   
   ```bash
   brew install node git
   ```

## <a name="install-additional-nodejs-development-tools"></a>Instalación de herramientas de desarrollo de Node.js adicionales
Use [gulp.js](http://gulpjs.com) implementación de hello tooautomate de tooyour de aplicación de ejemplo de Hola Pi. Hola de uso [cli de detección de dispositivo](https://github.com/Azure/device-discovery-cli) tooretrieve información de red acerca de los dispositivos de IoT.

Instalar `gulp` y `device-discovery-cli` ejecutando Hola siguiente comando en terminal hello:

```bash
sudo npm install -g device-discovery-cli gulp
```

Si experimenta problemas de instalación de Node.js y estas herramientas de desarrollo adicional en macOS, vea hello [Guía de solución de problemas](iot-hub-raspberry-pi-kit-c-troubleshooting.md) para soluciones toocommon problemas.

## <a name="install-visual-studio-code"></a>Instalación de Visual Studio Code
[Descargue](https://code.visualstudio.com/docs/setup/osx) e instale Visual Studio Code. Visual Studio Code es un editor de código fuente ligero pero eficaz para Windows, Linux y Mac OS. Utilice este editor más adelante en el código de ejemplo de Hola tooedit tutorial Hola.

## <a name="summary"></a>Resumen
Ha instalado herramientas de desarrollo de hello necesario y software para la primera aplicación de ejemplo Hola. Hola siguiente tarea es toocreate, implementar y ejecutar la aplicación de ejemplo de Hola en Pi.

## <a name="next-steps"></a>Pasos siguientes
[Crear e implementar la aplicación de hello parpadeo](iot-hub-raspberry-pi-kit-c-lesson1-deploy-blink-app.md)

