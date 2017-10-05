---
title: "Qué son Apache Hive y HiveQL: Azure HDInsight | Microsoft Docs"
description: Apache Hive es un sistema de almacenamiento de datos para Hadoop. Puede consultar datos almacenados en Hive mediante HiveQL, que se parece a Transact-SQL. En este documento, aprenda a usar Hive y HiveQL con Azure HDInsight.
keywords: "hiveql,qué es hive,hadoop hiveql,cómo usar hive,aprender hive,qué es hive"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 2c10f989-7636-41bf-b7f7-c4b67ec0814f
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/03/2017
ms.author: larryfr
ms.openlocfilehash: 6b3ee17141f773bec07cf40e0b6d63363e9b5164
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="what-is-apache-hive-and-hiveql-on-azure-hdinsight"></a><span data-ttu-id="e0798-106">¿Qué son Apache Hive y HiveQL en Azure HDInsight?</span><span class="sxs-lookup"><span data-stu-id="e0798-106">What is Apache Hive and HiveQL on Azure HDInsight?</span></span>

<span data-ttu-id="e0798-107">[Apache Hive](http://hive.apache.org/) es un sistema de almacenamiento de datos para Hadoop.</span><span class="sxs-lookup"><span data-stu-id="e0798-107">[Apache Hive](http://hive.apache.org/) is a data warehouse system for Hadoop.</span></span> <span data-ttu-id="e0798-108">Hive hace posibles el resumen de los datos, las consultas y el análisis de datos.</span><span class="sxs-lookup"><span data-stu-id="e0798-108">Hive enables data summarization, querying, and analysis of data.</span></span> <span data-ttu-id="e0798-109">Las consultas de Hive se escriben en HiveQL, que es un lenguaje de consulta similar a SQL.</span><span class="sxs-lookup"><span data-stu-id="e0798-109">Hive queries are written in HiveQL, which is a query language similar to SQL.</span></span>

<span data-ttu-id="e0798-110">Hive le permite proyectar la estructura del proyecto en datos que en gran medida no están estructurados.</span><span class="sxs-lookup"><span data-stu-id="e0798-110">Hive allows you to project structure on largely unstructured data.</span></span> <span data-ttu-id="e0798-111">Después de definir la estructura, puede usar HiveQL para consultar los datos sin conocimientos de Java ni MapReduce.</span><span class="sxs-lookup"><span data-stu-id="e0798-111">After you define the structure, you can use HiveQL to query the data without knowledge of Java or MapReduce.</span></span>

<span data-ttu-id="e0798-112">HDInsight proporciona varios tipos de clúster, que están optimizados para cargas de trabajo específicas.</span><span class="sxs-lookup"><span data-stu-id="e0798-112">HDInsight provides several cluster types, which are tuned for specific workloads.</span></span> <span data-ttu-id="e0798-113">Se suelen usar los siguientes tipos de clúster para consultas de Hive:</span><span class="sxs-lookup"><span data-stu-id="e0798-113">The following cluster types are most often used for Hive queries:</span></span>

* <span data-ttu-id="e0798-114">__Hive interactivo__: un clúster de Hadoop que proporciona funcionalidad de [procesamiento analítico de baja latencia (LLAP)](https://cwiki.apache.org/confluence/display/Hive/LLAP) para mejorar los tiempos de respuesta de las consultas interactivas.</span><span class="sxs-lookup"><span data-stu-id="e0798-114">__Interactive Hive__: A Hadoop cluster that provides [Low Latency Analytical Processing (LLAP)](https://cwiki.apache.org/confluence/display/Hive/LLAP) functionality to improve response times for interactive queries.</span></span> <span data-ttu-id="e0798-115">Para más información, consulte el documento sobre el [inicio con Hive interactivo en HDInsight](hdinsight-hadoop-use-interactive-hive.md).</span><span class="sxs-lookup"><span data-stu-id="e0798-115">For more information, see the [Start with Interactive Hive in HDInsight](hdinsight-hadoop-use-interactive-hive.md) document.</span></span>

* <span data-ttu-id="e0798-116">__Hadoop__: un clúster de Hadoop que está optimizado para cargas de trabajo de procesamiento por lotes.</span><span class="sxs-lookup"><span data-stu-id="e0798-116">__Hadoop__: A Hadoop cluster that is tuned for batch processing workloads.</span></span> <span data-ttu-id="e0798-117">Para más información, consulte el documento sobre el [inicio con Hadoop en HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="e0798-117">For more information, see the [Start with Hadoop in HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md) document.</span></span>

* <span data-ttu-id="e0798-118">__Spark__: Apache Spark tiene funcionalidad integrada para trabajar con Hive.</span><span class="sxs-lookup"><span data-stu-id="e0798-118">__Spark__: Apache Spark has built-in functionality for working with Hive.</span></span> <span data-ttu-id="e0798-119">Para más información, consulte el documento sobre el [inicio con Spark en HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="e0798-119">For more information, see the [Start with Spark on HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md) document.</span></span>

* <span data-ttu-id="e0798-120">__HBase__: se puede usar HiveQL para consultar datos almacenados en HBase.</span><span class="sxs-lookup"><span data-stu-id="e0798-120">__HBase__: HiveQL can be used to query data stored in HBase.</span></span> <span data-ttu-id="e0798-121">Para más información, consulte el documento sobre el [inicio con HBase en HDInsight](hdinsight-hbase-tutorial-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="e0798-121">For more information, see the [Start with HBase on HDInsight](hdinsight-hbase-tutorial-get-started-linux.md) document.</span></span>

## <a name="how-to-use-hive"></a><span data-ttu-id="e0798-122">Uso de Hive</span><span class="sxs-lookup"><span data-stu-id="e0798-122">How to use Hive</span></span>

<span data-ttu-id="e0798-123">Utilice la siguiente tabla para averiguar cómo usar Hive con HDInsight:</span><span class="sxs-lookup"><span data-stu-id="e0798-123">Use the following table to discover how to use Hive with HDInsight:</span></span>

| <span data-ttu-id="e0798-124">**Use este método** si desea…</span><span class="sxs-lookup"><span data-stu-id="e0798-124">**Use this method** if you want...</span></span> | <span data-ttu-id="e0798-125">...un shell **interactivo**</span><span class="sxs-lookup"><span data-stu-id="e0798-125">...an **interactive** shell</span></span> | <span data-ttu-id="e0798-126">...procesamiento por**lotes**</span><span class="sxs-lookup"><span data-stu-id="e0798-126">...**batch** processing</span></span> | <span data-ttu-id="e0798-127">...con este **sistema operativo de clúster**</span><span class="sxs-lookup"><span data-stu-id="e0798-127">...with this **cluster operating system**</span></span> | <span data-ttu-id="e0798-128">...desde este **sistema operativo de cliente**</span><span class="sxs-lookup"><span data-stu-id="e0798-128">...from this **client operating system**</span></span> |
|:--- |:---:|:---:|:--- |:--- |
| [<span data-ttu-id="e0798-129">Vista de Hive</span><span class="sxs-lookup"><span data-stu-id="e0798-129">Hive View</span></span>](hdinsight-hadoop-use-hive-ambari-view.md) |<span data-ttu-id="e0798-130">✔</span><span class="sxs-lookup"><span data-stu-id="e0798-130">✔</span></span> |<span data-ttu-id="e0798-131">✔</span><span class="sxs-lookup"><span data-stu-id="e0798-131">✔</span></span> |<span data-ttu-id="e0798-132">Linux</span><span class="sxs-lookup"><span data-stu-id="e0798-132">Linux</span></span> |<span data-ttu-id="e0798-133">Cualquiera (en función del explorador)</span><span class="sxs-lookup"><span data-stu-id="e0798-133">Any (browser based)</span></span> |
| [<span data-ttu-id="e0798-134">Cliente Beeline</span><span class="sxs-lookup"><span data-stu-id="e0798-134">Beeline client</span></span>](hdinsight-hadoop-use-hive-beeline.md) |<span data-ttu-id="e0798-135">✔</span><span class="sxs-lookup"><span data-stu-id="e0798-135">✔</span></span> |<span data-ttu-id="e0798-136">✔</span><span class="sxs-lookup"><span data-stu-id="e0798-136">✔</span></span> |<span data-ttu-id="e0798-137">Linux</span><span class="sxs-lookup"><span data-stu-id="e0798-137">Linux</span></span> |<span data-ttu-id="e0798-138">Linux, Unix, Mac OS X o Windows</span><span class="sxs-lookup"><span data-stu-id="e0798-138">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="e0798-139">API DE REST</span><span class="sxs-lookup"><span data-stu-id="e0798-139">REST API</span></span>](hdinsight-hadoop-use-hive-curl.md) |&nbsp; |<span data-ttu-id="e0798-140">✔</span><span class="sxs-lookup"><span data-stu-id="e0798-140">✔</span></span> |<span data-ttu-id="e0798-141">Linux o Windows*</span><span class="sxs-lookup"><span data-stu-id="e0798-141">Linux or Windows*</span></span> |<span data-ttu-id="e0798-142">Linux, Unix, Mac OS X o Windows</span><span class="sxs-lookup"><span data-stu-id="e0798-142">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="e0798-143">Herramientas de HDInsight para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e0798-143">HDInsight tools for Visual Studio</span></span>](hdinsight-hadoop-use-hive-visual-studio.md) |&nbsp; |<span data-ttu-id="e0798-144">✔</span><span class="sxs-lookup"><span data-stu-id="e0798-144">✔</span></span> |<span data-ttu-id="e0798-145">Linux o Windows*</span><span class="sxs-lookup"><span data-stu-id="e0798-145">Linux or Windows*</span></span> |<span data-ttu-id="e0798-146">Windows</span><span class="sxs-lookup"><span data-stu-id="e0798-146">Windows</span></span> |
| [<span data-ttu-id="e0798-147">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="e0798-147">Windows PowerShell</span></span>](hdinsight-hadoop-use-hive-powershell.md) |&nbsp; |<span data-ttu-id="e0798-148">✔</span><span class="sxs-lookup"><span data-stu-id="e0798-148">✔</span></span> |<span data-ttu-id="e0798-149">Linux o Windows*</span><span class="sxs-lookup"><span data-stu-id="e0798-149">Linux or Windows*</span></span> |<span data-ttu-id="e0798-150">Windows</span><span class="sxs-lookup"><span data-stu-id="e0798-150">Windows</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="e0798-151">\* Linux es el único sistema operativo que se usa en HDInsight versión 3.4 o posteriores.</span><span class="sxs-lookup"><span data-stu-id="e0798-151">\* Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="e0798-152">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="e0798-152">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="e0798-153">Si está usando un clúster de HDInsight basado en Windows, puede usar la [consola de consulta](hdinsight-hadoop-use-hive-query-console.md) desde el explorador o el [Escritorio remoto](hdinsight-hadoop-use-hive-remote-desktop.md) para ejecutar consultas de Hive.</span><span class="sxs-lookup"><span data-stu-id="e0798-153">If you are using a Windows-based HDInsight cluster, you can use the [Query console](hdinsight-hadoop-use-hive-query-console.md) from your browser or [Remote Desktop](hdinsight-hadoop-use-hive-remote-desktop.md) to run Hive queries.</span></span>

## <a name="hiveql-language-reference"></a><span data-ttu-id="e0798-154">Referencia del lenguaje HiveQL</span><span class="sxs-lookup"><span data-stu-id="e0798-154">HiveQL language reference</span></span>

<span data-ttu-id="e0798-155">La referencia sobre el lenguaje HiveQL está disponible en el [manual del lenguaje (https://cwiki.apache.org/confluence/display/Hive/LanguageManual)](https://cwiki.apache.org/confluence/display/Hive/LanguageManual).</span><span class="sxs-lookup"><span data-stu-id="e0798-155">HiveQL language reference is available in the [language manual (https://cwiki.apache.org/confluence/display/Hive/LanguageManual)](https://cwiki.apache.org/confluence/display/Hive/LanguageManual).</span></span>

## <a name="hive-and-data-structure"></a><span data-ttu-id="e0798-156">Hive y estructura de datos</span><span class="sxs-lookup"><span data-stu-id="e0798-156">Hive and data structure</span></span>

<span data-ttu-id="e0798-157">Hive entiende cómo trabajar con los datos estructurados y semiestructurados.</span><span class="sxs-lookup"><span data-stu-id="e0798-157">Hive understands how to work with structured and semi-structured data.</span></span> <span data-ttu-id="e0798-158">Por ejemplo, archivos de texto donde los campos están delimitados por caracteres específicos.</span><span class="sxs-lookup"><span data-stu-id="e0798-158">For example, text files where the fields are delimited by specific characters.</span></span> <span data-ttu-id="e0798-159">La siguiente instrucción HiveQL crea una tabla de datos delimitados por espacios:</span><span class="sxs-lookup"><span data-stu-id="e0798-159">The following HiveQL statement creates a table over space-delimited data:</span></span>

```hiveql
CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
STORED AS TEXTFILE LOCATION '/example/data/';
```

<span data-ttu-id="e0798-160">Hive también admite **serializador/deserializadores (SerDe)** personalizados para datos estructurados irregularmente o complejos.</span><span class="sxs-lookup"><span data-stu-id="e0798-160">Hive also supports custom **serializer/deserializers (SerDe)** for complex or irregularly structured data.</span></span> <span data-ttu-id="e0798-161">Para obtener más información, consulte el documento [Uso de un SerDe de JSON personalizado con HDInsight](http://blogs.msdn.com/b/bigdatasupport/archive/2014/06/18/how-to-use-a-custom-json-serde-with-microsoft-azure-hdinsight.aspx).</span><span class="sxs-lookup"><span data-stu-id="e0798-161">For more information, see the [How to use a custom JSON SerDe with HDInsight](http://blogs.msdn.com/b/bigdatasupport/archive/2014/06/18/how-to-use-a-custom-json-serde-with-microsoft-azure-hdinsight.aspx) document.</span></span>

<span data-ttu-id="e0798-162">Para más información sobre los formatos de archivo compatibles con Hive, consulte el [manual del lenguaje (https://cwiki.apache.org/confluence/display/Hive/LanguageManual)](https://cwiki.apache.org/confluence/display/Hive/LanguageManual).</span><span class="sxs-lookup"><span data-stu-id="e0798-162">For more information on file formats supported by Hive, see the [Language manual (https://cwiki.apache.org/confluence/display/Hive/LanguageManual)](https://cwiki.apache.org/confluence/display/Hive/LanguageManual)</span></span>

## <a name="hive-internal-tables-vs-external-tables"></a><span data-ttu-id="e0798-163">Tablas internas frente a tablas externas de Hive.</span><span class="sxs-lookup"><span data-stu-id="e0798-163">Hive internal tables vs external tables</span></span>

<span data-ttu-id="e0798-164">Hay dos tipos de tablas que puede crear con Hive:</span><span class="sxs-lookup"><span data-stu-id="e0798-164">There are two types of tables that you can create with Hive:</span></span>

* <span data-ttu-id="e0798-165">__Internas__: los datos se almacenan en el almacenamiento de datos de Hive.</span><span class="sxs-lookup"><span data-stu-id="e0798-165">__Internal__: Data is stored in the Hive data warehouse.</span></span> <span data-ttu-id="e0798-166">El almacenamiento de datos se encuentra en `/hive/warehouse/` en el almacenamiento predeterminado para el clúster.</span><span class="sxs-lookup"><span data-stu-id="e0798-166">The data warehouse is located at `/hive/warehouse/` on the default storage for the cluster.</span></span>

    <span data-ttu-id="e0798-167">Use tablas internas cuando:</span><span class="sxs-lookup"><span data-stu-id="e0798-167">Use internal tables when:</span></span>

    * <span data-ttu-id="e0798-168">Los datos sean temporales.</span><span class="sxs-lookup"><span data-stu-id="e0798-168">Data is temporary.</span></span>
    * <span data-ttu-id="e0798-169">Desee que Hive administre el ciclo de vida de la tabla y los datos.</span><span class="sxs-lookup"><span data-stu-id="e0798-169">You want Hive to manage the lifecycle of the table and data.</span></span>

* <span data-ttu-id="e0798-170">__Externas__: los datos se almacenan fuera del almacenamiento de datos.</span><span class="sxs-lookup"><span data-stu-id="e0798-170">__External__: Data is stored outside the data warehouse.</span></span> <span data-ttu-id="e0798-171">Los datos se pueden almacenar en cualquier almacenamiento accesible desde el clúster.</span><span class="sxs-lookup"><span data-stu-id="e0798-171">The data can be stored on any storage accessible by the cluster.</span></span>

    <span data-ttu-id="e0798-172">Use tablas externas cuando:</span><span class="sxs-lookup"><span data-stu-id="e0798-172">Use external tables when:</span></span>

    * <span data-ttu-id="e0798-173">Los datos también se utilicen fuera de Hive.</span><span class="sxs-lookup"><span data-stu-id="e0798-173">The data is also used outside of Hive.</span></span> <span data-ttu-id="e0798-174">Por ejemplo, los archivos de datos se actualizan en otro proceso (que no bloquea los archivos).</span><span class="sxs-lookup"><span data-stu-id="e0798-174">For example, the data files are updated by another process (that does not lock the files.)</span></span>
    * <span data-ttu-id="e0798-175">Los datos deban permanecer en la ubicación subyacente, incluso después de eliminarse la tabla.</span><span class="sxs-lookup"><span data-stu-id="e0798-175">Data needs to remain in the underlying location, even after dropping the table.</span></span>
    * <span data-ttu-id="e0798-176">Necesite una ubicación personalizada, como una cuenta de almacenamiento no predeterminada.</span><span class="sxs-lookup"><span data-stu-id="e0798-176">You need a custom location, such as a non-default storage account.</span></span>
    * <span data-ttu-id="e0798-177">Un programa distinto de Hive administre el formato de datos, la ubicación, etc.</span><span class="sxs-lookup"><span data-stu-id="e0798-177">A program other than hive manages the data format, location, etc.</span></span>

<span data-ttu-id="e0798-178">Para más información, consulte la entrada de blog [Hive Internal and External Tables Intro][cindygross-hive-tables] (Introducción a las tablas internas y externas de Hive).</span><span class="sxs-lookup"><span data-stu-id="e0798-178">For more information, see the [Hive Internal and External Tables Intro][cindygross-hive-tables] blog post.</span></span>

## <a name="user-defined-functions-udf"></a><span data-ttu-id="e0798-179">Funciones definidas por el usuario (UDF)</span><span class="sxs-lookup"><span data-stu-id="e0798-179">User-defined functions (UDF)</span></span>

<span data-ttu-id="e0798-180">Hive también puede extenderse a través de **funciones definidas por el usuario (UDF)**.</span><span class="sxs-lookup"><span data-stu-id="e0798-180">Hive can also be extended through **user-defined functions (UDF)**.</span></span> <span data-ttu-id="e0798-181">Una UDF le permite implementar la funcionalidad o la lógica que no se modela con facilidad en HiveQL.</span><span class="sxs-lookup"><span data-stu-id="e0798-181">A UDF allows you to implement functionality or logic that isn't easily modeled in HiveQL.</span></span> <span data-ttu-id="e0798-182">Para obtener un ejemplo del uso de UDF con Hive, vea los siguientes documentos:</span><span class="sxs-lookup"><span data-stu-id="e0798-182">For an example of using UDFs with Hive, see the following documents:</span></span>

* [<span data-ttu-id="e0798-183">Utilización de una función definida por el usuario de Java con Hive</span><span class="sxs-lookup"><span data-stu-id="e0798-183">Use a Java user-defined function with Hive</span></span>](hdinsight-hadoop-hive-java-udf.md)

* [<span data-ttu-id="e0798-184">Uso de funciones definidas por el usuario (UDF) de Python con Hive y Pig</span><span class="sxs-lookup"><span data-stu-id="e0798-184">Use a Python user-defined function with Hive and Pig</span></span>](hdinsight-python.md)

* [<span data-ttu-id="e0798-185">Uso de funciones definidas por el usuario de C# con Hive y Pig</span><span class="sxs-lookup"><span data-stu-id="e0798-185">Use a C# user-defined function with Hive and Pig</span></span>](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)

* [<span data-ttu-id="e0798-186">Cómo agregar una función definida por el usuario de Hive personalizada a HDInsight</span><span class="sxs-lookup"><span data-stu-id="e0798-186">How to add a custom Hive user-defined function to HDInsight</span></span>](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/14/how-to-add-custom-hive-udfs-to-hdinsight.aspx)

* [<span data-ttu-id="e0798-187">Un ejemplo de función definida por el usuario de Hive para convertir formatos de fecha y hora en una marca de tiempo de Hive</span><span class="sxs-lookup"><span data-stu-id="e0798-187">An example Hive user-defined function to convert date/time formats to Hive timestamp</span></span>](https://github.com/Azure-Samples/hdinsight-java-hive-udf)

## <span data-ttu-id="e0798-188"><a id="data"></a>Datos de ejemplo</span><span class="sxs-lookup"><span data-stu-id="e0798-188"><a id="data"></a>Example data</span></span>

<span data-ttu-id="e0798-189">Hive en HDInsight tiene ya cargada una tabla interna denominada `hivesampletable`.</span><span class="sxs-lookup"><span data-stu-id="e0798-189">Hive on HDInsight comes pre-loaded with an internal table named `hivesampletable`.</span></span> <span data-ttu-id="e0798-190">Además, HDInsight proporciona conjuntos de datos de ejemplo que se pueden usar con Hive.</span><span class="sxs-lookup"><span data-stu-id="e0798-190">HDInsight also provides example data sets that can be used with Hive.</span></span> <span data-ttu-id="e0798-191">Estos conjuntos de datos se almacenan en los directorios `/example/data` y `/HdiSamples`.</span><span class="sxs-lookup"><span data-stu-id="e0798-191">These data sets are stored in the `/example/data` and `/HdiSamples` directories.</span></span> <span data-ttu-id="e0798-192">Estos directorios existen en el almacenamiento predeterminado del clúster.</span><span class="sxs-lookup"><span data-stu-id="e0798-192">These directories exist in the default storage for your cluster.</span></span>

## <span data-ttu-id="e0798-193"><a id="job"></a>Ejemplo de consulta de Hive</span><span class="sxs-lookup"><span data-stu-id="e0798-193"><a id="job"></a>Example Hive query</span></span>

<span data-ttu-id="e0798-194">Las siguientes instrucciones de HiveQL proyectan columnas sobre el archivo `/example/data/sample.log`:</span><span class="sxs-lookup"><span data-stu-id="e0798-194">The following HiveQL statements project columns onto the `/example/data/sample.log` file:</span></span>

    set hive.execution.engine=tez;
    DROP TABLE log4jLogs;
    CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
    STORED AS TEXTFILE LOCATION '/example/data/';
    SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

<span data-ttu-id="e0798-195">En el ejemplo anterior, las instrucciones de HiveQL realizan las acciones siguientes:</span><span class="sxs-lookup"><span data-stu-id="e0798-195">In the previous example, the HiveQL statements perform the following actions:</span></span>

* <span data-ttu-id="e0798-196">`set hive.execution.engine=tez;`: establece el motor de ejecución para usar Tez.</span><span class="sxs-lookup"><span data-stu-id="e0798-196">`set hive.execution.engine=tez;`: Sets the execution engine to use Tez.</span></span> <span data-ttu-id="e0798-197">Si se utiliza Tez en lugar de MapReduce, se puede mejorar el rendimiento de las consultas.</span><span class="sxs-lookup"><span data-stu-id="e0798-197">Using Tez instead of MapReduce can provide an increase in query performance.</span></span> <span data-ttu-id="e0798-198">Para más información sobre Tez, consulte la sección [Use Apache Tez para un mejor rendimiento](#usetez) .</span><span class="sxs-lookup"><span data-stu-id="e0798-198">For more information on Tez, see the [Use Apache Tez for improved performance](#usetez) section.</span></span>

    > [!NOTE]
    > <span data-ttu-id="e0798-199">Esta instrucción solo se requiere cuando se usa un clúster de HDInsight basado en Windows.</span><span class="sxs-lookup"><span data-stu-id="e0798-199">This statement is only required when using a Windows-based HDInsight cluster.</span></span> <span data-ttu-id="e0798-200">Tez es el motor de ejecución predeterminado para HDInsight basado en Linux.</span><span class="sxs-lookup"><span data-stu-id="e0798-200">Tez is the default execution engine for Linux-based HDInsight.</span></span>

* <span data-ttu-id="e0798-201">`DROP TABLE`: si la tabla ya existe, la elimina.</span><span class="sxs-lookup"><span data-stu-id="e0798-201">`DROP TABLE`: If the table already exists, delete it.</span></span>

* <span data-ttu-id="e0798-202">`CREATE EXTERNAL TABLE`: crea una tabla **externa** en Hive.</span><span class="sxs-lookup"><span data-stu-id="e0798-202">`CREATE EXTERNAL TABLE`: Creates a new **external** table in Hive.</span></span> <span data-ttu-id="e0798-203">Las tablas externas solo almacenan la definición de Tabla en Hive.</span><span class="sxs-lookup"><span data-stu-id="e0798-203">External tables only store the table definition in Hive.</span></span> <span data-ttu-id="e0798-204">Los datos permanecen en la ubicación y formato originales.</span><span class="sxs-lookup"><span data-stu-id="e0798-204">The data is left in the original location and in the original format.</span></span>

* <span data-ttu-id="e0798-205">`ROW FORMAT`: Indica cómo se da formato a los datos de Hive.</span><span class="sxs-lookup"><span data-stu-id="e0798-205">`ROW FORMAT`: Tells Hive how the data is formatted.</span></span> <span data-ttu-id="e0798-206">En este caso, los campos de cada registro se separan mediante un espacio.</span><span class="sxs-lookup"><span data-stu-id="e0798-206">In this case, the fields in each log are separated by a space.</span></span>

* <span data-ttu-id="e0798-207">`STORED AS TEXTFILE LOCATION`: indica a Hive dónde se almacenan los datos (el directorio `example/data`) y que se almacenen como texto.</span><span class="sxs-lookup"><span data-stu-id="e0798-207">`STORED AS TEXTFILE LOCATION`: Tells Hive where the data is stored (the `example/data` directory) and that it is stored as text.</span></span> <span data-ttu-id="e0798-208">Los datos pueden estar en un archivo o distribuidos en varios archivos dentro del directorio.</span><span class="sxs-lookup"><span data-stu-id="e0798-208">The data can be in one file or spread across multiple files within the directory.</span></span>

* <span data-ttu-id="e0798-209">`SELECT`: selecciona el número total de filas donde la columna **t4** contiene el valor **[ERROR]**.</span><span class="sxs-lookup"><span data-stu-id="e0798-209">`SELECT`: Selects a count of all rows where the column **t4** contains the value **[ERROR]**.</span></span> <span data-ttu-id="e0798-210">Esta instrucción devuelve un valor de **3** porque hay tres filas que contienen este valor.</span><span class="sxs-lookup"><span data-stu-id="e0798-210">This statement returns a value of **3** because there are three rows that contain this value.</span></span>

* <span data-ttu-id="e0798-211">`INPUT__FILE__NAME LIKE '%.log'`: Hive intenta aplicar el esquema a todos los archivos en el directorio.</span><span class="sxs-lookup"><span data-stu-id="e0798-211">`INPUT__FILE__NAME LIKE '%.log'` - Hive attempts to apply the schema to all files in the directory.</span></span> <span data-ttu-id="e0798-212">En este caso, el directorio contiene archivos que no coinciden con el esquema.</span><span class="sxs-lookup"><span data-stu-id="e0798-212">In this case, the directory contains files that do not match the schema.</span></span> <span data-ttu-id="e0798-213">Para evitar que haya datos inservibles en los resultados, esta instrucción indica a Hive que solo se deben devolver datos de archivos que terminen en .log.</span><span class="sxs-lookup"><span data-stu-id="e0798-213">To prevent garbage data in the results, this statement tells Hive that we should only return data from files ending in .log.</span></span>

> [!NOTE]
> <span data-ttu-id="e0798-214">Las tablas externas se deben utilizar cuando se espera que un origen externo actualice los datos subyacentes.</span><span class="sxs-lookup"><span data-stu-id="e0798-214">External tables should be used when you expect the underlying data to be updated by an external source.</span></span> <span data-ttu-id="e0798-215">Por ejemplo, un proceso de carga de datos automatizado o una operación de MapReduce.</span><span class="sxs-lookup"><span data-stu-id="e0798-215">For example, an automated data upload process, or MapReduce operation.</span></span>
>
> <span data-ttu-id="e0798-216">La eliminación de una tabla externa **no** elimina los datos, solamente la definición de tabla.</span><span class="sxs-lookup"><span data-stu-id="e0798-216">Dropping an external table does **not** delete the data, it only deletes the table definition.</span></span>

<span data-ttu-id="e0798-217">Para crear una tabla **interna** en lugar de una externa, use el siguiente HiveQL:</span><span class="sxs-lookup"><span data-stu-id="e0798-217">To create an **internal** table instead of external, use the following HiveQL:</span></span>

    set hive.execution.engine=tez;
    CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    STORED AS ORC;
    INSERT OVERWRITE TABLE errorLogs
    SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]';

<span data-ttu-id="e0798-218">Estas instrucciones realizan las acciones siguientes:</span><span class="sxs-lookup"><span data-stu-id="e0798-218">These statements perform the following actions:</span></span>

* <span data-ttu-id="e0798-219">`CREATE TABLE IF NOT EXISTS`: si la tabla no existe, créela.</span><span class="sxs-lookup"><span data-stu-id="e0798-219">`CREATE TABLE IF NOT EXISTS`: If the table does not exist, create it.</span></span> <span data-ttu-id="e0798-220">Como no se usa la palabra clave **EXTERNAL**, esta instrucción crea una tabla interna.</span><span class="sxs-lookup"><span data-stu-id="e0798-220">Because the **EXTERNAL** keyword is not used, this statement creates an internal table.</span></span> <span data-ttu-id="e0798-221">La tabla se almacena en el almacenamiento de datos de Hive y Hive la administra por completo.</span><span class="sxs-lookup"><span data-stu-id="e0798-221">The table is stored in the Hive data warehouse and is managed completely by Hive.</span></span>

* <span data-ttu-id="e0798-222">`STORED AS ORC`: almacena los datos en el formato de columnas de filas optimizadas (ORC, Optimized Row Columnar).</span><span class="sxs-lookup"><span data-stu-id="e0798-222">`STORED AS ORC`: Stores the data in Optimized Row Columnar (ORC) format.</span></span> <span data-ttu-id="e0798-223">ORC es un formato altamente optimizado y eficiente para almacenar datos de Hive.</span><span class="sxs-lookup"><span data-stu-id="e0798-223">ORC is a highly optimized and efficient format for storing Hive data.</span></span>

* <span data-ttu-id="e0798-224">`INSERT OVERWRITE ... SELECT`: selecciona filas de la tabla **log4jLogs** que contiene **[ERROR]** y luego inserta los datos en la tabla **errorLogs**.</span><span class="sxs-lookup"><span data-stu-id="e0798-224">`INSERT OVERWRITE ... SELECT`: Selects rows from the **log4jLogs** table that contains **[ERROR]**, and then inserts the data into the **errorLogs** table.</span></span>

> [!NOTE]
> <span data-ttu-id="e0798-225">A diferencia de las tablas externas, la eliminación de una tabla interna también eliminará los datos subyacentes.</span><span class="sxs-lookup"><span data-stu-id="e0798-225">Unlike external tables, dropping an internal table also deletes the underlying data.</span></span>

## <a name="improve-hive-query-performance"></a><span data-ttu-id="e0798-226">Mejora del rendimiento de las consultas de Hive</span><span class="sxs-lookup"><span data-stu-id="e0798-226">Improve Hive query performance</span></span>

### <span data-ttu-id="e0798-227"><a id="usetez"></a>Apache Tez</span><span class="sxs-lookup"><span data-stu-id="e0798-227"><a id="usetez"></a>Apache Tez</span></span>

<span data-ttu-id="e0798-228">[Apache Tez](http://tez.apache.org) es un marco que permite que aplicaciones con uso intensivo de datos, como Hive, se ejecuten con mucha más eficacia a escala.</span><span class="sxs-lookup"><span data-stu-id="e0798-228">[Apache Tez](http://tez.apache.org) is a framework that allows data intensive applications, such as Hive, to run much more efficiently at scale.</span></span> <span data-ttu-id="e0798-229">Tez está habilitado de manera predeterminada para los clústeres de HDInsight basados en Linux.</span><span class="sxs-lookup"><span data-stu-id="e0798-229">Tez is enabled by default for Linux-based HDInsight clusters.</span></span>

> [!NOTE]
> <span data-ttu-id="e0798-230">Tez actualmente está desactivado de forma predeterminada para clústeres de HDInsight basados en Windows y debe estar habilitado.</span><span class="sxs-lookup"><span data-stu-id="e0798-230">Tez is currently off by default for Windows-based HDInsight clusters and it must be enabled.</span></span> <span data-ttu-id="e0798-231">Para aprovechar Tez, debe establecerse el siguiente valor en una consulta de Hive:</span><span class="sxs-lookup"><span data-stu-id="e0798-231">To take advantage of Tez, the following value must be set for a Hive query:</span></span>
>
> `set hive.execution.engine=tez;`
>
> <span data-ttu-id="e0798-232">Tez es el motor predeterminado para clústeres de HDInsight basados en Linux.</span><span class="sxs-lookup"><span data-stu-id="e0798-232">Tez is the default engine for Linux-based HDInsight clusters.</span></span>

<span data-ttu-id="e0798-233">Los [documentos de diseño de Hive en Tez](https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez) incluyen detalles sobre las opciones de implementación y las configuraciones de ajuste.</span><span class="sxs-lookup"><span data-stu-id="e0798-233">The [Hive on Tez design documents](https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez) contains details about the implementation choices and tuning configurations.</span></span>

<span data-ttu-id="e0798-234">Para ayudar a depurar los trabajos que se ejecutaron mediante Tez, HDInsight proporciona las siguientes interfaces de usuario web que le permiten ver los detalles de los trabajos de Tez:</span><span class="sxs-lookup"><span data-stu-id="e0798-234">To aid in debugging jobs ran using Tez, HDInsight provides the following web UIs that allow you to view details of Tez jobs:</span></span>

* [<span data-ttu-id="e0798-235">Use the Ambari Tez view on Linux-based HDInsight</span><span class="sxs-lookup"><span data-stu-id="e0798-235">Use the Ambari Tez view on Linux-based HDInsight</span></span>](hdinsight-debug-ambari-tez-view.md)

* [<span data-ttu-id="e0798-236">Use the Tez UI on Windows-based HDInsight</span><span class="sxs-lookup"><span data-stu-id="e0798-236">Use the Tez UI on Windows-based HDInsight</span></span>](hdinsight-debug-tez-ui.md)

### <a name="low-latency-analytical-processing-llap"></a><span data-ttu-id="e0798-237">Procesamiento analítico de baja latencia (LLAP)</span><span class="sxs-lookup"><span data-stu-id="e0798-237">Low Latency Analytical Processing (LLAP)</span></span>

<span data-ttu-id="e0798-238">[LLAP](https://cwiki.apache.org/confluence/display/Hive/LLAP) (conocido a veces como Larga vida y procesamiento) es una característica nueva de Hive 2.0 que permite el almacenamiento en memoria caché de las consultas.</span><span class="sxs-lookup"><span data-stu-id="e0798-238">[LLAP](https://cwiki.apache.org/confluence/display/Hive/LLAP) (sometimes known as Live Long and Process) is a new feature in Hive 2.0 that allows in-memory caching of queries.</span></span> <span data-ttu-id="e0798-239">LLAP hace que las consultas de Hive sean mucho más rápidas, hasta [26 más que Hive 1.x en algunos casos](https://hortonworks.com/blog/announcing-apache-hive-2-1-25x-faster-queries-much/).</span><span class="sxs-lookup"><span data-stu-id="e0798-239">LLAP makes Hive queries much faster, up to [26x faster than Hive 1.x in some cases](https://hortonworks.com/blog/announcing-apache-hive-2-1-25x-faster-queries-much/).</span></span>

<span data-ttu-id="e0798-240">HDInsight proporciona LLAP en el tipo de clúster Hive interactivo.</span><span class="sxs-lookup"><span data-stu-id="e0798-240">HDInsight provides LLAP in the Interactive Hive cluster type.</span></span> <span data-ttu-id="e0798-241">Para más información, consulte el documento sobre el [inicio con Hive interactivo](hdinsight-hadoop-use-interactive-hive.md).</span><span class="sxs-lookup"><span data-stu-id="e0798-241">For more information, see the [Start with Interactive Hive](hdinsight-hadoop-use-interactive-hive.md) document.</span></span>

## <a name="hive-jobs-and-sql-server-integration-services"></a><span data-ttu-id="e0798-242">Trabajos de Hive y servicios de integración de SQL Server</span><span class="sxs-lookup"><span data-stu-id="e0798-242">Hive jobs and SQL Server Integration Services</span></span>

<span data-ttu-id="e0798-243">Puede usar SQL Server Integration Services (SSIS) para ejecutar un trabajo de Hive.</span><span class="sxs-lookup"><span data-stu-id="e0798-243">You can use SQL Server Integration Services (SSIS) to run a Hive job.</span></span> <span data-ttu-id="e0798-244">El paquete de características de Azure para SSIS proporciona los siguientes componentes que funcionan con trabajos de Hive en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e0798-244">The Azure Feature Pack for SSIS provides the following components that work with Hive jobs on HDInsight.</span></span>

* <span data-ttu-id="e0798-245">[Tarea de Hive de Azure HDInsight][hivetask]</span><span class="sxs-lookup"><span data-stu-id="e0798-245">[Azure HDInsight Hive Task][hivetask]</span></span>

* <span data-ttu-id="e0798-246">[Administrador de conexiones de suscripción de Azure][connectionmanager]</span><span class="sxs-lookup"><span data-stu-id="e0798-246">[Azure Subscription Connection Manager][connectionmanager]</span></span>

<span data-ttu-id="e0798-247">Obtenga más información sobre el paquete de características de Azure para SSIS [aquí][ssispack].</span><span class="sxs-lookup"><span data-stu-id="e0798-247">Learn more about the Azure Feature Pack for SSIS [here][ssispack].</span></span>

## <span data-ttu-id="e0798-248"><a id="nextsteps"></a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e0798-248"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="e0798-249">Ahora que aprendió qué es Hive y cómo usarlo con Hadoop en HDInsight, use los siguientes vínculos para explorar otras formas de trabajar con HDInsight de Azure.</span><span class="sxs-lookup"><span data-stu-id="e0798-249">Now that you've learned what Hive is and how to use it with Hadoop in HDInsight, use the following links to explore other ways to work with Azure HDInsight.</span></span>

* <span data-ttu-id="e0798-250">[Carga de datos en HDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="e0798-250">[Upload data to HDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="e0798-251">[Uso de Pig con HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="e0798-251">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="e0798-252">[Uso de trabajos de MapReduce con HDInsight][hdinsight-use-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="e0798-252">[Use MapReduce jobs with HDInsight][hdinsight-use-mapreduce]</span></span>

[hdinsight-sdk-documentation]: http://msdnstage.redmond.corp.microsoft.com/library/dn479185.aspx

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[apache-tez]: http://tez.apache.org
[apache-hive]: http://hive.apache.org/
[apache-log4j]: http://en.wikipedia.org/wiki/Log4j
[hive-on-tez-wiki]: https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez
[import-to-excel]: http://azure.microsoft.com/documentation/articles/hdinsight-connect-excel-power-query/
[hivetask]: http://msdn.microsoft.com/library/mt146771(v=sql.120).aspx
[connectionmanager]: http://msdn.microsoft.com/library/mt146773(v=sql.120).aspx
[ssispack]: http://msdn.microsoft.com/library/mt146770(v=sql.120).aspx

[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md


[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md

[Powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx


[cindygross-hive-tables]: http://blogs.msdn.com/b/cindygross/archive/2013/02/06/hdinsight-hive-internal-and-external-tables-intro.aspx
