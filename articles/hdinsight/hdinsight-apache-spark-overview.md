---
title: aaaIntroduction tooSpark en HDInsight de Azure | Documentos de Microsoft
description: "Este artículo proporciona una introducción tooSpark en hello y HDInsight diferentes escenarios en los que puede usar clúster de Spark en HDInsight."
keywords: "¿Qué es spark apache, clúster de spark, toospark de introducción, spark en hdinsight"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 82334b9e-4629-4005-8147-19f875c8774e
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/12/2017
ms.author: nitinme
ms.openlocfilehash: 41996e733618b8534469fa239b980ac50161a535
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toospark-on-hdinsight"></a>Introducción tooSpark en HDInsight

Este artículo proporcionan con una tooSpark de introducción en HDInsight. <a href="http://spark.apache.org/" target="_blank">Apache Spark</a> es un marco de trabajo de procesamiento paralelo de código abierto que admite en memoria tooboost Hola rendimiento de aplicaciones analíticas de grandes cantidades de datos del procesamiento. Un clúster de Spark en HDInsight es compatible con Azure Storage (WASB), así como con Azure Data Lake Store, por lo que los datos existentes almacenados en Azure pueden procesarse fácilmente por medio de un clúster de Spark.

Cuando crea un clúster de Spark en HDInsight, aprovisiona recursos de proceso de Azure con Spark instalado y configurado. Solo toma cada diez minutos aproximadamente clúster toocreate un Spark en HDInsight. Hola toobe de datos procesado se almacena en el almacenamiento de Azure o almacén de Azure Data Lake. Consulte [Uso de Azure Storage con HDInsight](hdinsight-hadoop-use-blob-storage.md).

**clúster de toocreate un Spark en HDInsight**, consulte [inicio rápido: crear un clúster de Spark en HDInsight y ejecutar consultas interactivo mediante Jupyter](hdinsight-apache-spark-jupyter-spark-sql.md).


## <a name="what-is-apache-spark-on-azure-hdinsight"></a>¿Qué es Apache Spark en Azure HDInsight?
Los clústeres de Spark en HDInsight ofrecen un servicio de Spark completamente administrado. Aquí se enumeran las ventajas de crear un clúster de Spark en HDInsight.

| Característica | Descripción |
| --- | --- |
| Facilidad de creación de clústeres de Spark |Puede crear un nuevo clúster de Spark en HDInsight en minutos usando Hola Portal de Azure, Azure PowerShell o hello HDInsight .NET SDK. Consulte [Introducción al clúster de Spark en HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md) |
| Facilidad de uso |El clúster de Spark en HDInsight incluye notebooks de Jupyter y Zeppelin. Puede usarlos para el procesamiento y la visualización de datos interactivos.|
| API de REST |Los clústeres de Spark en HDInsight incluyen [Livio](https://github.com/cloudera/hue/tree/master/apps/spark/java#welcome-to-livy-the-rest-spark-server), un basadas en la API de REST Spark trabajo tooremotely monitor y enviar trabajos de servidor. |
| Compatibilidad con Almacén de Azure Data Lake | Clúster de Spark en HDInsight puede ser configurado toouse almacén de Azure Data Lake como un almacenamiento adicional, así como almacenamiento principal (sólo con clústeres de HDInsight 3.5). Para más información acerca del Almacén de Data Lake, consulte la página con [información general del Almacén de Azure Data Lake](../data-lake-store/data-lake-store-overview.md). |
| Integración con servicios de Azure |Clúster de Spark en HDInsight incluye un tooAzure conector centros de eventos. Los clientes pueden crear aplicaciones de streaming con concentradores de eventos de hello, además demasiado[Kafka](http://kafka.apache.org/), que ya está disponible como parte de Spark. |
| Compatibilidad con R Server | Puede configurar un servidor de R en HDInsight Spark clúster toorun distribuye cálculos de R con velocidades de hello prometidos con un clúster de Spark. Para obtener más información, consulte [Get started using R Server on HDInsight](hdinsight-hadoop-r-server-get-started.md)(Introducción a R Server en HDInsight). |
| Integración con IDE de terceros | HDInsight proporciona complementos para IDE como IntelliJ IDEA y Eclipse, que puede usar toocreate y enviar aplicaciones tooan clúster de HDInsight Spark. Para más información, consulte [Uso del kit de herramientas de Azure para IDEA IntelliJ](hdinsight-apache-spark-intellij-tool-plugin.md) y [Uso del kit de herramientas de Azure para Eclipse](hdinsight-apache-spark-eclipse-tool-plugin.md).|
| Consultas simultáneas |Los clústeres de Spark en HDInsight admiten consultas simultáneas. Esto permite que varias consultas de usuario de una o varias consultas de distintos usuarios y aplicaciones tooshare Hola mismos recursos de clúster. |
| Almacenamiento en caché en SSD |Puede elegir toocache datos en memoria o en SSD adjunta toohello nodos del clúster. Almacenamiento en caché en memoria proporciona mejor rendimiento de consultas Hola pero también podría ser costoso; almacenamiento en caché en SSD proporciona una buena opción para mejorar el rendimiento de las consultas sin necesidad de hello toocreate un clúster de un tamaño que sea necesario toofit Hola todo conjunto de datos en memoria. |
| Integración con herramientas de BI |Los clústeres de Spark en HDInsight ofrecen conectores para herramientas de BI como [Power BI](http://www.powerbi.com/) y [Tableau](http://www.tableau.com/products/desktop) para el análisis de datos. |
| Bibliotecas de Anaconda precargadas |Los clústeres Spark en HDInsight incluyen bibliotecas de Anaconda preinstaladas. [Anaconda](http://docs.continuum.io/anaconda/) proporciona bibliotecas de cierre too200 para el aprendizaje automático, análisis de datos, visualización, etcetera. |
| Escalabilidad |Aunque puede especificar Hola número de nodos en el clúster durante la creación, es conveniente toogrow o reducir la carga de trabajo de hello clúster toomatch. Todos los clústeres de HDInsight permiten a toochange número de Hola de nodos de clúster Hola. Además, se pueden quitar clústeres Spark sin pérdida de datos, ya que todos los datos de Hola se almacenan en el almacenamiento de Azure o almacén de Data Lake. |
| Soporte técnico ininterrumpido |Los clústeres de Spark en HDInsight incluyen soporte técnico ininterrumpido de nivel empresarial y un Acuerdo de Nivel de Servicio del 99,9 % de tiempo de actividad. |

## <a name="what-are-hello-use-cases-for-spark-on-hdinsight"></a>¿Qué casos de uso de Hola de Spark en HDInsight?
Los clústeres de Spark en HDInsight permiten Hola escenarios claves siguientes.

### <a name="interactive-data-analysis-and-bi"></a>Análisis interactivo de datos y BI
[Vea un tutorial](hdinsight-apache-spark-use-bi-tools.md)

Apache Spark en HDInsight almacena datos en Azure Storage o Azure Data Lake Store. Expertos comerciales y tomar decisiones clave puede analizar y generar informes con esos datos y usar informes interactivos de Microsoft Power BI toobuild de datos de hello analizado. Los analistas pueden iniciar desde los datos no estructurados y semiestructurados en almacenamiento de clúster, definir un esquema de datos de hello utilizando blocs de notas y, a continuación, generar modelos de datos con Microsoft Power BI. Los clústeres de Spark en HDInsight también admiten varias herramientas de BI de terceros, como Tableau, por lo que es una plataforma ideal para los analistas de datos, expertos de empresa y responsables de la toma de decisiones clave.

### <a name="spark-machine-learning"></a>Aprendizaje automático con Spark
[Mire un tutorial: predecir las temperaturas de edificios con datos HVAC](hdinsight-apache-spark-ipython-notebook-machine-learning.md)

[Mire un tutorial: predecir los resultados de la inspección de alimentos](hdinsight-apache-spark-machine-learning-mllib-ipython.md)

Apache Spark incluye [MLlib](http://spark.apache.org/mllib/), una biblioteca de aprendizaje automático basada en Spark que puede usar desde un clúster de Spark en HDInsight. El clúster de Spark en HDInsight también incluye Anaconda, una distribución de Python con diversos paquetes para aprendizaje automático. Si agregamos a esto la compatibilidad integrada con notebooks de Jupyter y Zeppelin, dispone de un entorno de primera línea para la creación de aplicaciones de aprendizaje automático.

### <a name="spark-streaming-and-real-time-data-analysis"></a>Streaming y análisis de datos en tiempo real con Spark
[Vea un tutorial](hdinsight-apache-spark-eventhub-streaming.md)

Los clústeres de Spark en HDInsight ofrecen amplia compatibilidad para crear soluciones de análisis en tiempo real. Mientras que Spark ya tiene datos de tooingest los conectores de varios orígenes como sockets Kafka, Flume, Twitter, ZeroMQ o TCP, Spark en HDInsight agrega soporte de primera clase para el consumo de datos de los centros de eventos de Azure. Los concentradores de eventos son hello más usadas de puesta en cola de servicio en Azure. La disponibilidad inmediata de la compatibilidad con Event Hubs convierte a los clústeres de Spark en HDInsight en una plataforma ideal para crear la canalización de análisis en tiempo real.

## <a name="next-steps"></a>¿Qué componentes se incluyen como parte de un clúster Spark?
Los clústeres de Spark en HDInsight incluyen Hola después de componentes que están disponibles en los clústeres de Hola de forma predeterminada.

* [Spark Core](https://spark.apache.org/docs/1.5.1/). Incluye Spark Core, Spark SQL, API Spark de streaming, GraphX y MLlib.
* [Anaconda](http://docs.continuum.io/anaconda/)
* [Livy](https://github.com/cloudera/hue/tree/master/apps/spark/java#welcome-to-livy-the-rest-spark-server)
* [Jupyter Notebook](https://jupyter.org)
* [Zeppelin Notebook](http://zeppelin-project.org/)

Los clústeres de Spark en HDInsight también proporcionan una [controlador ODBC](http://go.microsoft.com/fwlink/?LinkId=616229) para clústeres de tooSpark de conectividad en HDInsight de las herramientas de BI como Microsoft Power BI y Tableau.

## <a name="where-do-i-start"></a>¿Por dónde empiezo?
Empiece por crear un clúster de Spark en HDInsight. Consulte el [inicio rápido sobre cómo crear un clúster de Spark en HDInsight Linux y ejecutar consultas interactivas mediante Jupyter](hdinsight-apache-spark-jupyter-spark-sql.md). 

## <a name="next-steps"></a>Pasos siguientes
### <a name="scenarios"></a>Escenarios
* [Spark with BI: Realizar el análisis de datos interactivos con Spark en HDInsight con las herramientas de BI](hdinsight-apache-spark-use-bi-tools.md)
* [Creación de aplicaciones de Aprendizaje automático con Apache Spark en HDInsight de Azure](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark con aprendizaje automático: Use Spark en HDInsight toopredict de resultados de la inspección de alimentos](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Streaming con Spark: uso de Spark en HDInsight para compilar aplicaciones de streaming en tiempo real](hdinsight-apache-spark-eventhub-streaming.md)
* [Análisis del registro del sitio web con Spark en HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a>Creación y ejecución de aplicaciones
* [Crear una aplicación independiente con Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Ejecutar trabajos de forma remota en un clúster de Spark mediante Livy](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>Herramientas y extensiones
* [Usar el complemento de herramientas de HDInsight para toocreate IntelliJ IDEA y enviar Spark Scala aplicaciones](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Usar complemento Herramientas de HDInsight para aplicaciones de IDEA IntelliJ toodebug Spark de forma remota](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Uso de cuadernos de Zeppelin con un clúster Spark en HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Kernels disponibles para el cuaderno de Jupyter en el clúster Spark para HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Uso de paquetes externos con cuadernos de Jupyter Notebook](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Instale Jupyter en el equipo y conecte tooan clúster de HDInsight Spark](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>Administración de recursos
* [Administrar los recursos de clúster de hello Apache Spark en HDInsight de Azure](hdinsight-apache-spark-resource-manager.md)
* [Track and debug jobs running on an Apache Spark cluster in HDInsight (Seguimiento y depuración de trabajos que se ejecutan en un clúster de Apache Spark en HDInsight)](hdinsight-apache-spark-job-debugging.md)
* [Problemas conocidos de Apache Spark en Azure HDInsight](hdinsight-apache-spark-known-issues.md).
