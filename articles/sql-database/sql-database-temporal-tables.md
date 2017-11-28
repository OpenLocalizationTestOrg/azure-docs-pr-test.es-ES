---
title: aaaGetting iniciado con las tablas temporales de base de datos de SQL de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooget Introducción al uso de tablas temporales de base de datos de SQL Azure."
services: sql-database
documentationcenter: 
author: bonova
manager: jhubbard
editor: 
ms.assetid: c8c0f232-0751-4a7f-a36e-67a0b29fa1b8
ms.service: sql-database
ms.custom: develop databases
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: sql-database
ms.date: 01/10/2017
ms.author: bonova
ms.openlocfilehash: 54f394b51df07aa2f9bb299f207e692171d23479
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-temporal-tables-in-azure-sql-database"></a><span data-ttu-id="46ac3-103">Introducción a las tablas temporales de Base de datos SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="46ac3-103">Getting Started with Temporal Tables in Azure SQL Database</span></span>
<span data-ttu-id="46ac3-104">Las tablas temporales son una nueva característica de programación de base de datos de SQL de Azure permite tootrack y analizar el historial completo de Hola de cambios en los datos, sin necesidad de Hola de codificación personalizada.</span><span class="sxs-lookup"><span data-stu-id="46ac3-104">Temporal Tables are a new programmability feature of Azure SQL Database that allows you tootrack and analyze hello full history of changes in your data, without hello need for custom coding.</span></span> <span data-ttu-id="46ac3-105">Las tablas temporales conservar datos tootime estrechamente relacionadas con el contexto para que se pueden interpretar los hechos almacenados como válidas solo dentro de período específico de Hola.</span><span class="sxs-lookup"><span data-stu-id="46ac3-105">Temporal Tables keep data closely related tootime context so that stored facts can be interpreted as valid only within hello specific period.</span></span> <span data-ttu-id="46ac3-106">Esta propiedad de las tablas temporales permite un análisis eficaz basado en el tiempo y obtener información detalladas de la evolución de los datos.</span><span class="sxs-lookup"><span data-stu-id="46ac3-106">This property of Temporal Tables allows for efficient time-based analysis and getting insights from data evolution.</span></span>

## <a name="temporal-scenario"></a><span data-ttu-id="46ac3-107">Escenario temporal</span><span class="sxs-lookup"><span data-stu-id="46ac3-107">Temporal Scenario</span></span>
<span data-ttu-id="46ac3-108">Este artículo explica Hola pasos tooutilize tablas temporales en un escenario de aplicación.</span><span class="sxs-lookup"><span data-stu-id="46ac3-108">This article illustrates hello steps tooutilize Temporal Tables in an application scenario.</span></span> <span data-ttu-id="46ac3-109">Imagine que desea tootrack de actividad del usuario en un nuevo sitio Web que se está desarrollando desde el principio o en un sitio Web existente que desea que tooextend con análisis de actividad de usuario.</span><span class="sxs-lookup"><span data-stu-id="46ac3-109">Suppose that you want tootrack user activity on a new website that is being developed from scratch or on an existing website that you want tooextend with user activity analytics.</span></span> <span data-ttu-id="46ac3-110">En este ejemplo simplificado, se supone que el número de Hola de páginas web visitadas durante un período de tiempo es un indicador que necesita toobe captura y supervisarse en la base de datos de sitio Web de Hola que se hospeda en la base de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="46ac3-110">In this simplified example, we assume that hello number of visited web pages during a period of time is an indicator that needs toobe captured and monitored in hello website database that is hosted on Azure SQL Database.</span></span> <span data-ttu-id="46ac3-111">objetivo de Hola de análisis histórico de Hola de actividad de usuario es el sitio Web de tooget entradas tooredesign y ofrecer la mejor experiencia para los visitantes de Hola.</span><span class="sxs-lookup"><span data-stu-id="46ac3-111">hello goal of hello historical analysis of user activity is tooget inputs tooredesign website and provide better experience for hello visitors.</span></span>

<span data-ttu-id="46ac3-112">modelo de base de datos de Hola para este escenario es muy sencillo: métrica de la actividad de usuario se representa con un campo de número entero único, **PageVisited**y se han capturado junto con información básica acerca de perfil de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="46ac3-112">hello database model for this scenario is very simple - user activity metric is represented with a single integer field, **PageVisited**, and is captured along with basic information on hello user profile.</span></span> <span data-ttu-id="46ac3-113">Además, para el análisis basado en el tiempo, se mantendría una serie de filas para cada usuario, donde cada fila representa el número de Hola de páginas visitado un usuario concreto dentro de un período de tiempo específico.</span><span class="sxs-lookup"><span data-stu-id="46ac3-113">Additionally, for time based analysis, you would keep a series of rows for each user, where every row represents hello number of pages a particular user visited within a specific period of time.</span></span>

![Esquema](./media/sql-database-temporal-tables/AzureTemporal1.png)

<span data-ttu-id="46ac3-115">Afortunadamente, no es necesario tooput ningún esfuerzo en su aplicación toomaintain esta información de actividad.</span><span class="sxs-lookup"><span data-stu-id="46ac3-115">Fortunately, you do not need tooput any effort in your app toomaintain this activity information.</span></span> <span data-ttu-id="46ac3-116">Con las tablas temporales, se automatiza este proceso - ofrecerle una total flexibilidad durante el diseño de sitio Web y más toofocus de tiempo en el propio análisis de datos Hola.</span><span class="sxs-lookup"><span data-stu-id="46ac3-116">With Temporal Tables, this process is automated - giving you full flexibility during website design and more time toofocus on hello data analysis itself.</span></span> <span data-ttu-id="46ac3-117">Hola solo lo tienes toodo es tooensure que **WebSiteInfo** tabla está configurada como [temporales con versión del sistema](https://msdn.microsoft.com/library/dn935015.aspx#Anchor_0).</span><span class="sxs-lookup"><span data-stu-id="46ac3-117">hello only thing you have toodo is tooensure that **WebSiteInfo** table is configured as [temporal system-versioned](https://msdn.microsoft.com/library/dn935015.aspx#Anchor_0).</span></span> <span data-ttu-id="46ac3-118">los pasos exactos de Hello tooutilize que tablas temporales en este escenario se describen a continuación.</span><span class="sxs-lookup"><span data-stu-id="46ac3-118">hello exact steps tooutilize Temporal Tables in this scenario are described below.</span></span>

## <a name="step-1-configure-tables-as-temporal"></a><span data-ttu-id="46ac3-119">Paso 1: Configurar tablas como temporales</span><span class="sxs-lookup"><span data-stu-id="46ac3-119">Step 1: Configure tables as temporal</span></span>
<span data-ttu-id="46ac3-120">Dependiendo de si inicia un nuevo desarrollo o actualiza una aplicación existente, creará tablas temporales o modificará las existentes agregando atributos temporales.</span><span class="sxs-lookup"><span data-stu-id="46ac3-120">Depending on whether you are starting new development or upgrading existing application, you will either create temporal tables or modify existing ones by adding temporal attributes.</span></span> <span data-ttu-id="46ac3-121">En general, el escenario puede ser una combinación de estas dos opciones.</span><span class="sxs-lookup"><span data-stu-id="46ac3-121">In general case, your scenario can be a mix of these two options.</span></span> <span data-ttu-id="46ac3-122">Realice estas acciones utilizando [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) (SSMS), [SQL Server Data Tools](https://msdn.microsoft.com/library/mt204009.aspx) (SSDT) o cualquier otra herramienta de desarrollo de Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="46ac3-122">Perform these action using [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) (SSMS), [SQL Server Data Tools](https://msdn.microsoft.com/library/mt204009.aspx) (SSDT) or any other Transact-SQL development tool.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="46ac3-123">Se recomienda que siempre utilice Hola versión más reciente de Management Studio tooremain sincronizada con actualizaciones tooMicrosoft Azure y base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="46ac3-123">It is recommended that you always use hello latest version of Management Studio tooremain synchronized with updates tooMicrosoft Azure and SQL Database.</span></span> <span data-ttu-id="46ac3-124">[Actualice SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).</span><span class="sxs-lookup"><span data-stu-id="46ac3-124">[Update SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).</span></span>
> 
> 

### <a name="create-new-table"></a><span data-ttu-id="46ac3-125">Creación de una nueva tabla</span><span class="sxs-lookup"><span data-stu-id="46ac3-125">Create new table</span></span>
<span data-ttu-id="46ac3-126">Use el elemento del menú contextual "Nueva tabla con versiones del sistema" en el editor de consultas de explorador de objetos de SSMS tooopen Hola con una secuencia de comandos de plantilla de tabla temporal y, a continuación, usar plantillas de hello toopopulate "Especificar valores para parámetros de plantilla" (Ctrl + Mayús + M):</span><span class="sxs-lookup"><span data-stu-id="46ac3-126">Use context menu item “New System-Versioned Table” in SSMS Object Explorer tooopen hello query editor with a temporal table template script and then use “Specify Values for Template Parameters” (Ctrl+Shift+M) toopopulate hello template:</span></span>

![SSMSNewTable](./media/sql-database-temporal-tables/AzureTemporal2.png)

<span data-ttu-id="46ac3-128">En SSDT, elige la plantilla de "Tabla Temporal (con versiones del sistema)" al agregar el nuevo proyecto de base de datos de toohello de elementos.</span><span class="sxs-lookup"><span data-stu-id="46ac3-128">In SSDT, chose “Temporal Table (System-Versioned)” template when adding new items toohello database project.</span></span> <span data-ttu-id="46ac3-129">Que se Diseñador de tablas abiertas y habilitar tooeasily especifique Hola diseño de tabla:</span><span class="sxs-lookup"><span data-stu-id="46ac3-129">That will open table designer and enable you tooeasily specify hello table layout:</span></span>

![SSDTNewTable](./media/sql-database-temporal-tables/AzureTemporal3.png)

<span data-ttu-id="46ac3-131">También puede una tabla temporal crear especificando las instrucciones de Transact-SQL Hola directamente, como se muestra en el siguiente ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="46ac3-131">You can also a create temporal table by specifying hello Transact-SQL statements directly, as shown in hello example below.</span></span> <span data-ttu-id="46ac3-132">Tenga en cuenta que Hola elementos obligatorios de todas las tablas temporales son definición del período de Hola y cláusula de hello SYSTEM_VERSIONING con una tabla de usuario de tooanother de referencia que se va a almacenar versiones de filas de historial:</span><span class="sxs-lookup"><span data-stu-id="46ac3-132">Note that hello mandatory elements of every temporal table are hello PERIOD definition and hello SYSTEM_VERSIONING clause with a reference tooanother user table that will store historical row versions:</span></span>

````
CREATE TABLE WebsiteUserInfo 
(  
    [UserID] int NOT NULL PRIMARY KEY CLUSTERED 
  , [UserName] nvarchar(100) NOT NULL
  , [PagesVisited] int NOT NULL 
  , [ValidFrom] datetime2 (0) GENERATED ALWAYS AS ROW START
  , [ValidTo] datetime2 (0) GENERATED ALWAYS AS ROW END
  , PERIOD FOR SYSTEM_TIME (ValidFrom, ValidTo)
 )  
 WITH (SYSTEM_VERSIONING = ON (HISTORY_TABLE = dbo.WebsiteUserInfoHistory));
````

<span data-ttu-id="46ac3-133">Cuando se crea la tabla temporal con versiones del sistema, se crea automáticamente Hola que acompaña a la tabla de historial con la configuración predeterminada de Hola.</span><span class="sxs-lookup"><span data-stu-id="46ac3-133">When you create system-versioned temporal table, hello accompanying history table with hello default configuration is automatically created.</span></span> <span data-ttu-id="46ac3-134">tabla de historial de Hello predeterminada contiene un índice agrupado de árbol B de columnas de periodo (fin e inicio) Hola habilitada la compresión de página.</span><span class="sxs-lookup"><span data-stu-id="46ac3-134">hello default history table contains a clustered B-tree index on hello period columns (end, start) with page compression enabled.</span></span> <span data-ttu-id="46ac3-135">Esta configuración es óptima para la mayoría de Hola de los escenarios en que se usan las tablas temporales, especialmente para [auditoría de datos](https://msdn.microsoft.com/library/mt631669.aspx#Anchor_0).</span><span class="sxs-lookup"><span data-stu-id="46ac3-135">This configuration is optimal for hello majority of scenarios in which temporal tables are used, especially for [data auditing](https://msdn.microsoft.com/library/mt631669.aspx#Anchor_0).</span></span> 

<span data-ttu-id="46ac3-136">En este caso particular, nuestro objetivo es análisis de tendencias basados en tiempo de tooperform a través de un historial de datos más largo y con los conjuntos de datos más grandes, por lo que la elección de Hola de almacenamiento de tabla de historial de hello es un índice de almacén de columnas agrupado.</span><span class="sxs-lookup"><span data-stu-id="46ac3-136">In this particular case, we aim tooperform time-based trend analysis over a longer data history and with bigger data sets, so hello storage choice for hello history table is a clustered columnstore index.</span></span> <span data-ttu-id="46ac3-137">Un almacén de columnas agrupado proporciona muy buena compresión y rendimiento de consultas analíticas.</span><span class="sxs-lookup"><span data-stu-id="46ac3-137">A clustered columnstore provides very good compression and performance for analytical queries.</span></span> <span data-ttu-id="46ac3-138">Dé de tablas temporales Hola índices tooconfigure de flexibilidad en las tablas actual y temporal de hello completamente por separado.</span><span class="sxs-lookup"><span data-stu-id="46ac3-138">Temporal Tables give you hello flexibility tooconfigure indexes on hello current and temporal tables completely independently.</span></span> 

> [!NOTE]
> <span data-ttu-id="46ac3-139">Índices de almacén de columnas solo están disponibles en el nivel de servicio premium de Hola.</span><span class="sxs-lookup"><span data-stu-id="46ac3-139">Columnstore indexes are only available in hello premium service tier.</span></span>
>

<span data-ttu-id="46ac3-140">Hola siguiente secuencia de comandos muestra cómo índice predeterminado en la tabla de historial puede ser almacén de columnas modificadas toohello en clúster:</span><span class="sxs-lookup"><span data-stu-id="46ac3-140">hello following script shows how default index on history table can be changed toohello clustered columnstore:</span></span>

````
CREATE CLUSTERED COLUMNSTORE INDEX IX_WebsiteUserInfoHistory
ON dbo.WebsiteUserInfoHistory
WITH (DROP_EXISTING = ON); 
````

<span data-ttu-id="46ac3-141">Las tablas temporales se representan en hello Explorador de objetos con icono específico de Hola para facilitar la identificación, mientras que su tabla de historial se muestra como un nodo secundario.</span><span class="sxs-lookup"><span data-stu-id="46ac3-141">Temporal Tables are represented in hello Object Explorer with hello specific icon for easier identification, while its history table is displayed as a child node.</span></span>

![AlterTable](./media/sql-database-temporal-tables/AzureTemporal4.png)

### <a name="alter-existing-table-tootemporal"></a><span data-ttu-id="46ac3-143">ALTER tootemporal de tabla existente</span><span class="sxs-lookup"><span data-stu-id="46ac3-143">Alter existing table tootemporal</span></span>
<span data-ttu-id="46ac3-144">Vamos a cubrir escenario alternativo de hello en qué hello WebsiteUserInfo tabla ya existe, pero no fue diseñado tookeep un historial de cambios.</span><span class="sxs-lookup"><span data-stu-id="46ac3-144">Let’s cover hello alternative scenario in which hello WebsiteUserInfo table already exists, but was not designed tookeep a history of changes.</span></span> <span data-ttu-id="46ac3-145">En este caso, simplemente puede ampliar toobecome de tabla existente de hello temporal, como se muestra en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="46ac3-145">In this case, you can simply extend hello existing table toobecome temporal, as shown in hello following example:</span></span>

````
ALTER TABLE WebsiteUserInfo 
ADD 
    ValidFrom datetime2 (0) GENERATED ALWAYS AS ROW START HIDDEN  
        constraint DF_ValidFrom DEFAULT DATEADD(SECOND, -1, SYSUTCDATETIME())
    , ValidTo datetime2 (0)  GENERATED ALWAYS AS ROW END HIDDEN   
        constraint DF_ValidTo DEFAULT '9999.12.31 23:59:59.99'
    , PERIOD FOR SYSTEM_TIME (ValidFrom, ValidTo); 

ALTER TABLE WebsiteUserInfo  
SET (SYSTEM_VERSIONING = ON (HISTORY_TABLE = dbo.WebsiteUserInfoHistory));
GO

CREATE CLUSTERED COLUMNSTORE INDEX IX_WebsiteUserInfoHistory
ON dbo.WebsiteUserInfoHistory
WITH (DROP_EXISTING = ON); 
````

## <a name="step-2-run-your-workload-regularly"></a><span data-ttu-id="46ac3-146">Paso 2: Ejecutar la carga de trabajo regularmente</span><span class="sxs-lookup"><span data-stu-id="46ac3-146">Step 2: Run your workload regularly</span></span>
<span data-ttu-id="46ac3-147">Hola principal ventaja de las tablas temporales es que no necesita toochange o ajustar su sitio Web en cualquier seguimiento de cambios de forma tooperform.</span><span class="sxs-lookup"><span data-stu-id="46ac3-147">hello main advantage of Temporal Tables is that you do not need toochange or adjust your website in any way tooperform change tracking.</span></span> <span data-ttu-id="46ac3-148">Una vez creadas, las tablas temporales conservan las versiones de fila anteriores cada vez que realiza modificaciones en los datos.</span><span class="sxs-lookup"><span data-stu-id="46ac3-148">Once created, Temporal Tables transparently persist previous row versions every time you perform modifications on your data.</span></span> 

<span data-ttu-id="46ac3-149">En el seguimiento de cambios automático de orden tooleverage para este escenario en particular, vamos a simplemente actualizar la columna **PagesVisited** cada vez que al usuario finaliza la sesión en el sitio Web de hello:</span><span class="sxs-lookup"><span data-stu-id="46ac3-149">In order tooleverage automatic change tracking for this particular scenario, let’s just update column **PagesVisited** every time when user ends her/his session on hello website:</span></span>

````
UPDATE WebsiteUserInfo  SET [PagesVisited] = 5 
WHERE [UserID] = 1;
````

<span data-ttu-id="46ac3-150">Es importante toonotice que Hola consulta update no necesita la hora exacta de hello tooknow cuando se produjo la operación real de hello ni cómo se conservarán los datos históricos para su posterior análisis.</span><span class="sxs-lookup"><span data-stu-id="46ac3-150">It is important toonotice that hello update query doesn’t need tooknow hello exact time when hello actual operation occurred nor how historical data will be preserved for future analysis.</span></span> <span data-ttu-id="46ac3-151">Ambos aspectos se administran automáticamente Hola base de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="46ac3-151">Both aspects are automatically handled by hello Azure SQL Database.</span></span> <span data-ttu-id="46ac3-152">Hello diagrama siguiente ilustra cómo se generan los datos de historial en todas las actualizaciones.</span><span class="sxs-lookup"><span data-stu-id="46ac3-152">hello following diagram illustrates how history data is being generated on every update.</span></span>

![TemporalArchitecture](./media/sql-database-temporal-tables/AzureTemporal5.png)

## <a name="step-3-perform-historical-data-analysis"></a><span data-ttu-id="46ac3-154">Paso 3: Realizar análisis de datos históricos</span><span class="sxs-lookup"><span data-stu-id="46ac3-154">Step 3: Perform historical data analysis</span></span>
<span data-ttu-id="46ac3-155">Ahora, cuando el control de versiones del sistema temporal está habilitado, el análisis de datos históricos se realiza con una sola consulta.</span><span class="sxs-lookup"><span data-stu-id="46ac3-155">Now when temporal system-versioning is enabled, historical data analysis is just one query away from you.</span></span> <span data-ttu-id="46ac3-156">En este artículo se proporcionan algunos ejemplos que tratan situaciones comunes de análisis - toolearn todos los detalles, explorar diversas opciones que se introdujo con hello [FOR SYSTEM_TIME](https://msdn.microsoft.com/library/dn935015.aspx#Anchor_3) cláusula.</span><span class="sxs-lookup"><span data-stu-id="46ac3-156">In this article, we will provide a few examples that address common analysis scenarios - toolearn all details, explore various options introduced with hello [FOR SYSTEM_TIME](https://msdn.microsoft.com/library/dn935015.aspx#Anchor_3) clause.</span></span>

<span data-ttu-id="46ac3-157">toosee Hola superior 10 usuarios ordenados por número de Hola de páginas web que visita a partir de una hora hace, ejecute esta consulta:</span><span class="sxs-lookup"><span data-stu-id="46ac3-157">toosee hello top 10 users ordered by hello number of visited web pages as of an hour ago, run this query:</span></span>

````
DECLARE @hourAgo datetime2 = DATEADD(HOUR, -1, SYSUTCDATETIME());
SELECT TOP 10 * FROM dbo.WebsiteUserInfo FOR SYSTEM_TIME AS OF @hourAgo
ORDER BY PagesVisited DESC
````

<span data-ttu-id="46ac3-158">Puede modificar fácilmente esta consulta visitas al sitio de Hola de tooanalyze desde hace un día, hace un mes o en cualquier momento Hola anterior desea.</span><span class="sxs-lookup"><span data-stu-id="46ac3-158">You can easily modify this query tooanalyze hello site visits as of a day ago, a month ago or at any point in hello past you wish.</span></span>

<span data-ttu-id="46ac3-159">tooperform básica análisis estadísticos para hello día de ayer, Hola de uso siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="46ac3-159">tooperform basic statistical analysis for hello previous day, use hello following example:</span></span>

````
DECLARE @twoDaysAgo datetime2 = DATEADD(DAY, -2, SYSUTCDATETIME());
DECLARE @aDayAgo datetime2 = DATEADD(DAY, -1, SYSUTCDATETIME());

SELECT UserID, SUM (PagesVisited) as TotalVisitedPages, AVG (PagesVisited) as AverageVisitedPages,
MAX (PagesVisited) AS MaxVisitedPages, MIN (PagesVisited) AS MinVisitedPages,
STDEV (PagesVisited) as StDevViistedPages
FROM dbo.WebsiteUserInfo 
FOR SYSTEM_TIME BETWEEN @twoDaysAgo AND @aDayAgo
GROUP BY UserId
````

<span data-ttu-id="46ac3-160">toosearch para las actividades de un usuario específico, en un período de tiempo, use Hola CONTAINED IN cláusula:</span><span class="sxs-lookup"><span data-stu-id="46ac3-160">toosearch for activities of a specific user, within a period of time, use hello CONTAINED IN clause:</span></span>

````
DECLARE @hourAgo datetime2 = DATEADD(HOUR, -1, SYSUTCDATETIME());
DECLARE @twoHoursAgo datetime2 = DATEADD(HOUR, -2, SYSUTCDATETIME());
SELECT * FROM dbo.WebsiteUserInfo 
FOR SYSTEM_TIME CONTAINED IN (@twoHoursAgo, @hourAgo)
WHERE [UserID] = 1;
````

<span data-ttu-id="46ac3-161">La visualización de gráficos es especialmente conveniente para consultas temporales, ya que puede mostrar tendencias y patrones de uso de una forma intuitiva muy fácilmente:</span><span class="sxs-lookup"><span data-stu-id="46ac3-161">Graphic visualization is especially convenient for temporal queries as you can show trends and usage patterns in an intuitive way very easily:</span></span>

![TemporalGraph](./media/sql-database-temporal-tables/AzureTemporal6.png)

## <a name="evolving-table-schema"></a><span data-ttu-id="46ac3-163">Evolución del esquema de tabla</span><span class="sxs-lookup"><span data-stu-id="46ac3-163">Evolving table schema</span></span>
<span data-ttu-id="46ac3-164">Por lo general, deberá esquema de tabla temporal de hello toochange mientras se está realizando el desarrollo de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="46ac3-164">Typically, you will need toochange hello temporal table schema while you are doing app development.</span></span> <span data-ttu-id="46ac3-165">Para ello, simplemente ejecute instrucciones ALTER TABLE regulares y base de datos de SQL Azure correctamente se propagará a tabla de historial de cambios toohello.</span><span class="sxs-lookup"><span data-stu-id="46ac3-165">For that, simply run regular ALTER TABLE statements and Azure SQL Database will appropriately propagate changes toohello history table.</span></span> <span data-ttu-id="46ac3-166">Hello secuencia de comandos siguiente muestra cómo se pueden agregar atributos adicionales para el seguimiento de:</span><span class="sxs-lookup"><span data-stu-id="46ac3-166">hello following script shows how you can add additional attribute for tracking:</span></span>

````
/*Add new column for tracking source IP address*/
ALTER TABLE dbo.WebsiteUserInfo 
ADD  [IPAddress] varchar(128) NOT NULL CONSTRAINT DF_Address DEFAULT 'N/A';
````

<span data-ttu-id="46ac3-167">De forma similar, puede cambiar la definición de columna mientras la carga de trabajo esté activa:</span><span class="sxs-lookup"><span data-stu-id="46ac3-167">Similarly, you can change column definition while your workload is active:</span></span>

````
/*Increase hello length of name column*/
ALTER TABLE dbo.WebsiteUserInfo 
    ALTER COLUMN  UserName nvarchar(256) NOT NULL;
````

<span data-ttu-id="46ac3-168">Por último, puede quitar una columna que ya no necesite.</span><span class="sxs-lookup"><span data-stu-id="46ac3-168">Finally, you can remove a column that you do not need anymore.</span></span>

````
/*Drop unnecessary column */
ALTER TABLE dbo.WebsiteUserInfo 
    DROP COLUMN TemporaryColumn; 
````

<span data-ttu-id="46ac3-169">O bien, usar la versión más reciente [SSDT](https://msdn.microsoft.com/library/mt204009.aspx) toochange temporales esquema de tabla mientras estás conectado toohello de base de datos (modo en línea) o como parte del proyecto de base de datos de hello (modo sin conexión).</span><span class="sxs-lookup"><span data-stu-id="46ac3-169">Alternatively, use latest [SSDT](https://msdn.microsoft.com/library/mt204009.aspx) toochange temporal table schema while you are connected toohello database (online mode) or as part of hello database project (offline mode).</span></span>

## <a name="controlling-retention-of-historical-data"></a><span data-ttu-id="46ac3-170">Control de la retención de datos históricos</span><span class="sxs-lookup"><span data-stu-id="46ac3-170">Controlling retention of historical data</span></span>
<span data-ttu-id="46ac3-171">Con las tablas temporales con versión del sistema, tabla de historial de hello puede aumentar el tamaño de la base de datos de hello más de las tablas normales.</span><span class="sxs-lookup"><span data-stu-id="46ac3-171">With system-versioned temporal tables, hello history table may increase hello database size more than regular tables.</span></span> <span data-ttu-id="46ac3-172">Una tabla de historial de gran tamaño y creciente puede ser un problema debido a los costos de almacenamiento de toopure así como la imposición de un rendimiento impuesto sobre las consultas temporales.</span><span class="sxs-lookup"><span data-stu-id="46ac3-172">A large and ever-growing history table can become an issue both due toopure storage costs as well as imposing a performance tax on temporal querying.</span></span> <span data-ttu-id="46ac3-173">Por lo tanto, al desarrollar una directiva de retención de datos para administrar los datos en la tabla de historial de hello es un aspecto importante de planeación y la administración del ciclo de vida de Hola de cada tabla temporal.</span><span class="sxs-lookup"><span data-stu-id="46ac3-173">Hence, developing a data retention policy for managing data in hello history table is an important aspect of planning and managing hello lifecycle of every temporal table.</span></span> <span data-ttu-id="46ac3-174">Con la base de datos de SQL Azure, deberá Hola siguientes enfoques para administrar los datos históricos de la tabla temporal de hello:</span><span class="sxs-lookup"><span data-stu-id="46ac3-174">With Azure SQL Database, you have hello following approaches for managing historical data in hello temporal table:</span></span>

* [<span data-ttu-id="46ac3-175">Partición de tabla</span><span class="sxs-lookup"><span data-stu-id="46ac3-175">Table Partitioning</span></span>](https://msdn.microsoft.com/library/mt637341.aspx#Anchor_2)
* [<span data-ttu-id="46ac3-176">Script de limpieza personalizado</span><span class="sxs-lookup"><span data-stu-id="46ac3-176">Custom Cleanup Script</span></span>](https://msdn.microsoft.com/library/mt637341.aspx#Anchor_3)

## <a name="next-steps"></a><span data-ttu-id="46ac3-177">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="46ac3-177">Next steps</span></span>
<span data-ttu-id="46ac3-178">Para obtener información detallada sobre tablas temporales, consulte la [documentación de MSDN](https://msdn.microsoft.com/library/dn935015.aspx).</span><span class="sxs-lookup"><span data-stu-id="46ac3-178">For detailed information on Temporal Tables, check out [MSDN documentation](https://msdn.microsoft.com/library/dn935015.aspx).</span></span>
<span data-ttu-id="46ac3-179">Visita Channel 9 toohear una [historia de éxito de implementación temporal de clientes reales](https://channel9.msdn.com/Blogs/jsturtevant/Azure-SQL-Temporal-Tables-with-RockStep-Solutions) inspección y un [live demostración temporal](https://channel9.msdn.com/Shows/Data-Exposed/Temporal-in-SQL-Server-2016).</span><span class="sxs-lookup"><span data-stu-id="46ac3-179">Visit Channel 9 toohear a [real customer temporal implemenation success story](https://channel9.msdn.com/Blogs/jsturtevant/Azure-SQL-Temporal-Tables-with-RockStep-Solutions) and watch a [live temporal demonstration](https://channel9.msdn.com/Shows/Data-Exposed/Temporal-in-SQL-Server-2016).</span></span>

