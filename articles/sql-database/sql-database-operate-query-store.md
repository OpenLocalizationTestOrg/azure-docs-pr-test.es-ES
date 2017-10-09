---
title: "aaaOperating almacén de consultas de base de datos de SQL Azure"
description: "Obtenga información acerca de cómo toooperate Hola almacén de consultas de base de datos de SQL Azure"
keywords: 
services: sql-database
documentationcenter: 
author: bonova
manager: jhubbard
editor: 
ms.assetid: 0cccf6bd-1327-44f7-a6f9-8eff0c210463
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: sqldb-performance
ms.workload: data-management
ms.date: 11/08/2016
ms.author: bonova
ms.openlocfilehash: ab741e49685bf6df3bceab219aaf57ea51cdb25d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="operating-hello-query-store-in-azure-sql-database"></a>Hola funcionamiento almacén de consultas de base de datos de SQL Azure
El Almacén de consultas en Azure es una característica de base de datos completamente administrada que recopila y presenta constantemente información histórica detallada sobre todas las consultas. Puede pensar en el almacén de consultas como caja negra de datos del avión tooan similar que significativamente simplifica la solución de problemas para la nube de rendimiento de las consultas y los clientes locales. En este artículo se explican los aspectos específicos del funcionamiento del Almacén de consultas de Azure. Con estos datos de consulta previamente recopilados, puede diagnosticar y resolver rápidamente los problemas de rendimiento y así dedicar más tiempo a centrarse en sus negocios. 

El Almacén de consultas está [disponible globalmente](https://azure.microsoft.com/updates/general-availability-azure-sql-database-query-store/) en Base de datos SQL de Azure desde noviembre de 2015. Almacén de consultas está foundation hello para el análisis de rendimiento y optimización de características, como [Asistente de base de datos de SQL y el panel de rendimiento](https://azure.microsoft.com/updates/sqldatabaseadvisorga/). En el momento de hello sobre la publicación de este artículo, el almacén de consultas se está ejecutando en más de 200.000 bases de datos de usuario en Azure, recopilar información relacionada con la consulta durante varios meses, sin interrupción.

> [!IMPORTANT]
> Microsoft está en proceso de saludo de activación de almacén de consultas para todas las bases de datos de SQL Azure (existentes y nuevos). 
> 
> 

## <a name="optimal-query-store-configuration"></a>Configuración óptima del Almacén de consultas
Esta sección describen los valores predeterminados de la configuración óptima que se tooensure diseñado un funcionamiento confiable del almacén de consultas de Hola y las características dependientes, como [Asistente de base de datos de SQL y el panel de rendimiento](https://azure.microsoft.com/updates/sqldatabaseadvisorga/). La configuración predeterminada está optimizada para una recopilación continua de los datos, es decir, un tiempo mínimo en los estados OFF y READ_ONLY.

| Configuración | Description | Valor predeterminado | Comentario |
| --- | --- | --- | --- |
| MAX_STORAGE_SIZE_MB |Especifica el límite de Hola Hola espacio de datos que puede llevar a cabo el almacén de consultas dentro de la base de datos de clientes de z |100 |Se aplica a nuevas bases de datos. |
| INTERVAL_LENGTH_MINUTES |Define el tamaño de la ventana de tiempo durante la que se agregan y conservan las estadísticas recopiladas en tiempo de ejecución para los planes de consulta. Todos los planes de consulta activa tienen al menos una fila durante un período de tiempo definido con esta configuración. |60 |Se aplica a nuevas bases de datos. |
| STALE_QUERY_THRESHOLD_DAYS |Directiva de limpieza basada en el tiempo que controla el período de retención de Hola de estadísticas de tiempo de ejecución persistentes y las consultas inactivas |30 |Se aplica a nuevas bases de datos y bases de datos con la configuración predeterminada anterior (367). |
| SIZE_BASED_CLEANUP_MODE |Especifica si la limpieza automática de los datos tiene lugar cuando el tamaño de datos de almacén de consultas aproxime el límite de Hola |AUTO |Se aplica a todas las bases de datos. |
| QUERY_CAPTURE_MODE |Especifica si se realiza el seguimiento de todas las consultas o solo de un subconjunto de estas. |AUTO |Se aplica a todas las bases de datos. |
| FLUSH_INTERVAL_SECONDS |Especifica el periodo máximo durante el cual las estadísticas del runtime capturada se mantienen en memoria, antes del vaciado toodisk |900 |Se aplica a nuevas bases de datos. |
|  | | | |

> [!IMPORTANT]
> Estos valores predeterminados se aplican automáticamente en la fase final de saludo de activación de almacén de consultas en todas las bases de datos de SQL Azure (vea la nota importante anterior). Después de esta luz de una base de datos de SQL Azure no cambiar los valores de configuración establecidos por los clientes, a menos que afecten negativamente a operaciones confiables de hello almacén de consultas o carga de trabajo principal.
> 
> 

Si desea toostay con su configuración personalizada, utilice [ALTER DATABASE con las opciones de almacén de consultas](https://msdn.microsoft.com/library/bb522682.aspx) estado anterior de toorevert configuración toohello. Extraer del repositorio [prácticas recomendadas con hello almacén de consultas](https://msdn.microsoft.com/library/mt604821.aspx) en orden toolearn cómo superior eligió parámetros de configuración óptima.

## <a name="next-steps"></a>Pasos siguientes
[SQL Database Performance Insight (Información de rendimiento de Base de datos SQL)](sql-database-performance.md)

## <a name="additional-resources"></a>Recursos adicionales
Para más información desproteger Hola siguientes artículos:

* [A flight data recorder for your database (Una caja negra para la base de datos)](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database) 
* [Supervisión de rendimiento usando el almacén de consultas de Hola](https://msdn.microsoft.com/library/dn817826.aspx)
* [Query Store Usage Scenarios (Escenarios de uso del Almacén de consultas)](https://msdn.microsoft.com/library/mt614796.aspx)
* [Supervisión de rendimiento usando el almacén de consultas de Hola](https://msdn.microsoft.com/library/dn817826.aspx) 

