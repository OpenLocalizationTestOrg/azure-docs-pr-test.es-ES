---
title: "aaaGuide toocreating una plantilla de solución para hello Marketplace | Documentos de Microsoft"
description: "Instrucciones detalladas de cómo toocreate, certificar e implementar una plantilla de solución de imagen de varias VM a la venta en hello Azure Marketplace."
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
ms.openlocfilehash: b0e7067176337dd0d3f6f6ec04c963f80f706ab0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="guide-toocreate-a-solution-template-for-azure-marketplace"></a><span data-ttu-id="321fd-103">Guía de toocreate una plantilla de solución de Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="321fd-103">Guide toocreate a solution template for Azure Marketplace</span></span>
<span data-ttu-id="321fd-104">Después de completar el paso 1, [creación de cuentas y registro][link-acct-creation], se le han guiado durante la creación de hello de una plantilla de solución de Azure compatible en [técnicos requisitos previos para crear un plantilla de solución](marketplace-publishing-solution-template-creation-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="321fd-104">After completing step 1, [Account creation and registration][link-acct-creation], we guided you on hello creation of an Azure-compatible solution template at [Technical prerequisites for creating a solution template](marketplace-publishing-solution-template-creation-prerequisites.md).</span></span> <span data-ttu-id="321fd-105">Ahora se le guiará por los pasos de Hola para crear una plantilla de solución para varias máquinas virtuales en hello [Portal de publicación] [ link-pubportal] para hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="321fd-105">Now we will walk you through hello steps for creating a solution template for multiple VMs on hello [Publishing Portal][link-pubportal] for hello Azure Marketplace.</span></span>

## <a name="create-your-solution-template-offer-in-hello-publishing-portal"></a><span data-ttu-id="321fd-106">Crear su oferta de la plantilla de solución en hello Portal de publicación</span><span class="sxs-lookup"><span data-stu-id="321fd-106">Create your solution template offer in hello Publishing Portal</span></span>
<span data-ttu-id="321fd-107">Vaya demasiado [https://publish.windowsazure.com](http://publish.windowsazure.com). Al iniciar sesión por hello primera hora toohello [Portal de publicación](https://publish.windowsazure.com/), Hola uso misma cuenta con la que se registró el perfil de vendedor de su empresa.</span><span class="sxs-lookup"><span data-stu-id="321fd-107">Go too [https://publish.windowsazure.com](http://publish.windowsazure.com). When signing in for hello first time toohello [Publishing Portal](https://publish.windowsazure.com/), use hello same account with which your company’s seller profile was registered.</span></span> <span data-ttu-id="321fd-108">Más adelante, puede agregar a cualquier empleado de la empresa como Coadministrador en hello Portal de publicación.</span><span class="sxs-lookup"><span data-stu-id="321fd-108">Later, you can add any employee of your company as a co-admin in hello Publishing Portal.</span></span>

### <a name="1-select-solution-templates"></a><span data-ttu-id="321fd-109">1. Selección de "Plantillas de solución"</span><span class="sxs-lookup"><span data-stu-id="321fd-109">1. Select "Solution templates"</span></span>
  ![dibujo][img-pubportal-menu-sol-templ]

### <a name="2-create-a-new-solution-template"></a><span data-ttu-id="321fd-111">2. Creación de una plantilla de solución</span><span class="sxs-lookup"><span data-stu-id="321fd-111">2. Create a new solution template</span></span>
  ![dibujo][img-pubportal-sol-templ-new]

### <a name="3-start-with-topologies"></a><span data-ttu-id="321fd-113">3. Comienzo con topologías</span><span class="sxs-lookup"><span data-stu-id="321fd-113">3. Start with topologies</span></span>
<span data-ttu-id="321fd-114">Una plantilla de solución es un tooall "primario" de sus topologías.</span><span class="sxs-lookup"><span data-stu-id="321fd-114">A solution template is a "parent" tooall of its topologies.</span></span> <span data-ttu-id="321fd-115">Puede definir varias topologías en una oferta o plantilla de solución.</span><span class="sxs-lookup"><span data-stu-id="321fd-115">You can define multiple topologies in one offer/solution template.</span></span> <span data-ttu-id="321fd-116">Cuando una oferta se inserta toostaging, se inserta con todos sus topologías.</span><span class="sxs-lookup"><span data-stu-id="321fd-116">When an offer is pushed toostaging, it is pushed with all of its topologies.</span></span> <span data-ttu-id="321fd-117">Siga estos pasos hello toodefine su oferta:</span><span class="sxs-lookup"><span data-stu-id="321fd-117">Follow hello steps below toodefine your offer:</span></span>     

* <span data-ttu-id="321fd-118">Crear una topología: "Identificador de topología" suele ser nombre Hola de topología de hello para la plantilla de solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="321fd-118">Create a Topology: “Topology Identifier” is typically hello name of hello topology for hello solution template.</span></span> <span data-ttu-id="321fd-119">identificador de topología de Hola se usa en la dirección URL de hello tal y como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="321fd-119">hello topology identifier is used in hello URL as shown below:</span></span>

  <span data-ttu-id="321fd-120">Azure Marketplace: http://azure.microsoft.com/marketplace/partners/{PublisherNamespace}/{OfferIdentifier}{TopologyIdentifier}</span><span class="sxs-lookup"><span data-stu-id="321fd-120">Azure Marketplace: http://azure.microsoft.com/marketplace/partners/{PublisherNamespace}/{OfferIdentifier}{TopologyIdentifier}</span></span>

  <span data-ttu-id="321fd-121">Azure Portal: https://portal.azure.com/#gallery/{PublisherNamespace}.{OfferIdentifier}{TopologyIdentifier}</span><span class="sxs-lookup"><span data-stu-id="321fd-121">Azure Portal: https://portal.azure.com/#gallery/{PublisherNamespace}.{OfferIdentifier}{TopologyIdentifier}</span></span>
* <span data-ttu-id="321fd-122">Adición de una nueva versión</span><span class="sxs-lookup"><span data-stu-id="321fd-122">Add a new version.</span></span>

### <a name="4-get-your-topology-versions-certified"></a><span data-ttu-id="321fd-123">4. Certificación de las versiones de topología</span><span class="sxs-lookup"><span data-stu-id="321fd-123">4. Get your topology versions certified</span></span>
<span data-ttu-id="321fd-124">Cargar un archivo zip que contiene una versión concreta del topología Hola de tooprovision de todos los archivos necesarios.</span><span class="sxs-lookup"><span data-stu-id="321fd-124">Upload a zip file that contains all required files tooprovision that particular version of hello topology.</span></span> <span data-ttu-id="321fd-125">Este archivo zip debe contener la siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="321fd-125">This zip file must contain hello following:</span></span>

* <span data-ttu-id="321fd-126">Los archivos *mainTemplate.json* y *createUiDefinition.json* en su directorio raíz.</span><span class="sxs-lookup"><span data-stu-id="321fd-126">*mainTemplate.json* and *createUiDefinition.json* file at its root directory.</span></span>
* <span data-ttu-id="321fd-127">Las plantillas vinculadas y todos los scripts requeridos.</span><span class="sxs-lookup"><span data-stu-id="321fd-127">Any linked templates and all required scripts.</span></span>

  > [!TIP]
  > <span data-ttu-id="321fd-128">Mientras los desarrolladores trabajan sobre cómo crear soluciones de hello topologías de plantilla y obtenerlas certificada, negocio hello, departamentos de marketing o legales de la empresa pueden trabajar en el contenido de marketing y legal de Hola.</span><span class="sxs-lookup"><span data-stu-id="321fd-128">While your developers work on creating hello solution template topologies and getting them certified, hello business, marketing, and/or legal departments of your company can work on hello marketing and legal content.</span></span>
  >
  >

## <a name="next-steps"></a><span data-ttu-id="321fd-129">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="321fd-129">Next steps</span></span>
<span data-ttu-id="321fd-130">Ahora que ha creado la plantilla de solución y cargado el archivo zip de hello, siga las instrucciones de Hola Hola [Guía de contenido de marketing de Marketplace](marketplace-publishing-push-to-staging.md) antes de insertar Hola oferta toostaging.</span><span class="sxs-lookup"><span data-stu-id="321fd-130">Now that you created your solution template and uploaded hello zip file, please follow hello instructions in hello [Marketplace marketing content guide](marketplace-publishing-push-to-staging.md) before pushing hello offer toostaging.</span></span> <span data-ttu-id="321fd-131">conjunto completo de hello toosee de marketplace publicar artículos, visite [Introducción: cómo toopublish una toohello de oferta de Azure Marketplace](marketplace-publishing-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="321fd-131">toosee hello full set of marketplace publishing articles, visit [Getting started: How toopublish an offer toohello Azure Marketplace](marketplace-publishing-getting-started.md).</span></span>

<span data-ttu-id="321fd-132">Es posible que también le interesen los siguientes artículos relacionados:</span><span class="sxs-lookup"><span data-stu-id="321fd-132">You might also be interested in these related articles:</span></span>

* <span data-ttu-id="321fd-133">Imágenes de máquinas virtuales: [Acerca de las imágenes de máquina virtual en Azure](https://msdn.microsoft.com/library/azure/dn790290.aspx)</span><span class="sxs-lookup"><span data-stu-id="321fd-133">VM images: [About Virtual Machine Images in Azure](https://msdn.microsoft.com/library/azure/dn790290.aspx)</span></span>
* <span data-ttu-id="321fd-134">Extensiones de VM: [Información general del agente de máquina virtual y las extensiones de VM](https://msdn.microsoft.com/library/azure/dn832621.aspx) y [Características y extensiones de máquina virtual de Azure](https://msdn.microsoft.com/library/azure/dn606311.aspx)</span><span class="sxs-lookup"><span data-stu-id="321fd-134">VM extensions: [VM Agent and VM Extensions Overview](https://msdn.microsoft.com/library/azure/dn832621.aspx) and [Azure VM Extensions and Features](https://msdn.microsoft.com/library/azure/dn606311.aspx)</span></span>
* <span data-ttu-id="321fd-135">Azure Resource Manager: [Creación de plantillas de Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) y [Ejemplos sencillos de plantillas](https://github.com/rjmax/ArmExamples)</span><span class="sxs-lookup"><span data-stu-id="321fd-135">Azure Resource Manager: [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md) and [Simple Template Examples](https://github.com/rjmax/ArmExamples)</span></span>
* <span data-ttu-id="321fd-136">Limita la cuenta de almacenamiento: [cómo tooMonitor para la limitación de la cuenta de almacenamiento](http://blogs.msdn.com/b/mast/archive/2014/08/02/how-to-monitor-for-storage-account-throttling.aspx) y [almacenamiento Premium](../storage/common/storage-premium-storage.md#scalability-and-performance-targets)</span><span class="sxs-lookup"><span data-stu-id="321fd-136">Storage account throttles: [How tooMonitor for Storage Account Throttling](http://blogs.msdn.com/b/mast/archive/2014/08/02/how-to-monitor-for-storage-account-throttling.aspx) and [Premium storage](../storage/common/storage-premium-storage.md#scalability-and-performance-targets)</span></span>

[img-pubportal-menu-sol-templ]:media/marketplace-publishing-solution-template-creation/pubportal-menu-solution-templates.png
[img-pubportal-sol-templ-new]:media/marketplace-publishing-solution-template-creation/pubportal-solution-template-new.png
[link-acct-creation]:marketplace-publishing-accounts-creation-registration.md
[link-pubportal]:https://publish.windowsazure.com
