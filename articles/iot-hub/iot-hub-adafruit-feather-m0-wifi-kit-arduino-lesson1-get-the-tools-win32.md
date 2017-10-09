---
title: "Conectar Arduino tooAzure IoT - lección 1: obtener herramientas (Windows) | Documentos de Microsoft"
description: "Descargue e instale las herramientas que necesitan Hola y el software para la primera aplicación de ejemplo Hola para Adafruit compacto M0 Wi-Fi en Windows 7 y versiones posteriores."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: herramientas de desarrollo de Arduino, desarrollo de iot, software de iot, software de internet de las cosas, instalar git en Windows, instalar node js Windows
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 9cfb8cd2-eafb-4ba2-b23e-d94e114ff3a6
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 4dd946da6c84293987e166fd1d17fac117e94e4c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-windows-7-or-later"></a><span data-ttu-id="a2836-104">Obtener herramientas de hello (Windows 7 o posterior)</span><span class="sxs-lookup"><span data-stu-id="a2836-104">Get hello tools (Windows 7 or later)</span></span>

> [!div class="op_single_selector"]
> * <span data-ttu-id="a2836-105">[Windows 7 o posterior][windows]</span><span class="sxs-lookup"><span data-stu-id="a2836-105">[Windows 7 or later][windows]</span></span>
> * <span data-ttu-id="a2836-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="a2836-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="a2836-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="a2836-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="a2836-108">Lo que hará</span><span class="sxs-lookup"><span data-stu-id="a2836-108">What you will do</span></span>

<span data-ttu-id="a2836-109">Descargar herramientas de desarrollo de Hola y el software de hello para la primera aplicación de ejemplo hello para el panel de Adafruit compacto M0 Wi-Fi Arduino.</span><span class="sxs-lookup"><span data-stu-id="a2836-109">Download hello development tools and hello software for hello first sample application for your Adafruit Feather M0 WiFi Arduino board.</span></span>

<span data-ttu-id="a2836-110">Si tiene problemas, buscar soluciones en hello [solución de problemas de página][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="a2836-110">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

> [!NOTE]
> <span data-ttu-id="a2836-111">Aunque hello programming language de la lógica principal de hello es Arduino, Node.js tools se utilizan en hello lecciones toobuild e implementación aplicaciones de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="a2836-111">Although hello programming language of hello main logic is Arduino, Node.js tools are used in hello lessons toobuild and deploy sample applications.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="a2836-112">Lo qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="a2836-112">What you will learn</span></span>
<span data-ttu-id="a2836-113">En este artículo, aprenderá lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="a2836-113">In this article, you will learn:</span></span>

* <span data-ttu-id="a2836-114">¿Cómo tooinstall Git y Node.js.</span><span class="sxs-lookup"><span data-stu-id="a2836-114">How tooinstall Git and Node.js.</span></span>
  * <span data-ttu-id="a2836-115">[Git](https://git-scm.com) es un sistema de control de versiones distribuido de código.</span><span class="sxs-lookup"><span data-stu-id="a2836-115">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="a2836-116">aplicación de ejemplo de Hola para este artículo se almacena en Git.</span><span class="sxs-lookup"><span data-stu-id="a2836-116">hello sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="a2836-117">[Node.js](https://nodejs.org/en/) es un entorno de tiempo de ejecución de JavaScript con un amplio ecosistema de paquetes.</span><span class="sxs-lookup"><span data-stu-id="a2836-117">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="a2836-118">¿Cómo toouse NPM tooinstall adicionales Node.js las herramientas de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="a2836-118">How toouse NPM tooinstall additional Node.js development tools.</span></span>
  * <span data-ttu-id="a2836-119">requisito de versión mínima de Hola de Node.js es 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="a2836-119">hello minimum version requirement of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="a2836-120">[NPM](https://www.npmjs.com) es uno de hello administradores de paquetes para Node.js.</span><span class="sxs-lookup"><span data-stu-id="a2836-120">[NPM](https://www.npmjs.com) is one of hello package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="a2836-121">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="a2836-121">What you need</span></span>

<span data-ttu-id="a2836-122">toocomplete esta operación, debe:</span><span class="sxs-lookup"><span data-stu-id="a2836-122">toocomplete this operation, you will need:</span></span>

* <span data-ttu-id="a2836-123">Un toodownload de conexión de Internet Hola herramientas de desarrollo y Hola software.</span><span class="sxs-lookup"><span data-stu-id="a2836-123">An Internet connection toodownload hello development tools and hello software.</span></span>
* <span data-ttu-id="a2836-124">Un equipo que ejecute Windows</span><span class="sxs-lookup"><span data-stu-id="a2836-124">A computer that is running Windows.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="a2836-125">Instalación de Git y Node.js</span><span class="sxs-lookup"><span data-stu-id="a2836-125">Install Git and Node.js</span></span>

<span data-ttu-id="a2836-126">Haga clic en vínculos de hello toodownload e instale Git y LTS de Node.js para Windows.</span><span class="sxs-lookup"><span data-stu-id="a2836-126">Click hello links below toodownload and install Git and Node.js LTS for Windows.</span></span>

* [<span data-ttu-id="a2836-127">Obtención de Git para Windows</span><span class="sxs-lookup"><span data-stu-id="a2836-127">Get Git for Windows</span></span>](https://git-scm.com/download/win/)
* [<span data-ttu-id="a2836-128">Obtención de Node.js LTS para Windows</span><span class="sxs-lookup"><span data-stu-id="a2836-128">Get Node.js LTS for Windows</span></span>](https://nodejs.org/en/)

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="a2836-129">Instalación de herramientas de desarrollo de Node.js adicionales</span><span class="sxs-lookup"><span data-stu-id="a2836-129">Install additional Node.js development tools</span></span>

<span data-ttu-id="a2836-130">Use [gulp.js](http://gulpjs.com) implementación de hello tooautomate de tooyour de aplicación de ejemplo de Hola Arduino panel.</span><span class="sxs-lookup"><span data-stu-id="a2836-130">Use [gulp.js](http://gulpjs.com) tooautomate hello deployment of hello sample application tooyour Arduino board.</span></span>

<span data-ttu-id="a2836-131">Inicie un símbolo del sistema como administrador.</span><span class="sxs-lookup"><span data-stu-id="a2836-131">Start a command prompt as an administrator.</span></span> <span data-ttu-id="a2836-132">Instalar `gulp`, `device-discovery-cli` ejecutando Hola siguiente comando en terminal hello:</span><span class="sxs-lookup"><span data-stu-id="a2836-132">Install `gulp`, `device-discovery-cli` by running hello following command in hello terminal:</span></span>

```bash
npm install -g gulp device-discovery-cli
```

<span data-ttu-id="a2836-133">Si experimenta problemas de instalación de Node.js y estas otras herramientas de desarrollo de Node.js en el equipo, vea hello [Guía de solución de problemas] [ troubleshooting] para soluciones toocommon problemas.</span><span class="sxs-lookup"><span data-stu-id="a2836-133">If you experience issues installing Node.js and these additional Node.js development tools on your computer, see hello [troubleshooting guide][troubleshooting] for solutions toocommon problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="a2836-134">Instalación de Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="a2836-134">Install Visual Studio Code</span></span>

<span data-ttu-id="a2836-135">[Descargue](https://code.visualstudio.com/docs/setup/windows) e instale Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="a2836-135">[Download](https://code.visualstudio.com/docs/setup/windows) and install Visual Studio Code.</span></span> <span data-ttu-id="a2836-136">Visual Studio Code es un editor de código fuente ligero pero eficaz para Windows, Linux y Mac OS.</span><span class="sxs-lookup"><span data-stu-id="a2836-136">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="a2836-137">Utilice este editor más adelante en el código de ejemplo de Hola tooedit tutorial Hola.</span><span class="sxs-lookup"><span data-stu-id="a2836-137">You use this editor later in hello tutorial tooedit hello sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="a2836-138">Resumen</span><span class="sxs-lookup"><span data-stu-id="a2836-138">Summary</span></span>

<span data-ttu-id="a2836-139">Ha instalado herramientas de desarrollo de hello necesario y software para la primera aplicación de ejemplo Hola.</span><span class="sxs-lookup"><span data-stu-id="a2836-139">You've installed hello required development tools and software for hello first sample application.</span></span> <span data-ttu-id="a2836-140">Hola siguiente tarea es toocreate, implementar y ejecutar la aplicación de ejemplo de Hola en el panel de Arduino.</span><span class="sxs-lookup"><span data-stu-id="a2836-140">hello next task is toocreate, deploy, and run hello sample application on your Arduino board.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a2836-141">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a2836-141">Next steps</span></span>

<span data-ttu-id="a2836-142">[Crear e implementar la aplicación de ejemplo de Hola parpadeo][create-and-deploy-the-blink-sample-application]</span><span class="sxs-lookup"><span data-stu-id="a2836-142">[Create and deploy hello blink sample application][create-and-deploy-the-blink-sample-application]</span></span>
<!-- Images and links -->

[windows]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-win32.md
[ubuntu]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-ubuntu.md
[macos]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-mac.md
[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[create-and-deploy-the-blink-sample-application]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-deploy-blink-app.md