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
# <a name="use-mapreduce-in-hadoop-on-hdinsight"></a>Uso de MapReduce en Hadoop en HDInsight

Obtenga información acerca de cómo trabajos toorun MapReduce en clústeres de HDInsight. Usar hello después hello toodiscover de tabla que MapReduce puede utilizarse con HDInsight de varias maneras:

| **Use esto**... | **.. .toodo esto** | ...con este **sistema operativo de clúster** | ...desde este **sistema operativo de cliente** |
|:--- |:--- |:--- |:--- |
| [SSH](hdinsight-hadoop-use-mapreduce-ssh.md) |Usar comandos de Hadoop de Hola a través de **SSH** |Linux |Linux, Unix, Mac OS X o Windows |
| [REST](hdinsight-hadoop-use-mapreduce-curl.md) |Enviar trabajo Hola de forma remota mediante **REST** (ejemplos usan cURL) |Linux o Windows |Linux, Unix, Mac OS X o Windows |
| [Windows PowerShell](hdinsight-hadoop-use-mapreduce-powershell.md) |Enviar trabajo Hola de forma remota mediante **Windows PowerShell** |Linux o Windows |Windows |
| [Escritorio remoto](hdinsight-hadoop-use-mapreduce-remote-desktop.md) (HDInsight 3.2 y 3.3) |Usar comandos de Hadoop de Hola a través de **escritorio remoto** |Windows |Windows |

> [!IMPORTANT]
> Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior. Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a id="whatis"></a>Qué es MapReduce

MapReduce de Hadoop es un marco de software para escribir trabajos que procesan enormes cantidades de datos. Datos de entrada se dividen en fragmentos independientes, que, a continuación, se procesan en paralelo en todos los nodos de hello en el clúster. Un trabajo de MapReduce consta de dos funciones:

* **Asignador**: consume datos de entrada, los analiza (normalmente con un filtro y operaciones de ordenación) y emite tuplas (pares de clave-valor)

* **Reductor**: consume tuplas emitidos por el asignador de Hola y realiza una operación de resumen que crea un resultado más pequeño y combinado de hello datos asignador

Un ejemplo de trabajo de MapReduce de recuento word básico se muestra en hello siguiente diagrama:

![HDI.ProgramaRecuentoPalabras][image-hdi-wordcountdiagram]

salida de Hello de este trabajo es un recuento de cuántas veces se produjo cada palabra en el texto hello que se analizó.

* el asignador de Hello toma cada línea de texto de entrada de hello como entrada y lo divide en palabras. Emite un clave y valor par cada vez que se produce una palabra de la palabra Hola va seguido de un 1. salida de Hello se ordena antes de enviarlo tooreducer.
* reductor de Hello suma estos recuentos individuales para cada palabra y emite un par de clave/valor único que contiene la palabra Hola seguido de suma de Hola de sus repeticiones.

MapReduce se puede implementar en varios lenguajes. Java es la implementación más habitual de Hola y se usa para fines de demostración en este documento.

## <a name="development-languages"></a>Lenguajes de desarrollo

Idiomas o marcos de trabajo que se basan en Java y Hola Máquina Virtual Java se pueda ejecutar directamente como un trabajo de MapReduce. ejemplo de Hola usado en este documento es una aplicación de Java MapReduce. Los lenguajes que no son Java, como C# o Python, o ejecutables independientes, deben usar streaming de Hadoop.

Streaming de Hadoop se comunica con el asignador de Hola y reductor sobre STDIN y STDOUT. reductor y el asignador de hello leen datos de una línea de STDIN al mismo tiempo y escribir hello tooSTDOUT de salida. Cada línea de lectura o emitidos por reductor y el asignador de hello debe estar en formato de Hola de un par de clave y valor delimitado por un carácter de tabulación:

    [key]/t[value]

Para obtener más información, consulte [Streaming de Hadoop](http://hadoop.apache.org/docs/r1.2.1/streaming.html).

Para obtener ejemplos del uso de Hadoop con HDInsight de transmisión por secuencias, vea Hola siguientes documentos:

* [Desarrollar trabajos de MapReduce de C#](hdinsight-hadoop-dotnet-csharp-mapreduce-streaming.md)

* [Desarrollar trabajos de MapReduce de Python](hdinsight-hadoop-streaming-python.md)

## <a id="data"></a>Datos de ejemplo

HDInsight proporciona diversos conjuntos de datos de ejemplo, que se almacenan en hello `/example/data` y `/HdiSamples` directory. Son estos directorios en almacenamiento predeterminado de hello para el clúster. En este documento, se utiliza hello `/example/data/gutenberg/davinci.txt` archivo. Este archivo contiene los blocs de notas de Hola de Leonardo Da Vinci.

## <a id="job"></a>MapReduce de ejemplo

En el clúster de HDInsight se incluye un MapReduce de ejemplo de aplicación de recuento de palabras. En este ejemplo se encuentra en `/example/jars/hadoop-mapreduce-examples.jar` en almacenamiento predeterminado de hello para el clúster.

Hola después el código Java es el origen de Hola de hello aplicación MapReduce contenido en hello `hadoop-mapreduce-examples.jar` archivo:

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

Para instrucciones toowrite sus propias aplicaciones MapReduce, vea Hola siguientes documentos:

* [Desarrollo de aplicaciones MapReduce de Java para HDInsight](hdinsight-develop-deploy-java-mapreduce-linux.md)

* [Desarrollo de aplicaciones MapReduce de Python para HDInsight](hdinsight-hadoop-streaming-python.md)

## <a id="run"></a>Ejecute hello MapReduce

HDInsight puede ejecutar trabajos de HiveQL mediante varios métodos. Usar hello después toodecide tabla qué método es adecuado para usted, a continuación, siga el vínculo de Hola para ver un tutorial.

| **Use esto**... | **.. .toodo esto** | ...con este **sistema operativo de clúster** | ...desde este **sistema operativo de cliente** |
|:--- |:--- |:--- |:--- |
| [SSH](hdinsight-hadoop-use-mapreduce-ssh.md) |Usar comandos de Hadoop de Hola a través de **SSH** |Linux |Linux, Unix, Mac OS X o Windows |
| [Curl](hdinsight-hadoop-use-mapreduce-curl.md) |Enviar trabajo Hola de forma remota mediante **REST** |Linux o Windows |Linux, Unix, Mac OS X o Windows |
| [Windows PowerShell](hdinsight-hadoop-use-mapreduce-powershell.md) |Enviar trabajo Hola de forma remota mediante **Windows PowerShell** |Linux o Windows |Windows |
| [Escritorio remoto](hdinsight-hadoop-use-mapreduce-remote-desktop.md) (HDInsight 3.2 y 3.3) |Usar comandos de Hadoop de Hola a través de **escritorio remoto** |Windows |Windows |

> [!IMPORTANT]
> Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior. Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a id="nextsteps"></a>Pasos siguientes

toolearn más acerca de cómo trabajar con datos en HDInsight, vea Hola siguientes documentos:

* [Desarrollo de programas MapReduce de Java para HDInsight](hdinsight-develop-deploy-java-mapreduce-linux.md)

* [Desarrollo de programas de MapReduce de streaming de Python para HDInsight](hdinsight-hadoop-streaming-python.md)

* [Desarrollo de trabajos de MapReduce de Scalding con Hadoop Apache en HDInsight](hdinsight-hadoop-mapreduce-scalding.md)

* [Uso de Hive con HDInsight][hdinsight-use-hive]

* [Uso de Pig con HDInsight][hdinsight-use-pig]


[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-develop-mapreduce-jobs]: hdinsight-develop-deploy-java-mapreduce-linux.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md


[powershell-install-configure]: /powershell/azureps-cmdlets-docs

[image-hdi-wordcountdiagram]: ./media/hdinsight-use-mapreduce/HDI.WordCountDiagram.gif
