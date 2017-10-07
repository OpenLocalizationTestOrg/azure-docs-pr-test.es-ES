---
title: "entradas de muestreo AAA en análisis de transmisiones de Azure | Documentos de Microsoft"
description: "Identifique los problemas cuando realice la solución de problemas de trabajos de Stream Analytics."
keywords: "entrada de solución de problemas, muestreo de entrada"
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/20/2017
ms.author: jeffstok
ms.openlocfilehash: 9637a8664de099eebb8f5654036d2957f4c6b7ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-stream-analytics-input-stream-sampling"></a><span data-ttu-id="0d835-104">Muestreo de flujo de entrada de Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="0d835-104">Azure Stream Analytics input-stream sampling</span></span>

<span data-ttu-id="0d835-105">Mediante el análisis de transmisiones de Azure, puede muestrear eventos de entrada que proceden de un archivo y probar consultas en el portal de hello sin necesidad de toostart o detener un trabajo.</span><span class="sxs-lookup"><span data-stu-id="0d835-105">By using Azure Stream Analytics, you can sample input events that come from a file and test queries in hello portal without needing toostart or stop a job.</span></span>

## <a name="testing-your-query"></a><span data-ttu-id="0d835-106">Prueba de la consulta</span><span class="sxs-lookup"><span data-stu-id="0d835-106">Testing your query</span></span>

<span data-ttu-id="0d835-107">En el panel de detalles de trabajo de análisis de transmisiones de hello, abra hello **editor de consultas** hoja haciendo clic en el nombre de la consulta de hello en **consulta**.</span><span class="sxs-lookup"><span data-stu-id="0d835-107">In hello Stream Analytics job details pane, open hello **Query editor** blade by clicking hello query name under **Query**.</span></span> <span data-ttu-id="0d835-108">(En nuestro escenario de ejemplo, porque no hay ninguna consulta se ha creado aún, haga clic en hello **< >** marcador de posición.)</span><span class="sxs-lookup"><span data-stu-id="0d835-108">(In our example scenario, because no query has been created yet, click hello **< >** placeholder.)</span></span>

![editor de consultas de análisis de transmisiones de Hola](media/stream-analytics-sample-data-input/stream-analytics-query-editor.png)

<span data-ttu-id="0d835-110">hoja de editor enriquecido Hola para crear la consulta se muestra como ocurría en la versión anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="0d835-110">hello rich editor blade for creating your query is displayed as it was in hello previous release.</span></span> <span data-ttu-id="0d835-111">Ahora se ha actualizado la hoja de hello con un nuevo panel izquierdo de esa muestra hello entradas y salidas que son utilizados por la consulta de Hola y definidas para este trabajo.</span><span class="sxs-lookup"><span data-stu-id="0d835-111">Now hello blade has been updated with a new left pane that shows hello inputs and outputs that are used by hello query and defined for this job.</span></span>

![editor de consultas de análisis de transmisiones de Hello entradas y salidas de listas](media/stream-analytics-sample-data-input/stream-analytics-query-editor-highlight.png)

<span data-ttu-id="0d835-113">También se muestra una entrada o salida adicionales, que no se han definido.</span><span class="sxs-lookup"><span data-stu-id="0d835-113">Also shown are an additional input and output, which are not defined.</span></span> <span data-ttu-id="0d835-114">Provienen de la nueva plantilla de consulta de saludo inicial.</span><span class="sxs-lookup"><span data-stu-id="0d835-114">They come from hello new query template that you start with.</span></span> <span data-ttu-id="0d835-115">Se cambia, o incluso desaparecen por completo, al crear o Editar consulta Hola.</span><span class="sxs-lookup"><span data-stu-id="0d835-115">They change, or even disappear altogether, as you edit hello query.</span></span> <span data-ttu-id="0d835-116">Puede ignorar estos errores con seguridad por ahora.</span><span class="sxs-lookup"><span data-stu-id="0d835-116">You can safely ignore them for now.</span></span>

<span data-ttu-id="0d835-117">tootest con datos de entrada de ejemplo, haga clic en cualquiera de las entradas y, a continuación, seleccione **cargar datos de ejemplo de archivo**.</span><span class="sxs-lookup"><span data-stu-id="0d835-117">tootest with sample input data, right-click any of your inputs, and then select **Upload sample data from file**.</span></span>

![Hola datos de ejemplo de carga en editor de consulta de análisis de transmisiones de archivo (comando)](media/stream-analytics-sample-data-input/stream-analytics-query-editor-upload.png)

<span data-ttu-id="0d835-119">Una vez finalizada la carga de hello, haga clic en **prueba** tootest que acabas de proporcionar de datos de ejemplo de esta consulta contra Hola.</span><span class="sxs-lookup"><span data-stu-id="0d835-119">After hello upload is complete, click **Test** tootest this query against hello sample data you have just provided.</span></span>

![botón de prueba de editor de consulta de análisis de transmisiones de Hola](media/stream-analytics-sample-data-input/stream-analytics-query-editor-test.png)

<span data-ttu-id="0d835-121">Si desea generar resultados de pruebas de Hola de toosave para su uso posterior, salida de hello de la consulta se muestra en el Explorador de hello con resultados de la descarga de toohello de vínculo.</span><span class="sxs-lookup"><span data-stu-id="0d835-121">If you want toosave hello test output for later use, hello output of your query is displayed in hello browser with a link toohello download results.</span></span> <span data-ttu-id="0d835-122">Ahora puede fácilmente y de forma iterativa modifique la consulta y probarlo repetidamente toosee cómo cambia la salida de hello.</span><span class="sxs-lookup"><span data-stu-id="0d835-122">You can now easily and iteratively modify your query and test it repeatedly toosee how hello output changes.</span></span>

![Salida de ejemplo del editor de consultas de Stream Analytics](media/stream-analytics-sample-data-input/stream-analytics-query-editor-samples-output.png)

<span data-ttu-id="0d835-124">Hola delante de la imagen, se ha agregado una segunda salida, denominado **HighAvgTempOutput**.</span><span class="sxs-lookup"><span data-stu-id="0d835-124">In hello preceding image, a second output has been added, called **HighAvgTempOutput**.</span></span>

<span data-ttu-id="0d835-125">Cuando se usa varias salidas en una consulta, puede ver resultados de Hola para cada salida por separado y alternar fácilmente entre ellos.</span><span class="sxs-lookup"><span data-stu-id="0d835-125">When you use multiple outputs in a query, you can see hello results for each output separately and easily toggle between them.</span></span>

<span data-ttu-id="0d835-126">Cuando esté satisfecho con los resultados de hello, puede guardar la consulta, iniciar el trabajo, póngase cómodo y ver magia Hola de análisis de transmisiones.</span><span class="sxs-lookup"><span data-stu-id="0d835-126">After you are satisfied with hello results, you can save your query, start your job, sit back and watch hello magic of Stream Analytics.</span></span>

## <a name="get-help"></a><span data-ttu-id="0d835-127">Obtener ayuda</span><span class="sxs-lookup"><span data-stu-id="0d835-127">Get help</span></span>

<span data-ttu-id="0d835-128">Para obtener ayuda adicional, pruebe nuestro [foro de Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="0d835-128">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0d835-129">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0d835-129">Next steps</span></span>
* [<span data-ttu-id="0d835-130">Introducción tooAzure análisis de transmisiones</span><span class="sxs-lookup"><span data-stu-id="0d835-130">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="0d835-131">Introducción al uso de Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="0d835-131">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="0d835-132">Escalación de trabajos de Análisis de transmisiones de Azure</span><span class="sxs-lookup"><span data-stu-id="0d835-132">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="0d835-133">Referencia del lenguaje de consulta de Análisis de transmisiones de Azure</span><span class="sxs-lookup"><span data-stu-id="0d835-133">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="0d835-134">Referencia de API de REST de administración de Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="0d835-134">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
