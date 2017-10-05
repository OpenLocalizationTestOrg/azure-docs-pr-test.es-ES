---
title: Arquitectura de Microsoft Azure Stack Development Kit | Microsoft Docs
description: Vea la arquitectura de Microsoft Azure Stack Development Kit.
services: azure-stack
documentationcenter: 
author: heathl17
manager: byronr
editor: 
ms.assetid: a7e61ea4-be2f-4e55-9beb-7a079f348e05
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: helaw
ms.openlocfilehash: feb4f10f9f25515ba85011f467b2ada0cdfcdefb
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="microsoft-azure-stack-development-kit-architecture"></a><span data-ttu-id="1d299-103">Arquitectura de Microsoft Azure Stack Development Kit</span><span class="sxs-lookup"><span data-stu-id="1d299-103">Microsoft Azure Stack Development Kit architecture</span></span>
<span data-ttu-id="1d299-104">Azure Stack Development Kit es una implementación de un único nodo de Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="1d299-104">The Azure Stack Development Kit is a single-node deployment of Azure Stack.</span></span> <span data-ttu-id="1d299-105">Todos los componentes se instalan en máquinas virtuales que se ejecutan en un solo equipo host.</span><span class="sxs-lookup"><span data-stu-id="1d299-105">All the components are installed in virtual machines running on a single host machine.</span></span> 

## <a name="logical-architecture-diagram"></a><span data-ttu-id="1d299-106">Diagrama de arquitectura lógica</span><span class="sxs-lookup"><span data-stu-id="1d299-106">Logical architecture diagram</span></span>
<span data-ttu-id="1d299-107">El siguiente diagrama muestra la arquitectura lógica de Azure Stack Development Kit y sus componentes.</span><span class="sxs-lookup"><span data-stu-id="1d299-107">The following diagram illustrates the logical architecture of the Azure Stack development kit and its components.</span></span>

![](media/azure-stack-architecture/image1.png)

## <a name="virtual-machine-roles"></a><span data-ttu-id="1d299-108">Roles de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="1d299-108">Virtual machine roles</span></span>
<span data-ttu-id="1d299-109">Azure Stack Development Kit ofrece servicios a través de las siguientes máquinas virtuales en el host:</span><span class="sxs-lookup"><span data-stu-id="1d299-109">The Azure Stack development kit offers services using the following VMs on the host:</span></span>

| <span data-ttu-id="1d299-110">Nombre</span><span class="sxs-lookup"><span data-stu-id="1d299-110">Name</span></span> | <span data-ttu-id="1d299-111">Descripción</span><span class="sxs-lookup"><span data-stu-id="1d299-111">Description</span></span> |
| ----- | ----- |
| <span data-ttu-id="1d299-112">**AzS-ACS01**</span><span class="sxs-lookup"><span data-stu-id="1d299-112">**AzS-ACS01**</span></span> | <span data-ttu-id="1d299-113">Servicios de almacenamiento de Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="1d299-113">Azure Stack storage services.</span></span>|
| <span data-ttu-id="1d299-114">**AzS-ADFS01**</span><span class="sxs-lookup"><span data-stu-id="1d299-114">**AzS-ADFS01**</span></span> | <span data-ttu-id="1d299-115">Servicios de federación de Active Directory (AD FS).</span><span class="sxs-lookup"><span data-stu-id="1d299-115">Active Directory Federation Services (ADFS).</span></span>  |
| <span data-ttu-id="1d299-116">**AzS-BGPNAT01**</span><span class="sxs-lookup"><span data-stu-id="1d299-116">**AzS-BGPNAT01**</span></span> | <span data-ttu-id="1d299-117">Enrutador perimetral que proporciona funcionalidades de NAT y VPN para Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="1d299-117">Edge router and provides NAT and VPN capabilities for Azure Stack.</span></span> |
| <span data-ttu-id="1d299-118">**AzS-CA01**</span><span class="sxs-lookup"><span data-stu-id="1d299-118">**AzS-CA01**</span></span> | <span data-ttu-id="1d299-119">Servicios de entidad de certificación para servicios de rol de Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="1d299-119">Certificate authority services for Azure Stack role services.</span></span>|
| <span data-ttu-id="1d299-120">**AzS-DC01**</span><span class="sxs-lookup"><span data-stu-id="1d299-120">**AzS-DC01**</span></span> | <span data-ttu-id="1d299-121">Servicios de Active Directory, DNS y DHCP para Microsoft Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="1d299-121">Active Directory, DNS, and DHCP services for Microsoft Azure Stack.</span></span>|
| <span data-ttu-id="1d299-122">**AzS-ERCS01**</span><span class="sxs-lookup"><span data-stu-id="1d299-122">**AzS-ERCS01**</span></span> | <span data-ttu-id="1d299-123">Máquina virtual de la consola de recuperación de emergencia.</span><span class="sxs-lookup"><span data-stu-id="1d299-123">Emergency Recovery Console VM.</span></span> |
| <span data-ttu-id="1d299-124">**AzS-GWY01**</span><span class="sxs-lookup"><span data-stu-id="1d299-124">**AzS-GWY01**</span></span> | <span data-ttu-id="1d299-125">Servicios perimetrales de puerta de enlace, como las conexiones de sitio a sitio de VPN para redes de inquilinos.</span><span class="sxs-lookup"><span data-stu-id="1d299-125">Edge gateway services such as VPN site-to-site connections for tenant networks.</span></span>|
| <span data-ttu-id="1d299-126">**AzS-NC01**</span><span class="sxs-lookup"><span data-stu-id="1d299-126">**AzS-NC01**</span></span> | <span data-ttu-id="1d299-127">Controladora de red, que administra los servicios de red de Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="1d299-127">Network Controller, which manages Azure Stack network services.</span></span>  |
| <span data-ttu-id="1d299-128">**AzS-SLB01**</span><span class="sxs-lookup"><span data-stu-id="1d299-128">**AzS-SLB01**</span></span> | <span data-ttu-id="1d299-129">Servicios de multiplexor del equilibrio de carga en Azure Stack para los inquilinos y los servicios de infraestructura de Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="1d299-129">Load balancing multiplexer services in Azure Stack for both tenants and Azure Stack infrastructure services.</span></span>  |
| <span data-ttu-id="1d299-130">**AzS-SQL01**</span><span class="sxs-lookup"><span data-stu-id="1d299-130">**AzS-SQL01**</span></span> | <span data-ttu-id="1d299-131">Almacén de datos internos para los roles de infraestructura de Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="1d299-131">Internal data store for Azure Stack infrastructure roles.</span></span>  |
| <span data-ttu-id="1d299-132">**AzS-WAS01**</span><span class="sxs-lookup"><span data-stu-id="1d299-132">**AzS-WAS01**</span></span> | <span data-ttu-id="1d299-133">Portal de administración de Azure Stack y servicios de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="1d299-133">Azure Stack administrative portal and Azure Resource Manager services.</span></span>|
| <span data-ttu-id="1d299-134">**AzS-WASP01**</span><span class="sxs-lookup"><span data-stu-id="1d299-134">**AzS-WASP01**</span></span>| <span data-ttu-id="1d299-135">Portal del usuario (inquilino) de Azure Stack y servicios de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="1d299-135">Azure Stack user (tenant) portal and Azure Resource Manager services.</span></span>|
| <span data-ttu-id="1d299-136">**AzS-XRP01**</span><span class="sxs-lookup"><span data-stu-id="1d299-136">**AzS-XRP01**</span></span> | <span data-ttu-id="1d299-137">Controlador de administración de infraestructura para Microsoft Azure Stack, incluidos los proveedores de recursos de Compute, Networks y Storage.</span><span class="sxs-lookup"><span data-stu-id="1d299-137">Infrastructure management controller for Microsoft Azure Stack, including the Compute, Network, and Storage resource providers.</span></span>|


## <a name="next-steps"></a><span data-ttu-id="1d299-138">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1d299-138">Next steps</span></span>
[<span data-ttu-id="1d299-139">Implementación de Azure Stack</span><span class="sxs-lookup"><span data-stu-id="1d299-139">Deploy Azure Stack</span></span>](azure-stack-deploy.md)

[<span data-ttu-id="1d299-140">Primeros escenarios para probar</span><span class="sxs-lookup"><span data-stu-id="1d299-140">First scenarios to try</span></span>](azure-stack-first-scenarios.md)

