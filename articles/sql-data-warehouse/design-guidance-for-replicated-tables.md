---
title: "Guía de aaaDesign para replica tablas - almacenamiento de datos de SQL Azure | Documentos de Microsoft"
description: "Recomendaciones para el diseño de tablas replicadas en el esquema de Azure SQL Data Warehouse."
services: sql-data-warehouse
documentationcenter: NA
author: ronortloff
manager: jhubbard
editor: 
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 07/14/2017
ms.author: rortloff;barbkess
ms.openlocfilehash: 5d405b8c404c65177b387ba959126839c1cf8799
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="design-guidance-for-using-replicated-tables-in-azure-sql-data-warehouse"></a>Instrucciones de diseño para el uso de tablas replicadas en Azure SQL Data Warehouse
En este artículo se proporcionan recomendaciones para el diseño de tablas replicadas en el esquema de SQL Data Warehouse. Utilice estas recomendaciones tooimprove consulta las del rendimiento al reducir la complejidad de movimiento y la consulta de datos.

> [!NOTE]
> característica de tabla replicada Hola está actualmente en versión preliminar pública. Algunos comportamientos son toochange de asunto.
> 

## <a name="prerequisites"></a>Requisitos previos
En este artículo se da por supuesto que está familiarizado con los conceptos de distribución y movimiento de datos en SQL Data Warehouse.  Para más información, vea [Datos distribuidos](sql-data-warehouse-distributed-data.md). 

Como parte del diseño de tabla, comprender tanto como sea posible sobre los datos y cómo se consultan datos Hola.  Por ejemplo, considere estas preguntas:

- ¿Qué tamaño tiene tabla Hola?   
- ¿Con qué frecuencia se actualiza la tabla de hello?   
- ¿Tiene tablas de hechos y dimensiones en un almacenamiento de datos?   

## <a name="what-is-a-replicated-table"></a>¿Qué es una tabla replicada?
Una tabla replicada tiene una copia completa de la tabla de hello accesible en cada nodo de ejecución. Replicación de una tabla quita los datos de tootransfer de necesidad de hello entre los nodos de proceso antes de una combinación o una agregación. Puesto que la tabla de hello tiene varias copias, las tablas replicadas funcionan mejor cuando el tamaño de la tabla de hello es inferior a 2 GB comprimido.

Hello siguiente diagrama muestra una tabla replicada que sea accesible en cada nodo de ejecución. En el almacén de datos de SQL, tabla replicada hello es tooa copiado totalmente la base de datos de distribución en cada nodo de ejecución. 

![Tabla replicada](media/guidance-for-using-replicated-tables/replicated-table.png "Tabla replicada")  

Las tablas replicadas funcionan correctamente para tablas de dimensiones pequeñas de un esquema de estrella. Tablas de dimensiones suelen ser de un tamaño que hace más factible toostore y mantienen varias copias. Las dimensiones almacenan datos descriptivos que cambian lentamente, como el nombre y la dirección del cliente, y detalles del producto. Hola de variación lenta la naturaleza de los datos de hello conduce toofewer vuelve a generar de tabla replicada Hola. 

Considere la posibilidad de usar una tabla replicada cuando:

- tamaño de la tabla de Hello en el disco es inferior a 2 GB, independientemente del número de Hola de filas. tamaño de hello toofind de una tabla, puede usar hello [DBCC PDW_SHOWSPACEUSED](https://docs.microsoft.com/en-us/sql/t-sql/database-console-commands/dbcc-pdw-showspaceused-transact-sql) comando: `DBCC PDW_SHOWSPACEUSED('ReplTableCandidate')`. 
- tabla de Hola se utiliza en las combinaciones que en caso contrario requerirían el movimiento de datos. Por ejemplo, una combinación en las tablas hash distribuida requiere el movimiento de datos cuando las columnas de combinación de hello no son Hola misma columna de distribución. Si una de las tablas hash está distribuido de Hola es pequeña, considere la posibilidad de una tabla replicada. Una combinación en una tabla Round Robin requiere movimiento de datos. Se recomienda usar tablas replicadas en lugar de tablas Round Robin en la mayoría de los casos. 


Considere la posibilidad de convertir una existente distribuidas tooa tabla replicada tabla cuando:

- Operaciones de movimiento de datos de uso que difunden nodos de proceso de hello datos tooall Hola los planes de consulta. Hola BroadcastMoveOperation es caro y reduce el rendimiento de las consultas. tooview las operaciones de movimiento de datos en los planes de consulta, use [sys.dm_pdw_request_steps](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql).
 
Las tablas replicadas no pueden obtener el mejor rendimiento de consultas hello cuando:

- tabla de Hello tiene frecuentes de inserción, actualización y eliminación de las operaciones. Estas operaciones de DML (lenguaje) de manipulación de datos requieren una recompilación de la tabla de hello replicado. La recompilación puede provocar con frecuencia un rendimiento más lento.
- almacenamiento de datos de Hola se escala con frecuencia. Ajuste de escala en un almacén de datos cambia el número de Hola de nodos de cálculo, que implica una recompilación.
- tabla de Hello tiene un gran número de columnas, pero las operaciones de datos normalmente tienen acceso a solo un número pequeño de columnas. En este escenario, en lugar de replicar Hola toda la tabla, puede que sea más eficaz toohash distribuir tabla hello y, a continuación, crear un índice en columnas de hello accede con frecuencia. Si una consulta requiere el movimiento de datos, almacenamiento de datos de SQL solo mueve los datos en hello solicitan columnas. 



## <a name="use-replicated-tables-with-simple-query-predicates"></a>Usar tablas replicadas con predicados de consulta simples
Antes de elegir toodistribute o duplica una tabla, piense en tipos de Hola de consultas que tiene previsto toorun contra la tabla Hola. Siempre que sea posible,

- Use tablas replicadas para consultas con predicados de consulta simples, como los de igualdad o desigualdad.
- Use tablas replicadas para consultas con predicados de consulta complejos, como los de LIKE o NOT LIKE.

Las consultas que consumen más CPU demostrar un mejor cuándo se distribuye el trabajo de hello en todos los nodos de proceso de Hola. Por ejemplo, las consultas que ejecutan cálculos en todas las filas de una tabla funcionan mejor en tablas distribuidas que en tablas replicadas. Puesto que una tabla replicada se almacena por completo en cada nodo de proceso, una consulta de la CPU en una tabla replicada se ejecuta en toda la tabla hello en cada nodo de ejecución. Hello cálculo adicional puede ralentizar el rendimiento de las consultas.

Por ejemplo, esta consulta tiene un predicado complejo.  Se ejecuta con mayor rapidez cuando el proveedor está una tabla distribuida en lugar de una tabla replicada. En este ejemplo, el proveedor se puede distribuir por hash o mediante el método Round Robin.

```sql

SELECT EnglishProductName 
FROM DimProduct 
WHERE EnglishDescription LIKE '%frame%comfortable%'

```

## <a name="convert-existing-round-robin-tables-tooreplicated-tables"></a>Convertir tablas de tooreplicated round robin tablas existentes
Si ya tiene tablas round robin, se recomienda convertirlas tooreplicated tablas si cumplen con los criterios que se describen en este artículo. Las tablas replicadas mejoran el rendimiento en tablas de round-robin porque eliminan la necesidad de hello para el movimiento de datos.  Una tabla Round Robin siempre requiere movimiento de datos para las combinaciones. 

Este ejemplo se utiliza [CTAS](https://docs.microsoft.com/sql/t-sql/statements/create-table-as-select-azure-sql-data-warehouse) toochange hello DimSalesTerritory tabla tooa tabla replicada. Este ejemplo funciona independientemente de si DimSalesTerritory se distribuye por hash o Round Robin.

```sql
CREATE TABLE [dbo].[DimSalesTerritory_REPLICATE]   
WITH   
  (   
    CLUSTERED COLUMNSTORE INDEX,  
    DISTRIBUTION = REPLICATE  
  )  
AS SELECT * FROM [dbo].[DimSalesTerritory]
OPTION  (LABEL  = 'CTAS : DimSalesTerritory_REPLICATE') 

--Create statistics on new table
CREATE STATISTICS [SalesTerritoryKey] ON [DimSalesTerritory_REPLICATE] ([SalesTerritoryKey]);
CREATE STATISTICS [SalesTerritoryAlternateKey] ON [DimSalesTerritory_REPLICATE] ([SalesTerritoryAlternateKey]);
CREATE STATISTICS [SalesTerritoryRegion] ON [DimSalesTerritory_REPLICATE] ([SalesTerritoryRegion]);
CREATE STATISTICS [SalesTerritoryCountry] ON [DimSalesTerritory_REPLICATE] ([SalesTerritoryCountry]);
CREATE STATISTICS [SalesTerritoryGroup] ON [DimSalesTerritory_REPLICATE] ([SalesTerritoryGroup]);

-- Switch table names
RENAME OBJECT [dbo].[DimSalesTerritory] too[DimSalesTerritory_old];
RENAME OBJECT [dbo].[DimSalesTerritory_REPLICATE] too[DimSalesTerritory];

DROP TABLE [dbo].[DimSalesTerritory_old];
```  

### <a name="query-performance-example-for-round-robin-versus-replicated"></a>Ejemplo de rendimiento de consultas para tablas Round Robin frente a tablas replicadas 

Una tabla replicada no requiere ningún movimiento de datos para las combinaciones porque toda la tabla Hola ya está presente en cada nodo de ejecución. Si las tablas de dimensiones Hola son round-robin distribuida, una combinación copia tabla de dimensiones de hello en el nodo de proceso de tooeach completa. datos de hello toomove, plan de consulta de hello contiene una operación llamada BroadcastMoveOperation. Este tipo de operación de movimiento de datos reduce el rendimiento de las consultas y se elimina mediante el uso de tablas replicadas. pasos del plan de consulta de tooview, usar hello [sys.dm_pdw_request_steps](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql) vista de catálogo del sistema. 

Por ejemplo, en la siguiente consulta en el esquema de AdventureWorks de hello, Hola ` FactInternetSales` tabla es distribuidas de hash. Hola `DimDate` y `DimSalesTerritory` tablas son tablas de dimensión más pequeñas. Esta consulta devuelve las ventas totales de hello en América del Norte para el año fiscal 2004:
 
```sql
SELECT [TotalSalesAmount] = SUM(SalesAmount)
FROM dbo.FactInternetSales s
INNER JOIN dbo.DimDate d
  ON d.DateKey = s.OrderDateKey
INNER JOIN dbo.DimSalesTerritory t
  ON t.SalesTerritoryKey = s.SalesTerritoryKey
WHERE d.FiscalYear = 2004
  AND t.SalesTerritoryGroup = 'North America'
```
Se vuelve a crear `DimDate` y `DimSalesTerritory` como tablas Round Robin. Como resultado, consulta Hola mostró Hola siguiendo el plan de consulta, que tiene varios difusión mover operaciones: 
 
![Plan de consulta de round robin](media/design-guidance-for-replicated-tables/round-robin-tables-query-plan.jpg) 

Se vuelve a crear `DimDate` y `DimSalesTerritory` como tablas replicadas y se ejecutó consulta Hola de nuevo. plan de consulta resultante de Hello es mucho más corta y no haya ninguno emita se mueve.

![Plan de consulta replicado](media/design-guidance-for-replicated-tables/replicated-tables-query-plan.jpg) 


## <a name="performance-considerations-for-modifying-replicated-tables"></a>Consideraciones de rendimiento para modificar tablas replicadas
Almacenamiento de datos de SQL se implementa una tabla replicada manteniendo una versión principal de la tabla de Hola. Copia Hola de base de datos de distribución de tooone versión maestra en cada nodo de ejecución. Cuando se produce un cambio, almacenamiento de datos de SQL actualiza primero la tabla maestra de Hola. Requiere una recompilación de las tablas de hello en cada nodo de ejecución. Una recompilación de una tabla replicada incluye copiar Hola tabla tooeach de nodos de proceso y, a continuación, volver a generar índices Hola.

Las recompilaciones son necesarias después de que:
- Se carguen o modifiquen datos.
- almacén de datos de Hello es configuración diferente de la unidad de escala tooa
- Se actualice la definición de tabla

Las recompilaciones no son necesarias después de que:
- Se pause la operación.
- Se reanude la operación.

Hola regeneración no se produce inmediatamente después de que se modifican los datos. En su lugar, se desencadena la regeneración de Hola Hola la primera vez que selecciona una consulta de tabla de Hola.  Dentro de la instrucción select inicial de Hola de tabla de Hola son tabla replicada de pasos toorebuild Hola.  Puesto Hola regeneración se realiza dentro de la consulta de hello, instrucción select de la inicial de toohello Hola impacto podría ser significativa en función del tamaño de Hola de tabla de Hola.  Si varias tablas replicadas intervienen que necesitan una recompilación, cada copia se vuelven a generar en serie como pasos dentro de la instrucción de Hola.  coherencia de los datos toomaintain durante la regeneración de Hola de hello replica tabla que se toma un bloqueo exclusivo en la tabla de Hola.  Hola bloqueo impide la tabla de toohello de acceso a todos los dure Hola Hola recompilación. 

### <a name="use-indexes-conservatively"></a>Usar índices de manera conservadora
Prácticas recomendadas de indización estándares aplicarán tooreplicated tablas. Almacenamiento de datos SQL se vuelve a generar cada índice de tabla replicada como parte de la reconstrucción de Hola. Usar solo índices al aumento del rendimiento Hola supera con creces costo Hola de regeneración de índices de Hola.  
 
### <a name="batch-data-loads"></a>Cargas de datos por lotes
Al cargar datos en las tablas replicadas, intente toominimize vuelve a generar por lotes cargas juntos. Realizar todas las cargas de Hola por lotes antes de ejecutar las instrucciones select.

Por ejemplo, en este modelo de carga se cargan datos de cuatro orígenes y se invocan cuatro recompilaciones. 

- Carga desde el origen 1.
- La instrucción de selección desencadena la recompilación 1.
- Carga desde el origen 2.
- La instrucción de selección desencadena la recompilación 2.
- Carga desde el origen 3.
- La instrucción de selección desencadena la recompilación 3.
- Carga desde el origen 4.
- La instrucción de selección desencadena la recompilación 4.

Por ejemplo, en este modelo de carga se cargan datos de cuatro orígenes pero solo se invoca una recompilación.

- Carga desde el origen 1.
- Carga desde el origen 2.
- Carga desde el origen 3.
- Carga desde el origen 4.
- La instrucción de selección desencadena la recompilación.


### <a name="rebuild-a-replicated-table-after-a-batch-load"></a>Recompilar una tabla replicada después de una carga por lotes
tooensure los tiempos de ejecución de consulta coherentes, se recomienda forzar una actualización de tablas de saludo replican después de una carga por lotes. En caso contrario, primera consulta de hello debe esperar Hola tablas toorefresh, que incluye volver a generar índices Hola. Según el tamaño de Hola y el número de tablas replicadas afectados, impacto en el rendimiento Hola puede ser significativa.  

Esta consulta utiliza hello [sys.pdw_replicated_table_cache_state](https://docs.microsoft.com/sql/relational-databases/system-catalog-views/sys-pdw-replicated-table-cache-state-transact-sql) Hola de toolist DMV replica tablas que se han modificado, pero no vuelve a generar.

```sql 
SELECT [ReplicatedTable] = t.[name]
  FROM sys.tables t  
  JOIN sys.pdw_replicated_table_cache_state c  
    ON c.object_id = t.object_id 
  JOIN sys.pdw_table_distribution_properties p 
    ON p.object_id = t.object_id 
  WHERE c.[state] = 'NotReady'
    AND p.[distribution_policy_desc] = 'REPLICATE'
```
 
tooforce una recompilación, ejecute hello sigue instrucción en cada tabla de hello anterior de salida. 

```sql
SELECT TOP 1 * FROM [ReplicatedTable]
``` 
 
## <a name="next-steps"></a>Pasos siguientes 
toocreate una tabla replicada, use una de estas instrucciones:

- [CREATE TABLE (Azure SQL Data Warehouse)](https://docs.microsoft.com/sql/t-sql/statements/create-table-azure-sql-data-warehouse)
- [CREATE TABLE AS SELECT (Azure SQL Data Warehouse](https://docs.microsoft.com/sql/t-sql/statements/create-table-as-select-azure-sql-data-warehouse)

Para obtener información general de las tablas distribuidas, vea [tablas distribuidas](sql-data-warehouse-tables-distribute.md).



