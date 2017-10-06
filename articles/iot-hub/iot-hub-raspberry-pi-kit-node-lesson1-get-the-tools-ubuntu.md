---
title: "Conectar frambuesa Pi (nodo) tooAzure IoT - lección 1: obtener herramientas (Ubuntu) | Documentos de Microsoft"
description: "Descargue e instale las herramientas que necesitan Hola y el software para la primera aplicación de ejemplo hello de Pi en Ubuntu."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "desarrollo de iot, software de iot, software de internet de las cosas, instalar git en ubuntu, ejecución de gulp, instalar node js ubuntu"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 4d5e45c0-1db9-4662-a039-99ba26333085
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: b4f566fa0d1faf8b2321707145f675e3d87f0bef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-ubuntu-1604"></a>Obtener herramientas de hello (Ubuntu 16.04)

> [!div class="op_single_selector"]
> * [Windows 7 o posterior](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-win32.md)
> * [Ubuntu 16.04](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-ubuntu.md)
> * [macOS 10.10](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-mac.md)


## <a name="what-you-will-do"></a>Lo que hará
Descargar herramientas de desarrollo de Hola y el software de hello para la primera aplicación de ejemplo hello de frambuesa Pi 3. Si tiene problemas, buscar soluciones en hello [página solución de problemas](iot-hub-raspberry-pi-kit-node-troubleshooting.md).

## <a name="what-you-will-learn"></a>Lo qué aprenderá
En este artículo, aprenderá lo siguiente:

* ¿Cómo tooinstall Git y Node.js.
  * [Git](https://git-scm.com) es un sistema de control de versiones distribuido de código. aplicación de ejemplo de Hola para este artículo se almacena en Git.
  * [Node.js](https://nodejs.org/en/) es un entorno de tiempo de ejecución de JavaScript con un amplio ecosistema de paquetes.
* ¿Cómo toouse NPM tooinstall adicionales Node.js las herramientas de desarrollo.
  * Hola mínima versión requerida del Node.js es 4.5 LTS.
  * [NPM](https://www.npmjs.com) es uno de hello administradores de paquetes para Node.js.

## <a name="what-do-you-need"></a>Qué necesita
toocomplete esta operación, debe:

* Un toodownload de conexión de Internet Hola herramientas de desarrollo y Hola software.
* Un equipo que ejecute Ubuntu 16.04 o posterior

## <a name="install-git-nodejs-and-npm"></a>Instalación de Git, Node.js y NPM
Método abreviado de teclado de uso hello `Ctrl + Alt + T` tooopen un Hola de terminal y se ejecutan después de comandos:

```bash
sudo apt-get update
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
sudo apt-get install -y nodejs
sudo apt-get install git
```

## <a name="install-additional-nodejs-development-tools"></a>Instalación de herramientas de desarrollo de Node.js adicionales
Usa [gulp.js](http://gulpjs.com) implementación de hello tooautomate de tooPi de aplicación de ejemplo de Hola. También usar hello [cli de detección de dispositivo](https://github.com/Azure/device-discovery-cli) tooretrieve información de red acerca de los dispositivos de IoT.

Instalar `gulp` y `device-discovery-cli` ejecutando Hola siguiente comando en terminal hello:

```bash
sudo npm install -g device-discovery-cli gulp
```

Si experimenta problemas de instalación de Node.js y estas herramientas de desarrollo adicional en Ubuntu, vea hello [Guía de solución de problemas](iot-hub-raspberry-pi-kit-node-troubleshooting.md) para soluciones toocommon problemas.

## <a name="install-visual-studio-code"></a>Instalación de Visual Studio Code
[Descargue](https://code.visualstudio.com/docs/setup/linux) e instale Visual Studio Code. Visual Studio Code es un editor de código fuente ligero pero eficaz para Windows, Linux y Mac OS. Utilice este editor más adelante en el código de ejemplo de Hola tooedit tutorial Hola.

## <a name="summary"></a>Resumen
Ha instalado herramientas de desarrollo de hello necesario y software para la primera aplicación de ejemplo Hola. Hola siguiente tarea es toocreate, implementar y ejecutar la aplicación de ejemplo de Hola en Pi.

## <a name="next-steps"></a>Pasos siguientes
[Crear e implementar la aplicación de ejemplo de Hola parpadeo](iot-hub-raspberry-pi-kit-node-lesson1-deploy-blink-app.md)

