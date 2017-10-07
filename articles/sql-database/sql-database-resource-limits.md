---
title: "Límites de recursos de base de datos de SQL aaaAzure | Documentos de Microsoft"
description: "En esta página se describen algunos límites de recursos comunes para Base de datos SQL de Azure."
services: sql-database
documentationcenter: na
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 884e519f-23bb-4b73-a718-00658629646a
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/12/2017
ms.author: carlrab
ms.openlocfilehash: 3e7be4fdc74e802d37274690531caaf138bcedb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-resource-limits"></a>Límites de recursos de Base de datos SQL
## <a name="overview"></a>Información general
La base de datos de SQL Azure administra Hola recursos disponibles tooa base de datos mediante dos mecanismos diferentes: **regulación de recursos** y **cumplimiento de límites**. Este tema explica estas dos áreas principales de la administración de recursos.

## <a name="resource-governance"></a>Regulador de recursos
Uno de los objetivos de diseño de Hola de niveles de servicio Basic, Standard, Premium y Premium RS hello es como si la base de datos de Hola se ejecuta en su propia máquina, aislada de otras bases de datos para toobehave de base de datos de SQL Azure. La regulación de recursos emula este comportamiento. Si agrega Hola utilización de recursos alcanza Hola máxima disponible CPU, memoria, E/S de registro y base de datos de toohello asignado de recursos de E/S de datos, la regulación de recursos de las consultas de las colas en ejecución y asignar recursos toohello en cola las consultas que libere.

Como en un equipo dedicado, utilización de todos los resultados de recursos disponibles en una ejecución más larga de ejecución de las consultas, lo que puede traducirse en los tiempos de espera de comando en el cliente de Hola. Las aplicaciones con lógica de reintento agresiva y las aplicaciones que se ejecutan consultas en la base de datos de hello con gran frecuencia pueden encontrar mensajes de error al intentar tooexecute nuevas consultas cuando se ha alcanzado el límite de Hola de solicitudes simultáneas.

### <a name="recommendations"></a>Recomendaciones:
Supervisar el uso de recursos de Hola y tiempos de respuesta promedio de Hola de consultas cuando se acerque a la utilización máxima de Hola de una base de datos. Cuando encuentre latencias de consulta más elevadas generalmente tienen tres opciones:

1. Reduzca el número de Hola de entrante solicitudes toohello base de datos tooprevent hello y tiempo de espera apilen de solicitudes.
2. Asignar una base de datos de toohello de nivel superior de rendimiento.
3. Optimizar la utilización de recursos de las consultas tooreduce Hola de cada consulta. Para obtener más información, consulte la sección de optimización/sugerencias de consulta en el artículo de guía de rendimiento de base de datos de SQL Azure Hola Hola.

## <a name="enforcement-of-limits"></a>Aplicación de límites
Al denegar nuevas solicitudes cuando se alcanzan los límites, se aplican recursos otros recursos diferentes de la CPU, memoria, registro de E/S y datos de E/S. Cuando una base de datos alcanza el límite de tamaño máximo de hello configurado, inserciones y actualizaciones que aumentarán el tamaño de datos producirá un error, mientras selecciona y elimina continuar toowork. Los clientes reciben una [mensaje de error](sql-database-develop-error-messages.md) según el límite de Hola que se ha alcanzado.

Por ejemplo, número de Hola de base de datos SQL de las conexiones tooa y número de Hola de solicitudes simultáneas que pueden ser procesados están restringidos. Base de datos SQL permite a Hola número de conexiones toohello base de datos toobe mayor número de Hola de agrupación de conexiones de toosupport de solicitudes simultáneas. Aunque el número de Hola de conexiones que están disponibles fácilmente puede controlarse mediante la aplicación hello, Hola número de solicitudes paralelas suele veces más difícil tooestimate y toocontrol. Especialmente durante las cargas punta cuando Hola aplicación envía demasiadas solicitudes o base de datos de hello alcanza su límite de recursos y empieza a apilar subprocesos de trabajo debido a las consultas en ejecución toolonger, se pueden encontrar errores.

## <a name="service-tiers-and-performance-levels"></a>Niveles de servicio y niveles de rendimiento
Existen niveles de servicio y rendimiento para los grupos elásticos y bases de datos únicas.

### <a name="single-databases"></a>Bases de datos únicas
Para una base de datos, Hola base de datos servicio capa y nivel de rendimiento define los límites de Hola de una base de datos. Hello en la tabla siguiente describe las características de Hola de bases de datos Basic, Standard, Premium y Premium RS en distintos niveles de rendimiento.

[!INCLUDE [SQL DB service tiers table](../../includes/sql-database-service-tiers-table.md)]

> [!IMPORTANT]
> Pueden usar los clientes que usan los niveles de rendimiento P11 y P15 hasta too4 TB de almacenamiento incluyen sin cargo adicional. Esta opción de 4 TB está disponible actualmente en hello siguientes regiones: nos East2, oeste de Estados Unidos, nos Gov Virginia, Europa occidental, Alemania Central, sur Asia oriental, este de Japón, Australia Oriental, Canadá Central y este de Canadá.
>

### <a name="elastic-pools"></a>Grupos elásticos
[Grupos elásticos](sql-database-elastic-pool.md) compartir recursos entre las bases de datos en bloque de Hola. Hello en la tabla siguiente describe las características de Hola de Basic, Standard, Premium y Premium RS grupos elásticos.

[!INCLUDE [SQL DB service tiers table for elastic databases](../../includes/sql-database-service-tiers-table-elastic-pools.md)]

Para una definición expandida de cada recurso que se enumeran en hello anterior tablas, vea las descripciones de hello en [límites y capacidades de nivel de servicio](sql-database-performance-guidance.md#service-tier-capabilities-and-limits). Para obtener una descripción general de los niveles de servicio, consulte [Niveles de servicio y niveles de rendimiento de Base de datos SQL de Azure](sql-database-service-tiers.md).

## <a name="other-sql-database-limits"></a>Otros límites de Base de datos SQL
| Ámbito | Límite | Description |
| --- | --- | --- |
| Bases de datos que usan exportación automatizada por suscripción |10 |Exportación automatizada permite toocreate una programación personalizada para copia de seguridad de las bases de datos SQL. vista previa de Hola de esta característica va a finalizar en el 1 de marzo de 2017.  |
| Bases de datos por servidor |Seguridad too5000 |Seguridad too5000 se permiten las bases de datos por servidor. |
| DTU por servidor |45000 |Se permiten 45000 DTU por servidor para el aprovisionamiento de bases de datos independientes y grupos elásticos. número total de Hola de bases de datos independiente y grupos permitidas por el servidor está limitado únicamente por número de Hola de servidor Dtu.  

> [!IMPORTANT]
> La exportación automática de Azure SQL Database Automated Export se encuentra ahora en versión preliminar y se retirará el 1 de marzo de 2017. A partir del 1 de diciembre de 2016, ya no podrás exportación puede tooconfigure automatizada en cualquier base de datos SQL. Todos los trabajos de exportación automatizada existente continuará toowork hasta el 1 de marzo de 2017. Después del 1 de diciembre de 2016, puede usar [retención de copia de seguridad a largo plazo](sql-database-long-term-retention.md) o [automatización de Azure](../automation/automation-intro.md) tooarchive bases de datos SQL periódicamente con PowerShell periódicamente según programación tooa de su elección. Para obtener un script de ejemplo, puede descargar hello [GitHub del script de ejemplo](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-automation-automated-export).
>


## <a name="resources"></a>Recursos
[Límites, cuotas y restricciones de suscripción y servicios de Microsoft Azure](../azure-subscription-service-limits.md)

[Niveles de servicio y niveles de rendimiento de la Base de datos SQL de Azure](sql-database-service-tiers.md)

[Mensajes de error para los programas de cliente de base de datos SQL](sql-database-develop-error-messages.md)
