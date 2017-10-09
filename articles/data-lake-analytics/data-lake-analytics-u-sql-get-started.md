---
title: "Introducción al lenguaje U-SQL | Microsoft Docs"
description: "Obtenga información acerca de conceptos básicos de Hola de hello lenguaje SQL U."
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
ms.openlocfilehash: 5edee0e0d85211e84b3d47895c53d71f0a19f083
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-u-sql"></a><span data-ttu-id="2f067-103">Introducción a U-SQL</span><span class="sxs-lookup"><span data-stu-id="2f067-103">Get started with U-SQL</span></span>
<span data-ttu-id="2f067-104">U-SQL es un lenguaje que combina SQL declarativa con imperativo C# toolet procesar datos a cualquier escala.</span><span class="sxs-lookup"><span data-stu-id="2f067-104">U-SQL is a language that combines declarative SQL with imperative C# toolet you process data at any scale.</span></span> <span data-ttu-id="2f067-105">A través de hello escalable, consultas distribuidas capacidad de U-SQL, puede analizar eficazmente datos en almacenes relacionales como base de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="2f067-105">Through hello scalable, distributed-query capability of U-SQL, you can efficiently analyze data across relational stores such as Azure SQL Database.</span></span> <span data-ttu-id="2f067-106">Con U-SQL, puede procesar los datos no estructurados mediante la aplicación de esquemas en la lectura y la inserción de lógica personalizada y UDF.</span><span class="sxs-lookup"><span data-stu-id="2f067-106">With U-SQL, you can process unstructured data by applying schema on read and inserting custom logic and UDFs.</span></span> <span data-ttu-id="2f067-107">Además, SQL U incluye extensibilidad que proporciona control más preciso sobre cómo tooexecute a escala.</span><span class="sxs-lookup"><span data-stu-id="2f067-107">Additionally, U-SQL includes extensibility that gives you fine-grained control over how tooexecute at scale.</span></span> 

## <a name="learning-resources"></a><span data-ttu-id="2f067-108">Recursos de aprendizaje</span><span class="sxs-lookup"><span data-stu-id="2f067-108">Learning resources</span></span>

* <span data-ttu-id="2f067-109">Hola [U-SQL Tutorial](http://aka.ms/usqltutorial) proporciona un tutorial guiado de la mayoría de lenguaje de hello U-SQL.</span><span class="sxs-lookup"><span data-stu-id="2f067-109">hello [U-SQL Tutorial](http://aka.ms/usqltutorial) provides a guided walkthrough of most of hello U-SQL language.</span></span> <span data-ttu-id="2f067-110">Este documento se recomienda leer para todos los desarrolladores que deseen toolearn U-SQL.</span><span class="sxs-lookup"><span data-stu-id="2f067-110">This document is recommended reading for all developers wanting toolearn U-SQL.</span></span>
* <span data-ttu-id="2f067-111">Para obtener información detallada acerca de hello **sintaxis del lenguaje SQL U**, vea hello [referencia del lenguaje SQL U](http://go.microsoft.com/fwlink/p/?LinkId=691348).</span><span class="sxs-lookup"><span data-stu-id="2f067-111">For detailed information about hello **U-SQL language syntax**, see hello [U-SQL Language Reference](http://go.microsoft.com/fwlink/p/?LinkId=691348).</span></span>
* <span data-ttu-id="2f067-112">Hola toounderstand **filosofía de diseño de U-SQL**, consulte blog de Visual Studio de hello [Introducción U-SQL: un lenguaje que facilita tanto de procesamiento de datos grande](https://blogs.msdn.microsoft.com/visualstudio/2015/09/28/introducing-u-sql-a-language-that-makes-big-data-processing-easy/).</span><span class="sxs-lookup"><span data-stu-id="2f067-112">toounderstand hello **U-SQL design philosophy**, see hello Visual Studio blog post [Introducing U-SQL – A Language that makes Big Data Processing Easy](https://blogs.msdn.microsoft.com/visualstudio/2015/09/28/introducing-u-sql-a-language-that-makes-big-data-processing-easy/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2f067-113">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="2f067-113">Prerequisites</span></span>

<span data-ttu-id="2f067-114">Antes de ir a través de ejemplos de hello U-SQL en este documento, lea y siga [Tutorial: scripts U T-SQL desarrollar con Data Lake Tools para Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="2f067-114">Before you go through hello U-SQL samples in this document, read and complete [Tutorial: Develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span> <span data-ttu-id="2f067-115">Este tutorial explica mecánica de Hola de con SQL U con Azure Data Lake Tools para Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2f067-115">That tutorial explains hello mechanics of using U-SQL with Azure Data Lake Tools for Visual Studio.</span></span>

## <a name="your-first-u-sql-script"></a><span data-ttu-id="2f067-116">El primer script U-SQL</span><span class="sxs-lookup"><span data-stu-id="2f067-116">Your first U-SQL script</span></span>

<span data-ttu-id="2f067-117">Hola siguiente secuencia de comandos SQL U es sencillo y nos permite explorar muchos aspectos hello U-SQL lenguaje.</span><span class="sxs-lookup"><span data-stu-id="2f067-117">hello following U-SQL script is simple and lets us explore many aspects hello U-SQL language.</span></span>

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
    too"/output/SearchLog-first-u-sql.csv"
    USING Outputters.Csv();
```

<span data-ttu-id="2f067-118">Este script no contiene ningún paso de transformación.</span><span class="sxs-lookup"><span data-stu-id="2f067-118">This script doesn't have any transformation steps.</span></span> <span data-ttu-id="2f067-119">Lee del archivo de origen de hello denominada `SearchLog.tsv`, schematizes y vuelve a escribir el conjunto de filas de hello en un archivo denominado SearchLog-first-u-sql.csv.</span><span class="sxs-lookup"><span data-stu-id="2f067-119">It reads from hello source file called `SearchLog.tsv`, schematizes it, and writes hello rowset back into a file called SearchLog-first-u-sql.csv.</span></span>

<span data-ttu-id="2f067-120">Observe el tipo de datos toohello inmediatamente de Hola de signo de interrogación en hello `Duration` campo.</span><span class="sxs-lookup"><span data-stu-id="2f067-120">Notice hello question mark next toohello data type in hello `Duration` field.</span></span> <span data-ttu-id="2f067-121">Significa que hello `Duration` campo podría ser null.</span><span class="sxs-lookup"><span data-stu-id="2f067-121">It means that hello `Duration` field could be null.</span></span>

### <a name="key-concepts"></a><span data-ttu-id="2f067-122">Conceptos clave</span><span class="sxs-lookup"><span data-stu-id="2f067-122">Key concepts</span></span>
* <span data-ttu-id="2f067-123">**Variables de conjunto de filas**: cada expresión de consulta que genera un conjunto de filas se puede asignar tooa variable.</span><span class="sxs-lookup"><span data-stu-id="2f067-123">**Rowset variables**: Each query expression that produces a rowset can be assigned tooa variable.</span></span> <span data-ttu-id="2f067-124">U-SQL sigue el modelo de nomenclatura de variables de hello T-SQL (`@searchlog`, por ejemplo) en el script de Hola.</span><span class="sxs-lookup"><span data-stu-id="2f067-124">U-SQL follows hello T-SQL variable naming pattern (`@searchlog`, for example) in hello script.</span></span>
* <span data-ttu-id="2f067-125">Hola **extraer** palabra clave lee datos de un archivo y define el esquema de hello en la lectura.</span><span class="sxs-lookup"><span data-stu-id="2f067-125">hello **EXTRACT** keyword reads data from a file and defines hello schema on read.</span></span> <span data-ttu-id="2f067-126">`Extractors.Tsv` es un extractor de U-SQL integrado para archivos de valores separados por tabulación.</span><span class="sxs-lookup"><span data-stu-id="2f067-126">`Extractors.Tsv` is a built-in U-SQL extractor for tab-separated-value files.</span></span> <span data-ttu-id="2f067-127">Puede desarrollar extractores personalizados.</span><span class="sxs-lookup"><span data-stu-id="2f067-127">You can develop custom extractors.</span></span>
* <span data-ttu-id="2f067-128">Hola **salida** escribe datos desde un archivo de tooa de conjunto de filas.</span><span class="sxs-lookup"><span data-stu-id="2f067-128">hello **OUTPUT** writes data from a rowset tooa file.</span></span> <span data-ttu-id="2f067-129">`Outputters.Csv()`es un toocreate de outputter U-SQL integrada en un archivo de valores separados por comas.</span><span class="sxs-lookup"><span data-stu-id="2f067-129">`Outputters.Csv()` is a built-in U-SQL outputter toocreate a comma-separated-value file.</span></span> <span data-ttu-id="2f067-130">También puede desarrollar outputters personalizados.</span><span class="sxs-lookup"><span data-stu-id="2f067-130">You can develop custom outputters.</span></span>

### <a name="file-paths"></a><span data-ttu-id="2f067-131">Rutas de acceso de archivo</span><span class="sxs-lookup"><span data-stu-id="2f067-131">File paths</span></span>

<span data-ttu-id="2f067-132">Hola extraer e instrucciones de salida usan rutas de acceso de archivo.</span><span class="sxs-lookup"><span data-stu-id="2f067-132">hello EXTRACT and OUTPUT statements use file paths.</span></span> <span data-ttu-id="2f067-133">Las rutas de acceso de archivo puede ser absolutas o relativas:</span><span class="sxs-lookup"><span data-stu-id="2f067-133">File paths can be absolute or relative:</span></span>

<span data-ttu-id="2f067-134">Esta ruta de acceso absoluta del archivo siguiente hace referencia a archivos tooa en un almacén de Data Lake denominado `mystore`:</span><span class="sxs-lookup"><span data-stu-id="2f067-134">This following absolute file path refers tooa file in a Data Lake Store named `mystore`:</span></span>

    adl://mystore.azuredatalakestore.net/Samples/Data/SearchLog.tsv

<span data-ttu-id="2f067-135">La siguiente ruta de acceso relativa de archivo comienza con `"/"`.</span><span class="sxs-lookup"><span data-stu-id="2f067-135">This following file path starts with `"/"`.</span></span> <span data-ttu-id="2f067-136">Hace referencia archivo tooa en la cuenta de almacén de Data Lake Hola predeterminada:</span><span class="sxs-lookup"><span data-stu-id="2f067-136">It refers tooa file in hello default Data Lake Store account:</span></span>

    /output/SearchLog-first-u-sql.csv

## <a name="use-scalar-variables"></a><span data-ttu-id="2f067-137">Uso de variables escalares</span><span class="sxs-lookup"><span data-stu-id="2f067-137">Use scalar variables</span></span>

<span data-ttu-id="2f067-138">Puede usar variables escalares como toomake y el mantenimiento de la secuencia de comandos sea más fácil.</span><span class="sxs-lookup"><span data-stu-id="2f067-138">You can use scalar variables as well toomake your script maintenance easier.</span></span> <span data-ttu-id="2f067-139">script de Hola anterior U SQL también puede escribirse como:</span><span class="sxs-lookup"><span data-stu-id="2f067-139">hello previous U-SQL script can also be written as:</span></span>

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
        too@out
        USING Outputters.Csv();

## <a name="transform-rowsets"></a><span data-ttu-id="2f067-140">Transformación de conjuntos de filas</span><span class="sxs-lookup"><span data-stu-id="2f067-140">Transform rowsets</span></span>

<span data-ttu-id="2f067-141">Use **seleccione** tootransform conjuntos de filas:</span><span class="sxs-lookup"><span data-stu-id="2f067-141">Use **SELECT** tootransform rowsets:</span></span>

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
        too"/output/SearchLog-transform-rowsets.csv"
        USING Outputters.Csv();

<span data-ttu-id="2f067-142">Hola de cláusula WHERE utiliza un [expresión C# booleana](https://msdn.microsoft.com/library/6a71f45d.aspx).</span><span class="sxs-lookup"><span data-stu-id="2f067-142">hello WHERE clause uses a [C# Boolean expression](https://msdn.microsoft.com/library/6a71f45d.aspx).</span></span> <span data-ttu-id="2f067-143">Puede usar Hola C# expresión lenguaje toodo sus propias expresiones y funciones.</span><span class="sxs-lookup"><span data-stu-id="2f067-143">You can use hello C# expression language toodo your own expressions and functions.</span></span> <span data-ttu-id="2f067-144">Incluso puede realizar un filtrado más complejo si las combina con conjunciones (AND) y disyunciones (OR) lógicas.</span><span class="sxs-lookup"><span data-stu-id="2f067-144">You can even perform more complex filtering by combining them with logical conjunctions (ANDs) and disjunctions (ORs).</span></span>

<span data-ttu-id="2f067-145">Hello siguiente secuencia de comandos utiliza hello DateTime.Parse() método y una conjunción.</span><span class="sxs-lookup"><span data-stu-id="2f067-145">hello following script uses hello DateTime.Parse() method and a conjunction.</span></span>

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
        too"/output/SearchLog-transform-datetime.csv"
        USING Outputters.Csv();

 >[!NOTE]
 ><span data-ttu-id="2f067-146">segunda consulta de Hello está en funcionamiento en el resultado de hello de hello primer conjunto de filas, que crea un compuesto de hello dos filtros.</span><span class="sxs-lookup"><span data-stu-id="2f067-146">hello second query is operating on hello result of hello first rowset, which creates a composite of hello two filters.</span></span> <span data-ttu-id="2f067-147">También puede volver a usar un nombre de variable y nombres de hello léxicamente tienen como ámbito.</span><span class="sxs-lookup"><span data-stu-id="2f067-147">You can also reuse a variable name, and hello names are scoped lexically.</span></span>

## <a name="aggregate-rowsets"></a><span data-ttu-id="2f067-148">Conjuntos de filas agregados</span><span class="sxs-lookup"><span data-stu-id="2f067-148">Aggregate rowsets</span></span>
<span data-ttu-id="2f067-149">Deja de U-SQL Hola familiarizado ORDER BY, GROUP BY y las agregaciones.</span><span class="sxs-lookup"><span data-stu-id="2f067-149">U-SQL gives you hello familiar ORDER BY, GROUP BY, and aggregations.</span></span>

<span data-ttu-id="2f067-150">Hello siguiente consulta busca duración total de Hola por región y, a continuación, muestra superior Hola cinco duraciones en orden.</span><span class="sxs-lookup"><span data-stu-id="2f067-150">hello following query finds hello total duration per region, and then displays hello top five durations in order.</span></span>

<span data-ttu-id="2f067-151">Conjuntos de filas de U-SQL no conservan el orden de consulta siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="2f067-151">U-SQL rowsets do not preserve their order for hello next query.</span></span> <span data-ttu-id="2f067-152">Por lo tanto, tooorder una salida, necesita tooadd ORDER BY toohello salida instrucción:</span><span class="sxs-lookup"><span data-stu-id="2f067-152">Thus, tooorder an output, you need tooadd ORDER BY toohello OUTPUT statement:</span></span>

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
        too@out1
        ORDER BY TotalDuration DESC
        USING Outputters.Csv();

    OUTPUT @res
        too@out2
        ORDER BY TotalDuration DESC
        USING Outputters.Csv();

<span data-ttu-id="2f067-153">Hola SQL U ORDER BY cláusula requiere el uso de cláusula de captura de hello en una expresión SELECT.</span><span class="sxs-lookup"><span data-stu-id="2f067-153">hello U-SQL ORDER BY clause requires using hello FETCH clause in a SELECT expression.</span></span>

<span data-ttu-id="2f067-154">cláusula de Hello U-SQL tener puede ser usado toorestrict Hola salida toogroups que satisfacen la condición de hello HAVING:</span><span class="sxs-lookup"><span data-stu-id="2f067-154">hello U-SQL HAVING clause can be used toorestrict hello output toogroups that satisfy hello HAVING condition:</span></span>

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
        too"/output/Searchlog-having.csv"
        ORDER BY TotalDuration DESC
        USING Outputters.Csv();

<span data-ttu-id="2f067-155">Para escenarios avanzados de agregación, consulte la documentación de referencia de hello U-SQL de Hola para [agregar, analítica y hacer referencia a funciones](https://msdn.microsoft.com/en-us/library/azure/mt621335.aspx)</span><span class="sxs-lookup"><span data-stu-id="2f067-155">For advanced aggregation scenarios, see hello hello U-SQL reference documentation for [aggregate, analytic, and reference functions](https://msdn.microsoft.com/en-us/library/azure/mt621335.aspx)</span></span>

## <a name="next-steps"></a><span data-ttu-id="2f067-156">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2f067-156">Next steps</span></span>
* [<span data-ttu-id="2f067-157">Información general de Análisis de Microsoft Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="2f067-157">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="2f067-158">Desarrollo de scripts de U-SQL mediante Data Lake Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2f067-158">Develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
