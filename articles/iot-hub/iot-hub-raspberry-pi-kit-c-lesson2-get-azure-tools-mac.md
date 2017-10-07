---
title: "Connect Raspberry PI (C) tooAzure IoT - lección 2: herramientas de Azure (macOS) | Documentos de Microsoft"
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
ms.openlocfilehash: a079250fd94fa9bc1c11b6c21de02a8d46f6f3bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-azure-tools-macos-1010"></a><span data-ttu-id="4bbb6-104">Obtención de las herramientas de Azure (macOS 10.10)</span><span class="sxs-lookup"><span data-stu-id="4bbb6-104">Get Azure tools (macOS 10.10)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4bbb6-105">Windows 7 y versiones posteriores</span><span class="sxs-lookup"><span data-stu-id="4bbb6-105">Windows 7 and later</span></span>](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-win32.md)
> * [<span data-ttu-id="4bbb6-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="4bbb6-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-ubuntu.md)
> * [<span data-ttu-id="4bbb6-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="4bbb6-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="4bbb6-108">Lo que hará</span><span class="sxs-lookup"><span data-stu-id="4bbb6-108">What you will do</span></span>
<span data-ttu-id="4bbb6-109">Instalar hello Azure interfaz de línea de comandos (CLI de Azure).</span><span class="sxs-lookup"><span data-stu-id="4bbb6-109">Install hello Azure command-line interface (Azure CLI).</span></span> <span data-ttu-id="4bbb6-110">Si tiene problemas, buscar soluciones en hello [página solución de problemas](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="4bbb6-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="4bbb6-111">Lo qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="4bbb6-111">What you will learn</span></span>
<span data-ttu-id="4bbb6-112">En este artículo, aprenderá lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="4bbb6-112">In this article, you will learn:</span></span>
* <span data-ttu-id="4bbb6-113">¿Cómo tooinstall CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="4bbb6-113">How tooinstall Azure CLI.</span></span>
* <span data-ttu-id="4bbb6-114">¿Cómo tooadd un subgrupo de IoT de hello CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="4bbb6-114">How tooadd an IoT subgroup of hello Azure CLI.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="4bbb6-115">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="4bbb6-115">What you need</span></span>
* <span data-ttu-id="4bbb6-116">Un Mac con conexión a Internet.</span><span class="sxs-lookup"><span data-stu-id="4bbb6-116">A Mac with an Internet connection.</span></span>
* <span data-ttu-id="4bbb6-117">Una suscripción de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="4bbb6-117">An active Azure subscription.</span></span> <span data-ttu-id="4bbb6-118">Si no tiene ninguna cuenta de Azure, puede crear una [cuenta de evaluación gratuita de Azure](http://azure.microsoft.com/pricing/free-trial/) en solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="4bbb6-118">If you don't have an Azure account, you can create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>

## <a name="install-python"></a><span data-ttu-id="4bbb6-119">Instalación de Python</span><span class="sxs-lookup"><span data-stu-id="4bbb6-119">Install Python</span></span>
<span data-ttu-id="4bbb6-120">Aunque macOS incluye Python 2.7 fuera del cuadro de hello, se recomienda instalar Python a través de Homebrew.</span><span class="sxs-lookup"><span data-stu-id="4bbb6-120">Although macOS comes with Python 2.7 out of hello box, we recommend that you install Python through Homebrew.</span></span> <span data-ttu-id="4bbb6-121">Consulte [Instalación de Python en Mac OS](http://docs.python-guide.org/en/latest/starting/install/osx/).</span><span class="sxs-lookup"><span data-stu-id="4bbb6-121">See [Installing Python on macOS](http://docs.python-guide.org/en/latest/starting/install/osx/).</span></span>

<span data-ttu-id="4bbb6-122">Instalar Python y pip ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="4bbb6-122">Install Python and pip by running hello following command:</span></span>

```bash
brew install python
```

## <a name="install-hello-azure-cli"></a><span data-ttu-id="4bbb6-123">Instalar Hola CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="4bbb6-123">Install hello Azure CLI</span></span>
<span data-ttu-id="4bbb6-124">Hola CLI de Azure proporciona una experiencia de línea de comandos multiplataforma de Azure.</span><span class="sxs-lookup"><span data-stu-id="4bbb6-124">hello Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="4bbb6-125">Puede trabaja directamente desde la línea de comandos tooprovision y administrar recursos.</span><span class="sxs-lookup"><span data-stu-id="4bbb6-125">You work directly from your command line tooprovision and manage resources.</span></span> 

<span data-ttu-id="4bbb6-126">tooinstall Hola CLI más reciente de Azure, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="4bbb6-126">tooinstall hello latest Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="4bbb6-127">Ejecute hello siga los comandos en una ventana de terminal.</span><span class="sxs-lookup"><span data-stu-id="4bbb6-127">Run hello following commands in a terminal window.</span></span> <span data-ttu-id="4bbb6-128">Es posible que tarde cinco minutos tooinstall Hola CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="4bbb6-128">It might take five minutes tooinstall hello Azure CLI.</span></span>

   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
2. <span data-ttu-id="4bbb6-129">Comprobar la instalación de hello ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="4bbb6-129">Verify hello installation by running hello following command:</span></span>

   ```bash
   az iot -h
   ```

<span data-ttu-id="4bbb6-130">Debería ver la siguiente Hola de salida si la instalación de hello es correcta.</span><span class="sxs-lookup"><span data-stu-id="4bbb6-130">You should see hello following output if hello installation is successful.</span></span>

![Resultado que indica una instalación correcta](media/iot-hub-raspberry-pi-lessons/lesson2/az_iot_help_osx.png)

## <a name="summary"></a><span data-ttu-id="4bbb6-132">Resumen</span><span class="sxs-lookup"><span data-stu-id="4bbb6-132">Summary</span></span>
<span data-ttu-id="4bbb6-133">Ha instalado Hola CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="4bbb6-133">You've installed hello Azure CLI.</span></span> <span data-ttu-id="4bbb6-134">La siguiente tarea es toocreate su identidad de concentrador y dispositivos de IoT de Azure mediante el uso de Hola CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="4bbb6-134">Your next task is toocreate your Azure IoT hub and device identity by using hello Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4bbb6-135">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4bbb6-135">Next steps</span></span>
[<span data-ttu-id="4bbb6-136">Creación de un centro de IoT y registro de Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="4bbb6-136">Create your IoT hub and register Raspberry Pi 3</span></span>](iot-hub-raspberry-pi-kit-c-lesson2-prepare-azure-iot-hub.md)

