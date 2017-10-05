---
title: MapReduce y Escritorio remoto con Hadoop en HDInsight (Azure) | Microsoft Docs
description: "Obtenga información acerca de cómo usar Escritorio remoto para conectarse a Hadoop en HDInsight y ejecutar trabajos de MapReduce."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 9d3a7b34-7def-4c2e-bb6c-52682d30dee8
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/12/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: b56674857b013f9bb3d4dd4b6e97b34e0a97b1b2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="use-mapreduce-in-hadoop-on-hdinsight-with-remote-desktop"></a><span data-ttu-id="78746-103">Uso de MapReduce de Hadoop en HDInsight con Escritorio remoto</span><span class="sxs-lookup"><span data-stu-id="78746-103">Use MapReduce in Hadoop on HDInsight with Remote Desktop</span></span>
[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

<span data-ttu-id="78746-104">En este artículo, obtendrá información sobre cómo conectarse a un clúster de Hadoop en HDInsight mediante Escritorio remoto y, a continuación, ejecutar trabajos de MapReduce mediante el comando de Hadoop.</span><span class="sxs-lookup"><span data-stu-id="78746-104">In this article, you will learn how to connect to a Hadoop on HDInsight cluster by using Remote Desktop and then run MapReduce jobs by using the Hadoop command.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="78746-105">Escritorio remoto solo está disponible en los clústeres de HDInsight basados en Windows.</span><span class="sxs-lookup"><span data-stu-id="78746-105">Remote Desktop is only available on Windows-based HDInsight clusters.</span></span> <span data-ttu-id="78746-106">Linux es el único sistema operativo que se usa en la versión 3.4 de HDInsight, o en las superiores.</span><span class="sxs-lookup"><span data-stu-id="78746-106">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="78746-107">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="78746-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="78746-108">Para HDInsight 3.4 o superior, consulte [Uso de MapReduce con SSH](hdinsight-hadoop-use-mapreduce-ssh.md) para más información sobre cómo conectarse al clúster de HDInsight y ejecutar trabajos de MapReduce.</span><span class="sxs-lookup"><span data-stu-id="78746-108">For HDInsight 3.4 or greater, see [Use MapReduce with SSH](hdinsight-hadoop-use-mapreduce-ssh.md) for information on connecting to the HDInsight cluster and running MapReduce jobs.</span></span>

## <span data-ttu-id="78746-109"><a id="prereq"></a>Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="78746-109"><a id="prereq"></a>Prerequisites</span></span>
<span data-ttu-id="78746-110">Para completar los pasos de este artículo, necesitará lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="78746-110">To complete the steps in this article, you will need the following:</span></span>

* <span data-ttu-id="78746-111">Un clúster de HDInsight basado en Windows (Hadoop en HDInsight)</span><span class="sxs-lookup"><span data-stu-id="78746-111">A Windows-based HDInsight (Hadoop on HDInsight) cluster</span></span>
* <span data-ttu-id="78746-112">Un equipo cliente con Windows 10, Windows 8 o Windows 7</span><span class="sxs-lookup"><span data-stu-id="78746-112">A client computer running Windows 10, Windows 8, or Windows 7</span></span>

## <span data-ttu-id="78746-113"><a id="connect"></a>Conexión con el Escritorio remoto</span><span class="sxs-lookup"><span data-stu-id="78746-113"><a id="connect"></a>Connect with Remote Desktop</span></span>
<span data-ttu-id="78746-114">Habilite el Escritorio remoto para el clúster de HDInsight y conéctese a él siguiendo las instrucciones dadas en [Conexión a los clústeres de HDInsight con RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span><span class="sxs-lookup"><span data-stu-id="78746-114">Enable Remote Desktop for the HDInsight cluster, then connect to it by following the instructions at [Connect to HDInsight clusters using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>

## <span data-ttu-id="78746-115"><a id="hadoop"></a>Uso del comando Hadoop</span><span class="sxs-lookup"><span data-stu-id="78746-115"><a id="hadoop"></a>Use the Hadoop command</span></span>
<span data-ttu-id="78746-116">Una vez conectado al escritorio para el clúster de HDInsight, siga estos pasos para ejecutar un trabajo de MapReduce mediante el comando de Hadoop:</span><span class="sxs-lookup"><span data-stu-id="78746-116">When you are connected to the desktop for the HDInsight cluster, use the following steps to run a MapReduce job by using the Hadoop command:</span></span>

1. <span data-ttu-id="78746-117">Desde el escritorio de HDInsight, inicie la **línea de comandos de Hadoop**.</span><span class="sxs-lookup"><span data-stu-id="78746-117">From the HDInsight desktop, start the **Hadoop Command Line**.</span></span> <span data-ttu-id="78746-118">Se abrirá un nuevo símbolo del sistema en el directorio **c:\apps\dist\hadoop-&lt;número de versión>**.</span><span class="sxs-lookup"><span data-stu-id="78746-118">This opens a new command prompt in the **c:\apps\dist\hadoop-&lt;version number>** directory.</span></span>

   > [!NOTE]
   > <span data-ttu-id="78746-119">El número de versión cambia cuando se actualiza Hadoop.</span><span class="sxs-lookup"><span data-stu-id="78746-119">The version number changes as Hadoop is updated.</span></span> <span data-ttu-id="78746-120">La variable de entorno **HADOOP_HOME** puede usarse para encontrar la ruta de acceso.</span><span class="sxs-lookup"><span data-stu-id="78746-120">The **HADOOP_HOME** environment variable can be used to find the path.</span></span> <span data-ttu-id="78746-121">Por ejemplo, `cd %HADOOP_HOME%` cambiará los directorios al directorio de Hadoop, sin que sea necesario conocer el número de versión.</span><span class="sxs-lookup"><span data-stu-id="78746-121">For example, `cd %HADOOP_HOME%` changes directories to the Hadoop directory, without requiring you to know the version number.</span></span>
   >
   >
2. <span data-ttu-id="78746-122">Para usar el comando de **Hadoop** para ejecutar un trabajo de MapReduce de ejemplo, utilice el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="78746-122">To use the **Hadoop** command to run an example MapReduce job, use the following command:</span></span>

        hadoop jar hadoop-mapreduce-examples.jar wordcount wasb:///example/data/gutenberg/davinci.txt wasb:///example/data/WordCountOutput

    <span data-ttu-id="78746-123">Se inicia la clase **wordcount**, incluida en el archivo **hadoop-mapreduce-examples.jar** del directorio actual.</span><span class="sxs-lookup"><span data-stu-id="78746-123">This starts the **wordcount** class, which is contained in the **hadoop-mapreduce-examples.jar** file in the current directory.</span></span> <span data-ttu-id="78746-124">Como entrada, usa el documento **wasb://example/data/gutenberg/davinci.txt** y la salida se almacena en **wasb:///ejemplo/data/WordCountOutput**.</span><span class="sxs-lookup"><span data-stu-id="78746-124">As input, it uses the **wasb://example/data/gutenberg/davinci.txt** document, and output is stored at: **wasb:///example/data/WordCountOutput**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="78746-125">Para obtener más información acerca de este trabajo de MapReduce y los datos de ejemplo, consulte <a href="hdinsight-use-mapreduce.md">Uso de MapReduce en Hadoop de HDInsight</a>.</span><span class="sxs-lookup"><span data-stu-id="78746-125">for more information about this MapReduce job and the example data, see <a href="hdinsight-use-mapreduce.md">Use MapReduce in HDInsight Hadoop</a>.</span></span>
   >
   >
3. <span data-ttu-id="78746-126">El trabajo emite detalles cuando se procesa y devuelve información similar a la siguiente cuando finaliza el trabajo:</span><span class="sxs-lookup"><span data-stu-id="78746-126">The job emits details as it is processed, and it returns information similar to the following when the job is complete:</span></span>

        File Input Format Counters
        Bytes Read=1395666
        File Output Format Counters
        Bytes Written=337623
4. <span data-ttu-id="78746-127">Una vez completado, use el comando siguiente para enumerar los archivos de salida almacenados en **wasb://example/data/WordCountOutput**:</span><span class="sxs-lookup"><span data-stu-id="78746-127">When the job is complete, use the following command to list the output files stored at **wasb://example/data/WordCountOutput**:</span></span>

        hadoop fs -ls wasb:///example/data/WordCountOutput

    <span data-ttu-id="78746-128">Se deberían mostrar dos archivos, **_SUCCESS** y **part-r-00000**.</span><span class="sxs-lookup"><span data-stu-id="78746-128">This should display two files, **_SUCCESS** and **part-r-00000**.</span></span> <span data-ttu-id="78746-129">El archivo **part-r-00000** contiene la salida de este trabajo.</span><span class="sxs-lookup"><span data-stu-id="78746-129">The **part-r-00000** file contains the output for this job.</span></span>

   > [!NOTE]
   > <span data-ttu-id="78746-130">Algunos trabajos de MapReduce pueden dividir los resultados entre varios archivos **part-r-####** .</span><span class="sxs-lookup"><span data-stu-id="78746-130">Some MapReduce jobs may split the results across multiple **part-r-#####** files.</span></span> <span data-ttu-id="78746-131">Si es así, utilice el sufijo #### para indicar el orden de los archivos.</span><span class="sxs-lookup"><span data-stu-id="78746-131">If so, use the ##### suffix to indicate the order of the files.</span></span>
   >
   >
5. <span data-ttu-id="78746-132">Para ver la salida, use el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="78746-132">To view the output, use the following command:</span></span>

        hadoop fs -cat wasb:///example/data/WordCountOutput/part-r-00000

    <span data-ttu-id="78746-133">Se mostrará una lista de las palabras contenidas en el archivo **wasb://example/data/gutenberg/davinci.txt**, junto con el número de veces que aparecía cada palabra.</span><span class="sxs-lookup"><span data-stu-id="78746-133">This displays a list of the words that are contained in the **wasb://example/data/gutenberg/davinci.txt** file, along with the number of times each word occured.</span></span> <span data-ttu-id="78746-134">El siguiente es un ejemplo de los datos que estarán contenidos en el archivo:</span><span class="sxs-lookup"><span data-stu-id="78746-134">The following is an example of the data that will be contained in the file:</span></span>

        wreathed        3
        wreathing       1
        wreaths         1
        wrecked         3
        wrenching       1
        wretched        6
        wriggling       1

## <span data-ttu-id="78746-135"><a id="summary"></a>Resumen</span><span class="sxs-lookup"><span data-stu-id="78746-135"><a id="summary"></a>Summary</span></span>
<span data-ttu-id="78746-136">Como se puede ver, el comando de Hadoop proporciona una manera fácil de ejecutar trabajos de MapReduce en un clúster de HDInsight y, a continuación, ver la salida del trabajo.</span><span class="sxs-lookup"><span data-stu-id="78746-136">As you can see, the Hadoop command provides an easy way to run MapReduce jobs on an HDInsight cluster and then view the job output.</span></span>

## <span data-ttu-id="78746-137"><a id="nextsteps"></a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="78746-137"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="78746-138">Para obtener información general sobre los trabajos de MapReduce en HDInsight:</span><span class="sxs-lookup"><span data-stu-id="78746-138">For general information about MapReduce jobs in HDInsight:</span></span>

* [<span data-ttu-id="78746-139">Uso de MapReduce en Hadoop de HDInsight</span><span class="sxs-lookup"><span data-stu-id="78746-139">Use MapReduce on HDInsight Hadoop</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="78746-140">Para obtener información sobre otras maneras de trabajar con Hadoop en HDInsight:</span><span class="sxs-lookup"><span data-stu-id="78746-140">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="78746-141">Uso de Hive con Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="78746-141">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="78746-142">Uso de Pig con Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="78746-142">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
