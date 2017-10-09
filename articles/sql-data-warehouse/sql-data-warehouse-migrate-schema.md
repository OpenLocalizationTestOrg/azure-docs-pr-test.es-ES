---
title: aaaMigrate el almacenamiento de datos de esquema tooSQL | Documentos de Microsoft
description: Sugerencias para migrar el almacenamiento de datos SQL de esquema tooAzure para desarrollar soluciones.
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: 538b60c9-a07f-49bf-9ea3-1082ed6699fb
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 10/31/2016
ms.author: joeyong;barbkess
ms.openlocfilehash: 1309b743b78564575695038a4856d9d25a2b18d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-schemas-toosql-data-warehouse"></a>Migrar el almacenamiento de datos de esquemas tooSQL
Orientación para migrar su tooSQL de esquemas almacenamiento de datos SQL. 

## <a name="plan-your-schema-migration"></a>Planeamiento de la migración del esquema

Cuando planee una migración, vea hello [información general de la tabla] [ table overview] toobecome familiarizado con las consideraciones de diseño de tabla, como las estadísticas de distribución, particiones e índices.  También se incluyen algunas [características no admitidas de las tablas][unsupported table features] y las soluciones alternativas a tales carencias.

## <a name="use-user-defined-schemas-tooconsolidate-databases"></a>Usar bases de datos de esquemas definidos por el usuario tooconsolidate

Probablemente, su carga de trabajo existente tiene más de una base de datos. Por ejemplo, un almacenamiento de datos de SQL Server podría incluir una base de datos provisional, una de almacenamiento de datos y algunas de tipo data mart. En esta topología, cada base de datos se ejecuta como una carga de trabajo independiente con directivas de seguridad distintas.

Por el contrario, el almacenamiento de datos SQL se ejecuta como carga de trabajo del almacenamiento de datos todo de hello dentro de una base de datos. No se permiten las combinaciones entre bases de datos. Por lo tanto, almacenamiento de datos de SQL espera que todas las tablas utilizadas por toobe de almacenamiento de datos de hello almacenado en una base de datos de Hola.

Se recomienda utilizar esquemas definidos por el usuario tooconsolidate la carga de trabajo existente en una base de datos. Para ver ejemplos, consulte [Esquemas definidos por el usuario](sql-data-warehouse-develop-user-defined-schemas.md).

## <a name="use-compatible-data-types"></a>Uso de tipos de datos compatibles
Modifique la toobe de tipos de datos compatible con el almacenamiento de datos de SQL. Para ver una lista de tipos de datos admitidos y no admitidos, consulte el artículo sobre [tipos de datos][data types]. Ese tema proporciona soluciones alternativas para los tipos de hello no admitido. También proporciona una consulta tooidentify tipos existentes que no se admiten en el almacén de datos de SQL.

## <a name="minimize-row-size"></a>Minimización del tamaño de fila
Para obtener el mejor rendimiento, minimizar Hola fila con longitud de las tablas. Puesto que longitudes de fila más cortos conducen toobetter rendimiento, usar los datos más pequeños Hola que funcionan para los datos. 

Para el ancho de fila de tabla, PolyBase tiene un límite de 1 MB.  Si tiene previsto datos tooload en almacenamiento de datos de SQL con PolyBase, actualice los anchos de máximo de filas de tablas toohave de menos de 1 MB. 

<!--
- For example, this table uses variable length data but hello largest possible size of hello row is still less than 1 MB. PolyBase will load data into this table.

- This table uses variable length data and hello defined row width is less than one MB. When loading rows, PolyBase allocates hello full length of hello variable-length data. hello full length of this row is greater than one MB.  PolyBase will not load data into this table.  

-->

## <a name="specify-hello-distribution-option"></a>Especifique la opción de distribución de Hola
SQL Data Warehouse es un sistema de base de datos distribuida. Cada tabla se distribuyen o se replican a través de nodos de proceso de Hola. Hay una opción de tabla que le permite especificar cómo toodistribute Hola datos. Opciones de Hello tienen round-robin, replicación, o está distribuido hash. Cada una tiene ventajas y desventajas. Si no especifica la opción de distribución de hello, almacenamiento de datos de SQL utilizará round robin como valor predeterminado de Hola.

- Round-robin es predeterminado de Hola. Se toouse más sencilla de Hola y carga los datos de hello lo más rápidos posible, pero las combinaciones requerirá el movimiento de datos que reduce el rendimiento de las consultas.
- Replicada almacena una copia de la tabla de hello en cada nodo de ejecución. Las tablas replicadas tienen buen rendimiento porque no requieren que se muevan datos para las combinaciones y agregaciones. Sí requieren almacenamiento adicional y, por lo tanto, funcionan mejor con tablas más pequeñas.
- Hash distribuida distribuye filas de Hola a todos los nodos de Hola a través de una función hash. Las tablas hash distribuida son la esencia de Hola de almacenamiento de datos SQL ya que son tooprovide diseñada consulta alto rendimiento en tablas grandes. Esta opción requiere algunos planificación tooselect Hola mejor columna acerca de qué datos de hello toodistribute. Sin embargo, si no elige Hola Hola de columna mejor primera vez, se pueden volver a distribuir fácilmente datos de hello en una columna diferente. 

opción toochoose Hola de distribución recomendado para cada tabla, vea [distribuidas tablas](sql-data-warehouse-tables-distribute.md).


## <a name="next-steps"></a>Pasos siguientes
Una vez que haya migrado correctamente su tooSQL de esquema de base de datos almacén de datos, continúe tooone de hello siguientes artículos:

* [Migración de los datos][Migrate your data]
* [Migración del código][Migrate your code]

Para obtener más información sobre los procedimientos recomendados de almacenamiento de datos SQL, vea hello [prácticas recomendadas] [ best practices] artículo.

<!--Image references-->

<!--Article references-->
[Migrate your code]: ./sql-data-warehouse-migrate-code.md
[Migrate your data]: ./sql-data-warehouse-migrate-data.md
[best practices]: ./sql-data-warehouse-best-practices.md
[table overview]: ./sql-data-warehouse-tables-overview.md
[unsupported table features]: ./sql-data-warehouse-tables-overview.md#unsupported-table-features
[data types]: ./sql-data-warehouse-tables-data-types.md
[unsupported data types]: ./sql-data-warehouse-tables-data-types.md#unsupported-data-types

<!--MSDN references-->


<!--Other Web references-->
