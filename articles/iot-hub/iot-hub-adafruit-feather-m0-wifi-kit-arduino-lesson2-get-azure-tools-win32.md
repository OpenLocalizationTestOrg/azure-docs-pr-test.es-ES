---
title: "Conexión de Arduino a Azure IoT: Lección 2: Herramientas de Azure (Windows) | Microsoft Docs"
description: "Instale Python y la interfaz de la línea de comandos de Azure (CLI de Azure) en Windows 7 y versiones posteriores."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: CLI de Azure, servicio en la nube de IoT, Arduino en la nube
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 70dfff14-4be1-468d-9919-e40f4bead308
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 1f121d9f22f8a7c8582df4d2e62191cec364da46
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="get-azure-tools-windows-7-and-later"></a><span data-ttu-id="5e38d-104">Obtención de las herramientas de Azure (Windows 7 o posterior)</span><span class="sxs-lookup"><span data-stu-id="5e38d-104">Get Azure tools (Windows 7 and later)</span></span>

> [!div class="op_single_selector"]
> * <span data-ttu-id="5e38d-105">[Windows 7 o posterior][windows]</span><span class="sxs-lookup"><span data-stu-id="5e38d-105">[Windows 7 or later][windows]</span></span>
> * <span data-ttu-id="5e38d-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="5e38d-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="5e38d-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="5e38d-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="5e38d-108">Lo que hará</span><span class="sxs-lookup"><span data-stu-id="5e38d-108">What you will do</span></span>

<span data-ttu-id="5e38d-109">Instale Python y la interfaz de la línea de comandos de Azure (CLI de Azure).</span><span class="sxs-lookup"><span data-stu-id="5e38d-109">Install Python and the Azure command-line interface (Azure CLI).</span></span> <span data-ttu-id="5e38d-110">Si tiene problemas, busque soluciones en [esta página](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md) para la placa Adafruit Feather M0 WiFi Arduino.</span><span class="sxs-lookup"><span data-stu-id="5e38d-110">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md) for your Adafruit Feather M0 WiFi Arduino board.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="5e38d-111">Lo qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="5e38d-111">What you will learn</span></span>
<span data-ttu-id="5e38d-112">En este artículo, aprenderá lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="5e38d-112">In this article, you will learn:</span></span>
* <span data-ttu-id="5e38d-113">Cómo instalar Python.</span><span class="sxs-lookup"><span data-stu-id="5e38d-113">How to install Python.</span></span>
* <span data-ttu-id="5e38d-114">Cómo instalar la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="5e38d-114">How to install the Azure CLI.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="5e38d-115">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="5e38d-115">What you need</span></span>
* <span data-ttu-id="5e38d-116">Un equipo Windows con conexión a Internet.</span><span class="sxs-lookup"><span data-stu-id="5e38d-116">A Windows computer with an Internet connection.</span></span>
* <span data-ttu-id="5e38d-117">Una suscripción de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="5e38d-117">An active Azure subscription.</span></span> <span data-ttu-id="5e38d-118">Si no tiene ninguna cuenta de Azure, cree una [cuenta de evaluación gratuita de Azure](http://azure.microsoft.com/pricing/free-trial/) en solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="5e38d-118">If you don't have an Azure account, create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>

## <a name="install-python"></a><span data-ttu-id="5e38d-119">Instalación de Python</span><span class="sxs-lookup"><span data-stu-id="5e38d-119">Install Python</span></span>
<span data-ttu-id="5e38d-120">[Instale Python](https://www.python.org/downloads/) en el equipo Windows.</span><span class="sxs-lookup"><span data-stu-id="5e38d-120">[Install Python](https://www.python.org/downloads/) on your Windows computer.</span></span> <span data-ttu-id="5e38d-121">Puede instalar Python 2.7, 3.4 o 3.5.</span><span class="sxs-lookup"><span data-stu-id="5e38d-121">You can install Python 2.7, 3.4 or 3.5.</span></span> <span data-ttu-id="5e38d-122">Este tutorial se basa en Python 2.7.</span><span class="sxs-lookup"><span data-stu-id="5e38d-122">This tutorial is based on Python 2.7.</span></span> <span data-ttu-id="5e38d-123">Si ya ha instalado Python, vaya a la sección siguiente e instale la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="5e38d-123">If you've already installed Python, go to the next section and install the Azure CLI.</span></span>

<span data-ttu-id="5e38d-124">También debe agregar la ruta de acceso de las carpetas donde se instalan python.exe y pip.exe a la variable de entorno `PATH` del sistema.</span><span class="sxs-lookup"><span data-stu-id="5e38d-124">You also need to add the path of the folders where python.exe and pip.exe are installed to the system `PATH` environment variable.</span></span> <span data-ttu-id="5e38d-125">De forma predeterminada, se instala python.exe en `C:\Python27` y pip.exe en `C:\Python27\Scripts`.</span><span class="sxs-lookup"><span data-stu-id="5e38d-125">By default, python.exe is installed in `C:\Python27` and pip.exe is installed in `C:\Python27\Scripts`.</span></span>

## <a name="install-the-azure-cli"></a><span data-ttu-id="5e38d-126">Instalación de la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="5e38d-126">Install the Azure CLI</span></span>
<span data-ttu-id="5e38d-127">La CLI de Azure proporciona una experiencia de línea de comandos multiplataforma en Azure.</span><span class="sxs-lookup"><span data-stu-id="5e38d-127">The Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="5e38d-128">De este modo, puede trabajar directamente desde la línea de comandos para aprovisionar y administrar los recursos.</span><span class="sxs-lookup"><span data-stu-id="5e38d-128">You work directly from your command line to provision and manage resources.</span></span>

<span data-ttu-id="5e38d-129">Para instalar la CLI de Azure, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="5e38d-129">To install the Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="5e38d-130">Abra una ventana de símbolo del sistema como administrador.</span><span class="sxs-lookup"><span data-stu-id="5e38d-130">Open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="5e38d-131">Ejecute los comandos siguientes:</span><span class="sxs-lookup"><span data-stu-id="5e38d-131">Run the following commands:</span></span>

   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
3. <span data-ttu-id="5e38d-132">Compruebe la instalación ejecutando el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="5e38d-132">Verify the installation by running the following command:</span></span>

   ```bash
   az iot -h
   ```

<span data-ttu-id="5e38d-133">Si la instalación se realiza correctamente, verá el siguiente resultado.</span><span class="sxs-lookup"><span data-stu-id="5e38d-133">You see the following output if the installation is successful.</span></span>

![Resultado que indica una instalación correcta][output]

## <a name="summary"></a><span data-ttu-id="5e38d-135">Resumen</span><span class="sxs-lookup"><span data-stu-id="5e38d-135">Summary</span></span>
<span data-ttu-id="5e38d-136">Ha instalado la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="5e38d-136">You've installed the Azure CLI.</span></span> <span data-ttu-id="5e38d-137">La siguiente tarea consiste en crear la identidad de Azure IoT Hub y de dispositivos mediante la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="5e38d-137">Your next task to create your Azure IoT hub and device identity by using the Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5e38d-138">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5e38d-138">Next steps</span></span>
<span data-ttu-id="5e38d-139">[Creación de la instancia de IoT Hub y registro de Raspberry Pi][create-your-iot-hub-and-register-your-arduino-board]</span><span class="sxs-lookup"><span data-stu-id="5e38d-139">[Create your IoT hub and register your Arduino board][create-your-iot-hub-and-register-your-arduino-board]</span></span>


<!-- Images and links -->

[windows]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-win32.md
[ubuntu]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-ubuntu.md
[macos]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-mac.md
[output]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson2/az_iot_help_win.png
[create-your-iot-hub-and-register-your-arduino-board]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-prepare-azure-iot-hub.md