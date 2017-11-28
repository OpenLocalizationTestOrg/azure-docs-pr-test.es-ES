---
title: "Introducción al lenguaje U-SQL | Microsoft Docs"
description: "Conozca los aspectos básicos del lenguaje U-SQL."
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.assetid: 57143396-ab86-47dd-b6f8-613ba28c28d2
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/23/2017
ms.author: saveenr
ms.openlocfilehash: 38c4e1b9bd24ef0b8a81f6154620f3f98d3b5ac1
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-u-sql"></a><span data-ttu-id="0c564-103">Introducción a U-SQL</span><span class="sxs-lookup"><span data-stu-id="0c564-103">Get started with U-SQL</span></span>
<span data-ttu-id="0c564-104">U-SQL es un lenguaje que combina SQL declarativo con C# imperativo para permitirle procesar sus datos a cualquier escala.</span><span class="sxs-lookup"><span data-stu-id="0c564-104">U-SQL is a language that combines declarative SQL with imperative C# to let you process data at any scale.</span></span> <span data-ttu-id="0c564-105">Mediante la funcionalidad de consulta distribuida escalable de U-SQL, puede analizar los datos de manera eficaz entre almacenes relacionales, como Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="0c564-105">Through the scalable, distributed-query capability of U-SQL, you can efficiently analyze data across relational stores such as Azure SQL Database.</span></span> <span data-ttu-id="0c564-106">Con U-SQL, puede procesar los datos no estructurados mediante la aplicación de esquemas en la lectura y la inserción de lógica personalizada y UDF.</span><span class="sxs-lookup"><span data-stu-id="0c564-106">With U-SQL, you can process unstructured data by applying schema on read and inserting custom logic and UDFs.</span></span> <span data-ttu-id="0c564-107">Además, U-SQL incluye extensibilidad que proporciona un control más preciso sobre cómo ejecutarlo a escala.</span><span class="sxs-lookup"><span data-stu-id="0c564-107">Additionally, U-SQL includes extensibility that gives you fine-grained control over how to execute at scale.</span></span> 

## <a name="learning-resources"></a><span data-ttu-id="0c564-108">Recursos de aprendizaje</span><span class="sxs-lookup"><span data-stu-id="0c564-108">Learning resources</span></span>

* <span data-ttu-id="0c564-109">En el [Tutorial de U-SQL](http://aka.ms/usqltutorial) se proporciona un tutorial guiado de la mayor parte del lenguaje U-SQL.</span><span class="sxs-lookup"><span data-stu-id="0c564-109">The [U-SQL Tutorial](http://aka.ms/usqltutorial) provides a guided walkthrough of most of the U-SQL language.</span></span> <span data-ttu-id="0c564-110">Se recomienda leer este documento a todos los desarrolladores que quieran aprender U-SQL.</span><span class="sxs-lookup"><span data-stu-id="0c564-110">This document is recommended reading for all developers wanting to learn U-SQL.</span></span>
* <span data-ttu-id="0c564-111">Para más información sobre la **sintaxis del lenguaje U-SQL**, consulte la [referencia del lenguaje U-SQL](http://go.microsoft.com/fwlink/p/?LinkId=691348).</span><span class="sxs-lookup"><span data-stu-id="0c564-111">For detailed information about the **U-SQL language syntax**, see the [U-SQL Language Reference](http://go.microsoft.com/fwlink/p/?LinkId=691348).</span></span>
* <span data-ttu-id="0c564-112">Para comprender la **filosofía del diseño de U-SQL**, consulte la entrada del blog de Visual Studio [Introducing U-SQL – A Language that makes Big Data Processing Easy](https://blogs.msdn.microsoft.com/visualstudio/2015/09/28/introducing-u-sql-a-language-that-makes-big-data-processing-easy/) (Introducción s U-SQL: un lenguaje que facilita el procesamiento de marcrodatos).</span><span class="sxs-lookup"><span data-stu-id="0c564-112">To understand the **U-SQL design philosophy**, see the Visual Studio blog post [Introducing U-SQL – A Language that makes Big Data Processing Easy](https://blogs.msdn.microsoft.com/visualstudio/2015/09/28/introducing-u-sql-a-language-that-makes-big-data-processing-easy/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0c564-113">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="0c564-113">Prerequisites</span></span>

<span data-ttu-id="0c564-114">Antes de examinar los ejemplos de U-SQL de este documento, lea y realice el [Tutorial: Desarrollo de scripts U-SQL mediante Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="0c564-114">Before you go through the U-SQL samples in this document, read and complete [Tutorial: Develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span> <span data-ttu-id="0c564-115">En este tutorial se explican los mecanismos de uso de U-SQL con Herramientas de Azure Data Lake para Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0c564-115">That tutorial explains the mechanics of using U-SQL with Azure Data Lake Tools for Visual Studio.</span></span>

## <a name="your-first-u-sql-script"></a><span data-ttu-id="0c564-116">El primer script U-SQL</span><span class="sxs-lookup"><span data-stu-id="0c564-116">Your first U-SQL script</span></span>

<span data-ttu-id="0c564-117">El siguiente script U-SQL es sencillo y nos permite explorar muchos aspectos del lenguaje U-SQL.</span><span class="sxs-lookup"><span data-stu-id="0c564-117">The following U-SQL script is simple and lets us explore many aspects the U-SQL language.</span></span>

```
@searchlog =
    EXTRACT UserId          int,
            Start           DateTime,
            Region          string,
            Query           string,
            Duration        int?,
            Urls            string,
            ClickedUrls     string
    FROM "/Samples/Data/SearchLog.tsv"
    USING Extractors.Tsv();

OUTPUT @searchlog   
    TO "/output/SearchLog-first-u-sql.csv"
    USING Outputters.Csv();
```

<span data-ttu-id="0c564-118">Este script no contiene ningún paso de transformación.</span><span class="sxs-lookup"><span data-stu-id="0c564-118">This script doesn't have any transformation steps.</span></span> <span data-ttu-id="0c564-119">Lee el archivo de origen llamado `SearchLog.tsv`, lo esquematiza y vuelve a escribir el conjunto de filas en un archivo llamado SearchLog-first-u-sql.csv.</span><span class="sxs-lookup"><span data-stu-id="0c564-119">It reads from the source file called `SearchLog.tsv`, schematizes it, and writes the rowset back into a file called SearchLog-first-u-sql.csv.</span></span>

<span data-ttu-id="0c564-120">Observe el signo de interrogación junto al tipo de datos en el campo `Duration`.</span><span class="sxs-lookup"><span data-stu-id="0c564-120">Notice the question mark next to the data type in the `Duration` field.</span></span> <span data-ttu-id="0c564-121">Esto significa que el campo `Duration` podría ser nulo.</span><span class="sxs-lookup"><span data-stu-id="0c564-121">It means that the `Duration` field could be null.</span></span>

### <a name="key-concepts"></a><span data-ttu-id="0c564-122">Conceptos clave</span><span class="sxs-lookup"><span data-stu-id="0c564-122">Key concepts</span></span>
* <span data-ttu-id="0c564-123">**Variables de conjunto de filas**: cada expresión de consulta que produce un conjunto de filas se puede asignar a una variable.</span><span class="sxs-lookup"><span data-stu-id="0c564-123">**Rowset variables**: Each query expression that produces a rowset can be assigned to a variable.</span></span> <span data-ttu-id="0c564-124">U-SQL sigue el patrón de nomenclatura de variables de T-SQL (`@searchlog`, por ejemplo) en el script.</span><span class="sxs-lookup"><span data-stu-id="0c564-124">U-SQL follows the T-SQL variable naming pattern (`@searchlog`, for example) in the script.</span></span>
* <span data-ttu-id="0c564-125">La palabra clave **EXTRACT** lee los datos de un archivo y define el esquema en la lectura.</span><span class="sxs-lookup"><span data-stu-id="0c564-125">The **EXTRACT** keyword reads data from a file and defines the schema on read.</span></span> <span data-ttu-id="0c564-126">`Extractors.Tsv` es un extractor de U-SQL integrado para archivos de valores separados por tabulación.</span><span class="sxs-lookup"><span data-stu-id="0c564-126">`Extractors.Tsv` is a built-in U-SQL extractor for tab-separated-value files.</span></span> <span data-ttu-id="0c564-127">Puede desarrollar extractores personalizados.</span><span class="sxs-lookup"><span data-stu-id="0c564-127">You can develop custom extractors.</span></span>
* <span data-ttu-id="0c564-128">**OUTPUT** escribe datos de un conjunto de filas en un archivo.</span><span class="sxs-lookup"><span data-stu-id="0c564-128">The **OUTPUT** writes data from a rowset to a file.</span></span> <span data-ttu-id="0c564-129">`Outputters.Csv()` es un outputter U-SQL integrado para crear un archivo de valores separados por coma.</span><span class="sxs-lookup"><span data-stu-id="0c564-129">`Outputters.Csv()` is a built-in U-SQL outputter to create a comma-separated-value file.</span></span> <span data-ttu-id="0c564-130">También puede desarrollar outputters personalizados.</span><span class="sxs-lookup"><span data-stu-id="0c564-130">You can develop custom outputters.</span></span>

### <a name="file-paths"></a><span data-ttu-id="0c564-131">Rutas de acceso de archivo</span><span class="sxs-lookup"><span data-stu-id="0c564-131">File paths</span></span>

<span data-ttu-id="0c564-132">Las instrucciones EXTRACT y OUTPUT usan rutas de acceso de archivo.</span><span class="sxs-lookup"><span data-stu-id="0c564-132">The EXTRACT and OUTPUT statements use file paths.</span></span> <span data-ttu-id="0c564-133">Las rutas de acceso de archivo puede ser absolutas o relativas:</span><span class="sxs-lookup"><span data-stu-id="0c564-133">File paths can be absolute or relative:</span></span>

<span data-ttu-id="0c564-134">La siguiente ruta de acceso absoluta de archivo hace referencia a un archivo de Data Lake Store denominado `mystore`:</span><span class="sxs-lookup"><span data-stu-id="0c564-134">This following absolute file path refers to a file in a Data Lake Store named `mystore`:</span></span>

    adl://mystore.azuredatalakestore.net/Samples/Data/SearchLog.tsv

<span data-ttu-id="0c564-135">La siguiente ruta de acceso relativa de archivo comienza con `"/"`.</span><span class="sxs-lookup"><span data-stu-id="0c564-135">This following file path starts with `"/"`.</span></span> <span data-ttu-id="0c564-136">Hace referencia a un archivo en la cuenta de Data Lake Store predeterminada:</span><span class="sxs-lookup"><span data-stu-id="0c564-136">It refers to a file in the default Data Lake Store account:</span></span>

    /output/SearchLog-first-u-sql.csv

## <a name="use-scalar-variables"></a><span data-ttu-id="0c564-137">Uso de variables escalares</span><span class="sxs-lookup"><span data-stu-id="0c564-137">Use scalar variables</span></span>

<span data-ttu-id="0c564-138">Puede usar variables escalares para facilitar el mantenimiento del script.</span><span class="sxs-lookup"><span data-stu-id="0c564-138">You can use scalar variables as well to make your script maintenance easier.</span></span> <span data-ttu-id="0c564-139">El script de U-SQL anterior también se puede escribir como:</span><span class="sxs-lookup"><span data-stu-id="0c564-139">The previous U-SQL script can also be written as:</span></span>

    DECLARE @in  string = "/Samples/Data/SearchLog.tsv";
    DECLARE @out string = "/output/SearchLog-scalar-variables.csv";

    @searchlog =
        EXTRACT UserId          int,
                Start           DateTime,
                Region          string,
                Query           string,
                Duration        int?,
                Urls            string,
                ClickedUrls     string
        FROM @in
        USING Extractors.Tsv();

    OUTPUT @searchlog   
        TO @out
        USING Outputters.Csv();

## <a name="transform-rowsets"></a><span data-ttu-id="0c564-140">Transformación de conjuntos de filas</span><span class="sxs-lookup"><span data-stu-id="0c564-140">Transform rowsets</span></span>

<span data-ttu-id="0c564-141">Use **SELECT** para transformar conjuntos de filas:</span><span class="sxs-lookup"><span data-stu-id="0c564-141">Use **SELECT** to transform rowsets:</span></span>

    @searchlog =
        EXTRACT UserId          int,
                Start           DateTime,
                Region          string,
                Query           string,
                Duration        int?,
                Urls            string,
                ClickedUrls     string
        FROM "/Samples/Data/SearchLog.tsv"
        USING Extractors.Tsv();

    @rs1 =
        SELECT Start, Region, Duration
        FROM @searchlog
    WHERE Region == "en-gb";

    OUTPUT @rs1   
        TO "/output/SearchLog-transform-rowsets.csv"
        USING Outputters.Csv();

<span data-ttu-id="0c564-142">La cláusula WHERE usa una [expresión booleana de C#](https://msdn.microsoft.com/library/6a71f45d.aspx).</span><span class="sxs-lookup"><span data-stu-id="0c564-142">The WHERE clause uses a [C# Boolean expression](https://msdn.microsoft.com/library/6a71f45d.aspx).</span></span> <span data-ttu-id="0c564-143">Puede usar el lenguaje de expresiones de C# para crear sus propias expresiones y funciones.</span><span class="sxs-lookup"><span data-stu-id="0c564-143">You can use the C# expression language to do your own expressions and functions.</span></span> <span data-ttu-id="0c564-144">Incluso puede realizar un filtrado más complejo si las combina con conjunciones (AND) y disyunciones (OR) lógicas.</span><span class="sxs-lookup"><span data-stu-id="0c564-144">You can even perform more complex filtering by combining them with logical conjunctions (ANDs) and disjunctions (ORs).</span></span>

<span data-ttu-id="0c564-145">El siguiente script usa el método DateTime.Parse() y una conjunción.</span><span class="sxs-lookup"><span data-stu-id="0c564-145">The following script uses the DateTime.Parse() method and a conjunction.</span></span>

    @searchlog =
        EXTRACT UserId          int,
                Start           DateTime,
                Region          string,
                Query           string,
                Duration        int?,
                Urls            string,
                ClickedUrls     string
        FROM "/Samples/Data/SearchLog.tsv"
        USING Extractors.Tsv();

    @rs1 =
        SELECT Start, Region, Duration
        FROM @searchlog
    WHERE Region == "en-gb";

    @rs1 =
        SELECT Start, Region, Duration
        FROM @rs1
        WHERE Start >= DateTime.Parse("2012/02/16") AND Start <= DateTime.Parse("2012/02/17");

    OUTPUT @rs1   
        TO "/output/SearchLog-transform-datetime.csv"
        USING Outputters.Csv();

 >[!NOTE]
 ><span data-ttu-id="0c564-146">La segunda consulta opera con el resultado del primer conjunto de filas, que crea una composición de ambos filtros.</span><span class="sxs-lookup"><span data-stu-id="0c564-146">The second query is operating on the result of the first rowset, which creates a composite of the two filters.</span></span> <span data-ttu-id="0c564-147">También puede volver a usar un nombre de variable y los nombres tienen un ámbito léxico.</span><span class="sxs-lookup"><span data-stu-id="0c564-147">You can also reuse a variable name, and the names are scoped lexically.</span></span>

## <a name="aggregate-rowsets"></a><span data-ttu-id="0c564-148">Conjuntos de filas agregados</span><span class="sxs-lookup"><span data-stu-id="0c564-148">Aggregate rowsets</span></span>
<span data-ttu-id="0c564-149">U-SQL proporciona las conocidas cláusulas ORDER BY, GROUP BY y agregaciones.</span><span class="sxs-lookup"><span data-stu-id="0c564-149">U-SQL gives you the familiar ORDER BY, GROUP BY, and aggregations.</span></span>

<span data-ttu-id="0c564-150">La siguiente consulta busca la duración total por región y después muestra las cinco duraciones principales de forma ordenada.</span><span class="sxs-lookup"><span data-stu-id="0c564-150">The following query finds the total duration per region, and then displays the top five durations in order.</span></span>

<span data-ttu-id="0c564-151">Los conjuntos de filas de U-SQL no conservan el orden en la siguiente consulta.</span><span class="sxs-lookup"><span data-stu-id="0c564-151">U-SQL rowsets do not preserve their order for the next query.</span></span> <span data-ttu-id="0c564-152">Por lo tanto, para ordenar los resultados, necesita agregar ORDER BY a la instrucción OUTPUT:</span><span class="sxs-lookup"><span data-stu-id="0c564-152">Thus, to order an output, you need to add ORDER BY to the OUTPUT statement:</span></span>

    DECLARE @outpref string = "/output/Searchlog-aggregation";
    DECLARE @out1    string = @outpref+"_agg.csv";
    DECLARE @out2    string = @outpref+"_top5agg.csv";

    @searchlog =
        EXTRACT UserId          int,
                Start           DateTime,
                Region          string,
                Query           string,
                Duration        int?,
                Urls            string,
                ClickedUrls     string
        FROM "/Samples/Data/SearchLog.tsv"
        USING Extractors.Tsv();

    @rs1 =
        SELECT
            Region,
            SUM(Duration) AS TotalDuration
        FROM @searchlog
    GROUP BY Region;

    @res =
        SELECT *
        FROM @rs1
        ORDER BY TotalDuration DESC
        FETCH 5 ROWS;

    OUTPUT @rs1
        TO @out1
        ORDER BY TotalDuration DESC
        USING Outputters.Csv();

    OUTPUT @res
        TO @out2
        ORDER BY TotalDuration DESC
        USING Outputters.Csv();

<span data-ttu-id="0c564-153">La cláusula ORDER BY de The U-SQL requiere el uso de la cláusula FETCH en una expresión SELECT.</span><span class="sxs-lookup"><span data-stu-id="0c564-153">The U-SQL ORDER BY clause requires using the FETCH clause in a SELECT expression.</span></span>

<span data-ttu-id="0c564-154">La cláusula HAVING de U-SQL puede usarse para restringir los resultados a los grupos que cumplan la condición HAVING:</span><span class="sxs-lookup"><span data-stu-id="0c564-154">The U-SQL HAVING clause can be used to restrict the output to groups that satisfy the HAVING condition:</span></span>

    @searchlog =
        EXTRACT UserId          int,
                Start           DateTime,
                Region          string,
                Query           string,
                Duration        int?,
                Urls            string,
                ClickedUrls     string
        FROM "/Samples/Data/SearchLog.tsv"
        USING Extractors.Tsv();

    @res =
        SELECT
            Region,
            SUM(Duration) AS TotalDuration
        FROM @searchlog
        GROUP BY Region
        HAVING SUM(Duration) > 200;

    OUTPUT @res
        TO "/output/Searchlog-having.csv"
        ORDER BY TotalDuration DESC
        USING Outputters.Csv();

<span data-ttu-id="0c564-155">Para escenarios avanzados de agregación, consulte la documentación de referencia de U-SQL para [agregar, analizar y hacer referencia a funciones](https://msdn.microsoft.com/en-us/library/azure/mt621335.aspx)</span><span class="sxs-lookup"><span data-stu-id="0c564-155">For advanced aggregation scenarios, see the The U-SQL reference documentation for [aggregate, analytic, and reference functions](https://msdn.microsoft.com/en-us/library/azure/mt621335.aspx)</span></span>

## <a name="next-steps"></a><span data-ttu-id="0c564-156">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0c564-156">Next steps</span></span>
* [<span data-ttu-id="0c564-157">Información general de Análisis de Microsoft Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="0c564-157">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="0c564-158">Desarrollo de scripts de U-SQL mediante Data Lake Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0c564-158">Develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
