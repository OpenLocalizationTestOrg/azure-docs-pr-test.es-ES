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
# <a name="get-the-tools-macos-1010"></a><span data-ttu-id="73ff8-104">Obtención de las herramientas (Mac OS 10.10)</span><span class="sxs-lookup"><span data-stu-id="73ff8-104">Get the tools (macOS 10.10)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="73ff8-105">[Windows 7 o posterior][windows]</span><span class="sxs-lookup"><span data-stu-id="73ff8-105">[Windows 7 or later][windows]</span></span>
> * <span data-ttu-id="73ff8-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="73ff8-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="73ff8-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="73ff8-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="73ff8-108">Lo que hará</span><span class="sxs-lookup"><span data-stu-id="73ff8-108">What you will do</span></span>
<span data-ttu-id="73ff8-109">Descargue las herramientas de desarrollo y el software para la primera aplicación de ejemplo de Intel Edison.</span><span class="sxs-lookup"><span data-stu-id="73ff8-109">Download the development tools and the software for the first sample application for your Intel Edison.</span></span> <span data-ttu-id="73ff8-110">Si tiene problemas, busque soluciones en [esta página][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="73ff8-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="73ff8-111">Lo qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="73ff8-111">What you will learn</span></span>
<span data-ttu-id="73ff8-112">En este artículo, aprenderá lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="73ff8-112">In this article, you will learn:</span></span>

* <span data-ttu-id="73ff8-113">Cómo instalar Git y Node.js</span><span class="sxs-lookup"><span data-stu-id="73ff8-113">How to install Git and Node.js.</span></span>
  * <span data-ttu-id="73ff8-114">[Git](https://git-scm.com) es un sistema de control de versiones distribuido de código.</span><span class="sxs-lookup"><span data-stu-id="73ff8-114">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="73ff8-115">La aplicación de ejemplo de este artículo se almacena en Git.</span><span class="sxs-lookup"><span data-stu-id="73ff8-115">The sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="73ff8-116">[Node.js](https://nodejs.org/en/) es un entorno de tiempo de ejecución de JavaScript con un amplio ecosistema de paquetes.</span><span class="sxs-lookup"><span data-stu-id="73ff8-116">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="73ff8-117">Cómo usar NPM para instalar las herramientas de desarrollo de Node.js adicionales.</span><span class="sxs-lookup"><span data-stu-id="73ff8-117">How to use NPM to install additional Node.js development tools.</span></span>
  * <span data-ttu-id="73ff8-118">La versión mínima necesaria de Node.js es 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="73ff8-118">The minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="73ff8-119">[NPM](https://www.npmjs.com) es uno de los administradores de paquetes para Node.js.</span><span class="sxs-lookup"><span data-stu-id="73ff8-119">[NPM](https://www.npmjs.com) is one of the package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="73ff8-120">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="73ff8-120">What you need</span></span>
<span data-ttu-id="73ff8-121">Para completar esta operación, necesitará:</span><span class="sxs-lookup"><span data-stu-id="73ff8-121">To complete this operation, you will need:</span></span>
* <span data-ttu-id="73ff8-122">Una conexión a Internet para descargar el software y las herramientas de desarrollo necesarias</span><span class="sxs-lookup"><span data-stu-id="73ff8-122">An Internet connection to download the development tools and the software.</span></span>
* <span data-ttu-id="73ff8-123">Un equipo Mac que ejecute macOS Yosemite (10.10) o posterior</span><span class="sxs-lookup"><span data-stu-id="73ff8-123">A Mac that is running macOS Yosemite (10.10) or later.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="73ff8-124">Instalación de Git y Node.js</span><span class="sxs-lookup"><span data-stu-id="73ff8-124">Install Git and Node.js</span></span>
<span data-ttu-id="73ff8-125">Para instalar Git y Node.js, use la utilidad de administración de paquetes [Homebrew](http://brew.sh) siguiendo estos pasos:</span><span class="sxs-lookup"><span data-stu-id="73ff8-125">To install Git and Node.js, use the [Homebrew](http://brew.sh) package management utility by following these steps:</span></span>

1. <span data-ttu-id="73ff8-126">Instale Homebrew.</span><span class="sxs-lookup"><span data-stu-id="73ff8-126">Install Homebrew.</span></span> <span data-ttu-id="73ff8-127">Si ya ha instalado Homebrew, vaya al paso 2.</span><span class="sxs-lookup"><span data-stu-id="73ff8-127">If you've already installed Homebrew, go to step 2.</span></span>

   1. <span data-ttu-id="73ff8-128">Presione `Cmd + Space` y escriba `Terminal` para abrir una ventana de terminal.</span><span class="sxs-lookup"><span data-stu-id="73ff8-128">Press `Cmd + Space` and enter `Terminal` to open a terminal.</span></span>
   2. <span data-ttu-id="73ff8-129">Ejecute el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="73ff8-129">Run the following command:</span></span>

      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```
2. <span data-ttu-id="73ff8-130">Instale Git y Node.js ejecutando el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="73ff8-130">Install Git and Node.js by running the following command:</span></span>

   ```bash
   brew install node git
   ```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="73ff8-131">Instalación de herramientas de desarrollo de Node.js adicionales</span><span class="sxs-lookup"><span data-stu-id="73ff8-131">Install additional Node.js development tools</span></span>
<span data-ttu-id="73ff8-132">Utilice [gulp.js](http://gulpjs.com) para automatizar la implementación de la aplicación de ejemplo en Edison.</span><span class="sxs-lookup"><span data-stu-id="73ff8-132">Use [gulp.js](http://gulpjs.com) to automate the deployment of the sample application to your Edison.</span></span>

<span data-ttu-id="73ff8-133">Instale `gulp` ejecutando el comando siguiente en la ventana de terminal:</span><span class="sxs-lookup"><span data-stu-id="73ff8-133">Install `gulp` by running the following command in the terminal:</span></span>

```bash
sudo npm install -g gulp
```

<span data-ttu-id="73ff8-134">Si experimenta problemas al instalar Node.js y estas herramientas de desarrollo adicionales en Mac OS, consulte la [Guía de solución de problemas][troubleshooting] para ver soluciones a problemas comunes.</span><span class="sxs-lookup"><span data-stu-id="73ff8-134">If you experience issues installing Node.js and these additional development tools on macOS, see the [troubleshooting guide][troubleshooting] for solutions to common problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="73ff8-135">Instalación de Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="73ff8-135">Install Visual Studio Code</span></span>
<span data-ttu-id="73ff8-136">[Descargue](https://code.visualstudio.com/docs/setup/osx) e instale Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="73ff8-136">[Download](https://code.visualstudio.com/docs/setup/osx) and install Visual Studio Code.</span></span> <span data-ttu-id="73ff8-137">Visual Studio Code es un editor de código fuente ligero pero eficaz para Windows, Linux y Mac OS.</span><span class="sxs-lookup"><span data-stu-id="73ff8-137">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="73ff8-138">Use este editor más adelante en el tutorial para editar el código de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="73ff8-138">You use this editor later in the tutorial to edit the sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="73ff8-139">Resumen</span><span class="sxs-lookup"><span data-stu-id="73ff8-139">Summary</span></span>
<span data-ttu-id="73ff8-140">Ha instalado las herramientas de desarrollo y el software necesarios para la primera aplicación de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="73ff8-140">You've installed the required development tools and software for the first sample application.</span></span> <span data-ttu-id="73ff8-141">En la siguiente tarea, creará, implementará y ejecutará la aplicación de ejemplo en Edison.</span><span class="sxs-lookup"><span data-stu-id="73ff8-141">The next task is to create, deploy, and run the sample application on Edison.</span></span>

## <a name="next-steps"></a><span data-ttu-id="73ff8-142">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="73ff8-142">Next steps</span></span>
<span data-ttu-id="73ff8-143">[Creación e implementación de la aplicación de intermitencia][create-and-deploy-the-blink-application]</span><span class="sxs-lookup"><span data-stu-id="73ff8-143">[Create and deploy the blink application][create-and-deploy-the-blink-application]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[create-and-deploy-the-blink-application]: iot-hub-intel-edison-kit-node-lesson1-deploy-blink-app.md
[windows]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-mac.md
