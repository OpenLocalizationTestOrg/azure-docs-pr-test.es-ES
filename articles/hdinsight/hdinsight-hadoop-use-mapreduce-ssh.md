---
title: "aaaMapReduce y conexión de SSH con Hadoop en HDInsight - Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse SSH toorun MapReduce trabajos usando Hadoop en HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 844678ba-1e1f-4fda-b9ef-34df4035d547
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 9626577687fc5cc119a39d65a9c45298f57f81c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-mapreduce-with-hadoop-on-hdinsight-with-ssh"></a><span data-ttu-id="243f9-103">Uso de MapReduce con Hadoop en HDInsight con SSH</span><span class="sxs-lookup"><span data-stu-id="243f9-103">Use MapReduce with Hadoop on HDInsight with SSH</span></span>

[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

<span data-ttu-id="243f9-104">Obtenga información acerca de cómo toosubmit MapReduce trabajos desde un tooHDInsight de conexión de Secure Shell (SSH).</span><span class="sxs-lookup"><span data-stu-id="243f9-104">Learn how toosubmit MapReduce jobs from a Secure Shell (SSH) connection tooHDInsight.</span></span>

> [!NOTE]
> <span data-ttu-id="243f9-105">Si ya está familiarizado con el uso de Hadoop basado en Linux, servidores, pero están tooHDInsight nueva, vea [sugerencias de HDInsight basados en Linux](hdinsight-hadoop-linux-information.md).</span><span class="sxs-lookup"><span data-stu-id="243f9-105">If you are already familiar with using Linux-based Hadoop servers, but you are new tooHDInsight, see [Linux-based HDInsight tips](hdinsight-hadoop-linux-information.md).</span></span>

## <span data-ttu-id="243f9-106"><a id="prereq"></a>Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="243f9-106"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="243f9-107">Un clúster de HDInsight basado en Linux (Hadoop en HDInsight)</span><span class="sxs-lookup"><span data-stu-id="243f9-107">A Linux-based HDInsight (Hadoop on HDInsight) cluster</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="243f9-108">Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior.</span><span class="sxs-lookup"><span data-stu-id="243f9-108">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="243f9-109">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="243f9-109">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="243f9-110">Un cliente SSH.</span><span class="sxs-lookup"><span data-stu-id="243f9-110">An SSH client.</span></span> <span data-ttu-id="243f9-111">Para más información, consulte [Uso de SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="243f9-111">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>

## <span data-ttu-id="243f9-112"><a id="ssh"></a>Conexión con SSH</span><span class="sxs-lookup"><span data-stu-id="243f9-112"><a id="ssh"></a>Connect with SSH</span></span>

<span data-ttu-id="243f9-113">Conecte el clúster toohello mediante SSH.</span><span class="sxs-lookup"><span data-stu-id="243f9-113">Connect toohello cluster using SSH.</span></span> <span data-ttu-id="243f9-114">Por ejemplo, hello siguiente comando conecta con el nombre de clúster de tooa **myhdinsight**:</span><span class="sxs-lookup"><span data-stu-id="243f9-114">For example, hello following command connects tooa cluster named **myhdinsight**:</span></span>

```bash
ssh admin@myhdinsight-ssh.azurehdinsight.net
```

<span data-ttu-id="243f9-115">**Si utiliza una clave de certificado para la autenticación de SSH**, deberá toospecify ubicación de Hola de clave privada de hello en el sistema cliente, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="243f9-115">**If you use a certificate key for SSH authentication**, you may need toospecify hello location of hello private key on your client system, for example:</span></span>

```bash
ssh -i ~/mykey.key admin@myhdinsight-ssh.azurehdinsight.net
```

<span data-ttu-id="243f9-116">**Si utiliza una contraseña para la autenticación de SSH**, necesitará tooprovide Hola contraseña cuando se le solicite.</span><span class="sxs-lookup"><span data-stu-id="243f9-116">**If you use a password for SSH authentication**, you need tooprovide hello password when prompted.</span></span>

<span data-ttu-id="243f9-117">Para obtener más información sobre cómo utilizar SSH con HDInsight, consulte [Uso de SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="243f9-117">For more information on using SSH with HDInsight, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <span data-ttu-id="243f9-118"><a id="hadoop"></a>Uso de comandos Hadoop</span><span class="sxs-lookup"><span data-stu-id="243f9-118"><a id="hadoop"></a>Use Hadoop commands</span></span>

1. <span data-ttu-id="243f9-119">Después de clúster de HDInsight toohello conectado, use Hola después comando toostart un trabajo de MapReduce:</span><span class="sxs-lookup"><span data-stu-id="243f9-119">After you are connected toohello HDInsight cluster, use hello following command toostart a MapReduce job:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/WordCountOutput
    ```

    <span data-ttu-id="243f9-120">Este comando inicia hello `wordcount` (clase), que se encuentra en hello `hadoop-mapreduce-examples.jar` archivo.</span><span class="sxs-lookup"><span data-stu-id="243f9-120">This command starts hello `wordcount` class, which is contained in hello `hadoop-mapreduce-examples.jar` file.</span></span> <span data-ttu-id="243f9-121">Usa hello `/example/data/gutenberg/davinci.txt` documento como entrada y salida se almacena en `/example/data/WordCountOutput`.</span><span class="sxs-lookup"><span data-stu-id="243f9-121">It uses hello `/example/data/gutenberg/davinci.txt` document as input, and output is stored at `/example/data/WordCountOutput`.</span></span>

    > [!NOTE]
    > <span data-ttu-id="243f9-122">Para obtener más información acerca de estos datos de ejemplo de Hola y de trabajo de MapReduce, consulte [uso MapReduce en Hadoop en HDInsight](hdinsight-use-mapreduce.md).</span><span class="sxs-lookup"><span data-stu-id="243f9-122">For more information about this MapReduce job and hello example data, see [Use MapReduce in Hadoop on HDInsight](hdinsight-use-mapreduce.md).</span></span>

2. <span data-ttu-id="243f9-123">trabajo de Hello emite detalles tal y como lo procesa y devuelve información toohello similar después de texto cuando se completa el trabajo de hello:</span><span class="sxs-lookup"><span data-stu-id="243f9-123">hello job emits details as it processes, and it returns information similar toohello following text when hello job completes:</span></span>

        File Input Format Counters
        Bytes Read=1395666
        File Output Format Counters
        Bytes Written=337623

3. <span data-ttu-id="243f9-124">Cuando se completa el trabajo de hello, utilice Hola siguientes archivos de salida de comando toolist hello:</span><span class="sxs-lookup"><span data-stu-id="243f9-124">When hello job completes, use hello following command toolist hello output files:</span></span>

    ```bash
    hdfs dfs -ls /example/data/WordCountOutput
    ```

    <span data-ttu-id="243f9-125">Este comando muestra dos archivos, `_SUCCESS` y `part-r-00000`.</span><span class="sxs-lookup"><span data-stu-id="243f9-125">This command display two files, `_SUCCESS` and `part-r-00000`.</span></span> <span data-ttu-id="243f9-126">Hola `part-r-00000` archivo contiene la salida de hello para este trabajo.</span><span class="sxs-lookup"><span data-stu-id="243f9-126">hello `part-r-00000` file contains hello output for this job.</span></span>

    > [!NOTE]
    > <span data-ttu-id="243f9-127">Pueden que algunos de estos trabajos MapReduce divida resultados Hola entre varios **parte-r-###** archivos.</span><span class="sxs-lookup"><span data-stu-id="243f9-127">Some MapReduce jobs may split hello results across multiple **part-r-#####** files.</span></span> <span data-ttu-id="243f9-128">Si es así, usar hello ### tooindicate Hola orden de los archivos de Hola de sufijos.</span><span class="sxs-lookup"><span data-stu-id="243f9-128">If so, use hello ##### suffix tooindicate hello order of hello files.</span></span>

4. <span data-ttu-id="243f9-129">salida de hello tooview, Hola de uso siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="243f9-129">tooview hello output, use hello following command:</span></span>

    ```bash
    hdfs dfs -cat /example/data/WordCountOutput/part-r-00000
    ```

    <span data-ttu-id="243f9-130">Este comando muestra una lista de palabras de Hola que figuran en hello **wasb://example/data/gutenberg/davinci.txt** hello y archivo de número de veces que se produjo cada palabra.</span><span class="sxs-lookup"><span data-stu-id="243f9-130">This command displays a list of hello words that are contained in hello **wasb://example/data/gutenberg/davinci.txt** file and hello number of times each word occurred.</span></span> <span data-ttu-id="243f9-131">Hello texto siguiente es un ejemplo de Hola datos que se encuentra en el archivo hello:</span><span class="sxs-lookup"><span data-stu-id="243f9-131">hello following text is an example of hello data that is contained in hello file:</span></span>

        wreathed        3
        wreathing       1
        wreaths         1
        wrecked         3
        wrenching       1
        wretched        6
        wriggling       1

## <span data-ttu-id="243f9-132"><a id="summary"></a>Resumen</span><span class="sxs-lookup"><span data-stu-id="243f9-132"><a id="summary"></a>Summary</span></span>

<span data-ttu-id="243f9-133">Como puede ver, comandos de Hadoop constan de una manera sencilla de toorun trabajos MapReduce en un clúster de HDInsight y, a continuación, ver la salida de trabajo Hola.</span><span class="sxs-lookup"><span data-stu-id="243f9-133">As you can see, Hadoop commands provide an easy way toorun MapReduce jobs in an HDInsight cluster and then view hello job output.</span></span>

## <span data-ttu-id="243f9-134"><a id="nextsteps"></a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="243f9-134"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="243f9-135">Para obtener información general sobre los trabajos de MapReduce en HDInsight:</span><span class="sxs-lookup"><span data-stu-id="243f9-135">For general information about MapReduce jobs in HDInsight:</span></span>

* [<span data-ttu-id="243f9-136">Uso de MapReduce en Hadoop de HDInsight</span><span class="sxs-lookup"><span data-stu-id="243f9-136">Use MapReduce on HDInsight Hadoop</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="243f9-137">Para obtener información sobre otras maneras de trabajar con Hadoop en HDInsight:</span><span class="sxs-lookup"><span data-stu-id="243f9-137">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="243f9-138">Uso de Hive con Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="243f9-138">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="243f9-139">Uso de Pig con Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="243f9-139">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
