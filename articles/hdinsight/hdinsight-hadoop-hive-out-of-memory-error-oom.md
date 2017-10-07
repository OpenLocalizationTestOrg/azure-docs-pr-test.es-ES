---
title: "aaaFix un subárbol de error de memoria en HDInsight de Azure | Documentos de Microsoft"
description: "Corrija un error de memoria insuficiente de Hive en HDInsight. escenario de cliente Hello es una consulta a través de muchas tablas de gran tamaño."
keywords: "error de memoria insuficiente, OOM, configuración de Hive"
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 7bce3dff-9825-4fa0-a568-c52a9f7d1dad
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/17/2017
ms.author: jgao
ms.openlocfilehash: 00a12969322c1e74434ba6593ffd098f342edd84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="fix-a-hive-out-of-memory-error-in-azure-hdinsight"></a>Corrección de un error de memoria insuficiente de Hive en Azure HDInsight

Obtenga información acerca de cómo toofix un subárbol error de memoria insuficiente al procesar tablas de gran tamaño al establecer la configuración de memoria del subárbol.

## <a name="run-hive-query-against-large-tables"></a>Ejecución de una consulta de Hive en tablas de gran tamaño

Un cliente ejecutó una consulta de Hive:

    SELECT
        COUNT (T1.COLUMN1) as DisplayColumn1,
        …
        …
        ….
    FROM
        TABLE1 T1,
        TABLE2 T2,
        TABLE3 T3,
        TABLE5 T4,
        TABLE6 T5,
        TABLE7 T6
    where (T1.KEY1 = T2.KEY1….
        …
        …

Algunos matices de esta consulta:

* T1 es una tabla grande tooa alias, TABLE1, que tiene un gran número de tipos de columna de cadena.
* Otras tablas no son tan grandes, pero tienen un gran número de columnas.
* Todas las tablas se unen entre sí, en algunos casos con varias columnas en TABLE1, etc.

consulta de Hive Hola tardó 26 minutos toofinish en un clúster de HDInsight A3 24 nodo. Hola cliente avisado Hola siguientes mensajes de advertencia:

    Warning: Map Join MAPJOIN[428][bigTable=?] in task 'Stage-21:MAPRED' is a cross product
    Warning: Shuffle Join JOIN[8][tables = [t1933775, t1932766]] in Stage 'Stage-4:MAPRED' is a cross product

Mediante el uso de motor de ejecución de hello Tez. Hola misma consulta se ejecutó durante 15 minutos y, a continuación, produjo Hola siguiente error:

    Status: Failed
    Vertex failed, vertexName=Map 5, vertexId=vertex_1443634917922_0008_1_05, diagnostics=[Task failed, taskId=task_1443634917922_0008_1_05_000006, diagnostics=[TaskAttempt 0 failed, info=[Error: Failure while running task:java.lang.RuntimeException: java.lang.OutOfMemoryError: Java heap space
        at
    org.apache.hadoop.hive.ql.exec.tez.TezProcessor.initializeAndRunProcessor(TezProcessor.java:172)
        at org.apache.hadoop.hive.ql.exec.tez.TezProcessor.run(TezProcessor.java:138)
        at
    org.apache.tez.runtime.LogicalIOProcessorRuntimeTask.run(LogicalIOProcessorRuntimeTask.java:324)
        at
    org.apache.tez.runtime.task.TezTaskRunner$TaskRunnerCallable$1.run(TezTaskRunner.java:176)
        at
    org.apache.tez.runtime.task.TezTaskRunner$TaskRunnerCallable$1.run(TezTaskRunner.java:168)
        at java.security.AccessController.doPrivileged(Native Method)
        at javax.security.auth.Subject.doAs(Subject.java:415)
        at org.apache.hadoop.security.UserGroupInformation.doAs(UserGroupInformation.java:1628)
        at
    org.apache.tez.runtime.task.TezTaskRunner$TaskRunnerCallable.call(TezTaskRunner.java:168)
        at
    org.apache.tez.runtime.task.TezTaskRunner$TaskRunnerCallable.call(TezTaskRunner.java:163)
        at java.util.concurrent.FutureTask.run(FutureTask.java:262)
        at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1145)
        at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:615)
        at java.lang.Thread.run(Thread.java:745)
    Caused by: java.lang.OutOfMemoryError: Java heap space

error de Hello permanece cuando se usa una máquina virtual más grande (por ejemplo, D12).


## <a name="debug-hello-out-of-memory-error"></a>Depurar Hola error de memoria insuficiente

Nuestro servicio de asistencia y los equipos de ingeniería juntos encuentran uno de los problemas de Hola que hacen que Hola error de memoria insuficiente no era un [conocido problema descrito en hello Apache JIRA](https://issues.apache.org/jira/browse/HIVE-8306):

    When hive.auto.convert.join.noconditionaltask = true we check noconditionaltask.size and if hello sum  of tables sizes in hello map join is less than noconditionaltask.size hello plan would generate a Map join, hello issue with this is that hello calculation doesnt take into account hello overhead introduced by different HashTable implementation as results if hello sum of input sizes is smaller than hello noconditionaltask size by a small margin queries will hit OOM.

Hola **hive.auto.convert.join.noconditionaltask** en hello hive-site.xml archivo estableció demasiado**true**:

    <property>
        <name>hive.auto.convert.join.noconditionaltask</name>
        <value>true</value>
        <description>
              Whether Hive enables hello optimization about converting common join into mapjoin based on hello input file size.
              If this parameter is on, and hello sum of size for n-1 of hello tables/partitions for a n-way join is smaller than the
              specified size, hello join is directly converted tooa mapjoin (there is no conditional task).
        </description>
      </property>

Es probable que combinación de asignación fue la causa de Hola de hello espacio de montón de Java nuestro error de memoria. Como se explica en la entrada de blog de hello [configuración de memoria de Hadoop Yarn de HDInsight](http://blogs.msdn.com/b/shanyu/archive/2014/07/31/hadoop-yarn-memory-settings-in-hdinsigh.aspx), cuando Tez motor de ejecución es el espacio de montón de hello utilizados usa realmente pertenece toohello Tez contenedor. Vea Hola después de memoria de imagen que describen hello Tez contenedor.

![Diagrama de memoria del contenedor de Tez: error de memoria insuficiente de Hive](./media/hdinsight-hadoop-hive-out-of-memory-error-oom/hive-out-of-memory-error-oom-tez-container-memory.png)

Como sugiere su entrada de blog de hello, Hola siguiendo dos configuraciones de memoria define la memoria de contenedor de hello para el montón de hello: **hive.tez.container.size** y **hive.tez.java.opts**. De nuestra experiencia, Hola excepción de memoria insuficiente no significa el tamaño del contenedor de hello es demasiado pequeño. Significa Hola tamaño del montón de Java (hive.tez.java.opts) es demasiado pequeño. Por lo que cada vez que se haya quedado sin memoria, puede intentar tooincrease **hive.tez.java.opts**. Si es necesario es posible que tenga tooincrease **hive.tez.container.size**. Hola **java.opts** valor debe ser aproximadamente el 80% de **container.size**.

> [!NOTE]
> configuración de Hello **hive.tez.java.opts** siempre debe ser menor que **hive.tez.container.size**.
> 
> 

Dado que una máquina D12 tiene 28GB de memoria, se decidió toouse un tamaño de contenedor de 10GB (10 240 MB) y asignar el 80% toojava.opts:

    SET hive.tez.container.size=10240
    SET hive.tez.java.opts=-Xmx8192m

Con una nueva configuración de hello, consulta Hola se ejecutó correctamente en menos de 10 minutos.

## <a name="next-steps"></a>Pasos siguientes

Recibe un error de memoria insuficiente no significa necesariamente que el tamaño del contenedor de hello es demasiado pequeño. En su lugar, debe configurar opciones de memoria de Hola para que el tamaño del montón de hello aumenta y es al menos el 80% del tamaño de memoria de contenedor de Hola. Para optimizar las consultas de Hive, vea [Optimizar consultas de Hive para Hadoop en HDInsight](hdinsight-hadoop-optimize-hive-query.md).
