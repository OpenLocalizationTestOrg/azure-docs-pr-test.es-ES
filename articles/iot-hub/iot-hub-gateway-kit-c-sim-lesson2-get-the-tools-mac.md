---
title: "Dispositivo simulado y puerta de enlace de Azure IoT: Lección 2: Obtención de las herramientas (macOS) | Microsoft Docs"
description: Instale herramientas en su equipo Mac, cree una instancia de IoT Hub y registre su dispositivo en ella.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: desarrollo de iot, software de iot, servicio en la nube de iot, software de internet de las cosas, cli de azure, instalar python mac, instalar git en mac, ejecutar gulp, instalar node js mac
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 42f9d186-e20c-4ef9-98cc-71d39e058b06
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: d86332816130de7a6951a74ceb215c8ce476d5f8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-macos"></a><span data-ttu-id="7b7f8-104">Obtención de las herramientas (Mac OS)</span><span class="sxs-lookup"><span data-stu-id="7b7f8-104">Get the tools (macOS)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7b7f8-105">Windows 7 o posterior</span><span class="sxs-lookup"><span data-stu-id="7b7f8-105">Windows 7 or later</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)
> * [<span data-ttu-id="7b7f8-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="7b7f8-106">Ubuntu 16.04</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="7b7f8-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="7b7f8-107">macOS 10.10</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="7b7f8-108">Lo que hará</span><span class="sxs-lookup"><span data-stu-id="7b7f8-108">What you will do</span></span>

- <span data-ttu-id="7b7f8-109">Instale Git, Node.js, Gulp y Python.</span><span class="sxs-lookup"><span data-stu-id="7b7f8-109">Install Git, Node.js, Gulp, Python.</span></span>
- <span data-ttu-id="7b7f8-110">Instalación de la interfaz de la línea de comandos de Azure (CLI de Azure)</span><span class="sxs-lookup"><span data-stu-id="7b7f8-110">Install the Azure command-line interface (Azure CLI).</span></span> 

<span data-ttu-id="7b7f8-111">Si tiene problemas, busque soluciones en la [página de solución de problemas](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="7b7f8-111">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="7b7f8-112">Lo qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="7b7f8-112">What you will learn</span></span>

<span data-ttu-id="7b7f8-113">En esta lección, aprenderá lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="7b7f8-113">In this lesson, you will learn:</span></span>

- <span data-ttu-id="7b7f8-114">Instalación de [Git](https://git-scm.com/) y [Node.js](https://nodejs.org/en/).</span><span class="sxs-lookup"><span data-stu-id="7b7f8-114">How to install [Git](https://git-scm.com/) and [Node.js](https://nodejs.org/en/).</span></span>
  - <span data-ttu-id="7b7f8-115">Git es un sistema de control de versiones distribuido de código abierto.</span><span class="sxs-lookup"><span data-stu-id="7b7f8-115">Git is an open source distributed version control system.</span></span> <span data-ttu-id="7b7f8-116">La aplicación de ejemplo de esta lección se almacena en Git.</span><span class="sxs-lookup"><span data-stu-id="7b7f8-116">The sample application for this lesson is stored on Git.</span></span>
  - <span data-ttu-id="7b7f8-117">Node.js es un entorno en tiempo de ejecución de JavaScript con un amplio ecosistema de paquetes.</span><span class="sxs-lookup"><span data-stu-id="7b7f8-117">Node.js is a JavaScript runtime with a rich package ecosystem.</span></span>
- <span data-ttu-id="7b7f8-118">Uso de [NPM](https://www.npmjs.com/) para instalar las herramientas de desarrollo de Node.js.</span><span class="sxs-lookup"><span data-stu-id="7b7f8-118">How to use [NPM](https://www.npmjs.com/) to install Node.js development tools.</span></span>
  - <span data-ttu-id="7b7f8-119">La versión mínima necesaria de Node.js es 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="7b7f8-119">The minimum required version of Node.js is 4.5 LTS.</span></span>
  - <span data-ttu-id="7b7f8-120">NPM es uno de los administradores de paquetes para Node.js.</span><span class="sxs-lookup"><span data-stu-id="7b7f8-120">NPM is one of the package managers for Node.js.</span></span>
- <span data-ttu-id="7b7f8-121">Instalación de Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="7b7f8-121">How to install Visual Studio Code.</span></span>
  - <span data-ttu-id="7b7f8-122">Visual Studio Code es un editor de código fuente multiplataforma ligero pero eficaz para Windows, Linux y macOS.</span><span class="sxs-lookup"><span data-stu-id="7b7f8-122">Visual Studio Code is a cross platform, lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="7b7f8-123">Ofrece un elevado nivel de compatibilidad para la depuración, control de Git insertado, resaltado de sintaxis, función inteligente de autocompletar código, fragmentos de código y refactorización de código.</span><span class="sxs-lookup"><span data-stu-id="7b7f8-123">It has great support for debugging, embedded Git control, syntax highlighting, intelligent code completion, snippets, and code refactoring as well.</span></span>
- <span data-ttu-id="7b7f8-124">Cómo instalar Python.</span><span class="sxs-lookup"><span data-stu-id="7b7f8-124">How to install Python.</span></span>
  - <span data-ttu-id="7b7f8-125">Python es un lenguaje de programación general, muy usado, destinado a fines genéricos, interpretado y dinámico.</span><span class="sxs-lookup"><span data-stu-id="7b7f8-125">Python is a widely used high-level, general-purpose, interpreted and dynamic programming language.</span></span>
- <span data-ttu-id="7b7f8-126">Cómo instalar la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="7b7f8-126">How to install the Azure CLI.</span></span>
  - <span data-ttu-id="7b7f8-127">La CLI de Azure proporciona una experiencia de línea de comandos multiplataforma en Azure.</span><span class="sxs-lookup"><span data-stu-id="7b7f8-127">The Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="7b7f8-128">De este modo, puede trabajar directamente desde la línea de comandos para aprovisionar y administrar los recursos.</span><span class="sxs-lookup"><span data-stu-id="7b7f8-128">You work directly from a command line to provision and manage resources.</span></span>
- <span data-ttu-id="7b7f8-129">Uso de la CLI de Azure para crear una instancia de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="7b7f8-129">How to use the Azure CLI to create an IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="7b7f8-130">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="7b7f8-130">What you need</span></span>

- <span data-ttu-id="7b7f8-131">Una conexión a Internet para descargar las herramientas y el software.</span><span class="sxs-lookup"><span data-stu-id="7b7f8-131">An Internet connection to download the tools and software.</span></span>
- <span data-ttu-id="7b7f8-132">Un equipo Mac con OS X Yosemite (10.10) o posterior.</span><span class="sxs-lookup"><span data-stu-id="7b7f8-132">A Mac computer that’s running OS X Yosemite (10.10) or later.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="7b7f8-133">Instalación de Git y Node.js</span><span class="sxs-lookup"><span data-stu-id="7b7f8-133">Install Git and Node.js</span></span>

<span data-ttu-id="7b7f8-134">Para instalar Git y Node.js, use la utilidad de administración de paquetes Homebrew siguiendo estos pasos:</span><span class="sxs-lookup"><span data-stu-id="7b7f8-134">To install Git and Node.js, use the Homebrew package management utility by following these steps:</span></span>

1. <span data-ttu-id="7b7f8-135">[Descargue](http://brew.sh/) e instale Homebrew.</span><span class="sxs-lookup"><span data-stu-id="7b7f8-135">[Download](http://brew.sh/) and install Homebrew.</span></span> <span data-ttu-id="7b7f8-136">Si ya ha instalado Homebrew, vaya al paso 2.</span><span class="sxs-lookup"><span data-stu-id="7b7f8-136">If you’ve already installed Homebrew, go to step 2.</span></span>
   1. <span data-ttu-id="7b7f8-137">Presione `Cmd + Space` y escriba `Terminal` para abrir una ventana de terminal.</span><span class="sxs-lookup"><span data-stu-id="7b7f8-137">Press `Cmd + Space` and enter `Terminal` to open a terminal.</span></span>
   2. <span data-ttu-id="7b7f8-138">Ejecute el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="7b7f8-138">Run the following command:</span></span>

      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```

2. <span data-ttu-id="7b7f8-139">Instale Git y Node.js ejecutando el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="7b7f8-139">Install Git and Node.js by running the following command:</span></span>

    ```bash
    brew install node git
    ```

## <a name="install-nodejs-development-tools"></a><span data-ttu-id="7b7f8-140">Instalación de herramientas de desarrollo de Node.js</span><span class="sxs-lookup"><span data-stu-id="7b7f8-140">Install Node.js development tools</span></span>

<span data-ttu-id="7b7f8-141">Use [gulp.js](http://gulpjs.com/) para automatizar la implementación y ejecución de scripts.</span><span class="sxs-lookup"><span data-stu-id="7b7f8-141">You use [gulp.js](http://gulpjs.com/) to automate deployment and execution of scripts.</span></span>

<span data-ttu-id="7b7f8-142">Para instalar Gulp, ejecute el comando siguiente en una ventana del terminal:</span><span class="sxs-lookup"><span data-stu-id="7b7f8-142">To install gulp, run the following command in the terminal:</span></span>

```bash
npm install -g gulp
```

<span data-ttu-id="7b7f8-143">Si tiene problemas con la instalación, consulte la [guía de solución de problemas](iot-hub-gateway-kit-c-sim-troubleshooting.md) para solucionar problemas comunes.</span><span class="sxs-lookup"><span data-stu-id="7b7f8-143">If you experience issues with the installation, see the [troubleshooting guide](iot-hub-gateway-kit-c-sim-troubleshooting.md) for solutions to common problems.</span></span>

> [!Note]
> <span data-ttu-id="7b7f8-144">Se precisan Node, NPM y Gulp para ejecutar scripts de automatización desarrollados en Node.js.</span><span class="sxs-lookup"><span data-stu-id="7b7f8-144">Node, NPM and Gulp are required to run automation scripts developed in Node.js.</span></span>

## <a name="install-python"></a><span data-ttu-id="7b7f8-145">Instalación de Python</span><span class="sxs-lookup"><span data-stu-id="7b7f8-145">Install Python</span></span>

<span data-ttu-id="7b7f8-146">Aunque Mac OS X incluye Python 2.7 de serie, se recomienda instalar Python mediante Homebrew.</span><span class="sxs-lookup"><span data-stu-id="7b7f8-146">Although Mac OS X comes with Python 2.7, we recommend that you install Python through Homebrew.</span></span> <span data-ttu-id="7b7f8-147">Consulte [Installing Python on Mac OS X](http://docs.python-guide.org/en/latest/starting/install/osx/) (Instalación de Python en Mac OS X).</span><span class="sxs-lookup"><span data-stu-id="7b7f8-147">See [Installing Python on Mac OS X](http://docs.python-guide.org/en/latest/starting/install/osx/).</span></span>

<span data-ttu-id="7b7f8-148">Instale Python y pip ejecutando el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="7b7f8-148">Install Python and pip by running the following command:</span></span>

```bash
brew install python
```

## <a name="install-the-azure-cli"></a><span data-ttu-id="7b7f8-149">Instalación de la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="7b7f8-149">Install the Azure CLI</span></span>

<span data-ttu-id="7b7f8-150">Para instalar la CLI de Azure, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="7b7f8-150">To install the Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="7b7f8-151">Ejecute los siguientes comandos en una ventana de terminal:</span><span class="sxs-lookup"><span data-stu-id="7b7f8-151">Run the following commands in the terminal:</span></span>
   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
   <span data-ttu-id="7b7f8-152">La instalación puede tardar 5 minutos.</span><span class="sxs-lookup"><span data-stu-id="7b7f8-152">The installation might take 5 minutes.</span></span>

2. <span data-ttu-id="7b7f8-153">Compruebe la instalación ejecutando el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="7b7f8-153">Verify the installation by running the following command:</span></span>
   ```bash
   az iot -h
   ```
   <span data-ttu-id="7b7f8-154">Si la instalación se realiza correctamente, verá el siguiente resultado.</span><span class="sxs-lookup"><span data-stu-id="7b7f8-154">You should see the following output if the installation is successful.</span></span>

   ![Verificación de la instalación de la CLI de Azure](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_osx.png)

## <a name="install-visual-studio-code"></a><span data-ttu-id="7b7f8-156">Instalación de Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="7b7f8-156">Install Visual Studio Code</span></span>

<span data-ttu-id="7b7f8-157">Use Visual Studio Code, como se explica más adelante en este tutorial, para editar los archivos de configuración.</span><span class="sxs-lookup"><span data-stu-id="7b7f8-157">You use Visual Studio Code later in the tutorial to edit configuration files.</span></span>

<span data-ttu-id="7b7f8-158">[Descargue](https://code.visualstudio.com/docs/setup/osx) e instale Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="7b7f8-158">[Download](https://code.visualstudio.com/docs/setup/osx) and install Visual Studio Code.</span></span>

## <a name="summary"></a><span data-ttu-id="7b7f8-159">Resumen</span><span class="sxs-lookup"><span data-stu-id="7b7f8-159">Summary</span></span>

<span data-ttu-id="7b7f8-160">Ha instalado todas las herramientas y el software necesarios en el equipo Mac.</span><span class="sxs-lookup"><span data-stu-id="7b7f8-160">You’ve installed all the required tools and software on your Mac computer.</span></span> <span data-ttu-id="7b7f8-161">La siguiente tarea consiste en utilizar la CLI de Azure para crear una instancia de IoT Hub y registrar el dispositivo en ella.</span><span class="sxs-lookup"><span data-stu-id="7b7f8-161">Your next task is to use the Azure CLI to create an IoT hub and register your device in your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7b7f8-162">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7b7f8-162">Next steps</span></span>
[<span data-ttu-id="7b7f8-163">Creación de una instancia de IoT Hub y registro del dispositivo</span><span class="sxs-lookup"><span data-stu-id="7b7f8-163">Create an IoT hub and register Device</span></span>](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)
