---
title: "Introducción al catálogo de U-SQL | Microsoft Docs"
description: "Aprenda a usar el catálogo de U-SQL para compartir código y datos."
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
ms.date: 05/09/2017
ms.author: edmaca
ms.openlocfilehash: 08364c6c7bea53807844e3b1cc327dc3742e0487
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-u-sql-catalog"></a><span data-ttu-id="06e0d-103">Introducción al catálogo de U-SQL</span><span class="sxs-lookup"><span data-stu-id="06e0d-103">Get started with the U-SQL Catalog</span></span>

## <a name="create-a-tvf"></a><span data-ttu-id="06e0d-104">Creación de una TVF</span><span class="sxs-lookup"><span data-stu-id="06e0d-104">Create a TVF</span></span>

<span data-ttu-id="06e0d-105">En el anterior script de U-SQL, repitió el uso de EXTRACT para leer el mismo archivo de origen.</span><span class="sxs-lookup"><span data-stu-id="06e0d-105">In the previous U-SQL script, you repeated the use of EXTRACT to read from the same source file.</span></span> <span data-ttu-id="06e0d-106">La función con valores de tabla de U-SQL (TVF) permite encapsular los datos para volver a usarlos más adelante.</span><span class="sxs-lookup"><span data-stu-id="06e0d-106">With the U-SQL table-valued function (TVF), you can encapsulate the data for future reuse.</span></span>  

<span data-ttu-id="06e0d-107">El siguiente script crea una función TVF llamada `Searchlog()` en la base de datos y el esquema predeterminados:</span><span class="sxs-lookup"><span data-stu-id="06e0d-107">The following script creates a TVF called `Searchlog()` in the default database and schema:</span></span>

```
DROP FUNCTION IF EXISTS Searchlog;

CREATE FUNCTION Searchlog()
RETURNS @searchlog TABLE
(
            UserId          int,
            Start           DateTime,
            Region          string,
            Query           string,
            Duration        int?,
            Urls            string,
            ClickedUrls     string
)
AS BEGIN
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
RETURN;
END;
```

<span data-ttu-id="06e0d-108">El siguiente script muestra cómo usar la TVF definida en el anterior script:</span><span class="sxs-lookup"><span data-stu-id="06e0d-108">The following script shows you how to use the TVF that was defined in the previous script:</span></span>

```
@res =
    SELECT
        Region,
        SUM(Duration) AS TotalDuration
    FROM Searchlog() AS S
GROUP BY Region
HAVING SUM(Duration) > 200;

OUTPUT @res
    TO "/output/SerachLog-use-tvf.csv"
    ORDER BY TotalDuration DESC
    USING Outputters.Csv();
```

## <a name="create-views"></a><span data-ttu-id="06e0d-109">Creación de vistas</span><span class="sxs-lookup"><span data-stu-id="06e0d-109">Create views</span></span>

<span data-ttu-id="06e0d-110">Si tiene una expresión de consulta única, en lugar de una función TVF puede usar una vista de U-SQL para encapsular esa expresión.</span><span class="sxs-lookup"><span data-stu-id="06e0d-110">If you have a single query expression, instead of a TVF you can use a U-SQL VIEW to encapsulate that expression.</span></span>

<span data-ttu-id="06e0d-111">El siguiente script crea una vista llamada `SearchlogView` en la base de datos y el esquema predeterminados:</span><span class="sxs-lookup"><span data-stu-id="06e0d-111">The following script creates a view called `SearchlogView` in the default database and schema:</span></span>

```
DROP VIEW IF EXISTS SearchlogView;

CREATE VIEW SearchlogView AS  
    EXTRACT UserId          int,
            Start           DateTime,
            Region          string,
            Query           string,
            Duration        int?,
            Urls            string,
            ClickedUrls     string
    FROM "/Samples/Data/SearchLog.tsv"
USING Extractors.Tsv();
```

<span data-ttu-id="06e0d-112">El siguiente script muestra el uso de la vista definida:</span><span class="sxs-lookup"><span data-stu-id="06e0d-112">The following script demonstrates the use of the defined view:</span></span>

```
@res =
    SELECT
        Region,
        SUM(Duration) AS TotalDuration
    FROM SearchlogView
GROUP BY Region
HAVING SUM(Duration) > 200;

OUTPUT @res
    TO "/output/Searchlog-use-view.csv"
    ORDER BY TotalDuration DESC
    USING Outputters.Csv();
```

## <a name="create-tables"></a><span data-ttu-id="06e0d-113">Cree las tablas.</span><span class="sxs-lookup"><span data-stu-id="06e0d-113">Create tables</span></span>
<span data-ttu-id="06e0d-114">De forma semejante a una tabla de base de datos relacional, U-SQL permite crear una tabla con un esquema predefinido o crear una tabla que infiere el esquema a partir de la consulta que rellena la tabla (lo que también se conoce como CREATE TABLE AS SELECT o CTAS).</span><span class="sxs-lookup"><span data-stu-id="06e0d-114">As with relational database tables, with U-SQL you can create a table with a predefined schema or create a table that infers the schema from the query that populates the table (also known as CREATE TABLE AS SELECT or CTAS).</span></span>

<span data-ttu-id="06e0d-115">Cree una base de datos y dos tablas mediante el siguiente script:</span><span class="sxs-lookup"><span data-stu-id="06e0d-115">Create a database and two tables by using the following script:</span></span>

```
DROP DATABASE IF EXISTS SearchLogDb;
CREATE DATABASE SearchLogDb;
USE DATABASE SearchLogDb;

DROP TABLE IF EXISTS SearchLog1;
DROP TABLE IF EXISTS SearchLog2;

CREATE TABLE SearchLog1 (
            UserId          int,
            Start           DateTime,
            Region          string,
            Query           string,
            Duration        int?,
            Urls            string,
            ClickedUrls     string,

            INDEX sl_idx CLUSTERED (UserId ASC)
                DISTRIBUTED BY HASH (UserId)
);

INSERT INTO SearchLog1 SELECT * FROM master.dbo.Searchlog() AS s;

CREATE TABLE SearchLog2(
    INDEX sl_idx CLUSTERED (UserId ASC)
            DISTRIBUTED BY HASH (UserId)
) AS SELECT * FROM master.dbo.Searchlog() AS S; // You can use EXTRACT or SELECT here
```

## <a name="query-tables"></a><span data-ttu-id="06e0d-116">Consulta de tablas</span><span class="sxs-lookup"><span data-stu-id="06e0d-116">Query tables</span></span>
<span data-ttu-id="06e0d-117">Puede consultar tablas, como las creadas en el script anterior, de la misma forma que se consultan los archivos de datos.</span><span class="sxs-lookup"><span data-stu-id="06e0d-117">You can query tables, such as those created in the previous script, in the same way that you query the data files.</span></span> <span data-ttu-id="06e0d-118">En lugar de crear un conjunto de filas mediante EXTRACT, ahora se puede hacer referencia al nombre de la tabla.</span><span class="sxs-lookup"><span data-stu-id="06e0d-118">Instead of creating a rowset by using EXTRACT, you now can refer to the table name.</span></span>

<span data-ttu-id="06e0d-119">Para leer las tablas, modifique el script de transformación que usó anteriormente:</span><span class="sxs-lookup"><span data-stu-id="06e0d-119">To read from the tables, modify the transform script that you used previously:</span></span>

```
@rs1 =
    SELECT
        Region,
        SUM(Duration) AS TotalDuration
    FROM SearchLogDb.dbo.SearchLog2
GROUP BY Region;

@res =
    SELECT *
    FROM @rs1
    ORDER BY TotalDuration DESC
    FETCH 5 ROWS;

OUTPUT @res
    TO "/output/Searchlog-query-table.csv"
    ORDER BY TotalDuration DESC
    USING Outputters.Csv();
```

 >[!NOTE]
 ><span data-ttu-id="06e0d-120">Actualmente, no puede ejecutar una instrucción SELECT en una tabla del mismo script que aquel donde creó la tabla.</span><span class="sxs-lookup"><span data-stu-id="06e0d-120">Currently, you cannot run a SELECT on a table in the same script as the one where you created the table.</span></span>

## <a name="next-steps"></a><span data-ttu-id="06e0d-121">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="06e0d-121">Next Steps</span></span>
* [<span data-ttu-id="06e0d-122">Información general de Análisis de Microsoft Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="06e0d-122">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="06e0d-123">Desarrollo de scripts de U-SQL mediante Data Lake Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="06e0d-123">Develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
* [<span data-ttu-id="06e0d-124">Supervisión y solución de problemas de trabajos de Azure Data Lake Analytics con Azure Portal</span><span class="sxs-lookup"><span data-stu-id="06e0d-124">Monitor and troubleshoot Azure Data Lake Analytics jobs using Azure portal</span></span>](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)
