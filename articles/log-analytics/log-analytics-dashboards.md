---
title: "Creación de un panel personalizado en Azure Log Analytics | Microsoft Docs"
description: "Con esta guía le resultará más fácil comprender cómo los paneles de Log Analytics pueden mostrar todas las búsquedas de registros guardadas, lo que le permite ver su entorno en una sola vista."
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
ms.openlocfilehash: a90d9c620221bffbb225fb060b997af2f5e90390
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-custom-dashboard-for-use-in-log-analytics"></a><span data-ttu-id="986e8-103">Creación de un panel personalizado para usarse en Log Analytics</span><span class="sxs-lookup"><span data-stu-id="986e8-103">Create a custom dashboard for use in Log Analytics</span></span>

>[!NOTE]
> <span data-ttu-id="986e8-104">Si el área de trabajo se ha actualizado al [nuevo lenguaje de consulta de Log Analytics](log-analytics-log-search-upgrade.md), no podrá crear nuevos paneles ni editar los ya existentes.</span><span class="sxs-lookup"><span data-stu-id="986e8-104">If your workspace has been upgraded to the [new Log Analytics query language](log-analytics-log-search-upgrade.md), then you cannot create new dashboards or edit existing dashboards.</span></span> 

<span data-ttu-id="986e8-105">Con esta guía le resultará más fácil comprender cómo los paneles de Log Analytics pueden mostrar todas las búsquedas de registros guardadas, lo que le permite ver su entorno en una sola vista.</span><span class="sxs-lookup"><span data-stu-id="986e8-105">This guide helps you understand how Log Analytics dashboards can visualize all of your saved log searches, giving you a single lens to view your environment.</span></span>

![Panel de ejemplo](./media/log-analytics-dashboards/oms-dashboards-example-dash.png)

<span data-ttu-id="986e8-107">Todos los paneles personalizados que cree en el portal de OMS también están disponibles en la aplicación móvil de OMS.</span><span class="sxs-lookup"><span data-stu-id="986e8-107">All the custom dashboards that you create in the OMS portal are also available in the OMS Mobile App.</span></span> <span data-ttu-id="986e8-108">Para más información acerca de las aplicaciones, consulte las páginas siguientes.</span><span class="sxs-lookup"><span data-stu-id="986e8-108">See the following pages for more information about the apps.</span></span>

* [<span data-ttu-id="986e8-109">Aplicación móvil de OMS en Microsoft Store</span><span class="sxs-lookup"><span data-stu-id="986e8-109">OMS mobile app from the Microsoft Store</span></span>](http://www.windowsphone.com/store/app/operational-insights/4823b935-83ce-466c-82bb-bd0a3f58d865)
* [<span data-ttu-id="986e8-110">Aplicación móvil de OMS en Apple iTunes</span><span class="sxs-lookup"><span data-stu-id="986e8-110">OMS mobile app from Apple iTunes</span></span>](https://itunes.apple.com/app/microsoft-operations-management/id1042424859?mt=8)

![mobile dashboard](./media/log-analytics-dashboards/oms-search-mobile.png)

## <a name="how-do-i-create-my-dashboard"></a><span data-ttu-id="986e8-112">¿Cómo creo mi panel?</span><span class="sxs-lookup"><span data-stu-id="986e8-112">How do I create my dashboard?</span></span>
<span data-ttu-id="986e8-113">Para empezar, vaya a la página de información general de OMS.</span><span class="sxs-lookup"><span data-stu-id="986e8-113">To begin, go to the OMS Overview page.</span></span> <span data-ttu-id="986e8-114">Verá el icono **Mi panel** a la izquierda.</span><span class="sxs-lookup"><span data-stu-id="986e8-114">You'll see the **My Dashboard** tile on the left.</span></span> <span data-ttu-id="986e8-115">Haga clic en él para explorar en profundidad el panel.</span><span class="sxs-lookup"><span data-stu-id="986e8-115">Click it to drill down into your dashboard.</span></span>

![Información general](./media/log-analytics-dashboards/oms-dashboards-overview.png)

## <a name="adding-a-tile"></a><span data-ttu-id="986e8-117">Adición de un mosaico</span><span class="sxs-lookup"><span data-stu-id="986e8-117">Adding a tile</span></span>
<span data-ttu-id="986e8-118">En los paneles, los mosaicos se generan a partir de las búsquedas de registros guardadas.</span><span class="sxs-lookup"><span data-stu-id="986e8-118">In dashboards, tiles are powered by your saved log searches.</span></span> <span data-ttu-id="986e8-119">OMS incluye muchas búsquedas de registros guardadas de creación previa, para que pueda empezar inmediatamente.</span><span class="sxs-lookup"><span data-stu-id="986e8-119">OMS comes with many pre-made saved log searches, so you can begin right away.</span></span> <span data-ttu-id="986e8-120">Los siguientes pasos describen cómo empezar.</span><span class="sxs-lookup"><span data-stu-id="986e8-120">Use the following steps that outline how to begin.</span></span>

<span data-ttu-id="986e8-121">En la vista Mi panel, haga clic en **Personalizar** para especificar el modo de personalización.</span><span class="sxs-lookup"><span data-stu-id="986e8-121">In the My Dashboard view, simply click **Customize** to enter customize mode.</span></span>

![Gráfica](./media/log-analytics-dashboards/oms-dashboards-pictorial01.png)

 <span data-ttu-id="986e8-123">En el panel que se abre a la derecha de la página se muestran todas las búsquedas de registros guardadas del área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="986e8-123">The panel that opens on the right side of the page shows all of your workspace's saved log searches.</span></span> <span data-ttu-id="986e8-124">Para visualizar una búsqueda de registro guardada como un icono, mantenga el mouse sobre una búsqueda guardada y haga clic en el signo **más**.</span><span class="sxs-lookup"><span data-stu-id="986e8-124">To visualize a saved log search as a tile,  hover over a saved search and then click the **plus** symbol.</span></span>

![Agregar mosaicos 1](./media/log-analytics-dashboards/oms-dashboards-pictorial02.png)

<span data-ttu-id="986e8-126">Al hacer clic en el signo **más**, aparece un icono nuevo en la vista Mi panel.</span><span class="sxs-lookup"><span data-stu-id="986e8-126">When you click the **plus** symbol, a new tile appears in the My Dashboard view.</span></span>

![Agregar mosaicos 2](./media/log-analytics-dashboards/oms-dashboards-pictorial03.png)

## <a name="edit-a-tile"></a><span data-ttu-id="986e8-128">Editar un mosaico</span><span class="sxs-lookup"><span data-stu-id="986e8-128">Edit a tile</span></span>
<span data-ttu-id="986e8-129">En la vista Mi panel, haga clic en **Personalizar** para especificar el modo de personalización.</span><span class="sxs-lookup"><span data-stu-id="986e8-129">In the My Dashboard view, simply click  **Customize** to enter customize mode.</span></span> <span data-ttu-id="986e8-130">Haga clic en el mosaico que quiere editar.</span><span class="sxs-lookup"><span data-stu-id="986e8-130">Click the tile you want to edit.</span></span> <span data-ttu-id="986e8-131">El panel derecho cambia a editar y ofrece diferentes opciones:</span><span class="sxs-lookup"><span data-stu-id="986e8-131">The right panel changes to edit, and gives a selection of options:</span></span>

![Editar mosaico](./media/log-analytics-dashboards/oms-dashboards-pictorial04.png)

![Editar mosaico](./media/log-analytics-dashboards/oms-dashboards-pictorial05.png)

### <a name="tile-visualizations"></a><span data-ttu-id="986e8-134">Visualizaciones de mosaico</span><span class="sxs-lookup"><span data-stu-id="986e8-134">Tile visualizations</span></span>
<span data-ttu-id="986e8-135">Existen tres tipos de visualizaciones de iconos que puede elegir:</span><span class="sxs-lookup"><span data-stu-id="986e8-135">There are three kinds of tile visualizations to choose from:</span></span>

| <span data-ttu-id="986e8-136">tipo de gráfico</span><span class="sxs-lookup"><span data-stu-id="986e8-136">chart type</span></span> | <span data-ttu-id="986e8-137">qué hace</span><span class="sxs-lookup"><span data-stu-id="986e8-137">what it does</span></span> |
| --- | --- |
| ![Gráfico de barras](./media/log-analytics-dashboards/oms-dashboards-bar-chart.png) |<span data-ttu-id="986e8-139">Muestra una escala de tiempo de los resultados de búsquedas de registros guardadas como un gráfico de barras, o una lista de resultados por un campo en función de si la búsqueda de registros agrega los resultados por un campo o no.</span><span class="sxs-lookup"><span data-stu-id="986e8-139">Displays a timeline of your saved log search's results as a bar chart, or a list of results by a field depending on if your log search aggregates results by a field or not.</span></span> |
| ![métrica](./media/log-analytics-dashboards/oms-dashboards-metric.png) |<span data-ttu-id="986e8-141">Muestra el número total de resultados de la búsqueda de registros como número en un icono.</span><span class="sxs-lookup"><span data-stu-id="986e8-141">Displays your total log search result hits as a number in a tile.</span></span> <span data-ttu-id="986e8-142">Los mosaicos de métrica permiten establecer un umbral que hará resaltar el mosaico si se alcanza el umbral.</span><span class="sxs-lookup"><span data-stu-id="986e8-142">Metric tiles allow you to set a threshold that will highlight the tile when the threshold is reached.</span></span> |
| ![line](./media/log-analytics-dashboards/oms-dashboards-line.png) |<span data-ttu-id="986e8-144">Muestra una escala de tiempo de los resultados de búsquedas de registros guardadas con los valores en forma de gráfico de líneas.</span><span class="sxs-lookup"><span data-stu-id="986e8-144">Displays a timeline of your saved log search result hits with values as a line chart.</span></span> |

### <a name="threshold"></a><span data-ttu-id="986e8-145">Umbral</span><span class="sxs-lookup"><span data-stu-id="986e8-145">Threshold</span></span>
<span data-ttu-id="986e8-146">Puede crear un umbral en un mosaico mediante la visualización Métrica.</span><span class="sxs-lookup"><span data-stu-id="986e8-146">You can create a threshold on a tile using the Metric visualization.</span></span> <span data-ttu-id="986e8-147">Seleccione esta opción para crear un valor de umbral en el mosaico.</span><span class="sxs-lookup"><span data-stu-id="986e8-147">Select on to create a threshold value on the tile.</span></span> <span data-ttu-id="986e8-148">Elija si quiere resaltar el mosaico cuando el valor está por encima o por debajo del umbral seleccionado y, luego, establezca el valor del umbral.</span><span class="sxs-lookup"><span data-stu-id="986e8-148">Choose whether to highlight the tile when the value is over or under the chosen threshold, then set the threshold value below.</span></span>

## <a name="organizing-the-dashboard"></a><span data-ttu-id="986e8-149">Organización del panel</span><span class="sxs-lookup"><span data-stu-id="986e8-149">Organizing the dashboard</span></span>
<span data-ttu-id="986e8-150">Para organizar el panel, vaya a la vista Mi panel y haga clic en **Personalizar** para entrar en el modo de personalización.</span><span class="sxs-lookup"><span data-stu-id="986e8-150">To organize your dashboard, navigate to the My Dashboard view and click **Customize** to enter customize mode.</span></span> <span data-ttu-id="986e8-151">Haga clic y arrastre el mosaico que quiere mover y muévalo hasta donde quiere que esté.</span><span class="sxs-lookup"><span data-stu-id="986e8-151">Click and drag the tile you want to move, and move it to where you want your tile to be.</span></span>

![Organizar el panel](./media/log-analytics-dashboards/oms-dashboards-organize.png)

## <a name="remove-a-tile"></a><span data-ttu-id="986e8-153">Quitar un mosaico</span><span class="sxs-lookup"><span data-stu-id="986e8-153">Remove a tile</span></span>
<span data-ttu-id="986e8-154">Para quitar un icono, vaya a la vista Mi panel y haga clic en **Personalizar** para entrar en el modo de personalización.</span><span class="sxs-lookup"><span data-stu-id="986e8-154">To remove a tile, navigate to the My Dashboard view and click **Customize** to enter customize mode.</span></span> <span data-ttu-id="986e8-155">Seleccione el icono que quiere quitar y, luego, en el panel de la derecha, seleccione **Quitar icono**.</span><span class="sxs-lookup"><span data-stu-id="986e8-155">Select the tile you want to remove, then on the right panel select **Remove Tile**.</span></span>

![Quitar un mosaico](./media/log-analytics-dashboards/oms-dashboards-remove-tile.png)

## <a name="next-steps"></a><span data-ttu-id="986e8-157">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="986e8-157">Next steps</span></span>
* <span data-ttu-id="986e8-158">Cree [alertas](log-analytics-alerts.md) en Log Analytics para generar notificaciones y solucionar problemas.</span><span class="sxs-lookup"><span data-stu-id="986e8-158">Create [alerts](log-analytics-alerts.md) in Log Analytics to generate notifications and to remediate problems.</span></span>
