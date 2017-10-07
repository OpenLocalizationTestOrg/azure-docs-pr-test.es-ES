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
# <a name="getting-started-with-temporal-tables-in-azure-sql-database"></a>Introducción a las tablas temporales de Base de datos SQL de Azure
Las tablas temporales son una nueva característica de programación de base de datos de SQL de Azure permite tootrack y analizar el historial completo de Hola de cambios en los datos, sin necesidad de Hola de codificación personalizada. Las tablas temporales conservar datos tootime estrechamente relacionadas con el contexto para que se pueden interpretar los hechos almacenados como válidas solo dentro de período específico de Hola. Esta propiedad de las tablas temporales permite un análisis eficaz basado en el tiempo y obtener información detalladas de la evolución de los datos.

## <a name="temporal-scenario"></a>Escenario temporal
Este artículo explica Hola pasos tooutilize tablas temporales en un escenario de aplicación. Imagine que desea tootrack de actividad del usuario en un nuevo sitio Web que se está desarrollando desde el principio o en un sitio Web existente que desea que tooextend con análisis de actividad de usuario. En este ejemplo simplificado, se supone que el número de Hola de páginas web visitadas durante un período de tiempo es un indicador que necesita toobe captura y supervisarse en la base de datos de sitio Web de Hola que se hospeda en la base de datos de SQL Azure. objetivo de Hola de análisis histórico de Hola de actividad de usuario es el sitio Web de tooget entradas tooredesign y ofrecer la mejor experiencia para los visitantes de Hola.

modelo de base de datos de Hola para este escenario es muy sencillo: métrica de la actividad de usuario se representa con un campo de número entero único, **PageVisited**y se han capturado junto con información básica acerca de perfil de usuario de Hola. Además, para el análisis basado en el tiempo, se mantendría una serie de filas para cada usuario, donde cada fila representa el número de Hola de páginas visitado un usuario concreto dentro de un período de tiempo específico.

![Esquema](./media/sql-database-temporal-tables/AzureTemporal1.png)

Afortunadamente, no es necesario tooput ningún esfuerzo en su aplicación toomaintain esta información de actividad. Con las tablas temporales, se automatiza este proceso - ofrecerle una total flexibilidad durante el diseño de sitio Web y más toofocus de tiempo en el propio análisis de datos Hola. Hola solo lo tienes toodo es tooensure que **WebSiteInfo** tabla está configurada como [temporales con versión del sistema](https://msdn.microsoft.com/library/dn935015.aspx#Anchor_0). los pasos exactos de Hello tooutilize que tablas temporales en este escenario se describen a continuación.

## <a name="step-1-configure-tables-as-temporal"></a>Paso 1: Configurar tablas como temporales
Dependiendo de si inicia un nuevo desarrollo o actualiza una aplicación existente, creará tablas temporales o modificará las existentes agregando atributos temporales. En general, el escenario puede ser una combinación de estas dos opciones. Realice estas acciones utilizando [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) (SSMS), [SQL Server Data Tools](https://msdn.microsoft.com/library/mt204009.aspx) (SSDT) o cualquier otra herramienta de desarrollo de Transact-SQL.

> [!IMPORTANT]
> Se recomienda que siempre utilice Hola versión más reciente de Management Studio tooremain sincronizada con actualizaciones tooMicrosoft Azure y base de datos SQL. [Actualice SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).
> 
> 

### <a name="create-new-table"></a>Creación de una nueva tabla
Use el elemento del menú contextual "Nueva tabla con versiones del sistema" en el editor de consultas de explorador de objetos de SSMS tooopen Hola con una secuencia de comandos de plantilla de tabla temporal y, a continuación, usar plantillas de hello toopopulate "Especificar valores para parámetros de plantilla" (Ctrl + Mayús + M):

![SSMSNewTable](./media/sql-database-temporal-tables/AzureTemporal2.png)

En SSDT, elige la plantilla de "Tabla Temporal (con versiones del sistema)" al agregar el nuevo proyecto de base de datos de toohello de elementos. Que se Diseñador de tablas abiertas y habilitar tooeasily especifique Hola diseño de tabla:

![SSDTNewTable](./media/sql-database-temporal-tables/AzureTemporal3.png)

También puede una tabla temporal crear especificando las instrucciones de Transact-SQL Hola directamente, como se muestra en el siguiente ejemplo de Hola. Tenga en cuenta que Hola elementos obligatorios de todas las tablas temporales son definición del período de Hola y cláusula de hello SYSTEM_VERSIONING con una tabla de usuario de tooanother de referencia que se va a almacenar versiones de filas de historial:

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

Cuando se crea la tabla temporal con versiones del sistema, se crea automáticamente Hola que acompaña a la tabla de historial con la configuración predeterminada de Hola. tabla de historial de Hello predeterminada contiene un índice agrupado de árbol B de columnas de periodo (fin e inicio) Hola habilitada la compresión de página. Esta configuración es óptima para la mayoría de Hola de los escenarios en que se usan las tablas temporales, especialmente para [auditoría de datos](https://msdn.microsoft.com/library/mt631669.aspx#Anchor_0). 

En este caso particular, nuestro objetivo es análisis de tendencias basados en tiempo de tooperform a través de un historial de datos más largo y con los conjuntos de datos más grandes, por lo que la elección de Hola de almacenamiento de tabla de historial de hello es un índice de almacén de columnas agrupado. Un almacén de columnas agrupado proporciona muy buena compresión y rendimiento de consultas analíticas. Dé de tablas temporales Hola índices tooconfigure de flexibilidad en las tablas actual y temporal de hello completamente por separado. 

> [!NOTE]
> Índices de almacén de columnas solo están disponibles en el nivel de servicio premium de Hola.
>

Hola siguiente secuencia de comandos muestra cómo índice predeterminado en la tabla de historial puede ser almacén de columnas modificadas toohello en clúster:

````
CREATE CLUSTERED COLUMNSTORE INDEX IX_WebsiteUserInfoHistory
ON dbo.WebsiteUserInfoHistory
WITH (DROP_EXISTING = ON); 
````

Las tablas temporales se representan en hello Explorador de objetos con icono específico de Hola para facilitar la identificación, mientras que su tabla de historial se muestra como un nodo secundario.

![AlterTable](./media/sql-database-temporal-tables/AzureTemporal4.png)

### <a name="alter-existing-table-tootemporal"></a>ALTER tootemporal de tabla existente
Vamos a cubrir escenario alternativo de hello en qué hello WebsiteUserInfo tabla ya existe, pero no fue diseñado tookeep un historial de cambios. En este caso, simplemente puede ampliar toobecome de tabla existente de hello temporal, como se muestra en el siguiente ejemplo de Hola:

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

## <a name="step-2-run-your-workload-regularly"></a>Paso 2: Ejecutar la carga de trabajo regularmente
Hola principal ventaja de las tablas temporales es que no necesita toochange o ajustar su sitio Web en cualquier seguimiento de cambios de forma tooperform. Una vez creadas, las tablas temporales conservan las versiones de fila anteriores cada vez que realiza modificaciones en los datos. 

En el seguimiento de cambios automático de orden tooleverage para este escenario en particular, vamos a simplemente actualizar la columna **PagesVisited** cada vez que al usuario finaliza la sesión en el sitio Web de hello:

````
UPDATE WebsiteUserInfo  SET [PagesVisited] = 5 
WHERE [UserID] = 1;
````

Es importante toonotice que Hola consulta update no necesita la hora exacta de hello tooknow cuando se produjo la operación real de hello ni cómo se conservarán los datos históricos para su posterior análisis. Ambos aspectos se administran automáticamente Hola base de datos de SQL Azure. Hello diagrama siguiente ilustra cómo se generan los datos de historial en todas las actualizaciones.

![TemporalArchitecture](./media/sql-database-temporal-tables/AzureTemporal5.png)

## <a name="step-3-perform-historical-data-analysis"></a>Paso 3: Realizar análisis de datos históricos
Ahora, cuando el control de versiones del sistema temporal está habilitado, el análisis de datos históricos se realiza con una sola consulta. En este artículo se proporcionan algunos ejemplos que tratan situaciones comunes de análisis - toolearn todos los detalles, explorar diversas opciones que se introdujo con hello [FOR SYSTEM_TIME](https://msdn.microsoft.com/library/dn935015.aspx#Anchor_3) cláusula.

toosee Hola superior 10 usuarios ordenados por número de Hola de páginas web que visita a partir de una hora hace, ejecute esta consulta:

````
DECLARE @hourAgo datetime2 = DATEADD(HOUR, -1, SYSUTCDATETIME());
SELECT TOP 10 * FROM dbo.WebsiteUserInfo FOR SYSTEM_TIME AS OF @hourAgo
ORDER BY PagesVisited DESC
````

Puede modificar fácilmente esta consulta visitas al sitio de Hola de tooanalyze desde hace un día, hace un mes o en cualquier momento Hola anterior desea.

tooperform básica análisis estadísticos para hello día de ayer, Hola de uso siguiente ejemplo:

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

toosearch para las actividades de un usuario específico, en un período de tiempo, use Hola CONTAINED IN cláusula:

````
DECLARE @hourAgo datetime2 = DATEADD(HOUR, -1, SYSUTCDATETIME());
DECLARE @twoHoursAgo datetime2 = DATEADD(HOUR, -2, SYSUTCDATETIME());
SELECT * FROM dbo.WebsiteUserInfo 
FOR SYSTEM_TIME CONTAINED IN (@twoHoursAgo, @hourAgo)
WHERE [UserID] = 1;
````

La visualización de gráficos es especialmente conveniente para consultas temporales, ya que puede mostrar tendencias y patrones de uso de una forma intuitiva muy fácilmente:

![TemporalGraph](./media/sql-database-temporal-tables/AzureTemporal6.png)

## <a name="evolving-table-schema"></a>Evolución del esquema de tabla
Por lo general, deberá esquema de tabla temporal de hello toochange mientras se está realizando el desarrollo de aplicaciones. Para ello, simplemente ejecute instrucciones ALTER TABLE regulares y base de datos de SQL Azure correctamente se propagará a tabla de historial de cambios toohello. Hello secuencia de comandos siguiente muestra cómo se pueden agregar atributos adicionales para el seguimiento de:

````
/*Add new column for tracking source IP address*/
ALTER TABLE dbo.WebsiteUserInfo 
ADD  [IPAddress] varchar(128) NOT NULL CONSTRAINT DF_Address DEFAULT 'N/A';
````

De forma similar, puede cambiar la definición de columna mientras la carga de trabajo esté activa:

````
/*Increase hello length of name column*/
ALTER TABLE dbo.WebsiteUserInfo 
    ALTER COLUMN  UserName nvarchar(256) NOT NULL;
````

Por último, puede quitar una columna que ya no necesite.

````
/*Drop unnecessary column */
ALTER TABLE dbo.WebsiteUserInfo 
    DROP COLUMN TemporaryColumn; 
````

O bien, usar la versión más reciente [SSDT](https://msdn.microsoft.com/library/mt204009.aspx) toochange temporales esquema de tabla mientras estás conectado toohello de base de datos (modo en línea) o como parte del proyecto de base de datos de hello (modo sin conexión).

## <a name="controlling-retention-of-historical-data"></a>Control de la retención de datos históricos
Con las tablas temporales con versión del sistema, tabla de historial de hello puede aumentar el tamaño de la base de datos de hello más de las tablas normales. Una tabla de historial de gran tamaño y creciente puede ser un problema debido a los costos de almacenamiento de toopure así como la imposición de un rendimiento impuesto sobre las consultas temporales. Por lo tanto, al desarrollar una directiva de retención de datos para administrar los datos en la tabla de historial de hello es un aspecto importante de planeación y la administración del ciclo de vida de Hola de cada tabla temporal. Con la base de datos de SQL Azure, deberá Hola siguientes enfoques para administrar los datos históricos de la tabla temporal de hello:

* [Partición de tabla](https://msdn.microsoft.com/library/mt637341.aspx#Anchor_2)
* [Script de limpieza personalizado](https://msdn.microsoft.com/library/mt637341.aspx#Anchor_3)

## <a name="next-steps"></a>Pasos siguientes
Para obtener información detallada sobre tablas temporales, consulte la [documentación de MSDN](https://msdn.microsoft.com/library/dn935015.aspx).
Visita Channel 9 toohear una [historia de éxito de implementación temporal de clientes reales](https://channel9.msdn.com/Blogs/jsturtevant/Azure-SQL-Temporal-Tables-with-RockStep-Solutions) inspección y un [live demostración temporal](https://channel9.msdn.com/Shows/Data-Exposed/Temporal-in-SQL-Server-2016).

