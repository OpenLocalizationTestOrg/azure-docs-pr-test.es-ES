---
title: "las consultas aaaDebug análisis de transmisiones de Azure mediante el uso de SELECT INTO | Documentos de Microsoft"
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
ms.openlocfilehash: 27e41af1a6ea06b4509d07a3a67087490d0ec1fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="debug-queries-by-using-select-into-statements"></a><span data-ttu-id="a7824-103">Depuración de consultas mediante instrucciones SELECT INTO</span><span class="sxs-lookup"><span data-stu-id="a7824-103">Debug queries by using SELECT INTO statements</span></span>

<span data-ttu-id="a7824-104">En el procesamiento de datos en tiempo real, saber qué datos Hola parece en medio de Hola de hello consulta puede ser útil.</span><span class="sxs-lookup"><span data-stu-id="a7824-104">In real-time data processing, knowing what hello data looks like in hello middle of hello query can be helpful.</span></span> <span data-ttu-id="a7824-105">Como las entradas o pasos de un trabajo de Azure Stream Analytics se pueden leer muchas veces, puede escribir instrucciones SELECT INTO adicionales.</span><span class="sxs-lookup"><span data-stu-id="a7824-105">Because inputs or steps of an Azure Stream Analytics job can be read multiple times, you can write extra SELECT INTO statements.</span></span> <span data-ttu-id="a7824-106">Si lo hace, genera los datos intermedios en el almacenamiento y le permite inspeccionar la exactitud de Hola de datos de hello, al igual que *inspeccionar variables* hace cuando se depura un programa.</span><span class="sxs-lookup"><span data-stu-id="a7824-106">Doing so outputs intermediate data into storage and lets you inspect hello correctness of hello data, just as *watch variables* do when you debug a program.</span></span>

## <a name="use-select-into-toocheck-hello-data-stream"></a><span data-ttu-id="a7824-107">Use SELECT INTO toocheck Hola flujo de datos</span><span class="sxs-lookup"><span data-stu-id="a7824-107">Use SELECT INTO toocheck hello data stream</span></span>

<span data-ttu-id="a7824-108">Hello consulta de ejemplo siguiente en un trabajo de análisis de transmisiones de Azure tiene un flujo entrada, dos entradas de datos de referencia y un almacenamiento de tabla tooAzure de salida.</span><span class="sxs-lookup"><span data-stu-id="a7824-108">hello following example query in an Azure Stream Analytics job has one stream input, two reference data inputs, and an output tooAzure Table Storage.</span></span> <span data-ttu-id="a7824-109">consulta de Hello combina datos de concentrador de eventos de Hola y dos blobs tooget Hola nombre y categoría de información de referencia:</span><span class="sxs-lookup"><span data-stu-id="a7824-109">hello query joins data from hello event hub and two reference blobs tooget hello name and category information:</span></span>

![Ejemplo de consulta SELECT INTO](./media/stream-analytics-select-into/stream-analytics-select-into-query1.png)

<span data-ttu-id="a7824-111">Tenga en cuenta que se ejecuta el trabajo de hello, pero no se genera ningún evento de salida de hello.</span><span class="sxs-lookup"><span data-stu-id="a7824-111">Note that hello job is running, but no events are being produced in hello output.</span></span> <span data-ttu-id="a7824-112">En hello **supervisión** icono, se muestra a continuación, puede ver que Hola entrada produce datos, pero no sabe qué paso de hello **UNIR** iniciadas todos Hola toobe de eventos que se quita.</span><span class="sxs-lookup"><span data-stu-id="a7824-112">On hello **Monitoring** tile, shown here, you can see that hello input is producing data, but you don’t know which step of hello **JOIN** caused all hello events toobe dropped.</span></span>

![icono de supervisión de Hola](./media/stream-analytics-select-into/stream-analytics-select-into-monitor.png)
 
<span data-ttu-id="a7824-114">En esta situación, puede agregar algunas instrucciones de SELECT INTO adicionales demasiado "iniciar" hello los resultados intermedios de la combinación y datos de Hola que se leen de la entrada de Hola.</span><span class="sxs-lookup"><span data-stu-id="a7824-114">In this situation, you can add a few extra SELECT INTO statements too“log” hello intermediate JOIN results and hello data that's read from hello input.</span></span>

<span data-ttu-id="a7824-115">En este ejemplo, hemos agregado dos nuevas "salidas temporales".</span><span class="sxs-lookup"><span data-stu-id="a7824-115">In this example, we've added two new “temporary outputs.”</span></span> <span data-ttu-id="a7824-116">Estas pueden ser cualquier receptor que desee.</span><span class="sxs-lookup"><span data-stu-id="a7824-116">They can be any sink you like.</span></span> <span data-ttu-id="a7824-117">Aquí usamos Azure Storage como ejemplo:</span><span class="sxs-lookup"><span data-stu-id="a7824-117">Here we use Azure Storage as an example:</span></span>

![Adición de instrucciones SELECT INTO adicionales](./media/stream-analytics-select-into/stream-analytics-select-into-outputs.png)

<span data-ttu-id="a7824-119">A continuación, puede volver a escribir consultas Hola similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="a7824-119">You can then rewrite hello query like this:</span></span>

![Consulta SELECT INTO reescrita](./media/stream-analytics-select-into/stream-analytics-select-into-query2.png)

<span data-ttu-id="a7824-121">Ahora iniciar nuevo trabajo de Hola y permitir su ejecución durante unos minutos.</span><span class="sxs-lookup"><span data-stu-id="a7824-121">Now start hello job again, and let it run for a few minutes.</span></span> <span data-ttu-id="a7824-122">A continuación, consultar temp1 y temp2 con hello tooproduce de Visual Studio en la nube Explorer las tablas siguientes:</span><span class="sxs-lookup"><span data-stu-id="a7824-122">Then query temp1 and temp2 with Visual Studio Cloud Explorer tooproduce hello following tables:</span></span>

<span data-ttu-id="a7824-123">**tabla temp1**
![SELECT INTO tabla temp1](./media/stream-analytics-select-into/stream-analytics-select-into-temp-table-1.png)</span><span class="sxs-lookup"><span data-stu-id="a7824-123">**temp1 table**
![SELECT INTO temp1 table](./media/stream-analytics-select-into/stream-analytics-select-into-temp-table-1.png)</span></span>

<span data-ttu-id="a7824-124">**tabla temp2**
![SELECT INTO tabla temp2](./media/stream-analytics-select-into/stream-analytics-select-into-temp-table-2.png)</span><span class="sxs-lookup"><span data-stu-id="a7824-124">**temp2 table**
![SELECT INTO temp2 table](./media/stream-analytics-select-into/stream-analytics-select-into-temp-table-2.png)</span></span>

<span data-ttu-id="a7824-125">Como puede ver, temp1 y temp2 tienen datos y columna de nombre de Hola se rellena correctamente en temp2.</span><span class="sxs-lookup"><span data-stu-id="a7824-125">As you can see, temp1 and temp2 both have data, and hello name column is populated correctly in temp2.</span></span> <span data-ttu-id="a7824-126">Sin embargo, dado que todavía no hay ningún dato en la salida, algo sucede:</span><span class="sxs-lookup"><span data-stu-id="a7824-126">However, because there is still no data in output, something is wrong:</span></span>

![Tabla SELECT INTO output1 sin datos](./media/stream-analytics-select-into/stream-analytics-select-into-out-table-1.png)

<span data-ttu-id="a7824-128">Mediante el muestreo de datos de hello, puede estar casi seguro de que el problema de hello está Hola segundo combinación.</span><span class="sxs-lookup"><span data-stu-id="a7824-128">By sampling hello data, you can be almost certain that hello issue is with hello second JOIN.</span></span> <span data-ttu-id="a7824-129">Puede descargar los datos de referencia de Hola de blob de Hola y eche un vistazo:</span><span class="sxs-lookup"><span data-stu-id="a7824-129">You can download hello reference data from hello blob and take a look:</span></span>

![Tabla de referencia de SELECT INTO](./media/stream-analytics-select-into/stream-analytics-select-into-ref-table-1.png)

<span data-ttu-id="a7824-131">Como puede ver, formato de Hola de hello GUID en estos datos de referencia es distinto del formato de Hola de hello [columna temp2 from].</span><span class="sxs-lookup"><span data-stu-id="a7824-131">As you can see, hello format of hello GUID in this reference data is different from hello format of hello [from] column in temp2.</span></span> <span data-ttu-id="a7824-132">Por eso no llegan datos hello en output1 según lo previsto.</span><span class="sxs-lookup"><span data-stu-id="a7824-132">That’s why hello data didn’t arrive in output1 as expected.</span></span>

<span data-ttu-id="a7824-133">Puede corregir el formato de datos de hello, cargar blob tooreference y vuelva a intentarlo:</span><span class="sxs-lookup"><span data-stu-id="a7824-133">You can fix hello data format, upload it tooreference blob, and try again:</span></span>

![Tabla temporal de SELECT INTO](./media/stream-analytics-select-into/stream-analytics-select-into-ref-table-2.png)

<span data-ttu-id="a7824-135">En esta ocasión, datos de hello en la salida de hello formatea y rellena según lo previsto.</span><span class="sxs-lookup"><span data-stu-id="a7824-135">This time, hello data in hello output is formatted and populated as expected.</span></span>

![Tabla final de SELECT INTO](./media/stream-analytics-select-into/stream-analytics-select-into-final-table.png)


## <a name="get-help"></a><span data-ttu-id="a7824-137">Obtener ayuda</span><span class="sxs-lookup"><span data-stu-id="a7824-137">Get help</span></span>

<span data-ttu-id="a7824-138">Para obtener ayuda adicional, pruebe nuestro [foro de Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="a7824-138">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a7824-139">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a7824-139">Next steps</span></span>

* [<span data-ttu-id="a7824-140">Introducción tooAzure análisis de transmisiones</span><span class="sxs-lookup"><span data-stu-id="a7824-140">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="a7824-141">Introducción al uso de Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="a7824-141">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="a7824-142">Escalación de trabajos de Análisis de transmisiones de Azure</span><span class="sxs-lookup"><span data-stu-id="a7824-142">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="a7824-143">Referencia del lenguaje de consulta de Análisis de transmisiones de Azure</span><span class="sxs-lookup"><span data-stu-id="a7824-143">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="a7824-144">Referencia de API de REST de administración de Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="a7824-144">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

