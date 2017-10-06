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
# <a name="use-pig-with-hadoop-on-hdinsight"></a><span data-ttu-id="cbdb1-103">Uso de Pig con Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="cbdb1-103">Use Pig with Hadoop on HDInsight</span></span>

<span data-ttu-id="cbdb1-104">Obtenga información acerca de cómo toouse [Apache Pig](http://pig.apache.org/) con HDInsight...</span><span class="sxs-lookup"><span data-stu-id="cbdb1-104">Learn how toouse [Apache Pig](http://pig.apache.org/) with HDInsight...</span></span>

<span data-ttu-id="cbdb1-105">Pig es una plataforma para crear programas de Hadoop mediante un lenguaje de procedimientos que se conoce como *Pig Latin*.</span><span class="sxs-lookup"><span data-stu-id="cbdb1-105">Pig is a platform for creating programs for Hadoop by using a procedural language known as *Pig Latin*.</span></span> <span data-ttu-id="cbdb1-106">Pig es una alternativa tooJava para crear *MapReduce* soluciones y se incluye con HDInsight de Azure.</span><span class="sxs-lookup"><span data-stu-id="cbdb1-106">Pig is an alternative tooJava for creating *MapReduce* solutions, and it is included with Azure HDInsight.</span></span> <span data-ttu-id="cbdb1-107">Usar hello después hello toodiscover de tabla que Pig puede utilizarse con HDInsight de varias maneras:</span><span class="sxs-lookup"><span data-stu-id="cbdb1-107">Use hello following table toodiscover hello various ways that Pig can be used with HDInsight:</span></span>

| <span data-ttu-id="cbdb1-108">**Utilícelo** si desea...</span><span class="sxs-lookup"><span data-stu-id="cbdb1-108">**Use this** if you want...</span></span> | <span data-ttu-id="cbdb1-109">...un shell **interactivo**</span><span class="sxs-lookup"><span data-stu-id="cbdb1-109">...an **interactive** shell</span></span> | <span data-ttu-id="cbdb1-110">...procesamiento por**lotes**</span><span class="sxs-lookup"><span data-stu-id="cbdb1-110">...**batch** processing</span></span> | <span data-ttu-id="cbdb1-111">...con este **sistema operativo de clúster**</span><span class="sxs-lookup"><span data-stu-id="cbdb1-111">...with this **cluster operating system**</span></span> | <span data-ttu-id="cbdb1-112">...desde este **sistema operativo de cliente**</span><span class="sxs-lookup"><span data-stu-id="cbdb1-112">...from this **client operating system**</span></span> |
|:--- |:---:|:---:|:--- |:--- |
| [<span data-ttu-id="cbdb1-113">SSH</span><span class="sxs-lookup"><span data-stu-id="cbdb1-113">SSH</span></span>](hdinsight-hadoop-use-pig-ssh.md) |<span data-ttu-id="cbdb1-114">✔</span><span class="sxs-lookup"><span data-stu-id="cbdb1-114">✔</span></span> |<span data-ttu-id="cbdb1-115">✔</span><span class="sxs-lookup"><span data-stu-id="cbdb1-115">✔</span></span> |<span data-ttu-id="cbdb1-116">Linux</span><span class="sxs-lookup"><span data-stu-id="cbdb1-116">Linux</span></span> |<span data-ttu-id="cbdb1-117">Linux, Unix, Mac OS X o Windows</span><span class="sxs-lookup"><span data-stu-id="cbdb1-117">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="cbdb1-118">API DE REST</span><span class="sxs-lookup"><span data-stu-id="cbdb1-118">REST API</span></span>](hdinsight-hadoop-use-pig-curl.md) |&nbsp; |<span data-ttu-id="cbdb1-119">✔</span><span class="sxs-lookup"><span data-stu-id="cbdb1-119">✔</span></span> |<span data-ttu-id="cbdb1-120">Linux o Windows</span><span class="sxs-lookup"><span data-stu-id="cbdb1-120">Linux or Windows</span></span> |<span data-ttu-id="cbdb1-121">Linux, Unix, Mac OS X o Windows</span><span class="sxs-lookup"><span data-stu-id="cbdb1-121">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="cbdb1-122">.NET SDK para Hadoop</span><span class="sxs-lookup"><span data-stu-id="cbdb1-122">.NET SDK for Hadoop</span></span>](hdinsight-hadoop-use-pig-dotnet-sdk.md) |&nbsp; |<span data-ttu-id="cbdb1-123">✔</span><span class="sxs-lookup"><span data-stu-id="cbdb1-123">✔</span></span> |<span data-ttu-id="cbdb1-124">Linux o Windows</span><span class="sxs-lookup"><span data-stu-id="cbdb1-124">Linux or Windows</span></span> |<span data-ttu-id="cbdb1-125">Windows (por ahora)</span><span class="sxs-lookup"><span data-stu-id="cbdb1-125">Windows (for now)</span></span> |
| [<span data-ttu-id="cbdb1-126">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="cbdb1-126">Windows PowerShell</span></span>](hdinsight-hadoop-use-pig-powershell.md) |&nbsp; |<span data-ttu-id="cbdb1-127">✔</span><span class="sxs-lookup"><span data-stu-id="cbdb1-127">✔</span></span> |<span data-ttu-id="cbdb1-128">Linux o Windows</span><span class="sxs-lookup"><span data-stu-id="cbdb1-128">Linux or Windows</span></span> |<span data-ttu-id="cbdb1-129">Windows</span><span class="sxs-lookup"><span data-stu-id="cbdb1-129">Windows</span></span> |
| <span data-ttu-id="cbdb1-130">[Escritorio remoto](hdinsight-hadoop-use-pig-remote-desktop.md) (HDInsight 3.2 y 3.3)</span><span class="sxs-lookup"><span data-stu-id="cbdb1-130">[Remote Desktop](hdinsight-hadoop-use-pig-remote-desktop.md) (HDInsight 3.2 and 3.3)</span></span> |<span data-ttu-id="cbdb1-131">✔</span><span class="sxs-lookup"><span data-stu-id="cbdb1-131">✔</span></span> |<span data-ttu-id="cbdb1-132">✔</span><span class="sxs-lookup"><span data-stu-id="cbdb1-132">✔</span></span> |<span data-ttu-id="cbdb1-133">Windows</span><span class="sxs-lookup"><span data-stu-id="cbdb1-133">Windows</span></span> |<span data-ttu-id="cbdb1-134">Windows</span><span class="sxs-lookup"><span data-stu-id="cbdb1-134">Windows</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="cbdb1-135">Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior.</span><span class="sxs-lookup"><span data-stu-id="cbdb1-135">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="cbdb1-136">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="cbdb1-136">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="cbdb1-137"><a id="why"></a>¿Por qué usar Pig?</span><span class="sxs-lookup"><span data-stu-id="cbdb1-137"><a id="why"></a>Why use Pig</span></span>

<span data-ttu-id="cbdb1-138">Uno de los desafíos de Hola de procesamiento de datos mediante el uso de MapReduce en Hadoop consiste en implementar la lógica de procesamiento con solo una asignación y una función de reducción.</span><span class="sxs-lookup"><span data-stu-id="cbdb1-138">One of hello challenges of processing data by using MapReduce in Hadoop is implementing your processing logic by using only a map and a reduce function.</span></span> <span data-ttu-id="cbdb1-139">Para el procesamiento complejo, que a menudo tienen toobreak procesamiento en varias operaciones de MapReduce que son encadenar juntos tooachieve resultado de hello deseado.</span><span class="sxs-lookup"><span data-stu-id="cbdb1-139">For complex processing, you often have toobreak processing into multiple MapReduce operations that are chained together tooachieve hello desired result.</span></span>

<span data-ttu-id="cbdb1-140">Pig permite toodefine procesar como una serie de transformaciones que Hola datos fluyen a través de la salida de hello deseado tooproduce.</span><span class="sxs-lookup"><span data-stu-id="cbdb1-140">Pig allows you toodefine processing as a series of transformations that hello data flows through tooproduce hello desired output.</span></span>

<span data-ttu-id="cbdb1-141">lenguaje de Pig latino de Hello permite toodescribe Hola flujo de datos de entrada sin formato, a través de una o varias transformaciones, tooproduce salida de hello deseado.</span><span class="sxs-lookup"><span data-stu-id="cbdb1-141">hello Pig Latin language allows you toodescribe hello data flow from raw input, through one or more transformations, tooproduce hello desired output.</span></span> <span data-ttu-id="cbdb1-142">Los programas de Pig Latin siguen este patrón general:</span><span class="sxs-lookup"><span data-stu-id="cbdb1-142">Pig Latin programs follow this general pattern:</span></span>

* <span data-ttu-id="cbdb1-143">**Carga**: leer toobe datos manipulado Hola sistema de archivos</span><span class="sxs-lookup"><span data-stu-id="cbdb1-143">**Load**: Read data toobe manipulated from hello file system</span></span>

* <span data-ttu-id="cbdb1-144">**Transformar**: manipular datos Hola</span><span class="sxs-lookup"><span data-stu-id="cbdb1-144">**Transform**: Manipulate hello data</span></span>

* <span data-ttu-id="cbdb1-145">**Vuelque ni almacenar**: pantalla de toohello de datos de salida o en el almacén para el procesamiento</span><span class="sxs-lookup"><span data-stu-id="cbdb1-145">**Dump or store**: Output data toohello screen or store it for processing</span></span>

### <a name="user-defined-functions"></a><span data-ttu-id="cbdb1-146">Funciones definidas por el usuario</span><span class="sxs-lookup"><span data-stu-id="cbdb1-146">User-defined functions</span></span>

<span data-ttu-id="cbdb1-147">Pig latino también admite funciones definidas por el usuario (UDF), lo que permite tooinvoke componentes externos que implementan la lógica que es difícil toomodel en Pig latino.</span><span class="sxs-lookup"><span data-stu-id="cbdb1-147">Pig Latin also supports user-defined functions (UDF), which allows you tooinvoke external components that implement logic that is difficult toomodel in Pig Latin.</span></span>

<span data-ttu-id="cbdb1-148">Para más información sobre Pig Latin, consulte el [manual de referencia de Pig Latin 1](http://pig.apache.org/docs/r0.7.0/piglatin_ref1.html) y el [manual de referencia de Pig Latin 2](http://pig.apache.org/docs/r0.7.0/piglatin_ref2.html).</span><span class="sxs-lookup"><span data-stu-id="cbdb1-148">For more information about Pig Latin, see [Pig Latin Reference Manual 1](http://pig.apache.org/docs/r0.7.0/piglatin_ref1.html) and [Pig Latin Reference Manual 2](http://pig.apache.org/docs/r0.7.0/piglatin_ref2.html).</span></span>

<span data-ttu-id="cbdb1-149">Para obtener un ejemplo del uso de UDF con Pig, consulte Hola siguientes documentos:</span><span class="sxs-lookup"><span data-stu-id="cbdb1-149">For an example of using UDFs with Pig, see hello following documents:</span></span>

* <span data-ttu-id="cbdb1-150">[Utilice DataFu con Pig en HDInsight](hdinsight-hadoop-use-pig-datafu-udf.md) - DataFu es una colección de UDF útiles mantenida por Apache</span><span class="sxs-lookup"><span data-stu-id="cbdb1-150">[Use DataFu with Pig in HDInsight](hdinsight-hadoop-use-pig-datafu-udf.md) - DataFu is a collection of useful UDFs maintained by Apache</span></span>
* [<span data-ttu-id="cbdb1-151">Uso de Python con Pig y Hive en HDInsight</span><span class="sxs-lookup"><span data-stu-id="cbdb1-151">Use Python with Pig and Hive in HDInsight</span></span>](hdinsight-python.md)
* [<span data-ttu-id="cbdb1-152">Uso de C# con Hive y Pig en HDInsight</span><span class="sxs-lookup"><span data-stu-id="cbdb1-152">Use C# with Hive and Pig in HDInsight</span></span>](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)

## <span data-ttu-id="cbdb1-153"><a id="data"></a>Datos de ejemplo</span><span class="sxs-lookup"><span data-stu-id="cbdb1-153"><a id="data"></a>Example data</span></span>

<span data-ttu-id="cbdb1-154">HDInsight proporciona diversos conjuntos de datos de ejemplo, que se almacenan en hello `/example/data` y `/HdiSamples` directorios.</span><span class="sxs-lookup"><span data-stu-id="cbdb1-154">HDInsight provides various example data sets, which are stored in hello `/example/data` and `/HdiSamples` directories.</span></span> <span data-ttu-id="cbdb1-155">Son estos directorios en almacenamiento predeterminado de hello para el clúster.</span><span class="sxs-lookup"><span data-stu-id="cbdb1-155">These directories are in hello default storage for your cluster.</span></span> <span data-ttu-id="cbdb1-156">ejemplo de Hola Pig en este documento usa hello *log4j* de archivos de `/example/data/sample.log`.</span><span class="sxs-lookup"><span data-stu-id="cbdb1-156">hello Pig example in this document uses hello *log4j* file from `/example/data/sample.log`.</span></span>

<span data-ttu-id="cbdb1-157">Cada registro en el archivo hello consta de una línea de campos que contenga un `[LOG LEVEL]` campo gravedad de hello y tipo de hello tooshow, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="cbdb1-157">Each log inside hello file consists of a line of fields that contains a `[LOG LEVEL]` field tooshow hello type and hello severity, for example:</span></span>

    2012-02-03 20:26:41 SampleClass3 [ERROR] verbose detail for id 1527353937

<span data-ttu-id="cbdb1-158">En el ejemplo anterior de hello, nivel de registro de hello es ERROR.</span><span class="sxs-lookup"><span data-stu-id="cbdb1-158">In hello previous example, hello log level is ERROR.</span></span>

> [!NOTE]
> <span data-ttu-id="cbdb1-159">También puede generar un archivo de log4j mediante hello [Apache Log4j](http://en.wikipedia.org/wiki/Log4j) herramienta de registro y, a continuación, cargar ese blob tooyour de archivo.</span><span class="sxs-lookup"><span data-stu-id="cbdb1-159">You can also generate a log4j file by using hello [Apache Log4j](http://en.wikipedia.org/wiki/Log4j) logging tool and then upload that file tooyour blob.</span></span> <span data-ttu-id="cbdb1-160">Vea [tooHDInsight de cargar datos](hdinsight-upload-data.md) para obtener instrucciones.</span><span class="sxs-lookup"><span data-stu-id="cbdb1-160">See [Upload Data tooHDInsight](hdinsight-upload-data.md) for instructions.</span></span> <span data-ttu-id="cbdb1-161">Para obtener más información sobre el uso de los blobs en Azure Storage con HDInsight, consulte [Uso de Azure Blob Storage con HDInsight](hdinsight-hadoop-use-blob-storage.md).</span><span class="sxs-lookup"><span data-stu-id="cbdb1-161">For more information about how blobs in Azure storage are used with HDInsight, see [Use Azure Blob Storage with HDInsight](hdinsight-hadoop-use-blob-storage.md).</span></span>

## <span data-ttu-id="cbdb1-162"><a id="job"></a>Trabajo de ejemplo</span><span class="sxs-lookup"><span data-stu-id="cbdb1-162"><a id="job"></a>Example job</span></span>

<span data-ttu-id="cbdb1-163">siguiente trabajo de Pig latino Hello carga hello `sample.log` archivo de almacenamiento predeterminado de hello para el clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cbdb1-163">hello following Pig Latin job loads hello `sample.log` file from hello default storage for your HDInsight cluster.</span></span> <span data-ttu-id="cbdb1-164">A continuación, realiza una serie de transformaciones que se produce un recuento de cómo muchas veces cada datos de entrada de hello en nivel de registro.</span><span class="sxs-lookup"><span data-stu-id="cbdb1-164">Then it performs a series of transformations that result in a count of how many times each log level occurred in hello input data.</span></span> <span data-ttu-id="cbdb1-165">resultados de Hola se escriben tooSTDOUT.</span><span class="sxs-lookup"><span data-stu-id="cbdb1-165">hello results are written tooSTDOUT.</span></span>

    LOGS = LOAD 'wasb:///example/data/sample.log';
    LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
    FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
    GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
    FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
    RESULT = order FREQUENCIES by COUNT desc;
    DUMP RESULT;

<span data-ttu-id="cbdb1-166">Hello siguiente imagen muestra un resumen de las transformaciones de qué hace toohello datos.</span><span class="sxs-lookup"><span data-stu-id="cbdb1-166">hello following image shows a summary of what each transformation does toohello data.</span></span>

![Representación gráfica de las transformaciones de Hola][image-hdi-pig-data-transformation]

## <span data-ttu-id="cbdb1-168"><a id="run"></a>Ejecutar trabajo de Pig latino Hola</span><span class="sxs-lookup"><span data-stu-id="cbdb1-168"><a id="run"></a>Run hello Pig Latin job</span></span>

<span data-ttu-id="cbdb1-169">HDInsight puede ejecutar trabajos de Pig Latin mediante una variedad de métodos.</span><span class="sxs-lookup"><span data-stu-id="cbdb1-169">HDInsight can run Pig Latin jobs by using a variety of methods.</span></span> <span data-ttu-id="cbdb1-170">Usar hello después toodecide tabla qué método es adecuado para usted, a continuación, siga el vínculo de Hola para ver un tutorial.</span><span class="sxs-lookup"><span data-stu-id="cbdb1-170">Use hello following table toodecide which method is right for you, then follow hello link for a walkthrough.</span></span>

| <span data-ttu-id="cbdb1-171">**Utilícelo** si desea...</span><span class="sxs-lookup"><span data-stu-id="cbdb1-171">**Use this** if you want...</span></span> | <span data-ttu-id="cbdb1-172">...un shell **interactivo**</span><span class="sxs-lookup"><span data-stu-id="cbdb1-172">...an **interactive** shell</span></span> | <span data-ttu-id="cbdb1-173">...procesamiento por**lotes**</span><span class="sxs-lookup"><span data-stu-id="cbdb1-173">...**batch** processing</span></span> | <span data-ttu-id="cbdb1-174">...con este **sistema operativo de clúster**</span><span class="sxs-lookup"><span data-stu-id="cbdb1-174">...with this **cluster operating system**</span></span> | <span data-ttu-id="cbdb1-175">...de este **cliente**</span><span class="sxs-lookup"><span data-stu-id="cbdb1-175">...from this **client**</span></span> |
|:--- |:---:|:---:|:--- |:--- |
| [<span data-ttu-id="cbdb1-176">SSH</span><span class="sxs-lookup"><span data-stu-id="cbdb1-176">SSH</span></span>](hdinsight-hadoop-use-pig-ssh.md) |<span data-ttu-id="cbdb1-177">✔</span><span class="sxs-lookup"><span data-stu-id="cbdb1-177">✔</span></span> |<span data-ttu-id="cbdb1-178">✔</span><span class="sxs-lookup"><span data-stu-id="cbdb1-178">✔</span></span> |<span data-ttu-id="cbdb1-179">Linux</span><span class="sxs-lookup"><span data-stu-id="cbdb1-179">Linux</span></span> |<span data-ttu-id="cbdb1-180">Linux, Unix, Mac OS X o Windows</span><span class="sxs-lookup"><span data-stu-id="cbdb1-180">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="cbdb1-181">Curl</span><span class="sxs-lookup"><span data-stu-id="cbdb1-181">Curl</span></span>](hdinsight-hadoop-use-pig-curl.md) |&nbsp; |<span data-ttu-id="cbdb1-182">✔</span><span class="sxs-lookup"><span data-stu-id="cbdb1-182">✔</span></span> |<span data-ttu-id="cbdb1-183">Linux o Windows</span><span class="sxs-lookup"><span data-stu-id="cbdb1-183">Linux or Windows</span></span> |<span data-ttu-id="cbdb1-184">Linux, Unix, Mac OS X o Windows</span><span class="sxs-lookup"><span data-stu-id="cbdb1-184">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="cbdb1-185">.NET SDK para Hadoop</span><span class="sxs-lookup"><span data-stu-id="cbdb1-185">.NET SDK for Hadoop</span></span>](hdinsight-hadoop-use-pig-dotnet-sdk.md) |&nbsp; |<span data-ttu-id="cbdb1-186">✔</span><span class="sxs-lookup"><span data-stu-id="cbdb1-186">✔</span></span> |<span data-ttu-id="cbdb1-187">Linux o Windows</span><span class="sxs-lookup"><span data-stu-id="cbdb1-187">Linux or Windows</span></span> |<span data-ttu-id="cbdb1-188">Windows (por ahora)</span><span class="sxs-lookup"><span data-stu-id="cbdb1-188">Windows (for now)</span></span> |
| [<span data-ttu-id="cbdb1-189">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="cbdb1-189">Windows PowerShell</span></span>](hdinsight-hadoop-use-pig-powershell.md) |&nbsp; |<span data-ttu-id="cbdb1-190">✔</span><span class="sxs-lookup"><span data-stu-id="cbdb1-190">✔</span></span> |<span data-ttu-id="cbdb1-191">Linux o Windows</span><span class="sxs-lookup"><span data-stu-id="cbdb1-191">Linux or Windows</span></span> |<span data-ttu-id="cbdb1-192">Windows</span><span class="sxs-lookup"><span data-stu-id="cbdb1-192">Windows</span></span> |
| <span data-ttu-id="cbdb1-193">[Escritorio remoto](hdinsight-hadoop-use-pig-remote-desktop.md) (HDInsight 3.2 y 3.3)</span><span class="sxs-lookup"><span data-stu-id="cbdb1-193">[Remote Desktop](hdinsight-hadoop-use-pig-remote-desktop.md) (HDInsight 3.2 and 3.3)</span></span> |<span data-ttu-id="cbdb1-194">✔</span><span class="sxs-lookup"><span data-stu-id="cbdb1-194">✔</span></span> |<span data-ttu-id="cbdb1-195">✔</span><span class="sxs-lookup"><span data-stu-id="cbdb1-195">✔</span></span> |<span data-ttu-id="cbdb1-196">Windows</span><span class="sxs-lookup"><span data-stu-id="cbdb1-196">Windows</span></span> |<span data-ttu-id="cbdb1-197">Windows</span><span class="sxs-lookup"><span data-stu-id="cbdb1-197">Windows</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="cbdb1-198">Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior.</span><span class="sxs-lookup"><span data-stu-id="cbdb1-198">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="cbdb1-199">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="cbdb1-199">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="pig-and-sql-server-integration-services"></a><span data-ttu-id="cbdb1-200">Pig y SQL Server Integration Services</span><span class="sxs-lookup"><span data-stu-id="cbdb1-200">Pig and SQL Server Integration Services</span></span>

<span data-ttu-id="cbdb1-201">Puede utilizar SQL Server Integration Services (SSIS) toorun un trabajo de Pig.</span><span class="sxs-lookup"><span data-stu-id="cbdb1-201">You can use SQL Server Integration Services (SSIS) toorun a Pig job.</span></span> <span data-ttu-id="cbdb1-202">Hola Feature Pack de Azure para SSIS proporciona Hola trabajan con trabajos de Pig en HDInsight de los componentes siguientes.</span><span class="sxs-lookup"><span data-stu-id="cbdb1-202">hello Azure Feature Pack for SSIS provides hello following components that work with Pig jobs on HDInsight.</span></span>

* <span data-ttu-id="cbdb1-203">[Tarea de Pig de Azure HDInsight][pigtask]</span><span class="sxs-lookup"><span data-stu-id="cbdb1-203">[Azure HDInsight Pig Task][pigtask]</span></span>

* <span data-ttu-id="cbdb1-204">[Administrador de conexiones de suscripción de Azure][connectionmanager]</span><span class="sxs-lookup"><span data-stu-id="cbdb1-204">[Azure Subscription Connection Manager][connectionmanager]</span></span>

<span data-ttu-id="cbdb1-205">Obtener más información sobre Hola Feature Pack de Azure para SSIS [aquí][ssispack].</span><span class="sxs-lookup"><span data-stu-id="cbdb1-205">Learn more about hello Azure Feature Pack for SSIS [here][ssispack].</span></span>

## <span data-ttu-id="cbdb1-206"><a id="nextsteps"></a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="cbdb1-206"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="cbdb1-207">Ahora que ha aprendido cómo toouse Pig con HDInsight, Hola de uso siguiente vincula tooexplore otro toowork maneras con HDInsight de Azure.</span><span class="sxs-lookup"><span data-stu-id="cbdb1-207">Now that you have learned how toouse Pig with HDInsight, use hello following links tooexplore other ways toowork with Azure HDInsight.</span></span>

* <span data-ttu-id="cbdb1-208">[Cargar datos tooHDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="cbdb1-208">[Upload data tooHDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="cbdb1-209">[Uso de Hive con HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="cbdb1-209">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* [<span data-ttu-id="cbdb1-210">Uso de Sqoop con HDInsight</span><span class="sxs-lookup"><span data-stu-id="cbdb1-210">Use Sqoop with HDInsight</span></span>](hdinsight-use-sqoop.md)
* [<span data-ttu-id="cbdb1-211">Uso de Oozie con HDInsight</span><span class="sxs-lookup"><span data-stu-id="cbdb1-211">Use Oozie with HDInsight</span></span>](hdinsight-use-oozie.md)
* <span data-ttu-id="cbdb1-212">[Uso de trabajos de MapReduce con HDInsight][hdinsight-use-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="cbdb1-212">[Use MapReduce jobs with HDInsight][hdinsight-use-mapreduce]</span></span>

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
