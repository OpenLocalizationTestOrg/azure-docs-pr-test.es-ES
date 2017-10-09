---
title: "Conectar Intel Edison (nodo) tooAzure IoT - lección 1: obtener herramientas (Ubuntu) | Documentos de Microsoft"
description: "Descargue e instale las herramientas que necesitan Hola y el software para la primera aplicación de ejemplo Hola para Edison en Ubuntu."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: herramientas de desarrollo de Arduino, desarrollo de iot, software de iot, software de internet de las cosas, instalar git en Ubuntu, instalar node js Ubuntu
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: 9ab5b161-7ec5-41a6-9c5f-4456e4882752
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: ad1a48708bd74bcc07d09f105f597f18c3f9d2b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-ubuntu-1604"></a>Obtener herramientas de hello (Ubuntu 16.04)

> [!div class="op_single_selector"]
> * [Windows 7 o posterior][windows]
> * [Ubuntu 16.04][ubuntu]
> * [macOS 10.10][macos]

## <a name="what-you-will-do"></a>Lo que hará
Descargar herramientas de desarrollo de Hola y el software de hello para la primera aplicación de ejemplo Hola para su Edison de Intel. Si tiene problemas, buscar soluciones en hello [solución de problemas de página][troubleshooting].

## <a name="what-you-will-learn"></a>Lo qué aprenderá
En este artículo, aprenderá lo siguiente:

* ¿Cómo tooinstall Git y Node.js
  * [Git](https://git-scm.com) es un sistema de control de versiones distribuido de código. aplicación de ejemplo de Hola para este artículo se almacena en Git.
  * [Node.js](https://nodejs.org/en/) es un entorno de tiempo de ejecución de JavaScript con un amplio ecosistema de paquetes.
* ¿Cómo toouse NPM tooinstall adicionales Node.js las herramientas de desarrollo.
  * Hola mínima versión requerida del Node.js es 4.5 LTS.
  * [NPM](https://www.npmjs.com) es uno de hello administradores de paquetes para Node.js.

## <a name="what-you-need"></a>Lo que necesita
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
Use [gulp.js](http://gulpjs.com) implementación de hello tooautomate de tooEdison de aplicación de ejemplo de Hola.

Instalar `gulp` ejecutando Hola siguiente comando en terminal hello:

```bash
sudo npm install -g gulp
```

Si experimenta problemas de instalación de Node.js y estas herramientas de desarrollo adicional en Ubuntu, vea hello [Guía de solución de problemas] [ troubleshooting] para soluciones toocommon problemas.

## <a name="install-visual-studio-code"></a>Instalación de Visual Studio Code
[Descargue](https://code.visualstudio.com/docs/setup/linux) e instale Visual Studio Code. Visual Studio Code es un editor de código fuente ligero pero eficaz para Windows, Linux y Mac OS. Utilice este editor más adelante en el código de ejemplo de Hola tooedit tutorial Hola.

## <a name="summary"></a>Resumen
Ha instalado herramientas de desarrollo de hello necesario y software para la primera aplicación de ejemplo Hola. Hola siguiente tarea es toocreate, implementar y ejecutar la aplicación de ejemplo de Hola en Edison.

## <a name="next-steps"></a>Pasos siguientes
[Crear e implementar la aplicación de ejemplo de Hola parpadeo][create-and-deploy-the-blink-application]
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[create-and-deploy-the-blink-application]: iot-hub-intel-edison-kit-node-lesson1-deploy-blink-app.md
[windows]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-mac.md
