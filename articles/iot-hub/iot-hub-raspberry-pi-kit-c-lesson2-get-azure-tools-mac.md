---
title: "Conexión de Raspberry Pi (C) a Azure IoT: Lección 2: Herramientas de Azure (macOS) | Microsoft Docs"
description: "Instale Python la interfaz de la línea de comandos de Azure (CLI de Azure) en Mac OS."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: servicio en la nube iot, cli de azure
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: f2d7d584-7734-401c-976c-81788a7282a3
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 3810990f4a27270fa45709f4d9dbb36a8f4369a8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="get-azure-tools-macos-1010"></a><span data-ttu-id="b76a3-104">Obtención de las herramientas de Azure (macOS 10.10)</span><span class="sxs-lookup"><span data-stu-id="b76a3-104">Get Azure tools (macOS 10.10)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b76a3-105">Windows 7 y versiones posteriores</span><span class="sxs-lookup"><span data-stu-id="b76a3-105">Windows 7 and later</span></span>](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-win32.md)
> * [<span data-ttu-id="b76a3-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="b76a3-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-ubuntu.md)
> * [<span data-ttu-id="b76a3-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="b76a3-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="b76a3-108">Lo que hará</span><span class="sxs-lookup"><span data-stu-id="b76a3-108">What you will do</span></span>
<span data-ttu-id="b76a3-109">Instalación de la interfaz de la línea de comandos de Azure (CLI de Azure)</span><span class="sxs-lookup"><span data-stu-id="b76a3-109">Install the Azure command-line interface (Azure CLI).</span></span> <span data-ttu-id="b76a3-110">Si tiene problemas, busque soluciones en la [página de solución de problemas](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="b76a3-110">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="b76a3-111">Lo qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="b76a3-111">What you will learn</span></span>
<span data-ttu-id="b76a3-112">En este artículo, aprenderá lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="b76a3-112">In this article, you will learn:</span></span>
* <span data-ttu-id="b76a3-113">Cómo instalar la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="b76a3-113">How to install Azure CLI.</span></span>
* <span data-ttu-id="b76a3-114">Cómo agregar un subgrupo de IoT de la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="b76a3-114">How to add an IoT subgroup of the Azure CLI.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="b76a3-115">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="b76a3-115">What you need</span></span>
* <span data-ttu-id="b76a3-116">Un Mac con conexión a Internet.</span><span class="sxs-lookup"><span data-stu-id="b76a3-116">A Mac with an Internet connection.</span></span>
* <span data-ttu-id="b76a3-117">Una suscripción de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="b76a3-117">An active Azure subscription.</span></span> <span data-ttu-id="b76a3-118">Si no tiene ninguna cuenta de Azure, puede crear una [cuenta de evaluación gratuita de Azure](http://azure.microsoft.com/pricing/free-trial/) en solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="b76a3-118">If you don't have an Azure account, you can create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>

## <a name="install-python"></a><span data-ttu-id="b76a3-119">Instalación de Python</span><span class="sxs-lookup"><span data-stu-id="b76a3-119">Install Python</span></span>
<span data-ttu-id="b76a3-120">Aunque macOS incluye Python 2.7 de forma predetermina, se recomienda instalar Python mediante Homebrew.</span><span class="sxs-lookup"><span data-stu-id="b76a3-120">Although macOS comes with Python 2.7 out of the box, we recommend that you install Python through Homebrew.</span></span> <span data-ttu-id="b76a3-121">Consulte [Instalación de Python en Mac OS](http://docs.python-guide.org/en/latest/starting/install/osx/).</span><span class="sxs-lookup"><span data-stu-id="b76a3-121">See [Installing Python on macOS](http://docs.python-guide.org/en/latest/starting/install/osx/).</span></span>

<span data-ttu-id="b76a3-122">Instale Python y pip ejecutando el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="b76a3-122">Install Python and pip by running the following command:</span></span>

```bash
brew install python
```

## <a name="install-the-azure-cli"></a><span data-ttu-id="b76a3-123">Instalación de la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="b76a3-123">Install the Azure CLI</span></span>
<span data-ttu-id="b76a3-124">La CLI de Azure proporciona una experiencia de línea de comandos multiplataforma en Azure.</span><span class="sxs-lookup"><span data-stu-id="b76a3-124">The Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="b76a3-125">De este modo, puede trabajar directamente desde la línea de comandos para aprovisionar y administrar los recursos.</span><span class="sxs-lookup"><span data-stu-id="b76a3-125">You work directly from your command line to provision and manage resources.</span></span> 

<span data-ttu-id="b76a3-126">Para instalar la CLI de Azure más recientr, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="b76a3-126">To install the latest Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="b76a3-127">Ejecute los siguientes comandos en una ventana de terminal.</span><span class="sxs-lookup"><span data-stu-id="b76a3-127">Run the following commands in a terminal window.</span></span> <span data-ttu-id="b76a3-128">Este proceso puede tardar cinco minutos en instalar la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="b76a3-128">It might take five minutes to install the Azure CLI.</span></span>

   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
2. <span data-ttu-id="b76a3-129">Compruebe la instalación ejecutando el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="b76a3-129">Verify the installation by running the following command:</span></span>

   ```bash
   az iot -h
   ```

<span data-ttu-id="b76a3-130">Si la instalación se realiza correctamente, verá el siguiente resultado.</span><span class="sxs-lookup"><span data-stu-id="b76a3-130">You should see the following output if the installation is successful.</span></span>

![Resultado que indica una instalación correcta](media/iot-hub-raspberry-pi-lessons/lesson2/az_iot_help_osx.png)

## <a name="summary"></a><span data-ttu-id="b76a3-132">Resumen</span><span class="sxs-lookup"><span data-stu-id="b76a3-132">Summary</span></span>
<span data-ttu-id="b76a3-133">Ha instalado la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="b76a3-133">You've installed the Azure CLI.</span></span> <span data-ttu-id="b76a3-134">La siguiente tarea consiste en crear la identidad de Azure IoT Hub y de dispositivos mediante la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="b76a3-134">Your next task is to create your Azure IoT hub and device identity by using the Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b76a3-135">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b76a3-135">Next steps</span></span>
[<span data-ttu-id="b76a3-136">Creación de un centro de IoT y registro de Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="b76a3-136">Create your IoT hub and register Raspberry Pi 3</span></span>](iot-hub-raspberry-pi-kit-c-lesson2-prepare-azure-iot-hub.md)

