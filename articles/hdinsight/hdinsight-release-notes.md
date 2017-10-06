---
title: notas de la aaaRelease de componentes de Hadoop en HDInsight de Azure | Documentos de Microsoft
description: "Últimas notas de la versión y versiones de los componentes de Hadoop para HDInsight de Azure. Obtenga sugerencias de desarrollo y detalles sobre Spark, R Server, Hive, etc."
services: hdinsight
documentationcenter: 
editor: cgronlun
manager: jhubbard
author: nitinme
tags: azure-portal
ms.assetid: a363e5f6-dd75-476a-87fa-46beb480c1fe
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: nitinme
ms.openlocfilehash: ab08a74380fe0bbd7430c1096dca7eb177c11fe6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="release-notes-for-hadoop-components-on-azure-hdinsight"></a>Notas de la versión de los componentes de Hadoop en HDInsight de Azure

Este artículo proporciona información acerca de hello **más reciente** actualizaciones de versión de HDInsight de Azure. Para más información sobre versiones anteriores, vea [Notas de la versión (en archivo) de los componentes de Hadoop en Azure HDInsight](hdinsight-release-notes-archive.md).

> [!IMPORTANT]
> Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior. Para obtener más información, consulte el [artículo de control de versiones de HDInsight](hdinsight-component-versioning.md).


## <a name="notes-for-08012017-release-of-hdinsight"></a>Notas de la versión del 01/08/2017 de HDInsight

| Título | Descripción | Área afectada  | Tipo de clúster  | 
| --- | --- | --- | --- | --- |
| Lanzamiento de Microsoft R Server 9.1 en HDInsight |HDInsight ahora admite el aprovisionamiento de clústeres de R Server 9.1 en HDInsight. Para más información sobre la versión Microsoft R Server 9.1, vea [este blog](https://blogs.technet.microsoft.com/dataplatforminsider/2017/04/19/introducing-microsoft-r-server-9-1-release/). |Servicio |R Server |
| 3.6 de HDInsight ahora incluye las versiones más recientes de pila de hello Hadoop|<ul><li>Para obtener una lista detallada de las versiones actualizadas, vea [Componentes de Hadoop disponibles con las distintas versiones de HDInsight](hdinsight-component-versioning.md#hadoop-components-available-with-different-hdinsight-versions).</li><li>Para obtener una lista de errores corregidos en versiones más recientes de Hola de pila de Hadoop de hello, consulte [información acerca de la revisión de Apache](https://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.6.1/bk_release-notes/content/patch_parent.html).</li><li>Para obtener una lista de los principales cambios entre HDP 2.6.1 (que ahora está disponible en HDInsight 3.6), vea [https://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.6.1/bk_release-notes/content/behavior_changes.html](https://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.6.1/bk_release-notes/content/behavior_changes.html).</li><li>Para obtener una lista de los problemas conocidos de HDP 2.6.1, vea [Known issues](https://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.6.1/bk_release-notes/content/known_issues.html) (Problemas conocidos).</li></ul> |Servicio |Todo |N/D |
| Las actualizaciones de clústeres de tooInteractive Hive (versión preliminar) |<ul><li><b>Mejora de características.</b> Implementación de la tienda de metadatos almacenados en caché que reduce la carga de hello en hello back-end SQL almacenando en memoria caché los metadatos de Hola y mejora el rendimiento de todas las operaciones de metadatos.  Esta mejora ahora es una opción predeterminada en todas los clústeres de Hive interactivo. Para más información, vea [https://issues.apache.org/jira/browse/HIVE-16520](https://issues.apache.org/jira/browse/HIVE-16520).</li><li><b>Mejora de características.</b> Se optimiza la carga dinámica de partición. Para más información, vea [https://issues.apache.org/jira/browse/HIVE-14204] (https://issues.apache.org/jira/browse/HIVE-14204).</li><li><b>Mejora de características.</b> Optimizaciones de configuración de HDInsight en Linux.</li><li><b>Corrección de errores.</b> `CredentialProviderFactory$getProviders` no es seguro para subprocesos. Este problema está corregido. Para más información, vea [https://issues.apache.org/jira/browse/HADOOP-14195](https://issues.apache.org/jira/browse/HADOOP-14195).</li><li><b>Corrección de errores.</b> Uso elevado de la CPU con la API `liststatus` del controlador de WASB, que resulta en un rendimiento incorrecto de ATS. Este problema está corregido. Para más información, vea [https://github.com/Azure/azure-storage-java/pull/154](https://github.com/Azure/azure-storage-java/pull/154).</li></ul> |Servicio |Interactive Hive (versión preliminar) |
| Clústeres de tooHadoop de actualizaciones |Se mejora la confiabilidad de la operación de trabajo de Templeton. Para más información, vea [https://issues.apache.org/jira/browse/HIVE-15947](https://issues.apache.org/jira/browse/HIVE-15947). |Servicio |Hadoop |
| Actualizaciones de YARN | HDInsight ahora crea una base de datos de Ambari de 250 GB (sin aumentar el costo), que mejora la experiencia de los clientes. Este cambio debe impedir que se llene ATS, para ofrecer la posibilidad de mejorar el rendimiento. |Servicio |Todo |
| Actualizaciones de Spark | Versión de Spark 2.1.1. Para más información, vea [Notas de la versión de Spark 2.1.1](https://spark.apache.org/releases/spark-release-2-1-1.html). | Servicio | Spark |

  



## <a name="04062017---general-availability-of-hdinsight-36"></a>06/04/2017: Disponibilidad general de HDInsight 3.6

* En este lanzamiento, Azure HDInsight presenta la versión 3.6, que se basa en HDP 2.6. Las notas de la versión HDP 2.6 están disponibles [aquí](http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.6.0/bk_release-notes/content/ch_relnotes.html) y se puede encontrar más información sobre las versiones de HDInsight [aquí](hdinsight-component-versioning.md). 3.6 de HDInsight está disponible para hello siguiendo las cargas de trabajo:

    * Hadoop v2.7.3
    * HBase v1.1.2
    * Storm v1.1.0
    * Spark v2.1.0
    * Interactive Hive v2.1.0

* **Compatibilidad con Hive View 2.0**. Esto debe mejorar la experiencia del usuario Hola Hive interactivo. Para más información, vea la [documentación de Hortonworks](http://docs.hortonworks.com/HDPDocuments/Ambari-2.5.0.3/bk_ambari-views/content/ch_using_hive_view.html).

* **Mejoras de rendimiento con Hive LLAP**. Para más información, vea la [documentación de Hortonworks](https://hortonworks.com/blog/top-5-performance-boosters-with-apache-hive-llap/).

* **Nuevas características en Hive**. Vea la [documentación de Hortonworks](https://hortonworks.com/apache/hive/#section_4).

* **Degradación de CLI de Hive**: Hive CLI está en desuso y los clientes están toouse recomienda Beeline en su lugar. Para más información, consulte la [documentación de Apache](https://cwiki.apache.org/confluence/display/Hive/Replacing+the+Implementation+of+Hive+CLI+Using+Beeline). Para obtener instrucciones sobre cómo toouse Beeline con HDInsight, vea [Beeline de uso con Hadoop de HDInsight clústeres](hdinsight-hadoop-use-hive-beeline.md).

* **Nuevas características de Apache Phoenix y HBase**.
    * Compatibilidad de cuota de almacenamiento: se usa habitualmente en entornos multiinquilino, lo que permite un espacio de almacenamiento limitado por tabla y por espacio de nombres.
    * Mejoras de indización de Phoenix: creación de índices incremental y recompilación o reanudación de la indización a partir de errores anteriores.
    * Herramienta de integridad de datos de Phoenix: admite la validación de esquemas, índices y otros metadatos.


* **Problema con HBase**: mientras se ejecuta una masiva CSV cargar el trabajo de MapReduce, Hola según la sintaxis puede dar lugar a un error.

        HADOOP_CLASSPATH=$(hbase mapredcp):/path/to/hbase/conf hadoop jar phoenix-<version>-client.jar org.apache.phoenix.mapreduce.CsvBulkLoadTool --table EXAMPLE --input /data/example.csv

    Usar hello siguiendo la sintaxis en su lugar:

        HADOOP_CLASSPATH=/path/to/hbase-protocol.jar:/path/to/hbase/conf hadoop jar phoenix-<version>-client.jar org.apache.phoenix.mapreduce.CsvBulkLoadTool --table EXAMPLE --input /data/example.csv


## <a name="02282017---release-of-spark-21-on-hdinsight-36-preview"></a>28/02/2017: lanzamiento de Spark 2.1 en HDInsight 3.6 (versión preliminar)
* [2.1 Spark](http://spark.apache.org/releases/spark-release-2-1-0.html) mejora muchos de los problemas de estabilidad y uso que había en las versiones anteriores. También ofrece características nuevas en todas las cargas de trabajo de Spark, como Spark Core, SQL, ML y Streaming.
* Se ha mejorado la escalabilidad del streaming estructurado y se ha agregado compatibilidad con las marcas de agua de horas de evento y el conector Kafka 0.10.
* Ahora se puede controlar la creación de particiones de Spark SQL mediante el nuevo mecanismo de control de particiones escalable. Ver más detalles [aquí](http://spark.apache.org/releases/spark-release-2-1-0.html) acerca de cómo tooupgrade.
* En estos momentos, Spark 2.1 en HDInsight 3.6 (versión preliminar) de Azure no admite la conectividad de herramientas de BI con el controlador ODBC.
* En esta versión preliminar tampoco se puede acceder al almacén de Azure Data Lake Store desde los clústeres de Spark 2.1.


## <a name="11182016---release-of-spark-201-on-hdinsight-35"></a>18/11/2016: lanzamiento de Spark 2.0.1 en HDInsight 3.5
Spark 2.0.1 ahora está disponible en los clústeres Spark (HDInsight versión 3.5).

## <a name="11162016---release-of-r-server-90-on-hdinsight-35-spark-20"></a>16/11/2016 : lanzamiento de R Server 9.0 en HDInsight 3.5 (Spark 2.0)
*   Clústeres de servidores de R incluyen ahora la opción de hello en dos versiones: R Server 9.0 en HDI 3.5 (Spark 2.0) y R Server 8.0 en HDI 3.4 (Spark 1.6).
*   R Server 9.0 en la versión 3.5 de HDI (Spark 2.0) se basa en R 3.3.2 e incluye ScaleR nuevas funciones denominadas RxHiveData y RxParquetData para cargar los datos de Hive de origen de datos y Parquet directamente tooSpark tramas de datos para el análisis por ScaleR. ¿Para obtener más información, consulte en línea hello ayuda sobre estas funciones de R mediante el uso de hello **? ¿RxHiveData** y **? RxParquetData** comandos.
*   Edición de la Comunidad de RStudio Server ya está instalado de forma predeterminada (con una opción de cancelación) en hoja de configuración de clúster de hello como parte de hello aprovisionamiento flujo.

## <a name="11092016---release-of-spark-20-on-hdinsight"></a>09/11/2016: lanzamiento de Spark 2.0 en HDInsight
* Los clústeres de Spark 2.0 en HDInsight 3.5 ahora admiten servicios Livy y Jupyter.

## <a name="10262016---release-of-r-server-on-hdinsight"></a>26/10/2016: lanzamiento de R Server en HDInsight
* Hola URI para el acceso del nodo de borde cambió demasiado**clustername**-ed-ssh.azurehdinsight.net
* Se ha optimizado R Server en el aprovisionamiento de clústeres de HDInsight.
* R Server en HDInsight ahora está disponible como un tipo de clúster R Server regular de HDInsight y ya no se instala como una aplicación independiente de HDInsight. nodo del borde Hello y archivos binarios del servidor de R ahora se suministran como parte de la implementación de clúster de servidor de R Hola. Esto mejora la velocidad y la confiabilidad del aprovisionamiento. El modelo de precios para R Server se actualiza en consecuencia.
* El precio del tipo de clúster de R Server ahora se basa en el precio del nivel estándar más el suplemento de R Server. Ahora el nivel Premium se reserva para las características Premium disponibles en diferentes tipos de clúster y no se usa para el tipo de clúster de R Server. Este cambio no afecta al precio efectivo del servidor de R; cambia solo cómo cargos de Hola se presentan en factura Hola. Todos los clústeres de servidor de R existentes continúan toowork y plantillas de administrador de recursos siguen toofunction hasta que observe la degradación. **Es recomendable el tooupdate la plantilla nueva de administrador de recursos de las implementaciones de secuencias de comandos toouse.**






