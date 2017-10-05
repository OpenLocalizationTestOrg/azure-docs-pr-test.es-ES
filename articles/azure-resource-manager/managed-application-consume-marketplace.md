---
title: Uso de aplicaciones administradas de Azure en Marketplace | Microsoft Docs
description: "En este artículo se describe la creación de una aplicación administrada de Azure que está disponible a través de Marketplace."
services: azure-resource-manager
author: ravbhatnagar
manager: rjmax
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/11/2017
ms.author: gauravbh; tomfitz
ms.openlocfilehash: baf456740bddd562391ed64d707f990c8921d710
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/29/2017
---
# <a name="consume-azure-managed-applications-in-the-marketplace"></a><span data-ttu-id="12404-103">Uso de aplicaciones administradas de Azure en Marketplace</span><span class="sxs-lookup"><span data-stu-id="12404-103">Consume Azure managed applications in the Marketplace</span></span>

<span data-ttu-id="12404-104">Tal y como se describe en el artículo [Información general de las aplicaciones administradas](managed-application-overview.md), hay dos escenarios en la experiencia completa.</span><span class="sxs-lookup"><span data-stu-id="12404-104">As discussed in the [Managed Application overview](managed-application-overview.md) article, there are two scenarios in the end to end experience.</span></span> <span data-ttu-id="12404-105">Uno es el publicador o proveedor que desea crear una aplicación administrada para que la utilicen los usuarios.</span><span class="sxs-lookup"><span data-stu-id="12404-105">One is the publisher or vendor who wants to create a managed application for use by customers.</span></span> <span data-ttu-id="12404-106">El segundo es el usuario final de la aplicación administrada.</span><span class="sxs-lookup"><span data-stu-id="12404-106">The second is the end customer or the consumer of the managed application.</span></span> <span data-ttu-id="12404-107">Este artículo trata el segundo escenario.</span><span class="sxs-lookup"><span data-stu-id="12404-107">This article covers the second scenario.</span></span> <span data-ttu-id="12404-108">Describe cómo se puede implementar una aplicación administrada de Microsoft Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="12404-108">It describes how you can deploy a managed application from the Microsoft Azure Marketplace.</span></span>

## <a name="create-from-the-marketplace"></a><span data-ttu-id="12404-109">Creación desde Marketplace</span><span class="sxs-lookup"><span data-stu-id="12404-109">Create from the Marketplace</span></span>

<span data-ttu-id="12404-110">Implementar una aplicación administrada de Marketplace es similar a la implementación de cualquier tipo de recursos de Marketplace.</span><span class="sxs-lookup"><span data-stu-id="12404-110">Deploying a managed application from the Marketplace is similar to deploying any type of resources from the Marketplace.</span></span> 

<span data-ttu-id="12404-111">En el portal, seleccione **+ Nuevo** y busque el tipo de solución para implementar.</span><span class="sxs-lookup"><span data-stu-id="12404-111">In the portal, select **+ New** and search for the type of solution to deploy.</span></span> <span data-ttu-id="12404-112">Entre las opciones disponibles, seleccione la que necesita.</span><span class="sxs-lookup"><span data-stu-id="12404-112">From the available options, select the one you need.</span></span>

![Búsqueda de soluciones](./media/managed-application-consume-marketplace/search-apps.png)

<span data-ttu-id="12404-114">Revise el resumen de la aplicación y seleccione **Crear**.</span><span class="sxs-lookup"><span data-stu-id="12404-114">Review the summary of the application, and select **Create**.</span></span>

![Creación de aplicación administrada](./media/managed-application-consume-marketplace/create-marketplace-managed-app.png)

<span data-ttu-id="12404-116">Al igual que cualquier otra solución, se presentan diversos campos para los que debe proporcionar valores.</span><span class="sxs-lookup"><span data-stu-id="12404-116">Like any other solution, you are presented with fields to provide values for.</span></span> <span data-ttu-id="12404-117">Estos campos varían según el tipo de aplicación administrada que se cree.</span><span class="sxs-lookup"><span data-stu-id="12404-117">These fields vary by the type of managed application you create.</span></span> 

## <a name="view-support-information"></a><span data-ttu-id="12404-118">Ver la información de soporte técnico</span><span class="sxs-lookup"><span data-stu-id="12404-118">View support information</span></span>

<span data-ttu-id="12404-119">Una vez implementada una aplicación administrada, puede ver la información de soporte técnico para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="12404-119">After your managed application has deployed, view the support information for the application.</span></span> <span data-ttu-id="12404-120">En la hoja de la aplicación administrada, se muestra la información de soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="12404-120">In the managed application blade, the support information is listed.</span></span>

![support](./media/managed-application-consume-marketplace/support.png)

## <a name="view-publisher-permissions"></a><span data-ttu-id="12404-122">Ver los permisos del publicador</span><span class="sxs-lookup"><span data-stu-id="12404-122">View publisher permissions</span></span>

<span data-ttu-id="12404-123">Al proveedor que administra la aplicación se le concede acceso a sus recursos.</span><span class="sxs-lookup"><span data-stu-id="12404-123">The vendor that manages your application is granted access to your resources.</span></span> <span data-ttu-id="12404-124">Para ver los permisos, seleccione **Autorizaciones**.</span><span class="sxs-lookup"><span data-stu-id="12404-124">To see those permissions, select **Authorizations**.</span></span>

![Autorizaciones](./media/managed-application-consume-marketplace/authorizations.png)

## <a name="next-steps"></a><span data-ttu-id="12404-126">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="12404-126">Next steps</span></span>

* <span data-ttu-id="12404-127">Para información sobre cómo publicar aplicaciones administradas en Marketplace, consulte [Aplicaciones administradas de Azure en Marketplace](managed-application-author-marketplace.md).</span><span class="sxs-lookup"><span data-stu-id="12404-127">For information about publishing a managed application in the Marketplace, see [Azure Managed Applications in Marketplace](managed-application-author-marketplace.md).</span></span>
* <span data-ttu-id="12404-128">Para publicar aplicaciones administradas que solo están disponibles para los usuarios de su organización, consulte [Creación y publicación de una aplicación administrada del catálogo de servicios](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="12404-128">To publish managed applications that are only available to users in your organization, see [Create and publish Service Catalog Managed Application](managed-application-publishing.md).</span></span>
* <span data-ttu-id="12404-129">Para utilizar aplicaciones administradas que solo están disponibles para los usuarios de su organización, consulte [Utilización de una aplicación administrada del catálogo de servicios](managed-application-consumption.md).</span><span class="sxs-lookup"><span data-stu-id="12404-129">To consume managed applications that are only available to users in your organization, see [Consume a Service Catalog Managed Application](managed-application-consumption.md).</span></span>