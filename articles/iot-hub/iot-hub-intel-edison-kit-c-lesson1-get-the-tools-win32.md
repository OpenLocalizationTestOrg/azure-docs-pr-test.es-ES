---
title: "Connect Intel Edison (C) tooAzure IoT - lección 1: obtener herramientas (Windows) | Documentos de Microsoft"
description: "Descargue e instale las herramientas que necesitan Hola y el software para la primera aplicación de ejemplo Hola para Edison en Windows 7 y versiones posteriores."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: herramientas de desarrollo de Arduino, desarrollo de iot, software de iot, software de internet de las cosas, instalar git en Windows, instalar node js Windows
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: 7d29a358-544d-4657-a504-5ed9b79c2925
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 64d8684ffcb858845de02276a11cf2b2e5c701a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-windows-7-or-later"></a>Obtener herramientas de hello (Windows 7 o posterior)
> [!div class="op_single_selector"]
> * [Windows 7 o posterior][windows]
> * [Ubuntu 16.04][ubuntu]
> * [macOS 10.10][macos]

## <a name="what-you-will-do"></a>Lo que hará
Descargue las herramientas de desarrollo de Hola y el software de hello para la primera aplicación de ejemplo Hola para Edison de Intel. Si tiene problemas, buscar soluciones en hello [solución de problemas de página][troubleshooting].

> [!NOTE]
> Aunque hello programming language de la lógica principal de hello es C, Node.js tools se utilizan en hello lecciones toobuild e implementación aplicaciones de ejemplo.

## <a name="what-you-will-learn"></a>Lo qué aprenderá
En este artículo, aprenderá lo siguiente:

* ¿Cómo tooinstall Git y Node.js.
  * [Git](https://git-scm.com) es un sistema de control de versiones distribuido de código. aplicación de ejemplo de Hola para este artículo se almacena en Git.
  * [Node.js](https://nodejs.org/en/) es un entorno de tiempo de ejecución de JavaScript con un amplio ecosistema de paquetes.
* ¿Cómo toouse NPM tooinstall adicionales Node.js las herramientas de desarrollo.
  * requisito de versión mínima de Hola de Node.js es 4.5 LTS.
  * [NPM](https://www.npmjs.com) es uno de hello administradores de paquetes para Node.js.

## <a name="what-you-need"></a>Lo que necesita

toocomplete esta operación, debe:

* Un toodownload de conexión de Internet Hola herramientas de desarrollo y Hola software.
* Un equipo que ejecute Windows

## <a name="install-git-and-nodejs"></a>Instalación de Git y Node.js

Haga clic en vínculos de hello toodownload e instale Git y LTS de Node.js para Windows.

* [Obtención de Git para Windows](https://git-scm.com/download/win/)
* [Obtención de Node.js LTS para Windows](https://nodejs.org/en/)

## <a name="install-additional-nodejs-development-tools"></a>Instalación de herramientas de desarrollo de Node.js adicionales

Use [gulp.js](http://gulpjs.com) implementación de hello tooautomate de tooEdison de aplicación de ejemplo de Hola.

Inicie un símbolo del sistema como administrador. Instalar `gulp` ejecutando Hola siguiente comando:

```cmd
npm install -g gulp
```

Si experimenta problemas de instalación de Node.js y estas otras herramientas de desarrollo de Node.js en el equipo, vea hello [Guía de solución de problemas] [ troubleshooting] para soluciones toocommon problemas.

## <a name="install-visual-studio-code"></a>Instalación de Visual Studio Code

[Descargue](https://code.visualstudio.com/docs/setup/windows) e instale Visual Studio Code. Visual Studio Code es un editor de código fuente ligero pero eficaz para Windows, Linux y Mac OS. Utilice este editor más adelante en el código de ejemplo de Hola tooedit tutorial Hola.

## <a name="summary"></a>Resumen

Ha instalado herramientas de desarrollo de hello necesario y software para la primera aplicación de ejemplo Hola. Hola siguiente tarea es toocreate, implementar y ejecutar la aplicación de ejemplo de Hola en Edison.

## <a name="next-steps"></a>Pasos siguientes

[Crear e implementar la aplicación de hello parpadeo][create-and-deploy-the-blink-application]

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[create-and-deploy-the-blink-application]: iot-hub-intel-edison-kit-c-lesson1-deploy-blink-app.md
[windows]: iot-hub-intel-edison-kit-c-lesson1-get-the-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-c-lesson1-get-the-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-c-lesson1-get-the-tools-mac.md
