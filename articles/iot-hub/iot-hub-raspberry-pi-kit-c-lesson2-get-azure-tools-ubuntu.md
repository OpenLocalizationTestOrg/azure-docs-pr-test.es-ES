---
title: "Connect Raspberry PI (C) tooAzure IoT - lección 2: herramientas de Azure (Ubuntu) | Documentos de Microsoft"
description: "Instale Python y la interfaz de la línea de comandos de Azure (CLI de Azure) en Ubuntu."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: servicio en la nube iot, cli de azure
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: a03512f2-fabe-40c5-8505-b93eef8e5bec
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 1af4848f9fe0508e362c15b36eec8a35aea9ac5b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-azure-tools-ubuntu-1604"></a><span data-ttu-id="49466-104">Obtención de las herramientas de Azure (Ubuntu 16.04)</span><span class="sxs-lookup"><span data-stu-id="49466-104">Get Azure tools (Ubuntu 16.04)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="49466-105">Windows 7 y versiones posteriores</span><span class="sxs-lookup"><span data-stu-id="49466-105">Windows 7 and later</span></span>](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-win32.md)
> * [<span data-ttu-id="49466-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="49466-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-ubuntu.md)
> * [<span data-ttu-id="49466-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="49466-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="49466-108">Lo que hará</span><span class="sxs-lookup"><span data-stu-id="49466-108">What you will do</span></span>
<span data-ttu-id="49466-109">Instalar hello Azure interfaz de línea de comandos (CLI de Azure).</span><span class="sxs-lookup"><span data-stu-id="49466-109">Install hello Azure command-line interface (Azure CLI).</span></span> <span data-ttu-id="49466-110">Si tiene problemas, buscar soluciones en hello [página solución de problemas](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="49466-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="49466-111">Lo qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="49466-111">What you will learn</span></span>
<span data-ttu-id="49466-112">En este artículo, aprenderá lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="49466-112">In this article, you will learn:</span></span>
* <span data-ttu-id="49466-113">¿Cómo tooinstall Hola CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="49466-113">How tooinstall hello Azure CLI.</span></span>
* <span data-ttu-id="49466-114">¿Cómo tooadd un subgrupo de IoT de hello CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="49466-114">How tooadd an IoT subgroup of hello Azure CLI.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="49466-115">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="49466-115">What you need</span></span>
* <span data-ttu-id="49466-116">Un equipo con Ubuntu con conexión a Internet.</span><span class="sxs-lookup"><span data-stu-id="49466-116">An Ubuntu computer with an Internet connection.</span></span>
* <span data-ttu-id="49466-117">Una suscripción de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="49466-117">An active Azure subscription.</span></span> <span data-ttu-id="49466-118">Si no tiene ninguna, puede crear una [cuenta de evaluación gratuita](http://azure.microsoft.com/pricing/free-trial/) en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="49466-118">If you don't have an account, you can create a [free trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>

## <a name="install-hello-azure-cli"></a><span data-ttu-id="49466-119">Instalar Hola CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="49466-119">Install hello Azure CLI</span></span>
<span data-ttu-id="49466-120">Hola CLI de Azure proporciona una experiencia multiplataforma de línea de comandos de Azure, permitiéndole toowork directamente desde la línea de comandos tooprovision y administrar los recursos.</span><span class="sxs-lookup"><span data-stu-id="49466-120">hello Azure CLI provides a multiplatform command-line experience for Azure, enabling you toowork directly from your command line tooprovision and manage resources.</span></span>

<span data-ttu-id="49466-121">tooinstall Hola CLI más reciente de Azure, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="49466-121">tooinstall hello latest Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="49466-122">Ejecute hello siga los comandos en una ventana de terminal.</span><span class="sxs-lookup"><span data-stu-id="49466-122">Run hello following commands in a terminal window.</span></span> <span data-ttu-id="49466-123">Es posible que tarde cinco minutos tooinstall Hola CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="49466-123">It might take five minutes tooinstall hello Azure CLI.</span></span>

   ```bash
   sudo apt-get update
   sudo apt-get install -y libssl-dev libffi-dev
   sudo apt-get install -y python-dev
   sudo apt-get install -y build-essential
   sudo apt-get install -y python-pip
   sudo pip install --upgrade azure-cli
   sudo pip install --upgrade azure-cli-iot
   ```
2. <span data-ttu-id="49466-124">Comprobar la instalación de hello ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="49466-124">Verify hello installation by running hello following command:</span></span>

   ```bash
   az iot -h
   ```

<span data-ttu-id="49466-125">Debería ver la siguiente Hola de salida si la instalación de hello es correcta.</span><span class="sxs-lookup"><span data-stu-id="49466-125">You should see hello following output if hello installation is successful.</span></span>

![Resultado que indica una instalación correcta](media/iot-hub-raspberry-pi-lessons/lesson2/az_iot_help_ubuntu.png)

## <a name="summary"></a><span data-ttu-id="49466-127">Resumen</span><span class="sxs-lookup"><span data-stu-id="49466-127">Summary</span></span>
<span data-ttu-id="49466-128">Ha instalado Hola CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="49466-128">You've installed hello Azure CLI.</span></span> <span data-ttu-id="49466-129">La siguiente tarea es toocreate su centro de IoT de Azure y la identidad del dispositivo a través Hola CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="49466-129">Your next task is toocreate your Azure IoT hub and device identity using hello Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="49466-130">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="49466-130">Next steps</span></span>
[<span data-ttu-id="49466-131">Creación de un centro de IoT y registro de Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="49466-131">Create your IoT hub and register Raspberry Pi 3</span></span>](iot-hub-raspberry-pi-kit-c-lesson2-prepare-azure-iot-hub.md)

