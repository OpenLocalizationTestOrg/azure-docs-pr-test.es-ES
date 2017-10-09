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
# <a name="develop-python-streaming-mapreduce-programs-for-hdinsight"></a>Desarrollo de programas de MapReduce de streaming de Python para HDInsight

Obtenga información acerca de cómo toouse Python en operaciones de MapReduce de streaming. Hadoop proporciona una API de transmisión por secuencias para MapReduce que permite asignar toowrite y reduce las funciones en lenguajes distintos de Java. Hello pasos de este documento implementan Hola mapa y reducen los componentes de Python.

## <a name="prerequisites"></a>Requisitos previos

* Un clúster de Hadoop en HDInsight basado en Linux

  > [!IMPORTANT]
  > pasos de Hello en este documento requieren un clúster de HDInsight que usa Linux. Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior. Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* Un editor de texto

  > [!IMPORTANT]
  > editor de texto Hello debe utilizar LF como final de la línea de saludo. Usar un final de línea de CRLF produce errores cuando se ejecuta el trabajo de MapReduce de hello en clústeres de HDInsight basados en Linux.

* Hola `ssh` y `scp` comandos, o [PowerShell de Azure](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-3.8.0)

## <a name="word-count"></a>Recuento de palabras

Este ejemplo es un recuento de palabras básico implementado en un asignador y reductor de Python. el asignador de Hello divide las oraciones en palabras individuales y reductor Hola agrega palabras hello y recuentos de salida de hello tooproduce.

Hola después de diagrama de flujo muestra lo que sucede durante la asignación de Hola y reducir las fases.

![ilustración del proceso de mapreduce Hola](./media/hdinsight-hadoop-streaming-python/HDI.WordCountDiagram.png)

## <a name="streaming-mapreduce"></a>Transmisión de MapReduce

Hadoop le permite toospecify un archivo que contiene el mapa de Hola y reduce la lógica que se utiliza un trabajo. requisitos específicos de Hola para Hola de asignación y reducción lógica son:

* **Entrada**: Hola mapa y reducir los componentes deben leer datos de entrada desde STDIN.
* **Salida**: Hola mapa y reducir componentes deben escribir tooSTDOUT de datos de salida.
* **Formato de datos**: datos de hello consumido y generan deben ser un par de clave/valor, separado por un carácter de tabulación.

Python puede controlar fácilmente estos requisitos mediante hello `sys` tooread módulo STDIN y utilizar `print` tooprint tooSTDOUT. Hello tarea restante es simplemente aplicar formato a Hola datos con una pestaña (`\t`) carácter entre Hola clave y valor.

## <a name="create-hello-mapper-and-reducer"></a>Crear reductor y el asignador de Hola

1. Cree un archivo denominado `mapper.py` y use Hola siguiendo código como contenido de hello:

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

2. Cree un archivo denominado **reducer.py** y use Hola siguiendo código como contenido de hello:

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

## <a name="run-using-powershell"></a>Ejecución con PowerShell

tooensure que los archivos tienen finales de línea derecho de hello, Hola de uso siguiente script de PowerShell:

[!code-powershell[main](../../powershell_scripts/hdinsight/streaming-python/streaming-python.ps1?range=138-140)]

Usar hello siguientes PowerShell script tooupload Hola archivos, ejecutar trabajo de Hola y ver el resultado de hello:

[!code-powershell[main](../../powershell_scripts/hdinsight/streaming-python/streaming-python.ps1?range=5-134)]

## <a name="run-from-an-ssh-session"></a>Ejecución desde una sesión de SSH

1. Desde el entorno de desarrollo, en Hola mismo directorio como `mapper.py` y `reducer.py` archivos, usar hello siguiente comando:

    ```bash
    scp mapper.py reducer.py username@clustername-ssh.azurehdinsight.net:
    ```

    Reemplace `username` con el nombre de usuario SSH de hello para el clúster, y `clustername` con nombre hello del clúster.

    Este comando copia los archivos de Hola desde el nodo principal de hello sistema local toohello.

    > [!NOTE]
    > Si utiliza un toosecure de contraseña de su cuenta SSH, le pediremos contraseña Hola. Si usa una clave SSH, habrá hello toouse `-i` hello y parámetro de clave privada de toohello de ruta de acceso. Por ejemplo: `scp -i /path/to/private/key mapper.py reducer.py username@clustername-ssh.azurehdinsight.net:`.

2. Conectar toohello clúster a través de SSH:

    ```bash
    ssh username@clustername-ssh.azurehdinsight.net`
    ```

    Para más información, consulte [Uso de SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

3. REDUCER.py y tooensure hello mapper.py que Hola corregir finales de línea, siga Hola siguientes comandos:

    ```bash
    perl -pi -e 's/\r\n/\n/g' mapper.py
    perl -pi -e 's/\r\n/\n/g' reducer.py
    ```

4. Usar hello siguiendo el trabajo de MapReduce de comando toostart Hola.

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar -files mapper.py,reducer.py -mapper mapper.py -reducer reducer.py -input /example/data/gutenberg/davinci.txt -output /example/wordcountout
    ```

    Este comando tiene Hola siguientes componentes:

   * **hadoop-streaming.jar**: se usa cuando se realizan operaciones de streaming de MapReduce. Interfaces de Hadoop con código de hello externo MapReduce que proporcionan.

   * **-archivos**: Hola especificado se agrega trabajo de MapReduce toohello de archivos.

   * **-el asignador**: Hadoop indica que el archivo toouse Hola asignador.

   * **-reductor**: Hadoop indica que el archivo toouse Hola reductor.

   * **-entrada**: archivo de entrada de Hola que se debe contar palabras desde.

   * **-salida**: se escribió en el directorio de Hola que Hola de salida.

    A medida que trabaja el trabajo de MapReduce hello, proceso de Hola se muestra como porcentajes.

        15/02/05 19:01:04 INFO mapreduce.Job:  map 0% reduce 0%    15/02/05 19:01:16 INFO mapreduce.Job:  map 100% reduce 0%    15/02/05 19:01:27 INFO mapreduce.Job:  map 100% reduce 100%


5. salida de hello tooview, Hola de uso siguiente comando:

    ```bash
    hdfs dfs -text /example/wordcountout/part-00000
    ```

    Este comando muestra una lista de palabras y el número de veces palabra Hola se ha producido.

## <a name="next-steps"></a>Pasos siguientes

Ahora que ha aprendido cómo los trabajos de toouse MapRedcue de transmisión por secuencias con HDInsight, utilice Hola siguiendo vínculos tooexplore otro toowork maneras con HDInsight de Azure.

* [Uso de Hive con HDInsight](hdinsight-use-hive.md)
* [Uso de Pig con HDInsight](hdinsight-use-pig.md)
* [Uso de trabajos de MapReduce con HDInsight](hdinsight-use-mapreduce.md)
