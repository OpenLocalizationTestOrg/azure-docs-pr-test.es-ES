---
title: "Guía para crear una plantilla de solución en Marketplace | Microsoft Docs"
description: "Se ofrecen instrucciones detalladas sobre cómo crear, certificar e implementar una plantilla de solución de imagen de varias máquinas virtuales para la venta en Azure Marketplace."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: e14e05f2-2385-4ce0-b351-0747cb74ba19
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/27/2016
ms.author: hascipio; v-divte
ms.openlocfilehash: b753bfb4bd69bd9aacf4eebd8999397394c28bc4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="guide-to-create-a-solution-template-for-azure-marketplace"></a><span data-ttu-id="db030-103">Guía para crear una plantilla de solución en Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="db030-103">Guide to create a solution template for Azure Marketplace</span></span>
<span data-ttu-id="db030-104">Después de completar el paso 1, [Creación y registro de cuentas][link-acct-creation], le guiamos en la creación de una plantilla de solución compatible con Azure en [Requisitos previos técnicos para crear una plantilla de solución](marketplace-publishing-solution-template-creation-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="db030-104">After completing step 1, [Account creation and registration][link-acct-creation], we guided you on the creation of an Azure-compatible solution template at [Technical prerequisites for creating a solution template](marketplace-publishing-solution-template-creation-prerequisites.md).</span></span> <span data-ttu-id="db030-105">Ahora le guiaremos a través de los pasos para crear una plantilla de solución de varias máquinas virtuales en el [Portal de publicación][link-pubportal] de Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="db030-105">Now we will walk you through the steps for creating a solution template for multiple VMs on the [Publishing Portal][link-pubportal] for the Azure Marketplace.</span></span>

## <a name="create-your-solution-template-offer-in-the-publishing-portal"></a><span data-ttu-id="db030-106">Creación de la oferta de plantilla de solución en el Portal de publicación</span><span class="sxs-lookup"><span data-stu-id="db030-106">Create your solution template offer in the Publishing Portal</span></span>
<span data-ttu-id="db030-107">Vaya a [https://publish.windowsazure.com](http://publish.windowsazure.com). Cuando inicie sesión por primera vez en el [Portal de publicación](https://publish.windowsazure.com/), use la misma cuenta con la que se registró el perfil de vendedor de la compañía.</span><span class="sxs-lookup"><span data-stu-id="db030-107">Go to  [https://publish.windowsazure.com](http://publish.windowsazure.com). When signing in for the first time to the [Publishing Portal](https://publish.windowsazure.com/), use the same account with which your company’s seller profile was registered.</span></span> <span data-ttu-id="db030-108">Posteriormente, puede agregar a cualquier empleado de la empresa como coadministrador en el Portal de publicación.</span><span class="sxs-lookup"><span data-stu-id="db030-108">Later, you can add any employee of your company as a co-admin in the Publishing Portal.</span></span>

### <a name="1-select-solution-templates"></a><span data-ttu-id="db030-109">1. Selección de "Plantillas de solución"</span><span class="sxs-lookup"><span data-stu-id="db030-109">1. Select "Solution templates"</span></span>
  ![dibujo][img-pubportal-menu-sol-templ]

### <a name="2-create-a-new-solution-template"></a><span data-ttu-id="db030-111">2. Creación de una plantilla de solución</span><span class="sxs-lookup"><span data-stu-id="db030-111">2. Create a new solution template</span></span>
  ![dibujo][img-pubportal-sol-templ-new]

### <a name="3-start-with-topologies"></a><span data-ttu-id="db030-113">3. Comienzo con topologías</span><span class="sxs-lookup"><span data-stu-id="db030-113">3. Start with topologies</span></span>
<span data-ttu-id="db030-114">Una plantilla de solución es una "matriz" para todas sus topologías.</span><span class="sxs-lookup"><span data-stu-id="db030-114">A solution template is a "parent" to all of its topologies.</span></span> <span data-ttu-id="db030-115">Puede definir varias topologías en una oferta o plantilla de solución.</span><span class="sxs-lookup"><span data-stu-id="db030-115">You can define multiple topologies in one offer/solution template.</span></span> <span data-ttu-id="db030-116">Cuando se inserta una oferta en un entorno de ensayo, se inserta con todas sus topologías.</span><span class="sxs-lookup"><span data-stu-id="db030-116">When an offer is pushed to staging, it is pushed with all of its topologies.</span></span> <span data-ttu-id="db030-117">Siga estos pasos para definir la oferta:</span><span class="sxs-lookup"><span data-stu-id="db030-117">Follow the steps below to define your offer:</span></span>     

* <span data-ttu-id="db030-118">Creación de una topología: el "identificador de la topología" suele ser el nombre de la topología en la plantilla de solución.</span><span class="sxs-lookup"><span data-stu-id="db030-118">Create a Topology: “Topology Identifier” is typically the name of the topology for the solution template.</span></span> <span data-ttu-id="db030-119">El identificador de la topología se usará en la dirección URL, tal como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="db030-119">The topology identifier is used in the URL as shown below:</span></span>

  <span data-ttu-id="db030-120">Azure Marketplace: http://azure.microsoft.com/marketplace/partners/{PublisherNamespace}/{OfferIdentifier}{TopologyIdentifier}</span><span class="sxs-lookup"><span data-stu-id="db030-120">Azure Marketplace: http://azure.microsoft.com/marketplace/partners/{PublisherNamespace}/{OfferIdentifier}{TopologyIdentifier}</span></span>

  <span data-ttu-id="db030-121">Azure Portal: https://portal.azure.com/#gallery/{PublisherNamespace}.{OfferIdentifier}{TopologyIdentifier}</span><span class="sxs-lookup"><span data-stu-id="db030-121">Azure Portal: https://portal.azure.com/#gallery/{PublisherNamespace}.{OfferIdentifier}{TopologyIdentifier}</span></span>
* <span data-ttu-id="db030-122">Adición de una nueva versión</span><span class="sxs-lookup"><span data-stu-id="db030-122">Add a new version.</span></span>

### <a name="4-get-your-topology-versions-certified"></a><span data-ttu-id="db030-123">4. Certificación de las versiones de topología</span><span class="sxs-lookup"><span data-stu-id="db030-123">4. Get your topology versions certified</span></span>
<span data-ttu-id="db030-124">Cargue un archivo zip que contiene todos los archivos necesarios para realizar el aprovisionamiento de esa versión específica de la topología.</span><span class="sxs-lookup"><span data-stu-id="db030-124">Upload a zip file that contains all required files to provision that particular version of the topology.</span></span> <span data-ttu-id="db030-125">Este archivo zip debe contener lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="db030-125">This zip file must contain the following:</span></span>

* <span data-ttu-id="db030-126">Los archivos *mainTemplate.json* y *createUiDefinition.json* en su directorio raíz.</span><span class="sxs-lookup"><span data-stu-id="db030-126">*mainTemplate.json* and *createUiDefinition.json* file at its root directory.</span></span>
* <span data-ttu-id="db030-127">Las plantillas vinculadas y todos los scripts requeridos.</span><span class="sxs-lookup"><span data-stu-id="db030-127">Any linked templates and all required scripts.</span></span>

  > [!TIP]
  > <span data-ttu-id="db030-128">Mientras los desarrolladores trabajan en la creación de las topologías de la plantilla de solución y en conseguir que se certifiquen, el departamento comercial, de marketing o legal de su empresa puede trabajar en el contenido de marketing y legal.</span><span class="sxs-lookup"><span data-stu-id="db030-128">While your developers work on creating the solution template topologies and getting them certified, the business, marketing, and/or legal departments of your company can work on the marketing and legal content.</span></span>
  >
  >

## <a name="next-steps"></a><span data-ttu-id="db030-129">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="db030-129">Next steps</span></span>
<span data-ttu-id="db030-130">Ahora que ha creado la plantilla de solución y cargado el archivo .zip, siga las instrucciones de la [Guía de contenido de marketing de Marketplace](marketplace-publishing-push-to-staging.md) antes de enviar la oferta al entorno de ensayo.</span><span class="sxs-lookup"><span data-stu-id="db030-130">Now that you created your solution template and uploaded the zip file, please follow the instructions in the [Marketplace marketing content guide](marketplace-publishing-push-to-staging.md) before pushing the offer to staging.</span></span> <span data-ttu-id="db030-131">Para ver el conjunto completo de artículos de la publicación de Marketplace, consulte [Introducción: Publicación de una oferta en Azure Marketplace](marketplace-publishing-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="db030-131">To see the full set of marketplace publishing articles, visit [Getting started: How to publish an offer to the Azure Marketplace](marketplace-publishing-getting-started.md).</span></span>

<span data-ttu-id="db030-132">Es posible que también le interesen los siguientes artículos relacionados:</span><span class="sxs-lookup"><span data-stu-id="db030-132">You might also be interested in these related articles:</span></span>

* <span data-ttu-id="db030-133">Imágenes de máquinas virtuales: [Acerca de las imágenes de máquina virtual en Azure](https://msdn.microsoft.com/library/azure/dn790290.aspx)</span><span class="sxs-lookup"><span data-stu-id="db030-133">VM images: [About Virtual Machine Images in Azure](https://msdn.microsoft.com/library/azure/dn790290.aspx)</span></span>
* <span data-ttu-id="db030-134">Extensiones de VM: [Información general del agente de máquina virtual y las extensiones de VM](https://msdn.microsoft.com/library/azure/dn832621.aspx) y [Características y extensiones de máquina virtual de Azure](https://msdn.microsoft.com/library/azure/dn606311.aspx)</span><span class="sxs-lookup"><span data-stu-id="db030-134">VM extensions: [VM Agent and VM Extensions Overview](https://msdn.microsoft.com/library/azure/dn832621.aspx) and [Azure VM Extensions and Features](https://msdn.microsoft.com/library/azure/dn606311.aspx)</span></span>
* <span data-ttu-id="db030-135">Azure Resource Manager: [Creación de plantillas de Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) y [Ejemplos sencillos de plantillas](https://github.com/rjmax/ArmExamples)</span><span class="sxs-lookup"><span data-stu-id="db030-135">Azure Resource Manager: [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md) and [Simple Template Examples](https://github.com/rjmax/ArmExamples)</span></span>
* <span data-ttu-id="db030-136">Limitaciones de cuentas de almacenamiento: [Supervisión de limitaciones de cuentas de almacenamiento](http://blogs.msdn.com/b/mast/archive/2014/08/02/how-to-monitor-for-storage-account-throttling.aspx) y [Premium Storage](../storage/common/storage-premium-storage.md#scalability-and-performance-targets)</span><span class="sxs-lookup"><span data-stu-id="db030-136">Storage account throttles: [How to Monitor for Storage Account Throttling](http://blogs.msdn.com/b/mast/archive/2014/08/02/how-to-monitor-for-storage-account-throttling.aspx) and [Premium storage](../storage/common/storage-premium-storage.md#scalability-and-performance-targets)</span></span>

[img-pubportal-menu-sol-templ]:media/marketplace-publishing-solution-template-creation/pubportal-menu-solution-templates.png
[img-pubportal-sol-templ-new]:media/marketplace-publishing-solution-template-creation/pubportal-solution-template-new.png
[link-acct-creation]:marketplace-publishing-accounts-creation-registration.md
[link-pubportal]:https://publish.windowsazure.com
