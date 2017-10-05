---
title: Funcionamiento de Azure App Service
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
ms.openlocfilehash: 2d830963d3d2adba71a6ca99f79eac0fc8cbfb12
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-app-service-works"></a><span data-ttu-id="86025-104">Funcionamiento de App Service</span><span class="sxs-lookup"><span data-stu-id="86025-104">How App Service works</span></span>
<span data-ttu-id="86025-105">Azure App Service es un servicio en la nube diseñado para resolver los problemas prácticos a los que se enfrentan hoy en día los ingenieros.</span><span class="sxs-lookup"><span data-stu-id="86025-105">Azure App Service is a cloud service that's designed to solve the practical problems that engineers face today.</span></span>
<span data-ttu-id="86025-106">El objetivo de App Service es ofrecer a los desarrolladores una productividad superior sin que esto perjudique a la necesidad de entregar aplicaciones a escala de nube.</span><span class="sxs-lookup"><span data-stu-id="86025-106">App Service focuses on providing superior developer productivity without compromising on the need to deliver applications at cloud scale.</span></span> 

<span data-ttu-id="86025-107">App Service también proporciona las características y los marcos de trabajo que son necesarios para crear aplicaciones de línea de negocio de empresa.</span><span class="sxs-lookup"><span data-stu-id="86025-107">App Service also provides the features and frameworks that are necessary for creating enterprise line-of-business applications.</span></span> <span data-ttu-id="86025-108">App Service le permite desarrollar aplicaciones en la mayoría de lenguajes de desarrollo conocidos, como Java, PHP, Node.js, Python y los lenguajes de Microsoft .NET.</span><span class="sxs-lookup"><span data-stu-id="86025-108">App Service lets you develop apps in most popular development languages, including Java, PHP, Node.js, Python, and the Microsoft .NET languages.</span></span> <span data-ttu-id="86025-109">Con el Servicio de aplicaciones, puede:</span><span class="sxs-lookup"><span data-stu-id="86025-109">With App Service, you can:</span></span>

* <span data-ttu-id="86025-110">Crear aplicaciones web altamente escalables.</span><span class="sxs-lookup"><span data-stu-id="86025-110">Build highly scalable web apps.</span></span>
* <span data-ttu-id="86025-111">Crear rápidamente back-ends de Mobile Apps con un conjunto de funcionalidades móviles fáciles de usar, como back-ends de datos, autenticación de usuario y notificaciones push.</span><span class="sxs-lookup"><span data-stu-id="86025-111">Quickly build Mobile Apps back ends with a set of easy-to-use mobile capabilities such as data back ends, user authentication, and push notifications.</span></span>
* <span data-ttu-id="86025-112">Implementar y publicar las API con API Apps.</span><span class="sxs-lookup"><span data-stu-id="86025-112">Implement, deploy, and publish APIs with API Apps.</span></span>
* <span data-ttu-id="86025-113">Vincular las aplicaciones empresariales en flujos de trabajo y transformar datos con Aplicaciones lógicas.</span><span class="sxs-lookup"><span data-stu-id="86025-113">Tie business applications together into workflows and transform data with Logic Apps.</span></span>

> [!INCLUDE [app-service-linux](../../includes/app-service-linux.md)]
> 
> 

<span data-ttu-id="86025-114">Todos los tipos de aplicaciones se basan en la plataforma escalable y flexible de Web Apps, que ofrece a los desarrolladores una experiencia optimizada durante todo el ciclo de vida, desde el diseño de la aplicación hasta su mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="86025-114">All app types rely on the scalable and flexible Web Apps platform, which enables developers to have an optimized full lifecycle experience from app design to app maintenance.</span></span> <span data-ttu-id="86025-115">Las funcionalidades del ciclo de vida permiten lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="86025-115">The lifecycle capabilities enable the following:</span></span>

* <span data-ttu-id="86025-116">**Creación rápida de la aplicación**.</span><span class="sxs-lookup"><span data-stu-id="86025-116">**Quick app creation**.</span></span> <span data-ttu-id="86025-117">Comience desde cero o elija un paquete del sistema de ayuda para operaciones (OSS) de Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="86025-117">Start from scratch or pick an operational support system (OSS) package from the Azure Marketplace.</span></span>
* <span data-ttu-id="86025-118">**Implementación continua**.</span><span class="sxs-lookup"><span data-stu-id="86025-118">**Continuous deployment**.</span></span> <span data-ttu-id="86025-119">Implemente automáticamente el código nuevo a partir de soluciones de control de código fuente populares, como TFS, GitHub y BitBucket, y sincronice el contenido desde servicios de almacenamiento en línea, como OneDrive y DropBox.</span><span class="sxs-lookup"><span data-stu-id="86025-119">Automatically deploy new code from popular source control solutions such as TFS, GitHub, and Bitbucket, and sync content from online storage services such as OneDrive and Dropbox.</span></span>
* <span data-ttu-id="86025-120">**Pruebas de producción**.</span><span class="sxs-lookup"><span data-stu-id="86025-120">**Test in production**.</span></span> <span data-ttu-id="86025-121">Cree fácilmente entornos de preproducción y administre la parte del tráfico que se dirige hacia ellos.</span><span class="sxs-lookup"><span data-stu-id="86025-121">Smoothly create pre-production environments and manage the amount of traffic that's going to them.</span></span> <span data-ttu-id="86025-122">Realice la depuración en la nube cuando sea necesario y revierta los cambios si se produce algún problema.</span><span class="sxs-lookup"><span data-stu-id="86025-122">Debug in the cloud when needed, and roll back when issues are found.</span></span>
* <span data-ttu-id="86025-123">**Ejecución de tareas asincrónicas y trabajos por lotes**.</span><span class="sxs-lookup"><span data-stu-id="86025-123">**Running asynchronous tasks and batch jobs**.</span></span> <span data-ttu-id="86025-124">Ejecute el código mediante un proceso en segundo plano o active el código en función de eventos (como los mensajes que llegan a una cola de Azure Storage) y de horas programadas (CRON).</span><span class="sxs-lookup"><span data-stu-id="86025-124">Run code in a background process or activate your code based on events (such as messages landing in an Azure Storage queue) and scheduled times (CRON).</span></span>
* <span data-ttu-id="86025-125">**Escalado de la aplicación**.</span><span class="sxs-lookup"><span data-stu-id="86025-125">**Scaling the app**.</span></span> <span data-ttu-id="86025-126">Utilice una de las numerosas opciones para escalar su servicio horizontal y verticalmente de forma automática en función del tráfico y el uso de los recursos.</span><span class="sxs-lookup"><span data-stu-id="86025-126">Use one of many options to automatically scale your service horizontally and vertically based on traffic and resource utilization.</span></span> <span data-ttu-id="86025-127">Configure entornos privados que estén dedicados a las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="86025-127">Configure private environments that are dedicated to your apps.</span></span>   
* <span data-ttu-id="86025-128">**Mantenimiento de la aplicación**.</span><span class="sxs-lookup"><span data-stu-id="86025-128">**Maintaining the app**.</span></span> <span data-ttu-id="86025-129">Aproveche las numerosas características de depuración y diagnóstico para anticiparse a los problemas y resolverlos eficazmente en tiempo real (con características como la recuperación automática y la depuración en directo) o después de analizar los registros y los volcados de memoria.</span><span class="sxs-lookup"><span data-stu-id="86025-129">Use many of the debugging and diagnostics features to stay ahead of problems and to efficiently resolve them either in real time (with features such as auto-healing and live debugging) or after the fact by analyzing logs and memory dumps.</span></span>

<span data-ttu-id="86025-130">Juntas, las funcionalidades de App Service permiten a los desarrolladores centrarse en el código y llegar rápidamente a un estado de producción estable y muy escalable.</span><span class="sxs-lookup"><span data-stu-id="86025-130">As a whole, App Service capabilities enable developers to focus on their code and quickly reach a stable and highly scalable production state.</span></span> <span data-ttu-id="86025-131">Con las características de API Apps y Logic Apps, los desarrolladores pueden crear aplicaciones empresariales del mundo real que cierren las brechas entre las soluciones empresariales y contribuyan a la integración de las implementaciones locales en la nube.</span><span class="sxs-lookup"><span data-stu-id="86025-131">With the API Apps and Logic Apps features, developers can build real-world enterprise applications that bridge barriers between business solutions and on-premises to cloud integration.</span></span> 

## <a name="videos"></a><span data-ttu-id="86025-132">Vídeos</span><span class="sxs-lookup"><span data-stu-id="86025-132">Videos</span></span>
* [<span data-ttu-id="86025-133">Arquitectura del Servicio de aplicaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="86025-133">Azure App Service Architecture</span></span>](https://azure.microsoft.com/documentation/videos/why-azure-web-sites-plus-architecture/)

## <a name="next-steps"></a><span data-ttu-id="86025-134">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="86025-134">Next steps</span></span>

<span data-ttu-id="86025-135">Más información sobre App Service en uno de los siguientes temas:</span><span class="sxs-lookup"><span data-stu-id="86025-135">Learn more about App Service in one of the following topics:</span></span>

* [<span data-ttu-id="86025-136">¿Qué es Servicios de aplicaciones de Azure?</span><span class="sxs-lookup"><span data-stu-id="86025-136">What is Azure App Service?</span></span>](app-service-value-prop-what-is.md)
  * [<span data-ttu-id="86025-137">Aplicación web</span><span class="sxs-lookup"><span data-stu-id="86025-137">Web App</span></span>](../app-service-web/app-service-web-overview.md)
  * [<span data-ttu-id="86025-138">Aplicación móvil</span><span class="sxs-lookup"><span data-stu-id="86025-138">Mobile App</span></span>](../app-service-mobile/app-service-mobile-value-prop.md)
  * [<span data-ttu-id="86025-139">Aplicación de API</span><span class="sxs-lookup"><span data-stu-id="86025-139">API App</span></span>](../app-service-api/app-service-api-apps-why-best-platform.md)
* [<span data-ttu-id="86025-140">Arquitectura del Servicio de aplicaciones de Azure (presentación)</span><span class="sxs-lookup"><span data-stu-id="86025-140">Azure App Service Architecture (presentation)</span></span>](http://www.slideshare.net/maartenba/windows-azure-web-sites-things-they-dont-teach-kids-in-school-comunity-day-2013)
* [<span data-ttu-id="86025-141">Comparación entre el Servicio de aplicaciones de Azure, Servicios en la nube y Máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="86025-141">Azure App Service, Cloud Services, and Virtual Machines comparison</span></span>](../app-service-web/choose-web-site-cloud-service-vm.md)
* [<span data-ttu-id="86025-142">Descripción de los planes del Servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="86025-142">Understanding App Service Plans</span></span>](azure-web-sites-web-hosting-plans-in-depth-overview.md)
* [<span data-ttu-id="86025-143">Introducción al entorno del Servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="86025-143">Introduction to App Service Environment</span></span>](../app-service-web/app-service-app-service-environment-intro.md)
  * [<span data-ttu-id="86025-144">Ejercicio: Creación de un entorno del Servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="86025-144">Exercise: Create an App Service Environment</span></span>](../app-service-web/app-service-web-how-to-create-an-app-service-environment.md)
* [<span data-ttu-id="86025-145">Soporte de pilas de desarrollo del Servicio de aplicaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="86025-145">Azure App Service Development Stacks Support</span></span>](https://azure.microsoft.com/blog/windows-azure-websites-development-stacks-support/)



