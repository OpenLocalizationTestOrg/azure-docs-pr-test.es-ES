---
title: ejemplos de Hadoop MapReduce aaaRun en HDInsight - Azure | Documentos de Microsoft
description: "Introducción al uso de ejemplos de MapReduce en archivos jar incluidos en HDInsight. Utilizar SSH tooconnect toohello clúster y, a continuación, utilice trabajos de ejemplo de Hola Hadoop comando toorun."
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
ms.openlocfilehash: 7a16bbd51eb17570fcaa3b1e0f5990fa889c106a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="run-hello-mapreduce-examples-included-in-hdinsight"></a><span data-ttu-id="3bd73-105">Ejecutar los ejemplos de hello MapReduce que se incluyen en HDInsight</span><span class="sxs-lookup"><span data-stu-id="3bd73-105">Run hello MapReduce examples included in HDInsight</span></span>

[!INCLUDE [samples-selector](../../includes/hdinsight-run-samples-selector.md)]

<span data-ttu-id="3bd73-106">Obtenga información acerca de cómo se incluyen ejemplos de MapReduce hello toorun con Hadoop en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3bd73-106">Learn how toorun hello MapReduce examples included with Hadoop on HDInsight.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3bd73-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="3bd73-107">Prerequisites</span></span>

* <span data-ttu-id="3bd73-108">**Un clúster de HDInsight**: consulte [Introducción al uso de Hadoop con Hive en HDInsight en Linux](hdinsight-hadoop-linux-tutorial-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="3bd73-108">**An HDInsight cluster**: See [Get started using Hadoop with Hive in HDInsight on Linux](hdinsight-hadoop-linux-tutorial-get-started.md)</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="3bd73-109">Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior.</span><span class="sxs-lookup"><span data-stu-id="3bd73-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="3bd73-110">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="3bd73-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="3bd73-111">**Un cliente SSH**: para obtener más información, consulte [Uso de SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="3bd73-111">**An SSH client**: For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <a name="hello-mapreduce-examples"></a><span data-ttu-id="3bd73-112">ejemplos de Hello MapReduce</span><span class="sxs-lookup"><span data-stu-id="3bd73-112">hello MapReduce examples</span></span>

<span data-ttu-id="3bd73-113">**Ubicación**: Hola ejemplos se encuentran en hello clúster de HDInsight en `/usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar`.</span><span class="sxs-lookup"><span data-stu-id="3bd73-113">**Location**: hello samples are located on hello HDInsight cluster at `/usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar`.</span></span>

<span data-ttu-id="3bd73-114">**Contenido**: Hola siguiendo los ejemplos incluido en este archivo:</span><span class="sxs-lookup"><span data-stu-id="3bd73-114">**Contents**: hello following samples are contained in this archive:</span></span>

* <span data-ttu-id="3bd73-115">`aggregatewordcount`: Un agregado según el programa de mapreduce que recuentos de palabras de hello en los archivos de entrada de Hola.</span><span class="sxs-lookup"><span data-stu-id="3bd73-115">`aggregatewordcount`: An Aggregate based mapreduce program that counts hello words in hello input files.</span></span>
* <span data-ttu-id="3bd73-116">`aggregatewordhist`: Un agregado según el programa de mapreduce que calcula el histograma de Hola de palabras de hello en los archivos de entrada de Hola.</span><span class="sxs-lookup"><span data-stu-id="3bd73-116">`aggregatewordhist`: An Aggregate based mapreduce program that computes hello histogram of hello words in hello input files.</span></span>
* <span data-ttu-id="3bd73-117">`bbp`: Un programa de mapreduce que utiliza Bailey-Borwein-Plouffe toocompute dígitos exactos de Pi.</span><span class="sxs-lookup"><span data-stu-id="3bd73-117">`bbp`: A mapreduce program that uses Bailey-Borwein-Plouffe toocompute exact digits of Pi.</span></span>
* <span data-ttu-id="3bd73-118">`dbcount`: Un trabajo de ejemplo que cuente los registros de la vista de página de hello almacenados en una base de datos.</span><span class="sxs-lookup"><span data-stu-id="3bd73-118">`dbcount`: An example job that counts hello pageview logs stored in a database.</span></span>
* <span data-ttu-id="3bd73-119">`distbbp`: Un programa de mapreduce que utiliza un tipo BBP toocompute fórmulas de bits exacto de Pi.</span><span class="sxs-lookup"><span data-stu-id="3bd73-119">`distbbp`: A mapreduce program that uses a BBP-type formula toocompute exact bits of Pi.</span></span>
* <span data-ttu-id="3bd73-120">`grep`: Un programa de mapreduce que cuente Hola coincide con de una expresión regular en la entrada de Hola.</span><span class="sxs-lookup"><span data-stu-id="3bd73-120">`grep`: A mapreduce program that counts hello matches of a regex in hello input.</span></span>
* <span data-ttu-id="3bd73-121">`join`: trabajo que realiza una unión de conjuntos de datos ordenados con particiones equiparables.</span><span class="sxs-lookup"><span data-stu-id="3bd73-121">`join`: A job that performs a join over sorted, equally partitioned datasets.</span></span>
* <span data-ttu-id="3bd73-122">`multifilewc`: trabajo que cuenta las palabras de varios archivos.</span><span class="sxs-lookup"><span data-stu-id="3bd73-122">`multifilewc`: A job that counts words from several files.</span></span>
* <span data-ttu-id="3bd73-123">`pentomino`: Un icono de mapreduce diseñar soluciones de programa toofind toopentomino problemas.</span><span class="sxs-lookup"><span data-stu-id="3bd73-123">`pentomino`: A mapreduce tile laying program toofind solutions toopentomino problems.</span></span>
* <span data-ttu-id="3bd73-124">`pi`: programa de mapreduce que calcula Pi mediante un método cuasi Monte Carlo.</span><span class="sxs-lookup"><span data-stu-id="3bd73-124">`pi`: A mapreduce program that estimates Pi using a quasi-Monte Carlo method.</span></span>
* <span data-ttu-id="3bd73-125">`randomtextwriter`: programa de mapreduce que escribe 10 GB de datos de texto aleatorios por nodo.</span><span class="sxs-lookup"><span data-stu-id="3bd73-125">`randomtextwriter`: A mapreduce program that writes 10 GB of random textual data per node.</span></span>
* <span data-ttu-id="3bd73-126">`randomwriter`: programa de mapreduce que escribe 10 GB de datos aleatorios por nodo.</span><span class="sxs-lookup"><span data-stu-id="3bd73-126">`randomwriter`: A mapreduce program that writes 10 GB of random data per node.</span></span>
* <span data-ttu-id="3bd73-127">`secondarysort`: Un ejemplo define una toohello de orden secundaria reducir fase.</span><span class="sxs-lookup"><span data-stu-id="3bd73-127">`secondarysort`: An example defining a secondary sort toohello reduce phase.</span></span>
* <span data-ttu-id="3bd73-128">`sort`: Un programa de mapreduce que ordena datos Hola escritos Hola de escritura aleatoria.</span><span class="sxs-lookup"><span data-stu-id="3bd73-128">`sort`: A mapreduce program that sorts hello data written by hello random writer.</span></span>
* <span data-ttu-id="3bd73-129">`sudoku`: solucionador de sudokus.</span><span class="sxs-lookup"><span data-stu-id="3bd73-129">`sudoku`: A sudoku solver.</span></span>
* <span data-ttu-id="3bd73-130">`teragen`: Generar datos para terasort Hola.</span><span class="sxs-lookup"><span data-stu-id="3bd73-130">`teragen`: Generate data for hello terasort.</span></span>
* <span data-ttu-id="3bd73-131">`terasort`: Ejecute hello terasort.</span><span class="sxs-lookup"><span data-stu-id="3bd73-131">`terasort`: Run hello terasort.</span></span>
* <span data-ttu-id="3bd73-132">`teravalidate`: comprueba los resultados de la ordenación de terabytes (terasort).</span><span class="sxs-lookup"><span data-stu-id="3bd73-132">`teravalidate`: Checking results of terasort.</span></span>
* <span data-ttu-id="3bd73-133">`wordcount`: Un programa de mapreduce que recuentos de palabras de hello en los archivos de entrada de Hola.</span><span class="sxs-lookup"><span data-stu-id="3bd73-133">`wordcount`: A mapreduce program that counts hello words in hello input files.</span></span>
* <span data-ttu-id="3bd73-134">`wordmean`: Un programa de mapreduce que cuenta la duración media de Hola de palabras de hello en los archivos de entrada de Hola.</span><span class="sxs-lookup"><span data-stu-id="3bd73-134">`wordmean`: A mapreduce program that counts hello average length of hello words in hello input files.</span></span>
* <span data-ttu-id="3bd73-135">`wordmedian`: Archivos de entrada un programa de mapreduce que cuenta la longitud de mediana de Hola de palabras de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="3bd73-135">`wordmedian`: A mapreduce program that counts hello median length of hello words in hello input files.</span></span>
* <span data-ttu-id="3bd73-136">`wordstandarddeviation`: Archivos de entrada un programa de mapreduce que cuenta la desviación estándar de Hola de longitud de Hola de palabras de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="3bd73-136">`wordstandarddeviation`: A mapreduce program that counts hello standard deviation of hello length of hello words in hello input files.</span></span>

<span data-ttu-id="3bd73-137">**El código fuente**: código fuente de estos ejemplos se incluye en hello clúster de HDInsight en `/usr/hdp/2.2.4.9-1/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples`.</span><span class="sxs-lookup"><span data-stu-id="3bd73-137">**Source code**: Source code for these samples is included on hello HDInsight cluster at `/usr/hdp/2.2.4.9-1/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples`.</span></span>

> [!NOTE]
> <span data-ttu-id="3bd73-138">Hola `2.2.4.9-1` Hola ruta de acceso es la versión de Hola de hello Hortonworks Data Platform para clúster de HDInsight de Hola y pueden ser diferente para el clúster.</span><span class="sxs-lookup"><span data-stu-id="3bd73-138">hello `2.2.4.9-1` in hello path is hello version of hello Hortonworks Data Platform for hello HDInsight cluster, and may be different for your cluster.</span></span>

## <a name="run-hello-wordcount-example"></a><span data-ttu-id="3bd73-139">Ejecutar el ejemplo de wordcount Hola</span><span class="sxs-lookup"><span data-stu-id="3bd73-139">Run hello wordcount example</span></span>

1. <span data-ttu-id="3bd73-140">Conectar tooHDInsight mediante SSH.</span><span class="sxs-lookup"><span data-stu-id="3bd73-140">Connect tooHDInsight using SSH.</span></span> <span data-ttu-id="3bd73-141">Para más información, consulte [Uso SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="3bd73-141">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="3bd73-142">De hello `username@#######:~$` símbolo del sistema, use Hola siguiendo los ejemplos del comando toolist hello:</span><span class="sxs-lookup"><span data-stu-id="3bd73-142">From hello `username@#######:~$` prompt, use hello following command toolist hello samples:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar
    ```

    <span data-ttu-id="3bd73-143">Este comando genera lista Hola de ejemplo desde la sección anterior de Hola de este documento.</span><span class="sxs-lookup"><span data-stu-id="3bd73-143">This command generates hello list of sample from hello previous section of this document.</span></span>

3. <span data-ttu-id="3bd73-144">Hola de uso siguiente comando tooget ayuda de un ejemplo concreto.</span><span class="sxs-lookup"><span data-stu-id="3bd73-144">Use hello following command tooget help on a specific sample.</span></span> <span data-ttu-id="3bd73-145">En este caso, Hola **wordcount** ejemplo:</span><span class="sxs-lookup"><span data-stu-id="3bd73-145">In this case, hello **wordcount** sample:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount
    ```

    <span data-ttu-id="3bd73-146">Recibirá el siguiente mensaje de Hola:</span><span class="sxs-lookup"><span data-stu-id="3bd73-146">You receive hello following message:</span></span>

        Usage: wordcount <in> [<in>...] <out>

    <span data-ttu-id="3bd73-147">Este mensaje indica que puede proporcionar varias rutas de acceso de entrada para los documentos de origen de Hola.</span><span class="sxs-lookup"><span data-stu-id="3bd73-147">This message indicates that you can provide several input paths for hello source documents.</span></span> <span data-ttu-id="3bd73-148">ruta de acceso final Hello es donde se almacena el resultado de hello (recuento de palabras en documentos de origen de hello).</span><span class="sxs-lookup"><span data-stu-id="3bd73-148">hello final path is where hello output (count of words in hello source documents) is stored.</span></span>

4. <span data-ttu-id="3bd73-149">Usar hello después toocount todas las palabras en hello blocs de notas de Leonardo Da Vinci, que se proporcionan como datos de ejemplo con el clúster:</span><span class="sxs-lookup"><span data-stu-id="3bd73-149">Use hello following toocount all words in hello Notebooks of Leonardo Da Vinci, which are provided as sample data with your cluster:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/davinciwordcount
    ```

    <span data-ttu-id="3bd73-150">La entrada de este trabajo se lee desde `/example/data/gutenberg/davinci.txt`.</span><span class="sxs-lookup"><span data-stu-id="3bd73-150">Input for this job is read from `/example/data/gutenberg/davinci.txt`.</span></span> <span data-ttu-id="3bd73-151">La salida de este ejemplo se almacena en `/example/data/davinciwordcount`.</span><span class="sxs-lookup"><span data-stu-id="3bd73-151">Output for this example is stored in `/example/data/davinciwordcount`.</span></span> <span data-ttu-id="3bd73-152">Ambas rutas de acceso se encuentran en almacenamiento predeterminado para el clúster de hello, no el sistema de archivos local Hola.</span><span class="sxs-lookup"><span data-stu-id="3bd73-152">Both paths are located on default storage for hello cluster, not hello local file system.</span></span>

   > [!NOTE]
   > <span data-ttu-id="3bd73-153">Como se indicó en la Ayuda de hello para el ejemplo de wordcount hello, también puede especificar varios archivos de entrada.</span><span class="sxs-lookup"><span data-stu-id="3bd73-153">As noted in hello help for hello wordcount sample, you could also specify multiple input files.</span></span> <span data-ttu-id="3bd73-154">Por ejemplo, `hadoop jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/gutenberg/ulysses.txt /example/data/twowordcount` contaría las palabras de davinci.txt y ulysses.txt.</span><span class="sxs-lookup"><span data-stu-id="3bd73-154">For example, `hadoop jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/gutenberg/ulysses.txt /example/data/twowordcount` would count words in both davinci.txt and ulysses.txt.</span></span>

5. <span data-ttu-id="3bd73-155">Cuando se completa el trabajo de hello, utilice Hola siguiendo la salida del comando tooview hello:</span><span class="sxs-lookup"><span data-stu-id="3bd73-155">Once hello job completes, use hello following command tooview hello output:</span></span>

    ```bash
    hdfs dfs -cat /example/data/davinciwordcount/*
    ```

    <span data-ttu-id="3bd73-156">Este comando concatena todos los archivos de salida de hello generados por el trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="3bd73-156">This command concatenates all hello output files produced by hello job.</span></span> <span data-ttu-id="3bd73-157">Muestra la consola de toohello de salida de hello.</span><span class="sxs-lookup"><span data-stu-id="3bd73-157">It displays hello output toohello console.</span></span> <span data-ttu-id="3bd73-158">Hola de salida es toohello similar siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="3bd73-158">hello output is similar toohello following text:</span></span>

        zum     1
        zur     1
        zwanzig 1
        zweite  1

    <span data-ttu-id="3bd73-159">Cada línea representa una palabra y cuántas veces se produjo en hello los datos de entrada.</span><span class="sxs-lookup"><span data-stu-id="3bd73-159">Each line represents a word and how many times it occurred in hello input data.</span></span>

## <a name="hello-sudoku-example"></a><span data-ttu-id="3bd73-160">ejemplo de Hola Sudoku</span><span class="sxs-lookup"><span data-stu-id="3bd73-160">hello Sudoku example</span></span>

<span data-ttu-id="3bd73-161">[Sudoku](https://en.wikipedia.org/wiki/Sudoku) es un rompecabezas lógico compuesto por nueve cuadrículas de 3 × 3.</span><span class="sxs-lookup"><span data-stu-id="3bd73-161">[Sudoku](https://en.wikipedia.org/wiki/Sudoku) is a logic puzzle made up of nine 3x3 grids.</span></span> <span data-ttu-id="3bd73-162">Algunas celdas de cuadrícula de Hola tienen números, mientras que otros están en blanco y objetivo de hello es toosolve para las celdas en blanco de Hola.</span><span class="sxs-lookup"><span data-stu-id="3bd73-162">Some cells in hello grid have numbers, while others are blank, and hello goal is toosolve for hello blank cells.</span></span> <span data-ttu-id="3bd73-163">el vínculo anterior de Hello tiene más información sobre rompecabezas de hello, pero Hola de este ejemplo sirve toosolve para las celdas en blanco de Hola.</span><span class="sxs-lookup"><span data-stu-id="3bd73-163">hello previous link has more information on hello puzzle, but hello purpose of this sample is toosolve for hello blank cells.</span></span> <span data-ttu-id="3bd73-164">Por lo que la entrada debería ser un archivo que se encuentra en hello siguiendo el formato:</span><span class="sxs-lookup"><span data-stu-id="3bd73-164">So our input should be a file that is in hello following format:</span></span>

* <span data-ttu-id="3bd73-165">Nueve filas de nueve columnas;</span><span class="sxs-lookup"><span data-stu-id="3bd73-165">Nine rows of nine columns</span></span>
* <span data-ttu-id="3bd73-166">Cada columna puede contener un número o `?` (que indica una celda en blanco);</span><span class="sxs-lookup"><span data-stu-id="3bd73-166">Each column can contain either a number or `?` (which indicates a blank cell)</span></span>
* <span data-ttu-id="3bd73-167">Las celdas se separan por un espacio.</span><span class="sxs-lookup"><span data-stu-id="3bd73-167">Cells are separated by a space</span></span>

<span data-ttu-id="3bd73-168">Hay un determinado tooconstruct de manera rompecabezas Sudoku; no puede repetirse un número en una columna o fila.</span><span class="sxs-lookup"><span data-stu-id="3bd73-168">There is a certain way tooconstruct Sudoku puzzles; you can't repeat a number in a column or row.</span></span> <span data-ttu-id="3bd73-169">Hay un ejemplo en clúster de HDInsight de Hola que se cree correctamente.</span><span class="sxs-lookup"><span data-stu-id="3bd73-169">There's an example on hello HDInsight cluster that is properly constructed.</span></span> <span data-ttu-id="3bd73-170">Se encuentra en `/usr/hdp/*/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples/src/main/java/org/apache/hadoop/examples/dancing/puzzle1.dta` y contiene Hola siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="3bd73-170">It is located at `/usr/hdp/*/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples/src/main/java/org/apache/hadoop/examples/dancing/puzzle1.dta` and contains hello following text:</span></span>

    8 5 ? 3 9 ? ? ? ?
    ? ? 2 ? ? ? ? ? ?
    ? ? 6 ? 1 ? ? ? 2
    ? ? 4 ? ? 3 ? 5 9
    ? ? 8 9 ? 1 4 ? ?
    3 2 ? 4 ? ? 8 ? ?
    9 ? ? ? 8 ? 5 ? ?
    ? ? ? ? ? ? 2 ? ?
    ? ? ? ? 4 5 ? 7 8

<span data-ttu-id="3bd73-171">Este problema de ejemplo a través de hello ejemplo Sudoku, toorun, utilice Hola comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="3bd73-171">toorun this example problem through hello Sudoku example, use hello following command:</span></span>

```bash
yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar sudoku /usr/hdp/*/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples/src/main/java/org/apache/hadoop/examples/dancing/puzzle1.dta
```

<span data-ttu-id="3bd73-172">resultados de Hello aparecen toohello similar siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="3bd73-172">hello results appear similar toohello following text:</span></span>

    8 5 1 3 9 2 6 4 7
    4 3 2 6 7 8 1 9 5
    7 9 6 5 1 4 3 8 2
    6 1 4 8 2 3 7 5 9
    5 7 8 9 6 1 4 2 3
    3 2 9 4 5 7 8 1 6
    9 4 7 2 8 6 5 3 1
    1 8 5 7 3 9 2 6 4
    2 6 3 1 4 5 9 7 8

## <a name="pi--example"></a><span data-ttu-id="3bd73-173">Ejemplo de PI (π)</span><span class="sxs-lookup"><span data-stu-id="3bd73-173">Pi (π) example</span></span>

<span data-ttu-id="3bd73-174">ejemplo de Hola a pi usa una estadística (tipo de Monte Carlo) valor del método tooestimate Hola de pi.</span><span class="sxs-lookup"><span data-stu-id="3bd73-174">hello pi sample uses a statistical (quasi-Monte Carlo) method tooestimate hello value of pi.</span></span> <span data-ttu-id="3bd73-175">Los puntos se colocan de forma aleatoria en un cuadrado unitario.</span><span class="sxs-lookup"><span data-stu-id="3bd73-175">Points are placed at random in a unit square.</span></span> <span data-ttu-id="3bd73-176">cuadrado de Hello también contiene un círculo.</span><span class="sxs-lookup"><span data-stu-id="3bd73-176">hello square also contains a circle.</span></span> <span data-ttu-id="3bd73-177">probabilidad de que los puntos de Hola se sitúan dentro de círculo Hola Hola son toohello igual área no cliente de hello circle, pi/4.</span><span class="sxs-lookup"><span data-stu-id="3bd73-177">hello probability that hello points fall within hello circle are equal toohello area of hello circle, pi/4.</span></span> <span data-ttu-id="3bd73-178">valor de Hola de pi se puede estimar de valor de Hola de 4R.</span><span class="sxs-lookup"><span data-stu-id="3bd73-178">hello value of pi can be estimated from hello value of 4R.</span></span> <span data-ttu-id="3bd73-179">R es la relación de hello del número de Hola de puntos que están dentro de círculo hello toohello número total de puntos que están dentro de cuadrado Hola.</span><span class="sxs-lookup"><span data-stu-id="3bd73-179">R is hello ratio of hello number of points that are inside hello circle toohello total number of points that are within hello square.</span></span> <span data-ttu-id="3bd73-180">Hola Hola muestra de mayor tamaño puntos usados, que es mejor estimación de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="3bd73-180">hello larger hello sample of points used, hello better hello estimate is.</span></span>

<span data-ttu-id="3bd73-181">Use este ejemplo de Hola después toorun de comando.</span><span class="sxs-lookup"><span data-stu-id="3bd73-181">Use hello following command toorun this sample.</span></span> <span data-ttu-id="3bd73-182">Este comando utiliza 16 mapas con el valor de 10.000.000 ejemplos tooestimate Hola de pi:</span><span class="sxs-lookup"><span data-stu-id="3bd73-182">This command uses 16 maps with 10,000,000 samples each tooestimate hello value of pi:</span></span>

```bash
yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar pi 16 10000000
```

<span data-ttu-id="3bd73-183">Hello valor devuelto por este comando es similar demasiado**3.14159155000000000000**.</span><span class="sxs-lookup"><span data-stu-id="3bd73-183">hello value returned by this command is similar too**3.14159155000000000000**.</span></span> <span data-ttu-id="3bd73-184">Para las referencias, hello 10 primeros decimales de pi son 3.1415926535.</span><span class="sxs-lookup"><span data-stu-id="3bd73-184">For references, hello first 10 decimal places of pi are 3.1415926535.</span></span>

## <a name="10-gb-greysort-example"></a><span data-ttu-id="3bd73-185">Ejemplo de Greysort de 10 GB</span><span class="sxs-lookup"><span data-stu-id="3bd73-185">10 GB Greysort example</span></span>

<span data-ttu-id="3bd73-186">GraySort es una ordenación de pruebas comparativas.</span><span class="sxs-lookup"><span data-stu-id="3bd73-186">GraySort is a benchmark sort.</span></span> <span data-ttu-id="3bd73-187">métrica de Hello es la tasa de ordenación de hello (TB/minuto) que se logra al ordenar grandes cantidades de datos, normalmente un 100 TB mínimo.</span><span class="sxs-lookup"><span data-stu-id="3bd73-187">hello metric is hello sort rate (TB/minute) that is achieved while sorting large amounts of data, usually a 100 TB minimum.</span></span>

<span data-ttu-id="3bd73-188">Este ejemplo utiliza solo 10 GB de datos, para así poder ejecutarlo relativamente rápido.</span><span class="sxs-lookup"><span data-stu-id="3bd73-188">This sample uses a modest 10 GB of data so that it can be run relatively quickly.</span></span> <span data-ttu-id="3bd73-189">Usa las aplicaciones de MapReduce Hola desarrolladas por Owen O'Malley y Arun Murthy.</span><span class="sxs-lookup"><span data-stu-id="3bd73-189">It uses hello MapReduce applications developed by Owen O'Malley and Arun Murthy.</span></span> <span data-ttu-id="3bd73-190">Estas aplicaciones habían ganado el criterio de referencia de hello anual uso general ("daytona") terabyte ordenación en 2009, con una velocidad de 0.578 TB/min (100 TB en 173 minutos).</span><span class="sxs-lookup"><span data-stu-id="3bd73-190">These applications won hello annual general-purpose ("daytona") terabyte sort benchmark in 2009, with a rate of 0.578 TB/min (100 TB in 173 minutes).</span></span> <span data-ttu-id="3bd73-191">Para obtener más información sobre este y otros criterios de ordenación de referencia, vea hello [Sortbenchmark](http://sortbenchmark.org/) sitio.</span><span class="sxs-lookup"><span data-stu-id="3bd73-191">For more information on this and other sorting benchmarks, see hello [Sortbenchmark](http://sortbenchmark.org/) site.</span></span>

<span data-ttu-id="3bd73-192">Este ejemplo utiliza tres conjuntos de programas de MapReduce:</span><span class="sxs-lookup"><span data-stu-id="3bd73-192">This sample uses three sets of MapReduce programs:</span></span>

* <span data-ttu-id="3bd73-193">**TeraGen**: MapReduce de un programa que genera filas de datos toosort</span><span class="sxs-lookup"><span data-stu-id="3bd73-193">**TeraGen**: A MapReduce program that generates rows of data toosort</span></span>

* <span data-ttu-id="3bd73-194">**TeraSort**: ejemplos de datos de entrada de Hola y utiliza datos de hello toosort MapReduce en un orden total</span><span class="sxs-lookup"><span data-stu-id="3bd73-194">**TeraSort**: Samples hello input data and uses MapReduce toosort hello data into a total order</span></span>

    <span data-ttu-id="3bd73-195">TeraSort es una ordenación MapReduce estándar, salvo por el particionador personalizado.</span><span class="sxs-lookup"><span data-stu-id="3bd73-195">TeraSort is a standard MapReduce sort, except for a custom partitioner.</span></span> <span data-ttu-id="3bd73-196">particionador de Hello usa una lista ordenada de claves de n-1 muestreada que definen el intervalo de claves de Hola para cada reduce.</span><span class="sxs-lookup"><span data-stu-id="3bd73-196">hello partitioner uses a sorted list of N-1 sampled keys that define hello key range for each reduce.</span></span> <span data-ttu-id="3bd73-197">En particular, todas las claves de este tipo que muestra [i-1] < = clave < [i] de ejemplo se envían tooreduce.</span><span class="sxs-lookup"><span data-stu-id="3bd73-197">In particular, all keys such that sample[i-1] <= key < sample[i] are sent tooreduce i.</span></span> <span data-ttu-id="3bd73-198">Este particionador garantiza que las salidas de Hola de reducen i es todos los menores de reducir la salida de hello de i + 1.</span><span class="sxs-lookup"><span data-stu-id="3bd73-198">This partitioner guarantees that hello outputs of reduce i are all less than hello output of reduce i+1.</span></span>

* <span data-ttu-id="3bd73-199">**TeraValidate**: MapReduce de un programa que valida que los resultados del Hola global está ordenada</span><span class="sxs-lookup"><span data-stu-id="3bd73-199">**TeraValidate**: A MapReduce program that validates that hello output is globally sorted</span></span>

    <span data-ttu-id="3bd73-200">Crea una asignación por cada archivo en el directorio de salida de hello, y cada asignación garantiza que cada clave es menor o igual toohello anterior.</span><span class="sxs-lookup"><span data-stu-id="3bd73-200">It creates one map per file in hello output directory, and each map ensures that each key is less than or equal toohello previous one.</span></span> <span data-ttu-id="3bd73-201">función de asignación de Hello genera registros de hello primero y último claves de cada archivo.</span><span class="sxs-lookup"><span data-stu-id="3bd73-201">hello map function generates records of hello first and last keys of each file.</span></span> <span data-ttu-id="3bd73-202">Hola reduce (función) garantiza que Hola primera clave de archivo i es mayor que la clave de la última Hola de i-1 de archivo.</span><span class="sxs-lookup"><span data-stu-id="3bd73-202">hello reduce function ensures that hello first key of file i is greater than hello last key of file i-1.</span></span> <span data-ttu-id="3bd73-203">Los problemas se notifican como una salida de hello reducir la fase, con claves de Hola que no están ordenadas.</span><span class="sxs-lookup"><span data-stu-id="3bd73-203">Any problems are reported as an output of hello reduce phase, with hello keys that are out of order.</span></span>

<span data-ttu-id="3bd73-204">Use Hola siguientes pasos le indican datos toogenerate, ordenar y, a continuación, validar salida de hello:</span><span class="sxs-lookup"><span data-stu-id="3bd73-204">Use hello following steps toogenerate data, sort, and then validate hello output:</span></span>

1. <span data-ttu-id="3bd73-205">Generar 10 GB de datos, que es el almacenamiento de forma predeterminada del clúster de HDInsight de toohello almacenado en `/example/data/10GB-sort-input`:</span><span class="sxs-lookup"><span data-stu-id="3bd73-205">Generate 10 GB of data, which is stored toohello HDInsight cluster's default storage at `/example/data/10GB-sort-input`:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar teragen -Dmapred.map.tasks=50 100000000 /example/data/10GB-sort-input
    ```

    <span data-ttu-id="3bd73-206">Hola `-Dmapred.map.tasks` indica cuántos toouse de tareas de asignación para este trabajo de Hadoop.</span><span class="sxs-lookup"><span data-stu-id="3bd73-206">hello `-Dmapred.map.tasks` tells Hadoop how many map tasks toouse for this job.</span></span> <span data-ttu-id="3bd73-207">parámetros de Hello dos final indicar Hola trabajo toocreate 10 GB de datos y toostore en `/example/data/10GB-sort-input`.</span><span class="sxs-lookup"><span data-stu-id="3bd73-207">hello final two parameters instruct hello job toocreate 10 GB of data and toostore it at `/example/data/10GB-sort-input`.</span></span>

2. <span data-ttu-id="3bd73-208">Usar hello comando toosort Hola datos siguientes:</span><span class="sxs-lookup"><span data-stu-id="3bd73-208">Use hello following command toosort hello data:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar terasort -Dmapred.map.tasks=50 -Dmapred.reduce.tasks=25 /example/data/10GB-sort-input /example/data/10GB-sort-output
    ```

    <span data-ttu-id="3bd73-209">Hola `-Dmapred.reduce.tasks` indica Hadoop cuántos reducen toouse de tareas de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="3bd73-209">hello `-Dmapred.reduce.tasks` tells Hadoop how many reduce tasks toouse for hello job.</span></span> <span data-ttu-id="3bd73-210">Hola dos últimos parámetros Hola solo entrada y ubicaciones de los datos de salida.</span><span class="sxs-lookup"><span data-stu-id="3bd73-210">hello final two parameters are just hello input and output locations for data.</span></span>

3. <span data-ttu-id="3bd73-211">Usar hello toovalidate Hola datos generados por orden de hello siguientes:</span><span class="sxs-lookup"><span data-stu-id="3bd73-211">Use hello following toovalidate hello data generated by hello sort:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar teravalidate -Dmapred.map.tasks=50 -Dmapred.reduce.tasks=25 /example/data/10GB-sort-output /example/data/10GB-sort-validate
    ```

## <a name="next-steps"></a><span data-ttu-id="3bd73-212">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3bd73-212">Next steps</span></span>

<span data-ttu-id="3bd73-213">De este artículo, ha aprendido cómo ejemplos de hello toorun incluyen con hello clústeres de HDInsight basados en Linux.</span><span class="sxs-lookup"><span data-stu-id="3bd73-213">From this article, you learned how toorun hello samples included with hello Linux-based HDInsight clusters.</span></span> <span data-ttu-id="3bd73-214">Para ver los tutoriales sobre el uso de Pig, Hive y MapReduce con HDInsight, vea Hola temas siguientes:</span><span class="sxs-lookup"><span data-stu-id="3bd73-214">For tutorials about using Pig, Hive, and MapReduce with HDInsight, see hello following topics:</span></span>

* <span data-ttu-id="3bd73-215">[Uso de Pig con Hadoop en HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="3bd73-215">[Use Pig with Hadoop on HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="3bd73-216">[Uso de Hive con Hadoop en HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="3bd73-216">[Use Hive with Hadoop on HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="3bd73-217">[Uso de MapReduce con Hadoop en HDInsight][hdinsight-use-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="3bd73-217">[Use MapReduce with Hadoop on HDInsight][hdinsight-use-mapreduce]</span></span>

[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-sdk-documentation]: https://msdn.microsoft.com/library/azure/dn479185.aspx

[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-introduction]: hdinsight-hadoop-introduction.md



[hdinsight-samples]: hdinsight-run-samples.md

[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
