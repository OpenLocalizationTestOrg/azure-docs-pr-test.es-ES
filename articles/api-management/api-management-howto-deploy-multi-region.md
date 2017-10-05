---
title: "Implementación de servicios de Azure API Management en varias regiones de Azure | Microsoft Docs"
description: "Aprenda a implementar una instancia del servicio Administración de API de Azure en varias regiones de Azure."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 47389ad6-f865-4706-833f-846115e22e4d
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 1c39fee739c2f5fd4b928e1e76e1ea57f072b5f8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-deploy-an-azure-api-management-service-instance-to-multiple-azure-regions"></a><span data-ttu-id="8549b-103">Implementación de una instancia del servicio Administración de API de Azure en varias regiones de Azure</span><span class="sxs-lookup"><span data-stu-id="8549b-103">How to deploy an Azure API Management service instance to multiple Azure regions</span></span>
<span data-ttu-id="8549b-104">Administración de API admite la implementación en varias regiones, lo que permite a los publicadores de API distribuir un único servicio de Administración de API en el número de regiones de Azure deseado.</span><span class="sxs-lookup"><span data-stu-id="8549b-104">API Management supports multi-region deployment which enables API publishers to distribute a single API management service across any number of desired Azure regions.</span></span> <span data-ttu-id="8549b-105">Esto ayuda a reducir la latencia de solicitud que perciben los usuarios de API distribuidos geográficamente y, además, mejora la disponibilidad del servicio en caso de que una región se quede sin conexión.</span><span class="sxs-lookup"><span data-stu-id="8549b-105">This helps reduce request latency perceived by geographically distributed API consumers and also improves service availability if one region goes offline.</span></span> 

<span data-ttu-id="8549b-106">Al crear inicialmente un servicio de API Management, este contiene solo una [unidad][unit] y reside en una sola región de Azure, designada como región primaria.</span><span class="sxs-lookup"><span data-stu-id="8549b-106">When an API Management service is created initially, it contains only one [unit][unit] and resides in a single Azure region, which is designated as the Primary Region.</span></span> <span data-ttu-id="8549b-107">Pueden agregarse otras regiones fácilmente mediante Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="8549b-107">Additional regions can be easily added through the Azure Portal.</span></span> <span data-ttu-id="8549b-108">El servidor de puerta de enlace de API Management se implementa en cada región y el tráfico de llamada se enruta a la puerta de enlace más cercana.</span><span class="sxs-lookup"><span data-stu-id="8549b-108">An API Management gateway server is deployed to each region and call traffic will be routed to the closest gateway.</span></span> <span data-ttu-id="8549b-109">Cuando una región se queda sin conexión, el tráfico se redirige automáticamente a la siguiente puerta de enlace más cercana.</span><span class="sxs-lookup"><span data-stu-id="8549b-109">If a region goes offline, the traffic is automatically re-directed to the next closest gateway.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="8549b-110">La implementación en varias regiones solo está disponible en el nivel **[Premium][Premium]**.</span><span class="sxs-lookup"><span data-stu-id="8549b-110">Multi-region deployment is only available in the **[Premium][Premium]** tier.</span></span>
> 
> 

## <span data-ttu-id="8549b-111"><a name="add-region"> </a>Implementación de una instancia del servicio Administración de API en una nueva región</span><span class="sxs-lookup"><span data-stu-id="8549b-111"><a name="add-region"> </a>Deploy an API Management service instance to a new region</span></span>
> [!NOTE]
> <span data-ttu-id="8549b-112">Si aún no ha creado ninguna instancia del servicio de API Management, consulte [Creación de una instancia del servicio API Management][Create an API Management service instance] en el tutorial [Introducción a Azure API Management][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="8549b-112">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="8549b-113">En Azure Portal, vaya a la página de **escala y precios** de su instancia de servicio de API Management.</span><span class="sxs-lookup"><span data-stu-id="8549b-113">In the Azure Portal navigate to the **Scale and pricing** page for your API Management service instance.</span></span> 

![Pestaña Escala][api-management-scale-service]

<span data-ttu-id="8549b-115">Para implementar en una nueva región, haga clic en **+ Agregar región** desde la barra de herramientas.</span><span class="sxs-lookup"><span data-stu-id="8549b-115">To deploy to a new region, click on **+ Add region** from the toolbar.</span></span>

![Agregar región][api-management-add-region]

<span data-ttu-id="8549b-117">Seleccione la ubicación en la lista desplegable y establezca el número de unidades para el control deslizante.</span><span class="sxs-lookup"><span data-stu-id="8549b-117">Select the location from the drop-down list and set the number of units for with the slider.</span></span>

![Especificar unidades][api-management-select-location-units]

<span data-ttu-id="8549b-119">Haga clic en **Agregar** para colocar la selección en la tabla de ubicaciones.</span><span class="sxs-lookup"><span data-stu-id="8549b-119">Click **Add** to place your selection in the Locations table.</span></span> 

<span data-ttu-id="8549b-120">Repita este proceso hasta que haya configurado todas las ubicaciones y haga clic en **Guardar** en la barra de herramientas para iniciar el proceso de implementación.</span><span class="sxs-lookup"><span data-stu-id="8549b-120">Repeat this process until you have all locations configured and click **Save** from the toolbar to start the deployment process.</span></span>

## <span data-ttu-id="8549b-121"><a name="remove-region"> </a>Eliminación de una instancia de servicio de API Management de una ubicación</span><span class="sxs-lookup"><span data-stu-id="8549b-121"><a name="remove-region"> </a>Delete an API Management service instance from a location</span></span>
<span data-ttu-id="8549b-122">En Azure Portal, vaya a la página de **escala y precios** de su instancia de servicio de API Management.</span><span class="sxs-lookup"><span data-stu-id="8549b-122">In the Azure Portal navigate to the **Scale and pricing** page for your API Management service instance.</span></span> 

![Pestaña Escala][api-management-scale-service]

<span data-ttu-id="8549b-124">Para la ubicación que desee quitar, abra el menú contextual mediante el botón **...** situado a la derecha de la tabla.</span><span class="sxs-lookup"><span data-stu-id="8549b-124">For the location you would like to remove open the context menu using the **...** button at the right end of the table.</span></span> <span data-ttu-id="8549b-125">Haga clic en la opción **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="8549b-125">Select the **Delete** option.</span></span>

![Quitar región][api-management-remove-region]

<span data-ttu-id="8549b-127">Confirme la eliminación y haga clic en **Guardar** para aplicar los cambios.</span><span class="sxs-lookup"><span data-stu-id="8549b-127">Confirm the deletion and click **Save** to apply the changes.</span></span>

[api-management-management-console]: ./media/api-management-howto-deploy-multi-region/api-management-management-console.png

[api-management-scale-service]: ./media/api-management-howto-deploy-multi-region/api-management-scale-service.png
[api-management-add-region]: ./media/api-management-howto-deploy-multi-region/api-management-add-region.png
[api-management-select-location-units]: ./media/api-management-howto-deploy-multi-region/api-management-select-location-units.png
[api-management-remove-region]: ./media/api-management-howto-deploy-multi-region/api-management-remove-region.png

[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Get started with Azure API Management]: api-management-get-started.md

[Deploy an API Management service instance to a new region]: #add-region
[Delete an API Management service instance from a region]: #remove-region

[unit]: http://azure.microsoft.com/pricing/details/api-management/
[Premium]: http://azure.microsoft.com/pricing/details/api-management/

