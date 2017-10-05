---
title: "Conexión de Raspberry Pi (Node) a Azure IoT: Lección 1: Obtención de las herramientas (macOS) | Microsoft Docs"
description: "Descargue e instale las herramientas y el software necesarios para la primera aplicación de ejemplo de Pi en macOS."
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
ms.openlocfilehash: 6c2338baa8e88bab4c4be64568220f53178943cd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-macos-1010"></a><span data-ttu-id="12133-104">Obtención de las herramientas (Mac OS 10.10)</span><span class="sxs-lookup"><span data-stu-id="12133-104">Get the tools (macOS 10.10)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="12133-105">Windows 7 o posterior</span><span class="sxs-lookup"><span data-stu-id="12133-105">Windows 7 or later</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-win32.md)
> * [<span data-ttu-id="12133-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="12133-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="12133-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="12133-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="12133-108">Lo que hará</span><span class="sxs-lookup"><span data-stu-id="12133-108">What you will do</span></span>
<span data-ttu-id="12133-109">Descargue las herramientas de desarrollo y el software para la primera aplicación de ejemplo de Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="12133-109">Download the development tools and the software for the first sample application for your Raspberry Pi 3.</span></span> <span data-ttu-id="12133-110">Si tiene problemas, busque soluciones en la [página de solución de problemas](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="12133-110">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="12133-111">Lo qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="12133-111">What you will learn</span></span>
<span data-ttu-id="12133-112">En este artículo, aprenderá lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="12133-112">In this article, you will learn:</span></span>

* <span data-ttu-id="12133-113">Cómo instalar Git y Node.js</span><span class="sxs-lookup"><span data-stu-id="12133-113">How to install Git and Node.js.</span></span>
  * <span data-ttu-id="12133-114">[Git](https://git-scm.com) es un sistema de control de versiones distribuido de código.</span><span class="sxs-lookup"><span data-stu-id="12133-114">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="12133-115">La aplicación de ejemplo de este artículo se almacena en Git.</span><span class="sxs-lookup"><span data-stu-id="12133-115">The sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="12133-116">[Node.js](https://nodejs.org/en/) es un entorno de tiempo de ejecución de JavaScript con un amplio ecosistema de paquetes.</span><span class="sxs-lookup"><span data-stu-id="12133-116">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="12133-117">Cómo usar NPM para instalar las herramientas de desarrollo de Node.js adicionales.</span><span class="sxs-lookup"><span data-stu-id="12133-117">How to use NPM to install additional Node.js development tools.</span></span>
  * <span data-ttu-id="12133-118">La versión mínima necesaria de Node.js es 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="12133-118">The minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="12133-119">[NPM](https://www.npmjs.com) es uno de los administradores de paquetes para Node.js.</span><span class="sxs-lookup"><span data-stu-id="12133-119">[NPM](https://www.npmjs.com) is one of the package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="12133-120">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="12133-120">What you need</span></span>
<span data-ttu-id="12133-121">Para completar esta operación, necesitará:</span><span class="sxs-lookup"><span data-stu-id="12133-121">To complete this operation, you will need:</span></span>

* <span data-ttu-id="12133-122">Una conexión a Internet para descargar el software y las herramientas de desarrollo necesarias</span><span class="sxs-lookup"><span data-stu-id="12133-122">An Internet connection to download the development tools and the software.</span></span>
* <span data-ttu-id="12133-123">Un equipo Mac que ejecute macOS Yosemite (10.10) o posterior</span><span class="sxs-lookup"><span data-stu-id="12133-123">A Mac that is running macOS Yosemite (10.10) or later.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="12133-124">Instalación de Git y Node.js</span><span class="sxs-lookup"><span data-stu-id="12133-124">Install Git and Node.js</span></span>
<span data-ttu-id="12133-125">Para instalar Git y Node.js, use la utilidad de administración de paquetes [Homebrew](http://brew.sh) siguiendo estos pasos:</span><span class="sxs-lookup"><span data-stu-id="12133-125">To install Git and Node.js, use the [Homebrew](http://brew.sh) package management utility by following these steps:</span></span>

1. <span data-ttu-id="12133-126">Instale Homebrew.</span><span class="sxs-lookup"><span data-stu-id="12133-126">Install Homebrew.</span></span> <span data-ttu-id="12133-127">Si ya ha instalado Homebrew, vaya al paso 2.</span><span class="sxs-lookup"><span data-stu-id="12133-127">If you've already installed Homebrew, go to step 2.</span></span>
   
   1. <span data-ttu-id="12133-128">Presione `Cmd + Space` y escriba `Terminal` para abrir una ventana de terminal.</span><span class="sxs-lookup"><span data-stu-id="12133-128">Press `Cmd + Space` and enter `Terminal` to open a terminal.</span></span>
   2. <span data-ttu-id="12133-129">Ejecute el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="12133-129">Run the following command:</span></span>
      
      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```
2. <span data-ttu-id="12133-130">Instale Git y Node.js ejecutando el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="12133-130">Install Git and Node.js by running the following command:</span></span>
   
   ```bash
   brew install node git
   ```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="12133-131">Instalación de herramientas de desarrollo de Node.js adicionales</span><span class="sxs-lookup"><span data-stu-id="12133-131">Install additional Node.js development tools</span></span>
<span data-ttu-id="12133-132">Utilice [gulp.js](http://gulpjs.com) para automatizar la implementación de la aplicación de ejemplo en Pi.</span><span class="sxs-lookup"><span data-stu-id="12133-132">Use [gulp.js](http://gulpjs.com) to automate the deployment of the sample application to Pi.</span></span> <span data-ttu-id="12133-133">Utilice [device-discovery-cli](https://github.com/Azure/device-discovery-cli) para recuperar información de la red de los dispositivos de IoT.</span><span class="sxs-lookup"><span data-stu-id="12133-133">Use the [device-discovery-cli](https://github.com/Azure/device-discovery-cli) to retrieve network information about your IoT devices.</span></span>

<span data-ttu-id="12133-134">Instale `gulp` y `device-discovery-cli` ejecutando el comando siguiente en la ventana de terminal:</span><span class="sxs-lookup"><span data-stu-id="12133-134">Install `gulp` and `device-discovery-cli` by running the following command in the terminal:</span></span>

```bash
npm install -g device-discovery-cli gulp
```

<span data-ttu-id="12133-135">Si experimenta problemas al instalar Node.js y estas herramientas de desarrollo adicionales en Mac OS, consulte la [Guía de solución de problemas](iot-hub-raspberry-pi-kit-node-troubleshooting.md) para ver soluciones a problemas comunes.</span><span class="sxs-lookup"><span data-stu-id="12133-135">If you experience issues installing Node.js and these additional development tools on macOS, see the [troubleshooting guide](iot-hub-raspberry-pi-kit-node-troubleshooting.md) for solutions to common problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="12133-136">Instalación de Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="12133-136">Install Visual Studio Code</span></span>
<span data-ttu-id="12133-137">[Descargue](https://code.visualstudio.com/docs/setup/osx) e instale Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="12133-137">[Download](https://code.visualstudio.com/docs/setup/osx) and install Visual Studio Code.</span></span> <span data-ttu-id="12133-138">Visual Studio Code es un editor de código fuente ligero pero eficaz para Windows, Linux y Mac OS.</span><span class="sxs-lookup"><span data-stu-id="12133-138">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="12133-139">Use este editor más adelante en el tutorial para editar el código de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="12133-139">You use this editor later in the tutorial to edit the sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="12133-140">Resumen</span><span class="sxs-lookup"><span data-stu-id="12133-140">Summary</span></span>
<span data-ttu-id="12133-141">Ha instalado las herramientas de desarrollo y el software necesarios para la primera aplicación de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="12133-141">You've installed the required development tools and software for the first sample application.</span></span> <span data-ttu-id="12133-142">En la siguiente tarea, creará, implementará y ejecutará la aplicación de ejemplo en Pi.</span><span class="sxs-lookup"><span data-stu-id="12133-142">The next task is to create, deploy, and run the sample application on Pi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="12133-143">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="12133-143">Next steps</span></span>
[<span data-ttu-id="12133-144">Creación e implementación de la aplicación de intermitencia de ejemplo</span><span class="sxs-lookup"><span data-stu-id="12133-144">Create and deploy the blink sample application</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-deploy-blink-app.md)

