---
title: "Estadísticas en tiempo real en la red CDN de Azure | Microsoft Docs"
description: "Las estadísticas en tiempo real proporcionan datos en tiempo real sobre el rendimiento de la red CDN de Azure al entregar contenido a los clientes."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: c7989340-1172-4315-acbb-186ba34dd52a
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: e9b9522de6b2c54dc794b00100ffe358296ecfdd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="real-time-stats-in-microsoft-azure-cdn"></a><span data-ttu-id="6847f-103">Estadísticas en tiempo real en la CDN de Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="6847f-103">Real-time stats in Microsoft Azure CDN</span></span>
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a><span data-ttu-id="6847f-104">Información general</span><span class="sxs-lookup"><span data-stu-id="6847f-104">Overview</span></span>
<span data-ttu-id="6847f-105">En este documento se describe la funcionalidad de Estadísticas en tiempo real en la CDN de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="6847f-105">This document explains real-time stats in Microsoft Azure CDN.</span></span>  <span data-ttu-id="6847f-106">Esta funcionalidad proporciona datos en tiempo real, como el ancho de banda, los estados de la memoria caché y las conexiones simultáneas a su perfil de red CDN cuando se entrega el contenido a los clientes.</span><span class="sxs-lookup"><span data-stu-id="6847f-106">This functionality provides real-time data, such as bandwidth, cache statuses, and concurrent connections to your CDN profile when delivering content to your clients.</span></span> <span data-ttu-id="6847f-107">Esto permite la supervisión continua del estado de su servicio en cualquier momento, incluidos los eventos de puesta en marcha.</span><span class="sxs-lookup"><span data-stu-id="6847f-107">This enables continuous monitoring of the health of your service at any time, including go-live events.</span></span>

<span data-ttu-id="6847f-108">Los gráficos siguientes están disponibles:</span><span class="sxs-lookup"><span data-stu-id="6847f-108">The following graphs are available:</span></span>

* [<span data-ttu-id="6847f-109">Ancho de banda</span><span class="sxs-lookup"><span data-stu-id="6847f-109">Bandwidth</span></span>](#bandwidth)
* [<span data-ttu-id="6847f-110">Códigos de estado</span><span class="sxs-lookup"><span data-stu-id="6847f-110">Status Codes</span></span>](#status-codes)
* [<span data-ttu-id="6847f-111">Estados de la memoria caché</span><span class="sxs-lookup"><span data-stu-id="6847f-111">Cache Statuses</span></span>](#cache-statuses)
* [<span data-ttu-id="6847f-112">Conexiones</span><span class="sxs-lookup"><span data-stu-id="6847f-112">Connections</span></span>](#connections)

## <a name="accessing-real-time-stats"></a><span data-ttu-id="6847f-113">Acceso a estadísticas en tiempo real</span><span class="sxs-lookup"><span data-stu-id="6847f-113">Accessing real-time stats</span></span>
1. <span data-ttu-id="6847f-114">En el [Portal de Azure](https://portal.azure.com), vaya a su perfil de la red CDN.</span><span class="sxs-lookup"><span data-stu-id="6847f-114">In the [Azure Portal](https://portal.azure.com), browse to your CDN profile.</span></span>
   
    ![Hoja del perfil de red CDN](./media/cdn-real-time-stats/cdn-profile-blade.png)
2. <span data-ttu-id="6847f-116">En la hoja de perfil de CDN, haga clic en el botón **Administrar** .</span><span class="sxs-lookup"><span data-stu-id="6847f-116">From the CDN profile blade, click the **Manage** button.</span></span>
   
    ![Botón de administración de hoja de perfil de red CDN](./media/cdn-real-time-stats/cdn-manage-btn.png)
   
    <span data-ttu-id="6847f-118">Se abre el portal de administración de CDN.</span><span class="sxs-lookup"><span data-stu-id="6847f-118">The CDN management portal opens.</span></span>
3. <span data-ttu-id="6847f-119">Mantenga el mouse sobre la pestaña **Análisis** y, después, sobre el control flotante **Estadísticas en tiempo real**.</span><span class="sxs-lookup"><span data-stu-id="6847f-119">Hover over the **Analytics** tab, then hover over the **Real-Time Stats** flyout.</span></span>  <span data-ttu-id="6847f-120">Haga clic en **Objeto grande HTTP**.</span><span class="sxs-lookup"><span data-stu-id="6847f-120">Click on **HTTP Large Object**.</span></span>
   
    ![Portal de administración de la red CDN](./media/cdn-real-time-stats/cdn-premium-portal.png)
   
    <span data-ttu-id="6847f-122">Se muestran los gráficos de estadísticas en tiempo real.</span><span class="sxs-lookup"><span data-stu-id="6847f-122">The real-time stats graphs are displayed.</span></span>

<span data-ttu-id="6847f-123">Cada uno de los gráficos muestra estadísticas en tiempo real para el intervalo de tiempo seleccionado, a partir del momento en que se carga la página.</span><span class="sxs-lookup"><span data-stu-id="6847f-123">Each of the graphs displays real-time statistics for the selected time span, starting when the page loads.</span></span>  <span data-ttu-id="6847f-124">Los gráficos se actualizan automáticamente cada pocos segundos.</span><span class="sxs-lookup"><span data-stu-id="6847f-124">The graphs update automatically every few seconds.</span></span>  <span data-ttu-id="6847f-125">El botón **Actualizar gráfico** , si está presente, borrará el gráfico y solo se mostrarán los datos seleccionados.</span><span class="sxs-lookup"><span data-stu-id="6847f-125">The **Refresh Graph** button, if present, will clear the graph, after which it will only display the selected data.</span></span>

## <a name="bandwidth"></a><span data-ttu-id="6847f-126">Ancho de banda</span><span class="sxs-lookup"><span data-stu-id="6847f-126">Bandwidth</span></span>
![Gráfico Ancho de banda](./media/cdn-real-time-stats/cdn-bandwidth.png)

<span data-ttu-id="6847f-128">El gráfico **Ancho de banda** muestra la cantidad de ancho de banda que se usa en la plataforma actual durante el intervalo de tiempo especificado.</span><span class="sxs-lookup"><span data-stu-id="6847f-128">The **Bandwidth** graph displays the amount of bandwidth used for the current platform over the selected time span.</span></span> <span data-ttu-id="6847f-129">La parte sombreada del gráfico indica el uso de ancho de banda.</span><span class="sxs-lookup"><span data-stu-id="6847f-129">The shaded portion of the graph indicates bandwidth usage.</span></span> <span data-ttu-id="6847f-130">La cantidad exacta del ancho de banda que se usa actualmente se muestra directamente debajo del gráfico de líneas.</span><span class="sxs-lookup"><span data-stu-id="6847f-130">The exact amount of bandwidth currently being used is displayed directly below the line graph.</span></span>

## <a name="status-codes"></a><span data-ttu-id="6847f-131">Códigos de estado</span><span class="sxs-lookup"><span data-stu-id="6847f-131">Status Codes</span></span>
![Gráfico Código de estado](./media/cdn-real-time-stats/cdn-status-codes.png)

<span data-ttu-id="6847f-133">El gráfico **Códigos de estado** indica con qué frecuencia se producen ciertos códigos de respuesta HTTP durante el intervalo de tiempo especificado.</span><span class="sxs-lookup"><span data-stu-id="6847f-133">The **Status Codes** graph indicates how often certain HTTP response codes are occurring over the selected time span.</span></span>

> [!TIP]
> <span data-ttu-id="6847f-134">Para obtener una descripción de cada opción de código de estado de HTTP, consulte [Azure CDN HTTP Status Codes](https://msdn.microsoft.com/library/mt759238.aspx)(Códigos de estado HTTP de la red CDN de Azure).</span><span class="sxs-lookup"><span data-stu-id="6847f-134">For a description of each HTTP status code option, see [Azure CDN HTTP Status Codes](https://msdn.microsoft.com/library/mt759238.aspx).</span></span>
> 
> 

<span data-ttu-id="6847f-135">Justo encima del gráfico se muestra una lista de códigos de estado HTTP.</span><span class="sxs-lookup"><span data-stu-id="6847f-135">A list of HTTP status codes is displayed directly above the graph.</span></span> <span data-ttu-id="6847f-136">En esta lista se indica cada código de estado que se puede incluir en el gráfico de líneas y el número actual de repeticiones por segundo para ese código de estado.</span><span class="sxs-lookup"><span data-stu-id="6847f-136">This list indicates each status code that can be included in the line graph and the current number of occurrences per second for that status code.</span></span> <span data-ttu-id="6847f-137">De forma predeterminada, se muestra una línea para cada uno de estos códigos de estado del gráfico.</span><span class="sxs-lookup"><span data-stu-id="6847f-137">By default, a line is displayed for each of these status codes in the graph.</span></span> <span data-ttu-id="6847f-138">Pero se puede optar por supervisar solo los códigos de estado que tienen un significado especial para la configuración de la red CDN.</span><span class="sxs-lookup"><span data-stu-id="6847f-138">However, you can choose to only monitor the status codes that have special significance for your CDN configuration.</span></span> <span data-ttu-id="6847f-139">Para ello, active los códigos de estado que desee, desactive todas las demás opciones y haga clic en **Actualizar gráfico**.</span><span class="sxs-lookup"><span data-stu-id="6847f-139">To do this, check the desired status codes and clear all other options, then click **Refresh Graph**.</span></span> 

<span data-ttu-id="6847f-140">También puede ocultar temporalmente los datos registrados para un determinado código de estado.</span><span class="sxs-lookup"><span data-stu-id="6847f-140">You can temporarily hide logged data for a particular status code.</span></span>  <span data-ttu-id="6847f-141">En la leyenda, directamente debajo del gráfico, haga clic en el código de estado que desee ocultar.</span><span class="sxs-lookup"><span data-stu-id="6847f-141">From the legend directly below the graph, click the status code you want to hide.</span></span> <span data-ttu-id="6847f-142">El código de estado se ocultará inmediatamente en el gráfico.</span><span class="sxs-lookup"><span data-stu-id="6847f-142">The status code will be immediately hidden from the graph.</span></span> <span data-ttu-id="6847f-143">Al volver a hacer clic en ese código de estado volverá a mostrarse esa opción.</span><span class="sxs-lookup"><span data-stu-id="6847f-143">Clicking that status code again will cause that option to be displayed again.</span></span>

## <a name="cache-statuses"></a><span data-ttu-id="6847f-144">Estados de la memoria caché</span><span class="sxs-lookup"><span data-stu-id="6847f-144">Cache Statuses</span></span>
![Gráfico Estado de caché](./media/cdn-real-time-stats/cdn-cache-status.png)

<span data-ttu-id="6847f-146">El gráfico **Estado de caché** indica con qué frecuencia se producen determinados tipos de estados de la memoria caché durante el intervalo de tiempo especificado.</span><span class="sxs-lookup"><span data-stu-id="6847f-146">The **Cache Statuses** graph indicates how often certain types of cache statuses are occurring over the selected time span.</span></span> 

> [!TIP]
> <span data-ttu-id="6847f-147">Para ver una descripción de cada opción de código de estado de caché, consulte [Azure CDN Cache Status Codes](https://msdn.microsoft.com/library/mt759237.aspx)(Códigos de estado de caché de la red CDN de Azure).</span><span class="sxs-lookup"><span data-stu-id="6847f-147">For a description of each cache status code option, see [Azure CDN Cache Status Codes](https://msdn.microsoft.com/library/mt759237.aspx).</span></span>
> 
> 

<span data-ttu-id="6847f-148">Justo encima del gráfico se muestra una lista de códigos de estado de la memoria caché.</span><span class="sxs-lookup"><span data-stu-id="6847f-148">A list of cache status codes is displayed directly above the graph.</span></span> <span data-ttu-id="6847f-149">En esta lista se indica cada código de estado que se puede incluir en el gráfico de líneas y el número actual de repeticiones por segundo para ese código de estado.</span><span class="sxs-lookup"><span data-stu-id="6847f-149">This list indicates each status code that can be included in the line graph and the current number of occurrences per second for that status code.</span></span> <span data-ttu-id="6847f-150">De forma predeterminada, se muestra una línea para cada uno de estos códigos de estado del gráfico.</span><span class="sxs-lookup"><span data-stu-id="6847f-150">By default, a line is displayed for each of these status codes in the graph.</span></span> <span data-ttu-id="6847f-151">Pero se puede optar por supervisar solo los códigos de estado que tienen un significado especial para la configuración de la red CDN.</span><span class="sxs-lookup"><span data-stu-id="6847f-151">However, you can choose to only monitor the status codes that have special significance for your CDN configuration.</span></span> <span data-ttu-id="6847f-152">Para ello, active los códigos de estado que desee, desactive todas las demás opciones y haga clic en **Actualizar gráfico**.</span><span class="sxs-lookup"><span data-stu-id="6847f-152">To do this, check the desired status codes and clear all other options, then click **Refresh Graph**.</span></span> 

<span data-ttu-id="6847f-153">También puede ocultar temporalmente los datos registrados para un determinado código de estado.</span><span class="sxs-lookup"><span data-stu-id="6847f-153">You can temporarily hide logged data for a particular status code.</span></span>  <span data-ttu-id="6847f-154">En la leyenda, directamente debajo del gráfico, haga clic en el código de estado que desee ocultar.</span><span class="sxs-lookup"><span data-stu-id="6847f-154">From the legend directly below the graph, click the status code you want to hide.</span></span> <span data-ttu-id="6847f-155">El código de estado se ocultará inmediatamente en el gráfico.</span><span class="sxs-lookup"><span data-stu-id="6847f-155">The status code will be immediately hidden from the graph.</span></span> <span data-ttu-id="6847f-156">Al volver a hacer clic en ese código de estado volverá a mostrarse esa opción.</span><span class="sxs-lookup"><span data-stu-id="6847f-156">Clicking that status code again will cause that option to be displayed again.</span></span>

## <a name="connections"></a><span data-ttu-id="6847f-157">Conexiones</span><span class="sxs-lookup"><span data-stu-id="6847f-157">Connections</span></span>
![Gráfico Conexiones](./media/cdn-real-time-stats/cdn-connections.png)

<span data-ttu-id="6847f-159">Este gráfico indica cuántas conexiones se han establecido para los servidores perimetrales.</span><span class="sxs-lookup"><span data-stu-id="6847f-159">This graph indicates how many connections have been established to your edge servers.</span></span> <span data-ttu-id="6847f-160">Cada solicitud de un recurso que pasa por la red CDN genera una conexión.</span><span class="sxs-lookup"><span data-stu-id="6847f-160">Each request for an asset that passes through our CDN results in a connection.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6847f-161">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6847f-161">Next Steps</span></span>
* <span data-ttu-id="6847f-162">Recibir notificaciones con [alertas en tiempo real en la CDN de Azure](cdn-real-time-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="6847f-162">Get notified with [Real-time alerts in Azure CDN](cdn-real-time-alerts.md)</span></span>
* <span data-ttu-id="6847f-163">Profundizar más con [informes de HTTP avanzados](cdn-advanced-http-reports.md)</span><span class="sxs-lookup"><span data-stu-id="6847f-163">Dig deeper with [advanced HTTP reports](cdn-advanced-http-reports.md)</span></span>
* <span data-ttu-id="6847f-164">Analizar [patrones de uso](cdn-analyze-usage-patterns.md)</span><span class="sxs-lookup"><span data-stu-id="6847f-164">Analyze [usage patterns](cdn-analyze-usage-patterns.md)</span></span>

