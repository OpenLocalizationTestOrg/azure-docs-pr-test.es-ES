---
title: Servicio de aplicaciones de Azure y su impacto en los servicios de Azure existentes
description: "Se explica cómo el nuevo Servicio de aplicaciones de Azure y sus características afectan a los servicios ya existentes de Azure."
services: app-service
documentationcenter: 
author: yochay
manager: nirma
editor: 
ms.assetid: 86c6a292-3c33-49f4-890c-89cc0321b397
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/12/2016
ms.author: yochaykk
ms.openlocfilehash: ed967fda7a216ed49532be54228ebe888cf16b6f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="azure-app-service-and-existing-azure-services"></a><span data-ttu-id="2f186-103">Servicio de aplicaciones de Azure y los servicios de Azure existentes</span><span class="sxs-lookup"><span data-stu-id="2f186-103">Azure App Service and existing Azure services</span></span>
<span data-ttu-id="2f186-104">En este artículo se describen las modificaciones de los servicios de Azure ya existentes como parte del cambio para reunir varios servicios de Azure en el [Servicio de aplicaciones de Azure](https://azure.microsoft.com/services/app-service/), una nueva oferta integrada.</span><span class="sxs-lookup"><span data-stu-id="2f186-104">This article outlines the changes to existing Azure services as part of the change to bring together several Azure services into [Azure App Service](https://azure.microsoft.com/services/app-service/), a new integrated offering.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="overview"></a><span data-ttu-id="2f186-105">Información general</span><span class="sxs-lookup"><span data-stu-id="2f186-105">Overview</span></span>
<span data-ttu-id="2f186-106">[Servicio de aplicaciones de Azure](https://azure.microsoft.com/services/app-service/) es un servicio en la nube nuevo y exclusivo que permite a los desarrolladores crear aplicaciones web y móviles destinadas a cualquier plataforma y dispositivo.</span><span class="sxs-lookup"><span data-stu-id="2f186-106">[Azure App Service](https://azure.microsoft.com/services/app-service/) is a new and unique cloud service that enables developers to create web and mobile apps for any platform and any device.</span></span> <span data-ttu-id="2f186-107">Se trata de una solución integral diseñada para simplificar las funciones de codificación repetitivas, integrarse en sistemas Saas y empresariales y automatizar los procesos de negocio a la vez que cumplir sus necesidades de seguridad, confiabilidad y escalabilidad.</span><span class="sxs-lookup"><span data-stu-id="2f186-107">App Service is an integrated solution designed to streamline repeated coding functions, integrate with enterprise and SaaS systems, and automate business processes while meeting your needs for security, reliability, and scalability.</span></span>

<span data-ttu-id="2f186-108">App Service reúne los siguientes servicios de Azure existentes ([Websites](https://azure.microsoft.com/services/websites/), [Mobile Services](https://azure.microsoft.com/services/mobile-services/) y [BizTalk Services](https://azure.microsoft.com/services/biztalk-services/)) en un único servicio único combinado que, a su vez, agrega nuevas funcionalidades eficaces.</span><span class="sxs-lookup"><span data-stu-id="2f186-108">App Service brings together the following existing Azure services - [Websites](https://azure.microsoft.com/services/websites/), [Mobile Services](https://azure.microsoft.com/services/mobile-services/), and [Biztalk Services](https://azure.microsoft.com/services/biztalk-services/) into a single combined service, while adding powerful new capabilities.</span></span>  <span data-ttu-id="2f186-109">Además, permite hospedar los siguientes tipos de aplicaciones:</span><span class="sxs-lookup"><span data-stu-id="2f186-109">App Service allows you to host the following app types:</span></span>

* <span data-ttu-id="2f186-110">Aplicaciones web</span><span class="sxs-lookup"><span data-stu-id="2f186-110">Web Apps</span></span>
* <span data-ttu-id="2f186-111">Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="2f186-111">Mobile Apps</span></span>
* <span data-ttu-id="2f186-112">API Apps</span><span class="sxs-lookup"><span data-stu-id="2f186-112">API Apps</span></span>
* <span data-ttu-id="2f186-113">Aplicaciones lógicas</span><span class="sxs-lookup"><span data-stu-id="2f186-113">Logic Apps</span></span>

<span data-ttu-id="2f186-114">En la tabla siguiente se explica cómo se asignan los servicios de Azure existentes al Servicio de aplicaciones y los tipos de aplicaciones disponibles en este.</span><span class="sxs-lookup"><span data-stu-id="2f186-114">The following table explains how existing Azure services map to App Service and the app types available within it.</span></span>

<table>
<thead>
<tr class="header">
<th align="left", style="width:10%"><span data-ttu-id="2f186-115">Servicio de Azure existente</span><span class="sxs-lookup"><span data-stu-id="2f186-115">Existing Azure Service</span></span></th>
<th align="left", style="width:10%"><span data-ttu-id="2f186-116">Servicio de aplicaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="2f186-116">Azure App Service</span></span></th>
<th align="left", style="width:80%"><span data-ttu-id="2f186-117">Qué cambia</span><span class="sxs-lookup"><span data-stu-id="2f186-117">What changed</span></span></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><span data-ttu-id="2f186-118">Sitios web Azure</span><span class="sxs-lookup"><span data-stu-id="2f186-118">Azure Websites</span></span></td>
<td align="left"><span data-ttu-id="2f186-119">Web Apps</span><span class="sxs-lookup"><span data-stu-id="2f186-119">Web Apps</span></span></td>
<td align="left"><li><span data-ttu-id="2f186-120">En el caso de Azure Websites, App Service se limita estrictamente a cambiar el nombre de Websites por Web Apps.</span><span class="sxs-lookup"><span data-stu-id="2f186-120">For Azure Websites, App Service is strictly limited to changing the name  Websites to Web Apps.</span></span>
<p><li><span data-ttu-id="2f186-121">Todas las instancias existentes de Sitios web serán ahora Aplicaciones web en el Servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="2f186-121">All your existing instances of Websites are now Web Apps in App Service.</span></span></p>
<p><li><span data-ttu-id="2f186-122">Puede tener acceso a los sitios web existentes a través de <a href="http://go.microsoft.com/fwlink/?LinkId=529715">Azure Portal</a>, donde todos los sitios existentes se encuentran en <em>Web Apps</em>.</span><span class="sxs-lookup"><span data-stu-id="2f186-122">You can access your existing websites via the <a href="http://go.microsoft.com/fwlink/?LinkId=529715">Azure Portal</a>, where you will find all your existing sites under <em>Web Apps</em>.</span></span></p>
<p><li><span data-ttu-id="2f186-123"><em>Plan de hospedaje de Web</em> es ahora <em>Plan de servicio de aplicaciones</em>.</span><span class="sxs-lookup"><span data-stu-id="2f186-123"><em>Web Hosting Plan</em> is now <em>App Service Plan</em>.</span></span> <span data-ttu-id="2f186-124">Un <em>plan de App Service</em> puede hospedar cualquier tipo de aplicación de App Service, como Web Apps, Mobile Apps, Logic Apps o API Apps.</span><span class="sxs-lookup"><span data-stu-id="2f186-124">An <em>App Service Plan</em> can host any app type of App Service, such as Web, Mobile, Logic, or API apps.</span></span></p>
<p><li><span data-ttu-id="2f186-125">Aplicaciones web del Servicio de aplicaciones de Azure tiene ahora disponibilidad general.</span><span class="sxs-lookup"><span data-stu-id="2f186-125">Azure App Service Web Apps is in General Availability.</span></span></p>
<p><li><span data-ttu-id="2f186-126"><a href="http://azure.microsoft.com/services/app-service/web/">Obtener más información sobre las aplicaciones Web</a>.</span><span class="sxs-lookup"><span data-stu-id="2f186-126"><a href="http://azure.microsoft.com/services/app-service/web/">Learn more about Web Apps</a>.</span></span></p></td>
</tr>
<tr class="even">
<td align="left"><span data-ttu-id="2f186-127">Servicios móviles de Azure</span><span class="sxs-lookup"><span data-stu-id="2f186-127">Azure Mobile Services</span></span></td>
<td align="left"><span data-ttu-id="2f186-128">Aplicaciones móviles</span><span class="sxs-lookup"><span data-stu-id="2f186-128">Mobile Apps</span></span></td>
<td align="left"><p><li><span data-ttu-id="2f186-129">Servicios móviles sigue estando disponible como servicio independiente con plena compatibilidad.</span><span class="sxs-lookup"><span data-stu-id="2f186-129">Mobile Services continue to be available as a standalone service and remain fully supported.</span></span></p>
<p><li><span data-ttu-id="2f186-130">Aplicaciones móviles es un tipo de aplicación del servicio de aplicaciones, que integra toda la funcionalidad de los servicios móviles y mucho más.</span><span class="sxs-lookup"><span data-stu-id="2f186-130">Mobile Apps is an app type in App Service, which integrates all of the functionality of Mobile Services and more.</span></span></p>
<p><li><span data-ttu-id="2f186-131">Es fácil <a href="http://go.microsoft.com/fwlink/?LinkID=724279&clcid=0x409">migrar de Mobile Services a Mobile Apps</a>.</span><span class="sxs-lookup"><span data-stu-id="2f186-131">It is easy to <a href="http://go.microsoft.com/fwlink/?LinkID=724279&clcid=0x409">migrate from Mobile Services to Mobile Apps</a>.</span></span></p>
<p><li><span data-ttu-id="2f186-132">Como parte de App Service, Mobile Apps incluye nuevas funcionalidades, además de Mobile Services, como la integración con sistemas locales y SaaS, espacios de ensayo, WebJobs y opciones de escalado mejoradas, entre otras.</span><span class="sxs-lookup"><span data-stu-id="2f186-132">As part of App Service, Mobile Apps get new capabilities beyond Mobile Services, such as  integration with on-premises and SaaS systems, staging slots, WebJobs, better scaling options, and more.</span></span></p>
<p><li><span data-ttu-id="2f186-133"><a href="http://azure.microsoft.com/services/app-service/mobile/">Obtener más información sobre aplicaciones móviles</a>.</span><span class="sxs-lookup"><span data-stu-id="2f186-133"><a href="http://azure.microsoft.com/services/app-service/mobile/">Learn more about Mobile Apps</a>.</span></span></p>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"><span data-ttu-id="2f186-134">API Apps</span><span class="sxs-lookup"><span data-stu-id="2f186-134">API Apps</span></span></td>
<td align="left">
<p><li><span data-ttu-id="2f186-135">Aplicaciones de API es un nuevo tipo de aplicación del Servicio de aplicaciones que permite compilar y consumir API en la nube fácilmente.</span><span class="sxs-lookup"><span data-stu-id="2f186-135">API Apps is a new app type in App Service that lets you easily build and consume APIs in the cloud.</span></span></p>
<p><li><span data-ttu-id="2f186-136"><a href="http://azure.microsoft.com/services/app-service/api/">Más información acerca de las aplicaciones de la API</a>.</span><span class="sxs-lookup"><span data-stu-id="2f186-136"><a href="http://azure.microsoft.com/services/app-service/api/">Learn more about API Apps</a>.</span></span></p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><span data-ttu-id="2f186-137">Logic Apps</span><span class="sxs-lookup"><span data-stu-id="2f186-137">Logic Apps</span></span></td>
<td align="left">
<p><li><span data-ttu-id="2f186-138">Aplicaciones lógicas es un nuevo tipo de aplicación de App Service que permite automatizar los procesos de negocio fácilmente.</span><span class="sxs-lookup"><span data-stu-id="2f186-138">Logic Apps is a new app type in App Service that lets you easily automate business processes.</span></span></p>
<p><li><span data-ttu-id="2f186-139"><a href="http://azure.microsoft.com/services/app-service/logic/">Obtener más información sobre las aplicaciones lógicas</a>.</span><span class="sxs-lookup"><span data-stu-id="2f186-139"><a href="http://azure.microsoft.com/services/app-service/logic/">Learn more about Logic Apps</a>.</span></span></p></td>
</tr>
<tr class="odd">
<td align="left"><span data-ttu-id="2f186-140">Servicios de BizTalk de Azure</span><span class="sxs-lookup"><span data-stu-id="2f186-140">Azure BizTalk Services</span></span></td>
<td align="left"><span data-ttu-id="2f186-141">Aplicaciones de API de BizTalk</span><span class="sxs-lookup"><span data-stu-id="2f186-141">BizTalk API Apps</span></span></td>
<td align="left">
<li><p><span data-ttu-id="2f186-142">Servicios de Biztalk sigue estando disponible como servicio independiente con plena compatibilidad.</span><span class="sxs-lookup"><span data-stu-id="2f186-142">BizTalk Services continue to be available as a standalone service and remain fully supported.</span></span></p>
<li><p><span data-ttu-id="2f186-143">Todas las funcionalidades de BizTalk Services se integran en App Service como API Apps, lo que permite a los usuarios realizar tareas de integración de aplicaciones empresariales y de integración B2B con cualquiera de los tipos de aplicaciones de App Service.</span><span class="sxs-lookup"><span data-stu-id="2f186-143">All the capabilities of BizTalk Services are integrated into App Service as API Apps enabling users to perform enterprise application integration and B2B integration scenarios with any of the app types in App Service.</span></span></p>
<li><p><span data-ttu-id="2f186-144">Ahora, con Logic Apps, puede automatizar los procesos de negocio a través de una experiencia de diseño visual para crear flujos de trabajo.</span><span class="sxs-lookup"><span data-stu-id="2f186-144">With Logic Apps, you can now automate business processes using a visual design experience to create workflows.</span></span></p></td>
</tr>
</tbody>
</table>

<span data-ttu-id="2f186-145">Para obtener más información, visite [Documentación del Servicio de aplicaciones](https://azure.microsoft.com/documentation/services/app-service/).</span><span class="sxs-lookup"><span data-stu-id="2f186-145">To learn more, please visit [App Service documentation](https://azure.microsoft.com/documentation/services/app-service/).</span></span>

