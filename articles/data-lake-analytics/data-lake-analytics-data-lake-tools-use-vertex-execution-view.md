---
title: "Use the Vertex Execution View in Data Lake Tools for Visual Studio (Usar la vista de ejecución de vértices de Data Lake Tools para Visual Studio) | Microsoft Docs"
description: "Obtenga información acerca de cómo usar la vista de la ejecución de vértices para examinar los trabajos de Data Lake Analytics."
services: data-lake-analytics
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 5366d852-e7d6-44cf-a88c-e9f52f15f7df
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 10/13/2016
ms.author: jgao
ms.openlocfilehash: b788e7bc8ded86ebd49cc0be73e5b4e1bcbeaba3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-vertex-execution-view-in-data-lake-tools-for-visual-studio"></a><span data-ttu-id="dadef-103">Use the Vertex Execution View in Data Lake Tools for Visual Studio (Usar la vista de ejecución de vértices de Data Lake Tools para Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="dadef-103">Use the Vertex Execution View in Data Lake Tools for Visual Studio</span></span>
<span data-ttu-id="dadef-104">Obtenga información acerca de cómo usar la vista de la ejecución de vértices para examinar los trabajos de Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="dadef-104">Learn how to use the Vertex Execution View to exam Data Lake Analytics jobs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dadef-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="dadef-105">Prerequisites</span></span>

<span data-ttu-id="dadef-106">Necesitará conocimientos básicos de uso de Data Lake Tools para Visual Studio para desarrollar el script U-SQL.</span><span class="sxs-lookup"><span data-stu-id="dadef-106">You need basic knowledge of using Data Lake Tools for Visual Studio to develop U-SQL script.</span></span>  <span data-ttu-id="dadef-107">Vea [Tutorial: Desarrollo de scripts U-SQL mediante Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="dadef-107">See [Tutorial: develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>

## <a name="open-the-vertex-execution-view"></a><span data-ttu-id="dadef-108">Abrir la vista de ejecución de vértices</span><span class="sxs-lookup"><span data-stu-id="dadef-108">Open the Vertex Execution View</span></span>
<span data-ttu-id="dadef-109">Abra un trabajo de U-SQL en Data Lake Tools para Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="dadef-109">Open a U-SQL job in Data Lake Tools for Visual Studio.</span></span> <span data-ttu-id="dadef-110">Haga clic en la **vista de ejecución de vértices** en la esquina inferior izquierda.</span><span class="sxs-lookup"><span data-stu-id="dadef-110">Click **Vertex Execution View** in the bottom left corner.</span></span> <span data-ttu-id="dadef-111">Se le solicitará cargar primero los perfiles, lo que puede tardar algún tiempo según la conectividad de red.</span><span class="sxs-lookup"><span data-stu-id="dadef-111">You may be prompted to load profiles first and it can take some time depending on your network connectivity.</span></span>

![Vista de ejecución de vértices de Data Lake Analytics Tools](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-open-vertex-execution-view.png)

## <a name="understand-vertex-execution-view"></a><span data-ttu-id="dadef-113">Comprensión de la vista de ejecución de vértices</span><span class="sxs-lookup"><span data-stu-id="dadef-113">Understand Vertex Execution View</span></span>
<span data-ttu-id="dadef-114">La vista de ejecución de vértices consta de tres partes:</span><span class="sxs-lookup"><span data-stu-id="dadef-114">The Vertex Execution View has three parts:</span></span>

![Vista de ejecución de vértices de Data Lake Analytics Tools](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-vertex-execution-view.png)

<span data-ttu-id="dadef-116">El **selector de vértices** a la izquierda permite seleccionar vértices por características (como las 10 lecturas de datos más importantes o elegir por fase).</span><span class="sxs-lookup"><span data-stu-id="dadef-116">The **Vertex selector** on the left lets you select vertices by features (such as top 10 data read, or choose by stage).</span></span> <span data-ttu-id="dadef-117">Uno de los filtros usados más comúnmente es el de los **vértices en la ruta de acceso crítica**.</span><span class="sxs-lookup"><span data-stu-id="dadef-117">One of the most commonly-used filters is to see the **vertices on critical path**.</span></span> <span data-ttu-id="dadef-118">La **ruta de acceso crítica** es la cadena más larga de vértices de un trabajo de U-SQL.</span><span class="sxs-lookup"><span data-stu-id="dadef-118">The **Critical path** is the longest chain of vertices of a U-SQL job.</span></span> <span data-ttu-id="dadef-119">Saber cómo funciona resulta útil para la optimización de los trabajos al comprobar qué vértice tarda más tiempo.</span><span class="sxs-lookup"><span data-stu-id="dadef-119">Understanding the critical path is useful for optimizing your jobs by checking which vertex takes the longest time.</span></span>
  
![Vista de ejecución de vértices de Data Lake Analytics Tools](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-vertex-execution-view-pane2.png)

<span data-ttu-id="dadef-121">El panel superior central muestra el **estado de ejecución de todos los vértices**.</span><span class="sxs-lookup"><span data-stu-id="dadef-121">The top center pane shows the **running status of all the vertices**.</span></span>
  
![Vista de ejecución de vértices de Data Lake Analytics Tools](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-vertex-execution-view-pane3.png)

<span data-ttu-id="dadef-123">El panel inferior central muestra información sobre cada vértice:</span><span class="sxs-lookup"><span data-stu-id="dadef-123">The bottom center pane shows information about each vertex:</span></span>
* <span data-ttu-id="dadef-124">Nombre del proceso: nombre de la instancia de vértice.</span><span class="sxs-lookup"><span data-stu-id="dadef-124">Process Name: The name of the vertex instance.</span></span> <span data-ttu-id="dadef-125">Se compone de distintas partes de StageName|VertexName|VertexRunInstance.</span><span class="sxs-lookup"><span data-stu-id="dadef-125">It is composed of different parts in StageName|VertexName|VertexRunInstance.</span></span> <span data-ttu-id="dadef-126">Por ejemplo, el vértice SV7_Split[62].v1 corresponde a la segunda instancia en ejecución (.v1, índice que comienza desde 0) del número de vértice 62 en Stage SV7_Split.</span><span class="sxs-lookup"><span data-stu-id="dadef-126">For example, the SV7_Split[62].v1 vertex stands for the second running instance (.v1, index starting from 0) of Vertex number 62 in Stage SV7_Split.</span></span>
* <span data-ttu-id="dadef-127">Escritura/lectura de datos total: los datos leídos/escritos por este vértice.</span><span class="sxs-lookup"><span data-stu-id="dadef-127">Total Data Read/Written: The data was read/written by this vertex.</span></span>
* <span data-ttu-id="dadef-128">Estado de salida/estado: el estado final cuando finaliza el vértice.</span><span class="sxs-lookup"><span data-stu-id="dadef-128">State/Exit Status: The final status when the vertex is ended.</span></span>
* <span data-ttu-id="dadef-129">Código de salida/tipo d error: el error cuando produce un error en el vértice.</span><span class="sxs-lookup"><span data-stu-id="dadef-129">Exit Code/Failure Type: The error when the vertex failed.</span></span>
* <span data-ttu-id="dadef-130">Motivo de la creación: motivo por el que se creó el vértice.</span><span class="sxs-lookup"><span data-stu-id="dadef-130">Creation Reason: Why the vertex was created.</span></span>
* <span data-ttu-id="dadef-131">Latencia de cola PN/latencia de proceso/latencia de recurso: el tiempo que tarda el vértice en esperar a los recursos, procesar los datos y permanecer en la cola.</span><span class="sxs-lookup"><span data-stu-id="dadef-131">Resource Latency/Process Latency/PN Queue Latency: the time taken for the vertex to wait for resources, to process data, and to stay in the queue.</span></span>
* <span data-ttu-id="dadef-132">GUID del creador/proceso: GUID del vértice de ejecución actual o su creador.</span><span class="sxs-lookup"><span data-stu-id="dadef-132">Process/Creator GUID: GUID for the current running vertex or its creator.</span></span>
* <span data-ttu-id="dadef-133">Versión: la instancia N del vértice de ejecución (el sistema puede programar nuevas instancias de un vértice por diversos motivos, por ejemplo, conmutación por error, redundancia de proceso, etc.).</span><span class="sxs-lookup"><span data-stu-id="dadef-133">Version: the N-th instance of the running vertex (the system might schedule new instances of a vertex for many reasons, for example failover, compute redundancy, etc.)</span></span>
* <span data-ttu-id="dadef-134">Hora de creación de la versión</span><span class="sxs-lookup"><span data-stu-id="dadef-134">Version Created Time.</span></span>
* <span data-ttu-id="dadef-135">Tiempo de inicio de creación de proceso/Tiempo en cola de proceso/Tiempo de inicio de proceso/Tiempo completo de proceso: cuando el proceso de vértice comienza la creación; cuando el proceso de vértice comienza a almacenarse en cola; cuando comienza determinado proceso de vértice; cuando un vértice concreto se completa.</span><span class="sxs-lookup"><span data-stu-id="dadef-135">Process Create Start Time/Process Queued Time/Process Start Time/Process Complete Time: when the vertex process starts creation; when the vertex process starts to queue; when the certain vertex process starts; when the certain vertex is completed.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dadef-136">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="dadef-136">Next steps</span></span>
* <span data-ttu-id="dadef-137">Para registrar información de diagnóstico, consulte [Accessing Diagnostics logs for Azure Data Lake Analytics](data-lake-analytics-diagnostic-logs.md)</span><span class="sxs-lookup"><span data-stu-id="dadef-137">To log diagnostics information, see [Accessing diagnostics logs for Azure Data Lake Analytics](data-lake-analytics-diagnostic-logs.md)</span></span>
* <span data-ttu-id="dadef-138">Para ver una consulta más compleja, consulte la página sobre el [análisis de registros de sitio web mediante Análisis de Azure Data Lake](data-lake-analytics-analyze-weblogs.md).</span><span class="sxs-lookup"><span data-stu-id="dadef-138">To see a more complex query, see [Analyze Website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
* <span data-ttu-id="dadef-139">Para ver los detalles del trabajo, vea [Usar el explorador de trabajos y la vista de trabajos para trabajos de Azure Data Lake Analytics](data-lake-analytics-data-lake-tools-view-jobs.md)</span><span class="sxs-lookup"><span data-stu-id="dadef-139">To view job details, see [Use Job Browser and Job View for Azure Data lake Analytics jobs](data-lake-analytics-data-lake-tools-view-jobs.md)</span></span>
