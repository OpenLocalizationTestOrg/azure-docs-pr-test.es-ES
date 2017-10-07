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
# <a name="extended-events-in-sql-database"></a><span data-ttu-id="cdbb2-103">Eventos extendidos en Base de datos SQL</span><span class="sxs-lookup"><span data-stu-id="cdbb2-103">Extended events in SQL Database</span></span>
[!INCLUDE [sql-database-xevents-selectors-1-include](../../includes/sql-database-xevents-selectors-1-include.md)]

<span data-ttu-id="cdbb2-104">Este tema explica la implementación de Hola de eventos extendidos en base de datos de SQL Azure es eventos tooextended comparados ligeramente diferente en Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="cdbb2-104">This topic explains how hello implementation of extended events in Azure SQL Database is slightly different compared tooextended events in Microsoft SQL Server.</span></span>

- <span data-ttu-id="cdbb2-105">V12 de base de datos de SQL había obtenido característica eventos extendidos de Hola Hola en segundo lugar la mitad del calendario 2015.</span><span class="sxs-lookup"><span data-stu-id="cdbb2-105">SQL Database V12 gained hello extended events feature in hello second half of calendar 2015.</span></span>
- <span data-ttu-id="cdbb2-106">SQL Server tiene eventos extendidos desde 2008.</span><span class="sxs-lookup"><span data-stu-id="cdbb2-106">SQL Server has had extended events since 2008.</span></span>
- <span data-ttu-id="cdbb2-107">conjunto de características de Hola de eventos extendidos en base de datos SQL es un subconjunto robusto de características de hello en SQL Server.</span><span class="sxs-lookup"><span data-stu-id="cdbb2-107">hello feature set of extended events on SQL Database is a robust subset of hello features on SQL Server.</span></span>

<span data-ttu-id="cdbb2-108">*XEvents* es un sobrenombre informal que a veces se usa para los eventos extendidos en blogs y otras referencias informales.</span><span class="sxs-lookup"><span data-stu-id="cdbb2-108">*XEvents* is an informal nickname that is sometimes used for 'extended events' in blogs and other informal locations.</span></span>

<span data-ttu-id="cdbb2-109">Se puede encontrar información adicional sobre eventos extendidos, para Base de datos SQL de Azure y Microsoft SQL Server, en:</span><span class="sxs-lookup"><span data-stu-id="cdbb2-109">Additional information about extended events, for Azure SQL Database and Microsoft SQL Server, is available at:</span></span>

- [<span data-ttu-id="cdbb2-110">Quick Start: Extended events in SQL Server</span><span class="sxs-lookup"><span data-stu-id="cdbb2-110">Quick Start: Extended events in SQL Server</span></span>](http://msdn.microsoft.com/library/mt733217.aspx)
- [<span data-ttu-id="cdbb2-111">Eventos extendidos</span><span class="sxs-lookup"><span data-stu-id="cdbb2-111">Extended Events</span></span>](http://msdn.microsoft.com/library/bb630282.aspx)

## <a name="prerequisites"></a><span data-ttu-id="cdbb2-112">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="cdbb2-112">Prerequisites</span></span>

<span data-ttu-id="cdbb2-113">En este tema se da por sentado que ya tiene algunos conocimientos sobre:</span><span class="sxs-lookup"><span data-stu-id="cdbb2-113">This topic assumes you already have some knowledge of:</span></span>

- <span data-ttu-id="cdbb2-114">[Servicio Base de datos SQL de Azure](https://azure.microsoft.com/services/sql-database/).</span><span class="sxs-lookup"><span data-stu-id="cdbb2-114">[Azure SQL Database service](https://azure.microsoft.com/services/sql-database/).</span></span>
- <span data-ttu-id="cdbb2-115">[Eventos extendidos](http://msdn.microsoft.com/library/bb630282.aspx) en Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="cdbb2-115">[Extended events](http://msdn.microsoft.com/library/bb630282.aspx) in Microsoft SQL Server.</span></span>

- <span data-ttu-id="cdbb2-116">masiva Hola de nuestra documentación sobre los eventos extendidos aplica tooboth SQL Server y base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="cdbb2-116">hello bulk of our documentation about extended events applies tooboth SQL Server and SQL Database.</span></span>

<span data-ttu-id="cdbb2-117">Toohello de exposición anteriores siguientes elementos es útil cuando se elige el archivo de eventos como Hola Hola [destino](#AzureXEventsTargets):</span><span class="sxs-lookup"><span data-stu-id="cdbb2-117">Prior exposure toohello following items is helpful when choosing hello Event File as hello [target](#AzureXEventsTargets):</span></span>

- [<span data-ttu-id="cdbb2-118">Servicio Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="cdbb2-118">Azure Storage service</span></span>](https://azure.microsoft.com/services/storage/)


- <span data-ttu-id="cdbb2-119">PowerShell</span><span class="sxs-lookup"><span data-stu-id="cdbb2-119">PowerShell</span></span>
    - <span data-ttu-id="cdbb2-120">[Uso de PowerShell de Azure con el almacenamiento de Azure](../storage/common/storage-powershell-guide-full.md) -proporciona información completa sobre hello servicio de almacenamiento de Azure y PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cdbb2-120">[Using Azure PowerShell with Azure Storage](../storage/common/storage-powershell-guide-full.md) - Provides comprehensive information about PowerShell and hello Azure Storage service.</span></span>

## <a name="code-samples"></a><span data-ttu-id="cdbb2-121">Ejemplos de código</span><span class="sxs-lookup"><span data-stu-id="cdbb2-121">Code samples</span></span>

<span data-ttu-id="cdbb2-122">Los temas relacionados proporcionan dos ejemplos de código:</span><span class="sxs-lookup"><span data-stu-id="cdbb2-122">Related topics provide two code samples:</span></span>


- [<span data-ttu-id="cdbb2-123">Código de destino de búfer en anillo para eventos extendidos en Base de datos SQL</span><span class="sxs-lookup"><span data-stu-id="cdbb2-123">Ring Buffer target code for extended events in SQL Database</span></span>](sql-database-xevent-code-ring-buffer.md)
    - <span data-ttu-id="cdbb2-124">Breve script de Transact-SQL simple.</span><span class="sxs-lookup"><span data-stu-id="cdbb2-124">Short simple Transact-SQL script.</span></span>
    - <span data-ttu-id="cdbb2-125">Se resaltan en el tema de ejemplo de código de hello que, cuando haya terminado con un destino de búfer en anillo, debe liberar sus recursos mediante la ejecución de una lista de alter `ALTER EVENT SESSION ... ON DATABASE DROP TARGET ...;` instrucción.</span><span class="sxs-lookup"><span data-stu-id="cdbb2-125">We emphasize in hello code sample topic that, when you are done with a Ring Buffer target, you should release its resources by executing an alter-drop `ALTER EVENT SESSION ... ON DATABASE DROP TARGET ...;` statement.</span></span> <span data-ttu-id="cdbb2-126">Más adelante, puede agregar otra instancia de búfer en anillo de `ALTER EVENT SESSION ... ON DATABASE ADD TARGET ...`.</span><span class="sxs-lookup"><span data-stu-id="cdbb2-126">Later you can add another instance of Ring Buffer by `ALTER EVENT SESSION ... ON DATABASE ADD TARGET ...`.</span></span>


- [<span data-ttu-id="cdbb2-127">Código de destino del archivo de evento para eventos extendidos en Base de datos SQL</span><span class="sxs-lookup"><span data-stu-id="cdbb2-127">Event File target code for extended events in SQL Database</span></span>](sql-database-xevent-code-event-file.md)
    - <span data-ttu-id="cdbb2-128">Fase 1 es PowerShell toocreate un contenedor de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="cdbb2-128">Phase 1 is PowerShell toocreate an Azure Storage container.</span></span>
    - <span data-ttu-id="cdbb2-129">Fase 2 es Transact-SQL que utiliza el contenedor de almacenamiento de Azure de Hola.</span><span class="sxs-lookup"><span data-stu-id="cdbb2-129">Phase 2 is Transact-SQL that uses hello Azure Storage container.</span></span>

## <a name="transact-sql-differences"></a><span data-ttu-id="cdbb2-130">Diferencias de Transact-SQL</span><span class="sxs-lookup"><span data-stu-id="cdbb2-130">Transact-SQL differences</span></span>


- <span data-ttu-id="cdbb2-131">Cuando se ejecuta hello [CREATE EVENT SESSION](http://msdn.microsoft.com/library/bb677289.aspx) de comandos en SQL Server, usar hello **ON SERVER** cláusula.</span><span class="sxs-lookup"><span data-stu-id="cdbb2-131">When you execute hello [CREATE EVENT SESSION](http://msdn.microsoft.com/library/bb677289.aspx) command on SQL Server, you use hello **ON SERVER** clause.</span></span> <span data-ttu-id="cdbb2-132">Pero en la base de datos SQL usar hello **ON DATABASE** cláusula en su lugar.</span><span class="sxs-lookup"><span data-stu-id="cdbb2-132">But on SQL Database you use hello **ON DATABASE** clause instead.</span></span>


- <span data-ttu-id="cdbb2-133">Hola **ON DATABASE** cláusula también aplica toohello [ALTER EVENT SESSION](http://msdn.microsoft.com/library/bb630368.aspx) y [DROP EVENT SESSION](http://msdn.microsoft.com/library/bb630257.aspx) comandos Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="cdbb2-133">hello **ON DATABASE** clause also applies toohello [ALTER EVENT SESSION](http://msdn.microsoft.com/library/bb630368.aspx) and [DROP EVENT SESSION](http://msdn.microsoft.com/library/bb630257.aspx) Transact-SQL commands.</span></span>


- <span data-ttu-id="cdbb2-134">Una práctica recomendada es la opción de sesión de eventos tooinclude Hola de **STARTUP_STATE = ON** en su **CREATE EVENT SESSION** o **ALTER EVENT SESSION** instrucciones.</span><span class="sxs-lookup"><span data-stu-id="cdbb2-134">A best practice is tooinclude hello event session option of **STARTUP_STATE = ON** in your **CREATE EVENT SESSION**  or **ALTER EVENT SESSION** statements.</span></span>
    - <span data-ttu-id="cdbb2-135">Hola **= ON** valor admite un reinicio automático después de volver a configurar una base de datos lógico de hello debido tooa conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="cdbb2-135">hello **= ON** value supports an automatic restart after a reconfiguration of hello logical database due tooa failover.</span></span>

## <a name="new-catalog-views"></a><span data-ttu-id="cdbb2-136">Nuevas vistas de catálogo</span><span class="sxs-lookup"><span data-stu-id="cdbb2-136">New catalog views</span></span>

<span data-ttu-id="cdbb2-137">Hello característica eventos extendidos varias admiten [vistas de catálogo](http://msdn.microsoft.com/library/ms174365.aspx).</span><span class="sxs-lookup"><span data-stu-id="cdbb2-137">hello extended events feature is supported by several [catalog views](http://msdn.microsoft.com/library/ms174365.aspx).</span></span> <span data-ttu-id="cdbb2-138">Vistas de catálogo informarle sobre *metadatos o las definiciones de* de sesiones de eventos creados por el usuario en la base de datos actual de Hola.</span><span class="sxs-lookup"><span data-stu-id="cdbb2-138">Catalog views tell you about *metadata or definitions* of user-created event sessions in hello current database.</span></span> <span data-ttu-id="cdbb2-139">vistas de Hello no devuelven información acerca de las instancias de las sesiones de eventos activos.</span><span class="sxs-lookup"><span data-stu-id="cdbb2-139">hello views do not return information about instances of active event sessions.</span></span>

| <span data-ttu-id="cdbb2-140">Nombre de</span><span class="sxs-lookup"><span data-stu-id="cdbb2-140">Name of</span></span><br/><span data-ttu-id="cdbb2-141">vista de catálogo</span><span class="sxs-lookup"><span data-stu-id="cdbb2-141">catalog view</span></span> | <span data-ttu-id="cdbb2-142">Descripción</span><span class="sxs-lookup"><span data-stu-id="cdbb2-142">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="cdbb2-143">**sys.database_event_session_actions**</span><span class="sxs-lookup"><span data-stu-id="cdbb2-143">**sys.database_event_session_actions**</span></span> |<span data-ttu-id="cdbb2-144">Devuelve una fila por cada acción en cada evento de una sesión de eventos.</span><span class="sxs-lookup"><span data-stu-id="cdbb2-144">Returns a row for each action on each event of an event session.</span></span> |
| <span data-ttu-id="cdbb2-145">**sys.database_event_session_events**</span><span class="sxs-lookup"><span data-stu-id="cdbb2-145">**sys.database_event_session_events**</span></span> |<span data-ttu-id="cdbb2-146">Devuelve una fila por cada evento de una sesión de eventos.</span><span class="sxs-lookup"><span data-stu-id="cdbb2-146">Returns a row for each event in an event session.</span></span> |
| <span data-ttu-id="cdbb2-147">**sys.database_event_session_fields**</span><span class="sxs-lookup"><span data-stu-id="cdbb2-147">**sys.database_event_session_fields**</span></span> |<span data-ttu-id="cdbb2-148">Devuelve una fila por cada columna personalizable que se estableció de forma explícita en los eventos y destinos.</span><span class="sxs-lookup"><span data-stu-id="cdbb2-148">Returns a row for each customize-able column that was explicitly set on events and targets.</span></span> |
| <span data-ttu-id="cdbb2-149">**sys.database_event_session_targets**</span><span class="sxs-lookup"><span data-stu-id="cdbb2-149">**sys.database_event_session_targets**</span></span> |<span data-ttu-id="cdbb2-150">Devuelve una fila por cada destino de evento de una sesión de eventos.</span><span class="sxs-lookup"><span data-stu-id="cdbb2-150">Returns a row for each event target for an event session.</span></span> |
| <span data-ttu-id="cdbb2-151">**sys.database_event_sessions**</span><span class="sxs-lookup"><span data-stu-id="cdbb2-151">**sys.database_event_sessions**</span></span> |<span data-ttu-id="cdbb2-152">Devuelve una fila para cada sesión de eventos de base de datos de base de datos SQL de Hola.</span><span class="sxs-lookup"><span data-stu-id="cdbb2-152">Returns a row for each event session in hello SQL Database database.</span></span> |

<span data-ttu-id="cdbb2-153">En Microsoft SQL Server, hay vistas de catálogo similares con nombres que incluyen *.server\_* en lugar de *.database\_*.</span><span class="sxs-lookup"><span data-stu-id="cdbb2-153">In Microsoft SQL Server, similar catalog views have names that include *.server\_* instead of *.database\_*.</span></span> <span data-ttu-id="cdbb2-154">patrón de nombre de Hello es similar a **sys.server_event_%**.</span><span class="sxs-lookup"><span data-stu-id="cdbb2-154">hello name pattern is like **sys.server_event_%**.</span></span>

## <a name="new-dynamic-management-views-dmvshttpmsdnmicrosoftcomlibraryms188754aspx"></a><span data-ttu-id="cdbb2-155">Nuevas vistas de administración dinámica [(DMV)](http://msdn.microsoft.com/library/ms188754.aspx)</span><span class="sxs-lookup"><span data-stu-id="cdbb2-155">New dynamic management views [(DMVs)](http://msdn.microsoft.com/library/ms188754.aspx)</span></span>

<span data-ttu-id="cdbb2-156">Base de datos SQL de Azure tiene [vistas de administración dinámica (DMV)](http://msdn.microsoft.com/library/bb677293.aspx) que admiten eventos extendidos.</span><span class="sxs-lookup"><span data-stu-id="cdbb2-156">Azure SQL Database has [dynamic management views (DMVs)](http://msdn.microsoft.com/library/bb677293.aspx) that support extended events.</span></span> <span data-ttu-id="cdbb2-157">Las DMV le informan sobre las sesiones de eventos *activas* .</span><span class="sxs-lookup"><span data-stu-id="cdbb2-157">DMVs tell you about *active* event sessions.</span></span>

| <span data-ttu-id="cdbb2-158">Nombre de DMV</span><span class="sxs-lookup"><span data-stu-id="cdbb2-158">Name of DMV</span></span> | <span data-ttu-id="cdbb2-159">Descripción</span><span class="sxs-lookup"><span data-stu-id="cdbb2-159">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="cdbb2-160">**sys.dm_xe_database_session_event_actions**</span><span class="sxs-lookup"><span data-stu-id="cdbb2-160">**sys.dm_xe_database_session_event_actions**</span></span> |<span data-ttu-id="cdbb2-161">Devuelve información acerca de las acciones de la sesión de eventos.</span><span class="sxs-lookup"><span data-stu-id="cdbb2-161">Returns information about event session actions.</span></span> |
| <span data-ttu-id="cdbb2-162">**sys.dm_xe_database_session_events**</span><span class="sxs-lookup"><span data-stu-id="cdbb2-162">**sys.dm_xe_database_session_events**</span></span> |<span data-ttu-id="cdbb2-163">Devuelve información acerca de los eventos de sesión.</span><span class="sxs-lookup"><span data-stu-id="cdbb2-163">Returns information about session events.</span></span> |
| <span data-ttu-id="cdbb2-164">**sys.dm_xe_database_session_object_columns**</span><span class="sxs-lookup"><span data-stu-id="cdbb2-164">**sys.dm_xe_database_session_object_columns**</span></span> |<span data-ttu-id="cdbb2-165">Muestra los valores de configuración de Hola para los objetos que están enlazados tooa sesión.</span><span class="sxs-lookup"><span data-stu-id="cdbb2-165">Shows hello configuration values for objects that are bound tooa session.</span></span> |
| <span data-ttu-id="cdbb2-166">**sys.dm_xe_database_session_targets**</span><span class="sxs-lookup"><span data-stu-id="cdbb2-166">**sys.dm_xe_database_session_targets**</span></span> |<span data-ttu-id="cdbb2-167">Devuelve información acerca de los destinos de la sesión.</span><span class="sxs-lookup"><span data-stu-id="cdbb2-167">Returns information about session targets.</span></span> |
| <span data-ttu-id="cdbb2-168">**sys.dm_xe_database_sessions**</span><span class="sxs-lookup"><span data-stu-id="cdbb2-168">**sys.dm_xe_database_sessions**</span></span> |<span data-ttu-id="cdbb2-169">Devuelve una fila para cada sesión de eventos es toohello con ámbito de base de datos actual.</span><span class="sxs-lookup"><span data-stu-id="cdbb2-169">Returns a row for each event session that is scoped toohello current database.</span></span> |

<span data-ttu-id="cdbb2-170">En Microsoft SQL Server, vistas de catálogo similares se denominan sin hello  *\_base de datos* como parte del programa Hola nombre:</span><span class="sxs-lookup"><span data-stu-id="cdbb2-170">In Microsoft SQL Server, similar catalog views are named without hello *\_database* portion of hello name, such as:</span></span>

- <span data-ttu-id="cdbb2-171">**sys.dm_xe_sessions**, en vez del nombre</span><span class="sxs-lookup"><span data-stu-id="cdbb2-171">**sys.dm_xe_sessions**, instead of name</span></span><br/><span data-ttu-id="cdbb2-172">**sys.dm_xe_database_sessions**.</span><span class="sxs-lookup"><span data-stu-id="cdbb2-172">**sys.dm_xe_database_sessions**.</span></span>

### <a name="dmvs-common-tooboth"></a><span data-ttu-id="cdbb2-173">Tooboth comunes de DMV</span><span class="sxs-lookup"><span data-stu-id="cdbb2-173">DMVs common tooboth</span></span>
<span data-ttu-id="cdbb2-174">Para eventos extendidos son DMV adicionales que son comunes tooboth base de datos de SQL Azure y Microsoft SQL Server:</span><span class="sxs-lookup"><span data-stu-id="cdbb2-174">For extended events there are additional DMVs that are common tooboth Azure SQL Database and Microsoft SQL Server:</span></span>

- <span data-ttu-id="cdbb2-175">**sys.dm_xe_map_values**</span><span class="sxs-lookup"><span data-stu-id="cdbb2-175">**sys.dm_xe_map_values**</span></span>
- <span data-ttu-id="cdbb2-176">**sys.dm_xe_object_columns**</span><span class="sxs-lookup"><span data-stu-id="cdbb2-176">**sys.dm_xe_object_columns**</span></span>
- <span data-ttu-id="cdbb2-177">**sys.dm_xe_objects**</span><span class="sxs-lookup"><span data-stu-id="cdbb2-177">**sys.dm_xe_objects**</span></span>
- <span data-ttu-id="cdbb2-178">**sys.dm_xe_packages**</span><span class="sxs-lookup"><span data-stu-id="cdbb2-178">**sys.dm_xe_packages**</span></span>

 <a name="sqlfindseventsactionstargets" id="sqlfindseventsactionstargets"></a>

## <a name="find-hello-available-extended-events-actions-and-targets"></a><span data-ttu-id="cdbb2-179">Buscar eventos extendidos disponibles de hello, acciones y destinos</span><span class="sxs-lookup"><span data-stu-id="cdbb2-179">Find hello available extended events, actions, and targets</span></span>

<span data-ttu-id="cdbb2-180">Puede ejecutar una simple SQL **seleccione** tooobtain una lista de eventos disponibles de hello, acciones y de destino.</span><span class="sxs-lookup"><span data-stu-id="cdbb2-180">You can run a simple SQL **SELECT** tooobtain a list of hello available events, actions, and target.</span></span>

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


<span data-ttu-id="cdbb2-181"><a name="AzureXEventsTargets" id="AzureXEventsTargets"></a>&nbsp;</span><span class="sxs-lookup"><span data-stu-id="cdbb2-181"><a name="AzureXEventsTargets" id="AzureXEventsTargets"></a> &nbsp;</span></span>

## <a name="targets-for-your-sql-database-event-sessions"></a><span data-ttu-id="cdbb2-182">Destinos para las sesiones de eventos de Base de datos SQL</span><span class="sxs-lookup"><span data-stu-id="cdbb2-182">Targets for your SQL Database event sessions</span></span>

<span data-ttu-id="cdbb2-183">Estos son los destinos que pueden capturar los resultados de las sesiones de eventos en Base de datos SQL:</span><span class="sxs-lookup"><span data-stu-id="cdbb2-183">Here are targets that can capture results from your event sessions on SQL Database:</span></span>

- <span data-ttu-id="cdbb2-184">[Destino de búfer de anillo](http://msdn.microsoft.com/library/ff878182.aspx) : guarda brevemente los datos en la memoria.</span><span class="sxs-lookup"><span data-stu-id="cdbb2-184">[Ring Buffer target](http://msdn.microsoft.com/library/ff878182.aspx) - Briefly holds event data in memory.</span></span>
- <span data-ttu-id="cdbb2-185">[Destino del contador de eventos de](http://msdn.microsoft.com/library/ff878025.aspx) :cuenta todos los eventos que se producen durante una sesión de eventos extendidos.</span><span class="sxs-lookup"><span data-stu-id="cdbb2-185">[Event Counter target](http://msdn.microsoft.com/library/ff878025.aspx) - Counts all events that occur during an extended events session.</span></span>
- <span data-ttu-id="cdbb2-186">[Destino de archivo de eventos](http://msdn.microsoft.com/library/ff878115.aspx) -contenedor de almacenamiento Azure escribe búferes completos tooan.</span><span class="sxs-lookup"><span data-stu-id="cdbb2-186">[Event File target](http://msdn.microsoft.com/library/ff878115.aspx) - Writes complete buffers tooan Azure Storage container.</span></span>

<span data-ttu-id="cdbb2-187">Hola [seguimiento de eventos para Windows (ETW)](http://msdn.microsoft.com/library/ms751538.aspx) API no está disponible para eventos extendidos en base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="cdbb2-187">hello [Event Tracing for Windows (ETW)](http://msdn.microsoft.com/library/ms751538.aspx) API is not available for extended events on SQL Database.</span></span>

## <a name="restrictions"></a><span data-ttu-id="cdbb2-188">Restricciones</span><span class="sxs-lookup"><span data-stu-id="cdbb2-188">Restrictions</span></span>

<span data-ttu-id="cdbb2-189">Hay un par de diferencias relacionadas con la seguridad y el entorno de nube de Hola de base de datos SQL:</span><span class="sxs-lookup"><span data-stu-id="cdbb2-189">There are a couple of security-related differences befitting hello cloud environment of SQL Database:</span></span>

- <span data-ttu-id="cdbb2-190">Eventos extendidos se basan en el modelo de aislamiento de inquilinos solo Hola.</span><span class="sxs-lookup"><span data-stu-id="cdbb2-190">Extended events are founded on hello single-tenant isolation model.</span></span> <span data-ttu-id="cdbb2-191">Una sesión de eventos en una base de datos no puede tener acceso a datos o eventos desde otra base de datos.</span><span class="sxs-lookup"><span data-stu-id="cdbb2-191">An event session in one database cannot access data or events from another database.</span></span>
- <span data-ttu-id="cdbb2-192">No se puede emitir un **CREATE EVENT SESSION** instrucción en el contexto de Hola de hello **maestro** base de datos.</span><span class="sxs-lookup"><span data-stu-id="cdbb2-192">You cannot issue a **CREATE EVENT SESSION** statement in hello context of hello **master** database.</span></span>

## <a name="permission-model"></a><span data-ttu-id="cdbb2-193">Nombre del permiso</span><span class="sxs-lookup"><span data-stu-id="cdbb2-193">Permission model</span></span>

<span data-ttu-id="cdbb2-194">Debe tener **Control** permiso en tooissue de la base de datos de hello un **CREATE EVENT SESSION** instrucción.</span><span class="sxs-lookup"><span data-stu-id="cdbb2-194">You must have **Control** permission on hello database tooissue a **CREATE EVENT SESSION** statement.</span></span> <span data-ttu-id="cdbb2-195">Hola propietario de base de datos (dbo) tiene **Control** permiso.</span><span class="sxs-lookup"><span data-stu-id="cdbb2-195">hello database owner (dbo) has **Control** permission.</span></span>

### <a name="storage-container-authorizations"></a><span data-ttu-id="cdbb2-196">Autorizaciones de contenedor de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="cdbb2-196">Storage container authorizations</span></span>

<span data-ttu-id="cdbb2-197">símbolo (token) SAS de Hello generar para el contenedor de almacenamiento de Azure debe especificar **rwl** para los permisos de Hola.</span><span class="sxs-lookup"><span data-stu-id="cdbb2-197">hello SAS token you generate for your Azure Storage container must specify **rwl** for hello permissions.</span></span> <span data-ttu-id="cdbb2-198">Hola **rwl** valor proporciona Hola los siguientes permisos:</span><span class="sxs-lookup"><span data-stu-id="cdbb2-198">hello **rwl** value provides hello following permissions:</span></span>

- <span data-ttu-id="cdbb2-199">Lectura</span><span class="sxs-lookup"><span data-stu-id="cdbb2-199">Read</span></span>
- <span data-ttu-id="cdbb2-200">Escritura</span><span class="sxs-lookup"><span data-stu-id="cdbb2-200">Write</span></span>
- <span data-ttu-id="cdbb2-201">Enumerar</span><span class="sxs-lookup"><span data-stu-id="cdbb2-201">List</span></span>

## <a name="performance-considerations"></a><span data-ttu-id="cdbb2-202">Consideraciones sobre rendimiento</span><span class="sxs-lookup"><span data-stu-id="cdbb2-202">Performance considerations</span></span>

<span data-ttu-id="cdbb2-203">Existen escenarios donde un uso intensivo de eventos extendidos puede acumular active más memoria que está en buen estado para hello general del sistema.</span><span class="sxs-lookup"><span data-stu-id="cdbb2-203">There are scenarios where intensive use of extended events can accumulate more active memory than is healthy for hello overall system.</span></span> <span data-ttu-id="cdbb2-204">Por lo tanto, Hola sistema de base de datos de SQL Azure establece y ajusta los límites sobre Hola cantidad de memoria activa que se puede acumular por una sesión de eventos.</span><span class="sxs-lookup"><span data-stu-id="cdbb2-204">Therefore hello Azure SQL Database system dynamically sets and adjusts limits on hello amount of active memory that can be accumulated by an event session.</span></span> <span data-ttu-id="cdbb2-205">Muchos factores incluyen cálculos dinámicos Hola.</span><span class="sxs-lookup"><span data-stu-id="cdbb2-205">Many factors go into hello dynamic calculation.</span></span>

<span data-ttu-id="cdbb2-206">Si recibe un mensaje de error que indica que se aplicó un máximo de memoria, algunas acciones correctivas que puede tomar son:</span><span class="sxs-lookup"><span data-stu-id="cdbb2-206">If you receive an error message that says a memory maximum was enforced, some corrective actions you can take are:</span></span>

- <span data-ttu-id="cdbb2-207">Ejecutar menos sesiones de eventos simultáneas.</span><span class="sxs-lookup"><span data-stu-id="cdbb2-207">Run fewer concurrent event sessions.</span></span>
- <span data-ttu-id="cdbb2-208">A través de su **crear** y **ALTER** instrucciones para las sesiones de eventos, reducir la cantidad de Hola de memoria que se especifique en hello **MAX\_memoria** cláusula.</span><span class="sxs-lookup"><span data-stu-id="cdbb2-208">Through your **CREATE** and **ALTER** statements for event sessions, reduce hello amount of memory you specify on hello **MAX\_MEMORY** clause.</span></span>

### <a name="network-latency"></a><span data-ttu-id="cdbb2-209">Latencia de red</span><span class="sxs-lookup"><span data-stu-id="cdbb2-209">Network latency</span></span>

<span data-ttu-id="cdbb2-210">Hola **archivo eventos** destino puede experimentar latencia de red o errores al guardar tooAzure de datos, almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="cdbb2-210">hello **Event File** target might experience network latency or failures while persisting data tooAzure Storage blobs.</span></span> <span data-ttu-id="cdbb2-211">Otros eventos de base de datos de SQL se retrasa mientras esperan a toocomplete de comunicación de red de Hola.</span><span class="sxs-lookup"><span data-stu-id="cdbb2-211">Other events in SQL Database might be delayed while they wait for hello network communication toocomplete.</span></span> <span data-ttu-id="cdbb2-212">Este retraso puede reducir la carga de trabajo.</span><span class="sxs-lookup"><span data-stu-id="cdbb2-212">This delay can slow your workload.</span></span>

- <span data-ttu-id="cdbb2-213">toomitigate este rendimiento riesgo, no es necesario establecer hello **EVENT_RETENTION_MODE** opción demasiado**NO_EVENT_LOSS** en sus definiciones de sesión de eventos.</span><span class="sxs-lookup"><span data-stu-id="cdbb2-213">toomitigate this performance risk, avoid setting hello **EVENT_RETENTION_MODE** option too**NO_EVENT_LOSS** in your event session definitions.</span></span>

## <a name="related-links"></a><span data-ttu-id="cdbb2-214">Vínculos relacionados</span><span class="sxs-lookup"><span data-stu-id="cdbb2-214">Related links</span></span>

- <span data-ttu-id="cdbb2-215">[Usar Azure PowerShell con Almacenamiento de Azure](../storage/common/storage-powershell-guide-full.md)</span><span class="sxs-lookup"><span data-stu-id="cdbb2-215">[Using Azure PowerShell with Azure Storage](../storage/common/storage-powershell-guide-full.md).</span></span>
- [<span data-ttu-id="cdbb2-216">Cmdlets del almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="cdbb2-216">Azure Storage Cmdlets</span></span>](http://msdn.microsoft.com/library/dn806401.aspx)
- <span data-ttu-id="cdbb2-217">[Uso de PowerShell de Azure con el almacenamiento de Azure](../storage/common/storage-powershell-guide-full.md) -proporciona información completa sobre hello servicio de almacenamiento de Azure y PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cdbb2-217">[Using Azure PowerShell with Azure Storage](../storage/common/storage-powershell-guide-full.md) - Provides comprehensive information about PowerShell and hello Azure Storage service.</span></span>
- [<span data-ttu-id="cdbb2-218">¿Cómo toouse almacenamiento de blobs en .NET</span><span class="sxs-lookup"><span data-stu-id="cdbb2-218">How toouse Blob storage from .NET</span></span>](../storage/blobs/storage-dotnet-how-to-use-blobs.md)
- [<span data-ttu-id="cdbb2-219">CREATE CREDENTIAL (Transact-SQL).</span><span class="sxs-lookup"><span data-stu-id="cdbb2-219">CREATE CREDENTIAL (Transact-SQL)</span></span>](http://msdn.microsoft.com/library/ms189522.aspx)
- [<span data-ttu-id="cdbb2-220">CREATE EVENT SESSION (Transact-SQL)</span><span class="sxs-lookup"><span data-stu-id="cdbb2-220">CREATE EVENT SESSION (Transact-SQL)</span></span>](http://msdn.microsoft.com/library/bb677289.aspx)
- [<span data-ttu-id="cdbb2-221">Las publicaciones del blog de Jonathan Kehayias acerca de los eventos extendidos en Microsoft SQL Server</span><span class="sxs-lookup"><span data-stu-id="cdbb2-221">Jonathan Kehayias' blog posts about extended events in Microsoft SQL Server</span></span>](http://www.sqlskills.com/blogs/jonathan/category/extended-events/)


- <span data-ttu-id="cdbb2-222">Hello Azure *las actualizaciones del servicio* página Web, restringido a parámetro tooAzure base de datos SQL:</span><span class="sxs-lookup"><span data-stu-id="cdbb2-222">hello Azure *Service Updates* webpage, narrowed by parameter tooAzure SQL Database:</span></span>
    - [<span data-ttu-id="cdbb2-223">https://azure.microsoft.com/updates/?service=sql-database</span><span class="sxs-lookup"><span data-stu-id="cdbb2-223">https://azure.microsoft.com/updates/?service=sql-database</span></span>](https://azure.microsoft.com/updates/?service=sql-database)


<span data-ttu-id="cdbb2-224">Otros temas de ejemplo de código para eventos extendidos están disponibles en los siguientes vínculos de Hola.</span><span class="sxs-lookup"><span data-stu-id="cdbb2-224">Other code sample topics for extended events are available at hello following links.</span></span> <span data-ttu-id="cdbb2-225">Sin embargo, debe comprobar con regularidad cualquier toosee ejemplo si el ejemplo hello tiene como destino de Microsoft SQL Server frente a la base de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="cdbb2-225">However, you must routinely check any sample toosee whether hello sample targets Microsoft SQL Server versus Azure SQL Database.</span></span> <span data-ttu-id="cdbb2-226">A continuación, puede decidir si cambios menores son ejemplo de Hola a toorun necesarios.</span><span class="sxs-lookup"><span data-stu-id="cdbb2-226">Then you can decide whether minor changes are needed toorun hello sample.</span></span>

<!--
('lock_acquired' event.)

- Code sample for SQL Server: [Determine Which Queries Are Holding Locks](http://msdn.microsoft.com/library/bb677357.aspx)
- Code sample for SQL Server: [Find hello Objects That Have hello Most Locks Taken on Them](http://msdn.microsoft.com/library/bb630355.aspx)
-->
