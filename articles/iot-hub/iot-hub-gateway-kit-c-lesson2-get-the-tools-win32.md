---
title: "Dispositivo SensorTag y puerta de enlace de Azure IoT: Lección 2: Obtención de las herramientas (Windows) | Microsoft Docs"
description: Instale las herramientas y el software en el equipo host que ejecuta Windows, cree una instancia de IoT Hub y registre el dispositivo en ella.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "desarrollo de iot, software de iot, servicio en la nube de iot, software de internet de las cosas, cli de azure, instalar git en windows, ejecución de gulp, instalar node js windows, instalar npm en windows, instalar python en windows"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 18ae6ee4-574a-4d5f-9838-ca2a78165628
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 0d8ba03df63d0b8657a9e275fc636e806c66b683
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-windows-7-and-later"></a><span data-ttu-id="c9443-104">Obtención de las herramientas (Windows 7 y posterior)</span><span class="sxs-lookup"><span data-stu-id="c9443-104">Get the tools (Windows 7 and later)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c9443-105">Windows 7 o posterior</span><span class="sxs-lookup"><span data-stu-id="c9443-105">Windows 7 or later</span></span>](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)
> * [<span data-ttu-id="c9443-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="c9443-106">Ubuntu 16.04</span></span>](iot-hub-gateway-kit-c-lesson2-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="c9443-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="c9443-107">macOS 10.10</span></span>](iot-hub-gateway-kit-c-lesson2-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="c9443-108">Lo que hará</span><span class="sxs-lookup"><span data-stu-id="c9443-108">What you will do</span></span>

- <span data-ttu-id="c9443-109">Instale Git, Node.js, Gulp y Python.</span><span class="sxs-lookup"><span data-stu-id="c9443-109">Install Git, Node.js, Gulp, Python.</span></span>
- <span data-ttu-id="c9443-110">Instalación de la interfaz de la línea de comandos de Azure (CLI de Azure)</span><span class="sxs-lookup"><span data-stu-id="c9443-110">Install the Azure command-line interface (Azure CLI).</span></span> 

<span data-ttu-id="c9443-111">Si tiene problemas, busque soluciones en la [página de solución de problemas](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="c9443-111">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="c9443-112">Lo qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="c9443-112">What you will learn</span></span>

<span data-ttu-id="c9443-113">En esta lección, aprenderá lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="c9443-113">In this lesson, you will learn:</span></span>

- <span data-ttu-id="c9443-114">Instalación de [Git](https://git-scm.com/) y [Node.js](https://nodejs.org/en/).</span><span class="sxs-lookup"><span data-stu-id="c9443-114">How to install [Git](https://git-scm.com/) and [Node.js](https://nodejs.org/en/).</span></span>
  - <span data-ttu-id="c9443-115">Git es un sistema de control de versiones distribuido de código abierto.</span><span class="sxs-lookup"><span data-stu-id="c9443-115">Git is an open source distributed version control system.</span></span> <span data-ttu-id="c9443-116">La aplicación de ejemplo de esta lección se almacena en Git.</span><span class="sxs-lookup"><span data-stu-id="c9443-116">The sample application for this lesson is stored on Git.</span></span>
  - <span data-ttu-id="c9443-117">Node.js es un entorno en tiempo de ejecución de JavaScript con un amplio ecosistema de paquetes.</span><span class="sxs-lookup"><span data-stu-id="c9443-117">Node.js is a JavaScript runtime with a rich package ecosystem.</span></span>
- <span data-ttu-id="c9443-118">Uso de [NPM](https://www.npmjs.com/) para instalar las herramientas de desarrollo de Node.js.</span><span class="sxs-lookup"><span data-stu-id="c9443-118">How to use [NPM](https://www.npmjs.com/) to install Node.js development tools.</span></span>
  - <span data-ttu-id="c9443-119">La versión mínima necesaria de Node.js es 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="c9443-119">The minimum required version of Node.js is 4.5 LTS.</span></span>
  - <span data-ttu-id="c9443-120">NPM es uno de los administradores de paquetes para Node.js.</span><span class="sxs-lookup"><span data-stu-id="c9443-120">NPM is one of the package managers for Node.js.</span></span>
- <span data-ttu-id="c9443-121">Instalación de Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="c9443-121">How to install Visual Studio Code.</span></span>
  - <span data-ttu-id="c9443-122">Visual Studio Code es un editor de código fuente multiplataforma ligero pero eficaz para Windows, Linux y macOS.</span><span class="sxs-lookup"><span data-stu-id="c9443-122">Visual Studio Code is a cross platform, lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="c9443-123">Ofrece un elevado nivel de compatibilidad para la depuración, control de Git insertado, resaltado de sintaxis, función inteligente de autocompletar código, fragmentos de código y refactorización de código.</span><span class="sxs-lookup"><span data-stu-id="c9443-123">It has great support for debugging, embedded Git control, syntax highlighting, intelligent code completion, snippets, and code refactoring as well.</span></span>
- <span data-ttu-id="c9443-124">Cómo instalar Python.</span><span class="sxs-lookup"><span data-stu-id="c9443-124">How to install Python.</span></span>
  - <span data-ttu-id="c9443-125">Python es un lenguaje de programación general, muy usado, destinado a fines genéricos, interpretado y dinámico.</span><span class="sxs-lookup"><span data-stu-id="c9443-125">Python is a widely used high-level, general-purpose, interpreted and dynamic programming language.</span></span>
- <span data-ttu-id="c9443-126">Cómo instalar la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="c9443-126">How to install the Azure CLI.</span></span>
  - <span data-ttu-id="c9443-127">La CLI de Azure proporciona una experiencia de línea de comandos multiplataforma en Azure.</span><span class="sxs-lookup"><span data-stu-id="c9443-127">The Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="c9443-128">De este modo, puede trabajar directamente desde la línea de comandos para aprovisionar y administrar los recursos.</span><span class="sxs-lookup"><span data-stu-id="c9443-128">You work directly from a command line to provision and manage resources.</span></span>
- <span data-ttu-id="c9443-129">Uso de la CLI de Azure para crear una instancia de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="c9443-129">How to use the Azure CLI to create an IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="c9443-130">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="c9443-130">What you need</span></span>

- <span data-ttu-id="c9443-131">Una conexión a Internet para descargar las herramientas y el software.</span><span class="sxs-lookup"><span data-stu-id="c9443-131">An Internet connection to download the tools and software.</span></span>
- <span data-ttu-id="c9443-132">Un equipo Windows.</span><span class="sxs-lookup"><span data-stu-id="c9443-132">A Windows computer.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="c9443-133">Instalación de Git y Node.js</span><span class="sxs-lookup"><span data-stu-id="c9443-133">Install Git and Node.js</span></span>

<span data-ttu-id="c9443-134">Haga clic en los vínculos siguientes para descargar e instalar Git y Node.js LTS para Windows.</span><span class="sxs-lookup"><span data-stu-id="c9443-134">Click the following links to download and install Git and Node.js LTS for Windows.</span></span>

- [<span data-ttu-id="c9443-135">Obtención de Git para Windows</span><span class="sxs-lookup"><span data-stu-id="c9443-135">Get Git for Windows</span></span>](https://git-scm.com/download/win/)
- [<span data-ttu-id="c9443-136">Obtención de Node.js LTS para Windows</span><span class="sxs-lookup"><span data-stu-id="c9443-136">Get Node.js LTS for Windows</span></span>](https://nodejs.org/en/)

## <a name="install-nodejs-development-tools"></a><span data-ttu-id="c9443-137">Instalación de herramientas de desarrollo de Node.js</span><span class="sxs-lookup"><span data-stu-id="c9443-137">Install Node.js development tools</span></span>

<span data-ttu-id="c9443-138">Use [gulp.js](http://gulpjs.com/) para automatizar la implementación y ejecución de scripts.</span><span class="sxs-lookup"><span data-stu-id="c9443-138">You use [gulp.js](http://gulpjs.com/) to automate deployment and execution of scripts.</span></span>

<span data-ttu-id="c9443-139">Presione `Windows + R`, escriba `cmd` y presione `Enter` para abrir una ventana del símbolo del sistema y, después, ejecute el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="c9443-139">Press `Windows + R`, type `cmd` and press `Enter` to open a Command Prompt window, and then run the following command:</span></span>

```cmd
npm install -g gulp
```

<span data-ttu-id="c9443-140">Si tiene problemas con la instalación, consulte la [guía de solución de problemas](iot-hub-gateway-kit-c-troubleshooting.md) para solucionar problemas comunes.</span><span class="sxs-lookup"><span data-stu-id="c9443-140">If you experience issues with the installation, see the [troubleshooting guide](iot-hub-gateway-kit-c-troubleshooting.md) for solutions to common problems.</span></span>

> [!Note]
> <span data-ttu-id="c9443-141">Se precisan Node, NPM y Gulp para ejecutar scripts de automatización desarrollados en Node.js.</span><span class="sxs-lookup"><span data-stu-id="c9443-141">Node, NPM and Gulp are required to run automation scripts developed in Node.js.</span></span>

## <a name="install-python"></a><span data-ttu-id="c9443-142">Instalación de Python</span><span class="sxs-lookup"><span data-stu-id="c9443-142">Install Python</span></span>

<span data-ttu-id="c9443-143">Puede elegir entre Python 2.7, 3.4 o 3.5.</span><span class="sxs-lookup"><span data-stu-id="c9443-143">You can choose from Python 2.7, 3.4 or 3.5.</span></span> <span data-ttu-id="c9443-144">En este tutorial, se usa Python 2.7.</span><span class="sxs-lookup"><span data-stu-id="c9443-144">In this tutorial, we use Python 2.7.</span></span> <span data-ttu-id="c9443-145">Si ya ha instalado Python, vaya a la siguiente sección.</span><span class="sxs-lookup"><span data-stu-id="c9443-145">If you've already installed python, go to the next section.</span></span>

[<span data-ttu-id="c9443-146">Obtención de Python para Windows</span><span class="sxs-lookup"><span data-stu-id="c9443-146">Get Python for Windows</span></span>](https://www.python.org/downloads/)

<span data-ttu-id="c9443-147">También debe agregar la ruta de acceso de las carpetas donde se instalan Python.exe y pip.exe a la variable de entorno `PATH` del sistema.</span><span class="sxs-lookup"><span data-stu-id="c9443-147">You also need to add the path of the folders where Python.exe and pip.exe are installed to the system `PATH` environment variable.</span></span> <span data-ttu-id="c9443-148">De forma predeterminada, se instala python.exe en `C:\Python27` y pip.exe en `C:\Python27\Scripts`.</span><span class="sxs-lookup"><span data-stu-id="c9443-148">By default, python.exe is installed in `C:\Python27` and pip.exe is installed in `C:\Python27\Scripts`.</span></span>

## <a name="install-the-azure-cli"></a><span data-ttu-id="c9443-149">Instalación de la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="c9443-149">Install the Azure CLI</span></span>

<span data-ttu-id="c9443-150">Para instalar la CLI de Azure, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="c9443-150">To install the Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="c9443-151">Abra una ventana de símbolo del sistema como administrador.</span><span class="sxs-lookup"><span data-stu-id="c9443-151">Open a Command Prompt window as an administrator.</span></span>

2. <span data-ttu-id="c9443-152">Instale la CLI de Azure ejecutando el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="c9443-152">Install the Azure CLI by running the following commands:</span></span>

   ```cmd
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```

   <span data-ttu-id="c9443-153">La instalación puede tardar 5 minutos.</span><span class="sxs-lookup"><span data-stu-id="c9443-153">The installation might take 5 minutes.</span></span>

3. <span data-ttu-id="c9443-154">Compruebe la instalación ejecutando el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="c9443-154">Verify the installation by running the following command:</span></span>

   ```cmd
   az iot -h
   ```

   <span data-ttu-id="c9443-155">Si la instalación se realiza correctamente, verá el siguiente resultado.</span><span class="sxs-lookup"><span data-stu-id="c9443-155">You should see the following output if the installation is successful.</span></span>

   ![Verificación de la instalación de la CLI de Azure](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_win.png)

## <a name="install-visual-studio-code"></a><span data-ttu-id="c9443-157">Instalación de Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="c9443-157">Install Visual Studio Code</span></span>

<span data-ttu-id="c9443-158">Use Visual Studio Code, como se explica más adelante en este tutorial, para editar los archivos de configuración.</span><span class="sxs-lookup"><span data-stu-id="c9443-158">You use Visual Studio Code later in the tutorial to edit configuration files.</span></span>

<span data-ttu-id="c9443-159">[Descargue](https://code.visualstudio.com/docs/setup/windows) e instale Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="c9443-159">[Download](https://code.visualstudio.com/docs/setup/windows) and install Visual Studio Code.</span></span>

## <a name="summary"></a><span data-ttu-id="c9443-160">Resumen</span><span class="sxs-lookup"><span data-stu-id="c9443-160">Summary</span></span>

<span data-ttu-id="c9443-161">Ha instalado todas las herramientas y el software necesarios en el equipo host.</span><span class="sxs-lookup"><span data-stu-id="c9443-161">You've installed all the required tools and software on your host computer.</span></span> <span data-ttu-id="c9443-162">La siguiente tarea consiste en utilizar la CLI de Azure para crear una instancia de IoT Hub y registrar el dispositivo en ella.</span><span class="sxs-lookup"><span data-stu-id="c9443-162">Your next task is to use the Azure CLI to create an IoT hub and register your device in your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c9443-163">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c9443-163">Next steps</span></span>
[<span data-ttu-id="c9443-164">Creación de una instancia de IoT Hub y registro del dispositivo</span><span class="sxs-lookup"><span data-stu-id="c9443-164">Create an IoT hub and register your device</span></span>](iot-hub-gateway-kit-c-lesson2-register-device.md)
