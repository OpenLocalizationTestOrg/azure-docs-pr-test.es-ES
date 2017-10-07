---
title: "Aplicación administrada de Azure en marketplace aaaConsume | Documentos de Microsoft"
description: "Toocreate describe una aplicación administrada de Azure que está disponible a través de hello Marketplace."
services: azure-resource-manager
author: ravbhatnagar
manager: rjmax
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/11/2017
ms.author: gauravbh; tomfitz
ms.openlocfilehash: 9ae6e11a3f63eb58a9f3199364b5606a7afe5618
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="consume-azure-managed-applications-in-hello-marketplace"></a><span data-ttu-id="7b346-103">Consumir Azure administra las aplicaciones de hello Marketplace</span><span class="sxs-lookup"><span data-stu-id="7b346-103">Consume Azure managed applications in hello Marketplace</span></span>

<span data-ttu-id="7b346-104">Según lo descrito en hello [información general de la aplicación administrada](managed-application-overview.md) artículo, hay dos escenarios en hello final tooend experiencia.</span><span class="sxs-lookup"><span data-stu-id="7b346-104">As discussed in hello [Managed Application overview](managed-application-overview.md) article, there are two scenarios in hello end tooend experience.</span></span> <span data-ttu-id="7b346-105">Uno es el publicador de Hola o el proveedor que desea toocreate una aplicación administrada para su uso por los clientes.</span><span class="sxs-lookup"><span data-stu-id="7b346-105">One is hello publisher or vendor who wants toocreate a managed application for use by customers.</span></span> <span data-ttu-id="7b346-106">en segundo lugar, Hello es cliente de final de Hola o un consumidor de Hola de aplicación hello administrado.</span><span class="sxs-lookup"><span data-stu-id="7b346-106">hello second is hello end customer or hello consumer of hello managed application.</span></span> <span data-ttu-id="7b346-107">Este artículo trata el segundo escenario de Hola.</span><span class="sxs-lookup"><span data-stu-id="7b346-107">This article covers hello second scenario.</span></span> <span data-ttu-id="7b346-108">Describe cómo se puede implementar una aplicación administrada de hello Microsoft Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="7b346-108">It describes how you can deploy a managed application from hello Microsoft Azure Marketplace.</span></span>

## <a name="create-from-hello-marketplace"></a><span data-ttu-id="7b346-109">Crear a partir de hello Marketplace</span><span class="sxs-lookup"><span data-stu-id="7b346-109">Create from hello Marketplace</span></span>

<span data-ttu-id="7b346-110">Implementar una aplicación administrada de hello Marketplace es similar toodeploying cualquier tipo de recursos de hello Marketplace.</span><span class="sxs-lookup"><span data-stu-id="7b346-110">Deploying a managed application from hello Marketplace is similar toodeploying any type of resources from hello Marketplace.</span></span> 

<span data-ttu-id="7b346-111">En el portal de hello, seleccione **+ nuevo** y Buscar tipo hello de solución toodeploy.</span><span class="sxs-lookup"><span data-stu-id="7b346-111">In hello portal, select **+ New** and search for hello type of solution toodeploy.</span></span> <span data-ttu-id="7b346-112">En opciones disponibles de hello, seleccione Hola que necesita.</span><span class="sxs-lookup"><span data-stu-id="7b346-112">From hello available options, select hello one you need.</span></span>

![Búsqueda de soluciones](./media/managed-application-consume-marketplace/search-apps.png)

<span data-ttu-id="7b346-114">Revise el resumen de Hola de aplicación hello y seleccione **crear**.</span><span class="sxs-lookup"><span data-stu-id="7b346-114">Review hello summary of hello application, and select **Create**.</span></span>

![Creación de aplicación administrada](./media/managed-application-consume-marketplace/create-marketplace-managed-app.png)

<span data-ttu-id="7b346-116">Al igual que cualquier otra solución, se presentan con valores de campos tooprovide para.</span><span class="sxs-lookup"><span data-stu-id="7b346-116">Like any other solution, you are presented with fields tooprovide values for.</span></span> <span data-ttu-id="7b346-117">Estos campos varían según el tipo de saludo de la aplicación administrada que se cree.</span><span class="sxs-lookup"><span data-stu-id="7b346-117">These fields vary by hello type of managed application you create.</span></span> 

## <a name="view-support-information"></a><span data-ttu-id="7b346-118">Ver la información de soporte técnico</span><span class="sxs-lookup"><span data-stu-id="7b346-118">View support information</span></span>

<span data-ttu-id="7b346-119">Una vez implementada una aplicación administrada, ver información de soporte técnico de hello para la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="7b346-119">After your managed application has deployed, view hello support information for hello application.</span></span> <span data-ttu-id="7b346-120">En la hoja de la aplicación administrada de hello, se muestra información de soporte técnico de Hola.</span><span class="sxs-lookup"><span data-stu-id="7b346-120">In hello managed application blade, hello support information is listed.</span></span>

![support](./media/managed-application-consume-marketplace/support.png)

## <a name="view-publisher-permissions"></a><span data-ttu-id="7b346-122">Ver los permisos del publicador</span><span class="sxs-lookup"><span data-stu-id="7b346-122">View publisher permissions</span></span>

<span data-ttu-id="7b346-123">proveedor de Hola que administra la aplicación se concede acceso a los recursos de tooyour.</span><span class="sxs-lookup"><span data-stu-id="7b346-123">hello vendor that manages your application is granted access tooyour resources.</span></span> <span data-ttu-id="7b346-124">toosee esos permisos, seleccione **autorizaciones**.</span><span class="sxs-lookup"><span data-stu-id="7b346-124">toosee those permissions, select **Authorizations**.</span></span>

![Autorizaciones](./media/managed-application-consume-marketplace/authorizations.png)

## <a name="next-steps"></a><span data-ttu-id="7b346-126">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7b346-126">Next steps</span></span>

* <span data-ttu-id="7b346-127">Para obtener información acerca de cómo publicar una aplicación administrada en hello Marketplace, vea [las aplicaciones administradas de Azure en Marketplace](managed-application-author-marketplace.md).</span><span class="sxs-lookup"><span data-stu-id="7b346-127">For information about publishing a managed application in hello Marketplace, see [Azure Managed Applications in Marketplace](managed-application-author-marketplace.md).</span></span>
* <span data-ttu-id="7b346-128">toopublish administra las aplicaciones que están únicamente disponibles toousers en su organización, consulte [crear y publicar aplicación de servicio catálogo administrada](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="7b346-128">toopublish managed applications that are only available toousers in your organization, see [Create and publish Service Catalog Managed Application](managed-application-publishing.md).</span></span>
* <span data-ttu-id="7b346-129">tooconsume administra las aplicaciones que están únicamente disponibles toousers en su organización, consulte [consumir una aplicación de servicio catálogo administrada](managed-application-consumption.md).</span><span class="sxs-lookup"><span data-stu-id="7b346-129">tooconsume managed applications that are only available toousers in your organization, see [Consume a Service Catalog Managed Application](managed-application-consumption.md).</span></span>
