---
title: "la prueba de consultas de análisis de transmisiones de aaaAzure | Documentos de Microsoft"
description: "¿Cómo tootest las consultas en los trabajos de análisis de transmisiones."
keywords: "probar consulta, consulta de solución de problemas"
documentation center: 
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
ms.openlocfilehash: 3b141d98332fdc170e696e181c8446796a86f78e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="test-azure-stream-analytics-queries-in-hello-azure-portal"></a><span data-ttu-id="48775-104">Probar las consultas de análisis de transmisiones de Azure en hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="48775-104">Test Azure Stream Analytics queries in hello Azure portal</span></span>

<span data-ttu-id="48775-105">Con el análisis de transmisiones de Azure, puede probar las consultas en hello portal de Azure sin necesidad de toostart o detener un trabajo.</span><span class="sxs-lookup"><span data-stu-id="48775-105">With Azure Stream Analytics, you can test queries in hello Azure portal without needing toostart or stop a job.</span></span>

## <a name="test-hello-input"></a><span data-ttu-id="48775-106">Entrada de Hola de prueba</span><span class="sxs-lookup"><span data-stu-id="48775-106">Test hello input</span></span>

1. <span data-ttu-id="48775-107">tootest con datos de entrada de ejemplo, haga clic en cualquiera de las entradas y, a continuación, seleccione **cargar datos de ejemplo de archivo**.</span><span class="sxs-lookup"><span data-stu-id="48775-107">tootest with sample input data, right-click any of your inputs, and then select **Upload sample data from file**.</span></span>

    ![consulta de prueba del editor de consultas de Stream Analytics](media/stream-analytics-test-query/stream-analytics-test-query-editor-upload.png)

2. <span data-ttu-id="48775-109">Una vez finalizada la carga de hello, haga clic en **prueba** tootest esta consulta contra Hola muestreo de los datos que ha proporcionado.</span><span class="sxs-lookup"><span data-stu-id="48775-109">After hello upload is complete, click **Test** tootest this query against hello sample data you have provided.</span></span>

    ![datos de prueba de ejemplo del editor de consultas de Stream Analytics](media/stream-analytics-test-query/stream-analytics-test-query-editor-test.png)

<span data-ttu-id="48775-111">salida de Hello de la consulta se muestra en el Explorador de hello, con el vínculo de descarga de resultados si quiere toosave salida de la prueba de Hola para su uso posterior.</span><span class="sxs-lookup"><span data-stu-id="48775-111">hello output of your query is displayed in hello browser, with Download results link should you want toosave hello test output for later use.</span></span> <span data-ttu-id="48775-112">Ahora puede fácilmente y de forma iterativa modifique la consulta y probarlo repetidamente toosee cómo cambia la salida de hello.</span><span class="sxs-lookup"><span data-stu-id="48775-112">You can now easily and iteratively modify your query and test it repeatedly toosee how hello output changes.</span></span>

![Salida de ejemplo del editor de consultas de Stream Analytics](media/stream-analytics-test-query/stream-analytics-test-query-editor-samples-output.png)

<span data-ttu-id="48775-114">Con varias salidas usadas en una consulta, puede ver los resultados de Hola de ambas salidas por separado y alternar fácilmente entre ellos.</span><span class="sxs-lookup"><span data-stu-id="48775-114">With multiple outputs used in a query, you can see hello results for both outputs separately and easily toggle between them.</span></span>

<span data-ttu-id="48775-115">Cuando esté satisfecho con los resultados de Hola se muestra en el Explorador de hello, puede guardar la consulta, iniciar el trabajo y dejar que procesan los eventos sin errores.</span><span class="sxs-lookup"><span data-stu-id="48775-115">After you are satisfied with hello results shown in hello browser, you can save your query, start your job, and let it process events without error.</span></span>

## <a name="get-help"></a><span data-ttu-id="48775-116">Obtener ayuda</span><span class="sxs-lookup"><span data-stu-id="48775-116">Get help</span></span>

<span data-ttu-id="48775-117">Para obtener ayuda adicional, pruebe nuestro [foro de Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="48775-117">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="48775-118">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="48775-118">Next steps</span></span>

* [<span data-ttu-id="48775-119">Introducción tooAzure análisis de transmisiones</span><span class="sxs-lookup"><span data-stu-id="48775-119">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="48775-120">Introducción al uso de Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="48775-120">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="48775-121">Escalación de trabajos de Análisis de transmisiones de Azure</span><span class="sxs-lookup"><span data-stu-id="48775-121">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="48775-122">Referencia del lenguaje de consulta de Análisis de transmisiones de Azure</span><span class="sxs-lookup"><span data-stu-id="48775-122">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="48775-123">Referencia de API de REST de administración de Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="48775-123">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
