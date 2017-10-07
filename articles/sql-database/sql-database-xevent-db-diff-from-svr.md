---
title: eventos de aaaExtended en la base de datos SQL | Documentos de Microsoft
description: "Describe los eventos extendidos (XEvents) en Base de datos SQL de Azure y cómo las sesiones de eventos difieren ligeramente de las sesiones de eventos en Microsoft SQL Server."
services: sql-database
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: 
tags: 
ms.assetid: 3b28cf15-f820-4b3c-8310-908d6d5b9d0c
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2017
ms.author: genemi
ms.openlocfilehash: 8c966a84412aa561c92b16e5c6902102483eb1bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="extended-events-in-sql-database"></a>Eventos extendidos en Base de datos SQL
[!INCLUDE [sql-database-xevents-selectors-1-include](../../includes/sql-database-xevents-selectors-1-include.md)]

Este tema explica la implementación de Hola de eventos extendidos en base de datos de SQL Azure es eventos tooextended comparados ligeramente diferente en Microsoft SQL Server.

- V12 de base de datos de SQL había obtenido característica eventos extendidos de Hola Hola en segundo lugar la mitad del calendario 2015.
- SQL Server tiene eventos extendidos desde 2008.
- conjunto de características de Hola de eventos extendidos en base de datos SQL es un subconjunto robusto de características de hello en SQL Server.

*XEvents* es un sobrenombre informal que a veces se usa para los eventos extendidos en blogs y otras referencias informales.

Se puede encontrar información adicional sobre eventos extendidos, para Base de datos SQL de Azure y Microsoft SQL Server, en:

- [Quick Start: Extended events in SQL Server](http://msdn.microsoft.com/library/mt733217.aspx)
- [Eventos extendidos](http://msdn.microsoft.com/library/bb630282.aspx)

## <a name="prerequisites"></a>Requisitos previos

En este tema se da por sentado que ya tiene algunos conocimientos sobre:

- [Servicio Base de datos SQL de Azure](https://azure.microsoft.com/services/sql-database/).
- [Eventos extendidos](http://msdn.microsoft.com/library/bb630282.aspx) en Microsoft SQL Server.

- masiva Hola de nuestra documentación sobre los eventos extendidos aplica tooboth SQL Server y base de datos SQL.

Toohello de exposición anteriores siguientes elementos es útil cuando se elige el archivo de eventos como Hola Hola [destino](#AzureXEventsTargets):

- [Servicio Almacenamiento de Azure](https://azure.microsoft.com/services/storage/)


- PowerShell
    - [Uso de PowerShell de Azure con el almacenamiento de Azure](../storage/common/storage-powershell-guide-full.md) -proporciona información completa sobre hello servicio de almacenamiento de Azure y PowerShell.

## <a name="code-samples"></a>Ejemplos de código

Los temas relacionados proporcionan dos ejemplos de código:


- [Código de destino de búfer en anillo para eventos extendidos en Base de datos SQL](sql-database-xevent-code-ring-buffer.md)
    - Breve script de Transact-SQL simple.
    - Se resaltan en el tema de ejemplo de código de hello que, cuando haya terminado con un destino de búfer en anillo, debe liberar sus recursos mediante la ejecución de una lista de alter `ALTER EVENT SESSION ... ON DATABASE DROP TARGET ...;` instrucción. Más adelante, puede agregar otra instancia de búfer en anillo de `ALTER EVENT SESSION ... ON DATABASE ADD TARGET ...`.


- [Código de destino del archivo de evento para eventos extendidos en Base de datos SQL](sql-database-xevent-code-event-file.md)
    - Fase 1 es PowerShell toocreate un contenedor de almacenamiento de Azure.
    - Fase 2 es Transact-SQL que utiliza el contenedor de almacenamiento de Azure de Hola.

## <a name="transact-sql-differences"></a>Diferencias de Transact-SQL


- Cuando se ejecuta hello [CREATE EVENT SESSION](http://msdn.microsoft.com/library/bb677289.aspx) de comandos en SQL Server, usar hello **ON SERVER** cláusula. Pero en la base de datos SQL usar hello **ON DATABASE** cláusula en su lugar.


- Hola **ON DATABASE** cláusula también aplica toohello [ALTER EVENT SESSION](http://msdn.microsoft.com/library/bb630368.aspx) y [DROP EVENT SESSION](http://msdn.microsoft.com/library/bb630257.aspx) comandos Transact-SQL.


- Una práctica recomendada es la opción de sesión de eventos tooinclude Hola de **STARTUP_STATE = ON** en su **CREATE EVENT SESSION** o **ALTER EVENT SESSION** instrucciones.
    - Hola **= ON** valor admite un reinicio automático después de volver a configurar una base de datos lógico de hello debido tooa conmutación por error.

## <a name="new-catalog-views"></a>Nuevas vistas de catálogo

Hello característica eventos extendidos varias admiten [vistas de catálogo](http://msdn.microsoft.com/library/ms174365.aspx). Vistas de catálogo informarle sobre *metadatos o las definiciones de* de sesiones de eventos creados por el usuario en la base de datos actual de Hola. vistas de Hello no devuelven información acerca de las instancias de las sesiones de eventos activos.

| Nombre de<br/>vista de catálogo | Descripción |
|:--- |:--- |
| **sys.database_event_session_actions** |Devuelve una fila por cada acción en cada evento de una sesión de eventos. |
| **sys.database_event_session_events** |Devuelve una fila por cada evento de una sesión de eventos. |
| **sys.database_event_session_fields** |Devuelve una fila por cada columna personalizable que se estableció de forma explícita en los eventos y destinos. |
| **sys.database_event_session_targets** |Devuelve una fila por cada destino de evento de una sesión de eventos. |
| **sys.database_event_sessions** |Devuelve una fila para cada sesión de eventos de base de datos de base de datos SQL de Hola. |

En Microsoft SQL Server, hay vistas de catálogo similares con nombres que incluyen *.server\_* en lugar de *.database\_*. patrón de nombre de Hello es similar a **sys.server_event_%**.

## <a name="new-dynamic-management-views-dmvshttpmsdnmicrosoftcomlibraryms188754aspx"></a>Nuevas vistas de administración dinámica [(DMV)](http://msdn.microsoft.com/library/ms188754.aspx)

Base de datos SQL de Azure tiene [vistas de administración dinámica (DMV)](http://msdn.microsoft.com/library/bb677293.aspx) que admiten eventos extendidos. Las DMV le informan sobre las sesiones de eventos *activas* .

| Nombre de DMV | Descripción |
|:--- |:--- |
| **sys.dm_xe_database_session_event_actions** |Devuelve información acerca de las acciones de la sesión de eventos. |
| **sys.dm_xe_database_session_events** |Devuelve información acerca de los eventos de sesión. |
| **sys.dm_xe_database_session_object_columns** |Muestra los valores de configuración de Hola para los objetos que están enlazados tooa sesión. |
| **sys.dm_xe_database_session_targets** |Devuelve información acerca de los destinos de la sesión. |
| **sys.dm_xe_database_sessions** |Devuelve una fila para cada sesión de eventos es toohello con ámbito de base de datos actual. |

En Microsoft SQL Server, vistas de catálogo similares se denominan sin hello  *\_base de datos* como parte del programa Hola nombre:

- **sys.dm_xe_sessions**, en vez del nombre<br/>**sys.dm_xe_database_sessions**.

### <a name="dmvs-common-tooboth"></a>Tooboth comunes de DMV
Para eventos extendidos son DMV adicionales que son comunes tooboth base de datos de SQL Azure y Microsoft SQL Server:

- **sys.dm_xe_map_values**
- **sys.dm_xe_object_columns**
- **sys.dm_xe_objects**
- **sys.dm_xe_packages**

 <a name="sqlfindseventsactionstargets" id="sqlfindseventsactionstargets"></a>

## <a name="find-hello-available-extended-events-actions-and-targets"></a>Buscar eventos extendidos disponibles de hello, acciones y destinos

Puede ejecutar una simple SQL **seleccione** tooobtain una lista de eventos disponibles de hello, acciones y de destino.

```sql
SELECT
        o.object_type,
        p.name         AS [package_name],
        o.name         AS [db_object_name],
        o.description  AS [db_obj_description]
    FROM
                   sys.dm_xe_objects  AS o
        INNER JOIN sys.dm_xe_packages AS p  ON p.guid = o.package_guid
    WHERE
        o.object_type in
            (
            'action',  'event',  'target'
            )
    ORDER BY
        o.object_type,
        p.name,
        o.name;
```


<a name="AzureXEventsTargets" id="AzureXEventsTargets"></a>&nbsp;

## <a name="targets-for-your-sql-database-event-sessions"></a>Destinos para las sesiones de eventos de Base de datos SQL

Estos son los destinos que pueden capturar los resultados de las sesiones de eventos en Base de datos SQL:

- [Destino de búfer de anillo](http://msdn.microsoft.com/library/ff878182.aspx) : guarda brevemente los datos en la memoria.
- [Destino del contador de eventos de](http://msdn.microsoft.com/library/ff878025.aspx) :cuenta todos los eventos que se producen durante una sesión de eventos extendidos.
- [Destino de archivo de eventos](http://msdn.microsoft.com/library/ff878115.aspx) -contenedor de almacenamiento Azure escribe búferes completos tooan.

Hola [seguimiento de eventos para Windows (ETW)](http://msdn.microsoft.com/library/ms751538.aspx) API no está disponible para eventos extendidos en base de datos SQL.

## <a name="restrictions"></a>Restricciones

Hay un par de diferencias relacionadas con la seguridad y el entorno de nube de Hola de base de datos SQL:

- Eventos extendidos se basan en el modelo de aislamiento de inquilinos solo Hola. Una sesión de eventos en una base de datos no puede tener acceso a datos o eventos desde otra base de datos.
- No se puede emitir un **CREATE EVENT SESSION** instrucción en el contexto de Hola de hello **maestro** base de datos.

## <a name="permission-model"></a>Nombre del permiso

Debe tener **Control** permiso en tooissue de la base de datos de hello un **CREATE EVENT SESSION** instrucción. Hola propietario de base de datos (dbo) tiene **Control** permiso.

### <a name="storage-container-authorizations"></a>Autorizaciones de contenedor de almacenamiento

símbolo (token) SAS de Hello generar para el contenedor de almacenamiento de Azure debe especificar **rwl** para los permisos de Hola. Hola **rwl** valor proporciona Hola los siguientes permisos:

- Lectura
- Escritura
- Enumerar

## <a name="performance-considerations"></a>Consideraciones sobre rendimiento

Existen escenarios donde un uso intensivo de eventos extendidos puede acumular active más memoria que está en buen estado para hello general del sistema. Por lo tanto, Hola sistema de base de datos de SQL Azure establece y ajusta los límites sobre Hola cantidad de memoria activa que se puede acumular por una sesión de eventos. Muchos factores incluyen cálculos dinámicos Hola.

Si recibe un mensaje de error que indica que se aplicó un máximo de memoria, algunas acciones correctivas que puede tomar son:

- Ejecutar menos sesiones de eventos simultáneas.
- A través de su **crear** y **ALTER** instrucciones para las sesiones de eventos, reducir la cantidad de Hola de memoria que se especifique en hello **MAX\_memoria** cláusula.

### <a name="network-latency"></a>Latencia de red

Hola **archivo eventos** destino puede experimentar latencia de red o errores al guardar tooAzure de datos, almacenamiento de blobs. Otros eventos de base de datos de SQL se retrasa mientras esperan a toocomplete de comunicación de red de Hola. Este retraso puede reducir la carga de trabajo.

- toomitigate este rendimiento riesgo, no es necesario establecer hello **EVENT_RETENTION_MODE** opción demasiado**NO_EVENT_LOSS** en sus definiciones de sesión de eventos.

## <a name="related-links"></a>Vínculos relacionados

- [Usar Azure PowerShell con Almacenamiento de Azure](../storage/common/storage-powershell-guide-full.md)
- [Cmdlets del almacenamiento de Azure](http://msdn.microsoft.com/library/dn806401.aspx)
- [Uso de PowerShell de Azure con el almacenamiento de Azure](../storage/common/storage-powershell-guide-full.md) -proporciona información completa sobre hello servicio de almacenamiento de Azure y PowerShell.
- [¿Cómo toouse almacenamiento de blobs en .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md)
- [CREATE CREDENTIAL (Transact-SQL).](http://msdn.microsoft.com/library/ms189522.aspx)
- [CREATE EVENT SESSION (Transact-SQL)](http://msdn.microsoft.com/library/bb677289.aspx)
- [Las publicaciones del blog de Jonathan Kehayias acerca de los eventos extendidos en Microsoft SQL Server](http://www.sqlskills.com/blogs/jonathan/category/extended-events/)


- Hello Azure *las actualizaciones del servicio* página Web, restringido a parámetro tooAzure base de datos SQL:
    - [https://azure.microsoft.com/updates/?service=sql-database](https://azure.microsoft.com/updates/?service=sql-database)


Otros temas de ejemplo de código para eventos extendidos están disponibles en los siguientes vínculos de Hola. Sin embargo, debe comprobar con regularidad cualquier toosee ejemplo si el ejemplo hello tiene como destino de Microsoft SQL Server frente a la base de datos de SQL Azure. A continuación, puede decidir si cambios menores son ejemplo de Hola a toorun necesarios.

<!--
('lock_acquired' event.)

- Code sample for SQL Server: [Determine Which Queries Are Holding Locks](http://msdn.microsoft.com/library/bb677357.aspx)
- Code sample for SQL Server: [Find hello Objects That Have hello Most Locks Taken on Them](http://msdn.microsoft.com/library/bb630355.aspx)
-->
