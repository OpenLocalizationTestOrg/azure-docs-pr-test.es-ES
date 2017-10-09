---
title: un panel personalizado en Azure Log Analytics aaaCreate | Documentos de Microsoft
description: "Esta guía le ayudará a comprender cómo los paneles de análisis de registros pueden mostrar todas las búsquedas de registros guardadas, lo que proporciona una sola lente tooview su entorno."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: abb07f6c-b356-4f15-85f5-60e4415d0ba2
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: magoedte
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 73fcf131a91c743d473f37d5a40d52eaf78a7ba3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-dashboard-for-use-in-log-analytics"></a><span data-ttu-id="7dec6-103">Creación de un panel personalizado para usarse en Log Analytics</span><span class="sxs-lookup"><span data-stu-id="7dec6-103">Create a custom dashboard for use in Log Analytics</span></span>

>[!NOTE]
> <span data-ttu-id="7dec6-104">Si el área de trabajo se ha actualizado toohello [lenguaje de consulta de análisis de registros nueva](log-analytics-log-search-upgrade.md), a continuación, no puede crear nuevos paneles o editar otros paneles.</span><span class="sxs-lookup"><span data-stu-id="7dec6-104">If your workspace has been upgraded toohello [new Log Analytics query language](log-analytics-log-search-upgrade.md), then you cannot create new dashboards or edit existing dashboards.</span></span> 

<span data-ttu-id="7dec6-105">Esta guía le ayudará a comprender cómo los paneles de análisis de registros pueden mostrar todas las búsquedas de registros guardadas, lo que proporciona una sola lente tooview su entorno.</span><span class="sxs-lookup"><span data-stu-id="7dec6-105">This guide helps you understand how Log Analytics dashboards can visualize all of your saved log searches, giving you a single lens tooview your environment.</span></span>

![Panel de ejemplo](./media/log-analytics-dashboards/oms-dashboards-example-dash.png)

<span data-ttu-id="7dec6-107">Todos los paneles personalizados Hola que cree en el portal de OMS hello también están disponibles en hello aplicación móvil de OMS.</span><span class="sxs-lookup"><span data-stu-id="7dec6-107">All hello custom dashboards that you create in hello OMS portal are also available in hello OMS Mobile App.</span></span> <span data-ttu-id="7dec6-108">Vea Hola después de páginas para obtener más información acerca de las aplicaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="7dec6-108">See hello following pages for more information about hello apps.</span></span>

* [<span data-ttu-id="7dec6-109">Aplicación móvil de OMS de hello Microsoft Store</span><span class="sxs-lookup"><span data-stu-id="7dec6-109">OMS mobile app from hello Microsoft Store</span></span>](http://www.windowsphone.com/store/app/operational-insights/4823b935-83ce-466c-82bb-bd0a3f58d865)
* [<span data-ttu-id="7dec6-110">Aplicación móvil de OMS en Apple iTunes</span><span class="sxs-lookup"><span data-stu-id="7dec6-110">OMS mobile app from Apple iTunes</span></span>](https://itunes.apple.com/app/microsoft-operations-management/id1042424859?mt=8)

![mobile dashboard](./media/log-analytics-dashboards/oms-search-mobile.png)

## <a name="how-do-i-create-my-dashboard"></a><span data-ttu-id="7dec6-112">¿Cómo creo mi panel?</span><span class="sxs-lookup"><span data-stu-id="7dec6-112">How do I create my dashboard?</span></span>
<span data-ttu-id="7dec6-113">toobegin, página de información general de OMS toohello vaya.</span><span class="sxs-lookup"><span data-stu-id="7dec6-113">toobegin, go toohello OMS Overview page.</span></span> <span data-ttu-id="7dec6-114">Verá hello **Mi panel** icono de hello izquierda.</span><span class="sxs-lookup"><span data-stu-id="7dec6-114">You'll see hello **My Dashboard** tile on hello left.</span></span> <span data-ttu-id="7dec6-115">Haga clic en él toodrill hacia abajo en el panel.</span><span class="sxs-lookup"><span data-stu-id="7dec6-115">Click it toodrill down into your dashboard.</span></span>

![Información general](./media/log-analytics-dashboards/oms-dashboards-overview.png)

## <a name="adding-a-tile"></a><span data-ttu-id="7dec6-117">Adición de un mosaico</span><span class="sxs-lookup"><span data-stu-id="7dec6-117">Adding a tile</span></span>
<span data-ttu-id="7dec6-118">En los paneles, los mosaicos se generan a partir de las búsquedas de registros guardadas.</span><span class="sxs-lookup"><span data-stu-id="7dec6-118">In dashboards, tiles are powered by your saved log searches.</span></span> <span data-ttu-id="7dec6-119">OMS incluye muchas búsquedas de registros guardadas de creación previa, para que pueda empezar inmediatamente.</span><span class="sxs-lookup"><span data-stu-id="7dec6-119">OMS comes with many pre-made saved log searches, so you can begin right away.</span></span> <span data-ttu-id="7dec6-120">Pasos siguientes de Hola de utilizar dicho esquema cómo toobegin.</span><span class="sxs-lookup"><span data-stu-id="7dec6-120">Use hello following steps that outline how toobegin.</span></span>

<span data-ttu-id="7dec6-121">Hola vista Mi panel, simplemente haga clic en **personalizar** tooenter en el modo personalizar.</span><span class="sxs-lookup"><span data-stu-id="7dec6-121">In hello My Dashboard view, simply click **Customize** tooenter customize mode.</span></span>

![Gráfica](./media/log-analytics-dashboards/oms-dashboards-pictorial01.png)

 <span data-ttu-id="7dec6-123">panel de Hola que se abre en el lado derecho de Hola de página de Hola muestran todas las búsquedas de registros guardadas del área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="7dec6-123">hello panel that opens on hello right side of hello page shows all of your workspace's saved log searches.</span></span> <span data-ttu-id="7dec6-124">toovisualize buscar un registro guardado como un icono, mantenga el mouse sobre una búsqueda guardada y, a continuación, haga clic en hello **más** símbolos.</span><span class="sxs-lookup"><span data-stu-id="7dec6-124">toovisualize a saved log search as a tile,  hover over a saved search and then click hello **plus** symbol.</span></span>

![Agregar mosaicos 1](./media/log-analytics-dashboards/oms-dashboards-pictorial02.png)

<span data-ttu-id="7dec6-126">Al hacer clic en hello **más** de símbolos, aparece un icono nuevo en hello vista Mi panel.</span><span class="sxs-lookup"><span data-stu-id="7dec6-126">When you click hello **plus** symbol, a new tile appears in hello My Dashboard view.</span></span>

![Agregar mosaicos 2](./media/log-analytics-dashboards/oms-dashboards-pictorial03.png)

## <a name="edit-a-tile"></a><span data-ttu-id="7dec6-128">Editar un mosaico</span><span class="sxs-lookup"><span data-stu-id="7dec6-128">Edit a tile</span></span>
<span data-ttu-id="7dec6-129">Hola vista Mi panel, simplemente haga clic en **personalizar** tooenter en el modo personalizar.</span><span class="sxs-lookup"><span data-stu-id="7dec6-129">In hello My Dashboard view, simply click  **Customize** tooenter customize mode.</span></span> <span data-ttu-id="7dec6-130">Haga clic en el icono de hello desea tooedit.</span><span class="sxs-lookup"><span data-stu-id="7dec6-130">Click hello tile you want tooedit.</span></span> <span data-ttu-id="7dec6-131">el panel derecho Hola cambia tooedit y ofrece una selección de opciones:</span><span class="sxs-lookup"><span data-stu-id="7dec6-131">hello right panel changes tooedit, and gives a selection of options:</span></span>

![Editar mosaico](./media/log-analytics-dashboards/oms-dashboards-pictorial04.png)

![Editar mosaico](./media/log-analytics-dashboards/oms-dashboards-pictorial05.png)

### <a name="tile-visualizations"></a><span data-ttu-id="7dec6-134">Visualizaciones de mosaico</span><span class="sxs-lookup"><span data-stu-id="7dec6-134">Tile visualizations</span></span>
<span data-ttu-id="7dec6-135">Hay tres tipos de toochoose de visualizaciones de mosaico desde:</span><span class="sxs-lookup"><span data-stu-id="7dec6-135">There are three kinds of tile visualizations toochoose from:</span></span>

| <span data-ttu-id="7dec6-136">tipo de gráfico</span><span class="sxs-lookup"><span data-stu-id="7dec6-136">chart type</span></span> | <span data-ttu-id="7dec6-137">qué hace</span><span class="sxs-lookup"><span data-stu-id="7dec6-137">what it does</span></span> |
| --- | --- |
| ![Gráfico de barras](./media/log-analytics-dashboards/oms-dashboards-bar-chart.png) |<span data-ttu-id="7dec6-139">Muestra una escala de tiempo de los resultados de búsquedas de registros guardadas como un gráfico de barras, o una lista de resultados por un campo en función de si la búsqueda de registros agrega los resultados por un campo o no.</span><span class="sxs-lookup"><span data-stu-id="7dec6-139">Displays a timeline of your saved log search's results as a bar chart, or a list of results by a field depending on if your log search aggregates results by a field or not.</span></span> |
| ![métrica](./media/log-analytics-dashboards/oms-dashboards-metric.png) |<span data-ttu-id="7dec6-141">Muestra el número total de resultados de la búsqueda de registros como número en un icono.</span><span class="sxs-lookup"><span data-stu-id="7dec6-141">Displays your total log search result hits as a number in a tile.</span></span> <span data-ttu-id="7dec6-142">Mosaicos de métrica permiten tooset un umbral que hará resaltar el mosaico de hello cuando se alcanza el umbral de Hola.</span><span class="sxs-lookup"><span data-stu-id="7dec6-142">Metric tiles allow you tooset a threshold that will highlight hello tile when hello threshold is reached.</span></span> |
| ![line](./media/log-analytics-dashboards/oms-dashboards-line.png) |<span data-ttu-id="7dec6-144">Muestra una escala de tiempo de los resultados de búsquedas de registros guardadas con los valores en forma de gráfico de líneas.</span><span class="sxs-lookup"><span data-stu-id="7dec6-144">Displays a timeline of your saved log search result hits with values as a line chart.</span></span> |

### <a name="threshold"></a><span data-ttu-id="7dec6-145">Umbral</span><span class="sxs-lookup"><span data-stu-id="7dec6-145">Threshold</span></span>
<span data-ttu-id="7dec6-146">Puede crear un umbral en un mosaico mediante la visualización métrica Hola.</span><span class="sxs-lookup"><span data-stu-id="7dec6-146">You can create a threshold on a tile using hello Metric visualization.</span></span> <span data-ttu-id="7dec6-147">Seleccione en toocreate un valor de umbral en el icono de Hola.</span><span class="sxs-lookup"><span data-stu-id="7dec6-147">Select on toocreate a threshold value on hello tile.</span></span> <span data-ttu-id="7dec6-148">Elija si mosaico de hello toohighlight al valor de hello está por encima o debajo del umbral de hello elegido, a continuación, establezca el valor por debajo del umbral de Hola.</span><span class="sxs-lookup"><span data-stu-id="7dec6-148">Choose whether toohighlight hello tile when hello value is over or under hello chosen threshold, then set hello threshold value below.</span></span>

## <a name="organizing-hello-dashboard"></a><span data-ttu-id="7dec6-149">Organización Hola panel</span><span class="sxs-lookup"><span data-stu-id="7dec6-149">Organizing hello dashboard</span></span>
<span data-ttu-id="7dec6-150">tooorganize el panel, navegue a vista de toohello Mi panel y haga clic en **personalizar** tooenter en el modo personalizar.</span><span class="sxs-lookup"><span data-stu-id="7dec6-150">tooorganize your dashboard, navigate toohello My Dashboard view and click **Customize** tooenter customize mode.</span></span> <span data-ttu-id="7dec6-151">Haga clic y arrastre el icono de Hola que desee toomove y muévalo toowhere desea que su toobe de mosaico.</span><span class="sxs-lookup"><span data-stu-id="7dec6-151">Click and drag hello tile you want toomove, and move it toowhere you want your tile toobe.</span></span>

![Organizar el panel](./media/log-analytics-dashboards/oms-dashboards-organize.png)

## <a name="remove-a-tile"></a><span data-ttu-id="7dec6-153">Quitar un mosaico</span><span class="sxs-lookup"><span data-stu-id="7dec6-153">Remove a tile</span></span>
<span data-ttu-id="7dec6-154">tooremove un icono, navegue a vista de toohello Mi panel y haga clic en **personalizar** tooenter en el modo personalizar.</span><span class="sxs-lookup"><span data-stu-id="7dec6-154">tooremove a tile, navigate toohello My Dashboard view and click **Customize** tooenter customize mode.</span></span> <span data-ttu-id="7dec6-155">Icono de hello SELECT que desee tooremove, y después en el panel derecho Hola seleccione **Quitar icono**.</span><span class="sxs-lookup"><span data-stu-id="7dec6-155">Select hello tile you want tooremove, then on hello right panel select **Remove Tile**.</span></span>

![Quitar un mosaico](./media/log-analytics-dashboards/oms-dashboards-remove-tile.png)

## <a name="next-steps"></a><span data-ttu-id="7dec6-157">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7dec6-157">Next steps</span></span>
* <span data-ttu-id="7dec6-158">Crear [alertas](log-analytics-alerts.md) en las notificaciones de toogenerate de análisis de registros y tooremediate problemas.</span><span class="sxs-lookup"><span data-stu-id="7dec6-158">Create [alerts](log-analytics-alerts.md) in Log Analytics toogenerate notifications and tooremediate problems.</span></span>
