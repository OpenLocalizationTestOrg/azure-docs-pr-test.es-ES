---
title: ejemplos de hello aaaRun Hadoop en HDInsight - Azure | Documentos de Microsoft
description: "Empezar a trabajar con servicio de HDInsight de Azure Hola Hola ejemplos que se proporcionan. Use scripts de PowerShell que ejecutan programas MapReduce en clústeres de datos."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: bf76d452-abb4-4210-87bd-a2067778c6ed
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 544856a2cdfe5154cbd9bf1fb05db081af86cd46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="run-hadoop-mapreduce-samples-in-windows-based-hdinsight"></a>Ejecución de ejemplos de Hadoop MapReduce en HDInsight basado en Windows
[!INCLUDE [samples-selector](../../includes/hdinsight-run-samples-selector.md)]

Se proporciona un conjunto de muestras toohelp empezar a ejecutar trabajos MapReduce en clústeres de Hadoop con HDInsight de Azure. Estos ejemplos se ponen a disposición de cada uno de hello HDInsight clústeres administrados creados por usted. Estos ejemplos de la ejecución familiarizarse con el uso de trabajos de toorun de cmdlets de PowerShell de Azure en clústeres de Hadoop.

* [**Recuento de palabras**][hdinsight-sample-wordcount]: cuenta las apariciones de una palabra en un archivo de texto.
* [**Número de palabras de transmisión por secuencias de C#**][hdinsight-sample-csharp-streaming]: Hola de apariciones de recuentos de palabras en un archivo de texto con interfaz de streaming de Hadoop.
* [**Estimador de PI**][hdinsight-sample-pi-estimator]: utiliza una estadística (tipo de Monte Carlo) valor del método tooestimate Hola de pi.
* [**Graysort de 10 GB**][hdinsight-sample-10gb-graysort]: se ejecuta una muestra de GraySort de uso general en un archivo de 10 GB mediante HDInsight. Hay tres toorun de trabajos: Teragen toogenerate Hola datos, datos de hello toosort Terasort y tooconfirm Teravalidate que se han ordenado correctamente datos de Hola.

> [!NOTE]
> código fuente de Hello puede encontrarse en el apéndice de hello.

Existe documentación adicional mucho en web de Hola para las tecnologías relacionadas con Hadoop, como la programación de MapReduce basados en Java y transmisión por secuencias y documentación acerca de los cmdlets de Hola que se usan en Windows PowerShell scripting. Para obtener más información acerca de estos recursos, consulte:

* [Desarrollo de programas MapReduce de Java para Hadoop en HDInsight](hdinsight-develop-deploy-java-mapreduce-linux.md)
* [Envío de trabajos de Hadoop en HDInsight](hdinsight-submit-hadoop-jobs-programmatically.md)
* [Introducción tooAzure HDInsight][hdinsight-introduction]

En la actualidad, muchas personas prefieren Hive y Pig a MapReduce.  Para más información, consulte:

* [Uso de Hive en HDInsight](hdinsight-use-hive.md)
* [Uso de Pig en HDInsight](hdinsight-use-pig.md)

**Requisitos previos**:

* **Una suscripción de Azure**. Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* **un clúster de HDInsight**. Para obtener instrucciones sobre Hola distintas formas en que se pueden crear clústeres como éstos, vea [Hadoop crear clústeres de HDInsight](hdinsight-hadoop-provision-linux-clusters.md).
* **Una estación de trabajo con Azure PowerShell**.

    > [!IMPORTANT]
    > La compatibilidad con Azure PowerShell para administrar recursos de HDInsight mediante Azure Service Manager está **en desuso** y desaparecerá por completo el 1 de enero de 2017. Hola pasos de este documento use Hola nuevos cmdlets de HDInsight que funcionan con el Administrador de recursos de Azure.
    >
    > Siga los pasos de hello en [instalar y configurar Azure PowerShell](/powershell/azureps-cmdlets-docs) versión más reciente de hello tooinstall de PowerShell de Azure. Si tiene scripts de ese toobe necesidad de modifica toouse Hola nuevos cmdlets que funcionan con el Administrador de recursos de Azure, consulte [tooAzure desarrollo basado en el Administrador de recursos de migración de las herramientas de clústeres de HDInsight](hdinsight-hadoop-development-using-azure-resource-manager.md).

## <a name="hdinsight-sample-wordcount"></a>Recuento de palabras: Java
toosubmit un proyecto de MapReduce, primero cree una definición de trabajo de MapReduce. En la definición del trabajo hello, especificar archivo jar de hello MapReduce programa y la ubicación de Hola de archivo jar de hello, que es **wasb:///example/jars/hadoop-mapreduce-examples.jar**, Hola nombre de clase y Hola argumentos.  programa de Hello wordcount MapReduce toma dos argumentos: archivo de código fuente de Hola que es usado toocount palabras y la ubicación de hello para la salida.

código fuente de Hello puede encontrarse en hello [Apéndice A](#apendix-a---the-word-count-MapReduce-program-in-java).

Procedimiento de Hola de desarrollar un MapReduce de Java, consulte - [programas de MapReduce desarrollar de Java para Hadoop en HDInsight](hdinsight-develop-deploy-java-mapreduce-linux.md)

**toosubmit un trabajo de MapReduce de recuento de palabras**

1. Abra **Windows PowerShell ISE**. Para obtener más información, consulte [Instalación y configuración de Azure PowerShell][powershell-install-configure].
2. Pegue el siguiente script de PowerShell de hello:

    ```powershell
    $subscriptionName = "<Azure Subscription Name>"
    $resourceGroupName = "<Resource Group Name>"
    $clusterName = "<HDInsight cluster name>"             # HDInsight cluster name

    Select-AzureRmSubscription -SubscriptionName $subscriptionName

    # Define hello MapReduce job
    $mrJobDefinition = New-AzureRmHDInsightMapReduceJobDefinition `
                                -JarFile "wasb:///example/jars/hadoop-mapreduce-examples.jar" `
                                -ClassName "wordcount" `
                                -Arguments "wasb:///example/data/gutenberg/davinci.txt", "wasb:///example/data/WordCountOutput"

    # Submit hello job and wait for job completion
    $cred = Get-Credential -Message "Enter hello HDInsight cluster HTTP user credential:"
    $mrJob = Start-AzureRmHDInsightJob `
                        -ResourceGroupName $resourceGroupName `
                        -ClusterName $clusterName `
                        -HttpCredential $cred `
                        -JobDefinition $mrJobDefinition

    Wait-AzureRmHDInsightJob `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $clusterName `
        -HttpCredential $cred `
        -JobId $mrJob.JobId

    # Get hello job output
    $cluster = Get-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $clusterName
    $defaultStorageAccount = $cluster.DefaultStorageAccount -replace '.blob.core.windows.net'
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccount)[0].Value
    $defaultStorageContainer = $cluster.DefaultStorageContainer

    Get-AzureRmHDInsightJobOutput `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $clusterName `
        -HttpCredential $cred `
        -DefaultStorageAccountName $defaultStorageAccount `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultContainer $defaultStorageContainer  `
        -JobId $mrJob.JobId `
        -DisplayOutputType StandardError

    # Download hello job output toohello workstation
    $storageContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccount -StorageAccountKey $defaultStorageAccountKey
    Get-AzureStorageBlobContent -Container $defaultStorageContainer -Blob example/data/WordCountOutput/part-r-00000 -Context $storageContext -Force

    # Display hello output file
    cat ./example/data/WordCountOutput/part-r-00000 | findstr "there"
    ```

    trabajo de MapReduce Hello genera un archivo denominado *parte-r-00000*, que contiene palabras y recuentos de Hola. script de Hola usa hello **findstr** comando toolist Hola a todas las palabras que contiene *"there"*.
3. Establecer hello en primer lugar tres variables y ejecutar script de Hola.

## <a name="hdinsight-sample-csharp-streaming"></a>Recuento de palabras: streaming en C#
Hadoop proporciona una transmisión por secuencias tooMapReduce API, lo que permite asignar toowrite así como funciones en lenguajes distintos de Java.

> [!NOTE]
> pasos de Hello en este tutorial aplican según tooWindows solo clústeres de HDInsight. Para obtener un ejemplo de streaming para clústeres de HDInsight basados en Linux, consulte [Desarrollo de programas de streaming en Python para HDInsight](hdinsight-hadoop-streaming-python.md).

En hello (ejemplo), el asignador de Hola y reductor Hola son archivos ejecutables que leen la entrada de Hola de [stdin] [ stdin-stdout-stderr] (línea por línea) y emitir la salida de hello demasiado[stdout] [stdin-stdout-stderr]. programa Hello cuenta todas las palabras de hello en texto hello.

Cuando se especifica un archivo ejecutable para **asignadores**, cada tarea de asignador inicia Hola ejecutable como un proceso independiente cuando se inicializa el asignador de Hola. Tal y como se ejecuta la tarea de asignador de hello, su entrada convierte en líneas y fuentes Hola líneas toohello [stdin] [ stdin-stdout-stderr] del proceso de Hola.

Hola mientras tanto, el asignador de hello recopila salida orientada a líneas de hello de hello stdout del proceso de Hola. Cada línea convierte en un par de clave/valor, que se recopila como salida de hello de asignador de Hola. De forma predeterminada, prefijo Hola de una línea arriba toohello primer carácter de tabulación es la clave de hello y, resto Hola de línea hello (excepto Hola carácter de tabulación) es el valor de Hola. Si no hay ningún carácter de tabulación en línea hello, toda la línea se considera como clave de Hola y Hola valor es null.

Cuando se especifica un archivo ejecutable para **reductores**, cada tarea reductor inicia Hola ejecutable como un proceso independiente cuando se inicializa el reductor Hola. Hola reductor tarea se ejecuta, sus pares clave-valor de entrada convierte en líneas y fuentes de hello líneas toohello [stdin] [ stdin-stdout-stderr] del proceso de Hola.

Hola mientras tanto, reductor Hola recopila salida orientada a líneas de hello de hello [stdout] [ stdin-stdout-stderr] del proceso de Hola. Convierte a cada par de clave/valor tooa de línea, que se recopila como salida de hello de reductor Hola. De forma predeterminada, prefijo Hola de una línea arriba toohello primer carácter de tabulación es la clave de hello y, resto Hola de línea hello (excepto Hola carácter de tabulación) es el valor de Hola.

**trabajo de recuento de palabras streaming toosubmit C#**

* Siga el procedimiento de hello en [contar - Java palabras](#word-count-java)y reemplace la definición de trabajo de hello con hello después de línea:

    ```powershell
    $mrJobDefinition = New-AzureRmHDInsightStreamingMapReduceJobDefinition `
                            -Files "/example/apps/cat.exe","/example/apps/wc.exe" `
                            -Mapper "cat.exe" `
                            -Reducer "wc.exe" `
                            -InputPath "/example/data/gutenberg/davinci.txt" `
                            -OutputPath "/example/data/StreamingOutput/wc.txt"
    ```

    archivo de salida de Hello será:

        example/data/StreamingOutput/wc.txt/part-00000

## <a name="hdinsight-sample-pi-estimator"></a>Estimador de pi
Estimador de pi Hello usa una estadística (tipo de Monte Carlo) valor del método tooestimate Hola de pi. Puntos colocados aleatoriamente dentro de una unidad cuadrado también se sitúan dentro de un círculo inscribe dentro de ese cuadrado con un área de toohello igual de probabilidad del círculo hello, pi/4. valor de Hola de pi se puede estimar de valor de Hola de 4R, donde R es la proporción de hello del número de Hola de puntos que están dentro de círculo hello toohello número total de puntos que están dentro de cuadrado de Hola. Hola Hola muestra de mayor tamaño puntos usados, que es mejor estimación de Hola Hola.

script de Hola proporcionado para este ejemplo envía un trabajo de Hadoop jar y está configurado toorun con un valor de 16 mapas, cada uno de los cuales es toocompute requiere 10 millones de puntos de ejemplo por valores de parámetro de Hola. Estos parámetros los valores pueden cambiar tooimprove Hola estimado valor de pi. Como referencia, hello 10 primeros decimales de pi son 3.1415926535.

**toosubmit un trabajo del estimador de pi**

* Siga el procedimiento de hello en [contar - Java palabras](#word-count-java)y reemplace la definición de trabajo de hello con hello después de línea:

    ```powershell
    $mrJobJobDefinition = New-AzureRmHDInsightMapReduceJobDefinition `
                                -JarFile "wasb:///example/jars/hadoop-mapreduce-examples.jar" `
                                -ClassName "pi" `
                                -Arguments "16", "10000000"
    ```

## <a name="hdinsight-sample-10gb-graysort"></a>GraySort de 10 GB
Este ejemplo utiliza solo 10 GB de datos, para así poder ejecutarlo relativamente rápido. Usa las aplicaciones de MapReduce Hola desarrolladas por Owen O'Malley y Arun Murthy lograda comparativa de ordenación de hello anual uso general ("daytona") terabyte en 2009 con una velocidad de 0.578 TB/min (100 TB en 173 minutos). Para obtener más información sobre este y otros criterios de ordenación de referencia, vea hello [Sortbenchmark](http://sortbenchmark.org/) sitio.

Este ejemplo utiliza tres conjuntos de programas de MapReduce:

1. **TeraGen** es un programa de MapReduce que se pueden usar filas de hello toogenerate de toosort de datos.
2. **TeraSort** muestrea los datos de entrada de Hola y utiliza datos de hello toosort MapReduce en un orden total. TeraSort es una ordenación estándar de funciones de MapReduce, excepto un particionador personalizado que utiliza una lista ordenada de claves de n-1 muestreada que definen el intervalo de claves de Hola para cada reduce. En particular, todas las claves de este tipo que muestra [i-1] < = clave < [i] de ejemplo se envían tooreduce. Esto garantiza que las salidas de Hola de reducen i es todos los menores de reducir la salida de hello de i + 1.
3. **TeraValidate** es un programa de MapReduce que valida que los resultados del Hola global está ordenado. Crea una asignación por cada archivo en el directorio de salida de hello, y cada asignación garantiza que cada clave es menor o igual toohello anterior. función de asignación de Hello también genera registros de hello primero y último claves de cada archivo y Hola reducen (función) garantiza que Hola primera clave de archivo i es mayor que la clave de la última Hola de i-1 de archivo. Los problemas se notifican como una salida de hello reducir con claves de Hola que no están ordenadas.

Hola de entrada y el formato de salida, utilizado por todas las aplicaciones de tres, lee y escribe archivos de texto hello en el formato correcto de Hola. reducir la salida de Hello de hello replicación estableció too1, en lugar de hello valor predeterminado es 3, porque el contexto de la prueba comparativa de hello no requiere que los datos de salida de hello replicarse en nodos de toomultiple.

Ejemplo de Hola, cada tooone correspondiente de programas de MapReduce Hola que se describe en la introducción de Hola se requieren tres tareas:

1. Generar datos de hello para la ordenación mediante la ejecución de hello **TeraGen** trabajo MapReduce.
2. Ordenar los datos de hello ejecutando hello **TeraSort** trabajo MapReduce.
3. Confirme que los datos de Hola se han ordenado correctamente mediante la ejecución de hello **TeraValidate** trabajo MapReduce.

**trabajos de hello toosubmit**

* Siga el procedimiento de hello en [contar - Java palabras](#word-count-java), y use Hola siguiendo las definiciones de trabajos:

    ```powershell
    $teragen = New-AzureRmHDInsightMapReduceJobDefinition `
                                -JarFile "/example/jars/hadoop-mapreduce-examples.jar" `
                                -ClassName "teragen" `
                                -Arguments "-Dmapred.map.tasks=50", "100000000", "/example/data/10GB-sort-input"

    $terasort = New-AzureRmHDInsightMapReduceJobDefinition `
                                -JarFile "/example/jars/hadoop-mapreduce-examples.jar" `
                                -ClassName "terasort" `
                                -Arguments "-Dmapred.map.tasks=50", "-Dmapred.reduce.tasks=25", "/example/data/10GB-sort-input", "/example/data/10GB-sort-output"

    $teravalidate = New-AzureRmHDInsightMapReduceJobDefinition `
                                -JarFile "/example/jars/hadoop-mapreduce-examples.jar" `
                                -ClassName "teravalidate" `
                                -Arguments "-Dmapred.map.tasks=50", "-Dmapred.reduce.tasks=25", "/example/data/10GB-sort-output", "/example/data/10GB-sort-validate"
    ```

## <a name="next-steps"></a>Pasos siguientes
De este artículo y los artículos de hello en cada uno de los ejemplos de hello, ha aprendido cómo las muestras de hello toorun incluyan con hello clústeres de HDInsight mediante Azure PowerShell. Para ver los tutoriales sobre el uso de Pig, Hive y MapReduce con HDInsight, vea Hola temas siguientes:

* [Empezar a trabajar con Hadoop Hive en el uso de auriculares móviles de tooanalyze de HDInsight][hdinsight-get-started]
* [Uso de Pig con Hadoop en HDInsight][hdinsight-use-pig]
* [Uso de Hive con Hadoop en HDInsight][hdinsight-use-hive]
* [Envío de trabajos de Hadoop en HDInsight][hdinsight-submit-jobs]
* [Documentación de SDK de HDInsight de Azure][hdinsight-sdk-documentation]

## <a name="appendix-a---hello-word-count-source-code"></a>Apéndice A - Hola código fuente de recuento de palabras

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

## <a name="appendix-b---hello-word-count-streaming-source-code"></a>Apéndice B - número de palabras de hello transmisión por secuencias de código fuente
programa de MapReduce Hello usa la aplicación de cat.exe Hola como un texto de asignación interfaz toostream hello en la consola de Hola y Hola wc.exe como Hola reducir el número de hello toocount de interfaz de palabras que se transmiten desde un documento. El asignador de Hola y reductor leen caracteres, línea por línea del flujo de entrada estándar (stdin) de Hola y escribir toohello flujo de salida estándar (stdout).

```csharp
// hello source code for hello cat.exe (Mapper).

using System;
using System.IO;

namespace cat
{
    class cat
    {
        static void Main(string[] args)
        {
            if (args.Length > 0)
            {
                Console.SetIn(new StreamReader(args[0]));
            }

            string line;
            char[] separators = { ' ', '\n'};
            while ((line = Console.ReadLine()) != null)
            {
                string[] words = line.Split(separators);
                foreach (var word in words)
                {
                    Console.WriteLine("{0}\t1", word);
                }
            }
        }
    }
}
```

Hola código asignador en hello cat.cs archivos utiliza una [StreamReader] [ streamreader] tooread caracteres de Hola de Hola entrantes flujo toohello consola, que escribirá Hola flujo de salida estándar de toohello de flujo de objeto con hello estático [Console.Writeline] [ console-writeline] método.

```csharp
// hello source code for wc.exe (Reducer) is:

using System;
using System.IO;
using System.Linq;
using System.Collections;

namespace wc
{
    class wc
    {
        static void Main(string[] args)
        {
            string line;

            if (args.Length > 0)
            {
                Console.SetIn(new StreamReader(args[0]));
            }

            Hashtable wordCount = new Hashtable();
            while ((line = Console.ReadLine()) != null)
            {
                string[] words = line.Split('\t');

                string key = words[0];

                if (wordCount.ContainsKey(key) == true)
                {
                    int n = Convert.ToInt32(wordCount[key]);
                    wordCount[key] = Convert.ToString(n + 1);
                }
                else
                {
                    wordCount[key] = words[1];
                }
            }
            foreach (var key in wordCount.Keys)
            {
                Console.WriteLine("{0} {1}", key, wordCount[key]);
            }
        }
    }
}
```

Hola código reductor en hello wc.cs archivos utiliza una [StreamReader] [ streamreader] objeto tooread caracteres Hola flujo de entrada estándar que se han resultado por el asignador de cat.exe Hola. Tal y como lee los caracteres de hello con hello [Console.Writeline] [ console-writeline] método, recuentos palabras hello contando espacios y caracteres de fin de línea al final de Hola de cada palabra. A continuación, escribe flujo de salida estándar de hello toohello total con hello [Console.Writeline] [ console-writeline] método.

## <a name="appendix-c---hello-pi-estimator-source-code"></a>Apéndice C - Hola código fuente de Pi Estimador
Estimador de pi Hola código Java que contiene funciones de asignador y reductor Hola está disponible para su inspección siguiente. programa de asignador de Hello genera un número especificado de puntos colocado aleatoriamente dentro de un cuadrado de unidad y, a continuación, cuenta número de Hola de esos puntos que están dentro de círculo Hola. programa de reductor de Hello acumula puntos contados asignadores de Hola y a continuación, calcula el valor de Hola de pi de hello fórmulas 4R, donde R es la proporción de hello del número de Hola de puntos cuenta dentro de círculo hello toohello número total de puntos que están dentro de cuadrado Hola.

```java
/**
* Licensed toohello Apache Software Foundation (ASF) under one
* or more contributor license agreements. See hello NOTICE file
* distributed with this work for additional information
* regarding copyright ownership. hello ASF licenses this file
* tooyou under hello Apache License, Version 2.0 (the
* "License"); you may not use this file except in compliance
* with hello License. You may obtain a copy of hello License at
*
* http://www.apache.org/licenses/LICENSE-2.0
*
* Unless required by applicable law or agreed tooin writing, software
* distributed under hello License is distributed on an "AS IS" BASIS,
* WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or     implied.
* See hello License for hello specific language governing permissions and
* limitations under hello License.
*/

package org.apache.hadoop.examples;

import java.io.IOException;
import java.math.BigDecimal;
import java.util.Iterator;

import org.apache.hadoop.conf.Configured;
import org.apache.hadoop.fs.FileSystem;
import org.apache.hadoop.fs.Path;
import org.apache.hadoop.io.BooleanWritable;
import org.apache.hadoop.io.LongWritable;
import org.apache.hadoop.io.SequenceFile;
import org.apache.hadoop.io.Writable;
import org.apache.hadoop.io.WritableComparable;
import org.apache.hadoop.io.SequenceFile.CompressionType;
import org.apache.hadoop.mapred.FileInputFormat;
import org.apache.hadoop.mapred.FileOutputFormat;
import org.apache.hadoop.mapred.JobClient;
import org.apache.hadoop.mapred.JobConf;
import org.apache.hadoop.mapred.MapReduceBase;
import org.apache.hadoop.mapred.Mapper;
import org.apache.hadoop.mapred.OutputCollector;
import org.apache.hadoop.mapred.Reducer;
import org.apache.hadoop.mapred.Reporter;
import org.apache.hadoop.mapred.SequenceFileInputFormat;
import org.apache.hadoop.mapred.SequenceFileOutputFormat;
import org.apache.hadoop.util.Tool;
import org.apache.hadoop.util.ToolRunner;

//A Map-reduce program tooestimate hello value of Pi
//using quasi-Monte Carlo method.
//
//Mapper:
//Generate points in a unit square
//and then count points inside/outside of hello inscribed circle of hello square.
//
//Reducer:
//Accumulate points inside/outside results from hello mappers.
//Let numTotal = numInside + numOutside.
//hello fraction numInside/numTotal is a rational approximation of
//hello value (Area of hello circle)/(Area of hello square),
//where hello area of hello inscribed circle is Pi/4
//and hello area of unit square is 1.
//Then, Pi is estimated value toobe 4(numInside/numTotal).
//

public class PiEstimator extends Configured implements Tool {
//tmp directory for input/output
static private final Path TMP_DIR = new Path(
PiEstimator.class.getSimpleName() + "_TMP_3_141592654");

//2-dimensional Halton sequence {H(i)},
//where H(i) is a 2-dimensional point and i >= 1 is hello index.
//Halton sequence is used toogenerate sample points for Pi estimation.
private static class HaltonSequence {
// Bases
static final int[] P = {2, 3};
//Maximum number of digits allowed
static final int[] K = {63, 40};

private long index;
private double[] x;
private double[][] q;
private int[][] d;

//Initialize tooH(startindex),
//so hello sequence begins with H(startindex+1).
HaltonSequence(long startindex) {
index = startindex;
x = new double[K.length];
q = new double[K.length][];
d = new int[K.length][];
for(int i = 0; i < K.length; i++) {
q[i] = new double[K[i]];
d[i] = new int[K[i]];
}

for(int i = 0; i < K.length; i++) {
long k = index;
x[i] = 0;

for(int j = 0; j < K[i]; j++) {
q[i][j] = (j == 0? 1.0: q[i][j-1])/P[i];
d[i][j] = (int)(k % P[i]);
k = (k - d[i][j])/P[i];
x[i] += d[i][j] * q[i][j];
}
}
}

//Compute next point.
//Assume hello current point is H(index).
//Compute H(index+1).
//@return a 2-dimensional point with coordinates in [0,1)^2
double[] nextPoint() {
index++;
for(int i = 0; i < K.length; i++) {
for(int j = 0; j < K[i]; j++) {
d[i][j]++;
x[i] += q[i][j];
if (d[i][j] < P[i]) {
break;
}
d[i][j] = 0;
x[i] -= (j == 0? 1.0: q[i][j-1]);
}
}
return x;
}
}

//Mapper class for Pi estimation.
//Generate points in a unit square and then
//count points inside/outside of hello inscribed circle of hello square.
public static class PiMapper extends MapReduceBase
implements Mapper<LongWritable, LongWritable, BooleanWritable, LongWritable> {

//Map method.
//@param offset samples starting from hello (offset+1)th sample.
//@param size hello number of samples for this map
//@param out output {ture->numInside, false->numOutside}
//@param reporter
public void map(LongWritable offset,
LongWritable size,
OutputCollector<BooleanWritable, LongWritable> out,
Reporter reporter) throws IOException {

final HaltonSequence haltonsequence = new HaltonSequence(offset.get());
long numInside = 0L;
long numOutside = 0L;

for(long i = 0; i < size.get(); ) {
//generate points in a unit square
final double[] point = haltonsequence.nextPoint();

//count points inside/outside of hello inscribed circle of hello square
final double x = point[0] - 0.5;
final double y = point[1] - 0.5;
if (x*x + y*y > 0.25) {
numOutside++;
} else {
numInside++;
}

//report status
i++;
if (i % 1000 == 0) {
reporter.setStatus("Generated " + i + " samples.");
}
}

//output map results
out.collect(new BooleanWritable(true), new LongWritable(numInside));
out.collect(new BooleanWritable(false), new LongWritable(numOutside));
}
}

//Reducer class for Pi estimation.
//Accumulate points inside/outside results from hello mappers.
public static class PiReducer extends MapReduceBase
implements Reducer<BooleanWritable, LongWritable, WritableComparable<?>, Writable> {

private long numInside = 0;
private long numOutside = 0;
private JobConf conf; //configuration for accessing hello file system

//Store job configuration.
@Override
public void configure(JobConf job) {
conf = job;
}

// Accumulate number of points inside/outside results from hello mappers.
// @param isInside Is hello points inside?
// @param values An iterator tooa list of point counts
// @param output dummy, not used here.
// @param reporter

public void reduce(BooleanWritable isInside,
Iterator<LongWritable> values,
OutputCollector<WritableComparable<?>, Writable> output,
Reporter reporter) throws IOException {
if (isInside.get()) {
for(; values.hasNext(); numInside += values.next().get());
} else {
for(; values.hasNext(); numOutside += values.next().get());
}
}

//Reduce task done, write output tooa file.
@Override
public void close() throws IOException {
//write output tooa file
Path outDir = new Path(TMP_DIR, "out");
Path outFile = new Path(outDir, "reduce-out");
FileSystem fileSys = FileSystem.get(conf);
SequenceFile.Writer writer = SequenceFile.createWriter(fileSys, conf,
outFile, LongWritable.class, LongWritable.class,
CompressionType.NONE);
writer.append(new LongWritable(numInside), new LongWritable(numOutside));
writer.close();
}
}

//Run a map/reduce job for estimating Pi.
//@return hello estimated value of Pi.
public static BigDecimal estimate(int numMaps, long numPoints, JobConf jobConf
)
throws IOException {
//setup job conf
jobConf.setJobName(PiEstimator.class.getSimpleName());

jobConf.setInputFormat(SequenceFileInputFormat.class);

jobConf.setOutputKeyClass(BooleanWritable.class);
jobConf.setOutputValueClass(LongWritable.class);
jobConf.setOutputFormat(SequenceFileOutputFormat.class);

jobConf.setMapperClass(PiMapper.class);
jobConf.setNumMapTasks(numMaps);

jobConf.setReducerClass(PiReducer.class);
jobConf.setNumReduceTasks(1);

// turn off speculative execution, because DFS doesn't handle
// multiple writers toohello same file.
jobConf.setSpeculativeExecution(false);

//setup input/output directories
final Path inDir = new Path(TMP_DIR, "in");
final Path outDir = new Path(TMP_DIR, "out");
FileInputFormat.setInputPaths(jobConf, inDir);
FileOutputFormat.setOutputPath(jobConf, outDir);

final FileSystem fs = FileSystem.get(jobConf);
if (fs.exists(TMP_DIR)) {
throw new IOException("Tmp directory " + fs.makeQualified(TMP_DIR)
+ " already exists. Remove it first.");
}
if (!fs.mkdirs(inDir)) {
throw new IOException("Cannot create input directory " + inDir);
}

//generate an input file for each map task
try {
for(int i=0; i < numMaps; ++i) {
final Path file = new Path(inDir, "part"+i);
final LongWritable offset = new LongWritable(i * numPoints);
final LongWritable size = new LongWritable(numPoints);
final SequenceFile.Writer writer = SequenceFile.createWriter(
fs, jobConf, file,
LongWritable.class, LongWritable.class, CompressionType.NONE);
try {
writer.append(offset, size);
} finally {
writer.close();
}
System.out.println("Wrote input for Map #"+i);
}

//start a map/reduce job
System.out.println("Starting Job");
final long startTime = System.currentTimeMillis();
JobClient.runJob(jobConf);
final double duration = (System.currentTimeMillis() - startTime)/1000.0;
System.out.println("Job Finished in " + duration + " seconds");

//read outputs
Path inFile = new Path(outDir, "reduce-out");
LongWritable numInside = new LongWritable();
LongWritable numOutside = new LongWritable();
SequenceFile.Reader reader = new SequenceFile.Reader(fs, inFile, jobConf);
try {
reader.next(numInside, numOutside);
} finally {
reader.close();
}

//compute estimated value
return BigDecimal.valueOf(4).setScale(20)
.multiply(BigDecimal.valueOf(numInside.get()))
.divide(BigDecimal.valueOf(numMaps))
.divide(BigDecimal.valueOf(numPoints));
} finally {
fs.delete(TMP_DIR, true);
}
}

//Parse arguments and then runs a map/reduce job.
//Print output in standard out.
//@return a non-zero if there is an error. Otherwise, return 0.
public int run(String[] args) throws Exception {
if (args.length != 2) {
System.err.println("Usage: "+getClass().getName()+" <nMaps> <nSamples>");
ToolRunner.printGenericCommandUsage(System.err);
return -1;
}

final int nMaps = Integer.parseInt(args[0]);
final long nSamples = Long.parseLong(args[1]);

System.out.println("Number of Maps = " + nMaps);
System.out.println("Samples per Map = " + nSamples);

final JobConf jobConf = new JobConf(getConf(), getClass());
System.out.println("Estimated value of Pi is "
+ estimate(nMaps, nSamples, jobConf));
return 0;
}

//main method for running it as a stand alone command.
public static void main(String[] argv) throws Exception {
System.exit(ToolRunner.run(null, new PiEstimator(), argv));
}
}
```

## <a name="appendix-d---hello-10gb-graysort-source-code"></a>Apéndice D - código fuente de hello de 10 gb graysort
código de Hello de hello TeraSort MapReduce programa se presenta para la inspección en esta sección.

```java
/**
    * Licensed toohello Apache Software Foundation (ASF) under one
    * or more contributor license agreements.  See hello NOTICE file
    * distributed with this work for additional information
    * regarding copyright ownership.  hello ASF licenses this file
    * tooyou under hello Apache License, Version 2.0 (the
    * "License"); you may not use this file except in compliance
    * with hello License.  You may obtain a copy of hello License at
    *
    *     http://www.apache.org/licenses/LICENSE-2.0
    *
    * Unless required by applicable law or agreed tooin writing, software
    * distributed under hello License is distributed on an "AS IS" BASIS,
    * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    * See hello License for hello specific language governing permissions and
    * limitations under hello License.
    */

package org.apache.hadoop.examples.terasort;

import java.io.IOException;
import java.io.PrintStream;
import java.net.URI;
import java.util.ArrayList;
import java.util.List;

import org.apache.commons.logging.Log;
import org.apache.commons.logging.LogFactory;
import org.apache.hadoop.conf.Configured;
import org.apache.hadoop.filecache.DistributedCache;
import org.apache.hadoop.fs.FileSystem;
import org.apache.hadoop.fs.Path;
import org.apache.hadoop.io.NullWritable;
import org.apache.hadoop.io.SequenceFile;
import org.apache.hadoop.io.Text;
import org.apache.hadoop.mapred.FileOutputFormat;
import org.apache.hadoop.mapred.JobClient;
import org.apache.hadoop.mapred.JobConf;
import org.apache.hadoop.mapred.Partitioner;
import org.apache.hadoop.util.Tool;
import org.apache.hadoop.util.ToolRunner;

/**
    * Generates hello sampled split points, launches hello job,
    * and waits for it toofinish.
    * <p>
    * toorun hello program:
    * <b>bin/hadoop jar hadoop-examples-*.jar terasort in-dir out-dir</b>
    */

public class TeraSort extends Configured implements Tool {
    private static final Log LOG = LogFactory.getLog(TeraSort.class);

    /**
    * A partitioner that splits text keys into roughly equal
    * partitions in a global sorted order.
    */

    static class TotalOrderPartitioner implements Partitioner<Text,Text>{
    private TrieNode trie;
    private Text[] splitPoints;

    /**
        * A generic trie node
        */
    static abstract class TrieNode {
        private int level;
        TrieNode(int level) {
        this.level = level;
        }
        abstract int findPartition(Text key);
        abstract void print(PrintStream strm) throws IOException;
        int getLevel() {
        return level;
        }
    }

    /**
        * An inner trie node that contains 256 children based on hello next
        * character.
        */
    static class InnerTrieNode extends TrieNode {
        private TrieNode[] child = new TrieNode[256];

        InnerTrieNode(int level) {
        super(level);
        }
        int findPartition(Text key) {
        int level = getLevel();
        if (key.getLength() <= level) {
            return child[0].findPartition(key);
        }
        return child[key.getBytes()[level]].findPartition(key);
        }
        void setChild(int idx, TrieNode child) {
        this.child[idx] = child;
        }
        void print(PrintStream strm) throws IOException {
        for(int ch=0; ch < 255; ++ch) {
            for(int i = 0; i < 2*getLevel(); ++i) {
            strm.print(' ');
            }
            strm.print(ch);
            strm.println(" ->");
            if (child[ch] != null) {
            child[ch].print(strm);
            }
        }
        }
    }

    /**
        * A leaf trie node that does string compares toofigure out where hello given
        * key belongs between lower..upper.
        */
    static class LeafTrieNode extends TrieNode {
        int lower;
        int upper;
        Text[] splitPoints;
        LeafTrieNode(int level, Text[] splitPoints, int lower, int upper) {
        super(level);
        this.splitPoints = splitPoints;
        this.lower = lower;
        this.upper = upper;
        }
        int findPartition(Text key) {
        for(int i=lower; i<upper; ++i) {
            if (splitPoints[i].compareTo(key) >= 0) {
            return i;
            }
        }
        return upper;
        }
        void print(PrintStream strm) throws IOException {
        for(int i = 0; i < 2*getLevel(); ++i) {
            strm.print(' ');
        }
        strm.print(lower);
        strm.print(", ");
        strm.println(upper);
        }
    }

    /**
        * Read hello cut points from hello given sequence file.
        * @param fs hello file system
        * @param p hello path tooread
        * @param job hello job config
        * @return hello strings toosplit hello partitions on
        * @throws IOException
        */
    private static Text[] readPartitions(FileSystem fs, Path p,
                                            JobConf job) throws IOException {
        SequenceFile.Reader reader = new SequenceFile.Reader(fs, p, job);
        List<Text> parts = new ArrayList<Text>();
        Text key = new Text();
        NullWritable value = NullWritable.get();
        while (reader.next(key, value)) {
        parts.add(key);
        key = new Text();
        }
        reader.close();
        return parts.toArray(new Text[parts.size()]);
    }

    /**
        * Given a sorted set of cut points, build a trie that will find hello correct
        * partition quickly.
        * @param splits hello list of cut points
        * @param lower hello lower bound of partitions 0..numPartitions-1
        * @param upper hello upper bound of partitions 0..numPartitions-1
        * @param prefix hello prefix that we have already checked against
        * @param maxDepth hello maximum depth we will build a trie for
        * @return hello trie node that will divide hello splits correctly
        */
    private static TrieNode buildTrie(Text[] splits, int lower, int upper,
                                        Text prefix, int maxDepth) {
        int depth = prefix.getLength();
        if (depth >= maxDepth || lower == upper) {
        return new LeafTrieNode(depth, splits, lower, upper);
        }
        InnerTrieNode result = new InnerTrieNode(depth);
        Text trial = new Text(prefix);
        // append an extra byte on toohello prefix
        trial.append(new byte[1], 0, 1);
        int currentBound = lower;
        for(int ch = 0; ch < 255; ++ch) {
        trial.getBytes()[depth] = (byte) (ch + 1);
        lower = currentBound;
        while (currentBound < upper) {
            if (splits[currentBound].compareTo(trial) >= 0) {
            break;
            }
            currentBound += 1;
        }
        trial.getBytes()[depth] = (byte) ch;
        result.child[ch] = buildTrie(splits, lower, currentBound, trial,
                                        maxDepth);
        }
        // pick up hello rest
        trial.getBytes()[depth] = 127;
        result.child[255] = buildTrie(splits, currentBound, upper, trial,
                                    maxDepth);
        return result;
    }

    public void configure(JobConf job) {
        try {
        FileSystem fs = FileSystem.getLocal(job);
        Path partFile = new Path(TeraInputFormat.PARTITION_FILENAME);
        splitPoints = readPartitions(fs, partFile, job);
        trie = buildTrie(splitPoints, 0, splitPoints.length, new Text(), 2);
        } catch (IOException ie) {
        throw new IllegalArgumentException("can't read paritions file", ie);
        }
    }

    public TotalOrderPartitioner() {
    }

    public int getPartition(Text key, Text value, int numPartitions) {
        return trie.findPartition(key);
    }

    }

    public int run(String[] args) throws Exception {
    LOG.info("starting");
    JobConf job = (JobConf) getConf();
    Path inputDir = new Path(args[0]);
    inputDir = inputDir.makeQualified(inputDir.getFileSystem(job));
    Path partitionFile = new Path(inputDir, TeraInputFormat.PARTITION_FILENAME);
    URI partitionUri = new URI(partitionFile.toString() +
                                "#" + TeraInputFormat.PARTITION_FILENAME);
    TeraInputFormat.setInputPaths(job, new Path(args[0]));
    FileOutputFormat.setOutputPath(job, new Path(args[1]));
    job.setJobName("TeraSort");
    job.setJarByClass(TeraSort.class);
    job.setOutputKeyClass(Text.class);
    job.setOutputValueClass(Text.class);
    job.setInputFormat(TeraInputFormat.class);
    job.setOutputFormat(TeraOutputFormat.class);
    job.setPartitionerClass(TotalOrderPartitioner.class);
    TeraInputFormat.writePartitionFile(job, partitionFile);
    DistributedCache.addCacheFile(partitionUri, job);
    DistributedCache.createSymlink(job);
    job.setInt("dfs.replication", 1);
    TeraOutputFormat.setFinalSync(job, true);
    JobClient.runJob(job);
    LOG.info("done");
    return 0;
    }

    /**
    * @param args
    */

    public static void main(String[] args) throws Exception {
    int res = ToolRunner.run(new JobConf(), new TeraSort(), args);
    System.exit(res);
    }
}
```

[hdinsight-sdk-documentation]: https://msdn.microsoft.com/library/azure/dn479185.aspx

[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-introduction]: hdinsight-hadoop-introduction.md

[powershell-install-configure]: /powershell/azureps-cmdlets-docs

[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md

[hdinsight-samples]: hdinsight-run-samples.md
[hdinsight-sample-10gb-graysort]: #hdinsight-sample-10gb-graysort
[hdinsight-sample-csharp-streaming]: #hdinsight-sample-csharp-streaming
[hdinsight-sample-pi-estimator]: #hdinsight-sample-pi-estimator
[hdinsight-sample-wordcount]: #hdinsight-sample-wordcount

[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md

[streamreader]: http://msdn.microsoft.com/library/system.io.streamreader.aspx
[console-writeline]: http://msdn.microsoft.com/library/system.console.writeline
[stdin-stdout-stderr]: https://msdn.microsoft.com/library/3x292kth.aspx
