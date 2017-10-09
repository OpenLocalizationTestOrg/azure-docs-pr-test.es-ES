---
title: "Connect Intel Edison (C) tooAzure IoT - lección 2: herramientas de Azure (macOS) | Documentos de Microsoft"
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
ms.openlocfilehash: 0dfc9ff90e879d5fd03040016ac71a9fe4f4a744
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-azure-tools-macos-1010"></a><span data-ttu-id="5c9ad-104">Obtención de las herramientas de Azure (macOS 10.10)</span><span class="sxs-lookup"><span data-stu-id="5c9ad-104">Get Azure tools (macOS 10.10)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="5c9ad-105">[Windows 7 y versiones posteriores][windows]</span><span class="sxs-lookup"><span data-stu-id="5c9ad-105">[Windows 7 and later][windows]</span></span>
> * <span data-ttu-id="5c9ad-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="5c9ad-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="5c9ad-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="5c9ad-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="5c9ad-108">Lo que hará</span><span class="sxs-lookup"><span data-stu-id="5c9ad-108">What you will do</span></span>
<span data-ttu-id="5c9ad-109">Instalar hello Azure interfaz de línea de comandos (CLI de Azure).</span><span class="sxs-lookup"><span data-stu-id="5c9ad-109">Install hello Azure command-line interface (Azure CLI).</span></span> <span data-ttu-id="5c9ad-110">Si tiene problemas, buscar soluciones en hello [solución de problemas de página][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="5c9ad-110">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="5c9ad-111">Lo qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="5c9ad-111">What you will learn</span></span>
<span data-ttu-id="5c9ad-112">En este artículo, aprenderá lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="5c9ad-112">In this article, you will learn:</span></span>
* <span data-ttu-id="5c9ad-113">¿Cómo tooinstall CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="5c9ad-113">How tooinstall Azure CLI.</span></span>
* <span data-ttu-id="5c9ad-114">¿Cómo tooadd un subgrupo de IoT de hello CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="5c9ad-114">How tooadd an IoT subgroup of hello Azure CLI.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="5c9ad-115">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="5c9ad-115">What you need</span></span>
* <span data-ttu-id="5c9ad-116">Un Mac con conexión a Internet.</span><span class="sxs-lookup"><span data-stu-id="5c9ad-116">A Mac with an Internet connection.</span></span>
* <span data-ttu-id="5c9ad-117">Una suscripción de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="5c9ad-117">An active Azure subscription.</span></span> <span data-ttu-id="5c9ad-118">Si no tiene ninguna cuenta de Azure, puede crear una [cuenta de evaluación gratuita de Azure](http://azure.microsoft.com/pricing/free-trial/) en solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="5c9ad-118">If you don't have an Azure account, you can create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>

## <a name="install-python"></a><span data-ttu-id="5c9ad-119">Instalación de Python</span><span class="sxs-lookup"><span data-stu-id="5c9ad-119">Install Python</span></span>
<span data-ttu-id="5c9ad-120">Aunque macOS incluye Python 2.7 fuera del cuadro de hello, se recomienda instalar Python a través de Homebrew.</span><span class="sxs-lookup"><span data-stu-id="5c9ad-120">Although macOS comes with Python 2.7 out of hello box, we recommend that you install Python through Homebrew.</span></span> <span data-ttu-id="5c9ad-121">Consulte [Instalación de Python en Mac OS](http://docs.python-guide.org/en/latest/starting/install/osx/).</span><span class="sxs-lookup"><span data-stu-id="5c9ad-121">See [Installing Python on macOS](http://docs.python-guide.org/en/latest/starting/install/osx/).</span></span>

<span data-ttu-id="5c9ad-122">Instalar Python y pip ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="5c9ad-122">Install Python and pip by running hello following command:</span></span>

```bash
brew install python
```

## <a name="install-hello-azure-cli"></a><span data-ttu-id="5c9ad-123">Instalar Hola CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="5c9ad-123">Install hello Azure CLI</span></span>
<span data-ttu-id="5c9ad-124">Hola CLI de Azure proporciona una experiencia de línea de comandos multiplataforma de Azure.</span><span class="sxs-lookup"><span data-stu-id="5c9ad-124">hello Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="5c9ad-125">Puede trabaja directamente desde la línea de comandos tooprovision y administrar recursos.</span><span class="sxs-lookup"><span data-stu-id="5c9ad-125">You work directly from your command line tooprovision and manage resources.</span></span> 

<span data-ttu-id="5c9ad-126">tooinstall Hola CLI más reciente de Azure, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="5c9ad-126">tooinstall hello latest Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="5c9ad-127">Ejecute hello siga los comandos en una ventana de terminal.</span><span class="sxs-lookup"><span data-stu-id="5c9ad-127">Run hello following commands in a terminal window.</span></span> <span data-ttu-id="5c9ad-128">Es posible que tarde cinco minutos tooinstall Hola CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="5c9ad-128">It might take five minutes tooinstall hello Azure CLI.</span></span>

   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
2. <span data-ttu-id="5c9ad-129">Comprobar la instalación de hello ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="5c9ad-129">Verify hello installation by running hello following command:</span></span>

   ```bash
   az iot -h
   ```

<span data-ttu-id="5c9ad-130">Debería ver la siguiente Hola de salida si la instalación de hello es correcta.</span><span class="sxs-lookup"><span data-stu-id="5c9ad-130">You should see hello following output if hello installation is successful.</span></span>

![Resultado que indica una instalación correcta](media/iot-hub-intel-edison-lessons/lesson2/az_iot_help_osx.png)

## <a name="summary"></a><span data-ttu-id="5c9ad-132">Resumen</span><span class="sxs-lookup"><span data-stu-id="5c9ad-132">Summary</span></span>
<span data-ttu-id="5c9ad-133">Ha instalado Hola CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="5c9ad-133">You've installed hello Azure CLI.</span></span> <span data-ttu-id="5c9ad-134">La siguiente tarea es toocreate su identidad de concentrador y dispositivos de IoT de Azure mediante el uso de Hola CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="5c9ad-134">Your next task is toocreate your Azure IoT hub and device identity by using hello Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5c9ad-135">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5c9ad-135">Next steps</span></span>
<span data-ttu-id="5c9ad-136">[Creación de una instancia de IoT Hub y registro de Intel Edison][create-your-iot-hub-and-register-intel-edison]</span><span class="sxs-lookup"><span data-stu-id="5c9ad-136">[Create your IoT hub and register Intel Edison][create-your-iot-hub-and-register-intel-edison]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[create-your-iot-hub-and-register-intel-edison]: iot-hub-intel-edison-kit-c-lesson2-prepare-azure-iot-hub.md
[windows]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-mac.md
