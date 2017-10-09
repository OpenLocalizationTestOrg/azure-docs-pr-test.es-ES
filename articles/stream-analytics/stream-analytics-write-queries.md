---
title: "aaaHow toowrite consultas de análisis de transmisiones | Documentos de Microsoft"
description: "Escritura de consultas en Análisis de transmisiones y datos de consulta | segmento de ruta de aprendizaje."
keywords: "¿Cómo toowrite consultas, consultar los datos, escribir una consulta, escribir consultas"
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 0e9cdadd-0ee0-4bee-b65b-4a06fb863c95
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: b943c34f10afd2b21789afbd341c471a5f168729
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toowrite-queries-in-stream-analytics"></a><span data-ttu-id="95b27-104">Cómo toowrite las consultas de análisis de transmisiones</span><span class="sxs-lookup"><span data-stu-id="95b27-104">How toowrite queries in Stream Analytics</span></span>
<span data-ttu-id="95b27-105">Escribir consultas para el flujo de procesamiento de la lógica de análisis de transmisiones de Azure se implementa como una "consulta permanente" que se define antes de que un trabajo se inicia y se ejecuta con datos alcanzar trabajo Hola.</span><span class="sxs-lookup"><span data-stu-id="95b27-105">Writing queries for stream processing logic in Azure Stream Analytics is implemented as a "standing query" that is defined before a job starts and executed on data as it reaches hello job.</span></span> <span data-ttu-id="95b27-106">transformación de datos de Hola se expresa en un lenguaje de consulta similar a SQL, que es en gran medida un subconjunto de T-SQL con algunos agregan extensiones de lenguaje como [ventana](https://msdn.microsoft.com/library/azure/dn835019.aspx) utiliza semántica temporal tooexpress.</span><span class="sxs-lookup"><span data-stu-id="95b27-106">hello data transformation is expressed in a SQL-like query language, which is largely a subset of T-SQL with some added language extensions like [Windowing](https://msdn.microsoft.com/library/azure/dn835019.aspx) used tooexpress temporal semantics.</span></span>

## <a name="writing-queries"></a><span data-ttu-id="95b27-107">Escritura de consultas:</span><span class="sxs-lookup"><span data-stu-id="95b27-107">Writing Queries:</span></span>
1. <span data-ttu-id="95b27-108">En su trabajo de análisis de transmisiones en el portal de administración de Azure de hello, haga clic en **consulta**.</span><span class="sxs-lookup"><span data-stu-id="95b27-108">In your Stream Analytics Job in hello Azure Management portal, click **Query**.</span></span>
   
    ![Seleccionar consulta](./media/stream-analytics-write-queries/1-stream-analytics-write-queries.png)  
   
    <span data-ttu-id="95b27-110">Hola Portal de Azure, haga clic en **consulta**.</span><span class="sxs-lookup"><span data-stu-id="95b27-110">In hello Azure Portal, click **Query**.</span></span>
   
    ![Vista previa de selección de consulta](./media/stream-analytics-write-queries/query-preview-portal.png)  
2. <span data-ttu-id="95b27-112">Nuevos trabajos tienen un toohelp de plantilla de consulta ayudarle a comenzar.</span><span class="sxs-lookup"><span data-stu-id="95b27-112">New jobs have a query template toohelp get you started.</span></span> <span data-ttu-id="95b27-113">consulta de Hello plantilla realiza un "acceso directo" de consulta que proyecta todos los campos de eventos de entrada en la salida de hello.</span><span class="sxs-lookup"><span data-stu-id="95b27-113">hello query template performs a "pass-through" query that projects all fields from input events into hello output.</span></span>  
   
   * <span data-ttu-id="95b27-114">Si ha definido al menos una entrada y salida para el trabajo, puede reemplazar el marcador de posición de Hola "[YourOutputAlias]" y "[YourInputAlias]" campos con alias de Hola Hola de entrada y salida que desea usar en primer lugar.</span><span class="sxs-lookup"><span data-stu-id="95b27-114">If you have defined at least one input and output for your job, you can replace hello placeholder "[YourOutputAlias]" and "[YourInputAlias]" fields with hello aliases of hello input and output that you wish use first.</span></span> <span data-ttu-id="95b27-115">Además, todavía puede crear y probar la consulta en hello Portal clásico de Azure sin definir entradas y salidas de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="95b27-115">In addition, you can still author and test your query in hello Azure Classic Portal without defining inputs and outputs on hello job.</span></span>
   * <span data-ttu-id="95b27-116">Si desea tooperform procesamiento más complejo que un acceso directo simple, puede editar la definición de la consulta de Hola.</span><span class="sxs-lookup"><span data-stu-id="95b27-116">If you wish tooperform more processing than a simple pass-through, you can edit hello query definition.</span></span> <span data-ttu-id="95b27-117">tooget a trabajar con consultas de creación, eche un vistazo a algunas consultas comunes se capturan patrones [aquí](stream-analytics-stream-analytics-query-patterns.md).</span><span class="sxs-lookup"><span data-stu-id="95b27-117">tooget started with query authoring, take a look at some common query patterns are captured [here](stream-analytics-stream-analytics-query-patterns.md).</span></span>  
   
   ![Ventana de datos de consulta](./media/stream-analytics-write-queries/2-stream-analytics-write-queries.png)  

## <a name="toovalidate-query-data-is-working"></a><span data-ttu-id="95b27-119">consultar los datos de toovalidate funciona:</span><span class="sxs-lookup"><span data-stu-id="95b27-119">toovalidate query data is working:</span></span>
<span data-ttu-id="95b27-120">Puede probar que la consulta se comporta según lo esperado mediante la ejecución en el Explorador de hello en uno o más archivos JSON locales que contiene los datos de prueba.</span><span class="sxs-lookup"><span data-stu-id="95b27-120">You can test that your query behaves as expected by running it in hello browser over one or more local JSON files containing test data.</span></span> <span data-ttu-id="95b27-121">Esto no iniciar el trabajo de Hola o tiene las implicaciones de facturación.</span><span class="sxs-lookup"><span data-stu-id="95b27-121">This will not start hello job or have any billing implications.</span></span>

> [!NOTE]
> <span data-ttu-id="95b27-122">Actualmente no se admite la prueba de consultas en el Explorador de hello Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="95b27-122">Currently in-browser query testing is not supported in hello Azure Portal.</span></span>  
> 
> 

1. <span data-ttu-id="95b27-123">Asegúrese de que no hay ningún error en la consulta de hello (en caso contrario Hola prueba botón se deshabilitará) y, a continuación, haga clic en botón de prueba de Hola.</span><span class="sxs-lookup"><span data-stu-id="95b27-123">Make sure that there are no errors in hello query (otherwise hello Test button will be disabled) and then click hello Test button.</span></span>  
   
   ![Prueba de datos de consulta](./media/stream-analytics-write-queries/3-stream-analytics-write-queries.png)  
2. <span data-ttu-id="95b27-125">Es posible que los archivos toospecify solicitadas para cada una de las entradas de hello hace referencia en la consulta de Hola.</span><span class="sxs-lookup"><span data-stu-id="95b27-125">You will be prompted toospecify files for each of hello inputs referenced in hello query.</span></span> <span data-ttu-id="95b27-126">En este ejemplo, la consulta de la plantilla de Hola se deja como-es, por lo que está pidiendo al cuadro de diálogo de Hola para una entrada denominada "yourinputalias".</span><span class="sxs-lookup"><span data-stu-id="95b27-126">In this example, hello template query is left as-is, so hello dialog is prompting for an input named "yourinputalias".</span></span>  
   
   ![Consulta de datos de prueba](./media/stream-analytics-write-queries/4-stream-analytics-write-queries.png)  
3. <span data-ttu-id="95b27-128">Examinar el archivo de prueba de tooa.</span><span class="sxs-lookup"><span data-stu-id="95b27-128">Browse tooa test file.</span></span> <span data-ttu-id="95b27-129">Varios archivos de ejemplo están disponibles en [github](https://github.com/Azure/azure-stream-analytics/tree/master/Sample Data) y también puede recuperar los datos de ejemplo de sus propias entradas de flujo de datos a través de la función de datos de ejemplo en la pestaña de entradas de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="95b27-129">Several sample files are available on [github](https://github.com/Azure/azure-stream-analytics/tree/master/Sample Data) and you can also retrieve sample data from your own data stream inputs via hello Sample Data function on hello inputs tab.</span></span>  
   
   ![Entrada de consulta](./media/stream-analytics-write-queries/5-stream-analytics-write-queries.png)  
4. <span data-ttu-id="95b27-131">Después de cerrar el cuadro de diálogo de hello, la consulta se ejecutará sobre datos de prueba de Hola y verá los resultados de hello en parte inferior de Hola de página de la consulta de Hola.</span><span class="sxs-lookup"><span data-stu-id="95b27-131">After closing hello dialog, your query will be run over hello test data and you will see hello results at hello bottom of hello Query page.</span></span>  
   
   ![Resumen de la consulta](./media/stream-analytics-write-queries/6-stream-analytics-write-queries.png)  

## <a name="get-help"></a><span data-ttu-id="95b27-133">Obtener ayuda</span><span class="sxs-lookup"><span data-stu-id="95b27-133">Get help</span></span>
<span data-ttu-id="95b27-134">Para obtener más ayuda, pruebe nuestro [foro de Análisis de transmisiones de Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="95b27-134">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="95b27-135">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="95b27-135">Next steps</span></span>
* [<span data-ttu-id="95b27-136">Introducción tooAzure análisis de transmisiones</span><span class="sxs-lookup"><span data-stu-id="95b27-136">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="95b27-137">Introducción al uso de Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="95b27-137">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="95b27-138">Escalación de trabajos de Análisis de transmisiones de Azure</span><span class="sxs-lookup"><span data-stu-id="95b27-138">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="95b27-139">Referencia del lenguaje de consulta de Análisis de transmisiones de Azure</span><span class="sxs-lookup"><span data-stu-id="95b27-139">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="95b27-140">Referencia de API de REST de administración de Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="95b27-140">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

