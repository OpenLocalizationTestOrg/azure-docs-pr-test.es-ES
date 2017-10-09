---
title: "vistas de aaaUsing T-SQL en el almacén de datos de SQL de Azure | Documentos de Microsoft"
description: Sugerencias para usar las vistas Transact-SQL en el Almacenamiento de datos SQL Azure para desarrollar soluciones.
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: b5208f32-8f4a-4056-8788-2adbb253d9fd
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 3990b133946621691bdfa4b09523d21867470c74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="views-in-sql-data-warehouse"></a>Vistas en el Almacenamiento de datos SQL
Las vistas son especialmente útiles en el Almacenamiento de datos SQL. Que se puedan utilizar en un número de maneras diferentes tooimprove Hola de calidad de la solución.  Este artículo resalta algunos ejemplos de cómo tooenrich la solución con vistas, así como las limitaciones de Hola que necesitan toobe considera.

> [!NOTE]
> En este artículo no se explica la sintaxis de `CREATE VIEW`. Consulte toohello [CREATE VIEW] [ CREATE VIEW] artículo de MSDN para obtener esta información de referencia.
> 
> 

## <a name="architectural-abstraction"></a>Abstracción de arquitectura
Un modelo de aplicación muy común es toore-crear tablas mediante Crear tabla AS seleccione (CTAS) seguido por un objeto de cambiar el nombre de modelo durante la carga de datos.

ejemplo de Hola siguiente agrega dimensión de fecha nuevos registros tooa date. Tenga en cuenta cómo un nuevo tabble, DimDate_New, se crea por primera vez y, a continuación, cambiar el nombre de versión original de hello tooreplace de tabla Hola.

```sql
CREATE TABLE dbo.DimDate_New
WITH (DISTRIBUTION = ROUND_ROBIN
, CLUSTERED INDEX (DateKey ASC)
)
AS
SELECT *
FROM   dbo.DimDate  AS prod
UNION ALL
SELECT *
FROM   dbo.DimDate_stg AS stg
;

RENAME OBJECT DimDate tooDimDate_Old;
RENAME OBJECT DimDate_New tooDimDate;

```

Sin embargo, este enfoque puede provocar que las tablas aparezcan y desaparezcan de la vista del usuario, así como mensajes de error del tipo "la tabla no existe". Vistas pueden ser usuarios de tooprovide usado con una capa de presentación coherente mientras se cambia el nombre de los objetos subyacentes de Hola. Proporcionando acceso a los usuarios toohello datos a través de una vista, significa que los usuarios no tienen visibilidad toohave de tablas subyacentes de Hola. Esto proporciona una experiencia coherente al usuario y garantizar que los diseñadores de almacenes de datos de hello pueden evolucionar modelo de datos de Hola y maximizar el rendimiento mediante el uso de CTAS durante el proceso de carga de datos de Hola.    

## <a name="performance-optimization"></a>Optimización del rendimiento
Vistas también pueden ser usadas tooenforce rendimiento optimizado combinaciones entre tablas. Por ejemplo, una vista puede incorporar una clave de distribución redundante como parte del programa Hola a unir el movimiento de datos de toominimize de criterios.  Otra ventaja de una vista podría ser tooforce una consulta específica o una sugerencia de combinación. Mediante vistas de esta manera se garantiza que las combinaciones se realizan siempre de forma óptima, evitando la necesidad de hello for (construcción correcta hello) a los usuarios tooremember para sus combinaciones.

## <a name="limitations"></a>Limitaciones
Las vistas en el almacenamiento de datos SQL son solo metadatos.  Por consiguiente Hola siguientes opciones no está disponible:

* No hay ninguna opción de enlace de esquema.
* Tablas base no se puede actualizar a través de la vista de Hola
* No se pueden crear vistas en tablas temporales.
* No hay compatibilidad para hello expandir / sugerencias NOEXPAND
* No hay ninguna vista indexada en Almacenamiento de datos SQL.

## <a name="next-steps"></a>Pasos siguientes
Para obtener más sugerencias sobre desarrollo, consulte la [información general sobre desarrollo de Almacenamiento de datos SQL][SQL Data Warehouse development overview].
Para `CREATE VIEW` sintaxis consulte demasiado[CREATE VIEW][CREATE VIEW].

<!--Image references-->

<!--Article references-->
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[CREATE VIEW]: https://msdn.microsoft.com/en-us/library/ms187956.aspx

<!--Other Web references-->
