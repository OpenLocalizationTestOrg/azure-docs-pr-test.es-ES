---
title: aaaPublish un elemento de marketplace personalizado en la pila de Azure (operador de nube) | Documentos de Microsoft
description: "Como un operador en la nube, obtenga información acerca de cómo toopublish un mercado personalizado de elementos en la pila de Azure."
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
ms.openlocfilehash: e33e1c6574d43ada1c1c85bf77df7d0d191116aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="hello-azure-stack-marketplace-overview"></a><span data-ttu-id="6b946-103">información general de Hello Azure Marketplace de pila</span><span class="sxs-lookup"><span data-stu-id="6b946-103">hello Azure Stack Marketplace overview</span></span>
<span data-ttu-id="6b946-104">Hola Marketplace es una colección de servicios, aplicaciones y recursos personalizados para la pila de Azure, como redes, máquinas virtuales, el almacenamiento y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="6b946-104">hello Marketplace is a collection of services, applications, and resources customized for Azure Stack, like networks, virtual machines, storage, and so on.</span></span> <span data-ttu-id="6b946-105">Los usuarios venir aquí toocreate nuevos recursos e implementación aplicaciones nuevas.</span><span class="sxs-lookup"><span data-stu-id="6b946-105">Users come here toocreate new resources and deploy new applications.</span></span> <span data-ttu-id="6b946-106">Considerar como un catálogo de compra donde los usuarios pueden examinar y elija Hola elementos desee toouse.</span><span class="sxs-lookup"><span data-stu-id="6b946-106">Think of it as a shopping catalog where users can browse and choose hello items they want toouse.</span></span> <span data-ttu-id="6b946-107">toouse un elemento de Marketplace, los usuarios deben suscribirse oferta tooan que les concede el elemento toohello de acceso.</span><span class="sxs-lookup"><span data-stu-id="6b946-107">toouse a Marketplace item, users must subscribe tooan offer that grants them access toohello item.</span></span>

<span data-ttu-id="6b946-108">Como un operador en la nube, decidir qué tooadd elementos toohello Marketplace (publicar).</span><span class="sxs-lookup"><span data-stu-id="6b946-108">As a cloud operator, you decide which items tooadd (publish) toohello Marketplace.</span></span> <span data-ttu-id="6b946-109">Puede publicar elementos, como bases de datos, App Services, etc.</span><span class="sxs-lookup"><span data-stu-id="6b946-109">You can publish things like databases, App Services, and so on.</span></span> <span data-ttu-id="6b946-110">Esto hace que sean tooall visible a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="6b946-110">This makes them visible tooall your users.</span></span> <span data-ttu-id="6b946-111">Puede publicar elementos personalizados creados por usted.</span><span class="sxs-lookup"><span data-stu-id="6b946-111">You can publish custom items that you create.</span></span> <span data-ttu-id="6b946-112">También puede publicar elementos de una creciente [lista de elementos de Azure Marketplace](azure-stack-marketplace-azure-items.md).</span><span class="sxs-lookup"><span data-stu-id="6b946-112">You can also publish items from a growing [list of Azure Marketplace items](azure-stack-marketplace-azure-items.md).</span></span> <span data-ttu-id="6b946-113">Cuando se publica un toohello elemento Marketplace, los usuarios pueden ver con cinco minutos.</span><span class="sxs-lookup"><span data-stu-id="6b946-113">When you publish an item toohello Marketplace, users can see it within five minutes.</span></span>

<span data-ttu-id="6b946-114">Hola tooopen Marketplace, haga clic en **nuevo**.</span><span class="sxs-lookup"><span data-stu-id="6b946-114">tooopen hello Marketplace, click **New**.</span></span>

![](media/azure-stack-publish-custom-marketplace-item/image1.png)

## <a name="marketplace-items"></a><span data-ttu-id="6b946-115">Elementos de Marketplace</span><span class="sxs-lookup"><span data-stu-id="6b946-115">Marketplace items</span></span>
<span data-ttu-id="6b946-116">Un elemento de Azure Stack Marketplace es un servicio, una aplicación o un recurso que los usuarios pueden descargar y usar.</span><span class="sxs-lookup"><span data-stu-id="6b946-116">An Azure Stack Marketplace item is a service, application, or resource that your users can download and use.</span></span> <span data-ttu-id="6b946-117">Todos los elementos de la pila de Azure Marketplace es tooall visible a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="6b946-117">All Azure Stack Marketplace items are visible tooall your users.</span></span>

<span data-ttu-id="6b946-118">Cada elemento de Marketplace tiene:</span><span class="sxs-lookup"><span data-stu-id="6b946-118">Every Marketplace item has:</span></span>

* <span data-ttu-id="6b946-119">Una plantilla del Administrador de recursos de Azure para el aprovisionamiento de recursos</span><span class="sxs-lookup"><span data-stu-id="6b946-119">An Azure Resource Manager template for resource provisioning</span></span>
* <span data-ttu-id="6b946-120">Metadatos, como cadenas, iconos y otra documentación y material adjunto de marketing</span><span class="sxs-lookup"><span data-stu-id="6b946-120">Metadata, like strings, icons, and other marketing collateral</span></span>
* <span data-ttu-id="6b946-121">Aplicar formato a elementos de información toodisplay hello en el portal de Hola</span><span class="sxs-lookup"><span data-stu-id="6b946-121">Formatting information toodisplay hello item in hello portal</span></span>

<span data-ttu-id="6b946-122">Cada artículo publicado toohello Marketplace usa un paquete de galería de Azure (azpkg) de formato llamado hello.</span><span class="sxs-lookup"><span data-stu-id="6b946-122">Every item published toohello Marketplace uses a format called hello Azure Gallery Package (azpkg).</span></span> <span data-ttu-id="6b946-123">Agregar recursos de implementación o en tiempo de ejecución (por ejemplo, código, archivos zip con el software o imágenes de máquina virtual) tooAzure de la pila por separado, no como parte del programa Hola a elemento de Marketplace.</span><span class="sxs-lookup"><span data-stu-id="6b946-123">Add deployment or runtime resources (like code, zip files with software, or virtual machine images) tooAzure Stack separately, not as part of hello Marketplace Item.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="6b946-124">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6b946-124">Next steps</span></span>
[<span data-ttu-id="6b946-125">Crear y publicar un elemento en Marketplace</span><span class="sxs-lookup"><span data-stu-id="6b946-125">Create and publish a marketplace item</span></span>](azure-stack-create-and-publish-marketplace-item.md)

