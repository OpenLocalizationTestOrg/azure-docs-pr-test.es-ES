---
title: "estadísticas de tiempo de aaaReal en la red CDN de Azure | Documentos de Microsoft"
description: "Estadísticas en tiempo real proporciona datos en tiempo real sobre el rendimiento de hello red CDN de Azure para entregar el contenido de los clientes de tooyour contenido."
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
ms.openlocfilehash: 68900a5092b767e45c1fdf9cef2cd03f55f38a6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="real-time-stats-in-microsoft-azure-cdn"></a><span data-ttu-id="adbf1-103">Estadísticas en tiempo real en la CDN de Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="adbf1-103">Real-time stats in Microsoft Azure CDN</span></span>
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a><span data-ttu-id="adbf1-104">Información general</span><span class="sxs-lookup"><span data-stu-id="adbf1-104">Overview</span></span>
<span data-ttu-id="adbf1-105">En este documento se describe la funcionalidad de Estadísticas en tiempo real en la CDN de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="adbf1-105">This document explains real-time stats in Microsoft Azure CDN.</span></span>  <span data-ttu-id="adbf1-106">Esta funcionalidad proporciona datos en tiempo real, como perfil de ancho de banda, Estados de memoria caché y conexiones simultáneas tooyour CDN para entregar el contenido de los clientes de tooyour contenido.</span><span class="sxs-lookup"><span data-stu-id="adbf1-106">This functionality provides real-time data, such as bandwidth, cache statuses, and concurrent connections tooyour CDN profile when delivering content tooyour clients.</span></span> <span data-ttu-id="adbf1-107">Esto permite la supervisión continua del estado de Hola de su servicio en cualquier momento, incluidos los eventos de puesta en marcha.</span><span class="sxs-lookup"><span data-stu-id="adbf1-107">This enables continuous monitoring of hello health of your service at any time, including go-live events.</span></span>

<span data-ttu-id="adbf1-108">Hola siguiendo los gráficos está disponible:</span><span class="sxs-lookup"><span data-stu-id="adbf1-108">hello following graphs are available:</span></span>

* [<span data-ttu-id="adbf1-109">Ancho de banda</span><span class="sxs-lookup"><span data-stu-id="adbf1-109">Bandwidth</span></span>](#bandwidth)
* [<span data-ttu-id="adbf1-110">Códigos de estado</span><span class="sxs-lookup"><span data-stu-id="adbf1-110">Status Codes</span></span>](#status-codes)
* [<span data-ttu-id="adbf1-111">Estados de la memoria caché</span><span class="sxs-lookup"><span data-stu-id="adbf1-111">Cache Statuses</span></span>](#cache-statuses)
* [<span data-ttu-id="adbf1-112">Conexiones</span><span class="sxs-lookup"><span data-stu-id="adbf1-112">Connections</span></span>](#connections)

## <a name="accessing-real-time-stats"></a><span data-ttu-id="adbf1-113">Acceso a estadísticas en tiempo real</span><span class="sxs-lookup"><span data-stu-id="adbf1-113">Accessing real-time stats</span></span>
1. <span data-ttu-id="adbf1-114">Hola [Portal de Azure](https://portal.azure.com), examinar el perfil de CDN tooyour.</span><span class="sxs-lookup"><span data-stu-id="adbf1-114">In hello [Azure Portal](https://portal.azure.com), browse tooyour CDN profile.</span></span>
   
    ![Hoja del perfil de red CDN](./media/cdn-real-time-stats/cdn-profile-blade.png)
2. <span data-ttu-id="adbf1-116">En la hoja de perfil CDN Hola, haga clic en hello **administrar** botón.</span><span class="sxs-lookup"><span data-stu-id="adbf1-116">From hello CDN profile blade, click hello **Manage** button.</span></span>
   
    ![Botón de administración de hoja de perfil de red CDN](./media/cdn-real-time-stats/cdn-manage-btn.png)
   
    <span data-ttu-id="adbf1-118">se abre el portal de administración de red CDN Hola.</span><span class="sxs-lookup"><span data-stu-id="adbf1-118">hello CDN management portal opens.</span></span>
3. <span data-ttu-id="adbf1-119">Mantenga el mouse sobre hello **análisis** ficha y, a continuación, mantenga el mouse sobre hello **estadísticas en tiempo real** ventana flotante.</span><span class="sxs-lookup"><span data-stu-id="adbf1-119">Hover over hello **Analytics** tab, then hover over hello **Real-Time Stats** flyout.</span></span>  <span data-ttu-id="adbf1-120">Haga clic en **Objeto grande HTTP**.</span><span class="sxs-lookup"><span data-stu-id="adbf1-120">Click on **HTTP Large Object**.</span></span>
   
    ![Portal de administración de la red CDN](./media/cdn-real-time-stats/cdn-premium-portal.png)
   
    <span data-ttu-id="adbf1-122">se muestran gráficos de estadísticas en tiempo real de Hola.</span><span class="sxs-lookup"><span data-stu-id="adbf1-122">hello real-time stats graphs are displayed.</span></span>

<span data-ttu-id="adbf1-123">Cada uno de los gráficos de hello muestra estadísticas en tiempo real para intervalo de tiempo de hello seleccionado, se inicien cuando se carga la página de Hola.</span><span class="sxs-lookup"><span data-stu-id="adbf1-123">Each of hello graphs displays real-time statistics for hello selected time span, starting when hello page loads.</span></span>  <span data-ttu-id="adbf1-124">gráficos de Hola se actualizan automáticamente cada pocos segundos.</span><span class="sxs-lookup"><span data-stu-id="adbf1-124">hello graphs update automatically every few seconds.</span></span>  <span data-ttu-id="adbf1-125">Hola **Actualizar gráfico** botón, si está presente, borrará gráfico hello, tras el cual solo mostrará datos saludo seleccionado.</span><span class="sxs-lookup"><span data-stu-id="adbf1-125">hello **Refresh Graph** button, if present, will clear hello graph, after which it will only display hello selected data.</span></span>

## <a name="bandwidth"></a><span data-ttu-id="adbf1-126">Ancho de banda</span><span class="sxs-lookup"><span data-stu-id="adbf1-126">Bandwidth</span></span>
![Gráfico Ancho de banda](./media/cdn-real-time-stats/cdn-bandwidth.png)

<span data-ttu-id="adbf1-128">Hola **ancho de banda** gráfico muestra la cantidad de Hola de ancho de banda utilizado para la plataforma actual de hello en el intervalo de tiempo de hello seleccionado.</span><span class="sxs-lookup"><span data-stu-id="adbf1-128">hello **Bandwidth** graph displays hello amount of bandwidth used for hello current platform over hello selected time span.</span></span> <span data-ttu-id="adbf1-129">parte sombreado de Hola de gráfico de hello indica el uso de ancho de banda.</span><span class="sxs-lookup"><span data-stu-id="adbf1-129">hello shaded portion of hello graph indicates bandwidth usage.</span></span> <span data-ttu-id="adbf1-130">cantidad exacta de Hola de ancho de banda que se está usando actualmente se muestra directamente por debajo del gráfico de líneas de Hola.</span><span class="sxs-lookup"><span data-stu-id="adbf1-130">hello exact amount of bandwidth currently being used is displayed directly below hello line graph.</span></span>

## <a name="status-codes"></a><span data-ttu-id="adbf1-131">Códigos de estado</span><span class="sxs-lookup"><span data-stu-id="adbf1-131">Status Codes</span></span>
![Gráfico Código de estado](./media/cdn-real-time-stats/cdn-status-codes.png)

<span data-ttu-id="adbf1-133">Hola **códigos de estado** gráfico indica con qué frecuencia se producen ciertos códigos de respuesta HTTP a través intervalo de tiempo de hello seleccionado.</span><span class="sxs-lookup"><span data-stu-id="adbf1-133">hello **Status Codes** graph indicates how often certain HTTP response codes are occurring over hello selected time span.</span></span>

> [!TIP]
> <span data-ttu-id="adbf1-134">Para obtener una descripción de cada opción de código de estado de HTTP, consulte [Azure CDN HTTP Status Codes](https://msdn.microsoft.com/library/mt759238.aspx)(Códigos de estado HTTP de la red CDN de Azure).</span><span class="sxs-lookup"><span data-stu-id="adbf1-134">For a description of each HTTP status code option, see [Azure CDN HTTP Status Codes](https://msdn.microsoft.com/library/mt759238.aspx).</span></span>
> 
> 

<span data-ttu-id="adbf1-135">Se muestra una lista de códigos de estado HTTP directamente sobre el gráfico de Hola.</span><span class="sxs-lookup"><span data-stu-id="adbf1-135">A list of HTTP status codes is displayed directly above hello graph.</span></span> <span data-ttu-id="adbf1-136">Esta lista indica cada código de estado que puede incluirse en el gráfico de líneas de Hola y el número actual de Hola de repeticiones por segundo para ese código de estado.</span><span class="sxs-lookup"><span data-stu-id="adbf1-136">This list indicates each status code that can be included in hello line graph and hello current number of occurrences per second for that status code.</span></span> <span data-ttu-id="adbf1-137">De forma predeterminada, se muestra una línea para cada uno de estos códigos de estado en el gráfico de Hola.</span><span class="sxs-lookup"><span data-stu-id="adbf1-137">By default, a line is displayed for each of these status codes in hello graph.</span></span> <span data-ttu-id="adbf1-138">Sin embargo, puede elegir tooonly códigos de estado de monitor Hola que tienen un significado especial para la configuración de red CDN.</span><span class="sxs-lookup"><span data-stu-id="adbf1-138">However, you can choose tooonly monitor hello status codes that have special significance for your CDN configuration.</span></span> <span data-ttu-id="adbf1-139">toodo, comprobar los códigos de estado deseado de Hola y desactive todas las demás opciones, haga clic en **Actualizar gráfico**.</span><span class="sxs-lookup"><span data-stu-id="adbf1-139">toodo this, check hello desired status codes and clear all other options, then click **Refresh Graph**.</span></span> 

<span data-ttu-id="adbf1-140">También puede ocultar temporalmente los datos registrados para un determinado código de estado.</span><span class="sxs-lookup"><span data-stu-id="adbf1-140">You can temporarily hide logged data for a particular status code.</span></span>  <span data-ttu-id="adbf1-141">En leyenda de hello directamente por debajo del gráfico de hello, haga clic en código de estado de Hola que quiere toohide.</span><span class="sxs-lookup"><span data-stu-id="adbf1-141">From hello legend directly below hello graph, click hello status code you want toohide.</span></span> <span data-ttu-id="adbf1-142">código de estado de Hola se ocultará en gráfico de hello inmediatamente.</span><span class="sxs-lookup"><span data-stu-id="adbf1-142">hello status code will be immediately hidden from hello graph.</span></span> <span data-ttu-id="adbf1-143">Haga clic de nuevo en ese código de estado provocará que toobe opción volverá a aparecer.</span><span class="sxs-lookup"><span data-stu-id="adbf1-143">Clicking that status code again will cause that option toobe displayed again.</span></span>

## <a name="cache-statuses"></a><span data-ttu-id="adbf1-144">Estados de la memoria caché</span><span class="sxs-lookup"><span data-stu-id="adbf1-144">Cache Statuses</span></span>
![Gráfico Estado de caché](./media/cdn-real-time-stats/cdn-cache-status.png)

<span data-ttu-id="adbf1-146">Hola **Estados de memoria caché** gráfico indica con qué frecuencia se producen ciertos tipos de Estados de la memoria caché a través intervalo de tiempo de hello seleccionado.</span><span class="sxs-lookup"><span data-stu-id="adbf1-146">hello **Cache Statuses** graph indicates how often certain types of cache statuses are occurring over hello selected time span.</span></span> 

> [!TIP]
> <span data-ttu-id="adbf1-147">Para ver una descripción de cada opción de código de estado de caché, consulte [Azure CDN Cache Status Codes](https://msdn.microsoft.com/library/mt759237.aspx)(Códigos de estado de caché de la red CDN de Azure).</span><span class="sxs-lookup"><span data-stu-id="adbf1-147">For a description of each cache status code option, see [Azure CDN Cache Status Codes](https://msdn.microsoft.com/library/mt759237.aspx).</span></span>
> 
> 

<span data-ttu-id="adbf1-148">Se muestra una lista de códigos de estado de la memoria caché directamente sobre el gráfico de Hola.</span><span class="sxs-lookup"><span data-stu-id="adbf1-148">A list of cache status codes is displayed directly above hello graph.</span></span> <span data-ttu-id="adbf1-149">Esta lista indica cada código de estado que puede incluirse en el gráfico de líneas de Hola y el número actual de Hola de repeticiones por segundo para ese código de estado.</span><span class="sxs-lookup"><span data-stu-id="adbf1-149">This list indicates each status code that can be included in hello line graph and hello current number of occurrences per second for that status code.</span></span> <span data-ttu-id="adbf1-150">De forma predeterminada, se muestra una línea para cada uno de estos códigos de estado en el gráfico de Hola.</span><span class="sxs-lookup"><span data-stu-id="adbf1-150">By default, a line is displayed for each of these status codes in hello graph.</span></span> <span data-ttu-id="adbf1-151">Sin embargo, puede elegir tooonly códigos de estado de monitor Hola que tienen un significado especial para la configuración de red CDN.</span><span class="sxs-lookup"><span data-stu-id="adbf1-151">However, you can choose tooonly monitor hello status codes that have special significance for your CDN configuration.</span></span> <span data-ttu-id="adbf1-152">toodo, comprobar los códigos de estado deseado de Hola y desactive todas las demás opciones, haga clic en **Actualizar gráfico**.</span><span class="sxs-lookup"><span data-stu-id="adbf1-152">toodo this, check hello desired status codes and clear all other options, then click **Refresh Graph**.</span></span> 

<span data-ttu-id="adbf1-153">También puede ocultar temporalmente los datos registrados para un determinado código de estado.</span><span class="sxs-lookup"><span data-stu-id="adbf1-153">You can temporarily hide logged data for a particular status code.</span></span>  <span data-ttu-id="adbf1-154">En leyenda de hello directamente por debajo del gráfico de hello, haga clic en código de estado de Hola que quiere toohide.</span><span class="sxs-lookup"><span data-stu-id="adbf1-154">From hello legend directly below hello graph, click hello status code you want toohide.</span></span> <span data-ttu-id="adbf1-155">código de estado de Hola se ocultará en gráfico de hello inmediatamente.</span><span class="sxs-lookup"><span data-stu-id="adbf1-155">hello status code will be immediately hidden from hello graph.</span></span> <span data-ttu-id="adbf1-156">Haga clic de nuevo en ese código de estado provocará que toobe opción volverá a aparecer.</span><span class="sxs-lookup"><span data-stu-id="adbf1-156">Clicking that status code again will cause that option toobe displayed again.</span></span>

## <a name="connections"></a><span data-ttu-id="adbf1-157">Conexiones</span><span class="sxs-lookup"><span data-stu-id="adbf1-157">Connections</span></span>
![Gráfico Conexiones](./media/cdn-real-time-stats/cdn-connections.png)

<span data-ttu-id="adbf1-159">Este gráfico indica el número de conexiones se han establecido tooyour borde servidores.</span><span class="sxs-lookup"><span data-stu-id="adbf1-159">This graph indicates how many connections have been established tooyour edge servers.</span></span> <span data-ttu-id="adbf1-160">Cada solicitud de un recurso que pasa por la red CDN genera una conexión.</span><span class="sxs-lookup"><span data-stu-id="adbf1-160">Each request for an asset that passes through our CDN results in a connection.</span></span>

## <a name="next-steps"></a><span data-ttu-id="adbf1-161">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="adbf1-161">Next Steps</span></span>
* <span data-ttu-id="adbf1-162">Recibir notificaciones con [alertas en tiempo real en la CDN de Azure](cdn-real-time-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="adbf1-162">Get notified with [Real-time alerts in Azure CDN](cdn-real-time-alerts.md)</span></span>
* <span data-ttu-id="adbf1-163">Profundizar más con [informes de HTTP avanzados](cdn-advanced-http-reports.md)</span><span class="sxs-lookup"><span data-stu-id="adbf1-163">Dig deeper with [advanced HTTP reports](cdn-advanced-http-reports.md)</span></span>
* <span data-ttu-id="adbf1-164">Analizar [patrones de uso](cdn-analyze-usage-patterns.md)</span><span class="sxs-lookup"><span data-stu-id="adbf1-164">Analyze [usage patterns](cdn-analyze-usage-patterns.md)</span></span>

