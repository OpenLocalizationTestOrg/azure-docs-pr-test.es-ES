---
title: Hola aaaUsing CLI de Azure en Windows | Documentos de Microsoft
description: Uso de hello CLI de Azure en Windows
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
ms.openlocfilehash: edca4a2701a7dfc0fc54df5649e8a5e7afc95490
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-cli-on-windows"></a><span data-ttu-id="ebd05-103">Uso de hello CLI de Azure en Windows</span><span class="sxs-lookup"><span data-stu-id="ebd05-103">Using hello Azure CLI on Windows</span></span>

<span data-ttu-id="ebd05-104">Hola interfaz de línea de comandos (CLI) de Azure proporciona un entorno de scripting para crear y administrar recursos de Azure y la línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="ebd05-104">hello Azure Command Line Interface (CLI) provides a command line and scripting environment for creating and managing Azure resources.</span></span> <span data-ttu-id="ebd05-105">Hola CLI de Azure está disponible para sistemas operativos Windows, Linux y macOS.</span><span class="sxs-lookup"><span data-stu-id="ebd05-105">hello Azure CLI is available for macOS, Linux, and Windows operating systems.</span></span> <span data-ttu-id="ebd05-106">En estos sistemas operativos, los comandos de CLI de hello son idénticos, sin embargo, puede diferir la sintaxis de scripting de sistema operativo específico.</span><span class="sxs-lookup"><span data-stu-id="ebd05-106">Across these operating systems, hello CLI commands are identical, however operating system specific scripting syntax can differ.</span></span>

<span data-ttu-id="ebd05-107">Formas de detalles Hola este documento que Hola CLI de Azure se pueden instalar y ejecutar en Windows y detalles de las consideraciones de sintáctico para cada uno.</span><span class="sxs-lookup"><span data-stu-id="ebd05-107">This document details hello ways that hello Azure CLI can be installed and run on Windows and details syntactical considerations for each.</span></span> <span data-ttu-id="ebd05-108">Para documentación más detallada sobre la CLI de Azure, consulte la [documentación de la CLI de Azure]( https://docs.microsoft.com/en-us/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ebd05-108">For in-depth Azure CLI documentation see, [Azure CLI documentation]( https://docs.microsoft.com/en-us/cli/azure/overview).</span></span>

## <a name="windows-subsystem-for-linux"></a><span data-ttu-id="ebd05-109">Subsistema de Windows para Linux</span><span class="sxs-lookup"><span data-stu-id="ebd05-109">Windows Subsystem for Linux</span></span>

<span data-ttu-id="ebd05-110">Hola subsistema de Windows para Linux (WSL) proporciona un entorno de Ubuntu Linux en aniversario de Windows 10 y versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="ebd05-110">hello Windows Subsystem for Linux (WSL) provides an Ubuntu Linux environment on Windows 10 Anniversary and later editions.</span></span> <span data-ttu-id="ebd05-111">Cuando está habilitado, WSL proporciona una experiencia de Bash nativa que se puede usar para crear y ejecutar scripts de la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="ebd05-111">When enabled, WSL provides a native Bash experience, which can be used for creating and running Azure CLI scripts.</span></span> <span data-ttu-id="ebd05-112">Como WSL proporciona una experiencia de Bash nativa, los scripts de la CLI de Azure pueden compartirse entre macOS, Linux y Windows sin ninguna modificación.</span><span class="sxs-lookup"><span data-stu-id="ebd05-112">Because WSL provides a native Bash experience, Azure CLI scripts can be shared between macOS, Linux, and Windows without modification.</span></span>

<span data-ttu-id="ebd05-113">Hola toouse CLI de Azure en WSL, complete siguiente de Hola.</span><span class="sxs-lookup"><span data-stu-id="ebd05-113">toouse hello Azure CLI in WSL, complete hello following.</span></span>

|<span data-ttu-id="ebd05-114">Tarea</span><span class="sxs-lookup"><span data-stu-id="ebd05-114">Task</span></span> | <span data-ttu-id="ebd05-115">Instrucciones</span><span class="sxs-lookup"><span data-stu-id="ebd05-115">Instructions</span></span> |
|---|---|
| <span data-ttu-id="ebd05-116">Habilitación de WSL</span><span class="sxs-lookup"><span data-stu-id="ebd05-116">Enable WSL</span></span> | [<span data-ttu-id="ebd05-117">Instalación de la documentación de WSL</span><span class="sxs-lookup"><span data-stu-id="ebd05-117">Install WSL documentation </span></span>](https://msdn.microsoft.com/en-us/commandline/wsl/install_guide) |
| <span data-ttu-id="ebd05-118">Instalar Hola CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="ebd05-118">Install hello Azure CLI</span></span> |[<span data-ttu-id="ebd05-119">Instalar Hola CLI en WSL/Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="ebd05-119">Install hello CLI on WSL/Ubuntu 14.04</span></span>](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2#ubuntu)|

## <a name="powershell"></a><span data-ttu-id="ebd05-120">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ebd05-120">PowerShell</span></span>

<span data-ttu-id="ebd05-121">Hola CLI de Azure se puede ejecutar de forma nativa en Windows.</span><span class="sxs-lookup"><span data-stu-id="ebd05-121">hello Azure CLI can be run natively in Windows.</span></span> <span data-ttu-id="ebd05-122">En esta configuración, paquete de CLI de Azure de hello está instalado en el sistema operativo de Windows de Hola y se pueden ejecutar comandos de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ebd05-122">In this configuration, hello Azure CLI package is installed on hello Windows operating system, and commands can be run from PowerShell.</span></span> <span data-ttu-id="ebd05-123">En esta configuración, los scripts y comandos de la CLI de Azure se pueden ejecutar en cualquier versión admitida de Windows; sin embargo, se requiere la sintaxis de scripts específica de cada plataforma.</span><span class="sxs-lookup"><span data-stu-id="ebd05-123">In this configuration, Azure CLI commands and scripts can be run on any supported version of Windows, however platform specific scripting syntax is required.</span></span> <span data-ttu-id="ebd05-124">Por este motivo, los scripts no se comparten necesariamente entre macOS, Linux y Windows sin ninguna modificación.</span><span class="sxs-lookup"><span data-stu-id="ebd05-124">Because of this, scripts cannot necessarily be shared between macOS, Linux, and Windows without modification.</span></span>

<span data-ttu-id="ebd05-125">Hola toouse CLI de Azure en Windows, instalar el paquete de hello usando estas instrucciones, [Install Hola CLI en Windows](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2#windows).</span><span class="sxs-lookup"><span data-stu-id="ebd05-125">toouse hello Azure CLI on Windows, install hello package using these instructions, [Install hello CLI on Windows](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2#windows).</span></span>

## <a name="docker-image"></a><span data-ttu-id="ebd05-126">Imagen de Docker</span><span class="sxs-lookup"><span data-stu-id="ebd05-126">Docker Image</span></span>

<span data-ttu-id="ebd05-127">Al usar Docker para Windows, se puede iniciar una imagen de Docker que incluye Hola CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="ebd05-127">When using Docker for Windows, a Docker image can be started that includes hello Azure CLI.</span></span> <span data-ttu-id="ebd05-128">Esta imagen se basa en Linux e incluye una experiencia de Bash nativa.</span><span class="sxs-lookup"><span data-stu-id="ebd05-128">This image is based off of Linux, and includes a native Bash experience.</span></span>  <span data-ttu-id="ebd05-129">Cuando se usa Docker para Windows e imagen de CLI de Azure de hello, toobe de secuencias de comandos que se comparten entre macOS, Linux y Windows.</span><span class="sxs-lookup"><span data-stu-id="ebd05-129">When using Docker for Windows and hello Azure CLI image, scripts toobe shared between macOS, Linux, and Windows.</span></span> 

<span data-ttu-id="ebd05-130">Hola toouse CLI de Azure en Docker para Windows, asegúrese de que Docker para Windows se está ejecutando y ejecute el siguiente comando de Hola.</span><span class="sxs-lookup"><span data-stu-id="ebd05-130">toouse hello Azure CLI on Docker for Windows, ensure that Docker for Windows is running and run hello following command.</span></span>

```bash
docker run -it azuresdk/azure-cli-python:latest bash
```

<span data-ttu-id="ebd05-131">Una vez completado, una intensiva de sesión se iniciará decir precargados con herramientas de Azure CLI Hola.</span><span class="sxs-lookup"><span data-stu-id="ebd05-131">Once completed, a Bash session will start that is preloaded with hello Azure CLI tools.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ebd05-132">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ebd05-132">Next Steps</span></span>

[<span data-ttu-id="ebd05-133">Ejemplo de la CLI para máquinas virtuales de Azure</span><span class="sxs-lookup"><span data-stu-id="ebd05-133">CLI sample for Azure virtual machines</span></span>](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="ebd05-134">Ejemplos de la CLI para Azure Web Apps</span><span class="sxs-lookup"><span data-stu-id="ebd05-134">CLI samples for Azure Web Apps</span></span>](../../app-service-web/app-service-cli-samples.md)

[<span data-ttu-id="ebd05-135">Ejemplos de la CLI para SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="ebd05-135">CLI samples for Azure SQL</span></span>](../../sql-database/sql-database-cli-samples.md)
