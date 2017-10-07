---
title: "variables de aaaAssign en el almacén de datos de SQL | Documentos de Microsoft"
description: "Sugerencias para la asignación de variables de Transact-SQL en el Almacenamiento de datos SQL Azure para desarrollar soluciones."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: 81ddc7cf-a6ba-4585-91a3-b6ea50f49227
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 9de48739bb0af80ff2a117704b31512c680f78d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="assign-variables-in-sql-data-warehouse"></a>Asignación de variables en el Almacenamiento de datos SQL
Las variables en el almacén de datos de SQL se establecen mediante hello `DECLARE` instrucción o hello `SET` instrucción.

Todos Hola siguientes son formas perfectamente válidos tooset un valor de variable:

## <a name="setting-variables-with-declare"></a>Configuración de variables con DECLARE
Inicializar variables con DECLARE es uno de hello más flexible formas tooset un valor de la variable en el almacén de datos de SQL.

```sql
DECLARE @v  int = 0
;
```

También puede utilizar DECLARE tooset más de una variable a la vez. No se puede utilizar `SELECT` o `UPDATE` toodo esto:

```sql
DECLARE @v  INT = (SELECT TOP 1 c_customer_sk FROM Customer where c_last_name = 'Smith')
,       @v1 INT = (SELECT TOP 1 c_customer_sk FROM Customer where c_last_name = 'Jones')
;
```

No se puede inicializar y utilizar una variable en hello misma instrucción DECLARE. ejemplo de Hola de tooillustrate Hola punto es **no** permitido como @p1 tanto inicializado y usar en hello misma instrucción DECLARE. Esto generará un error.

```sql
DECLARE @p1 int = 0
,       @p2 int = (SELECT COUNT (*) FROM sys.types where is_user_defined = @p1 )
;
```

## <a name="setting-values-with-set"></a>Configuración de valores con SET
SET es un método muy común para configurar una sola variable.

Todos ejemplos de hello siguientes son formas válidas de establecer una variable con el conjunto:

```sql
SET     @v = (Select max(database_id) from sys.databases);
SET     @v = 1;
SET     @v = @v+1;
SET     @v +=1;
```

Solo puede establecer una variable al mismo tiempo con SET. Sin embargo, como hemos visto anteriormente, se admiten los operadores compuestos.

## <a name="limitations"></a>Limitaciones
Puede usar SELECT o UPDATE para la asignación de variables.

## <a name="next-steps"></a>Pasos siguientes
Para más sugerencias sobre desarrollo, consulte la [información general sobre desarrollo][development overview].

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->

<!--Other Web references-->
