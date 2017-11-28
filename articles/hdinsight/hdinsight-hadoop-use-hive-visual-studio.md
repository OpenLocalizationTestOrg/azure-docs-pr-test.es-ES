---
title: 'aaaHive con herramientas de Data Lake (Hadoop) para Visual Studio: HDInsight de Azure | Documentos de Microsoft'
description: "Obtenga información acerca de cómo toouse Hola Data Lake tools para toorun de Visual Studio Apache Hive consultas con Apache Hadoop en HDInsight de Azure."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 2b3e672a-1195-4fa5-afb7-b7b73937bfbe
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/07/2017
ms.author: larryfr
ms.openlocfilehash: dc76974c02cf68bcf701b2b155842c9e9c5cb988
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="run-hive-queries-using-hello-data-lake-tools-for-visual-studio"></a><span data-ttu-id="5a431-103">Ejecutar consultas de Hive con herramientas de Data Lake Hola para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5a431-103">Run Hive queries using hello Data Lake tools for Visual Studio</span></span>

<span data-ttu-id="5a431-104">Obtenga información acerca de cómo toouse Hola Data Lake tools para Apache Hive de tooquery de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5a431-104">Learn how toouse hello Data Lake tools for Visual Studio tooquery Apache Hive.</span></span> <span data-ttu-id="5a431-105">herramientas de Data Lake Hello tooeasily podrá crear, enviar y supervisar tooHadoop de las consultas de Hive en HDInsight de Azure.</span><span class="sxs-lookup"><span data-stu-id="5a431-105">hello Data Lake tools allow you tooeasily create, submit, and monitor Hive queries tooHadoop on Azure HDInsight.</span></span>

## <span data-ttu-id="5a431-106"><a id="prereq"></a>Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="5a431-106"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="5a431-107">Un clúster de Azure HDInsight (Hadoop en HDInsight).</span><span class="sxs-lookup"><span data-stu-id="5a431-107">An Azure HDInsight (Hadoop on HDInsight) cluster</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="5a431-108">Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior.</span><span class="sxs-lookup"><span data-stu-id="5a431-108">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="5a431-109">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="5a431-109">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="5a431-110">Visual Studio (uno de hello siguiendo las versiones):</span><span class="sxs-lookup"><span data-stu-id="5a431-110">Visual Studio (one of hello following versions):</span></span>

    * <span data-ttu-id="5a431-111">Visual Studio 2013 Community/Professional/Premium/Ultimate con la actualización 4</span><span class="sxs-lookup"><span data-stu-id="5a431-111">Visual Studio 2013 Community/Professional/Premium/Ultimate with Update 4</span></span>

    * <span data-ttu-id="5a431-112">Visual Studio 2015 (cualquier edición)</span><span class="sxs-lookup"><span data-stu-id="5a431-112">Visual Studio 2015 (any edition)</span></span>

    * <span data-ttu-id="5a431-113">Visual Studio 2017 (cualquier edición)</span><span class="sxs-lookup"><span data-stu-id="5a431-113">Visual Studio 2017 (any edition)</span></span>

* <span data-ttu-id="5a431-114">Herramientas de HDInsight para Visual Studio o Azure Data Lake Tools for Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5a431-114">HDInsight tools for Visual Studio or Azure Data Lake tools for Visual Studio.</span></span> <span data-ttu-id="5a431-115">Vea [Introducción al uso de Hadoop de Visual Studio tools para HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md) para obtener información sobre cómo instalar y configurar las herramientas de Hola.</span><span class="sxs-lookup"><span data-stu-id="5a431-115">See [Get started using Visual Studio Hadoop tools for HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md) for information on installing and configuring hello tools.</span></span>

## <span data-ttu-id="5a431-116"><a id="run"></a>Ejecutar consultas de Hive con hello Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5a431-116"><a id="run"></a> Run Hive queries using hello Visual Studio</span></span>

1. <span data-ttu-id="5a431-117">Abra **Visual Studio** y seleccione **Nuevo** > **Proyecto** > **Azure Data Lake** > **HIVE** > **Hive Application** (Aplicación de Hive).</span><span class="sxs-lookup"><span data-stu-id="5a431-117">Open **Visual Studio** and select **New** > **Project** > **Azure Data Lake** > **HIVE** > **Hive Application**.</span></span> <span data-ttu-id="5a431-118">Indique un nombre para este proyecto.</span><span class="sxs-lookup"><span data-stu-id="5a431-118">Provide a name for this project.</span></span>

2. <span data-ttu-id="5a431-119">Abra hello **Script.hql** archivo que se crea con este proyecto y pegar en hello siguiendo las instrucciones de HiveQL:</span><span class="sxs-lookup"><span data-stu-id="5a431-119">Open hello **Script.hql** file that is created with this project, and paste in hello following HiveQL statements:</span></span>

   ```hiveql
   set hive.execution.engine=tez;
   DROP TABLE log4jLogs;
   CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
   ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
   STORED AS TEXTFILE LOCATION '/example/data/';
   SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND  INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;
   ```

    <span data-ttu-id="5a431-120">Estas instrucciones realizan Hola siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="5a431-120">These statements perform hello following actions:</span></span>

   * <span data-ttu-id="5a431-121">`DROP TABLE`: Si existe en la tabla de hello, esta instrucción elimina.</span><span class="sxs-lookup"><span data-stu-id="5a431-121">`DROP TABLE`: If hello table exists, this statement deletes it.</span></span>

   * <span data-ttu-id="5a431-122">`CREATE EXTERNAL TABLE`: Crea una tabla 'externa' en Hive.</span><span class="sxs-lookup"><span data-stu-id="5a431-122">`CREATE EXTERNAL TABLE`: Creates a new 'external' table in Hive.</span></span> <span data-ttu-id="5a431-123">Tablas externas solo almacenan definición de la tabla de hello en el subárbol (Hola datos permanecen en la ubicación original de hello).</span><span class="sxs-lookup"><span data-stu-id="5a431-123">External tables only store hello table definition in Hive (hello data is left in hello original location).</span></span>

     > [!NOTE]
     > <span data-ttu-id="5a431-124">Tablas externas deben utilizarse cuando se espera Hola subyacente datos toobe actualizado a través de un origen externo.</span><span class="sxs-lookup"><span data-stu-id="5a431-124">External tables should be used when you expect hello underlying data toobe updated by an external source.</span></span> <span data-ttu-id="5a431-125">Por ejemplo, un trabajo de MapReduce o un servicio de Azure.</span><span class="sxs-lookup"><span data-stu-id="5a431-125">For example, a MapReduce job or Azure service.</span></span>
     >
     > <span data-ttu-id="5a431-126">Quitar una tabla externa **no** eliminar datos de hello, solo la definición de tabla Hola.</span><span class="sxs-lookup"><span data-stu-id="5a431-126">Dropping an external table does **not** delete hello data, only hello table definition.</span></span>

   * <span data-ttu-id="5a431-127">`ROW FORMAT`: Indica cómo se da formato a los datos de Hola de Hive.</span><span class="sxs-lookup"><span data-stu-id="5a431-127">`ROW FORMAT`: Tells Hive how hello data is formatted.</span></span> <span data-ttu-id="5a431-128">En este caso, los campos de hello en cada registro están separados por un espacio.</span><span class="sxs-lookup"><span data-stu-id="5a431-128">In this case, hello fields in each log are separated by a space.</span></span>

   * <span data-ttu-id="5a431-129">`STORED AS TEXTFILE LOCATION`: Indica Hive donde hello se almacenan los datos (directorio de datos del ejemplo de Hola) y que se almacena como texto.</span><span class="sxs-lookup"><span data-stu-id="5a431-129">`STORED AS TEXTFILE LOCATION`: Tells Hive where hello data is stored (hello example/data directory) and that it is stored as text.</span></span>

   * <span data-ttu-id="5a431-130">`SELECT`: Seleccionar un recuento de todas las filas donde columna `t4` contiene el valor de hello `[ERROR]`.</span><span class="sxs-lookup"><span data-stu-id="5a431-130">`SELECT`: Select a count of all rows where column `t4` contains hello value `[ERROR]`.</span></span> <span data-ttu-id="5a431-131">Esta instrucción devuelve un valor de `3` porque hay tres filas que contienen este valor.</span><span class="sxs-lookup"><span data-stu-id="5a431-131">This statement returns a value of `3` because there are three rows that contain this value.</span></span>

   * <span data-ttu-id="5a431-132">`INPUT__FILE__NAME LIKE '%.log'`: Indica a Hive que solo deberíamos devolver datos de archivos que terminan en .log.</span><span class="sxs-lookup"><span data-stu-id="5a431-132">`INPUT__FILE__NAME LIKE '%.log'` - Tells Hive that we should only return data from files ending in .log.</span></span> <span data-ttu-id="5a431-133">Esta cláusula restringe hello toohello sample.log archivo de búsqueda contiene datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="5a431-133">This clause restricts hello search toohello sample.log file that contains hello data.</span></span>

3. <span data-ttu-id="5a431-134">En la barra de herramientas de hello, seleccione hello **clúster de HDInsight** que desea toouse para esta consulta.</span><span class="sxs-lookup"><span data-stu-id="5a431-134">From hello toolbar, select hello **HDInsight Cluster** that you want toouse for this query.</span></span> <span data-ttu-id="5a431-135">Seleccione **enviar** instrucciones de hello toorun como un trabajo de Hive.</span><span class="sxs-lookup"><span data-stu-id="5a431-135">Select **Submit** toorun hello statements as a Hive job.</span></span>

   ![Barra Enviar](./media/hdinsight-hadoop-use-hive-visual-studio/toolbar.png)

4. <span data-ttu-id="5a431-137">Hola **resumen del trabajo de Hive** aparece y muestra información acerca de hello ejecutar trabajo.</span><span class="sxs-lookup"><span data-stu-id="5a431-137">hello **Hive Job Summary** appears and displays information about hello running job.</span></span> <span data-ttu-id="5a431-138">Hola de uso **actualizar** vincular toorefresh Hola información sobre el trabajo, hasta hello **estado del trabajo** cambia demasiado**completado**.</span><span class="sxs-lookup"><span data-stu-id="5a431-138">Use hello **Refresh** link toorefresh hello job information, until hello **Job Status** changes too**Completed**.</span></span>

   ![resumen de trabajos que muestra un trabajo completado](./media/hdinsight-hadoop-use-hive-visual-studio/jobsummary.png)

5. <span data-ttu-id="5a431-140">Hola de uso **salida del trabajo** vincular la salida de hello tooview de este trabajo.</span><span class="sxs-lookup"><span data-stu-id="5a431-140">Use hello **Job Output** link tooview hello output of this job.</span></span> <span data-ttu-id="5a431-141">Muestra `[ERROR] 3`, que es el valor de hello devuelto por esta consulta.</span><span class="sxs-lookup"><span data-stu-id="5a431-141">It displays `[ERROR] 3`, which is hello value returned by this query.</span></span>

6. <span data-ttu-id="5a431-142">También puede ejecutar consultas de Hive sin crear un proyecto.</span><span class="sxs-lookup"><span data-stu-id="5a431-142">You can also run Hive queries without creating a project.</span></span> <span data-ttu-id="5a431-143">Con el **Explorador de servidores**, expanda **Azure** > **HDInsight**, haga clic con el botón derecho en el servidor de HDInsight y luego seleccione **Escribir una consulta de Hive**.</span><span class="sxs-lookup"><span data-stu-id="5a431-143">Using **Server Explorer**, expand **Azure** > **HDInsight**, right-click your HDInsight server, and then select **Write a Hive Query**.</span></span>

7. <span data-ttu-id="5a431-144">Hola **temp.hql** documento que aparece, agregue Hola siguiendo las instrucciones de HiveQL:</span><span class="sxs-lookup"><span data-stu-id="5a431-144">In hello **temp.hql** document that appears, add hello following HiveQL statements:</span></span>

   ```hiveql
   set hive.execution.engine=tez;
   CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
   INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log';
   ```

    <span data-ttu-id="5a431-145">Estas instrucciones realizan Hola siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="5a431-145">These statements perform hello following actions:</span></span>

   * <span data-ttu-id="5a431-146">`CREATE TABLE IF NOT EXISTS`: Crea una tabla, si todavía no existe.</span><span class="sxs-lookup"><span data-stu-id="5a431-146">`CREATE TABLE IF NOT EXISTS`: Creates a table if it does not already exist.</span></span> <span data-ttu-id="5a431-147">Dado que hello `EXTERNAL` no se utiliza la palabra clave, esta instrucción crea una tabla interna.</span><span class="sxs-lookup"><span data-stu-id="5a431-147">Because hello `EXTERNAL` keyword is not used, this statement creates an internal table.</span></span> <span data-ttu-id="5a431-148">Las tablas internas se almacenan en el almacén de datos de Hive de Hola y administradas por el subárbol.</span><span class="sxs-lookup"><span data-stu-id="5a431-148">Internal tables are stored in hello Hive data warehouse and are managed by Hive.</span></span>

     > [!NOTE]
     > <span data-ttu-id="5a431-149">A diferencia de `EXTERNAL` tablas, quitar una tabla interna también elimina Hola datos subyacentes.</span><span class="sxs-lookup"><span data-stu-id="5a431-149">Unlike `EXTERNAL` tables, dropping an internal table also deletes hello underlying data.</span></span>

   * <span data-ttu-id="5a431-150">`STORED AS ORC`: Almacena Hola datos en formato de fila optimizado columnas (ORC).</span><span class="sxs-lookup"><span data-stu-id="5a431-150">`STORED AS ORC`: Stores hello data in optimized row columnar (ORC) format.</span></span> <span data-ttu-id="5a431-151">ORC es un formato altamente optimizado y eficiente para almacenar datos de Hive.</span><span class="sxs-lookup"><span data-stu-id="5a431-151">ORC is a highly optimized and efficient format for storing Hive data.</span></span>

   * <span data-ttu-id="5a431-152">`INSERT OVERWRITE ... SELECT`: Selecciona las filas de hello `log4jLogs` tabla que contenga `[ERROR]`, a continuación, inserta Hola datos en hello `errorLogs` tabla.</span><span class="sxs-lookup"><span data-stu-id="5a431-152">`INSERT OVERWRITE ... SELECT`: Selects rows from hello `log4jLogs` table that contain `[ERROR]`, then inserts hello data into hello `errorLogs` table.</span></span>

8. <span data-ttu-id="5a431-153">En la barra de herramientas de hello, seleccione **enviar** trabajo de hello toorun.</span><span class="sxs-lookup"><span data-stu-id="5a431-153">From hello toolbar, select **Submit** toorun hello job.</span></span> <span data-ttu-id="5a431-154">Hola de uso **estado del trabajo** toodetermine ese trabajo Hola se completó correctamente.</span><span class="sxs-lookup"><span data-stu-id="5a431-154">Use hello **Job Status** toodetermine that hello job has completed successfully.</span></span>

9. <span data-ttu-id="5a431-155">tooverify que Hola trabajo creado tabla hello, utilice **Explorador de servidores** y expanda **Azure** > **HDInsight** > su clúster de HDInsight > **Bases de datos de hive** > **predeterminado**.</span><span class="sxs-lookup"><span data-stu-id="5a431-155">tooverify that hello job created hello table, use **Server Explorer** and expand **Azure** > **HDInsight** > your HDInsight cluster > **Hive Databases** > **default**.</span></span> <span data-ttu-id="5a431-156">Hola **registros de errores de** hello y tabla **log4jLogs** tabla se enumeran.</span><span class="sxs-lookup"><span data-stu-id="5a431-156">hello **errorLogs** table and hello **log4jLogs** table are listed.</span></span>

## <span data-ttu-id="5a431-157"><a id="nextsteps"></a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5a431-157"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="5a431-158">Como puede ver, las herramientas de HDInsight de Hola para Visual Studio proporcionan una toowork fácilmente con consultas de Hive en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5a431-158">As you can see, hello HDInsight tools for Visual Studio provide an easy way toowork with Hive queries on HDInsight.</span></span>

<span data-ttu-id="5a431-159">Para obtener información general acerca de Hive en HDInsight:</span><span class="sxs-lookup"><span data-stu-id="5a431-159">For general information about Hive in HDInsight:</span></span>

* [<span data-ttu-id="5a431-160">Uso de Hive con Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="5a431-160">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="5a431-161">Para obtener información sobre otras maneras en que puede trabajar con Hadoop en HDInsight:</span><span class="sxs-lookup"><span data-stu-id="5a431-161">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="5a431-162">Uso de Pig con Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="5a431-162">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

* [<span data-ttu-id="5a431-163">Uso de MapReduce con Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="5a431-163">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="5a431-164">Para obtener más información acerca de hello HDInsight tools para Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="5a431-164">For more information about hello HDInsight tools for Visual Studio:</span></span>

* [<span data-ttu-id="5a431-165">Introducción a las herramientas de HDInsight para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5a431-165">Getting started with HDInsight tools for Visual Studio</span></span>](hdinsight-hadoop-visual-studio-tools-get-started.md)

[hdinsight-sdk-documentation]: http://msdnstage.redmond.corp.microsoft.com/library/dn479185.aspx

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[apache-tez]: http://tez.apache.org
[apache-hive]: http://hive.apache.org/
[apache-log4j]: http://en.wikipedia.org/wiki/Log4j
[hive-on-tez-wiki]: https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez
[import-to-excel]: http://azure.microsoft.com/documentation/articles/hdinsight-connect-excel-power-query/


[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md



[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md

[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx

[image-hdi-hive-powershell]: ./media/hdinsight-use-hive/HDI.HIVE.PowerShell.png
[img-hdi-hive-powershell-output]: ./media/hdinsight-use-hive/HDI.Hive.PowerShell.Output.png
[image-hdi-hive-architecture]: ./media/hdinsight-use-hive/HDI.Hive.Architecture.png
