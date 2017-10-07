---
title: "aaaMigrate el almacenamiento de datos de solución tooSQL | Documentos de Microsoft"
description: "Guía de migración para poner la plataforma de almacenamiento de datos SQL de solución tooAzure."
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: 198365eb-7451-4222-b99c-d1d9ef687f1b
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 06/27/2017
ms.author: joeyong;barbkess
ms.openlocfilehash: 27b51f15247603f054070f360ede7f24541c0288
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-solution-tooazure-sql-data-warehouse"></a>Migrar el almacenamiento de datos SQL de solución tooAzure
Vea las implicaciones de migrar un tooAzure de solución de base de datos almacén de datos SQL existente. 

## <a name="profile-your-workload"></a>Generación del perfil de la carga de trabajo
Antes de migrar, desea toobe seguro de que almacenamiento de datos SQL es la solución correcta de hello para la carga de trabajo. Almacén de datos de SQL es un sistema distribuido diseñado tooperform analizar los datos de gran tamaño.  Almacenamiento de datos de migración tooSQL requiere algunos cambios de diseño que no son demasiado difíciles de toounderstand pero pueden tardar algún tiempo tooimplement. Si su empresa requiere un almacenamiento de datos de clase empresarial, Hola ventajas son la pena Hola. Sin embargo, si no necesita la potencia de Hola de almacenamiento de datos SQL, resulta más rentable toouse SQL Server o base de datos de SQL Azure.

Considere usar SQL Data Warehouse cuando:
- Tenga uno o varios terabytes de datos
- Análisis de plan toorun en grandes cantidades de datos
- Necesita almacenamiento y proceso de hello capacidad tooscale 
- Desea que los costos de toosave colocando los recursos informáticos cuando no se necesitan.

No use SQL Data Warehouse para las cargas de trabajo operativas (OLTP) que tengan:
- Una elevada frecuencia de lecturas y escrituras
- Gran número de selecciones de singleton
- Grandes volúmenes de inserción de filas únicas
- Necesidades de procesamiento fila por fila
- Formatos incompatibles (JSON, XML)


## <a name="plan-hello-migration"></a>Migración del plan de Hola

Una vez que haya decidido toomigrate un tooSQL de solución almacenamiento de datos existente, es importante tooplan migración de hello antes de comenzar. 

Uno de los objetivos de la planificación es tooensure los datos, los esquemas de tabla, y el código son compatibles con el almacenamiento de datos de SQL. Hay algunas diferencias de compatibilidad toowork alrededor de entre el sistema actual y el almacenamiento de datos SQL. Además, la migración de grandes cantidades de datos tooAzure lleva tiempo. Un planeamiento cuidadoso acelera obtener su tooAzure de datos. 

Otro objetivo de diseño es el diseño de toomake tooensure ajustes que la solución aprovecha las ventajas de rendimiento de las consultas alta Hola que almacenamiento de datos de SQL está diseñado tooprovide. Diseñar los almacenes de datos para la escala presenta los patrones de diseño diferentes y enfoques tradicionales por lo que no siempre están Hola mejor. Aunque puede realizar algunos ajustes de diseño después de la migración, realizar cambios antes de proceso de hello guardará más tarde.

tooperform una migración correcta, debe toomigrate los esquemas de tabla, el código y los datos. Para instrucciones sobre estos temas de migración, consulte:

-  [Migración de los esquemas](sql-data-warehouse-migrate-schema.md)
-  [Migración del código](sql-data-warehouse-migrate-code.md)
-  [Migración de los datos](sql-data-warehouse-migrate-data.md) 

<!--
## Perform hello migration


## Deploy hello solution


## Validate hello migration

-->

## <a name="next-steps"></a>Pasos siguientes
Hola CAT (equipo de asesoramiento al cliente) también tiene alguna orientación excelente de almacenamiento de datos SQL, que publique a través de blogs.  Eche un vistazo a su artículo [migrar datos tooAzure almacenamiento de datos SQL en la práctica] [ Migrating data tooAzure SQL Data Warehouse in practice] para obtener instrucciones adicionales sobre la migración.

<!--Image references-->

<!--Article references-->

<!--MSDN references-->

<!--Other Web references-->
[Migrating data tooAzure SQL Data Warehouse in practice]: https://blogs.msdn.microsoft.com/sqlcat/2016/08/18/migrating-data-to-azure-sql-data-warehouse-in-practice/
