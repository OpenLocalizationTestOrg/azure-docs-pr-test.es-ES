---
title: "clúster de problemas de aaaTroubleshoot con Apache Spark en HDInsight de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de los problemas relacionados tooApache clústeres de Spark en HDInsight de Azure y cómo toowork alrededor de los."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 610c4103-ffc8-4ec0-ad06-fdaf3c4d7c10
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 7373b90524ae5dbb10ab8ded593aa38d12c14b55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="known-issues-for-apache-spark-cluster-on-hdinsight"></a>Problemas conocidos de clústeres de Apache Spark en HDInsight

Este documento hace un seguimiento de hello todos los problemas de versión preliminar pública de HDInsight Spark Hola conocidos.  

## <a name="livy-leaks-interactive-session"></a>Sesión interactiva con pérdidas de Livy
Cuando Livio se reinicia (desde Ambari o reinicio de la máquina virtual de tooheadnode 0) con una sesión interactiva mantiene la conexión, se perderá una sesión interactiva de tareas. Por este motivo, podrá trabajos nuevo atascada en hello estado aceptado y no se puede iniciar.

**Mitigación:**

Usar hello siguiendo el problema de hello tooworkaround procedimiento:

1. SSH en el nodo principal. Para más información, consulte [Uso de SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Hola ejecución tras la aplicación de comando toofind Hola identificadores de hello interactivo trabajos iniciado mediante Livio. 
   
        yarn application –list
   
    Hello nombres de trabajo predeterminada será Livio si trabajos Hola iniciados con una sesión interactiva Livio ningún nombre explícito de hello sesión de Livio iniciada por Jupyter notebook, el nombre del trabajo Hola se iniciará con remotesparkmagics_ *. 
3. Siguiente ejecución Hola comando tookill dichos trabajos. 
   
        yarn application –kill <Application ID>

Los nuevos trabajos empezarán a ejecutarse. 

## <a name="spark-history-server-not-started"></a>No se ha iniciado el servidor de historial de Spark
El servidor de historial de Spark no se inicia automáticamente después de crear un clúster.  

**Mitigación:** 

Iniciar manualmente el servidor de historial de Hola desde Ambari.

## <a name="permission-issue-in-spark-log-directory"></a>Problemas con permisos en el directorio de registros de Spark
Cuando hdiuser envía un trabajo con spark-submit, hay un error java.io.FileNotFoundException: hello y /var/log/spark/sparkdriver_hdiuser.log (permiso denegado) no se escribe el registro del controlador. 

**Mitigación:**

1. Agregar grupo de Hadoop de hdiuser toohello. 
2. Proporcione 777 permisos en /var/log/spark después de crear el clúster. 
3. Actualizar ubicación de registro de hello spark con Ambari toobe un directorio 777 permisos.  
4. Ejecute spark-submit como sudo.  

## <a name="spark-phoenix-connector-is-not-supported"></a>No se admite el conector Spark-Phoenix

Actualmente, el conector de Phoenix Spark de hello no es compatible con un clúster de HDInsight Spark.

**Mitigación:**

Debe utilizar el conector de HBase Spark de hello en su lugar. Para obtener instrucciones, consulte [cómo toouse Spark HBase conector](https://blogs.msdn.microsoft.com/azuredatalake/2016/07/25/hdinsight-how-to-use-spark-hbase-connector/).

## <a name="issues-related-toojupyter-notebooks"></a>Problemas relacionados con tooJupyter blocs de notas
Los siguientes son algunos problemas conocidos blocs de notas tooJupyter relacionados.

### <a name="notebooks-with-non-ascii-characters-in-filenames"></a>Cuadernos que tienen caracteres no ASCII en los nombres de archivo
Los cuadernos de Jupyter Notebook que pueden utilizarse en clústeres Spark de HDInsight no deben tener caracteres que no sean ASCII en los nombres de archivo. Si intentas tooupload un archivo a través de hello Jupyter UI que tiene un nombre de archivo no son ASCII, producirá un error en modo silencioso (es decir, Jupyter no le permitirá cargar archivo hello, pero no produce un error visible ya sea). 

### <a name="error-while-loading-notebooks-of-larger-sizes"></a>Error al cargar cuadernos con tamaños mayores
Es posible que aparezca un error **`Error loading notebook`** al cargar cuadernos de mayor tamaño.  

**Mitigación:**

El hecho de recibir este error no implica que los datos estén dañados o perdidos.  Los blocs de notas están todavía en el disco en `/var/lib/jupyter`, y puede SSH en hello clúster tooaccess ellos. Para más información, consulte [Uso de SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

Una vez que se ha conectado el clúster toohello mediante SSH, puede copiar los blocs de notas desde el equipo local de clúster tooyour (uso de SCP o WinSCP) como una pérdida de hello tooprevent copia de seguridad de los datos importantes en el Bloc de notas de Hola. Puede, a continuación, túnel SSH en el nodo principal en el puerto 8001 tooaccess Jupyter sin tener que pasar a través de puerta de enlace de Hola.  Desde allí, puede borrar la salida de hello del Bloc de notas y volver a guardarla tamaño toominimize Hola Bloc de notas.

tooprevent este error suceda en hello futura, debe seguir algunas prácticas recomendadas:

* Es importante tookeep Hola Bloc de notas el tamaño pequeño. Los resultados de los trabajos de Spark que se le envía tooJupyter se conserva en el Bloc de notas de Hola.  Es una práctica recomendada con Jupyter en tooavoid general ejecutando `.collect()` en RDD grandes o tramas de datos; en su lugar, si desea que toopeek en el contenido de un diseño dirigido por responsabilidades, considere la posibilidad de ejecutar `.take()` o `.sample()` para que el resultado no obtenga demasiado grande.
* Además, cuando se guarda un bloc de notas, desactive todas las celdas tooreduce Hola tamaño resultante.

### <a name="notebook-initial-startup-takes-longer-than-expected"></a>El primer inicio del cuaderno tarda más de lo esperado
La primera instrucción del cuaderno de Jupyter con la instrucción mágica de Spark podría tardar más de un minuto.  

**Explicación:**

Esto sucede porque cuando se ejecuta la primera celda de código de hello. En segundo plano de hello este comando inicia configuración de sesión y Spark, SQL y se establecen los contextos de Hive. Después de que se establecen estos contextos, se ejecuta la primera instrucción de Hola y así, impresión de Hola que instrucción Hola tardó un toocomplete mucho tiempo.

### <a name="jupyter-notebook-timeout-in-creating-hello-session"></a>Tiempo de espera de Jupyter notebook en Crear sesión de Hola
Al clúster de Spark carece de recursos, hello Spark y kernels Pyspark en el Bloc de notas de hello Jupyter aparecerá tratando de sesión de hello toocreate de tiempo de espera. 

**Mitigaciones:** 

1. Libere algunos recursos del clúster Spark de la siguiente forma:
   
   * Detener otros blocs de notas de Spark va toohello cierre y menú de detención o al hacer clic en Cerrar en el Explorador de hello Bloc de notas.
   * Detenga otras aplicaciones de Spark desde YARN.
2. Reinicie el Bloc de notas de Hola que estaba intentando toostart seguridad. Suficientes recursos deben estar disponibles para toocreate una sesión ahora.

## <a name="see-also"></a>Otras referencias
* [Introducción a Apache Spark en HDInsight de Azure](hdinsight-apache-spark-overview.md)

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

