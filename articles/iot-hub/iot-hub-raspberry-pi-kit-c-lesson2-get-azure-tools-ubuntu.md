---
title: "Conexión de Raspberry Pi (C) a Azure IoT: Lección 2: Herramientas de Azure (Ubuntu) | Microsoft Docs"
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
ms.openlocfilehash: be1506edf0e63190dbb85a3adb7897bd1cc84d38
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="get-azure-tools-ubuntu-1604"></a><span data-ttu-id="1baae-104">Obtención de las herramientas de Azure (Ubuntu 16.04)</span><span class="sxs-lookup"><span data-stu-id="1baae-104">Get Azure tools (Ubuntu 16.04)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1baae-105">Windows 7 y versiones posteriores</span><span class="sxs-lookup"><span data-stu-id="1baae-105">Windows 7 and later</span></span>](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-win32.md)
> * [<span data-ttu-id="1baae-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="1baae-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-ubuntu.md)
> * [<span data-ttu-id="1baae-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="1baae-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="1baae-108">Lo que hará</span><span class="sxs-lookup"><span data-stu-id="1baae-108">What you will do</span></span>
<span data-ttu-id="1baae-109">Instalación de la interfaz de la línea de comandos de Azure (CLI de Azure)</span><span class="sxs-lookup"><span data-stu-id="1baae-109">Install the Azure command-line interface (Azure CLI).</span></span> <span data-ttu-id="1baae-110">Si tiene problemas, busque soluciones en la [página de solución de problemas](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="1baae-110">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="1baae-111">Lo qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="1baae-111">What you will learn</span></span>
<span data-ttu-id="1baae-112">En este artículo, aprenderá lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="1baae-112">In this article, you will learn:</span></span>
* <span data-ttu-id="1baae-113">Cómo instalar la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="1baae-113">How to install the Azure CLI.</span></span>
* <span data-ttu-id="1baae-114">Cómo agregar un subgrupo de IoT de la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="1baae-114">How to add an IoT subgroup of the Azure CLI.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="1baae-115">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="1baae-115">What you need</span></span>
* <span data-ttu-id="1baae-116">Un equipo con Ubuntu con conexión a Internet.</span><span class="sxs-lookup"><span data-stu-id="1baae-116">An Ubuntu computer with an Internet connection.</span></span>
* <span data-ttu-id="1baae-117">Una suscripción de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="1baae-117">An active Azure subscription.</span></span> <span data-ttu-id="1baae-118">Si no tiene ninguna, puede crear una [cuenta de evaluación gratuita](http://azure.microsoft.com/pricing/free-trial/) en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="1baae-118">If you don't have an account, you can create a [free trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>

## <a name="install-the-azure-cli"></a><span data-ttu-id="1baae-119">Instalación de la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="1baae-119">Install the Azure CLI</span></span>
<span data-ttu-id="1baae-120">La CLI de Azure proporciona una experiencia de línea de comandos multiplataforma en Azure, lo que le permite trabajar directamente desde la línea de comandos para aprovisionar y administrar los recursos.</span><span class="sxs-lookup"><span data-stu-id="1baae-120">The Azure CLI provides a multiplatform command-line experience for Azure, enabling you to work directly from your command line to provision and manage resources.</span></span>

<span data-ttu-id="1baae-121">Para instalar la CLI de Azure más recientr, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="1baae-121">To install the latest Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="1baae-122">Ejecute los siguientes comandos en una ventana de terminal.</span><span class="sxs-lookup"><span data-stu-id="1baae-122">Run the following commands in a terminal window.</span></span> <span data-ttu-id="1baae-123">Este proceso puede tardar cinco minutos en instalar la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="1baae-123">It might take five minutes to install the Azure CLI.</span></span>

   ```bash
   sudo apt-get update
   sudo apt-get install -y libssl-dev libffi-dev
   sudo apt-get install -y python-dev
   sudo apt-get install -y build-essential
   sudo apt-get install -y python-pip
   sudo pip install --upgrade azure-cli
   sudo pip install --upgrade azure-cli-iot
   ```
2. <span data-ttu-id="1baae-124">Compruebe la instalación ejecutando el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="1baae-124">Verify the installation by running the following command:</span></span>

   ```bash
   az iot -h
   ```

<span data-ttu-id="1baae-125">Si la instalación se realiza correctamente, verá el siguiente resultado.</span><span class="sxs-lookup"><span data-stu-id="1baae-125">You should see the following output if the installation is successful.</span></span>

![Resultado que indica una instalación correcta](media/iot-hub-raspberry-pi-lessons/lesson2/az_iot_help_ubuntu.png)

## <a name="summary"></a><span data-ttu-id="1baae-127">Resumen</span><span class="sxs-lookup"><span data-stu-id="1baae-127">Summary</span></span>
<span data-ttu-id="1baae-128">Ha instalado la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="1baae-128">You've installed the Azure CLI.</span></span> <span data-ttu-id="1baae-129">La siguiente tarea consiste en crear la identidad de Azure IoT Hub y de dispositivos mediante la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="1baae-129">Your next task is to create your Azure IoT hub and device identity using the Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1baae-130">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1baae-130">Next steps</span></span>
[<span data-ttu-id="1baae-131">Creación de un centro de IoT y registro de Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="1baae-131">Create your IoT hub and register Raspberry Pi 3</span></span>](iot-hub-raspberry-pi-kit-c-lesson2-prepare-azure-iot-hub.md)

