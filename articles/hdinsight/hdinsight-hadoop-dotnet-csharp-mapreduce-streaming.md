---
title: aaaUse C# con MapReduce en Hadoop en HDInsight - Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse C# toocreate MapReduce soluciones con Hadoop en HDInsight de Azure."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: d83def76-12ad-4538-bb8e-3ba3542b7211
ms.custom: hdinsightactive
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: dd8b684e74155bc1a37d4ab8d6f9033276ef5aa3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-c-with-mapreduce-streaming-on-hadoop-in-hdinsight"></a>Uso de C# con el streaming de MapReduce en Hadoop en HDInsight

Obtenga información acerca de cómo toouse C# toocreate una solución de MapReduce en HDInsight.

> [!IMPORTANT]
> Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior. Para obtener más información, consulte el artículo relativo al [control de versiones de componentes de HDInsight](hdinsight-component-versioning.md).

Streaming de Hadoop es una utilidad que le permite toorun MapReduce trabajos mediante un script o un archivo ejecutable. En este ejemplo, .NET es tooimplement usado Hola asignador y reductor para una solución de recuento de palabras.

## <a name="net-on-hdinsight"></a>.NET en HDInsight

__HDInsight basados en Linux__ clústeres uso [Mono (https://mono-project.com)](https://mono-project.com) toorun aplicaciones. NET. La versión 4.2.1 de Mono está incluida en la versión 3.5 de HDInsight. Para obtener más información sobre la versión de Hola de Mono incluido con HDInsight, vea [versiones de componentes de HDInsight](hdinsight-component-versioning.md). toouse una versión específica de Mono, vea hello [instalación o una actualización Mono](hdinsight-hadoop-install-mono.md) documento.

Si desea conocer más detalles sobre la compatibilidad entre Mono y las versiones de .NET Framework, consulte la página en la que se trata la [compatibilidad de Mono](http://www.mono-project.com/docs/about-mono/compatibility/).

## <a name="how-hadoop-streaming-works"></a>Funcionamiento del streaming de Hadoop

proceso básico de Hello utilizado para la transmisión por secuencias en este documento es como sigue:

1. Hadoop pasa STDIN asignador de datos de toohello (mapper.exe en este ejemplo).
2. el asignador de Hello procesa los datos de Hola y emite tooSTDOUT de pares clave/valor delimitado por tabuladores.
3. salida de Hello lee hadoop y, a continuación, pasar STDIN toohello reductor (reducer.exe en este ejemplo).
4. reductor de Hello lee los pares de clave/valor Hola delimitado por tabuladores, procesa los datos de hello y, a continuación, emite el resultado de hello como pares de clave/valor delimitado por tabulaciones en STDOUT.
5. salida de Hello lee hadoop y escribe toohello directorio de salida.

Para obtener más información sobre el streaming, consulte la página relativa al [streaming de Hadoop (https://hadoop.apache.org/docs/r2.7.1/hadoop-streaming/HadoopStreaming.html)](https://hadoop.apache.org/docs/r2.7.1/hadoop-streaming/HadoopStreaming.html).

## <a name="prerequisites"></a>Requisitos previos

* Estar familiarizado con la escritura y la compilación del código C# orientado a .NET Framework 4.5. Hola pasos de este documento, use Visual Studio de 2017.

* Un clúster de toohello de los archivos .exe de manera tooupload. Hello pasos en este documento utilizan Hola Data Lake Tools por Visual Studio tooupload Hola archivos tooprimary almacenamiento de clúster de Hola.

* Azure PowerShell o un cliente de SSH.

* Hadoop en un clúster de HDInsight. Para obtener más información sobre cómo crear un clúster, consulte [Creación de un clúster de HDInsight](hdinsight-provision-clusters.md).

## <a name="create-hello-mapper"></a>Crear un asignador de Hola

En Visual Studio, cree una nueva __aplicación de consola__ denominada __mapper__. Usar hello después el código de aplicación hello:

```csharp
using System;
using System.Text.RegularExpressions;

namespace mapper
{
    class Program
    {
        static void Main(string[] args)
        {
            string line;
            //Hadoop passes data toohello mapper on STDIN
            while((line = Console.ReadLine()) != null)
            {
                // We only want words, so strip out punctuation, numbers, etc.
                var onlyText = Regex.Replace(line, @"\.|;|:|,|[0-9]|'", "");
                // Split at whitespace.
                var words = Regex.Matches(onlyText, @"[\w]+");
                // Loop over hello words
                foreach(var word in words)
                {
                    //Emit tab-delimited key/value pairs.
                    //In this case, a word and a count of 1.
                    Console.WriteLine("{0}\t1",word);
                }
            }
        }
    }
}
```

Después de crear la aplicación hello, genérelo hello tooproduce `/bin/Debug/mapper.exe` archivo en el directorio del proyecto de Hola.

## <a name="create-hello-reducer"></a>Crear reductor Hola

En Visual Studio, cree una nueva __aplicación de consola__ denominada __reducer__. Usar hello después el código de aplicación hello:

```csharp
using System;
using System.Collections.Generic;

namespace reducer
{
    class Program
    {
        static void Main(string[] args)
        {
            //Dictionary for holding a count of words
            Dictionary<string, int> words = new Dictionary<string, int>();

            string line;
            //Read from STDIN
            while ((line = Console.ReadLine()) != null)
            {
                // Data from Hadoop is tab-delimited key/value pairs
                var sArr = line.Split('\t');
                // Get hello word
                string word = sArr[0];
                // Get hello count
                int count = Convert.ToInt32(sArr[1]);

                //Do we already have a count for hello word?
                if(words.ContainsKey(word))
                {
                    //If so, increment hello count
                    words[word] += count;
                } else
                {
                    //Add hello key toohello collection
                    words.Add(word, count);
                }
            }
            //Finally, emit each word and count
            foreach (var word in words)
            {
                //Emit tab-delimited key/value pairs.
                //In this case, a word and a count of 1.
                Console.WriteLine("{0}\t{1}", word.Key, word.Value);
            }
        }
    }
}
```

Después de crear la aplicación hello, genérelo hello tooproduce `/bin/Debug/reducer.exe` archivo en el directorio del proyecto de Hola.

## <a name="upload-toostorage"></a>Cargar toostorage

1. En Visual Studio, abra el **Explorador de servidores**.

2. Expanda **Azure** y, después, haga lo mismo con **HDInsight**.

3. Si se le solicitan, escriba sus credenciales de suscripción de Azure y, a continuación, haga clic en **Iniciar sesión**.

4. Expanda el clúster de HDInsight de Hola que desee toodeploy para esta aplicación. Una entrada con el texto hello __(cuenta de almacenamiento predeterminada)__ aparece.

    ![Explorador de servidores mostrando la cuenta de almacenamiento de hello para el clúster de Hola](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/storage.png)

    * Si se puede expandir esta entrada, que usa un __cuenta de almacenamiento de Azure__ como almacenamiento predeterminado para el clúster de Hola. archivos de Hola de tooview en almacenamiento predeterminado de Hola para clúster hello, expanda la entrada de hello y, a continuación, haga doble clic en hello __(contenedor predeterminado)__.

    * Si no se puede expandir esta entrada, que usa __almacén de Azure Data Lake__ como almacenamiento predeterminado de hello para el clúster de Hola. archivos de hello tooview en almacenamiento predeterminado de hello para el clúster de hello, haga doble clic en hello __(cuenta de almacenamiento predeterminada)__ entrada.

5. archivos .exe de tooupload hello, use uno de los siguientes métodos de hello:

    * Si usa un __cuenta de almacenamiento de Azure__, haga clic en el icono de carga de hello y, a continuación, examinar toohello **bin\debug** carpeta para hello **asignador** proyecto. Por último, seleccione hello **mapper.exe** de archivo y haga clic en **Aceptar**.

        ![icono para cargar](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/upload.png)
    
    * Si usa __almacén de Azure Data Lake__, haga clic en un área vacía en lista de archivos de hello y, a continuación, seleccione __cargar__. Por último, seleccione hello **mapper.exe** de archivo y haga clic en **abiertos**.

    Una vez Hola __mapper.exe__ carga haya finalizado, el proceso de carga de repetición Hola para hello __reducer.exe__ archivo.

## <a name="run-a-job-using-an-ssh-session"></a>Ejecución de un trabajo mediante una sesión de SSH

1. Use el clúster de HDInsight de toohello tooconnect SSH. Para más información, consulte [Uso SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Use uno de hello siguiendo el trabajo de MapReduce de hello toostart de comando:

    * Si utiliza __Data Lake Store__ como almacenamiento predeterminado:

        ```bash
        yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar -files adl:///mapper.exe,adl:///reducer.exe -mapper mapper.exe -reducer reducer.exe -input /example/data/gutenberg/davinci.txt -output /example/wordcountout
        ```
    
    * Si emplea __Azure Storage__ como almacenamiento predeterminado:

        ```bash
        yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar -files wasb:///mapper.exe,wasb:///reducer.exe -mapper mapper.exe -reducer reducer.exe -input /example/data/gutenberg/davinci.txt -output /example/wordcountout
        ```

    Hola lista siguiente describe lo que hace cada parámetro:

    * `hadoop-streaming.jar`: archivo jar de Hola que contiene la funcionalidad de MapReduce de streaming de Hola.
    * `-files`: Agrega hello `mapper.exe` y `reducer.exe` trabajo toothis de archivos. Hola `adl:///` o `wasb:///` antes de cada archivo es la raíz de toohello de ruta de acceso de Hola de almacenamiento predeterminado para el clúster de Hola.
    * `-mapper`: Especifica el archivo que implementa el asignador de Hola.
    * `-reducer`: Especifica qué archivo implementa reductor Hola.
    * `-input`: Hola los datos de entrada.
    * `-output`: directorio de salida de hello.

3. Cuando se completa el trabajo de MapReduce hello, utilice Hola siguiendo los resultados de Hola tooview:

    ```bash
    hdfs dfs -text /example/wordcountout/part-00000
    ```

    Hello texto siguiente es un ejemplo de datos de hello devueltos por este comando:

        you     1128
        young   38
        younger 1
        youngest        1
        your    338
        yours   4
        yourself        34
        yourselves      3
        youth   17

## <a name="run-a-job-using-powershell"></a>Ejecución de un trabajo mediante PowerShell

Use Hola después toorun de secuencia de comandos de PowerShell un trabajo MapReduce y descargar los resultados de Hola.

[!code-powershell[main](../../powershell_scripts/hdinsight/use-csharp-mapreduce/use-csharp-mapreduce.ps1?range=5-87)]

Este script le nombre de cuenta de inicio de sesión de clúster de hello y una contraseña, junto con el nombre de clúster de HDInsight Hola. Cuando se completa el trabajo de hello, salida de hello es descargado toohello `output.txt` archivo en secuencia de comandos de hello directory Hola se ejecutó desde. Hello texto siguiente es un ejemplo de datos de Hola Hola `output.txt` archivo:

    you     1128
    young   38
    younger 1
    youngest        1
    your    338
    yours   4
    yourself        34
    yourselves      3
    youth   17

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre el uso de MapReduce con HDInsight, consulte [Uso de MapReduce con HDInsight](hdinsight-use-mapreduce.md).

Para obtener información sobre la utilización de C# con Hive y Pig, consulte el artículo referente al [uso de una función de C# definida por el usuario con Hive y Pig](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md).

Para obtener información sobre cómo emplear C# con Storm en HDInsight, consulte el artículo relativo al [desarrollo de topologías de C# para Storm en HDInsight](hdinsight-storm-develop-csharp-visual-studio-topology.md).