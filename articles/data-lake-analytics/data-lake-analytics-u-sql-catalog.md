---
title: "Empezar a trabajar con el catálogo de hello U-SQL | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse hello U-SQL catálogo tooshare código y datos."
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
ms.openlocfilehash: 559bb7a3879031eb290a3e82946d7bf42ac9f553
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-u-sql-catalog"></a><span data-ttu-id="6d03e-103">Empezar a trabajar con hello catálogo U-SQL</span><span class="sxs-lookup"><span data-stu-id="6d03e-103">Get started with hello U-SQL Catalog</span></span>

## <a name="create-a-tvf"></a><span data-ttu-id="6d03e-104">Creación de una TVF</span><span class="sxs-lookup"><span data-stu-id="6d03e-104">Create a TVF</span></span>

<span data-ttu-id="6d03e-105">En el script U-SQL Hola anterior, repite uso de Hola de extracción tooread de hello mismo archivo de origen.</span><span class="sxs-lookup"><span data-stu-id="6d03e-105">In hello previous U-SQL script, you repeated hello use of EXTRACT tooread from hello same source file.</span></span> <span data-ttu-id="6d03e-106">Con la función con valores de tabla de hello U T-SQL (TVF), puede encapsular los datos de Hola para reutilizarlo en un futuro.</span><span class="sxs-lookup"><span data-stu-id="6d03e-106">With hello U-SQL table-valued function (TVF), you can encapsulate hello data for future reuse.</span></span>  

<span data-ttu-id="6d03e-107">Hello script siguiente crea una función TVF denominada `Searchlog()` en la base de datos de hello predeterminada y el esquema:</span><span class="sxs-lookup"><span data-stu-id="6d03e-107">hello following script creates a TVF called `Searchlog()` in hello default database and schema:</span></span>

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

<span data-ttu-id="6d03e-108">Hola siguiente secuencia de comandos muestra cómo toouse Hola TVF que se definió en el script de Hola anterior:</span><span class="sxs-lookup"><span data-stu-id="6d03e-108">hello following script shows you how toouse hello TVF that was defined in hello previous script:</span></span>

```
@res =
    SELECT
        Region,
        SUM(Duration) AS TotalDuration
    FROM Searchlog() AS S
GROUP BY Region
HAVING SUM(Duration) > 200;

OUTPUT @res
    too"/output/SerachLog-use-tvf.csv"
    ORDER BY TotalDuration DESC
    USING Outputters.Csv();
```

## <a name="create-views"></a><span data-ttu-id="6d03e-109">Creación de vistas</span><span class="sxs-lookup"><span data-stu-id="6d03e-109">Create views</span></span>

<span data-ttu-id="6d03e-110">Si tiene una expresión de consulta única, en lugar de una función TVF se puede usar una vista SQL U tooencapsulate esa expresión.</span><span class="sxs-lookup"><span data-stu-id="6d03e-110">If you have a single query expression, instead of a TVF you can use a U-SQL VIEW tooencapsulate that expression.</span></span>

<span data-ttu-id="6d03e-111">Hello script siguiente crea una vista denominada `SearchlogView` en la base de datos de hello predeterminada y el esquema:</span><span class="sxs-lookup"><span data-stu-id="6d03e-111">hello following script creates a view called `SearchlogView` in hello default database and schema:</span></span>

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

<span data-ttu-id="6d03e-112">Hola siguiente secuencia de comandos muestra uso de saludo de la vista de hello definido:</span><span class="sxs-lookup"><span data-stu-id="6d03e-112">hello following script demonstrates hello use of hello defined view:</span></span>

```
@res =
    SELECT
        Region,
        SUM(Duration) AS TotalDuration
    FROM SearchlogView
GROUP BY Region
HAVING SUM(Duration) > 200;

OUTPUT @res
    too"/output/Searchlog-use-view.csv"
    ORDER BY TotalDuration DESC
    USING Outputters.Csv();
```

## <a name="create-tables"></a><span data-ttu-id="6d03e-113">Cree las tablas.</span><span class="sxs-lookup"><span data-stu-id="6d03e-113">Create tables</span></span>
<span data-ttu-id="6d03e-114">Como con tablas de base de datos relacional, con SQL U puede crear una tabla con un esquema predefinido o crear una tabla que deduce el esquema de Hola de consulta de Hola que rellena la tabla de hello (también conocido como CREATE TABLE AS SELECT o CTAS).</span><span class="sxs-lookup"><span data-stu-id="6d03e-114">As with relational database tables, with U-SQL you can create a table with a predefined schema or create a table that infers hello schema from hello query that populates hello table (also known as CREATE TABLE AS SELECT or CTAS).</span></span>

<span data-ttu-id="6d03e-115">Crear una base de datos y dos tablas mediante Hola siguiente secuencia de comandos:</span><span class="sxs-lookup"><span data-stu-id="6d03e-115">Create a database and two tables by using hello following script:</span></span>

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

## <a name="query-tables"></a><span data-ttu-id="6d03e-116">Consulta de tablas</span><span class="sxs-lookup"><span data-stu-id="6d03e-116">Query tables</span></span>
<span data-ttu-id="6d03e-117">Puede consultar las tablas, como los creados en el script anterior de hello, Hola igual que consultar los archivos de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="6d03e-117">You can query tables, such as those created in hello previous script, in hello same way that you query hello data files.</span></span> <span data-ttu-id="6d03e-118">En lugar de crear un conjunto de filas mediante el uso de extracción, ahora puede consultar toohello nombre de la tabla.</span><span class="sxs-lookup"><span data-stu-id="6d03e-118">Instead of creating a rowset by using EXTRACT, you now can refer toohello table name.</span></span>

<span data-ttu-id="6d03e-119">tooread de tablas de hello, modifique el script de transformación de Hola que usó anteriormente:</span><span class="sxs-lookup"><span data-stu-id="6d03e-119">tooread from hello tables, modify hello transform script that you used previously:</span></span>

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
    too"/output/Searchlog-query-table.csv"
    ORDER BY TotalDuration DESC
    USING Outputters.Csv();
```

 >[!NOTE]
 ><span data-ttu-id="6d03e-120">Actualmente, no se puede ejecutar una instrucción SELECT en una tabla de hello mismo script como Hola uno en la que creó la tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="6d03e-120">Currently, you cannot run a SELECT on a table in hello same script as hello one where you created hello table.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6d03e-121">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6d03e-121">Next Steps</span></span>
* [<span data-ttu-id="6d03e-122">Información general de Análisis de Microsoft Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="6d03e-122">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="6d03e-123">Desarrollo de scripts de U-SQL mediante Data Lake Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6d03e-123">Develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
* [<span data-ttu-id="6d03e-124">Supervisión y solución de problemas de trabajos de Azure Data Lake Analytics con Azure Portal</span><span class="sxs-lookup"><span data-stu-id="6d03e-124">Monitor and troubleshoot Azure Data Lake Analytics jobs using Azure portal</span></span>](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)
