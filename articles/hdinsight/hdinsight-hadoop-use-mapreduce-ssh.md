---
title: "MapReduce y conexión de SSH con Hadoop en HDInsight (Azure) | Microsoft Docs"
description: "Obtenga más información sobre cómo usar SSH para ejecutar trabajos de MapReduce mediante Hadoop en HDInsight."
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
ms.openlocfilehash: eaf6278f97cd5ddd7e049ff4745181f39d7949a0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="use-mapreduce-with-hadoop-on-hdinsight-with-ssh"></a><span data-ttu-id="20892-103">Uso de MapReduce con Hadoop en HDInsight con SSH</span><span class="sxs-lookup"><span data-stu-id="20892-103">Use MapReduce with Hadoop on HDInsight with SSH</span></span>

[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

<span data-ttu-id="20892-104">Aprenda a enviar trabajos de MapReduce desde una conexión Secure Shell (SSH) a HDInsight.</span><span class="sxs-lookup"><span data-stu-id="20892-104">Learn how to submit MapReduce jobs from a Secure Shell (SSH) connection to HDInsight.</span></span>

> [!NOTE]
> <span data-ttu-id="20892-105">Si ya está familiarizado con el uso de servidores de Hadoop basados en Linux, pero no conoce HDInsight, consulte [Información sobre el uso de HDInsight en Linux](hdinsight-hadoop-linux-information.md).</span><span class="sxs-lookup"><span data-stu-id="20892-105">If you are already familiar with using Linux-based Hadoop servers, but you are new to HDInsight, see [Linux-based HDInsight tips](hdinsight-hadoop-linux-information.md).</span></span>

## <span data-ttu-id="20892-106"><a id="prereq"></a>Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="20892-106"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="20892-107">Un clúster de HDInsight basado en Linux (Hadoop en HDInsight)</span><span class="sxs-lookup"><span data-stu-id="20892-107">A Linux-based HDInsight (Hadoop on HDInsight) cluster</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="20892-108">Linux es el único sistema operativo que se usa en la versión 3.4 de HDInsight, o en las superiores.</span><span class="sxs-lookup"><span data-stu-id="20892-108">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="20892-109">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="20892-109">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="20892-110">Un cliente SSH.</span><span class="sxs-lookup"><span data-stu-id="20892-110">An SSH client.</span></span> <span data-ttu-id="20892-111">Para más información, consulte [Uso de SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="20892-111">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>

## <span data-ttu-id="20892-112"><a id="ssh"></a>Conexión con SSH</span><span class="sxs-lookup"><span data-stu-id="20892-112"><a id="ssh"></a>Connect with SSH</span></span>

<span data-ttu-id="20892-113">Conéctese al clúster con SSH.</span><span class="sxs-lookup"><span data-stu-id="20892-113">Connect to the cluster using SSH.</span></span> <span data-ttu-id="20892-114">Por ejemplo, el siguiente comando conecta con un clúster llamado **myhdinsight**:</span><span class="sxs-lookup"><span data-stu-id="20892-114">For example, the following command connects to a cluster named **myhdinsight**:</span></span>

```bash
ssh admin@myhdinsight-ssh.azurehdinsight.net
```

<span data-ttu-id="20892-115">**Si usa una clave de certificado para la autenticación SSH**, puede que deba especificar la ubicación de la clave privada en su sistema cliente, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="20892-115">**If you use a certificate key for SSH authentication**, you may need to specify the location of the private key on your client system, for example:</span></span>

```bash
ssh -i ~/mykey.key admin@myhdinsight-ssh.azurehdinsight.net
```

<span data-ttu-id="20892-116">**Si usa una contraseña para la autenticación SSH**, deberá proporcionar la contraseña cuando se le solicite.</span><span class="sxs-lookup"><span data-stu-id="20892-116">**If you use a password for SSH authentication**, you need to provide the password when prompted.</span></span>

<span data-ttu-id="20892-117">Para obtener más información sobre cómo utilizar SSH con HDInsight, consulte [Uso de SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="20892-117">For more information on using SSH with HDInsight, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <span data-ttu-id="20892-118"><a id="hadoop"></a>Uso de comandos Hadoop</span><span class="sxs-lookup"><span data-stu-id="20892-118"><a id="hadoop"></a>Use Hadoop commands</span></span>

1. <span data-ttu-id="20892-119">Después de conectarse al clúster de HDInsight, use el siguiente comando para iniciar un trabajo de MapReduce:</span><span class="sxs-lookup"><span data-stu-id="20892-119">After you are connected to the HDInsight cluster, use the following command to start a MapReduce job:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/WordCountOutput
    ```

    <span data-ttu-id="20892-120">Este comando inicia la clase `wordcount`, que está contenido en el archivo `hadoop-mapreduce-examples.jar`.</span><span class="sxs-lookup"><span data-stu-id="20892-120">This command starts the `wordcount` class, which is contained in the `hadoop-mapreduce-examples.jar` file.</span></span> <span data-ttu-id="20892-121">Emplea como entrada el documento `/example/data/gutenberg/davinci.txt` y la salida se almacena en `/example/data/WordCountOutput`.</span><span class="sxs-lookup"><span data-stu-id="20892-121">It uses the `/example/data/gutenberg/davinci.txt` document as input, and output is stored at `/example/data/WordCountOutput`.</span></span>

    > [!NOTE]
    > <span data-ttu-id="20892-122">Para obtener más información sobre este trabajo de MapReduce y los datos de ejemplo, vea [Uso de MapReduce en Hadoop en HDInsight](hdinsight-use-mapreduce.md).</span><span class="sxs-lookup"><span data-stu-id="20892-122">For more information about this MapReduce job and the example data, see [Use MapReduce in Hadoop on HDInsight](hdinsight-use-mapreduce.md).</span></span>

2. <span data-ttu-id="20892-123">El trabajo emite detalles a medida que se procesa y devuelve información similar al siguiente texto cuando finaliza el trabajo:</span><span class="sxs-lookup"><span data-stu-id="20892-123">The job emits details as it processes, and it returns information similar to the following text when the job completes:</span></span>

        File Input Format Counters
        Bytes Read=1395666
        File Output Format Counters
        Bytes Written=337623

3. <span data-ttu-id="20892-124">Una vez completado el trabajo, use el siguiente comando para enumerar los archivos de salida:</span><span class="sxs-lookup"><span data-stu-id="20892-124">When the job completes, use the following command to list the output files:</span></span>

    ```bash
    hdfs dfs -ls /example/data/WordCountOutput
    ```

    <span data-ttu-id="20892-125">Este comando muestra dos archivos, `_SUCCESS` y `part-r-00000`.</span><span class="sxs-lookup"><span data-stu-id="20892-125">This command display two files, `_SUCCESS` and `part-r-00000`.</span></span> <span data-ttu-id="20892-126">El archivo `part-r-00000` contiene la salida de este trabajo.</span><span class="sxs-lookup"><span data-stu-id="20892-126">The `part-r-00000` file contains the output for this job.</span></span>

    > [!NOTE]
    > <span data-ttu-id="20892-127">Algunos trabajos de MapReduce pueden dividir los resultados entre varios archivos **part-r-####** .</span><span class="sxs-lookup"><span data-stu-id="20892-127">Some MapReduce jobs may split the results across multiple **part-r-#####** files.</span></span> <span data-ttu-id="20892-128">Si es así, utilice el sufijo #### para indicar el orden de los archivos.</span><span class="sxs-lookup"><span data-stu-id="20892-128">If so, use the ##### suffix to indicate the order of the files.</span></span>

4. <span data-ttu-id="20892-129">Para ver la salida, use el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="20892-129">To view the output, use the following command:</span></span>

    ```bash
    hdfs dfs -cat /example/data/WordCountOutput/part-r-00000
    ```

    <span data-ttu-id="20892-130">Este comando muestra una lista de las palabras contenidas en el archivo **wasb://example/data/gutenberg/davinci.txt**, junto con el número de veces que aparecía cada palabra.</span><span class="sxs-lookup"><span data-stu-id="20892-130">This command displays a list of the words that are contained in the **wasb://example/data/gutenberg/davinci.txt** file and the number of times each word occurred.</span></span> <span data-ttu-id="20892-131">El texto siguiente es un ejemplo de los datos contenidos en el archivo:</span><span class="sxs-lookup"><span data-stu-id="20892-131">The following text is an example of the data that is contained in the file:</span></span>

        wreathed        3
        wreathing       1
        wreaths         1
        wrecked         3
        wrenching       1
        wretched        6
        wriggling       1

## <span data-ttu-id="20892-132"><a id="summary"></a>Resumen</span><span class="sxs-lookup"><span data-stu-id="20892-132"><a id="summary"></a>Summary</span></span>

<span data-ttu-id="20892-133">Como se puede ver, los comando Hadoop proporcionan una manera fácil de ejecutar trabajos de MapReduce en un clúster de HDInsight y, a continuación, ver la salida del trabajo.</span><span class="sxs-lookup"><span data-stu-id="20892-133">As you can see, Hadoop commands provide an easy way to run MapReduce jobs in an HDInsight cluster and then view the job output.</span></span>

## <span data-ttu-id="20892-134"><a id="nextsteps"></a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="20892-134"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="20892-135">Para obtener información general sobre los trabajos de MapReduce en HDInsight:</span><span class="sxs-lookup"><span data-stu-id="20892-135">For general information about MapReduce jobs in HDInsight:</span></span>

* [<span data-ttu-id="20892-136">Uso de MapReduce en Hadoop de HDInsight</span><span class="sxs-lookup"><span data-stu-id="20892-136">Use MapReduce on HDInsight Hadoop</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="20892-137">Para obtener información sobre otras maneras de trabajar con Hadoop en HDInsight:</span><span class="sxs-lookup"><span data-stu-id="20892-137">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="20892-138">Uso de Hive con Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="20892-138">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="20892-139">Uso de Pig con Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="20892-139">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
