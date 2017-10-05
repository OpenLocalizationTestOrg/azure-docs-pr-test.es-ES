---
title: "Conexión de Raspberry Pi (Node) a Azure IoT: Lección 2: Obtención de las herramientas (Windows) | Microsoft Docs"
description: "Instale Python y la interfaz de la línea de comandos de Azure (CLI de Azure) en Windows 7 y versiones posteriores."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: servicio en la nube iot, cli de azure
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: acfa13e3-6d2c-4e68-9a77-1cbc2cf3f9c1
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: c7b927997b738f7a80b71c06d4dff2278dc7c64e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="get-azure-tools-windows-7-and-later"></a><span data-ttu-id="8f470-104">Obtención de las herramientas de Azure (Windows 7 o posterior)</span><span class="sxs-lookup"><span data-stu-id="8f470-104">Get Azure tools (Windows 7 and later)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8f470-105">Windows 7 y versiones posteriores</span><span class="sxs-lookup"><span data-stu-id="8f470-105">Windows 7 and later</span></span>](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-win32.md)
> * [<span data-ttu-id="8f470-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="8f470-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-ubuntu.md)
> * [<span data-ttu-id="8f470-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="8f470-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="8f470-108">Lo que hará</span><span class="sxs-lookup"><span data-stu-id="8f470-108">What you will do</span></span>
<span data-ttu-id="8f470-109">Instale Python y la interfaz de la línea de comandos de Azure (CLI de Azure).</span><span class="sxs-lookup"><span data-stu-id="8f470-109">Install Python and the Azure command-line interface (Azure CLI).</span></span> <span data-ttu-id="8f470-110">Si tiene problemas, busque soluciones en la [página de solución de problemas](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="8f470-110">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="8f470-111">Lo qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="8f470-111">What you will learn</span></span>
<span data-ttu-id="8f470-112">En este artículo, aprenderá lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="8f470-112">In this article, you will learn:</span></span>
* <span data-ttu-id="8f470-113">Cómo instalar Python.</span><span class="sxs-lookup"><span data-stu-id="8f470-113">How to install Python.</span></span>
* <span data-ttu-id="8f470-114">Cómo instalar la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="8f470-114">How to install the Azure CLI.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="8f470-115">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="8f470-115">What you need</span></span>
* <span data-ttu-id="8f470-116">Un equipo Windows con conexión a Internet.</span><span class="sxs-lookup"><span data-stu-id="8f470-116">A Windows computer with an Internet connection.</span></span>
* <span data-ttu-id="8f470-117">Una suscripción de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="8f470-117">An active Azure subscription.</span></span> <span data-ttu-id="8f470-118">Si no tiene ninguna cuenta de Azure, cree una [cuenta de evaluación gratuita de Azure](http://azure.microsoft.com/pricing/free-trial/) en solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="8f470-118">If you don't have an Azure account, create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>

## <a name="install-python"></a><span data-ttu-id="8f470-119">Instalación de Python</span><span class="sxs-lookup"><span data-stu-id="8f470-119">Install Python</span></span>
<span data-ttu-id="8f470-120">[Instale Python](https://www.python.org/downloads/) en el equipo Windows.</span><span class="sxs-lookup"><span data-stu-id="8f470-120">[Install Python](https://www.python.org/downloads/) on your Windows computer.</span></span> <span data-ttu-id="8f470-121">Puede instalar Python 2.7, 3.4 o 3.5.</span><span class="sxs-lookup"><span data-stu-id="8f470-121">You can install Python 2.7, 3.4 or 3.5.</span></span> <span data-ttu-id="8f470-122">Este tutorial se basa en Python 2.7.</span><span class="sxs-lookup"><span data-stu-id="8f470-122">This tutorial is based on Python 2.7.</span></span> <span data-ttu-id="8f470-123">Si ya ha instalado Python, vaya a la sección siguiente e instale la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="8f470-123">If you've already installed Python, go to the next section and install the Azure CLI.</span></span>

<span data-ttu-id="8f470-124">También debe agregar la ruta de acceso de las carpetas donde se instalan python.exe y pip.exe a la variable de entorno `PATH` del sistema.</span><span class="sxs-lookup"><span data-stu-id="8f470-124">You also need to add the path of the folders where python.exe and pip.exe are installed to the system `PATH` environment variable.</span></span> <span data-ttu-id="8f470-125">De forma predeterminada, se instala python.exe en `C:\Python27` y pip.exe en `C:\Python27\Scripts`.</span><span class="sxs-lookup"><span data-stu-id="8f470-125">By default, python.exe is installed in `C:\Python27` and pip.exe is installed in `C:\Python27\Scripts`.</span></span>

## <a name="install-the-azure-cli"></a><span data-ttu-id="8f470-126">Instalación de la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="8f470-126">Install the Azure CLI</span></span>
<span data-ttu-id="8f470-127">La CLI de Azure proporciona una experiencia de línea de comandos multiplataforma en Azure.</span><span class="sxs-lookup"><span data-stu-id="8f470-127">The Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="8f470-128">De este modo, puede trabajar directamente desde la línea de comandos para aprovisionar y administrar los recursos.</span><span class="sxs-lookup"><span data-stu-id="8f470-128">You work directly from your command-line to provision and manage resources.</span></span>

<span data-ttu-id="8f470-129">Para instalar la CLI de Azure, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="8f470-129">To install the Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="8f470-130">Abra una ventana de símbolo del sistema como administrador.</span><span class="sxs-lookup"><span data-stu-id="8f470-130">Open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="8f470-131">Ejecute los comandos siguientes:</span><span class="sxs-lookup"><span data-stu-id="8f470-131">Run the following commands:</span></span>

   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
3. <span data-ttu-id="8f470-132">Compruebe la instalación ejecutando el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="8f470-132">Verify the installation by running the following command:</span></span>

   ```bash
   az iot -h
   ```

<span data-ttu-id="8f470-133">Si la instalación se realiza correctamente, verá el siguiente resultado.</span><span class="sxs-lookup"><span data-stu-id="8f470-133">You see the following output if the installation is successful.</span></span>

![Resultado que indica una instalación correcta](media/iot-hub-raspberry-pi-lessons/lesson2/az_iot_help_win.png)

## <a name="summary"></a><span data-ttu-id="8f470-135">Resumen</span><span class="sxs-lookup"><span data-stu-id="8f470-135">Summary</span></span>
<span data-ttu-id="8f470-136">Ha instalado la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="8f470-136">You've installed the Azure CLI.</span></span> <span data-ttu-id="8f470-137">La siguiente tarea consiste en crear la identidad de Azure IoT Hub y de dispositivos mediante la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="8f470-137">Your next task to create your Azure IoT hub and device identity by using the Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8f470-138">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8f470-138">Next steps</span></span>
[<span data-ttu-id="8f470-139">Creación de un centro de IoT y registro de Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="8f470-139">Create your IoT hub and register Raspberry Pi 3</span></span>](iot-hub-raspberry-pi-kit-node-lesson2-prepare-azure-iot-hub.md)
