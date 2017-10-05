---
title: MapReduce con Hadoop en HDInsight | Microsoft Docs
description: "Obtenga información sobre cómo ejecutar trabajos de MapReduce en Hadoop en clústeres de HDInsight."
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
ms.openlocfilehash: df8ac578a56de72df667b1fa7f90f981c79d9999
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="use-mapreduce-in-hadoop-on-hdinsight"></a><span data-ttu-id="25fa5-103">Uso de MapReduce en Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="25fa5-103">Use MapReduce in Hadoop on HDInsight</span></span>

<span data-ttu-id="25fa5-104">Obtenga información sobre cómo ejecutar trabajos de MapReduce en clústeres de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="25fa5-104">Learn how to run MapReduce jobs on HDInsight clusters.</span></span> <span data-ttu-id="25fa5-105">Utilice la tabla siguiente para conocer las distintas formas de usar MapReduce con HDInsight:</span><span class="sxs-lookup"><span data-stu-id="25fa5-105">Use the following table to discover the various ways that MapReduce can be used with HDInsight:</span></span>

| <span data-ttu-id="25fa5-106">**Use esto**...</span><span class="sxs-lookup"><span data-stu-id="25fa5-106">**Use this**...</span></span> | <span data-ttu-id="25fa5-107">**...para hacer esto**</span><span class="sxs-lookup"><span data-stu-id="25fa5-107">**...to do this**</span></span> | <span data-ttu-id="25fa5-108">...con este **sistema operativo de clúster**</span><span class="sxs-lookup"><span data-stu-id="25fa5-108">...with this **cluster operating system**</span></span> | <span data-ttu-id="25fa5-109">...desde este **sistema operativo de cliente**</span><span class="sxs-lookup"><span data-stu-id="25fa5-109">...from this **client operating system**</span></span> |
|:--- |:--- |:--- |:--- |
| [<span data-ttu-id="25fa5-110">SSH</span><span class="sxs-lookup"><span data-stu-id="25fa5-110">SSH</span></span>](hdinsight-hadoop-use-mapreduce-ssh.md) |<span data-ttu-id="25fa5-111">Uso del comando Hadoop mediante **SSH**</span><span class="sxs-lookup"><span data-stu-id="25fa5-111">Use the Hadoop command through **SSH**</span></span> |<span data-ttu-id="25fa5-112">Linux</span><span class="sxs-lookup"><span data-stu-id="25fa5-112">Linux</span></span> |<span data-ttu-id="25fa5-113">Linux, Unix, Mac OS X o Windows</span><span class="sxs-lookup"><span data-stu-id="25fa5-113">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="25fa5-114">REST</span><span class="sxs-lookup"><span data-stu-id="25fa5-114">REST</span></span>](hdinsight-hadoop-use-mapreduce-curl.md) |<span data-ttu-id="25fa5-115">Enviar el trabajo de forma remota mediante **REST** (los ejemplos usan cURL)</span><span class="sxs-lookup"><span data-stu-id="25fa5-115">Submit the job remotely by using **REST** (examples use cURL)</span></span> |<span data-ttu-id="25fa5-116">Linux o Windows</span><span class="sxs-lookup"><span data-stu-id="25fa5-116">Linux or Windows</span></span> |<span data-ttu-id="25fa5-117">Linux, Unix, Mac OS X o Windows</span><span class="sxs-lookup"><span data-stu-id="25fa5-117">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="25fa5-118">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="25fa5-118">Windows PowerShell</span></span>](hdinsight-hadoop-use-mapreduce-powershell.md) |<span data-ttu-id="25fa5-119">Enviar el trabajo de forma remota mediante **Windows PowerShell**</span><span class="sxs-lookup"><span data-stu-id="25fa5-119">Submit the job remotely by using **Windows PowerShell**</span></span> |<span data-ttu-id="25fa5-120">Linux o Windows</span><span class="sxs-lookup"><span data-stu-id="25fa5-120">Linux or Windows</span></span> |<span data-ttu-id="25fa5-121">Windows</span><span class="sxs-lookup"><span data-stu-id="25fa5-121">Windows</span></span> |
| <span data-ttu-id="25fa5-122">[Escritorio remoto](hdinsight-hadoop-use-mapreduce-remote-desktop.md) (HDInsight 3.2 y 3.3)</span><span class="sxs-lookup"><span data-stu-id="25fa5-122">[Remote Desktop](hdinsight-hadoop-use-mapreduce-remote-desktop.md) (HDInsight 3.2 and 3.3)</span></span> |<span data-ttu-id="25fa5-123">Uso del comando Hadoop mediante **Escritorio remoto**</span><span class="sxs-lookup"><span data-stu-id="25fa5-123">Use the Hadoop command through **Remote Desktop**</span></span> |<span data-ttu-id="25fa5-124">Windows</span><span class="sxs-lookup"><span data-stu-id="25fa5-124">Windows</span></span> |<span data-ttu-id="25fa5-125">Windows</span><span class="sxs-lookup"><span data-stu-id="25fa5-125">Windows</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="25fa5-126">Linux es el único sistema operativo que se usa en la versión 3.4 de HDInsight, o en las superiores.</span><span class="sxs-lookup"><span data-stu-id="25fa5-126">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="25fa5-127">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="25fa5-127">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="25fa5-128"><a id="whatis"></a>Qué es MapReduce</span><span class="sxs-lookup"><span data-stu-id="25fa5-128"><a id="whatis"></a>What is MapReduce</span></span>

<span data-ttu-id="25fa5-129">MapReduce de Hadoop es un marco de software para escribir trabajos que procesan enormes cantidades de datos.</span><span class="sxs-lookup"><span data-stu-id="25fa5-129">Hadoop MapReduce is a software framework for writing jobs that process vast amounts of data.</span></span> <span data-ttu-id="25fa5-130">La entrada de datos se divide en fragmentos independientes que, a continuación, se procesan en paralelo a través de los nodos del clúster.</span><span class="sxs-lookup"><span data-stu-id="25fa5-130">Input data is split into independent chunks, which are then processed in parallel across the nodes in your cluster.</span></span> <span data-ttu-id="25fa5-131">Un trabajo de MapReduce consta de dos funciones:</span><span class="sxs-lookup"><span data-stu-id="25fa5-131">A MapReduce job consists of two functions:</span></span>

* <span data-ttu-id="25fa5-132">**Asignador**: consume datos de entrada, los analiza (normalmente con un filtro y operaciones de ordenación) y emite tuplas (pares de clave-valor)</span><span class="sxs-lookup"><span data-stu-id="25fa5-132">**Mapper**: Consumes input data, analyzes it (usually with filter and sorting operations), and emits tuples (key-value pairs)</span></span>

* <span data-ttu-id="25fa5-133">**Reductor**: consume tuplas emitidas por el asignador y realiza una operación de resumen que crea un resultado combinado más pequeño de los datos del asignador</span><span class="sxs-lookup"><span data-stu-id="25fa5-133">**Reducer**: Consumes tuples emitted by the Mapper and performs a summary operation that creates a smaller, combined result from the Mapper data</span></span>

<span data-ttu-id="25fa5-134">En el siguiente diagrama se muestra un ejemplo de trabajo de MapReduce de recuento de palabras básico:</span><span class="sxs-lookup"><span data-stu-id="25fa5-134">A basic word count MapReduce job example is illustrated in the following diagram:</span></span>

![HDI.ProgramaRecuentoPalabras][image-hdi-wordcountdiagram]

<span data-ttu-id="25fa5-136">La salida de este trabajo es un recuento de las veces que aparece cada palabra en el texto que se ha analizado.</span><span class="sxs-lookup"><span data-stu-id="25fa5-136">The output of this job is a count of how many times each word occurred in the text that was analyzed.</span></span>

* <span data-ttu-id="25fa5-137">El asignador utiliza cada línea del texto de entrada como una entrada y la desglosa en palabras.</span><span class="sxs-lookup"><span data-stu-id="25fa5-137">The mapper takes each line from the input text as an input and breaks it into words.</span></span> <span data-ttu-id="25fa5-138">Emite un par clave-valor cada vez que se detecta una palabra, seguida por un 1.</span><span class="sxs-lookup"><span data-stu-id="25fa5-138">It emits a key/value pair each time a word occurs of the word is followed by a 1.</span></span> <span data-ttu-id="25fa5-139">La salida se ordena antes de enviarla al reductor.</span><span class="sxs-lookup"><span data-stu-id="25fa5-139">The output is sorted before sending it to reducer.</span></span>
* <span data-ttu-id="25fa5-140">El reductor suma estos recuentos individuales de cada palabra y emite un solo par clave-valor que contiene la palabra seguido de la suma de sus apariciones.</span><span class="sxs-lookup"><span data-stu-id="25fa5-140">The reducer sums these individual counts for each word and emits a single key/value pair that contains the word followed by the sum of its occurrences.</span></span>

<span data-ttu-id="25fa5-141">MapReduce se puede implementar en varios lenguajes.</span><span class="sxs-lookup"><span data-stu-id="25fa5-141">MapReduce can be implemented in various languages.</span></span> <span data-ttu-id="25fa5-142">Java es la implementación más común y se utiliza para fines de demostración en este documento.</span><span class="sxs-lookup"><span data-stu-id="25fa5-142">Java is the most common implementation, and is used for demonstration purposes in this document.</span></span>

## <a name="development-languages"></a><span data-ttu-id="25fa5-143">Lenguajes de desarrollo</span><span class="sxs-lookup"><span data-stu-id="25fa5-143">Development languages</span></span>

<span data-ttu-id="25fa5-144">Los lenguajes o marcos de trabajo basados en Java y la máquina virtual de Java se pueden ejecutar directamente como un trabajo de MapReduce.</span><span class="sxs-lookup"><span data-stu-id="25fa5-144">Languages or frameworks that are based on Java and the Java Virtual Machine can be ran directly as a MapReduce job.</span></span> <span data-ttu-id="25fa5-145">El ejemplo usado en este documento es una aplicación de MapReduce de Java.</span><span class="sxs-lookup"><span data-stu-id="25fa5-145">The example used in this document is a Java MapReduce application.</span></span> <span data-ttu-id="25fa5-146">Los lenguajes que no son Java, como C# o Python, o ejecutables independientes, deben usar streaming de Hadoop.</span><span class="sxs-lookup"><span data-stu-id="25fa5-146">Non-Java languages, such as C#, Python, or standalone executables, must use Hadoop streaming.</span></span>

<span data-ttu-id="25fa5-147">El streaming de Hadoop se comunica con el asignador y el reductor a través de STDIN y STDOUT.</span><span class="sxs-lookup"><span data-stu-id="25fa5-147">Hadoop streaming communicates with the mapper and reducer over STDIN and STDOUT.</span></span> <span data-ttu-id="25fa5-148">El asignador y reductor leen datos línea a línea desde STDIN y escriben el resultado en STDOUT.</span><span class="sxs-lookup"><span data-stu-id="25fa5-148">The mapper and reducer read data a line at a time from STDIN, and write the output to STDOUT.</span></span> <span data-ttu-id="25fa5-149">Cada línea leída o emitida por el asignador y el reductor debe estar en el formato de un par de clave-valor delimitado por un carácter de tabulación:</span><span class="sxs-lookup"><span data-stu-id="25fa5-149">Each line read or emitted by the mapper and reducer must be in the format of a key/value pair, delimited by a tab character:</span></span>

    [key]/t[value]

<span data-ttu-id="25fa5-150">Para obtener más información, consulte [Streaming de Hadoop](http://hadoop.apache.org/docs/r1.2.1/streaming.html).</span><span class="sxs-lookup"><span data-stu-id="25fa5-150">For more information, see [Hadoop Streaming](http://hadoop.apache.org/docs/r1.2.1/streaming.html).</span></span>

<span data-ttu-id="25fa5-151">Para obtener ejemplos del uso del streaming de Hadoop con HDInsight, vea los documentos siguientes:</span><span class="sxs-lookup"><span data-stu-id="25fa5-151">For examples of using Hadoop streaming with HDInsight, see the following documents:</span></span>

* [<span data-ttu-id="25fa5-152">Desarrollar trabajos de MapReduce de C#</span><span class="sxs-lookup"><span data-stu-id="25fa5-152">Develop C# MapReduce jobs</span></span>](hdinsight-hadoop-dotnet-csharp-mapreduce-streaming.md)

* [<span data-ttu-id="25fa5-153">Desarrollar trabajos de MapReduce de Python</span><span class="sxs-lookup"><span data-stu-id="25fa5-153">Develop Python MapReduce jobs</span></span>](hdinsight-hadoop-streaming-python.md)

## <span data-ttu-id="25fa5-154"><a id="data"></a>Datos de ejemplo</span><span class="sxs-lookup"><span data-stu-id="25fa5-154"><a id="data"></a>Example data</span></span>

<span data-ttu-id="25fa5-155">HDInsight proporciona diversos conjuntos de datos de ejemplo que se almacenan en los directorios `/example/data` y `/HdiSamples`.</span><span class="sxs-lookup"><span data-stu-id="25fa5-155">HDInsight provides various example data sets, which are stored in the `/example/data` and `/HdiSamples` directory.</span></span> <span data-ttu-id="25fa5-156">Estos directorios están en el almacenamiento predeterminado de su clúster.</span><span class="sxs-lookup"><span data-stu-id="25fa5-156">These directories are in the default storage for your cluster.</span></span> <span data-ttu-id="25fa5-157">En este documento, se utiliza el archivo `/example/data/gutenberg/davinci.txt`.</span><span class="sxs-lookup"><span data-stu-id="25fa5-157">In this document, we use the `/example/data/gutenberg/davinci.txt` file.</span></span> <span data-ttu-id="25fa5-158">Este archivo contiene los blocs de notas de Leonardo Da Vinci.</span><span class="sxs-lookup"><span data-stu-id="25fa5-158">This file contains the notebooks of Leonardo Da Vinci.</span></span>

## <span data-ttu-id="25fa5-159"><a id="job"></a>MapReduce de ejemplo</span><span class="sxs-lookup"><span data-stu-id="25fa5-159"><a id="job"></a>Example MapReduce</span></span>

<span data-ttu-id="25fa5-160">En el clúster de HDInsight se incluye un MapReduce de ejemplo de aplicación de recuento de palabras.</span><span class="sxs-lookup"><span data-stu-id="25fa5-160">An example MapReduce word count application is included with your HDInsight cluster.</span></span> <span data-ttu-id="25fa5-161">En este ejemplo se encuentra en `/example/jars/hadoop-mapreduce-examples.jar` en el almacenamiento predeterminado del clúster.</span><span class="sxs-lookup"><span data-stu-id="25fa5-161">This example is located at `/example/jars/hadoop-mapreduce-examples.jar` on the default storage for your cluster.</span></span>

<span data-ttu-id="25fa5-162">El código Java siguiente es el origen de la aplicación de MapReduce contenida en el archivo `hadoop-mapreduce-examples.jar`:</span><span class="sxs-lookup"><span data-stu-id="25fa5-162">The following Java code is the source of the MapReduce application contained in the `hadoop-mapreduce-examples.jar` file:</span></span>

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

<span data-ttu-id="25fa5-163">Para obtener instrucciones sobre cómo escribir sus propias aplicaciones de MapReduce, consulte los documentos siguientes:</span><span class="sxs-lookup"><span data-stu-id="25fa5-163">For instructions to write your own MapReduce applications, see the following documents:</span></span>

* [<span data-ttu-id="25fa5-164">Desarrollo de aplicaciones MapReduce de Java para HDInsight</span><span class="sxs-lookup"><span data-stu-id="25fa5-164">Develop Java MapReduce applications for HDInsight</span></span>](hdinsight-develop-deploy-java-mapreduce-linux.md)

* [<span data-ttu-id="25fa5-165">Desarrollo de aplicaciones MapReduce de Python para HDInsight</span><span class="sxs-lookup"><span data-stu-id="25fa5-165">Develop Python MapReduce applications for HDInsight</span></span>](hdinsight-hadoop-streaming-python.md)

## <span data-ttu-id="25fa5-166"><a id="run"></a>Ejecución de MapReduce</span><span class="sxs-lookup"><span data-stu-id="25fa5-166"><a id="run"></a>Run the MapReduce</span></span>

<span data-ttu-id="25fa5-167">HDInsight puede ejecutar trabajos de HiveQL mediante varios métodos.</span><span class="sxs-lookup"><span data-stu-id="25fa5-167">HDInsight can run HiveQL jobs by using various methods.</span></span> <span data-ttu-id="25fa5-168">Use la tabla siguiente para decidir cuál es el método adecuado para usted luego siga el vínculo para ver un tutorial.</span><span class="sxs-lookup"><span data-stu-id="25fa5-168">Use the following table to decide which method is right for you, then follow the link for a walkthrough.</span></span>

| <span data-ttu-id="25fa5-169">**Use esto**...</span><span class="sxs-lookup"><span data-stu-id="25fa5-169">**Use this**...</span></span> | <span data-ttu-id="25fa5-170">**...para hacer esto**</span><span class="sxs-lookup"><span data-stu-id="25fa5-170">**...to do this**</span></span> | <span data-ttu-id="25fa5-171">...con este **sistema operativo de clúster**</span><span class="sxs-lookup"><span data-stu-id="25fa5-171">...with this **cluster operating system**</span></span> | <span data-ttu-id="25fa5-172">...desde este **sistema operativo de cliente**</span><span class="sxs-lookup"><span data-stu-id="25fa5-172">...from this **client operating system**</span></span> |
|:--- |:--- |:--- |:--- |
| [<span data-ttu-id="25fa5-173">SSH</span><span class="sxs-lookup"><span data-stu-id="25fa5-173">SSH</span></span>](hdinsight-hadoop-use-mapreduce-ssh.md) |<span data-ttu-id="25fa5-174">Uso del comando Hadoop mediante **SSH**</span><span class="sxs-lookup"><span data-stu-id="25fa5-174">Use the Hadoop command through **SSH**</span></span> |<span data-ttu-id="25fa5-175">Linux</span><span class="sxs-lookup"><span data-stu-id="25fa5-175">Linux</span></span> |<span data-ttu-id="25fa5-176">Linux, Unix, Mac OS X o Windows</span><span class="sxs-lookup"><span data-stu-id="25fa5-176">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="25fa5-177">Curl</span><span class="sxs-lookup"><span data-stu-id="25fa5-177">Curl</span></span>](hdinsight-hadoop-use-mapreduce-curl.md) |<span data-ttu-id="25fa5-178">Enviar el trabajo de forma remota mediante **REST**</span><span class="sxs-lookup"><span data-stu-id="25fa5-178">Submit the job remotely by using **REST**</span></span> |<span data-ttu-id="25fa5-179">Linux o Windows</span><span class="sxs-lookup"><span data-stu-id="25fa5-179">Linux or Windows</span></span> |<span data-ttu-id="25fa5-180">Linux, Unix, Mac OS X o Windows</span><span class="sxs-lookup"><span data-stu-id="25fa5-180">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="25fa5-181">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="25fa5-181">Windows PowerShell</span></span>](hdinsight-hadoop-use-mapreduce-powershell.md) |<span data-ttu-id="25fa5-182">Enviar el trabajo de forma remota mediante **Windows PowerShell**</span><span class="sxs-lookup"><span data-stu-id="25fa5-182">Submit the job remotely by using **Windows PowerShell**</span></span> |<span data-ttu-id="25fa5-183">Linux o Windows</span><span class="sxs-lookup"><span data-stu-id="25fa5-183">Linux or Windows</span></span> |<span data-ttu-id="25fa5-184">Windows</span><span class="sxs-lookup"><span data-stu-id="25fa5-184">Windows</span></span> |
| <span data-ttu-id="25fa5-185">[Escritorio remoto](hdinsight-hadoop-use-mapreduce-remote-desktop.md) (HDInsight 3.2 y 3.3)</span><span class="sxs-lookup"><span data-stu-id="25fa5-185">[Remote Desktop](hdinsight-hadoop-use-mapreduce-remote-desktop.md) (HDInsight 3.2 and 3.3)</span></span> |<span data-ttu-id="25fa5-186">Uso del comando Hadoop mediante **Escritorio remoto**</span><span class="sxs-lookup"><span data-stu-id="25fa5-186">Use the Hadoop command through **Remote Desktop**</span></span> |<span data-ttu-id="25fa5-187">Windows</span><span class="sxs-lookup"><span data-stu-id="25fa5-187">Windows</span></span> |<span data-ttu-id="25fa5-188">Windows</span><span class="sxs-lookup"><span data-stu-id="25fa5-188">Windows</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="25fa5-189">Linux es el único sistema operativo que se usa en la versión 3.4 de HDInsight, o en las superiores.</span><span class="sxs-lookup"><span data-stu-id="25fa5-189">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="25fa5-190">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="25fa5-190">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="25fa5-191"><a id="nextsteps"></a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="25fa5-191"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="25fa5-192">Para conocer más acerca del trabajo con datos en HDInsight, consulte los siguientes documentos:</span><span class="sxs-lookup"><span data-stu-id="25fa5-192">To learn more about working with data in HDInsight, see the following documents:</span></span>

* [<span data-ttu-id="25fa5-193">Desarrollo de programas MapReduce de Java para HDInsight</span><span class="sxs-lookup"><span data-stu-id="25fa5-193">Develop Java MapReduce programs for HDInsight</span></span>](hdinsight-develop-deploy-java-mapreduce-linux.md)

* [<span data-ttu-id="25fa5-194">Desarrollo de programas de MapReduce de streaming de Python para HDInsight</span><span class="sxs-lookup"><span data-stu-id="25fa5-194">Develop Python streaming MapReduce programs for HDInsight</span></span>](hdinsight-hadoop-streaming-python.md)

* [<span data-ttu-id="25fa5-195">Desarrollo de trabajos de MapReduce de Scalding con Hadoop Apache en HDInsight</span><span class="sxs-lookup"><span data-stu-id="25fa5-195">Develop Scalding MapReduce jobs with Apache Hadoop on HDInsight</span></span>](hdinsight-hadoop-mapreduce-scalding.md)

* <span data-ttu-id="25fa5-196">[Uso de Hive con HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="25fa5-196">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>

* <span data-ttu-id="25fa5-197">[Uso de Pig con HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="25fa5-197">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>


[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-develop-mapreduce-jobs]: hdinsight-develop-deploy-java-mapreduce-linux.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md


[powershell-install-configure]: /powershell/azureps-cmdlets-docs

[image-hdi-wordcountdiagram]: ./media/hdinsight-use-mapreduce/HDI.WordCountDiagram.gif
