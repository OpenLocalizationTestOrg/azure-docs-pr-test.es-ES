---
title: "datos de aaaSync (versión preliminar) | Documentos de Microsoft"
description: "Se trata de una introducción a Azure SQL Data Sync (versión preliminar)."
services: sql-database
documentationcenter: 
author: douglaslms
manager: craigg
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: load & move data
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: douglasl
ms.openlocfilehash: d5b2bbd6a502ba94dba7fb309a6583d2d95cc1d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="sync-data-across-multiple-cloud-and-on-premises-databases-with-sql-data-sync"></a>Sincronización de datos entre varias bases de datos locales y de la nube con SQL Data Sync

Sincronización de datos de SQL es un servicio basado en la base de datos de SQL de Azure que le permite sincronizar los datos de hello que selecciona bidireccional a través de varias bases de datos SQL y las instancias de SQL Server.

Sincronización de datos se basa en el concepto de Hola de un grupo de sincronización. Un grupo de sincronización es un grupo de bases de datos que desea toosynchronize.

Un grupo de sincronización tiene Hola propiedades siguientes:

-   Hola **esquema de sincronización** describe qué datos se están sincronizando.

-   Hola **dirección de sincronización** puede ser bidireccional o pueden fluir en una única dirección. Es decir, Hola puede ser la dirección de sincronización *concentrador tooMember* o *tooHub miembro*, o ambos.

-   Hola **intervalo de sincronización** es con qué frecuencia se produce la sincronización.

-   Hola **directiva de resolución de conflictos** es una directiva de nivel de grupo, que puede ser *gana la central* o *wins miembro*.

Sincronización de datos utiliza un datos de toosynchronize de topología de concentrador y radio. Define una de las bases de datos de hello en el grupo de Hola como base de datos central de Hola. resto de Hola de bases de datos de hello son bases de datos miembro. Sincronización solo se produce entre hello concentrador y miembros individuales.
-   Hola **base de datos central** debe ser una base de datos de SQL Azure.
-   Hola **bases de datos miembro** puede ser bases de datos SQL, bases de datos de SQL Server local o instancias de SQL Server en máquinas virtuales de Azure.
-   Hola **base de datos de sincronización** contiene metadatos de Hola y de registro de sincronización de datos. Hola base de datos de sincronización tiene toobe una base de datos de SQL Azure ubicada en hello misma región que la base de datos central de Hola. Hola base de datos de sincronización es creado y propiedad del cliente.

> [!NOTE]
> Si usa una base de datos local, tiene demasiado[configurar un agente local.](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-get-started-sql-data-sync)

![Sincronización de datos entre bases de datos](media/sql-database-sync-data/sync-data-overview.png)

## <a name="when-toouse-data-sync"></a>Cuando toouse Data Sync

Sincronización de datos es útil en casos donde datos necesitan toobe mantiene toodate a través de varias bases de datos de SQL Azure o las bases de datos de SQL Server. Estos son los casos de uso principales de hello para la sincronización de datos:

-   **La sincronización de datos híbrido:** con la sincronización de datos, puede mantener los datos sincronizados entre bases de datos locales y aplicaciones híbridas de tooenable de bases de datos de SQL Azure. Esta capacidad puede apelar toocustomers que se va a mover en la nube toohello y desearía tooput algunos de sus aplicaciones de Azure.

-   **Las aplicaciones distribuidas:** en muchos casos, resulta beneficioso tooseparate distintas cargas de trabajo a través de diferentes bases de datos. Por ejemplo, si tiene una base de datos de producción de gran tamaño, pero también necesita toorun un informe o la carga de trabajo de análisis en estos datos, resulta útil toohave una segunda base de datos para esta carga de trabajo adicional. Este enfoque minimiza el impacto de rendimiento de hello en la carga de trabajo de producción. Puede usar estas dos bases de datos sincronizadas de tookeep de sincronización de datos.

-   **Aplicaciones globalmente distribuidas:** muchas empresas abarcan varias regiones e incluso varios países. latencia de red toominimize, es mejor toohave cerrar los datos en una región tooyou. Con la sincronización de datos, puede mantener fácilmente las bases de datos en regiones Hola mundo sincronizado.

No se recomienda Data Sync para hello los escenarios siguientes:

-   Recuperación ante desastres

-   Escalado de lectura

-   ETL (OLTP tooOLAP)

-   Migración de tooAzure de SQL Server local base de datos SQL

## <a name="how-does-data-sync-work"></a>¿Cómo funciona Data Sync? 

-   **Seguimiento de cambios de datos:** Data Sync realiza un seguimiento de cambios mediante los desencadenadores de inserción, actualización y eliminación. cambios de Hola se registran en una tabla de base de datos de usuario de Hola.

-   **Sincronización de datos:** Data Sync está diseñado en un modelo de concentrador y radio. Hello concentrador se sincroniza con cada miembro individualmente. Cambios de hello concentrador están miembro de toohello descargado y, a continuación, cambios de miembros de Hola están cargado toohello concentrador.

-   **Resolución de conflictos:** Data Sync proporciona dos opciones para la resolución de conflictos, *Prevalece la base de datos central* o *Prevalece el cliente*.
    -   Si selecciona *gana la central*, cambios de hello en el concentrador de hello siempre sobrescriben los cambios en miembro de Hola.
    -   Si selecciona *wins miembro*, Hola cambios en cambios de sobrescritura de miembro de Hola de concentrador de Hola. Si hay más de un miembro, valor final Hola depende de qué miembros se sincroniza en primer lugar.

## <a name="limitations-and-considerations"></a>Limitaciones y consideraciones

### <a name="performance-impact"></a>Impacto en el rendimiento
Sincronización de datos usa inserta, actualiza y elimina desencadenadores tootrack cambios. Crea tablas de base de datos de usuario de hello para el seguimiento de cambios. Estas actividades de seguimiento de cambios afectan a la carga de trabajo de la base de datos. Evalúe el nivel de servicio y realice la actualización si fuera necesario.

### <a name="eventual-consistency"></a>Coherencia final
Como Data Sync se basa en desencadenadores, la coherencia transaccional no está garantizada. Microsoft garantiza que todos los cambios se realicen finalmente y que Data Sync no ocasione pérdida de datos.

### <a name="unsupported-data-types"></a>Tipos de datos no admitidos

-   Secuencia de archivos

-   UDT SQL/CLR

-   XMLSchemaCollection (XML admitido)

-   Cursor, Timestamp, Hierarchyid

### <a name="requirements"></a>Requisitos

-   Cada tabla debe tener una clave principal.

-   Una tabla no puede tener una columna de identidad que no es clave principal de Hola.

-   nombres de Hola de objetos (bases de datos, tablas y columnas) no pueden contener Hola caracteres imprimibles punto (.), corchete ([]), o corchete de (]).

### <a name="limitations-on-service-and-database-dimensions"></a>Limitaciones de las dimensiones de la base de datos y del servicio

|                                                                 |                        |                             |
|-----------------------------------------------------------------|------------------------|-----------------------------|
| **Dimensiones**                                                      | **Límite**              | **Solución alternativa**              |
| Número máximo de grupos de sincronización a los que una base de datos puede pertenecer       | 5                      |                             |
| Número máximo de puntos de conexión en un único grupo de sincronización              | 30                     | Crear varios grupos de sincronización |
| Número máximo de puntos de conexión locales en un único grupo de sincronización | 5                      | Crear varios grupos de sincronización |
| Nombres de base de datos, tabla, esquema y columna                       | 50 caracteres por nombre |                             |
| Tablas de un grupo de sincronización                                          | 500                    | Crear varios grupos de sincronización |
| Columnas de una tabla de un grupo de sincronización                              | 1000                   |                             |
| Tamaño de la fila de datos en una tabla                                        | 24 Mb                  |                             |
| Intervalo de sincronización mínimo                                           | 5 minutos              |                             |

## <a name="common-questions"></a>Preguntas frecuentes

### <a name="how-frequently-can-data-sync-synchronize-my-data"></a>¿Con qué frecuencia puede sincronizar mis datos 
Data Sync? 
frecuencia mínima de Hello es cada cinco minutos.

### <a name="can-i-use-data-sync-toosync-between-sql-server-on-premises-databases-only"></a>¿Puedo usar toosync de sincronización de datos entre SQL Server local sólo bases de datos? 
No directamente. Puede sincronizar entre bases de datos de SQL Server local indirectamente, sin embargo, mediante la creación de una base de datos central en Azure y, a continuación, Agregar grupo de sincronización de toohello de hello local las bases de datos.
   
### <a name="can-i-use-data-sync-tooseed-data-from-my-production-database-tooan-empty-database-and-then-keep-them-synchronized"></a>¿Puedo usar datos de sincronización de datos de tooseed de mi base de datos producción vacía tooan de base de datos y, a continuación, mantenerlos sincronizados? 
Sí. Crear manualmente el esquema de hello en nueva base de datos de hello mediante scripting de hello original. Después de crear el esquema de hello, agregar datos de saludo tablas tooa sincronización grupo toocopy Hola y mantenerlo sincronizado.

### <a name="why-do-i-see-tables-that-i-did-not-create"></a>¿Por qué veo tablas que no he creado?  
Data Sync crea tablas laterales en su base de datos para hacer un seguimiento de los cambios. No las elimine, ya que Data Sync dejaría de funcionar.
   
### <a name="i-got-an-error-message-that-said-cannot-insert-hello-value-null-into-hello-column-column-column-does-not-allow-nulls-what-does-this-mean-and-how-can-i-fix-hello-error"></a>Recibí un mensaje de error que dice "no se puede insertar valores NULL de hello en columna de hello \<columna\>. La columna no admite valores NULL." ¿Qué significa esto y ¿cómo puedo solucionar error Hola? 
Este mensaje de error indica que uno de los siguientes problemas de dos hello:
1.  Puede haber una tabla sin una clave principal. toofix este problema, agregue una tablas de hello tooall de clave principal está sincronizando.
2.  Puede haber una cláusula WHERE en la instrucción CREATE INDEX. La sincronización no controla esta condición. toofix este problema, quite la cláusula WHERE de Hola o realizar cambios de hello manualmente las bases de datos de tooall. 
 
### <a name="how-does-data-sync-handle-circular-references-that-is-when-hello-same-data-is-synced-in-multiple-sync-groups-and-keeps-changing-as-a-result"></a>¿Cómo trata Data Sync las referencias circulares? ¿Es decir, cuando hello mismos datos se sincronizan en varios grupos de sincronización y sigue cambiando como resultado?
Data Sync no controla las referencias circulares, Ser tooavoid seguro de ellos. 

## <a name="next-steps"></a>Pasos siguientes

Para más información sobre SQL Data Sync, consulte:

-   [Introducción a SQL Data Sync](sql-database-get-started-sql-data-sync.md)

-   Completar los ejemplos de PowerShell que muestran cómo tooconfigure SQL Data Sync:
    -   [Usar PowerShell toosync entre varias bases de datos de SQL Azure](scripts/sql-database-sync-data-between-sql-databases.md)
    -   [Usar PowerShell toosync entre una base de datos de SQL Azure y una base de datos de SQL Server local](scripts/sql-database-sync-data-between-azure-onprem.md)

-   [Descargar documentación técnica de hello completa de SQL Data Sync](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_full_documentation.pdf?raw=true)

-   [Descargue la documentación de API de REST de sincronización de datos de SQL de Hola](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_REST_API.pdf?raw=true)

Para más información sobre SQL Database, consulte:

-   [Información general de SQL Database](sql-database-technical-overview.md)

-   [Administración del ciclo de vida de las aplicaciones](https://msdn.microsoft.com/library/jj907294.aspx)
