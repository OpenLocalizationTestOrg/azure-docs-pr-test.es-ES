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
# <a name="get-hello-tools-ubuntu-1604"></a><span data-ttu-id="989b0-104">Obtener herramientas de hello (Ubuntu 16.04)</span><span class="sxs-lookup"><span data-stu-id="989b0-104">Get hello tools (Ubuntu 16.04)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="989b0-105">Windows 7 o posterior</span><span class="sxs-lookup"><span data-stu-id="989b0-105">Windows 7 or later</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-win32.md)
> * [<span data-ttu-id="989b0-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="989b0-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="989b0-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="989b0-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-mac.md)


## <a name="what-you-will-do"></a><span data-ttu-id="989b0-108">Lo que hará</span><span class="sxs-lookup"><span data-stu-id="989b0-108">What you will do</span></span>
<span data-ttu-id="989b0-109">Descargar herramientas de desarrollo de Hola y el software de hello para la primera aplicación de ejemplo hello de frambuesa Pi 3.</span><span class="sxs-lookup"><span data-stu-id="989b0-109">Download hello development tools and hello software for hello first sample application for Raspberry Pi 3.</span></span> <span data-ttu-id="989b0-110">Si tiene problemas, buscar soluciones en hello [página solución de problemas](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="989b0-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="989b0-111">Lo qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="989b0-111">What you will learn</span></span>
<span data-ttu-id="989b0-112">En este artículo, aprenderá lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="989b0-112">In this article, you will learn:</span></span>

* <span data-ttu-id="989b0-113">¿Cómo tooinstall Git y Node.js.</span><span class="sxs-lookup"><span data-stu-id="989b0-113">How tooinstall Git and Node.js.</span></span>
  * <span data-ttu-id="989b0-114">[Git](https://git-scm.com) es un sistema de control de versiones distribuido de código.</span><span class="sxs-lookup"><span data-stu-id="989b0-114">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="989b0-115">aplicación de ejemplo de Hola para este artículo se almacena en Git.</span><span class="sxs-lookup"><span data-stu-id="989b0-115">hello sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="989b0-116">[Node.js](https://nodejs.org/en/) es un entorno de tiempo de ejecución de JavaScript con un amplio ecosistema de paquetes.</span><span class="sxs-lookup"><span data-stu-id="989b0-116">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="989b0-117">¿Cómo toouse NPM tooinstall adicionales Node.js las herramientas de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="989b0-117">How toouse NPM tooinstall additional Node.js development tools.</span></span>
  * <span data-ttu-id="989b0-118">Hola mínima versión requerida del Node.js es 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="989b0-118">hello minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="989b0-119">[NPM](https://www.npmjs.com) es uno de hello administradores de paquetes para Node.js.</span><span class="sxs-lookup"><span data-stu-id="989b0-119">[NPM](https://www.npmjs.com) is one of hello package managers for Node.js.</span></span>

## <a name="what-do-you-need"></a><span data-ttu-id="989b0-120">Qué necesita</span><span class="sxs-lookup"><span data-stu-id="989b0-120">What do you need</span></span>
<span data-ttu-id="989b0-121">toocomplete esta operación, debe:</span><span class="sxs-lookup"><span data-stu-id="989b0-121">toocomplete this operation, you will need:</span></span>

* <span data-ttu-id="989b0-122">Un toodownload de conexión de Internet Hola herramientas de desarrollo y Hola software.</span><span class="sxs-lookup"><span data-stu-id="989b0-122">An Internet connection toodownload hello development tools and hello software.</span></span>
* <span data-ttu-id="989b0-123">Un equipo que ejecute Ubuntu 16.04 o posterior</span><span class="sxs-lookup"><span data-stu-id="989b0-123">A computer that is running Ubuntu 16.04 or later.</span></span>

## <a name="install-git-nodejs-and-npm"></a><span data-ttu-id="989b0-124">Instalación de Git, Node.js y NPM</span><span class="sxs-lookup"><span data-stu-id="989b0-124">Install Git, Node.js, and NPM</span></span>
<span data-ttu-id="989b0-125">Método abreviado de teclado de uso hello `Ctrl + Alt + T` tooopen un Hola de terminal y se ejecutan después de comandos:</span><span class="sxs-lookup"><span data-stu-id="989b0-125">Use hello keyboard shortcut `Ctrl + Alt + T` tooopen a terminal and run hello following commands:</span></span>

```bash
sudo apt-get update
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
sudo apt-get install -y nodejs
sudo apt-get install git
```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="989b0-126">Instalación de herramientas de desarrollo de Node.js adicionales</span><span class="sxs-lookup"><span data-stu-id="989b0-126">Install additional Node.js development tools</span></span>
<span data-ttu-id="989b0-127">Usa [gulp.js](http://gulpjs.com) implementación de hello tooautomate de tooPi de aplicación de ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="989b0-127">You use [gulp.js](http://gulpjs.com) tooautomate hello deployment of hello sample application tooPi.</span></span> <span data-ttu-id="989b0-128">También usar hello [cli de detección de dispositivo](https://github.com/Azure/device-discovery-cli) tooretrieve información de red acerca de los dispositivos de IoT.</span><span class="sxs-lookup"><span data-stu-id="989b0-128">You also use hello [device-discovery-cli](https://github.com/Azure/device-discovery-cli) tooretrieve network information about your IoT devices.</span></span>

<span data-ttu-id="989b0-129">Instalar `gulp` y `device-discovery-cli` ejecutando Hola siguiente comando en terminal hello:</span><span class="sxs-lookup"><span data-stu-id="989b0-129">Install `gulp` and `device-discovery-cli` by running hello following command in hello terminal:</span></span>

```bash
sudo npm install -g device-discovery-cli gulp
```

<span data-ttu-id="989b0-130">Si experimenta problemas de instalación de Node.js y estas herramientas de desarrollo adicional en Ubuntu, vea hello [Guía de solución de problemas](iot-hub-raspberry-pi-kit-node-troubleshooting.md) para soluciones toocommon problemas.</span><span class="sxs-lookup"><span data-stu-id="989b0-130">If you experience issues installing Node.js and these additional development tools on Ubuntu, see hello [troubleshooting guide](iot-hub-raspberry-pi-kit-node-troubleshooting.md) for solutions toocommon problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="989b0-131">Instalación de Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="989b0-131">Install Visual Studio Code</span></span>
<span data-ttu-id="989b0-132">[Descargue](https://code.visualstudio.com/docs/setup/linux) e instale Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="989b0-132">[Download](https://code.visualstudio.com/docs/setup/linux) and install Visual Studio Code.</span></span> <span data-ttu-id="989b0-133">Visual Studio Code es un editor de código fuente ligero pero eficaz para Windows, Linux y Mac OS.</span><span class="sxs-lookup"><span data-stu-id="989b0-133">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="989b0-134">Utilice este editor más adelante en el código de ejemplo de Hola tooedit tutorial Hola.</span><span class="sxs-lookup"><span data-stu-id="989b0-134">You use this editor later in hello tutorial tooedit hello sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="989b0-135">Resumen</span><span class="sxs-lookup"><span data-stu-id="989b0-135">Summary</span></span>
<span data-ttu-id="989b0-136">Ha instalado herramientas de desarrollo de hello necesario y software para la primera aplicación de ejemplo Hola.</span><span class="sxs-lookup"><span data-stu-id="989b0-136">You've installed hello required development tools and software for hello first sample application.</span></span> <span data-ttu-id="989b0-137">Hola siguiente tarea es toocreate, implementar y ejecutar la aplicación de ejemplo de Hola en Pi.</span><span class="sxs-lookup"><span data-stu-id="989b0-137">hello next task is toocreate, deploy, and run hello sample application on Pi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="989b0-138">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="989b0-138">Next steps</span></span>
[<span data-ttu-id="989b0-139">Crear e implementar la aplicación de ejemplo de Hola parpadeo</span><span class="sxs-lookup"><span data-stu-id="989b0-139">Create and deploy hello blink sample application</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-deploy-blink-app.md)

