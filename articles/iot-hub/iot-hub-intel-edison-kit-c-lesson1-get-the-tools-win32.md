---
title: "Conexión de Intel Edison (C) a Azure IoT: Lección 1: Obtención de las herramientas (Windows) | Microsoft Docs"
description: "Descargue e instale las herramientas y el software necesarios para la primera aplicación de ejemplo de Edison en Windows 7 y versiones posteriores."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: herramientas de desarrollo de Arduino, desarrollo de iot, software de iot, software de internet de las cosas, instalar git en Windows, instalar node js Windows
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: 7d29a358-544d-4657-a504-5ed9b79c2925
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: f9d614d17f262b81a75d6128cbc5898dc18ab906
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-windows-7-or-later"></a><span data-ttu-id="04cc5-104">Obtención de las herramientas (Windows 7 o posterior)</span><span class="sxs-lookup"><span data-stu-id="04cc5-104">Get the tools (Windows 7 or later)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="04cc5-105">[Windows 7 o posterior][windows]</span><span class="sxs-lookup"><span data-stu-id="04cc5-105">[Windows 7 or later][windows]</span></span>
> * <span data-ttu-id="04cc5-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="04cc5-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="04cc5-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="04cc5-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="04cc5-108">Lo que hará</span><span class="sxs-lookup"><span data-stu-id="04cc5-108">What you will do</span></span>
<span data-ttu-id="04cc5-109">Descargue las herramientas de desarrollo y el software para la primera aplicación de ejemplo de Intel Edison.</span><span class="sxs-lookup"><span data-stu-id="04cc5-109">Download the development tools and the software for the first sample application for Intel Edison.</span></span> <span data-ttu-id="04cc5-110">Si tiene problemas, busque soluciones en [esta página][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="04cc5-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

> [!NOTE]
> <span data-ttu-id="04cc5-111">Aunque el lenguaje de programación de la lógica principal es C, las herramientas de Node.js se usan en las lecciones para compilar e implementar aplicaciones de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="04cc5-111">Although the programming language of the main logic is C, Node.js tools are used in the lessons to build and deploy sample applications.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="04cc5-112">Lo qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="04cc5-112">What you will learn</span></span>
<span data-ttu-id="04cc5-113">En este artículo, aprenderá lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="04cc5-113">In this article, you will learn:</span></span>

* <span data-ttu-id="04cc5-114">Cómo instalar Git y Node.js</span><span class="sxs-lookup"><span data-stu-id="04cc5-114">How to install Git and Node.js.</span></span>
  * <span data-ttu-id="04cc5-115">[Git](https://git-scm.com) es un sistema de control de versiones distribuido de código.</span><span class="sxs-lookup"><span data-stu-id="04cc5-115">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="04cc5-116">La aplicación de ejemplo de este artículo se almacena en Git.</span><span class="sxs-lookup"><span data-stu-id="04cc5-116">The sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="04cc5-117">[Node.js](https://nodejs.org/en/) es un entorno de tiempo de ejecución de JavaScript con un amplio ecosistema de paquetes.</span><span class="sxs-lookup"><span data-stu-id="04cc5-117">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="04cc5-118">Cómo usar NPM para instalar las herramientas de desarrollo de Node.js adicionales.</span><span class="sxs-lookup"><span data-stu-id="04cc5-118">How to use NPM to install additional Node.js development tools.</span></span>
  * <span data-ttu-id="04cc5-119">La versión mínima necesaria de Node.js es 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="04cc5-119">The minimum version requirement of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="04cc5-120">[NPM](https://www.npmjs.com) es uno de los administradores de paquetes para Node.js.</span><span class="sxs-lookup"><span data-stu-id="04cc5-120">[NPM](https://www.npmjs.com) is one of the package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="04cc5-121">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="04cc5-121">What you need</span></span>

<span data-ttu-id="04cc5-122">Para completar esta operación, necesitará:</span><span class="sxs-lookup"><span data-stu-id="04cc5-122">To complete this operation, you will need:</span></span>

* <span data-ttu-id="04cc5-123">Una conexión a Internet para descargar el software y las herramientas de desarrollo necesarias</span><span class="sxs-lookup"><span data-stu-id="04cc5-123">An Internet connection to download the development tools and the software.</span></span>
* <span data-ttu-id="04cc5-124">Un equipo que ejecute Windows</span><span class="sxs-lookup"><span data-stu-id="04cc5-124">A computer that is running Windows.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="04cc5-125">Instalación de Git y Node.js</span><span class="sxs-lookup"><span data-stu-id="04cc5-125">Install Git and Node.js</span></span>

<span data-ttu-id="04cc5-126">Haga clic en los vínculos siguientes para descargar e instalar Git y Node.js LTS para Windows.</span><span class="sxs-lookup"><span data-stu-id="04cc5-126">Click the links below to download and install Git and Node.js LTS for Windows.</span></span>

* [<span data-ttu-id="04cc5-127">Obtención de Git para Windows</span><span class="sxs-lookup"><span data-stu-id="04cc5-127">Get Git for Windows</span></span>](https://git-scm.com/download/win/)
* [<span data-ttu-id="04cc5-128">Obtención de Node.js LTS para Windows</span><span class="sxs-lookup"><span data-stu-id="04cc5-128">Get Node.js LTS for Windows</span></span>](https://nodejs.org/en/)

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="04cc5-129">Instalación de herramientas de desarrollo de Node.js adicionales</span><span class="sxs-lookup"><span data-stu-id="04cc5-129">Install additional Node.js development tools</span></span>

<span data-ttu-id="04cc5-130">Utilice [gulp.js](http://gulpjs.com) para automatizar la implementación de la aplicación de ejemplo en Edison.</span><span class="sxs-lookup"><span data-stu-id="04cc5-130">Use [gulp.js](http://gulpjs.com) to automate the deployment of the sample application to Edison.</span></span>

<span data-ttu-id="04cc5-131">Inicie un símbolo del sistema como administrador.</span><span class="sxs-lookup"><span data-stu-id="04cc5-131">Start a command prompt as an administrator.</span></span> <span data-ttu-id="04cc5-132">Instale `gulp` ejecutando el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="04cc5-132">Install `gulp` by running the following command:</span></span>

```cmd
npm install -g gulp
```

<span data-ttu-id="04cc5-133">Si experimenta problemas al instalar Node.js y estas herramientas de desarrollo adicionales de Node.js en el equipo, consulte la [Guía de solución de problemas][troubleshooting] para ver soluciones a problemas comunes.</span><span class="sxs-lookup"><span data-stu-id="04cc5-133">If you experience issues installing Node.js and these additional Node.js development tools on your computer, see the [troubleshooting guide][troubleshooting] for solutions to common problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="04cc5-134">Instalación de Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="04cc5-134">Install Visual Studio Code</span></span>

<span data-ttu-id="04cc5-135">[Descargue](https://code.visualstudio.com/docs/setup/windows) e instale Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="04cc5-135">[Download](https://code.visualstudio.com/docs/setup/windows) and install Visual Studio Code.</span></span> <span data-ttu-id="04cc5-136">Visual Studio Code es un editor de código fuente ligero pero eficaz para Windows, Linux y Mac OS.</span><span class="sxs-lookup"><span data-stu-id="04cc5-136">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="04cc5-137">Use este editor más adelante en el tutorial para editar el código de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="04cc5-137">You use this editor later in the tutorial to edit the sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="04cc5-138">Resumen</span><span class="sxs-lookup"><span data-stu-id="04cc5-138">Summary</span></span>

<span data-ttu-id="04cc5-139">Ha instalado las herramientas de desarrollo y el software necesarios para la primera aplicación de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="04cc5-139">You've installed the required development tools and software for the first sample application.</span></span> <span data-ttu-id="04cc5-140">En la siguiente tarea, creará, implementará y ejecutará la aplicación de ejemplo en Edison.</span><span class="sxs-lookup"><span data-stu-id="04cc5-140">The next task is to create, deploy, and run the sample application on Edison.</span></span>

## <a name="next-steps"></a><span data-ttu-id="04cc5-141">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="04cc5-141">Next steps</span></span>

<span data-ttu-id="04cc5-142">[Creación e implementación de la aplicación de intermitencia][create-and-deploy-the-blink-application]</span><span class="sxs-lookup"><span data-stu-id="04cc5-142">[Create and deploy the blink application][create-and-deploy-the-blink-application]</span></span>

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[create-and-deploy-the-blink-application]: iot-hub-intel-edison-kit-c-lesson1-deploy-blink-app.md
[windows]: iot-hub-intel-edison-kit-c-lesson1-get-the-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-c-lesson1-get-the-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-c-lesson1-get-the-tools-mac.md
