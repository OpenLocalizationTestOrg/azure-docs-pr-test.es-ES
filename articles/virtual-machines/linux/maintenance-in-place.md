---
title: "aaaVM conserva el mantenimiento de máquinas virtuales de Windows en Azure | Documentos de Microsoft"
description: "Migración local de máquinas virtuales para la realización de actualizaciones con conservación de memoria."
services: virtual-machines-windows
documentationcenter: 
author: 
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/27/2017
ms.author: 
ms.openlocfilehash: 544a2dcca52bb3ac51d341bceaf4ba3e7c71fd82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="vm-preserving-maintenance-in-place-vm-migration"></a><span data-ttu-id="6b271-103">Mantenimiento de conservación de máquinas virtuales (migración local de máquinas virtuales)</span><span class="sxs-lookup"><span data-stu-id="6b271-103">VM preserving maintenance (In-place VM migration)</span></span>

<span data-ttu-id="6b271-104">Aunque mayoría Hola de las actualizaciones no tienen ningún toohosted de impacto en las máquinas virtuales, hay casos donde toocomponents actualizaciones o servicios producir interferencias mínimo toorunning máquinas virtuales (sin un reinicio completo de la máquina virtual de hello).</span><span class="sxs-lookup"><span data-stu-id="6b271-104">While hello majority of updates have no impact toohosted VMs, there are cases where updates toocomponents or services result in minimal interference toorunning VMs (without a full reboot of hello virtual machine).</span></span>

<span data-ttu-id="6b271-105">Estas actualizaciones se realizan con la tecnología que permite la migración local en vivo, también llamada "actualización con conservación de memoria".</span><span class="sxs-lookup"><span data-stu-id="6b271-105">These updates are accomplished with technology that enables in-place live migration, also called "memory-preserving update".</span></span> <span data-ttu-id="6b271-106">Al actualizar el host de hello, máquina virtual de Hola se coloca en un estado "en pausa", conservar memoria hello en la RAM, mientras hello (por ejemplo, el sistema operativo subyacente) del entorno de hospedaje aplica revisiones y actualizaciones necesarias de Hola.</span><span class="sxs-lookup"><span data-stu-id="6b271-106">When updating hello host, hello virtual machine is placed into a “paused” state, preserving hello memory in RAM, while hello hosting environment (e.g. the underlying operating system) applies hello necessary updates and patches.</span></span>
<span data-ttu-id="6b271-107">máquina virtual de Hello, a continuación, se reanuda en 30 segundos de pausa.</span><span class="sxs-lookup"><span data-stu-id="6b271-107">hello virtual machine is then resumed within 30 seconds of being paused.</span></span>
<span data-ttu-id="6b271-108">Después de reanudar, reloj Hola de máquina virtual de Hola se sincronizará automáticamente.</span><span class="sxs-lookup"><span data-stu-id="6b271-108">After resuming, hello clock of hello virtual machine is automatically synchronized.</span></span>

<span data-ttu-id="6b271-109">No todas las actualizaciones se pueden implementar mediante este mecanismo, pero dado el período breve pausa, implementar las actualizaciones de esta forma en gran medida reduce máquinas toovirtual de impacto.</span><span class="sxs-lookup"><span data-stu-id="6b271-109">Not all updates can be deployed by using this mechanism, but given the short pause period, deploying updates in this way greatly reduces impact toovirtual machines.</span></span>

<span data-ttu-id="6b271-110">Las actualizaciones de varias instancias (máquinas virtuales en un conjunto de disponibilidad) se aplican a un dominio de actualización a la vez.</span><span class="sxs-lookup"><span data-stu-id="6b271-110">Multi-instance updates (VMs in an availability set) are applied one update domain at a time.</span></span>

<span data-ttu-id="6b271-111">Algunas aplicaciones pueden resultar afectadas por estas actualizaciones más que otras.</span><span class="sxs-lookup"><span data-stu-id="6b271-111">Some applications may be impacted by these updates more than others.</span></span> <span data-ttu-id="6b271-112">Las aplicaciones que realizan procesamiento de eventos en tiempo real, transmisión por secuencias multimedia o transcodificación o alto rendimiento redes escenarios, por ejemplo, no pueden ser tootolerate diseñado una pausa de segundo 30.</span><span class="sxs-lookup"><span data-stu-id="6b271-112">Applications that perform real-time event processing, media streaming or transcoding, or high throughput networking scenarios, for example, may not be designed tootolerate a 30 second pause.</span></span> <span data-ttu-id="6b271-113">Aplicaciones que se ejecutan en una máquina virtual pueden obtener información acerca de las próximas actualizaciones que realiza la llamada hello [eventos programados](../virtual-machines-scheduled-events.md) API de hello [el servicio de metadatos de Azure](../virtual-machines-instancemetadataservice-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6b271-113">Applications running in a virtual machine can learn about upcoming updates by calling hello [Scheduled Events](../virtual-machines-scheduled-events.md) API of hello [Azure Metadata Service](../virtual-machines-instancemetadataservice-overview.md).</span></span>
