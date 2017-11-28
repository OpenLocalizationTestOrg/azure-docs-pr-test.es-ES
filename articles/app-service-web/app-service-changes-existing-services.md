---
title: aaaAzure servicio de aplicaciones y su impacto en los servicios de Azure existentes
description: "Explica cómo Hola nuevo servicio de aplicación de Azure y sus características de afectan a los servicios existentes en Azure."
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
ms.openlocfilehash: a831a88fee38465e5b0b7c2c2340cf8a0d64c864
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-and-existing-azure-services"></a><span data-ttu-id="160cf-103">Servicio de aplicaciones de Azure y los servicios de Azure existentes</span><span class="sxs-lookup"><span data-stu-id="160cf-103">Azure App Service and existing Azure services</span></span>
<span data-ttu-id="160cf-104">En este artículo se describe Hola cambios tooexisting servicios de Azure como parte de hello cambio toobring junto varios servicios de Azure en [servicio de aplicaciones de Azure](https://azure.microsoft.com/services/app-service/), una nueva oferta integrada.</span><span class="sxs-lookup"><span data-stu-id="160cf-104">This article outlines hello changes tooexisting Azure services as part of hello change toobring together several Azure services into [Azure App Service](https://azure.microsoft.com/services/app-service/), a new integrated offering.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="overview"></a><span data-ttu-id="160cf-105">Información general</span><span class="sxs-lookup"><span data-stu-id="160cf-105">Overview</span></span>
<span data-ttu-id="160cf-106">[Servicio de aplicaciones de Azure](https://azure.microsoft.com/services/app-service/) es un servicio de nube nuevos y únicos que permite a los desarrolladores toocreate web y aplicaciones móviles para cualquier plataforma y en cualquier dispositivo.</span><span class="sxs-lookup"><span data-stu-id="160cf-106">[Azure App Service](https://azure.microsoft.com/services/app-service/) is a new and unique cloud service that enables developers toocreate web and mobile apps for any platform and any device.</span></span> <span data-ttu-id="160cf-107">Servicio de aplicaciones es que una solución integrada diseñada toostreamline repite las funciones de codificación, integrar con enterprise y sistemas de SaaS y automatizar procesos de negocio al tiempo que satisface sus necesidades de seguridad, confiabilidad y escalabilidad.</span><span class="sxs-lookup"><span data-stu-id="160cf-107">App Service is an integrated solution designed toostreamline repeated coding functions, integrate with enterprise and SaaS systems, and automate business processes while meeting your needs for security, reliability, and scalability.</span></span>

<span data-ttu-id="160cf-108">Servicio de aplicaciones reúne Hola después de Azure existentes services - [sitios Web](https://azure.microsoft.com/services/websites/), [servicios móviles](https://azure.microsoft.com/services/mobile-services/), y [servicios de Biztalk](https://azure.microsoft.com/services/biztalk-services/) en una sola combinan servicio, mientras que agregar nuevas capacidades.</span><span class="sxs-lookup"><span data-stu-id="160cf-108">App Service brings together hello following existing Azure services - [Websites](https://azure.microsoft.com/services/websites/), [Mobile Services](https://azure.microsoft.com/services/mobile-services/), and [Biztalk Services](https://azure.microsoft.com/services/biztalk-services/) into a single combined service, while adding powerful new capabilities.</span></span>  <span data-ttu-id="160cf-109">Servicio de aplicaciones permite hello toohost siguientes tipos de aplicación:</span><span class="sxs-lookup"><span data-stu-id="160cf-109">App Service allows you toohost hello following app types:</span></span>

* <span data-ttu-id="160cf-110">Web Apps</span><span class="sxs-lookup"><span data-stu-id="160cf-110">Web Apps</span></span>
* <span data-ttu-id="160cf-111">Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="160cf-111">Mobile Apps</span></span>
* <span data-ttu-id="160cf-112">API Apps</span><span class="sxs-lookup"><span data-stu-id="160cf-112">API Apps</span></span>
* <span data-ttu-id="160cf-113">Logic Apps</span><span class="sxs-lookup"><span data-stu-id="160cf-113">Logic Apps</span></span>

<span data-ttu-id="160cf-114">Hello tabla siguiente explica cómo existente Azure servicios asignan tooApp hello y servicio aplicación tipos disponibles dentro de él.</span><span class="sxs-lookup"><span data-stu-id="160cf-114">hello following table explains how existing Azure services map tooApp Service and hello app types available within it.</span></span>

<table>
<thead>
<tr class="header">
<th align="left", style="width:10%"><span data-ttu-id="160cf-115">Servicio de Azure existente</span><span class="sxs-lookup"><span data-stu-id="160cf-115">Existing Azure Service</span></span></th>
<th align="left", style="width:10%"><span data-ttu-id="160cf-116">Servicio de aplicaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="160cf-116">Azure App Service</span></span></th>
<th align="left", style="width:80%"><span data-ttu-id="160cf-117">Qué cambia</span><span class="sxs-lookup"><span data-stu-id="160cf-117">What changed</span></span></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><span data-ttu-id="160cf-118">Sitios web Azure</span><span class="sxs-lookup"><span data-stu-id="160cf-118">Azure Websites</span></span></td>
<td align="left"><span data-ttu-id="160cf-119">Web Apps</span><span class="sxs-lookup"><span data-stu-id="160cf-119">Web Apps</span></span></td>
<td align="left"><li><span data-ttu-id="160cf-120">Para los sitios Web de Azure, servicio de aplicaciones está estrictamente limitado toochanging Hola nombre sitios Web tooWeb aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="160cf-120">For Azure Websites, App Service is strictly limited toochanging hello name  Websites tooWeb Apps.</span></span>
<p><li><span data-ttu-id="160cf-121">Todas las instancias existentes de Sitios web serán ahora Aplicaciones web en el Servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="160cf-121">All your existing instances of Websites are now Web Apps in App Service.</span></span></p>
<p><li><span data-ttu-id="160cf-122">Puede tener acceso a sus sitios Web existente a través de hello <a href="http://go.microsoft.com/fwlink/?LinkId=529715">Portal de Azure</a>, donde encontrará todos los sitios existentes en <em>aplicaciones Web</em>.</span><span class="sxs-lookup"><span data-stu-id="160cf-122">You can access your existing websites via hello <a href="http://go.microsoft.com/fwlink/?LinkId=529715">Azure Portal</a>, where you will find all your existing sites under <em>Web Apps</em>.</span></span></p>
<p><li><span data-ttu-id="160cf-123"><em>Plan de hospedaje de Web</em> es ahora <em>Plan de servicio de aplicaciones</em>.</span><span class="sxs-lookup"><span data-stu-id="160cf-123"><em>Web Hosting Plan</em> is now <em>App Service Plan</em>.</span></span> <span data-ttu-id="160cf-124">Un <em>plan de App Service</em> puede hospedar cualquier tipo de aplicación de App Service, como Web Apps, Mobile Apps, Logic Apps o API Apps.</span><span class="sxs-lookup"><span data-stu-id="160cf-124">An <em>App Service Plan</em> can host any app type of App Service, such as Web, Mobile, Logic, or API apps.</span></span></p>
<p><li><span data-ttu-id="160cf-125">Aplicaciones web del Servicio de aplicaciones de Azure tiene ahora disponibilidad general.</span><span class="sxs-lookup"><span data-stu-id="160cf-125">Azure App Service Web Apps is in General Availability.</span></span></p>
<p><li><span data-ttu-id="160cf-126"><a href="http://azure.microsoft.com/services/app-service/web/">Obtener más información sobre las aplicaciones Web</a>.</span><span class="sxs-lookup"><span data-stu-id="160cf-126"><a href="http://azure.microsoft.com/services/app-service/web/">Learn more about Web Apps</a>.</span></span></p></td>
</tr>
<tr class="even">
<td align="left"><span data-ttu-id="160cf-127">Servicios móviles de Azure</span><span class="sxs-lookup"><span data-stu-id="160cf-127">Azure Mobile Services</span></span></td>
<td align="left"><span data-ttu-id="160cf-128">Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="160cf-128">Mobile Apps</span></span></td>
<td align="left"><p><li><span data-ttu-id="160cf-129">Servicios móviles continuar toobe disponible como un servicio independiente y siguen siendo totalmente compatibles.</span><span class="sxs-lookup"><span data-stu-id="160cf-129">Mobile Services continue toobe available as a standalone service and remain fully supported.</span></span></p>
<p><li><span data-ttu-id="160cf-130">Aplicaciones móviles es un tipo de aplicación de servicio de aplicaciones, que integra toda la funcionalidad de hello de servicios móviles y mucho más.</span><span class="sxs-lookup"><span data-stu-id="160cf-130">Mobile Apps is an app type in App Service, which integrates all of hello functionality of Mobile Services and more.</span></span></p>
<p><li><span data-ttu-id="160cf-131">Es fácil demasiado<a href="http://go.microsoft.com/fwlink/?LinkID=724279&clcid=0x409">migrar desde servicios móviles tooMobile aplicaciones</a>.</span><span class="sxs-lookup"><span data-stu-id="160cf-131">It is easy too<a href="http://go.microsoft.com/fwlink/?LinkID=724279&clcid=0x409">migrate from Mobile Services tooMobile Apps</a>.</span></span></p>
<p><li><span data-ttu-id="160cf-132">Como parte de App Service, Mobile Apps incluye nuevas funcionalidades, además de Mobile Services, como la integración con sistemas locales y SaaS, espacios de ensayo, WebJobs y opciones de escalado mejoradas, entre otras.</span><span class="sxs-lookup"><span data-stu-id="160cf-132">As part of App Service, Mobile Apps get new capabilities beyond Mobile Services, such as  integration with on-premises and SaaS systems, staging slots, WebJobs, better scaling options, and more.</span></span></p>
<p><li><span data-ttu-id="160cf-133"><a href="http://azure.microsoft.com/services/app-service/mobile/">Obtener más información sobre aplicaciones móviles</a>.</span><span class="sxs-lookup"><span data-stu-id="160cf-133"><a href="http://azure.microsoft.com/services/app-service/mobile/">Learn more about Mobile Apps</a>.</span></span></p>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"><span data-ttu-id="160cf-134">API Apps</span><span class="sxs-lookup"><span data-stu-id="160cf-134">API Apps</span></span></td>
<td align="left">
<p><li><span data-ttu-id="160cf-135">Aplicaciones de API es un nuevo tipo de aplicación de servicio de aplicaciones que permite crear y utilizar las API en la nube de hello con facilidad.</span><span class="sxs-lookup"><span data-stu-id="160cf-135">API Apps is a new app type in App Service that lets you easily build and consume APIs in hello cloud.</span></span></p>
<p><li><span data-ttu-id="160cf-136"><a href="http://azure.microsoft.com/services/app-service/api/">Más información acerca de las aplicaciones de la API</a>.</span><span class="sxs-lookup"><span data-stu-id="160cf-136"><a href="http://azure.microsoft.com/services/app-service/api/">Learn more about API Apps</a>.</span></span></p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><span data-ttu-id="160cf-137">Logic Apps</span><span class="sxs-lookup"><span data-stu-id="160cf-137">Logic Apps</span></span></td>
<td align="left">
<p><li><span data-ttu-id="160cf-138">Aplicaciones lógicas es un nuevo tipo de aplicación de App Service que permite automatizar los procesos de negocio fácilmente.</span><span class="sxs-lookup"><span data-stu-id="160cf-138">Logic Apps is a new app type in App Service that lets you easily automate business processes.</span></span></p>
<p><li><span data-ttu-id="160cf-139"><a href="http://azure.microsoft.com/services/app-service/logic/">Obtener más información sobre las aplicaciones lógicas</a>.</span><span class="sxs-lookup"><span data-stu-id="160cf-139"><a href="http://azure.microsoft.com/services/app-service/logic/">Learn more about Logic Apps</a>.</span></span></p></td>
</tr>
<tr class="odd">
<td align="left"><span data-ttu-id="160cf-140">Servicios de BizTalk de Azure</span><span class="sxs-lookup"><span data-stu-id="160cf-140">Azure BizTalk Services</span></span></td>
<td align="left"><span data-ttu-id="160cf-141">Aplicaciones de API de BizTalk</span><span class="sxs-lookup"><span data-stu-id="160cf-141">BizTalk API Apps</span></span></td>
<td align="left">
<li><p><span data-ttu-id="160cf-142">Servicios de BizTalk continuar toobe disponible como un servicio independiente y siguen siendo totalmente compatibles.</span><span class="sxs-lookup"><span data-stu-id="160cf-142">BizTalk Services continue toobe available as a standalone service and remain fully supported.</span></span></p>
<li><p><span data-ttu-id="160cf-143">Todas las funcionalidades de hello de servicios de BizTalk se integran en servicio de aplicaciones como aplicaciones de API permite a los usuarios tooperform integraciones y escenarios de integración de B2B con cualquiera de los tipos de aplicación hello en el servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="160cf-143">All hello capabilities of BizTalk Services are integrated into App Service as API Apps enabling users tooperform enterprise application integration and B2B integration scenarios with any of hello app types in App Service.</span></span></p>
<li><p><span data-ttu-id="160cf-144">Con las aplicaciones lógicas, ahora puede automatizar procesos empresariales mediante una experiencia visual diseñar toocreate flujos de trabajo.</span><span class="sxs-lookup"><span data-stu-id="160cf-144">With Logic Apps, you can now automate business processes using a visual design experience toocreate workflows.</span></span></p></td>
</tr>
</tbody>
</table>

<span data-ttu-id="160cf-145">toolearn más información, visite [documentación de servicio de aplicaciones](https://azure.microsoft.com/documentation/services/app-service/).</span><span class="sxs-lookup"><span data-stu-id="160cf-145">toolearn more, please visit [App Service documentation](https://azure.microsoft.com/documentation/services/app-service/).</span></span>

