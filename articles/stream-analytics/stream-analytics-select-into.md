---
title: "Depuración de consultas de Azure Stream Analytics mediante SELECT INTO | Microsoft Docs"
description: Datos de ejemplo de consulta intermedia mediante instrucciones SELECT INTO en Stream Analytics
keywords: 
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 9952e2cf-b335-4a5c-8f45-8d3e1eda2e20
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/20/2017
ms.author: jeffstok
ms.openlocfilehash: b05222c6d6f4fc2c5b847dd75ff7e29352cd538c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="debug-queries-by-using-select-into-statements"></a><span data-ttu-id="b58ed-103">Depuración de consultas mediante instrucciones SELECT INTO</span><span class="sxs-lookup"><span data-stu-id="b58ed-103">Debug queries by using SELECT INTO statements</span></span>

<span data-ttu-id="b58ed-104">En el procesamiento de datos en tiempo real, puede ser útil conocer qué aspecto tendrán los datos en el medio de la consulta.</span><span class="sxs-lookup"><span data-stu-id="b58ed-104">In real-time data processing, knowing what the data looks like in the middle of the query can be helpful.</span></span> <span data-ttu-id="b58ed-105">Como las entradas o pasos de un trabajo de Azure Stream Analytics se pueden leer muchas veces, puede escribir instrucciones SELECT INTO adicionales.</span><span class="sxs-lookup"><span data-stu-id="b58ed-105">Because inputs or steps of an Azure Stream Analytics job can be read multiple times, you can write extra SELECT INTO statements.</span></span> <span data-ttu-id="b58ed-106">Si lo hace, se generan daros intermedios en el almacenamiento y puede inspeccionar la integridad de los datos, igual que hacen las *variables de inspección* cuando se depura un programa.</span><span class="sxs-lookup"><span data-stu-id="b58ed-106">Doing so outputs intermediate data into storage and lets you inspect the correctness of the data, just as *watch variables* do when you debug a program.</span></span>

## <a name="use-select-into-to-check-the-data-stream"></a><span data-ttu-id="b58ed-107">Uso de SELECT INTO para comprobar el flujo de datos</span><span class="sxs-lookup"><span data-stu-id="b58ed-107">Use SELECT INTO to check the data stream</span></span>

<span data-ttu-id="b58ed-108">La siguiente consulta de ejemplo en un trabajo de Azure Stream Analytics tiene una entrada de secuencias, dos entradas de datos de referencia y una salida a Azure Table Storage.</span><span class="sxs-lookup"><span data-stu-id="b58ed-108">The following example query in an Azure Stream Analytics job has one stream input, two reference data inputs, and an output to Azure Table Storage.</span></span> <span data-ttu-id="b58ed-109">La consulta combina datos del centro de eventos y dos blobs de referencia para obtener la información de nombre y categoría:</span><span class="sxs-lookup"><span data-stu-id="b58ed-109">The query joins data from the event hub and two reference blobs to get the name and category information:</span></span>

![Ejemplo de consulta SELECT INTO](./media/stream-analytics-select-into/stream-analytics-select-into-query1.png)

<span data-ttu-id="b58ed-111">Tenga en cuenta que el trabajo está en ejecución, pero no se genera ningún evento en la salida.</span><span class="sxs-lookup"><span data-stu-id="b58ed-111">Note that the job is running, but no events are being produced in the output.</span></span> <span data-ttu-id="b58ed-112">En el icono **Supervisión**, que se muestra aquí, puede ver que la entrada genera datos, pero no sabe qué paso de la cláusula **JOIN** ha hecho que se descarten todos los eventos.</span><span class="sxs-lookup"><span data-stu-id="b58ed-112">On the **Monitoring** tile, shown here, you can see that the input is producing data, but you don’t know which step of the **JOIN** caused all the events to be dropped.</span></span>

![Icono de Supervisión](./media/stream-analytics-select-into/stream-analytics-select-into-monitor.png)
 
<span data-ttu-id="b58ed-114">En esta situación, puede agregar unas cuantas instrucciones SELECT INTO adicionales para "registrar" los resultados intermedios de JOIN y los datos que se leen de la entrada.</span><span class="sxs-lookup"><span data-stu-id="b58ed-114">In this situation, you can add a few extra SELECT INTO statements to “log” the intermediate JOIN results and the data that's read from the input.</span></span>

<span data-ttu-id="b58ed-115">En este ejemplo, hemos agregado dos nuevas "salidas temporales".</span><span class="sxs-lookup"><span data-stu-id="b58ed-115">In this example, we've added two new “temporary outputs.”</span></span> <span data-ttu-id="b58ed-116">Estas pueden ser cualquier receptor que desee.</span><span class="sxs-lookup"><span data-stu-id="b58ed-116">They can be any sink you like.</span></span> <span data-ttu-id="b58ed-117">Aquí usamos Azure Storage como ejemplo:</span><span class="sxs-lookup"><span data-stu-id="b58ed-117">Here we use Azure Storage as an example:</span></span>

![Adición de instrucciones SELECT INTO adicionales](./media/stream-analytics-select-into/stream-analytics-select-into-outputs.png)

<span data-ttu-id="b58ed-119">A continuación, puede volver a escribir la consulta del modo siguiente:</span><span class="sxs-lookup"><span data-stu-id="b58ed-119">You can then rewrite the query like this:</span></span>

![Consulta SELECT INTO reescrita](./media/stream-analytics-select-into/stream-analytics-select-into-query2.png)

<span data-ttu-id="b58ed-121">Ahora, inicie de nuevo el trabajo y deje que se ejecute durante unos minutos.</span><span class="sxs-lookup"><span data-stu-id="b58ed-121">Now start the job again, and let it run for a few minutes.</span></span> <span data-ttu-id="b58ed-122">A continuación, consulte temp1 y temp2 con Visual Studio Cloud Explorer para generar las siguientes tablas:</span><span class="sxs-lookup"><span data-stu-id="b58ed-122">Then query temp1 and temp2 with Visual Studio Cloud Explorer to produce the following tables:</span></span>

<span data-ttu-id="b58ed-123">**tabla temp1**
![SELECT INTO tabla temp1](./media/stream-analytics-select-into/stream-analytics-select-into-temp-table-1.png)</span><span class="sxs-lookup"><span data-stu-id="b58ed-123">**temp1 table**
![SELECT INTO temp1 table](./media/stream-analytics-select-into/stream-analytics-select-into-temp-table-1.png)</span></span>

<span data-ttu-id="b58ed-124">**tabla temp2**
![SELECT INTO tabla temp2](./media/stream-analytics-select-into/stream-analytics-select-into-temp-table-2.png)</span><span class="sxs-lookup"><span data-stu-id="b58ed-124">**temp2 table**
![SELECT INTO temp2 table](./media/stream-analytics-select-into/stream-analytics-select-into-temp-table-2.png)</span></span>

<span data-ttu-id="b58ed-125">Como puede ver, temp1 y temp2 tienen ambas datos, y la columna de nombre está rellenada correctamente en temp2.</span><span class="sxs-lookup"><span data-stu-id="b58ed-125">As you can see, temp1 and temp2 both have data, and the name column is populated correctly in temp2.</span></span> <span data-ttu-id="b58ed-126">Sin embargo, dado que todavía no hay ningún dato en la salida, algo sucede:</span><span class="sxs-lookup"><span data-stu-id="b58ed-126">However, because there is still no data in output, something is wrong:</span></span>

![Tabla SELECT INTO output1 sin datos](./media/stream-analytics-select-into/stream-analytics-select-into-out-table-1.png)

<span data-ttu-id="b58ed-128">Mediante el muestreo de los datos, puede estar casi seguro de que el problema está relacionado con la segunda cláusula JOIN.</span><span class="sxs-lookup"><span data-stu-id="b58ed-128">By sampling the data, you can be almost certain that the issue is with the second JOIN.</span></span> <span data-ttu-id="b58ed-129">Puede descargar los datos de referencia del blob y echar un vistazo:</span><span class="sxs-lookup"><span data-stu-id="b58ed-129">You can download the reference data from the blob and take a look:</span></span>

![Tabla de referencia de SELECT INTO](./media/stream-analytics-select-into/stream-analytics-select-into-ref-table-1.png)

<span data-ttu-id="b58ed-131">Como puede ver, el formato del GUID en los datos de esta referencia es distinto del formato de la columna [from] en temp2.</span><span class="sxs-lookup"><span data-stu-id="b58ed-131">As you can see, the format of the GUID in this reference data is different from the format of the [from] column in temp2.</span></span> <span data-ttu-id="b58ed-132">Por eso los datos no llegan a output1 como estaba previsto.</span><span class="sxs-lookup"><span data-stu-id="b58ed-132">That’s why the data didn’t arrive in output1 as expected.</span></span>

<span data-ttu-id="b58ed-133">Puede corregir el formato de datos, cargarlo para que haga referencia al blob e intentarlo de nuevo:</span><span class="sxs-lookup"><span data-stu-id="b58ed-133">You can fix the data format, upload it to reference blob, and try again:</span></span>

![Tabla temporal de SELECT INTO](./media/stream-analytics-select-into/stream-analytics-select-into-ref-table-2.png)

<span data-ttu-id="b58ed-135">Esta vez, los datos en la salida tienen el formato adecuado y se han rellenado según lo previsto.</span><span class="sxs-lookup"><span data-stu-id="b58ed-135">This time, the data in the output is formatted and populated as expected.</span></span>

![Tabla final de SELECT INTO](./media/stream-analytics-select-into/stream-analytics-select-into-final-table.png)


## <a name="get-help"></a><span data-ttu-id="b58ed-137">Obtener ayuda</span><span class="sxs-lookup"><span data-stu-id="b58ed-137">Get help</span></span>

<span data-ttu-id="b58ed-138">Para obtener ayuda adicional, pruebe nuestro [foro de Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="b58ed-138">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b58ed-139">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b58ed-139">Next steps</span></span>

* [<span data-ttu-id="b58ed-140">Introducción a Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="b58ed-140">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="b58ed-141">Introducción al uso de Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="b58ed-141">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="b58ed-142">Escalación de trabajos de Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="b58ed-142">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="b58ed-143">Referencia del lenguaje de consulta de Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="b58ed-143">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="b58ed-144">Referencia de API de REST de administración de Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="b58ed-144">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

