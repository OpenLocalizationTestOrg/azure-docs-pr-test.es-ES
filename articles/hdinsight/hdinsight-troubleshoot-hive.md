---
title: "aaaTroubleshoot subárbol mediante el uso de HDInsight de Azure | Documentos de Microsoft"
description: "Obtenga respuestas toocommon preguntas sobre cómo trabajar con Apache Hive y HDInsight de Azure."
keywords: "Azure HDInsight, Hive, preguntas más frecuentes, guía de solución de problemas, preguntas comunes"
services: Azure HDInsight
documentationcenter: na
author: dharmeshkakadia
manager: 
editor: 
ms.assetid: 15B8D0F3-F2D3-4746-BDCB-C72944AA9252
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/7/2017
ms.author: dharmeshkakadia
ms.openlocfilehash: ac459316e658d0b29eb66f5685f0bc7e693bb277
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-hive-by-using-azure-hdinsight"></a>Solución de problemas de Hive mediante Azure HDInsight

Obtenga información sobre preguntas más frecuentes de Hola y sus soluciones cuando se trabaja con cargas Apache Hive en Apache Ambari.


## <a name="how-do-i-export-a-hive-metastore-and-import-it-on-another-cluster"></a>¿Cómo se exporta Hive Metastore y se importa en otro clúster?


### <a name="resolution-steps"></a>Pasos de la solución

1. Conecta el clúster de HDInsight de toohello con un cliente de Shell seguro (SSH). Para más información, consulte [Lecturas adicionales](#additional-reading-end).

2. Ejecute hello siguiente comando en clúster de HDInsight de Hola desde el que desea que tienda de metadatos de Hola tooexport:

    ```apache
    for d in `hive -e "show databases"`; do echo "create database $d; use $d;" >> alltables.sql ; for t in `hive --database $d -e "show tables"` ; do ddl=`hive --database $d -e "show create table $t"`; echo "$ddl ;" >> alltables.sql ; echo "$ddl" | grep -q "PARTITIONED\s*BY" && echo "MSCK REPAIR TABLE $t ;" >> alltables.sql ; done; done
    ```

  Este comando genera un archivo denominado allatables.sql.

3. Copie Hola archivo alltables.sql toohello nuevo clúster de HDInsight y, a continuación, ejecute el siguiente comando de hello:

  ```apache
  hive -f alltables.sql
  ```

código de Hello en los pasos de resolución de Hola se da por supuesto que las rutas de acceso en el nuevo clúster de Hola de datos mismo Hola como rutas de acceso de datos de hello en el clúster antiguo Hola. Si las rutas de acceso de datos de hello son diferentes, puede editar manualmente Hola genera alltables.sql archivo tooreflect los cambios.

### <a name="additional-reading"></a>Lecturas adicionales

- [Conecta el clúster de HDInsight de tooan a través de SSH](hdinsight-hadoop-linux-use-ssh-unix.md)


## <a name="how-do-i-locate-hive-logs-on-a-cluster"></a>Búsqueda de registros de Hive en un clúster

### <a name="resolution-steps"></a>Pasos de la solución

1. Conecte el clúster de HDInsight toohello a través de SSH. Para más información, consulte **Lecturas adicionales**.

2. registros de cliente de tooview Hive, utilice Hola siguiente comando:

  ```apache
  /tmp/<username>/hive.log 
  ```

3. registros de tienda de metadatos de Hive tooview, usar hello siguiente comando:

  ```apache
  /var/log/hive/hivemetastore.log 
  ```

4. tooview Hiveserver registros, utilice Hola siguiente comando:

  ```apache
  /var/log/hive/hiveserver2.log 
  ```

### <a name="additional-reading"></a>Lecturas adicionales

- [Conecta el clúster de HDInsight de tooan a través de SSH](hdinsight-hadoop-linux-use-ssh-unix.md)


## <a name="how-do-i-launch-hello-hive-shell-with-specific-configurations-on-a-cluster"></a>Cómo se puede iniciar Hola shell de Hive con configuraciones específicas en un clúster

### <a name="resolution-steps"></a>Pasos de la solución

1. Especificar un par de clave y valor de configuración cuando se inicia Hola shell de Hive. Para más información, consulte [Lecturas adicionales](#additional-reading-end).

  ```apache
  hive -hiveconf a=b 
  ```

2. toolist de comandos de todas las configuraciones efectivo en shell de Hive, Hola de uso después de:

  ```apache
  hive> set;
  ```

  Por ejemplo, usar hello siguiendo el shell de comandos toostart Hive con el registro de depuración habilitado en la consola de hello:

  ```apache
  hive -hiveconf hive.root.logger=ALL,console 
  ```

### <a name="additional-reading"></a>Lecturas adicionales

- [Propiedades de configuración de Hive](https://cwiki.apache.org/confluence/display/Hive/Configuration+Properties)


## <a name="how-do-i-analyze-tez-dag-data-on-a-cluster-critical-path"></a>Análisis de datos DAG de Tez en una ruta crítica de clúster


### <a name="resolution-steps"></a>Pasos de la solución
 
1. tooanalyze una Tez Apache dirige gráfico acíclico (DAG) en un gráfico de clúster crítico, clúster de HDInsight de toohello se conectan a través de SSH. Para más información, consulte [Lecturas adicionales](#additional-reading-end).

2. En un símbolo del sistema, ejecute hello siguiente comando:
   
  ```apache
  hadoop jar /usr/hdp/current/tez-client/tez-job-analyzer-*.jar CriticalPath --saveResults --dagId <DagId> --eventFileName <DagData.zip> 
  ```

3. toolist otros analizadores que pueden ser utilizado tooanalyze Tez DAG, usar hello siguiente comando:

  ```apache
  hadoop jar /usr/hdp/current/tez-client/tez-job-analyzer-*.jar
  ```

  Debe proporcionar un programa de ejemplo como primer argumento de Hola.

  Los nombres de programa válidos incluyen:
    - **ContainerReuseAnalyzer**: imprima los detalles de la reutilización del contenedor en un DAG.
    - **CriticalPath**: ruta crítica de Hola de búsqueda de un DAG
    - **LocalityAnalyzer**: imprima los detalles de localidad en un DAG.
    - **ShuffleTimeAnalyzer**: analizar los detalles de tiempo de hello orden aleatorio en un DAG
    - **SkewAnalyzer**: analizar los detalles sesgo de hello en un DAG
    - **SlowNodeAnalyzer**: imprima los detalles del nodo en un DAG.
    - **SlowTaskIdentifier**: imprima los detalles de una tarea lenta en un DAG.
    - **SlowestVertexAnalyzer**: imprima los detalles de los vértices más lentos en un DAG.
    - **SpillAnalyzer**: imprima los detalles de desbordamiento en un DAG.
    - **TaskConcurrencyAnalyzer**: imprimir los detalles de simultaneidad de la tarea de hello en un DAG
    - **VertexLevelCriticalPathAnalyzer**: ruta crítica de Hola de búsqueda en el nivel de vértices en un DAG


### <a name="additional-reading"></a>Lecturas adicionales

- [Conecta el clúster de HDInsight de tooan a través de SSH](hdinsight-hadoop-linux-use-ssh-unix.md)


## <a name="how-do-i-download-tez-dag-data-from-a-cluster"></a>Cómo se descargan datos de DAG de Tez de un clúster


#### <a name="resolution-steps"></a>Pasos de la solución

Hay dos formas de datos de Tez DAG Hola toocollect:

- Desde la línea de comandos de hello:
 
    Conecte el clúster de HDInsight toohello a través de SSH. En el símbolo de hello, ejecute hello siguiente comando:

  ```apache
  hadoop jar /usr/hdp/current/tez-client/tez-history-parser-*.jar org.apache.tez.history.ATSImportTool -downloadDir . -dagId <DagId> 
  ```

- Usar hello Ambari Tez vista:
   
  1. Vaya tooAmbari. 
  2. Vista de tooTez vaya (bajo el icono de mosaicos de hello en la esquina superior derecha de hello). 
  3. Seleccione Hola DAG desea tooview.
  4. Seleccione **Descargar datos**.

### <a name="additional-reading-end"></a>Lecturas adicionales

[Conecta el clúster de HDInsight de tooan a través de SSH](hdinsight-hadoop-linux-use-ssh-unix.md)






