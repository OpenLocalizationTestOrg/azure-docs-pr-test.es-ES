---
title: "Conexión de Intel Edison (C) a Azure IoT: Lección 1: Obtención de las herramientas (macOS) | Microsoft Docs"
description: "Descargue e instale las herramientas y el software necesarios para la primera aplicación de ejemplo de Edison en macOS."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: herramientas de desarrollo de Arduino, desarrollo de iot, software de iot, software de internet de las cosas, instalar git en mac, instalar node js mac
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: 3f764f2e-25fa-4dde-9e8d-d278453fccfd
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 27939f731121522f688e606052492bda8ae045fe
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-macos-1010"></a><span data-ttu-id="be6e1-104">Obtención de las herramientas (Mac OS 10.10)</span><span class="sxs-lookup"><span data-stu-id="be6e1-104">Get the tools (macOS 10.10)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="be6e1-105">[Windows 7 o posterior][windows]</span><span class="sxs-lookup"><span data-stu-id="be6e1-105">[Windows 7 or later][windows]</span></span>
> * <span data-ttu-id="be6e1-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="be6e1-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="be6e1-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="be6e1-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="be6e1-108">Lo que hará</span><span class="sxs-lookup"><span data-stu-id="be6e1-108">What you will do</span></span>
<span data-ttu-id="be6e1-109">Descargue las herramientas de desarrollo y el software para la primera aplicación de ejemplo de Intel Edison.</span><span class="sxs-lookup"><span data-stu-id="be6e1-109">Download the development tools and the software for the first sample application for your Intel Edison.</span></span> <span data-ttu-id="be6e1-110">Si tiene problemas, busque soluciones en [esta página][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="be6e1-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

> [!NOTE]
> <span data-ttu-id="be6e1-111">Aunque el lenguaje de programación de la lógica principal es C, las herramientas de Node.js se usan en las lecciones para compilar e implementar aplicaciones de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="be6e1-111">Although the programming language of the main logic is C, Node.js tools are used in the lessons to build and deploy sample applications.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="be6e1-112">Lo qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="be6e1-112">What you will learn</span></span>
<span data-ttu-id="be6e1-113">En este artículo, aprenderá lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="be6e1-113">In this article, you will learn:</span></span>

* <span data-ttu-id="be6e1-114">Cómo instalar Git y Node.js</span><span class="sxs-lookup"><span data-stu-id="be6e1-114">How to install Git and Node.js.</span></span>
  * <span data-ttu-id="be6e1-115">[Git](https://git-scm.com) es un sistema de control de versiones distribuido de código.</span><span class="sxs-lookup"><span data-stu-id="be6e1-115">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="be6e1-116">La aplicación de ejemplo de este artículo se almacena en Git.</span><span class="sxs-lookup"><span data-stu-id="be6e1-116">The sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="be6e1-117">[Node.js](https://nodejs.org/en/) es un entorno de tiempo de ejecución de JavaScript con un amplio ecosistema de paquetes.</span><span class="sxs-lookup"><span data-stu-id="be6e1-117">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="be6e1-118">Cómo usar NPM para instalar las herramientas de desarrollo de Node.js adicionales.</span><span class="sxs-lookup"><span data-stu-id="be6e1-118">How to use NPM to install additional Node.js development tools.</span></span>
  * <span data-ttu-id="be6e1-119">La versión mínima necesaria de Node.js es 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="be6e1-119">The minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="be6e1-120">[NPM](https://www.npmjs.com) es uno de los administradores de paquetes para Node.js.</span><span class="sxs-lookup"><span data-stu-id="be6e1-120">[NPM](https://www.npmjs.com) is one of the package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="be6e1-121">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="be6e1-121">What you need</span></span>
<span data-ttu-id="be6e1-122">Para completar esta operación, necesitará:</span><span class="sxs-lookup"><span data-stu-id="be6e1-122">To complete this operation, you will need:</span></span>
* <span data-ttu-id="be6e1-123">Una conexión a Internet para descargar el software y las herramientas de desarrollo necesarias</span><span class="sxs-lookup"><span data-stu-id="be6e1-123">An Internet connection to download the development tools and the software.</span></span>
* <span data-ttu-id="be6e1-124">Un equipo Mac que ejecute macOS Yosemite (10.10) o posterior</span><span class="sxs-lookup"><span data-stu-id="be6e1-124">A Mac that is running macOS Yosemite (10.10) or later.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="be6e1-125">Instalación de Git y Node.js</span><span class="sxs-lookup"><span data-stu-id="be6e1-125">Install Git and Node.js</span></span>
<span data-ttu-id="be6e1-126">Para instalar Git y Node.js, use la utilidad de administración de paquetes [Homebrew](http://brew.sh) siguiendo estos pasos:</span><span class="sxs-lookup"><span data-stu-id="be6e1-126">To install Git and Node.js, use the [Homebrew](http://brew.sh) package management utility by following these steps:</span></span>

1. <span data-ttu-id="be6e1-127">Instale Homebrew.</span><span class="sxs-lookup"><span data-stu-id="be6e1-127">Install Homebrew.</span></span> <span data-ttu-id="be6e1-128">Si ya ha instalado Homebrew, vaya al paso 2.</span><span class="sxs-lookup"><span data-stu-id="be6e1-128">If you've already installed Homebrew, go to step 2.</span></span>

   1. <span data-ttu-id="be6e1-129">Presione `Cmd + Space` y escriba `Terminal` para abrir una ventana de terminal.</span><span class="sxs-lookup"><span data-stu-id="be6e1-129">Press `Cmd + Space` and enter `Terminal` to open a terminal.</span></span>
   2. <span data-ttu-id="be6e1-130">Ejecute el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="be6e1-130">Run the following command:</span></span>

      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```
2. <span data-ttu-id="be6e1-131">Instale Git y Node.js ejecutando el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="be6e1-131">Install Git and Node.js by running the following command:</span></span>

   ```bash
   brew install node git
   ```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="be6e1-132">Instalación de herramientas de desarrollo de Node.js adicionales</span><span class="sxs-lookup"><span data-stu-id="be6e1-132">Install additional Node.js development tools</span></span>
<span data-ttu-id="be6e1-133">Utilice [gulp.js](http://gulpjs.com) para automatizar la implementación de la aplicación de ejemplo en Edison.</span><span class="sxs-lookup"><span data-stu-id="be6e1-133">Use [gulp.js](http://gulpjs.com) to automate the deployment of the sample application to your Edison.</span></span>

<span data-ttu-id="be6e1-134">Instale `gulp` ejecutando el comando siguiente en la ventana de terminal:</span><span class="sxs-lookup"><span data-stu-id="be6e1-134">Install `gulp` by running the following command in the terminal:</span></span>

```bash
sudo npm install -g gulp
```

<span data-ttu-id="be6e1-135">Si experimenta problemas al instalar Node.js y estas herramientas de desarrollo adicionales en Mac OS, consulte la [Guía de solución de problemas][troubleshooting] para ver soluciones a problemas comunes.</span><span class="sxs-lookup"><span data-stu-id="be6e1-135">If you experience issues installing Node.js and these additional development tools on macOS, see the [troubleshooting guide][troubleshooting] for solutions to common problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="be6e1-136">Instalación de Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="be6e1-136">Install Visual Studio Code</span></span>
<span data-ttu-id="be6e1-137">[Descargue](https://code.visualstudio.com/docs/setup/osx) e instale Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="be6e1-137">[Download](https://code.visualstudio.com/docs/setup/osx) and install Visual Studio Code.</span></span> <span data-ttu-id="be6e1-138">Visual Studio Code es un editor de código fuente ligero pero eficaz para Windows, Linux y Mac OS.</span><span class="sxs-lookup"><span data-stu-id="be6e1-138">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="be6e1-139">Use este editor más adelante en el tutorial para editar el código de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="be6e1-139">You use this editor later in the tutorial to edit the sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="be6e1-140">Resumen</span><span class="sxs-lookup"><span data-stu-id="be6e1-140">Summary</span></span>
<span data-ttu-id="be6e1-141">Ha instalado las herramientas de desarrollo y el software necesarios para la primera aplicación de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="be6e1-141">You've installed the required development tools and software for the first sample application.</span></span> <span data-ttu-id="be6e1-142">En la siguiente tarea, creará, implementará y ejecutará la aplicación de ejemplo en Edison.</span><span class="sxs-lookup"><span data-stu-id="be6e1-142">The next task is to create, deploy, and run the sample application on Edison.</span></span>

## <a name="next-steps"></a><span data-ttu-id="be6e1-143">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="be6e1-143">Next steps</span></span>
<span data-ttu-id="be6e1-144">[Creación e implementación de la aplicación de intermitencia][create-and-deploy-the-blink-application]</span><span class="sxs-lookup"><span data-stu-id="be6e1-144">[Create and deploy the blink application][create-and-deploy-the-blink-application]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[create-and-deploy-the-blink-application]: iot-hub-intel-edison-kit-c-lesson1-deploy-blink-app.md
[windows]: iot-hub-intel-edison-kit-c-lesson1-get-the-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-c-lesson1-get-the-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-c-lesson1-get-the-tools-mac.md
