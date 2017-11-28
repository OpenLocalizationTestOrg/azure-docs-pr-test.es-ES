---
title: "Conexión de Intel Edison (Node) a Azure IoT: Lección 1: Obtención de las herramientas (Ubuntu) | Microsoft Docs"
description: "Descargue e instale las herramientas y el software necesarios para la primera aplicación de ejemplo de Edison en Ubuntu."
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
ms.openlocfilehash: 74c5f06c2b12d140814bfb75125d60b83addf70c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-ubuntu-1604"></a><span data-ttu-id="beb0d-104">Obtención de las herramientas (Ubuntu 16.04)</span><span class="sxs-lookup"><span data-stu-id="beb0d-104">Get the tools (Ubuntu 16.04)</span></span>

> [!div class="op_single_selector"]
> * <span data-ttu-id="beb0d-105">[Windows 7 o posterior][windows]</span><span class="sxs-lookup"><span data-stu-id="beb0d-105">[Windows 7 or later][windows]</span></span>
> * <span data-ttu-id="beb0d-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="beb0d-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="beb0d-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="beb0d-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="beb0d-108">Lo que hará</span><span class="sxs-lookup"><span data-stu-id="beb0d-108">What you will do</span></span>
<span data-ttu-id="beb0d-109">Descargue las herramientas de desarrollo y el software para la primera aplicación de ejemplo de Intel Edison.</span><span class="sxs-lookup"><span data-stu-id="beb0d-109">Download the development tools and the software for the first sample application for your Intel Edison.</span></span> <span data-ttu-id="beb0d-110">Si tiene problemas, busque soluciones en [esta página][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="beb0d-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="beb0d-111">Lo qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="beb0d-111">What you will learn</span></span>
<span data-ttu-id="beb0d-112">En este artículo, aprenderá lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="beb0d-112">In this article, you will learn:</span></span>

* <span data-ttu-id="beb0d-113">Cómo instalar Git y Node.js</span><span class="sxs-lookup"><span data-stu-id="beb0d-113">How to install Git and Node.js</span></span>
  * <span data-ttu-id="beb0d-114">[Git](https://git-scm.com) es un sistema de control de versiones distribuido de código.</span><span class="sxs-lookup"><span data-stu-id="beb0d-114">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="beb0d-115">La aplicación de ejemplo de este artículo se almacena en Git.</span><span class="sxs-lookup"><span data-stu-id="beb0d-115">The sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="beb0d-116">[Node.js](https://nodejs.org/en/) es un entorno de tiempo de ejecución de JavaScript con un amplio ecosistema de paquetes.</span><span class="sxs-lookup"><span data-stu-id="beb0d-116">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="beb0d-117">Cómo usar NPM para instalar las herramientas de desarrollo de Node.js adicionales.</span><span class="sxs-lookup"><span data-stu-id="beb0d-117">How to use NPM to install additional Node.js development tools.</span></span>
  * <span data-ttu-id="beb0d-118">La versión mínima necesaria de Node.js es 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="beb0d-118">The minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="beb0d-119">[NPM](https://www.npmjs.com) es uno de los administradores de paquetes para Node.js.</span><span class="sxs-lookup"><span data-stu-id="beb0d-119">[NPM](https://www.npmjs.com) is one of the package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="beb0d-120">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="beb0d-120">What you need</span></span>
<span data-ttu-id="beb0d-121">Para completar esta operación, necesitará:</span><span class="sxs-lookup"><span data-stu-id="beb0d-121">To complete this operation, you will need:</span></span>
* <span data-ttu-id="beb0d-122">Una conexión a Internet para descargar el software y las herramientas de desarrollo necesarias</span><span class="sxs-lookup"><span data-stu-id="beb0d-122">An Internet connection to download the development tools and the software.</span></span>
* <span data-ttu-id="beb0d-123">Un equipo que ejecute Ubuntu 16.04 o posterior</span><span class="sxs-lookup"><span data-stu-id="beb0d-123">A computer that is running Ubuntu 16.04 or later.</span></span>

## <a name="install-git-nodejs-and-npm"></a><span data-ttu-id="beb0d-124">Instalación de Git, Node.js y NPM</span><span class="sxs-lookup"><span data-stu-id="beb0d-124">Install Git, Node.js, and NPM</span></span>
<span data-ttu-id="beb0d-125">Utilice el método abreviado de teclado `Ctrl + Alt + T` para abrir una ventana de terminal y ejecute los siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="beb0d-125">Use the keyboard shortcut `Ctrl + Alt + T` to open a terminal and run the following commands:</span></span>

```bash
sudo apt-get update
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
sudo apt-get install -y nodejs
sudo apt-get install git
```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="beb0d-126">Instalación de herramientas de desarrollo de Node.js adicionales</span><span class="sxs-lookup"><span data-stu-id="beb0d-126">Install additional Node.js development tools</span></span>
<span data-ttu-id="beb0d-127">Utilice [gulp.js](http://gulpjs.com) para automatizar la implementación de la aplicación de ejemplo en Edison.</span><span class="sxs-lookup"><span data-stu-id="beb0d-127">Use [gulp.js](http://gulpjs.com) to automate the deployment of the sample application to Edison.</span></span>

<span data-ttu-id="beb0d-128">Instale `gulp` ejecutando el comando siguiente en la ventana de terminal:</span><span class="sxs-lookup"><span data-stu-id="beb0d-128">Install `gulp` by running the following command in the terminal:</span></span>

```bash
sudo npm install -g gulp
```

<span data-ttu-id="beb0d-129">Si experimenta problemas al instalar Node.js y estas herramientas de desarrollo adicionales en Ubuntu, consulte la [Guía de solución de problemas][troubleshooting] para ver soluciones a problemas comunes.</span><span class="sxs-lookup"><span data-stu-id="beb0d-129">If you experience issues installing Node.js and these additional development tools on Ubuntu, see the [troubleshooting guide][troubleshooting] for solutions to common problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="beb0d-130">Instalación de Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="beb0d-130">Install Visual Studio Code</span></span>
<span data-ttu-id="beb0d-131">[Descargue](https://code.visualstudio.com/docs/setup/linux) e instale Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="beb0d-131">[Download](https://code.visualstudio.com/docs/setup/linux) and install Visual Studio Code.</span></span> <span data-ttu-id="beb0d-132">Visual Studio Code es un editor de código fuente ligero pero eficaz para Windows, Linux y Mac OS.</span><span class="sxs-lookup"><span data-stu-id="beb0d-132">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="beb0d-133">Use este editor más adelante en el tutorial para editar el código de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="beb0d-133">You use this editor later in the tutorial to edit the sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="beb0d-134">Resumen</span><span class="sxs-lookup"><span data-stu-id="beb0d-134">Summary</span></span>
<span data-ttu-id="beb0d-135">Ha instalado las herramientas de desarrollo y el software necesarios para la primera aplicación de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="beb0d-135">You've installed the required development tools and software for the first sample application.</span></span> <span data-ttu-id="beb0d-136">En la siguiente tarea, creará, implementará y ejecutará la aplicación de ejemplo en Edison.</span><span class="sxs-lookup"><span data-stu-id="beb0d-136">The next task is to create, deploy, and run the sample application on Edison.</span></span>

## <a name="next-steps"></a><span data-ttu-id="beb0d-137">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="beb0d-137">Next steps</span></span>
<span data-ttu-id="beb0d-138">[Creación e implementación de la aplicación de intermitencia de ejemplo][create-and-deploy-the-blink-application]</span><span class="sxs-lookup"><span data-stu-id="beb0d-138">[Create and deploy the blink sample application][create-and-deploy-the-blink-application]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[create-and-deploy-the-blink-application]: iot-hub-intel-edison-kit-node-lesson1-deploy-blink-app.md
[windows]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-mac.md
