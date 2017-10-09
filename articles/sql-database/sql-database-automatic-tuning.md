---
title: "base de datos - aaaSQL para la optimización automática | Documentos de Microsoft"
description: "Base de datos SQL analiza la consulta SQL y automáticamente adapta a cargas de trabajo de toouser."
services: sql-database
documentationcenter: 
author: jovanpop-msft
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/05/2017
ms.author: jovanpop
ms.openlocfilehash: 897a8deaabedb6727dc49958c64d0433c5f2e4f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="automatic-tuning"></a>Ajuste automático

La base de datos de SQL Azure es un servicio de datos completamente administrado que supervisa las consultas de Hola que se ejecutan en la base de datos de Hola y automáticamente se pueden mejorar el rendimiento de carga de trabajo de Hola. La base de datos de SQL Azure tiene un mecanismo de inteligencia incorporada que puede optimizar y mejorar el rendimiento de las consultas adaptando dinámicamente la carga de trabajo de tooyour de base de datos de hello automáticamente. El ajuste automático de la base de datos de SQL Azure puede ser una de las características más importantes de Hola que se pueden habilitar en el rendimiento de base de datos de SQL Azure toooptimize de las consultas.

Consulte este artículo para conocer los pasos Hola demasiado[habilitar el ajuste automático](sql-database-automatic-tuning-enable.md) utilizando Hola portal de Azure.

## <a name="why-automatic-tuning"></a>¿Por qué el ajuste automático?

Una de las principales tareas de hello en administración clásico de la base de datos está supervisando la carga de trabajo de hello, identificar críticas SQL realiza una consulta, los índices que se deben agregar tooimprove rendimiento y usan índices con poca frecuencia. La base de datos de SQL Azure proporciona una visión detallada de las consultas de Hola y de índices que necesita toomonitor. Sin embargo, supervisar constantemente una base de datos es una tarea ardua y tediosa, sobre todo cuando se trabaja con muchas bases de datos. Administrar un gran número de bases de datos podría ser eficazmente toodo imposible incluso con todas las herramientas disponibles e informes que ofrecen de base de datos de SQL Azure y portal de Azure. En lugar de supervisión y optimización de la base de datos manualmente, considere la posibilidad de delegar algunas de Hola de supervisión y optimización tooAzure de acciones base de datos SQL mediante la característica de optimización automática. 


> [!VIDEO https://channel9.msdn.com/Blogs/Azure-in-the-Enterprise/Enabling-Azure-SQL-Database-Auto-Tuning-at-Scale-for-Microsoft-IT/player]
>

## <a name="how-does-automatic-tuning-work"></a>¿Cómo funciona el ajuste automático?

La base de datos de SQL Azure tiene un proceso de supervisión y análisis de rendimiento continua que constantemente aprende Hola característico de la carga de trabajo e identifica posibles problemas y mejoras.

![Proceso de ajuste automático](./media/sql-database-automatic-tuning/tuning-process.png)

Esto permite que proceso toodynamically de base de datos de SQL Azure adaptar tooyour carga de trabajo mediante la búsqueda de los índices y los planes pueden mejorar el rendimiento de las cargas de trabajo y los índices afecta a las cargas de trabajo. En función de lo que encuentre, el ajuste automático pone en práctica acciones de optimización que mejoran el rendimiento de la carga de trabajo. Además, base de datos de SQL Azure supervisa continuamente el rendimiento después de cualquier cambio realizado por tooensure de optimización automática que mejora el rendimiento de la carga de trabajo. Cualquier acción que no mejore el rendimiento se revierte automáticamente. Este proceso de comprobación es una característica clave que garantiza que cualquier cambio realizado por el ajuste automático no reducir el rendimiento de saludo de la carga de trabajo.

Hay dos aspectos del ajuste automático disponibles en Azure SQL Database:

 -  **Administración automática de índices** que identifica tanto los índices que se deberían agregar a la base de datos como los que se deberían quitar.
 -  **Corrección automática de planes** (próximamente, ya disponible en SQL Server 2017) que identifica planes problemáticos y corrige los problemas de rendimiento de los planes de SQL.

## <a name="automatic-index-management"></a>Administración automática de índices

En Azure SQL Database, la administración de índices resulta sencilla porque Azure SQL Database obtiene información acerca de la carga de trabajo y se asegura de que los datos estén siempre indexados de forma óptima. El diseño adecuado de índices es fundamental para un rendimiento óptimo de la carga de trabajo y la administración automática de índices puede ayudar a optimizar los índices. Administración automática del índice puede corregir problemas de rendimiento en las bases de datos indizadas incorrectamente, o se mantienen y mejore los índices en el esquema de base de datos existente de Hola. 

### <a name="why-do-you-need-index-management"></a>¿Por qué se necesita la administración de índices?

Acelerar algunas de las consultas que leen datos de tablas de hello; Sin embargo, podrían ralentizar las consultas de Hola que actualizan los datos. Necesita toocarefully analizar cuando toocreate un índice y qué columnas necesita tooinclude en Hola índice. Es posible que algunos índices no sean necesarios pasado un tiempo. Por lo tanto, deberá tooperiodically identificar y quitar índices de Hola que no proporcionan ningún beneficio. Si omite Hola índices no usados, rendimiento de las consultas de Hola que actualizan los datos podría reducirse sin ninguna ventaja en las consultas de Hola que leer los datos. Índices no usados también afecta a rendimiento general del sistema de hello porque actualizaciones adicionales necesitan un registro innecesario.

Buscar conjunto óptimo de Hola de índices que mejoren el rendimiento de las consultas de Hola que leer los datos de las tablas y tiene un impacto mínimo en las actualizaciones puede requerir análisis complejo y continuado.

La base de datos de SQL Azure usa inteligencia integrada y reglas avanzadas que analizar las consultas, identificar los índices que sean óptimos para las cargas de trabajo actuales y se podrían quitar índices Hola. La base de datos de SQL Azure se asegura de que tiene un conjunto mínimo necesario de índices que optimizar las consultas de Hola que leen los datos, con un impacto Hola minimizado en Hola otras consultas.

### <a name="how-tooidentify-indexes-that-need-toobe-changed-in-your-database"></a>¿Cómo tooidentify indiza ese toobe necesidad cambiado en la base de datos?

Azure SQL Database facilita el proceso de administración de índices. En lugar de proceso tedioso de Hola de análisis de carga de trabajo manual y la supervisión de índice, base de datos de SQL Azure analiza la carga de trabajo, identifica las consultas de Hola que pudieron ejecutarse más rápidamente con un nuevo índice e identifica los índices no usados o duplicados. Para más información sobre la identificación de los índices que deben cambiarse, consulte cómo [buscar recomendaciones de índices en Azure Portal](sql-database-advisor-portal.md).

### <a name="automatic-index-management-considerations"></a>Consideraciones sobre la administración automática de índices

Si encuentra que las reglas integradas de hello mejoran el rendimiento de hello de la base de datos, puede dejar que base de datos SQL de Azure administre automáticamente los índices.

Se requieren acciones toocreate índices necesarios en bases de datos de SQL Azure podrían consumir recursos y temporalmente afectan al rendimiento de la carga de trabajo. impacto de hello toominimize de creación de índices en el rendimiento de la carga de trabajo, base de datos de SQL Azure busca el período de tiempo adecuado de Hola para cualquier operación de administración de índice. Acción para la optimización se pospone si la base de datos de hello necesita recursos tooexecute la carga de trabajo e iniciarse cuando base de datos de hello tiene suficientes recursos no utilizados que se pueden usar para tareas de mantenimiento de Hola. Una característica importante de la administración de índices automática es una comprobación de acciones de Hola. Cuando la base de datos de SQL Azure crea o quita el índice, un proceso de supervisión analiza el rendimiento de su tooverify de carga de trabajo que acción Hola mejora el rendimiento de Hola. Si lo no aportar mejora considerable, inmediatamente se revierte la acción de Hola. De esta manera, Azure SQL Database garantiza que las acciones automáticas no surtan un efecto negativo sobre el rendimiento de la carga de trabajo. Índices creados por el ajuste automático son transparentes para la operación de mantenimiento de hello en el esquema subyacente Hola. Cambios de esquema, como quitar o cambiar el nombre de las columnas no estén bloqueados por la presencia de Hola de índices creados de forma automática. Los índices que Azure SQL Database crea automáticamente se quitan de inmediato cuando se quitan la tabla o las columnas relacionadas.

## <a name="automatic-plan-choice-correction"></a>Corrección automática de la selección de plan

La corrección automática de planes es una nueva característica de ajuste automático que se agregó en SQL Server de 2017 CTP2.0 y que identifica los planes de SQL que no funcionan correctamente. Esta opción de ajuste automático estará disponible en breve en Azure SQL Database. Puede ver más información en el artículo sobre el [ajuste automático en SQL Server 2017](https://docs.microsoft.com/sql/relational-databases/automatic-tuning/automatic-tuning).

## <a name="next-steps"></a>Pasos siguientes

- característica de optimización totalmente administrar la carga de trabajo, consulte tooenable automática para la optimización de base de datos de SQL Azure y permita que automática [habilitar el ajuste automático](sql-database-automatic-tuning-enable.md).
- toouse manual para la optimización, puede revisar [recomendaciones en portal de Azure de optimización](sql-database-advisor-portal.md) y aplicar manualmente hello las que mejoran el rendimiento de las consultas.
