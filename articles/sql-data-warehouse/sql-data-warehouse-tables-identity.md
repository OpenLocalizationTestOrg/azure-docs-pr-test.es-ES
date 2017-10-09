---
title: las claves suplentes de aaaCreate mediante identidad | Documentos de Microsoft
description: "Obtenga información acerca de cómo las claves suplentes de toouse identidad toocreate en las tablas."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: faa1034d-314c-4f9d-af81-f5a9aedf33e4
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 06/13/2017
ms.author: jrj;barbkess
ms.openlocfilehash: 502cdd2b510b229b2a19c1f78b11862a7386ae3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-surrogate-keys-by-using-identity"></a>Creación de claves suplentes mediante IDENTITY
> [!div class="op_single_selector"]
> * [Información general][Overview]
> * [Tipos de datos][Data Types]
> * [Distribución][Distribute]
> * [Índice][Index]
> * [Partición][Partition]
> * [Estadísticas][Statistics]
> * [Temporal][Temporary]
> * [Identidad][Identity]
> 
> 

Muchos de los modeladores de datos, como las claves suplentes de toocreate en sus tablas cuando diseñan modelos de almacenamiento de datos. Puede usar tooachieve de propiedad de identidad de hello este objetivo simple y eficaz sin afectar al rendimiento de carga. 

## <a name="get-started-with-identity"></a>Introducción a IDENTITY
Puede definir una tabla como con la propiedad de identidad de hello cuando primero crear tabla de hello mediante la sintaxis que sea similar toohello siguiente instrucción:

```sql
CREATE TABLE dbo.T1
(   C1 INT IDENTITY(1,1) NOT NULL
,   C2 INT NULL
)
WITH
(   DISTRIBUTION = HASH(C2)
,   CLUSTERED COLUMNSTORE INDEX
)
;
```

A continuación, puede usar `INSERT..SELECT` tabla de hello toopopulate.

## <a name="behavior"></a>Comportamiento
Hola propiedad IDENTITY es diseñada tooscale out en todas las distribuciones de Hola Hola almacenamiento de datos sin afectar al rendimiento de carga. Por lo tanto, la implementación de Hola de identidad es orientada a lograr estos objetivos. Esta sección resalta los matices de Hola de hello implementación toohelp entienda más completa.  

### <a name="allocation-of-values"></a>Asignación de valores
Hola propiedad IDENTITY no garantiza el orden de hello en qué Hola se asignan los valores de suplente, que reflejan el comportamiento de Hola de SQL Server y base de datos de SQL Azure. Sin embargo, en el almacén de datos de SQL Azure, ausencia de Hola de garantía es mayor. 

Hola siguiente ejemplo es una ilustración:

```sql
CREATE TABLE dbo.T1
(   C1 INT IDENTITY(1,1)    NOT NULL
,   C2 VARCHAR(30)              NULL
)
WITH
(   DISTRIBUTION = HASH(C2)
,   CLUSTERED COLUMNSTORE INDEX
)
;

INSERT INTO dbo.T1
VALUES (NULL);

INSERT INTO dbo.T1
VALUES (NULL);

SELECT *
FROM dbo.T1;

DBCC PDW_SHOWSPACEUSED('dbo.T1');
```

En el anterior ejemplo de Hola, dos filas desembarquen en la distribución de 1. primera fila de Hello tiene el valor de suplente de Hola de 1 en la columna `C1`, y Hola segunda fila tiene el valor de suplente de Hola de 61. Estos dos valores generados por hello propiedad IDENTITY. Sin embargo, la asignación de Hola de valores de hello no es contiguo. Este comportamiento es así por diseño.

### <a name="skewed-data"></a>Datos sesgados 
intervalo de Hola de valores de tipo de datos de hello están repartidos por igual entre las distribuciones de Hola. Si se produce una tabla distribuida de datos sesgados, Hola, a continuación, el intervalo de valores disponibles toohello tipo de datos se puede agotar prematuramente. Por ejemplo, si todos los datos de hello terminan en una sola distribución, a continuación, eficazmente Hola tabla tiene acceso tooonly sesentavo de uno de los valores de Hola Hola del tipo de datos. Por esta razón, Hola propiedad de identidad se limita demasiado`INT` y `BIGINT` sólo los tipos de datos.

### <a name="selectinto"></a>SELECT..INTO
Cuando se selecciona una columna de identidad existente en una tabla nueva, Hola nueva columna hereda propiedades de identidad de hello, a menos que una de hello condiciones siguientes es verdadera:
- instrucción SELECT de Hello contiene una combinación.
- Varias instrucciones SELECT se combinan mediante UNION.
- columna de identidad de Hello aparece más de una vez en la lista de selección de Hola.
- columna de identidad de Hello es parte de una expresión.
    
Si alguna de estas condiciones es true, columna Hola se crea NOT NULL en lugar de heredar la propiedad IDENTITY de Hola.

### <a name="create-table-as-select"></a>CREATE TABLE AS SELECT
Crear tabla AS seleccione (CTAS) sigue Hola mismo comportamiento SQL Server que se documenta para SELECT... A. Sin embargo, no se puede especificar una propiedad de identidad en la definición de columna de Hola de hello `CREATE TABLE` forma parte de la instrucción de Hola. Tampoco puede utilizar función de identidad de hello en hello `SELECT` forma parte de hello CTAS. toopopulate una tabla, deberá toouse `CREATE TABLE` seguido de la tabla de hello toodefine `INSERT..SELECT` toopopulate lo.

## <a name="explicitly-insert-values-into-an-identity-column"></a>Inserción explícita de valores en una columna IDENTITY 
SQL Data Warehouse admite la sintaxis `SET IDENTITY_INSERT <your table> ON|OFF`. Puede usar este sintaxis tooexplicitly insertar los valores en la columna de identidad de Hola.

Muchos modeladores de datos como toouse predefinidos negativo para ciertos valores de filas en sus dimensiones. Un ejemplo es Hola -1 o fila de "miembro desconocido". 

script de Hola siguiente muestra cómo tooexplicitly agrega esta fila mediante el uso de SET IDENTITY_INSERT:

```sql
SET IDENTITY_INSERT dbo.T1 ON;

INSERT INTO dbo.T1
(   C1
,   C2
)
VALUES (-1,'UNKNOWN')
;

SET IDENTITY_INSERT dbo.T1 OFF;

SELECT  *
FROM    dbo.T1
;
```    

## <a name="load-data-into-a-table-with-identity"></a>Carga de datos en una tabla con IDENTITY

presencia de Hola de hello propiedad de identidad tiene algún código de carga de datos de tooyour implicaciones. En esta sección se resaltan algunos patrones básicos para cargar datos en tablas mediante IDENTITY. 

### <a name="load-data-with-polybase"></a>Carga de datos con PolyBase
datos de tooload en una tabla y generar una clave suplente mediante el uso de identidad, crear tabla de hello y, a continuación, utilice INSERT... SELECT o INSERT... VALORES tooperform Hola carga.

Hello en el ejemplo siguiente se resalta patrón básico de hello:
 
```sql
--CREATE TABLE with IDENTITY
CREATE TABLE dbo.T1
(   C1 INT IDENTITY(1,1)
,   C2 VARCHAR(30)
)
WITH
(   DISTRIBUTION = HASH(C2)
,   CLUSTERED COLUMNSTORE INDEX
)
;

--Use INSERT..SELECT toopopulate hello table from an external table
INSERT INTO dbo.T1
(C2)
SELECT  C2
FROM    ext.T1
;

SELECT  *
FROM    dbo.T1
;

DBCC PDW_SHOWSPACEUSED('dbo.T1');
```

> [!NOTE] 
> No es posible toouse `CREATE TABLE AS SELECT` actualmente al cargar datos en una tabla con una columna de identidad.
> 

Para obtener más información sobre cómo cargar datos mediante el uso de la herramienta de programa de (copia masiva BCP) de copia masiva de hello, vea Hola siguientes artículos:

- [Carga con PolyBase][]
- [Procedimientos recomendados para PolyBase][]

### <a name="load-data-with-bcp"></a>Carga de datos con BCP
BCP es una herramienta de línea de comandos que puede utilizar datos de tooload en almacenamiento de datos de SQL. Uno de sus parámetros (-E) controles Hola comportamiento de BCP al cargar datos en una tabla con una columna de identidad. 

Cuando se especifica -E, se conservan los valores de hello mantenidos en archivo de entrada de hello para la columna de hello con la identidad. Si es -E *no* se especifica, se omiten los valores de hello en esta columna. Si no se incluye la columna de identidad de hello, datos de Hola se cargan con normalidad. se generan valores de Hello según la directiva de incremento y el valor de inicialización de toohello de propiedad Hola.

Para obtener más información sobre cómo cargar datos mediante la utilidad BCP, vea Hola siguientes artículos:

- [Carga con BCP][]
- [BCP en MSDN][]

## <a name="catalog-views"></a>Vistas de catálogo
Almacenamiento de datos SQL admite hello `sys.identity_columns` vista de catálogo. Esta vista puede ser tooidentify usa una columna que tiene la propiedad de identidad de Hola.

toohelp se comprender mejor el esquema de base de datos de hello, este ejemplo se muestra cómo toointegrate `sys.identity_columns` con otras vistas de catálogo del sistema:

```sql
SELECT  sm.name
,       tb.name
,       co.name
,       CASE WHEN ic.column_id IS NOT NULL
             THEN 1
        ELSE 0
        END AS is_identity 
FROM        sys.schemas AS sm
JOIN        sys.tables  AS tb           ON  sm.schema_id = tb.schema_id
JOIN        sys.columns AS co           ON  tb.object_id = co.object_id
LEFT JOIN   sys.identity_columns AS ic  ON  co.object_id = ic.object_id
                                        AND co.column_id = ic.column_id
WHERE   sm.name = 'dbo'
AND     tb.name = 'T1'
;
```

## <a name="limitations"></a>Limitaciones
Hola propiedad IDENTITY no se puede usar en hello los escenarios siguientes:
- En tipo de datos de columna de hello no es INT o BIGINT
- Donde la columna de hello también es la clave de distribución de Hola
- En la tabla hello es una tabla externa 

Hola siguientes funciones relacionadas no se admite en el almacén de datos de SQL:

- [IDENTITY()][]
- [@@IDENTITY][]
- [SCOPE_IDENTITY][]
- [IDENT_CURRENT][]
- [IDENT_INCR][]
- [IDENT_SEED][]
- [DBCC CHECK_IDENT()][]

## <a name="tasks"></a>Tareas

Esta sección proporciona ejemplos de código puede usar tareas comunes de tooperform cuando se trabaja con las columnas de identidad.

> [!NOTE] 
> Columna C1 es hello identidad Hola todas las siguientes tareas.
> 
 
### <a name="find-hello-highest-allocated-value-for-a-table"></a>Buscar el valor de hello más alto asignado para una tabla
Hola de uso `MAX()` función toodetermine Hola valor más alto asignado para una tabla distribuida:

```sql
SELECT  MAX(C1)
FROM    dbo.T1
``` 

### <a name="find-hello-seed-and-increment-for-hello-identity-property"></a>Busque Hola inicialización e incremento Hola propiedad IDENTITY
Puede usar Hola catálogo vistas toodiscover Hola identidad de incremento y valor de inicialización de valores de configuración para una tabla mediante Hola después de consulta: 

```sql
SELECT  sm.name
,       tb.name
,       co.name
,       ic.seed_value
,       ic.increment_value 
FROM        sys.schemas AS sm
JOIN        sys.tables  AS tb           ON  sm.schema_id = tb.schema_id
JOIN        sys.columns AS co           ON  tb.object_id = co.object_id
JOIN        sys.identity_columns AS ic  ON  co.object_id = ic.object_id
                                        AND co.column_id = ic.column_id
WHERE   sm.name = 'dbo'
AND     tb.name = 'T1'
;
```

## <a name="next-steps"></a>Pasos siguientes

* toolearn más sobre el desarrollo de tablas, vea [información general de la tabla][Overview], [tipos de datos de tabla][Data Types], [distribuir una tabla] [ Distribute], [Una tabla de índice][Index], [crear particiones de una tabla][Partition], y [ Tablas temporales][Temporary]. 
* Para más información sobre los procedimientos recomendados, vea [Procedimientos recomendados para SQL Data Warehouse][SQL Data Warehouse Best Practices].  

<!--Image references-->

<!--Article references-->
[Overview]: ./sql-data-warehouse-tables-overview.md
[Data Types]: ./sql-data-warehouse-tables-data-types.md
[Distribute]: ./sql-data-warehouse-tables-distribute.md
[Index]: ./sql-data-warehouse-tables-index.md
[Partition]: ./sql-data-warehouse-tables-partition.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary]: ./sql-data-warehouse-tables-temporary.md
[Identity]: ./sql-data-warehouse-tables-identity.md
[SQL Data Warehouse Best Practices]: ./sql-data-warehouse-best-practices.md

[Carga con BCP]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-with-bcp/
[Carga con PolyBase]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-from-azure-blob-storage-with-polybase/
[Procedimientos recomendados para PolyBase]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-polybase-guide/


<!--MSDN references-->
[Identity property]: https://msdn.microsoft.com/library/ms186775.aspx
[sys.identity_columns]: https://msdn.microsoft.com/library/ms187334.aspx
[IDENTITY()]: https://msdn.microsoft.com/library/ms189838.aspx
[@@IDENTITY]: https://msdn.microsoft.com/library/ms187342.aspx
[SCOPE_IDENTITY]: https://msdn.microsoft.com/library/ms190315.aspx
[IDENT_CURRENT]: https://msdn.microsoft.com/library/ms175098.aspx
[IDENT_INCR]: https://msdn.microsoft.com/library/ms189795.aspx
[IDENT_SEED]: https://msdn.microsoft.com/library/ms189834.aspx
[DBCC CHECK_IDENT()]: https://msdn.microsoft.com/library/ms176057.aspx

[BCP en MSDN]: https://msdn.microsoft.com/library/ms162802.aspx
  

<!--Other Web references-->  
