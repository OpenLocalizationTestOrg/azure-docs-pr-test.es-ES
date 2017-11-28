---
title: Glosario de herramientas de base de datos aaaElastic | Documentos de Microsoft
description: "Explicación de los términos usados en las herramientas de bases de datos elásticas"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: a23a4e81-6706-452d-afc1-a550e5e47af9
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: d6573aad9a097e07135b0a64d1dafec19bb8cc7c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="elastic-database-tools-glossary"></a><span data-ttu-id="3aca3-103">Glosario de las herramientas de bases de datos elásticas</span><span class="sxs-lookup"><span data-stu-id="3aca3-103">Elastic Database tools glossary</span></span>
<span data-ttu-id="3aca3-104">Hello siguientes se definen los términos de hello [herramientas de base de datos elástica](sql-database-elastic-scale-introduction.md), una característica de base de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="3aca3-104">hello following terms are defined for hello [Elastic Database tools](sql-database-elastic-scale-introduction.md), a feature of Azure SQL Database.</span></span> <span data-ttu-id="3aca3-105">Hello herramientas son utilizado toomanage [partición se asigna](sql-database-elastic-scale-shard-map-management.md)e incluyen hello [biblioteca de cliente](sql-database-elastic-database-client-library.md), hello [herramienta Dividir-combinar](sql-database-elastic-scale-overview-split-and-merge.md), [grupos elásticos](sql-database-elastic-pool.md), y [consultas](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3aca3-105">hello tools are used toomanage [shard maps](sql-database-elastic-scale-shard-map-management.md), and include hello [client library](sql-database-elastic-database-client-library.md), hello [split-merge tool](sql-database-elastic-scale-overview-split-and-merge.md), [elastic pools](sql-database-elastic-pool.md), and [queries](sql-database-elastic-query-overview.md).</span></span> 

<span data-ttu-id="3aca3-106">Estos términos se usan en [agregar una partición con herramientas de base de datos elástica](sql-database-elastic-scale-add-a-shard.md) y [con los problemas de asignación de particiones de la clase toofix de hello RecoveryManager](sql-database-elastic-database-recovery-manager.md).</span><span class="sxs-lookup"><span data-stu-id="3aca3-106">These terms are used in [Adding a shard using Elastic Database tools](sql-database-elastic-scale-add-a-shard.md) and [Using hello RecoveryManager class toofix shard map problems](sql-database-elastic-database-recovery-manager.md).</span></span>

![Términos de Escalado elástico][1]

<span data-ttu-id="3aca3-108">**Base de datos**: una base de datos SQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="3aca3-108">**Database**: An Azure SQL database.</span></span> 

<span data-ttu-id="3aca3-109">**Enrutamiento dependiente de datos**: Hola funcionalidad que permite una partición de aplicación tooconnect tooa tiene una clave de particionamiento específica.</span><span class="sxs-lookup"><span data-stu-id="3aca3-109">**Data dependent routing**: hello functionality that enables an application tooconnect tooa shard given a specific sharding key.</span></span> <span data-ttu-id="3aca3-110">Consulte [Enrutamiento dependiente de los datos](sql-database-elastic-scale-data-dependent-routing.md).</span><span class="sxs-lookup"><span data-stu-id="3aca3-110">See [Data dependent routing](sql-database-elastic-scale-data-dependent-routing.md).</span></span> <span data-ttu-id="3aca3-111">Comparar demasiado**[particiones múltiples consultas](sql-database-elastic-scale-multishard-querying.md)**.</span><span class="sxs-lookup"><span data-stu-id="3aca3-111">Compare too**[Multi-Shard Query](sql-database-elastic-scale-multishard-querying.md)**.</span></span>

<span data-ttu-id="3aca3-112">**Mapa de particiones global**: Hola asignación entre las claves de particionamiento y sus respectivos particiones dentro de un **conjunto de particiones**.</span><span class="sxs-lookup"><span data-stu-id="3aca3-112">**Global shard map**: hello map between sharding keys and their respective shards within a **shard set**.</span></span> <span data-ttu-id="3aca3-113">mapa de particiones global de Hola se almacena en hello **manager de mapa de particiones**.</span><span class="sxs-lookup"><span data-stu-id="3aca3-113">hello global shard map is stored in hello **shard map manager**.</span></span> <span data-ttu-id="3aca3-114">Comparar demasiado**mapa de particiones local**.</span><span class="sxs-lookup"><span data-stu-id="3aca3-114">Compare too**local shard map**.</span></span>

<span data-ttu-id="3aca3-115">**Mapa de particiones de lista**: un mapa de particiones en el que las claves de particionamiento se asignan de manera individual.</span><span class="sxs-lookup"><span data-stu-id="3aca3-115">**List shard map**: A shard map in which sharding keys are mapped individually.</span></span> <span data-ttu-id="3aca3-116">Comparar demasiado**mapa de particiones de intervalo**.</span><span class="sxs-lookup"><span data-stu-id="3aca3-116">Compare too**Range Shard Map**.</span></span>   

<span data-ttu-id="3aca3-117">**Mapa de particiones local**: almacenados en una partición, mapa de particiones locales de hello contiene asignaciones para hello shardlets que residen en la partición de Hola.</span><span class="sxs-lookup"><span data-stu-id="3aca3-117">**Local shard map**: Stored on a shard, hello local shard map contains mappings for hello shardlets that reside on hello shard.</span></span>

<span data-ttu-id="3aca3-118">**Consulta de varias particiones**: Hola capacidad tooissue una consulta en varias particiones; se devuelven conjuntos de resultados con UNION ALL semántica (también conocido como "consulta de distribución ramificada").</span><span class="sxs-lookup"><span data-stu-id="3aca3-118">**Multi-shard query**: hello ability tooissue a query against multiple shards; results sets are returned using UNION ALL semantics (also known as “fan-out query”).</span></span> <span data-ttu-id="3aca3-119">Comparar demasiado**enrutamiento dependiente de datos**.</span><span class="sxs-lookup"><span data-stu-id="3aca3-119">Compare too**data dependent routing**.</span></span>

<span data-ttu-id="3aca3-120">**Multiinquilino** e **Inquilino único**: muestra una base de datos de inquilino único y multiinquilino:</span><span class="sxs-lookup"><span data-stu-id="3aca3-120">**Multi-tenant** and **Single-tenant**: This shows a single-tenant database and a multi-tenant database:</span></span>

![Bases de datos de inquilino único y multiinquilino](./media/sql-database-elastic-scale-glossary/multi-single-simple.png)

<span data-ttu-id="3aca3-122">Aquí se muestra una representación de bases de datos de inquilino único y multiinquino **particionadas** .</span><span class="sxs-lookup"><span data-stu-id="3aca3-122">Here is a representation of **sharded** single and multi-tenant databases.</span></span> 

![Bases de datos de inquilino único y multiinquilino](./media/sql-database-elastic-scale-glossary/shards-single-multi.png)

<span data-ttu-id="3aca3-124">**Mapa de particiones de intervalo**: un mapa de particiones en qué Hola estrategia de distribución de la partición se basa en varios intervalos de valores no contiguos.</span><span class="sxs-lookup"><span data-stu-id="3aca3-124">**Range shard map**: A shard map in which hello shard distribution strategy is based on multiple ranges of contiguous values.</span></span> 

<span data-ttu-id="3aca3-125">**Tablas de referencia**: tablas no particionadas, pero que se replican entre particiones.</span><span class="sxs-lookup"><span data-stu-id="3aca3-125">**Reference tables**: Tables that are not sharded but are replicated across shards.</span></span> <span data-ttu-id="3aca3-126">Por ejemplo, los códigos postales se pueden almacenar en una tabla de referencia.</span><span class="sxs-lookup"><span data-stu-id="3aca3-126">For example, zip codes can be stored in a reference table.</span></span> 

<span data-ttu-id="3aca3-127">**Partición**: una base de datos SQL de Azure que almacena datos desde un conjunto de datos particionados.</span><span class="sxs-lookup"><span data-stu-id="3aca3-127">**Shard**: An Azure SQL database that stores data from a sharded data set.</span></span> 

<span data-ttu-id="3aca3-128">**Elasticidad de partición**: Hola tooperform de la capacidad **escalado horizontal** y **escalado vertical**.</span><span class="sxs-lookup"><span data-stu-id="3aca3-128">**Shard elasticity**: hello ability tooperform both **horizontal scaling** and **vertical scaling**.</span></span>

<span data-ttu-id="3aca3-129">**Tablas particionadas**: tablas que se particionan, es decir, cuyos datos se distribuyen entre particiones según sus valores de clave de particionamiento.</span><span class="sxs-lookup"><span data-stu-id="3aca3-129">**Sharded tables**: Tables that are sharded, i.e., whose data is distributed across shards based on their sharding key values.</span></span> 

<span data-ttu-id="3aca3-130">**Clave de particionamiento**: un valor de columna que determina cómo se distribuyen los datos entre particiones.</span><span class="sxs-lookup"><span data-stu-id="3aca3-130">**Sharding key**: A column value that determines how data is distributed across shards.</span></span> <span data-ttu-id="3aca3-131">Hello tipo de valor puede ser uno de hello siguientes: **int**, **bigint**, **varbinary**, o **uniqueidentifier**.</span><span class="sxs-lookup"><span data-stu-id="3aca3-131">hello value type can be one of hello following: **int**, **bigint**, **varbinary**, or **uniqueidentifier**.</span></span> 

<span data-ttu-id="3aca3-132">**Conjunto de particiones**: Hola colección de particiones que son atributos toohello mismo mapa de particiones en el Administrador de mapa de particiones de Hola.</span><span class="sxs-lookup"><span data-stu-id="3aca3-132">**Shard set**: hello collection of shards that are attributed toohello same shard map in hello shard map manager.</span></span>  

<span data-ttu-id="3aca3-133">**Shardlet**: todos los datos de hello asociados con un único valor de una clave de particionamiento en una partición.</span><span class="sxs-lookup"><span data-stu-id="3aca3-133">**Shardlet**: All of hello data associated with a single value of a sharding key on a shard.</span></span> <span data-ttu-id="3aca3-134">Un shardlet es la unidad más pequeña de Hola de movimiento de datos posibles cuando redistribuir tablas particionadas.</span><span class="sxs-lookup"><span data-stu-id="3aca3-134">A shardlet is hello smallest unit of data movement possible when redistributing sharded tables.</span></span> 

<span data-ttu-id="3aca3-135">**Mapa de particiones**: Hola conjunto de asignaciones entre las claves de particionamiento y sus respectivos particiones.</span><span class="sxs-lookup"><span data-stu-id="3aca3-135">**Shard map**: hello set of mappings between sharding keys and their respective shards.</span></span>

<span data-ttu-id="3aca3-136">**Administrador de mapa de particiones**: un almacén de datos y objetos de administración que contenga Hola particiones map(s), ubicaciones de particiones y asignaciones para uno o varios conjuntos de particiones.</span><span class="sxs-lookup"><span data-stu-id="3aca3-136">**Shard map manager**: A management object and data store that contains hello shard map(s), shard locations, and mappings for one or more shard sets.</span></span>

![Asignaciones][2]

## <a name="verbs"></a><span data-ttu-id="3aca3-138">Verbos</span><span class="sxs-lookup"><span data-stu-id="3aca3-138">Verbs</span></span>
<span data-ttu-id="3aca3-139">**Escalado horizontal**: acto de Hola de ajuste de escala (o) una colección de particiones agregando o quitando el mapa de particiones de tooa de particiones, tal y como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="3aca3-139">**Horizontal scaling**: hello act of scaling out (or in) a collection of shards by adding or removing shards tooa shard map, as shown below.</span></span>

![Escalado horizontal y vertical][3]

<span data-ttu-id="3aca3-141">**Mezcla**: acto de Hola de mover shardlets de partición de tooone dos particiones y actualizar el mapa de particiones de hello en consecuencia.</span><span class="sxs-lookup"><span data-stu-id="3aca3-141">**Merge**: hello act of moving shardlets from two shards tooone shard and updating hello shard map accordingly.</span></span>

<span data-ttu-id="3aca3-142">**Movimiento de Shardlets**: acto de Hola de mover una partición diferente de tooa único shardlet.</span><span class="sxs-lookup"><span data-stu-id="3aca3-142">**Shardlet move**: hello act of moving a single shardlet tooa different shard.</span></span> 

<span data-ttu-id="3aca3-143">**Partición**: acto de Hola de partición horizontal de forma idéntica datos estructurados a través de varias bases de datos basadas en una clave de particionamiento.</span><span class="sxs-lookup"><span data-stu-id="3aca3-143">**Shard**: hello act of horizontally partitioning identically structured data across multiple databases based on a sharding key.</span></span>

<span data-ttu-id="3aca3-144">**División**: acto de Hola de mover varios shardlets de partición de una partición tooanother (normalmente nuevo).</span><span class="sxs-lookup"><span data-stu-id="3aca3-144">**Split**: hello act of moving several shardlets from one shard tooanother (typically new) shard.</span></span> <span data-ttu-id="3aca3-145">Una clave de particionamiento proporcionada por usuario de hello como punto de división de Hola.</span><span class="sxs-lookup"><span data-stu-id="3aca3-145">A sharding key is provided by hello user as hello split point.</span></span>

<span data-ttu-id="3aca3-146">**Ajuste de escala vertical**: acto de Hola de ajuste de escala hacia arriba (o hacia abajo) Hola a nivel de rendimiento de una partición individual.</span><span class="sxs-lookup"><span data-stu-id="3aca3-146">**Vertical Scaling**: hello act of scaling up (or down) hello performance level of an individual shard.</span></span> <span data-ttu-id="3aca3-147">Por ejemplo, cambiar una partición de tooPremium estándar (que da lugar a más recursos informáticos).</span><span class="sxs-lookup"><span data-stu-id="3aca3-147">For example, changing a shard from Standard tooPremium (which results in more computing resources).</span></span> 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-glossary/glossary.png
[2]: ./media/sql-database-elastic-scale-glossary/mappings.png
[3]: ./media/sql-database-elastic-scale-glossary/h_versus_vert.png

