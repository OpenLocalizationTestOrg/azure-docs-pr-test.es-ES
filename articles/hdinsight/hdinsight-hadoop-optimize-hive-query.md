---
title: "Optimización de las consultas de Hive en Azure HDInsight | Microsoft Docs"
description: Aprenda a optimizar sus consultas de Hive para Hadoop en HDInsight.
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: d6174c08-06aa-42ac-8e9b-8b8718d9978e
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/26/2016
ms.author: jgao
ms.openlocfilehash: edbf797e6277a65b5311e4939f5ab72776b11557
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="optimize-hive-queries-in-azure-hdinsight"></a><span data-ttu-id="0beb5-103">Optimización de las consultas de Hive en Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="0beb5-103">Optimize Hive queries in Azure HDInsight</span></span>

<span data-ttu-id="0beb5-104">De manera predeterminada, los clústeres de Hadoop no están optimizados para el rendimiento.</span><span class="sxs-lookup"><span data-stu-id="0beb5-104">By default, Hadoop clusters are not optimized for performance.</span></span> <span data-ttu-id="0beb5-105">En este artículo se tratan algunos de los métodos de optimización de rendimiento de Hive más comunes que se pueden aplicar a nuestras consultas.</span><span class="sxs-lookup"><span data-stu-id="0beb5-105">This article covers some most common Hive performance optimization methods that you can apply to your queries.</span></span>

## <a name="scale-out-worker-nodes"></a><span data-ttu-id="0beb5-106">Escalar horizontalmente nodos de trabajo</span><span class="sxs-lookup"><span data-stu-id="0beb5-106">Scale out worker nodes</span></span>

<span data-ttu-id="0beb5-107">El aumento del número de nodos de trabajo de un clúster puede aprovechar más asignadores y reductores para ejecutarse en paralelo.</span><span class="sxs-lookup"><span data-stu-id="0beb5-107">Increasing the number of worker nodes in a cluster can leverage more mappers and reducers to be run in parallel.</span></span> <span data-ttu-id="0beb5-108">Hay dos maneras de aumentar la escala horizontal en HDInsight:</span><span class="sxs-lookup"><span data-stu-id="0beb5-108">There are two ways you can increase scale out in HDInsight:</span></span>

* <span data-ttu-id="0beb5-109">En el momento de aprovisionamiento, puede especificar el número de nodos de trabajo mediante Azure Portal, Azure PowerShell y la interfaz de la línea de comandos multiplataformas.</span><span class="sxs-lookup"><span data-stu-id="0beb5-109">At the provision time, you can specify the number of worker nodes using the Azure portal, Azure PowerShell, or Cross-platform command-line interface.</span></span>  <span data-ttu-id="0beb5-110">Para más información, consulte [Creación de clústeres de Hadoop en HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="0beb5-110">For more information, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span> <span data-ttu-id="0beb5-111">En la siguiente captura de pantalla se muestra la configuración del nodo de trabajo en Azure Portal:</span><span class="sxs-lookup"><span data-stu-id="0beb5-111">The following screenshot shows the worker node configuration on the Azure portal:</span></span>
  
    ![scaleout_1][image-hdi-optimize-hive-scaleout_1]
* <span data-ttu-id="0beb5-113">En tiempo de ejecución, también puede escalar horizontalmente un clúster sin volver a crear uno:</span><span class="sxs-lookup"><span data-stu-id="0beb5-113">At the run time, you can also scale out a cluster without recreating one:</span></span>

    ![scaleout_1][image-hdi-optimize-hive-scaleout_2]

<span data-ttu-id="0beb5-115">Para más información sobre las distintas máquinas virtuales admitidas por HDInsight, vea los [precios de HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="0beb5-115">For more information about the different virtual machines supported by HDInsight, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

## <a name="enable-tez"></a><span data-ttu-id="0beb5-116">Habilitar Tez</span><span class="sxs-lookup"><span data-stu-id="0beb5-116">Enable Tez</span></span>

<span data-ttu-id="0beb5-117">[Apache Tez](http://hortonworks.com/hadoop/tez/) es un motor de ejecución alternativa al motor de MapReduce:</span><span class="sxs-lookup"><span data-stu-id="0beb5-117">[Apache Tez](http://hortonworks.com/hadoop/tez/) is an alternative execution engine to the MapReduce engine:</span></span>

![tez_1][image-hdi-optimize-hive-tez_1]

<span data-ttu-id="0beb5-119">Tez es más rápido porque:</span><span class="sxs-lookup"><span data-stu-id="0beb5-119">Tez is faster because:</span></span>

* <span data-ttu-id="0beb5-120">**Ejecuta el grafo acíclico dirigido (DAG) como un único trabajo en el motor de MapReduce**.</span><span class="sxs-lookup"><span data-stu-id="0beb5-120">**Execute Directed Acyclic Graph (DAG) as a single job in the MapReduce engine**.</span></span> <span data-ttu-id="0beb5-121">El DAG requiere que cada conjunto de asignadores vaya seguido de un conjunto de reductores.</span><span class="sxs-lookup"><span data-stu-id="0beb5-121">The DAG requires each set of mappers to be followed by one set of reducers.</span></span> <span data-ttu-id="0beb5-122">Esto hace que se ponga en marcha varios trabajos de MapReduce para cada consulta de Hive.</span><span class="sxs-lookup"><span data-stu-id="0beb5-122">This causes multiple MapReduce jobs to be spun off for each Hive query.</span></span> <span data-ttu-id="0beb5-123">Tez no tiene dicha restricción y puede procesar DAG complejo como un trabajo minimizando así la sobrecarga de inicio del trabajo.</span><span class="sxs-lookup"><span data-stu-id="0beb5-123">Tez does not have such constraint and can process complex DAG as one job thus minimizing job startup overhead.</span></span>
* <span data-ttu-id="0beb5-124">**Evita escrituras innecesarias**.</span><span class="sxs-lookup"><span data-stu-id="0beb5-124">**Avoids unnecessary writes**.</span></span> <span data-ttu-id="0beb5-125">Debido a que se están poniendo en marcha varios trabajos para la misma consulta de Hive en el motor de MapReduce, la salida de cada trabajo se escribe en HDFS para los datos intermedios.</span><span class="sxs-lookup"><span data-stu-id="0beb5-125">Due to multiple jobs being spun for the same Hive query in the MapReduce engine, the output of each job is written to HDFS for intermediate data.</span></span> <span data-ttu-id="0beb5-126">Puesto que Tez minimiza el número de trabajos para cada consulta de Hive, puede evitar la escritura innecesaria.</span><span class="sxs-lookup"><span data-stu-id="0beb5-126">Since Tez minimizes number of jobs for each Hive query it is able to avoid unnecessary write.</span></span>
* <span data-ttu-id="0beb5-127">**Reduce retrasos de inicio**.</span><span class="sxs-lookup"><span data-stu-id="0beb5-127">**Minimizes start-up delays**.</span></span> <span data-ttu-id="0beb5-128">Tez puede reducir mejor el retraso de inicio disminuyendo el número de asignadores que necesita para iniciar y mejorando también la optimización.</span><span class="sxs-lookup"><span data-stu-id="0beb5-128">Tez is better able to minimize start-up delay by reducing the number of mappers it needs to start and also improving optimization throughout.</span></span>
* <span data-ttu-id="0beb5-129">**Reutiliza contenedores**.</span><span class="sxs-lookup"><span data-stu-id="0beb5-129">**Reuses containers**.</span></span> <span data-ttu-id="0beb5-130">Siempre que es posible, Tez puede reutilizar contenedores para asegurarse de que se reduce la latencia debido al reinicio de contenedores.</span><span class="sxs-lookup"><span data-stu-id="0beb5-130">Whenever possible Tez is able to reuse containers to ensure that latency due to starting up containers is reduced.</span></span>
* <span data-ttu-id="0beb5-131">**Técnicas de optimización continua**.</span><span class="sxs-lookup"><span data-stu-id="0beb5-131">**Continuous optimization techniques**.</span></span> <span data-ttu-id="0beb5-132">Tradicionalmente, la optimización se realizó durante la fase de compilación.</span><span class="sxs-lookup"><span data-stu-id="0beb5-132">Traditionally optimization was done during compilation phase.</span></span> <span data-ttu-id="0beb5-133">Sin embargo, hay más información disponible acerca de las entradas que permiten una mejor optimización en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="0beb5-133">However more information about the inputs is available that allow for better optimization during runtime.</span></span> <span data-ttu-id="0beb5-134">Tez usa las técnicas de optimización continua que le permiten optimizar más el plan en la fase de tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="0beb5-134">Tez uses continuous optimization techniques that allows it to optimize the plan further into the runtime phase.</span></span>

<span data-ttu-id="0beb5-135">Para más detalles sobre estos conceptos, consulte [Apache TEZ](http://hortonworks.com/hadoop/tez/).</span><span class="sxs-lookup"><span data-stu-id="0beb5-135">For more details on these concepts, see [Apache TEZ](http://hortonworks.com/hadoop/tez/).</span></span>

<span data-ttu-id="0beb5-136">Puede realizar cualquier consulta de Hive habilitada con Tez anteponiendo a la consulta la siguiente configuración:</span><span class="sxs-lookup"><span data-stu-id="0beb5-136">You can make any Hive query Tez enabled by prefixing the query with the setting below:</span></span>

    set hive.execution.engine=tez;

<span data-ttu-id="0beb5-137">Los clústeres de HDInsight basados en Linux tienen Tez habilitada de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="0beb5-137">Linux-based HDInsight clusters have Tez enabled by default.</span></span>


## <a name="hive-partitioning"></a><span data-ttu-id="0beb5-138">Creación de particiones de Hive</span><span class="sxs-lookup"><span data-stu-id="0beb5-138">Hive partitioning</span></span>

<span data-ttu-id="0beb5-139">La operación de E/S es el principal cuello de botella de rendimiento para ejecutar consultas de Hive.</span><span class="sxs-lookup"><span data-stu-id="0beb5-139">I/O operation is the major performance bottleneck for running Hive queries.</span></span> <span data-ttu-id="0beb5-140">El rendimiento se puede mejorar si se puede reducir la cantidad de datos que deben leerse.</span><span class="sxs-lookup"><span data-stu-id="0beb5-140">The performance can be improved if the amount of data that needs to be read can be reduced.</span></span> <span data-ttu-id="0beb5-141">De forma predeterminada, las consultas de Hive examinan tablas completas de Hive.</span><span class="sxs-lookup"><span data-stu-id="0beb5-141">By default, Hive queries scan entire Hive tables.</span></span> <span data-ttu-id="0beb5-142">Esto es excelente para las consultas como recorridos de tabla.</span><span class="sxs-lookup"><span data-stu-id="0beb5-142">This is great for queries like table scans.</span></span> <span data-ttu-id="0beb5-143">Sin embargo, para las consultas que solo necesitan examinar una pequeña cantidad de datos (por ejemplo, consultas con filtrado), esto crea una sobrecarga innecesaria.</span><span class="sxs-lookup"><span data-stu-id="0beb5-143">However for queries that only need to scan a small amount of data (for example, queries with filtering), this behavior creates unnecessary overhead.</span></span> <span data-ttu-id="0beb5-144">La creación de particiones de Hive permite a las consultas de Hive tener acceso solo a la cantidad de datos necesaria en las tablas de Hive.</span><span class="sxs-lookup"><span data-stu-id="0beb5-144">Hive partitioning allows Hive queries to access only the necessary amount of data in Hive tables.</span></span>

<span data-ttu-id="0beb5-145">La creación de particiones de Hive se implementa mediante la reorganización de los datos sin procesar en nuevos directorios teniendo cada partición su propio directorio (donde la partición se define por el usuario).</span><span class="sxs-lookup"><span data-stu-id="0beb5-145">Hive partitioning is implemented by reorganizing the raw data into new directories with each partition having its own directory - where the partition is defined by the user.</span></span> <span data-ttu-id="0beb5-146">En el siguiente diagrama se ilustra la creación de particiones de una tabla de Hive por la columna *Año*.</span><span class="sxs-lookup"><span data-stu-id="0beb5-146">The following diagram illustrates partitioning a Hive table by the column *Year*.</span></span> <span data-ttu-id="0beb5-147">Se crea un nuevo directorio para cada año.</span><span class="sxs-lookup"><span data-stu-id="0beb5-147">A new directory is created for each year.</span></span>

![creación de particiones][image-hdi-optimize-hive-partitioning_1]

<span data-ttu-id="0beb5-149">Algunas consideraciones de particiones:</span><span class="sxs-lookup"><span data-stu-id="0beb5-149">Some partitioning considerations:</span></span>

* <span data-ttu-id="0beb5-150">**No cree particiones insuficientes**: la creación de particiones en columnas con solo unos pocos valores puede generar pocas particiones.</span><span class="sxs-lookup"><span data-stu-id="0beb5-150">**Do not under partition** - Partitioning on columns with only a few values can cause few partitions.</span></span> <span data-ttu-id="0beb5-151">Por ejemplo, la creación de particiones por sexo solo crea dos particiones (hombres y mujeres); por tanto, solo se reduce la latencia a un máximo de la mitad.</span><span class="sxs-lookup"><span data-stu-id="0beb5-151">For example, partitioning on gender only creates two partitions to be created (male and female), thus only reduce the latency by a maximum of half.</span></span>
* <span data-ttu-id="0beb5-152">**No cree particiones en exceso**: por el contrario, la creación de una partición en una columna con un valor único (por ejemplo, userid) da lugar a varias particiones.</span><span class="sxs-lookup"><span data-stu-id="0beb5-152">**Do not over partition** - On the other extreme, creating a partition on a column with a unique value (for example, userid) causes multiple partitions.</span></span> <span data-ttu-id="0beb5-153">La creación de particiones en exceso provoca mucho esfuerzo en el nodo de nombre del clúster, ya que tiene que administrar una gran cantidad de directorios.</span><span class="sxs-lookup"><span data-stu-id="0beb5-153">Over partition causes much stress on the cluster namenode as it has to handle the large number of directories.</span></span>
* <span data-ttu-id="0beb5-154">**Evite el sesgo de datos** : elija su clave de creación de particiones con cuidado de manera que todas las particiones tengan el mismo tamaño.</span><span class="sxs-lookup"><span data-stu-id="0beb5-154">**Avoid data skew** - Choose your partitioning key wisely so that all partitions are even size.</span></span> <span data-ttu-id="0beb5-155">Un ejemplo es que la creación de particiones en *Estado* puede hacer que el número de registros en California 30 veces superior al de Vermont debido a la diferencia en la población.</span><span class="sxs-lookup"><span data-stu-id="0beb5-155">An example is partitioning on *State* may cause the number of records under California to be almost 30x that of Vermont due to the difference in population.</span></span>

<span data-ttu-id="0beb5-156">Para crear una tabla de particiones, use la cláusula *Particionado por* :</span><span class="sxs-lookup"><span data-stu-id="0beb5-156">To create a partition table, use the *Partitioned By* clause:</span></span>

    CREATE TABLE lineitem_part
        (L_ORDERKEY INT, L_PARTKEY INT, L_SUPPKEY INT,L_LINENUMBER INT,
         L_QUANTITY DOUBLE, L_EXTENDEDPRICE DOUBLE, L_DISCOUNT DOUBLE,
         L_TAX DOUBLE, L_RETURNFLAG STRING, L_LINESTATUS STRING,
         L_SHIPDATE_PS STRING, L_COMMITDATE STRING, L_RECEIPTDATE            STRING, L_SHIPINSTRUCT STRING, L_SHIPMODE STRING,
         L_COMMENT STRING)
    PARTITIONED BY(L_SHIPDATE STRING)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    STORED AS TEXTFILE;

<span data-ttu-id="0beb5-157">Cuando se cree la tabla con particiones, puede crear las particiones estáticas o las particiones dinámicas.</span><span class="sxs-lookup"><span data-stu-id="0beb5-157">Once the partitioned table is created, you can either create static partitioning or dynamic partitioning.</span></span>

* <span data-ttu-id="0beb5-158">**particiones estáticas** indican que ya ha particionado datos en los directorios adecuados y que puede pedir particiones de Hive manualmente según la ubicación del directorio.</span><span class="sxs-lookup"><span data-stu-id="0beb5-158">**Static partitioning** means that you have already sharded data in the appropriate directories and you can ask Hive partitions manually based on the directory location.</span></span> <span data-ttu-id="0beb5-159">El siguiente fragmento de código es un ejemplo.</span><span class="sxs-lookup"><span data-stu-id="0beb5-159">The following code snippet is an example.</span></span>
  
        INSERT OVERWRITE TABLE lineitem_part
        PARTITION (L_SHIPDATE = ‘5/23/1996 12:00:00 AM’)
        SELECT * FROM lineitem 
        WHERE lineitem.L_SHIPDATE = ‘5/23/1996 12:00:00 AM’
  
        ALTER TABLE lineitem_part ADD PARTITION (L_SHIPDATE = ‘5/23/1996 12:00:00 AM’))
        LOCATION ‘wasb://sampledata@ignitedemo.blob.core.windows.net/partitions/5_23_1996/'
* <span data-ttu-id="0beb5-160">**La partición dinámica** significa que desea que Hive cree particiones automáticamente para usted.</span><span class="sxs-lookup"><span data-stu-id="0beb5-160">**Dynamic partitioning** means that you want Hive to create partitions automatically for you.</span></span> <span data-ttu-id="0beb5-161">Dado que ya hemos creado la tabla de particiones desde la tabla de almacenamiento temporal, lo único que debemos hacer es insertar datos en la tabla con particiones:</span><span class="sxs-lookup"><span data-stu-id="0beb5-161">Since we have already created the partitioning table from the staging table, all we need to do is insert data to the partitioned table:</span></span>
  
        SET hive.exec.dynamic.partition = true;
        SET hive.exec.dynamic.partition.mode = nonstrict;
        INSERT INTO TABLE lineitem_part
        PARTITION (L_SHIPDATE)
        SELECT L_ORDERKEY as L_ORDERKEY, L_PARTKEY as L_PARTKEY , 
             L_SUPPKEY as L_SUPPKEY, L_LINENUMBER as L_LINENUMBER,
              L_QUANTITY as L_QUANTITY, L_EXTENDEDPRICE as L_EXTENDEDPRICE,
             L_DISCOUNT as L_DISCOUNT, L_TAX as L_TAX, L_RETURNFLAG as           L_RETURNFLAG, L_LINESTATUS as L_LINESTATUS, L_SHIPDATE as           L_SHIPDATE_PS, L_COMMITDATE as L_COMMITDATE, L_RECEIPTDATE as      L_RECEIPTDATE, L_SHIPINSTRUCT as L_SHIPINSTRUCT, L_SHIPMODE as      L_SHIPMODE, L_COMMENT as L_COMMENT, L_SHIPDATE as L_SHIPDATE FROM lineitem;

<span data-ttu-id="0beb5-162">Para obtener más información, vea [Tablas con particiones](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+DDL#LanguageManualDDL-PartitionedTables).</span><span class="sxs-lookup"><span data-stu-id="0beb5-162">For more details, see [Partitioned Tables](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+DDL#LanguageManualDDL-PartitionedTables).</span></span>

## <a name="use-the-orcfile-format"></a><span data-ttu-id="0beb5-163">Usar el formato ORCFile</span><span class="sxs-lookup"><span data-stu-id="0beb5-163">Use the ORCFile format</span></span>
<span data-ttu-id="0beb5-164">Hive admite diferentes formatos de archivo.</span><span class="sxs-lookup"><span data-stu-id="0beb5-164">Hive supports different file formats.</span></span> <span data-ttu-id="0beb5-165">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="0beb5-165">For example:</span></span>

* <span data-ttu-id="0beb5-166">**Texto**: este es el formato de archivo predeterminado y funciona con la mayoría de escenarios</span><span class="sxs-lookup"><span data-stu-id="0beb5-166">**Text**: this is the default file format and works with most scenarios</span></span>
* <span data-ttu-id="0beb5-167">**Avro**: funciona bien para escenarios de interoperabilidad</span><span class="sxs-lookup"><span data-stu-id="0beb5-167">**Avro**: works well for interoperability scenarios</span></span>
* <span data-ttu-id="0beb5-168">**ORC/Parquet**: idóneo para el rendimiento</span><span class="sxs-lookup"><span data-stu-id="0beb5-168">**ORC/Parquet**: best suited for performance</span></span>

<span data-ttu-id="0beb5-169">El formato ORC (Optimized Row Columnar) es una manera muy eficaz de almacenar datos de Hive.</span><span class="sxs-lookup"><span data-stu-id="0beb5-169">ORC (Optimized Row Columnar) format is a highly efficient way to store Hive data.</span></span> <span data-ttu-id="0beb5-170">En comparación con otros formatos, ORC tiene las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="0beb5-170">Compared to other formats, ORC has the following advantages:</span></span>

* <span data-ttu-id="0beb5-171">compatibilidad con tipos complejos incluidos DateTime y tipos complejos y semiestructurados</span><span class="sxs-lookup"><span data-stu-id="0beb5-171">support for complex types including DateTime and complex and semi-structured types</span></span>
* <span data-ttu-id="0beb5-172">hasta un 70 % de compresión</span><span class="sxs-lookup"><span data-stu-id="0beb5-172">up to 70% compression</span></span>
* <span data-ttu-id="0beb5-173">indiza cada 10 000 filas, lo que permite omitir filas</span><span class="sxs-lookup"><span data-stu-id="0beb5-173">indexes every 10,000 rows, which allow skipping rows</span></span>
* <span data-ttu-id="0beb5-174">un gran descenso en la ejecución del tiempo de ejecución</span><span class="sxs-lookup"><span data-stu-id="0beb5-174">a significant drop in run-time execution</span></span>

<span data-ttu-id="0beb5-175">Para habilitar el formato ORC, debe crear primero una tabla con la cláusula *Almacenados como ORC*:</span><span class="sxs-lookup"><span data-stu-id="0beb5-175">To enable ORC format, you first create a table with the clause *Stored as ORC*:</span></span>

    CREATE TABLE lineitem_orc_part
        (L_ORDERKEY INT, L_PARTKEY INT,L_SUPPKEY INT, L_LINENUMBER INT,
         L_QUANTITY DOUBLE, L_EXTENDEDPRICE DOUBLE, L_DISCOUNT DOUBLE,
         L_TAX DOUBLE, L_RETURNFLAG STRING, L_LINESTATUS STRING,
         L_SHIPDATE_PS STRING, L_COMMITDATE STRING, L_RECEIPTDATE STRING,
         L_SHIPINSTRUCT STRING, L_SHIPMODE STRING, L_COMMENT      STRING)
    PARTITIONED BY(L_SHIPDATE STRING)
    STORED AS ORC;

<span data-ttu-id="0beb5-176">A continuación, inserte datos en la tabla ORC desde la tabla de almacenamiento temporal.</span><span class="sxs-lookup"><span data-stu-id="0beb5-176">Next, you insert data to the ORC table from the staging table.</span></span> <span data-ttu-id="0beb5-177">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="0beb5-177">For example:</span></span>

    INSERT INTO TABLE lineitem_orc
    SELECT L_ORDERKEY as L_ORDERKEY, 
           L_PARTKEY as L_PARTKEY , 
           L_SUPPKEY as L_SUPPKEY,
           L_LINENUMBER as L_LINENUMBER,
            L_QUANTITY as L_QUANTITY, 
           L_EXTENDEDPRICE as L_EXTENDEDPRICE,
           L_DISCOUNT as L_DISCOUNT,
           L_TAX as L_TAX,
           L_RETURNFLAG as L_RETURNFLAG,
           L_LINESTATUS as L_LINESTATUS,
           L_SHIPDATE as L_SHIPDATE,
           L_COMMITDATE as L_COMMITDATE,
           L_RECEIPTDATE as L_RECEIPTDATE, 
           L_SHIPINSTRUCT as L_SHIPINSTRUCT,
           L_SHIPMODE as L_SHIPMODE,
           L_COMMENT as L_COMMENT
    FROM lineitem;

<span data-ttu-id="0beb5-178">Puede leer más sobre el formato ORC [aquí](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+ORC).</span><span class="sxs-lookup"><span data-stu-id="0beb5-178">You can read more on the ORC format [here](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+ORC).</span></span>

## <a name="vectorization"></a><span data-ttu-id="0beb5-179">Vectorización</span><span class="sxs-lookup"><span data-stu-id="0beb5-179">Vectorization</span></span>

<span data-ttu-id="0beb5-180">La vectorización permite a Hive procesar un lote de 1024 filas juntas en lugar de procesar una fila cada vez.</span><span class="sxs-lookup"><span data-stu-id="0beb5-180">Vectorization allows Hive to process a batch of 1024 rows together instead of processing one row at a time.</span></span> <span data-ttu-id="0beb5-181">Esto significa que las operaciones sencillas se realizan con mayor rapidez porque se necesita ejecutar menos código interno.</span><span class="sxs-lookup"><span data-stu-id="0beb5-181">It means that simple operations are done faster because less internal code needs to run.</span></span>

<span data-ttu-id="0beb5-182">Para habilitar la vectorización, anteponga a su consulta de Hive la siguiente configuración:</span><span class="sxs-lookup"><span data-stu-id="0beb5-182">To enable vectorization prefix your Hive query with the following setting:</span></span>

    set hive.vectorized.execution.enabled = true;

<span data-ttu-id="0beb5-183">Para obtener más información, vea [Ejecución de consultas vectorizadas](https://cwiki.apache.org/confluence/display/Hive/Vectorized+Query+Execution).</span><span class="sxs-lookup"><span data-stu-id="0beb5-183">For more information, see [Vectorized query execution](https://cwiki.apache.org/confluence/display/Hive/Vectorized+Query+Execution).</span></span>

## <a name="other-optimization-methods"></a><span data-ttu-id="0beb5-184">Otros métodos de optimización</span><span class="sxs-lookup"><span data-stu-id="0beb5-184">Other optimization methods</span></span>
<span data-ttu-id="0beb5-185">Hay más métodos de optimización que puede considerar, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="0beb5-185">There are more optimization methods that you can consider, for example:</span></span>

* <span data-ttu-id="0beb5-186">**Creación de depósitos de Hive:** una técnica que permite agrupar o segmentar grandes conjuntos de datos para optimizar el rendimiento de las consultas.</span><span class="sxs-lookup"><span data-stu-id="0beb5-186">**Hive bucketing:** a technique that allows to cluster or segment large sets of data to optimize query performance.</span></span>
* <span data-ttu-id="0beb5-187">**Optimización de combinación:** optimización de la planeación de la ejecución de consultas de Hive para mejorar la eficacia de las combinaciones y reducir la necesidad de sugerencias de usuario.</span><span class="sxs-lookup"><span data-stu-id="0beb5-187">**Join optimization:** optimization of Hive's query execution planning to improve the efficiency of joins and reduce the need for user hints.</span></span> <span data-ttu-id="0beb5-188">Para obtener más información, vea [Optimización de combinación](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+JoinOptimization#LanguageManualJoinOptimization-JoinOptimization).</span><span class="sxs-lookup"><span data-stu-id="0beb5-188">For more information, see [Join optimization](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+JoinOptimization#LanguageManualJoinOptimization-JoinOptimization).</span></span>
* <span data-ttu-id="0beb5-189">**Aumento de reductores**.</span><span class="sxs-lookup"><span data-stu-id="0beb5-189">**Increase Reducers**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0beb5-190">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0beb5-190">Next steps</span></span>
<span data-ttu-id="0beb5-191">En este artículo, ha aprendido varios métodos comunes de optimización de consultas de Hive.</span><span class="sxs-lookup"><span data-stu-id="0beb5-191">In this article, you have learned several common Hive query optimization methods.</span></span> <span data-ttu-id="0beb5-192">Para obtener más información, consulte los artículos siguientes:</span><span class="sxs-lookup"><span data-stu-id="0beb5-192">To learn more, see the following articles:</span></span>

* [<span data-ttu-id="0beb5-193">Uso de Apache Hive en HDInsight</span><span class="sxs-lookup"><span data-stu-id="0beb5-193">Use Apache Hive in HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="0beb5-194">Análisis de datos de retraso de vuelos con Hive en HDInsight</span><span class="sxs-lookup"><span data-stu-id="0beb5-194">Analyze flight delay data by using Hive in HDInsight</span></span>](hdinsight-analyze-flight-delay-data.md)
* [<span data-ttu-id="0beb5-195">Análisis de datos de Twitter con Hive en HDInsight</span><span class="sxs-lookup"><span data-stu-id="0beb5-195">Analyze Twitter data using Hive in HDInsight</span></span>](hdinsight-analyze-twitter-data.md)
* [<span data-ttu-id="0beb5-196">Análisis de datos de sensor mediante la consola de consultas de Hive en Hadoop con HDInsight</span><span class="sxs-lookup"><span data-stu-id="0beb5-196">Analyze sensor data using the Hive Query Console on Hadoop in HDInsight</span></span>](hdinsight-hive-analyze-sensor-data.md)
* [<span data-ttu-id="0beb5-197">Uso de Hive con HDInsight para analizar registros de sitios web</span><span class="sxs-lookup"><span data-stu-id="0beb5-197">Use Hive with HDInsight to analyze logs from websites</span></span>](hdinsight-hive-analyze-website-log.md)

[image-hdi-optimize-hive-scaleout_1]: ./media/hdinsight-hadoop-optimize-hive-query/scaleout_1.png
[image-hdi-optimize-hive-scaleout_2]: ./media/hdinsight-hadoop-optimize-hive-query/scaleout_2.png
[image-hdi-optimize-hive-tez_1]: ./media/hdinsight-hadoop-optimize-hive-query/tez_1.png
[image-hdi-optimize-hive-partitioning_1]: ./media/hdinsight-hadoop-optimize-hive-query/partitioning_1.png
