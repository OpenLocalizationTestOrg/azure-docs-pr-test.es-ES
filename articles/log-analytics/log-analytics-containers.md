---
title: "Solución de Supervisión de contenedores de Azure Log Analytics | Microsoft Docs"
description: "La solución de Supervisión de contenedores de Log Analytics le ayuda a ver y administrar los hosts de contenedores de Docker y Windows en una sola ubicación."
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
ms.openlocfilehash: b2e03531ee401f4552198e5dd50fbfe1d970f0e5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="container-monitoring-solution-in-log-analytics"></a><span data-ttu-id="cebcc-103">Solución de Supervisión de contenedores de Azure Log Analytics</span><span class="sxs-lookup"><span data-stu-id="cebcc-103">Container Monitoring solution in Log Analytics</span></span>

![Símbolo de Containers](./media/log-analytics-containers/containers-symbol.png)

<span data-ttu-id="cebcc-105">En este artículo se describe cómo configurar y usar la solución de Supervisión de contenedores de Log Analytics, que le permite ver y administrar los hosts de contenedores de Docker y Windows en una sola ubicación.</span><span class="sxs-lookup"><span data-stu-id="cebcc-105">This article describes how to set up and use the Container Monitoring solution in Log Analytics, which helps you view and manage your Docker and Windows container hosts in a single location.</span></span> <span data-ttu-id="cebcc-106">Docker es un sistema de virtualización de software que usa para crear contenedores que automatizan la implementación de software en su infraestructura de TI.</span><span class="sxs-lookup"><span data-stu-id="cebcc-106">Docker is a software virtualization system used to create containers that automate software deployment to their IT infrastructure.</span></span>

<span data-ttu-id="cebcc-107">La solución muestra qué contenedores están en ejecución, qué imagen de contenedor están ejecutando y dónde se ejecutan los contenedores.</span><span class="sxs-lookup"><span data-stu-id="cebcc-107">The solution shows which containers are running, what container image they’re running, and where containers are running.</span></span> <span data-ttu-id="cebcc-108">Puede ver información de auditoría detallada que muestra los comandos que se usan con los contenedores.</span><span class="sxs-lookup"><span data-stu-id="cebcc-108">You can view detailed audit information showing commands used with containers.</span></span> <span data-ttu-id="cebcc-109">Y, para solucionar los problemas de los contenedores, puede ver y buscar registros centralizados sin tener que ver los hosts de Docker o Windows de forma remota.</span><span class="sxs-lookup"><span data-stu-id="cebcc-109">And, you can troubleshoot containers by viewing and searching centralized logs without having to remotely view Docker or Windows hosts.</span></span> <span data-ttu-id="cebcc-110">Puede encontrar los contenedores que están causando ruido o realizando un consumo excesivo de recursos en un host.</span><span class="sxs-lookup"><span data-stu-id="cebcc-110">You can find containers that may be noisy and consuming excess resources on a host.</span></span> <span data-ttu-id="cebcc-111">También puede ver la información centralizada acerca de la CPU, la memoria, el almacenamiento y el uso y el rendimiento de la red en relación con los contenedores.</span><span class="sxs-lookup"><span data-stu-id="cebcc-111">And, you can view centralized CPU, memory, storage, and network usage and performance information for containers.</span></span> <span data-ttu-id="cebcc-112">En equipos con Windows, puede centralizar y comparar registros de Windows Server, Hyper-V y contenedores de Docker.</span><span class="sxs-lookup"><span data-stu-id="cebcc-112">On computers running Windows, you can centralize and compare logs from Windows Server, Hyper-V, and Docker containers.</span></span> <span data-ttu-id="cebcc-113">La solución es compatible con los siguientes orquestadores de contenedores:</span><span class="sxs-lookup"><span data-stu-id="cebcc-113">The solution supports the following container orchestrators:</span></span>

- <span data-ttu-id="cebcc-114">Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="cebcc-114">Docker Swarm</span></span>
- <span data-ttu-id="cebcc-115">DC/OS</span><span class="sxs-lookup"><span data-stu-id="cebcc-115">DC/OS</span></span>
- <span data-ttu-id="cebcc-116">kubernetes</span><span class="sxs-lookup"><span data-stu-id="cebcc-116">Kubernetes</span></span>
- <span data-ttu-id="cebcc-117">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="cebcc-117">Service Fabric</span></span>
- <span data-ttu-id="cebcc-118">Red Hat OpenShift</span><span class="sxs-lookup"><span data-stu-id="cebcc-118">Red Hat OpenShift</span></span>


<span data-ttu-id="cebcc-119">El siguiente diagrama muestra las relaciones entre varios hosts de contenedores y los agentes con OMS.</span><span class="sxs-lookup"><span data-stu-id="cebcc-119">The following diagram shows the relationships between various container hosts and agents with OMS.</span></span>

![Diagrama de contenedores](./media/log-analytics-containers/containers-diagram.png)

## <a name="system-requirements"></a><span data-ttu-id="cebcc-121">Requisitos del sistema</span><span class="sxs-lookup"><span data-stu-id="cebcc-121">System requirements</span></span>

<span data-ttu-id="cebcc-122">Antes de comenzar, revise los detalles siguientes para comprobar que cumple los requisitos previos.</span><span class="sxs-lookup"><span data-stu-id="cebcc-122">Before starting, review the following details to verify you meet the prerequisites.</span></span>

### <a name="container-monitoring-solution-support-for-docker-orchestrator-and-os-platform"></a><span data-ttu-id="cebcc-123">Compatibilidad con solución de supervisión de contenedores para el orquestador y la plataforma de sistema operativo de Docker</span><span class="sxs-lookup"><span data-stu-id="cebcc-123">Container monitoring solution support for Docker Orchestrator and OS platform</span></span>
<span data-ttu-id="cebcc-124">En la tabla siguiente se hace un resumen de la compatibilidad de supervisión del sistema operativo y orquestación de Docker del inventario, rendimiento y registro de contenedores con Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="cebcc-124">The following table outlines the Docker orchestration and operating system monitoring support of container inventory, performance, and logs with Log Analytics.</span></span>   

| | <span data-ttu-id="cebcc-125">ACS</span><span class="sxs-lookup"><span data-stu-id="cebcc-125">ACS</span></span> | <span data-ttu-id="cebcc-126">Linux</span><span class="sxs-lookup"><span data-stu-id="cebcc-126">Linux</span></span> | <span data-ttu-id="cebcc-127">Windows</span><span class="sxs-lookup"><span data-stu-id="cebcc-127">Windows</span></span> | <span data-ttu-id="cebcc-128">Contenedor</span><span class="sxs-lookup"><span data-stu-id="cebcc-128">Container</span></span><br><span data-ttu-id="cebcc-129">Inventario</span><span class="sxs-lookup"><span data-stu-id="cebcc-129">Inventory</span></span> | <span data-ttu-id="cebcc-130">Imagen</span><span class="sxs-lookup"><span data-stu-id="cebcc-130">Image</span></span><br><span data-ttu-id="cebcc-131">Inventario</span><span class="sxs-lookup"><span data-stu-id="cebcc-131">Inventory</span></span> | <span data-ttu-id="cebcc-132">Nodo</span><span class="sxs-lookup"><span data-stu-id="cebcc-132">Node</span></span><br><span data-ttu-id="cebcc-133">Inventario</span><span class="sxs-lookup"><span data-stu-id="cebcc-133">Inventory</span></span> | <span data-ttu-id="cebcc-134">Contenedor</span><span class="sxs-lookup"><span data-stu-id="cebcc-134">Container</span></span><br><span data-ttu-id="cebcc-135">Rendimiento</span><span class="sxs-lookup"><span data-stu-id="cebcc-135">Performance</span></span> | <span data-ttu-id="cebcc-136">Contenedor</span><span class="sxs-lookup"><span data-stu-id="cebcc-136">Container</span></span><br><span data-ttu-id="cebcc-137">Evento</span><span class="sxs-lookup"><span data-stu-id="cebcc-137">Event</span></span> | <span data-ttu-id="cebcc-138">Evento</span><span class="sxs-lookup"><span data-stu-id="cebcc-138">Event</span></span><br><span data-ttu-id="cebcc-139">Registro</span><span class="sxs-lookup"><span data-stu-id="cebcc-139">Log</span></span> | <span data-ttu-id="cebcc-140">Contenedor</span><span class="sxs-lookup"><span data-stu-id="cebcc-140">Container</span></span><br><span data-ttu-id="cebcc-141">Registro</span><span class="sxs-lookup"><span data-stu-id="cebcc-141">Log</span></span> |
|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|
| <span data-ttu-id="cebcc-142">kubernetes</span><span class="sxs-lookup"><span data-stu-id="cebcc-142">Kubernetes</span></span> | <span data-ttu-id="cebcc-143">&#8226;</span><span class="sxs-lookup"><span data-stu-id="cebcc-143">&#8226;</span></span> | <span data-ttu-id="cebcc-144">&#8226;</span><span class="sxs-lookup"><span data-stu-id="cebcc-144">&#8226;</span></span> | | <span data-ttu-id="cebcc-145">&#8226;</span><span class="sxs-lookup"><span data-stu-id="cebcc-145">&#8226;</span></span> | <span data-ttu-id="cebcc-146">&#8226;</span><span class="sxs-lookup"><span data-stu-id="cebcc-146">&#8226;</span></span> | <span data-ttu-id="cebcc-147">&#8226;</span><span class="sxs-lookup"><span data-stu-id="cebcc-147">&#8226;</span></span> | <span data-ttu-id="cebcc-148">&#8226;</span><span class="sxs-lookup"><span data-stu-id="cebcc-148">&#8226;</span></span> | <span data-ttu-id="cebcc-149">&#8226;</span><span class="sxs-lookup"><span data-stu-id="cebcc-149">&#8226;</span></span> | <span data-ttu-id="cebcc-150">&#8226;</span><span class="sxs-lookup"><span data-stu-id="cebcc-150">&#8226;</span></span> | <span data-ttu-id="cebcc-151">&#8226;</span><span class="sxs-lookup"><span data-stu-id="cebcc-151">&#8226;</span></span> |
| <span data-ttu-id="cebcc-152">Mesosphere</span><span class="sxs-lookup"><span data-stu-id="cebcc-152">Mesosphere</span></span><br><span data-ttu-id="cebcc-153">DC/OS</span><span class="sxs-lookup"><span data-stu-id="cebcc-153">DC/OS</span></span> | <span data-ttu-id="cebcc-154">&#8226;</span><span class="sxs-lookup"><span data-stu-id="cebcc-154">&#8226;</span></span> | <span data-ttu-id="cebcc-155">&#8226;</span><span class="sxs-lookup"><span data-stu-id="cebcc-155">&#8226;</span></span> | | <span data-ttu-id="cebcc-156">&#8226;</span><span class="sxs-lookup"><span data-stu-id="cebcc-156">&#8226;</span></span> | <span data-ttu-id="cebcc-157">&#8226;</span><span class="sxs-lookup"><span data-stu-id="cebcc-157">&#8226;</span></span> | <span data-ttu-id="cebcc-158">&#8226;</span><span class="sxs-lookup"><span data-stu-id="cebcc-158">&#8226;</span></span> | <span data-ttu-id="cebcc-159">&#8226;</span><span class="sxs-lookup"><span data-stu-id="cebcc-159">&#8226;</span></span>| <span data-ttu-id="cebcc-160">&#8226;</span><span class="sxs-lookup"><span data-stu-id="cebcc-160">&#8226;</span></span> | <span data-ttu-id="cebcc-161">&#8226;</span><span class="sxs-lookup"><span data-stu-id="cebcc-161">&#8226;</span></span> | <span data-ttu-id="cebcc-162">&#8226;</span><span class="sxs-lookup"><span data-stu-id="cebcc-162">&#8226;</span></span> |
| <span data-ttu-id="cebcc-163">Docker</span><span class="sxs-lookup"><span data-stu-id="cebcc-163">Docker</span></span><br><span data-ttu-id="cebcc-164">Swarm</span><span class="sxs-lookup"><span data-stu-id="cebcc-164">Swarm</span></span> | <span data-ttu-id="cebcc-165">&#8226;</span><span class="sxs-lookup"><span data-stu-id="cebcc-165">&#8226;</span></span> | <span data-ttu-id="cebcc-166">&#8226;</span><span class="sxs-lookup"><span data-stu-id="cebcc-166">&#8226;</span></span> | <span data-ttu-id="cebcc-167">&#8226;</span><span class="sxs-lookup"><span data-stu-id="cebcc-167">&#8226;</span></span> | <span data-ttu-id="cebcc-168">&#8226;</span><span class="sxs-lookup"><span data-stu-id="cebcc-168">&#8226;</span></span> | <span data-ttu-id="cebcc-169">&#8226;</span><span class="sxs-lookup"><span data-stu-id="cebcc-169">&#8226;</span></span> | <span data-ttu-id="cebcc-170">&#8226;</span><span class="sxs-lookup"><span data-stu-id="cebcc-170">&#8226;</span></span> | <span data-ttu-id="cebcc-171">&#8226;</span><span class="sxs-lookup"><span data-stu-id="cebcc-171">&#8226;</span></span> | <span data-ttu-id="cebcc-172">&#8226;</span><span class="sxs-lookup"><span data-stu-id="cebcc-172">&#8226;</span></span> | | <span data-ttu-id="cebcc-173">&#8226;</span><span class="sxs-lookup"><span data-stu-id="cebcc-173">&#8226;</span></span> |
| <span data-ttu-id="cebcc-174">Servicio</span><span class="sxs-lookup"><span data-stu-id="cebcc-174">Service</span></span><br><span data-ttu-id="cebcc-175">Fabric</span><span class="sxs-lookup"><span data-stu-id="cebcc-175">Fabric</span></span> | | | <span data-ttu-id="cebcc-176">&#8226;</span><span class="sxs-lookup"><span data-stu-id="cebcc-176">&#8226;</span></span> | <span data-ttu-id="cebcc-177">&#8226;</span><span class="sxs-lookup"><span data-stu-id="cebcc-177">&#8226;</span></span> | <span data-ttu-id="cebcc-178">&#8226;</span><span class="sxs-lookup"><span data-stu-id="cebcc-178">&#8226;</span></span> | <span data-ttu-id="cebcc-179">&#8226;</span><span class="sxs-lookup"><span data-stu-id="cebcc-179">&#8226;</span></span> | <span data-ttu-id="cebcc-180">&#8226;</span><span class="sxs-lookup"><span data-stu-id="cebcc-180">&#8226;</span></span> | <span data-ttu-id="cebcc-181">&#8226;</span><span class="sxs-lookup"><span data-stu-id="cebcc-181">&#8226;</span></span> | <span data-ttu-id="cebcc-182">&#8226;</span><span class="sxs-lookup"><span data-stu-id="cebcc-182">&#8226;</span></span> | <span data-ttu-id="cebcc-183">&#8226;</span><span class="sxs-lookup"><span data-stu-id="cebcc-183">&#8226;</span></span> |
| <span data-ttu-id="cebcc-184">Red Hat Open</span><span class="sxs-lookup"><span data-stu-id="cebcc-184">Red Hat Open</span></span><br><span data-ttu-id="cebcc-185">Shift</span><span class="sxs-lookup"><span data-stu-id="cebcc-185">Shift</span></span> | | <span data-ttu-id="cebcc-186">&#8226;</span><span class="sxs-lookup"><span data-stu-id="cebcc-186">&#8226;</span></span> | | <span data-ttu-id="cebcc-187">&#8226;</span><span class="sxs-lookup"><span data-stu-id="cebcc-187">&#8226;</span></span> | <span data-ttu-id="cebcc-188">&#8226;</span><span class="sxs-lookup"><span data-stu-id="cebcc-188">&#8226;</span></span>| <span data-ttu-id="cebcc-189">&#8226;</span><span class="sxs-lookup"><span data-stu-id="cebcc-189">&#8226;</span></span> | <span data-ttu-id="cebcc-190">&#8226;</span><span class="sxs-lookup"><span data-stu-id="cebcc-190">&#8226;</span></span> | <span data-ttu-id="cebcc-191">&#8226;</span><span class="sxs-lookup"><span data-stu-id="cebcc-191">&#8226;</span></span> | | <span data-ttu-id="cebcc-192">&#8226;</span><span class="sxs-lookup"><span data-stu-id="cebcc-192">&#8226;</span></span> |
| <span data-ttu-id="cebcc-193">Windows Server</span><span class="sxs-lookup"><span data-stu-id="cebcc-193">Windows Server</span></span><br><span data-ttu-id="cebcc-194">(independiente)</span><span class="sxs-lookup"><span data-stu-id="cebcc-194">(standalone)</span></span> | | | <span data-ttu-id="cebcc-195">&#8226;</span><span class="sxs-lookup"><span data-stu-id="cebcc-195">&#8226;</span></span> | <span data-ttu-id="cebcc-196">&#8226;</span><span class="sxs-lookup"><span data-stu-id="cebcc-196">&#8226;</span></span> | <span data-ttu-id="cebcc-197">&#8226;</span><span class="sxs-lookup"><span data-stu-id="cebcc-197">&#8226;</span></span> | <span data-ttu-id="cebcc-198">&#8226;</span><span class="sxs-lookup"><span data-stu-id="cebcc-198">&#8226;</span></span> | <span data-ttu-id="cebcc-199">&#8226;</span><span class="sxs-lookup"><span data-stu-id="cebcc-199">&#8226;</span></span> | <span data-ttu-id="cebcc-200">&#8226;</span><span class="sxs-lookup"><span data-stu-id="cebcc-200">&#8226;</span></span> | | <span data-ttu-id="cebcc-201">&#8226;</span><span class="sxs-lookup"><span data-stu-id="cebcc-201">&#8226;</span></span> |
| <span data-ttu-id="cebcc-202">Linux Server</span><span class="sxs-lookup"><span data-stu-id="cebcc-202">Linux Server</span></span><br><span data-ttu-id="cebcc-203">(independiente)</span><span class="sxs-lookup"><span data-stu-id="cebcc-203">(standalone)</span></span> | | <span data-ttu-id="cebcc-204">&#8226;</span><span class="sxs-lookup"><span data-stu-id="cebcc-204">&#8226;</span></span> | | <span data-ttu-id="cebcc-205">&#8226;</span><span class="sxs-lookup"><span data-stu-id="cebcc-205">&#8226;</span></span> | <span data-ttu-id="cebcc-206">&#8226;</span><span class="sxs-lookup"><span data-stu-id="cebcc-206">&#8226;</span></span> | <span data-ttu-id="cebcc-207">&#8226;</span><span class="sxs-lookup"><span data-stu-id="cebcc-207">&#8226;</span></span> | <span data-ttu-id="cebcc-208">&#8226;</span><span class="sxs-lookup"><span data-stu-id="cebcc-208">&#8226;</span></span> | <span data-ttu-id="cebcc-209">&#8226;</span><span class="sxs-lookup"><span data-stu-id="cebcc-209">&#8226;</span></span> | | <span data-ttu-id="cebcc-210">&#8226;</span><span class="sxs-lookup"><span data-stu-id="cebcc-210">&#8226;</span></span> |


### <a name="docker-versions-supported-on-linux"></a><span data-ttu-id="cebcc-211">Versiones de docker admitidas en Linux</span><span class="sxs-lookup"><span data-stu-id="cebcc-211">Docker versions supported on Linux</span></span>

- <span data-ttu-id="cebcc-212">Docker de 1.11 a 1.13</span><span class="sxs-lookup"><span data-stu-id="cebcc-212">Docker 1.11 to 1.13</span></span>
- <span data-ttu-id="cebcc-213">Docker CE y EE v17.06</span><span class="sxs-lookup"><span data-stu-id="cebcc-213">Docker CE and EE v17.06</span></span>

### <a name="x64-linux-distributions-supported-as-container-hosts"></a><span data-ttu-id="cebcc-214">Las distribuciones x64 de Linux se admiten como hosts de contenedor</span><span class="sxs-lookup"><span data-stu-id="cebcc-214">x64 Linux distributions supported as container hosts</span></span>

- <span data-ttu-id="cebcc-215">Ubuntu 14.04 LTS y 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="cebcc-215">Ubuntu 14.04 LTS and 16.04 LTS</span></span>
- <span data-ttu-id="cebcc-216">CoreOS(stable)</span><span class="sxs-lookup"><span data-stu-id="cebcc-216">CoreOS(stable)</span></span>
- <span data-ttu-id="cebcc-217">Amazon Linux 2016.09.0</span><span class="sxs-lookup"><span data-stu-id="cebcc-217">Amazon Linux 2016.09.0</span></span>
- <span data-ttu-id="cebcc-218">openSUSE 13.2</span><span class="sxs-lookup"><span data-stu-id="cebcc-218">openSUSE 13.2</span></span>
- <span data-ttu-id="cebcc-219">openSUSE LEAP 42.2</span><span class="sxs-lookup"><span data-stu-id="cebcc-219">openSUSE LEAP 42.2</span></span>
- <span data-ttu-id="cebcc-220">CentOS 7.2 y 7.3</span><span class="sxs-lookup"><span data-stu-id="cebcc-220">CentOS 7.2 and 7.3</span></span>
- <span data-ttu-id="cebcc-221">SLES 12</span><span class="sxs-lookup"><span data-stu-id="cebcc-221">SLES 12</span></span>
- <span data-ttu-id="cebcc-222">RHEL 7.2 y 7.3</span><span class="sxs-lookup"><span data-stu-id="cebcc-222">RHEL 7.2 and 7.3</span></span>
- <span data-ttu-id="cebcc-223">Red Hat OpenShift Container Platform (OCP) 3.4 y 3.5</span><span class="sxs-lookup"><span data-stu-id="cebcc-223">Red Hat OpenShift Container Platform (OCP) 3.4 and 3.5</span></span>
- <span data-ttu-id="cebcc-224">ACS Mesosphere DC/OS 1.7.3 a 1.8.8</span><span class="sxs-lookup"><span data-stu-id="cebcc-224">ACS Mesosphere DC/OS 1.7.3 to 1.8.8</span></span>
- <span data-ttu-id="cebcc-225">ACS Kubernetes 1.4.5 a 1.6</span><span class="sxs-lookup"><span data-stu-id="cebcc-225">ACS Kubernetes 1.4.5 to 1.6</span></span>
- <span data-ttu-id="cebcc-226">ACS Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="cebcc-226">ACS Docker Swarm</span></span>

### <a name="supported-windows-operating-system"></a><span data-ttu-id="cebcc-227">Sistemas operativos Windows compatibles</span><span class="sxs-lookup"><span data-stu-id="cebcc-227">Supported Windows operating system</span></span>

- <span data-ttu-id="cebcc-228">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="cebcc-228">Windows Server 2016</span></span>
- <span data-ttu-id="cebcc-229">Windows 10 Anniversary Edition (Professional o Enterprise)</span><span class="sxs-lookup"><span data-stu-id="cebcc-229">Windows 10 Anniversary Edition (Professional or Enterprise)</span></span>

### <a name="docker-versions-supported-on-windows"></a><span data-ttu-id="cebcc-230">Versiones de docker admitidas en Windows</span><span class="sxs-lookup"><span data-stu-id="cebcc-230">Docker versions supported on Windows</span></span>

- <span data-ttu-id="cebcc-231">Docker de 1.12 y 1.13</span><span class="sxs-lookup"><span data-stu-id="cebcc-231">Docker 1.12 and 1.13</span></span>
- <span data-ttu-id="cebcc-232">Docker 17.03.0 y versiones posteriores</span><span class="sxs-lookup"><span data-stu-id="cebcc-232">Docker 17.03.0 and later</span></span>

## <a name="installing-and-configuring-the-solution"></a><span data-ttu-id="cebcc-233">Instalación y configuración de la solución</span><span class="sxs-lookup"><span data-stu-id="cebcc-233">Installing and configuring the solution</span></span>
<span data-ttu-id="cebcc-234">Utilice la siguiente información para instalar y configurar la solución.</span><span class="sxs-lookup"><span data-stu-id="cebcc-234">Use the following information to install and configure the solution.</span></span>

1. <span data-ttu-id="cebcc-235">Agregue la solución de Supervisión de contenedores al área de trabajo de OMS desde [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.ContainersOMS?tab=Overview) o mediante el proceso descrito en [Agregación de soluciones de Log Analytics desde la Galería de soluciones](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="cebcc-235">Add the Container Monitoring solution to your OMS workspace from [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.ContainersOMS?tab=Overview) or by using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span>

2. <span data-ttu-id="cebcc-236">Instalación y uso de Docker con un agente de OMS.</span><span class="sxs-lookup"><span data-stu-id="cebcc-236">Install and use Docker with an OMS agent.</span></span>  <span data-ttu-id="cebcc-237">Según el sistema operativo, puede elegir entre los siguientes métodos:</span><span class="sxs-lookup"><span data-stu-id="cebcc-237">Based on your operating system, you can choose from the following methods:</span></span>

  * <span data-ttu-id="cebcc-238">En sistemas operativos compatibles con Linux, instale y ejecute Docker y, después, instale y configure el [Agente de OMS para Linux](log-analytics-agent-linux.md).</span><span class="sxs-lookup"><span data-stu-id="cebcc-238">On supported Linux operating systems, install and run Docker and then install and configure the [OMS Agent for Linux](log-analytics-agent-linux.md).</span></span>  
  * <span data-ttu-id="cebcc-239">En CoreOS, no se puede ejecutar el agente de OMS para Linux.</span><span class="sxs-lookup"><span data-stu-id="cebcc-239">On CoreOS, you cannot run the OMS Agent for Linux.</span></span> <span data-ttu-id="cebcc-240">En su lugar, ejecute una versión en contenedores del agente de OMS para Linux.</span><span class="sxs-lookup"><span data-stu-id="cebcc-240">Instead, you run a containerized version of the OMS Agent for Linux.</span></span> <span data-ttu-id="cebcc-241">Repase las secciones [Hosts de contenedores de Linux incluido CoreOS](#for-all-linux-container-hosts-including-coreos) o [Hosts de contenedores de Azure Government Linux incluidos CoreOS](#for-all-azure-government-linux-container-hosts-including-coreos) si va a trabajar con contenedores en la nube de Azure Government.</span><span class="sxs-lookup"><span data-stu-id="cebcc-241">Review [Linux container hosts including CoreOS](#for-all-linux-container-hosts-including-coreos) or [Azure Government Linux container hosts including CoreOS](#for-all-azure-government-linux-container-hosts-including-coreos) if you are working with containers in Azure Government Cloud.</span></span>
  * <span data-ttu-id="cebcc-242">En Windows Server 2016 y Windows 10, instale el cliente de Docker y Docker Engine y luego conecte un agente para recopilar información y enviarla a Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="cebcc-242">On Windows Server 2016 and Windows 10, install the Docker Engine and client then connect an agent to gather information and send it to Log Analytics.</span></span>  

### <a name="container-services"></a><span data-ttu-id="cebcc-243">Servicios de contenedor</span><span class="sxs-lookup"><span data-stu-id="cebcc-243">Container services</span></span>

- <span data-ttu-id="cebcc-244">Si tiene un entorno de Red Hat OpenShift, consulte [Configuración de un agente de OMS para Red Hat OpenShift](#configure-an-oms-agent-for-red-hat-openshift).</span><span class="sxs-lookup"><span data-stu-id="cebcc-244">If you have a Red Hat OpenShift environment, review [Configure an OMS agent for Red Hat OpenShift](#configure-an-oms-agent-for-red-hat-openshift).</span></span>
- <span data-ttu-id="cebcc-245">Si tiene un clúster de Kubernetes con Azure Container Service, consulte [Supervisión de un clúster de Azure Container Service con Microsoft Operations Management Suite (OMS)](../container-service/kubernetes/container-service-kubernetes-oms.md).</span><span class="sxs-lookup"><span data-stu-id="cebcc-245">If you have a Kubernetes cluster using the Azure Container Service, review [Monitor an Azure Container Service cluster with Microsoft Operations Management Suite (OMS)](../container-service/kubernetes/container-service-kubernetes-oms.md).</span></span>
- <span data-ttu-id="cebcc-246">Si tiene un clúster DC/OS de Azure Container Service, obtenga más información en [Monitor an Azure Container Service DC/OS cluster with Operations Management Suite](../container-service/dcos-swarm/container-service-monitoring-oms.md) (Uso de Operations Management Suite para supervisar un clúster DC/OS de Azure Container Service).</span><span class="sxs-lookup"><span data-stu-id="cebcc-246">If you have an Azure Container Service DC/OS cluster, learn more at [Monitor an Azure Container Service DC/OS cluster with Operations Management Suite](../container-service/dcos-swarm/container-service-monitoring-oms.md).</span></span>
- <span data-ttu-id="cebcc-247">Si tiene un entorno en modo Docker Swarm, obtenga más información en [Configuración de un agente de OMS para Docker Swarm](#configure-an-oms-agent-for-docker-swarm).</span><span class="sxs-lookup"><span data-stu-id="cebcc-247">If you have a Docker Swarm mode environment, learn more at [Configure an OMS agent for Docker Swarm](#configure-an-oms-agent-for-docker-swarm).</span></span>
- <span data-ttu-id="cebcc-248">Si usa contenedores con Service Fabric, obtenga más información en [Información general de Azure Service Fabric ](../service-fabric/service-fabric-overview.md).</span><span class="sxs-lookup"><span data-stu-id="cebcc-248">If you use containers with Service Fabric, learn more at [Overview of Azure Service Fabric](../service-fabric/service-fabric-overview.md).</span></span>
- <span data-ttu-id="cebcc-249">Revise el artículo [Docker Engine en Windows](https://docs.microsoft.com/virtualization/windowscontainers/manage-docker/configure-docker-daemon) para obtener información adicional sobre cómo instalar y configurar Docker Engine en equipos con Windows.</span><span class="sxs-lookup"><span data-stu-id="cebcc-249">Review the [Docker Engine on Windows](https://docs.microsoft.com/virtualization/windowscontainers/manage-docker/configure-docker-daemon) article for additional information about how to install and configure your Docker Engines on computers running Windows.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cebcc-250">Docker se debe estar ejecutando **antes de** instalar el [agente de OMS para Linux](log-analytics-agent-linux.md) en los hosts de contenedores.</span><span class="sxs-lookup"><span data-stu-id="cebcc-250">Docker must be running **before** you install the [OMS Agent for Linux](log-analytics-agent-linux.md) on your container hosts.</span></span> <span data-ttu-id="cebcc-251">Si ya ha instalado el agente antes de instalar Docker, debe volver a instalar el agente de OMS para Linux.</span><span class="sxs-lookup"><span data-stu-id="cebcc-251">If you've already installed the agent before installing Docker, you need to reinstall the OMS Agent for Linux.</span></span> <span data-ttu-id="cebcc-252">Para más información acerca de Docker, consulte el [sitio web de Docker](https://www.docker.com).</span><span class="sxs-lookup"><span data-stu-id="cebcc-252">For more information about Docker, see the [Docker website](https://www.docker.com).</span></span>


## <a name="linux-container-hosts"></a><span data-ttu-id="cebcc-253">Hosts de contenedores de Linux</span><span class="sxs-lookup"><span data-stu-id="cebcc-253">Linux container hosts</span></span>

<span data-ttu-id="cebcc-254">Después de instalar Docker, use la siguientes opciones para el host de contenedores para configurar el agente que se usará con Docker.</span><span class="sxs-lookup"><span data-stu-id="cebcc-254">After you've installed Docker, use the following settings for your container host to configure the agent for use with Docker.</span></span> <span data-ttu-id="cebcc-255">En primer lugar necesita el identificador y la clave del área de trabajo de OMS, que puede encontrar en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="cebcc-255">First you need your OMS workspace ID and key, which you can find in the Azure portal.</span></span> <span data-ttu-id="cebcc-256">En el área de trabajo, haga clic en **Inicio rápido** > **Equipos** para ver el **Id. de área de trabajo** y la **Clave principal**.</span><span class="sxs-lookup"><span data-stu-id="cebcc-256">In your workspace, click **Quick Start** > **Computers** to view your **Workspace ID** and **Primary Key**.</span></span>  <span data-ttu-id="cebcc-257">Copie y pegue ambos valores en el editor que prefiera.</span><span class="sxs-lookup"><span data-stu-id="cebcc-257">Copy and paste both into your favorite editor.</span></span>

### <a name="for-all-linux-container-hosts-except-coreos"></a><span data-ttu-id="cebcc-258">Para todos los hosts de contenedores de Linux excepto CoreOS</span><span class="sxs-lookup"><span data-stu-id="cebcc-258">For all Linux container hosts except CoreOS</span></span>

- <span data-ttu-id="cebcc-259">Para más información sobre cómo instalar el Agente de OMS para Linux, consulte [Conexión de equipos Linux a Operations Management Suite (OMS)](log-analytics-agent-linux.md).</span><span class="sxs-lookup"><span data-stu-id="cebcc-259">For more information and steps on how to install the OMS Agent for Linux, see [Connect your Linux Computers to Operations Management Suite (OMS)](log-analytics-agent-linux.md).</span></span>

### <a name="for-all-linux-container-hosts-including-coreos"></a><span data-ttu-id="cebcc-260">Para todos los hosts de contenedores de Linux incluido CoreOS</span><span class="sxs-lookup"><span data-stu-id="cebcc-260">For all Linux container hosts including CoreOS</span></span>

<span data-ttu-id="cebcc-261">Inicie el contenedor de OMS que desea supervisar.</span><span class="sxs-lookup"><span data-stu-id="cebcc-261">Start the OMS container that you want to monitor.</span></span> <span data-ttu-id="cebcc-262">Modifique y use el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="cebcc-262">Modify and use the following example:</span></span>

```
sudo docker run --privileged -d -v /var/run/docker.sock:/var/run/docker.sock -e WSID="your workspace id" -e KEY="your key" -h=`hostname` -p 127.0.0.1:25225:25225 --name="omsagent" --restart=always microsoft/oms
```

### <a name="for-all-azure-government-linux-container-hosts-including-coreos"></a><span data-ttu-id="cebcc-263">Para todos los hosts de contenedores de Linux para Azure Government, incluido CoreOS</span><span class="sxs-lookup"><span data-stu-id="cebcc-263">For all Azure Government Linux container hosts including CoreOS</span></span>

<span data-ttu-id="cebcc-264">Inicie el contenedor de OMS que desea supervisar.</span><span class="sxs-lookup"><span data-stu-id="cebcc-264">Start the OMS container that you want to monitor.</span></span> <span data-ttu-id="cebcc-265">Modifique y use el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="cebcc-265">Modify and use the following example:</span></span>

```
sudo docker run --privileged -d -v /var/run/docker.sock:/var/run/docker.sock -v /var/log:/var/log -e WSID="your workspace id" -e KEY="your key" -e DOMAIN="opinsights.azure.us" -p 127.0.0.1:25225:25225 -p 127.0.0.1:25224:25224/udp --name="omsagent" -h=`hostname` --restart=always microsoft/oms
```

### <a name="switching-from-using-an-installed-linux-agent-to-one-in-a-container"></a><span data-ttu-id="cebcc-266">Cambio de un agente de Linux instalado a un agente en un contenedor</span><span class="sxs-lookup"><span data-stu-id="cebcc-266">Switching from using an installed Linux agent to one in a container</span></span>
<span data-ttu-id="cebcc-267">Si antes usaba el agente instalado directamente y ahora desea usar un agente que se ejecuta en un contenedor, primero debe quitar el Agente de OMS para Linux.</span><span class="sxs-lookup"><span data-stu-id="cebcc-267">If you previously used the directly-installed agent and want to instead use an agent running in a container, you must first remove the OMS Agent for Linux.</span></span> <span data-ttu-id="cebcc-268">Consulte [Desinstalación del agente de OMS para Linux](log-analytics-agent-linux.md#uninstalling-the-oms-agent-for-linux) para aprender a desinstalar correctamente el agente.</span><span class="sxs-lookup"><span data-stu-id="cebcc-268">See [Uninstalling the OMS Agent for Linux](log-analytics-agent-linux.md#uninstalling-the-oms-agent-for-linux) to understand how to successfully uninstall the agent.</span></span>  

### <a name="configure-an-oms-agent-for-docker-swarm"></a><span data-ttu-id="cebcc-269">Configuración de un agente de OMS para Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="cebcc-269">Configure an OMS agent for Docker Swarm</span></span>

<span data-ttu-id="cebcc-270">Puede ejecutar el agente de OMS como un servicio global en Docker Swarm.</span><span class="sxs-lookup"><span data-stu-id="cebcc-270">You can run the OMS Agent as a global service on Docker Swarm.</span></span> <span data-ttu-id="cebcc-271">Use la información siguiente para crear un servicio de agente de OMS.</span><span class="sxs-lookup"><span data-stu-id="cebcc-271">Use the following information to create an OMS Agent service.</span></span> <span data-ttu-id="cebcc-272">Debe insertar el identificador de área de trabajo y la clave principal de OMS.</span><span class="sxs-lookup"><span data-stu-id="cebcc-272">You need to insert your OMS Workspace ID and Primary Key.</span></span>

- <span data-ttu-id="cebcc-273">Ejecute lo siguiente en el nodo principal.</span><span class="sxs-lookup"><span data-stu-id="cebcc-273">Run the following on the master node.</span></span>

    ```
    sudo docker service create  --name omsagent --mode global  --mount type=bind,source=/var/run/docker.sock,destination=/var/run/docker.sock  -e WSID="<WORKSPACE ID>" -e KEY="<PRIMARY KEY>" -p 25225:25225 -p 25224:25224/udp  --restart-condition=on-failure microsoft/oms
    ```

### <a name="configure-an-oms-agent-for-red-hat-openshift"></a><span data-ttu-id="cebcc-274">Configuración de un agente de OMS para Red Hat OpenShift</span><span class="sxs-lookup"><span data-stu-id="cebcc-274">Configure an OMS Agent for Red Hat OpenShift</span></span>
<span data-ttu-id="cebcc-275">Hay tres maneras de agregar el agente de OMS a Red Hat OpenShift para comenzar a recopilar datos de supervisión de contenedores.</span><span class="sxs-lookup"><span data-stu-id="cebcc-275">There are three ways to add the OMS Agent to Red Hat OpenShift to start collecting container monitoring data.</span></span>

* <span data-ttu-id="cebcc-276">[Instalación del agente de OMS para Linux](log-analytics-agent-linux.md) directamente en cada nodo OpenShift</span><span class="sxs-lookup"><span data-stu-id="cebcc-276">[Install the OMS Agent for Linux](log-analytics-agent-linux.md) directly on each OpenShift node</span></span>  
* <span data-ttu-id="cebcc-277">[Habilitar la extensión de máquina virtual de Log Analytics](log-analytics-azure-vm-extension.md) en cada nodo de OpenShift que reside en Azure</span><span class="sxs-lookup"><span data-stu-id="cebcc-277">[Enable Log Analytics VM Extension](log-analytics-azure-vm-extension.md) on each OpenShift node residing in Azure</span></span>  
* <span data-ttu-id="cebcc-278">Instalación del agente de OMS como daemon-set de OpenShift</span><span class="sxs-lookup"><span data-stu-id="cebcc-278">Install the OMS Agent as a OpenShift daemon-set</span></span>  

<span data-ttu-id="cebcc-279">En esta sección trataremos los pasos necesarios para instalar al agente de OMS como daemon-set de OpenShift.</span><span class="sxs-lookup"><span data-stu-id="cebcc-279">In this section we cover the steps required to install the OMS Agent as an OpenShift daemon-set.</span></span>  

1. <span data-ttu-id="cebcc-280">Inicie sesión en el nodo principal de OpenShift y copie el archivo yaml [ocp-omsagent.yaml](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-omsagent.yaml) desde GitHub en el nodo principal y modifique el valor con el identificador del área de trabajo de OMS y con la clave principal.</span><span class="sxs-lookup"><span data-stu-id="cebcc-280">Sign on to the OpenShift master node and copy the yaml file [ocp-omsagent.yaml](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-omsagent.yaml) from GitHub to your master node and modify the value with your OMS Workspace ID and with your Primary Key.</span></span>
2. <span data-ttu-id="cebcc-281">Ejecute los comandos siguientes para crear un proyecto para OMS y establecer la cuenta de usuario.</span><span class="sxs-lookup"><span data-stu-id="cebcc-281">Run the following commands to create a project for OMS and set the user account.</span></span>

    ```
    oadm new-project omslogging --node-selector='zone=default'
    oc project omslogging  
    oc create serviceaccount omsagent  
    oadm policy add-cluster-role-to-user cluster-reader   system:serviceaccount:omslogging:omsagent  
    oadm policy add-scc-to-user privileged system:serviceaccount:omslogging:omsagent  
    ```

4. <span data-ttu-id="cebcc-282">Para implementar daemon-set, ejecute lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="cebcc-282">To deploy the daemon-set, run the following:</span></span>

    `oc create -f ocp-omsagent.yaml`

5. <span data-ttu-id="cebcc-283">Para comprobar que se ha configurado y funciona correctamente, escriba lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="cebcc-283">To verify it is configured and working correctly, type the following:</span></span>

    `oc describe daemonset omsagent`  

    <span data-ttu-id="cebcc-284">y la salida debería ser similar a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="cebcc-284">and the output should resemble:</span></span>

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

<span data-ttu-id="cebcc-285">Si desea utilizar secretos para proteger el identificador del área de trabajo y la clave principal de OMS al usar el archivo yaml de daemon-set del agente de OMS, realice los siguientes pasos.</span><span class="sxs-lookup"><span data-stu-id="cebcc-285">If you want to use secrets to secure your OMS Workspace ID and Primary Key when using the OMS Agent daemon-set yaml file, perform the following steps.</span></span>

1. <span data-ttu-id="cebcc-286">Inicie sesión en el nodo principal de OpenShift y copie el archivo yaml [ocp-ds-omsagent.yaml](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-ds-omsagent.yaml) y el script de generación de secretos [ocp-secretgen.sh](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-secretgen.sh) de GitHub.</span><span class="sxs-lookup"><span data-stu-id="cebcc-286">Sign on to the OpenShift master node and copy the yaml file [ocp-ds-omsagent.yaml](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-ds-omsagent.yaml) and secret generating script [ocp-secretgen.sh](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-secretgen.sh) from GitHub.</span></span>  <span data-ttu-id="cebcc-287">Este script generará el archivo yaml de secretos para el identificador del área de trabajo y la clave principal de OMS.</span><span class="sxs-lookup"><span data-stu-id="cebcc-287">This script will generate the secrets yaml file for OMS Workspace ID and Primary Key to secure your secrete information.</span></span>  
2. <span data-ttu-id="cebcc-288">Ejecute los comandos siguientes para crear un proyecto para OMS y establecer la cuenta de usuario.</span><span class="sxs-lookup"><span data-stu-id="cebcc-288">Run the following commands to create a project for OMS and set the user account.</span></span> <span data-ttu-id="cebcc-289">El script de generación de secretos le pedirá el identificador del área de trabajo <WSID> y la clave principal <KEY> y, al terminar, creará el archivo ocp-secret.yaml.</span><span class="sxs-lookup"><span data-stu-id="cebcc-289">The secret generating script asks for your OMS Workspace ID <WSID> and Primary Key <KEY> and upon completion, it creates the ocp-secret.yaml file.</span></span>  

    ```
    oadm new-project omslogging --node-selector='zone=default'  
    oc project omslogging  
    oc create serviceaccount omsagent  
    oadm policy add-cluster-role-to-user cluster-reader   system:serviceaccount:omslogging:omsagent  
    oadm policy add-scc-to-user privileged system:serviceaccount:omslogging:omsagent  
    ```

4. <span data-ttu-id="cebcc-290">Implemente el archivo de secretos ejecutando lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="cebcc-290">Deploy the secret file by running the following:</span></span>

    `oc create -f ocp-secret.yaml`

5. <span data-ttu-id="cebcc-291">Compruebe la implementación ejecutando lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="cebcc-291">Verify deployment by running the following:</span></span>

    `oc describe secret omsagent-secret`  

    <span data-ttu-id="cebcc-292">y la salida debería ser similar a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="cebcc-292">and the  output should resemble:</span></span>  

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

6. <span data-ttu-id="cebcc-293">Implemente el archivo yaml de daemon-set del agente de OMS ejecutando lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="cebcc-293">Deploy the OMS Agent daemon-set yaml file by running the following:</span></span>

    `oc create -f ocp-ds-omsagent.yaml`  

7. <span data-ttu-id="cebcc-294">Compruebe la implementación ejecutando lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="cebcc-294">Verify deployment by running the following:</span></span>

    `oc describe ds oms`

    <span data-ttu-id="cebcc-295">y la salida debería ser similar a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="cebcc-295">and the output should resemble:</span></span>

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

### <a name="secure-your-secret-information-for-docker-swarm-and-kubernetes"></a><span data-ttu-id="cebcc-296">Protección de la información secreta para Docker Swarm y Kubernetes</span><span class="sxs-lookup"><span data-stu-id="cebcc-296">Secure your secret information for Docker Swarm and Kubernetes</span></span>

<span data-ttu-id="cebcc-297">Puede proteger el identificador de área de trabajo y las claves principales de OMS para los servicios de contenedor de Docker Swarm y Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="cebcc-297">You can secure your secret OMS Workspace ID and Primary Keys for Docker Swarm and Kubernetes container services.</span></span>

#### <a name="secure-secrets-for-docker-swarm"></a><span data-ttu-id="cebcc-298">Protección de secretos de Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="cebcc-298">Secure secrets for Docker Swarm</span></span>

<span data-ttu-id="cebcc-299">Para Docker Swarm, una vez que se crea el secreto para el identificador de área de trabajo y la clave principal, puede ejecutar la creación del servicio Docker para OMSagent.</span><span class="sxs-lookup"><span data-stu-id="cebcc-299">For Docker Swarm, once the secret for Workspace ID and Primary Key is created, you can run the create the Docker service for OMSagent.</span></span> <span data-ttu-id="cebcc-300">Use la información siguiente para crear la información secreta.</span><span class="sxs-lookup"><span data-stu-id="cebcc-300">Use the following information to create your secret information.</span></span>

1. <span data-ttu-id="cebcc-301">Ejecute lo siguiente en el nodo principal.</span><span class="sxs-lookup"><span data-stu-id="cebcc-301">Run the following on the master node.</span></span>

    ```
    echo "WSID" | docker secret create WSID -
    echo "KEY" | docker secret create KEY -
    ```

2. <span data-ttu-id="cebcc-302">Compruebe que los secretos se crearon correctamente.</span><span class="sxs-lookup"><span data-stu-id="cebcc-302">Verify that secrets were created properly.</span></span>

    ```
    keiko@swarmm-master-13957614-0:/run# sudo docker secret ls
    ```

    ```
    ID                          NAME                CREATED             UPDATED
    j2fj153zxy91j8zbcitnjxjiv   WSID                43 minutes ago      43 minutes ago
    l9rh3n987g9c45zffuxdxetd9   KEY                 38 minutes ago      38 minutes ago
    ```

3. <span data-ttu-id="cebcc-303">Ejecute el comando siguiente para montar los secretos en el agente de OMS en contenedores.</span><span class="sxs-lookup"><span data-stu-id="cebcc-303">Run the following command to mount the secrets to the containerized OMS Agent.</span></span>

    ```
    sudo docker service create  --name omsagent --mode global  --mount type=bind,source=/var/run/docker.sock,destination=/var/run/docker.sock --secret source=WSID,target=WSID --secret source=KEY,target=KEY  -p 25225:25225 -p 25224:25224/udp --restart-condition=on-failure microsoft/oms
    ```

#### <a name="secure-secrets-for-kubernetes-with-yaml-files"></a><span data-ttu-id="cebcc-304">Protección de secretos de Kubernetes con archivos yaml</span><span class="sxs-lookup"><span data-stu-id="cebcc-304">Secure secrets for Kubernetes with yaml files</span></span>

<span data-ttu-id="cebcc-305">Para Kubernetes, se usa un script para generar el archivo .yaml de secretos para el identificador de área de trabajo y la clave principal.</span><span class="sxs-lookup"><span data-stu-id="cebcc-305">For Kubernetes, you use a script to generate the secrets yaml file for your Workspace ID and Primary Key.</span></span> <span data-ttu-id="cebcc-306">En la página [OMS Docker Kubernetes GitHub](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes), hay archivos que se pueden usar con o sin la información secreta.</span><span class="sxs-lookup"><span data-stu-id="cebcc-306">At the [OMS Docker Kubernetes GitHub](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes) page, there are files that you can use with or without your secret information.</span></span>

- <span data-ttu-id="cebcc-307">El DaemonSet del agente de OMS predeterminado no tiene información secreta (omsagent.yaml)</span><span class="sxs-lookup"><span data-stu-id="cebcc-307">The Default OMS Agent DaemonSet does not have secret information (omsagent.yaml)</span></span>
- <span data-ttu-id="cebcc-308">El archivo yaml del DaemonSet del agente de OMS usa información secreta (omsagent-ds-secrets.yaml) con scripts de generación de secretos que genera el archivo yaml (omsagentsecret.yaml) de secretos.</span><span class="sxs-lookup"><span data-stu-id="cebcc-308">The OMS Agent DaemonSet yaml file uses secret information (omsagent-ds-secrets.yaml) with secret generation scripts to generate the secrets yaml (omsagentsecret.yaml) file.</span></span>

<span data-ttu-id="cebcc-309">Puede elegir crear DaemonSets de omsagent con o sin secretos.</span><span class="sxs-lookup"><span data-stu-id="cebcc-309">You can choose to create omsagent DaemonSets with or without secrets.</span></span>

##### <a name="default-omsagent-daemonset-yaml-file-without-secrets"></a><span data-ttu-id="cebcc-310">Archivo yaml de DaemonSet de OMSagent predeterminado sin secretos</span><span class="sxs-lookup"><span data-stu-id="cebcc-310">Default OMSagent DaemonSet yaml file without secrets</span></span>

- <span data-ttu-id="cebcc-311">Para el archivo yaml de DaemonSet del agente de OMS predeterminado, reemplace `<WSID>` y `<KEY>` por su WSID y KEY.</span><span class="sxs-lookup"><span data-stu-id="cebcc-311">For the default OMS Agent DaemonSet yaml file, replace the `<WSID>` and `<KEY>` to your WSID and KEY.</span></span> <span data-ttu-id="cebcc-312">Copie el archivo en el nodo principal y ejecute lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="cebcc-312">Copy the file to your master node and run the following:</span></span>

    ```
    sudo kubectl create -f omsagent.yaml
    ```

##### <a name="default-omsagent-daemonset-yaml-file-with-secrets"></a><span data-ttu-id="cebcc-313">Archivo yaml de DaemonSet de OMSagent predeterminado con secretos</span><span class="sxs-lookup"><span data-stu-id="cebcc-313">Default OMSagent DaemonSet yaml file with secrets</span></span>

1. <span data-ttu-id="cebcc-314">Para usar DaemonSet del agente de OMS con información secreta, primero cree los secretos.</span><span class="sxs-lookup"><span data-stu-id="cebcc-314">To use OMS Agent DaemonSet using secret information, create the secrets first.</span></span>
    1. <span data-ttu-id="cebcc-315">Copie el script y el archivo de plantilla secreto y asegúrese de que estén en el mismo directorio.</span><span class="sxs-lookup"><span data-stu-id="cebcc-315">Copy the script and secret template file and make sure they are on the same directory.</span></span>
        - <span data-ttu-id="cebcc-316">Script de generación de secretos: secret-gen.sh</span><span class="sxs-lookup"><span data-stu-id="cebcc-316">Secret generating script - secret-gen.sh</span></span>
        - <span data-ttu-id="cebcc-317">Plantilla de secretos: secret-template.yaml</span><span class="sxs-lookup"><span data-stu-id="cebcc-317">secret template - secret-template.yaml</span></span>
    2. <span data-ttu-id="cebcc-318">Ejecute el script, como en el ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="cebcc-318">Run the script, like the following example.</span></span> <span data-ttu-id="cebcc-319">El script pide el identificador del área de trabajo y la clave principal de OMS y, una vez que los escribe, se crea un archivo .yaml secreto para que pueda ejecutarlo.</span><span class="sxs-lookup"><span data-stu-id="cebcc-319">The script asks for the OMS Workspace ID and Primary Key and after you enter them, the script creates a secret yaml file so you can run it.</span></span>   

        ```
        #> sudo bash ./secret-gen.sh
        ```

    3. <span data-ttu-id="cebcc-320">Ejecute lo siguiente para crear el pod de secretos:</span><span class="sxs-lookup"><span data-stu-id="cebcc-320">Create the secrets pod by running the following:</span></span>
        ```
        sudo kubectl create -f omsagentsecret.yaml
        ```

    4. <span data-ttu-id="cebcc-321">Para realizar una comprobación, ejecute lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="cebcc-321">To verify, run the following:</span></span>

        ```
        keiko@ubuntu16-13db:~# sudo kubectl get secrets
        ```

        <span data-ttu-id="cebcc-322">La salida debe ser similar a lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="cebcc-322">Output should resemble:</span></span>

        ```
        NAME                  TYPE                                  DATA      AGE
        default-token-gvl91   kubernetes.io/service-account-token   3         50d
        omsagent-secret       Opaque                                2         1d
        ```

        ```
        keiko@ubuntu16-13db:~# sudo kubectl describe secrets omsagent-secret
        ```

        <span data-ttu-id="cebcc-323">La salida debe ser similar a lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="cebcc-323">Output should resemble:</span></span>

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

    5. <span data-ttu-id="cebcc-324">Ejecute ``` sudo kubectl create -f omsagent-ds-secrets.yaml ``` para crear el daemon-set de omsagent</span><span class="sxs-lookup"><span data-stu-id="cebcc-324">Create your omsagent daemon-set by running ``` sudo kubectl create -f omsagent-ds-secrets.yaml ```</span></span>

2. <span data-ttu-id="cebcc-325">Compruebe que DaemonSet del agente de OMS está en ejecución, de manera similar a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="cebcc-325">Verify that the OMS Agent DaemonSet is running, similar to the following:</span></span>

    ```
    keiko@ubuntu16-13db:~# sudo kubectl get ds omsagent
    ```

    ```
    NAME       DESIRED   CURRENT   NODE-SELECTOR   AGE
    omsagent   3         3         <none>          1h
    ```


<span data-ttu-id="cebcc-326">Para Kubernetes, use un script para generar el archivo .yaml de secretos para el identificador de área de trabajo y clave principal.</span><span class="sxs-lookup"><span data-stu-id="cebcc-326">For Kubernetes, use a script to generate the secrets yaml file for Workspace ID and Primary Key.</span></span> <span data-ttu-id="cebcc-327">Use la información de ejemplo siguiente con el [archivo yaml omsagent](https://github.com/Microsoft/OMS-docker/blob/master/Kubernetes/omsagent.yaml) para proteger la información secreta.</span><span class="sxs-lookup"><span data-stu-id="cebcc-327">Use the following example information with the [omsagent yaml file](https://github.com/Microsoft/OMS-docker/blob/master/Kubernetes/omsagent.yaml) to secure your secret information.</span></span>

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

## <a name="windows-container-hosts"></a><span data-ttu-id="cebcc-328">Hosts de contenedores Windows</span><span class="sxs-lookup"><span data-stu-id="cebcc-328">Windows container hosts</span></span>

### <a name="preparation-before-installing-windows-agents"></a><span data-ttu-id="cebcc-329">Preparación antes de instalar agentes de Windows</span><span class="sxs-lookup"><span data-stu-id="cebcc-329">Preparation before installing Windows agents</span></span>

<span data-ttu-id="cebcc-330">Antes de instalar agentes en equipos con Windows, debe configurar el servicio Docker.</span><span class="sxs-lookup"><span data-stu-id="cebcc-330">Before you install agents on computers running Windows, you need to configure the Docker service.</span></span> <span data-ttu-id="cebcc-331">La configuración permite que el agente de Windows o la extensión de máquina virtual de Log Analytics utilice el socket TCP de Docker para que los agentes puedan acceder al demonio de Docker de forma remota y capturar datos para supervisión.</span><span class="sxs-lookup"><span data-stu-id="cebcc-331">The configuration allows the Windows agent or the Log Analytics virtual machine extension to use the Docker TCP socket so that the agents can access the Docker daemon remotely and to capture data for monitoring.</span></span>

#### <a name="to-start-docker-and-verify-its-configuration"></a><span data-ttu-id="cebcc-332">Para iniciar Docker y comprobar su configuración</span><span class="sxs-lookup"><span data-stu-id="cebcc-332">To start Docker and verify its configuration</span></span>

<span data-ttu-id="cebcc-333">Es necesario realiza algunos pasos para configurar la canalización con nombre TCP para Windows Server:</span><span class="sxs-lookup"><span data-stu-id="cebcc-333">There are steps needed to set up TCP named pipe for Windows Server:</span></span>

1. <span data-ttu-id="cebcc-334">En Windows PowerShell, habilite la canalización TCP y la canalización con nombre.</span><span class="sxs-lookup"><span data-stu-id="cebcc-334">In Windows PowerShell, enable TCP pipe and named pipe.</span></span>

    ```
    Stop-Service docker
    dockerd --unregister-service
    dockerd --register-service -H npipe:// -H 0.0.0.0:2375  
    Start-Service docker
    ```

2. <span data-ttu-id="cebcc-335">Configure Docker con el archivo de configuración para la canalización TCP y la canalización con nombre.</span><span class="sxs-lookup"><span data-stu-id="cebcc-335">Configure Docker with the configuration file for TCP pipe and named pipe.</span></span> <span data-ttu-id="cebcc-336">El archivo de configuración se encuentra en C:\ProgramData\docker\config\daemon.json.</span><span class="sxs-lookup"><span data-stu-id="cebcc-336">The configuration file is located at C:\ProgramData\docker\config\daemon.json.</span></span>

    <span data-ttu-id="cebcc-337">En el archivo daemon.json, necesitará lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="cebcc-337">In the daemon.json file, you will need the following:</span></span>

    ```
    {
    "hosts": ["tcp://0.0.0.0:2375", "npipe://"]
    }
    ```

<span data-ttu-id="cebcc-338">Para más información sobre la configuración del demonio de Docker usada con contenedores Windows, consulte [Docker Engine on Windows](https://docs.microsoft.com/virtualization/windowscontainers/manage-docker/configure-docker-daemon) (Docker Engine en Windows).</span><span class="sxs-lookup"><span data-stu-id="cebcc-338">For more information about the Docker daemon configuration used with Windows Containers, see [Docker Engine on Windows](https://docs.microsoft.com/virtualization/windowscontainers/manage-docker/configure-docker-daemon).</span></span>


### <a name="install-windows-agents"></a><span data-ttu-id="cebcc-339">Instalación de agentes de Windows</span><span class="sxs-lookup"><span data-stu-id="cebcc-339">Install Windows agents</span></span>

<span data-ttu-id="cebcc-340">Para habilitar la supervisión de contenedores de Hyper-V y Windows, instale Microsoft Monitoring Agent (MMA) en equipos Windows que sean hosts de contenedores.</span><span class="sxs-lookup"><span data-stu-id="cebcc-340">To enable Windows and Hyper-V container monitoring, install the Microsoft Monitoring Agent (MMA) on Windows computers that are container hosts.</span></span> <span data-ttu-id="cebcc-341">Para equipos con Windows en su entorno local, consulte [Conexión de equipos Windows a Log Analytics](log-analytics-windows-agents.md).</span><span class="sxs-lookup"><span data-stu-id="cebcc-341">For computers running Windows in your on-premises environment, see [Connect Windows computers to Log Analytics](log-analytics-windows-agents.md).</span></span> <span data-ttu-id="cebcc-342">Para máquinas virtuales que se ejecutan en Azure, conéctelas a Log Analytics mediante la [extensión de máquina virtual](log-analytics-azure-vm-extension.md).</span><span class="sxs-lookup"><span data-stu-id="cebcc-342">For virtual machines running in Azure, connect them to Log Analytics using the [virtual machine extension](log-analytics-azure-vm-extension.md).</span></span>

<span data-ttu-id="cebcc-343">Puede supervisar los contenedores de Windows que se ejecutan en Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="cebcc-343">You can monitor Windows containers running on Service Fabric.</span></span> <span data-ttu-id="cebcc-344">Sin embargo, actualmente solo las [máquinas virtuales que se ejecutan en Azure](log-analytics-azure-vm-extension.md) y en [equipos Windows de su entorno local](log-analytics-windows-agents.md) son compatibles con Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="cebcc-344">However, only [virtual machines running in Azure](log-analytics-azure-vm-extension.md) and [computers running Windows in your on-premises environment](log-analytics-windows-agents.md) are currently supported for Service Fabric.</span></span>

<span data-ttu-id="cebcc-345">Puede comprobar que la solución de Supervisión de contenedores está configurada correctamente para Windows.</span><span class="sxs-lookup"><span data-stu-id="cebcc-345">You can verify that the Container Monitoring solution is set correctly for Windows.</span></span> <span data-ttu-id="cebcc-346">Para comprobar si el módulo de administración se descargó correctamente, busque *ContainerManagement.xxx*.</span><span class="sxs-lookup"><span data-stu-id="cebcc-346">To check whether the management pack was download properly, look for *ContainerManagement.xxx*.</span></span> <span data-ttu-id="cebcc-347">Los archivos deben estar en la carpeta C:\Archivos de programa\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs.</span><span class="sxs-lookup"><span data-stu-id="cebcc-347">The files should be in the C:\Program Files\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs folder.</span></span>


## <a name="solution-components"></a><span data-ttu-id="cebcc-348">Componentes de soluciones</span><span class="sxs-lookup"><span data-stu-id="cebcc-348">Solution components</span></span>

<span data-ttu-id="cebcc-349">Si está utilizando agentes de Windows, el siguiente módulo de administración se instala en cada equipo con un agente cuando se agrega esta solución.</span><span class="sxs-lookup"><span data-stu-id="cebcc-349">If you are using Windows agents, then the following management pack is installed on each computer with an agent when you add this solution.</span></span> <span data-ttu-id="cebcc-350">No es necesario realizar tareas de configuración o mantenimiento del módulo de administración.</span><span class="sxs-lookup"><span data-stu-id="cebcc-350">No configuration or maintenance is required for the management pack.</span></span>

- <span data-ttu-id="cebcc-351">*ContainerManagement.xxx* instalado en C:\Program Files\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs</span><span class="sxs-lookup"><span data-stu-id="cebcc-351">*ContainerManagement.xxx* installed in C:\Program Files\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs</span></span>

## <a name="container-data-collection-details"></a><span data-ttu-id="cebcc-352">Información detallada sobre la recopilación de datos en contenedores</span><span class="sxs-lookup"><span data-stu-id="cebcc-352">Container data collection details</span></span>
<span data-ttu-id="cebcc-353">La solución de Supervisión de contenedores recopila diversos datos de registro y métricas de rendimiento de los hosts de contenedores y de los contenedores mediante agentes que el usuario habilita.</span><span class="sxs-lookup"><span data-stu-id="cebcc-353">The Container Monitoring solution collects various performance metrics and log data from container hosts and containers using agents that you enable.</span></span>

<span data-ttu-id="cebcc-354">Los siguientes tipos de agente recopilan los datos cada tres minutos.</span><span class="sxs-lookup"><span data-stu-id="cebcc-354">Data is collected every three minutes by the following agent types.</span></span>

- [<span data-ttu-id="cebcc-355">Agente de OMS para Linux</span><span class="sxs-lookup"><span data-stu-id="cebcc-355">OMS Agent for Linux</span></span>](log-analytics-linux-agents.md)
- [<span data-ttu-id="cebcc-356">Agente de Windows</span><span class="sxs-lookup"><span data-stu-id="cebcc-356">Windows agent</span></span>](log-analytics-windows-agents.md)
- [<span data-ttu-id="cebcc-357">Extensión de VM de Log Analytics</span><span class="sxs-lookup"><span data-stu-id="cebcc-357">Log Analytics VM extension</span></span>](log-analytics-azure-vm-extension.md)


### <a name="container-records"></a><span data-ttu-id="cebcc-358">Registros de contenedor</span><span class="sxs-lookup"><span data-stu-id="cebcc-358">Container records</span></span>

<span data-ttu-id="cebcc-359">En la tabla siguiente se muestran ejemplos de registros recopilados por la solución de Supervisión de contenedores y los tipos de datos que aparecen en los resultados de las búsquedas de registros.</span><span class="sxs-lookup"><span data-stu-id="cebcc-359">The following table shows examples of records collected by the Container Monitoring solution and the data types that appear in log search results.</span></span>

| <span data-ttu-id="cebcc-360">Tipo de datos</span><span class="sxs-lookup"><span data-stu-id="cebcc-360">Data type</span></span> | <span data-ttu-id="cebcc-361">Tipo de datos en la búsqueda de registros</span><span class="sxs-lookup"><span data-stu-id="cebcc-361">Data type in Log Search</span></span> | <span data-ttu-id="cebcc-362">Fields</span><span class="sxs-lookup"><span data-stu-id="cebcc-362">Fields</span></span> |
| --- | --- | --- |
| <span data-ttu-id="cebcc-363">Rendimiento de hosts y contenedores</span><span class="sxs-lookup"><span data-stu-id="cebcc-363">Performance for hosts and containers</span></span> | `Type=Perf` | <span data-ttu-id="cebcc-364">Computer, ObjectName, CounterName &#40;%Processor Time, Disk Reads MB, Disk Writes MB, Memory Usage MB, Network Receive Bytes, Network Send Bytes, Processor Usage sec, Network&#41;, CounterValue,TimeGenerated, CounterPath, SourceSystem</span><span class="sxs-lookup"><span data-stu-id="cebcc-364">Computer, ObjectName, CounterName &#40;%Processor Time, Disk Reads MB, Disk Writes MB, Memory Usage MB, Network Receive Bytes, Network Send Bytes, Processor Usage sec, Network&#41;, CounterValue,TimeGenerated, CounterPath, SourceSystem</span></span> |
| <span data-ttu-id="cebcc-365">Inventario de contenedor</span><span class="sxs-lookup"><span data-stu-id="cebcc-365">Container inventory</span></span> | `Type=ContainerInventory` | <span data-ttu-id="cebcc-366">TimeGenerated, Computer, container name, ContainerHostname, Image, ImageTag, ContainerState, ExitCode, EnvironmentVar, Command, CreatedTime, StartedTime, FinishedTime, SourceSystem, ContainerID, ImageID</span><span class="sxs-lookup"><span data-stu-id="cebcc-366">TimeGenerated, Computer, container name, ContainerHostname, Image, ImageTag, ContainerState, ExitCode, EnvironmentVar, Command, CreatedTime, StartedTime, FinishedTime, SourceSystem, ContainerID, ImageID</span></span> |
| <span data-ttu-id="cebcc-367">Inventario de imágenes de contenedor</span><span class="sxs-lookup"><span data-stu-id="cebcc-367">Container image inventory</span></span> | `Type=ContainerImageInventory` | <span data-ttu-id="cebcc-368">TimeGenerated, Computer, Image, ImageTag, ImageSize, VirtualSize, Running, Paused, Stopped, Failed, SourceSystem, ImageID, TotalContainer</span><span class="sxs-lookup"><span data-stu-id="cebcc-368">TimeGenerated, Computer, Image, ImageTag, ImageSize, VirtualSize, Running, Paused, Stopped, Failed, SourceSystem, ImageID, TotalContainer</span></span> |
| <span data-ttu-id="cebcc-369">Registro de contenedor</span><span class="sxs-lookup"><span data-stu-id="cebcc-369">Container log</span></span> | `Type=ContainerLog` | <span data-ttu-id="cebcc-370">TimeGenerated, Computer, image ID, container name, LogEntrySource, LogEntry, SourceSystem, ContainerID</span><span class="sxs-lookup"><span data-stu-id="cebcc-370">TimeGenerated, Computer, image ID, container name, LogEntrySource, LogEntry, SourceSystem, ContainerID</span></span> |
| <span data-ttu-id="cebcc-371">Registro del servicio de contenedores</span><span class="sxs-lookup"><span data-stu-id="cebcc-371">Container service log</span></span> | `Type=ContainerServiceLog`  | <span data-ttu-id="cebcc-372">TimeGenerated, Computer, TimeOfCommand, Image, Command, SourceSystem, ContainerID</span><span class="sxs-lookup"><span data-stu-id="cebcc-372">TimeGenerated, Computer, TimeOfCommand, Image, Command, SourceSystem, ContainerID</span></span> |
| <span data-ttu-id="cebcc-373">Inventario de nodo de contenedor</span><span class="sxs-lookup"><span data-stu-id="cebcc-373">Container node inventory</span></span> | `Type=ContainerNodeInventory_CL`| <span data-ttu-id="cebcc-374">TimeGenerated, Computer, ClassName_s, DockerVersion_s, OperatingSystem_s, Volume_s, Network_s, NodeRole_s, OrchestratorType_s, InstanceID_g, SourceSystem</span><span class="sxs-lookup"><span data-stu-id="cebcc-374">TimeGenerated, Computer, ClassName_s, DockerVersion_s, OperatingSystem_s, Volume_s, Network_s, NodeRole_s, OrchestratorType_s, InstanceID_g, SourceSystem</span></span>|
| <span data-ttu-id="cebcc-375">Inventario de Kubernetes</span><span class="sxs-lookup"><span data-stu-id="cebcc-375">Kubernetes inventory</span></span> | `Type=KubePodInventory_CL` | <span data-ttu-id="cebcc-376">TimeGenerated, Computer, PodLabel_deployment_s, PodLabel_deploymentconfig_s, PodLabel_docker_registry_s, Name_s, Namespace_s, PodStatus_s, PodIp_s, PodUid_g, PodCreationTimeStamp_t, SourceSystem</span><span class="sxs-lookup"><span data-stu-id="cebcc-376">TimeGenerated, Computer, PodLabel_deployment_s, PodLabel_deploymentconfig_s, PodLabel_docker_registry_s, Name_s, Namespace_s, PodStatus_s, PodIp_s, PodUid_g, PodCreationTimeStamp_t, SourceSystem</span></span> |
| <span data-ttu-id="cebcc-377">Proceso del contenedor</span><span class="sxs-lookup"><span data-stu-id="cebcc-377">Container process</span></span> | `Type=ContainerProcess_CL` | <span data-ttu-id="cebcc-378">TimeGenerated, Computer, Pod_s, Namespace_s, ClassName_s, InstanceID_s, Uid_s, PID_s, PPID_s, C_s, STIME_s, Tty_s, TIME_s, Cmd_s, Id_s, Name_s, SourceSystem</span><span class="sxs-lookup"><span data-stu-id="cebcc-378">TimeGenerated, Computer, Pod_s, Namespace_s, ClassName_s, InstanceID_s, Uid_s, PID_s, PPID_s, C_s, STIME_s, Tty_s, TIME_s, Cmd_s, Id_s, Name_s, SourceSystem</span></span> |
| <span data-ttu-id="cebcc-379">Eventos de Kubernetes</span><span class="sxs-lookup"><span data-stu-id="cebcc-379">Kubernetes events</span></span> | `Type=KubeEvents_CL` | <span data-ttu-id="cebcc-380">TimeGenerated, Computer, Name_s, ObjectKind_s, Namespace_s, Reason_s, Type_s, SourceComponent_s, SourceSystem, Message</span><span class="sxs-lookup"><span data-stu-id="cebcc-380">TimeGenerated, Computer, Name_s, ObjectKind_s, Namespace_s, Reason_s, Type_s, SourceComponent_s, SourceSystem, Message</span></span> |

<span data-ttu-id="cebcc-381">Las etiquetas que se anexan a los tipos de datos *PodLabel* son sus propias etiquetas personalizadas.</span><span class="sxs-lookup"><span data-stu-id="cebcc-381">Labels appended to *PodLabel* data types are your own custom labels.</span></span> <span data-ttu-id="cebcc-382">Las etiquetas de PodLabel anexadas que se muestran en la tabla son ejemplos.</span><span class="sxs-lookup"><span data-stu-id="cebcc-382">The appended PodLabel labels shown in the table are examples.</span></span> <span data-ttu-id="cebcc-383">Por lo tanto, `PodLabel_deployment_s`, `PodLabel_deploymentconfig_s`, `PodLabel_docker_registry_s` se diferencian en el conjunto de datos de su entorno y genéricamente son similares a `PodLabel_yourlabel_s`.</span><span class="sxs-lookup"><span data-stu-id="cebcc-383">So, `PodLabel_deployment_s`, `PodLabel_deploymentconfig_s`, `PodLabel_docker_registry_s` will differ in your environment's data set and generically resemble `PodLabel_yourlabel_s`.</span></span>


## <a name="monitor-containers"></a><span data-ttu-id="cebcc-384">Supervisión de contenedores</span><span class="sxs-lookup"><span data-stu-id="cebcc-384">Monitor containers</span></span>
<span data-ttu-id="cebcc-385">Una vez habilitada la solución en el portal de OMS, el icono **Contenedores** muestra la información de resumen de los hosts de contenedores y de los contenedores en ejecución en los hosts.</span><span class="sxs-lookup"><span data-stu-id="cebcc-385">After you have the solution enabled in the OMS portal, the **Containers** tile shows summary information about your container hosts and the containers running in hosts.</span></span>

![Icono de Containers](./media/log-analytics-containers/containers-title.png)

<span data-ttu-id="cebcc-387">El icono muestra información general de cuántos contenedores hay en el entorno y si su estado es de error, en ejecución o detenido.</span><span class="sxs-lookup"><span data-stu-id="cebcc-387">The tile shows an overview of how many containers you have in the environment and whether they're failed, running, or stopped.</span></span>

### <a name="using-the-containers-dashboard"></a><span data-ttu-id="cebcc-388">Uso del panel Containers</span><span class="sxs-lookup"><span data-stu-id="cebcc-388">Using the Containers dashboard</span></span>
<span data-ttu-id="cebcc-389">Haga clic en el icono **Containers**.</span><span class="sxs-lookup"><span data-stu-id="cebcc-389">Click the **Containers** tile.</span></span> <span data-ttu-id="cebcc-390">Desde allí verá las vistas organizadas por:</span><span class="sxs-lookup"><span data-stu-id="cebcc-390">From there you'll see views organized by:</span></span>

- <span data-ttu-id="cebcc-391">**Eventos de contenedor**: muestra el estado de contenedor y los equipos con contenedores en estado de error.</span><span class="sxs-lookup"><span data-stu-id="cebcc-391">**Container Events** - Shows container status and computers with failed containers.</span></span>
- <span data-ttu-id="cebcc-392">**Registros de contenedor**: muestra un gráfico de archivos de registro de contenedor generados durante el tiempo y una lista de equipos con el mayor número de archivos de registro.</span><span class="sxs-lookup"><span data-stu-id="cebcc-392">**Container Logs** - Shows a chart of container log files generated over time and a list of computers with the highest number of log files.</span></span>
- <span data-ttu-id="cebcc-393">**Eventos de Kubernetes**: muestra un gráfico de eventos de Kubernetes generados durante el tiempo y una lista de los motivos por los que los pods generaron los eventos.</span><span class="sxs-lookup"><span data-stu-id="cebcc-393">**Kubernetes Events** - Shows a chart of Kubernetes events generated over time and a list of the reasons why pods generated the events.</span></span> <span data-ttu-id="cebcc-394">*Este conjunto de datos solo se usa en entornos Linux.*</span><span class="sxs-lookup"><span data-stu-id="cebcc-394">*This data set is used only in Linux environments.*</span></span>
- <span data-ttu-id="cebcc-395">**Inventario de espacios de nombres de Kubernetes**: muestra el número de espacios de nombres y pods y muestra su jerarquía.</span><span class="sxs-lookup"><span data-stu-id="cebcc-395">**Kubernetes Namespace Inventory** - Shows the number of namespaces and pods and shows their hierarchy.</span></span> <span data-ttu-id="cebcc-396">*Este conjunto de datos solo se usa en entornos Linux.*</span><span class="sxs-lookup"><span data-stu-id="cebcc-396">*This data set is used only in Linux environments.*</span></span>
- <span data-ttu-id="cebcc-397">**Inventario de nodo de contenedor**: muestra el número de tipos de orquestación usados en los nodos o hosts del contenedor.</span><span class="sxs-lookup"><span data-stu-id="cebcc-397">**Container Node Inventory** - Shows the number of orchestration types used on container nodes/hosts.</span></span> <span data-ttu-id="cebcc-398">Los nodos de equipo y hosts también se enumeran según el número de contenedores.</span><span class="sxs-lookup"><span data-stu-id="cebcc-398">The computer nodes/hosts are also listed by the number of containers.</span></span> <span data-ttu-id="cebcc-399">*Este conjunto de datos solo se usa en entornos Linux.*</span><span class="sxs-lookup"><span data-stu-id="cebcc-399">*This data set is used only in Linux environments.*</span></span>
- <span data-ttu-id="cebcc-400">**Inventario de imágenes de contenedor**: muestra el número total de imágenes de contenedor que se utilizan y el número de tipos de imagen.</span><span class="sxs-lookup"><span data-stu-id="cebcc-400">**Container Images Inventory** - Shows the total number of container images used and number of image types.</span></span> <span data-ttu-id="cebcc-401">También se muestra el número de imágenes según la etiqueta de imagen.</span><span class="sxs-lookup"><span data-stu-id="cebcc-401">The number of images are also listed by the image tag.</span></span>
- <span data-ttu-id="cebcc-402">**Estado de contenedores**: muestra el número total de nodos de contenedor y equipos host que tienen contenedores en ejecución.</span><span class="sxs-lookup"><span data-stu-id="cebcc-402">**Containers Status** - Shows the total number of container nodes/host computers that have running containers.</span></span> <span data-ttu-id="cebcc-403">También se enumeran los equipos según el número de hosts en ejecución.</span><span class="sxs-lookup"><span data-stu-id="cebcc-403">Computers are also listed by the number of running hosts.</span></span>
- <span data-ttu-id="cebcc-404">**Procesos del contenedor**: muestra un gráfico de líneas de procesos de contenedor en ejecución a lo largo del tiempo.</span><span class="sxs-lookup"><span data-stu-id="cebcc-404">**Container Process** - Shows a line chart of container processes running over time.</span></span> <span data-ttu-id="cebcc-405">También se enumeran los contenedores según los comandos o procesos en ejecución en los contenedores.</span><span class="sxs-lookup"><span data-stu-id="cebcc-405">Containers are also listed by running command/process within containers.</span></span> <span data-ttu-id="cebcc-406">*Este conjunto de datos solo se usa en entornos Linux.*</span><span class="sxs-lookup"><span data-stu-id="cebcc-406">*This data set is used only in Linux environments.*</span></span>
- <span data-ttu-id="cebcc-407">**Rendimiento de la CPU del contenedor**: muestra un gráfico de líneas del promedio de uso de CPU a lo largo del tiempo para los nodos y hosts.</span><span class="sxs-lookup"><span data-stu-id="cebcc-407">**Container CPU Performance** - Shows a line chart of the average CPU utilization over time for computer nodes/hosts.</span></span> <span data-ttu-id="cebcc-408">También enumera los nodos y hosts según el uso medio de CPU.</span><span class="sxs-lookup"><span data-stu-id="cebcc-408">Also lists the computer nodes/hosts based on average CPU utilization.</span></span>
- <span data-ttu-id="cebcc-409">**Rendimiento de la memoria del contenedor**: muestra un gráfico de líneas del uso de memoria a lo largo del tiempo.</span><span class="sxs-lookup"><span data-stu-id="cebcc-409">**Container Memory Performance** - Shows a line chart of memory usage over time.</span></span> <span data-ttu-id="cebcc-410">También muestra el uso de memoria de los equipos según el nombre de la instancia.</span><span class="sxs-lookup"><span data-stu-id="cebcc-410">Also lists computer memory utilization based on instance name.</span></span>
- <span data-ttu-id="cebcc-411">**Rendimiento del equipo**: muestra gráficos de líneas del porcentaje de rendimiento de la CPU, del porcentaje de uso de memoria y de los megabytes de espacio libre en disco a lo largo del tiempo.</span><span class="sxs-lookup"><span data-stu-id="cebcc-411">**Computer Performance** - Shows line charts of the percent of CPU performance over time, percent of memory usage over time, and megabytes of free disk space over time.</span></span> <span data-ttu-id="cebcc-412">Puede mantener el ratón sobre cualquier línea de un gráfico para ver más detalles.</span><span class="sxs-lookup"><span data-stu-id="cebcc-412">You can hover over any line in a chart to view more details.</span></span>


<span data-ttu-id="cebcc-413">Cada área del panel es una representación visual de una búsqueda que se ejecuta en los datos recopilados.</span><span class="sxs-lookup"><span data-stu-id="cebcc-413">Each area of the dashboard is a visual representation of a search that is run on collected data.</span></span>

![Panel Containers](./media/log-analytics-containers/containers-dash01.png)

![Panel Containers](./media/log-analytics-containers/containers-dash02.png)

<span data-ttu-id="cebcc-416">En el área **Estado del contenedor**, haga clic en la parte superior, como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="cebcc-416">In the **Container Status** area, click the top area, as shown below.</span></span>

![Estado de los contenedores](./media/log-analytics-containers/containers-status.png)

<span data-ttu-id="cebcc-418">Se abre la Búsqueda de registros, con información sobre el estado de los contenedores.</span><span class="sxs-lookup"><span data-stu-id="cebcc-418">Log Search opens, displaying information about the state of your containers.</span></span>

![Búsqueda de registros para contenedores](./media/log-analytics-containers/containers-log-search.png)

<span data-ttu-id="cebcc-420">Desde aquí, puede editar la consulta de búsqueda para modificarla y encontrar la información específica que le interesa.</span><span class="sxs-lookup"><span data-stu-id="cebcc-420">From here, you can edit the search query to modify it to find the specific information you're interested in.</span></span> <span data-ttu-id="cebcc-421">Para más información acerca del uso de la búsqueda de registros, consulte [Búsquedas de registros en Log Analytics](log-analytics-log-searches.md).</span><span class="sxs-lookup"><span data-stu-id="cebcc-421">For more information about Log Searches, see [Log searches in Log Analytics](log-analytics-log-searches.md).</span></span>

## <a name="troubleshoot-by-finding-a-failed-container"></a><span data-ttu-id="cebcc-422">Solución de problemas mediante la búsqueda de un contenedor con error</span><span class="sxs-lookup"><span data-stu-id="cebcc-422">Troubleshoot by finding a failed container</span></span>

<span data-ttu-id="cebcc-423">Log Analytics marca un contenedor como **Failed** (Error) si ha terminado con un código de salida distinto de cero.</span><span class="sxs-lookup"><span data-stu-id="cebcc-423">Log Analytics marks a container as **Failed** if it has exited with a non-zero exit code.</span></span> <span data-ttu-id="cebcc-424">Puede ver un resumen de los errores del entorno en el área **Contenedores con errores**.</span><span class="sxs-lookup"><span data-stu-id="cebcc-424">You can see an overview of the errors and failures in the environment in the **Failed Containers** area.</span></span>

### <a name="to-find-failed-containers"></a><span data-ttu-id="cebcc-425">Para buscar contenedores con errores</span><span class="sxs-lookup"><span data-stu-id="cebcc-425">To find failed containers</span></span>
1. <span data-ttu-id="cebcc-426">Haga clic en el área **Estado del contenedor**.</span><span class="sxs-lookup"><span data-stu-id="cebcc-426">Click the **Container Status** area.</span></span>  
   <span data-ttu-id="cebcc-427">![estado de los contenedores](./media/log-analytics-containers/containers-status.png)</span><span class="sxs-lookup"><span data-stu-id="cebcc-427">![containers status](./media/log-analytics-containers/containers-status.png)</span></span>
2. <span data-ttu-id="cebcc-428">Se abre la Búsqueda de registros y muestra el estado de los contenedores, de forma similar a la siguiente.</span><span class="sxs-lookup"><span data-stu-id="cebcc-428">Log Search opens and displays the state of your containers, similar to the following.</span></span>  
   ![estado de los contenedores](./media/log-analytics-containers/containers-log-search.png)
3. <span data-ttu-id="cebcc-430">A continuación, haga clic en el valor agregado de contenedores con errores para ver información adicional.</span><span class="sxs-lookup"><span data-stu-id="cebcc-430">Next, click the aggregated value of failed containers to view additional information.</span></span> <span data-ttu-id="cebcc-431">Expanda **mostrar más** para ver el identificador de la imagen.</span><span class="sxs-lookup"><span data-stu-id="cebcc-431">Expand **show more** to view the image ID.</span></span>  
   <span data-ttu-id="cebcc-432">![contenedores con errores](./media/log-analytics-containers/containers-state-failed.png)</span><span class="sxs-lookup"><span data-stu-id="cebcc-432">![failed containers](./media/log-analytics-containers/containers-state-failed.png)</span></span>  
4. <span data-ttu-id="cebcc-433">A continuación, escriba lo siguiente en la consulta de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="cebcc-433">Next, type the following in the search query.</span></span> <span data-ttu-id="cebcc-434">`Type=ContainerInventory <ImageID>` para ver detalles de la imagen como tamaño de la imagen y el número de imágenes detenidas y con error.</span><span class="sxs-lookup"><span data-stu-id="cebcc-434">`Type=ContainerInventory <ImageID>` to see details about the image such as image size and number of stopped and failed images.</span></span>  
   <span data-ttu-id="cebcc-435">![contenedores con errores](./media/log-analytics-containers/containers-failed04.png)</span><span class="sxs-lookup"><span data-stu-id="cebcc-435">![failed containers](./media/log-analytics-containers/containers-failed04.png)</span></span>

## <a name="search-logs-for-container-data"></a><span data-ttu-id="cebcc-436">Registros de búsqueda de datos de contenedor</span><span class="sxs-lookup"><span data-stu-id="cebcc-436">Search logs for container data</span></span>
<span data-ttu-id="cebcc-437">Cuando está solucionando un error específico, puede resultar de ayuda ver dónde se está produciendo en su entorno.</span><span class="sxs-lookup"><span data-stu-id="cebcc-437">When you're troubleshooting a specific error, it can help to see where it is occurring in your environment.</span></span> <span data-ttu-id="cebcc-438">Los siguientes tipos de registro le ayudarán a crear consultas que devuelven la información que desea.</span><span class="sxs-lookup"><span data-stu-id="cebcc-438">The following log types will help you create queries to return the information you want.</span></span>


- <span data-ttu-id="cebcc-439">**ContainerImageInventory**: use este tipo si desea encontrar información organizada por imagen, y para ver información sobre la imagen, por ejemplo, identificadores o tamaños de imagen.</span><span class="sxs-lookup"><span data-stu-id="cebcc-439">**ContainerImageInventory** – Use this type when you're trying to find information organized by image and to view image information such as image IDs or sizes.</span></span>
- <span data-ttu-id="cebcc-440">**ContainerInventory**: use este tipo si desea obtener información sobre la ubicación del contenedor, cuáles son sus nombres y qué imágenes se están ejecutando.</span><span class="sxs-lookup"><span data-stu-id="cebcc-440">**ContainerInventory** – Use this type when you want information about container location, what their names are, and what images they're running.</span></span>
- <span data-ttu-id="cebcc-441">**ContainerLog**: use este tipo si desea buscar la información de registro de un error específico y sus entradas.</span><span class="sxs-lookup"><span data-stu-id="cebcc-441">**ContainerLog** – Use this type when you want to find specific error log information and entries.</span></span>
- <span data-ttu-id="cebcc-442">**ContainerNodeInventory_CL** use este tipo cuando desee ver la información sobre el nodo o host donde se encuentran los contenedores.</span><span class="sxs-lookup"><span data-stu-id="cebcc-442">**ContainerNodeInventory_CL**  Use this type when you want the information about host/node where containers are residing.</span></span> <span data-ttu-id="cebcc-443">Proporciona información sobre la versión de Docker, el tipo de orquestación, almacenamiento y red.</span><span class="sxs-lookup"><span data-stu-id="cebcc-443">It provides you Docker version, orchestration type, storage, and network information.</span></span>
- <span data-ttu-id="cebcc-444">**ContainerProcess_CL** use este tipo para ver rápidamente los procesos en ejecución en el contenedor.</span><span class="sxs-lookup"><span data-stu-id="cebcc-444">**ContainerProcess_CL** Use this type to quickly see the process running within the container.</span></span>
- <span data-ttu-id="cebcc-445">**ContainerServiceLog**: use este tipo si desea encontrar información de seguimiento de auditoría para el daemon de Docker, tales como los comandos de inicio, detención, eliminación o extracción.</span><span class="sxs-lookup"><span data-stu-id="cebcc-445">**ContainerServiceLog** – Use this type when you're trying to find audit trail information for the Docker daemon, such as start, stop, delete, or pull commands.</span></span>
- <span data-ttu-id="cebcc-446">**KubeEvents_CL** use este tipo para ver los eventos de Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="cebcc-446">**KubeEvents_CL**  Use this type to see the Kubernetes events.</span></span>
- <span data-ttu-id="cebcc-447">**KubePodInventory_CL** use este tipo cuando desee conocer la información de la jerarquía del clúster.</span><span class="sxs-lookup"><span data-stu-id="cebcc-447">**KubePodInventory_CL**  Use this type when you want to understand the cluster hierarchy information.</span></span>


### <a name="to-search-logs-for-container-data"></a><span data-ttu-id="cebcc-448">Para buscar registros de datos de contenedor</span><span class="sxs-lookup"><span data-stu-id="cebcc-448">To search logs for container data</span></span>
* <span data-ttu-id="cebcc-449">Elija una imagen que sabe que ha tenido errores recientemente y busque los registros de errores de ella.</span><span class="sxs-lookup"><span data-stu-id="cebcc-449">Choose an image that you know has failed recently and find the error logs for it.</span></span> <span data-ttu-id="cebcc-450">Para empezar, busque un nombre de contenedor que esté ejecutando esa imagen con una búsqueda **ContainerInventory**.</span><span class="sxs-lookup"><span data-stu-id="cebcc-450">Start by finding a container name that is running that image with a **ContainerInventory** search.</span></span> <span data-ttu-id="cebcc-451">Por ejemplo, busque `Type=ContainerInventory ubuntu Failed`.</span><span class="sxs-lookup"><span data-stu-id="cebcc-451">For example, search for `Type=ContainerInventory ubuntu Failed`</span></span>  
    <span data-ttu-id="cebcc-452">![Búsqueda de contenedores de Ubuntu](./media/log-analytics-containers/search-ubuntu.png)</span><span class="sxs-lookup"><span data-stu-id="cebcc-452">![Search for Ubuntu containers](./media/log-analytics-containers/search-ubuntu.png)</span></span>

  <span data-ttu-id="cebcc-453">Anote el nombre del contenedor junto a **Nombre** y busque los registros.</span><span class="sxs-lookup"><span data-stu-id="cebcc-453">The name of the container next to **Name**, and search for those logs.</span></span> <span data-ttu-id="cebcc-454">En este ejemplo, es `Type=ContainerLog cranky_stonebreaker`.</span><span class="sxs-lookup"><span data-stu-id="cebcc-454">In this example, it is `Type=ContainerLog cranky_stonebreaker`.</span></span>

<span data-ttu-id="cebcc-455">**Ver información de rendimiento**</span><span class="sxs-lookup"><span data-stu-id="cebcc-455">**View performance information**</span></span>

<span data-ttu-id="cebcc-456">Si está empezando a crear consultas, puede resultar de ayuda ver antes qué es posible hacer.</span><span class="sxs-lookup"><span data-stu-id="cebcc-456">When you're beginning to construct queries, it can help to see what's possible first.</span></span> <span data-ttu-id="cebcc-457">Por ejemplo, para ver todos los datos de rendimiento, pruebe con una consulta amplia como la siguiente consulta de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="cebcc-457">For example, to see all performance data, try a broad query by typing the following search query.</span></span>

```
Type=Perf
```

![rendimiento de contenedores](./media/log-analytics-containers/containers-perf01.png)

<span data-ttu-id="cebcc-459">Para limitar el ámbito de los datos de rendimiento que se muestran a un contenedor específico, escriba el nombre del mismo a la derecha de su consulta.</span><span class="sxs-lookup"><span data-stu-id="cebcc-459">You can scope the performance data you're seeing to a specific container by typing the name of it to the right of your query.</span></span>

```
Type=Perf <containerName>
```

<span data-ttu-id="cebcc-460">Se muestra la lista de las métricas de rendimiento recopiladas para un contenedor individual.</span><span class="sxs-lookup"><span data-stu-id="cebcc-460">That shows the list of performance metrics that are collected for an individual container.</span></span>

![rendimiento de contenedores](./media/log-analytics-containers/containers-perf03.png)

## <a name="example-log-search-queries"></a><span data-ttu-id="cebcc-462">Ejemplos de consultas de búsqueda de registros</span><span class="sxs-lookup"><span data-stu-id="cebcc-462">Example log search queries</span></span>
<span data-ttu-id="cebcc-463">Suele resultar útil crear consultas a partir de un ejemplo o dos y modificarlas para adaptarlas a su entorno.</span><span class="sxs-lookup"><span data-stu-id="cebcc-463">It's often useful to build queries starting with an example or two and then modifying them to fit your environment.</span></span> <span data-ttu-id="cebcc-464">Para empezar, puede experimentar con el área **Consultas de ejemplo** para ayudarle a crear consultas más avanzadas.</span><span class="sxs-lookup"><span data-stu-id="cebcc-464">As a starting point, you can experiment with the **Sample Queries** area to help you build more advanced queries.</span></span>

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

![Consultas de contenedores](./media/log-analytics-containers/containers-queries.png)


## <a name="saving-log-search-queries"></a><span data-ttu-id="cebcc-466">Guardado de consultas de búsqueda de registros</span><span class="sxs-lookup"><span data-stu-id="cebcc-466">Saving log search queries</span></span>
<span data-ttu-id="cebcc-467">El guardado de consultas es una característica estándar de Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="cebcc-467">Saving queries is a standard feature in Log Analytics.</span></span> <span data-ttu-id="cebcc-468">Guárdelas para volver a usar en el futuro aquellas que haya encontrado más útiles.</span><span class="sxs-lookup"><span data-stu-id="cebcc-468">By saving them, you'll have those that you've found useful handy for future use.</span></span>

<span data-ttu-id="cebcc-469">Después de crear una consulta que encuentre útil, guárdela haciendo clic en **Favoritos** en la parte superior de la página Búsqueda de registros.</span><span class="sxs-lookup"><span data-stu-id="cebcc-469">After you create a query that you find useful, save it by clicking **Favorites** at the top of the Log Search page.</span></span> <span data-ttu-id="cebcc-470">Podrá volver a acceder fácilmente a ella más adelante desde la página **Mi panel**.</span><span class="sxs-lookup"><span data-stu-id="cebcc-470">Then you can easily access it later from the **My Dashboard** page.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cebcc-471">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="cebcc-471">Next steps</span></span>
* <span data-ttu-id="cebcc-472">[Búsqueda de registros](log-analytics-log-searches.md), para ver los registros de datos detallados de los contenedores.</span><span class="sxs-lookup"><span data-stu-id="cebcc-472">[Search logs](log-analytics-log-searches.md) to view detailed container data records.</span></span>
