---
title: "Conexión de Arduino a Azure IoT: Lección 2: Herramientas de Azure (Ubuntu) | Microsoft Docs"
description: "Instale Python y la interfaz de la línea de comandos de Azure (CLI de Azure) en Ubuntu."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: CLI de Azure, servicio en la nube de IoT, Arduino en la nube
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: bb5cb602-7292-4772-ac90-c0b52ebc8340
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: a2f83e59a37abc3f44e770b22ac089b88481a6a4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="get-azure-tools-ubuntu-1604"></a><span data-ttu-id="cef98-104">Obtención de las herramientas de Azure (Ubuntu 16.04)</span><span class="sxs-lookup"><span data-stu-id="cef98-104">Get Azure tools (Ubuntu 16.04)</span></span>

> [!div class="op_single_selector"]
> * <span data-ttu-id="cef98-105">[Windows 7 o posterior][windows]</span><span class="sxs-lookup"><span data-stu-id="cef98-105">[Windows 7 or later][windows]</span></span>
> * <span data-ttu-id="cef98-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="cef98-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="cef98-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="cef98-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="cef98-108">Lo que hará</span><span class="sxs-lookup"><span data-stu-id="cef98-108">What you will do</span></span>

<span data-ttu-id="cef98-109">Instalación de la interfaz de la línea de comandos de Azure (CLI de Azure)</span><span class="sxs-lookup"><span data-stu-id="cef98-109">Install the Azure command-line interface (Azure CLI).</span></span> <span data-ttu-id="cef98-110">Si tiene problemas, busque soluciones en [esta página](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md) para la placa Adafruit Feather M0 WiFi Arduino.</span><span class="sxs-lookup"><span data-stu-id="cef98-110">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md) for your Adafruit Feather M0 WiFi Arduino board.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="cef98-111">Lo qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="cef98-111">What you will learn</span></span>
<span data-ttu-id="cef98-112">En este artículo, aprenderá lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="cef98-112">In this article, you will learn:</span></span>
* <span data-ttu-id="cef98-113">Cómo instalar la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="cef98-113">How to install the Azure CLI.</span></span>
* <span data-ttu-id="cef98-114">Cómo agregar un subgrupo de IoT de la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="cef98-114">How to add an IoT subgroup of the Azure CLI.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="cef98-115">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="cef98-115">What you need</span></span>
* <span data-ttu-id="cef98-116">Un equipo con Ubuntu con conexión a Internet.</span><span class="sxs-lookup"><span data-stu-id="cef98-116">An Ubuntu computer with an Internet connection.</span></span>
* <span data-ttu-id="cef98-117">Una suscripción de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="cef98-117">An active Azure subscription.</span></span> <span data-ttu-id="cef98-118">Si no tiene ninguna, puede crear una [cuenta de evaluación gratuita](http://azure.microsoft.com/pricing/free-trial/) en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="cef98-118">If you don't have an account, you can create a [free trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>

## <a name="install-the-azure-cli"></a><span data-ttu-id="cef98-119">Instalación de la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="cef98-119">Install the Azure CLI</span></span>
<span data-ttu-id="cef98-120">La CLI de Azure proporciona una experiencia de línea de comandos multiplataforma en Azure, lo que le permite trabajar directamente desde la línea de comandos para aprovisionar y administrar los recursos.</span><span class="sxs-lookup"><span data-stu-id="cef98-120">The Azure CLI provides a multiplatform command-line experience for Azure, enabling you to work directly from your command line to provision and manage resources.</span></span>

<span data-ttu-id="cef98-121">Para instalar la CLI de Azure más recientr, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="cef98-121">To install the latest Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="cef98-122">Ejecute los siguientes comandos en una ventana de terminal.</span><span class="sxs-lookup"><span data-stu-id="cef98-122">Run the following commands in a terminal window.</span></span> <span data-ttu-id="cef98-123">Este proceso puede tardar cinco minutos en instalar la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="cef98-123">It might take five minutes to install the Azure CLI.</span></span>

   ```bash
   sudo apt-get update
   sudo apt-get install -y libssl-dev libffi-dev
   sudo apt-get install -y python-dev
   sudo apt-get install -y build-essential
   sudo apt-get install -y python-pip
   sudo pip install --upgrade azure-cli
   sudo pip install --upgrade azure-cli-iot
   ```
2. <span data-ttu-id="cef98-124">Compruebe la instalación ejecutando el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="cef98-124">Verify the installation by running the following command:</span></span>

   ```bash
   az iot -h
   ```

<span data-ttu-id="cef98-125">Si la instalación se realiza correctamente, verá el siguiente resultado.</span><span class="sxs-lookup"><span data-stu-id="cef98-125">You should see the following output if the installation is successful.</span></span>

![Resultado que indica una instalación correcta][output]

## <a name="summary"></a><span data-ttu-id="cef98-127">Resumen</span><span class="sxs-lookup"><span data-stu-id="cef98-127">Summary</span></span>
<span data-ttu-id="cef98-128">Ha instalado la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="cef98-128">You've installed the Azure CLI.</span></span> <span data-ttu-id="cef98-129">La siguiente tarea consiste en crear la identidad de Azure IoT Hub y de dispositivos mediante la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="cef98-129">Your next task is to create your Azure IoT hub and device identity using the Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cef98-130">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="cef98-130">Next steps</span></span>
<span data-ttu-id="cef98-131">[Creación de la instancia de IoT Hub y registro de Raspberry Pi][create-your-iot-hub-and-register-your-arduino-board]</span><span class="sxs-lookup"><span data-stu-id="cef98-131">[Create your IoT hub and register your Arduino board][create-your-iot-hub-and-register-your-arduino-board]</span></span>
<!-- Images and links -->

[windows]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-win32.md
[ubuntu]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-ubuntu.md
[macos]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-mac.md
[output]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson2/az_iot_help_ubuntu.png
[create-your-iot-hub-and-register-your-arduino-board]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-prepare-azure-iot-hub.md