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
# <a name="get-started-with-u-sql"></a>Introducción a U-SQL
U-SQL es un lenguaje que combina SQL declarativa con imperativo C# toolet procesar datos a cualquier escala. A través de hello escalable, consultas distribuidas capacidad de U-SQL, puede analizar eficazmente datos en almacenes relacionales como base de datos de SQL Azure. Con U-SQL, puede procesar los datos no estructurados mediante la aplicación de esquemas en la lectura y la inserción de lógica personalizada y UDF. Además, SQL U incluye extensibilidad que proporciona control más preciso sobre cómo tooexecute a escala. 

## <a name="learning-resources"></a>Recursos de aprendizaje

* Hola [U-SQL Tutorial](http://aka.ms/usqltutorial) proporciona un tutorial guiado de la mayoría de lenguaje de hello U-SQL. Este documento se recomienda leer para todos los desarrolladores que deseen toolearn U-SQL.
* Para obtener información detallada acerca de hello **sintaxis del lenguaje SQL U**, vea hello [referencia del lenguaje SQL U](http://go.microsoft.com/fwlink/p/?LinkId=691348).
* Hola toounderstand **filosofía de diseño de U-SQL**, consulte blog de Visual Studio de hello [Introducción U-SQL: un lenguaje que facilita tanto de procesamiento de datos grande](https://blogs.msdn.microsoft.com/visualstudio/2015/09/28/introducing-u-sql-a-language-that-makes-big-data-processing-easy/).

## <a name="prerequisites"></a>Requisitos previos

Antes de ir a través de ejemplos de hello U-SQL en este documento, lea y siga [Tutorial: scripts U T-SQL desarrollar con Data Lake Tools para Visual Studio](data-lake-analytics-data-lake-tools-get-started.md). Este tutorial explica mecánica de Hola de con SQL U con Azure Data Lake Tools para Visual Studio.

## <a name="your-first-u-sql-script"></a>El primer script U-SQL

Hola siguiente secuencia de comandos SQL U es sencillo y nos permite explorar muchos aspectos hello U-SQL lenguaje.

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

Este script no contiene ningún paso de transformación. Lee del archivo de origen de hello denominada `SearchLog.tsv`, schematizes y vuelve a escribir el conjunto de filas de hello en un archivo denominado SearchLog-first-u-sql.csv.

Observe el tipo de datos toohello inmediatamente de Hola de signo de interrogación en hello `Duration` campo. Significa que hello `Duration` campo podría ser null.

### <a name="key-concepts"></a>Conceptos clave
* **Variables de conjunto de filas**: cada expresión de consulta que genera un conjunto de filas se puede asignar tooa variable. U-SQL sigue el modelo de nomenclatura de variables de hello T-SQL (`@searchlog`, por ejemplo) en el script de Hola.
* Hola **extraer** palabra clave lee datos de un archivo y define el esquema de hello en la lectura. `Extractors.Tsv` es un extractor de U-SQL integrado para archivos de valores separados por tabulación. Puede desarrollar extractores personalizados.
* Hola **salida** escribe datos desde un archivo de tooa de conjunto de filas. `Outputters.Csv()`es un toocreate de outputter U-SQL integrada en un archivo de valores separados por comas. También puede desarrollar outputters personalizados.

### <a name="file-paths"></a>Rutas de acceso de archivo

Hola extraer e instrucciones de salida usan rutas de acceso de archivo. Las rutas de acceso de archivo puede ser absolutas o relativas:

Esta ruta de acceso absoluta del archivo siguiente hace referencia a archivos tooa en un almacén de Data Lake denominado `mystore`:

    adl://mystore.azuredatalakestore.net/Samples/Data/SearchLog.tsv

La siguiente ruta de acceso relativa de archivo comienza con `"/"`. Hace referencia archivo tooa en la cuenta de almacén de Data Lake Hola predeterminada:

    /output/SearchLog-first-u-sql.csv

## <a name="use-scalar-variables"></a>Uso de variables escalares

Puede usar variables escalares como toomake y el mantenimiento de la secuencia de comandos sea más fácil. script de Hola anterior U SQL también puede escribirse como:

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

## <a name="transform-rowsets"></a>Transformación de conjuntos de filas

Use **seleccione** tootransform conjuntos de filas:

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

Hola de cláusula WHERE utiliza un [expresión C# booleana](https://msdn.microsoft.com/library/6a71f45d.aspx). Puede usar Hola C# expresión lenguaje toodo sus propias expresiones y funciones. Incluso puede realizar un filtrado más complejo si las combina con conjunciones (AND) y disyunciones (OR) lógicas.

Hello siguiente secuencia de comandos utiliza hello DateTime.Parse() método y una conjunción.

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
 >segunda consulta de Hello está en funcionamiento en el resultado de hello de hello primer conjunto de filas, que crea un compuesto de hello dos filtros. También puede volver a usar un nombre de variable y nombres de hello léxicamente tienen como ámbito.

## <a name="aggregate-rowsets"></a>Conjuntos de filas agregados
Deja de U-SQL Hola familiarizado ORDER BY, GROUP BY y las agregaciones.

Hello siguiente consulta busca duración total de Hola por región y, a continuación, muestra superior Hola cinco duraciones en orden.

Conjuntos de filas de U-SQL no conservan el orden de consulta siguiente Hola. Por lo tanto, tooorder una salida, necesita tooadd ORDER BY toohello salida instrucción:

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

Hola SQL U ORDER BY cláusula requiere el uso de cláusula de captura de hello en una expresión SELECT.

cláusula de Hello U-SQL tener puede ser usado toorestrict Hola salida toogroups que satisfacen la condición de hello HAVING:

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

Para escenarios avanzados de agregación, consulte la documentación de referencia de hello U-SQL de Hola para [agregar, analítica y hacer referencia a funciones](https://msdn.microsoft.com/en-us/library/azure/mt621335.aspx)

## <a name="next-steps"></a>Pasos siguientes
* [Información general de Análisis de Microsoft Azure Data Lake](data-lake-analytics-overview.md)
* [Desarrollo de scripts de U-SQL mediante Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md)
