---
title: aaaUse Ambari Tez vista con HDInsight - Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse hello Ambari Tez ver trabajos de Tez toodebug en HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 9c39ea56-670b-4699-aba0-0f64c261e411
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 5d61bd0403c98284c86982073af91468ae62ac60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-ambari-views-toodebug-tez-jobs-on-hdinsight"></a><span data-ttu-id="e2eeb-103">Usar vistas de Ambari toodebug Tez trabajos en HDInsight</span><span class="sxs-lookup"><span data-stu-id="e2eeb-103">Use Ambari Views toodebug Tez Jobs on HDInsight</span></span>

<span data-ttu-id="e2eeb-104">Hola Ambari Web UI para HDInsight contiene una vista de Tez que puede ser utilizados trabajos toounderstand y depuración que utilizan Tez.</span><span class="sxs-lookup"><span data-stu-id="e2eeb-104">hello Ambari Web UI for HDInsight contains a Tez view that can be used toounderstand and debug jobs that use Tez.</span></span> <span data-ttu-id="e2eeb-105">Hola Tez vista le permite toovisualize trabajo de hello, como un gráfico de elementos conectados, profundizar en cada elemento y recuperar las estadísticas y la información de registro.</span><span class="sxs-lookup"><span data-stu-id="e2eeb-105">hello Tez view allows you toovisualize hello job as a graph of connected items, drill into each item, and retrieve statistics and logging information.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e2eeb-106">pasos de Hello en este documento requieren un clúster de HDInsight que usa Linux.</span><span class="sxs-lookup"><span data-stu-id="e2eeb-106">hello steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="e2eeb-107">Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior.</span><span class="sxs-lookup"><span data-stu-id="e2eeb-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="e2eeb-108">Para obtener más información, consulte el artículo relativo al [control de versiones de componentes de HDInsight](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="e2eeb-108">For more information, see [HDInsight component versioning](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e2eeb-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="e2eeb-109">Prerequisites</span></span>

* <span data-ttu-id="e2eeb-110">Un clúster de HDInsight basado en Linux</span><span class="sxs-lookup"><span data-stu-id="e2eeb-110">A Linux-based HDInsight cluster.</span></span> <span data-ttu-id="e2eeb-111">Para conocer la forma de crear un clúster, consulte el [artículo de introducción al uso de HDInsight basado en Linux](hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="e2eeb-111">For steps on creating a cluster, see [Get started using Linux-based HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>
* <span data-ttu-id="e2eeb-112">Un explorador web moderno que sea compatible con HTML5.</span><span class="sxs-lookup"><span data-stu-id="e2eeb-112">A modern web browser that supports HTML5.</span></span>

## <a name="understanding-tez"></a><span data-ttu-id="e2eeb-113">Descripción de Tez</span><span class="sxs-lookup"><span data-stu-id="e2eeb-113">Understanding Tez</span></span>

<span data-ttu-id="e2eeb-114">Tez es un marco de trabajo extensible para el procesamiento de datos en Hadoop que proporciona una mayor velocidad que el procesamiento tradicional de MapReduce.</span><span class="sxs-lookup"><span data-stu-id="e2eeb-114">Tez is an extensible framework for data processing in Hadoop that provides greater speeds than traditional MapReduce processing.</span></span> <span data-ttu-id="e2eeb-115">Para los clústeres de HDInsight basados en Linux, es motor predeterminado de Hola de Hive.</span><span class="sxs-lookup"><span data-stu-id="e2eeb-115">For Linux-based HDInsight clusters, it is hello default engine for Hive.</span></span>

<span data-ttu-id="e2eeb-116">Tez crea un dirigen acíclico gráfico (DAG) que describe el orden de Hola de acciones requeridas por los trabajos.</span><span class="sxs-lookup"><span data-stu-id="e2eeb-116">Tez creates a Directed Acyclic Graph (DAG) that describes hello order of actions required by jobs.</span></span> <span data-ttu-id="e2eeb-117">Acciones individuales se denominan vértices y ejecutar una parte del programa Hola trabajo completo.</span><span class="sxs-lookup"><span data-stu-id="e2eeb-117">Individual actions are called vertices, and execute a piece of hello overall job.</span></span> <span data-ttu-id="e2eeb-118">ejecución real de Hola de trabajo de hello descrita por un vértice se denomina una tarea y se puede distribuir en varios nodos de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="e2eeb-118">hello actual execution of hello work described by a vertex is called a task, and may be distributed across multiple nodes in hello cluster.</span></span>

### <a name="understanding-hello-tez-view"></a><span data-ttu-id="e2eeb-119">Hola descripción Tez vista</span><span class="sxs-lookup"><span data-stu-id="e2eeb-119">Understanding hello Tez view</span></span>

<span data-ttu-id="e2eeb-120">Hola Tez vista proporciona información histórica y obtener información acerca de procesos que se ejecutan.</span><span class="sxs-lookup"><span data-stu-id="e2eeb-120">hello Tez view provides both historical information and information on processes that are running.</span></span> <span data-ttu-id="e2eeb-121">Esta información muestra la distribución de un trabajo a través de los clústeres,</span><span class="sxs-lookup"><span data-stu-id="e2eeb-121">This information shows how a job is distributed across clusters.</span></span> <span data-ttu-id="e2eeb-122">También muestra los contadores que se usan las tareas y los vértices y toohello trabajos relacionados con la información de error.</span><span class="sxs-lookup"><span data-stu-id="e2eeb-122">It also displays counters used by tasks and vertices, and error information related toohello job.</span></span> <span data-ttu-id="e2eeb-123">Puede ofrecer información útil en hello los escenarios siguientes:</span><span class="sxs-lookup"><span data-stu-id="e2eeb-123">It may offer useful information in hello following scenarios:</span></span>

* <span data-ttu-id="e2eeb-124">Supervisión de los procesos de larga ejecución, ver progreso de asignación de Hola y reduzcan las tareas.</span><span class="sxs-lookup"><span data-stu-id="e2eeb-124">Monitoring long-running processes, viewing hello progress of map and reduce tasks.</span></span>
* <span data-ttu-id="e2eeb-125">Analizar datos históricos para procesos correctos o con error toolearn cómo se puede mejorar el procesamiento o por qué se produjo un error.</span><span class="sxs-lookup"><span data-stu-id="e2eeb-125">Analyzing historical data for successful or failed processes toolearn how processing could be improved or why it failed.</span></span>

## <a name="generate-a-dag"></a><span data-ttu-id="e2eeb-126">Generar un DAG</span><span class="sxs-lookup"><span data-stu-id="e2eeb-126">Generate a DAG</span></span>

<span data-ttu-id="e2eeb-127">Hola Tez vista solo contiene datos si un trabajo que utiliza Hola Tez motor está actualmente se está ejecutando o se ha ejecutado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="e2eeb-127">hello Tez view only contains data if a job that uses hello Tez engine is currently running, or has been ran previously.</span></span> <span data-ttu-id="e2eeb-128">Las consultas simples de Hive pueden resolverse sin necesidad de usar Tez.</span><span class="sxs-lookup"><span data-stu-id="e2eeb-128">Simple Hive queries can be resolved without using Tez.</span></span> <span data-ttu-id="e2eeb-129">Para aquellas consultas más complejas que realizan filtrados, agrupaciones, ordenaciones, combinaciones, etc.,</span><span class="sxs-lookup"><span data-stu-id="e2eeb-129">More complex queries that do filtering, grouping, ordering, joins, etc.</span></span> <span data-ttu-id="e2eeb-130">Use hello Tez motor.</span><span class="sxs-lookup"><span data-stu-id="e2eeb-130">use hello Tez engine.</span></span>

<span data-ttu-id="e2eeb-131">Usar hello siguiendo los pasos toorun una consulta de Hive que usa Tez:</span><span class="sxs-lookup"><span data-stu-id="e2eeb-131">Use hello following steps toorun a Hive query that uses Tez:</span></span>

1. <span data-ttu-id="e2eeb-132">En un explorador web, vaya toohttps://CLUSTERNAME.azurehdinsight.net, donde **CLUSTERNAME** es Hola nombre de su clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e2eeb-132">In a web browser, navigate toohttps://CLUSTERNAME.azurehdinsight.net, where **CLUSTERNAME** is hello name of your HDInsight cluster.</span></span>

2. <span data-ttu-id="e2eeb-133">En menú de hello al principio de Hola de página de hello, seleccione hello **vistas** icono.</span><span class="sxs-lookup"><span data-stu-id="e2eeb-133">From hello menu at hello top of hello page, select hello **Views** icon.</span></span> <span data-ttu-id="e2eeb-134">Este icono tiene el aspecto de un conjunto de cuadrados.</span><span class="sxs-lookup"><span data-stu-id="e2eeb-134">This icon looks like a series of squares.</span></span> <span data-ttu-id="e2eeb-135">En la lista desplegable de Hola que aparece, seleccione **Hive vista**.</span><span class="sxs-lookup"><span data-stu-id="e2eeb-135">In hello dropdown that appears, select **Hive view**.</span></span>

    ![Seleccionar la vista de Hive](./media/hdinsight-debug-ambari-tez-view/selecthive.png)

3. <span data-ttu-id="e2eeb-137">Cuando se carga Hola vista Hive, siguiente de hello pegar consultas en el Editor de consultas de hello y, a continuación, haga clic en **ejecutar**.</span><span class="sxs-lookup"><span data-stu-id="e2eeb-137">When hello Hive view loads, paste hello following query into hello Query Editor, and then click **execute**.</span></span>

        select market, state, country from hivesampletable where deviceplatform='Android' group by market, country, state;

    <span data-ttu-id="e2eeb-138">Cuando haya completado el trabajo de hello, debería ver el resultado de hello muestra de Hola **resultados del proceso de consulta** sección.</span><span class="sxs-lookup"><span data-stu-id="e2eeb-138">Once hello job has completed, you should see hello output displayed in hello **Query Process Results** section.</span></span> <span data-ttu-id="e2eeb-139">resultados de Hello deberían ser similar toohello siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="e2eeb-139">hello results should be similar toohello following text:</span></span>

        market  state       country
        en-GB   Hessen      Germany
        en-GB   Kingston    Jamaica

4. <span data-ttu-id="e2eeb-140">Seleccione hello **registro** ficha. Vea información toohello similar siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="e2eeb-140">Select hello **Log** tab. You see information similar toohello following text:</span></span>

        INFO : Session is already open
        INFO :

        INFO : Status: Running (Executing on YARN cluster with App id application_1454546500517_0063)

    <span data-ttu-id="e2eeb-141">Guardar hello **Id. de aplicación** valor, tal como este valor se utiliza en la sección siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="e2eeb-141">Save hello **App id** value, as this value is used in hello next section.</span></span>

## <a name="use-hello-tez-view"></a><span data-ttu-id="e2eeb-142">Usar hello Tez vista</span><span class="sxs-lookup"><span data-stu-id="e2eeb-142">Use hello Tez View</span></span>

1. <span data-ttu-id="e2eeb-143">En menú de hello al principio de Hola de página de hello, seleccione hello **vistas** icono.</span><span class="sxs-lookup"><span data-stu-id="e2eeb-143">From hello menu at hello top of hello page, select hello **Views** icon.</span></span> <span data-ttu-id="e2eeb-144">En la lista desplegable de Hola que aparece, seleccione **Tez vista**.</span><span class="sxs-lookup"><span data-stu-id="e2eeb-144">In hello dropdown that appears, select **Tez view**.</span></span>

    ![Seleccionar la vista de Tez](./media/hdinsight-debug-ambari-tez-view/selecttez.png)

2. <span data-ttu-id="e2eeb-146">Cuando se cargue hello Tez vista, verá una lista de consultas de hive que se están ejecutando actualmente, o bien haber ejecutado en clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="e2eeb-146">When hello Tez view loads, you see a list of hive queries that are currently running, or have been ran on hello cluster.</span></span>

    ![Todos los DAG](./media/hdinsight-debug-ambari-tez-view/tez-view-home.png)

3. <span data-ttu-id="e2eeb-148">Si tiene sólo una entrada, es de consulta de Hola que se ejecutó en la sección anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="e2eeb-148">If you have only one entry, it is for hello query that you ran in hello previous section.</span></span> <span data-ttu-id="e2eeb-149">Si tiene varias entradas, puede buscar mediante campos hello en parte superior de Hola de página Hola.</span><span class="sxs-lookup"><span data-stu-id="e2eeb-149">If you have multiple entries, you can search by using hello fields at hello top of hello page.</span></span>

4. <span data-ttu-id="e2eeb-150">Seleccione hello **identificador de la consulta** para una consulta de Hive.</span><span class="sxs-lookup"><span data-stu-id="e2eeb-150">Select hello **Query ID** for a Hive query.</span></span> <span data-ttu-id="e2eeb-151">Se muestra información sobre la consulta de Hola.</span><span class="sxs-lookup"><span data-stu-id="e2eeb-151">Information about hello query is displayed.</span></span>

    ![Detalles del DAG](./media/hdinsight-debug-ambari-tez-view/query-details.png)

5. <span data-ttu-id="e2eeb-153">pestañas de Hello en esta página le permiten hello tooview siguiente información:</span><span class="sxs-lookup"><span data-stu-id="e2eeb-153">hello tabs on this page allow you tooview hello following information:</span></span>

    * <span data-ttu-id="e2eeb-154">**Detalles de la consulta**: obtener detalles acerca de la consulta de Hive Hola.</span><span class="sxs-lookup"><span data-stu-id="e2eeb-154">**Query Details**: Details about hello Hive query.</span></span>
    * <span data-ttu-id="e2eeb-155">**Escala de tiempo**: información sobre cuánto tiempo ha tardado cada fase de procesamiento.</span><span class="sxs-lookup"><span data-stu-id="e2eeb-155">**Timeline**: Information about how long each stage of processing took.</span></span>
    * <span data-ttu-id="e2eeb-156">**Las configuraciones de**: configuración de hello utilizado para esta consulta.</span><span class="sxs-lookup"><span data-stu-id="e2eeb-156">**Configurations**: hello configuration used for this query.</span></span>

    <span data-ttu-id="e2eeb-157">De __detalles de la consulta__ puede utilizar Hola vínculos toofind información acerca de hello __aplicación__ o hello __DAG__ para esta consulta.</span><span class="sxs-lookup"><span data-stu-id="e2eeb-157">From __Query Details__ you can use hello links toofind information about hello __Application__ or hello __DAG__ for this query.</span></span>
    
    * <span data-ttu-id="e2eeb-158">Hola __aplicación__ vínculo muestra información acerca de hello aplicación YARN para esta consulta.</span><span class="sxs-lookup"><span data-stu-id="e2eeb-158">hello __Application__ link displays information about hello YARN application for this query.</span></span> <span data-ttu-id="e2eeb-159">Desde aquí puede tener acceso a registros de la aplicación hello YARN.</span><span class="sxs-lookup"><span data-stu-id="e2eeb-159">From here you can access hello YARN application logs.</span></span>
    * <span data-ttu-id="e2eeb-160">Hola __DAG__ vínculo muestra información acerca de gráfico acíclico dirigido Hola para esta consulta.</span><span class="sxs-lookup"><span data-stu-id="e2eeb-160">hello __DAG__ link displays information about hello directed acyclic graph for this query.</span></span> <span data-ttu-id="e2eeb-161">Desde aquí puede ver una representación gráfica de hello DAG.</span><span class="sxs-lookup"><span data-stu-id="e2eeb-161">From here you can view a graphical representation of hello DAG.</span></span> <span data-ttu-id="e2eeb-162">También puede encontrar información sobre los vértices de hello en hello DAG.</span><span class="sxs-lookup"><span data-stu-id="e2eeb-162">You can also find information on hello vertices within hello DAG.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e2eeb-163">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e2eeb-163">Next Steps</span></span>

<span data-ttu-id="e2eeb-164">Ahora que ha aprendido cómo ver hello toouse Tez, obtenga más información sobre [utilizando Hive en HDInsight](hdinsight-use-hive.md).</span><span class="sxs-lookup"><span data-stu-id="e2eeb-164">Now that you have learned how toouse hello Tez view, learn more about [Using Hive on HDInsight](hdinsight-use-hive.md).</span></span>

<span data-ttu-id="e2eeb-165">Para obtener más información técnica sobre Tez, consulte hello [Tez página en Hortonworks](http://hortonworks.com/hadoop/tez/).</span><span class="sxs-lookup"><span data-stu-id="e2eeb-165">For more detailed technical information on Tez, see hello [Tez page at Hortonworks](http://hortonworks.com/hadoop/tez/).</span></span>

<span data-ttu-id="e2eeb-166">Para obtener más información sobre el uso de Ambari con HDInsight, vea [administrar clústeres de HDInsight con hello Ambari Web UI](hdinsight-hadoop-manage-ambari.md)</span><span class="sxs-lookup"><span data-stu-id="e2eeb-166">For more information on using Ambari with HDInsight, see [Manage HDInsight clusters using hello Ambari Web UI](hdinsight-hadoop-manage-ambari.md)</span></span>
