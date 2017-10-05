---
title: "Características de Azure Cloud Shell (versión preliminar) | Microsoft Docs"
description: "Introducción a las características de Azure Cloud Shell"
services: 
documentationcenter: 
author: jluk
manager: timlt
tags: azure-resource-manager
ms.assetid: 
ms.service: azure
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: juluk
ms.openlocfilehash: 67f03d5857e37b253ac57536e289b5468d69e9b5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="features-and-tools-for-azure-cloud-shell"></a><span data-ttu-id="95f57-103">Características y herramientas para Azure Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="95f57-103">Features and Tools for Azure Cloud Shell</span></span>
<span data-ttu-id="95f57-104">Azure Cloud Shell es una experiencia de shell basado en el explorador para administrar y desarrollar recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="95f57-104">Azure Cloud Shell is a browser-based shell experience to manage and develop Azure resources.</span></span>

<span data-ttu-id="95f57-105">Cloud Shell ofrece una experiencia de shell preconfigurado y accesible desde el explorador para administrar recursos de Azure sin el trabajo añadido de realizar la instalación, el control de versiones y el mantenimiento de una máquina de forma manual.</span><span class="sxs-lookup"><span data-stu-id="95f57-105">Cloud Shell offers a browser-accessible, pre-configured shell experience for managing Azure resources without the overhead of installing, versioning, and maintaining a machine yourself.</span></span>

<span data-ttu-id="95f57-106">Cloud Shell aprovisiona máquinas a medida que se solicitan y, por tanto, el estado de la máquina no se conservará entre sesiones.</span><span class="sxs-lookup"><span data-stu-id="95f57-106">Cloud Shell provisions machines on a per-request basis and as a result machine state will not persist across sessions.</span></span> <span data-ttu-id="95f57-107">Como Cloud Shell se ha creado para sesiones interactivas, los shells finalizan automáticamente después de 20 minutos de inactividad.</span><span class="sxs-lookup"><span data-stu-id="95f57-107">Since Cloud Shell is built for interactive sessions, shells automatically terminate after 20 minutes of shell inactivity.</span></span>

## <a name="bash-in-cloud-shell"></a><span data-ttu-id="95f57-108">Bash en Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="95f57-108">Bash in Cloud Shell</span></span>
### <a name="tools"></a><span data-ttu-id="95f57-109">Herramientas</span><span class="sxs-lookup"><span data-stu-id="95f57-109">Tools</span></span>
|<span data-ttu-id="95f57-110">Categoría</span><span class="sxs-lookup"><span data-stu-id="95f57-110">Category</span></span>   |<span data-ttu-id="95f57-111">Nombre</span><span class="sxs-lookup"><span data-stu-id="95f57-111">Name</span></span>   |
|---|---|
|<span data-ttu-id="95f57-112">Intérprete de shell de Linux</span><span class="sxs-lookup"><span data-stu-id="95f57-112">Linux shell interpreter</span></span>|<span data-ttu-id="95f57-113">Bash</span><span class="sxs-lookup"><span data-stu-id="95f57-113">Bash</span></span><br> <span data-ttu-id="95f57-114">sh</span><span class="sxs-lookup"><span data-stu-id="95f57-114">sh</span></span>               |
|<span data-ttu-id="95f57-115">Herramientas de Azure</span><span class="sxs-lookup"><span data-stu-id="95f57-115">Azure tools</span></span>            |<span data-ttu-id="95f57-116">[CLI de Azure 2.0](https://github.com/Azure/azure-cli) y [1.0](https://github.com/Azure/azure-xplat-cli)</span><span class="sxs-lookup"><span data-stu-id="95f57-116">[Azure CLI 2.0](https://github.com/Azure/azure-cli) and [1.0](https://github.com/Azure/azure-xplat-cli)</span></span><br> [<span data-ttu-id="95f57-117">AzCopy</span><span class="sxs-lookup"><span data-stu-id="95f57-117">AzCopy</span></span>](https://docs.microsoft.com/azure/storage/storage-use-azcopy)<br> [<span data-ttu-id="95f57-118">Batch Shipyard</span><span class="sxs-lookup"><span data-stu-id="95f57-118">Batch Shipyard</span></span>](https://github.com/Azure/batch-shipyard)     |
|<span data-ttu-id="95f57-119">Editores de texto</span><span class="sxs-lookup"><span data-stu-id="95f57-119">Text editors</span></span>           |<span data-ttu-id="95f57-120">vim</span><span class="sxs-lookup"><span data-stu-id="95f57-120">vim</span></span><br> <span data-ttu-id="95f57-121">nano</span><span class="sxs-lookup"><span data-stu-id="95f57-121">nano</span></span><br> <span data-ttu-id="95f57-122">emacs</span><span class="sxs-lookup"><span data-stu-id="95f57-122">emacs</span></span>       |
|<span data-ttu-id="95f57-123">Control de código fuente</span><span class="sxs-lookup"><span data-stu-id="95f57-123">Source control</span></span>         |<span data-ttu-id="95f57-124">git</span><span class="sxs-lookup"><span data-stu-id="95f57-124">git</span></span>                    |
|<span data-ttu-id="95f57-125">Herramientas de compilación</span><span class="sxs-lookup"><span data-stu-id="95f57-125">Build tools</span></span>            |<span data-ttu-id="95f57-126">make</span><span class="sxs-lookup"><span data-stu-id="95f57-126">make</span></span><br> <span data-ttu-id="95f57-127">maven</span><span class="sxs-lookup"><span data-stu-id="95f57-127">maven</span></span><br> <span data-ttu-id="95f57-128">npm</span><span class="sxs-lookup"><span data-stu-id="95f57-128">npm</span></span><br> <span data-ttu-id="95f57-129">pip</span><span class="sxs-lookup"><span data-stu-id="95f57-129">pip</span></span>         |
|<span data-ttu-id="95f57-130">Contenedores</span><span class="sxs-lookup"><span data-stu-id="95f57-130">Containers</span></span>             |<span data-ttu-id="95f57-131">[CLI de Docker](https://github.com/docker/cli)/[Docker Machine](https://github.com/docker/machine)</span><span class="sxs-lookup"><span data-stu-id="95f57-131">[Docker CLI](https://github.com/docker/cli)/[Docker Machine](https://github.com/docker/machine)</span></span><br> [<span data-ttu-id="95f57-132">Kubectl</span><span class="sxs-lookup"><span data-stu-id="95f57-132">Kubectl</span></span>](https://kubernetes.io/docs/user-guide/kubectl-overview/)<br> [<span data-ttu-id="95f57-133">Draft</span><span class="sxs-lookup"><span data-stu-id="95f57-133">Draft</span></span>](https://github.com/Azure/draft)<br> [<span data-ttu-id="95f57-134">CLI de DC/OS</span><span class="sxs-lookup"><span data-stu-id="95f57-134">DC/OS CLI</span></span>](https://github.com/dcos/dcos-cli)         |
|<span data-ttu-id="95f57-135">Bases de datos</span><span class="sxs-lookup"><span data-stu-id="95f57-135">Databases</span></span>              |<span data-ttu-id="95f57-136">Cliente de MySQL</span><span class="sxs-lookup"><span data-stu-id="95f57-136">MySQL client</span></span><br> <span data-ttu-id="95f57-137">Cliente de PostgreSql</span><span class="sxs-lookup"><span data-stu-id="95f57-137">PostgreSql client</span></span><br> [<span data-ttu-id="95f57-138">Utilidad sqlcmd</span><span class="sxs-lookup"><span data-stu-id="95f57-138">sqlcmd Utility</span></span>](https://docs.microsoft.com/sql/tools/sqlcmd-utility)<br> [<span data-ttu-id="95f57-139">mssql-scripter</span><span class="sxs-lookup"><span data-stu-id="95f57-139">mssql-scripter</span></span>](https://github.com/Microsoft/sql-xplat-cli) |
|<span data-ttu-id="95f57-140">Otros</span><span class="sxs-lookup"><span data-stu-id="95f57-140">Other</span></span>                  |<span data-ttu-id="95f57-141">Cliente de iPython</span><span class="sxs-lookup"><span data-stu-id="95f57-141">iPython Client</span></span><br> [<span data-ttu-id="95f57-142">CLI de Cloud Foundry</span><span class="sxs-lookup"><span data-stu-id="95f57-142">Cloud Foundry CLI</span></span>](https://github.com/cloudfoundry/cli)<br> |

### <a name="language-support"></a><span data-ttu-id="95f57-143">Compatibilidad con idiomas</span><span class="sxs-lookup"><span data-stu-id="95f57-143">Language support</span></span>
|<span data-ttu-id="95f57-144">language</span><span class="sxs-lookup"><span data-stu-id="95f57-144">Language</span></span>   |<span data-ttu-id="95f57-145">Versión</span><span class="sxs-lookup"><span data-stu-id="95f57-145">Version</span></span>   |
|---|---|
|<span data-ttu-id="95f57-146">.NET</span><span class="sxs-lookup"><span data-stu-id="95f57-146">.NET</span></span>       |<span data-ttu-id="95f57-147">1.01</span><span class="sxs-lookup"><span data-stu-id="95f57-147">1.01</span></span>       |
|<span data-ttu-id="95f57-148">Go</span><span class="sxs-lookup"><span data-stu-id="95f57-148">Go</span></span>         |<span data-ttu-id="95f57-149">1.7</span><span class="sxs-lookup"><span data-stu-id="95f57-149">1.7</span></span>        |
|<span data-ttu-id="95f57-150">Java</span><span class="sxs-lookup"><span data-stu-id="95f57-150">Java</span></span>       |<span data-ttu-id="95f57-151">1.8</span><span class="sxs-lookup"><span data-stu-id="95f57-151">1.8</span></span>        |
|<span data-ttu-id="95f57-152">Node.js</span><span class="sxs-lookup"><span data-stu-id="95f57-152">Node.js</span></span>    |<span data-ttu-id="95f57-153">6.9.4</span><span class="sxs-lookup"><span data-stu-id="95f57-153">6.9.4</span></span>      |
|<span data-ttu-id="95f57-154">Python</span><span class="sxs-lookup"><span data-stu-id="95f57-154">Python</span></span>     |<span data-ttu-id="95f57-155">2.7 y 3.5 (predeterminadas)</span><span class="sxs-lookup"><span data-stu-id="95f57-155">2.7 and 3.5 (default)</span></span>|

## <a name="secure-automatic-authentication"></a><span data-ttu-id="95f57-156">Protección de la autenticación automática</span><span class="sxs-lookup"><span data-stu-id="95f57-156">Secure automatic authentication</span></span>
<span data-ttu-id="95f57-157">Cloud Shell autentica de forma segura y automática el acceso a la cuenta para la CLI de Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="95f57-157">Cloud Shell securely and automatically authenticates account access for the Azure CLI 2.0.</span></span>

## <a name="azure-files-persistence"></a><span data-ttu-id="95f57-158">Persistencia de Azure Files</span><span class="sxs-lookup"><span data-stu-id="95f57-158">Azure Files persistence</span></span>
<span data-ttu-id="95f57-159">Dado que Cloud Shell se asigna para cada solicitud mediante una máquina temporal, los archivos fuera de $Home y el estado de la máquina no se conservan entre sesiones.</span><span class="sxs-lookup"><span data-stu-id="95f57-159">Since Cloud Shell is allocated on a per-request basis using a temporary machine, files outside of your $Home and machine state are not persisted across sessions.</span></span>
<span data-ttu-id="95f57-160">Para conservar archivos entre sesiones, la primera vez que se inicia Cloud Shell se explica cómo conectar un recurso compartido de archivos de Azure.</span><span class="sxs-lookup"><span data-stu-id="95f57-160">To persist files across sessions, Cloud Shell walks you through attaching an Azure file share on first launch.</span></span>
<span data-ttu-id="95f57-161">Una vez finalizado, Cloud Shell conectará automáticamente su almacenamiento para todas las sesiones futuras.</span><span class="sxs-lookup"><span data-stu-id="95f57-161">Once completed Cloud Shell will automatically attach your storage for all future sessions.</span></span>

<span data-ttu-id="95f57-162">[Obtenga más información sobre cómo conectar recursos compartidos de archivos de Azure a Cloud Shell](persisting-shell-storage.md).</span><span class="sxs-lookup"><span data-stu-id="95f57-162">[Learn more about attaching Azure file shares to Cloud Shell.](persisting-shell-storage.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="95f57-163">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="95f57-163">Next steps</span></span>
[<span data-ttu-id="95f57-164">Inicio rápido de Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="95f57-164">Cloud Shell Quickstart</span></span>](quickstart.md) <br><span data-ttu-id="95f57-165">
[Más información sobre la CLI de Azure 2.0](https://docs.microsoft.com/cli/azure/)</span><span class="sxs-lookup"><span data-stu-id="95f57-165">
[Learn about Azure CLI 2.0](https://docs.microsoft.com/cli/azure/)</span></span> <br>