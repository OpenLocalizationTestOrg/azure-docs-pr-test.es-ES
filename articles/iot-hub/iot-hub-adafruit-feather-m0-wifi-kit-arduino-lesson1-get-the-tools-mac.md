---
title: "Conectar Arduino tooAzure IoT - lección 1: obtener herramientas (macOS) | Documentos de Microsoft"
description: "Descargue e instale las herramientas que necesitan Hola y el software para la primera aplicación de ejemplo Hola para Adafruit compacto M0 Wi-Fi en macOS."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: herramientas de desarrollo de Arduino, desarrollo de iot, software de iot, software de internet de las cosas, instalar git en mac, instalar node js mac
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 0262f3dd-0259-4eb0-962f-9fb534f8359e
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 5fd306fecd7259fb8f1e99d76282a1e464c4d4f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-macos-1010"></a><span data-ttu-id="8575b-104">Obtener herramientas de hello (macOS 10.10)</span><span class="sxs-lookup"><span data-stu-id="8575b-104">Get hello tools (macOS 10.10)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="8575b-105">[Windows 7 o posterior][windows]</span><span class="sxs-lookup"><span data-stu-id="8575b-105">[Windows 7 or later][windows]</span></span>
> * <span data-ttu-id="8575b-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="8575b-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="8575b-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="8575b-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="8575b-108">Lo que hará</span><span class="sxs-lookup"><span data-stu-id="8575b-108">What you will do</span></span>

<span data-ttu-id="8575b-109">Descargar herramientas de desarrollo de Hola y el software de hello para la primera aplicación de ejemplo hello para el panel de Adafruit compacto M0 Wi-Fi Arduino.</span><span class="sxs-lookup"><span data-stu-id="8575b-109">Download hello development tools and hello software for hello first sample application for your Adafruit Feather M0 WiFi Arduino board.</span></span> 

<span data-ttu-id="8575b-110">Si tiene problemas, buscar soluciones en hello [solución de problemas de página][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="8575b-110">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

> [!NOTE]
> <span data-ttu-id="8575b-111">Aunque hello programming language de la lógica principal de hello es Arduino, Node.js tools se utilizan en hello lecciones toobuild e implementación aplicaciones de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="8575b-111">Although hello programming language of hello main logic is Arduino, Node.js tools are used in hello lessons toobuild and deploy sample applications.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="8575b-112">Lo qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="8575b-112">What you will learn</span></span>
<span data-ttu-id="8575b-113">En este artículo, aprenderá lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="8575b-113">In this article, you will learn:</span></span>

* <span data-ttu-id="8575b-114">¿Cómo tooinstall Git y Node.js.</span><span class="sxs-lookup"><span data-stu-id="8575b-114">How tooinstall Git and Node.js.</span></span>
  * <span data-ttu-id="8575b-115">[Git](https://git-scm.com) es un sistema de control de versiones distribuido de código.</span><span class="sxs-lookup"><span data-stu-id="8575b-115">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="8575b-116">aplicación de ejemplo de Hola para este artículo se almacena en Git.</span><span class="sxs-lookup"><span data-stu-id="8575b-116">hello sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="8575b-117">[Node.js](https://nodejs.org/en/) es un entorno de tiempo de ejecución de JavaScript con un amplio ecosistema de paquetes.</span><span class="sxs-lookup"><span data-stu-id="8575b-117">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="8575b-118">¿Cómo toouse NPM tooinstall adicionales Node.js las herramientas de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="8575b-118">How toouse NPM tooinstall additional Node.js development tools.</span></span>
  * <span data-ttu-id="8575b-119">Hola mínima versión requerida del Node.js es 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="8575b-119">hello minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="8575b-120">[NPM](https://www.npmjs.com) es uno de hello administradores de paquetes para Node.js.</span><span class="sxs-lookup"><span data-stu-id="8575b-120">[NPM](https://www.npmjs.com) is one of hello package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="8575b-121">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="8575b-121">What you need</span></span>
<span data-ttu-id="8575b-122">toocomplete esta operación, debe:</span><span class="sxs-lookup"><span data-stu-id="8575b-122">toocomplete this operation, you will need:</span></span>
* <span data-ttu-id="8575b-123">Un toodownload de conexión de Internet Hola herramientas de desarrollo y Hola software.</span><span class="sxs-lookup"><span data-stu-id="8575b-123">An Internet connection toodownload hello development tools and hello software.</span></span>
* <span data-ttu-id="8575b-124">Un equipo Mac que ejecute macOS Yosemite (10.10) o posterior</span><span class="sxs-lookup"><span data-stu-id="8575b-124">A Mac that is running macOS Yosemite (10.10) or later.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="8575b-125">Instalación de Git y Node.js</span><span class="sxs-lookup"><span data-stu-id="8575b-125">Install Git and Node.js</span></span>
<span data-ttu-id="8575b-126">tooinstall Git y Node.js, usar hello [Homebrew](http://brew.sh) utilidad de administración del paquete, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="8575b-126">tooinstall Git and Node.js, use hello [Homebrew](http://brew.sh) package management utility by following these steps:</span></span>

1. <span data-ttu-id="8575b-127">Instale Homebrew.</span><span class="sxs-lookup"><span data-stu-id="8575b-127">Install Homebrew.</span></span> <span data-ttu-id="8575b-128">Si ya ha instalado Homebrew, vaya toostep 2.</span><span class="sxs-lookup"><span data-stu-id="8575b-128">If you've already installed Homebrew, go toostep 2.</span></span>

   1. <span data-ttu-id="8575b-129">Presione `Cmd + Space` y escriba `Terminal` tooopen un terminal.</span><span class="sxs-lookup"><span data-stu-id="8575b-129">Press `Cmd + Space` and enter `Terminal` tooopen a terminal.</span></span>
   2. <span data-ttu-id="8575b-130">Ejecute el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="8575b-130">Run hello following command:</span></span>

      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```
2. <span data-ttu-id="8575b-131">Instale Git y Node.js con hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="8575b-131">Install Git and Node.js by running hello following command:</span></span>

   ```bash
   brew install node git
   ```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="8575b-132">Instalación de herramientas de desarrollo de Node.js adicionales</span><span class="sxs-lookup"><span data-stu-id="8575b-132">Install additional Node.js development tools</span></span>
<span data-ttu-id="8575b-133">Use [gulp.js](http://gulpjs.com) implementación de hello tooautomate de tooyour de aplicación de ejemplo de Hola Arduino panel.</span><span class="sxs-lookup"><span data-stu-id="8575b-133">Use [gulp.js](http://gulpjs.com) tooautomate hello deployment of hello sample application tooyour Arduino board.</span></span>

<span data-ttu-id="8575b-134">Instalar `gulp`, `device-discovery-cli` ejecutando Hola siguiente comando en terminal hello:</span><span class="sxs-lookup"><span data-stu-id="8575b-134">Install `gulp`, `device-discovery-cli` by running hello following command in hello terminal:</span></span>

```bash
sudo npm install -g gulp device-discovery-cli
```

<span data-ttu-id="8575b-135">Si experimenta problemas de instalación de Node.js y estas herramientas de desarrollo adicional en macOS, vea hello [Guía de solución de problemas] [ troubleshooting] para soluciones toocommon problemas.</span><span class="sxs-lookup"><span data-stu-id="8575b-135">If you experience issues installing Node.js and these additional development tools on macOS, see hello [troubleshooting guide][troubleshooting] for solutions toocommon problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="8575b-136">Instalación de Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="8575b-136">Install Visual Studio Code</span></span>
<span data-ttu-id="8575b-137">[Descargue](https://code.visualstudio.com/docs/setup/osx) e instale Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="8575b-137">[Download](https://code.visualstudio.com/docs/setup/osx) and install Visual Studio Code.</span></span> <span data-ttu-id="8575b-138">Visual Studio Code es un editor de código fuente ligero pero eficaz para Windows, Linux y Mac OS.</span><span class="sxs-lookup"><span data-stu-id="8575b-138">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="8575b-139">Utilice este editor más adelante en el código de ejemplo de Hola tooedit tutorial Hola.</span><span class="sxs-lookup"><span data-stu-id="8575b-139">You use this editor later in hello tutorial tooedit hello sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="8575b-140">Resumen</span><span class="sxs-lookup"><span data-stu-id="8575b-140">Summary</span></span>
<span data-ttu-id="8575b-141">Ha instalado herramientas de desarrollo de hello necesario y software para la primera aplicación de ejemplo Hola.</span><span class="sxs-lookup"><span data-stu-id="8575b-141">You've installed hello required development tools and software for hello first sample application.</span></span> <span data-ttu-id="8575b-142">Hola siguiente tarea es toocreate, implementar y ejecutar la aplicación de ejemplo de Hola en el panel de Arduino.</span><span class="sxs-lookup"><span data-stu-id="8575b-142">hello next task is toocreate, deploy, and run hello sample application on your Arduino board.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8575b-143">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8575b-143">Next steps</span></span>
<span data-ttu-id="8575b-144">[Crear e implementar la aplicación de hello parpadeo][create-and-deploy-the-blink-application]</span><span class="sxs-lookup"><span data-stu-id="8575b-144">[Create and deploy hello blink application][create-and-deploy-the-blink-application]</span></span>
<!-- Images and links -->

[windows]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-win32.md
[ubuntu]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-ubuntu.md
[macos]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-mac.md
[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[create-and-deploy-the-blink-application]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-deploy-blink-app.md