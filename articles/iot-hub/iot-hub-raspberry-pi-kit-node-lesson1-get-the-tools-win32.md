---
title: "Conectar frambuesa Pi (nodo) tooAzure IoT - lección 1: obtener herramientas (Windows) | Documentos de Microsoft"
description: "Descargue e instale las herramientas que necesitan Hola y el software para la primera aplicación de ejemplo hello de Pi en Windows 7 y versiones posteriores."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "desarrollo de iot, software de iot, software de internet de las cosas, instalar git en windows, ejecución de gulp, instalar node js windows, instalar npm en windows, instalar python en windows"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: b3d88e17-97cc-4f23-85fd-a688fc228eb8
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: ea7f77cc79c70c8c7952b63462b926471fcf71cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-windows-7-or-later"></a><span data-ttu-id="80447-104">Obtener herramientas de hello (Windows 7 o posterior)</span><span class="sxs-lookup"><span data-stu-id="80447-104">Get hello tools (Windows 7 or later)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="80447-105">Windows 7 o posterior</span><span class="sxs-lookup"><span data-stu-id="80447-105">Windows 7 or later</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-win32.md)
> * [<span data-ttu-id="80447-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="80447-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="80447-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="80447-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-mac.md)


## <a name="what-you-will-do"></a><span data-ttu-id="80447-108">Lo que hará</span><span class="sxs-lookup"><span data-stu-id="80447-108">What you will do</span></span>
<span data-ttu-id="80447-109">Descargar herramientas de desarrollo de Hola y el software de hello para la primera aplicación de ejemplo hello de frambuesa Pi 3.</span><span class="sxs-lookup"><span data-stu-id="80447-109">Download hello development tools and hello software for hello first sample application for Raspberry Pi 3.</span></span> <span data-ttu-id="80447-110">Si tiene problemas, buscar soluciones en hello [página solución de problemas](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="80447-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="80447-111">Lo qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="80447-111">What you will learn</span></span>
<span data-ttu-id="80447-112">En este artículo, aprenderá lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="80447-112">In this article, you will learn:</span></span>

* <span data-ttu-id="80447-113">¿Cómo tooinstall Git y Node.js.</span><span class="sxs-lookup"><span data-stu-id="80447-113">How tooinstall Git and Node.js.</span></span>
  * <span data-ttu-id="80447-114">[Git](https://git-scm.com) es un sistema de control de versiones distribuido de código.</span><span class="sxs-lookup"><span data-stu-id="80447-114">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="80447-115">aplicación de ejemplo de Hola para este artículo se almacena en Git.</span><span class="sxs-lookup"><span data-stu-id="80447-115">hello sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="80447-116">[Node.js](https://nodejs.org/en/) es un entorno de tiempo de ejecución de JavaScript con un amplio ecosistema de paquetes.</span><span class="sxs-lookup"><span data-stu-id="80447-116">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="80447-117">¿Cómo toouse NPM tooinstall adicionales Node.js las herramientas de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="80447-117">How toouse NPM tooinstall additional Node.js development tools.</span></span>
  * <span data-ttu-id="80447-118">requisito de versión mínima de Hola de Node.js es 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="80447-118">hello minimum version requirement of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="80447-119">[NPM](https://www.npmjs.com) es uno de hello administradores de paquetes para Node.js.</span><span class="sxs-lookup"><span data-stu-id="80447-119">[NPM](https://www.npmjs.com) is one of hello package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="80447-120">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="80447-120">What you need</span></span>
<span data-ttu-id="80447-121">toocomplete esta operación, debe:</span><span class="sxs-lookup"><span data-stu-id="80447-121">toocomplete this operation, you will need:</span></span>

* <span data-ttu-id="80447-122">Un toodownload de conexión de Internet Hola herramientas de desarrollo y Hola software.</span><span class="sxs-lookup"><span data-stu-id="80447-122">An Internet connection toodownload hello development tools and hello software.</span></span>
* <span data-ttu-id="80447-123">Un equipo que ejecute Windows</span><span class="sxs-lookup"><span data-stu-id="80447-123">A computer that is running Windows.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="80447-124">Instalación de Git y Node.js</span><span class="sxs-lookup"><span data-stu-id="80447-124">Install Git and Node.js</span></span>
<span data-ttu-id="80447-125">Haga clic en hello después toodownload vínculos e instale Git y LTS de Node.js para Windows.</span><span class="sxs-lookup"><span data-stu-id="80447-125">Click hello following links toodownload and install Git and Node.js LTS for Windows.</span></span>

* [<span data-ttu-id="80447-126">Obtención de Git para Windows</span><span class="sxs-lookup"><span data-stu-id="80447-126">Get Git for Windows</span></span>](https://git-scm.com/download/win/)
* [<span data-ttu-id="80447-127">Obtención de Node.js LTS para Windows</span><span class="sxs-lookup"><span data-stu-id="80447-127">Get Node.js LTS for Windows</span></span>](https://nodejs.org/en/)

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="80447-128">Instalación de herramientas de desarrollo de Node.js adicionales</span><span class="sxs-lookup"><span data-stu-id="80447-128">Install additional Node.js development tools</span></span>
<span data-ttu-id="80447-129">Use [gulp.js](http://gulpjs.com) implementación de hello tooautomate de tooPi de aplicación de ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="80447-129">Use [gulp.js](http://gulpjs.com) tooautomate hello deployment of hello sample application tooPi.</span></span> <span data-ttu-id="80447-130">También usar hello [cli de detección de dispositivo](https://github.com/Azure/device-discovery-cli) tooretrieve información de red acerca de los dispositivos de IoT.</span><span class="sxs-lookup"><span data-stu-id="80447-130">You also use hello [device-discovery-cli](https://github.com/Azure/device-discovery-cli) tooretrieve network information about your IoT devices.</span></span>

<span data-ttu-id="80447-131">Inicie un símbolo del sistema como administrador.</span><span class="sxs-lookup"><span data-stu-id="80447-131">Start a command prompt as an administrator.</span></span> <span data-ttu-id="80447-132">Instalar `gulp` y `device-discovery-cli` ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="80447-132">Install `gulp` and `device-discovery-cli` by running hello following command:</span></span>

```bash
npm install -g device-discovery-cli gulp
```

<span data-ttu-id="80447-133">Si experimenta problemas de instalación de Node.js y estas otras herramientas de desarrollo de Node.js en el equipo, vea hello [Guía de solución de problemas](iot-hub-raspberry-pi-kit-node-troubleshooting.md) para soluciones toocommon problemas.</span><span class="sxs-lookup"><span data-stu-id="80447-133">If you experience issues installing Node.js and these additional Node.js development tools on your computer, see hello [troubleshooting guide](iot-hub-raspberry-pi-kit-node-troubleshooting.md) for solutions toocommon problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="80447-134">Instalación de Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="80447-134">Install Visual Studio Code</span></span>
<span data-ttu-id="80447-135">[Descargue](https://code.visualstudio.com/docs/setup/windows) e instale Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="80447-135">[Download](https://code.visualstudio.com/docs/setup/windows) and install Visual Studio Code.</span></span> <span data-ttu-id="80447-136">Visual Studio Code es un editor de código fuente ligero pero eficaz para Windows, Linux y Mac OS.</span><span class="sxs-lookup"><span data-stu-id="80447-136">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="80447-137">Utilice este editor más adelante en el código de ejemplo de Hola tooedit tutorial Hola.</span><span class="sxs-lookup"><span data-stu-id="80447-137">You use this editor later in hello tutorial tooedit hello sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="80447-138">Resumen</span><span class="sxs-lookup"><span data-stu-id="80447-138">Summary</span></span>
<span data-ttu-id="80447-139">Ha instalado herramientas de desarrollo de hello necesario y software para la primera aplicación de ejemplo Hola.</span><span class="sxs-lookup"><span data-stu-id="80447-139">You've installed hello required development tools and software for hello first sample application.</span></span> <span data-ttu-id="80447-140">Hola siguiente tarea es toocreate, implementar y ejecutar la aplicación de ejemplo de Hola en Pi.</span><span class="sxs-lookup"><span data-stu-id="80447-140">hello next task is toocreate, deploy, and run hello sample application on Pi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="80447-141">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="80447-141">Next steps</span></span>
[<span data-ttu-id="80447-142">Crear e implementar la aplicación de ejemplo de Hola parpadeo</span><span class="sxs-lookup"><span data-stu-id="80447-142">Create and deploy hello blink sample application</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-deploy-blink-app.md)

