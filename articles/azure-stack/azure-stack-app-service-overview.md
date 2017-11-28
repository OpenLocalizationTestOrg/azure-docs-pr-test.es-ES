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
ms.openlocfilehash: 1d763f592212b3a2dcc2f03ebe317eed84e9e2de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="app-service-on-azure-stack-overview"></a><span data-ttu-id="c629c-103">Introducción a App Service en Azure Stack</span><span class="sxs-lookup"><span data-stu-id="c629c-103">App Service on Azure Stack overview</span></span>

<span data-ttu-id="c629c-104">Servicio de aplicaciones de Azure en la pila de Azure es hello Azure oferta poner tooAzure pila.</span><span class="sxs-lookup"><span data-stu-id="c629c-104">Azure App Service on Azure Stack is hello Azure offering brought tooAzure Stack.</span></span> <span data-ttu-id="c629c-105">Hola servicio de aplicaciones en el instalador de la pila de Azure crea Hola siguiendo el conjunto de instancias de rol:</span><span class="sxs-lookup"><span data-stu-id="c629c-105">hello App Service on Azure Stack installer creates hello following set of role instances:</span></span>

*  <span data-ttu-id="c629c-106">Controller</span><span class="sxs-lookup"><span data-stu-id="c629c-106">Controller</span></span>
*  <span data-ttu-id="c629c-107">Administración (se crean dos instancias)</span><span class="sxs-lookup"><span data-stu-id="c629c-107">Management (two instances are created)</span></span>
*  <span data-ttu-id="c629c-108">FrontEnd</span><span class="sxs-lookup"><span data-stu-id="c629c-108">FrontEnd</span></span>
*  <span data-ttu-id="c629c-109">Publicador</span><span class="sxs-lookup"><span data-stu-id="c629c-109">Publisher</span></span>
*  <span data-ttu-id="c629c-110">Trabajo (en modo compartido)</span><span class="sxs-lookup"><span data-stu-id="c629c-110">Worker (in Shared mode)</span></span>

<span data-ttu-id="c629c-111">Además, Hola servicio de aplicaciones en el instalador de la pila de Azure crea un servidor de archivos.</span><span class="sxs-lookup"><span data-stu-id="c629c-111">In addition, hello App Service on Azure Stack installer creates a file server.</span></span>
    
## <a name="whats-new-in-hello-first-release-candidate-of-app-service-on-azure-stack"></a><span data-ttu-id="c629c-112">¿Novedades de hello primera versión release candidate de servicio de aplicaciones en la pila de Azure?</span><span class="sxs-lookup"><span data-stu-id="c629c-112">What's new in hello first release candidate of App Service on Azure Stack?</span></span>
![Servicio de aplicaciones de portal de Azure pila Hola][1]

<span data-ttu-id="c629c-114">Hola primera versión release candidate de servicio de aplicaciones en la pila de Azure se basa en la vista previa terceros de Hola y aporta mejoras y nuevas funcionalidades:</span><span class="sxs-lookup"><span data-stu-id="c629c-114">hello first release candidate of App Service on Azure Stack builds on top of hello third preview and brings new capabilities and improvements:</span></span>

* <span data-ttu-id="c629c-115">Azure Functions en entornos de Azure Stack basado en los Servicios de federación de Active Directory (AD FS)</span><span class="sxs-lookup"><span data-stu-id="c629c-115">Azure Functions in Azure Stack environments based on Active Directory Federation Services</span></span> 
* <span data-ttu-id="c629c-116">Inicio de sesión único, soporte para el portal de funciones de Hola y Hola herramientas de desarrollo avanzadas (Kudu)</span><span class="sxs-lookup"><span data-stu-id="c629c-116">Single sign-on support for hello Functions portal and hello advanced developer tools (Kudu)</span></span>
* <span data-ttu-id="c629c-117">Compatibilidad con Java para aplicaciones web, móviles y de API</span><span class="sxs-lookup"><span data-stu-id="c629c-117">Java support for web, mobile, and API applications</span></span>
* <span data-ttu-id="c629c-118">Administración de niveles de trabajo por la escala de máquinas virtuales establece tooimprove capacidades de escalabilidad horizontal para los administradores de servicios</span><span class="sxs-lookup"><span data-stu-id="c629c-118">Management of worker tiers by virtual machine scale sets tooimprove scale-out capabilities for service administrators</span></span>
* <span data-ttu-id="c629c-119">Localización de la experiencia de administración de Hola</span><span class="sxs-lookup"><span data-stu-id="c629c-119">Localization of hello admin experience</span></span>
* <span data-ttu-id="c629c-120">Mayor estabilidad del servicio de Hola</span><span class="sxs-lookup"><span data-stu-id="c629c-120">Increased stability of hello service</span></span>
* <span data-ttu-id="c629c-121">Actualizaciones de la experiencia con el portal del inquilino y actualizaciones del proceso de instalación</span><span class="sxs-lookup"><span data-stu-id="c629c-121">Tenant portal experience updates and installation process updates</span></span>

## <a name="limitations-of-hello-technical-preview"></a><span data-ttu-id="c629c-122">Limitaciones de vista previa técnica de Hola</span><span class="sxs-lookup"><span data-stu-id="c629c-122">Limitations of hello technical preview</span></span>

<span data-ttu-id="c629c-123">No hay ninguna compatibilidad para Hola servicio de aplicaciones en versiones preliminares de pila de Azure, aunque se supervisará Hola foro de MSDN de pila de Azure.</span><span class="sxs-lookup"><span data-stu-id="c629c-123">There is no support for hello App Service on Azure Stack preview releases, although we do monitor hello Azure Stack MSDN Forum.</span></span> <span data-ttu-id="c629c-124">No se deben poner cargas de trabajo de producción en esta versión preliminar.</span><span class="sxs-lookup"><span data-stu-id="c629c-124">Do not put production workloads on this preview release.</span></span> <span data-ttu-id="c629c-125">Tampoco existen actualizaciones entre versiones preliminares de App Service en Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="c629c-125">There is also no upgrade between App Service on Azure Stack preview releases.</span></span> <span data-ttu-id="c629c-126">Hello fines principales de estas versiones de vista previa son tooshow que ofrecemos también y tooobtain comentarios.</span><span class="sxs-lookup"><span data-stu-id="c629c-126">hello primary purposes of these preview releases are tooshow what we're providing and tooobtain feedback.</span></span> 

## <a name="what-is-an-app-service-plan"></a><span data-ttu-id="c629c-127">¿Qué es un plan de App Service?</span><span class="sxs-lookup"><span data-stu-id="c629c-127">What is an App Service plan?</span></span>

<span data-ttu-id="c629c-128">Hola proveedor de recursos de servicio de aplicaciones usa Hola el mismo código que usa el servicio de aplicaciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="c629c-128">hello App Service resource provider uses hello same code that Azure App Service uses.</span></span> <span data-ttu-id="c629c-129">Como resultado, merece la pena describir algunos conceptos comunes.</span><span class="sxs-lookup"><span data-stu-id="c629c-129">As a result, some common concepts are worth describing.</span></span> <span data-ttu-id="c629c-130">En el servicio de aplicaciones, Hola precios contenedor para las aplicaciones se denomina hello plan de servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="c629c-130">In App Service, hello pricing container for applications is called hello App Service plan.</span></span> <span data-ttu-id="c629c-131">Representa conjunto de Hola de máquinas virtuales dedicadas usa toohold sus aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="c629c-131">It represents hello set of dedicated virtual machines used toohold your apps.</span></span> <span data-ttu-id="c629c-132">Dentro de una suscripción determinada, pueden haber varios planes de App Service.</span><span class="sxs-lookup"><span data-stu-id="c629c-132">Within a given subscription, you can have multiple App Service plans.</span></span> 

<span data-ttu-id="c629c-133">En Azure, hay trabajados compartidos y dedicados.</span><span class="sxs-lookup"><span data-stu-id="c629c-133">In Azure, there are shared and dedicated workers.</span></span> <span data-ttu-id="c629c-134">Un trabajo compartido admite el hospedaje de aplicaciones para varios inquilinos de alta densidad, y solo existe un conjunto de trabajos compartidos.</span><span class="sxs-lookup"><span data-stu-id="c629c-134">A shared worker supports high-density multitenant app hosting, and there is only one set of shared workers.</span></span> <span data-ttu-id="c629c-135">Solo un inquilino usa los servidores dedicados que pueden ser de tres tamaños: pequeño, mediano y grande.</span><span class="sxs-lookup"><span data-stu-id="c629c-135">Dedicated servers are used by only one tenant and come in three sizes: small, medium, and large.</span></span> <span data-ttu-id="c629c-136">necesidades de Hola de clientes local no se puede describir siempre mediante el uso de estos términos.</span><span class="sxs-lookup"><span data-stu-id="c629c-136">hello needs of on-premises customers can't always be described by using those terms.</span></span> <span data-ttu-id="c629c-137">En el servicio de aplicaciones en la pila de Azure, los administradores de proveedor de recursos pueden definir los niveles de trabajo Hola desean toomake disponible.</span><span class="sxs-lookup"><span data-stu-id="c629c-137">In App Service on Azure Stack, resource provider administrators can define hello worker tiers they want toomake available.</span></span> <span data-ttu-id="c629c-138">Los administradores pueden definir varios conjuntos de trabajos compartidos o diferentes conjuntos de trabajos dedicados en función de sus necesidades únicas de hospedaje.</span><span class="sxs-lookup"><span data-stu-id="c629c-138">Administrators can define multiple sets of shared workers or different sets of dedicated workers based on their unique hosting needs.</span></span> <span data-ttu-id="c629c-139">Mediante el uso de esas definiciones de nivel de trabajo, pueden definir sus propias SKU de precios.</span><span class="sxs-lookup"><span data-stu-id="c629c-139">By using those worker-tier definitions, they can then define their own pricing SKUs.</span></span>

## <a name="portal-features"></a><span data-ttu-id="c629c-140">Características del portal</span><span class="sxs-lookup"><span data-stu-id="c629c-140">Portal features</span></span>

<span data-ttu-id="c629c-141">Servicio de aplicaciones en la pila de Azure usa Hola terminar la misma interfaz de usuario que utiliza el servicio de aplicación de Azure, como ocurre con hello hacer una copia.</span><span class="sxs-lookup"><span data-stu-id="c629c-141">App Service on Azure Stack uses hello same UI that Azure App Service uses, as is true with hello back end.</span></span> <span data-ttu-id="c629c-142">Algunas características están deshabilitadas y no funcionan en Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="c629c-142">Some features are disabled and aren't functional in Azure Stack.</span></span> <span data-ttu-id="c629c-143">Hola expectativas específicas de Azure o servicios que requieren estas características aún no están disponibles en la pila de Azure.</span><span class="sxs-lookup"><span data-stu-id="c629c-143">hello Azure-specific expectations or services that those features require aren't yet available in Azure Stack.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="c629c-144">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c629c-144">Next steps</span></span>

- [<span data-ttu-id="c629c-145">Antes de empezar a trabajar con App Service en Azure Stack</span><span class="sxs-lookup"><span data-stu-id="c629c-145">Before you get started with App Service on Azure Stack</span></span>](azure-stack-app-service-before-you-get-started.md)
- [<span data-ttu-id="c629c-146">Instalar Hola proveedor de recursos de servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="c629c-146">Install hello App Service resource provider</span></span>](azure-stack-app-service-deploy.md)

<span data-ttu-id="c629c-147">También puede probar otros [plataforma como servicio (PaaS)](azure-stack-tools-paas-services.md), como hello [proveedor de recursos de SQL Server](azure-stack-sql-resource-provider-deploy.md) hello y [proveedor de recursos MySQL](azure-stack-mysql-resource-provider-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="c629c-147">You can also try out other [platform as a service (PaaS) services](azure-stack-tools-paas-services.md), like hello [SQL Server resource provider](azure-stack-sql-resource-provider-deploy.md) and hello [MySQL resource provider](azure-stack-mysql-resource-provider-deploy.md).</span></span>

<!--Image references-->
[1]: ./media/azure-stack-app-service-overview/AppService_Portal.png
