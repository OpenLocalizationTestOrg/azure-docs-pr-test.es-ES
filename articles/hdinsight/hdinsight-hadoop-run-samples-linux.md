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
# <a name="run-hello-mapreduce-examples-included-in-hdinsight"></a>Ejecutar los ejemplos de hello MapReduce que se incluyen en HDInsight

[!INCLUDE [samples-selector](../../includes/hdinsight-run-samples-selector.md)]

Obtenga información acerca de cómo se incluyen ejemplos de MapReduce hello toorun con Hadoop en HDInsight.

## <a name="prerequisites"></a>Requisitos previos

* **Un clúster de HDInsight**: consulte [Introducción al uso de Hadoop con Hive en HDInsight en Linux](hdinsight-hadoop-linux-tutorial-get-started.md)

    > [!IMPORTANT]
    > Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior. Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* **Un cliente SSH**: para obtener más información, consulte [Uso de SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

## <a name="hello-mapreduce-examples"></a>ejemplos de Hello MapReduce

**Ubicación**: Hola ejemplos se encuentran en hello clúster de HDInsight en `/usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar`.

**Contenido**: Hola siguiendo los ejemplos incluido en este archivo:

* `aggregatewordcount`: Un agregado según el programa de mapreduce que recuentos de palabras de hello en los archivos de entrada de Hola.
* `aggregatewordhist`: Un agregado según el programa de mapreduce que calcula el histograma de Hola de palabras de hello en los archivos de entrada de Hola.
* `bbp`: Un programa de mapreduce que utiliza Bailey-Borwein-Plouffe toocompute dígitos exactos de Pi.
* `dbcount`: Un trabajo de ejemplo que cuente los registros de la vista de página de hello almacenados en una base de datos.
* `distbbp`: Un programa de mapreduce que utiliza un tipo BBP toocompute fórmulas de bits exacto de Pi.
* `grep`: Un programa de mapreduce que cuente Hola coincide con de una expresión regular en la entrada de Hola.
* `join`: trabajo que realiza una unión de conjuntos de datos ordenados con particiones equiparables.
* `multifilewc`: trabajo que cuenta las palabras de varios archivos.
* `pentomino`: Un icono de mapreduce diseñar soluciones de programa toofind toopentomino problemas.
* `pi`: programa de mapreduce que calcula Pi mediante un método cuasi Monte Carlo.
* `randomtextwriter`: programa de mapreduce que escribe 10 GB de datos de texto aleatorios por nodo.
* `randomwriter`: programa de mapreduce que escribe 10 GB de datos aleatorios por nodo.
* `secondarysort`: Un ejemplo define una toohello de orden secundaria reducir fase.
* `sort`: Un programa de mapreduce que ordena datos Hola escritos Hola de escritura aleatoria.
* `sudoku`: solucionador de sudokus.
* `teragen`: Generar datos para terasort Hola.
* `terasort`: Ejecute hello terasort.
* `teravalidate`: comprueba los resultados de la ordenación de terabytes (terasort).
* `wordcount`: Un programa de mapreduce que recuentos de palabras de hello en los archivos de entrada de Hola.
* `wordmean`: Un programa de mapreduce que cuenta la duración media de Hola de palabras de hello en los archivos de entrada de Hola.
* `wordmedian`: Archivos de entrada un programa de mapreduce que cuenta la longitud de mediana de Hola de palabras de Hola Hola.
* `wordstandarddeviation`: Archivos de entrada un programa de mapreduce que cuenta la desviación estándar de Hola de longitud de Hola de palabras de Hola Hola.

**El código fuente**: código fuente de estos ejemplos se incluye en hello clúster de HDInsight en `/usr/hdp/2.2.4.9-1/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples`.

> [!NOTE]
> Hola `2.2.4.9-1` Hola ruta de acceso es la versión de Hola de hello Hortonworks Data Platform para clúster de HDInsight de Hola y pueden ser diferente para el clúster.

## <a name="run-hello-wordcount-example"></a>Ejecutar el ejemplo de wordcount Hola

1. Conectar tooHDInsight mediante SSH. Para más información, consulte [Uso SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

2. De hello `username@#######:~$` símbolo del sistema, use Hola siguiendo los ejemplos del comando toolist hello:

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar
    ```

    Este comando genera lista Hola de ejemplo desde la sección anterior de Hola de este documento.

3. Hola de uso siguiente comando tooget ayuda de un ejemplo concreto. En este caso, Hola **wordcount** ejemplo:

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount
    ```

    Recibirá el siguiente mensaje de Hola:

        Usage: wordcount <in> [<in>...] <out>

    Este mensaje indica que puede proporcionar varias rutas de acceso de entrada para los documentos de origen de Hola. ruta de acceso final Hello es donde se almacena el resultado de hello (recuento de palabras en documentos de origen de hello).

4. Usar hello después toocount todas las palabras en hello blocs de notas de Leonardo Da Vinci, que se proporcionan como datos de ejemplo con el clúster:

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/davinciwordcount
    ```

    La entrada de este trabajo se lee desde `/example/data/gutenberg/davinci.txt`. La salida de este ejemplo se almacena en `/example/data/davinciwordcount`. Ambas rutas de acceso se encuentran en almacenamiento predeterminado para el clúster de hello, no el sistema de archivos local Hola.

   > [!NOTE]
   > Como se indicó en la Ayuda de hello para el ejemplo de wordcount hello, también puede especificar varios archivos de entrada. Por ejemplo, `hadoop jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/gutenberg/ulysses.txt /example/data/twowordcount` contaría las palabras de davinci.txt y ulysses.txt.

5. Cuando se completa el trabajo de hello, utilice Hola siguiendo la salida del comando tooview hello:

    ```bash
    hdfs dfs -cat /example/data/davinciwordcount/*
    ```

    Este comando concatena todos los archivos de salida de hello generados por el trabajo de Hola. Muestra la consola de toohello de salida de hello. Hola de salida es toohello similar siguiente texto:

        zum     1
        zur     1
        zwanzig 1
        zweite  1

    Cada línea representa una palabra y cuántas veces se produjo en hello los datos de entrada.

## <a name="hello-sudoku-example"></a>ejemplo de Hola Sudoku

[Sudoku](https://en.wikipedia.org/wiki/Sudoku) es un rompecabezas lógico compuesto por nueve cuadrículas de 3 × 3. Algunas celdas de cuadrícula de Hola tienen números, mientras que otros están en blanco y objetivo de hello es toosolve para las celdas en blanco de Hola. el vínculo anterior de Hello tiene más información sobre rompecabezas de hello, pero Hola de este ejemplo sirve toosolve para las celdas en blanco de Hola. Por lo que la entrada debería ser un archivo que se encuentra en hello siguiendo el formato:

* Nueve filas de nueve columnas;
* Cada columna puede contener un número o `?` (que indica una celda en blanco);
* Las celdas se separan por un espacio.

Hay un determinado tooconstruct de manera rompecabezas Sudoku; no puede repetirse un número en una columna o fila. Hay un ejemplo en clúster de HDInsight de Hola que se cree correctamente. Se encuentra en `/usr/hdp/*/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples/src/main/java/org/apache/hadoop/examples/dancing/puzzle1.dta` y contiene Hola siguiente texto:

    8 5 ? 3 9 ? ? ? ?
    ? ? 2 ? ? ? ? ? ?
    ? ? 6 ? 1 ? ? ? 2
    ? ? 4 ? ? 3 ? 5 9
    ? ? 8 9 ? 1 4 ? ?
    3 2 ? 4 ? ? 8 ? ?
    9 ? ? ? 8 ? 5 ? ?
    ? ? ? ? ? ? 2 ? ?
    ? ? ? ? 4 5 ? 7 8

Este problema de ejemplo a través de hello ejemplo Sudoku, toorun, utilice Hola comando siguiente:

```bash
yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar sudoku /usr/hdp/*/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples/src/main/java/org/apache/hadoop/examples/dancing/puzzle1.dta
```

resultados de Hello aparecen toohello similar siguiente texto:

    8 5 1 3 9 2 6 4 7
    4 3 2 6 7 8 1 9 5
    7 9 6 5 1 4 3 8 2
    6 1 4 8 2 3 7 5 9
    5 7 8 9 6 1 4 2 3
    3 2 9 4 5 7 8 1 6
    9 4 7 2 8 6 5 3 1
    1 8 5 7 3 9 2 6 4
    2 6 3 1 4 5 9 7 8

## <a name="pi--example"></a>Ejemplo de PI (π)

ejemplo de Hola a pi usa una estadística (tipo de Monte Carlo) valor del método tooestimate Hola de pi. Los puntos se colocan de forma aleatoria en un cuadrado unitario. cuadrado de Hello también contiene un círculo. probabilidad de que los puntos de Hola se sitúan dentro de círculo Hola Hola son toohello igual área no cliente de hello circle, pi/4. valor de Hola de pi se puede estimar de valor de Hola de 4R. R es la relación de hello del número de Hola de puntos que están dentro de círculo hello toohello número total de puntos que están dentro de cuadrado Hola. Hola Hola muestra de mayor tamaño puntos usados, que es mejor estimación de Hola Hola.

Use este ejemplo de Hola después toorun de comando. Este comando utiliza 16 mapas con el valor de 10.000.000 ejemplos tooestimate Hola de pi:

```bash
yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar pi 16 10000000
```

Hello valor devuelto por este comando es similar demasiado**3.14159155000000000000**. Para las referencias, hello 10 primeros decimales de pi son 3.1415926535.

## <a name="10-gb-greysort-example"></a>Ejemplo de Greysort de 10 GB

GraySort es una ordenación de pruebas comparativas. métrica de Hello es la tasa de ordenación de hello (TB/minuto) que se logra al ordenar grandes cantidades de datos, normalmente un 100 TB mínimo.

Este ejemplo utiliza solo 10 GB de datos, para así poder ejecutarlo relativamente rápido. Usa las aplicaciones de MapReduce Hola desarrolladas por Owen O'Malley y Arun Murthy. Estas aplicaciones habían ganado el criterio de referencia de hello anual uso general ("daytona") terabyte ordenación en 2009, con una velocidad de 0.578 TB/min (100 TB en 173 minutos). Para obtener más información sobre este y otros criterios de ordenación de referencia, vea hello [Sortbenchmark](http://sortbenchmark.org/) sitio.

Este ejemplo utiliza tres conjuntos de programas de MapReduce:

* **TeraGen**: MapReduce de un programa que genera filas de datos toosort

* **TeraSort**: ejemplos de datos de entrada de Hola y utiliza datos de hello toosort MapReduce en un orden total

    TeraSort es una ordenación MapReduce estándar, salvo por el particionador personalizado. particionador de Hello usa una lista ordenada de claves de n-1 muestreada que definen el intervalo de claves de Hola para cada reduce. En particular, todas las claves de este tipo que muestra [i-1] < = clave < [i] de ejemplo se envían tooreduce. Este particionador garantiza que las salidas de Hola de reducen i es todos los menores de reducir la salida de hello de i + 1.

* **TeraValidate**: MapReduce de un programa que valida que los resultados del Hola global está ordenada

    Crea una asignación por cada archivo en el directorio de salida de hello, y cada asignación garantiza que cada clave es menor o igual toohello anterior. función de asignación de Hello genera registros de hello primero y último claves de cada archivo. Hola reduce (función) garantiza que Hola primera clave de archivo i es mayor que la clave de la última Hola de i-1 de archivo. Los problemas se notifican como una salida de hello reducir la fase, con claves de Hola que no están ordenadas.

Use Hola siguientes pasos le indican datos toogenerate, ordenar y, a continuación, validar salida de hello:

1. Generar 10 GB de datos, que es el almacenamiento de forma predeterminada del clúster de HDInsight de toohello almacenado en `/example/data/10GB-sort-input`:

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar teragen -Dmapred.map.tasks=50 100000000 /example/data/10GB-sort-input
    ```

    Hola `-Dmapred.map.tasks` indica cuántos toouse de tareas de asignación para este trabajo de Hadoop. parámetros de Hello dos final indicar Hola trabajo toocreate 10 GB de datos y toostore en `/example/data/10GB-sort-input`.

2. Usar hello comando toosort Hola datos siguientes:

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar terasort -Dmapred.map.tasks=50 -Dmapred.reduce.tasks=25 /example/data/10GB-sort-input /example/data/10GB-sort-output
    ```

    Hola `-Dmapred.reduce.tasks` indica Hadoop cuántos reducen toouse de tareas de trabajo de Hola. Hola dos últimos parámetros Hola solo entrada y ubicaciones de los datos de salida.

3. Usar hello toovalidate Hola datos generados por orden de hello siguientes:

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar teravalidate -Dmapred.map.tasks=50 -Dmapred.reduce.tasks=25 /example/data/10GB-sort-output /example/data/10GB-sort-validate
    ```

## <a name="next-steps"></a>Pasos siguientes

De este artículo, ha aprendido cómo ejemplos de hello toorun incluyen con hello clústeres de HDInsight basados en Linux. Para ver los tutoriales sobre el uso de Pig, Hive y MapReduce con HDInsight, vea Hola temas siguientes:

* [Uso de Pig con Hadoop en HDInsight][hdinsight-use-pig]
* [Uso de Hive con Hadoop en HDInsight][hdinsight-use-hive]
* [Uso de MapReduce con Hadoop en HDInsight][hdinsight-use-mapreduce]

[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-sdk-documentation]: https://msdn.microsoft.com/library/azure/dn479185.aspx

[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-introduction]: hdinsight-hadoop-introduction.md



[hdinsight-samples]: hdinsight-run-samples.md

[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
