---
title: "Conexión de Intel Edison (Node) a Azure IoT: Lección 1: Obtención de las herramientas (macOS) | Microsoft Docs"
description: "Descargue e instale las herramientas y el software necesarios para la primera aplicación de ejemplo de Edison en macOS."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: herramientas de desarrollo de Arduino, desarrollo de iot, software de iot, software de internet de las cosas, instalar git en mac, instalar node js mac
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: fb6742be-2825-4524-89f7-8ccb7e7f1de1
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: a5e406f49379e9f2192ee93334ab1dcf9f3e53d4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-macos-1010"></a>Obtención de las herramientas (Mac OS 10.10)
> [!div class="op_single_selector"]
> * [Windows 7 o posterior][windows]
> * [Ubuntu 16.04][ubuntu]
> * [macOS 10.10][macos]

## <a name="what-you-will-do"></a>Lo que hará
Descargue las herramientas de desarrollo y el software para la primera aplicación de ejemplo de Intel Edison. Si tiene problemas, busque soluciones en [esta página][troubleshooting].

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
* Un equipo Mac que ejecute macOS Yosemite (10.10) o posterior

## <a name="install-git-and-nodejs"></a>Instalación de Git y Node.js
Para instalar Git y Node.js, use la utilidad de administración de paquetes [Homebrew](http://brew.sh) siguiendo estos pasos:

1. Instale Homebrew. Si ya ha instalado Homebrew, vaya al paso 2.

   1. Presione `Cmd + Space` y escriba `Terminal` para abrir una ventana de terminal.
   2. Ejecute el siguiente comando:

      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```
2. Instale Git y Node.js ejecutando el comando siguiente:

   ```bash
   brew install node git
   ```

## <a name="install-additional-nodejs-development-tools"></a>Instalación de herramientas de desarrollo de Node.js adicionales
Utilice [gulp.js](http://gulpjs.com) para automatizar la implementación de la aplicación de ejemplo en Edison.

Instale `gulp` ejecutando el comando siguiente en la ventana de terminal:

```bash
sudo npm install -g gulp
```

Si experimenta problemas al instalar Node.js y estas herramientas de desarrollo adicionales en Mac OS, consulte la [Guía de solución de problemas][troubleshooting] para ver soluciones a problemas comunes.

## <a name="install-visual-studio-code"></a>Instalación de Visual Studio Code
[Descargue](https://code.visualstudio.com/docs/setup/osx) e instale Visual Studio Code. Visual Studio Code es un editor de código fuente ligero pero eficaz para Windows, Linux y Mac OS. Use este editor más adelante en el tutorial para editar el código de ejemplo.

## <a name="summary"></a>Resumen
Ha instalado las herramientas de desarrollo y el software necesarios para la primera aplicación de ejemplo. En la siguiente tarea, creará, implementará y ejecutará la aplicación de ejemplo en Edison.

## <a name="next-steps"></a>Pasos siguientes
[Creación e implementación de la aplicación de intermitencia][create-and-deploy-the-blink-application]
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[create-and-deploy-the-blink-application]: iot-hub-intel-edison-kit-node-lesson1-deploy-blink-app.md
[windows]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-mac.md
