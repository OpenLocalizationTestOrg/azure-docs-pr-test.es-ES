---
title: aaaMonitoring & ajuste del rendimiento - base de datos de SQL de Azure | Documentos de Microsoft
description: "Sugerencias para la optimización del rendimiento de Base de datos SQL de Azure a través de la evaluación y la mejora."
services: sql-database
documentationcenter: 
author: v-shysun
manager: felixwu
editor: 
keywords: "SQL optimización del rendimiento, base de datos optimización del rendimiento, sugerencias para la optimización del rendimiento de SQL, optimización del rendimiento de Base de datos SQL"
ms.assetid: eb7b3f66-3b33-4e1b-84fb-424a928a6672
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: v-shysun
ms.openlocfilehash: 9e196831902aa6ea841ef14caf5713e82ebfc62d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-and-performance-tuning"></a>Optimización de la supervisión y el rendimiento

Administra automáticamente la base de datos de SQL Azure y servicio de datos flexible que puede fácilmente supervisar el uso, agregar o quitar recursos (CPU, memoria, e/s), busque las recomendaciones que pueden mejorar el rendimiento de la base de datos, o dejar que base de datos a adaptar la carga de trabajo de tooyour y optimizar automáticamente el rendimiento.

En este artículo se proporciona información general de las opciones de optimización de la supervisión y el rendimiento disponibles en Azure SQL Database.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="monitoring-and-troubleshooting-database-performance"></a>Supervisión y solución de problemas de rendimiento de base de datos

Habilita la base de datos de SQL Azure es tooeasily supervisar el uso de la base de datos e identifique las consultas que podrían causar problemas de rendimiento de Hola. Puede supervisar el rendimiento de la base de datos mediante Azure Portal o vistas del sistema. Tener Hola siguientes opciones para la supervisión y solución de problemas de rendimiento de la base de datos:

1. Hola [portal de Azure](https://portal.azure.com), haga clic en **bases de datos SQL**, seleccione la base de datos de hello y, a continuación, usar Hola supervisión gráfico toolook para los recursos que se está aproximando a su máximo. El consumo de DTU se muestra de manera predeterminada. Haga clic en **editar** toochange Hola intervalo de tiempo y valores que se muestran.
2. Use [Query Performance Insight](sql-database-query-performance.md) consultas de hello tooidentify que gastan más Hola de recursos.
3. Puede usar vistas de administración dinámica (DMV), Extended Events (`XEvents`), y Hola almacén de consultas en parámetros de rendimiento de tooget SSMS en tiempo real.

Vea hello [tema de la Guía de rendimiento](sql-database-performance-guidance.md) técnicas de toofind que puede usar tooimprove rendimiento de base de datos de SQL Azure si encuentra algún problema al usar estos informes o vistas.

> [!IMPORTANT] 
> Se recomienda que siempre utilice Hola versión más reciente de Management Studio tooremain sincronizada con actualizaciones tooMicrosoft Azure y base de datos SQL. [Actualice SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).
>

## <a name="optimize-database-tooimprove-performance"></a>Optimizar el rendimiento de tooimprove de base de datos

La base de datos de SQL Azure permite tooidentify oportunidades tooimprove y optimizar el rendimiento de las consultas sin cambiar los recursos mediante la revisión [recomendaciones de optimización de rendimiento](sql-database-advisor.md). Entre los motivos comunes para un rendimiento deficiente de la base de datos se encuentran índices que faltan y consultas mal optimizadas. Puede aplicar estos ajustar recomendaciones tooimprove el rendimiento de la carga de trabajo.
También puede permitir que base de datos de SQL Azure demasiado[automáticamente optimizar el rendimiento de las consultas](sql-database-automatic-tuning.md) aplicando todas identifican recomendaciones y comprobar que mejora el rendimiento de la base de datos. Puede usar Hola tras la ejecución de tooimprove de opciones de la base de datos:

1. Use [Asistente de base de datos de SQL](sql-database-advisor-portal.md) tooview recomendados para crear y quitar índices, parametrizar las consultas y solucionar problemas del esquema.
2. [Habilitar la optimización automática](sql-database-automatic-tuning-enable.md) y dejar que SQL Azure Database corrija problemas de rendimiento automáticamente.

## <a name="improving-database-performance-with-more-resources"></a>Mejora del rendimiento de la base de datos con más recursos

Por último, si no hay elementos procesables que pueden mejorar el rendimiento de la base de datos, puede cambiar la cantidad de Hola de recursos disponibles en la base de datos de SQL Azure. Puede asignar más recursos cambiando hello [nivel de servicio](sql-database-service-tiers.md) de una independiente de la base de datos o aumentar hello Edtu de un grupo elástico en cualquier momento.
1. Para las bases de datos independiente, también puede [cambiar los niveles de servicio](sql-database-service-tiers.md) rendimiento de base de datos a petición tooimprove.
2. Para varias bases de datos, considere el uso de [grupos elásticos](sql-database-elastic-pool-guidance.md) tooscale recursos automáticamente.

## <a name="tune-and-refactor-application-or-database-code"></a>Optimización y refactorización del código de la aplicación o base de datos

Puede cambiar toomore de código de aplicación de forma óptima usar base de datos de hello, cambiar índices, forzar los planes o usar sugerencias toomanually adaptar la carga de trabajo de tooyour de base de datos de Hola. Busque algunas directrices y sugerencias para la optimización manual y volver a escribir código de hello en hello [tema de la Guía de rendimiento](sql-database-performance-guidance.md) artículo.


## <a name="next-steps"></a>Pasos siguientes

- característica de optimización totalmente administrar la carga de trabajo, consulte tooenable automática para la optimización de base de datos de SQL Azure y permita que automática [habilitar el ajuste automático](sql-database-automatic-tuning-enable.md).
- toouse manual para la optimización, puede revisar [recomendaciones en portal de Azure de optimización](sql-database-advisor-portal.md) y aplicar manualmente hello las que mejoran el rendimiento de las consultas.
- Cambiar los recursos que están disponibles en la base de datos cambiando los [niveles de servicio de Azure SQL Database](sql-database-performance-guidance.md).