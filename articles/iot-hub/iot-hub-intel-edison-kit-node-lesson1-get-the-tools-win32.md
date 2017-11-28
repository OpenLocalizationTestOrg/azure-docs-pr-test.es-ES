---
title: "Conexión de Intel Edison (Node) a Azure IoT: Lección 1: Obtención de las herramientas (Windows) | Microsoft Docs"
description: "Descargue e instale las herramientas y el software necesarios para la primera aplicación de ejemplo de Edison en Windows 7 y versiones posteriores."
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
ms.openlocfilehash: 35b7ae24f8616848eaa6affccb96630603b823b1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-windows-7-or-later"></a><span data-ttu-id="1e8e9-104">Obtención de las herramientas (Windows 7 o posterior)</span><span class="sxs-lookup"><span data-stu-id="1e8e9-104">Get the tools (Windows 7 or later)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="1e8e9-105">[Windows 7 o posterior][windows]</span><span class="sxs-lookup"><span data-stu-id="1e8e9-105">[Windows 7 or later][windows]</span></span>
> * <span data-ttu-id="1e8e9-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="1e8e9-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="1e8e9-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="1e8e9-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="1e8e9-108">Lo que hará</span><span class="sxs-lookup"><span data-stu-id="1e8e9-108">What you will do</span></span>
<span data-ttu-id="1e8e9-109">Descargue las herramientas de desarrollo y el software para la primera aplicación de ejemplo de Intel Edison.</span><span class="sxs-lookup"><span data-stu-id="1e8e9-109">Download the development tools and the software for the first sample application for Intel Edison.</span></span> <span data-ttu-id="1e8e9-110">Si tiene problemas, busque soluciones en [esta página][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="1e8e9-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="1e8e9-111">Lo qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="1e8e9-111">What you will learn</span></span>
<span data-ttu-id="1e8e9-112">En este artículo, aprenderá lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="1e8e9-112">In this article, you will learn:</span></span>

* <span data-ttu-id="1e8e9-113">Cómo instalar Git y Node.js</span><span class="sxs-lookup"><span data-stu-id="1e8e9-113">How to install Git and Node.js.</span></span>
  * <span data-ttu-id="1e8e9-114">[Git](https://git-scm.com) es un sistema de control de versiones distribuido de código.</span><span class="sxs-lookup"><span data-stu-id="1e8e9-114">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="1e8e9-115">La aplicación de ejemplo de este artículo se almacena en Git.</span><span class="sxs-lookup"><span data-stu-id="1e8e9-115">The sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="1e8e9-116">[Node.js](https://nodejs.org/en/) es un entorno de tiempo de ejecución de JavaScript con un amplio ecosistema de paquetes.</span><span class="sxs-lookup"><span data-stu-id="1e8e9-116">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="1e8e9-117">Cómo usar NPM para instalar las herramientas de desarrollo de Node.js adicionales.</span><span class="sxs-lookup"><span data-stu-id="1e8e9-117">How to use NPM to install additional Node.js development tools.</span></span>
  * <span data-ttu-id="1e8e9-118">La versión mínima necesaria de Node.js es 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="1e8e9-118">The minimum version requirement of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="1e8e9-119">[NPM](https://www.npmjs.com) es uno de los administradores de paquetes para Node.js.</span><span class="sxs-lookup"><span data-stu-id="1e8e9-119">[NPM](https://www.npmjs.com) is one of the package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="1e8e9-120">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="1e8e9-120">What you need</span></span>

<span data-ttu-id="1e8e9-121">Para completar esta operación, necesitará:</span><span class="sxs-lookup"><span data-stu-id="1e8e9-121">To complete this operation, you will need:</span></span>

* <span data-ttu-id="1e8e9-122">Una conexión a Internet para descargar el software y las herramientas de desarrollo necesarias</span><span class="sxs-lookup"><span data-stu-id="1e8e9-122">An Internet connection to download the development tools and the software.</span></span>
* <span data-ttu-id="1e8e9-123">Un equipo que ejecute Windows</span><span class="sxs-lookup"><span data-stu-id="1e8e9-123">A computer that is running Windows.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="1e8e9-124">Instalación de Git y Node.js</span><span class="sxs-lookup"><span data-stu-id="1e8e9-124">Install Git and Node.js</span></span>

<span data-ttu-id="1e8e9-125">Haga clic en los vínculos siguientes para descargar e instalar Git y Node.js LTS para Windows.</span><span class="sxs-lookup"><span data-stu-id="1e8e9-125">Click the links below to download and install Git and Node.js LTS for Windows.</span></span>

* [<span data-ttu-id="1e8e9-126">Obtención de Git para Windows</span><span class="sxs-lookup"><span data-stu-id="1e8e9-126">Get Git for Windows</span></span>](https://git-scm.com/download/win/)
* [<span data-ttu-id="1e8e9-127">Obtención de Node.js LTS para Windows</span><span class="sxs-lookup"><span data-stu-id="1e8e9-127">Get Node.js LTS for Windows</span></span>](https://nodejs.org/en/)

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="1e8e9-128">Instalación de herramientas de desarrollo de Node.js adicionales</span><span class="sxs-lookup"><span data-stu-id="1e8e9-128">Install additional Node.js development tools</span></span>

<span data-ttu-id="1e8e9-129">Utilice [gulp.js](http://gulpjs.com) para automatizar la implementación de la aplicación de ejemplo en Edison.</span><span class="sxs-lookup"><span data-stu-id="1e8e9-129">Use [gulp.js](http://gulpjs.com) to automate the deployment of the sample application to Edison.</span></span>

<span data-ttu-id="1e8e9-130">Inicie un símbolo del sistema como administrador.</span><span class="sxs-lookup"><span data-stu-id="1e8e9-130">Start a command prompt as an administrator.</span></span> <span data-ttu-id="1e8e9-131">Instale `gulp` ejecutando el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="1e8e9-131">Install `gulp` by running the following command:</span></span>

```cmd
npm install -g gulp
```

<span data-ttu-id="1e8e9-132">Si experimenta problemas al instalar Node.js y estas herramientas de desarrollo adicionales de Node.js en el equipo, consulte la [Guía de solución de problemas][troubleshooting] para ver soluciones a problemas comunes.</span><span class="sxs-lookup"><span data-stu-id="1e8e9-132">If you experience issues installing Node.js and these additional Node.js development tools on your computer, see the [troubleshooting guide][troubleshooting] for solutions to common problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="1e8e9-133">Instalación de Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="1e8e9-133">Install Visual Studio Code</span></span>

<span data-ttu-id="1e8e9-134">[Descargue](https://code.visualstudio.com/docs/setup/windows) e instale Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="1e8e9-134">[Download](https://code.visualstudio.com/docs/setup/windows) and install Visual Studio Code.</span></span> <span data-ttu-id="1e8e9-135">Visual Studio Code es un editor de código fuente ligero pero eficaz para Windows, Linux y Mac OS.</span><span class="sxs-lookup"><span data-stu-id="1e8e9-135">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="1e8e9-136">Use este editor más adelante en el tutorial para editar el código de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="1e8e9-136">You use this editor later in the tutorial to edit the sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="1e8e9-137">Resumen</span><span class="sxs-lookup"><span data-stu-id="1e8e9-137">Summary</span></span>

<span data-ttu-id="1e8e9-138">Ha instalado las herramientas de desarrollo y el software necesarios para la primera aplicación de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="1e8e9-138">You've installed the required development tools and software for the first sample application.</span></span> <span data-ttu-id="1e8e9-139">En la siguiente tarea, creará, implementará y ejecutará la aplicación de ejemplo en Edison.</span><span class="sxs-lookup"><span data-stu-id="1e8e9-139">The next task is to create, deploy, and run the sample application on Edison.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1e8e9-140">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1e8e9-140">Next steps</span></span>

<span data-ttu-id="1e8e9-141">[Creación e implementación de la aplicación de intermitencia][create-and-deploy-the-blink-application]</span><span class="sxs-lookup"><span data-stu-id="1e8e9-141">[Create and deploy the blink application][create-and-deploy-the-blink-application]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[create-and-deploy-the-blink-application]: iot-hub-intel-edison-kit-node-lesson1-deploy-blink-app.md
[windows]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-mac.md
