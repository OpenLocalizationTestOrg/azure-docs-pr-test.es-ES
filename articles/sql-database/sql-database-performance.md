---
title: aaaMonitor y mejorar el rendimiento - base de datos de SQL de Azure | Documentos de Microsoft
description: "Hola que la base de datos SQL Azure proporciona un rendimiento de las herramientas toohelp identificar áreas que pueden mejorar el rendimiento de la consulta actual."
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: monicar
ms.assetid: a60b75ac-cf27-4d73-8322-ee4d4c448aa2
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/19/2016
ms.author: sstein
ms.openlocfilehash: 84b8a1bc62698a29deb49e765f208bd7e14d0870
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-improve-performance"></a>Supervisión y mejora del rendimiento
Azure SQL Database identifica posibles problemas en la base de datos y recomienda las acciones que pueden mejorar el rendimiento de la carga de trabajo mediante recomendaciones y acciones de optimización inteligentes.

tooreview el rendimiento de la base de datos, use hello **rendimiento** de mosaico en la página de información general de Hola o navegar hacia abajo demasiado "Compatibilidad con + solución de problemas" sección:

   ![Vista Rendimiento](./media/sql-database-performance/entries.png)

En la sección "Compatibilidad con + solución de problemas" de Hola, puede usar Hola siguientes páginas:


1. [Información general sobre rendimiento](#performance-overview) toomonitor rendimiento de la base de datos. 
2. [Recomendaciones de rendimiento](#performance-recommendations) toofind recomendaciones de rendimiento que pueden mejorar el rendimiento de la carga de trabajo.
3. [Consultar información de rendimiento de](#query-performance-insight) toofind las consultas que consumen más de los recursos.
4. [El ajuste automático](#automatic-tuning) toolet base de datos de SQL Azure optimice automáticamente la base de datos.

## <a name="performance-overview"></a>Información general de rendimiento
Esta vista ofrece un resumen del rendimiento de la base de datos y le ayuda con la optimización y solución de problemas de rendimiento. 

![Rendimiento](./media/sql-database-performance/performance.png)

* Hola **recomendaciones** mosaico proporciona un desglose de recomendaciones para la base de datos de optimización (tres primeras se muestran recomendaciones si hay más). Al hacer clic en este icono le lleva demasiado**[recomendaciones de rendimiento](#performance-recommendations)**. 
* Hola **para la optimización actividad** mosaico proporciona un resumen de hello en curso y completada las acciones para la base de datos para la optimización, lo que le ofrece una vista rápida de historial de Hola de actividad para la optimización. Al hacer clic en este icono, se le toohello completa para la optimización vista Historial para la base de datos.
* Hola **ajuste automático** icono muestra hello [ajuste automático de la configuración](sql-database-automatic-tuning-enable.md) para la base de datos (optimización de opciones de base de datos de tooyour automáticamente aplicado). Al hacer clic en este icono abre el cuadro de diálogo de configuración de automatización de Hola.
* Hola **consultas de base de datos** mosaico muestra Hola resumen del rendimiento de las consultas de hello para la base de datos (general DTU uso y los principales consultas que consumen recursos). Al hacer clic en este icono le lleva demasiado**[Query Performance Insight](#query-performance-insight)**.

## <a name="performance-recommendations"></a>Recomendaciones de rendimiento
En esta página se proporcionan [recomendaciones de ajuste](sql-database-advisor.md) inteligentes que pueden mejorar el rendimiento de la base de datos. Hola siguientes tipos de recomendaciones se muestra en esta página:

* Obtener recomendaciones sobre qué índices toocreate o drop.
* Recomendaciones cuando se identifiquen problemas del esquema de base de datos de Hola.
* Recomendaciones en caso de consultas que puedan beneficiarse de consultas parametrizadas.

![Rendimiento](./media/sql-database-performance/recommendations.png)

También puede encontrar el historial completo de las acciones que se aplicaron en hello pasado para la optimización.

Obtenga información acerca de cómo toofind apply recomendaciones de rendimiento en [buscar y aplicar las recomendaciones de rendimiento](sql-database-advisor-portal.md) artículo.

## <a name="automatic-tuning"></a>Ajuste automático
Las bases de datos de Azure SQL Database puede optimizar automáticamente el rendimiento de base de datos mediante la aplicación de [recomendaciones de rendimiento](sql-database-advisor.md). más información, lea toolearn [artículo optimización automática](sql-database-automatic-tuning.md). tooenable, leer [cómo el ajuste automático de tooenable](sql-database-automatic-tuning-enable.md).

## <a name="query-performance-insight"></a>Información de rendimiento de consultas
[Consultar información de rendimiento de](sql-database-query-performance.md) permite toospend menos tiempo a la solución de problemas de rendimiento de la base de datos al proporcionar:

* Información más detallada sobre el consumo de recursos (DTU) de las bases de datos. 
* Hola que consuman más CPU consultas, que pueden optimizarse para mejorar el rendimiento. 
* Hola capacidad toodrill hacia abajo en los detalles de Hola de una consulta. 

  ![panel de rendimiento](./media/sql-database-query-performance/performance.png)

Obtener más información acerca de esta página en el artículo de hello  **[cómo toouse Query Performance Insight](sql-database-query-performance.md)**.

## <a name="additional-resources"></a>Recursos adicionales
* [Guía de rendimiento de Azure SQL Database](sql-database-performance-guidance.md)
* [¿Cuándo se debe utilizar un grupo elástico?](sql-database-elastic-pool-guidance.md)

