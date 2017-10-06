---
title: aaaMapReduce y el escritorio remoto con Hadoop en HDInsight - Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse escritorio remoto tooconnect tooHadoop en HDInsight y ejecución de los trabajos de MapReduce."
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
ms.openlocfilehash: bdbbcf59ca86dd1b170471aa9e12334a04c23667
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-mapreduce-in-hadoop-on-hdinsight-with-remote-desktop"></a><span data-ttu-id="1b29c-103">Uso de MapReduce de Hadoop en HDInsight con Escritorio remoto</span><span class="sxs-lookup"><span data-stu-id="1b29c-103">Use MapReduce in Hadoop on HDInsight with Remote Desktop</span></span>
[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

<span data-ttu-id="1b29c-104">En este artículo, se obtenga información acerca de cómo tooconnect tooa Hadoop en HDInsight de clúster mediante Escritorio remoto y, a continuación, ejecutar trabajos MapReduce mediante comandos de Hadoop de Hola.</span><span class="sxs-lookup"><span data-stu-id="1b29c-104">In this article, you will learn how tooconnect tooa Hadoop on HDInsight cluster by using Remote Desktop and then run MapReduce jobs by using hello Hadoop command.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1b29c-105">Escritorio remoto solo está disponible en los clústeres de HDInsight basados en Windows.</span><span class="sxs-lookup"><span data-stu-id="1b29c-105">Remote Desktop is only available on Windows-based HDInsight clusters.</span></span> <span data-ttu-id="1b29c-106">Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior.</span><span class="sxs-lookup"><span data-stu-id="1b29c-106">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="1b29c-107">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="1b29c-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="1b29c-108">Para HDInsight 3.4 o superior, consulte [MapReduce de uso mediante SSH](hdinsight-hadoop-use-mapreduce-ssh.md) para obtener información sobre cómo conectar el clúster de HDInsight toohello y ejecutar trabajos de MapReduce.</span><span class="sxs-lookup"><span data-stu-id="1b29c-108">For HDInsight 3.4 or greater, see [Use MapReduce with SSH](hdinsight-hadoop-use-mapreduce-ssh.md) for information on connecting toohello HDInsight cluster and running MapReduce jobs.</span></span>

## <span data-ttu-id="1b29c-109"><a id="prereq"></a>Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="1b29c-109"><a id="prereq"></a>Prerequisites</span></span>
<span data-ttu-id="1b29c-110">pasos de hello toocomplete en este artículo, se necesita Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="1b29c-110">toocomplete hello steps in this article, you will need hello following:</span></span>

* <span data-ttu-id="1b29c-111">Un clúster de HDInsight basado en Windows (Hadoop en HDInsight)</span><span class="sxs-lookup"><span data-stu-id="1b29c-111">A Windows-based HDInsight (Hadoop on HDInsight) cluster</span></span>
* <span data-ttu-id="1b29c-112">Un equipo cliente con Windows 10, Windows 8 o Windows 7</span><span class="sxs-lookup"><span data-stu-id="1b29c-112">A client computer running Windows 10, Windows 8, or Windows 7</span></span>

## <span data-ttu-id="1b29c-113"><a id="connect"></a>Conexión con el Escritorio remoto</span><span class="sxs-lookup"><span data-stu-id="1b29c-113"><a id="connect"></a>Connect with Remote Desktop</span></span>
<span data-ttu-id="1b29c-114">Habilitar Escritorio remoto para el clúster de HDInsight de Hola y conéctela tooit siguiendo las instrucciones de hello en [conectarse mediante RDP de clústeres de tooHDInsight](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span><span class="sxs-lookup"><span data-stu-id="1b29c-114">Enable Remote Desktop for hello HDInsight cluster, then connect tooit by following hello instructions at [Connect tooHDInsight clusters using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>

## <span data-ttu-id="1b29c-115"><a id="hadoop"></a>Usar comandos de Hadoop de Hola</span><span class="sxs-lookup"><span data-stu-id="1b29c-115"><a id="hadoop"></a>Use hello Hadoop command</span></span>
<span data-ttu-id="1b29c-116">Cuando haya conectado toohello escritorio para clúster de HDInsight de hello, use Hola después toorun pasos un trabajo de MapReduce con hello Hadoop comando:</span><span class="sxs-lookup"><span data-stu-id="1b29c-116">When you are connected toohello desktop for hello HDInsight cluster, use hello following steps toorun a MapReduce job by using hello Hadoop command:</span></span>

1. <span data-ttu-id="1b29c-117">Desde el escritorio de HDInsight de hello, inicie hello **línea de comandos de Hadoop**.</span><span class="sxs-lookup"><span data-stu-id="1b29c-117">From hello HDInsight desktop, start hello **Hadoop Command Line**.</span></span> <span data-ttu-id="1b29c-118">Se abre un nuevo símbolo en hello **c:\apps\dist\hadoop-&lt;número de versión >** directory.</span><span class="sxs-lookup"><span data-stu-id="1b29c-118">This opens a new command prompt in hello **c:\apps\dist\hadoop-&lt;version number>** directory.</span></span>

   > [!NOTE]
   > <span data-ttu-id="1b29c-119">número de versión de Hola cambia cuando se actualiza Hadoop.</span><span class="sxs-lookup"><span data-stu-id="1b29c-119">hello version number changes as Hadoop is updated.</span></span> <span data-ttu-id="1b29c-120">Hola **HADOOP_HOME** variable de entorno puede ser la ruta de acceso de toofind usado Hola.</span><span class="sxs-lookup"><span data-stu-id="1b29c-120">hello **HADOOP_HOME** environment variable can be used toofind hello path.</span></span> <span data-ttu-id="1b29c-121">Por ejemplo, `cd %HADOOP_HOME%` directorio de Hadoop en toohello de directorios de cambios, sin necesidad de número de versión de hello tooknow.</span><span class="sxs-lookup"><span data-stu-id="1b29c-121">For example, `cd %HADOOP_HOME%` changes directories toohello Hadoop directory, without requiring you tooknow hello version number.</span></span>
   >
   >
2. <span data-ttu-id="1b29c-122">Hola toouse **Hadoop** toorun un trabajo de MapReduce de ejemplo de comando, use Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="1b29c-122">toouse hello **Hadoop** command toorun an example MapReduce job, use hello following command:</span></span>

        hadoop jar hadoop-mapreduce-examples.jar wordcount wasb:///example/data/gutenberg/davinci.txt wasb:///example/data/WordCountOutput

    <span data-ttu-id="1b29c-123">Esto inicia hello **wordcount** (clase), que se encuentra en hello **archivo hadoop mapreduce examples.jar** archivo Hola de directorio actual.</span><span class="sxs-lookup"><span data-stu-id="1b29c-123">This starts hello **wordcount** class, which is contained in hello **hadoop-mapreduce-examples.jar** file in hello current directory.</span></span> <span data-ttu-id="1b29c-124">Como entrada, utiliza hello **wasb://example/data/gutenberg/davinci.txt** documento y la salida se almacena en: **wasb: / / / ejemplo/datos/WordCountOutput**.</span><span class="sxs-lookup"><span data-stu-id="1b29c-124">As input, it uses hello **wasb://example/data/gutenberg/davinci.txt** document, and output is stored at: **wasb:///example/data/WordCountOutput**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="1b29c-125">Para obtener más información acerca de estos datos de ejemplo de Hola y de trabajo de MapReduce, consulte <a href="hdinsight-use-mapreduce.md">uso MapReduce en Hadoop de HDInsight</a>.</span><span class="sxs-lookup"><span data-stu-id="1b29c-125">for more information about this MapReduce job and hello example data, see <a href="hdinsight-use-mapreduce.md">Use MapReduce in HDInsight Hadoop</a>.</span></span>
   >
   >
3. <span data-ttu-id="1b29c-126">trabajo de Hello emite detalles tal y como lo procesa y devuelve siguiente toohello similar de información cuando se complete el trabajo de hello:</span><span class="sxs-lookup"><span data-stu-id="1b29c-126">hello job emits details as it is processed, and it returns information similar toohello following when hello job is complete:</span></span>

        File Input Format Counters
        Bytes Read=1395666
        File Output Format Counters
        Bytes Written=337623
4. <span data-ttu-id="1b29c-127">Cuando se complete el trabajo de hello, usar hello después de archivos de salida de comando toolist Hola almacenados en **wasb://example/data/WordCountOutput**:</span><span class="sxs-lookup"><span data-stu-id="1b29c-127">When hello job is complete, use hello following command toolist hello output files stored at **wasb://example/data/WordCountOutput**:</span></span>

        hadoop fs -ls wasb:///example/data/WordCountOutput

    <span data-ttu-id="1b29c-128">Se deberían mostrar dos archivos, **_SUCCESS** y **part-r-00000**.</span><span class="sxs-lookup"><span data-stu-id="1b29c-128">This should display two files, **_SUCCESS** and **part-r-00000**.</span></span> <span data-ttu-id="1b29c-129">Hola **parte-r-00000** archivo contiene la salida de hello para este trabajo.</span><span class="sxs-lookup"><span data-stu-id="1b29c-129">hello **part-r-00000** file contains hello output for this job.</span></span>

   > [!NOTE]
   > <span data-ttu-id="1b29c-130">Pueden que algunos de estos trabajos MapReduce divida resultados Hola entre varios **parte-r-###** archivos.</span><span class="sxs-lookup"><span data-stu-id="1b29c-130">Some MapReduce jobs may split hello results across multiple **part-r-#####** files.</span></span> <span data-ttu-id="1b29c-131">Si es así, usar hello ### tooindicate Hola orden de los archivos de Hola de sufijos.</span><span class="sxs-lookup"><span data-stu-id="1b29c-131">If so, use hello ##### suffix tooindicate hello order of hello files.</span></span>
   >
   >
5. <span data-ttu-id="1b29c-132">salida de hello tooview, Hola de uso siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="1b29c-132">tooview hello output, use hello following command:</span></span>

        hadoop fs -cat wasb:///example/data/WordCountOutput/part-r-00000

    <span data-ttu-id="1b29c-133">Esto muestra una lista de palabras de Hola que figuran en hello **wasb://example/data/gutenberg/davinci.txt** archivo, junto con el número de Hola de veces que se produjo cada palabra.</span><span class="sxs-lookup"><span data-stu-id="1b29c-133">This displays a list of hello words that are contained in hello **wasb://example/data/gutenberg/davinci.txt** file, along with hello number of times each word occured.</span></span> <span data-ttu-id="1b29c-134">Hola te mostramos un ejemplo de Hola datos que se incluirán en el archivo hello:</span><span class="sxs-lookup"><span data-stu-id="1b29c-134">hello following is an example of hello data that will be contained in hello file:</span></span>

        wreathed        3
        wreathing       1
        wreaths         1
        wrecked         3
        wrenching       1
        wretched        6
        wriggling       1

## <span data-ttu-id="1b29c-135"><a id="summary"></a>Resumen</span><span class="sxs-lookup"><span data-stu-id="1b29c-135"><a id="summary"></a>Summary</span></span>
<span data-ttu-id="1b29c-136">Como puede ver, hello Hadoop comando proporciona una toorun fácilmente trabajos MapReduce en un clúster de HDInsight y, a continuación, ver la salida de trabajo Hola.</span><span class="sxs-lookup"><span data-stu-id="1b29c-136">As you can see, hello Hadoop command provides an easy way toorun MapReduce jobs on an HDInsight cluster and then view hello job output.</span></span>

## <span data-ttu-id="1b29c-137"><a id="nextsteps"></a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1b29c-137"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="1b29c-138">Para obtener información general sobre los trabajos de MapReduce en HDInsight:</span><span class="sxs-lookup"><span data-stu-id="1b29c-138">For general information about MapReduce jobs in HDInsight:</span></span>

* [<span data-ttu-id="1b29c-139">Uso de MapReduce en Hadoop de HDInsight</span><span class="sxs-lookup"><span data-stu-id="1b29c-139">Use MapReduce on HDInsight Hadoop</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="1b29c-140">Para obtener información sobre otras maneras de trabajar con Hadoop en HDInsight:</span><span class="sxs-lookup"><span data-stu-id="1b29c-140">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="1b29c-141">Uso de Hive con Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="1b29c-141">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="1b29c-142">Uso de Pig con Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="1b29c-142">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
