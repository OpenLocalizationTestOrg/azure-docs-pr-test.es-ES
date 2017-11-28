---
title: "características de Shell en la nube (versión preliminar) aaaAzure | Documentos de Microsoft"
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
ms.openlocfilehash: 65482ca6caeac01dda18a6b12eabe943e3d68a96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="features-and-tools-for-azure-cloud-shell"></a><span data-ttu-id="0eddd-103">Características y herramientas para Azure Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="0eddd-103">Features and Tools for Azure Cloud Shell</span></span>
<span data-ttu-id="0eddd-104">Shell de nube de Azure es un toomanage de experiencia de shell basado en un explorador y desarrollar recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="0eddd-104">Azure Cloud Shell is a browser-based shell experience toomanage and develop Azure resources.</span></span>

<span data-ttu-id="0eddd-105">Shell de nube ofrece un explorador accesible, preconfigurado y experiencia de shell de administración de recursos de Azure sin sobrecarga de Hola de instalar, control de versiones y el mantenimiento de una máquina usted mismo.</span><span class="sxs-lookup"><span data-stu-id="0eddd-105">Cloud Shell offers a browser-accessible, pre-configured shell experience for managing Azure resources without hello overhead of installing, versioning, and maintaining a machine yourself.</span></span>

<span data-ttu-id="0eddd-106">Cloud Shell aprovisiona máquinas a medida que se solicitan y, por tanto, el estado de la máquina no se conservará entre sesiones.</span><span class="sxs-lookup"><span data-stu-id="0eddd-106">Cloud Shell provisions machines on a per-request basis and as a result machine state will not persist across sessions.</span></span> <span data-ttu-id="0eddd-107">Como Cloud Shell se ha creado para sesiones interactivas, los shells finalizan automáticamente después de 20 minutos de inactividad.</span><span class="sxs-lookup"><span data-stu-id="0eddd-107">Since Cloud Shell is built for interactive sessions, shells automatically terminate after 20 minutes of shell inactivity.</span></span>

## <a name="bash-in-cloud-shell"></a><span data-ttu-id="0eddd-108">Bash en Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="0eddd-108">Bash in Cloud Shell</span></span>
### <a name="tools"></a><span data-ttu-id="0eddd-109">Herramientas</span><span class="sxs-lookup"><span data-stu-id="0eddd-109">Tools</span></span>
|<span data-ttu-id="0eddd-110">Categoría</span><span class="sxs-lookup"><span data-stu-id="0eddd-110">Category</span></span>   |<span data-ttu-id="0eddd-111">Nombre</span><span class="sxs-lookup"><span data-stu-id="0eddd-111">Name</span></span>   |
|---|---|
|<span data-ttu-id="0eddd-112">Intérprete de shell de Linux</span><span class="sxs-lookup"><span data-stu-id="0eddd-112">Linux shell interpreter</span></span>|<span data-ttu-id="0eddd-113">Bash</span><span class="sxs-lookup"><span data-stu-id="0eddd-113">Bash</span></span><br> <span data-ttu-id="0eddd-114">sh</span><span class="sxs-lookup"><span data-stu-id="0eddd-114">sh</span></span>               |
|<span data-ttu-id="0eddd-115">Herramientas de Azure</span><span class="sxs-lookup"><span data-stu-id="0eddd-115">Azure tools</span></span>            |<span data-ttu-id="0eddd-116">[CLI de Azure 2.0](https://github.com/Azure/azure-cli) y [1.0](https://github.com/Azure/azure-xplat-cli)</span><span class="sxs-lookup"><span data-stu-id="0eddd-116">[Azure CLI 2.0](https://github.com/Azure/azure-cli) and [1.0](https://github.com/Azure/azure-xplat-cli)</span></span><br> [<span data-ttu-id="0eddd-117">AzCopy</span><span class="sxs-lookup"><span data-stu-id="0eddd-117">AzCopy</span></span>](https://docs.microsoft.com/azure/storage/storage-use-azcopy)<br> [<span data-ttu-id="0eddd-118">Batch Shipyard</span><span class="sxs-lookup"><span data-stu-id="0eddd-118">Batch Shipyard</span></span>](https://github.com/Azure/batch-shipyard)     |
|<span data-ttu-id="0eddd-119">Editores de texto</span><span class="sxs-lookup"><span data-stu-id="0eddd-119">Text editors</span></span>           |<span data-ttu-id="0eddd-120">vim</span><span class="sxs-lookup"><span data-stu-id="0eddd-120">vim</span></span><br> <span data-ttu-id="0eddd-121">nano</span><span class="sxs-lookup"><span data-stu-id="0eddd-121">nano</span></span><br> <span data-ttu-id="0eddd-122">emacs</span><span class="sxs-lookup"><span data-stu-id="0eddd-122">emacs</span></span>       |
|<span data-ttu-id="0eddd-123">Control de código fuente</span><span class="sxs-lookup"><span data-stu-id="0eddd-123">Source control</span></span>         |<span data-ttu-id="0eddd-124">git</span><span class="sxs-lookup"><span data-stu-id="0eddd-124">git</span></span>                    |
|<span data-ttu-id="0eddd-125">Herramientas de compilación</span><span class="sxs-lookup"><span data-stu-id="0eddd-125">Build tools</span></span>            |<span data-ttu-id="0eddd-126">make</span><span class="sxs-lookup"><span data-stu-id="0eddd-126">make</span></span><br> <span data-ttu-id="0eddd-127">maven</span><span class="sxs-lookup"><span data-stu-id="0eddd-127">maven</span></span><br> <span data-ttu-id="0eddd-128">npm</span><span class="sxs-lookup"><span data-stu-id="0eddd-128">npm</span></span><br> <span data-ttu-id="0eddd-129">pip</span><span class="sxs-lookup"><span data-stu-id="0eddd-129">pip</span></span>         |
|<span data-ttu-id="0eddd-130">Contenedores</span><span class="sxs-lookup"><span data-stu-id="0eddd-130">Containers</span></span>             |<span data-ttu-id="0eddd-131">[CLI de Docker](https://github.com/docker/cli)/[Docker Machine](https://github.com/docker/machine)</span><span class="sxs-lookup"><span data-stu-id="0eddd-131">[Docker CLI](https://github.com/docker/cli)/[Docker Machine](https://github.com/docker/machine)</span></span><br> [<span data-ttu-id="0eddd-132">Kubectl</span><span class="sxs-lookup"><span data-stu-id="0eddd-132">Kubectl</span></span>](https://kubernetes.io/docs/user-guide/kubectl-overview/)<br> [<span data-ttu-id="0eddd-133">Draft</span><span class="sxs-lookup"><span data-stu-id="0eddd-133">Draft</span></span>](https://github.com/Azure/draft)<br> [<span data-ttu-id="0eddd-134">CLI de DC/OS</span><span class="sxs-lookup"><span data-stu-id="0eddd-134">DC/OS CLI</span></span>](https://github.com/dcos/dcos-cli)         |
|<span data-ttu-id="0eddd-135">Bases de datos</span><span class="sxs-lookup"><span data-stu-id="0eddd-135">Databases</span></span>              |<span data-ttu-id="0eddd-136">Cliente de MySQL</span><span class="sxs-lookup"><span data-stu-id="0eddd-136">MySQL client</span></span><br> <span data-ttu-id="0eddd-137">Cliente de PostgreSql</span><span class="sxs-lookup"><span data-stu-id="0eddd-137">PostgreSql client</span></span><br> [<span data-ttu-id="0eddd-138">Utilidad sqlcmd</span><span class="sxs-lookup"><span data-stu-id="0eddd-138">sqlcmd Utility</span></span>](https://docs.microsoft.com/sql/tools/sqlcmd-utility)<br> [<span data-ttu-id="0eddd-139">mssql-scripter</span><span class="sxs-lookup"><span data-stu-id="0eddd-139">mssql-scripter</span></span>](https://github.com/Microsoft/sql-xplat-cli) |
|<span data-ttu-id="0eddd-140">Otros</span><span class="sxs-lookup"><span data-stu-id="0eddd-140">Other</span></span>                  |<span data-ttu-id="0eddd-141">Cliente de iPython</span><span class="sxs-lookup"><span data-stu-id="0eddd-141">iPython Client</span></span><br> [<span data-ttu-id="0eddd-142">CLI de Cloud Foundry</span><span class="sxs-lookup"><span data-stu-id="0eddd-142">Cloud Foundry CLI</span></span>](https://github.com/cloudfoundry/cli)<br> |

### <a name="language-support"></a><span data-ttu-id="0eddd-143">Compatibilidad con idiomas</span><span class="sxs-lookup"><span data-stu-id="0eddd-143">Language support</span></span>
|<span data-ttu-id="0eddd-144">language</span><span class="sxs-lookup"><span data-stu-id="0eddd-144">Language</span></span>   |<span data-ttu-id="0eddd-145">Versión</span><span class="sxs-lookup"><span data-stu-id="0eddd-145">Version</span></span>   |
|---|---|
|<span data-ttu-id="0eddd-146">.NET</span><span class="sxs-lookup"><span data-stu-id="0eddd-146">.NET</span></span>       |<span data-ttu-id="0eddd-147">1.01</span><span class="sxs-lookup"><span data-stu-id="0eddd-147">1.01</span></span>       |
|<span data-ttu-id="0eddd-148">Go</span><span class="sxs-lookup"><span data-stu-id="0eddd-148">Go</span></span>         |<span data-ttu-id="0eddd-149">1.7</span><span class="sxs-lookup"><span data-stu-id="0eddd-149">1.7</span></span>        |
|<span data-ttu-id="0eddd-150">Java</span><span class="sxs-lookup"><span data-stu-id="0eddd-150">Java</span></span>       |<span data-ttu-id="0eddd-151">1.8</span><span class="sxs-lookup"><span data-stu-id="0eddd-151">1.8</span></span>        |
|<span data-ttu-id="0eddd-152">Node.js</span><span class="sxs-lookup"><span data-stu-id="0eddd-152">Node.js</span></span>    |<span data-ttu-id="0eddd-153">6.9.4</span><span class="sxs-lookup"><span data-stu-id="0eddd-153">6.9.4</span></span>      |
|<span data-ttu-id="0eddd-154">Python</span><span class="sxs-lookup"><span data-stu-id="0eddd-154">Python</span></span>     |<span data-ttu-id="0eddd-155">2.7 y 3.5 (predeterminadas)</span><span class="sxs-lookup"><span data-stu-id="0eddd-155">2.7 and 3.5 (default)</span></span>|

## <a name="secure-automatic-authentication"></a><span data-ttu-id="0eddd-156">Protección de la autenticación automática</span><span class="sxs-lookup"><span data-stu-id="0eddd-156">Secure automatic authentication</span></span>
<span data-ttu-id="0eddd-157">En la nube Shell automáticamente y de forma segura autentica el acceso de cuenta de hello 2.0 de CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="0eddd-157">Cloud Shell securely and automatically authenticates account access for hello Azure CLI 2.0.</span></span>

## <a name="azure-files-persistence"></a><span data-ttu-id="0eddd-158">Persistencia de Azure Files</span><span class="sxs-lookup"><span data-stu-id="0eddd-158">Azure Files persistence</span></span>
<span data-ttu-id="0eddd-159">Dado que Cloud Shell se asigna para cada solicitud mediante una máquina temporal, los archivos fuera de $Home y el estado de la máquina no se conservan entre sesiones.</span><span class="sxs-lookup"><span data-stu-id="0eddd-159">Since Cloud Shell is allocated on a per-request basis using a temporary machine, files outside of your $Home and machine state are not persisted across sessions.</span></span>
<span data-ttu-id="0eddd-160">archivos de toopersist entre las sesiones, los recorridos de Shell en la nube a través de adjuntar un archivo de Azure comparten en el primer inicio.</span><span class="sxs-lookup"><span data-stu-id="0eddd-160">toopersist files across sessions, Cloud Shell walks you through attaching an Azure file share on first launch.</span></span>
<span data-ttu-id="0eddd-161">Una vez finalizado, Cloud Shell conectará automáticamente su almacenamiento para todas las sesiones futuras.</span><span class="sxs-lookup"><span data-stu-id="0eddd-161">Once completed Cloud Shell will automatically attach your storage for all future sessions.</span></span>

[<span data-ttu-id="0eddd-162">Más información acerca de cómo adjuntar tooCloud de recursos compartidos de archivos de Azure Shell.</span><span class="sxs-lookup"><span data-stu-id="0eddd-162">Learn more about attaching Azure file shares tooCloud Shell.</span></span>](persisting-shell-storage.md)

## <a name="next-steps"></a><span data-ttu-id="0eddd-163">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0eddd-163">Next steps</span></span>
[<span data-ttu-id="0eddd-164">Inicio rápido de Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="0eddd-164">Cloud Shell Quickstart</span></span>](quickstart.md) <br><span data-ttu-id="0eddd-165">
[Más información sobre la CLI de Azure 2.0](https://docs.microsoft.com/cli/azure/)</span><span class="sxs-lookup"><span data-stu-id="0eddd-165">
[Learn about Azure CLI 2.0](https://docs.microsoft.com/cli/azure/)</span></span> <br>