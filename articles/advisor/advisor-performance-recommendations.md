---
title: recomendaciones de Advisor rendimiento aaaAzure | Documentos de Microsoft
description: Utilice el Asistente toooptimize Hola rendimiento de las implementaciones de Azure.
services: advisor
documentationcenter: NA
author: kumudd
manager: carmonm
editor: 
ms.assetid: 
ms.service: advisor
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 11/16/2016
ms.author: kumud
ms.openlocfilehash: eb3d928664717f6f322132ac740f42015f56b76e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="advisor-performance-recommendations"></a>Recomendaciones sobre rendimiento de Advisor

Azure recomendaciones del Asistente para rendimiento ayudar a mejorar la velocidad de Hola y la capacidad de respuesta de las aplicaciones empresariales críticas. Puede obtener recomendaciones de rendimiento del asistente en hello **rendimiento** ficha del panel de Asistente de Hola.

![Pestaña Advisor Performance (Rendimiento de Advisor)](./media/advisor-performance-recommendations/advisor-performance-tab.png)

## <a name="improve-database-performance-with-sql-db-advisor"></a>Mejora del rendimiento de la base de datos con SQL DB Advisor

Advisor proporciona una vista coherente y consolidada de recomendaciones para todos los recursos de Azure. Se integran con toobring de Asistente de base de datos de SQL, recomendaciones para mejorar el rendimiento de saludo de la base de datos de SQL Azure. Asistente de base de datos de SQL evalúa rendimiento Hola de las bases de datos de SQL Azure mediante el análisis de su historial de uso. A continuación, ofrece las recomendaciones que son más adecuadas para ejecutar la carga de trabajo típica de la base de datos de Hola. 

> [!NOTE]
> recomendaciones de tooget, una base de datos debe tener una semana de uso y, dentro de esa semana debe ser una actividad coherente. SQL Database Advisor puede optimizar los patrones de consultas coherentes con más facilidad que en el caso de ráfagas aleatorias de actividad.

Para más información acerca de SQL Database Advisor, consulte [SQL Database Advisor](https://azure.microsoft.com/en-us/documentation/articles/sql-database-advisor/).

![Recomendaciones de SQL Database](./media/advisor-performance-recommendations/advisor-performance-sql.png)

## <a name="improve-redis-cache-performance-and-reliability"></a>Mejora de la confiabilidad y el rendimiento de Redis Cache

Advisor identifica las instancias de Redis Cache donde el rendimiento puede verse afectado negativamente por la utilización intensa de la memoria, la carga del servidor, el ancho de banda de red o un número elevado de conexiones de cliente. El asesor también proporciona mejores prácticas toohelp recomendaciones para evitar posibles problemas. Para obtener más información acerca de las recomendaciones de Redis Cache, vea [Advisor de Redis Cache](https://azure.microsoft.com/en-us/documentation/articles/cache-configure/#redis-cache-advisor).


## <a name="improve-app-service-performance-and-reliability"></a>Mejora de la confiabilidad y el rendimiento de App Service

Azure Advisor integra las sugerencias de los procedimientos recomendados para mejorar su experiencia de App Services y para descubrir las funciones de la plataforma adecuada. Ejemplos de recomendaciones de App Services:
* Detección de instancias en las que los tiempos de ejecución de las aplicaciones con opciones de mitigación agotan los recursos de la memoria o la CPU.
* Detección de instancias donde la colocación de recursos como aplicaciones web y bases de datos puede mejorar el rendimiento y reducir el costo. 

Para obtener más información acerca de las recomendaciones de App Services, consulte los [procedimientos recomendados para Azure App Service](https://azure.microsoft.com/en-us/documentation/articles/app-service-best-practices/).
![Recomendaciones de App Services](./media/advisor-performance-recommendations/advisor-performance-app-service.png)

## <a name="how-tooaccess-performance-recommendations-in-advisor"></a>¿Cómo tooaccess recomendaciones de rendimiento en el Asistente

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).

2. En el panel izquierdo de hello, haga clic en **más servicios**.

3. Hola servicio panel de menú, en **supervisión y administración**, haga clic en **Asistente de Azure**.  
 Hola Advisor panel se abre.

4. En el panel del Asistente de hello, haga clic en hello **rendimiento** ficha.

5. Seleccione la suscripción de hello para el que desea tooreceive recomendaciones y, a continuación, haga clic en **obtener recomendaciones**.

> [!NOTE]
> tooaccess las recomendaciones del asistente, primero debe *registrar su suscripción* con el asistente. Una suscripción se registra cuando un *suscripción propietario* inicia Hola Hola de panel y hace clic en el asistente **obtener recomendaciones** botón. Esta operación *solo se realiza una vez*. Después de registra la suscripción de hello, puede tener acceso a las recomendaciones del asistente como *propietario*, *colaborador*, o *lector* para una suscripción de un grupo de recursos, o recurso específico.

## <a name="next-steps"></a>Pasos siguientes

toolearn más información acerca de las recomendaciones del asistente, vea:

* [Introducción tooAdvisor](advisor-overview.md)
* [Introducción a Advisor](advisor-get-started.md)
* [Recomendaciones sobre el costo de Advisor](advisor-performance-recommendations.md)
* [Recomendaciones sobre alta disponibilidad de Advisor](advisor-high-availability-recommendations.md)
* [Recomendaciones sobre seguridad de Advisor](advisor-security-recommendations.md)

