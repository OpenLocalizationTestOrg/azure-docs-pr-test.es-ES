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
# <a name="get-hello-tools-ubuntu-1604"></a><span data-ttu-id="5c77f-104">Obtener herramientas de hello (Ubuntu 16.04)</span><span class="sxs-lookup"><span data-stu-id="5c77f-104">Get hello tools (Ubuntu 16.04)</span></span>

> [!div class="op_single_selector"]
> * <span data-ttu-id="5c77f-105">[Windows 7 o posterior][windows]</span><span class="sxs-lookup"><span data-stu-id="5c77f-105">[Windows 7 or later][windows]</span></span>
> * <span data-ttu-id="5c77f-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="5c77f-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="5c77f-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="5c77f-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="5c77f-108">Lo que hará</span><span class="sxs-lookup"><span data-stu-id="5c77f-108">What you will do</span></span>
<span data-ttu-id="5c77f-109">Descargar herramientas de desarrollo de Hola y el software de hello para la primera aplicación de ejemplo Hola para su Edison de Intel.</span><span class="sxs-lookup"><span data-stu-id="5c77f-109">Download hello development tools and hello software for hello first sample application for your Intel Edison.</span></span> <span data-ttu-id="5c77f-110">Si tiene problemas, buscar soluciones en hello [solución de problemas de página][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="5c77f-110">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="5c77f-111">Lo qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="5c77f-111">What you will learn</span></span>
<span data-ttu-id="5c77f-112">En este artículo, aprenderá lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="5c77f-112">In this article, you will learn:</span></span>

* <span data-ttu-id="5c77f-113">¿Cómo tooinstall Git y Node.js</span><span class="sxs-lookup"><span data-stu-id="5c77f-113">How tooinstall Git and Node.js</span></span>
  * <span data-ttu-id="5c77f-114">[Git](https://git-scm.com) es un sistema de control de versiones distribuido de código.</span><span class="sxs-lookup"><span data-stu-id="5c77f-114">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="5c77f-115">aplicación de ejemplo de Hola para este artículo se almacena en Git.</span><span class="sxs-lookup"><span data-stu-id="5c77f-115">hello sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="5c77f-116">[Node.js](https://nodejs.org/en/) es un entorno de tiempo de ejecución de JavaScript con un amplio ecosistema de paquetes.</span><span class="sxs-lookup"><span data-stu-id="5c77f-116">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="5c77f-117">¿Cómo toouse NPM tooinstall adicionales Node.js las herramientas de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="5c77f-117">How toouse NPM tooinstall additional Node.js development tools.</span></span>
  * <span data-ttu-id="5c77f-118">Hola mínima versión requerida del Node.js es 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="5c77f-118">hello minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="5c77f-119">[NPM](https://www.npmjs.com) es uno de hello administradores de paquetes para Node.js.</span><span class="sxs-lookup"><span data-stu-id="5c77f-119">[NPM](https://www.npmjs.com) is one of hello package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="5c77f-120">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="5c77f-120">What you need</span></span>
<span data-ttu-id="5c77f-121">toocomplete esta operación, debe:</span><span class="sxs-lookup"><span data-stu-id="5c77f-121">toocomplete this operation, you will need:</span></span>
* <span data-ttu-id="5c77f-122">Un toodownload de conexión de Internet Hola herramientas de desarrollo y Hola software.</span><span class="sxs-lookup"><span data-stu-id="5c77f-122">An Internet connection toodownload hello development tools and hello software.</span></span>
* <span data-ttu-id="5c77f-123">Un equipo que ejecute Ubuntu 16.04 o posterior</span><span class="sxs-lookup"><span data-stu-id="5c77f-123">A computer that is running Ubuntu 16.04 or later.</span></span>

## <a name="install-git-nodejs-and-npm"></a><span data-ttu-id="5c77f-124">Instalación de Git, Node.js y NPM</span><span class="sxs-lookup"><span data-stu-id="5c77f-124">Install Git, Node.js, and NPM</span></span>
<span data-ttu-id="5c77f-125">Método abreviado de teclado de uso hello `Ctrl + Alt + T` tooopen un Hola de terminal y se ejecutan después de comandos:</span><span class="sxs-lookup"><span data-stu-id="5c77f-125">Use hello keyboard shortcut `Ctrl + Alt + T` tooopen a terminal and run hello following commands:</span></span>

```bash
sudo apt-get update
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
sudo apt-get install -y nodejs
sudo apt-get install git
```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="5c77f-126">Instalación de herramientas de desarrollo de Node.js adicionales</span><span class="sxs-lookup"><span data-stu-id="5c77f-126">Install additional Node.js development tools</span></span>
<span data-ttu-id="5c77f-127">Use [gulp.js](http://gulpjs.com) implementación de hello tooautomate de tooEdison de aplicación de ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="5c77f-127">Use [gulp.js](http://gulpjs.com) tooautomate hello deployment of hello sample application tooEdison.</span></span>

<span data-ttu-id="5c77f-128">Instalar `gulp` ejecutando Hola siguiente comando en terminal hello:</span><span class="sxs-lookup"><span data-stu-id="5c77f-128">Install `gulp` by running hello following command in hello terminal:</span></span>

```bash
sudo npm install -g gulp
```

<span data-ttu-id="5c77f-129">Si experimenta problemas de instalación de Node.js y estas herramientas de desarrollo adicional en Ubuntu, vea hello [Guía de solución de problemas] [ troubleshooting] para soluciones toocommon problemas.</span><span class="sxs-lookup"><span data-stu-id="5c77f-129">If you experience issues installing Node.js and these additional development tools on Ubuntu, see hello [troubleshooting guide][troubleshooting] for solutions toocommon problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="5c77f-130">Instalación de Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="5c77f-130">Install Visual Studio Code</span></span>
<span data-ttu-id="5c77f-131">[Descargue](https://code.visualstudio.com/docs/setup/linux) e instale Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="5c77f-131">[Download](https://code.visualstudio.com/docs/setup/linux) and install Visual Studio Code.</span></span> <span data-ttu-id="5c77f-132">Visual Studio Code es un editor de código fuente ligero pero eficaz para Windows, Linux y Mac OS.</span><span class="sxs-lookup"><span data-stu-id="5c77f-132">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="5c77f-133">Utilice este editor más adelante en el código de ejemplo de Hola tooedit tutorial Hola.</span><span class="sxs-lookup"><span data-stu-id="5c77f-133">You use this editor later in hello tutorial tooedit hello sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="5c77f-134">Resumen</span><span class="sxs-lookup"><span data-stu-id="5c77f-134">Summary</span></span>
<span data-ttu-id="5c77f-135">Ha instalado herramientas de desarrollo de hello necesario y software para la primera aplicación de ejemplo Hola.</span><span class="sxs-lookup"><span data-stu-id="5c77f-135">You've installed hello required development tools and software for hello first sample application.</span></span> <span data-ttu-id="5c77f-136">Hola siguiente tarea es toocreate, implementar y ejecutar la aplicación de ejemplo de Hola en Edison.</span><span class="sxs-lookup"><span data-stu-id="5c77f-136">hello next task is toocreate, deploy, and run hello sample application on Edison.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5c77f-137">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5c77f-137">Next steps</span></span>
<span data-ttu-id="5c77f-138">[Crear e implementar la aplicación de ejemplo de Hola parpadeo][create-and-deploy-the-blink-application]</span><span class="sxs-lookup"><span data-stu-id="5c77f-138">[Create and deploy hello blink sample application][create-and-deploy-the-blink-application]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[create-and-deploy-the-blink-application]: iot-hub-intel-edison-kit-node-lesson1-deploy-blink-app.md
[windows]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-mac.md
