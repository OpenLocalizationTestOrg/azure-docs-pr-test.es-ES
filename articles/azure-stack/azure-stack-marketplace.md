---
title: Publicar un elemento de Marketplace personalizado en Azure Stack (operador de nube) | Microsoft Docs
description: "Como operador de nube, aprenda cómo publicar un elemento de Marketplace personalizado en Azure Stack."
services: azure-stack
documentationcenter: 
author: ErikjeMS
manager: byronr
editor: 
ms.assetid: 60871cbb-eed2-433c-a76d-d605c7aec06c
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: erikje
ms.openlocfilehash: be61e746d97fbce166f44262fcc33e2f7118fd82
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="the-azure-stack-marketplace-overview"></a><span data-ttu-id="af8f4-103">Información general de Azure Stack Marketplace</span><span class="sxs-lookup"><span data-stu-id="af8f4-103">The Azure Stack Marketplace overview</span></span>
<span data-ttu-id="af8f4-104">Marketplace es un conjunto de servicios, aplicaciones y recursos personalizados para Azure Stack, como redes, máquinas virtuales, almacenamiento, etc.</span><span class="sxs-lookup"><span data-stu-id="af8f4-104">The Marketplace is a collection of services, applications, and resources customized for Azure Stack, like networks, virtual machines, storage, and so on.</span></span> <span data-ttu-id="af8f4-105">Es el lugar donde los usuarios vienen para crear nuevos recursos e implementar nuevas aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="af8f4-105">Users come here to create new resources and deploy new applications.</span></span> <span data-ttu-id="af8f4-106">Piense que es como un catálogo de compras donde los usuarios pueden examinar y elegir los elementos que se quieren usar.</span><span class="sxs-lookup"><span data-stu-id="af8f4-106">Think of it as a shopping catalog where users can browse and choose the items they want to use.</span></span> <span data-ttu-id="af8f4-107">Los usuarios, para utilizar un elemento de Marketplace, deben suscribirse a una oferta que les concede acceso al elemento.</span><span class="sxs-lookup"><span data-stu-id="af8f4-107">To use a Marketplace item, users must subscribe to an offer that grants them access to the item.</span></span>

<span data-ttu-id="af8f4-108">Como operador de nube, usted decide qué elementos quiere agregar (publicar) en Marketplace.</span><span class="sxs-lookup"><span data-stu-id="af8f4-108">As a cloud operator, you decide which items to add (publish) to the Marketplace.</span></span> <span data-ttu-id="af8f4-109">Puede publicar elementos, como bases de datos, App Services, etc.</span><span class="sxs-lookup"><span data-stu-id="af8f4-109">You can publish things like databases, App Services, and so on.</span></span> <span data-ttu-id="af8f4-110">Esto hace que sean visibles para todos los usuarios.</span><span class="sxs-lookup"><span data-stu-id="af8f4-110">This makes them visible to all your users.</span></span> <span data-ttu-id="af8f4-111">Puede publicar elementos personalizados creados por usted.</span><span class="sxs-lookup"><span data-stu-id="af8f4-111">You can publish custom items that you create.</span></span> <span data-ttu-id="af8f4-112">También puede publicar elementos de una creciente [lista de elementos de Azure Marketplace](azure-stack-marketplace-azure-items.md).</span><span class="sxs-lookup"><span data-stu-id="af8f4-112">You can also publish items from a growing [list of Azure Marketplace items](azure-stack-marketplace-azure-items.md).</span></span> <span data-ttu-id="af8f4-113">Al publicar un elemento en Marketplace, los usuarios pueden verlo a los cinco minutos.</span><span class="sxs-lookup"><span data-stu-id="af8f4-113">When you publish an item to the Marketplace, users can see it within five minutes.</span></span>

<span data-ttu-id="af8f4-114">Para abrir Marketplace, haga clic en **Nuevo**.</span><span class="sxs-lookup"><span data-stu-id="af8f4-114">To open the Marketplace, click **New**.</span></span>

![](media/azure-stack-publish-custom-marketplace-item/image1.png)

## <a name="marketplace-items"></a><span data-ttu-id="af8f4-115">Elementos de Marketplace</span><span class="sxs-lookup"><span data-stu-id="af8f4-115">Marketplace items</span></span>
<span data-ttu-id="af8f4-116">Un elemento de Azure Stack Marketplace es un servicio, una aplicación o un recurso que los usuarios pueden descargar y usar.</span><span class="sxs-lookup"><span data-stu-id="af8f4-116">An Azure Stack Marketplace item is a service, application, or resource that your users can download and use.</span></span> <span data-ttu-id="af8f4-117">Todos los elementos de Azure Stack Marketplace son visibles para todos los usuarios.</span><span class="sxs-lookup"><span data-stu-id="af8f4-117">All Azure Stack Marketplace items are visible to all your users.</span></span>

<span data-ttu-id="af8f4-118">Cada elemento de Marketplace tiene:</span><span class="sxs-lookup"><span data-stu-id="af8f4-118">Every Marketplace item has:</span></span>

* <span data-ttu-id="af8f4-119">Una plantilla del Administrador de recursos de Azure para el aprovisionamiento de recursos</span><span class="sxs-lookup"><span data-stu-id="af8f4-119">An Azure Resource Manager template for resource provisioning</span></span>
* <span data-ttu-id="af8f4-120">Metadatos, como cadenas, iconos y otra documentación y material adjunto de marketing</span><span class="sxs-lookup"><span data-stu-id="af8f4-120">Metadata, like strings, icons, and other marketing collateral</span></span>
* <span data-ttu-id="af8f4-121">Información de formato para mostrar el elemento en el portal</span><span class="sxs-lookup"><span data-stu-id="af8f4-121">Formatting information to display the item in the portal</span></span>

<span data-ttu-id="af8f4-122">Cada elemento publicado en Marketplace utiliza un formato denominado paquete de galería de Azure (azpkg).</span><span class="sxs-lookup"><span data-stu-id="af8f4-122">Every item published to the Marketplace uses a format called the Azure Gallery Package (azpkg).</span></span> <span data-ttu-id="af8f4-123">Agregue recursos de implementación o de entorno en tiempo de ejecución (por ejemplo, código, archivos comprimidos con software o imágenes de máquinas virtuales) a Azure Stack por separado, no como parte del elemento de Marketplace.</span><span class="sxs-lookup"><span data-stu-id="af8f4-123">Add deployment or runtime resources (like code, zip files with software, or virtual machine images) to Azure Stack separately, not as part of the Marketplace Item.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="af8f4-124">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="af8f4-124">Next steps</span></span>
[<span data-ttu-id="af8f4-125">Crear y publicar un elemento en Marketplace</span><span class="sxs-lookup"><span data-stu-id="af8f4-125">Create and publish a marketplace item</span></span>](azure-stack-create-and-publish-marketplace-item.md)

