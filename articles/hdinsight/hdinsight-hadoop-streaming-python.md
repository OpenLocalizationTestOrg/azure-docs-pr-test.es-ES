---
title: los trabajos de MapReduce de streaming de Python aaaDevelop con HDInsight - Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse Python en los trabajos MapReduce de streaming. Hadoop proporciona una API de streaming para MapReduce para escribir en lenguajes diferentes de Java."
services: hdinsight
keyword: mapreduce python,python map reduce,python mapreduce
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 7631d8d9-98ae-42ec-b9ec-ee3cf7e57fb3
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: a6ae3ba650b665ecc5839a4ddf5282f8ccfb6bd6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="develop-python-streaming-mapreduce-programs-for-hdinsight"></a><span data-ttu-id="737a9-104">Desarrollo de programas de MapReduce de streaming de Python para HDInsight</span><span class="sxs-lookup"><span data-stu-id="737a9-104">Develop Python streaming MapReduce programs for HDInsight</span></span>

<span data-ttu-id="737a9-105">Obtenga información acerca de cómo toouse Python en operaciones de MapReduce de streaming.</span><span class="sxs-lookup"><span data-stu-id="737a9-105">Learn how toouse Python in streaming MapReduce operations.</span></span> <span data-ttu-id="737a9-106">Hadoop proporciona una API de transmisión por secuencias para MapReduce que permite asignar toowrite y reduce las funciones en lenguajes distintos de Java.</span><span class="sxs-lookup"><span data-stu-id="737a9-106">Hadoop provides a streaming API for MapReduce that enables you toowrite map and reduce functions in languages other than Java.</span></span> <span data-ttu-id="737a9-107">Hello pasos de este documento implementan Hola mapa y reducen los componentes de Python.</span><span class="sxs-lookup"><span data-stu-id="737a9-107">hello steps in this document implement hello Map and Reduce components in Python.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="737a9-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="737a9-108">Prerequisites</span></span>

* <span data-ttu-id="737a9-109">Un clúster de Hadoop en HDInsight basado en Linux</span><span class="sxs-lookup"><span data-stu-id="737a9-109">A Linux-based Hadoop on HDInsight cluster</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="737a9-110">pasos de Hello en este documento requieren un clúster de HDInsight que usa Linux.</span><span class="sxs-lookup"><span data-stu-id="737a9-110">hello steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="737a9-111">Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior.</span><span class="sxs-lookup"><span data-stu-id="737a9-111">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="737a9-112">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="737a9-112">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="737a9-113">Un editor de texto</span><span class="sxs-lookup"><span data-stu-id="737a9-113">A text editor</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="737a9-114">editor de texto Hello debe utilizar LF como final de la línea de saludo.</span><span class="sxs-lookup"><span data-stu-id="737a9-114">hello text editor must use LF as hello line ending.</span></span> <span data-ttu-id="737a9-115">Usar un final de línea de CRLF produce errores cuando se ejecuta el trabajo de MapReduce de hello en clústeres de HDInsight basados en Linux.</span><span class="sxs-lookup"><span data-stu-id="737a9-115">Using a line ending of CRLF causes errors when running hello MapReduce job on Linux-based HDInsight clusters.</span></span>

* <span data-ttu-id="737a9-116">Hola `ssh` y `scp` comandos, o [PowerShell de Azure](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-3.8.0)</span><span class="sxs-lookup"><span data-stu-id="737a9-116">hello `ssh` and `scp` commands, or [Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-3.8.0)</span></span>

## <a name="word-count"></a><span data-ttu-id="737a9-117">Recuento de palabras</span><span class="sxs-lookup"><span data-stu-id="737a9-117">Word count</span></span>

<span data-ttu-id="737a9-118">Este ejemplo es un recuento de palabras básico implementado en un asignador y reductor de Python.</span><span class="sxs-lookup"><span data-stu-id="737a9-118">This example is a basic word count implemented in a python a mapper and reducer.</span></span> <span data-ttu-id="737a9-119">el asignador de Hello divide las oraciones en palabras individuales y reductor Hola agrega palabras hello y recuentos de salida de hello tooproduce.</span><span class="sxs-lookup"><span data-stu-id="737a9-119">hello mapper breaks sentences into individual words, and hello reducer aggregates hello words and counts tooproduce hello output.</span></span>

<span data-ttu-id="737a9-120">Hola después de diagrama de flujo muestra lo que sucede durante la asignación de Hola y reducir las fases.</span><span class="sxs-lookup"><span data-stu-id="737a9-120">hello following flowchart illustrates what happens during hello map and reduce phases.</span></span>

![ilustración del proceso de mapreduce Hola](./media/hdinsight-hadoop-streaming-python/HDI.WordCountDiagram.png)

## <a name="streaming-mapreduce"></a><span data-ttu-id="737a9-122">Transmisión de MapReduce</span><span class="sxs-lookup"><span data-stu-id="737a9-122">Streaming MapReduce</span></span>

<span data-ttu-id="737a9-123">Hadoop le permite toospecify un archivo que contiene el mapa de Hola y reduce la lógica que se utiliza un trabajo.</span><span class="sxs-lookup"><span data-stu-id="737a9-123">Hadoop allows you toospecify a file that contains hello map and reduce logic that is used by a job.</span></span> <span data-ttu-id="737a9-124">requisitos específicos de Hola para Hola de asignación y reducción lógica son:</span><span class="sxs-lookup"><span data-stu-id="737a9-124">hello specific requirements for hello map and reduce logic are:</span></span>

* <span data-ttu-id="737a9-125">**Entrada**: Hola mapa y reducir los componentes deben leer datos de entrada desde STDIN.</span><span class="sxs-lookup"><span data-stu-id="737a9-125">**Input**: hello map and reduce components must read input data from STDIN.</span></span>
* <span data-ttu-id="737a9-126">**Salida**: Hola mapa y reducir componentes deben escribir tooSTDOUT de datos de salida.</span><span class="sxs-lookup"><span data-stu-id="737a9-126">**Output**: hello map and reduce components must write output data tooSTDOUT.</span></span>
* <span data-ttu-id="737a9-127">**Formato de datos**: datos de hello consumido y generan deben ser un par de clave/valor, separado por un carácter de tabulación.</span><span class="sxs-lookup"><span data-stu-id="737a9-127">**Data format**: hello data consumed and produced must be a key/value pair, separated by a tab character.</span></span>

<span data-ttu-id="737a9-128">Python puede controlar fácilmente estos requisitos mediante hello `sys` tooread módulo STDIN y utilizar `print` tooprint tooSTDOUT.</span><span class="sxs-lookup"><span data-stu-id="737a9-128">Python can easily handle these requirements by using hello `sys` module tooread from STDIN and using `print` tooprint tooSTDOUT.</span></span> <span data-ttu-id="737a9-129">Hello tarea restante es simplemente aplicar formato a Hola datos con una pestaña (`\t`) carácter entre Hola clave y valor.</span><span class="sxs-lookup"><span data-stu-id="737a9-129">hello remaining task is simply formatting hello data with a tab (`\t`) character between hello key and value.</span></span>

## <a name="create-hello-mapper-and-reducer"></a><span data-ttu-id="737a9-130">Crear reductor y el asignador de Hola</span><span class="sxs-lookup"><span data-stu-id="737a9-130">Create hello mapper and reducer</span></span>

1. <span data-ttu-id="737a9-131">Cree un archivo denominado `mapper.py` y use Hola siguiendo código como contenido de hello:</span><span class="sxs-lookup"><span data-stu-id="737a9-131">Create a file named `mapper.py` and use hello following code as hello content:</span></span>

   ```python
   #!/usr/bin/env python

   # Use hello sys module
   import sys

   # 'file' in this case is STDIN
   def read_input(file):
       # Split each line into words
       for line in file:
           yield line.split()

   def main(separator='\t'):
       # Read hello data using read_input
       data = read_input(sys.stdin)
       # Process each word returned from read_input
       for words in data:
           # Process each word
           for word in words:
               # Write tooSTDOUT
               print '%s%s%d' % (word, separator, 1)

   if __name__ == "__main__":
       main()
   ```

2. <span data-ttu-id="737a9-132">Cree un archivo denominado **reducer.py** y use Hola siguiendo código como contenido de hello:</span><span class="sxs-lookup"><span data-stu-id="737a9-132">Create a file named **reducer.py** and use hello following code as hello content:</span></span>

   ```python
   #!/usr/bin/env python

   # import modules
   from itertools import groupby
   from operator import itemgetter
   import sys

   # 'file' in this case is STDIN
   def read_mapper_output(file, separator='\t'):
       # Go through each line
       for line in file:
           # Strip out hello separator character
           yield line.rstrip().split(separator, 1)

   def main(separator='\t'):
       # Read hello data using read_mapper_output
       data = read_mapper_output(sys.stdin, separator=separator)
       # Group words and counts into 'group'
       #   Since MapReduce is a distributed process, each word
       #   may have multiple counts. 'group' will have all counts
       #   which can be retrieved using hello word as hello key.
       for current_word, group in groupby(data, itemgetter(0)):
           try:
               # For each word, pull hello count(s) for hello word
               #   from 'group' and create a total count
               total_count = sum(int(count) for current_word, count in group)
               # Write toostdout
               print "%s%s%d" % (current_word, separator, total_count)
           except ValueError:
               # Count was not a number, so do nothing
               pass

   if __name__ == "__main__":
       main()
   ```

## <a name="run-using-powershell"></a><span data-ttu-id="737a9-133">Ejecución con PowerShell</span><span class="sxs-lookup"><span data-stu-id="737a9-133">Run using PowerShell</span></span>

<span data-ttu-id="737a9-134">tooensure que los archivos tienen finales de línea derecho de hello, Hola de uso siguiente script de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="737a9-134">tooensure that your files have hello right line endings, use hello following PowerShell script:</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/streaming-python/streaming-python.ps1?range=138-140)]

<span data-ttu-id="737a9-135">Usar hello siguientes PowerShell script tooupload Hola archivos, ejecutar trabajo de Hola y ver el resultado de hello:</span><span class="sxs-lookup"><span data-stu-id="737a9-135">Use hello following PowerShell script tooupload hello files, run hello job, and view hello output:</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/streaming-python/streaming-python.ps1?range=5-134)]

## <a name="run-from-an-ssh-session"></a><span data-ttu-id="737a9-136">Ejecución desde una sesión de SSH</span><span class="sxs-lookup"><span data-stu-id="737a9-136">Run from an SSH session</span></span>

1. <span data-ttu-id="737a9-137">Desde el entorno de desarrollo, en Hola mismo directorio como `mapper.py` y `reducer.py` archivos, usar hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="737a9-137">From your development environment, in hello same directory as `mapper.py` and `reducer.py` files, use hello following command:</span></span>

    ```bash
    scp mapper.py reducer.py username@clustername-ssh.azurehdinsight.net:
    ```

    <span data-ttu-id="737a9-138">Reemplace `username` con el nombre de usuario SSH de hello para el clúster, y `clustername` con nombre hello del clúster.</span><span class="sxs-lookup"><span data-stu-id="737a9-138">Replace `username` with hello SSH user name for your cluster, and `clustername` with hello name of your cluster.</span></span>

    <span data-ttu-id="737a9-139">Este comando copia los archivos de Hola desde el nodo principal de hello sistema local toohello.</span><span class="sxs-lookup"><span data-stu-id="737a9-139">This command copies hello files from hello local system toohello head node.</span></span>

    > [!NOTE]
    > <span data-ttu-id="737a9-140">Si utiliza un toosecure de contraseña de su cuenta SSH, le pediremos contraseña Hola.</span><span class="sxs-lookup"><span data-stu-id="737a9-140">If you used a password toosecure your SSH account, you are prompted for hello password.</span></span> <span data-ttu-id="737a9-141">Si usa una clave SSH, habrá hello toouse `-i` hello y parámetro de clave privada de toohello de ruta de acceso.</span><span class="sxs-lookup"><span data-stu-id="737a9-141">If you used an SSH key, you may have toouse hello `-i` parameter and hello path toohello private key.</span></span> <span data-ttu-id="737a9-142">Por ejemplo: `scp -i /path/to/private/key mapper.py reducer.py username@clustername-ssh.azurehdinsight.net:`.</span><span class="sxs-lookup"><span data-stu-id="737a9-142">For example, `scp -i /path/to/private/key mapper.py reducer.py username@clustername-ssh.azurehdinsight.net:`.</span></span>

2. <span data-ttu-id="737a9-143">Conectar toohello clúster a través de SSH:</span><span class="sxs-lookup"><span data-stu-id="737a9-143">Connect toohello cluster by using SSH:</span></span>

    ```bash
    ssh username@clustername-ssh.azurehdinsight.net`
    ```

    <span data-ttu-id="737a9-144">Para más información, consulte [Uso de SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="737a9-144">For more information on, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

3. <span data-ttu-id="737a9-145">REDUCER.py y tooensure hello mapper.py que Hola corregir finales de línea, siga Hola siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="737a9-145">tooensure hello mapper.py and reducer.py have hello correct line endings, use hello following commands:</span></span>

    ```bash
    perl -pi -e 's/\r\n/\n/g' mapper.py
    perl -pi -e 's/\r\n/\n/g' reducer.py
    ```

4. <span data-ttu-id="737a9-146">Usar hello siguiendo el trabajo de MapReduce de comando toostart Hola.</span><span class="sxs-lookup"><span data-stu-id="737a9-146">Use hello following command toostart hello MapReduce job.</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar -files mapper.py,reducer.py -mapper mapper.py -reducer reducer.py -input /example/data/gutenberg/davinci.txt -output /example/wordcountout
    ```

    <span data-ttu-id="737a9-147">Este comando tiene Hola siguientes componentes:</span><span class="sxs-lookup"><span data-stu-id="737a9-147">This command has hello following parts:</span></span>

   * <span data-ttu-id="737a9-148">**hadoop-streaming.jar**: se usa cuando se realizan operaciones de streaming de MapReduce.</span><span class="sxs-lookup"><span data-stu-id="737a9-148">**hadoop-streaming.jar**: Used when performing streaming MapReduce operations.</span></span> <span data-ttu-id="737a9-149">Interfaces de Hadoop con código de hello externo MapReduce que proporcionan.</span><span class="sxs-lookup"><span data-stu-id="737a9-149">It interfaces Hadoop with hello external MapReduce code you provide.</span></span>

   * <span data-ttu-id="737a9-150">**-archivos**: Hola especificado se agrega trabajo de MapReduce toohello de archivos.</span><span class="sxs-lookup"><span data-stu-id="737a9-150">**-files**: Adds hello specified files toohello MapReduce job.</span></span>

   * <span data-ttu-id="737a9-151">**-el asignador**: Hadoop indica que el archivo toouse Hola asignador.</span><span class="sxs-lookup"><span data-stu-id="737a9-151">**-mapper**: Tells Hadoop which file toouse as hello mapper.</span></span>

   * <span data-ttu-id="737a9-152">**-reductor**: Hadoop indica que el archivo toouse Hola reductor.</span><span class="sxs-lookup"><span data-stu-id="737a9-152">**-reducer**: Tells Hadoop which file toouse as hello reducer.</span></span>

   * <span data-ttu-id="737a9-153">**-entrada**: archivo de entrada de Hola que se debe contar palabras desde.</span><span class="sxs-lookup"><span data-stu-id="737a9-153">**-input**: hello input file that we should count words from.</span></span>

   * <span data-ttu-id="737a9-154">**-salida**: se escribió en el directorio de Hola que Hola de salida.</span><span class="sxs-lookup"><span data-stu-id="737a9-154">**-output**: hello directory that hello output is written to.</span></span>

    <span data-ttu-id="737a9-155">A medida que trabaja el trabajo de MapReduce hello, proceso de Hola se muestra como porcentajes.</span><span class="sxs-lookup"><span data-stu-id="737a9-155">As hello MapReduce job works, hello process is displayed as percentages.</span></span>

        <span data-ttu-id="737a9-156">15/02/05 19:01:04 INFO mapreduce.Job:  map 0% reduce 0%    15/02/05 19:01:16 INFO mapreduce.Job:  map 100% reduce 0%    15/02/05 19:01:27 INFO mapreduce.Job:  map 100% reduce 100%</span><span class="sxs-lookup"><span data-stu-id="737a9-156">15/02/05 19:01:04 INFO mapreduce.Job:  map 0% reduce 0%    15/02/05 19:01:16 INFO mapreduce.Job:  map 100% reduce 0%    15/02/05 19:01:27 INFO mapreduce.Job:  map 100% reduce 100%</span></span>


5. <span data-ttu-id="737a9-157">salida de hello tooview, Hola de uso siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="737a9-157">tooview hello output, use hello following command:</span></span>

    ```bash
    hdfs dfs -text /example/wordcountout/part-00000
    ```

    <span data-ttu-id="737a9-158">Este comando muestra una lista de palabras y el número de veces palabra Hola se ha producido.</span><span class="sxs-lookup"><span data-stu-id="737a9-158">This command displays a list of words and how many times hello word occurred.</span></span>

## <a name="next-steps"></a><span data-ttu-id="737a9-159">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="737a9-159">Next steps</span></span>

<span data-ttu-id="737a9-160">Ahora que ha aprendido cómo los trabajos de toouse MapRedcue de transmisión por secuencias con HDInsight, utilice Hola siguiendo vínculos tooexplore otro toowork maneras con HDInsight de Azure.</span><span class="sxs-lookup"><span data-stu-id="737a9-160">Now that you have learned how toouse streaming MapRedcue jobs with HDInsight, use hello following links tooexplore other ways toowork with Azure HDInsight.</span></span>

* [<span data-ttu-id="737a9-161">Uso de Hive con HDInsight</span><span class="sxs-lookup"><span data-stu-id="737a9-161">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="737a9-162">Uso de Pig con HDInsight</span><span class="sxs-lookup"><span data-stu-id="737a9-162">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="737a9-163">Uso de trabajos de MapReduce con HDInsight</span><span class="sxs-lookup"><span data-stu-id="737a9-163">Use MapReduce jobs with HDInsight</span></span>](hdinsight-use-mapreduce.md)
