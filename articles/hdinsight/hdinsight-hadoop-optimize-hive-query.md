---
title: las consultas aaaOptimize Hive en HDInsight de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toooptimize consultas de su subárbol para Hadoop en HDInsight."
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
ms.openlocfilehash: d27f8100e1e9f4823040ff9f693e7b78d6192c6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-hive-queries-in-azure-hdinsight"></a><span data-ttu-id="3cbfd-103">Optimización de las consultas de Hive en Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="3cbfd-103">Optimize Hive queries in Azure HDInsight</span></span>

<span data-ttu-id="3cbfd-104">De manera predeterminada, los clústeres de Hadoop no están optimizados para el rendimiento.</span><span class="sxs-lookup"><span data-stu-id="3cbfd-104">By default, Hadoop clusters are not optimized for performance.</span></span> <span data-ttu-id="3cbfd-105">Este artículo tratan algunos métodos de optimización de rendimiento de Hive más comunes que se pueden aplicar consultas tooyour.</span><span class="sxs-lookup"><span data-stu-id="3cbfd-105">This article covers some most common Hive performance optimization methods that you can apply tooyour queries.</span></span>

## <a name="scale-out-worker-nodes"></a><span data-ttu-id="3cbfd-106">Escalar horizontalmente nodos de trabajo</span><span class="sxs-lookup"><span data-stu-id="3cbfd-106">Scale out worker nodes</span></span>

<span data-ttu-id="3cbfd-107">Aumentar Hola número de nodos de trabajador en un clúster puede aprovechar más toobe asignadores y reductores ejecutar en paralelo.</span><span class="sxs-lookup"><span data-stu-id="3cbfd-107">Increasing hello number of worker nodes in a cluster can leverage more mappers and reducers toobe run in parallel.</span></span> <span data-ttu-id="3cbfd-108">Hay dos maneras de aumentar la escala horizontal en HDInsight:</span><span class="sxs-lookup"><span data-stu-id="3cbfd-108">There are two ways you can increase scale out in HDInsight:</span></span>

* <span data-ttu-id="3cbfd-109">En tiempo de aprovisionamiento de hello, puede especificar Hola número de nodos de trabajador con hello portal de Azure, Azure PowerShell o interfaz de línea de comandos entre plataformas.</span><span class="sxs-lookup"><span data-stu-id="3cbfd-109">At hello provision time, you can specify hello number of worker nodes using hello Azure portal, Azure PowerShell, or Cross-platform command-line interface.</span></span>  <span data-ttu-id="3cbfd-110">Para más información, consulte [Creación de clústeres de Hadoop en HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="3cbfd-110">For more information, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span> <span data-ttu-id="3cbfd-111">Hello captura de pantalla siguiente muestra a trabajo Hola configuración del nodo en hello portal de Azure:</span><span class="sxs-lookup"><span data-stu-id="3cbfd-111">hello following screenshot shows hello worker node configuration on hello Azure portal:</span></span>
  
    ![scaleout_1][image-hdi-optimize-hive-scaleout_1]
* <span data-ttu-id="3cbfd-113">En tiempo de ejecución de hello, también puede escalar horizontalmente un clúster sin volver a crear uno:</span><span class="sxs-lookup"><span data-stu-id="3cbfd-113">At hello run time, you can also scale out a cluster without recreating one:</span></span>

    ![scaleout_1][image-hdi-optimize-hive-scaleout_2]

<span data-ttu-id="3cbfd-115">Para obtener más información acerca de hello distintas máquinas virtuales compatibles con HDInsight, vea [precios HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="3cbfd-115">For more information about hello different virtual machines supported by HDInsight, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

## <a name="enable-tez"></a><span data-ttu-id="3cbfd-116">Habilitar Tez</span><span class="sxs-lookup"><span data-stu-id="3cbfd-116">Enable Tez</span></span>

<span data-ttu-id="3cbfd-117">[Apache Tez](http://hortonworks.com/hadoop/tez/) es un motor de ejecución alternativa motor toohello MapReduce:</span><span class="sxs-lookup"><span data-stu-id="3cbfd-117">[Apache Tez](http://hortonworks.com/hadoop/tez/) is an alternative execution engine toohello MapReduce engine:</span></span>

![tez_1][image-hdi-optimize-hive-tez_1]

<span data-ttu-id="3cbfd-119">Tez es más rápido porque:</span><span class="sxs-lookup"><span data-stu-id="3cbfd-119">Tez is faster because:</span></span>

* <span data-ttu-id="3cbfd-120">**Ejecutar gráfico acíclico dirigido (DAG) como un único trabajo de motor de MapReduce hello**.</span><span class="sxs-lookup"><span data-stu-id="3cbfd-120">**Execute Directed Acyclic Graph (DAG) as a single job in hello MapReduce engine**.</span></span> <span data-ttu-id="3cbfd-121">Hola DAG requiere que cada conjunto de toobe asignadores seguido de un conjunto de reductores.</span><span class="sxs-lookup"><span data-stu-id="3cbfd-121">hello DAG requires each set of mappers toobe followed by one set of reducers.</span></span> <span data-ttu-id="3cbfd-122">Esto hace que varios toobe de trabajos de MapReduce creada para cada consulta de Hive.</span><span class="sxs-lookup"><span data-stu-id="3cbfd-122">This causes multiple MapReduce jobs toobe spun off for each Hive query.</span></span> <span data-ttu-id="3cbfd-123">Tez no tiene dicha restricción y puede procesar DAG complejo como un trabajo minimizando así la sobrecarga de inicio del trabajo.</span><span class="sxs-lookup"><span data-stu-id="3cbfd-123">Tez does not have such constraint and can process complex DAG as one job thus minimizing job startup overhead.</span></span>
* <span data-ttu-id="3cbfd-124">**Evita escrituras innecesarias**.</span><span class="sxs-lookup"><span data-stu-id="3cbfd-124">**Avoids unnecessary writes**.</span></span> <span data-ttu-id="3cbfd-125">Debido a trabajos de toomultiple se creadas para hello misma consulta de Hive en el motor de MapReduce hello, salida de hello de cada trabajo se escribe tooHDFS para los datos intermedios.</span><span class="sxs-lookup"><span data-stu-id="3cbfd-125">Due toomultiple jobs being spun for hello same Hive query in hello MapReduce engine, hello output of each job is written tooHDFS for intermediate data.</span></span> <span data-ttu-id="3cbfd-126">Puesto que Tez minimiza el número de trabajos para cada consulta de Hive es capaz de tooavoid innecesarios escritura.</span><span class="sxs-lookup"><span data-stu-id="3cbfd-126">Since Tez minimizes number of jobs for each Hive query it is able tooavoid unnecessary write.</span></span>
* <span data-ttu-id="3cbfd-127">**Reduce retrasos de inicio**.</span><span class="sxs-lookup"><span data-stu-id="3cbfd-127">**Minimizes start-up delays**.</span></span> <span data-ttu-id="3cbfd-128">Tez es mejor retraso de inicio puede toominimize reduciendo el número de Hola de asignadores necesita toostart y también mejorar la optimización a lo largo.</span><span class="sxs-lookup"><span data-stu-id="3cbfd-128">Tez is better able toominimize start-up delay by reducing hello number of mappers it needs toostart and also improving optimization throughout.</span></span>
* <span data-ttu-id="3cbfd-129">**Reutiliza contenedores**.</span><span class="sxs-lookup"><span data-stu-id="3cbfd-129">**Reuses containers**.</span></span> <span data-ttu-id="3cbfd-130">Siempre que sea posible Tez es capaz de tooreuse contenedores tooensure que la latencia debido toostarting los contenedores se reduce.</span><span class="sxs-lookup"><span data-stu-id="3cbfd-130">Whenever possible Tez is able tooreuse containers tooensure that latency due toostarting up containers is reduced.</span></span>
* <span data-ttu-id="3cbfd-131">**Técnicas de optimización continua**.</span><span class="sxs-lookup"><span data-stu-id="3cbfd-131">**Continuous optimization techniques**.</span></span> <span data-ttu-id="3cbfd-132">Tradicionalmente, la optimización se realizó durante la fase de compilación.</span><span class="sxs-lookup"><span data-stu-id="3cbfd-132">Traditionally optimization was done during compilation phase.</span></span> <span data-ttu-id="3cbfd-133">Sin embargo, para obtener más información sobre las entradas de hello es disponible que permiten la mejor optimización en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="3cbfd-133">However more information about hello inputs is available that allow for better optimization during runtime.</span></span> <span data-ttu-id="3cbfd-134">Tez usa técnicas de optimización continua que permite el plan de hello toooptimize aún más en la fase de hello en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="3cbfd-134">Tez uses continuous optimization techniques that allows it toooptimize hello plan further into hello runtime phase.</span></span>

<span data-ttu-id="3cbfd-135">Para más detalles sobre estos conceptos, consulte [Apache TEZ](http://hortonworks.com/hadoop/tez/).</span><span class="sxs-lookup"><span data-stu-id="3cbfd-135">For more details on these concepts, see [Apache TEZ](http://hortonworks.com/hadoop/tez/).</span></span>

<span data-ttu-id="3cbfd-136">Puede realizar cualquier consulta de Hive Tez habilitado anteponiendo consulta Hola con configuración de hello siguiente:</span><span class="sxs-lookup"><span data-stu-id="3cbfd-136">You can make any Hive query Tez enabled by prefixing hello query with hello setting below:</span></span>

    set hive.execution.engine=tez;

<span data-ttu-id="3cbfd-137">Los clústeres de HDInsight basados en Linux tienen Tez habilitada de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="3cbfd-137">Linux-based HDInsight clusters have Tez enabled by default.</span></span>


## <a name="hive-partitioning"></a><span data-ttu-id="3cbfd-138">Creación de particiones de Hive</span><span class="sxs-lookup"><span data-stu-id="3cbfd-138">Hive partitioning</span></span>

<span data-ttu-id="3cbfd-139">Operación de E/S es el cuello de botella de rendimiento principales de Hola para ejecutar consultas de Hive.</span><span class="sxs-lookup"><span data-stu-id="3cbfd-139">I/O operation is hello major performance bottleneck for running Hive queries.</span></span> <span data-ttu-id="3cbfd-140">puede mejorar el rendimiento de Hola si cantidad Hola de datos que necesita toobe lectura puede ser reducido.</span><span class="sxs-lookup"><span data-stu-id="3cbfd-140">hello performance can be improved if hello amount of data that needs toobe read can be reduced.</span></span> <span data-ttu-id="3cbfd-141">De forma predeterminada, las consultas de Hive examinan tablas completas de Hive.</span><span class="sxs-lookup"><span data-stu-id="3cbfd-141">By default, Hive queries scan entire Hive tables.</span></span> <span data-ttu-id="3cbfd-142">Esto es excelente para las consultas como recorridos de tabla.</span><span class="sxs-lookup"><span data-stu-id="3cbfd-142">This is great for queries like table scans.</span></span> <span data-ttu-id="3cbfd-143">Sin embargo para las consultas que solo necesitan tooscan una pequeña cantidad de datos (por ejemplo, las consultas con filtrado), este comportamiento crea sobrecarga innecesaria.</span><span class="sxs-lookup"><span data-stu-id="3cbfd-143">However for queries that only need tooscan a small amount of data (for example, queries with filtering), this behavior creates unnecessary overhead.</span></span> <span data-ttu-id="3cbfd-144">Subdivisión de Hive permite Hive consultas tooaccess únicamente Hola necesaria una cantidad de datos en tablas de Hive.</span><span class="sxs-lookup"><span data-stu-id="3cbfd-144">Hive partitioning allows Hive queries tooaccess only hello necessary amount of data in Hive tables.</span></span>

<span data-ttu-id="3cbfd-145">Creación de particiones de subárbol se implementa mediante la reorganización de los datos sin procesar de hello en nuevos directorios con cada partición tiene su propio directorio - donde se define la partición de Hola por usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="3cbfd-145">Hive partitioning is implemented by reorganizing hello raw data into new directories with each partition having its own directory - where hello partition is defined by hello user.</span></span> <span data-ttu-id="3cbfd-146">Hello siguiente diagrama ilustra crear particiones de una tabla de Hive columna hello *año*.</span><span class="sxs-lookup"><span data-stu-id="3cbfd-146">hello following diagram illustrates partitioning a Hive table by hello column *Year*.</span></span> <span data-ttu-id="3cbfd-147">Se crea un nuevo directorio para cada año.</span><span class="sxs-lookup"><span data-stu-id="3cbfd-147">A new directory is created for each year.</span></span>

![creación de particiones][image-hdi-optimize-hive-partitioning_1]

<span data-ttu-id="3cbfd-149">Algunas consideraciones de particiones:</span><span class="sxs-lookup"><span data-stu-id="3cbfd-149">Some partitioning considerations:</span></span>

* <span data-ttu-id="3cbfd-150">**No cree particiones insuficientes**: la creación de particiones en columnas con solo unos pocos valores puede generar pocas particiones.</span><span class="sxs-lookup"><span data-stu-id="3cbfd-150">**Do not under partition** - Partitioning on columns with only a few values can cause few partitions.</span></span> <span data-ttu-id="3cbfd-151">Por ejemplo, creación de particiones por género solo crea dos toobe particiones creado (masculinos y femeninos), lo que solo reducen la latencia de Hola por un máximo de la mitad.</span><span class="sxs-lookup"><span data-stu-id="3cbfd-151">For example, partitioning on gender only creates two partitions toobe created (male and female), thus only reduce hello latency by a maximum of half.</span></span>
* <span data-ttu-id="3cbfd-152">**Hacer no sobre partición** : en Hola otro extremo, la creación de una partición en una columna con un valor único (por ejemplo, userid) hace que varias particiones.</span><span class="sxs-lookup"><span data-stu-id="3cbfd-152">**Do not over partition** - On hello other extreme, creating a partition on a column with a unique value (for example, userid) causes multiple partitions.</span></span> <span data-ttu-id="3cbfd-153">A través de la partición hace mucho esfuerzo en hello clúster namenode porque tiene muchos hello toohandle de directorios.</span><span class="sxs-lookup"><span data-stu-id="3cbfd-153">Over partition causes much stress on hello cluster namenode as it has toohandle hello large number of directories.</span></span>
* <span data-ttu-id="3cbfd-154">**Evite el sesgo de datos** : elija su clave de creación de particiones con cuidado de manera que todas las particiones tengan el mismo tamaño.</span><span class="sxs-lookup"><span data-stu-id="3cbfd-154">**Avoid data skew** - Choose your partitioning key wisely so that all partitions are even size.</span></span> <span data-ttu-id="3cbfd-155">Un ejemplo es crear particiones en *estado* puede hacer que Hola número de registros en California toobe casi 30 x que Vermont debido toohello diferencia de población.</span><span class="sxs-lookup"><span data-stu-id="3cbfd-155">An example is partitioning on *State* may cause hello number of records under California toobe almost 30x that of Vermont due toohello difference in population.</span></span>

<span data-ttu-id="3cbfd-156">toocreate una tabla de particiones, utilice hello *particiones por* cláusula:</span><span class="sxs-lookup"><span data-stu-id="3cbfd-156">toocreate a partition table, use hello *Partitioned By* clause:</span></span>

    CREATE TABLE lineitem_part
        (L_ORDERKEY INT, L_PARTKEY INT, L_SUPPKEY INT,L_LINENUMBER INT,
         L_QUANTITY DOUBLE, L_EXTENDEDPRICE DOUBLE, L_DISCOUNT DOUBLE,
         L_TAX DOUBLE, L_RETURNFLAG STRING, L_LINESTATUS STRING,
         L_SHIPDATE_PS STRING, L_COMMITDATE STRING, L_RECEIPTDATE            STRING, L_SHIPINSTRUCT STRING, L_SHIPMODE STRING,
         L_COMMENT STRING)
    PARTITIONED BY(L_SHIPDATE STRING)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    STORED AS TEXTFILE;

<span data-ttu-id="3cbfd-157">Una vez que se crea la tabla con particiones de hello, puede crear partición estática o dinámica particiones.</span><span class="sxs-lookup"><span data-stu-id="3cbfd-157">Once hello partitioned table is created, you can either create static partitioning or dynamic partitioning.</span></span>

* <span data-ttu-id="3cbfd-158">**Partición estática** significa que tiene datos particionados ya en hello directorios adecuados y puede pedir las particiones de Hive manualmente en función de la ubicación del directorio Hola.</span><span class="sxs-lookup"><span data-stu-id="3cbfd-158">**Static partitioning** means that you have already sharded data in hello appropriate directories and you can ask Hive partitions manually based on hello directory location.</span></span> <span data-ttu-id="3cbfd-159">Hola siguiente fragmento de código es un ejemplo.</span><span class="sxs-lookup"><span data-stu-id="3cbfd-159">hello following code snippet is an example.</span></span>
  
        INSERT OVERWRITE TABLE lineitem_part
        PARTITION (L_SHIPDATE = ‘5/23/1996 12:00:00 AM’)
        SELECT * FROM lineitem 
        WHERE lineitem.L_SHIPDATE = ‘5/23/1996 12:00:00 AM’
  
        ALTER TABLE lineitem_part ADD PARTITION (L_SHIPDATE = ‘5/23/1996 12:00:00 AM’))
        LOCATION ‘wasb://sampledata@ignitedemo.blob.core.windows.net/partitions/5_23_1996/'
* <span data-ttu-id="3cbfd-160">**Crear particiones dinámicas** significa que desee Hive toocreate particiones automáticamente para usted.</span><span class="sxs-lookup"><span data-stu-id="3cbfd-160">**Dynamic partitioning** means that you want Hive toocreate partitions automatically for you.</span></span> <span data-ttu-id="3cbfd-161">Puesto que ya hemos creado Hola creación de particiones de tabla de hello tabla de ensayo, lo que debemos toodo es insertar datos toohello particiones tabla:</span><span class="sxs-lookup"><span data-stu-id="3cbfd-161">Since we have already created hello partitioning table from hello staging table, all we need toodo is insert data toohello partitioned table:</span></span>
  
        SET hive.exec.dynamic.partition = true;
        SET hive.exec.dynamic.partition.mode = nonstrict;
        INSERT INTO TABLE lineitem_part
        PARTITION (L_SHIPDATE)
        SELECT L_ORDERKEY as L_ORDERKEY, L_PARTKEY as L_PARTKEY , 
             L_SUPPKEY as L_SUPPKEY, L_LINENUMBER as L_LINENUMBER,
              L_QUANTITY as L_QUANTITY, L_EXTENDEDPRICE as L_EXTENDEDPRICE,
             L_DISCOUNT as L_DISCOUNT, L_TAX as L_TAX, L_RETURNFLAG as           L_RETURNFLAG, L_LINESTATUS as L_LINESTATUS, L_SHIPDATE as           L_SHIPDATE_PS, L_COMMITDATE as L_COMMITDATE, L_RECEIPTDATE as      L_RECEIPTDATE, L_SHIPINSTRUCT as L_SHIPINSTRUCT, L_SHIPMODE as      L_SHIPMODE, L_COMMENT as L_COMMENT, L_SHIPDATE as L_SHIPDATE FROM lineitem;

<span data-ttu-id="3cbfd-162">Para obtener más información, vea [Tablas con particiones](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+DDL#LanguageManualDDL-PartitionedTables).</span><span class="sxs-lookup"><span data-stu-id="3cbfd-162">For more details, see [Partitioned Tables](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+DDL#LanguageManualDDL-PartitionedTables).</span></span>

## <a name="use-hello-orcfile-format"></a><span data-ttu-id="3cbfd-163">Usar el formato de ORCFile Hola</span><span class="sxs-lookup"><span data-stu-id="3cbfd-163">Use hello ORCFile format</span></span>
<span data-ttu-id="3cbfd-164">Hive admite diferentes formatos de archivo.</span><span class="sxs-lookup"><span data-stu-id="3cbfd-164">Hive supports different file formats.</span></span> <span data-ttu-id="3cbfd-165">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="3cbfd-165">For example:</span></span>

* <span data-ttu-id="3cbfd-166">**Texto**: este es el formato de archivo predeterminado de Hola y funciona con la mayoría de los escenarios</span><span class="sxs-lookup"><span data-stu-id="3cbfd-166">**Text**: this is hello default file format and works with most scenarios</span></span>
* <span data-ttu-id="3cbfd-167">**Avro**: funciona bien para escenarios de interoperabilidad</span><span class="sxs-lookup"><span data-stu-id="3cbfd-167">**Avro**: works well for interoperability scenarios</span></span>
* <span data-ttu-id="3cbfd-168">**ORC/Parquet**: idóneo para el rendimiento</span><span class="sxs-lookup"><span data-stu-id="3cbfd-168">**ORC/Parquet**: best suited for performance</span></span>

<span data-ttu-id="3cbfd-169">Formato ORC (columnas de fila optimizado) es un toostore de manera muy eficaz datos de Hive.</span><span class="sxs-lookup"><span data-stu-id="3cbfd-169">ORC (Optimized Row Columnar) format is a highly efficient way toostore Hive data.</span></span> <span data-ttu-id="3cbfd-170">Formatos de tooother comparados, ORC tiene Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="3cbfd-170">Compared tooother formats, ORC has hello following advantages:</span></span>

* <span data-ttu-id="3cbfd-171">compatibilidad con tipos complejos incluidos DateTime y tipos complejos y semiestructurados</span><span class="sxs-lookup"><span data-stu-id="3cbfd-171">support for complex types including DateTime and complex and semi-structured types</span></span>
* <span data-ttu-id="3cbfd-172">la compresión de % too70</span><span class="sxs-lookup"><span data-stu-id="3cbfd-172">up too70% compression</span></span>
* <span data-ttu-id="3cbfd-173">indiza cada 10 000 filas, lo que permite omitir filas</span><span class="sxs-lookup"><span data-stu-id="3cbfd-173">indexes every 10,000 rows, which allow skipping rows</span></span>
* <span data-ttu-id="3cbfd-174">un gran descenso en la ejecución del tiempo de ejecución</span><span class="sxs-lookup"><span data-stu-id="3cbfd-174">a significant drop in run-time execution</span></span>

<span data-ttu-id="3cbfd-175">formato de tooenable ORC, se cree primero una tabla con la cláusula de hello *almacenados como ORC*:</span><span class="sxs-lookup"><span data-stu-id="3cbfd-175">tooenable ORC format, you first create a table with hello clause *Stored as ORC*:</span></span>

    CREATE TABLE lineitem_orc_part
        (L_ORDERKEY INT, L_PARTKEY INT,L_SUPPKEY INT, L_LINENUMBER INT,
         L_QUANTITY DOUBLE, L_EXTENDEDPRICE DOUBLE, L_DISCOUNT DOUBLE,
         L_TAX DOUBLE, L_RETURNFLAG STRING, L_LINESTATUS STRING,
         L_SHIPDATE_PS STRING, L_COMMITDATE STRING, L_RECEIPTDATE STRING,
         L_SHIPINSTRUCT STRING, L_SHIPMODE STRING, L_COMMENT      STRING)
    PARTITIONED BY(L_SHIPDATE STRING)
    STORED AS ORC;

<span data-ttu-id="3cbfd-176">A continuación, Insertar tabla de datos toohello ORC de hello tabla de ensayo.</span><span class="sxs-lookup"><span data-stu-id="3cbfd-176">Next, you insert data toohello ORC table from hello staging table.</span></span> <span data-ttu-id="3cbfd-177">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="3cbfd-177">For example:</span></span>

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

<span data-ttu-id="3cbfd-178">Puede leer más en formato de hello ORC [aquí](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+ORC).</span><span class="sxs-lookup"><span data-stu-id="3cbfd-178">You can read more on hello ORC format [here](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+ORC).</span></span>

## <a name="vectorization"></a><span data-ttu-id="3cbfd-179">Vectorización</span><span class="sxs-lookup"><span data-stu-id="3cbfd-179">Vectorization</span></span>

<span data-ttu-id="3cbfd-180">Permite que la vectorización Hive tooprocess un lote de 1024 filas entre sí en lugar de procesar una fila a la vez.</span><span class="sxs-lookup"><span data-stu-id="3cbfd-180">Vectorization allows Hive tooprocess a batch of 1024 rows together instead of processing one row at a time.</span></span> <span data-ttu-id="3cbfd-181">Significa que se realizan operaciones sencillas con mayor rapidez porque menos código interno debe toorun.</span><span class="sxs-lookup"><span data-stu-id="3cbfd-181">It means that simple operations are done faster because less internal code needs toorun.</span></span>

<span data-ttu-id="3cbfd-182">la vectorización tooenable prefijo su consulta de Hive con hello después de configuración:</span><span class="sxs-lookup"><span data-stu-id="3cbfd-182">tooenable vectorization prefix your Hive query with hello following setting:</span></span>

    set hive.vectorized.execution.enabled = true;

<span data-ttu-id="3cbfd-183">Para obtener más información, vea [Ejecución de consultas vectorizadas](https://cwiki.apache.org/confluence/display/Hive/Vectorized+Query+Execution).</span><span class="sxs-lookup"><span data-stu-id="3cbfd-183">For more information, see [Vectorized query execution](https://cwiki.apache.org/confluence/display/Hive/Vectorized+Query+Execution).</span></span>

## <a name="other-optimization-methods"></a><span data-ttu-id="3cbfd-184">Otros métodos de optimización</span><span class="sxs-lookup"><span data-stu-id="3cbfd-184">Other optimization methods</span></span>
<span data-ttu-id="3cbfd-185">Hay más métodos de optimización que puede considerar, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="3cbfd-185">There are more optimization methods that you can consider, for example:</span></span>

* <span data-ttu-id="3cbfd-186">**Creación de depósitos de Hive:** una técnica que permite toocluster o segmento conjuntos grandes de rendimiento de consultas de datos toooptimize.</span><span class="sxs-lookup"><span data-stu-id="3cbfd-186">**Hive bucketing:** a technique that allows toocluster or segment large sets of data toooptimize query performance.</span></span>
* <span data-ttu-id="3cbfd-187">**Optimización de la combinación:** optimización del subárbol ejecución de consulta planeación tooimprove Hola eficacia de combinaciones y reducir la necesidad de Hola de sugerencias de usuario.</span><span class="sxs-lookup"><span data-stu-id="3cbfd-187">**Join optimization:** optimization of Hive's query execution planning tooimprove hello efficiency of joins and reduce hello need for user hints.</span></span> <span data-ttu-id="3cbfd-188">Para obtener más información, vea [Optimización de combinación](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+JoinOptimization#LanguageManualJoinOptimization-JoinOptimization).</span><span class="sxs-lookup"><span data-stu-id="3cbfd-188">For more information, see [Join optimization](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+JoinOptimization#LanguageManualJoinOptimization-JoinOptimization).</span></span>
* <span data-ttu-id="3cbfd-189">**Aumento de reductores**.</span><span class="sxs-lookup"><span data-stu-id="3cbfd-189">**Increase Reducers**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3cbfd-190">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3cbfd-190">Next steps</span></span>
<span data-ttu-id="3cbfd-191">En este artículo, ha aprendido varios métodos comunes de optimización de consultas de Hive.</span><span class="sxs-lookup"><span data-stu-id="3cbfd-191">In this article, you have learned several common Hive query optimization methods.</span></span> <span data-ttu-id="3cbfd-192">toolearn más información, vea Hola siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="3cbfd-192">toolearn more, see hello following articles:</span></span>

* [<span data-ttu-id="3cbfd-193">Uso de Apache Hive en HDInsight</span><span class="sxs-lookup"><span data-stu-id="3cbfd-193">Use Apache Hive in HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="3cbfd-194">Análisis de datos de retraso de vuelos con Hive en HDInsight</span><span class="sxs-lookup"><span data-stu-id="3cbfd-194">Analyze flight delay data by using Hive in HDInsight</span></span>](hdinsight-analyze-flight-delay-data.md)
* [<span data-ttu-id="3cbfd-195">Análisis de datos de Twitter con Hive en HDInsight</span><span class="sxs-lookup"><span data-stu-id="3cbfd-195">Analyze Twitter data using Hive in HDInsight</span></span>](hdinsight-analyze-twitter-data.md)
* [<span data-ttu-id="3cbfd-196">Analizar datos de sensor mediante Hola consola de consultas de Hive en Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="3cbfd-196">Analyze sensor data using hello Hive Query Console on Hadoop in HDInsight</span></span>](hdinsight-hive-analyze-sensor-data.md)
* [<span data-ttu-id="3cbfd-197">Usar el subárbol con HDInsight tooanalyze registros de sitios Web</span><span class="sxs-lookup"><span data-stu-id="3cbfd-197">Use Hive with HDInsight tooanalyze logs from websites</span></span>](hdinsight-hive-analyze-website-log.md)

[image-hdi-optimize-hive-scaleout_1]: ./media/hdinsight-hadoop-optimize-hive-query/scaleout_1.png
[image-hdi-optimize-hive-scaleout_2]: ./media/hdinsight-hadoop-optimize-hive-query/scaleout_2.png
[image-hdi-optimize-hive-tez_1]: ./media/hdinsight-hadoop-optimize-hive-query/tez_1.png
[image-hdi-optimize-hive-partitioning_1]: ./media/hdinsight-hadoop-optimize-hive-query/partitioning_1.png
