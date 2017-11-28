---
title: "Dispositivo simulado y puerta de enlace de Azure IoT: Lección 2: Obtención de las herramientas (Ubuntu) | Microsoft Docs"
description: Instale las herramientas y el software en el equipo host que ejecuta Ubuntu, cree una instancia de IoT Hub y registre el dispositivo en ella.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "desarrollo de iot, software de iot, servicio en la nube de iot, software de internet de las cosas, cli de azure, instalar git en ubuntu, ejecución de gulp, instalar node js ubuntu"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: cf673154-ce67-4ed7-a9f7-2440301c6270
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 349daf5c3206f7fc20662beebd16928624142a56
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-ubuntu-1604"></a><span data-ttu-id="be3fe-104">Obtención de las herramientas (Ubuntu 16.04)</span><span class="sxs-lookup"><span data-stu-id="be3fe-104">Get the tools (Ubuntu 16.04)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="be3fe-105">Windows 7 o posterior</span><span class="sxs-lookup"><span data-stu-id="be3fe-105">Windows 7 or later</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)
> * [<span data-ttu-id="be3fe-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="be3fe-106">Ubuntu 16.04</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="be3fe-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="be3fe-107">macOS 10.10</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="be3fe-108">Lo que hará</span><span class="sxs-lookup"><span data-stu-id="be3fe-108">What you will do</span></span>

- <span data-ttu-id="be3fe-109">Instale Git, Node.js, Gulp y Python.</span><span class="sxs-lookup"><span data-stu-id="be3fe-109">Install Git, Node.js, Gulp, Python.</span></span>
- <span data-ttu-id="be3fe-110">Instalación de la interfaz de la línea de comandos de Azure (CLI de Azure)</span><span class="sxs-lookup"><span data-stu-id="be3fe-110">Install the Azure command-line interface (Azure CLI).</span></span> 

<span data-ttu-id="be3fe-111">Si tiene problemas, busque soluciones en la [página de solución de problemas](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="be3fe-111">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>
## <a name="what-you-will-learn"></a><span data-ttu-id="be3fe-112">Lo qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="be3fe-112">What you will learn</span></span>

<span data-ttu-id="be3fe-113">En esta lección, aprenderá lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="be3fe-113">In this lesson, you will learn:</span></span>

- <span data-ttu-id="be3fe-114">Cómo instalar Git y Node.js</span><span class="sxs-lookup"><span data-stu-id="be3fe-114">How to install Git and Node.js.</span></span>
  - <span data-ttu-id="be3fe-115">Git es un sistema de control de versiones distribuido de código abierto.</span><span class="sxs-lookup"><span data-stu-id="be3fe-115">Git is an open source distributed version control system.</span></span> <span data-ttu-id="be3fe-116">La aplicación de ejemplo de esta lección se almacena en Git.</span><span class="sxs-lookup"><span data-stu-id="be3fe-116">The sample application for this lesson is stored on Git.</span></span>
  - <span data-ttu-id="be3fe-117">Node.js es un entorno de tiempo de ejecución de JavaScript con un amplio ecosistema de paquetes.</span><span class="sxs-lookup"><span data-stu-id="be3fe-117">Node.js is a JavaScript runtime with a rich package ecosystem.</span></span>
- <span data-ttu-id="be3fe-118">Uso de NPM para instalar las herramientas de desarrollo de Node.js.</span><span class="sxs-lookup"><span data-stu-id="be3fe-118">How to use NPM to install Node.js development tools.</span></span>
  - <span data-ttu-id="be3fe-119">La versión mínima necesaria de Node.js es 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="be3fe-119">The minimum required version of Node.js is 4.5 LTS.</span></span>
  - <span data-ttu-id="be3fe-120">NPM es uno de los administradores de paquetes para Node.js.</span><span class="sxs-lookup"><span data-stu-id="be3fe-120">NPM is one of the package managers for Node.js.</span></span>
- <span data-ttu-id="be3fe-121">Instalación de Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="be3fe-121">How to install Visual Studio Code.</span></span>
  - <span data-ttu-id="be3fe-122">Visual Studio Code es un editor de código fuente multiplataforma ligero pero eficaz para Windows, Linux y macOS.</span><span class="sxs-lookup"><span data-stu-id="be3fe-122">Visual Studio Code is a cross platform, lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="be3fe-123">Ofrece un elevado nivel de compatibilidad para la depuración, control de Git insertado, resaltado de sintaxis, función inteligente de autocompletar código, fragmentos de código y refactorización de código.</span><span class="sxs-lookup"><span data-stu-id="be3fe-123">It has great support for debugging, embedded Git control, syntax highlighting, intelligent code completion, snippets, and code refactoring as well.</span></span>
- <span data-ttu-id="be3fe-124">Instalación de la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="be3fe-124">How to install the Azure CLI</span></span>
  - <span data-ttu-id="be3fe-125">La CLI de Azure proporciona una experiencia de línea de comandos multiplataforma en Azure.</span><span class="sxs-lookup"><span data-stu-id="be3fe-125">The Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="be3fe-126">De este modo, puede trabajar directamente desde la línea de comandos para aprovisionar y administrar los recursos.</span><span class="sxs-lookup"><span data-stu-id="be3fe-126">You work directly from a command line to provision and manage resources.</span></span>
- <span data-ttu-id="be3fe-127">Uso de la CLI de Azure para crear una instancia de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="be3fe-127">How to use the Azure CLI to create an IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="be3fe-128">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="be3fe-128">What you need</span></span>

- <span data-ttu-id="be3fe-129">Una conexión a Internet para descargar las herramientas y el software.</span><span class="sxs-lookup"><span data-stu-id="be3fe-129">An Internet connection to download the tools and software.</span></span>
- <span data-ttu-id="be3fe-130">Un equipo que ejecute Ubuntu 16.04 o posterior</span><span class="sxs-lookup"><span data-stu-id="be3fe-130">A computer that is running Ubuntu 16.04 or later.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="be3fe-131">Instalación de Git y Node.js</span><span class="sxs-lookup"><span data-stu-id="be3fe-131">Install Git and Node.js</span></span>

<span data-ttu-id="be3fe-132">Para instalar Git y Node.js, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="be3fe-132">To install Git and Node.js, follow these steps:</span></span>

1. <span data-ttu-id="be3fe-133">Presione `Ctrl + Alt + T` para abrir una ventana de terminal.</span><span class="sxs-lookup"><span data-stu-id="be3fe-133">Press `Ctrl + Alt + T` to open a terminal.</span></span>
2. <span data-ttu-id="be3fe-134">Ejecute los comandos siguientes:</span><span class="sxs-lookup"><span data-stu-id="be3fe-134">Run the following commands:</span></span>

   ```bash
   sudo apt-get update
   curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
   sudo apt-get install -y nodejs
   sudo apt-get install git
   ```

## <a name="install-nodejs-development-tools"></a><span data-ttu-id="be3fe-135">Instalación de herramientas de desarrollo de Node.js</span><span class="sxs-lookup"><span data-stu-id="be3fe-135">Install Node.js development tools</span></span>

<span data-ttu-id="be3fe-136">Use [gulp.js](http://gulpjs.com/) para automatizar la implementación y ejecución de scripts.</span><span class="sxs-lookup"><span data-stu-id="be3fe-136">You use [gulp.js](http://gulpjs.com/) to automate deployment and execution of scripts.</span></span>

<span data-ttu-id="be3fe-137">Para instalar Gulp, ejecute el comando siguiente en una ventana del terminal:</span><span class="sxs-lookup"><span data-stu-id="be3fe-137">To install gulp, run the following command in the terminal:</span></span>

```bash
sudo npm install -g gulp
```

<span data-ttu-id="be3fe-138">Si tiene problemas con la instalación, consulte la [guía de solución de problemas](iot-hub-gateway-kit-c-sim-troubleshooting.md) para solucionar problemas comunes.</span><span class="sxs-lookup"><span data-stu-id="be3fe-138">If you experience issues with the installation, see the [troubleshooting guide](iot-hub-gateway-kit-c-sim-troubleshooting.md) for solutions to common problems.</span></span>

> [!Note]
> <span data-ttu-id="be3fe-139">Se precisan Node, NPM y Gulp para ejecutar scripts de automatización desarrollados en Node.js.</span><span class="sxs-lookup"><span data-stu-id="be3fe-139">Node, NPM and Gulp are required to run automation scripts developed in Node.js.</span></span>

## <a name="install-the-azure-cli"></a><span data-ttu-id="be3fe-140">Instalación de la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="be3fe-140">Install the Azure CLI</span></span>

<span data-ttu-id="be3fe-141">Para instalar la CLI de Azure, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="be3fe-141">To install the Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="be3fe-142">Ejecute los siguientes comandos en una ventana de terminal:</span><span class="sxs-lookup"><span data-stu-id="be3fe-142">Run the following commands in the terminal:</span></span>

   ```bash
   sudo apt-get update
   sudo apt-get install -y libssl-dev libffi-dev
   sudo apt-get install -y python-dev
   sudo apt-get install -y build-essential
   sudo apt-get install -y python-pip
   sudo pip install --upgrade azure-cli
   sudo pip install --upgrade azure-cli-iot
   ```

   <span data-ttu-id="be3fe-143">La instalación puede tardar 5 minutos.</span><span class="sxs-lookup"><span data-stu-id="be3fe-143">The installation might take 5 minutes.</span></span>

2. <span data-ttu-id="be3fe-144">Compruebe la instalación ejecutando el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="be3fe-144">Verify the installation by running the following command:</span></span>

   ```bash
   az iot -h
   ```
<span data-ttu-id="be3fe-145">Si la instalación se realiza correctamente, verá el siguiente resultado.</span><span class="sxs-lookup"><span data-stu-id="be3fe-145">You should see the following output if the installation is successful.</span></span>
<span data-ttu-id="be3fe-146">![Verificación de la instalación de la CLI de Azure](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_ubuntu.png)</span><span class="sxs-lookup"><span data-stu-id="be3fe-146">![Verify Azure CLI installation](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_ubuntu.png)</span></span>

### <a name="install-visual-studio-code"></a><span data-ttu-id="be3fe-147">Instalación de Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="be3fe-147">Install Visual Studio Code</span></span>

<span data-ttu-id="be3fe-148">Use Visual Studio Code, como se explica más adelante en este tutorial, para editar los archivos de configuración.</span><span class="sxs-lookup"><span data-stu-id="be3fe-148">You use Visual Studio Code later in the tutorial to edit configuration files.</span></span>

<span data-ttu-id="be3fe-149">[Descargue](https://code.visualstudio.com/docs/setup/linux) e instale Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="be3fe-149">[Download](https://code.visualstudio.com/docs/setup/linux) and install Visual Studio Code.</span></span>

## <a name="summary"></a><span data-ttu-id="be3fe-150">Resumen</span><span class="sxs-lookup"><span data-stu-id="be3fe-150">Summary</span></span>

<span data-ttu-id="be3fe-151">Ha instalado todas las herramientas y el software necesarios en el equipo host.</span><span class="sxs-lookup"><span data-stu-id="be3fe-151">You've installed all the required tools and software on your host computer.</span></span> <span data-ttu-id="be3fe-152">La siguiente tarea consiste en utilizar la CLI de Azure para crear una instancia de IoT Hub y registrar el dispositivo en ella.</span><span class="sxs-lookup"><span data-stu-id="be3fe-152">Your next task is to use the Azure CLI to create an IoT hub and register your device in your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="be3fe-153">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="be3fe-153">Next steps</span></span>
[<span data-ttu-id="be3fe-154">Creación de una instancia de IoT Hub y registro del dispositivo</span><span class="sxs-lookup"><span data-stu-id="be3fe-154">Create an IoT hub and register your device</span></span>](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)
