---
title: "Conexión de Raspberry Pi (Node) a Azure IoT: Lección 1: Obtención de las herramientas (Ubuntu) | Microsoft Docs"
description: "Descargue e instale las herramientas y el software necesarios para la primera aplicación de ejemplo de Pi en Ubuntu."
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
ms.openlocfilehash: de583be0cdce058c83091f421376812e8013d76e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-ubuntu-1604"></a><span data-ttu-id="e123a-104">Obtención de las herramientas (Ubuntu 16.04)</span><span class="sxs-lookup"><span data-stu-id="e123a-104">Get the tools (Ubuntu 16.04)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="e123a-105">Windows 7 o posterior</span><span class="sxs-lookup"><span data-stu-id="e123a-105">Windows 7 or later</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-win32.md)
> * [<span data-ttu-id="e123a-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="e123a-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="e123a-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="e123a-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-mac.md)


## <a name="what-you-will-do"></a><span data-ttu-id="e123a-108">Lo que hará</span><span class="sxs-lookup"><span data-stu-id="e123a-108">What you will do</span></span>
<span data-ttu-id="e123a-109">Descargue las herramientas de desarrollo y el software para la primera aplicación de ejemplo de Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="e123a-109">Download the development tools and the software for the first sample application for Raspberry Pi 3.</span></span> <span data-ttu-id="e123a-110">Si tiene problemas, busque soluciones en la [página de solución de problemas](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="e123a-110">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="e123a-111">Lo qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="e123a-111">What you will learn</span></span>
<span data-ttu-id="e123a-112">En este artículo, aprenderá lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="e123a-112">In this article, you will learn:</span></span>

* <span data-ttu-id="e123a-113">Cómo instalar Git y Node.js</span><span class="sxs-lookup"><span data-stu-id="e123a-113">How to install Git and Node.js.</span></span>
  * <span data-ttu-id="e123a-114">[Git](https://git-scm.com) es un sistema de control de versiones distribuido de código.</span><span class="sxs-lookup"><span data-stu-id="e123a-114">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="e123a-115">La aplicación de ejemplo de este artículo se almacena en Git.</span><span class="sxs-lookup"><span data-stu-id="e123a-115">The sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="e123a-116">[Node.js](https://nodejs.org/en/) es un entorno de tiempo de ejecución de JavaScript con un amplio ecosistema de paquetes.</span><span class="sxs-lookup"><span data-stu-id="e123a-116">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="e123a-117">Cómo usar NPM para instalar las herramientas de desarrollo de Node.js adicionales.</span><span class="sxs-lookup"><span data-stu-id="e123a-117">How to use NPM to install additional Node.js development tools.</span></span>
  * <span data-ttu-id="e123a-118">La versión mínima necesaria de Node.js es 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="e123a-118">The minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="e123a-119">[NPM](https://www.npmjs.com) es uno de los administradores de paquetes para Node.js.</span><span class="sxs-lookup"><span data-stu-id="e123a-119">[NPM](https://www.npmjs.com) is one of the package managers for Node.js.</span></span>

## <a name="what-do-you-need"></a><span data-ttu-id="e123a-120">Qué necesita</span><span class="sxs-lookup"><span data-stu-id="e123a-120">What do you need</span></span>
<span data-ttu-id="e123a-121">Para completar esta operación, necesitará:</span><span class="sxs-lookup"><span data-stu-id="e123a-121">To complete this operation, you will need:</span></span>

* <span data-ttu-id="e123a-122">Una conexión a Internet para descargar el software y las herramientas de desarrollo necesarias</span><span class="sxs-lookup"><span data-stu-id="e123a-122">An Internet connection to download the development tools and the software.</span></span>
* <span data-ttu-id="e123a-123">Un equipo que ejecute Ubuntu 16.04 o posterior</span><span class="sxs-lookup"><span data-stu-id="e123a-123">A computer that is running Ubuntu 16.04 or later.</span></span>

## <a name="install-git-nodejs-and-npm"></a><span data-ttu-id="e123a-124">Instalación de Git, Node.js y NPM</span><span class="sxs-lookup"><span data-stu-id="e123a-124">Install Git, Node.js, and NPM</span></span>
<span data-ttu-id="e123a-125">Utilice el método abreviado de teclado `Ctrl + Alt + T` para abrir una ventana de terminal y ejecute los siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="e123a-125">Use the keyboard shortcut `Ctrl + Alt + T` to open a terminal and run the following commands:</span></span>

```bash
sudo apt-get update
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
sudo apt-get install -y nodejs
sudo apt-get install git
```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="e123a-126">Instalación de herramientas de desarrollo de Node.js adicionales</span><span class="sxs-lookup"><span data-stu-id="e123a-126">Install additional Node.js development tools</span></span>
<span data-ttu-id="e123a-127">Utilice [gulp.js](http://gulpjs.com) para automatizar la implementación de la aplicación de ejemplo en Pi.</span><span class="sxs-lookup"><span data-stu-id="e123a-127">You use [gulp.js](http://gulpjs.com) to automate the deployment of the sample application to Pi.</span></span> <span data-ttu-id="e123a-128">Utiliza también [device-discovery-cli](https://github.com/Azure/device-discovery-cli) para recuperar información de la red de los dispositivos de IoT.</span><span class="sxs-lookup"><span data-stu-id="e123a-128">You also use the [device-discovery-cli](https://github.com/Azure/device-discovery-cli) to retrieve network information about your IoT devices.</span></span>

<span data-ttu-id="e123a-129">Instale `gulp` y `device-discovery-cli` ejecutando el comando siguiente en la ventana de terminal:</span><span class="sxs-lookup"><span data-stu-id="e123a-129">Install `gulp` and `device-discovery-cli` by running the following command in the terminal:</span></span>

```bash
sudo npm install -g device-discovery-cli gulp
```

<span data-ttu-id="e123a-130">Si experimenta problemas al instalar Node.js y estas herramientas de desarrollo adicionales en Ubuntu, consulte la [Guía de solución de problemas](iot-hub-raspberry-pi-kit-node-troubleshooting.md) para ver soluciones a problemas comunes.</span><span class="sxs-lookup"><span data-stu-id="e123a-130">If you experience issues installing Node.js and these additional development tools on Ubuntu, see the [troubleshooting guide](iot-hub-raspberry-pi-kit-node-troubleshooting.md) for solutions to common problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="e123a-131">Instalación de Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="e123a-131">Install Visual Studio Code</span></span>
<span data-ttu-id="e123a-132">[Descargue](https://code.visualstudio.com/docs/setup/linux) e instale Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="e123a-132">[Download](https://code.visualstudio.com/docs/setup/linux) and install Visual Studio Code.</span></span> <span data-ttu-id="e123a-133">Visual Studio Code es un editor de código fuente ligero pero eficaz para Windows, Linux y Mac OS.</span><span class="sxs-lookup"><span data-stu-id="e123a-133">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="e123a-134">Use este editor más adelante en el tutorial para editar el código de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="e123a-134">You use this editor later in the tutorial to edit the sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="e123a-135">Resumen</span><span class="sxs-lookup"><span data-stu-id="e123a-135">Summary</span></span>
<span data-ttu-id="e123a-136">Ha instalado las herramientas de desarrollo y el software necesarios para la primera aplicación de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="e123a-136">You've installed the required development tools and software for the first sample application.</span></span> <span data-ttu-id="e123a-137">En la siguiente tarea, creará, implementará y ejecutará la aplicación de ejemplo en Pi.</span><span class="sxs-lookup"><span data-stu-id="e123a-137">The next task is to create, deploy, and run the sample application on Pi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e123a-138">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e123a-138">Next steps</span></span>
[<span data-ttu-id="e123a-139">Creación e implementación de la aplicación de intermitencia de ejemplo</span><span class="sxs-lookup"><span data-stu-id="e123a-139">Create and deploy the blink sample application</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-deploy-blink-app.md)
