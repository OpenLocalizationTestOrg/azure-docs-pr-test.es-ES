---
title: "aaaDebug Apache Spark trabajos se están ejecutando en HDInsight de Azure | Documentos de Microsoft"
description: "Usar la interfaz de usuario de hilo, interfaz de usuario de Spark e historial de Spark server tootrack y depuración trabajos que se ejecutan en un clúster de Spark en HDInsight de Azure"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 59af05a7-2bd9-44b0-b55f-2438d294198b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: nitinme
ms.openlocfilehash: 33d352a5773920735aa4e5e8532b78122f381377
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="debug-apache-spark-jobs-running-on-azure-hdinsight"></a><span data-ttu-id="9434e-103">Depuración de trabajos de Apache Spark que se ejecutan en Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="9434e-103">Debug Apache Spark jobs running on Azure HDInsight</span></span>

<span data-ttu-id="9434e-104">En este artículo, aprenderá cómo tootrack y depuración inspirará trabajos que se ejecutan en clústeres de HDInsight con hello YARN de interfaz de usuario, interfaz de usuario de Spark y Hola Spark historial de servidor.</span><span class="sxs-lookup"><span data-stu-id="9434e-104">In this article you will learn how tootrack and debug Spark jobs running on HDInsight clusters using hello YARN UI, Spark UI, and hello Spark History Server.</span></span> <span data-ttu-id="9434e-105">En este artículo, se iniciará un trabajo de Spark utilizando un bloc de notas disponible con clúster de Spark hello, **aprendizaje automático: análisis predictivos en datos de la inspección de alimentos mediante MLLib**.</span><span class="sxs-lookup"><span data-stu-id="9434e-105">For this article, we will start a Spark job using a notebook available with hello Spark cluster, **Machine learning: Predictive analysis on food inspection data using MLLib**.</span></span> <span data-ttu-id="9434e-106">Puede usar estos pasos hello tootrack una aplicación que envió utilizando cualquier otro enfoque así, por ejemplo, **spark-submit**.</span><span class="sxs-lookup"><span data-stu-id="9434e-106">You can use hello steps below tootrack an application that you submitted using any other approach as well, for example, **spark-submit**.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9434e-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="9434e-107">Prerequisites</span></span>
<span data-ttu-id="9434e-108">Debe disponer de hello siguiente:</span><span class="sxs-lookup"><span data-stu-id="9434e-108">You must have hello following:</span></span>

* <span data-ttu-id="9434e-109">Una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="9434e-109">An Azure subscription.</span></span> <span data-ttu-id="9434e-110">Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="9434e-110">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="9434e-111">Un clúster de Apache Spark en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9434e-111">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="9434e-112">Para obtener instrucciones, vea [Creación de clústeres Apache Spark en HDInsight de Azure](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="9434e-112">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>
* <span data-ttu-id="9434e-113">Debería haberse iniciado ejecutando Bloc de notas de hello,  **[aprendizaje automático: análisis predictivos en datos de la inspección de alimentos con MLLib](hdinsight-apache-spark-machine-learning-mllib-ipython.md)**.</span><span class="sxs-lookup"><span data-stu-id="9434e-113">You should have started running hello notebook, **[Machine learning: Predictive analysis on food inspection data using MLLib](hdinsight-apache-spark-machine-learning-mllib-ipython.md)**.</span></span> <span data-ttu-id="9434e-114">Para obtener instrucciones sobre cómo toorun este bloc de notas, siga Hola vínculo.</span><span class="sxs-lookup"><span data-stu-id="9434e-114">For instructions on how toorun this notebook, follow hello link.</span></span>  

## <a name="track-an-application-in-hello-yarn-ui"></a><span data-ttu-id="9434e-115">Realizar un seguimiento de una aplicación Hola interfaz de usuario de hilo</span><span class="sxs-lookup"><span data-stu-id="9434e-115">Track an application in hello YARN UI</span></span>
1. <span data-ttu-id="9434e-116">Inicie hello YARN interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="9434e-116">Launch hello YARN UI.</span></span> <span data-ttu-id="9434e-117">En la hoja de clúster de hello, haga clic en **panel clúster**y, a continuación, haga clic en **YARN**.</span><span class="sxs-lookup"><span data-stu-id="9434e-117">From hello cluster blade, click **Cluster Dashboard**, and then click **YARN**.</span></span>
   
    ![Iniciar interfaz de usuario de YARN](./media/hdinsight-apache-spark-job-debugging/launch-yarn-ui.png)
   
   > [!TIP]
   > <span data-ttu-id="9434e-119">Como alternativa, también puede iniciar hello YARN UI de hello Ambari UI.</span><span class="sxs-lookup"><span data-stu-id="9434e-119">Alternatively, you can also launch hello YARN UI from hello Ambari UI.</span></span> <span data-ttu-id="9434e-120">Hola toolaunch Ambari UI, desde la hoja de clúster de hello, haga clic en **panel clúster**y, a continuación, haga clic en **panel de clúster de HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="9434e-120">toolaunch hello Ambari UI, from hello cluster blade, click **Cluster Dashboard**, and then click **HDInsight Cluster Dashboard**.</span></span> <span data-ttu-id="9434e-121">En hello Ambari UI, haga clic en **YARN**, haga clic en **vínculos rápidos**, haga clic en Administrador de recursos activos de hello y, a continuación, haga clic en **ResourceManager UI**.</span><span class="sxs-lookup"><span data-stu-id="9434e-121">From hello Ambari UI, click **YARN**, click **Quick Links**, click hello active resource manager, and then click **ResourceManager UI**.</span></span>    
   > 
   > 
2. <span data-ttu-id="9434e-122">Dado que se inició el trabajo de Spark de hello mediante Jupyter blocs de notas, aplicación hello tiene el nombre de hello **remotesparkmagics** (es decir, nombre de Hola para todas las aplicaciones que se inician desde blocs de notas de hello).</span><span class="sxs-lookup"><span data-stu-id="9434e-122">Because you started hello Spark job using Jupyter notebooks, hello application has hello name **remotesparkmagics** (this is hello name for all applications that are started from hello notebooks).</span></span> <span data-ttu-id="9434e-123">Haga clic en Id. de aplicación Hola contra Hola aplicación nombre tooget obtener más información sobre el trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="9434e-123">Click hello application ID against hello application name tooget more information about hello job.</span></span> <span data-ttu-id="9434e-124">Se abre la vista de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="9434e-124">This launches hello application view.</span></span>
   
    ![Buscar identificador de aplicación Spark](./media/hdinsight-apache-spark-job-debugging/find-application-id.png)
   
    <span data-ttu-id="9434e-126">Para estas aplicaciones que se inicien desde blocs de notas de hello Jupyter, estado de hello es siempre **EJECUTANDO** hasta que salga de Bloc de notas de Hola.</span><span class="sxs-lookup"><span data-stu-id="9434e-126">For such applications that are launched from hello Jupyter notebooks, hello status is always **RUNNING** until you exit hello notebook.</span></span>
3. <span data-ttu-id="9434e-127">Hola desde vista de aplicación, puede explorar en profundidad más toofind contenedores Hola asociados con la aplicación hello y registros de hello (stdout y stderr).</span><span class="sxs-lookup"><span data-stu-id="9434e-127">From hello application view, you can drill down further toofind out hello containers associated with hello application and hello logs (stdout/stderr).</span></span> <span data-ttu-id="9434e-128">También puede iniciar Hola Spark UI haciendo clic en hello vinculación correspondiente toohello **dirección URL de seguimiento**, tal y como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="9434e-128">You can also launch hello Spark UI by clicking hello linking corresponding toohello **Tracking URL**, as shown below.</span></span> 
   
    ![Descargar registros de contenedor](./media/hdinsight-apache-spark-job-debugging/download-container-logs.png)

## <a name="track-an-application-in-hello-spark-ui"></a><span data-ttu-id="9434e-130">Realizar un seguimiento de una aplicación Hola Spark UI</span><span class="sxs-lookup"><span data-stu-id="9434e-130">Track an application in hello Spark UI</span></span>
<span data-ttu-id="9434e-131">Hola Spark interfaz de usuario, puede profundizar en los trabajos de Spark Hola que son generados por la aplicación hello que inició anteriormente.</span><span class="sxs-lookup"><span data-stu-id="9434e-131">In hello Spark UI, you can drill down into hello Spark jobs that are spawned by hello application you started earlier.</span></span>

1. <span data-ttu-id="9434e-132">Hola toolaunch Spark de interfaz de usuario, desde la vista de la aplicación hello, haga clic en vínculo Hola contra Hola **dirección URL de seguimiento**, tal y como se muestra en la captura de pantalla de hello anterior.</span><span class="sxs-lookup"><span data-stu-id="9434e-132">toolaunch hello Spark UI, from hello application view, click hello link against hello **Tracking URL**, as shown in hello screen capture above.</span></span> <span data-ttu-id="9434e-133">Puede ver todos los trabajos de Spark Hola iniciados por aplicación Hola que se ejecuta en el Bloc de notas de hello Jupyter.</span><span class="sxs-lookup"><span data-stu-id="9434e-133">You can see all hello Spark jobs that are launched by hello application running in hello Jupyter notebook.</span></span>
   
    ![Ver trabajos de Spark](./media/hdinsight-apache-spark-job-debugging/view-spark-jobs.png)
2. <span data-ttu-id="9434e-135">Haga clic en hello **ejecutor** toosee información de procesamiento y almacenamiento para cada elemento de ejecución de la ficha.</span><span class="sxs-lookup"><span data-stu-id="9434e-135">Click hello **Executors** tab toosee processing and storage information for each executor.</span></span> <span data-ttu-id="9434e-136">También puede recuperar la pila de llamadas de hello haciendo clic en hello **subprocesos volcar** vínculo.</span><span class="sxs-lookup"><span data-stu-id="9434e-136">You can also retrieve hello call stack by clicking on hello **Thread Dump** link.</span></span>
   
    ![Ver ejecutores de Spark](./media/hdinsight-apache-spark-job-debugging/view-spark-executors.png)
3. <span data-ttu-id="9434e-138">Haga clic en hello **fases** ficha fases de hello toosee asociados a la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="9434e-138">Click hello **Stages** tab toosee hello stages associated with hello application.</span></span>
   
    ![Ver fases de Spark](./media/hdinsight-apache-spark-job-debugging/view-spark-stages.png)
   
    <span data-ttu-id="9434e-140">Cada fase puede tener varias tareas de las que puede ver las estadísticas de ejecución, como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="9434e-140">Each stage can have multiple tasks for which you can view execution statistics, like shown below.</span></span>
   
    ![Ver fases de Spark](./media/hdinsight-apache-spark-job-debugging/view-spark-stages-details.png) 
4. <span data-ttu-id="9434e-142">Desde la página de detalles de la fase de hello, puede iniciar la visualización de DAG.</span><span class="sxs-lookup"><span data-stu-id="9434e-142">From hello stage details page, you can launch DAG Visualization.</span></span> <span data-ttu-id="9434e-143">Expanda hello **DAG visualización** vincular al principio de Hola de página de hello, tal y como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="9434e-143">Expand hello **DAG Visualization** link at hello top of hello page, as shown below.</span></span>
   
    ![Ver visualización DAG de las fases de Spark](./media/hdinsight-apache-spark-job-debugging/view-spark-stages-dag-visualization.png)
   
    <span data-ttu-id="9434e-145">DAG o un gráfico de Aclyic directo representa las distintas fases de hello en la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="9434e-145">DAG or Direct Aclyic Graph represents hello different stages in hello application.</span></span> <span data-ttu-id="9434e-146">Cada cuadro azul en el gráfico de hello representa una operación de Spark invocada desde aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="9434e-146">Each blue box in hello graph represents a Spark operation invoked from hello application.</span></span>
5. <span data-ttu-id="9434e-147">Desde la página de detalles de la fase de hello, también puede iniciar la vista de escala de tiempo de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="9434e-147">From hello stage details page, you can also launch hello application timeline view.</span></span> <span data-ttu-id="9434e-148">Expanda hello **escala de tiempo del evento** vincular al principio de Hola de página de hello, tal y como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="9434e-148">Expand hello **Event Timeline** link at hello top of hello page, as shown below.</span></span>
   
    ![Ver escala de tiempo de eventos de fases de Spark](./media/hdinsight-apache-spark-job-debugging/view-spark-stages-event-timeline.png)
   
    <span data-ttu-id="9434e-150">Esto muestra eventos de Spark hello en forma de Hola de una escala de tiempo.</span><span class="sxs-lookup"><span data-stu-id="9434e-150">This displays hello Spark events in hello form of a timeline.</span></span> <span data-ttu-id="9434e-151">vista de escala de tiempo de Hello está disponible en tres niveles, en los trabajos, en un trabajo y, en una fase.</span><span class="sxs-lookup"><span data-stu-id="9434e-151">hello timeline view is available at three levels, across jobs, within a job, and within a stage.</span></span> <span data-ttu-id="9434e-152">imagen de Hello anterior captura la vista de escala de tiempo de Hola para una determinada fase.</span><span class="sxs-lookup"><span data-stu-id="9434e-152">hello image above captures hello timeline view for a given stage.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="9434e-153">Si selecciona hello **habilitar Zoom** casilla de verificación, puede desplazarse a la izquierda y derecha en la vista de escala de tiempo de Hola.</span><span class="sxs-lookup"><span data-stu-id="9434e-153">If you select hello **Enable zooming** check box, you can scroll left and right across hello timeline view.</span></span>
   > 
   > 
6. <span data-ttu-id="9434e-154">Otras fichas de hello Spark UI proporcionan información útil acerca de la instancia de Spark Hola así.</span><span class="sxs-lookup"><span data-stu-id="9434e-154">Other tabs in hello Spark UI provide useful information about hello Spark instance as well.</span></span>
   
   * <span data-ttu-id="9434e-155">Pestaña de almacenamiento: si la aplicación crea un RDDs, puede encontrar información sobre los agentes en la pestaña de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="9434e-155">Storage tab - If your application creates an RDDs, you can find information about those in hello Storage tab.</span></span>
   * <span data-ttu-id="9434e-156">Ficha entorno - esta pestaña proporciona mucha información útil sobre la instancia de Spark como Hola</span><span class="sxs-lookup"><span data-stu-id="9434e-156">Environment tab - This tab provides a lot of useful information about your Spark instance such as hello</span></span> 
     * <span data-ttu-id="9434e-157">La versión de la escala</span><span class="sxs-lookup"><span data-stu-id="9434e-157">Scala version</span></span>
     * <span data-ttu-id="9434e-158">Directorio de registro de eventos asociado con el clúster de Hola</span><span class="sxs-lookup"><span data-stu-id="9434e-158">Event log directory associated with hello cluster</span></span>
     * <span data-ttu-id="9434e-159">Número de núcleos de ejecutor para la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="9434e-159">Number of executor cores for hello application</span></span>
     * <span data-ttu-id="9434e-160">Etc.</span><span class="sxs-lookup"><span data-stu-id="9434e-160">Etc.</span></span>

## <a name="find-information-about-completed-jobs-using-hello-spark-history-server"></a><span data-ttu-id="9434e-161">Buscar información acerca de los trabajos completados con hello Spark historial de servidor</span><span class="sxs-lookup"><span data-stu-id="9434e-161">Find information about completed jobs using hello Spark History Server</span></span>
<span data-ttu-id="9434e-162">Una vez que se completa un trabajo, información de hello sobre trabajo Hola se mantiene en hello Spark historial de servidor.</span><span class="sxs-lookup"><span data-stu-id="9434e-162">Once a job is completed, hello information about hello job is persisted in hello Spark History Server.</span></span>

1. <span data-ttu-id="9434e-163">Hola toolaunch Spark historial de servidor, de hoja de clúster de hello, haga clic en **panel clúster**y, a continuación, haga clic en **Spark historial Server**.</span><span class="sxs-lookup"><span data-stu-id="9434e-163">toolaunch hello Spark History Server, from hello cluster blade, click **Cluster Dashboard**, and then click **Spark History Server**.</span></span>
   
    ![Iniciar servidor de historial de Spark](./media/hdinsight-apache-spark-job-debugging/launch-spark-history-server.png)
   
   > [!TIP]
   > <span data-ttu-id="9434e-165">Como alternativa, también puede iniciar Hola interfaz de usuario del servidor de historial de Spark de hello Ambari UI.</span><span class="sxs-lookup"><span data-stu-id="9434e-165">Alternatively, you can also launch hello Spark History Server UI from hello Ambari UI.</span></span> <span data-ttu-id="9434e-166">Hola toolaunch Ambari UI, desde la hoja de clúster de hello, haga clic en **panel clúster**y, a continuación, haga clic en **panel de clúster de HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="9434e-166">toolaunch hello Ambari UI, from hello cluster blade, click **Cluster Dashboard**, and then click **HDInsight Cluster Dashboard**.</span></span> <span data-ttu-id="9434e-167">En hello Ambari UI, haga clic en **Spark**, haga clic en **vínculos rápidos**y, a continuación, haga clic en **interfaz de usuario del servidor de historial de Spark**.</span><span class="sxs-lookup"><span data-stu-id="9434e-167">From hello Ambari UI, click **Spark**, click **Quick Links**, and then click **Spark History Server UI**.</span></span>
   > 
   > 
2. <span data-ttu-id="9434e-168">Verá todas las aplicaciones de hello completado enumeradas.</span><span class="sxs-lookup"><span data-stu-id="9434e-168">You will see all hello completed applications listed.</span></span> <span data-ttu-id="9434e-169">Haga clic en un toodrill de Id. de aplicación hacia abajo en una aplicación para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="9434e-169">Click an application ID toodrill down into an application for more info.</span></span>
   
    ![Iniciar servidor de historial de Spark](./media/hdinsight-apache-spark-job-debugging/view-completed-applications.png)

## <a name="see-also"></a><span data-ttu-id="9434e-171">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="9434e-171">See also</span></span>
*  [<span data-ttu-id="9434e-172">Administrar los recursos de clúster de hello Apache Spark en HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="9434e-172">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)

### <a name="for-data-analysts"></a><span data-ttu-id="9434e-173">Para analistas de datos</span><span class="sxs-lookup"><span data-stu-id="9434e-173">For data analysts</span></span>

* [<span data-ttu-id="9434e-174">Creación de aplicaciones de Aprendizaje automático con Apache Spark en HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="9434e-174">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="9434e-175">Spark con aprendizaje automático: Use Spark en HDInsight toopredict de resultados de la inspección de alimentos</span><span class="sxs-lookup"><span data-stu-id="9434e-175">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="9434e-176">Análisis del registro del sitio web con Spark en HDInsight</span><span class="sxs-lookup"><span data-stu-id="9434e-176">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)
* [<span data-ttu-id="9434e-177">Análisis de datos de telemetría de Application Insights con Spark en HDInsight</span><span class="sxs-lookup"><span data-stu-id="9434e-177">Application Insight telemetry data analysis using Spark in HDInsight</span></span>](hdinsight-spark-analyze-application-insight-logs.md)
* [<span data-ttu-id="9434e-178">Uso de Caffe en Azure HDInsight Spark para el aprendizaje profundo distribuido</span><span class="sxs-lookup"><span data-stu-id="9434e-178">Use Caffe on Azure HDInsight Spark for distributed deep learning</span></span>](hdinsight-deep-learning-caffe-spark.md)

### <a name="for-spark-developers"></a><span data-ttu-id="9434e-179">Para desarrolladores de Spark</span><span class="sxs-lookup"><span data-stu-id="9434e-179">For Spark developers</span></span>

* [<span data-ttu-id="9434e-180">Crear una aplicación independiente con Scala</span><span class="sxs-lookup"><span data-stu-id="9434e-180">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="9434e-181">Ejecutar trabajos de forma remota en un clúster de Spark mediante Livy</span><span class="sxs-lookup"><span data-stu-id="9434e-181">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)
* [<span data-ttu-id="9434e-182">Usar el complemento de herramientas de HDInsight para toocreate IntelliJ IDEA y enviar solicitudes de Spark Scala</span><span class="sxs-lookup"><span data-stu-id="9434e-182">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="9434e-183">Streaming con Spark: uso de Spark en HDInsight para compilar aplicaciones de streaming en tiempo real</span><span class="sxs-lookup"><span data-stu-id="9434e-183">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="9434e-184">Usar complemento Herramientas de HDInsight para aplicaciones de IDEA IntelliJ toodebug Spark de forma remota</span><span class="sxs-lookup"><span data-stu-id="9434e-184">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="9434e-185">Uso de cuadernos de Zeppelin con un clúster Spark en HDInsight</span><span class="sxs-lookup"><span data-stu-id="9434e-185">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="9434e-186">Kernels disponibles para el cuaderno de Jupyter en el clúster Spark para HDInsight</span><span class="sxs-lookup"><span data-stu-id="9434e-186">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="9434e-187">Uso de paquetes externos con cuadernos de Jupyter Notebook</span><span class="sxs-lookup"><span data-stu-id="9434e-187">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="9434e-188">Instale Jupyter en el equipo y conecte tooan clúster de HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="9434e-188">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)


