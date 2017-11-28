---
title: "Profundización técnica en la migración compatible con la plataforma de la implementación clásica a la de Azure Resource Manager | Microsoft Docs"
description: "En este artículo se realiza una profundización técnica en la migración compatible con la plataforma de la implementación clásica a la de Azure Resource Manager."
services: virtual-machines-linux
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 29267453-f894-4180-bb67-dce2a0e062bb
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: kasing
ms.openlocfilehash: 557a61f266c494cb6b8003cff945fa1a14348898
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="technical-deep-dive-on-platform-supported-migration-from-classic-to-azure-resource-manager"></a><span data-ttu-id="f3f59-103">Profundización técnica en la migración compatible con la plataforma de la implementación clásica a la de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f3f59-103">Technical deep dive on platform-supported migration from classic to Azure Resource Manager</span></span>

<span data-ttu-id="f3f59-104">Profundicemos en la migración desde el modelo de implementación clásica de Azure hasta el modelo de implementación de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="f3f59-104">Let's take a deep-dive on migrating from the Azure classic deployment model to the Azure Resource Manager deployment model.</span></span> <span data-ttu-id="f3f59-105">Nos centramos en los recursos en un nivel de recursos y función que le ayudarán a comprender cómo la Plataforma de Azure migra los recursos entre los dos modelos de implementación.</span><span class="sxs-lookup"><span data-stu-id="f3f59-105">We look at resources at a resource and feature level to help you understand how the Azure platform migrates resources between the two deployment models.</span></span> <span data-ttu-id="f3f59-106">Para más información, lea el artículo de anuncio de servicio [Migración compatible con la plataforma de recursos de IaaS del modelo clásico al de Azure Resource Manager](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f3f59-106">For more information, please read the service announcement article: [Platform-supported migration of IaaS resources from classic to Azure Resource Manager](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-migration-deep-dive](../../../includes/virtual-machines-common-classic-resource-manager-migration-deep-dive.md)]

## <a name="next-steps"></a><span data-ttu-id="f3f59-107">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f3f59-107">Next steps</span></span>

* [<span data-ttu-id="f3f59-108">Información general sobre la migración compatible con la plataforma de recursos de IaaS desde el modelo de implementación clásica a Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f3f59-108">Overview of platform-supported migration of IaaS resources from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* <span data-ttu-id="f3f59-109">[Planning for migration of IaaS resources from classic to Azure Resource Manager](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Planificación de la migración de recursos de IaaS del modelo clásico a Azure Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="f3f59-109">[Planning for migration of IaaS resources from classic to Azure Resource Manager](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>
* [<span data-ttu-id="f3f59-110">Migración de recursos de IaaS de la implementación clásica a Resource Manager con Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="f3f59-110">Use PowerShell to migrate IaaS resources from classic to Azure Resource Manager</span></span>](../windows/migration-classic-resource-manager-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="f3f59-111">Migración de recursos de IaaS de la implementación clásica a Azure Resource Manager con la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="f3f59-111">Use CLI to migrate IaaS resources from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="f3f59-112">Herramientas de la comunidad para ayudar con la migración de recursos de IaaS de la versión clásica a Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f3f59-112">Community tools for assisting with migration of IaaS resources from classic to Azure Resource Manager</span></span>](../windows/migration-classic-resource-manager-community-tools.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="f3f59-113">Revisión de los errores más comunes en la migración</span><span class="sxs-lookup"><span data-stu-id="f3f59-113">Review most common migration errors</span></span>](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="f3f59-114">Revisión de las preguntas más frecuentes acerca de cómo migrar recursos de IaaS de la versión clásica a Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f3f59-114">Review the most frequently asked questions about migrating IaaS resources from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
