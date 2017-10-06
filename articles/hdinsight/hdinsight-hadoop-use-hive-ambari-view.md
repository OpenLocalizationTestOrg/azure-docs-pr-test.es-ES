---
title: aaaUse Ambari vistas toowork con Hive en HDInsight (Hadoop) - Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse Hola Hive vista de las consultas de Hive de toosubmit de explorador web. Hola Hive vista forma parte de hello que ambari Web UI proporcionado con el clúster de HDInsight basados en Linux."
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
ms.openlocfilehash: f9a77b652e70d34a0ff9165fbb8c2e16d3401ae0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-hive-view-with-hadoop-in-hdinsight"></a><span data-ttu-id="ba1a3-104">Usar hello vista Hive con Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="ba1a3-104">Use hello Hive View with Hadoop in HDInsight</span></span>

[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="ba1a3-105">Obtenga información acerca de cómo las consultas que utilizan la vista del subárbol Ambari toorun Hive.</span><span class="sxs-lookup"><span data-stu-id="ba1a3-105">Learn how toorun Hive queries using Ambari Hive View.</span></span> <span data-ttu-id="ba1a3-106">Ambari es una utilidad de administración y supervisión proporcionada con los clústeres de HDInsight basados en Linux.</span><span class="sxs-lookup"><span data-stu-id="ba1a3-106">Ambari is a management and monitoring utility provided with Linux-based HDInsight clusters.</span></span> <span data-ttu-id="ba1a3-107">Una de las características de hello proporcionados a través de Ambari es una interfaz de usuario Web que pueden ser consultas de Hive toorun usado.</span><span class="sxs-lookup"><span data-stu-id="ba1a3-107">One of hello features provided through Ambari is a Web UI that can be used toorun Hive queries.</span></span>

> [!NOTE]
> <span data-ttu-id="ba1a3-108">Ambari cuenta con muchas funcionalidades que no se tratan en este documento.</span><span class="sxs-lookup"><span data-stu-id="ba1a3-108">Ambari has many capabilities that are not discussed in this document.</span></span> <span data-ttu-id="ba1a3-109">Para obtener más información, consulte [HDInsight administrar clústeres mediante el uso de hello Ambari Web UI](hdinsight-hadoop-manage-ambari.md).</span><span class="sxs-lookup"><span data-stu-id="ba1a3-109">For more information, see [Manage HDInsight clusters by using hello Ambari Web UI](hdinsight-hadoop-manage-ambari.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ba1a3-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="ba1a3-110">Prerequisites</span></span>

* <span data-ttu-id="ba1a3-111">Un clúster de HDInsight basado en Linux</span><span class="sxs-lookup"><span data-stu-id="ba1a3-111">A Linux-based HDInsight cluster.</span></span> <span data-ttu-id="ba1a3-112">Para información sobre la creación de un clúster, consulte [Introducción a HDInsight en Linux](hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="ba1a3-112">For information on creating cluster, see [Get started with Linux-based HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ba1a3-113">pasos de Hello en este documento requieren un clúster de HDInsight que usa Linux.</span><span class="sxs-lookup"><span data-stu-id="ba1a3-113">hello steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="ba1a3-114">Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior.</span><span class="sxs-lookup"><span data-stu-id="ba1a3-114">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="ba1a3-115">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="ba1a3-115">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="open-hello-hive-view"></a><span data-ttu-id="ba1a3-116">Abrir la vista del subárbol de Hola</span><span class="sxs-lookup"><span data-stu-id="ba1a3-116">Open hello Hive view</span></span>

<span data-ttu-id="ba1a3-117">También puede Ambari vistas de hello portal de Azure; Seleccione el clúster de HDInsight y, a continuación, seleccione **Ambari vistas** de hello **vínculos rápidos** sección.</span><span class="sxs-lookup"><span data-stu-id="ba1a3-117">You can Ambari Views from hello Azure portal; select your HDInsight cluster and then select **Ambari Views** from hello **Quick Links** section.</span></span>

![sección de vínculos rápidos de portal de Hola](./media/hdinsight-hadoop-use-hive-ambari-view/quicklinks.png)

<span data-ttu-id="ba1a3-119">En lista de Hola de vistas, seleccione hello __Hive vista__.</span><span class="sxs-lookup"><span data-stu-id="ba1a3-119">From hello list of views, select hello __Hive View__.</span></span>

![Hola vista Hive seleccionada](./media/hdinsight-hadoop-use-hive-ambari-view/select-hive-view.png)

> [!NOTE]
> <span data-ttu-id="ba1a3-121">Cuando se obtiene acceso a Ambari, son tooauthenticate solicitadas toohello sitio.</span><span class="sxs-lookup"><span data-stu-id="ba1a3-121">When accessing Ambari, you are prompted tooauthenticate toohello site.</span></span> <span data-ttu-id="ba1a3-122">Escriba Hola, administrador (valor predeterminado `admin`) cuenta de nombre y la contraseña que utilizó al crear Hola clúster.</span><span class="sxs-lookup"><span data-stu-id="ba1a3-122">Enter hello admin (default `admin`) account name and password you used when creating hello cluster.</span></span>

<span data-ttu-id="ba1a3-123">Debería ver un toohello similar de página después de la imagen:</span><span class="sxs-lookup"><span data-stu-id="ba1a3-123">You should see a page similar toohello following image:</span></span>

![Imagen de hoja de cálculo de consulta de hello para la vista del subárbol de Hola](./media/hdinsight-hadoop-use-hive-ambari-view/ambari-hive-view.png)

## <span data-ttu-id="ba1a3-125"><a name="hivequery"></a>Ejecución de una consulta</span><span class="sxs-lookup"><span data-stu-id="ba1a3-125"><a name="hivequery"></a>Run a query</span></span>

<span data-ttu-id="ba1a3-126">toorun una consulta de hive, utilice Hola siguiendo los pasos de la vista del subárbol de Hola.</span><span class="sxs-lookup"><span data-stu-id="ba1a3-126">toorun a hive query, use hello following steps from hello Hive view.</span></span>

1. <span data-ttu-id="ba1a3-127">De hello __consulta__ ficha, pegue Hola siguiendo las instrucciones de HiveQL en la hoja de cálculo de hello:</span><span class="sxs-lookup"><span data-stu-id="ba1a3-127">From hello __Query__ tab, paste hello following HiveQL statements into hello worksheet:</span></span>

    ```hiveql
    DROP TABLE log4jLogs;
    CREATE EXTERNAL TABLE log4jLogs(t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
    STORED AS TEXTFILE LOCATION '/example/data/';
    SELECT t4 AS sev, COUNT(*) AS cnt FROM log4jLogs WHERE t4 = '[ERROR]' GROUP BY t4;
    ```

    <span data-ttu-id="ba1a3-128">Estas instrucciones realizan Hola siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="ba1a3-128">These statements perform hello following actions:</span></span>

   * <span data-ttu-id="ba1a3-129">`DROP TABLE`-Elimina tabla hello y archivo de datos de hello, en caso de hello tabla ya existe.</span><span class="sxs-lookup"><span data-stu-id="ba1a3-129">`DROP TABLE` - Deletes hello table and hello data file, in case hello table already exists.</span></span>

   * <span data-ttu-id="ba1a3-130">`CREATE EXTERNAL TABLE`: crea una nueva tabla "externa" en Hive.</span><span class="sxs-lookup"><span data-stu-id="ba1a3-130">`CREATE EXTERNAL TABLE` - Creates a new "external" table in Hive.</span></span>
   <span data-ttu-id="ba1a3-131">Tablas externas almacenan solo la definición de tabla hello en el subárbol.</span><span class="sxs-lookup"><span data-stu-id="ba1a3-131">External tables store only hello table definition in Hive.</span></span> <span data-ttu-id="ba1a3-132">Hola datos permanecen en la ubicación original de Hola.</span><span class="sxs-lookup"><span data-stu-id="ba1a3-132">hello data is left in hello original location.</span></span>

   * <span data-ttu-id="ba1a3-133">`ROW FORMAT`-Cómo se da formato a los datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="ba1a3-133">`ROW FORMAT` - How hello data is formatted.</span></span> <span data-ttu-id="ba1a3-134">En este caso, los campos de hello en cada registro están separados por un espacio.</span><span class="sxs-lookup"><span data-stu-id="ba1a3-134">In this case, hello fields in each log are separated by a space.</span></span>

   * <span data-ttu-id="ba1a3-135">`STORED AS TEXTFILE LOCATION`-Donde se almacenan los datos de Hola y que se almacena como texto.</span><span class="sxs-lookup"><span data-stu-id="ba1a3-135">`STORED AS TEXTFILE LOCATION` - Where hello data is stored, and that it is stored as text.</span></span>

   * <span data-ttu-id="ba1a3-136">`SELECT`-Selecciona un recuento de todas las filas donde t4 columna contiene el valor de hello [ERROR].</span><span class="sxs-lookup"><span data-stu-id="ba1a3-136">`SELECT` - Selects a count of all rows where column t4 contains hello value [ERROR].</span></span>

     > [!NOTE]
     > <span data-ttu-id="ba1a3-137">Tablas externas deben utilizarse cuando se espera Hola subyacente datos toobe actualizado a través de un origen externo.</span><span class="sxs-lookup"><span data-stu-id="ba1a3-137">External tables should be used when you expect hello underlying data toobe updated by an external source.</span></span> <span data-ttu-id="ba1a3-138">Por ejemplo, un proceso de carga de datos automatizado u otra operación de MapReduce.</span><span class="sxs-lookup"><span data-stu-id="ba1a3-138">For example, an automated data upload process, or by another MapReduce operation.</span></span> <span data-ttu-id="ba1a3-139">Quitar una tabla externa *no* eliminar datos de hello, solo la definición de tabla Hola.</span><span class="sxs-lookup"><span data-stu-id="ba1a3-139">Dropping an external table does *not* delete hello data, only hello table definition.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="ba1a3-140">Deje hello __base de datos__ selección __predeterminado__.</span><span class="sxs-lookup"><span data-stu-id="ba1a3-140">Leave hello __Database__ selection at __default__.</span></span> <span data-ttu-id="ba1a3-141">ejemplos de Hola en este documento utiliza base de datos de hello predeterminada incluida con HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ba1a3-141">hello examples in this document use hello default database included with HDInsight.</span></span>

2. <span data-ttu-id="ba1a3-142">consulta de hello toostart, use hello **Execute** botón por debajo de la hoja de cálculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="ba1a3-142">toostart hello query, use hello **Execute** button below hello worksheet.</span></span> <span data-ttu-id="ba1a3-143">Convierte los cambios de texto hello y naranja demasiado**detener**.</span><span class="sxs-lookup"><span data-stu-id="ba1a3-143">It turns orange and hello text changes too**Stop**.</span></span>

3. <span data-ttu-id="ba1a3-144">Cuando haya finalizado la consulta de hello, Hola **resultados** ficha muestra resultados de Hola de operación de Hola.</span><span class="sxs-lookup"><span data-stu-id="ba1a3-144">Once hello query has finished, hello **Results** tab displays hello results of hello operation.</span></span> <span data-ttu-id="ba1a3-145">Hola después de texto es resultado de hello de consulta de hello:</span><span class="sxs-lookup"><span data-stu-id="ba1a3-145">hello following text is hello result of hello query:</span></span>

        sev       cnt
        [ERROR]   3

    <span data-ttu-id="ba1a3-146">Hola **registros** ficha puede ser información de registro de hello tooview usado creada por el trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="ba1a3-146">hello **Logs** tab can be used tooview hello logging information created by hello job.</span></span>

   > [!TIP]
   > <span data-ttu-id="ba1a3-147">Hola **guardar resultados** cuadro de diálogo de lista desplegable de hello superior izquierda de hello **resultados del proceso de consulta** sección permite toodownload o guardar los resultados.</span><span class="sxs-lookup"><span data-stu-id="ba1a3-147">hello **Save results** drop-down dialog in hello upper left of hello **Query Process Results** section allows you toodownload or save results.</span></span>

4. <span data-ttu-id="ba1a3-148">Seleccione Hola cuatro primeras líneas de esta consulta, a continuación, seleccione **Execute**.</span><span class="sxs-lookup"><span data-stu-id="ba1a3-148">Select hello first four lines of this query, then select **Execute**.</span></span> <span data-ttu-id="ba1a3-149">Tenga en cuenta que no hay ningún resultado, cuando se completa el trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="ba1a3-149">Notice that there are no results when hello job completes.</span></span> <span data-ttu-id="ba1a3-150">Con hello **Execute** botón si forma parte de la consulta de hello está activada solamente se ejecuta Hola instrucciones seleccionadas.</span><span class="sxs-lookup"><span data-stu-id="ba1a3-150">Using hello **Execute** button when part of hello query is selected only runs hello selected statements.</span></span> <span data-ttu-id="ba1a3-151">En este caso, selección de Hola no incluyó la instrucción final Hola que recupera filas de tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="ba1a3-151">In this case, hello selection didn't include hello final statement that retrieves rows from hello table.</span></span> <span data-ttu-id="ba1a3-152">Si selecciona sólo esa línea y usar **Execute**, debería ver los resultados de hello esperado.</span><span class="sxs-lookup"><span data-stu-id="ba1a3-152">If you select just that line and use **Execute**, you should see hello expected results.</span></span>

5. <span data-ttu-id="ba1a3-153">tooadd una hoja de cálculo, use hello **nueva hoja de cálculo** situado en la parte inferior de Hola de hello **Editor de consultas**.</span><span class="sxs-lookup"><span data-stu-id="ba1a3-153">tooadd a worksheet, use hello **New Worksheet** button at hello bottom of hello **Query Editor**.</span></span> <span data-ttu-id="ba1a3-154">En hello nueva hoja de cálculo, escriba Hola siguiendo las instrucciones de HiveQL:</span><span class="sxs-lookup"><span data-stu-id="ba1a3-154">In hello new worksheet, enter hello following HiveQL statements:</span></span>

    ```hiveql
    CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
    INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]';
    ```

  <span data-ttu-id="ba1a3-155">Estas instrucciones realizan Hola siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="ba1a3-155">These statements perform hello following actions:</span></span>

   * <span data-ttu-id="ba1a3-156">**CREATE TABLE IF NOT EXISTS** : crea una tabla, si todavía no existe.</span><span class="sxs-lookup"><span data-stu-id="ba1a3-156">**CREATE TABLE IF NOT EXISTS** - Creates a table, if it does not already exist.</span></span> <span data-ttu-id="ba1a3-157">Desde hello **externo** no se utiliza la palabra clave, se crea una tabla interna.</span><span class="sxs-lookup"><span data-stu-id="ba1a3-157">Since hello **EXTERNAL** keyword is not used, an internal table is created.</span></span> <span data-ttu-id="ba1a3-158">Una tabla interna se almacena en el almacén de datos de Hive de Hola y se administra completamente por el subárbol.</span><span class="sxs-lookup"><span data-stu-id="ba1a3-158">An internal table is stored in hello Hive data warehouse and is managed completely by Hive.</span></span> <span data-ttu-id="ba1a3-159">A diferencia de las tablas externas, al quitar una tabla interna, eliminan datos subyacente de saludo.</span><span class="sxs-lookup"><span data-stu-id="ba1a3-159">Unlike external tables, dropping an internal table deletes hello underlying data as well.</span></span>

   * <span data-ttu-id="ba1a3-160">**ALMACENA AS ORC** -almacena los datos de hello en formato optimizado fila columnas (ORC).</span><span class="sxs-lookup"><span data-stu-id="ba1a3-160">**STORED AS ORC** - Stores hello data in Optimized Row Columnar (ORC) format.</span></span> <span data-ttu-id="ba1a3-161">ORC es un formato altamente optimizado y eficiente para almacenar datos de Hive.</span><span class="sxs-lookup"><span data-stu-id="ba1a3-161">ORC is a highly optimized and efficient format for storing Hive data.</span></span>

   * <span data-ttu-id="ba1a3-162">**INSERT OVERWRITE ... Seleccione** -selecciona las filas de hello **log4jLogs** tabla que contenga `[ERROR]`, y, a continuación, inserta Hola datos en hello **registros de errores de** tabla.</span><span class="sxs-lookup"><span data-stu-id="ba1a3-162">**INSERT OVERWRITE ... SELECT** - Selects rows from hello **log4jLogs** table that contain `[ERROR]`, and then inserts hello data into hello **errorLogs** table.</span></span>

     <span data-ttu-id="ba1a3-163">Hola de uso **Execute** botón toorun esta consulta.</span><span class="sxs-lookup"><span data-stu-id="ba1a3-163">Use hello **Execute** button toorun this query.</span></span> <span data-ttu-id="ba1a3-164">Hola **resultados** ficha no contiene ninguna información cuando Hola consulta devuelve cero filas.</span><span class="sxs-lookup"><span data-stu-id="ba1a3-164">hello **Results** tab does not contain any information when hello query returns zero rows.</span></span> <span data-ttu-id="ba1a3-165">Hola estado debe aparecer como **correcto** cuando consulta Hola se haya completado.</span><span class="sxs-lookup"><span data-stu-id="ba1a3-165">hello status should show as **SUCCEEDED** once hello query completes.</span></span>

### <a name="visual-explain"></a><span data-ttu-id="ba1a3-166">Explicación visual</span><span class="sxs-lookup"><span data-stu-id="ba1a3-166">Visual explain</span></span>

<span data-ttu-id="ba1a3-167">toodisplay una visualización del plan de consulta de hello, seleccione hello **explican Visual** ficha debajo de la hoja de cálculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="ba1a3-167">toodisplay a visualization of hello query plan, select hello **Visual Explain** tab below hello worksheet.</span></span>

<span data-ttu-id="ba1a3-168">Hola **explican Visual** la vista de consulta de hello puede ser útil para comprender el flujo de Hola de consultas complejas.</span><span class="sxs-lookup"><span data-stu-id="ba1a3-168">hello **Visual Explain** view of hello query can be helpful in understanding hello flow of complex queries.</span></span> <span data-ttu-id="ba1a3-169">Puede ver un equivalente textual de esta vista mediante hello **explicativo** botón Hola Editor de consultas.</span><span class="sxs-lookup"><span data-stu-id="ba1a3-169">You can view a textual equivalent of this view by using hello **Explain** button in hello Query Editor.</span></span>

### <a name="tez-ui"></a><span data-ttu-id="ba1a3-170">Interfaz de usuario de Tez</span><span class="sxs-lookup"><span data-stu-id="ba1a3-170">Tez UI</span></span>

<span data-ttu-id="ba1a3-171">toodisplay Hola Tez UI para consulta de hello, seleccione hello **Tez** ficha debajo de la hoja de cálculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="ba1a3-171">toodisplay hello Tez UI for hello query, select hello **Tez** tab below hello worksheet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ba1a3-172">Tez es tooresolve no se utiliza en todas las consultas.</span><span class="sxs-lookup"><span data-stu-id="ba1a3-172">Tez is not used tooresolve all queries.</span></span> <span data-ttu-id="ba1a3-173">Muchas consultas pueden resolverse sin necesidad de usar Tez.</span><span class="sxs-lookup"><span data-stu-id="ba1a3-173">Many queries can be resolved without using Tez.</span></span> 

<span data-ttu-id="ba1a3-174">Si Tez estuviera consulta de hello tooresolve usado, Hola se muestra el gráfico acíclico dirigido (DAG).</span><span class="sxs-lookup"><span data-stu-id="ba1a3-174">If Tez was used tooresolve hello query, hello Directed Acyclic Graph (DAG) is displayed.</span></span> <span data-ttu-id="ba1a3-175">Si desea tooview Hola DAG para las consultas que ha ejecutado Hola anteriores o depurar Hola Tez proceso, use hello [Tez vista](hdinsight-debug-ambari-tez-view.md) en su lugar.</span><span class="sxs-lookup"><span data-stu-id="ba1a3-175">If you want tooview hello DAG for queries you've ran in hello past, or debug hello Tez process, use hello [Tez View](hdinsight-debug-ambari-tez-view.md) instead.</span></span>

## <a name="view-job-history"></a><span data-ttu-id="ba1a3-176">Visualización del historial de trabajos</span><span class="sxs-lookup"><span data-stu-id="ba1a3-176">View job history</span></span>

<span data-ttu-id="ba1a3-177">Hola __trabajos__ ficha muestra un historial de consultas de Hive.</span><span class="sxs-lookup"><span data-stu-id="ba1a3-177">hello __Jobs__ tab displays a history of Hive queries.</span></span>

![Imagen del historial de trabajos de Hola](./media/hdinsight-hadoop-use-hive-ambari-view/job-history.png)

## <a name="database-tables"></a><span data-ttu-id="ba1a3-179">Tablas de la base de datos</span><span class="sxs-lookup"><span data-stu-id="ba1a3-179">Database tables</span></span>

<span data-ttu-id="ba1a3-180">Puede usar hello __tablas__ ficha toowork con tablas en una base de datos de Hive.</span><span class="sxs-lookup"><span data-stu-id="ba1a3-180">You can use hello __Tables__ tab toowork with tables within a Hive database.</span></span>

![Imagen de la pestaña de tablas de Hola](./media/hdinsight-hadoop-use-hive-ambari-view/tables.png)

## <a name="saved-queries"></a><span data-ttu-id="ba1a3-182">Consultas guardadas</span><span class="sxs-lookup"><span data-stu-id="ba1a3-182">Saved queries</span></span>

<span data-ttu-id="ba1a3-183">Desde la pestaña de consulta de hello, si lo desea puede guardar consultas.</span><span class="sxs-lookup"><span data-stu-id="ba1a3-183">From hello Query tab, you can optionally save queries.</span></span> <span data-ttu-id="ba1a3-184">Una vez guardado, puede volver a usar consultas de Hola de hello __consultas guardadas__ ficha.</span><span class="sxs-lookup"><span data-stu-id="ba1a3-184">Once saved, you can reuse hello query from hello __Saved Queries__ tab.</span></span>

![Imagen de la pestaña de consultas guardadas](./media/hdinsight-hadoop-use-hive-ambari-view/saved-queries.png)

## <a name="user-defined-functions"></a><span data-ttu-id="ba1a3-186">Funciones definidas por el usuario</span><span class="sxs-lookup"><span data-stu-id="ba1a3-186">User-defined functions</span></span>

<span data-ttu-id="ba1a3-187">Hive también puede extenderse a través de funciones definidas por el usuario (UDF).</span><span class="sxs-lookup"><span data-stu-id="ba1a3-187">Hive can also be extended through user-defined functions (UDF).</span></span> <span data-ttu-id="ba1a3-188">Una UDF permite la funcionalidad de tooimplement o lógica que no está modelada fácilmente en HiveQL.</span><span class="sxs-lookup"><span data-stu-id="ba1a3-188">A UDF allows you tooimplement functionality or logic that isn't easily modeled in HiveQL.</span></span>

<span data-ttu-id="ba1a3-189">Hola pestaña UDF en parte superior de Hola de hello Hive vista permite toodeclare y guardar un conjunto de archivos UDF.</span><span class="sxs-lookup"><span data-stu-id="ba1a3-189">hello UDF tab at hello top of hello Hive View allows you toodeclare and save a set of UDFs.</span></span> <span data-ttu-id="ba1a3-190">Estos archivos UDF se pueden utilizar con hello **Editor de consultas**.</span><span class="sxs-lookup"><span data-stu-id="ba1a3-190">These UDFs can be used with hello **Query Editor**.</span></span>

![Imagen de la pestaña UDF](./media/hdinsight-hadoop-use-hive-ambari-view/user-defined-functions.png)

<span data-ttu-id="ba1a3-192">Una vez haya agregado una vista de Hive, de UDF toohello una **insertar UDF** botón aparece en la parte inferior de Hola de Hola **Editor de consultas**.</span><span class="sxs-lookup"><span data-stu-id="ba1a3-192">Once you have added a UDF toohello Hive View, an **Insert udfs** button appears at hello bottom of hello **Query Editor**.</span></span> <span data-ttu-id="ba1a3-193">Al seleccionar esta entrada, muestra una lista de desplegable de hello UDF definidas en hello Hive vista.</span><span class="sxs-lookup"><span data-stu-id="ba1a3-193">Selecting this entry displays a drop-down list of hello UDFs defined in hello Hive View.</span></span> <span data-ttu-id="ba1a3-194">Si selecciona una UDF, agrega HiveQL instrucciones tooyour consulta tooenable Hola UDF.</span><span class="sxs-lookup"><span data-stu-id="ba1a3-194">Selecting a UDF adds HiveQL statements tooyour query tooenable hello UDF.</span></span>

<span data-ttu-id="ba1a3-195">Por ejemplo, si ha definido una UDF con hello propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="ba1a3-195">For example, if you have defined a UDF with hello following properties:</span></span>

* <span data-ttu-id="ba1a3-196">Nombre de recurso: myudfs</span><span class="sxs-lookup"><span data-stu-id="ba1a3-196">Resource name: myudfs</span></span>

* <span data-ttu-id="ba1a3-197">Ruta de acceso de recurso: /myudfs.jar</span><span class="sxs-lookup"><span data-stu-id="ba1a3-197">Resource path: /myudfs.jar</span></span>

* <span data-ttu-id="ba1a3-198">Nombre de la UDF: myawesomeudf</span><span class="sxs-lookup"><span data-stu-id="ba1a3-198">UDF name: myawesomeudf</span></span>

* <span data-ttu-id="ba1a3-199">Nombre de la clase UDF: com.myudfs.Awesome</span><span class="sxs-lookup"><span data-stu-id="ba1a3-199">UDF class name: com.myudfs.Awesome</span></span>

<span data-ttu-id="ba1a3-200">Con hello **insertar UDF** botón muestra una entrada denominada **myudfs**, con otra lista desplegable para cada UDF definidas para ese recurso.</span><span class="sxs-lookup"><span data-stu-id="ba1a3-200">Using hello **Insert udfs** button displays an entry named **myudfs**, with another drop-down for each UDF defined for that resource.</span></span> <span data-ttu-id="ba1a3-201">En este caso, **myawesomeudf**.</span><span class="sxs-lookup"><span data-stu-id="ba1a3-201">In this case, **myawesomeudf**.</span></span> <span data-ttu-id="ba1a3-202">Si selecciona esta entrada, agrega Hola después toohello a partir de consultas de hello:</span><span class="sxs-lookup"><span data-stu-id="ba1a3-202">Selecting this entry adds hello following toohello beginning of hello query:</span></span>

```hiveql
add jar /myudfs.jar;
create temporary function myawesomeudf as 'com.myudfs.Awesome';
```

<span data-ttu-id="ba1a3-203">A continuación, puede usar Hola UDF en la consulta.</span><span class="sxs-lookup"><span data-stu-id="ba1a3-203">You can then use hello UDF in your query.</span></span> <span data-ttu-id="ba1a3-204">Por ejemplo: `SELECT myawesomeudf(name) FROM people;`.</span><span class="sxs-lookup"><span data-stu-id="ba1a3-204">For example, `SELECT myawesomeudf(name) FROM people;`.</span></span>

<span data-ttu-id="ba1a3-205">Para obtener más información sobre el uso de UDF con Hive en HDInsight, vea Hola siguientes documentos:</span><span class="sxs-lookup"><span data-stu-id="ba1a3-205">For more information on using UDFs with Hive on HDInsight, see hello following documents:</span></span>

* [<span data-ttu-id="ba1a3-206">Uso de Python con Hive y Pig en HDInsight</span><span class="sxs-lookup"><span data-stu-id="ba1a3-206">Using Python with Hive and Pig in HDInsight</span></span>](hdinsight-python.md)
* [<span data-ttu-id="ba1a3-207">¿Cómo tooadd un tooHDInsight Hive UDF personalizado</span><span class="sxs-lookup"><span data-stu-id="ba1a3-207">How tooadd a custom Hive UDF tooHDInsight</span></span>](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/14/how-to-add-custom-hive-udfs-to-hdinsight.aspx)

## <a name="hive-settings"></a><span data-ttu-id="ba1a3-208">Configuración de Hive</span><span class="sxs-lookup"><span data-stu-id="ba1a3-208">Hive settings</span></span>

<span data-ttu-id="ba1a3-209">La configuración puede ser usado toochange distintas configuraciones de Hive.</span><span class="sxs-lookup"><span data-stu-id="ba1a3-209">Settings can be used toochange various Hive settings.</span></span> <span data-ttu-id="ba1a3-210">Por ejemplo, cambiar el motor de ejecución de Hola de Hive de tooMapReduce Tez (valor predeterminado de hello).</span><span class="sxs-lookup"><span data-stu-id="ba1a3-210">For example, changing hello execution engine for Hive from Tez (hello default) tooMapReduce.</span></span>

## <span data-ttu-id="ba1a3-211"><a id="nextsteps"></a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ba1a3-211"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="ba1a3-212">Para obtener información general acerca de Hive en HDInsight:</span><span class="sxs-lookup"><span data-stu-id="ba1a3-212">For general information on Hive in HDInsight:</span></span>

* [<span data-ttu-id="ba1a3-213">Uso de Hive con Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="ba1a3-213">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="ba1a3-214">Para obtener información sobre otras formas en que puede trabajar con Hadoop en HDInsight:</span><span class="sxs-lookup"><span data-stu-id="ba1a3-214">For information on other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="ba1a3-215">Uso de Pig con Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="ba1a3-215">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="ba1a3-216">Uso de MapReduce con Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="ba1a3-216">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
