---
title: "Connect Raspberry PI (C) tooAzure IoT - lección 1: obtener herramientas (Windows) | Documentos de Microsoft"
description: "Descargue e instale las herramientas que necesitan Hola y el software para la primera aplicación de ejemplo hello de Pi en Windows 7 y versiones posteriores."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "desarrollo de iot, software de iot, software de internet de las cosas, instalar git en Windows, instalar node js Windows, instalación de npm en Windows"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: bd765ddd-65b7-4241-a391-dc77cb3af1c0
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 70ae6d15f9d6af116ff065a79a30d99afc67bffd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-windows-7-or-later"></a><span data-ttu-id="13ca4-104">Obtener herramientas de hello (Windows 7 o posterior)</span><span class="sxs-lookup"><span data-stu-id="13ca4-104">Get hello tools (Windows 7 or later)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="13ca4-105">Windows 7 o posterior</span><span class="sxs-lookup"><span data-stu-id="13ca4-105">Windows 7 or later</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)
> * [<span data-ttu-id="13ca4-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="13ca4-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="13ca4-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="13ca4-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="13ca4-108">Lo que hará</span><span class="sxs-lookup"><span data-stu-id="13ca4-108">What you will do</span></span>
<span data-ttu-id="13ca4-109">Descargar herramientas de desarrollo de Hola y el software de hello para la primera aplicación de ejemplo hello de frambuesa Pi 3.</span><span class="sxs-lookup"><span data-stu-id="13ca4-109">Download hello development tools and hello software for hello first sample application for Raspberry Pi 3.</span></span> <span data-ttu-id="13ca4-110">Si tiene problemas, buscar soluciones en hello [página solución de problemas](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="13ca4-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

> [!NOTE]
> <span data-ttu-id="13ca4-111">Aunque hello programming language de la lógica principal de hello es C, herramientas de Node.js se usan en los dispositivos de toodiscover lecciones hello y compilación e implementación aplicaciones de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="13ca4-111">Although hello programming language of hello main logic is C, Node.js tools are used in hello lessons toodiscover devices, and build and deploy sample applications.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="13ca4-112">Lo qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="13ca4-112">What you will learn</span></span>
<span data-ttu-id="13ca4-113">En este artículo, aprenderá lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="13ca4-113">In this article, you will learn:</span></span>

* <span data-ttu-id="13ca4-114">¿Cómo tooinstall Git y Node.js.</span><span class="sxs-lookup"><span data-stu-id="13ca4-114">How tooinstall Git and Node.js.</span></span>
  * <span data-ttu-id="13ca4-115">[Git](https://git-scm.com) es un sistema de control de versiones distribuido de código.</span><span class="sxs-lookup"><span data-stu-id="13ca4-115">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="13ca4-116">aplicación de ejemplo de Hola para este artículo se almacena en Git.</span><span class="sxs-lookup"><span data-stu-id="13ca4-116">hello sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="13ca4-117">[Node.js](https://nodejs.org/en/) es un entorno de tiempo de ejecución de JavaScript con un amplio ecosistema de paquetes.</span><span class="sxs-lookup"><span data-stu-id="13ca4-117">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="13ca4-118">¿Cómo toouse NPM tooinstall adicionales Node.js las herramientas de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="13ca4-118">How toouse NPM tooinstall additional Node.js development tools.</span></span>
  * <span data-ttu-id="13ca4-119">requisito de versión mínima de Hola de Node.js es 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="13ca4-119">hello minimum version requirement of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="13ca4-120">[NPM](https://www.npmjs.com) es uno de hello administradores de paquetes para Node.js.</span><span class="sxs-lookup"><span data-stu-id="13ca4-120">[NPM](https://www.npmjs.com) is one of hello package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="13ca4-121">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="13ca4-121">What you need</span></span>

<span data-ttu-id="13ca4-122">toocomplete esta operación, debe:</span><span class="sxs-lookup"><span data-stu-id="13ca4-122">toocomplete this operation, you will need:</span></span>

* <span data-ttu-id="13ca4-123">Un toodownload de conexión de Internet Hola herramientas de desarrollo y Hola software.</span><span class="sxs-lookup"><span data-stu-id="13ca4-123">An Internet connection toodownload hello development tools and hello software.</span></span>
* <span data-ttu-id="13ca4-124">Un equipo que ejecute Windows</span><span class="sxs-lookup"><span data-stu-id="13ca4-124">A computer that is running Windows.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="13ca4-125">Instalación de Git y Node.js</span><span class="sxs-lookup"><span data-stu-id="13ca4-125">Install Git and Node.js</span></span>

<span data-ttu-id="13ca4-126">Haga clic en vínculos de hello toodownload e instale Git y LTS de Node.js para Windows.</span><span class="sxs-lookup"><span data-stu-id="13ca4-126">Click hello links below toodownload and install Git and Node.js LTS for Windows.</span></span>

* [<span data-ttu-id="13ca4-127">Obtención de Git para Windows</span><span class="sxs-lookup"><span data-stu-id="13ca4-127">Get Git for Windows</span></span>](https://git-scm.com/download/win/)
* [<span data-ttu-id="13ca4-128">Obtención de Node.js LTS para Windows</span><span class="sxs-lookup"><span data-stu-id="13ca4-128">Get Node.js LTS for Windows</span></span>](https://nodejs.org/en/)

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="13ca4-129">Instalación de herramientas de desarrollo de Node.js adicionales</span><span class="sxs-lookup"><span data-stu-id="13ca4-129">Install additional Node.js development tools</span></span>

<span data-ttu-id="13ca4-130">Use [gulp.js](http://gulpjs.com) implementación de hello tooautomate de tooPi de aplicación de ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="13ca4-130">Use [gulp.js](http://gulpjs.com) tooautomate hello deployment of hello sample application tooPi.</span></span> <span data-ttu-id="13ca4-131">Hola de uso [cli de detección de dispositivo](https://github.com/Azure/device-discovery-cli) tooretrieve información de red acerca de los dispositivos de IoT.</span><span class="sxs-lookup"><span data-stu-id="13ca4-131">Use hello [device-discovery-cli](https://github.com/Azure/device-discovery-cli) tooretrieve network information about your IoT devices.</span></span>

<span data-ttu-id="13ca4-132">Inicie un símbolo del sistema como administrador.</span><span class="sxs-lookup"><span data-stu-id="13ca4-132">Start a command prompt as an administrator.</span></span> <span data-ttu-id="13ca4-133">Instalar `gulp` y `device-discovery-cli` ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="13ca4-133">Install `gulp` and `device-discovery-cli` by running hello following command:</span></span>

```bash
npm install -g device-discovery-cli gulp
```

<span data-ttu-id="13ca4-134">Si experimenta problemas de instalación de Node.js y estas otras herramientas de desarrollo de Node.js en el equipo, vea hello [Guía de solución de problemas](iot-hub-raspberry-pi-kit-c-troubleshooting.md) para soluciones toocommon problemas.</span><span class="sxs-lookup"><span data-stu-id="13ca4-134">If you experience issues installing Node.js and these additional Node.js development tools on your computer, see hello [troubleshooting guide](iot-hub-raspberry-pi-kit-c-troubleshooting.md) for solutions toocommon problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="13ca4-135">Instalación de Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="13ca4-135">Install Visual Studio Code</span></span>

<span data-ttu-id="13ca4-136">[Descargue](https://code.visualstudio.com/docs/setup/windows) e instale Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="13ca4-136">[Download](https://code.visualstudio.com/docs/setup/windows) and install Visual Studio Code.</span></span> <span data-ttu-id="13ca4-137">Visual Studio Code es un editor de código fuente ligero pero eficaz para Windows, Linux y Mac OS.</span><span class="sxs-lookup"><span data-stu-id="13ca4-137">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="13ca4-138">Utilice este editor más adelante en el código de ejemplo de Hola tooedit tutorial Hola.</span><span class="sxs-lookup"><span data-stu-id="13ca4-138">You use this editor later in hello tutorial tooedit hello sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="13ca4-139">Resumen</span><span class="sxs-lookup"><span data-stu-id="13ca4-139">Summary</span></span>

<span data-ttu-id="13ca4-140">Ha instalado herramientas de desarrollo de hello necesario y software para la primera aplicación de ejemplo Hola.</span><span class="sxs-lookup"><span data-stu-id="13ca4-140">You've installed hello required development tools and software for hello first sample application.</span></span> <span data-ttu-id="13ca4-141">Hola siguiente tarea es toocreate, implementar y ejecutar la aplicación de ejemplo de Hola en Pi.</span><span class="sxs-lookup"><span data-stu-id="13ca4-141">hello next task is toocreate, deploy, and run hello sample application on Pi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="13ca4-142">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="13ca4-142">Next steps</span></span>

[<span data-ttu-id="13ca4-143">Crear e implementar la aplicación de hello parpadeo</span><span class="sxs-lookup"><span data-stu-id="13ca4-143">Create and deploy hello blink application</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-deploy-blink-app.md)
