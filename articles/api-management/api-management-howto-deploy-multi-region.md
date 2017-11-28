---
title: "Administración de API de Azure aaaDeploy services toomultiple Azure regiones | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toodeploy una administración de API de Azure service instancia toomultiple Azure regiones."
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
ms.openlocfilehash: 04a3e762261237d73a769320a21363f99f1d20cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-an-azure-api-management-service-instance-toomultiple-azure-regions"></a><span data-ttu-id="73926-103">Cómo toodeploy una administración de API de Azure service instancia toomultiple Azure regiones</span><span class="sxs-lookup"><span data-stu-id="73926-103">How toodeploy an Azure API Management service instance toomultiple Azure regions</span></span>
<span data-ttu-id="73926-104">Administración de API admite la implementación de varias regiones que habilita la API publicadores toodistribute un único servicio de administración de API a través de cualquier número de regiones de Azure deseadas.</span><span class="sxs-lookup"><span data-stu-id="73926-104">API Management supports multi-region deployment which enables API publishers toodistribute a single API management service across any number of desired Azure regions.</span></span> <span data-ttu-id="73926-105">Esto ayuda a reducir la latencia de solicitud que perciben los usuarios de API distribuidos geográficamente y, además, mejora la disponibilidad del servicio en caso de que una región se quede sin conexión.</span><span class="sxs-lookup"><span data-stu-id="73926-105">This helps reduce request latency perceived by geographically distributed API consumers and also improves service availability if one region goes offline.</span></span> 

<span data-ttu-id="73926-106">Cuando se crea inicialmente un servicio de administración de API, contiene solamente un [unidad] [ unit] y reside en una sola región de Azure, que se designa como Hola región principal.</span><span class="sxs-lookup"><span data-stu-id="73926-106">When an API Management service is created initially, it contains only one [unit][unit] and resides in a single Azure region, which is designated as hello Primary Region.</span></span> <span data-ttu-id="73926-107">Otras regiones pueden agregarse fácilmente a través de hello Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="73926-107">Additional regions can be easily added through hello Azure Portal.</span></span> <span data-ttu-id="73926-108">Un servidor de puerta de enlace de administración de API es región tooeach implementado y el tráfico de llamada será toohello enrutado puerta de enlace más cercano.</span><span class="sxs-lookup"><span data-stu-id="73926-108">An API Management gateway server is deployed tooeach region and call traffic will be routed toohello closest gateway.</span></span> <span data-ttu-id="73926-109">Si una región se queda sin conexión, el tráfico de hello es toohello redirige automáticamente siguiente más cercano puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="73926-109">If a region goes offline, hello traffic is automatically re-directed toohello next closest gateway.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="73926-110">Implementación de varias regiones solo está disponible en hello  **[Premium] [ Premium]**  capa.</span><span class="sxs-lookup"><span data-stu-id="73926-110">Multi-region deployment is only available in hello **[Premium][Premium]** tier.</span></span>
> 
> 

## <span data-ttu-id="73926-111"><a name="add-region"></a>Implementar un área nueva de administración de API servicio instancia tooa</span><span class="sxs-lookup"><span data-stu-id="73926-111"><a name="add-region"> </a>Deploy an API Management service instance tooa new region</span></span>
> [!NOTE]
> <span data-ttu-id="73926-112">Si aún no ha creado una instancia de servicio de administración de API, consulte [crear una instancia de servicio de administración de API] [ Create an API Management service instance] en hello [Introducción a administración de API de Azure] [ Get started with Azure API Management] tutorial.</span><span class="sxs-lookup"><span data-stu-id="73926-112">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="73926-113">Hola Portal de Azure, navegue toohello **escala y precios** página para la instancia de servicio de administración de API.</span><span class="sxs-lookup"><span data-stu-id="73926-113">In hello Azure Portal navigate toohello **Scale and pricing** page for your API Management service instance.</span></span> 

![Pestaña Escala][api-management-scale-service]

<span data-ttu-id="73926-115">toodeploy tooa nueva región, haga clic en **+ Agregar región** de barra de herramientas de Hola.</span><span class="sxs-lookup"><span data-stu-id="73926-115">toodeploy tooa new region, click on **+ Add region** from hello toolbar.</span></span>

![Agregar región][api-management-add-region]

<span data-ttu-id="73926-117">Seleccionar ubicación de hello en la lista desplegable de Hola y establecer el número de Hola de unidades con el control deslizante de Hola.</span><span class="sxs-lookup"><span data-stu-id="73926-117">Select hello location from hello drop-down list and set hello number of units for with hello slider.</span></span>

![Especificar unidades][api-management-select-location-units]

<span data-ttu-id="73926-119">Haga clic en **agregar** tooplace su selección en la tabla de ubicaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="73926-119">Click **Add** tooplace your selection in hello Locations table.</span></span> 

<span data-ttu-id="73926-120">Repita este proceso hasta que haya configurado de todas las ubicaciones y haga clic en **guardar** del proceso de implementación de hello barra de herramientas toostart Hola.</span><span class="sxs-lookup"><span data-stu-id="73926-120">Repeat this process until you have all locations configured and click **Save** from hello toolbar toostart hello deployment process.</span></span>

## <span data-ttu-id="73926-121"><a name="remove-region"></a>Eliminación de una instancia de servicio de API Management de una ubicación</span><span class="sxs-lookup"><span data-stu-id="73926-121"><a name="remove-region"> </a>Delete an API Management service instance from a location</span></span>
<span data-ttu-id="73926-122">Hola Portal de Azure, navegue toohello **escala y precios** página para la instancia de servicio de administración de API.</span><span class="sxs-lookup"><span data-stu-id="73926-122">In hello Azure Portal navigate toohello **Scale and pricing** page for your API Management service instance.</span></span> 

![Pestaña Escala][api-management-scale-service]

<span data-ttu-id="73926-124">Para la ubicación de hello le gustaría tooremove abrir menú contextual de hello mediante hello **...**  situado en el extremo derecho de Hola de tabla Hola.</span><span class="sxs-lookup"><span data-stu-id="73926-124">For hello location you would like tooremove open hello context menu using hello **...** button at hello right end of hello table.</span></span> <span data-ttu-id="73926-125">Seleccione hello **eliminar** opción.</span><span class="sxs-lookup"><span data-stu-id="73926-125">Select hello **Delete** option.</span></span>

![Quitar región][api-management-remove-region]

<span data-ttu-id="73926-127">Confirmar eliminación de Hola y haga clic en **guardar** cambios de hello tooapply.</span><span class="sxs-lookup"><span data-stu-id="73926-127">Confirm hello deletion and click **Save** tooapply hello changes.</span></span>

[api-management-management-console]: ./media/api-management-howto-deploy-multi-region/api-management-management-console.png

[api-management-scale-service]: ./media/api-management-howto-deploy-multi-region/api-management-scale-service.png
[api-management-add-region]: ./media/api-management-howto-deploy-multi-region/api-management-add-region.png
[api-management-select-location-units]: ./media/api-management-howto-deploy-multi-region/api-management-select-location-units.png
[api-management-remove-region]: ./media/api-management-howto-deploy-multi-region/api-management-remove-region.png

[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Get started with Azure API Management]: api-management-get-started.md

[Deploy an API Management service instance tooa new region]: #add-region
[Delete an API Management service instance from a region]: #remove-region

[unit]: http://azure.microsoft.com/pricing/details/api-management/
[Premium]: http://azure.microsoft.com/pricing/details/api-management/

