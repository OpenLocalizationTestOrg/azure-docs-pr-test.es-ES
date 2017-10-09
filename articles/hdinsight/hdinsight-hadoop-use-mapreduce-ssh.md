---
title: "aaaMapReduce y conexión de SSH con Hadoop en HDInsight - Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse SSH toorun MapReduce trabajos usando Hadoop en HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 844678ba-1e1f-4fda-b9ef-34df4035d547
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 9626577687fc5cc119a39d65a9c45298f57f81c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-mapreduce-with-hadoop-on-hdinsight-with-ssh"></a>Uso de MapReduce con Hadoop en HDInsight con SSH

[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

Obtenga información acerca de cómo toosubmit MapReduce trabajos desde un tooHDInsight de conexión de Secure Shell (SSH).

> [!NOTE]
> Si ya está familiarizado con el uso de Hadoop basado en Linux, servidores, pero están tooHDInsight nueva, vea [sugerencias de HDInsight basados en Linux](hdinsight-hadoop-linux-information.md).

## <a id="prereq"></a>Requisitos previos

* Un clúster de HDInsight basado en Linux (Hadoop en HDInsight)

  > [!IMPORTANT]
  > Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior. Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* Un cliente SSH. Para más información, consulte [Uso de SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

## <a id="ssh"></a>Conexión con SSH

Conecte el clúster toohello mediante SSH. Por ejemplo, hello siguiente comando conecta con el nombre de clúster de tooa **myhdinsight**:

```bash
ssh admin@myhdinsight-ssh.azurehdinsight.net
```

**Si utiliza una clave de certificado para la autenticación de SSH**, deberá toospecify ubicación de Hola de clave privada de hello en el sistema cliente, por ejemplo:

```bash
ssh -i ~/mykey.key admin@myhdinsight-ssh.azurehdinsight.net
```

**Si utiliza una contraseña para la autenticación de SSH**, necesitará tooprovide Hola contraseña cuando se le solicite.

Para obtener más información sobre cómo utilizar SSH con HDInsight, consulte [Uso de SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

## <a id="hadoop"></a>Uso de comandos Hadoop

1. Después de clúster de HDInsight toohello conectado, use Hola después comando toostart un trabajo de MapReduce:

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/WordCountOutput
    ```

    Este comando inicia hello `wordcount` (clase), que se encuentra en hello `hadoop-mapreduce-examples.jar` archivo. Usa hello `/example/data/gutenberg/davinci.txt` documento como entrada y salida se almacena en `/example/data/WordCountOutput`.

    > [!NOTE]
    > Para obtener más información acerca de estos datos de ejemplo de Hola y de trabajo de MapReduce, consulte [uso MapReduce en Hadoop en HDInsight](hdinsight-use-mapreduce.md).

2. trabajo de Hello emite detalles tal y como lo procesa y devuelve información toohello similar después de texto cuando se completa el trabajo de hello:

        File Input Format Counters
        Bytes Read=1395666
        File Output Format Counters
        Bytes Written=337623

3. Cuando se completa el trabajo de hello, utilice Hola siguientes archivos de salida de comando toolist hello:

    ```bash
    hdfs dfs -ls /example/data/WordCountOutput
    ```

    Este comando muestra dos archivos, `_SUCCESS` y `part-r-00000`. Hola `part-r-00000` archivo contiene la salida de hello para este trabajo.

    > [!NOTE]
    > Pueden que algunos de estos trabajos MapReduce divida resultados Hola entre varios **parte-r-###** archivos. Si es así, usar hello ### tooindicate Hola orden de los archivos de Hola de sufijos.

4. salida de hello tooview, Hola de uso siguiente comando:

    ```bash
    hdfs dfs -cat /example/data/WordCountOutput/part-r-00000
    ```

    Este comando muestra una lista de palabras de Hola que figuran en hello **wasb://example/data/gutenberg/davinci.txt** hello y archivo de número de veces que se produjo cada palabra. Hello texto siguiente es un ejemplo de Hola datos que se encuentra en el archivo hello:

        wreathed        3
        wreathing       1
        wreaths         1
        wrecked         3
        wrenching       1
        wretched        6
        wriggling       1

## <a id="summary"></a>Resumen

Como puede ver, comandos de Hadoop constan de una manera sencilla de toorun trabajos MapReduce en un clúster de HDInsight y, a continuación, ver la salida de trabajo Hola.

## <a id="nextsteps"></a>Pasos siguientes

Para obtener información general sobre los trabajos de MapReduce en HDInsight:

* [Uso de MapReduce en Hadoop de HDInsight](hdinsight-use-mapreduce.md)

Para obtener información sobre otras maneras de trabajar con Hadoop en HDInsight:

* [Uso de Hive con Hadoop en HDInsight](hdinsight-use-hive.md)
* [Uso de Pig con Hadoop en HDInsight](hdinsight-use-pig.md)
