---
title: aaaMapReduce y el escritorio remoto con Hadoop en HDInsight - Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse escritorio remoto tooconnect tooHadoop en HDInsight y ejecución de los trabajos de MapReduce."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 9d3a7b34-7def-4c2e-bb6c-52682d30dee8
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/12/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: bdbbcf59ca86dd1b170471aa9e12334a04c23667
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-mapreduce-in-hadoop-on-hdinsight-with-remote-desktop"></a>Uso de MapReduce de Hadoop en HDInsight con Escritorio remoto
[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

En este artículo, se obtenga información acerca de cómo tooconnect tooa Hadoop en HDInsight de clúster mediante Escritorio remoto y, a continuación, ejecutar trabajos MapReduce mediante comandos de Hadoop de Hola.

> [!IMPORTANT]
> Escritorio remoto solo está disponible en los clústeres de HDInsight basados en Windows. Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior. Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).
>
> Para HDInsight 3.4 o superior, consulte [MapReduce de uso mediante SSH](hdinsight-hadoop-use-mapreduce-ssh.md) para obtener información sobre cómo conectar el clúster de HDInsight toohello y ejecutar trabajos de MapReduce.

## <a id="prereq"></a>Requisitos previos
pasos de hello toocomplete en este artículo, se necesita Hola siguiente:

* Un clúster de HDInsight basado en Windows (Hadoop en HDInsight)
* Un equipo cliente con Windows 10, Windows 8 o Windows 7

## <a id="connect"></a>Conexión con el Escritorio remoto
Habilitar Escritorio remoto para el clúster de HDInsight de Hola y conéctela tooit siguiendo las instrucciones de hello en [conectarse mediante RDP de clústeres de tooHDInsight](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).

## <a id="hadoop"></a>Usar comandos de Hadoop de Hola
Cuando haya conectado toohello escritorio para clúster de HDInsight de hello, use Hola después toorun pasos un trabajo de MapReduce con hello Hadoop comando:

1. Desde el escritorio de HDInsight de hello, inicie hello **línea de comandos de Hadoop**. Se abre un nuevo símbolo en hello **c:\apps\dist\hadoop-&lt;número de versión >** directory.

   > [!NOTE]
   > número de versión de Hola cambia cuando se actualiza Hadoop. Hola **HADOOP_HOME** variable de entorno puede ser la ruta de acceso de toofind usado Hola. Por ejemplo, `cd %HADOOP_HOME%` directorio de Hadoop en toohello de directorios de cambios, sin necesidad de número de versión de hello tooknow.
   >
   >
2. Hola toouse **Hadoop** toorun un trabajo de MapReduce de ejemplo de comando, use Hola siguiente comando:

        hadoop jar hadoop-mapreduce-examples.jar wordcount wasb:///example/data/gutenberg/davinci.txt wasb:///example/data/WordCountOutput

    Esto inicia hello **wordcount** (clase), que se encuentra en hello **archivo hadoop mapreduce examples.jar** archivo Hola de directorio actual. Como entrada, utiliza hello **wasb://example/data/gutenberg/davinci.txt** documento y la salida se almacena en: **wasb: / / / ejemplo/datos/WordCountOutput**.

   > [!NOTE]
   > Para obtener más información acerca de estos datos de ejemplo de Hola y de trabajo de MapReduce, consulte <a href="hdinsight-use-mapreduce.md">uso MapReduce en Hadoop de HDInsight</a>.
   >
   >
3. trabajo de Hello emite detalles tal y como lo procesa y devuelve siguiente toohello similar de información cuando se complete el trabajo de hello:

        File Input Format Counters
        Bytes Read=1395666
        File Output Format Counters
        Bytes Written=337623
4. Cuando se complete el trabajo de hello, usar hello después de archivos de salida de comando toolist Hola almacenados en **wasb://example/data/WordCountOutput**:

        hadoop fs -ls wasb:///example/data/WordCountOutput

    Se deberían mostrar dos archivos, **_SUCCESS** y **part-r-00000**. Hola **parte-r-00000** archivo contiene la salida de hello para este trabajo.

   > [!NOTE]
   > Pueden que algunos de estos trabajos MapReduce divida resultados Hola entre varios **parte-r-###** archivos. Si es así, usar hello ### tooindicate Hola orden de los archivos de Hola de sufijos.
   >
   >
5. salida de hello tooview, Hola de uso siguiente comando:

        hadoop fs -cat wasb:///example/data/WordCountOutput/part-r-00000

    Esto muestra una lista de palabras de Hola que figuran en hello **wasb://example/data/gutenberg/davinci.txt** archivo, junto con el número de Hola de veces que se produjo cada palabra. Hola te mostramos un ejemplo de Hola datos que se incluirán en el archivo hello:

        wreathed        3
        wreathing       1
        wreaths         1
        wrecked         3
        wrenching       1
        wretched        6
        wriggling       1

## <a id="summary"></a>Resumen
Como puede ver, hello Hadoop comando proporciona una toorun fácilmente trabajos MapReduce en un clúster de HDInsight y, a continuación, ver la salida de trabajo Hola.

## <a id="nextsteps"></a>Pasos siguientes
Para obtener información general sobre los trabajos de MapReduce en HDInsight:

* [Uso de MapReduce en Hadoop de HDInsight](hdinsight-use-mapreduce.md)

Para obtener información sobre otras maneras de trabajar con Hadoop en HDInsight:

* [Uso de Hive con Hadoop en HDInsight](hdinsight-use-hive.md)
* [Uso de Pig con Hadoop en HDInsight](hdinsight-use-pig.md)
