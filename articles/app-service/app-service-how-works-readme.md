---
title: aaaHow funciona de servicio de aplicaciones de Azure
description: "Obtener información acerca de cómo funciona el Servicio de aplicaciones"
keywords: servicio de aplicaciones, servicio de aplicaciones de azure, escala, escalable, plan del servicio de aplicaciones, costo del servicio de aplicaciones
services: app-service
documentationcenter: 
author: yochay
manager: erikre
editor: 
ms.assetid: ae74fc32-969e-4580-8d61-02c922f1f184
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 02/23/2017
ms.author: yochayk
ms.openlocfilehash: b20733ec8844773d063e2b6918605c4a48db1f5c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-app-service-works"></a><span data-ttu-id="a3d32-104">Funcionamiento de App Service</span><span class="sxs-lookup"><span data-stu-id="a3d32-104">How App Service works</span></span>
<span data-ttu-id="a3d32-105">Servicio de aplicaciones de Azure es un servicio de nube que es problemas concretos de toosolve diseñado Hola que se enfrentan los ingenieros de hoy en día.</span><span class="sxs-lookup"><span data-stu-id="a3d32-105">Azure App Service is a cloud service that's designed toosolve hello practical problems that engineers face today.</span></span>
<span data-ttu-id="a3d32-106">Servicio de aplicaciones enfoques sobre cómo proporcionar la productividad del desarrollador superior sin comprometer Hola necesitan que las aplicaciones de toodeliver a escala de nube.</span><span class="sxs-lookup"><span data-stu-id="a3d32-106">App Service focuses on providing superior developer productivity without compromising on hello need toodeliver applications at cloud scale.</span></span> 

<span data-ttu-id="a3d32-107">Servicio de aplicaciones también proporciona características de Hola y marcos de trabajo que son necesarios para crear aplicaciones de línea de negocio de empresa.</span><span class="sxs-lookup"><span data-stu-id="a3d32-107">App Service also provides hello features and frameworks that are necessary for creating enterprise line-of-business applications.</span></span> <span data-ttu-id="a3d32-108">Servicio de aplicaciones le permite desarrollar aplicaciones en lenguajes de desarrollo más populares, incluidos Java, PHP, Node.js, Python y lenguajes de .NET de Microsoft de Hola.</span><span class="sxs-lookup"><span data-stu-id="a3d32-108">App Service lets you develop apps in most popular development languages, including Java, PHP, Node.js, Python, and hello Microsoft .NET languages.</span></span> <span data-ttu-id="a3d32-109">Con el Servicio de aplicaciones, puede:</span><span class="sxs-lookup"><span data-stu-id="a3d32-109">With App Service, you can:</span></span>

* <span data-ttu-id="a3d32-110">Crear aplicaciones web altamente escalables.</span><span class="sxs-lookup"><span data-stu-id="a3d32-110">Build highly scalable web apps.</span></span>
* <span data-ttu-id="a3d32-111">Crear rápidamente back-ends de Mobile Apps con un conjunto de funcionalidades móviles fáciles de usar, como back-ends de datos, autenticación de usuario y notificaciones push.</span><span class="sxs-lookup"><span data-stu-id="a3d32-111">Quickly build Mobile Apps back ends with a set of easy-to-use mobile capabilities such as data back ends, user authentication, and push notifications.</span></span>
* <span data-ttu-id="a3d32-112">Implementar y publicar las API con API Apps.</span><span class="sxs-lookup"><span data-stu-id="a3d32-112">Implement, deploy, and publish APIs with API Apps.</span></span>
* <span data-ttu-id="a3d32-113">Vincular las aplicaciones empresariales en flujos de trabajo y transformar datos con Aplicaciones lógicas.</span><span class="sxs-lookup"><span data-stu-id="a3d32-113">Tie business applications together into workflows and transform data with Logic Apps.</span></span>

> [!INCLUDE [app-service-linux](../../includes/app-service-linux.md)]
> 
> 

<span data-ttu-id="a3d32-114">Todos los tipos de aplicación se basan en hello plataforma escalable y flexible aplicaciones Web, que permite toohave a los desarrolladores un ciclo de vida completo optimizado que aportan mantenimiento de tooapp de diseño de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="a3d32-114">All app types rely on hello scalable and flexible Web Apps platform, which enables developers toohave an optimized full lifecycle experience from app design tooapp maintenance.</span></span> <span data-ttu-id="a3d32-115">capacidades de ciclo de vida de Hello habilitar siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="a3d32-115">hello lifecycle capabilities enable hello following:</span></span>

* <span data-ttu-id="a3d32-116">**Creación rápida de la aplicación**.</span><span class="sxs-lookup"><span data-stu-id="a3d32-116">**Quick app creation**.</span></span> <span data-ttu-id="a3d32-117">Empezar desde cero o seleccionar un paquete de sistema operativo de soporte técnico (OSS) desde hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="a3d32-117">Start from scratch or pick an operational support system (OSS) package from hello Azure Marketplace.</span></span>
* <span data-ttu-id="a3d32-118">**Implementación continua**.</span><span class="sxs-lookup"><span data-stu-id="a3d32-118">**Continuous deployment**.</span></span> <span data-ttu-id="a3d32-119">Implemente automáticamente el código nuevo a partir de soluciones de control de código fuente populares, como TFS, GitHub y BitBucket, y sincronice el contenido desde servicios de almacenamiento en línea, como OneDrive y DropBox.</span><span class="sxs-lookup"><span data-stu-id="a3d32-119">Automatically deploy new code from popular source control solutions such as TFS, GitHub, and Bitbucket, and sync content from online storage services such as OneDrive and Dropbox.</span></span>
* <span data-ttu-id="a3d32-120">**Pruebas de producción**.</span><span class="sxs-lookup"><span data-stu-id="a3d32-120">**Test in production**.</span></span> <span data-ttu-id="a3d32-121">Crear entornos de preproducción y administre Hola cantidad de tráfico que circula toothem con facilidad.</span><span class="sxs-lookup"><span data-stu-id="a3d32-121">Smoothly create pre-production environments and manage hello amount of traffic that's going toothem.</span></span> <span data-ttu-id="a3d32-122">Depurar en la nube de hello cuando sea necesario y poner de nuevo cuando se encuentren problemas.</span><span class="sxs-lookup"><span data-stu-id="a3d32-122">Debug in hello cloud when needed, and roll back when issues are found.</span></span>
* <span data-ttu-id="a3d32-123">**Ejecución de tareas asincrónicas y trabajos por lotes**.</span><span class="sxs-lookup"><span data-stu-id="a3d32-123">**Running asynchronous tasks and batch jobs**.</span></span> <span data-ttu-id="a3d32-124">Ejecute el código mediante un proceso en segundo plano o active el código en función de eventos (como los mensajes que llegan a una cola de Azure Storage) y de horas programadas (CRON).</span><span class="sxs-lookup"><span data-stu-id="a3d32-124">Run code in a background process or activate your code based on events (such as messages landing in an Azure Storage queue) and scheduled times (CRON).</span></span>
* <span data-ttu-id="a3d32-125">**Escala aplicación hello**.</span><span class="sxs-lookup"><span data-stu-id="a3d32-125">**Scaling hello app**.</span></span> <span data-ttu-id="a3d32-126">Use uno de muchos tooautomatically opciones escalar el servicio horizontalmente y verticalmente en función de tráfico y uso de recursos.</span><span class="sxs-lookup"><span data-stu-id="a3d32-126">Use one of many options tooautomatically scale your service horizontally and vertically based on traffic and resource utilization.</span></span> <span data-ttu-id="a3d32-127">Configurar entornos privados que son aplicaciones tooyour dedicado.</span><span class="sxs-lookup"><span data-stu-id="a3d32-127">Configure private environments that are dedicated tooyour apps.</span></span>   
* <span data-ttu-id="a3d32-128">**Mantener aplicación hello**.</span><span class="sxs-lookup"><span data-stu-id="a3d32-128">**Maintaining hello app**.</span></span> <span data-ttu-id="a3d32-129">Usar muchos de depuración de Hola y toostay de características de diagnóstico por delante de los problemas y tooefficiently resolver en tiempo real (con características como la depuración en directo y recuperación automática) o después de hechos de hello mediante el análisis de registros y la memoria volcados de memoria.</span><span class="sxs-lookup"><span data-stu-id="a3d32-129">Use many of hello debugging and diagnostics features toostay ahead of problems and tooefficiently resolve them either in real time (with features such as auto-healing and live debugging) or after hello fact by analyzing logs and memory dumps.</span></span>

<span data-ttu-id="a3d32-130">En su conjunto, capacidades de servicio de aplicaciones permiten a los desarrolladores toofocus en su código y alcanzan rápidamente el estado de producción estable y altamente escalable.</span><span class="sxs-lookup"><span data-stu-id="a3d32-130">As a whole, App Service capabilities enable developers toofocus on their code and quickly reach a stable and highly scalable production state.</span></span> <span data-ttu-id="a3d32-131">Con aplicaciones de API de Hola y las características de las aplicaciones lógicas, los desarrolladores pueden crear aplicaciones empresariales reales que vinculan las barreras que existen entre las soluciones empresariales y la integración de toocloud local.</span><span class="sxs-lookup"><span data-stu-id="a3d32-131">With hello API Apps and Logic Apps features, developers can build real-world enterprise applications that bridge barriers between business solutions and on-premises toocloud integration.</span></span> 

## <a name="videos"></a><span data-ttu-id="a3d32-132">Vídeos</span><span class="sxs-lookup"><span data-stu-id="a3d32-132">Videos</span></span>
* [<span data-ttu-id="a3d32-133">Arquitectura del Servicio de aplicaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="a3d32-133">Azure App Service Architecture</span></span>](https://azure.microsoft.com/documentation/videos/why-azure-web-sites-plus-architecture/)

## <a name="next-steps"></a><span data-ttu-id="a3d32-134">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a3d32-134">Next steps</span></span>

<span data-ttu-id="a3d32-135">Más información sobre el servicio de aplicaciones en uno de los temas siguientes de hello:</span><span class="sxs-lookup"><span data-stu-id="a3d32-135">Learn more about App Service in one of hello following topics:</span></span>

* [<span data-ttu-id="a3d32-136">¿Qué es Servicios de aplicaciones de Azure?</span><span class="sxs-lookup"><span data-stu-id="a3d32-136">What is Azure App Service?</span></span>](app-service-value-prop-what-is.md)
  * [<span data-ttu-id="a3d32-137">Aplicación web</span><span class="sxs-lookup"><span data-stu-id="a3d32-137">Web App</span></span>](../app-service-web/app-service-web-overview.md)
  * [<span data-ttu-id="a3d32-138">Aplicación móvil</span><span class="sxs-lookup"><span data-stu-id="a3d32-138">Mobile App</span></span>](../app-service-mobile/app-service-mobile-value-prop.md)
  * [<span data-ttu-id="a3d32-139">Aplicación de API</span><span class="sxs-lookup"><span data-stu-id="a3d32-139">API App</span></span>](../app-service-api/app-service-api-apps-why-best-platform.md)
* [<span data-ttu-id="a3d32-140">Arquitectura del Servicio de aplicaciones de Azure (presentación)</span><span class="sxs-lookup"><span data-stu-id="a3d32-140">Azure App Service Architecture (presentation)</span></span>](http://www.slideshare.net/maartenba/windows-azure-web-sites-things-they-dont-teach-kids-in-school-comunity-day-2013)
* [<span data-ttu-id="a3d32-141">Comparación entre el Servicio de aplicaciones de Azure, Servicios en la nube y Máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="a3d32-141">Azure App Service, Cloud Services, and Virtual Machines comparison</span></span>](../app-service-web/choose-web-site-cloud-service-vm.md)
* [<span data-ttu-id="a3d32-142">Descripción de los planes del Servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="a3d32-142">Understanding App Service Plans</span></span>](azure-web-sites-web-hosting-plans-in-depth-overview.md)
* [<span data-ttu-id="a3d32-143">Introducción tooApp entorno del servicio</span><span class="sxs-lookup"><span data-stu-id="a3d32-143">Introduction tooApp Service Environment</span></span>](../app-service-web/app-service-app-service-environment-intro.md)
  * [<span data-ttu-id="a3d32-144">Ejercicio: Creación de un entorno del Servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="a3d32-144">Exercise: Create an App Service Environment</span></span>](../app-service-web/app-service-web-how-to-create-an-app-service-environment.md)
* [<span data-ttu-id="a3d32-145">Soporte de pilas de desarrollo del Servicio de aplicaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="a3d32-145">Azure App Service Development Stacks Support</span></span>](https://azure.microsoft.com/blog/windows-azure-websites-development-stacks-support/)



