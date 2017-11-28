---
title: "Conexión de Intel Edison (C) a Azure IoT: Lección 2: Herramientas de Azure (macOS) | Microsoft Docs"
description: "Instale Python la interfaz de la línea de comandos de Azure (CLI de Azure) en Mac OS."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: CLI de Azure, servicio en la nube de IoT, Arduino en la nube
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: d561680f-69cc-427a-820d-24f710ba05a8
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 97beb04781f3f9809cdafc945d9499e71cbbd9b1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="get-azure-tools-macos-1010"></a><span data-ttu-id="99d5c-104">Obtención de las herramientas de Azure (macOS 10.10)</span><span class="sxs-lookup"><span data-stu-id="99d5c-104">Get Azure tools (macOS 10.10)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="99d5c-105">[Windows 7 y versiones posteriores][windows]</span><span class="sxs-lookup"><span data-stu-id="99d5c-105">[Windows 7 and later][windows]</span></span>
> * <span data-ttu-id="99d5c-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="99d5c-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="99d5c-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="99d5c-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="99d5c-108">Lo que hará</span><span class="sxs-lookup"><span data-stu-id="99d5c-108">What you will do</span></span>
<span data-ttu-id="99d5c-109">Instalación de la interfaz de la línea de comandos de Azure (CLI de Azure)</span><span class="sxs-lookup"><span data-stu-id="99d5c-109">Install the Azure command-line interface (Azure CLI).</span></span> <span data-ttu-id="99d5c-110">Si tiene problemas, busque soluciones en [esta página][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="99d5c-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="99d5c-111">Lo qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="99d5c-111">What you will learn</span></span>
<span data-ttu-id="99d5c-112">En este artículo, aprenderá lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="99d5c-112">In this article, you will learn:</span></span>
* <span data-ttu-id="99d5c-113">Cómo instalar la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="99d5c-113">How to install Azure CLI.</span></span>
* <span data-ttu-id="99d5c-114">Cómo agregar un subgrupo de IoT de la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="99d5c-114">How to add an IoT subgroup of the Azure CLI.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="99d5c-115">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="99d5c-115">What you need</span></span>
* <span data-ttu-id="99d5c-116">Un Mac con conexión a Internet.</span><span class="sxs-lookup"><span data-stu-id="99d5c-116">A Mac with an Internet connection.</span></span>
* <span data-ttu-id="99d5c-117">Una suscripción de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="99d5c-117">An active Azure subscription.</span></span> <span data-ttu-id="99d5c-118">Si no tiene ninguna cuenta de Azure, puede crear una [cuenta de evaluación gratuita de Azure](http://azure.microsoft.com/pricing/free-trial/) en solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="99d5c-118">If you don't have an Azure account, you can create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>

## <a name="install-python"></a><span data-ttu-id="99d5c-119">Instalación de Python</span><span class="sxs-lookup"><span data-stu-id="99d5c-119">Install Python</span></span>
<span data-ttu-id="99d5c-120">Aunque macOS incluye Python 2.7 de forma predetermina, se recomienda instalar Python mediante Homebrew.</span><span class="sxs-lookup"><span data-stu-id="99d5c-120">Although macOS comes with Python 2.7 out of the box, we recommend that you install Python through Homebrew.</span></span> <span data-ttu-id="99d5c-121">Consulte [Instalación de Python en Mac OS](http://docs.python-guide.org/en/latest/starting/install/osx/).</span><span class="sxs-lookup"><span data-stu-id="99d5c-121">See [Installing Python on macOS](http://docs.python-guide.org/en/latest/starting/install/osx/).</span></span>

<span data-ttu-id="99d5c-122">Instale Python y pip ejecutando el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="99d5c-122">Install Python and pip by running the following command:</span></span>

```bash
brew install python
```

## <a name="install-the-azure-cli"></a><span data-ttu-id="99d5c-123">Instalación de la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="99d5c-123">Install the Azure CLI</span></span>
<span data-ttu-id="99d5c-124">La CLI de Azure proporciona una experiencia de línea de comandos multiplataforma en Azure.</span><span class="sxs-lookup"><span data-stu-id="99d5c-124">The Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="99d5c-125">De este modo, puede trabajar directamente desde la línea de comandos para aprovisionar y administrar los recursos.</span><span class="sxs-lookup"><span data-stu-id="99d5c-125">You work directly from your command line to provision and manage resources.</span></span> 

<span data-ttu-id="99d5c-126">Para instalar la CLI de Azure más recientr, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="99d5c-126">To install the latest Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="99d5c-127">Ejecute los siguientes comandos en una ventana de terminal.</span><span class="sxs-lookup"><span data-stu-id="99d5c-127">Run the following commands in a terminal window.</span></span> <span data-ttu-id="99d5c-128">Este proceso puede tardar cinco minutos en instalar la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="99d5c-128">It might take five minutes to install the Azure CLI.</span></span>

   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
2. <span data-ttu-id="99d5c-129">Compruebe la instalación ejecutando el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="99d5c-129">Verify the installation by running the following command:</span></span>

   ```bash
   az iot -h
   ```

<span data-ttu-id="99d5c-130">Si la instalación se realiza correctamente, verá el siguiente resultado.</span><span class="sxs-lookup"><span data-stu-id="99d5c-130">You should see the following output if the installation is successful.</span></span>

![Resultado que indica una instalación correcta](media/iot-hub-intel-edison-lessons/lesson2/az_iot_help_osx.png)

## <a name="summary"></a><span data-ttu-id="99d5c-132">Resumen</span><span class="sxs-lookup"><span data-stu-id="99d5c-132">Summary</span></span>
<span data-ttu-id="99d5c-133">Ha instalado la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="99d5c-133">You've installed the Azure CLI.</span></span> <span data-ttu-id="99d5c-134">La siguiente tarea consiste en crear la identidad de Azure IoT Hub y de dispositivos mediante la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="99d5c-134">Your next task is to create your Azure IoT hub and device identity by using the Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="99d5c-135">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="99d5c-135">Next steps</span></span>
<span data-ttu-id="99d5c-136">[Creación de una instancia de IoT Hub y registro de Intel Edison][create-your-iot-hub-and-register-intel-edison]</span><span class="sxs-lookup"><span data-stu-id="99d5c-136">[Create your IoT hub and register Intel Edison][create-your-iot-hub-and-register-intel-edison]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[create-your-iot-hub-and-register-intel-edison]: iot-hub-intel-edison-kit-c-lesson2-prepare-azure-iot-hub.md
[windows]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-mac.md
