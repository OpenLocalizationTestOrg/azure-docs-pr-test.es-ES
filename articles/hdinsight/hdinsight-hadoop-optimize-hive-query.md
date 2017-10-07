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
# <a name="optimize-hive-queries-in-azure-hdinsight"></a>Optimización de las consultas de Hive en Azure HDInsight

De manera predeterminada, los clústeres de Hadoop no están optimizados para el rendimiento. Este artículo tratan algunos métodos de optimización de rendimiento de Hive más comunes que se pueden aplicar consultas tooyour.

## <a name="scale-out-worker-nodes"></a>Escalar horizontalmente nodos de trabajo

Aumentar Hola número de nodos de trabajador en un clúster puede aprovechar más toobe asignadores y reductores ejecutar en paralelo. Hay dos maneras de aumentar la escala horizontal en HDInsight:

* En tiempo de aprovisionamiento de hello, puede especificar Hola número de nodos de trabajador con hello portal de Azure, Azure PowerShell o interfaz de línea de comandos entre plataformas.  Para más información, consulte [Creación de clústeres de Hadoop en HDInsight](hdinsight-hadoop-provision-linux-clusters.md). Hello captura de pantalla siguiente muestra a trabajo Hola configuración del nodo en hello portal de Azure:
  
    ![scaleout_1][image-hdi-optimize-hive-scaleout_1]
* En tiempo de ejecución de hello, también puede escalar horizontalmente un clúster sin volver a crear uno:

    ![scaleout_1][image-hdi-optimize-hive-scaleout_2]

Para obtener más información acerca de hello distintas máquinas virtuales compatibles con HDInsight, vea [precios HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).

## <a name="enable-tez"></a>Habilitar Tez

[Apache Tez](http://hortonworks.com/hadoop/tez/) es un motor de ejecución alternativa motor toohello MapReduce:

![tez_1][image-hdi-optimize-hive-tez_1]

Tez es más rápido porque:

* **Ejecutar gráfico acíclico dirigido (DAG) como un único trabajo de motor de MapReduce hello**. Hola DAG requiere que cada conjunto de toobe asignadores seguido de un conjunto de reductores. Esto hace que varios toobe de trabajos de MapReduce creada para cada consulta de Hive. Tez no tiene dicha restricción y puede procesar DAG complejo como un trabajo minimizando así la sobrecarga de inicio del trabajo.
* **Evita escrituras innecesarias**. Debido a trabajos de toomultiple se creadas para hello misma consulta de Hive en el motor de MapReduce hello, salida de hello de cada trabajo se escribe tooHDFS para los datos intermedios. Puesto que Tez minimiza el número de trabajos para cada consulta de Hive es capaz de tooavoid innecesarios escritura.
* **Reduce retrasos de inicio**. Tez es mejor retraso de inicio puede toominimize reduciendo el número de Hola de asignadores necesita toostart y también mejorar la optimización a lo largo.
* **Reutiliza contenedores**. Siempre que sea posible Tez es capaz de tooreuse contenedores tooensure que la latencia debido toostarting los contenedores se reduce.
* **Técnicas de optimización continua**. Tradicionalmente, la optimización se realizó durante la fase de compilación. Sin embargo, para obtener más información sobre las entradas de hello es disponible que permiten la mejor optimización en tiempo de ejecución. Tez usa técnicas de optimización continua que permite el plan de hello toooptimize aún más en la fase de hello en tiempo de ejecución.

Para más detalles sobre estos conceptos, consulte [Apache TEZ](http://hortonworks.com/hadoop/tez/).

Puede realizar cualquier consulta de Hive Tez habilitado anteponiendo consulta Hola con configuración de hello siguiente:

    set hive.execution.engine=tez;

Los clústeres de HDInsight basados en Linux tienen Tez habilitada de forma predeterminada.


## <a name="hive-partitioning"></a>Creación de particiones de Hive

Operación de E/S es el cuello de botella de rendimiento principales de Hola para ejecutar consultas de Hive. puede mejorar el rendimiento de Hola si cantidad Hola de datos que necesita toobe lectura puede ser reducido. De forma predeterminada, las consultas de Hive examinan tablas completas de Hive. Esto es excelente para las consultas como recorridos de tabla. Sin embargo para las consultas que solo necesitan tooscan una pequeña cantidad de datos (por ejemplo, las consultas con filtrado), este comportamiento crea sobrecarga innecesaria. Subdivisión de Hive permite Hive consultas tooaccess únicamente Hola necesaria una cantidad de datos en tablas de Hive.

Creación de particiones de subárbol se implementa mediante la reorganización de los datos sin procesar de hello en nuevos directorios con cada partición tiene su propio directorio - donde se define la partición de Hola por usuario de Hola. Hello siguiente diagrama ilustra crear particiones de una tabla de Hive columna hello *año*. Se crea un nuevo directorio para cada año.

![creación de particiones][image-hdi-optimize-hive-partitioning_1]

Algunas consideraciones de particiones:

* **No cree particiones insuficientes**: la creación de particiones en columnas con solo unos pocos valores puede generar pocas particiones. Por ejemplo, creación de particiones por género solo crea dos toobe particiones creado (masculinos y femeninos), lo que solo reducen la latencia de Hola por un máximo de la mitad.
* **Hacer no sobre partición** : en Hola otro extremo, la creación de una partición en una columna con un valor único (por ejemplo, userid) hace que varias particiones. A través de la partición hace mucho esfuerzo en hello clúster namenode porque tiene muchos hello toohandle de directorios.
* **Evite el sesgo de datos** : elija su clave de creación de particiones con cuidado de manera que todas las particiones tengan el mismo tamaño. Un ejemplo es crear particiones en *estado* puede hacer que Hola número de registros en California toobe casi 30 x que Vermont debido toohello diferencia de población.

toocreate una tabla de particiones, utilice hello *particiones por* cláusula:

    CREATE TABLE lineitem_part
        (L_ORDERKEY INT, L_PARTKEY INT, L_SUPPKEY INT,L_LINENUMBER INT,
         L_QUANTITY DOUBLE, L_EXTENDEDPRICE DOUBLE, L_DISCOUNT DOUBLE,
         L_TAX DOUBLE, L_RETURNFLAG STRING, L_LINESTATUS STRING,
         L_SHIPDATE_PS STRING, L_COMMITDATE STRING, L_RECEIPTDATE            STRING, L_SHIPINSTRUCT STRING, L_SHIPMODE STRING,
         L_COMMENT STRING)
    PARTITIONED BY(L_SHIPDATE STRING)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    STORED AS TEXTFILE;

Una vez que se crea la tabla con particiones de hello, puede crear partición estática o dinámica particiones.

* **Partición estática** significa que tiene datos particionados ya en hello directorios adecuados y puede pedir las particiones de Hive manualmente en función de la ubicación del directorio Hola. Hola siguiente fragmento de código es un ejemplo.
  
        INSERT OVERWRITE TABLE lineitem_part
        PARTITION (L_SHIPDATE = ‘5/23/1996 12:00:00 AM’)
        SELECT * FROM lineitem 
        WHERE lineitem.L_SHIPDATE = ‘5/23/1996 12:00:00 AM’
  
        ALTER TABLE lineitem_part ADD PARTITION (L_SHIPDATE = ‘5/23/1996 12:00:00 AM’))
        LOCATION ‘wasb://sampledata@ignitedemo.blob.core.windows.net/partitions/5_23_1996/'
* **Crear particiones dinámicas** significa que desee Hive toocreate particiones automáticamente para usted. Puesto que ya hemos creado Hola creación de particiones de tabla de hello tabla de ensayo, lo que debemos toodo es insertar datos toohello particiones tabla:
  
        SET hive.exec.dynamic.partition = true;
        SET hive.exec.dynamic.partition.mode = nonstrict;
        INSERT INTO TABLE lineitem_part
        PARTITION (L_SHIPDATE)
        SELECT L_ORDERKEY as L_ORDERKEY, L_PARTKEY as L_PARTKEY , 
             L_SUPPKEY as L_SUPPKEY, L_LINENUMBER as L_LINENUMBER,
              L_QUANTITY as L_QUANTITY, L_EXTENDEDPRICE as L_EXTENDEDPRICE,
             L_DISCOUNT as L_DISCOUNT, L_TAX as L_TAX, L_RETURNFLAG as           L_RETURNFLAG, L_LINESTATUS as L_LINESTATUS, L_SHIPDATE as           L_SHIPDATE_PS, L_COMMITDATE as L_COMMITDATE, L_RECEIPTDATE as      L_RECEIPTDATE, L_SHIPINSTRUCT as L_SHIPINSTRUCT, L_SHIPMODE as      L_SHIPMODE, L_COMMENT as L_COMMENT, L_SHIPDATE as L_SHIPDATE FROM lineitem;

Para obtener más información, vea [Tablas con particiones](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+DDL#LanguageManualDDL-PartitionedTables).

## <a name="use-hello-orcfile-format"></a>Usar el formato de ORCFile Hola
Hive admite diferentes formatos de archivo. Por ejemplo:

* **Texto**: este es el formato de archivo predeterminado de Hola y funciona con la mayoría de los escenarios
* **Avro**: funciona bien para escenarios de interoperabilidad
* **ORC/Parquet**: idóneo para el rendimiento

Formato ORC (columnas de fila optimizado) es un toostore de manera muy eficaz datos de Hive. Formatos de tooother comparados, ORC tiene Hola siguientes ventajas:

* compatibilidad con tipos complejos incluidos DateTime y tipos complejos y semiestructurados
* la compresión de % too70
* indiza cada 10 000 filas, lo que permite omitir filas
* un gran descenso en la ejecución del tiempo de ejecución

formato de tooenable ORC, se cree primero una tabla con la cláusula de hello *almacenados como ORC*:

    CREATE TABLE lineitem_orc_part
        (L_ORDERKEY INT, L_PARTKEY INT,L_SUPPKEY INT, L_LINENUMBER INT,
         L_QUANTITY DOUBLE, L_EXTENDEDPRICE DOUBLE, L_DISCOUNT DOUBLE,
         L_TAX DOUBLE, L_RETURNFLAG STRING, L_LINESTATUS STRING,
         L_SHIPDATE_PS STRING, L_COMMITDATE STRING, L_RECEIPTDATE STRING,
         L_SHIPINSTRUCT STRING, L_SHIPMODE STRING, L_COMMENT      STRING)
    PARTITIONED BY(L_SHIPDATE STRING)
    STORED AS ORC;

A continuación, Insertar tabla de datos toohello ORC de hello tabla de ensayo. Por ejemplo:

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

Puede leer más en formato de hello ORC [aquí](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+ORC).

## <a name="vectorization"></a>Vectorización

Permite que la vectorización Hive tooprocess un lote de 1024 filas entre sí en lugar de procesar una fila a la vez. Significa que se realizan operaciones sencillas con mayor rapidez porque menos código interno debe toorun.

la vectorización tooenable prefijo su consulta de Hive con hello después de configuración:

    set hive.vectorized.execution.enabled = true;

Para obtener más información, vea [Ejecución de consultas vectorizadas](https://cwiki.apache.org/confluence/display/Hive/Vectorized+Query+Execution).

## <a name="other-optimization-methods"></a>Otros métodos de optimización
Hay más métodos de optimización que puede considerar, por ejemplo:

* **Creación de depósitos de Hive:** una técnica que permite toocluster o segmento conjuntos grandes de rendimiento de consultas de datos toooptimize.
* **Optimización de la combinación:** optimización del subárbol ejecución de consulta planeación tooimprove Hola eficacia de combinaciones y reducir la necesidad de Hola de sugerencias de usuario. Para obtener más información, vea [Optimización de combinación](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+JoinOptimization#LanguageManualJoinOptimization-JoinOptimization).
* **Aumento de reductores**.

## <a name="next-steps"></a>Pasos siguientes
En este artículo, ha aprendido varios métodos comunes de optimización de consultas de Hive. toolearn más información, vea Hola siguientes artículos:

* [Uso de Apache Hive en HDInsight](hdinsight-use-hive.md)
* [Análisis de datos de retraso de vuelos con Hive en HDInsight](hdinsight-analyze-flight-delay-data.md)
* [Análisis de datos de Twitter con Hive en HDInsight](hdinsight-analyze-twitter-data.md)
* [Analizar datos de sensor mediante Hola consola de consultas de Hive en Hadoop en HDInsight](hdinsight-hive-analyze-sensor-data.md)
* [Usar el subárbol con HDInsight tooanalyze registros de sitios Web](hdinsight-hive-analyze-website-log.md)

[image-hdi-optimize-hive-scaleout_1]: ./media/hdinsight-hadoop-optimize-hive-query/scaleout_1.png
[image-hdi-optimize-hive-scaleout_2]: ./media/hdinsight-hadoop-optimize-hive-query/scaleout_2.png
[image-hdi-optimize-hive-tez_1]: ./media/hdinsight-hadoop-optimize-hive-query/tez_1.png
[image-hdi-optimize-hive-partitioning_1]: ./media/hdinsight-hadoop-optimize-hive-query/partitioning_1.png
