---
title: "guías de solución de problemas de HDInsight de aaaAzure | Documentos de Microsoft"
description: "Solucione problemas de cargas de trabajo de Hadoop con Azure HDInsight. Documentación paso a paso muestra cómo toouse HDInsight toosolve problemas comunes de Hive, Spark, YARN, HBase, HDFS y Storm."
services: hdinsight
author: arijitt
manager: arijitt
layout: LandingPage
ms.assetid: 
ms.service: hdinsight
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: landing - page
ms.date: 7/06/2017
ms.author: arijitt
ms.openlocfilehash: 6d801389cba738345b36364302c62008b8318018
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-by-using-azure-hdinsight"></a><span data-ttu-id="2b241-104">Solución de problemas mediante Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="2b241-104">Troubleshoot by using Azure HDInsight</span></span>

| <span data-ttu-id="2b241-105">Carga de trabajo de Apache</span><span class="sxs-lookup"><span data-stu-id="2b241-105">Apache workload</span></span> | <span data-ttu-id="2b241-106">Preguntas más frecuentes</span><span class="sxs-lookup"><span data-stu-id="2b241-106">Top questions</span></span> |
|---|---|
|<span data-ttu-id="2b241-107">![HBase](./media/hdinsight-troubleshoot-guide/HBASE.png)</span><span class="sxs-lookup"><span data-stu-id="2b241-107">![HBase](./media/hdinsight-troubleshoot-guide/HBASE.png)</span></span><br>[<span data-ttu-id="2b241-108">Solución de problemas de HBase</span><span class="sxs-lookup"><span data-stu-id="2b241-108">Troubleshoot HBase</span></span>](hdinsight-troubleshoot-hbase.md)|<br>[<span data-ttu-id="2b241-109">Cómo se ejecutan informes de comando hbck con varias regiones sin asignar</span><span class="sxs-lookup"><span data-stu-id="2b241-109">How do I run hbck command reports with multiple unassigned regions</span></span>](hdinsight-troubleshoot-hbase.md#how-do-i-run-hbck-command-reports-with-multiple-unassigned-regions)<br><br>[<span data-ttu-id="2b241-110">Cómo solucionar problemas de tiempo de espera con comandos hbck para las asignaciones de regiones</span><span class="sxs-lookup"><span data-stu-id="2b241-110">How do I fix timeout issues when using hbck commands for region assignments</span></span>](hdinsight-troubleshoot-hbase.md#how-do-i-fix-timeout-issues-with-hbck-commands-for-region-assignments)<br><br>[<span data-ttu-id="2b241-111">Cómo forzar la deshabilitación del modo seguro de HDFS en un clúster</span><span class="sxs-lookup"><span data-stu-id="2b241-111">How do I force-disable HDFS safe mode on a cluster</span></span>](hdinsight-troubleshoot-hbase.md#how-do-i-force-disable-hdfs-safe-mode-in-a-cluster)<br><br>[<span data-ttu-id="2b241-112">Cómo se solucionan problemas de conectividad de JDBC o SQLLine con Apache Phoenix</span><span class="sxs-lookup"><span data-stu-id="2b241-112">How do I fix JDBC or SQLLine connectivity issues with Apache Phoenix</span></span>](hdinsight-troubleshoot-hbase.md#how-do-i-fix-jdbc-or-sqlline-connectivity-issues-with-apache-phoenix)<br><br>[<span data-ttu-id="2b241-113">¿Qué hace que un servidor maestro toofail toostart</span><span class="sxs-lookup"><span data-stu-id="2b241-113">What causes a master server toofail toostart</span></span>](hdinsight-troubleshoot-hbase.md#what-causes-a-master-server-to-fail-to-start)<br><br>[<span data-ttu-id="2b241-114">Qué provoca un error de reinicio en un servidor de regiones</span><span class="sxs-lookup"><span data-stu-id="2b241-114">What causes a restart failure on a region server</span></span>](hdinsight-troubleshoot-hbase.md#what-causes-a-restart-failure-on-a-region-server)|
|<span data-ttu-id="2b241-115">![HDFS](./media/hdinsight-troubleshoot-guide/HDFS.png)</span><span class="sxs-lookup"><span data-stu-id="2b241-115">![HDFS](./media/hdinsight-troubleshoot-guide/HDFS.png)</span></span><br>[<span data-ttu-id="2b241-116">Solución de problemas de HDFS</span><span class="sxs-lookup"><span data-stu-id="2b241-116">Troubleshoot HDFS</span></span>](hdinsight-troubleshoot-hdfs.md)|<br>[<span data-ttu-id="2b241-117">Cómo se accede a la instancia de HDFS local desde un clúster</span><span class="sxs-lookup"><span data-stu-id="2b241-117">How do I access a local HDFS from inside a cluster</span></span>](hdinsight-troubleshoot-hdfs.md#how-do-i-access-local-hdfs-from-inside-a-cluster)<br><br>[<span data-ttu-id="2b241-118">Cómo forzar la deshabilitación del modo seguro de HDFS en un clúster</span><span class="sxs-lookup"><span data-stu-id="2b241-118">How do I force-disable HDFS safe mode on a cluster</span></span>](hdinsight-troubleshoot-hdfs.md#how-do-i-force-disable-hdfs-safe-mode-in-a-cluster)|
|<span data-ttu-id="2b241-119">![Hive](./media/hdinsight-troubleshoot-guide/HIVE.png)</span><span class="sxs-lookup"><span data-stu-id="2b241-119">![Hive](./media/hdinsight-troubleshoot-guide/HIVE.png)</span></span><br>[<span data-ttu-id="2b241-120">Solución de problemas de HBase</span><span class="sxs-lookup"><span data-stu-id="2b241-120">Troubleshoot HBase</span></span>](hdinsight-troubleshoot-hive.md)|<br><span data-ttu-id="2b241-121">[How do I export a Hive metastore and import it on another cluster](hdinsight-troubleshoot-hive.md#how-do-i-export-a-hive-metastore-and-import-it-on-another-cluster) (Cómo se explota Hive Metastore y se importa en otro clúster)</span><span class="sxs-lookup"><span data-stu-id="2b241-121">[How do I export a Hive metastore and import it on another cluster](hdinsight-troubleshoot-hive.md#how-do-i-export-a-hive-metastore-and-import-it-on-another-cluster)</span></span><br><br>[<span data-ttu-id="2b241-122">Búsqueda de registros de Hive en un clúster</span><span class="sxs-lookup"><span data-stu-id="2b241-122">How do I locate Hive logs on a cluster</span></span>](hdinsight-troubleshoot-hive.md#how-do-i-locate-hive-logs-on-a-cluster)<br><br>[<span data-ttu-id="2b241-123">Cómo se puede iniciar Hola shell de Hive con configuraciones específicas en un clúster</span><span class="sxs-lookup"><span data-stu-id="2b241-123">How do I launch hello Hive shell with specific configurations on a cluster</span></span>](hdinsight-troubleshoot-hive.md#how-do-i-launch-the-hive-shell-with-specific-configurations-on-a-cluster)<br><br>[<span data-ttu-id="2b241-124">¿Cómo se analizan datos de DAG de Tez en una ruta crítica de clúster?</span><span class="sxs-lookup"><span data-stu-id="2b241-124">How do I analyze Tez DAG data on a cluster-critical path</span></span>](hdinsight-troubleshoot-hive.md#how-do-i-analyze-tez-dag-data-on-a-cluster-critical-path)<br><br><span data-ttu-id="2b241-125">[How do I download Tez DAG data from a cluster](hdinsight-troubleshoot-hive.md#how-do-i-download-tez-dag-data-from-a-cluster) (Cómo se descargan datos de Tez DAG desde un clúster)</span><span class="sxs-lookup"><span data-stu-id="2b241-125">[How do I download Tez DAG data from a cluster](hdinsight-troubleshoot-hive.md#how-do-i-download-tez-dag-data-from-a-cluster)</span></span>|
|<span data-ttu-id="2b241-126">![Spark](./media/hdinsight-troubleshoot-guide/SPARK.png)</span><span class="sxs-lookup"><span data-stu-id="2b241-126">![Spark](./media/hdinsight-troubleshoot-guide/SPARK.png)</span></span><br>[<span data-ttu-id="2b241-127">Solución de problemas de Spark</span><span class="sxs-lookup"><span data-stu-id="2b241-127">Troubleshoot Spark</span></span>](hdinsight-troubleshoot-SPARK.md)|<br>[<span data-ttu-id="2b241-128">Cómo se configura una aplicación de Spark a través de Ambari en clústeres</span><span class="sxs-lookup"><span data-stu-id="2b241-128">How do I configure a Spark application by using Ambari on clusters</span></span>](hdinsight-troubleshoot-spark.md#how-do-i-configure-a-spark-application-by-using-ambari-on-clusters)<br><br>[<span data-ttu-id="2b241-129">Cómo se configura una aplicación de Spark a través de un cuaderno de Jupyter Notebook en clústeres</span><span class="sxs-lookup"><span data-stu-id="2b241-129">How do I configure a Spark application by using a Jupyter notebook on clusters</span></span>](hdinsight-troubleshoot-spark.md#how-do-i-configure-a-spark-application-by-using-a-jupyter-notebook-on-clusters)<br><br>[<span data-ttu-id="2b241-130">Cómo se configura una aplicación de Spark a través de LIVY en clústeres</span><span class="sxs-lookup"><span data-stu-id="2b241-130">How do I configure a Spark application by using Livy on clusters</span></span>](hdinsight-troubleshoot-spark.md#how-do-i-configure-a-spark-application-by-using-livy-on-clusters)<br><br>[<span data-ttu-id="2b241-131">Cómo se configura una aplicación de Spark a través de spark-submit en clústeres</span><span class="sxs-lookup"><span data-stu-id="2b241-131">How do I configure a Spark application by using spark-submit on clusters</span></span>](hdinsight-troubleshoot-spark.md#how-do-i-configure-a-spark-application-by-using-spark-submit-on-clusters)<br><br>[<span data-ttu-id="2b241-132">Qué produce una excepción OutOfMemoryError en una aplicación Spark</span><span class="sxs-lookup"><span data-stu-id="2b241-132">What causes a Spark application OutOfMemoryError exception</span></span>](hdinsight-troubleshoot-spark.md#what-causes-a-spark-application-outofmemoryerror-exception)|
|<span data-ttu-id="2b241-133">![Storm](./media/hdinsight-troubleshoot-guide/STORM.png)</span><span class="sxs-lookup"><span data-stu-id="2b241-133">![Storm](./media/hdinsight-troubleshoot-guide/STORM.png)</span></span><br>[<span data-ttu-id="2b241-134">Solución de problemas de Storm</span><span class="sxs-lookup"><span data-stu-id="2b241-134">Troubleshoot Storm</span></span>](hdinsight-troubleshoot-STORM.md)|<br>[<span data-ttu-id="2b241-135">¿Cómo obtengo acceso Hola aluvión de interfaz de usuario en un clúster</span><span class="sxs-lookup"><span data-stu-id="2b241-135">How do I access hello Storm UI on a cluster</span></span>](hdinsight-troubleshoot-storm.md#how-do-i-access-the-storm-ui-on-a-cluster)<br><br>[<span data-ttu-id="2b241-136">Cómo transferir información de punto de comprobación de Storm eventos concentrador pitorro de una topología tooanother</span><span class="sxs-lookup"><span data-stu-id="2b241-136">How do I transfer Storm event hub spout checkpoint information from one topology tooanother</span></span>](hdinsight-troubleshoot-storm.md#how-do-i-transfer-storm-event-hub-spout-checkpoint-information-from-one-topology-to-another)<br><br>[<span data-ttu-id="2b241-137">Cómo se buscan los archivos binarios de Storm en un clúster</span><span class="sxs-lookup"><span data-stu-id="2b241-137">How do I locate Storm binaries on a cluster</span></span>](hdinsight-troubleshoot-storm.md#how-do-i-locate-storm-binaries-on-a-cluster)<br><br>[<span data-ttu-id="2b241-138">¿Cómo se puede determinar la topología de implementación de Hola de un clúster de Storm</span><span class="sxs-lookup"><span data-stu-id="2b241-138">How do I determine hello deployment topology of a Storm cluster</span></span>](hdinsight-troubleshoot-storm.md#how-do-i-determine-the-deployment-topology-of-a-storm-cluster)<br><br>[<span data-ttu-id="2b241-139">Localización de los archivos binarios del spout del centro de eventos de Storm para el desarrollo</span><span class="sxs-lookup"><span data-stu-id="2b241-139">How do I locate Storm event hub spout binaries for development</span></span>](hdinsight-troubleshoot-storm.md#how-do-i-locate-storm-event-hub-spout-binaries-for-development)<br><br>[<span data-ttu-id="2b241-140">Cómo se encuentran los archivos de configuración Log4J de Storm en clústeres</span><span class="sxs-lookup"><span data-stu-id="2b241-140">How do I locate Storm Log4J configuration files on clusters</span></span>](hdinsight-troubleshoot-storm.md#how-do-i-locate-storm-log4j-configuration-files-on-clusters)|
|<span data-ttu-id="2b241-141">![YARN](./media/hdinsight-troubleshoot-guide/YARN.png)</span><span class="sxs-lookup"><span data-stu-id="2b241-141">![YARN](./media/hdinsight-troubleshoot-guide/YARN.png)</span></span><br>[<span data-ttu-id="2b241-142">Solución de problemas de YARN</span><span class="sxs-lookup"><span data-stu-id="2b241-142">Troubleshoot YARN</span></span>](hdinsight-troubleshoot-YARN.md)|<br>[<span data-ttu-id="2b241-143">Creación de una nueva cola Yarn en un clúster</span><span class="sxs-lookup"><span data-stu-id="2b241-143">How do I create a new YARN queue on a cluster</span></span>](hdinsight-troubleshoot-yarn.md#how-do-i-create-a-new-yarn-queue-on-a-cluster)<br><br>[<span data-ttu-id="2b241-144">Descarga de los registros de Yarn desde un clúster</span><span class="sxs-lookup"><span data-stu-id="2b241-144">How do I download YARN logs from a cluster</span></span>](hdinsight-troubleshoot-yarn.md#how-do-i-download-yarn-logs-from-a-cluster)|

## <a name="hdinsight-troubleshooting-resources"></a><span data-ttu-id="2b241-145">Recursos de solución de problemas de HDInsight</span><span class="sxs-lookup"><span data-stu-id="2b241-145">HDInsight troubleshooting resources</span></span>

| <span data-ttu-id="2b241-146">Para información acerca de</span><span class="sxs-lookup"><span data-stu-id="2b241-146">For information about</span></span> | <span data-ttu-id="2b241-147">Consulte estos artículos</span><span class="sxs-lookup"><span data-stu-id="2b241-147">See these articles</span></span> |
| --- | --- |
| <span data-ttu-id="2b241-148">HDInsight en Linux y optimización</span><span class="sxs-lookup"><span data-stu-id="2b241-148">HDInsight on Linux and optimization</span></span> | <span data-ttu-id="2b241-149">- [Información sobre el uso de HDInsight en Linux](hdinsight-hadoop-linux-information.md)</span><span class="sxs-lookup"><span data-stu-id="2b241-149">- [Information about using HDInsight on Linux](hdinsight-hadoop-linux-information.md)</span></span><br><span data-ttu-id="2b241-150">- [Solución de problemas de memoria y rendimiento de Hadoop](hdinsight-hadoop-stack-trace-error-messages.md)</span><span class="sxs-lookup"><span data-stu-id="2b241-150">- [Hadoop memory and performance troubleshooting](hdinsight-hadoop-stack-trace-error-messages.md)</span></span><br><span data-ttu-id="2b241-151">- [Rendimiento de consultas de Hive](https://blogs.msdn.microsoft.com/bigdatasupport/2015/08/13/troubleshooting-hive-query-performance-in-hdinsight-hadoop-cluster/)</span><span class="sxs-lookup"><span data-stu-id="2b241-151">- [Hive query performance](https://blogs.msdn.microsoft.com/bigdatasupport/2015/08/13/troubleshooting-hive-query-performance-in-hdinsight-hadoop-cluster/)</span></span> |
| <span data-ttu-id="2b241-152">Registros y volcados de memoria</span><span class="sxs-lookup"><span data-stu-id="2b241-152">Logs and dumps</span></span> | <span data-ttu-id="2b241-153">- [Acceso a registros de aplicación de YARN en HDInsight basado en Linux](hdinsight-hadoop-access-yarn-app-logs-linux.md)</span><span class="sxs-lookup"><span data-stu-id="2b241-153">- [Access Hadoop YARN application logs on Linux](hdinsight-hadoop-access-yarn-app-logs-linux.md)</span></span><br><span data-ttu-id="2b241-154">- [Habilitación de los volcados de montón de los servicios de Hadoop en HDInsight basado en Linux](hdinsight-hadoop-collect-debug-heap-dump-linux.md)</span><span class="sxs-lookup"><span data-stu-id="2b241-154">- [Enable heap dumps for Hadoop services on Linux](hdinsight-hadoop-collect-debug-heap-dump-linux.md)</span></span><br><span data-ttu-id="2b241-155">- [Análisis de registros de HDInsight](hdinsight-debug-jobs.md)</span><span class="sxs-lookup"><span data-stu-id="2b241-155">- [Analyze HDInsight logs](hdinsight-debug-jobs.md)</span></span>|
| <span data-ttu-id="2b241-156">Errors</span><span class="sxs-lookup"><span data-stu-id="2b241-156">Errors</span></span> | <span data-ttu-id="2b241-157">- [Entender y resolver errores recibidos de WebHCat en HDInsight](hdinsight-hadoop-templeton-webhcat-debug-errors.md)</span><span class="sxs-lookup"><span data-stu-id="2b241-157">- [Understand and resolve WebHCat errors](hdinsight-hadoop-templeton-webhcat-debug-errors.md)</span></span><br><span data-ttu-id="2b241-158">- [Hive toofix OutofMemory error de configuración](hdinsight-hadoop-hive-out-of-memory-error-oom.md)</span><span class="sxs-lookup"><span data-stu-id="2b241-158">- [Hive settings toofix OutofMemory error](hdinsight-hadoop-hive-out-of-memory-error-oom.md)</span></span> |
| <span data-ttu-id="2b241-159">Herramientas</span><span class="sxs-lookup"><span data-stu-id="2b241-159">Tools</span></span> | <span data-ttu-id="2b241-160">- [Utilice las vistas de Ambari toodebug Tez trabajos](hdinsight-debug-ambari-tez-view.md)</span><span class="sxs-lookup"><span data-stu-id="2b241-160">- [Use Ambari Views toodebug Tez jobs](hdinsight-debug-ambari-tez-view.md)</span></span><br><span data-ttu-id="2b241-161">- [Optimización de consultas de Hive](hdinsight-hadoop-optimize-hive-query.md)</span><span class="sxs-lookup"><span data-stu-id="2b241-161">- [Optimize Hive queries](hdinsight-hadoop-optimize-hive-query.md)</span></span> |