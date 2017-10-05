---
title: "Guía de solución de problemas de Azure Mobile Engagement - Análisis"
description: "Solución de problemas de análisis, supervisión, segmentación y panel en Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 04a7020a-ad74-4491-be69-0bd574890029
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: e30c9ac0a8421ffcf4fc3e2548cfd7ac49701900
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-guide-for-analytics-monitoring-segmentation-and-dashboard-issues"></a><span data-ttu-id="f4466-103">Guía de solución de problemas de análisis, supervisión, segmentación y panel</span><span class="sxs-lookup"><span data-stu-id="f4466-103">Troubleshooting guide for Analytics, Monitoring, Segmentation, and Dashboard issues</span></span>
<span data-ttu-id="f4466-104">Los siguientes son posibles problemas que pueden producirse con cómo reúne Azure Mobile Engagement información acerca de sus aplicaciones, dispositivos y usuarios.</span><span class="sxs-lookup"><span data-stu-id="f4466-104">The following are possible issues you may encounter with how Azure Mobile Engagement gathers information about your applications, devices, and users.</span></span>

## <a name="missingdelayed-information"></a><span data-ttu-id="f4466-105">Información no encontrada o retrasada</span><span class="sxs-lookup"><span data-stu-id="f4466-105">Missing/Delayed information</span></span>
### <a name="issue"></a><span data-ttu-id="f4466-106">Problema</span><span class="sxs-lookup"><span data-stu-id="f4466-106">Issue</span></span>
* <span data-ttu-id="f4466-107">La información se retrasa en aparecer en el análisis, la segmentación o el panel.</span><span class="sxs-lookup"><span data-stu-id="f4466-107">Information is delayed in appearing in Analytics, Segmentation, or Dashboard.</span></span>
* <span data-ttu-id="f4466-108">Falta información en la supervisión.</span><span class="sxs-lookup"><span data-stu-id="f4466-108">Information is missing from Monitoring.</span></span>
* <span data-ttu-id="f4466-109">Falta información de análisis, de la segmentación o del panel.</span><span class="sxs-lookup"><span data-stu-id="f4466-109">Information is missing from Analytics, Segmentation, or Dashboard.</span></span>
* <span data-ttu-id="f4466-110">Alcanzar límites de segmentación.</span><span class="sxs-lookup"><span data-stu-id="f4466-110">Hitting segmentation limits.</span></span>

### <a name="causes"></a><span data-ttu-id="f4466-111">Causas</span><span class="sxs-lookup"><span data-stu-id="f4466-111">Causes</span></span>
* <span data-ttu-id="f4466-112">Puede utilizar la API de análisis, API de supervisión y la API de segmentos para ver si los datos que faltan en la interfaz de usuario están visibles a través de las API.</span><span class="sxs-lookup"><span data-stu-id="f4466-112">You can use the Analytics API, Monitor API, and Segments API to see if any data you are missing from the UI is visible through the APIs.</span></span>
* <span data-ttu-id="f4466-113">Si el SDK de Azure Mobile Engagement no está integrado correctamente en la aplicación no podrá ver la información de análisis, segmentación, supervisión o paneles.</span><span class="sxs-lookup"><span data-stu-id="f4466-113">If the Azure Mobile Engagement SDK is not correctly integrated into your app then you won't be able to see information in the Analytics, Segmentation, Monitoring, or Dashboards.</span></span>
* <span data-ttu-id="f4466-114">Los segmentos no se pueden cambiar una vez creados, solo se pueden "clonar" (copiar) o "destruir" (eliminar).</span><span class="sxs-lookup"><span data-stu-id="f4466-114">Segments can't be changed once they are created, segments can only be "cloned" (copied) or "destroyed" (deleted).</span></span> <span data-ttu-id="f4466-115">Los segmentos solo pueden contener 10 criterios.</span><span class="sxs-lookup"><span data-stu-id="f4466-115">Segments can only contain 10 criteria.</span></span>
* <span data-ttu-id="f4466-116">La mejor manera de probar la información que falta en la supervisión es configurar un dispositivo de prueba y desinstalar o volver a instalar la aplicación en el dispositivo de prueba.</span><span class="sxs-lookup"><span data-stu-id="f4466-116">The best way to test missing information from monitoring is to setup a test device, uninstall and/or reinstall the app on the test device.</span></span>
* <span data-ttu-id="f4466-117">La información se actualiza cada 24 horas para analizarla, segmentarla o para los paneles.</span><span class="sxs-lookup"><span data-stu-id="f4466-117">Information is refreshed every 24 hours for Analytics, Segmentation, or Dashboards.</span></span>
* <span data-ttu-id="f4466-118">Es posible que la información de los segmentos nuevos no se muestre hasta 24 horas después de que se creen, aunque si el segmento se base en información anterior.</span><span class="sxs-lookup"><span data-stu-id="f4466-118">Information in new segments may not be displayed until 24 hours after they are created even if the segment is based on previous information.</span></span>
* <span data-ttu-id="f4466-119">Filtrar los datos de análisis de la interfaz de usuario mostrará todos los ejemplos de este tipo, independientemente de la versión de la aplicación (p. ej., "se bloquea" filtrado por nombre mostrará desde las versiones 1 y 2 de la aplicación).</span><span class="sxs-lookup"><span data-stu-id="f4466-119">Filtering your analytics data in the UI will show all examples of this type regardless of the version of your app (e.g. "Crashes" filtered by name will show from version 1 and version 2 of your app).</span></span>
* <span data-ttu-id="f4466-120">El período de tiempo de análisis se basa en la fecha de la configuración de dispositivo de los usuarios, por lo que un usuario cuyo teléfono tiene la fecha establecida incorrectamente podría aparecer en el período de tiempo incorrecto.</span><span class="sxs-lookup"><span data-stu-id="f4466-120">The time period for Analytics is based on the date from the users' device settings, so a user whose phone has the date incorrectly set could show up in the wrong time period.</span></span>
* <span data-ttu-id="f4466-121">No se registra ningún dato del servidor cuando utiliza el botón para "probar" inserciones, los datos solo se registran para campañas de inserción real.</span><span class="sxs-lookup"><span data-stu-id="f4466-121">No server side data is logged when you use the button to "test" pushes, data is only logged for real push campaigns.</span></span>

## <a name="cant-locate-items-in-ui"></a><span data-ttu-id="f4466-122">No puede buscar los elementos de la interfaz de usuario</span><span class="sxs-lookup"><span data-stu-id="f4466-122">Can't locate items in UI</span></span>
### <a name="issue"></a><span data-ttu-id="f4466-123">Problema</span><span class="sxs-lookup"><span data-stu-id="f4466-123">Issue</span></span>
* <span data-ttu-id="f4466-124">No se pueden crear segmentos basados en determinados criterios de etiqueta de información de la aplicación personalizada o integrada.</span><span class="sxs-lookup"><span data-stu-id="f4466-124">Can't create segments based on certain built in or custom app info tag criteria.</span></span>
* <span data-ttu-id="f4466-125">No se puede encontrar determinados criterios de etiquetas de información de aplicación personalizada o integrada en análisis, supervisión o paneles.</span><span class="sxs-lookup"><span data-stu-id="f4466-125">Can't find certain built in or custom app info tag criteria in Analytics, Monitoring, or Dashboards.</span></span>
* <span data-ttu-id="f4466-126">No se pueden interpretar los datos de análisis, supervisión, segmentación o paneles.</span><span class="sxs-lookup"><span data-stu-id="f4466-126">Can't interpret the data in Analytics, Monitoring, Segmentation, or Dashboards.</span></span>

### <a name="causes"></a><span data-ttu-id="f4466-127">Causas</span><span class="sxs-lookup"><span data-stu-id="f4466-127">Causes</span></span>
* <span data-ttu-id="f4466-128">Algunos elementos integrados y etiquetas de información de aplicación solo están disponibles como criterios de inserción, pero puede que no se agreguen a un segmento o no estén visibles desde el análisis, la supervisión o el panel.</span><span class="sxs-lookup"><span data-stu-id="f4466-128">Some built in items and app info tags are only available as push criteria but may not be added to a segment or visible from Analytics, Monitoring, or Dashboard.</span></span> 
* <span data-ttu-id="f4466-129">Para los elementos integrados y las etiquetas de información de aplicación que no se pueden agregar a un segmento, necesitará configurar la lista de criterios de destinatarios en cada campaña para realizar la misma función que la orientación en función de un segmento.</span><span class="sxs-lookup"><span data-stu-id="f4466-129">For built in items and app info tags that can't be added to a segment, you will need to setup list of targeting criteria in each campaign to perform the same function as targeting based on a segment.</span></span>
* <span data-ttu-id="f4466-130">Consulte los menús contextuales en las secciones de análisis, supervisión, segmentación y paneles de la interfaz de usuario de Azure Mobile Engagement para obtener más ayuda e información práctica.</span><span class="sxs-lookup"><span data-stu-id="f4466-130">See the context menus in the Analytics, Monitoring, Segmentation, and Dashboards sections of the Azure Mobile Engagement UI for more help and how to information.</span></span>

## <a name="crash-troubleshooting"></a><span data-ttu-id="f4466-131">Solución de problemas de bloqueos</span><span class="sxs-lookup"><span data-stu-id="f4466-131">Crash troubleshooting</span></span>
### <a name="issue"></a><span data-ttu-id="f4466-132">Problema</span><span class="sxs-lookup"><span data-stu-id="f4466-132">Issue</span></span>
* <span data-ttu-id="f4466-133">Bloqueos de la aplicación que aparecen en el panel, supervisión o análisis.</span><span class="sxs-lookup"><span data-stu-id="f4466-133">Application Crashes appearing in Analytics, Monitoring, or Dashboard.</span></span>

### <a name="causes"></a><span data-ttu-id="f4466-134">Causas</span><span class="sxs-lookup"><span data-stu-id="f4466-134">Causes</span></span>
* <span data-ttu-id="f4466-135">Para solucionar problemas de bloqueos de aplicaciones vistos en el análisis, la supervisión o el panel, asegúrese de comprobar las notas de la versión para obtener información sobre problemas conocidos con las versiones anteriores del SDK.</span><span class="sxs-lookup"><span data-stu-id="f4466-135">To troubleshoot Application Crashes seen in Analytics, Monitoring, or Dashboard make sure to check the release notes for known issues with previous versions of the SDK.</span></span>
* <span data-ttu-id="f4466-136">Para solucionar más bloqueos de la aplicación, realice un evento desde un dispositivo de prueba con la aplicación instalada y buscar el identificador del dispositivo en la sección "Monitor – eventos" de la interfaz de usuario de Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="f4466-136">To further troubleshoot application crashes perform an event from a test device with your application installed and look up your device ID in the “Monitor – Events” section of the Azure Mobile Engagement UI.</span></span> <span data-ttu-id="f4466-137">Después, realice el evento que causa que la aplicación se bloquee y busque información adicional en la sección "Supervisión – Bloqueo" de la interfaz de usuario de Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="f4466-137">Then perform the event that is causing your application to crash and look up additional information in the “Monitor – Crash” section of the Azure Mobile Engagement UI.</span></span> 

