---
title: Glosario de herramientas de base de datos aaaElastic | Documentos de Microsoft
description: "Explicación de los términos usados en las herramientas de bases de datos elásticas"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: a23a4e81-6706-452d-afc1-a550e5e47af9
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: d6573aad9a097e07135b0a64d1dafec19bb8cc7c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="elastic-database-tools-glossary"></a>Glosario de las herramientas de bases de datos elásticas
Hello siguientes se definen los términos de hello [herramientas de base de datos elástica](sql-database-elastic-scale-introduction.md), una característica de base de datos de SQL Azure. Hello herramientas son utilizado toomanage [partición se asigna](sql-database-elastic-scale-shard-map-management.md)e incluyen hello [biblioteca de cliente](sql-database-elastic-database-client-library.md), hello [herramienta Dividir-combinar](sql-database-elastic-scale-overview-split-and-merge.md), [grupos elásticos](sql-database-elastic-pool.md), y [consultas](sql-database-elastic-query-overview.md). 

Estos términos se usan en [agregar una partición con herramientas de base de datos elástica](sql-database-elastic-scale-add-a-shard.md) y [con los problemas de asignación de particiones de la clase toofix de hello RecoveryManager](sql-database-elastic-database-recovery-manager.md).

![Términos de Escalado elástico][1]

**Base de datos**: una base de datos SQL de Azure. 

**Enrutamiento dependiente de datos**: Hola funcionalidad que permite una partición de aplicación tooconnect tooa tiene una clave de particionamiento específica. Consulte [Enrutamiento dependiente de los datos](sql-database-elastic-scale-data-dependent-routing.md). Comparar demasiado**[particiones múltiples consultas](sql-database-elastic-scale-multishard-querying.md)**.

**Mapa de particiones global**: Hola asignación entre las claves de particionamiento y sus respectivos particiones dentro de un **conjunto de particiones**. mapa de particiones global de Hola se almacena en hello **manager de mapa de particiones**. Comparar demasiado**mapa de particiones local**.

**Mapa de particiones de lista**: un mapa de particiones en el que las claves de particionamiento se asignan de manera individual. Comparar demasiado**mapa de particiones de intervalo**.   

**Mapa de particiones local**: almacenados en una partición, mapa de particiones locales de hello contiene asignaciones para hello shardlets que residen en la partición de Hola.

**Consulta de varias particiones**: Hola capacidad tooissue una consulta en varias particiones; se devuelven conjuntos de resultados con UNION ALL semántica (también conocido como "consulta de distribución ramificada"). Comparar demasiado**enrutamiento dependiente de datos**.

**Multiinquilino** e **Inquilino único**: muestra una base de datos de inquilino único y multiinquilino:

![Bases de datos de inquilino único y multiinquilino](./media/sql-database-elastic-scale-glossary/multi-single-simple.png)

Aquí se muestra una representación de bases de datos de inquilino único y multiinquino **particionadas** . 

![Bases de datos de inquilino único y multiinquilino](./media/sql-database-elastic-scale-glossary/shards-single-multi.png)

**Mapa de particiones de intervalo**: un mapa de particiones en qué Hola estrategia de distribución de la partición se basa en varios intervalos de valores no contiguos. 

**Tablas de referencia**: tablas no particionadas, pero que se replican entre particiones. Por ejemplo, los códigos postales se pueden almacenar en una tabla de referencia. 

**Partición**: una base de datos SQL de Azure que almacena datos desde un conjunto de datos particionados. 

**Elasticidad de partición**: Hola tooperform de la capacidad **escalado horizontal** y **escalado vertical**.

**Tablas particionadas**: tablas que se particionan, es decir, cuyos datos se distribuyen entre particiones según sus valores de clave de particionamiento. 

**Clave de particionamiento**: un valor de columna que determina cómo se distribuyen los datos entre particiones. Hello tipo de valor puede ser uno de hello siguientes: **int**, **bigint**, **varbinary**, o **uniqueidentifier**. 

**Conjunto de particiones**: Hola colección de particiones que son atributos toohello mismo mapa de particiones en el Administrador de mapa de particiones de Hola.  

**Shardlet**: todos los datos de hello asociados con un único valor de una clave de particionamiento en una partición. Un shardlet es la unidad más pequeña de Hola de movimiento de datos posibles cuando redistribuir tablas particionadas. 

**Mapa de particiones**: Hola conjunto de asignaciones entre las claves de particionamiento y sus respectivos particiones.

**Administrador de mapa de particiones**: un almacén de datos y objetos de administración que contenga Hola particiones map(s), ubicaciones de particiones y asignaciones para uno o varios conjuntos de particiones.

![Asignaciones][2]

## <a name="verbs"></a>Verbos
**Escalado horizontal**: acto de Hola de ajuste de escala (o) una colección de particiones agregando o quitando el mapa de particiones de tooa de particiones, tal y como se muestra a continuación.

![Escalado horizontal y vertical][3]

**Mezcla**: acto de Hola de mover shardlets de partición de tooone dos particiones y actualizar el mapa de particiones de hello en consecuencia.

**Movimiento de Shardlets**: acto de Hola de mover una partición diferente de tooa único shardlet. 

**Partición**: acto de Hola de partición horizontal de forma idéntica datos estructurados a través de varias bases de datos basadas en una clave de particionamiento.

**División**: acto de Hola de mover varios shardlets de partición de una partición tooanother (normalmente nuevo). Una clave de particionamiento proporcionada por usuario de hello como punto de división de Hola.

**Ajuste de escala vertical**: acto de Hola de ajuste de escala hacia arriba (o hacia abajo) Hola a nivel de rendimiento de una partición individual. Por ejemplo, cambiar una partición de tooPremium estándar (que da lugar a más recursos informáticos). 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-glossary/glossary.png
[2]: ./media/sql-database-elastic-scale-glossary/mappings.png
[3]: ./media/sql-database-elastic-scale-glossary/h_versus_vert.png

