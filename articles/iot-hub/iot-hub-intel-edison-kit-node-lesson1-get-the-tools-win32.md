---
title: "Conectar Intel Edison (nodo) tooAzure IoT - lección 1: obtener herramientas (Windows) | Documentos de Microsoft"
description: "Descargue e instale las herramientas que necesitan Hola y el software para la primera aplicación de ejemplo Hola para Edison en Windows 7 y versiones posteriores."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: herramientas de desarrollo de Arduino, desarrollo de iot, software de iot, software de internet de las cosas, instalar git en Windows, instalar node js Windows
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: 4164b5a1-5a42-4d8a-9ff6-441e79fcc936
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 933cc585d1b8b0236d76452f5c449ae9f2f3987b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-windows-7-or-later"></a><span data-ttu-id="a922b-104">Obtener herramientas de hello (Windows 7 o posterior)</span><span class="sxs-lookup"><span data-stu-id="a922b-104">Get hello tools (Windows 7 or later)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="a922b-105">[Windows 7 o posterior][windows]</span><span class="sxs-lookup"><span data-stu-id="a922b-105">[Windows 7 or later][windows]</span></span>
> * <span data-ttu-id="a922b-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="a922b-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="a922b-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="a922b-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="a922b-108">Lo que hará</span><span class="sxs-lookup"><span data-stu-id="a922b-108">What you will do</span></span>
<span data-ttu-id="a922b-109">Descargue las herramientas de desarrollo de Hola y el software de hello para la primera aplicación de ejemplo Hola para Edison de Intel.</span><span class="sxs-lookup"><span data-stu-id="a922b-109">Download hello development tools and hello software for hello first sample application for Intel Edison.</span></span> <span data-ttu-id="a922b-110">Si tiene problemas, buscar soluciones en hello [solución de problemas de página][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="a922b-110">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="a922b-111">Lo qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="a922b-111">What you will learn</span></span>
<span data-ttu-id="a922b-112">En este artículo, aprenderá lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="a922b-112">In this article, you will learn:</span></span>

* <span data-ttu-id="a922b-113">¿Cómo tooinstall Git y Node.js.</span><span class="sxs-lookup"><span data-stu-id="a922b-113">How tooinstall Git and Node.js.</span></span>
  * <span data-ttu-id="a922b-114">[Git](https://git-scm.com) es un sistema de control de versiones distribuido de código.</span><span class="sxs-lookup"><span data-stu-id="a922b-114">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="a922b-115">aplicación de ejemplo de Hola para este artículo se almacena en Git.</span><span class="sxs-lookup"><span data-stu-id="a922b-115">hello sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="a922b-116">[Node.js](https://nodejs.org/en/) es un entorno de tiempo de ejecución de JavaScript con un amplio ecosistema de paquetes.</span><span class="sxs-lookup"><span data-stu-id="a922b-116">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="a922b-117">¿Cómo toouse NPM tooinstall adicionales Node.js las herramientas de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="a922b-117">How toouse NPM tooinstall additional Node.js development tools.</span></span>
  * <span data-ttu-id="a922b-118">requisito de versión mínima de Hola de Node.js es 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="a922b-118">hello minimum version requirement of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="a922b-119">[NPM](https://www.npmjs.com) es uno de hello administradores de paquetes para Node.js.</span><span class="sxs-lookup"><span data-stu-id="a922b-119">[NPM](https://www.npmjs.com) is one of hello package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="a922b-120">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="a922b-120">What you need</span></span>

<span data-ttu-id="a922b-121">toocomplete esta operación, debe:</span><span class="sxs-lookup"><span data-stu-id="a922b-121">toocomplete this operation, you will need:</span></span>

* <span data-ttu-id="a922b-122">Un toodownload de conexión de Internet Hola herramientas de desarrollo y Hola software.</span><span class="sxs-lookup"><span data-stu-id="a922b-122">An Internet connection toodownload hello development tools and hello software.</span></span>
* <span data-ttu-id="a922b-123">Un equipo que ejecute Windows</span><span class="sxs-lookup"><span data-stu-id="a922b-123">A computer that is running Windows.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="a922b-124">Instalación de Git y Node.js</span><span class="sxs-lookup"><span data-stu-id="a922b-124">Install Git and Node.js</span></span>

<span data-ttu-id="a922b-125">Haga clic en vínculos de hello toodownload e instale Git y LTS de Node.js para Windows.</span><span class="sxs-lookup"><span data-stu-id="a922b-125">Click hello links below toodownload and install Git and Node.js LTS for Windows.</span></span>

* [<span data-ttu-id="a922b-126">Obtención de Git para Windows</span><span class="sxs-lookup"><span data-stu-id="a922b-126">Get Git for Windows</span></span>](https://git-scm.com/download/win/)
* [<span data-ttu-id="a922b-127">Obtención de Node.js LTS para Windows</span><span class="sxs-lookup"><span data-stu-id="a922b-127">Get Node.js LTS for Windows</span></span>](https://nodejs.org/en/)

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="a922b-128">Instalación de herramientas de desarrollo de Node.js adicionales</span><span class="sxs-lookup"><span data-stu-id="a922b-128">Install additional Node.js development tools</span></span>

<span data-ttu-id="a922b-129">Use [gulp.js](http://gulpjs.com) implementación de hello tooautomate de tooEdison de aplicación de ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="a922b-129">Use [gulp.js](http://gulpjs.com) tooautomate hello deployment of hello sample application tooEdison.</span></span>

<span data-ttu-id="a922b-130">Inicie un símbolo del sistema como administrador.</span><span class="sxs-lookup"><span data-stu-id="a922b-130">Start a command prompt as an administrator.</span></span> <span data-ttu-id="a922b-131">Instalar `gulp` ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="a922b-131">Install `gulp` by running hello following command:</span></span>

```cmd
npm install -g gulp
```

<span data-ttu-id="a922b-132">Si experimenta problemas de instalación de Node.js y estas otras herramientas de desarrollo de Node.js en el equipo, vea hello [Guía de solución de problemas] [ troubleshooting] para soluciones toocommon problemas.</span><span class="sxs-lookup"><span data-stu-id="a922b-132">If you experience issues installing Node.js and these additional Node.js development tools on your computer, see hello [troubleshooting guide][troubleshooting] for solutions toocommon problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="a922b-133">Instalación de Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="a922b-133">Install Visual Studio Code</span></span>

<span data-ttu-id="a922b-134">[Descargue](https://code.visualstudio.com/docs/setup/windows) e instale Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="a922b-134">[Download](https://code.visualstudio.com/docs/setup/windows) and install Visual Studio Code.</span></span> <span data-ttu-id="a922b-135">Visual Studio Code es un editor de código fuente ligero pero eficaz para Windows, Linux y Mac OS.</span><span class="sxs-lookup"><span data-stu-id="a922b-135">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="a922b-136">Utilice este editor más adelante en el código de ejemplo de Hola tooedit tutorial Hola.</span><span class="sxs-lookup"><span data-stu-id="a922b-136">You use this editor later in hello tutorial tooedit hello sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="a922b-137">Resumen</span><span class="sxs-lookup"><span data-stu-id="a922b-137">Summary</span></span>

<span data-ttu-id="a922b-138">Ha instalado herramientas de desarrollo de hello necesario y software para la primera aplicación de ejemplo Hola.</span><span class="sxs-lookup"><span data-stu-id="a922b-138">You've installed hello required development tools and software for hello first sample application.</span></span> <span data-ttu-id="a922b-139">Hola siguiente tarea es toocreate, implementar y ejecutar la aplicación de ejemplo de Hola en Edison.</span><span class="sxs-lookup"><span data-stu-id="a922b-139">hello next task is toocreate, deploy, and run hello sample application on Edison.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a922b-140">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a922b-140">Next steps</span></span>

<span data-ttu-id="a922b-141">[Crear e implementar la aplicación de hello parpadeo][create-and-deploy-the-blink-application]</span><span class="sxs-lookup"><span data-stu-id="a922b-141">[Create and deploy hello blink application][create-and-deploy-the-blink-application]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[create-and-deploy-the-blink-application]: iot-hub-intel-edison-kit-node-lesson1-deploy-blink-app.md
[windows]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-mac.md
