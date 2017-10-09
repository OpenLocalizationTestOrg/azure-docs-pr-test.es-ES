---
title: almacenamiento en memoria de aaaMonitor XTP | Documentos de Microsoft
description: Estimar y supervisar el uso y la capacidad del almacenamiento en memoria de XTP; resolver el error de capacidad 41823
services: sql-database
documentationcenter: 
author: jodebrui
manager: jhubbard
editor: 
ms.assetid: b617308e-692c-4938-8fa2-070034a3ecef
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/19/2016
ms.author: jodebrui
ms.openlocfilehash: fcb17bd8e9ebef4862d4b55bf5a79b45b9419fca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-in-memory-oltp-storage"></a>Supervisión del almacenamiento OLTP en memoria
Cuando se usa [OLTP en memoria](sql-database-in-memory.md), los datos de tablas con optimización de memoria y las variables de tabla residen en el almacenamiento OLTP en memoria. Cada nivel de servicio Premium tiene un tamaño máximo de almacenamiento de OLTP en memoria, que se documenta en hello [artículo niveles de servicio de base de datos de SQL](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels). Una vez que se supera ese límite, las operaciones de inserción y actualización pueden empezar a producir errores (con el error 41823). En ese momento se necesitan tooeither eliminar datos tooreclaim memoria o actualizar el nivel de rendimiento de saludo de la base de datos.

## <a name="determine-whether-data-will-fit-within-hello-in-memory-storage-cap"></a>Determinar si los datos se ajustan dentro del límite de almacenamiento en memoria de Hola
Determinar el límite de almacenamiento de hello: consulte hello [artículo niveles de servicio de base de datos de SQL](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) para los límites de almacenamiento de Hola de distintos niveles de servicio Premium Hola.

Calcular la memoria requisitos para una tabla con optimización para memoria funciona igual Hola forma para SQL Server tal como se hace en la base de datos de SQL Azure. Desconectar de ese tema tooreview unos minutos en [MSDN](https://msdn.microsoft.com/library/dn282389.aspx).

Tenga en cuenta que la tabla de Hola y filas de variables de tabla, así como índices, cuentan para tamaño de datos de usuario max Hola. Además, ALTER TABLE necesita suficiente toocreate sala una nueva versión de toda la tabla hello y sus índices.

## <a name="monitoring-and-alerting"></a>Supervisión y alertas
Puede supervisar el uso de almacenamiento en memoria como un porcentaje de hello [límite de almacenamiento para el nivel de rendimiento](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) en hello Azure [portal](https://portal.azure.com/): 

* En la hoja de la base de datos de hello, busque el cuadro de utilización de recursos de Hola y haga clic en Editar.
* A continuación, seleccione la métrica de hello `In-Memory OLTP Storage percentage`.
* tooadd una alerta, haga clic en la hoja de métricas de hello utilización de recursos cuadro tooopen hello, a continuación, haga clic en Agregar alerta.

O bien utilizar Hola después de utilización del almacenamiento en memoria de consulta tooshow hello:

    SELECT xtp_storage_percent FROM sys.dm_db_resource_stats


## <a name="correct-out-of-memory-situations---error-41823"></a>Corrección de situaciones de falta de memoria (error 41823)
Si el sistema se queda sin memoria, las operaciones INSERT, UPDATE y CREATE no se llevarán a cabo, y se mostrará el mensaje de error 41823.

Mensaje de error 41823 indica que las tablas optimizadas en memoria de Hola y las variables de tabla han superado el tamaño máximo de Hola.

tooresolve este error, ya sea:

* Eliminar datos de tablas optimizadas en memoria de hello, potencialmente descarga Hola datos tootraditional, las tablas basadas en disco; o bien,
* Actualizar tooone de nivel de servicio de hello con suficiente almacenamiento en memoria para los datos de hello debe tookeep en tablas optimizadas en memoria.

## <a name="next-steps"></a>Pasos siguientes
Para obtener instrucciones sobre la supervisión, consulte [Supervisión de Azure SQL Database con vistas de administración dinámica](sql-database-monitoring-with-dmvs.md).
