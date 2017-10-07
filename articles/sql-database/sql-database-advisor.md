---
title: recomendaciones de aaaPerformance - base de datos de SQL de Azure | Documentos de Microsoft
description: Hola base de datos de SQL Azure proporciona recomendaciones para las bases de datos de SQL que puede mejorar el rendimiento de la consulta actual.
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: monicar
ms.assetid: 1db441ff-58f5-45da-8d38-b54dc2aa6145
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/05/2017
ms.author: sstein
ms.openlocfilehash: 77db338a0a395aec78c9e02849ae5ba4f2d01680
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="performance-recommendations"></a>Recomendaciones de rendimiento

La base de datos de SQL Azure aprende y se adapta a su aplicación y proporciona recomendaciones personalizadas habilitar rendimiento de hello toomaximize de las bases de datos SQL. Se evalúa continuamente el rendimiento mediante el análisis de su historial de uso de SQL Database. recomendaciones de Hola que se proporcionan se basan en un patrón de carga de trabajo único de la base de datos y ayudar a mejorar su rendimiento.

> [!NOTE]
> La manera recomendada de usar las recomendaciones es habilitando "Ajuste automático" en la base de datos. Para ver detalles, consulte [Ajuste automático](sql-database-automatic-tuning.md).
>

## <a name="create-index-recommendations"></a>Recomendaciones Crear índice
La base de datos de SQL Azure continuamente supervisa las consultas de Hola que se está ejecutadas e identifica los índices de Hola que pudieron mejorar el rendimiento de Hola. Una vez que se crea suficiente confianza de que falta un determinado índice, se crea una recomendación **Crear índice**. Confianza de compilaciones de base de datos de SQL Azure calculando el índice de Hola de ganancia de rendimiento aportaría a través del tiempo. Función hello estimado mejora del rendimiento, las recomendaciones se clasifican como alta, Media o baja. 

Los índices creados mediante recomendaciones se marcan siempre como índices auto_created. Puede ver qué índices son auto_created en la vista sys.indexes. Los índices creados de forma automática no bloquean los comandos ALTER/RENAME. Si trata de columna de hello toodrop cuya automático índice creada sobre él, Hola comando pasa y se quita automáticamente Hola índice creado con el comando de hello así. Índices normales bloquearían Hola ALTER/comando Cambiar nombre en las columnas que se indizan.

Una vez que cree Hola se aplica la recomendación de índice, base de datos de SQL Azure comparará el rendimiento de las consultas de hello con rendimiento de línea de base de Hola. Si el nuevo índice, vuelva a mejoras en el rendimiento de hello, recomendación se marcará como correcta e impacto en el informe estará disponible. En caso de que el índice de hello no ofrecen beneficios de hello, se revertirán automáticamente. Esta base de datos de SQL Azure de manera se asegura de que mediante recomendaciones solo mejorará el rendimiento de la base de datos de Hola.

Cualquier **crear índice** recomendación tiene una directiva que no permita que aplicando la recomendación de hello si el uso DTU de base de datos o grupo de hello es superior al 80% en los últimos 20 minutos o si el almacenamiento de hello es superior al 90% de uso de retroceso. En este caso, se puede posponer la recomendación de Hola.

## <a name="drop-index-recommendations"></a>Recomendaciones Quitar índice
Además toodetecting un índice que falta, Azure SQL Database continuamente analiza el rendimiento de Hola de los índices existentes. Si no se usa un índice, Azure SQL Database recomendará quitarlo. Se recomienda quitar un índice en dos casos:
* El índice es un duplicado de otro (misma columna indexada e incluida, esquema de partición y filtros)
* El índice lleva sin usarse un período prolongado (93 días)

Recomendaciones de quitar índice también ir a través de la comprobación de hello después de la implementación. Si se ha mejorado el rendimiento de hello informe del impacto de hello estará disponible. Si se detecta una degradación del rendimiento, se revertirá la recomendación.


## <a name="parameterize-queries-recommendations"></a>Recomendaciones para parametrizar consultas
**Parametrizar consultas** recomendaciones aparecen cuando tiene uno o más consultas que constantemente se están volviendo a compilar, pero terminan con Hola mismo plan de ejecución de consulta. Esta condición se abre un tooapply oportunidad fuerza la parametrización, lo que le permitirá planes de consulta toobe almacena en caché y volver a usar en hello futura mejora el rendimiento y reducir el uso de recursos. 

Cada consulta que se emite inicialmente en SQL Server debe toogenerate toobe compila un plan de ejecución. Cada plan generado se agrega memoria caché del plan toohello y las ejecuciones posteriores de hello misma consulta puede volver a usar este plan desde la memoria caché de hello, lo que elimina la necesidad de Hola de compilación adicional. 

Las aplicaciones que envían las consultas, que incluyen valores sin parámetros, pueden provocar sobrecarga de rendimiento de tooa, donde para cada consulta con distintos valores de parámetro plan de ejecución de Hola se compila de nuevo. En muchos Hola casos mismas consultas con parámetros diferentes valores generan Hola mismo planes de ejecución, pero estos planes todavía por separado se agregan toohello memoria caché del plan. Recompilación de planes de ejecución utilizan recursos de base de datos, aumentar Hola Duración tiempo y un desbordamiento de hello plan de consulta que produce la memoria caché planes toobe expulsa de la memoria caché de Hola. Este comportamiento de SQL Server se puede modificar estableciendo Hola forzada la opción parameterization de la base de datos de Hola. 

toohelp estimar el impacto de Hola de esta recomendación, son proporcionados por una comparación entre la CPU real de hello hello y uso proyectan el uso de CPU (como si se aplicó la recomendación de hello). Además tooCPU ahorro, reduce la duración de la consulta para hello tiempo de compilación. También habrá mucha menos sobrecarga en memoria caché del plan, lo que permite la mayoría de hello toostay en caché los planes y volverá a utilizar. Puede aplicar esta recomendación rápida y fácilmente haciendo clic en hello **aplicar** comando. 

Una vez que se aplica esta recomendación, se habilitará la parametrización forzada en minutos en la base de datos y comienza Hola supervisión de proceso que dura aproximadamente 24 horas. Después de este período, tendrá que ser capaz de toosee Hola validación informe que muestra el uso de CPU de la base de datos 24 horas antes y después de aplicar la recomendación de Hola. Asistente de base de datos de SQL tiene un mecanismo de seguridad que se revierte automáticamente la recomendación de hello aplicado en caso de que se ha detectado una regresión del rendimiento.

## <a name="fix-schema-issues-recommendations"></a>Recomendaciones para solucionar problemas del esquema
**Solucionar problemas del esquema** recomendaciones aparecen cuando hello una anomalía en número de hello relacionadas con el esquema de errores de SQL en la base de datos de SQL Azure está pasando lo los avisos de servicio de base de datos SQL. Esta recomendación suele aparecer cuando la base de datos encuentra varios errores relacionados con el esquema (nombre de columna no válido, nombre de objeto no válido, etc.) en el curso de una hora.

"Problemas del esquema" son una clase de errores de sintaxis de SQL Server que se producen cuando la definición de Hola de consulta SQL de Hola y Hola de esquema de base de datos de hello no estén alineados. Por ejemplo, una de las columnas de hello esperadas por la consulta de hello pueden faltar en la tabla de destino de hello, o viceversa. 

Recomendación "Corregir el problema de esquema" aparece cuando el servicio de base de datos de SQL Azure observa una anomalía en número de hello relacionadas con el esquema de errores de SQL ocurre en la base de datos de SQL Azure. Hola siguientes errores de Hola de muestra de tabla que están relacionados tooschema problemas:

| Código de error SQL | Message |
| --- | --- |
| 201 |El procedimiento o la función '*' espera parámetros '*', que no se han proporcionado. |
| 207 |Nombre de columna '*' no válido. |
| 208 |Nombre de objeto '*' no válido. |
| 213 |El nombre de columna o los valores especificados no corresponden a la definición de la tabla. |
| 2812 |No se pudo encontrar el procedimiento almacenado '*'. |
| 8144 |La función o el procedimiento * tiene demasiados argumentos. |

## <a name="next-steps"></a>Pasos siguientes
Supervisar sus recomendaciones y continuar tooapply les toorefine rendimiento. Las cargas de trabajo de bases de datos son dinámicas y cambian con frecuencia. Asistente de base de datos SQL continúa toomonitor y proporcionar recomendaciones que pueden mejorar el rendimiento de la base de datos. 

* Vea [recomendaciones de rendimiento en el portal de Azure hello](sql-database-advisor-portal.md) para conocer los pasos sobre cómo las recomendaciones de rendimiento de toouse de Hola portal de Azure.
* Vea [información de rendimiento de consultas](sql-database-query-performance.md) toolearn sobre y vista de impacto en el rendimiento de las consultas principales de Hola.

## <a name="additional-resources"></a>Recursos adicionales
* [Almacén de consultas](https://msdn.microsoft.com/library/dn817826.aspx)
* [CREATE INDEX](https://msdn.microsoft.com/library/ms188783.aspx)
* [Control de acceso basado en rol](../active-directory/role-based-access-control-what-is.md)

