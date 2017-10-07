---
title: "Conectar frambuesa Pi (nodo) tooAzure IoT - lección 1: obtener herramientas (macOS) | Documentos de Microsoft"
description: "Descargue e instale las herramientas que necesitan Hola y el software para la primera aplicación de ejemplo hello de Pi en macOS."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "desarrollo de iot, software de iot, software de internet de las cosas, instalar python mac, instalar git en mac, ejecución de gulp, instalar node js mac"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 2ea6d211-c0e8-4ade-ac69-d1c2261d78c4
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 382b066cb7ece7ffdeb22b162b725727b22e5fac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-macos-1010"></a><span data-ttu-id="85c47-104">Obtener herramientas de hello (macOS 10.10)</span><span class="sxs-lookup"><span data-stu-id="85c47-104">Get hello tools (macOS 10.10)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="85c47-105">Windows 7 o posterior</span><span class="sxs-lookup"><span data-stu-id="85c47-105">Windows 7 or later</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-win32.md)
> * [<span data-ttu-id="85c47-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="85c47-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="85c47-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="85c47-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="85c47-108">Lo que hará</span><span class="sxs-lookup"><span data-stu-id="85c47-108">What you will do</span></span>
<span data-ttu-id="85c47-109">Descargar herramientas de desarrollo de Hola y el software de hello para la primera aplicación de ejemplo hello para el 3 de frambuesa Pi.</span><span class="sxs-lookup"><span data-stu-id="85c47-109">Download hello development tools and hello software for hello first sample application for your Raspberry Pi 3.</span></span> <span data-ttu-id="85c47-110">Si tiene problemas, buscar soluciones en hello [página solución de problemas](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="85c47-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="85c47-111">Lo qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="85c47-111">What you will learn</span></span>
<span data-ttu-id="85c47-112">En este artículo, aprenderá lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="85c47-112">In this article, you will learn:</span></span>

* <span data-ttu-id="85c47-113">¿Cómo tooinstall Git y Node.js.</span><span class="sxs-lookup"><span data-stu-id="85c47-113">How tooinstall Git and Node.js.</span></span>
  * <span data-ttu-id="85c47-114">[Git](https://git-scm.com) es un sistema de control de versiones distribuido de código.</span><span class="sxs-lookup"><span data-stu-id="85c47-114">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="85c47-115">aplicación de ejemplo de Hola para este artículo se almacena en Git.</span><span class="sxs-lookup"><span data-stu-id="85c47-115">hello sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="85c47-116">[Node.js](https://nodejs.org/en/) es un entorno de tiempo de ejecución de JavaScript con un amplio ecosistema de paquetes.</span><span class="sxs-lookup"><span data-stu-id="85c47-116">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="85c47-117">¿Cómo toouse NPM tooinstall adicionales Node.js las herramientas de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="85c47-117">How toouse NPM tooinstall additional Node.js development tools.</span></span>
  * <span data-ttu-id="85c47-118">Hola mínima versión requerida del Node.js es 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="85c47-118">hello minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="85c47-119">[NPM](https://www.npmjs.com) es uno de hello administradores de paquetes para Node.js.</span><span class="sxs-lookup"><span data-stu-id="85c47-119">[NPM](https://www.npmjs.com) is one of hello package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="85c47-120">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="85c47-120">What you need</span></span>
<span data-ttu-id="85c47-121">toocomplete esta operación, debe:</span><span class="sxs-lookup"><span data-stu-id="85c47-121">toocomplete this operation, you will need:</span></span>

* <span data-ttu-id="85c47-122">Un toodownload de conexión de Internet Hola herramientas de desarrollo y Hola software.</span><span class="sxs-lookup"><span data-stu-id="85c47-122">An Internet connection toodownload hello development tools and hello software.</span></span>
* <span data-ttu-id="85c47-123">Un equipo Mac que ejecute macOS Yosemite (10.10) o posterior</span><span class="sxs-lookup"><span data-stu-id="85c47-123">A Mac that is running macOS Yosemite (10.10) or later.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="85c47-124">Instalación de Git y Node.js</span><span class="sxs-lookup"><span data-stu-id="85c47-124">Install Git and Node.js</span></span>
<span data-ttu-id="85c47-125">tooinstall Git y Node.js, usar hello [Homebrew](http://brew.sh) utilidad de administración del paquete, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="85c47-125">tooinstall Git and Node.js, use hello [Homebrew](http://brew.sh) package management utility by following these steps:</span></span>

1. <span data-ttu-id="85c47-126">Instale Homebrew.</span><span class="sxs-lookup"><span data-stu-id="85c47-126">Install Homebrew.</span></span> <span data-ttu-id="85c47-127">Si ya ha instalado Homebrew, vaya toostep 2.</span><span class="sxs-lookup"><span data-stu-id="85c47-127">If you've already installed Homebrew, go toostep 2.</span></span>
   
   1. <span data-ttu-id="85c47-128">Presione `Cmd + Space` y escriba `Terminal` tooopen un terminal.</span><span class="sxs-lookup"><span data-stu-id="85c47-128">Press `Cmd + Space` and enter `Terminal` tooopen a terminal.</span></span>
   2. <span data-ttu-id="85c47-129">Ejecute el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="85c47-129">Run hello following command:</span></span>
      
      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```
2. <span data-ttu-id="85c47-130">Instale Git y Node.js con hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="85c47-130">Install Git and Node.js by running hello following command:</span></span>
   
   ```bash
   brew install node git
   ```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="85c47-131">Instalación de herramientas de desarrollo de Node.js adicionales</span><span class="sxs-lookup"><span data-stu-id="85c47-131">Install additional Node.js development tools</span></span>
<span data-ttu-id="85c47-132">Use [gulp.js](http://gulpjs.com) implementación de hello tooautomate de tooPi de aplicación de ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="85c47-132">Use [gulp.js](http://gulpjs.com) tooautomate hello deployment of hello sample application tooPi.</span></span> <span data-ttu-id="85c47-133">Hola de uso [cli de detección de dispositivo](https://github.com/Azure/device-discovery-cli) tooretrieve información de red acerca de los dispositivos de IoT.</span><span class="sxs-lookup"><span data-stu-id="85c47-133">Use hello [device-discovery-cli](https://github.com/Azure/device-discovery-cli) tooretrieve network information about your IoT devices.</span></span>

<span data-ttu-id="85c47-134">Instalar `gulp` y `device-discovery-cli` ejecutando Hola siguiente comando en terminal hello:</span><span class="sxs-lookup"><span data-stu-id="85c47-134">Install `gulp` and `device-discovery-cli` by running hello following command in hello terminal:</span></span>

```bash
npm install -g device-discovery-cli gulp
```

<span data-ttu-id="85c47-135">Si experimenta problemas de instalación de Node.js y estas herramientas de desarrollo adicional en macOS, vea hello [Guía de solución de problemas](iot-hub-raspberry-pi-kit-node-troubleshooting.md) para soluciones toocommon problemas.</span><span class="sxs-lookup"><span data-stu-id="85c47-135">If you experience issues installing Node.js and these additional development tools on macOS, see hello [troubleshooting guide](iot-hub-raspberry-pi-kit-node-troubleshooting.md) for solutions toocommon problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="85c47-136">Instalación de Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="85c47-136">Install Visual Studio Code</span></span>
<span data-ttu-id="85c47-137">[Descargue](https://code.visualstudio.com/docs/setup/osx) e instale Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="85c47-137">[Download](https://code.visualstudio.com/docs/setup/osx) and install Visual Studio Code.</span></span> <span data-ttu-id="85c47-138">Visual Studio Code es un editor de código fuente ligero pero eficaz para Windows, Linux y Mac OS.</span><span class="sxs-lookup"><span data-stu-id="85c47-138">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="85c47-139">Utilice este editor más adelante en el código de ejemplo de Hola tooedit tutorial Hola.</span><span class="sxs-lookup"><span data-stu-id="85c47-139">You use this editor later in hello tutorial tooedit hello sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="85c47-140">Resumen</span><span class="sxs-lookup"><span data-stu-id="85c47-140">Summary</span></span>
<span data-ttu-id="85c47-141">Ha instalado herramientas de desarrollo de hello necesario y software para la primera aplicación de ejemplo Hola.</span><span class="sxs-lookup"><span data-stu-id="85c47-141">You've installed hello required development tools and software for hello first sample application.</span></span> <span data-ttu-id="85c47-142">Hola siguiente tarea es toocreate, implementar y ejecutar la aplicación de ejemplo de Hola en Pi.</span><span class="sxs-lookup"><span data-stu-id="85c47-142">hello next task is toocreate, deploy, and run hello sample application on Pi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="85c47-143">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="85c47-143">Next steps</span></span>
[<span data-ttu-id="85c47-144">Crear e implementar la aplicación de ejemplo de Hola parpadeo</span><span class="sxs-lookup"><span data-stu-id="85c47-144">Create and deploy hello blink sample application</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-deploy-blink-app.md)

