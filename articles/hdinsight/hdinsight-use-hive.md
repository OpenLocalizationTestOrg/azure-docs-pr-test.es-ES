---
title: aaaWhat es Apache Hive y HiveQL - HDInsight de Azure | Documentos de Microsoft
description: "Apache Hive es un sistema de almacenamiento de datos para Hadoop. Puede consultar los datos almacenados en el subárbol usando HiveQL, qué similar tooTransact-SQL. En este documento, obtenga información acerca de cómo toouse Hive y HiveQL con HDInsight de Azure."
keywords: "hiveql, ¿qué es hive, hiveql hadoop, cómo toouse hive, obtenga información acerca de hive, ¿qué es el subárbol"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 2c10f989-7636-41bf-b7f7-c4b67ec0814f
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/03/2017
ms.author: larryfr
ms.openlocfilehash: a2772312263895ff99b499898264c2e6d5e816e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-apache-hive-and-hiveql-on-azure-hdinsight"></a>¿Qué son Apache Hive y HiveQL en Azure HDInsight?

[Apache Hive](http://hive.apache.org/) es un sistema de almacenamiento de datos para Hadoop. Hive hace posibles el resumen de los datos, las consultas y el análisis de datos. HiveQL, que es un tooSQL similar de lenguaje de consulta que se escriben consultas de Hive.

Subárbol permite tooproject estructura de datos no estructurados en gran medida. Después de definir la estructura de hello, puede usar datos de saludo de HiveQL tooquery sin conocimiento de Java o MapReduce.

HDInsight proporciona varios tipos de clúster, que están optimizados para cargas de trabajo específicas. Hola siguientes tipos de clúster se suelen usar para consultas de Hive:

* __Subárbol interactivo__: Hadoop de un clúster que proporciona [baja latencia analíticos procesamiento (LLAP)](https://cwiki.apache.org/confluence/display/Hive/LLAP) tiempos de respuesta de tooimprove de funcionalidad para realizar consultas interactivas. Para obtener más información, vea hello [iniciar con interactivo de Hive en HDInsight](hdinsight-hadoop-use-interactive-hive.md) documento.

* __Hadoop__: un clúster de Hadoop que está optimizado para cargas de trabajo de procesamiento por lotes. Para obtener más información, vea hello [iniciar con Hadoop en HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md) documento.

* __Spark__: Apache Spark tiene funcionalidad integrada para trabajar con Hive. Para obtener más información, vea hello [iniciar con Spark en HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md) documento.

* __HBase__: HiveQL puede ser tooquery usa los datos almacenados en HBase. Para obtener más información, vea hello [iniciar con HBase en HDInsight](hdinsight-hbase-tutorial-get-started-linux.md) documento.

## <a name="how-toouse-hive"></a>¿Cómo toouse Hive

Usar hello después toodiscover tabla cómo toouse Hive con HDInsight:

| **Use este método** si desea… | ...un shell **interactivo** | ...procesamiento por**lotes** | ...con este **sistema operativo de clúster** | ...desde este **sistema operativo de cliente** |
|:--- |:---:|:---:|:--- |:--- |
| [Vista de Hive](hdinsight-hadoop-use-hive-ambari-view.md) |✔ |✔ |Linux |Cualquiera (en función del explorador) |
| [Cliente Beeline](hdinsight-hadoop-use-hive-beeline.md) |✔ |✔ |Linux |Linux, Unix, Mac OS X o Windows |
| [API DE REST](hdinsight-hadoop-use-hive-curl.md) |&nbsp; |✔ |Linux o Windows* |Linux, Unix, Mac OS X o Windows |
| [Herramientas de HDInsight para Visual Studio](hdinsight-hadoop-use-hive-visual-studio.md) |&nbsp; |✔ |Linux o Windows* |Windows |
| [Windows PowerShell](hdinsight-hadoop-use-hive-powershell.md) |&nbsp; |✔ |Linux o Windows* |Windows |

> [!IMPORTANT]
> \*Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior. Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).
>
> Si está usando un clúster de HDInsight basados en Windows, puede usar hello [consola de consultas](hdinsight-hadoop-use-hive-query-console.md) desde el explorador o [escritorio remoto](hdinsight-hadoop-use-hive-remote-desktop.md) toorun consultas de Hive.

## <a name="hiveql-language-reference"></a>Referencia del lenguaje HiveQL

Referencia del lenguaje de HiveQL está disponible en hello [manual del lenguaje (https://cwiki.apache.org/confluence/display/Hive/LanguageManual)](https://cwiki.apache.org/confluence/display/Hive/LanguageManual).

## <a name="hive-and-data-structure"></a>Hive y estructura de datos

Subárbol entiende cómo toowork con estructura y datos semiestructurados. Por ejemplo, texto los archivos donde los campos de hello están delimitados por caracteres específicos. Hola sigue HiveQL instrucción crea una tabla con datos delimitados por espacios:

```hiveql
CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
STORED AS TEXTFILE LOCATION '/example/data/';
```

Hive también admite **serializador/deserializadores (SerDe)** personalizados para datos estructurados irregularmente o complejos. Para obtener más información, vea hello [cómo toouse una SerDe de JSON personalizada con HDInsight](http://blogs.msdn.com/b/bigdatasupport/archive/2014/06/18/how-to-use-a-custom-json-serde-with-microsoft-azure-hdinsight.aspx) documento.

Para obtener más información sobre formatos de archivo compatibles con Hive, consulte hello [manual del lenguaje (https://cwiki.apache.org/confluence/display/Hive/LanguageManual)](https://cwiki.apache.org/confluence/display/Hive/LanguageManual)

## <a name="hive-internal-tables-vs-external-tables"></a>Tablas internas frente a tablas externas de Hive.

Hay dos tipos de tablas que puede crear con Hive:

* __Interno__: datos se almacenan en el almacén de datos de Hive Hola. Hello almacenamiento de datos se encuentra en `/hive/warehouse/` en el almacenamiento predeterminado Hola clúster Hola.

    Use tablas internas cuando:

    * Los datos sean temporales.
    * Desea que el ciclo de vida de Hive toomanage Hola de tabla de Hola y de datos.

* __Externo__: los datos se almacenan fuera de almacenamiento de datos de Hola. datos de Hello pueden almacenarse en cualquier almacenamiento accesible por clúster Hola.

    Use tablas externas cuando:

    * datos de Hello también se utilizan fuera de Hive. Por ejemplo, se actualizan los archivos de datos de Hola por otro proceso (que no bloquea los archivos de Hola.)
    * Los datos tienen tooremain Hola subyacente ubicación, incluso después de quitar tabla Hola.
    * Necesite una ubicación personalizada, como una cuenta de almacenamiento no predeterminada.
    * Un programa distinto de hive administra etcetera, la ubicación, el formato de datos de Hola.

Para obtener más información, vea hello [Hive internos y externos preliminar tablas] [ cindygross-hive-tables] entrada de blog.

## <a name="user-defined-functions-udf"></a>Funciones definidas por el usuario (UDF)

Hive también puede extenderse a través de **funciones definidas por el usuario (UDF)**. Una UDF permite la funcionalidad de tooimplement o lógica que no está modelada fácilmente en HiveQL. Para obtener un ejemplo del uso de UDF con Hive, vea Hola siguientes documentos:

* [Utilización de una función definida por el usuario de Java con Hive](hdinsight-hadoop-hive-java-udf.md)

* [Uso de funciones definidas por el usuario (UDF) de Python con Hive y Pig](hdinsight-python.md)

* [Uso de funciones definidas por el usuario de C# con Hive y Pig](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)

* [Cómo funcionan las tooHDInsight tooadd un subárbol personalizado definido por el usuario](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/14/how-to-add-custom-hive-udfs-to-hdinsight.aspx)

* [Marca de tiempo de tooHive da formato a una subárbol ejemplo función definida por el usuario tooconvert fecha y hora](https://github.com/Azure-Samples/hdinsight-java-hive-udf)

## <a id="data"></a>Datos de ejemplo

Hive en HDInsight tiene ya cargada una tabla interna denominada `hivesampletable`. Además, HDInsight proporciona conjuntos de datos de ejemplo que se pueden usar con Hive. Estos conjuntos de datos se almacenan en hello `/example/data` y `/HdiSamples` directorios. Estos directorios existen en el almacenamiento predeterminado de hello para el clúster.

## <a id="job"></a>Ejemplo de consulta de Hive

Hola después de las columnas del proyecto de instrucciones de HiveQL en hello `/example/data/sample.log` archivo:

    set hive.execution.engine=tez;
    DROP TABLE log4jLogs;
    CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
    STORED AS TEXTFILE LOCATION '/example/data/';
    SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

En el ejemplo anterior de hello, instrucciones de HiveQL Hola realizan Hola siguientes acciones:

* `set hive.execution.engine=tez;`: Conjuntos Hola toouse de motor de ejecución Tez. Si se utiliza Tez en lugar de MapReduce, se puede mejorar el rendimiento de las consultas. Para obtener más información sobre Tez, vea hello [Tez de Apache de uso para mejorar el rendimiento](#usetez) sección.

    > [!NOTE]
    > Esta instrucción solo se requiere cuando se usa un clúster de HDInsight basado en Windows. Tez es el motor de ejecución predeterminado de Hola de HDInsight basados en Linux.

* `DROP TABLE`: Si ya existe una tabla de hello, elimínelo.

* `CREATE EXTERNAL TABLE`: crea una tabla **externa** en Hive. Tablas externas solo almacenan definición de la tabla de hello en el subárbol. Hola datos permanecen en la ubicación original de Hola y en formato original Hola.

* `ROW FORMAT`: Indica cómo se da formato a los datos de Hola de Hive. En este caso, los campos de hello en cada registro están separados por un espacio.

* `STORED AS TEXTFILE LOCATION`: Indica Hive donde hello se almacenan los datos (hello `example/data` directorio) y que se almacena como texto. datos Hola pueden estar en un archivo o distribuir en varios archivos en el directorio de Hola.

* `SELECT`: Selecciona un recuento de todas las filas donde hello columna **t4** contiene el valor de hello **[ERROR]**. Esta instrucción devuelve un valor de **3** porque hay tres filas que contienen este valor.

* `INPUT__FILE__NAME LIKE '%.log'`-Subárbol intenta tooapply Hola esquema tooall archivos hello del directorio. En este caso, el directorio de hello contiene archivos que no coinciden con el esquema de Hola. tooprevent los datos de elementos no utilizados en los resultados de hello, esta instrucción indica Hive que solo debemos devolver datos de archivos que finalizan con. registro.

> [!NOTE]
> Tablas externas deben utilizarse cuando se espera Hola subyacente datos toobe actualizado a través de un origen externo. Por ejemplo, un proceso de carga de datos automatizado o una operación de MapReduce.
>
> Quitar una tabla externa **no** eliminar datos de hello, sólo elimina la definición de la tabla de Hola.

toocreate una **interno** tablas en lugar de externas, utilice Hola después de HiveQL:

    set hive.execution.engine=tez;
    CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    STORED AS ORC;
    INSERT OVERWRITE TABLE errorLogs
    SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]';

Estas instrucciones realizan Hola siguientes acciones:

* `CREATE TABLE IF NOT EXISTS`: Si la tabla hello no existe, créela. Dado que hello **externo** no se utiliza la palabra clave, esta instrucción crea una tabla interna. tabla de Hola se almacena en el almacén de datos de Hive de Hola y se administra completamente por el subárbol.

* `STORED AS ORC`: Almacena los datos de hello en formato de fila de optimizado columnas (ORC). ORC es un formato altamente optimizado y eficiente para almacenar datos de Hive.

* `INSERT OVERWRITE ... SELECT`: Selecciona las filas de hello **log4jLogs** tabla que contiene **[ERROR]**, y, a continuación, inserta Hola datos en hello **registros de errores de** tabla.

> [!NOTE]
> A diferencia de las tablas externas, quitar una tabla interna también elimina los datos subyacentes de Hola.

## <a name="improve-hive-query-performance"></a>Mejora del rendimiento de las consultas de Hive

### <a id="usetez"></a>Apache Tez

[Apache Tez](http://tez.apache.org) es un marco que permite a las aplicaciones de uso intensivo de datos, como Hive, toorun mucho más eficazmente a escala. Tez está habilitado de manera predeterminada para los clústeres de HDInsight basados en Linux.

> [!NOTE]
> Tez actualmente está desactivado de forma predeterminada para clústeres de HDInsight basados en Windows y debe estar habilitado. tootake aprovechar Tez, Hola siguiente valor se debe establecer para una consulta de Hive:
>
> `set hive.execution.engine=tez;`
>
> Tez es motor predeterminado de Hola para clústeres de HDInsight basados en Linux.

Hola [Hive en documentos de diseño de Tez](https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez) contiene detalles sobre las opciones de implementación de Hola y las configuraciones de optimización.

tooaid en la depuración de trabajos se ejecutó con Tez, HDInsight proporciona Hola siguientes interfaces de usuario web que le permiten tooview detalles de los trabajos de Tez:

* [Usar hello vista Ambari Tez en HDInsight basados en Linux](hdinsight-debug-ambari-tez-view.md)

* [Usar hello Tez UI en HDInsight basados en Windows](hdinsight-debug-tez-ui.md)

### <a name="low-latency-analytical-processing-llap"></a>Procesamiento analítico de baja latencia (LLAP)

[LLAP](https://cwiki.apache.org/confluence/display/Hive/LLAP) (conocido a veces como Larga vida y procesamiento) es una característica nueva de Hive 2.0 que permite el almacenamiento en memoria caché de las consultas. LLAP hace mucho más rápido, seguridad de consultas de Hive demasiado[x 26 más rápidamente de Hive 1.x en algunos casos](https://hortonworks.com/blog/announcing-apache-hive-2-1-25x-faster-queries-much/).

HDInsight proporciona LLAP Hola Hive interactivo tipo de clúster. Para obtener más información, vea hello [iniciar con Hive interactivo](hdinsight-hadoop-use-interactive-hive.md) documento.

## <a name="hive-jobs-and-sql-server-integration-services"></a>Trabajos de Hive y servicios de integración de SQL Server

Puede utilizar SQL Server Integration Services (SSIS) toorun un trabajo de Hive. Hola Feature Pack de Azure para SSIS proporciona Hola trabajan con trabajos de Hive en HDInsight de los componentes siguientes.

* [Tarea de Hive de Azure HDInsight][hivetask]

* [Administrador de conexiones de suscripción de Azure][connectionmanager]

Obtener más información sobre Hola Feature Pack de Azure para SSIS [aquí][ssispack].

## <a id="nextsteps"></a>Pasos siguientes

Ahora que ha aprendido Novedades de Hive y cómo toouse con Hadoop en HDInsight, Hola de uso siguiente vincula tooexplore otro toowork maneras con HDInsight de Azure.

* [Cargar datos tooHDInsight][hdinsight-upload-data]
* [Uso de Pig con HDInsight][hdinsight-use-pig]
* [Uso de trabajos de MapReduce con HDInsight][hdinsight-use-mapreduce]

[hdinsight-sdk-documentation]: http://msdnstage.redmond.corp.microsoft.com/library/dn479185.aspx

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[apache-tez]: http://tez.apache.org
[apache-hive]: http://hive.apache.org/
[apache-log4j]: http://en.wikipedia.org/wiki/Log4j
[hive-on-tez-wiki]: https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez
[import-to-excel]: http://azure.microsoft.com/documentation/articles/hdinsight-connect-excel-power-query/
[hivetask]: http://msdn.microsoft.com/library/mt146771(v=sql.120).aspx
[connectionmanager]: http://msdn.microsoft.com/library/mt146773(v=sql.120).aspx
[ssispack]: http://msdn.microsoft.com/library/mt146770(v=sql.120).aspx

[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md


[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md

[Powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx


[cindygross-hive-tables]: http://blogs.msdn.com/b/cindygross/archive/2013/02/06/hdinsight-hive-internal-and-external-tables-intro.aspx
