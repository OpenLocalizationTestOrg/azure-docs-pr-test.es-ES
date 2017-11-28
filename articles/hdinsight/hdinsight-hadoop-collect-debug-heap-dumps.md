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
# <a name="collect-heap-dumps-in-blob-storage-toodebug-and-analyze-hadoop-services"></a><span data-ttu-id="293ba-103">Recopilar volcados de memoria del montón en toodebug de almacenamiento de blobs y analizar los servicios Hadoop</span><span class="sxs-lookup"><span data-stu-id="293ba-103">Collect heap dumps in Blob storage toodebug and analyze Hadoop services</span></span>
[!INCLUDE [heapdump-selector](../../includes/hdinsight-selector-heap-dump.md)]

<span data-ttu-id="293ba-104">Los volcados del montón contienen una instantánea de memoria de la aplicación hello, incluidos los valores de hello de variables en tiempo de Hola se creó el volcado de Hola.</span><span class="sxs-lookup"><span data-stu-id="293ba-104">Heap dumps contain a snapshot of hello application's memory, including hello values of variables at hello time hello dump was created.</span></span> <span data-ttu-id="293ba-105">Por ello, estos volcados resultan útiles a la hora de diagnosticar cualquier problema que ocurra en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="293ba-105">So they are useful for diagnosing problems that occur at run-time.</span></span> <span data-ttu-id="293ba-106">Los volcados del montón pueden recopilarse para servicios de Hadoop y colocar dentro de la cuenta de almacenamiento de blobs de Azure de un usuario en HDInsightHeapDumps Hola automáticamente /.</span><span class="sxs-lookup"><span data-stu-id="293ba-106">Heap dumps can be automatically collected for Hadoop services and placed inside hello Azure Blob storage account of a user under HDInsightHeapDumps/.</span></span>

<span data-ttu-id="293ba-107">colección de Hola de volcados de memoria del montón para diversos servicios debe estar habilitado para los servicios en clústeres individuales.</span><span class="sxs-lookup"><span data-stu-id="293ba-107">hello collection of heap dumps for various services must be enabled for services on individual clusters.</span></span> <span data-ttu-id="293ba-108">valor predeterminado de Hola para esta característica es toobe off para un clúster.</span><span class="sxs-lookup"><span data-stu-id="293ba-108">hello default for this feature is toobe off for a cluster.</span></span> <span data-ttu-id="293ba-109">Estos archivos de volcado de montón pueden ser grandes, por lo que es cuenta de almacenamiento Blob de toomonitor aconsejable Hola donde se va a guardar una vez que se ha habilitado la colección de Hola.</span><span class="sxs-lookup"><span data-stu-id="293ba-109">These heap dumps can be large, so it is advisable toomonitor hello Blob storage account where they are being saved once hello collection has been enabled.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="293ba-110">Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior.</span><span class="sxs-lookup"><span data-stu-id="293ba-110">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="293ba-111">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="293ba-111">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="293ba-112">información de Hello en este artículo solo aplica en función de tooWindows HDInsight.</span><span class="sxs-lookup"><span data-stu-id="293ba-112">hello information in this article only applies tooWindows-based HDInsight.</span></span> <span data-ttu-id="293ba-113">Para obtener más información sobre el HDInsight basado en Linux, consulte [Habilitar volcados de memoria para servicios de Hadoop en el HDInsight basado en Linux](hdinsight-hadoop-collect-debug-heap-dump-linux.md)</span><span class="sxs-lookup"><span data-stu-id="293ba-113">For information on Linux-based HDInsight, see [Enable heap dumps for Hadoop services on Linux-based HDInsight](hdinsight-hadoop-collect-debug-heap-dump-linux.md)</span></span>


## <a name="eligible-services-for-heap-dumps"></a><span data-ttu-id="293ba-114">Servicios de volcados de memoria aptos</span><span class="sxs-lookup"><span data-stu-id="293ba-114">Eligible services for heap dumps</span></span>
<span data-ttu-id="293ba-115">Puede habilitar los volcados del montón para hello siguientes servicios:</span><span class="sxs-lookup"><span data-stu-id="293ba-115">You can enable heap dumps for hello following services:</span></span>

* <span data-ttu-id="293ba-116">**hcatalog** - tempelton</span><span class="sxs-lookup"><span data-stu-id="293ba-116">**hcatalog** - tempelton</span></span>
* <span data-ttu-id="293ba-117">**hive** - hiveserver2, metastore, derbyserver</span><span class="sxs-lookup"><span data-stu-id="293ba-117">**hive** - hiveserver2, metastore, derbyserver</span></span>
* <span data-ttu-id="293ba-118">**mapreduce** - jobhistoryserver</span><span class="sxs-lookup"><span data-stu-id="293ba-118">**mapreduce** - jobhistoryserver</span></span>
* <span data-ttu-id="293ba-119">**yarn** - resourcemanager, nodemanager, timelineserver</span><span class="sxs-lookup"><span data-stu-id="293ba-119">**yarn** - resourcemanager, nodemanager, timelineserver</span></span>
* <span data-ttu-id="293ba-120">**hdfs** - datanode, secondarynamenode, namenode</span><span class="sxs-lookup"><span data-stu-id="293ba-120">**hdfs** - datanode, secondarynamenode, namenode</span></span>

## <a name="configuration-elements-that-enable-heap-dumps"></a><span data-ttu-id="293ba-121">Elementos de configuración que habilitan los volcados de memoria</span><span class="sxs-lookup"><span data-stu-id="293ba-121">Configuration elements that enable heap dumps</span></span>
<span data-ttu-id="293ba-122">tooturn en los volcados del montón para un servicio, necesita los elementos de configuración adecuada de hello tooset en la sección de Hola para ese servicio, que se especifica mediante **service_name**.</span><span class="sxs-lookup"><span data-stu-id="293ba-122">tooturn on heap dumps for a service, you need tooset hello appropriate configuration elements in hello section for that service, which is specified by **service_name**.</span></span>

    "javaargs.<service_name>.XX:+HeapDumpOnOutOfMemoryError" = "-XX:+HeapDumpOnOutOfMemoryError",
    "javaargs.<service_name>.XX:HeapDumpPath" = "-XX:HeapDumpPath=c:\Dumps\<service_name>_%date:~4,2%%date:~7,2%%date:~10,2%%time:~0,2%%time:~3,2%%time:~6,2%.hprof"

<span data-ttu-id="293ba-123">Hola valo **service_name** puede ser cualquiera de los servicios de hello enumerados aquí: tempelton, hiveserver2, tienda de metadatos, derbyserver, jobhistoryserver, resourcemanager, nodemanager, timelineserver, datanode, secondarynamenode, o namenode.</span><span class="sxs-lookup"><span data-stu-id="293ba-123">hello value of **service_name** can be any of hello services listed here: tempelton, hiveserver2, metastore, derbyserver, jobhistoryserver, resourcemanager, nodemanager, timelineserver, datanode, secondarynamenode, or namenode.</span></span>

## <a name="enable-using-azure-powershell"></a><span data-ttu-id="293ba-124">Habilitar con Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="293ba-124">Enable using Azure PowerShell</span></span>
<span data-ttu-id="293ba-125">Por ejemplo, tooturn en los volcados del montón mediante Azure PowerShell para jobhistoryserver, puede usar Hola siguiente secuencia de comandos:</span><span class="sxs-lookup"><span data-stu-id="293ba-125">For example, tooturn on heap dumps by using Azure PowerShell for jobhistoryserver, you can use hello following script:</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

    $MapRedConfigValues = new-object 'Microsoft.WindowsAzure.Management.HDInsight.Cmdlet.DataObjects.AzureHDInsightMapReduceConfiguration'

    $MapRedConfigValues.Configuration = @{ "javaargs.jobhistoryserver.XX:+HeapDumpOnOutOfMemoryError"="-XX:+HeapDumpOnOutOfMemoryError" ; "javaargs.jobhistoryserver.XX:HeapDumpPath" = "-XX:HeapDumpPath=c:\\Dumps\\jobhistoryserver_%date:~4,2%_%date:~7,2%_%date:~10,2%_%time:~0,2%_%time:~3,2%_%time:~6,2%.hprof" }

## <a name="enable-using-net-sdk"></a><span data-ttu-id="293ba-126">Habilitar con SDK para .NET</span><span class="sxs-lookup"><span data-stu-id="293ba-126">Enable using .NET SDK</span></span>
<span data-ttu-id="293ba-127">Por ejemplo, tooturn en los volcados del montón mediante el uso de hello Azure HDInsight .NET SDK para jobhistoryserver, puede usar Hola siguiente código:</span><span class="sxs-lookup"><span data-stu-id="293ba-127">For example, tooturn on heap dumps by using hello Azure HDInsight .NET SDK for jobhistoryserver, you can use hello following code:</span></span>

    clusterInfo.MapReduceConfiguration.ConfigurationCollection.Add(new KeyValuePair<string, string>("javaargs.jobhistoryserver.XX:+HeapDumpOnOutOfMemoryError", "-XX:+HeapDumpOnOutOfMemoryError"));

    clusterInfo.MapReduceConfiguration.ConfigurationCollection.Add(new KeyValuePair<string, string>("javaargs.jobhistoryserver.XX:HeapDumpPath", "-XX:HeapDumpPath=c:\\Dumps\\jobhistoryserver_%date:~4,2%_%date:~7,2%_%date:~10,2%_%time:~0,2%_%time:~3,2%_%time:~6,2%.hprof"));
