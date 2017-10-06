---
title: "aaaDebug y analizar los servicios de Hadoop con los volcados del montón - Azure | Documentos de Microsoft"
description: "Recopilar volcados de memoria del montón para servicios de Hadoop y colocar dentro de la cuenta de almacenamiento de blobs de Azure para la depuración y análisis de hello automáticamente."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: e4ec4ebb-fd32-4668-8382-f956581485c4
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 70fbc2d6d97d35b0d7b1d9149673b02ae1878eb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="collect-heap-dumps-in-blob-storage-toodebug-and-analyze-hadoop-services"></a>Recopilar volcados de memoria del montón en toodebug de almacenamiento de blobs y analizar los servicios Hadoop
[!INCLUDE [heapdump-selector](../../includes/hdinsight-selector-heap-dump.md)]

Los volcados del montón contienen una instantánea de memoria de la aplicación hello, incluidos los valores de hello de variables en tiempo de Hola se creó el volcado de Hola. Por ello, estos volcados resultan útiles a la hora de diagnosticar cualquier problema que ocurra en tiempo de ejecución. Los volcados del montón pueden recopilarse para servicios de Hadoop y colocar dentro de la cuenta de almacenamiento de blobs de Azure de un usuario en HDInsightHeapDumps Hola automáticamente /.

colección de Hola de volcados de memoria del montón para diversos servicios debe estar habilitado para los servicios en clústeres individuales. valor predeterminado de Hola para esta característica es toobe off para un clúster. Estos archivos de volcado de montón pueden ser grandes, por lo que es cuenta de almacenamiento Blob de toomonitor aconsejable Hola donde se va a guardar una vez que se ha habilitado la colección de Hola.

> [!IMPORTANT]
> Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior. Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement). información de Hello en este artículo solo aplica en función de tooWindows HDInsight. Para obtener más información sobre el HDInsight basado en Linux, consulte [Habilitar volcados de memoria para servicios de Hadoop en el HDInsight basado en Linux](hdinsight-hadoop-collect-debug-heap-dump-linux.md)


## <a name="eligible-services-for-heap-dumps"></a>Servicios de volcados de memoria aptos
Puede habilitar los volcados del montón para hello siguientes servicios:

* **hcatalog** - tempelton
* **hive** - hiveserver2, metastore, derbyserver
* **mapreduce** - jobhistoryserver
* **yarn** - resourcemanager, nodemanager, timelineserver
* **hdfs** - datanode, secondarynamenode, namenode

## <a name="configuration-elements-that-enable-heap-dumps"></a>Elementos de configuración que habilitan los volcados de memoria
tooturn en los volcados del montón para un servicio, necesita los elementos de configuración adecuada de hello tooset en la sección de Hola para ese servicio, que se especifica mediante **service_name**.

    "javaargs.<service_name>.XX:+HeapDumpOnOutOfMemoryError" = "-XX:+HeapDumpOnOutOfMemoryError",
    "javaargs.<service_name>.XX:HeapDumpPath" = "-XX:HeapDumpPath=c:\Dumps\<service_name>_%date:~4,2%%date:~7,2%%date:~10,2%%time:~0,2%%time:~3,2%%time:~6,2%.hprof"

Hola valo **service_name** puede ser cualquiera de los servicios de hello enumerados aquí: tempelton, hiveserver2, tienda de metadatos, derbyserver, jobhistoryserver, resourcemanager, nodemanager, timelineserver, datanode, secondarynamenode, o namenode.

## <a name="enable-using-azure-powershell"></a>Habilitar con Azure PowerShell
Por ejemplo, tooturn en los volcados del montón mediante Azure PowerShell para jobhistoryserver, puede usar Hola siguiente secuencia de comandos:

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

    $MapRedConfigValues = new-object 'Microsoft.WindowsAzure.Management.HDInsight.Cmdlet.DataObjects.AzureHDInsightMapReduceConfiguration'

    $MapRedConfigValues.Configuration = @{ "javaargs.jobhistoryserver.XX:+HeapDumpOnOutOfMemoryError"="-XX:+HeapDumpOnOutOfMemoryError" ; "javaargs.jobhistoryserver.XX:HeapDumpPath" = "-XX:HeapDumpPath=c:\\Dumps\\jobhistoryserver_%date:~4,2%_%date:~7,2%_%date:~10,2%_%time:~0,2%_%time:~3,2%_%time:~6,2%.hprof" }

## <a name="enable-using-net-sdk"></a>Habilitar con SDK para .NET
Por ejemplo, tooturn en los volcados del montón mediante el uso de hello Azure HDInsight .NET SDK para jobhistoryserver, puede usar Hola siguiente código:

    clusterInfo.MapReduceConfiguration.ConfigurationCollection.Add(new KeyValuePair<string, string>("javaargs.jobhistoryserver.XX:+HeapDumpOnOutOfMemoryError", "-XX:+HeapDumpOnOutOfMemoryError"));

    clusterInfo.MapReduceConfiguration.ConfigurationCollection.Add(new KeyValuePair<string, string>("javaargs.jobhistoryserver.XX:HeapDumpPath", "-XX:HeapDumpPath=c:\\Dumps\\jobhistoryserver_%date:~4,2%_%date:~7,2%_%date:~10,2%_%time:~0,2%_%time:~3,2%_%time:~6,2%.hprof"));
