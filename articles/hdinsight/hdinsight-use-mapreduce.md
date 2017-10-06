---
title: aaaMapReduce con Hadoop en HDInsight | Documentos de Microsoft
description: "Obtenga información acerca de cómo trabajos toorun MapReduce en Hadoop en clústeres de HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 7f321501-d62c-4ffc-b5d6-102ecba6dd76
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: 0cf7ad0e6769e678be64f9e4ec8ed7a214ab7af2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-mapreduce-in-hadoop-on-hdinsight"></a><span data-ttu-id="6ec22-103">Uso de MapReduce en Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="6ec22-103">Use MapReduce in Hadoop on HDInsight</span></span>

<span data-ttu-id="6ec22-104">Obtenga información acerca de cómo trabajos toorun MapReduce en clústeres de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="6ec22-104">Learn how toorun MapReduce jobs on HDInsight clusters.</span></span> <span data-ttu-id="6ec22-105">Usar hello después hello toodiscover de tabla que MapReduce puede utilizarse con HDInsight de varias maneras:</span><span class="sxs-lookup"><span data-stu-id="6ec22-105">Use hello following table toodiscover hello various ways that MapReduce can be used with HDInsight:</span></span>

| <span data-ttu-id="6ec22-106">**Use esto**...</span><span class="sxs-lookup"><span data-stu-id="6ec22-106">**Use this**...</span></span> | <span data-ttu-id="6ec22-107">**.. .toodo esto**</span><span class="sxs-lookup"><span data-stu-id="6ec22-107">**...toodo this**</span></span> | <span data-ttu-id="6ec22-108">...con este **sistema operativo de clúster**</span><span class="sxs-lookup"><span data-stu-id="6ec22-108">...with this **cluster operating system**</span></span> | <span data-ttu-id="6ec22-109">...desde este **sistema operativo de cliente**</span><span class="sxs-lookup"><span data-stu-id="6ec22-109">...from this **client operating system**</span></span> |
|:--- |:--- |:--- |:--- |
| [<span data-ttu-id="6ec22-110">SSH</span><span class="sxs-lookup"><span data-stu-id="6ec22-110">SSH</span></span>](hdinsight-hadoop-use-mapreduce-ssh.md) |<span data-ttu-id="6ec22-111">Usar comandos de Hadoop de Hola a través de **SSH**</span><span class="sxs-lookup"><span data-stu-id="6ec22-111">Use hello Hadoop command through **SSH**</span></span> |<span data-ttu-id="6ec22-112">Linux</span><span class="sxs-lookup"><span data-stu-id="6ec22-112">Linux</span></span> |<span data-ttu-id="6ec22-113">Linux, Unix, Mac OS X o Windows</span><span class="sxs-lookup"><span data-stu-id="6ec22-113">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="6ec22-114">REST</span><span class="sxs-lookup"><span data-stu-id="6ec22-114">REST</span></span>](hdinsight-hadoop-use-mapreduce-curl.md) |<span data-ttu-id="6ec22-115">Enviar trabajo Hola de forma remota mediante **REST** (ejemplos usan cURL)</span><span class="sxs-lookup"><span data-stu-id="6ec22-115">Submit hello job remotely by using **REST** (examples use cURL)</span></span> |<span data-ttu-id="6ec22-116">Linux o Windows</span><span class="sxs-lookup"><span data-stu-id="6ec22-116">Linux or Windows</span></span> |<span data-ttu-id="6ec22-117">Linux, Unix, Mac OS X o Windows</span><span class="sxs-lookup"><span data-stu-id="6ec22-117">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="6ec22-118">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="6ec22-118">Windows PowerShell</span></span>](hdinsight-hadoop-use-mapreduce-powershell.md) |<span data-ttu-id="6ec22-119">Enviar trabajo Hola de forma remota mediante **Windows PowerShell**</span><span class="sxs-lookup"><span data-stu-id="6ec22-119">Submit hello job remotely by using **Windows PowerShell**</span></span> |<span data-ttu-id="6ec22-120">Linux o Windows</span><span class="sxs-lookup"><span data-stu-id="6ec22-120">Linux or Windows</span></span> |<span data-ttu-id="6ec22-121">Windows</span><span class="sxs-lookup"><span data-stu-id="6ec22-121">Windows</span></span> |
| <span data-ttu-id="6ec22-122">[Escritorio remoto](hdinsight-hadoop-use-mapreduce-remote-desktop.md) (HDInsight 3.2 y 3.3)</span><span class="sxs-lookup"><span data-stu-id="6ec22-122">[Remote Desktop](hdinsight-hadoop-use-mapreduce-remote-desktop.md) (HDInsight 3.2 and 3.3)</span></span> |<span data-ttu-id="6ec22-123">Usar comandos de Hadoop de Hola a través de **escritorio remoto**</span><span class="sxs-lookup"><span data-stu-id="6ec22-123">Use hello Hadoop command through **Remote Desktop**</span></span> |<span data-ttu-id="6ec22-124">Windows</span><span class="sxs-lookup"><span data-stu-id="6ec22-124">Windows</span></span> |<span data-ttu-id="6ec22-125">Windows</span><span class="sxs-lookup"><span data-stu-id="6ec22-125">Windows</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="6ec22-126">Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior.</span><span class="sxs-lookup"><span data-stu-id="6ec22-126">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="6ec22-127">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="6ec22-127">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="6ec22-128"><a id="whatis"></a>Qué es MapReduce</span><span class="sxs-lookup"><span data-stu-id="6ec22-128"><a id="whatis"></a>What is MapReduce</span></span>

<span data-ttu-id="6ec22-129">MapReduce de Hadoop es un marco de software para escribir trabajos que procesan enormes cantidades de datos.</span><span class="sxs-lookup"><span data-stu-id="6ec22-129">Hadoop MapReduce is a software framework for writing jobs that process vast amounts of data.</span></span> <span data-ttu-id="6ec22-130">Datos de entrada se dividen en fragmentos independientes, que, a continuación, se procesan en paralelo en todos los nodos de hello en el clúster.</span><span class="sxs-lookup"><span data-stu-id="6ec22-130">Input data is split into independent chunks, which are then processed in parallel across hello nodes in your cluster.</span></span> <span data-ttu-id="6ec22-131">Un trabajo de MapReduce consta de dos funciones:</span><span class="sxs-lookup"><span data-stu-id="6ec22-131">A MapReduce job consists of two functions:</span></span>

* <span data-ttu-id="6ec22-132">**Asignador**: consume datos de entrada, los analiza (normalmente con un filtro y operaciones de ordenación) y emite tuplas (pares de clave-valor)</span><span class="sxs-lookup"><span data-stu-id="6ec22-132">**Mapper**: Consumes input data, analyzes it (usually with filter and sorting operations), and emits tuples (key-value pairs)</span></span>

* <span data-ttu-id="6ec22-133">**Reductor**: consume tuplas emitidos por el asignador de Hola y realiza una operación de resumen que crea un resultado más pequeño y combinado de hello datos asignador</span><span class="sxs-lookup"><span data-stu-id="6ec22-133">**Reducer**: Consumes tuples emitted by hello Mapper and performs a summary operation that creates a smaller, combined result from hello Mapper data</span></span>

<span data-ttu-id="6ec22-134">Un ejemplo de trabajo de MapReduce de recuento word básico se muestra en hello siguiente diagrama:</span><span class="sxs-lookup"><span data-stu-id="6ec22-134">A basic word count MapReduce job example is illustrated in hello following diagram:</span></span>

![HDI.ProgramaRecuentoPalabras][image-hdi-wordcountdiagram]

<span data-ttu-id="6ec22-136">salida de Hello de este trabajo es un recuento de cuántas veces se produjo cada palabra en el texto hello que se analizó.</span><span class="sxs-lookup"><span data-stu-id="6ec22-136">hello output of this job is a count of how many times each word occurred in hello text that was analyzed.</span></span>

* <span data-ttu-id="6ec22-137">el asignador de Hello toma cada línea de texto de entrada de hello como entrada y lo divide en palabras.</span><span class="sxs-lookup"><span data-stu-id="6ec22-137">hello mapper takes each line from hello input text as an input and breaks it into words.</span></span> <span data-ttu-id="6ec22-138">Emite un clave y valor par cada vez que se produce una palabra de la palabra Hola va seguido de un 1.</span><span class="sxs-lookup"><span data-stu-id="6ec22-138">It emits a key/value pair each time a word occurs of hello word is followed by a 1.</span></span> <span data-ttu-id="6ec22-139">salida de Hello se ordena antes de enviarlo tooreducer.</span><span class="sxs-lookup"><span data-stu-id="6ec22-139">hello output is sorted before sending it tooreducer.</span></span>
* <span data-ttu-id="6ec22-140">reductor de Hello suma estos recuentos individuales para cada palabra y emite un par de clave/valor único que contiene la palabra Hola seguido de suma de Hola de sus repeticiones.</span><span class="sxs-lookup"><span data-stu-id="6ec22-140">hello reducer sums these individual counts for each word and emits a single key/value pair that contains hello word followed by hello sum of its occurrences.</span></span>

<span data-ttu-id="6ec22-141">MapReduce se puede implementar en varios lenguajes.</span><span class="sxs-lookup"><span data-stu-id="6ec22-141">MapReduce can be implemented in various languages.</span></span> <span data-ttu-id="6ec22-142">Java es la implementación más habitual de Hola y se usa para fines de demostración en este documento.</span><span class="sxs-lookup"><span data-stu-id="6ec22-142">Java is hello most common implementation, and is used for demonstration purposes in this document.</span></span>

## <a name="development-languages"></a><span data-ttu-id="6ec22-143">Lenguajes de desarrollo</span><span class="sxs-lookup"><span data-stu-id="6ec22-143">Development languages</span></span>

<span data-ttu-id="6ec22-144">Idiomas o marcos de trabajo que se basan en Java y Hola Máquina Virtual Java se pueda ejecutar directamente como un trabajo de MapReduce.</span><span class="sxs-lookup"><span data-stu-id="6ec22-144">Languages or frameworks that are based on Java and hello Java Virtual Machine can be ran directly as a MapReduce job.</span></span> <span data-ttu-id="6ec22-145">ejemplo de Hola usado en este documento es una aplicación de Java MapReduce.</span><span class="sxs-lookup"><span data-stu-id="6ec22-145">hello example used in this document is a Java MapReduce application.</span></span> <span data-ttu-id="6ec22-146">Los lenguajes que no son Java, como C# o Python, o ejecutables independientes, deben usar streaming de Hadoop.</span><span class="sxs-lookup"><span data-stu-id="6ec22-146">Non-Java languages, such as C#, Python, or standalone executables, must use Hadoop streaming.</span></span>

<span data-ttu-id="6ec22-147">Streaming de Hadoop se comunica con el asignador de Hola y reductor sobre STDIN y STDOUT.</span><span class="sxs-lookup"><span data-stu-id="6ec22-147">Hadoop streaming communicates with hello mapper and reducer over STDIN and STDOUT.</span></span> <span data-ttu-id="6ec22-148">reductor y el asignador de hello leen datos de una línea de STDIN al mismo tiempo y escribir hello tooSTDOUT de salida.</span><span class="sxs-lookup"><span data-stu-id="6ec22-148">hello mapper and reducer read data a line at a time from STDIN, and write hello output tooSTDOUT.</span></span> <span data-ttu-id="6ec22-149">Cada línea de lectura o emitidos por reductor y el asignador de hello debe estar en formato de Hola de un par de clave y valor delimitado por un carácter de tabulación:</span><span class="sxs-lookup"><span data-stu-id="6ec22-149">Each line read or emitted by hello mapper and reducer must be in hello format of a key/value pair, delimited by a tab character:</span></span>

    [key]/t[value]

<span data-ttu-id="6ec22-150">Para obtener más información, consulte [Streaming de Hadoop](http://hadoop.apache.org/docs/r1.2.1/streaming.html).</span><span class="sxs-lookup"><span data-stu-id="6ec22-150">For more information, see [Hadoop Streaming](http://hadoop.apache.org/docs/r1.2.1/streaming.html).</span></span>

<span data-ttu-id="6ec22-151">Para obtener ejemplos del uso de Hadoop con HDInsight de transmisión por secuencias, vea Hola siguientes documentos:</span><span class="sxs-lookup"><span data-stu-id="6ec22-151">For examples of using Hadoop streaming with HDInsight, see hello following documents:</span></span>

* [<span data-ttu-id="6ec22-152">Desarrollar trabajos de MapReduce de C#</span><span class="sxs-lookup"><span data-stu-id="6ec22-152">Develop C# MapReduce jobs</span></span>](hdinsight-hadoop-dotnet-csharp-mapreduce-streaming.md)

* [<span data-ttu-id="6ec22-153">Desarrollar trabajos de MapReduce de Python</span><span class="sxs-lookup"><span data-stu-id="6ec22-153">Develop Python MapReduce jobs</span></span>](hdinsight-hadoop-streaming-python.md)

## <span data-ttu-id="6ec22-154"><a id="data"></a>Datos de ejemplo</span><span class="sxs-lookup"><span data-stu-id="6ec22-154"><a id="data"></a>Example data</span></span>

<span data-ttu-id="6ec22-155">HDInsight proporciona diversos conjuntos de datos de ejemplo, que se almacenan en hello `/example/data` y `/HdiSamples` directory.</span><span class="sxs-lookup"><span data-stu-id="6ec22-155">HDInsight provides various example data sets, which are stored in hello `/example/data` and `/HdiSamples` directory.</span></span> <span data-ttu-id="6ec22-156">Son estos directorios en almacenamiento predeterminado de hello para el clúster.</span><span class="sxs-lookup"><span data-stu-id="6ec22-156">These directories are in hello default storage for your cluster.</span></span> <span data-ttu-id="6ec22-157">En este documento, se utiliza hello `/example/data/gutenberg/davinci.txt` archivo.</span><span class="sxs-lookup"><span data-stu-id="6ec22-157">In this document, we use hello `/example/data/gutenberg/davinci.txt` file.</span></span> <span data-ttu-id="6ec22-158">Este archivo contiene los blocs de notas de Hola de Leonardo Da Vinci.</span><span class="sxs-lookup"><span data-stu-id="6ec22-158">This file contains hello notebooks of Leonardo Da Vinci.</span></span>

## <span data-ttu-id="6ec22-159"><a id="job"></a>MapReduce de ejemplo</span><span class="sxs-lookup"><span data-stu-id="6ec22-159"><a id="job"></a>Example MapReduce</span></span>

<span data-ttu-id="6ec22-160">En el clúster de HDInsight se incluye un MapReduce de ejemplo de aplicación de recuento de palabras.</span><span class="sxs-lookup"><span data-stu-id="6ec22-160">An example MapReduce word count application is included with your HDInsight cluster.</span></span> <span data-ttu-id="6ec22-161">En este ejemplo se encuentra en `/example/jars/hadoop-mapreduce-examples.jar` en almacenamiento predeterminado de hello para el clúster.</span><span class="sxs-lookup"><span data-stu-id="6ec22-161">This example is located at `/example/jars/hadoop-mapreduce-examples.jar` on hello default storage for your cluster.</span></span>

<span data-ttu-id="6ec22-162">Hola después el código Java es el origen de Hola de hello aplicación MapReduce contenido en hello `hadoop-mapreduce-examples.jar` archivo:</span><span class="sxs-lookup"><span data-stu-id="6ec22-162">hello following Java code is hello source of hello MapReduce application contained in hello `hadoop-mapreduce-examples.jar` file:</span></span>

```java
package org.apache.hadoop.examples;

import java.io.IOException;
import java.util.StringTokenizer;

import org.apache.hadoop.conf.Configuration;
import org.apache.hadoop.fs.Path;
import org.apache.hadoop.io.IntWritable;
import org.apache.hadoop.io.Text;
import org.apache.hadoop.mapreduce.Job;
import org.apache.hadoop.mapreduce.Mapper;
import org.apache.hadoop.mapreduce.Reducer;
import org.apache.hadoop.mapreduce.lib.input.FileInputFormat;
import org.apache.hadoop.mapreduce.lib.output.FileOutputFormat;
import org.apache.hadoop.util.GenericOptionsParser;

public class WordCount {

    public static class TokenizerMapper
        extends Mapper<Object, Text, Text, IntWritable>{

    private final static IntWritable one = new IntWritable(1);
    private Text word = new Text();

    public void map(Object key, Text value, Context context
                    ) throws IOException, InterruptedException {
        StringTokenizer itr = new StringTokenizer(value.toString());
        while (itr.hasMoreTokens()) {
        word.set(itr.nextToken());
        context.write(word, one);
        }
    }
    }

    public static class IntSumReducer
        extends Reducer<Text,IntWritable,Text,IntWritable> {
    private IntWritable result = new IntWritable();

    public void reduce(Text key, Iterable<IntWritable> values,
                        Context context
                        ) throws IOException, InterruptedException {
        int sum = 0;
        for (IntWritable val : values) {
        sum += val.get();
        }
        result.set(sum);
        context.write(key, result);
    }
    }

    public static void main(String[] args) throws Exception {
    Configuration conf = new Configuration();
    String[] otherArgs = new GenericOptionsParser(conf, args).getRemainingArgs();
    if (otherArgs.length != 2) {
        System.err.println("Usage: wordcount <in> <out>");
        System.exit(2);
    }
    Job job = new Job(conf, "word count");
    job.setJarByClass(WordCount.class);
    job.setMapperClass(TokenizerMapper.class);
    job.setCombinerClass(IntSumReducer.class);
    job.setReducerClass(IntSumReducer.class);
    job.setOutputKeyClass(Text.class);
    job.setOutputValueClass(IntWritable.class);
    FileInputFormat.addInputPath(job, new Path(otherArgs[0]));
    FileOutputFormat.setOutputPath(job, new Path(otherArgs[1]));
    System.exit(job.waitForCompletion(true) ? 0 : 1);
    }
}
```

<span data-ttu-id="6ec22-163">Para instrucciones toowrite sus propias aplicaciones MapReduce, vea Hola siguientes documentos:</span><span class="sxs-lookup"><span data-stu-id="6ec22-163">For instructions toowrite your own MapReduce applications, see hello following documents:</span></span>

* [<span data-ttu-id="6ec22-164">Desarrollo de aplicaciones MapReduce de Java para HDInsight</span><span class="sxs-lookup"><span data-stu-id="6ec22-164">Develop Java MapReduce applications for HDInsight</span></span>](hdinsight-develop-deploy-java-mapreduce-linux.md)

* [<span data-ttu-id="6ec22-165">Desarrollo de aplicaciones MapReduce de Python para HDInsight</span><span class="sxs-lookup"><span data-stu-id="6ec22-165">Develop Python MapReduce applications for HDInsight</span></span>](hdinsight-hadoop-streaming-python.md)

## <span data-ttu-id="6ec22-166"><a id="run"></a>Ejecute hello MapReduce</span><span class="sxs-lookup"><span data-stu-id="6ec22-166"><a id="run"></a>Run hello MapReduce</span></span>

<span data-ttu-id="6ec22-167">HDInsight puede ejecutar trabajos de HiveQL mediante varios métodos.</span><span class="sxs-lookup"><span data-stu-id="6ec22-167">HDInsight can run HiveQL jobs by using various methods.</span></span> <span data-ttu-id="6ec22-168">Usar hello después toodecide tabla qué método es adecuado para usted, a continuación, siga el vínculo de Hola para ver un tutorial.</span><span class="sxs-lookup"><span data-stu-id="6ec22-168">Use hello following table toodecide which method is right for you, then follow hello link for a walkthrough.</span></span>

| <span data-ttu-id="6ec22-169">**Use esto**...</span><span class="sxs-lookup"><span data-stu-id="6ec22-169">**Use this**...</span></span> | <span data-ttu-id="6ec22-170">**.. .toodo esto**</span><span class="sxs-lookup"><span data-stu-id="6ec22-170">**...toodo this**</span></span> | <span data-ttu-id="6ec22-171">...con este **sistema operativo de clúster**</span><span class="sxs-lookup"><span data-stu-id="6ec22-171">...with this **cluster operating system**</span></span> | <span data-ttu-id="6ec22-172">...desde este **sistema operativo de cliente**</span><span class="sxs-lookup"><span data-stu-id="6ec22-172">...from this **client operating system**</span></span> |
|:--- |:--- |:--- |:--- |
| [<span data-ttu-id="6ec22-173">SSH</span><span class="sxs-lookup"><span data-stu-id="6ec22-173">SSH</span></span>](hdinsight-hadoop-use-mapreduce-ssh.md) |<span data-ttu-id="6ec22-174">Usar comandos de Hadoop de Hola a través de **SSH**</span><span class="sxs-lookup"><span data-stu-id="6ec22-174">Use hello Hadoop command through **SSH**</span></span> |<span data-ttu-id="6ec22-175">Linux</span><span class="sxs-lookup"><span data-stu-id="6ec22-175">Linux</span></span> |<span data-ttu-id="6ec22-176">Linux, Unix, Mac OS X o Windows</span><span class="sxs-lookup"><span data-stu-id="6ec22-176">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="6ec22-177">Curl</span><span class="sxs-lookup"><span data-stu-id="6ec22-177">Curl</span></span>](hdinsight-hadoop-use-mapreduce-curl.md) |<span data-ttu-id="6ec22-178">Enviar trabajo Hola de forma remota mediante **REST**</span><span class="sxs-lookup"><span data-stu-id="6ec22-178">Submit hello job remotely by using **REST**</span></span> |<span data-ttu-id="6ec22-179">Linux o Windows</span><span class="sxs-lookup"><span data-stu-id="6ec22-179">Linux or Windows</span></span> |<span data-ttu-id="6ec22-180">Linux, Unix, Mac OS X o Windows</span><span class="sxs-lookup"><span data-stu-id="6ec22-180">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="6ec22-181">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="6ec22-181">Windows PowerShell</span></span>](hdinsight-hadoop-use-mapreduce-powershell.md) |<span data-ttu-id="6ec22-182">Enviar trabajo Hola de forma remota mediante **Windows PowerShell**</span><span class="sxs-lookup"><span data-stu-id="6ec22-182">Submit hello job remotely by using **Windows PowerShell**</span></span> |<span data-ttu-id="6ec22-183">Linux o Windows</span><span class="sxs-lookup"><span data-stu-id="6ec22-183">Linux or Windows</span></span> |<span data-ttu-id="6ec22-184">Windows</span><span class="sxs-lookup"><span data-stu-id="6ec22-184">Windows</span></span> |
| <span data-ttu-id="6ec22-185">[Escritorio remoto](hdinsight-hadoop-use-mapreduce-remote-desktop.md) (HDInsight 3.2 y 3.3)</span><span class="sxs-lookup"><span data-stu-id="6ec22-185">[Remote Desktop](hdinsight-hadoop-use-mapreduce-remote-desktop.md) (HDInsight 3.2 and 3.3)</span></span> |<span data-ttu-id="6ec22-186">Usar comandos de Hadoop de Hola a través de **escritorio remoto**</span><span class="sxs-lookup"><span data-stu-id="6ec22-186">Use hello Hadoop command through **Remote Desktop**</span></span> |<span data-ttu-id="6ec22-187">Windows</span><span class="sxs-lookup"><span data-stu-id="6ec22-187">Windows</span></span> |<span data-ttu-id="6ec22-188">Windows</span><span class="sxs-lookup"><span data-stu-id="6ec22-188">Windows</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="6ec22-189">Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior.</span><span class="sxs-lookup"><span data-stu-id="6ec22-189">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="6ec22-190">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="6ec22-190">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="6ec22-191"><a id="nextsteps"></a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6ec22-191"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="6ec22-192">toolearn más acerca de cómo trabajar con datos en HDInsight, vea Hola siguientes documentos:</span><span class="sxs-lookup"><span data-stu-id="6ec22-192">toolearn more about working with data in HDInsight, see hello following documents:</span></span>

* [<span data-ttu-id="6ec22-193">Desarrollo de programas MapReduce de Java para HDInsight</span><span class="sxs-lookup"><span data-stu-id="6ec22-193">Develop Java MapReduce programs for HDInsight</span></span>](hdinsight-develop-deploy-java-mapreduce-linux.md)

* [<span data-ttu-id="6ec22-194">Desarrollo de programas de MapReduce de streaming de Python para HDInsight</span><span class="sxs-lookup"><span data-stu-id="6ec22-194">Develop Python streaming MapReduce programs for HDInsight</span></span>](hdinsight-hadoop-streaming-python.md)

* [<span data-ttu-id="6ec22-195">Desarrollo de trabajos de MapReduce de Scalding con Hadoop Apache en HDInsight</span><span class="sxs-lookup"><span data-stu-id="6ec22-195">Develop Scalding MapReduce jobs with Apache Hadoop on HDInsight</span></span>](hdinsight-hadoop-mapreduce-scalding.md)

* <span data-ttu-id="6ec22-196">[Uso de Hive con HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="6ec22-196">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>

* <span data-ttu-id="6ec22-197">[Uso de Pig con HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="6ec22-197">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>


[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-develop-mapreduce-jobs]: hdinsight-develop-deploy-java-mapreduce-linux.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md


[powershell-install-configure]: /powershell/azureps-cmdlets-docs

[image-hdi-wordcountdiagram]: ./media/hdinsight-use-mapreduce/HDI.WordCountDiagram.gif
