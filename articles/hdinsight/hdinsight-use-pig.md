---
title: aaaUse Pig con Hadoop en HDInsight | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse de Pig con Hadoop en HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: acfeb52b-4b81-4a7d-af77-3e9908407404
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/15/2017
ms.author: larryfr
ms.openlocfilehash: 90850f2c742b8954c66ce277127e01b14fc3906f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-pig-with-hadoop-on-hdinsight"></a>Uso de Pig con Hadoop en HDInsight

Obtenga información acerca de cómo toouse [Apache Pig](http://pig.apache.org/) con HDInsight...

Pig es una plataforma para crear programas de Hadoop mediante un lenguaje de procedimientos que se conoce como *Pig Latin*. Pig es una alternativa tooJava para crear *MapReduce* soluciones y se incluye con HDInsight de Azure. Usar hello después hello toodiscover de tabla que Pig puede utilizarse con HDInsight de varias maneras:

| **Utilícelo** si desea... | ...un shell **interactivo** | ...procesamiento por**lotes** | ...con este **sistema operativo de clúster** | ...desde este **sistema operativo de cliente** |
|:--- |:---:|:---:|:--- |:--- |
| [SSH](hdinsight-hadoop-use-pig-ssh.md) |✔ |✔ |Linux |Linux, Unix, Mac OS X o Windows |
| [API DE REST](hdinsight-hadoop-use-pig-curl.md) |&nbsp; |✔ |Linux o Windows |Linux, Unix, Mac OS X o Windows |
| [.NET SDK para Hadoop](hdinsight-hadoop-use-pig-dotnet-sdk.md) |&nbsp; |✔ |Linux o Windows |Windows (por ahora) |
| [Windows PowerShell](hdinsight-hadoop-use-pig-powershell.md) |&nbsp; |✔ |Linux o Windows |Windows |
| [Escritorio remoto](hdinsight-hadoop-use-pig-remote-desktop.md) (HDInsight 3.2 y 3.3) |✔ |✔ |Windows |Windows |

> [!IMPORTANT]
> Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior. Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a id="why"></a>¿Por qué usar Pig?

Uno de los desafíos de Hola de procesamiento de datos mediante el uso de MapReduce en Hadoop consiste en implementar la lógica de procesamiento con solo una asignación y una función de reducción. Para el procesamiento complejo, que a menudo tienen toobreak procesamiento en varias operaciones de MapReduce que son encadenar juntos tooachieve resultado de hello deseado.

Pig permite toodefine procesar como una serie de transformaciones que Hola datos fluyen a través de la salida de hello deseado tooproduce.

lenguaje de Pig latino de Hello permite toodescribe Hola flujo de datos de entrada sin formato, a través de una o varias transformaciones, tooproduce salida de hello deseado. Los programas de Pig Latin siguen este patrón general:

* **Carga**: leer toobe datos manipulado Hola sistema de archivos

* **Transformar**: manipular datos Hola

* **Vuelque ni almacenar**: pantalla de toohello de datos de salida o en el almacén para el procesamiento

### <a name="user-defined-functions"></a>Funciones definidas por el usuario

Pig latino también admite funciones definidas por el usuario (UDF), lo que permite tooinvoke componentes externos que implementan la lógica que es difícil toomodel en Pig latino.

Para más información sobre Pig Latin, consulte el [manual de referencia de Pig Latin 1](http://pig.apache.org/docs/r0.7.0/piglatin_ref1.html) y el [manual de referencia de Pig Latin 2](http://pig.apache.org/docs/r0.7.0/piglatin_ref2.html).

Para obtener un ejemplo del uso de UDF con Pig, consulte Hola siguientes documentos:

* [Utilice DataFu con Pig en HDInsight](hdinsight-hadoop-use-pig-datafu-udf.md) - DataFu es una colección de UDF útiles mantenida por Apache
* [Uso de Python con Pig y Hive en HDInsight](hdinsight-python.md)
* [Uso de C# con Hive y Pig en HDInsight](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)

## <a id="data"></a>Datos de ejemplo

HDInsight proporciona diversos conjuntos de datos de ejemplo, que se almacenan en hello `/example/data` y `/HdiSamples` directorios. Son estos directorios en almacenamiento predeterminado de hello para el clúster. ejemplo de Hola Pig en este documento usa hello *log4j* de archivos de `/example/data/sample.log`.

Cada registro en el archivo hello consta de una línea de campos que contenga un `[LOG LEVEL]` campo gravedad de hello y tipo de hello tooshow, por ejemplo:

    2012-02-03 20:26:41 SampleClass3 [ERROR] verbose detail for id 1527353937

En el ejemplo anterior de hello, nivel de registro de hello es ERROR.

> [!NOTE]
> También puede generar un archivo de log4j mediante hello [Apache Log4j](http://en.wikipedia.org/wiki/Log4j) herramienta de registro y, a continuación, cargar ese blob tooyour de archivo. Vea [tooHDInsight de cargar datos](hdinsight-upload-data.md) para obtener instrucciones. Para obtener más información sobre el uso de los blobs en Azure Storage con HDInsight, consulte [Uso de Azure Blob Storage con HDInsight](hdinsight-hadoop-use-blob-storage.md).

## <a id="job"></a>Trabajo de ejemplo

siguiente trabajo de Pig latino Hello carga hello `sample.log` archivo de almacenamiento predeterminado de hello para el clúster de HDInsight. A continuación, realiza una serie de transformaciones que se produce un recuento de cómo muchas veces cada datos de entrada de hello en nivel de registro. resultados de Hola se escriben tooSTDOUT.

    LOGS = LOAD 'wasb:///example/data/sample.log';
    LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
    FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
    GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
    FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
    RESULT = order FREQUENCIES by COUNT desc;
    DUMP RESULT;

Hello siguiente imagen muestra un resumen de las transformaciones de qué hace toohello datos.

![Representación gráfica de las transformaciones de Hola][image-hdi-pig-data-transformation]

## <a id="run"></a>Ejecutar trabajo de Pig latino Hola

HDInsight puede ejecutar trabajos de Pig Latin mediante una variedad de métodos. Usar hello después toodecide tabla qué método es adecuado para usted, a continuación, siga el vínculo de Hola para ver un tutorial.

| **Utilícelo** si desea... | ...un shell **interactivo** | ...procesamiento por**lotes** | ...con este **sistema operativo de clúster** | ...de este **cliente** |
|:--- |:---:|:---:|:--- |:--- |
| [SSH](hdinsight-hadoop-use-pig-ssh.md) |✔ |✔ |Linux |Linux, Unix, Mac OS X o Windows |
| [Curl](hdinsight-hadoop-use-pig-curl.md) |&nbsp; |✔ |Linux o Windows |Linux, Unix, Mac OS X o Windows |
| [.NET SDK para Hadoop](hdinsight-hadoop-use-pig-dotnet-sdk.md) |&nbsp; |✔ |Linux o Windows |Windows (por ahora) |
| [Windows PowerShell](hdinsight-hadoop-use-pig-powershell.md) |&nbsp; |✔ |Linux o Windows |Windows |
| [Escritorio remoto](hdinsight-hadoop-use-pig-remote-desktop.md) (HDInsight 3.2 y 3.3) |✔ |✔ |Windows |Windows |

> [!IMPORTANT]
> Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior. Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="pig-and-sql-server-integration-services"></a>Pig y SQL Server Integration Services

Puede utilizar SQL Server Integration Services (SSIS) toorun un trabajo de Pig. Hola Feature Pack de Azure para SSIS proporciona Hola trabajan con trabajos de Pig en HDInsight de los componentes siguientes.

* [Tarea de Pig de Azure HDInsight][pigtask]

* [Administrador de conexiones de suscripción de Azure][connectionmanager]

Obtener más información sobre Hola Feature Pack de Azure para SSIS [aquí][ssispack].

## <a id="nextsteps"></a>Pasos siguientes
Ahora que ha aprendido cómo toouse Pig con HDInsight, Hola de uso siguiente vincula tooexplore otro toowork maneras con HDInsight de Azure.

* [Cargar datos tooHDInsight][hdinsight-upload-data]
* [Uso de Hive con HDInsight][hdinsight-use-hive]
* [Uso de Sqoop con HDInsight](hdinsight-use-sqoop.md)
* [Uso de Oozie con HDInsight](hdinsight-use-oozie.md)
* [Uso de trabajos de MapReduce con HDInsight][hdinsight-use-mapreduce]

[apachepig-home]: http://pig.apache.org/
[putty]: http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html
[curl]: http://curl.haxx.se/
[pigtask]: http://msdn.microsoft.com/library/mt146781(v=sql.120).aspx
[connectionmanager]: http://msdn.microsoft.com/library/mt146773(v=sql.120).aspx
[ssispack]: http://msdn.microsoft.com/library/mt146770(v=sql.120).aspx


[hdinsight-upload-data]: hdinsight-upload-data.md

[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md

[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md#mapreduce-sdk

[Powershell-install-configure]: /powershell/azureps-cmdlets-docs

[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx


[image-hdi-pig-data-transformation]: ./media/hdinsight-use-pig/HDI.DataTransformation.gif
