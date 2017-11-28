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
# <a name="fix-a-hive-out-of-memory-error-in-azure-hdinsight"></a><span data-ttu-id="26cc5-105">Corrección de un error de memoria insuficiente de Hive en Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="26cc5-105">Fix a Hive out of memory error in Azure HDInsight</span></span>

<span data-ttu-id="26cc5-106">Obtenga información acerca de cómo toofix un subárbol error de memoria insuficiente al procesar tablas de gran tamaño al establecer la configuración de memoria del subárbol.</span><span class="sxs-lookup"><span data-stu-id="26cc5-106">Learn how toofix a Hive out of memory error when process large tables by configuring Hive memory settings.</span></span>

## <a name="run-hive-query-against-large-tables"></a><span data-ttu-id="26cc5-107">Ejecución de una consulta de Hive en tablas de gran tamaño</span><span class="sxs-lookup"><span data-stu-id="26cc5-107">Run Hive query against large tables</span></span>

<span data-ttu-id="26cc5-108">Un cliente ejecutó una consulta de Hive:</span><span class="sxs-lookup"><span data-stu-id="26cc5-108">A customer ran a Hive query:</span></span>

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

<span data-ttu-id="26cc5-109">Algunos matices de esta consulta:</span><span class="sxs-lookup"><span data-stu-id="26cc5-109">Some nuances of this query:</span></span>

* <span data-ttu-id="26cc5-110">T1 es una tabla grande tooa alias, TABLE1, que tiene un gran número de tipos de columna de cadena.</span><span class="sxs-lookup"><span data-stu-id="26cc5-110">T1 is an alias tooa big table, TABLE1, which has lots of STRING column types.</span></span>
* <span data-ttu-id="26cc5-111">Otras tablas no son tan grandes, pero tienen un gran número de columnas.</span><span class="sxs-lookup"><span data-stu-id="26cc5-111">Other tables are not that big but do have many columns.</span></span>
* <span data-ttu-id="26cc5-112">Todas las tablas se unen entre sí, en algunos casos con varias columnas en TABLE1, etc.</span><span class="sxs-lookup"><span data-stu-id="26cc5-112">All tables are joining each other, in some cases with multiple columns in TABLE1 and others.</span></span>

<span data-ttu-id="26cc5-113">consulta de Hive Hola tardó 26 minutos toofinish en un clúster de HDInsight A3 24 nodo.</span><span class="sxs-lookup"><span data-stu-id="26cc5-113">hello Hive query took 26 minutes toofinish on a 24 node A3 HDInsight cluster.</span></span> <span data-ttu-id="26cc5-114">Hola cliente avisado Hola siguientes mensajes de advertencia:</span><span class="sxs-lookup"><span data-stu-id="26cc5-114">hello customer noticed hello following warning messages:</span></span>

    Warning: Map Join MAPJOIN[428][bigTable=?] in task 'Stage-21:MAPRED' is a cross product
    Warning: Shuffle Join JOIN[8][tables = [t1933775, t1932766]] in Stage 'Stage-4:MAPRED' is a cross product

<span data-ttu-id="26cc5-115">Mediante el uso de motor de ejecución de hello Tez.</span><span class="sxs-lookup"><span data-stu-id="26cc5-115">By using hello Tez execution engine.</span></span> <span data-ttu-id="26cc5-116">Hola misma consulta se ejecutó durante 15 minutos y, a continuación, produjo Hola siguiente error:</span><span class="sxs-lookup"><span data-stu-id="26cc5-116">hello same query ran for 15 minutes, and then threw hello following error:</span></span>

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

<span data-ttu-id="26cc5-117">error de Hello permanece cuando se usa una máquina virtual más grande (por ejemplo, D12).</span><span class="sxs-lookup"><span data-stu-id="26cc5-117">hello error remains when using a bigger virtual machine (for example, D12).</span></span>


## <a name="debug-hello-out-of-memory-error"></a><span data-ttu-id="26cc5-118">Depurar Hola error de memoria insuficiente</span><span class="sxs-lookup"><span data-stu-id="26cc5-118">Debug hello out of memory error</span></span>

<span data-ttu-id="26cc5-119">Nuestro servicio de asistencia y los equipos de ingeniería juntos encuentran uno de los problemas de Hola que hacen que Hola error de memoria insuficiente no era un [conocido problema descrito en hello Apache JIRA](https://issues.apache.org/jira/browse/HIVE-8306):</span><span class="sxs-lookup"><span data-stu-id="26cc5-119">Our support and engineering teams together found one of hello issues causing hello out of memory error was a [known issue described in hello Apache JIRA](https://issues.apache.org/jira/browse/HIVE-8306):</span></span>

    When hive.auto.convert.join.noconditionaltask = true we check noconditionaltask.size and if hello sum  of tables sizes in hello map join is less than noconditionaltask.size hello plan would generate a Map join, hello issue with this is that hello calculation doesnt take into account hello overhead introduced by different HashTable implementation as results if hello sum of input sizes is smaller than hello noconditionaltask size by a small margin queries will hit OOM.

<span data-ttu-id="26cc5-120">Hola **hive.auto.convert.join.noconditionaltask** en hello hive-site.xml archivo estableció demasiado**true**:</span><span class="sxs-lookup"><span data-stu-id="26cc5-120">hello **hive.auto.convert.join.noconditionaltask** in hello hive-site.xml file was set too**true**:</span></span>

    <property>
        <name>hive.auto.convert.join.noconditionaltask</name>
        <value>true</value>
        <description>
              Whether Hive enables hello optimization about converting common join into mapjoin based on hello input file size.
              If this parameter is on, and hello sum of size for n-1 of hello tables/partitions for a n-way join is smaller than the
              specified size, hello join is directly converted tooa mapjoin (there is no conditional task).
        </description>
      </property>

<span data-ttu-id="26cc5-121">Es probable que combinación de asignación fue la causa de Hola de hello espacio de montón de Java nuestro error de memoria.</span><span class="sxs-lookup"><span data-stu-id="26cc5-121">It is likely map join was hello cause of hello Java Heap Space our of memory error.</span></span> <span data-ttu-id="26cc5-122">Como se explica en la entrada de blog de hello [configuración de memoria de Hadoop Yarn de HDInsight](http://blogs.msdn.com/b/shanyu/archive/2014/07/31/hadoop-yarn-memory-settings-in-hdinsigh.aspx), cuando Tez motor de ejecución es el espacio de montón de hello utilizados usa realmente pertenece toohello Tez contenedor.</span><span class="sxs-lookup"><span data-stu-id="26cc5-122">As explained in hello blog post [Hadoop Yarn memory settings in HDInsight](http://blogs.msdn.com/b/shanyu/archive/2014/07/31/hadoop-yarn-memory-settings-in-hdinsigh.aspx), when Tez execution engine is used hello heap space used actually belongs toohello Tez container.</span></span> <span data-ttu-id="26cc5-123">Vea Hola después de memoria de imagen que describen hello Tez contenedor.</span><span class="sxs-lookup"><span data-stu-id="26cc5-123">See hello following image describing hello Tez container memory.</span></span>

![Diagrama de memoria del contenedor de Tez: error de memoria insuficiente de Hive](./media/hdinsight-hadoop-hive-out-of-memory-error-oom/hive-out-of-memory-error-oom-tez-container-memory.png)

<span data-ttu-id="26cc5-125">Como sugiere su entrada de blog de hello, Hola siguiendo dos configuraciones de memoria define la memoria de contenedor de hello para el montón de hello: **hive.tez.container.size** y **hive.tez.java.opts**.</span><span class="sxs-lookup"><span data-stu-id="26cc5-125">As hello blog post suggests, hello following two memory settings define hello container memory for hello heap: **hive.tez.container.size** and **hive.tez.java.opts**.</span></span> <span data-ttu-id="26cc5-126">De nuestra experiencia, Hola excepción de memoria insuficiente no significa el tamaño del contenedor de hello es demasiado pequeño.</span><span class="sxs-lookup"><span data-stu-id="26cc5-126">From our experience, hello out of memory exception does not mean hello container size is too small.</span></span> <span data-ttu-id="26cc5-127">Significa Hola tamaño del montón de Java (hive.tez.java.opts) es demasiado pequeño.</span><span class="sxs-lookup"><span data-stu-id="26cc5-127">It means hello Java heap size (hive.tez.java.opts) is too small.</span></span> <span data-ttu-id="26cc5-128">Por lo que cada vez que se haya quedado sin memoria, puede intentar tooincrease **hive.tez.java.opts**.</span><span class="sxs-lookup"><span data-stu-id="26cc5-128">So whenever you see out of memory, you can try tooincrease **hive.tez.java.opts**.</span></span> <span data-ttu-id="26cc5-129">Si es necesario es posible que tenga tooincrease **hive.tez.container.size**.</span><span class="sxs-lookup"><span data-stu-id="26cc5-129">If needed you might have tooincrease **hive.tez.container.size**.</span></span> <span data-ttu-id="26cc5-130">Hola **java.opts** valor debe ser aproximadamente el 80% de **container.size**.</span><span class="sxs-lookup"><span data-stu-id="26cc5-130">hello **java.opts** setting should be around 80% of **container.size**.</span></span>

> [!NOTE]
> <span data-ttu-id="26cc5-131">configuración de Hello **hive.tez.java.opts** siempre debe ser menor que **hive.tez.container.size**.</span><span class="sxs-lookup"><span data-stu-id="26cc5-131">hello setting **hive.tez.java.opts** must always be smaller than **hive.tez.container.size**.</span></span>
> 
> 

<span data-ttu-id="26cc5-132">Dado que una máquina D12 tiene 28GB de memoria, se decidió toouse un tamaño de contenedor de 10GB (10 240 MB) y asignar el 80% toojava.opts:</span><span class="sxs-lookup"><span data-stu-id="26cc5-132">Because a D12 machine has 28GB memory, we decided toouse a container size of 10GB (10240MB) and assign 80% toojava.opts:</span></span>

    SET hive.tez.container.size=10240
    SET hive.tez.java.opts=-Xmx8192m

<span data-ttu-id="26cc5-133">Con una nueva configuración de hello, consulta Hola se ejecutó correctamente en menos de 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="26cc5-133">With hello new settings, hello query successfully ran in under 10 minutes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="26cc5-134">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="26cc5-134">Next steps</span></span>

<span data-ttu-id="26cc5-135">Recibe un error de memoria insuficiente no significa necesariamente que el tamaño del contenedor de hello es demasiado pequeño.</span><span class="sxs-lookup"><span data-stu-id="26cc5-135">Getting an OOM error doesn't necessarily mean hello container size is too small.</span></span> <span data-ttu-id="26cc5-136">En su lugar, debe configurar opciones de memoria de Hola para que el tamaño del montón de hello aumenta y es al menos el 80% del tamaño de memoria de contenedor de Hola.</span><span class="sxs-lookup"><span data-stu-id="26cc5-136">Instead, you should configure hello memory settings so that hello heap size is increased and is at least 80% of hello container memory size.</span></span> <span data-ttu-id="26cc5-137">Para optimizar las consultas de Hive, vea [Optimizar consultas de Hive para Hadoop en HDInsight](hdinsight-hadoop-optimize-hive-query.md).</span><span class="sxs-lookup"><span data-stu-id="26cc5-137">For optimizing Hive queries, see [Optimize Hive queries for Hadoop in HDInsight](hdinsight-hadoop-optimize-hive-query.md).</span></span>
