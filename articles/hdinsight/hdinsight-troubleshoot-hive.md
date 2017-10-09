---
title: "aaaTroubleshoot subárbol mediante el uso de HDInsight de Azure | Documentos de Microsoft"
description: "Obtenga respuestas toocommon preguntas sobre cómo trabajar con Apache Hive y HDInsight de Azure."
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
ms.openlocfilehash: ac459316e658d0b29eb66f5685f0bc7e693bb277
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-hive-by-using-azure-hdinsight"></a><span data-ttu-id="2eb1f-104">Solución de problemas de Hive mediante Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="2eb1f-104">Troubleshoot Hive by using Azure HDInsight</span></span>

<span data-ttu-id="2eb1f-105">Obtenga información sobre preguntas más frecuentes de Hola y sus soluciones cuando se trabaja con cargas Apache Hive en Apache Ambari.</span><span class="sxs-lookup"><span data-stu-id="2eb1f-105">Learn about hello top questions and their resolutions when working with Apache Hive payloads in Apache Ambari.</span></span>


## <a name="how-do-i-export-a-hive-metastore-and-import-it-on-another-cluster"></a><span data-ttu-id="2eb1f-106">¿Cómo se exporta Hive Metastore y se importa en otro clúster?</span><span class="sxs-lookup"><span data-stu-id="2eb1f-106">How do I export a Hive metastore and import it on another cluster</span></span>


### <a name="resolution-steps"></a><span data-ttu-id="2eb1f-107">Pasos de la solución</span><span class="sxs-lookup"><span data-stu-id="2eb1f-107">Resolution steps</span></span>

1. <span data-ttu-id="2eb1f-108">Conecta el clúster de HDInsight de toohello con un cliente de Shell seguro (SSH).</span><span class="sxs-lookup"><span data-stu-id="2eb1f-108">Connect toohello HDInsight cluster by using a Secure Shell (SSH) client.</span></span> <span data-ttu-id="2eb1f-109">Para más información, consulte [Lecturas adicionales](#additional-reading-end).</span><span class="sxs-lookup"><span data-stu-id="2eb1f-109">For more information, see [Additional reading](#additional-reading-end).</span></span>

2. <span data-ttu-id="2eb1f-110">Ejecute hello siguiente comando en clúster de HDInsight de Hola desde el que desea que tienda de metadatos de Hola tooexport:</span><span class="sxs-lookup"><span data-stu-id="2eb1f-110">Run hello following command on hello HDInsight cluster from which you want tooexport hello metastore:</span></span>

    ```apache
    for d in `hive -e "show databases"`; do echo "create database $d; use $d;" >> alltables.sql ; for t in `hive --database $d -e "show tables"` ; do ddl=`hive --database $d -e "show create table $t"`; echo "$ddl ;" >> alltables.sql ; echo "$ddl" | grep -q "PARTITIONED\s*BY" && echo "MSCK REPAIR TABLE $t ;" >> alltables.sql ; done; done
    ```

  <span data-ttu-id="2eb1f-111">Este comando genera un archivo denominado allatables.sql.</span><span class="sxs-lookup"><span data-stu-id="2eb1f-111">This command generates a file named allatables.sql.</span></span>

3. <span data-ttu-id="2eb1f-112">Copie Hola archivo alltables.sql toohello nuevo clúster de HDInsight y, a continuación, ejecute el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="2eb1f-112">Copy hello file alltables.sql toohello new HDInsight cluster, and then run hello following command:</span></span>

  ```apache
  hive -f alltables.sql
  ```

<span data-ttu-id="2eb1f-113">código de Hello en los pasos de resolución de Hola se da por supuesto que las rutas de acceso en el nuevo clúster de Hola de datos mismo Hola como rutas de acceso de datos de hello en el clúster antiguo Hola.</span><span class="sxs-lookup"><span data-stu-id="2eb1f-113">hello code in hello resolution steps assumes that data paths on hello new cluster are hello same as hello data paths on hello old cluster.</span></span> <span data-ttu-id="2eb1f-114">Si las rutas de acceso de datos de hello son diferentes, puede editar manualmente Hola genera alltables.sql archivo tooreflect los cambios.</span><span class="sxs-lookup"><span data-stu-id="2eb1f-114">If hello data paths are different, you can manually edit hello generated alltables.sql file tooreflect any changes.</span></span>

### <a name="additional-reading"></a><span data-ttu-id="2eb1f-115">Lecturas adicionales</span><span class="sxs-lookup"><span data-stu-id="2eb1f-115">Additional reading</span></span>

- [<span data-ttu-id="2eb1f-116">Conecta el clúster de HDInsight de tooan a través de SSH</span><span class="sxs-lookup"><span data-stu-id="2eb1f-116">Connect tooan HDInsight cluster by using SSH</span></span>](hdinsight-hadoop-linux-use-ssh-unix.md)


## <a name="how-do-i-locate-hive-logs-on-a-cluster"></a><span data-ttu-id="2eb1f-117">Búsqueda de registros de Hive en un clúster</span><span class="sxs-lookup"><span data-stu-id="2eb1f-117">How do I locate Hive logs on a cluster</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="2eb1f-118">Pasos de la solución</span><span class="sxs-lookup"><span data-stu-id="2eb1f-118">Resolution steps</span></span>

1. <span data-ttu-id="2eb1f-119">Conecte el clúster de HDInsight toohello a través de SSH.</span><span class="sxs-lookup"><span data-stu-id="2eb1f-119">Connect toohello HDInsight cluster by using SSH.</span></span> <span data-ttu-id="2eb1f-120">Para más información, consulte **Lecturas adicionales**.</span><span class="sxs-lookup"><span data-stu-id="2eb1f-120">For more information, see **Additional reading**.</span></span>

2. <span data-ttu-id="2eb1f-121">registros de cliente de tooview Hive, utilice Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="2eb1f-121">tooview Hive client logs, use hello following command:</span></span>

  ```apache
  /tmp/<username>/hive.log 
  ```

3. <span data-ttu-id="2eb1f-122">registros de tienda de metadatos de Hive tooview, usar hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="2eb1f-122">tooview Hive metastore logs, use hello following command:</span></span>

  ```apache
  /var/log/hive/hivemetastore.log 
  ```

4. <span data-ttu-id="2eb1f-123">tooview Hiveserver registros, utilice Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="2eb1f-123">tooview Hiveserver logs, use hello following command:</span></span>

  ```apache
  /var/log/hive/hiveserver2.log 
  ```

### <a name="additional-reading"></a><span data-ttu-id="2eb1f-124">Lecturas adicionales</span><span class="sxs-lookup"><span data-stu-id="2eb1f-124">Additional reading</span></span>

- [<span data-ttu-id="2eb1f-125">Conecta el clúster de HDInsight de tooan a través de SSH</span><span class="sxs-lookup"><span data-stu-id="2eb1f-125">Connect tooan HDInsight cluster by using SSH</span></span>](hdinsight-hadoop-linux-use-ssh-unix.md)


## <a name="how-do-i-launch-hello-hive-shell-with-specific-configurations-on-a-cluster"></a><span data-ttu-id="2eb1f-126">Cómo se puede iniciar Hola shell de Hive con configuraciones específicas en un clúster</span><span class="sxs-lookup"><span data-stu-id="2eb1f-126">How do I launch hello Hive shell with specific configurations on a cluster</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="2eb1f-127">Pasos de la solución</span><span class="sxs-lookup"><span data-stu-id="2eb1f-127">Resolution steps</span></span>

1. <span data-ttu-id="2eb1f-128">Especificar un par de clave y valor de configuración cuando se inicia Hola shell de Hive.</span><span class="sxs-lookup"><span data-stu-id="2eb1f-128">Specify a configuration key-value pair when you start hello Hive shell.</span></span> <span data-ttu-id="2eb1f-129">Para más información, consulte [Lecturas adicionales](#additional-reading-end).</span><span class="sxs-lookup"><span data-stu-id="2eb1f-129">For more information, see [Additional reading](#additional-reading-end).</span></span>

  ```apache
  hive -hiveconf a=b 
  ```

2. <span data-ttu-id="2eb1f-130">toolist de comandos de todas las configuraciones efectivo en shell de Hive, Hola de uso después de:</span><span class="sxs-lookup"><span data-stu-id="2eb1f-130">toolist all effective configurations on Hive shell, use hello following command:</span></span>

  ```apache
  hive> set;
  ```

  <span data-ttu-id="2eb1f-131">Por ejemplo, usar hello siguiendo el shell de comandos toostart Hive con el registro de depuración habilitado en la consola de hello:</span><span class="sxs-lookup"><span data-stu-id="2eb1f-131">For example, use hello following command toostart Hive shell with debug logging enabled on hello console:</span></span>

  ```apache
  hive -hiveconf hive.root.logger=ALL,console 
  ```

### <a name="additional-reading"></a><span data-ttu-id="2eb1f-132">Lecturas adicionales</span><span class="sxs-lookup"><span data-stu-id="2eb1f-132">Additional reading</span></span>

- [<span data-ttu-id="2eb1f-133">Propiedades de configuración de Hive</span><span class="sxs-lookup"><span data-stu-id="2eb1f-133">Hive configuration properties</span></span>](https://cwiki.apache.org/confluence/display/Hive/Configuration+Properties)


## <span data-ttu-id="2eb1f-134"><a name="how-do-i-analyze-tez-dag-data-on-a-cluster-critical-path"></a>Análisis de datos DAG de Tez en una ruta crítica de clúster</span><span class="sxs-lookup"><span data-stu-id="2eb1f-134"><a name="how-do-i-analyze-tez-dag-data-on-a-cluster-critical-path"></a>How do I analyze Tez DAG data on a cluster-critical path</span></span>


### <a name="resolution-steps"></a><span data-ttu-id="2eb1f-135">Pasos de la solución</span><span class="sxs-lookup"><span data-stu-id="2eb1f-135">Resolution steps</span></span>
 
1. <span data-ttu-id="2eb1f-136">tooanalyze una Tez Apache dirige gráfico acíclico (DAG) en un gráfico de clúster crítico, clúster de HDInsight de toohello se conectan a través de SSH.</span><span class="sxs-lookup"><span data-stu-id="2eb1f-136">tooanalyze an Apache Tez directed acyclic graph (DAG) on a cluster-critical graph, connect toohello HDInsight cluster by using SSH.</span></span> <span data-ttu-id="2eb1f-137">Para más información, consulte [Lecturas adicionales](#additional-reading-end).</span><span class="sxs-lookup"><span data-stu-id="2eb1f-137">For more information, see [Additional reading](#additional-reading-end).</span></span>

2. <span data-ttu-id="2eb1f-138">En un símbolo del sistema, ejecute hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="2eb1f-138">At a command prompt, run hello following command:</span></span>
   
  ```apache
  hadoop jar /usr/hdp/current/tez-client/tez-job-analyzer-*.jar CriticalPath --saveResults --dagId <DagId> --eventFileName <DagData.zip> 
  ```

3. <span data-ttu-id="2eb1f-139">toolist otros analizadores que pueden ser utilizado tooanalyze Tez DAG, usar hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="2eb1f-139">toolist other analyzers that can be used tooanalyze Tez DAG, use hello following command:</span></span>

  ```apache
  hadoop jar /usr/hdp/current/tez-client/tez-job-analyzer-*.jar
  ```

  <span data-ttu-id="2eb1f-140">Debe proporcionar un programa de ejemplo como primer argumento de Hola.</span><span class="sxs-lookup"><span data-stu-id="2eb1f-140">You must provide an example program as hello first argument.</span></span>

  <span data-ttu-id="2eb1f-141">Los nombres de programa válidos incluyen:</span><span class="sxs-lookup"><span data-stu-id="2eb1f-141">Valid program names include:</span></span>
    - <span data-ttu-id="2eb1f-142">**ContainerReuseAnalyzer**: imprima los detalles de la reutilización del contenedor en un DAG.</span><span class="sxs-lookup"><span data-stu-id="2eb1f-142">**ContainerReuseAnalyzer**: Print container reuse details in a DAG</span></span>
    - <span data-ttu-id="2eb1f-143">**CriticalPath**: ruta crítica de Hola de búsqueda de un DAG</span><span class="sxs-lookup"><span data-stu-id="2eb1f-143">**CriticalPath**: Find hello critical path of a DAG</span></span>
    - <span data-ttu-id="2eb1f-144">**LocalityAnalyzer**: imprima los detalles de localidad en un DAG.</span><span class="sxs-lookup"><span data-stu-id="2eb1f-144">**LocalityAnalyzer**: Print locality details in a DAG</span></span>
    - <span data-ttu-id="2eb1f-145">**ShuffleTimeAnalyzer**: analizar los detalles de tiempo de hello orden aleatorio en un DAG</span><span class="sxs-lookup"><span data-stu-id="2eb1f-145">**ShuffleTimeAnalyzer**: Analyze hello shuffle time details in a DAG</span></span>
    - <span data-ttu-id="2eb1f-146">**SkewAnalyzer**: analizar los detalles sesgo de hello en un DAG</span><span class="sxs-lookup"><span data-stu-id="2eb1f-146">**SkewAnalyzer**: Analyze hello skew details in a DAG</span></span>
    - <span data-ttu-id="2eb1f-147">**SlowNodeAnalyzer**: imprima los detalles del nodo en un DAG.</span><span class="sxs-lookup"><span data-stu-id="2eb1f-147">**SlowNodeAnalyzer**: Print node details in a DAG</span></span>
    - <span data-ttu-id="2eb1f-148">**SlowTaskIdentifier**: imprima los detalles de una tarea lenta en un DAG.</span><span class="sxs-lookup"><span data-stu-id="2eb1f-148">**SlowTaskIdentifier**: Print slow task details in a DAG</span></span>
    - <span data-ttu-id="2eb1f-149">**SlowestVertexAnalyzer**: imprima los detalles de los vértices más lentos en un DAG.</span><span class="sxs-lookup"><span data-stu-id="2eb1f-149">**SlowestVertexAnalyzer**: Print slowest vertex details in a DAG</span></span>
    - <span data-ttu-id="2eb1f-150">**SpillAnalyzer**: imprima los detalles de desbordamiento en un DAG.</span><span class="sxs-lookup"><span data-stu-id="2eb1f-150">**SpillAnalyzer**: Print spill details in a DAG</span></span>
    - <span data-ttu-id="2eb1f-151">**TaskConcurrencyAnalyzer**: imprimir los detalles de simultaneidad de la tarea de hello en un DAG</span><span class="sxs-lookup"><span data-stu-id="2eb1f-151">**TaskConcurrencyAnalyzer**: Print hello task concurrency details in a DAG</span></span>
    - <span data-ttu-id="2eb1f-152">**VertexLevelCriticalPathAnalyzer**: ruta crítica de Hola de búsqueda en el nivel de vértices en un DAG</span><span class="sxs-lookup"><span data-stu-id="2eb1f-152">**VertexLevelCriticalPathAnalyzer**: Find hello critical path at vertex level in a DAG</span></span>


### <a name="additional-reading"></a><span data-ttu-id="2eb1f-153">Lecturas adicionales</span><span class="sxs-lookup"><span data-stu-id="2eb1f-153">Additional reading</span></span>

- [<span data-ttu-id="2eb1f-154">Conecta el clúster de HDInsight de tooan a través de SSH</span><span class="sxs-lookup"><span data-stu-id="2eb1f-154">Connect tooan HDInsight cluster by using SSH</span></span>](hdinsight-hadoop-linux-use-ssh-unix.md)


## <a name="how-do-i-download-tez-dag-data-from-a-cluster"></a><span data-ttu-id="2eb1f-155">Cómo se descargan datos de DAG de Tez de un clúster</span><span class="sxs-lookup"><span data-stu-id="2eb1f-155">How do I download Tez DAG data from a cluster</span></span>


#### <a name="resolution-steps"></a><span data-ttu-id="2eb1f-156">Pasos de la solución</span><span class="sxs-lookup"><span data-stu-id="2eb1f-156">Resolution steps</span></span>

<span data-ttu-id="2eb1f-157">Hay dos formas de datos de Tez DAG Hola toocollect:</span><span class="sxs-lookup"><span data-stu-id="2eb1f-157">There are two ways toocollect hello Tez DAG data:</span></span>

- <span data-ttu-id="2eb1f-158">Desde la línea de comandos de hello:</span><span class="sxs-lookup"><span data-stu-id="2eb1f-158">From hello command line:</span></span>
 
    <span data-ttu-id="2eb1f-159">Conecte el clúster de HDInsight toohello a través de SSH.</span><span class="sxs-lookup"><span data-stu-id="2eb1f-159">Connect toohello HDInsight cluster by using SSH.</span></span> <span data-ttu-id="2eb1f-160">En el símbolo de hello, ejecute hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="2eb1f-160">At hello command prompt, run hello following command:</span></span>

  ```apache
  hadoop jar /usr/hdp/current/tez-client/tez-history-parser-*.jar org.apache.tez.history.ATSImportTool -downloadDir . -dagId <DagId> 
  ```

- <span data-ttu-id="2eb1f-161">Usar hello Ambari Tez vista:</span><span class="sxs-lookup"><span data-stu-id="2eb1f-161">Use hello Ambari Tez view:</span></span>
   
  1. <span data-ttu-id="2eb1f-162">Vaya tooAmbari.</span><span class="sxs-lookup"><span data-stu-id="2eb1f-162">Go tooAmbari.</span></span> 
  2. <span data-ttu-id="2eb1f-163">Vista de tooTez vaya (bajo el icono de mosaicos de hello en la esquina superior derecha de hello).</span><span class="sxs-lookup"><span data-stu-id="2eb1f-163">Go tooTez view (under hello tiles icon in hello upper-right corner).</span></span> 
  3. <span data-ttu-id="2eb1f-164">Seleccione Hola DAG desea tooview.</span><span class="sxs-lookup"><span data-stu-id="2eb1f-164">Select hello DAG you want tooview.</span></span>
  4. <span data-ttu-id="2eb1f-165">Seleccione **Descargar datos**.</span><span class="sxs-lookup"><span data-stu-id="2eb1f-165">Select **Download data**.</span></span>

### <span data-ttu-id="2eb1f-166"><a name="additional-reading-end"></a>Lecturas adicionales</span><span class="sxs-lookup"><span data-stu-id="2eb1f-166"><a name="additional-reading-end"></a>Additional reading</span></span>

[<span data-ttu-id="2eb1f-167">Conecta el clúster de HDInsight de tooan a través de SSH</span><span class="sxs-lookup"><span data-stu-id="2eb1f-167">Connect tooan HDInsight cluster by using SSH</span></span>](hdinsight-hadoop-linux-use-ssh-unix.md)






