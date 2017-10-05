---
title: 'Desarrollo de trabajos de MapReduce de streaming de Python con HDInsight: Azure | Microsoft Docs'
description: Aprenda a usar Python en trabajos de MapReduce de streaming. Hadoop proporciona una API de streaming para MapReduce para escribir en lenguajes diferentes de Java.
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
ms.openlocfilehash: b86605c49291a99f49c4b2841d46324cfd0db56d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="develop-python-streaming-mapreduce-programs-for-hdinsight"></a><span data-ttu-id="cb155-104">Desarrollo de programas de MapReduce de streaming de Python para HDInsight</span><span class="sxs-lookup"><span data-stu-id="cb155-104">Develop Python streaming MapReduce programs for HDInsight</span></span>

<span data-ttu-id="cb155-105">Aprenda a usar Python en operaciones de MapReduce de streaming.</span><span class="sxs-lookup"><span data-stu-id="cb155-105">Learn how to use Python in streaming MapReduce operations.</span></span> <span data-ttu-id="cb155-106">Hadoop proporciona una API de streaming para MapReduce que le permite escribir mapas y reducir funciones en lenguajes distintos de Java.</span><span class="sxs-lookup"><span data-stu-id="cb155-106">Hadoop provides a streaming API for MapReduce that enables you to write map and reduce functions in languages other than Java.</span></span> <span data-ttu-id="cb155-107">Los pasos descritos en este documento implementan los componentes de asignación y reducción de Python.</span><span class="sxs-lookup"><span data-stu-id="cb155-107">The steps in this document implement the Map and Reduce components in Python.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cb155-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="cb155-108">Prerequisites</span></span>

* <span data-ttu-id="cb155-109">Un clúster de Hadoop en HDInsight basado en Linux</span><span class="sxs-lookup"><span data-stu-id="cb155-109">A Linux-based Hadoop on HDInsight cluster</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="cb155-110">Los pasos descritos en este documento requieren un clúster de HDInsight que use Linux.</span><span class="sxs-lookup"><span data-stu-id="cb155-110">The steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="cb155-111">Linux es el único sistema operativo que se usa en la versión 3.4 de HDInsight, o en las superiores.</span><span class="sxs-lookup"><span data-stu-id="cb155-111">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="cb155-112">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="cb155-112">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="cb155-113">Un editor de texto</span><span class="sxs-lookup"><span data-stu-id="cb155-113">A text editor</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="cb155-114">El editor de texto debe usar LF como final de línea.</span><span class="sxs-lookup"><span data-stu-id="cb155-114">The text editor must use LF as the line ending.</span></span> <span data-ttu-id="cb155-115">El uso de un final de línea de CRLF provoca errores al ejecutar el trabajo de MapReduce en clústeres de HDInsight basados en Linux.</span><span class="sxs-lookup"><span data-stu-id="cb155-115">Using a line ending of CRLF causes errors when running the MapReduce job on Linux-based HDInsight clusters.</span></span>

* <span data-ttu-id="cb155-116">Los comandos `ssh` y `scp` o [Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-3.8.0)</span><span class="sxs-lookup"><span data-stu-id="cb155-116">The `ssh` and `scp` commands, or [Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-3.8.0)</span></span>

## <a name="word-count"></a><span data-ttu-id="cb155-117">Recuento de palabras</span><span class="sxs-lookup"><span data-stu-id="cb155-117">Word count</span></span>

<span data-ttu-id="cb155-118">Este ejemplo es un recuento de palabras básico implementado en un asignador y reductor de Python.</span><span class="sxs-lookup"><span data-stu-id="cb155-118">This example is a basic word count implemented in a python a mapper and reducer.</span></span> <span data-ttu-id="cb155-119">El asignador divide las oraciones en palabras individuales y el reductor agrega las palabras y los recuentos para generar la salida.</span><span class="sxs-lookup"><span data-stu-id="cb155-119">The mapper breaks sentences into individual words, and the reducer aggregates the words and counts to produce the output.</span></span>

<span data-ttu-id="cb155-120">El siguiente diagrama de flujo ilustra lo que sucede durante las fases de asignación y reducción.</span><span class="sxs-lookup"><span data-stu-id="cb155-120">The following flowchart illustrates what happens during the map and reduce phases.</span></span>

![Ilustración del proceso de MapReduce](./media/hdinsight-hadoop-streaming-python/HDI.WordCountDiagram.png)

## <a name="streaming-mapreduce"></a><span data-ttu-id="cb155-122">Transmisión de MapReduce</span><span class="sxs-lookup"><span data-stu-id="cb155-122">Streaming MapReduce</span></span>

<span data-ttu-id="cb155-123">Hadoop le permite especificar un archivo que contiene la lógica de asignación y reducción que usa un trabajo.</span><span class="sxs-lookup"><span data-stu-id="cb155-123">Hadoop allows you to specify a file that contains the map and reduce logic that is used by a job.</span></span> <span data-ttu-id="cb155-124">Los requisitos específicos de la lógica de asignación y reducción son:</span><span class="sxs-lookup"><span data-stu-id="cb155-124">The specific requirements for the map and reduce logic are:</span></span>

* <span data-ttu-id="cb155-125">**Entrada**: los componentes de asignación y reducción deben leer los datos de entrada desde STDIN.</span><span class="sxs-lookup"><span data-stu-id="cb155-125">**Input**: The map and reduce components must read input data from STDIN.</span></span>
* <span data-ttu-id="cb155-126">**Salida**: los componentes de asignación y reducción deben escribir los datos de salida en STDOUT.</span><span class="sxs-lookup"><span data-stu-id="cb155-126">**Output**: The map and reduce components must write output data to STDOUT.</span></span>
* <span data-ttu-id="cb155-127">**Formato de datos**: los datos consumidos y producidos deben ser un par clave-valor, separado por un carácter de tabulación.</span><span class="sxs-lookup"><span data-stu-id="cb155-127">**Data format**: The data consumed and produced must be a key/value pair, separated by a tab character.</span></span>

<span data-ttu-id="cb155-128">Con Python se pueden controlar fácilmente estos requisitos mediante el uso del módulo `sys` para leer desde STDIN y `print` para imprimir en STDOUT.</span><span class="sxs-lookup"><span data-stu-id="cb155-128">Python can easily handle these requirements by using the `sys` module to read from STDIN and using `print` to print to STDOUT.</span></span> <span data-ttu-id="cb155-129">La tarea restante consiste simplemente en dar formato a los datos con un carácter de tabulación (`\t`) entre la clave y el valor.</span><span class="sxs-lookup"><span data-stu-id="cb155-129">The remaining task is simply formatting the data with a tab (`\t`) character between the key and value.</span></span>

## <a name="create-the-mapper-and-reducer"></a><span data-ttu-id="cb155-130">Creación del asignador y del reductor</span><span class="sxs-lookup"><span data-stu-id="cb155-130">Create the mapper and reducer</span></span>

1. <span data-ttu-id="cb155-131">Cree un archivo llamado `mapper.py` y use el siguiente código como contenido:</span><span class="sxs-lookup"><span data-stu-id="cb155-131">Create a file named `mapper.py` and use the following code as the content:</span></span>

   ```python
   #!/usr/bin/env python

   # Use the sys module
   import sys

   # 'file' in this case is STDIN
   def read_input(file):
       # Split each line into words
       for line in file:
           yield line.split()

   def main(separator='\t'):
       # Read the data using read_input
       data = read_input(sys.stdin)
       # Process each word returned from read_input
       for words in data:
           # Process each word
           for word in words:
               # Write to STDOUT
               print '%s%s%d' % (word, separator, 1)

   if __name__ == "__main__":
       main()
   ```

2. <span data-ttu-id="cb155-132">Cree un archivo nuevo llamado **reducer.py** y use el siguiente código como contenido:</span><span class="sxs-lookup"><span data-stu-id="cb155-132">Create a file named **reducer.py** and use the following code as the content:</span></span>

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
           # Strip out the separator character
           yield line.rstrip().split(separator, 1)

   def main(separator='\t'):
       # Read the data using read_mapper_output
       data = read_mapper_output(sys.stdin, separator=separator)
       # Group words and counts into 'group'
       #   Since MapReduce is a distributed process, each word
       #   may have multiple counts. 'group' will have all counts
       #   which can be retrieved using the word as the key.
       for current_word, group in groupby(data, itemgetter(0)):
           try:
               # For each word, pull the count(s) for the word
               #   from 'group' and create a total count
               total_count = sum(int(count) for current_word, count in group)
               # Write to stdout
               print "%s%s%d" % (current_word, separator, total_count)
           except ValueError:
               # Count was not a number, so do nothing
               pass

   if __name__ == "__main__":
       main()
   ```

## <a name="run-using-powershell"></a><span data-ttu-id="cb155-133">Ejecución con PowerShell</span><span class="sxs-lookup"><span data-stu-id="cb155-133">Run using PowerShell</span></span>

<span data-ttu-id="cb155-134">Para asegurarse de que los archivos tengan los finales de línea correctos, use el siguiente script de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="cb155-134">To ensure that your files have the right line endings, use the following PowerShell script:</span></span>

<span data-ttu-id="cb155-135">[!code-powershell[main](../../powershell_scripts/hdinsight/streaming-python/streaming-python.ps1?range=138-140)]</span><span class="sxs-lookup"><span data-stu-id="cb155-135">[!code-powershell[main](../../powershell_scripts/hdinsight/streaming-python/streaming-python.ps1?range=138-140)]</span></span>

<span data-ttu-id="cb155-136">Use el siguiente script de PowerShell para cargar los archivos, ejecutar el trabajo y ver la salida:</span><span class="sxs-lookup"><span data-stu-id="cb155-136">Use the following PowerShell script to upload the files, run the job, and view the output:</span></span>

<span data-ttu-id="cb155-137">[!code-powershell[main](../../powershell_scripts/hdinsight/streaming-python/streaming-python.ps1?range=5-134)]</span><span class="sxs-lookup"><span data-stu-id="cb155-137">[!code-powershell[main](../../powershell_scripts/hdinsight/streaming-python/streaming-python.ps1?range=5-134)]</span></span>

## <a name="run-from-an-ssh-session"></a><span data-ttu-id="cb155-138">Ejecución desde una sesión de SSH</span><span class="sxs-lookup"><span data-stu-id="cb155-138">Run from an SSH session</span></span>

1. <span data-ttu-id="cb155-139">En el entorno de desarrollo, en el mismo directorio que `mapper.py` y `reducer.py`, use el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="cb155-139">From your development environment, in the same directory as `mapper.py` and `reducer.py` files, use the following command:</span></span>

    ```bash
    scp mapper.py reducer.py username@clustername-ssh.azurehdinsight.net:
    ```

    <span data-ttu-id="cb155-140">Reemplace `username` por el nombre de usuario de SSH del clúster y `clustername` o el nombre de su clúster.</span><span class="sxs-lookup"><span data-stu-id="cb155-140">Replace `username` with the SSH user name for your cluster, and `clustername` with the name of your cluster.</span></span>

    <span data-ttu-id="cb155-141">Este comando copia los archivos del sistema local al nodo principal.</span><span class="sxs-lookup"><span data-stu-id="cb155-141">This command copies the files from the local system to the head node.</span></span>

    > [!NOTE]
    > <span data-ttu-id="cb155-142">Si usó una contraseña para proteger su cuenta SSH, se le preguntará la contraseña.</span><span class="sxs-lookup"><span data-stu-id="cb155-142">If you used a password to secure your SSH account, you are prompted for the password.</span></span> <span data-ttu-id="cb155-143">Si usó una clave SSH, es posible que deba usar el parámetro `-i` y la ruta de acceso a la clave privada.</span><span class="sxs-lookup"><span data-stu-id="cb155-143">If you used an SSH key, you may have to use the `-i` parameter and the path to the private key.</span></span> <span data-ttu-id="cb155-144">Por ejemplo: `scp -i /path/to/private/key mapper.py reducer.py username@clustername-ssh.azurehdinsight.net:`.</span><span class="sxs-lookup"><span data-stu-id="cb155-144">For example, `scp -i /path/to/private/key mapper.py reducer.py username@clustername-ssh.azurehdinsight.net:`.</span></span>

2. <span data-ttu-id="cb155-145">Conéctese al clúster mediante SSH:</span><span class="sxs-lookup"><span data-stu-id="cb155-145">Connect to the cluster by using SSH:</span></span>

    ```bash
    ssh username@clustername-ssh.azurehdinsight.net`
    ```

    <span data-ttu-id="cb155-146">Para más información, consulte [Uso de SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="cb155-146">For more information on, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

3. <span data-ttu-id="cb155-147">Para asegurarse de que mapper.py y reducer.py tengan los finales de línea correctos, use los siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="cb155-147">To ensure the mapper.py and reducer.py have the correct line endings, use the following commands:</span></span>

    ```bash
    perl -pi -e 's/\r\n/\n/g' mapper.py
    perl -pi -e 's/\r\n/\n/g' reducer.py
    ```

4. <span data-ttu-id="cb155-148">Use el comando siguiente para iniciar el trabajo de MapReduce.</span><span class="sxs-lookup"><span data-stu-id="cb155-148">Use the following command to start the MapReduce job.</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar -files mapper.py,reducer.py -mapper mapper.py -reducer reducer.py -input /example/data/gutenberg/davinci.txt -output /example/wordcountout
    ```

    <span data-ttu-id="cb155-149">Este comando cuenta con las siguientes partes:</span><span class="sxs-lookup"><span data-stu-id="cb155-149">This command has the following parts:</span></span>

   * <span data-ttu-id="cb155-150">**hadoop-streaming.jar**: se usa cuando se realizan operaciones de streaming de MapReduce.</span><span class="sxs-lookup"><span data-stu-id="cb155-150">**hadoop-streaming.jar**: Used when performing streaming MapReduce operations.</span></span> <span data-ttu-id="cb155-151">Crea una interfaz de Hadoop con el código de MapReduce externo que proporciona.</span><span class="sxs-lookup"><span data-stu-id="cb155-151">It interfaces Hadoop with the external MapReduce code you provide.</span></span>

   * <span data-ttu-id="cb155-152">**-files**: agrega los archivos especificados al trabajo de MapReduce.</span><span class="sxs-lookup"><span data-stu-id="cb155-152">**-files**: Adds the specified files to the MapReduce job.</span></span>

   * <span data-ttu-id="cb155-153">**-mapper**: indica a Hadoop qué archivo debe usar como asignador.</span><span class="sxs-lookup"><span data-stu-id="cb155-153">**-mapper**: Tells Hadoop which file to use as the mapper.</span></span>

   * <span data-ttu-id="cb155-154">**-reducer**: indica a Hadoop qué archivo debe usar como reductor.</span><span class="sxs-lookup"><span data-stu-id="cb155-154">**-reducer**: Tells Hadoop which file to use as the reducer.</span></span>

   * <span data-ttu-id="cb155-155">**-input**: el archivo de entrada en el cual debemos contar las palabras.</span><span class="sxs-lookup"><span data-stu-id="cb155-155">**-input**: The input file that we should count words from.</span></span>

   * <span data-ttu-id="cb155-156">**-output**: el directorio en el que se escribe la salida.</span><span class="sxs-lookup"><span data-stu-id="cb155-156">**-output**: The directory that the output is written to.</span></span>

    <span data-ttu-id="cb155-157">Cuando el trabajo de MapReduce funciona, el proceso se muestra como porcentajes.</span><span class="sxs-lookup"><span data-stu-id="cb155-157">As the MapReduce job works, the process is displayed as percentages.</span></span>

        <span data-ttu-id="cb155-158">15/02/05 19:01:04 INFO mapreduce.Job:  map 0% reduce 0%    15/02/05 19:01:16 INFO mapreduce.Job:  map 100% reduce 0%    15/02/05 19:01:27 INFO mapreduce.Job:  map 100% reduce 100%</span><span class="sxs-lookup"><span data-stu-id="cb155-158">15/02/05 19:01:04 INFO mapreduce.Job:  map 0% reduce 0%    15/02/05 19:01:16 INFO mapreduce.Job:  map 100% reduce 0%    15/02/05 19:01:27 INFO mapreduce.Job:  map 100% reduce 100%</span></span>


5. <span data-ttu-id="cb155-159">Para ver la salida, use el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="cb155-159">To view the output, use the following command:</span></span>

    ```bash
    hdfs dfs -text /example/wordcountout/part-00000
    ```

    <span data-ttu-id="cb155-160">Este comando muestra una lista de palabras y el número de veces que aparecieron.</span><span class="sxs-lookup"><span data-stu-id="cb155-160">This command displays a list of words and how many times the word occurred.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cb155-161">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="cb155-161">Next steps</span></span>

<span data-ttu-id="cb155-162">Ahora que aprendió a usar los trabajos de transmisión de MapReduce con HDInsight, use los siguientes vínculos para explorar otras formas de trabajar con HDInsight de Azure.</span><span class="sxs-lookup"><span data-stu-id="cb155-162">Now that you have learned how to use streaming MapRedcue jobs with HDInsight, use the following links to explore other ways to work with Azure HDInsight.</span></span>

* [<span data-ttu-id="cb155-163">Uso de Hive con HDInsight</span><span class="sxs-lookup"><span data-stu-id="cb155-163">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="cb155-164">Uso de Pig con HDInsight</span><span class="sxs-lookup"><span data-stu-id="cb155-164">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="cb155-165">Uso de trabajos de MapReduce con HDInsight</span><span class="sxs-lookup"><span data-stu-id="cb155-165">Use MapReduce jobs with HDInsight</span></span>](hdinsight-use-mapreduce.md)
