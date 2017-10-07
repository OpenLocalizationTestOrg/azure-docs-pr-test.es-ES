---
title: "aaaSupportability de Agregar conjunto de disponibilidad existente de máquinas virtuales de Azure tooan | Documentos de Microsoft"
description: "Compatibilidad de Agregar conjunto de disponibilidad de máquinas virtuales de Azure tooan existente."
services: virtual-machines-linux
documentationcenter: 
author: Deland-Han
manager: cshepard
editor: 
ms.assetid: 
ms.service: virtual-machines
ms.workload: virtual-machines
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/15/2017
ms.author: delhan
ms.openlocfilehash: dc2bd86b916f1d1a0a0d4c9e870df829434c96b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="supportability-of-adding-azure-vms-tooan-existing-availability-set"></a><span data-ttu-id="64794-103">Compatibilidad de Agregar conjunto de disponibilidad de máquinas virtuales de Azure tooan existente</span><span class="sxs-lookup"><span data-stu-id="64794-103">Supportability of adding Azure VMs tooan existing availability set</span></span>

<span data-ttu-id="64794-104">En ocasiones, puede encontrar limitaciones cuando se agrega nuevas máquinas virtuales (VM) tooan conjunto de disponibilidad existente.</span><span class="sxs-lookup"><span data-stu-id="64794-104">You may occasionally encounter limitations when you add new virtual machines (VMs) tooan existing availability set.</span></span> <span data-ttu-id="64794-105">Hola Hola a las series VM se pueden mezclar en el mismo conjunto de disponibilidad de detalles de gráfico siguientes.</span><span class="sxs-lookup"><span data-stu-id="64794-105">hello following chart details which VM series you can mix in hello same availability set.</span></span>

<span data-ttu-id="64794-106">Aquí es Hola compatibilidad toomix diferentes tipos de matriz de máquinas virtuales:</span><span class="sxs-lookup"><span data-stu-id="64794-106">Here is hello supportability matrix toomix different types of VMs:</span></span>

<span data-ttu-id="64794-107">Serie y conjunto de disponibilidad</span><span class="sxs-lookup"><span data-stu-id="64794-107">Series & Availability Set</span></span>|<span data-ttu-id="64794-108">Segunda máquina virtual</span><span class="sxs-lookup"><span data-stu-id="64794-108">Second VM</span></span>|<span data-ttu-id="64794-109">Una </span><span class="sxs-lookup"><span data-stu-id="64794-109">A</span></span>|<span data-ttu-id="64794-110">Av2</span><span class="sxs-lookup"><span data-stu-id="64794-110">Av2</span></span>|<span data-ttu-id="64794-111">D</span><span class="sxs-lookup"><span data-stu-id="64794-111">D</span></span>|<span data-ttu-id="64794-112">Dv2</span><span class="sxs-lookup"><span data-stu-id="64794-112">Dv2</span></span>|<span data-ttu-id="64794-113">Dv3</span><span class="sxs-lookup"><span data-stu-id="64794-113">Dv3</span></span>|
|---|---|---|---|---|---|---|
|<span data-ttu-id="64794-114">Primera máquina virtual</span><span class="sxs-lookup"><span data-stu-id="64794-114">First VM</span></span>|||||||
|<span data-ttu-id="64794-115">Una </span><span class="sxs-lookup"><span data-stu-id="64794-115">A</span></span>||<span data-ttu-id="64794-116">OK</span><span class="sxs-lookup"><span data-stu-id="64794-116">OK</span></span>|<span data-ttu-id="64794-117">OK</span><span class="sxs-lookup"><span data-stu-id="64794-117">OK</span></span>|<span data-ttu-id="64794-118">OK</span><span class="sxs-lookup"><span data-stu-id="64794-118">OK</span></span>|<span data-ttu-id="64794-119">OK</span><span class="sxs-lookup"><span data-stu-id="64794-119">OK</span></span>|<span data-ttu-id="64794-120">OK</span><span class="sxs-lookup"><span data-stu-id="64794-120">OK</span></span>|
|<span data-ttu-id="64794-121">Av2</span><span class="sxs-lookup"><span data-stu-id="64794-121">Av2</span></span>||<span data-ttu-id="64794-122">OK</span><span class="sxs-lookup"><span data-stu-id="64794-122">OK</span></span>|<span data-ttu-id="64794-123">OK</span><span class="sxs-lookup"><span data-stu-id="64794-123">OK</span></span>|<span data-ttu-id="64794-124">OK</span><span class="sxs-lookup"><span data-stu-id="64794-124">OK</span></span>|<span data-ttu-id="64794-125">OK</span><span class="sxs-lookup"><span data-stu-id="64794-125">OK</span></span>|<span data-ttu-id="64794-126">OK</span><span class="sxs-lookup"><span data-stu-id="64794-126">OK</span></span>|
|<span data-ttu-id="64794-127">D</span><span class="sxs-lookup"><span data-stu-id="64794-127">D</span></span>||<span data-ttu-id="64794-128">OK</span><span class="sxs-lookup"><span data-stu-id="64794-128">OK</span></span>|<span data-ttu-id="64794-129">OK</span><span class="sxs-lookup"><span data-stu-id="64794-129">OK</span></span>|<span data-ttu-id="64794-130">OK</span><span class="sxs-lookup"><span data-stu-id="64794-130">OK</span></span>|<span data-ttu-id="64794-131">OK</span><span class="sxs-lookup"><span data-stu-id="64794-131">OK</span></span>|<span data-ttu-id="64794-132">OK</span><span class="sxs-lookup"><span data-stu-id="64794-132">OK</span></span>|
|<span data-ttu-id="64794-133">Dv2</span><span class="sxs-lookup"><span data-stu-id="64794-133">Dv2</span></span>||<span data-ttu-id="64794-134">OK</span><span class="sxs-lookup"><span data-stu-id="64794-134">OK</span></span>|<span data-ttu-id="64794-135">OK</span><span class="sxs-lookup"><span data-stu-id="64794-135">OK</span></span>|<span data-ttu-id="64794-136">OK</span><span class="sxs-lookup"><span data-stu-id="64794-136">OK</span></span>|<span data-ttu-id="64794-137">OK</span><span class="sxs-lookup"><span data-stu-id="64794-137">OK</span></span>|<span data-ttu-id="64794-138">OK</span><span class="sxs-lookup"><span data-stu-id="64794-138">OK</span></span>|
|<span data-ttu-id="64794-139">Dv3</span><span class="sxs-lookup"><span data-stu-id="64794-139">Dv3</span></span>||<span data-ttu-id="64794-140">OK</span><span class="sxs-lookup"><span data-stu-id="64794-140">OK</span></span>|<span data-ttu-id="64794-141">OK</span><span class="sxs-lookup"><span data-stu-id="64794-141">OK</span></span>|<span data-ttu-id="64794-142">OK</span><span class="sxs-lookup"><span data-stu-id="64794-142">OK</span></span>|<span data-ttu-id="64794-143">OK</span><span class="sxs-lookup"><span data-stu-id="64794-143">OK</span></span>|<span data-ttu-id="64794-144">OK</span><span class="sxs-lookup"><span data-stu-id="64794-144">OK</span></span>|

<span data-ttu-id="64794-145">No se pudo todas las otras series de hello conjunto de disponibilidad mismo porque requieren un hardware específico.</span><span class="sxs-lookup"><span data-stu-id="64794-145">All other series could not be in hello same availability set because they require a specific hardware.</span></span>
