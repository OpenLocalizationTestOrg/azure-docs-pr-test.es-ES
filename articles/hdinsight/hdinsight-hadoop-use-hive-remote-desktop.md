---
title: aaaUse Hive de Hadoop y el escritorio remoto en HDInsight - Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooconnect tooHadoop de clúster de HDInsight mediante Escritorio remoto y, a continuación, ejecutar consultas de Hive mediante Hola Hive interfaz de línea de comandos."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 8c228e35-d58a-4f22-917a-1d20c9da89b4
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/12/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: f86ffc1be33a8b0b2346d1a1388e5dfa6d0f8777
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-hive-with-hadoop-on-hdinsight-with-remote-desktop"></a><span data-ttu-id="80006-103">Uso de Hive con Hadoop en HDInsight con el escritorio remoto</span><span class="sxs-lookup"><span data-stu-id="80006-103">Use Hive with Hadoop on HDInsight with Remote Desktop</span></span>
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="80006-104">En este artículo, aprenderá cómo las consultas tooconnect tooan HDInsight clúster mediante Escritorio remoto y, a continuación, ejecute subárbol mediante el uso de hello Hive interfaz de línea de comandos (CLI).</span><span class="sxs-lookup"><span data-stu-id="80006-104">In this article, you will learn how tooconnect tooan HDInsight cluster by using Remote Desktop, and then run Hive queries by using hello Hive Command-Line Interface (CLI).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="80006-105">Escritorio remoto sólo está disponible en los clústeres de HDInsight que usa Windows como sistema operativo de Hola.</span><span class="sxs-lookup"><span data-stu-id="80006-105">Remote Desktop is only available on HDInsight clusters that use Windows as hello operating system.</span></span> <span data-ttu-id="80006-106">Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior.</span><span class="sxs-lookup"><span data-stu-id="80006-106">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="80006-107">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="80006-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="80006-108">Para HDInsight 3.4 o superior, consulte [uso de Hive con HDInsight y Beeline](hdinsight-hadoop-use-hive-beeline.md) para obtener información acerca de cómo ejecutar consultas de Hive directamente en el clúster de Hola desde una línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="80006-108">For HDInsight 3.4 or greater, see [Use Hive with HDInsight and Beeline](hdinsight-hadoop-use-hive-beeline.md) for information on running Hive queries directly on hello cluster from a command-line.</span></span>

## <span data-ttu-id="80006-109"><a id="prereq"></a>Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="80006-109"><a id="prereq"></a>Prerequisites</span></span>
<span data-ttu-id="80006-110">pasos de hello toocomplete en este artículo, se necesita Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="80006-110">toocomplete hello steps in this article, you will need hello following:</span></span>

* <span data-ttu-id="80006-111">Un clúster de HDInsight basado en Windows (Hadoop en HDInsight)</span><span class="sxs-lookup"><span data-stu-id="80006-111">A Windows-based HDInsight (Hadoop on HDInsight) cluster</span></span>
* <span data-ttu-id="80006-112">Un equipo cliente con Windows 10, Window 8 o Windows 7</span><span class="sxs-lookup"><span data-stu-id="80006-112">A client computer running Windows 10, Window 8, or Windows 7</span></span>

## <span data-ttu-id="80006-113"><a id="connect"></a>Conexión con el Escritorio remoto</span><span class="sxs-lookup"><span data-stu-id="80006-113"><a id="connect"></a>Connect with Remote Desktop</span></span>
<span data-ttu-id="80006-114">Habilitar Escritorio remoto para el clúster de HDInsight de Hola y conéctela tooit siguiendo las instrucciones de hello en [conectarse mediante RDP de clústeres de tooHDInsight](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span><span class="sxs-lookup"><span data-stu-id="80006-114">Enable Remote Desktop for hello HDInsight cluster, then connect tooit by following hello instructions at [Connect tooHDInsight clusters using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>

## <span data-ttu-id="80006-115"><a id="hive"></a>Usar comandos de Hive Hola</span><span class="sxs-lookup"><span data-stu-id="80006-115"><a id="hive"></a>Use hello Hive command</span></span>
<span data-ttu-id="80006-116">Cuando se ha conectado el escritorio de toohello para el clúster de HDInsight de hello, utilice Hola siguiendo los pasos toowork con Hive:</span><span class="sxs-lookup"><span data-stu-id="80006-116">When you have connected toohello desktop for hello HDInsight cluster, use hello following steps toowork with Hive:</span></span>

1. <span data-ttu-id="80006-117">Desde el escritorio de HDInsight de hello, inicie hello **línea de comandos de Hadoop**.</span><span class="sxs-lookup"><span data-stu-id="80006-117">From hello HDInsight desktop, start hello **Hadoop Command Line**.</span></span>
2. <span data-ttu-id="80006-118">Escriba Hola después comando toostart hello Hive CLI:</span><span class="sxs-lookup"><span data-stu-id="80006-118">Enter hello following command toostart hello Hive CLI:</span></span>

        %hive_home%\bin\hive

    <span data-ttu-id="80006-119">Cuando se ha iniciado Hola CLI, verá el símbolo del sistema de hello Hive CLI: `hive>`.</span><span class="sxs-lookup"><span data-stu-id="80006-119">When hello CLI has started, you will see hello Hive CLI prompt: `hive>`.</span></span>
3. <span data-ttu-id="80006-120">Hola CLI, escriba Hola siguiendo las instrucciones toocreate una nueva tabla denominada **log4jLogs** con datos de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="80006-120">Using hello CLI, enter hello following statements toocreate a new table named **log4jLogs** using sample data:</span></span>

        set hive.execution.engine=tez;
        DROP TABLE log4jLogs;
        CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
        STORED AS TEXTFILE LOCATION 'wasb:///example/data/';
        SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

    <span data-ttu-id="80006-121">Estas instrucciones realizan Hola siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="80006-121">These statements perform hello following actions:</span></span>

   * <span data-ttu-id="80006-122">**DROP TABLE**: elimina la tabla de Hola y archivo de datos de hello si Hola tabla ya existe.</span><span class="sxs-lookup"><span data-stu-id="80006-122">**DROP TABLE**: Deletes hello table and hello data file if hello table already exists.</span></span>
   * <span data-ttu-id="80006-123">**CREATE EXTERNAL TABLE**: crea una tabla "externa" nueva en Hive.</span><span class="sxs-lookup"><span data-stu-id="80006-123">**CREATE EXTERNAL TABLE**: Creates a new 'external' table in Hive.</span></span> <span data-ttu-id="80006-124">Tablas externas almacenan definición única de la tabla de hello en el subárbol (Hola datos permanecen en la ubicación original de hello).</span><span class="sxs-lookup"><span data-stu-id="80006-124">External tables store only hello table definition in Hive (hello data is left in hello original location).</span></span>

     > [!NOTE]
     > <span data-ttu-id="80006-125">Tablas externas deben utilizarse cuando creas Hola subyacente toobe datos actualizado por un origen externo (por ejemplo, un proceso de carga de datos automatizado) o por otra operación de MapReduce, pero desea siempre que datos más recientes de toouse Hola de consulta de Hive.</span><span class="sxs-lookup"><span data-stu-id="80006-125">External tables should be used when you expect hello underlying data toobe updated by an external source (such as an automated data upload process) or by another MapReduce operation, but you always want Hive queries toouse hello latest data.</span></span>
     >
     > <span data-ttu-id="80006-126">Quitar una tabla externa **no** eliminar datos de hello, solo la definición de tabla Hola.</span><span class="sxs-lookup"><span data-stu-id="80006-126">Dropping an external table does **not** delete hello data, only hello table definition.</span></span>
     >
     >
   * <span data-ttu-id="80006-127">**FORMATO de fila**: indica cómo se da formato a los datos de Hola de Hive.</span><span class="sxs-lookup"><span data-stu-id="80006-127">**ROW FORMAT**: Tells Hive how hello data is formatted.</span></span> <span data-ttu-id="80006-128">En este caso, los campos de hello en cada registro están separados por un espacio.</span><span class="sxs-lookup"><span data-stu-id="80006-128">In this case, hello fields in each log are separated by a space.</span></span>
   * <span data-ttu-id="80006-129">**UBICACIÓN de archivo de texto de AS almacenados**: indica Hive donde están Hola datos almacenados (directorio de datos del ejemplo de Hola) y que se almacena como texto.</span><span class="sxs-lookup"><span data-stu-id="80006-129">**STORED AS TEXTFILE LOCATION**: Tells Hive where hello data is stored (hello example/data directory) and that it is stored as text.</span></span>
   * <span data-ttu-id="80006-130">**Seleccione**: selecciona un recuento de todas las filas donde columna **t4** contiene el valor de hello **[ERROR]**.</span><span class="sxs-lookup"><span data-stu-id="80006-130">**SELECT**: Selects a count of all rows where column **t4** contains hello value **[ERROR]**.</span></span> <span data-ttu-id="80006-131">Esto debe devolver un valor de **3** porque hay tres filas que contienen este valor.</span><span class="sxs-lookup"><span data-stu-id="80006-131">This should return a value of **3** because there are three rows that contain this value.</span></span>
   * <span data-ttu-id="80006-132">**INPUT__FILE__NAME LIKE '%.log'**: indica a Hive que solo deberíamos devolver datos de archivos que terminan en .log.</span><span class="sxs-lookup"><span data-stu-id="80006-132">**INPUT__FILE__NAME LIKE '%.log'** - Tells Hive that we should only return data from files ending in .log.</span></span> <span data-ttu-id="80006-133">Así restringe hello toohello sample.log archivo de búsqueda contiene datos de Hola y mantiene devuelvan datos del ejemplo de otro archivos de datos que no coinciden con el esquema de Hola que se define.</span><span class="sxs-lookup"><span data-stu-id="80006-133">This restricts hello search toohello sample.log file that contains hello data, and keeps it from returning data from other example data files that do not match hello schema we defined.</span></span>
4. <span data-ttu-id="80006-134">Hola uso siguiendo las instrucciones toocreate una nueva tabla 'interna' denominada **registros de errores de**:</span><span class="sxs-lookup"><span data-stu-id="80006-134">Use hello following statements toocreate a new 'internal' table named **errorLogs**:</span></span>

        CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
        INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log';

    <span data-ttu-id="80006-135">Estas instrucciones realizan Hola siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="80006-135">These statements perform hello following actions:</span></span>

   * <span data-ttu-id="80006-136">**CREATE TABLE IF NOT EXISTS**: crea una tabla, si todavía no existe.</span><span class="sxs-lookup"><span data-stu-id="80006-136">**CREATE TABLE IF NOT EXISTS**: Creates a table if it does not already exist.</span></span> <span data-ttu-id="80006-137">Dado que hello **externo** no se utiliza la palabra clave, se trata de una tabla interna, que se almacena en el almacén de datos de Hive de Hola y Hive administra completamente.</span><span class="sxs-lookup"><span data-stu-id="80006-137">Because hello **EXTERNAL** keyword is not used, this is an internal table, which is stored in hello Hive data warehouse and is managed completely by Hive.</span></span>

     > [!NOTE]
     > <span data-ttu-id="80006-138">A diferencia de **externo** tablas, quitar una tabla interna también elimina Hola datos subyacentes.</span><span class="sxs-lookup"><span data-stu-id="80006-138">Unlike **EXTERNAL** tables, dropping an internal table also deletes hello underlying data.</span></span>
     >
     >
   * <span data-ttu-id="80006-139">**ALMACENA AS ORC**: almacena los datos de hello en formato de fila optimizado columnas (ORC).</span><span class="sxs-lookup"><span data-stu-id="80006-139">**STORED AS ORC**: Stores hello data in optimized row columnar (ORC) format.</span></span> <span data-ttu-id="80006-140">Se trata de un formato altamente optimizado y eficiente para almacenar datos de Hive.</span><span class="sxs-lookup"><span data-stu-id="80006-140">This is a highly optimized and efficient format for storing Hive data.</span></span>
   * <span data-ttu-id="80006-141">**INSERT OVERWRITE ... Seleccione**: selecciona las filas de hello **log4jLogs** tabla que contenga **[ERROR]**, a continuación, inserta Hola datos en hello **registros de errores de** tabla.</span><span class="sxs-lookup"><span data-stu-id="80006-141">**INSERT OVERWRITE ... SELECT**: Selects rows from hello **log4jLogs** table that contain **[ERROR]**, then inserts hello data into hello **errorLogs** table.</span></span>

     <span data-ttu-id="80006-142">tooverify que solo las filas que contienen **[ERROR]** en columna t4 estaban almacenado toohello **registros de errores de** tablas, utilice Hola después tooreturn instrucción todos Hola filas de **registros de errores de**:</span><span class="sxs-lookup"><span data-stu-id="80006-142">tooverify that only rows that contain **[ERROR]** in column t4 were stored toohello **errorLogs** table, use hello following statement tooreturn all hello rows from **errorLogs**:</span></span>

       <span data-ttu-id="80006-143">SELECT * de errorLogs;</span><span class="sxs-lookup"><span data-stu-id="80006-143">SELECT * from errorLogs;</span></span>

     <span data-ttu-id="80006-144">Se deben devolver tres filas de datos y todas ellas deben contener **[ERROR]** en la columna t4.</span><span class="sxs-lookup"><span data-stu-id="80006-144">Three rows of data should be returned, all containing **[ERROR]** in column t4.</span></span>

## <span data-ttu-id="80006-145"><a id="summary"></a>Resumen</span><span class="sxs-lookup"><span data-stu-id="80006-145"><a id="summary"></a>Summary</span></span>
<span data-ttu-id="80006-146">Como puede ver, Hola Hola comando Hive proporciona un toointeractively fácilmente ejecutar consultas de Hive en un clúster de HDInsight, Hola monitor Estado del trabajo y recuperar la salida de hello.</span><span class="sxs-lookup"><span data-stu-id="80006-146">As you can see, hello hello Hive command provides an easy way toointeractively run Hive queries on an HDInsight cluster, monitor hello job status, and retrieve hello output.</span></span>

## <span data-ttu-id="80006-147"><a id="nextsteps"></a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="80006-147"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="80006-148">Para obtener información general acerca de Hive en HDInsight:</span><span class="sxs-lookup"><span data-stu-id="80006-148">For general information about Hive in HDInsight:</span></span>

* [<span data-ttu-id="80006-149">Uso de Hive con Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="80006-149">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="80006-150">Para obtener información sobre otras maneras en que puede trabajar con Hadoop en HDInsight:</span><span class="sxs-lookup"><span data-stu-id="80006-150">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="80006-151">Uso de Pig con Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="80006-151">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="80006-152">Uso de MapReduce con Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="80006-152">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="80006-153">Si usas Tez con Hive, vea Hola después de documentos para información de depuración:</span><span class="sxs-lookup"><span data-stu-id="80006-153">If you are using Tez with Hive, see hello following documents for debugging information:</span></span>

* [<span data-ttu-id="80006-154">Usar hello Tez UI en HDInsight basados en Windows</span><span class="sxs-lookup"><span data-stu-id="80006-154">Use hello Tez UI on Windows-based HDInsight</span></span>](hdinsight-debug-tez-ui.md)
* [<span data-ttu-id="80006-155">Usar hello vista Ambari Tez en HDInsight basados en Linux</span><span class="sxs-lookup"><span data-stu-id="80006-155">Use hello Ambari Tez view on Linux-based HDInsight</span></span>](hdinsight-debug-ambari-tez-view.md)

[1]: ../HDInsight/hdinsight-hadoop-visual-studio-tools-get-started.md

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





[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md


[Powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx