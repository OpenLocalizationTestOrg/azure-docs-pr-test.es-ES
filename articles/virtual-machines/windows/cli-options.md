---
title: Uso de la CLI de Azure en Windows | Microsoft Docs
description: Uso de la CLI de Azure en Windows
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 02/14/2017
ms.author: nepeters
ms.openlocfilehash: be02ad0d7752cb08f092deeb5a86dcd126403237
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="using-the-azure-cli-on-windows"></a><span data-ttu-id="dbe0b-103">Uso de la CLI de Azure en Windows</span><span class="sxs-lookup"><span data-stu-id="dbe0b-103">Using the Azure CLI on Windows</span></span>

<span data-ttu-id="dbe0b-104">La interfaz de línea de comandos (CLI) de Azure proporciona un entorno de scripting para crear y administrar recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="dbe0b-104">The Azure Command Line Interface (CLI) provides a command line and scripting environment for creating and managing Azure resources.</span></span> <span data-ttu-id="dbe0b-105">La CLI de Azure está disponible para los sistemas operativos Windows, Linux y macOS.</span><span class="sxs-lookup"><span data-stu-id="dbe0b-105">The Azure CLI is available for macOS, Linux, and Windows operating systems.</span></span> <span data-ttu-id="dbe0b-106">En estos sistemas operativos, los comandos de la CLI son idénticos; sin embargo, puede diferir la sintaxis de scripting de cada sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="dbe0b-106">Across these operating systems, the CLI commands are identical, however operating system specific scripting syntax can differ.</span></span>

<span data-ttu-id="dbe0b-107">En este documento se describen las maneras en que la CLI de Azure se puede instalar y ejecutar en Windows, y ofrece información sobre las consideraciones sintácticas de cada uno.</span><span class="sxs-lookup"><span data-stu-id="dbe0b-107">This document details the ways that the Azure CLI can be installed and run on Windows and details syntactical considerations for each.</span></span> <span data-ttu-id="dbe0b-108">Para documentación más detallada sobre la CLI de Azure, consulte la [documentación de la CLI de Azure]( https://docs.microsoft.com/en-us/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="dbe0b-108">For in-depth Azure CLI documentation see, [Azure CLI documentation]( https://docs.microsoft.com/en-us/cli/azure/overview).</span></span>

## <a name="windows-subsystem-for-linux"></a><span data-ttu-id="dbe0b-109">Subsistema de Windows para Linux</span><span class="sxs-lookup"><span data-stu-id="dbe0b-109">Windows Subsystem for Linux</span></span>

<span data-ttu-id="dbe0b-110">El subsistema de Windows para Linux (WSL) proporciona un entorno Linux de Ubuntu en Windows 10 Anniversary Edition y ediciones posteriores.</span><span class="sxs-lookup"><span data-stu-id="dbe0b-110">The Windows Subsystem for Linux (WSL) provides an Ubuntu Linux environment on Windows 10 Anniversary and later editions.</span></span> <span data-ttu-id="dbe0b-111">Cuando está habilitado, WSL proporciona una experiencia de Bash nativa que se puede usar para crear y ejecutar scripts de la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="dbe0b-111">When enabled, WSL provides a native Bash experience, which can be used for creating and running Azure CLI scripts.</span></span> <span data-ttu-id="dbe0b-112">Como WSL proporciona una experiencia de Bash nativa, los scripts de la CLI de Azure pueden compartirse entre macOS, Linux y Windows sin ninguna modificación.</span><span class="sxs-lookup"><span data-stu-id="dbe0b-112">Because WSL provides a native Bash experience, Azure CLI scripts can be shared between macOS, Linux, and Windows without modification.</span></span>

<span data-ttu-id="dbe0b-113">Para usar la CLI de Azure en WSL, haga lo siguiente.</span><span class="sxs-lookup"><span data-stu-id="dbe0b-113">To use the Azure CLI in WSL, complete the following.</span></span>

|<span data-ttu-id="dbe0b-114">Tarea</span><span class="sxs-lookup"><span data-stu-id="dbe0b-114">Task</span></span> | <span data-ttu-id="dbe0b-115">Instrucciones</span><span class="sxs-lookup"><span data-stu-id="dbe0b-115">Instructions</span></span> |
|---|---|
| <span data-ttu-id="dbe0b-116">Habilitación de WSL</span><span class="sxs-lookup"><span data-stu-id="dbe0b-116">Enable WSL</span></span> | [<span data-ttu-id="dbe0b-117">Instalación de la documentación de WSL</span><span class="sxs-lookup"><span data-stu-id="dbe0b-117">Install WSL documentation </span></span>](https://msdn.microsoft.com/en-us/commandline/wsl/install_guide) |
| <span data-ttu-id="dbe0b-118">Instalación de la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="dbe0b-118">Install the Azure CLI</span></span> |[<span data-ttu-id="dbe0b-119">Instalación de la CLI en WSL/Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="dbe0b-119">Install the CLI on WSL/Ubuntu 14.04</span></span>](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2#ubuntu)|

## <a name="powershell"></a><span data-ttu-id="dbe0b-120">PowerShell</span><span class="sxs-lookup"><span data-stu-id="dbe0b-120">PowerShell</span></span>

<span data-ttu-id="dbe0b-121">La CLI de Azure se puede ejecutar de forma nativa en Windows.</span><span class="sxs-lookup"><span data-stu-id="dbe0b-121">The Azure CLI can be run natively in Windows.</span></span> <span data-ttu-id="dbe0b-122">En esta configuración, el paquete de la CLI de Azure está instalado en el sistema operativo Windows y se pueden ejecutar comandos de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="dbe0b-122">In this configuration, the Azure CLI package is installed on the Windows operating system, and commands can be run from PowerShell.</span></span> <span data-ttu-id="dbe0b-123">En esta configuración, los scripts y comandos de la CLI de Azure se pueden ejecutar en cualquier versión admitida de Windows; sin embargo, se requiere la sintaxis de scripts específica de cada plataforma.</span><span class="sxs-lookup"><span data-stu-id="dbe0b-123">In this configuration, Azure CLI commands and scripts can be run on any supported version of Windows, however platform specific scripting syntax is required.</span></span> <span data-ttu-id="dbe0b-124">Por este motivo, los scripts no se comparten necesariamente entre macOS, Linux y Windows sin ninguna modificación.</span><span class="sxs-lookup"><span data-stu-id="dbe0b-124">Because of this, scripts cannot necessarily be shared between macOS, Linux, and Windows without modification.</span></span>

<span data-ttu-id="dbe0b-125">Para usar la CLI de Azure en Windows, instale el paquete siguiendo estas instrucciones, [Instalación de la CLI en Windows](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2#windows).</span><span class="sxs-lookup"><span data-stu-id="dbe0b-125">To use the Azure CLI on Windows, install the package using these instructions, [Install the CLI on Windows](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2#windows).</span></span>

## <a name="docker-image"></a><span data-ttu-id="dbe0b-126">Imagen de Docker</span><span class="sxs-lookup"><span data-stu-id="dbe0b-126">Docker Image</span></span>

<span data-ttu-id="dbe0b-127">Cuando se usa Docker para Windows, se puede iniciar una imagen de Docker que incluye la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="dbe0b-127">When using Docker for Windows, a Docker image can be started that includes the Azure CLI.</span></span> <span data-ttu-id="dbe0b-128">Esta imagen se basa en Linux e incluye una experiencia de Bash nativa.</span><span class="sxs-lookup"><span data-stu-id="dbe0b-128">This image is based off of Linux, and includes a native Bash experience.</span></span>  <span data-ttu-id="dbe0b-129">Cuando se usa Docker para Windows y la imagen de la CLI de Azure, los scripts deben compartirse entre macOS, Linux y Windows.</span><span class="sxs-lookup"><span data-stu-id="dbe0b-129">When using Docker for Windows and the Azure CLI image, scripts to be shared between macOS, Linux, and Windows.</span></span> 

<span data-ttu-id="dbe0b-130">Para usar la CLI de Azure en Docker para Windows, asegúrese de que se está ejecutando Docker para Windows y ejecute el siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="dbe0b-130">To use the Azure CLI on Docker for Windows, ensure that Docker for Windows is running and run the following command.</span></span>

```bash
docker run -it azuresdk/azure-cli-python:latest bash
```

<span data-ttu-id="dbe0b-131">Una vez completado, se iniciará una sesión de Bash que se cargó previamente con las herramientas de la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="dbe0b-131">Once completed, a Bash session will start that is preloaded with the Azure CLI tools.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dbe0b-132">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="dbe0b-132">Next Steps</span></span>

[<span data-ttu-id="dbe0b-133">Ejemplo de la CLI para máquinas virtuales de Azure</span><span class="sxs-lookup"><span data-stu-id="dbe0b-133">CLI sample for Azure virtual machines</span></span>](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="dbe0b-134">Ejemplos de la CLI para Azure Web Apps</span><span class="sxs-lookup"><span data-stu-id="dbe0b-134">CLI samples for Azure Web Apps</span></span>](../../app-service-web/app-service-cli-samples.md)

[<span data-ttu-id="dbe0b-135">Ejemplos de la CLI para SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="dbe0b-135">CLI samples for Azure SQL</span></span>](../../sql-database/sql-database-cli-samples.md)
