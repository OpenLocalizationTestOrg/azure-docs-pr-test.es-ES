---
title: aaaMicrosoft arquitectura del Kit de desarrollo de pila de Azure | Documentos de Microsoft
description: Hola vista arquitectura del Kit de desarrollo de pila de Microsoft Azure.
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
ms.openlocfilehash: 32a19ced7ddd57b97ba796679c116132090402e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-azure-stack-development-kit-architecture"></a><span data-ttu-id="de863-103">Arquitectura de Microsoft Azure Stack Development Kit</span><span class="sxs-lookup"><span data-stu-id="de863-103">Microsoft Azure Stack Development Kit architecture</span></span>
<span data-ttu-id="de863-104">Hola Kit de desarrollo de pila de Azure es una implementación de un único nodo de pila de Azure.</span><span class="sxs-lookup"><span data-stu-id="de863-104">hello Azure Stack Development Kit is a single-node deployment of Azure Stack.</span></span> <span data-ttu-id="de863-105">Todos los componentes de Hola se instalan en máquinas virtuales se ejecutan en una máquina de host único.</span><span class="sxs-lookup"><span data-stu-id="de863-105">All hello components are installed in virtual machines running on a single host machine.</span></span> 

## <a name="logical-architecture-diagram"></a><span data-ttu-id="de863-106">Diagrama de arquitectura lógica</span><span class="sxs-lookup"><span data-stu-id="de863-106">Logical architecture diagram</span></span>
<span data-ttu-id="de863-107">Hello diagrama siguiente ilustra la arquitectura lógica de hello del kit de desarrollo de hello pila de Azure y sus componentes.</span><span class="sxs-lookup"><span data-stu-id="de863-107">hello following diagram illustrates hello logical architecture of hello Azure Stack development kit and its components.</span></span>

![](media/azure-stack-architecture/image1.png)

## <a name="virtual-machine-roles"></a><span data-ttu-id="de863-108">Roles de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="de863-108">Virtual machine roles</span></span>
<span data-ttu-id="de863-109">Hola kit de desarrollo de la pila de Azure ofrece servicios mediante Hola siguiendo las máquinas virtuales en el host de hello:</span><span class="sxs-lookup"><span data-stu-id="de863-109">hello Azure Stack development kit offers services using hello following VMs on hello host:</span></span>

| <span data-ttu-id="de863-110">Nombre</span><span class="sxs-lookup"><span data-stu-id="de863-110">Name</span></span> | <span data-ttu-id="de863-111">Descripción</span><span class="sxs-lookup"><span data-stu-id="de863-111">Description</span></span> |
| ----- | ----- |
| <span data-ttu-id="de863-112">**AzS-ACS01**</span><span class="sxs-lookup"><span data-stu-id="de863-112">**AzS-ACS01**</span></span> | <span data-ttu-id="de863-113">Servicios de almacenamiento de Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="de863-113">Azure Stack storage services.</span></span>|
| <span data-ttu-id="de863-114">**AzS-ADFS01**</span><span class="sxs-lookup"><span data-stu-id="de863-114">**AzS-ADFS01**</span></span> | <span data-ttu-id="de863-115">Servicios de federación de Active Directory (AD FS).</span><span class="sxs-lookup"><span data-stu-id="de863-115">Active Directory Federation Services (ADFS).</span></span>  |
| <span data-ttu-id="de863-116">**AzS-BGPNAT01**</span><span class="sxs-lookup"><span data-stu-id="de863-116">**AzS-BGPNAT01**</span></span> | <span data-ttu-id="de863-117">Enrutador perimetral que proporciona funcionalidades de NAT y VPN para Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="de863-117">Edge router and provides NAT and VPN capabilities for Azure Stack.</span></span> |
| <span data-ttu-id="de863-118">**AzS-CA01**</span><span class="sxs-lookup"><span data-stu-id="de863-118">**AzS-CA01**</span></span> | <span data-ttu-id="de863-119">Servicios de entidad de certificación para servicios de rol de Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="de863-119">Certificate authority services for Azure Stack role services.</span></span>|
| <span data-ttu-id="de863-120">**AzS-DC01**</span><span class="sxs-lookup"><span data-stu-id="de863-120">**AzS-DC01**</span></span> | <span data-ttu-id="de863-121">Servicios de Active Directory, DNS y DHCP para Microsoft Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="de863-121">Active Directory, DNS, and DHCP services for Microsoft Azure Stack.</span></span>|
| <span data-ttu-id="de863-122">**AzS-ERCS01**</span><span class="sxs-lookup"><span data-stu-id="de863-122">**AzS-ERCS01**</span></span> | <span data-ttu-id="de863-123">Máquina virtual de la consola de recuperación de emergencia.</span><span class="sxs-lookup"><span data-stu-id="de863-123">Emergency Recovery Console VM.</span></span> |
| <span data-ttu-id="de863-124">**AzS-GWY01**</span><span class="sxs-lookup"><span data-stu-id="de863-124">**AzS-GWY01**</span></span> | <span data-ttu-id="de863-125">Servicios perimetrales de puerta de enlace, como las conexiones de sitio a sitio de VPN para redes de inquilinos.</span><span class="sxs-lookup"><span data-stu-id="de863-125">Edge gateway services such as VPN site-to-site connections for tenant networks.</span></span>|
| <span data-ttu-id="de863-126">**AzS-NC01**</span><span class="sxs-lookup"><span data-stu-id="de863-126">**AzS-NC01**</span></span> | <span data-ttu-id="de863-127">Controladora de red, que administra los servicios de red de Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="de863-127">Network Controller, which manages Azure Stack network services.</span></span>  |
| <span data-ttu-id="de863-128">**AzS-SLB01**</span><span class="sxs-lookup"><span data-stu-id="de863-128">**AzS-SLB01**</span></span> | <span data-ttu-id="de863-129">Servicios de multiplexor del equilibrio de carga en Azure Stack para los inquilinos y los servicios de infraestructura de Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="de863-129">Load balancing multiplexer services in Azure Stack for both tenants and Azure Stack infrastructure services.</span></span>  |
| <span data-ttu-id="de863-130">**AzS-SQL01**</span><span class="sxs-lookup"><span data-stu-id="de863-130">**AzS-SQL01**</span></span> | <span data-ttu-id="de863-131">Almacén de datos internos para los roles de infraestructura de Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="de863-131">Internal data store for Azure Stack infrastructure roles.</span></span>  |
| <span data-ttu-id="de863-132">**AzS-WAS01**</span><span class="sxs-lookup"><span data-stu-id="de863-132">**AzS-WAS01**</span></span> | <span data-ttu-id="de863-133">Portal de administración de Azure Stack y servicios de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="de863-133">Azure Stack administrative portal and Azure Resource Manager services.</span></span>|
| <span data-ttu-id="de863-134">**AzS-WASP01**</span><span class="sxs-lookup"><span data-stu-id="de863-134">**AzS-WASP01**</span></span>| <span data-ttu-id="de863-135">Portal del usuario (inquilino) de Azure Stack y servicios de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="de863-135">Azure Stack user (tenant) portal and Azure Resource Manager services.</span></span>|
| <span data-ttu-id="de863-136">**AzS-XRP01**</span><span class="sxs-lookup"><span data-stu-id="de863-136">**AzS-XRP01**</span></span> | <span data-ttu-id="de863-137">Controlador de administración de infraestructura para la pila de Microsoft Azure, incluidos los proveedores de recursos de proceso, red y almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="de863-137">Infrastructure management controller for Microsoft Azure Stack, including hello Compute, Network, and Storage resource providers.</span></span>|


## <a name="next-steps"></a><span data-ttu-id="de863-138">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="de863-138">Next steps</span></span>
[<span data-ttu-id="de863-139">Implementación de Azure Stack</span><span class="sxs-lookup"><span data-stu-id="de863-139">Deploy Azure Stack</span></span>](azure-stack-deploy.md)

[<span data-ttu-id="de863-140">Primera tootry escenarios</span><span class="sxs-lookup"><span data-stu-id="de863-140">First scenarios tootry</span></span>](azure-stack-first-scenarios.md)

