---
title: aaaResources para desarrollar un almacenamiento de datos en Azure | Documentos de Microsoft
description: "Conceptos de desarrollo, decisiones de diseño, recomendaciones y técnicas de codificación para el Almacenamiento de datos SQL."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: barbkess
editor: 
ms.assetid: 996e3afc-c21c-4e21-b9df-997f953f6dfd
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: develop
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 67e3a6a3e2664919c3445ea5d5eba251054de020
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="design-decisions-and-coding-techniques-for-sql-data-warehouse"></a>Decisiones de diseño y técnicas de codificación para el Almacenamiento de datos SQL
Eche un vistazo a través de estos artículos de desarrollo toobetter comprender las decisiones de diseño clave, recomendaciones y técnicas de codificación para el almacenamiento de datos de SQL.

## <a name="key-design-decisions"></a>Decisiones de diseño clave
Hello artículos siguientes resaltan algunos de los conceptos básicos de Hola y decisiones de diseño que deberá toounderstand para el desarrollo de Hola de su almacén de datos distribuidos con almacenamiento de datos SQL:

* [conexiones][connections]
* [simultaneidad][concurrency]
* [transacciones][transactions]
* [esquemas definidos por el usuario][user-defined schemas]
* [distribución de tablas][table distribution]
* [índices de tabla][table indexes]
* [particiones de tabla][table partitions]
* [CTAS][CTAS]
* [estadísticas][statistics]

## <a name="development-recommendations-and-coding-techniques"></a>Recomendaciones de desarrollo y técnicas de codificación
En estos artículos se abordan técnicas de codificación, sugerencias y recomendaciones específicas para el desarrollo de su Almacenamiento de datos SQL:

* [procedimientos almacenados][stored procedures]
* [etiquetas][labels]
* [vistas][views]
* [tablas temporales][temporary tables]
* [SQL dinámico][dynamic SQL]
* [bucle][looping]
* [opciones de agrupar por][group by options]
* [asignación de variables][variable assignment]

## <a name="next-steps"></a>Pasos siguientes
Una vez que ha estado a través de los artículos de desarrollo de Hola, eche un vistazo a través de hello [referencia de Transact-SQL] [ Transact-SQL reference] página para obtener más información acerca de la sintaxis de hello compatible para almacenamiento de datos de SQL.

<!--Image references-->

<!--Article references-->
[concurrency]: ./sql-data-warehouse-develop-concurrency.md
[connections]: ./sql-data-warehouse-connect-overview.md
[CTAS]: ./sql-data-warehouse-develop-ctas.md
[dynamic SQL]: ./sql-data-warehouse-develop-dynamic-sql.md
[group by options]: ./sql-data-warehouse-develop-group-by-options.md
[labels]: ./sql-data-warehouse-develop-label.md
[looping]: ./sql-data-warehouse-develop-loops.md
[statistics]: ./sql-data-warehouse-tables-statistics.md
[stored procedures]: ./sql-data-warehouse-develop-stored-procedures.md
[table distribution]: ./sql-data-warehouse-tables-distribute.md
[table indexes]: ./sql-data-warehouse-tables-index.md
[table partitions]: ./sql-data-warehouse-tables-partition.md
[temporary tables]: ./sql-data-warehouse-tables-temporary.md
[transactions]: ./sql-data-warehouse-develop-transactions.md
[user-defined schemas]: ./sql-data-warehouse-develop-user-defined-schemas.md
[variable assignment]: ./sql-data-warehouse-develop-variable-assignment.md
[views]: ./sql-data-warehouse-develop-views.md
[Transact-SQL reference]: ./sql-data-warehouse-overview-reference.md

<!--MSDN references-->
[renaming objects]: https://msdn.microsoft.com/library/mt631611.aspx

<!--Other Web references-->
