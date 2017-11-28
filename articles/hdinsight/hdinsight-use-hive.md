---
title: aaaWhat es Apache Hive y HiveQL - HDInsight de Azure | Documentos de Microsoft
description: "Apache Hive es un sistema de almacenamiento de datos para Hadoop. Puede consultar los datos almacenados en el subárbol usando HiveQL, qué similar tooTransact-SQL. En este documento, obtenga información acerca de cómo toouse Hive y HiveQL con HDInsight de Azure."
keywords: "hiveql, ¿qué es hive, hiveql hadoop, cómo toouse hive, obtenga información acerca de hive, ¿qué es el subárbol"
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
ms.openlocfilehash: a2772312263895ff99b499898264c2e6d5e816e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-apache-hive-and-hiveql-on-azure-hdinsight"></a><span data-ttu-id="07a2e-106">¿Qué son Apache Hive y HiveQL en Azure HDInsight?</span><span class="sxs-lookup"><span data-stu-id="07a2e-106">What is Apache Hive and HiveQL on Azure HDInsight?</span></span>

<span data-ttu-id="07a2e-107">[Apache Hive](http://hive.apache.org/) es un sistema de almacenamiento de datos para Hadoop.</span><span class="sxs-lookup"><span data-stu-id="07a2e-107">[Apache Hive](http://hive.apache.org/) is a data warehouse system for Hadoop.</span></span> <span data-ttu-id="07a2e-108">Hive hace posibles el resumen de los datos, las consultas y el análisis de datos.</span><span class="sxs-lookup"><span data-stu-id="07a2e-108">Hive enables data summarization, querying, and analysis of data.</span></span> <span data-ttu-id="07a2e-109">HiveQL, que es un tooSQL similar de lenguaje de consulta que se escriben consultas de Hive.</span><span class="sxs-lookup"><span data-stu-id="07a2e-109">Hive queries are written in HiveQL, which is a query language similar tooSQL.</span></span>

<span data-ttu-id="07a2e-110">Subárbol permite tooproject estructura de datos no estructurados en gran medida.</span><span class="sxs-lookup"><span data-stu-id="07a2e-110">Hive allows you tooproject structure on largely unstructured data.</span></span> <span data-ttu-id="07a2e-111">Después de definir la estructura de hello, puede usar datos de saludo de HiveQL tooquery sin conocimiento de Java o MapReduce.</span><span class="sxs-lookup"><span data-stu-id="07a2e-111">After you define hello structure, you can use HiveQL tooquery hello data without knowledge of Java or MapReduce.</span></span>

<span data-ttu-id="07a2e-112">HDInsight proporciona varios tipos de clúster, que están optimizados para cargas de trabajo específicas.</span><span class="sxs-lookup"><span data-stu-id="07a2e-112">HDInsight provides several cluster types, which are tuned for specific workloads.</span></span> <span data-ttu-id="07a2e-113">Hola siguientes tipos de clúster se suelen usar para consultas de Hive:</span><span class="sxs-lookup"><span data-stu-id="07a2e-113">hello following cluster types are most often used for Hive queries:</span></span>

* <span data-ttu-id="07a2e-114">__Subárbol interactivo__: Hadoop de un clúster que proporciona [baja latencia analíticos procesamiento (LLAP)](https://cwiki.apache.org/confluence/display/Hive/LLAP) tiempos de respuesta de tooimprove de funcionalidad para realizar consultas interactivas.</span><span class="sxs-lookup"><span data-stu-id="07a2e-114">__Interactive Hive__: A Hadoop cluster that provides [Low Latency Analytical Processing (LLAP)](https://cwiki.apache.org/confluence/display/Hive/LLAP) functionality tooimprove response times for interactive queries.</span></span> <span data-ttu-id="07a2e-115">Para obtener más información, vea hello [iniciar con interactivo de Hive en HDInsight](hdinsight-hadoop-use-interactive-hive.md) documento.</span><span class="sxs-lookup"><span data-stu-id="07a2e-115">For more information, see hello [Start with Interactive Hive in HDInsight](hdinsight-hadoop-use-interactive-hive.md) document.</span></span>

* <span data-ttu-id="07a2e-116">__Hadoop__: un clúster de Hadoop que está optimizado para cargas de trabajo de procesamiento por lotes.</span><span class="sxs-lookup"><span data-stu-id="07a2e-116">__Hadoop__: A Hadoop cluster that is tuned for batch processing workloads.</span></span> <span data-ttu-id="07a2e-117">Para obtener más información, vea hello [iniciar con Hadoop en HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md) documento.</span><span class="sxs-lookup"><span data-stu-id="07a2e-117">For more information, see hello [Start with Hadoop in HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md) document.</span></span>

* <span data-ttu-id="07a2e-118">__Spark__: Apache Spark tiene funcionalidad integrada para trabajar con Hive.</span><span class="sxs-lookup"><span data-stu-id="07a2e-118">__Spark__: Apache Spark has built-in functionality for working with Hive.</span></span> <span data-ttu-id="07a2e-119">Para obtener más información, vea hello [iniciar con Spark en HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md) documento.</span><span class="sxs-lookup"><span data-stu-id="07a2e-119">For more information, see hello [Start with Spark on HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md) document.</span></span>

* <span data-ttu-id="07a2e-120">__HBase__: HiveQL puede ser tooquery usa los datos almacenados en HBase.</span><span class="sxs-lookup"><span data-stu-id="07a2e-120">__HBase__: HiveQL can be used tooquery data stored in HBase.</span></span> <span data-ttu-id="07a2e-121">Para obtener más información, vea hello [iniciar con HBase en HDInsight](hdinsight-hbase-tutorial-get-started-linux.md) documento.</span><span class="sxs-lookup"><span data-stu-id="07a2e-121">For more information, see hello [Start with HBase on HDInsight](hdinsight-hbase-tutorial-get-started-linux.md) document.</span></span>

## <a name="how-toouse-hive"></a><span data-ttu-id="07a2e-122">¿Cómo toouse Hive</span><span class="sxs-lookup"><span data-stu-id="07a2e-122">How toouse Hive</span></span>

<span data-ttu-id="07a2e-123">Usar hello después toodiscover tabla cómo toouse Hive con HDInsight:</span><span class="sxs-lookup"><span data-stu-id="07a2e-123">Use hello following table toodiscover how toouse Hive with HDInsight:</span></span>

| <span data-ttu-id="07a2e-124">**Use este método** si desea…</span><span class="sxs-lookup"><span data-stu-id="07a2e-124">**Use this method** if you want...</span></span> | <span data-ttu-id="07a2e-125">...un shell **interactivo**</span><span class="sxs-lookup"><span data-stu-id="07a2e-125">...an **interactive** shell</span></span> | <span data-ttu-id="07a2e-126">...procesamiento por**lotes**</span><span class="sxs-lookup"><span data-stu-id="07a2e-126">...**batch** processing</span></span> | <span data-ttu-id="07a2e-127">...con este **sistema operativo de clúster**</span><span class="sxs-lookup"><span data-stu-id="07a2e-127">...with this **cluster operating system**</span></span> | <span data-ttu-id="07a2e-128">...desde este **sistema operativo de cliente**</span><span class="sxs-lookup"><span data-stu-id="07a2e-128">...from this **client operating system**</span></span> |
|:--- |:---:|:---:|:--- |:--- |
| [<span data-ttu-id="07a2e-129">Vista de Hive</span><span class="sxs-lookup"><span data-stu-id="07a2e-129">Hive View</span></span>](hdinsight-hadoop-use-hive-ambari-view.md) |<span data-ttu-id="07a2e-130">✔</span><span class="sxs-lookup"><span data-stu-id="07a2e-130">✔</span></span> |<span data-ttu-id="07a2e-131">✔</span><span class="sxs-lookup"><span data-stu-id="07a2e-131">✔</span></span> |<span data-ttu-id="07a2e-132">Linux</span><span class="sxs-lookup"><span data-stu-id="07a2e-132">Linux</span></span> |<span data-ttu-id="07a2e-133">Cualquiera (en función del explorador)</span><span class="sxs-lookup"><span data-stu-id="07a2e-133">Any (browser based)</span></span> |
| [<span data-ttu-id="07a2e-134">Cliente Beeline</span><span class="sxs-lookup"><span data-stu-id="07a2e-134">Beeline client</span></span>](hdinsight-hadoop-use-hive-beeline.md) |<span data-ttu-id="07a2e-135">✔</span><span class="sxs-lookup"><span data-stu-id="07a2e-135">✔</span></span> |<span data-ttu-id="07a2e-136">✔</span><span class="sxs-lookup"><span data-stu-id="07a2e-136">✔</span></span> |<span data-ttu-id="07a2e-137">Linux</span><span class="sxs-lookup"><span data-stu-id="07a2e-137">Linux</span></span> |<span data-ttu-id="07a2e-138">Linux, Unix, Mac OS X o Windows</span><span class="sxs-lookup"><span data-stu-id="07a2e-138">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="07a2e-139">API DE REST</span><span class="sxs-lookup"><span data-stu-id="07a2e-139">REST API</span></span>](hdinsight-hadoop-use-hive-curl.md) |&nbsp; |<span data-ttu-id="07a2e-140">✔</span><span class="sxs-lookup"><span data-stu-id="07a2e-140">✔</span></span> |<span data-ttu-id="07a2e-141">Linux o Windows*</span><span class="sxs-lookup"><span data-stu-id="07a2e-141">Linux or Windows*</span></span> |<span data-ttu-id="07a2e-142">Linux, Unix, Mac OS X o Windows</span><span class="sxs-lookup"><span data-stu-id="07a2e-142">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="07a2e-143">Herramientas de HDInsight para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="07a2e-143">HDInsight tools for Visual Studio</span></span>](hdinsight-hadoop-use-hive-visual-studio.md) |&nbsp; |<span data-ttu-id="07a2e-144">✔</span><span class="sxs-lookup"><span data-stu-id="07a2e-144">✔</span></span> |<span data-ttu-id="07a2e-145">Linux o Windows*</span><span class="sxs-lookup"><span data-stu-id="07a2e-145">Linux or Windows*</span></span> |<span data-ttu-id="07a2e-146">Windows</span><span class="sxs-lookup"><span data-stu-id="07a2e-146">Windows</span></span> |
| [<span data-ttu-id="07a2e-147">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="07a2e-147">Windows PowerShell</span></span>](hdinsight-hadoop-use-hive-powershell.md) |&nbsp; |<span data-ttu-id="07a2e-148">✔</span><span class="sxs-lookup"><span data-stu-id="07a2e-148">✔</span></span> |<span data-ttu-id="07a2e-149">Linux o Windows*</span><span class="sxs-lookup"><span data-stu-id="07a2e-149">Linux or Windows*</span></span> |<span data-ttu-id="07a2e-150">Windows</span><span class="sxs-lookup"><span data-stu-id="07a2e-150">Windows</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="07a2e-151">\*Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior.</span><span class="sxs-lookup"><span data-stu-id="07a2e-151">\* Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="07a2e-152">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="07a2e-152">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="07a2e-153">Si está usando un clúster de HDInsight basados en Windows, puede usar hello [consola de consultas](hdinsight-hadoop-use-hive-query-console.md) desde el explorador o [escritorio remoto](hdinsight-hadoop-use-hive-remote-desktop.md) toorun consultas de Hive.</span><span class="sxs-lookup"><span data-stu-id="07a2e-153">If you are using a Windows-based HDInsight cluster, you can use hello [Query console](hdinsight-hadoop-use-hive-query-console.md) from your browser or [Remote Desktop](hdinsight-hadoop-use-hive-remote-desktop.md) toorun Hive queries.</span></span>

## <a name="hiveql-language-reference"></a><span data-ttu-id="07a2e-154">Referencia del lenguaje HiveQL</span><span class="sxs-lookup"><span data-stu-id="07a2e-154">HiveQL language reference</span></span>

<span data-ttu-id="07a2e-155">Referencia del lenguaje de HiveQL está disponible en hello [manual del lenguaje (https://cwiki.apache.org/confluence/display/Hive/LanguageManual)](https://cwiki.apache.org/confluence/display/Hive/LanguageManual).</span><span class="sxs-lookup"><span data-stu-id="07a2e-155">HiveQL language reference is available in hello [language manual (https://cwiki.apache.org/confluence/display/Hive/LanguageManual)](https://cwiki.apache.org/confluence/display/Hive/LanguageManual).</span></span>

## <a name="hive-and-data-structure"></a><span data-ttu-id="07a2e-156">Hive y estructura de datos</span><span class="sxs-lookup"><span data-stu-id="07a2e-156">Hive and data structure</span></span>

<span data-ttu-id="07a2e-157">Subárbol entiende cómo toowork con estructura y datos semiestructurados.</span><span class="sxs-lookup"><span data-stu-id="07a2e-157">Hive understands how toowork with structured and semi-structured data.</span></span> <span data-ttu-id="07a2e-158">Por ejemplo, texto los archivos donde los campos de hello están delimitados por caracteres específicos.</span><span class="sxs-lookup"><span data-stu-id="07a2e-158">For example, text files where hello fields are delimited by specific characters.</span></span> <span data-ttu-id="07a2e-159">Hola sigue HiveQL instrucción crea una tabla con datos delimitados por espacios:</span><span class="sxs-lookup"><span data-stu-id="07a2e-159">hello following HiveQL statement creates a table over space-delimited data:</span></span>

```hiveql
CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
STORED AS TEXTFILE LOCATION '/example/data/';
```

<span data-ttu-id="07a2e-160">Hive también admite **serializador/deserializadores (SerDe)** personalizados para datos estructurados irregularmente o complejos.</span><span class="sxs-lookup"><span data-stu-id="07a2e-160">Hive also supports custom **serializer/deserializers (SerDe)** for complex or irregularly structured data.</span></span> <span data-ttu-id="07a2e-161">Para obtener más información, vea hello [cómo toouse una SerDe de JSON personalizada con HDInsight](http://blogs.msdn.com/b/bigdatasupport/archive/2014/06/18/how-to-use-a-custom-json-serde-with-microsoft-azure-hdinsight.aspx) documento.</span><span class="sxs-lookup"><span data-stu-id="07a2e-161">For more information, see hello [How toouse a custom JSON SerDe with HDInsight](http://blogs.msdn.com/b/bigdatasupport/archive/2014/06/18/how-to-use-a-custom-json-serde-with-microsoft-azure-hdinsight.aspx) document.</span></span>

<span data-ttu-id="07a2e-162">Para obtener más información sobre formatos de archivo compatibles con Hive, consulte hello [manual del lenguaje (https://cwiki.apache.org/confluence/display/Hive/LanguageManual)](https://cwiki.apache.org/confluence/display/Hive/LanguageManual)</span><span class="sxs-lookup"><span data-stu-id="07a2e-162">For more information on file formats supported by Hive, see hello [Language manual (https://cwiki.apache.org/confluence/display/Hive/LanguageManual)](https://cwiki.apache.org/confluence/display/Hive/LanguageManual)</span></span>

## <a name="hive-internal-tables-vs-external-tables"></a><span data-ttu-id="07a2e-163">Tablas internas frente a tablas externas de Hive.</span><span class="sxs-lookup"><span data-stu-id="07a2e-163">Hive internal tables vs external tables</span></span>

<span data-ttu-id="07a2e-164">Hay dos tipos de tablas que puede crear con Hive:</span><span class="sxs-lookup"><span data-stu-id="07a2e-164">There are two types of tables that you can create with Hive:</span></span>

* <span data-ttu-id="07a2e-165">__Interno__: datos se almacenan en el almacén de datos de Hive Hola.</span><span class="sxs-lookup"><span data-stu-id="07a2e-165">__Internal__: Data is stored in hello Hive data warehouse.</span></span> <span data-ttu-id="07a2e-166">Hello almacenamiento de datos se encuentra en `/hive/warehouse/` en el almacenamiento predeterminado Hola clúster Hola.</span><span class="sxs-lookup"><span data-stu-id="07a2e-166">hello data warehouse is located at `/hive/warehouse/` on hello default storage for hello cluster.</span></span>

    <span data-ttu-id="07a2e-167">Use tablas internas cuando:</span><span class="sxs-lookup"><span data-stu-id="07a2e-167">Use internal tables when:</span></span>

    * <span data-ttu-id="07a2e-168">Los datos sean temporales.</span><span class="sxs-lookup"><span data-stu-id="07a2e-168">Data is temporary.</span></span>
    * <span data-ttu-id="07a2e-169">Desea que el ciclo de vida de Hive toomanage Hola de tabla de Hola y de datos.</span><span class="sxs-lookup"><span data-stu-id="07a2e-169">You want Hive toomanage hello lifecycle of hello table and data.</span></span>

* <span data-ttu-id="07a2e-170">__Externo__: los datos se almacenan fuera de almacenamiento de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="07a2e-170">__External__: Data is stored outside hello data warehouse.</span></span> <span data-ttu-id="07a2e-171">datos de Hello pueden almacenarse en cualquier almacenamiento accesible por clúster Hola.</span><span class="sxs-lookup"><span data-stu-id="07a2e-171">hello data can be stored on any storage accessible by hello cluster.</span></span>

    <span data-ttu-id="07a2e-172">Use tablas externas cuando:</span><span class="sxs-lookup"><span data-stu-id="07a2e-172">Use external tables when:</span></span>

    * <span data-ttu-id="07a2e-173">datos de Hello también se utilizan fuera de Hive.</span><span class="sxs-lookup"><span data-stu-id="07a2e-173">hello data is also used outside of Hive.</span></span> <span data-ttu-id="07a2e-174">Por ejemplo, se actualizan los archivos de datos de Hola por otro proceso (que no bloquea los archivos de Hola.)</span><span class="sxs-lookup"><span data-stu-id="07a2e-174">For example, hello data files are updated by another process (that does not lock hello files.)</span></span>
    * <span data-ttu-id="07a2e-175">Los datos tienen tooremain Hola subyacente ubicación, incluso después de quitar tabla Hola.</span><span class="sxs-lookup"><span data-stu-id="07a2e-175">Data needs tooremain in hello underlying location, even after dropping hello table.</span></span>
    * <span data-ttu-id="07a2e-176">Necesite una ubicación personalizada, como una cuenta de almacenamiento no predeterminada.</span><span class="sxs-lookup"><span data-stu-id="07a2e-176">You need a custom location, such as a non-default storage account.</span></span>
    * <span data-ttu-id="07a2e-177">Un programa distinto de hive administra etcetera, la ubicación, el formato de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="07a2e-177">A program other than hive manages hello data format, location, etc.</span></span>

<span data-ttu-id="07a2e-178">Para obtener más información, vea hello [Hive internos y externos preliminar tablas] [ cindygross-hive-tables] entrada de blog.</span><span class="sxs-lookup"><span data-stu-id="07a2e-178">For more information, see hello [Hive Internal and External Tables Intro][cindygross-hive-tables] blog post.</span></span>

## <a name="user-defined-functions-udf"></a><span data-ttu-id="07a2e-179">Funciones definidas por el usuario (UDF)</span><span class="sxs-lookup"><span data-stu-id="07a2e-179">User-defined functions (UDF)</span></span>

<span data-ttu-id="07a2e-180">Hive también puede extenderse a través de **funciones definidas por el usuario (UDF)**.</span><span class="sxs-lookup"><span data-stu-id="07a2e-180">Hive can also be extended through **user-defined functions (UDF)**.</span></span> <span data-ttu-id="07a2e-181">Una UDF permite la funcionalidad de tooimplement o lógica que no está modelada fácilmente en HiveQL.</span><span class="sxs-lookup"><span data-stu-id="07a2e-181">A UDF allows you tooimplement functionality or logic that isn't easily modeled in HiveQL.</span></span> <span data-ttu-id="07a2e-182">Para obtener un ejemplo del uso de UDF con Hive, vea Hola siguientes documentos:</span><span class="sxs-lookup"><span data-stu-id="07a2e-182">For an example of using UDFs with Hive, see hello following documents:</span></span>

* [<span data-ttu-id="07a2e-183">Utilización de una función definida por el usuario de Java con Hive</span><span class="sxs-lookup"><span data-stu-id="07a2e-183">Use a Java user-defined function with Hive</span></span>](hdinsight-hadoop-hive-java-udf.md)

* [<span data-ttu-id="07a2e-184">Uso de funciones definidas por el usuario (UDF) de Python con Hive y Pig</span><span class="sxs-lookup"><span data-stu-id="07a2e-184">Use a Python user-defined function with Hive and Pig</span></span>](hdinsight-python.md)

* [<span data-ttu-id="07a2e-185">Uso de funciones definidas por el usuario de C# con Hive y Pig</span><span class="sxs-lookup"><span data-stu-id="07a2e-185">Use a C# user-defined function with Hive and Pig</span></span>](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)

* [<span data-ttu-id="07a2e-186">Cómo funcionan las tooHDInsight tooadd un subárbol personalizado definido por el usuario</span><span class="sxs-lookup"><span data-stu-id="07a2e-186">How tooadd a custom Hive user-defined function tooHDInsight</span></span>](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/14/how-to-add-custom-hive-udfs-to-hdinsight.aspx)

* [<span data-ttu-id="07a2e-187">Marca de tiempo de tooHive da formato a una subárbol ejemplo función definida por el usuario tooconvert fecha y hora</span><span class="sxs-lookup"><span data-stu-id="07a2e-187">An example Hive user-defined function tooconvert date/time formats tooHive timestamp</span></span>](https://github.com/Azure-Samples/hdinsight-java-hive-udf)

## <span data-ttu-id="07a2e-188"><a id="data"></a>Datos de ejemplo</span><span class="sxs-lookup"><span data-stu-id="07a2e-188"><a id="data"></a>Example data</span></span>

<span data-ttu-id="07a2e-189">Hive en HDInsight tiene ya cargada una tabla interna denominada `hivesampletable`.</span><span class="sxs-lookup"><span data-stu-id="07a2e-189">Hive on HDInsight comes pre-loaded with an internal table named `hivesampletable`.</span></span> <span data-ttu-id="07a2e-190">Además, HDInsight proporciona conjuntos de datos de ejemplo que se pueden usar con Hive.</span><span class="sxs-lookup"><span data-stu-id="07a2e-190">HDInsight also provides example data sets that can be used with Hive.</span></span> <span data-ttu-id="07a2e-191">Estos conjuntos de datos se almacenan en hello `/example/data` y `/HdiSamples` directorios.</span><span class="sxs-lookup"><span data-stu-id="07a2e-191">These data sets are stored in hello `/example/data` and `/HdiSamples` directories.</span></span> <span data-ttu-id="07a2e-192">Estos directorios existen en el almacenamiento predeterminado de hello para el clúster.</span><span class="sxs-lookup"><span data-stu-id="07a2e-192">These directories exist in hello default storage for your cluster.</span></span>

## <span data-ttu-id="07a2e-193"><a id="job"></a>Ejemplo de consulta de Hive</span><span class="sxs-lookup"><span data-stu-id="07a2e-193"><a id="job"></a>Example Hive query</span></span>

<span data-ttu-id="07a2e-194">Hola después de las columnas del proyecto de instrucciones de HiveQL en hello `/example/data/sample.log` archivo:</span><span class="sxs-lookup"><span data-stu-id="07a2e-194">hello following HiveQL statements project columns onto hello `/example/data/sample.log` file:</span></span>

    set hive.execution.engine=tez;
    DROP TABLE log4jLogs;
    CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
    STORED AS TEXTFILE LOCATION '/example/data/';
    SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

<span data-ttu-id="07a2e-195">En el ejemplo anterior de hello, instrucciones de HiveQL Hola realizan Hola siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="07a2e-195">In hello previous example, hello HiveQL statements perform hello following actions:</span></span>

* <span data-ttu-id="07a2e-196">`set hive.execution.engine=tez;`: Conjuntos Hola toouse de motor de ejecución Tez.</span><span class="sxs-lookup"><span data-stu-id="07a2e-196">`set hive.execution.engine=tez;`: Sets hello execution engine toouse Tez.</span></span> <span data-ttu-id="07a2e-197">Si se utiliza Tez en lugar de MapReduce, se puede mejorar el rendimiento de las consultas.</span><span class="sxs-lookup"><span data-stu-id="07a2e-197">Using Tez instead of MapReduce can provide an increase in query performance.</span></span> <span data-ttu-id="07a2e-198">Para obtener más información sobre Tez, vea hello [Tez de Apache de uso para mejorar el rendimiento](#usetez) sección.</span><span class="sxs-lookup"><span data-stu-id="07a2e-198">For more information on Tez, see hello [Use Apache Tez for improved performance](#usetez) section.</span></span>

    > [!NOTE]
    > <span data-ttu-id="07a2e-199">Esta instrucción solo se requiere cuando se usa un clúster de HDInsight basado en Windows.</span><span class="sxs-lookup"><span data-stu-id="07a2e-199">This statement is only required when using a Windows-based HDInsight cluster.</span></span> <span data-ttu-id="07a2e-200">Tez es el motor de ejecución predeterminado de Hola de HDInsight basados en Linux.</span><span class="sxs-lookup"><span data-stu-id="07a2e-200">Tez is hello default execution engine for Linux-based HDInsight.</span></span>

* <span data-ttu-id="07a2e-201">`DROP TABLE`: Si ya existe una tabla de hello, elimínelo.</span><span class="sxs-lookup"><span data-stu-id="07a2e-201">`DROP TABLE`: If hello table already exists, delete it.</span></span>

* <span data-ttu-id="07a2e-202">`CREATE EXTERNAL TABLE`: crea una tabla **externa** en Hive.</span><span class="sxs-lookup"><span data-stu-id="07a2e-202">`CREATE EXTERNAL TABLE`: Creates a new **external** table in Hive.</span></span> <span data-ttu-id="07a2e-203">Tablas externas solo almacenan definición de la tabla de hello en el subárbol.</span><span class="sxs-lookup"><span data-stu-id="07a2e-203">External tables only store hello table definition in Hive.</span></span> <span data-ttu-id="07a2e-204">Hola datos permanecen en la ubicación original de Hola y en formato original Hola.</span><span class="sxs-lookup"><span data-stu-id="07a2e-204">hello data is left in hello original location and in hello original format.</span></span>

* <span data-ttu-id="07a2e-205">`ROW FORMAT`: Indica cómo se da formato a los datos de Hola de Hive.</span><span class="sxs-lookup"><span data-stu-id="07a2e-205">`ROW FORMAT`: Tells Hive how hello data is formatted.</span></span> <span data-ttu-id="07a2e-206">En este caso, los campos de hello en cada registro están separados por un espacio.</span><span class="sxs-lookup"><span data-stu-id="07a2e-206">In this case, hello fields in each log are separated by a space.</span></span>

* <span data-ttu-id="07a2e-207">`STORED AS TEXTFILE LOCATION`: Indica Hive donde hello se almacenan los datos (hello `example/data` directorio) y que se almacena como texto.</span><span class="sxs-lookup"><span data-stu-id="07a2e-207">`STORED AS TEXTFILE LOCATION`: Tells Hive where hello data is stored (hello `example/data` directory) and that it is stored as text.</span></span> <span data-ttu-id="07a2e-208">datos Hola pueden estar en un archivo o distribuir en varios archivos en el directorio de Hola.</span><span class="sxs-lookup"><span data-stu-id="07a2e-208">hello data can be in one file or spread across multiple files within hello directory.</span></span>

* <span data-ttu-id="07a2e-209">`SELECT`: Selecciona un recuento de todas las filas donde hello columna **t4** contiene el valor de hello **[ERROR]**.</span><span class="sxs-lookup"><span data-stu-id="07a2e-209">`SELECT`: Selects a count of all rows where hello column **t4** contains hello value **[ERROR]**.</span></span> <span data-ttu-id="07a2e-210">Esta instrucción devuelve un valor de **3** porque hay tres filas que contienen este valor.</span><span class="sxs-lookup"><span data-stu-id="07a2e-210">This statement returns a value of **3** because there are three rows that contain this value.</span></span>

* <span data-ttu-id="07a2e-211">`INPUT__FILE__NAME LIKE '%.log'`-Subárbol intenta tooapply Hola esquema tooall archivos hello del directorio.</span><span class="sxs-lookup"><span data-stu-id="07a2e-211">`INPUT__FILE__NAME LIKE '%.log'` - Hive attempts tooapply hello schema tooall files in hello directory.</span></span> <span data-ttu-id="07a2e-212">En este caso, el directorio de hello contiene archivos que no coinciden con el esquema de Hola.</span><span class="sxs-lookup"><span data-stu-id="07a2e-212">In this case, hello directory contains files that do not match hello schema.</span></span> <span data-ttu-id="07a2e-213">tooprevent los datos de elementos no utilizados en los resultados de hello, esta instrucción indica Hive que solo debemos devolver datos de archivos que finalizan con. registro.</span><span class="sxs-lookup"><span data-stu-id="07a2e-213">tooprevent garbage data in hello results, this statement tells Hive that we should only return data from files ending in .log.</span></span>

> [!NOTE]
> <span data-ttu-id="07a2e-214">Tablas externas deben utilizarse cuando se espera Hola subyacente datos toobe actualizado a través de un origen externo.</span><span class="sxs-lookup"><span data-stu-id="07a2e-214">External tables should be used when you expect hello underlying data toobe updated by an external source.</span></span> <span data-ttu-id="07a2e-215">Por ejemplo, un proceso de carga de datos automatizado o una operación de MapReduce.</span><span class="sxs-lookup"><span data-stu-id="07a2e-215">For example, an automated data upload process, or MapReduce operation.</span></span>
>
> <span data-ttu-id="07a2e-216">Quitar una tabla externa **no** eliminar datos de hello, sólo elimina la definición de la tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="07a2e-216">Dropping an external table does **not** delete hello data, it only deletes hello table definition.</span></span>

<span data-ttu-id="07a2e-217">toocreate una **interno** tablas en lugar de externas, utilice Hola después de HiveQL:</span><span class="sxs-lookup"><span data-stu-id="07a2e-217">toocreate an **internal** table instead of external, use hello following HiveQL:</span></span>

    set hive.execution.engine=tez;
    CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    STORED AS ORC;
    INSERT OVERWRITE TABLE errorLogs
    SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]';

<span data-ttu-id="07a2e-218">Estas instrucciones realizan Hola siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="07a2e-218">These statements perform hello following actions:</span></span>

* <span data-ttu-id="07a2e-219">`CREATE TABLE IF NOT EXISTS`: Si la tabla hello no existe, créela.</span><span class="sxs-lookup"><span data-stu-id="07a2e-219">`CREATE TABLE IF NOT EXISTS`: If hello table does not exist, create it.</span></span> <span data-ttu-id="07a2e-220">Dado que hello **externo** no se utiliza la palabra clave, esta instrucción crea una tabla interna.</span><span class="sxs-lookup"><span data-stu-id="07a2e-220">Because hello **EXTERNAL** keyword is not used, this statement creates an internal table.</span></span> <span data-ttu-id="07a2e-221">tabla de Hola se almacena en el almacén de datos de Hive de Hola y se administra completamente por el subárbol.</span><span class="sxs-lookup"><span data-stu-id="07a2e-221">hello table is stored in hello Hive data warehouse and is managed completely by Hive.</span></span>

* <span data-ttu-id="07a2e-222">`STORED AS ORC`: Almacena los datos de hello en formato de fila de optimizado columnas (ORC).</span><span class="sxs-lookup"><span data-stu-id="07a2e-222">`STORED AS ORC`: Stores hello data in Optimized Row Columnar (ORC) format.</span></span> <span data-ttu-id="07a2e-223">ORC es un formato altamente optimizado y eficiente para almacenar datos de Hive.</span><span class="sxs-lookup"><span data-stu-id="07a2e-223">ORC is a highly optimized and efficient format for storing Hive data.</span></span>

* <span data-ttu-id="07a2e-224">`INSERT OVERWRITE ... SELECT`: Selecciona las filas de hello **log4jLogs** tabla que contiene **[ERROR]**, y, a continuación, inserta Hola datos en hello **registros de errores de** tabla.</span><span class="sxs-lookup"><span data-stu-id="07a2e-224">`INSERT OVERWRITE ... SELECT`: Selects rows from hello **log4jLogs** table that contains **[ERROR]**, and then inserts hello data into hello **errorLogs** table.</span></span>

> [!NOTE]
> <span data-ttu-id="07a2e-225">A diferencia de las tablas externas, quitar una tabla interna también elimina los datos subyacentes de Hola.</span><span class="sxs-lookup"><span data-stu-id="07a2e-225">Unlike external tables, dropping an internal table also deletes hello underlying data.</span></span>

## <a name="improve-hive-query-performance"></a><span data-ttu-id="07a2e-226">Mejora del rendimiento de las consultas de Hive</span><span class="sxs-lookup"><span data-stu-id="07a2e-226">Improve Hive query performance</span></span>

### <span data-ttu-id="07a2e-227"><a id="usetez"></a>Apache Tez</span><span class="sxs-lookup"><span data-stu-id="07a2e-227"><a id="usetez"></a>Apache Tez</span></span>

<span data-ttu-id="07a2e-228">[Apache Tez](http://tez.apache.org) es un marco que permite a las aplicaciones de uso intensivo de datos, como Hive, toorun mucho más eficazmente a escala.</span><span class="sxs-lookup"><span data-stu-id="07a2e-228">[Apache Tez](http://tez.apache.org) is a framework that allows data intensive applications, such as Hive, toorun much more efficiently at scale.</span></span> <span data-ttu-id="07a2e-229">Tez está habilitado de manera predeterminada para los clústeres de HDInsight basados en Linux.</span><span class="sxs-lookup"><span data-stu-id="07a2e-229">Tez is enabled by default for Linux-based HDInsight clusters.</span></span>

> [!NOTE]
> <span data-ttu-id="07a2e-230">Tez actualmente está desactivado de forma predeterminada para clústeres de HDInsight basados en Windows y debe estar habilitado.</span><span class="sxs-lookup"><span data-stu-id="07a2e-230">Tez is currently off by default for Windows-based HDInsight clusters and it must be enabled.</span></span> <span data-ttu-id="07a2e-231">tootake aprovechar Tez, Hola siguiente valor se debe establecer para una consulta de Hive:</span><span class="sxs-lookup"><span data-stu-id="07a2e-231">tootake advantage of Tez, hello following value must be set for a Hive query:</span></span>
>
> `set hive.execution.engine=tez;`
>
> <span data-ttu-id="07a2e-232">Tez es motor predeterminado de Hola para clústeres de HDInsight basados en Linux.</span><span class="sxs-lookup"><span data-stu-id="07a2e-232">Tez is hello default engine for Linux-based HDInsight clusters.</span></span>

<span data-ttu-id="07a2e-233">Hola [Hive en documentos de diseño de Tez](https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez) contiene detalles sobre las opciones de implementación de Hola y las configuraciones de optimización.</span><span class="sxs-lookup"><span data-stu-id="07a2e-233">hello [Hive on Tez design documents](https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez) contains details about hello implementation choices and tuning configurations.</span></span>

<span data-ttu-id="07a2e-234">tooaid en la depuración de trabajos se ejecutó con Tez, HDInsight proporciona Hola siguientes interfaces de usuario web que le permiten tooview detalles de los trabajos de Tez:</span><span class="sxs-lookup"><span data-stu-id="07a2e-234">tooaid in debugging jobs ran using Tez, HDInsight provides hello following web UIs that allow you tooview details of Tez jobs:</span></span>

* [<span data-ttu-id="07a2e-235">Usar hello vista Ambari Tez en HDInsight basados en Linux</span><span class="sxs-lookup"><span data-stu-id="07a2e-235">Use hello Ambari Tez view on Linux-based HDInsight</span></span>](hdinsight-debug-ambari-tez-view.md)

* [<span data-ttu-id="07a2e-236">Usar hello Tez UI en HDInsight basados en Windows</span><span class="sxs-lookup"><span data-stu-id="07a2e-236">Use hello Tez UI on Windows-based HDInsight</span></span>](hdinsight-debug-tez-ui.md)

### <a name="low-latency-analytical-processing-llap"></a><span data-ttu-id="07a2e-237">Procesamiento analítico de baja latencia (LLAP)</span><span class="sxs-lookup"><span data-stu-id="07a2e-237">Low Latency Analytical Processing (LLAP)</span></span>

<span data-ttu-id="07a2e-238">[LLAP](https://cwiki.apache.org/confluence/display/Hive/LLAP) (conocido a veces como Larga vida y procesamiento) es una característica nueva de Hive 2.0 que permite el almacenamiento en memoria caché de las consultas.</span><span class="sxs-lookup"><span data-stu-id="07a2e-238">[LLAP](https://cwiki.apache.org/confluence/display/Hive/LLAP) (sometimes known as Live Long and Process) is a new feature in Hive 2.0 that allows in-memory caching of queries.</span></span> <span data-ttu-id="07a2e-239">LLAP hace mucho más rápido, seguridad de consultas de Hive demasiado[x 26 más rápidamente de Hive 1.x en algunos casos](https://hortonworks.com/blog/announcing-apache-hive-2-1-25x-faster-queries-much/).</span><span class="sxs-lookup"><span data-stu-id="07a2e-239">LLAP makes Hive queries much faster, up too[26x faster than Hive 1.x in some cases](https://hortonworks.com/blog/announcing-apache-hive-2-1-25x-faster-queries-much/).</span></span>

<span data-ttu-id="07a2e-240">HDInsight proporciona LLAP Hola Hive interactivo tipo de clúster.</span><span class="sxs-lookup"><span data-stu-id="07a2e-240">HDInsight provides LLAP in hello Interactive Hive cluster type.</span></span> <span data-ttu-id="07a2e-241">Para obtener más información, vea hello [iniciar con Hive interactivo](hdinsight-hadoop-use-interactive-hive.md) documento.</span><span class="sxs-lookup"><span data-stu-id="07a2e-241">For more information, see hello [Start with Interactive Hive](hdinsight-hadoop-use-interactive-hive.md) document.</span></span>

## <a name="hive-jobs-and-sql-server-integration-services"></a><span data-ttu-id="07a2e-242">Trabajos de Hive y servicios de integración de SQL Server</span><span class="sxs-lookup"><span data-stu-id="07a2e-242">Hive jobs and SQL Server Integration Services</span></span>

<span data-ttu-id="07a2e-243">Puede utilizar SQL Server Integration Services (SSIS) toorun un trabajo de Hive.</span><span class="sxs-lookup"><span data-stu-id="07a2e-243">You can use SQL Server Integration Services (SSIS) toorun a Hive job.</span></span> <span data-ttu-id="07a2e-244">Hola Feature Pack de Azure para SSIS proporciona Hola trabajan con trabajos de Hive en HDInsight de los componentes siguientes.</span><span class="sxs-lookup"><span data-stu-id="07a2e-244">hello Azure Feature Pack for SSIS provides hello following components that work with Hive jobs on HDInsight.</span></span>

* <span data-ttu-id="07a2e-245">[Tarea de Hive de Azure HDInsight][hivetask]</span><span class="sxs-lookup"><span data-stu-id="07a2e-245">[Azure HDInsight Hive Task][hivetask]</span></span>

* <span data-ttu-id="07a2e-246">[Administrador de conexiones de suscripción de Azure][connectionmanager]</span><span class="sxs-lookup"><span data-stu-id="07a2e-246">[Azure Subscription Connection Manager][connectionmanager]</span></span>

<span data-ttu-id="07a2e-247">Obtener más información sobre Hola Feature Pack de Azure para SSIS [aquí][ssispack].</span><span class="sxs-lookup"><span data-stu-id="07a2e-247">Learn more about hello Azure Feature Pack for SSIS [here][ssispack].</span></span>

## <span data-ttu-id="07a2e-248"><a id="nextsteps"></a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="07a2e-248"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="07a2e-249">Ahora que ha aprendido Novedades de Hive y cómo toouse con Hadoop en HDInsight, Hola de uso siguiente vincula tooexplore otro toowork maneras con HDInsight de Azure.</span><span class="sxs-lookup"><span data-stu-id="07a2e-249">Now that you've learned what Hive is and how toouse it with Hadoop in HDInsight, use hello following links tooexplore other ways toowork with Azure HDInsight.</span></span>

* <span data-ttu-id="07a2e-250">[Cargar datos tooHDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="07a2e-250">[Upload data tooHDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="07a2e-251">[Uso de Pig con HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="07a2e-251">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="07a2e-252">[Uso de trabajos de MapReduce con HDInsight][hdinsight-use-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="07a2e-252">[Use MapReduce jobs with HDInsight][hdinsight-use-mapreduce]</span></span>

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
