---
title: 'Uso de las Vistas de Ambari para trabajar con Hive en HDInsight (Hadoop): Azure | Microsoft Docs'
description: "Obtenga información acerca de cómo usar la Vista de Hive desde el explorador web para enviar consultas de Hive. La Vista de Hive es parte de la interfaz de usuario web Ambari que se proporciona con el clúster de HDInsight basado en Linux."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 1abe9104-f4b2-41b9-9161-abbc43de8294
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 80df3da4d62feb814ea2dd97c96e57954093c5c5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="use-the-hive-view-with-hadoop-in-hdinsight"></a><span data-ttu-id="eeca1-104">Uso de Vista de Hive con Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="eeca1-104">Use the Hive View with Hadoop in HDInsight</span></span>

[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="eeca1-105">Aprenda a ejecutar consultas de Hive mediante Ambari Hive View.</span><span class="sxs-lookup"><span data-stu-id="eeca1-105">Learn how to run Hive queries using Ambari Hive View.</span></span> <span data-ttu-id="eeca1-106">Ambari es una utilidad de administración y supervisión proporcionada con los clústeres de HDInsight basados en Linux.</span><span class="sxs-lookup"><span data-stu-id="eeca1-106">Ambari is a management and monitoring utility provided with Linux-based HDInsight clusters.</span></span> <span data-ttu-id="eeca1-107">Una de las características que se proporcionan a través de Ambari es una interfaz de usuario web que puede usarse para ejecutar consultas de Hive.</span><span class="sxs-lookup"><span data-stu-id="eeca1-107">One of the features provided through Ambari is a Web UI that can be used to run Hive queries.</span></span>

> [!NOTE]
> <span data-ttu-id="eeca1-108">Ambari cuenta con muchas funcionalidades que no se tratan en este documento.</span><span class="sxs-lookup"><span data-stu-id="eeca1-108">Ambari has many capabilities that are not discussed in this document.</span></span> <span data-ttu-id="eeca1-109">Para más información, consulte [Administración de clústeres de HDInsight con la interfaz de usuario web de Ambari](hdinsight-hadoop-manage-ambari.md).</span><span class="sxs-lookup"><span data-stu-id="eeca1-109">For more information, see [Manage HDInsight clusters by using the Ambari Web UI](hdinsight-hadoop-manage-ambari.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="eeca1-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="eeca1-110">Prerequisites</span></span>

* <span data-ttu-id="eeca1-111">Un clúster de HDInsight basado en Linux</span><span class="sxs-lookup"><span data-stu-id="eeca1-111">A Linux-based HDInsight cluster.</span></span> <span data-ttu-id="eeca1-112">Para información sobre la creación de un clúster, consulte [Introducción a HDInsight en Linux](hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="eeca1-112">For information on creating cluster, see [Get started with Linux-based HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="eeca1-113">Los pasos descritos en este documento requieren un clúster de HDInsight que use Linux.</span><span class="sxs-lookup"><span data-stu-id="eeca1-113">The steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="eeca1-114">Linux es el único sistema operativo que se usa en la versión 3.4 de HDInsight, o en las superiores.</span><span class="sxs-lookup"><span data-stu-id="eeca1-114">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="eeca1-115">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="eeca1-115">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="open-the-hive-view"></a><span data-ttu-id="eeca1-116">Abra la Vista de Hive.</span><span class="sxs-lookup"><span data-stu-id="eeca1-116">Open the Hive view</span></span>

<span data-ttu-id="eeca1-117">Para ver Vistas Ambari en Azure Portal, seleccione el clúster de HDInsight y **Vistas de Ambari** en la sección **Vínculos rápidos**.</span><span class="sxs-lookup"><span data-stu-id="eeca1-117">You can Ambari Views from the Azure portal; select your HDInsight cluster and then select **Ambari Views** from the **Quick Links** section.</span></span>

![sección de vínculos rápidos del portal](./media/hdinsight-hadoop-use-hive-ambari-view/quicklinks.png)

<span data-ttu-id="eeca1-119">En la lista de vistas, seleccione __Vista de Hive__.</span><span class="sxs-lookup"><span data-stu-id="eeca1-119">From the list of views, select the __Hive View__.</span></span>

![La vista de Hive seleccionada](./media/hdinsight-hadoop-use-hive-ambari-view/select-hive-view.png)

> [!NOTE]
> <span data-ttu-id="eeca1-121">Al acceder a Ambari, se le pide autenticarse en el sitio.</span><span class="sxs-lookup"><span data-stu-id="eeca1-121">When accessing Ambari, you are prompted to authenticate to the site.</span></span> <span data-ttu-id="eeca1-122">Escriba el nombre de la cuenta del administrador (de manera predeterminada `admin`) y la contraseña que usó al crear el clúster.</span><span class="sxs-lookup"><span data-stu-id="eeca1-122">Enter the admin (default `admin`) account name and password you used when creating the cluster.</span></span>

<span data-ttu-id="eeca1-123">Debería ver una página similar a la siguiente imagen:</span><span class="sxs-lookup"><span data-stu-id="eeca1-123">You should see a page similar to the following image:</span></span>

![Imagen de la hoja de cálculo de consulta de la vista de Hive](./media/hdinsight-hadoop-use-hive-ambari-view/ambari-hive-view.png)

## <span data-ttu-id="eeca1-125"><a name="hivequery"></a>Ejecución de una consulta</span><span class="sxs-lookup"><span data-stu-id="eeca1-125"><a name="hivequery"></a>Run a query</span></span>

<span data-ttu-id="eeca1-126">Para ejecutar una consulta de Hive, use los pasos siguientes en la vista de Hive.</span><span class="sxs-lookup"><span data-stu-id="eeca1-126">To run a hive query, use the following steps from the Hive view.</span></span>

1. <span data-ttu-id="eeca1-127">En la pestaña __Consulta__, pegue las instrucciones HiveQL siguientes en la hoja de cálculo:</span><span class="sxs-lookup"><span data-stu-id="eeca1-127">From the __Query__ tab, paste the following HiveQL statements into the worksheet:</span></span>

    ```hiveql
    DROP TABLE log4jLogs;
    CREATE EXTERNAL TABLE log4jLogs(t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
    STORED AS TEXTFILE LOCATION '/example/data/';
    SELECT t4 AS sev, COUNT(*) AS cnt FROM log4jLogs WHERE t4 = '[ERROR]' GROUP BY t4;
    ```

    <span data-ttu-id="eeca1-128">Estas instrucciones realizan las acciones siguientes:</span><span class="sxs-lookup"><span data-stu-id="eeca1-128">These statements perform the following actions:</span></span>

   * <span data-ttu-id="eeca1-129">`DROP TABLE`: elimina la tabla y el archivo de datos, en caso de que ya exista la tabla.</span><span class="sxs-lookup"><span data-stu-id="eeca1-129">`DROP TABLE` - Deletes the table and the data file, in case the table already exists.</span></span>

   * <span data-ttu-id="eeca1-130">`CREATE EXTERNAL TABLE`: crea una nueva tabla "externa" en Hive.</span><span class="sxs-lookup"><span data-stu-id="eeca1-130">`CREATE EXTERNAL TABLE` - Creates a new "external" table in Hive.</span></span>
   <span data-ttu-id="eeca1-131">Las tablas externas solo almacenan la definición de tabla en Hive.</span><span class="sxs-lookup"><span data-stu-id="eeca1-131">External tables store only the table definition in Hive.</span></span> <span data-ttu-id="eeca1-132">Los datos permanecen en la ubicación original.</span><span class="sxs-lookup"><span data-stu-id="eeca1-132">The data is left in the original location.</span></span>

   * <span data-ttu-id="eeca1-133">`ROW FORMAT`: indica el formato de los datos.</span><span class="sxs-lookup"><span data-stu-id="eeca1-133">`ROW FORMAT` - How the data is formatted.</span></span> <span data-ttu-id="eeca1-134">En este caso, los campos de cada registro se separan mediante un espacio.</span><span class="sxs-lookup"><span data-stu-id="eeca1-134">In this case, the fields in each log are separated by a space.</span></span>

   * <span data-ttu-id="eeca1-135">`STORED AS TEXTFILE LOCATION`: indica dónde se almacenan los datos y que se almacenan como texto.</span><span class="sxs-lookup"><span data-stu-id="eeca1-135">`STORED AS TEXTFILE LOCATION` - Where the data is stored, and that it is stored as text.</span></span>

   * <span data-ttu-id="eeca1-136">`SELECT`: selecciona un recuento de todas las filas donde la columna t4 contiene el valor [ERROR].</span><span class="sxs-lookup"><span data-stu-id="eeca1-136">`SELECT` - Selects a count of all rows where column t4 contains the value [ERROR].</span></span>

     > [!NOTE]
     > <span data-ttu-id="eeca1-137">Las tablas externas se deben utilizar cuando se espera que un origen externo actualice los datos subyacentes.</span><span class="sxs-lookup"><span data-stu-id="eeca1-137">External tables should be used when you expect the underlying data to be updated by an external source.</span></span> <span data-ttu-id="eeca1-138">Por ejemplo, un proceso de carga de datos automatizado u otra operación de MapReduce.</span><span class="sxs-lookup"><span data-stu-id="eeca1-138">For example, an automated data upload process, or by another MapReduce operation.</span></span> <span data-ttu-id="eeca1-139">La eliminación de una tabla externa *no* elimina los datos, solamente la definición de tabla.</span><span class="sxs-lookup"><span data-stu-id="eeca1-139">Dropping an external table does *not* delete the data, only the table definition.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="eeca1-140">Deje la selección de __base de datos__ en el __valor predeterminado__.</span><span class="sxs-lookup"><span data-stu-id="eeca1-140">Leave the __Database__ selection at __default__.</span></span> <span data-ttu-id="eeca1-141">Los ejemplos de este documento usan la base de datos predeterminada que se incluye en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="eeca1-141">The examples in this document use the default database included with HDInsight.</span></span>

2. <span data-ttu-id="eeca1-142">Para iniciar la consulta, use el botón **Ejecutar** que se encuentra debajo de la hoja de cálculo.</span><span class="sxs-lookup"><span data-stu-id="eeca1-142">To start the query, use the **Execute** button below the worksheet.</span></span> <span data-ttu-id="eeca1-143">Su color cambia a naranja y el texto a **Detener**.</span><span class="sxs-lookup"><span data-stu-id="eeca1-143">It turns orange and the text changes to **Stop**.</span></span>

3. <span data-ttu-id="eeca1-144">Cuando haya finalizado la consulta, la pestaña **Resultados** muestra los resultados de la operación.</span><span class="sxs-lookup"><span data-stu-id="eeca1-144">Once the query has finished, The **Results** tab displays the results of the operation.</span></span> <span data-ttu-id="eeca1-145">El texto siguiente es el resultado de la consulta:</span><span class="sxs-lookup"><span data-stu-id="eeca1-145">The following text is the result of the query:</span></span>

        sev       cnt
        [ERROR]   3

    <span data-ttu-id="eeca1-146">La pestaña **Registros** puede usarse para ver la información de registro creada por el trabajo.</span><span class="sxs-lookup"><span data-stu-id="eeca1-146">The **Logs** tab can be used to view the logging information created by the job.</span></span>

   > [!TIP]
   > <span data-ttu-id="eeca1-147">El cuadro de diálogo desplegable **Guardar resultados** situado en la parte superior izquierda de la sección **Resultados del proceso de consulta** le permite descargar o guardar los resultados.</span><span class="sxs-lookup"><span data-stu-id="eeca1-147">The **Save results** drop-down dialog in the upper left of the **Query Process Results** section allows you to download or save results.</span></span>

4. <span data-ttu-id="eeca1-148">Seleccione las cuatro primeras líneas de esta consulta y después elija **Ejecutar**.</span><span class="sxs-lookup"><span data-stu-id="eeca1-148">Select the first four lines of this query, then select **Execute**.</span></span> <span data-ttu-id="eeca1-149">Observe que no hay ningún resultado cuando finaliza el trabajo.</span><span class="sxs-lookup"><span data-stu-id="eeca1-149">Notice that there are no results when the job completes.</span></span> <span data-ttu-id="eeca1-150">Al usar el botón **Ejecutar** cuando parte de la consulta está seleccionada, solo se ejecutan las instrucciones seleccionadas.</span><span class="sxs-lookup"><span data-stu-id="eeca1-150">Using the **Execute** button when part of the query is selected only runs the selected statements.</span></span> <span data-ttu-id="eeca1-151">En este caso, la selección no incluyó la instrucción final que recupera filas de la tabla.</span><span class="sxs-lookup"><span data-stu-id="eeca1-151">In this case, the selection didn't include the final statement that retrieves rows from the table.</span></span> <span data-ttu-id="eeca1-152">Si selecciona solo esa línea y usa **Ejecutar**, debería ver los resultados esperados.</span><span class="sxs-lookup"><span data-stu-id="eeca1-152">If you select just that line and use **Execute**, you should see the expected results.</span></span>

5. <span data-ttu-id="eeca1-153">Para agregar una hoja de cálculo, use el botón **Nueva hoja de cálculo** situado en la parte inferior del **Editor de consultas**.</span><span class="sxs-lookup"><span data-stu-id="eeca1-153">To add a worksheet, use the **New Worksheet** button at the bottom of the **Query Editor**.</span></span> <span data-ttu-id="eeca1-154">En la hoja de cálculo nueva, escriba las siguientes instrucciones de HiveQL:</span><span class="sxs-lookup"><span data-stu-id="eeca1-154">In the new worksheet, enter the following HiveQL statements:</span></span>

    ```hiveql
    CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
    INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]';
    ```

  <span data-ttu-id="eeca1-155">Estas instrucciones realizan las acciones siguientes:</span><span class="sxs-lookup"><span data-stu-id="eeca1-155">These statements perform the following actions:</span></span>

   * <span data-ttu-id="eeca1-156">**CREATE TABLE IF NOT EXISTS** : crea una tabla, si todavía no existe.</span><span class="sxs-lookup"><span data-stu-id="eeca1-156">**CREATE TABLE IF NOT EXISTS** - Creates a table, if it does not already exist.</span></span> <span data-ttu-id="eeca1-157">Puesto que la palabra clave **EXTERNAL** no se utiliza, se crea una tabla interna.</span><span class="sxs-lookup"><span data-stu-id="eeca1-157">Since the **EXTERNAL** keyword is not used, an internal table is created.</span></span> <span data-ttu-id="eeca1-158">Una tabla interna se almacena en el almacenamiento de datos de Hive y Hive la administra completamente.</span><span class="sxs-lookup"><span data-stu-id="eeca1-158">An internal table is stored in the Hive data warehouse and is managed completely by Hive.</span></span> <span data-ttu-id="eeca1-159">A diferencia de las tablas externas , la eliminación de una tabla interna también elimina los datos subyacentes.</span><span class="sxs-lookup"><span data-stu-id="eeca1-159">Unlike external tables, dropping an internal table deletes the underlying data as well.</span></span>

   * <span data-ttu-id="eeca1-160">**STORED AS ORC** : almacena los datos en el formato Optimized Row Columnar (ORC).</span><span class="sxs-lookup"><span data-stu-id="eeca1-160">**STORED AS ORC** - Stores the data in Optimized Row Columnar (ORC) format.</span></span> <span data-ttu-id="eeca1-161">ORC es un formato altamente optimizado y eficiente para almacenar datos de Hive.</span><span class="sxs-lookup"><span data-stu-id="eeca1-161">ORC is a highly optimized and efficient format for storing Hive data.</span></span>

   * <span data-ttu-id="eeca1-162">**INSERT OVERWRITE ... SELECT**: selecciona filas de la tabla **log4jLogs** que contienen `[ERROR]` e inserta los datos en la tabla **errorLogs**.</span><span class="sxs-lookup"><span data-stu-id="eeca1-162">**INSERT OVERWRITE ... SELECT** - Selects rows from the **log4jLogs** table that contain `[ERROR]`, and then inserts the data into the **errorLogs** table.</span></span>

     <span data-ttu-id="eeca1-163">Use el botón **Ejecutar** para ejecutar esta consulta.</span><span class="sxs-lookup"><span data-stu-id="eeca1-163">Use the **Execute** button to run this query.</span></span> <span data-ttu-id="eeca1-164">La pestaña **Resultados** no contiene ninguna información cuando la consulta devuelve cero filas.</span><span class="sxs-lookup"><span data-stu-id="eeca1-164">The **Results** tab does not contain any information when the query returns zero rows.</span></span> <span data-ttu-id="eeca1-165">El estado debe aparecer como **CORRECTO** una vez completada la consulta.</span><span class="sxs-lookup"><span data-stu-id="eeca1-165">The status should show as **SUCCEEDED** once the query completes.</span></span>

### <a name="visual-explain"></a><span data-ttu-id="eeca1-166">Explicación visual</span><span class="sxs-lookup"><span data-stu-id="eeca1-166">Visual explain</span></span>

<span data-ttu-id="eeca1-167">Para mostrar una visualización del plan de consulta, seleccione la pestaña **Explicación visual** que se encuentra debajo de la hoja de cálculo.</span><span class="sxs-lookup"><span data-stu-id="eeca1-167">To display a visualization of the query plan, select the **Visual Explain** tab below the worksheet.</span></span>

<span data-ttu-id="eeca1-168">La vista de **explicación visual** de la consulta puede ser útil para comprender el flujo de las consultas complejas.</span><span class="sxs-lookup"><span data-stu-id="eeca1-168">The **Visual Explain** view of the query can be helpful in understanding the flow of complex queries.</span></span> <span data-ttu-id="eeca1-169">Puede ver un equivalente textual de esta vista con el botón **Explicar** en el Editor de consultas.</span><span class="sxs-lookup"><span data-stu-id="eeca1-169">You can view a textual equivalent of this view by using the **Explain** button in the Query Editor.</span></span>

### <a name="tez-ui"></a><span data-ttu-id="eeca1-170">Interfaz de usuario de Tez</span><span class="sxs-lookup"><span data-stu-id="eeca1-170">Tez UI</span></span>

<span data-ttu-id="eeca1-171">Para mostrar la interfaz de usuario de Tez, seleccione la pestaña **Tez** que se encuentra debajo de la hoja de cálculo.</span><span class="sxs-lookup"><span data-stu-id="eeca1-171">To display the Tez UI for the query, select the **Tez** tab below the worksheet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="eeca1-172">Tez no se usa para resolver todas las consultas.</span><span class="sxs-lookup"><span data-stu-id="eeca1-172">Tez is not used to resolve all queries.</span></span> <span data-ttu-id="eeca1-173">Muchas consultas pueden resolverse sin necesidad de usar Tez.</span><span class="sxs-lookup"><span data-stu-id="eeca1-173">Many queries can be resolved without using Tez.</span></span> 

<span data-ttu-id="eeca1-174">Si se usó Tez para resolver la consulta, se muestra el gráfico acíclico dirigido (DAG).</span><span class="sxs-lookup"><span data-stu-id="eeca1-174">If Tez was used to resolve the query, the Directed Acyclic Graph (DAG) is displayed.</span></span> <span data-ttu-id="eeca1-175">Si desea ver el DAG para las consultas que se ejecutaron en el pasado, o depurar el proceso Tez, use la [vista de Tez](hdinsight-debug-ambari-tez-view.md) en su lugar.</span><span class="sxs-lookup"><span data-stu-id="eeca1-175">If you want to view the DAG for queries you've ran in the past, or debug the Tez process, use the [Tez View](hdinsight-debug-ambari-tez-view.md) instead.</span></span>

## <a name="view-job-history"></a><span data-ttu-id="eeca1-176">Visualización del historial de trabajos</span><span class="sxs-lookup"><span data-stu-id="eeca1-176">View job history</span></span>

<span data-ttu-id="eeca1-177">La pestaña __Trabajos__ muestra un historial de las consultas de Hive.</span><span class="sxs-lookup"><span data-stu-id="eeca1-177">The __Jobs__ tab displays a history of Hive queries.</span></span>

![Imagen del historial de trabajos](./media/hdinsight-hadoop-use-hive-ambari-view/job-history.png)

## <a name="database-tables"></a><span data-ttu-id="eeca1-179">Tablas de la base de datos</span><span class="sxs-lookup"><span data-stu-id="eeca1-179">Database tables</span></span>

<span data-ttu-id="eeca1-180">Puede usar la pestaña __Tablas__ para trabajar con tablas dentro de una base de datos de Hive.</span><span class="sxs-lookup"><span data-stu-id="eeca1-180">You can use the __Tables__ tab to work with tables within a Hive database.</span></span>

![Imagen de la pestaña de tablas](./media/hdinsight-hadoop-use-hive-ambari-view/tables.png)

## <a name="saved-queries"></a><span data-ttu-id="eeca1-182">Consultas guardadas</span><span class="sxs-lookup"><span data-stu-id="eeca1-182">Saved queries</span></span>

<span data-ttu-id="eeca1-183">En la pestaña Consulta, también puede guardar consultas si lo desea.</span><span class="sxs-lookup"><span data-stu-id="eeca1-183">From the Query tab, you can optionally save queries.</span></span> <span data-ttu-id="eeca1-184">Una vez que guarda la consulta, puede volver a usarla en la pestaña __Consultas guardadas__.</span><span class="sxs-lookup"><span data-stu-id="eeca1-184">Once saved, you can reuse the query from the __Saved Queries__ tab.</span></span>

![Imagen de la pestaña de consultas guardadas](./media/hdinsight-hadoop-use-hive-ambari-view/saved-queries.png)

## <a name="user-defined-functions"></a><span data-ttu-id="eeca1-186">Funciones definidas por el usuario</span><span class="sxs-lookup"><span data-stu-id="eeca1-186">User-defined functions</span></span>

<span data-ttu-id="eeca1-187">Hive también puede extenderse a través de funciones definidas por el usuario (UDF).</span><span class="sxs-lookup"><span data-stu-id="eeca1-187">Hive can also be extended through user-defined functions (UDF).</span></span> <span data-ttu-id="eeca1-188">Una UDF le permite implementar la funcionalidad o la lógica que no se modela con facilidad en HiveQL.</span><span class="sxs-lookup"><span data-stu-id="eeca1-188">A UDF allows you to implement functionality or logic that isn't easily modeled in HiveQL.</span></span>

<span data-ttu-id="eeca1-189">La pestaña UDF en la parte superior de la vista de Hive permite declarar y guardar un conjunto de UDF.</span><span class="sxs-lookup"><span data-stu-id="eeca1-189">The UDF tab at the top of the Hive View allows you to declare and save a set of UDFs.</span></span> <span data-ttu-id="eeca1-190">Estas UDF se pueden usar con el **Editor de consultas**.</span><span class="sxs-lookup"><span data-stu-id="eeca1-190">These UDFs can be used with the **Query Editor**.</span></span>

![Imagen de la pestaña UDF](./media/hdinsight-hadoop-use-hive-ambari-view/user-defined-functions.png)

<span data-ttu-id="eeca1-192">Una vez que haya agregado una función definida por el usuario a la Vista de Hive, aparecerá un botón **Insertar UDF** en la parte inferior del **Editor de consultas**.</span><span class="sxs-lookup"><span data-stu-id="eeca1-192">Once you have added a UDF to the Hive View, an **Insert udfs** button appears at the bottom of the **Query Editor**.</span></span> <span data-ttu-id="eeca1-193">Al seleccionar esta entrada se muestra una lista desplegable de UDF definidas en la vista de Hive.</span><span class="sxs-lookup"><span data-stu-id="eeca1-193">Selecting this entry displays a drop-down list of the UDFs defined in the Hive View.</span></span> <span data-ttu-id="eeca1-194">Al seleccionar una función definida por el usuario se agregan instrucciones HiveQL a la consulta para habilitar dicha función.</span><span class="sxs-lookup"><span data-stu-id="eeca1-194">Selecting a UDF adds HiveQL statements to your query to enable the UDF.</span></span>

<span data-ttu-id="eeca1-195">Por ejemplo, si definió una función definida por el usuario con las siguientes propiedades:</span><span class="sxs-lookup"><span data-stu-id="eeca1-195">For example, if you have defined a UDF with the following properties:</span></span>

* <span data-ttu-id="eeca1-196">Nombre de recurso: myudfs</span><span class="sxs-lookup"><span data-stu-id="eeca1-196">Resource name: myudfs</span></span>

* <span data-ttu-id="eeca1-197">Ruta de acceso de recurso: /myudfs.jar</span><span class="sxs-lookup"><span data-stu-id="eeca1-197">Resource path: /myudfs.jar</span></span>

* <span data-ttu-id="eeca1-198">Nombre de la UDF: myawesomeudf</span><span class="sxs-lookup"><span data-stu-id="eeca1-198">UDF name: myawesomeudf</span></span>

* <span data-ttu-id="eeca1-199">Nombre de la clase UDF: com.myudfs.Awesome</span><span class="sxs-lookup"><span data-stu-id="eeca1-199">UDF class name: com.myudfs.Awesome</span></span>

<span data-ttu-id="eeca1-200">Si usa el botón **Insertar UDF**, aparecerá una entrada llamada **myudfs**, con otra lista desplegable para cada función definida por el usuario establecida para ese recurso.</span><span class="sxs-lookup"><span data-stu-id="eeca1-200">Using the **Insert udfs** button displays an entry named **myudfs**, with another drop-down for each UDF defined for that resource.</span></span> <span data-ttu-id="eeca1-201">En este caso, **myawesomeudf**.</span><span class="sxs-lookup"><span data-stu-id="eeca1-201">In this case, **myawesomeudf**.</span></span> <span data-ttu-id="eeca1-202">Al seleccionar esta entrada se agrega lo siguiente al principio de la consulta:</span><span class="sxs-lookup"><span data-stu-id="eeca1-202">Selecting this entry adds the following to the beginning of the query:</span></span>

```hiveql
add jar /myudfs.jar;
create temporary function myawesomeudf as 'com.myudfs.Awesome';
```

<span data-ttu-id="eeca1-203">A continuación, puede usar la función definida por el usuario en la consulta.</span><span class="sxs-lookup"><span data-stu-id="eeca1-203">You can then use the UDF in your query.</span></span> <span data-ttu-id="eeca1-204">Por ejemplo: `SELECT myawesomeudf(name) FROM people;`.</span><span class="sxs-lookup"><span data-stu-id="eeca1-204">For example, `SELECT myawesomeudf(name) FROM people;`.</span></span>

<span data-ttu-id="eeca1-205">Para más información sobre el uso de UDF con Hive en HDInsight, consulte los siguientes documentos:</span><span class="sxs-lookup"><span data-stu-id="eeca1-205">For more information on using UDFs with Hive on HDInsight, see the following documents:</span></span>

* [<span data-ttu-id="eeca1-206">Uso de Python con Hive y Pig en HDInsight</span><span class="sxs-lookup"><span data-stu-id="eeca1-206">Using Python with Hive and Pig in HDInsight</span></span>](hdinsight-python.md)
* [<span data-ttu-id="eeca1-207">Cómo agregar una UDF de Hive personalizada a HDInsight</span><span class="sxs-lookup"><span data-stu-id="eeca1-207">How to add a custom Hive UDF to HDInsight</span></span>](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/14/how-to-add-custom-hive-udfs-to-hdinsight.aspx)

## <a name="hive-settings"></a><span data-ttu-id="eeca1-208">Configuración de Hive</span><span class="sxs-lookup"><span data-stu-id="eeca1-208">Hive settings</span></span>

<span data-ttu-id="eeca1-209">Se puede usar la configuración para cambiar los diferentes valores de Hive.</span><span class="sxs-lookup"><span data-stu-id="eeca1-209">Settings can be used to change various Hive settings.</span></span> <span data-ttu-id="eeca1-210">Por ejemplo, para cambiar el motor de ejecución de Hive de Tez (el valor predeterminado) a MapReduce.</span><span class="sxs-lookup"><span data-stu-id="eeca1-210">For example, changing the execution engine for Hive from Tez (the default) to MapReduce.</span></span>

## <span data-ttu-id="eeca1-211"><a id="nextsteps"></a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="eeca1-211"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="eeca1-212">Para obtener información general acerca de Hive en HDInsight:</span><span class="sxs-lookup"><span data-stu-id="eeca1-212">For general information on Hive in HDInsight:</span></span>

* [<span data-ttu-id="eeca1-213">Uso de Hive con Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="eeca1-213">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="eeca1-214">Para obtener información sobre otras formas en que puede trabajar con Hadoop en HDInsight:</span><span class="sxs-lookup"><span data-stu-id="eeca1-214">For information on other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="eeca1-215">Uso de Pig con Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="eeca1-215">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="eeca1-216">Uso de MapReduce con Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="eeca1-216">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
