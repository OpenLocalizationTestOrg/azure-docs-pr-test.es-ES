---
title: "aaaLeverage T-SQL bucles en el almacén de datos de SQL de Azure | Documentos de Microsoft"
description: Sugerencias para los bucles de Transact-SQL en Almacenamiento de datos SQL de Azure para el desarrollo de soluciones.
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: f3384b81-b943-431b-bc73-90e47e4c195f
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: c7e8f71b910d00d0dfc30f6e5eba190fd05014b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="loops-in-sql-data-warehouse"></a>Bucles en Almacenamiento de datos SQL
Almacenamiento de datos SQL admite hello [mientras][mientras] bucle para ejecutar repetidamente los bloques de instrucciones. Esta operación continuará para mientras Hola especifica las condiciones son true o hasta que código de hello termina específicamente bucle de hello mediante hello `BREAK` palabra clave. Los bucles son especialmente útiles para reemplazar los cursores definidos en código SQL. Afortunadamente, casi todos los cursores que se escriben en el código SQL son de hello rápido hacia delante, de lectura solo diversos. Por lo tanto, [mientras] bucles son una buena alternativa si descubre que tiene que tener tooreplace uno.

## <a name="leveraging-loops-and-replacing-cursors-in-sql-data-warehouse"></a>Aprovechamiento de bucles y sustitución de cursores en Almacenamiento de datos SQL
Sin embargo, antes de adentrarnos en head en primer lugar debe pregúntese lo siguiente: Hola siguiente pregunta: "este cursor se pudo volver a escribirse toouse operaciones basadas en conjuntos?". En muchos casos respuesta Hola será Sí y a menudo es más recomendable Hola. Una operación basada en conjunto a menudo se realiza bastante más rápido que un enfoque iterativo, fila a fila.

Los cursores de avance rápido y solo lectura se pueden reemplazar fácilmente por una construcción de bucle. A continuación se muestra un ejemplo sencillo: Este ejemplo de código actualiza las estadísticas de Hola para todas las tablas de base de datos de Hola. Una iteración sobre tablas de hello en bucle Hola se está tooexecute capaz de cada comando de la secuencia.

En primer lugar, cree una tabla temporal que contiene una fila única número tooidentify usado Hola instrucciones individuales:

```
CREATE TABLE #tbl
WITH
( DISTRIBUTION = ROUND_ROBIN
)
AS
SELECT  ROW_NUMBER() OVER(ORDER BY (SELECT NULL)) AS Sequence
,       [name]
,       'UPDATE STATISTICS '+QUOTENAME([name]) AS sql_code
FROM    sys.tables
;
```

En segundo lugar, inicializar el bucle de Hola de hello variables tooperform necesarios:

```
DECLARE @nbr_statements INT = (SELECT COUNT(*) FROM #tbl)
,       @i INT = 1
;
```

Ahora, recorra las instrucciones ejecutándolas de una en una:

```
WHILE   @i <= @nbr_statements
BEGIN
    DECLARE @sql_code NVARCHAR(4000) = (SELECT sql_code FROM #tbl WHERE Sequence = @i);
    EXEC    sp_executesql @sql_code;
    SET     @i +=1;
END
```

Finalmente, descargará la tabla temporal de hello creada en el primer paso de Hola

```
DROP TABLE #tbl;
```


<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->

## <a name="next-steps"></a>Pasos siguientes
Para más sugerencias sobre desarrollo, consulte la [información general sobre desarrollo][development overview].

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[mientras]: https://msdn.microsoft.com/library/ms178642.aspx


<!--Other Web references-->
