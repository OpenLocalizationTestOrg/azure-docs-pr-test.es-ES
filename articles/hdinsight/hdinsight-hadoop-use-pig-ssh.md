---
title: "aaaUse Hadoop Pig mediante SSH en un clúster de HDInsight - Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo conectar tooa basado en Linux, Hadoop clúster mediante SSH y, a continuación, usar Hola Pig comando toorun Pig latino instrucciones interactivamente o como un lote de trabajo."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: b646a93b-4c51-4ba4-84da-3275d9124ebe
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 1da303e239b537e6b331b1d33010058582718c90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="run-pig-jobs-on-a-linux-based-cluster-with-hello-pig-command-ssh"></a>Ejecutar trabajos de Pig en un clúster basado en Linux con hello comando Pig (SSH)

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

Obtenga información acerca de cómo toointeractively ejecutar trabajos de Pig desde un clúster de HDInsight de tooyour de conexión SSH. Hola lenguaje de programación de Pig latino permite transformaciones toodescribe toohello aplicado entrada datos tooproduce Hola deseado de salida.

> [!IMPORTANT]
> Hello pasos de este documento requieren un clúster de HDInsight basados en Linux. Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior. Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a id="ssh"></a>Conexión con SSH

Use el clúster de HDInsight de tooyour tooconnect SSH. Hello en el ejemplo siguiente se conecta con el nombre de clúster de tooa **myhdinsight** como cuenta de hello denominada **sshuser**:

    ssh sshuser@myhdinsight-ssh.azurehdinsight.net

**Si proporciona una clave de certificado para la autenticación de SSH** cuando se creó el clúster de HDInsight de hello, puede que necesite toospecify ubicación de Hola de clave privada de hello en el sistema cliente.

    ssh sshuser@myhdinsight-ssh.azurehdinsight.net -i ~/mykey.key

**Si proporciona una contraseña para la autenticación de SSH** cuando se creó el clúster de HDInsight de hello, proporcionar contraseña de hello cuando se le solicite.

Para obtener más información sobre cómo utilizar SSH con HDInsight, consulte [Uso de SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

## <a id="pig"></a>Usar comandos de Pig Hola

1. Una vez conectado, inicie la interfaz de línea de comandos de Pig hello (CLI) mediante Hola siguiente comando:

        pig

    Después de un momento, debiera ver un símbolo de sistema de `grunt>` .

2. Escriba Hola siguiente instrucción:

        LOGS = LOAD '/example/data/sample.log';

    Este comando carga contenido de Hola de archivo sample.log de hello en los registros. Puede ver contenido de Hola de archivo hello mediante Hola siguiente instrucción:

        DUMP LOGS;

3. A continuación, transformar datos de hello aplicando un nivel de registro de hello solo de tooextract de expresión regular de cada registro mediante el uso de hello siguiente instrucción:

        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;

    Puede usar **VOLCAR** datos de hello tooview después de la transformación de Hola. En este caso, utilice `DUMP LEVELS;`.

4. Continúe aplicando transformaciones mediante instrucciones de hello en hello en la tabla siguiente:

    | Instrucción de Pig Latin | ¿Qué instrucción Hola realiza |
    | ---- | ---- |
    | `FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;` | Quita las filas que contienen un valor null para el nivel de registro de hello y almacena los resultados de hello en `FILTEREDLEVELS`. |
    | `GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;` | Hola grupos filas por nivel de registro y almacena los resultados de hello en `GROUPEDLEVELS`. |
    | `FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;` | Crea un conjunto de datos que contiene cada valor de registro único y cuántas veces se produce. conjunto de datos de Hola se almacena en `FREQUENCIES`. |
    | `RESULT = order FREQUENCIES by COUNT desc;` | Ordena los niveles de registro de hello por recuento (descendente) y almacena en `RESULT`. |

    > [!TIP]
    > Use `DUMP` tooview resultado de hello de transformación de hello después de cada paso.

5. También puede guardar los resultados de Hola de una transformación mediante hello `STORE` instrucción. Por ejemplo, después de la instrucción de hello guarda hello `RESULT` toohello `/example/data/pigout` directorio de almacenamiento predeterminado de hello para el clúster:

        STORE RESULT into '/example/data/pigout';

   > [!NOTE]
   > Hola datos se almacenan en el directorio especificado de hello en los archivos denominados `part-nnnnn`. Si ya existe el directorio de hello, recibirá un error.

6. Hola tooexit grunt símbolo del sistema, escriba Hola siguiente instrucción:

        QUIT;

### <a name="pig-latin-batch-files"></a>Archivos por lotes de Pig Latin

También puede utilizar Hola Pig comando toorun latino Pig contenidos en un archivo.

1. Después de salir del símbolo del sistema de hello grunt, siguiente Hola de uso del comando toopipe STDIN en un archivo denominado `pigbatch.pig`. Este archivo se crea en el directorio principal Hola Hola cuenta de usuario SSH.

        cat > ~/pigbatch.pig

2. Escriba o pegue Hola siguiendo las líneas y, a continuación, utilice Ctrl + D cuando termine.

        LOGS = LOAD '/example/data/sample.log';
        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
        FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
        GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
        FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
        RESULT = order FREQUENCIES by COUNT desc;
        DUMP RESULT;

3. Siguiente Hola de uso del comando hello toorun `pigbatch.pig` archivo mediante el comando de Pig Hola.

        pig ~/pigbatch.pig

    Una vez que finalice el trabajo por lotes de hello, vea Hola después de salida:

        (TRACE,816)
        (DEBUG,434)
        (INFO,96)
        (WARN,11)
        (ERROR,6)
        (FATAL,2)


## <a id="nextsteps"></a>Pasos siguientes

Para obtener información general sobre Pig en HDInsight, vea Hola siguiente documento:

* [Uso de Pig con Hadoop en HDInsight](hdinsight-use-pig.md)

Para obtener más información sobre otra maneras de toowork con Hadoop en HDInsight, vea Hola siguientes documentos:

* [Uso de Hive con Hadoop en HDInsight](hdinsight-use-hive.md)
* [Uso de MapReduce con Hadoop en HDInsight](hdinsight-use-mapreduce.md)
