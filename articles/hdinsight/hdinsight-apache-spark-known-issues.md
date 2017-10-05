---
title: "Solución de problemas con el clúster de Apache Spark en Azure HDInsight | Microsoft Docs"
description: "Obtenga información sobre problemas relacionados con los clústeres de Apache Spark en Azure HDInsight y cómo evitarlos."
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
ms.openlocfilehash: 3a493a2c35a6cdd31bb1e4ff66113a8f8d97d4f4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="known-issues-for-apache-spark-cluster-on-hdinsight"></a><span data-ttu-id="f2a8f-103">Problemas conocidos de clústeres de Apache Spark en HDInsight</span><span class="sxs-lookup"><span data-stu-id="f2a8f-103">Known issues for Apache Spark cluster on HDInsight</span></span>

<span data-ttu-id="f2a8f-104">En este documento se hace un seguimiento de todos los problemas conocidos de la versión preliminar pública de HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="f2a8f-104">This document keeps track of all the known issues for the HDInsight Spark public preview.</span></span>  

## <a name="livy-leaks-interactive-session"></a><span data-ttu-id="f2a8f-105">Sesión interactiva con pérdidas de Livy</span><span class="sxs-lookup"><span data-stu-id="f2a8f-105">Livy leaks interactive session</span></span>
<span data-ttu-id="f2a8f-106">Cuando se reinicia Livy (desde Ambari o debido al reinicio de la máquina virtual del nodo principal 0) con una sesión interactiva activa, se perderá una sesión de trabajo interactiva.</span><span class="sxs-lookup"><span data-stu-id="f2a8f-106">When Livy is restarted (from Ambari or due to headnode 0 virtual machine reboot) with an interactive session still alive, an interactive job session will be leaked.</span></span> <span data-ttu-id="f2a8f-107">Por este motivo, los nuevos trabajos pueden bloquearse en el estado Aceptado y no se pueden iniciar.</span><span class="sxs-lookup"><span data-stu-id="f2a8f-107">Because of this, new jobs can stuck in the Accepted state, and cannot be started.</span></span>

<span data-ttu-id="f2a8f-108">**Mitigación:**</span><span class="sxs-lookup"><span data-stu-id="f2a8f-108">**Mitigation:**</span></span>

<span data-ttu-id="f2a8f-109">Utilice el procedimiento siguiente para encontrar una solución alternativa para el problema:</span><span class="sxs-lookup"><span data-stu-id="f2a8f-109">Use the following procedure to workaround the issue:</span></span>

1. <span data-ttu-id="f2a8f-110">SSH en el nodo principal.</span><span class="sxs-lookup"><span data-stu-id="f2a8f-110">Ssh into headnode.</span></span> <span data-ttu-id="f2a8f-111">Para obtener más información, consulte [Uso de SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="f2a8f-111">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="f2a8f-112">Ejecute el siguiente comando para buscar los identificadores de aplicación de los trabajos interactivos iniciados mediante Livy.</span><span class="sxs-lookup"><span data-stu-id="f2a8f-112">Run the following command to find the application IDs of the interactive jobs started through Livy.</span></span> 
   
        yarn application –list
   
    <span data-ttu-id="f2a8f-113">Los nombres predeterminados de los trabajos serán Livy si se han iniciado con una sesión interactiva de Livy sin nombres explícitos especificados; en caso de que la sesión de Livy se haya iniciado mediante el cuaderno de Jupyter, el nombre del trabajo empezará por remotesparkmagics_*.</span><span class="sxs-lookup"><span data-stu-id="f2a8f-113">The default job names will be Livy if the jobs were started with a Livy interactive session with no explicit names specified, For the Livy session started by Jupyter notebook, the job name will start with remotesparkmagics_*.</span></span> 
3. <span data-ttu-id="f2a8f-114">Ejecute el comando siguiente para terminar esos trabajos.</span><span class="sxs-lookup"><span data-stu-id="f2a8f-114">Run the following command to kill those jobs.</span></span> 
   
        yarn application –kill <Application ID>

<span data-ttu-id="f2a8f-115">Los nuevos trabajos empezarán a ejecutarse.</span><span class="sxs-lookup"><span data-stu-id="f2a8f-115">New jobs will start running.</span></span> 

## <a name="spark-history-server-not-started"></a><span data-ttu-id="f2a8f-116">No se ha iniciado el servidor de historial de Spark</span><span class="sxs-lookup"><span data-stu-id="f2a8f-116">Spark History Server not started</span></span>
<span data-ttu-id="f2a8f-117">El servidor de historial de Spark no se inicia automáticamente después de crear un clúster.</span><span class="sxs-lookup"><span data-stu-id="f2a8f-117">Spark History Server is not started automatically after a cluster is created.</span></span>  

<span data-ttu-id="f2a8f-118">**Mitigación:**</span><span class="sxs-lookup"><span data-stu-id="f2a8f-118">**Mitigation:**</span></span> 

<span data-ttu-id="f2a8f-119">Inicie el servidor de historial manualmente desde Ambari.</span><span class="sxs-lookup"><span data-stu-id="f2a8f-119">Manually start the history server from Ambari.</span></span>

## <a name="permission-issue-in-spark-log-directory"></a><span data-ttu-id="f2a8f-120">Problemas con permisos en el directorio de registros de Spark</span><span class="sxs-lookup"><span data-stu-id="f2a8f-120">Permission issue in Spark log directory</span></span>
<span data-ttu-id="f2a8f-121">Cuando hdiuser envía un trabajo con spark-submit, hay un error java.io.FileNotFoundException: /var/log/spark/sparkdriver_hdiuser.log (permiso denegado) y el registro del controlador no se ha escrito.</span><span class="sxs-lookup"><span data-stu-id="f2a8f-121">When hdiuser submits a job with spark-submit, there is an error java.io.FileNotFoundException: /var/log/spark/sparkdriver_hdiuser.log (Permission denied) and the driver log is not written.</span></span> 

<span data-ttu-id="f2a8f-122">**Mitigación:**</span><span class="sxs-lookup"><span data-stu-id="f2a8f-122">**Mitigation:**</span></span>

1. <span data-ttu-id="f2a8f-123">Agregue hdiuser al grupo de Hadoop.</span><span class="sxs-lookup"><span data-stu-id="f2a8f-123">Add hdiuser to the Hadoop group.</span></span> 
2. <span data-ttu-id="f2a8f-124">Proporcione 777 permisos en /var/log/spark después de crear el clúster.</span><span class="sxs-lookup"><span data-stu-id="f2a8f-124">Provide 777 permissions on /var/log/spark after cluster creation.</span></span> 
3. <span data-ttu-id="f2a8f-125">Actualice la ubicación del registro spark con Ambari para que sea un directorio con 777 permisos.</span><span class="sxs-lookup"><span data-stu-id="f2a8f-125">Update the spark log location using Ambari to be a directory with 777 permissions.</span></span>  
4. <span data-ttu-id="f2a8f-126">Ejecute spark-submit como sudo.</span><span class="sxs-lookup"><span data-stu-id="f2a8f-126">Run spark-submit as sudo.</span></span>  

## <a name="spark-phoenix-connector-is-not-supported"></a><span data-ttu-id="f2a8f-127">No se admite el conector Spark-Phoenix</span><span class="sxs-lookup"><span data-stu-id="f2a8f-127">Spark-Phoenix connector is not supported</span></span>

<span data-ttu-id="f2a8f-128">En este momento, el conector Spark-Phoenix no es compatible con un clúster de Spark de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f2a8f-128">Currently, the Spark-Phoenix connector is not supported with an HDInsight Spark cluster.</span></span>

<span data-ttu-id="f2a8f-129">**Mitigación:**</span><span class="sxs-lookup"><span data-stu-id="f2a8f-129">**Mitigation:**</span></span>

<span data-ttu-id="f2a8f-130">Debe usar el conector Spark-HBase en su lugar.</span><span class="sxs-lookup"><span data-stu-id="f2a8f-130">You must use the Spark-HBase connector instead.</span></span> <span data-ttu-id="f2a8f-131">Para obtener instrucciones al respecto, consulte [Utilización del conector Spark-HBase](https://blogs.msdn.microsoft.com/azuredatalake/2016/07/25/hdinsight-how-to-use-spark-hbase-connector/).</span><span class="sxs-lookup"><span data-stu-id="f2a8f-131">For instructions see [How to use Spark-HBase connector](https://blogs.msdn.microsoft.com/azuredatalake/2016/07/25/hdinsight-how-to-use-spark-hbase-connector/).</span></span>

## <a name="issues-related-to-jupyter-notebooks"></a><span data-ttu-id="f2a8f-132">Problemas relacionados con los cuadernos de Jupyter Notebook</span><span class="sxs-lookup"><span data-stu-id="f2a8f-132">Issues related to Jupyter notebooks</span></span>
<span data-ttu-id="f2a8f-133">A continuación, se muestran algunos problemas conocidos relacionados con los cuadernos de Jupyter Notebook.</span><span class="sxs-lookup"><span data-stu-id="f2a8f-133">Following are some known issues related to Jupyter notebooks.</span></span>

### <a name="notebooks-with-non-ascii-characters-in-filenames"></a><span data-ttu-id="f2a8f-134">Cuadernos que tienen caracteres no ASCII en los nombres de archivo</span><span class="sxs-lookup"><span data-stu-id="f2a8f-134">Notebooks with non-ASCII characters in filenames</span></span>
<span data-ttu-id="f2a8f-135">Los cuadernos de Jupyter Notebook que pueden utilizarse en clústeres Spark de HDInsight no deben tener caracteres que no sean ASCII en los nombres de archivo.</span><span class="sxs-lookup"><span data-stu-id="f2a8f-135">Jupyter notebooks that can be used in Spark HDInsight clusters should not have non-ASCII characters in filenames.</span></span> <span data-ttu-id="f2a8f-136">Si trata de cargar un archivo a través de la interfaz de usuario de Jupyter con un nombre de archivo que incluye caracteres que no son ASCII, se producirá un error silenciosamente (es decir, Jupyter no permitirá cargar el archivo y tampoco se mostrará un error).</span><span class="sxs-lookup"><span data-stu-id="f2a8f-136">If you try to upload a file through the Jupyter UI which has a non-ASCII filename, it will fail silently (that is, Jupyter won’t let you upload the file, but it won’t throw a visible error either).</span></span> 

### <a name="error-while-loading-notebooks-of-larger-sizes"></a><span data-ttu-id="f2a8f-137">Error al cargar cuadernos con tamaños mayores</span><span class="sxs-lookup"><span data-stu-id="f2a8f-137">Error while loading notebooks of larger sizes</span></span>
<span data-ttu-id="f2a8f-138">Es posible que aparezca un error **`Error loading notebook`** al cargar cuadernos de mayor tamaño.</span><span class="sxs-lookup"><span data-stu-id="f2a8f-138">You might see an error **`Error loading notebook`** when you load notebooks that are larger in size.</span></span>  

<span data-ttu-id="f2a8f-139">**Mitigación:**</span><span class="sxs-lookup"><span data-stu-id="f2a8f-139">**Mitigation:**</span></span>

<span data-ttu-id="f2a8f-140">El hecho de recibir este error no implica que los datos estén dañados o perdidos.</span><span class="sxs-lookup"><span data-stu-id="f2a8f-140">If you get this error, it does not mean your data is corrupt or lost.</span></span>  <span data-ttu-id="f2a8f-141">Los cuadernos siguen aún en el disco en `/var/lib/jupyter`y se puede conectar mediante SSH al clúster para acceder ellos.</span><span class="sxs-lookup"><span data-stu-id="f2a8f-141">Your notebooks are still on disk in `/var/lib/jupyter`, and you can SSH into the cluster to access them.</span></span> <span data-ttu-id="f2a8f-142">Para obtener más información, consulte [Uso de SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="f2a8f-142">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="f2a8f-143">Cuando se haya conectado al clúster mediante SSH, puede copiar sus cuadernos desde el clúster en la máquina local (mediante SCP o WinSCP) como copia de seguridad para impedir la pérdida de datos importantes en el cuaderno.</span><span class="sxs-lookup"><span data-stu-id="f2a8f-143">Once you have connected to the cluster using SSH, you can copy your notebooks from your cluster to your local machine (using SCP or WinSCP) as a backup to prevent the loss of any important data in the notebook.</span></span> <span data-ttu-id="f2a8f-144">A continuación, puede aplicar túneles SSH al nodo principal del puerto 8001 para tener acceso a Jupyter sin pasar por la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="f2a8f-144">You can then SSH tunnel into your headnode at port 8001 to access Jupyter without going through the gateway.</span></span>  <span data-ttu-id="f2a8f-145">Desde ahí, puede borrar la salida del bloc de notas y volver a guardarla para minimizar el tamaño del bloc de notas.</span><span class="sxs-lookup"><span data-stu-id="f2a8f-145">From there, you can clear the output of your notebook and re-save it to minimize the notebook’s size.</span></span>

<span data-ttu-id="f2a8f-146">Para evitar que este error ocurra en el futuro, debe seguir algunos procedimientos recomendados:</span><span class="sxs-lookup"><span data-stu-id="f2a8f-146">To prevent this error from happening in the future, you must follow some best practices:</span></span>

* <span data-ttu-id="f2a8f-147">Es importante mantener reducido el tamaño del bloc de notas.</span><span class="sxs-lookup"><span data-stu-id="f2a8f-147">It is important to keep the notebook size small.</span></span> <span data-ttu-id="f2a8f-148">Las salidas de los trabajos de Spark que se envían a Jupyter de vuelta se conservan en el bloc de notas.</span><span class="sxs-lookup"><span data-stu-id="f2a8f-148">Any output from your Spark jobs that is sent back to Jupyter is persisted in the notebook.</span></span>  <span data-ttu-id="f2a8f-149">En general, con Jupyter se recomienda evitar ejecutar `.collect()` en RDD o tramas de datos de gran tamaño; en su lugar, si desea inspeccionar el contenido de un RDD, considere la posibilidad de ejecutar `.take()` o `.sample()` para que la salida no sea demasiado grande.</span><span class="sxs-lookup"><span data-stu-id="f2a8f-149">It is a best practice with Jupyter in general to avoid running `.collect()` on large RDD’s or dataframes; instead, if you want to peek at an RDD’s contents, consider running `.take()` or `.sample()` so that your output doesn’t get too big.</span></span>
* <span data-ttu-id="f2a8f-150">Además, cuando guarde un bloc de notas, desactive todas las celdas de la salida para reducir el tamaño.</span><span class="sxs-lookup"><span data-stu-id="f2a8f-150">Also, when you save a notebook, clear all output cells to reduce the size.</span></span>

### <a name="notebook-initial-startup-takes-longer-than-expected"></a><span data-ttu-id="f2a8f-151">El primer inicio del cuaderno tarda más de lo esperado</span><span class="sxs-lookup"><span data-stu-id="f2a8f-151">Notebook initial startup takes longer than expected</span></span>
<span data-ttu-id="f2a8f-152">La primera instrucción del cuaderno de Jupyter con la instrucción mágica de Spark podría tardar más de un minuto.</span><span class="sxs-lookup"><span data-stu-id="f2a8f-152">First code statement in Jupyter notebook using Spark magic could take more than a minute.</span></span>  

<span data-ttu-id="f2a8f-153">**Explicación:**</span><span class="sxs-lookup"><span data-stu-id="f2a8f-153">**Explanation:**</span></span>

<span data-ttu-id="f2a8f-154">Esto sucede cuando se ejecuta la primera celda de código.</span><span class="sxs-lookup"><span data-stu-id="f2a8f-154">This happens because when the first code cell is run.</span></span> <span data-ttu-id="f2a8f-155">En segundo plano se inicia la configuración de la sesión y se establecen los contextos de Spark, SQL y Hive.</span><span class="sxs-lookup"><span data-stu-id="f2a8f-155">In the background this initiates session configuration and Spark, SQL, and Hive contexts are set.</span></span> <span data-ttu-id="f2a8f-156">Una vez establecidos estos contextos, se ejecuta la primera instrucción y esto da la impresión de que la instrucción tardó mucho tiempo en completarse.</span><span class="sxs-lookup"><span data-stu-id="f2a8f-156">After these contexts are set, the first statement is run and this gives the impression that the statement took a long time to complete.</span></span>

### <a name="jupyter-notebook-timeout-in-creating-the-session"></a><span data-ttu-id="f2a8f-157">Tiempo de espera del cuaderno de Jupyter en la creación de la sesión</span><span class="sxs-lookup"><span data-stu-id="f2a8f-157">Jupyter notebook timeout in creating the session</span></span>
<span data-ttu-id="f2a8f-158">Cuando el clúster Spark se está quedando sin recursos, el tiempo de espera de los kernels Spark y Pyspark del cuaderno de Jupyter se agotará al tratar de crear la sesión.</span><span class="sxs-lookup"><span data-stu-id="f2a8f-158">When Spark cluster is out of resources, the Spark and Pyspark kernels in the Jupyter notebook will timeout trying to create the session.</span></span> 

<span data-ttu-id="f2a8f-159">**Mitigaciones:**</span><span class="sxs-lookup"><span data-stu-id="f2a8f-159">**Mitigations:**</span></span> 

1. <span data-ttu-id="f2a8f-160">Libere algunos recursos del clúster Spark de la siguiente forma:</span><span class="sxs-lookup"><span data-stu-id="f2a8f-160">Free up some resources in your Spark cluster by:</span></span>
   
   * <span data-ttu-id="f2a8f-161">Detenga otros cuadernos de Spark en el menú Cerrar y detener o haga clic en Apagar en el explorador del cuaderno.</span><span class="sxs-lookup"><span data-stu-id="f2a8f-161">Stopping other Spark notebooks by going to the Close and Halt menu or clicking Shutdown in the notebook explorer.</span></span>
   * <span data-ttu-id="f2a8f-162">Detenga otras aplicaciones de Spark desde YARN.</span><span class="sxs-lookup"><span data-stu-id="f2a8f-162">Stopping other Spark applications from YARN.</span></span>
2. <span data-ttu-id="f2a8f-163">Reinicie el cuaderno que trataba de iniciar.</span><span class="sxs-lookup"><span data-stu-id="f2a8f-163">Restart the notebook you were trying to start up.</span></span> <span data-ttu-id="f2a8f-164">Debe haber suficientes recursos para crear una sesión ahora.</span><span class="sxs-lookup"><span data-stu-id="f2a8f-164">Enough resources should be available for you to create a session now.</span></span>

## <a name="see-also"></a><span data-ttu-id="f2a8f-165">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="f2a8f-165">See also</span></span>
* [<span data-ttu-id="f2a8f-166">Introducción a Apache Spark en HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="f2a8f-166">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="f2a8f-167">Escenarios</span><span class="sxs-lookup"><span data-stu-id="f2a8f-167">Scenarios</span></span>
* [<span data-ttu-id="f2a8f-168">Spark with BI: Realizar el análisis de datos interactivos con Spark en HDInsight con las herramientas de BI</span><span class="sxs-lookup"><span data-stu-id="f2a8f-168">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="f2a8f-169">Creación de aplicaciones de Aprendizaje automático con Apache Spark en HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="f2a8f-169">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="f2a8f-170">Spark con aprendizaje automático: uso de Spark en HDInsight para predecir los resultados de la inspección de alimentos</span><span class="sxs-lookup"><span data-stu-id="f2a8f-170">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="f2a8f-171">Streaming con Spark: uso de Spark en HDInsight para compilar aplicaciones de streaming en tiempo real</span><span class="sxs-lookup"><span data-stu-id="f2a8f-171">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="f2a8f-172">Análisis del registro del sitio web con Spark en HDInsight</span><span class="sxs-lookup"><span data-stu-id="f2a8f-172">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="f2a8f-173">Creación y ejecución de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="f2a8f-173">Create and run applications</span></span>
* [<span data-ttu-id="f2a8f-174">Crear una aplicación independiente con Scala</span><span class="sxs-lookup"><span data-stu-id="f2a8f-174">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="f2a8f-175">Ejecutar trabajos de forma remota en un clúster de Spark mediante Livy</span><span class="sxs-lookup"><span data-stu-id="f2a8f-175">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="f2a8f-176">Herramientas y extensiones</span><span class="sxs-lookup"><span data-stu-id="f2a8f-176">Tools and extensions</span></span>
* [<span data-ttu-id="f2a8f-177">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applications (Uso del complemento de herramientas de HDInsight para IntelliJ IDEA para crear y enviar aplicaciones Scala Spark)</span><span class="sxs-lookup"><span data-stu-id="f2a8f-177">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="f2a8f-178">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely (Uso del complemento de herramientas de HDInsight para IntelliJ IDEA para depurar aplicaciones de Spark de forma remota)</span><span class="sxs-lookup"><span data-stu-id="f2a8f-178">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="f2a8f-179">Uso de cuadernos de Zeppelin con un clúster Spark en HDInsight</span><span class="sxs-lookup"><span data-stu-id="f2a8f-179">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="f2a8f-180">Kernels disponibles para el cuaderno de Jupyter en el clúster Spark para HDInsight</span><span class="sxs-lookup"><span data-stu-id="f2a8f-180">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="f2a8f-181">Uso de paquetes externos con cuadernos de Jupyter Notebook</span><span class="sxs-lookup"><span data-stu-id="f2a8f-181">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="f2a8f-182">Instalación de un cuaderno de Jupyter Notebook en el equipo y conexión al clúster de Apache Spark en HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="f2a8f-182">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="f2a8f-183">Administración de recursos</span><span class="sxs-lookup"><span data-stu-id="f2a8f-183">Manage resources</span></span>
* [<span data-ttu-id="f2a8f-184">Administración de recursos para el clúster Apache Spark en HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="f2a8f-184">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="f2a8f-185">Track and debug jobs running on an Apache Spark cluster in HDInsight (Seguimiento y depuración de trabajos que se ejecutan en un clúster de Apache Spark en HDInsight)</span><span class="sxs-lookup"><span data-stu-id="f2a8f-185">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

