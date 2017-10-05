---
title: "Conexión de Raspberry Pi (C) a Azure IoT: Lección 1: Obtención de las herramientas (Ubuntu) | Microsoft Docs"
description: "Descargue e instale las herramientas y el software necesarios para la primera aplicación de ejemplo de Pi en Ubuntu."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "desarrollo de iot, software de iot, software de internet de las cosas, instalar git en ubuntu, ejecución de gulp, instalar node js ubuntu"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: 32cfea00-c254-4cef-8f6f-bbf807eca6b6
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 28ebba82e90d91470518cd830c96e6da39d8b9b4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-ubuntu-1604"></a>Obtención de las herramientas (Ubuntu 16.04)

> [!div class="op_single_selector"]
> * [Windows 7 o posterior](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)
> * [Ubuntu 16.04](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-ubuntu.md)
> * [macOS 10.10](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-mac.md)

## <a name="what-you-will-do"></a>Lo que hará
Descargue las herramientas de desarrollo y el software para la primera aplicación de ejemplo de Raspberry Pi 3. Si tiene problemas, busque soluciones en la [página de solución de problemas](iot-hub-raspberry-pi-kit-c-troubleshooting.md).

> [!NOTE]
> Aunque el lenguaje de programación de la lógica principal es C, las herramientas de Node.js se usan en las lecciones para detectar dispositivos, compilar e implementar aplicaciones de ejemplo.

## <a name="what-you-will-learn"></a>Lo qué aprenderá
En este artículo, aprenderá lo siguiente:

* Cómo instalar Git y Node.js
  * [Git](https://git-scm.com) es un sistema de control de versiones distribuido de código. La aplicación de ejemplo de este artículo se almacena en Git.
  * [Node.js](https://nodejs.org/en/) es un entorno de tiempo de ejecución de JavaScript con un amplio ecosistema de paquetes.
* Cómo usar NPM para instalar las herramientas de desarrollo de Node.js adicionales.
  * La versión mínima necesaria de Node.js es 4.5 LTS.
  * [NPM](https://www.npmjs.com) es uno de los administradores de paquetes para Node.js.

## <a name="what-you-need"></a>Lo que necesita
Para completar esta operación, necesitará:

* Una conexión a Internet para descargar el software y las herramientas de desarrollo necesarias
* Un equipo que ejecute Ubuntu 16.04 o posterior

## <a name="install-git-nodejs-and-npm"></a>Instalación de Git, Node.js y NPM
Utilice el método abreviado de teclado `Ctrl + Alt + T` para abrir una ventana de terminal y ejecute los siguientes comandos:

```bash
sudo apt-get update
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
sudo apt-get install -y nodejs
sudo apt-get install git
```

## <a name="install-additional-nodejs-development-tools"></a>Instalación de herramientas de desarrollo de Node.js adicionales
Utilice [gulp.js](http://gulpjs.com) para automatizar la implementación de la aplicación de ejemplo en Pi. Utilice [device-discovery-cli](https://github.com/Azure/device-discovery-cli) para recuperar información de la red de los dispositivos de IoT.

Instale `gulp` y `device-discovery-cli` ejecutando el comando siguiente en la ventana de terminal:

```bash
sudo npm install -g device-discovery-cli gulp
```

Si experimenta problemas al instalar Node.js y estas herramientas de desarrollo adicionales en Ubuntu, consulte la [Guía de solución de problemas](iot-hub-raspberry-pi-kit-c-troubleshooting.md) para ver soluciones a problemas comunes.

## <a name="install-visual-studio-code"></a>Instalación de Visual Studio Code
[Descargue](https://code.visualstudio.com/docs/setup/linux) e instale Visual Studio Code. Visual Studio Code es un editor de código fuente ligero pero eficaz para Windows, Linux y Mac OS. Use este editor más adelante en el tutorial para editar el código de ejemplo.

## <a name="summary"></a>Resumen
Ha instalado las herramientas de desarrollo y el software necesarios para la primera aplicación de ejemplo. En la siguiente tarea, creará, implementará y ejecutará la aplicación de ejemplo en Pi.

## <a name="next-steps"></a>Pasos siguientes
[Creación e implementación de la aplicación de intermitencia](iot-hub-raspberry-pi-kit-c-lesson1-deploy-blink-app.md)

