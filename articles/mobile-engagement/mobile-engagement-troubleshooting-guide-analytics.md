---
title: "aaaAzure Mobile Engagement Troubleshooting Guide - análisis"
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
ms.openlocfilehash: 69c6ff8f5c8540f8ba8b85b9ffec55acc59329fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-analytics-monitoring-segmentation-and-dashboard-issues"></a><span data-ttu-id="8aade-103">Guía de solución de problemas de análisis, supervisión, segmentación y panel</span><span class="sxs-lookup"><span data-stu-id="8aade-103">Troubleshooting guide for Analytics, Monitoring, Segmentation, and Dashboard issues</span></span>
<span data-ttu-id="8aade-104">Hello siguientes son posibles problemas que pueden producirse con el modo en que Azure Mobile Engagement recopila información sobre los usuarios, dispositivos y aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="8aade-104">hello following are possible issues you may encounter with how Azure Mobile Engagement gathers information about your applications, devices, and users.</span></span>

## <a name="missingdelayed-information"></a><span data-ttu-id="8aade-105">Información no encontrada o retrasada</span><span class="sxs-lookup"><span data-stu-id="8aade-105">Missing/Delayed information</span></span>
### <a name="issue"></a><span data-ttu-id="8aade-106">Problema</span><span class="sxs-lookup"><span data-stu-id="8aade-106">Issue</span></span>
* <span data-ttu-id="8aade-107">La información se retrasa en aparecer en el análisis, la segmentación o el panel.</span><span class="sxs-lookup"><span data-stu-id="8aade-107">Information is delayed in appearing in Analytics, Segmentation, or Dashboard.</span></span>
* <span data-ttu-id="8aade-108">Falta información en la supervisión.</span><span class="sxs-lookup"><span data-stu-id="8aade-108">Information is missing from Monitoring.</span></span>
* <span data-ttu-id="8aade-109">Falta información de análisis, de la segmentación o del panel.</span><span class="sxs-lookup"><span data-stu-id="8aade-109">Information is missing from Analytics, Segmentation, or Dashboard.</span></span>
* <span data-ttu-id="8aade-110">Alcanzar límites de segmentación.</span><span class="sxs-lookup"><span data-stu-id="8aade-110">Hitting segmentation limits.</span></span>

### <a name="causes"></a><span data-ttu-id="8aade-111">Causas</span><span class="sxs-lookup"><span data-stu-id="8aade-111">Causes</span></span>
* <span data-ttu-id="8aade-112">Puede usar Hola API de análisis, API de Monitor, y API de segmentos toosee si los datos faltan desde la interfaz de usuario de hello es visible a través de hello API.</span><span class="sxs-lookup"><span data-stu-id="8aade-112">You can use hello Analytics API, Monitor API, and Segments API toosee if any data you are missing from hello UI is visible through hello APIs.</span></span>
* <span data-ttu-id="8aade-113">Si hello Azure Mobile Engagement SDK no se integra correctamente en la aplicación no será capaz de toosee información Hola análisis, segmentación, supervisión o paneles.</span><span class="sxs-lookup"><span data-stu-id="8aade-113">If hello Azure Mobile Engagement SDK is not correctly integrated into your app then you won't be able toosee information in hello Analytics, Segmentation, Monitoring, or Dashboards.</span></span>
* <span data-ttu-id="8aade-114">Los segmentos no se pueden cambiar una vez creados, solo se pueden "clonar" (copiar) o "destruir" (eliminar).</span><span class="sxs-lookup"><span data-stu-id="8aade-114">Segments can't be changed once they are created, segments can only be "cloned" (copied) or "destroyed" (deleted).</span></span> <span data-ttu-id="8aade-115">Los segmentos solo pueden contener 10 criterios.</span><span class="sxs-lookup"><span data-stu-id="8aade-115">Segments can only contain 10 criteria.</span></span>
* <span data-ttu-id="8aade-116">Hola mejor manera tootest falta información de la supervisión es toosetup un dispositivo de prueba, desinstalar o volver a instalar la aplicación hello en dispositivo de prueba de Hola.</span><span class="sxs-lookup"><span data-stu-id="8aade-116">hello best way tootest missing information from monitoring is toosetup a test device, uninstall and/or reinstall hello app on hello test device.</span></span>
* <span data-ttu-id="8aade-117">La información se actualiza cada 24 horas para analizarla, segmentarla o para los paneles.</span><span class="sxs-lookup"><span data-stu-id="8aade-117">Information is refreshed every 24 hours for Analytics, Segmentation, or Dashboards.</span></span>
* <span data-ttu-id="8aade-118">Información de los nuevos segmentos no puede mostrarse hasta 24 horas después de que se creen incluso si el segmento de Hola se basa en la información anterior.</span><span class="sxs-lookup"><span data-stu-id="8aade-118">Information in new segments may not be displayed until 24 hours after they are created even if hello segment is based on previous information.</span></span>
* <span data-ttu-id="8aade-119">Filtrado de los datos de análisis en la interfaz de usuario de hello le mostrará todos los ejemplos de este tipo, independientemente de la versión de hello de la aplicación (por ejemplo "se bloquea" filtrado por nombre mostrará desde las versiones 1 y 2 de la aplicación).</span><span class="sxs-lookup"><span data-stu-id="8aade-119">Filtering your analytics data in hello UI will show all examples of this type regardless of hello version of your app (e.g. "Crashes" filtered by name will show from version 1 and version 2 of your app).</span></span>
* <span data-ttu-id="8aade-120">Hello período de tiempo para el análisis se basa en hello fecha de la configuración de dispositivo de los usuarios de hello, por lo que un usuario cuyo teléfono tiene fecha Hola establecido incorrectamente podría aparecer en hello incorrecto período de tiempo.</span><span class="sxs-lookup"><span data-stu-id="8aade-120">hello time period for Analytics is based on hello date from hello users' device settings, so a user whose phone has hello date incorrectly set could show up in hello wrong time period.</span></span>
* <span data-ttu-id="8aade-121">Inserta ningún servidor datos se registran cuando se usa el botón de hello demasiado "test", solo los datos se registran para las campañas de inserción real.</span><span class="sxs-lookup"><span data-stu-id="8aade-121">No server side data is logged when you use hello button too"test" pushes, data is only logged for real push campaigns.</span></span>

## <a name="cant-locate-items-in-ui"></a><span data-ttu-id="8aade-122">No puede buscar los elementos de la interfaz de usuario</span><span class="sxs-lookup"><span data-stu-id="8aade-122">Can't locate items in UI</span></span>
### <a name="issue"></a><span data-ttu-id="8aade-123">Problema</span><span class="sxs-lookup"><span data-stu-id="8aade-123">Issue</span></span>
* <span data-ttu-id="8aade-124">No se pueden crear segmentos basados en determinados criterios de etiqueta de información de la aplicación personalizada o integrada.</span><span class="sxs-lookup"><span data-stu-id="8aade-124">Can't create segments based on certain built in or custom app info tag criteria.</span></span>
* <span data-ttu-id="8aade-125">No se puede encontrar determinados criterios de etiquetas de información de aplicación personalizada o integrada en análisis, supervisión o paneles.</span><span class="sxs-lookup"><span data-stu-id="8aade-125">Can't find certain built in or custom app info tag criteria in Analytics, Monitoring, or Dashboards.</span></span>
* <span data-ttu-id="8aade-126">No se puede interpretar los datos de hello en análisis, supervisión, segmentación o paneles.</span><span class="sxs-lookup"><span data-stu-id="8aade-126">Can't interpret hello data in Analytics, Monitoring, Segmentation, or Dashboards.</span></span>

### <a name="causes"></a><span data-ttu-id="8aade-127">Causas</span><span class="sxs-lookup"><span data-stu-id="8aade-127">Causes</span></span>
* <span data-ttu-id="8aade-128">Algunas integradas en elementos e información de la aplicación etiquetas solo están disponibles como criterios de inserción, pero no puede agrega segmento tooa o visible desde el análisis, supervisión o panel.</span><span class="sxs-lookup"><span data-stu-id="8aade-128">Some built in items and app info tags are only available as push criteria but may not be added tooa segment or visible from Analytics, Monitoring, or Dashboard.</span></span> 
* <span data-ttu-id="8aade-129">En elementos e información de aplicación etiquetas que no se pueden agregan segmento tooa integrados, necesitará toosetup lista de destinatarios de criterios en cada hello tooperform de campaña la misma función que en función de un segmento de destino.</span><span class="sxs-lookup"><span data-stu-id="8aade-129">For built in items and app info tags that can't be added tooa segment, you will need toosetup list of targeting criteria in each campaign tooperform hello same function as targeting based on a segment.</span></span>
* <span data-ttu-id="8aade-130">Vea los menús contextuales de hello en secciones de análisis, supervisión, segmentación y paneles de Hola de hello interfaz de usuario de Azure Mobile Engagement para obtener más ayuda y cómo tooinformation.</span><span class="sxs-lookup"><span data-stu-id="8aade-130">See hello context menus in hello Analytics, Monitoring, Segmentation, and Dashboards sections of hello Azure Mobile Engagement UI for more help and how tooinformation.</span></span>

## <a name="crash-troubleshooting"></a><span data-ttu-id="8aade-131">Solución de problemas de bloqueos</span><span class="sxs-lookup"><span data-stu-id="8aade-131">Crash troubleshooting</span></span>
### <a name="issue"></a><span data-ttu-id="8aade-132">Problema</span><span class="sxs-lookup"><span data-stu-id="8aade-132">Issue</span></span>
* <span data-ttu-id="8aade-133">Bloqueos de la aplicación que aparecen en el panel, supervisión o análisis.</span><span class="sxs-lookup"><span data-stu-id="8aade-133">Application Crashes appearing in Analytics, Monitoring, or Dashboard.</span></span>

### <a name="causes"></a><span data-ttu-id="8aade-134">Causas</span><span class="sxs-lookup"><span data-stu-id="8aade-134">Causes</span></span>
* <span data-ttu-id="8aade-135">tootroubleshoot aplicación se bloquea visto en el análisis, supervisión o panel realizar seguro toocheck Hola notas a los problemas conocidos con las versiones anteriores de hello SDK.</span><span class="sxs-lookup"><span data-stu-id="8aade-135">tootroubleshoot Application Crashes seen in Analytics, Monitoring, or Dashboard make sure toocheck hello release notes for known issues with previous versions of hello SDK.</span></span>
* <span data-ttu-id="8aade-136">toofurther solucionar problemas de aplicación realizan un evento desde un dispositivo de prueba con la aplicación se instale y buscar su ID de dispositivo en la sección de Hola "Monitor de – eventos" de la interfaz de usuario de Azure Mobile Engagement Hola los bloqueos.</span><span class="sxs-lookup"><span data-stu-id="8aade-136">toofurther troubleshoot application crashes perform an event from a test device with your application installed and look up your device ID in hello “Monitor – Events” section of hello Azure Mobile Engagement UI.</span></span> <span data-ttu-id="8aade-137">A continuación, realizar eventos Hola que esté ocasionando la toocrash de aplicación y buscar información adicional en hello "Monitor – bloquearse" sección de la interfaz de usuario de Azure Mobile Engagement Hola.</span><span class="sxs-lookup"><span data-stu-id="8aade-137">Then perform hello event that is causing your application toocrash and look up additional information in hello “Monitor – Crash” section of hello Azure Mobile Engagement UI.</span></span> 

