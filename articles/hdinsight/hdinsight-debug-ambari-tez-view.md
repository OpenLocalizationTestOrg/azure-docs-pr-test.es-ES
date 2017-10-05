---
title: Uso de la vista Tez de Ambari con HDInsight - Azure | Microsoft Docs
description: "Obtenga información sobre cómo usar la vista de Tez de Ambari para depurar trabajos de Tez en HDInsight."
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
ms.openlocfilehash: 65d89309b9eea8544b85d16687baa90d49688d77
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="use-ambari-views-to-debug-tez-jobs-on-hdinsight"></a><span data-ttu-id="4ccc7-103">Usar vistas de Ambari para depurar trabajos de Tez en HDInsight</span><span class="sxs-lookup"><span data-stu-id="4ccc7-103">Use Ambari Views to debug Tez Jobs on HDInsight</span></span>

<span data-ttu-id="4ccc7-104">La interfaz de usuario de Ambari Web para HDInsight contiene una vista de Tez que puede usarse para comprender y depurar los trabajos que utilizan Tez.</span><span class="sxs-lookup"><span data-stu-id="4ccc7-104">The Ambari Web UI for HDInsight contains a Tez view that can be used to understand and debug jobs that use Tez.</span></span> <span data-ttu-id="4ccc7-105">La vista de Tez permite visualizar el trabajo como un gráfico de elementos conectados, profundizar en cada elemento y recuperar las estadísticas y la información de registro.</span><span class="sxs-lookup"><span data-stu-id="4ccc7-105">The Tez view allows you to visualize the job as a graph of connected items, drill into each item, and retrieve statistics and logging information.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4ccc7-106">Para realizar los pasos que se describen en este documento se requiere un clúster de HDInsight que use Linux.</span><span class="sxs-lookup"><span data-stu-id="4ccc7-106">The steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="4ccc7-107">Linux es el único sistema operativo que se usa en la versión 3.4 de HDInsight, o en las superiores.</span><span class="sxs-lookup"><span data-stu-id="4ccc7-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="4ccc7-108">Para obtener más información, consulte el artículo relativo al [control de versiones de componentes de HDInsight](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="4ccc7-108">For more information, see [HDInsight component versioning](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4ccc7-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="4ccc7-109">Prerequisites</span></span>

* <span data-ttu-id="4ccc7-110">Un clúster de HDInsight basado en Linux</span><span class="sxs-lookup"><span data-stu-id="4ccc7-110">A Linux-based HDInsight cluster.</span></span> <span data-ttu-id="4ccc7-111">Para conocer la forma de crear un clúster, consulte el [artículo de introducción al uso de HDInsight basado en Linux](hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="4ccc7-111">For steps on creating a cluster, see [Get started using Linux-based HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>
* <span data-ttu-id="4ccc7-112">Un explorador web moderno que sea compatible con HTML5.</span><span class="sxs-lookup"><span data-stu-id="4ccc7-112">A modern web browser that supports HTML5.</span></span>

## <a name="understanding-tez"></a><span data-ttu-id="4ccc7-113">Descripción de Tez</span><span class="sxs-lookup"><span data-stu-id="4ccc7-113">Understanding Tez</span></span>

<span data-ttu-id="4ccc7-114">Tez es un marco de trabajo extensible para el procesamiento de datos en Hadoop que proporciona una mayor velocidad que el procesamiento tradicional de MapReduce.</span><span class="sxs-lookup"><span data-stu-id="4ccc7-114">Tez is an extensible framework for data processing in Hadoop that provides greater speeds than traditional MapReduce processing.</span></span> <span data-ttu-id="4ccc7-115">Para los clústeres de HDInsight basados en Linux, es el motor predeterminado de Hive.</span><span class="sxs-lookup"><span data-stu-id="4ccc7-115">For Linux-based HDInsight clusters, it is the default engine for Hive.</span></span>

<span data-ttu-id="4ccc7-116">Tez crea un grafo acíclico dirigido (DAG) que describe el orden de las acciones que requieren los trabajos.</span><span class="sxs-lookup"><span data-stu-id="4ccc7-116">Tez creates a Directed Acyclic Graph (DAG) that describes the order of actions required by jobs.</span></span> <span data-ttu-id="4ccc7-117">Las acciones individuales se denominan vértices y ejecutan una parte del trabajo total.</span><span class="sxs-lookup"><span data-stu-id="4ccc7-117">Individual actions are called vertices, and execute a piece of the overall job.</span></span> <span data-ttu-id="4ccc7-118">La ejecución real del trabajo descrito por un vértice se denomina tarea, y puede distribuirse por varios nodos del clúster.</span><span class="sxs-lookup"><span data-stu-id="4ccc7-118">The actual execution of the work described by a vertex is called a task, and may be distributed across multiple nodes in the cluster.</span></span>

### <a name="understanding-the-tez-view"></a><span data-ttu-id="4ccc7-119">Descripción de la vista de Tez</span><span class="sxs-lookup"><span data-stu-id="4ccc7-119">Understanding the Tez view</span></span>

<span data-ttu-id="4ccc7-120">La vista de Tez proporciona información histórica y datos sobre los procesos que se están ejecutando.</span><span class="sxs-lookup"><span data-stu-id="4ccc7-120">The Tez view provides both historical information and information on processes that are running.</span></span> <span data-ttu-id="4ccc7-121">Esta información muestra la distribución de un trabajo a través de los clústeres,</span><span class="sxs-lookup"><span data-stu-id="4ccc7-121">This information shows how a job is distributed across clusters.</span></span> <span data-ttu-id="4ccc7-122">así como los contadores que emplean las tareas y vértices, e información sobre errores en relación con el trabajo.</span><span class="sxs-lookup"><span data-stu-id="4ccc7-122">It also displays counters used by tasks and vertices, and error information related to the job.</span></span> <span data-ttu-id="4ccc7-123">Puede ofrecer información útil en los escenarios siguientes:</span><span class="sxs-lookup"><span data-stu-id="4ccc7-123">It may offer useful information in the following scenarios:</span></span>

* <span data-ttu-id="4ccc7-124">Supervisión de procesos de ejecución prolongada, visualización del progreso de asignación y reducción de las tareas.</span><span class="sxs-lookup"><span data-stu-id="4ccc7-124">Monitoring long-running processes, viewing the progress of map and reduce tasks.</span></span>
* <span data-ttu-id="4ccc7-125">Análisis de datos históricos de procesos correctos o con errores para obtener información sobre cómo se puede mejorar el procesamiento o sobre la causa del error.</span><span class="sxs-lookup"><span data-stu-id="4ccc7-125">Analyzing historical data for successful or failed processes to learn how processing could be improved or why it failed.</span></span>

## <a name="generate-a-dag"></a><span data-ttu-id="4ccc7-126">Generar un DAG</span><span class="sxs-lookup"><span data-stu-id="4ccc7-126">Generate a DAG</span></span>

<span data-ttu-id="4ccc7-127">La vista de Tez solo contiene datos si se está ejecutando, o se ejecutó previamente, un trabajo que utiliza el motor de Tez.</span><span class="sxs-lookup"><span data-stu-id="4ccc7-127">The Tez view only contains data if a job that uses the Tez engine is currently running, or has been ran previously.</span></span> <span data-ttu-id="4ccc7-128">Las consultas simples de Hive pueden resolverse sin necesidad de usar Tez.</span><span class="sxs-lookup"><span data-stu-id="4ccc7-128">Simple Hive queries can be resolved without using Tez.</span></span> <span data-ttu-id="4ccc7-129">Para aquellas consultas más complejas que realizan filtrados, agrupaciones, ordenaciones, combinaciones, etc.,</span><span class="sxs-lookup"><span data-stu-id="4ccc7-129">More complex queries that do filtering, grouping, ordering, joins, etc.</span></span> <span data-ttu-id="4ccc7-130">sí se emplea el motor de Tez.</span><span class="sxs-lookup"><span data-stu-id="4ccc7-130">use the Tez engine.</span></span>

<span data-ttu-id="4ccc7-131">Siga estos pasos para ejecutar una consulta de Hive que utilice Tez:</span><span class="sxs-lookup"><span data-stu-id="4ccc7-131">Use the following steps to run a Hive query that uses Tez:</span></span>

1. <span data-ttu-id="4ccc7-132">En un explorador web, vaya a https://CLUSTERNAME.azurehdinsight.net, donde **CLUSTERNAME** es el nombre de su clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4ccc7-132">In a web browser, navigate to https://CLUSTERNAME.azurehdinsight.net, where **CLUSTERNAME** is the name of your HDInsight cluster.</span></span>

2. <span data-ttu-id="4ccc7-133">En el menú que aparece en la parte superior de la página, seleccione el icono **Vistas**.</span><span class="sxs-lookup"><span data-stu-id="4ccc7-133">From the menu at the top of the page, select the **Views** icon.</span></span> <span data-ttu-id="4ccc7-134">Este icono tiene el aspecto de un conjunto de cuadrados.</span><span class="sxs-lookup"><span data-stu-id="4ccc7-134">This icon looks like a series of squares.</span></span> <span data-ttu-id="4ccc7-135">En la lista desplegable que aparece, seleccione **Vista de Hive**.</span><span class="sxs-lookup"><span data-stu-id="4ccc7-135">In the dropdown that appears, select **Hive view**.</span></span>

    ![Seleccionar la vista de Hive](./media/hdinsight-debug-ambari-tez-view/selecthive.png)

3. <span data-ttu-id="4ccc7-137">Cuando se cargue la vista de Hive, pegue la siguiente consulta en el Editor de consultas y, a continuación, haga clic en **Ejecutar**.</span><span class="sxs-lookup"><span data-stu-id="4ccc7-137">When the Hive view loads, paste the following query into the Query Editor, and then click **execute**.</span></span>

        select market, state, country from hivesampletable where deviceplatform='Android' group by market, country, state;

    <span data-ttu-id="4ccc7-138">Cuando se haya completado el trabajo, debería ver el resultado en la sección **Resultados del proceso de consulta**.</span><span class="sxs-lookup"><span data-stu-id="4ccc7-138">Once the job has completed, you should see the output displayed in the **Query Process Results** section.</span></span> <span data-ttu-id="4ccc7-139">Los resultados deberían asemejarse a este texto:</span><span class="sxs-lookup"><span data-stu-id="4ccc7-139">The results should be similar to the following text:</span></span>

        market  state       country
        en-GB   Hessen      Germany
        en-GB   Kingston    Jamaica

4. <span data-ttu-id="4ccc7-140">Seleccione la pestaña **Registro**.</span><span class="sxs-lookup"><span data-stu-id="4ccc7-140">Select the **Log** tab.</span></span> <span data-ttu-id="4ccc7-141">Verá información similar al texto siguiente:</span><span class="sxs-lookup"><span data-stu-id="4ccc7-141">You see information similar to the following text:</span></span>

        INFO : Session is already open
        INFO :

        INFO : Status: Running (Executing on YARN cluster with App id application_1454546500517_0063)

    <span data-ttu-id="4ccc7-142">Guarde el valor de **App id**, ya que se usará en la próxima sección.</span><span class="sxs-lookup"><span data-stu-id="4ccc7-142">Save the **App id** value, as this value is used in the next section.</span></span>

## <a name="use-the-tez-view"></a><span data-ttu-id="4ccc7-143">Usar la vista de Tez</span><span class="sxs-lookup"><span data-stu-id="4ccc7-143">Use the Tez View</span></span>

1. <span data-ttu-id="4ccc7-144">En el menú que aparece en la parte superior de la página, seleccione el icono **Vistas**.</span><span class="sxs-lookup"><span data-stu-id="4ccc7-144">From the menu at the top of the page, select the **Views** icon.</span></span> <span data-ttu-id="4ccc7-145">En la lista desplegable que aparece, seleccione **Vista de Tez**.</span><span class="sxs-lookup"><span data-stu-id="4ccc7-145">In the dropdown that appears, select **Tez view**.</span></span>

    ![Seleccionar la vista de Tez](./media/hdinsight-debug-ambari-tez-view/selecttez.png)

2. <span data-ttu-id="4ccc7-147">Cuando se cargue la vista de Tez, verá una lista de consultas de Hive que se están ejecutando o que se ejecutaron anteriormente en el clúster.</span><span class="sxs-lookup"><span data-stu-id="4ccc7-147">When the Tez view loads, you see a list of hive queries that are currently running, or have been ran on the cluster.</span></span>

    ![Todos los DAG](./media/hdinsight-debug-ambari-tez-view/tez-view-home.png)

3. <span data-ttu-id="4ccc7-149">Si solo tiene una entrada, será la de la consulta que ejecutó en la sección anterior.</span><span class="sxs-lookup"><span data-stu-id="4ccc7-149">If you have only one entry, it is for the query that you ran in the previous section.</span></span> <span data-ttu-id="4ccc7-150">Si tiene varias entradas, puede buscar mediante los campos de la parte superior de la página.</span><span class="sxs-lookup"><span data-stu-id="4ccc7-150">If you have multiple entries, you can search by using the fields at the top of the page.</span></span>

4. <span data-ttu-id="4ccc7-151">Seleccione el **Id. de consulta** para una consulta de Hive.</span><span class="sxs-lookup"><span data-stu-id="4ccc7-151">Select the **Query ID** for a Hive query.</span></span> <span data-ttu-id="4ccc7-152">Se muestra información sobre la consulta.</span><span class="sxs-lookup"><span data-stu-id="4ccc7-152">Information about the query is displayed.</span></span>

    ![Detalles del DAG](./media/hdinsight-debug-ambari-tez-view/query-details.png)

5. <span data-ttu-id="4ccc7-154">Las pestañas de esta página le permiten ver la información siguiente:</span><span class="sxs-lookup"><span data-stu-id="4ccc7-154">The tabs on this page allow you to view the following information:</span></span>

    * <span data-ttu-id="4ccc7-155">**Detalles de la consulta**: detalles sobre la consulta de Hive.</span><span class="sxs-lookup"><span data-stu-id="4ccc7-155">**Query Details**: Details about the Hive query.</span></span>
    * <span data-ttu-id="4ccc7-156">**Escala de tiempo**: información sobre cuánto tiempo ha tardado cada fase de procesamiento.</span><span class="sxs-lookup"><span data-stu-id="4ccc7-156">**Timeline**: Information about how long each stage of processing took.</span></span>
    * <span data-ttu-id="4ccc7-157">**Configuraciones**: la configuración usada para esta consulta.</span><span class="sxs-lookup"><span data-stu-id="4ccc7-157">**Configurations**: The configuration used for this query.</span></span>

    <span data-ttu-id="4ccc7-158">Desde __Detalles de la consulta__ puede usar los vínculos para buscar información sobre la __Aplicación__ o el __DAG__ para esta consulta.</span><span class="sxs-lookup"><span data-stu-id="4ccc7-158">From __Query Details__ you can use the links to find information about the __Application__ or the __DAG__ for this query.</span></span>
    
    * <span data-ttu-id="4ccc7-159">El vínculo __Aplicación__ muestra información sobre la aplicación de YARN para esta consulta.</span><span class="sxs-lookup"><span data-stu-id="4ccc7-159">The __Application__ link displays information about the YARN application for this query.</span></span> <span data-ttu-id="4ccc7-160">Desde aquí puede tener acceso a los registros de aplicaciones en YARN.</span><span class="sxs-lookup"><span data-stu-id="4ccc7-160">From here you can access the YARN application logs.</span></span>
    * <span data-ttu-id="4ccc7-161">El vínculo __DAG__ muestra información sobre el grafo acíclico dirigido para esta consulta.</span><span class="sxs-lookup"><span data-stu-id="4ccc7-161">The __DAG__ link displays information about the directed acyclic graph for this query.</span></span> <span data-ttu-id="4ccc7-162">Desde aquí puede ver una representación gráfica del DAG.</span><span class="sxs-lookup"><span data-stu-id="4ccc7-162">From here you can view a graphical representation of the DAG.</span></span> <span data-ttu-id="4ccc7-163">También puede encontrar información sobre los vértices en el DAG.</span><span class="sxs-lookup"><span data-stu-id="4ccc7-163">You can also find information on the vertices within the DAG.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4ccc7-164">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4ccc7-164">Next Steps</span></span>

<span data-ttu-id="4ccc7-165">Ahora que ha aprendido a usar la vista de Tez, obtenga más información sobre el [Uso de Hive en HDInsight](hdinsight-use-hive.md).</span><span class="sxs-lookup"><span data-stu-id="4ccc7-165">Now that you have learned how to use the Tez view, learn more about [Using Hive on HDInsight](hdinsight-use-hive.md).</span></span>

<span data-ttu-id="4ccc7-166">Para obtener información técnica más detallada sobre Tez, consulte la [página de Tez en Hortonworks](http://hortonworks.com/hadoop/tez/).</span><span class="sxs-lookup"><span data-stu-id="4ccc7-166">For more detailed technical information on Tez, see the [Tez page at Hortonworks](http://hortonworks.com/hadoop/tez/).</span></span>

<span data-ttu-id="4ccc7-167">Para obtener más información sobre el uso de Ambari con HDInsight, consulte [Administración de clústeres de HDInsight con la interfaz de usuario web de Ambari](hdinsight-hadoop-manage-ambari.md)</span><span class="sxs-lookup"><span data-stu-id="4ccc7-167">For more information on using Ambari with HDInsight, see [Manage HDInsight clusters using the Ambari Web UI](hdinsight-hadoop-manage-ambari.md)</span></span>
