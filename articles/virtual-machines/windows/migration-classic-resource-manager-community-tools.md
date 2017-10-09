---
title: "herramientas de aaaCommunity - mover recursos clásicos tooAzure el Administrador de recursos | Documentos de Microsoft"
description: "Estas herramientas de Hola de catálogos de artículo que se han proporcionado por hello Comunidad toohelp migración recursos de IaaS de modelo de implementación de Azure Resource Manager toohello clásico."
services: virtual-machines-windows
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 228b697b-3950-49f5-84bb-283bb56621b1
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: kasing
ms.openlocfilehash: 67d5624a14d12a2d9eb46eb12aef461b706d4589
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="community-tools-toomigrate-iaas-resources-from-classic-tooazure-resource-manager"></a><span data-ttu-id="16abd-103">Comunidad de las herramientas toomigrate recursos de IaaS de tooAzure clásico Administrador de recursos</span><span class="sxs-lookup"><span data-stu-id="16abd-103">Community tools toomigrate IaaS resources from classic tooAzure Resource Manager</span></span>
<span data-ttu-id="16abd-104">Estas herramientas de Hola de catálogos de artículo que Hola Comunidad tooassist han proporcionado con la migración de los recursos de IaaS de modelo de implementación de Azure Resource Manager toohello clásico.</span><span class="sxs-lookup"><span data-stu-id="16abd-104">This article catalogs hello tools that have been provided by hello community tooassist with migration of IaaS resources from classic toohello Azure Resource Manager deployment model.</span></span>

> [!NOTE]
> <span data-ttu-id="16abd-105">Estas herramientas no se incluyen en el soporte técnico de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="16abd-105">These tools are not officially supported by Microsoft Support.</span></span> <span data-ttu-id="16abd-106">Por lo tanto, están disponibles con origen en GitHub y estamos pr tooaccept encantados de correcciones o escenarios adicionales.</span><span class="sxs-lookup"><span data-stu-id="16abd-106">Therefore they are open sourced on GitHub and we're happy tooaccept PRs for fixes or additional scenarios.</span></span> <span data-ttu-id="16abd-107">tooreport un problema, utilice hello GitHub emite característica.</span><span class="sxs-lookup"><span data-stu-id="16abd-107">tooreport an issue, use hello GitHub issues feature.</span></span>
> 
> <span data-ttu-id="16abd-108">La migración con estas herramientas provocará tiempo de inactividad en la máquina virtual clásica.</span><span class="sxs-lookup"><span data-stu-id="16abd-108">Migrating with these tools will cause downtime for your classic Virtual Machine.</span></span> <span data-ttu-id="16abd-109">Si lo que busca es información sobre la migración compatible con la plataforma, visite</span><span class="sxs-lookup"><span data-stu-id="16abd-109">If you're looking for platform supported migration, visit</span></span> 
> 
>   * [<span data-ttu-id="16abd-110">Migración de plataforma admitida de los recursos de IaaS de pila del Administrador de recursos de tooAzure clásico</span><span class="sxs-lookup"><span data-stu-id="16abd-110">Platform supported migration of IaaS resources from Classic tooAzure Resource Manager stack</span></span>](migration-classic-resource-manager-overview.md)
>   * [<span data-ttu-id="16abd-111">Técnica profundización en plataforma admite migración de clásico tooAzure el Administrador de recursos</span><span class="sxs-lookup"><span data-stu-id="16abd-111">Technical Deep Dive on Platform supported migration from Classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-deep-dive.md)
>   * [<span data-ttu-id="16abd-112">Migrar recursos de IaaS de clásico tooAzure Administrador de recursos del uso de PowerShell de Azure</span><span class="sxs-lookup"><span data-stu-id="16abd-112">Migrate IaaS resources from Classic tooAzure Resource Manager using Azure PowerShell</span></span>](migration-classic-resource-manager-ps.md)
> 
> 

## <a name="asmmetadataparser"></a><span data-ttu-id="16abd-113">AsmMetadataParser</span><span class="sxs-lookup"><span data-stu-id="16abd-113">AsmMetadataParser</span></span>
<span data-ttu-id="16abd-114">Se trata de una colección de herramientas auxiliares creados como parte de las migraciones de empresa de tooAzure Administrador de recursos de administración de servicios de Azure.</span><span class="sxs-lookup"><span data-stu-id="16abd-114">This is a collection of helper tools created as part of enterprise migrations from Azure Service Management tooAzure Resource Manager.</span></span> <span data-ttu-id="16abd-115">Esta herramienta le permite tooreplicate la infraestructura en otra suscripción que puede utilizarse para probar la migración y coloque los posibles problemas antes de ejecutar la migración de hello en su suscripción de producción.</span><span class="sxs-lookup"><span data-stu-id="16abd-115">This tool allows you tooreplicate your infrastructure into another subscription which can be used for testing migration and iron out any issues before running hello migration on your Production subscription.</span></span>

[<span data-ttu-id="16abd-116">Documentación de la herramienta de vínculo toohello</span><span class="sxs-lookup"><span data-stu-id="16abd-116">Link toohello tool documentation</span></span>](https://github.com/Azure/classic-iaas-resourcemanager-migration/tree/master/AsmToArmMigrationApiToolset)

## <a name="migaz"></a><span data-ttu-id="16abd-117">migAz</span><span class="sxs-lookup"><span data-stu-id="16abd-117">migAz</span></span>
<span data-ttu-id="16abd-118">migAz es un toomigrate un conjunto completo de recursos de IaaS de administrador de recursos de tooAzure de recursos de IaaS clásicos de opción adicional.</span><span class="sxs-lookup"><span data-stu-id="16abd-118">migAz is an additional option toomigrate a complete set of classic IaaS resources tooAzure Resource Manager IaaS resources.</span></span> <span data-ttu-id="16abd-119">Hello migración puede ocurrir dentro de hello misma suscripción o entre distintas suscripciones y tipos de suscripción (ex: suscripciones de CSP).</span><span class="sxs-lookup"><span data-stu-id="16abd-119">hello migration can occur within hello same subscription or between different subscriptions and subscription types (ex: CSP subscriptions).</span></span>

[<span data-ttu-id="16abd-120">Documentación de la herramienta de vínculo toohello</span><span class="sxs-lookup"><span data-stu-id="16abd-120">Link toohello tool documentation</span></span>](https://github.com/Azure/migAz)

## <a name="next-steps"></a><span data-ttu-id="16abd-121">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="16abd-121">Next Steps</span></span>

* [<span data-ttu-id="16abd-122">Información general de migración admitida por la plataforma de recursos de IaaS de tooAzure clásico Administrador de recursos</span><span class="sxs-lookup"><span data-stu-id="16abd-122">Overview of platform-supported migration of IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="16abd-123">Técnica de fondo admitida por la plataforma de migración de clásico tooAzure el Administrador de recursos</span><span class="sxs-lookup"><span data-stu-id="16abd-123">Technical deep dive on platform-supported migration from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-deep-dive.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="16abd-124">Planear la migración de los recursos de IaaS de tooAzure clásico Administrador de recursos</span><span class="sxs-lookup"><span data-stu-id="16abd-124">Planning for migration of IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="16abd-125">Usar recursos de IaaS PowerShell toomigrate desde tooAzure clásico Administrador de recursos</span><span class="sxs-lookup"><span data-stu-id="16abd-125">Use PowerShell toomigrate IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="16abd-126">Usar recursos de IaaS CLI toomigrate de tooAzure clásico Administrador de recursos</span><span class="sxs-lookup"><span data-stu-id="16abd-126">Use CLI toomigrate IaaS resources from classic tooAzure Resource Manager</span></span>](../linux/migration-classic-resource-manager-cli.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="16abd-127">Revisión de los errores más comunes en la migración</span><span class="sxs-lookup"><span data-stu-id="16abd-127">Review most common migration errors</span></span>](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="16abd-128">Hola de revisión más preguntas más frecuentes acerca de cómo migrar recursos de IaaS de tooAzure clásico Administrador de recursos</span><span class="sxs-lookup"><span data-stu-id="16abd-128">Review hello most frequently asked questions about migrating IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

