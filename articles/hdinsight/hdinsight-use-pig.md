---
title: Uso de Pig de Hadoop en HDInsight | Microsoft Docs
description: Aprenda a usar Pig con Hadoop en HDInsight.
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
ms.openlocfilehash: 474f901ffdaf1ed372ace19076ef723b8b10cb9a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="use-pig-with-hadoop-on-hdinsight"></a><span data-ttu-id="bfb1f-103">Uso de Pig con Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="bfb1f-103">Use Pig with Hadoop on HDInsight</span></span>

<span data-ttu-id="bfb1f-104">Aprenda a usar [Apache Pig](http://pig.apache.org/) con HDInsight...</span><span class="sxs-lookup"><span data-stu-id="bfb1f-104">Learn how to use [Apache Pig](http://pig.apache.org/) with HDInsight...</span></span>

<span data-ttu-id="bfb1f-105">Pig es una plataforma para crear programas de Hadoop mediante un lenguaje de procedimientos que se conoce como *Pig Latin*.</span><span class="sxs-lookup"><span data-stu-id="bfb1f-105">Pig is a platform for creating programs for Hadoop by using a procedural language known as *Pig Latin*.</span></span> <span data-ttu-id="bfb1f-106">Pig es una alternativa a Java para crear soluciones *MapReduce* y se incluye con HDInsight de Azure.</span><span class="sxs-lookup"><span data-stu-id="bfb1f-106">Pig is an alternative to Java for creating *MapReduce* solutions, and it is included with Azure HDInsight.</span></span> <span data-ttu-id="bfb1f-107">Utilice la tabla siguiente para conocer las distintas formas de usar Pig con HDInsight:</span><span class="sxs-lookup"><span data-stu-id="bfb1f-107">Use the following table to discover the various ways that Pig can be used with HDInsight:</span></span>

| <span data-ttu-id="bfb1f-108">**Utilícelo** si desea...</span><span class="sxs-lookup"><span data-stu-id="bfb1f-108">**Use this** if you want...</span></span> | <span data-ttu-id="bfb1f-109">...un shell **interactivo**</span><span class="sxs-lookup"><span data-stu-id="bfb1f-109">...an **interactive** shell</span></span> | <span data-ttu-id="bfb1f-110">...procesamiento por**lotes**</span><span class="sxs-lookup"><span data-stu-id="bfb1f-110">...**batch** processing</span></span> | <span data-ttu-id="bfb1f-111">...con este **sistema operativo de clúster**</span><span class="sxs-lookup"><span data-stu-id="bfb1f-111">...with this **cluster operating system**</span></span> | <span data-ttu-id="bfb1f-112">...desde este **sistema operativo de cliente**</span><span class="sxs-lookup"><span data-stu-id="bfb1f-112">...from this **client operating system**</span></span> |
|:--- |:---:|:---:|:--- |:--- |
| [<span data-ttu-id="bfb1f-113">SSH</span><span class="sxs-lookup"><span data-stu-id="bfb1f-113">SSH</span></span>](hdinsight-hadoop-use-pig-ssh.md) |<span data-ttu-id="bfb1f-114">✔</span><span class="sxs-lookup"><span data-stu-id="bfb1f-114">✔</span></span> |<span data-ttu-id="bfb1f-115">✔</span><span class="sxs-lookup"><span data-stu-id="bfb1f-115">✔</span></span> |<span data-ttu-id="bfb1f-116">Linux</span><span class="sxs-lookup"><span data-stu-id="bfb1f-116">Linux</span></span> |<span data-ttu-id="bfb1f-117">Linux, Unix, Mac OS X o Windows</span><span class="sxs-lookup"><span data-stu-id="bfb1f-117">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="bfb1f-118">API DE REST</span><span class="sxs-lookup"><span data-stu-id="bfb1f-118">REST API</span></span>](hdinsight-hadoop-use-pig-curl.md) |&nbsp; |<span data-ttu-id="bfb1f-119">✔</span><span class="sxs-lookup"><span data-stu-id="bfb1f-119">✔</span></span> |<span data-ttu-id="bfb1f-120">Linux o Windows</span><span class="sxs-lookup"><span data-stu-id="bfb1f-120">Linux or Windows</span></span> |<span data-ttu-id="bfb1f-121">Linux, Unix, Mac OS X o Windows</span><span class="sxs-lookup"><span data-stu-id="bfb1f-121">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="bfb1f-122">.NET SDK para Hadoop</span><span class="sxs-lookup"><span data-stu-id="bfb1f-122">.NET SDK for Hadoop</span></span>](hdinsight-hadoop-use-pig-dotnet-sdk.md) |&nbsp; |<span data-ttu-id="bfb1f-123">✔</span><span class="sxs-lookup"><span data-stu-id="bfb1f-123">✔</span></span> |<span data-ttu-id="bfb1f-124">Linux o Windows</span><span class="sxs-lookup"><span data-stu-id="bfb1f-124">Linux or Windows</span></span> |<span data-ttu-id="bfb1f-125">Windows (por ahora)</span><span class="sxs-lookup"><span data-stu-id="bfb1f-125">Windows (for now)</span></span> |
| [<span data-ttu-id="bfb1f-126">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="bfb1f-126">Windows PowerShell</span></span>](hdinsight-hadoop-use-pig-powershell.md) |&nbsp; |<span data-ttu-id="bfb1f-127">✔</span><span class="sxs-lookup"><span data-stu-id="bfb1f-127">✔</span></span> |<span data-ttu-id="bfb1f-128">Linux o Windows</span><span class="sxs-lookup"><span data-stu-id="bfb1f-128">Linux or Windows</span></span> |<span data-ttu-id="bfb1f-129">Windows</span><span class="sxs-lookup"><span data-stu-id="bfb1f-129">Windows</span></span> |
| <span data-ttu-id="bfb1f-130">[Escritorio remoto](hdinsight-hadoop-use-pig-remote-desktop.md) (HDInsight 3.2 y 3.3)</span><span class="sxs-lookup"><span data-stu-id="bfb1f-130">[Remote Desktop](hdinsight-hadoop-use-pig-remote-desktop.md) (HDInsight 3.2 and 3.3)</span></span> |<span data-ttu-id="bfb1f-131">✔</span><span class="sxs-lookup"><span data-stu-id="bfb1f-131">✔</span></span> |<span data-ttu-id="bfb1f-132">✔</span><span class="sxs-lookup"><span data-stu-id="bfb1f-132">✔</span></span> |<span data-ttu-id="bfb1f-133">Windows</span><span class="sxs-lookup"><span data-stu-id="bfb1f-133">Windows</span></span> |<span data-ttu-id="bfb1f-134">Windows</span><span class="sxs-lookup"><span data-stu-id="bfb1f-134">Windows</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="bfb1f-135">Linux es el único sistema operativo que se usa en la versión 3.4 de HDInsight, o en las superiores.</span><span class="sxs-lookup"><span data-stu-id="bfb1f-135">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="bfb1f-136">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="bfb1f-136">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="bfb1f-137"><a id="why"></a>¿Por qué usar Pig?</span><span class="sxs-lookup"><span data-stu-id="bfb1f-137"><a id="why"></a>Why use Pig</span></span>

<span data-ttu-id="bfb1f-138">Uno de los desafíos del procesamiento de datos mediante el uso de MapReduce en Hadoop es la implementación de la lógica de procesamiento únicamente con un mapa y una función de reducción.</span><span class="sxs-lookup"><span data-stu-id="bfb1f-138">One of the challenges of processing data by using MapReduce in Hadoop is implementing your processing logic by using only a map and a reduce function.</span></span> <span data-ttu-id="bfb1f-139">Para el procesamiento complejo, a menudo debe interrumpir el procesamiento en varias operaciones de MapReduce que están encadenadas para lograr el resultado deseado.</span><span class="sxs-lookup"><span data-stu-id="bfb1f-139">For complex processing, you often have to break processing into multiple MapReduce operations that are chained together to achieve the desired result.</span></span>

<span data-ttu-id="bfb1f-140">Pig permite definir los procesos como una serie de transformaciones por la que fluyen los datos para producir el resultado deseado.</span><span class="sxs-lookup"><span data-stu-id="bfb1f-140">Pig allows you to define processing as a series of transformations that the data flows through to produce the desired output.</span></span>

<span data-ttu-id="bfb1f-141">El lenguaje de Pig Latin le permite describir el flujo de datos desde entrada sin formato, a través de una o varias transformaciones, para producir el resultado deseado.</span><span class="sxs-lookup"><span data-stu-id="bfb1f-141">The Pig Latin language allows you to describe the data flow from raw input, through one or more transformations, to produce the desired output.</span></span> <span data-ttu-id="bfb1f-142">Los programas de Pig Latin siguen este patrón general:</span><span class="sxs-lookup"><span data-stu-id="bfb1f-142">Pig Latin programs follow this general pattern:</span></span>

* <span data-ttu-id="bfb1f-143">**Carga**: Los datos leídos que se van a manipular desde el sistema de archivos.</span><span class="sxs-lookup"><span data-stu-id="bfb1f-143">**Load**: Read data to be manipulated from the file system</span></span>

* <span data-ttu-id="bfb1f-144">**Transformación**: manipula los datos.</span><span class="sxs-lookup"><span data-stu-id="bfb1f-144">**Transform**: Manipulate the data</span></span>

* <span data-ttu-id="bfb1f-145">**Volcado o almacén**: generar datos en la pantalla o almacenarlos para su procesamiento.</span><span class="sxs-lookup"><span data-stu-id="bfb1f-145">**Dump or store**: Output data to the screen or store it for processing</span></span>

### <a name="user-defined-functions"></a><span data-ttu-id="bfb1f-146">Funciones definidas por el usuario</span><span class="sxs-lookup"><span data-stu-id="bfb1f-146">User-defined functions</span></span>

<span data-ttu-id="bfb1f-147">Pig Latin también admite las funciones definidas por el usuario (UDF), que le permiten invocar componentes externos que implementan la lógica que es difícil de modelar en Pig Latin.</span><span class="sxs-lookup"><span data-stu-id="bfb1f-147">Pig Latin also supports user-defined functions (UDF), which allows you to invoke external components that implement logic that is difficult to model in Pig Latin.</span></span>

<span data-ttu-id="bfb1f-148">Para más información sobre Pig Latin, consulte el [manual de referencia de Pig Latin 1](http://pig.apache.org/docs/r0.7.0/piglatin_ref1.html) y el [manual de referencia de Pig Latin 2](http://pig.apache.org/docs/r0.7.0/piglatin_ref2.html).</span><span class="sxs-lookup"><span data-stu-id="bfb1f-148">For more information about Pig Latin, see [Pig Latin Reference Manual 1](http://pig.apache.org/docs/r0.7.0/piglatin_ref1.html) and [Pig Latin Reference Manual 2](http://pig.apache.org/docs/r0.7.0/piglatin_ref2.html).</span></span>

<span data-ttu-id="bfb1f-149">Para obtener un ejemplo del uso de UDF con Pig, vea los siguientes documentos:</span><span class="sxs-lookup"><span data-stu-id="bfb1f-149">For an example of using UDFs with Pig, see the following documents:</span></span>

* <span data-ttu-id="bfb1f-150">[Utilice DataFu con Pig en HDInsight](hdinsight-hadoop-use-pig-datafu-udf.md) - DataFu es una colección de UDF útiles mantenida por Apache</span><span class="sxs-lookup"><span data-stu-id="bfb1f-150">[Use DataFu with Pig in HDInsight](hdinsight-hadoop-use-pig-datafu-udf.md) - DataFu is a collection of useful UDFs maintained by Apache</span></span>
* [<span data-ttu-id="bfb1f-151">Uso de Python con Pig y Hive en HDInsight</span><span class="sxs-lookup"><span data-stu-id="bfb1f-151">Use Python with Pig and Hive in HDInsight</span></span>](hdinsight-python.md)
* [<span data-ttu-id="bfb1f-152">Uso de C# con Hive y Pig en HDInsight</span><span class="sxs-lookup"><span data-stu-id="bfb1f-152">Use C# with Hive and Pig in HDInsight</span></span>](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)

## <span data-ttu-id="bfb1f-153"><a id="data"></a>Datos de ejemplo</span><span class="sxs-lookup"><span data-stu-id="bfb1f-153"><a id="data"></a>Example data</span></span>

<span data-ttu-id="bfb1f-154">HDInsight proporciona diversos conjuntos de datos de ejemplo que se almacenan en los directorios `/example/data` y `/HdiSamples`.</span><span class="sxs-lookup"><span data-stu-id="bfb1f-154">HDInsight provides various example data sets, which are stored in the `/example/data` and `/HdiSamples` directories.</span></span> <span data-ttu-id="bfb1f-155">Estos directorios están en el almacenamiento predeterminado del clúster.</span><span class="sxs-lookup"><span data-stu-id="bfb1f-155">These directories are in the default storage for your cluster.</span></span> <span data-ttu-id="bfb1f-156">El ejemplo de Pig de este documento utiliza el archivo *log4j* de `/example/data/sample.log`.</span><span class="sxs-lookup"><span data-stu-id="bfb1f-156">The Pig example in this document uses the *log4j* file from `/example/data/sample.log`.</span></span>

<span data-ttu-id="bfb1f-157">Cada registro del archivo consta de una línea de campos que contiene un campo `[LOG LEVEL]` para mostrar el tipo y la gravedad, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="bfb1f-157">Each log inside the file consists of a line of fields that contains a `[LOG LEVEL]` field to show the type and the severity, for example:</span></span>

    2012-02-03 20:26:41 SampleClass3 [ERROR] verbose detail for id 1527353937

<span data-ttu-id="bfb1f-158">En el ejemplo anterior, el nivel de registro es ERROR.</span><span class="sxs-lookup"><span data-stu-id="bfb1f-158">In the previous example, the log level is ERROR.</span></span>

> [!NOTE]
> <span data-ttu-id="bfb1f-159">También puede generar un archivo log4j con la herramienta de registro [Apache Log4j](http://en.wikipedia.org/wiki/Log4j) y luego cargarlo en el blob.</span><span class="sxs-lookup"><span data-stu-id="bfb1f-159">You can also generate a log4j file by using the [Apache Log4j](http://en.wikipedia.org/wiki/Log4j) logging tool and then upload that file to your blob.</span></span> <span data-ttu-id="bfb1f-160">Consulte [Carga de datos en HDInsight](hdinsight-upload-data.md) para obtener instrucciones.</span><span class="sxs-lookup"><span data-stu-id="bfb1f-160">See [Upload Data to HDInsight](hdinsight-upload-data.md) for instructions.</span></span> <span data-ttu-id="bfb1f-161">Para obtener más información sobre el uso de los blobs en Azure Storage con HDInsight, consulte [Uso de Azure Blob Storage con HDInsight](hdinsight-hadoop-use-blob-storage.md).</span><span class="sxs-lookup"><span data-stu-id="bfb1f-161">For more information about how blobs in Azure storage are used with HDInsight, see [Use Azure Blob Storage with HDInsight](hdinsight-hadoop-use-blob-storage.md).</span></span>

## <span data-ttu-id="bfb1f-162"><a id="job"></a>Trabajo de ejemplo</span><span class="sxs-lookup"><span data-stu-id="bfb1f-162"><a id="job"></a>Example job</span></span>

<span data-ttu-id="bfb1f-163">El siguiente trabajo de Pig Latin carga el archivo `sample.log` desde el almacenamiento predeterminado para el clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="bfb1f-163">The following Pig Latin job loads the `sample.log` file from the default storage for your HDInsight cluster.</span></span> <span data-ttu-id="bfb1f-164">A continuación, realiza una serie de transformaciones que generan un recuento de cuántas veces se ha producido cada nivel de registro en los datos de entrada.</span><span class="sxs-lookup"><span data-stu-id="bfb1f-164">Then it performs a series of transformations that result in a count of how many times each log level occurred in the input data.</span></span> <span data-ttu-id="bfb1f-165">Los resultados se escriben en STDOUT.</span><span class="sxs-lookup"><span data-stu-id="bfb1f-165">The results are written to STDOUT.</span></span>

    LOGS = LOAD 'wasb:///example/data/sample.log';
    LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
    FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
    GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
    FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
    RESULT = order FREQUENCIES by COUNT desc;
    DUMP RESULT;

<span data-ttu-id="bfb1f-166">En la siguiente imagen se muestra un resumen de lo que hace cada transformación a los datos.</span><span class="sxs-lookup"><span data-stu-id="bfb1f-166">The following image shows a summary of what each transformation does to the data.</span></span>

![Representación gráfica de las transformaciones][image-hdi-pig-data-transformation]

## <span data-ttu-id="bfb1f-168"><a id="run"></a>Ejecutar el trabajo de Pig Latin</span><span class="sxs-lookup"><span data-stu-id="bfb1f-168"><a id="run"></a>Run the Pig Latin job</span></span>

<span data-ttu-id="bfb1f-169">HDInsight puede ejecutar trabajos de Pig Latin mediante una variedad de métodos.</span><span class="sxs-lookup"><span data-stu-id="bfb1f-169">HDInsight can run Pig Latin jobs by using a variety of methods.</span></span> <span data-ttu-id="bfb1f-170">Use la tabla siguiente para decidir cuál es el método adecuado para usted luego siga el vínculo para ver un tutorial.</span><span class="sxs-lookup"><span data-stu-id="bfb1f-170">Use the following table to decide which method is right for you, then follow the link for a walkthrough.</span></span>

| <span data-ttu-id="bfb1f-171">**Utilícelo** si desea...</span><span class="sxs-lookup"><span data-stu-id="bfb1f-171">**Use this** if you want...</span></span> | <span data-ttu-id="bfb1f-172">...un shell **interactivo**</span><span class="sxs-lookup"><span data-stu-id="bfb1f-172">...an **interactive** shell</span></span> | <span data-ttu-id="bfb1f-173">...procesamiento por**lotes**</span><span class="sxs-lookup"><span data-stu-id="bfb1f-173">...**batch** processing</span></span> | <span data-ttu-id="bfb1f-174">...con este **sistema operativo de clúster**</span><span class="sxs-lookup"><span data-stu-id="bfb1f-174">...with this **cluster operating system**</span></span> | <span data-ttu-id="bfb1f-175">...de este **cliente**</span><span class="sxs-lookup"><span data-stu-id="bfb1f-175">...from this **client**</span></span> |
|:--- |:---:|:---:|:--- |:--- |
| [<span data-ttu-id="bfb1f-176">SSH</span><span class="sxs-lookup"><span data-stu-id="bfb1f-176">SSH</span></span>](hdinsight-hadoop-use-pig-ssh.md) |<span data-ttu-id="bfb1f-177">✔</span><span class="sxs-lookup"><span data-stu-id="bfb1f-177">✔</span></span> |<span data-ttu-id="bfb1f-178">✔</span><span class="sxs-lookup"><span data-stu-id="bfb1f-178">✔</span></span> |<span data-ttu-id="bfb1f-179">Linux</span><span class="sxs-lookup"><span data-stu-id="bfb1f-179">Linux</span></span> |<span data-ttu-id="bfb1f-180">Linux, Unix, Mac OS X o Windows</span><span class="sxs-lookup"><span data-stu-id="bfb1f-180">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="bfb1f-181">Curl</span><span class="sxs-lookup"><span data-stu-id="bfb1f-181">Curl</span></span>](hdinsight-hadoop-use-pig-curl.md) |&nbsp; |<span data-ttu-id="bfb1f-182">✔</span><span class="sxs-lookup"><span data-stu-id="bfb1f-182">✔</span></span> |<span data-ttu-id="bfb1f-183">Linux o Windows</span><span class="sxs-lookup"><span data-stu-id="bfb1f-183">Linux or Windows</span></span> |<span data-ttu-id="bfb1f-184">Linux, Unix, Mac OS X o Windows</span><span class="sxs-lookup"><span data-stu-id="bfb1f-184">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="bfb1f-185">.NET SDK para Hadoop</span><span class="sxs-lookup"><span data-stu-id="bfb1f-185">.NET SDK for Hadoop</span></span>](hdinsight-hadoop-use-pig-dotnet-sdk.md) |&nbsp; |<span data-ttu-id="bfb1f-186">✔</span><span class="sxs-lookup"><span data-stu-id="bfb1f-186">✔</span></span> |<span data-ttu-id="bfb1f-187">Linux o Windows</span><span class="sxs-lookup"><span data-stu-id="bfb1f-187">Linux or Windows</span></span> |<span data-ttu-id="bfb1f-188">Windows (por ahora)</span><span class="sxs-lookup"><span data-stu-id="bfb1f-188">Windows (for now)</span></span> |
| [<span data-ttu-id="bfb1f-189">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="bfb1f-189">Windows PowerShell</span></span>](hdinsight-hadoop-use-pig-powershell.md) |&nbsp; |<span data-ttu-id="bfb1f-190">✔</span><span class="sxs-lookup"><span data-stu-id="bfb1f-190">✔</span></span> |<span data-ttu-id="bfb1f-191">Linux o Windows</span><span class="sxs-lookup"><span data-stu-id="bfb1f-191">Linux or Windows</span></span> |<span data-ttu-id="bfb1f-192">Windows</span><span class="sxs-lookup"><span data-stu-id="bfb1f-192">Windows</span></span> |
| <span data-ttu-id="bfb1f-193">[Escritorio remoto](hdinsight-hadoop-use-pig-remote-desktop.md) (HDInsight 3.2 y 3.3)</span><span class="sxs-lookup"><span data-stu-id="bfb1f-193">[Remote Desktop](hdinsight-hadoop-use-pig-remote-desktop.md) (HDInsight 3.2 and 3.3)</span></span> |<span data-ttu-id="bfb1f-194">✔</span><span class="sxs-lookup"><span data-stu-id="bfb1f-194">✔</span></span> |<span data-ttu-id="bfb1f-195">✔</span><span class="sxs-lookup"><span data-stu-id="bfb1f-195">✔</span></span> |<span data-ttu-id="bfb1f-196">Windows</span><span class="sxs-lookup"><span data-stu-id="bfb1f-196">Windows</span></span> |<span data-ttu-id="bfb1f-197">Windows</span><span class="sxs-lookup"><span data-stu-id="bfb1f-197">Windows</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="bfb1f-198">Linux es el único sistema operativo que se usa en la versión 3.4 de HDInsight, o en las superiores.</span><span class="sxs-lookup"><span data-stu-id="bfb1f-198">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="bfb1f-199">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="bfb1f-199">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="pig-and-sql-server-integration-services"></a><span data-ttu-id="bfb1f-200">Pig y SQL Server Integration Services</span><span class="sxs-lookup"><span data-stu-id="bfb1f-200">Pig and SQL Server Integration Services</span></span>

<span data-ttu-id="bfb1f-201">Puede usar SQL Server Integration Services (SSIS) para ejecutar un trabajo de Pig.</span><span class="sxs-lookup"><span data-stu-id="bfb1f-201">You can use SQL Server Integration Services (SSIS) to run a Pig job.</span></span> <span data-ttu-id="bfb1f-202">El paquete de características de Azure para SSIS proporciona los siguientes componentes que funcionan con trabajos de Pig en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="bfb1f-202">The Azure Feature Pack for SSIS provides the following components that work with Pig jobs on HDInsight.</span></span>

* <span data-ttu-id="bfb1f-203">[Tarea de Pig de Azure HDInsight][pigtask]</span><span class="sxs-lookup"><span data-stu-id="bfb1f-203">[Azure HDInsight Pig Task][pigtask]</span></span>

* <span data-ttu-id="bfb1f-204">[Administrador de conexiones de suscripción de Azure][connectionmanager]</span><span class="sxs-lookup"><span data-stu-id="bfb1f-204">[Azure Subscription Connection Manager][connectionmanager]</span></span>

<span data-ttu-id="bfb1f-205">Obtenga más información sobre el paquete de características de Azure para SSIS [aquí][ssispack].</span><span class="sxs-lookup"><span data-stu-id="bfb1f-205">Learn more about the Azure Feature Pack for SSIS [here][ssispack].</span></span>

## <span data-ttu-id="bfb1f-206"><a id="nextsteps"></a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="bfb1f-206"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="bfb1f-207">Ahora que aprendió a usar Pig con HDInsight, use los siguientes vínculos para explorar otras formas de trabajar con HDInsight de Azure.</span><span class="sxs-lookup"><span data-stu-id="bfb1f-207">Now that you have learned how to use Pig with HDInsight, use the following links to explore other ways to work with Azure HDInsight.</span></span>

* <span data-ttu-id="bfb1f-208">[Carga de datos en HDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="bfb1f-208">[Upload data to HDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="bfb1f-209">[Uso de Hive con HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="bfb1f-209">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* [<span data-ttu-id="bfb1f-210">Uso de Sqoop con HDInsight</span><span class="sxs-lookup"><span data-stu-id="bfb1f-210">Use Sqoop with HDInsight</span></span>](hdinsight-use-sqoop.md)
* [<span data-ttu-id="bfb1f-211">Uso de Oozie con HDInsight</span><span class="sxs-lookup"><span data-stu-id="bfb1f-211">Use Oozie with HDInsight</span></span>](hdinsight-use-oozie.md)
* <span data-ttu-id="bfb1f-212">[Uso de trabajos de MapReduce con HDInsight][hdinsight-use-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="bfb1f-212">[Use MapReduce jobs with HDInsight][hdinsight-use-mapreduce]</span></span>

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
