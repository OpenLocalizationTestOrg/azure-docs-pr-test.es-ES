---
title: "Introducción a App Service: Azure Stack | Microsoft Docs"
description: "Introducción a App Service en Azure Stack"
services: azure-stack
documentationcenter: 
author: apwestgarth
manager: stefsch
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: app-service
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/3/2017
ms.author: anwestg
ms.openlocfilehash: 13928744e7d2fc145662c2a0d5c26d512cf02150
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="app-service-on-azure-stack-overview"></a><span data-ttu-id="ad676-103">Introducción a App Service en Azure Stack</span><span class="sxs-lookup"><span data-stu-id="ad676-103">App Service on Azure Stack overview</span></span>

<span data-ttu-id="ad676-104">Azure App Service en Azure Stack es la oferta de Azure para Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="ad676-104">Azure App Service on Azure Stack is the Azure offering brought to Azure Stack.</span></span> <span data-ttu-id="ad676-105">El instalador de App Service en Azure Stack crea el siguiente conjunto de instancias de rol:</span><span class="sxs-lookup"><span data-stu-id="ad676-105">The App Service on Azure Stack installer creates the following set of role instances:</span></span>

*  <span data-ttu-id="ad676-106">Controller</span><span class="sxs-lookup"><span data-stu-id="ad676-106">Controller</span></span>
*  <span data-ttu-id="ad676-107">Administración (se crean dos instancias)</span><span class="sxs-lookup"><span data-stu-id="ad676-107">Management (two instances are created)</span></span>
*  <span data-ttu-id="ad676-108">FrontEnd</span><span class="sxs-lookup"><span data-stu-id="ad676-108">FrontEnd</span></span>
*  <span data-ttu-id="ad676-109">Publicador</span><span class="sxs-lookup"><span data-stu-id="ad676-109">Publisher</span></span>
*  <span data-ttu-id="ad676-110">Trabajo (en modo compartido)</span><span class="sxs-lookup"><span data-stu-id="ad676-110">Worker (in Shared mode)</span></span>

<span data-ttu-id="ad676-111">Además, el instalador de App Service en Azure Stack crea un servidor de archivos.</span><span class="sxs-lookup"><span data-stu-id="ad676-111">In addition, the App Service on Azure Stack installer creates a file server.</span></span>
    
## <a name="whats-new-in-the-first-release-candidate-of-app-service-on-azure-stack"></a><span data-ttu-id="ad676-112">Novedades de la primera versión candidata para lanzamiento de App Service en Azure Stack</span><span class="sxs-lookup"><span data-stu-id="ad676-112">What's new in the first release candidate of App Service on Azure Stack?</span></span>
![App Service en el portal de Azure Stack][1]

<span data-ttu-id="ad676-114">La primera versión candidata para lanzamiento de App Service en Azure Stack se basa en la tercera versión preliminar y aporta mejoras y nuevas funcionalidades:</span><span class="sxs-lookup"><span data-stu-id="ad676-114">The first release candidate of App Service on Azure Stack builds on top of the third preview and brings new capabilities and improvements:</span></span>

* <span data-ttu-id="ad676-115">Azure Functions en entornos de Azure Stack basado en los Servicios de federación de Active Directory (AD FS)</span><span class="sxs-lookup"><span data-stu-id="ad676-115">Azure Functions in Azure Stack environments based on Active Directory Federation Services</span></span> 
* <span data-ttu-id="ad676-116">Compatibilidad con el inicio de sesión único para el portal de Functions y las herramientas avanzadas de desarrollador (Kudu)</span><span class="sxs-lookup"><span data-stu-id="ad676-116">Single sign-on support for the Functions portal and the advanced developer tools (Kudu)</span></span>
* <span data-ttu-id="ad676-117">Compatibilidad con Java para aplicaciones web, móviles y de API</span><span class="sxs-lookup"><span data-stu-id="ad676-117">Java support for web, mobile, and API applications</span></span>
* <span data-ttu-id="ad676-118">Administración de niveles de trabajo por conjuntos de escalado de máquinas virtuales para mejorar las funcionalidades de escalabilidad horizontal de los administradores de servicios</span><span class="sxs-lookup"><span data-stu-id="ad676-118">Management of worker tiers by virtual machine scale sets to improve scale-out capabilities for service administrators</span></span>
* <span data-ttu-id="ad676-119">Localización de la experiencia de administración</span><span class="sxs-lookup"><span data-stu-id="ad676-119">Localization of the admin experience</span></span>
* <span data-ttu-id="ad676-120">Mayor estabilidad del servicio</span><span class="sxs-lookup"><span data-stu-id="ad676-120">Increased stability of the service</span></span>
* <span data-ttu-id="ad676-121">Actualizaciones de la experiencia con el portal del inquilino y actualizaciones del proceso de instalación</span><span class="sxs-lookup"><span data-stu-id="ad676-121">Tenant portal experience updates and installation process updates</span></span>

## <a name="limitations-of-the-technical-preview"></a><span data-ttu-id="ad676-122">Limitaciones de la versión preliminar técnica</span><span class="sxs-lookup"><span data-stu-id="ad676-122">Limitations of the technical preview</span></span>

<span data-ttu-id="ad676-123">No se ofrece soporte técnico para las versiones preliminares de App Service en Azure Stack, aunque se supervisará el foro de MSDN de Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="ad676-123">There is no support for the App Service on Azure Stack preview releases, although we do monitor the Azure Stack MSDN Forum.</span></span> <span data-ttu-id="ad676-124">No se deben poner cargas de trabajo de producción en esta versión preliminar.</span><span class="sxs-lookup"><span data-stu-id="ad676-124">Do not put production workloads on this preview release.</span></span> <span data-ttu-id="ad676-125">Tampoco existen actualizaciones entre versiones preliminares de App Service en Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="ad676-125">There is also no upgrade between App Service on Azure Stack preview releases.</span></span> <span data-ttu-id="ad676-126">Los principales objetivos de estas versiones preliminares son mostrar lo que ofrecemos y obtener comentarios.</span><span class="sxs-lookup"><span data-stu-id="ad676-126">The primary purposes of these preview releases are to show what we're providing and to obtain feedback.</span></span> 

## <a name="what-is-an-app-service-plan"></a><span data-ttu-id="ad676-127">¿Qué es un plan de App Service?</span><span class="sxs-lookup"><span data-stu-id="ad676-127">What is an App Service plan?</span></span>

<span data-ttu-id="ad676-128">El proveedor de recursos de App Service usa el mismo código que Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="ad676-128">The App Service resource provider uses the same code that Azure App Service uses.</span></span> <span data-ttu-id="ad676-129">Como resultado, merece la pena describir algunos conceptos comunes.</span><span class="sxs-lookup"><span data-stu-id="ad676-129">As a result, some common concepts are worth describing.</span></span> <span data-ttu-id="ad676-130">En App Service, el contenedor de precios para las aplicaciones se denomina plan de App Service.</span><span class="sxs-lookup"><span data-stu-id="ad676-130">In App Service, the pricing container for applications is called the App Service plan.</span></span> <span data-ttu-id="ad676-131">Representa el conjunto de máquinas virtuales dedicadas usadas para hospedar las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="ad676-131">It represents the set of dedicated virtual machines used to hold your apps.</span></span> <span data-ttu-id="ad676-132">Dentro de una suscripción determinada, pueden haber varios planes de App Service.</span><span class="sxs-lookup"><span data-stu-id="ad676-132">Within a given subscription, you can have multiple App Service plans.</span></span> 

<span data-ttu-id="ad676-133">En Azure, hay trabajados compartidos y dedicados.</span><span class="sxs-lookup"><span data-stu-id="ad676-133">In Azure, there are shared and dedicated workers.</span></span> <span data-ttu-id="ad676-134">Un trabajo compartido admite el hospedaje de aplicaciones para varios inquilinos de alta densidad, y solo existe un conjunto de trabajos compartidos.</span><span class="sxs-lookup"><span data-stu-id="ad676-134">A shared worker supports high-density multitenant app hosting, and there is only one set of shared workers.</span></span> <span data-ttu-id="ad676-135">Solo un inquilino usa los servidores dedicados que pueden ser de tres tamaños: pequeño, mediano y grande.</span><span class="sxs-lookup"><span data-stu-id="ad676-135">Dedicated servers are used by only one tenant and come in three sizes: small, medium, and large.</span></span> <span data-ttu-id="ad676-136">Las necesidades de los clientes locales no siempre se pueden describir con estos términos.</span><span class="sxs-lookup"><span data-stu-id="ad676-136">The needs of on-premises customers can't always be described by using those terms.</span></span> <span data-ttu-id="ad676-137">En App Service en Azure Stack, los administradores de proveedores de recursos pueden definir los niveles de trabajo que quieren que estén disponibles.</span><span class="sxs-lookup"><span data-stu-id="ad676-137">In App Service on Azure Stack, resource provider administrators can define the worker tiers they want to make available.</span></span> <span data-ttu-id="ad676-138">Los administradores pueden definir varios conjuntos de trabajos compartidos o diferentes conjuntos de trabajos dedicados en función de sus necesidades únicas de hospedaje.</span><span class="sxs-lookup"><span data-stu-id="ad676-138">Administrators can define multiple sets of shared workers or different sets of dedicated workers based on their unique hosting needs.</span></span> <span data-ttu-id="ad676-139">Mediante el uso de esas definiciones de nivel de trabajo, pueden definir sus propias SKU de precios.</span><span class="sxs-lookup"><span data-stu-id="ad676-139">By using those worker-tier definitions, they can then define their own pricing SKUs.</span></span>

## <a name="portal-features"></a><span data-ttu-id="ad676-140">Características del portal</span><span class="sxs-lookup"><span data-stu-id="ad676-140">Portal features</span></span>

<span data-ttu-id="ad676-141">App Service en Azure Stack usa la misma interfaz de usuario que Azure App Service, como ocurre con el back-end.</span><span class="sxs-lookup"><span data-stu-id="ad676-141">App Service on Azure Stack uses the same UI that Azure App Service uses, as is true with the back end.</span></span> <span data-ttu-id="ad676-142">Algunas características están deshabilitadas y no funcionan en Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="ad676-142">Some features are disabled and aren't functional in Azure Stack.</span></span> <span data-ttu-id="ad676-143">Las expectativas o los servicios específicos de Azure que requieren esas características no están disponibles aún en Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="ad676-143">The Azure-specific expectations or services that those features require aren't yet available in Azure Stack.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="ad676-144">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ad676-144">Next steps</span></span>

- [<span data-ttu-id="ad676-145">Antes de empezar a trabajar con App Service en Azure Stack</span><span class="sxs-lookup"><span data-stu-id="ad676-145">Before you get started with App Service on Azure Stack</span></span>](azure-stack-app-service-before-you-get-started.md)
- [<span data-ttu-id="ad676-146">Instale el proveedor de recursos de App Service</span><span class="sxs-lookup"><span data-stu-id="ad676-146">Install the App Service resource provider</span></span>](azure-stack-app-service-deploy.md)

<span data-ttu-id="ad676-147">También puede probar otros [servicios de plataforma como servicio (PaaS)](azure-stack-tools-paas-services.md), como el [proveedor de recursos de SQL Server](azure-stack-sql-resource-provider-deploy.md) y el [proveedor de recursos de MySQL](azure-stack-mysql-resource-provider-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="ad676-147">You can also try out other [platform as a service (PaaS) services](azure-stack-tools-paas-services.md), like the [SQL Server resource provider](azure-stack-sql-resource-provider-deploy.md) and the [MySQL resource provider](azure-stack-mysql-resource-provider-deploy.md).</span></span>

<!--Image references-->
[1]: ./media/azure-stack-app-service-overview/AppService_Portal.png
