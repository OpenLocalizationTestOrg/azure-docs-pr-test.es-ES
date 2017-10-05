---
title: "Ejecución de ejemplos de MapReduce de Hadoop en HDInsight y Azure | Microsoft Docs"
description: "Introducción al uso de ejemplos de MapReduce en archivos jar incluidos en HDInsight. Use SSH para conectarse al clúster y, a continuación, use el comando de Hadoop para ejecutar trabajos de ejemplo."
keywords: jar de ejemplo de hadoop, jar de ejemplos de hadoop, ejemplos de mapreduce de hadoop, ejemplos de mapreduce
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: e1d2a0b9-1659-4fab-921e-4a8990cbb30a
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: 447c07f869ff9a2a2a00089248be98e6729d6dc4
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="run-the-mapreduce-examples-included-in-hdinsight"></a><span data-ttu-id="e5c88-105">Ejecución de los ejemplos de MapReduce incluidos en HDInsight</span><span class="sxs-lookup"><span data-stu-id="e5c88-105">Run the MapReduce examples included in HDInsight</span></span>

[!INCLUDE [samples-selector](../../includes/hdinsight-run-samples-selector.md)]

<span data-ttu-id="e5c88-106">Aprenda a ejecutar los ejemplos de MapReduce incluidos con Hadoop en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e5c88-106">Learn how to run the MapReduce examples included with Hadoop on HDInsight.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e5c88-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="e5c88-107">Prerequisites</span></span>

* <span data-ttu-id="e5c88-108">**Un clúster de HDInsight**: consulte [Introducción al uso de Hadoop con Hive en HDInsight en Linux](hdinsight-hadoop-linux-tutorial-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="e5c88-108">**An HDInsight cluster**: See [Get started using Hadoop with Hive in HDInsight on Linux](hdinsight-hadoop-linux-tutorial-get-started.md)</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="e5c88-109">Linux es el único sistema operativo que se usa en la versión 3.4 de HDInsight, o en las superiores.</span><span class="sxs-lookup"><span data-stu-id="e5c88-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="e5c88-110">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="e5c88-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="e5c88-111">**Un cliente SSH**: para obtener más información, consulte [Uso de SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="e5c88-111">**An SSH client**: For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <a name="the-mapreduce-examples"></a><span data-ttu-id="e5c88-112">Ejemplos de MapReduce</span><span class="sxs-lookup"><span data-stu-id="e5c88-112">The MapReduce examples</span></span>

<span data-ttu-id="e5c88-113">**Ubicación**: Los ejemplos se encuentran en el clúster de HDInsight en `/usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar`.</span><span class="sxs-lookup"><span data-stu-id="e5c88-113">**Location**: The samples are located on the HDInsight cluster at `/usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar`.</span></span>

<span data-ttu-id="e5c88-114">**Contenido**: se incluyen los siguientes ejemplos en este archivo:</span><span class="sxs-lookup"><span data-stu-id="e5c88-114">**Contents**: The following samples are contained in this archive:</span></span>

* <span data-ttu-id="e5c88-115">`aggregatewordcount`: programa mapreduce basado en agregación que cuenta las palabras de los archivos de entrada.</span><span class="sxs-lookup"><span data-stu-id="e5c88-115">`aggregatewordcount`: An Aggregate based mapreduce program that counts the words in the input files.</span></span>
* <span data-ttu-id="e5c88-116">`aggregatewordhist`: programa mapreduce basado en agregación que cuenta el histograma de las palabras de los archivos de entrada.</span><span class="sxs-lookup"><span data-stu-id="e5c88-116">`aggregatewordhist`: An Aggregate based mapreduce program that computes the histogram of the words in the input files.</span></span>
* <span data-ttu-id="e5c88-117">`bbp`: programa de mapreduce que usa una fórmula Bailey-Borwein-Plouffe para calcular los dígitos exactos de Pi.</span><span class="sxs-lookup"><span data-stu-id="e5c88-117">`bbp`: A mapreduce program that uses Bailey-Borwein-Plouffe to compute exact digits of Pi.</span></span>
* <span data-ttu-id="e5c88-118">`dbcount`: trabajo de ejemplo que cuenta los registros de vistas de página almacenados en una base de datos.</span><span class="sxs-lookup"><span data-stu-id="e5c88-118">`dbcount`: An example job that counts the pageview logs stored in a database.</span></span>
* <span data-ttu-id="e5c88-119">`distbbp`: programa de mapreduce que usa una fórmula de tipo BBP para calcular los bits exactos de Pi.</span><span class="sxs-lookup"><span data-stu-id="e5c88-119">`distbbp`: A mapreduce program that uses a BBP-type formula to compute exact bits of Pi.</span></span>
* <span data-ttu-id="e5c88-120">`grep`: programa de mapreduce que cuenta las coincidencias de regex en la entrada.</span><span class="sxs-lookup"><span data-stu-id="e5c88-120">`grep`: A mapreduce program that counts the matches of a regex in the input.</span></span>
* <span data-ttu-id="e5c88-121">`join`: trabajo que realiza una unión de conjuntos de datos ordenados con particiones equiparables.</span><span class="sxs-lookup"><span data-stu-id="e5c88-121">`join`: A job that performs a join over sorted, equally partitioned datasets.</span></span>
* <span data-ttu-id="e5c88-122">`multifilewc`: trabajo que cuenta las palabras de varios archivos.</span><span class="sxs-lookup"><span data-stu-id="e5c88-122">`multifilewc`: A job that counts words from several files.</span></span>
* <span data-ttu-id="e5c88-123">`pentomino`: programa de mapreduce para la colocación de mosaicos con el fin de encontrar soluciones a problemas de pentominó.</span><span class="sxs-lookup"><span data-stu-id="e5c88-123">`pentomino`: A mapreduce tile laying program to find solutions to pentomino problems.</span></span>
* <span data-ttu-id="e5c88-124">`pi`: programa de mapreduce que calcula Pi mediante un método cuasi Monte Carlo.</span><span class="sxs-lookup"><span data-stu-id="e5c88-124">`pi`: A mapreduce program that estimates Pi using a quasi-Monte Carlo method.</span></span>
* <span data-ttu-id="e5c88-125">`randomtextwriter`: programa de mapreduce que escribe 10 GB de datos de texto aleatorios por nodo.</span><span class="sxs-lookup"><span data-stu-id="e5c88-125">`randomtextwriter`: A mapreduce program that writes 10 GB of random textual data per node.</span></span>
* <span data-ttu-id="e5c88-126">`randomwriter`: programa de mapreduce que escribe 10 GB de datos aleatorios por nodo.</span><span class="sxs-lookup"><span data-stu-id="e5c88-126">`randomwriter`: A mapreduce program that writes 10 GB of random data per node.</span></span>
* <span data-ttu-id="e5c88-127">`secondarysort`: ejemplo que define una ordenación secundaria para la fase de reducción.</span><span class="sxs-lookup"><span data-stu-id="e5c88-127">`secondarysort`: An example defining a secondary sort to the reduce phase.</span></span>
* <span data-ttu-id="e5c88-128">`sort`: programa de mapreduce que ordena los datos escritos por el escritor aleatorio.</span><span class="sxs-lookup"><span data-stu-id="e5c88-128">`sort`: A mapreduce program that sorts the data written by the random writer.</span></span>
* <span data-ttu-id="e5c88-129">`sudoku`: solucionador de sudokus.</span><span class="sxs-lookup"><span data-stu-id="e5c88-129">`sudoku`: A sudoku solver.</span></span>
* <span data-ttu-id="e5c88-130">`teragen`: genera datos para la ordenación de terabytes (terasort).</span><span class="sxs-lookup"><span data-stu-id="e5c88-130">`teragen`: Generate data for the terasort.</span></span>
* <span data-ttu-id="e5c88-131">`terasort`: ejecuta la ordenación de terabytes (terasort).</span><span class="sxs-lookup"><span data-stu-id="e5c88-131">`terasort`: Run the terasort.</span></span>
* <span data-ttu-id="e5c88-132">`teravalidate`: comprueba los resultados de la ordenación de terabytes (terasort).</span><span class="sxs-lookup"><span data-stu-id="e5c88-132">`teravalidate`: Checking results of terasort.</span></span>
* <span data-ttu-id="e5c88-133">`wordcount`: programa de mapreduce que cuenta las palabras de los archivos de entrada.</span><span class="sxs-lookup"><span data-stu-id="e5c88-133">`wordcount`: A mapreduce program that counts the words in the input files.</span></span>
* <span data-ttu-id="e5c88-134">`wordmean`: programa de mapreduce que cuenta la longitud media de las palabras de los archivos de entrada.</span><span class="sxs-lookup"><span data-stu-id="e5c88-134">`wordmean`: A mapreduce program that counts the average length of the words in the input files.</span></span>
* <span data-ttu-id="e5c88-135">`wordmedian`: programa de mapreduce que cuenta la mediana de la longitud de las palabras de los archivos de entrada.</span><span class="sxs-lookup"><span data-stu-id="e5c88-135">`wordmedian`: A mapreduce program that counts the median length of the words in the input files.</span></span>
* <span data-ttu-id="e5c88-136">`wordstandarddeviation`: programa de mapreduce que cuenta la desviación estándar de la longitud de las palabras de los archivos de entrada.</span><span class="sxs-lookup"><span data-stu-id="e5c88-136">`wordstandarddeviation`: A mapreduce program that counts the standard deviation of the length of the words in the input files.</span></span>

<span data-ttu-id="e5c88-137">**Código fuente**: el código fuente de estos ejemplos se incluye en el clúster de HDInsight en `/usr/hdp/2.2.4.9-1/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples`.</span><span class="sxs-lookup"><span data-stu-id="e5c88-137">**Source code**: Source code for these samples is included on the HDInsight cluster at `/usr/hdp/2.2.4.9-1/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples`.</span></span>

> [!NOTE]
> <span data-ttu-id="e5c88-138">El `2.2.4.9-1` en la ruta de acceso es la versión de Hortonworks Data Platform para el clúster de HDInsight y puede que sea diferente para su clúster.</span><span class="sxs-lookup"><span data-stu-id="e5c88-138">The `2.2.4.9-1` in the path is the version of the Hortonworks Data Platform for the HDInsight cluster, and may be different for your cluster.</span></span>

## <a name="run-the-wordcount-example"></a><span data-ttu-id="e5c88-139">Ejecución del ejemplo de wordcount</span><span class="sxs-lookup"><span data-stu-id="e5c88-139">Run the wordcount example</span></span>

1. <span data-ttu-id="e5c88-140">Conéctese a HDInsight mediante SSH.</span><span class="sxs-lookup"><span data-stu-id="e5c88-140">Connect to HDInsight using SSH.</span></span> <span data-ttu-id="e5c88-141">Para más información, consulte [Uso SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="e5c88-141">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="e5c88-142">En el símbolo `username@#######:~$` , use el siguiente comando para mostrar los ejemplos:</span><span class="sxs-lookup"><span data-stu-id="e5c88-142">From the `username@#######:~$` prompt, use the following command to list the samples:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar
    ```

    <span data-ttu-id="e5c88-143">Este comando genera la lista de ejemplos de la sección anterior de este documento.</span><span class="sxs-lookup"><span data-stu-id="e5c88-143">This command generates the list of sample from the previous section of this document.</span></span>

3. <span data-ttu-id="e5c88-144">Use el siguiente comando para obtener ayuda sobre un ejemplo concreto.</span><span class="sxs-lookup"><span data-stu-id="e5c88-144">Use the following command to get help on a specific sample.</span></span> <span data-ttu-id="e5c88-145">En este caso, el ejemplo **wordcount** :</span><span class="sxs-lookup"><span data-stu-id="e5c88-145">In this case, the **wordcount** sample:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount
    ```

    <span data-ttu-id="e5c88-146">Recibirá el siguiente mensaje:</span><span class="sxs-lookup"><span data-stu-id="e5c88-146">You receive the following message:</span></span>

        Usage: wordcount <in> [<in>...] <out>

    <span data-ttu-id="e5c88-147">Este mensaje indica que puede proporcionar varias rutas de entrada para los documentos de origen.</span><span class="sxs-lookup"><span data-stu-id="e5c88-147">This message indicates that you can provide several input paths for the source documents.</span></span> <span data-ttu-id="e5c88-148">La ruta de acceso final es donde se almacena la salida (la cantidad de palabras en los documentos de origen).</span><span class="sxs-lookup"><span data-stu-id="e5c88-148">The final path is where the output (count of words in the source documents) is stored.</span></span>

4. <span data-ttu-id="e5c88-149">Use lo siguiente para contar todas las palabras en los cuadernos de Leonardo Da Vinci, que se proporcionan como datos de ejemplo con su clúster:</span><span class="sxs-lookup"><span data-stu-id="e5c88-149">Use the following to count all words in the Notebooks of Leonardo Da Vinci, which are provided as sample data with your cluster:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/davinciwordcount
    ```

    <span data-ttu-id="e5c88-150">La entrada de este trabajo se lee desde `/example/data/gutenberg/davinci.txt`.</span><span class="sxs-lookup"><span data-stu-id="e5c88-150">Input for this job is read from `/example/data/gutenberg/davinci.txt`.</span></span> <span data-ttu-id="e5c88-151">La salida de este ejemplo se almacena en `/example/data/davinciwordcount`.</span><span class="sxs-lookup"><span data-stu-id="e5c88-151">Output for this example is stored in `/example/data/davinciwordcount`.</span></span> <span data-ttu-id="e5c88-152">Ambas rutas de acceso se encuentran en el almacenamiento predeterminado del clúster, no en el sistema de archivos local.</span><span class="sxs-lookup"><span data-stu-id="e5c88-152">Both paths are located on default storage for the cluster, not the local file system.</span></span>

   > [!NOTE]
   > <span data-ttu-id="e5c88-153">Como se indica en la Ayuda del ejemplo wordcount, también puede especificar varios archivos de entrada.</span><span class="sxs-lookup"><span data-stu-id="e5c88-153">As noted in the help for the wordcount sample, you could also specify multiple input files.</span></span> <span data-ttu-id="e5c88-154">Por ejemplo, `hadoop jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/gutenberg/ulysses.txt /example/data/twowordcount` contaría las palabras de davinci.txt y ulysses.txt.</span><span class="sxs-lookup"><span data-stu-id="e5c88-154">For example, `hadoop jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/gutenberg/ulysses.txt /example/data/twowordcount` would count words in both davinci.txt and ulysses.txt.</span></span>

5. <span data-ttu-id="e5c88-155">Una vez completado el trabajo, use el siguiente comando para ver la salida:</span><span class="sxs-lookup"><span data-stu-id="e5c88-155">Once the job completes, use the following command to view the output:</span></span>

    ```bash
    hdfs dfs -cat /example/data/davinciwordcount/*
    ```

    <span data-ttu-id="e5c88-156">Este comando concatena todos los archivos de salida generados por el trabajo.</span><span class="sxs-lookup"><span data-stu-id="e5c88-156">This command concatenates all the output files produced by the job.</span></span> <span data-ttu-id="e5c88-157">Muestra la salida en la consola.</span><span class="sxs-lookup"><span data-stu-id="e5c88-157">It displays the output to the console.</span></span> <span data-ttu-id="e5c88-158">La salida será similar al siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="e5c88-158">The output is similar to the following text:</span></span>

        zum     1
        zur     1
        zwanzig 1
        zweite  1

    <span data-ttu-id="e5c88-159">Cada línea representa una palabra y el número de veces que aparece en los datos de entrada.</span><span class="sxs-lookup"><span data-stu-id="e5c88-159">Each line represents a word and how many times it occurred in the input data.</span></span>

## <a name="the-sudoku-example"></a><span data-ttu-id="e5c88-160">Ejemplo de Sudoku</span><span class="sxs-lookup"><span data-stu-id="e5c88-160">The Sudoku example</span></span>

<span data-ttu-id="e5c88-161">[Sudoku](https://en.wikipedia.org/wiki/Sudoku) es un rompecabezas lógico compuesto por nueve cuadrículas de 3 × 3.</span><span class="sxs-lookup"><span data-stu-id="e5c88-161">[Sudoku](https://en.wikipedia.org/wiki/Sudoku) is a logic puzzle made up of nine 3x3 grids.</span></span> <span data-ttu-id="e5c88-162">Algunas celdas de la cuadrícula tienen números y otras están en blanco; el objetivo es resolver las celdas en blanco.</span><span class="sxs-lookup"><span data-stu-id="e5c88-162">Some cells in the grid have numbers, while others are blank, and the goal is to solve for the blank cells.</span></span> <span data-ttu-id="e5c88-163">El vínculo anterior contiene más información sobre el rompecabezas, pero el propósito de este ejemplo consiste en resolver las celdas en blanco.</span><span class="sxs-lookup"><span data-stu-id="e5c88-163">The previous link has more information on the puzzle, but the purpose of this sample is to solve for the blank cells.</span></span> <span data-ttu-id="e5c88-164">Así que nuestra entrada debe ser un archivo en el formato siguiente:</span><span class="sxs-lookup"><span data-stu-id="e5c88-164">So our input should be a file that is in the following format:</span></span>

* <span data-ttu-id="e5c88-165">Nueve filas de nueve columnas;</span><span class="sxs-lookup"><span data-stu-id="e5c88-165">Nine rows of nine columns</span></span>
* <span data-ttu-id="e5c88-166">Cada columna puede contener un número o `?` (que indica una celda en blanco);</span><span class="sxs-lookup"><span data-stu-id="e5c88-166">Each column can contain either a number or `?` (which indicates a blank cell)</span></span>
* <span data-ttu-id="e5c88-167">Las celdas se separan por un espacio.</span><span class="sxs-lookup"><span data-stu-id="e5c88-167">Cells are separated by a space</span></span>

<span data-ttu-id="e5c88-168">Existe una forma determinada de construir rompecabezas sudoku para que no se repita un número en una columna o fila.</span><span class="sxs-lookup"><span data-stu-id="e5c88-168">There is a certain way to construct Sudoku puzzles; you can't repeat a number in a column or row.</span></span> <span data-ttu-id="e5c88-169">Hay un ejemplo en el clúster de HDInsight que se ha creado correctamente.</span><span class="sxs-lookup"><span data-stu-id="e5c88-169">There's an example on the HDInsight cluster that is properly constructed.</span></span> <span data-ttu-id="e5c88-170">Se encuentra en `/usr/hdp/*/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples/src/main/java/org/apache/hadoop/examples/dancing/puzzle1.dta` y contiene el texto siguiente:</span><span class="sxs-lookup"><span data-stu-id="e5c88-170">It is located at `/usr/hdp/*/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples/src/main/java/org/apache/hadoop/examples/dancing/puzzle1.dta` and contains the following text:</span></span>

    8 5 ? 3 9 ? ? ? ?
    ? ? 2 ? ? ? ? ? ?
    ? ? 6 ? 1 ? ? ? 2
    ? ? 4 ? ? 3 ? 5 9
    ? ? 8 9 ? 1 4 ? ?
    3 2 ? 4 ? ? 8 ? ?
    9 ? ? ? 8 ? 5 ? ?
    ? ? ? ? ? ? 2 ? ?
    ? ? ? ? 4 5 ? 7 8

<span data-ttu-id="e5c88-171">Para ejecutar este problema con el ejemplo sudoku, use el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="e5c88-171">To run this example problem through the Sudoku example, use the following command:</span></span>

```bash
yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar sudoku /usr/hdp/*/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples/src/main/java/org/apache/hadoop/examples/dancing/puzzle1.dta
```

<span data-ttu-id="e5c88-172">Los resultados deberían asemejarse a este texto:</span><span class="sxs-lookup"><span data-stu-id="e5c88-172">The results appear similar to the following text:</span></span>

    8 5 1 3 9 2 6 4 7
    4 3 2 6 7 8 1 9 5
    7 9 6 5 1 4 3 8 2
    6 1 4 8 2 3 7 5 9
    5 7 8 9 6 1 4 2 3
    3 2 9 4 5 7 8 1 6
    9 4 7 2 8 6 5 3 1
    1 8 5 7 3 9 2 6 4
    2 6 3 1 4 5 9 7 8

## <a name="pi--example"></a><span data-ttu-id="e5c88-173">Ejemplo de PI (π)</span><span class="sxs-lookup"><span data-stu-id="e5c88-173">Pi (π) example</span></span>

<span data-ttu-id="e5c88-174">El ejemplo pi usa un método estadístico (cuasi Monte Carlo) para calcular el valor de pi.</span><span class="sxs-lookup"><span data-stu-id="e5c88-174">The pi sample uses a statistical (quasi-Monte Carlo) method to estimate the value of pi.</span></span> <span data-ttu-id="e5c88-175">Los puntos se colocan de forma aleatoria en un cuadrado unitario.</span><span class="sxs-lookup"><span data-stu-id="e5c88-175">Points are placed at random in a unit square.</span></span> <span data-ttu-id="e5c88-176">El cuadrado también contiene un círculo.</span><span class="sxs-lookup"><span data-stu-id="e5c88-176">The square also contains a circle.</span></span> <span data-ttu-id="e5c88-177">La probabilidad de que los puntos se encuentren dentro del círculo es igual al área del círculo, pi/4.</span><span class="sxs-lookup"><span data-stu-id="e5c88-177">The probability that the points fall within the circle are equal to the area of the circle, pi/4.</span></span> <span data-ttu-id="e5c88-178">El valor de pi se puede estimar a partir del valor de 4R.</span><span class="sxs-lookup"><span data-stu-id="e5c88-178">The value of pi can be estimated from the value of 4R.</span></span> <span data-ttu-id="e5c88-179">R es la proporción de la cantidad de puntos dentro del círculo con respecto al número total de puntos que se encuentran dentro del cuadrado.</span><span class="sxs-lookup"><span data-stu-id="e5c88-179">R is the ratio of the number of points that are inside the circle to the total number of points that are within the square.</span></span> <span data-ttu-id="e5c88-180">Mientras más grande sea la muestra de puntos usada, mejor resulta el valor calculado.</span><span class="sxs-lookup"><span data-stu-id="e5c88-180">The larger the sample of points used, the better the estimate is.</span></span>

<span data-ttu-id="e5c88-181">Use el siguiente comando para ejecutar este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="e5c88-181">Use the following command to run this sample.</span></span> <span data-ttu-id="e5c88-182">Este comando usa 16 asignaciones con 10 millones de ejemplos cada una para calcular el valor de pi:</span><span class="sxs-lookup"><span data-stu-id="e5c88-182">This command uses 16 maps with 10,000,000 samples each to estimate the value of pi:</span></span>

```bash
yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar pi 16 10000000
```

<span data-ttu-id="e5c88-183">El valor devuelto debería asemejarse a **3,14159155000000000000**.</span><span class="sxs-lookup"><span data-stu-id="e5c88-183">The value returned by this command is similar to **3.14159155000000000000**.</span></span> <span data-ttu-id="e5c88-184">Como referencia, las primeras 10 posiciones decimales de pi son 3,1415926535.</span><span class="sxs-lookup"><span data-stu-id="e5c88-184">For references, the first 10 decimal places of pi are 3.1415926535.</span></span>

## <a name="10-gb-greysort-example"></a><span data-ttu-id="e5c88-185">Ejemplo de Greysort de 10 GB</span><span class="sxs-lookup"><span data-stu-id="e5c88-185">10 GB Greysort example</span></span>

<span data-ttu-id="e5c88-186">GraySort es una ordenación de pruebas comparativas.</span><span class="sxs-lookup"><span data-stu-id="e5c88-186">GraySort is a benchmark sort.</span></span> <span data-ttu-id="e5c88-187">La métrica es la velocidad de ordenación (TB/minuto) que se logra después de ordenar enormes volúmenes de datos, normalmente 100 TB, como mínimo.</span><span class="sxs-lookup"><span data-stu-id="e5c88-187">The metric is the sort rate (TB/minute) that is achieved while sorting large amounts of data, usually a 100 TB minimum.</span></span>

<span data-ttu-id="e5c88-188">Este ejemplo utiliza solo 10 GB de datos, para así poder ejecutarlo relativamente rápido.</span><span class="sxs-lookup"><span data-stu-id="e5c88-188">This sample uses a modest 10 GB of data so that it can be run relatively quickly.</span></span> <span data-ttu-id="e5c88-189">Usa las aplicaciones de MapReduce desarrolladas por Owen O'Malley y Arun Murthy.</span><span class="sxs-lookup"><span data-stu-id="e5c88-189">It uses the MapReduce applications developed by Owen O'Malley and Arun Murthy.</span></span> <span data-ttu-id="e5c88-190">Estas aplicaciones ganaron el estándar de comparación anual de ordenación de terabytes de fin general ("daytona") en 2009 con una velocidad de 0,578 TB/min (100 TB en 173 minutos).</span><span class="sxs-lookup"><span data-stu-id="e5c88-190">These applications won the annual general-purpose ("daytona") terabyte sort benchmark in 2009, with a rate of 0.578 TB/min (100 TB in 173 minutes).</span></span> <span data-ttu-id="e5c88-191">Para obtener más información sobre este y otros estándares de comparación de ordenación, consulte el sitio [Sortbenchmark](http://sortbenchmark.org/) .</span><span class="sxs-lookup"><span data-stu-id="e5c88-191">For more information on this and other sorting benchmarks, see the [Sortbenchmark](http://sortbenchmark.org/) site.</span></span>

<span data-ttu-id="e5c88-192">Este ejemplo utiliza tres conjuntos de programas de MapReduce:</span><span class="sxs-lookup"><span data-stu-id="e5c88-192">This sample uses three sets of MapReduce programs:</span></span>

* <span data-ttu-id="e5c88-193">**TeraGen**: programa de MapReduce que genera filas de datos que se van a ordenar.</span><span class="sxs-lookup"><span data-stu-id="e5c88-193">**TeraGen**: A MapReduce program that generates rows of data to sort</span></span>

* <span data-ttu-id="e5c88-194">**TeraSort**: toma una muestra de los datos de entrada y usa MapReduce para ordenar los datos de manera absoluta.</span><span class="sxs-lookup"><span data-stu-id="e5c88-194">**TeraSort**: Samples the input data and uses MapReduce to sort the data into a total order</span></span>

    <span data-ttu-id="e5c88-195">TeraSort es una ordenación MapReduce estándar, salvo por el particionador personalizado.</span><span class="sxs-lookup"><span data-stu-id="e5c88-195">TeraSort is a standard MapReduce sort, except for a custom partitioner.</span></span> <span data-ttu-id="e5c88-196">El particionador usa una lista ordenada de N-1 claves de muestra que definen el intervalo de claves para cada reducción.</span><span class="sxs-lookup"><span data-stu-id="e5c88-196">The partitioner uses a sorted list of N-1 sampled keys that define the key range for each reduce.</span></span> <span data-ttu-id="e5c88-197">En concreto, todas las claves, como esa muestra[i-1] <= clave < muestra[i] se envían a la reducción i.</span><span class="sxs-lookup"><span data-stu-id="e5c88-197">In particular, all keys such that sample[i-1] <= key < sample[i] are sent to reduce i.</span></span> <span data-ttu-id="e5c88-198">Esta particionador garantiza que las salidas de la reducción i sean todas menores que la salida de la reducción i+1.</span><span class="sxs-lookup"><span data-stu-id="e5c88-198">This partitioner guarantees that the outputs of reduce i are all less than the output of reduce i+1.</span></span>

* <span data-ttu-id="e5c88-199">**TeraValidate**: programa de MapReduce que valida que la salida se ordene de manera global.</span><span class="sxs-lookup"><span data-stu-id="e5c88-199">**TeraValidate**: A MapReduce program that validates that the output is globally sorted</span></span>

    <span data-ttu-id="e5c88-200">Crea una asignación por archivo en el directorio de salida y cada asignación asegura que cada clave es menor o igual que la anterior.</span><span class="sxs-lookup"><span data-stu-id="e5c88-200">It creates one map per file in the output directory, and each map ensures that each key is less than or equal to the previous one.</span></span> <span data-ttu-id="e5c88-201">La función de asignación genera registros de la primera y última clave de cada archivo.</span><span class="sxs-lookup"><span data-stu-id="e5c88-201">The map function generates records of the first and last keys of each file.</span></span> <span data-ttu-id="e5c88-202">La función de reducción se asegura de que la primera clave del archivo i es mayor que la última clave del archivo i-1.</span><span class="sxs-lookup"><span data-stu-id="e5c88-202">The reduce function ensures that the first key of file i is greater than the last key of file i-1.</span></span> <span data-ttu-id="e5c88-203">Los problemas se notifican como una salida de la fase de reducción con las claves que no están en orden.</span><span class="sxs-lookup"><span data-stu-id="e5c88-203">Any problems are reported as an output of the reduce phase, with the keys that are out of order.</span></span>

<span data-ttu-id="e5c88-204">Utilice los siguientes pasos para generar datos, ordenarlos y, a continuación, validar el resultado:</span><span class="sxs-lookup"><span data-stu-id="e5c88-204">Use the following steps to generate data, sort, and then validate the output:</span></span>

1. <span data-ttu-id="e5c88-205">Genere 10 GB de datos que se almacenen en el almacenamiento predeterminado del clúster de HDInsight en `/example/data/10GB-sort-input`:</span><span class="sxs-lookup"><span data-stu-id="e5c88-205">Generate 10 GB of data, which is stored to the HDInsight cluster's default storage at `/example/data/10GB-sort-input`:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar teragen -Dmapred.map.tasks=50 100000000 /example/data/10GB-sort-input
    ```

    <span data-ttu-id="e5c88-206">`-Dmapred.map.tasks` indica a Hadoop cuántas tareas de asignación se usarán para el trabajo.</span><span class="sxs-lookup"><span data-stu-id="e5c88-206">The `-Dmapred.map.tasks` tells Hadoop how many map tasks to use for this job.</span></span> <span data-ttu-id="e5c88-207">Los dos parámetros finales indican al trabajo que cree 10 GB de datos y los almacene en `/example/data/10GB-sort-input`.</span><span class="sxs-lookup"><span data-stu-id="e5c88-207">The final two parameters instruct the job to create 10 GB of data and to store it at `/example/data/10GB-sort-input`.</span></span>

2. <span data-ttu-id="e5c88-208">Use el siguiente comando para ordenar los datos:</span><span class="sxs-lookup"><span data-stu-id="e5c88-208">Use the following command to sort the data:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar terasort -Dmapred.map.tasks=50 -Dmapred.reduce.tasks=25 /example/data/10GB-sort-input /example/data/10GB-sort-output
    ```

    <span data-ttu-id="e5c88-209">`-Dmapred.reduce.tasks` indica a Hadoop cuántas tareas de reducción se usarán para el trabajo.</span><span class="sxs-lookup"><span data-stu-id="e5c88-209">The `-Dmapred.reduce.tasks` tells Hadoop how many reduce tasks to use for the job.</span></span> <span data-ttu-id="e5c88-210">Los dos parámetros finales son simplemente las ubicaciones de entrada y salida de los datos.</span><span class="sxs-lookup"><span data-stu-id="e5c88-210">The final two parameters are just the input and output locations for data.</span></span>

3. <span data-ttu-id="e5c88-211">Use lo siguiente para validar los datos generados por la ordenación:</span><span class="sxs-lookup"><span data-stu-id="e5c88-211">Use the following to validate the data generated by the sort:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar teravalidate -Dmapred.map.tasks=50 -Dmapred.reduce.tasks=25 /example/data/10GB-sort-output /example/data/10GB-sort-validate
    ```

## <a name="next-steps"></a><span data-ttu-id="e5c88-212">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e5c88-212">Next steps</span></span>

<span data-ttu-id="e5c88-213">En este artículo, ha obtenido información acerca de cómo ejecutar los ejemplos incluidos en los clústeres de HDInsight basado en Linux.</span><span class="sxs-lookup"><span data-stu-id="e5c88-213">From this article, you learned how to run the samples included with the Linux-based HDInsight clusters.</span></span> <span data-ttu-id="e5c88-214">Para obtener acceso a tutoriales sobre cómo usar Pig, Hive y MapReduce con HDInsight, consulte los siguientes temas:</span><span class="sxs-lookup"><span data-stu-id="e5c88-214">For tutorials about using Pig, Hive, and MapReduce with HDInsight, see the following topics:</span></span>

* <span data-ttu-id="e5c88-215">[Uso de Pig con Hadoop en HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="e5c88-215">[Use Pig with Hadoop on HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="e5c88-216">[Uso de Hive con Hadoop en HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="e5c88-216">[Use Hive with Hadoop on HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="e5c88-217">[Uso de MapReduce con Hadoop en HDInsight][hdinsight-use-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="e5c88-217">[Use MapReduce with Hadoop on HDInsight][hdinsight-use-mapreduce]</span></span>

[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-sdk-documentation]: https://msdn.microsoft.com/library/azure/dn479185.aspx

[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-introduction]: hdinsight-hadoop-introduction.md



[hdinsight-samples]: hdinsight-run-samples.md

[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
