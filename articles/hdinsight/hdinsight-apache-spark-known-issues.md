---
title: "clúster de problemas de aaaTroubleshoot con Apache Spark en HDInsight de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de los problemas relacionados tooApache clústeres de Spark en HDInsight de Azure y cómo toowork alrededor de los."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 610c4103-ffc8-4ec0-ad06-fdaf3c4d7c10
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 7373b90524ae5dbb10ab8ded593aa38d12c14b55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="known-issues-for-apache-spark-cluster-on-hdinsight"></a><span data-ttu-id="3b5f1-103">Problemas conocidos de clústeres de Apache Spark en HDInsight</span><span class="sxs-lookup"><span data-stu-id="3b5f1-103">Known issues for Apache Spark cluster on HDInsight</span></span>

<span data-ttu-id="3b5f1-104">Este documento hace un seguimiento de hello todos los problemas de versión preliminar pública de HDInsight Spark Hola conocidos.</span><span class="sxs-lookup"><span data-stu-id="3b5f1-104">This document keeps track of all hello known issues for hello HDInsight Spark public preview.</span></span>  

## <a name="livy-leaks-interactive-session"></a><span data-ttu-id="3b5f1-105">Sesión interactiva con pérdidas de Livy</span><span class="sxs-lookup"><span data-stu-id="3b5f1-105">Livy leaks interactive session</span></span>
<span data-ttu-id="3b5f1-106">Cuando Livio se reinicia (desde Ambari o reinicio de la máquina virtual de tooheadnode 0) con una sesión interactiva mantiene la conexión, se perderá una sesión interactiva de tareas.</span><span class="sxs-lookup"><span data-stu-id="3b5f1-106">When Livy is restarted (from Ambari or due tooheadnode 0 virtual machine reboot) with an interactive session still alive, an interactive job session will be leaked.</span></span> <span data-ttu-id="3b5f1-107">Por este motivo, podrá trabajos nuevo atascada en hello estado aceptado y no se puede iniciar.</span><span class="sxs-lookup"><span data-stu-id="3b5f1-107">Because of this, new jobs can stuck in hello Accepted state, and cannot be started.</span></span>

<span data-ttu-id="3b5f1-108">**Mitigación:**</span><span class="sxs-lookup"><span data-stu-id="3b5f1-108">**Mitigation:**</span></span>

<span data-ttu-id="3b5f1-109">Usar hello siguiendo el problema de hello tooworkaround procedimiento:</span><span class="sxs-lookup"><span data-stu-id="3b5f1-109">Use hello following procedure tooworkaround hello issue:</span></span>

1. <span data-ttu-id="3b5f1-110">SSH en el nodo principal.</span><span class="sxs-lookup"><span data-stu-id="3b5f1-110">Ssh into headnode.</span></span> <span data-ttu-id="3b5f1-111">Para más información, consulte [Uso de SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="3b5f1-111">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="3b5f1-112">Hola ejecución tras la aplicación de comando toofind Hola identificadores de hello interactivo trabajos iniciado mediante Livio.</span><span class="sxs-lookup"><span data-stu-id="3b5f1-112">Run hello following command toofind hello application IDs of hello interactive jobs started through Livy.</span></span> 
   
        yarn application –list
   
    <span data-ttu-id="3b5f1-113">Hello nombres de trabajo predeterminada será Livio si trabajos Hola iniciados con una sesión interactiva Livio ningún nombre explícito de hello sesión de Livio iniciada por Jupyter notebook, el nombre del trabajo Hola se iniciará con remotesparkmagics_ *.</span><span class="sxs-lookup"><span data-stu-id="3b5f1-113">hello default job names will be Livy if hello jobs were started with a Livy interactive session with no explicit names specified, For hello Livy session started by Jupyter notebook, hello job name will start with remotesparkmagics_*.</span></span> 
3. <span data-ttu-id="3b5f1-114">Siguiente ejecución Hola comando tookill dichos trabajos.</span><span class="sxs-lookup"><span data-stu-id="3b5f1-114">Run hello following command tookill those jobs.</span></span> 
   
        yarn application –kill <Application ID>

<span data-ttu-id="3b5f1-115">Los nuevos trabajos empezarán a ejecutarse.</span><span class="sxs-lookup"><span data-stu-id="3b5f1-115">New jobs will start running.</span></span> 

## <a name="spark-history-server-not-started"></a><span data-ttu-id="3b5f1-116">No se ha iniciado el servidor de historial de Spark</span><span class="sxs-lookup"><span data-stu-id="3b5f1-116">Spark History Server not started</span></span>
<span data-ttu-id="3b5f1-117">El servidor de historial de Spark no se inicia automáticamente después de crear un clúster.</span><span class="sxs-lookup"><span data-stu-id="3b5f1-117">Spark History Server is not started automatically after a cluster is created.</span></span>  

<span data-ttu-id="3b5f1-118">**Mitigación:**</span><span class="sxs-lookup"><span data-stu-id="3b5f1-118">**Mitigation:**</span></span> 

<span data-ttu-id="3b5f1-119">Iniciar manualmente el servidor de historial de Hola desde Ambari.</span><span class="sxs-lookup"><span data-stu-id="3b5f1-119">Manually start hello history server from Ambari.</span></span>

## <a name="permission-issue-in-spark-log-directory"></a><span data-ttu-id="3b5f1-120">Problemas con permisos en el directorio de registros de Spark</span><span class="sxs-lookup"><span data-stu-id="3b5f1-120">Permission issue in Spark log directory</span></span>
<span data-ttu-id="3b5f1-121">Cuando hdiuser envía un trabajo con spark-submit, hay un error java.io.FileNotFoundException: hello y /var/log/spark/sparkdriver_hdiuser.log (permiso denegado) no se escribe el registro del controlador.</span><span class="sxs-lookup"><span data-stu-id="3b5f1-121">When hdiuser submits a job with spark-submit, there is an error java.io.FileNotFoundException: /var/log/spark/sparkdriver_hdiuser.log (Permission denied) and hello driver log is not written.</span></span> 

<span data-ttu-id="3b5f1-122">**Mitigación:**</span><span class="sxs-lookup"><span data-stu-id="3b5f1-122">**Mitigation:**</span></span>

1. <span data-ttu-id="3b5f1-123">Agregar grupo de Hadoop de hdiuser toohello.</span><span class="sxs-lookup"><span data-stu-id="3b5f1-123">Add hdiuser toohello Hadoop group.</span></span> 
2. <span data-ttu-id="3b5f1-124">Proporcione 777 permisos en /var/log/spark después de crear el clúster.</span><span class="sxs-lookup"><span data-stu-id="3b5f1-124">Provide 777 permissions on /var/log/spark after cluster creation.</span></span> 
3. <span data-ttu-id="3b5f1-125">Actualizar ubicación de registro de hello spark con Ambari toobe un directorio 777 permisos.</span><span class="sxs-lookup"><span data-stu-id="3b5f1-125">Update hello spark log location using Ambari toobe a directory with 777 permissions.</span></span>  
4. <span data-ttu-id="3b5f1-126">Ejecute spark-submit como sudo.</span><span class="sxs-lookup"><span data-stu-id="3b5f1-126">Run spark-submit as sudo.</span></span>  

## <a name="spark-phoenix-connector-is-not-supported"></a><span data-ttu-id="3b5f1-127">No se admite el conector Spark-Phoenix</span><span class="sxs-lookup"><span data-stu-id="3b5f1-127">Spark-Phoenix connector is not supported</span></span>

<span data-ttu-id="3b5f1-128">Actualmente, el conector de Phoenix Spark de hello no es compatible con un clúster de HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="3b5f1-128">Currently, hello Spark-Phoenix connector is not supported with an HDInsight Spark cluster.</span></span>

<span data-ttu-id="3b5f1-129">**Mitigación:**</span><span class="sxs-lookup"><span data-stu-id="3b5f1-129">**Mitigation:**</span></span>

<span data-ttu-id="3b5f1-130">Debe utilizar el conector de HBase Spark de hello en su lugar.</span><span class="sxs-lookup"><span data-stu-id="3b5f1-130">You must use hello Spark-HBase connector instead.</span></span> <span data-ttu-id="3b5f1-131">Para obtener instrucciones, consulte [cómo toouse Spark HBase conector](https://blogs.msdn.microsoft.com/azuredatalake/2016/07/25/hdinsight-how-to-use-spark-hbase-connector/).</span><span class="sxs-lookup"><span data-stu-id="3b5f1-131">For instructions see [How toouse Spark-HBase connector](https://blogs.msdn.microsoft.com/azuredatalake/2016/07/25/hdinsight-how-to-use-spark-hbase-connector/).</span></span>

## <a name="issues-related-toojupyter-notebooks"></a><span data-ttu-id="3b5f1-132">Problemas relacionados con tooJupyter blocs de notas</span><span class="sxs-lookup"><span data-stu-id="3b5f1-132">Issues related tooJupyter notebooks</span></span>
<span data-ttu-id="3b5f1-133">Los siguientes son algunos problemas conocidos blocs de notas tooJupyter relacionados.</span><span class="sxs-lookup"><span data-stu-id="3b5f1-133">Following are some known issues related tooJupyter notebooks.</span></span>

### <a name="notebooks-with-non-ascii-characters-in-filenames"></a><span data-ttu-id="3b5f1-134">Cuadernos que tienen caracteres no ASCII en los nombres de archivo</span><span class="sxs-lookup"><span data-stu-id="3b5f1-134">Notebooks with non-ASCII characters in filenames</span></span>
<span data-ttu-id="3b5f1-135">Los cuadernos de Jupyter Notebook que pueden utilizarse en clústeres Spark de HDInsight no deben tener caracteres que no sean ASCII en los nombres de archivo.</span><span class="sxs-lookup"><span data-stu-id="3b5f1-135">Jupyter notebooks that can be used in Spark HDInsight clusters should not have non-ASCII characters in filenames.</span></span> <span data-ttu-id="3b5f1-136">Si intentas tooupload un archivo a través de hello Jupyter UI que tiene un nombre de archivo no son ASCII, producirá un error en modo silencioso (es decir, Jupyter no le permitirá cargar archivo hello, pero no produce un error visible ya sea).</span><span class="sxs-lookup"><span data-stu-id="3b5f1-136">If you try tooupload a file through hello Jupyter UI which has a non-ASCII filename, it will fail silently (that is, Jupyter won’t let you upload hello file, but it won’t throw a visible error either).</span></span> 

### <a name="error-while-loading-notebooks-of-larger-sizes"></a><span data-ttu-id="3b5f1-137">Error al cargar cuadernos con tamaños mayores</span><span class="sxs-lookup"><span data-stu-id="3b5f1-137">Error while loading notebooks of larger sizes</span></span>
<span data-ttu-id="3b5f1-138">Es posible que aparezca un error **`Error loading notebook`** al cargar cuadernos de mayor tamaño.</span><span class="sxs-lookup"><span data-stu-id="3b5f1-138">You might see an error **`Error loading notebook`** when you load notebooks that are larger in size.</span></span>  

<span data-ttu-id="3b5f1-139">**Mitigación:**</span><span class="sxs-lookup"><span data-stu-id="3b5f1-139">**Mitigation:**</span></span>

<span data-ttu-id="3b5f1-140">El hecho de recibir este error no implica que los datos estén dañados o perdidos.</span><span class="sxs-lookup"><span data-stu-id="3b5f1-140">If you get this error, it does not mean your data is corrupt or lost.</span></span>  <span data-ttu-id="3b5f1-141">Los blocs de notas están todavía en el disco en `/var/lib/jupyter`, y puede SSH en hello clúster tooaccess ellos.</span><span class="sxs-lookup"><span data-stu-id="3b5f1-141">Your notebooks are still on disk in `/var/lib/jupyter`, and you can SSH into hello cluster tooaccess them.</span></span> <span data-ttu-id="3b5f1-142">Para más información, consulte [Uso de SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="3b5f1-142">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="3b5f1-143">Una vez que se ha conectado el clúster toohello mediante SSH, puede copiar los blocs de notas desde el equipo local de clúster tooyour (uso de SCP o WinSCP) como una pérdida de hello tooprevent copia de seguridad de los datos importantes en el Bloc de notas de Hola.</span><span class="sxs-lookup"><span data-stu-id="3b5f1-143">Once you have connected toohello cluster using SSH, you can copy your notebooks from your cluster tooyour local machine (using SCP or WinSCP) as a backup tooprevent hello loss of any important data in hello notebook.</span></span> <span data-ttu-id="3b5f1-144">Puede, a continuación, túnel SSH en el nodo principal en el puerto 8001 tooaccess Jupyter sin tener que pasar a través de puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="3b5f1-144">You can then SSH tunnel into your headnode at port 8001 tooaccess Jupyter without going through hello gateway.</span></span>  <span data-ttu-id="3b5f1-145">Desde allí, puede borrar la salida de hello del Bloc de notas y volver a guardarla tamaño toominimize Hola Bloc de notas.</span><span class="sxs-lookup"><span data-stu-id="3b5f1-145">From there, you can clear hello output of your notebook and re-save it toominimize hello notebook’s size.</span></span>

<span data-ttu-id="3b5f1-146">tooprevent este error suceda en hello futura, debe seguir algunas prácticas recomendadas:</span><span class="sxs-lookup"><span data-stu-id="3b5f1-146">tooprevent this error from happening in hello future, you must follow some best practices:</span></span>

* <span data-ttu-id="3b5f1-147">Es importante tookeep Hola Bloc de notas el tamaño pequeño.</span><span class="sxs-lookup"><span data-stu-id="3b5f1-147">It is important tookeep hello notebook size small.</span></span> <span data-ttu-id="3b5f1-148">Los resultados de los trabajos de Spark que se le envía tooJupyter se conserva en el Bloc de notas de Hola.</span><span class="sxs-lookup"><span data-stu-id="3b5f1-148">Any output from your Spark jobs that is sent back tooJupyter is persisted in hello notebook.</span></span>  <span data-ttu-id="3b5f1-149">Es una práctica recomendada con Jupyter en tooavoid general ejecutando `.collect()` en RDD grandes o tramas de datos; en su lugar, si desea que toopeek en el contenido de un diseño dirigido por responsabilidades, considere la posibilidad de ejecutar `.take()` o `.sample()` para que el resultado no obtenga demasiado grande.</span><span class="sxs-lookup"><span data-stu-id="3b5f1-149">It is a best practice with Jupyter in general tooavoid running `.collect()` on large RDD’s or dataframes; instead, if you want toopeek at an RDD’s contents, consider running `.take()` or `.sample()` so that your output doesn’t get too big.</span></span>
* <span data-ttu-id="3b5f1-150">Además, cuando se guarda un bloc de notas, desactive todas las celdas tooreduce Hola tamaño resultante.</span><span class="sxs-lookup"><span data-stu-id="3b5f1-150">Also, when you save a notebook, clear all output cells tooreduce hello size.</span></span>

### <a name="notebook-initial-startup-takes-longer-than-expected"></a><span data-ttu-id="3b5f1-151">El primer inicio del cuaderno tarda más de lo esperado</span><span class="sxs-lookup"><span data-stu-id="3b5f1-151">Notebook initial startup takes longer than expected</span></span>
<span data-ttu-id="3b5f1-152">La primera instrucción del cuaderno de Jupyter con la instrucción mágica de Spark podría tardar más de un minuto.</span><span class="sxs-lookup"><span data-stu-id="3b5f1-152">First code statement in Jupyter notebook using Spark magic could take more than a minute.</span></span>  

<span data-ttu-id="3b5f1-153">**Explicación:**</span><span class="sxs-lookup"><span data-stu-id="3b5f1-153">**Explanation:**</span></span>

<span data-ttu-id="3b5f1-154">Esto sucede porque cuando se ejecuta la primera celda de código de hello.</span><span class="sxs-lookup"><span data-stu-id="3b5f1-154">This happens because when hello first code cell is run.</span></span> <span data-ttu-id="3b5f1-155">En segundo plano de hello este comando inicia configuración de sesión y Spark, SQL y se establecen los contextos de Hive.</span><span class="sxs-lookup"><span data-stu-id="3b5f1-155">In hello background this initiates session configuration and Spark, SQL, and Hive contexts are set.</span></span> <span data-ttu-id="3b5f1-156">Después de que se establecen estos contextos, se ejecuta la primera instrucción de Hola y así, impresión de Hola que instrucción Hola tardó un toocomplete mucho tiempo.</span><span class="sxs-lookup"><span data-stu-id="3b5f1-156">After these contexts are set, hello first statement is run and this gives hello impression that hello statement took a long time toocomplete.</span></span>

### <a name="jupyter-notebook-timeout-in-creating-hello-session"></a><span data-ttu-id="3b5f1-157">Tiempo de espera de Jupyter notebook en Crear sesión de Hola</span><span class="sxs-lookup"><span data-stu-id="3b5f1-157">Jupyter notebook timeout in creating hello session</span></span>
<span data-ttu-id="3b5f1-158">Al clúster de Spark carece de recursos, hello Spark y kernels Pyspark en el Bloc de notas de hello Jupyter aparecerá tratando de sesión de hello toocreate de tiempo de espera.</span><span class="sxs-lookup"><span data-stu-id="3b5f1-158">When Spark cluster is out of resources, hello Spark and Pyspark kernels in hello Jupyter notebook will timeout trying toocreate hello session.</span></span> 

<span data-ttu-id="3b5f1-159">**Mitigaciones:**</span><span class="sxs-lookup"><span data-stu-id="3b5f1-159">**Mitigations:**</span></span> 

1. <span data-ttu-id="3b5f1-160">Libere algunos recursos del clúster Spark de la siguiente forma:</span><span class="sxs-lookup"><span data-stu-id="3b5f1-160">Free up some resources in your Spark cluster by:</span></span>
   
   * <span data-ttu-id="3b5f1-161">Detener otros blocs de notas de Spark va toohello cierre y menú de detención o al hacer clic en Cerrar en el Explorador de hello Bloc de notas.</span><span class="sxs-lookup"><span data-stu-id="3b5f1-161">Stopping other Spark notebooks by going toohello Close and Halt menu or clicking Shutdown in hello notebook explorer.</span></span>
   * <span data-ttu-id="3b5f1-162">Detenga otras aplicaciones de Spark desde YARN.</span><span class="sxs-lookup"><span data-stu-id="3b5f1-162">Stopping other Spark applications from YARN.</span></span>
2. <span data-ttu-id="3b5f1-163">Reinicie el Bloc de notas de Hola que estaba intentando toostart seguridad.</span><span class="sxs-lookup"><span data-stu-id="3b5f1-163">Restart hello notebook you were trying toostart up.</span></span> <span data-ttu-id="3b5f1-164">Suficientes recursos deben estar disponibles para toocreate una sesión ahora.</span><span class="sxs-lookup"><span data-stu-id="3b5f1-164">Enough resources should be available for you toocreate a session now.</span></span>

## <a name="see-also"></a><span data-ttu-id="3b5f1-165">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="3b5f1-165">See also</span></span>
* [<span data-ttu-id="3b5f1-166">Introducción a Apache Spark en HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="3b5f1-166">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="3b5f1-167">Escenarios</span><span class="sxs-lookup"><span data-stu-id="3b5f1-167">Scenarios</span></span>
* [<span data-ttu-id="3b5f1-168">Spark with BI: Realizar el análisis de datos interactivos con Spark en HDInsight con las herramientas de BI</span><span class="sxs-lookup"><span data-stu-id="3b5f1-168">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="3b5f1-169">Creación de aplicaciones de Aprendizaje automático con Apache Spark en HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="3b5f1-169">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="3b5f1-170">Spark con aprendizaje automático: Use Spark en HDInsight toopredict de resultados de la inspección de alimentos</span><span class="sxs-lookup"><span data-stu-id="3b5f1-170">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="3b5f1-171">Streaming con Spark: uso de Spark en HDInsight para compilar aplicaciones de streaming en tiempo real</span><span class="sxs-lookup"><span data-stu-id="3b5f1-171">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="3b5f1-172">Análisis del registro del sitio web con Spark en HDInsight</span><span class="sxs-lookup"><span data-stu-id="3b5f1-172">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="3b5f1-173">Creación y ejecución de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="3b5f1-173">Create and run applications</span></span>
* [<span data-ttu-id="3b5f1-174">Crear una aplicación independiente con Scala</span><span class="sxs-lookup"><span data-stu-id="3b5f1-174">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="3b5f1-175">Ejecutar trabajos de forma remota en un clúster de Spark mediante Livy</span><span class="sxs-lookup"><span data-stu-id="3b5f1-175">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="3b5f1-176">Herramientas y extensiones</span><span class="sxs-lookup"><span data-stu-id="3b5f1-176">Tools and extensions</span></span>
* [<span data-ttu-id="3b5f1-177">Usar el complemento de herramientas de HDInsight para toocreate IntelliJ IDEA y enviar Spark Scala aplicaciones</span><span class="sxs-lookup"><span data-stu-id="3b5f1-177">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="3b5f1-178">Usar complemento Herramientas de HDInsight para aplicaciones de IDEA IntelliJ toodebug Spark de forma remota</span><span class="sxs-lookup"><span data-stu-id="3b5f1-178">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="3b5f1-179">Uso de cuadernos de Zeppelin con un clúster Spark en HDInsight</span><span class="sxs-lookup"><span data-stu-id="3b5f1-179">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="3b5f1-180">Kernels disponibles para el cuaderno de Jupyter en el clúster Spark para HDInsight</span><span class="sxs-lookup"><span data-stu-id="3b5f1-180">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="3b5f1-181">Uso de paquetes externos con cuadernos de Jupyter Notebook</span><span class="sxs-lookup"><span data-stu-id="3b5f1-181">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="3b5f1-182">Instale Jupyter en el equipo y conecte tooan clúster de HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="3b5f1-182">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="3b5f1-183">Administración de recursos</span><span class="sxs-lookup"><span data-stu-id="3b5f1-183">Manage resources</span></span>
* [<span data-ttu-id="3b5f1-184">Administrar los recursos de clúster de hello Apache Spark en HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="3b5f1-184">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="3b5f1-185">Track and debug jobs running on an Apache Spark cluster in HDInsight (Seguimiento y depuración de trabajos que se ejecutan en un clúster de Apache Spark en HDInsight)</span><span class="sxs-lookup"><span data-stu-id="3b5f1-185">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

