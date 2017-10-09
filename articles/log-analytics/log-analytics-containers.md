---
title: "solución de supervisión en Azure Log Analytics aaaContainer | Documentos de Microsoft"
description: "Hola solución de supervisión de contenedor en el análisis de registros le ayuda a ver y administrar el Docker y Windows hosts de contenedor en una sola ubicación."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: e1e4b52b-92d5-4bfa-8a09-ff8c6b5a9f78
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: magoedte;banders
ms.openlocfilehash: 2eed1dd81c22faef78a375fca3ebece9e5300c09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="container-monitoring-solution-in-log-analytics"></a><span data-ttu-id="ab70c-103">Solución de Supervisión de contenedores de Azure Log Analytics</span><span class="sxs-lookup"><span data-stu-id="ab70c-103">Container Monitoring solution in Log Analytics</span></span>

![Símbolo de Containers](./media/log-analytics-containers/containers-symbol.png)

<span data-ttu-id="ab70c-105">Este artículo describe cómo tooset seguridad y el uso Hola solución de supervisión de contenedor en el análisis de registros, que le ayuda a ver y administrar el Docker y Windows hosts de contenedor en una sola ubicación.</span><span class="sxs-lookup"><span data-stu-id="ab70c-105">This article describes how tooset up and use hello Container Monitoring solution in Log Analytics, which helps you view and manage your Docker and Windows container hosts in a single location.</span></span> <span data-ttu-id="ab70c-106">Docker es un sistema de virtualización de software que usa contenedores toocreate que automatizan la implementación de software tootheir TI infraestructura.</span><span class="sxs-lookup"><span data-stu-id="ab70c-106">Docker is a software virtualization system used toocreate containers that automate software deployment tootheir IT infrastructure.</span></span>

<span data-ttu-id="ab70c-107">Hola solución se muestra qué contenedores se ejecutan, ¿qué imagen de contenedor que se está ejecutando, y donde se ejecutan los contenedores.</span><span class="sxs-lookup"><span data-stu-id="ab70c-107">hello solution shows which containers are running, what container image they’re running, and where containers are running.</span></span> <span data-ttu-id="ab70c-108">Puede ver información de auditoría detallada que muestra los comandos que se usan con los contenedores.</span><span class="sxs-lookup"><span data-stu-id="ab70c-108">You can view detailed audit information showing commands used with containers.</span></span> <span data-ttu-id="ab70c-109">Además, puede solucionar los contenedores de visualización y búsqueda de registros centralizados sin necesidad de vista tooremotely Docker o hosts de Windows.</span><span class="sxs-lookup"><span data-stu-id="ab70c-109">And, you can troubleshoot containers by viewing and searching centralized logs without having tooremotely view Docker or Windows hosts.</span></span> <span data-ttu-id="ab70c-110">Puede encontrar los contenedores que están causando ruido o realizando un consumo excesivo de recursos en un host.</span><span class="sxs-lookup"><span data-stu-id="ab70c-110">You can find containers that may be noisy and consuming excess resources on a host.</span></span> <span data-ttu-id="ab70c-111">También puede ver la información centralizada acerca de la CPU, la memoria, el almacenamiento y el uso y el rendimiento de la red en relación con los contenedores.</span><span class="sxs-lookup"><span data-stu-id="ab70c-111">And, you can view centralized CPU, memory, storage, and network usage and performance information for containers.</span></span> <span data-ttu-id="ab70c-112">En equipos con Windows, puede centralizar y comparar registros de Windows Server, Hyper-V y contenedores de Docker.</span><span class="sxs-lookup"><span data-stu-id="ab70c-112">On computers running Windows, you can centralize and compare logs from Windows Server, Hyper-V, and Docker containers.</span></span> <span data-ttu-id="ab70c-113">solución de Hello admite Hola después orchestrators de contenedor:</span><span class="sxs-lookup"><span data-stu-id="ab70c-113">hello solution supports hello following container orchestrators:</span></span>

- <span data-ttu-id="ab70c-114">Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="ab70c-114">Docker Swarm</span></span>
- <span data-ttu-id="ab70c-115">DC/OS</span><span class="sxs-lookup"><span data-stu-id="ab70c-115">DC/OS</span></span>
- <span data-ttu-id="ab70c-116">kubernetes</span><span class="sxs-lookup"><span data-stu-id="ab70c-116">Kubernetes</span></span>
- <span data-ttu-id="ab70c-117">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="ab70c-117">Service Fabric</span></span>
- <span data-ttu-id="ab70c-118">Red Hat OpenShift</span><span class="sxs-lookup"><span data-stu-id="ab70c-118">Red Hat OpenShift</span></span>


<span data-ttu-id="ab70c-119">Hello siguiente diagrama muestra las relaciones de hello entre varios hosts de contenedor y los agentes con OMS.</span><span class="sxs-lookup"><span data-stu-id="ab70c-119">hello following diagram shows hello relationships between various container hosts and agents with OMS.</span></span>

![Diagrama de contenedores](./media/log-analytics-containers/containers-diagram.png)

## <a name="system-requirements"></a><span data-ttu-id="ab70c-121">Requisitos del sistema</span><span class="sxs-lookup"><span data-stu-id="ab70c-121">System requirements</span></span>

<span data-ttu-id="ab70c-122">Antes de comenzar, revise Hola después tooverify detalles cumplen los requisitos previos de Hola.</span><span class="sxs-lookup"><span data-stu-id="ab70c-122">Before starting, review hello following details tooverify you meet hello prerequisites.</span></span>

### <a name="container-monitoring-solution-support-for-docker-orchestrator-and-os-platform"></a><span data-ttu-id="ab70c-123">Compatibilidad con solución de supervisión de contenedores para el orquestador y la plataforma de sistema operativo de Docker</span><span class="sxs-lookup"><span data-stu-id="ab70c-123">Container monitoring solution support for Docker Orchestrator and OS platform</span></span>
<span data-ttu-id="ab70c-124">Hello tabla siguiente se describe Hola orquestación de Docker y soporte técnico de inventario de contenedor, el rendimiento y los registros de análisis de registros de supervisión del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="ab70c-124">hello following table outlines hello Docker orchestration and operating system monitoring support of container inventory, performance, and logs with Log Analytics.</span></span>   

| | <span data-ttu-id="ab70c-125">ACS</span><span class="sxs-lookup"><span data-stu-id="ab70c-125">ACS</span></span> | <span data-ttu-id="ab70c-126">Linux</span><span class="sxs-lookup"><span data-stu-id="ab70c-126">Linux</span></span> | <span data-ttu-id="ab70c-127">Windows</span><span class="sxs-lookup"><span data-stu-id="ab70c-127">Windows</span></span> | <span data-ttu-id="ab70c-128">Contenedor</span><span class="sxs-lookup"><span data-stu-id="ab70c-128">Container</span></span><br><span data-ttu-id="ab70c-129">Inventario</span><span class="sxs-lookup"><span data-stu-id="ab70c-129">Inventory</span></span> | <span data-ttu-id="ab70c-130">Imagen</span><span class="sxs-lookup"><span data-stu-id="ab70c-130">Image</span></span><br><span data-ttu-id="ab70c-131">Inventario</span><span class="sxs-lookup"><span data-stu-id="ab70c-131">Inventory</span></span> | <span data-ttu-id="ab70c-132">Nodo</span><span class="sxs-lookup"><span data-stu-id="ab70c-132">Node</span></span><br><span data-ttu-id="ab70c-133">Inventario</span><span class="sxs-lookup"><span data-stu-id="ab70c-133">Inventory</span></span> | <span data-ttu-id="ab70c-134">Contenedor</span><span class="sxs-lookup"><span data-stu-id="ab70c-134">Container</span></span><br><span data-ttu-id="ab70c-135">Rendimiento</span><span class="sxs-lookup"><span data-stu-id="ab70c-135">Performance</span></span> | <span data-ttu-id="ab70c-136">Contenedor</span><span class="sxs-lookup"><span data-stu-id="ab70c-136">Container</span></span><br><span data-ttu-id="ab70c-137">Evento</span><span class="sxs-lookup"><span data-stu-id="ab70c-137">Event</span></span> | <span data-ttu-id="ab70c-138">Evento</span><span class="sxs-lookup"><span data-stu-id="ab70c-138">Event</span></span><br><span data-ttu-id="ab70c-139">Registro</span><span class="sxs-lookup"><span data-stu-id="ab70c-139">Log</span></span> | <span data-ttu-id="ab70c-140">Contenedor</span><span class="sxs-lookup"><span data-stu-id="ab70c-140">Container</span></span><br><span data-ttu-id="ab70c-141">Registro</span><span class="sxs-lookup"><span data-stu-id="ab70c-141">Log</span></span> |
|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|
| <span data-ttu-id="ab70c-142">kubernetes</span><span class="sxs-lookup"><span data-stu-id="ab70c-142">Kubernetes</span></span> | <span data-ttu-id="ab70c-143">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ab70c-143">&#8226;</span></span> | <span data-ttu-id="ab70c-144">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ab70c-144">&#8226;</span></span> | | <span data-ttu-id="ab70c-145">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ab70c-145">&#8226;</span></span> | <span data-ttu-id="ab70c-146">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ab70c-146">&#8226;</span></span> | <span data-ttu-id="ab70c-147">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ab70c-147">&#8226;</span></span> | <span data-ttu-id="ab70c-148">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ab70c-148">&#8226;</span></span> | <span data-ttu-id="ab70c-149">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ab70c-149">&#8226;</span></span> | <span data-ttu-id="ab70c-150">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ab70c-150">&#8226;</span></span> | <span data-ttu-id="ab70c-151">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ab70c-151">&#8226;</span></span> |
| <span data-ttu-id="ab70c-152">Mesosphere</span><span class="sxs-lookup"><span data-stu-id="ab70c-152">Mesosphere</span></span><br><span data-ttu-id="ab70c-153">DC/OS</span><span class="sxs-lookup"><span data-stu-id="ab70c-153">DC/OS</span></span> | <span data-ttu-id="ab70c-154">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ab70c-154">&#8226;</span></span> | <span data-ttu-id="ab70c-155">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ab70c-155">&#8226;</span></span> | | <span data-ttu-id="ab70c-156">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ab70c-156">&#8226;</span></span> | <span data-ttu-id="ab70c-157">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ab70c-157">&#8226;</span></span> | <span data-ttu-id="ab70c-158">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ab70c-158">&#8226;</span></span> | <span data-ttu-id="ab70c-159">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ab70c-159">&#8226;</span></span>| <span data-ttu-id="ab70c-160">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ab70c-160">&#8226;</span></span> | <span data-ttu-id="ab70c-161">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ab70c-161">&#8226;</span></span> | <span data-ttu-id="ab70c-162">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ab70c-162">&#8226;</span></span> |
| <span data-ttu-id="ab70c-163">Docker</span><span class="sxs-lookup"><span data-stu-id="ab70c-163">Docker</span></span><br><span data-ttu-id="ab70c-164">Swarm</span><span class="sxs-lookup"><span data-stu-id="ab70c-164">Swarm</span></span> | <span data-ttu-id="ab70c-165">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ab70c-165">&#8226;</span></span> | <span data-ttu-id="ab70c-166">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ab70c-166">&#8226;</span></span> | <span data-ttu-id="ab70c-167">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ab70c-167">&#8226;</span></span> | <span data-ttu-id="ab70c-168">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ab70c-168">&#8226;</span></span> | <span data-ttu-id="ab70c-169">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ab70c-169">&#8226;</span></span> | <span data-ttu-id="ab70c-170">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ab70c-170">&#8226;</span></span> | <span data-ttu-id="ab70c-171">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ab70c-171">&#8226;</span></span> | <span data-ttu-id="ab70c-172">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ab70c-172">&#8226;</span></span> | | <span data-ttu-id="ab70c-173">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ab70c-173">&#8226;</span></span> |
| <span data-ttu-id="ab70c-174">Servicio</span><span class="sxs-lookup"><span data-stu-id="ab70c-174">Service</span></span><br><span data-ttu-id="ab70c-175">Fabric</span><span class="sxs-lookup"><span data-stu-id="ab70c-175">Fabric</span></span> | | | <span data-ttu-id="ab70c-176">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ab70c-176">&#8226;</span></span> | <span data-ttu-id="ab70c-177">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ab70c-177">&#8226;</span></span> | <span data-ttu-id="ab70c-178">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ab70c-178">&#8226;</span></span> | <span data-ttu-id="ab70c-179">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ab70c-179">&#8226;</span></span> | <span data-ttu-id="ab70c-180">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ab70c-180">&#8226;</span></span> | <span data-ttu-id="ab70c-181">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ab70c-181">&#8226;</span></span> | <span data-ttu-id="ab70c-182">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ab70c-182">&#8226;</span></span> | <span data-ttu-id="ab70c-183">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ab70c-183">&#8226;</span></span> |
| <span data-ttu-id="ab70c-184">Red Hat Open</span><span class="sxs-lookup"><span data-stu-id="ab70c-184">Red Hat Open</span></span><br><span data-ttu-id="ab70c-185">Shift</span><span class="sxs-lookup"><span data-stu-id="ab70c-185">Shift</span></span> | | <span data-ttu-id="ab70c-186">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ab70c-186">&#8226;</span></span> | | <span data-ttu-id="ab70c-187">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ab70c-187">&#8226;</span></span> | <span data-ttu-id="ab70c-188">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ab70c-188">&#8226;</span></span>| <span data-ttu-id="ab70c-189">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ab70c-189">&#8226;</span></span> | <span data-ttu-id="ab70c-190">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ab70c-190">&#8226;</span></span> | <span data-ttu-id="ab70c-191">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ab70c-191">&#8226;</span></span> | | <span data-ttu-id="ab70c-192">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ab70c-192">&#8226;</span></span> |
| <span data-ttu-id="ab70c-193">Windows Server</span><span class="sxs-lookup"><span data-stu-id="ab70c-193">Windows Server</span></span><br><span data-ttu-id="ab70c-194">(independiente)</span><span class="sxs-lookup"><span data-stu-id="ab70c-194">(standalone)</span></span> | | | <span data-ttu-id="ab70c-195">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ab70c-195">&#8226;</span></span> | <span data-ttu-id="ab70c-196">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ab70c-196">&#8226;</span></span> | <span data-ttu-id="ab70c-197">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ab70c-197">&#8226;</span></span> | <span data-ttu-id="ab70c-198">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ab70c-198">&#8226;</span></span> | <span data-ttu-id="ab70c-199">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ab70c-199">&#8226;</span></span> | <span data-ttu-id="ab70c-200">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ab70c-200">&#8226;</span></span> | | <span data-ttu-id="ab70c-201">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ab70c-201">&#8226;</span></span> |
| <span data-ttu-id="ab70c-202">Linux Server</span><span class="sxs-lookup"><span data-stu-id="ab70c-202">Linux Server</span></span><br><span data-ttu-id="ab70c-203">(independiente)</span><span class="sxs-lookup"><span data-stu-id="ab70c-203">(standalone)</span></span> | | <span data-ttu-id="ab70c-204">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ab70c-204">&#8226;</span></span> | | <span data-ttu-id="ab70c-205">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ab70c-205">&#8226;</span></span> | <span data-ttu-id="ab70c-206">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ab70c-206">&#8226;</span></span> | <span data-ttu-id="ab70c-207">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ab70c-207">&#8226;</span></span> | <span data-ttu-id="ab70c-208">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ab70c-208">&#8226;</span></span> | <span data-ttu-id="ab70c-209">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ab70c-209">&#8226;</span></span> | | <span data-ttu-id="ab70c-210">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ab70c-210">&#8226;</span></span> |


### <a name="docker-versions-supported-on-linux"></a><span data-ttu-id="ab70c-211">Versiones de docker admitidas en Linux</span><span class="sxs-lookup"><span data-stu-id="ab70c-211">Docker versions supported on Linux</span></span>

- <span data-ttu-id="ab70c-212">Docker 1.11 too1.13</span><span class="sxs-lookup"><span data-stu-id="ab70c-212">Docker 1.11 too1.13</span></span>
- <span data-ttu-id="ab70c-213">Docker CE y EE v17.06</span><span class="sxs-lookup"><span data-stu-id="ab70c-213">Docker CE and EE v17.06</span></span>

### <a name="x64-linux-distributions-supported-as-container-hosts"></a><span data-ttu-id="ab70c-214">Las distribuciones x64 de Linux se admiten como hosts de contenedor</span><span class="sxs-lookup"><span data-stu-id="ab70c-214">x64 Linux distributions supported as container hosts</span></span>

- <span data-ttu-id="ab70c-215">Ubuntu 14.04 LTS y 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="ab70c-215">Ubuntu 14.04 LTS and 16.04 LTS</span></span>
- <span data-ttu-id="ab70c-216">CoreOS(stable)</span><span class="sxs-lookup"><span data-stu-id="ab70c-216">CoreOS(stable)</span></span>
- <span data-ttu-id="ab70c-217">Amazon Linux 2016.09.0</span><span class="sxs-lookup"><span data-stu-id="ab70c-217">Amazon Linux 2016.09.0</span></span>
- <span data-ttu-id="ab70c-218">openSUSE 13.2</span><span class="sxs-lookup"><span data-stu-id="ab70c-218">openSUSE 13.2</span></span>
- <span data-ttu-id="ab70c-219">openSUSE LEAP 42.2</span><span class="sxs-lookup"><span data-stu-id="ab70c-219">openSUSE LEAP 42.2</span></span>
- <span data-ttu-id="ab70c-220">CentOS 7.2 y 7.3</span><span class="sxs-lookup"><span data-stu-id="ab70c-220">CentOS 7.2 and 7.3</span></span>
- <span data-ttu-id="ab70c-221">SLES 12</span><span class="sxs-lookup"><span data-stu-id="ab70c-221">SLES 12</span></span>
- <span data-ttu-id="ab70c-222">RHEL 7.2 y 7.3</span><span class="sxs-lookup"><span data-stu-id="ab70c-222">RHEL 7.2 and 7.3</span></span>
- <span data-ttu-id="ab70c-223">Red Hat OpenShift Container Platform (OCP) 3.4 y 3.5</span><span class="sxs-lookup"><span data-stu-id="ab70c-223">Red Hat OpenShift Container Platform (OCP) 3.4 and 3.5</span></span>
- <span data-ttu-id="ab70c-224">ACS Mesosphere DC/OS 1.7.3 too1.8.8</span><span class="sxs-lookup"><span data-stu-id="ab70c-224">ACS Mesosphere DC/OS 1.7.3 too1.8.8</span></span>
- <span data-ttu-id="ab70c-225">ACS Kubernetes 1.4.5 too1.6</span><span class="sxs-lookup"><span data-stu-id="ab70c-225">ACS Kubernetes 1.4.5 too1.6</span></span>
- <span data-ttu-id="ab70c-226">ACS Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="ab70c-226">ACS Docker Swarm</span></span>

### <a name="supported-windows-operating-system"></a><span data-ttu-id="ab70c-227">Sistemas operativos Windows compatibles</span><span class="sxs-lookup"><span data-stu-id="ab70c-227">Supported Windows operating system</span></span>

- <span data-ttu-id="ab70c-228">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="ab70c-228">Windows Server 2016</span></span>
- <span data-ttu-id="ab70c-229">Windows 10 Anniversary Edition (Professional o Enterprise)</span><span class="sxs-lookup"><span data-stu-id="ab70c-229">Windows 10 Anniversary Edition (Professional or Enterprise)</span></span>

### <a name="docker-versions-supported-on-windows"></a><span data-ttu-id="ab70c-230">Versiones de docker admitidas en Windows</span><span class="sxs-lookup"><span data-stu-id="ab70c-230">Docker versions supported on Windows</span></span>

- <span data-ttu-id="ab70c-231">Docker de 1.12 y 1.13</span><span class="sxs-lookup"><span data-stu-id="ab70c-231">Docker 1.12 and 1.13</span></span>
- <span data-ttu-id="ab70c-232">Docker 17.03.0 y versiones posteriores</span><span class="sxs-lookup"><span data-stu-id="ab70c-232">Docker 17.03.0 and later</span></span>

## <a name="installing-and-configuring-hello-solution"></a><span data-ttu-id="ab70c-233">Instalar y configurar soluciones de Hola</span><span class="sxs-lookup"><span data-stu-id="ab70c-233">Installing and configuring hello solution</span></span>
<span data-ttu-id="ab70c-234">Usar hello después tooinstall de información y configurar soluciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="ab70c-234">Use hello following information tooinstall and configure hello solution.</span></span>

1. <span data-ttu-id="ab70c-235">Agregar Hola contenedor supervisión solución tooyour OMS área de trabajo de [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.ContainersOMS?tab=Overview) o mediante el proceso de hello descrito en [soluciones de análisis de registro agregar desde la Galería de soluciones de hello](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="ab70c-235">Add hello Container Monitoring solution tooyour OMS workspace from [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.ContainersOMS?tab=Overview) or by using hello process described in [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md).</span></span>

2. <span data-ttu-id="ab70c-236">Instalación y uso de Docker con un agente de OMS.</span><span class="sxs-lookup"><span data-stu-id="ab70c-236">Install and use Docker with an OMS agent.</span></span>  <span data-ttu-id="ab70c-237">En función de su sistema operativo, puede elegir entre Hola siguientes métodos:</span><span class="sxs-lookup"><span data-stu-id="ab70c-237">Based on your operating system, you can choose from hello following methods:</span></span>

  * <span data-ttu-id="ab70c-238">En sistemas operativos de Linux compatibles, instalar y ejecutar Docker y, a continuación, instalar y configurar hello [agente de OMS para Linux](log-analytics-agent-linux.md).</span><span class="sxs-lookup"><span data-stu-id="ab70c-238">On supported Linux operating systems, install and run Docker and then install and configure hello [OMS Agent for Linux](log-analytics-agent-linux.md).</span></span>  
  * <span data-ttu-id="ab70c-239">En CoreOS, no se puede ejecutar Hola agente de OMS para Linux.</span><span class="sxs-lookup"><span data-stu-id="ab70c-239">On CoreOS, you cannot run hello OMS Agent for Linux.</span></span> <span data-ttu-id="ab70c-240">En su lugar, ejecute una versión en contenedores de hello agente de OMS para Linux.</span><span class="sxs-lookup"><span data-stu-id="ab70c-240">Instead, you run a containerized version of hello OMS Agent for Linux.</span></span> <span data-ttu-id="ab70c-241">Repase las secciones [Hosts de contenedores de Linux incluido CoreOS](#for-all-linux-container-hosts-including-coreos) o [Hosts de contenedores de Azure Government Linux incluidos CoreOS](#for-all-azure-government-linux-container-hosts-including-coreos) si va a trabajar con contenedores en la nube de Azure Government.</span><span class="sxs-lookup"><span data-stu-id="ab70c-241">Review [Linux container hosts including CoreOS](#for-all-linux-container-hosts-including-coreos) or [Azure Government Linux container hosts including CoreOS](#for-all-azure-government-linux-container-hosts-including-coreos) if you are working with containers in Azure Government Cloud.</span></span>
  * <span data-ttu-id="ab70c-242">En Windows Server 2016 y Windows 10, instale Hola motor de Docker y el cliente, a continuación, una información de toogather de agente de conexión y envíelo tooLog análisis.</span><span class="sxs-lookup"><span data-stu-id="ab70c-242">On Windows Server 2016 and Windows 10, install hello Docker Engine and client then connect an agent toogather information and send it tooLog Analytics.</span></span>  

### <a name="container-services"></a><span data-ttu-id="ab70c-243">Servicios de contenedor</span><span class="sxs-lookup"><span data-stu-id="ab70c-243">Container services</span></span>

- <span data-ttu-id="ab70c-244">Si tiene un entorno de Red Hat OpenShift, consulte [Configuración de un agente de OMS para Red Hat OpenShift](#configure-an-oms-agent-for-red-hat-openshift).</span><span class="sxs-lookup"><span data-stu-id="ab70c-244">If you have a Red Hat OpenShift environment, review [Configure an OMS agent for Red Hat OpenShift](#configure-an-oms-agent-for-red-hat-openshift).</span></span>
- <span data-ttu-id="ab70c-245">Si tiene un clúster de Kubernetes con hello servicio de contenedor de Azure, consulte [supervisar un clúster de servicio de contenedor de Azure con Microsoft Operations Management Suite (OMS)](../container-service/kubernetes/container-service-kubernetes-oms.md).</span><span class="sxs-lookup"><span data-stu-id="ab70c-245">If you have a Kubernetes cluster using hello Azure Container Service, review [Monitor an Azure Container Service cluster with Microsoft Operations Management Suite (OMS)](../container-service/kubernetes/container-service-kubernetes-oms.md).</span></span>
- <span data-ttu-id="ab70c-246">Si tiene un clúster DC/OS de Azure Container Service, obtenga más información en [Monitor an Azure Container Service DC/OS cluster with Operations Management Suite](../container-service/dcos-swarm/container-service-monitoring-oms.md) (Uso de Operations Management Suite para supervisar un clúster DC/OS de Azure Container Service).</span><span class="sxs-lookup"><span data-stu-id="ab70c-246">If you have an Azure Container Service DC/OS cluster, learn more at [Monitor an Azure Container Service DC/OS cluster with Operations Management Suite](../container-service/dcos-swarm/container-service-monitoring-oms.md).</span></span>
- <span data-ttu-id="ab70c-247">Si tiene un entorno en modo Docker Swarm, obtenga más información en [Configuración de un agente de OMS para Docker Swarm](#configure-an-oms-agent-for-docker-swarm).</span><span class="sxs-lookup"><span data-stu-id="ab70c-247">If you have a Docker Swarm mode environment, learn more at [Configure an OMS agent for Docker Swarm](#configure-an-oms-agent-for-docker-swarm).</span></span>
- <span data-ttu-id="ab70c-248">Si usa contenedores con Service Fabric, obtenga más información en [Información general de Azure Service Fabric ](../service-fabric/service-fabric-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ab70c-248">If you use containers with Service Fabric, learn more at [Overview of Azure Service Fabric](../service-fabric/service-fabric-overview.md).</span></span>
- <span data-ttu-id="ab70c-249">Hola de revisión [Docker Engine en Windows](https://docs.microsoft.com/virtualization/windowscontainers/manage-docker/configure-docker-daemon) artículo para obtener información adicional acerca de cómo tooinstall y configurar los motores de Docker en equipos que ejecutan Windows.</span><span class="sxs-lookup"><span data-stu-id="ab70c-249">Review hello [Docker Engine on Windows](https://docs.microsoft.com/virtualization/windowscontainers/manage-docker/configure-docker-daemon) article for additional information about how tooinstall and configure your Docker Engines on computers running Windows.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ab70c-250">Debe ejecutar docker **antes de** instalar hello [agente de OMS para Linux](log-analytics-agent-linux.md) en los hosts de contenedor.</span><span class="sxs-lookup"><span data-stu-id="ab70c-250">Docker must be running **before** you install hello [OMS Agent for Linux](log-analytics-agent-linux.md) on your container hosts.</span></span> <span data-ttu-id="ab70c-251">Si ya ha instalado el agente de hello antes de instalar Docker, necesitará tooreinstall Hola agente de OMS para Linux.</span><span class="sxs-lookup"><span data-stu-id="ab70c-251">If you've already installed hello agent before installing Docker, you need tooreinstall hello OMS Agent for Linux.</span></span> <span data-ttu-id="ab70c-252">Para obtener más información sobre Docker, consulte hello [sitio Web de Docker](https://www.docker.com).</span><span class="sxs-lookup"><span data-stu-id="ab70c-252">For more information about Docker, see hello [Docker website](https://www.docker.com).</span></span>


## <a name="linux-container-hosts"></a><span data-ttu-id="ab70c-253">Hosts de contenedores de Linux</span><span class="sxs-lookup"><span data-stu-id="ab70c-253">Linux container hosts</span></span>

<span data-ttu-id="ab70c-254">Después de instalar a Docker, use Hola después de configuración para el agente de Hola de tooconfigure de host de contenedor para su uso con Docker.</span><span class="sxs-lookup"><span data-stu-id="ab70c-254">After you've installed Docker, use hello following settings for your container host tooconfigure hello agent for use with Docker.</span></span> <span data-ttu-id="ab70c-255">En primer lugar debe clave, que encontrará en el portal de Azure de Hola y el identificador de área de trabajo OMS.</span><span class="sxs-lookup"><span data-stu-id="ab70c-255">First you need your OMS workspace ID and key, which you can find in hello Azure portal.</span></span> <span data-ttu-id="ab70c-256">En el área de trabajo, haga clic en **inicio rápido** > **equipos** tooview su **Id. de área de trabajo** y **Primary Key**.</span><span class="sxs-lookup"><span data-stu-id="ab70c-256">In your workspace, click **Quick Start** > **Computers** tooview your **Workspace ID** and **Primary Key**.</span></span>  <span data-ttu-id="ab70c-257">Copie y pegue ambos valores en el editor que prefiera.</span><span class="sxs-lookup"><span data-stu-id="ab70c-257">Copy and paste both into your favorite editor.</span></span>

### <a name="for-all-linux-container-hosts-except-coreos"></a><span data-ttu-id="ab70c-258">Para todos los hosts de contenedores de Linux excepto CoreOS</span><span class="sxs-lookup"><span data-stu-id="ab70c-258">For all Linux container hosts except CoreOS</span></span>

- <span data-ttu-id="ab70c-259">Para obtener más información y pasos acerca de cómo tooinstall Hola agente de OMS para Linux, consulte [conectar su tooOperations de equipos Linux Management Suite (OMS)](log-analytics-agent-linux.md).</span><span class="sxs-lookup"><span data-stu-id="ab70c-259">For more information and steps on how tooinstall hello OMS Agent for Linux, see [Connect your Linux Computers tooOperations Management Suite (OMS)](log-analytics-agent-linux.md).</span></span>

### <a name="for-all-linux-container-hosts-including-coreos"></a><span data-ttu-id="ab70c-260">Para todos los hosts de contenedores de Linux incluido CoreOS</span><span class="sxs-lookup"><span data-stu-id="ab70c-260">For all Linux container hosts including CoreOS</span></span>

<span data-ttu-id="ab70c-261">Inicie el contenedor OMS de Hola que desea toomonitor.</span><span class="sxs-lookup"><span data-stu-id="ab70c-261">Start hello OMS container that you want toomonitor.</span></span> <span data-ttu-id="ab70c-262">Modifique y use el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="ab70c-262">Modify and use hello following example:</span></span>

```
sudo docker run --privileged -d -v /var/run/docker.sock:/var/run/docker.sock -e WSID="your workspace id" -e KEY="your key" -h=`hostname` -p 127.0.0.1:25225:25225 --name="omsagent" --restart=always microsoft/oms
```

### <a name="for-all-azure-government-linux-container-hosts-including-coreos"></a><span data-ttu-id="ab70c-263">Para todos los hosts de contenedores de Linux para Azure Government, incluido CoreOS</span><span class="sxs-lookup"><span data-stu-id="ab70c-263">For all Azure Government Linux container hosts including CoreOS</span></span>

<span data-ttu-id="ab70c-264">Inicie el contenedor OMS de Hola que desea toomonitor.</span><span class="sxs-lookup"><span data-stu-id="ab70c-264">Start hello OMS container that you want toomonitor.</span></span> <span data-ttu-id="ab70c-265">Modifique y use el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="ab70c-265">Modify and use hello following example:</span></span>

```
sudo docker run --privileged -d -v /var/run/docker.sock:/var/run/docker.sock -v /var/log:/var/log -e WSID="your workspace id" -e KEY="your key" -e DOMAIN="opinsights.azure.us" -p 127.0.0.1:25225:25225 -p 127.0.0.1:25224:25224/udp --name="omsagent" -h=`hostname` --restart=always microsoft/oms
```

### <a name="switching-from-using-an-installed-linux-agent-tooone-in-a-container"></a><span data-ttu-id="ab70c-266">Cambio del uso de un tooone de agente de Linux instalado en un contenedor</span><span class="sxs-lookup"><span data-stu-id="ab70c-266">Switching from using an installed Linux agent tooone in a container</span></span>
<span data-ttu-id="ab70c-267">Si anteriormente utilizaba agente instalado directamente de Hola y desea usar tooinstead un agente en el que se ejecuta en un contenedor, primero debe quitar Hola agente de OMS para Linux.</span><span class="sxs-lookup"><span data-stu-id="ab70c-267">If you previously used hello directly-installed agent and want tooinstead use an agent running in a container, you must first remove hello OMS Agent for Linux.</span></span> <span data-ttu-id="ab70c-268">Vea [Hola Desinstalar agente de OMS para Linux](log-analytics-agent-linux.md#uninstalling-the-oms-agent-for-linux) toounderstand cómo desinstalar toosuccessfully Hola agente.</span><span class="sxs-lookup"><span data-stu-id="ab70c-268">See [Uninstalling hello OMS Agent for Linux](log-analytics-agent-linux.md#uninstalling-the-oms-agent-for-linux) toounderstand how toosuccessfully uninstall hello agent.</span></span>  

### <a name="configure-an-oms-agent-for-docker-swarm"></a><span data-ttu-id="ab70c-269">Configuración de un agente de OMS para Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="ab70c-269">Configure an OMS agent for Docker Swarm</span></span>

<span data-ttu-id="ab70c-270">Puede ejecutar Hola agente de OMS como un servicio global en Docker Swarm.</span><span class="sxs-lookup"><span data-stu-id="ab70c-270">You can run hello OMS Agent as a global service on Docker Swarm.</span></span> <span data-ttu-id="ab70c-271">Usar hello después información toocreate un servicio de agente de OMS.</span><span class="sxs-lookup"><span data-stu-id="ab70c-271">Use hello following information toocreate an OMS Agent service.</span></span> <span data-ttu-id="ab70c-272">Deberá tooinsert el Id. de área de trabajo de OMS y la clave principal.</span><span class="sxs-lookup"><span data-stu-id="ab70c-272">You need tooinsert your OMS Workspace ID and Primary Key.</span></span>

- <span data-ttu-id="ab70c-273">Ejecute hello siguiente en el nodo principal de Hola.</span><span class="sxs-lookup"><span data-stu-id="ab70c-273">Run hello following on hello master node.</span></span>

    ```
    sudo docker service create  --name omsagent --mode global  --mount type=bind,source=/var/run/docker.sock,destination=/var/run/docker.sock  -e WSID="<WORKSPACE ID>" -e KEY="<PRIMARY KEY>" -p 25225:25225 -p 25224:25224/udp  --restart-condition=on-failure microsoft/oms
    ```

### <a name="configure-an-oms-agent-for-red-hat-openshift"></a><span data-ttu-id="ab70c-274">Configuración de un agente de OMS para Red Hat OpenShift</span><span class="sxs-lookup"><span data-stu-id="ab70c-274">Configure an OMS Agent for Red Hat OpenShift</span></span>
<span data-ttu-id="ab70c-275">Hay tres maneras tooadd Hola agente de OMS tooRed Hat OpenShift toostart recopilación contenedor datos de supervisión.</span><span class="sxs-lookup"><span data-stu-id="ab70c-275">There are three ways tooadd hello OMS Agent tooRed Hat OpenShift toostart collecting container monitoring data.</span></span>

* <span data-ttu-id="ab70c-276">[Instale Hola agente de OMS para Linux](log-analytics-agent-linux.md) directamente en cada nodo OpenShift</span><span class="sxs-lookup"><span data-stu-id="ab70c-276">[Install hello OMS Agent for Linux](log-analytics-agent-linux.md) directly on each OpenShift node</span></span>  
* <span data-ttu-id="ab70c-277">[Habilitar la extensión de máquina virtual de Log Analytics](log-analytics-azure-vm-extension.md) en cada nodo de OpenShift que reside en Azure</span><span class="sxs-lookup"><span data-stu-id="ab70c-277">[Enable Log Analytics VM Extension](log-analytics-azure-vm-extension.md) on each OpenShift node residing in Azure</span></span>  
* <span data-ttu-id="ab70c-278">Instalar agente de OMS Hola como un conjunto de demonio OpenShift</span><span class="sxs-lookup"><span data-stu-id="ab70c-278">Install hello OMS Agent as a OpenShift daemon-set</span></span>  

<span data-ttu-id="ab70c-279">En esta sección trataremos Hola pasos necesarios tooinstall Hola agente de OMS como un conjunto de demonio OpenShift.</span><span class="sxs-lookup"><span data-stu-id="ab70c-279">In this section we cover hello steps required tooinstall hello OMS Agent as an OpenShift daemon-set.</span></span>  

1. <span data-ttu-id="ab70c-280">Inicio de sesión toohello OpenShift nodo y copiar hello yaml archivo maestro [omsagent.yaml ocp](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-omsagent.yaml) desde GitHub tooyour maestro de nodo y modificar valor de Hola por su identificador de área de trabajo de OMS y con la clave principal.</span><span class="sxs-lookup"><span data-stu-id="ab70c-280">Sign on toohello OpenShift master node and copy hello yaml file [ocp-omsagent.yaml](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-omsagent.yaml) from GitHub tooyour master node and modify hello value with your OMS Workspace ID and with your Primary Key.</span></span>
2. <span data-ttu-id="ab70c-281">Ejecutar un proyecto de hello después toocreate de comandos para OMS y establecer la cuenta de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="ab70c-281">Run hello following commands toocreate a project for OMS and set hello user account.</span></span>

    ```
    oadm new-project omslogging --node-selector='zone=default'
    oc project omslogging  
    oc create serviceaccount omsagent  
    oadm policy add-cluster-role-to-user cluster-reader   system:serviceaccount:omslogging:omsagent  
    oadm policy add-scc-to-user privileged system:serviceaccount:omslogging:omsagent  
    ```

4. <span data-ttu-id="ab70c-282">Hola toodeploy conjunto de demonio, ejecute la siguiente de hello:</span><span class="sxs-lookup"><span data-stu-id="ab70c-282">toodeploy hello daemon-set, run hello following:</span></span>

    `oc create -f ocp-omsagent.yaml`

5. <span data-ttu-id="ab70c-283">tooverify está configurado y funciona correctamente, escriba Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="ab70c-283">tooverify it is configured and working correctly, type hello following:</span></span>

    `oc describe daemonset omsagent`  

    <span data-ttu-id="ab70c-284">y debe ser similar la salida de hello:</span><span class="sxs-lookup"><span data-stu-id="ab70c-284">and hello output should resemble:</span></span>

    ```
    [ocpadmin@khm-0 ~]$ oc describe ds oms  
    Name:           oms  
    Image(s):       microsoft/oms  
    Selector:       name=omsagent  
    Node-Selector:  zone=default  
    Labels:         agentVersion=1.4.0-12  
                    dockerProviderVersion=10.0.0-25  
                    name=omsagent  
    Desired Number of Nodes Scheduled: 3  
    Current Number of Nodes Scheduled: 3  
    Number of Nodes Misscheduled: 0  
    Pods Status:    3 Running / 0 Waiting / 0 Succeeded / 0 Failed  
    No events.  
    ```

<span data-ttu-id="ab70c-285">Si desea toouse secretos toosecure el Id. de área de trabajo de OMS y la clave principal al utilizar Hola agente de OMS demonio conjunto yaml archivo, realizar Hola pasos.</span><span class="sxs-lookup"><span data-stu-id="ab70c-285">If you want toouse secrets toosecure your OMS Workspace ID and Primary Key when using hello OMS Agent daemon-set yaml file, perform hello following steps.</span></span>

1. <span data-ttu-id="ab70c-286">Inicio de sesión toohello OpenShift nodo y copiar hello yaml archivo maestro [ocp-ds-omsagent.yaml](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-ds-omsagent.yaml) y el secreto de generar script [secretgen.sh ocp](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-secretgen.sh) desde GitHub.</span><span class="sxs-lookup"><span data-stu-id="ab70c-286">Sign on toohello OpenShift master node and copy hello yaml file [ocp-ds-omsagent.yaml](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-ds-omsagent.yaml) and secret generating script [ocp-secretgen.sh](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-secretgen.sh) from GitHub.</span></span>  <span data-ttu-id="ab70c-287">Esta secuencia de comandos generará el archivo de yaml de secretos de hello para el Id. de área de trabajo de OMS y la clave principal toosecure su secrete información.</span><span class="sxs-lookup"><span data-stu-id="ab70c-287">This script will generate hello secrets yaml file for OMS Workspace ID and Primary Key toosecure your secrete information.</span></span>  
2. <span data-ttu-id="ab70c-288">Ejecutar un proyecto de hello después toocreate de comandos para OMS y establecer la cuenta de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="ab70c-288">Run hello following commands toocreate a project for OMS and set hello user account.</span></span> <span data-ttu-id="ab70c-289">Generar script de secreto de Hola solicita el identificador de área de trabajo de OMS <WSID> y la clave principal <KEY> y tras la finalización, se crea el archivo de ocp secret.yaml de Hola.</span><span class="sxs-lookup"><span data-stu-id="ab70c-289">hello secret generating script asks for your OMS Workspace ID <WSID> and Primary Key <KEY> and upon completion, it creates hello ocp-secret.yaml file.</span></span>  

    ```
    oadm new-project omslogging --node-selector='zone=default'  
    oc project omslogging  
    oc create serviceaccount omsagent  
    oadm policy add-cluster-role-to-user cluster-reader   system:serviceaccount:omslogging:omsagent  
    oadm policy add-scc-to-user privileged system:serviceaccount:omslogging:omsagent  
    ```

4. <span data-ttu-id="ab70c-290">Implementar el archivo de secreto de hello ejecutando Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="ab70c-290">Deploy hello secret file by running hello following:</span></span>

    `oc create -f ocp-secret.yaml`

5. <span data-ttu-id="ab70c-291">Comprobar la implementación mediante la ejecución Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="ab70c-291">Verify deployment by running hello following:</span></span>

    `oc describe secret omsagent-secret`  

    <span data-ttu-id="ab70c-292">y debe ser similar la salida de hello:</span><span class="sxs-lookup"><span data-stu-id="ab70c-292">and hello  output should resemble:</span></span>  

    ```
    [ocpadmin@khocp-master-0 ~]$ oc describe ds oms  
    Name:           oms  
    Image(s):       microsoft/oms  
    Selector:       name=omsagent  
    Node-Selector:  zone=default  
    Labels:         agentVersion=1.4.0-12  
                    dockerProviderVersion=10.0.0-25  
                    name=omsagent  
    Desired Number of Nodes Scheduled: 3  
    Current Number of Nodes Scheduled: 3  
    Number of Nodes Misscheduled: 0  
    Pods Status:    3 Running / 0 Waiting / 0 Succeeded / 0 Failed  
    No events.  
    ```

6. <span data-ttu-id="ab70c-293">Implementar archivo de conjunto de demonio yaml de agente de OMS hello ejecutando Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="ab70c-293">Deploy hello OMS Agent daemon-set yaml file by running hello following:</span></span>

    `oc create -f ocp-ds-omsagent.yaml`  

7. <span data-ttu-id="ab70c-294">Comprobar la implementación mediante la ejecución Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="ab70c-294">Verify deployment by running hello following:</span></span>

    `oc describe ds oms`

    <span data-ttu-id="ab70c-295">y debe ser similar la salida de hello:</span><span class="sxs-lookup"><span data-stu-id="ab70c-295">and hello output should resemble:</span></span>

    ```
    [ocpadmin@khocp-master-0 ~]$ oc describe secret omsagent-secret  
    Name:           omsagent-secret  
    Namespace:      omslogging  
    Labels:         <none>  
    Annotations:    <none>  

    Type:   Opaque  

     Data  
     ====  
     KEY:    89 bytes  
     WSID:   37 bytes  
    ```

### <a name="secure-your-secret-information-for-docker-swarm-and-kubernetes"></a><span data-ttu-id="ab70c-296">Protección de la información secreta para Docker Swarm y Kubernetes</span><span class="sxs-lookup"><span data-stu-id="ab70c-296">Secure your secret information for Docker Swarm and Kubernetes</span></span>

<span data-ttu-id="ab70c-297">Puede proteger el identificador de área de trabajo y las claves principales de OMS para los servicios de contenedor de Docker Swarm y Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="ab70c-297">You can secure your secret OMS Workspace ID and Primary Keys for Docker Swarm and Kubernetes container services.</span></span>

#### <a name="secure-secrets-for-docker-swarm"></a><span data-ttu-id="ab70c-298">Protección de secretos de Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="ab70c-298">Secure secrets for Docker Swarm</span></span>

<span data-ttu-id="ab70c-299">Para Docker Swarm, una vez creado el secreto de hello para el Id. de área de trabajo y la clave principal, puede ejecutar Hola crear servicio de Docker de Hola para OMSagent.</span><span class="sxs-lookup"><span data-stu-id="ab70c-299">For Docker Swarm, once hello secret for Workspace ID and Primary Key is created, you can run hello create hello Docker service for OMSagent.</span></span> <span data-ttu-id="ab70c-300">Usar hello después información toocreate la información secreta.</span><span class="sxs-lookup"><span data-stu-id="ab70c-300">Use hello following information toocreate your secret information.</span></span>

1. <span data-ttu-id="ab70c-301">Ejecute hello siguiente en el nodo principal de Hola.</span><span class="sxs-lookup"><span data-stu-id="ab70c-301">Run hello following on hello master node.</span></span>

    ```
    echo "WSID" | docker secret create WSID -
    echo "KEY" | docker secret create KEY -
    ```

2. <span data-ttu-id="ab70c-302">Compruebe que los secretos se crearon correctamente.</span><span class="sxs-lookup"><span data-stu-id="ab70c-302">Verify that secrets were created properly.</span></span>

    ```
    keiko@swarmm-master-13957614-0:/run# sudo docker secret ls
    ```

    ```
    ID                          NAME                CREATED             UPDATED
    j2fj153zxy91j8zbcitnjxjiv   WSID                43 minutes ago      43 minutes ago
    l9rh3n987g9c45zffuxdxetd9   KEY                 38 minutes ago      38 minutes ago
    ```

3. <span data-ttu-id="ab70c-303">Hola ejecución después de comando toomount Hola secretos toohello en contenedores a agente de OMS.</span><span class="sxs-lookup"><span data-stu-id="ab70c-303">Run hello following command toomount hello secrets toohello containerized OMS Agent.</span></span>

    ```
    sudo docker service create  --name omsagent --mode global  --mount type=bind,source=/var/run/docker.sock,destination=/var/run/docker.sock --secret source=WSID,target=WSID --secret source=KEY,target=KEY  -p 25225:25225 -p 25224:25224/udp --restart-condition=on-failure microsoft/oms
    ```

#### <a name="secure-secrets-for-kubernetes-with-yaml-files"></a><span data-ttu-id="ab70c-304">Protección de secretos de Kubernetes con archivos yaml</span><span class="sxs-lookup"><span data-stu-id="ab70c-304">Secure secrets for Kubernetes with yaml files</span></span>

<span data-ttu-id="ab70c-305">Para Kubernetes, se usa un archivo de script toogenerate Hola secretos yaml para el Id. de área de trabajo y la clave principal.</span><span class="sxs-lookup"><span data-stu-id="ab70c-305">For Kubernetes, you use a script toogenerate hello secrets yaml file for your Workspace ID and Primary Key.</span></span> <span data-ttu-id="ab70c-306">En hello [OMS Docker Kubernetes GitHub](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes) página, hay archivos que se pueden utilizar con o sin la información secreta.</span><span class="sxs-lookup"><span data-stu-id="ab70c-306">At hello [OMS Docker Kubernetes GitHub](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes) page, there are files that you can use with or without your secret information.</span></span>

- <span data-ttu-id="ab70c-307">Hola DaemonSet de agente OMS predeterminado no tiene información secreta (omsagent.yaml)</span><span class="sxs-lookup"><span data-stu-id="ab70c-307">hello Default OMS Agent DaemonSet does not have secret information (omsagent.yaml)</span></span>
- <span data-ttu-id="ab70c-308">archivo yaml de Hello DaemonSet de agente de OMS utiliza información secreta (omsagent-ds-secrets.yaml) con el archivo de generación secreto scripts toogenerate Hola secretos yaml (omsagentsecret.yaml).</span><span class="sxs-lookup"><span data-stu-id="ab70c-308">hello OMS Agent DaemonSet yaml file uses secret information (omsagent-ds-secrets.yaml) with secret generation scripts toogenerate hello secrets yaml (omsagentsecret.yaml) file.</span></span>

<span data-ttu-id="ab70c-309">Puede elegir toocreate omsagent DaemonSets con o sin secretos.</span><span class="sxs-lookup"><span data-stu-id="ab70c-309">You can choose toocreate omsagent DaemonSets with or without secrets.</span></span>

##### <a name="default-omsagent-daemonset-yaml-file-without-secrets"></a><span data-ttu-id="ab70c-310">Archivo yaml de DaemonSet de OMSagent predeterminado sin secretos</span><span class="sxs-lookup"><span data-stu-id="ab70c-310">Default OMSagent DaemonSet yaml file without secrets</span></span>

- <span data-ttu-id="ab70c-311">Archivo yaml de hello predeterminado DaemonSet de agente de OMS, reemplace hello `<WSID>` y `<KEY>` tooyour WSID y la clave.</span><span class="sxs-lookup"><span data-stu-id="ab70c-311">For hello default OMS Agent DaemonSet yaml file, replace hello `<WSID>` and `<KEY>` tooyour WSID and KEY.</span></span> <span data-ttu-id="ab70c-312">Copie nodo maestro de hello archivo tooyour y siguiente ejecución hello:</span><span class="sxs-lookup"><span data-stu-id="ab70c-312">Copy hello file tooyour master node and run hello following:</span></span>

    ```
    sudo kubectl create -f omsagent.yaml
    ```

##### <a name="default-omsagent-daemonset-yaml-file-with-secrets"></a><span data-ttu-id="ab70c-313">Archivo yaml de DaemonSet de OMSagent predeterminado con secretos</span><span class="sxs-lookup"><span data-stu-id="ab70c-313">Default OMSagent DaemonSet yaml file with secrets</span></span>

1. <span data-ttu-id="ab70c-314">toouse DaemonSet de agente de OMS con información secreta, cree primero los secretos de Hola.</span><span class="sxs-lookup"><span data-stu-id="ab70c-314">toouse OMS Agent DaemonSet using secret information, create hello secrets first.</span></span>
    1. <span data-ttu-id="ab70c-315">Copiar script de Hola y el archivo de plantilla secreto y asegúrese de que se encuentren en hello mismo directorio.</span><span class="sxs-lookup"><span data-stu-id="ab70c-315">Copy hello script and secret template file and make sure they are on hello same directory.</span></span>
        - <span data-ttu-id="ab70c-316">Script de generación de secretos: secret-gen.sh</span><span class="sxs-lookup"><span data-stu-id="ab70c-316">Secret generating script - secret-gen.sh</span></span>
        - <span data-ttu-id="ab70c-317">Plantilla de secretos: secret-template.yaml</span><span class="sxs-lookup"><span data-stu-id="ab70c-317">secret template - secret-template.yaml</span></span>
    2. <span data-ttu-id="ab70c-318">Ejecutar script de Hola, como el siguiente ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="ab70c-318">Run hello script, like hello following example.</span></span> <span data-ttu-id="ab70c-319">script de Hola solicita Hola Id. de área de trabajo de OMS y la clave principal y después escribirlos, script de Hola crea un archivo de yaml secreto para que pueda ejecutar.</span><span class="sxs-lookup"><span data-stu-id="ab70c-319">hello script asks for hello OMS Workspace ID and Primary Key and after you enter them, hello script creates a secret yaml file so you can run it.</span></span>   

        ```
        #> sudo bash ./secret-gen.sh
        ```

    3. <span data-ttu-id="ab70c-320">Crear pod de secretos de hello ejecutando Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="ab70c-320">Create hello secrets pod by running hello following:</span></span>
        ```
        sudo kubectl create -f omsagentsecret.yaml
        ```

    4. <span data-ttu-id="ab70c-321">tooverify, ejecute hello siguiente:</span><span class="sxs-lookup"><span data-stu-id="ab70c-321">tooverify, run hello following:</span></span>

        ```
        keiko@ubuntu16-13db:~# sudo kubectl get secrets
        ```

        <span data-ttu-id="ab70c-322">La salida debe ser similar a lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="ab70c-322">Output should resemble:</span></span>

        ```
        NAME                  TYPE                                  DATA      AGE
        default-token-gvl91   kubernetes.io/service-account-token   3         50d
        omsagent-secret       Opaque                                2         1d
        ```

        ```
        keiko@ubuntu16-13db:~# sudo kubectl describe secrets omsagent-secret
        ```

        <span data-ttu-id="ab70c-323">La salida debe ser similar a lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="ab70c-323">Output should resemble:</span></span>

        ```
        Name:           omsagent-secret
        Namespace:      default
        Labels:         <none>
        Annotations:    <none>

        Type:   Opaque

        Data
        ====
        WSID:   36 bytes
        KEY:    88 bytes
        ```

    5. <span data-ttu-id="ab70c-324">Ejecute ``` sudo kubectl create -f omsagent-ds-secrets.yaml ``` para crear el daemon-set de omsagent</span><span class="sxs-lookup"><span data-stu-id="ab70c-324">Create your omsagent daemon-set by running ``` sudo kubectl create -f omsagent-ds-secrets.yaml ```</span></span>

2. <span data-ttu-id="ab70c-325">Compruebe que hello que daemonset de agente de OMS se está ejecutando, toohello similar después de:</span><span class="sxs-lookup"><span data-stu-id="ab70c-325">Verify that hello OMS Agent DaemonSet is running, similar toohello following:</span></span>

    ```
    keiko@ubuntu16-13db:~# sudo kubectl get ds omsagent
    ```

    ```
    NAME       DESIRED   CURRENT   NODE-SELECTOR   AGE
    omsagent   3         3         <none>          1h
    ```


<span data-ttu-id="ab70c-326">Para Kubernetes, usar un archivo de yaml de secretos de secuencia de comandos toogenerate hello para el Id. de área de trabajo y la clave principal.</span><span class="sxs-lookup"><span data-stu-id="ab70c-326">For Kubernetes, use a script toogenerate hello secrets yaml file for Workspace ID and Primary Key.</span></span> <span data-ttu-id="ab70c-327">Hola de uso después de la información de ejemplo con hello [omsagent yaml archivo](https://github.com/Microsoft/OMS-docker/blob/master/Kubernetes/omsagent.yaml) toosecure la información secreta.</span><span class="sxs-lookup"><span data-stu-id="ab70c-327">Use hello following example information with hello [omsagent yaml file](https://github.com/Microsoft/OMS-docker/blob/master/Kubernetes/omsagent.yaml) toosecure your secret information.</span></span>

```
keiko@ubuntu16-13db:~# sudo kubectl describe secrets omsagent-secret
Name:           omsagent-secret
Namespace:      default
Labels:         <none>
Annotations:    <none>

Type:   Opaque

Data
====
WSID:   36 bytes
KEY:    88 bytes
```

## <a name="windows-container-hosts"></a><span data-ttu-id="ab70c-328">Hosts de contenedores Windows</span><span class="sxs-lookup"><span data-stu-id="ab70c-328">Windows container hosts</span></span>

### <a name="preparation-before-installing-windows-agents"></a><span data-ttu-id="ab70c-329">Preparación antes de instalar agentes de Windows</span><span class="sxs-lookup"><span data-stu-id="ab70c-329">Preparation before installing Windows agents</span></span>

<span data-ttu-id="ab70c-330">Antes de instalar a agentes en equipos que ejecutan Windows, necesita servicio de Docker de tooconfigure Hola.</span><span class="sxs-lookup"><span data-stu-id="ab70c-330">Before you install agents on computers running Windows, you need tooconfigure hello Docker service.</span></span> <span data-ttu-id="ab70c-331">configuración de Hello permite Hola Windows hello o agente de análisis de registros máquina virtual extensión toouse Hola socket de TCP de Docker para que los agentes de hello pueden acceder remotamente demonio de Docker de Hola y toocapture datos para la supervisión.</span><span class="sxs-lookup"><span data-stu-id="ab70c-331">hello configuration allows hello Windows agent or hello Log Analytics virtual machine extension toouse hello Docker TCP socket so that hello agents can access hello Docker daemon remotely and toocapture data for monitoring.</span></span>

#### <a name="toostart-docker-and-verify-its-configuration"></a><span data-ttu-id="ab70c-332">toostart Docker y compruebe su configuración</span><span class="sxs-lookup"><span data-stu-id="ab70c-332">toostart Docker and verify its configuration</span></span>

<span data-ttu-id="ab70c-333">Hay pasos necesarios tooset seguridad TCP, canalización con nombre para Windows Server:</span><span class="sxs-lookup"><span data-stu-id="ab70c-333">There are steps needed tooset up TCP named pipe for Windows Server:</span></span>

1. <span data-ttu-id="ab70c-334">En Windows PowerShell, habilite la canalización TCP y la canalización con nombre.</span><span class="sxs-lookup"><span data-stu-id="ab70c-334">In Windows PowerShell, enable TCP pipe and named pipe.</span></span>

    ```
    Stop-Service docker
    dockerd --unregister-service
    dockerd --register-service -H npipe:// -H 0.0.0.0:2375  
    Start-Service docker
    ```

2. <span data-ttu-id="ab70c-335">Configuración de Docker con el archivo de configuración de hello de canalización TCP y la canalización con nombre.</span><span class="sxs-lookup"><span data-stu-id="ab70c-335">Configure Docker with hello configuration file for TCP pipe and named pipe.</span></span> <span data-ttu-id="ab70c-336">archivo de configuración de Hola se encuentra en C:\ProgramData\docker\config\daemon.json.</span><span class="sxs-lookup"><span data-stu-id="ab70c-336">hello configuration file is located at C:\ProgramData\docker\config\daemon.json.</span></span>

    <span data-ttu-id="ab70c-337">En el archivo de daemon.json hello, necesitará siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="ab70c-337">In hello daemon.json file, you will need hello following:</span></span>

    ```
    {
    "hosts": ["tcp://0.0.0.0:2375", "npipe://"]
    }
    ```

<span data-ttu-id="ab70c-338">Para obtener más información acerca de la configuración del demonio de Docker de hello usado con contenedores de Windows, vea [Docker Engine en Windows](https://docs.microsoft.com/virtualization/windowscontainers/manage-docker/configure-docker-daemon).</span><span class="sxs-lookup"><span data-stu-id="ab70c-338">For more information about hello Docker daemon configuration used with Windows Containers, see [Docker Engine on Windows](https://docs.microsoft.com/virtualization/windowscontainers/manage-docker/configure-docker-daemon).</span></span>


### <a name="install-windows-agents"></a><span data-ttu-id="ab70c-339">Instalación de agentes de Windows</span><span class="sxs-lookup"><span data-stu-id="ab70c-339">Install Windows agents</span></span>

<span data-ttu-id="ab70c-340">tooenable Windows y supervisión, el contenedor de Hyper-V instala Hola Microsoft Monitoring Agent (MMA) en equipos de Windows que son hosts de contenedor.</span><span class="sxs-lookup"><span data-stu-id="ab70c-340">tooenable Windows and Hyper-V container monitoring, install hello Microsoft Monitoring Agent (MMA) on Windows computers that are container hosts.</span></span> <span data-ttu-id="ab70c-341">Para equipos que ejecutan Windows en su entorno local, vea [tooLog de equipos de Windows conectarse análisis](log-analytics-windows-agents.md).</span><span class="sxs-lookup"><span data-stu-id="ab70c-341">For computers running Windows in your on-premises environment, see [Connect Windows computers tooLog Analytics](log-analytics-windows-agents.md).</span></span> <span data-ttu-id="ab70c-342">Para las máquinas virtuales ejecutan en Azure, conéctelos tooLog análisis con hello [extensión de máquina virtual](log-analytics-azure-vm-extension.md).</span><span class="sxs-lookup"><span data-stu-id="ab70c-342">For virtual machines running in Azure, connect them tooLog Analytics using hello [virtual machine extension](log-analytics-azure-vm-extension.md).</span></span>

<span data-ttu-id="ab70c-343">Puede supervisar los contenedores de Windows que se ejecutan en Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="ab70c-343">You can monitor Windows containers running on Service Fabric.</span></span> <span data-ttu-id="ab70c-344">Sin embargo, actualmente solo las [máquinas virtuales que se ejecutan en Azure](log-analytics-azure-vm-extension.md) y en [equipos Windows de su entorno local](log-analytics-windows-agents.md) son compatibles con Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="ab70c-344">However, only [virtual machines running in Azure](log-analytics-azure-vm-extension.md) and [computers running Windows in your on-premises environment](log-analytics-windows-agents.md) are currently supported for Service Fabric.</span></span>

<span data-ttu-id="ab70c-345">Puede comprobar que la solución de supervisión de contenedor de hello está establecido correctamente para Windows.</span><span class="sxs-lookup"><span data-stu-id="ab70c-345">You can verify that hello Container Monitoring solution is set correctly for Windows.</span></span> <span data-ttu-id="ab70c-346">toocheck si el módulo de administración de hello era descarga correctamente, busque *ContainerManagement.xxx*.</span><span class="sxs-lookup"><span data-stu-id="ab70c-346">toocheck whether hello management pack was download properly, look for *ContainerManagement.xxx*.</span></span> <span data-ttu-id="ab70c-347">archivos de Hello deben estar en la carpeta C:\Program Files\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs de Hola.</span><span class="sxs-lookup"><span data-stu-id="ab70c-347">hello files should be in hello C:\Program Files\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs folder.</span></span>


## <a name="solution-components"></a><span data-ttu-id="ab70c-348">Componentes de soluciones</span><span class="sxs-lookup"><span data-stu-id="ab70c-348">Solution components</span></span>

<span data-ttu-id="ab70c-349">Si está utilizando a Windows agentes, a continuación, hello siguiente módulo de administración se instala en cada equipo con un agente cuando se agrega esta solución.</span><span class="sxs-lookup"><span data-stu-id="ab70c-349">If you are using Windows agents, then hello following management pack is installed on each computer with an agent when you add this solution.</span></span> <span data-ttu-id="ab70c-350">Ninguna configuración ni mantenimiento es necesario para el módulo de administración de Hola.</span><span class="sxs-lookup"><span data-stu-id="ab70c-350">No configuration or maintenance is required for hello management pack.</span></span>

- <span data-ttu-id="ab70c-351">*ContainerManagement.xxx* instalado en C:\Program Files\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs</span><span class="sxs-lookup"><span data-stu-id="ab70c-351">*ContainerManagement.xxx* installed in C:\Program Files\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs</span></span>

## <a name="container-data-collection-details"></a><span data-ttu-id="ab70c-352">Información detallada sobre la recopilación de datos en contenedores</span><span class="sxs-lookup"><span data-stu-id="ab70c-352">Container data collection details</span></span>
<span data-ttu-id="ab70c-353">Hola solución de supervisión de contenedor recopila diversos datos de registro y métricas de rendimiento de hosts de contenedor y los contenedores con agentes que se activan.</span><span class="sxs-lookup"><span data-stu-id="ab70c-353">hello Container Monitoring solution collects various performance metrics and log data from container hosts and containers using agents that you enable.</span></span>

<span data-ttu-id="ab70c-354">Datos se recopilan cada tres minutos por hello siguientes tipos de agente.</span><span class="sxs-lookup"><span data-stu-id="ab70c-354">Data is collected every three minutes by hello following agent types.</span></span>

- [<span data-ttu-id="ab70c-355">Agente de OMS para Linux</span><span class="sxs-lookup"><span data-stu-id="ab70c-355">OMS Agent for Linux</span></span>](log-analytics-linux-agents.md)
- [<span data-ttu-id="ab70c-356">Agente de Windows</span><span class="sxs-lookup"><span data-stu-id="ab70c-356">Windows agent</span></span>](log-analytics-windows-agents.md)
- [<span data-ttu-id="ab70c-357">Extensión de VM de Log Analytics</span><span class="sxs-lookup"><span data-stu-id="ab70c-357">Log Analytics VM extension</span></span>](log-analytics-azure-vm-extension.md)


### <a name="container-records"></a><span data-ttu-id="ab70c-358">Registros de contenedor</span><span class="sxs-lookup"><span data-stu-id="ab70c-358">Container records</span></span>

<span data-ttu-id="ab70c-359">Hello siguiente tabla muestran ejemplos de registros recopilados por la solución de supervisión de contenedor de Hola y tipos de datos de Hola que aparecen en los resultados de búsqueda de registros.</span><span class="sxs-lookup"><span data-stu-id="ab70c-359">hello following table shows examples of records collected by hello Container Monitoring solution and hello data types that appear in log search results.</span></span>

| <span data-ttu-id="ab70c-360">Tipo de datos</span><span class="sxs-lookup"><span data-stu-id="ab70c-360">Data type</span></span> | <span data-ttu-id="ab70c-361">Tipo de datos en la búsqueda de registros</span><span class="sxs-lookup"><span data-stu-id="ab70c-361">Data type in Log Search</span></span> | <span data-ttu-id="ab70c-362">Fields</span><span class="sxs-lookup"><span data-stu-id="ab70c-362">Fields</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ab70c-363">Rendimiento de hosts y contenedores</span><span class="sxs-lookup"><span data-stu-id="ab70c-363">Performance for hosts and containers</span></span> | `Type=Perf` | <span data-ttu-id="ab70c-364">Computer, ObjectName, CounterName &#40;%Processor Time, Disk Reads MB, Disk Writes MB, Memory Usage MB, Network Receive Bytes, Network Send Bytes, Processor Usage sec, Network&#41;, CounterValue,TimeGenerated, CounterPath, SourceSystem</span><span class="sxs-lookup"><span data-stu-id="ab70c-364">Computer, ObjectName, CounterName &#40;%Processor Time, Disk Reads MB, Disk Writes MB, Memory Usage MB, Network Receive Bytes, Network Send Bytes, Processor Usage sec, Network&#41;, CounterValue,TimeGenerated, CounterPath, SourceSystem</span></span> |
| <span data-ttu-id="ab70c-365">Inventario de contenedor</span><span class="sxs-lookup"><span data-stu-id="ab70c-365">Container inventory</span></span> | `Type=ContainerInventory` | <span data-ttu-id="ab70c-366">TimeGenerated, Computer, container name, ContainerHostname, Image, ImageTag, ContainerState, ExitCode, EnvironmentVar, Command, CreatedTime, StartedTime, FinishedTime, SourceSystem, ContainerID, ImageID</span><span class="sxs-lookup"><span data-stu-id="ab70c-366">TimeGenerated, Computer, container name, ContainerHostname, Image, ImageTag, ContainerState, ExitCode, EnvironmentVar, Command, CreatedTime, StartedTime, FinishedTime, SourceSystem, ContainerID, ImageID</span></span> |
| <span data-ttu-id="ab70c-367">Inventario de imágenes de contenedor</span><span class="sxs-lookup"><span data-stu-id="ab70c-367">Container image inventory</span></span> | `Type=ContainerImageInventory` | <span data-ttu-id="ab70c-368">TimeGenerated, Computer, Image, ImageTag, ImageSize, VirtualSize, Running, Paused, Stopped, Failed, SourceSystem, ImageID, TotalContainer</span><span class="sxs-lookup"><span data-stu-id="ab70c-368">TimeGenerated, Computer, Image, ImageTag, ImageSize, VirtualSize, Running, Paused, Stopped, Failed, SourceSystem, ImageID, TotalContainer</span></span> |
| <span data-ttu-id="ab70c-369">Registro de contenedor</span><span class="sxs-lookup"><span data-stu-id="ab70c-369">Container log</span></span> | `Type=ContainerLog` | <span data-ttu-id="ab70c-370">TimeGenerated, Computer, image ID, container name, LogEntrySource, LogEntry, SourceSystem, ContainerID</span><span class="sxs-lookup"><span data-stu-id="ab70c-370">TimeGenerated, Computer, image ID, container name, LogEntrySource, LogEntry, SourceSystem, ContainerID</span></span> |
| <span data-ttu-id="ab70c-371">Registro del servicio de contenedores</span><span class="sxs-lookup"><span data-stu-id="ab70c-371">Container service log</span></span> | `Type=ContainerServiceLog`  | <span data-ttu-id="ab70c-372">TimeGenerated, Computer, TimeOfCommand, Image, Command, SourceSystem, ContainerID</span><span class="sxs-lookup"><span data-stu-id="ab70c-372">TimeGenerated, Computer, TimeOfCommand, Image, Command, SourceSystem, ContainerID</span></span> |
| <span data-ttu-id="ab70c-373">Inventario de nodo de contenedor</span><span class="sxs-lookup"><span data-stu-id="ab70c-373">Container node inventory</span></span> | `Type=ContainerNodeInventory_CL`| <span data-ttu-id="ab70c-374">TimeGenerated, Computer, ClassName_s, DockerVersion_s, OperatingSystem_s, Volume_s, Network_s, NodeRole_s, OrchestratorType_s, InstanceID_g, SourceSystem</span><span class="sxs-lookup"><span data-stu-id="ab70c-374">TimeGenerated, Computer, ClassName_s, DockerVersion_s, OperatingSystem_s, Volume_s, Network_s, NodeRole_s, OrchestratorType_s, InstanceID_g, SourceSystem</span></span>|
| <span data-ttu-id="ab70c-375">Inventario de Kubernetes</span><span class="sxs-lookup"><span data-stu-id="ab70c-375">Kubernetes inventory</span></span> | `Type=KubePodInventory_CL` | <span data-ttu-id="ab70c-376">TimeGenerated, Computer, PodLabel_deployment_s, PodLabel_deploymentconfig_s, PodLabel_docker_registry_s, Name_s, Namespace_s, PodStatus_s, PodIp_s, PodUid_g, PodCreationTimeStamp_t, SourceSystem</span><span class="sxs-lookup"><span data-stu-id="ab70c-376">TimeGenerated, Computer, PodLabel_deployment_s, PodLabel_deploymentconfig_s, PodLabel_docker_registry_s, Name_s, Namespace_s, PodStatus_s, PodIp_s, PodUid_g, PodCreationTimeStamp_t, SourceSystem</span></span> |
| <span data-ttu-id="ab70c-377">Proceso del contenedor</span><span class="sxs-lookup"><span data-stu-id="ab70c-377">Container process</span></span> | `Type=ContainerProcess_CL` | <span data-ttu-id="ab70c-378">TimeGenerated, Computer, Pod_s, Namespace_s, ClassName_s, InstanceID_s, Uid_s, PID_s, PPID_s, C_s, STIME_s, Tty_s, TIME_s, Cmd_s, Id_s, Name_s, SourceSystem</span><span class="sxs-lookup"><span data-stu-id="ab70c-378">TimeGenerated, Computer, Pod_s, Namespace_s, ClassName_s, InstanceID_s, Uid_s, PID_s, PPID_s, C_s, STIME_s, Tty_s, TIME_s, Cmd_s, Id_s, Name_s, SourceSystem</span></span> |
| <span data-ttu-id="ab70c-379">Eventos de Kubernetes</span><span class="sxs-lookup"><span data-stu-id="ab70c-379">Kubernetes events</span></span> | `Type=KubeEvents_CL` | <span data-ttu-id="ab70c-380">TimeGenerated, Computer, Name_s, ObjectKind_s, Namespace_s, Reason_s, Type_s, SourceComponent_s, SourceSystem, Message</span><span class="sxs-lookup"><span data-stu-id="ab70c-380">TimeGenerated, Computer, Name_s, ObjectKind_s, Namespace_s, Reason_s, Type_s, SourceComponent_s, SourceSystem, Message</span></span> |

<span data-ttu-id="ab70c-381">Las etiquetas se anexan demasiado*PodLabel* tipos de datos son sus propias etiquetas personalizadas.</span><span class="sxs-lookup"><span data-stu-id="ab70c-381">Labels appended too*PodLabel* data types are your own custom labels.</span></span> <span data-ttu-id="ab70c-382">Hello anexadas etiquetas PodLabel se muestra en la tabla de hello son ejemplos.</span><span class="sxs-lookup"><span data-stu-id="ab70c-382">hello appended PodLabel labels shown in hello table are examples.</span></span> <span data-ttu-id="ab70c-383">Por lo tanto, `PodLabel_deployment_s`, `PodLabel_deploymentconfig_s`, `PodLabel_docker_registry_s` se diferencian en el conjunto de datos de su entorno y genéricamente son similares a `PodLabel_yourlabel_s`.</span><span class="sxs-lookup"><span data-stu-id="ab70c-383">So, `PodLabel_deployment_s`, `PodLabel_deploymentconfig_s`, `PodLabel_docker_registry_s` will differ in your environment's data set and generically resemble `PodLabel_yourlabel_s`.</span></span>


## <a name="monitor-containers"></a><span data-ttu-id="ab70c-384">Supervisión de contenedores</span><span class="sxs-lookup"><span data-stu-id="ab70c-384">Monitor containers</span></span>
<span data-ttu-id="ab70c-385">Una vez haya solución Hola habilitada en el portal de OMS hello, Hola **contenedores** icono muestra información de resumen sobre los hosts de contenedor y los contenedores de Hola que se ejecutan en hosts.</span><span class="sxs-lookup"><span data-stu-id="ab70c-385">After you have hello solution enabled in hello OMS portal, hello **Containers** tile shows summary information about your container hosts and hello containers running in hosts.</span></span>

![Icono de Containers](./media/log-analytics-containers/containers-title.png)

<span data-ttu-id="ab70c-387">icono de Hello muestra un resumen de cuántos contenedores tiene en entorno de Hola y si está error, ejecución o detenido.</span><span class="sxs-lookup"><span data-stu-id="ab70c-387">hello tile shows an overview of how many containers you have in hello environment and whether they're failed, running, or stopped.</span></span>

### <a name="using-hello-containers-dashboard"></a><span data-ttu-id="ab70c-388">Utilizando el panel de contenedores de Hola</span><span class="sxs-lookup"><span data-stu-id="ab70c-388">Using hello Containers dashboard</span></span>
<span data-ttu-id="ab70c-389">Haga clic en hello **contenedores** icono.</span><span class="sxs-lookup"><span data-stu-id="ab70c-389">Click hello **Containers** tile.</span></span> <span data-ttu-id="ab70c-390">Desde allí verá las vistas organizadas por:</span><span class="sxs-lookup"><span data-stu-id="ab70c-390">From there you'll see views organized by:</span></span>

- <span data-ttu-id="ab70c-391">**Eventos de contenedor**: muestra el estado de contenedor y los equipos con contenedores en estado de error.</span><span class="sxs-lookup"><span data-stu-id="ab70c-391">**Container Events** - Shows container status and computers with failed containers.</span></span>
- <span data-ttu-id="ab70c-392">**Registros de contenedor** -muestra un gráfico de los archivos de registro de contenedor generados con el tiempo y una lista de equipos con mayor número de archivos de registro de hello.</span><span class="sxs-lookup"><span data-stu-id="ab70c-392">**Container Logs** - Shows a chart of container log files generated over time and a list of computers with hello highest number of log files.</span></span>
- <span data-ttu-id="ab70c-393">**Eventos de Kubernetes** -muestra un gráfico de eventos de Kubernetes generados con el tiempo y una lista de motivos de hello ¿por qué pod genera eventos de Hola.</span><span class="sxs-lookup"><span data-stu-id="ab70c-393">**Kubernetes Events** - Shows a chart of Kubernetes events generated over time and a list of hello reasons why pods generated hello events.</span></span> <span data-ttu-id="ab70c-394">*Este conjunto de datos solo se usa en entornos Linux.*</span><span class="sxs-lookup"><span data-stu-id="ab70c-394">*This data set is used only in Linux environments.*</span></span>
- <span data-ttu-id="ab70c-395">**Inventario de Namespace Kubernetes** : muestra el número de Hola de espacios de nombres y cajas de y muestra su jerarquía.</span><span class="sxs-lookup"><span data-stu-id="ab70c-395">**Kubernetes Namespace Inventory** - Shows hello number of namespaces and pods and shows their hierarchy.</span></span> <span data-ttu-id="ab70c-396">*Este conjunto de datos solo se usa en entornos Linux.*</span><span class="sxs-lookup"><span data-stu-id="ab70c-396">*This data set is used only in Linux environments.*</span></span>
- <span data-ttu-id="ab70c-397">**Inventario de nodo de contenedor** -muestra hello número de tipos de orquestación usada en nodos/hosts del contenedor.</span><span class="sxs-lookup"><span data-stu-id="ab70c-397">**Container Node Inventory** - Shows hello number of orchestration types used on container nodes/hosts.</span></span> <span data-ttu-id="ab70c-398">nodos del equipo Hola/hosts también se enumeran por número de Hola de contenedores.</span><span class="sxs-lookup"><span data-stu-id="ab70c-398">hello computer nodes/hosts are also listed by hello number of containers.</span></span> <span data-ttu-id="ab70c-399">*Este conjunto de datos solo se usa en entornos Linux.*</span><span class="sxs-lookup"><span data-stu-id="ab70c-399">*This data set is used only in Linux environments.*</span></span>
- <span data-ttu-id="ab70c-400">**Inventario de imágenes de contenedor** -muestra el número total de Hola de imágenes de contenedor que se utilizan y el número de tipos de imagen.</span><span class="sxs-lookup"><span data-stu-id="ab70c-400">**Container Images Inventory** - Shows hello total number of container images used and number of image types.</span></span> <span data-ttu-id="ab70c-401">número de Hola de imágenes también se muestran por etiqueta de imagen de Hola.</span><span class="sxs-lookup"><span data-stu-id="ab70c-401">hello number of images are also listed by hello image tag.</span></span>
- <span data-ttu-id="ab70c-402">**Estado de contenedores** -muestra el número total de hello del contenedor de equipos de host/nodos que tienen contenedores en ejecución.</span><span class="sxs-lookup"><span data-stu-id="ab70c-402">**Containers Status** - Shows hello total number of container nodes/host computers that have running containers.</span></span> <span data-ttu-id="ab70c-403">También se muestran los equipos por número de Hola de hosts en ejecución.</span><span class="sxs-lookup"><span data-stu-id="ab70c-403">Computers are also listed by hello number of running hosts.</span></span>
- <span data-ttu-id="ab70c-404">**Procesos del contenedor**: muestra un gráfico de líneas de procesos de contenedor en ejecución a lo largo del tiempo.</span><span class="sxs-lookup"><span data-stu-id="ab70c-404">**Container Process** - Shows a line chart of container processes running over time.</span></span> <span data-ttu-id="ab70c-405">También se enumeran los contenedores según los comandos o procesos en ejecución en los contenedores.</span><span class="sxs-lookup"><span data-stu-id="ab70c-405">Containers are also listed by running command/process within containers.</span></span> <span data-ttu-id="ab70c-406">*Este conjunto de datos solo se usa en entornos Linux.*</span><span class="sxs-lookup"><span data-stu-id="ab70c-406">*This data set is used only in Linux environments.*</span></span>
- <span data-ttu-id="ab70c-407">**Rendimiento de la CPU de contenedor** -muestra un gráfico de líneas Hola promedio de uso de CPU con el tiempo para hosts de nodos de equipo.</span><span class="sxs-lookup"><span data-stu-id="ab70c-407">**Container CPU Performance** - Shows a line chart of hello average CPU utilization over time for computer nodes/hosts.</span></span> <span data-ttu-id="ab70c-408">También listas Hola equipo/hosts de nodos se basan en Media de la CPU.</span><span class="sxs-lookup"><span data-stu-id="ab70c-408">Also lists hello computer nodes/hosts based on average CPU utilization.</span></span>
- <span data-ttu-id="ab70c-409">**Rendimiento de la memoria del contenedor**: muestra un gráfico de líneas del uso de memoria a lo largo del tiempo.</span><span class="sxs-lookup"><span data-stu-id="ab70c-409">**Container Memory Performance** - Shows a line chart of memory usage over time.</span></span> <span data-ttu-id="ab70c-410">También muestra el uso de memoria de los equipos según el nombre de la instancia.</span><span class="sxs-lookup"><span data-stu-id="ab70c-410">Also lists computer memory utilization based on instance name.</span></span>
- <span data-ttu-id="ab70c-411">**Rendimiento del equipo** -muestra el porcentaje de uso de memoria con el tiempo y megabytes de espacio libre en disco de gráficos de líneas de porcentaje de Hola de rendimiento de la CPU con el tiempo, con el tiempo.</span><span class="sxs-lookup"><span data-stu-id="ab70c-411">**Computer Performance** - Shows line charts of hello percent of CPU performance over time, percent of memory usage over time, and megabytes of free disk space over time.</span></span> <span data-ttu-id="ab70c-412">Puede mantener el mouse sobre cualquier línea de un gráfico tooview más detalles.</span><span class="sxs-lookup"><span data-stu-id="ab70c-412">You can hover over any line in a chart tooview more details.</span></span>


<span data-ttu-id="ab70c-413">Cada área del panel de hello es una representación visual de una búsqueda que se ejecuta en los datos recopilados.</span><span class="sxs-lookup"><span data-stu-id="ab70c-413">Each area of hello dashboard is a visual representation of a search that is run on collected data.</span></span>

![Panel Containers](./media/log-analytics-containers/containers-dash01.png)

![Panel Containers](./media/log-analytics-containers/containers-dash02.png)

<span data-ttu-id="ab70c-416">Hola **estado de contenedor** área, haga clic en la parte superior de hello, tal y como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="ab70c-416">In hello **Container Status** area, click hello top area, as shown below.</span></span>

![Estado de los contenedores](./media/log-analytics-containers/containers-status.png)

<span data-ttu-id="ab70c-418">Búsqueda de registros, se muestra información sobre el estado de saludo de los contenedores.</span><span class="sxs-lookup"><span data-stu-id="ab70c-418">Log Search opens, displaying information about hello state of your containers.</span></span>

![Búsqueda de registros para contenedores](./media/log-analytics-containers/containers-log-search.png)

<span data-ttu-id="ab70c-420">Desde aquí, puede editar toomodify de consulta de búsqueda de hello, información específica de toofind Hola que le interesa.</span><span class="sxs-lookup"><span data-stu-id="ab70c-420">From here, you can edit hello search query toomodify it toofind hello specific information you're interested in.</span></span> <span data-ttu-id="ab70c-421">Para más información acerca del uso de la búsqueda de registros, consulte [Búsquedas de registros en Log Analytics](log-analytics-log-searches.md).</span><span class="sxs-lookup"><span data-stu-id="ab70c-421">For more information about Log Searches, see [Log searches in Log Analytics](log-analytics-log-searches.md).</span></span>

## <a name="troubleshoot-by-finding-a-failed-container"></a><span data-ttu-id="ab70c-422">Solución de problemas mediante la búsqueda de un contenedor con error</span><span class="sxs-lookup"><span data-stu-id="ab70c-422">Troubleshoot by finding a failed container</span></span>

<span data-ttu-id="ab70c-423">Log Analytics marca un contenedor como **Failed** (Error) si ha terminado con un código de salida distinto de cero.</span><span class="sxs-lookup"><span data-stu-id="ab70c-423">Log Analytics marks a container as **Failed** if it has exited with a non-zero exit code.</span></span> <span data-ttu-id="ab70c-424">Puede ver un resumen de errores de Hola y errores en el entorno de Hola Hola **contenedores no se pudo** área.</span><span class="sxs-lookup"><span data-stu-id="ab70c-424">You can see an overview of hello errors and failures in hello environment in hello **Failed Containers** area.</span></span>

### <a name="toofind-failed-containers"></a><span data-ttu-id="ab70c-425">toofind no se pudo contenedores</span><span class="sxs-lookup"><span data-stu-id="ab70c-425">toofind failed containers</span></span>
1. <span data-ttu-id="ab70c-426">Haga clic en hello **estado de contenedor** área.</span><span class="sxs-lookup"><span data-stu-id="ab70c-426">Click hello **Container Status** area.</span></span>  
   <span data-ttu-id="ab70c-427">![estado de los contenedores](./media/log-analytics-containers/containers-status.png)</span><span class="sxs-lookup"><span data-stu-id="ab70c-427">![containers status](./media/log-analytics-containers/containers-status.png)</span></span>
2. <span data-ttu-id="ab70c-428">Búsqueda de registros se abre y muestra el estado de Hola de los contenedores, toohello similar después.</span><span class="sxs-lookup"><span data-stu-id="ab70c-428">Log Search opens and displays hello state of your containers, similar toohello following.</span></span>  
   ![estado de los contenedores](./media/log-analytics-containers/containers-log-search.png)
3. <span data-ttu-id="ab70c-430">A continuación, haga clic en el valor de hello agregado de información adicional de errores contenedores tooview.</span><span class="sxs-lookup"><span data-stu-id="ab70c-430">Next, click hello aggregated value of failed containers tooview additional information.</span></span> <span data-ttu-id="ab70c-431">Expanda **mostrar más** imagen de identificador hello tooview.</span><span class="sxs-lookup"><span data-stu-id="ab70c-431">Expand **show more** tooview hello image ID.</span></span>  
   <span data-ttu-id="ab70c-432">![contenedores con errores](./media/log-analytics-containers/containers-state-failed.png)</span><span class="sxs-lookup"><span data-stu-id="ab70c-432">![failed containers](./media/log-analytics-containers/containers-state-failed.png)</span></span>  
4. <span data-ttu-id="ab70c-433">A continuación, escriba el siguiente de hello en la consulta de búsqueda de Hola.</span><span class="sxs-lookup"><span data-stu-id="ab70c-433">Next, type hello following in hello search query.</span></span> <span data-ttu-id="ab70c-434">`Type=ContainerInventory <ImageID>`toosee los detalles acerca de la imagen de hello como tamaño de la imagen y el número de imágenes detenidas pero no lo consiguió.</span><span class="sxs-lookup"><span data-stu-id="ab70c-434">`Type=ContainerInventory <ImageID>` toosee details about hello image such as image size and number of stopped and failed images.</span></span>  
   <span data-ttu-id="ab70c-435">![contenedores con errores](./media/log-analytics-containers/containers-failed04.png)</span><span class="sxs-lookup"><span data-stu-id="ab70c-435">![failed containers](./media/log-analytics-containers/containers-failed04.png)</span></span>

## <a name="search-logs-for-container-data"></a><span data-ttu-id="ab70c-436">Registros de búsqueda de datos de contenedor</span><span class="sxs-lookup"><span data-stu-id="ab70c-436">Search logs for container data</span></span>
<span data-ttu-id="ab70c-437">Cuando esté solucionando problemas de un error específico, puede ayudar a toosee donde se lleva a cabo en su entorno.</span><span class="sxs-lookup"><span data-stu-id="ab70c-437">When you're troubleshooting a specific error, it can help toosee where it is occurring in your environment.</span></span> <span data-ttu-id="ab70c-438">Hola siguientes tipos de registro le ayudará a crear consultas de información de hello tooreturn que desee.</span><span class="sxs-lookup"><span data-stu-id="ab70c-438">hello following log types will help you create queries tooreturn hello information you want.</span></span>


- <span data-ttu-id="ab70c-439">**ContainerImageInventory** : Utilice este tipo si está tratando de información de toofind organizada por información de la imagen de imagen y tooview como identificadores de imagen o tamaños.</span><span class="sxs-lookup"><span data-stu-id="ab70c-439">**ContainerImageInventory** – Use this type when you're trying toofind information organized by image and tooview image information such as image IDs or sizes.</span></span>
- <span data-ttu-id="ab70c-440">**ContainerInventory**: use este tipo si desea obtener información sobre la ubicación del contenedor, cuáles son sus nombres y qué imágenes se están ejecutando.</span><span class="sxs-lookup"><span data-stu-id="ab70c-440">**ContainerInventory** – Use this type when you want information about container location, what their names are, and what images they're running.</span></span>
- <span data-ttu-id="ab70c-441">**ContainerLog** : Use este tipo cuando se desea información de registro de toofind específica del error y las entradas.</span><span class="sxs-lookup"><span data-stu-id="ab70c-441">**ContainerLog** – Use this type when you want toofind specific error log information and entries.</span></span>
- <span data-ttu-id="ab70c-442">**ContainerNodeInventory_CL** usar este tipo cuando desee Hola información acerca de host/nodo donde se encuentran los contenedores.</span><span class="sxs-lookup"><span data-stu-id="ab70c-442">**ContainerNodeInventory_CL**  Use this type when you want hello information about host/node where containers are residing.</span></span> <span data-ttu-id="ab70c-443">Proporciona información sobre la versión de Docker, el tipo de orquestación, almacenamiento y red.</span><span class="sxs-lookup"><span data-stu-id="ab70c-443">It provides you Docker version, orchestration type, storage, and network information.</span></span>
- <span data-ttu-id="ab70c-444">**ContainerProcess_CL** Utilice este tipo tooquickly consulte proceso Hola que se ejecuta en el contenedor de Hola.</span><span class="sxs-lookup"><span data-stu-id="ab70c-444">**ContainerProcess_CL** Use this type tooquickly see hello process running within hello container.</span></span>
- <span data-ttu-id="ab70c-445">**ContainerServiceLog** : Use este tipo al que está tratando de información de pista de auditoría de toofind para hello demonio de Docker, como iniciar, detener, eliminar o comandos de extracción.</span><span class="sxs-lookup"><span data-stu-id="ab70c-445">**ContainerServiceLog** – Use this type when you're trying toofind audit trail information for hello Docker daemon, such as start, stop, delete, or pull commands.</span></span>
- <span data-ttu-id="ab70c-446">**KubeEvents_CL** usar esta tipo toosee hello Kubernetes los eventos.</span><span class="sxs-lookup"><span data-stu-id="ab70c-446">**KubeEvents_CL**  Use this type toosee hello Kubernetes events.</span></span>
- <span data-ttu-id="ab70c-447">**KubePodInventory_CL** usar este tipo si desea información de jerarquía de clúster de toounderstand Hola.</span><span class="sxs-lookup"><span data-stu-id="ab70c-447">**KubePodInventory_CL**  Use this type when you want toounderstand hello cluster hierarchy information.</span></span>


### <a name="toosearch-logs-for-container-data"></a><span data-ttu-id="ab70c-448">toosearch registros de datos del contenedor</span><span class="sxs-lookup"><span data-stu-id="ab70c-448">toosearch logs for container data</span></span>
* <span data-ttu-id="ab70c-449">Elija una imagen que sabe que no ha funcionado recientemente y buscar registros de errores de Hola para ellos.</span><span class="sxs-lookup"><span data-stu-id="ab70c-449">Choose an image that you know has failed recently and find hello error logs for it.</span></span> <span data-ttu-id="ab70c-450">Para empezar, busque un nombre de contenedor que esté ejecutando esa imagen con una búsqueda **ContainerInventory**.</span><span class="sxs-lookup"><span data-stu-id="ab70c-450">Start by finding a container name that is running that image with a **ContainerInventory** search.</span></span> <span data-ttu-id="ab70c-451">Por ejemplo, busque `Type=ContainerInventory ubuntu Failed`.</span><span class="sxs-lookup"><span data-stu-id="ab70c-451">For example, search for `Type=ContainerInventory ubuntu Failed`</span></span>  
    <span data-ttu-id="ab70c-452">![Búsqueda de contenedores de Ubuntu](./media/log-analytics-containers/search-ubuntu.png)</span><span class="sxs-lookup"><span data-stu-id="ab70c-452">![Search for Ubuntu containers](./media/log-analytics-containers/search-ubuntu.png)</span></span>

  <span data-ttu-id="ab70c-453">Hola a continuación el nombre del contenedor de hello demasiado**nombre**y busque los registros.</span><span class="sxs-lookup"><span data-stu-id="ab70c-453">hello name of hello container next too**Name**, and search for those logs.</span></span> <span data-ttu-id="ab70c-454">En este ejemplo, es `Type=ContainerLog cranky_stonebreaker`.</span><span class="sxs-lookup"><span data-stu-id="ab70c-454">In this example, it is `Type=ContainerLog cranky_stonebreaker`.</span></span>

<span data-ttu-id="ab70c-455">**Ver información de rendimiento**</span><span class="sxs-lookup"><span data-stu-id="ab70c-455">**View performance information**</span></span>

<span data-ttu-id="ab70c-456">Cuando está empezando tooconstruct consultas, puede ayudar a toosee lo que es posible en primer lugar.</span><span class="sxs-lookup"><span data-stu-id="ab70c-456">When you're beginning tooconstruct queries, it can help toosee what's possible first.</span></span> <span data-ttu-id="ab70c-457">Por ejemplo, toosee buscar todos los datos de rendimiento, intente una amplia consulta escribiendo Hola después de consultar.</span><span class="sxs-lookup"><span data-stu-id="ab70c-457">For example, toosee all performance data, try a broad query by typing hello following search query.</span></span>

```
Type=Perf
```

![rendimiento de contenedores](./media/log-analytics-containers/containers-perf01.png)

<span data-ttu-id="ab70c-459">Puede definir el ámbito de los datos de rendimiento de Hola que está viendo contenedor específico tooa escribiendo el nombre de hello del mismo toohello derecha de la consulta.</span><span class="sxs-lookup"><span data-stu-id="ab70c-459">You can scope hello performance data you're seeing tooa specific container by typing hello name of it toohello right of your query.</span></span>

```
Type=Perf <containerName>
```

<span data-ttu-id="ab70c-460">Que muestra la lista de Hola de métricas de rendimiento que se recopilan para un contenedor por separado.</span><span class="sxs-lookup"><span data-stu-id="ab70c-460">That shows hello list of performance metrics that are collected for an individual container.</span></span>

![rendimiento de contenedores](./media/log-analytics-containers/containers-perf03.png)

## <a name="example-log-search-queries"></a><span data-ttu-id="ab70c-462">Ejemplos de consultas de búsqueda de registros</span><span class="sxs-lookup"><span data-stu-id="ab70c-462">Example log search queries</span></span>
<span data-ttu-id="ab70c-463">A menudo útil toobuild su consulta a partir de un ejemplo o dos y, a continuación, modificándolos toofit su entorno.</span><span class="sxs-lookup"><span data-stu-id="ab70c-463">It's often useful toobuild queries starting with an example or two and then modifying them toofit your environment.</span></span> <span data-ttu-id="ab70c-464">Como punto de partida, puede experimentar con hello **consultas de ejemplo** toohelp de área se generan las consultas más avanzadas.</span><span class="sxs-lookup"><span data-stu-id="ab70c-464">As a starting point, you can experiment with hello **Sample Queries** area toohelp you build more advanced queries.</span></span>

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

![Consultas de contenedores](./media/log-analytics-containers/containers-queries.png)


## <a name="saving-log-search-queries"></a><span data-ttu-id="ab70c-466">Guardado de consultas de búsqueda de registros</span><span class="sxs-lookup"><span data-stu-id="ab70c-466">Saving log search queries</span></span>
<span data-ttu-id="ab70c-467">El guardado de consultas es una característica estándar de Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="ab70c-467">Saving queries is a standard feature in Log Analytics.</span></span> <span data-ttu-id="ab70c-468">Guárdelas para volver a usar en el futuro aquellas que haya encontrado más útiles.</span><span class="sxs-lookup"><span data-stu-id="ab70c-468">By saving them, you'll have those that you've found useful handy for future use.</span></span>

<span data-ttu-id="ab70c-469">Después de crear una consulta que encuentre útil, puede guardarlo si hace clic **favoritos** al principio de Hola de página de búsqueda de registros de Hola.</span><span class="sxs-lookup"><span data-stu-id="ab70c-469">After you create a query that you find useful, save it by clicking **Favorites** at hello top of hello Log Search page.</span></span> <span data-ttu-id="ab70c-470">A continuación, se puede acceder fácilmente a ella más adelante desde hello **Mi panel** página.</span><span class="sxs-lookup"><span data-stu-id="ab70c-470">Then you can easily access it later from hello **My Dashboard** page.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ab70c-471">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ab70c-471">Next steps</span></span>
* <span data-ttu-id="ab70c-472">[Buscar registros](log-analytics-log-searches.md) tooview obtener registros de datos del contenedor.</span><span class="sxs-lookup"><span data-stu-id="ab70c-472">[Search logs](log-analytics-log-searches.md) tooview detailed container data records.</span></span>
