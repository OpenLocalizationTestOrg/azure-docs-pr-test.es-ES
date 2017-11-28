---
title: "Solución de problemas de Hive mediante Azure HDInsight | Microsoft Docs"
description: "Obtenga respuestas a las preguntas comunes sobre cómo trabajar con Apache Hive y Azure HDInsight."
keywords: "Azure HDInsight, Hive, preguntas más frecuentes, guía de solución de problemas, preguntas comunes"
services: Azure HDInsight
documentationcenter: na
author: dharmeshkakadia
manager: 
editor: 
ms.assetid: 15B8D0F3-F2D3-4746-BDCB-C72944AA9252
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/7/2017
ms.author: dharmeshkakadia
ms.openlocfilehash: 53e9685458190efe6a586504721b8e7baadaed60
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="troubleshoot-hive-by-using-azure-hdinsight"></a><span data-ttu-id="30560-104">Solución de problemas de Hive mediante Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="30560-104">Troubleshoot Hive by using Azure HDInsight</span></span>

<span data-ttu-id="30560-105">Obtenga información sobre las principales preguntas y sus soluciones al trabajar con cargas útiles de Apache Hive en Apache Ambari.</span><span class="sxs-lookup"><span data-stu-id="30560-105">Learn about the top questions and their resolutions when working with Apache Hive payloads in Apache Ambari.</span></span>


## <a name="how-do-i-export-a-hive-metastore-and-import-it-on-another-cluster"></a><span data-ttu-id="30560-106">¿Cómo se exporta Hive Metastore y se importa en otro clúster?</span><span class="sxs-lookup"><span data-stu-id="30560-106">How do I export a Hive metastore and import it on another cluster</span></span>


### <a name="resolution-steps"></a><span data-ttu-id="30560-107">Pasos de la solución</span><span class="sxs-lookup"><span data-stu-id="30560-107">Resolution steps</span></span>

1. <span data-ttu-id="30560-108">Conéctese al clúster de HDInsight con un cliente Secure Shell (SSH).</span><span class="sxs-lookup"><span data-stu-id="30560-108">Connect to the HDInsight cluster by using a Secure Shell (SSH) client.</span></span> <span data-ttu-id="30560-109">Para más información, consulte [Lecturas adicionales](#additional-reading-end).</span><span class="sxs-lookup"><span data-stu-id="30560-109">For more information, see [Additional reading](#additional-reading-end).</span></span>

2. <span data-ttu-id="30560-110">Ejecute el siguiente comando en el clúster de HDInsight desde donde desea exportar Metastore:</span><span class="sxs-lookup"><span data-stu-id="30560-110">Run the following command on the HDInsight cluster from which you want to export the metastore:</span></span>

    ```apache
    for d in `hive -e "show databases"`; do echo "create database $d; use $d;" >> alltables.sql ; for t in `hive --database $d -e "show tables"` ; do ddl=`hive --database $d -e "show create table $t"`; echo "$ddl ;" >> alltables.sql ; echo "$ddl" | grep -q "PARTITIONED\s*BY" && echo "MSCK REPAIR TABLE $t ;" >> alltables.sql ; done; done
    ```

  <span data-ttu-id="30560-111">Este comando genera un archivo denominado allatables.sql.</span><span class="sxs-lookup"><span data-stu-id="30560-111">This command generates a file named allatables.sql.</span></span>

3. <span data-ttu-id="30560-112">Copie el archivo alltables.sql en el nuevo clúster de HDInsight y ejecute el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="30560-112">Copy the file alltables.sql to the new HDInsight cluster, and then run the following command:</span></span>

  ```apache
  hive -f alltables.sql
  ```

<span data-ttu-id="30560-113">El código de los pasos de resolución asume que las rutas de acceso de datos en el nuevo clúster son las mismos que las rutas de acceso de datos en el clúster antiguo.</span><span class="sxs-lookup"><span data-stu-id="30560-113">The code in the resolution steps assumes that data paths on the new cluster are the same as the data paths on the old cluster.</span></span> <span data-ttu-id="30560-114">Si las rutas de acceso de datos son diferentes, puede editar manualmente el archivo alltables.sql generado para reflejar cualquier cambio.</span><span class="sxs-lookup"><span data-stu-id="30560-114">If the data paths are different, you can manually edit the generated alltables.sql file to reflect any changes.</span></span>

### <a name="additional-reading"></a><span data-ttu-id="30560-115">Lecturas adicionales</span><span class="sxs-lookup"><span data-stu-id="30560-115">Additional reading</span></span>

- [<span data-ttu-id="30560-116">Conexión a través de SSH con HDInsight (Hadoop)</span><span class="sxs-lookup"><span data-stu-id="30560-116">Connect to an HDInsight cluster by using SSH</span></span>](hdinsight-hadoop-linux-use-ssh-unix.md)


## <a name="how-do-i-locate-hive-logs-on-a-cluster"></a><span data-ttu-id="30560-117">Búsqueda de registros de Hive en un clúster</span><span class="sxs-lookup"><span data-stu-id="30560-117">How do I locate Hive logs on a cluster</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="30560-118">Pasos de la solución</span><span class="sxs-lookup"><span data-stu-id="30560-118">Resolution steps</span></span>

1. <span data-ttu-id="30560-119">Conéctese al clúster de HDInsight con SSH.</span><span class="sxs-lookup"><span data-stu-id="30560-119">Connect to the HDInsight cluster by using SSH.</span></span> <span data-ttu-id="30560-120">Para más información, consulte **Lecturas adicionales**.</span><span class="sxs-lookup"><span data-stu-id="30560-120">For more information, see **Additional reading**.</span></span>

2. <span data-ttu-id="30560-121">Para ver los registros de cliente de Hive, use el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="30560-121">To view Hive client logs, use the following command:</span></span>

  ```apache
  /tmp/<username>/hive.log 
  ```

3. <span data-ttu-id="30560-122">Para ver los registros de Hive Metastore, use el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="30560-122">To view Hive metastore logs, use the following command:</span></span>

  ```apache
  /var/log/hive/hivemetastore.log 
  ```

4. <span data-ttu-id="30560-123">Para ver los registros de HiveServer, use el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="30560-123">To view Hiveserver logs, use the following command:</span></span>

  ```apache
  /var/log/hive/hiveserver2.log 
  ```

### <a name="additional-reading"></a><span data-ttu-id="30560-124">Lecturas adicionales</span><span class="sxs-lookup"><span data-stu-id="30560-124">Additional reading</span></span>

- [<span data-ttu-id="30560-125">Conexión a través de SSH con HDInsight (Hadoop)</span><span class="sxs-lookup"><span data-stu-id="30560-125">Connect to an HDInsight cluster by using SSH</span></span>](hdinsight-hadoop-linux-use-ssh-unix.md)


## <a name="how-do-i-launch-the-hive-shell-with-specific-configurations-on-a-cluster"></a><span data-ttu-id="30560-126">Inicio del shell de Hive con configuraciones específicas en un clúster</span><span class="sxs-lookup"><span data-stu-id="30560-126">How do I launch the Hive shell with specific configurations on a cluster</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="30560-127">Pasos de la solución</span><span class="sxs-lookup"><span data-stu-id="30560-127">Resolution steps</span></span>

1. <span data-ttu-id="30560-128">Especifique un par clave-valor de configuración cuando inicie el shell de Hive.</span><span class="sxs-lookup"><span data-stu-id="30560-128">Specify a configuration key-value pair when you start the Hive shell.</span></span> <span data-ttu-id="30560-129">Para más información, consulte [Lecturas adicionales](#additional-reading-end).</span><span class="sxs-lookup"><span data-stu-id="30560-129">For more information, see [Additional reading](#additional-reading-end).</span></span>

  ```apache
  hive -hiveconf a=b 
  ```

2. <span data-ttu-id="30560-130">Para enumerar todas las configuraciones efectivas en el shell de Hive, use el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="30560-130">To list all effective configurations on Hive shell, use the following command:</span></span>

  ```apache
  hive> set;
  ```

  <span data-ttu-id="30560-131">Por ejemplo, utilice el siguiente comando para iniciar el shell de Hive con el registro de depuración habilitado en la consola:</span><span class="sxs-lookup"><span data-stu-id="30560-131">For example, use the following command to start Hive shell with debug logging enabled on the console:</span></span>

  ```apache
  hive -hiveconf hive.root.logger=ALL,console 
  ```

### <a name="additional-reading"></a><span data-ttu-id="30560-132">Lecturas adicionales</span><span class="sxs-lookup"><span data-stu-id="30560-132">Additional reading</span></span>

- [<span data-ttu-id="30560-133">Propiedades de configuración de Hive</span><span class="sxs-lookup"><span data-stu-id="30560-133">Hive configuration properties</span></span>](https://cwiki.apache.org/confluence/display/Hive/Configuration+Properties)


## <span data-ttu-id="30560-134"><a name="how-do-i-analyze-tez-dag-data-on-a-cluster-critical-path"></a>Análisis de datos DAG de Tez en una ruta crítica de clúster</span><span class="sxs-lookup"><span data-stu-id="30560-134"><a name="how-do-i-analyze-tez-dag-data-on-a-cluster-critical-path"></a>How do I analyze Tez DAG data on a cluster-critical path</span></span>


### <a name="resolution-steps"></a><span data-ttu-id="30560-135">Pasos de la solución</span><span class="sxs-lookup"><span data-stu-id="30560-135">Resolution steps</span></span>
 
1. <span data-ttu-id="30560-136">Para analizar un gráfico acíclico dirigido (DAG) de Apache Tez en un grafo crítico para el clúster, conéctese al clúster de HDInsight con SSH.</span><span class="sxs-lookup"><span data-stu-id="30560-136">To analyze an Apache Tez directed acyclic graph (DAG) on a cluster-critical graph, connect to the HDInsight cluster by using SSH.</span></span> <span data-ttu-id="30560-137">Para más información, consulte [Lecturas adicionales](#additional-reading-end).</span><span class="sxs-lookup"><span data-stu-id="30560-137">For more information, see [Additional reading](#additional-reading-end).</span></span>

2. <span data-ttu-id="30560-138">En el símbolo del sistema, ejecute el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="30560-138">At a command prompt, run the following command:</span></span>
   
  ```apache
  hadoop jar /usr/hdp/current/tez-client/tez-job-analyzer-*.jar CriticalPath --saveResults --dagId <DagId> --eventFileName <DagData.zip> 
  ```

3. <span data-ttu-id="30560-139">Para enumerar otros analizadores que pueden usarse para analizar DAG de Tez, utilice el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="30560-139">To list other analyzers that can be used to analyze Tez DAG, use the following command:</span></span>

  ```apache
  hadoop jar /usr/hdp/current/tez-client/tez-job-analyzer-*.jar
  ```

  <span data-ttu-id="30560-140">Debe proporcionar un programa de ejemplo como el primer argumento.</span><span class="sxs-lookup"><span data-stu-id="30560-140">You must provide an example program as the first argument.</span></span>

  <span data-ttu-id="30560-141">Los nombres de programa válidos incluyen:</span><span class="sxs-lookup"><span data-stu-id="30560-141">Valid program names include:</span></span>
    - <span data-ttu-id="30560-142">**ContainerReuseAnalyzer**: imprima los detalles de la reutilización del contenedor en un DAG.</span><span class="sxs-lookup"><span data-stu-id="30560-142">**ContainerReuseAnalyzer**: Print container reuse details in a DAG</span></span>
    - <span data-ttu-id="30560-143">**CriticalPath**: busque la ruta crítica de un DAG.</span><span class="sxs-lookup"><span data-stu-id="30560-143">**CriticalPath**: Find the critical path of a DAG</span></span>
    - <span data-ttu-id="30560-144">**LocalityAnalyzer**: imprima los detalles de localidad en un DAG.</span><span class="sxs-lookup"><span data-stu-id="30560-144">**LocalityAnalyzer**: Print locality details in a DAG</span></span>
    - <span data-ttu-id="30560-145">**ShuffleTimeAnalyzer**: analice los detalles de tiempo de orden aleatorio en un DAG.</span><span class="sxs-lookup"><span data-stu-id="30560-145">**ShuffleTimeAnalyzer**: Analyze the shuffle time details in a DAG</span></span>
    - <span data-ttu-id="30560-146">**SkewAnalyzer**: analice los detalles de sesgo en un DAG.</span><span class="sxs-lookup"><span data-stu-id="30560-146">**SkewAnalyzer**: Analyze the skew details in a DAG</span></span>
    - <span data-ttu-id="30560-147">**SlowNodeAnalyzer**: imprima los detalles del nodo en un DAG.</span><span class="sxs-lookup"><span data-stu-id="30560-147">**SlowNodeAnalyzer**: Print node details in a DAG</span></span>
    - <span data-ttu-id="30560-148">**SlowTaskIdentifier**: imprima los detalles de una tarea lenta en un DAG.</span><span class="sxs-lookup"><span data-stu-id="30560-148">**SlowTaskIdentifier**: Print slow task details in a DAG</span></span>
    - <span data-ttu-id="30560-149">**SlowestVertexAnalyzer**: imprima los detalles de los vértices más lentos en un DAG.</span><span class="sxs-lookup"><span data-stu-id="30560-149">**SlowestVertexAnalyzer**: Print slowest vertex details in a DAG</span></span>
    - <span data-ttu-id="30560-150">**SpillAnalyzer**: imprima los detalles de desbordamiento en un DAG.</span><span class="sxs-lookup"><span data-stu-id="30560-150">**SpillAnalyzer**: Print spill details in a DAG</span></span>
    - <span data-ttu-id="30560-151">**TaskConcurrencyAnalyzer**: imprima los detalles de la simultaneidad de tareas en un DAG.</span><span class="sxs-lookup"><span data-stu-id="30560-151">**TaskConcurrencyAnalyzer**: Print the task concurrency details in a DAG</span></span>
    - <span data-ttu-id="30560-152">**VertexLevelCriticalPathAnalyzer**: busque la ruta crítica en el nivel de vértices en un DAG.</span><span class="sxs-lookup"><span data-stu-id="30560-152">**VertexLevelCriticalPathAnalyzer**: Find the critical path at vertex level in a DAG</span></span>


### <a name="additional-reading"></a><span data-ttu-id="30560-153">Lecturas adicionales</span><span class="sxs-lookup"><span data-stu-id="30560-153">Additional reading</span></span>

- [<span data-ttu-id="30560-154">Conexión a través de SSH con HDInsight (Hadoop)</span><span class="sxs-lookup"><span data-stu-id="30560-154">Connect to an HDInsight cluster by using SSH</span></span>](hdinsight-hadoop-linux-use-ssh-unix.md)


## <a name="how-do-i-download-tez-dag-data-from-a-cluster"></a><span data-ttu-id="30560-155">Cómo se descargan datos de DAG de Tez de un clúster</span><span class="sxs-lookup"><span data-stu-id="30560-155">How do I download Tez DAG data from a cluster</span></span>


#### <a name="resolution-steps"></a><span data-ttu-id="30560-156">Pasos de la solución</span><span class="sxs-lookup"><span data-stu-id="30560-156">Resolution steps</span></span>

<span data-ttu-id="30560-157">Hay dos maneras de recopilar los datos de DAG de Tez.</span><span class="sxs-lookup"><span data-stu-id="30560-157">There are two ways to collect the Tez DAG data:</span></span>

- <span data-ttu-id="30560-158">Desde la línea de comandos:</span><span class="sxs-lookup"><span data-stu-id="30560-158">From the command line:</span></span>
 
    <span data-ttu-id="30560-159">Conéctese al clúster de HDInsight con SSH.</span><span class="sxs-lookup"><span data-stu-id="30560-159">Connect to the HDInsight cluster by using SSH.</span></span> <span data-ttu-id="30560-160">En el símbolo del sistema, ejecute el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="30560-160">At the command prompt, run the following command:</span></span>

  ```apache
  hadoop jar /usr/hdp/current/tez-client/tez-history-parser-*.jar org.apache.tez.history.ATSImportTool -downloadDir . -dagId <DagId> 
  ```

- <span data-ttu-id="30560-161">Use la vista de Tez de Ambari:</span><span class="sxs-lookup"><span data-stu-id="30560-161">Use the Ambari Tez view:</span></span>
   
  1. <span data-ttu-id="30560-162">Vaya a Ambari.</span><span class="sxs-lookup"><span data-stu-id="30560-162">Go to Ambari.</span></span> 
  2. <span data-ttu-id="30560-163">Vaya a la vista de Tez (en el icono de la esquina superior derecha).</span><span class="sxs-lookup"><span data-stu-id="30560-163">Go to Tez view (under the tiles icon in the upper-right corner).</span></span> 
  3. <span data-ttu-id="30560-164">Seleccione el DAG que desea ver.</span><span class="sxs-lookup"><span data-stu-id="30560-164">Select the DAG you want to view.</span></span>
  4. <span data-ttu-id="30560-165">Seleccione **Descargar datos**.</span><span class="sxs-lookup"><span data-stu-id="30560-165">Select **Download data**.</span></span>

### <span data-ttu-id="30560-166"><a name="additional-reading-end"></a>Lecturas adicionales</span><span class="sxs-lookup"><span data-stu-id="30560-166"><a name="additional-reading-end"></a>Additional reading</span></span>

[<span data-ttu-id="30560-167">Conexión a través de SSH con HDInsight (Hadoop)</span><span class="sxs-lookup"><span data-stu-id="30560-167">Connect to an HDInsight cluster by using SSH</span></span>](hdinsight-hadoop-linux-use-ssh-unix.md)






