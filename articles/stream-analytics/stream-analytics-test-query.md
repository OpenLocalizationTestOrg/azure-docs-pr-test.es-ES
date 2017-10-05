---
title: Prueba de consulta de Azure Stream Analytics | Microsoft Docs
description: "Cómo probar consultas en trabajos de Stream Analytics."
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
ms.openlocfilehash: 16bb3f26ec3a69e5204162db9e54a186cf1ec6a6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="test-azure-stream-analytics-queries-in-the-azure-portal"></a><span data-ttu-id="a2495-104">Prueba de consultas de Azure Stream Analytics en Azure Portal</span><span class="sxs-lookup"><span data-stu-id="a2495-104">Test Azure Stream Analytics queries in the Azure portal</span></span>

<span data-ttu-id="a2495-105">Con Azure Stream Analytics, puede probar consultas en Azure Portal sin tener que iniciar o detener un trabajo.</span><span class="sxs-lookup"><span data-stu-id="a2495-105">With Azure Stream Analytics, you can test queries in the Azure portal without needing to start or stop a job.</span></span>

## <a name="test-the-input"></a><span data-ttu-id="a2495-106">Prueba de la entrada</span><span class="sxs-lookup"><span data-stu-id="a2495-106">Test the input</span></span>

1. <span data-ttu-id="a2495-107">Para probar con datos de entrada de ejemplo, haga clic en cualquiera de las entradas y, a continuación, seleccione **Cargar datos de ejemplo desde un archivo**.</span><span class="sxs-lookup"><span data-stu-id="a2495-107">To test with sample input data, right-click any of your inputs, and then select **Upload sample data from file**.</span></span>

    ![consulta de prueba del editor de consultas de Stream Analytics](media/stream-analytics-test-query/stream-analytics-test-query-editor-upload.png)

2. <span data-ttu-id="a2495-109">Una vez finalizada la carga, haga clic en **Probar** para probar esta consulta con los datos de ejemplo que ha proporcionado.</span><span class="sxs-lookup"><span data-stu-id="a2495-109">After the upload is complete, click **Test** to test this query against the sample data you have provided.</span></span>

    ![datos de prueba de ejemplo del editor de consultas de Stream Analytics](media/stream-analytics-test-query/stream-analytics-test-query-editor-test.png)

<span data-ttu-id="a2495-111">El resultado de la consulta se muestra en el explorador, con el vínculo Descargar resultados por si desea guardar el resultado de prueba para un uso posterior.</span><span class="sxs-lookup"><span data-stu-id="a2495-111">The output of your query is displayed in the browser, with Download results link should you want to save the test output for later use.</span></span> <span data-ttu-id="a2495-112">Ahora puede modificar iterativamente y fácilmente la consulta y probarla repetidamente para ver cómo cambia la salida.</span><span class="sxs-lookup"><span data-stu-id="a2495-112">You can now easily and iteratively modify your query and test it repeatedly to see how the output changes.</span></span>

![Salida de ejemplo del editor de consultas de Stream Analytics](media/stream-analytics-test-query/stream-analytics-test-query-editor-samples-output.png)

<span data-ttu-id="a2495-114">Con varias salidas usadas en una consulta, podrá ver los resultados de ambas salidas de forma separada y alternar fácilmente entre ellas.</span><span class="sxs-lookup"><span data-stu-id="a2495-114">With multiple outputs used in a query, you can see the results for both outputs separately and easily toggle between them.</span></span>

<span data-ttu-id="a2495-115">Cuando esté satisfecho con los resultados mostrados en el explorador, podrá guardar la consulta, iniciar el trabajo y permitir que se procesen eventos sin errores.</span><span class="sxs-lookup"><span data-stu-id="a2495-115">After you are satisfied with the results shown in the browser, you can save your query, start your job, and let it process events without error.</span></span>

## <a name="get-help"></a><span data-ttu-id="a2495-116">Obtener ayuda</span><span class="sxs-lookup"><span data-stu-id="a2495-116">Get help</span></span>

<span data-ttu-id="a2495-117">Para obtener ayuda adicional, pruebe nuestro [foro de Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="a2495-117">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a2495-118">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a2495-118">Next steps</span></span>

* [<span data-ttu-id="a2495-119">Introducción a Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="a2495-119">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="a2495-120">Introducción al uso de Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="a2495-120">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="a2495-121">Escalación de trabajos de Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="a2495-121">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="a2495-122">Referencia del lenguaje de consulta de Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="a2495-122">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="a2495-123">Referencia de API de REST de administración de Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="a2495-123">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
