---
title: Depurar y analizar servicios de Hadoop con volcados de memoria - Azure | Microsoft Docs
description: "Recopile automáticamente volcados de memoria para servicios de Hadoop y coloque dentro de la cuenta de almacenamiento de blobs de Azure para depuración y análisis."
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
ms.openlocfilehash: 6d1d4d47d279eb7a1f0bf1f587445683f0ace7a0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="collect-heap-dumps-in-blob-storage-to-debug-and-analyze-hadoop-services"></a><span data-ttu-id="ba3e8-103">Recopilar volcados de memoria en el almacenamiento de blobs para depurar y analizar servicios de Hadoop</span><span class="sxs-lookup"><span data-stu-id="ba3e8-103">Collect heap dumps in Blob storage to debug and analyze Hadoop services</span></span>
[!INCLUDE [heapdump-selector](../../includes/hdinsight-selector-heap-dump.md)]

<span data-ttu-id="ba3e8-104">Los volcados de montón contienen una instantánea de la memoria de la aplicación, incluidos los valores de variables en el momento en el que se creó el volcado de memoria.</span><span class="sxs-lookup"><span data-stu-id="ba3e8-104">Heap dumps contain a snapshot of the application's memory, including the values of variables at the time the dump was created.</span></span> <span data-ttu-id="ba3e8-105">Por ello, estos volcados resultan útiles a la hora de diagnosticar cualquier problema que ocurra en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="ba3e8-105">So they are useful for diagnosing problems that occur at run-time.</span></span> <span data-ttu-id="ba3e8-106">Los volcados de memoria pueden recopilarse automáticamente para servicios Hadoop y se colocan en la cuenta de almacenamiento de blobs de Azure de un usuario en HDInsightHeapDumps/.</span><span class="sxs-lookup"><span data-stu-id="ba3e8-106">Heap dumps can be automatically collected for Hadoop services and placed inside the Azure Blob storage account of a user under HDInsightHeapDumps/.</span></span>

<span data-ttu-id="ba3e8-107">La recopilación de volcados de memoria para los distintos servicios debe habilitarse para los servicios en clústeres individuales.</span><span class="sxs-lookup"><span data-stu-id="ba3e8-107">The collection of heap dumps for various services must be enabled for services on individual clusters.</span></span> <span data-ttu-id="ba3e8-108">De forma predeterminada, esta característica está desactivada para un clúster.</span><span class="sxs-lookup"><span data-stu-id="ba3e8-108">The default for this feature is to be off for a cluster.</span></span> <span data-ttu-id="ba3e8-109">Los volcados de memoria pueden ser de gran tamaño, por lo que se recomienda supervisar la cuenta de almacenamiento de blobs en la que se van a guardar tras habilitar la recopilación.</span><span class="sxs-lookup"><span data-stu-id="ba3e8-109">These heap dumps can be large, so it is advisable to monitor the Blob storage account where they are being saved once the collection has been enabled.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ba3e8-110">Linux es el único sistema operativo que se usa en la versión 3.4 de HDInsight, o en las superiores.</span><span class="sxs-lookup"><span data-stu-id="ba3e8-110">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="ba3e8-111">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="ba3e8-111">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="ba3e8-112">La información de este artículo solo se aplica al HDInsight basado en Windows.</span><span class="sxs-lookup"><span data-stu-id="ba3e8-112">The information in this article only applies to Windows-based HDInsight.</span></span> <span data-ttu-id="ba3e8-113">Para obtener más información sobre el HDInsight basado en Linux, consulte [Habilitar volcados de memoria para servicios de Hadoop en el HDInsight basado en Linux](hdinsight-hadoop-collect-debug-heap-dump-linux.md)</span><span class="sxs-lookup"><span data-stu-id="ba3e8-113">For information on Linux-based HDInsight, see [Enable heap dumps for Hadoop services on Linux-based HDInsight](hdinsight-hadoop-collect-debug-heap-dump-linux.md)</span></span>


## <a name="eligible-services-for-heap-dumps"></a><span data-ttu-id="ba3e8-114">Servicios de volcados de memoria aptos</span><span class="sxs-lookup"><span data-stu-id="ba3e8-114">Eligible services for heap dumps</span></span>
<span data-ttu-id="ba3e8-115">Puede habilitar los volcados de montón en los siguientes servicios:</span><span class="sxs-lookup"><span data-stu-id="ba3e8-115">You can enable heap dumps for the following services:</span></span>

* <span data-ttu-id="ba3e8-116">**hcatalog** - tempelton</span><span class="sxs-lookup"><span data-stu-id="ba3e8-116">**hcatalog** - tempelton</span></span>
* <span data-ttu-id="ba3e8-117">**hive** - hiveserver2, metastore, derbyserver</span><span class="sxs-lookup"><span data-stu-id="ba3e8-117">**hive** - hiveserver2, metastore, derbyserver</span></span>
* <span data-ttu-id="ba3e8-118">**mapreduce** - jobhistoryserver</span><span class="sxs-lookup"><span data-stu-id="ba3e8-118">**mapreduce** - jobhistoryserver</span></span>
* <span data-ttu-id="ba3e8-119">**yarn** - resourcemanager, nodemanager, timelineserver</span><span class="sxs-lookup"><span data-stu-id="ba3e8-119">**yarn** - resourcemanager, nodemanager, timelineserver</span></span>
* <span data-ttu-id="ba3e8-120">**hdfs** - datanode, secondarynamenode, namenode</span><span class="sxs-lookup"><span data-stu-id="ba3e8-120">**hdfs** - datanode, secondarynamenode, namenode</span></span>

## <a name="configuration-elements-that-enable-heap-dumps"></a><span data-ttu-id="ba3e8-121">Elementos de configuración que habilitan los volcados de memoria</span><span class="sxs-lookup"><span data-stu-id="ba3e8-121">Configuration elements that enable heap dumps</span></span>
<span data-ttu-id="ba3e8-122">Para activar el volcado de memoria para un servicio, el usuario deberá definir los elementos de configuración adecuados en la sección de dicho servicio, que se especifica mediante **nombre_servicio**.</span><span class="sxs-lookup"><span data-stu-id="ba3e8-122">To turn on heap dumps for a service, you need to set the appropriate configuration elements in the section for that service, which is specified by **service_name**.</span></span>

    "javaargs.<service_name>.XX:+HeapDumpOnOutOfMemoryError" = "-XX:+HeapDumpOnOutOfMemoryError",
    "javaargs.<service_name>.XX:HeapDumpPath" = "-XX:HeapDumpPath=c:\Dumps\<service_name>_%date:~4,2%%date:~7,2%%date:~10,2%%time:~0,2%%time:~3,2%%time:~6,2%.hprof"

<span data-ttu-id="ba3e8-123">El valor de **nombre_servicio** puede ser cualquiera de los servicios enumerados aquí: tempelton, hiveserver2, metastore, derbyserver, jobhistoryserver, resourcemanager, nodemanager, timelineserver, datanode, secondarynamenode o namenode.</span><span class="sxs-lookup"><span data-stu-id="ba3e8-123">The value of **service_name** can be any of the services listed here: tempelton, hiveserver2, metastore, derbyserver, jobhistoryserver, resourcemanager, nodemanager, timelineserver, datanode, secondarynamenode, or namenode.</span></span>

## <a name="enable-using-azure-powershell"></a><span data-ttu-id="ba3e8-124">Habilitar con Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="ba3e8-124">Enable using Azure PowerShell</span></span>
<span data-ttu-id="ba3e8-125">Por ejemplo, para activar los volcados de memoria mediante Azure PowerShell para jobhistoryserver, puede usar el siguiente script:</span><span class="sxs-lookup"><span data-stu-id="ba3e8-125">For example, to turn on heap dumps by using Azure PowerShell for jobhistoryserver, you can use the following script:</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

    $MapRedConfigValues = new-object 'Microsoft.WindowsAzure.Management.HDInsight.Cmdlet.DataObjects.AzureHDInsightMapReduceConfiguration'

    $MapRedConfigValues.Configuration = @{ "javaargs.jobhistoryserver.XX:+HeapDumpOnOutOfMemoryError"="-XX:+HeapDumpOnOutOfMemoryError" ; "javaargs.jobhistoryserver.XX:HeapDumpPath" = "-XX:HeapDumpPath=c:\\Dumps\\jobhistoryserver_%date:~4,2%_%date:~7,2%_%date:~10,2%_%time:~0,2%_%time:~3,2%_%time:~6,2%.hprof" }

## <a name="enable-using-net-sdk"></a><span data-ttu-id="ba3e8-126">Habilitar con SDK para .NET</span><span class="sxs-lookup"><span data-stu-id="ba3e8-126">Enable using .NET SDK</span></span>
<span data-ttu-id="ba3e8-127">Por ejemplo, para activar los volcados de memoria mediante el SDK de .NET de Azure HDInsight para jobhistoryserver, puede usar el siguiente código:</span><span class="sxs-lookup"><span data-stu-id="ba3e8-127">For example, to turn on heap dumps by using the Azure HDInsight .NET SDK for jobhistoryserver, you can use the following code:</span></span>

    clusterInfo.MapReduceConfiguration.ConfigurationCollection.Add(new KeyValuePair<string, string>("javaargs.jobhistoryserver.XX:+HeapDumpOnOutOfMemoryError", "-XX:+HeapDumpOnOutOfMemoryError"));

    clusterInfo.MapReduceConfiguration.ConfigurationCollection.Add(new KeyValuePair<string, string>("javaargs.jobhistoryserver.XX:HeapDumpPath", "-XX:HeapDumpPath=c:\\Dumps\\jobhistoryserver_%date:~4,2%_%date:~7,2%_%date:~10,2%_%time:~0,2%_%time:~3,2%_%time:~6,2%.hprof"));
