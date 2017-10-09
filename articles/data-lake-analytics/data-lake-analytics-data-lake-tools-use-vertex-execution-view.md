---
title: "Hola aaaUse vista de ejecución de vértices de Data Lake Tools para Visual Studio | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse Hola trabajos de análisis de Data Lake tooexam de vista de la ejecución de vértices."
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
ms.openlocfilehash: fb54d2af8a32aa27a54ff50a73c1b4903677a21e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-vertex-execution-view-in-data-lake-tools-for-visual-studio"></a><span data-ttu-id="ed96f-103">Usar hello vista de ejecución de vértices en Data Lake Tools para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ed96f-103">Use hello Vertex Execution View in Data Lake Tools for Visual Studio</span></span>
<span data-ttu-id="ed96f-104">Obtenga información acerca de cómo toouse Hola trabajos de análisis de Data Lake tooexam de vista de la ejecución de vértices.</span><span class="sxs-lookup"><span data-stu-id="ed96f-104">Learn how toouse hello Vertex Execution View tooexam Data Lake Analytics jobs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ed96f-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="ed96f-105">Prerequisites</span></span>

<span data-ttu-id="ed96f-106">Se necesitan conocimientos básicos del uso de Data Lake Tools para secuencia de comandos de Visual Studio toodevelop U-SQL.</span><span class="sxs-lookup"><span data-stu-id="ed96f-106">You need basic knowledge of using Data Lake Tools for Visual Studio toodevelop U-SQL script.</span></span>  <span data-ttu-id="ed96f-107">Vea [Tutorial: Desarrollo de scripts U-SQL mediante Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="ed96f-107">See [Tutorial: develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>

## <a name="open-hello-vertex-execution-view"></a><span data-ttu-id="ed96f-108">Hola Abrir vista de ejecución de vértices</span><span class="sxs-lookup"><span data-stu-id="ed96f-108">Open hello Vertex Execution View</span></span>
<span data-ttu-id="ed96f-109">Abra un trabajo de U-SQL en Data Lake Tools para Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ed96f-109">Open a U-SQL job in Data Lake Tools for Visual Studio.</span></span> <span data-ttu-id="ed96f-110">Haga clic en **vista de ejecución de vértices** en la esquina izquierda inferior de Hola.</span><span class="sxs-lookup"><span data-stu-id="ed96f-110">Click **Vertex Execution View** in hello bottom left corner.</span></span> <span data-ttu-id="ed96f-111">Es posible que los perfiles de tooload solicitadas en primer lugar y puede tardar algún tiempo, según la conectividad de red.</span><span class="sxs-lookup"><span data-stu-id="ed96f-111">You may be prompted tooload profiles first and it can take some time depending on your network connectivity.</span></span>

![Vista de ejecución de vértices de Data Lake Analytics Tools](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-open-vertex-execution-view.png)

## <a name="understand-vertex-execution-view"></a><span data-ttu-id="ed96f-113">Comprensión de la vista de ejecución de vértices</span><span class="sxs-lookup"><span data-stu-id="ed96f-113">Understand Vertex Execution View</span></span>
<span data-ttu-id="ed96f-114">Hola vértices ejecución vista tiene tres partes:</span><span class="sxs-lookup"><span data-stu-id="ed96f-114">hello Vertex Execution View has three parts:</span></span>

![Vista de ejecución de vértices de Data Lake Analytics Tools](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-vertex-execution-view.png)

<span data-ttu-id="ed96f-116">Hola **selector de vértices** en permite izquierdo Hola seleccionar vértices características (como top 10 datos leer, o elija por fase).</span><span class="sxs-lookup"><span data-stu-id="ed96f-116">hello **Vertex selector** on hello left lets you select vertices by features (such as top 10 data read, or choose by stage).</span></span> <span data-ttu-id="ed96f-117">Uno de los filtros usados con más frecuencia hello es hello toosee **vértices en la ruta crítica**.</span><span class="sxs-lookup"><span data-stu-id="ed96f-117">One of hello most commonly-used filters is toosee hello **vertices on critical path**.</span></span> <span data-ttu-id="ed96f-118">Hola **ruta crítica** Hola cadena más larga de vértices de un trabajo de SQL U.</span><span class="sxs-lookup"><span data-stu-id="ed96f-118">hello **Critical path** is hello longest chain of vertices of a U-SQL job.</span></span> <span data-ttu-id="ed96f-119">Ruta de acceso crítica Hola de descripción es útil para optimizar los trabajos mediante la comprobación de los vértices lleva tiempo más largo de Hola.</span><span class="sxs-lookup"><span data-stu-id="ed96f-119">Understanding hello critical path is useful for optimizing your jobs by checking which vertex takes hello longest time.</span></span>
  
![Vista de ejecución de vértices de Data Lake Analytics Tools](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-vertex-execution-view-pane2.png)

<span data-ttu-id="ed96f-121">panel del centro superior de Hello muestra hello **ejecutando el estado de todos los vértices de hello**.</span><span class="sxs-lookup"><span data-stu-id="ed96f-121">hello top center pane shows hello **running status of all hello vertices**.</span></span>
  
![Vista de ejecución de vértices de Data Lake Analytics Tools](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-vertex-execution-view-pane3.png)

<span data-ttu-id="ed96f-123">panel de Hello inferior central muestra información sobre cada vértice:</span><span class="sxs-lookup"><span data-stu-id="ed96f-123">hello bottom center pane shows information about each vertex:</span></span>
* <span data-ttu-id="ed96f-124">Nombre del proceso: nombre de Hola de instancia de vértices Hola.</span><span class="sxs-lookup"><span data-stu-id="ed96f-124">Process Name: hello name of hello vertex instance.</span></span> <span data-ttu-id="ed96f-125">Se compone de distintas partes de StageName|VertexName|VertexRunInstance.</span><span class="sxs-lookup"><span data-stu-id="ed96f-125">It is composed of different parts in StageName|VertexName|VertexRunInstance.</span></span> <span data-ttu-id="ed96f-126">Por ejemplo, vértices de hello SV7_Split .v1 [62] significa Hola segunda instancia en ejecución (.v1, índice que empieza por 0) del número de vértices 62 en fase SV7_Split.</span><span class="sxs-lookup"><span data-stu-id="ed96f-126">For example, hello SV7_Split[62].v1 vertex stands for hello second running instance (.v1, index starting from 0) of Vertex number 62 in Stage SV7_Split.</span></span>
* <span data-ttu-id="ed96f-127">Lectura de datos total/escrito: datos de hello estaban leídos/escritos por este vértice.</span><span class="sxs-lookup"><span data-stu-id="ed96f-127">Total Data Read/Written: hello data was read/written by this vertex.</span></span>
* <span data-ttu-id="ed96f-128">Estado de estado y de salida: Hola estado final cuando finaliza el vértice de Hola.</span><span class="sxs-lookup"><span data-stu-id="ed96f-128">State/Exit Status: hello final status when hello vertex is ended.</span></span>
* <span data-ttu-id="ed96f-129">Tipo de código o con errores de salida: error de Hola cuando vértices Hola produce un error.</span><span class="sxs-lookup"><span data-stu-id="ed96f-129">Exit Code/Failure Type: hello error when hello vertex failed.</span></span>
* <span data-ttu-id="ed96f-130">Motivo de creación: ¿Por qué vértices Hola se crean.</span><span class="sxs-lookup"><span data-stu-id="ed96f-130">Creation Reason: Why hello vertex was created.</span></span>
* <span data-ttu-id="ed96f-131">Latencia de la cola de latencia/PN de recursos latencia o proceso: Hola tiempo de hello vértices toowait para los recursos, datos de tooprocess y toostay en cola Hola.</span><span class="sxs-lookup"><span data-stu-id="ed96f-131">Resource Latency/Process Latency/PN Queue Latency: hello time taken for hello vertex toowait for resources, tooprocess data, and toostay in hello queue.</span></span>
* <span data-ttu-id="ed96f-132">GUID de proceso/creador: El GUID de vértice de ejecución actual de Hola o su autor.</span><span class="sxs-lookup"><span data-stu-id="ed96f-132">Process/Creator GUID: GUID for hello current running vertex or its creator.</span></span>
* <span data-ttu-id="ed96f-133">Versión: una instancia Hola N-ésimo de hello ejecutando vértices (sistema de hello puede programar nuevas instancias de un vértice por diversos motivos, por ejemplo, conmutación por error, de proceso redundancia, etcetera).</span><span class="sxs-lookup"><span data-stu-id="ed96f-133">Version: hello N-th instance of hello running vertex (hello system might schedule new instances of a vertex for many reasons, for example failover, compute redundancy, etc.)</span></span>
* <span data-ttu-id="ed96f-134">Hora de creación de la versión</span><span class="sxs-lookup"><span data-stu-id="ed96f-134">Version Created Time.</span></span>
* <span data-ttu-id="ed96f-135">Crear inicio tiempo o proceso en cola tiempo o proceso inicio tiempo o proceso completado de procesar tiempo: cuando inicia el proceso de vértices Hola creación; proceso de vértices de hello cuando inicia tooqueue; Hola cuando cierta vértices proceso comienza; Cuando Hola vértices se ha completado.</span><span class="sxs-lookup"><span data-stu-id="ed96f-135">Process Create Start Time/Process Queued Time/Process Start Time/Process Complete Time: when hello vertex process starts creation; when hello vertex process starts tooqueue; when hello certain vertex process starts; when hello certain vertex is completed.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ed96f-136">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ed96f-136">Next steps</span></span>
* <span data-ttu-id="ed96f-137">información de diagnóstico de toolog, consulte [acceso a registros de diagnóstico para el análisis de Azure Data Lake](data-lake-analytics-diagnostic-logs.md)</span><span class="sxs-lookup"><span data-stu-id="ed96f-137">toolog diagnostics information, see [Accessing diagnostics logs for Azure Data Lake Analytics](data-lake-analytics-diagnostic-logs.md)</span></span>
* <span data-ttu-id="ed96f-138">toosee una consulta más compleja, vea [sitio Web de analizar registros con análisis de Azure Data Lake](data-lake-analytics-analyze-weblogs.md).</span><span class="sxs-lookup"><span data-stu-id="ed96f-138">toosee a more complex query, see [Analyze Website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
* <span data-ttu-id="ed96f-139">Detalles del trabajo tooview, consulte [trabajo utilizar un explorador y la vista de trabajos de trabajos de análisis de Azure Data lake](data-lake-analytics-data-lake-tools-view-jobs.md)</span><span class="sxs-lookup"><span data-stu-id="ed96f-139">tooview job details, see [Use Job Browser and Job View for Azure Data lake Analytics jobs](data-lake-analytics-data-lake-tools-view-jobs.md)</span></span>
