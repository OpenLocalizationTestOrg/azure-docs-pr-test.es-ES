---
title: rendimiento de aaaTroubleshoot problemas y optimizar la base de datos | Documentos de Microsoft
description: "Aplicar recomendaciones de rendimiento tooyour base de datos SQL así como borrar cómo toogain información acerca de Hola rendimiento de las consultas de Hola que se ejecuta en la base de datos"
metakeywords: azure sql database performance monitoring recommendation
services: sql-database
documentationcenter: 
manager: jhubbard
author: jan-eng
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,monitor & tune
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: janeng
ms.openlocfilehash: e948d30ac74eecf45420d5d77ef55e3c0b6f3f47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-performance-issues-and-optimize-your-database"></a>Solución de problemas de rendimiento y optimización de bases de datos

Entre los motivos comunes para un rendimiento deficiente de la base de datos se encuentran índices que faltan y consultas mal optimizadas. En este tutorial, aprenderá a:
> [!div class="checklist"]
> * Revisar, aplicar y revertir las recomendaciones para la mejora de rendimiento
> * Buscar consultas con un uso intensivo de los recursos
> * Buscar consultas de ejecución prolongada

> Necesita una carga de trabajo continua en una base de datos con problemas de rendimiento: falta un índice, por ejemplo tooreceive una recomendación.
>

## <a name="log-in-toohello-azure-portal"></a>Inicie sesión en toohello portal de Azure

Inicie sesión en toohello [portal de Azure](https://portal.azure.com/).

## <a name="review-and-apply-a-recommendation"></a>Revisión y aplicación de una recomendación

Siga estos tooapply pasos una recomendación de sistema de hello para la base de datos:

1. Haga clic en hello **recomendaciones de rendimiento** menú en la hoja de la base de datos de Hola.

    ![recomendación de rendimiento](./media/sql-database-performance-tutorial/perf_recommendations.png)

2. Seleccionar una recomendación de active en hello lista de recomendaciones. En este ejemplo, Create Index.

    ![seleccionar recomendación](./media/sql-database-performance-tutorial/create_index.png)

3. Aplique la recomendación de hello haciendo clic en hello **aplicar** botón. Si lo desea, revise los detalles de la recomendación de Hola y ver script de Hola T-SQL ejecutará demasiado haciendo clic en **ver Script** botón.

    ![aplicar recomendación](./media/sql-database-performance-tutorial/apply.png)

4. [Opcional] Habilitar el ajuste automático para toobe de recomendaciones que se aplican automáticamente.

    ![ajuste automático](./media/sql-database-performance-tutorial/auto_tuning.png)

## <a name="revert-a-recommendation"></a>Reversión de una recomendación

Hola Asesor de la base de datos supervisa cada recomendación implementado. Si una recomendación no mejora la carga de trabajo de Hola se revertirán automáticamente. Cualquier recomendación se puede revertir, pero en la mayoría de los casos no es necesario. toorevert una recomendación:

1. Vaya el menú de las recomendaciones de rendimiento de toohello y seleccione una de las recomendaciones de hello aplica.

    ![seleccionar recomendación](./media/sql-database-performance-tutorial/select.png)

2. En la vista de detalles de hello, haga clic en **Revert**.

    ![revertir recomendación](./media/sql-database-performance-tutorial/revert.png)

## <a name="find-hello-query-that-consumes-hello-most-resources"></a>Encontrar más recursos de consulta de Hola que consume Hola

Siga estas consultas de hello pasos toofind consumiendo Hola mayoría de los recursos:

1. Haga clic en hello **Query Performance Insight** menú en la hoja de la base de datos de Hola.

    ![información de consultas](./media/sql-database-performance-tutorial/query_perf_insights.png)

2. Seleccione de un tipo de recurso.

    ![información de consultas](./media/sql-database-performance-tutorial/select_resource_type.png)

3. Hola seleccione primera consulta de tabla de Hola.

    ![información de consultas](./media/sql-database-performance-tutorial/select_query.png)

4. Revise los detalles de la consulta de Hola.

    ![información de consultas](./media/sql-database-performance-tutorial/query_details.png)

## <a name="find-hello-longest-running-query"></a>Buscar consultas de ejecución más larga de Hola

1. Vaya tooQuery Performance Insight y seleccione hello **consultas de larga ejecución** ficha.

    ![información de consultas](./media/sql-database-performance-tutorial/long_running.png)

3. Hola seleccione primera consulta de tabla de Hola.

    ![información de consultas](./media/sql-database-performance-tutorial/select_first_query.png)

4. Revise los detalles de la consulta de Hola.

    ![información de consultas](./media/sql-database-performance-tutorial/review_query_details.png)



## <a name="next-steps"></a>Pasos siguientes 
Entre los motivos comunes para un rendimiento deficiente de la base de datos se encuentran índices que faltan y consultas mal optimizadas. En este tutorial aprendió lo siguiente:
> [!div class="checklist"]
> * Revisar, aplicar y revertir las recomendaciones para la mejora de rendimiento
> * Buscar consultas con un uso intensivo de los recursos
> * Buscar consultas de ejecución prolongada

[Sugerencias para la optimización del rendimiento de Base de datos SQL](https://docs.microsoft.com/azure/sql-database/sql-database-troubleshoot-performance)
