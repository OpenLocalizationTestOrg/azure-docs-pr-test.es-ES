---
title: "¿aaaWhat son HDInsight, pila de tecnología de Hadoop de hello & clústeres? -Azure | Microsoft Docs"
description: "Una pila de tecnología Introducción hello y tooHDInsight Hadoop y los componentes, como Spark, Kafka, Hive, HBase para el análisis de grandes cantidades de datos."
keywords: "hadoop Azure, azure hadoop, introducción de hadoop, introducción de hadoop, pila de tecnología de hadoop, toohadoop preliminar, toohadoop introducción, ¿qué es un clúster de hadoop, ¿qué es el clúster de hadoop, lo que sirve hadoop para"
services: hdinsight
documentationcenter: 
author: cjgronlund
manager: jhubbard
editor: cgronlun
ms.assetid: e56a396a-1b39-43e0-b543-f2dee5b8dd3a
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/20/2017
ms.author: cgronlun
ms.openlocfilehash: 0aed3d1a6cf3c0cdc3b036cfa4865a2e0b58e2c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-hdinsight-hello-hadoop-technology-stack-and-hadoop-clusters"></a>Introducción tooAzure HDInsight, pila de tecnología de Hadoop de Hola y clústeres de Hadoop
 Este artículo proporciona una tooAzure Introducción HDInsight, una distribución de nube de pila de tecnología de Hadoop de Hola. También explica qué es un clúster de Hadoop y cuándo se utilizaría. 

## <a name="what-is-hdinsight-and-hello-hadoop-technology-stack"></a>¿Qué es hello pila de tecnología de Hadoop y HDInsight? 
HDInsight de Azure es una distribución de nube de componentes de Hadoop de Hola de hello [Hortonworks Data Platform (HDP)](https://hortonworks.com/products/data-center/hdp/). [Apache Hadoop](http://hadoop.apache.org/) era el marco de código abierto original de hello para el procesamiento distribuido y el análisis de grandes conjuntos de datos en clústeres de equipos. 


pila de tecnología de Hadoop de Hello incluye software relacionado y utilidades, incluidas Apache Hive, HBase, Spark, Kafka y muchas otras. toosee Hadoop tecnología pila componentes disponibles en HDInsight, vea [componentes y las versiones disponibles con HDInsight][component-versioning]. tooread más información acerca de Hadoop en HDInsight, vea hello [página de características de Azure para HDInsight](https://azure.microsoft.com/services/hdinsight/).

## <a name="what-is-a-hadoop-cluster-and-when-do-you-use-it"></a>¿Qué es un clúster de Hadoop y cuándo se utiliza?
*Hadoop* también es un tipo de clúster que dispone de:

* YARN para programación de trabajos y administración de recursos
* MapReduce para procesamiento en paralelo
* Hola de sistema de archivos distribuido de Hadoop (HDFS)
  
Los clústeres de Hadoop se suelen usar para el procesamiento por lotes de datos almacenados. Otros tipos de clústeres de HDInsight tienen funcionalidades adicionales: Spark ha crecido en popularidad debido a su procesamiento más rápido y en memoria. Consulte [Tipos de clúster de HDInsight](#overview) para más información.

## <a name="what-is-big-data"></a>¿Qué son grandes volúmenes de datos?
Por macrodatos se entiende cualquier volumen grande de información digital, tales como:

* Datos de sensores de equipos industriales
* Actividad de los clientes recopilada en un sitio web
* Una fuente de noticias de Twitter

Los macrodatos se recopilan en volúmenes de escala, a mayores velocidades y para una variedad mayor de formatos. Puede ser histórico (es decir, almacenados) o en tiempo real (es decir, transmite por secuencias desde el origen de hello). 

## <a name="overview"></a>Tipos de clúster de HDInsight
HDInsight incluye tipos de clúster concretos y funcionalidades de personalización del clúster, tales como agregar componentes, utilidades y lenguajes.

### <a name="spark-kafka-interactive-hive-hbase-customized-and-other-cluster-types"></a>Spark, Kafka, Interactive Hive, HBase, personalizado y otros tipos de clúster
HDInsight ofrece Hola siguientes tipos de clúster:

* **[Apache Hadoop](https://wiki.apache.org/hadoop)**: usa [HDFS](#hdfs), [YARN](#yarn) administración de recursos y una sencilla [MapReduce](#mapreduce) tooprocess de modelo de programación y analizar los datos por lotes en paralelo.
* **[Apache Spark](http://spark.apache.org/)**: un marco de trabajo de procesamiento en paralelo que admite el procesamiento en memoria tooboost Hola rendimiento de aplicaciones de análisis de grandes cantidades de datos, inspirará works para SQL, la transmisión de datos y aprendizaje automático. Consulte [¿qué es Apache Spark en HDInsight?](hdinsight-apache-spark-overview.md)
* **[Apache HBase](http://hbase.apache.org/)**: base de datos NoSQL en Hadoop que proporciona acceso aleatorio y gran coherencia para grandes cantidades de datos no estructurados y semiestructurados; potencialmente miles de millones de filas multiplicadas por millones de columnas. Consulte [¿qué es HBase en HDInsight?](hdinsight-hbase-overview.md)
* **[Microsoft R Server](https://msdn.microsoft.com/microsoft-r/rserver)**: un servidor para hospedar y administrar procesos de R distribuidos en paralelo. Proporciona los científicos de datos y estadistas, los programadores de R con acceso a petición tooscalable, distribuidas métodos de análisis en HDInsight. [Información general de R Server en HDInsight](hdinsight-hadoop-r-server-overview.md).
* **[Apache Storm](https://storm.incubator.apache.org/)**: sistema distribuido de cálculo en tiempo real para el procesamiento rápido de grandes transmisiones de datos. Storm se ofrece como clúster administrado en HDInsight. Consulte [Análisis de datos de sensor en tiempo real con Storm y Hadoop](hdinsight-storm-sensor-data-analysis.md).
* **[Versión preliminar de Apache Interactive Hive (también conocido como Live Long and Process)](https://cwiki.apache.org/confluence/display/Hive/LLAP)**: almacenamiento en caché en memoria para consultas de Hive interactivas y más rápidas. Consulte [Uso de Interactive Hive en HDInsight](hdinsight-hadoop-use-interactive-hive.md).
* **[Apache Kafka](https://kafka.apache.org/)**: una plataforma de código abierto usada para crear canalizaciones y aplicaciones de datos de streaming. Kafka también proporciona la funcionalidad de cola de mensajes que le permite toopublish y suscribirse toodata secuencias. Vea [Introducción tooApache Kafka en HDInsight](hdinsight-apache-kafka-introduction.md).

También puede configurar clústeres usando Hola siguientes métodos:
* **[Vista previa de clústeres Unidos al dominio](hdinsight-domain-joined-introduction.md)**: un clúster Unidos a un dominio de Active Directory tooan para que pueda controlar el acceso y proporcionar el control de los datos.
* **[Clústeres personalizados con acciones de script](hdinsight-hadoop-customize-cluster-linux.md)**: clústeres con scripts que se ejecutan durante el aprovisionamiento y que instalan componentes.

### <a name="example-cluster-customization-scripts"></a>Scripts de personalización de clúster de ejemplo
Las acciones de script son scripts de Bash en Linux que se ejecutan durante el aprovisionamiento de clústeres y que pueden ser utilizados tooinstall componentes adicionales en el clúster de Hola. 

Hello se proporcionan secuencias de comandos de ejemplo siguientes que el equipo de Hola HDInsight:

* **[Matiz](hdinsight-hadoop-hue-linux.md)**: un conjunto de web toointeract de aplicaciones que se usan con un clúster. Solo clústeres Linux.
* **[Giraph](hdinsight-hadoop-giraph-install-linux.md)**: gráfico de procesamiento toomodel relaciones entre elementos o para usuarios.
* **[Solr](hdinsight-hadoop-solr-install-linux.md)**: plataforma de búsqueda de escala empresarial que permite la búsqueda de texto completo en los datos.

Para obtener información sobre el desarrollo de sus propias acciones de script, consulte [Desarrollo de la acción de script con HDInsight](hdinsight-hadoop-script-actions-linux.md).

## <a name="components-and-utilities-on-hdinsight-clusters"></a>Componentes y utilidades en clústeres de HDInsight
Hello componentes y las utilidades siguientes se incluyen en clústeres de HDInsight:

* **[Ambari](#ambari)**: aprovisionamiento, administración, supervisión y utilidades de clústeres.
* **[Avro](#avro)**  (biblioteca de Microsoft .NET para Avro): la serialización de datos para el entorno de Microsoft .NET Hola. 
* **[Hive y HCatalog](#hive)**: consultas tipo SQL y una capa de administración de almacenamiento y de tablas.
* **[Mahout](#mahout)**: para aplicaciones de aprendizaje automático escalables.
* **[MapReduce](#mapreduce)**: marco heredado para el procesamiento distribuido y la administración de recursos de Hadoop. Consulte [YARN](#yarn).
* **[Oozie](#oozie)**: administración de flujo de trabajo.
* **[Phoenix](#phoenix)**: capa de base de datos relacional sobre HBase.
* **[Pig](#pig)**: scripts más sencillos para transformaciones de MapReduce.
* **[Sqoop](#sqoop)**: importación y exportación de datos.
* **[Tez](#tez)**: permite toorun de procesos de uso intensivo de datos eficazmente a escala.
* **[YARN](#yarn)**: administración de recursos que forma parte de la biblioteca principal de hello Hadoop.
* **[ZooKeeper](#zookeeper)**: coordinación de procesos en sistemas distribuidos.

> [!NOTE]
> Para obtener información acerca de los componentes específicos de hello e información de versión, consulte [Hadoop componentes y las versiones en HDInsight][component-versioning]
>
>

### <a name="ambari"></a>Ambari
Apache Ambari se utiliza para aprovisionar, administrar y supervisar clústeres de Apache Hadoop. Incluye una colección de herramientas de operador intuitiva y un potente conjunto de API que reducen la complejidad de Hola de Hadoop, simplificar la operación de Hola de clústeres. Clústeres de HDInsight en Linux proporcionan Hola Ambari web UI tanto Hola API de REST de Ambari. Las Vistas de Ambari en clústeres de HDInsight admiten funcionalidades de IU de complementos.
Consulte [Administración de clústeres de HDInsight con Ambari](hdinsight-hadoop-manage-ambari.md) y <a target="_blank" href="https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md">Referencia de la API de Apache Ambari</a>.

### <a name="avro"></a>Avro (biblioteca de Microsoft .NET para Avro)
Hola biblioteca .NET de Microsoft para Avro implementa Hola Apache Avro el formato de intercambio de datos binarios compact para la serialización para el entorno de Microsoft .NET Hola. Define un esquema independiente del idioma para que los datos serializados en un idioma puedan leerse en otro. Encontrará información detallada en formato de Hola Hola < un destino = _ "blank" href = "http://avro.apache.org/docs/current/spec.html" > especificación de Apache Avro</a>. formato de Hola Hola de Avro archivos admite distribuidas MapReduce modelo de programación: archivos son "divisibles", lo que significa que puede buscar cualquier punto en un archivo y empezar a leer desde un bloque específico. toofind más información sobre cómo, consulte [serializar los datos con hello biblioteca de Microsoft .NET para Avro](hdinsight-dotnet-avro-serialization.md). Toocome de soporte técnico de clúster basado en Linux.

### <a name="hdfs"></a>HDFS
Sistema de archivos distribuido de Hadoop (HDFS) es un sistema de archivos que, con YARN y MapReduce, es el núcleo de Hola de tecnología de Hadoop. 'S sistema de archivos estándar de Hola para clústeres de Hadoop en HDInsight. Consulte [Consultar datos de un almacenamiento compatible con HDFS](hdinsight-hadoop-use-blob-storage.md).

### <a name="hive"></a>Hive y HCatalog
<a target="_blank" href="http://hive.apache.org/">Apache Hive</a> es software integrado en Hadoop que le permite tooquery del almacenamiento de datos y administración grandes conjuntos de datos de almacenamiento distribuido mediante un lenguaje parecido a SQL denominado HiveQL. Hive, como Pig, es una abstracción por encima de MapReduce y convierte las consultas en una serie de trabajos de MapReduce. Subárbol es más cerca de sistema de administración de base de datos relacional de tooa de Pig y se utiliza con los datos más estructurados. Para los datos no estructurados, Pig es Hola mejor opción. Consulte el artículo sobre el [uso de Hive con Hadoop en HDInsight](hdinsight-use-hive.md).

<a target="_blank" href="https://cwiki.apache.org/confluence/display/Hive/HCatalog/">Apache HCatalog</a> es una capa de administración de almacenamiento y tablas para Hadoop que presenta una vista relacional de los datos. En HCatalog, se pueden leer y escribir archivos en cualquier formato que sirva para un SerDe (serializador-deserializador) de Hive.

### <a name="mahout"></a>Mahout
<a target="_blank" href="https://mahout.apache.org/">Apache Mahout</a> es una biblioteca de algoritmos de aprendizaje automático que se ejecuta en Hadoop. Con los principios de estadísticas, las aplicaciones de aprendizaje de máquina enseñan toolearn de sistemas de datos y toouse más allá de su comportamiento futuro toodetermine resultados. Consulte [Generación de recomendaciones de películas mediante Mahout en Hadoop](hdinsight-mahout.md).

### <a name="mapreduce"></a>MapReduce
MapReduce es el marco de software heredado de Hola para Hadoop para escribir aplicaciones de proceso de toobatch grandes conjuntos de datos en paralelo. Un trabajo de MapReduce divide grandes conjuntos de datos y organiza los datos de hello en pares de clave y valor para su procesamiento. Los trabajos de MapReduce se ejecutan en [YARN](#yarn). Vea <a target="_blank" href="http://wiki.apache.org/hadoop/MapReduce">MapReduce</a> Hola Hadoop Wiki.

### <a name="oozie"></a>Oozie
<a target="_blank" href="http://oozie.apache.org/">Apache Oozie</a> es un sistema de coordinación de flujos de trabajo que administra trabajos de Hadoop. Se integra con la pila de Hadoop de Hola y es compatible con trabajos de Hadoop MapReduce, Pig, Hive y Sqoop. También puede ser usado tooschedule trabajos tooa específico sistema, como programas Java o secuencias de comandos de shell. Consulte [Uso de Oozie con Hadoop para definir y ejecutar un flujo de trabajo en HDInsight](hdinsight-use-oozie-linux-mac.md).

### <a name="phoenix"></a>Phoenix
<a  target="_blank" href="http://phoenix.apache.org/">Apache Phoenix</a> es una capa de base de datos relacional sobre HBase. Phoenix incluye un controlador JDBC que le permite tooquery y administra directamente las tablas SQL. Phoenix traduce consultas y otras instrucciones en llamadas nativas de la API NoSQL nativas en lugar de usar MapReduce, lo que permite aplicaciones más rápidas además de los almacenes NoSQL. Consulte [Usar Apache Phoenix y SQuirreL con clústeres de HBase](hdinsight-hbase-phoenix-squirrel.md).

### <a name="pig"></a>Pig
<a  target="_blank" href="http://pig.apache.org/">Apache Pig</a> es una plataforma de alto nivel que permite las transformaciones complejas de MapReduce tooperform en grandes conjuntos de datos mediante el uso de un lenguaje de scripting simple denominado Pig latino. Pig traduce scripts de Pig latino hello, por lo que va a ejecutar en Hadoop. Puede crear funciones definidas por el usuario (UDF) tooextend Pig latino. Consulte [Uso de Pig con Hadoop en HDInsight](hdinsight-use-pig.md).

### <a name="sqoop"></a>Sqoop
<a  target="_blank" href="http://sqoop.apache.org/">Apache Sqoop</a> es una herramienta que transfiere grandes cantidades de datos entre Hadoop y bases de datos relacionales, como SQL, u otros almacenes de datos estructurados, de la manera más eficiente posible. Consulte [Uso de Sqoop con Hadoop](hdinsight-use-sqoop.md).

### <a name="tez"></a>Tez
<a  target="_blank" href="http://tez.apache.org/">Apache Tez</a> es un marco de aplicación basado en Hadoop YARN que ejecuta gráficos complejos y acíclicos general de procesamiento de datos generales. Es más flexible y eficaz sucesor toohello MapReduce marco que permite procesos de uso intensivo de datos, como Hive, toorun más eficazmente a escala. Consulte ["Usar Apache Tez para un rendimiento mejorado" en Usar Hive y HiveQL](hdinsight-use-hive.md#usetez).

### <a name="yarn"></a>YARN
Apache YARN es hello de siguiente generación de MapReduce (MapReduce 2.0 o MRv2) y es compatible con escenarios de procesamiento de datos más allá de MapReduce procesamiento por lotes con mayor escalabilidad y el procesamiento en tiempo real. YARN proporciona un marco de aplicación distribuida y administración de recursos. Los trabajos de MapReduce se ejecutan en YARN. Consulte <a target="_blank" href="http://hadoop.apache.org/docs/current/hadoop-yarn/hadoop-yarn-site/YARN.html">Apache Hadoop NextGen MapReduce (YARN)</a>.

### <a name="zookeeper"></a>ZooKeeper
<a  target="_blank" href="http://zookeeper.apache.org/">Apache ZooKeeper</a> coordina procesos en grandes sistemas distribuidos por medio de un espacio de nombres jerárquico compartido de registros de datos (znodes). Znodes contener pequeñas cantidades de metadatos información necesaria toocoordinate procesos: estado, ubicación, configuración y así sucesivamente. Ver un ejemplo de [ZooKeeper con un clúster de HBase y Apache Phoenix](hdinsight-hbase-phoenix-squirrel-linux.md). 

## <a name="programming-languages-on-hdinsight"></a>Lenguajes de programación en HDInsight
Los clústeres de HDInsight, como Spark, HBase, Kafka, Hadoop y otros clústeres, admiten varios lenguajes de programación, aunque algunos no están instalados de manera predeterminada. Para las bibliotecas, módulos o paquetes no instalados de forma predeterminada, [utilizar un componente de script acción tooinstall hello](hdinsight-hadoop-script-actions-linux.md). 

### <a name="default-programming-language-support"></a>Compatibilidad con lenguajes de programación predeterminados
De forma predeterminada, los clústeres de HDInsight admiten lo siguiente:

* Java
* Python

Se pueden instalar lenguajes adicionales mediante [acciones de script](hdinsight-hadoop-script-actions-linux.md).

### <a name="java-virtual-machine-jvm-languages"></a>Lenguajes de la máquina virtual de Java (JVM)
Muchos lenguajes que no sean Java pueden ejecutar en una máquina virtual de Java (JVM); Sin embargo, con algunos de estos idiomas puede requerir componentes adicionales instalados en el clúster de Hola.

Estos lenguajes basados en JVM son compatibles con clústeres de HDInsight:

* Clojure
* Jython (Python para Java)
* Scala

### <a name="hadoop-specific-languages"></a>Lenguajes específicos de Hadoop
Clústeres de HDInsight admiten Hola siguiendo los idiomas que están pila de tecnología de Hadoop de toohello específica:

* Pig Latin para trabajos de Pig
* HiveQL para trabajos de Hive y SparkSQL

## <a name="hdinsight-standard-and-hdinsight-premium"></a>HDInsight Standard y HDInsight Premium
HDInsight proporciona ofertas en la nube de macrodatos en dos categorías, Estándar y Premium. HDInsight estándar proporciona un clúster de escala empresarial que las organizaciones pueden usar toorun sus cargas de trabajo grandes cantidades de datos. HDInsight Premium va más allá de las funcionalidades estándar y proporciona funcionalidades avanzadas de análisis y seguridad para un clúster de HDInsight. Para más información, consulte [Novedades en las versiones de clústeres de Hadoop proporcionadas por HDInsight](hdinsight-component-versioning.md#hdinsight-standard-and-hdinsight-premium)

## <a name="microsoft-business-intelligence-and-hdinsight"></a>Microsoft Business Intelligence y HDInsight
Herramientas familiares de business intelligence (BI) recuperar, analizar y notificar datos integrados con HDInsight utilizando cualquier Hola complemento Power Query u Hola Microsoft Hive ODBC Driver:

* [Conectar Excel tooHadoop con Power Query](hdinsight-connect-excel-power-query.md): Obtenga información acerca de cómo Hola tooconnect Excel toohello cuenta de almacenamiento de Azure que almacena los datos de su clúster de HDInsight mediante Microsoft Power Query para Excel. Se requiere una estación de trabajo de Windows. 
* [Conectar Excel tooHadoop con hello Microsoft Hive ODBC Driver](hdinsight-connect-excel-hive-odbc-driver.md): Obtenga información acerca de cómo tooimport datos de HDInsight con Hola Microsoft Hive ODBC Driver. Se requiere una estación de trabajo de Windows. 
* [Plataforma de nube de Microsoft](http://www.microsoft.com/server-cloud/solutions/business-intelligence/default.aspx): Obtenga información acerca de Power BI para Office 365, descargue la versión de prueba de SQL Server de Hola y configurar SharePoint Server 2013 y SQL Server BI.
* [SQL Server Analysis Services](http://msdn.microsoft.com/library/hh231701.aspx)
* [SQL Server Reporting Services](http://msdn.microsoft.com/library/ms159106.aspx)


## <a name="next-steps"></a>Pasos siguientes

* [Introducción a Hadoop en HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md): un tutorial de inicio rápido sobre el aprovisionamiento de clústeres de Hadoop para HDInsight y la ejecución de consultas de ejemplo de Hive.
* [Introducción a Spark en HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md): un tutorial de inicio rápido para crear un clúster Spark y ejecutar consultas Spark SQL interactivas.
* [Introducción al uso de R Server en HDInsight (versión preliminar)](hdinsight-hadoop-r-server-get-started.md): empiece a utilizar R Server en HDInsight Premium.
* [Aprovisionar clústeres de HDInsight](hdinsight-hadoop-provision-linux-clusters.md): Obtenga información acerca de cómo tooprovision un Hadoop de HDInsight de clúster a través de Hola portal de Azure, Azure CLI o PowerShell de Azure.


[component-versioning]: hdinsight-component-versioning.md
[zookeeper]: http://zookeeper.apache.org/