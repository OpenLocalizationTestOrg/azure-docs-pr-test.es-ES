---
title: "Connect Intel Edison (C) tooAzure IoT - lección 2: herramientas de Azure (Ubuntu) | Documentos de Microsoft"
description: "Instale Python y la interfaz de la línea de comandos de Azure (CLI de Azure) en Ubuntu."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: CLI de Azure, servicio en la nube de IoT, Arduino en la nube
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: 2463cb8e-5758-4d72-af98-62520d41f2f7
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: a7691c13d43aa6dfff24adf2b470728d5266713e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-azure-tools-ubuntu-1604"></a><span data-ttu-id="96458-104">Obtención de las herramientas de Azure (Ubuntu 16.04)</span><span class="sxs-lookup"><span data-stu-id="96458-104">Get Azure tools (Ubuntu 16.04)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="96458-105">[Windows 7 y versiones posteriores][windows]</span><span class="sxs-lookup"><span data-stu-id="96458-105">[Windows 7 and later][windows]</span></span>
> * <span data-ttu-id="96458-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="96458-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="96458-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="96458-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="96458-108">Lo que hará</span><span class="sxs-lookup"><span data-stu-id="96458-108">What you will do</span></span>
<span data-ttu-id="96458-109">Instalar hello Azure interfaz de línea de comandos (CLI de Azure).</span><span class="sxs-lookup"><span data-stu-id="96458-109">Install hello Azure command-line interface (Azure CLI).</span></span> <span data-ttu-id="96458-110">Si tiene problemas, buscar soluciones en hello [solución de problemas de página][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="96458-110">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="96458-111">Lo qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="96458-111">What you will learn</span></span>
<span data-ttu-id="96458-112">En este artículo, aprenderá lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="96458-112">In this article, you will learn:</span></span>
* <span data-ttu-id="96458-113">¿Cómo tooinstall Hola CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="96458-113">How tooinstall hello Azure CLI.</span></span>
* <span data-ttu-id="96458-114">¿Cómo tooadd un subgrupo de IoT de hello CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="96458-114">How tooadd an IoT subgroup of hello Azure CLI.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="96458-115">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="96458-115">What you need</span></span>
* <span data-ttu-id="96458-116">Un equipo con Ubuntu con conexión a Internet.</span><span class="sxs-lookup"><span data-stu-id="96458-116">An Ubuntu computer with an Internet connection.</span></span>
* <span data-ttu-id="96458-117">Una suscripción de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="96458-117">An active Azure subscription.</span></span> <span data-ttu-id="96458-118">Si no tiene ninguna, puede crear una [cuenta de evaluación gratuita](http://azure.microsoft.com/pricing/free-trial/) en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="96458-118">If you don't have an account, you can create a [free trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>

## <a name="install-hello-azure-cli"></a><span data-ttu-id="96458-119">Instalar Hola CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="96458-119">Install hello Azure CLI</span></span>
<span data-ttu-id="96458-120">Hola CLI de Azure proporciona una experiencia multiplataforma de línea de comandos de Azure, permitiéndole toowork directamente desde la línea de comandos tooprovision y administrar los recursos.</span><span class="sxs-lookup"><span data-stu-id="96458-120">hello Azure CLI provides a multiplatform command-line experience for Azure, enabling you toowork directly from your command line tooprovision and manage resources.</span></span>

<span data-ttu-id="96458-121">tooinstall Hola CLI más reciente de Azure, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="96458-121">tooinstall hello latest Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="96458-122">Ejecute hello siga los comandos en una ventana de terminal.</span><span class="sxs-lookup"><span data-stu-id="96458-122">Run hello following commands in a terminal window.</span></span> <span data-ttu-id="96458-123">Es posible que tarde cinco minutos tooinstall Hola CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="96458-123">It might take five minutes tooinstall hello Azure CLI.</span></span>

   ```bash
   sudo apt-get update
   sudo apt-get install -y libssl-dev libffi-dev
   sudo apt-get install -y python-dev
   sudo apt-get install -y build-essential
   sudo apt-get install -y python-pip
   sudo pip install --upgrade azure-cli
   sudo pip install --upgrade azure-cli-iot
   ```
2. <span data-ttu-id="96458-124">Comprobar la instalación de hello ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="96458-124">Verify hello installation by running hello following command:</span></span>

   ```bash
   az iot -h
   ```

<span data-ttu-id="96458-125">Debería ver la siguiente Hola de salida si la instalación de hello es correcta.</span><span class="sxs-lookup"><span data-stu-id="96458-125">You should see hello following output if hello installation is successful.</span></span>

![Resultado que indica una instalación correcta](media/iot-hub-intel-edison-lessons/lesson2/az_iot_help_ubuntu.png)

## <a name="summary"></a><span data-ttu-id="96458-127">Resumen</span><span class="sxs-lookup"><span data-stu-id="96458-127">Summary</span></span>
<span data-ttu-id="96458-128">Ha instalado Hola CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="96458-128">You've installed hello Azure CLI.</span></span> <span data-ttu-id="96458-129">La siguiente tarea es toocreate su centro de IoT de Azure y la identidad del dispositivo a través Hola CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="96458-129">Your next task is toocreate your Azure IoT hub and device identity using hello Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="96458-130">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="96458-130">Next steps</span></span>
<span data-ttu-id="96458-131">[Creación de una instancia de IoT Hub y registro de Intel Edison][create-your-iot-hub-and-register-intel-edison]</span><span class="sxs-lookup"><span data-stu-id="96458-131">[Create your IoT hub and register Intel Edison][create-your-iot-hub-and-register-intel-edison]</span></span>


<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[create-your-iot-hub-and-register-intel-edison]: iot-hub-intel-edison-kit-c-lesson2-prepare-azure-iot-hub.md
[windows]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-mac.md
