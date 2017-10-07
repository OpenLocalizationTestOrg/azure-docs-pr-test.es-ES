---
title: aaaUse Hadoop Pig con Escritorio remoto en HDInsight - Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse Hola toorun Pig latino instrucciones de Pig comandos desde un clúster de Hadoop basado en Windows de tooa de conexión de escritorio remoto en HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: e034a286-de0f-465f-8bf1-3d085ca6abed
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/17/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 2a4565fa827cd45fdbe6194b0486df93a6561084
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="run-pig-jobs-from-a-remote-desktop-connection"></a>Ejecución de trabajos de Pig desde una conexión de Escritorio remoto
[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

Este documento proporciona un tutorial para utilizar instrucciones de Pig latino Hola Pig comandos toorun desde un clúster de HDInsight basados en Windows de tooa de conexión de escritorio remoto. Pig latino permite toocreate MapReduce aplicaciones, se describen las transformaciones de datos, en lugar de asignar y reducir las funciones.

> [!IMPORTANT]
> Escritorio remoto sólo está disponible en los clústeres de HDInsight que usa Windows como sistema operativo de Hola. Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior. Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).
>
> Para HDInsight 3.4 o superior, consulte [uso de Pig con HDInsight y SSH](hdinsight-hadoop-use-pig-ssh.md) para obtener información acerca de cómo ejecutar interactivamente Pig trabajos directamente en hello clúster desde una línea de comandos.

## <a id="prereq"></a>Requisitos previos
pasos de hello toocomplete en este artículo, deberá siguiente Hola.

* Un clúster de HDInsight basado en Windows (Hadoop en HDInsight)
* Un equipo cliente con Windows 10, Windows 8 o Windows 7

## <a id="connect"></a>Conexión con el Escritorio remoto
Habilitar Escritorio remoto para el clúster de HDInsight de Hola y conéctela tooit siguiendo las instrucciones de hello en [conectarse mediante RDP de clústeres de tooHDInsight](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).

## <a id="pig"></a>Usar comandos de Pig Hola
1. Una vez que una conexión a Escritorio remoto, iniciar hello **línea de comandos de Hadoop** mediante el icono de hello en el escritorio de Hola.
2. Usar hello siguiente toostart Hola Pig comando:

        %pig_home%\bin\pig

    Aparecerá un símbolo del sistema de `grunt>` .
3. Escriba Hola siguiente instrucción:

        LOGS = LOAD 'wasb:///example/data/sample.log';

    Este comando carga contenido de Hola de archivo sample.log de hello en el archivo de registros de hello. Puede ver contenido de Hola de archivo hello mediante Hola siguiente comando:

        DUMP LOGS;
4. Transformar datos de hello aplicando un nivel de registro de hello solo de tooextract de expresión regular de cada registro:

        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;

    Puede usar **VOLCAR** datos de hello tooview después de la transformación de Hola. En este caso, `DUMP LEVELS;`.
5. Continúe aplicando transformaciones utilizando Hola siguiendo las instrucciones. Use `DUMP` tooview resultado de hello de transformación de hello después de cada paso.

    <table>
    <tr>
    <th>Instrucción</th><th>Qué hace</th>
    </tr>
    <tr>
    <td>FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;</td><td>Quita las filas que contienen un valor null para el nivel de registro de hello y almacena los resultados de hello en FILTEREDLEVELS.</td>
    </tr>
    <tr>
    <td>GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;</td><td>Hola grupos filas por nivel de registro y almacena los resultados de hello en GROUPEDLEVELS.</td>
    </tr>
    <tr>
    <td>FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;</td><td>Crea un nuevo conjunto de datos que contiene cada valor de registro único y cuántas veces se produce. Esto se almacena en FRECUENCIAS</td>
    </tr>
    <tr>
    <td>RESULT = order FREQUENCIES by COUNT desc;</td><td>Ordena los niveles de registro de hello por recuento (descendente) y almacena en el resultado</td>
    </tr>
    </table>
6.También puede guardar los resultados de Hola de una transformación mediante hello `STORE` instrucción. Por ejemplo, hello siguiente comando guarda hello `RESULT` toohello **/example/data/pigout** directorio en el contenedor de almacenamiento predeterminado de hello para el clúster:

        STORE RESULT into 'wasb:///example/data/pigout'

   > [!NOTE]
   > Hola datos se almacenan en el directorio especificado de hello en los archivos denominados **parte nnnnn**. Si ya existe el directorio de hello, recibirá un mensaje de error.
   >
   >
7. Hola tooexit grunt símbolo del sistema, escriba Hola después de la instrucción.

        QUIT;

### <a name="pig-latin-batch-files"></a>Archivos por lotes de Pig Latin
También puede utilizar Hola Pig comando toorun latino Pig que se encuentra en un archivo.

1. Después de salir del símbolo del sistema de hello grunt, abra **el Bloc de notas** y crear un nuevo archivo denominado **pigbatch.pig** en hello **PIG_HOME %** directory.
2. Tipo o pegar siguiente de hello líneas en hello **pigbatch.pig** de archivos y, a continuación, guárdelo:

        LOGS = LOAD 'wasb:///example/data/sample.log';
        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
        FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
        GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
        FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
        RESULT = order FREQUENCIES by COUNT desc;
        DUMP RESULT;
3. Hola de uso después de hello toorun **pigbatch.pig** archivo mediante el comando de pig Hola.

        pig %PIG_HOME%\pigbatch.pig

    Cuando se completa el proceso por lotes de hello, debería ver Hola después de salida, que debe ser igual Hola como cuando usa `DUMP RESULT;` en pasos anteriores hello:

        (TRACE,816)
        (DEBUG,434)
        (INFO,96)
        (WARN,11)
        (ERROR,6)
        (FATAL,2)

## <a id="summary"></a>Resumen
Como puede ver, Hola comando Pig permite toointeractively ejecutar operaciones de MapReduce o ejecutar trabajos de Pig latinos que se almacenan en un archivo por lotes.

## <a id="nextsteps"></a>Pasos siguientes
Para obtener información general sobre Pig en HDInsight, siga estos pasos:

* [Uso de Pig con Hadoop en HDInsight](hdinsight-use-pig.md)

Para obtener información sobre otras maneras de trabajar con Hadoop en HDInsight:

* [Uso de Hive con Hadoop en HDInsight](hdinsight-use-hive.md)
* [Uso de MapReduce con Hadoop en HDInsight](hdinsight-use-mapreduce.md)
