---
title: aaaUse Hive de Hadoop en la consola de consultas en HDInsight - Azure Hola | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse Hola basada en web consola de consultas toorun consultas de Hive en un Hadoop de HDInsight de clúster desde el explorador."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 5ae074b0-f55e-472d-94a7-005b0e79f779
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/12/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 621882082c9a07655d34b8dc980b8e47dd04b745
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="run-hive-queries-using-hello-query-console"></a><span data-ttu-id="0bfc9-103">Ejecutar consultas de Hive con hello consola de consultas</span><span class="sxs-lookup"><span data-stu-id="0bfc9-103">Run Hive queries using hello Query Console</span></span>
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="0bfc9-104">En este artículo, aprenderá cómo consultas de Hive toouse Hola consola de consultas de HDInsight toorun en un Hadoop de HDInsight de clúster desde el explorador.</span><span class="sxs-lookup"><span data-stu-id="0bfc9-104">In this article, you will learn how toouse hello HDInsight Query Console toorun Hive queries on an HDInsight Hadoop cluster from your browser.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0bfc9-105">Hola HDInsight consulta consola sólo está disponible en clústeres de HDInsight basados en Windows.</span><span class="sxs-lookup"><span data-stu-id="0bfc9-105">hello HDInsight Query Console is only available on Windows-based HDInsight clusters.</span></span> <span data-ttu-id="0bfc9-106">Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior.</span><span class="sxs-lookup"><span data-stu-id="0bfc9-106">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="0bfc9-107">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="0bfc9-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="0bfc9-108">Para HDInsight 3.4 o superior, consulte [Ejecución de consultas de Hive en la vista Hive de Ambari](hdinsight-hadoop-use-hive-ambari-view.md) para más información sobre cómo ejecutar consultas de Hive desde un explorador web.</span><span class="sxs-lookup"><span data-stu-id="0bfc9-108">For HDInsight 3.4 or greater, see [Run Hive queries in Ambari Hive View](hdinsight-hadoop-use-hive-ambari-view.md) for information on running Hive queries from a web browser.</span></span>

## <span data-ttu-id="0bfc9-109"><a id="prereq"></a>Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="0bfc9-109"><a id="prereq"></a>Prerequisites</span></span>
<span data-ttu-id="0bfc9-110">pasos de hello toocomplete en este artículo, deberá siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="0bfc9-110">toocomplete hello steps in this article, you will need hello following.</span></span>

* <span data-ttu-id="0bfc9-111">Un clúster de Hadoop para HDInsight basado en Windows</span><span class="sxs-lookup"><span data-stu-id="0bfc9-111">A Windows-based HDInsight Hadoop cluster</span></span>
* <span data-ttu-id="0bfc9-112">Un explorador web moderno</span><span class="sxs-lookup"><span data-stu-id="0bfc9-112">A modern web browser</span></span>

## <span data-ttu-id="0bfc9-113"><a id="run"></a>Ejecutar consultas de Hive con hello consola de consultas</span><span class="sxs-lookup"><span data-stu-id="0bfc9-113"><a id="run"></a> Run Hive queries using hello Query Console</span></span>
1. <span data-ttu-id="0bfc9-114">Abra un explorador web y navegue demasiado**https://CLUSTERNAME.azurehdinsight.net**, donde **CLUSTERNAME** es Hola nombre de su clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0bfc9-114">Open a web browser and navigate too**https://CLUSTERNAME.azurehdinsight.net**, where **CLUSTERNAME** is hello name of your HDInsight cluster.</span></span> <span data-ttu-id="0bfc9-115">Si se le solicite, escriba nombre de usuario de Hola y la contraseña que utilizó cuando creó el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="0bfc9-115">If prompted, enter hello user name and password that you used when you created hello cluster.</span></span>
2. <span data-ttu-id="0bfc9-116">En los vínculos de hello al principio de Hola de página de hello, seleccione **Editor de Hive**.</span><span class="sxs-lookup"><span data-stu-id="0bfc9-116">From hello links at hello top of hello page, select **Hive Editor**.</span></span> <span data-ttu-id="0bfc9-117">Esto muestra un formulario que puede ser usado tooenter hello HiveQL instrucciones que desea toorun en clúster de HDInsight de Hola.</span><span class="sxs-lookup"><span data-stu-id="0bfc9-117">This displays a form that can be used tooenter hello HiveQL statements that you want toorun in hello HDInsight cluster.</span></span>

    ![editor de subárboles Hola](./media/hdinsight-hadoop-use-hive-query-console/queryconsole.png)

    <span data-ttu-id="0bfc9-119">Reemplazar texto hello `Select * from hivesampletable` con hello siguiendo las instrucciones de HiveQL:</span><span class="sxs-lookup"><span data-stu-id="0bfc9-119">Replace hello text `Select * from hivesampletable` with hello following HiveQL statements:</span></span>

        set hive.execution.engine=tez;
        DROP TABLE log4jLogs;
        CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
        STORED AS TEXTFILE LOCATION 'wasb:///example/data/';
        SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

    <span data-ttu-id="0bfc9-120">Estas instrucciones realizan Hola siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="0bfc9-120">These statements perform hello following actions:</span></span>

   * <span data-ttu-id="0bfc9-121">**DROP TABLE**: elimina la tabla de Hola y archivo de datos de hello si Hola tabla ya existe.</span><span class="sxs-lookup"><span data-stu-id="0bfc9-121">**DROP TABLE**: Deletes hello table and hello data file if hello table already exists.</span></span>
   * <span data-ttu-id="0bfc9-122">**CREATE EXTERNAL TABLE**: crea una tabla "externa" nueva en Hive.</span><span class="sxs-lookup"><span data-stu-id="0bfc9-122">**CREATE EXTERNAL TABLE**: Creates a new 'external' table in Hive.</span></span> <span data-ttu-id="0bfc9-123">Tablas externas almacenan definición única de la tabla de hello en el subárbol; Hola datos permanecen en la ubicación original de Hola.</span><span class="sxs-lookup"><span data-stu-id="0bfc9-123">External tables store only hello table definition in Hive; hello data is left in hello original location.</span></span>

     > [!NOTE]
     > <span data-ttu-id="0bfc9-124">Tablas externas deben utilizarse cuando creas Hola subyacente toobe datos actualizado por un origen externo (por ejemplo, un proceso de carga de datos automatizado) o por otra operación de MapReduce, pero desea siempre que datos más recientes de toouse Hola de consulta de Hive.</span><span class="sxs-lookup"><span data-stu-id="0bfc9-124">External tables should be used when you expect hello underlying data toobe updated by an external source (such as an automated data upload process) or by another MapReduce operation, but you always want Hive queries toouse hello latest data.</span></span>
     >
     > <span data-ttu-id="0bfc9-125">Quitar una tabla externa **no** eliminar datos de hello, solo la definición de tabla Hola.</span><span class="sxs-lookup"><span data-stu-id="0bfc9-125">Dropping an external table does **not** delete hello data, only hello table definition.</span></span>
     >
     >
   * <span data-ttu-id="0bfc9-126">**FORMATO de fila**: indica cómo se da formato a los datos de Hola de Hive.</span><span class="sxs-lookup"><span data-stu-id="0bfc9-126">**ROW FORMAT**: Tells Hive how hello data is formatted.</span></span> <span data-ttu-id="0bfc9-127">En este caso, los campos de hello en cada registro están separados por un espacio.</span><span class="sxs-lookup"><span data-stu-id="0bfc9-127">In this case, hello fields in each log are separated by a space.</span></span>
   * <span data-ttu-id="0bfc9-128">**UBICACIÓN de archivo de texto de AS almacenados**: indica Hive donde están Hola datos almacenados (directorio de datos del ejemplo de Hola) y que se almacena como texto</span><span class="sxs-lookup"><span data-stu-id="0bfc9-128">**STORED AS TEXTFILE LOCATION**: Tells Hive where hello data is stored (hello example/data directory) and that it is stored as text</span></span>
   * <span data-ttu-id="0bfc9-129">**Seleccione**: seleccionar un recuento de todas las filas donde columna **t4** contienen el valor de hello **[ERROR]**.</span><span class="sxs-lookup"><span data-stu-id="0bfc9-129">**SELECT**: Select a count of all rows where column **t4** contain hello value **[ERROR]**.</span></span> <span data-ttu-id="0bfc9-130">Esto debe devolver un valor de **3** porque hay tres filas que contienen este valor.</span><span class="sxs-lookup"><span data-stu-id="0bfc9-130">This should return a value of **3** because there are three rows that contain this value.</span></span>
   * <span data-ttu-id="0bfc9-131">**INPUT__FILE__NAME LIKE '%.log'**: indica a Hive que solo deberíamos devolver datos de archivos que terminan en .log.</span><span class="sxs-lookup"><span data-stu-id="0bfc9-131">**INPUT__FILE__NAME LIKE '%.log'** - Tells Hive that we should only return data from files ending in .log.</span></span> <span data-ttu-id="0bfc9-132">Así restringe hello toohello sample.log archivo de búsqueda contiene datos de Hola y mantiene devuelvan datos del ejemplo de otro archivos de datos que no coinciden con el esquema de Hola que se define.</span><span class="sxs-lookup"><span data-stu-id="0bfc9-132">This restricts hello search toohello sample.log file that contains hello data, and keeps it from returning data from other example data files that do not match hello schema we defined.</span></span>
3. <span data-ttu-id="0bfc9-133">Haga clic en **Enviar**.</span><span class="sxs-lookup"><span data-stu-id="0bfc9-133">Click **Submit**.</span></span> <span data-ttu-id="0bfc9-134">Hola **sesión de trabajo** en hello parte inferior de la página de hello debe mostrar detalles de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="0bfc9-134">hello **Job Session** at hello bottom of hello page should display details for hello job.</span></span>
4. <span data-ttu-id="0bfc9-135">Cuando Hola **estado** cambia de campo demasiado**completado**, seleccione **ver detalles** trabajo Hola.</span><span class="sxs-lookup"><span data-stu-id="0bfc9-135">When hello **Status** field changes too**Completed**, select **View Details** for hello job.</span></span> <span data-ttu-id="0bfc9-136">En la página de detalles de Hola Hola **salida del trabajo** contiene `[ERROR]    3`.</span><span class="sxs-lookup"><span data-stu-id="0bfc9-136">On hello details page, hello **Job Output** contains `[ERROR]    3`.</span></span> <span data-ttu-id="0bfc9-137">Puede usar hello **descargar** situado bajo este toodownload de campo de un archivo que contiene la salida de hello de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="0bfc9-137">You can use hello **Download** button under this field toodownload a file that contains hello output of hello job.</span></span>

## <span data-ttu-id="0bfc9-138"><a id="summary"></a>Resumen</span><span class="sxs-lookup"><span data-stu-id="0bfc9-138"><a id="summary"></a>Summary</span></span>
<span data-ttu-id="0bfc9-139">Como puede ver, Hola consola de consultas proporciona una manera sencilla de toorun consultas de Hive en un clúster de HDInsight, supervisar el estado del trabajo de Hola y recuperar la salida de hello.</span><span class="sxs-lookup"><span data-stu-id="0bfc9-139">As you can see, hello Query Console provides an easy way toorun Hive queries in an HDInsight cluster, monitor hello job status, and retrieve hello output.</span></span>

<span data-ttu-id="0bfc9-140">Seleccione toolearn más sobre el uso de trabajos de Hive de consola de consultas de Hive toorun, **Introducción** Hola parte superior de hello consola de consultas, a continuación, utilice los ejemplos de hello que se proporcionan.</span><span class="sxs-lookup"><span data-stu-id="0bfc9-140">toolearn more about using Hive Query Console toorun Hive jobs, select **Getting Started** at hello top of hello Query Console, then use hello samples that are provided.</span></span> <span data-ttu-id="0bfc9-141">Cada ejemplo recorre de proceso de hello consiste en utilizar datos de Hive tooanalyze, incluidas explicaciones acerca de las instrucciones de HiveQL Hola utilizadas en el ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="0bfc9-141">Each sample walks through hello process of using Hive tooanalyze data, including explanations about hello HiveQL statements used in hello sample.</span></span>

## <span data-ttu-id="0bfc9-142"><a id="nextsteps"></a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0bfc9-142"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="0bfc9-143">Para obtener información general acerca de Hive en HDInsight:</span><span class="sxs-lookup"><span data-stu-id="0bfc9-143">For general information about Hive in HDInsight:</span></span>

* [<span data-ttu-id="0bfc9-144">Uso de Hive con Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="0bfc9-144">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="0bfc9-145">Para obtener información sobre otras maneras en que puede trabajar con Hadoop en HDInsight:</span><span class="sxs-lookup"><span data-stu-id="0bfc9-145">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="0bfc9-146">Uso de Pig con Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="0bfc9-146">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="0bfc9-147">Uso de MapReduce con Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="0bfc9-147">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="0bfc9-148">Si usas Tez con Hive, vea Hola después de documentos para información de depuración:</span><span class="sxs-lookup"><span data-stu-id="0bfc9-148">If you are using Tez with Hive, see hello following documents for debugging information:</span></span>

* [<span data-ttu-id="0bfc9-149">Usar hello Tez UI en HDInsight basados en Windows</span><span class="sxs-lookup"><span data-stu-id="0bfc9-149">Use hello Tez UI on Windows-based HDInsight</span></span>](hdinsight-debug-tez-ui.md)
* [<span data-ttu-id="0bfc9-150">Usar hello vista Ambari Tez en HDInsight basados en Linux</span><span class="sxs-lookup"><span data-stu-id="0bfc9-150">Use hello Ambari Tez view on Linux-based HDInsight</span></span>](hdinsight-debug-ambari-tez-view.md)

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



[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md

[Powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx


[img-hdi-hive-powershell-output]: ./media/hdinsight-use-hive/HDI.Hive.PowerShell.Output.png
